---
title: "Create a call queue"
ms.author: dstrome
author: dstrome
manager: serdars
ms.reviewer: phans, wasseemh
ms.topic: article
ms.assetid: 67ccda94-1210-43fb-a25b-7b9785f8a061
ms.tgt.pltfrm: cloud
ms.service: msteams
search.appverid: MET150
ms.collection: 
  - M365-voice
audience: Admin
appliesto: 
  - Skype for Business
  - Microsoft Teams
localization_priority: Normal
f1.keywords: 
  - CSH
ms.custom: 
  - ms.teamsadmincenter.callqueues.overview"
  - Phone System
  - seo-marvel-apr2020
description: Learn how to set up Phone System for Cloud call queues with Microsoft Teams, which provide a greeting message, hold music, call redirecting, and other features.
---

# Create a Cloud call queue

Cloud call queues can provide:

- A greeting message.
- Music while people are waiting on hold.
- Redirecting calls to call agents in mail-enabled distribution lists and security groups.
- Setting different parameters such as queue maximum size, timeout, and call handling options.
- Shared voicemail for callers to leave a message for an organization.

You don't directly associate a phone number to a call queue, instead the phone number is associated to a [resource account](manage-resource-accounts.md). A call queue can be dialed directly or accessed by a selection on an auto attendant.

The caller hears music while they are on hold, and the call connects to the call agents in *First In, First Out* (FIFO) order.

All calls in the queue are sent to agents by one of the following methods:

- With attendant routing, the first call in the queue rings all agents at the same time.
- With serial routing, the first call in the queue rings all call agents one by one.
- With longest idle routing, the call agent whose has been idle the longest time receives the next available call. The idle time is defined as the length of time a call agent's presence state is set to **Available** or **Away** (if less than 10 minutes), at the time of the call. If a call agent's presence is **Away** for more than 10 minutes, the idle timer resets.
- With round robin, routing of incoming calls is balanced so that each call agent gets the same number of calls from the queue.

You can set call handling options, such as agent opt-in/opt-out, presence-based routing, call wait time, and call time-out options with any of the above methods.

Only one incoming call notification (for the call at the head of the queue) at a time goes to the call agents. After a call agent accepts the call, the next incoming call in the queue will start ringing call agents.

> [!NOTE]
> This article applies to both Microsoft Teams and Skype for Business Online.

## Step 1 — Get started

To get started using call queues, it's important to remember a few things:

- A call queue is required to have an associated resource account. See [Manage resource accounts in Teams](manage-resource-accounts.md) for details on resource accounts.
- When you assign a phone number to a resource account, you can now use the cost-free Phone System [Virtual User license](teams-add-on-licensing/virtual-user.md). Phone System allows phone numbers at the organizational level for use with low-cost auto attendant and call queue services.

  > [!NOTE]
  > Direct Routing service numbers for call queues are supported for Microsoft Teams users and agents only.

> [!NOTE]
> To redirect calls to people in your organization who are online, they must have a **Phone System** license and be enabled for Enterprise Voice or have Microsoft 365 or Office 365 Calling Plans. See [Assign Microsoft Teams add-on licenses](teams-add-on-licensing/assign-teams-add-on-licenses.md). To enable them for Enterprise Voice, you can use Windows PowerShell. For example, run: `Set-CsUser -identity "Amos Marble" -EnterpriseVoiceEnabled $true.

- To learn more about Calling Plans, see [Phone System and Calling Plans](calling-plan-landing-page.md) and [Calling Plans for Microsoft 365 or Office 365](calling-plans-for-office-365.md).

- You can only assign Cloud call queues toll and toll-free service phone numbers that you got in the **Microsoft Teams admin center** or transferred from another service provider. Communications Credits are required for toll-free service numbers.

    > [!NOTE]
    > User (subscriber) phone numbers can't be assigned to call queues - only service toll or toll-free phone numbers can be used.

- The following clients are supported for call agents associated to a Cloud call queue:

  - Skype for Business desktop client 2016 (32-bit and 64-bit versions)
  - Lync desktop client 2013 (32-bit and 64-bit versions)
  - All IP phone models supported for Microsoft Teams. See [Getting phones for Skype for Business Online](/skypeforbusiness/what-is-phone-system-in-office-365/getting-phones-for-skype-for-business-online/getting-phones-for-skype-for-business-online).
  - Mac Skype for Business Client (version 16.8.196 and later)
  - Android Skype for Business Client (version 6.16.0.9 and later)
  - iPhone Skype for Business Client (version 6.16.0 and later)
  - iPad Skype for Business Client (version 6.16.0 and later)
  - Microsoft Teams Windows client (32-bit and 64-bit versions)
  - Microsoft Teams Mac client
  - Microsoft Teams iPhone app
  - Microsoft Teams Android app

    > [!NOTE]
    > Call queues that are assigned a direct routing number don't support Skype for Business clients, Lync clients, or Skype for Business IP Phones as agents.

## Step 2 — Get or transfer toll or toll-free service phone numbers

Before you can create and set up your call queues, you need to get or transfer your existing toll or toll-free service numbers. To get your service numbers, see [Getting service phone numbers](getting-service-phone-numbers.md) or if you want to transfer an existing service number, see [Transfer phone numbers to Teams](phone-number-calling-plans/transfer-phone-numbers-to-teams.md). After you get the toll or toll-free service phone numbers, they will show up in **Microsoft Teams admin center** > **Voice** > **Phone numbers**. Toll free numbers will be listed with a **Number type** of **Service — Toll-Free**.

> [!NOTE]
> If you are outside the United States, you can't use the Microsoft Teams admin center to get service numbers. Go to [Manage phone numbers for your organization](manage-phone-numbers-for-your-organization/manage-phone-numbers-for-your-organization.md) instead to see how to do it from the outside of the United States.

When you set up multiple auto attendants, you would usually assign a phone number to the main auto attendant's resource account. Resource accounts associated to nested auto attendants or call queues often don't need phone numbers. That auto attendant can direct callers to your call queues or nested auto attendants even if they don't have a phone number. In those situations, you can create all auto attendants and call queues in your system without assigning dialpad options, and then edit the settings later. A call queue or auto attendant must exist to set it as a menu option.

## Step 3 — Create a call queue

[!INCLUDE [updating-admin-interfaces](includes/updating-admin-interfaces.md)]

> [!IMPORTANT]
> Every call queue is required to have an associated [resource account](manage-resource-accounts.md). You must create the resource account first, then you can associate it to the call queue.

### Use the Microsoft Teams admin center

In the **Microsoft Teams admin center**, **Voice** > **Call queues**, then click **+ Add new**:

### Set the display name and resource account

![Screenshot of a new call queue, with numbered callouts](media/37ecc300-a108-4294-8463-fce570dfce72.png)

* * *

![Icon of the number 1, references a callout in the previous screenshot](media/teamscallout1.png)
**Name** Enter a descriptive display name for the call queue. This name is required and can contain up to 64 characters, including spaces.

 This name is displayed in the notification for the incoming call.

* * *

![Icon of the number 2, references a callout in the previous screenshot](media/teamscallout2.png)
**Add Accounts** Select a resource account. All call queues are required to have a resource account. Resource accounts aren't required to have a service toll or toll-free phone number.

If there aren't any listed,  get service numbers and assign them to a Resource account before you create the call queue, as described earlier. To get your service numbers, see [Getting service phone numbers](getting-service-phone-numbers.md). See [Manage resource accounts in Teams](manage-resource-accounts.md) for specifics on how to assign a phone number.

> [!NOTE]
> If you want or need to assign a **Domain** you would  assign it to the resource account for the call queue.

### Set the greeting and music played while on hold

![screenshot of greeting and music options, with numbered callouts](media/1d395a93-7cab-4178-9295-12d5379e20de.png)

* * *

![Icon of the number 1, references a callout in the previous screenshot](media/teamscallout1.png)
**Greeting** the optional greeting played for people who call the call queue number.

You can upload an audio file (.wav, .mp3, or .wma formats).

![Icon of the number 2, references a callout in the previous screenshot](media/teamscallout2.png)
**Music on hold** You can use the default Music on Hold provided with the call queue. You can also upload an audio file in .wav, mp3, or .wma formats to use as your custom Music on hold.

* * *

### Select the call answering options

![Screenshot of call answering options](media/teams-cq-call-answering-options.png)

![Icon of the number 1, references a callout in the previous screenshot](media/teamscallout1.png)
**Call agents and groups** To add individual agents directly, without adding them to a group, click **Add users**. Put individual agents in the order in which you want them to receive the call. You can add up to 20 individual agents (to add more than 20, put them in a group).

Calls are routed first to individual agents, then to the agents in groups. 

You can select up to 200 call agents who belong to any of the following mailing lists or groups:

- Microsoft 365 group
- Security group
- Distribution list

Call agents selected must be one of the following: 

- Online users with a Phone System license and Enterprise Voice enabled
- Online users with a Calling Plan
- On-premises Skype for Business Server users

  > [!NOTE]
  > This also applies if you want to redirect calls to people in your organization who are online. These individuals must have a Phone System license and Enterprise Voice enabled *or* have a Calling Plan. For more information, see [Assign Skype for Business licenses](https://docs.microsoft.com/skypeforbusiness/skype-for-business-and-microsoft-teams-add-on-licensing/assign-skype-for-business-and-microsoft-teams-licenses), [Assign Microsoft Teams licenses](https://docs.microsoft.com/microsoftteams/teams-add-on-licensing/assign-teams-add-on-licenses), or [Which Calling Plan is right for you?](https://docs.microsoft.com/microsoftteams/calling-plan-landing-page)

   To enable an agent for Enterprise Voice, you can use Windows PowerShell. For example, run: `Set-CsUser -identity "Amos Marble" -EnterpriseVoiceEnabled $true`

- Users with a Phone System license or a Calling Plan that are added to a Microsoft 365 Group, a mail-enabled distribution list, or a security group. When you add an agent in a distribution list or a security group as a call queue agent, it can take up to three hours for the first call to arrive. A newly created distribution list or security group might take up to 48 hours to become available to be used with call queues. Newly created Microsoft 365 Groups are available almost immediately.

- If your agents are using the Microsoft Teams app for call queue calls, they need to be in TeamsOnly mode.

![Icon of the number 2, references a callout in the previous screenshot](media/teamscallout2.png)
**Conference mode** Conference mode significantly reduces the amount of time it takes for a caller to be connected to an agent, after the agent accepts the call. If you have more than one call queue, you can enable conference mode on some or all of your call queues; enabling or disabling conference mode on one call queue doesn't impact any other call queues.

Conference mode is disabled by default but can be enabled at any time if the following requirements are met:

- Agents added to the call queue need to use one of the following clients:
  - The latest version of the Microsoft Teams desktop client, Android app, or iOS app
  - Microsoft Teams phone version 1449/1.0.94.2020051601 or later
- Agents' Teams accounts need to be set to Teams-only mode

> [!IMPORTANT]
> If the agent requirements above aren't met and conference mode is enabled on a call queue, agents who don't meet the requirements aren't included in the call routing list. Agents who aren't in the call routing list won't receive calls. If you have agents who don't meet the agent requirements above, don't enable conference mode on the call queue.

After conference mode is enabled on a call queue, calls will benefit from the faster connection time if they're received via one of the following methods:

- VoIP calls from another Microsoft Teams desktop client
- Calling Plan PSTN calls
- Direct Routing PSTN calls

The majority of calls are received via one of the methods listed above. If a call is received via another method (such as a VoIP call from a Skype for Business client), the call will still be added to the call queue, however, it won't benefit from the faster connection time.

![Icon of the number 3, references a callout in the previous screenshot](media/teamscallout3.png)
**Routing method** You can choose either **Attendant**, **Serial**, **Longest idle**, or **Round Robin** as the distribution method. All new and existing call queues have attendant routing selected by default. When attendant routing is used, the first call in the queue rings all call agents at the same time. The first call agent to pick up the call gets the call.

- **Attendant routing** causes the first call in the queue to ring all call agents at the same time. The first call agent to pick up the call gets the call.
- **Serial routing** incoming calls ring all call agents one by one, from the beginning of the call agent list. Agents can't be ordered within the call agent list. If an agent dismisses or does not pick up a call, the call will ring the next agent and will try all agents until it is picked up or times out.
- **Longest idle** routes the next available call to the call agent whose has been idle the longest time. The idle time is defined as the length of time a call agent's presence state is set to **Available** or **Away** (if less than 10 minutes), at the time of the call. If a call agent's presence is set to **Away** for more than 10 minutes, the idle timer resets. Presence states of users are queried every minute.

    It's important to know that enabling this setting forces **Presence-based routing** to also be enabled.

    > [!IMPORTANT]
    > Agents who use the Skype for Business client won't receive calls when the longest idle setting is enabled. If you have agents who use Skype or Business, don't enable this setting.
- **Round robin** balances routing of incoming calls so that each call agent gets the same number of calls from the queue. This may be desirable in an inbound sales environment to assure equal opportunity among all the call agents.

![Icon of the number 4, references a callout in the previous screenshot](media/teamscallout4.png)
**Presence-based routing** Presence-based routing uses the availability status of call agents to determine whether an agent should be included in the call routing list for the selected routing method. Call agents whose availability status is set to **Available** are included in the call routing list and can receive calls. Agents whose availability status is set to any other status are excluded from the call routing list and won't receive calls until their availability status changes back to **Available**.  

You can enable presence-based call routing with any of the routing methods.

If an agent opts out of getting calls, they won't be included in the call routing list regardless of what their availability status is set to. 

> [!IMPORTANT]
> Agents who use the Skype for Business client aren't included in the call routing list when presence-based routing is enabled, regardless of their availability status. Agents who aren't in the call routing list won't receive calls. If you have agents who use Skype for Business, don't enable presence-based call routing.

### Select an agent opt-out option

![Screenshot of agent opt-out options, with numbered callouts](media/99279eff-db61-4acf-9b62-64be84b6414b.png)

* * *

![Icon of the number 1, references a callout in the previous screenshot](media/teamscallout1.png)
**Agent can opt out of getting calls** You can choose to allow call queue agents to opt-out of taking calls from a particular queue by enabling this option.

Enabling this option allows all agents in this queue to start or stop receiving calls from this call queue at will. You can revoke the agent opt-out privilege at any time by clearing the check box, causing agents to become automatically opted in for this queue again (the default setting for all agents).

To access the opt-out option, agents can:

 1. Open **Options** in their desktop Skype for Business client.
 2. On the **Call Forwarding** tab, click the **Edit settings online** link.
 3. On the user settings page, click **Call Queues**, and then clear the check boxes to opt-out of queues.

    > [!NOTE]
    > Agents using apps or endpoints other than Skype for Business Desktop can access the opt-out option from the user settings portal [https://aka.ms/cqsettings](https://aka.ms/cqsettings).
    >
    > If the agents are in Microsoft Teams desktop clients, then they can opt-out by using the Call Settings. 

![Icon of the number 2, references a callout in the previous screenshot](media/teamscallout2.png)
**Agent Alert setting**

This defines the duration of an agent being notified of a call before the Serial or Round Robin routing methods move to the next agent.

The default setting is 30 seconds, but it can be set for up to 3 minutes.

* * *

### Set the call overflow and timeout handling options

![Screenshot of overflow handling options, with numbered callouts](media/3f018734-16fe-458b-827d-71fc25155cde.png)

* * *

![Icon of the number 1, references a callout in the previous screenshot](media/teamscallout1.png)
**Maximum calls in the queue** Use this to set the maximum calls that can wait in the queue at the same time. The default is 50, but it can range from 0 to 200. When this limit is reached, the call is handled in the way you set on the **When the maximum number of calls is reached** setting below.

* * *

![Icon of the number 2, references a callout in the previous screenshot](media/teamscallout2.png)
**When the maximum number of calls is reached** When the call queue reaches its maximum size (set using the **Maximum calls in the queue** setting), you can choose what happens to new incoming calls.

- **Disconnect** The call is disconnected.
- **Redirect to** When you choose this, select one of the following:

  - **Person in organization** An online user with a Phone System license and is enabled for Enterprise Voice or has a Calling Plan.

  - **Voice app** Select the name of a resource account associated to either a call queue or auto attendant that has already been created.

  - **External phone number** Choose this to transfer the caller to an external phone number that you specify. Note the following:

    - The resource account associated with the application making the PSTN transfer out must have a phone number and be assigned a Virtual Phone System license. Phone System licenses aren't supported. Additionally, the resource account must have one of the following:
        - For a resource account with a Calling Plan number, assign a [Calling Plan](calling-plans-for-office-365.md) license.
        - For a resource account with a Direct Routing number, assign an [online voice routing policy](manage-voice-routing-policies.md).
    - The outbound phone number that's displayed is determined as follows:
        - For Calling Plan numbers, the original caller's phone number is displayed.
        - For Direct Routing numbers, the number sent is based on the P-Asserted-Identity (PAI) setting on the SBC, as follows:
            - If set to Disabled, the original caller's phone number is displayed. This is the default and recommended setting.
            - If set to Enabled, the resource account phone number is displayed.
    - Transfers between Calling Plan trunks and Direct Routing trunks aren't supported.
  - **Voicemail** Select the Microsoft 365 group that contains the users in your organization that need to access voicemail received by this call queue, and then select one of the following:
      - **Play an audio file** If you choose this option, select **Upload file** to upload a recorded greeting message. The recording can be no larger than 5 MB. 
      - **Type in a greeting message** If you choose this option, enter text you want the system to read (up to 1000 characters). For example, you can type "Sorry that we can't take your call at this time. Please leave your name, phone number, and reason for your call after the beep."

      Turn on transcription if you want to enable voice-to-text transcription of voicemail messages.

      Voicemail messages are sent to the Microsoft 365 group you specify. To access voicemail messages, members of the group can open them by navigating to the group in Outlook.

* * *

![Icon of the number 3, references a callout in the previous screenshot](media/teamscallout3.png)
**Call Timeout: maximum wait time** You can also decide how much time a call can be on hold in the queue before it times out and needs to be redirected or disconnected. Where it is redirected is based on how you set the **When a call times out** setting. You can set a time from 0 to 45 minutes.

The timeout value can be set in seconds, at 15-second intervals. This allows you to manipulate the call flow with finer granularity. For example, you could specify that any calls that are not answered by an agent within 30 seconds go to a Directory Search auto attendant.

![Icon of the number 4, references a callout in the previous screenshot](media/teamscallout4.png)
**When call times out** When the call reaches the limit you set on the **How long a call can wait in the queue** setting, you can choose what happens to the call:

- **Disconnect** The call is disconnected.
- **Redirect this call to** When you choose this, you have these options:
  - **Person in organization** An online user with a Phone System license and enabled for Enterprise Voice or have Calling Plans.

  - **Voice app** Select the name of a resource account associated with either a call queue or auto attendant that you already created.

  - **External phone number** Choose this to transfer the caller to an external phone number that you specify. Note the following:

    - The resource account associated with the application making the PSTN transfer out must have a phone number and be assigned a Virtual Phone System license. Phone System licenses aren't supported. Additionally, the resource account must have one of the following:
        - For a resource account with a Calling Plan number, assign a [Calling Plan](calling-plans-for-office-365.md) license.
        - For a resource account with a Direct Routing number, assign an [online voice routing policy](manage-voice-routing-policies.md).
    - The outbound phone number that's displayed is determined as follows:
        - For Calling Plan numbers, the original caller's phone number is displayed.
        - For Direct Routing numbers, the number sent is based on the P-Asserted-Identity (PAI) setting on the SBC, as follows:
            - If set to Disabled, the original caller's phone number is displayed. This is the default and recommended setting.
            - If set to Enabled, the resource account phone number is displayed.
    - Transfers between Calling Plan trunks and Direct Routing trunks aren't supported.
    - **Voicemail** Select the Microsoft 365 group that contains the users in your organization that need to access voicemail received by this call queue, and then select one of the following:
      - **Play an audio file** If you choose this option, select **Upload file** to upload a recorded greeting message. The recording can be no larger than 5 MB.
      - **Type in a greeting message** If you choose this option, enter text you want the system to read (up to 1000 characters). For example, you can type "Sorry that we can't take your call at this time. Please leave your name, phone number, and reason for your call after the beep."

      Turn on transcription if you want to enable voice-to-text transcription of voicemail messages.

      Voicemail messages are sent to the Microsoft 365 group you specify. To access voicemail messages, members of the group can open them by navigating to the group in Outlook.

## Change Caller ID for outbound calls

To protect a call agent's identity, change their caller ID for outbound calls to a call queue, auto attendant, or any service number with the **New-CsCallingLineIdentity** cmdlet as in the following example:

``` Powershell
New-CsCallingLineIdentity -Identity "UKSalesQueue" -CallingIdSubstitute "Service" -ServiceNumber 14258828080 -EnableUserOverride $False -Verbose
```

Then apply the policy to the user with the **Grant-CallingLineIdentity** cmdlet as in the following example: 

``` Powershell
Grant-CsCallingLineIdentity -PolicyName UKSalesQueue -Identity "AmosMarble@contoso.com"
```

For more information, see [How can caller ID be used in your organization](/microsoftteams/how-can-caller-id-be-used-in-your-organization).

## Call queue cmdlets

You can also use Windows PowerShell to create and set up call queues. Here are the cmdlets that you use to manage a call queue.

- [New-CsCallQueue](https://docs.microsoft.com/powershell/module/skype/new-CsCallQueue?view=skype-ps)

- [Set-CsCallQueue](https://docs.microsoft.com/powershell/module/skype/set-CsCallQueue?view=skype-ps)

- [Get-CsCallQueue](https://docs.microsoft.com/powershell/module/skype/get-CsCallQueue?view=skype-ps)

- [Remove-CsCallQueue](https://docs.microsoft.com/powershell/module/skype/remove-CsCallQueue?view=skype-ps)

### More about Windows PowerShell

- Windows PowerShell is all about managing users and what users are allowed or not allowed to do. With Windows PowerShell, you can manage Microsoft 365 or Office 365 and Microsoft Teams with a single point of administration. It can simplify your daily work, when you have multiple tasks to do. To get started with Windows PowerShell, see these topics:

  - [An introduction to Windows PowerShell and Skype for Business Online](/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)

  - [Why you need to use Office 365 PowerShell](https://docs.microsoft.com/office365/enterprise/powershell/why-you-need-to-use-office-365-powershell)

- Windows PowerShell has many advantages in speed, simplicity, and productivity over the Microsoft Teams admin center when you make changes for many users at once. Learn about these advantages in the following topics:

  - [Manage Microsoft 365 or Office 365 with Windows PowerShell](https://docs.microsoft.com/office365/enterprise/powershell/manage-office-365-with-office-365-powershell)

  - [Set up your computer for Windows PowerShell](https://docs.microsoft.com/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)

## Related topics

[Here's what you get with Phone System](here-s-what-you-get-with-phone-system.md)

[Getting service phone numbers](getting-service-phone-numbers.md)

[Country and region availability for Audio Conferencing and Calling Plans](country-and-region-availability-for-audio-conferencing-and-calling-plans/country-and-region-availability-for-audio-conferencing-and-calling-plans.md)

[New-CsOnlineApplicationInstance](https://docs.microsoft.com/powershell/module/skype/new-csonlineapplicationinstance?view=skype-ps)
