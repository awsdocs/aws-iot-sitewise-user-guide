# Configure storage settings \(console\)<a name="configure-storage-console"></a>

The following procedure shows you how to configure the storage settings to replicate data to the cold tier in the AWS IoT SiteWise console\.

**To configure storage settings in the console**

1. Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the navigation pane, under **Settings**, choose **Storage**\.

1. In the upper\-right corner, choose **Edit**\.

1. On the **Edit storage** page, do the following:

   1. For **Storage settings**, choose **Enable cold tier storage**\. The cold tier storage is disabled by default\.

   1. For **S3 bucket location**, enter the name of an existing Amazon S3 bucket and a prefix\.
**Note**  
Amazon S3 uses the prefix as a folder name in the Amazon S3 bucket\. The prefix must have 1\-255 characters and end with a forward slash \(/\)\. Your AWS IoT SiteWise data is saved in this folder\.
If you don't have an Amazon S3 bucket, choose **View**, and then create one in the Amazon S3 console\. For more information, see [Create your first S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) in the *Amazon S3 User Guide*\.

   1. For **S3 access role**, do one of the following:
      + Choose **Create a role from an AWS managed template**, AWS automatically creates an IAM role that allows AWS IoT SiteWise to send data to Amazon S3\.
      + Choose **Use an existing role**, and then choose the role that you created from the list\.
**Note**  
You must use the same Amazon S3 bucket name for the **S3 bucket location** that you used in the previous step and in your IAM policy\.
Make sure that your role has the permissions shown in the following example\.  

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

   1. \(Optional\) For **Hot tier settings**, do the following\.

      1. If you want to set a retention period for how long your data is stored in the hot tier before it's deleted, choose **Enable retention period**\.

      1. To configure a retention period, enter a whole number and choose a unit\. The retention period must be greater than or equal to 30 days\.

      AWS IoT SiteWise will delete any data in the hot tier that's older than the retention period\. If you don't set a retention period, your data is stored indefinitely\.

   1. \(Optional\) For **AWS IoT Analytics integration**, do the following\.

      1. If you want to use AWS IoT Analytics to query your data, choose **Enabled AWS IoT Analytics data store**\.

      1. AWS IoT SiteWise generates a name for your data store or you can enter a different name\.

      AWS IoT SiteWise automatically creates a data store in AWS IoT Analytics to save your data\. To query the data, you can use AWS IoT Analytics to create datasets\. For more information, see [Working with AWS IoT SiteWise data](https://docs.aws.amazon.com/iotanalytics/latest/userguide/dataset-itsw.html) in the *AWS IoT Analytics User Guide*\.

   1. Choose **Save**\.

In the **AWS IoT SiteWise storage** section, the **Cold tier storage** can be one of the following values:
+ **Enabled** – AWS IoT SiteWise replicates your data to the specified Amazon S3 bucket\.
+ **Enabling** – AWS IoT SiteWise is processing your request to enable the cold tier storage\. This process can take several minutes to complete\.
+ **Enable\_Failed** – AWS IoT SiteWise couldn't process your request to enable the cold tier storage\. If you enabled AWS IoT SiteWise to send logs to Amazon CloudWatch Logs, you can use these logs to troubleshoot issues\. For more information, see [Monitoring AWS IoT SiteWise with Amazon CloudWatch Logs](monitor-cloudwatch-logs.md)\.
+ **Disabled** – The cold tier storage is disabled\.