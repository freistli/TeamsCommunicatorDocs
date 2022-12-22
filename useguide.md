# Introduction

**ON-PREM Communicator** can help business admins to send adaptive card **Microsoft Teams** messages to users, group, team, or Everyone securely through minimum deployment efforts and convenient operations. 

With it, can send notification messages on behavior of admins and as Bot App.

Install [ON-PREM Communicator](https://www.microsoft.com/store/apps/9NVN32B4V6G3) from Windows Store directly.

Here is the user guide


- [Setup](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#Setup)
  - [Azure AD Side](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#azure-side)
    - [MS Graph Settings (required)](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#ms-graph-settings)
    - [Bot Settings (optional)](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#bot-settings)
  - [Windows Client Side](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#client-side) 
- [Warm Up](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#Warm-Up)
- [Send Message](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#Send-Message)
- [Resume Tasks](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#Resume-Tasks)
- [Export receivers list](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#Export-receivers-list)
- [Backup Client Data](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#Backup-Client-Data)
- [Restore Client Data](https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md#Restore-Client-Data)

![image](https://user-images.githubusercontent.com/8623897/196637359-f4ed2270-3487-478b-8e8f-8b860f404db0.png)

### Send Messages As User
![image](https://user-images.githubusercontent.com/8623897/196637988-aaccb612-9a87-48d3-b834-032d5f679aea.png)

### Send Messages As Bot (Receiver View)
![image](https://user-images.githubusercontent.com/8623897/209061862-a3061b0a-b750-4532-b623-a147d460987f.png)


## Setup
[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md

### Azure Side
[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md

#### MS Graph Settings
[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md

> [!NOTE]
>
> Graph Settings are required for this app.

1. Register App (for example: TCApp) in Azure AD https://aad.portal.azure.com (Refer to [Register your app with the Azure AD v2.0 endpoint](https://learn.microsoft.com/en-us/graph/auth-register-app-v2?view=graph-rest-1.0)). 

2. Add Mobile and desktop applications call back, set "https://login.microsoftonline.com/common/oauth2/nativeclient" as call back Url
  

![image](https://user-images.githubusercontent.com/8623897/196860298-bd24ff54-05a3-4ea4-8df8-b5de3bc07817.png)


3. Add below scopes for **Delegated Permissions** of **Microsoft Graph** in the **API permissions** left menu:

                "User.Read"
                "User.Read.All
                "Group.Read.All"
                "Chat.Create"
                "Chat.ReadWrite"
                "ChannelSettings.Read.All"
                "ChannelMessage.Send"
 
> [!NOTE]
>
> If you send notificaitons as Bot instead of User, "Chat.Create", "Chat.ReadWrite" and "ChannelMessage.Send" are not required.
                
![image](https://user-images.githubusercontent.com/8623897/196862663-c2c27e19-55d2-4f13-92e3-2d05396e4fa0.png)


   Copy Tenant ID and Client ID of the App from https://aad.portal.azure.com.
   
   

3. The ON-PREM communicator users need to be in the AAD group (create a security group **TeamsCommunicatorGP** if don't have) and be able to get Admin Consent to use the above scopes (either the user has Global Admin role, Application Admin role, Cloud Application Admin role in AAD, or Admins consents the scopes for the organization) 
   

  ![image](https://user-images.githubusercontent.com/8623897/196481916-bada985b-8725-45e3-b334-e74a8dd2b19b.png)
  

#### Bot Settings
[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md

> [!NOTE]
>
> If you don't want to send notifications as Bot App, this section can be skipped. This section reuquires experienced skillsets of configurating Azure Bot Service and deploying Teams Bot App.

1. Register App (for example: TCBotApp) in Azure AD https://aad.portal.azure.com (Refer to [Register your app with the Azure AD v2.0 endpoint](https://learn.microsoft.com/en-us/graph/auth-register-app-v2?view=graph-rest-1.0)). Copy the client ID.

2. Add Mobile and desktop applications call back, set "https://login.microsoftonline.com/common/oauth2/nativeclient" as call back Url

Steps 1&2 are the same as above MS Graph Settings section.

3. Add below scopes for **Application Permissions** of **Microsoft Graph** in the **API permissions** left menu:

                "AppCatalog.Read.All"
                "Group.Read.All"
                "User.Read.All
                "TeamsAppInstallation.ReadWriteForTeam.All"
                "TeamsAppInstallation.ReadWriteForUser.All"

4. Add a new client secret in the **Certificates & secrets" left menu. Copy the client secret.

5. Open Azure Portal, add a new Azure Bot Service.

![image](https://user-images.githubusercontent.com/8623897/209060598-8edc0f63-6b37-4cc5-8df9-fb04bb9f202d.png)

6. Use the copied App ID to fill the Bot Service client ID. Create the new Bot service.

![image](https://user-images.githubusercontent.com/8623897/209060631-fcb09b48-4aed-4b7b-91d6-976907d4d92f.png)


7. Open **Teams**, Open the **Developer Portal** app, create a new App, add Bot feature with the copied client ID, choose **Only send notifications**, **Peronsal**, and **Team** optins.

![image](https://user-images.githubusercontent.com/8623897/209060644-d211d09d-8598-45e6-9fca-4713d053a679.png)


8. Click **Basic Information**, copy its Teams App ID.

![image](https://user-images.githubusercontent.com/8623897/209060830-636abce7-8f1a-4325-96c6-596da9f8ad2c.png)


9. Publish the Bot App, get its package. 

10. Upload the app to your organization.


### Client Side


[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md

 1. On Windows 10/11, install it from Windows Store [ON-PREM Communicator](https://www.microsoft.com/store/apps/9NVN32B4V6G3)

 2. Config Tenant ID, Client ID, and Redirect Uri in **MS Graph Setting**. If the register the app as Multi-Tenant, use **common** in the Tenant ID field, otherwise, use the real Tenant ID

![image](https://user-images.githubusercontent.com/8623897/209060865-54a396c5-6ba4-4f37-a167-01a56a03f8b9.png)


 3. This step is for **Send Messages as Bot**. If don't need, can skip it.

    Click Settings, click **Bot Settings**. Config Tenant ID (requires the accurate GUID, cannot use **common**), Bot Teams App ID, Bot Client ID, Bot Secret, and Bot Connector Region (in, apac, emea, amer).
   
 ![image](https://user-images.githubusercontent.com/8623897/209085844-b970b290-a6a7-42e5-b2c9-505ff1ae4380.png)

   
 4. Click Logon, to give Admin Consent (If you only want Admin roles to use this app, don't select Consent on behalf of your organaization):
 
    ![image](https://user-images.githubusercontent.com/8623897/196863017-2d94db31-7daa-4c14-9d0a-e1517082dfc7.png)

    If the user is not Admin (a member of Global Administrator, Cloud Application Administrator, or Application Administrator), and the  admin didn't grant Admin  Consent for organization, the user will see this warning and not able to continue:
    
    [<img src="https://user-images.githubusercontent.com/8623897/196958321-58382c41-22ea-48a3-9980-e2dedce02758.png" width="400"/>]
    

## Warm Up
[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md

It is optional and general recommended if the amount of recipients is larger than 2000

This only need to warm up once for the same logon user with the same recipients. 

1. Open ON-PREM Communicator, click Logon
2. Choose Task type (group, everyone)
3. Click Warm Up.

The Warm up task can be stopped by click Stop or close the app. Logon user can continuously warm up it later at any time. 

When send messages as User, warm up time is mainly spent getting chats' ids from MS Graph between logon user (sender) and recipents. Several thousands may take several hours for warm up completion.

When send messages as Bot,  warm up time is mainly spent auto installing the bot app for the recipents. Several thousands may take one hour. It is faster.


## Send Message
[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md

1. Open ON-PREM Communicator, click Logon
2. Click Compose Message to edit message
   1. To generate the message content, click the AdaptiveCard Designer to design it. Make sure the card target version is **1.2**
   2. Copy Card Payload, and paste it into the Compose Message editor.
3. Click Send Message, choose Task type (single, team, group, everyone). 

   **Please input accurate alias when sending to team & group. Otherwise the app picks up the first matched one for you to double confirm**
  
4. Click Send, and follow the wizard.

The Send task can be stopped by click Stop or close the app.  Logon user can resume the same task later. After completing warm up, general tests result is sending to 6500 users takes less than 7 minutes.

## Resume Tasks
[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md

1. Open ON-PREM Communicator, click Logon
2. Click Tasks View to view existing tasks, click Load Tasks
3. Select one Task, click Resume Selected Task
4. In Send Message, click Send

## Export receivers list
[1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md
1. Open ON-PREM Communicator, click Logon
2. Click Tasks View to view existing tasks, click Load Tasks
3. Select one Task, click Export Receivers

   
 ## Backup Client Data
 [1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md
 
 1. Open ON-PREM Communicator, click Settings. Copy the Data File Path
 2. Close App, copy all data in the data file path to backup place
 
 ## Restore Client Data
 [1]: https://github.com/freistli/TeamsCommunicatorDocs/blob/main/useguide.md
 
 1. Open ON-PREM Communicator, click Settings. Copy the Data File Path
 2. Close App, copy data from backup place to data file path, overwrite existed ones.
 3. Open App.

