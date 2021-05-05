# Variables<a name="expression-variables"></a>

Variables represent AWS IoT SiteWise asset properties in formula expressions\. Use variables to input values from other asset properties in your expressions, so that you can process data from constant properties \([attributes](attributes.md)\), raw data streams \([measurements](measurements.md)\), and other formula properties\.

Variables can represent asset properties from the same asset model or from associated child asset models\. Only metric formulas can input variables from child asset models\.

You identify variables by different names in the console and the API\.
+ **AWS IoT SiteWise console** – Use asset property names as variables in your expressions\.
+ **AWS IoT SiteWise API \(AWS CLI, AWS SDKs\)** – Define variables with the [ExpressionVariable](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ExpressionVariable.html) structure, which requires a variable name and a reference to an asset property\. The variable name can contain lowercase letters, numbers, and underscores\. Then, use variable names to reference asset properties in your expressions\.

Variable names are case sensitive\.

For more information, see [Defining transforms](transforms.md) and [Defining metrics](metrics.md)\.