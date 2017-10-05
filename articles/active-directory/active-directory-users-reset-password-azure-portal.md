---
title: "Azure Active Directory 中的密碼重設 | Microsoft Docs"
description: "說明如何在 Azure Active Directory 中重設使用者的密碼"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fad5624b-2f13-4abc-b3d4-b347903a8f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8e7c38c7f0d40a310dd0b6bd0e866d2d55115550
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="reset-the-password-for-a-user-in-azure-active-directory"></a><span data-ttu-id="6b877-103">在 Azure Active Directory 中重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="6b877-103">Reset the password for a user in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b877-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6b877-104">Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
> * [<span data-ttu-id="6b877-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="6b877-105">Azure classic portal</span></span>](active-directory-create-users-reset-password.md)
>
>

## <a name="how-to-reset-the-password-for-a-user"></a><span data-ttu-id="6b877-106">如何重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="6b877-106">How to reset the password for a user</span></span>
1. <span data-ttu-id="6b877-107">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="6b877-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="6b877-108">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="6b877-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-users-reset-password-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="6b877-110">在 [使用者和群組] 刀鋒視窗上，選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="6b877-110">On the **Users and groups** blade, select **Users**.</span></span>

   ![開啟 [使用者] 刀鋒視窗](./media/active-directory-users-reset-password-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="6b877-112">在 [使用者和群組 - 使用者]  刀鋒視窗上，從清單中選取一個使用者。</span><span class="sxs-lookup"><span data-stu-id="6b877-112">On the **Users and groups - Users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="6b877-113">在所選使用者的刀鋒視窗上選取 [概觀]，然後在命令列中選取 [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="6b877-113">On the blade for the selected user, select **Overview**, and then in the command bar, select **Reset password**.</span></span>

    ![選取 [重設密碼] 命令](./media/active-directory-users-reset-password-azure-portal/create-users-reset-password-command.png)
6. <span data-ttu-id="6b877-115">在 [重設密碼] 刀鋒視窗上，選取 [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="6b877-115">On the **Reset password** blade, select **Reset password**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b877-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b877-116">Next steps</span></span>
* [<span data-ttu-id="6b877-117">新增使用者</span><span class="sxs-lookup"><span data-stu-id="6b877-117">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="6b877-118">在 Azure AD 中將使用者指派給角色</span><span class="sxs-lookup"><span data-stu-id="6b877-118">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
* [<span data-ttu-id="6b877-119">變更使用者的工作資訊</span><span class="sxs-lookup"><span data-stu-id="6b877-119">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="6b877-120">管理使用者設定檔</span><span class="sxs-lookup"><span data-stu-id="6b877-120">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="6b877-121">在 Azure AD 中刪除使用者</span><span class="sxs-lookup"><span data-stu-id="6b877-121">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
