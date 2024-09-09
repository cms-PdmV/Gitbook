# How to search for datasets in DAS and McM

### How to find a request, given a prep-ID <a href="#gmail-how-to-find-a-request-given-a-prep-id" id="gmail-how-to-find-a-request-given-a-prep-id"></a>

&#x20;(example here: TOP-RunIIFall18-00005)

&#x20;[https://cms-pdmv.cern.ch/mcm/requests?prepid=TOP-RunIIFall18GS-00005\&page=0\&shown=127![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm/requests?prepid=TOP-RunIIFall18GS-00005\&page=0\&shown=2147483775)

&#x20;or go to [https://cms-pdmv.cern.ch/mcm![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm) , and click "Request" in the top, and click the "Navigation", and in the prepid field, paste the given prepID, and click "Search"

### How to find a request, given the dataset name

(example here: /ST\_t-channel\_tauDecays\_13TeV-comphep-pythia8\_TuneCP5/RunIIFall18GS-102X\_upgrade2018\_realistic\_v11-v1/GEN-SIM)

[https://cms-pdmv.cern.ch/mcm/requests?produce=%2FST\_t-channel\_tauDecays\_13TeV-comphep-pythia8\_TuneCP5%2FRunIIFall18GS-102X\_upgrade2018\_realistic\_v11-v1%2FGEN-SIM\&page=0\&shown=127](https://cms-pdmv.cern.ch/mcm/requests?produce=%2FST\_t-channel\_tauDecays\_13TeV-comphep-pythia8\_TuneCP5%2FRunIIFall18GS-102X\_upgrade2018\_realistic\_v11-v1%2FGEN-SIM\&page=0\&shown=127)

&#x20;or go to [https://cms-pdmv.cern.ch/mcm![](https://twiki.cern.ch/twiki/pub/TWiki/TWikiDocGraphics/external-link.gif)](https://cms-pdmv.cern.ch/mcm) , and click "Request" in the top, and click the "Output dataset", and paste the dataset name, and click "Search"

### Sample overview in DAS

All completed samples will be available in DAS\
• Analysts can find various type of data samples and can transfer files to laptop/Tier-2/3\
• General queries about DAS, command line tool, etc. are available at DAS-FAQs\
• Find datasets in DAS: https://cmsweb.cern.ch/das/\
• Currently no direct link between DAS and McM. So find McM prep-ID in DAS and use in McM

* Status VALID: production is finished and dataset is available
*   Status PRODUCTION: Its statistics is still growing due to running production jobs

    and dataset is not yet announced. But analysts can still run over the existing statistics by using crab parameter "allowNonValidInputDataset" parameter inCRAB3 configuration parameters
