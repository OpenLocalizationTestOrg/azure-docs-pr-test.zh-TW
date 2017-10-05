---
title: "在 Azure Active Directory 中建立使用者群組 | Microsoft Docs"
description: "如何在 Azure Active Directory 中建立群組並將成員新增到群組中"
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
ms.openlocfilehash: 6d3d37761a9fdf9bd9801396d45f2fcd47efb0be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="824c0-103">在 Azure Active Directory 中建立群組和新增使用者</span><span class="sxs-lookup"><span data-stu-id="824c0-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="824c0-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="824c0-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="824c0-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="824c0-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="824c0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="824c0-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="824c0-107">本文說明如何在 Azure Active Directory 中建立及填入新群組。</span><span class="sxs-lookup"><span data-stu-id="824c0-107">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="824c0-108">您可以使用群組來執行管理工作，例如將授權或權限一次指派給數個使用者或裝置。</span><span class="sxs-lookup"><span data-stu-id="824c0-108">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="824c0-109">如何建立群組？</span><span class="sxs-lookup"><span data-stu-id="824c0-109">How do I create a group?</span></span>
1. <span data-ttu-id="824c0-110">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="824c0-110">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="824c0-111">選取 [更多服務]，在文字方塊中輸入**使用者和群組**，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="824c0-111">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="824c0-113">在 [使用者和群組] 刀鋒視窗上，選取 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="824c0-113">On the **Users and groups** blade, select **All groups**.</span></span>

   ![開啟群組刀鋒視窗](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="824c0-115">在 [使用者和群組 - 所有群組] 刀鋒視窗上，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="824c0-115">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![選取 [新增] 命令](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="824c0-117">在 [群組]  刀鋒視窗上，輸入群組的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="824c0-117">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="824c0-118">若要選取要新增到群組中的成員，請在 [成員資格類型] 方塊中選取 [已指派]，然後選取 [成員]。</span><span class="sxs-lookup"><span data-stu-id="824c0-118">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="824c0-119">如需有關如何動態管理群組成員資格的詳細資訊，請參閱 [使用屬性來建立群組成員資格的進階規則](active-directory-groups-dynamic-membership-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="824c0-119">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![選取要新增的成員](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="824c0-121">在 [成員] 刀鋒視窗上，選取一或多個要新增到群組中的使用者或裝置，然後選取刀鋒視窗底部的 [選取] 按鈕來將它們新增到群組中。</span><span class="sxs-lookup"><span data-stu-id="824c0-121">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="824c0-122">[使用者]  方塊會根據將您的輸入內容與使用者或裝置名稱的任何部分進行比對來篩選顯示。</span><span class="sxs-lookup"><span data-stu-id="824c0-122">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="824c0-123">該方塊中不接受任何萬用字元。</span><span class="sxs-lookup"><span data-stu-id="824c0-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="824c0-124">完成將成員新增到群組中時，在 [群組] 刀鋒視窗上選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="824c0-124">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![建立群組確認](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="824c0-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="824c0-126">Next steps</span></span>
<span data-ttu-id="824c0-127">這些文章提供有關 Azure Active Directory 的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="824c0-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="824c0-128">查看現有的群組</span><span class="sxs-lookup"><span data-stu-id="824c0-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="824c0-129">管理群組的設定</span><span class="sxs-lookup"><span data-stu-id="824c0-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="824c0-130">管理群組的成員</span><span class="sxs-lookup"><span data-stu-id="824c0-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="824c0-131">管理群組的成員資格</span><span class="sxs-lookup"><span data-stu-id="824c0-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="824c0-132">管理群組中使用者的動態規則</span><span class="sxs-lookup"><span data-stu-id="824c0-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
