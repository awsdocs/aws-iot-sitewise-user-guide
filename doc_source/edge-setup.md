# Edge processing prerequisites<a name="edge-setup"></a>

 Before you can use edge processing with AWS IoT SiteWise, you need to verify that your AWS account and devices are configured correctly\. Ensure that you have met the following prerequisites: 
+ A configured and deployed AWS IoT SiteWise gateway\. Your gateway device must be an industrial computer that has at least 4 core processors, 16 GB of RAM, and 256 GB HDD\. For more information about configuring a gateway, see [Configuring a gateway](configure-gateway.md)\.
+ An AWS IoT Greengrass service role attached to your AWS account and the AWS IoT Core console\. This role must have permissions that allow your AWS IoT Greengrass device to perform AWS IoT SiteWise operations and access Amazon Elastic Container Registry \(Amazon ECR\)\.

  The following example service role policy grants access to AWS IoT SiteWise, Amazon ECR, and the AWS IoT SiteWise Data Processor connector\.

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Sid": "VisualEditor0",
              "Effect": "Allow",
              "Action": [
                  "ecr:GetDownloadUrlForLayer",
                  "ecr:BatchGetImage"
              ],
              "Resource": [
                  "arn:aws:ecr:*:123456789012:repository/sync/sync-app",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/ssl-proxy/ssl-proxy",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/property-state-service/property-state-service",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/property-state-internal-service/property-state-internal-service",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/model-service/model-service",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/monitor-control-plane/monitor-control-plane",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/monitor-app/monitor-app",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/dependency-routing-service/dependency-routing-service",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/hotpath/hotpath",
                  "arn:aws:ecr:*:123456789012:repository/edgerunner/dynamodb-local/dynamodb-local",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/monitor-app/monitor-app",
                  "arn:aws:ecr:*:123456789012:repository/edgerunner/influxdb/influxdb",
                  "arn:aws:ecr:*:123456789012:repository/edgerunner/minio/minio",
                  "arn:aws:ecr:*:123456789012:repository/sitewise/monitoring-service/monitoring-service",
                  "arn:aws:ecr:*:123456789012:repository/edgerunner/edge-formation/edge-formation"
              ]
          },
          {
              "Sid": "VisualEditor1",
              "Effect": "Allow",
              "Action": "ecr:GetAuthorizationToken",
              "Resource": "*"
          },
          {
              "Sid": "VisualEditor2",
              "Effect": "Allow",
              "Action": "iotsitewise:*",
              "Resource": "*"
          }
      ]
  }
  ```
+ An edge device\. This device must meet the minimum configuration requirements of 4 CPU cores, 16 GB RAM, and 256 GB of HDD storage\. In addition, the device must meet the following requirements:
  + Enabled inbound MQTT communication – Consult your device documentation for more information\. For more information about enabling MQTT communication on your device, see the [MQTT documentation](http://www.steves-internet-guide.com/mqtt-works/)\.
  + Java 8 – Run the following example command to verify your Java version\.

    ```
    java8 -version
    ```
  + Python 3\.7 – Run the following example command to verify your Python version

    ```
    python3.7 --version
    ```
  + Docker and docker\-compose – Run the following example commands to verify your Docker and Docker\-compose versions\. 

    ```
    docker --version
    docker-compose --version
    ```
  + A Docker user – We also recommend that you create a directory for the deployment of the AWS IoT SiteWise Data Processor connector\. Run the following commands on your device to create the user and directory\.

    ```
    sudo mkdir /sitewise_edge
    
    sudo useradd -u GGC_USER_ID ggc_user //if it doesn't exist
    
    //to find GGC_USER_ID
    id -u ggc_user
    
    sudo usermod -aG docker ggc_user
    sudo chown GGC_USER_ID /sitewise_edge
    sudo chmod 700 /sitewise_edge
    ```