# Defining AWS IoT Events alarms<a name="define-iot-events-alarms"></a>


|  | 
| --- |
|  The alarms feature is in preview release for AWS IoT SiteWise, AWS IoT Events, and SiteWise Monitor, and is subject to change\. We recommend that you use this feature only with test data, and not in production environments\. While the alarms feature is in preview, you must download the alarms preview AWS SDK and AWS Command Line Interface \(AWS CLI\) to use the API operations for this feature\. These API operations aren't available in the public AWS SDK or AWS CLI\. For more information, see [Alarms preview AWS CLI and AWS SDKs](alarms-preview-sdk.md)\.  | 

When you create an AWS IoT Events alarm, AWS IoT SiteWise sends asset property values to AWS IoT Events to evaluate the state of the alarm\. AWS IoT Events alarm definitions depend on an alarm model that you define in AWS IoT Events\. To define an AWS IoT Events alarm on an asset model, you define an alarm composite model that specifies the AWS IoT Events alarm model as its alarm source property\.

AWS IoT Events alarms depend on inputs such as alarm thresholds and alarm notification settings\. You define these inputs as attributes on the asset model\. You can then customize these inputs on each asset based on the model\. The AWS IoT SiteWise console can create these attributes for you\. If you define alarms with the AWS CLI or API, you must manually define these attributes on the asset model\.

After you define an alarm and create an AWS IoT Events alarm model, you must create a *subscription* that enables AWS IoT SiteWise to send data to AWS IoT Events\. Subscriptions specify which data AWS IoT SiteWise sends to other AWS services\. You enable subscriptions on asset properties at the scope of assets or asset models\. When you enable a subscription on a property for an asset model, AWS IoT SiteWise sends that property's data for all assets based on that asset model\. When you enable a subscription on a property for an asset, AWS IoT SiteWise sends that property's data for only that asset\. Subscriptions on assets override subscriptions on asset models\.

**Important**  
If you update an alarm model in AWS IoT Events after you create an alarm, you must set its values that use attributes from the AWS IoT SiteWise asset model\. Otherwise, the alarm won't monitor data\. You can update the subscription for each attribute to send the current values to the alarm model\. For more information, see [Step 3: Enabling data flow between AWS IoT SiteWise and AWS IoT Events](define-iot-events-alarm-cli.md#define-iot-events-alarm-data-flow-cli)\.

**Topics**
+ [Requirements for alarm notifications](#iot-events-alarm-notification-requirements)
+ [Defining an AWS IoT Events alarm \(console\)](define-iot-events-alarm-console.md)
+ [Defining an AWS IoT Events alarm \(CLI\)](define-iot-events-alarm-cli.md)

## Requirements for alarm notifications<a name="iot-events-alarm-notification-requirements"></a>

AWS IoT Events uses an AWS Lambda function in your AWS account to send alarm notifications\. You must create this Lambda function in the same AWS Region as your alarms to enable alarm notifications\. This Lambda function uses [Amazon Simple Notification Service \(Amazon SNS\)](https://docs.aws.amazon.com/sns/latest/dg/welcome.html) to send text notifications and [Amazon Simple Email Service \(Amazon SES\)](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/Welcome.html) to send email notifications\. When you create the AWS IoT Events alarm, you configure the protocols and settings that the alarm uses to send notifications\.

AWS IoT Events provides an AWS CloudFormation stack template that you can use to create this Lambda function in your account\. For more information, see [Alarm notification Lambda function](https://docs.aws.amazon.com/iotevents/latest/developerguide/lambda-support.html) in the *AWS IoT Events Developer Guide*\.

**Note**  
You can define other actions that happen when your alarm detects, such as custom alarm notification actions\. For example, you can configure an action that sends a push notification to an Amazon SNS topic\. For more information the actions that you can define, see [Working with other AWS services](https://docs.aws.amazon.com/iotevents/latest/developerguide/iotevents-other-aws-services.html) in the *AWS IoT Events Developer Guide*\.