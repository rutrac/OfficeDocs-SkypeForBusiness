---
title: "Change the phone numbers on your Audio Conferencing bridge"
ms.author: tonysmit
author: tonysmit
manager: serdars
ms.reviewer: oscarr
ms.topic: article
ms.assetid: 6403f6d1-c05a-44ab-a6e0-558000e246f4
ms.tgt.pltfrm: cloud
ms.service: skype-for-business-online
ms.collection: 
- Adm_Skype4B_Online
- Strat_SB_PSTN
ms.audience: Admin
appliesto:
- Skype for Business 
- Microsoft Teams
localization_priority: Priority
f1keywords: None
ms.custom:
- Audio Conferencing
description: "When you buy Audio Conferencing licenses, Microsoft is hosting your audio conferencing bridge for your organization. The audio conferencing bridge gives out dial-in phone numbers from different locations so meeting organizers and participants can use them to join Skype for Business or Microsoft Teams meetings using a phone."
---

# Change the phone numbers on your Audio Conferencing bridge

When you buy **Audio Conferencing** licenses, Microsoft is hosting your *audio conferencing bridge*  for your organization. The audio conferencing bridge gives out dial-in phone numbers from different locations so meeting organizers and participants can use them to join Skype for Business or Microsoft Teams meetings using a phone.
  
In addition to the phone numbers already assigned to your conferencing bridge, you can [get additional service numbers](../what-is-phone-system-in-office-365/getting-service-phone-numbers.md) (toll and toll-free numbers used for audio conferencing) from other locations and then assign them to the conferencing bridge so you can expand coverage for your users.
  
> [!NOTE]
> To be able to assign/unassign a phone number for a conferencing bridge, the phone number must be a '*service*' number. You can see the type of number it is by navigating to **Voice** > **Phone numbers** and looking in the **Number Type** column. Office 365 Communications Credits must be set up first in order for users to dial into the bridge on a toll free number. 
  
## Steps when you are assigning a new service phone number to your conference bridge

### Step 1 - Assign the new phone number to your audio conferencing bridge

1. Sign in to Office 365 with your work account.
    
2. Go to the **Office 365 admin center** > **Admin centers** > **Skype for Business** > **Voice** > **Phone numbers**.
    
3. Select the phone number from the list, and in the Action pane, click **Assign**.
    
4. On the **Assign** page, click **Save**.
    
    Only a service toll number can be set as the default number for your conferencing bridge; **service toll-free numbers can't be set as the default number of your conferencing bridge**. If you are assigning a service toll number and you would like to set it as the new default number for your audio conferencing bridge, select **Use this number as the default**.
    
    > [!NOTE]
    > After a new phone number has been assigned, even if the number became the new default number, the default number for existing users won't change. To set the default toll or a toll-free number that is added to an organizer's meeting invites, see [Set the phone numbers included on invites](set-the-phone-numbers-included-on-invites.md). 
  
> [!Note]
> [!INCLUDE [updating-admin-interfaces](../includes/updating-admin-interfaces.md)]

### Step 2 - Change the default phone numbers that are included in the meeting invites of users (optional)

The default phone numbers for user are the ones that are included on their meeting invites when they schedule a meeting. For more information, see [Set the phone numbers included on invites](set-the-phone-numbers-included-on-invites.md).
  
1. Sign in to Office 365 with your work or school account.
    
2. Go to the **Office 365 admin center** > **Admin centers** > **Skype for Business** > **Audio conferencing** > **Users** and select the users in the list.
    
3. Click **Edit** in the action pane.
    
4. Under **Default toll number** or **Default toll-free number**, select the number in the list and click **Save**.
    
After the changes have been saved, the new default phone numbers will be included on the meeting invites of organizers the next time they schedule a new meeting.
  
### Step 3 - Update existing meeting invites of users using the Meeting Migration Service (optional)

For the next two steps, you will need to start Windows PowerShell.
  
Using the Meeting Migration Service, you can optionally update meeting invites that were already sent to users in your organization before their default phone numbers were changed. For additional information, see [Setting up the Meeting Migration Service (MMS)](setting-up-the-meeting-migration-service-mms.md).
  
- Run the Meeting Migration Service (MMS) for the users who had their default phone numbers changed in Step 2. To do this, run the following command:
    
```
	Start-CsExMeetingMigration user@contoso.com

```

- You can also view the meeting migration status. All meetings would be rescheduled once there are no operations in  *Pending*  or *In-Progress*  state.
    
```
	Get-CsMeetingMigrationStatus -SummaryOnly
```

## Steps when you are unassigning a service phone number for a conferencing bridge


When you unassign a phone number from a conferencing bridge, users won't be able to join any meetings using that phone number anymore. Because the phone number is changing, it's important to update all users that could have a phone number as their default number (if any) and to update their existing meeting invites before the phone number is unassigned from the audio conferencing bridge. 
  
If the phone number is removed without updating the users and their meetings, their existing meeting invites could contain a phone number that won't work for joining their meetings anymore.
  
For the first three steps, you will need to start Windows PowerShell. To see how to do this, click [Want to know how to manage with Windows PowerShell?](change-the-phone-numbers-on-your-audio-conferencing-bridge.md#bkPowerShell)
  
### Step 1 - Update users that have the phone number to be unassigned as one of their default numbers

Replace the default toll or toll-free number for all users that have the number to be unassigned as a default number and start the process of rescheduling their meetings. To do this, run the following command:
  
```
Set-CsOnlineDialInConferencingUserDefaultNumber -FromNumber <Number to be removed> -ToNumber <Number to be set as new default> -NumberType <"Toll" or "Toll-Free"> -RescheduleMeetings
```
 > [!IMPORTANT] 
 >You can also change the default toll or toll-free number of users in the Skype for Business admin center. However, this won't automatically reschedule their meetings. 
 
 For additional information, see [Set the phone numbers included on invites](set-the-phone-numbers-included-on-invites.md).

  > [!NOTE]
  > Depending on the size of your organization, this could take some time to complete. 
  
### Step 2 - View meeting migration status using Windows PowerShell

All meetings will be rescheduled once there are no operations in *Pending* or *In-Progress* state.
  
```
Get-CsMeetingMigrationStatus -SummaryOnly
```

For more information about the Meeting Migration Service, see [Setting up the Meeting Migration Service (MMS)](setting-up-the-meeting-migration-service-mms.md).
  
### Step 3 - Unassign the old phone number from the audio conferencing bridge

1. Sign in to Office 365 with your work or school account.
    
2. Go to the **Office 365 admin center** > **Admin centers** > **Skype for Business** > **Voice** > **Phone numbers**.
    
3. Select the phone number from the list, and in the Action pane, click **Unassign**.
    
4. In the confirmation window, click **Yes**.
    
  > [!IMPORTANT]
  > After a phone number is unassigned from an audio conferencing bridge, the phone number will no longer be available for users to join new or existing meetings. 
  
## Want to know how to manage with Windows PowerShell?
<a name="bkPowerShell"> </a>

### To verify that Windows PowerShell is ready to go

 **Check that you are running Windows PowerShell version 3.0 or higher**
  
1. To verify that you are running version 3.0 or higher: **Start Menu** > **Windows PowerShell**.
    
2. Check the version by typing  _Get-Host_ in the **Windows PowerShell** window.
    
3. If you don't have version 3.0 or higher, you need to download and install updates to Windows PowerShell. See [Windows Management Framework 4.0 ](https://go.microsoft.com/fwlink/?LinkId=716845) to download and update Windows PowerShell to version 4.0. Restart your computer when you are prompted.
    
4. You will also need to install the Windows PowerShell module for Skype for Business Online that enables you to create a remote Windows PowerShell session that connects to Skype for Business Online. This module, which is supported only on 64-bit computers, can be downloaded from the Microsoft Download Center at [Windows PowerShell Module for Skype for Business Online](https://go.microsoft.com/fwlink/?LinkId=294688). Restart your computer if you are prompted.
    
If you need to know more, see [Connect to all Office 365 services in a single Windows PowerShell window](https://technet.microsoft.com/EN-US/library/dn568015.aspx).
  
### To start Windows PowerShell

 **Start a Windows PowerShell session**
  
1. From the **Start Menu** > **Windows PowerShell**.
    
2. In the **Windows PowerShell** window, connect to your Office 365 organization by running:
    
    > [!NOTE]
    > You only have to run the **Import-Module** command the first time you use the Skype for Business Online Windows PowerShell module.
  
> 
  ```
    Import-Module "C:\\Program Files\\Common Files\\Skype for Business Online\\Modules\\SkypeOnlineConnector\\SkypeOnlineConnector.psd1"
    $credential = Get-Credential
    $session = New-CsOnlineSession -Credential $credential
    Import-PSSession $session
  ```

If you want more information about starting Windows PowerShell, see [Connect to all Office 365 services in a single Windows PowerShell window](https://technet.microsoft.com/EN-US/library/dn568015.aspx) or [Connecting to Skype for Business Online by using Windows PowerShell](https://technet.microsoft.com/en-us/library/dn362795%28v=ocs.15%29.aspx).
  
### Save time or automate

To save time or automate this process, you can use the [Set-CsOnlineDialInConferencingUser](http://go.microsoft.com/fwlink/?LinkId=617688) or the **Set-CsOnlineDialInConferencingUserDefaultNumber** cmdlets.
  
- Use the [Set-CsOnlineDialInConferencingUser](http://go.microsoft.com/fwlink/?LinkId=617688) cmdlet to change the default toll or toll-free number for specific users.
    
  - To change the default toll-free number for a user, run:
    
  ```
  Set-CsOnlineDialinConferencingUser -Identity amos.marble@Contoso.com -TollFreeServiceNumber   80045551234
  ```

- Use the **Set-CsOnlineDialInConferencingUserDefaultNumber** cmdlet to change the default toll or toll-free number of users based on their original default number or their location.
    
    > [!NOTE]
    > To find the BridgeID, use the **Get-CsOnlineDialInConferencingBridge**.
  
  - To set the default toll-free number for all users without one to 8005551234, run:
    
  ```
  Set-CsOnlineDialInConferencingUserDefaultNumber -FromNumber $null -ToNumber 8005551234 -NumberType TollFree -BridgeId <Bridge Id>  
  ```

  - To change the default toll-free number of all users that have 8005551234 as their default toll-free number to 8005551239 and automatically reschedule their meetings, run:
    
  ```
  Set-CsOnlineDialInConferencingUserDefaultNumber -FromNumber 8005551234 -ToNumber 8005551239 NumberType TollFree -BridgeId <Bridge Id> -RescheduleMeetings
  ```

  - To set the default toll-free number of all users located in the U.S. to 8005551234 and automatically reschedule their meetings, run:
    
  ```
  Set-CsOnlineDialInConferencingUserDefaultNumber -Country US -ToNumber 8005551234 -NumberType TollFree -BridgeId <Bridge Id> -RescheduleMeetings
  ```

    > [!NOTE]
    > The location that is used above needs to match the contact information of user(s) that is set in the Office 365 admin center. 
  
## About Windows PowerShell

When it comes to Windows PowerShell is all about managing users and what users are allowed or not allowed to do. With Windows PowerShell, you can manage Office 365 and Skype for Business Online using a single point of administration that can simplify your daily work, when you have multiple tasks to do. To get started with Windows PowerShell, see these topics:
    
  - [An introduction to Windows PowerShell and Skype for Business Online](https://go.microsoft.com/fwlink/?LinkId=525039)
    
  - [Why you need to use Office 365 PowerShell](https://go.microsoft.com/fwlink/?LinkId=525041)
    
Windows PowerShell has many advantages in speed, simplicity, and productivity over only using the Office 365 admin center such as when you are making setting changes for many users at one time. Learn about these advantages in the following topics:
    
  - [Best ways to manage Office 365 with Windows PowerShell](https://go.microsoft.com/fwlink/?LinkId=525142)
    
  - [Using Windows PowerShell to manage Skype for Business Online](https://go.microsoft.com/fwlink/?LinkId=525453)
    
  - [Using Windows PowerShell to do common Skype for Business Online management tasks](https://go.microsoft.com/fwlink/?LinkId=525038)

## Related topics
[Change the settings for an Audio Conferencing bridge](change-the-settings-for-an-audio-conferencing-bridge.md)
