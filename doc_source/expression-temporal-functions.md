# Temporal functions<a name="expression-temporal-functions"></a>

You can use temporal functions to return values based on timestamps of data points\.

## Using temporal functions in metrics<a name="temporal-functions-in-metrics"></a>

In [metrics](metrics.md) only, you can use the following functions that return values based on timestamps of data points\.

Temporal function arguments must be properties from the local asset model or nested expressions\. This means that you can't use properties from child asset models in temporal functions\.

You can use nested expressions in temporal functions\. When you use nested expressions, the following rules apply: 
+ Each argument can have only one variable\.

  For example, `latest( t*9/5 + 32 )` is supported\.
+ Arguments can't be aggregation functions\.

  For example, `first( sum(x) )` isn't supported\.


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

## Using temporal functions in transforms<a name="temporal-functions-in-transforms"></a>

In [transforms](transforms.md) only, you can use the `pretrigger()` function to retrieve the `GOOD` quality value for a variable prior to the property update that triggered the current transform calculation\.

Consider an example where a manufacturer uses AWS IoT SiteWise to monitor the status of a machine\. The manufacturer uses the following measurements and transforms to represent the process:
+ A measurement, `current_state`, that can be 0 or 1\.
  + If the machine is in the cleaning state, `current_state` equals 1\.
  + If the machine is in the manufacturing state, `current_state` equals 0\.
+ A transform, `cleaning_state_duration`, that equals `if(pretrigger(current_state) == 1, timestamp(current_state) - timestamp(pretrigger(current_state)), none)`\. This transform returns how long the machine has been in the cleaning state in seconds, in the Unix epoch format\. For more information, see [Conditional functions](expression-conditional-functions.md) and the [timestamp\(\)](expression-date-and-time-functions.md) function\.

If the machine stays in the cleaning state longer than expected, the manufacturer might investigate the machine\.

You can also use the `pretrigger()` function in multivariate transforms\. For example, you have two measurements named `x` and `y`, and a transform, `z`, that equals `x + y + pretrigger(y)`\. The following table shows the values for `x`, `y`, and `z` from 9:00 AM to 9:15 AM\.

**Note**  
This example assumes that the values for the measurements arrive chronologically\. For example, the value of `x` for 09:00 AM arrives before the value of `x` for 09:05 AM\.
If the data points for 9:05 AM arrive before the data points for 9:00 AM, `z` isn't calculated at 9:05 AM\.
If the value of `x` for 9:05 AM arrives before the value of `x` for 09:00 AM and the values of `y` arrive chronologically, `z` equals `22 = 20 + 1 + 1` at 9:05 AM\.


|  | 09:00 AM | 09:05 AM | 09:10 AM | 09:15 AM | 
| --- | --- | --- | --- | --- | 
|  `x`  |  10  |  20  |    |  30  | 
|  `y`  |  1  |  2  |  3  |    | 
|  `z = x + y + pretrigger(y)`  |  `y` doesn't receive any data point before 09:00 AM\. Therefore, `z` isn't calculated at 09:00 AM\.  |  23 = 20 \+ 2 \+ 1 `pretrigger(y)` equals 1\.  |  25 = 20 \+ 3 \+ 2 `x` doesn't receive a new data point\. `pretrigger(y)` equals 2\.  |  36 = 30 \+ 3 \+ 3 `y` doesn't receive a new data point\. Therefore, `pretrigger(y)` equals 3 at 09:15 AM\.  | 