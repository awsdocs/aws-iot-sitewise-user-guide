# Configuring data sources<a name="configure-sources"></a>

After you set up a gateway, you can configure data sources so that your gateway can ingest data from local servers to AWS IoT SiteWise\. Each source represents a local server, such as an OPC\-UA server, that your gateway connects and retrieves industrial data streams\. For more information about setting up a gateway, see [Configuring a gateway](configure-gateway.md)\.

**Note**  
AWS IoT SiteWise restarts your gateway each time you add or edit a source\. Your gateway won't ingest data while it's restarting\. The time to restart your gateway depends on the number of tags on your gateway's sources\. Restart time can range from a few seconds \(for a gateway with few tags\) to several minutes \(for a gateway with many tags\)\.

After you create sources, you can associate your data streams with asset properties\. For more information about how to create and use assets, see [Modeling industrial assets](industrial-asset-models.md) and [Mapping industrial data streams to asset properties](connect-data-streams.md)\.

You can view CloudWatch metrics to verify that a data source is connected to AWS IoT SiteWise\. For more information, see [Gateway metrics](monitor-cloudwatch-metrics.md#gateway-metrics)\.

Currently, AWS IoT SiteWise supports the following data source protocols:
+ [OPC\-UA](https://en.wikipedia.org/wiki/OPC_Unified_Architecture) – A machine\-to\-machine \(M2M\) communication protocol for industrial automation\.
+ [Modbus TCP](https://en.wikipedia.org/wiki/Modbus) – A data communications protocol used to interface with programmable logic controllers \(PLCs\)\.
+ [Ethernet/IP \(EIP\)](https://en.wikipedia.org/wiki/EtherNet/IP) – An industrial network protocol that adapts the Common Industrial Protocol \(CIP\) to standard Ethernet\.

**Note**  
Gateways running on AWS IoT Greengrass V2 currently don't support Modbus TCP and Ethernet IP sources\.

**Topics**
+ [Configure an OPC\-UA source](configure-opcua-source.md)
+ [Configure a Modbus TCP source](configure-modbus-source.md)
+ [Configure an Ethernet/IP \(EIP\) source](configure-eip-source.md)
+ [Choosing a destination for your source server data](source-destination.md)
+ [Upgrading a connector](upgrade-gateway.md)