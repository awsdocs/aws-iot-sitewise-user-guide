# Temporal functions<a name="expression-temporal-functions"></a>

In [metrics](metrics.md) only, you can use the following functions that return values based on timestamps of data points\.

Temporal function arguments must be properties from the local asset model\. This means that you can't use properties from child asset models in temporal functions\. You also can't use expressions as arguments to temporal functions\.


| Function | Description | 
| --- | --- | 
|  `first(x)`  |  Returns the given variable's value with the earliest timestamp over the current time interval\.  | 
|   `last(x)`  |  Returns the given variable's value with the latest timestamp over the current time interval\.  | 
|  `earliest(x)`  |  Returns the given variable's value with the earliest timestamp before the current time interval\. This function computes a data point for every time interval, if the input property has at least one data point in its history\.  | 
|   `latest(x)`  |  Returns the given variable's value with the latest timestamp before the end of the current time interval\. This function computes a data point for every time interval, if the input property has at least one data point in its history\.  | 
|   `statetime(x)`  |  Returns the amount of time in seconds that the given variables are positive over the current time interval\. You can use the [comparison functions](expression-comparison-functions.md) to create a transform property for the `statetime` function to consume\.  For example, if you have an `Idle` property that is `0` or `1`, you can calculate idle time per time interval with this expression: `IdleTime = statetime(Idle)`\. For more information, see the [example statetime scenario](#statetime-example)\. This function doesn't support metric properties as input variables\. This function computes a data point for every time interval, if the input property has at least one data point in its history\.  | 

The following diagram shows how AWS IoT SiteWise computes the temporal functions `first`, `last`, `earliest`, and `latest`, relative to the current time interval\.

![\[AWS IoT SiteWise temporal functions return data points based on their timestamp.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-temporal-functions.png)

**Example statetime scenario**  
Consider an example where you have an asset with the following properties:  
+ `Idle` – A measurement that is `0` or `1`\. When the value is `1`, the machine is idle\.
+ `Idle Time` – A metric that uses the formula `statetime(Idle)` to calculate the amount of time in seconds where the machine is idle, per 1 minute interval\.
The `Idle` property has the following data points\.  


|  |  |  |  |  |  | 
| --- |--- |--- |--- |--- |--- |
| Timestamp | 2:00:00 PM | 2:00:30 PM | 2:01:15 PM | 2:02:45 PM | 2:04:00 PM | 
| Idle | 0 | 1 | 1 | 0 | 0 | 
AWS IoT SiteWise calculates the `Idle Time` property every minute from the values of `Idle`\. After this calculation completes, the `Idle Time` property has the following data points\.  


|  |  |  |  |  |  | 
| --- |--- |--- |--- |--- |--- |
| Timestamp | 2:00:00 PM | 2:01:00 PM | 2:02:00 PM | 2:03:00 PM | 2:04:00 PM | 
| Idle Time | N/A | 30 | 60 | 45 | 0 | 
AWS IoT SiteWise performs the following calculations for `Idle Time` at the end of each minute\.  
+ At 2:00 PM \(for 1:59 PM to 2:00 PM\)
  + There is no data for `Idle` before 2:00 PM, so no data point is calculated\.
+ At 2:01 PM \(for 2:00 PM to 2:01 PM\)
  + At 2:00:00 PM, the machine is active \(`Idle` is `0`\)\.
  + At 2:00:30 PM, the machine is idle \(`Idle` is `1`\)\.
  + `Idle` doesn't change again before the end of the interval at 2:01:00 PM, so `Idle Time` is 30 seconds\.
+ At 2:02 PM \(for 2:01 PM to 2:02 PM\)
  + At 2:01:00 PM, the machine is idle \(per the last data point at 2:00:30 PM\)\.
  + At 2:01:15 PM, the machine is still idle\.
  + `Idle` doesn't change again before the end of the interval at 2:02:00 PM, so `Idle Time` is 60 seconds\.
+ At 2:03 PM \(for 2:02 PM to 2:03 PM\)
  + At 2:02:00 PM, the machine is idle \(per the last data point at 2:01:15 PM\)\.
  + At 2:02:45 PM, the machine is active\.
  + `Idle` doesn't change again before the end of the interval at 2:03:00 PM, so `Idle Time` is 45 seconds\.
+ At 2:04 PM \(for 2:03 PM to 2:04 PM\)
  + At 2:03:00 PM, the machine is active \(per the last data point at 2:02:45 PM\)\.
  + `Idle` doesn't change again before the end of the interval at 2:04:00 PM, so `Idle Time` is 0 seconds\.