---
title: "使用 RBAC 共用 Azure 入口網站儀表板 | Microsoft Docs"
description: "本文說明如何在 Azure 入口網站中使用角色型存取控制來共用儀表板。"
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
ms.openlocfilehash: ea0cf7ad074f95c2b49a92f9a8e32270a1d39b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a><span data-ttu-id="6ed2a-103">使用角色型存取控制來共用 Azure 儀表板</span><span class="sxs-lookup"><span data-stu-id="6ed2a-103">Share Azure dashboards by using Role-Based Access Control</span></span>
<span data-ttu-id="6ed2a-104">設定儀表板之後，您可以將它發佈，並與組織中的其他使用者共用。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-104">After configuring a dashboard, you can publish it and share it with other users in your organization.</span></span> <span data-ttu-id="6ed2a-105">使用 Azure [角色型存取控制](../active-directory/role-based-access-control-configure.md)，您可允許其他人檢視您的儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-105">You allow others to view your dashboard by using Azure [Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="6ed2a-106">您可以將一名使用者或一群使用者指派給某個角色，該角色就會定義這些使用者可以檢視或修改已發佈的儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-106">You assign a user or group of users to a role, and that role defines whether those users can view or modify the published dashboard.</span></span> 

<span data-ttu-id="6ed2a-107">所有已發佈的儀表板會實作為 Azure 資源，這表示它們是做為您訂用帳戶內可管理的項目而存在，並且會包含在資源群組中。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-107">All published dashboards are implemented as Azure resources, which means they exist as manageable items within your subscription and are contained in a resource group.</span></span>  <span data-ttu-id="6ed2a-108">從存取控制的觀點來看，儀表板與其他資源 (例如虛擬機器或儲存體帳戶) 並無不同。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-108">From an access control perspective, dashboards are no different than other resources, such as a virtual machine or a storage account.</span></span>

> [!TIP]
> <span data-ttu-id="6ed2a-109">儀表板上的個別圖格會根據其顯示的資源，強制執行自己的存取控制需求。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-109">Individual tiles on the dashboard enforce their own access control requirements based on the resources they display.</span></span>  <span data-ttu-id="6ed2a-110">因此，您可以設計一個廣泛共用且同時仍會保護個別圖格上資料的儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-110">Therefore, you can design a dashboard that is shared broadly while still protecting the data on individual tiles.</span></span>
> 
> 

## <a name="understanding-access-control-for-dashboards"></a><span data-ttu-id="6ed2a-111">了解儀表板的存取控制</span><span class="sxs-lookup"><span data-stu-id="6ed2a-111">Understanding access control for dashboards</span></span>
<span data-ttu-id="6ed2a-112">若使用角色型存取控制 (RBAC)，您可以將使用者指派給三個不同範圍層級的角色︰</span><span class="sxs-lookup"><span data-stu-id="6ed2a-112">With Role-Based Access Control (RBAC), you can assign users to roles at three different levels of scope:</span></span>

* <span data-ttu-id="6ed2a-113">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6ed2a-113">subscription</span></span>
* <span data-ttu-id="6ed2a-114">資源群組</span><span class="sxs-lookup"><span data-stu-id="6ed2a-114">resource group</span></span>
* <span data-ttu-id="6ed2a-115">資源</span><span class="sxs-lookup"><span data-stu-id="6ed2a-115">resource</span></span>

<span data-ttu-id="6ed2a-116">您指派的權限會從訂用帳戶往下繼承到資源。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-116">The permissions you assign are inherited from subscription down to the resource.</span></span> <span data-ttu-id="6ed2a-117">發佈的儀表板是一種資源。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-117">The published dashboard is a resource.</span></span> <span data-ttu-id="6ed2a-118">因此，您可能已將使用者指派給訂用帳戶的角色，而這也對已發佈的儀表板有效。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-118">Therefore, you may already have users assigned to roles for the subscription which also work for the published dashboard.</span></span> 

<span data-ttu-id="6ed2a-119">範例如下。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-119">Here is an example.</span></span>  <span data-ttu-id="6ed2a-120">假設您有 Azure 訂用帳戶，而且已為小組各種成員指派訂用帳戶的**擁有者**、**參與者**或**讀取者**角色。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-120">Let's say you have an Azure subscription and various members of your team have been assigned the roles of **owner**, **contributor**, or **reader** for the subscription.</span></span> <span data-ttu-id="6ed2a-121">身為擁有者或參與者的使用者能夠列出、檢視、建立、修改或刪除訂用帳戶內的儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-121">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within the subscription.</span></span>  <span data-ttu-id="6ed2a-122">身為讀取者的使用者能夠列出和檢視儀表板，但無法進行修改或刪除。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-122">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="6ed2a-123">具有讀取者存取權的使用者能夠對已發佈的儀表板進行本機編輯 (例如在針對問題進行疑難排解時)，但無法將這些變更發佈回伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-123">Users with reader access are able to make local edits to a published dashboard (such as, when troubleshooting an issue), but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="6ed2a-124">他們會有為自己製作儀表板的私人複本的選項。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-124">They will have the option to make a private copy of the dashboard for themselves</span></span>

<span data-ttu-id="6ed2a-125">不過，您也可以指派權限給包含數個儀表板的資源群組或指派給個別儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-125">However, you could also assign permissions to the resource group that contains several dashboards or to an individual dashboard.</span></span> <span data-ttu-id="6ed2a-126">例如，您可能會決定，一群使用者應具有有限的訂用帳戶權限，但對特定儀表板則具有更大範圍的存取權。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-126">For example, you may decide that a group of users should have limited permissions across the subscription but greater access to a particular dashboard.</span></span> <span data-ttu-id="6ed2a-127">您可以將這些使用者指派給該儀表板的角色。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-127">You assign those users to a role for that dashboard.</span></span> 

## <a name="publish-dashboard"></a><span data-ttu-id="6ed2a-128">發佈儀表板</span><span class="sxs-lookup"><span data-stu-id="6ed2a-128">Publish dashboard</span></span>
<span data-ttu-id="6ed2a-129">讓我們假設您已完成設定想要與訂用帳戶中的一群使用者共用的儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-129">Let's suppose you have finished configuring a dashboard that you want to share with a group of users in your subscription.</span></span> <span data-ttu-id="6ed2a-130">下列步驟描述稱為「儲存體管理員」的自訂群組，但您可以將您的群組命名為任何您喜歡的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-130">The steps below depict a customized group called Storage Managers, but you can name your group whatever you would like.</span></span> <span data-ttu-id="6ed2a-131">如需建立 Active Directory 群組和將使用者新增至該群組的相關資訊，請參閱 [在 Azure Active Directory 中管理群組](../active-directory/active-directory-accessmanagement-manage-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-131">For information about creating an Active Directory group and adding users to that group, see [Managing groups in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).</span></span>

1. <span data-ttu-id="6ed2a-132">在儀表板中選取 [共用] 。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-132">In the dashboard, select **Share**.</span></span>
   
     ![選取共用](./media/azure-portal-dashboard-share-access/select-share.png)
2. <span data-ttu-id="6ed2a-134">在指派存取權之前，您必須先發佈儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-134">Before assigning access, you must publish the dashboard.</span></span> <span data-ttu-id="6ed2a-135">根據預設，儀表板會發佈到名為 **儀表板**的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-135">By default, the dashboard will be published to a resource group named **dashboards**.</span></span> <span data-ttu-id="6ed2a-136">選取 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-136">Select **Publish**.</span></span>
   
     ![publish](./media/azure-portal-dashboard-share-access/publish.png)

<span data-ttu-id="6ed2a-138">儀表板現已發佈。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-138">Your dashboard is now published.</span></span> <span data-ttu-id="6ed2a-139">如果繼承自訂用帳戶的權限合適，則不需要再執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-139">If the permissions inherited from the subscription are suitable, you do not need to do anything more.</span></span> <span data-ttu-id="6ed2a-140">組織中的其他使用者將可以根據其訂用帳戶層級的角色來存取和修改儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-140">Other users in your organization will be able to access and modify the dashboard based on their subscription level role.</span></span> <span data-ttu-id="6ed2a-141">不過，在本教學課程中，讓我們將一群使用者指派給該儀表板的角色。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-141">However, for this tutorial, let's assign a group of users to a role for that dashboard.</span></span>

## <a name="assign-access-to-a-dashboard"></a><span data-ttu-id="6ed2a-142">指派儀表板存取權</span><span class="sxs-lookup"><span data-stu-id="6ed2a-142">Assign access to a dashboard</span></span>
1. <span data-ttu-id="6ed2a-143">在發佈儀表板之後，選取 [管理使用者] 。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-143">After publishing the dashboard, select **Manage users**.</span></span>
   
     ![管理使用者](./media/azure-portal-dashboard-share-access/manage-users.png)
2. <span data-ttu-id="6ed2a-145">您會看到已對其指派此儀表板角色的現有使用者清單。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-145">You will see a list of existing users that are already assigned a role for this dashboard.</span></span> <span data-ttu-id="6ed2a-146">您的現有使用者清單會不同於下面的影像。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-146">Your list of existing users will be different than the image below.</span></span> <span data-ttu-id="6ed2a-147">指派很可能是繼承自訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-147">Most likely, the assignments are inherited from the subscription.</span></span> <span data-ttu-id="6ed2a-148">若要新增使用者或群組，請選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-148">To add a new user or group, select **Add**.</span></span>
   
     ![新增使用者](./media/azure-portal-dashboard-share-access/existing-users.png)
3. <span data-ttu-id="6ed2a-150">選取代表您想要授與之權限的角色。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-150">Select the role that represents the permissions you would like to grant.</span></span> <span data-ttu-id="6ed2a-151">在此範例中，請選取 [參與者] 。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-151">For this example, select **Contributor**.</span></span>
   
     ![選取角色](./media/azure-portal-dashboard-share-access/select-role.png)
4. <span data-ttu-id="6ed2a-153">選取想要指派給角色的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-153">Select the user or group that you wish to assign to the role.</span></span> <span data-ttu-id="6ed2a-154">如果您在清單中沒有看見要尋找的使用者或群組，請使用搜尋方塊。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-154">If you do not see the user or group you are looking for in the list, use the search box.</span></span> <span data-ttu-id="6ed2a-155">您的可用群組清單取決於您已在 Active Directory 中建立的群組。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-155">Your list of available groups will depend on the groups you have created in your Active Directory.</span></span>
   
     ![選取使用者](./media/azure-portal-dashboard-share-access/select-user.png) 
5. <span data-ttu-id="6ed2a-157">使用者或群組新增完成時，請選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-157">When you have finished adding users or groups, select **OK**.</span></span> 
6. <span data-ttu-id="6ed2a-158">新的指派就會加入至使用者清單。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-158">The new assignment is added to the list of users.</span></span> <span data-ttu-id="6ed2a-159">請注意，其**存取權**會列為 [已指派] 而非 [已繼承]。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-159">Notice that its **Access** is listed as **Assigned** rather than **Inherited**.</span></span>
   
     ![指派的角色](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a><span data-ttu-id="6ed2a-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ed2a-161">Next steps</span></span>
* <span data-ttu-id="6ed2a-162">如需角色清單，請參閱 [RBAC︰內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-162">For a list of roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="6ed2a-163">若要了解如何管理資源，請參閱 [透過入口網站管理 Azure 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6ed2a-163">To learn about managing resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

