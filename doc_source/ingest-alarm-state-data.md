# Ingesting alarm state data<a name="ingest-alarm-state-data"></a>

Alarm state properties expect alarm state as a serialized JSON string\. To ingest alarm state to an external alarm in AWS IoT SiteWise, you ingest this serialized string as a timestamped string value\. The following example demonstrates a state data value for an active alarm\.

```
{\"stateName\":\"ACTIVE\"}
```

To identify an alarm state property, you can specify one of the following:
+ The `assetId` and `propertyId` of the alarm property that you're sending data to\.
+ The `propertyAlias`, which is a data stream alias \(for example, `/company/windfarm/3/turbine/7/temperature/high`\)\. To use this option, you must first set your alarm property's alias\. To learn how to set property aliases for alarm state properties, see [Mapping external alarm state streams](connect-alarm-data-streams.md)\.

The following example [BatchPutAssetPropertyValue](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_BatchPutAssetPropertyValue.html) API payload demonstrates how to format the state of an external alarm\. This external alarm reports when a wind turbine's rotations per minute \(RPM\) reading is too high\.

**Example BatchPutAssetPropertyValue payload for alarm state data**  

```
{
  "entries": [
    {
      "entryId": "unique entry ID",
      "propertyAlias": "/company/windfarm/3/turbine/7/temperature/high",
      "propertyValues": [
        {
          "value": {
            "stringValue": "{\"stateName\":\"ACTIVE\"}"
          },
          "timestamp": {
            "timeInSeconds": 1607550262
          }
        }
      ]
    }
  ]
}
```
For more information about how to use the `BatchPutAssetPropertyValue` API to ingest data, see [Ingesting data using the AWS IoT SiteWise API](ingest-api.md)\.  
For more information about other ways to ingest data, see [Ingesting data to AWS IoT SiteWise](industrial-data-ingestion.md)\.