# Dashboard

### Submission threads

A single Request submission might take up to 10 minutes, so they are done in ReReco machine's background threads, called workers. Workers are independent of user presence, so if user pushes request to status `submitting` and immediately goes offline, request will still be submitted by these background workers. Otherwise submission would rely on user and ReReco machine having an active connection for each Request while it is being submitted.

In the Dashboard, "Submission threads" shows current size and occupancy of the submission worker pool. Pool size is dynamic and can expand to concurrent 15 threads or shrink to 0, depending on amount of Requests to be submitted.

![Two Requests being submitted and no Requests waiting in the queue](<.gitbook/assets/Screenshot from 2021-05-12 18-08-50.png>)

### Submission queue

Submission queue shows list of PrepIDs of Requests that are waiting to be submitted.
