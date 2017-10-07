---
title: "在 Azure 入口網站 hello aaaRole 型存取控制 |Microsoft 文件"
description: "快速入門中存取管理 hello Azure 入口網站中的 角色型存取控制。 使用角色指派 tooassign 權限 tooyour 資源。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="6c8a6-104">使用角色型存取控制 toomanage 存取 tooyour Azure 訂用帳戶資源</span><span class="sxs-lookup"><span data-stu-id="6c8a6-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c8a6-105">使用者或群組管理存取</span><span class="sxs-lookup"><span data-stu-id="6c8a6-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="6c8a6-106">資源管理存取</span><span class="sxs-lookup"><span data-stu-id="6c8a6-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="6c8a6-107">Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="6c8a6-108">使用 RBAC 時，您可以授與只 hello 少量的存取權，使用者需要 tooperform 他們的工作。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="6c8a6-109">這篇文章可協助您立即執行 RBAC 與 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="6c8a6-110">如果您需要有關 RBAC 如何協助您管理存取權的詳細資訊，請參閱 [什麼是角色型存取控制](role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="6c8a6-111">在每個訂用帳戶，您可以授與向上 too2000 角色指派。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="6c8a6-112">檢視存取權</span><span class="sxs-lookup"><span data-stu-id="6c8a6-112">View access</span></span>
<span data-ttu-id="6c8a6-113">您可以查看誰存取 tooa 資源、 資源群組或從其主要刀鋒視窗的訂用帳戶中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6c8a6-114">例如，我們想要擁有我們的資源群組的存取 tooone toosee:</span><span class="sxs-lookup"><span data-stu-id="6c8a6-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="6c8a6-115">選取**資源群組**hello hello 左側的導覽列中。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="6c8a6-116">![資源群組 - 圖示](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="6c8a6-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="6c8a6-117">選取 hello hello hello 資源群組名稱**資源群組**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="6c8a6-118">選取**存取控制 (IAM)** hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="6c8a6-119">hello 存取控制刀鋒視窗會列出所有使用者、 群組和已被授與存取 toohello 資源群組的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![使用者刀鋒視窗 - 繼承的存取權和指派的存取權螢幕擷取畫面](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="6c8a6-121">請注意，某些角色的範圍太**此資源**有些則是**繼承**從另一個範圍內。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="6c8a6-122">存取指派特別 toohello 資源群組，或繼承自指派 toohello 父訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6c8a6-123">Hello 新 RBAC 模型中，以傳統訂用帳戶系統管理員和共同管理員會視為 hello 訂用帳戶的擁有者。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="6c8a6-124">新增存取權</span><span class="sxs-lookup"><span data-stu-id="6c8a6-124">Add Access</span></span>
<span data-ttu-id="6c8a6-125">您授與從 hello 資源、 資源群組或訂用帳戶 hello hello 角色指派範圍內。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="6c8a6-126">選取**新增**hello 存取控制 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="6c8a6-127">您想從 hello tooassign 選取 hello 角色**選取角色**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="6c8a6-128">選取您想 toogrant 存取您目錄中的 hello 使用者、 群組或應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="6c8a6-129">您可以搜尋顯示名稱、 電子郵件地址與物件識別碼 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![新增使用者刀鋒視窗 - 搜尋螢幕擷取畫面](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="6c8a6-131">選取**確定**toocreate hello 分派。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="6c8a6-132">hello**加入使用者**快顯視窗會追蹤 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="6c8a6-133">![新增使用者進度列 - 螢幕擷取畫面](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="6c8a6-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="6c8a6-134">已成功加入之後的角色指派，它會出現在 hello**使用者**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="6c8a6-135">移除存取權</span><span class="sxs-lookup"><span data-stu-id="6c8a6-135">Remove Access</span></span>
1. <span data-ttu-id="6c8a6-136">將游標停留 hello 分派的 tooremove hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="6c8a6-137">核取方塊會顯示下一個 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="6c8a6-138">使用 hello 核取方塊 tooselect 一或多個角色指派。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="6c8a6-139">選取 [移除]。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="6c8a6-140">選取**是**tooconfirm hello 移除。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="6c8a6-141">無法移除已繼承的指派。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="6c8a6-142">如果您需要 tooremove 繼承的指派，您會需要的 toodo 在 hello hello 角色指派建立所在的範圍。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="6c8a6-143">在 [hello**範圍**資料行中下, 一步] 太**繼承**會帶您 toohello 資源已在指派給這個角色的連結。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="6c8a6-144">請列於該處 toohello 資源移 tooremove hello 角色指派。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![使用者刀鋒視窗 - 繼承的存取存停用 [移除] 按鈕螢幕擷取畫面](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="6c8a6-146">其他工具 toomanage 存取</span><span class="sxs-lookup"><span data-stu-id="6c8a6-146">Other tools toomanage access</span></span>
<span data-ttu-id="6c8a6-147">您可以將角色指派和使用 Azure rbac 進行命令，在 hello Azure 入口網站以外的工具管理存取權。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="6c8a6-148">遵循 hello 連結 toolearn 更多關於 hello 必要條件，並開始使用 hello Azure rbac 進行命令。</span><span class="sxs-lookup"><span data-stu-id="6c8a6-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="6c8a6-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c8a6-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="6c8a6-150">Azure 命令列介面</span><span class="sxs-lookup"><span data-stu-id="6c8a6-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="6c8a6-151">REST API</span><span class="sxs-lookup"><span data-stu-id="6c8a6-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="6c8a6-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c8a6-152">Next Steps</span></span>
* [<span data-ttu-id="6c8a6-153">建立存取權變更歷程記錄報告</span><span class="sxs-lookup"><span data-stu-id="6c8a6-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="6c8a6-154">請參閱 hello [RBAC 內建的角色](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="6c8a6-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="6c8a6-155">定義您自己的 [Azure RBAC 中的自訂角色](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="6c8a6-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

