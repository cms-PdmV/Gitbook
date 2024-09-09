# Rules for Run3 dataset names

## General Conventions

### **Naming : PROCESS\_BINNING\_FILTER\_TUNE\_BEAME\_ME-PS**

* **PROCESS** : DY, Z, W, TT, T, WW, WZ, ZZ, QCD, ...
* **BINNING** : MLL-XtoX, HT-XtoX, XJ, …
* **FILTER** : EMEnriched, MuEnriched, BEnriched, …
* **TUNE** : Decided from campaign
* **BEAME** : Decided from campaign
* **ME-PS** : madgraphMLM-pythia8, powheg-pythia8, amcatnloFXFX-pythia8 (generator names in lower cases and merging schemes in upper cases)

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

Specify the process we are producing.&#x20;

<mark style="color:blue;">**Always using number if more than one same particle, and Arrange in alphabetical order**</mark>

* Using **DYto2L** instead of DYtoLL
* Usng **WtoLNu and WtoQQ** to distinguish decay of W boson
* Using **TT** instead of TTbar
* Using **TtoLNu and TbartoLNu** to distinguish top and anti-top
* Using **WWto2L2Nu** instead of WWtoLLNuNu (or WWto2Nu2L)
* Using **WWtoLNu2Q** instead of WWtoLNuQQ

&#x20;<mark style="color:blue;">**Merging information if it is not confusing**</mark>

* Using **WZto3LNu** instead of WZtoLNu2L
* Using **WWto4Q** instead of WWto2Q2Q

### **BINNING**

When producing binning samples, e.g., DY process with maximum 4jet in LHE level,&#x20;

* The inclusive process name: **DYto2L-4Jets**
* the corresponding jet-binned sample, e.g., 1 jet at LHE-level: **DYto2L-4Jets\_1J**

<mark style="color:blue;">N.B.: check the hyphen and underscore in this case carefully!!</mark>

Other binning cases are trivial, e.g., DYto2L-4Jets\_MLL-60to90, DYto2L-4Jets\_HT-100to200 ...&#x20;

bin e.g. "600toInf" should be "600" directly, i.e., no need to add "Inf"

### **FILTER**

Some complicated cases:

* DYto2L-4Jets\_BEnriched: GEN filter requiring for b quarks from parton shower (maximum jet multiplicity is 4 in LHE level )
* DYBto2LB-4Jets: LHE requiring one b quark in ME (e.g. p p > e+ e- b) (maximum jet multiplicity is 4 in LHE level )



### **TUNE**

TuneCP5

### BEAME

13p6TeV

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

When madspin is used, e.g., `powheg-madspin-pythia8`

### Some full examples

* DYto2L-4Jets\_TuneCP5\_13p6TeV\_madgraphMLM-pythia8
* DYto2L-4Jets\_XJ\_TuneCP5\_13p6TeV\_madgraphMLM-pythia8 (X = number of j)
* DYto2L-2Jets\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8
* DYto2L-2Jets_X_J\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8 (X = number of j)
* DYBto2LB-4Jets\_TuneCP5\_13p6TeV\_madgraphMLM-pythia8
* TTto2L2Nu-2Jets\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8
* TTTo2L2Nu\_TuneCP5\_13p6TeV\_powheg-pythia8
* TTtoLplusNu2Q-2Jets\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8
* TtoLNu-2Jets\_s-channel\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8
* TbartoLNu-2Jets\_s-channel\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8
* TbarWplustoLNu2Q-2Jets\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8
* WWto2L2Nu-2Jets\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8
* ZZto2L2Q-2Jets\_TuneCP5\_13p6TeV\_amcatnloFXFX-pythia8
* GluGluHto2B\_PT-200\_M-125\_TuneCP5\_13p6TeV\_powheg-minlo-pythia8
* ggZH\_Hto2B\_Zto2Nu\_M-125\_TuneCP5\_13p6TeV\_powheg-pythia8
* ZH\_Hto2B\_Zto2L\_M-125\_TuneCP5\_13p6TeV\_powheg-pythia8
