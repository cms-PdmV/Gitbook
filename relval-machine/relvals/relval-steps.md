# RelVal steps

### Introduction

RelVal step represents a single cmsDriver.py command.

### RelVal step type

RelVal step can be one of two types - driver step or input file \[dataset] step.

### Lumisection and run whitelist

Input step can have a whitelist that specifies either lumisections or runs that should be processed. Step has both attributes -  `lumisection` and `run`, but machine first checks if lumisections are specified. If they are specified, lumisection ranges are submitted as `LumiList` attribute in job dict. If they are not specified, machine checks if runs are specified. If they are, they are submitted as `RunWhitelist`.&#x20;

### RelVal step attributes

* Step name (`name`) - step name
* CMSSW release (`cmssw_release`) - CMSSW release name or an absolute path to the public directory with CMSSW release to be used when generating config for the step
* Config ID (`config_id`) - hash of configuration file uploaded to ReqMgr2
* cmsDriver as step (`driver`), all attributes correspond to the cmsDriver arguments:
  * `beamspot`
  * `conditions`
  * `customise`
  * `customise_commands`
  * `data`
  * `datatier`
  * `era`
  * `eventcontent`
  * `extra`
  * `fast`
  * `filetype`
  * `geometry`
  * `hltProcess`
  * `mc`
  * `number`
  * `nStreams`
  * `pileup`
  * `pileup_input`
  * `process`
  * `relval`
  * `runUnscheduled`
  * `fragment_name`
  * `scenario`
  * `step`
* Events per lumi (`events_per_lumi`) - events per lumisection, if empty, events per job will be used
* GPU (`gpu.requires`) - indicate whether GPU parameters should be added to Job Dict. Possible values: `forbidden`, `optional`, `required`
* GPU Parameters (more info: [https://github.com/dmwm/WMCore/wiki/GPU-Support#gpu-parameter-specification](https://github.com/dmwm/WMCore/wiki/GPU-Support#gpu-parameter-specification)):
  * GPU Memory (`gpu.gpu_memory`) - memory in MB
  * CUDA Capabilities (`gpu.cuda_capabilities`) - comma separated values
  * CUDA Runtime (`gpu.cuda_runtime`) - ?
  * GPU Name (`gpu.gpu_name`) - ?
  * CUDA Driver Version (`gpu.cuda_driver_version`) - ?
  * CUDA Runtime Version (`gpu.cuda_runtime_version`) - ?
* Input dataset as step (`input`):
  * Dataset (`dataset`) - input dataset name
  * Lumisection (`lumisection`) - dictionary (JSON) of run numbers and lumisection ranges
  * Label (`label`) - input step label, if RelVal has any steps with `data` set to True, this will be used in the request string and processing string
  * Run (`run`) - list of runs as run white list
* Keep output (`keep_output`) - whether to keep output of this task, default True
* Lumis per job (`lumis_per_job`) - lumis per job, applicable only to non-first steps
* Resolved globaltag (`resolved_globaltag`) - actual globaltag, resolved from auto:... conditions
* SCRAM Arch (`scram_arch`) - if specified, overwrite scram arch of the RelVal, if empty, use  arch of the RelVal
