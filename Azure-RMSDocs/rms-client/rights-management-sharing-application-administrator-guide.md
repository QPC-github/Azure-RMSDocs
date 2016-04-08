---
# required metadata

title: Rights Management sharing application administrator guide | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Rights Management sharing application administrator guide

Use the following information if you are responsible for the Microsoft Rights Management sharing application on an enterprise network, or if you want more technical information than is in the [Rights Management sharing application user guide](rights-management-sharing-application-user-guide.md) or [FAQ for Microsoft Rights Management Sharing Application for Windows](http://go.microsoft.com/fwlink/?LinkId=303971):

The RMS sharing application is best suited to work with Azure RMS, because this deployment configuration supports sending protected attachments to users in another organization, and options such as email notifications and document tracking with revocation.  However, with some limitations, it also works with the on-premises version, AD RMS. For a comprehensive comparison of features that are supported by Azure RMS and AD RMS, see [Comparing Azure Rights Management and AD RMS](../understand-explore/comparing-azure-rights-management-and-ad-rms.md). If you have AD RMS and want to migrate to Azure RMS, see [Migrating from AD RMS to Azure Rights Management](../plan-design/migrating-from-ad-rms-to-azure-rights-management.md).

## Automatic deployment for the Microsoft Rights Management sharing application
The Windows version of the RMS sharing application supports a scripted installation, which makes it suitable for enterprise deployments.

The only prerequisites for installations are that the computers run a minimum version of Windows 7 Service Pack 1, and that the Microsoft Framework, minimum version 4.0 is installed. If you need to install the Microsoft .NET Framework 4.0, you can [download it for installation from the Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=17718).

### To download the RMS sharing application for automatic deployment

1.  Go to the [Microsoft Rights Management sharing application for Windows](http://www.microsoft.com/download/details.aspx?id=40857) page in the Microsoft Download Center, and click **Download**.

2.  Select and download the files that you need. There are two client installation packages: one for Windows 64-bit (Microsoft Rights Management sharing application x64.zip), and another for Windows 32-bit (Microsoft Rights Management sharing application x86.zip).

3.  Extract the files from the compressed installation packages, for example, by double-clicking them. Then copy the extracted files to a network location that client computers can access.

The setup packages for the RMS sharing application supports different deployment scenarios and includes the following:

|Description|Deployment scenario|
|---------------|-----------------------|
|Microsoft Online Sign-In Assistant|Office 2010 and Azure RMS<br /><br />Office 2013 and Azure RMS if you have not installed the [June 9, 2015, update for Office 2013](https://support.microsoft.com/kb/3054853) (KB3054853)|
|Hotfix for Office (KB 2596501)|Office 2010 and Azure RMS<br /><br />Office 2010 and Active Directory RMS|
|Hotfix to enable the AD RMS Client 1.0 to work with Azure RMS (KB 2843630)|Office 2010 and Azure RMS<br /><br />Office 2010 and Active Directory RMS|
|AD RMS Client and the RMS sharing application|Office 2016 or Office 2013 and Azure RMS or Active Directory RMS<br /><br />Office 2010 and Azure RMS<br /><br />Office 2010 and Active Directory RMS<br /><br />RMS sharing application and Office add-in only|
|Office add-in for the ribbon|Office 2016 or Office 2013 and Azure RMS or Active Directory RMS<br /><br />Office 2010 and Azure RMS<br /><br />Office 2010 and Active Directory RMS<br /><br />RMS sharing application and Office add-in only|
|Azure Active Directory Rights Management preparation tool|Office 2010 and Azure RMS|
Use the following procedures to identify the commands required to deploy the RMS sharing application for these deployment scenarios:

-   **Office 2016 or Office 2013 and Azure RMS or Active Directory RMS**

    Your users are running Office 2016 or Office 2013, your organization uses Azure RMS or Active Directory RMS, and users collaborate with other organizations who use Azure RMS or Active Directory RMS.

-   **Office 2010 and Azure RMS**

    Your users are running Office 2010, your organization uses Azure RMS, and users collaborate with other organizations who use Azure RMS or Active Directory RMS.

-   **Office 2010 and Active Directory RMS**

    Your users are running Office 2010, your organization uses AD RMS, and users collaborate with other organizations who use Azure RMS.

-   **RMS sharing application and Office add-in only**

    Your users are running Office 2016, Office 2013, or Office 2010, your organization uses AD RMS, and users do not need to collaborate with other organizations who use Azure RMS. This installation lets you install just the sharing application and Office add-in.

> [!NOTE]
> In these scenarios, if your organization is running AD RMS, your users can receive protected content from other organizations who use Azure RMS, but your users cannot send protected content to users in an organization that uses Azure RMS. However, if your organization is running Azure RMS, your users can send and receive protected content from other organizations.

To complete the installation for each procedure, the computer must restart. You can initiate an automatic restart by using a command such as shutdown /i.

### To deploy the RMS sharing application for Office 2016 or Office 2013 and Azure RMS or Active Directory RMS

-   On each computer on which you want to install the RMS sharing application and related components, run the following command with elevated privileges:

    ```
    setup.exe /s
    ```

To verify success, see the [Verifying installation success](rights-management-sharing-application-administrator-guide.md#BKMK_verifyscripted) section in this topic.

### To deploy the RMS sharing application for Office 2010 and Azure RMS

1.  You must be the global administrator for your Office 365 or Azure Active Directory tenant so that you can get your organization’s certification service URL by running the Azure Active Directory Rights Management preparation tool. You need run this tool only once, on a single computer. You will use the certification service URL when you install the RMS sharing application on each computer:

    1.  Log in to a computer by using a local administrator account.

    2.  On that computer, [download and install the Microsoft Online Sign In Assistant](http://www.microsoft.com/download/details.aspx?id=28177).

    3.  Run the following command to see displayed on the screen the certification service URL, which you can then copy and save for the next step:

        -   For Windows 8.1 and Windows 8, 64-bit:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   For Windows 8.1 and  Windows 8, 32-bit:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   For Windows 7, 64-bit:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > This command might prompt you to enter your credentials for Azure. If the computer is not joined to a domain, you will be prompted. If the computer is joined to a domain, the tool might be able to use cached credentials.

2.  On each computer on which you will install the RMS sharing application, run the following command with elevated privileges:

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  On each computer on which you will install the RMS sharing application, users must run the following command (does not need elevated privileges). There are different ways to achieve this, including asking users to run the command (for example, a link in an email message or a link on the help desk portal) or you can add it to their logon script:

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

To verify success, see the [Verifying installation success](rights-management-sharing-application-administrator-guide.md#BKMK_verifyscripted) section in this topic.

### To deploy the RMS sharing application for Office 2010 and Active Directory RMS

1.  On each computer on which you will install the RMS sharing application, run the following command with elevated privileges:

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  On each computer on which you will install the RMS sharing application, users must run the following command (does not need elevated privileges). There are different ways to achieve this, including asking users to run the command (for example, a link in an email message or a link on the help desk portal) or you can add it to their logon script:

    -   For Windows 10, Windows 8.1  and Windows 8, 64-bit:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   For Windows 10, Windows 8.1 and Windows 8, 32-bit:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   For Windows 7, 64-bit:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

To verify success, see the [Verifying installation success](rights-management-sharing-application-administrator-guide.md#BKMK_verifyscripted) section in this topic.

### To install the RMS sharing application and Office add-in only

1.  Install the AD RMS Client and the RMS sharing application by using the following command:

    -   For 64-bit Windows:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   For 32-bit Windows:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    For example: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  Install the Office add-in by using the following commands:

    -   For 64-bit version of Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   For 32-bit version of Office:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    For example: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

To verify success, see the [Verifying installation success](rights-management-sharing-application-administrator-guide.md#BKMK_verifyscripted) section in this topic.

## Verifying installation success
You can use the installation log files to verify a successful installation.

### To verify installation success for the RMS sharing application for Office 2016 or Office 2013 and Azure RMS or Active Directory RMS

-   To verify success of the Setup.exe command, on each computer, search for the installation log file **RMInstaller.log** in the *%temp%\RMS_installer_&lt;guid&gt;* folder, and then identify the exit code.

    A successful installation has an exit code of 0 and any other number indicates a failed installation.

    Example log file name: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### To verify installation success for the RMS sharing application for Office 2010 and Azure RMS

1.  To verify success of the Setup.exe command, on each computer, search for the installation log file **RMInstaller.log** in the *%temp%\RMS_installer_&lt;guid&gt;* folder, and then identify the exit code.

    A successful installation has an exit code of 0 and any other number indicates a failed installation.

    Example log file name: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  To verify success for the RMSSetup.exe command, the user should have the following files created in their *%localappdata%\microsoft\drm* folder:

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    Example of a CLC-&#42;.drm file:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

### To verify installation success for the RMS sharing application for Office 2010 and Active Directory RMS

1.  To verify success of the Setup.exe command, on each computer, search for the installation log file in the *%temp%\RMS_installer_&lt;guid&gt;* folder, and identify the exit code.

    A successful installation has an exit code of 0 and any other number indicates a failed installation.

    Example log file name: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  To verify success of the aadrmprep.exe command, on each computer, search for the following text in the installation log file: **aadrmprep.exe exited with status SUCCESS**

    > [!NOTE]
    > Sometimes, this installation can run twice; the first occurrence fails and the second is successful.

    If you want to manually check the registry changes that this tool makes, they are as follows:

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationHomeRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

### To verify installation success for the RMS sharing application and Office add-in only

1.  To verify success of the Setup_ipviewer.exe command, search for the following text in the installation log file: **Installation success or error status: 0**

    Example lines from a successful installation:

    **MSI (s) (F0:B8) [14:19:57:854]: Product: Active Directory Rights Management Services Client 2.1 -- Installation completed successfully.**

    **MSI (s) (F0:B8) [14:19:57:854]: Windows Installer installed the product. Product Name: Active Directory Rights Management Services Client 2.1. Product Version: 1.0.1179.1. Product Language: 1033. Manufacturer: Microsoft Corporation. Installation success or error status: 0.**

2.  To verify success of the Office add-in, on each computer, search for the following text in the installation log file: **Installation success or error status: 0**

    Example lines from a successful installation:

    **MSI (s) (9C:88) [18:49:04:007]: Product: Microsoft RMS Office Addins -- Installation completed successfully.**

    **MSI (s) (9C:88) [18:49:04:007]: Windows Installer installed the product. Product Name: Microsoft RMS Office Addins. Product Version: 1.0.7. Product Language: 1033. Manufacturer: Microsoft. Installation success or error status: 0.**

## Uninstall commands
Not all of the installation commands that are required for these deployments support an uninstallation command. You can uninstall the AD RMS client and the sharing application, and you can uninstall the Office add-in. Use the following commands to uninstall these elements.

### To uninstall the AD RMS Client and the RMS sharing application

-   Use the following commands:

    -   For 64-bit Windows:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   For 32-bit Windows:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### To uninstall the Office add-in

-   Use the following commands:

    -   For 64-bit version of Office:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   For 32-bit version of Office:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## Suppressing automatic updates
By default, users are notified if there is a later version of the RMS sharing application, and prompted to download it. You can suppress this notification by making the following registry edit:

1.  Navigate to **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** and if not already present, create a new key named **RmsSharingApp**.

2.  Select **RmsSharingApp**, create a new DWORD Value of **AllowUpdatePrompt**, and set the value to **0**.

Because the RMS sharing application is not supported by WSUS, you can use the following technique to test any new versions of the RMS sharing application before deploying it to all users:

1.  On all users’ computers, run a script to suppress automatic updates. On the computers that administrators use to test new versions, do not run this script.

2.  When a new version is available, administrators download it and test it.

3.  When testing is complete and any issues resolved, deploy the latest version to all users by using the automatic deployment instructions in this guide.

## Azure RMS only: Configuring document tracking
If you have a [subscription that supports document tracking](https://technet.microsoft.com/en-us/dn858608), the document tracking site is enabled by default for all users in your organization.  Document tracking shows information such as email addresses of the people who attempted to access protected documents that users shared, when these people tried to access them, and their location. If displaying this information is prohibited in your organization because of privacy requirements, you can disable access to the document tracking site by using the  [Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) cmdlet. You can re-enable access to the site at any time, by using the [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037), and you can check whether access is currently enabled or disabled by using [Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037).

To run these cmdlets, you must have at least version **2.3.0.0** of the Azure RMS module for Windows PowerShell.  For installation instructions, see [Installing Windows PowerShell for Azure Rights Management](https://technet.microsoft.com/library/jj585012.aspx).

> [!TIP]
> If you have previously downloaded and installed the module, check the version number by running: `(Get-Module aadrm –ListAvailable).Version`

The following URLs are used for document tracking and must be allowed (for example, add them to your Trusted Sites if you're using Internet Explorer with Enhanced Security):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > This URL is for Bing maps.

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## AD RMS only: Support for multiple email domains within your organization
If you use AD RMS and users in your organization have multiple email domains, perhaps as a result of a merger or acquisition, you must make the following registry edit:

1.  Navigate to **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** and if not already present, create a new key named **RmsSharingApp**.

2.  Select **RmsSharingApp**, create a new Multi-String Value named **FederatedDomains**, and then add the domains and all the subdomains that your organization uses. Wildcards are not supported.

    For example: The company Coho Vineyard &amp; Winery has a standard email domain of **cohovineyardandwinery.com**, but as a result of mergers, they also use the email domains **cohowinery.com**, **eastcoast.cohowinery.com**, and **cohovineyard**. For the **FederatedDomains** value data, the administrator enters: **cohowinery.com; eastcoast.cohowinery.com; cohovineyard**

If you do not make this registry change, users might not be able to consume content that has been protected by other users in their organization. This registry edit is not needed if you use Azure RMS.


## Next steps
For additional technical information that includes explaining the difference between the levels of protections (native and generic), the supported file types and file name extensions, and how to change the default protection level, see [Technical overview for the Rights Management sharing application](rights-management-sharing-application-administrator-guide-technical-overview.md).
