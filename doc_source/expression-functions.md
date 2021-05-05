# Functions<a name="expression-functions"></a>

You can use the following functions to operate on data in your formula expressions\.

Transforms and metrics support different functions\. The following table indicates which types of functions are compatible with each type of formula property\.


| Function type | Transforms | Metrics | 
| --- | --- | --- | 
|  [Common functions](expression-common-functions.md)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Comparison functions](expression-comparison-functions.md)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Conditional functions](expression-conditional-functions.md)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [String functions](expression-string-functions.md)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Aggregation functions](expression-aggregation-functions.md)  |  <a name="polaris-no-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-no.png) No  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Temporal functions](expression-temporal-functions.md)  |  <a name="polaris-no-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-no.png) No  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 
|  [Date and time functions](expression-date-and-time-functions.md)  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  |  <a name="polaris-yes-para"></a>![\[Image NOT FOUND\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/icon-yes.png) Yes  | 

## Function syntax<a name="expression-function-syntax"></a>

You can use the following syntax to create functions:

Regular syntax  
With the regular syntax, the function name is followed by parentheses with zero or more arguments\.  
`function_name(argument1, argument2, argument3, ...)`\. For example, functions with the regular syntax might look like `log(x)` and `contains(s, substring)`\.

Uniform function call syntax \(UFCS\)  
UFCS enables you to call functions using the syntax for method calls in object\-oriented programming\. With UFCS, the first argument is followed by dot \(`.`\), then the function name and the remaining arguments \(if any\) inside parentheses\.  
`argument1.function_name(argument2, argument3, ...)`\. For example, functions with UFCS might look like `x.log()` and `s.contains(substring)`\.  
You can also use UFCS to chain subsequent functions\. AWS IoT SiteWise uses the evaluation result of the current function as the first argument for the next function\.  
For example, you can use `message.jp('$.status').lower().contains('fail')` instead of `contains(lower(jp(message, '$.status')),'fail')`\.  
For more information, visit the [D Programming Language](https://tour.dlang.org/tour/en/gems/uniform-function-call-syntax-ufcs) website\.

**Note**  
You can use UFCS for all AWS IoT SiteWise functions\.  
AWS IoT SiteWise functions are not case sensitive\. For example, you can use `lower(s)` and `Lower(s)` interchangeably\.