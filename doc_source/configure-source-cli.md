# Configuring data sources \(AWS CLI\)<a name="configure-source-cli"></a>

You can use the AWS IoT SiteWise API and AWS Command Line Interface to add sources to your gateway\. You define sources in gateway capabilities\. A gateway capability represents a software feature that runs on the gateway, such as the capability to collect industrial data from OPC\-UA sources\.

Gateway capabilities have the following components:
+ A configuration – A JSON document that defines all of the data sources for a capability\.
+ A namespace – A unique string that identifies the type and version of a capability\. For example, the OPC\-UA source capability namespace is `iotsitewise:opcuacollector:version`, where *version* is the version of the OPC\-UA capability\. All OPC\-UA sources are defined in one capability with this namespace\.
+ A synchronization status – A status that indicates if a capability is synchronized between the AWS Cloud and the gateway\. The sync status can be one of the following:
  + `IN_SYNC` – The gateway is running the capability configuration\.
  + `OUT_OF_SYNC` – The gateway hasn't received the capability configuration\.
  + `SYNC_FAILED` – The gateway rejected the capability configuration\.

  After you update a capability configuration, its sync status is `OUT_OF_SYNC` until the gateway receives and applies or rejects the updated configuration\.

Use the following operations to query and update your gateway sources and capability configurations:
+ [DescribeGateway](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeGateway.html) – Retrieves information about a specific gateway\. The response includes a list of capability summaries, including capability namespaces\.
+ [DescribeGatewayCapabilityConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_DescribeGatewayCapabilityConfiguration.html) – Retrieves the configuration of a specific capability\. Use this operation to retrieve a capability configuration to update\.
+ [ListGateways](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_ListGateways.html) – Lists information about all gateways\. The response includes a list of capability summaries for each gateway, including capability namespaces\.
+ [UpdateGatewayCapabilityConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateGatewayCapabilityConfiguration.html) – Updates a gateway capability configuration or defines a new capability configuration\. This operation identifies capabilities by a capability namespace\. If you provide a namespace that already exists, this operation updates the capability for that namespace\. Otherwise, this operation creates a new capability\.
**Warning**  
The [UpdateGatewayCapabilityConfiguration](https://docs.aws.amazon.com/iot-sitewise/latest/APIReference/API_UpdateGatewayCapabilityConfiguration.html) operation overwrites the existing capability configuration with the configuration that you provide in the payload\. To avoid deleting your capability's configuration, you must add to the existing configuration when you update the capability\.<a name="gateway-capability-list"></a>

**Gateway capabilities**
+ [Configure an OPC\-UA source \(CLI\)](configure-opc-ua-source-cli.md)
+ [Configure a Modbus TCP source \(CLI\)](configure-modbus-tcp-source-cli.md)
+ [Configure an Ethernet/IP source \(CLI\)](configure-eip-source-cli.md)