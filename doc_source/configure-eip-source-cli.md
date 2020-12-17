# Configure an Ethernet/IP source \(CLI\)<a name="configure-eip-source-cli"></a>

You can define EIP data sources in a gateway capability\. You must define all of your EIP sources in a single capability configuration\.

For more information about defining sources with the AWS CLI, see [Configuring data sources \(AWS CLI\)](configure-source-cli.md)\.

**Note**  
You must install the AWS IoT SiteWise connector to use an Ethernet IP source\.

This capability has the following versions\.


| Version | Namespace | 
| --- | --- | 
| 1 | iotsitewise:eipcollector:1 | 

## EIP capability configuration parameters<a name="eip-source-parameters-cli"></a>

When you define EIP sources in a capability configuration, you must specify the following information in the `capabilityConfiguration` JSON document:

`sources`  
A list of EIP source definition structures that each contain the following information:    
`name`  
A unique, friendly name for the source\. This can be up to 256 characters\.  
`destinationPathPrefix`  
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
The IP address of the EIP source\.  
`port`  
\(Optional\) The port of the EIP source\. Accepted values are numbers between 1 and 65535\.  
`minimumInterRequestDuration`  
\(Optional\) The minimum duration between each request in milliseconds\.  
`propertyGroups`  
The list of property groups that define the tag definition requested by the protocol\. Each source can have one property group\.    
`name`  
The name of the property group\. This should be a unique identifier with a maximum length of 256 characters\.  
`tagPathDefinitions `  
The list of structures specifying the data to collect from the Ethernet/IP device and how to transform it for output\.    
`type`  
The type of the `tagPathDefinition`\. For example, `EIPTagPath`\.  
`path`  
The path of the `tagPathDefinition`\. Each tag in a path can be a maximum length of 40 characters and can start with a letter or an underscore\. Tags can’t contain consecutive or trailing underscores\. The path is prefixed with any value of destinationPathPrefix\.  
`dstDataType`  
The data type to output the tag data\. Accepted values are `integer`, `double`, `string`, and `boolean`\.  
`scanMode`  
Defines the scan mode behavior and configurable parameters for the source\.    
`type`  
The type of the scan mode behavior\. Accepted values are `POLL`\.  
`rate`  
The rate in milliseconds that the connector should read tags from the Ethernet/IP source\.