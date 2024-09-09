---
description: >-
  Very important for a request manager is to open campaigns where to submit
  requests. In this page.
---

# Procedure how to create and setup a campaign

The idea of opening a campaign (and related actions) is to test a cmsDriver before a massive injection of requests using this driver is performed. This test happens with a workflow called "pilot".&#x20;

![Schematic of a campaign opening.](<../.gitbook/assets/image (22).png>)

The actions required by a request manager in the right order are:

* Create the campaign in McM and setup the driver and the campaign features accordingly to the validated "RelVal" and the needs for that campaign
* Open a JIRA ticket in computing project: [Link](https://its.cern.ch/jira/projects/PRCAMPAIGNS/issues/PRCAMPAIGNS-5?filter=allopenissues), asking to open a campaign (example [here](https://its.cern.ch/jira/projects/PRCAMPAIGNS/issues/PRCAMPAIGNS-24?filter=allopenissues)). Normally one ticket per campaign needs to be created. This set of information needs to be added.

1\. **Summary:** ' \<campaign name>'//please try to have one campaign per JIRA so it is easy to manage and also will help for closing the campaigns. \
\
2\. **Description:** 'Details about the campaign including the configuration'\
\
3.For now, the **Assignee:** "Sharad Agarwal"

\
4\. **Status**: "TO DO"

\
5\. Please update the JIRA as soon as the pilot is injected. If the pilot finishes without issues, we will enable the campaign and update the JIRA status as "OPEN".\
\
5\. The data set that you want to lock - please specify the data set name, number of sites, and the time period on the ticket of the campaign where it is produced and tag the transfer team.

\
6\. Tag us(computing) to add the secondaries(MB samples and secondaries) on the JIRAs of the campaign where it is suppose to be added as input data set and not on the JIRA of the campaign where you asked Transfer team to lock it. Please do mention the ticket number of the JIRA where you got it locked for reference. \
\
7\. Please update the JIRA ticket and tell us that the campaign has no more requests to process and it can be closed.&#x20;

* Circulate the cmsDriver to the experts (example [here](https://hypernews.cern.ch/HyperNews/CMS/get/comp-ops/4462.html)). This means send a mail to the following hypernews:
  * prep-ops (hn-cms-prep-ops@cern.ch)
  * comp-ops (hn-cms-comp-ops@cern.ch)
  * software and release validation (cms-release-dataops@cern.ch)
  *
*   If no modification to the driver is required, prepare a pilot requets in McM.

    * Set 10000 events
    * Add "pilot" in the process string of the request


* Validate the request in McM and submit.
* Post the workflow name in the corresponding JIRA ticket, so that the request can be monitored.
* If the request is successful, the campaign is enabled by computing (No action required from request managers).

N.B. Please follow possible changes (in release for GS and wmLHEGS campaigns) which will be announced after the campaign is opened.

## Special actions for opening DIGI-RECO requests

The speciality of a DIGI-RECO request is that this needs an input pileup dataset. Additional actions from request managers for a DR (standard mixing) campaign are:

* Creating the MB sample under the GS campaign of the corresponding DR campaign
* As soon as the MB sample gets submitted, ask the transfer team to lock this sample to disk in a JIRA ticket (example [here](https://its.cern.ch/jira/browse/CMSTRANSF-40)).
* As soon as the MB sample gets completed, ask the P\&R team to allow the use of this input dataset for the created DR campaign. This also happens in a JIRA ticket (example [here](https://its.cern.ch/jira/browse/CMSCOMPPR-5107)).

For a DRPremix, three additional actions needs to be taken by request managers:

* Prepare the premix library under the PrePremix campaign (example [here](https://cms-pdmv.cern.ch/mcm/campaigns?prepid=RunIISummer17PrePremix\&page=0\&shown=63)). Request managers need to manually change the driver of this campaign for the production of the premix library (The PrePremix campaign is used by ALL premix library submissions).
* Ask the P\&R team to allow the use of the MB sample as allowed input dataset for the PrePremix campaign.
* Submit the premix library.
* As soon as the premix library gets completed, ask the P\&R team to allow the use of this input dataset for the created DRPremix campaign (in a JIRA) and the transfer team to lock it (can happen within the same JIRA).

