---
title: "Azure Active Directory 中的使用者群組 aaaCreate |Microsoft 文件"
description: "如何 toocreate Azure Active Directory 中的群組，並加入成員 toohello 群組"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="f2f0e-103">在 Azure Active Directory 中建立群組和新增使用者</span><span class="sxs-lookup"><span data-stu-id="f2f0e-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2f0e-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f2f0e-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="f2f0e-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="f2f0e-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="f2f0e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2f0e-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="f2f0e-107">這篇文章說明如何 toocreate 並填入 Azure Active Directory 中的新群組。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="f2f0e-108">使用群組 tooperform 管理工作，例如指派授權或權限的使用者或裝置的 tooa 數次。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="f2f0e-109">如何建立群組？</span><span class="sxs-lookup"><span data-stu-id="f2f0e-109">How do I create a group?</span></span>
1. <span data-ttu-id="f2f0e-110">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="f2f0e-111">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="f2f0e-113">在 hello**使用者和群組**刀鋒視窗中，選取**所有群組**。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![開啟 hello 群組刀鋒視窗](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="f2f0e-115">在 hello**使用者和群組的所有群組**刀鋒視窗中，選取 hello**新增**命令。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![選取 hello Add 命令](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="f2f0e-117">在 hello**群組**刀鋒視窗中，加入名稱與 hello 群組的描述。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="f2f0e-118">tooselect 成員 tooadd toohello 群組中，選取**指派**在 hello**成員資格類型**方塊，並選取**成員**。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="f2f0e-119">如需有關如何 toomanage hello 群組成員資格以動態方式的詳細資訊，請參閱[使用屬性 toocreate 進階規則群組的成員資格](active-directory-groups-dynamic-membership-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![選取成員 tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="f2f0e-121">在 hello**成員**刀鋒視窗中，選取其中一個或多個使用者或裝置 tooadd toohello 群組則選取 hello**選取**按鈕在 hello 底部 hello 刀鋒視窗 tooadd 它們 toohello 群組。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="f2f0e-122">hello**使用者**方塊篩選 hello 顯示根據比對您的使用者或裝置名稱的項目 tooany 部分。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="f2f0e-123">該方塊中不接受任何萬用字元。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="f2f0e-124">當您完成新增成員 toohello 群組時，選取**建立**上 hello**群組**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![建立群組確認](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="f2f0e-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2f0e-126">Next steps</span></span>
<span data-ttu-id="f2f0e-127">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="f2f0e-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="f2f0e-128">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="f2f0e-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="f2f0e-129">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="f2f0e-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="f2f0e-130">管理群組的成員</span><span class="sxs-lookup"><span data-stu-id="f2f0e-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="f2f0e-131">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="f2f0e-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="f2f0e-132">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="f2f0e-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
