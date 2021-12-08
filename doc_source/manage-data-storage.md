# Managing data storage<a name="manage-data-storage"></a>


****  

|  | 
| --- |
| The retention period configuration for the hot tier is in preview release for AWS IoT SiteWise and is subject to change\. We recommend that you use this tool only with test databases, and not in production environments\. | 

You can configure AWS IoT SiteWise to save your data in the following storage tiers\.

**Cold tier**  
A customer\-managed Amazon S3 bucket in your account\. AWS IoT SiteWise can export raw data and metadata to the Amazon S3 bucket\. Raw data includes measurements \(equipment data\) and metrics\. Metadata includes assets and asset hierarchy metadata\. For more information about how to configure storage settings to save your data in the cold tier, see [Configuring the cold tier](configure-cold-tier.md)\.  
After your data is sent to the cold tier, you can use the following AWS services to create historical reports or analyze and query your data:  
+ Run SQL queries on your data by using [Amazon Athena](https://docs.aws.amazon.com/athena/latest/ug/)\.
+ Perform big data analysis by using [Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html)\.
+ Search and analyze your data by using [Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/)\.
For more information about other AWS services that can interact with your data in Amazon S3, see the list under **Analytics** in the [AWS Management Console](https://console.aws.amazon.com/)\.

**Hot tier**  
A service\-managed database\. By default, AWS IoT SiteWise saves your data in the hot tier\. You can define a retention period to control how long your data is kept in the hot tier\. For more information about how to define a retention period for the hot tier, see [Configuring a retention period for the hot tier](configure-hot-tier-retention.md)\.

**Topics**
+ [Configuring storage settings](configure-storage.md)
+ [File paths and schemas of data saved in the cold tier](file-path-and-schema.md)