# Monitoring data with alarms<a name="industrial-alarms"></a>

You can configure alarms for your data to alert your team when equipment or processes perform sub\-optimally\. Optimal performance of a machine or process means that the values for certain metrics should be within a range of high and low limits\. When these metrics are outside their operating range, equipment operators must be notified so they can fix the issue\. Use alarms to quickly identify issues and notify operators to maximize performance of your equipment and processes\.

**Topics**
+ [Alarm types](#alarm-types)
+ [Alarm states](#alarm-states)
+ [Alarm state properties](#alarm-state-properties)
+ [Defining alarms on asset models](define-alarms.md)
+ [Configuring alarms on assets](configure-alarms.md)
+ [Responding to alarms](respond-to-alarms.md)
+ [Ingesting external alarm state](ingest-external-alarm-state.md)

## Alarm types<a name="alarm-types"></a>

You can define alarms that detect in the AWS Cloud and alarms that you detect with external processes\. AWS IoT SiteWise supports the following types of alarms:
+ **AWS IoT Events alarms**

  AWS IoT Events alarms are alarms that detect in AWS IoT Events\. AWS IoT SiteWise sends asset property values to an alarm model in AWS IoT Events\. Then, AWS IoT Events sends the alarm state to AWS IoT SiteWise\. You can configure options such as when the alarm detects and whom to notify when the alarm state changes\. You can also define the [AWS IoT Events actions](https://docs.aws.amazon.com/iotevents/latest/developerguide/iotevents-supported-actions.html) that occur when the alarm state changes\.

  Alarms in AWS IoT Events are instances of alarm models\. The alarm model specifies the threshold and severity of the alarm, what to do when the alarm state changes, and more\. When you configure each trait of the alarm model, you specify an attribute property from the asset model that the alarm monitors\. All assets based on the asset model use the value of the attribute when AWS IoT Events evaluates that trait of the alarm\.  For more information, see [Using alarms](https://docs.aws.amazon.com/iotevents/latest/developerguide/iotevents-alarms.html) in the *AWS IoT Events Developer Guide*\.

  You can respond to an AWS IoT Events alarm when it changes state\. For example, you can acknowledge or snooze an alarm when it becomes active\. You can also enable, disable, and reset alarms\.

  SiteWise Monitor users can visualize, configure, and respond to AWS IoT Events alarms in SiteWise Monitor portals\. For more information, see [Monitoring with alarms](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/monitor-alarms.html) in the *AWS IoT SiteWise Monitor Application Guide*\.
**Note**  
AWS IoT Events charges apply to evaluate these alarms and transfer data between AWS IoT SiteWise and AWS IoT Events\. For more information, see [AWS IoT Events pricing](http://aws.amazon.com/iot-events/pricing/)\.
+ **External alarms**

  External alarms are alarms that you evaluate outside of AWS IoT SiteWise\. Use external alarms if you have a data source that reports alarm state\. The external alarm contains a measurement property to which you ingest the alarm state data\.

  You can't acknowledge or snooze an external alarm when it changes state\.

  SiteWise Monitor users can see the state of external alarms in SiteWise Monitor portals, but they can't configure or respond to these alarms\.

  AWS IoT SiteWise doesn't evaluate the state of external alarms\.

## Alarm states<a name="alarm-states"></a>

Industrial alarms include information about the state of the equipment or process they monitor and \(optional\) information about the operator's response to the alarm state\.

When you define an AWS IoT Events alarm, you specify whether or not to enable the *acknowledge flow*\. The acknowledge flow is enabled by default\. When you enable this option, operators can acknowledge the alarm and leave a note with details about the alarm or the actions they took to address it\. If an operator doesn't acknowledge an active alarm before it becomes inactive, the alarm becomes latched\. The latched state indicates that the alarm became active and wasn't acknowledged, so an operator needs to check on the equipment or process and acknowledge the latched alarm\.

Alarms have the following states:
+ **Normal** \(`Normal`\) – The alarm is enabled but inactive\. The industrial process or equipment operates as expected\.
+ **Active** \(`Active`\) – The alarm is active\. The industrial process or equipment is outside its operating range and needs attention\.
+ **Acknowledged** \(`Acknowledged`\) – An operator acknowledged the state of the alarm\.

  This state applies to only alarms where you enable the acknowledge flow\.
+ **Latched** \(`Latched`\) – The alarm returned to normal but was active and no operator acknowledged it\. The industrial process or equipment requires attention from an operator to reset the alarm to normal\.

  This state applies to only alarms where you enable the acknowledge flow\.
+ **Snoozed** \(`SnoozeDisabled`\) – The alarm is disabled because an operator snoozed the alarm\. The operator defines the duration for which the alarm snoozes\. After that duration, the alarm returns to normal state\.
+ **Disabled** \(`Disabled`\) – The alarm is disabled and won't detect\.

## Alarm state properties<a name="alarm-state-properties"></a>

AWS IoT SiteWise stores alarm state data as a JSON object serialized to a string\. This object contains the state and additional information about the alarm, such as operator response actions and the rule that the alarm evaluates\.

You identify the alarm state property by its name and structure type, `AWS/ALARM_STATE`\. For more information, see [Defining alarms on asset models](define-alarms.md)\.

The alarm state data object contains the following information:

`stateName`  
The state of the alarm\. For more information, see [Alarm states](#alarm-states)\.  
Data type: `STRING`

`customerAction`  
\(Optional\) An object that contains information about an operator's response to the alarm\. Operators can enable, disable, acknowledge, and snooze alarms\. When they do so, the alarm state data includes their response and the note that they can leave when they respond\. This object contains the following information:    
`actionName`  
The name of the action that the operator takes to respond to the alarm\. This value contains one of the following strings:  
+ `ENABLE`
+ `DISABLE`
+ `SNOOZE`
+ `ACKNOWLEDGE`
+ `RESET`
Data type: `STRING`  
`enable`  
\(Optional\) An object that is present in `customerAction` when the operator enables the alarm\. When an operator enables the alarm, the alarm state changes to `Normal`\. This object contains the following information:    
`note`  
\(Optional\) The note that the customer leaves when they enable the alarm\.  
Data type: `STRING`  
Maximum length: 128 characters  
`disable`  
\(Optional\) An object that is present in `customerAction` when the operator disables the alarm\. When an operator enables the alarm, the alarm state changes to `Disabled`\. This object contains the following information:    
`note`  
\(Optional\) The note that the customer leaves when they disable the alarm\.  
Data type: `STRING`  
Maximum length: 128 characters  
`acknowledge`  
\(Optional\) An object that is present in `customerAction` when the operator acknowledges the alarm\. When an operator enables the alarm, the alarm state changes to `Acknowledged`\. This object contains the following information:    
`note`  
\(Optional\) The note that the customer leaves when they acknowledge the alarm\.  
Data type: `STRING`  
Maximum length: 128 characters  
`snooze`  
\(Optional\) An object that is present in `customerAction` when the operator snoozes the alarm\. When an operator enables the alarm, the alarm state changes to `SnoozeDisabled`\. This object contains the following information:    
`snoozeDuration`  
The duration in seconds that the operator snoozes the alarm\. The alarm changes to `Normal` state after this duration\.  
Data type: `INTEGER`  
`note`  
\(Optional\) The note that the customer leaves when they snooze the alarm\.  
Data type: `STRING`  
Maximum length: 128 characters

`ruleEvaluation`  
\(Optional\) An object that contains information about the rule that evaluates the alarm\. This object contains the following information:    
`simpleRule`  
An object that contains information about a simple rule, which compares a property value to a threshold value with a comparison operator\. This object contains the following information:    
`inputProperty`  
The value of the property that this alarm evaluates\.  
Data type: `DOUBLE`  
`operator`  
The comparison operator that this alarm uses to compare the property with the threshold\. This value contains one of the following strings:  
+ `<` – Less than
+ `<=` – Less than or equal
+ `==` – Equal
+ `!=` – Not equal
+ `>=` – Greater than or equal
+ `>` – Greater than
Data type: `STRING`  
`threshold`  
The threshold value that this alarm compares the property value against\.  
Data type: `DOUBLE`