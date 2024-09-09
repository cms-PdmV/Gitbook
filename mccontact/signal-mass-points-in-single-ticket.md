---
description: This will describe how to generalize the fragmentation.
---

# Randomized Parameters

Now instead of producing a 100 tickets with different masses but the same general parameters one ticket can now take care of all the masses in a single ticket.&#x20;

First lets talk about the fragmentation portion of the MCM page. This field is the generator fragment that will be used for the request. It is stored in the [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM) database (or in git genproductions repository which is somewhat out dated now). In the request edit page of [McM](https://twiki.cern.ch/twiki/bin/view/CMS/McM), the free text box can be used to:

* Copy paste a python fragment
* Drag and Drop a file from any local directory
* Edit the text of the fragment

The different portions include:

* A basePythiaParameters which corresponds to PythiaParameters from simple config, for a specific model point

![](../.gitbook/assets/PythiaParameters\_Gen\_Fragment.png)

* List of model points with parameters, weight, & description can be seen here:

![](../.gitbook/assets/model\_points\_GenFragment.png)

ConfigWeight is defined as the relative importance of the model point. A Model point with a weight of 2.0 appears twice as often as a point with a weight of  1.0. This can be driven by filter efficiency, acceptance, etc. There is no need to normalize it.&#x20;

The ConfigDescription is a string that uniquely identifies models. It should contain all relevant parameter values and any other information that is need as a descriptor. An example for the semi visible jets analysis is: SVJ\_mZprime-1000\_mDark-1\_rinv-0.5\_alpha-peak. This is accessed via GenLumiInfoHeader.configDescription().

GridpackPath

* Can be omitted in case of Pythia-only production
* Is located in the: generator.RandomizedParameters
* The location to put them in /cvmfs/cms.cern.ch/phys\_generator/gridpacks/

The other thing that can be added is an SLHATableForPythia8. This is actual a multiline string with SLHA values. This can be omitted for non-SUSY production.

In miniAOD, the configDescription() from GenLumiInfoHeader must be used to identify the exact choice of parameters for any specific signal event. This is a string specified for each PSet in RandomizedParameters, so analyzers or MC contacts must take care to make the string unique for each model point simulated.&#x20;

Also please add a customize command to the cmsDriver of the request: --customise\_commands "process.source.numberEventsInLuminosityBlock = cms.untracked.uint32(200)"

When making changes to the cmsDriver command please also add RP for randomized parameter to the process string field that is on the MCM page. Process string RP

An example that contains all of this is a SUSY request here: [SUSY\_MCM\_Example](https://cms-pdmv.cern.ch/mcm/requests?prepid=SUS-RunIIFall17FSPremix-00009\&page=0\&shown=127)
