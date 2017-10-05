---
title: "在 Azure Active Directory 中將使用者從目錄中刪除 | Microsoft Docs"
description: "說明如何從 Azure Active Directory 中刪除使用者及其所有資訊"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bd1c9ccc-2d80-42bf-82cc-db37bb1a1d67
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: 19a4d2c37c785b3b56a2e0e1b6797ec56dad9835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-user-from-a-directory-in-azure-active-directory"></a><span data-ttu-id="5d6f1-103">在 Azure Active Directory 中將使用者從目錄中刪除</span><span class="sxs-lookup"><span data-stu-id="5d6f1-103">Delete a user from a directory in Azure Active Directory</span></span>
<span data-ttu-id="5d6f1-104">本文說明如何在 Azure Active Directory (Azure AD) 中將使用者從目錄中刪除。</span><span class="sxs-lookup"><span data-stu-id="5d6f1-104">This article explains how to delete a user from a directory in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5d6f1-105">如需有關將新的使用者新增至組織的資訊，請參閱[將新的使用者新增至 Azure Active Directory](active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="5d6f1-105">For information about adding new users to your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="to-delete-a-user"></a><span data-ttu-id="5d6f1-106">刪除使用者</span><span class="sxs-lookup"><span data-stu-id="5d6f1-106">To delete a user</span></span>
1. <span data-ttu-id="5d6f1-107">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5d6f1-107">Sign in to [the Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="5d6f1-108">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="5d6f1-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-users-delete-user-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="5d6f1-110">在 [使用者和群組] 刀鋒視窗上，選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="5d6f1-110">On the **Users and groups** blade, select **Users**.</span></span>

   ![開啟 [使用者] 刀鋒視窗](./media/active-directory-users-delete-user-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="5d6f1-112">在 [使用者和群組 - 使用者]  刀鋒視窗上，從清單中選取一個使用者。</span><span class="sxs-lookup"><span data-stu-id="5d6f1-112">On the **Users and groups - Users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="5d6f1-113">在所選使用者的刀鋒視窗上選取 [概觀]，然後在命令列中選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="5d6f1-113">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![選取 [刪除] 命令](./media/active-directory-users-delete-user-azure-portal/create-users-delete-command.png)

## <a name="next-steps"></a><span data-ttu-id="5d6f1-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d6f1-115">Next steps</span></span>
* [<span data-ttu-id="5d6f1-116">將新的使用者加入 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d6f1-116">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="5d6f1-117">在 Azure Active Directory 中重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="5d6f1-117">Reset the password for a user in Azure Active Directory</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="5d6f1-118">在 Azure Active Directory 中將使用者指派給系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="5d6f1-118">Assign a user to administrator roles in Azure Active Directory</span></span>](active-directory-users-assign-role-azure-portal.md)
* [<span data-ttu-id="5d6f1-119">在 Azure Active Directory 中新增或變更使用者的設定檔資訊</span><span class="sxs-lookup"><span data-stu-id="5d6f1-119">Add or change profile information for a user in Azure Active Directory</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="5d6f1-120">在 Azure Active Directory 中將使用者從目錄中刪除</span><span class="sxs-lookup"><span data-stu-id="5d6f1-120">Delete a user from a directory in Azure Active Directory</span></span>](active-directory-users-profile-azure-portal.md)