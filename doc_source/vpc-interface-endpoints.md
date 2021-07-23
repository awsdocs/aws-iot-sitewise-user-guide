# AWS IoT SiteWise and interface VPC endpoints \(AWS PrivateLink\)<a name="vpc-interface-endpoints"></a>

You can establish a private connection between your virtual private cloud \(VPC\) and AWS IoT SiteWise by creating an *interface VPC endpoint*\. Interface endpoints are powered by [AWS PrivateLink](http://aws.amazon.com/privatelink), a technology that you can use to privately access AWS IoT SiteWise API operations without an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection\. Instances in your VPC don't need public IP addresses to communicate with AWS IoT SiteWise API operations\. Traffic between your VPC and AWS IoT SiteWise doesn't leave the AWS network\.

Each interface endpoint is represented by one or more [elastic network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) in your subnets\. 

For more information, see [Interface VPC endpoints \(AWS PrivateLink\)](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) in the *Amazon VPC User Guide*\.

## Considerations for AWS IoT SiteWise VPC endpoints<a name="vpc-endpoint-considerations"></a>

Before you set up an interface VPC endpoint for AWS IoT SiteWise, review the [Interface endpoint properties and limitations](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-limitations) in the *Amazon VPC User Guide*\. 

AWS IoT SiteWise supports making calls to the following AWS IoT SiteWise API operations from your VPC:
+ For all the data plane API operations, use the following endpoint\. Replace `region` with your AWS Region\.

  ```
  data.iotsitewise.region.amazonaws.com
  ```

  The data plane API operations include [BatchPutAssetPropertyValue](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_BatchPutAssetPropertyValue.html), [GetAssetPropertyAggregates](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_GetAssetPropertyAggregates.html), [GetAssetPropertyValue](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_GetAssetPropertyValue.html), [GetAssetPropertyValueHistory](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_GetAssetPropertyValueHistory.html) and [GetInterpolatedAssetPropertyValues](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_GetInterpolatedAssetPropertyValues.html)\.
+ For the control plane API operations that you use to manage asset models, assets, gateways, tags, and account configurations, use the following endpoint\. Replace `region` with your AWS Region\.

  ```
  api.iotsitewise.region.amazonaws.com
  ```

  The supported control plane API operations include [AssociateAssets](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_AssociateAssets.html), [CreateAsset](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_CreateAsset.html), [CreateAssetModel](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_CreateAssetModel.html), [DeleteAsset](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DeleteAsset.html), [DeleteAssetModel](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DeleteAssetModel.html), [DeleteDashboard](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DeleteDashboard.html), [DescribeAsset](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeAsset.html), [DescribeAssetModel](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeAssetModel.html), [DescribeAssetProperty](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeAssetProperty.html), [DescribeDashboard](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeDashboard.html), [DescribeLoggingOptions](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeLoggingOptions.html), [DisassociateAssets](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DisassociateAssets.html), [ListAssetModels](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListAssetModels.html), [ListAssetRelationships](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListAssetRelationships.html), [ListAssets](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListAssets.html), [ListAssociatedAssets](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListAssociatedAssets.html), [PutLoggingOptions](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_PutLoggingOptions.html), [UpdateAsset](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateAsset.html), [UpdateAssetModel](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateAssetModel.html), [UpdateAssetProperty](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateAssetProperty.html), [CreateGateway](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_CreateGateway.html), [DeleteGateway](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DeleteGateway.html), [DescribeGateway](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeGateway.html), [DescribeGatewayCapabilityConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeGatewayCapabilityConfiguration.html), [ListGateways](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListGateways.html), [UpdateGateway](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateGateway.html), [UpdateGatewayCapabilityConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateGatewayCapabilityConfiguration.html), [DescribeStorageConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeStorageConfiguration.html), [PutStorageConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_PutStorageConfiguration.html),  [DescribeDefaultEncryptionConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeDefaultEncryptionConfiguration.html), [ListTagsForResource](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListTagsForResource.html), [PutDefaultEncryptionConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_PutDefaultEncryptionConfiguration.html), [TagResource](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_TagResource.html), and [UntagResource](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UntagResource.html)\.
**Note**  
The interface VPC endpoint for the control plane API operations currently doesn't support making calls to the following SiteWise Monitor API operations: [BatchAssociateProjectAssets](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_BatchAssociateProjectAssets.html), [BatchDisassociateProjectAssets](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_BatchDisassociateProjectAssets.html), [CreateAccessPolicy](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_CreateAccessPolicy.html), [CreateDashboard](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_CreateDashboard.html), [CreatePortal](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_CreatePortal.html), [CreateProject](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_CreateProject.html), [DeleteAccessPolicy](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DeleteAccessPolicy.html), [DeletePortal](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DeletePortal.html), [DeleteProject](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DeleteProject.html), [DescribeAccessPolicy](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeAccessPolicy.html), [DescribePortal](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribePortal.html), [DescribeProject](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeProject.html), [ListAccessPolicies](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListAccessPolicies.html), [ListDashboards](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListDashboards.html), [ListPortals](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListPortals.html), [ListProjectAssets](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListProjectAssets.html), [ListProjects](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListProjects.html), [UpdateAccessPolicy](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateAccessPolicy.html), [UpdateDashboard](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateDashboard.html), [UpdatePortal](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdatePortal.html), and [UpdateProject](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateProject.html)\.

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

## Creating a VPC endpoint policy for AWS IoT SiteWise<a name="vpc-endpoint-policy"></a>

You can attach an endpoint policy to your VPC endpoint that controls access to AWS IoT SiteWise\. The policy specifies the following information:
+ The principal that can perform operations\.
+ The operations that can be performed\.
+ The resources on which operations can be performed\.

For more information, see [Controlling access to services with VPC endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-access.html) in the *Amazon VPC User Guide*\. 

**Example: VPC endpoint policy for AWS IoT SiteWise actions**  
The following is an example of an endpoint policy for AWS IoT SiteWise\. When attached to an endpoint, this policy grants access to the listed AWS IoT SiteWise actions for the IAM user *`iotsitewiseadmin`* in AWS account *123456789012* on the specified asset\.

```
{
    "Statement": [
        {
            "Action": [
                "iotsitewise:CreateAsset",
                "iotsitewise:ListGateways",
                "iotsitewise:ListTagsForResource"
            ],
            "Effect": "Allow",
            "Resource": "arn:aws:iotsitewise:us-west-2:123456789012:asset/a1b2c3d4-5678-90ab-cdef-33333EXAMPLE",
            "Principal": {
                "AWS": [
                    "123456789012:user/iotsitewiseadmin"
                ]
            }
        }
    ]
}
```

**Note**  
The interface VPC endpoint for the data plane API operations currently doesn't support VPC endpoint policies\.