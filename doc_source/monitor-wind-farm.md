# Visualizing and sharing wind farm data in AWS IoT SiteWise Monitor<a name="monitor-wind-farm"></a>

You can configure AWS IoT SiteWise Monitor to visualize and share your industrial data through managed web applications\. Each web application is called a portal\. Each portal contains projects, and you choose which data is available in each project\. 

You can then specify people in your company that can access each portal\. Your users sign in to portals using AWS Single Sign\-On accounts, so you can use your existing identity store or an AWS\-managed one\.

You, and your users with sufficient permissions, can create dashboards in each project to visualize your industrial data in meaningful ways\. Then, your users can view these dashboards to quickly gain insights into your data and monitor your operation\. You can configure administrative or read\-only permissions to each project for every user in your company\. For more information, see [Monitoring data with AWS IoT SiteWise Monitor](monitor-data.md)\.

In this tutorial, you build on the AWS IoT SiteWise demo that provides a sample set of data for a wind farm\. You configure a portal in SiteWise Monitor and create a project and dashboards to visualize the wind farm data\. Then, you create additional users who you give permissions to own or view the project and its dashboards\.

**Note**  
When you use SiteWise Monitor, you're charged per AWS SSO user that signs in to a portal \(per month\)\. In this tutorial, you create three users, but you only need to sign in with one user\. After you complete this tutorial, you incur charges for one user\. For more information, see [AWS IoT SiteWise Pricing](https://aws.amazon.com/iot-sitewise/pricing/)\.

**Topics**
+ [Prerequisites](#monitor-tutorial-prerequisites)
+ [Creating a portal in SiteWise Monitor](#monitor-tutorial-create-portal)
+ [Signing in to a portal](#monitor-tutorial-sign-in-portal)
+ [Creating a wind farm project](#monitor-tutorial-create-project)
+ [Creating dashboards to visualize wind farm data](#monitor-tutorial-create-dashboard)
+ [Creating AWS SSO users](#monitor-tutorial-create-users)
+ [Adding AWS SSO users to a portal](#monitor-tutorial-add-portal-users)
+ [Assigning users to a project](#monitor-tutorial-assign-users)
+ [Cleaning up resources after the tutorial](#monitor-tutorial-clean-up-resources)

## Prerequisites<a name="monitor-tutorial-prerequisites"></a>

To complete this tutorial, you need the following:
+ An AWS account\. If you don't have one, see [Setting up an AWS account](set-up-aws-account.md)\.
+ A development computer running Windows, macOS, Linux, or Unix to access the AWS Management Console\. For more information, see [Getting Started with the AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/getting-started.html)\.
+ An IAM user with administrator permissions\.
+ A running AWS IoT SiteWise wind farm demo\. When you set up the demo, it defines models and assets in AWS IoT SiteWise and streams data to them to represent a wind farm\. For more information, see [Using the AWS IoT SiteWise demo](getting-started-demo.md)\.

## Creating a portal in SiteWise Monitor<a name="monitor-tutorial-create-portal"></a>

In this procedure, you create a portal in SiteWise Monitor\. Each portal is a managed web application that you and your users can sign in to with AWS Single Sign\-On accounts\. AWS SSO lets you use your company's existing identity store or create one managed by AWS\. Your company's employees can sign in without creating separate AWS accounts\.

**To create a portal**

1. Sign in to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. Review the [AWS Regions](getting-started.md#requirements) where AWS IoT SiteWise is supported and switch Regions, if needed\. If you already set up AWS SSO, you must switch to the Region where you have AWS SSO configured\. You must run the AWS IoT SiteWise demo in the same Region\. For more information, including instructions in case you set up AWS SSO in a Region that AWS IoT SiteWise doesn't support, see [Enabling AWS SSO](monitor-getting-started.md#monitor-enable-sso)\.

1. In the left navigation pane, choose **Portals**\.

1. Choose **Create portal**\.

1. If you already enabled AWS SSO in the current Region, skip to step 6\. Otherwise, complete the following steps to enable AWS SSO:

   1. On the **Enable AWS Single Sign\-On \(SSO\)** page, enter your **Email address**, **First name**, and **Last name** to create an AWS SSO user for yourself to be the portal administrator\. Use an email address you can access so that you can receive an email to set a password for your new AWS SSO user\.

      In a portal, the portal administrator creates projects and assigns users to projects\. You can create more users later\.  
![\[The "Enable AWS Single Sign-On (SSO)" page of the "Create portal" process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-enable-sso-console.png)

   1. Choose **Create user**\.

1. On the **Portal configuration** page, complete the following steps:

   1. Enter a name for your portal, such as **WindFarmPortal**\.

   1. \(Optional\) Enter a description for your portal\. If you have multiple portals, use meaningful descriptions to keep track of what each portal contains\.

   1. Enter an email address that portal users can contact when they have an issue with the portal and need help from your company's AWS administrator to resolve it\.

   1. Choose **Create portal**\.  
![\[The "Portal configuration" page of the "Create portal" process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sitewise-configure-portal-console.png)

1. On the **Invite administrators** page, complete the following steps:

   1. Choose a user to be the portal administrator\. If you're using SiteWise Monitor for the first time, choose the user that you created when you enabled AWS SSO earlier in this tutorial\.

   1. \(Optional\) Choose **Send invite to selected users**\. Your email client opens, and an invitation is populated in the message body\. You can customize the email before you send it to your portal administrators\. You can also send the email to your portal administrators later\. If you're trying SiteWise Monitor for the first time and will be the portal administrator, you don't need to email yourself\.

   1. Choose **Next**\.  
![\[The "Invite administrators" page of the "Create portal" process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sitewise-invite-portal-administrators-console.png)

1. On the **Assign users** page, choose **Assign users** to create the portal\. You can assign portal users that are the end users of your portal\. The portal administrator can later assign these users as project owners, who can create dashboards in projects, or project viewers, who have read\-only access to the projects that they're assigned\. You can create a portal without assigning portal users\.  
![\[The "Assign users" page of the "Create portal" process.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sitewise-assign-portal-users-console.png)

   The portals page opens with your new portal listed\.

## Signing in to a portal<a name="monitor-tutorial-sign-in-portal"></a>

In this procedure, you sign in to your new portal using the AWS SSO user that you added to the portal\.

**To sign in to a portal**

1. On the **Portals** page, choose your new portal's **Link** to open your portal in a new tab\.  
![\[The "Portals" page with the wind farm portal's link highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sitewise-choose-portal-link-console.png)

1. If you created your first AWS SSO user earlier in the tutorial, use the following steps to create a password for your user:

   1. Check your email for the subject line **Invitation to join AWS Single Sign\-On**\.

   1. Open that invitation email and choose **Accept invitation**\.

   1. In the new window, set a password for your AWS SSO user\.
**Note**  
If you didn't receive an email, you can generate a password for your user in the AWS SSO console\. For more information, see [Reset a user password](https://docs.aws.amazon.com/singlesignon/latest/userguide/resetuserpwd.html) in the *AWS Single Sign\-On User Guide*\.

1. Enter your AWS SSO **Username** and **Password**\. If you enabled AWS SSO earlier in this tutorial, your **Username** is the email address of the portal administrator user that you created\.

   All portal users, including the portal administrator, must sign in with their AWS SSO user credentials\. These credentials are typically not the same credentials that you use to sign in to the AWS Management Console\.  
![\[The portal sign-in page.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/portal-sign-in-console.png)

1. Choose **Sign in**\.

   Your portal opens\.

## Creating a wind farm project<a name="monitor-tutorial-create-project"></a>

In this procedure, you create a project in your portal\. Projects are resources that define a set of permissions, assets, and dashboards, which you can configure to visualize asset data in that project\. You can assign other portal users as owners or viewers of each project\. Project owners create and maintain dashboards to visualize data\. Project owners also assign viewers to projects to grant access to dashboards and data\. With projects, you define who has access to which subsets of your operation and how those subsets' data is visualized\.

**To create a wind farm project**

1. In the left navigation pane in your portal, choose the **Asset library** tab\. In the asset library, you can explore all assets available in the portal and add assets to projects\.

1. In the asset browser, choose **Demo Wind Farm Asset**\. When you choose an asset in the asset library, you can explore that asset's live and historical data\. You can also press Shift to select multiple assets and compare their data side\-by\-side\.

1. Choose **Add asset to project** in the upper right\. Projects contain dashboards that your portal users can view to explore your data\. Each project has access to a subset of your assets in AWS IoT SiteWise\. When you add an asset to a project, all users with access to that project can also access data for that asset and its children\.  
![\[The "Asset library" page with the demo wind farm asset and "Add asset to project" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/portal-add-asset-project-console.png)

1. In the **Add asset to project** dialog, choose **Create new project**, and then choose **Next**\.  
![\[The "Add asset to project" dialog with "Create new project" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/portal-choose-new-project-console.png)

1. In the **Create new project** dialog, enter a **Project name** and **Project description** for your project, and then choose **Add asset to project**\.  
![\[The "Create new project" dialog.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/portal-create-new-project-console.png)

   Your new project's page opens\.

## Creating dashboards to visualize wind farm data<a name="monitor-tutorial-create-dashboard"></a>

In this procedure, you create dashboards to visualize the demo wind farm data\. Dashboards contain customizable visualizations of your project's asset data\. Each visualization can have a different type, such as a line chart, bar chart, or KPI display\. You can choose the visualization type that works best for your data\. Project owners can edit dashboards, while project viewers can only view them to gain insights\.

**To create a dashboard with visualizations**

1. On your new project's page, choose **Create dashboard**\.

1. In the dashboard, choose **Edit** in the upper right\.

   In a dashboard's edit page, you can drag asset properties from the asset hierarchy to the dashboard to create visualizations\. Then, you can edit each visualization's title, legend titles, type, size, and location in the dashboard\.

1. In the edit view, rename your dashboard\.  
![\[The "Dashboard" edit page with the dashboard name highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/dashboard-edit-console.png)

1. Drag **Total Average Power** from the **Demo Wind Farm Asset** to the dashboard to create a visualization\.  
![\[The "Dashboard" edit page with the "Average Total Power" property highlighted to demonstrate dragging an asset property to the dashboard.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/dashboard-add-total-power-console.png)

1. Choose the arrow next to **Demo Wind Farm Asset** to expand the wind farm asset hierarchy and view all of the wind turbine assets that you made available to your project earlier\.  
![\[The "Dashboard" edit page with the arrow next to the demo wind farm asset highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/dashboard-expand-asset-hierarchy-console.png)

1. Under **Demo Turbine Asset 1**, drag **Wind Speed** to the space next to the **Total Average Power** visualization to create a visualization for wind speed\.  
![\[The "Dashboard" edit page with a wind turbine's "Wind Speed" property highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/dashboard-add-wind-speed-console.png)

1. Add **Wind Speed** to the new wind speed visualization for each **Demo Turbine Asset 2**, **3**, and **4** \(in that order\)\.

   Your **Wind Speed** visualization should look similar to the following screenshot\.  
![\[A "Wind Speed" visualization that contains four demo wind turbine assets' wind speeds.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/dashboard-add-all-wind-speeds-console.png)

1. Repeat steps 6 and 7 for the wind turbines' **Torque \(KiloNewton Meter\)** properties to create a visualization for wind turbine torque\. Create this visualization in the space below the **Total Average Power** visualization\.

1. Choose the visualization type icon for the **Torque \(KiloNewton Meter\)** visualization, and then choose the bar chart icon\.  
![\[A "Torque (KiloNewton Meter)" visualization with the visualization type and bar chart icons highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/dashboard-change-torque-visualization-type-console.png)

1. Repeat steps 6 and 7 for the wind turbines' **Wind Direction** properties to create a visualization for wind direction\. Create this visualization in the space below the **Wind Speed** visualization\.

1. Choose the visualization type icon for the **Wind Direction** visualization, and then choose the KPI chart icon \(**30%**\)\.  
![\[A "Wind Direction" visualization with the visualization type and KPI chart icons highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/dashboard-change-wind-direction-visualization-type-console.png)

1. \(Optional\) Make other changes to each visualization's title, legend titles, type, size, and location as needed\.

1. Choose **Done** in the upper right to save your dashboard\.

   Your dashboard should look similar to the following screenshot\.  
![\[A complete wind farm dashboard.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/wind-farm-dashboard-console.png)

1. \(Optional\) Create an additional dashboard for each wind turbine asset\.

   As a best practice, we recommend that you create a dashboard for each asset so that your project viewers can investigate any issues with each individual asset\. You can only add up to 5 assets to each visualization, so you must create multiple dashboards for your hierarchical assets in many scenarios\.

   A dashboard for a demo wind turbine might look similar to the following screenshot\.  
![\[A complete wind turbine dashboard.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/wind-turbine-dashboard-console.png)

1. \(Optional\) Change the timeline or select data points on a visualization to explore the data in your dashboard\. For more information, see [Viewing dashboards](https://docs.aws.amazon.com/iot-sitewise/latest/appguide/view-dashboards.html) in the *AWS IoT SiteWise Monitor Application Guide*\.

## Creating AWS SSO users<a name="monitor-tutorial-create-users"></a>

In this procedure, you create additional AWS SSO users that you can add to your portal\. After you have additional users in your portal, you can add them as owners or viewers of your projects to share your operational data\.

**To create AWS SSO users**

1. Navigate to the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. In the left navigation pane, choose **Users**\.

1. Choose **Add user**\.

1. Enter details for your new AWS SSO user, then choose **Next: Groups**\. Later in this tutorial, you make this user an owner of your wind farm project\.  
![\[AWS SSO "Add user" page.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sso-create-user-console.png)

1. On the **Add users to groups** page, choose **Add user**\.

   You should see a confirmation similar to that shown in the following screenshot\.  
![\[AWS SSO "Users" page with a confirmation that the new user is added.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sso-user-added-success-console.png)

1. Repeat steps 3 through 5 to create another AWS SSO user\. Later in this tutorial, you make this user a viewer of your wind farm project\.  
![\[AWS SSO "Users" page with a confirmation that the second new user is added.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sso-user-added-success2-console.png)

## Adding AWS SSO users to a portal<a name="monitor-tutorial-add-portal-users"></a>

In this procedure, you add your new AWS SSO users to your wind farm portal\. After you add users to a portal, you can add them to projects as owners or viewers within that portal\.

**To add AWS SSO users to a portal**

1. Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the left navigation pane, choose **Portals**\.

1. Choose your portal, **WindFarmPortal**\.  
![\[The "Portals" page with the wind farm portal highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sitewise-choose-portal-console.png)

1. Under **Portal users**, choose **Assign users**\.  
![\[The "Portal details" page with "Assign users" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sitewise-choose-assign-portal-users-console.png)

1. Choose the two AWS SSO users that you created in the previous procedure, and then choose **Assign users**\.  
![\[The "Assign users" page with the new AWS SSO users highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sitewise-choose-users-to-assign-console.png)

   In the portal, you can now assign these AWS SSO users to projects as owners or viewers\.

## Assigning users to a project<a name="monitor-tutorial-assign-users"></a>

In this procedure, you assign your new AWS SSO users as owners or viewers of your wind farm project\. Project owners can edit dashboards and share the project with other users\. Project viewers can view dashboards but not edit them\. For more information about roles in SiteWise Monitor, see [SiteWise Monitor roles](monitor-data.md#monitor-roles)\.

**To assign users to a project as owners or viewers**

1. Navigate to your portal, **WindFarmPortal**, and sign in as your portal administrator \(for example, **john\.doe@example\.com**\)\.

1. In the left navigation pane, choose **Projects**\.

1. Choose your project, **Wind Farm 1**\.  
![\[The "Projects" page with the wind farm project highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/portal-choose-project-console.png)

1. Under **Project owners**, choose **Add owners** or **Edit users**\.  
![\[The "Project details" page with "Assign users" and "Edit users" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/project-add-users-console.png)

1. Choose the user to add as a project owner \(for example, **Mary Major**\), and then choose the **>>** icon\.  
![\[The "Project owners" dialog with a user highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/project-choose-owner-console.png)

1. Choose **Save**\.  
![\[The "Project owners" dialog with "Save" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/project-save-owner-console.png)

   Your AWS SSO user **Mary Major** can sign in to this portal to edit the dashboards in this project and share this project with other users in this portal\.

1. Under **Project viewers**, choose **Add viewers**\.

1. Choose the user to add as a project viewer, and then choose the **>>** icon\.

1. Choose **Save**\.

   Your other AWS SSO user can sign in to this portal to view, but not edit, the dashboards in the wind farm project\.

1. \(Optional\) Sign in to the portal as your new project owner or project viewer accounts to explore the portal as a user with fewer permissions than a portal administrator\.
**Note**  
You're charged for each AWS SSO user that signs in to a portal, so you incur charges if you sign in as these users\. For more information, see [AWS IoT SiteWise Pricing](https://aws.amazon.com/iot-sitewise/pricing/)\.

1. Now that you completed the tutorial, continue to explore your demo wind farm in SiteWise Monitor\. When you're done, follow the next procedure to clean up your resources\.

## Cleaning up resources after the tutorial<a name="monitor-tutorial-clean-up-resources"></a>

After you complete the tutorial, you can clean up your resources\. You aren't charged for SiteWise Monitor if users don't sign in to your portal, but you can delete your portal and AWS SSO users\. Your demo wind farm assets are deleted at the end of the duration that you chose when you created the demo, or you can delete the demo manually\. For more information, see [Deleting the AWS IoT SiteWise demo](getting-started-demo.md#delete-getting-started-demo)\.

Use the following procedures to delete your portal and AWS SSO users\.

**To delete a portal**

1. Navigate to the [AWS IoT SiteWise console](https://console.aws.amazon.com/iotsitewise/)\.

1. In the left navigation pane, choose **Portals**\.

1. Choose your portal, **WindFarmPortal**, and then choose **Delete**\.

   When you delete a portal or project, the assets associated to deleted projects aren't affected\.  
![\[The "Portals" page with the wind farm portal and "Delete" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sitewise-choose-delete-portal-console.png)

1. In the **Delete portal** dialog, choose **Remove administrators and users**\.  
![\[The "Delete portal" dialog with "Remove administrators and users" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-delete-portal-remove-users-console.png)

1. Enter **delete** to confirm deletion, and then choose **Delete**\.  
![\[The "Delete portal" dialog with "Delete" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/sitewise-delete-portal-confirm-delete-console.png)

**To delete AWS SSO users**

1. Navigate to the [AWS SSO console](https://console.aws.amazon.com/singlesignon)\.

1. In the left navigation pane, choose **Users**\.

1. Select the check box for each user to delete, and then choose **Delete users**\.  
![\[AWS SSO "Users" page with "Delete users" highlighted.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sso-choose-delete-users-console.png)

1. In the **Delete users** dialog, enter **DELETE**, and then choose **Delete users**\.  
![\[AWS SSO "Delete users" dialog.\]](http://docs.aws.amazon.com/iot-sitewise/latest/userguide/images/monitor-wind-farm/sso-delete-users-console.png)