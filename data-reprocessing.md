---
description: >-
  This page aims for explaining how to perform data reprocessing from the
  available tools in cmssw. Adapted from twiki page by Francesco Fabozzi.
---

# Data reprocessing (old injection method via script)

### Introduction and references&#x20;

In general, we identify several types of data reprocessings:&#x20;

* The **light** reprocessings where only a subset of the primary datasets and runs are taken into account, without skims. In general, these reprocessings are motivated by particular needs and are performed upon request of a particular area of the collaboration.
* The **complete** reprocessings, which consider all the primary datasets (or at least all the ones of interest for physics analysis, as agreed at coordination level), all the runs (collision and commissioning) and all the active skims.
* The **re-MiniAOD** reprocessing, where only [MiniAOD](https://twiki.cern.ch/twiki/bin/view/CMS/MiniAOD) are re-done starting from [AOD](https://twiki.cern.ch/twiki/bin/view/CMS/AOD) input datasets. No re-reco and re-skimming is performed.
* The **NanoAOD** (re)processing, where only [NanoAOD](https://twiki.cern.ch/twiki/bin/edit/CMS/NanoAOD?topicparent=CMS.PdmVReRecoScriptInstructions;nowysiwyg=1) are (re)done starting from [MiniAOD](https://twiki.cern.ch/twiki/bin/view/CMS/MiniAOD) input datasets. No re-reco and re-skimming is performed.

We keep track of all reprocessings in the [PdmVDataReprocessing](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVDataReprocessing) twiki. There are dedicated twiki pages for each reprocessing campaign, where here one can access all details about datasets, configuration, status.

The tool to inject a re-processing wf is the `wmcontrol.py` script. Detailed instructions on the tool are provided in the [PdmVProductionManagerInstructions](https://twiki.cern.ch/twiki/bin/view/CMS/PdmVProductionManagerInstructions) twiki.

In this twiki we collect some practical recipes for preparation and injection of reprocessing workflows. The examples decribed here are based on the legacy reprocessing of 2016 data or first reprocessings of 2017 data.

### Procedure when opening a campaign&#x20;

When we open a new data reprocessing campaign, we notify comp-ops via a JIRA ticket and ask to enable one workflow as a pilot (inject a workflow with a limited set of runs to not take too long). We will use the JIRA ticket to follow-up about the pilot workflow. Example [here![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://its.cern.ch/jira/browse/CMSCOMPPR-2185).

**REMEMBER**: make sure to add the [UnifiedOfficer](https://twiki.cern.ch/twiki/bin/edit/CMS/UnifiedOfficer?topicparent=CMS.PdmVReRecoScriptInstructions;nowysiwyg=1) label and assign the ticket to Marc Gabriel Weinberg.

If the pilot is OK, then the campaign will be enabled and all the workflows submitted in the campaign will be automatically assigned.

### Injection of re-reco workflows using wmcontrol.py&#x20;

The command to inject a re-reco wf in the computing system is:

`wmcontrol.py --req_file=master.conf`

In the above command, `master.conf` is a configuration file where the parameters of the workflows are specified. It is adviced, before the actual injection, to printout and check the dictionary of the parameters sent to computing with:

`wmcontrol.py --test --req_file=master.conf`

You can find below an example of a master.conf file. Several sections can be identified. The first section (`[DEFAULT]`) specifies the parameters that will be attributed by default to each workflow, if not overwritten in the other sections. The other sections (one section for each of the workflows, such as `[Run2016D-v2-MuonEG-18Apr2017]`) define the parameters that are unique for each workflow (such as the input dataset and the run list) and eventually overwrite the parameters of the default section.

Some of the parameters are self explicative. The setting of the processing\_string (= the string which identifies that particular re-reco and will enter in the re-recoed dataset name) and the campaign name (=era name) reflect the present convention. The `cfg_path` specifies the cmsRun re-reco configuration file, which is different for each dataset. The requestID identifies the workflow sent to computing and must be unique.

```
[DEFAULT] 
group=ppd 
user=fabozzi 
request_type=ReReco 
release=CMSSW_8_0_28 
globaltag=80X_dataRun2_2016LegacyRepro_v3 

campaign=Run2016D

processing_string=18Apr2017 

priority=85000 
time_event=4 
size_event=500 
size_memory = 7000 
multicore=4 
harvest_cfg=harvesting.py 

[Run2016D-v2-MuonEG-18Apr2017]
dset_run_dict={"/MuonEG/Run2016D-v2/RAW" : [276315, 276317, 276318, 276326, 276327, 276352, 276355, 276357, 276361, 276363, 276384, 276437, 276453, 276454, 276458, 276495, 276501, 276502, 276525, 276527, 276528, 276542, 276543, 276544, 276545, 276581, 276582, 276583, 276584, 276585, 276586, 276587, 276653, 276655, 276659, 276775, 276776, 276794, 276807, 276808, 276810, 276811] }
cfg_path=recoskim_Run2016D_MuonEG.py
request_id=ReReco-Run2016D-MuonEG-18Apr2017-0001 
priority=90000 

[Run2016D-v2-Tau-18Apr2017]
dset_run_dict={"/Tau/Run2016D-v2/RAW" : [276315, 276317, 276318, 276327, 276352, 276355, 276357, 276361, 276363, 276384, 276437, 276453, 276454, 276458, 276495, 276501, 276502, 276525, 276527, 276528, 276542, 276543, 276544, 276545, 276581, 276582, 276583, 276584, 276585, 276586, 276587, 276653, 276655, 276659, 276775, 276776, 276794, 276807, 276808, 276810, 276811] }
cfg_path=recoskim_Run2016D_Tau.py
request_id=ReReco-Run2016D-Tau-18Apr2017-0002 
```

### An introductory tutorial&#x20;

Injection of a data reprocessing workflow is not much different as injection of any other workflow (for instance a relval workflow).

It requires basically:&#x20;

* A CMSSW production release
* The cmsRun configuration file(s) of the steps of the workflow, that are produced by cmsDriver(s)
* A set of parameters associated to the workflow needed by computing, that have to be compliant with WMAgent specifications

The configuration files and the computing parameters will be sent to computing system when injecting.

Like runTheMatrix for relvals, that can be considered as a user-interface script to prepare and inject the the workflows, also for data re-reco we have a user interface script: wmcontrol.py. The script uses a .conf configuration file to specify:&#x20;

* location of the cmsRun configuration files
* parameters for computing that will be used to create the dictionary for WMAgent

The usage is `wmcontrol.py --req_file=master.conf`.

The CMSSW release working areas and configurations for official reprocessings are stored in a common [PdmV](https://twiki.cern.ch/twiki/bin/view/CMS/PdmV) area: /afs/cern.ch/cms/PPD/PdmV/work/

Here we have&#x20;

* reprocessingW13 (for reprocessing until 2016 data)
* reprocessing2017 (for reprocessing 2017 data)
* reprocessing2018 (for reprocessing 2018 data)

#### Preparation of config files&#x20;

The files used for this tutorial are in:

```
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/test_2017Binjection
```

In this example we consider a full data re-reco on the [SingleMuon](https://twiki.cern.ch/twiki/bin/edit/CMS/SingleMuon?topicparent=CMS.PdmVReRecoScriptInstructions;nowysiwyg=1) PD of 2017 data for a few runs of 2017B era. A full data re-reco starts from RAW input dataset and re-does the [RECO](https://twiki.cern.ch/twiki/bin/view/CMS/RECO), SKIM (if needed), ALCARECO (if needed), miniAOD and [DQM](https://twiki.cern.ch/twiki/bin/view/CMS/DQM). The [HLT](https://twiki.cern.ch/twiki/bin/view/CMS/HLT) is never re-done in data reprocessing.

The SKIMs and ALCARECOs to be run for each primary dataset are deployed into the release in the [Skim Matrix![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/cmssw/blob/master/Configuration/Skimming/python/autoSkim.py) and [AlcaReco Matrix![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-sw/cmssw/blob/master/Configuration/AlCa/python/autoAlca.py). NOTE: in a reprocessing, we do not necessarily run all the SKIMs associated to a primary dataset, but only the ones agreed in advance with the groups. Similarly, for ALCARECOs an up-to-date [AlcaRecoMatrix](https://twiki.cern.ch/twiki/bin/edit/CMS/AlcaRecoMatrix?topicparent=CMS.PdmVReRecoScriptInstructions;nowysiwyg=1) w.r.t. the release can be provided by [AlCa](https://twiki.cern.ch/twiki/bin/view/CMS/AlCa) for the reprocessing.

Create a CMSSW working area (the production release for a reprocessing has been established in advance: this is usually a production release, only for very very exceptional cases it is a pre-release)

```
scramv1 project -n CMSSW_9_2_3_patch2_Commissioning2017 CMSSW CMSSW_9_2_3_patch2
cd CMSSW_9_2_3_patch2_Commissioning2017/src
```

Source the usual script to setup [PdmV](https://twiki.cern.ch/twiki/bin/view/CMS/PdmV) tools

```
source /afs/cern.ch/cms/PPD/PdmV/tools/subSetupAuto.sh 
```

Let’s work in a sub-directory

```
mkdir test_2017Binjection 
cd test_2017Binjection
```

Produce the cfg file for the reprocessing with cmsDriver. The cmsDriver to be used must have been inspected in advance (not last minute, but possibly weeks in advance...) by all the relevant experts: offline, [AlCa](https://twiki.cern.ch/twiki/bin/view/CMS/AlCa), miniAOD, etc.. This is done by an explicit request on prep-ops hypernews + CC the experts. An example [here![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://hypernews.cern.ch/HyperNews/CMS/get/prep-ops/3909.html) (many more examples are in prep-ops hypernews).

The starting point to set up a re-reco cmsDriver is of course the cmsDriver used for data relvals + any needed special GT or customisation. For this tutorial you can start from the cfg here:

```
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/test_2017Binjection/recoskim_Run2017B_SingleMuon.py
```

and read the cmsDriver used to create it. Now, you can re-create the file by yourself. In the same area there are a few more examples of cfg files.

Produce the cfg file for the harvesting step. This is needed if you have included the [DQM](https://twiki.cern.ch/twiki/bin/view/CMS/DQM) step in the cmsDriver for re-reco. Again you can take the cfg file from here:

```
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/test_2017Binjection/harvesting.py
```

Test locally the re-reco cmsDriver to guarantee that it does not crash before injecting into computing. For the local test, you need to specify in the cmsDriver the number of events you want to run (e.g. 10 events) and the input file (that must be accessible, of course). There is an example of cfg for a local test here:

```
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/test_2017Binjection/local_test/recoskim_Run2017B_ZeroBias2TEST.py
```

When we start a new reprocessing campaign we also need to make local test for another reason: indeed we want to estimate parameters (time\_event, size\_event, size\_memory) to be written in the master.conf file. The time\_event parameter it is used by computing to make the job splitting. The size\_memory parameter refers to RSS memory of the job, and it used by computing to assign to computing resources with enough memory. In this case, it is suggested to run on at least 100 events to get reliable estimates for these parameters. Also, a monitoring utility has to be added into the cmsDriver

```
--customise Configuration/DataProcessing/Utils.addMonitoring 
```

and run the local test in this way:

```
cmsRun -e -j file.xml file_cfg.py
```

The output xml file will be used to find for instance `PeakValueRss` value for memory.

**Note** : test locally the recoskim\_Run2017B\_SingleMuon.py (cmsRun recoskim\_Run2017B\_SingleMuon.py) to check output files and parameter values (produced root files are needed to estimate the time\_event = rootfilesum/run\_time)

#### Preparation of master.conf&#x20;

Once we have the cfg files for cmsRun, then we have to edit the master.conf file for wmcontrol.py. You can take the master.conf file from here and change where it is needed:

```
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/test_2017Binjection/master.conf
```

The file content appears like this:

```
[DEFAULT] 
group=ppd 
user=fabozzi
request_type=ReReco 
release=CMSSW_9_2_3_patch2 
globaltag=92X_dataRun2_Jun23ReReco_PixelCommissioning 

campaign=Commissioning2017
acquisition_era=Run2017B

processing_string=23Jun2017 

priority=500000 
time_event=4 
size_event=500 
size_memory = 7000 
multicore=4 
harvest_cfg=harvesting.py 

[Run2017B-v1-SingleMuon-23Jun2017]
dset_run_dict={"/SingleMuon/Run2017B-v1/RAW" : [297099, 297113, 297175, 297176, 297215, 297219, 297281, 297286, 297292] }
cfg_path=recoskim_Run2017B_SingleMuon.py
request_id=ReReco-Run2017B-SingleMuon-23Jun2017-0003
```

Note that release must match the release you are working on and globaltag must match the GT used in cmsDrivers of cfg files.

Note that for 2017 data rereco we now distinguish `campaign` parameter (i.e. a conventional name to identify reprocessings of same tipology), `acquisition_era` parameter (to specify the era of the RAW dataset), and `processing_string` parameter (a conventional date to specify a certain reprocessing setup under a campaign).

NOTE: `acquisition_era` and `processing_string` will appear into the re-recoed dataset name, while `campaign` will not.

Until 2016 data reprocessings, only `acquisition_era` was specified and by default `campaign = acquisition_era`. In 2017 data reprocessings we are distinguishing the two parameters.

Priority is a number to specify priority of the workflow in computing. Higher number gives higher priority. There are some conventional numbers ( [blocks![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://github.com/cms-PdmV/cmsPdmV/blob/v1.4.11/mcm/tools/priority.py)) that are used for MC production, but in principle you can use any number.

Other parameters are `multicore` that must match to `-- nThreads` in the cmsDriver of [RECO](https://twiki.cern.ch/twiki/bin/view/CMS/RECO) cfg and `harvest_cfg` if you have a harvesting cfg file.

The parameters in the `[DEFAULT]` section are common to all the workflows.

Then, under `[Run2017B-v1-SingleMuon-23Jun2017]` we specify parameters that are specific to each workflow. These are basically `dset_run_dict` to specify input dataset and run numbers, `cfg_path`, that is the cfg file to be used for that workflow, and a `request_id` string to identify that workflow into computing system.

**To calculate time/event, size/event and memory peak, you can use this script here, which runs on a xml file, called report.xml:**

[**https://github.com/pgunnell/ReRecoProcessing/blob/master/scriptforcheck.sh**](https://github.com/pgunnell/ReRecoProcessing/blob/master/scriptforcheck.sh)

RSS memory is in MB in file.xml => size\_memory 14000 = 14GB (all cms resources are now > 14 GB so don't need to change unless the [PeakRss](https://twiki.cern.ch/twiki/bin/edit/CMS/PeakRss?topicparent=CMS.PdmVReRecoScriptInstructions;nowysiwyg=1) return bigger value)

size\_event in kB rootfilesize/#testrunevents so if 100 evts (better run at least 500evts) with root 2.6M (ls -lh in the directory) then size\_event= 26kB

time\_event = #events/runtime in seconds

#### Injection with wmcontrol.py&#x20;

Before injecting, it is important to printout the set of parameters associated to that workflow:

```
wmcontrol.py --test --req_file=master.conf
```

You can compare with printout of a relval workflow to see that they are similar.

For the final injection:

```
wmcontrol.py --req_file=master.conf
```

### Using a script to prepare configuration files: prepare\_cfg.py&#x20;

For major reprocessings of CMS data we need to inject tens of workflows for each era, each of them with specific CMSSW cfg file and computing parameters.

Therefore it is useful to prepare CMSSW cfg files and the master.conf file via a script. The example described below is based on the script employed for 2016 legacy re-reco.

You can take the script `prepare_conf.py` as well as the main script `prepare_conf_2016H.py` from the following directory:

```
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/prepare_cfg/prepare_conf.py
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/prepare_cfg/prepare_conf_2016H.py
```

In order to run this example, you also need a local copy of `autoSkim.py` because we do not want to run all the possible skims in the release (as explained in the above sections):

```
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/prepare_cfg/autoSkim.py
```

Instead, the autoAlca matrix is taken from the release, so you do not need a local copy.

The main script `prepare_conf_2016H.py` simply sources `prepare_conf.py` and launch a prepare() function with the following parameters as arguments: acquisition era, proc\_string, and GT:

```
from prepare_conf import prepare
prepare(era = "Run2016H", proc_string = "18Apr2017", GT = "80X_dataRun2_2016LegacyRepro_v3")
```

You can launch the main script as follows:

```
source /afs/cern.ch/cms/PPD/PdmV/tools/subSetupAuto.sh 
ipython prepare_conf_2016H.py
```

You can also use option -i if you do not want to get off the ipython environment at the end.

The output will be a directory ("Run2016H" in this case) containing:&#x20;

* cmsRun cfg files for each dataset: `recoskim_Run2016H_xxx_cfg.py`
* a harvesting cfg `harvesting.py`
* the master.conf file for the [Run2016H](https://twiki.cern.ch/twiki/bin/edit/CMS/Run2016H?topicparent=CMS.PdmVReRecoScriptInstructions;nowysiwyg=1) workflows injection: `master_Run2016H.conf`
* a summary table of all datasets and runs to be copied in the re-reco twiki `twiki_Run2016H.twiki`

In the same repository you can find also updated versions employed for 2017 re-reco:

```
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/prepare_cfg/prepare_conf_FOR2017.py
/afs/cern.ch/user/f/fabozzi/workspace/public/CMSSW_9_2_3_patch2_Commissioning2017/src/prepare_cfg/prepare_conf_2017B.py
```

#### Tutorial: how the script works&#x20;

In the following, we will briefly explain the main features of the `prepare_conf.py` script, so that you can adapt to your needs.

We first import some libraries:

```
import os
import  sys,time,json
from    dbs.apis.dbsClient import DbsApi
from    time import gmtime
import commands
url="https://cmsweb.cern.ch/dbs/prod/global/DBSReader"
api=DbsApi(url=url)
```

In particular, the DbsApi will be used to make queries for the datasets, runs, etc.

We also import the (local) autoSkim and the (release) autoAlca:

```
from autoSkim import autoSkim
from Configuration.AlCa.autoAlca import AlCaRecoMatrixRereco
```

We specify a dictionary of customise to be used in reco cmsDriver, since the customise can be different for each era:

```
 customera = {}
    customera["Run2016B"] = 'Configuration/DataProcessing/RecoTLR.customisePostEra_Run2_2016,RecoTracker/Configuration/customizeMinPtForHitRecoveryInGluedDet.customizeHitRecoveryInGluedDetTkSeedsOnly'
    customera["Run2016C"] = 'Configuration/DataProcessing/RecoTLR.customisePostEra_Run2_2016,RecoTracker/Configuration/customizeMinPtForHitRecoveryInGluedDet.customizeHitRecoveryInGluedDetTkSeedsOnly'
    customera["Run2016D"] = 'Configuration/DataProcessing/RecoTLR.customisePostEra_Run2_2016,RecoTracker/Configuration/customizeMinPtForHitRecoveryInGluedDet.customizeHitRecoveryInGluedDetTkSeedsOnly'
    customera["Run2016E"] = 'Configuration/DataProcessing/RecoTLR.customisePostEra_Run2_2016,RecoTracker/Configuration/customizeMinPtForHitRecoveryInGluedDet.customizeHitRecoveryInGluedDetTkSeedsOnly'
    customera["Run2016F"] = 'Configuration/DataProcessing/RecoTLR.customisePostEra_Run2_2016,RecoTracker/Configuration/customizeMinPtForHitRecoveryInGluedDet.customizeHitRecoveryInGluedDetTkSeedsOnly'
    customera["Run2016G"] = 'Configuration/DataProcessing/RecoTLR.customisePostEra_Run2_2016'
    customera["Run2016H"] = 'Configuration/DataProcessing/RecoTLR.customisePostEra_Run2_2016'
```

We specify the json file for runs selection and the default priority of the workflows:

```
jsonFile = '/afs/cern.ch/cms/CAF/CMSCOMM/COMM_DQM/certification/Collisions16/13TeV/DCSOnly/json_DCSONLY.txt'
default_priority = 85000
```

We specify the list of PD that must NOT be reprocessed:

```
 pd_blacklist = ["HighMultiplicity",
                    "L1MinimumBias",
                    "HLTPhysics", #FIXME should be?
                    "HLTPhysics0",
                    "HLTPhysics1",
                    "HLTPhysics2",
                    "HLTPhysics3",
                    "HcalNZS",
                    "HcalHPDNoise",
                    "Commissioning",
                    "Cosmics",
                    "EmptyBX"]
```

We can play with DbsApi query to attach more datasets to the above list. For instance, we attach to the list all the ZeroBias\[N] datasets :

```
for ds in api.listDatasets(dataset='/ZeroBias*/%s*/RAW' % acquisition_era):
        pd_tmp = ds['dataset'].split('/')[1]
        if(pd_tmp != 'ZeroBias'):
            pd_blacklist.append(pd_tmp)
```

We can specify priorities different from the default in a dictionary and also other parameters for the master.conf:

```
 pd_priorities = {}
    pd_priorities['ZeroBias'] = 90000
    pd_priorities['SinglePhoton'] = 90000
    pd_priorities['JetHT'] = 90000
    pd_priorities['DoubleEG'] = 90000
    pd_priorities['DoubleMuon'] = 90000
    pd_priorities['SingleElectron'] = 90000
    pd_priorities['SingleMuon'] = 90000
    pd_priorities['MuonEG'] = 90000
    pd_priorities['Charmonium'] = 90000
    pd_priorities['MuOnia'] = 90000

    campaign = acquisition_era
    num_core = 4
```

Here we extract the runs from the json:

```
   with open(jsonFile) as data_file:
        data = json.load(data_file)
    AlltheRuns = map(int,data.keys())
```

And here we extract all the RAW and [AOD](https://twiki.cern.ch/twiki/bin/view/CMS/AOD) datasets for the acquisition era we are considering (indeed we will consider below only datasets that have an [AOD](https://twiki.cern.ch/twiki/bin/view/CMS/AOD) datasets produced in Prompt):

```
theDatasets = api.listDatasets(data_tier_name='RAW', processed_ds_name='*%s*' % era)
    theDatasetsAOD = api.listDatasets( data_tier_name='AOD', processed_ds_name='*%s*' % acquisition_era)
    for mydataset in theDatasetsAOD:
        tempdataset = mydataset['dataset']
        theDatasetsToProcessAOD.append((tempdataset.split('/'))[1])
```

Here we open a new master.conf and write the DEFAULT section:

```
 master=file('master_'+era+'.conf','w')
    master.write("[DEFAULT] \n")
    master.write("group=ppd \n")
    master.write("user=%s \n" % username)
    master.write("request_type=ReReco \n")
    master.write("release=%s \n" % cmssw_version)
    master.write("globaltag=%s \n" % GT)
    master.write("\n")
    master.write("campaign="+campaign+"\n")
    master.write("\n")
    master.write("processing_string="+proc_string+" \n")
    master.write("\n")
    master.write("priority=%i \n" % default_priority)
    master.write("time_event=4 \n")
    master.write("size_event=500 \n")
    master.write("size_memory = 7000 \n")
    master.write("multicore=%i \n" % num_core)

    cfg_harvesting_file_name = 'harvesting.py'
    master.write("harvest_cfg=%s \n" % cfg_harvesting_file_name)
```

And here we run the cmsDriver for the harvesting step (only if the file does not exists):

```
  harvesting_command = 'cmsDriver.py step4 --data --filetype DQM --conditions %s -s HARVESTING:@allForPrompt --scenario pp --filein file:RECO_RAW2DIGI_L1Reco_RECO_ALCA_EI_PAT_DQM_inDQM.root --python_filename=%s --no_exec' % (GT, cfg_harvesting_file_name)
    if not os.path.isfile(cfg_harvesting_file_name):
        print 'creating harvesting cfg...'
        st_and_out_harvst = commands.getstatusoutput(harvesting_command)
```

We loop on the RAW input datasets and consider only if they have an [AOD](https://twiki.cern.ch/twiki/bin/view/CMS/AOD) conterpart and are not blacklisted:

```
 for oneDS in theDatasets:
        theDataset= oneDS['dataset']
        pd_name = theDataset.split('/')[1]
        era_version = theDataset.split('/')[2]
        if pd_name in theDatasetsToProcessAOD:
            if pd_name in pd_blacklist:
                continue
```

For each dataset, we consider only those runs that are in the json file (with the **exception of** [**NoBPTX**](https://twiki.cern.ch/twiki/bin/edit/CMS/NoBPTX?topicparent=CMS.PdmVReRecoScriptInstructions;nowysiwyg=1) **dataset**):

**Note:** for COSMICS there are required changes wrt runs and in cmsdriver.

```
  runs = api.listRuns(dataset=theDataset)[0]['run_num']
            if("NoBPTX" in (pd_name) ) :
                inter = set(runs)
            else :
                inter = set(runs) & set(theRuns)
```

If the dataset has at least one good run, then we add it to the master.conf section:

```
 if len(inter) > 0 :
                theDatasetsToProcess.append(theDataset)
                nd = nd+1
                theruns = sorted(inter)
                cfg_file_name = 'recoskim_%s_%s.py' % (era, pd_name)
                prep_id = "ReReco-"+campaign+"-"+pd_name+"-"+proc_string+"-"+(format(nd, '04d'))
                master.write("\n")
                master.write('[%s-%s-%s]\n' % (era_version, pd_name, proc_string))
                master.write("dset_run_dict={\""+theDataset+"\" : "+str(theruns)+" }\n")
                master.write("cfg_path=%s\n" % cfg_file_name)
                master.write("request_id=%s \n" % prep_id)
                if pd_name in pd_priorities.keys():
                    master.write("priority=%i \n" % pd_priorities[pd_name])
```

And we prepare the cmsDriver to write the reco cfg:

```
 alcaseq = ''
                skimseq = ''
                recotier = ''
                keepreco = False
                if ("NoBPTX" in pd_name) :
                    recotier = 'RECO,'
                if pd_name in autoSkim.keys():
                    skimseq='SKIM:%s,'%(autoSkim[pd_name])
                if pd_name in AlCaRecoMatrixRereco.keys():
                    alcaseq='ALCA:%s,'%(AlCaRecoMatrixRereco[pd_name])

                reco_command = 'cmsDriver.py RECO -s RAW2DIGI,L1Reco,RECO,%sEI,PAT,DQM:@allForPrompt --runUnscheduled --nThreads %i --data --era Run2_2016 --scenario pp --conditions %s --eventcontent %sAOD,MINIAOD,DQM --datatier %sAOD,MINIAOD,DQMIO --customise %s --filein %s -n 100 --python_filename=%s --no_exec' % (skimseq+alcaseq, num_core, GT, recotier, recotier, str(customera[campaign]), input_file_name, cfg_file_name)
```

If the reco cfg does not exists in the local area, then write it:

```
  if not os.path.isfile(cfg_file_name):
                    print '     creating the cfg...'
                    st_and_out = commands.getstatusoutput(reco_command)
```

And finally write also the dataset info in the twiki table file:

```
                twiki.write("| %s | [[https://cms-pdmv.cern.ch/pmp/historical?r=%s][%s]] | %s |\n"  %(theDataset, prep_id, prep_id, str(theruns)))
```

You can run this example, look the printout and outputs. You can also try to run the 2017 script to look at the differences. Also, for re-MiniAOD reprocessing the script must be changed (e.g. we start from [AOD](https://twiki.cern.ch/twiki/bin/view/CMS/AOD) inputs, the reco cmsDriver is different, etc.). In the official re-reco repository you can have a look at the script employed in the re-MiniAOD.

## Official code used for data reprocessing will be collected here:

{% embed url="https://github.com/pgunnell/ReRecoProcessing" %}

