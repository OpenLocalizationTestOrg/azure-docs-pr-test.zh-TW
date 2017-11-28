---
title: "aaaAdd 擁有者和使用者在 Azure DevTest Labs |Microsoft 文件"
description: "在 Azure DevTest Labs 使用 hello Azure 入口網站或 PowerShell 加入擁有者和使用者"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="9db72-103">在 Azure DevTest Labs 中新增擁有者和使用者</span><span class="sxs-lookup"><span data-stu-id="9db72-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="9db72-104">Azure DevTest Labs 的存取權是由 [Azure 角色型存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md)所控制。</span><span class="sxs-lookup"><span data-stu-id="9db72-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="9db72-105">使用 RBAC 時，您可以分隔責任至您小組內*角色*您授與只能存取必要 toousers tooperform hello 量他們的工作。</span><span class="sxs-lookup"><span data-stu-id="9db72-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="9db72-106">這些 RBAC 角色的其中三個分別是*擁有者*、*DevTest Labs 使用者*和*參與者*。</span><span class="sxs-lookup"><span data-stu-id="9db72-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="9db72-107">在本文中，您學會中每個 hello 三個主要 RBAC 角色可以執行的動作。</span><span class="sxs-lookup"><span data-stu-id="9db72-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="9db72-108">您了解從該處，同時透過 hello tooadd 使用者 tooa 實驗室-如何入口網站與透過 PowerShell 指令碼，和如何 tooadd 使用者在 hello 訂用帳戶層級。</span><span class="sxs-lookup"><span data-stu-id="9db72-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="9db72-109">可在每個角色執行的動作</span><span class="sxs-lookup"><span data-stu-id="9db72-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="9db72-110">您可以對使用者指派三個主要角色︰</span><span class="sxs-lookup"><span data-stu-id="9db72-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="9db72-111">擁有者</span><span class="sxs-lookup"><span data-stu-id="9db72-111">Owner</span></span>
* <span data-ttu-id="9db72-112">DevTest Labs 使用者</span><span class="sxs-lookup"><span data-stu-id="9db72-112">DevTest Labs User</span></span>
* <span data-ttu-id="9db72-113">參與者</span><span class="sxs-lookup"><span data-stu-id="9db72-113">Contributor</span></span>

<span data-ttu-id="9db72-114">hello 下表說明每個角色中的使用者可以執行的 hello 動作：</span><span class="sxs-lookup"><span data-stu-id="9db72-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="9db72-115">**此角色中的使用者可以執行的動作**</span><span class="sxs-lookup"><span data-stu-id="9db72-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="9db72-116">**DevTest Labs 使用者**</span><span class="sxs-lookup"><span data-stu-id="9db72-116">**DevTest Labs User**</span></span> | <span data-ttu-id="9db72-117">**擁有者**</span><span class="sxs-lookup"><span data-stu-id="9db72-117">**Owner**</span></span> | <span data-ttu-id="9db72-118">**參與者**</span><span class="sxs-lookup"><span data-stu-id="9db72-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9db72-119">**實驗室工作**</span><span class="sxs-lookup"><span data-stu-id="9db72-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="9db72-120">加入使用者 tooa 實驗室</span><span class="sxs-lookup"><span data-stu-id="9db72-120">Add users tooa lab</span></span> |<span data-ttu-id="9db72-121">否</span><span class="sxs-lookup"><span data-stu-id="9db72-121">No</span></span> |<span data-ttu-id="9db72-122">是</span><span class="sxs-lookup"><span data-stu-id="9db72-122">Yes</span></span> |<span data-ttu-id="9db72-123">否</span><span class="sxs-lookup"><span data-stu-id="9db72-123">No</span></span> |
| <span data-ttu-id="9db72-124">更新成本設定</span><span class="sxs-lookup"><span data-stu-id="9db72-124">Update cost settings</span></span> |<span data-ttu-id="9db72-125">否</span><span class="sxs-lookup"><span data-stu-id="9db72-125">No</span></span> |<span data-ttu-id="9db72-126">是</span><span class="sxs-lookup"><span data-stu-id="9db72-126">Yes</span></span> |<span data-ttu-id="9db72-127">是</span><span class="sxs-lookup"><span data-stu-id="9db72-127">Yes</span></span> |
| <span data-ttu-id="9db72-128">**VM 的基本工作**</span><span class="sxs-lookup"><span data-stu-id="9db72-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="9db72-129">新增和移除自訂映像</span><span class="sxs-lookup"><span data-stu-id="9db72-129">Add and remove custom images</span></span> |<span data-ttu-id="9db72-130">否</span><span class="sxs-lookup"><span data-stu-id="9db72-130">No</span></span> |<span data-ttu-id="9db72-131">是</span><span class="sxs-lookup"><span data-stu-id="9db72-131">Yes</span></span> |<span data-ttu-id="9db72-132">是</span><span class="sxs-lookup"><span data-stu-id="9db72-132">Yes</span></span> |
| <span data-ttu-id="9db72-133">新增、更新和刪除公式</span><span class="sxs-lookup"><span data-stu-id="9db72-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="9db72-134">是</span><span class="sxs-lookup"><span data-stu-id="9db72-134">Yes</span></span> |<span data-ttu-id="9db72-135">是</span><span class="sxs-lookup"><span data-stu-id="9db72-135">Yes</span></span> |<span data-ttu-id="9db72-136">是</span><span class="sxs-lookup"><span data-stu-id="9db72-136">Yes</span></span> |
| <span data-ttu-id="9db72-137">將 Azure Marketplace 映像加入白名單</span><span class="sxs-lookup"><span data-stu-id="9db72-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="9db72-138">否</span><span class="sxs-lookup"><span data-stu-id="9db72-138">No</span></span> |<span data-ttu-id="9db72-139">是</span><span class="sxs-lookup"><span data-stu-id="9db72-139">Yes</span></span> |<span data-ttu-id="9db72-140">是</span><span class="sxs-lookup"><span data-stu-id="9db72-140">Yes</span></span> |
| <span data-ttu-id="9db72-141">**VM 工作**</span><span class="sxs-lookup"><span data-stu-id="9db72-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="9db72-142">建立 VM</span><span class="sxs-lookup"><span data-stu-id="9db72-142">Create VMs</span></span> |<span data-ttu-id="9db72-143">是</span><span class="sxs-lookup"><span data-stu-id="9db72-143">Yes</span></span> |<span data-ttu-id="9db72-144">是</span><span class="sxs-lookup"><span data-stu-id="9db72-144">Yes</span></span> |<span data-ttu-id="9db72-145">是</span><span class="sxs-lookup"><span data-stu-id="9db72-145">Yes</span></span> |
| <span data-ttu-id="9db72-146">啟動、停止和刪除 VM</span><span class="sxs-lookup"><span data-stu-id="9db72-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="9db72-147">Hello 使用者所建立的 Vm</span><span class="sxs-lookup"><span data-stu-id="9db72-147">Only VMs created by hello user</span></span> |<span data-ttu-id="9db72-148">是</span><span class="sxs-lookup"><span data-stu-id="9db72-148">Yes</span></span> |<span data-ttu-id="9db72-149">是</span><span class="sxs-lookup"><span data-stu-id="9db72-149">Yes</span></span> |
| <span data-ttu-id="9db72-150">更新 VM 原則</span><span class="sxs-lookup"><span data-stu-id="9db72-150">Update VM policies</span></span> |<span data-ttu-id="9db72-151">否</span><span class="sxs-lookup"><span data-stu-id="9db72-151">No</span></span> |<span data-ttu-id="9db72-152">是</span><span class="sxs-lookup"><span data-stu-id="9db72-152">Yes</span></span> |<span data-ttu-id="9db72-153">是</span><span class="sxs-lookup"><span data-stu-id="9db72-153">Yes</span></span> |
| <span data-ttu-id="9db72-154">在 VM 中新增/移除資料磁碟</span><span class="sxs-lookup"><span data-stu-id="9db72-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="9db72-155">Hello 使用者所建立的 Vm</span><span class="sxs-lookup"><span data-stu-id="9db72-155">Only VMs created by hello user</span></span> |<span data-ttu-id="9db72-156">是</span><span class="sxs-lookup"><span data-stu-id="9db72-156">Yes</span></span> |<span data-ttu-id="9db72-157">是</span><span class="sxs-lookup"><span data-stu-id="9db72-157">Yes</span></span> |
| <span data-ttu-id="9db72-158">**構件工作**</span><span class="sxs-lookup"><span data-stu-id="9db72-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="9db72-159">新增和移除構件儲存機制</span><span class="sxs-lookup"><span data-stu-id="9db72-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="9db72-160">否</span><span class="sxs-lookup"><span data-stu-id="9db72-160">No</span></span> |<span data-ttu-id="9db72-161">是</span><span class="sxs-lookup"><span data-stu-id="9db72-161">Yes</span></span> |<span data-ttu-id="9db72-162">是</span><span class="sxs-lookup"><span data-stu-id="9db72-162">Yes</span></span> |
| <span data-ttu-id="9db72-163">套用構件</span><span class="sxs-lookup"><span data-stu-id="9db72-163">Apply artifacts</span></span> |<span data-ttu-id="9db72-164">是</span><span class="sxs-lookup"><span data-stu-id="9db72-164">Yes</span></span> |<span data-ttu-id="9db72-165">是</span><span class="sxs-lookup"><span data-stu-id="9db72-165">Yes</span></span> |<span data-ttu-id="9db72-166">是</span><span class="sxs-lookup"><span data-stu-id="9db72-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="9db72-167">當使用者建立的 VM 時，該使用者會自動指派 toohello**擁有者**hello 建立 VM 角色。</span><span class="sxs-lookup"><span data-stu-id="9db72-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="9db72-168">在 hello 實驗室層級加入擁有者或使用者</span><span class="sxs-lookup"><span data-stu-id="9db72-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="9db72-169">擁有者和使用者可以加入層級 hello 實驗室透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9db72-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="9db72-170">這包括擁有有效 [Microsoft 帳戶 (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)的外部使用者。</span><span class="sxs-lookup"><span data-stu-id="9db72-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="9db72-171">hello 步驟會引導您加入的擁有者或使用者 tooa 實驗室中 Azure DevTest Labs hello 程序：</span><span class="sxs-lookup"><span data-stu-id="9db72-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="9db72-172">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="9db72-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="9db72-173">選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="9db72-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="9db72-174">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="9db72-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="9db72-175">在 hello 實驗室刀鋒視窗中，選取 **組態**。</span><span class="sxs-lookup"><span data-stu-id="9db72-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="9db72-176">在 hello**組態**刀鋒視窗中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="9db72-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="9db72-177">在 hello**使用者**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="9db72-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![新增使用者](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="9db72-179">在 hello**選取角色**刀鋒視窗中，選取 hello 所需的角色。</span><span class="sxs-lookup"><span data-stu-id="9db72-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="9db72-180">hello 區段[可在每個角色執行的動作](#actions-that-can-be-performed-in-each-role)清單 hello hello 擁有者、 DevTest 使用者和參與者角色中的可執行各種動作。</span><span class="sxs-lookup"><span data-stu-id="9db72-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="9db72-181">在 hello**將使用者新增**刀鋒視窗中，輸入 hello 電子郵件地址或您想要在您指定的 hello 角色 tooadd hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="9db72-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="9db72-182">如果找不到 hello 使用者，錯誤訊息，說明 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="9db72-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="9db72-183">如果找到 hello 使用者，則會列出該使用者，並選取。</span><span class="sxs-lookup"><span data-stu-id="9db72-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="9db72-184">選取 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="9db72-184">Select **Select**.</span></span>
10. <span data-ttu-id="9db72-185">選取**確定**tooclose hello**新增存取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9db72-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="9db72-186">當您傳回 toohello**使用者**刀鋒視窗中，已新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="9db72-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="9db72-187">新增外部使用者 tooa 實驗室使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="9db72-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="9db72-188">此外 tooadding hello Azure 入口網站中的使用者，您可以新增要使用 PowerShell 指令碼的外部使用者 tooyour 實驗室。</span><span class="sxs-lookup"><span data-stu-id="9db72-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="9db72-189">在 hello 遵循範例中，只需修改 hello 參數值在 hello**值 toochange**註解。</span><span class="sxs-lookup"><span data-stu-id="9db72-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="9db72-190">您可以擷取 hello `subscriptionId`， `labResourceGroup`，和`labName`hello Azure 入口網站中的 hello 實驗室刀鋒視窗中的值。</span><span class="sxs-lookup"><span data-stu-id="9db72-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="9db72-191">hello 範例指令碼會假設該 hello 指定的使用者都已經加入成為客體 toohello Active Directory，和如果不是 hello 案例將會失敗。</span><span class="sxs-lookup"><span data-stu-id="9db72-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="9db72-192">tooadd 使用者不在 hello Active Directory tooa 實驗室中，使用 hello Azure 入口網站 tooassign hello 使用者 tooa 角色 hello 區段中所示[hello 實驗室層級加入擁有者或使用者](#add-an-owner-or-user-at-the-lab-level)。</span><span class="sxs-lookup"><span data-stu-id="9db72-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="9db72-193">在 hello 訂用帳戶層級加入擁有者或使用者</span><span class="sxs-lookup"><span data-stu-id="9db72-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="9db72-194">在 Azure 中的父範圍 toochild 範圍從傳播 azure 權限。</span><span class="sxs-lookup"><span data-stu-id="9db72-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="9db72-195">因此，包含實驗室之 Azure 訂用帳戶的擁有者會自動成為這些實驗室的擁有者。</span><span class="sxs-lookup"><span data-stu-id="9db72-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="9db72-196">他們也擁有 hello Vm 和 hello 實驗室的使用者和 hello Azure DevTest Labs 服務所建立的其他資源。</span><span class="sxs-lookup"><span data-stu-id="9db72-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="9db72-197">您可以加入其他擁有者 tooa 實驗室透過 hello 實驗室刀鋒視窗中 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="9db72-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="9db72-198">不過，hello 加入擁有者的系統管理範圍是較窄比 hello 訂用帳戶擁有者的範圍。</span><span class="sxs-lookup"><span data-stu-id="9db72-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="9db72-199">例如，hello 加入擁有者不需要完整存取 toosome 的 hello 資源建立 hello 訂用帳戶中的 hello DevTest Labs 服務。</span><span class="sxs-lookup"><span data-stu-id="9db72-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="9db72-200">tooadd 擁有者 tooan Azure 訂用帳戶，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9db72-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="9db72-201">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="9db72-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="9db72-202">選取**更服務**，然後選取**訂閱**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="9db72-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="9db72-203">選取所需的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9db72-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="9db72-204">選取 [存取]  圖示。</span><span class="sxs-lookup"><span data-stu-id="9db72-204">Select **Access** icon.</span></span> 
   
    ![存取使用者](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="9db72-206">在 hello**使用者**刀鋒視窗中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="9db72-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![新增使用者](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="9db72-208">在 hello**選取角色**刀鋒視窗中，選取**擁有者**。</span><span class="sxs-lookup"><span data-stu-id="9db72-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="9db72-209">在 hello**將使用者新增**刀鋒視窗中，輸入 hello 電子郵件地址或名稱要的 hello 使用者作為擁有者 tooadd。</span><span class="sxs-lookup"><span data-stu-id="9db72-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="9db72-210">如果找不到 hello 使用者，您會取得錯誤訊息，說明 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="9db72-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="9db72-211">如果找到 hello 使用者，該使用者列在 hello**使用者**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9db72-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="9db72-212">選取 hello 所在的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="9db72-212">Select hello located user name.</span></span>
9. <span data-ttu-id="9db72-213">選取 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="9db72-213">Select **Select**.</span></span>
10. <span data-ttu-id="9db72-214">選取**確定**tooclose hello**新增存取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9db72-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="9db72-215">當您傳回 toohello**使用者**刀鋒視窗中，已新增 hello 使用者作為擁有者。</span><span class="sxs-lookup"><span data-stu-id="9db72-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="9db72-216">此使用者現在是任何實驗室建立這個訂用帳戶，底下的擁有者，並因此可能無法 tooperform 擁有者工作。</span><span class="sxs-lookup"><span data-stu-id="9db72-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

