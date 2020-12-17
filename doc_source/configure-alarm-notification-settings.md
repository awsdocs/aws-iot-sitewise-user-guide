# Configuring notification settings<a name="configure-alarm-notification-settings"></a>

You can use the AWS IoT SiteWise console or API to configure the alarm notification settings for an asset\.

**Topics**
+ [Configuring notification settings \(console\)](#configure-alarm-notification-settings-console)
+ [Configuring notification settings \(CLI\)](#configure-alarm-notification-settings-cli)

## Configuring notification settings \(console\)<a name="configure-alarm-notification-settings-console"></a>

You can use the AWS IoT SiteWise console to update the value of the attributes that specify the notification settings for an alarm\.

**To update an alarm's notification settings \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-assets"></a>In the navigation pane, choose **Assets**\.

1. Choose the asset to for which you want to update the alarm threshold value\.
**Tip**  <a name="sitewise-expand-asset-hierarchy"></a>
You can choose the arrow icon to expand an asset hierarchy to find your asset\.  

![\[AWS IoT SiteWise "Assets" page screenshot with an asset hierarchy highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-expand-asset-hierarchy-console.png)

1. Choose **Edit**\.

1. Find the attribute that the alarm uses for the notification setting that you want to change, and then enter its new value\.

1. Choose **Save**\.

## Configuring notification settings \(CLI\)<a name="configure-alarm-notification-settings-cli"></a>

You can use the AWS Command Line Interface \(AWS CLI\) to update the value of the attributes that specify the notification settings for an alarm\. For more information, see [Updating an attribute value \(CLI\)](update-attribute-values.md#update-attribute-value-cli)\.