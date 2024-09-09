---
description: Multiple step request validation in McM
---

# \[DRAFT] MultiValidation in McM

### Starting point

MultiValidation is triggered the same way as the old validation - by clicking ">" button for none-new request so it would go into validation-new status. Only difference is that user should set time per event, size per event and memory values for a single core run and set nThreads to 1 in GEN/GS request sequences.

All steps of MultiValidation will be performed automatically and do not require any input from a user. Input from a user is needed only when validation fails and is not going to be automatically retried.

### MultiValidation steps and value checks

MultiValidation starts with a single core validation. When single core job finishes, McM parses job report and checks whether time per event, size per event, memory and filter efficiency is within threshold. Measured time per event must be within user set time per event +-40%. Size per event must be within user set size per event +-10%. Peak RSS value of validation must not exceed memory set in the request. Filter efficiency must be within user given filter efficiency (generator parameters filter efficiency × match efficiency) +- 3 sigma where sigma is:

```
# measured_eff - comes from job report
# events_ran - number of events ran, "-n" value of cmsDriver.py
sigma = sqrt((measured_eff * (1 - measured_eff)) / events_ran)
sigma = max(sigma, 0.05 * measured_eff)
```

If measured memory is higher than user entered memory or filter efficiency is not within allowed threshold, validation fails. If time per event or size per event is not within range, it is adjusted to:

```
new_value = (3 * measured_value + 1 * old_value) / 4
```

This is a more aggressive way of adjusting value than just a normal average. After size or time per event value is adjusted, single core validation is automatically resubmitted. This is done automatically up to two times and as a result McM tries to validate up to three times before giving up.

If single validation succeeds and request's CMSSW version is newer than 7.3, McM submits 2, 4 and 8 core validations at the same time. CMSSW 7.3 and older versions do not support nThreads argument. Once 2, 4 and 8 core validations finish, values in reports are not checked, just saved.

### GEN request checking script and DQMIO upload to DQM GUI

GEN request checking script and DQMIO file upload to DQM GUI runs only during single core validation.

### Memory scaling in validation

If nThreads is 1, then request memory value is used for a single core validation. Memory for 2, 4 and 8 core validations are scaled linearly with one exception - if single core memory is 2300MB, then 2000MB is used for scale, that is 2 cores is 4000MB, 4 is 8000MB and 8 is 16000MB, otherwise it is cores x single\_core\_memory.

* Request with 2300 memory and 1 nThreads:
  * 1 core validation - 1 <= 1, not scale down, memory 2300 MB
  * 2 core validation - 2 > 1, scale up, single\_core\_memory × cores = 2000 x 2 = 4000 MB
  * 4 core validation - 4 > 1, scale up, single\_core\_memory × cores = 2000 x 4 = 8000 MB
  * 8 core validation - 8 > 1, scale up, single\_core\_memory × cores = 2000 x 8 = 16000 MB
* Request with 1900 memory and 1 nThreads:
  * 1 core validation - 1 <= 1, not scale down, memory 1900 MB
  * 2 core validation - 2 > 1, scale up, single\_core\_memory × cores = 1900 x 2 = 3800 MB
  * 4 core validation - 4 > 1, scale up, single\_core\_memory × cores = 1900 x 4 = 7600 MB
  * 8 core validation - 8 > 1, scale up, single\_core\_memory × cores = 1900 x 8 = 15200 MB

If nThreads is not 1, same request memory value is used for validations where cores <= nThreads, but is scaled up for validations where cores > nThreads. This is "scale only up, never down" strategy single\_core\_memory is calculated by dividing memory by nThreads. Then single\_core\_memory is multiplied by number of cores for validation - 2, 4 or 8. Example:

* Request with 4000 memory and 2 nThreads:
  * 1 core validation - 1 <= 2, not scale down, memory 4000MB
  * 2 core validation - 2 <= 2, not scale down, memory 4000MB
  * 4 core validation - 4 > 2, scale up, single\_core\_memory × cores = (4000 / 2) x 4 = 8000MB&#x20;
  * 8 core validation - 8 > 2, scale up, single\_core\_memory × cores = (4000 / 2)  8 = 16000MB
* Request with 9000 memory and 4 nThreads:
  * 1 core validation - 1 <= 4, not scale down, memory 9000 MB
  * 2 core validation - 2 <= 4, not scale down, memory 9000 MB
  * 4 core validation - 4 <= 4, not scale down, memory 9000 MB
  * 8 core validation - 8 > 4, scale up, single\_core\_memory × cores = (9000 / 4) \* 8 = 18000 MB

&#x20; single\_core\_memory is limited within 500MB and 4000MB, i.e.:

```
single_core_memory = max(500, min(4000, single_core_memory))
```

### MultiValidation values in McM

Validation results can be seen in McM column "Validation":

![PrepID and Validation columns](<../.gitbook/assets/Screenshot from 2020-07-06 13-53-49.png>)

### Request submission to computing

If request passed MultiValidation then number of cores, memory, time and size per event that will be submitted to computing will be taken from MultiValidation results. If request passed old validation, not MultiValidation then it will be submitted with nThreads cores and memory, size, time per event from request, like it was before.&#x20;

McM, just before submission will take results of validation with most cores where CPU efficiency is above 70%. If no such validation exists, then single core validation results will be used. Memory will be set to Peak value RSS with 10% margin rounded up to next thousands of MB, i.e.

```
memory = math.ceil((peak_value_rss * 1.1) / 1000.0) * 1000
```
