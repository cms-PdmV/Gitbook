# Tickets

### Introduction

Tickets are the way to easily create a set of requests in a certain subcampaign or chain of subcampaigns where output of one request is input for the next one. Ticket itself is a one-use-only object - when ticket is created, it can be then used to create requests and after that it is there only for the bookkeeping purposes. If new requests need to be created, a new ticket must be created. Two fundamental ingredients for a ticket are list of input datasets or requests and subcampaign.

Ticket can use either datasets or existing requests as input. List can can be a mix of both.

### Getting datasets from DBS

In order to ease up getting list of input datasets, ReReco machine offers a function to query the DBS. To do so, user has to click "Query for datasets" button at the bottom which will show a popup.

!["Query for datasets" button](<.gitbook/assets/Screenshot from 2021-10-18 17-11-56 (2).png>)

In the popup user has two fields: query and comma-separated values to filter out. In the first field user must enter a query, usually with wildcards. It must satisfy such format "/\*/\*/DATATIER", e.g. /\*Electron\*/Run2016A-v\*/RAW. However, this could include datasets that were produced by validation or pilot requests. In order to remove such datasets, user can specify "validation,pilot" in the second field. This field is a list of comma-separated values that will be used when filtering-out the datasets. If field has "validation,pilot", it means that after fetching the dataset names, all names that have either "validation" or "pilot" in them, will be removed. Note that these values are case sensitive. Some primary datasets are blacklisted in the ReReco machines, which means that dataset names with these primary datasets will be implicitly removed from the fetch results.

The blacklist can be found here: [https://cms-pdmv.cern.ch/rereco/api/settings/get/dataset\_blacklist](https://cms-pdmv.cern.ch/rereco/api/settings/get/dataset\_blacklist)&#x20;

![Fields with query and filter-out values](<.gitbook/assets/Screenshot from 2021-06-02 19-36-45.png>)

If list of datasets is not empty, user will have two options what to do with existing datasets: "Fetch and replace" will fetch dataset list from DBS and replace existing list or "Fetch and append" will fetch dataset list and append it to already existing list. If user chooses to append, only datasets that are not in existing list will be appended, i.e. appending will not duplicate dataset names.

![Options to "Fetch and replace" or "Fetch and append"](<.gitbook/assets/Screenshot from 2021-06-02 19-37-48.png>)

### Getting PrepIDs of existing requests

In order to ease up getting list of input requests, just like input datasets, ReReco machine has a helper to search for and fetch PrepIDs of already existing requests. Popup for fetching can be opened by clicking "Query for requests" button at the bottom.

!["Query for requests" button](<.gitbook/assets/Screenshot from 2021-10-18 17-11-56.png>)

This feature will search ReReco machine database for requests based on user given query. Just like with datasets, there are buttons to "Fetch and replace" or to "Fetch and append".

Due to performance reasons result size is limited to 1000 PrepIDs.

![Options to "Fetch and replace" or "Fetch and append"](<.gitbook/assets/Screenshot from 2021-10-18 17-12-13.png>)

### Ticket steps

ReReco machine allows to create tickets with one or multiple steps. Steps represent requests in different campaigns where output of one request will be used as input for the subsequent request. For example, first step can produce AOD and MiniAOD datasets in subcampaign A and seconds step can then use MiniAOD as input and produce NanoAOD dataset in subcampaign B. Each step has a subcampaign, processing string, list of sizes per event (same number of values as there are sequences in subcampaign), list of times per event (same number of values as there are sequences in subcampaign) and priority. All of these attribute will be propagated to the created request and sequences will be copied from subcampaign to the request.

![Two steps - UltraLegacy2016-Cosmics and NANOAODRun2DataProd-NanoAODv7\_2016](<.gitbook/assets/Screenshot from 2021-06-02 20-44-20.png>)

### Creating requests

When user clicks a button to create requests, ReReco machine will go over list of input datasets or request PrepIDs and for each of them will create as many requests as there are steps and set input of requests appropriately. For example, if there are two steps, first one has Subcampaign1 and second has Subcampaign2 and three datasets: AAA, BBB and CCC. ReReco machine will create six requests: three in Subcampaign1 with AAA, BBB and CCC as input and another three in Subcampaign2 with the first ones as input respectively.&#x20;

### Ticket attributes

* PrepID (`prepid`) - unique identifier of the ticket
* Created requests (`created_requests`) - list of PrepIDs of requests that were created from this ticket
* History (`history`) - history of actions performed on the ticket, such as creation or editing. Each entry includes date, user username, action and value
* Input (`input`) - list of input dataset names or request PrepIDs that will be used as input
* Notes (`notes`) - free-form user text&#x20;
* Status (`status`) - ticket status, can be either `new` or `done`&#x20;
* Steps (`steps`) - list of dictionaries that have subcampaign name, processing string, sizes and times per event values that will be used to create "chains" of requests

### Ticket actions

* Edit - open editing page of the ticket
* Delete - delete the ticket. This is allowed only if it is new or if all requests, that were created from the ticket are deleted. If the requests are present, they have to be deleted first
* Clone - open a form to create a new ticket and prefill form fields with info of given ticket
* Create requests - create requests for each input dataset or request and each step
* Requests - show requests that were created from the ticket
* TWiki - open a snippet that can be copied to ReReco TWiki. Snippet forms tables of eras with each row having a primary dataset name, link to historical pMp plot and list of runs&#x20;
