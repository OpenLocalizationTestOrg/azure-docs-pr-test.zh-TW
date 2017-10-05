---
title: "在 Azure Active Directory 中管理群組的成員 | Microsoft Docs"
description: "如何在 Azure Active Directory 的群組中新增或移除使用者和裝置"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="2f325-103">管理 Azure Active Directory 租用戶中使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="2f325-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="2f325-104">本文說明如何在 Azure Active Directory (Azure AD) 中管理群組的成員。</span><span class="sxs-lookup"><span data-stu-id="2f325-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="2f325-105">如何尋找成員及管理這些成員？</span><span class="sxs-lookup"><span data-stu-id="2f325-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="2f325-106">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="2f325-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="2f325-107">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="2f325-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="2f325-109">在 [使用者和群組] 刀鋒視窗上，選取 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="2f325-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![開啟群組刀鋒視窗](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="2f325-111">在 [使用者和群組 - 所有群組]  刀鋒視窗上，選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="2f325-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="2f325-112">在 [群組- *groupname*] 刀鋒視窗上，選取 [成員]。</span><span class="sxs-lookup"><span data-stu-id="2f325-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![開啟 [成員] 刀鋒視窗](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="2f325-114">若要將成員新增到群組中，請在 [群組 - 成員] 刀鋒視窗上，選取 [新增成員]。</span><span class="sxs-lookup"><span data-stu-id="2f325-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![[新增成員] 命令](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="2f325-116">在 [成員] 刀鋒視窗上，選取一或多個要新增到群組中的使用者或裝置，然後選取刀鋒視窗底部的 [選取] 按鈕來將它們新增到群組中。</span><span class="sxs-lookup"><span data-stu-id="2f325-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="2f325-117">[使用者]  方塊會根據將您的輸入內容與使用者或裝置名稱的任何部分進行比對來篩選顯示。</span><span class="sxs-lookup"><span data-stu-id="2f325-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="2f325-118">該方塊中不接受任何萬用字元。</span><span class="sxs-lookup"><span data-stu-id="2f325-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="2f325-119">若要從群組中移除成員，請在 [群組 - 成員]  刀鋒視窗上，選取一個成員。</span><span class="sxs-lookup"><span data-stu-id="2f325-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="2f325-120">在 [***membername***] 刀鋒視窗上，選取 [移除] 命令，並在出現提示時確認您的選擇。</span><span class="sxs-lookup"><span data-stu-id="2f325-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![[移除成員] 命令](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="2f325-122">完成變更群組的成員時，選取 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2f325-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="2f325-123">其他資訊</span><span class="sxs-lookup"><span data-stu-id="2f325-123">Additional information</span></span>
<span data-ttu-id="2f325-124">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="2f325-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="2f325-125">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="2f325-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="2f325-126">建立新群組並新增成員</span><span class="sxs-lookup"><span data-stu-id="2f325-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="2f325-127">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="2f325-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="2f325-128">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="2f325-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="2f325-129">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="2f325-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
