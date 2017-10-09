---
title: "aaaUse hello Azure 堆疊原則模組 |Microsoft 文件"
description: "了解 Azure 訂用帳戶 toobehave tooconstrain 像堆疊 Azure 訂用帳戶"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 937ef34f-14d4-4ea9-960b-362ba986f000
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/28/2017
ms.author: helaw
ms.openlocfilehash: a9d01b759d7c4a248f727de682a71a7655ed12d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-policy-using-hello-azure-stack-policy-module"></a>管理 Azure 原則使用 hello Azure 堆疊原則模組
hello Azure 堆疊原則模組可讓您 tooconfigure hello 與 Azure 訂用帳戶相同的版本控制和服務可用性 Azure 堆疊。  hello 模組使用 hello**新增 AzureRMPolicyAssignment** cmdlet toocreate Azure 的原則，進而限制 hello 資源類型，並在服務可用的訂用帳戶中。  完成後，您可以使用針對 Azure 堆疊的 Azure 訂用帳戶 toodevelop 應用程式。  

## <a name="install-hello-module"></a>安裝 hello 模組
1. 安裝 hello 必要的 hello AzureRM PowerShell 模組的版本中的步驟 1 所述[安裝 PowerShell Azure 堆疊以](azure-stack-powershell-install.md)。   
2. [從 GitHub 下載 hello Azure 堆疊工具](azure-stack-powershell-download.md)  
3. [設定 PowerShell 以便搭配 Azure Stack 使用](azure-stack-powershell-configure-user.md)

4. 匯入 hello AzureStack.Policy.psm1 模組：

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-toosubscription"></a>套用原則 toosubscription
hello，下列命令可以使用的 tooapply 針對您的 Azure 訂用帳戶預設 Azure 堆疊原則。 執行前，以您的 Azure 訂用帳戶取代 *Azure 訂用帳戶名稱*。

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-tooa-resource-group"></a>套用原則 tooa 資源群組
您可以在更細微的方法中的 tooapply 原則。  例如，您可能在 hello 中執行的其他資源相同的訂用帳戶。  您可以為範圍 hello 原則應用程式 tooa 特定資源群組，可讓您測試您的應用程式的 Azure 堆疊使用的 Azure 資源。 執行前，以您的 Azure 訂用帳戶名稱取代 *Azure 訂用帳戶名稱*。

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a>動作中的原則
一旦您已部署的 hello Azure 原則，當您嘗試 toodeploy 禁止使用的資源時收到錯誤的原則。  

![資源部署結果因原則限制而失敗](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a>後續步驟
[使用 PowerShell 部署範本](azure-stack-deploy-template-powershell.md)

[使用 Azure CLI 部署範本](azure-stack-deploy-template-command-line.md)

[使用 Visual Studio 部署範本](azure-stack-deploy-template-visual-studio.md)
