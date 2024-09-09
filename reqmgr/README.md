---
description: In this page, we collect the relevant information for request managers
---

# Request manager's corner

#### &#x20;<a href="#gmail-campaigns" id="gmail-campaigns"></a>

## How to increase the role of a user

&#x20;All users register in [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM) have a designated role like user, generator\_contact, request\_manager etc.

&#x20;To raise the role of a user, go to the _user page:_ [_https://cms-pdmv.cern.ch/mcm/users?page=-1\&shown=51_](https://cms-pdmv.cern.ch/mcm/users?page=-1\&shown=51)

&#x20;Find the user by its username or email, show the actions

* &#x20;And raise/decrease the role
* &#x20;Edit the user to add or remove a pwg to a user by using the drop down menu
* The available values of "pwg" is a name of the PAG and/or POG like BTV, EGM, HIG, HIN, etc.

## How to create a flow?

&#x20;The **flow** objects characterize how to go from one campaign to another

* &#x20;Navigate to the _flow_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/flows)
* &#x20;Click on "create new flow" or edit an existing one
* &#x20;Edit the parameters of the flow
* &#x20;The core of the Flows is the "request parameters" which determined what is going to be applied on top the request and the campaign parameter in going to the next step.
* &#x20;The "sequences" parameter is created automatically with the proper formatting according to the "next release".
  * &#x20;Nested in it, there can be any parameter in the request schema
  * &#x20;The "time\_event" and "size\_event" need to be filled where applicable (i.e. going into a release for which no-one will fill it up by hand)

## How to create a chained campaign?

Campaigns that are connected with a flow are gathered in chained campaign

* &#x20;When a flow is created, the chained campaigns are not created automatically
* &#x20;Navigate to the _flows_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/flows) and search for your needed flow
* &#x20;Click "Show possible Chained campaigns" (a list icon)
  * &#x20;This will open chained\_campaigns page where all **not\_created** chained campaigns using/connecting to the selected flow are displayed
  * &#x20;Click on "create" to add the corresponding chained campaign

## Daily actions for a request manager

&#x20;The **actions** that need to be taken for each requests are stored in [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM). Upon setting an action, verify that it has not yet been set.

* &#x20;Go to the _mccms_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/mccms)
  * &#x20;Get the ticket to be operated
  * &#x20;**Verify** the current chaining situation of the requests by clicking on "view all requests" and check that member\_of\_chain is empty or contains known existing chains to which something need to be added by enacting the ticket.
  * &#x20;**Verify** that there is a priority block number or a deadline provided
* &#x20;Click on "Generate chains"
  * &#x20;"Generate chains and reserve" can be clicked instead if one wants to create all pertaining requests (we should get into the habit of doing so)
* &#x20;**Verify** the chaining situation of the requests by clicking on "view all requests" and check that member\_of\_chain is in accordance to expectations
*
  * &#x20;Setting action on single request can be done through the priority change page directly, although using the mccm document is better for tracking
  *
    * &#x20;Go to the _priority\_change_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/priority\_change)
    * &#x20;Select one of the tabs, either requests, chained requests or chained campaigns
    * &#x20;Search for the ones you want by using the available parameters
      * &#x20;Set the desired block, staged, threshold or flag (For requests, only block number) and click the checkbox on the left (same row).
    * &#x20;Save the changes by clicking "Submit" button in the bottom right of your screen.
    * &#x20;**Key points:**
      * &#x20;Propagation: chained campaigns ---> chained requests ---> requests
      * &#x20;If you modify the block number for chained requests, it will be propagated to all the requests in the chain
      * &#x20;Chained campaign changes won't be propagated, but staged and threshold values will be used when you generate chained requests and requests in a mccm ticket, in case you didn't set them up in the ticket.
* Repeat the operation of setting the action and create the chained requests as many times as necessary.

## How to flow a chained request?

&#x20;The _import_ of a request into a new campaign is now fully performed with **flows**, although further manipulation of the requests are possible for full customisation.

* &#x20;Go to the _chained request_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained\_requests)
* &#x20;Select the chained request with **last status** in done (meaning that the last request in the chain has status done)
* &#x20;Multiple select or single click on "Flow"
* &#x20;Depending on the level of approval of different components, the request will be imported and set to be "submit" approval (\*)

## How to force flow a chained request?

Due to mis-configuration of a request, it could end up with less statistics than expected. Notifications are send. One can then force flow if the available stat is OK

* &#x20;Go to the _chained request_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained\_requests)
* &#x20;Select the chained request which flow is prevented due to missing statistics or because the statistics are good enough and the Analyzers need the request&#x20;
* &#x20;Choose one of the following
  * &#x20;Take a look at the details and figure out whether really something is not correct
  * &#x20;Rewind the chain if the stat is not OK to the requester&#x20;
  * &#x20;Click "force flow" for the chain to prevent the statistics check to limit the flowing

## How to submit a request?

Upon toggling "submit" approval, injection are performed and collected in batches

* &#x20;Go to the _requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests)
* &#x20;Have the "actions" displayed by clicking "Show" and ticking "Actions"
* &#x20;Toggling the "submit" approval will perform the injection in a separate thread
  * &#x20;For requests in approval "approved", single or multiple select and click "next step"
* &#x20;In case the submission has failed (the request is still in approval "submit" and status "approved"
  * &#x20;Single or multiple select and click "submit"
* &#x20;Upon completion (or failure) a notification is send and the status is changed to "submitted" (if success)
* &#x20;Request have to be part of a chain to be toggled into submit approval, report at the [next MccM](https://twiki.cern.ch/twiki/bin/view/CMS/WebSearchAdvanced?search=MonteCarloCoordinationMeeting2013\&scope=topic\&order=topic%AEex=on\&limit=all) or browse for missing actions in HN or previous [MccM minutes](https://twiki.cern.ch/twiki/bin/view/CMS/WebSearchAdvanced?search=MonteCarloCoordinationMeeting2013\&scope=topic\&order=topic%AEex=on\&limit=all)

## How to resubmit a request?

It could happen that a request needs only to be resubmitted, and it does not have to be hard reset

* &#x20;Go to the _requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests)
* &#x20;Have the "actions" displayed by clicking "Show" and ticking "Actions"
* &#x20;Click on "soft reset" button to have the request return to the previous approval and status
  * &#x20;The request will be removed from any "not announced" or done" batch
  * &#x20;The request in request manager should be either rejected by hand, or [use the invalidation procedure](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcMProdManager#Invalidations)
* &#x20;The request can now be retoggled to submit before the system does pick it up for automatic submission

## How to reserve a chain?

Instead of having request id being created as a chain items get completed, it is possible to reserve the next requests within a chained request

* &#x20;Either go to the _chained requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained\_requests)
  * &#x20;Click on the "Reserve chain" button to have all next requests created
* &#x20;Or go to the _mccm_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/mcm)
  * &#x20;Instead of clicking on "Generate chains for ...", click on "Generate chains and **reserve** for ..."

## How to submit a chain?

* &#x20;Go to the _requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests)
* &#x20;Find the first request of a chain that needs to be submitted as a chain of request
* &#x20;Toggle the submit approval of the request
* &#x20;In case of failures with submit, please contact an admin

#### Chain Re-Submit <a href="#gmail-chain-re-submit" id="gmail-chain-re-submit"></a>

In case of failures, or the wrong request being put in request manager, a soft-reset of the chain should be done

* &#x20;Go to _chained requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained\_requests)
* &#x20;Click on the "soft reset the flow" to have all request properly sof-reset
  * &#x20;The request will be removed from any "not announced" or done" batch
  * &#x20;The request in request manager should be either rejected by hand, or [use the invalidation procedure](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcMProdManager#Invalidations)
* &#x20;The requests in the chain can now be retoggled to submit before the system does pick it up for automatic submission

#### Injection Log <a href="#gmail-injection-log" id="gmail-injection-log"></a>

For requests in approval "submit" one can access the injection status and logs

* &#x20;If a "facetime" icon is present in the actions of a request, one can single or multiple click "see injection logs" and be redirected to a page with the logs and status
* &#x20;The injection status page that one is redirected at after submission can be closed at anytime, the injection process is not tied to the page.

## How to announce a batch?

&#x20;Batches of request need to be announced to [data operation requests HN![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://hypernews.cern.ch/HyperNews/CMS/get/dataopsrequests.html?)

* &#x20;Go to the _batches_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/batches)
* &#x20;Have the "actions" displayed by clicking "Show" and ticking "Actions"
* &#x20;For batches in the new status, click on the "Announce the batch to data Ops"
  * &#x20;Provide any further details of the submission batch, in addition to the "Notes" of the batch.

#### Notification <a href="#gmail-notification" id="gmail-notification"></a>

Notifications can be send automatically through [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM) to users registered to a given request

* &#x20;Go to the _requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests)
* &#x20;Multiple select or single click on "Notify"
  * &#x20;Enter the text for notification and click "Send"

#### Request Reset <a href="#gmail-request-reset" id="gmail-request-reset"></a>

&#x20;To reset a request after submission, given that usually a whole batch is affected, it is **probably more efficient** to reset the full batch : see below

* &#x20;Navigate to the batch the request is in by clicking "view batches containing ..." to navigate to the batch
* &#x20;Verify that indeed all requests in that batch are affected
  * &#x20;If yes, proceed with batch reset.
  * &#x20;If not, reset requests one by one.

#### Rewind <a href="#gmail-rewind" id="gmail-rewind"></a>

When a chained request needs to be invalidated, it has to berewinded

* &#x20;Go to the _chained requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained%20requests)
* &#x20;Click on rewind (this might not work on first click : to be fixed)
  * &#x20;this will reset and invalidate the last request of the chain
* &#x20;Repeat as many times as necessary to invalidate requests in the chain, and to put the "currently processing" asterix next to the proper request.
* &#x20;Navigate to the request from which the chain should restart in order to reset it and operate on it

#### Batch Holding <a href="#gmail-batch-holding" id="gmail-batch-holding"></a>

It might happen that a batch of already submitted requests, but not announced has to be put on hold from being announced

* &#x20;Go to the _batches_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/batches)
* &#x20;Have the "actions" displayed by clicking "Show" and ticking "Actions"
* &#x20;Click on "hold/unhold" button to set the status to "hold"
* &#x20;Once the batch can eventually be announced, click again on the "hold/unhold" button to set the status back to "new"

#### Batch Reset <a href="#gmail-batch-reset" id="gmail-batch-reset"></a>

In the unlucky case that a whole batch need to be reset, instead of resetting requests one-by-one.

* &#x20;Go to the _batches_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/batches)
* &#x20;Have the "actions" displayed by clicking "Show" and ticking "Actions"
* &#x20;Click on the "reset batch" button.

#### Invalidations <a href="#gmail-invalidations" id="gmail-invalidations"></a>

For requests already in production, the output dataset and requests need to be invalidated

&#x20;When a request is reset, its components are put in the invalidation DB

&#x20;Navigate to the _invalidations_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/invalidations)

&#x20;Browse the datasets and request that need invalidation

&#x20;Navigate to **`https://cms-pdmv.cern.ch/mcm/restapi/invalidations/inspect/`**

&#x20;You can announce it to dataops with **`https://cms-pdmv.cern.ch/mcm/restapi/invalidations/inspect/announced`**

#### Remove Request <a href="#gmail-remove-request" id="gmail-remove-request"></a>

Some request might have to be removed if not necessary anymore.

* &#x20;Go to the _requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests)
* &#x20;Find the request that needs to be removed.
  * &#x20;It has to be in "new" status
  * &#x20;It should not be the current "end point" of any chain. (rewind the chain if necessary)
* &#x20;Click on "Delete request"
* &#x20;If the corresponding chain has to be removed, refer to the corresponding section.

#### Remove Chain <a href="#gmail-remove-chain" id="gmail-remove-chain"></a>

Some chained requests might have been created by mistake and need to be removed.

* &#x20;Go to the _chained requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained\_requests)
* &#x20;Find the chain that need to be removed.
  * &#x20;It's corresponding "action" needs to be disabled.
  * &#x20;Its deletion cannot be leaving a request unchained, unless that request is new.
* &#x20;Click on "Delete chained request"
* &#x20;If end points request need to be removed first, please refer to the corresponding section.

#### Manage Step by Step <a href="#gmail-manage-step-by-step" id="gmail-manage-step-by-step"></a>

&#x20;Step by Step for managing requests in [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM)

* &#x20;Set the campaigns parameters in the _campaigns_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/campaigns)
* &#x20;Set the flow parameters in the _flows_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/flows)
  * &#x20;Generate if necessary the chained campaigns that need to be created ![Work in progress, under construction](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/wip.gif) (additional work needed)
* &#x20;Set the action in the _priority\_change_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/priority\_change) (**`requests not belonging to any chain cannot be submitted`**)
  * &#x20;You may click on the "view action" icon in the _requests_ [tab of McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests)
* &#x20;Once approved submit the requests by either
  * &#x20;Letting the regular inspection do the submission
  * &#x20;Toggling "submit" approval (and subsequently click submit upon hypothetical failures)
* &#x20;Upon completion of a request, either
  * &#x20;Let the routine inspection perform the flowing
  * &#x20;Navigate to the corresponding chained request and click "flow"
    * &#x20;If the flow's approval is sufficient, the flowing will be done. Otherwise, if the chained request's approval is sufficient, the flowing will be done, otherwise nothing will happen
      * &#x20;Upon successful flowing new requests will be created and put in the approval & status according to the flow
    * &#x20;New requests can be submitted or further modified

\====================================================

### How to create new flows and chained campaigns <a href="#gmail-how-to-create-new-flows-and-chained-campaigns" id="gmail-how-to-create-new-flows-and-chained-campaigns"></a>

&#x20;(0) Before creating new flows/chained campaigns, please check if there are existing flows which can be used. all flows can be found here:

&#x20;[https://cms-pdmv.cern.ch/mcm/flows?page=-1\&shown=95![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/flows?page=-1\&shown=95)

&#x20;What are most important are: "Allowed Campaigns", "Next Campaign", and "Request parameters".

&#x20;(1) if a new flow is indeed needed, go to page

&#x20;[https://cms-pdmv.cern.ch/mcm/flows?page=-1\&shown=31![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/flows?page=-1\&shown=31)

&#x20;click "Create new flow"

&#x20;put the name: (use similar name from similar existing flows)

&#x20;\[a new flow should appear on the page ]

&#x20;in the action, click, "Edit details"

&#x20;(2) to modify relevant information. (the best way is to copy and paste a similar flows and modify from that)

&#x20;Allowed campaings:

&#x20;Next campaign:

&#x20;Request parameters : here is the place we update information like: release, global tag, pileup, etc. note that "process\_string" should be unique for each flow. So be sure to pick up a different string for this value. (again, best way is to update from existing similar ones)

&#x20;add "some notes" about this flow, though this is not absolutely needed.

&#x20;Then click "Commit" in the left, Then click "View". Now in the approval column, it shows "None" In the Actions column, click "Next Step", approval column --> flow

&#x20;(3) once a new flow is created. go to the "chained campaigns" page

&#x20;click "Crate chained campaigns" in the bottom left,

&#x20;should be on this page

&#x20;[https://cms-pdmv.cern.ch/mcm/chained\_campaigns?select=\&page=0\&shown=15![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained\_campaigns?select=\&page=0\&shown=15)

&#x20;Search for the flow name which you just created.

&#x20;in the action columns, click "Create chain campaign" (the middle one)

&#x20;in the "Alias" field, put something meaningful (again, the best way is to look up existing similar chained campaigns), though it is also fine to leave it empty.

&#x20;click "Commit"

&#x20;Go to this page again

&#x20;[https://cms-pdmv.cern.ch/mcm/chained\_campaigns?select=\&page=0\&shown=15![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained\_campaigns?select=\&page=0\&shown=15)

&#x20;Normally need to repeat the above for wmLHE, pLHE and non-LHE based.

&#x20;(4) after the chained campaign is created, you should be able find the new "chains" when you create the ticket. It is either the "Alias" which you put in the chained campaign, or the full name (the [PrepId](https://twiki.cern.ch/twiki/bin/edit/CMS/PrepId?topicparent=CMS.PdmVMcMProdManagerOpsCorner;nowysiwyg=1) in the first column of the chained campaign).

&#x20;(4a) After clicking the "generate chains" button in the ticket page, click the "View chains from ..." in the Requests column, it will link to a page like:

&#x20;[https://cms-pdmv.cern.ch/mcm/chained\_requests?contains=B2G-Fall13pLHE-00003\&page=0![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/chained\_requests?contains=B2G-Fall13pLHE-00003\&page=0)

&#x20;On this page, you should find one or multiple [PrepId](https://twiki.cern.ch/twiki/bin/edit/CMS/PrepId?topicparent=CMS.PdmVMcMProdManagerOpsCorner;nowysiwyg=1), each of them refers to a different chain. You should be able to find the new chain which you just generated. And you will notice that in the "Chain" column, there is only one prepID (which is the root request in your ticket ).

&#x20;Now, in the Action column, you should click the "Flow" button to move forward. After this, you will see a new request (with itsprepID) appeared. This request should be a DR request, if it is GS request (which means the root request is a LHE request), click again the flow. Here we assume the GS request is ready (which means in "done" status"). This is normally the case, if the GS request is not ready, we can not do DR at all.

&#x20;Now you have the new DR request created. Now click on the DR request, it will link to your the DR request page, on this page, you can double check the "Sequences", if it contains the new information you added in the Flow, for example, if you updated the global tag, or the pileup, you should be able to see it there.

&#x20;(4b) Here we might want to update the information of the size/event and time/event. Usually, if this flow is general flows (for example, the ones we used for [Phys14DR](https://twiki.cern.ch/twiki/bin/edit/CMS/Phys14DR?topicparent=CMS.PdmVMcMProdManagerOpsCorner;nowysiwyg=1), or the ones which we will have for [RunII](https://twiki.cern.ch/twiki/bin/edit/CMS/RunII?topicparent=CMS.PdmVMcMProdManagerOpsCorner;nowysiwyg=1) DR campaign), it is good to run the test command of the Request, which also test if everything is fine. For these flows, we usually run a TTbar sample to represent the all samples.

&#x20;To run a test command, go to the request page,

&#x20;click "Get test command" in the Action column.it should go to this page, for example

&#x20;[https://cms-pdmv.cern.ch/mcm/public/restapi/requests/get\_test/BPH-Phys14DR-00001![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/public/restapi/requests/get\_test/BPH-Phys14DR-00001)

&#x20;Then, login to lxplus,

&#x20;wget [https://cms-pdmv.cern.ch/mcm/public/restapi/requests/get\_test/BPH-Phys14DR-00001![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/public/restapi/requests/get\_test/BPH-Phys14DR-00001)

&#x20;open this file, make sure the number of events are at least 50, if not, put 50. it is the "-n " option in the cmsDriver command. Note that there can be multiple cmsDriver commands. you need to update all of them to be the same.

&#x20;echo "ls -l" >> BPH-Phys14DR-00001

&#x20;voms-proxy-init -voms cms -valid 999:00

&#x20;Note here the XXXX refers to your ID (which is unique for each user), do not copy and paste directly below.

&#x20;cp /tmp/x509up\_uXXXX $HOME/private/personal/voms\_proxy.cert

&#x20;\[ more here, [https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookXrootdService#DownCmd\]](https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBookXrootdService#DownCmd])

&#x20;bsub -q 8nh -J test < BPH-Phys14DR-00001

&#x20;\*\* After the "bsub" is done, in the LSFJOB\_\*/STDOUT file, add the values (can be more than one) of "AvgEventCPU", and add the size of the root files produced, given by the "ls -l", (and divided by [TotalEvents](https://twiki.cern.ch/twiki/bin/edit/CMS/TotalEvents?topicparent=CMS.PdmVMcMProdManagerOpsCorner;nowysiwyg=1) and by 1024 to get kB). And put back these numbers in the Flow page, see (2) above in the "Request parameters"

&#x20;Note that, you can also directly add these time and size information in the Request, to do that, go to the request page, click the "Edit details" button, you can fill these information as well. Normally we do this if we want to update these information for individual request.

&#x20;(4c) Once the DR request is ready to go, you can click the "Next step" in the "Actions" column, to approve it, and click again, to submit. If submission is successful, the "Approval" column will be "submit" and the "Status" column will be "submitted". Otherwise there might be some problem of injection. In this case, you should also receive an email from the [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM) system (with part of the injection log sent to you). In this case, contact experts.

### How to fix "configuration upload fail" error for request <a href="#gmail-how-to-fix-configuration-upload-fail-error-for-request" id="gmail-how-to-fix-configuration-upload-fail-error-for-request"></a>

&#x20;Sometimes a request can be approved "by hand" twice in the DR step by mistake before its submission (a short period of time between the approvals) and that causes its configuration to fail upload. To fix this, here is an example for request HIN-pAWinter13DR53X-00084:

&#x20;(1) Reset the request (it will change its Approval/Status from submit/approved to none/new);

&#x20;(2) In the "Actions" column, click on the "Option Reset" button (this will change its "--datatier" parameter value in step 2 from GEN-SIM-RECO to GEN-SIM-RECO,DQM);

&#x20;(3) In the "Actions" column, click on the "Next step" (this will change its Approval/Status from none/new to approve/approved).

## How to change the priority block?

&#x20;Sometimes, we need to update the priority for some request. To do this, first we need to find the root request, then go to the request page, and, then, click the button of "View action on this request" in the Actions column, find the chain you want to update,and update the block number.

&#x20;Example:

&#x20;(1) first , go to this page. [https://cms-pdmv.cern.ch/mcm/requests?prepid=TOP-Summer12pLHE-00097\&page=0\&shown=127![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests?prepid=TOP-Summer12pLHE-00097\&page=0\&shown=127)

&#x20;(2) click "View action on this request" button in the Action field, then you should be on this page [https://cms-pdmv.cern.ch/mcm/actions?prepid=TOP-Summer12pLHE-00097\&select=Summer12pLHE\&page=0\&shown=1019![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/actions?prepid=TOP-Summer12pLHE-00097\&select=Summer12pLHE\&page=0\&shown=1019)

&#x20;(3) now, in this column, pLHE12DR53, click the second "tool button" , it will show "5", now you can change that to 6 , you can save the update by clicking the button (next the History) in the Actions field , the button is a "triangle with a exclamation mark inside"

## How to select a range of request?

&#x20;use "range" in the url: [https://cms-pdmv.cern.ch/mcm/requests?page=0\&range=EXO-Fall13-00237,EXO-Fall13-00266\&shown=127![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests?page=0\&range=EXO-Fall13-00237,EXO-Fall13-00266\&shown=127)

## How to reset a request?

Sometimes, Gen contacts ask us to reset a request so they can modify it, first we need to find the request, and in the "Action" field, click the reset button

## Reset the request

&#x20;Instructions:

1. &#x20;go to the chained request which contains the request;
2. &#x20;rewind the flow until the asterix stays after the request to be reseted;
3. &#x20;reset the request;
4. &#x20;go to [https://cms-pdmv.cern.ch/mcm/restapi/invalidations/inspect![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/restapi/invalidations/inspect) and announce invalidations (if the dataset **has to be kept**, click on "clear invalidation withouth announcing").

## Basic instructions to submit a ticket

The following shows the instructions to approve a ticket (which is generally reported about in the MCCM Wednesday's meeting) and to submit the corresponding requests included in the ticket.

&#x20;\- Go to the page of the ticket to submit

&#x20;\- Check the block of the requests, the status of the requests (they need to be all approved by the GEN conveners), the flag of keep output and the name of the dataset (if it makes sense)

&#x20;\- Click the button "approve and reserve chains"

&#x20;\- Wait until the browser says "Everything went fine"

&#x20;\- Refresh the page and look at the "generated chains"

&#x20;\- Click "approve all requests"

&#x20;\- You are (almost) done!

&#x20;\- After some time (might be minutes or hours), you should get a mail saying "Injection succeded for...": this means that the status of the request changed from "approved" to "submitted"

For submitting a request you need to announce to data-ops the corresponding batch

&#x20;\- You need to go the batch page which by default shows the non-announced batches

&#x20;\- Click on actions

&#x20;\- Identify the corresponding batch, which should be listed in the page

&#x20;\- Click on the megaphone button, which automatically announces the batch

&#x20;\- You are done!

## How to handle a pLHE request

&#x20;\- MC contact presents a pLHE request with the full chain up to [NanoAOD](https://twiki.cern.ch/twiki/bin/edit/CMS/NanoAOD?topicparent=CMS.PdmVMcMProdManagerActions;nowysiwyg=1) in the ticket

&#x20;\- Req Manager approves the ticket and reserve up to GS step. This does not reserve all the other steps of the chain but only pLHE and GS requests will be in place.

We ask MC contacts to validate the two requests together ("star" button in the chained request page). When it's validated, GEN approves.

&#x20;\- Req Manager submits the two steps (pLHE+GS).

&#x20;\- When it’s done, the request will flow automatically to DR, Mini and NanoAOD.  No additional action is needed for the whole cahin (except the announcement of the corresponding batch).
