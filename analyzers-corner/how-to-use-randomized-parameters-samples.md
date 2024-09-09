---
description: >-
  Randomized parameters is a sample generation method in which a whole signal
  grid is generated in a single dataset. This page documents the use of such
  samples for analyzers.
---

# How to use randomized parameters samples

## Randomized parameters

Randomized parameters (RP) is a method used to generate a whole signal grid in a single dataset, rather than creating a dataset for each signal point (see [Randomized Parameters](../mccontact/signal-mass-points-in-single-ticket.md) for how to create a RP dataset, i.e. instructions for MC contacts). At each lumisection transition, a signal point is randomly chosen. For very large (>\~100) signal scans, RP has several advantages:

* Significantly reduced overhead for MC contacts, PDMV, computing, and analysis teams.
* More robust against job failures (event losses are spread evenly across the signal grid, instead of concentrated in a single point).

On the other hand, RP has a few disadvantages, mostly related to it being relatively new to CMS. See below for use cases that are not yet supported.

To use the samples, analyzers will need to separate the signal scan into individual signal points. To summarize, the signal points are identified by a unique string in the `GenLumiInfoHeader` object, which can be retrieved using the method `GenLumiInfoHeader::configDescription()`. In NanoAOD, the string identifiers are translated into boolean branches. See the next sections for detailed examples.

## How to use: MiniAOD

_Example courtesy of Kevin Pedro (_[_https://github.com/TreeMaker/TreeMaker/blob/Run2\_2017/Utils/src/SignalScanProducer.cc_](https://github.com/TreeMaker/TreeMaker/blob/Run2\_2017/Utils/src/SignalScanProducer.cc#L127-L139)_)._&#x20;

To use a MiniAOD sample with randomized parameters, you'll need add something like the following to the `beginLuminosityBlock()` method :

```
void MyNtuplizer::beginLuminosityBlock(edm::LuminosityBlock const& iLumi, edm::EventSetup const& iSetup)
{
		edm::Handle<GenLumiInfoHeader> gen_header;
		iLumi.getByToken(genLumiHeaderToken_, gen_header);
		std::string scanId_ = gen_header.configDescription();
		// Up to you to decide how to use the string (should probably be a member variable):
		// - Add branch to output ntuple
		// - Make unique ntuple for each signal point
}

```

In the above example, the signal point identifier (a `std::string`) is read from `GenLumiInfoHeader::configDescription()` into the member variable `scanId_`. It's up to the analyzer to determine how to use this string. For example:

1. It can be added directly to the output ntuple (not very efficient).
2. Following NanoAOD, a boolean branch can be added for each signal point.&#x20;
3. A separate TTree can be created for each signal point.&#x20;

See  [https://indico.cern.ch/event/816207/contributions/3410168/attachments/1835934/3008052/randomizedparameters\_tutorial\_apr\_29\_2019.pdf](https://indico.cern.ch/event/816207/contributions/3410168/attachments/1835934/3008052/randomizedparameters\_tutorial\_apr\_29\_2019.pdf) for a specific implementation combining options (2) and (3) (some of the links are broken, but the code can be found in the github link above).

## How to use: NanoAOD

In NanoAOD v6 and newer, a boolean branch is created for each signal point, where the branch name is `GenModel_<signal point identifier>`. For each event, one and only one branch should have the value `True`, and the rest should be `False`. For example, the branch list for this dataset:`/DarkHiggs_MonoJet_LO_TuneCP5_13TeV-madgraph-pythia8/RunIIAutumn18NanoAODv7-Nano02Apr2020_rp_102X_upgrade2018_realistic_v21-v1/NANOAODSIM` contains the following:

```
>> root -l root://xrootd-cms.infn.it//store/mc/RunIIAutumn18NanoAODv7/DarkHiggs_MonoJet_LO_TuneCP5_13TeV-madgraph-pythia8/NANOAODSIM/Nano02Apr2020_rp_102X_upgrade2018_realistic_v21-v1/70000/9CC2B10A-A1F7-784A-A575-8AEA97C084FE.root
root [0] 
Attaching file root://xrootd-cms.infn.it//store/mc/RunIIAutumn18NanoAODv7/DarkHiggs_MonoJet_LO_TuneCP5_13TeV-madgraph-pythia8/NANOAODSIM/Nano02Apr2020_rp_102X_upgrade2018_realistic_v21-v1/70000/9CC2B10A-A1F7-784A-A575-8AEA97C084FE.root as _file0...
(TFile *) 0x4183150
root [1] Events->Print("GenModel_*")
******************************************************************************
*Tree    :Events    : Events                                                 *
*Entries :    73282 : Total =       439813623 bytes  File  Size =   90334522 *
*        :          : Tree compression factor =   4.86                       *
******************************************************************************
*Br    0 :GenModel_DarkHiggs_MonoJet_LO_MZprime_1995_Mchi_1000_TuneCP5_13TeV_madgraph_pythia8 : *
*         | Bool_t EventString bit                                           *
*Entries :    73282 : Total  Size=      76059 bytes  File Size  =       3341 *
*Baskets :       13 : Basket Size=      16384 bytes  Compression=  22.53     *
*............................................................................*
*Br    1 :GenModel_DarkHiggs_MonoJet_LO_MZprime_500_Mchi_500_TuneCP5_13TeV_madgraph_pythia8 : *
*         | Bool_t EventString bit                                           *
*Entries :    73282 : Total  Size=      76027 bytes  File Size  =       3319 *
*Baskets :       13 : Basket Size=      16384 bytes  Compression=  22.67     *
*............................................................................*
*Br    2 :GenModel_DarkHiggs_MonoJet_LO_MZprime_200_Mchi_150_TuneCP5_13TeV_madgraph_pythia8 : *
*         | Bool_t EventString bit                                           *
*Entries :    73282 : Total  Size=      76027 bytes  File Size  =       3323 *
*Baskets :       13 : Basket Size=      16384 bytes  Compression=  22.64     *
*............................................................................*
...etc
```

As for MiniAOD, it's up to you to determine how to handle separating the signal points using these branches.&#x20;

## Caveats

* The GenXsecAnalyzer tool doesn't support randomized parameters (yet).&#x20;
  * It runs over the entire dataset ignoring the randomized parameters aspect, and hence returns the average cross section of the signal scan.&#x20;
  * Further, GenXsecAnalyzer returns incorrect values for randomized parameter datasets with jet merging. The information required to account for the merging efficiency is unfortunately not propagated through the GEN step. The GEN group is investigating how to solve this issue, but for now, it's probably easiest to compute the cross sections privately, running a small GEN job for each point.&#x20;
* In NanoAOD\_v6, the `GenModel_*` branch names might contain dashes, which interferes with `TTree:Draw()` and other methods that interpret a string (the dash is interpreted as a minus sign).
  * This is fixed in NanoAOD\_v7: the dashes are replaced with underscores.

