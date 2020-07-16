# Asset properties<a name="asset-properties"></a>

Asset properties are the structures within each asset that contain asset data\. Asset properties can be any of the following types:
+ **Attributes** – An asset's generally static properties, such as device manufacturer or geographic region\. For more information, see [Attributes](attributes.md)\.
+ **Measurements** – An asset's raw device's sensor data streams, such as timestamped rotation speed values or timestamped temperature values in Celsius\. A measurement is defined by a data stream alias\. For more information, see [Measurements](measurements.md)\.
+ **Transforms** – An asset's transformed time\-series values, such as timestamped temperature values in Fahrenheit\. A transform is defined by an expression and the variables to consume with that expression\. For more information, see [Transforms](transforms.md)\.
+ **Metrics** – An asset's data aggregated over a specified time interval, such as the hourly average temperature\. A metric is defined by a time interval, an expression, and the variables to consume with that expression\. Metric expressions can access associated assets' metric properties\. For more information, see [Metrics](metrics.md)\.

For an example of how to use measurements, transforms, and metrics to calculate Overall Equipment Effectiveness \(OEE\), see [Calculating OEE in AWS IoT SiteWise](calculate-oee.md)\.

**Topics**
+ [Attributes](attributes.md)
+ [Measurements](measurements.md)
+ [Transforms](transforms.md)
+ [Metrics](metrics.md)
+ [Using formula expressions](formula-expressions.md)