---
description: In this page, we give a description of icons and features of tickets in McM
---

# McM glossary: tickets

### What is a ticket?

A ticket is the way to communicate and present the requests to be submitted in central production. In a ticket, a MC contact places the list of requests to submit, the priority at which the requests will be submitted and the chain to use, which defines among other things the PU scenario and the reconstruction conditions which will be used for the requests.

In the following, the different entries for a ticket are explained (not all are mandatory).

### mccms pwg&#x20;

This is the pwg that has made a request for chains. It can be different than the pwg of the requests to be chained.

### mccms notes&#x20;

This should contain enough information to understand the origin and the need of the request.

### mccms meeting&#x20;

This is assigned automatically to the [next MccM meeting date![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/settings?prepid=mccm\_meeting\_day).

### mccms deadline&#x20;

This is an indication of the required deadline for the chains to complete, as an indication for now, it might get used automatically in the future to set the priority accordingly.

### mccms staged&#x20;

In case the ticket needs to create chains for which only part of the processing will be done at the end-point (digi-reco), this number should indicate the amount of events required

### mccms threshold&#x20;

In case the ticket needs to create chains for which only part of the processing will be done at the end-point (digi-reco), this number should indicate the fraction of events required.

### mccms chains&#x20;

These are the aliases of the chained campaigns that chains need to be created in.

### mccms repetitions&#x20;

If the root request needs to be chains multiple times within the same chained campaign, this should indicate the number of chains required (defaults to 1).

### mccms size&#x20;

As an indication of the total amount of events expected in the end (repetitions times chains times requests times ...)

### mccms block&#x20;

This is the priority block number [mapped to priority![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/settings?prepid=priority\_per\_block)

### mccms special&#x20;

In case the ticket needs to be hosting [special requests](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcM#Special\_Request) from [special chains](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVMcM#Special\_Chain), this should be ticked to true.
