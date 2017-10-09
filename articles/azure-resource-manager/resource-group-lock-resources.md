---
title: "aaaLock Azure 資源 tooprevent 變更 |Microsoft 文件"
description: "透過將鎖定套用到所有使用者和角色，防止使用者更新或刪除重要的 Azure 資源。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="02567-103">鎖定資源 tooprevent 突如其來的變化</span><span class="sxs-lookup"><span data-stu-id="02567-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="02567-104">身為管理員，您可能需要 toolock 訂用帳戶、 資源群組或資源 tooprevent 不小心刪除或修改重要的資源組織中其他使用者。</span><span class="sxs-lookup"><span data-stu-id="02567-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="02567-105">您可以設定 hello 鎖定層級太**CanNotDelete**或**ReadOnly**。</span><span class="sxs-lookup"><span data-stu-id="02567-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="02567-106">**CanNotDelete**表示授權的使用者仍然可以讀取和修改資源，但無法刪除 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="02567-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="02567-107">**ReadOnly**表示授權的使用者可以讀取資源，但不能刪除或更新 hello 的資源。</span><span class="sxs-lookup"><span data-stu-id="02567-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="02567-108">套用這個鎖定是所有授權使用者 toohello 權限授與的 hello 類似 toorestricting**讀取器**角色。</span><span class="sxs-lookup"><span data-stu-id="02567-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="02567-109">如何套用鎖定</span><span class="sxs-lookup"><span data-stu-id="02567-109">How locks are applied</span></span>

<span data-ttu-id="02567-110">當您套用在父範圍的鎖定時，該範圍內的所有資源都繼承 hello 相同的鎖定。</span><span class="sxs-lookup"><span data-stu-id="02567-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="02567-111">即使您稍後新增的資源會繼承 hello 父系中的 hello 鎖定。</span><span class="sxs-lookup"><span data-stu-id="02567-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="02567-112">hello hello 繼承中限制最嚴格的鎖定會優先使用。</span><span class="sxs-lookup"><span data-stu-id="02567-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="02567-113">不同於以角色為基礎的存取控制，您可以使用管理鎖定 tooapply 限制跨所有使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="02567-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="02567-114">toolearn 有關設定權限的使用者和角色，請參閱[Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="02567-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="02567-115">資源管理員鎖定套用在 hello 管理平面組成太傳送作業中發生的 toooperations`https://management.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="02567-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="02567-116">hello 鎖定不會限制資源如何執行他們自己的函式。</span><span class="sxs-lookup"><span data-stu-id="02567-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="02567-117">限制資源的變更，但沒有限制資源的作業。</span><span class="sxs-lookup"><span data-stu-id="02567-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="02567-118">例如，SQL Database 的 ReadOnly 鎖定可防止您刪除或修改 hello 資料庫，但它不會阻止您建立、 更新或刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="02567-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="02567-119">可以使用資料的交易，因為這些作業不會傳送過`https://management.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="02567-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="02567-120">套用**ReadOnly**可能會造成 toounexpected 結果，因為看起來雖然某些作業讀取作業實際需要的其他動作。</span><span class="sxs-lookup"><span data-stu-id="02567-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="02567-121">例如，放置**ReadOnly**儲存體帳戶上的鎖定可防止所有使用者列出 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="02567-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="02567-122">hello 清單索引鍵作業透過 POST 要求因為 hello 傳回索引鍵是可用的寫入作業。</span><span class="sxs-lookup"><span data-stu-id="02567-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="02567-123">如需其他範例，放置**ReadOnly** App Service 資源鎖定可防止 Visual Studio 伺服器總管顯示 hello 資源的檔案，因為互動需要寫入權限。</span><span class="sxs-lookup"><span data-stu-id="02567-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="02567-124">誰可以建立或刪除您的組織中的鎖定</span><span class="sxs-lookup"><span data-stu-id="02567-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="02567-125">toocreate 或刪除管理鎖定，您必須能夠存取太`Microsoft.Authorization/*`或`Microsoft.Authorization/locks/*`動作。</span><span class="sxs-lookup"><span data-stu-id="02567-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="02567-126">Hello 內建角色時，只有**擁有者**和**使用者存取系統管理員**授與這些動作。</span><span class="sxs-lookup"><span data-stu-id="02567-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="02567-127">入口網站</span><span class="sxs-lookup"><span data-stu-id="02567-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="02567-128">範本</span><span class="sxs-lookup"><span data-stu-id="02567-128">Template</span></span>
<span data-ttu-id="02567-129">hello 下列範例顯示建立鎖定的儲存體帳戶的範本。</span><span class="sxs-lookup"><span data-stu-id="02567-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="02567-130">hello 哪些 tooapply 當成參數提供 hello 鎖定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="02567-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="02567-131">hello hello 鎖定的名稱由串連 hello 資源名稱與**/Microsoft.Authorization/**和 hello hello 鎖定的名稱在此情況下**myLock**。</span><span class="sxs-lookup"><span data-stu-id="02567-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="02567-132">提供的 hello 型別是特定 toohello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="02567-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="02567-133">針對存放裝置，設定 hello 類型 too"Microsoft.Storage/storageaccounts/providers/locks 」。</span><span class="sxs-lookup"><span data-stu-id="02567-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="02567-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02567-134">PowerShell</span></span>
<span data-ttu-id="02567-135">您的鎖定資源使用 Azure PowerShell 使用部署的 hello[新增 AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock)命令。</span><span class="sxs-lookup"><span data-stu-id="02567-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="02567-136">toolock 資源時，提供 hello hello 資源名稱、 資源類型，以及其資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="02567-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="02567-137">資源群組、 toolock 提供 hello hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="02567-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="02567-138">鎖定時，使用的 tooget 資訊[Get AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock)。</span><span class="sxs-lookup"><span data-stu-id="02567-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="02567-139">tooget 所有 hello 鎖定您的訂閱中都使用：</span><span class="sxs-lookup"><span data-stu-id="02567-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="02567-140">tooget 所有鎖定的資源，都使用：</span><span class="sxs-lookup"><span data-stu-id="02567-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="02567-141">tooget 所有鎖定的資源群組中，都使用：</span><span class="sxs-lookup"><span data-stu-id="02567-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="02567-142">Azure PowerShell 提供其他命令工作鎖定，例如[組 AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate 鎖定，以及[移除 AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete 鎖定。</span><span class="sxs-lookup"><span data-stu-id="02567-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="02567-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="02567-143">Azure CLI</span></span>

<span data-ttu-id="02567-144">您的鎖定資源使用 Azure CLI 使用部署的 hello [az 鎖定建立](/cli/azure/lock#create)命令。</span><span class="sxs-lookup"><span data-stu-id="02567-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="02567-145">toolock 資源時，提供 hello hello 資源名稱、 資源類型，以及其資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="02567-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="02567-146">資源群組、 toolock 提供 hello hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="02567-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="02567-147">鎖定時，使用的 tooget 資訊[az 鎖定清單](/cli/azure/lock#list)。</span><span class="sxs-lookup"><span data-stu-id="02567-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="02567-148">tooget 所有 hello 鎖定您的訂閱中都使用：</span><span class="sxs-lookup"><span data-stu-id="02567-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="02567-149">tooget 所有鎖定的資源，都使用：</span><span class="sxs-lookup"><span data-stu-id="02567-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="02567-150">tooget 所有鎖定的資源群組中，都使用：</span><span class="sxs-lookup"><span data-stu-id="02567-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="02567-151">Azure CLI 提供其他命令工作鎖定，例如[az 鎖定更新](/cli/azure/lock#update)tooupdate 鎖定，以及[az 鎖定刪除](/cli/azure/lock#delete)toodelete 鎖定。</span><span class="sxs-lookup"><span data-stu-id="02567-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="02567-152">REST API</span><span class="sxs-lookup"><span data-stu-id="02567-152">REST API</span></span>
<span data-ttu-id="02567-153">您可以鎖定已部署的資源，以 hello [REST API 管理鎖定](https://docs.microsoft.com/rest/api/resources/managementlocks)。</span><span class="sxs-lookup"><span data-stu-id="02567-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="02567-154">hello REST API 可讓您 toocreate 及刪除鎖定，以及擷取現有的鎖定有關的資訊。</span><span class="sxs-lookup"><span data-stu-id="02567-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="02567-155">toocreate 鎖定，執行：</span><span class="sxs-lookup"><span data-stu-id="02567-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="02567-156">訂用帳戶、 資源群組或資源，可能是 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="02567-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="02567-157">hello 鎖定名稱是您所要的任何 toocall hello 鎖定。</span><span class="sxs-lookup"><span data-stu-id="02567-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="02567-158">對於 api-version，請使用 **2015-01-01**。</span><span class="sxs-lookup"><span data-stu-id="02567-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="02567-159">Hello 要求中包含的 JSON 物件，指定 hello hello 鎖定屬性。</span><span class="sxs-lookup"><span data-stu-id="02567-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="02567-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02567-160">Next steps</span></span>
* <span data-ttu-id="02567-161">的如需使用資源鎖定的詳細資訊，請參閱 [鎖定您的 Azure 資源](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="02567-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="02567-162">toolearn 需以邏輯方式組織您的資源，請參閱[使用標記 tooorganize 資源](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="02567-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="02567-163">toochange 哪一個資源群組資源所在，請參閱[移動資源 toonew 資源群組](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="02567-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="02567-164">您可以使用自訂原則，在訂用帳戶內套用限制和慣例。</span><span class="sxs-lookup"><span data-stu-id="02567-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="02567-165">如需詳細資訊，請參閱[使用原則 toomanage 資源和控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="02567-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="02567-166">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="02567-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

