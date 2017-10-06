---
title: "您的群組所屬 tooin Azure Active Directory aaaManage hello 群組 |Microsoft 文件"
description: "在 Azure Active Directory 中，群組可以包含其他群組。 以下是如何 toomanage 那些成員資格。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="34dae-104">管理您的 Azure Active Directory 租用戶中的群組所屬的 toowhich 群組</span><span class="sxs-lookup"><span data-stu-id="34dae-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="34dae-105">在 Azure Active Directory 中，群組可以包含其他群組。</span><span class="sxs-lookup"><span data-stu-id="34dae-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="34dae-106">以下是如何 toomanage 那些成員資格。</span><span class="sxs-lookup"><span data-stu-id="34dae-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="34dae-107">如何找到我的群組隸屬的 hello 群組？</span><span class="sxs-lookup"><span data-stu-id="34dae-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="34dae-108">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="34dae-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="34dae-109">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取 [ **Enter**。</span><span class="sxs-lookup"><span data-stu-id="34dae-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="34dae-111">在 [hello**使用者和群組**刀鋒視窗中，選取**所有群組**。</span><span class="sxs-lookup"><span data-stu-id="34dae-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![開啟 hello 群組刀鋒視窗](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="34dae-113">在 [hello**使用者和群組的所有群組**刀鋒視窗中，選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="34dae-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="34dae-114">在 [hello**群組- *groupname* **刀鋒視窗中，選取**群組成員資格**。</span><span class="sxs-lookup"><span data-stu-id="34dae-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![開啟 hello 群組成員資格] 刀鋒視窗](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="34dae-116">tooadd hello 上的另一個群組的成員身分群組**群組-群組成員資格**刀鋒視窗中，選取 hello**新增**命令。</span><span class="sxs-lookup"><span data-stu-id="34dae-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="34dae-117">選取群組從 hello**選取群組**刀鋒視窗，，然後選取 hello**選取**在 hello hello 刀鋒視窗底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="34dae-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="34dae-118">您可以加入群組 tooonly 的一個群組，一次。</span><span class="sxs-lookup"><span data-stu-id="34dae-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="34dae-119">hello**使用者**方塊篩選 hello 顯示根據比對您的使用者或裝置名稱的項目 tooany 部分。</span><span class="sxs-lookup"><span data-stu-id="34dae-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="34dae-120">該方塊中不接受任何萬用字元。</span><span class="sxs-lookup"><span data-stu-id="34dae-120">No wildcard characters are accepted in that box.</span></span>

   ![新增群組成員資格](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="34dae-122">tooremove hello 上的另一個群組的成員身分群組**群組-群組成員資格**刀鋒視窗中，選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="34dae-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="34dae-123">在 [hello ***groupname***刀鋒視窗中，選取 hello**移除**命令，然後確認您選擇在 hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="34dae-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![移除成員資格命令](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="34dae-125">完成變更您群組的群組成員資格時，選取 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="34dae-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="34dae-126">其他資訊</span><span class="sxs-lookup"><span data-stu-id="34dae-126">Additional information</span></span>
<span data-ttu-id="34dae-127">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="34dae-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="34dae-128">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="34dae-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="34dae-129">建立新群組並新增成員</span><span class="sxs-lookup"><span data-stu-id="34dae-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="34dae-130">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="34dae-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="34dae-131">管理群組的成員</span><span class="sxs-lookup"><span data-stu-id="34dae-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="34dae-132">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="34dae-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
