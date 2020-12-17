# Alarms preview AWS CLI and AWS SDKs<a name="alarms-preview-sdk"></a>


|  | 
| --- |
|  The alarms feature is in preview release for AWS IoT SiteWise, AWS IoT Events, and SiteWise Monitor, and is subject to change\. We recommend that you use this feature only with test data, and not in production environments\. While the alarms feature is in preview, you must download the alarms preview AWS SDK and AWS Command Line Interface \(AWS CLI\) to use the API operations for this feature\. These API operations aren't available in the public AWS SDK or AWS CLI\. For more information, see [Alarms preview AWS CLI and AWS SDKs](#alarms-preview-sdk)\.  | 

Because the alarms feature is in preview, you must download the AWS CLI and SDK resources from the following links to use the feature in your scripts and applications\. The preview AWS CLI and AWS SDKs include the subscription API operations that you use to enable data flow from AWS IoT SiteWise to AWS IoT Events\.
+ [AWS IoT SiteWise alarms preview AWS SDK for Java](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWiseAlarmsPreviewJavaSDK.zip)
+ [AWS IoT SiteWise alarms preview AWS SDK for Python \(Boto3\)](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWiseAlarmsPreviewPythonSDK.zip)
+ [AWS IoT SiteWise alarms preview AWS SDK for JavaScript in Node\.js](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWiseAlarmsPreviewNodeSDK.zip)
+ [AWS IoT SiteWise alarms preview AWS SDK for Go](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWiseAlarmsPreviewGoSDK.zip)

## Configuring the AWS CLI<a name="configure-alarms-cli"></a>

You must complete this step to enable AWS IoT SiteWise alarms commands in the AWS CLI\.

From a command prompt, run `aws --version` to determine if the AWS CLI is installed\. If you don't have it installed, follow the instructions to install the [AWS CLI](https://aws.amazon.com/cli/)\.

**To enable the alarms feature APIs in the AWS CLI**

1. Download the AWS IoT SiteWise [service\-2\-alarms\-preview\.json](https://aws-iot-sitewise.s3.amazonaws.com/cli/service-2-alarms-preview.json) file\.

1. Navigate to the directory where you downloaded the `service-2-alarms-preview.json` file\.

1. From a command prompt, run the following command\.

   ```
   aws configure add-model --service-name iotsitewise-alarms --service-model file://service-2-alarms-preview.json
   ```

The `aws iotsitewise-alarms` AWS CLI commands are now available\.