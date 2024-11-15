# Rules for Run3 2024 dataset names

The following dataset name rules are enforced for all MC samples innjected in the `RunIII2024Summer24` MC campaign.
The same rules apply also for 2022 and 2023 Run 3 re-reco campaigns (`RunIII2022Summer24`, `RunIII2023Summer24`), as well as all future MC campaigns.

## General Conventions

### **Naming : PROCESS\_[BINNING]\_[FILTER]\_[PARAMETERS]\_TUNE\_BEAME\_ME-PS**

* **PROCESS** : DY, Z, W, TT, T, WW, WZ, ZZ, QCD, ...
* **BINNING** : Bin-MLL-XtoX, Bin-HT-XtoX, Bin-XJ, …
* **FILTER** : Fil-EMEnriched, Fil-MuEnriched, Fil-BEnriched, …
* **PARAMETERS** : Par-MH-125, ...
* **TUNE** : TuneCPX
* **BEAME** : 13p6TeV
* **ME-PS** : madgraphMLM-pythia8, powheg-pythia8, amcatnloFXFX-pythia8 (generator names in lower cases and merging schemes in upper cases)

The dataset name structure must respect the following rules:
- The blocks PROCESS, TUNE, BEAME and ME-PS are mandatory. Every dataset name must contain these blocks.
- The blocks BINNING, FILTER, and PARAMETERS are optional. The name can contain none, one, two, or all of them, depending on the physics process.
- The `_` (underscore) must be used **ONLY** to separate the main blocks of the dataset name.
- The `-` (dash) can be used to separate strings within a given block.
- The `Bin-` header must be pesent at the beginning of the BINNING block.
- The `Fil-` header must be pesent at the beginning of the FILTER block.
- The `Par-` header must be pesent at the beginning of the PARAMETERS block.


### **Particle** Acronyms

| Particle     | Acronyms | Additional information (Only when needed) |
| ------------ | -------- | ----------------------------------------- |
| lepton       | L        | Lplus, Lminus                             |
| electron     | E        | Eplus, Eminus                             |
| muon         | Mu       |                                           |
| tau          | Tau      |                                           |
| neutrino     | Nu       |                                           |
| quark        | Q        |                                           |
| quark+gluon  | J        |                                           |
| top quark    | T        | Tbar                                      |
| bottom quark | B        | Bbar                                      |
| higgs        | H        |                                           |
| photon       | G        |                                           |
| gluon        | Glu      |                                           |
| W boson      | W        |                                           |
| Z boson      | Z        |                                           |

### **PROCESS**

Specify the process we are producing.

To unify this part we suggest to use the following conventions:

* all 'particles' start with capital letters, followed by minor letters, e.g. `W, Z, Mu, Tau, E, Nu, Wplus, H, Jets, Tbar, B, Bbar`
* if a specific decay is simulated, this is specified using the keyword `to`, e.g. `WtoENu, HtoWWto2L2Nu`
* initial state particles are only specified if needed to distinguish between other processes, e.g. `GluGluToWW` with respect to `WW`
* charge fo a particle is only specified if relevant, i.e. use `Wplus` if only W+ is in the sample, but **don't use** `WplusWminus` for W-pair production
* the same for anti-particles: use `Tbar` if only anti-top is in the sample, but **don't use** `TTbar`, but rather `TT`
* if one one part of the process name there is a) more then one particle of the same kind **and** b) more then two particles in total, use `2E2Nu` rather then `EENuNu`

<span style="color:blue;">**Always using number if more than one same particle, and arrange in alphabetical order**</span>

* Using **DYto2L** instead of DYtoLL
* Usng **WtoLNu and WtoQQ** to distinguish decay of W boson
* Using **TT** instead of TTbar
* Using **TtoLNu and TbartoLNu** to distinguish top and anti-top
* Using **WWto2L2Nu** instead of WWtoLLNuNu (or WWto2Nu2L)
* Using **WWtoLNu2Q** instead of WWtoLNuQQ

<span style="color:blue;">**Merging information if it is not confusing**</span>

* Using **WZto3LNu** instead of WZtoLNu2L
* Using **WWto4Q** instead of WWto2Q2Q

**IMPORTANT**: Use the `Jet` keyword with caution. We're operating a hadron collider, there are jets all over the place. We propose to use it only if there are matrix elements in the generation that explicitly include the higher QCD multiplicity diagrams, i.e. MadGraph, Alpgen and Sherpa, and some matching procedure had/has to be applied. From this definition the keyword `Jet` should never appear in a leading order MC generator sample. If there are cuts on pthat, this should be indicated using the dedicated keywords. A an example `ZJet` in Pythia6, which is nothing but Z production with a cut on pthat of the hard interaction should become `Z`, or `ZmumuJet` simply `ZToMuMu`. In case of decay products, e.g. RS Gravitons decaying into quarks and gluons, use the keyword `J`, e.g. `RSGravToJJ`.

### **BINNING**

The format is: <span style="color:blue;">**Bin-VAR1-X1toY1-VAR2-X2toY2**</span>

When producing binned samples, e.g., DY process with maximum 4jet in LHE level:

* The inclusive process name is: **DYto2L-4Jets**
* The corresponding jet-binned sample, e.g., 1 jet at LHE-level is: **DYto2L-4Jets\_Bin-1J**

<span style="color:red;">N.B.: check the hyphen and underscore in this case carefully!!</span>

Other binning cases are trivial, e.g., DYto2L-4Jets\_Bin-MLL-60to90, DYto2L-4Jets\_Bin-HT-100to200 ...

For bins without an upper boundary no need to add `Inf`: e.g. `600toInf` should be `600` directly.

If sample is binned in multiple variables, separate the various parts with `-` and list bins in alphabetical order, e.g. `Bin-HT-100to400-MLL-50to120`.

<span style="color:red;">N.B.:The only exception to this rule is for jet bins (for historical reasons). In this case you should use the format `Bin-0J`, `Bin-1J`, ...</span>


### **FILTER**

The format is: <span style="color:blue;">**Fil-FILTER1-FILTER2**</span>

If more than one filter is used, separate them with `-` and list filters in alphabetical order, e.g. `Fil-K0s-Mu`.

Some complicated cases:

* `DYto2L-4Jets\_Fil-BEnriched`: GEN filter requiring for b quarks from parton shower (maximum jet multiplicity is 4 in LHE level )


### **PARAMETERS**

The format is: <span style="color:blue;">**Par-PARAMETER1-VALUE1-PARAMETER2-VALUE2**</span>

This is used to identify the values (NB: not the ranges, for which we use BINNING) of some relevant parameters in the physics process, such as the mass of the Higgs boson, Z', ... 

If more than one parameter is used, separate them with `-` and list parameters in alphabetical order, e.g. `Par-ctau-100cm-M-1000GeV`.


### **TUNE**

The format is: <span style="color:blue;">**TuneCPX**</span> with X between 1 and 5.

- Tunes CP1 and CP2 are LO tunes and go along with LO PDF sets (NNPDF3.1 LO - \alpha_s = 0.130)
- Tunes CP3, CP4, CP5 are NLO tunes and go along with NLO PDF sets (NNPDF3.1 N(N)LO - \alpha_s = 0.180)

### BEAME

The format is: <span style="color:blue;">**13p6TeV**</span>

This is fixed and must not be changed for Run3 pp collisions.

### ME-PS

The generators to be used are:​

| Pythia6                                                   | `pythia6`          |
| --------------------------------------------------------- | ------------------ |
| Pythia8                                                   | `pythia8`          |
| Herwig6                                                   | `herwig6`          |
| Herwig++                                                  | `herwigpp`         |
| Herwig7                                                   | `herwig7`          |
| Sherpa                                                    | `sherpa`           |
| MadGraph/MG5\_aMC@NLO (LO)                                | `madgraph`         |
| MadGraph/MG5\_aMC@NLO (LO) **e.g. showered with Pythia8** | `madgraph-pythia8` |
| MadGraph/MG5\_aMC@NLO (NLO)                               | `amcatnlo`         |
| Alpgen                                                    | `alpgen`           |
| MC@NLO                                                    | `mcatnlo`          |
| POWHEG                                                    | `powheg`           |
| HARDCOL                                                   | `hardcol`          |
| BCVEGPY 2                                                 | `bcvegpy2`         |
| ...                                                       | ...                |

If there are specialized decay tool used, please append this to the name, e.g. if EvtGen was used after Pythia8, use `...pythia8-evtgen, ...pythia8-tauola, ...pythia8-photos`

When madspin is used, please append to the name, e.g.: `powheg-madspin-pythia8`,  `madgraph-madspin-pythia8`.

### Some full examples

This is a list of examples, comparing OLD (not ok) and NEW names (following the current rules).

* <span style="color:red;"> OLD</span>:   ADDGravTo2G_NegInt-0_LambdaT-10000_M-1000To2000_TuneCP5_13p6TeV_pythia8
* <span style="color:green;"> NEW</span>: ADDGravTo2G_Bin-M-1000to2000_Par-NegInt-0-LambdaT-10000_TuneCP5_13p6TeV_pythia8

* <span style="color:red;"> OLD</span>:   AMSB_Higgsino_M1000GeV_ctau100cm_TuneCP5_13p6TeV_madgraph-pythia8
* <span style="color:green;"> NEW</span>: AMSB-Higgsino_Par-ctau-100cm-M-1000GeV_TuneCP5_13p6TeV_madgraph-pythia8

* <span style="color:red;"> OLD</span>:   B0ToJpsiK0s_JMM_BMuFilter_DGamma0_SoftQCDnonD_TuneCP5_13p6TeV-pythia8-evtgen
* <span style="color:green;"> NEW</span>: B0ToJpsiK0s-JMM_Fil-BMu_Par-DGamma-0_SoftQCDnonD_TuneCP5_13p6TeV_pythia8-evtgen

* <span style="color:red;"> OLD</span>:   bbH_Hto2Zto4L_M-125_TuneCP5_13p6TeV_JHUGenV752-pythia8
* <span style="color:green;"> NEW</span>: BBH-Hto2Zto4L_Par-M-125_TuneCP5_13p6TeV_JHUGenV752-pythia8

* <span style="color:red;"> OLD</span>:   B0ToK0sMuMu_MuFilter_K0sFilter_TuneCP5_13p6TeV_pythia8-evtgen
* <span style="color:green;"> NEW</span>: B0ToK0sMuMu_Fil-K0s-Mu_TuneCP5_13p6TeV_pythia8-evtgen

* <span style="color:red;"> OLD</span>:   DYBto2LB-4Jets_MLL-120_HT-100to400_TuneCP5_13p6TeV_madgraphMLM-pythia8  
* <span style="color:green;"> NEW</span>: DYBto2LB-4Jets_Bin-HT100to400-MLL-120_TuneCP5_13p6TeV_madgraphMLM-pythia8

* <span style="color:red;"> OLD</span>:   DYto2L-2Jets_MLL-50_0J_TuneCP5Down_13p6TeV_amcatnloFXFX-pythia8
* <span style="color:green;"> NEW</span>: DYto2L-2Jets_Bin-0J-MLL-50_TuneCP5Down_13p6TeV_amcatnloFXFX-pythia8

* <span style="color:red;"> OLD</span>:   DYto2L-4Jets_MLL-50to120_HT-100to400_TuneCP5_13p6TeV_madgraphMLM-pythia8
* <span style="color:green;"> NEW</span>: DYto2L-4Jets_Bin-HT100to400-MLL-50to120_TuneCP5_13p6TeV_madgraphMLM-pythia8

* <span style="color:red;"> OLD</span>:   RPVStopStopToJets_UDD323_M-700_TuneCP5_13p6TeV-madgraphMLM-pythia8
* <span style="color:green;"> NEW</span>: RPVStopStoptoJets_Par-M-700_UDD323_TuneCP5_13p6TeV_madgraphMLM-pythia8

* <span style="color:red;"> OLD</span>:   SUEP_mMed-125_mDark-2_temp-0p5_decay-generic_14TeV-pythia8
* <span style="color:green;"> NEW</span>: SUEP_Par-mDark-2-mMed-125-temp-0p5_decayGeneric_14TeV-pythia8

* <span style="color:red;"> OLD</span>:   WminusH_Wto2Q_Hto2G_M-125_TuneCP5_13p6TeV_powheg-minlo-HWJ-pythia8
* <span style="color:green;"> NEW</span>: WminusH-Wto2Q-Hto2G_Par-M-125_TuneCP5_13p6TeV_powheg-minlo-HWJ-pythia8

* <span style="color:red;"> OLD</span>:   TtoLNu-2Jets_s-channel_TuneCP5_13p6TeV_amcatnloFXFX-pythia8
* <span style="color:green;"> NEW</span>: TtoLNu-2Jets-schannel_TuneCP5_13p6TeV_amcatnloFXFX-pythia8

* <span style="color:red;"> OLD</span>:   GluGluSpin0To2G_W-5p6_M-1750_TuneCP5_13p6TeV_pythia8
* <span style="color:green;"> NEW</span>: GluGluSpin0To2G_Par-M-1750-W-5p6_TuneCP5_13p6TeV_pythia8
