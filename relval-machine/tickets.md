# Tickets

### Introduction

Tickets are the way to easily create a set of RelVals in with a certain release and same metadata like number of CPU cores. Ticket itself is a one-use-only object - when ticket is created, it can be then used to create RelVals and after that it is there only for the bookkeeping purposes. If new RelVals need to be created, a new ticket must be created. Three fundamental ingredients for a ticket are CMSSW release name, matrix name (standard, upgrade, generator, etc.) and list of workflow IDs.

A ticket can be seen as the runTheMatrix.py command - a single instance creates and submits multiple RelVals with identical metadata. Most of ticket attributes directly represent runTheMatrix.py arguments.

Note: RelVal machine **DOES NOT** use runTheMatrix.py itself, but uses same source of information - RelVal matrices. RelVal machine uses alternative script - [run\_the\_matrix\_pdmv.py](https://github.com/cms-PdmV/RelVal/blob/master/core/utils/run\_the\_matrix\_pdmv.py) - to dump the cmsDriver arguments from CMSSW.

### Creating RelVals

#### Workflow IDs to cmsDriver arguments

Workflow IDs are converted to actual cmsDriver.py commands using matrices in CMSSW. CMSSW release specified in the ticket will be used to get these matrices, so some wokflows IDs might not be present in some releases.

There are a multiple matrices available, e.g. `standard`, `upgrade`, `generator`, etc. Based on chosen matrix in a ticket, appropriate file will be used to fetch workflow steps from workflow IDs. These files [are available here](https://github.com/cms-sw/cmssw/tree/master/Configuration/PyReleaseValidation/python). If matrix is `standard`, then `relval_standard.py` file will be used to fetch workflows, if it's `upgrade`, then `relval_upgrade.py`, etc.

Once workflow's list of step names is fetched from the matrix file, [this file](https://github.com/cms-sw/cmssw/blob/master/Configuration/PyReleaseValidation/python/relval\_steps.py) is used to convert step names to actual cmsDriver arguments. These arguments are then downloaded to RelVal machine and used to generate RelVal objects.

All of this is done in lxplus by checking out the ticket's CMSSW release and then running [run\_the\_matrix\_pdmv.py](https://github.com/cms-PdmV/RelVal/blob/master/core/utils/run\_the\_matrix\_pdmv.py) script to dump the info. This happens in the background and is not visible to the user.

#### Recycle GS

If Recycle GS option is selected, RelVal run\_the\_matrix\_pdmv.py will add `INPUT` suffix to first step name of each workflow and will try to fetch the step with `INPUT` in the name. For example if step names of a workflow are as follows: `RunMuonEG2018B`, `HLTDR2_2018`, `RECODR2_2018reHLT`, `HARVEST2018` then script will try to fetch steps with these names: `RunMuonEG2018BINPUT`, `HLTDR2_2018`, `RECODR2_2018reHLT`, `HARVEST2018`.

#### Recycle input of ...

"Recycle input of" field allows to specify a RelVal step which should have its input recycled. This enables users to recycle steps that are not recyclable with "Recycle GS" options (i.e. HIN workflows) or to recycle steps further down the pipeline, for example to recycle DIGI and run RECO-only RelVals. If it is specified, RelVal machine \[when creating relvals from ticket] will fetch workflow info from appropriate matrix as usual, but then remove all the RelVal steps before the specified step while keeping in memory last removed step. For example if "Recycle input of" has `DIGI`, all RelVal steps before DIGI will be removed and `GEN-SIM` will be kept in memory as a "step to be recycled", if it's `RECO`, all RelVal steps up to RECO will be removed and `DIGI` will be kept in memory as "step to be recycled". RelVal machine will try to find an existing dataset that was already produced by "step to be recycled". Dataset's name will be built based on RelVal name, CMSSW release, processing string and datatier. Datatier will be the last `--datatier` specified in "step to be recycled". If multiple versions of the dataset will be found, newest one will be used.

If "Rewrite GT string" is also specified, it will be used instead of the CMSSW release and processing string while looking for a dataset to be recycled.

If "Recycle GS" is checked, it will be ignored and recycling will be based only on "Recycle input of" logic.

Example: ticket's release is `CMSSW_12_0_0`, workflow's name is `TTbar_14TeV`, step to "Recycle input of" is `RECO`. When creating the RelVal, GEN-SIM and DIGI steps will be removed and replaced with a recycled dataset of DIGI step as input for the RECO step. `auto:` conditions will be automatically resolved to a GT. Recycled dataset will be queried with (note the \* for dataset version): `/RelValTTbar_14TeV/CMSSW_12_0_0-113X_mcRun4_realistic_v7-v*/GEN-SIM-DIGI-RAW`. Datatier is`GEN-SIM-DIGI-RAW` because the last (and only) `--datatier` of the DIGI step is `GEN-SIM-DIGI-RAW`. If the "Rewrite GT string" was specified, e.g. `ABCD`, the query would have looked like `RelValTTbar_14TeV/ABCD/GEN-SIM-DIGI-RAW`.

#### Rewrite GT string

If Rewrite GT string field is not empty, it will be used to overwrite the middle part of input dataset (if it exists) and middle part of `pileup_input` of each step (if it exists). There is a small logic difference when changing input dataset and pileup dataset:

* For input dataset, the middle part is replaced with as-is Rewrite GT value, e.g. if Rewrite GT string value is `AABBCC`, and input dataset is `/PrimaryDS/EraGlobalTagPS/DATATIER` then it will be changed to `/PrimaryDS/AABBCC/DATATIER.`
* For pileup dataset, `PU_` is removed from Rewrite GT value first (if it was there) and only then middle part is replaced with this vale, e.g. if Rewrite GT string value is `A-PU_BBBCCC` and `pileup_input` is `/PrimaryDS/EraGlobalTagPS/DATATIER` then it will be changed to `/PrimaryDS/A-BBBCCC/DATATIER` and newest version of `/PrimaryDS/A-BBBCCC-vX/DATATIER` will be fetched and used, where X is the version.

This feature is useful when globaltag specified in RelVal steps file is not up to date and would have to be changed for each created RelVal.

#### Overriding default SCRAM arch

When setting up CMSSW environment to run `run_the_matrix_pdmv.py` RelVal machine will use default SCRAM arch of the CMSSW release specified in the ticket. Default SCRAM arch for each release can be found here: [https://cmssdt.cern.ch/SDT/cgi-bin/ReleasesXML?anytype=1](https://cmssdt.cern.ch/SDT/cgi-bin/ReleasesXML?anytype=1).&#x20;

It is possible to override this default SCRAM arch lookup by specifying a SCRAM arch in the "SCRAM arch" field. If the field is empty, default value will be used. If field is not empty, specified value will be used when setting up the environment.

Example: if ticket CMSSW release is set to `CMSSW_12_0_0_pre4` and SCRAM arch field is empty, then `slc7_amd64_gcc900` will be used. However, if there is a need to use different SCRAM arch, e.g. `slc7_amd64_gcc10` then this can be achieved by putting `slc7_amd64_gcc10` in ticket's SCRAM arch field.

SCRAM arch value (either specified or empty field) will be propagated to all created RelVals.

### Ticket attributes

* PrepID (`prepid`) - unique identifier of the ticket
* Batch name (`batch_name`) - batch name that will be propagated to each created RelVal
* CMSSW release (`cmssw_release`) - CMSSW release name or an absolute path to the public directory that will be used to generate RelVals and that will be propagated to created RelVals
* Command (`command`) - additional string that will be added to all cmsDrivers commands of created RelVals&#x20;
* Command steps (`command_steps`) - list of `--step` values that indicate which RelVal steps should get the Command (`command`) applied, e.g. `GEN,SIM,DIGI` . If empty, Command will be applied to all steps
* CPU cores (`cpu_cores`) - number of CPU cores that will be propagated to all created RelVals
* Created RelVals (`created_relvals`) - list of PrepIDs of RelVals that were created from this ticket&#x20;
* Events factor (`events_factor`) - factor by which number of events in `--relval` argument will be multiplied
* GPU (`gpu.requires`) - indicate whether GPU should be added to RelVal steps. Steps can be indicated in "GPU Steps" field. Possible values: `forbidden`, `optional`, `required`
* GPU Parameters (more info: [https://github.com/dmwm/WMCore/wiki/GPU-Support#gpu-parameter-specification](https://github.com/dmwm/WMCore/wiki/GPU-Support#gpu-parameter-specification)):
  * GPU Memory (`gpu.gpu_memory`) - memory in MB
  * CUDA Capabilities (`gpu.cuda_capabilities`) - comma separated values
  * CUDA Runtime (`gpu.cuda_runtime`) - ?
  * GPU Name (`gpu.gpu_name`) - ?
  * CUDA Driver Version (`gpu.cuda_driver_version`) - ?
  * CUDA Runtime Version (`gpu.cuda_runtime_version`) - ?
* GPU Steps (`gpu_steps`) - list of `--step` values that indicate which RelVal steps should get the GPU and GPU Parameters applied, e.g. `HLT`. If empty and GPU is not `forbidden`, GPU and GPU Parameters will be applie to all steps
* History (`history`) - history of actions performed on the ticket, such as creation or editing. Each entry includes date, user username, action and value
* Label (`label`) - label that will be propagated to each created RelVal
* Matrix (`matrix`) - type of relval: standard, upgrade, premix, etc.
* Memory (`memory`) - memory in MB to be provided to computing
* Notes (`notes`) - free-form user text
* nStreams (`n_streams`) - number of streams to be used in all steps of created RelVals, 0 defaults to nThreads
* Recycle GS (`recycle_gs`) - flag indicating whether to try and recycle first step by looking for a RelVal step with INPUT suffix
* Rewrite GT string (`rewrite_gt_string`) - if specified, this string will be used to rewrite middle part of input dataset and `pileup_input` of created RelVals - /.../THIS\_PART/...
* Sample tag (`sample_tag`) - tag to group similar tickets together
* SCRAM Arch (`scram_arch`) - if specified, overwrite default scram arch of release with this value and propagate it to all created RelVals
* Status (`status`) - ticket status: new or done
* Workflow IDs (`workflow_ids`) - list of workflow ids that specify which RelVals will be created from the ticket

### Ticket actions

* Edit - open editing page of the ticket
* Delete - delete the ticket. This is allowed only if it is new or if all RelVals, that were created from the ticket are deleted. If the created RelVals are present, they have to be deleted first
* Clone - open a form to create a new ticket and prefill form fields with info of given ticket
* Create RelVals - create RelVals of each workflow id and apply settings present in the ticket
* Show RelVals - show RelVals that were created from the ticket
* List for RelMon - show a list of ReqMgr2 workflow names of submitted requests that can be pasted to RelMon Service
* runTheMatrix.py - get runTheMatrix.py command that tries to reflect the ticket as good as possible
