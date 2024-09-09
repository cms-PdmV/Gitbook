# How to create a new ticket

The following procedure applies when we receive new requests (e.g. in the [MccM](https://twiki.cern.ch/twiki/bin/view/CMS/MccM) meetings) Gen contacts provide us the prepID and we create a new ticket, and set the priority, campaigns, etc

&#x20;1.1) Go to [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM) page ([https://cms-pdmv.cern.ch/mcm/![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/) ) and click on "Mccm" tab;

&#x20;(1.2) In the bottom of the page, click on "Create new [MccM](https://twiki.cern.ch/twiki/bin/view/CMS/MccM) ticket";

&#x20;(1.3) Choose the PWG which asked the requests (for instance, HIG);

&#x20;(1.4) From the [MccM](https://twiki.cern.ch/twiki/bin/view/CMS/MccM) Twiki page ([https://twiki.cern.ch/twiki/bin/viewauth/CMS/MonteCarloCoordinationMeeting20141009](https://twiki.cern.ch/twiki/bin/viewauth/CMS/MonteCarloCoordinationMeeting20141009)), copy the text concerning the requests and paste in the field "Notes" (for example, HIG-Summer12-02281, ... 02285, 02287, 02289, 02290 w(qq)h invisible (\~4M events, nigh priority, no-RD MC) ). From now on, lets suppose we have to submit these requests;

&#x20;(1.5) In the field "Block", put the agreed prioritisation for the set of requests (for example, 4);

&#x20;(1.6) In the field "Requests", put "HIG-Summer12-02281" and click in the "+" beside it. To create a range of requests, click in the "+" beside it again and put the last request of the range ("HIG-Summer12-02285"). Click in the "+" beside "HIG-Summer12-02285". Each request could be entered individually using the "+" below each of them;

&#x20;(1.7) In the field "Chains", click on the "+" button and choose the chain. The correct chain will depend on the campaign the request will have to enter. To discover which chain you will have to use, you can have a look on the set of existing chained campaigns and have a guess. To open the chained campaigns page, click on the "Chained campaign" button at the top of the page. To see all chained campaigns click on the "All" button at the bottom of the page:

&#x20;(1.7-a) From their prepid we know they have been created in the Summer12 campaign. Also, gen contact said they will have to be digi-recod without Run Dependent conditions (no-RD MC). We will have to look for a chain containing these two informations (starting from Summer12 and digi-recoding without RD conditions).

&#x20;(1.7-b) In the "Campaigns" collumn, look for all chained campaigns starting from "Summer12";

&#x20;(1.7-c) Every chained campaing has an alias ("Alias" column). The ones having "DR" in its alias are used for normal reconstruction, the ones having "RD" are for Run Dependent conditions, "BPH" are for B-Physics studies, "MU" for muon, "NP" for No Pile up, "LT" for trigger studies ("LT" ones automatically keep the "RAW" event content in its samples);

&#x20;(1.7-d) In the "Alias" column we see that the only campaign which satisfy our needs is the one which has the alias "S12DR53". That is the alias we will have to enter in the "Chains" field of the ticket.

&#x20;(1.8) In the ticket page, click on the "Commit" button. If everything goes fine, click on the "View" button to view the created ticket.
