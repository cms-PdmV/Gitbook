---
description: In this page, we give a description of icons and features of requests in McM
---

# McM Glossary: requests

{% file src="../.gitbook/assets/McMRequests.png" %}
Screenshot of features for requests in McM
{% endfile %}

### What is a request?

A request is simply a MC sample that is submitted (or prepared for submission) in central production.&#x20;

In the following, the different columns seen in McM for a request are explained.

### Prep ID:

It is the identification string of a request in McM. It is created automatically according to the specified PWG, the campaign under which the request is created and a progressive number.

### Actions:

This panels provides buttons on possible action and links regarding the request. typically cloning, create, approve to next step, reset, ...

### PWG (Physics working group):

PWG stands for Physics Working Group and defines what group the requests has been created by.

### Approval:

The approval represents what is to become of the request&#x20;

* none : there is no action required on the request
* validation : the request needs to be processed to provide validation material
* define : the request is ready to be defined
* approve : the request is ready to be approved
* submit : the request is ready to be submitted

The decoupling of status and approval is to be able to have "post-processing" in between statuses. Toggling the approval should trigger an action that is done either on the server side, or by exterior jobs, and could take up to a few hours. This requires anyway the presence of approval, i.e a request in \[status=new, approval=none] does not have to be validation processed until toggled to do so, and its status should not change to validation, until the process runs to completion.

### Status:

This represent the status of a request:&#x20;

* new : this needs to be operated on by a [generator contact](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcMGenContact) for request in root or possible root campaign (lhe or gen-sim)
* validation : the request has been processed and is ready for validation procedure by the [gen contact](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcMGenContact)
* defined : the request needs to be approved by the [generator conveners](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcMGenConvener)
* approved : the request needs to be submitted by the [production manager](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcMProdManager)
* submitted : is being processed by computing operation
* done : is ready for consumption, or further processing

### Status-approval combination

This is a list of all possible (valid) combinations of request approval and request status values:&#x20;

* none-new - new request which is waiting to be pushed into next step manually.
* validation-new - test (validation) job is currently running in condor. When it will be finished, [ValidationControl](https://twiki.cern.ch/twiki/bin/edit/CMS/ValidationControl?topicparent=CMS.PdmVMcMGlossary;nowysiwyg=1).py (Jenkins: [ValidationJobs](https://twiki.cern.ch/twiki/bin/edit/CMS/ValidationJobs?topicparent=CMS.PdmVMcMGlossary;nowysiwyg=1)) will take care of it.
* validation-validation - validation job was successful and now generator contract can recheck the configuration and move it to the next step.
* define-defined - generator group have to check and approve (including production managers)
* approve-approved - approved, waiting to be put into injection thread pool (size - 15, others will be in queue which size is visible in Dashboard, below the table) by [RequestFlow](https://twiki.cern.ch/twiki/bin/edit/CMS/RequestFlow?topicparent=CMS.PdmVMcMGlossary;nowysiwyg=1) (Jenkins).
* submit-approved - put into injection thread pool by [RequestFlow](https://twiki.cern.ch/twiki/bin/edit/CMS/RequestFlow?topicparent=CMS.PdmVMcMGlossary;nowysiwyg=1) (Jenkins). Waiting to be injected into computing. If request is stuck in this step, it needs a soft reset which will change status to approve-approved (one step back).
* submit-submitted - injection into computing succeeded. Being computed at the moment.
* submit-done - computing finished computing request.

### Validation (to be implemented):

For certain request, a validation step is required of the generator contact and a set of plots are provided in the [DQM](https://twiki.cern.ch/twiki/bin/view/CMS/DQM) gui under a "four scares" icon. The [generator contact](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcMGenContact) should scrutinize these plots prior to toggling the define approval for the request.

### Input dataset:

This defines the dataset, if any, in input to the request.

### Output dataset:

This is the list of datasets that were created in output by the request. If empty, no output dataset is saved. This is possible for any intermediate step of a chain

### Mcdb ID:

This gives the unique private lhe file identifier, which maps into EOS space at Cern cmsLs /store/lhe/, //eoscms//eos/cms/store/lhe/. This is used when the LHE files cannot be created within a CMSSW environment (and hence a private LHE file is used), and used for production of a sample.

The usage of this kind of input require special campaign separated from the usual GEN-SIM campaigns (pLHE).&#x20;

* \-1 means request is root of chain. No input files.
* 0 - request is possible root request. Possible input files.
* \>0 - request has an private LHE file for input. This number will be translated to file path when generating cmsDriver campaign. Input files exist.

### &#x20;Fragment:

This field is the generator fragment that will be used for the request. It is stored in the [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM) database instead of being in cvs (legacy) or in git genproductions repository. In the request edit page of [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM), the free text box can be used to:&#x20;

* Copy paste a python fragment
* Drag and Drop a file from any local directory
* Edit the text of the fragment

### Fragment name:

This is the name of the gen fragment for the request, it can be either be of the form Configuration/GenProduction/python/name\_of\_fragment or name\_of\_fragment, where the only requirement is for it to be reachable via [https://raw.github.com/cms-sw/genproductions/master/name\_of\_fragment![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://raw.github.com/cms-sw/genproductions/master/name\_of\_fragment).

name\_of\_fragment can contain "/" if designating a path to a file.

More information is available under [GitRepositoryForGenProduction](https://twiki.cern.ch/twiki/bin/view/CMS/GitRepositoryForGenProduction)

### Dataset name:

The dataset name (or dsn) is not the full dataset name that will appear in [DAS](https://twiki.cern.ch/twiki/bin/view/CMS/DAS), but only the label between the first two / of the [DAS](https://twiki.cern.ch/twiki/bin/view/CMS/DAS) dataset name. It is used to define the even type as documented in : [ProductionDataSetNames](https://twiki.cern.ch/twiki/bin/view/CMS/ProductionDataSetNames)

I case of special request, that are variations of the standard configuration , a pocessing string needs to be added to the final dataset name.

### Process string:

A process string should NOT be added to a request by MC contacts, except in very exceptional cases. Examples of process strings added for sets of requests are the following:

1. "Nano14Dec2018": requests of campaign NanoAODv4 (2016, 2017 and 2018) reprocessing. The process string is useful for consistency with ReReco NanoAOD data, carrying the same process string.

### Extensions:

In case a request is an extension of another (exactly same fragment but need for additional statistics), this parameter should be set to the proper numerical value (1 for first extension, 2 for second and so on), so that it is taken into account properly in production. The output dataset name will have the string -ext1, -ext2, etc.

### Total events:

This is the number of events demanded in output for a given workflow. In the case of requests involving filtering or matching efficiency (e.g. if the request has a GEN-SIM step), 'total events' is set by the GEN contact to be the number of events produced after the filtering.

In the **task-chain** case (let's assume chaining N campaigns; typically N is 2), the total events of the first request in the chain is used by [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM) to set the total events for all subsequent requests in the task-chain; that's because the completed events is not available for any request in the task-chain, at the moment of its creation.

In the case of a **task-chain** involving wmLHE and GEN-SIM separately (now there are very few cases where this happens), the 'total events' of the wmLHE request needs to be set to total\_events = needed\_events/(matching\_efficiency\*filter\_efficiency), to account for the filtering in the GEN-SIM step. There's no need of setting the 'total events' of the GEN-SIM (unless there's a need to process only a sub-set of the wmLHW output).&#x20;

In every other case total\_events = needed\_events. The matching and filter efficiencies have to be measured with large precision, so that the total number of events can be accurately estimated.

### CMSSW release:

This is the exact release that has been used for the production of the request. Together with sequences, it allows to produce the sample.

### Sequences:

This is the exact cmsDriver command that is attached to the request and that will be run in production for the considered step.

### Keep output:

This indicates if the output of the possible intermediate step will be kept in production.

### Generator parameters:

This contains generator information that can be modified at any time by the generator contact. It should be the place to put more precise values of the cross section, filter\&match efficiencies. Efficiencies need to be provided with accuracy so as to have an accurate number of events in output of production. These values are recomputed automatically during the new validation run-test, if the calculated error is lower than the one already provided.

### Generators:

This indicates what are the generators that have been used to produce the sample. This has to be filled properly by the generator contact as there is no automatic way of "discovering" this value from the request itself.

### Notes:

This is a free text field in order to provide notes to the user of the sample. It has been used to provide the madgraph cards used for producing the sample. It can be used for giving indications on where to find refined cross sections of the samples, if calculated with higher orders (although the generator parameters filled is meant for that).

These **are not** notes to production managers, as they do not get exposed to it.

### Tags:

This is a free tagging field that can be used to categorize samples, and simplify the book-keeping of what is meant for what. It is up to the generator contacts to tag their or others requests. To create a tag user enter a needed tag as string and clicks ',' then the string will be created to tag the object.

### Config ID:

This provides a link to the exact configuration which had been generated from the sequences and send for production.

### Time/event:

List of values, where each value represents cmsDriver's step, e.g. \[1,2] 1 - DIGI step, 2 - [RECO](https://twiki.cern.ch/twiki/bin/view/CMS/RECO) step. This is the cpu time per generated event. To compute it, you must divide the time of your test job by the number of events in the job configuration. This must not be confused with the number of events in the output dataset, which could be much lower when there is a filter.

It can be obtain by dividing the total cpu time by the number of events in input after running the [test provided by McM](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcM#Testing).

### Type:

This is the technical type of a request in [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM).

### History:

This provides the history of the request including updates and status transitions.

### Flown with:

This indicates, if any, what flow object has been used to create the request from another request of the same chain.

### Priority:

The priority indicates what has been the chosen number given to that request in the production system. Priorities are organized in blocks, from 1 to 6, where 1 corresponds the highest priority and 6 to the lowest. Priority blocks need to be specified in the tickets and are approved by the PPD group, according to the overall CMS analysis and publication plan.

### Completed events:

This is the number of events actually produced, set once the request turns into done status.

### Reqmgr name:

This gives a list of the actual requests in wmagent/request-manager made or required for the sample production. The "details" link is for expert level and direct to the request manager page with all technical details of the requests. The "stats" link goes to the stats monitoring page for medium-expert use. The "eye" allows to load primordial information on the outcome of the processing of the [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM) request in WMagent.
