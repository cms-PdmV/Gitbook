# Home (Initial page)

### Introduction

Home page provides a search across all objects in the RelVal machine, a couple of links to quickly see your own items in the machine as well as overview of number of objects in the database with more details on submitted RelVals.

### Search

Whenever a query is entered into the search field, RelVal machine performs multiple searches on multiple attributes across both types of objects in the database.

Currently these attributes are included in the search:

* PrepID of Tickets and RelVals
* CMSSW Release of Tickets and RelVals
* Batch name of Tickets and RelVals
* Workflow id(s) of Tickets and RelVals
* Label of Tickets
* Workflow name of RelVals
* Output datasets of RelVals,
* Workflows (in ReqMgr2) of RelVals

Search supports wildcards, i.e. asterisks (\*) as any number of any characters, e.g. `A*C` would match `AC`, `ABC`, `ABBC`, etc. Space character is automatically translated to an asterisk and both can be used interchangeably. Search is based on regex, however it is not guaranteed to support full regex functionality.

Search results is a list of three values: found `value` on the left and database and attribute name on the right in a format `database:attribute` . When user clicks on a search result, user will be directed to the page indicated in the `database` part and results that match the criteria `attribute=value` will be shown.\
Example 1: user types `RECO` in the search field and is presented with a search result that has value `RECOonly` (on the left) and `tickets:label` as database and the attribute (on the right). If user clicks on this result, all tickets that have a label "RECOonly" will be shown.\
Example 2: user types `/RelValTTbar_13/CMSSW_10_6_20-PU_106X_mc2017_realistic_v9-v1` in the search field and is presented with a search result that has value `/RelValTTbar_13/CMSSW_10_6_20-PU_106X_mc2017_realistic_v9-v1/DQMIO` (on the left) and `relvals:output_datasets` on the right. If user clicks on this result, a RelVal that has "/RelValTTbar\_13/CMSSW\_10\_6\_20-PU\_106X\_mc2017\_realistic\_v9-v1/DQMIO" as output dataset will be shown.

![Search results for "DD4HEP", note the object type and attribute name on the right](<../.gitbook/assets/Screenshot from 2021-07-21 13-54-36.png>)

### Quick links

Quick links allow quick access to ticket creation page or to tickets and RelVals created by the user.

![Links to create a new ticket or show all user's tickets and RelVals](<../.gitbook/assets/Screenshot from 2021-07-21 13-52-04.png>)

### Objects in RelVal database

This section provides quick access to each type of objects (Tickets and RelVals) as well as show how many Tickets and RelVals are in the database. Tickets and RelVals are expanded to show number of items with a particular status. RelVals that have status "submitted" are expanded to even more granularity and show how many RelVals with different releases and batch names are submitted. Items in the "submitted RelVals" outer list are sorted by release name (higher on top) and by number of RelVals in the inner (batch name) list.

Clicking on links will lead to pages of items of that type with that particular status, release and batch name.

![Tickets: no new and 313 done. RelVals 19 new, 171 submitted and 1816 done](<../.gitbook/assets/Screenshot from 2021-07-21 13-52-13.png>)
