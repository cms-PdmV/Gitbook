---
description: >-
  This is a developing page, which contains some of the frequently asked
  questions.
---

# FAQ

### Where can I find the slides of the McM tutorials?

The slides can be found at the bottom of this page:

{% embed url="https://twiki.cern.ch/twiki/bin/viewauth/CMS/PdmVMcMProdManagerActions" %}

### What is the difference between premix and classical mixing?

There are two ways to produce samples with simulation of pile-up: premix and classical mixing.

Classical mixing implies a previous production of a MB sample (with a datatier "GEN-SIM"). It contains the event at generator level and the interaction of the particles with the detector material. For the generation of the sample with PU (which happens in the DIGI-RECO step), a root wmLHEGS/GS request is digitized (namely the interaction of the particles with the detector material are used to simulate the signals in the detector cells) together with the PU sample. The DR step needs the PU input dataset and the pile-up scenario, namely according to which distribution the pile-up should be simulated (and added to the root request). Since the DIGI step is quite consuming and happens for both root request and MB sample, classical mixing is generally more time and CPU consuming.

Premix is different because the PU sample is digitized separately (at the time of the production of the premix library). A MB sample (datatier GEN-SIM) is produced in the same way as before, but it is here used for the production of a SingleNeutrino sample (basically nothing in the final state) which is interfaced with the simulation of the PU according to a certain scenario and using the MB sample. The output of the SingleNeutrino sample is a GEN-SIM-DIGI sample (already digitized). For root requests using premix PU simulation, the DIGI step is run only on them, while the PU simulation is added after this step. SInce the DIGI step is run only once, premix requests are much faster and less CPU consuming than classical mixing requests.

### How can I estimate the memory consumption of a request?

One can execute the get\_test script for that particular request for a number of events close to 1000. (You can find the get\_test script at each request's McM link, by clicking the "tick" button, an example is here: [https://cms-pdmv.cern.ch/mcm/public/restapi/requests/get\_test/SUS-RunIIFall18wmLHEGS-00113](https://cms-pdmv.cern.ch/mcm/public/restapi/requests/get\_test/SUS-RunIIFall18wmLHEGS-00113)).

By executing it locally, one produces a .xml file. By executing the following command, one gets access to the peak memory consumption and the average one for the produced events:

#### grep "Peak" myfile.xml

&#x20;This gives an estimate of how much memory one needs to setup for this request.

### When will my sample be ready?

This is a very difficult question to answer, since it implies the knowledge of the general overview of the system. If there are many high priority requests in the system, a standard request in block2-3 will take more time, than if there are none. Normally, if the requested sample is not targeting an immediate conference, the ETA might be between 4-6 months (depending on the number of events), but already a small increase in priority might complete it in 1-2 months.

### Is it convenient to first run a GEN-SIM request standalone and run the DR step afterwards?

The general answer is NO. This is due to the fact that the already produced GS sample is generally immediately transferred to tape. There, access is not possible and if one wants to run DR step on top of it, the sample needs to be re-transferred to disk again. This operation takes time and it's more convenient to restart production from scratch, in general.

### Issue with 2017 MiniAOD/NanoAOD samples:

Some miniAODV2 samples in the Fall17 campaign have inconsistent pileup (PU) information in the dataset names. These samples \[1] are produced from the 'original-buggy-PU-AODSIM' samples, which are in fact good to be used for the physics analyses. The more information about the PU issue and the solution is given in T. Boccali's talk \[2] in the PPD General meeting. However, it is generally recommended that the analysts must always reweigh the MC samples to match the data pileup since you may want to know which pileup library has been used for a certain dataset. Here is a brief overview of this issue.

&#x20;There are more than 1 AODSIM sample existing for some Fall17 GEN-SIMs.

It happened due to a problem in the old premix library \[2]. So the corresponding AODSIM samples have a buggy-PU profile, which can be corrected by PU-reweighing at the analysis level.

&#x20;    \*   Then a new premix library was created with the 'corrected-PU' information. The word 'PU2017' is added in the dataset names of AODSIM and miniAODv2 samples that have been submitted/produced centrally with this 'corrected-PU' library.

&#x20;    \*   So 'PU2017' in the dataset names can be used to differentiate the 'original-buggy-PU-AODSIM' and the 'corrected-PU-AODSIM' samples.

&#x20; Then, another central migration was done to get MiniAODv2+nanoAOD samples from all the existing AODSIMs (original-buggy-PU and new-corrected-PU) but mistakenly, the same 'setup' was used to create all the MiniAODv2s (for original-buggy-PU and new-corrected-PU).

&#x20;    \*   So the word 'PU2017' in the dataset names is not enough to differentiate the Fall17 miniAODv2 samples of the 'original-buggy-PU-AODSIM' and the 'corrected-PU-AODSIM' samples. Now 1054 MiniAODv2 requests \[2] have incorrectly 'PU2017' in the dataset name but these have been produced with 'original-buggy-PU-AODSIM'.

&#x20;       \*   Solution: You can always see the 'Parent' dataset of these samples in DAS to confirm the PU info. If the AODSIM for your miniAODv2 has 'PU2017' in the dataset name then it's the 'corrected-PU' otherwise it's the 'original-buggy-PU'.

\[1] /afs/cern.ch/user/g/gurpreet/public/Fall17\_oldPU.txt

\[2] T. Boccali (February 1, 2018) https://indico.cern.ch/event/695872/contributions/2877123/attachments/1593469/2522749/pileup\_ppd\_feb\_2018.pdf

