# Configure a Modbus TCP source \(CLI\)<a name="configure-modbus-tcp-source-cli"></a>

You can define Modbus TCP data sources in a gateway capability\. You must define all of your Modbus TCP sources in a single capability configuration\.

For more information about defining sources with the AWS CLI, see [Configuring data sources \(AWS CLI\)](configure-source-cli.md)\.

**Note**  
You must install the AWS IoT SiteWise connector to use a Modbus TCP source\.

This capability has the following versions\.


| Version | Namespace | 
| --- | --- | 
| 1 | iotsitewise:modbuscollector:1 | 

## Modbus TCP capability configuration parameters<a name="modbus-source-parameters-cli"></a>

When you define Modbus TCP sources in a capability configuration, you must specify the following information in the `capabilityConfiguration` JSON document:

`sources`  
A list of Modbus\-TCP source definition structures that each contain the following information:    
`name`  
A unique, friendly name for the source\.  
`measurementDataStreamPrefix`  
\(Optional\) A string to prepend to all data streams from the source\. The gateway adds this prefix to all data streams from this source\. Use a data stream prefix to distinguish between data streams that have the same name from different sources\. Each data stream should have a unique name within your account\.  
`destination`  
A destination structure that contains the following information:    
`type`  
The type of the destination\.  
`streamName`  
The name of the AWS IoT Greengrass stream\.  
`streamBufferSize`  
The size of the stream buffer\.  
`endpoint`  
An endpoint structure that contains the following information:    
`ipAddress`  
The IP address of the Modbus TCP source\.  
`port`  
\(Optional\) The port of the Modbus TCP source\.  
`unitId`  
\(Optional\) The unitId\. This defaults to a value of 1\.  
`minimumInterRequestDuration`  
The minimum duration between each request in milliseconds\.  
`propertyGroups`  
The list of property groups that define the tag definition requested by the protocol\.    
`name`  
The name of the property group\. This should be a unique identifier\.  
`tagPathDefinitions `  
The location of the measurement within the source\. For example, the byte and word order, address, and transformation type\. The structure of each `MeasurementPathDefinition` is defined by the connector\.  
`scanMode`  
Defines the scan mode behavior and configurable parameters for the source\.