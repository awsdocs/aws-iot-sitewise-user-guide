# Key management<a name="key-management"></a>

## AWS IoT SiteWise cloud key management<a name="key-cloud-sw"></a>

By default, AWS IoT SiteWise uses AWS managed customer master keys \(CMKs\) to protect your data in the AWS Cloud\. You can update your settings to use a customer managed CMK to encrypt some data in AWS IoT SiteWise\. You can create, manage, and view your encryption key through AWS Key Management Service \(AWS KMS\)\.

AWS IoT SiteWise supports server\-side encryption with customer managed CMKs stored in AWS KMS to encrypt the following data:
+ Asset property values
+ Aggregate values

**Note**  
 Other data and resources are encrypted using the default encryption with keys managed by AWS IoT SiteWise\. This key is stored in the AWS IoT SiteWise account\. 

 For more information, see [What is AWS Key Management Service?](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html) in the *AWS Key Management Service Developer Guide*\. 

### Enable encryption using customer managed CMKs<a name="CMK-setup"></a>

To use customer managed CMKs with AWS IoT SiteWise, you need to update your AWS IoT SiteWise settings\.

**To enable encryption using CMKs**

1.  

   Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\. 

1. Choose **Account Settings** and choose **Edit** to open the **Edit account settings** page\. 

1.  For **Encryption key type**, choose **Choose a different AWS KMS key**\. This enables encryption with customer managed CMKs stored in AWS KMS\. 
**Note**  
Currently, you can only use customer managed CMK encryption for asset property values and aggregate values\.

1. Choose your CMK with one of the following options:
   + **To use an existing CMK** – Choose your CMK alias from the list\. 
   + **To create a new CMK** – Choose **Create an AWS KMS key**\.
**Note**  
This opens the AWS KMS dashboard\. For more information about creating a CMK, see [Creating keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) in the *AWS Key Management Service Developer Guide*\.

1. Choose **Save** to update your settings\.

## AWS IoT Greengrass gateway key management<a name="key-gateway-gg"></a>

 AWS IoT SiteWise gateways run on AWS IoT Greengrass, and AWS IoT Greengrass core devices use public and private keys to authenticate with the AWS Cloud and encrypt local secrets, such as OPC\-UA authentication secrets\. For more information, see [Key management](https://docs.aws.amazon.com/greengrass/latest/developerguide/key-management.html) in the *AWS IoT Greengrass Developer Guide*\. 