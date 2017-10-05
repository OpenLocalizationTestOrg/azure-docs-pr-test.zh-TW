---
title: "將使用者新增至 Azure Active Directory | Microsoft Docs"
description: "說明如何在 Azure Active Directory 中新增新的使用者或變更使用者資訊。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="00b86-103">將新的使用者新增至 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00b86-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00b86-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="00b86-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="00b86-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="00b86-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="00b86-106">本文說明如何透過 Azure Active Directory (Azure AD)，在您的組織中新增新的使用者。</span><span class="sxs-lookup"><span data-stu-id="00b86-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="00b86-107">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="00b86-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="00b86-108">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="00b86-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者和群組](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="00b86-110">在 [使用者和群組] 刀鋒視窗上，選取 [所有使用者]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="00b86-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![選取 [新增] 命令](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="00b86-112">輸入使用者的詳細資料，例如「名稱」和「使用者名稱」。</span><span class="sxs-lookup"><span data-stu-id="00b86-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="00b86-113">使用者名稱的網域名稱部分必須是初始預設網域名稱 "foo.onmicrosoft.com" 網域名稱，或是已驗證的非同盟網域名稱，例如"contoso.com"。</span><span class="sxs-lookup"><span data-stu-id="00b86-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="00b86-114">複製或記下產生的使用者密碼，以便在此程序完成後，將它提供給使用者。</span><span class="sxs-lookup"><span data-stu-id="00b86-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="00b86-115">(選擇性) 您可以開啟使用者的 [設定檔] 刀鋒視窗、[群組] 刀鋒視窗或 [目錄角色] 刀鋒視窗，然後在其中填入資訊。</span><span class="sxs-lookup"><span data-stu-id="00b86-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="00b86-116">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="00b86-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="00b86-117">在 [使用者] 刀鋒視窗上，選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="00b86-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="00b86-118">將產生的密碼安全地散發給新使用者，以便讓使用者可以登入。</span><span class="sxs-lookup"><span data-stu-id="00b86-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="00b86-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00b86-119">Next steps</span></span>
* [<span data-ttu-id="00b86-120">新增外部使用者</span><span class="sxs-lookup"><span data-stu-id="00b86-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="00b86-121">在新 Azure 入口網站中重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="00b86-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="00b86-122">變更使用者的工作資訊</span><span class="sxs-lookup"><span data-stu-id="00b86-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="00b86-123">管理使用者設定檔</span><span class="sxs-lookup"><span data-stu-id="00b86-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="00b86-124">在 Azure AD 中刪除使用者</span><span class="sxs-lookup"><span data-stu-id="00b86-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="00b86-125">在 Azure AD 中將使用者指派給角色</span><span class="sxs-lookup"><span data-stu-id="00b86-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
