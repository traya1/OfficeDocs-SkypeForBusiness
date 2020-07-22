---
title: Manage policy packages in Microsoft Teams
author: lanachin
ms.author: v-lanac
manager: serdars
ms.reviewer: sekrantz, aaglick
ms.topic: article
ms.tgt.pltfrm: cloud
ms.service: msteams
audience: Admin
ms.collection: 
  - M365-collaboration
appliesto: 
  - Microsoft Teams
f1.keywords:
- CSH
ms.custom: 
- ms.teamsadmincenter.policypackages.overview
- seo-marvel-apr2020
localization_priority: Normal
search.appverid: MET150
description: Learn how to use and manage policy packages in Microsoft Teams to simplify, streamline, and help provide consistency when managing policies for groups of users.
---

# Manage policy packages in Microsoft Teams

A policy package in Microsoft Teams is a collection of predefined policies and policy settings that you can assign to users who have similar roles in your organization. We built policy packages to simplify, streamline, and help provide consistency when managing policies for groups of users across your organization.  

When you assign a policy package to users, the policies in the package are created and you can then customize the settings of the policies in the package to meet your organization's needs.

## What is a policy package

Policy packages let you control Teams features that you want to allow or restrict for specific sets of people across your organization. Each policy package in Teams is designed around a user role and includes predefined policies and policy settings that support the collaboration and communication activities that are typical for that role.

Teams currently includes the following policy packages.

|**Package name**  |**Description** |
|---------|---------|
|Education (Higher education student)    |Creates a set of policies and policy settings that apply to higher education students.|
|Education (Primary school student)   |Creates a set of policies and policy settings that apply to primary students.|
|Education (Secondary school student)    |Creates a set of policies and policy settings that apply to secondary students.         |
|Education (Teacher)    |Creates a set of policies and policy settings that apply to teachers.      |
|Education (Primary school teacher using remote learning)    |Creates a set of policies that apply to primary teachers to maximize student safety and collaboration when using remote learning.      |
|Education (Primary school student using remote learning)    |Creates a set of policies that apply to primary students to maximize student safety and collaboration when using remote learning.      |
|Firstline manager |Creates a set of policies and applies those settings to Firstline Managers in your organization. |
|Firstline worker |Creates a set of policies and applies those settings to Firstline Workers in your organization. |
|Healthcare clinical worker  |Creates a set of policies and policy settings that give clinical workers such as registered nurses, charge nurses, physicians, and social workers full access to chat, calling, shift management, and meetings. |
|Healthcare information worker  |Creates a set of policies and policy settings that give information workers such as IT personnel, informatics staff, finance personnel, and compliance officers, full access to chat, calling, and meetings.|
|Healthcare patient room  |Creates a set of policies and policy settings that apply to patient rooms in your healthcare organization.|
|Small and medium business user (Business Voice) |Creates an app setup policy that includes the apps for a business voice experience.|
|Small and medium business user (without Business Voice) |Creates an app setup policy relevant for a small and medium sized business Teams users (non-Business Voice experience).
|Public safety officer   |Creates a set of policies and policy settings that apply to public safety officers in your organization.|

> [!NOTE]
> We'll be adding more policy packages in future releases of Teams, so check back for the most up-to-date information.  

Each individual policy is given the name of the policy package so you can easily identify the policies that are linked to a policy package.
For example, when you assign the Education (Teacher) policy package to teachers in your school, a policy that's named Education_Teacher is created for each policy in the package.

![Screenshot of the Education (Teacher) policy package](media/policy-packages-education_teacher.png)

## How to use policy packages

The following outlines how to use policy packages in your organization.

![Overview of how to use policy packages](media/manage-policy-packages-overview.png)

- **[View](#view-the-settings-of-a-policy-in-a-policy-package)**: View the settings of each policy in a policy package before you assign a package. Make sure that you understand each setting and then decide whether the predefined values are appropriate for your organization or whether you need to change them to be more restrictive or lenient based on your organization's needs.

    If a policy is deleted, you can still view the settings but you won't be able to change any settings. A deleted policy is re-created with the predefined settings when you assign the policy package.

- **[Assign](#assign-a-policy-package)**: Assign the policy package to users. Remember that policies in a policy package aren't created until you assign the package, after which you can change the settings of individual policies in the package.  

- **[Customize](#customize-policies-in-a-policy-package)**: Customize the settings of policies in the policy package to fit the needs of your organization. Any changes you make to policy settings are automatically applied to users who are assigned the package.

Here are the steps for how to view, assign, and customize policy packages in the Microsoft Teams admin center.

### View the settings of a policy in a policy package

1. In the left navigation of the Microsoft Teams admin center, click **Policy packages**, and then select a policy package by clicking to the left of the package name.
2. Click the policy you want to view.

### Assign a policy package

#### Assign a policy package to one user

1. In the left navigation of the Microsoft Teams admin center, go to **Users**, and then click the user.
2. On the user's page, click **Policies**, and then next to **Policy package**, click **Edit**.
3. In the **Assign policy package** pane, select the package you want to assign, and then click **Save**.

#### Assign a policy package to multiple users

1. In the left navigation of the Microsoft Teams admin center, go to **Policy packages**, and then select the policy package you want to assign by clicking to the left of the package name.
2. Click **Manage users**.
3. In the **Manage users** pane, search for the user by display name or by user name, select the name, and then click **Add**. Repeat this step for each user that you want to add.
4. When you're finished adding users, click **Save**.

#### Assign a policy package to a large set (batch) of users

Use batch policy package assignment to assign a policy package to large sets of users at a time. You use the [New-CsBatchPolicyPackageAssignmentOperation](https://docs.microsoft.com/powershell/module/teams/new-csbatchpolicypackageassignmentoperation) cmdlet to submit a batch of users and the policy package that you want to assign. The assignments are processed as a background operation and an operation ID is generated for each batch.

A batch can contain up to 5,000 users. You can specify users by their object Id, UPN, SIP address, or email address. To learn more, see [Assign a policy package to a batch of users](assign-policies.md#assign-a-policy-package-to-a-batch-of-users).

### Customize policies in a policy package

You can edit the settings of a policy through the **Policy packages** page or by going directly to the policy page in the Microsoft Teams admin center.

1. In the left navigation of the Microsoft Teams admin center, do one of the following:
    - Click **Policy packages**, and then select the policy package by clicking to the left of the package name.
    - Click the policy type.  For example, click **Messaging policies**.
2. Click the policy you want to edit. Policies that are linked to a policy package have the same name as the policy package.
3. Make the changes that you want, and then click **Save**.

## Troubleshooting

**You receive an error when you assign a policy package**

This may occur if one or more policies in the package weren't created or applied successfully. Reassign the policy package to your users. Retrying the operation typically fixes this issue.

## Related topics

[Microsoft Teams policy packages for EDU admins](policy-packages-edu.md)
