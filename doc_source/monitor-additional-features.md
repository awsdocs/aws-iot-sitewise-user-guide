# Enabling alarms for your SiteWise Monitor portals<a name="monitor-additional-features"></a>

You can enable the alarms feature supported by AWS IoT Events for your portals so that portal administrators can create, edit, and delete AWS IoT Events alarm models in your SiteWise Monitor portals\. Project owners can configure alarms\. Project viewers can view alarm details\. This section explains how you can use the AWS IoT SiteWise console to enable the alarms feature for your portals\.

**Important**  
You can't create external alarms in your portals\.
If you want to send alarm notifications, you must choose AWS SSO for the user authentication service\.
The alarm notifications feature isn't available in the China \(Beijing\) Region\.

When you configure and create a portal, you can enable alarms and alarm notifications in **Step 2 Additional features**\. Based on the user authentication service, choose one of the following options:

------
#### [ SSM ]

![\[Additional features page for enabling alarms for portals.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/portal-create-console-enable-alarms-sso.png)

**To enable alarms for a portal**

1. \(Optional\) Choose **Enable alarms**\.

   1. For **AWS IoT SiteWise access role**, use an existing role or create a role with the required permissions\. This role requires the `iotevents:BatchPutMessage` permission and a trust relationship that allows `iot.amazonaws.com` and `iotevents.amazonaws.com` to assume the role\.

1. \(Optional\) Choose **Enable alarm notifications**\.

   1. For **Sender**, choose the sender\.
**Important**  
You must verify the sender email address in Amazon SES\. For more information, see [Verifying email addresses in Amazon SES](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-addresses-and-domains.html), in the *Amazon Simple Email Service Developer Guide*\.

   1. For **AWS Lambda role**, use an existing role or create a role with the required permissions\. This role requires the `lambda:InvokeFunction` and `sso-directory:DescribeUser`permissions and a trust relationship that allows `iotevents.amazonaws.com` and `lambda.amazonaws.com` to assume the role\.

   1. For **AWS Lambda functions**, choose an existing Lambda function or create a function that manages alarm notifications\. For more information, see [Managing alarm notifications](https://docs.aws.amazon.com/iotevents/latest/developerguide/lambda-support.html) in the *AWS IoT Events Developer Guide*\.

------
#### [ IAM ]

![\[Additional features page for enabling alarms for portals.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/portal-create-console-enable-alarms-iam.png)

**To enable alarms for a portal**
+ \(Optional\) Choose **Enable alarms**\.

  1. For **AWS IoT SiteWise access role**, use an existing role or create a role with the required permissions\. This role requires the `iotevents:BatchPutMessage` permission and a trust relationship that allows `iot.amazonaws.com` and `iotevents.amazonaws.com` to assume the role\.

------

For more information about alarms in SiteWise Monitor, see [Monitoring with alarms](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/monitor-alarms.html) in the *AWS IoT SiteWise Application Guide*\.