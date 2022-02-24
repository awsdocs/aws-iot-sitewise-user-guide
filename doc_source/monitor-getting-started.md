# Getting started with AWS IoT SiteWise Monitor<a name="monitor-getting-started"></a>

If you're the AWS administrator for your organization, you create portals from the AWS IoT SiteWise console\. Complete the following steps to create a portal so that members of your organization can view your AWS IoT SiteWise data:

1. Configure and create a portal

1. Add portal administrators and send invitation emails

1. Add portal users

After you create a portal, the portal administrator can view your AWS IoT SiteWise assets and assign them to projects in the portal\. Project owners can then create dashboards to visualize the properties of the assets that help project viewers understand how your devices, processes, and equipment are performing\.

You can follow a tutorial that walks through the steps required to set up a portal with a project, dashboards, and multiple users for a specific scenario using wind farm data\. For more information, see [Visualizing and sharing wind farm data in AWS IoT SiteWise Monitor](monitor-wind-farm.md)\.

## Creating a portal<a name="monitor-create-portal"></a>

You create a SiteWise Monitor portal in the AWS IoT SiteWise console\.

**To create a portal**

1. Sign in to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/home)\.

1. In the navigation pane, choose **Monitor**, **Getting started**\.  
![\[The left navigation pane of the AWS IoT SiteWise console with Getting started highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-choose-monitor-getting-started-console.png)

1. Choose **Create Portal**\.  
![\[The AWS IoT SiteWise Monitor Getting started page with Create portal highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-choose-create-portal-console.png)

   Next, you must provide some basic information to configure your portal\.

## Configuring your portal<a name="monitor-configure-portal"></a>

Your users use portals to view your data\. You can customize a portal's name, description, branding, user authentication, support contact email, and permissions\.

![\[The "Portal configuration" page used to create a portal.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/PortalConfiguration.png)

**To configure a portal**

1. Enter a name for your portal\.

1. \(Optional\) Enter a description for your portal\. If you have multiple portals, use meaningful descriptions to help you keep track of what each portal contains\.

1. \(Optional\) Upload an image to display your brand in the portal\. Choose a square, PNG image\. If you upload a non\-square image, the portal scales the image down to a square\.

1. Choose one of the following options:
   + Choose **AWS SSO** if your portal users sign in to this portal with their corporate user names and passwords\.

     If you haven't enabled AWS SSO in your account, do the following:

     1. Choose **Create user**\.

     1. On the **Create user** page, to create the first portal, enter the user's email address, first name, and last name, and then choose **Create user**\.  
![\[Enable AWS SSO if you haven't enable AWS SSO in your AWS account.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/SSOUserCreation.png)
**Note**  
AWS automatically enables AWS SSO in your account when you create the first portal user\.
<a name="cross-region-sso"></a>You can configure AWS SSO in only one Region at a time\. SiteWise Monitor connects to the Region that you configured for AWS SSO\. This means that you use one Region for AWS SSO access, but you can create portals in any Region\.
     + Choose **IAM** if your portal users sign in to this portal with their IAM credentials\.
**Important**  <a name="iam-portal-user-permissions"></a>
IAM users or roles must have the `iotsitewise:DescribePortal` permission to sign in to the portal\.

1. Enter an email address that portal users can contact when they have an issue with the portal and need help to resolve it\.

1. \(Optional\) Add tags for your portal\. For more information, see [Tagging your AWS IoT SiteWise resources](tag-resources.md)\.

1. Choose one of the following options:
   + Choose **Create and use a new service role**\. By default, SiteWise Monitor automatically creates a service role for each portal\. This role allows your portal users to access your AWS IoT SiteWise resources\. For more information, see [Using service roles for AWS IoT SiteWise Monitor](monitor-service-role.md)\.
   + Choose **Use an existing service role**, and then choose the target role\.

1. Choose **Next**

1. \(Optional\) Enable alarms for your portal\. For more information, see [Enabling additional features for portals](monitor-additional-features.md)\.

1. Choose **Create**\. AWS IoT SiteWise will create your portal\.
**Note**  
 If you close the console, you can finish the setup process by adding administrators and users\. For more information, see [Adding or removing portal administrators](administer-portals.md#portal-change-admins)\. If you don't want to keep this portal, delete it so it doesn't use resources\. For more information, see [Deleting a portal](administer-portals.md#portal-delete-portal)\.

The **Status** column can be one of the following values\.
+ **CREATING** ‐ AWS IoT SiteWise is processing your request to create the portal\. This process can take several minutes to complete\.
+ **UPDATING** ‐ AWS IoT SiteWise is processing your request to update the portal\. This process can take several minutes to complete\.
+ **PENDING** ‐ AWS IoT SiteWise is waiting for the DNS record propagation to finish\. This process can take several minutes to complete\. You can delete the portal while the status is **PENDING**\.
+ **DELETING** ‐ AWS IoT SiteWise is processing your request to delete the portal\. This process can take several minutes to complete\. 
+ **ACTIVE** ‐ When the portal becomes active, your portal users can access it\.
+ **FAILED** ‐ AWS IoT SiteWise couldn't process your request to create, update, or delete the portal\. If you enabled AWS IoT SiteWise to send logs to CloudWatch Logs, you can use these logs to troubleshoot issues\. For more information, see [ Monitoring AWS IoT SiteWise with CloudWatch Logs](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/monitor-cloudwatch-logs.html)\. 

A message appears when your portal is created\.

![\[An example successful portal creation message.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-create-portal-success-console.png)

Next, you must invite one or more portal administrators to the portal\. So far, you created a portal but no one can access it\.

## Inviting administrators<a name="monitor-invite-administrators"></a>

To get started in your new portal, you must assign a portal administrator\. The portal administrator creates projects, chooses project owners, and assigns assets to projects\. Portal administrators can see all of your AWS IoT SiteWise assets\.

Based on the user authentication service, choose one of the following options:

------
#### [ AWS SSO ]

If you're using SiteWise Monitor for the first time, you can choose the user that you created earlier to be the portal administrator\. If you want to add another user as a portal administrator, you can create an AWS SSO user from this page\. Alternatively, you can connect an external identity provider to AWS SSO\. For more information, see the [AWS Single Sign\-On User Guide](https://docs.aws.amazon.com/singlesignon/latest/userguide/)\.

**To invite administrators**

1. Select the check boxes for the users that you want as your portal administrators\. This adds the users to the **Portal administrators** list\.
**Note**  
If you use AWS SSO as your identity store, and you're signed in to your AWS Organizations management account, you can choose **Create user** to create an AWS SSO user\. AWS SSO sends the new user an email for them to set their password\. You can then assign the user to the portal as an administrator\. For more information, see [Manage identities in AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-sso.html.html)\.

1. \(Optional\) Choose **Send invite to selected users**\. Your email client opens, and an invitation is populated in the message body, as shown in the following example\.  
![\[The invitation email body that is sent to your AWS SSO portal administrators.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/SSOAdminInviteEmail.png)

   You can customize the email before you send it to your portal administrators\. You can also send the email to your portal administrators later\. If you're trying SiteWise Monitor for the first time and adding your new AWS SSO or IAM user or role as the portal administrator, you don't need to email yourself\.

1. If you add a user that you don't want as an administrator, clear the check box for that user\.

1. When you're finished inviting portal administrators, choose **Next**\.

![\[The invite AWS SSO administrators step of the portal creation process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/SSOAdminInvite.png)

------
#### [ IAM ]

You can choose an IAM user or role to be the portal administrator\. If you want to add another IAM user or role as a portal administrator, you can create an user or role in the IAM console\. For more information, see [Creating an IAM user in your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) and [Creating IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create.html) in the *IAM User Guide*\.

**To invite administrators**

1. Do the following:
   + Choose **IAM users** to add an IAM user as your portal administrator\.
   + Choose **IAM roles** to add an IAM role as your portal administrator\.

1. Select the check boxes for the users or roles that you want as your portal administrators\. This adds the users or roles to the **Portal administrators** list\.

1. If you add a user or role that you don't want as an administrator, clear the check box for that user or role\.

1. When you're finished inviting portal administrators, choose **Next**\.

**Important**  <a name="iam-portal-user-permissions"></a>
IAM users or roles must have the `iotsitewise:DescribePortal` permission to sign in to the portal\.

**Note**  
If you use AWS SSO as your identity store, and you're signed in to your AWS Organizations management account, you can choose **Create user** to create an AWS SSO user\. AWS SSO sends the new user an email for them to set their password\. You can then assign the user to the portal as an administrator\. For more information, see [Manage identities in AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-sso.html.html)\.

![\[The invite AWS SSO user administrators step of the portal creation process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/IAMUserAdminInvite.png)

![\[The invite AWS SSO role administrators step of the portal creation process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/IAMRoleAdminInvite.png)

------

You can change the list of portal administrators later\. For more information, see [Adding or removing portal administrators](administer-portals.md#portal-change-admins)\.

**Note**  
Because only a portal administrator can create projects and assign assets to them, you should specify at least one portal administrator\.

As the last step, you add users who can access your new portal\.

## Adding portal users<a name="monitor-add-portal-users"></a>

You control which users have access to your portals\. In each portal, the portal administrators create one or more projects and assign portal users as owners or viewers for each project\. Each project owner can invite additional portal users to own or view the project\.

Based on the user authentication service, choose one of the following options:

------
#### [ AWS SSO ]

If you want to add a user to the **Users** list, complete the following steps\.

**To add portal users**

1. Choose users from the **Users** list to add to the portal\. This adds the users to the **Portal users** list\. If you're using SiteWise Monitor for the first time, you don't need to add your portal administrator as a portal user\.
**Note**  
If you use AWS SSO as your identity store, and you're signed in to your AWS Organizations management account, you can choose **Create user** to create an AWS SSO user\. AWS SSO sends the new user an email for them to set their password\. You can then assign the user to the portal as a user\. For more information, see [Manage identities in AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-sso.html.html)\.

1. If you add a user that you don't want to have access to the portal, clear the check box for that user\.

1. When you're finished selecting users, choose **Assign users**\.

![\[The assign AWS SSO users step of the portal creation process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/SSOUserAssign.png)

------
#### [ IAM ]

If you see the user or role that you want to add in the **IAM users** or **IAM roles** list, complete the following steps\.

**To add portal users**

1. Do the following options:
   + Choose **IAM users** to add an IAM user as a portal user\.
   + Choose **IAM roles** to add an IAM role as a portal user\.

   If you're using SiteWise Monitor for the first time, you don't need to add your portal administrator as a portal user\.

1. Select the check boxes for the users or roles that you want as portal users\. This adds the users or roles to the **Portal users** list\.

1. If you add a user that you don't want to have access to the portal, clear the check box for that user\.

1. When you're finished selecting users, choose **Assign users**\.

**Important**  <a name="iam-portal-user-permissions"></a>
IAM users or roles must have the `iotsitewise:DescribePortal` permission to sign in to the portal\.

![\[The assign IAM users step of the portal creation process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/IAMUserAssign.png)

![\[The assign IAM step of the portal creation process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/IAMRoleAssign.png)

------

Congratulations\! You successfully created a portal, assigned portal administrators, and assigned users who can use that portal when invited to do so\. Your portal administrators can now create projects and add assets to those projects\. Then, your project owners can create dashboards to visualize the data for each project's assets\.

You can change the list of portal users later\. For more information, see [Adding or removing portal users](administer-portals.md#portal-change-users)\.

If you need to make changes to the portal, see [Administering your SiteWise Monitor portals](administer-portals.md)\.

To get started in the portal, see [Getting started](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/getting-started) in the *SiteWise Monitor Application Guide*\.