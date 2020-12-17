# Ingesting external alarm state<a name="ingest-external-alarm-state"></a>


|  | 
| --- |
|  The alarms feature is in preview release for AWS IoT SiteWise, AWS IoT Events, and SiteWise Monitor, and is subject to change\. We recommend that you use this feature only with test data, and not in production environments\. While the alarms feature is in preview, you must download the alarms preview AWS SDK and AWS Command Line Interface \(AWS CLI\) to use the API operations for this feature\. These API operations aren't available in the public AWS SDK or AWS CLI\. For more information, see [Alarms preview AWS CLI and AWS SDKs](alarms-preview-sdk.md)\.  | 

External alarms are alarms that you evaluate outside of AWS IoT SiteWise\. You can use external alarms when you have a data source that reports alarm state that you want to ingest to AWS IoT SiteWise\.

Alarm state properties require a specific format for alarm state data values\. Each data value must be a JSON object serialized to a string\. Then, you ingest the serialized string as a string value\. For more information, see [Alarm state properties](industrial-alarms.md#alarm-state-properties)\.

**Example alarm state data value \(not serialized\)**  

```
{
  "stateName": "ACTIVE"
}
```

**Example alarm state data value \(serialized\)**  

```
{\"stateName\":\"ACTIVE\"}
```

**Note**  
If your data source can't report data in this format, or you can't convert your data to this format before you ingest it, you might choose not to use an alarm property\. Instead, you can ingest the data as a measurement property with the string data type, for example\. For more information, see [Defining data streams from equipment \(measurements\)](measurements.md) and [Ingesting data to AWS IoT SiteWise](industrial-data-ingestion.md)\.

**Topics**
+ [Mapping external alarm state streams](connect-alarm-data-streams.md)
+ [Ingesting alarm state data](ingest-alarm-state-data.md)