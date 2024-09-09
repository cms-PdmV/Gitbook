# Requests

### Introduction

Requests are the main objects in the machine. Each request represent a single or multiple cmsDriver.py commands that are called a "sequences" as well as hold some metadata. Requests are the units of work that will be submitted to computing as jobs.

### Request status

#### Statuses

Unlike other objects in ReReco machine, requests have multiple different statuses. They are (in order):

* New - this is request's initial state. Most of the attributes can be edited or the request itself can be deleted. Request can also have it's "Options reset"
* Approved - this "freezes" request values and acts as a last step before submission to computing. If request has another request as input, output dataset is taken from input request and set as input dataset of the request
* Submitting - request is either in queue to be submitted or is currently being submitted (running `cmsDriver.py` and uploading JobDict to ReqMgr2). Whether it is in the queue or being submitted can be seen in the Dashboard
* Submitted - request was submitted for production in computing. Workflows (requests in ReqMgr2) can be seen in "Workflows" column
* Done - request successfully ran in computing and finished. Workflows are in `announced` or `normal-archived` status and all output datasets are in `VALID` status. There are no subsequent steps

#### Moving to next status ("Next" button)

* New -> approved - if input is set to a request X, output dataset of request X will be set as input dataset
* Approved -> submitting - puts request in submission queue that can be seen in the Dashboard
* Submitted -> done - can be either moved by user or by periodic script when last workflow is `announced` or `normal-archived` and output datasets are `VALID`

#### Moving to previous status ("Previous" button)

* Approved -> new - sets status to new
* Submitted -> approved - rejects workflows in ReqMgr2, resets total events and completed events to 0 and clears ConfigCacheID in the sequences. Output datasets are NOT invalidated
* Done -> new - moves request to approved and then back to new status, same actions as Submitted -> approved -> new are performed

### Getting runs and lumisection ranges

It is possible to automatically fetch list of runs and lumisection ranges in request editing page.

!["Get runs" and "Get lumisections" buttons](<../.gitbook/assets/Screenshot from 2021-06-08 20-05-13.png>)

"Get runs" will fetch all runs of input dataset and, if subcampaign's Runs JSON path is set, will intersect them with runs in the Runs JSON file. If subcampaign does not have Runs JSON path set, all runs of input dataset will be used. List of runs will appear in "Runs" field.

If subcampaign's Runs JSON path is set, "Get lumisections" will take list of runs of "Runs" field and intersect them with Runs JSON file and return lumisection ranges from the Runs JSON file. If subcampaign's Runs JSON path is not set, empty dictionary of lumisection ranges will be returned. If "Runs" field was edited and has different runs than what would be returned by "Get runs", specified runs will be used for the intersection, even if they do not appear in the input dataset.&#x20;

This will be automatically done when requests are created from the ticket.

### Request submission

If request has only one sequence, it will be submitted with `RequestType` set to`ReReco` and the whole workflow would represent a single task.

If request has more than one sequence, it will be submitted with `RequestType` set to `TaskChain` and each sequence will appear as a `Task` in the Job Dictionary.

If request has lumisections specified, Job Dictionary will include them as `LumiList` attribute. Otherwise, if \[no lumisections, but] request has a list of runs, they will be submitted as `RunWhitelist`. If both lumisection and runs values are empty, neither will be added to Job Dictionary.

### Request priority

Request's priority can be changed at any time before it is done.

If request is submitted, priority change in editing page will also change workflow priority in the ReqMgr2.

If priority is changed directly in ReqMgr2 or somewhere else outside the ReReco machine, it will be updated in the machine during the next update from Stats2.

### Picking input dataset

If request "B" has request "A" as input, ReReco machine will try to automatically pick output dataset of "A" to use as input for "B". It checks if first datatier of first sequence of "B" is present in `datatier_mapping` setting. If it is, list of datatiers are used to find corresponding output dataset in "A". Datatier list in `datatier_mapping` is in decreasing priority. For example, if mapping is `{"AAA": ["FOO", "BAR"]}` and first datatier of "B" is "AAA", then ReReco machine will try to find output dataset `/.../.../FOO` in "A", if it does not exist, it'll look for `/.../.../BAR`.

If attempt above does not yield an input dataset, last output dataset of "A" is picked.

`datatier_mapping` setting can be found here: [https://cms-pdmv.cern.ch/rereco/api/settings/get/datatier\_mapping](https://cms-pdmv.cern.ch/rereco/api/settings/get/datatier\_mapping)

### Job dict overwrite

**WARNING:** this is an expert feature that allows unsupervised/unchecked edit, use with great caution. Incorrect use might lead to misconfigured jobs.

ReReco machine allows each request to have it's own "Job dict overwrite" JSON which is a way to customize automatically built Job dict. This enables, for example, to change SCRAM architecture of submitted job, add BlockWhitelist, RequestString, URLs, etc. The dictionary specified here will be "applied on top" of the built job dict, for example `{"ScramArch": "slc7_ppc64le_gcc9"}` will overwrite global ScramArch to  "`slc7_ppc64le_gcc9`".  If only one attribute of the nested dictionary needs changing, this supports dot notation to reach them, e.g. `{"Task1.ScramArch": "slc7_ppc64le_gcc9"}` will overwrite Task1's ScramArch. Note that `{"Task1": {"ScramArch": "slc7_ppc64le_gcc9"}}` would overwrite the whole Task1 with a dictionary that has only a ScramArch attribute.

Make sure to double check the Job dict before submission if Job dict overwrite is used. This is indicated by a red exclamation mark next to "Job dict" button.

### Request attributes

* PrepID (`prepid`) - unique identifier of the request
* CMSSW release (`cmssw_release`) - CMSSW Release that will be used to generate configs and run the job
* Completed events (`completed_events`) - number of events of the last output dataset that were produced so far
* Enable harvesting (`enable_harvesting`) - whether to automatically add HARVESTING step if there is a sequence with DQM `--step`
* Energy (`energy`) - energy in TeV
* History (`history`) - history of actions performed on the request, such as creation, submission or editing. Each entry includes date, user username, action and value
* Input (`input`) - input can be either request or dataset. If input is another request, then the value is it's prepid, if input is a dataset, then it's dataset name
* Job dict overwrite (`job_dict_overwrite`) - a JSON that will be applied to built Job dict. This is an expert feature and should be used with great caution
* Lumisections (`lumisections`) - dictionary of runs as keys and lumisection ranges as values
* Memory (`memory`) - memory in MB, to be provided to computing
* Notes (`notes`) - free-form user text
* Output datasets (`output_datasets`) - list of output datasets fetched from Stats2 (ReqMgr2)
* Priority (`priority`) - request priority, to be provided to computing during submission. If this is changed when request is submitted , new priority will be set in ReqMgr2 too
* Processing string (`processing_string`) - processing string of the request
* Runs (`runs`) - list of runs to be processed. If Lumisections is not empty, runs will not be included in the Job Dict
* Sequences (`sequences`) - list of sequences (`cmsDriver.py` commands and their attributes)
* Size per event (`size_per_event`) - list of size per event values (same number of values as sequences) to be provided to computing, each size per event corresponds to one sequence
* Status (`status`) - request status
* Subcampaign (`subcampaign`) - subcampaign that request is member of
* Time per event (`time_per_event`) - list of time per event values (same number of values as sequences) to be provided to computing, each time per event corresponds to one sequence
* Total events (`total_events`) - number of expected to be processed events, fetched from Stats2 (ReqMgr2)
* Workflows (`workflows`) - list of workflows in computing and their output datasets

### Request actions

* Edit - open editing page of the request
* Delete - delete this request. Requests can be deleted only if their status is "new"
* Clone - open a form to create a new request and prefill form fields with info of given request
* cmsDriver - open a simple-text page with CMSSW environment setup and `cmsDriver.py` commands of the request
* Job dict - open a simple-text page that contains the JSON that will be/is submitted to the ReqMgr2. Red exclamation mark indicates that Job dictionary has custom overwrites
* Previous - move request to previous status
* Next - move request to next status
* Create ticket - (only at the bottom, when multiple requests are selected) open Ticket creation form with selected requests placed as Input
* Option reset - available only when request is in "new" status, this overwrites request's memory, sequences and energy with ones from the subcampaign (for example, if subcampaign was updated after request was created)
* Update from Stats2 - manually pull workflow information from Stats2
* Stats2 - open Stats2 page with all workflows of the request
