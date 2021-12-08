# Processing and consuming data locally<a name="process-gateway-data-edge"></a>

You must configure your asset model for the edge before your can process your gateway data at the edge\. Your asset model edge configuration specifies where your assets properties are computed\. You can compute all properties at the edge, or you can configure your asset model properties separately\.

Asset model properties include metrics, transforms, and measurements:
+ Metrics are the asset's aggregated data over a specified period of time\. You can compute new metrics by using existing metric data\. AWS IoT SiteWise always sends your metrics to the AWS Cloud for long\-term storage\. AWS IoT SiteWise computes metrics on the AWS Cloud by default\. You can configure your asset model to compute your metrics at the edge\. AWS IoT SiteWise sends processed results to the AWS Cloud\.
+ Transforms are mathematical expressions that map an asset property's data points from one form to another\. Transforms can use metrics as input data and must be computed and stored at the same location as their inputs\. If you configure a metric input to compute at the edge, AWS IoT SiteWise also computes its associated transform at the edge\. 
+ Measurements are formatted as raw data that your device collects and sends to the AWS Cloud by default\. You can configure your asset model to store this data on your local device\.

For more information about asset properties, see [Defining data properties](asset-properties.md)\.

 After you create your asset model, you can then configure it for the edge\. For more information about configuring your asset model for the edge, see [Creating an asset model \(console\)](create-asset-models.md#create-asset-model-console)\. 

**Note**  
Asset models and dashboards are automatically synced between the AWS Cloud and your AWS IoT SiteWise gateway every 10 minutes\. You can also sync manually from the [local gateway application](manage-gateways-ggv2.md)\.

You can use the AWS IoT SiteWise REST APIs and the AWS Command Line Interface \(AWS CLI\) to query your gateway for data at the edge\. Before you query your gateway for data at the edge, you must meet the following prerequisites:
+ Your credentials must be set for the REST APIs\. For more information about setting credentials, see [Managing gateways](manage-gateways-ggv2.md)\.
+ The SDK endpoint must point to the IP address of your gateway\. You can find more information in the documentation for your SDK\. For example, see [Specifying Custom Endpoints](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/specifying-endpoints.html) in the *AWS SDK for Java 2\.x Developer Guide*\.
+ Your gateway certificate must be registered\. You can find more information about registering your gateway certificate in the documentation for your SDK\. For example, see the [Registering Certificate Bundles in Node\.js](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/node-registering-certs.html) in the *AWS SDK for Java 2\.x Developer Guide*\.

For more information about querying data with AWS IoT SiteWise, see [Querying asset property values and aggregates](query-industrial-data.md)\.