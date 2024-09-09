# Monitoring submitted requests

In order to monitor a request in McM, one should first of all look at the status of the request:

* done status means the sample has been produced and is announced and available in DAS
* submitted status means the sample is in process (can already have events available in DAS but not yet in status VALID)
* new/validation/defined/approved status means that the sample is NOT running

By clicking the camera button for a request, the specific monitoring page of the request opens up and looks like the following:

![](<../.gitbook/assets/image (21).png>)

![Camera button ](<../.gitbook/assets/image (18).png>)

The monitoring page shows the list of output datasets along with the number of events already produced (they can be run over in CRAB).

By looking at the column ReqMgr status, one can have access at the status of the request in computing:

* running-open/running-closed: request is running
* completed: the wf is completed (dataset can be either announced or resubmitted for completing the missing statistics)
* rejected/assignment-approved/acquired: request is NOT running

## Monitoring requests from pMp:

pMp is developed to monitor the progress and statistics of Monte Carlo requests, flows, campaigns and workflows using their prepIDs in 3 view options:

• Present: total events or requests for the specific searched items, there are multiple options to modify plot’s logic using the available selections.

• Historical: Shows expected, current and done events over time, and a list of submitted requests with their progress.

• Performance: Shows total time taken by a request to go from one status to another.

In order to see the progress of a request/group of request, one should go to:

{% embed url="https://cms-pdmv.cern.ch/pmp/" %}

and click "Historical". By adding the prep-id of a request or the tag, or the campaign name, one can see the number of events processed as a function of time (Example: [https://cms-pdmv.cern.ch/pmp/historical?r=B2G-RunIIAutumn18DRPremix-00003](https://cms-pdmv.cern.ch/pmp/historical?r=B2G-RunIIAutumn18DRPremix-00003))
