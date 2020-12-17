# Configure an OPC\-UA source \(console\)<a name="config-opcua-source-console"></a>

**To configure an OPC\-UA source using the AWS IoT SiteWise console**

1. Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the navigation pane, choose **Gateways**\.

1. On the gateway that you want to create a source for, choose **Manage**, and then choose **View details**\.  
![\[AWS IoT SiteWise "Gateways" page screenshot with "View details" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/gateway-view-details-console.png)

1. Choose **New source** in the upper\-right corner\.

1. For **Protocol options**, choose **OPC\-UA**\.

1. For **OPC\-UA source configuration**, enter a **Name** for the source\.

1. For **IP address or hostname**, enter the local endpoint of the data source server\. For example, your local endpoint might look like **opc\.tcp://203\.0\.113\.0:49320**\.

1. \(Optional\) Enter a **Data stream prefix**\. The gateway adds this prefix to all data streams from this source\. Use a data stream prefix to distinguish between data streams that have the same name from different sources\. Each data stream should have a unique name within your account\.

1. Choose a **Message security mode** for connections and data in transit between your source server and your gateway\. This field is the combination of the OPC\-UA security policy and message security mode\. You must choose the same security policy and message security mode that you specified for your OPC\-UA server\.

   Choose the security policy from the following options:
   + **None** – The gateway doesn't secure connections to the OPC\-UA source\. We recommend that you choose a different security policy\.
   + **Basic256Sha256** – The **Basic256Sha256** security policy\.
   + **Aes128\_Sha256\_RsaOaep** – The **Aes128\_Sha256\_RsaOaep** security policy\.
   + **Aes256\_Sha256\_RsaPss** – The **Aes256\_Sha256\_RsaPss** security policy\.
   + **Basic128Rsa15** – \(Deprecated\) The **Basic128Rsa15** security policy is deprecated in the OPC\-UA specification because it's no longer considered secure\. We recommend that you choose a different security policy\. For more information, see [Basic128Rsa15](http://opcfoundation.org/UA-Profile/UA/SecurityPolicy%23Basic128Rsa15)\.
   + **Basic256** – \(Deprecated\) The **Basic256** security policy is deprecated in the OPC\-UA specification because it's no longer considered secure\. We recommend that you choose a different security policy\. For more information, see [Basic256](http://opcfoundation.org/UA-Profile/UA/SecurityPolicy%23Basic256)\.

   Except for the **None** option, each security policy has two options for message security mode:
   + **Sign** – The data in transit between the gateway and the source is signed but not encrypted\.
   + **Sign and encrypt** – The data in transit between the gateway and the source is signed and encrypted\.
**Important**  
If you choose a message security mode other than **None**, you must enable your source server to trust the gateway\. For more information, see [Enabling your source servers to trust the gateway](enable-source-trust.md)\.

1. If your source requires authentication, choose an AWS Secrets Manager secret from the **Authentication configuration** list\. The gateway uses the authentication credentials in this secret when it connects to this source\. You must attach secrets to your gateway's IoT SiteWise connector to use them for source authentication\. For more information, see [Configuring source authentication](configure-source-authentication.md)\.
**Tip**  
Your data server might have an option named **Allow anonymous login**\. If this option is **Yes**, then your source doesn't require authentication\.

1. For **Property groups**, enter a **Name**\.

1. For **Properties**:

   1. \(Optional\) For **Node paths**, add OPC\-UA node filters to limit which OPC\-UA paths are uploaded to AWS IoT SiteWise\. You can use node filters to reduce your gateway's startup time and CPU usage by only including paths to data that you model in AWS IoT SiteWise\. By default, gateways upload all OPC\-UA paths except those that start with `/Server/`\. To define OPC\-UA node filters, you can use node paths and the `*` and `**` wildcard characters\. For more information, see [Using OPC\-UA node filters](opc-ua-node-filters.md)\.

   1. For **Scan mode**, choose the mode that you want AWS IoT SiteWise to use to collect your data\. For more information about scan mode, see [Filter data ingestion ranges with OPC\-UA](opcua-data-acquisition.md)\.

   1. For **Scan rate**, update the rate that want the gateway to read your registers\. AWS IoT SiteWise automatically calculates the minimum allowable scan rate for your gateway\.

   1.  \(Optional\) Configure a **Deadband setting** for your source\. This controls what data your source sends to your AWS IoT SiteWise, and what data it discards\. For more information about the deadband setting, see [Filter data ingestion ranges with OPC\-UA](opcua-data-acquisition.md)\. 

1. \(Optional\) For **Destination**, choose where the source data is sent\. By default, your source sends data to AWS IoT SiteWise\. You can use a AWS IoT Greengrass stream to export your data to a local destination or to the AWS Cloud instead\. 
**Note**  
You must choose AWS IoT SiteWise as your source destination if you want to process data from this source at the edge with AWS IoT SiteWise\. For more information about processing data at the edge, see [Process data locally with AWS IoT SiteWise](edge-processing.md)\.

   To send your data to another destination:

   1. For **Destination options**, choose **Other destinations**\.

   1. For **Greengrass stream name**, enter the exact name of your AWS IoT Greengrass stream\.
**Note**  
 You can use a stream that you've already created, or you can create a new AWS IoT Greengrass stream to export your data\. If you want to use an existing stream, you must enter the exact name of the stream or a new stream will be created\.   
For more information about working with AWS IoT Greengrass streams, see [Manage data streams](https://docs.aws.amazon.com/greengrass/latest/developerguide/stream-manager.html) in the *AWS IoT Greengrass Developer Guide*\.

1. Choose **Add source**\.

   AWS IoT SiteWise deploys the gateway configuration to your AWS IoT Greengrass core\. You don't need to manually trigger a deployment\.