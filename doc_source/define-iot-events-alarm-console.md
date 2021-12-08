# Defining an AWS IoT Events alarm \(console\)<a name="define-iot-events-alarm-console"></a>

You can use the AWS IoT SiteWise console to define an AWS IoT Events alarm on an existing asset model\. To define an AWS IoT Events alarm on a new asset model, create the asset model, and then complete these steps\. For more information, see [Creating asset models](create-asset-models.md)\.

**Important**  
Each alarm requires an attribute that specifies the threshold value to compare against for the alarm\. You must define the threshold value attribute on the asset model before you can define an alarm\.  
Consider an example where you want to define an alarm that detects when a wind turbine exceeds its maximum wind speed rating of 50 mph\. Before you define the alarm, you must define an attribute \(**Maximum wind speed**\) with a default value of `50`\.

**To define an AWS IoT Events alarm on an asset model**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-models"></a>In the navigation pane, choose **Models**\.

1. Choose the asset model for which to define an alarm\.

1. Choose the **Alarm definitions** tab\.

1. Choose **Add alarm**\.

1. In **Alarm type options**, choose **AWS IoT Events alarm**\.

1. Enter a name for your alarm\.

1. \(Optional\) Enter a description for your alarm\.

1. In the **Threshold definitions** pane, you define when the alarm detects and the severity of the alarm\. Do the following:

   1. Select the **Property** on which the alarm detects\. Each time this property receives a new value, AWS IoT SiteWise sends the value to AWS IoT Events to evaluate the state of the alarm\.

   1. Select the **Operator** to use to compare the property with the threshold value\. Choose from the following options:
      + **< less than**
      + **<= less than or equal**
      + **== equal**
      + **\!= not equal**
      + **>= greater than or equal**
      + **> greater than**

   1. Select the attribute property to use as the threshold **Value**\. AWS IoT Events compares the value of the property with the value of this attribute\.

   1. Enter the **Severity** of the alarm\. Use a number that your team understands to reflect the severity of this alarm\.

1. \(Optional\) In the **Notification settings** pane, you can configure the notification settings for the alarm\. The alarm uses an AWS Lambda function in your AWS account to manage alarm notifications\. For more information, see [Requirements for alarm notifications](define-iot-events-alarms.md#iot-events-alarm-notification-requirements)\.

   In this pane, you configure this Lambda function, the message protocol, the message recipient, and the custom message that AWS IoT Events sends when this alarm is invoked\. You define the recipient and custom message in an attribute property, so you can later customize these values for each asset based on this model\. You can use an existing attribute or create an attribute for each setting\. If you create an attribute, you can define its default value for all assets based on this asset model\.

   In the **Notification settings** pane, do the following:

   1. Choose **Enabled**\.
**Note**  
If you choose **Disabled**, you and your team won't receive any alarm notifications\.

   1. For **Recipient**, choose the recipient\.
**Important**  <a name="alarm-notifications-sso-requirement"></a>
You can send alarm notifications to AWS Single Sign\-On users\. To use this feature, you must enable AWS SSO\. You can only enable AWS SSO in one AWS Region at a time\. This means that you can define alarm notifications only in the Region where you enable AWS SSO\. For more information, see [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the *AWS Single Sign\-On User Guide*\.

   1. For **Protocol**, choose from the following options:
      + **Email & text** – The alarm notifies AWS SSO users with an SMS message and an email message\.
      + **Email** – The alarm notifies AWS SSO users with an email message\.
      + **Text** – The alarm notifies AWS SSO users with an SMS message\.

   1. For **Sender**, choose the sender\.
**Important**  
You must verify the sender email address in Amazon Simple Email Service \(Amazon SES\)\. For more information, see [Verifying email addresses in Amazon SES](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-addresses-and-domains.html), in the *Amazon Simple Email Service Developer Guide*\.

1. Specify the **Default asset state** for this alarm\. You can enable or disable this alarm for all assets that you create from this asset model in a later step\.

1. In the **Advanced settings** pane, you can configure the permissions, the additional notification settings, the alarm state actions, the alarm model in SiteWise Monitor, and the acknowledge flow\.
**Note**  
AWS IoT Events alarms require the following service roles:  
A role that AWS IoT Events assumes to send alarm state values to AWS IoT SiteWise\.
A role that AWS IoT Events assumes to send data to Lambda\. You only need this role if your alarm sends notifications\.

   In the **Permissions** pane, do the following:

   1. For **AWS IoT Events role**, use an existing role or create a role with the required permissions\. This role requires the `iotsitewise:BatchPutAssetPropertyValue` permission and a trust relationship that allows iotevents\.amazonaws\.com to assume the role\.

   1. For the **AWS IoT Events Lambda role**, use an existing role or create a role with the required permissions\. This role requires the `lambda:InvokeFunction` and `sso-directory:DescribeUser` permissions and a trust relationship that allows `iotevents.amazonaws.com` to assume the role\.

1. \(Optional\) In the **Additional notification settings** pane, do the following:

   1. For **Recipient attribute**, you define an attribute whose value specifies the recipient of the notification\. You can choose AWS SSO users as recipients\.

      You can create an attribute or use an existing attribute on the asset model\.<a name="sitewise-alarms-notification-attributes-options"></a>
      + If you choose to create an attribute, specify the **Attribute name** and **Default value** for the attribute\.
      + If you choose to use an existing attribute, choose the attribute in **Attribute name**\. The alarm uses the default value of the attribute that you choose\.

      You can override the default value on each asset that you create from this asset model\.

   1. For **Custom message attribute**, you define an attribute whose value specifies the custom message to send in addition to the default state change message\. For example, you can specify a message that helps your team understand how to address this alarm\.

      You can choose to create an attribute or use an existing attribute on the asset model\.<a name="sitewise-alarms-notification-attributes-options"></a>
      + If you choose to create an attribute, specify the **Attribute name** and **Default value** for the attribute\.
      + If you choose to use an existing attribute, choose the attribute in **Attribute name**\. The alarm uses the default value of the attribute that you choose\.

      You can override the default value on each asset that you create from this asset model\.

   1. For **Function name**, choose an existing Lambda function or create a function that manages alarm notifications\. For more information, see [Managing alarm notifications](https://docs.aws.amazon.com/iotevents/latest/developerguide/lambda-support.html) in the *AWS IoT Events Developer Guide*\.

1. \(Optional\) In the **Set state action** pane, do the following:

   1. Choose **Edit action**\.

   1. On the **Add alarm state actions** page, add actions\. You can add up to 10 actions\.

   AWS IoT Events can perform actions when the alarm is active\. You can define built\-in actions to use a timer or set a variable, or send data to other AWS resources\. For more information, see [Supported actions](https://docs.aws.amazon.com/iotevents/latest/developerguide/iotevents-supported-actions.html) in the *AWS IoT Events Developer Guide*\.

1. \(Optional\) In the **Manage alarm model in SiteWise Monitor** pane, choose **Enabled** or **Disabled**\.

   Use this option so that you can update the alarm model in SiteWise Monitorss\. This option is enabled by default\.

1. In **Acknowledge flow**, you can specify if the acknowledge flow is enabled\. For more information about the acknowledge flow, see [Alarm states](industrial-alarms.md#alarm-states)\.

1. Choose **Add alarm**\.
**Note**  
The AWS IoT SiteWise console makes multiple API requests to add the alarm to the asset model\. When you choose **Add alarm**, the console opens a dialog box that shows the progress of these API requests\. Stay on this page until each API requests succeeds or until an API request fails\. If a request fails, close the dialog box, fix the issue, and choose **Add alarm** to try again\.