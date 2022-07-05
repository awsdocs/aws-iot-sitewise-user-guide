# Setting up edge capability<a name="using-sitewise-edge"></a>

To use edge processing, you must configure your AWS IoT SiteWise gateway and asset model for the edge\. Your gateway ingests data from your source server, and sends that data to the destination of your choice\. Your asset model controls specifies where your assets are stored and computed\. 

**Note**  
Before you begin, make sure that you meet the [Edge processing prerequisites](edge-setup.md)\.

You must complete the following steps to use edge processing\. You don't need to complete these steps in order, because AWS IoT SiteWise automatically syncs your gateway with the AWS cloud every 10 minutes\.

For more information about getting started with edge processing, see [Introducing AWS IoT SiteWise](https://aws-blogs-prod.amazon.com/iot/introducing-aws-iot-sitewise-edge/) in the AWS official blog\.
+  **Add the data processing pack to your gateway** – Add the data processing pack so that your gateway can communicate with all asset models that you configured for the edge\. You add this pack when you add your gateway to AWS IoT SiteWise, or when you edit an existing gateway\. For more information about your AWS IoT SiteWise gateway, see [Ingesting data using a gateway](gateways.md)\. 

  After you add the data processing pack to your gateway, you must configure and add the AWS IoT SiteWise Data Processor connector to your AWS IoT Greengrass group\. For more information about adding the AWS IoT SiteWise Data Processor connector to your AWS IoT Greengrass group, see [the configuration step](configure-gateway.md#setup-swe-connector) in [Adding the gateway to AWS IoT SiteWise](configure-gateway.md#add-gateway)\. 
**Note**  
You need v9 of the data collection pack to use the data processing pack on your gateway\.
+ **Configure your source destination to AWS IoT SiteWise** – This specifies where your gateway source sends your data\. You configure this when you add a source to your gateway, or when you edit an existing source\. To process data at the edge, you must choose AWS IoT SiteWise as your source destination\. For more information about source destinations, see [Choosing a destination for your source server data](source-destination.md)\. 
+ **Configure your asset model for the edge** – Your asset model edge configuration specifies where your assets properties are computed\. You can compute all properties at the edge, or you can configure your asset model properties separately\.

  Asset model properties include metrics, transforms, and measurements:
  + Metrics are the asset's aggregated data over a specified period of time\. You can compute new metrics by using existing metric data\. AWS IoT SiteWise always sends your metrics to the AWS Cloud for long\-term storage\. AWS IoT SiteWise computes metrics on the AWS Cloud by default\. You can configure your asset model to compute your metrics at the edge\. AWS IoT SiteWise sends processed results to the AWS Cloud\.
  + Transforms are mathematical expressions that map an asset property's data points from one form to another\. Transforms can use metrics as input data and must be computed and stored at the same location as their inputs\. If you configure a metric input to compute at the edge, AWS IoT SiteWise also computes its associated transform at the edge\. 
  + Measurements are formatted as raw data that your device collects and sends to the AWS Cloud by default\. You can configure your asset model to store this data on your local device\.

  For more information about asset properties, see [Defining data properties](asset-properties.md)\.

   After you create your asset model, you can then configure it for the edge\. For more information about configuring your asset model for the edge, see [Creating an asset model \(console\)](create-asset-models.md#create-asset-model-console)\. 
**Note**  
Asset models and dashboards are automatically synced between the AWS Cloud and your AWS IoT SiteWise gateway every 10 minutes\. You can also sync manually from the local gateway application\.
