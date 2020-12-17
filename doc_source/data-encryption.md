# Data encryption<a name="data-encryption"></a>

Data encryption refers to protecting data while in\-transit \(as it travels to and from AWS IoT SiteWise, and between gateways and servers\), and at rest \(while it is stored on local devices or in AWS services\)\. You can protect data in transit using Transport Layer Security \(TLS\) or at rest using client\-side encryption\.

**Note**  
AWS IoT SiteWise edge processing exposes APIs that are hosted within SiteWise gateways and accessible over the local network\. These APIs are exposed over a TLS connection backed by a server\-certificate owned by the AWS IoT SiteWise Edge connector\. For client authentication, these APIs use an access\-control password\. The server\-certificate private\-key and the access\-control password are both stored on disk\. AWS IoT SiteWise edge processing relies on file\-system encryption for the security of these credentials at rest\.

For more information about server\-side encryption and client\-side encryption, review the topics listed below\.

**Topics**
+ [Encryption at rest](encryption-at-rest.md)
+ [Encryption in transit](encryption-in-transit.md)
+ [Key management](key-management.md)