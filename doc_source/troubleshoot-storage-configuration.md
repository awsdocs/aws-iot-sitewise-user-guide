# Troubleshoot<a name="troubleshoot-storage-configuration"></a>

Use the following information to troubleshoot and resolve issues with the storage configuration\.

**Topics**
+ [Error: Bucket doesn't exist](#no-s3-bucket)
+ [Error: Access denied to S3 path](#iam-permissions)
+ [Error: Role ARN can't be assumed](#iam-trust-relationship)
+ [Error: Failed to access cross\-Region S3 bucket](#cross-region-s3-bucket)

## Error: Bucket doesn't exist<a name="no-s3-bucket"></a>

**Solution:** AWS IoT SiteWise couldn't find your Amazon S3 bucket\. Make sure you enter the name of an existing Amazon S3 bucket in the current Region\.

## Error: Access denied to S3 path<a name="iam-permissions"></a>

**Solution:** AWS IoT SiteWise couldn't access your Amazon S3 bucket\. Do the following:
+ Make sure that you use the same Amazon S3 bucket that you specified in the IAM policy\.
+ Make sure that your role has the permissions shown in the following example\.  
**Example permissions policy**  

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "s3:PutObject",
                  "s3:GetObject",
                  "s3:DeleteObject",
                  "s3:GetBucketLocation",
                  "s3:ListBucket"
              ],
              "Resource": [
                  "arn:aws:s3:::bucket-name",
                  "arn:aws:s3:::bucket-name/*"
              ]
          }
      ]
  }
  ```

  Replace *bucket\-name* with the name of your Amazon S3 bucket\.

## Error: Role ARN can't be assumed<a name="iam-trust-relationship"></a>

**Solution:** AWS IoT SiteWise couldn't assume the IAM role on your behalf\. Make sure that your role trusts the following service: `iotsitewise.amazonaws.com`\. For more information, see [I can't assume a role](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_roles.html#troubleshoot_roles_cant-assume-role) see *IAM User Guide*\.

## Error: Failed to access cross\-Region S3 bucket<a name="cross-region-s3-bucket"></a>

**Solution:** The Amazon S3 bucket that you specified is in a different AWS Region\. Make sure that your Amazon S3 bucket and AWS IoT SiteWise assets are in the same Region\.