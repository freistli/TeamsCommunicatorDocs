# Introduction

Teams Communicator can help business admins to send adaptive card Teams messages to users, group, team, or Everyone securely through minimum deployment efforts and convenient operations. 

Here is the user guide


- [Setup](https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#Setup)
  - [Azure Side](https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#azure-side)
  - [Client Side](https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#client-side) 
- [Warm Up](https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#Warm-Up)
- [Send Message](https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#Send-Message)
- [Resume Tasks](https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#Resume-Tasks)
- [Backup Client Data](https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#Backup-Client-Data)
- [Restore Client Data](https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#Restore-Client-Data)

## Setup
[1]: https://github.com/freistli/privacy/edit/master/TCSetupGuide.md#Setup

### Azure Side
[1]: https://github.com/freistli/privacy/edit/master/TCSetupGuide.md

1. Register App in Azure AD https://aad.portal.azure.com (Refer to [Register your app with the Azure AD v2.0 endpoint](https://learn.microsoft.com/en-us/graph/auth-register-app-v2?view=graph-rest-1.0)), with below scopes for Delegated Permissions of Microsoft Graph:
  
                "User.Read.All
                "Group.Read.All"
                "Chat.Create"
                "ChannelSettings.Read.All"
                "ChannelMessage.Send"
                

2. Add Mobile and desktop applications call back, set "https://login.microsoftonline.com/common/oauth2/nativeclient" as call back Url

   ![image](https://user-images.githubusercontent.com/8623897/196481082-ac1d9ce5-398e-47d8-a531-9b1a9c290d68.png)

   Copy Tenant ID and Client ID of the App from https://aad.portal.azure.com.
   
   

3. The login users need to be in the AAD group (create a security group **TeamsCommunicatorGP** if don't have) and be able to get Admin Consent to use the above scopes 

   

  ![image](https://user-images.githubusercontent.com/8623897/196481916-bada985b-8725-45e3-b334-e74a8dd2b19b.png)
  
  
### Client Side
[1]: https://github.com/freistli/privacy/edit/master/TCSetupGuide.md

 1. Config Tenant ID, Client ID, and Redirect Uri as below. If the register the app as Multi-Tenant, use **common** in the Tenant ID field, otherwise, use the real Tenant ID


   ![image](https://user-images.githubusercontent.com/8623897/196483155-ef6ed635-373c-4a6e-90c2-50d5bcc77669.png)
   

## Warm Up
[1]: https://github.com/freistli/privacy/edit/master/TCSetupGuide.md

It is optional.

When send message to large amount users (several thousands to hundreds of thousands) at the first time, recommend to warm up before sending. This only need to do once for the same logon user with the same recipients. 

1. Open Teams Communicator, click Logon
2. Choose Task type (single, team, group, everyone)
3. Click Warm Up.

The Warm up task can be stopped by click Stop or close the app. Logon user can continuously warm up it later at any time. Time is mainly spent initializing chats between logon user (sender) and recipents. Several thousands may take several hours for warm up completion.


## Send Message
[1]: https://github.com/freistli/privacy/edit/master/TCSetupGuide.md

1. Open Teams Communicator, click Logon
2. Click Compose Message to edit message
   1. To generate the message content, click the AdaptiveCard Designer to design it. Make sure the card target version is **1.2**
   2. Copy Card Payload, and paste it into the Compose Message editor.
3. Click Send Message, choose Task type (single, team, group, everyone)
4. Click Send, and follow the wizard.

The Send task can be stopped by click Stop or close the app.  Logon user can resume the same task later. After completing warm up, general tests result is sending to 6500 users takes less than 7 minutes.

## Resume Tasks
[1]: https://github.com/freistli/privacy/edit/master/TCSetupGuide.md

1. Open Teams Communicator, click Logon
2. Click Tasks View to view existing tasks
3. Select one Task, click Resume Selected Task
4. In Send Message, click Send

   
 ## Backup Client Data
 [1]: https://github.com/freistli/privacy/edit/master/TCSetupGuide.md
 
 1. Open Teams Communicator, click Settings. Copy the Data File Path
 2. Close App, copy all data in the data file path to backup place
 
 ## Restore Client Data
 [1]: https://github.com/freistli/privacy/edit/master/TCSetupGuide.md
 
 1. Open Teams Communicator, click Settings. Copy the Data File Path
 2. Close App, copy data from backup place to data file path, overwrite existed ones.
 3. Open App.

