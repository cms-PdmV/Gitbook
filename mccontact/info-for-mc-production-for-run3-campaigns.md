# Info for MC production for Run3 Campaigns

## List for samples taken care centrally

[Link to gSheet](https://docs.google.com/spreadsheets/d/1mzrhaacEG65k601OJNFNG17c4-4FjLT4GFMBRclaifQ/edit#gid=211250911), sheet4 (PdmV sheet with XS). Those samples will be handled centrally by PdMV and the request prepid will start with "GEN". Other samples need to be handled by PAG MC contacts as usual.

## Recommendations on the usage of PDFs and CPX Tunes

**The current master branch with MG299 (07/2022) is the recommended default for UL production.**

```
Positive definite sets with hessian variations:
-----------------------------------------------
NNPDF31_nnlo_as_0118_mc_hessian_pdfas
LHAPDF ID: 325300

For 4 flavor:
NNPDF31_nnlo_as_0118_nf_4_mc_hessian
LHAPDF ID: 325500

Note that there are no alpha_s variations for the 4-flavor case. 
NNPDF authors recommend to estimate the relative alpha_s uncertainty from the 5-flavor set. 
They expect the resulting uncertainties to be similar to what we would have obtained from the 4-flavor set. 

non-positive sets with hessian variations:
------------------------------------------
NNPDF31_nnlo_hessian_pdfas
LHAPDF ID: 306000

For 4 flavor:
NNPDF31_nnlo_as_0118_nf_4
LHAPDF ID: 320900
```

325300 and 325500 are positive-definite (all positive at very high mass scales as well).&#x20;

_Note that e.g. 325300 (325500) and 306000 (320900) are considered equivalent at the SM regions._&#x20;

PDF lists are summarized in [Run3\__5f_](https://github.com/cms-sw/genproductions/blob/master/MetaData/pdflist\_5f\_run3.dat) _and_ [_Run3\__4f](https://github.com/cms-sw/genproductions/blob/master/MetaData/pdflist\_4f\_run3.dat), please notice that those lists are a bit different from Run2 UL, while some old version PDFs are updated, and NNPDF40 is now added for 5f scheme.

The default tune to be used with this PDF set is CP5. The corresponding paper for CPX tunes ([http://cms-results.web.cern.ch/cms-results/public-results/publications/GEN-17-001/index.html](http://cms-results.web.cern.ch/cms-results/public-results/publications/GEN-17-001/index.html)) needs to be cited in CMS publications. (FYI, [total/elastic cross section in pythia](https://indico.cern.ch/event/1169048/contributions/4909711/attachments/2456268/4210106/2022\_June6\_GEN\_CPXnormForRun3\_SercanSen.pdf) has been updated and [integrated to CMSSW](https://github.com/cms-sw/cmssw/pull/38362/) for Run3)

For PDF uncertainty calculation the corresponding prescription ([http://nnpdf.mi.infn.it/wp-content/uploads/2019/03/NNPDFfits\_Positivity\_PhysicalCrossSections\_v2.pdf](http://nnpdf.mi.infn.it/wp-content/uploads/2019/03/NNPDFfits\_Positivity\_PhysicalCrossSections\_v2.pdf)) must be used. _**Note that in the median and uncertainty calculation the weights that are zero needs to be cut first.**_

If, for some reason, you prefer a PDF which is only LO or NLO accurate, we recommend to use the corresponding tune of the CPx family.  please check the following twiki: [https://twiki.cern.ch/twiki/bin/view/CMS/PhysicsComparisonAndGeneratorTunes#Recommendations\_on\_the\_usage\_of](https://twiki.cern.ch/twiki/bin/view/CMS/PhysicsComparisonAndGeneratorTunes#Recommendations\_on\_the\_usage\_of).&#x20;

**FYI, A dedicated CP5 tune with new intrinsic kT will be applied in FXFX DY sample (Other samples use CP5 as default). Corresponding link is** [**HERE**](https://indico.cern.ch/event/1201070/contributions/5050341/attachments/2514936/4323492/validation\_13p6TeV\_centralsample\_v3.pdf)**.**

## **How to produce gridpack**

The method producing gridpack is the same with before, the link for reference is [HERE](https://twiki.cern.ch/twiki/bin/viewauth/CMS/GeneratorMain#How\_to\_produce\_gridpacks).

## Where to put gridpack

/eos/cms/store/group/phys\_generator/cvmfs/gridpacks/RunIII/13p6TeV/
