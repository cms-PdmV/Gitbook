# Info for MC production for Ultra Legacy Campaigns 2016, 2017, 2018

## Sample Collection through McM and monitoring via PMP

Ultra legacy (UL) campaigns are displayed at this [link](https://cms-pdmv.cern.ch/mcm/campaigns?prepid=RunIISummer20UL\*\&page=-1\&shown=63). The UL campaigns are the standard campaigns with the corresponding setup schemes to emulate the RunII datataking period. &#x20;

Sample collection is done through McM y entering requests that are not chained. MC contacts create requests first (even before the requests are ready). This is done in the corresponding campaign. The pre-defined tags, sample name, number of events, and target groups need to be entered in the creation of the requests (if known CADI line can be entered as well). The tags are predefined to avoid typos. History of updating tags are kept showing explicitly if a tag was changed and when. No approval of tags are needed, it's just for monitoring purposes.

&#x20;Monitoring of the samples can be done with PMP. Notice that in pMp, it is only shown what is marked to be kept from the McM side. Therefore, MINIAODSIM is a good datatier for the monitoring requests in the system. For all the 20UL campaigns, this is the [link](https://cms-pdmv.cern.ch/pmp/present?r=RunIISummer20UL18MiniAOD,RunIISummer20UL17MiniAOD,RunIISummer20UL16MiniAOD,RunIISummer20UL16MiniAODAPV\&mode=events\&groupBy=\&colorBy=pwg\&stackBy=total\_events\&showUnchainedTable=true).&#x20;

## Recommendations on the usage of PDFs and CPX Tunes

The default PDF sets that could be used along with CP5 tune are

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

**The current master branch (08/2021) is the recommended default for UL production:**   \
[**https://github.com/cms-sw/genproductions**](https://github.com/cms-sw/genproductions/tree/mg261\_UL)

325300 and 325500 are positive-definite (all positive at very high mass scales as well).&#x20;

_Note that e.g. 325300 (325500) and 306000 (320900) are considered equivalent at the SM regions._&#x20;

LHAPDF has been updated to include above PDFs, see [https://github.com/cms-sw/cmsdist/pull/4927](https://github.com/cms-sw/cmsdist/pull/4927))

The default tune to be used with this PDF set is CP5. The corresponding paper for CPX tunes ([http://cms-results.web.cern.ch/cms-results/public-results/publications/GEN-17-001/index.html](http://cms-results.web.cern.ch/cms-results/public-results/publications/GEN-17-001/index.html)) needs to be cited in CMS publications.&#x20;

For PDF uncertainty calculation the corresponding prescription ([http://nnpdf.mi.infn.it/wp-content/uploads/2019/03/NNPDFfits\_Positivity\_PhysicalCrossSections\_v2.pdf](http://nnpdf.mi.infn.it/wp-content/uploads/2019/03/NNPDFfits\_Positivity\_PhysicalCrossSections\_v2.pdf)) must be used. _**Note that in the median and uncertainty calculation the weights that are zero needs to be cut first.**_

If, for some reason, you prefer a PDF which is only LO or NLO accurate, we recommend to use the corresponding tune of the CPx family.  please check the following twiki: [https://twiki.cern.ch/twiki/bin/view/CMS/PhysicsComparisonAndGeneratorTunes#Recommendations\_on\_the\_usage\_of](https://twiki.cern.ch/twiki/bin/view/CMS/PhysicsComparisonAndGeneratorTunes#Recommendations\_on\_the\_usage\_of).&#x20;

## **Generators and Parton Showers**

### **PS versions:**

```
PYTHIA8: 240
HERWIG7: ...
```

Note the PYTHIA8 authors decided to remove our previous main pdf set from PYTHIA8 internal sets therefore we need to make the following change in fragments:

```
# The following lines should be added
'SigmaTotal:mode = 0',
'SigmaTotal:sigmaEl = 21.89',
'SigmaTotal:sigmaTot = 100.309',
# 'PDF:pSet=20',  <-- we can not access LHAPDF6:NNPDF31_nnlo_as_0118 like this anymore. 
# If you want to use our previous default PDF set:
# ‘PDF:pSet=LHAPDF6:NNPDF31_nnlo_as_0118’
# In any case, we will now use this set:
‘PDF:pSet=LHAPDF6:NNPDF31_nnlo_as_0118_mc’
```

### Generator versions and gridpacks**:**

```
MG5_aMC@NLO: 265 
             (242 and 260 should not be used 
               - when GEN and SIM steps are 
               separate as in UL campaign, 
               only >= 261 works propertly. )
SHERPA: ....
....
```

**For gridpacks: CMSConnect Submission(SL7) from login-el7.uscms.org should be working now.**

## Parton Shower Weights

Details of the weights can be found in [the talk](https://indico.cern.ch/event/746817/contributions/3101385/attachments/1702410/2742087/psweights\_mseidel.pdf).

GEN contacts just need to add these 3 lines at the appropriate places:



```
from Configuration.Generator.PSweightsPythia.PythiaPSweightsSettings_cfi import *
pythia8PSweightsSettingsBlock,
'pythia8PSweightsSettings',
```

## Parameter Scans

Starting from these UL campaigns, we will not accept tickets for a single process consisting of huge number of requests making a scan (e.g. mass). Instead one request should be defined for scans following: [https://monte-carlo-production-tools.gitbook.io/project/mccontact/signal-mass-points-in-single-ticket![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://monte-carlo-production-tools.gitbook.io/project/mccontact/signal-mass-points-in-single-ticket)
