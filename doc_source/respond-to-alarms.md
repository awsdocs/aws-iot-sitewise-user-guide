# Responding to alarms<a name="respond-to-alarms"></a>


|  | 
| --- |
|  The alarms feature is in preview release for AWS IoT SiteWise, AWS IoT Events, and SiteWise Monitor, and is subject to change\. We recommend that you use this feature only with test data, and not in production environments\. While the alarms feature is in preview, you must download the alarms preview AWS SDK and AWS Command Line Interface \(AWS CLI\) to use the API operations for this feature\. These API operations aren't available in the public AWS SDK or AWS CLI\. For more information, see [Alarms preview AWS CLI and AWS SDKs](alarms-preview-sdk.md)\.  | 

When an AWS IoT Events alarm changes state, you can do the following to respond to the alarm:
+ Acknowledge an alarm to indicate that you are handling the issue\.
+ Snooze an alarm to disable it temporarily\.
+ Disable an alarm to disable it permanently until you enable it again\.
+ Enable a disabled alarm to detect alarm state\.
+ Reset an alarm to clear its state and latest value\.

You can use the AWS IoT SiteWise console or the AWS IoT Events API to respond to an alarm\.

**Note**  
You can respond to AWS IoT Events alarms, but not external alarms\.

**Topics**
+ [Responding to an alarm \(console\)](#respond-to-alarm-console)
+ [Responding to an alarm \(API\)](#respond-to-alarm-cli)

## Responding to an alarm \(console\)<a name="respond-to-alarm-console"></a>

You can use the AWS IoT SiteWise console to acknowledge, snooze, disable, or enable an alarm\.

**Topics**
+ [Acknowledge an alarm \(console\)](#acknowledge-alarm-console)
+ [Snooze an alarm \(console\)](#snooze-alarm-console)
+ [Disable an alarm \(console\)](#disable-alarm-console)
+ [Enable an alarm \(console\)](#enable-alarm-console)
+ [Reset an alarm \(console\)](#reset-alarm-console)

### Acknowledge an alarm \(console\)<a name="acknowledge-alarm-console"></a>

You can acknowledge an alarm to indicate that you're handling the issue\.

**Note**  
You must enable the acknowledge flow on the alarm so that you can acknowledge the alarm\. This option is enabled by default if you define the alarm from the AWS IoT SiteWise console\.

**To acknowledge an alarm \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-assets"></a>In the navigation pane, choose **Assets**\.

1. Choose the asset to for which you want to acknowledge an alarm\.
**Tip**  <a name="sitewise-expand-asset-hierarchy"></a>
You can choose the arrow icon to expand an asset hierarchy to find your asset\.  

![\[AWS IoT SiteWise "Assets" page screenshot with an asset hierarchy highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-expand-asset-hierarchy-console.png)

1. Choose the **Alarms** tab\.

1. Select the alarm to acknowledge, and then choose **Actions** to open the response action menu\.

1. Choose **Acknowledge**\. The alarm's state changes to **Acknowledged**\.

### Snooze an alarm \(console\)<a name="snooze-alarm-console"></a>

You can snooze an alarm to disable it temporarily\. Specify the duration for which to snooze the alarm\.

**To snooze an alarm \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-assets"></a>In the navigation pane, choose **Assets**\.

1. Choose the asset to for which you want to snooze an alarm\.
**Tip**  <a name="sitewise-expand-asset-hierarchy"></a>
You can choose the arrow icon to expand an asset hierarchy to find your asset\.  

![\[AWS IoT SiteWise "Assets" page screenshot with an asset hierarchy highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-expand-asset-hierarchy-console.png)

1. Choose the **Alarms** tab\.

1. Select the alarm to snooze, and then choose **Actions** to open the response action menu\.

1. Choose **Snooze**\. A model opens where you specify the duration to snooze\.

1. Choose the **Snooze length** or enter a **Custom snooze length**\.

1. Choose **Save**\. The alarm's state changes to **Snoozed**\.

### Disable an alarm \(console\)<a name="disable-alarm-console"></a>

You can disable an alarm so that it doesn't detect anymore\. After you disable the alarm, you must enable it again if you want the alarm to detect\.

**To disable an alarm \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-assets"></a>In the navigation pane, choose **Assets**\.

1. Choose the asset to for which you want to disable an alarm\.
**Tip**  <a name="sitewise-expand-asset-hierarchy"></a>
You can choose the arrow icon to expand an asset hierarchy to find your asset\.  

![\[AWS IoT SiteWise "Assets" page screenshot with an asset hierarchy highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-expand-asset-hierarchy-console.png)

1. Choose the **Alarms** tab\.

1. Select the alarm to disable, and then choose **Actions** to open the response action menu\.

1. Choose **Disable**\. The alarm's state changes to **Disabled**\.

### Enable an alarm \(console\)<a name="enable-alarm-console"></a>

You can enable an alarm to detect again after you disable or snooze it\.

**To enable an alarm \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-assets"></a>In the navigation pane, choose **Assets**\.

1. Choose the asset to for which you want to enable an alarm\.
**Tip**  <a name="sitewise-expand-asset-hierarchy"></a>
You can choose the arrow icon to expand an asset hierarchy to find your asset\.  

![\[AWS IoT SiteWise "Assets" page screenshot with an asset hierarchy highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-expand-asset-hierarchy-console.png)

1. Choose the **Alarms** tab\.

1. Select the alarm to enable, and then choose **Actions** to open the response action menu\.

1. Choose **Enable**\. The alarm's state changes to **Normal**\.

### Reset an alarm \(console\)<a name="reset-alarm-console"></a>

You can reset an alarm to clear its state and latest value\.

**To reset an alarm \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-assets"></a>In the navigation pane, choose **Assets**\.

1. Choose the asset to for which you want to reset an alarm\.
**Tip**  <a name="sitewise-expand-asset-hierarchy"></a>
You can choose the arrow icon to expand an asset hierarchy to find your asset\.  

![\[AWS IoT SiteWise "Assets" page screenshot with an asset hierarchy highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-expand-asset-hierarchy-console.png)

1. Choose the **Alarms** tab\.

1. Select the alarm to enable, and then choose **Actions** to open the response action menu\.

1. Choose **Reset**\. The alarm's state changes to **Normal**\.

## Responding to an alarm \(API\)<a name="respond-to-alarm-cli"></a>

You can use the AWS IoT Events API to acknowledge, snooze, disable, enable, or reset an alarm\. For more information, see the following operations in the *AWS IoT Events API Reference*:
+ [BatchAcknowledgeAlarm](https://docs.aws.amazon.com/iotevents/latest/apireference/API_iotevents-data_BatchAcknowledgeAlarm.html)
+ [BatchSnoozeAlarm](https://docs.aws.amazon.com/iotevents/latest/apireference/API_iotevents-data_BatchSnoozeAlarm.html)
+ [BatchDisableAlarm](https://docs.aws.amazon.com/iotevents/latest/apireference/API_iotevents-data_BatchDisableAlarm.html)
+ [BatchEnableAlarm](https://docs.aws.amazon.com/iotevents/latest/apireference/API_iotevents-data_BatchEnableAlarm.html)
+ [BatchResetAlarm](https://docs.aws.amazon.com/iotevents/latest/apireference/API_iotevents-data_BatchResetAlarm.html)

For more information, see [Responding to alarms](https://docs.aws.amazon.com/iotevents/latest/developerguide/respond-to-alarms.html) in the *AWS IoT Events Developer Guide*\.