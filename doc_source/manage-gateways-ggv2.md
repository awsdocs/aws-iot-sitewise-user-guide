# Managing gateways<a name="manage-gateways-ggv2"></a>

You can use the AWS IoT SiteWise console, APIs, or the AWS OpsHub for AWS IoT SiteWise application to manage gateways\.

We highly recommend that you use the AWS OpsHub for AWS IoT SiteWise application to monitor the disk usage on your gateway device\. Make sure that your device has enough space for upcoming data\. When you're about to run out of space on your gateway device, the service automatically deletes a small amount of data with the oldest timestamps to make room for upcoming data\.

To check if the service deleted your data, do the following:

1. Sign in to the AWS OpsHub for AWS IoT SiteWise application\.

1. Choose **Settings**

1. For **Logs**, specify a time range, and then choose **Download**\.

1. Unzip the log file\.

1. If the log file contains the following message, the service deleted your data\.

   ```
   number bytes of data have been deleted to prevent gateway storage from running out of space.
   ```

## Managing gateways using AWS OpsHub for AWS IoT SiteWise<a name="opshub-app"></a>

You use the AWS OpsHub for AWS IoT SiteWise application to manage and monitor your gateways\. This application provides the following monitoring and management options:
+ Under **Overview**, you can do the following:
  + View gateway details that help you get insights into your gateway device data, identify issues, and improve the gateway's performance\.
  + View SiteWise Monitor portals that monitor the data from local servers and equipment at the edge\. For more information, see [What is AWS IoT SiteWise Monitor](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/what-is-monitor-app.html) in the *AWS IoT SiteWise Monitor Application Guide*\.
+ Under **Health**, there's a dashboard that displays data from your gateway\. Domain experts, such as process engineers can use the bashboard to quickly understand gateway behavior\.
+ Under **Assets**, view assets deployed to the gateway device and the last value collected or computed for asset properties\.
+ Under **Settings**, you can do the following\.
  + View the gateway configuration information and sync resources with the AWS Cloud\.
  + Download the authentication files that you can use the to access the gateway by using other tools\. 
  + Download logs that you can use to troubleshoot the gateway\.
  + View the AWS IoT SiteWise components deployed to the gateway\.

**Important**  
Your gateway device and the AWS OpsHub application must be connected to the same network\.

**To manage gateways using AWS OpsHub**

1. Download and install the [AWS OpsHub for AWS IoT SiteWise for Windows](https://aws-iot-sitewise.s3.amazonaws.com/gateway/OpsHub+for+AWS+IoT+SiteWise.exe) application\.

1. Open the application\.

1. You can sign in to your gateway with your Linux or Lightweight Directory Access Protocol \(LDAP\) credentials\. To sign in to your gateway, do one of the following:

------
#### [ Linux ]

   1. For **Hostname or IP address**, enter the hostname or IP address of your gateway device\.

   1. For **Authentication**, choose **Linux**\.

   1. For **User name**, enter the user name of your Linux operating system\.

   1. For **Password**, enter the password of your Linux operating system\.

   1. Choose **Sign in**\.

------
#### [ LDAP ]

   1. For **Hostname or IP address**, enter the hostname or IP address of your gateway device\.

   1. For **Authentication**, choose **LDAP**\.

   1. For **User name**, enter your LDAP's user name\.

   1. For **Password**, enter your LDAP's password\.

   1. Choose **Sign in**\.

------

## Managing your gateway with the AWS IoT SiteWise console<a name="cloud-console"></a>

You can use the AWS IoT SiteWise console to configure, update, and monitor all gateways in your AWS account\. 

You can view your AWS IoT SiteWise gateways by navigating to the **Gateways** page in the AWS IoT SiteWise console\. The AWS IoT SiteWise console provides the following monitoring and management options:
+ Update data source configuration and configure additional data sources
+ View the number of data points ingested per data source
+ Add data packs to your gateway
+ View the connectivity status of your gateways
+ View the gateway sync status of resources and configuration changes

## Accessing your gateway using Linux credentials<a name="linux-user-pool"></a>

Besides Lightweight Directory Access Protocol \(LDAP\), you can use the Linux credentials to access your gateway\. The following steps assume that you use a device with Ubuntu\. If you use a different Linux distribution, consult the relevant documentation for your device\.

**Important**  
To access your gateway with Linux credentials, you must enable the data processing pack for your gateway\.

**To create a Linux user pool**

1. To create an admin group, run the following command\.

   ```
   sudo groupadd --system SWE_ADMIN_GROUP
   ```

   Users in the `SWE_ADMIN_GROUP` group can allow admin access for the gateway\.

1. To create a user group, run the following command\.

   ```
   sudo groupadd --system SWE_USER_GROUP
   ```

   Users in the `SWE_USER_GROUP` group can allow ready\-only access for the gateway\.

1. To add a user to the admin group, run the following command\. Replace *user\-name* with the user name that you want to add\.

   ```
   sudo adduser --system user-name && sudo adduser user-name SWE_ADMIN_GROUP
   ```

1. To create a password, run the following command\. Replace *user\-name* and *password* with the the user name that you added in the previous step and the password that you want to create\.

   ```
   sudo passwd user-name password
   ```

You can now use the user name and password to sign in to the gateway on the AWS OpsHub for AWS IoT SiteWise application\.

## Managing the gateway certificate<a name="manage-gateway-certificate"></a>

You can use SiteWise Monitor and third\-party applications, such as Grafana on your gateway devices\. These applications require a TLS connection to the service\. Gateways currently use a service\-signed certificate\. If you use a browser to open the applications, such as a SiteWise Monitor portal, you might receive a warning for untrusted certificate\.

The following shows how to download the trusted certificate from the AWS OpsHub for AWS IoT SiteWise application\.

1. Sign in to the application\.

1. Choose **Settings**\.

1. For **Authentication**, choose **Download certificate**\.

The following assumes that you use Google Chrome or FireFox\. If you use a different browser, consult the relevant documentation for your browser\. To add the certificate that you downloaded in the previous step to a browser, do one of the following:
+ If you use Google Chrome, follow the [Set up certificates](https://support.google.com/chrome/a/answer/3505249?hl=en) in the *Google Chrome Enterprise Help documentation*\.
+ If you use Firefox, follow the [To Load the Certificate into the Mozilla or Firefox Browser](https://docs.oracle.com/cd/E19528-01/819-4639/gaesv/index.html) in the *Oracle documentation*\.