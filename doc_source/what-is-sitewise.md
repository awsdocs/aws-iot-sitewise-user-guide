# What is AWS IoT SiteWise?<a name="what-is-sitewise"></a>

AWS IoT SiteWise is a managed service that lets you collect, model, analyze, and visualize data from industrial equipment at scale\. With AWS IoT SiteWise Monitor, you can quickly create web applications for non\-technical users to view and analyze your industrial data in real time\. You can gain insights about your industrial operations by configuring and monitoring metrics such as *mean time between failures* and *overall equipment effectiveness* \(OEE\)\. With AWS IoT SiteWise Edge, you can view and process your data on your local devices\.

The following diagram shows the basic architecture of AWS IoT SiteWise\.

![\[AWS IoT Greengrass "How AWS IoT SiteWise works" page screenshot.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/how-sw-works-with-edge.png)

## How AWS IoT SiteWise works<a name="how-sitewise-works"></a>

AWS IoT SiteWise provides an asset modeling framework that you can use to build representations of your industrial devices, processes, and facilities\. With asset models, you define what raw data to consume and how to process your raw data into complex metrics\. You can build and visualize assets and models for your industrial operation in the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\. You can configure asset models to collect and process data at the edge, or process data in the AWS Cloud\.

You can upload industrial data to AWS IoT SiteWise in the following ways:
+ Use AWS IoT SiteWise gateway software that runs on any platform that supports AWS IoT Greengrass, such as common industrial gateways or virtual servers\. This software can read data directly from on\-site servers over protocols such as the OPC\-UA protocol\. You can connect up to 100 OPC\-UA servers to a single AWS IoT SiteWise gateway\. You can also read data over the Modbus TCP and Ethernet/IP \(EIP\) protocol\. For more information, see [Ingesting data using a gateway](gateways.md)\.
**Note**  
You can add packs to your gateway to enable edge capability\. With Sitewise Edge, you can read and process data directly on\-site and send it to the AWS Cloud using a AWS IoT Greengrass stream\. For more information, see [Enabling edge data processing](edge-processing.md)\.
+ Use AWS IoT Core rules\. If you have devices connected to AWS IoT Core sending [MQTT](https://docs.aws.amazon.com/iot/latest/developerguide/mqtt.html) messages, you can use the AWS IoT Core rules engine to route those messages to AWS IoT SiteWise\. For more information, see [Ingesting data using AWS IoT Core rules](iot-rules.md)\.
+ Use AWS IoT Events actions\. You can configure the IoT SiteWise action in AWS IoT Events to send data to AWS IoT SiteWise when events occur\. For more information, see [Ingesting data from AWS IoT Events](iot-events.md)\.
+ Use AWS IoT Greengrass stream manager\. You can configure solutions on the edge that send high\-volume IoT data to AWS IoT SiteWise\. For more information, see [Ingesting data using AWS IoT Greengrass stream manager](greengrass-stream-manager.md)\.
+ Use the AWS IoT SiteWise API\. Your applications at the edge or in the cloud can directly send data to AWS IoT SiteWise\. For more information, see [Ingesting data using the AWS IoT SiteWise API](ingest-api.md)\.

You can set up SiteWise Monitor to create web applications for your non\-technical employees to visualize your operations\. With AWS SSO or IAM, you can configure unique logins and permissions for each employee to view specific subsets of an entire industrial operation\. AWS IoT SiteWise provides an [application guide](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/) for these employees to learn how to use SiteWise Monitor\.

## Why use AWS IoT SiteWise?<a name="why-use-sitewise"></a>

### Benefits<a name="sitewise-benefits"></a>

**Collect data consistently from all your sources**  
With AWS IoT SiteWise, you can gather data reliably from multiple facilities, structure it, and make it accessible and understandable – without developing additional software\. You can query information and metrics about equipment or processes across multiple facilities, so it’s readily available for applications\. AWS IoT SiteWise as the data collection, management and visualization capabilities you need built right in\. So, you can invest your development resources on new applications that help you learn more from your data\.

**Identify issues quickly with remote monitoring**  
Assess the performance of your industrial equipment remotely, across locations, with AWS IoT SiteWise\. Before, you had to dispatch a technician to diagnose a problem and then send another technician to fix the problem\. Now, you can remotely diagnose a problem and only dispatch technicians when needed to fix issues\. You can spend less time coordinating on\-site diagnostic activities and let your engineers focus on what they do best: understanding your operations and designing better systems\.

**Improve cross\-facility processes with a central data source**  
Visibility across industrial facilities allows you to streamline operations, as well as identify gaps in production and waste\. With AWS IoT SiteWise, you can create models of industrial processes and equipment across multiple facilities, and then automatically discover and visualize live and historical asset data through customizable charts and dashboards\. Through SiteWise Monitor, you have the ability to launch a web application with your asset data in minutes and give industrial engineers the visibility to react to issues or identify differences across facilities\. SiteWise Monitor makes it easy to create a centralized, authoritative source of information to better understand your operations, improve processes, and reduce waste across your entire organization\.

**Process and monitor data on\-premises for shop floor applications**  
AWS IoT SiteWise includes software \(in preview\), Sitewise Edge, that runs on\-premises, securely connecting to and reading data from equipment or local historian databases\. Once you have modeled your equipment and environment in the cloud, Sitewise Edge uses the same models locally to maintain consistency across both cloud and on\-premise environments, reducing duplication, effort, and development costs\. You can choose where to use and store your data across multiple locations such as keeping data on\-premises for data residency requirements or for use by local edge applications\. You can also send data to AWS IoT SiteWise or other AWS services in the cloud for additional storage and further analysis\. With Sitewise Edge, you can deploy SiteWise Monitor web applications locally so users like process engineers can visualize equipment data in near real time on the shop floor\. Sitewise Edge continues to operate even when connectivity to the cloud is not available, for on\-premises scenarios\.

### Use cases<a name="sitewise-use-cases"></a>

**Manufacturing**  
With AWS IoT SiteWise, you can easily collect and use data from your equipment to identify and reduce inefficiencies and improve industrial operations\. AWS IoT SiteWise helps you collect data from manufacturing lines and assembly robots, transfer it to the AWS Cloud, and structure performance metrics for your specific equipment and processes\. You can use these metrics to understand the overall effectiveness of your operations and identify opportunities for innovation and improvement\. You can also view your manufacturing process and identify equipment and process deficiencies, production gaps, or product defects\.

**Food and beverage**  
Food and beverage industry facilities handle a wide variety of food processing, including grinding grain to flour, butchering and packing meat, and assembling, cooking, and freezing microwaveable meals\. These processing plants often span multiple locations with plant and equipment operators in a centralized location monitoring processes and equipment\. For example, they may be monitoring refrigeration units, assessing ingredient handling and expiration, or they may be monitoring waste creation across facilities to ensure operational efficiency\. With AWS IoT SiteWise, you can group sensor data streams from multiple locations by production line and facility so your process engineers can better understand and improve processes across facilities\.

**Energy and utilities**  
Companies often deploy their power\-generation assets in remote areas, far from the technicians who are trained to fix the equipment\. When an issue arises, the technicians receive a notification, travel to the site to diagnose the problem, and then make another trip to fix it\. With AWS IoT SiteWise, you can resolve equipment issues easier and more efficiently\. You can monitor asset performance remotely in real time and access historical equipment data from anywhere to pinpoint potential problems, dispatch the right resources, and both prevent and fix issues faster\.

## Are you new to AWS IoT SiteWise?<a name="first-time-user"></a>

If you're a first\-time user of AWS IoT SiteWise, we recommend that you read about the components and concepts of AWS IoT SiteWise and set up the [AWS IoT SiteWise demo](getting-started.md#requirements)\.
+ [Key components of AWS IoT SiteWise](feature-overview.md)
+ [AWS IoT SiteWise concepts](concept-overview.md)

You can complete the following tutorials to explore certain features of AWS IoT SiteWise:
+ [Ingesting data to AWS IoT SiteWise from AWS IoT things](ingest-data-from-iot-things.md)
+ [Visualizing and sharing wind farm data in AWS IoT SiteWise Monitor](monitor-wind-farm.md)
+ [Publishing property value updates to Amazon DynamoDB](publish-to-amazon-dynamodb.md)

See the following topics to learn more about AWS IoT SiteWise:
+ [Ingesting data to AWS IoT SiteWise](industrial-data-ingestion.md)
+ [Modeling industrial assets](industrial-asset-models.md)
+ [Monitoring data with AWS IoT SiteWise Monitor](monitor-data.md)
+ [Querying asset property values and aggregates](query-industrial-data.md)
+ [Interacting with other AWS services](interact-with-other-services.md)

## Related services<a name="related-services"></a>

AWS IoT SiteWise integrates with the following AWS services so that you can develop a complete AWS IoT solution in the AWS Cloud:
+ **AWS IoT Core** – Register and control AWS IoT devices that upload sensor data to AWS IoT SiteWise\. You can configure AWS IoT SiteWise to publish notifications to the AWS IoT message broker, which lets you send AWS IoT SiteWise data to other AWS services\. For more information, see the following topics:
  + [Ingesting data using AWS IoT Core](iot-rules.md)
  + [Interacting with other AWS services](interact-with-other-services.md)
  + [What is AWS IoT?](https://docs.aws.amazon.com/iot/latest/developerguide/) in the *AWS IoT Developer Guide*
+ **AWS IoT Greengrass** – Deploy edge devices that have AWS Cloud capabilities and can communicate with local AWS IoT devices\. AWS IoT SiteWise gateways run on AWS IoT Greengrass to collect data from local servers and publish data to the AWS Cloud\. For more information, see the following topics:
  + [Ingesting data using a gateway](gateways.md)
  + [What is AWS IoT Greengrass?](https://docs.aws.amazon.com/greengrass/latest/developerguide/) in the *AWS IoT Greengrass Version 1 Developer Guide*
+ **AWS IoT Events** – Monitor your IoT data for process failures or changes in operation, and trigger actions when such events occur\. For more information, see the following topics:
  + [Monitoring data with alarms](industrial-alarms.md)
  + [Monitoring with alarms](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/monitor-alarms.html) in the *AWS IoT SiteWise Monitor Application Guide*
  + [What is AWS IoT Events?](https://docs.aws.amazon.com/iotevents/latest/developerguide/) in the *AWS IoT Events Developer Guide*
+ **AWS Single Sign\-On \(AWS SSO\) and AWS Identity and Access Management \(IAM\)** – Create and manage user identities and permissions\. SiteWise Monitor users sign in to web portals with AWS SSO or IAM credentials, and you can define which users have access to which assets' data\. For more information, see the following topics:
  + [Monitoring data with AWS IoT SiteWise Monitor](monitor-data.md)
  + [What is SiteWise Monitor?](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/) in the *AWS IoT SiteWise Monitor Application Guide*
  + [What is AWS SSO?](https://docs.aws.amazon.com/singlesignon/latest/userguide/) in the *AWS Single Sign\-On User Guide*
  + [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/) in the *IAM User Guide*

## We want to hear from you<a name="contact-us"></a>

We welcome your feedback\. To contact us, visit the [AWS IoT SiteWise Discussion Forums](https://forums.aws.amazon.com/forum.jspa?forumID=336) or use one of the feedback links:
+ **Provide feedback** at the bottom of the page\.
+ **Feedback** at the top right of the page\.