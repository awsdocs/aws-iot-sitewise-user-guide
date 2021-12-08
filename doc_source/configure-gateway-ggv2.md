# Setting up SiteWise Edge gateways \(Greengrass V2\)<a name="configure-gateway-ggv2"></a>

AWS IoT SiteWise gateways run on AWS IoT Greengrass V2 as a Greeengrass component that supports data collection and processing on premises\. To configure a gateway that runs on AWS IoT Greengrass V2, you need to create a gateway in the AWS Cloud and run the gateway software to set up your gateway device\.

**Topics**
+ [Requirements](#gateway-requirements)
+ [Create a gateway](create-gateway-ggv2.md)
+ [Installing the gateway software](install-gateway-software.md)

## Requirements<a name="gateway-requirements"></a>

Gateway devices must meet the followng requiments to install and run the gateway software\.
+ Supports [AWS IoT Greengrass V2 Core software v2\.3\.0](https://docs.aws.amazon.com/greengrass/v2/developerguide/greengrass-release-2021-06-29.html)\. For more information, see [Requirements](https://docs.aws.amazon.com/greengrass/v2/developerguide/setting-up.html#greengrass-v2-requirements) in the *AWS IoT Greengrass Version 2 Developer Guide*\.
+ One of the following supported platforms:
  + OS: Ubuntu 20\.04 or 18\.04

    Architecture: x86\_64 \(AMD64\)
  + OS: Red Hat Enterprise Linux \(RHEL\) 8

    Architecture: x86\_64 \(AMD64\)
  + OS: Amazon Linux 2

    Architecture: x86\_64 \(AMD64\)
+ Minimum 1 GB RAM allocated to the gateway software\.
+ Minimum 10 GB disk space available for the gateway software\.
+ If you plan to process data at the edge with AWS IoT SiteWise, your gateway device must also meet the following requirements:
  + Has an x86 64 bit quad\-core processor\.
  + Has at least 16 GB of RAM\.
  + Had at least 256 GB of free disk space\.
+ Choose a gateway with sufficient disk, networking, and compute capacity for your workload\.

  The disk space required for caching data for intermittent internet connectivity depends on the following factors:
  + Number of data streams uploaded
  + Data points per data stream per second
  + Size of each data point
  + Communication speeds
  + Expected network downtime

  The compute capacity required to poll and upload data depends on the following factors:
  + Number of data streams uploaded
  + Data points per data stream per second
+ Configure your gateway device to make sure that the following ports are accessible:
  + The gateway device must allow inbound traffic on port 443\.
  + The gateway device must allow outbound traffic on port 443 and 8883\.
  + The following ports are reserved for use by AWS IoT SiteWise: 80, 443, 3001, 8000, 8081, 8082, 8084, 8085, 8445, 8086, 9000, 9500, and 11080\. Using a reserved port for traffic can result in a terminated connection\.

You must have the following permissions to use AWS IoT SiteWise gateways
+ Uses the `AWSServiceRoleForIoTSiteWise` role that allows AWS IoT SiteWise to complete required actions on AWS IoT Greengrass's and AWS IoT Core's resources in your account\. For more information, see [Service\-linked role permissions for AWS IoT SiteWise ](using-service-linked-roles.md#service-linked-role-permissions)\.
+ The IAM role for your gateway must allow you to use an AWS IoT SiteWise gateway on an AWS IoT Greengrass V2 device to process asset model data and asset data\.

  The role allows the following service to assume the role: `credentials.iot.amazonaws.com`\.

  **Permissions details**

  The role must have the following permissions\.
  + `ecr` – Allows principals to download Sitewise Edge gateway docker containers from Amazon Elastic Container Registry \(Amazon ECR\)\.
  + `iotsitewise` – Allows principals to retrieve asset model data and asset data at the edge\.
  + `iot` – Allows your AWS IoT Greengrass V2 devices to interact with AWS IoT\.
  + `logs` – Allows your AWS IoT Greengrass V2 devices to send logs to Amazon CloudWatch Logs\.
  + `s3` – Allows your AWS IoT Greengrass V2 devices to download custom component artifacts from Amazon S3\.

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                  "ecr:GetDownloadUrlForLayer",
                  "ecr:BatchGetImage",
                  "ecr:GetAuthorizationToken"
              ],
              "Resource": "*"
          },
          {
              "Effect": "Allow",
              "Action": [
                  "iotsitewise:BatchPutAssetPropertyValue",
                  "iotsitewise:List*",
                  "iotsitewise:Describe*",
                  "iotsitewise:Get*"
              ],
              "Resource": "*"
          },
          {
              "Effect": "Allow",
              "Action": [
                  "iot:DescribeCertificate",
                  "logs:CreateLogGroup",
                  "logs:CreateLogStream",
                  "logs:PutLogEvents",
                  "logs:DescribeLogStreams",
                  "s3:GetBucketLocation",
                  "iot:Connect",
                  "iot:Publish",
                  "iot:Subscribe",
                  "iot:Receive",
                  "iot:DescribeEndpoint"
              ],
              "Resource": "*"
          }
      ]
  }
  ```