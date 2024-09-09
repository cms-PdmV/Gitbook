---
description: >-
  In this page, we list some rules which should be used for choosing the name of
  a dataset in McM
---

# Rules for dataset names

## WHAT IS THE Primary Dataset NAME?&#x20;

It's the part of the dataset-name before the second 'slash', i.e. for the dataset

```
/DiPhotonBorn_Pt10to25/Summer09-MC_31X_V3_7TeV_TrackingParticles-v1/GEN-SIM-RAW
```

the PD name is

```
DiPhotonBorn_Pt10to25
```

## CONVENTION&#x20;

We propose to use the following convention for this name:

```
PROCESS_RANGETYPE-RANGELOWToRANGEHIGH_FILTER_TUNE_COMMENT_COMENERGY-GENERATOR
```

where&#x20;

* `PROCESS` is the Phyics process in the sample, e.g. `QCD, TT, W, DY`
* `RANGETYPE` is the variable the sample is binned in, e.g. `PT,M`
* `RANGELOW` is the lower bound of that range in GeV, e.g. `0,10,200`
* `RANGEHIGH` is the upper bound
* `FILTER` denotes information on additional filters applied
* `TUNE` is the underlying-event tune (e.g. [TuneZ2Star](https://twiki.cern.ch/twiki/bin/edit/CMS/TuneZ2Star?topicparent=CMS.ProductionDataSetNames;nowysiwyg=1))
* `COMMENT` for additional comments
* `COMENERGY` cnter of mass collision enetgy, e.g. `7TeV, 10TeV`
* `GENERATOR` is the generator used, e.g. `pythia8, herwigpp, sherpa, herwig7`

Some details on all these parts follow here.

### PROCESS&#x20;

To unify this part we suggest to use the following conventions:&#x20;

* all 'particles' start with capital letters, followed by minor letters, e.g. `W, Z, Mu, Tau, E, Nu, Wplus, H, Jets, Tbar, B, Bbar`
* if a specific decay is simulated, this is specified using the keyword `To`, e.g. `WToENu, HToWWTo2L2Nu`
* initial state particles are only specified if needed to distinguish between other processes, e.g. `GluGluToWW` with respect to `WW`
* charge fo a particle is only specified if relevant, i.e. use `Wplus` if only W+ is in the sample, but **don't use** `WplusWminus` for W-pair production
* the same for anti-particles: use `Tbar` if only anti-top is in the sample, but **don't use** `TTbar`, but rather `TT`
* if one one part of the process name there is a) more then one particle of the same kind **and** b) more then two particles in total, use `2E2Nu` rather then `EENuNu`

We propose the following conventions for the most common particles:

| [Particle](https://twiki.cern.ch/twiki/bin/viewauth/CMS/ProductionDataSetNames?sortcol=0;table=1;up=0#sorted\_table) | [KEYWORD](https://twiki.cern.ch/twiki/bin/viewauth/CMS/ProductionDataSetNames?sortcol=1;table=1;up=0#sorted\_table) | [modifications if needed](https://twiki.cern.ch/twiki/bin/viewauth/CMS/ProductionDataSetNames?sortcol=2;table=1;up=0#sorted\_table) |
| -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| electron/positron                                                                                                    | `E`                                                                                                                 | `Eminus`, `Eplus`                                                                                                                   |
| muon                                                                                                                 | `Mu`                                                                                                                | `Muplus`, `Muminus`                                                                                                                 |
| tau                                                                                                                  | `Tau`                                                                                                               | `Tauplus`, `Tauminus`                                                                                                               |
| charged lepton                                                                                                       | `L`                                                                                                                 |                                                                                                                                     |
| neutrino                                                                                                             | `Nu`                                                                                                                | `Nue`, `Numu`, `Nutau`, `Nuebar`,...                                                                                                |
| W                                                                                                                    | `W`                                                                                                                 | `Wplus`, `Wminus`, `Wprime`                                                                                                         |
| Z (no photon)                                                                                                        | `Z`                                                                                                                 | `Zprime`                                                                                                                            |
| Z/gamma (Drell-Yan)                                                                                                  | `DY`                                                                                                                |                                                                                                                                     |
| photon                                                                                                               | `G`                                                                                                                 |                                                                                                                                     |
| gluon                                                                                                                | `Glu`                                                                                                               |                                                                                                                                     |
| top                                                                                                                  | `T`                                                                                                                 | `Tbar`, `Tprime`                                                                                                                    |
| bottom                                                                                                               | `B`                                                                                                                 | `Bbar`, `Bprime`                                                                                                                    |
| quark                                                                                                                | `Q`                                                                                                                 | `Qbar`                                                                                                                              |
| jet                                                                                                                  | `Jet`                                                                                                               | `Jets` for more than one (inclusive), `1Jet`, `2Jets`, ... for exclusive \*ONLY FOR ME GENERATORS (see below)                       |
| jet                                                                                                                  | `J`                                                                                                                 | for decay products, if both quarks and gluons are produced                                                                          |

**IMPORTANT**: Use the `Jet` keyword with caution. We're operating a hadron collider, there are jets all over the place. We propose to use it only if there are matrix elements in the generation that explicitly include the higher QCD multiplicity diagrams, i.e. MadGraph, Alpgen and Sherpa, and some matching procedure had/has to be applied. From this definition the keyword `Jet` should never appear in a leading order MC generator sample. If there are cuts on pthat, this should be indicated using the dedicated keywords. A an example `ZJet` in Pythia6, which is nothing but Z production with a cut on pthat of the hard interaction should become `Z`, or `ZmumuJet` simply `ZToMuMu`. In case of decay products, e.g. RS Gravitons decaying into quarks and gluons, use the keyword `J`, e.g. `RSGravToJJ`.

Here we list a few examples, comparing the 'old' existing names to the new convention

| [old name](https://twiki.cern.ch/twiki/bin/viewauth/CMS/ProductionDataSetNames?sortcol=0;table=2;up=0#sorted\_table) | [new convention](https://twiki.cern.ch/twiki/bin/viewauth/CMS/ProductionDataSetNames?sortcol=1;table=2;up=0#sorted\_table) |
| -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `DYmumu`                                                                                                             | `DYToMuMu`                                                                                                                 |
| `HZZ_4l`                                                                                                             | `HToZZTo4L`                                                                                                                |
| `Hgg`                                                                                                                | `HToGG`                                                                                                                    |
| `JPsiEE`                                                                                                             | `JPsiToEE`                                                                                                                 |
| `MinBias`                                                                                                            | `MinBias`                                                                                                                  |
| `QCD`                                                                                                                | `QCD`                                                                                                                      |
| `Wgamma`                                                                                                             | `WG`                                                                                                                       |
| `Wenu`                                                                                                               | `WToENu`                                                                                                                   |
| `InclusiveMu5`                                                                                                       | `QCD` (see below for explanations)                                                                                         |

### RANGETYPE, RANGELOW, RANGEHIGH&#x20;

This part denotes in what variable (if at all) the sample is binned. Typical possibilities are `Pt` (pthat), `M` (inv. mass), as well as the range for this variable. This part of the name can also be used (togther with `M` to specify the mass of a particles, that is used as a parameter (e.g. Higgs mass, Z' mass, ...). Examples are&#x20;

* `Pt-100To200` for binning in pthat from 100 GeV to 200 GeV
* `Pt-50` if there is only a lower cut on pthat
* `M-30` as a lower inv. mass cut (e.g. in Drell-Yan)
* `M-160` for Higgs mass of 160 GeV

If needed, the variable can be accompanied by specification on which particle in the process the cut is applied on:&#x20;

* `PtW-300` if there is a lower cut on the W pt

If there is no binning, inv. mass cut etc. you can drop this part of the PD name. **IMPORTANT**: Only put the cut/binning information here that is applied at the lelevl of the event generation, i.e. as parameter in PYTHIA. **Do not** add information coming from an additional filter (GenFilter) that is run after the event production. This information should enter in the next section.

### FILTER&#x20;

Is there a GEN level filter for the production? Specify it here. This part is very difficult to standardize, so be a little creative. Here a few examples:&#x20;

* `EMEnriched`, you apply some filter enriching the sample with electrons/photons
* `MuEnriched`, Gen level filter on Muons
* `MuEnrichedPt5`, cut on GEN level muons of 5 GeV

Using this new convention, there should be in future no samples anymore starting like `QCDEnriched`, or `InclusiveMu5` etc. The should all become `QCD_MuEnrichedPt5` and similar.

It is also helpful for the users if the filter you are applying in the production has a similar (even the same?) name.

### COMMENT&#x20;

Only use this if really needed information cannot be put in any of the other fields. e.g. only QCD or only EWK production, special selections etc.

### COMENERGY and GENERATOR&#x20;

Add the units in the `COMENERGY`, i.e. `7TeV`, `10TeV`, `900GeV`, `2360GeV` and so on. **Don not** use things like `0.9TeV`, so only integer numbers, no floating points.

The generators to be used are:

| [GENERATOR](https://twiki.cern.ch/twiki/bin/viewauth/CMS/ProductionDataSetNames?sortcol=0;table=3;up=0#sorted\_table) | [KEYWORD](https://twiki.cern.ch/twiki/bin/viewauth/CMS/ProductionDataSetNames?sortcol=1;table=3;up=0#sorted\_table) |
| --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Pythia6                                                                                                               | `pythia6`                                                                                                           |
| Pythia8                                                                                                               | `pythia8`                                                                                                           |
| Herwig6                                                                                                               | `herwig6`                                                                                                           |
| Herwig++                                                                                                              | `herwigpp`                                                                                                          |
| Herwig7                                                                                                               | `herwig7`                                                                                                           |
| Sherpa                                                                                                                | `sherpa`                                                                                                            |
| MadGraph/MG5\_aMC@NLO (LO)                                                                                            | `madgraph`                                                                                                          |
| MadGraph/MG5\_aMC@NLO (LO) **e.g. showered with Pythia8**                                                             | `madgraph-pythia8`                                                                                                  |
| MadGraph/MG5\_aMC@NLO (NLO)                                                                                           | `amcatnlo`                                                                                                          |
| Alpgen                                                                                                                | `alpgen`                                                                                                            |
| MC@NLO                                                                                                                | `mcatnlo`                                                                                                           |
| POWHEG                                                                                                                | `powheg`                                                                                                            |
| HARDCOL                                                                                                               | `hardcol`                                                                                                           |
| BCVEGPY 2                                                                                                             | `bcvegpy2`                                                                                                          |
| ...                                                                                                                   | ...                                                                                                                 |

If there are specialized decay tool used, please append this to the name, e.g. if EvtGen was used after Pythia8, use `...-pythia8-evtgen, ...-pythia8-tauola, ...-pythia8-photos`.

### DATASET EXTENSION&#x20;

For the same primary dataset, with extended number of events please use the **EXACT** same name for the dataset, in the request **set the extension parameter accordingly**. It might be also useful to mention, when reporting these request to hn-cms-prep-ops or at the [MccM](https://twiki.cern.ch/twiki/bin/view/CMS/MccM) that the request is an extension.
