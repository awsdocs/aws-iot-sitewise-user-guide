# Managing data streams \(console\)<a name="manage-data-streams-console"></a>

You can use the AWS IoT SiteWise console to manage your data streams\.

**To manage data streams \(console\)**

1. <a name="sitewise-open-console"></a>Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the navigation pane, choose **Data streams**\.

1. \(Optional\) In the **Data stream** table, you can filter data streams in the following ways\.
   + Choose **Alias prefix** or **Asset ID**\.
     + **Alias prefix** – The alias prefix of the data stream\. You might choose this option if your target data streams have an alias prefix\.
     + **Asset ID** – The ID of the asset in which the asset property was created\. You might choose this option if your target data streams are associated with an asset property\.
   + Choose **All data streams**, **Associated data streams**, or **Disassociated data streams**\.
     + **All data streams** – Data streams that are associated with or not associated with an asset property\. 
     + **Associated data streams** – Data streams that are associated with an asset property\.
     + **Disassociated data streams** – Data streams that aren't associated with an asset property\.

1. Choose the data streams that you're managing\. AWS IoT SiteWise displays the data streams that you chose in a graph at the bottom of the page\. If you choose more than 10, the graph will display only the first 10 you chose\.

1. \(Optional\) You can configure the graph in the following ways\.

   1. For **Aggregation function**, choose one of the following\.
      + **Data point count** – The total number of data points for the given variables over the current time interval\.
      + **Average** – The mean of the given variables' values over the current time interval\.
      + **Sum** – The sum of the given variables' values over the current time interval\.
      + **Minimum** – The minimum of the given variables' values over the current time interval\.
      + **Maximum** – The maximum of the given variables' values over the current time interval\.

      For more information, see [Aggregation functions](expression-aggregation-functions.md)\.

   1. For **Time ranges**, choose one of the following\.
      + **Last 1 hour** – The graph displays aggregated data over the last hour\.
      + **Last 2 hours** – The graph displays aggregated data over the last two hours\.
      + **Last 3 hours** – The graph displays aggregated data over the last three hours\.
      + **Last 4 hours** – The graph displays aggregated data over the last four hours\.

   1. For **Time interval**, choose one of the following\.
      + **1 minute** – Aggregates data every minute over the specified time range\.
      + **1 hour** – Aggregates data every hour over the specified time range\.

1. Choose **Manage data streams**\.  
![\[AWS IoT SiteWise "Data stream list" page screenshot.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/data-stream-list.png)

1. In the **Update data stream associations** section, in the **Measurement** column, do one of the following\.
   + If the data stream is associated with a measurement, delete the association by choosing the close icon\.
   + If the data stream isn't associated with a measurement, choose **Choose measurement**\.

1. In the **Choose a measurement** table, navigate to the target asset, and then choose the measurement that you're associating\.

1. \(Optional\) In the **Update asset property aliases** section, enter a unique alias for each measurement\.

1. Choose **Update**\.  
![\[AWS IoT SiteWise "Manage data streams" page screenshot.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/manage-data-streams.png)

The **Status** column can be one of the following values\.
+ **Pending** – You're updating the data stream association or asset property alias\.
+ **Submit** – Your change to the association or asset property alias is saved\.
+ **Error** – AWS IoT SiteWise couldn't process your request to update the data stream association or the alias for the measurement\.
+ **Success** – You successfully updated the data stream association or the alias for the measurement\.