# Security best practices for AWS IoT SiteWise<a name="security-best-practices"></a>

This topic contains security best practices for AWS IoT SiteWise\.

## Use authentication credentials on your OPC\-UA servers<a name="security-best-practices-opc-ua-authentication"></a>

Require authentication credentials to connect to your OPC\-UA servers\. Consult the documentation for your servers to do so\. Then, to allow your gateway to connect to your OPC\-UA servers, add server authentication secrets to your gateway\. For more information, see [Configuring source authentication](configure-source-authentication.md)\.

## Use encrypted communication modes for your OPC\-UA servers<a name="security-best-practices-opc-ua-encryption"></a>

Choose a non\-deprecated, encrypted message security mode when you configure your OPC\-UA sources for your gateway\. This helps secure your industrial data as it moves from your OPC\-UA servers to the gateway\. For more information, see [Data in transit over the local network](encryption-in-transit.md#local-encryption-in-transit) and [Configuring data sources](configure-sources.md)\.

## Keep your components up to date<a name="security-best-practices-update-regularly"></a>

If you use AWS IoT SiteWise gateways to ingest data to the service, it's your responsibility to conﬁgure and maintain your gateway's environment\. This responsibility includes upgrading to the latest versions of the gateway's system software, AWS IoT Greengrass software, and connectors\. 

**Note**  
The AWS IoT SiteWise Edge connector stores secrets on your file system\. These secrets control who can view the data cached within your gateway\. It's strongly recommended that you turn on disk or file\-system encryption for the system running your gateway\. 

## Encrypt your gateway's file system<a name="security-best-practices-gateway-encryption"></a>

Encrypt and secure your gateway, so your industrial data is secure as it moves through the gateway\. If your gateway has a hardware security module, you can configure AWS IoT Greengrass to secure your gateway\. For more information, see [Hardware security integration](https://docs.aws.amazon.com/greengrass/latest/developerguide/hardware-security.html) in the *AWS IoT Greengrass Developer Guide*\. Otherwise, consult the documentation for your operating system to learn how to encrypt and secure your file system\.

## Secure access to your edge configuration<a name="security-best-practices-edge-access-control"></a>

Don't share your edge console application password or your SiteWise Monitor application password\. Don't put this password in places where anyone can see them\. Implement a healthy password rotation policy by configuring an appropriate expiration for your password\.

## Grant SiteWise Monitor users minimum possible permissions<a name="security-best-practices-minimum-monitor-permissions"></a>

Follow the principle of least privilege by using the minimum set of access policy permissions for your AWS SSO users and groups\.
+ When you create a portal, define a role that allows the minimum set of assets needed for that portal\. For more information, see [Using service roles for AWS IoT SiteWise Monitor](monitor-service-role.md)\.
+ When you and your portal administrators create and share projects, use the minimum set of assets needed for that project\.
+ When a user or group no longer needs access to a portal or project, remove them from that resource\. If that user or group is no longer applicable to your organization, delete that user or group from your identity store\.

The least principle best practice also applies to IAM roles\. For more information, see [Policy best practices](security_iam_id-based-policy-examples.md#security_iam_service-with-iam-policy-best-practices)\.

## Don't expose sensitive information<a name="security-best-practices-sensitive-information"></a>

You should prevent the logging of credentials and other sensitive information, such as personally identifiable information \(PII\)\. We recommend that you implement the following safeguards even though access to local logs on a gateway requires root privileges and access to CloudWatch Logs requires IAM permissions\.
+ Don't use sensitive information in names, descriptions, or properties of your assets or models\.
+ Don't use sensitive information in gateway or source names\.
+ Don't use sensitive information in names or descriptions of your portals, projects, or dashboards\.

## Follow AWS IoT Greengrass security best practices<a name="security-best-practices-greengrass-guidelines"></a>

Follow AWS IoT Greengrass security best practices for your gateway\. For more information, see [Security best practices](https://docs.aws.amazon.com/greengrass/latest/developerguide/security-best-practices.html) in the *AWS IoT Greengrass Developer Guide*\.

## See also<a name="security-best-practices-see-also"></a>
+ [Security best practices](https://docs.aws.amazon.com/iot/latest/developerguide/security-best-practices.html) in the *AWS IoT Developer Guide*
+ [Ten security golden rules for IoT solutions](http://aws.amazon.com/blogs/iot/ten-security-golden-rules-for-iot-solutions/)