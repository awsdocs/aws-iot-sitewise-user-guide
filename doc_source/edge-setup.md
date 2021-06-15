# Edge processing prerequisites<a name="edge-setup"></a>


|  | 
| --- |
|  Processing at the edge is in preview release for AWS IoT SiteWise and is subject to change\. We recommend that you use this feature only with test data, and not in production environments\. While the edge processing feature is in preview, you must download the edge processing preview AWS SDK and AWS CLI to use the API operations for this feature\. These API operations aren't available in the public AWS SDK or AWS CLI\. For more information, see [Edge processing preview AWS CLI and AWS SDKs](edge-preview-sdks.md)\.  | 

 Before you can use edge processing with AWS IoT SiteWise, you need to verify that your AWS account and devices are configured correctly\. For more information about getting started with edge processing, see [Introducing AWS IoT SiteWise](https://aws-blogs-prod.amazon.com/iot/introducing-aws-iot-sitewise-edge/) in the AWS official blog\.

Ensure that you have met the following prerequisites: 
+ An edge device\. This device must meet the minimum configuration requirements of an x86 64 bit quad\-core processor, 16 GB of RAM, and 256 GB in disk space\. This device should be running Linux\. In addition, the device must meet the following requirements:
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
  + A Docker user – To create a home directory and a user for the deployment of the AWS IoT SiteWise Data Processor connector, do the following: 

    1. Run the following command to create the home directory\.

       ```
       sudo mkdir /sitewise_edge
       ```

    1. Run the following command to add the `ggc_user` user\.

       ```
       sudo useradd -u ggc_user-id ggc_user 
       sudo usermod -aG docker ggc_user
       sudo chown ggc_user-id /sitewise_edge
       sudo chmod 700 /sitewise_edge
       ```
**Note**  
Replace *ggc\_user\-id* with the ID of the `ggc_user` user\.
Run the following command to find the ID of the `ggc_user` user\.  

         ```
         id -u ggc_user
         ```
+ Choose one of the following options:
  + If you use AWS IoT SiteWise Data Processor connector version 1, 2, 3, or 4, ports 443, 8443, and 8883 must be externally accessible on your device\.
  + If you use AWS IoT SiteWise Data Processor connector version 5, ports 443 and 8883 must be externally accessible on your device\.
+ An AWS IoT Greengrass service role attached to your AWS account and the AWS IoT Core console\. This role must have permissions that allow your AWS IoT Greengrass device to perform AWS IoT SiteWise operations and access Amazon Elastic Container Registry \(Amazon ECR\)\.
**Note**  
You need to re\-deploy your AWS IoT SiteWise connectors after updating your service role policy\. For more information, see [Introducing AWS IoT SiteWise](https://aws-blogs-prod.amazon.com/iot/introducing-aws-iot-sitewise-edge/) in the AWS official blog\.

  To grant permissions to the role:

  1. Navigate to the IAM console and search for the role that is associated with your gateway Greengrass group\.

  1. Attach an inline policy to this role\.

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
                 "Resource": "*"
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
+ A configured and deployed AWS IoT SiteWise gateway with the data processing pack enabled\. For more information about setting up your gateway, see [Configuring a gateway](configure-gateway.md)\.

For more information about the prerequisites you need to use edge processing, see [Introducing AWS IoT SiteWise](https://aws-blogs-prod.amazon.com/iot/introducing-aws-iot-sitewise-edge/) in the AWS official blog\.