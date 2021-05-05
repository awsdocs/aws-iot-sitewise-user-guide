# Managing your AWS IoT SiteWise gateway<a name="manage-gateways"></a>

 You can use the AWS IoT SiteWise console or the local gateway application to monitor your AWS IoT SiteWise gateway\. 

You can also use Amazon CloudWatch to view detailed metrics for your gateway device\. For more information, see [Monitoring AWS IoT SiteWise with Amazon CloudWatch metrics](monitor-cloudwatch-metrics.md)\.

## Managing your gateway with the local gateway application<a name="edge-console"></a>

 You can use the local gateway application to monitor the state of your gateway locally without internet connectivity\. The local gateway application provides the following monitoring and management options: 
+ View device resource usage\.
+ View services running locally\. 
+ View asset model instances deployed to the device and the last value collected or computed for asset properties\.
+ View SiteWise Monitor portals\.
+ Sync resources with the AWS Cloud\.
+ Remote restart of gateway software\. This restarts all software services and syncs all asset models with the AWS Cloud\.

For more information about using the local gateway application, see [Monitor data at the edge](using-opshub.md)\.

## Managing your gateway with the AWS IoT SiteWise console<a name="cloud-console"></a>

You can use the AWS IoT SiteWise console to configure, update, and monitor all gateways in your AWS account\. 

You can view your AWS IoT SiteWise gateways by navigating to the **Gateways** page in the AWS IoT SiteWise console\. The AWS IoT SiteWise console provides the following monitoring and management options:
+ Update data source configuration and configure additional data sources
+ View the number of data points ingested per data source
+ Add data packs to your gateway
+ View the connectivity status of your gateways
+ View the gateway sync status of resources and configuration changes