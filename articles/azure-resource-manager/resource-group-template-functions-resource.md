---
title: "Azure Resource Manager 範本函式 - 資源 | Microsoft Docs"
description: "描述 Azure Resource Manager 範本中用來擷取資源相關值的函式。"
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
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="20f01-103">Azure Resource Manager 範本的資源函式</span><span class="sxs-lookup"><span data-stu-id="20f01-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="20f01-104">資源管理員提供下列函式以取得資源值：</span><span class="sxs-lookup"><span data-stu-id="20f01-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="20f01-105">listKeys 和 list{Value}</span><span class="sxs-lookup"><span data-stu-id="20f01-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="20f01-106">提供者</span><span class="sxs-lookup"><span data-stu-id="20f01-106">providers</span></span>](#providers)
* [<span data-ttu-id="20f01-107">reference</span><span class="sxs-lookup"><span data-stu-id="20f01-107">reference</span></span>](#reference)
* [<span data-ttu-id="20f01-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="20f01-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="20f01-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="20f01-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="20f01-110">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="20f01-110">subscription</span></span>](#subscription)

<span data-ttu-id="20f01-111">若要從參數、變數或目前的部署中取得值，請參閱 [部署值函式](resource-group-template-functions-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="20f01-111">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="20f01-112">listKeys 和 list{Value}</span><span class="sxs-lookup"><span data-stu-id="20f01-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="20f01-113">對支援 list 作業的任何資源類型傳回值。</span><span class="sxs-lookup"><span data-stu-id="20f01-113">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="20f01-114">最常見的用法是 `listKeys`。</span><span class="sxs-lookup"><span data-stu-id="20f01-114">The most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="20f01-115">參數</span><span class="sxs-lookup"><span data-stu-id="20f01-115">Parameters</span></span>

| <span data-ttu-id="20f01-116">參數</span><span class="sxs-lookup"><span data-stu-id="20f01-116">Parameter</span></span> | <span data-ttu-id="20f01-117">必要</span><span class="sxs-lookup"><span data-stu-id="20f01-117">Required</span></span> | <span data-ttu-id="20f01-118">類型</span><span class="sxs-lookup"><span data-stu-id="20f01-118">Type</span></span> | <span data-ttu-id="20f01-119">說明</span><span class="sxs-lookup"><span data-stu-id="20f01-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20f01-120">resourceName 或 resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="20f01-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="20f01-121">是</span><span class="sxs-lookup"><span data-stu-id="20f01-121">Yes</span></span> |<span data-ttu-id="20f01-122">字串</span><span class="sxs-lookup"><span data-stu-id="20f01-122">string</span></span> |<span data-ttu-id="20f01-123">資源的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="20f01-123">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="20f01-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="20f01-124">apiVersion</span></span> |<span data-ttu-id="20f01-125">是</span><span class="sxs-lookup"><span data-stu-id="20f01-125">Yes</span></span> |<span data-ttu-id="20f01-126">字串</span><span class="sxs-lookup"><span data-stu-id="20f01-126">string</span></span> |<span data-ttu-id="20f01-127">資源執行階段狀態的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="20f01-127">API version of resource runtime state.</span></span> <span data-ttu-id="20f01-128">一般而言，格式為 **yyyy-mm-dd**。</span><span class="sxs-lookup"><span data-stu-id="20f01-128">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20f01-129">傳回值</span><span class="sxs-lookup"><span data-stu-id="20f01-129">Return value</span></span>

<span data-ttu-id="20f01-130">從 listKeys 傳回的物件具有下列格式︰</span><span class="sxs-lookup"><span data-stu-id="20f01-130">The returned object from listKeys has the following format:</span></span>

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

<span data-ttu-id="20f01-131">其他 list 函式具有不同的傳回格式。</span><span class="sxs-lookup"><span data-stu-id="20f01-131">Other list functions have different return formats.</span></span> <span data-ttu-id="20f01-132">若要查看函式的格式，請將函式放入 [輸出] 區段，如範本範例所示。</span><span class="sxs-lookup"><span data-stu-id="20f01-132">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="20f01-133">備註</span><span class="sxs-lookup"><span data-stu-id="20f01-133">Remarks</span></span>

<span data-ttu-id="20f01-134">開頭為 **list** 的任何作業都可在您的範本中用為函式。</span><span class="sxs-lookup"><span data-stu-id="20f01-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="20f01-135">可用作業不只包含 listKeys，還包含像 `list`、`listAdminKeys` 和 `listStatus` 等作業。</span><span class="sxs-lookup"><span data-stu-id="20f01-135">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="20f01-136">不過若 **list** 作業需要要求本文中的值，則無法使用。</span><span class="sxs-lookup"><span data-stu-id="20f01-136">However, you cannot use **list** operations that require values in the request body.</span></span> <span data-ttu-id="20f01-137">舉例來說，[List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) 作業需要要求本文之參數，例如 *signedExpiry*，所以您無法在範本中使用此作業。</span><span class="sxs-lookup"><span data-stu-id="20f01-137">For example, the [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="20f01-138">為判斷哪一個資源類型具有 list 作業，您可以使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="20f01-138">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="20f01-139">檢視資源提供者的 [REST API 作業](/rest/api/)，並尋找 list 作業。</span><span class="sxs-lookup"><span data-stu-id="20f01-139">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="20f01-140">例如，儲存體帳戶具有 [listKeys 作業](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys)。</span><span class="sxs-lookup"><span data-stu-id="20f01-140">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="20f01-141">使用 [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="20f01-141">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="20f01-142">下列範例會取得儲存體帳戶的所有 list 作業︰</span><span class="sxs-lookup"><span data-stu-id="20f01-142">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="20f01-143">使用下列 Azure CLI 命令可只篩選出 list 作業：</span><span class="sxs-lookup"><span data-stu-id="20f01-143">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="20f01-144">使用 [resourceId 函式](#resourceid)或 `{providerNamespace}/{resourceType}/{resourceName}` 格式來指定資源。</span><span class="sxs-lookup"><span data-stu-id="20f01-144">Specify the resource by using either the [resourceId function](#resourceid), or the format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="20f01-145">範例</span><span class="sxs-lookup"><span data-stu-id="20f01-145">Example</span></span>

<span data-ttu-id="20f01-146">下列範例顯示如何在 outputs 區段中從儲存體帳戶傳回主要和次要金鑰。</span><span class="sxs-lookup"><span data-stu-id="20f01-146">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

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

## <a name="providers"></a><span data-ttu-id="20f01-147">提供者</span><span class="sxs-lookup"><span data-stu-id="20f01-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="20f01-148">傳回資源提供者和其所支援資源類型的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="20f01-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="20f01-149">如果未提供資源類型，則函式會傳回資源提供者所有的支援類型。</span><span class="sxs-lookup"><span data-stu-id="20f01-149">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="20f01-150">參數</span><span class="sxs-lookup"><span data-stu-id="20f01-150">Parameters</span></span>

| <span data-ttu-id="20f01-151">參數</span><span class="sxs-lookup"><span data-stu-id="20f01-151">Parameter</span></span> | <span data-ttu-id="20f01-152">必要</span><span class="sxs-lookup"><span data-stu-id="20f01-152">Required</span></span> | <span data-ttu-id="20f01-153">類型</span><span class="sxs-lookup"><span data-stu-id="20f01-153">Type</span></span> | <span data-ttu-id="20f01-154">說明</span><span class="sxs-lookup"><span data-stu-id="20f01-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20f01-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="20f01-155">providerNamespace</span></span> |<span data-ttu-id="20f01-156">是</span><span class="sxs-lookup"><span data-stu-id="20f01-156">Yes</span></span> |<span data-ttu-id="20f01-157">字串</span><span class="sxs-lookup"><span data-stu-id="20f01-157">string</span></span> |<span data-ttu-id="20f01-158">提供者的命名空間</span><span class="sxs-lookup"><span data-stu-id="20f01-158">Namespace of the provider</span></span> |
| <span data-ttu-id="20f01-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="20f01-159">resourceType</span></span> |<span data-ttu-id="20f01-160">否</span><span class="sxs-lookup"><span data-stu-id="20f01-160">No</span></span> |<span data-ttu-id="20f01-161">字串</span><span class="sxs-lookup"><span data-stu-id="20f01-161">string</span></span> |<span data-ttu-id="20f01-162">所指定命名空間內的資源類型。</span><span class="sxs-lookup"><span data-stu-id="20f01-162">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20f01-163">傳回值</span><span class="sxs-lookup"><span data-stu-id="20f01-163">Return value</span></span>

<span data-ttu-id="20f01-164">每個支援類型都會以下列格式傳回：</span><span class="sxs-lookup"><span data-stu-id="20f01-164">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="20f01-165">不保證所傳回的值會有陣列順序。</span><span class="sxs-lookup"><span data-stu-id="20f01-165">Array ordering of the returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="20f01-166">範例</span><span class="sxs-lookup"><span data-stu-id="20f01-166">Example</span></span>

<span data-ttu-id="20f01-167">下列範例顯示如何使用 provider 函數：</span><span class="sxs-lookup"><span data-stu-id="20f01-167">The following example shows how to use the provider function:</span></span>

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

<span data-ttu-id="20f01-168">上述範例會以下列格式傳回物件︰</span><span class="sxs-lookup"><span data-stu-id="20f01-168">The preceding example returns an object in the following format:</span></span>

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

## <a name="reference"></a><span data-ttu-id="20f01-169">reference</span><span class="sxs-lookup"><span data-stu-id="20f01-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="20f01-170">傳回代表資源執行階段狀態的物件。</span><span class="sxs-lookup"><span data-stu-id="20f01-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="20f01-171">參數</span><span class="sxs-lookup"><span data-stu-id="20f01-171">Parameters</span></span>

| <span data-ttu-id="20f01-172">參數</span><span class="sxs-lookup"><span data-stu-id="20f01-172">Parameter</span></span> | <span data-ttu-id="20f01-173">必要</span><span class="sxs-lookup"><span data-stu-id="20f01-173">Required</span></span> | <span data-ttu-id="20f01-174">類型</span><span class="sxs-lookup"><span data-stu-id="20f01-174">Type</span></span> | <span data-ttu-id="20f01-175">說明</span><span class="sxs-lookup"><span data-stu-id="20f01-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20f01-176">resourceName 或 resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="20f01-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="20f01-177">是</span><span class="sxs-lookup"><span data-stu-id="20f01-177">Yes</span></span> |<span data-ttu-id="20f01-178">string</span><span class="sxs-lookup"><span data-stu-id="20f01-178">string</span></span> |<span data-ttu-id="20f01-179">資源的名稱或唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="20f01-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="20f01-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="20f01-180">apiVersion</span></span> |<span data-ttu-id="20f01-181">否</span><span class="sxs-lookup"><span data-stu-id="20f01-181">No</span></span> |<span data-ttu-id="20f01-182">字串</span><span class="sxs-lookup"><span data-stu-id="20f01-182">string</span></span> |<span data-ttu-id="20f01-183">指定的資源的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="20f01-183">API version of the specified resource.</span></span> <span data-ttu-id="20f01-184">如果在相同的範本內未供應資源，則請包含此參數。</span><span class="sxs-lookup"><span data-stu-id="20f01-184">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="20f01-185">一般而言，格式為 **yyyy-mm-dd**。</span><span class="sxs-lookup"><span data-stu-id="20f01-185">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20f01-186">傳回值</span><span class="sxs-lookup"><span data-stu-id="20f01-186">Return value</span></span>

<span data-ttu-id="20f01-187">每種資源類型都會針對 reference 函式傳回不同屬性。</span><span class="sxs-lookup"><span data-stu-id="20f01-187">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="20f01-188">此函式不會傳回單一的預先定義格式。</span><span class="sxs-lookup"><span data-stu-id="20f01-188">The function does not return a single, predefined format.</span></span> <span data-ttu-id="20f01-189">若要查看資源類型的屬性，請在輸出區段中傳回物件，如範例所示。</span><span class="sxs-lookup"><span data-stu-id="20f01-189">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="20f01-190">備註</span><span class="sxs-lookup"><span data-stu-id="20f01-190">Remarks</span></span>

<span data-ttu-id="20f01-191">reference 函數會從執行階段狀態衍生其值，因此不能用在 variables 區段中。</span><span class="sxs-lookup"><span data-stu-id="20f01-191">The reference function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="20f01-192">它可以用於範本的 outputs 區段中。</span><span class="sxs-lookup"><span data-stu-id="20f01-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="20f01-193">如果在相同的範本內佈建所參考的資源，則可使用 reference 函式來隱含宣告一個資源相依於另一個資源。</span><span class="sxs-lookup"><span data-stu-id="20f01-193">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="20f01-194">您不需要同時使用 dependsOn 屬性。</span><span class="sxs-lookup"><span data-stu-id="20f01-194">You do not need to also use the dependsOn property.</span></span> <span data-ttu-id="20f01-195">所參考的資源完成部署之前不會評估函式。</span><span class="sxs-lookup"><span data-stu-id="20f01-195">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="20f01-196">若要查看資源類型的屬性名稱和值，請建立一個會在 outputs 區段中傳回物件的範本。</span><span class="sxs-lookup"><span data-stu-id="20f01-196">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="20f01-197">如果您有一個該類型的現有資源，您的範本就會傳回物件，而不會部署任何新資源。</span><span class="sxs-lookup"><span data-stu-id="20f01-197">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="20f01-198">一般而言，您可以使用 **reference** 函式從物件傳回特定值，例如 Blob 端點 URI 或完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="20f01-198">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

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

### <a name="example"></a><span data-ttu-id="20f01-199">範例</span><span class="sxs-lookup"><span data-stu-id="20f01-199">Example</span></span>

<span data-ttu-id="20f01-200">若要部署並參考相同範本中的資源，請使用：</span><span class="sxs-lookup"><span data-stu-id="20f01-200">To deploy and reference the resource in the same template, use:</span></span>

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

<span data-ttu-id="20f01-201">上述範例會以下列格式傳回物件︰</span><span class="sxs-lookup"><span data-stu-id="20f01-201">The preceding example returns an object in the following format:</span></span>

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

<span data-ttu-id="20f01-202">下列範例參照了本範本中未部署之儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="20f01-202">The following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="20f01-203">此儲存體帳戶已經存在在同樣的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="20f01-203">The storage account already exists within the same resource group.</span></span>

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

## <a name="resourcegroup"></a><span data-ttu-id="20f01-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="20f01-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="20f01-205">傳回代表目前資源群組的物件。</span><span class="sxs-lookup"><span data-stu-id="20f01-205">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="20f01-206">傳回值</span><span class="sxs-lookup"><span data-stu-id="20f01-206">Return value</span></span>

<span data-ttu-id="20f01-207">傳回的物件會使用下列格式：</span><span class="sxs-lookup"><span data-stu-id="20f01-207">The returned object is in the following format:</span></span>

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

### <a name="remarks"></a><span data-ttu-id="20f01-208">備註</span><span class="sxs-lookup"><span data-stu-id="20f01-208">Remarks</span></span>

<span data-ttu-id="20f01-209">resourceGroup 函式的常見用法是在和資源群組相同的位置中建立資源。</span><span class="sxs-lookup"><span data-stu-id="20f01-209">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="20f01-210">下列範例使用資源群組位置來指派網站的位置。</span><span class="sxs-lookup"><span data-stu-id="20f01-210">The following example uses the resource group location to assign the location for a web site.</span></span>

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

### <a name="example"></a><span data-ttu-id="20f01-211">範例</span><span class="sxs-lookup"><span data-stu-id="20f01-211">Example</span></span>

<span data-ttu-id="20f01-212">下列範本會傳回資源群組的屬性。</span><span class="sxs-lookup"><span data-stu-id="20f01-212">The following template returns the properties of the resource group.</span></span>

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

<span data-ttu-id="20f01-213">上述範例會以下列格式傳回物件︰</span><span class="sxs-lookup"><span data-stu-id="20f01-213">The preceding example returns an object in the following format:</span></span>

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

## <a name="resourceid"></a><span data-ttu-id="20f01-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="20f01-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="20f01-215">傳回資源的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="20f01-215">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="20f01-216">如果資源名稱不確定或未佈建在相同的範本內，請使用此函數。</span><span class="sxs-lookup"><span data-stu-id="20f01-216">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="20f01-217">參數</span><span class="sxs-lookup"><span data-stu-id="20f01-217">Parameters</span></span>

| <span data-ttu-id="20f01-218">參數</span><span class="sxs-lookup"><span data-stu-id="20f01-218">Parameter</span></span> | <span data-ttu-id="20f01-219">必要</span><span class="sxs-lookup"><span data-stu-id="20f01-219">Required</span></span> | <span data-ttu-id="20f01-220">類型</span><span class="sxs-lookup"><span data-stu-id="20f01-220">Type</span></span> | <span data-ttu-id="20f01-221">說明</span><span class="sxs-lookup"><span data-stu-id="20f01-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="20f01-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="20f01-222">subscriptionId</span></span> |<span data-ttu-id="20f01-223">否</span><span class="sxs-lookup"><span data-stu-id="20f01-223">No</span></span> |<span data-ttu-id="20f01-224">字串 (GUID 格式)</span><span class="sxs-lookup"><span data-stu-id="20f01-224">string (In GUID format)</span></span> |<span data-ttu-id="20f01-225">預設值為目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="20f01-225">Default value is the current subscription.</span></span> <span data-ttu-id="20f01-226">需要擷取另一個訂用帳戶中的資源群組時，請指定此值。</span><span class="sxs-lookup"><span data-stu-id="20f01-226">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="20f01-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="20f01-227">resourceGroupName</span></span> |<span data-ttu-id="20f01-228">否</span><span class="sxs-lookup"><span data-stu-id="20f01-228">No</span></span> |<span data-ttu-id="20f01-229">字串</span><span class="sxs-lookup"><span data-stu-id="20f01-229">string</span></span> |<span data-ttu-id="20f01-230">預設值為目前資源群組。</span><span class="sxs-lookup"><span data-stu-id="20f01-230">Default value is current resource group.</span></span> <span data-ttu-id="20f01-231">需要擷取另一個訂用帳戶中的資源群組時，請指定此值。</span><span class="sxs-lookup"><span data-stu-id="20f01-231">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="20f01-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="20f01-232">resourceType</span></span> |<span data-ttu-id="20f01-233">是</span><span class="sxs-lookup"><span data-stu-id="20f01-233">Yes</span></span> |<span data-ttu-id="20f01-234">字串</span><span class="sxs-lookup"><span data-stu-id="20f01-234">string</span></span> |<span data-ttu-id="20f01-235">資源的類型 (包括資源提供者命名空間)。</span><span class="sxs-lookup"><span data-stu-id="20f01-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="20f01-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="20f01-236">resourceName1</span></span> |<span data-ttu-id="20f01-237">是</span><span class="sxs-lookup"><span data-stu-id="20f01-237">Yes</span></span> |<span data-ttu-id="20f01-238">string</span><span class="sxs-lookup"><span data-stu-id="20f01-238">string</span></span> |<span data-ttu-id="20f01-239">資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="20f01-239">Name of resource.</span></span> |
| <span data-ttu-id="20f01-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="20f01-240">resourceName2</span></span> |<span data-ttu-id="20f01-241">否</span><span class="sxs-lookup"><span data-stu-id="20f01-241">No</span></span> |<span data-ttu-id="20f01-242">string</span><span class="sxs-lookup"><span data-stu-id="20f01-242">string</span></span> |<span data-ttu-id="20f01-243">如果是巢狀資源，則為下一個資源名稱區段。</span><span class="sxs-lookup"><span data-stu-id="20f01-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="20f01-244">傳回值</span><span class="sxs-lookup"><span data-stu-id="20f01-244">Return value</span></span>

<span data-ttu-id="20f01-245">識別碼會以下列格式傳回：</span><span class="sxs-lookup"><span data-stu-id="20f01-245">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="20f01-246">備註</span><span class="sxs-lookup"><span data-stu-id="20f01-246">Remarks</span></span>

<span data-ttu-id="20f01-247">您指定的參數值取決於資源是否在相同的訂用帳戶和資源群組中作為目前的部署。</span><span class="sxs-lookup"><span data-stu-id="20f01-247">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="20f01-248">若要在相同的訂用帳戶和資源群組中取得儲存體帳戶的資源識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="20f01-248">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="20f01-249">若要在相同的訂用帳戶但不同的資源群組中取得儲存體帳戶的資源識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="20f01-249">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="20f01-250">若要在不同的訂用帳戶和資源群組中取得儲存體帳戶的資源識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="20f01-250">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="20f01-251">若要在不同的資源群組中取得資料庫的資源識別碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="20f01-251">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="20f01-252">通常，在替代資源群組中使用儲存體帳戶或虛擬網路時，需要使用此函數。</span><span class="sxs-lookup"><span data-stu-id="20f01-252">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="20f01-253">下列範例顯示如何輕鬆地使用外部資源群組中的資源：</span><span class="sxs-lookup"><span data-stu-id="20f01-253">The following example shows how a resource from an external resource group can easily be used:</span></span>

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

### <a name="example"></a><span data-ttu-id="20f01-254">範例</span><span class="sxs-lookup"><span data-stu-id="20f01-254">Example</span></span>

<span data-ttu-id="20f01-255">下列範例會傳回資源群組中儲存體帳戶的資源識別碼：</span><span class="sxs-lookup"><span data-stu-id="20f01-255">The following example returns the resource ID for a storage account in the resource group:</span></span>

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

<span data-ttu-id="20f01-256">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="20f01-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="20f01-257">名稱</span><span class="sxs-lookup"><span data-stu-id="20f01-257">Name</span></span> | <span data-ttu-id="20f01-258">類型</span><span class="sxs-lookup"><span data-stu-id="20f01-258">Type</span></span> | <span data-ttu-id="20f01-259">值</span><span class="sxs-lookup"><span data-stu-id="20f01-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="20f01-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="20f01-260">sameRGOutput</span></span> | <span data-ttu-id="20f01-261">String</span><span class="sxs-lookup"><span data-stu-id="20f01-261">String</span></span> | <span data-ttu-id="20f01-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="20f01-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="20f01-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="20f01-263">differentRGOutput</span></span> | <span data-ttu-id="20f01-264">String</span><span class="sxs-lookup"><span data-stu-id="20f01-264">String</span></span> | <span data-ttu-id="20f01-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="20f01-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="20f01-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="20f01-266">differentSubOutput</span></span> | <span data-ttu-id="20f01-267">String</span><span class="sxs-lookup"><span data-stu-id="20f01-267">String</span></span> | <span data-ttu-id="20f01-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="20f01-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="20f01-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="20f01-269">nestedResourceOutput</span></span> | <span data-ttu-id="20f01-270">String</span><span class="sxs-lookup"><span data-stu-id="20f01-270">String</span></span> | <span data-ttu-id="20f01-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="20f01-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="20f01-272">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="20f01-272">subscription</span></span>
`subscription()`

<span data-ttu-id="20f01-273">傳回目前部署的訂用帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="20f01-273">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="20f01-274">傳回值</span><span class="sxs-lookup"><span data-stu-id="20f01-274">Return value</span></span>

<span data-ttu-id="20f01-275">此函式會傳回下列格式︰</span><span class="sxs-lookup"><span data-stu-id="20f01-275">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="20f01-276">範例</span><span class="sxs-lookup"><span data-stu-id="20f01-276">Example</span></span>

<span data-ttu-id="20f01-277">下列範例顯示在 outputs 區段中所呼叫的 subscription 函式。</span><span class="sxs-lookup"><span data-stu-id="20f01-277">The following example shows the subscription function called in the outputs section.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="20f01-278">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20f01-278">Next steps</span></span>
* <span data-ttu-id="20f01-279">如需有關 Azure Resource Manager 範本中各區段的說明，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="20f01-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="20f01-280">若要合併多個範本，請參閱[透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="20f01-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="20f01-281">若要依指定的次數重複建立資源類型，請參閱 [在 Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="20f01-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="20f01-282">若要了解如何部署已建立的範本，請參閱[使用 Azure Resource Manager 範本部署應用程式](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="20f01-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

