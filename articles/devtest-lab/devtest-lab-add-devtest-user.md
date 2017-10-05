---
title: "在 Azure DevTest Labs 中新增擁有者和使用者 | Microsoft Docs"
description: "使用 Azure 入口網站或 PowerShell 在 Azure DevTest Labs 中新增擁有者和使用者"
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
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="8b0e6-103">在 Azure DevTest Labs 中新增擁有者和使用者</span><span class="sxs-lookup"><span data-stu-id="8b0e6-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="8b0e6-104">Azure DevTest Labs 的存取權是由 [Azure 角色型存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md)所控制。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="8b0e6-105">RBAC 可讓您將小組內的職責區隔為「角色」  ，而僅授與使用者執行作業所需的存取權數量。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="8b0e6-106">這些 RBAC 角色的其中三個分別是*擁有者*、*DevTest Labs 使用者*和*參與者*。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="8b0e6-107">在本文中，您會了解三個主要 RBAC 角色中各自可執行哪些動作。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="8b0e6-108">從中您將會了解如何透過入口網站和透過 PowerShell 指令碼將使用者新增至實驗室，以及如何在訂用帳戶層級新增使用者。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="8b0e6-109">可在每個角色執行的動作</span><span class="sxs-lookup"><span data-stu-id="8b0e6-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="8b0e6-110">您可以對使用者指派三個主要角色︰</span><span class="sxs-lookup"><span data-stu-id="8b0e6-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="8b0e6-111">擁有者</span><span class="sxs-lookup"><span data-stu-id="8b0e6-111">Owner</span></span>
* <span data-ttu-id="8b0e6-112">DevTest Labs 使用者</span><span class="sxs-lookup"><span data-stu-id="8b0e6-112">DevTest Labs User</span></span>
* <span data-ttu-id="8b0e6-113">參與者</span><span class="sxs-lookup"><span data-stu-id="8b0e6-113">Contributor</span></span>

<span data-ttu-id="8b0e6-114">下表說明使用者可在每個角色中執行的動作︰</span><span class="sxs-lookup"><span data-stu-id="8b0e6-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="8b0e6-115">**此角色中的使用者可以執行的動作**</span><span class="sxs-lookup"><span data-stu-id="8b0e6-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="8b0e6-116">**DevTest Labs 使用者**</span><span class="sxs-lookup"><span data-stu-id="8b0e6-116">**DevTest Labs User**</span></span> | <span data-ttu-id="8b0e6-117">**擁有者**</span><span class="sxs-lookup"><span data-stu-id="8b0e6-117">**Owner**</span></span> | <span data-ttu-id="8b0e6-118">**參與者**</span><span class="sxs-lookup"><span data-stu-id="8b0e6-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b0e6-119">**實驗室工作**</span><span class="sxs-lookup"><span data-stu-id="8b0e6-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="8b0e6-120">將使用者新增至實驗室</span><span class="sxs-lookup"><span data-stu-id="8b0e6-120">Add users to a lab</span></span> |<span data-ttu-id="8b0e6-121">否</span><span class="sxs-lookup"><span data-stu-id="8b0e6-121">No</span></span> |<span data-ttu-id="8b0e6-122">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-122">Yes</span></span> |<span data-ttu-id="8b0e6-123">否</span><span class="sxs-lookup"><span data-stu-id="8b0e6-123">No</span></span> |
| <span data-ttu-id="8b0e6-124">更新成本設定</span><span class="sxs-lookup"><span data-stu-id="8b0e6-124">Update cost settings</span></span> |<span data-ttu-id="8b0e6-125">否</span><span class="sxs-lookup"><span data-stu-id="8b0e6-125">No</span></span> |<span data-ttu-id="8b0e6-126">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-126">Yes</span></span> |<span data-ttu-id="8b0e6-127">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-127">Yes</span></span> |
| <span data-ttu-id="8b0e6-128">**VM 的基本工作**</span><span class="sxs-lookup"><span data-stu-id="8b0e6-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="8b0e6-129">新增和移除自訂映像</span><span class="sxs-lookup"><span data-stu-id="8b0e6-129">Add and remove custom images</span></span> |<span data-ttu-id="8b0e6-130">否</span><span class="sxs-lookup"><span data-stu-id="8b0e6-130">No</span></span> |<span data-ttu-id="8b0e6-131">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-131">Yes</span></span> |<span data-ttu-id="8b0e6-132">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-132">Yes</span></span> |
| <span data-ttu-id="8b0e6-133">新增、更新和刪除公式</span><span class="sxs-lookup"><span data-stu-id="8b0e6-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="8b0e6-134">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-134">Yes</span></span> |<span data-ttu-id="8b0e6-135">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-135">Yes</span></span> |<span data-ttu-id="8b0e6-136">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-136">Yes</span></span> |
| <span data-ttu-id="8b0e6-137">將 Azure Marketplace 映像加入白名單</span><span class="sxs-lookup"><span data-stu-id="8b0e6-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="8b0e6-138">否</span><span class="sxs-lookup"><span data-stu-id="8b0e6-138">No</span></span> |<span data-ttu-id="8b0e6-139">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-139">Yes</span></span> |<span data-ttu-id="8b0e6-140">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-140">Yes</span></span> |
| <span data-ttu-id="8b0e6-141">**VM 工作**</span><span class="sxs-lookup"><span data-stu-id="8b0e6-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="8b0e6-142">建立 VM</span><span class="sxs-lookup"><span data-stu-id="8b0e6-142">Create VMs</span></span> |<span data-ttu-id="8b0e6-143">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-143">Yes</span></span> |<span data-ttu-id="8b0e6-144">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-144">Yes</span></span> |<span data-ttu-id="8b0e6-145">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-145">Yes</span></span> |
| <span data-ttu-id="8b0e6-146">啟動、停止和刪除 VM</span><span class="sxs-lookup"><span data-stu-id="8b0e6-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="8b0e6-147">僅限使用者所建立的 VM</span><span class="sxs-lookup"><span data-stu-id="8b0e6-147">Only VMs created by the user</span></span> |<span data-ttu-id="8b0e6-148">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-148">Yes</span></span> |<span data-ttu-id="8b0e6-149">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-149">Yes</span></span> |
| <span data-ttu-id="8b0e6-150">更新 VM 原則</span><span class="sxs-lookup"><span data-stu-id="8b0e6-150">Update VM policies</span></span> |<span data-ttu-id="8b0e6-151">否</span><span class="sxs-lookup"><span data-stu-id="8b0e6-151">No</span></span> |<span data-ttu-id="8b0e6-152">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-152">Yes</span></span> |<span data-ttu-id="8b0e6-153">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-153">Yes</span></span> |
| <span data-ttu-id="8b0e6-154">在 VM 中新增/移除資料磁碟</span><span class="sxs-lookup"><span data-stu-id="8b0e6-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="8b0e6-155">僅限使用者所建立的 VM</span><span class="sxs-lookup"><span data-stu-id="8b0e6-155">Only VMs created by the user</span></span> |<span data-ttu-id="8b0e6-156">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-156">Yes</span></span> |<span data-ttu-id="8b0e6-157">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-157">Yes</span></span> |
| <span data-ttu-id="8b0e6-158">**構件工作**</span><span class="sxs-lookup"><span data-stu-id="8b0e6-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="8b0e6-159">新增和移除構件儲存機制</span><span class="sxs-lookup"><span data-stu-id="8b0e6-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="8b0e6-160">否</span><span class="sxs-lookup"><span data-stu-id="8b0e6-160">No</span></span> |<span data-ttu-id="8b0e6-161">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-161">Yes</span></span> |<span data-ttu-id="8b0e6-162">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-162">Yes</span></span> |
| <span data-ttu-id="8b0e6-163">套用構件</span><span class="sxs-lookup"><span data-stu-id="8b0e6-163">Apply artifacts</span></span> |<span data-ttu-id="8b0e6-164">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-164">Yes</span></span> |<span data-ttu-id="8b0e6-165">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-165">Yes</span></span> |<span data-ttu-id="8b0e6-166">是</span><span class="sxs-lookup"><span data-stu-id="8b0e6-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="8b0e6-167">當使用者建立 VM 時，該使用者會自動指派給所建立 VM 的 **擁有者** 角色。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="8b0e6-168">在實驗室層級新增擁有者或使用者</span><span class="sxs-lookup"><span data-stu-id="8b0e6-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="8b0e6-169">可透過 Azure 入口網站在實驗室層級新增擁有者和使用者。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="8b0e6-170">這包括擁有有效 [Microsoft 帳戶 (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)的外部使用者。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="8b0e6-171">下列步驟會引導您進行在 Azure DevTest Labs 新增擁有者或使用者至實驗室的程序︰</span><span class="sxs-lookup"><span data-stu-id="8b0e6-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="8b0e6-172">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="8b0e6-173">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-173">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="8b0e6-174">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="8b0e6-175">在實驗室的刀鋒視窗上，選取 [組態] 。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-175">On the lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="8b0e6-176">在 [組態] 刀鋒視窗上，選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-176">On the **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="8b0e6-177">在 [使用者] 刀鋒視窗上，選取 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-177">On the **Users** blade, select **+Add**.</span></span>
   
    ![新增使用者](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="8b0e6-179">在 [選取角色]  刀鋒視窗上，選取所需的角色。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-179">On the **Select a role** blade, select the desired role.</span></span> <span data-ttu-id="8b0e6-180">[可在每個角色執行的動作](#actions-that-can-be-performed-in-each-role) 一節列出使用者可在擁有者、DevTest 使用者和參與者角色中執行的各種動作。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-180">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="8b0e6-181">在 [新增使用者]  刀鋒視窗上，輸入您想要在指定角色中新增之使用者的電子郵件地址或名稱。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-181">On the **Add users** blade, enter the email address or name of the user you want to add in the role you specified.</span></span> <span data-ttu-id="8b0e6-182">如果找不到該使用者，會出現錯誤訊息來說明問題。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-182">If the user can't be found, an error message explains the issue.</span></span> <span data-ttu-id="8b0e6-183">如果有找到使用者，則會列出並選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-183">If the user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="8b0e6-184">選取 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-184">Select **Select**.</span></span>
10. <span data-ttu-id="8b0e6-185">選取 [確定]，以關閉 [新增存取] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-185">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="8b0e6-186">當您返回 [使用者]  刀鋒視窗時，該使用者已新增。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-186">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="8b0e6-187">使用 PowerShell 將外部使用者新增至實驗室</span><span class="sxs-lookup"><span data-stu-id="8b0e6-187">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="8b0e6-188">除了在 Azure 入口網站新增使用者，您還可以使用 PowerShell 指令碼將外部使用者新增至實驗室。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-188">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="8b0e6-189">在下列範例中，直接修改 **Values to change** 註解底下的值。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-189">In the following example, simply modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="8b0e6-190">您可以從 Azure 入口網站中的 [實驗室] 刀鋒視窗擷取 `subscriptionId`、`labResourceGroup` 及 `labName`。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-190">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="8b0e6-191">範例指令碼假設指定的使用者已做為來賓新增至 Active Directory 中，如果並非如此則會失敗。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-191">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="8b0e6-192">若要將不在 Active Directory 中的使用者新增至實驗室，請如 [在實驗室層級新增擁有者或使用者](#add-an-owner-or-user-at-the-lab-level)一節所述使用 Azure 入口網站將使用者指派給角色。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-192">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="8b0e6-193">在訂用帳戶層級新增擁有者或使用者</span><span class="sxs-lookup"><span data-stu-id="8b0e6-193">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="8b0e6-194">在 Azure 中，Azure 權限會從父範圍傳播至子範圍。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-194">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="8b0e6-195">因此，包含實驗室之 Azure 訂用帳戶的擁有者會自動成為這些實驗室的擁有者。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="8b0e6-196">他們也擁有實驗室使用者和 Azure DevTest Labs 服務所建立的 VM 和其他資源。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-196">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="8b0e6-197">您可以在 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)中透過實驗室的刀鋒視窗對實驗室新增其他擁有者。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-197">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="8b0e6-198">不過，所新增擁有者的管理範圍小於訂用帳戶擁有者的範圍。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-198">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="8b0e6-199">例如，新增的擁有者沒有 DevTest Labs 服務在訂用帳戶中所建立之某些資源的完整存取權。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-199">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="8b0e6-200">若要對 Azure 訂用帳戶新增擁有者，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="8b0e6-200">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="8b0e6-201">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-201">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="8b0e6-202">選取 [更多服務]，然後從清單中選取 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-202">Select **More Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="8b0e6-203">選取所需的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-203">Select the desired subscription.</span></span>
4. <span data-ttu-id="8b0e6-204">選取 [存取]  圖示。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-204">Select **Access** icon.</span></span> 
   
    ![存取使用者](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="8b0e6-206">在 [使用者] 刀鋒視窗上，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-206">On the **Users** blade, select **Add**.</span></span>
   
    ![新增使用者](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="8b0e6-208">在 [選取角色] 刀鋒視窗中，選取 [擁有者]。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-208">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="8b0e6-209">在 [新增使用者]  刀鋒視窗上，輸入您想要新增為擁有者之使用者的電子郵件地址或名稱。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-209">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="8b0e6-210">如果找不到該使用者，您會收到錯誤訊息來說明問題。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-210">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="8b0e6-211">如果有找到使用者，該使用者會列在 [使用者]  文字方塊底下。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-211">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="8b0e6-212">選取找到的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-212">Select the located user name.</span></span>
9. <span data-ttu-id="8b0e6-213">選取 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-213">Select **Select**.</span></span>
10. <span data-ttu-id="8b0e6-214">選取 [確定]，以關閉 [新增存取] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-214">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="8b0e6-215">當您返回 [使用者]  刀鋒視窗時，該使用者已新增為擁有者。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-215">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="8b0e6-216">此使用者現在是在此訂用帳戶下建立之所有實驗室的擁有者，因而能夠執行擁有者工作。</span><span class="sxs-lookup"><span data-stu-id="8b0e6-216">This user is now an owner of any labs created under this subscription, and thus be able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

