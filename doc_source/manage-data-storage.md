# Exporting data to Amazon S3<a name="manage-data-storage"></a>

AWS IoT SiteWise can export raw data and metadata to an Amazon S3 bucket in your account\. Raw data includes measurements \(equipment data\), metrics, and transforms\. AWS IoT SiteWise exports raw data to Amazon S3 once every six hours\. Metadata includes asset and asset hierarchy metadata\. AWS IoT SiteWise exports metadata to Amazon S3 when you change asset model definitions or asset definitions\.

After you export your data to an Amazon S3 bucket, you can use the following AWS services to create historical reports or analyze and query your data:
+ Run SQL queries on your data using [Amazon Athena](https://docs.aws.amazon.com/athena/latest/ug/)\.
+ Perform big data analysis using [Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html)\.
+ Search and analyze your data using [Amazon Elasticsearch Service](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/)\.

For more information about other AWS services that can interact with your data in Amazon S3, see the list under **Analytics** in the [AWS Management Console](https://console.aws.amazon.com/)\.

You can also use asset property notifications to export data from asset properties that you select to Amazon S3 in near\-real time\. For more information, see [Exporting data to Amazon S3 by using asset property notifications](export-to-s3.md)\.