---
title: "aaaAssign 使用者在 Azure Active Directory tooadministrator 角色 |Microsoft 文件"
description: "說明如何在 Azure Active Directory toochange 使用者管理資訊"
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
ms.openlocfilehash: 8bb6711c2570843962fe075b6026542a4bca525f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-tooadministrator-roles-in-azure-active-directory"></a><span data-ttu-id="22e8e-103">在 Azure Active Directory tooadministrator 角色指派給使用者</span><span class="sxs-lookup"><span data-stu-id="22e8e-103">Assign a user tooadministrator roles in Azure Active Directory</span></span>
<span data-ttu-id="22e8e-104">這篇文章說明如何在 Azure Active Directory (Azure AD) 中的系統管理角色 tooa 使用者 tooassign。</span><span class="sxs-lookup"><span data-stu-id="22e8e-104">This article explains how tooassign an administrative role tooa user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="22e8e-105">如需在組織中加入新的使用者資訊，請參閱[加入新使用者 tooAzure Active Directory](active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="22e8e-105">For information about adding new users in your organization, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="22e8e-106">新增的使用者時，不需要系統管理員權限，根據預設，但您可以在任何時間指派角色 toothem。</span><span class="sxs-lookup"><span data-stu-id="22e8e-106">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="22e8e-107">指派給某個角色 tooa 使用者</span><span class="sxs-lookup"><span data-stu-id="22e8e-107">Assign a role tooa user</span></span>
1. <span data-ttu-id="22e8e-108">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="22e8e-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="22e8e-109">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="22e8e-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="22e8e-111">在 hello**使用者和群組**刀鋒視窗中，選取**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="22e8e-111">On hello **Users and groups** blade, select **All users**.</span></span>

   ![開啟 hello 所有使用者 刀鋒視窗](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="22e8e-113">在 hello**使用者和群組的所有使用者**刀鋒視窗中，選取的使用者從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="22e8e-113">On hello **Users and groups - All users** blade, select a user from hello list.</span></span>
5. <span data-ttu-id="22e8e-114">在 hello 選使用者的 hello 刀鋒視窗，選取 **目錄角色**，然後將 hello 使用者 tooa 角色指派從 hello**目錄角色**清單。</span><span class="sxs-lookup"><span data-stu-id="22e8e-114">On hello blade for hello selected user, select **Directory role**, and then assign hello user tooa role from hello **Directory role** list.</span></span> <span data-ttu-id="22e8e-115">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="22e8e-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![將使用者 tooa 角色指派](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="22e8e-117">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="22e8e-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22e8e-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22e8e-118">Next steps</span></span>
* [<span data-ttu-id="22e8e-119">新增使用者</span><span class="sxs-lookup"><span data-stu-id="22e8e-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="22e8e-120">重設使用者密碼在 hello 新版 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="22e8e-120">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="22e8e-121">變更使用者的工作資訊</span><span class="sxs-lookup"><span data-stu-id="22e8e-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="22e8e-122">管理使用者設定檔</span><span class="sxs-lookup"><span data-stu-id="22e8e-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="22e8e-123">在 Azure AD 中刪除使用者</span><span class="sxs-lookup"><span data-stu-id="22e8e-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
