# Mapping external alarm state streams<a name="connect-alarm-data-streams"></a>

You can define property aliases to map your data streams to your alarm state properties\. This helps you easily identify an alarm state property when you ingest or retrieve data\. For more information about property aliases, see [Mapping industrial data streams to asset properties](connect-data-streams.md)\.

**Topics**
+ [Mapping external alarm state streams \(console\)](#connect-alarm-data-stream-console)
+ [Mapping external alarm state streams \(CLI\)](#connect-alarm-data-stream-cli)

## Mapping external alarm state streams \(console\)<a name="connect-alarm-data-stream-console"></a>

You can use the AWS IoT SiteWise console to set an alias for an alarm state property\.

**To set a property alias for an alarm state property \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-assets"></a>In the navigation pane, choose **Assets**\.

1. Choose the asset for which you want to set a property alias\.
**Tip**  <a name="sitewise-expand-asset-hierarchy"></a>
You can choose the arrow icon to expand an asset hierarchy to find your asset\.  

![\[AWS IoT SiteWise "Assets" page screenshot with an asset hierarchy highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-expand-asset-hierarchy-console.png)

1. Choose **Alarms**\.

1. Select the external alarm for which you want to set a property alias\.

1. Choose **View**\.

1. In the **Alarm state details** pane, choose **Edit**\.

1. Enter the property alias\.

1. Choose **Update**\.

## Mapping external alarm state streams \(CLI\)<a name="connect-alarm-data-stream-cli"></a>

You can use the AWS Command Line Interface \(AWS CLI\) to set an alias for an alarm state property\.

You must know your asset's `assetId` and property's `propertyId` to complete this procedure\. If you created an asset but don't know its `assetId`, use the [ListAssets](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListAssets.html) operation to view all of your assets for a specific model\. Then, use the [DescribeAsset](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeAsset.html) operation to view your asset's properties including property IDs\.

**Note**  
The [DescribeAsset](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeAsset.html) response includes the list of composite asset models for the asset\. Each alarm is a composite model\. To find the `propertyId`, find the composite model for the alarm, and then find the `AWS/ALARM_STATE` property in that composite model\.

For more information about how to set the property alias, see [Setting a property alias \(CLI\)](connect-data-streams.md#set-property-alias-cli)\.