# Literals<a name="expression-literals"></a>

You can define number and string literals in formula expressions\.
+ <a name="number-literal-definition"></a>**Numbers**

  Use numbers and scientific notation to define integers and doubles\. You can use [E notation](https://en.wikipedia.org/wiki/Scientific_notation#E_notation) to express numbers with scientific notation\.

  Examples: `1`, `2.0`, `.9`, `-23.1`, `7.89e3`, `3.4E-5`
+ <a name="string-literal-definition"></a>**Strings**

  Use the `'` \(quote\) and `"` \(double quote\) characters to define strings\. The quote type for the start and end must match\. To escape a quote that matches the one that you use to declare a string, include that quote character twice\. This is the only escape character in AWS IoT SiteWise strings\.

  Examples: `'active'`, `"inactive"`, `'{"temp": 52}'`, `"{""temp"": ""high""}"`