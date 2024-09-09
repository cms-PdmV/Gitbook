# RelVals

### Introduction

RelVals are the main objects in the machine. Each RelVal usually holds multiple RelVal Steps - `cmsDriver.py` commands. In addition, RelVals have attributes like job priority, notes, list of output datasets, batch name, etc. RelVals are objects that will be submitted to computing as independent TaskChain jobs with RelVal Steps as Tasks inside them.

### RelVal status

#### Statuses

Unlike tickets, RelVals have quite a few statuses. Statuses (in order):

* New - this is RelVal's initial state. Most of the attributes can be edited or the RelVal itself can be deleted
* Approved - this "freezes" RelVal values and acts as last step before submission to computing. In this status "auto:" conditions are already resolved to global tags (refer to Resolving "auto:" conditions section)
* Submitting - RelVal is either in a queue to be submitted or is currently being submitted (running `cmsDriver.py` and uploading Job Dictionary to ReqMgr2). Whether it is in the queue or being worked on can be seen in the Dashboard
* Submitted - RelVal was submitted for production in computing. Computing workflows (requests in ReqMgr2) can be seen in "Workflows (jobs in ReqMgr2)" column
* Done - RelVal successfully ran in computing and finished workflows have `completed` in their status history and all output datasets are in `VALID` status. There are no subsequent steps
* Archived - RelVal was submitted and was archived (`normal-archived`, `rejected-archived` or `aborted-archived`) for some time by computing \["done" in computing side], but not all datasets are not `VALID`, most likely due to issues in production. There are no subsequent steps

#### Moving to next status ("Next" button)

* New -> approved - during status change "auto:" conditions are resolved to global tags (refer to Resolving "auto:" conditions section)
* Approved -> submitting - RelVal machine checks if input dataset (if any) and `pileup_input` dataset (if any) (of all RelVal steps) statuses are `VALID`. RelVal is also assigned a campaign timestamp (refer to Campaign name). Finally, if required datasets are `VALID`, RelVal is put in submission queue that can be seen in the Dashboard
* Submitted -> done - can be either moved by user or by periodic script when last workflow has `completed` in it's status history and all output datasets are `VALID`
* Submitted -> archived - can be either moved by user or by periodic script when last workflow has been in archived status for some time, but not all output datasets are `VALID`&#x20;

#### Moving to previous status ("Previous" button)

* Approved -> new - resolved "auto:" conditions are removed from each step
* Submitted -> approved - submitted workflows are rejected in ReqMgr2, ConfigCacheID cleared in steps, campaign timestamp is unset. Output datasets are NOT invalidated
* Done -> new - moves RelVal to approved and then back to new status, same actions as Submitted -> approved -> new are performed
* Archived -> new - same as "Done -> new"

### Resolving "auto:" conditions

Job Dictionary that is submitted to ReqMgr2 requires RelVal machine to provide a "GlobalTag" for each step (Task in TaskChain). However, RelVals usually do not have actual global tags, but values such as   `auto:run2_mc` or `auto:run3_data_express` as step `--conditions`. This is no problem for `cmsDriver.py` as it knows how to resolve `auto:...` conditions to actual global tags, however RelVal machine has to explicitly "resolve" them before submission. That is why, when RelVal is moved from status "new" to "approved", RelVal machine checks out required CMSSW version and "resolves" these `auto:...` conditions - `--conditions` of each step - to actual global tags.

RelVal machine uses a custom built script - [resolve\_auto\_global\_tag.py](https://github.com/cms-PdmV/RelVal/blob/master/core/utils/resolve\_auto\_global\_tag.py) to do the resolving. It uses `autoCond` dictionary from [this file](https://github.com/cms-sw/cmssw/blob/master/Configuration/AlCa/python/autoCond.py) from appropriate release.

### RequestString and ProcessingString

Both RequestString and ProcessingString share a common suffix.

#### Suffix

Suffix is built from multiple parts that are joined by an underscore `_` in the end. Parts:

* If RelVal has non-empty label, it is added as a part
* If RelVal's matrix is "generator", a `gen` part is added
* If any of the RelVal steps have `--fast` option set, `FastSim` is added as part
* If RelVal's first step is input file and at any of the steps have `--data` option set, then `RelVal_{first_step_label}` is added as part

Suffix format with parts wrapped in square brackets: `[{relval_label}_][gen_][FastSim_][RelVal_{first_step_label}]`

Leading or trailing underscores are stripped.

#### RequestString

Request string is built from letters `RV`, release name, RelVal name and suffix. RelVal name is the `workflow_name` if it exists or name of the first step otherwise.

RequestString format: `RV{cmssw_release}{relval_name}__{suffix}`&#x20;

If RequestString is longer than 72 characters, it is truncated by removing part after the last underscore. This is repeated until there are no underscores left of RequestString is not longer than 72 characters. This is due to 100 character limit on workflow name in ReqMgr2.

#### ProcessingString

Processing string is generated for each step individually. It is made of GlobalTag (that had to be resolved), optional PU prefix and a suffix.

ProcessingString format: `{pu_prefix}{resolved_globaltag}_{suffix}`

* If step has `pileup_input` set and `premix_stage2` in it's `extra` field then PU prefix is `PUpmx_`
* Otherwise, if step has `pileup_inpu` set then PU prefix is `PU_`&#x20;
* Otherwise PU prefix is not set

### Campaign name during RelVal submission

For every bunch of similar RelVals, a new campaign is automatically opened in computing. Once all RelVals in that campaign are done, that campaign is automatically closed and a new one will be created the next time. Campaign name is made of CMSSW release of RelVals, their batch name and a timestamp.

Unlike original `runTheMatrix.py`, RelVal machine tries to submit similar RelVals to the same campaign even if they are not submitted at exactly the same second. When RelVal is moved to `submitting` step, RelVal machine assigns a "campaign timestamp" (UNIX timestamp - value of seconds since 1970 January 1st) (and a campaign name) to it. In order to get campaign timestamp of a RelVal, machine queries a database for RelVals that have same CMSSW release and batch name **and** were submitted within last hour (3600 seconds). If such RelVals exist, their campaign timestamp is reused and RelVal goes to the same campaign as already submitted RelVals. If such RelVals do not exist, a new campaign timestamp of current time is assigned and other RelVals might reuse it.

For example: RelVal1 release is `CMSSW_12_0_0` and batch name `XYZ`. RelVal2 and RelVal3 have the same release and same batch name. When RelVal1 is submitted, RelVal machine looks for RelVals with `CMSSW_12_0_0` and batch name `XYZ` submitted within last hour. Since there are none, current timestamp, e.g. `1000` is assigned and RelVal is submitted to campaign `CMSSW_12_0_0__XYZ-1000`. 10 minutes later, RelVal2 is being submitted. Machine finds RelVal1 as submitted RelVal with same release and batch name as well as it was less than an hour ago. RelVal2 gets `1000` as campaign timestamp and is submitted to the `CMSSW_12_0_0__XYZ-1000` campaign. If RelVal2 submission fails, it can be retried for the next 50 minutes and still get into the same campaign. RelVal3 is submitted 2 hours after RelVal1 submission. RelVal3 will get `8200` campaign timestamp, 1000 + 2 \* 3600 = 8200 and will be submitted to campaign named `CMSSW_12_0_0__XYZ-8200`.

Timestamp reuse for up to an hour allows to fix failed submission and still submit to the same campaign.

### Job dict overwrite

**WARNING:** this is an expert feature that allows unsupervised/unchecked edit, use with great caution. Incorrect use might lead to misconfigured jobs.

RelVal machine allows each relval to have it's own "Job dict overwrite" JSON which is a way to customize automatically built Job dict. This enables, for example, to change SCRAM architecture of submitted job, add BlockWhitelist, RequestString, URLs, etc. The dictionary specified here will be "applied on top" of the built job dict, for example `{"ScramArch": "slc7_ppc64le_gcc9"}` will overwrite global ScramArch to  "`slc7_ppc64le_gcc9`".  If only one attribute of the nested dictionary needs changing, this supports dot notation to reach them, e.g. `{"Task1.ScramArch": "slc7_ppc64le_gcc9"}` will overwrite Task1's ScramArch. Note that `{"Task1": {"ScramArch": "slc7_ppc64le_gcc9"}}` would overwrite the whole Task1 with a dictionary that has only a ScramArch attribute.

Make sure to double check the Job dict before submission if Job dict overwrite is used. This is indicated by a red exclamation mark next to "Job dict" button.

### RelVal attributes

* PrepID (`prepid`) - unique identifier of the RelVal
* Batch name (`batch_name`) - batch name that will be used in RelVal campaign name
* Campaign timestamp (`campaign_timestamp`) - timestamp that will be used in the campaign name
* CMSSW release (`cmssw_release`) - CMSSW release or an absolute path to the public directory with CMSSW release of the RelVal
* CPU cores (`cpu_cores`) - number of CPU cores to be used in production, to be passed to computing
* Fragment (`fragment`) - custom fragment for the first step
* History (`history`) - history of actions performed on the request, such as creation, submission or editing. Each entry includes date, user username, action and value
* Job dict overwrite (`job_dict_overwrite`) - a JSON that will be applied to built Job dict. This is an expert feature and should be used with great caution
* Label (`label`) - label used in RequestString and ProcessingString
* Matrix (`matrix`) - matrix of the RelVal, `standard`, `upgrade`, `generator`, etc.
* Memory (`memory`) - memory in MB, to be passed to computing&#x20;
* Notes (`notes`) - free-form user text
* Output datasets (`output_datasets`) - list of output datasets fetched from Stats2
* Sample tag (`sample_tag`) - tag to group similar tickets together
* SCRAM arch (`scram_arch`) - overwrite default SCRAM arch of the RelVal release, if empty use default arch of the release
* Size per event (`size_per_event`) - size per event value in kilobytes, same value will be set for each step
* Status (`status`) - RelVal status
* Steps (`steps`) - list of RelVal steps (`cmsDriver.py` commands)
* Time per event (`time_per_event`) - time per event value in seconds, same value will be set for each step
* Workflow ID (`workflow_id`) - workflow ID number which was used to create the RelVal
* Workflow name (`workflow_name`) - RelVal name if available, otherwise name of the first step
* Workflows (jobs in ReqMgr2) (`workflows`) - list of workflows (jobs) in computing and their output datasets

### RelVal actions

* Edit - open editing page of the RelVal
* Delete -  delete this RelVal. RelVals can be deleted only if their status is "new"
* Clone -  open a form to create a new RelVal and prefill form fields with info of given RelVal
* cmsDriver - open a simple-text page with CMSSW environment setup and `cmsDriver.py` commands of all RelVal steps
* Job dict - open a simple-text page that contains the JSON that will be/is submitted to the ReqMgr2. Red exclamation mark indicates that Job dictionary has custom overwrites
* Config upload - open a simple-text page that contains the bash script used to upload configs to ReqMgr2 config cache
* Previous - move RelVal to previous status
* Next - move RelVal to next status
* Update from Stats2 - manually pull ReqMgr2 workflow information from Stats2&#x20;
* Stats2 - open Stats2 page with all workflows of the RelVal
