# Choosing a destination for your source server data<a name="source-destination"></a>

You can use destinations to control where to send your source's incoming data\. You can either send your data to AWS IoT SiteWise, or you can use a AWS IoT Greengrass stream to send your data to a different location\. You configure a different source destination for each source server in your gateway\.
+  AWS IoT SiteWise – Send your source data to AWS IoT SiteWise for storage and processing\. This is the default option\. 
**Note**  
You must choose AWS IoT SiteWise as your source destination if you want to process data from this source at the edge with AWS IoT SiteWise\. For more information about processing data at the edge, see [Process data locally with AWS IoT SiteWise](edge-processing.md)\.
+ AWS IoT Greengrass stream – You choose a custom AWS IoT Greengrass stream to receive your source data\. You can use the AWS IoT Greengrass stream to forward received data to an on\-premises application, or to another AWS IoT service in the AWS Cloud\.

  You can choose an existing AWS IoT Greengrass stream for your source destination, or you can create a new one\. For more information about how to choose a custom AWS IoT Greengrass stream as your destination, see [Configuring data sources](configure-sources.md)\.

The following example shows the required data stream message structure\. All fields are required\. 

```
{
  "alias" : "string",
  "messages" : [
     {
        "name": "string",
        "value": boolean|double|integer|string,
        "timestamp": number,
        "quality": "string"
     }
  ]
}
```

`alias`  
The alias of the data stream\. See the following example\.  

```
/company/windfarm/3/turbine/7/temperature
```

`messages`  
The list of tuples in this batch\. Each tuple contains a `timestamp`, `value`, and `quality`\.

`name`  
The alias of the data stream\. This must match the `alias`\.

`value`  
The type of value contained in this message\. Valid values are `boolean`, `double`, `integer`, or `string`\.

`timestamp`  
The timestamp of the tag data\. This is formatted as the number of milliseconds since the Unix epoch\.

`quality`  
The quality of the tag data\. Valid values are `GOOD`, `BAD`, or `UNCERTAIN`\.