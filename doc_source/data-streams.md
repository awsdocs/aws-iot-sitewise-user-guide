# Managing data ingestion<a name="data-streams"></a>

You can configure your data sources to send industrial data to AWS IoT SiteWise before you create asset models and assets\. AWS IoT SiteWise automatically creates data streams to receive streams of raw data from your equipment\. Each data stream corresponds to a unique data stream alias\. For example, a wind farm has an AWS IoT SiteWise Edge gateway that transfers air temperature, propeller rotation speed, and power output time\-series data from an OPC\-UA server to AWS IoT SiteWise, and the `server1-windfarm/3/turbine/7/temperature` data stream alias identifies temperature values coming from turbine \#7 in wind farm \#3\. `server1` is the name of the OPC\-UA data source\. `server1-` is a prefix added to all data streams reported from this OPC\-UA server\.

After you create asset models and assets, you can associate data streams with asset properties defined in your assets to structure your data, then AWS IoT SiteWise can use asset models and assets to process incoming data from your data streams\. You can also disassociate data streams from asset properties\.

Currently, you can associate data streams with measurements only\. Measurements are a type of asset property that represent devices' raw sensor data streams, such as timestamped temperature values or timestamped rotations per minute \(RPM\) values\.

**Note**  
AWS IoT SiteWise uses `TimeSeries` for the Amazon Resource Name \(ARN\) resource to determine your storage charges\. For more information, see [AWS IoT SiteWise Pricing](https://aws.amazon.com/iot-sitewise/pricing/)\.