---
description: >-
  This is to talk about the SUSY FastSim campaign that is used for signal
  samples.
---

# Fast Simulation Campaigns

The goal of a FastSim campaign is to produce the Gen-Sim and Digi-Reco steps in the same work flow. Doing it this way means that the Gen-Sim is not as precise as it is in FullSim. For example the tracking is . More information about the FastSim code can be found here[ FastSim Twiki](https://twiki.cern.ch/twiki/bin/viewauth/CMS/FastSim).&#x20;

How is it different than a "normal" campaign?&#x20;

* There is no individual GS starting point, so it starts with FSPremix as the first part of the campaign.&#x20;
* That means that the step option in the cmsDriver command will include : GEN,SIM,RECOBEFMIX,DIGI,DATAMIX,L1,DIGI2RAW,L1Reco,RECO
* \--fast is included in the cmsDriver command as an extra option that turns on that FastSim code
* There is a specific era that usually has FAST in the name. If an era is not included, then it will need to be merged in to the CMSSW release via a PR. Please talk to the FastSim group, who will take care of the request.

A pileup premix library needs to be made:

* Prepare the premix library under the PrePremix campaign (example [here](https://cms-pdmv.cern.ch/mcm/campaigns?prepid=RunIIFall17FSPrePremix\&page=0\&shown=63)). Request managers need to manually change the driver of this campaign for the production of the premix library. The PrePremix campaign is used by ALL premix library submissions.
* Ask the production & reprocessing (P\&R) team to allow the use of the MinBias (MB) sample as an allowed input dataset for the PrePremix campaign.
* Submit the premix library.
* As soon as the premix library gets completed, ask the P\&R team to allow the use of this input dataset for the created DRPremix campaign (via a JIRA ticket). Then ask the transfer team to lock it, which may be requested within the same JIRA ticket.

There are five background samples which are required to be produced in any FastSim campaign (i.e. QCD for the JERC group to create FastSim JECs).

* DYJetsToLL\_M-50, TTJets\_DiLept, TTJets\_SingleLeptFromT, TTJets\_SingleLeptFromTbar, QCD\_Pt-15to7000
* For&#x20;
  * DYJetsToLL\_M-50, TTJets\_DiLept, TTJets\_SingleLeptFromT, TTJets\_SingleLeptFromTbar
    * The requester (MC contact) should add LHE to the step's portion of the cmsDriver command.
  * QCD
    * The request manager this is the only DR campaign and is currently being negotiated with computing on how to produce this sample.

In order to produce the MiniAOD and NanoAOD samples a flow must be created, the extra --fast option needs to be included in the cmsDriver command, and the time/size per event should also be checked.&#x20;





