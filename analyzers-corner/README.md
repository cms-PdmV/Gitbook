---
description: >-
  In this page, we give a basic explanation of the glossary, needed for
  analysers to understand the logic of the central MC production
---

# Analyzer's corner

## Types of root requests in McM:

*   wmLHE: Les Houches Event production, produced with WMAgent (Workload

    Management System)
* wmLHEGS: LHE and GEN-SIM production in single step (default way)
* pLHE: private or personal LHE files
*   Pythia (GEN-SIM): The generator which can do both hard scattering and hadronization

    • Its input can be LHE file
* wmLHE and pLHE steps are the step that produces hard scattering processes, and then stores those events in EDM format (i.e. genParticles), which can be used later by hadronizer

## Campaign:&#x20;

A central platform in McM used to produce a set of requests sharing the same physics goal, software release, c.o.m. energy and event processing configuration. e.g. GENonly, GEN-SIM, wmLHE, WMLHEGS, DIGI-RECO, DIGIonly, etc.

## Chained campaign:&#x20;

A sequence of campaigns connected by flows determining the sequence of processing steps/campaigns needed to deliver datasets for analysis.

## Chained request:&#x20;

Several requests can be created with a chained campaign, and a specific member of a chained campaign, made from existing requests is chained request.

## Dataset name format

The dataset name of a sample is unique and follows the rules below:

/PRIMARY\_DATASET/CampaignName-ProcessString\_GT/DATATIER

/PRIMARY\_DATASET/CampaignName-ProcessString\_GT-v**XXX**/DATATIER

(where XXX is the version number in case there were multiple resubmission of the same sample)

/PRIMARY\_DATASET/CampaignName-ProcessString\_GT-ext**XXX**/DATATIER

(where XXX is the extension number in case two similar samples were submitted as extensions, namely the same process has been generated in two independent generations).

Examples are the following:

/Graviton2PBToZZTo2L2Q\_width0p2\_M-1200\_13TeV-JHUgenV7-pythi8/RunIISummer16MiniAODv3-PUMoriond17\_94X\_mcRun2\_asymptotic\_v3-v2/MINIAODSIM

/QCD\_Pt\_3200toInf\_TuneCP5\_13TeV\_pythia8/RunIIFall18GS-pilot\_102X\_upgrade2018\_realistic\_v11-v2/GEN-SIM

/VBFHToGG\_M120\_13TeV\_amcatnlo\_pythia8/RunIIAutumn18DRPremix-102X\_upgrade2018\_realistic\_v15-v1/AODSIM

N.B. Extension samples are always independent of each other and can be used together (combined) in the analysis.

*
*
