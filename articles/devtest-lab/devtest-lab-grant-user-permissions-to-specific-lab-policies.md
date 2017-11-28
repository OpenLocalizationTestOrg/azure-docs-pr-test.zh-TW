---
title: "aaaGrant 使用者權限 toospecific 實驗室原則 |Microsoft 文件"
description: "了解如何 toogrant 使用者權限 toospecific 實驗室中的原則 DevTest Labs 根據每個使用者的需求"
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
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="07a44-103">Toospecific 實驗室原則授與使用者權限</span><span class="sxs-lookup"><span data-stu-id="07a44-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="07a44-104">概觀</span><span class="sxs-lookup"><span data-stu-id="07a44-104">Overview</span></span>
<span data-ttu-id="07a44-105">本文將說明如何 toouse PowerShell toogrant 使用者權限 tooa 特定實驗室原則。</span><span class="sxs-lookup"><span data-stu-id="07a44-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="07a44-106">這樣便可根據每個使用者的需求來套用權限。</span><span class="sxs-lookup"><span data-stu-id="07a44-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="07a44-107">例如，您可能想 toogrant 特定使用者 hello 能力 toochange hello VM 原則設定，但不是 hello 成本的原則。</span><span class="sxs-lookup"><span data-stu-id="07a44-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="07a44-108">原則即資源</span><span class="sxs-lookup"><span data-stu-id="07a44-108">Policies as resources</span></span>
<span data-ttu-id="07a44-109">Hello 中所述[Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)文件： RBAC 啟用 azure 的精細存取管理的資源。</span><span class="sxs-lookup"><span data-stu-id="07a44-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="07a44-110">使用 RBAC 時，您可以隔離 DevOps 小組內的責任，並授與存取 toousers 只有 hello 數量他們需要 tooperform 他們的工作。</span><span class="sxs-lookup"><span data-stu-id="07a44-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="07a44-111">DevTest 實驗室中原則已啟用 hello RBAC 動作資源類型**Microsoft.DevTestLab/labs/policySets/policies/**。</span><span class="sxs-lookup"><span data-stu-id="07a44-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="07a44-112">每個實驗室原則 hello 原則資源類型中的資源，且可以指派為範圍 tooan RBAC 角色。</span><span class="sxs-lookup"><span data-stu-id="07a44-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="07a44-113">例如，在訂單 toogrant 使用者讀取/寫入權限 toohello**允許 VM 大小**原則，您會建立自訂安全性角色可搭配 hello **Microsoft.DevTestLab/labs/policySets/policies/*** 動作，然後再指派 hello 適當的使用者 toothis 自訂角色中的 hello 範圍**Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**。</span><span class="sxs-lookup"><span data-stu-id="07a44-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="07a44-114">toolearn 進一步了解自訂角色中 RBAC，請參閱 hello[自訂角色存取控制](../active-directory/role-based-access-control-custom-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="07a44-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="07a44-115">使用 PowerShell 建立實驗室自訂角色</span><span class="sxs-lookup"><span data-stu-id="07a44-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="07a44-116">在啟動順序 tooget，您將需要 tooread hello 下列文章，將說明如何 tooinstall 及設定 hello Azure PowerShell cmdlet: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre)。</span><span class="sxs-lookup"><span data-stu-id="07a44-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="07a44-117">一旦您已設定 hello Azure PowerShell cmdlet，您可以執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="07a44-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="07a44-118">列出所有 hello operations/動作的資源提供者</span><span class="sxs-lookup"><span data-stu-id="07a44-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="07a44-119">列出特定角色中的動作：</span><span class="sxs-lookup"><span data-stu-id="07a44-119">List actions in a particular role:</span></span>
* <span data-ttu-id="07a44-120">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="07a44-120">Create a custom role</span></span>

<span data-ttu-id="07a44-121">下列 PowerShell 指令碼的 hello 說明的範例 tooperform 這些工作：</span><span class="sxs-lookup"><span data-stu-id="07a44-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="07a44-122">指派權限 tooa 使用者提供具體的原則，使用自訂角色</span><span class="sxs-lookup"><span data-stu-id="07a44-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="07a44-123">一旦您定義了自訂角色，您可以將它們指派 toousers。</span><span class="sxs-lookup"><span data-stu-id="07a44-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="07a44-124">在訂單 tooassign 自訂角色 tooa 使用者，您必須先取得 hello **ObjectId**代表該使用者。</span><span class="sxs-lookup"><span data-stu-id="07a44-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="07a44-125">可使用 hello toodo **Get AzureRmADUser** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="07a44-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="07a44-126">在下列範例的 hello，hello **ObjectId**的 hello *SomeUser*使用者是 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3。</span><span class="sxs-lookup"><span data-stu-id="07a44-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="07a44-127">一旦您擁有 hello **ObjectId** hello 使用者和自訂角色名稱，您可以指派給該角色 toohello 使用者以 hello**新增 AzureRmRoleAssignment** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="07a44-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="07a44-128">Hello 上述範例中，在 hello **AllowedVmSizesInLab**原則使用。</span><span class="sxs-lookup"><span data-stu-id="07a44-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="07a44-129">您可以使用任何 hello 下列原則：</span><span class="sxs-lookup"><span data-stu-id="07a44-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="07a44-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="07a44-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="07a44-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="07a44-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="07a44-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="07a44-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="07a44-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="07a44-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="07a44-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07a44-134">Next steps</span></span>
<span data-ttu-id="07a44-135">一次您授與使用者權限 toospecific 實驗室原則，以下是一些下一個步驟 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="07a44-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="07a44-136">[安全存取 tooa 實驗室](devtest-lab-add-devtest-user.md)。</span><span class="sxs-lookup"><span data-stu-id="07a44-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="07a44-137">[設定實驗室原則](devtest-lab-set-lab-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="07a44-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="07a44-138">[建立實驗室範本](devtest-lab-create-template.md)。</span><span class="sxs-lookup"><span data-stu-id="07a44-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="07a44-139">[為您的 VM 建立自訂成品](devtest-lab-artifact-author.md)。</span><span class="sxs-lookup"><span data-stu-id="07a44-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="07a44-140">[加入具有成品 tooa 實驗室 VM](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="07a44-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

