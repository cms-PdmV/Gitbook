---
description: >-
  In this page, we describe the general ideas and steps of the central Monte
  Carlo production
---

# Monte Carlo Management (McM): introduction

Central Monte Carlo production in CMS is organized in different campaigns. Each of them produce a certain output ("datatier") which contains different information, related to which step is executed in the cmsDriver (click [here](https://monte-carlo-production-tools.gitbook.io/project/experts-corner/cmsdriver-argument-and-meaning) for more infos). The campaigns are executed as chains, namely the output of the previous campaign serves as input for the next one.

Generally, one goes through the following campaigns:

**GEN-SIM**: starts from a Monte Carlo generator, produces events at generator level (the four vectors of the particles) and simulates the energy released by the particles in the crossed detectors. Important parameters for such campaigns are:

* Beamspot
* Generator fragment (specifies the process which needs to be generated)
* Detector geometry

The output format of this campaign is generally an GEN-SIM sample.

**DIGI-RECO:**  the simulated detector signals are digitized and reconstruction algorithms are applied on top. In this process, pile-up is also included in the simulation. Trigger menu information also appears as output of this campaign. Important parameters for such campaigns are:

* Pile-up input dataset name (either a sample with pre-processed and pre-mixed events which are just added on top of the simulated events or a GEN-SIM MB sample)
* Pile-up scenario (in case the GEN-SIM MB sample is given as input)

The output format of this campaign is generally an AODSIM sample.

**MINIAOD:** the produced DIGI-RECO events are skimmed and reduced in size by running the MiniAOD module, which saves information of physics objects which can be directly used for analyses.&#x20;

The output format of this campaign is a MINIAODSIM sample.

**NANOAOD:** the produced MINIAOD events are further skimmed and further reduced in size. The idea of NanoAOD format is to have a plain-root sample, which can be analyzed outside any CMSSW environment.&#x20;

The output format of this campaign is a NANOAODSIM sample.

A summary of the whole workflow is summarized in the following table.

*

![Credits: Gurpreet Chahal](<.gitbook/assets/image (13).png>)

