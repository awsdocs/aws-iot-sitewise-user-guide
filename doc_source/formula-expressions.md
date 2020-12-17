# Using formula expressions<a name="formula-expressions"></a>

With formula expressions, you can define the mathematical functions to transform and aggregate your raw industrial data to gain insights about your operation\. For more information about how to define asset properties that use formula expressions, see [Transforming data \(transforms\)](transforms.md) and [Aggregating data from properties and other assets \(metrics\)](metrics.md)\. Transforms and metrics are formula properties\.

**Contents**
+ [Variables](#expression-variables)
+ [Literals](#expression-literals)
+ [Operators](#expression-operators)
+ [Constants](#expression-constants)
+ [Functions](#expression-functions)
  + [Common functions](#expression-common-functions)
  + [Comparison functions](#expression-comparison-functions)
  + [Conditional functions](#expression-conditional-functions)
  + [String functions](#expression-string-functions)
  + [Aggregation functions](#expression-aggregation-functions)
  + [Temporal functions](#expression-temporal-functions)
+ [Using strings in formulas](#use-strings-in-formulas)
+ [Filtering data points](#filter-data)
+ [Counting data points that match a condition](#count-filtered-data)
+ [Late data in formulas](#late-data)
+ [Data quality in formulas](#data-quality)
+ [Undefined, infinite, and overflow values](#undefined-values)

## Variables<a name="expression-variables"></a>

Variables represent AWS IoT SiteWise asset properties in formula expressions\. Use variables to input values from other asset properties in your expressions, so that you can process data from constant properties \([attributes](attributes.md)\), raw data streams \([measurements](measurements.md)\), and other formula properties\.

Variables can represent asset properties from the same asset model or from associated child asset models\. Only metric formulas can input variables from child asset models\.

You identify variables by different names in the console and the API\.
+ **AWS IoT SiteWise console** – Use asset property names as variables in your expressions\.
+ **AWS IoT SiteWise API \(AWS CLI, AWS SDKs\)** – Define variables with the [ExpressionVariable](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ExpressionVariable.html) structure, which requires a variable name and a reference to an asset property\. The variable name can contain lowercase letters, numbers, and underscores\. Then, use variable names to reference asset properties in your expressions\.

Variable names are case sensitive\.

For more information, see [Defining transforms](transforms.md) and [Defining metrics](metrics.md)\.

## Literals<a name="expression-literals"></a>

You can define number and string literals in formula expressions\.
+ <a name="number-literal-definition"></a>**Numbers**

  Use numbers and scientific notation to define integers and doubles\. You can use [E notation](https://en.wikipedia.org/wiki/Scientific_notation#E_notation) to express numbers with scientific notation\.

  Examples: `1`, `2.0`, `.9`, `-23.1`, `7.89e3`, `3.4E-5`
+ <a name="string-literal-definition"></a>**Strings**

  Use the `'` \(quote\) and `"` \(double quote\) characters to define strings\. The quote type for the start and end must match\. To escape a quote that matches the one that you use to declare a string, include that quote character twice\. This is the only escape character in AWS IoT SiteWise strings\.

  Examples: `'active'`, `"inactive"`, `'{"temp": 52}'`, `"{""temp"": ""high""}"`

## Operators<a name="expression-operators"></a>

You can use the following common operators in formula expressions\.


| Operator | Description | 
| --- | --- | 
| `+` |  If both operands are numbers, this operator adds the left and right operands\. If either operand is a string, this operator concatenates the left and right operands as strings\. For example, the expression `1 + 2 + " is three"` evaluates to `"3 is three"`\. The concatenated string can have up to 1024 characters\. If the string exceeds 1024 characters, then AWS IoT SiteWise doesn't output a data point for that computation\.  | 
| `-` |  Subtracts the right operand from the left operand\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
| `/` |  Divides the left operand by the right operand\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
| `*` |  Multiplies the left and right operands\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
| `^` |  Raises the left operand to the power of the right operand \(exponentiation\)\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
| `%` |  Returns the remainder from dividing the left operand by the right operand\. The result has the same sign as the left operand\. This behavior differs from the modulo operation\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
|   `[]` `s[index]`  |  Returns the character at an index `index` of the string `s`\. This is equivalent to the index syntax in Python\. 

**Examples**  
+ `"Hello!"[1]` returns `e`\.
+ `"Hello!"[-2]` returns `o`\.  | 
|   `[]` `s[start:end:step]`  |  Returns a slice of the string `s`\. This is equivalent to the slice syntax in Python\. This operator has the following arguments: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/formula-expressions.html) You can omit the `step` argument to use its default value\. For example, `s[1:4:1]` is equivalent to `s[1:4]`\. The arguments must be integers or the [none](#none-definition) constant\. If you specify `none`, AWS IoT SiteWise uses the default value for that argument\. 

**Examples**  
+ `"Hello!"[1:4]` returns `"ell"`\.
+ `"Hello!"[:2]` returns `"He"`\.
+ `"Hello!"[3:]` returns `"lo!"`\.
+ `"Hello!"[:-4]` returns `"He"`\.
+ `"Hello!"[::2]` returns `"Hlo"`\.
+ `"Hello!"[::-1]` returns `"!olleH"`\.  | 

## Constants<a name="expression-constants"></a>

You can use the following common mathematical constants in your expressions\. All constants are case insensitive\.

**Note**  
If you define a variable with the same name as a constant, the variable overrides the constant\.


| Constant | Description | 
| --- | --- | 
| `pi` |  The number pi \(`π`\): `3.141592653589793`  | 
| `e` |  The number e: `2.718281828459045`  | 
| `true` |  Equivalent to the number 1\. In AWS IoT SiteWise, Booleans convert to their number equivalents\.  | 
| `false` |  Equivalent to the number 0\. In AWS IoT SiteWise, Booleans convert to their number equivalents\.  | 
|   `none`  |  Equivalent to no value\. You can use this constant to output nothing as the result of a [conditional expression](#expression-conditional-functions)\.  | 

## Functions<a name="expression-functions"></a>

You can use the following functions to operate on data in your formula expressions\.

Transforms and metrics support different functions\. The following table indicates which types of functions are compatible with each type of formula property\.


| Function type | Transforms | Metrics | 
| --- | --- | --- | 
|  [Common functions](#expression-common-functions)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Comparison functions](#expression-comparison-functions)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Conditional functions](#expression-conditional-functions)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [String functions](#expression-string-functions)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Aggregation functions](#expression-aggregation-functions)  |  <a name="polaris-no-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-no.png) No  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Temporal functions](#expression-temporal-functions)  |  <a name="polaris-no-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-no.png) No  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 

### Common functions<a name="expression-common-functions"></a>

In [transforms](transforms.md) and [metrics](metrics.md), you can use the following functions to calculate common mathematical functions in transforms and metrics\.


| Function | Description | 
| --- | --- | 
| `abs(x)` |  Returns the absolute value of `x`\.  | 
| `acos(x)` |  Returns the arccosine of `x`\.  | 
| `asin(x)` |  Returns the arcsine of `x`\.  | 
| `atan(x)` |  Returns the arctangent of `x`\.  | 
| `cbrt(x)` |  Returns the cubic root of `x`\.  | 
| `ceil(x)` |  Returns the nearest integer greater than `x`\.  | 
| `cos(x)` |  Returns the cosine of `x`\.  | 
| `cosh(x)` |  Returns the hyperbolic cosine of `x`\.  | 
| `cot(x)` |  Returns the cotangent of `x`\.  | 
| `exp(x)` |  Returns `e` to the power of `x`\.  | 
| `expm1(x)` |  Returns `exp(x) - 1`\. Use this function to more accurately calculate `exp(x) - 1` for small values of `x`\.  | 
| `floor(x)` |  Returns the nearest integer less than `x`\.  | 
| `log(x)` |  Returns the `loge` \(base `e`\) of `x`\.  | 
| `log10(x)` |  Returns the `log10` \(base `10`\) of `x`\.  | 
| `log1p(x)` |  Returns `log(1 + x)`\. Use this function to more accurately calculate `log(1 + x)` for small values of `x`\.  | 
| `log2(x)` |  Returns the `log2` \(base `2`\) of `x`\.  | 
| `pow(x, y)` |  Returns `x` to the power of `y`\. This is equivalent to `x ^ y`\.  | 
| `signum(x)` |  Returns the sign of `x` \(`-1` for negative inputs, `0` for zero inputs, `+1` for positive inputs\)\.  | 
| `sin(x)` |  Returns the sine of `x`\.  | 
| `sinh(x)` |  Returns the hyperbolic sine of `x`\.  | 
| `sqrt(x)` |  Returns the square root of `x`\.  | 
| `tan(x)` |  Returns the tangent of `x`\.  | 
| `tanh(x)` |  Returns the hyperbolic tangent of `x`\.  | 

### Comparison functions<a name="expression-comparison-functions"></a>

In [transforms](transforms.md) and [metrics](metrics.md), you can use the following comparison functions to compare two values and output `1` \(true\) or `0` \(false\)\. AWS IoT SiteWise compares strings by [lexicographic order](https://en.wikipedia.org/wiki/Lexicographic_order)\.


| Function | Description | 
| --- | --- | 
| `gt(x, y)` |  Returns `1` if `x` is greater than `y`, otherwise `0` \(`x > y`\)\. <a name="comparison-function-incompatible-types"></a>This function doesn't return a value if `x` and `y` are incompatible types, such as a number and a string\.  | 
| `gte(x, y)` |  Returns `1` if `x` is greater than or equal to `y`, otherwise `0` \(`x ≥ y`\)\. <a name="comparison-function-relative-tolerance"></a>AWS IoT SiteWise considers the arguments equal if they are within a relative tolerance of `1E-9`\. This behaves similar to the [isclose](https://docs.python.org/3/library/math.html#math.isclose) function in Python\. <a name="comparison-function-incompatible-types"></a>This function doesn't return a value if `x` and `y` are incompatible types, such as a number and a string\.  | 
| `eq(x, y)` |  Returns `1` if `x` is equal to `y`, otherwise `0` \(`x == y`\)\. <a name="comparison-function-relative-tolerance"></a>AWS IoT SiteWise considers the arguments equal if they are within a relative tolerance of `1E-9`\. This behaves similar to the [isclose](https://docs.python.org/3/library/math.html#math.isclose) function in Python\.  | 
| `lt(x, y)` |  Returns `1` if `x` is less than `y`, otherwise `0` \(`x < y`\)\. <a name="comparison-function-incompatible-types"></a>This function doesn't return a value if `x` and `y` are incompatible types, such as a number and a string\.  | 
| `lte(x, y)` |  Returns `1` if `x` is less than or equal to `y`, otherwise `0` \(`x ≤ y`\)\. <a name="comparison-function-relative-tolerance"></a>AWS IoT SiteWise considers the arguments equal if they are within a relative tolerance of `1E-9`\. This behaves similar to the [isclose](https://docs.python.org/3/library/math.html#math.isclose) function in Python\. <a name="comparison-function-incompatible-types"></a>This function doesn't return a value if `x` and `y` are incompatible types, such as a number and a string\.  | 
| `isnan(x)` |  Returns `1` if `x` is equal to `NaN`, otherwise `0`\. This function doesn't return a value if `x` is a string\.  | 

### Conditional functions<a name="expression-conditional-functions"></a>

In [transforms](transforms.md) and [metrics](metrics.md), you can use the following function to check a condition and return different results whether the condition evaluates to true or false\.


| Function | Description | 
| --- | --- | 
|   `if(condition, result_if_true, result_if_false)`  |  Evaluates the `condition` and returns `result_if_true` if the condition evaluates to true or `result_if_false` if the condition evaluates to false\. `condition` must be a number\. This function considers `0` as false and everything else \(including `NaN`\) as true\. Booleans convert to `0` \(false\) and `1` \(true\)\. You can return the [none constant](#none-definition) from this function to discard the output for a particular condition\. This means you can filter out data points that don't meet a condition\. For more information, see [Filtering data points](#filter-data)\.   

**Examples**  
+ `if(0, x, y)` returns the variable `y`\.
+ `if(5, x, y)` returns the variable `x`\.
+ `if(gt(temp, 300), x, y)` returns the variable `x` if the variable `temp` is greater than `300`\.
+ `if(gt(temp, 300), temp, none)` returns the variable `temp` if it's greater than or equal to `300`, or `none` \(no value\) if `temp` is less than `300`\.  | 

### String functions<a name="expression-string-functions"></a>

In [transforms](transforms.md) and [metrics](metrics.md), you can use the following functions to operate on strings\. For more information, see [Using strings in formulas](#use-strings-in-formulas)\.

**Important**  
<a name="formula-output-rules"></a>Formula expressions can only output double values\. Nested expressions can output other data types, such as strings, but the formula as a whole must evaluate to a number\. You can use the [jp function](#jp-definition) to convert a string to a number\. If you define a formula that computes a non\-numeric value, AWS IoT SiteWise doesn't output a data point for that computation\. For more information, see [Undefined, infinite, and overflow values](#undefined-values)\.


| Function | Description | 
| --- | --- | 
| `len(s)` |  Returns the length of the string `s`\.  | 
| `find(s, substring)` |  Returns the index of the string `substring` in the string `s`\.  | 
| `contains(s, substring)` |  Returns `1` if the string `s` contains the string `substring`, otherwise `0`\.  | 
| `upper(s)` |  Returns the string `s` in uppercase form\.  | 
| `lower(s)` |  Returns the string `s` in lowercase form\.  | 
|   `jp(s, json_path)`  |  Evaluates the string `s` with the [JsonPath](https://github.com/json-path/JsonPath) expression `json_path` and returns the result\. Use this function to do the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/formula-expressions.html) To extract a string value from a JSON structure and return it as a number, you must use multiple nested `jp` functions\. The outer `jp` function extracts the string from the JSON structure, and the inner `jp` function converts the string to a number\. The string `json_path` must contain a string literal\. This means that `json_path` can't be an expression that evaluates to a string\. 

**Examples**  
+ `jp('{"status":"active","value":15}', '$.value')` returns `15`\.
+ `jp('{"measurement":{"reading":25,"confidence":0.95}}', '$.measurement.reading')` returns `25`\.
+ `jp('[2,8,23]', '$[2]')` returns `23`\.
+ `jp('{"values":[3,6,7]}', '$.values[1]')` returns `6`\.
+ `jp('111', '$')` returns `111`\.
+ `jp(jp('{"measurement":{"reading":25,"confidence":"0.95"}}', '$.measurement.confidence'), '$')` returns `0.95`\.  | 

### Aggregation functions<a name="expression-aggregation-functions"></a>

In [metrics](metrics.md) only, you can use the following functions that aggregate input values over each time interval and calculate a single output value\. Aggregation functions can aggregate data from associated assets\.

Aggregation function arguments can be [variables](#expression-variables), [number literals](#number-literal-definition), [temporal functions](#expression-temporal-functions), or aggregation functions\. This means that you can't provide nested expressions as arguments to aggregation functions\. For example, the formula `avg(x + 1)` isn't valid\. By contrast, the formula `max(latest(x), latest(y), latest(z))` is valid and returns the largest current value of the `x`, `y`, and `z` properties\.

**Note**  
AWS IoT SiteWise also automatically computes aggregates over certain time intervals for all properties\. For more information, see [Querying asset property aggregates](query-industrial-data.md#aggregates)\.


| Function | Description | 
| --- | --- | 
|  `avg(x0, ..., xn)`  |  Returns the mean of the given variables' values over the current time interval\. <a name="aggregation-function-no-output"></a>This function outputs a data point only if the given variables have at least one data point over the current time interval\.  | 
|   `sum(x0, ..., xn)`  |  Returns the sum of the given variables' values over the current time interval\. <a name="aggregation-function-no-output"></a>This function outputs a data point only if the given variables have at least one data point over the current time interval\.  | 
|  `min(x0, ..., xn)`  |  Returns the minimum of the given variables' values over the current time interval\. <a name="aggregation-function-no-output"></a>This function outputs a data point only if the given variables have at least one data point over the current time interval\.  | 
|  `max(x0, ..., xn)`  |  Returns the maximum of the given variables' values over the current time interval\. <a name="aggregation-function-no-output"></a>This function outputs a data point only if the given variables have at least one data point over the current time interval\.  | 
|  `count(x0, ..., xn)`  |  Returns the total number of data points for the given variables over the current time interval\. For more information about how to count the number of data points that meet a condition, see [Counting data points that match a condition](#count-filtered-data)\. <a name="aggregation-function-always-output"></a>This function computes a data point for every time interval\.  | 

### Temporal functions<a name="expression-temporal-functions"></a>

In [metrics](metrics.md) only, you can use the following functions that return values based on timestamps of data points\.

Temporal function arguments must be properties from the local asset model\. This means that you can't use properties from child asset models in temporal functions\. You also can't use expressions as arguments to temporal functions\.


| Function | Description | 
| --- | --- | 
| `first(x)` |  Returns the given variable's value with the earliest timestamp over the current time interval\.  | 
|   `last(x)`  |  Returns the given variable's value with the latest timestamp over the current time interval\.  | 
| `earliest(x)` |  Returns the given variable's value with the latest timestamp before the current time interval\. This function computes a data point for every time interval, if the input property has at least one data point in its history\.  | 
|   `latest(x)`  |  Returns the given variable's value with the latest timestamp before the end of the current time interval\. This function computes a data point for every time interval, if the input property has at least one data point in its history\.  | 
|   `statetime(x)`  |  Returns the amount of time in seconds that the given variables are positive over the current time interval\. You can use the [comparison functions](#expression-comparison-functions) to create a transform property for the `statetime` function to consume\.  For example, if you have an `Idle` property that is `0` or `1`, you can calculate idle time per time interval with this expression: `IdleTime = statetime(Idle)`\. For more information, see the [example statetime scenario](#statetime-example)\. This function doesn't support metric properties as input variables\. This function computes a data point for every time interval, if the input property has at least one data point in its history\.  | 

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

## Using strings in formulas<a name="use-strings-in-formulas"></a>

You can operate on strings in your formula expressions\. You also can input strings from variables that reference attribute and measurement properties\.

**Important**  
<a name="formula-output-rules"></a>Formula expressions can only output double values\. Nested expressions can output other data types, such as strings, but the formula as a whole must evaluate to a number\. You can use the [jp function](#jp-definition) to convert a string to a number\. If you define a formula that computes a non\-numeric value, AWS IoT SiteWise doesn't output a data point for that computation\. For more information, see [Undefined, infinite, and overflow values](#undefined-values)\.

AWS IoT SiteWise provides the following formula expression features that you can use to operate on strings:
+ [String literals](#string-literal-definition)
+ The [index operator](#index-operator-definition) \(`s[index]`\)
+ The [slice operator](#slice-operator-definition) \(`s[start:end:step]`\)
+ [Comparison functions](#expression-comparison-functions), which you can use compare strings by [lexicographic order](https://en.wikipedia.org/wiki/Lexicographic_order)
+ [String functions](#expression-string-functions), which includes the `jp` function that can parse serialized JSON objects and convert strings to numbers

## Filtering data points<a name="filter-data"></a>

You can use the [if function](#if-definition) to filter out data points that don't meet a condition\. The `if` function evaluates a condition and returns different values for `true` and `false` results\. You can use the [none constant](#none-definition) as an output for one case of an `if` function to discard the data point for that case\.

**To filter out data points that match a condition**
+ Create a transform that uses the `if` function to define a condition that checks if an condition is met, and returns `none` as either the `result_if_true` or `result_if_false` value\.

**Example: Filter out data points where water isn't boiling**  
Consider a scenario where you have a measurement, `temp_c`, that provides the temperature \(in Celsius\) of water in a machine\. You can define the following transform to filter out data points where the water isn't boiling:  
+ Transform: `boiling_temps = if(gte(temp_c, 100), temp_c, none)` – Returns the temperature if it's greater than or equal to 100 degrees Celsius, otherwise returns no data point\.

## Counting data points that match a condition<a name="count-filtered-data"></a>

You can use [comparison functions](#expression-comparison-functions) and [sum\(\)](#sum-definition) to count the number of data points for which a condition is true\.

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

AWS IoT SiteWise also doesn't output a data point if it computes a non\-numeric value as the result of a formula expression\. This means that if you define a formula that computes a string, array, or the [none constant](#none-definition), then AWS IoT SiteWise doesn't output a data point for that computation\.

**Examples**  
Each of the following formula expressions result in a value that AWS IoT SiteWise can't represent as a number\. AWS IoT SiteWise doesn't output a data point when it computes these formula expressions\.  
+ `x / 0` is undefined\.
+ `log(0)` is undefined\.
+ `sqrt(-1)` is undefined in a real number system\.
+ `"hello" + " world"` is a string\.
+ `jp('{"values":[3,6,7]}', '$.values')` is an array\.
+ `if(gte(temp, 300), temp, none)` is `none` when `temp` is less than `300`\.