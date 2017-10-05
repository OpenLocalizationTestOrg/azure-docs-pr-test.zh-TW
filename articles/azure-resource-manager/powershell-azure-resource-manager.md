---
title: "使用 PowerShell 管理 Azure 解決方案 | Microsoft Docs"
description: "使用 Azure PowerShell 和 Resource Manager 管理資源。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: ff42e5cb29005c5f4b97babdae58bef9382071f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="3ff38-103">使用 Azure PowerShell 和 Resource Manager 管理資源</span><span class="sxs-lookup"><span data-stu-id="3ff38-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ff38-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="3ff38-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="3ff38-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3ff38-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="3ff38-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ff38-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="3ff38-107">REST API</span><span class="sxs-lookup"><span data-stu-id="3ff38-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="3ff38-108">在本文中，您會了解如何使用 Azure PowerShell 和 Azure Resource Manager 管理您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3ff38-108">In this article, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="3ff38-109">如果您不熟悉如何使用 Resource Manager，請參閱 [Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="3ff38-110">本主題著重於管理工作。</span><span class="sxs-lookup"><span data-stu-id="3ff38-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="3ff38-111">您將：</span><span class="sxs-lookup"><span data-stu-id="3ff38-111">You will:</span></span>

1. <span data-ttu-id="3ff38-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="3ff38-112">Create a resource group</span></span>
2. <span data-ttu-id="3ff38-113">將資源加入資源群組</span><span class="sxs-lookup"><span data-stu-id="3ff38-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="3ff38-114">將標籤加入資源</span><span class="sxs-lookup"><span data-stu-id="3ff38-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="3ff38-115">根據名稱或標籤值查詢資源</span><span class="sxs-lookup"><span data-stu-id="3ff38-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="3ff38-116">套用和移除資源的鎖定</span><span class="sxs-lookup"><span data-stu-id="3ff38-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="3ff38-117">刪除資源群組</span><span class="sxs-lookup"><span data-stu-id="3ff38-117">Delete a resource group</span></span>

<span data-ttu-id="3ff38-118">本文不會說明如何將 Resource Manager 範本部署到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ff38-118">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="3ff38-119">如需該資訊，請參閱[使用 Resource Manager 範本與 Azure PowerShell 來部署資源](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="3ff38-120">開始使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ff38-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="3ff38-121">如果您未安裝 Azure PowerShell，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-121">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="3ff38-122">如果您之前已安裝 Azure PowerShell 但近期未更新，請考慮安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="3ff38-122">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="3ff38-123">您可以透過先前用來安裝的方法來更新版本。</span><span class="sxs-lookup"><span data-stu-id="3ff38-123">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="3ff38-124">例如，如果您使用 Web Platform Installer，請再次啟動它並尋找更新。</span><span class="sxs-lookup"><span data-stu-id="3ff38-124">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="3ff38-125">若要檢查您 Azure 資源模組的版本，請使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="3ff38-125">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="3ff38-126">本主題已針對版本 3.3.0 更新。</span><span class="sxs-lookup"><span data-stu-id="3ff38-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="3ff38-127">如果您的版本較舊，您的經驗可能與本主題中所顯示的步驟不符。</span><span class="sxs-lookup"><span data-stu-id="3ff38-127">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="3ff38-128">如需此版本中 Cmdlet 的相關文件，請參閱 [AzureRM.Resources 模組](/powershell/module/azurerm.resources)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-128">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="3ff38-129">登入您的 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="3ff38-129">Log in to your Azure account</span></span>
<span data-ttu-id="3ff38-130">在使用您的解決方案之前，您必須登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ff38-130">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="3ff38-131">若要登入您的 Azure 帳戶，請使用 **Login-AzureRmAccount** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ff38-131">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3ff38-132">cmdlet 會提示您 Azure 帳戶的登入認證。</span><span class="sxs-lookup"><span data-stu-id="3ff38-132">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="3ff38-133">登入之後，它會下載您的帳戶設定以供 Azure PowerShell 使用。</span><span class="sxs-lookup"><span data-stu-id="3ff38-133">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="3ff38-134">Cmdlet 會傳回您的帳戶和訂用帳戶的相關資訊供作業使用。</span><span class="sxs-lookup"><span data-stu-id="3ff38-134">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="3ff38-135">如果您有多個訂用帳戶，可以切換成其他訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ff38-135">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="3ff38-136">首先，我們來看看您帳戶的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ff38-136">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="3ff38-137">它會傳回啟用和停用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ff38-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="3ff38-138">若要切換成其他訂用帳戶，請使用 **Set-AzureRmContext** Cmdlet 提供訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3ff38-138">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3ff38-139">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="3ff38-139">Create a resource group</span></span>
<span data-ttu-id="3ff38-140">將任何資源部署至訂用帳戶之前，您必須建立將包含該資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ff38-140">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="3ff38-141">若要建立資源群組，請使用 **New-AzureRmResourceGroup** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ff38-141">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="3ff38-142">此命令會使用 **Name** 參數來指定資源群組的名稱，並使用 **Location** 參數來指定其位置。</span><span class="sxs-lookup"><span data-stu-id="3ff38-142">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="3ff38-143">輸出的格式如下：</span><span class="sxs-lookup"><span data-stu-id="3ff38-143">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="3ff38-144">如果您稍後需要擷取資源群組，請使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="3ff38-144">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="3ff38-145">若要取得訂用帳戶中所有資源群組，請不要指定名稱：</span><span class="sxs-lookup"><span data-stu-id="3ff38-145">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="3ff38-146">將資源加入資源群組</span><span class="sxs-lookup"><span data-stu-id="3ff38-146">Add resources to a resource group</span></span>
<span data-ttu-id="3ff38-147">若要將資源加入資源群組，您可以使用 **New-AzureRmResource** Cmdlet 或是與您建立之資源類型相關的 Cmdlet (像是**New-AzureRmStorageAccount**)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-147">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="3ff38-148">您可能會發現使用與資源類型相關的 Cmdlet 會比較容易，因為它包含新資源所需的屬性參數。</span><span class="sxs-lookup"><span data-stu-id="3ff38-148">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="3ff38-149">若要使用 **New-AzureRmResource**，您必須知道要設定的所有屬性而不需經過提示。</span><span class="sxs-lookup"><span data-stu-id="3ff38-149">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="3ff38-150">不過，透過 Cmdlet 新增資源可能會造成未來的混淆，因為新的資源不在 Resource Manager 範本中。</span><span class="sxs-lookup"><span data-stu-id="3ff38-150">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="3ff38-151">Microsoft 建議在 Resource Manager 範本中定義 Azure 解決方案的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3ff38-151">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="3ff38-152">範本可讓您可靠且重複地部署您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3ff38-152">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="3ff38-153">在本主題中，您會使用 PowerShell Cmdlet 建立儲存體帳戶，但之後您會從資源群組中產生範本。</span><span class="sxs-lookup"><span data-stu-id="3ff38-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="3ff38-154">下列 Cmdlet 會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ff38-154">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="3ff38-155">請不要使用範例所顯示的名稱，而是為儲存體帳戶提供唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="3ff38-155">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="3ff38-156">名稱的長度必須介於 3 到 24 個字元，而且只能使用數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="3ff38-156">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="3ff38-157">如果使用範例所顯示的名稱，您會收到錯誤，因為該名稱已在使用中。</span><span class="sxs-lookup"><span data-stu-id="3ff38-157">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="3ff38-158">如果您稍後需要擷取此資源，請使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="3ff38-158">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="3ff38-159">新增標記</span><span class="sxs-lookup"><span data-stu-id="3ff38-159">Add a tag</span></span>

<span data-ttu-id="3ff38-160">標籤可讓您根據不同的屬性組織您的資源。</span><span class="sxs-lookup"><span data-stu-id="3ff38-160">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="3ff38-161">例如，您在不同的資源群組中可能有數個資源，屬於相同的部門。</span><span class="sxs-lookup"><span data-stu-id="3ff38-161">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="3ff38-162">您可以對這些資源套用部門標籤和值，將它們標示為屬於相同的類別目錄。</span><span class="sxs-lookup"><span data-stu-id="3ff38-162">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="3ff38-163">或者，您可以標記資源是在生產或測試環境中使用。</span><span class="sxs-lookup"><span data-stu-id="3ff38-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="3ff38-164">本主題中，您只會對一個資源套用標籤，但在您的環境中，很有可能會對所有資源套用標籤。</span><span class="sxs-lookup"><span data-stu-id="3ff38-164">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="3ff38-165">下列 Cmdlet 對您的儲存體帳戶套用兩個標籤︰</span><span class="sxs-lookup"><span data-stu-id="3ff38-165">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="3ff38-166">標籤會以一個物件的方式更新。</span><span class="sxs-lookup"><span data-stu-id="3ff38-166">Tags are updated as a single object.</span></span> <span data-ttu-id="3ff38-167">若要對已經包含標籤的資源新增標籤，請先擷取現有的標籤。</span><span class="sxs-lookup"><span data-stu-id="3ff38-167">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="3ff38-168">將新的標籤加入包含現有標籤的物件，然後對資源重新套用所有標籤。</span><span class="sxs-lookup"><span data-stu-id="3ff38-168">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="3ff38-169">搜尋資源</span><span class="sxs-lookup"><span data-stu-id="3ff38-169">Search for resources</span></span>

<span data-ttu-id="3ff38-170">使用 **Find-AzureRmResource** Cmdlet 擷取不同搜尋條件的資源。</span><span class="sxs-lookup"><span data-stu-id="3ff38-170">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="3ff38-171">若要依名稱取得資源，請提供 **ResourceNameContains** 參數︰</span><span class="sxs-lookup"><span data-stu-id="3ff38-171">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="3ff38-172">若要取得資源群組中的所有資源，請提供 **ResourceGroupNameContains** 參數︰</span><span class="sxs-lookup"><span data-stu-id="3ff38-172">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="3ff38-173">若要取得有某個標籤名稱和值的所有資源，請提供 **TagName** 和 **TagValue** 參數︰</span><span class="sxs-lookup"><span data-stu-id="3ff38-173">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="3ff38-174">若要取得有特定資源類型的所有資源，請提供 **ResourceType** 參數︰</span><span class="sxs-lookup"><span data-stu-id="3ff38-174">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="3ff38-175">鎖定資源</span><span class="sxs-lookup"><span data-stu-id="3ff38-175">Lock a resource</span></span>

<span data-ttu-id="3ff38-176">當您必須確保重要資源不會意外被刪除或修改時，就可以對資源進行鎖定。</span><span class="sxs-lookup"><span data-stu-id="3ff38-176">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="3ff38-177">您可以指定 **CanNotDelete** 或 **ReadOnly**。</span><span class="sxs-lookup"><span data-stu-id="3ff38-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="3ff38-178">若要建立或刪除管理鎖定，您必須擁有 `Microsoft.Authorization/*` 或 `Microsoft.Authorization/locks/*` 動作的存取權。</span><span class="sxs-lookup"><span data-stu-id="3ff38-178">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="3ff38-179">在內建角色中，只有「擁有者」和「使用者存取管理員」被授與這些動作的存取權。</span><span class="sxs-lookup"><span data-stu-id="3ff38-179">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="3ff38-180">若要套用鎖定，請使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="3ff38-180">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="3ff38-181">在上述範例中鎖定的資源要到鎖定移除之後才能刪除。</span><span class="sxs-lookup"><span data-stu-id="3ff38-181">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="3ff38-182">若要移除鎖定，請使用︰</span><span class="sxs-lookup"><span data-stu-id="3ff38-182">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="3ff38-183">如需設定鎖定的詳細資訊，請參閱[使用 Azure Resource Manager 鎖定資源](resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="3ff38-184">移除資源或資源群組</span><span class="sxs-lookup"><span data-stu-id="3ff38-184">Remove resources or resource group</span></span>
<span data-ttu-id="3ff38-185">您可以移除資源或資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ff38-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="3ff38-186">當您移除資源群組時，也會移除該資源群組內的所有資源。</span><span class="sxs-lookup"><span data-stu-id="3ff38-186">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="3ff38-187">若要從資源群組中刪除資源，請使用 **Remove-AzureRmResource** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ff38-187">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="3ff38-188">此 Cmdlet 會刪除資源，但不會刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ff38-188">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="3ff38-189">若要刪除資源群組及其所有資源，請使用 **Remove-AzureRmResourceGroup** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ff38-189">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="3ff38-190">這兩個 Cmdlet 都會要求您確認您想要移除資源或資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ff38-190">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="3ff38-191">如果作業成功刪除資源或資源群組，則會傳回 **True**。</span><span class="sxs-lookup"><span data-stu-id="3ff38-191">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="3ff38-192">使用 Azure 自動化執行 Resource Manager 指令碼</span><span class="sxs-lookup"><span data-stu-id="3ff38-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="3ff38-193">本主題說明如何使用 Azure PowerShell 對資源執行基本作業。</span><span class="sxs-lookup"><span data-stu-id="3ff38-193">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="3ff38-194">對於更進階的管理案例，您通常要建立指令碼，並視需要或根據排程重複使用該指令碼。</span><span class="sxs-lookup"><span data-stu-id="3ff38-194">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="3ff38-195">[Azure 自動化](../automation/automation-intro.md)提供您一種方式自動化經常使用的指令碼，管理您的 Azure 解決方案。</span><span class="sxs-lookup"><span data-stu-id="3ff38-195">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="3ff38-196">下列主題說明如何使用 Azure 自動化、Resource Manager 和 PowerShell 有效地執行管理工作︰</span><span class="sxs-lookup"><span data-stu-id="3ff38-196">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="3ff38-197">如需建立 Runbook 的相關資訊，請參閱[我的第一個 PowerShell Runbook](../automation/automation-first-runbook-textual-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="3ff38-198">如需使用指令碼資源庫的相關資訊，請參閱[Azure 自動化的 Runbook 和模組資源庫](../automation/automation-runbook-gallery.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="3ff38-199">如需啟動和停止虛擬機器的 Runbook，請參閱 [Azure 自動化案例：使用 JSON 格式化標籤來建立 Azure VM 啟動和關閉的排程](../automation/automation-scenario-start-stop-vm-wjson-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="3ff38-200">如需於下班時間啟動和停止虛擬機器的 Runbook，請參閱[於下班時間自動化啟動/停止 VM 的解決方案](../automation/automation-solution-vm-management.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ff38-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ff38-201">Next steps</span></span>
* <span data-ttu-id="3ff38-202">若要了解如何建立 Resource Manager 範本，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-202">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3ff38-203">若要了解部署範本的相關資訊，請參閱[使用 Azure Resource Manager 範本部署應用程式](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-203">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="3ff38-204">您可以將現有的資源移動到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ff38-204">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="3ff38-205">如需範例，請參閱 [將資源移至新的資源群組或訂用帳戶](resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-205">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="3ff38-206">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="3ff38-206">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

