# Setting up permissions for AWS IoT Events alarms<a name="alarms-iam-permissions"></a>

When you use an AWS IoT Events alarm model to monitor an AWS IoT SiteWise asset property, you must have the following IAM permissions:
+ An AWS IoT Events service role that allows AWS IoT Events to send data to AWS IoT SiteWise\. For more information, see [Identity and access management for AWS IoT Events](https://docs.aws.amazon.com/iotevents/latest/developerguide/security-iam.html) in the *AWS IoT Events Developer Guide*\.
+ You must have the following AWS IoT SiteWise action permissions: `iotsitewise:DescribeAssetModel` and `iotsitewise:UpdateAssetModelPropertyRouting`\. These permissions allow AWS IoT SiteWise to send asset property values to AWS IoT Events alarm models\.

For more information, see [Resource\-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_resource-based) in the *IAM User Guide*\.

## Required action permissions<a name="alarms-action-permissions"></a>

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\. The `Action` element of a JSON policy describes the actions that you can use to allow or deny access in a policy\.

Before you define an AWS IoT Events alarm model, you must grant the following permissions that allow AWS IoT SiteWise to send asset property values to the alarm model\.
+ `iotsitewise:DescribeAssetModel` – Allows AWS IoT Events to check if an asset property exists\.
+ `iotsitewise:UpdateAssetModelPropertyRouting` – Allows AWS IoT SiteWise to automatically create subscriptions that enable AWS IoT SiteWise to send data to AWS IoT Events\.

For more information about AWS IoT SiteWise supported actions, see [Actions defined by AWS IoT SiteWise](https://docs.aws.amazon.com/service-authorization/latest/reference/list_awsiotsitewise.html#awsiotsitewise-actions-as-permissions) in the *Service Authorization Reference*\.

**Example permissions policy 1**  
The following policy allows AWS IoT SiteWise to send asset property values to any AWS IoT Events alarm models\.  

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iotevents:CreateAlarmModel",
                "iotevents:UpdateAlarmModel"
            ],
            "Resource": "arn:aws:iotevents:us-east-1:123456789012:alarmModel/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "iotsitewise:DescribeAssetModel",
                "iotsitewise:UpdateAssetModelPropertyRouting"
            ],
            "Resource": "arn:aws:iotsitewise:us-east-1:123456789012:asset-model/*"
        }
    ]
}
```

**Example permissions policy 2**  
The following policy allows AWS IoT SiteWise to send values of a specified asset property to a specified AWS IoT Events alarm model\.  

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iotevents:CreateAlarmModel",
                "iotevents:UpdateAlarmModel"
            ],
            "Resource": "arn:aws:iotevents:us-east-1:123456789012:alarmModel/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "iotsitewise:DescribeAssetModel"
            ],
            "Resource": "arn:aws:iotsitewise:us-east-1:123456789012:asset-model/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "iotsitewise:UpdateAssetModelPropertyRouting"
            ],
            "Resource": [
                "arn:aws:iotsitewise:us-east-1:123456789012:asset-model/12345678-90ab-cdef-1234-567890abcdef"
            ],
            "Condition": {
                "StringLike": {
                    "iotsitewise:propertyId": "abcdef12-3456-7890-abcd-ef1234567890",
                    "iotevents:alarmModelArn": "arn:aws:iotevents:us-east-1:123456789012:alarmModel/MyAlarmModel"
                }
            }
        }
    ]
}
```

## \(Optional\) ListInputRoutings permission<a name="alarms-listInputRoutings-permissions"></a>

When you update or delete an asset model, AWS IoT SiteWise can check if an alarm model in AWS IoT Events is monitoring an asset property associated with this asset model\. This prevents you from deleting an asset property that an AWS IoT Events alarm is currently using\. To enable this feature in AWS IoT SiteWise, you must have the `iotevents:ListInputRoutings` permission\. This permission allows AWS IoT SiteWise to make calls to the [ListInputRoutings](https://docs.aws.amazon.com/iotevents/latest/apireference/API_ListInputRoutings.html) API operation supported by AWS IoT Events\.

**Note**  
We strongly recommend that you add the `ListInputRoutings` permission\.

**Example permissions policy**  
The following policy allows you to update and delete asset models, and use the `ListInputRoutings` API in AWS IoT SiteWise\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iotsitewise:UpdateAssetModel",
                "iotsitewise:DeleteAssetModel",
                "iotevents:ListInputRoutings"
            ],
            "Resource": "arn:aws:iotsitewise:us-east-1:123456789012:asset-model/*"
        }
    ]
}
```

## Required permissions for SiteWise Monitor<a name="alarms-swmonitor-permissions"></a>

If you want to use the alarms feature in SiteWise Monitor portals, you must update the [SiteWise Monitor service role](monitor-service-role.md) with the following policy:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iotsitewise:DescribePortal",
                "iotsitewise:CreateProject",
                "iotsitewise:DescribeProject",
                "iotsitewise:UpdateProject",
                "iotsitewise:DeleteProject",
                "iotsitewise:ListProjects",
                "iotsitewise:BatchAssociateProjectAssets",
                "iotsitewise:BatchDisassociateProjectAssets",
                "iotsitewise:ListProjectAssets",
                "iotsitewise:CreateDashboard",
                "iotsitewise:DescribeDashboard",
                "iotsitewise:UpdateDashboard",
                "iotsitewise:DeleteDashboard",
                "iotsitewise:ListDashboards",
                "iotsitewise:CreateAccessPolicy",
                "iotsitewise:DescribeAccessPolicy",
                "iotsitewise:UpdateAccessPolicy",
                "iotsitewise:DeleteAccessPolicy",
                "iotsitewise:ListAccessPolicies",
                "iotsitewise:DescribeAsset",
                "iotsitewise:ListAssets",
                "iotsitewise:ListAssociatedAssets",
                "iotsitewise:DescribeAssetProperty",
                "iotsitewise:GetAssetPropertyValue",
                "iotsitewise:GetAssetPropertyValueHistory",
                "iotsitewise:GetAssetPropertyAggregates",
                "iotsitewise:BatchPutAssetPropertyValue",
                "iotsitewise:ListAssetRelationships",
                "iotsitewise:DescribeAssetModel",
                "iotsitewise:ListAssetModels",
                "iotsitewise:UpdateAssetModel",
                "iotsitewise:UpdateAssetModelPropertyRouting",
                "sso-directory:DescribeUsers",
                "sso-directory:DescribeUser",
                "iotevents:DescribeAlarmModel",
                "iotevents:ListTagsForResource"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "iotevents:BatchAcknowledgeAlarm",
                "iotevents:BatchSnoozeAlarm",
                "iotevents:BatchEnableAlarm",
                "iotevents:BatchDisableAlarm"
            ],
            "Resource": "*",
            "Condition": {
                "Null": {
                    "iotevents:keyValue": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iotevents:CreateAlarmModel",
                "iotevents:TagResource"
            ],
            "Resource": "*",
            "Condition": {
                "Null": {
                    "aws:RequestTag/iotsitewisemonitor": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iotevents:UpdateAlarmModel",
                "iotevents:DeleteAlarmModel"
            ],
            "Resource": "*",
            "Condition": {
                "Null": {
                    "aws:ResourceTag/iotsitewisemonitor": "false"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:PassRole"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:PassedToService": [
                        "iotevents.amazonaws.com"
                    ]
                }
            }
        }
    ]
}
```