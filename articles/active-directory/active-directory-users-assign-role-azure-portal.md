---
title: "在 Azure Active Directory 中將使用者指派給系統管理員角色 | Microsoft Docs"
description: "說明如何在 Azure Active Directory 中變更使用者系統管理資訊"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="10b99-103">在 Azure Active Directory 中將使用者指派給系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="10b99-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="10b99-104">本文說明如何在 Azure Active Directory (Azure AD) 中將系統管理角色指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="10b99-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="10b99-105">如需有關在您組織中新增新使用者的資訊，請參閱[將新的使用者新增到 Azure Active Directory](active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="10b99-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="10b99-106">新增的使用者預設不會有系統管理員權限，但是您可以隨時指派角色給他們。</span><span class="sxs-lookup"><span data-stu-id="10b99-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="10b99-107">將角色指派給使用者</span><span class="sxs-lookup"><span data-stu-id="10b99-107">Assign a role to a user</span></span>
1. <span data-ttu-id="10b99-108">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="10b99-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="10b99-109">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="10b99-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="10b99-111">在 [使用者和群組] 刀鋒視窗上，選取 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="10b99-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![開啟 [所有使用者] 刀鋒視窗](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="10b99-113">在 [使用者和群組 - 所有使用者]  刀鋒視窗上，從清單中選取一個使用者。</span><span class="sxs-lookup"><span data-stu-id="10b99-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="10b99-114">在所選使用者的刀鋒視窗上，選取 [目錄角色]，然後將使用者指派給 [目錄角色] 清單中的角色。</span><span class="sxs-lookup"><span data-stu-id="10b99-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="10b99-115">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="10b99-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![將使用者指派給角色](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="10b99-117">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="10b99-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10b99-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10b99-118">Next steps</span></span>
* [<span data-ttu-id="10b99-119">新增使用者</span><span class="sxs-lookup"><span data-stu-id="10b99-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="10b99-120">在新 Azure 入口網站中重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="10b99-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="10b99-121">變更使用者的工作資訊</span><span class="sxs-lookup"><span data-stu-id="10b99-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="10b99-122">管理使用者設定檔</span><span class="sxs-lookup"><span data-stu-id="10b99-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="10b99-123">在 Azure AD 中刪除使用者</span><span class="sxs-lookup"><span data-stu-id="10b99-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
