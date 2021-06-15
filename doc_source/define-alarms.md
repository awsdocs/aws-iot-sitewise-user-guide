# Defining alarms on asset models<a name="define-alarms"></a>

Asset models drive standardization of your industrial data and alarms\. You can define alarm definitions on asset models to standardize the alarms for all assets based on an asset model\.

You use *composite asset models* to define alarms on asset models\. Composite asset models are asset models that standardize a specific set of properties on another asset model\. Composite asset models ensure that certain properties are present on an asset model\. Alarms have type, state, and \(optional\) source properties, so the alarm composite model enforces that these properties exist\.

Each composite asset model has a type that defines the properties for that composite model\. Alarm composite models define properties for alarm type, alarm state, and \(optional\) alarm source\. When you create an asset from an asset model with composite models, the asset includes the properties from the composite model alongside the properties that you specify in the asset model\.

Each property in a composite model must have the name that identifies it for its type of composite model\. Composite model properties support properties with complex data types\. These properties have the `STRUCT` data type and a `dataTypeSpec` trait that specifies the complex data type of the property\. Complex data type properties contain JSON data serialized as strings\.

Alarm composite models have the following properties\. Each property must have the name that identifies it for this type of composite model\.

**Alarm type**  
The type of the alarm\. Specify one of the following:  
+ `IOT_EVENTS` – An AWS IoT Events alarm\. AWS IoT SiteWise sends data to AWS IoT Events to evaluate the state of this alarm\. You must specify the alarm source property to define the AWS IoT Events alarm model for this alarm definition\.
+ `EXTERNAL` – An external alarm\. You ingest the state of the alarm as a measurement\.
Property name: `AWS/ALARM_TYPE`  
Property type: [attribute](attributes.md)  
Data type: `STRING`

**Alarm state**  
The time series data for the state of the alarm\. This is an object serialized as a string that contains the state and other information about the alarm\. For more information, see [Alarm state properties](industrial-alarms.md#alarm-state-properties)\.  
Property name: `AWS/ALARM_STATE`  
Property type: [measurement](measurements.md)  
Data type: `STRUCT`  
Data structure type: `AWS/ALARM_STATE`

**Alarm source**  
\(Optional\) The Amazon Resource Name \(ARN\) of the resource that evaluates the state of the alarm\. For AWS IoT Events alarms, this is the ARN of the alarm model\.  
Property name: `AWS/ALARM_SOURCE`  
Property type: [attribute](attributes.md)  
Data type: `STRING`

**Example alarm composite model**  
The following asset model represents a boiler that has an alarm to monitor its temperature\. AWS IoT SiteWise sends the temperature data to AWS IoT Events to detect the alarm\.  

```
{
  "assetModelName": "Boiler",
  "assetModelDescription": "A boiler that alarms when its temperature exceeds its limit.",
  "assetModelProperties": [
    {
      "name": "Temperature",
      "dataType": "DOUBLE",
      "unit": "Celsius",
      "type": {
        "measurement": {}
      }
    },
    {
      "name": "High Temperature",
      "dataType": "DOUBLE",
      "unit": "Celsius",
      "type": {
        "attribute": {
          "defaultValue": "105.0"
        }
      }
    }
  ],
  "assetModelCompositeModels": [
    {
      "name": "BoilerTemperatureHighAlarm",
      "type": "AWS/ALARM",
      "properties": [
        {
          "name": "AWS/ALARM_TYPE",
          "dataType": "STRING",
          "type": {
            "attribute": {
              "defaultValue": "IOT_EVENTS"
            }
          }
        },
        {
          "name": "AWS/ALARM_STATE",
          "dataType": "STRUCT",
          "dataTypeSpec": "AWS/ALARM_STATE",
          "type": {
            "measurement": {}
          }
        },
        {
          "name": "AWS/ALARM_SOURCE",
          "dataType": "STRING",
          "type": {
            "attribute": {}
          }
        }
      ]
    }
  ]
}
```

**Topics**
+ [Defining AWS IoT Events alarms](define-iot-events-alarms.md)
+ [Defining external alarms](define-external-alarms.md)