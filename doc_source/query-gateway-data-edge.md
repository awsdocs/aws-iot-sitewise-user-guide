# Query gateway data at the edge<a name="query-gateway-data-edge"></a>

You can use the AWS IoT SiteWise REST APIs and the AWS Command Line Interface \(AWS CLI\) to query your gateway for data at the edge\. Before you query your gateway for data at the edge, you must meet the following prerequisites:
+ Credentials set to use with the REST APIs\. For more information about setting credentials, see [Monitor data at the edge](using-opshub.md)\.
+ The SDK endpoint must point to the IP address of your gateway\. You can find more information in the documentation for your SDK\. For an example, see the [JavaScript SDK documentation](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/specifying-endpoints.html)\.
+ Your gateway certificate must be registered\. You can find more information about registering your gateway certificate in the documentation for your SDK\. For an example, see the [JavaScript SDK documentation](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/node-registering-certs.html )\.

For more information about querying data with AWS IoT SiteWise, see [Querying asset property values and aggregates](query-industrial-data.md)\.