# Interacting with other AWS services<a name="interact-with-other-services"></a>

AWS IoT SiteWise can publish asset data to the AWS IoT MQTT publish\-subscribe message broker, so that you can interact with your asset data from other AWS services\. AWS IoT SiteWise assigns each asset property a unique MQTT topic that you can use to route your asset data to other AWS services using AWS IoT Core rules\. For example, you can configure AWS IoT Core rules to do the following tasks:
+ Identify equipment failure and notify appropriate personnel by sending data to [AWS IoT Events](https://docs.aws.amazon.com/iotevents/latest/developerguide/)\.
+ Historize select asset data for use in external software solutions by sending data to [Amazon DynamoDB](https://docs.aws.amazon.com/dynamodb)\.
+ Generate weekly reports by triggering an [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/) function\.

You can follow a tutorial that walks through the steps required to set up a rule that stores property values in DynamoDB\. For more information, see [Publishing property value updates to Amazon DynamoDB](publish-to-amazon-dynamodb.md)\.

For more information about how to configure a rule, see [Rules](https://docs.aws.amazon.com/iot/latest/developerguide/iot-rules.html) in the *AWS IoT Developer Guide*\.

You can also consume data from other AWS services back into AWS IoT SiteWise\. To ingest data through the AWS IoT SiteWise rule action, see [Ingesting data using AWS IoT Core rules](iot-rules.md)\.

**Topics**
+ [Understanding asset properties' MQTT topics](#mqtt-topics)
+ [Working with asset property notifications](property-notifications.md)

## Understanding asset properties' MQTT topics<a name="mqtt-topics"></a>

Every asset property has a unique MQTT topic path in the following format\.

```
$aws/sitewise/asset-models/assetModelId/assets/assetId/properties/propertyId
```

**Note**  
AWS IoT SiteWise doesn't support the `#` \(multi\-level\) topic filter wildcard in the AWS IoT Core rules engine\. You can use the `+` \(single\-level\) wildcard\. For example, you can use the following topic filter to match all updates for a particular asset model\.  

```
$aws/sitewise/asset-models/assetModelId/assets/+/properties/+
```
To learn more about topic filter wildcards, see [Topics](https://docs.aws.amazon.com/iot/latest/developerguide/topics.html) in the *AWS IoT Core Developer Guide*\.