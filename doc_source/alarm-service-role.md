# Using service roles for alarms<a name="alarm-service-role"></a>

  A service role is an [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) that a service assumes to perform actions on your behalf\. Service roles provide access only within your account and cannot be used to grant access to services in other accounts\. An IAM administrator can create, modify, and delete a service role from within IAM\. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html) in the *IAM User Guide*\. 

To allow AWS IoT SiteWise to send asset property values to AWS IoT Events to detect alarm state, you must attach a service role to each alarm subscription that you create\. The service role must specify AWS IoT SiteWise as a trusted entity and define the `iotevents:BatchPutMessage` permission\. For more information about alarms, see [Monitoring data with alarms](industrial-alarms.md)\.

When you define an AWS IoT Events alarm on an asset model, you must choose a role that allows AWS IoT SiteWise to send asset property values to AWS IoT Events\. The AWS IoT SiteWise console can create and configure the role for you\. You can edit the role in IAM later\. Your alarm won't detect if you remove the required permissions from the role or delete the role\.

**Note**  
AWS IoT Events alarms also require a service role that AWS IoT Events assumes to ingest alarm state to AWS IoT SiteWise\. For more information, see [Alarm service roles](https://docs.aws.amazon.com/iotevents/latest/developerguide/security-iam.html) in the *AWS IoT Events Developer Guide*\.

The following sections describe how to create and manage the alarm service role in the AWS Management Console or the AWS Command Line Interface \(AWS CLI\)\.

**Contents**
+ [Service role permissions for SiteWise Monitor](#alarm-service-role-permissions)

## Service role permissions for SiteWise Monitor<a name="alarm-service-role-permissions"></a>

When you define an alarm in the AWS IoT SiteWise console, you can create a role whose name starts with **IoTEventsAccessForIoTSiteWise\-role**\. This role allows AWS IoT SiteWise to send asset property values to AWS IoT Events\.

The role trusts the following service to assume the role:
+ `iotsitewise.amazonaws.com`

The role uses the following permissions policy to allow AWS IoT SiteWise to send asset property data to AWS IoT Events\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iotevents:BatchPutMessage"
      ],
      "Resource": "*"
    }
  ]
}
```