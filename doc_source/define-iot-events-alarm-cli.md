# Defining an AWS IoT Events alarm \(CLI\)<a name="define-iot-events-alarm-cli"></a>

You can use the AWS Command Line Interface \(AWS CLI\) to define an AWS IoT Events alarm that monitors an asset property\. You can define the alarm on a new or existing asset model\. After you define the alarm on the asset model, you create an alarm detector in AWS IoT Events and connect it to the asset model\. In this process, you do the following:

**Topics**
+ [Step 1: Defining an alarm on an asset model](#define-iot-events-alarm-definition-cli)
+ [Step 2: Defining an AWS IoT Events alarm detector model](#define-iot-events-alarm-model-cli)
+ [Step 3: Enabling data flow between AWS IoT SiteWise and AWS IoT Events](#define-iot-events-alarm-data-flow-cli)

## Step 1: Defining an alarm on an asset model<a name="define-iot-events-alarm-definition-cli"></a>

Add an alarm definition and associated properties to a new or existing asset model\.

**To define an alarm on an asset model \(CLI\)**

1. Create a file called `asset-model-payload.json`\. Follow the steps in these other sections to add your asset model's details to the file, but don't submit the request to create or update the asset model\. In this section, you add an alarm definition to the asset model details in the `asset-model-payload.json` file\.
   + For more information about how to create an asset model, see [Creating an asset model \(CLI\)](create-asset-models.md#create-asset-model-cli)\.
   + For more information about how to update an existing asset model, see [Updating an asset model \(CLI\)](update-assets-and-models.md#update-asset-model-cli)\.
**Note**  
Your asset model must define at least one asset property, including the asset property to monitor with the alarm\.

1. Add an alarm composite model \(`assetModelCompositeModels`\) to the asset model\. An AWS IoT Events alarm composite model specifies the `IOT_EVENTS` type and specifies an alarm source property\. You add the alarm source property after you create the alarm detector model in AWS IoT Events\.
**Important**  
The alarm composite model must have the same name as the AWS IoT Events alarm model you create later\. Alarm model names can contain only alphanumeric characters\. Specify a unique, alphanumeric name so that you can use the same name for the alarm model\.

   ```
   {
     ...
     "assetModelCompositeModels": [
       {
         "name": "BoilerTemperatureHighAlarm",
         "type": "AWS/ALARM",
         "properties": [
           {
             "name": "AWS/ALARM_TYPE",
             "dataType": "STRING",
             "type": {
               "attribute": {
                 "defaultValue": "IOT_EVENTS"
               }
             }
           },
           {
             "name": "AWS/ALARM_STATE",
             "dataType": "STRUCT",
             "dataTypeSpec": "AWS/ALARM_STATE",
             "type": {
               "measurement": {}
             }
           }
         ]
       }
     ]
   }
   ```

1. Add an alarm threshold attribute to the asset model\. Specify the default value to use for this threshold\. You can override this default value on each asset based on this model\.
**Note**  
The alarm threshold attribute must be an `INTEGER` or a `DOUBLE`\.

   ```
   {
     ...
     "assetModelProperties": [
       ...
       {
         "name": "Temperature Max Threshold",
         "dataType": "DOUBLE",
         "type": {
           "attribute": {
             "defaultValue": "105.0"
           }
         }
       }
     ]
   }
   ```

1. \(Optional\) Add alarm notification attributes to the asset model\. These attributes specify the AWS SSO recipient and other inputs that AWS IoT Events uses to send notifications when the alarm changes state\. You can override these defaults on each asset based on this model\.
**Important**  <a name="alarm-notifications-sso-requirement"></a>
You can send alarm notifications to AWS Single Sign\-On users\. To use this feature, you must enable AWS SSO\. You can only enable AWS SSO in one AWS Region at a time\. This means that you can define alarm notifications only in the Region where you enable AWS SSO\. For more information, see [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the *AWS Single Sign\-On User Guide*\.

   Do the following:

   1. Add an attribute that specifies the ID of your AWS SSO identity store\. You can use the AWS SSO [ListInstances](https://docs.aws.amazon.com/singlesignon/latest/APIReference/API_ListInstances.html) API operation to list your identity stores\. This operation works only in the Region where you enable AWS SSO\.

      ```
      aws sso-admin list-instances
      ```

      Then, specify the identity store ID \(for example, `d-123EXAMPLE`\) as the default value for the attribute\.

      ```
      {
        ...
        "assetModelProperties": [
          ...
          {
            "name": "identityStoreId",
            "dataType": "STRING",
            "type": {
              "attribute": {
                "defaultValue": "d-123EXAMPLE"
              }
            }
          }
        ]
      }
      ```

   1. Add an attribute that specifies the ID of the AWS SSO user who receives notifications\. To define a default notification recipient, add an AWS SSO user ID as the default value\. Do one of the following to get an AWS SSO user ID:

      1. You can use the AWS SSO [ListUsers](https://docs.aws.amazon.com/singlesignon/latest/IdentityStoreAPIReference/API_ListUsers.html) API to get the ID of a user whose user name you know\. Replace *d\-123EXAMPLE* with the ID of your identity store, and replace *Name* with the user name of the user\.

         ```
         aws identitystore list-users \
           --identity-store-id d-123EXAMPLE \
           --filters AttributePath=UserName,AttributeValue=Name
         ```

      1. Use the [AWS SSO console](https://console.aws.amazon.com/singlesignon) to browse your users and find a user ID\.

      Then, specify the user ID \(for example, `123EXAMPLE-a1b2c3d4-5678-90ab-cdef-33333EXAMPLE`\) as the default value for the attribute, or define the attribute without a default value\.

      ```
      {
        ...
        "assetModelProperties": [
          ...
          {
            "name": "userId",
            "dataType": "STRING",
            "type": {
              "attribute": {
                "defaultValue": "123EXAMPLE-a1b2c3d4-5678-90ab-cdef-33333EXAMPLE"
              }
            }
          }
        ]
      }
      ```

   1. \(Optional\) Add an attribute that specifies the default sender ID for SMS \(text\) message notifications\. The sender ID displays as the message sender on messages that Amazon Simple Notification Service \(Amazon SNS\) sends\. For more information, see [Requesting sender IDs for SMS messaging with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/channels-sms-awssupport-sender-id.html) in the *Amazon Simple Notification Service Developer Guide*\.

      ```
      {
        ...
        "assetModelProperties": [
          ...
          {
            "name": "senderId",
            "dataType": "STRING",
            "type": {
              "attribute": {
                "defaultValue": "MyFactory"
              }
            }
          }
        ]
      }
      ```

   1. \(Optional\) Add an attribute that specifies the default email address to use as the *from* address in email notifications\.

      ```
      {
        ...
        "assetModelProperties": [
          ...
          {
            "name": "fromAddress",
            "dataType": "STRING",
            "type": {
              "attribute": {
                "defaultValue": "my.factory@example.com"
              }
            }
          }
        ]
      }
      ```

   1. \(Optional\) Add an attribute that specifies the default subject to use in email notifications\.

      ```
      {
        ...
        "assetModelProperties": [
          ...
          {
            "name": "emailSubject",
            "dataType": "STRING",
            "type": {
              "attribute": {
                "defaultValue": "[ALERT] High boiler temperature"
              }
            }
          }
        ]
      }
      ```

   1. \(Optional\) Add an attribute that specifies an additional message to include in notifications\. By default, notification messages include information about the alarm\. You can also include an additional message that gives the user more information\.\.

      ```
      {
        ...
        "assetModelProperties": [
          ...
          {
            "name": "additionalMessage",
            "dataType": "STRING",
            "type": {
              "attribute": {
                "defaultValue": "Turn off the power before you check the alarm."
              }
            }
          }
        ]
      }
      ```

1. Create the asset model or update the existing asset model\. Do one of the following:
   + To create the asset model, run the following command\.

     ```
     aws iotsitewise create-asset-model --cli-input-json file://asset-model-payload.json
     ```
   + To update the existing asset model, run the following command\. Replace *asset\-model\-id* with the ID of the asset model\.

     ```
     aws iotsitewise update-asset-model \
       --asset-model-id asset-model-id \
       --cli-input-json file://asset-model-payload.json
     ```

   After you run the command, note the `assetModelId` in the response\.

### Example: Boiler asset model<a name="alarm-asset-model-example"></a>

The following asset model represents a boiler that reports temperature data\. This asset model defines an alarm that detects when the boiler overheats\.

```
{
  "assetModelName": "Boiler Model",
  "assetModelDescription": "Represents a boiler.",
  "assetModelProperties": [
    {
      "name": "Temperature",
      "dataType": "DOUBLE",
      "unit": "C",
      "type": {
        "measurement": {}
      }
    },
    {
      "name": "Temperature Max Threshold",
      "dataType": "DOUBLE",
      "type": {
        "attribute": {
          "defaultValue": "105.0"
        }
      }
    },
    {
      "name": "identityStoreId",
      "dataType": "STRING",
      "type": {
        "attribute": {
          "defaultValue": "d-123EXAMPLE"
        }
      }
    },
    {
      "name": "userId",
      "dataType": "STRING",
      "type": {
        "attribute": {
          "defaultValue": "123EXAMPLE-a1b2c3d4-5678-90ab-cdef-33333EXAMPLE"
        }
      }
    },
    {
      "name": "senderId",
      "dataType": "STRING",
      "type": {
        "attribute": {
          "defaultValue": "MyFactory"
        }
      }
    },
    {
      "name": "fromAddress",
      "dataType": "STRING",
      "type": {
        "attribute": {
          "defaultValue": "my.factory@example.com"
        }
      }
    },
    {
      "name": "emailSubject",
      "dataType": "STRING",
      "type": {
        "attribute": {
          "defaultValue": "[ALERT] High boiler temperature"
        }
      }
    },
    {
      "name": "additionalMessage",
      "dataType": "STRING",
      "type": {
        "attribute": {
          "defaultValue": "Turn off the power before you check the alarm."
        }
      }
    }
  ],
  "assetModelHierarchies": [
  
  ],
  "assetModelCompositeModels": [
    {
      "name": "BoilerTemperatureHighAlarm",
      "type": "AWS/ALARM",
      "properties": [
        {
          "name": "AWS/ALARM_TYPE",
          "dataType": "STRING",
          "type": {
            "attribute": {
              "defaultValue": "IOT_EVENTS"
            }
          }
        },
        {
          "name": "AWS/ALARM_STATE",
          "dataType": "STRUCT",
          "dataTypeSpec": "AWS/ALARM_STATE",
          "type": {
            "measurement": {}
          }
        }
      ]
    }
  ]
}
```

## Step 2: Defining an AWS IoT Events alarm detector model<a name="define-iot-events-alarm-model-cli"></a>

Create the alarm detector model in AWS IoT Events\. In AWS IoT Events, you use *expressions* to specify values in alarm detector models\. You can use expressions to specify values from AWS IoT SiteWise to evaluate and use as inputs to the alarm\. When AWS IoT SiteWise sends asset property values to the alarm detector model, AWS IoT Events evaluates the expression to get the value of the property or the ID of the asset\. You can use the following expressions in the alarm detector model:
+ **Asset property values**

  To get the value of an asset property, use the following expression\. Replace *assetModelId* with the ID of the asset model and replace *propertyId* with the ID of the property\.

  ```
  $sitewise.assetModel.`assetModelId`.`propertyId`.propertyValue.value
  ```
+ **Asset IDs**

  To get the ID of the asset, use the following expression\. Replace *assetModelId* with the ID of the asset model and replace *propertyId* with the ID of the property\.

  ```
  $sitewise.assetModel.`assetModelId`.`propertyId`.assetId
  ```

**Note**  
When you create the alarm detector model, you can define literals instead of expressions that evaluate to AWS IoT SiteWise values\. This can reduce the number of attributes that you define on your asset model\. However, if you define a value as a literal, you can't customize that value on assets based on the asset model\. Your AWS IoT SiteWise Monitor users also can't customize the alarm, because they can configure alarm settings on assets only\.

**To create an AWS IoT Events alarm detector model \(CLI\)**

1. When you create the alarm detector model in AWS IoT Events, you must specify the ID of each property that the alarm uses, which includes the following:
   + The alarm state property in the composite asset model
   + The property that the alarm monitors
   + The threshold attribute
   + \(Optional\) The AWS SSO identity store ID attribute
   + \(Optional\) The AWS SSO user ID attribute
   + \(Optional\) The SMS sender ID attribute
   + \(Optional\) The email *from* address attribute
   + \(Optional\) The email subject attribute
   + \(Optional\) The additional message attribute

   Run the following command to retrieve the IDs of these properties on the asset model\. Replace *asset\-model\-id* with the ID of the asset model from the previous step\.

   ```
   aws iotsitewise describe-asset-model --asset-model-id asset-model-id
   ```

   The operation returns a response that contains the asset model's details\. Note the ID of each property that the alarm uses\. You use these IDs when you create the AWS IoT Events alarm detector model in the next step\.

1. Create the alarm detector model in AWS IoT Events\. Do the following:

   1. Create a file called `alarm-detector-model-payload.json`\.

   1. Copy the following JSON object into the file\.

   1. Enter a name \(`alarmModelName`\), description \(`alarmModelDescription`\), and severity \(`severity`\) for your alarm\. For severity, specify an integer that reflects your company's severity levels\.
**Important**  
The alarm detector model must have the same name as the alarm composite model that you defined on your asset model earlier\.  
Alarm detector model names can contain only alphanumeric characters\.

      ```
      {
        "alarmModelName": "BoilerTemperatureHighAlarm",
        "alarmModelDescription": "Detects when the boiler temperature is high.",
        "severity": 3
      }
      ```

   1. Add the comparison rule \(`alarmRule`\) to the alarm\. This rule defines the property to monitor \(`inputProperty`\), the threshold value to compare \(`threshold`\), and the comparison operator to use \(`comparisonOperator`\)\.
      + Replace *assetModelId* with the ID of the asset model\.
      + Replace *alarmPropertyId* with the ID of the property that the alarm monitors\.
      + Replace *thresholdAttributeId* with the ID of the threshold attribute property\.
      + Replace *GREATER* with the operator to use to compare the property values with the threshold\. Choose from the following options:
        + `LESS`
        + `LESS_OR_EQUAL`
        + `EQUAL`
        + `NOT_EQUAL`
        + `GREATER_OR_EQUAL`
        + `GREATER`

      ```
      {
        "alarmModelName": "BoilerTemperatureHighAlarm",
        "alarmModelDescription": "Detects when the boiler temperature is high.",
        "severity": 3,
        "alarmRule": {
          "simpleRule": {
            "inputProperty": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.propertyValue.value",
            "comparisonOperator": "GREATER",
            "threshold": "$sitewise.assetModel.`assetModelId`.`thresholdAttributeId`.propertyValue.value"
          }
        }
      }
      ```

   1. Add an action \(`alarmEventActions`\) to send alarm state to the AWS IoT SiteWise when the alarm changes state\.
**Note**  
For advanced configuration, you can define additional actions to perform when the alarm changes state\. For example, you might call an AWS Lambda function or publish to an MQTT topic\. For more information, see [Working with other AWS services](https://docs.aws.amazon.com/iotevents/latest/developerguide/iotevents-other-aws-services.html) in the *AWS IoT Events Developer Guide*\.
      + Replace *assetModelId* with the ID of the asset model\.
      + Replace *alarmPropertyId* with the ID of the property that the alarm monitors\.
      + Replace *alarmStatePropertyId* with the ID of the alarm state property in the alarm composite model\.

      ```
      {
        "alarmModelName": "BoilerTemperatureHighAlarm",
        "alarmModelDescription": "Detects when the boiler temperature is high.",
        "severity": 3,
        "alarmRule": {
          "simpleRule": {
            "inputProperty": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.propertyValue.value",
            "comparisonOperator": "GREATER",
            "threshold": "$sitewise.assetModel.`assetModelId`.`thresholdAttributeId`.propertyValue.value"
          }
        },
        "alarmEventActions": {
          "alarmActions": [
            {
              "iotSiteWise": {
                "assetId": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.assetId",
                "propertyId": "'alarmStatePropertyId'"
              }
            }
          ]
        }
      }
      ```

   1. \(Optional\) Configure alarm notification settings\. The alarm notification action uses a Lambda function in your account to send alarm notifications\. For more information, see [Requirements for alarm notifications](define-iot-events-alarms.md#iot-events-alarm-notification-requirements)\. In the alarm notification settings, you can configure SMS and email notifications to send to AWS SSO users\. Do the following:

      1. Add the alarm notification configuration \(`alarmNotification`\) to the payload in `alarm-detector-model-payload.json`\.
         + Replace *alarmNotificationFunctionArn* with the ARN of the Lambda function that handles alarm notifications\. 

         ```
         {
           "alarmModelName": "BoilerTemperatureHighAlarm",
           "alarmModelDescription": "Detects when the boiler temperature is high.",
           "severity": 3,
           "alarmRule": {
             "simpleRule": {
               "inputProperty": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.propertyValue.value",
               "comparisonOperator": "GREATER",
               "threshold": "$sitewise.assetModel.`assetModelId`.`thresholdAttributeId`.propertyValue.value"
             }
           },
           "alarmEventActions": {
             "alarmActions": [
               {
                 "iotSiteWise": {
                   "assetId": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.assetId",
                   "propertyId": "'alarmStatePropertyId'"
                 }
               }
             ]
           },
           "alarmNotification": {
             "notificationActions": [
               {
                 "action": {
                   "lambdaAction": {
                     "functionArn": "alarmNotificationFunctionArn"
                   }
                 }
               }
             ]
           }
         }
         ```

      1. \(Optional\) Configure the SMS notifications \(`smsConfigurations`\) to send to an AWS SSO user when the alarm changes state\.
         + Replace *identityStoreIdAttributeId* with the ID of the attribute that contains the ID of the AWS SSO identity store\.
         + Replace *userIdAttributeId* with the ID of the attribute that contains the ID of the AWS SSO user\.
         + Replace *senderIdAttributeId* with the ID of the attribute that contains the Amazon SNS sender ID, or remove `senderId` from the payload\.
         + Replace *additionalMessageAttributeId* with the ID of the attribute that contains the additional message, or remove `additionalMessage` from the payload\.

         ```
         {
           "alarmModelName": "BoilerTemperatureHighAlarm",
           "alarmModelDescription": "Detects when the boiler temperature is high.",
           "severity": 3,
           "alarmRule": {
             "simpleRule": {
               "inputProperty": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.propertyValue.value",
               "comparisonOperator": "GREATER",
               "threshold": "$sitewise.assetModel.`assetModelId`.`thresholdAttributeId`.propertyValue.value"
             }
           },
           "alarmEventActions": {
             "alarmActions": [
               {
                 "iotSiteWise": {
                   "assetId": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.assetId",
                   "propertyId": "'alarmStatePropertyId'"
                 }
               }
             ]
           },
           "alarmNotification": {
             "notificationActions": [
               {
                 "action": {
                   "lambdaAction": {
                     "functionArn": "alarmNotificationFunctionArn"
                   }
                 },
                 "smsConfigurations": [
                   {
                     "recipients": [
                       {
                         "ssoIdentity": {
                           "identityStoreId": "$sitewise.assetModel.`assetModelId`.`identityStoreIdAttributeId`.propertyValue.value",
                           "userId": "$sitewise.assetModel.`assetModelId`.`userIdAttributeId`.propertyValue.value"
                         }
                       }
                     ],
                     "senderId": "$sitewise.assetModel.`assetModelId`.`senderIdAttributeId`.propertyValue.value",
                     "additionalMessage": "$sitewise.assetModel.`assetModelId`.`additionalMessageAttributeId`.propertyValue.value"
                   }
                 ]
               }
             ]
           }
         }
         ```

      1. \(Optional\) Configure the email notifications \(`emailConfigurations`\) to send to an AWS SSO user when the alarm changes state\.
         + Replace *identityStoreIdAttributeId* with the ID of the AWS SSO identity store ID attribute property\.
         + Replace *userIdAttributeId* with the ID of the AWS SSO user ID attribute property\.
         + Replace *fromAddressAttributeId* with the ID of the "from" address attribute property, or remove `from` from the payload\.
         + Replace *emailSubjectAttributeId* with the ID of the email subject attribute property, or remove `subject` from the payload\.
         + Replace *additionalMessageAttributeId* with the ID of the additional message attribute property, or remove `additionalMessage` from the payload\.

         ```
         {
           "alarmModelName": "BoilerTemperatureHighAlarm",
           "alarmModelDescription": "Detects when the boiler temperature is high.",
           "severity": 3,
           "alarmRule": {
             "simpleRule": {
               "inputProperty": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.propertyValue.value",
               "comparisonOperator": "GREATER",
               "threshold": "$sitewise.assetModel.`assetModelId`.`thresholdAttributeId`.propertyValue.value"
             }
           },
           "alarmEventActions": {
             "alarmActions": [
               {
                 "iotSiteWise": {
                   "assetId": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.assetId",
                   "propertyId": "'alarmStatePropertyId'"
                 }
               }
             ]
           },
           "alarmNotification": {
             "notificationActions": [
               {
                 "action": {
                   "lambdaAction": {
                     "functionArn": "alarmNotificationFunctionArn"
                   }
                 },
                 "smsConfigurations": [
                   {
                     "recipients": [
                       {
                         "ssoIdentity": {
                           "identityStoreId": "$sitewise.assetModel.`assetModelId`.`identityStoreIdAttributeId`.propertyValue.value",
                           "userId": "$sitewise.assetModel.`assetModelId`.`userIdAttributeId`.propertyValue.value"
                         }
                       }
                     ],
                     "senderId": "$sitewise.assetModel.`assetModelId`.`senderIdAttributeId`.propertyValue.value",
                     "additionalMessage": "$sitewise.assetModel.`assetModelId`.`additionalMessageAttributeId`.propertyValue.value"
                   }
                 ],
                 "emailConfigurations": [
                   {
                     "from": "$sitewise.assetModel.`assetModelId`.`fromAddressAttributeId`.propertyValue.value",
                     "recipients": {
                       "to": [
                         {
                           "ssoIdentity": {
                             "identityStoreId": "$sitewise.assetModel.`assetModelId`.`identityStoreIdAttributeId`.propertyValue.value",
                             "userId": "$sitewise.assetModel.`assetModelId`.`userIdAttributeId`.propertyValue.value"
                           }
                         }
                       ]
                     },
                     "content": {
                       "subject": "$sitewise.assetModel.`assetModelId`.`emailSubjectAttributeId`.propertyValue.value",
                       "additionalMessage": "$sitewise.assetModel.`assetModelId`.`additionalMessageAttributeId`.propertyValue.value"
                     }
                   }
                 ]
               }
             ]
           }
         }
         ```

   1. \(Optional\) Add the alarm capabilities \(`alarmCapabilities`\) to the payload in `alarm-detector-model-payload.json`\. In this object, you can specify if the acknowledge flow is enabled and the default enable state for assets based on the asset model\. For more information about the acknowledge flow, see [Alarm states](industrial-alarms.md#alarm-states)\.

      ```
      {
        "alarmModelName": "BoilerTemperatureHighAlarm",
        "alarmModelDescription": "Detects when the boiler temperature is high.",
        "severity": 3,
        "alarmRule": {
          "simpleRule": {
            "inputProperty": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.propertyValue.value",
            "comparisonOperator": "GREATER",
            "threshold": "$sitewise.assetModel.`assetModelId`.`thresholdAttributeId`.propertyValue.value"
          }
        },
        "alarmEventActions": {
          "alarmActions": [
            {
              "iotSiteWise": {
                "assetId": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.assetId",
                "propertyId": "'alarmStatePropertyId'"
              }
            }
          ]
        },
        "alarmNotification": {
          "notificationActions": [
            {
              "action": {
                "lambdaAction": {
                  "functionArn": "alarmNotificationFunctionArn"
                }
              },
              "smsConfigurations": [
                {
                  "recipients": [
                    {
                      "ssoIdentity": {
                        "identityStoreId": "$sitewise.assetModel.`assetModelId`.`identityStoreIdAttributeId`.propertyValue.value",
                        "userId": "$sitewise.assetModel.`assetModelId`.`userIdAttributeId`.propertyValue.value"
                      }
                    }
                  ],
                  "senderId": "$sitewise.assetModel.`assetModelId`.`senderIdAttributeId`.propertyValue.value",
                  "additionalMessage": "$sitewise.assetModel.`assetModelId`.`additionalMessageAttributeId`.propertyValue.value"
                }
              ],
              "emailConfigurations": [
                {
                  "from": "$sitewise.assetModel.`assetModelId`.`fromAddressAttributeId`.propertyValue.value",
                  "recipients": {
                    "to": [
                      {
                        "ssoIdentity": {
                          "identityStoreId": "$sitewise.assetModel.`assetModelId`.`identityStoreIdAttributeId`.propertyValue.value",
                          "userId": "$sitewise.assetModel.`assetModelId`.`userIdAttributeId`.propertyValue.value"
                        }
                      }
                    ]
                  },
                  "content": {
                    "subject": "$sitewise.assetModel.`assetModelId`.`emailSubjectAttributeId`.propertyValue.value",
                    "additionalMessage": "$sitewise.assetModel.`assetModelId`.`additionalMessageAttributeId`.propertyValue.value"
                  }
                }
              ]
            }
          ]
        },
        "alarmCapabilities": {
          "initializationConfiguration": {
            "disabledOnInitialization": false
          },
          "acknowledgeFlow": {
            "enabled": true
          }
        }
      }
      ```

   1. Add the IAM service role \(`roleArn`\) that AWS IoT Events can assume to send data to AWS IoT SiteWise\. This role requires the `iotsitewise:BatchPutAssetPropertyValue` permission and a trust relationship that allows `iotevents.amazonaws.com` to assume the role\. To send notifications, this role also requires the `lambda:InvokeFunction` and `sso-directory:DescribeUser` permissions\. For more information, see [Alarm service roles](https://docs.aws.amazon.com/iotevents/latest/developerguide/security-iam.html) in the *AWS IoT Events Developer Guide*\.
      + Replace the `roleArn` with the ARN of the role that AWS IoT Events can assume to perform these actions\.

      ```
      {
        "alarmModelName": "BoilerTemperatureHighAlarm",
        "alarmModelDescription": "Detects when the boiler temperature is high.",
        "severity": 3,
        "alarmRule": {
          "simpleRule": {
            "inputProperty": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.propertyValue.value",
            "comparisonOperator": "GREATER",
            "threshold": "$sitewise.assetModel.`assetModelId`.`thresholdAttributeId`.propertyValue.value"
          }
        },
        "alarmEventActions": {
          "alarmActions": [
            {
              "iotSiteWise": {
                "assetId": "$sitewise.assetModel.`assetModelId`.`alarmPropertyId`.assetId",
                "propertyId": "'alarmStatePropertyId'"
              }
            }
          ]
        },
        "alarmNotification": {
          "notificationActions": [
            {
              "action": {
                "lambdaAction": {
                  "functionArn": "alarmNotificationFunctionArn"
                }
              },
              "smsConfigurations": [
                {
                  "recipients": [
                    {
                      "ssoIdentity": {
                        "identityStoreId": "$sitewise.assetModel.`assetModelId`.`identityStoreIdAttributeId`.propertyValue.value",
                        "userId": "$sitewise.assetModel.`assetModelId`.`userIdAttributeId`.propertyValue.value"
                      }
                    }
                  ],
                  "senderId": "$sitewise.assetModel.`assetModelId`.`senderIdAttributeId`.propertyValue.value",
                  "additionalMessage": "$sitewise.assetModel.`assetModelId`.`additionalMessageAttributeId`.propertyValue.value"
                }
              ],
              "emailConfigurations": [
                {
                  "from": "$sitewise.assetModel.`assetModelId`.`fromAddressAttributeId`.propertyValue.value",
                  "recipients": {
                    "to": [
                      {
                        "ssoIdentity": {
                          "identityStoreId": "$sitewise.assetModel.`assetModelId`.`identityStoreIdAttributeId`.propertyValue.value",
                          "userId": "$sitewise.assetModel.`assetModelId`.`userIdAttributeId`.propertyValue.value"
                        }
                      }
                    ]
                  },
                  "content": {
                    "subject": "$sitewise.assetModel.`assetModelId`.`emailSubjectAttributeId`.propertyValue.value",
                    "additionalMessage": "$sitewise.assetModel.`assetModelId`.`additionalMessageAttributeId`.propertyValue.value"
                  }
                }
              ]
            }
          ]
        },
        "alarmCapabilities": {
          "initializationConfiguration": {
            "disabledOnInitialization": false
          },
          "acknowledgeFlow": {
            "enabled": false
          }
        },
        "roleArn": "arn:aws:iam::123456789012:role/MyIoTEventsAlarmRole"
      }
      ```

   1. Run the following command to create the AWS IoT Events alarm detector model from the payload in `alarm-detector-model-payload.json`\. 

      ```
      aws iotevents create-alarm-model --cli-input-json file://alarm-detector-model-payload.json
      ```

   1. The operation returns a response that includes the ARN of the alarm detector model, `alarmModelArn`\. Copy this ARN to set in the alarm definition on your asset model in the next step\.

## Step 3: Enabling data flow between AWS IoT SiteWise and AWS IoT Events<a name="define-iot-events-alarm-data-flow-cli"></a>

After you create the required resources in AWS IoT SiteWise and AWS IoT Events, you can enable data flow between the resources to enable your alarm\. In this section, you do the following:
+ Update the alarm definition in the asset model to use the alarm detector model that you created in the previous step\.
+ Configure subscriptions to enable AWS IoT SiteWise to send asset property data to the alarm detector model in AWS IoT Events\.

**To enable data flow between AWS IoT SiteWise and AWS IoT Events \(CLI\)**

1. Set the alarm detector model as the alarm's source in the asset model\. Do the following:

   1. Run the following command to retrieve the existing asset model definition\. Replace *asset\-model\-id* with the ID of the asset model\.

      ```
      aws iotsitewise describe-asset-model --asset-model-id asset-model-id
      ```

      The operation returns a response that contains the asset model's details\.

   1. Create a file called `update-asset-model-payload.json` and copy the previous command's response into the file\.

   1. Remove the following key\-value pairs from the `update-asset-model-payload.json` file:
      + `assetModelId`
      + `assetModelArn`
      + `assetModelCreationDate`
      + `assetModelLastUpdateDate`
      + `assetModelStatus`

   1. Add the alarm source property \(`AWS/ALARM_SOURCE`\) to the alarm composite model that you defined earlier\. Replace *alarmModelArn* with the ARN of the alarm detector model, which sets the value of the alarm source property\.

      ```
      {
        ...
        "assetModelCompositeModels": [
          ...
          {
            "name": "BoilerTemperatureHighAlarm",
            "type": "AWS/ALARM",
            "properties": [
              {
                "id": "a1b2c3d4-5678-90ab-cdef-11111EXAMPLE",
                "name": "AWS/ALARM_TYPE",
                "dataType": "STRING",
                "type": {
                  "attribute": {
                    "defaultValue": "IOT_EVENTS"
                  }
                }
              },
              {
                "id": "a1b2c3d4-5678-90ab-cdef-22222EXAMPLE",
                "name": "AWS/ALARM_STATE",
                "dataType": "STRUCT",
                "dataTypeSpec": "AWS/ALARM_STATE",
                "type": {
                  "measurement": {}
                }
              },
              {
                "name": "AWS/ALARM_SOURCE",
                "dataType": "STRING",
                "type": {
                  "attribute": {
                    "defaultValue": "alarmModelArn"
                  }
                }
              }
            ]
          }
        ]
      }
      ```

   1. Run the following command to update the asset model with the definition stored in the `update-asset-model-payload.json` file\. Replace *asset\-model\-id* with the ID of the asset model\.

      ```
      aws iotsitewise update-asset-model \
        --asset-model-id asset-model-id \
        --cli-input-json file://update-asset-model-payload.json
      ```

1. Configure a subscription for each asset property that the AWS IoT Events alarm model uses, which includes the following:
   + The property that the alarm monitors
   + The threshold attribute
   + \(Optional\) The AWS SSO identity store ID attribute
   + \(Optional\) The AWS SSO user ID attribute
   + \(Optional\) The SMS sender ID attribute
   + \(Optional\) The email *from* address attribute
   + \(Optional\) The email subject attribute
   + \(Optional\) The additional message attribute

   Each subscription requires an IAM service role that AWS IoT SiteWise can assume to send data to AWS IoT Events\. This role requires the `iotevents:BatchPutMessage` permission and a trust relationship that allows `iotsitewise.amazonaws.com` to assume the role\. For more information, see [Using service roles for alarms](alarm-service-role.md)\.
**Important**  
You must use the [alarms preview AWS CLI](alarms-preview-sdk.md) to call the subscription API operations\.

   Run the following command for each asset property that the AWS IoT Events alarm model uses\. This command also sends the current value of the property to set the values in the alarm model\.
   + Replace *asset\-model\-id* with the ID of the asset model\.
   + Replace *property\-id* with the ID of each asset property that the AWS IoT Events alarm model uses\.
   + Replace *roleArn* with the ARN of the role that AWS IoT SiteWise can assume to send data to AWS IoT Events\.

   ```
   aws iotsitewise-alarms update-subscription \
     --service IOT_EVENTS \
     --asset-model-id asset-model-id \
     --property-id property-id \
     --send-current-value \
     --config roleArn=roleArn
   ```
**Note**  
This command enables the subscriptions for every asset based on the asset model\. You can also enable or disable subscriptions for the property on an asset\. Subscriptions on assets override subscriptions on asset models\. To do so, specify `--asset-id` instead of `--asset-model-id` in the request\.

1. \(Optional\) Run the following command to verify that you enabled subscriptions for each asset property that the alarm detector model uses\. Replace *asset\-model\-id* with the ID of the asset model\.

   ```
   aws iotsitewise-alarms list-subscriptions --asset-model-id asset-model-id
   ```

   The response contains the list of all subscriptions for the asset model\. Check that there's a subscription for the property to monitor, the threshold attribute, and each notification attribute\.

Your asset model now defines an alarm that detects in AWS IoT Events\. The alarm monitors the target property in all assets based on this asset model\. You can configure the alarm on each asset to customize properties such as the threshold or AWS SSO recipient for each asset\. For more information, see [Configuring alarms on assets](configure-alarms.md)\.