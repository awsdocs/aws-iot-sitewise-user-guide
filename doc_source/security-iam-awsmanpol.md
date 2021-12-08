# AWS managed policies for AWS IoT SiteWise<a name="security-iam-awsmanpol"></a>

When you add permissions to users, groups, and roles, you might find it easier to use AWS managed policies rather than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. For a quicker start, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services don't remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the **ReadOnlyAccess** AWS managed policy provides read\-only access to all AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list with descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## AWS managed policy: AWSIoTSiteWiseReadOnlyAccess<a name="security-iam-awsmanpol-AWSIoTSiteWiseReadOnlyAccess"></a>

Use the `AWSIoTSiteWiseReadOnlyAccess` AWS managed policy to allow read\-only access to AWS IoT SiteWise\.

You can attach the `AWSIoTSiteWiseReadOnlyAccess` policy to your IAM identities\.

**Service\-level permissions**

This policy provides read\-only access to AWS IoT SiteWise\. No other service permissions are included in this policy\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iotsitewise:Describe*",
                "iotsitewise:List*",
                "iotsitewise:Get*"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS IoT SiteWise updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>

You can view details about updates to AWS managed policies for AWS IoT SiteWise, beginning from when this service began tracking the changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the AWS IoT SiteWise Document history page\.


| Change | Description | Date | 
| --- | --- | --- | 
|  [AWSIoTSiteWiseReadOnlyAccess](#security-iam-awsmanpol-AWSIoTSiteWiseReadOnlyAccess) – New policy  |  AWS IoT SiteWise added a new policy to grant read\-only access to AWS IoT SiteWise\.  | November 24, 2021 | 
|  AWS IoT SiteWise started tracking changes  |  AWS IoT SiteWise started tracking changes for its AWS managed policies\.  | November 24, 2021 | 