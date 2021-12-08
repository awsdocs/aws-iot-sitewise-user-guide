# Setting up SiteWise gateways \(Greengrass V1\)<a name="gateways-ggv1"></a>

**Note**  
Gateways running on AWS IoT Greengrass V1 are available only if you started using this feature before July 29, 2021\. Otherwise, you [set up gateways running on AWS IoT Greengrass V2](configure-gateway-ggv2.md)\.

You can send industrial data to AWS IoT SiteWise using an AWS IoT SiteWise gateway to upload data from servers\. The gateway serves as the intermediary between AWS IoT SiteWise and your data servers\. AWS IoT SiteWise provides AWS IoT Greengrass connectors that you can deploy on any platform that can run AWS IoT Greengrass to set up a gateway\. AWS IoT SiteWise supports linking with [OPC\-UA](https://en.wikipedia.org/wiki/OPC_Unified_Architecture), [Modbus TCP](https://en.wikipedia.org/wiki/Modbus), and [Ethernet/IP](https://en.wikipedia.org/wiki/EtherNet/IP) server protocols\.

**Topics**
+ [Ingesting data using a gateway](gateways.md)
+ [Enabling edge data processing](edge-processing.md)