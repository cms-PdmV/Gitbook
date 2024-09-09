---
description: >-
  In this page, we collect useful information for Monte Carlo contacts about how
  to act in McM
---

# Status of requests in computing

**acquired**: request has been split by the global WorkQueue into work element, but no work element has been injected into the local WorkQueue.

**running-open**: at least 1 work element injected into local WorkQueue, jobs are created running.

**running-closed**: all work elements are in running state.

Computing offers many tools to monitor the status of a request in central production (please see [here](https://monte-carlo-production-tools.gitbook.io/project/monte-carlo-production-overview)). In order to understand at which stage of production requests are, two main things need to be monitored:

* Status in RequestManager page
* Status in Unified

For additional information, one can consult the Log of a request or the ErrorReport. All these features can be accessed by the camera button in McM (see again [here](https://monte-carlo-production-tools.gitbook.io/project/monte-carlo-production-overview)), where the following page will open up (example):

*

![Example of monitoring page. One can see the Log button, the ErrorReport, and the status in ReqMgr page and Unified.](<../.gitbook/assets/image (3).png>)

## Status of requests in RequestManager page

![](<../.gitbook/assets/image (23).png>)

Below is the explanation of the status of requests in computing:

**assignment-approved**: will be moved to assigned in the next Unified cycle if the campaign is enabled.

**force-completed**: set by users/operators to kill all remaining work and move to completed status.

**completed**: all work elements are done.

**rejected**: invalid at assignment or produced output is not satisfactory.

**failed**: has failure in one of the work elements.

**closed-out**: output is ready to be announced.

**aborted**: set by users/operators to kill all current jobs, run only auxiliary tasks and move to aborted-completed status.

**staging**: waiting for input data to be transferred to disk.

**staged**: workflow ready to be assigned.away: workflow set to assigned in ReqMgr.

**close**: synchronising with closed-out, all output satisfactory.

**assistance**: all jobs are finished with produced output less than threshold due to job failures. “assistance” status is usually accompanied by one or more keywords (see next page).

## IMPORTANT PARAMETERS FOR PRODUCTION

Unified and ReqMgr split events per job based on **TimePerEvent** and **SizePerEvent** with the following constraints:

**announced**: request has been announced to the requestors.

## Status of requests in Unified

![](<../.gitbook/assets/image (4).png>)

Below is the explanation of the status of requests in Unified:

**considered**: workflow obtained from request manager, will move to the next state if campaign is enabled.

If TimePerEvent and SizePerEvent are not close to the true value, jobs will exceed the limit and fail.

## MOST COMMON REASONS FOR WORKFLOWS NOT (YET) RUNNING / GETTING ANNOUNCED

[Link to computing tutorial](https://indico.cern.ch/event/674156/contributions/2796716/attachments/1569722/2475537/McMTutorial.pdf)



* Maximize number of events per job to maintain CPU efficiency.&#x20;
* Each job finishes within 8 hours.&#x20;
* Total output size for each job is less than (20 GB \* Ncores)

Same for **Memory**: jobs use more memory than requested will fail. Wrong Memory requirement will make job run at improper sites and fail.&#x20;

* Waiting for input dataset to be transferred on disk.
* Low priority.
* Workflows have errors and need to be handled by operators.
* Workflows have long running tails.

## Useful links:

[Unified assistance page](https://cms-unified.web.cern.ch/cms-unified/assistance.html)

[JIRA page](https://its.cern.ch/jira/issues/)

[wmStats](https://cmsweb.cern.ch/wmstats/index.html) (live status of a workflow)
