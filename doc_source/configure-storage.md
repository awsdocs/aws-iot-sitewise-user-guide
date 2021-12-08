# Configuring storage settings<a name="configure-storage"></a>


****  

|  | 
| --- |
| The retention period configuration for the hot tier is in preview release for AWS IoT SiteWise and is subject to change\. We recommend that you use this tool only with test databases, and not in production environments\. | 

You can configure storage settings to send data to the cold tier\. When you use the AWS IoT SiteWise console to configure storage settings, you can enable AWS IoT SiteWise to create an AWS IoT Analytics data store to save AWS IoT SiteWise data\. To query your data, you can create datasets in AWS IoT Analytics\.

You can also use the [PutStorageConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_RetentionPeriod.html) API to define a retention period for the hot storage\.

**Topics**
+ [Configuring the cold tier](configure-cold-tier.md)
+ [Configuring a retention period for the hot tier](configure-hot-tier-retention.md)
+ [Troubleshoot](troubleshoot-storage-configuration.md)