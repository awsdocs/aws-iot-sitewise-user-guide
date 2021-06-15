# Ingesting external alarm state<a name="ingest-external-alarm-state"></a>

External alarms are alarms that you evaluate outside of AWS IoT SiteWise\. You can use external alarms when you have a data source that reports alarm state that you want to ingest to AWS IoT SiteWise\.

Alarm state properties require a specific format for alarm state data values\. Each data value must be a JSON object serialized to a string\. Then, you ingest the serialized string as a string value\. For more information, see [Alarm state properties](industrial-alarms.md#alarm-state-properties)\.

**Example alarm state data value \(not serialized\)**  

```
{
  "stateName": "Active"
}
```

**Example alarm state data value \(serialized\)**  

```
{\"stateName\":\"Active\"}
```

**Note**  
If your data source can't report data in this format, or you can't convert your data to this format before you ingest it, you might choose not to use an alarm property\. Instead, you can ingest the data as a measurement property with the string data type, for example\. For more information, see [Defining data streams from equipment \(measurements\)](measurements.md) and [Ingesting data to AWS IoT SiteWise](industrial-data-ingestion.md)\.

**Topics**
+ [Mapping external alarm state streams](connect-alarm-data-streams.md)
+ [Ingesting alarm state data](ingest-alarm-state-data.md)