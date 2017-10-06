---
title: "aaaView Azure 資源存取設定 |Microsoft 文件"
description: "檢視及管理的任何使用者或群組 hello Azure 入口網站中的所有 hello 角色型存取控制指派"
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
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="f59a4-103">檢視存取工作分派 hello Azure 入口網站中的使用者及群組</span><span class="sxs-lookup"><span data-stu-id="f59a4-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f59a4-104">使用者或群組管理存取</span><span class="sxs-lookup"><span data-stu-id="f59a4-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="f59a4-105">資源管理存取</span><span class="sxs-lookup"><span data-stu-id="f59a4-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="f59a4-106">您可以使用角色型存取控制 (RBAC) hello Azure Active Directory (Azure AD) 中，管理存取 tooyour Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f59a4-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="f59a4-107">使用 RBAC 指派的存取是更細緻的因為有兩種方式，您可以限制 hello 權限：</span><span class="sxs-lookup"><span data-stu-id="f59a4-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="f59a4-108">**範圍：** RBAC 角色指派是已設定領域的 tooa 特定訂用帳戶、 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="f59a4-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="f59a4-109">指定存取 tooa 單一資源的使用者無法存取 hello 中的任何其他資源相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f59a4-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="f59a4-110">**角色：**存取縮小到 hello 在範圍內的 hello 分派，甚至進一步將角色指派。</span><span class="sxs-lookup"><span data-stu-id="f59a4-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="f59a4-111">角色可為高層級，例如擁有者或特定，例如虛擬機器讀取器。</span><span class="sxs-lookup"><span data-stu-id="f59a4-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="f59a4-112">只能從 hello 訂用帳戶、 資源群組或資源，是 hello 分派 hello 範圍內指派角色。</span><span class="sxs-lookup"><span data-stu-id="f59a4-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="f59a4-113">但是，您可以在單一位置來檢視指定的使用者或群組的所有 hello 存取指派。</span><span class="sxs-lookup"><span data-stu-id="f59a4-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="f59a4-114">您可以向上 too2000 每個訂用帳戶中的角色指派。</span><span class="sxs-lookup"><span data-stu-id="f59a4-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="f59a4-115">取得有關的詳細資訊太[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="f59a4-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="f59a4-116">檢視存取權指派</span><span class="sxs-lookup"><span data-stu-id="f59a4-116">View access assignments</span></span>
<span data-ttu-id="f59a4-117">toolook 向上 hello 存取指派單一使用者或群組，開始在 Azure Active Directory 中 hello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f59a4-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="f59a4-118">選取 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="f59a4-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="f59a4-119">如果此選項不是顯示在瀏覽清單上，選取**更服務**，然後捲動 toofind **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="f59a4-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="f59a4-120">選取 [使用者和群組]，然後選取 [所有使用者]或 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="f59a4-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="f59a4-121">在此範例中，我們將重點放在個別使用者。</span><span class="sxs-lookup"><span data-stu-id="f59a4-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="f59a4-122">![在 Azure Active Directory 中管理使用者和群組 - 螢幕擷取畫面](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="f59a4-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="f59a4-123">依名稱或使用者名稱搜尋 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="f59a4-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="f59a4-124">選取**Azure 資源**hello 使用者] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f59a4-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="f59a4-125">該使用者的所有 hello 存取指派會都出現。</span><span class="sxs-lookup"><span data-stu-id="f59a4-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="f59a4-126">Tooview 指派讀取權限</span><span class="sxs-lookup"><span data-stu-id="f59a4-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="f59a4-127">此頁面只會顯示 hello 存取指派您有權限 tooread。</span><span class="sxs-lookup"><span data-stu-id="f59a4-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="f59a4-128">比方說，您具有讀取權限 toosubscription A，並移 toohello Azure 資源刀鋒視窗 toocheck 使用者的指派。</span><span class="sxs-lookup"><span data-stu-id="f59a4-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="f59a4-129">您可以看到她的訂用帳戶 A 存取權指派，但無法看到她在訂用帳戶 B 上也擁有存取權指派。</span><span class="sxs-lookup"><span data-stu-id="f59a4-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="f59a4-130">刪除存取權指派</span><span class="sxs-lookup"><span data-stu-id="f59a4-130">Delete access assignments</span></span>
<span data-ttu-id="f59a4-131">從這個刀鋒視窗中，您可以刪除 tooa 使用者或群組直接指派的存取權指派。</span><span class="sxs-lookup"><span data-stu-id="f59a4-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="f59a4-132">如果 hello 存取指派繼承自父群組，您會需要 toogo toohello 資源或訂用帳戶和管理那里 hello 分派。</span><span class="sxs-lookup"><span data-stu-id="f59a4-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="f59a4-133">從 hello 的所有 hello 存取指派使用者或群組] 清單中，選取 hello 其中一個要 toodelete。</span><span class="sxs-lookup"><span data-stu-id="f59a4-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="f59a4-134">選取**移除**然後**是**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="f59a4-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="f59a4-135">![移除存取權指派 - 螢幕擷取畫面](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="f59a4-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f59a4-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f59a4-136">Next steps</span></span>

* <span data-ttu-id="f59a4-137">開始使用角色型存取控制中太[使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="f59a4-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="f59a4-138">請參閱 hello [RBAC 內建的角色](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="f59a4-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

