---
title: "aaaManage hello 群組成員的 Azure Active Directory 中 |Microsoft 文件"
description: "如何 tooadd 或從 Azure Active Directory 中的群組移除使用者和裝置"
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
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="37a6e-103">管理 Azure Active Directory 租用戶中使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="37a6e-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="37a6e-104">本文說明如何 toomanage hello Azure Active Directory (Azure AD) 中之群組的成員。</span><span class="sxs-lookup"><span data-stu-id="37a6e-104">This article explains how toomanage hello members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-hello-members-and-manage-them"></a><span data-ttu-id="37a6e-105">如何尋找 hello 成員和進行管理？</span><span class="sxs-lookup"><span data-stu-id="37a6e-105">How do I find hello members and manage them?</span></span>
1. <span data-ttu-id="37a6e-106">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="37a6e-106">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="37a6e-107">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="37a6e-107">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="37a6e-109">在 hello**使用者和群組**刀鋒視窗中，選取**所有群組**。</span><span class="sxs-lookup"><span data-stu-id="37a6e-109">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![開啟 hello 群組刀鋒視窗](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="37a6e-111">在 hello**使用者和群組的所有群組**刀鋒視窗中，選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="37a6e-111">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="37a6e-112">在 hello**群組- *groupname*** 刀鋒視窗中，選取**成員**。</span><span class="sxs-lookup"><span data-stu-id="37a6e-112">On hello **Group - *groupname*** blade, select **Members**.</span></span>

   ![開啟 hello 成員刀鋒視窗](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="37a6e-114">在 hello，tooadd 成員 toohello 群組**群組-成員**刀鋒視窗中，選取**新增成員**。</span><span class="sxs-lookup"><span data-stu-id="37a6e-114">tooadd members toohello group, on hello **Group - Members** blade, select **Add Members**.</span></span>

   ![[新增成員] 命令](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="37a6e-116">在 hello**成員**刀鋒視窗中，選取其中一個或多個使用者或裝置 tooadd toohello 群組則選取 hello**選取**按鈕在 hello 底部 hello 刀鋒視窗 tooadd 它們 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="37a6e-116">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="37a6e-117">hello**使用者**方塊篩選 hello 顯示根據比對您的使用者或裝置名稱的項目 tooany 部分。</span><span class="sxs-lookup"><span data-stu-id="37a6e-117">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="37a6e-118">該方塊中不接受任何萬用字元。</span><span class="sxs-lookup"><span data-stu-id="37a6e-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="37a6e-119">從 hello 群組 hello tooremove 成員**群組-成員**刀鋒視窗中，選取的成員。</span><span class="sxs-lookup"><span data-stu-id="37a6e-119">tooremove members from hello group, on hello **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="37a6e-120">在 hello ***membername***刀鋒視窗中，選取 hello**移除**命令，然後確認您選擇在 hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="37a6e-120">On hello ***membername*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![[移除成員] 命令](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="37a6e-122">當您完成變更 hello 群組的成員時，選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="37a6e-122">When you finish changing members for hello group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="37a6e-123">其他資訊</span><span class="sxs-lookup"><span data-stu-id="37a6e-123">Additional information</span></span>
<span data-ttu-id="37a6e-124">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="37a6e-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="37a6e-125">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="37a6e-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="37a6e-126">建立新群組並新增成員</span><span class="sxs-lookup"><span data-stu-id="37a6e-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="37a6e-127">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="37a6e-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="37a6e-128">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="37a6e-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="37a6e-129">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="37a6e-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
