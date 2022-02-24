# Managing data streams \(AWS CLI\)<a name="manage-data-streams-cli"></a>

You can use the following API operations to manage your data streams\. The code examples use the AWS CLI\.
+ [AssociateTimeSeriesToAssetProperty](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_AssociateTimeSeriesToAssetProperty.html) – Associates a data stream \(time series\) with an asset property\.
+ [DisassociateTimeSeriesFromAssetProperty](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DisassociateTimeSeriesFromAssetProperty.html) – Disassociates a data stream from an asset property\.
+ [DeleteTimeSeries](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DeleteTimeSeries.html) – Deletes a data stream\.
+ [DescribeTimeSeries](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeTimeSeries.html) – Retrieves information about a data stream\.
+ [ListTimeSeries](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListTimeSeries.html) – Retrieves a paginated list of data streams\.

## AssociateTimeSeriesToAssetProperty<a name="AssociateTimeSeriesToAssetProperty"></a>

To associate a data stream with an asset property, run the following command\.

**Important**  
The specified asset property must not be currently associated with any data stream\.
+ Replace *data\-stream\-alias* with the alias of the data stream that you're associating\.
+ Replace *asset\-ID* with the ID of the asset in which the asset property was created\.
+ Replace *property\-ID* with the ID of the asset property\.

```
aws iotsitewise associate-time-series-to-asset-propert \ 
                 --alias data-stream-alias \
                 --assetId asset-ID \
                 --propertyId property-ID
```

## DisassociateTimeSeriesFromAssetProperty<a name="DisassociateTimeSeriesFromAssetProperty"></a>

To disassociate a data stream from an asset property, run the following command\.
+ Replace *data\-stream\-alias* with the alias of the data stream that you're disassociating\.
+ Replace *asset\-ID* with the ID of the asset in which the asset property was created\.
+ Replace *property\-ID* with the ID of the asset property\.

```
aws iotsitewise disassociate-time-series-from-asset-property \ 
                 --alias data-stream-alias \
                 --assetId asset-ID \
                 --propertyId property-ID
```

## DeleteTimeSeries<a name="DeleteTimeSeries"></a>

To delete a data stream, run the following command\.

Replace *data\-stream\-alias* with the alias of the data stream that you're deleting\.

```
aws iotsitewise delete-time-series --alias data-stream-alias
```

To identify a data stream, do one of the following:
+ If the data stream isn't associated with an asset property, specify the `alias` of the data stream\.
+ If the data stream is associated with an asset property, specify one of the following: 
  + The `alias` of the data stream\.
  + The `assetId` and `propertyId` that identifies the asset property\.

## DescribeTimeSeries<a name="DescribeTimeSeries"></a>

You can use the `DescribeTimeSeries` API operation to verify if you successfully associated or disassociated a data stream\.

To retrieve information about a data stream, run the following command\.

```
aws iotsitewise describe-time-series --alias data-stream-alias
```

To identify a data stream, do one of the following:
+ If the data stream isn't associated with an asset property, specify the `alias` of the data stream\.
+ If the data stream is associated with an asset property, specify one of the following: 
  + The `alias` of the data stream\.
  + The `assetId` and `propertyId` that identifies the asset property\.

## ListTimeSeries<a name="ListTimeSeries"></a>

You can use the `ListTimeSeries` API operation to verify if you successfully deleted a data stream\.

To retrieve a paginated list of data streams, run the following command\.

```
aws iotsitewise list-time-series
```