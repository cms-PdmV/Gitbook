# Sequences (cmsDriver.py)

### Introduction

Sequence represents a single cmsDriver.py command.

### Harvesting

If sequence has a `DQM` step and parent object has Enable Harvesting set to true, additional harvesting step (cmsDriver.py) will be created. If `DQM` step has additional specification in a form of `--step DQM:XYZ`, harvesting step will have the same format - `--step HARVESTING:XYZ`.

### ALCA/SKIM steps

If sequence has `ALCA` or `SKIM` step that do not have additional specification, i.e. not `ALCA:XYZ` and not `SKIM:ABC`, but are just `ALCA` and/or `SKIM` then these steps will have `:@Dataset` added (where `{Dataset}` is the primary dataset of the request) if primary dataset is present in `AlCaRecoMatrix` dictionary in`Configuration.AlCa.autoAlca` and `autoSkim` dictionary in `Configuration.Skimming.autoSkim` respectively. If primary dataset is not in the mentioned dictionaries, step will be removed completely.

For example, request's primary dataset is `HLTPhysics` and steps in sequence are like this `--step ALCA,SKIM`. Then, if `HLTPhysics` is present in `AlCaRecoMatrix` dictionary, `ALCA` step will become `ALCA:@HLTPhysics` and if `HLTPhysics` is in `autoSkim` dictionary, `SKIM` will become `SKIM:@HLTPhysics`. In the end it will look like `--step ALCA:@HLTPhysics,SKIM:@HLTPhysics`.

If these steps already have specification as `:ABC`, they will be left as is, e.g. `--step ALCA:AAA` will be kept as `--step ALCA:AAA`.

### Sequence attributes

* Conditions (`conditions`) - cmsDriver.py argument `--conditions`
* Customise (`customise`) - cmsDriver.py argument `--customise`
* Datatier (`datatier`) - cmsDriver.py argument `--datatier`, list of comma separated datatiers
* Era (`era`) - cmsDriver.py argument `--era`
* Eventcontent (`eventcontent`) - cmsDriver.py argument `--eventcontent`, list of comma separated event contents
* Extra (`extra`) - additional arguments that will be added to the end of built cmsDriver command, e.g. `--runUnscheduled` or `--data`
* GPU (`gpu.requires`) - indicate whether GPU parameters should be added to Job Dict. Possible values: forbidden, optional, required
* GPU parameters (more info: [https://github.com/dmwm/WMCore/wiki/GPU-Support#gpu-parameter-specification](https://github.com/dmwm/WMCore/wiki/GPU-Support#gpu-parameter-specification)):
  * GPU memory (`gpu.gpu_memory`) - memory in MB
  * CUDA capabilities (`gpu.cuda_capabilities`) - comma separated values
  * CUDA runtime (`gpu.cuda_runtime`) - ?
  * GPU name (`gpu.gpu_name`) - ?
  * CUDA driver version (`gpu.cuda_driver_version`) - ?
  * CUDA runtime version (`gpu.cuda_runtime_version`) - ?
* nThreads (`nThreads`) - cmsDriver.py argument `--nThreads`, number of CPU cores to use in production
* Scenario (`scenario`) - cmsDriver.py argument `--scenario`, one of predefined values: `pp`, `cosmics`, `nocoll` or `HeavyIons`
* Step (`step`) - cmsDriver.py argument `--step`, list of comma separated steps
