# AWS IoT SiteWise and interface VPC endpoints \(AWS PrivateLink\)<a name="vpc-interface-endpoints"></a>


|  | 
| --- |
|  The interface VPC endpoint for the control plane API operations is in preview release for AWS IoT SiteWise and is subject to change\. We recommend that you use this endpoint only with test data, and not in production environments\. While the interface VPC endpoint for the control plane API operations is in preview, you must download the preview AWS SDK and AWS Command Line Interface \(AWS CLI\) to access AWS IoT SiteWise through the endpoint\. For more information, see [Interface VPC endpoints preview AWS CLI and AWS SDKs](#private-link-preview-sdk)\.  | 

You can establish a private connection between your virtual private cloud \(VPC\) and AWS IoT SiteWise by creating an *interface VPC endpoint*\. Interface endpoints are powered by [AWS PrivateLink](http://aws.amazon.com/privatelink), a technology that you can use to privately access AWS IoT SiteWise API operations without an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection\. Instances in your VPC don't need public IP addresses to communicate with AWS IoT SiteWise API operations\. Traffic between your VPC and AWS IoT SiteWise doesn't leave the AWS network\.

Each interface endpoint is represented by one or more [elastic network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) in your subnets\. 

For more information, see [Interface VPC endpoints \(AWS PrivateLink\)](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) in the *Amazon VPC User Guide*\.

## Considerations for AWS IoT SiteWise VPC endpoints<a name="vpc-endpoint-considerations"></a>

Before you set up an interface VPC endpoint for AWS IoT SiteWise, review the [Interface endpoint properties and limitations](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-limitations) in the *Amazon VPC User Guide*\. 

VPC endpoint policies are not supported for AWS IoT SiteWise\. By default, full access to AWS IoT SiteWise is allowed through the endpoint\. For more information, see [Controlling access to services with VPC endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-access.html) in the *Amazon VPC User Guide*\.

AWS IoT SiteWise supports making calls to the following AWS IoT SiteWise API operations from your VPC:
+ For the data plane API operations \([BatchPutAssetPropertyValue](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_BatchPutAssetPropertyValue.html), [GetAssetPropertyAggregates](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_GetAssetPropertyAggregates.html), [GetAssetPropertyValue](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_GetAssetPropertyValue.html), and [GetAssetPropertyValueHistory](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_GetAssetPropertyValueHistory.html), use the the following endpoint\. Replace `region` with your AWS region\.

  ```
  data.iotsitewise.region.amazonaws.com
  ```
+ The remaining [AWS IoT SiteWise API operations](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_Operations.html) are the control plane API operations\. For the control plane API operations, you can now use the following endpoint\. Replace `region` with your AWS region\.

  ```
  api.iotsitewise.region.amazonaws.com
  ```
**Note**  
For the control plane API operations, if you have firewalls or VPCs with strict egress \(outbound traffic\) rules, you might configure the rules before you set up an interface VPC endpoint\. The rules must grant you access to the `com.amazonaws.region.iotsitewise.api` service through the `api.iotsitewise.region.amazonaws.com` endpoint\.
The interface VPC endpoint for the control plane API operations currently doesn't support condition keys for IAM policies\. For more information, see [Condition keys](security_iam_service-with-iam.md#security_iam_service-with-iam-id-based-policies-conditionkeys)\.
While the interface VPC endpoint for the control plane API operations is in preview, you must download the preview AWS CLI and AWS SDK to access AWS IoT SiteWise through the endpoint\. For more information, see [Interface VPC endpoints preview AWS CLI and AWS SDKs](#private-link-preview-sdk)\.

  Instead of using the following endpoints for the associated API operations, you can use `api.iotsitewise.region.amazonaws.com` for all the control plane API operations\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/vpc-interface-endpoints.html)

## Creating an interface VPC endpoint for AWS IoT SiteWise<a name="vpc-endpoint-create"></a>

You can create a VPC endpoint for the AWS IoT SiteWise service\. You can use either the Amazon VPC console or the AWS Command Line Interface \(AWS CLI\)\. For more information, see [Creating an interface endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint) in the *Amazon VPC User Guide*\.

Create a VPC endpoint for AWS IoT SiteWise by using one of the following service names:
+ For the data plane API operations, use the following service name: 

  ```
  com.amazonaws.region.iotsitewise.data
  ```
+ For the control plane API operations, use the following service name: 

  ```
  com.amazonaws.region.iotsitewise.api
  ```

## Accessing AWS IoT SiteWise through an interface VPC endpoint<a name="vpc-endpoint-access"></a>

When you create an interface endpoint, we generate endpoint\-specific DNS hostnames that you can use to communicate with AWS IoT SiteWise\. The private DNS option is enabled by default\. For more information, see [Using private hosted zones](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-private-hosted-zones) in the *Amazon VPC User Guide*\.

If you enable private DNS for the endpoint, you can make API requests to AWS IoT SiteWise through one of the following VPC endpoints\.
+ For the data plane API operations, use the following endpoint\. Replace *region* with your AWS Region\.

  ```
  data.iotsitewise.region.amazonaws.com
  ```
+ For the control plane API operations, use the following endpoint\. Replace *region* with your AWS Region\.

  ```
  api.iotsitewise.region.amazonaws.com
  ```

If you disable private DNS for the endpoint, you must do the following to access AWS IoT SiteWise through the endpoint:
+ Specify the VPC endpoint url in API requests\.
  + For the data plane API operations, use the following endpoint url\. Replace *vpc\-endpoint\-id* and *region* with your VPC endpoint ID and Region\.

    ```
    vpc-endpoint-id.data.iotsitewise.region.vpce.amazonaws.com
    ```
  + For the control plane API operations, use the following endpoint url\. Replace *vpc\-endpoint\-id* and *region* with your VPC endpoint ID and Region\.

    ```
    vpc-endpoint-id.api.iotsitewise.region.vpce.amazonaws.com
    ```
+ Disable host prefix injection\. The AWS CLI and AWS SDKs prepend the service endpoint with various host prefixes when you call each API operation\. This feature causes the AWS CLI and AWS SDKs to produce invalid URLs for AWS IoT SiteWise when you specify a VPC endpoint\.
**Important**  
You can't disable host prefix injection in the AWS CLI or the AWS Tools for PowerShell\. This means that if you disable private DNS, then you can't use these tools to access AWS IoT SiteWise through the VPC endpoint\. Enable private DNS to use the AWS CLI or the AWS Tools for PowerShell to access AWS IoT SiteWise through the endpoint\.

  For more information about how to disable host prefix injection in the AWS SDKs, see the following documentation sections for each SDK:
  + [AWS SDK for C\+\+](https://sdk.amazonaws.com/cpp/api/LATEST/struct_aws_1_1_client_1_1_client_configuration.html#a3579c1a2f2e1c9d54e99c59d27643499)
  + [AWS SDK for Go](https://docs.aws.amazon.com/sdk-for-go/api/aws/#Config.WithDisableEndpointHostPrefix)
  + [AWS SDK for Go v2](https://docs.aws.amazon.com/sdk-for-go/v2/api/aws/#Config)
  + [AWS SDK for Java](https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/ClientConfiguration.html#setDisableHostPrefixInjection-boolean-)
  + [AWS SDK for Java 2\.x](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/core/client/config/SdkAdvancedClientOption.html)
  + [AWS SDK for JavaScript](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/Config.html#hostPrefixEnabled-property)
  + [AWS SDK for \.NET](https://docs.aws.amazon.com/sdkfornet/v3/apidocs/items/Runtime/TClientConfig.html)
  + [AWS SDK for PHP](https://docs.aws.amazon.com/aws-sdk-php/v3/api/class-Aws.AwsClient.html#___construct)
  + [AWS SDK for Python \(Boto3\)](https://botocore.amazonaws.com/v1/documentation/api/latest/reference/config.html)
  + [AWS SDK for Ruby](https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/IoTSiteWise/Client.html#initialize-instance_method)

For more information, see [Accessing a service through an interface endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#access-service-though-endpoint) in the *Amazon VPC User Guide*\.

### Interface VPC endpoints preview AWS CLI and AWS SDKs<a name="private-link-preview-sdk"></a>

Because the interface VPC endpoint for the control plane API operations is in preview, you must download the AWS CLI and SDK resources from the following links to use the endpoint in your scripts and applications\.
+ [AWS IoT SiteWise interface VPC endpoints preview AWS SDK for Java](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWisePrivateLinkJavaSDK.zip)
+ [AWS IoT SiteWise interface VPC endpoints preview AWS SDK for Python \(Boto3\)](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWisePrivateLinkPythonSDK.zip)
+ [AWS IoT SiteWise interface VPC endpoints preview AWS SDK for JavaScript in Node\.js](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWisePrivateLinkNodeSDK.zip)
+ [AWS IoT SiteWise interface VPC endpoints preview AWS SDK for Go](https://aws-iot-sitewise.s3.amazonaws.com/sdk/AWSIoTSiteWisePrivateLinkGoSDK.zip)

#### Configuring the AWS CLI<a name="configure-alarms-cli"></a>

You must complete this step to enable the interface VPC endpoint for the control plane API operations in the AWS CLI\.

From a command prompt, run `aws --version` to determine if the AWS CLI is installed\. If you don't have it installed, follow the instructions to install the [AWS CLI](https://aws.amazon.com/cli/)\.

**To enable the interface VPC endpoint for the control plane API operations in the AWS CLI**

1. Download the AWS IoT SiteWise [iotsitewise\-private\-link\.json](https://aws-iot-sitewise.s3.amazonaws.com/cli/iotsitewise-private-link.json) file\.

1. Navigate to the directory where you downloaded the `iotsitewise-private-link.json` file\.

1. From a command prompt, run the following command\.

   When you configure the preview AWS CLI, you must specify a different service name instead of `iotsitewise`\. You must use the new service name in the commands\. The following example command uses *iotsitewise\-privateLink*\.

   ```
   aws configure add-model --service-name iotsitewise-privateLink --service-model file://iotsitewise-private-link.json
   ```

The `aws iotsitewise-privateLink` AWS CLI commands are now available\.