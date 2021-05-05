# Monitor data at the edge<a name="using-opshub"></a>

You can use SiteWise Monitor to monitor your industrial assets at the edge\. SiteWise Monitor integrates with the gateway to provide visualization of measurements, transforms, and metrics\. 

**Note**  
Currently, this feature doesn't support alarms\.

To get started, you create dashboards in the AWS Cloud\. AWS IoT SiteWise automatically deploys these dashboards to your local gateways\. Then, you can access these dashboards from a web browser from any device in the same local network as your gateway\. For more information about creating dashboards in the AWS Cloud, see [Creating dashboards \(AWS Command Line Interface\)](create-dashboards-using-aws-cli.md)\.

Complete the following steps to access SiteWise Monitor at the edge\.

**To access SiteWise Monitor at the edge**

1.  Download and install the [OpsHub for AWS IoT SiteWise application](https://aws-iot-sitewise.s3.amazonaws.com/gateway/OpsHub+for+AWS+IoT+SiteWise.exe) on your host device\. Follow the provided instructions for installation\. This is your local gateway application\. 

1. Generate your server certificate and gateway password\. On your gateway terminal, run the following command\.

   ```
   sudo path-to-sitewise-edge-directory/credentials/create-credentials.sh
   ```

1. When prompted, enter a password that meets the minimum password requirements\.

   ```
   my-machine % ./create-credentials.sh 
   
   Password has following minimum requirements:
   1. Must be at least 12 characters long.
   2. Contain mixture of both uppercase and lowercase letters.
   3. Contain a mixture of letters and numbers.
   4. Include of at least one special character, e.g., ! @ # ? ].
   5. Characters < or > are prohibited as both can cause problems in Web browsers.
   
   Enter Password: examplepassword
   Confirm Password: examplepassword
   Enter a date (yyyy-mm-dd) [leave empty for never]: 2022-12-31
   --------------------------------------------------------------------------------
   Security Reminder:
    
   You are responsible for securing your devices, local network connections, and
   private keys stored on your gateway device. In addition to setting up a strong
   password, AWS strongly recommends that you encrypt and appropriately secure your
   gateway so your data and, more importantly, your password remains secure. For
   more information about hardware security integration with AWS IoT Greengrass,
   visit https://docs.aws.amazon.com/greengrass/latest/developerguide/security.html
   Otherwise, consult the documentation for your operating system to learn about how
   to encrypt and secure your gateway device’s file system.
   --------------------------------------------------------------------------------
   
   
   Your API access credentials expiring on (2022-12-31) are:
   export AWS_ACCESS_KEY_ID="AKIAIOSFODNN7EXAMPLE"
   export AWS_SECRET_ACCESS_KEY="wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"
   export AWS_REGION="Edge"
   ```
**Note**  
Securely store your password and credentials\. You use these with Sitewise Edge and the AWS SDK\.

1. Download your gateway certificate\. Run the following command on your gateway host terminal to copy your certificate to your host device\.

   ```
   cp path-to-sitewise-edge-directory/certificates/servercert.pem path-to-save-certificate
   ```

1. Open the local gateway application\. On the **Welcome** page, enter the following details for your gateway\. 
**Note**  
 You can connect to another gateway using the local gateway application at any time on the **Preferences** page\. 

   1. For **Password**, enter your gateway's password\.

   1. For **Server certificate**, choose the file that contains your certificate\.

   1. For **SiteWise gateway address**, enter the IP address of your gateway\.

   Choose **Connect** to connect to your gateway\. You can now use the local gateway application to visualize your local edge\-configured data with AWS IoT SiteWise\.