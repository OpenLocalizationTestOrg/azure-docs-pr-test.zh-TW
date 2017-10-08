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
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Toospecific 實驗室原則授與使用者權限
## <a name="overview"></a>概觀
本文將說明如何 toouse PowerShell toogrant 使用者權限 tooa 特定實驗室原則。 這樣便可根據每個使用者的需求來套用權限。 例如，您可能想 toogrant 特定使用者 hello 能力 toochange hello VM 原則設定，但不是 hello 成本的原則。

## <a name="policies-as-resources"></a>原則即資源
Hello 中所述[Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)文件： RBAC 啟用 azure 的精細存取管理的資源。 使用 RBAC 時，您可以隔離 DevOps 小組內的責任，並授與存取 toousers 只有 hello 數量他們需要 tooperform 他們的工作。

DevTest 實驗室中原則已啟用 hello RBAC 動作資源類型**Microsoft.DevTestLab/labs/policySets/policies/**。 每個實驗室原則 hello 原則資源類型中的資源，且可以指派為範圍 tooan RBAC 角色。

例如，在訂單 toogrant 使用者讀取/寫入權限 toohello**允許 VM 大小**原則，您會建立自訂安全性角色可搭配 hello **Microsoft.DevTestLab/labs/policySets/policies/*** 動作，然後再指派 hello 適當的使用者 toothis 自訂角色中的 hello 範圍**Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**。

toolearn 進一步了解自訂角色中 RBAC，請參閱 hello[自訂角色存取控制](../active-directory/role-based-access-control-custom-roles.md)。

## <a name="creating-a-lab-custom-role-using-powershell"></a>使用 PowerShell 建立實驗室自訂角色
在啟動順序 tooget，您將需要 tooread hello 下列文章，將說明如何 tooinstall 及設定 hello Azure PowerShell cmdlet: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre)。

一旦您已設定 hello Azure PowerShell cmdlet，您可以執行下列工作的 hello:

* 列出所有 hello operations/動作的資源提供者
* 列出特定角色中的動作：
* 建立自訂角色

下列 PowerShell 指令碼的 hello 說明的範例 tooperform 這些工作：

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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>指派權限 tooa 使用者提供具體的原則，使用自訂角色
一旦您定義了自訂角色，您可以將它們指派 toousers。 在訂單 tooassign 自訂角色 tooa 使用者，您必須先取得 hello **ObjectId**代表該使用者。 可使用 hello toodo **Get AzureRmADUser** cmdlet。

在下列範例的 hello，hello **ObjectId**的 hello *SomeUser*使用者是 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3。

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

一旦您擁有 hello **ObjectId** hello 使用者和自訂角色名稱，您可以指派給該角色 toohello 使用者以 hello**新增 AzureRmRoleAssignment** cmdlet:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

Hello 上述範例中，在 hello **AllowedVmSizesInLab**原則使用。 您可以使用任何 hello 下列原則：

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>後續步驟
一次您授與使用者權限 toospecific 實驗室原則，以下是一些下一個步驟 tooconsider:

* [安全存取 tooa 實驗室](devtest-lab-add-devtest-user.md)。
* [設定實驗室原則](devtest-lab-set-lab-policy.md)。
* [建立實驗室範本](devtest-lab-create-template.md)。
* [為您的 VM 建立自訂成品](devtest-lab-artifact-author.md)。
* [加入具有成品 tooa 實驗室 VM](devtest-lab-add-vm-with-artifacts.md)。

