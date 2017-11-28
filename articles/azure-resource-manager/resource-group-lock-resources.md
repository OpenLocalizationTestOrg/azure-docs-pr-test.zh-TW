---
title: "鎖定 Azure 資源以防止變更 | Microsoft Docs"
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
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="dcb07-103">鎖定資源以防止非預期的變更</span><span class="sxs-lookup"><span data-stu-id="dcb07-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="dcb07-104">身為系統管理員，您可能需要鎖定訂用帳戶、資源群組或資源，以防止組織中的其他使用者不小心刪除或修改重要資源。</span><span class="sxs-lookup"><span data-stu-id="dcb07-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="dcb07-105">您可以將鎖定層級設定為 **CanNotDelete** 或 **ReadOnly**。</span><span class="sxs-lookup"><span data-stu-id="dcb07-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="dcb07-106">**CanNotDelete** 表示經過授權的使用者仍然可以讀取和修改資源，但無法刪除資源。</span><span class="sxs-lookup"><span data-stu-id="dcb07-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="dcb07-107">**ReadOnly** 表示經過授權的使用者可以讀取資源，但無法刪除或更新資源。</span><span class="sxs-lookup"><span data-stu-id="dcb07-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="dcb07-108">套用這個鎖定類似於限制所有經過授權使用者的權限是由「讀取者」角色所授與。</span><span class="sxs-lookup"><span data-stu-id="dcb07-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="dcb07-109">如何套用鎖定</span><span class="sxs-lookup"><span data-stu-id="dcb07-109">How locks are applied</span></span>

<span data-ttu-id="dcb07-110">當您在父範圍套用鎖定時，該範圍內的所有資源都會都繼承相同的鎖定。</span><span class="sxs-lookup"><span data-stu-id="dcb07-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="dcb07-111">甚至您稍後新增的資源都會繼承父項的鎖定。</span><span class="sxs-lookup"><span data-stu-id="dcb07-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="dcb07-112">繼承中限制最嚴格的鎖定優先順序最高。</span><span class="sxs-lookup"><span data-stu-id="dcb07-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="dcb07-113">不同於角色型存取控制，您可以使用管理鎖定來對所有使用者和角色套用限制。</span><span class="sxs-lookup"><span data-stu-id="dcb07-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="dcb07-114">如要了解使用者和角色的設定權限，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="dcb07-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="dcb07-115">Resource Manager 鎖定只會套用於管理平面發生的作業，亦即要傳送至 `https://management.azure.com` 的作業。</span><span class="sxs-lookup"><span data-stu-id="dcb07-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="dcb07-116">鎖定並不會限制資源執行自己函式的方式。</span><span class="sxs-lookup"><span data-stu-id="dcb07-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="dcb07-117">限制資源的變更，但沒有限制資源的作業。</span><span class="sxs-lookup"><span data-stu-id="dcb07-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="dcb07-118">例如，SQL 資料庫的 ReadOnly 鎖定會防止您刪除或修改資料庫，但它不會阻止您建立、更新或刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="dcb07-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="dcb07-119">允許資料的交易，因為這些作業不會傳送到 `https://management.azure.com`。</span><span class="sxs-lookup"><span data-stu-id="dcb07-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="dcb07-120">套用 **ReadOnly** 會導致無法預期的結果，因為有些看似讀取作業的作業實際上需要其他動作。</span><span class="sxs-lookup"><span data-stu-id="dcb07-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="dcb07-121">例如，將 **ReadOnly** 鎖定放置在儲存體帳戶上，會防止所有使用者列出金鑰。</span><span class="sxs-lookup"><span data-stu-id="dcb07-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="dcb07-122">清單金鑰作業是透過 POST 要求進行處理，因為傳回的金鑰可用於寫入作業。</span><span class="sxs-lookup"><span data-stu-id="dcb07-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="dcb07-123">至於其他範例，將 **ReadOnly** 鎖定放置在 App Service 資源，會防止 Visual Studio 伺服器總管顯示資源的檔案，因為該互動需要寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="dcb07-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="dcb07-124">誰可以建立或刪除您的組織中的鎖定</span><span class="sxs-lookup"><span data-stu-id="dcb07-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="dcb07-125">若要建立或刪除管理鎖定，您必須擁有 `Microsoft.Authorization/*` 或 `Microsoft.Authorization/locks/*` 動作的存取權。</span><span class="sxs-lookup"><span data-stu-id="dcb07-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="dcb07-126">在內建角色中，只有 **擁有者** 和 **使用者存取管理員** 被授與這些動作的存取權。</span><span class="sxs-lookup"><span data-stu-id="dcb07-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="dcb07-127">入口網站</span><span class="sxs-lookup"><span data-stu-id="dcb07-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="dcb07-128">範本</span><span class="sxs-lookup"><span data-stu-id="dcb07-128">Template</span></span>
<span data-ttu-id="dcb07-129">以下範例顯示的範本會在儲存體帳戶建立鎖定。</span><span class="sxs-lookup"><span data-stu-id="dcb07-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="dcb07-130">要套用鎖定的儲存體帳戶會提供作為參數。</span><span class="sxs-lookup"><span data-stu-id="dcb07-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="dcb07-131">鎖定名稱的建立方式是串連資源名稱與 **/Microsoft.Authorization/**，而在此案例中，鎖定名稱為 **myLock**。</span><span class="sxs-lookup"><span data-stu-id="dcb07-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="dcb07-132">必須依資源型別提供型別。</span><span class="sxs-lookup"><span data-stu-id="dcb07-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="dcb07-133">若是儲存體，將型別設定為 "Microsoft.Storage/storageaccounts/providers/locks"。</span><span class="sxs-lookup"><span data-stu-id="dcb07-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="dcb07-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcb07-134">PowerShell</span></span>
<span data-ttu-id="dcb07-135">您可以使用 [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) 命令，利用 Azure PowerShell 來鎖定已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="dcb07-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="dcb07-136">若要鎖定資源，請提供資源的名稱、其資源類型，以及其資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="dcb07-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="dcb07-137">若要鎖定資源群組，請提供資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="dcb07-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="dcb07-138">若要取得鎖定的相關資訊，請使用 [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock)。</span><span class="sxs-lookup"><span data-stu-id="dcb07-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="dcb07-139">若要取得訂用帳戶中的所有鎖定，請使用︰</span><span class="sxs-lookup"><span data-stu-id="dcb07-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="dcb07-140">若要取得資源的所有鎖定，請使用︰</span><span class="sxs-lookup"><span data-stu-id="dcb07-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="dcb07-141">若要取得資源群組的所有鎖定，請使用︰</span><span class="sxs-lookup"><span data-stu-id="dcb07-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="dcb07-142">Azure PowerShell 可為使用中的鎖定提供其他命令，例如可更新鎖定的 [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock)，以及可刪除鎖定的 [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock)。</span><span class="sxs-lookup"><span data-stu-id="dcb07-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="dcb07-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dcb07-143">Azure CLI</span></span>

<span data-ttu-id="dcb07-144">您可使用 [az lock create](/cli/azure/lock#create) 命令，透過 Azure CLI 來鎖定已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="dcb07-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="dcb07-145">若要鎖定資源，請提供資源的名稱、其資源類型，以及其資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="dcb07-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="dcb07-146">若要鎖定資源群組，請提供資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="dcb07-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="dcb07-147">若要取得鎖定的相關資訊，請使用 [az lock list](/cli/azure/lock#list)。</span><span class="sxs-lookup"><span data-stu-id="dcb07-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="dcb07-148">若要取得訂用帳戶中的所有鎖定，請使用︰</span><span class="sxs-lookup"><span data-stu-id="dcb07-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="dcb07-149">若要取得資源的所有鎖定，請使用︰</span><span class="sxs-lookup"><span data-stu-id="dcb07-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="dcb07-150">若要取得資源群組的所有鎖定，請使用︰</span><span class="sxs-lookup"><span data-stu-id="dcb07-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="dcb07-151">Azure CLI 可為使用中的鎖定提供其他命令，例如可更新鎖定的 [az lock update](/cli/azure/lock#update)，以及可刪除鎖定的 [az lock delete](/cli/azure/lock#delete)。</span><span class="sxs-lookup"><span data-stu-id="dcb07-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="dcb07-152">REST API</span><span class="sxs-lookup"><span data-stu-id="dcb07-152">REST API</span></span>
<span data-ttu-id="dcb07-153">您可以使用[管理鎖定的 REST API](https://docs.microsoft.com/rest/api/resources/managementlocks)，來鎖定已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="dcb07-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="dcb07-154">此 REST API 可讓您建立及刪除鎖定，以及抓取現有鎖定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="dcb07-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="dcb07-155">若要建立鎖定，請執行：</span><span class="sxs-lookup"><span data-stu-id="dcb07-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="dcb07-156">範圍可以是訂用帳戶、資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="dcb07-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="dcb07-157">lock-name 是您想要命名鎖定的任何名稱。</span><span class="sxs-lookup"><span data-stu-id="dcb07-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="dcb07-158">對於 api-version，請使用 **2015-01-01**。</span><span class="sxs-lookup"><span data-stu-id="dcb07-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="dcb07-159">在要求中，包含指定鎖定屬性的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="dcb07-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="dcb07-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dcb07-160">Next steps</span></span>
* <span data-ttu-id="dcb07-161">的如需使用資源鎖定的詳細資訊，請參閱 [鎖定您的 Azure 資源](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="dcb07-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="dcb07-162">若要了解如何邏輯地組織您的資源，請參閱 [使用標記來組織您的資源](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="dcb07-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="dcb07-163">若要變更資源所在的資源群組，請參閱 [將資源移動到新的資源群組](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="dcb07-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="dcb07-164">您可以使用自訂原則，在訂用帳戶內套用限制和慣例。</span><span class="sxs-lookup"><span data-stu-id="dcb07-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="dcb07-165">如需詳細資訊，請參閱 [使用原則來管理資源和控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="dcb07-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="dcb07-166">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="dcb07-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

