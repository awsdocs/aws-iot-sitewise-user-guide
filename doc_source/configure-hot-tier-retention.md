# Configuring a retention period for the hot tier<a name="configure-hot-tier-retention"></a>


****  

|  | 
| --- |
| The retention period configuration for the hot tier is in preview release for AWS IoT SiteWise and is subject to change\. We recommend that you use this tool only with test databases, and not in production environments\. | 

You can use the [PutStorageConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_RetentionPeriod.html) API operation to configure a retention period that controls how long your data is kept in the hot tier\. After a retention period is defined, AWS IoT SiteWise removes expired data from the hot tier\. If no retention period is defined, your data is kept indefinitely in the hot tier\.

**Important**  
Your changes to the retention period for the hot tier take effect immediately\.

The following procedure shows you how to configure a retention period for the hot tier\.

**To define a retention period \(AWS CLI\)**

1. To define a retention period for the cold tier, run the following command\. Replace *Retention\_period\_configuration* with the name of the file that contains the AWS IoT SiteWise storage configuration\.

   ```
   aws iotsitewise put-storage-configuration --cli-input-json file://Retention_period_configuration.json
   ```

## <a name="w490aac33c11c13c11b3b5b1b1"></a>
   + Replace *retention\-in\-days* with an integer that is greater than or equal to 30\.

**Important**  
To define a retention period for the hot tier, `storageType` must be configured to `MULTI_LAYER_STORAGE` and `unlimited` must be configured to `false`\.

   ```
   {
         "storageType": "MULTI_LAYER_STORAGE",
         "multiLayerStorage": {
             "customerManagedS3Storage": {
                 "s3ResourceArn": "arn:aws:s3:::bucket-name/prefix/",
                 "roleArn": "arn:aws:iam::aws-account-id:role/role-name"
             }
         }, 
         "retentionPeriod": { 
             "numberOfDays": retention-in-days,
             "unlimited": false
         }
     }
   ```

   Example output

   ```
   {
       "storageType": "MULTI_LAYER_STORAGE",
       "retentionPeriod": {
           "numberOfDays": 100,
           "unlimited": false
       },
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

## <a name="w490aac33c11c13c11b5b5b1b1"></a>

   ```
   {
         "storageType": "MULTI_LAYER_STORAGE",
         "multiLayerStorage": {
             "customerManagedS3Storage": {
                 "s3ResourceArn": "arn:aws:s3:::DOC-EXAMPLE-BUCKET/torque/",
                 "roleArn": "arn:aws:iam::123456789012:role/SWAccessS3Role"
             }
         },
         "retentionPeriod": { 
             "numberOfDays": 100,
             "unlimited": false
         },
         "configurationStatus": {
             "state": "ACTIVE"
         },
         "lastUpdateDate": "2021-03-30T15:54:14-07:00"
     }
   ```