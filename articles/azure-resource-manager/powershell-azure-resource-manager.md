---
title: "aaaManage Azure PowerShell 解決方案 |Microsoft 文件"
description: "使用 Azure PowerShell 和資源管理員 toomanage 您的資源。"
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
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="60eae-103">使用 Azure PowerShell 和 Resource Manager 管理資源</span><span class="sxs-lookup"><span data-stu-id="60eae-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60eae-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="60eae-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="60eae-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="60eae-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="60eae-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="60eae-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="60eae-107">REST API</span><span class="sxs-lookup"><span data-stu-id="60eae-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="60eae-108">在本文中，您將學習如何 toomanage 您使用 Azure PowerShell 和 Azure 資源管理員的解決方案。</span><span class="sxs-lookup"><span data-stu-id="60eae-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="60eae-109">如果您不熟悉如何使用 Resource Manager，請參閱 [Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="60eae-110">本主題著重於管理工作。</span><span class="sxs-lookup"><span data-stu-id="60eae-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="60eae-111">您將：</span><span class="sxs-lookup"><span data-stu-id="60eae-111">You will:</span></span>

1. <span data-ttu-id="60eae-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="60eae-112">Create a resource group</span></span>
2. <span data-ttu-id="60eae-113">新增資源 toohello 資源群組</span><span class="sxs-lookup"><span data-stu-id="60eae-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="60eae-114">加入標記 toohello 資源</span><span class="sxs-lookup"><span data-stu-id="60eae-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="60eae-115">根據名稱或標籤值查詢資源</span><span class="sxs-lookup"><span data-stu-id="60eae-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="60eae-116">套用和移除 hello 資源的鎖定</span><span class="sxs-lookup"><span data-stu-id="60eae-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="60eae-117">刪除資源群組</span><span class="sxs-lookup"><span data-stu-id="60eae-117">Delete a resource group</span></span>

<span data-ttu-id="60eae-118">這篇文章不會顯示如何 toodeploy 資源管理員範本 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="60eae-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="60eae-119">如需該資訊，請參閱[使用 Resource Manager 範本與 Azure PowerShell 來部署資源](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="60eae-120">開始使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="60eae-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="60eae-121">如果您尚未安裝 Azure PowerShell，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="60eae-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="60eae-122">如果您已安裝 Azure PowerShell，在過去的 hello 但近期尚未更新它，請考慮安裝 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="60eae-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="60eae-123">您可以更新 hello 版本透過 hello tooinstall 時所使用的相同方法它。</span><span class="sxs-lookup"><span data-stu-id="60eae-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="60eae-124">例如，如果您使用 Web Platform Installer hello，重新啟動，並尋找更新。</span><span class="sxs-lookup"><span data-stu-id="60eae-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="60eae-125">toocheck 您版本的 hello Azure 資源模組，使用下列 cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="60eae-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="60eae-126">本主題已針對版本 3.3.0 更新。</span><span class="sxs-lookup"><span data-stu-id="60eae-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="60eae-127">如果您有較早版本，您的體驗可能不符合本主題中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="60eae-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="60eae-128">如需有關這個版本中的 hello cmdlet 的文件，請參閱[AzureRM.Resources 模組](/powershell/module/azurerm.resources)。</span><span class="sxs-lookup"><span data-stu-id="60eae-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="60eae-129">登入 tooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="60eae-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="60eae-130">之前，先在您的方案，您必須登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="60eae-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="60eae-131">toolog tooyour Azure 帳戶，請在使用 hello**登入 AzureRmAccount** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="60eae-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="60eae-132">hello cmdlet 會提示您輸入您的 Azure 帳戶的 hello 登入認證。</span><span class="sxs-lookup"><span data-stu-id="60eae-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="60eae-133">登入之後，它會下載您的帳戶設定，這樣就可以使用 tooAzure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="60eae-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="60eae-134">hello cmdlet 會傳回您的帳戶和 hello 訂用帳戶 toouse hello 工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="60eae-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="60eae-135">如果您有多個訂用帳戶，您可以切換 tooa 不同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="60eae-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="60eae-136">首先，我們來看看您帳戶的所有 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="60eae-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="60eae-137">它會傳回啟用和停用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="60eae-137">It returns enabled and disabled subscriptions.</span></span>

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

<span data-ttu-id="60eae-138">tooswitch tooa 不同訂用帳戶，提供 hello 訂用帳戶名稱以 hello**組 AzureRmContext** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="60eae-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="60eae-139">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="60eae-139">Create a resource group</span></span>
<span data-ttu-id="60eae-140">在部署之前的任何資源 tooyour 訂閱，您必須建立資源群組將包含 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="60eae-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="60eae-141">toocreate 資源群組、 使用 hello**新增 AzureRmResourceGroup** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="60eae-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="60eae-142">hello 命令使用 hello**名稱**參數 toospecify hello 資源群組的名稱 hello**位置**參數 toospecify 其位置。</span><span class="sxs-lookup"><span data-stu-id="60eae-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="60eae-143">hello 輸出是以下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="60eae-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="60eae-144">如果您稍後需要 tooretrieve hello 資源群組，請使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="60eae-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="60eae-145">tooget 所有 hello 訂用帳戶中的資源群組中，未指定名稱：</span><span class="sxs-lookup"><span data-stu-id="60eae-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="60eae-146">新增資源 tooa 資源群組</span><span class="sxs-lookup"><span data-stu-id="60eae-146">Add resources tooa resource group</span></span>
<span data-ttu-id="60eae-147">tooadd toohello 資源群組，您可以使用 hello**新增 AzureRmResource**您所建立的 cmdlet 或指令程式來為特定 toohello 資源類型 (例如**新增 AzureRmStorageAccount**)。</span><span class="sxs-lookup"><span data-stu-id="60eae-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="60eae-148">您可能會發現它更容易 toouse 是特定 tooa 資源類型，因為它包含所需的 hello 新資源的 hello 屬性參數的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="60eae-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="60eae-149">toouse**新增 AzureRmResource**，您必須知道所有 hello 屬性 tooset 不需輸入它們。</span><span class="sxs-lookup"><span data-stu-id="60eae-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="60eae-150">不過，加入資源，以透過 cmdlet 可能會導致未來產生混淆因為 hello 新的資源不存在於 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="60eae-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="60eae-151">Microsoft 建議在 Resource Manager 範本中定義 Azure 方案的 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="60eae-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="60eae-152">範本讓您 tooreliably，而且重複地部署您的方案。</span><span class="sxs-lookup"><span data-stu-id="60eae-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="60eae-153">在本主題中，您會使用 PowerShell Cmdlet 建立儲存體帳戶，但之後您會從資源群組中產生範本。</span><span class="sxs-lookup"><span data-stu-id="60eae-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="60eae-154">hello 下列 cmdlet 會建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="60eae-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="60eae-155">而不使用 hello 名稱 hello 範例所示，提供 hello 儲存體帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="60eae-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="60eae-156">hello 名稱必須介於 3 到 24 個字元的長度，且只能使用數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="60eae-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="60eae-157">如果您使用 hello 名稱 hello 範例所示，您收到錯誤，因為該名稱已在使用中。</span><span class="sxs-lookup"><span data-stu-id="60eae-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="60eae-158">如果您需要 tooretrieve 此資源之後，使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="60eae-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="60eae-159">新增標記</span><span class="sxs-lookup"><span data-stu-id="60eae-159">Add a tag</span></span>

<span data-ttu-id="60eae-160">標籤可讓您 tooorganize toodifferent 屬性，根據您的資源。</span><span class="sxs-lookup"><span data-stu-id="60eae-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="60eae-161">例如，您可能有數個資源 toohello 屬於不同的資源群組中相同的部門。</span><span class="sxs-lookup"><span data-stu-id="60eae-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="60eae-162">您可以套用部門 toothose 資源標記和值 toomark 它們隸屬 toohello 為相同類別目錄。</span><span class="sxs-lookup"><span data-stu-id="60eae-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="60eae-163">或者，您可以標記資源是在生產或測試環境中使用。</span><span class="sxs-lookup"><span data-stu-id="60eae-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="60eae-164">在本主題中，您套用標記 tooonly 一個資源，但您的環境中最有可能是合理 tooapply 標記 tooall 您的資源。</span><span class="sxs-lookup"><span data-stu-id="60eae-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="60eae-165">hello 下列 cmdlet 適用於兩個標記 tooyour 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="60eae-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="60eae-166">標籤會以一個物件的方式更新。</span><span class="sxs-lookup"><span data-stu-id="60eae-166">Tags are updated as a single object.</span></span> <span data-ttu-id="60eae-167">tooadd 標記 tooa 資源已包含標記，首先抓取 hello 現有的標記。</span><span class="sxs-lookup"><span data-stu-id="60eae-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="60eae-168">新增 hello 新標記 toohello 物件，其中包含 hello 現有的標記，並重新套用所有 hello 標記 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="60eae-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="60eae-169">搜尋資源</span><span class="sxs-lookup"><span data-stu-id="60eae-169">Search for resources</span></span>

<span data-ttu-id="60eae-170">使用 hello**尋找 AzureRmResource** cmdlet tooretrieve 不同的搜尋條件的資源。</span><span class="sxs-lookup"><span data-stu-id="60eae-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="60eae-171">tooget 依名稱、 資源提供 hello **ResourceNameContains**參數：</span><span class="sxs-lookup"><span data-stu-id="60eae-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="60eae-172">tooget 在資源群組中，所有的 hello 資源提供 hello **ResourceGroupNameContains**參數：</span><span class="sxs-lookup"><span data-stu-id="60eae-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="60eae-173">tooget 使用標記名稱和值，所有的 hello 資源提供 hello **TagName**和**TagValue**參數：</span><span class="sxs-lookup"><span data-stu-id="60eae-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="60eae-174">tooall hello 資源的特定資源類型，提供 hello **ResourceType**參數：</span><span class="sxs-lookup"><span data-stu-id="60eae-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="60eae-175">鎖定資源</span><span class="sxs-lookup"><span data-stu-id="60eae-175">Lock a resource</span></span>

<span data-ttu-id="60eae-176">當您需要確定重要的資源不會意外刪除或修改 toomake 時，套用鎖定 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="60eae-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="60eae-177">您可以指定 **CanNotDelete** 或 **ReadOnly**。</span><span class="sxs-lookup"><span data-stu-id="60eae-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="60eae-178">toocreate 或刪除管理鎖定，您必須能夠存取太`Microsoft.Authorization/*`或`Microsoft.Authorization/locks/*`動作。</span><span class="sxs-lookup"><span data-stu-id="60eae-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="60eae-179">Hello 內建角色中，只有擁有者和使用者存取系統管理員會授與這些動作。</span><span class="sxs-lookup"><span data-stu-id="60eae-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="60eae-180">tooapply 鎖定，請使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="60eae-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="60eae-181">hello hello 前面範例中的鎖定的資源，才能刪除移除 hello 鎖定為止。</span><span class="sxs-lookup"><span data-stu-id="60eae-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="60eae-182">tooremove 鎖定，請使用：</span><span class="sxs-lookup"><span data-stu-id="60eae-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="60eae-183">如需設定鎖定的詳細資訊，請參閱[使用 Azure Resource Manager 鎖定資源](resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="60eae-184">移除資源或資源群組</span><span class="sxs-lookup"><span data-stu-id="60eae-184">Remove resources or resource group</span></span>
<span data-ttu-id="60eae-185">您可以移除資源或資源群組。</span><span class="sxs-lookup"><span data-stu-id="60eae-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="60eae-186">當您移除資源群組時，也會移除該資源群組中的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="60eae-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="60eae-187">將資源從 hello 資源群組中，使用 hello toodelete**移除 AzureRmResource** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="60eae-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="60eae-188">這個指令程式刪除 hello 資源，但不會刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="60eae-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="60eae-189">toodelete 資源群組和其所有資源，使用 hello**移除 AzureRmResourceGroup** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="60eae-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="60eae-190">針對這兩個 cmdlet，系統會要求您 tooconfirm 且想 tooremove hello 資源或資源群組。</span><span class="sxs-lookup"><span data-stu-id="60eae-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="60eae-191">如果 hello 作業已成功刪除 hello 資源或資源群組，它會傳回**True**。</span><span class="sxs-lookup"><span data-stu-id="60eae-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="60eae-192">使用 Azure 自動化執行 Resource Manager 指令碼</span><span class="sxs-lookup"><span data-stu-id="60eae-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="60eae-193">本主題說明如何使用 Azure PowerShell 資源的 tooperform 基本作業。</span><span class="sxs-lookup"><span data-stu-id="60eae-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="60eae-194">更進階的管理案例，您通常會想 toocreate 指令碼，而且重複使用該指令碼，視需要或依排程。</span><span class="sxs-lookup"><span data-stu-id="60eae-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="60eae-195">[Azure 自動化](../automation/automation-intro.md)提供一個方法，讓您管理 Azure 解決方案的常用 tooautomate 指令碼。</span><span class="sxs-lookup"><span data-stu-id="60eae-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="60eae-196">hello 下列主題將示範如何 toouse Azure 自動化中，資源管理員和 PowerShell tooeffectively 執行管理工作：</span><span class="sxs-lookup"><span data-stu-id="60eae-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="60eae-197">如需建立 Runbook 的相關資訊，請參閱[我的第一個 PowerShell Runbook](../automation/automation-first-runbook-textual-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="60eae-198">如需使用指令碼資源庫的相關資訊，請參閱[Azure 自動化的 Runbook 和模組資源庫](../automation/automation-runbook-gallery.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="60eae-199">啟動和停止虛擬機器的 runbook，請參閱[Azure 自動化案例： 使用 JSON 格式的標記 toocreate Azure VM 啟動或關閉排程](../automation/automation-scenario-start-stop-vm-wjson-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="60eae-200">如需於下班時間啟動和停止虛擬機器的 Runbook，請參閱[於下班時間自動化啟動/停止 VM 的解決方案](../automation/automation-solution-vm-management.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60eae-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60eae-201">Next steps</span></span>
* <span data-ttu-id="60eae-202">toolearn 有關建立資源管理員範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="60eae-203">toolearn 有關部署範本，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="60eae-204">您可以移動現有資源 tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="60eae-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="60eae-205">如需範例，請參閱[移動資源 tooNew 資源群組或訂用帳戶](resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="60eae-206">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="60eae-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

