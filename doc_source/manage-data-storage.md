# Managing data storage<a name="manage-data-storage"></a>

You can configure AWS IoT SiteWise to save your data in the following storage tiers\.

**Hot tier**  
A service\-managed database\. By default, your data is stored only in the hot tier of AWS IoT SiteWise\. You can set a retention period for how long your data is stored in the hot tier before it's deleted\. AWS IoT SiteWise will delete any data in the hot tier that's older than the retention period\. If you don't set a retention period, your data is stored indefinitely\. You can use the hot tier to store recent data that requires frequent access and low latency\.

**Cold tier**  
A customer\-managed Amazon S3 bucket\. AWS IoT SiteWise stores your data in an Amazon S3 bucket in your account by replicating time series, including measurements, metrics, transforms and aggregates, and also asset and asset model definitions\. You can use the cold tier to store historical data that requires infrequent access and high latency\.  
After your data is sent to the cold tier, you can use the following AWS services to create historical reports or analyze and query your data:  
+ Run SQL queries on your data by using [Amazon Athena](https://docs.aws.amazon.com/athena/latest/ug/)\.
+ Perform big data analysis by using [Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html)\.
+ Search and analyze your data by using [Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/)\.
For more information about other AWS services that can interact with your data in Amazon S3, see the list under **Analytics** in the [AWS Management Console](https://console.aws.amazon.com/)\.

**Topics**
+ [Configuring storage settings](configure-storage.md)
+ [Troubleshoot](troubleshoot-storage-configuration.md)
+ [File paths and schemas of data saved in the cold tier](file-path-and-schema.md)