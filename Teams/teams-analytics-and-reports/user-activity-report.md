---
title: Microsoft Teams user activity report
author: LanaChin
ms.author: v-lanac
manager: serdars
audience: Admin
ms.topic: article
ms.service: msteams
ms.reviewer: svemu
f1.keywords:
- NOCSH
localization_priority: Normal
search.appverid: MET150
ms.collection: 
  - M365-collaboration
description: Learn how to use the Teams user activity report in the Microsoft Teams admin center to see how users in your organization are using Teams.
appliesto: 
  - Microsoft Teams
ms.custom: seo-marvel-apr2020
---

# Microsoft Teams user activity report

The Teams user activity report gives you insight into the types of activities that users in your organization perform in Teams. For example, you can see how many users communicate through 1:1 calls, how many users communicate through channel messages, and how many users engage in private chat messages.

## View the user activity report

You must be an admin to make these changes. See [Use Teams administrator roles to manage Teams](https://docs.microsoft.com/microsoftteams/using-admin-roles) to read about getting admin roles and permissions.

1. In the left navigation of the admin center, click **Analytics & reports** > **Usage reports**. On the **View reports** tab, under **Report**, select **Teams user activity**.
2. Under **Date range**, select a range, and then click **Run report**.

    ![Screenshot of the Teams user activity report in the Teams admin center with callouts](../media/teams-reports-user-activity-with-callouts.png "Screenshot of the Teams user activity report in the Teams admin center with callouts")

## Interpret the report

|Callout |Description  |
|--------|-------------|
|**1**   |The Teams user activity report can be viewed for trends over the last 7 days, 28 or 90 days. |
|**2**   |Each report has a date for when this report was generated. The reports usually reflect a 24 to 48 hour latency from time of activity. |
|**3**   |<ul><li>The X axis on the charts is the selected date range for the specific report. </li><li>The Y axis is the number of users participating in the activity.</li></ul>Hover over the dot representing an activity on a given date to see the number of instances of that activity on that given date. |
|**4**   |You can filter what you see on the chart by clicking an item in the legend. For example, click **1:1 calls**, **Channel messages**, or **Chat messages** to see only the info related to each one. Changing the selection doesn’t change the information in the table. |
|**5**   |The table gives you a breakdown of usage by user.   <ul><li>**Display name** is the display name of the user. You can click the display name to go to the user's setting page in the Microsoft Teams admin center.</li><li>**1:1 calls** is the number of 1:1 calls that the user participated in during the specified time period.</li><li>**Channel messages** is the number of unique messages that the user posted in a team chat during the specified time period.</li><li>**Reply messages** is the number of unique reply messages that the user posted in a team channel during the specified time period.</li> <li>**Post messages** is the number of unique post messages that the user posted in a team channel during the specified time period.</li><li>**Meetings organized** is the number of scheduled meetings a user organized during the specified time period.</li><li>**Meetings participated** is the number of scheduled meetings a user participated in during the specified time period.</li><li>**Chat messages** is the number of unique messages that the user posted in a private chat during the specified time period.</li><li>**Urgent messages** is the number of urgent messages that the user posted in a  chat during the specified time period.</li><li>**Group Calls** is the number of group calls that the user participated in during the specified time period.</li><li>**Audio time** is the total audio time that the user participated in during the specified time period.</li><li>**Video time** is the total video time that the user participated in during the specified time period.</li><li>**Screen Share time** is the total screen share time that the user participated in during the specified time period.</li>  <li>**Last activity** is the last date (UTC) that the user participated in a Teams activity.</li> </ul>Note that if a user account no longer exists in Azure AD, the user name is displayed as "--" in the table. <br><br>To see the information that you want in the table, make sure to add the columns to the table.
|**6**   |Select **Edit columns** to add or remove columns in the table. |
|**7**   |You can export the report to a CSV file for offline analysis. Click **Export to Excel**, and then on the **Downloads** tab, click **Download** to download the report when it's ready.<br><br>![Screenshot of the Downloads tab showing exported reports to download](../media/teams-reports-export-to-csv.png) <br>When you view the report in Excel, you'll also see an **Id** column, which represents the team ID. A team ID is typically an alphanumeric string. If the **Id** column shows as **\n**, this means that a user requested their information to be deleted. ||

[!INCLUDE [teams-reports-definitions](../includes/teams-reports-definitions.md)]

## Related topics

- [Teams analytics and reporting](teams-reporting-reference.md)
