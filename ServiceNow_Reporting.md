# ServiceNow Reporting

- [Performance Analytics Indicators](https://docs.servicenow.com/bundle/newyork-performance-analytics-and-reporting/page/use/performance-analytics/concept/c_Indicators.html)
- [Reference - Performance Analytics Indicators](https://www.youtube.com/watch?v=QQNujcNOhlY)

## MTTR
Mean time to repair (MTTR) is a basic measure of the maintainability of repairable items. 
- It represents the average time required to repair a failed component or device.
- Expressed mathematically, it is 
```
the total corrective maintenance time for failures 
----------------------------------------------------------------------------------------------
the total number of corrective maintenance actions for failures during a given period of time.
```
- It generally does not include lead time for parts not readily available or other Administrative or Logistic Downtime (ALDT).

- In fault-tolerant design, MTTR is usually considered to also include the time the fault is latent (the time from when the failure occurs until it is detected). If a latent fault goes undetected until an independent failure occurs, 
the system may not be able to recover.

- MTTR is often part of a maintenance contract, where a system whose MTTR is 24 hours is generally more valuable than for one of 7 days if mean time between failures is equal, because its Operational Availability is higher.

- However, in the context of a maintenance contract, it would be important to distinguish whether MTTR is meant to be a measure of the mean time between the point at which the failure is first discovered until the point at which 
the equipment returns to operation (usually termed "mean time to recovery"), or only a measure of the elapsed time between the point where repairs actually begin until the point at which 
the equipment returns to operation (usually termed "mean time to repair"). 
- For example, a system with a service contract guaranteeing a mean time to "repair" of 24 hours, but with additional part lead times, administrative delays, and technician transportation delays adding up to a mean of 6 days, 
would not be any more attractive than another system with a service contract guaranteeing a mean time to "recovery" of 7 days.
