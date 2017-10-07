---
title: "aaaShare Azure 入口網站的儀表板使用 RBAC |Microsoft 文件"
description: "本文說明 tooshare 儀表板中的 hello Azure 入口網站使用以角色為基礎的存取控制的方式。"
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a><span data-ttu-id="91744-103">使用角色型存取控制來共用 Azure 儀表板</span><span class="sxs-lookup"><span data-stu-id="91744-103">Share Azure dashboards by using Role-Based Access Control</span></span>
<span data-ttu-id="91744-104">設定儀表板之後，您可以將它發佈，並與組織中的其他使用者共用。</span><span class="sxs-lookup"><span data-stu-id="91744-104">After configuring a dashboard, you can publish it and share it with other users in your organization.</span></span> <span data-ttu-id="91744-105">允許其他人 tooview 透過 Azure 儀表板[角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="91744-105">You allow others tooview your dashboard by using Azure [Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="91744-106">您指派使用者或群組的使用者 tooa 角色，而該角色定義這些使用者可以檢視或修改 hello 已發行的儀表板。</span><span class="sxs-lookup"><span data-stu-id="91744-106">You assign a user or group of users tooa role, and that role defines whether those users can view or modify hello published dashboard.</span></span> 

<span data-ttu-id="91744-107">所有已發佈的儀表板會實作為 Azure 資源，這表示它們是做為您訂用帳戶內可管理的項目而存在，並且會包含在資源群組中。</span><span class="sxs-lookup"><span data-stu-id="91744-107">All published dashboards are implemented as Azure resources, which means they exist as manageable items within your subscription and are contained in a resource group.</span></span>  <span data-ttu-id="91744-108">從存取控制的觀點來看，儀表板與其他資源 (例如虛擬機器或儲存體帳戶) 並無不同。</span><span class="sxs-lookup"><span data-stu-id="91744-108">From an access control perspective, dashboards are no different than other resources, such as a virtual machine or a storage account.</span></span>

> [!TIP]
> <span data-ttu-id="91744-109">個別的圖格 hello 儀表板上強制執行自己根據它們顯示 hello 資源的存取控制需求。</span><span class="sxs-lookup"><span data-stu-id="91744-109">Individual tiles on hello dashboard enforce their own access control requirements based on hello resources they display.</span></span>  <span data-ttu-id="91744-110">因此，您可以設計 hello 個別的磚上的資料仍受到保護時廣泛共用的儀表板。</span><span class="sxs-lookup"><span data-stu-id="91744-110">Therefore, you can design a dashboard that is shared broadly while still protecting hello data on individual tiles.</span></span>
> 
> 

## <a name="understanding-access-control-for-dashboards"></a><span data-ttu-id="91744-111">了解儀表板的存取控制</span><span class="sxs-lookup"><span data-stu-id="91744-111">Understanding access control for dashboards</span></span>
<span data-ttu-id="91744-112">使用角色型存取控制 (RBAC)，您可以指派使用者 tooroles 三個不同的範圍層級：</span><span class="sxs-lookup"><span data-stu-id="91744-112">With Role-Based Access Control (RBAC), you can assign users tooroles at three different levels of scope:</span></span>

* <span data-ttu-id="91744-113">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91744-113">subscription</span></span>
* <span data-ttu-id="91744-114">資源群組</span><span class="sxs-lookup"><span data-stu-id="91744-114">resource group</span></span>
* <span data-ttu-id="91744-115">resource</span><span class="sxs-lookup"><span data-stu-id="91744-115">resource</span></span>

<span data-ttu-id="91744-116">您指派的 hello 權限被繼承自 toohello 資源下的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="91744-116">hello permissions you assign are inherited from subscription down toohello resource.</span></span> <span data-ttu-id="91744-117">hello 已發行的儀表板是資源。</span><span class="sxs-lookup"><span data-stu-id="91744-117">hello published dashboard is a resource.</span></span> <span data-ttu-id="91744-118">因此，您可能已經有 hello 訂用帳戶的使用者指派 tooroles 這也適用於 hello 已發行的儀表板。</span><span class="sxs-lookup"><span data-stu-id="91744-118">Therefore, you may already have users assigned tooroles for hello subscription which also work for hello published dashboard.</span></span> 

<span data-ttu-id="91744-119">範例如下。</span><span class="sxs-lookup"><span data-stu-id="91744-119">Here is an example.</span></span>  <span data-ttu-id="91744-120">假設您有 Azure 訂用帳戶，並已指派不同的成員，您的小組 hello 角色**擁有者**，**參與者**，或**讀取器**hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="91744-120">Let's say you have an Azure subscription and various members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** for hello subscription.</span></span> <span data-ttu-id="91744-121">使用者是擁有者或參與者都可以 toolist，檢視、 建立、 修改或刪除儀表板 hello 訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="91744-121">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within hello subscription.</span></span>  <span data-ttu-id="91744-122">讀取器的使用者都能 toolist 和檢視儀表板，但無法修改或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="91744-122">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="91744-123">讀取器存取的使用者都能 toomake 本機編輯 tooa 發行儀表板 (例如，對問題進行疑難排解時)，但您不能 toopublish 這些變更後 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="91744-123">Users with reader access are able toomake local edits tooa published dashboard (such as, when troubleshooting an issue), but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="91744-124">將自己擁有 hello 選項 toomake hello 儀表板的私用複本</span><span class="sxs-lookup"><span data-stu-id="91744-124">They will have hello option toomake a private copy of hello dashboard for themselves</span></span>

<span data-ttu-id="91744-125">不過，您也可以指派包含數個儀表板或 tooan 個別儀表板的權限 toohello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="91744-125">However, you could also assign permissions toohello resource group that contains several dashboards or tooan individual dashboard.</span></span> <span data-ttu-id="91744-126">例如，您可能會決定，一群使用者應具有有限的權限跨 hello 訂用帳戶，但大於存取 tooa 特定儀表板。</span><span class="sxs-lookup"><span data-stu-id="91744-126">For example, you may decide that a group of users should have limited permissions across hello subscription but greater access tooa particular dashboard.</span></span> <span data-ttu-id="91744-127">您指派這些使用者 tooa 角色，該儀表板。</span><span class="sxs-lookup"><span data-stu-id="91744-127">You assign those users tooa role for that dashboard.</span></span> 

## <a name="publish-dashboard"></a><span data-ttu-id="91744-128">發佈儀表板</span><span class="sxs-lookup"><span data-stu-id="91744-128">Publish dashboard</span></span>
<span data-ttu-id="91744-129">讓我們假設您已完成設定您想 tooshare 要與使用者群組之前，您的訂用帳戶中的儀表板。</span><span class="sxs-lookup"><span data-stu-id="91744-129">Let's suppose you have finished configuring a dashboard that you want tooshare with a group of users in your subscription.</span></span> <span data-ttu-id="91744-130">hello 步驟描繪一個稱為 「 存放裝置管理員的自訂的群組，但您可以命名您的群組您想要的任何內容。</span><span class="sxs-lookup"><span data-stu-id="91744-130">hello steps below depict a customized group called Storage Managers, but you can name your group whatever you would like.</span></span> <span data-ttu-id="91744-131">如需建立 Active Directory 群組並加入使用者 toothat 群組資訊，請參閱[管理 Azure Active Directory 中的群組](../active-directory/active-directory-accessmanagement-manage-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="91744-131">For information about creating an Active Directory group and adding users toothat group, see [Managing groups in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).</span></span>

1. <span data-ttu-id="91744-132">在 hello 儀表板中，選取 **共用**。</span><span class="sxs-lookup"><span data-stu-id="91744-132">In hello dashboard, select **Share**.</span></span>
   
     ![選取共用](./media/azure-portal-dashboard-share-access/select-share.png)
2. <span data-ttu-id="91744-134">再指派存取權，您必須發佈 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="91744-134">Before assigning access, you must publish hello dashboard.</span></span> <span data-ttu-id="91744-135">根據預設，hello 儀表板將會發行的 tooa 資源群組名稱**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="91744-135">By default, hello dashboard will be published tooa resource group named **dashboards**.</span></span> <span data-ttu-id="91744-136">選取 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="91744-136">Select **Publish**.</span></span>
   
     ![publish](./media/azure-portal-dashboard-share-access/publish.png)

<span data-ttu-id="91744-138">儀表板現已發佈。</span><span class="sxs-lookup"><span data-stu-id="91744-138">Your dashboard is now published.</span></span> <span data-ttu-id="91744-139">如果適合 hello 繼承自 hello 訂用帳戶的權限，您不需要 toodo 任何資料。</span><span class="sxs-lookup"><span data-stu-id="91744-139">If hello permissions inherited from hello subscription are suitable, you do not need toodo anything more.</span></span> <span data-ttu-id="91744-140">您組織中的其他使用者將會無法 tooaccess 並修改其訂用帳戶層級的角色為基礎的 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="91744-140">Other users in your organization will be able tooaccess and modify hello dashboard based on their subscription level role.</span></span> <span data-ttu-id="91744-141">不過，本教學課程，讓我們指定使用者 tooa 角色，該儀表板的群組。</span><span class="sxs-lookup"><span data-stu-id="91744-141">However, for this tutorial, let's assign a group of users tooa role for that dashboard.</span></span>

## <a name="assign-access-tooa-dashboard"></a><span data-ttu-id="91744-142">指派存取 tooa 儀表板</span><span class="sxs-lookup"><span data-stu-id="91744-142">Assign access tooa dashboard</span></span>
1. <span data-ttu-id="91744-143">發行之後 hello 儀表板，選取**管理使用者**。</span><span class="sxs-lookup"><span data-stu-id="91744-143">After publishing hello dashboard, select **Manage users**.</span></span>
   
     ![管理使用者](./media/azure-portal-dashboard-share-access/manage-users.png)
2. <span data-ttu-id="91744-145">您會看到已對其指派此儀表板角色的現有使用者清單。</span><span class="sxs-lookup"><span data-stu-id="91744-145">You will see a list of existing users that are already assigned a role for this dashboard.</span></span> <span data-ttu-id="91744-146">您的現有使用者清單會不同於下面的 hello 影像。</span><span class="sxs-lookup"><span data-stu-id="91744-146">Your list of existing users will be different than hello image below.</span></span> <span data-ttu-id="91744-147">最可能的原因 hello 分派被繼承自 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="91744-147">Most likely, hello assignments are inherited from hello subscription.</span></span> <span data-ttu-id="91744-148">tooadd 新的使用者或群組，請選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="91744-148">tooadd a new user or group, select **Add**.</span></span>
   
     ![新增使用者](./media/azure-portal-dashboard-share-access/existing-users.png)
3. <span data-ttu-id="91744-150">選取代表您想要 toogrant hello 權限的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="91744-150">Select hello role that represents hello permissions you would like toogrant.</span></span> <span data-ttu-id="91744-151">在此範例中，請選取 [參與者] 。</span><span class="sxs-lookup"><span data-stu-id="91744-151">For this example, select **Contributor**.</span></span>
   
     ![選取角色](./media/azure-portal-dashboard-share-access/select-role.png)
4. <span data-ttu-id="91744-153">選取 hello 使用者或群組，您會希望 tooassign toohello 角色。</span><span class="sxs-lookup"><span data-stu-id="91744-153">Select hello user or group that you wish tooassign toohello role.</span></span> <span data-ttu-id="91744-154">如果您看不 hello 使用者或群組，您要尋找 hello 清單中，使用 hello [搜尋] 方塊。</span><span class="sxs-lookup"><span data-stu-id="91744-154">If you do not see hello user or group you are looking for in hello list, use hello search box.</span></span> <span data-ttu-id="91744-155">您可以使用群組的清單取決於您建立 Active Directory 中的 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="91744-155">Your list of available groups will depend on hello groups you have created in your Active Directory.</span></span>
   
     ![選取使用者](./media/azure-portal-dashboard-share-access/select-user.png) 
5. <span data-ttu-id="91744-157">使用者或群組新增完成時，請選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="91744-157">When you have finished adding users or groups, select **OK**.</span></span> 
6. <span data-ttu-id="91744-158">hello 新作業加入 toohello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="91744-158">hello new assignment is added toohello list of users.</span></span> <span data-ttu-id="91744-159">請注意，其**存取權**會列為 [已指派] 而非 [已繼承]。</span><span class="sxs-lookup"><span data-stu-id="91744-159">Notice that its **Access** is listed as **Assigned** rather than **Inherited**.</span></span>
   
     ![指派的角色](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a><span data-ttu-id="91744-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91744-161">Next steps</span></span>
* <span data-ttu-id="91744-162">如需角色清單，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="91744-162">For a list of roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="91744-163">toolearn 關於管理資源，請參閱[透過入口網站管理 Azure 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="91744-163">toolearn about managing resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

