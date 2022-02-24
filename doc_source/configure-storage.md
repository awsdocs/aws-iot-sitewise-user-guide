# Configuring storage settings<a name="configure-storage"></a>

You can configure storage settings to replicate data to the cold tier\. When you configure storage settings, you can also do the following\.
+ Set a retention period for how long your data is stored in the hot tier before it's deleted\. AWS IoT SiteWise will delete any data in the hot tier that's older than the retention period\. If you don't set a retention period, your data is stored indefinitely\. 
+ Enable AWS IoT SiteWise to create an AWS IoT Analytics data store to save AWS IoT SiteWise data\. To query your data, you can create datasets in AWS IoT Analytics\. For more information, see [Working with AWS IoT SiteWise data](https://docs.aws.amazon.com/iotanalytics/latest/userguide/dataset-itsw.html) in the *AWS IoT Analytics User Guide*\.

**Topics**
+ [Configure storage settings \(console\)](configure-storage-console.md)
+ [Configure storage settings \(AWS CLI\)](configure-storage-cli.md)