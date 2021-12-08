# AWS IoT SiteWise quotas<a name="quotas"></a>

The following tables describe quotas in AWS IoT SiteWise\. For more information about quotas and how to request quota increases, see [AWS service quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) in the *AWS General Reference*\.


**Quotas for assets and asset models**  

| Resource | Quota | Adjustable | Notes | 
| --- | --- | --- | --- | 
| Number of asset models per Region per AWS account | 100 | Yes |  | 
| Number of assets per asset model | 10,000 | Yes |  | 
| Number of parent asset models per child asset model | 10 | Yes |  | 
| Number of child assets per parent asset | 100 | Yes |  | 
| Depth of asset hierarchy tree | 10 | Yes |  | 
| Number of asset hierarchy definitions per asset model | 20 | Yes |  | 
| Number of properties per asset model | 200 | Yes |  | 
| Number of property variables per property formula expression | 10 | Yes |  | 
| Number of functions per property formula expression | 10 | Yes |  | 
| Depth of property tree per asset model | 10 | Yes | For example, a model with a transform property C that consumes a transform property B that consumes a measurement property A has a depth of 3\. | 
| Number of asset models per hierarchy tree | 50 | Yes |  | 
| Number of directly dependent properties per asset model | 20 | Yes | This quota limits how many properties can directly depend on a single property, as defined in property formula expressions\. | 
| Number of dependent properties per asset model | 30 | Yes | This quota limits how many properties can directly or indirectly depend on a single property, as defined in property formula expressions\. | 
| Request rate for model API operations and logging options | 10 requests per second per Region per AWS account | Yes | This quota applies to API operations such as CreateAssetModel and logging options\. | 
| Request rate for asset API operations | 30 requests per second per Region per AWS account | Yes | This quota applies to API operations such as CreateAsset and AssociateAssets\. | 
| Request rate for data stream \(time series\) API operations | 30 requests per second per Region per AWS account | Yes | This quota applies to API operations such as DescribeTimeSeries and AssociateTimeSeriesToAssetProperty\. | 


**Quotas for asset property data**  

| Resource | Quota | Adjustable | Notes | 
| --- | --- | --- | --- | 
| Request rate for asset property data API operations | 1,000 requests per second per Region per AWS account | Yes | This quota applies to API operations such as GetAssetPropertyValue and BatchPutAssetPropertyValue\. | 
| Number of data points per second per data quality per asset property | 10 data points | No | This quota applies to the maximum number of timestamp\-quality\-value \(TQV\) data points with the same timestamp in seconds per data quality for each asset property\. You can store up to this number of good\-quality, uncertain\-quality, and bad\-quality data points for any given second for each asset property\. | 
| Number of BatchPutAssetPropertyValue entries ingested per second per asset property per Region per AWS Account\. | 10 entries per asset property | No | This quota applies to BatchPutAssetPropertyValue entries from all sources, including gateways, AWS IoT Core rules, and API calls\. | 
| Rate of data points ingested | 1,000 data points per second per Region per AWS account | Yes | Timestamp\-quality\-value \(TQV\) data points\. | 
| Rate of GetInterpolatedAssetPropertyValues requests | 500 | Yes | The maximum number of GetInterpolatedAssetPropertyValues requests per second that you can perform in this account in the current Region\. | 
| Number of results per GetInterpolatedAssetPropertyValues request | 10 | Yes | The maximum number of results to return per paginated GetInterpolatedAssetPropertyValues request\. | 
| Number of days between the start date in the past and today for GetInterpolatedAssetPropertyValues | 28 | Yes | The maximum number of days between the start date and today\. This quota applies to the startTimeInSeconds parameter when you specify a start date in the past for GetInterpolatedAssetPropertyValues requests\. | 


**Quotas for AWS IoT SiteWise gateways**  

| Resource | Quota | Adjustable | 
| --- | --- | --- | 
| Number of gateways per Region per AWS account | 100 | Yes | 
| Number of OPC\-UA sources per gateway | 100 | No | 
| Number of Modbus TCP sources per gateway | 100 | No | 
| Number of Ethernet/IP sources per gateway | 100 | No | 


**Quotas for AWS IoT SiteWise Monitor**  

| Resource | Quota | Adjustable | 
| --- | --- | --- | 
| Number of portals per Region per AWS account | 100 | Yes | 
| Number of projects per portal | 100 | Yes | 
| Number of dashboards per project | 100 | Yes | 
| Number of root assets per project | 1 | No | 
| Number of visualizations per dashboard | 10 | Yes | 
| Number of metrics per dashboard visualization | 5 | Yes | 
| Number of thresholds per dashboard visualization | 12 | No | 