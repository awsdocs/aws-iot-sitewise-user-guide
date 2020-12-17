# Edge processing preview AWS CLI and AWS SDKs<a name="edge-preview-sdks"></a>

The edge processing feature is in preview, so its API operations aren't included in the AWS Command Line Interface or AWS SDKs\. You can download the AWS CLI and SDK resources from the following links to interact with the edge processing feature in your scripts and applications\.
+ [AWS IoT SiteWise edge preview AWS SDK for Java](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWiseEdgePreviewJavaSDK.zip)
+ [AWS IoT SiteWise edge preview AWS SDK for Python \(Boto3\)](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWiseEdgePreviewPythonSDK.zip)
+ [AWS IoT SiteWise edge preview AWS SDK for JavaScript in Node\.js](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWiseEdgePreviewNodeSDK.zip)
+ [AWS IoT SiteWise edge preview AWS SDK for Go](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWiseEdgePreviewGoSDK.zip)

## Configuring the AWS CLI<a name="configure-swe-cli"></a>

You must complete this step to enable AWS IoT SiteWise edge commands in the AWS CLI\.

From a command prompt, run `aws --version` to determine if the AWS CLI is installed\. If you don't have it installed, follow the instructions to install the [AWS CLI](https://aws.amazon.com/cli/)\.

**To enable the edge feature APIs in the AWS CLI**

1. Download the AWS IoT SiteWise [service\-2\-edge\-preview\.json](https://aws-iot-sitewise.s3.amazonaws.com/cli/service-2-edge-preview.json) file\.

1. Navigate to the directory where you downloaded the `service-2-edge-preview.json` file\.

1. From a command prompt, run the following command\.

   ```
   aws configure add-model --service-name iotsitewise-edge --service-model file://service-2-edge-preview.json
   ```

The `aws iotsitewise-edge` AWS CLI commands are now available\.