# Configuring threshold values<a name="configure-alarm-threshold-values"></a>

You can use the AWS IoT SiteWise console or API to configure the threshold value of an alarm for an asset\.

**Topics**
+ [Configuring a threshold value \(console\)](#configure-alarm-threshold-value-console)
+ [Configuring a threshold value \(CLI\)](#configure-alarm-threshold-value-cli)

## Configuring a threshold value \(console\)<a name="configure-alarm-threshold-value-console"></a>

You can use the AWS IoT SiteWise console to update the value of the attribute that specifies the threshold value of an alarm\.

**To update an alarm's threshold value \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-assets"></a>In the navigation pane, choose **Assets**\.

1. Choose the asset for which you want to update an alarm threshold value\.
**Tip**  <a name="sitewise-expand-asset-hierarchy"></a>
You can choose the arrow icon to expand an asset hierarchy to find your asset\.  

![\[AWS IoT SiteWise "Assets" page screenshot with an asset hierarchy highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-expand-asset-hierarchy-console.png)

1. Choose **Edit**\.

1. Find the attribute that the alarm uses for its threshold value, and then enter its new value\.

1. Choose **Save**\.

## Configuring a threshold value \(CLI\)<a name="configure-alarm-threshold-value-cli"></a>

You can use the AWS Command Line Interface \(AWS CLI\) to update the value of the attribute that specifies the threshold value of an alarm\. For more information, see [Updating an attribute value \(CLI\)](update-attribute-values.md#update-attribute-value-cli)\.