# "Dead" requests and tickets

### Introduction

McM has a script that periodically goes over all `submitted` requests and checks how are they doing. This script runs twice per day. There are a couple of primitive metrics that are checked whether request is progressing or not. If it appears that request is having problems or is stuck, it is tagged with one of three tags: "Dead", "StatusNew" or "StatusAssistance-Manual". Reason for why it was tagged is added to the request's `Notes`.

Added tags are same, simple tags that users tag requests with, so they can be used while searching for requests in McM, pMp or GrASP.

If request is no longer problematic, it will have the tag automatically removed during next script run. Please note that fixed request does not immediately get the tag removed, this is done during the next script run which might be as far as 12h away. pMp and GrASP also need time to synchronize with McM.&#x20;

### Requests tagged "Dead"

pMp link: [https://cms-pdmv.cern.ch/pmp/present?r=Dead\&groupBy=\&colorBy=pwg](https://cms-pdmv.cern.ch/pmp/present?r=Dead\&groupBy=\&colorBy=pwg)

This is the broadest tag of all. Requests can be tagged `Dead` for one of the following reasons:

* &#x20;If newest workflow of request is in status `rejected`, `aborted`, `rejected-archived` or `aborted-archived` for more than 30 days
  * Explanation and solution: request was rejected/aborted on computing side, but is still `submitted` in McM. Request(s) in McM should be reset back to new and deleted or resubmitted after solving problems which caused the workflow to be rejected/aborted
* If newest workflow of request is in status `normal-archived` for more than 5 days
  * Explanation and solution: this usually means that workflow is finished and is "archived", but output dataset(s) are not yet in `VALID` status, but (probably) stuck in `PRODUCTION` status. Solution would be to nicely ask operators on computing side "_if there is a reason why these datasets are still in PRODUCTION status_". More often than not computing will manually trigger datasets to become `VALID` and request in McM will become `done` and lose the `Dead` tag
* If newest workflow did not change it's status for more than 365 days
  * Explanation and solution: this means that nothing happened for a year which means either the priority is too low or there are other problems. These cases do not have a common answer, each should be investigated individually

The best place to start fixing a `Dead` request is to read the request's `Notes` to see why and when it was pronounced dead and then inspect request's workflows in Stats: [https://cms-pdmv.cern.ch/stats/](https://cms-pdmv.cern.ch/stats/) (paste request PrepID in the search bar and click "Search").

![Example of a "normal-archived" workflow with output dataset still being in PRODUCTION status ](<../.gitbook/assets/Screenshot from 2021-10-19 11-38-03.png>)

![Example of workflow and it's](<../.gitbook/assets/Screenshot from 2021-10-19 11-38-39.png>)

### Requests tagged "StatusNew"

pMp link: [https://cms-pdmv.cern.ch/pmp/present?r=StatusNew\&groupBy=\&colorBy=pwg](https://cms-pdmv.cern.ch/pmp/present?r=StatusNew\&groupBy=\&colorBy=pwg)

Requests are tagged `StatusNew` when their workflow is in status `new` for more than 5 days. This can happen either because batches were not yet announced (in this case tag should be ignored) or that batch announcement failed and workflow has to be manually put to `assignment-approved` in ReqMgr2.

### Requests tagged "StatusAssistance-Manual"

pMp link: [https://cms-pdmv.cern.ch/pmp/present?r=StatusAssistance-Manual\&status=submitted\&groupBy=\&colorBy=pwg](https://cms-pdmv.cern.ch/pmp/present?r=StatusAssistance-Manual\&status=submitted\&groupBy=\&colorBy=pwg)

Requests are tagged `StatusAssistance-Manual` if their workflow is in `assistance-manual` status in computing. Status in computing is taken from here: [http://cms-unified.web.cern.ch/cms-unified/public/statuses.json](http://cms-unified.web.cern.ch/cms-unified/public/statuses.json)

There is no universal answer for this status, best place to start looking for answers is CMSUnified logs. CMSUnified logs for the workflow can be reached by clicking "CMSUnified" link in Stats.&#x20;

### Automatic deletion of abandoned tickets

Tickets that are in status `new` and last action in their history is more than 100 days ago are automatically deleted.

Users who acted on the ticket receive a notification email 5 days before deletion.
