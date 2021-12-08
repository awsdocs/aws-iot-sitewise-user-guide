# Installing the gateway software<a name="install-gateway-software"></a>

This section shows you how to install the gateway software on your gateway device\.

**Important**  
Make sure that your gateway device connects to the Internet\.

**Topics**
+ [Step 1: Copy the installer to your gateway device](#connect-gateway-device-ssh)
+ [Step 2: Set up your environment](#set-up-gateway-environment)
+ [Step 3: Install the gateway software](#set-up-gateway-device)

## Step 1: Copy the installer to your gateway device<a name="connect-gateway-device-ssh"></a>

The following uses SSH to connect to your getway device\. You can use a USB flash drive or other tools to transfer the installer file to your gateway device\.

### Connect to your gateway device using SSH<a name="connect-gateway-device"></a>

The following instructions explain how to connect to your gateway device using an SSH client\.

#### Prerequisites<a name="ssh-prereqs"></a>

Before you connect to your device, complete the following prerequisites\.
+ Get the IP address and user name to connect to your device\.
+ Install an SSH client on your local computer as needed\.

  Your local computer might have an SSH client installed by default\. You can verify this by typing ssh at the command line\. If your computer doesn't recognize the command, you can install an SSH client\.
  + Recent versions of Windows Server 2019 and Windows 10 \- OpenSSH is included as an installable component\. For more information, see [OpenSSH in Windows](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_overview)\.
  + Earlier versions of Windows \- Download and install OpenSSH\. For more information, see [Win32\-OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/wiki)\.
  + Linux and macOS X \- Download and install OpenSSH\. For more information, see [https://www\.openssh\.com](https://www.openssh.com/)\.

1. To connect to your device, run the following command in a terminal window on your computer\.
**Note**  
Replace *username* and *IP* with your user name and IP address\.

   ```
   ssh username@IP
   ```

1. To transfer the installer file that AWS IoT SiteWise generated to your gateway device, run the following command\.
**Note**  
Replace *path\-to\-saved\-installer* with the path on your computer that you used to save the installer file and the name of the installer file\.
Replace *IP\-address* with the IP address of your gateway device\.
Replace *directory\-to\-receive\-installer* with the path on your gateway device that you use to receive the installer file\.

   ```
   scp path-to-saved-installer.sh user-name@IP-address:directory-to-receive-installer
   ```

## Step 2: Set up your environment<a name="set-up-gateway-environment"></a>

Follow the steps in this section to set up a Linux device to use as your AWS IoT SiteWise gateway device\. These steps assume that you use a device with Ubuntu\. If you use a different Linux distribution, consult the relevant documentation for your device\.

**To set up a gateway device**

1. To set up a DNS compliant fully qualified hostname, run the following command in a terminal window on your gateway device\. Replace *hostname* with a qualified hostname \(for example, `sitewise-gateway-rhel.amazon.com`\)\.

   ```
   sudo hostnamectl set-hostname hostname
   ```
**Note**  
If you use a registered domain, you can configure the IPv4 address for the hostname\. In step 3, you must follow the second instruction\.
If you use a registered domain, in step 3, you must follow the first option\.

1. To verify the hostname, run the following command\.

   ```
   hostname -f
   ```

   Example output

   ```
   sitewise-gateway-rhel-pdx.amazon.com
   ```

   The output should be the hostname that you created in the previous step\.

1. Do one of the following:

   1. Add a DNS entry A record that resolves the IPv4 address for the hostname created in step 1\. For more info about A record, see [A record type](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html#AFormat) in the *Amazon Route 53 Developer Guide*\.

   1. Set the `/etc/hosts` file on the gateway device and all user managed client machines\.

   Add the following message to the `/etc/hosts` file on the gateway device and all user\-managed client machines\.
**Note**  
Replace *IPv4\-address* with your IPv4 address,
Replace *simple\-hostname* with the simple hostname\.
Replace *fully\-qualified\-hostname* with the hostname that you created in step 1\.

   ```
   IPv4-address simple-hostname fully-qualified-hostname
   ```

   Example

   ```
   127.0.0.0 sitewise-gateway sitewise-gateway.amazon.com
   ```

**Note**  
You must use the configured hostname to ssh into the gateway device instead of the IPv4 address\. Verify this before you run the installer\.
You can now use the configured hostname to sign in to the gateway on the AWS OpsHub for AWS IoT SiteWise application\.

## Step 3: Install the gateway software<a name="set-up-gateway-device"></a>

In the following procedures, run the commands in a terminal window on your gateway device\.

1. Give the installer file the execute permission\.

   ```
   chmod +x path-to-installer.sh
   ```

1. Run the insatller\.

   ```
   sudo ./path-to-installer.sh
   ```