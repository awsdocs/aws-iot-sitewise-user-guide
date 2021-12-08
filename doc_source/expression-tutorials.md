# Formula expression tutorials<a name="expression-tutorials"></a>

You can follow these tutorials to use formula expressions in AWS IoT SiteWise\.

**Topics**
+ [Using strings in formulas](#use-strings-in-formulas)
+ [Filtering data points](#filter-data)
+ [Counting data points that match a condition](#count-filtered-data)
+ [Late data in formulas](#late-data)
+ [Data quality in formulas](#data-quality)
+ [Undefined, infinite, and overflow values](#undefined-values)

## Using strings in formulas<a name="use-strings-in-formulas"></a>

You can operate on strings in your formula expressions\. You also can input strings from variables that reference attribute and measurement properties\.

**Important**  
<a name="formula-output-rules"></a>Formula expressions can only output double or string values\. Nested expressions can output other data types, such as strings, but the formula as a whole must evaluate to a number or string\. You can use the [jp function](expression-string-functions.md#jp-definition) to convert a string to a number\. The Boolean value must be 1 \(true\) or 0 \(false\)\. For more information, see [Undefined, infinite, and overflow values](#undefined-values)\.

AWS IoT SiteWise provides the following formula expression features that you can use to operate on strings:
+ [String literals](expression-literals.md#string-literal-definition)
+ The [index operator](expression-operators.md#index-operator-definition) \(`s[index]`\)
+ The [slice operator](expression-operators.md#slice-operator-definition) \(`s[start:end:step]`\)
+ [Comparison functions](expression-comparison-functions.md), which you can use compare strings by [lexicographic order](https://en.wikipedia.org/wiki/Lexicographic_order)
+ [String functions](expression-string-functions.md), which includes the `jp` function that can parse serialized JSON objects and convert strings to numbers

## Filtering data points<a name="filter-data"></a>

You can use the [if function](expression-conditional-functions.md#if-definition) to filter out data points that don't meet a condition\. The `if` function evaluates a condition and returns different values for `true` and `false` results\. You can use the [none constant](expression-constants.md#none-definition) as an output for one case of an `if` function to discard the data point for that case\.

**To filter out data points that match a condition**
+ Create a transform that uses the `if` function to define a condition that checks if a condition is met, and returns `none` as either the `result_if_true` or `result_if_false` value\.

**Example: Filter out data points where water isn't boiling**  
Consider a scenario where you have a measurement, `temp_c`, that provides the temperature \(in Celsius\) of water in a machine\. You can define the following transform to filter out data points where the water isn't boiling:  
+ Transform: `boiling_temps = if(gte(temp_c, 100), temp_c, none)` – Returns the temperature if it's greater than or equal to 100 degrees Celsius, otherwise returns no data point\.

## Counting data points that match a condition<a name="count-filtered-data"></a>

You can use [comparison functions](expression-comparison-functions.md) and [sum\(\)](expression-aggregation-functions.md#sum-definition) to count the number of data points for which a condition is true\.

**To count data points that match a condition**

1. Create a transform that uses a comparison function to define a filter condition on another property\.

1. Create a metric that sums the data points where that condition is met\.

**Example: Count the number of data points where water is boiling**  
Consider a scenario where you have a measurement, `temp_c`, that provides the temperature \(in Celsius\) of water in a machine\. You can define the following transform and metric properties to count the number of data points where the water is boiling:  
+ Transform: `is_boiling = gte(temp_c, 100)` – Returns `1` if the temperature is greater than or equal to 100 degrees Celsius, otherwise returns `0`\.
+ Metric: `boiling_count = sum(is_boiling)` – Returns the number of data points where water is boiling\.

## Late data in formulas<a name="late-data"></a>

AWS IoT SiteWise supports late data ingestion of data that is up to 7 days old\. When AWS IoT SiteWise receives late data, it recalculates existing values for any metric that inputs the late data in a past window\. These recalculations result in data processing charges\.

**Note**  
When AWS IoT SiteWise computes properties that input late data, it uses each property's current formula expression\.

After AWS IoT SiteWise recalculates a past window for a metric, it replaces the previous value for that window\. If you enabled notifications for that metric, AWS IoT SiteWise also emits a property value notification\. This means that you can receive a new property value update notification for the same property and timestamp for which you previously received a notification\. If your applications or data lakes consume property value notifications, you must update the previous value with the new value so that their data is accurate\.

## Data quality in formulas<a name="data-quality"></a>

In AWS IoT SiteWise, each data point has a quality code, which can be one of the following:
+ `GOOD` – The data isn't affected by any issues\.
+ `BAD` – The data is affected by an issue such as sensor failure\.
+ `UNCERTAIN` – The data is affected by an issue such as sensor inaccuracy\.

AWS IoT SiteWise consumes only `GOOD` quality data when it computes transforms and metrics\. AWS IoT SiteWise outputs only `GOOD` quality data for successful computations\. If a computation is unsuccessful, then AWS IoT SiteWise doesn't output a data point for that computation\. This can occur if a computation results in an undefined, infinite, or overflow value\.

For more information about how to query data and filter by data quality, see [Querying asset property values and aggregates](query-industrial-data.md)\.

## Undefined, infinite, and overflow values<a name="undefined-values"></a>

Some formula expressions \(such as `x / 0`, `sqrt(-1)`, or `log(0)`\) calculate values that are undefined in a real number system, infinite, or outside the range supported by AWS IoT SiteWise\. When an asset property's expression computes an undefined, infinite, or overflow value, AWS IoT SiteWise doesn't output a data point for that computation\.

AWS IoT SiteWise also doesn't output a data point if it computes a non\-numeric value as the result of a formula expression\. This means that if you define a formula that computes a string, array, or the [none constant](expression-constants.md#none-definition), then AWS IoT SiteWise doesn't output a data point for that computation\.

**Examples**  
Each of the following formula expressions result in a value that AWS IoT SiteWise can't represent as a number\. AWS IoT SiteWise doesn't output a data point when it computes these formula expressions\.  
+ `x / 0` is undefined\.
+ `log(0)` is undefined\.
+ `sqrt(-1)` is undefined in a real number system\.
+ `"hello" + " world"` is a string\.
+ `jp('{"values":[3,6,7]}', '$.values')` is an array\.
+ `if(gte(temp, 300), temp, none)` is `none` when `temp` is less than `300`\.