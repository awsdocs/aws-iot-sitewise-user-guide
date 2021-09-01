# Enabling edge data processing<a name="edge-processing"></a>

 You can use AWS IoT SiteWise to collect, organize, process, and monitor equipment data locally\. You can use AWS IoT SiteWise so that you can use asset models and SiteWise Monitor on your local data\. You can process your data locally and send it to AWS IoT SiteWise, or load it  into on\-premise applications by using AWS IoT SiteWise API operations\. 

Because you can use AWS IoT SiteWise to process and route your data locally, you can choose to send only aggregated data to the AWS Cloud\. Use this feature to optimize your bandwidth usage and cloud storage costs\. 

**Note**  
AWS IoT SiteWise retains your edge data on your gateways up to 30 days\. The retention of your data is dependent on your device and the available disk space\.
30 days after your gateway has been disconnected from the AWS Cloud, the data processing pack is automatically disabled\.

**Topics**
+ [Edge processing prerequisites](edge-setup.md)
+ [Setting up edge capability](using-sitewise-edge.md)