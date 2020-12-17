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

1. \(Optional\) In the **Notification settings** pane, you configure the notification settings for the alarm\. The alarm uses an AWS Lambda function in your AWS account to send alarm notification\. For more information, see [Requirements for alarm notifications](define-iot-events-alarms.md#iot-events-alarm-notification-requirements)\.

   In this pane, you configure this Lambda function, the message protocol, the message recipient, and the custom message that AWS IoT Events sends when this alarm detects\. You define the recipient and custom message in an attribute property, so you can later customize these values for each asset based on this model\. You can use an existing attribute or create an attribute for each setting\. If you create an attribute, you can define its default value for all assets based on this asset model\.
**Important**  <a name="alarm-notifications-sso-requirement"></a>
You can send alarm notifications to AWS Single Sign\-On users\. To use this feature, you must enable AWS SSO\. You can only enable AWS SSO in one AWS Region at a time\. This means that you can define alarm notifications only in the Region where you enable AWS SSO\. For more information, see [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the *AWS Single Sign\-On User Guide*\.

   In the **Notification settings** pane, do the following:

   1. For **Function name**, choose the Lambda function that sends alarm notifications\.

   1. For **Protocol**, choose from the following options:
      + **Text and email** – The alarm notifies AWS SSO users with an SMS message and an email\.
      + **Email** – The alarm notifies AWS SSO users with an email\.
      + **Text** – The alarm notifies AWS SSO users with an SMS message\.

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

1. Specify the **Default asset state** for this alarm\. You can enable or disable this alarm for all assets that you create from this asset model\. You can enable or disable this alarm for all assets that you create from this asset model in a later step\.

1. AWS IoT Events alarms require two service roles:

   1. A role that AWS IoT SiteWise assumes to send asset property values to AWS IoT Events\.

   1. A role that AWS IoT Events assumes to send alarm state values to AWS IoT SiteWise\.

   When you create an alarm, you can choose existing roles or create roles with the permissions that each service requires\. In the **Permissions** pane, do the following:

   1. For **AWS IoT SiteWise role**, use an existing role or create a role with the required permissions\. This role requires the `iotevents:BatchPutMessage` permission and a trust relationship that allows `iotsitewise.amazonaws.com` to assume the role\. For more information, see [Using service roles for alarms](alarm-service-role.md)\.

   1. For **AWS IoT Events role**, use an existing role or create a role with the required permissions\. This role requires the `iotsitewise:BatchPutAssetPropertyValue` permission and a trust relationship that allows `iotevents.amazonaws.com` to assume the role\. To send notifications, this role also requires the `lambda:InvokeFunction` and `sso-directory:DescribeUser` permissions\. For more information, see [Alarm service roles](https://docs.aws.amazon.com/iotevents/latest/developerguide/security-iam.html) in the *AWS IoT Events Developer Guide*\.

1. \(Optional\) In **Advanced configuration**, you can specify if the acknowledge flow is enabled\. For more information about the acknowledge flow, see [Alarm states](industrial-alarms.md#alarm-states)\.

1. Choose **Add alarm**\.

1. The AWS IoT SiteWise console makes multiple API requests to add the alarm to the asset model\. When you choose **Add alarm**, the console opens a dialog box that shows the progress of these API requests\. Stay on this page until each API requests succeeds or until an API request fails\. If a request fails, close the dialog box, fix the issue, and choose **Add alarm** to try again\.