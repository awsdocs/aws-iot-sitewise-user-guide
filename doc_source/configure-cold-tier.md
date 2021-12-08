# Configuring the cold tier<a name="configure-cold-tier"></a>

AWS IoT SiteWise saves your data in the hot tier by default\. You can use the AWS IoT SiteWise console or API to configure the storage settings in your account so that AWS IoT SiteWise can export data to the cold tier\.

**Topics**
+ [Configure storage settings \(console\)](#configure-storage-console)
+ [Configure storage for data replication \(AWS CLI\)](#configure-storage-cli)
+ [\(Optional\) Create an AWS IoT Analytics data store \(AWS CLI\)](#create-iotanalytics-data-store-cli)

## Configure storage settings \(console\)<a name="configure-storage-console"></a>

The following procedure shows you how to configure the storage settings to export data to Amazon S3 in the AWS IoT SiteWise console\.

**To configure storage settings in the console**

1. Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the navigation pane, under **Settings**, choose **Storage**\.

1. In the upper\-right corner, choose **Edit**\.

1. On the **Edit storage** page, do the following:

   1. For **Storage settings**, choose **Enabled**\. The **Storage settings** is disabled by default\.

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

   1. \(Optional\) If you want to use AWS IoT Analytics to query your data, enable **AWS IoT Analytics data store**\. Do the following:

      1. Choose **Enabled**\.

      1. AWS IoT SiteWise generates a name for your data store or you can enter a different name\.

      AWS IoT SiteWise automatically creates a data store in AWS IoT Analytics to save your data\. To query the data, you can use AWS IoT Analytics to create datasets\. For more information, see [Working with AWS IoT SiteWise data](https://docs.aws.amazon.com/iotanalytics/latest/userguide/dataset-itsw.html) in the *AWS IoT Analytics User Guide*\.

   1. Choose **Save**\.

![\[Edit page showing Export data to Amazon S3.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/mls-edit.png)

In the **Export new data to S3** section, the **Status** can be one of the following:
+ **Enabled** – AWS IoT SiteWise exports your data to the specified Amazon S3 bucket\.
+ **Enabling** – AWS IoT SiteWise is enabling this feature\. This process can take several minutes to complete\.
+ **Enable\_Failed** – AWS IoT SiteWise couldn't enable this feature\. If you enabled AWS IoT SiteWise to send logs to Amazon CloudWatch Logs, you can use these logs to troubleshoot issues\. For more information, see [Monitoring AWS IoT SiteWise with Amazon CloudWatch Logs](monitor-cloudwatch-logs.md)\.
+ **Disabled** \- This feature is disabled\.

![\[Status page showing Export data to Amazon S3.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/mls-status.png)

## Configure storage for data replication \(AWS CLI\)<a name="configure-storage-cli"></a>

The following procedure shows you how to configure the storage settings to export data to Amazon S3 using AWS CLI\.

**To configure storage settings using AWS CLI**

1. To export data to an Amazon S3 bucket in your account, run the following command to configure the storage settings\. Replace *file\-name* with the name of the file that contains the AWS IoT SiteWise storage configuration\.

   ```
   aws iotsitewise put-storage-configuration --cli-input-json file://file-name.json
   ```  
**Example AWS IoT SiteWise storage configuration**  
   + Replace *bucket\-name* with your Amazon S3 bucket name\.
   + Replace *prefix* with your Amazon S3 prefix\.
   + Replace *aws\-account\-id* with your AWS account ID\.
   + Replace *role\-name* with the name of the Amazon S3 access role that allows AWS IoT SiteWise to send data to Amazon S3\.

   ```
   {
         "storageType": "MULTI_LAYER_STORAGE",
         "multiLayerStorage": {
             "customerManagedS3Storage": {
                 "s3ResourceArn": "arn:aws:s3:::bucket-name/prefix/",
                 "roleArn": "arn:aws:iam::aws-account-id:role/role-name"
             }
         }, 
     }
   ```
**Note**  
You must use the same Amazon S3 bucket name in the AWS IoT SiteWise storage configuration and IAM policy\.
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
**Example response**  

   ```
   {
         "storageType": "MULTI_LAYER_STORAGE",
         "configurationStatus": {
             "state": "UPDATE_IN_PROGRESS"
         }
     }
   ```
**Note**  
It can take a few minutes for AWS IoT SiteWise to update the storage configuration\.

1. To retrieve the storage configuration information, run the following command\.

   ```
   aws iotsitewise describe-storage-configuration
   ```  
**Example response**  

   ```
   {
         "storageType": "MULTI_LAYER_STORAGE",
         "multiLayerStorage": {
             "customerManagedS3Storage": {
                 "s3ResourceArn": "arn:aws:s3:::DOC-EXAMPLE-BUCKET/torque/",
                 "roleArn": "arn:aws:iam::123456789012:role/SWAccessS3Role"
             }
         },
         "configurationStatus": {
             "state": "ACTIVE"
         },
         "lastUpdateDate": "2021-03-30T15:54:14-07:00"
     }
   ```

1. To stop exporting data to the Amazon S3 bucket, run the following command to configure storage settings\.

   ```
   aws iotsitewise put-storage-configuration --storage-type SITEWISE_DEFAULT_STORAGE
   ```
**Note**  
By default, AWS IoT SiteWise only saves data to a service\-managed database\.  
**Example response**  

   ```
   {
         "storageType": "SITEWISE_DEFAULT_STORAGE",
         "configurationStatus": {
             "state": "UPDATE_IN_PROGRESS"
         }
     }
   ```

1. To retrieve the storage configuration information, run the following command\.

   ```
   aws iotsitewise describe-storage-configuration
   ```  
**Example response**  

   ```
   {
         "storageType": "SITEWISE_DEFAULT_STORAGE",
         "configurationStatus": {
             "state": "ACTIVE"
         },
         "lastUpdateDate": "2021-03-30T15:57:14-07:00"
     }
   ```

## \(Optional\) Create an AWS IoT Analytics data store \(AWS CLI\)<a name="create-iotanalytics-data-store-cli"></a>

An AWS IoT Analytics data store is a scalable and queryable repository that receives and stores data\. You can use the AWS IoT SiteWise console or AWS IoT Analytics APIs to create an AWS IoT Analytics data store to save your AWS IoT SiteWise data\. To query the data, you create datasets by using AWS IoT Analytics\. For more information, see [Working with AWS IoT SiteWise data](https://docs.aws.amazon.com/iotanalytics/latest/userguide/dataset-itsw.html) in the *AWS IoT Analytics User Guide*\.

The following steps use AWS CLI to create a data store in AWS IoT Analytics\.

To create a data store, run the following command\. Replace *file\-name* with the name of the file that contains the data store configuration\.

```
aws iotanalytics create-datastore --cli-input-json file://file-name.json
```

**Note**  
You must specify the name of an existing Amazon S3 bucket\. If you don't have an Amazon S3 bucket, create one first\. For more information, see [Create your first S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) in *Amazon S3 User Guide*\.
You must use the same Amazon S3 bucket name in the AWS IoT SiteWise storage configuration, IAM policy, and AWS IoT Analytics data store configuration\.

**Example AWS IoT Analytics data store configuration**  
Replace *data\-store\-name* and *s3\-bucket\-name* with your AWS IoT Analytics data store name and Amazon S3 bucket name\.  

```
{
      "datastoreName": "data-store-name",
      "datastoreStorage": {
          "iotSiteWiseMultiLayerStorage": {
              "customerManagedS3Storage": {
                  "bucket": "s3-bucket-name"
              }
          }
      },
      "retentionPeriod": {
          "numberOfDays": 90
      }
  }
```

**Example response**  

```
{
      "datastoreName": "datastore_IoTSiteWise_demo",
      "datastoreArn": "arn:aws:iotanalytics:us-west-2:123456789012:datastore/datastore_IoTSiteWise_demo",
      "retentionPeriod": {
          "numberOfDays": 90,
          "unlimited": false
      }
  }
```