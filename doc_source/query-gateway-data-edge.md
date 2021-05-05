# Query gateway data at the edge<a name="query-gateway-data-edge"></a>


|  | 
| --- |
|  Processing at the edge is in preview release for AWS IoT SiteWise and is subject to change\. We recommend that you use this feature only with test data, and not in production environments\. While the edge processing feature is in preview, you must download the edge processing preview AWS SDK and AWS CLI to use the API operations for this feature\. These API operations aren't available in the public AWS SDK or AWS CLI\. For more information, see [Edge processing preview AWS CLI and AWS SDKs](edge-preview-sdks.md)\.  | 

You can use the AWS IoT SiteWise REST APIs and the AWS Command Line Interface \(AWS CLI\) to query your gateway for data at the edge\. Before you query your gateway for data at the edge, you must meet the following prerequisites:
+ Your credentials must be set for the REST APIs\. For more information about setting credentials, see [Monitor data at the edge](using-opshub.md)\.
+ The SDK endpoint must point to the IP address of your gateway\. You can find more information in the documentation for your SDK\. For example, see [Specifying Custom Endpoints](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/specifying-endpoints.html) in the *AWS SDK for Java 2\.x Developer Guide*\.
+ Your gateway certificate must be registered\. You can find more information about registering your gateway certificate in the documentation for your SDK\. For example, see the [Registering Certificate Bundles in Node\.js](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/node-registering-certs.html) in the *AWS SDK for Java 2\.x Developer Guide*\.

For more information about querying data with AWS IoT SiteWise, see [Querying asset property values and aggregates](query-industrial-data.md)\.