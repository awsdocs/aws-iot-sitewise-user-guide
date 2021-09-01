# Configure a Modbus TCP source<a name="configure-modbus-source"></a>

You can use the AWS IoT SiteWise console or a gateway capability to define and add a Modbus TCP source to your gateway\. This source represents a local Modbus TCP server\.

**Note**  
Gateways running on AWS IoT Greengrass V2 currently don't support Modbus TCP sources\.
You must install the AWS IoT SiteWise connector to use a Modbus TCP source\.

You can use the Modbus TCP source to convert the data type from your source into a different data type when it's received on your gateway\. The source data type determines the data types that you can choose for your destination data\. You can also choose to swap bytes using the Modbus TCP source\. The following table provides more information on the source data types, destination data types, and swap modes that are compatible\. 

For more information about swap modes, see the [How Real \(Floating Point\) and 32\-bit Data is Encoded in Modbus RTU Messages](https://store.chipkin.com/articles/how-real-floating-point-and-32-bit-data-is-encoded-in-modbus-rtu-messages) article on Modbus message encoding\.


| Source data type | Compatible destination data types | Compatible swap modes | Compatible connector versions | 
| --- | --- | --- | --- | 
| ASCII | String | noSwap | 2 | 
| UTF8 | String | noSwap | 2 | 
| ISO8859 | String | noSwap | 2 | 
| Int16 | Integer, Double, String | noSwap | 1 and 2 | 
| Int32 | Integer, Double, String | noSwap, byteWordSwap, byteSwap, wordSwap | 1 and 2 | 
| Float | Double, String | noSwap, byteWordSwap, byteSwap, wordSwap | 1 and 2 | 
| Boolean | Boolean | noSwap | 1 and 2 | 
| Hex\-dump | String | noSwap | 1 and 2 | 

**Topics**
+ [Configure a Modbus TCP source \(console\)](config-modbus-console.md)
+ [Configure a Modbus TCP source \(CLI\)](configure-modbus-tcp-source-cli.md)