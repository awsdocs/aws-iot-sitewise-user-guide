# Upgrading packs<a name="update-gateway-packs"></a>

Gateways use different packs to determine how to collect and process your data\. You can use the AWS IoT SiteWise console to upgrade packs\.

**To upgrade packs \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the navigation pane, choose **Gateways**\.

1. In the **Gateways** list, choose the gateway with the packs you want to upgrade\.

1. On the gateway summary page, choose **Updates**\.
**Note**  
You can only upgrade packs that are enabled\. To find the list of packs that are enabled for this gateway, choose **Overview**, and then see the **Edge capabilities** section\.

1. In the **Pack updates** section, do one of the following\.
   + For **OPC\-UA collector**, choose **Version 2\.0\.3**, and then choose **Deploy**\.
   + For **Publisher**, choose **Version 2\.0\.2**, and then choose **Deploy**\.
   + For **Data processing pack**, choose **Version 2\.0\.14**, and then choose **Deploy**\.
**Note**  
We strongly recommend that you use the latest version of each pack\.

1. To confirm the deployment, choose **Deploy**\. In the **Deployment** column in the **Gateways** list, you'll see **Completed**\. If you don't see an update to the deployment status, refresh the page\.
**Note**  
Deploy only one pack at a time\. If you deploy multiple packs at the same time, only the last pack that you chose will get deployed\.


If you're experiencing problems upgrading the packs, see [Unable to deploy packs to AWS IoT SiteWise Edge gateways](troubleshooting-gateway.md#gateway-issue-ggv2-packs)\.