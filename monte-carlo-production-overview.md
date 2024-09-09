---
description: In this page, we describe the general idea of central Monte Carlo production.
---

# Monte Carlo production overview

The CMS experiment provides the analyzers with a central production system for the simulation of Monte Carlo samples, which can be used for analyses. Monte Carlo production is handled by the Pdmv group (see [here](https://twiki.cern.ch/twiki/bin/view/CMS/PdmV) for more information) under the PPD group.

The tools that are used for production and monitoring are the following:

* [McM](https://cms-pdmv.cern.ch/mcm/) (Monte Carlo Management): database which collects all Monte Carlo requests already produced or aiming for production centrally.
* [pMp](https://cms-pdmv.cern.ch/pmp/) (Production Monitoring Platform): monitoring tool which visualizes in an user friendly way the produced events for specified requests/ group of requests.

The actors of this central system are the following:

* Analyzers/CMS users: they request MC samples which they need for their own analysis
* Monte Carlo contacts: they collect requests from the analyzers and they setup the requests in McM. Each POG/PAG/DPG group has its own Monte Carlo contacts, which can be contacted.
* Request managers: L3 coordinators inside Pdmv which review the requests and submit them. Request managers are also responsible for setting up the campaigns, under which the requests are created.

In these documentation pages, we give a separate overview of the features of McM and pMp, which are relevant for:

* [Analyzers](https://monte-carlo-production-tools.gitbook.io/project/analyzers-corner)
* [Monte Carlo contacts](https://monte-carlo-production-tools.gitbook.io/project/untitled)
* [Request managers](https://monte-carlo-production-tools.gitbook.io/project/untitled-1)

An additional important link for getting an idea about which campaigns are currently running in the central system can be found below:

[https://dmytro.web.cern.ch/dmytro/cmsprodmon/](https://dmytro.web.cern.ch/dmytro/cmsprodmon/)

![Example plot from https://dmytro.web.cern.ch/dmytro/cmsprodmon/ ](<.gitbook/assets/image (9).png>)
