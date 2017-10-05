---
title: "將特定實驗室原則的權限授與使用者 | Microsoft Docs"
description: "了解如何根據每個使用者的需求將使用者權限授與研發/測試實驗室中的特定實驗室原則"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="235c6-103">將特定實驗室原則的權限授與使用者</span><span class="sxs-lookup"><span data-stu-id="235c6-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="235c6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="235c6-104">Overview</span></span>
<span data-ttu-id="235c6-105">本文說明如何使用 PowerShell 將特定實驗室原則的權限授與使用者。</span><span class="sxs-lookup"><span data-stu-id="235c6-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="235c6-106">這樣便可根據每個使用者的需求來套用權限。</span><span class="sxs-lookup"><span data-stu-id="235c6-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="235c6-107">例如，您可能想要將變更 VM 原則設定 (而非成本原則) 的能力授與特定的使用者。</span><span class="sxs-lookup"><span data-stu-id="235c6-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="235c6-108">原則即資源</span><span class="sxs-lookup"><span data-stu-id="235c6-108">Policies as resources</span></span>
<span data-ttu-id="235c6-109">如 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md) 中所討論，RBAC 可讓您對 Azure 的資源進行更細緻的存取管理。</span><span class="sxs-lookup"><span data-stu-id="235c6-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="235c6-110">您可以使用 RBAC 來區隔開發小組的職責，僅授與使用者作業所需的存取權。</span><span class="sxs-lookup"><span data-stu-id="235c6-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="235c6-111">在研發/測試實驗室中，原則是一種可啟用 RBAC 動作 **Microsoft.DevTestLab/labs/policySets/policies/**的資源類型。</span><span class="sxs-lookup"><span data-stu-id="235c6-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="235c6-112">每個實驗室原則都是「原則」資源類型中的資源，並且可被指派成某個 RBAC 角色的範圍。</span><span class="sxs-lookup"><span data-stu-id="235c6-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="235c6-113">例如，若要授與使用者讀取/寫入權限**允許 VM 大小**原則，您會建立自訂安全性角色可搭配**Microsoft.DevTestLab/labs/policySets/policies/***動作，然後將適當的使用者指派給此自訂角色的範圍內**Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**。</span><span class="sxs-lookup"><span data-stu-id="235c6-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="235c6-114">若要深入了解 RBAC 中的自訂角色，請參閱[自訂角色存取控制](../active-directory/role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="235c6-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="235c6-115">使用 PowerShell 建立實驗室自訂角色</span><span class="sxs-lookup"><span data-stu-id="235c6-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="235c6-116">為了開始進行，您將需要閱讀下列文章，此文章將說明如何安裝和設定 Azure PowerShell Cmdlet： [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre)。</span><span class="sxs-lookup"><span data-stu-id="235c6-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="235c6-117">設定完 Azure PowerShell Cmdlet 之後，您便可執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="235c6-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="235c6-118">列出資源提供者的所有作業/動作</span><span class="sxs-lookup"><span data-stu-id="235c6-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="235c6-119">列出特定角色中的動作：</span><span class="sxs-lookup"><span data-stu-id="235c6-119">List actions in a particular role:</span></span>
* <span data-ttu-id="235c6-120">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="235c6-120">Create a custom role</span></span>

<span data-ttu-id="235c6-121">下列 PowerShell 指令碼提供範例來說明如何執行這些工作：</span><span class="sxs-lookup"><span data-stu-id="235c6-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="235c6-122">使用自訂角色將特定原則的權限指派給使用者</span><span class="sxs-lookup"><span data-stu-id="235c6-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="235c6-123">定義自訂角色之後，您便可以將它們指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="235c6-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="235c6-124">為了將自訂角色指派給使用者，您必須先取得代表該使用者的 **ObjectId** 。</span><span class="sxs-lookup"><span data-stu-id="235c6-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="235c6-125">若要這樣做，請使用 **Get-AzureRmADUser** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="235c6-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="235c6-126">在下列範例中， **SomeUser** 使用者的 *ObjectId* 是 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3。</span><span class="sxs-lookup"><span data-stu-id="235c6-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="235c6-127">有了使用者的 **ObjectId** 和自訂角色名稱之後，您便可以使用 **New-AzureRmRoleAssignment** Cmdlet 將該角色指派給使用者：</span><span class="sxs-lookup"><span data-stu-id="235c6-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="235c6-128">在先前的範例中，使用的是 **AllowedVmSizesInLab** 原則。</span><span class="sxs-lookup"><span data-stu-id="235c6-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="235c6-129">您也可以使用下列任何原則：</span><span class="sxs-lookup"><span data-stu-id="235c6-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="235c6-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="235c6-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="235c6-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="235c6-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="235c6-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="235c6-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="235c6-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="235c6-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="235c6-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="235c6-134">Next steps</span></span>
<span data-ttu-id="235c6-135">將特定實驗室原則的權限授與使用者之後，以下是一些需要考量的後續步驟：</span><span class="sxs-lookup"><span data-stu-id="235c6-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="235c6-136">[安全存取實驗室](devtest-lab-add-devtest-user.md)。</span><span class="sxs-lookup"><span data-stu-id="235c6-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="235c6-137">[設定實驗室原則](devtest-lab-set-lab-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="235c6-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="235c6-138">[建立實驗室範本](devtest-lab-create-template.md)。</span><span class="sxs-lookup"><span data-stu-id="235c6-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="235c6-139">[為您的 VM 建立自訂成品](devtest-lab-artifact-author.md)。</span><span class="sxs-lookup"><span data-stu-id="235c6-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="235c6-140">[將具有構件的 VM 新增至實驗室](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="235c6-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

