---
description: >-
  In this section, we comment on the errors observed in production and on the
  possible solutions that should be adopted to correct them. (page to be
  completed)
---

# Errors in production: explanation

The errors observed in production are listed in the following: (twiki page with the job exit codes can be found [here](https://twiki.cern.ch/twiki/bin/view/CMSPublic/JobExitCodes))

**53**

* **Phase space integration or un-reweighting efficiency problems**
* **Missing text file for fragment**

**73**

* &#x20;**Missing files at Premix stage**

**134**

* &#x20;**G4 error**

**139 - segmentation violation**

* **Merging problems**
* **Missing gridpacks**
* **NanoAOD problem**

**8001**

* &#x20;**nThread problem**

**8003**

* &#x20;**Premix error**

**8021**

* &#x20;**Merging problem**
* &#x20;**Server not available**

**50664**

* &#x20;**Timeout - due to incorrect tune**

**60450**

* &#x20;**Merging error due to server problem**

**99303**

* &#x20;**Stageout problem**

**99305**

* &#x20;**pLHE problem with too many events for time given**

**99996**

* &#x20;**Module problem at NanoAOD stage**
*   **53 :**

    **Powheg +  JHUGen phase space integration or unreweighting efficiency problems  (physics process related errors )**

    &#x20;**lhe file contains fewer events than were requested  ⇒ phase space problem. (physics process related errors )**\


    **73 :**

    **Pythia8 :**

    **vanishing cross section (physics process related errors )**   \


    **134:**

    **Mg leading order patching problem, + nb of threads issue.  (not physics process related errors**\


    **139 :  mainly : file access , request configuration issues.  (not physics process related errors )**

    **8001:**

    **Only 1 request with this exit code , error related to premixing step (not physics process related errors )**

    **50115 :**

    **Mad + pythia8 : (not a physics process related problem).  Issue observed in premixing step.**

    **Needs more investigation, for few other requests.**\
    \
