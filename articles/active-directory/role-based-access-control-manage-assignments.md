---
title: "檢視 Azure 資源存取權指派 | Microsoft Docs"
description: "檢視及管理 Azure 入口網站中任何使用者或群組的所有角色型存取控制指派"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: 72c695d08bdf5de003d51ffb0768184e1e4d00ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-the-azure-portal"></a><span data-ttu-id="96617-103">在 Azure 入口網站中檢視使用者和群組的存取指派</span><span class="sxs-lookup"><span data-stu-id="96617-103">View access assignments for users and groups in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96617-104">使用者或群組管理存取</span><span class="sxs-lookup"><span data-stu-id="96617-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="96617-105">資源管理存取</span><span class="sxs-lookup"><span data-stu-id="96617-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="96617-106">您可以使用 Azure Active Directory (Azure AD) 中的角色型存取控制 (RBAC) 來管理 Azure 資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="96617-106">With role-based access control (RBAC) in the Azure Active Directory (Azure AD), you can manage access to your Azure resources.</span></span> 

<span data-ttu-id="96617-107">使用 RBAC 指派的存取是精細的，因為有兩種方式可以限制權限︰</span><span class="sxs-lookup"><span data-stu-id="96617-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span></span>

* <span data-ttu-id="96617-108">**範圍︰** RBAC 角色指派範圍設定為特定的訂用帳戶、資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="96617-108">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span></span> <span data-ttu-id="96617-109">取得單一資源存取權的使用者無法在相同的訂用帳戶中存取任何其他資源。</span><span class="sxs-lookup"><span data-stu-id="96617-109">A user given access to a single resource cannot access any other resources in the same subscription.</span></span>
* <span data-ttu-id="96617-110">**角色︰** 在指派的範圍內，會指派角色以進一步縮小存取範圍。</span><span class="sxs-lookup"><span data-stu-id="96617-110">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="96617-111">角色可為高層級，例如擁有者或特定，例如虛擬機器讀取器。</span><span class="sxs-lookup"><span data-stu-id="96617-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="96617-112">只能從指派範圍內的訂用帳戶、資源群組或資源指派角色。</span><span class="sxs-lookup"><span data-stu-id="96617-112">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span></span> <span data-ttu-id="96617-113">但是，您可以在單一位置檢視指定使用者或群組的存取權指派。</span><span class="sxs-lookup"><span data-stu-id="96617-113">But you can view all the access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="96617-114">您在每個訂用帳戶中可以有最多 2000 個角色指派。</span><span class="sxs-lookup"><span data-stu-id="96617-114">You can have up to 2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="96617-115">取得 [使用角色指派來管理 Azure 訂用帳戶資源的存取權](role-based-access-control-configure.md)的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="96617-115">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="96617-116">檢視存取權指派</span><span class="sxs-lookup"><span data-stu-id="96617-116">View access assignments</span></span>
<span data-ttu-id="96617-117">若要尋找單一使用者或群組的存取權指派，請在 [Azure 入口網站](http://portal.azure.com)的 Azure Active Directory 中開始。</span><span class="sxs-lookup"><span data-stu-id="96617-117">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="96617-118">選取 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96617-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="96617-119">如果您的瀏覽清單上看不到這個選項，選取 [更多服務]，然後向下捲動以尋找 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="96617-119">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span></span>
2. <span data-ttu-id="96617-120">選取 [使用者和群組]，然後選取 [所有使用者]或 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="96617-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="96617-121">在此範例中，我們將重點放在個別使用者。</span><span class="sxs-lookup"><span data-stu-id="96617-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="96617-122">![在 Azure Active Directory 中管理使用者和群組 - 螢幕擷取畫面](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="96617-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="96617-123">依名稱或使用者名稱搜尋使用者。</span><span class="sxs-lookup"><span data-stu-id="96617-123">Search for the user by name or username.</span></span>
4. <span data-ttu-id="96617-124">在使用者刀鋒視窗上選取 [Azure 資源]  。</span><span class="sxs-lookup"><span data-stu-id="96617-124">Select **Azure resources** on the user blade.</span></span> <span data-ttu-id="96617-125">隨即出現該使用者的所有存取權指派。</span><span class="sxs-lookup"><span data-stu-id="96617-125">All the access assignments for that user appear.</span></span>

### <a name="read-permissions-to-view-assignments"></a><span data-ttu-id="96617-126">檢視指派的讀取權限</span><span class="sxs-lookup"><span data-stu-id="96617-126">Read permissions to view assignments</span></span>
<span data-ttu-id="96617-127">此頁面只會顯示您擁有讀取權限的存取權指派。</span><span class="sxs-lookup"><span data-stu-id="96617-127">This page only shows the access assignments that you have permission to read.</span></span> <span data-ttu-id="96617-128">例如，您擁有訂用帳戶 A 的讀取權限，並移至 Azure 資源刀鋒視窗檢查使用者的指派。</span><span class="sxs-lookup"><span data-stu-id="96617-128">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span></span> <span data-ttu-id="96617-129">您可以看到她的訂用帳戶 A 存取權指派，但無法看到她在訂用帳戶 B 上也擁有存取權指派。</span><span class="sxs-lookup"><span data-stu-id="96617-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="96617-130">刪除存取權指派</span><span class="sxs-lookup"><span data-stu-id="96617-130">Delete access assignments</span></span>
<span data-ttu-id="96617-131">從這個刀鋒視窗中，您可以刪除已直接指派給使用者或群組的存取權指派。</span><span class="sxs-lookup"><span data-stu-id="96617-131">From this blade, you can delete access assignments that were assigned directly to a user or group.</span></span> <span data-ttu-id="96617-132">如果從父群組繼承存取權指派，您需要移至資源或訂用帳戶，並在那裡管理指派。</span><span class="sxs-lookup"><span data-stu-id="96617-132">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span></span>

1. <span data-ttu-id="96617-133">從使用者或群組的所有存取權指派清單中，選取您想要刪除的項目。</span><span class="sxs-lookup"><span data-stu-id="96617-133">From the list of all the access assignments for a user or group, select the one you want to delete.</span></span>
2. <span data-ttu-id="96617-134">選取 [移除]然後選取 [是] 以確認。</span><span class="sxs-lookup"><span data-stu-id="96617-134">Select **Remove** and then **Yes** to confirm.</span></span>
    <span data-ttu-id="96617-135">![移除存取權指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="96617-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="96617-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96617-136">Next steps</span></span>

* <span data-ttu-id="96617-137">取得 [使用角色指派來管理 Azure 訂用帳戶資源的存取權](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="96617-137">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="96617-138">參閱 [RBAC 內建角色](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="96617-138">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

