# Operators<a name="expression-operators"></a>

You can use the following common operators in formula expressions\.


| Operator | Description | 
| --- | --- | 
| `+` |  If both operands are numbers, this operator adds the left and right operands\. If either operand is a string, this operator concatenates the left and right operands as strings\. For example, the expression `1 + 2 + " is three"` evaluates to `"3 is three"`\. The concatenated string can have up to 1024 characters\. If the string exceeds 1024 characters, then AWS IoT SiteWise doesn't output a data point for that computation\.  | 
| `-` |  Subtracts the right operand from the left operand\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
| `/` |  Divides the left operand by the right operand\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
| `*` |  Multiplies the left and right operands\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
| `^` |  Raises the left operand to the power of the right operand \(exponentiation\)\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
| `%` |  Returns the remainder from dividing the left operand by the right operand\. The result has the same sign as the left operand\. This behavior differs from the modulo operation\. <a name="operator-numbers-only"></a>You can only use this operator with numeric operands\.  | 
|   `x < y`  |  Returns `1` if `x` is less than `y`, otherwise `0`\.  | 
|   `x > y`  |  Returns `1` if `x` is greater than `y`, otherwise `0`\.  | 
|   `x <= y`  |  Returns `1` if `x` is less than or equal to `y`, otherwise `0`\.  | 
|   `x >= y`  |  Returns `1` if `x` is greater than or equal to `y`, otherwise `0`\.  | 
|   `x == y`  |  Returns `1` if `x` is equal to `y`, otherwise `0`\.  | 
|   `x != y`  |  Returns `1` if `x` is not equal to `y`, otherwise `0`\.  | 
|   `!x`  |  Returns `1` if `x` is evaluated to `0` \(false\), otherwise `0`\. `x` is evaluated to false if:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/expression-operators.html)  | 
|   `x and y`  |  Returns `0` if `x` is evaluated to `0` \(false\)\. Otherwise, returns the evaluated result of `y`\. `x` or `y` is evaluated to false if:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/expression-operators.html)  | 
|   `x or y`  |  Returns `1` if `x` is evaluated to `1` \(true\)\. Otherwise, returns the evaluated result of `y`\. `x` or `y` is evaluated to false if:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/expression-operators.html)  | 
|   `not x`  |  Returns `1` if `x` is evaluated to `0` \(false\), otherwise `0`\. `x` is evaluated to false if:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/expression-operators.html)  | 
|   `[]` `s[index]`  |  Returns the character at an index `index` of the string `s`\. This is equivalent to the index syntax in Python\. 

**Examples**  
+ `"Hello!"[1]` returns `e`\.
+ `"Hello!"[-2]` returns `o`\.  | 
|   `[]` `s[start:end:step]`  |  Returns a slice of the string `s`\. This is equivalent to the slice syntax in Python\. This operator has the following arguments: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/expression-operators.html) You can omit the `step` argument to use its default value\. For example, `s[1:4:1]` is equivalent to `s[1:4]`\. The arguments must be integers or the [none](expression-constants.md#none-definition) constant\. If you specify `none`, AWS IoT SiteWise uses the default value for that argument\. 

**Examples**  
+ `"Hello!"[1:4]` returns `"ell"`\.
+ `"Hello!"[:2]` returns `"He"`\.
+ `"Hello!"[3:]` returns `"lo!"`\.
+ `"Hello!"[:-4]` returns `"He"`\.
+ `"Hello!"[::2]` returns `"Hlo"`\.
+ `"Hello!"[::-1]` returns `"!olleH"`\.  | 