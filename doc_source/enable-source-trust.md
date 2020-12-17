# Enabling your source servers to trust the gateway<a name="enable-source-trust"></a>

If you choose a message security mode other than **None**, you must enable your source servers to trust the gateway\. The gateway generates a certificate that you must accept on your source server\. Steps can vary depending on the source servers that you use\. Consult the documentation for each server\.

The procedure might be similar to the following steps\.

**To enable an OPC\-UA server to trust the gateway**

1. Open the interface for configuring your OPC\-UA server \(for example, right\-click the OPC\-UA icon in the system tray\)\.

1. Enter the user name and password for the OPC\-UA server administrator\.

1. Locate **Trusted Clients** in the interface, and then choose **AWS IoT SiteWise Gateway Client**\.

1. Choose **Trust**\.

## Exporting the OPC\-UA client certificate<a name="export-opc-ua-client-certificate"></a>

Some OPC\-UA servers require access to the OPC\-UA client certificate file to trust the gateway\. If this applies to your OPC\-UA servers, you can use the following procedure to export the OPC\-UA client certificate from the gateway\. Then, you can import the certificate on your OPC\-UA server\.

**To export the OPC\-UA client certificate file for a source**

1. The gateway stores an OPC\-UA client certificate for each source\. Each source is identified by a unique ID\. The gateway stores source IDs in a configuration file located at `/sitewise-root/config/sitewise-COLLECTOR-config.json`\. You can't use the AWS IoT SiteWise API to return the source IDs, so you must find them in this configuration file\.

   On the gateway, run one of the following commands to print the output of the collector configuration file\. Replace *sitewise\-root* with the local storage path for your AWS IoT SiteWise configuration\. The default *sitewise\-root* is `/var/sitewise`\.
   + If you have [jq](https://stedolan.github.io/jq/) installed, run the following command to pretty\-print the configuration file with syntax highlighting\.

     ```
     cat /sitewise-root/config/sitewise-COLLECTOR-config.json | jq .
     ```
   + If you have [Python](https://www.python.org/) installed, run the following command to pretty\-print the configuration file\.

     ```
     cat /sitewise-root/config/sitewise-COLLECTOR-config.json | python -m json.tool
     ```
   + If you don't have a JSON printing tool, run the following command to print the configuration file\.

     ```
     cat /sitewise-root/config/sitewise-COLLECTOR-config.json
     ```  
**Example : Configuration file for a gateway**  

   The following JSON example demonstrates a configuration file for a gateway with one basic OPC\-UA source\.

   ```
   {
     "creationDate": 1588369971457,
     "dataVersion": null,
     "gatewayConfiguration": {
       "schemaVersion": "DefaultSchemaVersion",
       "sources": [
         {
           "endpoint": {
             "certificateTrust": {
               "type": "TrustAny"
             },
             "endpointUri": "opc.tcp://203.0.113.0:49320",
             "identityProvider": {
               "type": "Anonymous"
             },
             "messageSecurityMode": "NONE",
             "nodeFilterRules": [],
             "securityPolicy": "NONE"
           },
           "id": "a1b2c3d4-5678-90ab-cdef-1c1c1EXAMPLE",
           "measurementDataStreamPrefix": "",
           "name": "Wind Farm #1",
           "type": "OpcUaSource"
         }
       ],
       "syncStatus": "OUT_OF_SYNC",
       "version": 27
     },
     "id": {
       "accountId": "123456789012",
       "value": "a1b2c3d4-5678-90ab-cdef-1a1a1EXAMPLE"
     },
     "lastUpdateDate": 1592004024251,
     "name": "ExampleCorpGateway",
     "platform": {
       "groupArn": "arn:aws:greengrass:us-west-2:123456789012:/greengrass/groups/a1b2c3d4-5678-90ab-cdef-1b1b1EXAMPLE",
       "type": "Greengrass"
     },
     "sink": null,
     "state": "ACTIVE"
   }
   ```

   Find the source that corresponds to the OPC\-UA server\. The ID of the source is in the `id` field\. In the above example, *a1b2c3d4\-5678\-90ab\-cdef\-1c1c1EXAMPLE* is the source ID for the OPC\-UA source named `Wind Farm #1`\.

1. Run the following command to change to the directory that contains the certificate file\. Replace *sitewise\-root* with the local storage path for your AWS IoT SiteWise configuration and replace *source\-id* with the source ID that you found in the previous step\.

   ```
   cd /sitewise-root/pusher/source-id/opcua-certificate-store
   ```

1. The gateway's OPC\-UA client certificate for this source is in the `aws-iot-opcua-client.pfx` file\.

   Run the following command to export the certificate to a `.pem` file called `aws-iot-opcua-client-certificate.pem`\.

   ```
   keytool -exportcert -v -alias aws-iot-opcua-client -keystore aws-iot-opcua-client.pfx -storepass amazon -storetype PKCS12 -rfc > aws-iot-opcua-client-certificate.pem
   ```

1. Transfer the certificate file, `aws-iot-opcua-client-certificate.pem`, from the gateway to the OPC\-UA server\.

   To do so, you can use common software such as the `scp` program to transfer the file using the SSH protocol\. For more information, see [Secure copy](https://en.wikipedia.org/wiki/Secure_copy) on *Wikipedia*\.
**Note**  
If your gateway is running on Amazon Elastic Compute Cloud \(Amazon EC2\) and you're connecting to it for the first time, you must configure prerequisites to connect\. For more information, see [Connect to your Linux instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html) in the *Amazon EC2 User Guide for Linux Instances*\.

1. Import the certificate file, `aws-iot-opcua-client-certificate.pem`, on the OPC\-UA server to trust the gateway\. Steps can vary depending on the source server that you use\. Consult the documentation for the server\.