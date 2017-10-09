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
# <a name="manage-azure-policy-using-hello-azure-stack-policy-module"></a><span data-ttu-id="f2ebd-103">管理 Azure 原則使用 hello Azure 堆疊原則模組</span><span class="sxs-lookup"><span data-stu-id="f2ebd-103">Manage Azure policy using hello Azure Stack Policy Module</span></span>
<span data-ttu-id="f2ebd-104">hello Azure 堆疊原則模組可讓您 tooconfigure hello 與 Azure 訂用帳戶相同的版本控制和服務可用性 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-104">hello Azure Stack Policy module allows you tooconfigure an Azure subscription with hello same versioning and service availability as Azure Stack.</span></span>  <span data-ttu-id="f2ebd-105">hello 模組使用 hello**新增 AzureRMPolicyAssignment** cmdlet toocreate Azure 的原則，進而限制 hello 資源類型，並在服務可用的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-105">hello module uses hello **New-AzureRMPolicyAssignment** cmdlet toocreate an Azure policy, which limits hello resource types and services available in a subscription.</span></span>  <span data-ttu-id="f2ebd-106">完成後，您可以使用針對 Azure 堆疊的 Azure 訂用帳戶 toodevelop 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-106">Once complete, you can use your Azure subscription toodevelop apps targeted for Azure Stack.</span></span>  

## <a name="install-hello-module"></a><span data-ttu-id="f2ebd-107">安裝 hello 模組</span><span class="sxs-lookup"><span data-stu-id="f2ebd-107">Install hello module</span></span>
1. <span data-ttu-id="f2ebd-108">安裝 hello 必要的 hello AzureRM PowerShell 模組的版本中的步驟 1 所述[安裝 PowerShell Azure 堆疊以](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-108">Install hello required version of hello AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>   
2. [<span data-ttu-id="f2ebd-109">從 GitHub 下載 hello Azure 堆疊工具</span><span class="sxs-lookup"><span data-stu-id="f2ebd-109">Download hello Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)  
3. [<span data-ttu-id="f2ebd-110">設定 PowerShell 以便搭配 Azure Stack 使用</span><span class="sxs-lookup"><span data-stu-id="f2ebd-110">Configure PowerShell for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md)

4. <span data-ttu-id="f2ebd-111">匯入 hello AzureStack.Policy.psm1 模組：</span><span class="sxs-lookup"><span data-stu-id="f2ebd-111">Import hello AzureStack.Policy.psm1 module:</span></span>

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-toosubscription"></a><span data-ttu-id="f2ebd-112">套用原則 toosubscription</span><span class="sxs-lookup"><span data-stu-id="f2ebd-112">Apply policy toosubscription</span></span>
<span data-ttu-id="f2ebd-113">hello，下列命令可以使用的 tooapply 針對您的 Azure 訂用帳戶預設 Azure 堆疊原則。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-113">hello following command can be used tooapply a default Azure Stack policy against your Azure subscription.</span></span> <span data-ttu-id="f2ebd-114">執行前，以您的 Azure 訂用帳戶取代 *Azure 訂用帳戶名稱*。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-114">Before running, replace *Azure Subscription Name* with your Azure subscription.</span></span>

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-tooa-resource-group"></a><span data-ttu-id="f2ebd-115">套用原則 tooa 資源群組</span><span class="sxs-lookup"><span data-stu-id="f2ebd-115">Apply policy tooa resource group</span></span>
<span data-ttu-id="f2ebd-116">您可以在更細微的方法中的 tooapply 原則。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-116">You may want tooapply policies in a more granular method.</span></span>  <span data-ttu-id="f2ebd-117">例如，您可能在 hello 中執行的其他資源相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-117">As an example, you may have other resources running in hello same subscription.</span></span>  <span data-ttu-id="f2ebd-118">您可以為範圍 hello 原則應用程式 tooa 特定資源群組，可讓您測試您的應用程式的 Azure 堆疊使用的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-118">You can scope hello policy application tooa specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span></span> <span data-ttu-id="f2ebd-119">執行前，以您的 Azure 訂用帳戶名稱取代 *Azure 訂用帳戶名稱*。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-119">Before running, replace *Azure Subscription Name* with your Azure subscription name.</span></span>

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a><span data-ttu-id="f2ebd-120">動作中的原則</span><span class="sxs-lookup"><span data-stu-id="f2ebd-120">Policy in action</span></span>
<span data-ttu-id="f2ebd-121">一旦您已部署的 hello Azure 原則，當您嘗試 toodeploy 禁止使用的資源時收到錯誤的原則。</span><span class="sxs-lookup"><span data-stu-id="f2ebd-121">Once you've deployed hello Azure policy, you receive an error when you try toodeploy a resource that prohibited by policy.</span></span>  

![資源部署結果因原則限制而失敗](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a><span data-ttu-id="f2ebd-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2ebd-123">Next steps</span></span>
[<span data-ttu-id="f2ebd-124">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="f2ebd-124">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

[<span data-ttu-id="f2ebd-125">使用 Azure CLI 部署範本</span><span class="sxs-lookup"><span data-stu-id="f2ebd-125">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="f2ebd-126">使用 Visual Studio 部署範本</span><span class="sxs-lookup"><span data-stu-id="f2ebd-126">Deploy Templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)
