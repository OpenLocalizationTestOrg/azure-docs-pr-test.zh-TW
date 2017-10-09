---
title: "aaaAzure 資源管理員範本函式-部署 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 tooretrieve 部署資訊中的 hello 函式 toouse。"
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="207e5-103">Azure Resource Manager 範本的部署函式</span><span class="sxs-lookup"><span data-stu-id="207e5-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="207e5-104">資源管理員提供 hello 下列函數來取得從 hello 範本的區段值和值相關的 toohello 部署：</span><span class="sxs-lookup"><span data-stu-id="207e5-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="207e5-105">部署</span><span class="sxs-lookup"><span data-stu-id="207e5-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="207e5-106">參數</span><span class="sxs-lookup"><span data-stu-id="207e5-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="207e5-107">變數</span><span class="sxs-lookup"><span data-stu-id="207e5-107">variables</span></span>](#variables)

<span data-ttu-id="207e5-108">tooget 或值的資源、 資源群組訂閱，請參閱[資源函式](resource-group-template-functions-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="207e5-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="207e5-109">部署</span><span class="sxs-lookup"><span data-stu-id="207e5-109">deployment</span></span>
`deployment()`

<span data-ttu-id="207e5-110">傳回 hello 目前的部署作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="207e5-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="207e5-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="207e5-111">Return value</span></span>

<span data-ttu-id="207e5-112">此函數會傳回部署期間所傳入的 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="207e5-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="207e5-113">依是否 hello 部署物件會傳遞為連結或內嵌物件中傳回物件的 hello hello 內容有所不同。</span><span class="sxs-lookup"><span data-stu-id="207e5-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="207e5-114">當 hello 部署物件時，會傳遞內嵌，例如使用 hello **-TemplateFile**參數在 Azure PowerShell toopoint tooa 本機檔案中，傳回的物件具有下列格式的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="207e5-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="207e5-115">當 hello 物件傳遞為連結，例如當使用 hello **-TemplateUri**參數 toopoint tooa 遠端物件、 hello 物件會傳入 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="207e5-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="207e5-116">備註</span><span class="sxs-lookup"><span data-stu-id="207e5-116">Remarks</span></span>

<span data-ttu-id="207e5-117">您可以使用 hello hello 父範本的 URI 為基礎的 deployment() toolink tooanother 範本。</span><span class="sxs-lookup"><span data-stu-id="207e5-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="207e5-118">範例</span><span class="sxs-lookup"><span data-stu-id="207e5-118">Example</span></span>

<span data-ttu-id="207e5-119">hello 下列範例會傳回 hello 部署物件：</span><span class="sxs-lookup"><span data-stu-id="207e5-119">hello following example returns hello deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="207e5-120">hello 上述範例會傳回下列物件的 hello:</span><span class="sxs-lookup"><span data-stu-id="207e5-120">hello preceding example returns hello following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="207e5-121">參數</span><span class="sxs-lookup"><span data-stu-id="207e5-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="207e5-122">傳回參數值。</span><span class="sxs-lookup"><span data-stu-id="207e5-122">Returns a parameter value.</span></span> <span data-ttu-id="207e5-123">hello 指定的參數名稱必須 hello 範本 hello 參數區段中定義。</span><span class="sxs-lookup"><span data-stu-id="207e5-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="207e5-124">參數</span><span class="sxs-lookup"><span data-stu-id="207e5-124">Parameters</span></span>

| <span data-ttu-id="207e5-125">參數</span><span class="sxs-lookup"><span data-stu-id="207e5-125">Parameter</span></span> | <span data-ttu-id="207e5-126">必要</span><span class="sxs-lookup"><span data-stu-id="207e5-126">Required</span></span> | <span data-ttu-id="207e5-127">類型</span><span class="sxs-lookup"><span data-stu-id="207e5-127">Type</span></span> | <span data-ttu-id="207e5-128">說明</span><span class="sxs-lookup"><span data-stu-id="207e5-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="207e5-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="207e5-129">parameterName</span></span> |<span data-ttu-id="207e5-130">是</span><span class="sxs-lookup"><span data-stu-id="207e5-130">Yes</span></span> |<span data-ttu-id="207e5-131">字串</span><span class="sxs-lookup"><span data-stu-id="207e5-131">string</span></span> |<span data-ttu-id="207e5-132">hello 參數 tooreturn hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="207e5-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="207e5-133">傳回值</span><span class="sxs-lookup"><span data-stu-id="207e5-133">Return value</span></span>

<span data-ttu-id="207e5-134">hello hello 值指定參數。</span><span class="sxs-lookup"><span data-stu-id="207e5-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="207e5-135">備註</span><span class="sxs-lookup"><span data-stu-id="207e5-135">Remarks</span></span>

<span data-ttu-id="207e5-136">一般而言，您可以使用參數 tooset 資源值。</span><span class="sxs-lookup"><span data-stu-id="207e5-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="207e5-137">hello 下列範例會設定網站 toohello 參數值在部署期間所傳入的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="207e5-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="207e5-138">範例</span><span class="sxs-lookup"><span data-stu-id="207e5-138">Example</span></span>

<span data-ttu-id="207e5-139">hello 下列範例示範簡化的使用 hello 參數函式。</span><span class="sxs-lookup"><span data-stu-id="207e5-139">hello following example shows a simplified use of hello parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="207e5-140">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="207e5-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="207e5-141">名稱</span><span class="sxs-lookup"><span data-stu-id="207e5-141">Name</span></span> | <span data-ttu-id="207e5-142">類型</span><span class="sxs-lookup"><span data-stu-id="207e5-142">Type</span></span> | <span data-ttu-id="207e5-143">值</span><span class="sxs-lookup"><span data-stu-id="207e5-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="207e5-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="207e5-144">stringOutput</span></span> | <span data-ttu-id="207e5-145">String</span><span class="sxs-lookup"><span data-stu-id="207e5-145">String</span></span> | <span data-ttu-id="207e5-146">選項 1</span><span class="sxs-lookup"><span data-stu-id="207e5-146">option 1</span></span> |
| <span data-ttu-id="207e5-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="207e5-147">intOutput</span></span> | <span data-ttu-id="207e5-148">int</span><span class="sxs-lookup"><span data-stu-id="207e5-148">Int</span></span> | <span data-ttu-id="207e5-149">1</span><span class="sxs-lookup"><span data-stu-id="207e5-149">1</span></span> |
| <span data-ttu-id="207e5-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="207e5-150">objectOutput</span></span> | <span data-ttu-id="207e5-151">Object</span><span class="sxs-lookup"><span data-stu-id="207e5-151">Object</span></span> | <span data-ttu-id="207e5-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="207e5-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="207e5-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="207e5-153">arrayOutput</span></span> | <span data-ttu-id="207e5-154">陣列</span><span class="sxs-lookup"><span data-stu-id="207e5-154">Array</span></span> | <span data-ttu-id="207e5-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="207e5-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="207e5-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="207e5-156">crossOutput</span></span> | <span data-ttu-id="207e5-157">String</span><span class="sxs-lookup"><span data-stu-id="207e5-157">String</span></span> | <span data-ttu-id="207e5-158">選項 1</span><span class="sxs-lookup"><span data-stu-id="207e5-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="207e5-159">variables</span><span class="sxs-lookup"><span data-stu-id="207e5-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="207e5-160">傳回 hello 變數的值。</span><span class="sxs-lookup"><span data-stu-id="207e5-160">Returns hello value of variable.</span></span> <span data-ttu-id="207e5-161">hello 指定的變數名稱必須 hello 變數 hello 範本區段中定義。</span><span class="sxs-lookup"><span data-stu-id="207e5-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="207e5-162">參數</span><span class="sxs-lookup"><span data-stu-id="207e5-162">Parameters</span></span>

| <span data-ttu-id="207e5-163">參數</span><span class="sxs-lookup"><span data-stu-id="207e5-163">Parameter</span></span> | <span data-ttu-id="207e5-164">必要</span><span class="sxs-lookup"><span data-stu-id="207e5-164">Required</span></span> | <span data-ttu-id="207e5-165">類型</span><span class="sxs-lookup"><span data-stu-id="207e5-165">Type</span></span> | <span data-ttu-id="207e5-166">說明</span><span class="sxs-lookup"><span data-stu-id="207e5-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="207e5-167">variableName</span><span class="sxs-lookup"><span data-stu-id="207e5-167">variableName</span></span> |<span data-ttu-id="207e5-168">是</span><span class="sxs-lookup"><span data-stu-id="207e5-168">Yes</span></span> |<span data-ttu-id="207e5-169">String</span><span class="sxs-lookup"><span data-stu-id="207e5-169">String</span></span> |<span data-ttu-id="207e5-170">hello 變數 tooreturn hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="207e5-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="207e5-171">傳回值</span><span class="sxs-lookup"><span data-stu-id="207e5-171">Return value</span></span>

<span data-ttu-id="207e5-172">hello hello 指定變數的值。</span><span class="sxs-lookup"><span data-stu-id="207e5-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="207e5-173">備註</span><span class="sxs-lookup"><span data-stu-id="207e5-173">Remarks</span></span>

<span data-ttu-id="207e5-174">一般而言，您使用變數 toosimplify 範本可以建構複雜的值一次。</span><span class="sxs-lookup"><span data-stu-id="207e5-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="207e5-175">hello 下列範例會建構儲存體帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="207e5-175">hello following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="207e5-176">範例</span><span class="sxs-lookup"><span data-stu-id="207e5-176">Example</span></span>

<span data-ttu-id="207e5-177">hello 範例範本會傳回不同的變數值。</span><span class="sxs-lookup"><span data-stu-id="207e5-177">hello example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="207e5-178">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="207e5-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="207e5-179">名稱</span><span class="sxs-lookup"><span data-stu-id="207e5-179">Name</span></span> | <span data-ttu-id="207e5-180">類型</span><span class="sxs-lookup"><span data-stu-id="207e5-180">Type</span></span> | <span data-ttu-id="207e5-181">值</span><span class="sxs-lookup"><span data-stu-id="207e5-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="207e5-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="207e5-182">exampleOutput1</span></span> | <span data-ttu-id="207e5-183">String</span><span class="sxs-lookup"><span data-stu-id="207e5-183">String</span></span> | <span data-ttu-id="207e5-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="207e5-184">myVariable</span></span> |
| <span data-ttu-id="207e5-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="207e5-185">exampleOutput2</span></span> | <span data-ttu-id="207e5-186">陣列</span><span class="sxs-lookup"><span data-stu-id="207e5-186">Array</span></span> | <span data-ttu-id="207e5-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="207e5-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="207e5-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="207e5-188">exampleOutput3</span></span> | <span data-ttu-id="207e5-189">String</span><span class="sxs-lookup"><span data-stu-id="207e5-189">String</span></span> | <span data-ttu-id="207e5-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="207e5-190">myVariable</span></span> |
| <span data-ttu-id="207e5-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="207e5-191">exampleOutput4</span></span> |  <span data-ttu-id="207e5-192">Object</span><span class="sxs-lookup"><span data-stu-id="207e5-192">Object</span></span> | <span data-ttu-id="207e5-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="207e5-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="207e5-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="207e5-194">Next steps</span></span>
* <span data-ttu-id="207e5-195">如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="207e5-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="207e5-196">toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="207e5-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="207e5-197">tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="207e5-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="207e5-198">toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="207e5-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

