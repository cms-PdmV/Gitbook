---
description: >-
  This page describes the usage of monte carlo request checking script in CMS
  that uses McM info and gridpacks and does automated patches for certain type
  of problem in MG5_aMC in the CMSSW setup.
---

# Request checking script

In lxplus, do:

```
$ git clone git@github.com:cms-sw/genproductions.git
$ cd genproductions/bin/utils
$ python request_fragment_check.py -h
```

This will bring up a list of things that the script checks. It also displays the list of optional arguments:

```
optional arguments:
  -h, --help            show this help message and exit
  --prepid PREPID [PREPID ...]
                        check mcm requests using prepids
  --ticket TICKET       check mcm requests using ticket number
  --bypass_status       don't check request status in mcm
  --bypass_validation   proceed to next prepid even if there are errors
  --apply_many_threads_patch
                        apply the many threads MG5_aMC@NLO LO patch if
                        necessary
  --dev                 Run on DEV instance of McM
  --debug               Print debugging information

```

{% hint style="info" %}
Note that the code acceps list of prepids, but a single ticket (not to kill the database with too much access). When you use a list of prepids or the --ticket option locally, you should also specify --bypass\_validation.&#x20;

Unless the --apply\_many\_threads\_patch is specified it won't do any patches but will still check the existence of the patch.&#x20;
{% endhint %}

