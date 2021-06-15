# Defining external alarms<a name="define-external-alarms"></a>

External alarms contain the state of an alarm that you detect outside of AWS IoT SiteWise\.

## Defining an external alarm \(console\)<a name="define-external-alarm-console"></a>

You can use the AWS IoT SiteWise console to define an external alarm on an existing asset model\. To define an external alarm on a new asset model, create the asset model, and then complete these steps\. For more information, see [Creating asset models](create-asset-models.md)\.

**To define an alarm on an asset model**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. <a name="sitewise-choose-models"></a>In the navigation pane, choose **Models**\.

1. Choose the asset model for which to define an alarm\.

1. Choose the **Alarm definitions** tab\.

1. Choose **Add alarm**\.

1. In **Alarm type options**, choose **External alarm**\.

1. Enter a name for your alarm\.

1. \(Optional\) Enter a description for your alarm\.

1. Choose **Add alarm**\.

## Defining an external alarm \(CLI\)<a name="define-external-alarm-cli"></a>

You can use the AWS CLI to define an external alarm on a new or existing asset model\.

To add an external alarm to an asset model, you add an alarm composite model to the asset model\. An external alarm composite model specifies the `EXTERNAL` type and doesn't specify an alarm source property\. The following example composite alarm defines an external temperature alarm\.

```
{
  ...
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
              "defaultValue": "EXTERNAL"
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
        }
      ]
    }
  ]
}
```

For more information about how to add a composite model to a new or existing asset model, see the following:
+ [Creating an asset model \(CLI\)](create-asset-models.md#create-asset-model-cli)
+ [Updating an asset model \(CLI\)](update-assets-and-models.md#update-asset-model-cli)

After you define the external alarm, you can ingest alarm state to assets based on the asset model\. For more information, see [Ingesting external alarm state](ingest-external-alarm-state.md)\.