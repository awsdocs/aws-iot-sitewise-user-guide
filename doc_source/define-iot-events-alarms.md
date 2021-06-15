# Defining AWS IoT Events alarms<a name="define-iot-events-alarms"></a>

When you create an AWS IoT Events alarm, AWS IoT SiteWise sends asset property values to AWS IoT Events to evaluate the state of the alarm\. AWS IoT Events alarm definitions depend on an alarm model that you define in AWS IoT Events\. To define an AWS IoT Events alarm on an asset model, you define an alarm composite model that specifies the AWS IoT Events alarm model as its alarm source property\.

AWS IoT Events alarms depend on inputs such as alarm thresholds and alarm notification settings\. You define these inputs as attributes on the asset model\. You can then customize these inputs on each asset based on the model\. The AWS IoT SiteWise console can create these attributes for you\. If you define alarms with the AWS CLI or API, you must manually define these attributes on the asset model\.

You can also define other actions that happen when your alarm detects, such as custom alarm notification actions\. For example, you can configure an action that sends a push notification to an Amazon SNS topic\. For more information the actions that you can define, see [Working with other AWS services](https://docs.aws.amazon.com/iotevents/latest/developerguide/iotevents-other-aws-services.html) in the *AWS IoT Events Developer Guide*\.

When you update or delete an asset model, AWS IoT SiteWise can check if an alarm model in AWS IoT Events is monitoring an asset property associated with this asset model\. This prevents you from deleting an asset property that an AWS IoT Events alarm is currently using\. To enable this feature in AWS IoT SiteWise, you must have the `iotevents:ListInputRoutings` permission\. This permission allows AWS IoT SiteWise to make calls to the [ListInputRoutings](https://docs.aws.amazon.com/iotevents/latest/apireference/API_ListInputRoutings.html) API operation supported by AWS IoT Events\. For more information, see [\(Optional\) ListInputRoutings permission](alarms-iam-permissions.md#alarms-listInputRoutings-permissions)\.

**Note**  
The alarm notifications feature isn't available in the China \(Beijing\) Region\.

**Topics**
+ [Requirements for alarm notifications](#iot-events-alarm-notification-requirements)
+ [Defining an AWS IoT Events alarm \(console\)](define-iot-events-alarm-console.md)
+ [Defining an AWS IoT Events alarm \(CLI\)](define-iot-events-alarm-cli.md)

## Requirements for alarm notifications<a name="iot-events-alarm-notification-requirements"></a>

AWS IoT Events uses an AWS Lambda function in your AWS account to send alarm notifications\. You must create this Lambda function in the same AWS Region as your alarms to enable alarm notifications\. This Lambda function uses [Amazon Simple Notification Service \(Amazon SNS\)](https://docs.aws.amazon.com/sns/latest/dg/welcome.html) to send text notifications and [Amazon Simple Email Service \(Amazon SES\)](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/Welcome.html) to send email notifications\. When you create the AWS IoT Events alarm, you configure the protocols and settings that the alarm uses to send notifications\.

AWS IoT Events provides an AWS CloudFormation stack template that you can use to create this Lambda function in your account\. For more information, see [Alarm notification Lambda function](https://docs.aws.amazon.com/iotevents/latest/developerguide/lambda-support.html) in the *AWS IoT Events Developer Guide*\.