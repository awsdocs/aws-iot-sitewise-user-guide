# Configure an Ethernet/IP source \(console\)<a name="config-eip-console"></a>

**To configure an Ethernet/IP source**

1. Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the left navigation pane, choose **Gateways**\.

1. On the gateway you want to create a source for, choose **Manage**, and then choose **View details**\.  
![\[AWS IoT SiteWise "Gateways" page screenshot with "View details" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/gateway-view-details-console.png)

1. Choose **New source** in the upper\-right corner\.

1. For **Protocol options**, choose **Ethernet/IP \(EIP\)**\.

1. For **EtherNet/IP source configuration**, enter a **Name** for the source\.

1. For **IP address**, enter the IP address for the data source server\.

1. \(Optional\) Enter the **Port** for the source server\.

1. For **Minimum inter\-request duration**, enter the time interval between subsequent requests sent to your server\. Your gateway automatically calculates the minimum allowable interval based on your device and the number of registers you have\. 

1. For **Property groups**, enter a **Name**\.

1. For **Properties**:

   1. For **Tag**, enter the property alias for your register set\. For example, **boiler\.inlet\.temperature\.value**\.

   1. For **Destination data type**, choose the AWS IoT SiteWise data type that you want your data to be converted to\. The default is **String**\.

1. For **Scan rate**, update the rate at which you want the gateway to read your registers\. AWS IoT SiteWise automatically calculates the minimum allowable scan rate for your gateway\.

1. \(Optional\) For **Destination**, choose where the source data is sent\. By default, your source sends data to AWS IoT SiteWise\.You can use a AWS IoT Greengrass stream to export your data to a local destination or to the AWS Cloud instead\. 
**Note**  
You must choose AWS IoT SiteWise as your source destination if you want to process data from this source at the edge with AWS IoT SiteWise\. For more information about processing data at the edge, see [Process data locally with AWS IoT SiteWise](edge-processing.md)\.

   To send your data to another destination:

   1. For **Destination options**, choose **Other destinations**\.

   1. For **Greengrass stream name**, enter the exact name of your AWS IoT Greengrass stream\.
**Note**  
 You can use a stream that you've already created, or you can create a new AWS IoT Greengrass stream to export your data\. If you want to use an existing stream, you must enter the exact name of the stream or a new stream will be created\.   
For more information about working with AWS IoT Greengrass streams, see [Manage data streams](https://docs.aws.amazon.com/greengrass/latest/developerguide/stream-manager.html) in the AWS IoT Greengrass developer guide\.

1. Choose **Add source**\.

   AWS IoT SiteWise deploys the gateway configuration to your AWS IoT Greengrass core\. You don't need to manually trigger a deployment\.