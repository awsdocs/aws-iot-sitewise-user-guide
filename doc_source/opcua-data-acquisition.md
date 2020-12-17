# Filter data ingestion ranges with OPC\-UA<a name="opcua-data-acquisition"></a>

You can control the way you ingest data with an OPC\-UA source by using scan mode and deadband ranges\. These features let you control what kind of data to ingest, and how and when your server and gateway exchange this information\.

## Control data collection frequency with Scan mode<a name="opcua-scanmode"></a>

You can configure your OPC\-UA scan mode to control the way you collect data from your OPC\-UA source\. You can choose subscription or polling mode\.
+ Subscription mode – The OPC\-UA source collects data to send to your gateway at the frequency defined by your scan rate\. The server only sends data when the value has changed, so this is the maximum frequency your gateway receives data\.
+ Polling mode – Your gateway polls the OPC\-UA source at a set frequency defined by your scan rate\. The server sends data regardless of whether the value has changed, so your gateway always receives data at this interval\.
**Note**  
The polling mode option overrides your deadband settings for this source\.

## Filter OPC\-UA data ingestion with deadband ranges<a name="opcua-deadbanding"></a>

 You can apply a deadband to your OPC\-UA source property groups to filter out and discard certain data instead of sending it to the AWS Cloud\. A deadband specifies a window of expected fluctuations in the incoming data values from your OPC\-UA source\. If the values fall within this window, your OPC\-UA server won't send it to the AWS Cloud\. You can use deadband filtering to reduce the amount of data you're processing and sending to the AWS Cloud\. To learn how to set up OPC\-UA sources for your gateway, see [Configuring data sources](configure-sources.md)\.

**Note**  
 Your server deletes all data that falls inside the window specified by your deadband\. You can't recover this discarded data\.

### Types of deadbands<a name="deadband-types"></a>

 You can specify two types of deadbands for your OPC\-UA server property group\. These let you choose how much data is sent to the AWS Cloud, and how much is discarded\.
+ Percentage – You specify a window using a percentage of expected fluctuation in the measurement value\. The server calculates the exact window from this percentage, and sends data to the AWS Cloud that exceeds falls outside the window\. For example, specifying a 2% deadband value on a sensor with a range from \-100 degrees Fahrenheit to \+100 degrees Fahrenheit tells the server to send data to the AWS Cloud when the value changes by 4 degrees Fahrenheit or more\. 
**Note**  
 You can optionally specify a minimum and maximum deadband value for this window if your source server doesn't define engineering units\. If an engineering unit range is not provided, the OPC\-UA server defaults to the full range of the measurement data type\.
+ Absolute – You specify a window using exact units\. For example, specifying a deadband value of 2 on a sensor tells the server to send data to the AWS Cloud when its value changes by at least 2 units\. You can use absolute deadbanding for dynamic environments where fluctuations are regularly expected during normal operations\.

### Deadband timeouts<a name="deadband-timeout"></a>

 You can optionally configure a deadband timeout setting\. After this timeout, the OPC\-UA server sends the current measurement value even if it is within the expected deadband fluctuation\. You can use the timeout setting to ensure that AWS IoT SiteWise is ingesting a steady stream of data at all times, even when values do not exceed the defined deadband window\. 