# Conditional functions<a name="expression-conditional-functions"></a>

In [transforms](transforms.md) and [metrics](metrics.md), you can use the following function to check a condition and return different results whether the condition evaluates to true or false\.


| Function | Description | 
| --- | --- | 
|   `if(condition, result_if_true, result_if_false)`  |  Evaluates the `condition` and returns `result_if_true` if the condition evaluates to true or `result_if_false` if the condition evaluates to false\. `condition` must be a number\. This function considers `0` and an empty string as false and everything else \(including `NaN`\) as true\. Booleans convert to `0` \(false\) and `1` \(true\)\. You can return the [none constant](expression-constants.md#none-definition) from this function to discard the output for a particular condition\. This means you can filter out data points that don't meet a condition\. For more information, see [Filtering data points](expression-tutorials.md#filter-data)\.   

**Examples**  
+ `if(0, x, y)` returns the variable `y`\.
+ `if(5, x, y)` returns the variable `x`\.
+ `if(gt(temp, 300), x, y)` returns the variable `x` if the variable `temp` is greater than `300`\.
+ `if(gt(temp, 300), temp, none)` returns the variable `temp` if it's greater than or equal to `300`, or `none` \(no value\) if `temp` is less than `300`\. We recommend that you use UFCS for nested conditional functions where one or more arguments are conditional functions\. You can use `if(condition, result_if_true)` to evaluate a condition and `elif(condition, result_if_true, result_if_false)` to evaluate additional conditions\. For example, you can use `if(condition1, result1_if_true).elif(condition2, result2_if_true, result2_if_false)` instead of `if(condition1, result1_if_true, if(condition2, result2_if_true, result2_if_false))`\.  You must use `elif(condition, result_if_true, result_if_false)` with UFCS\.   | 