# Home (Initial Page)

### Introduction

Home page provides a search across all objects in the ReReco machine, a couple of links to quickly see newest items in the machine as well as overview of number of objects in the database with more details on submitted Requests.

### Search

Whenever a query is entered into the search field, ReReco machine performs multiple searches on multiple attributes across all three types of objects in the database.

Currently these attributes are included in the search:

* PrepID of Subcampaigns, Tickets and Requests
* Subcampaign of Tickets and Requests
* Processing string of Tickets and Requests
* Input datasets and requests of Tickets
* Input dataset of Requests
* Output datasets of Requests
* Workflows (in ReqMgr2) of Requests

Search supports wildcards, i.e. asterisks (\*) as any number of any characters, e.g. `A*C` would match `AC`, `ABC`, `ABBC`, etc. Space character is automatically translated to an asterisk and both can be used interchangeably. Search is based on regex, however it is not guaranteed to support full regex functionality.

Search results is a list of three values: found `value` on the left and database and attribute name on the right in a format `database:attribute` . When user clicks on a search result, user will be directed to the page indicated in the `database` part and results that match the criteria `attribute=value` will be shown. \
Example 1: user types `ABC` in the search field and is presented with a search result that has value `ABCD` (on the left) and `requests:processing_string` as database and the attribute (on the right). If user clicks on this result, all Requests that have processing string "ABCD" will be shown.\
Example 2: user types `/HIDoubleMuon/HIRun2018A-04Apr2019-v1/AOD` in the search field and is presented with a search result that has value `/HIDoubleMuon/HIRun2018A-04Apr2019-v1/AOD` (on the left) and `requests:input_dataset` on the right. If user clicks on this result, all Requests that have "/HIDoubleMuon/HIRun2018A-04Apr2019-v1/AOD" as input dataset will be shown.

![Search results for "single electron", note the object type and attribute name on the right](<.gitbook/assets/Screenshot from 2021-05-12 18-03-21.png>)

### Quick links

Quick links allow quick access to ticket creation page or to requests or tickets pages where items are sorted by creation date with newest at the top.

![Links to create a new ticket or show all requests or tickets with newest at the beginning](<.gitbook/assets/Screenshot from 2021-05-12 18-03-36.png>)

### Objects in ReReco database&#x20;

This section provides quick access to each type of objects (Subcampaigns, Tickets and Requests) as well as show how many Tickets and Requests are in the database. Tickets and Requests are expanded to show number of items with a particular status. Requests that have status "submitted" are expanded to even more granularity and show how many Requests with different processing strings are submitted. Items in the "submitted Requests" list are sorted by number of Requests with given processing string.

Clicking on links will lead to pages of items of that type with that particular status (and processing string).

![Tickets: 6 new and 94 done. Requests 30 new, 15 approved, 54 submitted and 1592 done](<.gitbook/assets/Screenshot from 2021-05-12 18-03-44.png>)
