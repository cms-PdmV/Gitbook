# Subcampaigns

### Introduction

Campaigns on computing side group together a big number of similar requests. This concept is also used in the ReReco machine where it is not only used to group, but also to act as a template for the requests. It would be tedious to create tens or hundreds of identical requests where only the input dataset is different. Such template can store the `cmsDriver.py` command values and requests then can be created by taking an input dataset and the `cmsDriver.py`. This way arguments are defined only once and can be reused multiple times. Unfortunately "Computing Campaigns" cannot be directly used in the ReReco machine because even though a campaign groups similar requests, it can contain different primary datasets and, subsequently, fundamentally different `cmsDriver.py` commands, e.g. "UltraLegacy2017" campaign could be used for both "Cosmics" and "ZeroBiasScouting" requests and their `cmsDriver.py` attributes are very different. This means that after submitting "Cosmics", the template would have to be discarded and created from scratch for "ZeroBiasScouting". If "Cosmics" had to be submitted again, then template once again would have to be scrapped and recreated. This is why it was decided to introduce a smaller unit of "Campaign" in ReReco machine - a subcampaign. Subcampaign still represents one of the campaigns in computing, but different subcampaigns can have different `cmsDriver.py` and not conflict with each other. In the example mentioned above, there would be two UltraLegacy2017 subcampaigns - one for Cosmics and one for ZeroBiasScouting. This way ReReco machine can preserve different `cmsDriver.py` arguments that are used in a single computing campaign. This is why this is called a subcampaign - it is like one snapshot of a campaign. subcampaign name is not submitted to computing, requests that are submitted to computing, use campaign name that given subcampaign is part of, so this new object type does not affect anything outside the ReReco machine.

Subcampaigns in the ReReco machine: [https://cms-pdmv.cern.ch/rereco/subcampaigns](https://cms-pdmv.cern.ch/rereco/subcampaigns?shown=127\&page=0\&limit=50)

### Subcampaign naming

It is important to understand how subcampaigns are and should be named. subcampaign name is always made of two parts that are joined with a dash ( - minus). First part is the campaign name in computing. Second part is subcampaign's identifier - string that gives more insight on what is the purpose of given subcampaign.

All available computing campaigns and their names: [https://github.com/CMSCompOps/WmAgentScripts/blob/master/campaigns.json](https://github.com/CMSCompOps/WmAgentScripts/blob/master/campaigns.json)

If needed name is not there, user needs to first announce the new campaign to computing, inject a pilot request, wait for its completion and then ask for the activation of the campaign.

Names of two example subcampaigns mentioned in the Introduction section would be: "UltraLegacy2017-Cosmics" and "UltraLegacy2017-ZeroBiasScouting" where "UltraLegacy2017" is the computing campaign name and "Comics" and "ZeroBiasScouting" are subcampaign identifiers.

Some examples of existing subcampaigns:

* [UltraLegacy2018-LowMass](https://cms-pdmv.cern.ch/rereco/subcampaigns?prepid=UltraLegacy2018-LowMass)&#x20;
  * Computing campaign: UltraLegacy2018
  * Subcampaign identifier: LowMass
* [NANOAODRun2DataProd-NanoAODv7\_2016](https://cms-pdmv.cern.ch/rereco/subcampaigns?prepid=NANOAODRun2DataProd-NanoAODv7\_2016)
  * Computing campaign: NANOAODRun2DataProd
  * Subcampaign identifier: NanoAODv7\_2016
* [MiniAODHI18Data-Winter2021](https://cms-pdmv.cern.ch/rereco/subcampaigns?prepid=MiniAODHI18Data-Winter2021)
  * Computing campaign: MiniAODHI18Data
  * Subcampaign identifier: Winter2021

### Subcampaign attributes

* PrepID (`prepid`) - unique identifier of the subcampaign. Made of two parts joined with a dash. Refer to "Subcampaign naming" section for more info.
* CMSSW release (`cmssw_release`) - CMSSW Release name that will be used in all requests created from this campaign. Name must follow the `CMSSW_X_Y_Z[_abc]` pattern
* Enable harvesting (`enable_harvesting`) - whether to automatically add HARVESTING step if there is a sequence with DQM `--step`, will be propagated to the created requests
* Energy (`energy`) - energy in TeV, will be propagated the the created requests
* History (`history`) - history of actions performed on the subcampaign, such as creation or editing. Each entry includes date, user username, action and value
* Memory (`memory`) - memory in MB, will be propagated to the created requests
* Notes (`notes`) - free-form user text&#x20;
* Runs JSON (`runs_json_path`) - path where DCS JSON file is located, this path will be prepended by "[https://cms-service-dqmdc.web.cern.ch/CAF/certification/](https://cms-service-dqmdc.web.cern.ch/CAF/certification/)", so this attribute should be something like "Collisions17/13TeV/DCSOnly/json\_DCSONLY\_LowPU\_eraH.txt"
* Sequences (`sequences`) - list of cmsDriver sequence arguments that will be propagated to the created requests

### Subcampaign actions

* Edit - open editing page of the subcampaign
* Delete - delete the subcampaign. This is allowed only if there are no requests and no tickets with given subcampaign. If there are, they have to be deleted first
* Clone - open a form to create a new subcampaign and prefill form fields with info of given subcampaign
* Requests - show requests that belong to this subcampaign
