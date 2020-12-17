# Integrating with Grafana<a name="grafana-integration"></a>

Grafana is a data visualization platform that you can use to visualize and monitor data in dashboards\. In Grafana version 7\.3\.0 and later, you can use the AWS IoT SiteWise plugin to visualize your AWS IoT SiteWise asset data in Grafana dashboards\. You can visualize data from multiple AWS sources \(such as AWS IoT SiteWise, Amazon Timestream, and Amazon CloudWatch\) and other data sources with a single Grafana dashboard\.

You have two options to use the AWS IoT SiteWise plugin:
+ **Local Grafana servers**

  You can set up the AWS IoT SiteWise plugin on a Grafana server that you manage\. For more information about how to add and use the plugin, see the [AWS IoT SiteWise Datasource README](https://github.com/grafana/iot-sitewise-datasource/blob/main/src/README.md) file on the GitHub website\.
+ **AWS Managed Service for Grafana**

  You can use the AWS IoT SiteWise plugin in the AWS Managed Service for Grafana \(AMG\)\. AMG manages Grafana servers for you so that you can visualize your data without having to build, package, or deploy any hardware or any other Grafana infrastructure\. For more information, see the following topics in the *AWS Managed Service for Grafana User Guide*:
  + [What is Amazon Managed Service for Grafana \(AMG\)?](https://docs.aws.amazon.com/grafana/latest/userguide/what-is-Amazon-Managed-Service-Grafana.html)
  + [Using the AWS IoT SiteWise data source](https://docs.aws.amazon.com/grafana/latest/userguide/using-iotsitewise-in-AMG.html)

**Example Grafana dashboard**  
The following Grafana dashboard visualizes the [demo wind farm](getting-started-demo.md)\. You can access this demo dashboard on the [Grafana Play](https://play.grafana.org/d/avzwehmz/demo-wind-farm?orgId=1) website\.  

![\[An example Grafana dashboard that visualizes the AWS IoT SiteWise demo wind farm.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/grafana-dashboard-example.png)