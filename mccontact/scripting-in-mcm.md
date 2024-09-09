---
description: >-
  In this page, some examples of scripts which can be used in McM for queries
  and actions are listed.
---

# Scripting in McM

## McM Scripts

Repository for using McM scripts and example scripts

#### Basic info

* Link to McM: [https://cms-pdmv.cern.ch/mcm/](https://cms-pdmv.cern.ch/mcm/)
* McM Rest API: [https://cms-pdmv.cern.ch/mcm/restapi](https://cms-pdmv.cern.ch/mcm/restapi)
* For most actions you will NEED to have a valid CERN SSO cookie
* Public APIs do not require a cookie. Index of public API: [https://cms-pdmv.cern.ch/mcm/public/restapi/](https://cms-pdmv.cern.ch/mcm/public/restapi/)

#### CERN SSO cookie

* Use `cern-get-sso-cookie` command line tool to generate it:
  * `cern-get-sso-cookie --url https://cms-pdmv-dev.cern.ch/mcm/ -o dev-cookie.txt`
  * `cern-get-sso-cookie --url https://cms-pdmv.cern.ch/mcm/ -o prod-cookie.txt`
* `cern-get-sso-cookie` is already available in lxplus nodes
* It expires after \~10 hours, so be sure to regenerate it
* Dev cookie is valid only for dev environment and production cookie is valid only for production environment

#### Priority change

* If you want to use priority changing scripts or do anything else related to cmsweb, you'll have to use voms-proxy:
  * `voms-proxy-init -voms cms`
  * `export X509_USER_PROXY=$(voms-proxy-info --path)`

## Link to script repository

{% embed url="https://github.com/cms-PdmV/mcm_scripts" %}

{% embed url="https://github.com/pgunnell/mcm_scripts/tree/master" %}

(Please use it with care, only if you know what you are doing)
