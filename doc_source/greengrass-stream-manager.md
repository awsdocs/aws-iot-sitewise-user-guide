# Ingesting data using AWS IoT Greengrass stream manager<a name="greengrass-stream-manager"></a>

The AWS IoT Greengrass stream manager feature integrates with AWS IoT SiteWise to transfer data from local sources to the AWS Cloud\. You can add a data destination by configuring a local source on the AWS IoT SiteWise console or you can use stream manager in your custom AWS IoT Greengrass solution to ingest data to AWS IoT SiteWise\.

**Note**  
To ingest data from OPC\-UA, Modbus TCP, and Ethernet/IP sources, you can configure a gateway that runs on AWS IoT Greengrass\. For more information, see [Ingesting data using a gateway](gateways.md)\.

For more information about how to configure a destination for local source data, see [Configuring data sources](configure-sources.md)\.

For more information about how to ingest data using stream manager in a custom AWS IoT Greengrass solution, see the following topics in the *AWS IoT Greengrass Version 1 Developer Guide*:
+ [What is AWS IoT Greengrass?](https://docs.aws.amazon.com/greengrass/latest/developerguide/)
+ [Manage data streams on the AWS IoT Greengrass core](https://docs.aws.amazon.com/greengrass/latest/developerguide/stream-manager.html)
+ [Exporting data to AWS IoT SiteWise asset properties](https://docs.aws.amazon.com/greengrass/latest/developerguide/stream-export-configurations.html#export-to-iot-sitewise)