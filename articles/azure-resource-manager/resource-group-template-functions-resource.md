---
title: "aaaAzure 資源管理員範本函式-資源 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 tooretrieve 值中的 hello 函式 toouse 相關資源。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="a90fc-103">Azure Resource Manager 範本的資源函式</span><span class="sxs-lookup"><span data-stu-id="a90fc-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="a90fc-104">資源管理員提供下列函數來取得資源值 hello:</span><span class="sxs-lookup"><span data-stu-id="a90fc-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="a90fc-105">listKeys 和 list{Value}</span><span class="sxs-lookup"><span data-stu-id="a90fc-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="a90fc-106">提供者</span><span class="sxs-lookup"><span data-stu-id="a90fc-106">providers</span></span>](#providers)
* [<span data-ttu-id="a90fc-107">reference</span><span class="sxs-lookup"><span data-stu-id="a90fc-107">reference</span></span>](#reference)
* [<span data-ttu-id="a90fc-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="a90fc-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="a90fc-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="a90fc-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="a90fc-110">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a90fc-110">subscription</span></span>](#subscription)

<span data-ttu-id="a90fc-111">tooget 值參數、 變數或 hello 目前部署中，請參閱[部署值函式](resource-group-template-functions-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a90fc-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="a90fc-112">listKeys 和 list{Value}</span><span class="sxs-lookup"><span data-stu-id="a90fc-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="a90fc-113">傳回 hello 任何支援 hello 清單作業的資源類型的值。</span><span class="sxs-lookup"><span data-stu-id="a90fc-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="a90fc-114">hello 最常見的用法是`listKeys`。</span><span class="sxs-lookup"><span data-stu-id="a90fc-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="a90fc-115">參數</span><span class="sxs-lookup"><span data-stu-id="a90fc-115">Parameters</span></span>

| <span data-ttu-id="a90fc-116">參數</span><span class="sxs-lookup"><span data-stu-id="a90fc-116">Parameter</span></span> | <span data-ttu-id="a90fc-117">必要</span><span class="sxs-lookup"><span data-stu-id="a90fc-117">Required</span></span> | <span data-ttu-id="a90fc-118">類型</span><span class="sxs-lookup"><span data-stu-id="a90fc-118">Type</span></span> | <span data-ttu-id="a90fc-119">說明</span><span class="sxs-lookup"><span data-stu-id="a90fc-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a90fc-120">resourceName 或 resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="a90fc-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="a90fc-121">是</span><span class="sxs-lookup"><span data-stu-id="a90fc-121">Yes</span></span> |<span data-ttu-id="a90fc-122">字串</span><span class="sxs-lookup"><span data-stu-id="a90fc-122">string</span></span> |<span data-ttu-id="a90fc-123">Hello 資源的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a90fc-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="a90fc-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a90fc-124">apiVersion</span></span> |<span data-ttu-id="a90fc-125">是</span><span class="sxs-lookup"><span data-stu-id="a90fc-125">Yes</span></span> |<span data-ttu-id="a90fc-126">字串</span><span class="sxs-lookup"><span data-stu-id="a90fc-126">string</span></span> |<span data-ttu-id="a90fc-127">資源執行階段狀態的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="a90fc-127">API version of resource runtime state.</span></span> <span data-ttu-id="a90fc-128">一般來說，在 hello 格式**yyyy-mm-dd**。</span><span class="sxs-lookup"><span data-stu-id="a90fc-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a90fc-129">傳回值</span><span class="sxs-lookup"><span data-stu-id="a90fc-129">Return value</span></span>

<span data-ttu-id="a90fc-130">hello 傳回來自 Listkey 物件具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="a90fc-130">hello returned object from listKeys has hello following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="a90fc-131">其他 list 函式具有不同的傳回格式。</span><span class="sxs-lookup"><span data-stu-id="a90fc-131">Other list functions have different return formats.</span></span> <span data-ttu-id="a90fc-132">在函式、 toosee hello 格式包含在 hello 輸出區段 hello 範例範本中所示。</span><span class="sxs-lookup"><span data-stu-id="a90fc-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="a90fc-133">備註</span><span class="sxs-lookup"><span data-stu-id="a90fc-133">Remarks</span></span>

<span data-ttu-id="a90fc-134">開頭為 **list** 的任何作業都可在您的範本中用為函式。</span><span class="sxs-lookup"><span data-stu-id="a90fc-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="a90fc-135">hello 可用的作業包括不僅 Listkey，但等作業也`list`， `listAdminKeys`，和`listStatus`。</span><span class="sxs-lookup"><span data-stu-id="a90fc-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="a90fc-136">不過，您無法使用**清單**需要在 hello 中的值的作業要求本文。</span><span class="sxs-lookup"><span data-stu-id="a90fc-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="a90fc-137">比方說，hello[清單帳戶 SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS)作業需要要求主體參數喜歡*signedExpiry*，因此您無法在樣板內使用它。</span><span class="sxs-lookup"><span data-stu-id="a90fc-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="a90fc-138">toodetermine 哪些資源類型都有清單作業，您有下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="a90fc-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="a90fc-139">檢視 hello [REST API 作業](/rest/api/)資源提供者，以及尋找清單作業。</span><span class="sxs-lookup"><span data-stu-id="a90fc-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="a90fc-140">例如，儲存體帳戶有 hello [Listkey 作業](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys)。</span><span class="sxs-lookup"><span data-stu-id="a90fc-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="a90fc-141">使用 hello [Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a90fc-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="a90fc-142">hello 下列範例會取得所有儲存體帳戶的清單作業：</span><span class="sxs-lookup"><span data-stu-id="a90fc-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="a90fc-143">使用下列 Azure CLI 命令 toofilter 只 hello 列出作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="a90fc-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="a90fc-144">使用任一個 hello 指定 hello 資源[resourceId 函數](#resourceid)，或 hello 格式`{providerNamespace}/{resourceType}/{resourceName}`。</span><span class="sxs-lookup"><span data-stu-id="a90fc-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="a90fc-145">範例</span><span class="sxs-lookup"><span data-stu-id="a90fc-145">Example</span></span>

<span data-ttu-id="a90fc-146">hello 下列範例顯示如何 tooreturn hello 主要和次要金鑰從 hello 的儲存體帳戶會輸出一節。</span><span class="sxs-lookup"><span data-stu-id="a90fc-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="a90fc-147">提供者</span><span class="sxs-lookup"><span data-stu-id="a90fc-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="a90fc-148">傳回資源提供者和其所支援資源類型的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a90fc-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="a90fc-149">如果您未提供資源類型，hello 函式會傳回所有支援的 hello 型別 hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="a90fc-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="a90fc-150">參數</span><span class="sxs-lookup"><span data-stu-id="a90fc-150">Parameters</span></span>

| <span data-ttu-id="a90fc-151">參數</span><span class="sxs-lookup"><span data-stu-id="a90fc-151">Parameter</span></span> | <span data-ttu-id="a90fc-152">必要</span><span class="sxs-lookup"><span data-stu-id="a90fc-152">Required</span></span> | <span data-ttu-id="a90fc-153">類型</span><span class="sxs-lookup"><span data-stu-id="a90fc-153">Type</span></span> | <span data-ttu-id="a90fc-154">說明</span><span class="sxs-lookup"><span data-stu-id="a90fc-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a90fc-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="a90fc-155">providerNamespace</span></span> |<span data-ttu-id="a90fc-156">是</span><span class="sxs-lookup"><span data-stu-id="a90fc-156">Yes</span></span> |<span data-ttu-id="a90fc-157">字串</span><span class="sxs-lookup"><span data-stu-id="a90fc-157">string</span></span> |<span data-ttu-id="a90fc-158">Hello 提供者命名空間</span><span class="sxs-lookup"><span data-stu-id="a90fc-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="a90fc-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="a90fc-159">resourceType</span></span> |<span data-ttu-id="a90fc-160">否</span><span class="sxs-lookup"><span data-stu-id="a90fc-160">No</span></span> |<span data-ttu-id="a90fc-161">字串</span><span class="sxs-lookup"><span data-stu-id="a90fc-161">string</span></span> |<span data-ttu-id="a90fc-162">指定命名空間內 hello 資源 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="a90fc-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a90fc-163">傳回值</span><span class="sxs-lookup"><span data-stu-id="a90fc-163">Return value</span></span>

<span data-ttu-id="a90fc-164">每個支援的型別會傳回在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="a90fc-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="a90fc-165">Hello 排序陣列傳回不保證值。</span><span class="sxs-lookup"><span data-stu-id="a90fc-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="a90fc-166">範例</span><span class="sxs-lookup"><span data-stu-id="a90fc-166">Example</span></span>

<span data-ttu-id="a90fc-167">hello 下列範例顯示如何 toouse hello 提供者函式：</span><span class="sxs-lookup"><span data-stu-id="a90fc-167">hello following example shows how toouse hello provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="a90fc-168">hello 上述範例會傳回物件中 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="a90fc-168">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="a90fc-169">reference</span><span class="sxs-lookup"><span data-stu-id="a90fc-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="a90fc-170">傳回代表資源執行階段狀態的物件。</span><span class="sxs-lookup"><span data-stu-id="a90fc-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="a90fc-171">參數</span><span class="sxs-lookup"><span data-stu-id="a90fc-171">Parameters</span></span>

| <span data-ttu-id="a90fc-172">參數</span><span class="sxs-lookup"><span data-stu-id="a90fc-172">Parameter</span></span> | <span data-ttu-id="a90fc-173">必要</span><span class="sxs-lookup"><span data-stu-id="a90fc-173">Required</span></span> | <span data-ttu-id="a90fc-174">類型</span><span class="sxs-lookup"><span data-stu-id="a90fc-174">Type</span></span> | <span data-ttu-id="a90fc-175">說明</span><span class="sxs-lookup"><span data-stu-id="a90fc-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a90fc-176">resourceName 或 resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="a90fc-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="a90fc-177">是</span><span class="sxs-lookup"><span data-stu-id="a90fc-177">Yes</span></span> |<span data-ttu-id="a90fc-178">string</span><span class="sxs-lookup"><span data-stu-id="a90fc-178">string</span></span> |<span data-ttu-id="a90fc-179">資源的名稱或唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a90fc-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="a90fc-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a90fc-180">apiVersion</span></span> |<span data-ttu-id="a90fc-181">否</span><span class="sxs-lookup"><span data-stu-id="a90fc-181">No</span></span> |<span data-ttu-id="a90fc-182">字串</span><span class="sxs-lookup"><span data-stu-id="a90fc-182">string</span></span> |<span data-ttu-id="a90fc-183">API 版的 hello 指定的資源。</span><span class="sxs-lookup"><span data-stu-id="a90fc-183">API version of hello specified resource.</span></span> <span data-ttu-id="a90fc-184">Hello 資源不會提供相同的範本中時包含此參數。</span><span class="sxs-lookup"><span data-stu-id="a90fc-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="a90fc-185">一般來說，在 hello 格式**yyyy-mm-dd**。</span><span class="sxs-lookup"><span data-stu-id="a90fc-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a90fc-186">傳回值</span><span class="sxs-lookup"><span data-stu-id="a90fc-186">Return value</span></span>

<span data-ttu-id="a90fc-187">每個資源類型傳回 hello 參考函式的不同屬性。</span><span class="sxs-lookup"><span data-stu-id="a90fc-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="a90fc-188">hello 函式不會傳回單一的預先定義的格式。</span><span class="sxs-lookup"><span data-stu-id="a90fc-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="a90fc-189">資源類型，toosee hello 屬性傳回 hello 中的 hello 物件輸出區段中 hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="a90fc-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="a90fc-190">備註</span><span class="sxs-lookup"><span data-stu-id="a90fc-190">Remarks</span></span>

<span data-ttu-id="a90fc-191">hello 參考函式衍生其值從執行階段的狀態，並因此不能用在 hello 變數區段。</span><span class="sxs-lookup"><span data-stu-id="a90fc-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="a90fc-192">它可以用於範本的 outputs 區段中。</span><span class="sxs-lookup"><span data-stu-id="a90fc-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="a90fc-193">利用 hello 參考的函式，您隱含地宣告一個資源依存於另一個資源如果 hello 參考資源相同的範本內佈建。</span><span class="sxs-lookup"><span data-stu-id="a90fc-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="a90fc-194">您不需要 tooalso 使用 hello dependsOn 屬性。</span><span class="sxs-lookup"><span data-stu-id="a90fc-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="a90fc-195">hello 函式之前不會評估 hello 參照的資源已完成部署。</span><span class="sxs-lookup"><span data-stu-id="a90fc-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="a90fc-196">toosee hello 屬性名稱和值的資源類型，建立傳回 hello 輸出區段中的 hello 物件的範本。</span><span class="sxs-lookup"><span data-stu-id="a90fc-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="a90fc-197">如果您有現有的資源，該類型時，您的範本會傳回 hello 物件而不會部署任何新的資源。</span><span class="sxs-lookup"><span data-stu-id="a90fc-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="a90fc-198">一般而言，您可以使用 hello**參考**函式 tooreturn 特定值的物件，例如 hello blob 端點 URI 或完整的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="a90fc-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="a90fc-199">範例</span><span class="sxs-lookup"><span data-stu-id="a90fc-199">Example</span></span>

<span data-ttu-id="a90fc-200">hello toodeploy 和參考 hello 資源相同的範本，使用：</span><span class="sxs-lookup"><span data-stu-id="a90fc-200">toodeploy and reference hello resource in hello same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="a90fc-201">hello 上述範例會傳回物件中 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="a90fc-201">hello preceding example returns an object in hello following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="a90fc-202">hello 下列範例會參考未部署此範本中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a90fc-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="a90fc-203">hello 儲存體帳戶已經存在於 hello 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="a90fc-203">hello storage account already exists within hello same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="a90fc-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="a90fc-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="a90fc-205">傳回代表 hello 目前的資源群組的物件。</span><span class="sxs-lookup"><span data-stu-id="a90fc-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="a90fc-206">傳回值</span><span class="sxs-lookup"><span data-stu-id="a90fc-206">Return value</span></span>

<span data-ttu-id="a90fc-207">hello 傳回的物件處於 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="a90fc-207">hello returned object is in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="a90fc-208">備註</span><span class="sxs-lookup"><span data-stu-id="a90fc-208">Remarks</span></span>

<span data-ttu-id="a90fc-209">Hello resourceGroup 函式的常見用法是在 hello toocreate 資源與 hello 資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="a90fc-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="a90fc-210">hello 下列範例會使用 hello 資源群組位置 tooassign hello 位置的網站。</span><span class="sxs-lookup"><span data-stu-id="a90fc-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="a90fc-211">範例</span><span class="sxs-lookup"><span data-stu-id="a90fc-211">Example</span></span>

<span data-ttu-id="a90fc-212">hello 下列範本會傳回 hello hello 資源群組的屬性。</span><span class="sxs-lookup"><span data-stu-id="a90fc-212">hello following template returns hello properties of hello resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="a90fc-213">hello 上述範例會傳回物件中 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="a90fc-213">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="a90fc-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="a90fc-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="a90fc-215">傳回 hello 資源的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a90fc-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="a90fc-216">Hello 資源名稱模稜兩可或 hello 內不會佈建時，會使用此函式相同的範本。</span><span class="sxs-lookup"><span data-stu-id="a90fc-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="a90fc-217">參數</span><span class="sxs-lookup"><span data-stu-id="a90fc-217">Parameters</span></span>

| <span data-ttu-id="a90fc-218">參數</span><span class="sxs-lookup"><span data-stu-id="a90fc-218">Parameter</span></span> | <span data-ttu-id="a90fc-219">必要</span><span class="sxs-lookup"><span data-stu-id="a90fc-219">Required</span></span> | <span data-ttu-id="a90fc-220">類型</span><span class="sxs-lookup"><span data-stu-id="a90fc-220">Type</span></span> | <span data-ttu-id="a90fc-221">說明</span><span class="sxs-lookup"><span data-stu-id="a90fc-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a90fc-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a90fc-222">subscriptionId</span></span> |<span data-ttu-id="a90fc-223">否</span><span class="sxs-lookup"><span data-stu-id="a90fc-223">No</span></span> |<span data-ttu-id="a90fc-224">字串 (GUID 格式)</span><span class="sxs-lookup"><span data-stu-id="a90fc-224">string (In GUID format)</span></span> |<span data-ttu-id="a90fc-225">預設值為 hello 目前訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a90fc-225">Default value is hello current subscription.</span></span> <span data-ttu-id="a90fc-226">當您需要 tooretrieve 其他訂用帳戶中的資源時，請指定這個值。</span><span class="sxs-lookup"><span data-stu-id="a90fc-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="a90fc-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="a90fc-227">resourceGroupName</span></span> |<span data-ttu-id="a90fc-228">否</span><span class="sxs-lookup"><span data-stu-id="a90fc-228">No</span></span> |<span data-ttu-id="a90fc-229">字串</span><span class="sxs-lookup"><span data-stu-id="a90fc-229">string</span></span> |<span data-ttu-id="a90fc-230">預設值為目前資源群組。</span><span class="sxs-lookup"><span data-stu-id="a90fc-230">Default value is current resource group.</span></span> <span data-ttu-id="a90fc-231">當您需要 tooretrieve 另一個資源群組中的資源時，請指定這個值。</span><span class="sxs-lookup"><span data-stu-id="a90fc-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="a90fc-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="a90fc-232">resourceType</span></span> |<span data-ttu-id="a90fc-233">是</span><span class="sxs-lookup"><span data-stu-id="a90fc-233">Yes</span></span> |<span data-ttu-id="a90fc-234">字串</span><span class="sxs-lookup"><span data-stu-id="a90fc-234">string</span></span> |<span data-ttu-id="a90fc-235">資源的類型 (包括資源提供者命名空間)。</span><span class="sxs-lookup"><span data-stu-id="a90fc-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="a90fc-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="a90fc-236">resourceName1</span></span> |<span data-ttu-id="a90fc-237">是</span><span class="sxs-lookup"><span data-stu-id="a90fc-237">Yes</span></span> |<span data-ttu-id="a90fc-238">string</span><span class="sxs-lookup"><span data-stu-id="a90fc-238">string</span></span> |<span data-ttu-id="a90fc-239">資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="a90fc-239">Name of resource.</span></span> |
| <span data-ttu-id="a90fc-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="a90fc-240">resourceName2</span></span> |<span data-ttu-id="a90fc-241">否</span><span class="sxs-lookup"><span data-stu-id="a90fc-241">No</span></span> |<span data-ttu-id="a90fc-242">string</span><span class="sxs-lookup"><span data-stu-id="a90fc-242">string</span></span> |<span data-ttu-id="a90fc-243">如果是巢狀資源，則為下一個資源名稱區段。</span><span class="sxs-lookup"><span data-stu-id="a90fc-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="a90fc-244">傳回值</span><span class="sxs-lookup"><span data-stu-id="a90fc-244">Return value</span></span>

<span data-ttu-id="a90fc-245">hello 識別碼會傳入 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="a90fc-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="a90fc-246">備註</span><span class="sxs-lookup"><span data-stu-id="a90fc-246">Remarks</span></span>

<span data-ttu-id="a90fc-247">hello 參數所指定的值取決於 hello 資源是在 hello 與 hello 目前部署的相同訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="a90fc-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="a90fc-248">tooget hello 資源識別碼 hello 的儲存體帳戶的相同訂用帳戶和資源群組中，使用：</span><span class="sxs-lookup"><span data-stu-id="a90fc-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="a90fc-249">儲存體帳戶中的 tooget hello 資源識別碼 hello 相同訂用帳戶，但不同的資源群組，請使用：</span><span class="sxs-lookup"><span data-stu-id="a90fc-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="a90fc-250">使用不同訂用帳戶和資源群組中的儲存體帳戶的 tooget hello 的資源 ID:</span><span class="sxs-lookup"><span data-stu-id="a90fc-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="a90fc-251">tooget hello 資源資料庫識別碼，在不同的資源群組中，使用：</span><span class="sxs-lookup"><span data-stu-id="a90fc-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="a90fc-252">通常，您需要 toouse 此函式時使用替代的資源群組中的儲存體帳戶或虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="a90fc-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="a90fc-253">hello 下列範例顯示如何從外部的資源群組的資源可以輕鬆地加以使用：</span><span class="sxs-lookup"><span data-stu-id="a90fc-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="a90fc-254">範例</span><span class="sxs-lookup"><span data-stu-id="a90fc-254">Example</span></span>

<span data-ttu-id="a90fc-255">hello 下列範例會傳回儲存體帳戶的 hello 資源識別碼 hello 資源群組中：</span><span class="sxs-lookup"><span data-stu-id="a90fc-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="a90fc-256">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="a90fc-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="a90fc-257">名稱</span><span class="sxs-lookup"><span data-stu-id="a90fc-257">Name</span></span> | <span data-ttu-id="a90fc-258">類型</span><span class="sxs-lookup"><span data-stu-id="a90fc-258">Type</span></span> | <span data-ttu-id="a90fc-259">值</span><span class="sxs-lookup"><span data-stu-id="a90fc-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="a90fc-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="a90fc-260">sameRGOutput</span></span> | <span data-ttu-id="a90fc-261">String</span><span class="sxs-lookup"><span data-stu-id="a90fc-261">String</span></span> | <span data-ttu-id="a90fc-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="a90fc-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="a90fc-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="a90fc-263">differentRGOutput</span></span> | <span data-ttu-id="a90fc-264">String</span><span class="sxs-lookup"><span data-stu-id="a90fc-264">String</span></span> | <span data-ttu-id="a90fc-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="a90fc-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="a90fc-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="a90fc-266">differentSubOutput</span></span> | <span data-ttu-id="a90fc-267">String</span><span class="sxs-lookup"><span data-stu-id="a90fc-267">String</span></span> | <span data-ttu-id="a90fc-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="a90fc-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="a90fc-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="a90fc-269">nestedResourceOutput</span></span> | <span data-ttu-id="a90fc-270">String</span><span class="sxs-lookup"><span data-stu-id="a90fc-270">String</span></span> | <span data-ttu-id="a90fc-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="a90fc-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="a90fc-272">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a90fc-272">subscription</span></span>
`subscription()`

<span data-ttu-id="a90fc-273">傳回有關 hello 目前部署的 hello 訂用帳戶的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a90fc-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="a90fc-274">傳回值</span><span class="sxs-lookup"><span data-stu-id="a90fc-274">Return value</span></span>

<span data-ttu-id="a90fc-275">hello 函式會傳回下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="a90fc-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="a90fc-276">範例</span><span class="sxs-lookup"><span data-stu-id="a90fc-276">Example</span></span>

<span data-ttu-id="a90fc-277">hello 下列範例顯示 hello 訂用帳戶函式，呼叫 hello 輸出區段中。</span><span class="sxs-lookup"><span data-stu-id="a90fc-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="a90fc-278">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a90fc-278">Next steps</span></span>
* <span data-ttu-id="a90fc-279">如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a90fc-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a90fc-280">toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a90fc-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="a90fc-281">tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="a90fc-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="a90fc-282">toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="a90fc-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

