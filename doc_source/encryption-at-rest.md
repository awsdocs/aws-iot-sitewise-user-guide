# Encryption at rest<a name="encryption-at-rest"></a>

AWS IoT SiteWise stores your data in the AWS Cloud and on gateways\.

## Data at rest in the AWS Cloud<a name="cloud-encryption-at-rest"></a>

AWS IoT SiteWise stores data in other AWS services that encrypt data at rest by default\. Encryption at rest integrates with AWS Key Management Service \(AWS KMS\) for managing the encryption key that is used to encrypt your asset property values and aggregate values in AWS IoT SiteWise\. You can choose to use a customer managed key to encrypt asset property values and aggregate values in AWS IoT SiteWise\. You can create, manage, and view your encryption key through AWS KMS\.

You can choose an AWS owned key to encrypt your data, or choose a customer managed keyto encrypt your asset property values and aggregate values:

### How it works<a name="how-it-works"></a>

Encryption at rest integrates with AWS KMS for managing the encryption key that is used to encrypt your data\.
+ AWS owned key – Default encryption key\. AWS IoT SiteWise owns this key\. You can't view this key in your AWS account\. You also can't see operations on the key in AWS CloudTrail logs\. You can use this key at no additional charge\.
+ Customer managed key – The key is stored in your account, which you create, own, and manage\. You have full control over the KMS key\. Additional AWS KMS charges apply\.

### AWS owned keys<a name="aws-owned-cmk"></a>

AWS owned keys aren't stored in your account\. They're part of a collection of KMS keys that AWS owns and manages for use in multiple AWS accounts\. AWS services can use AWS owned keys to protect your data\. 

 You can't view, manage, use AWS owned keys, or audit their use\. However, you don't need to do any work or change any programs to protect the keys that encrypt your data\. 

 You're not charged a monthly fee or a usage fee if you use AWS owned keys, and they don't count against AWS KMS quotas for your account\. 

### Customer managed keys<a name="customer-managed-cmk"></a>

Customer managed keys are KMS keys in your account that you create, own, and manage\. You have full control over these KMS keys, such as the following:
+ Establishing and maintaining their key policies, IAM policies, and grants
+ Enabling and disabling them
+ Rotating their cryptographic material
+ Adding tags
+ Creating aliases that refer to them 
+ Scheduling them for deletion



You can also use CloudTrail and Amazon CloudWatch Logs to track the requests that AWS IoT SiteWise sends to AWS KMS on your behalf\. 

 If you're using customer managed keys, you need to grant AWS IoT SiteWise access to the KMS key stored in your account\. AWS IoT SiteWise uses envelope encryption and key hierarchy to encrypt data\. Your AWS KMS encryption key is used to encrypt the root key of this key hierarchy\. For more information, see [Envelope encryption](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#enveloping) in the *AWS Key Management Service Developer Guide*\. 

 The following example policy grants AWS IoT SiteWise permissions to a create customer managed key on your behalf\. When you create your key, you need to allow the `kms:CreateGrant` and `kms:DescribeKey` actions\. 

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1603902045292",
      "Action": [
        "kms:CreateGrant",
        "kms:DescribeKey"
      ],
      "Effect": "Allow",
      "Resource": "*"
    }
  ]
}
```

 The encryption context for your created grant uses your `aws:iotsitewise:subscriberId` and account ID\. 

## Data at rest on gateways<a name="gateway-encryption-at-rest"></a>

AWS IoT SiteWise gateways store the following data on the local file system:
+ OPC\-UA source configuration information
+ The set of OPC\-UA data stream paths from connected OPC\-UA sources
+ Industrial data cached when the gateway loses connection to the internet

AWS IoT SiteWise gateways run on AWS IoT Greengrass\. AWS IoT Greengrass relies on Unix file permissions and full\-disk encryption \(if enabled\) to protect data at rest on the core\. It's your responsibility to secure the file system and device\.

However, AWS IoT Greengrass does encrypt local copies of your OPC\-UA server secrets retrieved from Secrets Manager\. For more information, see [Secrets encryption](https://docs.aws.amazon.com/greengrass/latest/developerguide/secrets.html#secrets-encryption) in the *AWS IoT Greengrass Version 1 Developer Guide*\.

For more information about encryption at rest on AWS IoT Greengrass cores, see [Encryption at rest](https://docs.aws.amazon.com/greengrass/latest/developerguide/encryption-at-rest.html) in the *AWS IoT Greengrass Version 1 Developer Guide*\.