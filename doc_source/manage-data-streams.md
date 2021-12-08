# Managing data streams<a name="manage-data-streams"></a>

You can organize your data by associating data streams with asset properties or disassociating data streams from asset properties\. Currently, you can associate data streams with measurements only\. Measurements are a type of asset property that represent devices' raw sensor data streams, such as timestamped temperature values or timestamped rotations per minute \(RPM\) values\.

If the associated measurement is used to define a metric or transform, incoming data from the data stream initiates computations\.

**Note**  
An asset property can't be associated with multiple data streams at the same time\.

The following sections show you how to use the AWS IoT SiteWise console or API to manage data streams\.

**Topics**
+ [Prerequisites](#manage-data-streams-prerequisites)
+ [Managing data streams \(console\)](manage-data-streams-console.md)
+ [Managing data streams \(AWS CLI\)](manage-data-streams-cli.md)

## Prerequisites<a name="manage-data-streams-prerequisites"></a>

To begin managing data streams, completing the following\.

**Note**  
If you're new to AWS IoT SiteWise after November 24, 2021, you can skip this section\.
+ Make sure that your IAM role has the permissions shown in the following example\.  
**Example IAM user policy**  

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Sid": "PutAssetPropertyValuesAssetPropertyOnly",
              "Effect": "Allow",
              "Action": "iotsitewise:BatchPutAssetPropertyValue",
              "Resource": "arn:aws:iotsitewise:*:*:asset/*"
          },
          {
              "Sid": "PutAssetPropertyValuesPropertyAliasAllowed",
              "Effect": "Allow",
              "Action": "iotsitewise:BatchPutAssetPropertyValue",
              "Resource": "arn:aws:iotsitewise:*:*:timeseries/*"
          }
      ]
  }
  ```
**Important**  
Before you ingest data to a data stream, do the following\.  
The `timeseries` resource must be authorized if you use a property alias to identify the data stream\.
The `asset` resource must be authorized if you use an asset ID to identify the asset that contains the associated asset property\.

  For more information about configuring IAM policies, see [Managing IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage.html) in the *IAM User Guide*\.
+ Configure data ingestion settings to enable AWS IoT SiteWise to accept data streams that aren't associated with asset properties \.

### Configure data ingestion settings \(console\)<a name="configure-data-ingestion-console"></a>

You can enable AWS IoT SiteWise to accept data streams not associated with asset properties by using the AWS IoT SiteWise console\.

**To configure data ingestion settings \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the navigation pane, under **Settings**, choose **Data ingestion**\.

1. On the **Data ingestion** page, choose **Edit**\.

1. In the **Disassociated data ingestion** section, choose **Enable data ingestion for data streams not associated with asset properties**\.
**Important**  
After you enable AWS IoT SiteWise to accept data streams not associated with asset properties, you can't disable this setting\.

1. Choose **Save**\.

1. In **Enable disassociated data ingestion**, choose **Update**\. The status for **Disassociated data ingestion** becomes **Active**\. This process can take a few minutes to complete\.

### Configure data ingestion settings \(AWS CLI\)<a name="configure-data-ingestion-cli"></a>

You can enable AWS IoT SiteWise to accept data streams not associated with asset properties by using the [PutStorageConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_PutStorageConfiguration.html) API operation\. The following section uses the AWS CLI\.

**To configure data ingestion settings \(AWS CLI\)**

1. To enable AWS IoT SiteWise to receive data streams not associated with asset properties, run the following command\.
**Important**  
After you enable AWS IoT SiteWise to accept data streams not associated with asset properties, you can't disable this setting\.

   ```
   aws iot-sitewise put-storage-configuration \
                            --storage-type SITEWISE_DEFAULT_STORAGE \
                            --disassociated-data-storage ENABLED
   ```

   The `storageType` can be configured to `MULTI_LAYER_STORAGE`\. For more information, see [Managing data storage](manage-data-storage.md)\.  
**Example response**  

   ```
   {
       "storageType": "SITEWISE_DEFAULT_STORAGE",
       "disassociatedDataStorage": "ENABLED",
       "configurationStatus": {
           "state": "UPDATE_IN_PROGRESS"
       }
   }
   ```

   This process can take a few minutes to complete\.

1. To retrieve the storage configuration information, run the following command\.

   ```
   aws iot-sitewise --describe-storage-configuration
   ```  
**Example response**  

   ```
   {
       "storageType": "SITEWISE_DEFAULT_STORAGE",
       "disassociatedDataStorage": "ENABLED",
       "configurationStatus": {
           "state": "ACTIVE"
       },
       "lastUpdateDate": "2021-11-16T15:54:14-07:00"
   }
   ```