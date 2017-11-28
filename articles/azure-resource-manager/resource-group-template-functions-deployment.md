---
title: "Azure Resource Manager 範本函式 - 部署 | Microsoft Docs"
description: "描述 Azure Resource Manager 範本中用來擷取部署資訊的函式。"
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
ms.openlocfilehash: d7e6bcd669d40cb19de44b646505856ecd8f51a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="5f362-103">Azure Resource Manager 範本的部署函式</span><span class="sxs-lookup"><span data-stu-id="5f362-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="5f362-104">資源管理員提供下列函式，以從與部署相關的範本和值的區段中取得值：</span><span class="sxs-lookup"><span data-stu-id="5f362-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="5f362-105">部署</span><span class="sxs-lookup"><span data-stu-id="5f362-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="5f362-106">參數</span><span class="sxs-lookup"><span data-stu-id="5f362-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="5f362-107">變數</span><span class="sxs-lookup"><span data-stu-id="5f362-107">variables</span></span>](#variables)

<span data-ttu-id="5f362-108">若要從資源、資源群組或訂用帳戶中取得值，請參閱 [資源函式](resource-group-template-functions-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="5f362-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="5f362-109">部署</span><span class="sxs-lookup"><span data-stu-id="5f362-109">deployment</span></span>
`deployment()`

<span data-ttu-id="5f362-110">傳回目前部署作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5f362-110">Returns information about the current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="5f362-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="5f362-111">Return value</span></span>

<span data-ttu-id="5f362-112">此函式會傳回部署期間所傳遞的物件。</span><span class="sxs-lookup"><span data-stu-id="5f362-112">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="5f362-113">視部署物件是以連結或內嵌物件形式傳遞，所傳回物件中的屬性將有所不同。</span><span class="sxs-lookup"><span data-stu-id="5f362-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="5f362-114">部署物件以內嵌形式傳遞時 (例如使用 Azure PowerShell 中的 **-TemplateFile** 參數指向本機檔案時)，所傳回的物件為下列格式：</span><span class="sxs-lookup"><span data-stu-id="5f362-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

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

<span data-ttu-id="5f362-115">部署物件以連結形式傳遞時 (例如使用 **-TemplateUri** 參數指向遠端檔案時)，所傳回的物件為下列格式：</span><span class="sxs-lookup"><span data-stu-id="5f362-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

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

### <a name="remarks"></a><span data-ttu-id="5f362-116">備註</span><span class="sxs-lookup"><span data-stu-id="5f362-116">Remarks</span></span>

<span data-ttu-id="5f362-117">您可以上層範本的 URI 作為基礎，使用部署() 連結至另一個範本。</span><span class="sxs-lookup"><span data-stu-id="5f362-117">You can use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="5f362-118">範例</span><span class="sxs-lookup"><span data-stu-id="5f362-118">Example</span></span>

<span data-ttu-id="5f362-119">下列範例會傳回部署物件︰</span><span class="sxs-lookup"><span data-stu-id="5f362-119">The following example returns the deployment object:</span></span>

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

<span data-ttu-id="5f362-120">上述範例會傳回下列物件︰</span><span class="sxs-lookup"><span data-stu-id="5f362-120">The preceding example returns the following object:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="5f362-121">參數</span><span class="sxs-lookup"><span data-stu-id="5f362-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="5f362-122">傳回參數值。</span><span class="sxs-lookup"><span data-stu-id="5f362-122">Returns a parameter value.</span></span> <span data-ttu-id="5f362-123">指定的參數名稱必須定義於範本的 parameters 區段中。</span><span class="sxs-lookup"><span data-stu-id="5f362-123">The specified parameter name must be defined in the parameters section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="5f362-124">參數</span><span class="sxs-lookup"><span data-stu-id="5f362-124">Parameters</span></span>

| <span data-ttu-id="5f362-125">參數</span><span class="sxs-lookup"><span data-stu-id="5f362-125">Parameter</span></span> | <span data-ttu-id="5f362-126">必要</span><span class="sxs-lookup"><span data-stu-id="5f362-126">Required</span></span> | <span data-ttu-id="5f362-127">類型</span><span class="sxs-lookup"><span data-stu-id="5f362-127">Type</span></span> | <span data-ttu-id="5f362-128">說明</span><span class="sxs-lookup"><span data-stu-id="5f362-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5f362-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="5f362-129">parameterName</span></span> |<span data-ttu-id="5f362-130">是</span><span class="sxs-lookup"><span data-stu-id="5f362-130">Yes</span></span> |<span data-ttu-id="5f362-131">字串</span><span class="sxs-lookup"><span data-stu-id="5f362-131">string</span></span> |<span data-ttu-id="5f362-132">要傳回的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="5f362-132">The name of the parameter to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5f362-133">傳回值</span><span class="sxs-lookup"><span data-stu-id="5f362-133">Return value</span></span>

<span data-ttu-id="5f362-134">指定參數的值。</span><span class="sxs-lookup"><span data-stu-id="5f362-134">The value of the specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="5f362-135">備註</span><span class="sxs-lookup"><span data-stu-id="5f362-135">Remarks</span></span>

<span data-ttu-id="5f362-136">一般而言，您可以使用參數來設定資源的值。</span><span class="sxs-lookup"><span data-stu-id="5f362-136">Typically, you use parameters to set resource values.</span></span> <span data-ttu-id="5f362-137">下列範例會將網站的名稱設定為部署期間所傳入的參數值。</span><span class="sxs-lookup"><span data-stu-id="5f362-137">The following example sets the name of web site to the parameter value passed in during deployment.</span></span>

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

### <a name="example"></a><span data-ttu-id="5f362-138">範例</span><span class="sxs-lookup"><span data-stu-id="5f362-138">Example</span></span>

<span data-ttu-id="5f362-139">下列範例顯示 parameters 函數的簡化用法。</span><span class="sxs-lookup"><span data-stu-id="5f362-139">The following example shows a simplified use of the parameters function.</span></span>

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

<span data-ttu-id="5f362-140">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="5f362-140">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5f362-141">名稱</span><span class="sxs-lookup"><span data-stu-id="5f362-141">Name</span></span> | <span data-ttu-id="5f362-142">類型</span><span class="sxs-lookup"><span data-stu-id="5f362-142">Type</span></span> | <span data-ttu-id="5f362-143">值</span><span class="sxs-lookup"><span data-stu-id="5f362-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5f362-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="5f362-144">stringOutput</span></span> | <span data-ttu-id="5f362-145">String</span><span class="sxs-lookup"><span data-stu-id="5f362-145">String</span></span> | <span data-ttu-id="5f362-146">選項 1</span><span class="sxs-lookup"><span data-stu-id="5f362-146">option 1</span></span> |
| <span data-ttu-id="5f362-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="5f362-147">intOutput</span></span> | <span data-ttu-id="5f362-148">int</span><span class="sxs-lookup"><span data-stu-id="5f362-148">Int</span></span> | <span data-ttu-id="5f362-149">1</span><span class="sxs-lookup"><span data-stu-id="5f362-149">1</span></span> |
| <span data-ttu-id="5f362-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="5f362-150">objectOutput</span></span> | <span data-ttu-id="5f362-151">Object</span><span class="sxs-lookup"><span data-stu-id="5f362-151">Object</span></span> | <span data-ttu-id="5f362-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="5f362-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="5f362-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="5f362-153">arrayOutput</span></span> | <span data-ttu-id="5f362-154">陣列</span><span class="sxs-lookup"><span data-stu-id="5f362-154">Array</span></span> | <span data-ttu-id="5f362-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="5f362-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="5f362-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="5f362-156">crossOutput</span></span> | <span data-ttu-id="5f362-157">String</span><span class="sxs-lookup"><span data-stu-id="5f362-157">String</span></span> | <span data-ttu-id="5f362-158">選項 1</span><span class="sxs-lookup"><span data-stu-id="5f362-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="5f362-159">變數</span><span class="sxs-lookup"><span data-stu-id="5f362-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="5f362-160">傳回變數的值。</span><span class="sxs-lookup"><span data-stu-id="5f362-160">Returns the value of variable.</span></span> <span data-ttu-id="5f362-161">指定的變數名稱必須定義於範本的 variables 區段中。</span><span class="sxs-lookup"><span data-stu-id="5f362-161">The specified variable name must be defined in the variables section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="5f362-162">參數</span><span class="sxs-lookup"><span data-stu-id="5f362-162">Parameters</span></span>

| <span data-ttu-id="5f362-163">參數</span><span class="sxs-lookup"><span data-stu-id="5f362-163">Parameter</span></span> | <span data-ttu-id="5f362-164">必要</span><span class="sxs-lookup"><span data-stu-id="5f362-164">Required</span></span> | <span data-ttu-id="5f362-165">類型</span><span class="sxs-lookup"><span data-stu-id="5f362-165">Type</span></span> | <span data-ttu-id="5f362-166">說明</span><span class="sxs-lookup"><span data-stu-id="5f362-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="5f362-167">variableName</span><span class="sxs-lookup"><span data-stu-id="5f362-167">variableName</span></span> |<span data-ttu-id="5f362-168">是</span><span class="sxs-lookup"><span data-stu-id="5f362-168">Yes</span></span> |<span data-ttu-id="5f362-169">String</span><span class="sxs-lookup"><span data-stu-id="5f362-169">String</span></span> |<span data-ttu-id="5f362-170">要傳回的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="5f362-170">The name of the variable to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="5f362-171">傳回值</span><span class="sxs-lookup"><span data-stu-id="5f362-171">Return value</span></span>

<span data-ttu-id="5f362-172">指定變數的值。</span><span class="sxs-lookup"><span data-stu-id="5f362-172">The value of the specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="5f362-173">備註</span><span class="sxs-lookup"><span data-stu-id="5f362-173">Remarks</span></span>

<span data-ttu-id="5f362-174">一般而言，您可以使用變數將範本簡化，方法是僅建構一次複雜的值。</span><span class="sxs-lookup"><span data-stu-id="5f362-174">Typically, you use variables to simplify your template by constructing complex values only once.</span></span> <span data-ttu-id="5f362-175">下列範例會建構儲存體帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="5f362-175">The following example constructs a unique name for a storage account.</span></span>

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

### <a name="example"></a><span data-ttu-id="5f362-176">範例</span><span class="sxs-lookup"><span data-stu-id="5f362-176">Example</span></span>

<span data-ttu-id="5f362-177">範例範本會傳回不同的變數值。</span><span class="sxs-lookup"><span data-stu-id="5f362-177">The example template returns different variable values.</span></span>

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

<span data-ttu-id="5f362-178">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="5f362-178">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="5f362-179">名稱</span><span class="sxs-lookup"><span data-stu-id="5f362-179">Name</span></span> | <span data-ttu-id="5f362-180">類型</span><span class="sxs-lookup"><span data-stu-id="5f362-180">Type</span></span> | <span data-ttu-id="5f362-181">值</span><span class="sxs-lookup"><span data-stu-id="5f362-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="5f362-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="5f362-182">exampleOutput1</span></span> | <span data-ttu-id="5f362-183">String</span><span class="sxs-lookup"><span data-stu-id="5f362-183">String</span></span> | <span data-ttu-id="5f362-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="5f362-184">myVariable</span></span> |
| <span data-ttu-id="5f362-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="5f362-185">exampleOutput2</span></span> | <span data-ttu-id="5f362-186">陣列</span><span class="sxs-lookup"><span data-stu-id="5f362-186">Array</span></span> | <span data-ttu-id="5f362-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="5f362-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="5f362-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="5f362-188">exampleOutput3</span></span> | <span data-ttu-id="5f362-189">String</span><span class="sxs-lookup"><span data-stu-id="5f362-189">String</span></span> | <span data-ttu-id="5f362-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="5f362-190">myVariable</span></span> |
| <span data-ttu-id="5f362-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="5f362-191">exampleOutput4</span></span> |  <span data-ttu-id="5f362-192">Object</span><span class="sxs-lookup"><span data-stu-id="5f362-192">Object</span></span> | <span data-ttu-id="5f362-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="5f362-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5f362-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f362-194">Next steps</span></span>
* <span data-ttu-id="5f362-195">如需有關 Azure Resource Manager 範本中各區段的說明，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="5f362-195">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="5f362-196">若要合併多個範本，請參閱[透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="5f362-196">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="5f362-197">若要依指定的次數重複建立資源類型，請參閱 [在 Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="5f362-197">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="5f362-198">若要了解如何部署已建立的範本，請參閱[使用 Azure Resource Manager 範本部署應用程式](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="5f362-198">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

