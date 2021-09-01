# Using packs<a name="data-packs"></a>

Gateways use different packs to determine how to collect and process your data\. 

Currently, the following packs are available:
+ **Data collection pack** – Use this pack to collect your industrial data and route it to AWS Cloud destinations\. By default, this pack is enabled automatically for your gateway\.
+ **Data processing pack** – Use this pack to enable gateway communication with edge\-configured asset models and assets\. You can use edge configuration to control what asset data to compute and process on\-site\. You can then send your data to AWS IoT SiteWise or other AWS services\. For more information about the data processing pack, see [Enabling edge data processing](edge-processing.md)\.
**Note**  
You need v9 of the data collection pack to use the data processing pack on your gateway\.