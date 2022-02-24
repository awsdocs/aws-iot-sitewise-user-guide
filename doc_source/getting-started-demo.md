# Using the AWS IoT SiteWise demo<a name="getting-started-demo"></a>

You can easily explore AWS IoT SiteWise by using the AWS IoT SiteWise demo\. AWS IoT SiteWise provides the demo as an AWS CloudFormation template that you can deploy to create asset models, assets, and a SiteWise Monitor portal, and generate sample data for up to a week\.

**Important**  
You will be charged for the resources that this demo creates and consumes\. 

**Topics**
+ [Creating the AWS IoT SiteWise demo](#create-getting-started-demo)
+ [Deleting the AWS IoT SiteWise demo](#delete-getting-started-demo)

## Creating the AWS IoT SiteWise demo<a name="create-getting-started-demo"></a>

You can create the AWS IoT SiteWise demo from the AWS IoT SiteWise console\.

**Note**  
The demo creates Lambda functions, one CloudWatch Events rule, and the IAM roles required for the demo\. You might see these resources in your AWS account\. We recommend that you keep these resources until you're done with the demo\. If you delete the resources, the demo might stop working correctly\.

**To create the demo in the AWS IoT SiteWise console**

1. Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/) and find the **SiteWise demo** in the upper\-right corner of the page\.

1. \(Optional\) Under **SiteWise demo**, change the **Days to keep demo assets** field to specify how many days to keep the demo before deleting it\.

1. \(Optional\) To create a SiteWise Monitor portal to monitor sample data, do the following\.
**Note**  
You will be charged for the SiteWise Monitor resources that this demo creates and consumes\. For more information, see [SiteWise Monitor](https://aws.amazon.com/iot-sitewise/pricing/) in the *AWS IoT SiteWise Pricing*\.

   1. Choose **SiteWise Monitor**\.

   1. Choose **Permission**\.

   1. Choose an existing IAM role that grants your federated IAM users access to the portal\.
**Important**  
Your IAM role must have the following permissions\.  

      ```
      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "iotsitewise:Describe*",
                      "iotsitewise:List*",
                      "iotsitewise:Get*",
                      "cloudformation:DescribeStacks",
                      "iam:GetPolicyVersion",
                      "iam:GetPolicy",
                      "iam:ListAttachedRolePolicies",
                      "sso:DescribeRegisteredRegions",
                      "organizations:DescribeOrganization"
                  ],
                  "Resource": "*"
              }
          ]
      }
      ```

   For more information about how to work with SiteWise Monitor, see [What is AWS IoT SiteWise Monitor?](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/what-is-monitor-app.html) in the *AWS IoT SiteWise Monitor Application Guide*\.

1. Choose **Create demo**\.

   The demo takes around 3 minutes to create\. If the demo fails to create, your account might have insufficient permissions\. Switch to an account that has administrative permissions, or use the following steps to delete the demo and try again:

   1. Choose **Delete demo**\.

      The demo takes around 15 minutes to delete\.

   1. If the demo doesn't delete, open the [AWS CloudFormation console](https://console.aws.amazon.com/cloudformation/), choose the stack named **IoTSiteWiseDemoAssets**, and choose **Delete** in the upper\-right corner\.

   1. If the demo fails to delete again, follow the steps in the AWS CloudFormation console to skip the resources that failed to delete, and try again\.

1. After the demo creates successfully, you can explore the demo assets and data in the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

## Deleting the AWS IoT SiteWise demo<a name="delete-getting-started-demo"></a>

The AWS IoT SiteWise demo deletes itself after a week, or the number of days you chose if you created the demo stack from the AWS CloudFormation console\. You can delete the demo before if you're done using the demo resources\. You can also delete the demo if the demo fails to create\. Use the following steps to delete the demo manually\.

**To delete the AWS IoT SiteWise demo**

1. Navigate to the [AWS CloudFormation console](https://console.aws.amazon.com/cloudformation)\.

1. Choose **IoTSiteWiseDemoAssets** from the list of **Stacks**\.

1. Choose **Delete**\.

   When you delete the stack, all of the resources created for the demo are deleted\.

1. In the confirmation dialog, choose **Delete stack**\.

   The stack takes around 15 minutes to delete\. If the demo fails to delete, choose **Delete** in the upper\-right corner again\. If the demo fails to delete again, follow the steps in the AWS CloudFormation console to skip the resources that failed to delete, and try again\.