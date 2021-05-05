# Aggregation functions<a name="expression-aggregation-functions"></a>

In [metrics](metrics.md) only, you can use the following functions that aggregate input values over each time interval and calculate a single output value\. Aggregation functions can aggregate data from associated assets\.

Aggregation function arguments can be [variables](expression-variables.md), [number literals](expression-literals.md#number-literal-definition), [temporal functions](expression-temporal-functions.md), or aggregation functions\. This means that you can't provide nested expressions as arguments to aggregation functions\. For example, the formula `avg(x + 1)` isn't valid\. By contrast, the formula `max(latest(x), latest(y), latest(z))` is valid and returns the largest current value of the `x`, `y`, and `z` properties\.

**Note**  
AWS IoT SiteWise also automatically computes aggregates over certain time intervals for all properties\. For more information, see [Querying asset property aggregates](query-industrial-data.md#aggregates)\.


| Function | Description | 
| --- | --- | 
|  `avg(x0, ..., xn)`  |  Returns the mean of the given variables' values over the current time interval\. <a name="aggregation-function-no-output"></a>This function outputs a data point only if the given variables have at least one data point over the current time interval\.  | 
|   `sum(x0, ..., xn)`  |  Returns the sum of the given variables' values over the current time interval\. <a name="aggregation-function-no-output"></a>This function outputs a data point only if the given variables have at least one data point over the current time interval\.  | 
|  `min(x0, ..., xn)`  |  Returns the minimum of the given variables' values over the current time interval\. <a name="aggregation-function-no-output"></a>This function outputs a data point only if the given variables have at least one data point over the current time interval\.  | 
|  `max(x0, ..., xn)`  |  Returns the maximum of the given variables' values over the current time interval\. <a name="aggregation-function-no-output"></a>This function outputs a data point only if the given variables have at least one data point over the current time interval\.  | 
|  `count(x0, ..., xn)`  |  Returns the total number of data points for the given variables over the current time interval\. For more information about how to count the number of data points that meet a condition, see [Counting data points that match a condition](expression-tutorials.md#count-filtered-data)\. <a name="aggregation-function-always-output"></a>This function computes a data point for every time interval\.  | 