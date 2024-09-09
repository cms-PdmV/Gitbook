---
description: >-
  In this page, we collect useful information for Monte Carlo contacts about how
  to act in McM
---

# Monte Carlo contact's corner

### Preliminary steps&#x20;

Let us know your name! When we have the names of all MC subgroup contacts we will create a mailing list.

* [Monte Carlo contacts](https://twiki.cern.ch/twiki/bin/viewauth/CMS/GeneratorContactPersons)

Register to McM using these instructions (**for generator contacts**, not as a normal user):&#x20;

* [https://twiki.cern.ch/twiki/bin/viewauth/CMS/McM#Register](https://twiki.cern.ch/twiki/bin/viewauth/CMS/McM#Register)

Ask the generator conveners [cms-phys-conveners-GEN@cernNOSPAMPLEASE.ch](mailto:cms-phys-conveners-GEN@cernNOSPAMPLEASE.ch) the permission to upload LHE files to EOS disks.

Be subscribed to the following HNs:&#x20;

* to actively use: [https://hypernews.cern.ch/HyperNews/CMS/get/prep-ops.html![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://hypernews.cern.ch/HyperNews/CMS/get/prep-ops.html)
* to ask questions: [https://hypernews.cern.ch/HyperNews/CMS/get/generators.html![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://hypernews.cern.ch/HyperNews/CMS/get/generators.html)
* just to monitor generation status: [https://hypernews.cern.ch/HyperNews/CMS/get/datasets.html![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://hypernews.cern.ch/HyperNews/CMS/get/datasets.html), [https://hypernews.cern.ch/HyperNews/CMS/get/dataopsrequests.htm](https://hypernews.cern.ch/HyperNews/CMS/get/dataopsrequests.html)l [https://hypernews.cern.ch/HyperNews/CMS/get/comp-ops.html](https://hypernews.cern.ch/HyperNews/CMS/get/comp-ops.html)![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)

### A general flow-chart of MC request submission (courtesy of D. Sheffield)&#x20;

![Flow chart of Monte Carlo request submission](https://twiki.cern.ch/twiki/pub/CMSPublic/SWGuideSubgroupMC/sheffield.png)

### &#x20;1- Preparing LHE files&#x20;

Many generators (POWHEG, MadGraph5\_aMCatNLO etc.) use LHE files as a starting point for generation. If you use a generator that does the ME step on the fly (e.g. bare Pythia) just skip this part.&#x20;

* See the dedicated section of [this Twiki](https://twiki.cern.ch/twiki/bin/viewauth/CMS/GeneratorMain) for Matrix Element generators
* If you need help to prepare Madgraph5\_aMCatNLO LHE files, you can contact the cms Madgraph team using the generators hypernews.

There are two ways to technically produce LHE files:&#x20;

* In most cases, you should use campaigns called "xxxwmLHE" to request a central production of the LHE. It can also help to keep track of the sample.
* Only if this is not possible or analysts provide LHE files directly, you can do it "privately", then you can use campaigns called "xxxpLHE"

P.S: It is strongly recommended to check the LHE files locally before uploading, so that we don"t upload the broken LHE files which cause a lot of problem later in production

**xmllint --stream --noout ${file}.lhe > /dev/null 2>&1; test $? -eq 0 || fail\_exit "xmllint integrity check failed on ${file}.lhe"**

#### 1.1 - Using wmLHE campaigns&#x20;

**Only if you want automatic production of LHE files** follow these instructions:&#x20;

* Supported generators for this option are Madgraph5\_aMCatNLO (replaces old MadGraph) and POWHEG v2 (if a process is not yet available in v2, we temporarily accept v1)
* In order to use this option you need to produce first a "gridpack" (Madgraph5\_aMCatNLO) or a executable/grid file tarball (POWHEG). Instructions to produce those can be found at:&#x20;
  * [Madgraph5\_aMCatNLO](https://twiki.cern.ch/twiki/bin/viewauth/CMS/QuickGuideMadGraph5aMCatNLO)
  * [POWHEG](https://twiki.cern.ch/twiki/bin/viewauth/CMS/PowhegBOXPrecompiled)
* **Before** starting the execution of the gridpack/tarball, run\_card.dat or proc\_card.dat cards (for Madgraph5\_aMCatNLO) or powheg.input cards (for POWHEG) should be uploaded to the following repositories (to do that use instructions [here](https://twiki.cern.ch/twiki/bin/viewauth/CMS/GitRepositoryForGenProduction)):&#x20;
  * [production card repository for MadGraph5\_aMCatNLO![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/genproductions/tree/master/bin/MadGraph5\_aMCatNLO/cards/production/)
  * [production card repository for POWHEG![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/genproductions/tree/master/bin/Powheg/production/)
* **Exception**: if you use cards provided in the [example card repository for MadGraph5\_aMCatNLO![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/genproductions/tree/master/bin/MadGraph5\_aMCatNLO/cards/examples) or in the [example card repository for POWHEG![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/genproductions/tree/master/bin/Powheg/examples), without any changes, there is no need to upload them in the production area
* Generator conveners must approve the pull request, at that point the cards can be used for production of gridpack/tarball.
* When you have the gridpack/tarball, this should be copied to this area of [EOS](https://twiki.cern.ch/twiki/bin/view/CMSPublic/EOS) (cmsStage), after creating a proper subdirectory (cmsMkdir):

```
/store/group/phys_generator/cvmfs/gridpacks/<your scram architecture>/13TeV/<your generator>/<your version>/
```

e.g.

```
/store/group/phys_generator/cvmfs/gridpacks/slc6_amd64_gcc481/13TeV/madgraph/V5_2.2.2/
/store/group/phys_generator/cvmfs/gridpacks/slc6_amd64_gcc491/13TeV/powheg/V2/
```

After a few hours these files will be autmatically copied to the cvmfs repository under:

```
/cvmfs/cms.cern.ch/phys_generator/gridpacks/slc...  etc. etc.
```

At this point these are usable for externalLHEProducer. See below. It is possible of course to use already existing gridpacks.&#x20;

#### 1.2 - Using pLHE campaigns&#x20;

**Only if you have produced LHE privately** follow these instructions:&#x20;

* Store them in a temporary directory, e.g. tempdir/.
* In any CMS release, produce a script while using the following command, which aims at translating the LHE into a [EDM](https://twiki.cern.ch/twiki/bin/view/CMSPublic/EDM) roottuple:

```
cmsDriver.py MCDBtoEDM --conditions <conditions for that release> -s NONE \
                                              --eventcontent RAWSIM --datatier GEN \
                                               --filein file:/tmp/covarell/h_PG_TT_TTVBF_90_0.lhe --no_exec -n 1
```

* change the LHESource PSet to have your files as input (it would be good to run on all of them, if possible, to check for single corrupted files) and run normally.&#x20;
* When running the script with cmsRun, if it goes to the end with no exceptions/errors, your LHE files are validated.
* Your LHE files should go in a new directory named as the first available number on /store/lhe. To do this, use the script: [GeneratorInterface/LHEInterface/scripts/cmsLHEtoEOSManager.py![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/genproductions/blob/master/bin/utils/cmsLHEtoEOSManager.py). The command format is:

```
cmsLHEtoEOSManager.py -n --compress -f <list of LHE files separated by comma (no blanks!)>
```

e.g.

```
cmsLHEtoEOSManager.py -n --compress -f tempdir/h_to_tautau_120_1.lhe,tempdir/h_to_tautau_120_2.lhe,tempdir/h_to_tautau_120_3.lhe
```

If the compress option does not work, remove it. **In particular do not use it if the samples are going to be processed in releases < 5.3.8**

* If you have a lot of LHE files with a small number of events in them (typical output of batch queue processing) it may be a good idea to first merge them in a single or a few files. To do this, download the script [mergeLheFiles.cpp](https://twiki.cern.ch/twiki/pub/CMSPublic/SWGuideSubgroupMC/mergeLheFiles.cpp), modify the following line defining the output merged file:

```
std::ofstream outFile("/tmp/covarell/out.lhe", std::ios::out);
```

and perform the following actions:

```markup
g++ -Wall -o mergeLheFiles mergeLheFiles.cpp
ls tempdir/*.lhe > laMiaLista
./mergeLheFiles laMiaLista
```

and you will get a single LHE file called out.lhe.&#x20;

### 2 - Submitting a request in [McM](https://twiki.cern.ch/twiki/bin/view/CMSPublic/McM)

Complete instructions on how to use this tool are [here](https://twiki.cern.ch/twiki/bin/viewauth/CMS/McM). These simple actions are needed to submit a sample:

* Go to [McM![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/)
* Make sure you understand which campaign you want to use. Every base name (e.g. Summer12, RunIIWinter15 etc.) corresponds to a well-defined release cycle and set of DB conditions
* The procedure to follow is different if you have prepared gridpacks/LHE files from the step 1, or if the request does not need a LHE step

#### 2.1 - If starting from LHE files/wmLHE workflows&#x20;

**You must start from a campaign called xxxpLHE or xxxwmLHE**. To create a new request in those campaigns you can follow [creating instructions](https://twiki.cern.ch/twiki/bin/viewauth/CMS/PdmVMcM#Create), but in practice in most cases it is simpler to **clone** an existing sample in a campaign:&#x20;

* Use [cloning instructions](https://twiki.cern.ch/twiki/bin/viewauth/CMS/PdmVMcM#Clone)
* If the original request is very old, use the button "option reset"
* Edit the cloned request&#x20;
  * You can check the "Valid" box and set a number of events n, in the range 0 < n <= nTotal. Do it at your own risk, as the validation may crash badly.&#x20;
  * If this is a "xxxpLHE" request, set "MCDB Id" (= LHE number on eos, see above), otherwise set 0.
  * Put the number of events actually available in the above upload, or less. **Never not put more than this number, e.g. if you have uploaded 199800 events in LHE files, do not round to 200000**
  * Put the cross-section if people in analysis are supposed to use it! If there are better estimations of total cross-section than the present generator (e.g. at higher QCD orders, or from LHC XS WG etc.), then just put 1.0. **Leaving -1 is not OK.**
  * For filter and matching efficiencies always put 1 with error 0. **Leaving -1 is not OK.**
  * Set generators (use the json format that you see in the original request)
  * If this is a "xxxwmLHE" request, put the generator fragment for external LHE production, **otherwise leave blank**. You can copy it by hand in the big window "Fragment":&#x20;
    * Example of xxxwmLHE fragment is here (**just change the tarball name, commented link to cards with specific github revision, eventually the nEvents per job, leave the same configuration for the rest**). Note that for [madgraph\_aMC@NLO](mailto:madgraph\_aMC@NLO) gridpacks, the git revision information is also written in the gridpack\_generation.log inside the tarball if in doubt.:

```c
import FWCore.ParameterSet.Config as cms

# link to cards:
# https://github.com/cms-sw/genproductions/tree/e30fc9c7d9226a2c96869c0ddbe5e65884afd013/bin/MadGraph5_aMCatNLO/cards/production/13TeV/dyellell012j_5f_NLO_FXFX

externalLHEProducer = cms.EDProducer("ExternalLHEProducer",
    args = cms.vstring('/cvmfs/cms.cern.ch/phys_generator/gridpacks/slc6_amd64_gcc481/13TeV/madgraph/V5_2.2.2/dyellell012j_5f_NLO_FXFX/v1/dyellell012j_5f_NLO_FXFX_tarball.tar.xz'),
    nEvents = cms.untracked.uint32(5000),
    numberOfParameters = cms.uint32(1),
    outputFile = cms.string('cmsgrid_final.lhe'),
    scriptName = cms.FileInPath('GeneratorInterface/LHEInterface/data/run_generic_tarball_cvmfs.sh')
)
```

*
  * For time and size per event otherwise just put dummy (= very small) values, e.g. 0.001 s and 30 kB.
  * Put the dataset name following [these rules](https://twiki.cern.ch/twiki/bin/view/CMS/ProductionDataSetNames)

Report at the MC coordination meeting (thursday 3pm) that the request is ready (if the request is very urgent tell directly [hn-cms-prep-ops@cernNOSPAMPLEASE.ch](mailto:hn-cms-prep-ops@cernNOSPAMPLEASE.ch)). The request is accepted (or you will be asked to revise it) and prioritized. **At this point production managers will "chain" the request**, i.e. the system will create automatically a GENSIM request in the campaign with the same xxxGS name (e.g. RunIIWinterpLHE or RunIIWinter15wmLHE will create an entry in RunIIWinter15GS). **This request will not go on automatically** so it is up to you to edit the new request:

*   **First of all**, put the generator fragment for showering/hadronizing/decaying your MC sample. You can copy it by hand in the big window or you give the name and fill in "Fragment tag" the corresponding package tag in github. If you need to upload a new one in github, follow instructions [here](https://twiki.cern.ch/twiki/bin/viewauth/CMS/GitRepositoryForGenProduction). A list of already available fragments is [here![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/genproductions/tree/master/python/). Possible associations:&#x20;

    | [generator at 13 ](https://twiki.cern.ch/twiki/bin/view/CMSPublic/SWGuideSubgroupMC?sortcol=0;table=1;up=0#sorted\_table)[TeV](https://twiki.cern.ch/twiki/bin/edit/CMSPublic/TeV?topicparent=CMSPublic.SWGuideSubgroupMC;nowysiwyg=1) | [fragment](https://twiki.cern.ch/twiki/bin/view/CMSPublic/SWGuideSubgroupMC?sortcol=1;table=1;up=0#sorted\_table)                                                                                                                                               |
    | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | with [FxFx](https://twiki.cern.ch/twiki/bin/edit/CMSPublic/FxFx?topicparent=CMSPublic.SWGuideSubgroupMC;nowysiwyg=1) jet matching (MadGraph\_aMCatNLO at NLO)                                                                          | [link![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/cmssw/blob/CMSSW\_7\_5\_X/Configuration/Generator/python/Hadronizer\_TuneCUETP8M1\_13TeV\_aMCatNLO\_FXFX\_5f\_max1j\_max1p\_LHE\_pythia8\_cff.py) |
    | with MLM jet matching (MadGraph\_aMCatNLO at LO)                                                                                                                                                                                       | [link![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/cmssw/blob/CMSSW\_7\_5\_X/Configuration/Generator/python/Hadronizer\_TuneCUETP8M1\_13TeV\_MLM\_5f\_max4j\_LHE\_pythia8\_cff.py)                   |
    | with POWHEG emission veto (POWHEG)                                                                                                                                                                                                     | [link![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/genproductions/blob/master/python/ThirteenTeV/Hadronizer\_TuneCUETP8M1\_13TeV\_powhegEmissionVeto\_1p\_LHE\_pythia8\_cff.py)                      |
    | generic hadronizer for LO generators with no jet matching                                                                                                                                                                              | [link![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/cmssw/blob/CMSSW\_7\_4\_X/Configuration/Generator/python/Hadronizer\_TuneCUETP8M1\_13TeV\_generic\_LHE\_pythia8\_cff.py)                          |

    * Settings in these files should be adapted to your case (flavor scheme, extra weak particles etc.). In particular if you are using jet matching and **the gridpack is new (created by yourself)** the qCut must be measured (see step 4 on how to measure it)&#x20;
* You should check the "Valid" box and set a number of events n about 30-50.&#x20;
* Put the cross-section if people in analysis are supposed to use it! If there are better estimations of total cross-section than the present generator (e.g. at higher QCD orders, or from LHC XS WG etc.), then just put 1.0 (after hadronization, see step 4 on how to measure it). **Leaving -1 is not OK.**
* Insert sensible filter and matching efficiencies (see step 4 on how to measure them). **Leaving -1 is not OK.**
* Insert sensible timing and size (see step 4 on how to measure them).
* Move the request to the next step (chain validation). In the action box close to the request name, click on "chained request", then in the new page that will appear click on "validate chain" in the action box: when this is completed you will receive a mail from [McM](https://twiki.cern.ch/twiki/bin/view/CMSPublic/McM).
* At that point, if you had activated the validation, you should go back to the request, click on the "Select View" tab above and ticking "Validation": a new column will appear with a link to a DQM page (maybe).&#x20;
  * If the validation fails, you will be notified by email with the logfile attached. So go back and edit the request to fix it.
* In the DQM page, navigate to the proper folder and look in the plots that everything is like you expect and define the request (click "next step" again)

#### 2.2 - If not starting from LHE files&#x20;

**You must start from a campaign called xxxGS, e.g. RunIIWinter15GS**. To create a new request in those campaigns you can follow [creating instructions](https://twiki.cern.ch/twiki/bin/viewauth/CMS/PdmVMcM#Create), but in practice in most cases it is simpler to **clone** an existing sample in a campaign:&#x20;

* Use [cloning instructions](https://twiki.cern.ch/twiki/bin/viewauth/CMS/PdmVMcM#Clone)
* If the original request is very old, use the button "option reset"
* Edit the cloned request&#x20;
  * **First of all**, put the generator fragment for generating your MC sample. You can copy it by hand in the big window or you give the name and fill in "Fragment tag" the corresponding package tag in github. If you need to upload a new one in github, follow instructions [here](https://twiki.cern.ch/twiki/bin/viewauth/CMS/GitRepositoryForGenProduction).&#x20;
  * You should check the "Valid" box and set a number of events n, in the range 30-50.&#x20;
  * Add cross-section (see step 4 how to measure it). **Leaving -1 is not OK.**
  * Add filter and matching efficiencies (see step 4 on how to measure them), if unity, put 1 with error 0. **Leaving -1 is not OK.**
  * Set generators (use the json format that you see in the original request)
  * Set time and size per event (see step 4 on how to measure them).
  * Put the dataset name following [these rules](https://twiki.cern.ch/twiki/bin/view/CMS/ProductionDataSetNames)
* Move the request to the next step (validation) (it's the ">" small symbol besides the request name, in the "view" panel): when this is completed you will receive a mail from [McM](https://twiki.cern.ch/twiki/bin/view/CMSPublic/McM).
* At that point, you should go back to the request, click on the "Select View" tab above and ticking "Validation": a new column will appear with a link to a DQM page (maybe).&#x20;
  * If the validation fails, you will be notified by email with the logfile attached. So go back and edit the request to fix it.
* In the DQM page, navigate to the proper folder and look in the plots that everything is like you expect and define the request (click "next step" again)
* After, report at the MC coordination meeting (thursday 3pm) that the request is ready (if the request is very urgent tell directly [hn-cms-prep-ops@cern.ch](mailto:hn-cms-prep-ops@cern.ch))

### 3 - Checking status&#x20;

To check the status of a submitted request:&#x20;

* Go to the request, click on the "Select View" tab above and ticking "Reqmgr name": a new column will appear with some links ("details", "stats", etc.). Click on the small eye close to the links to see a graph of the sample status.&#x20;

### 4 - Additional things&#x20;

There are some quantities you have to measure so that the production team knows the properties of the request, to go ahead with the central production. Filter efficiency can be measured while running just the GEN step, while the timing and size are the time needed to run one GENSIM event and its size.

To start this procedure go on the "Get setup" button of the request and check that the output is correct (N.B. for this you need to upload the generator decay fragment before!).

#### Measure filter efficiencies and cross-section&#x20;

You need this step if:&#x20;

* you want to measure a cross-section after hadronization (for backgrounds, for signal there are precise estimates from the LHC cross-section WG already)
* you have filters on final state particles, so filter efficiency is smaller than 1
* you have jet matching cuts, so matching efficiency is smaller than 1

If you don't need this step all numbers above are 1, just proceed to "Measure time and size".

Use the script [CmsDrivEasier.sh](https://twiki.cern.ch/twiki/pub/CMSPublic/SWGuideSubgroupMC/CmsDrivEasier.sh) in this way:

```
source CmsDrivEasier.sh <request or chained request McM ID> <n> 1 
```

e.g.

```
source CmsDrivEasier.sh HIG-Fall13-00001 10000 1     or
source CmsDrivEasier.sh SMP-chain_Summer12WMLHE_flowLHE2S12_flowS12to53-00008 10000 1 
```

where n is a sufficient number of events to measure precisely the efficiency, e.g. if the efficiency is expected to be o(1/100) you could use 100000 events. E.g.&#x20;

In the output look for the string "GenXsecAnalyzer". Below this you have a detailed logging of the needed quantities.

#### Measure proper value of qCut&#x20;

You need this step if you have jet matching cuts.

Do all steps of the paragraph above, using a lot of events and a reasonable starting qCut: this should be about 1.5-2 times larger than the ptj or xqcut parameter used in ME generation. You should find a root file in the end in `/tmp/<your username>/<request ID>.root` . Then download [this macro![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/genproductions/blob/master/bin/MadGraph5\_aMCatNLO/macros/plotdjr.C) and run in ROOT as:

```
root [0] .x plotdjr.C("/tmp/<your username>/<request ID>.root","test.root")
```

test.root will contain a canvas which shows plots of differential jet distributions separated according to the number of original partons in an event. Of course histograms and plots do not match perfectly because additional jets are created by the parton shower: in fact, for the plot corresponding to the i-th jet, you have a sharp drop at pT = qCut of the sample with i-1 partons and a sharp rise of the sample with i partons.&#x20;

* You should check that the TOTAL jet rate distributions appear smooth at pT \~ qCut.&#x20;
* If there is a kink somewhere, try with a larger qCut, if there is a dip try with a smaller one.&#x20;
* Repeat until you find smooth distributions.&#x20;

#### Measure timing and size&#x20;

Use the script [CmsDrivEasier.sh](https://twiki.cern.ch/twiki/pub/CMSPublic/SWGuideSubgroupMC/CmsDrivEasier.sh) in this way:

```
source CmsDrivEasier.sh <request or chained request McM ID> <n> 2 
```

e.g.

```
source CmsDrivEasier.sh HIG-Fall13-00001 30 2     or
source CmsDrivEasier.sh SMP-chain_Summer12WMLHE_flowLHE2S12_flowS12to53-00008 30 2
```

where 30 (or 30/filter efficiency if filter efficiency is not 1) if is usually a sufficient number of events to measure time and size&#x20;

* In the end of the output, you get the needed statistics:&#x20;
  * AvgEventTime is the value to fill for time/event (in sec)
  * Timing-tstoragefile-write-totalMegabytes divided by TotalEvents is the size/event (in MB, in [McM](https://twiki.cern.ch/twiki/bin/view/CMSPublic/McM) you have to change to kB)

#### Validation failure because of non existing wmLHE dataset&#x20;

If a GENSIM request is chained to a wmLHE request that was produced far in the past, validation may fail because it is run at CERN, but files of the LHE dataset could have been moved elsewhere in the meantime. In that case you need to request a [PhedEx](https://twiki.cern.ch/twiki/bin/edit/CMSPublic/PhedEx?topicparent=CMSPublic.SWGuideSubgroupMC;nowysiwyg=1) transfer.

* You click on one "input dataset" you need from [McM](https://twiki.cern.ch/twiki/bin/view/CMSPublic/McM) GS request page (or output dataset in wmLHE request page), it will direct you to the [PheDeX](https://twiki.cern.ch/twiki/bin/edit/CMSPublic/PheDeX?topicparent=CMSPublic.SWGuideSubgroupMC;nowysiwyg=1) page.
* Click on "Subscribe to [PhEDEx](https://twiki.cern.ch/twiki/bin/view/CMSPublic/PhEDEx)".
* On the first box, you will see that dataset. You can put all datasets you need in the same box.
* Choose T2\_CH\_CERN.
* Choose [AnalysisOps](https://twiki.cern.ch/twiki/bin/edit/CMSPublic/AnalysisOps?topicparent=CMSPublic.SWGuideSubgroupMC;nowysiwyg=1).
* Add reason, i.e. For [McM](https://twiki.cern.ch/twiki/bin/view/CMSPublic/McM) validation.
* Click Accept.
* Please ping prep-ops HN, so we can approve quickly.
