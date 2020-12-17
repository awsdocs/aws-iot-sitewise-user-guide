# Configuring alarms on assets<a name="configure-alarms"></a>


|  | 
| --- |
|  The alarms feature is in preview release for AWS IoT SiteWise, AWS IoT Events, and SiteWise Monitor, and is subject to change\. We recommend that you use this feature only with test data, and not in production environments\. While the alarms feature is in preview, you must download the alarms preview AWS SDK and AWS Command Line Interface \(AWS CLI\) to use the API operations for this feature\. These API operations aren't available in the public AWS SDK or AWS CLI\. For more information, see [Alarms preview AWS CLI and AWS SDKs](alarms-preview-sdk.md)\.  | 

After you define an AWS IoT Events alarm on an asset model, you can configure the alarm on each asset based on the asset model\. You can edit the threshold value and the notification settings for the alarm\. Each of these values is an attribute on the asset, so you can update the default value of the attribute to configure these values\.

**Note**  
You can configure these values for AWS IoT Events alarms, but not external alarms\.

**Topics**
+ [Configuring threshold values](configure-alarm-threshold-values.md)
+ [Configuring notification settings](configure-alarm-notification-settings.md)