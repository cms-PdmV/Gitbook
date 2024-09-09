---
description: In this page, we give a description of icons and features of flows in McM
---

# McM glossary: flows

### What is a flow?

A flow is used to connect two campaigns between each other, so that the next campaign uses as input the output dataset of the previous campaign. While the cmsDriver of a request is defined at the campaign level, a flow can be used to modify some of the arguments of the cmsDriver for specific cases (e.g. pileup scenario, saved datatier, etc.)

In the following, the different entries needed for the defintion of a flow are explained.

### Allowed campaigns&#x20;

Are the campaign the flow can start from.

### Next campaign&#x20;

Is the campaign the flow is going into.

### Approval&#x20;

Has various action depending on its value:

* **none** - request of this flow will not be created
* **flow** - request of this flow will be automatically created, but will remain in status "none-new"
* **submit** - request of this flow will be automatically created and pushed into "approve-approved" status and also submitted to computing (only one request)
* **tasksubmit** - request of this flow will be automatically created, pushed in "approve-approved" status and also submitted to computing. If two or more requests are connected with tasksubmit, they will be submitted as a single chain (preferred way)

For example:\
GS Campaign -> flowDR + DR Campaign -> flowMini + MiniAOD Campaign -> flowNano + NanoAOD Campaign

Example 1:\
If flowDR is tasksubmit, flowMini is tasksubmit, flowNano is tasksubmit\
When GS is done, McM will flow to NanoAOD and submit all of them

Example 2:\
If flowDR is tasksubmit, flowMini is tasksubmit, flowNano is submit\
When GS is done, McM will flow to MiniAOD and submit DR with MiniAOD\
When MiniAOD is done, McM will flow to NanoAOD and submit NanoAOD

Example 3:\
If flowDR is tasksubmit, flowMini is submit, flowNano is submit\
When GS is done, McM will flow to DR and submit DR\
When DR is done, McM will flow to MiniAOD and submit MiniAOD\
When MiniAOD is done, McM will flow to NanoAOD and submit NanoAOD

### Request parameters&#x20;

This is a list of dictionary which will work as a **modifier** to the request from the allowed campaign to the next campaign

### Process string&#x20;

In order to label properly the output dataset, flow may contain the _process string_ parameter to label as follows:

### Notes&#x20;

These are notes of the flow that area here for documentation, and also are copied in batch announcement to ops. It should contain indications necessary for processing if any.
