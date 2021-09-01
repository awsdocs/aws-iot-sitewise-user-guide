# Configure a Modbus TCP source \(console\)<a name="config-modbus-console"></a>

**To configure a Modbus TCP source**

1. Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the left navigation pane, choose **Gateways**\.

1. On the gateway you want to create a source for, choose **Manage**, and then choose **View details**\.  
![\[AWS IoT SiteWise "Gateways" page screenshot with "View details" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/gateway-view-details-console.png)

1. Choose **New source** in the upper\-right corner\.

1. For **Protocol options**, choose **Modbus TCP**\.

1. For **Modbus TCP source configuration**, enter a **Name** for the source\.

1. For **IP address**, enter the IP address for the data source server\.

1. \(Optional\) Enter the **Port** and **Unit ID** for the source server\.

1.  \(Optional\) For **Minimum inter\-request duration**, enter the time interval between subsequent requests sent to your server\. Your gateway automatically calculates the minimum allowable interval based on your device and the number of registers you have\. 

1. For **Property groups**, enter a **Name**\.

1. For **Properties**:

   1. For **Tag**, enter a property alias for your register set\. For example, **TT\-001**\.

   1. For **Register address**, enter the register address that starts the register set\.

   1. For **Source data type**, choose the Modbus TCP data type you want to convert data from\. This defaults to **Hex dump**\.
**Note**  
The source data type you choose determines the data size, destination data type, and swap mode you can choose\. For more information, see [Configure a Modbus TCP source](configure-modbus-source.md)\. 

   1. For **Data size**, enter the number of registers to read when starting from the **Register address**\. This is determined by the source data type you choose for this source\.

   1. For **Destination data type**, choose the AWS IoT SiteWise data type that you want your data to be converted to\. The default is **String**\. The destination type must be compatible with the source data type you choose for this source\. For more information, see [Configure a Modbus TCP source](configure-modbus-source.md)\.

   1. For **Swap mode**, choose the data swap mode you want to use to read data from your register set\. The swap mode must be compatible with the source data type you choose for this source\. For more information, see [Configure a Modbus TCP source](configure-modbus-source.md)\.

1. For **Scan rate**, update the rate at which you want the gateway to read your registers\. AWS IoT SiteWise automatically calculates the minimum allowable scan rate for your gateway\.

1. \(Optional\) For **Destination**, choose where the source data is sent\. By default, your source sends data to AWS IoT SiteWise\.You can use a AWS IoT Greengrass stream to export your data to a local destination or to the AWS Cloud instead\. 
**Note**  
You must choose AWS IoT SiteWise as your source destination if you want to process data from this source at the edge with AWS IoT SiteWise\. For more information about processing data at the edge, see [Enabling edge data processing](edge-processing.md)\.

   To send your data to another destination:

   1. For **Destination options**, choose **Other destinations**\.

   1. For **Greengrass stream name**, enter the exact name of your AWS IoT Greengrass stream\.
**Note**  
 You can use a stream that you've already created, or you can create a new AWS IoT Greengrass stream to export your data\. If you want to use an existing stream, you must enter the exact name of the stream or a new stream will be created\.   
For more information about working with AWS IoT Greengrass streams, see [Manage data streams](https://docs.aws.amazon.com/greengrass/latest/developerguide/stream-manager.html) in the AWS IoT Greengrass developer guide\.

1. Choose **Add source**\.

   AWS IoT SiteWise deploys the gateway configuration to your AWS IoT Greengrass core\. You don't need to manually trigger a deployment\.