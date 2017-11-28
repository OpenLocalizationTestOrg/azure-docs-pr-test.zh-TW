---
title: "使用 Azure Stack 原則模組 | Microsoft Docs"
description: "瞭解如何將 Azure 訂用帳戶的行為限制為與 Azure Stack 訂用帳戶類似"
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
ms.openlocfilehash: 22251dd0428b959069dfc392f4ccdda19b08b9de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-policy-using-the-azure-stack-policy-module"></a><span data-ttu-id="f8429-103">使用 Azure Stack 原則模組管理 Azure 原則</span><span class="sxs-lookup"><span data-stu-id="f8429-103">Manage Azure policy using the Azure Stack Policy Module</span></span>
<span data-ttu-id="f8429-104">Azure Stack 原則模組可讓您將 Azure 訂用帳戶，設定與 Azure Stack 具有相同的版本和服務可用性。</span><span class="sxs-lookup"><span data-stu-id="f8429-104">The Azure Stack Policy module allows you to configure an Azure subscription with the same versioning and service availability as Azure Stack.</span></span>  <span data-ttu-id="f8429-105">此模組會使用 **New-AzureRMPolicyAssignment** cmdlet 來建立 Azure 原則，限制訂用帳戶中可用的資源類型和服務。</span><span class="sxs-lookup"><span data-stu-id="f8429-105">The module uses the **New-AzureRMPolicyAssignment** cmdlet to create an Azure policy, which limits the resource types and services available in a subscription.</span></span>  <span data-ttu-id="f8429-106">完成後，您可以使用您的 Azure 訂用帳戶來開發 Azure Stack 的目標應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8429-106">Once complete, you can use your Azure subscription to develop apps targeted for Azure Stack.</span></span>  

## <a name="install-the-module"></a><span data-ttu-id="f8429-107">安裝模組</span><span class="sxs-lookup"><span data-stu-id="f8429-107">Install the module</span></span>
1. <span data-ttu-id="f8429-108">依據[安裝 Azure Stack 的 PowerShell](azure-stack-powershell-install.md) 步驟 1 的說明，安裝必要的 AzureRM PowerShell 模組版本。</span><span class="sxs-lookup"><span data-stu-id="f8429-108">Install the required version of the AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>   
2. [<span data-ttu-id="f8429-109">從 GitHub 下載 Azure Stack 工具</span><span class="sxs-lookup"><span data-stu-id="f8429-109">Download the Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)  
3. [<span data-ttu-id="f8429-110">設定 PowerShell 以便搭配 Azure Stack 使用</span><span class="sxs-lookup"><span data-stu-id="f8429-110">Configure PowerShell for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md)

4. <span data-ttu-id="f8429-111">匯入 AzureStack.Policy.psm1 模組：</span><span class="sxs-lookup"><span data-stu-id="f8429-111">Import the AzureStack.Policy.psm1 module:</span></span>

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-to-subscription"></a><span data-ttu-id="f8429-112">將原則套用至訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f8429-112">Apply policy to subscription</span></span>
<span data-ttu-id="f8429-113">下列命令可針對您的 Azure 訂用帳戶來套用預設 Azure Stack 原則。</span><span class="sxs-lookup"><span data-stu-id="f8429-113">The following command can be used to apply a default Azure Stack policy against your Azure subscription.</span></span> <span data-ttu-id="f8429-114">執行前，以您的 Azure 訂用帳戶取代 *Azure 訂用帳戶名稱*。</span><span class="sxs-lookup"><span data-stu-id="f8429-114">Before running, replace *Azure Subscription Name* with your Azure subscription.</span></span>

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-to-a-resource-group"></a><span data-ttu-id="f8429-115">將原則套用至資源群組</span><span class="sxs-lookup"><span data-stu-id="f8429-115">Apply policy to a resource group</span></span>
<span data-ttu-id="f8429-116">您可能想要以更細微的方式套用原則。</span><span class="sxs-lookup"><span data-stu-id="f8429-116">You may want to apply policies in a more granular method.</span></span>  <span data-ttu-id="f8429-117">例如，您在相同的訂用帳戶中可能有其他正在執行的資源。</span><span class="sxs-lookup"><span data-stu-id="f8429-117">As an example, you may have other resources running in the same subscription.</span></span>  <span data-ttu-id="f8429-118">您可以將原則應用程式領域套用至特定的資源群組，可讓您使用 Azure 資源測試 Azure Stack 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8429-118">You can scope the policy application to a specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span></span> <span data-ttu-id="f8429-119">執行前，以您的 Azure 訂用帳戶名稱取代 *Azure 訂用帳戶名稱*。</span><span class="sxs-lookup"><span data-stu-id="f8429-119">Before running, replace *Azure Subscription Name* with your Azure subscription name.</span></span>

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a><span data-ttu-id="f8429-120">動作中的原則</span><span class="sxs-lookup"><span data-stu-id="f8429-120">Policy in action</span></span>
<span data-ttu-id="f8429-121">部署 Azure 原則後，當您嘗試部署原則禁止的資源時會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8429-121">Once you've deployed the Azure policy, you receive an error when you try to deploy a resource that prohibited by policy.</span></span>  

![資源部署結果因原則限制而失敗](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a><span data-ttu-id="f8429-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8429-123">Next steps</span></span>
[<span data-ttu-id="f8429-124">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="f8429-124">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

[<span data-ttu-id="f8429-125">使用 Azure CLI 部署範本</span><span class="sxs-lookup"><span data-stu-id="f8429-125">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="f8429-126">使用 Visual Studio 部署範本</span><span class="sxs-lookup"><span data-stu-id="f8429-126">Deploy Templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)
