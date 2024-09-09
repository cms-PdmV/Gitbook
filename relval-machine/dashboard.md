# Dashboard

### Submission threads

A single RelVal submission might take up to 5 minutes, so they are done in RelVal machine's background threads, called workers. Workers are independent of user presence, so if user pushes RelVal to status `submitting` and immediately goes offline, RelVal will still be submitted by these background workers. Otherwise submission would rely on user and RelVal machine having an active connection for each RelVal while it is being submitted.

In the Dashboard, "Submission threads" shows current size and occupancy of the submission worker pool. Pool size is dynamic and can expand to concurrent 15 threads or shrink to 0, depending on amount of RelVals to be submitted.

![Two RelVals being submitted and no RelVals waiting in the queue](<../.gitbook/assets/Screenshot from 2021-07-21 13-56-44.png>)

### Submission queue

Submission queue shows list of PrepIDs of RelVals that are waiting to be submitted.
