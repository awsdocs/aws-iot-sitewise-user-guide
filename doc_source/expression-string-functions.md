# String functions<a name="expression-string-functions"></a>

In [transforms](transforms.md) and [metrics](metrics.md), you can use the following functions to operate on strings\. For more information, see [Using strings in formulas](expression-tutorials.md#use-strings-in-formulas)\.

**Important**  
<a name="formula-output-rules"></a>Formula expressions can only output double values\. Nested expressions can output other data types, such as strings, but the formula as a whole must evaluate to a number\. You can use the [jp function](#jp-definition) to convert a string to a number\. If you define a formula that computes a non\-numeric value, AWS IoT SiteWise doesn't output a data point for that computation\. For more information, see [Undefined, infinite, and overflow values](expression-tutorials.md#undefined-values)\.


| Function | Description | 
| --- | --- | 
|  `len(s)`  |  Returns the length of the string `s`\.  | 
|  `find(s, substring)`  |  Returns the index of the string `substring` in the string `s`\.  | 
|  `contains(s, substring)`  |  Returns `1` if the string `s` contains the string `substring`, otherwise `0`\.  | 
|  `upper(s)`  |  Returns the string `s` in uppercase form\.  | 
|  `lower(s)`  |  Returns the string `s` in lowercase form\.  | 
|   `jp(s, json_path)`  |  Evaluates the string `s` with the [JsonPath](https://github.com/json-path/JsonPath) expression `json_path` and returns the result\. Use this function to do the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/expression-string-functions.html) To extract a string value from a JSON structure and return it as a number, you must use multiple nested `jp` functions\. The outer `jp` function extracts the string from the JSON structure, and the inner `jp` function converts the string to a number\. The string `json_path` must contain a string literal\. This means that `json_path` can't be an expression that evaluates to a string\. 

**Examples**  
+ `jp('{"status":"active","value":15}', '$.value')` returns `15`\.
+ `jp('{"measurement":{"reading":25,"confidence":0.95}}', '$.measurement.reading')` returns `25`\.
+ `jp('[2,8,23]', '$[2]')` returns `23`\.
+ `jp('{"values":[3,6,7]}', '$.values[1]')` returns `6`\.
+ `jp('111', '$')` returns `111`\.
+ `jp(jp('{"measurement":{"reading":25,"confidence":"0.95"}}', '$.measurement.confidence'), '$')` returns `0.95`\.  | 
|  `join(s0, s1, s2, s3, ...)`  |  Returns a concatenated string with a delimiter\. This function uses the first input string as a delimiter and joins the remaining input strings together\. This behaves similar to the [join\(CharSequence delimiter, CharSequence\.\.\. elements\)](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#join-java.lang.CharSequence-java.lang.CharSequence...-) function in Java\. 

**Examples**  
+ `join("-", "aa", "bb", "cc")` returns `aa-bb-cc`  | 
|  `format(expression: "format")` or `format("format", expression)`  |  Returns a string in the specified format\. This function evaluates `expression` to a value, and then returns the value in the specified format\. This behaves similar to the [format\(String format, Object\.\.\. args\)](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#format-java.lang.String-java.lang.Object...-) function in Java\. For more information about supported formats, see Conversions under [Class Formatter](https://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html) in the *Java Platform, Standard Edition 7 API Specification*\. 

**Examples**  
+ `format(100+1: "d")` returns an integer, `101`\.
+ `format("The result is %d", 100+1)` returns a string, `The result is 101`\.  | 
|  `f'expression'`  |  Returns a concatenated string\. With this formatted function, you can use a simple expression to concatenate and format strings\. These functions may contain nested expressions\. You can use `{}` \(curly braces\) to interpolate expressions\. This behaves similar to the [formatted string literals](https://docs.python.org/3/reference/lexical_analysis.html#f-strings) in Python\. 

**Examples**  
+ `f'abc{1+2: "f"}d'` returns `abc3.000000d`\. To evaluate this example expression, do the following:

  1. `format(1+2: "f")` returns a floating point number, `3.000000`\.

  1. `join('', "abc", 1+2, 'd')` returns a string, `abc3.000000d`\.

  You can also write the expression in the the following way: `join('', "abc", format(1+2: "f"), 'd')`\.  | 