---
title: "Azure Resource Manager 範本結構和語法 | Microsoft Docs"
description: "使用宣告式 JSON 語法描述 Azure Resource Manager 範本的結構和屬性。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="a979d-103">了解 Azure Resource Manager 範本的結構和語法</span><span class="sxs-lookup"><span data-stu-id="a979d-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="a979d-104">本主題說明 Azure Resource Manager 範本的結構。</span><span class="sxs-lookup"><span data-stu-id="a979d-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="a979d-105">它會呈現範本的不同區段，以及這些區段中可用的屬性。</span><span class="sxs-lookup"><span data-stu-id="a979d-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="a979d-106">範本由 JSON 與運算式所組成，可讓您用來為部署建構值。</span><span class="sxs-lookup"><span data-stu-id="a979d-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="a979d-107">如需建立範本的逐步教學課程，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="a979d-108">範本格式</span><span class="sxs-lookup"><span data-stu-id="a979d-108">Template format</span></span>
<span data-ttu-id="a979d-109">在最簡單的結構中，範本包含下列元素：</span><span class="sxs-lookup"><span data-stu-id="a979d-109">In its simplest structure, a template contains the following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="a979d-110">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a979d-110">Element name</span></span> | <span data-ttu-id="a979d-111">必要</span><span class="sxs-lookup"><span data-stu-id="a979d-111">Required</span></span> | <span data-ttu-id="a979d-112">說明</span><span class="sxs-lookup"><span data-stu-id="a979d-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a979d-113">$schema</span><span class="sxs-lookup"><span data-stu-id="a979d-113">$schema</span></span> |<span data-ttu-id="a979d-114">是</span><span class="sxs-lookup"><span data-stu-id="a979d-114">Yes</span></span> |<span data-ttu-id="a979d-115">JSON 結構描述檔案的位置，說明範本語言的版本。</span><span class="sxs-lookup"><span data-stu-id="a979d-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="a979d-116">使用上述範例所示的 URL。</span><span class="sxs-lookup"><span data-stu-id="a979d-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="a979d-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="a979d-117">contentVersion</span></span> |<span data-ttu-id="a979d-118">是</span><span class="sxs-lookup"><span data-stu-id="a979d-118">Yes</span></span> |<span data-ttu-id="a979d-119">範本版本 (例如 1.0.0.0)。</span><span class="sxs-lookup"><span data-stu-id="a979d-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="a979d-120">您可以為此元素提供任何值。</span><span class="sxs-lookup"><span data-stu-id="a979d-120">You can provide any value for this element.</span></span> <span data-ttu-id="a979d-121">使用範本部署資源時，這個值可用來確定使用的是正確的範本。</span><span class="sxs-lookup"><span data-stu-id="a979d-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="a979d-122">parameters</span><span class="sxs-lookup"><span data-stu-id="a979d-122">parameters</span></span> |<span data-ttu-id="a979d-123">否</span><span class="sxs-lookup"><span data-stu-id="a979d-123">No</span></span> |<span data-ttu-id="a979d-124">執行部署以自訂資源部署時所提供的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="a979d-125">variables</span><span class="sxs-lookup"><span data-stu-id="a979d-125">variables</span></span> |<span data-ttu-id="a979d-126">否</span><span class="sxs-lookup"><span data-stu-id="a979d-126">No</span></span> |<span data-ttu-id="a979d-127">範本中做為 JSON 片段以簡化範本語言運算式的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="a979d-128">resources</span><span class="sxs-lookup"><span data-stu-id="a979d-128">resources</span></span> |<span data-ttu-id="a979d-129">是</span><span class="sxs-lookup"><span data-stu-id="a979d-129">Yes</span></span> |<span data-ttu-id="a979d-130">在資源群組中部署或更新的資源類型。</span><span class="sxs-lookup"><span data-stu-id="a979d-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="a979d-131">outputs</span><span class="sxs-lookup"><span data-stu-id="a979d-131">outputs</span></span> |<span data-ttu-id="a979d-132">否</span><span class="sxs-lookup"><span data-stu-id="a979d-132">No</span></span> |<span data-ttu-id="a979d-133">部署後傳回的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="a979d-134">每個元素都包含可以設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="a979d-134">Each element contains properties you can set.</span></span> <span data-ttu-id="a979d-135">下列範例包含範本的完整語法：</span><span class="sxs-lookup"><span data-stu-id="a979d-135">The following example contains the full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-the parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="a979d-136">我們在本主題稍後更詳細探討範本的各個區段。</span><span class="sxs-lookup"><span data-stu-id="a979d-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="a979d-137">運算式和函式</span><span class="sxs-lookup"><span data-stu-id="a979d-137">Expressions and functions</span></span>
<span data-ttu-id="a979d-138">範本的基本語法是 JSON。</span><span class="sxs-lookup"><span data-stu-id="a979d-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="a979d-139">不過，運算式和函式可延伸範本中提供的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="a979d-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="a979d-140">運算式是在 JSON 字串常值內撰寫，其第一個字元和最後一個字元分別為下列兩種方括號：`[` 和 `]`。</span><span class="sxs-lookup"><span data-stu-id="a979d-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="a979d-141">部署範本時，會評估運算式的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="a979d-142">雖然是以字串常值撰寫，評估運算式的結果，根據實際的運算式可能會是不同的 JSON 類型 (例如陣列或整數)。</span><span class="sxs-lookup"><span data-stu-id="a979d-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="a979d-143">針對開頭為方括號 `[` 的常值字串，若不要將它解譯為運算式，請加入額外的方括號，使字串開頭成為 `[[`。</span><span class="sxs-lookup"><span data-stu-id="a979d-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="a979d-144">一般而言，您可以將運算式搭配函數使用，以執行可設定部署的作業。</span><span class="sxs-lookup"><span data-stu-id="a979d-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="a979d-145">和在 JavaScript 中相同，函式呼叫的格式為 `functionName(arg1,arg2,arg3)`。</span><span class="sxs-lookup"><span data-stu-id="a979d-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="a979d-146">您可以使用點與 [index] 運算子來參考屬性。</span><span class="sxs-lookup"><span data-stu-id="a979d-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="a979d-147">下列範例將示範如何在結構化值時使用數個函數：</span><span class="sxs-lookup"><span data-stu-id="a979d-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="a979d-148">如需範本函數的完整清單，請參閱 [Azure 資源管理員範本函數](resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="a979d-149">參數</span><span class="sxs-lookup"><span data-stu-id="a979d-149">Parameters</span></span>
<span data-ttu-id="a979d-150">在範本的 parameters 區段中，您會指定可在部署資源時輸入的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="a979d-151">提供針對特定環境 (例如開發、測試和生產環境) 量身訂做的參數值，可讓您自訂部署。</span><span class="sxs-lookup"><span data-stu-id="a979d-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="a979d-152">您不必在範本中提供參數，但若沒有參數，您的範本一律會部署具有相同名稱、位置和屬性的相同資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="a979d-153">您會定義結構如下的參數：</span><span class="sxs-lookup"><span data-stu-id="a979d-153">You define parameters with the following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="a979d-154">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a979d-154">Element name</span></span> | <span data-ttu-id="a979d-155">必要</span><span class="sxs-lookup"><span data-stu-id="a979d-155">Required</span></span> | <span data-ttu-id="a979d-156">說明</span><span class="sxs-lookup"><span data-stu-id="a979d-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a979d-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="a979d-157">parameterName</span></span> |<span data-ttu-id="a979d-158">是</span><span class="sxs-lookup"><span data-stu-id="a979d-158">Yes</span></span> |<span data-ttu-id="a979d-159">參數名稱。</span><span class="sxs-lookup"><span data-stu-id="a979d-159">Name of the parameter.</span></span> <span data-ttu-id="a979d-160">必須是有效的 JavaScript 識別碼。</span><span class="sxs-lookup"><span data-stu-id="a979d-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="a979d-161">type</span><span class="sxs-lookup"><span data-stu-id="a979d-161">type</span></span> |<span data-ttu-id="a979d-162">是</span><span class="sxs-lookup"><span data-stu-id="a979d-162">Yes</span></span> |<span data-ttu-id="a979d-163">參數值類型。</span><span class="sxs-lookup"><span data-stu-id="a979d-163">Type of the parameter value.</span></span> <span data-ttu-id="a979d-164">請參閱此表格之後的允許類型清單。</span><span class="sxs-lookup"><span data-stu-id="a979d-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="a979d-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="a979d-165">defaultValue</span></span> |<span data-ttu-id="a979d-166">否</span><span class="sxs-lookup"><span data-stu-id="a979d-166">No</span></span> |<span data-ttu-id="a979d-167">如果未提供參數值，則會使用參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="a979d-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="a979d-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="a979d-168">allowedValues</span></span> |<span data-ttu-id="a979d-169">否</span><span class="sxs-lookup"><span data-stu-id="a979d-169">No</span></span> |<span data-ttu-id="a979d-170">參數的允許值陣列，確保提供正確的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="a979d-171">minValue</span><span class="sxs-lookup"><span data-stu-id="a979d-171">minValue</span></span> |<span data-ttu-id="a979d-172">否</span><span class="sxs-lookup"><span data-stu-id="a979d-172">No</span></span> |<span data-ttu-id="a979d-173">int 類型參數的最小值，含此值。</span><span class="sxs-lookup"><span data-stu-id="a979d-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="a979d-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="a979d-174">maxValue</span></span> |<span data-ttu-id="a979d-175">否</span><span class="sxs-lookup"><span data-stu-id="a979d-175">No</span></span> |<span data-ttu-id="a979d-176">int 類型參數的最大值，含此值。</span><span class="sxs-lookup"><span data-stu-id="a979d-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="a979d-177">minLength</span><span class="sxs-lookup"><span data-stu-id="a979d-177">minLength</span></span> |<span data-ttu-id="a979d-178">否</span><span class="sxs-lookup"><span data-stu-id="a979d-178">No</span></span> |<span data-ttu-id="a979d-179">字串、secureString 及陣列類型參數長度的最小值，含此值。</span><span class="sxs-lookup"><span data-stu-id="a979d-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="a979d-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="a979d-180">maxLength</span></span> |<span data-ttu-id="a979d-181">否</span><span class="sxs-lookup"><span data-stu-id="a979d-181">No</span></span> |<span data-ttu-id="a979d-182">字串、secureString 及陣列類型參數長度的最大值，含此值。</span><span class="sxs-lookup"><span data-stu-id="a979d-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="a979d-183">description</span><span class="sxs-lookup"><span data-stu-id="a979d-183">description</span></span> |<span data-ttu-id="a979d-184">否</span><span class="sxs-lookup"><span data-stu-id="a979d-184">No</span></span> |<span data-ttu-id="a979d-185">透過入口網站向使用者顯示的參數說明。</span><span class="sxs-lookup"><span data-stu-id="a979d-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="a979d-186">允許的類型和值為：</span><span class="sxs-lookup"><span data-stu-id="a979d-186">The allowed types and values are:</span></span>

* <span data-ttu-id="a979d-187">**字串**</span><span class="sxs-lookup"><span data-stu-id="a979d-187">**string**</span></span>
* <span data-ttu-id="a979d-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="a979d-188">**secureString**</span></span>
* <span data-ttu-id="a979d-189">**int**</span><span class="sxs-lookup"><span data-stu-id="a979d-189">**int**</span></span>
* <span data-ttu-id="a979d-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="a979d-190">**bool**</span></span>
* <span data-ttu-id="a979d-191">**object**</span><span class="sxs-lookup"><span data-stu-id="a979d-191">**object**</span></span> 
* <span data-ttu-id="a979d-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="a979d-192">**secureObject**</span></span>
* <span data-ttu-id="a979d-193">**array**</span><span class="sxs-lookup"><span data-stu-id="a979d-193">**array**</span></span>

<span data-ttu-id="a979d-194">若要將參數指定為選用，請提供 defaultValue (可為空字串)。</span><span class="sxs-lookup"><span data-stu-id="a979d-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="a979d-195">如果您在範本中指定的參數名稱和要部署範本的命令中的參數相符，提供的值就有可能模稜兩可。</span><span class="sxs-lookup"><span data-stu-id="a979d-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="a979d-196">Resource Manager 會在範本參數加上後置詞 **FromTemplate** 以避免混淆。</span><span class="sxs-lookup"><span data-stu-id="a979d-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="a979d-197">例如，如果您在範本中包含名為 **ResourceGroupName** 的參數，這會與 [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) Cmdlet 中的 **ResourceGroupName** 參數發生衝突。</span><span class="sxs-lookup"><span data-stu-id="a979d-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="a979d-198">部署期間，系統會提示您為 **ResourceGroupNameFromTemplate** 提供值。</span><span class="sxs-lookup"><span data-stu-id="a979d-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="a979d-199">一般而言，在為參數命名時，請勿使用與部署作業所用參數相同的名稱，以避免發生這種混淆的情形。</span><span class="sxs-lookup"><span data-stu-id="a979d-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="a979d-200">所有密碼、金鑰和其他密碼都應該使用 **secureString** 類型。</span><span class="sxs-lookup"><span data-stu-id="a979d-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="a979d-201">如果您在 JSON 物件中傳遞敏感資料，請使用 **secureObject** 類型。</span><span class="sxs-lookup"><span data-stu-id="a979d-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="a979d-202">部署資源後，無法讀取類型為 secureString 或 secureObject 的範本參數。</span><span class="sxs-lookup"><span data-stu-id="a979d-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="a979d-203">例如，在部署歷程記錄中，下列項目會顯示字串和物件的值，但不會顯示 secureString 和 secureObject 的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![show deployment values](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="a979d-205">下列範例示範如何定義參數：</span><span class="sxs-lookup"><span data-stu-id="a979d-205">The following example shows how to define parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="a979d-206">如需如何在部署期間輸入參數值的資訊，請參閱 [使用 Azure Resource Manager 範本部署資源](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="a979d-207">變數</span><span class="sxs-lookup"><span data-stu-id="a979d-207">Variables</span></span>
<span data-ttu-id="a979d-208">在 variables 區段中，您會建構可用於整個範本中的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="a979d-209">您不需要定義變數，但它們通常會經由減少複雜運算式來簡化您的範本。</span><span class="sxs-lookup"><span data-stu-id="a979d-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="a979d-210">您可使用以下結構定義變數：</span><span class="sxs-lookup"><span data-stu-id="a979d-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="a979d-211">下列範例說明如何定義由兩個參數值建構的變數：</span><span class="sxs-lookup"><span data-stu-id="a979d-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="a979d-212">接下來的範例說明複雜 JSON 類型的變數，以及由其他變數建構的變數：</span><span class="sxs-lookup"><span data-stu-id="a979d-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="a979d-213">資源</span><span class="sxs-lookup"><span data-stu-id="a979d-213">Resources</span></span>
<span data-ttu-id="a979d-214">在資源區段中，您會定義要部署或更新的資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="a979d-215">此區段會變得複雜，因為您必須了解您要部署的類型才能提供正確的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="a979d-216">針對您必須設定的資源特定值 (apiVersion、類型及屬性)，請參閱[定義 Azure Resource Manager 範本中的資源](/azure/templates/)。</span><span class="sxs-lookup"><span data-stu-id="a979d-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="a979d-217">您會定義結構如下的資源：</span><span class="sxs-lookup"><span data-stu-id="a979d-217">You define resources with the following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="a979d-218">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a979d-218">Element name</span></span> | <span data-ttu-id="a979d-219">必要</span><span class="sxs-lookup"><span data-stu-id="a979d-219">Required</span></span> | <span data-ttu-id="a979d-220">說明</span><span class="sxs-lookup"><span data-stu-id="a979d-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a979d-221">condition</span><span class="sxs-lookup"><span data-stu-id="a979d-221">condition</span></span> | <span data-ttu-id="a979d-222">否</span><span class="sxs-lookup"><span data-stu-id="a979d-222">No</span></span> | <span data-ttu-id="a979d-223">布林值，表示是否已部署資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="a979d-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a979d-224">apiVersion</span></span> |<span data-ttu-id="a979d-225">是</span><span class="sxs-lookup"><span data-stu-id="a979d-225">Yes</span></span> |<span data-ttu-id="a979d-226">要用來建立資源的 REST API 版本。</span><span class="sxs-lookup"><span data-stu-id="a979d-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="a979d-227">type</span><span class="sxs-lookup"><span data-stu-id="a979d-227">type</span></span> |<span data-ttu-id="a979d-228">是</span><span class="sxs-lookup"><span data-stu-id="a979d-228">Yes</span></span> |<span data-ttu-id="a979d-229">資源類型。</span><span class="sxs-lookup"><span data-stu-id="a979d-229">Type of the resource.</span></span> <span data-ttu-id="a979d-230">這個值是資源提供者的命名空間與資源類型的組合 (例如 **Microsoft.Storage/storageAccounts**)。</span><span class="sxs-lookup"><span data-stu-id="a979d-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="a979d-231">name</span><span class="sxs-lookup"><span data-stu-id="a979d-231">name</span></span> |<span data-ttu-id="a979d-232">是</span><span class="sxs-lookup"><span data-stu-id="a979d-232">Yes</span></span> |<span data-ttu-id="a979d-233">資源名稱。</span><span class="sxs-lookup"><span data-stu-id="a979d-233">Name of the resource.</span></span> <span data-ttu-id="a979d-234">此名稱必須遵循在 RFC3986 中定義的 URI 元件限制。</span><span class="sxs-lookup"><span data-stu-id="a979d-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="a979d-235">此外，將資源名稱公開到外部合作對象的 Azure 服務會驗證該名稱，確定不是有人嘗試詐騙其他身分識別。</span><span class="sxs-lookup"><span data-stu-id="a979d-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="a979d-236">location</span><span class="sxs-lookup"><span data-stu-id="a979d-236">location</span></span> |<span data-ttu-id="a979d-237">視情況而異</span><span class="sxs-lookup"><span data-stu-id="a979d-237">Varies</span></span> |<span data-ttu-id="a979d-238">所提供資源的支援地理位置。</span><span class="sxs-lookup"><span data-stu-id="a979d-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="a979d-239">您可以選取任何可用的位置，但通常選擇接近您的使用者的位置很合理。</span><span class="sxs-lookup"><span data-stu-id="a979d-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="a979d-240">通常，將彼此互動的資源放在相同區域也合乎常理。</span><span class="sxs-lookup"><span data-stu-id="a979d-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="a979d-241">大部分的資源類型都需要有位置，但某些類型 (例如角色指派) 不需要位置。</span><span class="sxs-lookup"><span data-stu-id="a979d-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="a979d-242">請參閱[設定 Azure Resource Manager 範本中的資源位置](resource-manager-template-location.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="a979d-243">tags</span><span class="sxs-lookup"><span data-stu-id="a979d-243">tags</span></span> |<span data-ttu-id="a979d-244">否</span><span class="sxs-lookup"><span data-stu-id="a979d-244">No</span></span> |<span data-ttu-id="a979d-245">與資源相關聯的標記。</span><span class="sxs-lookup"><span data-stu-id="a979d-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="a979d-246">請參閱[標記 Azure Resource Manager 範本中的資源](resource-manager-template-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="a979d-247">comments</span><span class="sxs-lookup"><span data-stu-id="a979d-247">comments</span></span> |<span data-ttu-id="a979d-248">否</span><span class="sxs-lookup"><span data-stu-id="a979d-248">No</span></span> |<span data-ttu-id="a979d-249">您在範本中記錄資源的註解</span><span class="sxs-lookup"><span data-stu-id="a979d-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="a979d-250">copy</span><span class="sxs-lookup"><span data-stu-id="a979d-250">copy</span></span> |<span data-ttu-id="a979d-251">否</span><span class="sxs-lookup"><span data-stu-id="a979d-251">No</span></span> |<span data-ttu-id="a979d-252">如果需要多個執行個體，要建立的資源數目。</span><span class="sxs-lookup"><span data-stu-id="a979d-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="a979d-253">預設模式為平行。</span><span class="sxs-lookup"><span data-stu-id="a979d-253">The default mode is parallel.</span></span> <span data-ttu-id="a979d-254">如果您不想要同時部署所有或某些資源，請指定序列模式。</span><span class="sxs-lookup"><span data-stu-id="a979d-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="a979d-255">如需詳細資訊，請參閱[在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="a979d-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="a979d-256">dependsOn</span></span> |<span data-ttu-id="a979d-257">否</span><span class="sxs-lookup"><span data-stu-id="a979d-257">No</span></span> |<span data-ttu-id="a979d-258">在部署這項資源之前必須部署的資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="a979d-259">Resource Manager 會評估資源之間的相依性，並依正確的順序進行部署。</span><span class="sxs-lookup"><span data-stu-id="a979d-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="a979d-260">資源若不互相依賴，則會平行部署資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="a979d-261">值可以是以逗號分隔的資源名稱或資源唯一識別碼清單。</span><span class="sxs-lookup"><span data-stu-id="a979d-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="a979d-262">只會列出此範本中已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="a979d-263">此範本中未定義的資源必須已經存在。</span><span class="sxs-lookup"><span data-stu-id="a979d-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="a979d-264">避免加入不必要的相依性，因為可能會降低部署速度並產生循環相依性。</span><span class="sxs-lookup"><span data-stu-id="a979d-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="a979d-265">如需設定相依性的指引，請參閱[定義 Azure Resource Manager 範本中的相依性](resource-group-define-dependencies.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="a979d-266">properties</span><span class="sxs-lookup"><span data-stu-id="a979d-266">properties</span></span> |<span data-ttu-id="a979d-267">否</span><span class="sxs-lookup"><span data-stu-id="a979d-267">No</span></span> |<span data-ttu-id="a979d-268">資源特定的組態設定。</span><span class="sxs-lookup"><span data-stu-id="a979d-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="a979d-269">屬性的值和您在 REST API 作業 (PUT 方法) 要求主體中提供來建立資源的值是一樣的。</span><span class="sxs-lookup"><span data-stu-id="a979d-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="a979d-270">您也可以指定複本陣列，以建立屬性的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="a979d-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="a979d-271">如需詳細資訊，請參閱[在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="a979d-272">resources</span><span class="sxs-lookup"><span data-stu-id="a979d-272">resources</span></span> |<span data-ttu-id="a979d-273">否</span><span class="sxs-lookup"><span data-stu-id="a979d-273">No</span></span> |<span data-ttu-id="a979d-274">與正在定義的資源相依的下層資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="a979d-275">只提供父資源的結構描述允許的資源類型。</span><span class="sxs-lookup"><span data-stu-id="a979d-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="a979d-276">子資源的完整類型包含父資源類型，例如 **Microsoft.Web/sites/extensions**。</span><span class="sxs-lookup"><span data-stu-id="a979d-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="a979d-277">沒有隱含父資源的相依性。</span><span class="sxs-lookup"><span data-stu-id="a979d-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="a979d-278">您必須明確定義該相依性。</span><span class="sxs-lookup"><span data-stu-id="a979d-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="a979d-279">resources 區段包含要部署的資源陣列。</span><span class="sxs-lookup"><span data-stu-id="a979d-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="a979d-280">在每個資源內，您也可以定義子資源陣列。</span><span class="sxs-lookup"><span data-stu-id="a979d-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="a979d-281">因此，您的 resources 區段可能會有類似以下的結構：</span><span class="sxs-lookup"><span data-stu-id="a979d-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="a979d-282">如需定義子資源的詳細資訊，請參閱[在 Resource Manager 範本中設定子資源的名稱和類型](resource-manager-template-child-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="a979d-283">**condition** 元素會指定是否要部署資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="a979d-284">此元素的值會解析為 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="a979d-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="a979d-285">例如，若要指定是否要部署新的儲存體帳戶，請使用：</span><span class="sxs-lookup"><span data-stu-id="a979d-285">For example, to specify whether a new storage account is deployed, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="a979d-286">如需使用新的或現有資源的範例，請參閱[新的或現有條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)。</span><span class="sxs-lookup"><span data-stu-id="a979d-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="a979d-287">若要指定是否要透過密碼或 SSH 金鑰部署虛擬機器，請在範本中定義兩個版本的虛擬機器，並使用 **condition** 區分使用情況。</span><span class="sxs-lookup"><span data-stu-id="a979d-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="a979d-288">傳遞可指定要部署哪個案例的參數。</span><span class="sxs-lookup"><span data-stu-id="a979d-288">Pass a parameter that specifies which scenario to deploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="a979d-289">如需使用密碼或 SSH 金鑰來部署虛擬機器的範例，請參閱[使用者名稱或 SSH 條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)。</span><span class="sxs-lookup"><span data-stu-id="a979d-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="a979d-290">輸出</span><span class="sxs-lookup"><span data-stu-id="a979d-290">Outputs</span></span>
<span data-ttu-id="a979d-291">在輸出區段中，您可以指定從部署傳回的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="a979d-292">例如，您可以傳回 URI 以存取所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="a979d-293">下列範例顯示輸出定義的結構：</span><span class="sxs-lookup"><span data-stu-id="a979d-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="a979d-294">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a979d-294">Element name</span></span> | <span data-ttu-id="a979d-295">必要</span><span class="sxs-lookup"><span data-stu-id="a979d-295">Required</span></span> | <span data-ttu-id="a979d-296">說明</span><span class="sxs-lookup"><span data-stu-id="a979d-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a979d-297">outputName</span><span class="sxs-lookup"><span data-stu-id="a979d-297">outputName</span></span> |<span data-ttu-id="a979d-298">是</span><span class="sxs-lookup"><span data-stu-id="a979d-298">Yes</span></span> |<span data-ttu-id="a979d-299">輸出值的名稱。</span><span class="sxs-lookup"><span data-stu-id="a979d-299">Name of the output value.</span></span> <span data-ttu-id="a979d-300">必須是有效的 JavaScript 識別碼。</span><span class="sxs-lookup"><span data-stu-id="a979d-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="a979d-301">type</span><span class="sxs-lookup"><span data-stu-id="a979d-301">type</span></span> |<span data-ttu-id="a979d-302">是</span><span class="sxs-lookup"><span data-stu-id="a979d-302">Yes</span></span> |<span data-ttu-id="a979d-303">輸出值的類型。</span><span class="sxs-lookup"><span data-stu-id="a979d-303">Type of the output value.</span></span> <span data-ttu-id="a979d-304">輸出值支援與範本輸入參數相同的類型。</span><span class="sxs-lookup"><span data-stu-id="a979d-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="a979d-305">value</span><span class="sxs-lookup"><span data-stu-id="a979d-305">value</span></span> |<span data-ttu-id="a979d-306">是</span><span class="sxs-lookup"><span data-stu-id="a979d-306">Yes</span></span> |<span data-ttu-id="a979d-307">評估並傳回做為輸出值的範本語言運算式。</span><span class="sxs-lookup"><span data-stu-id="a979d-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="a979d-308">下列範例顯示在輸出區段中傳回的值。</span><span class="sxs-lookup"><span data-stu-id="a979d-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="a979d-309">如需使用輸出的相關資訊，請參閱 [Azure Resource Manager 範本中的共用狀態](best-practices-resource-manager-state.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="a979d-310">範本限制</span><span class="sxs-lookup"><span data-stu-id="a979d-310">Template limits</span></span>

<span data-ttu-id="a979d-311">將範本大小限制為 1 MB，並將每個參數檔案限制為 64 KB。</span><span class="sxs-lookup"><span data-stu-id="a979d-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="a979d-312">1 MB 的限制適用於已增加反覆資源定義和變數和參數值之範本的最終狀態。</span><span class="sxs-lookup"><span data-stu-id="a979d-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="a979d-313">您也受限於：</span><span class="sxs-lookup"><span data-stu-id="a979d-313">You are also limited to:</span></span>

* <span data-ttu-id="a979d-314">256 個參數</span><span class="sxs-lookup"><span data-stu-id="a979d-314">256 parameters</span></span>
* <span data-ttu-id="a979d-315">256 個變數</span><span class="sxs-lookup"><span data-stu-id="a979d-315">256 variables</span></span>
* <span data-ttu-id="a979d-316">800 個資源 (包括複本計數)</span><span class="sxs-lookup"><span data-stu-id="a979d-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="a979d-317">64 個輸出值</span><span class="sxs-lookup"><span data-stu-id="a979d-317">64 output values</span></span>
* <span data-ttu-id="a979d-318">範本運算式中的 24,576 個字元</span><span class="sxs-lookup"><span data-stu-id="a979d-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="a979d-319">使用巢狀範本，即可超出一些範本限制。</span><span class="sxs-lookup"><span data-stu-id="a979d-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="a979d-320">如需詳細資訊，請參閱[在部署 Azure 資源時使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="a979d-321">若要減少參數、變數或輸出數目，您可以將數個值合併成一個物件。</span><span class="sxs-lookup"><span data-stu-id="a979d-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="a979d-322">如需詳細資訊，請參閱[物件作為參數](resource-manager-objects-as-parameters.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a979d-323">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a979d-323">Next steps</span></span>
* <span data-ttu-id="a979d-324">若要檢視許多不同類型解決方案的完整範本，請參閱 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="a979d-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="a979d-325">如需您可以在範本內使用哪些函式的詳細資料，請參閱 [Azure Resource Manager 範本函式](resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="a979d-326">若要在部署期間合併多個範本，請參閱 [透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="a979d-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="a979d-327">您可能需要使用不同資源群組內的資源。</span><span class="sxs-lookup"><span data-stu-id="a979d-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="a979d-328">這案例常見於使用多個資源群組之間所共用的儲存體帳戶或虛擬網路時。</span><span class="sxs-lookup"><span data-stu-id="a979d-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="a979d-329">如需詳細資訊，請參閱 [resourceId 函式](resource-group-template-functions-resource.md#resourceid)。</span><span class="sxs-lookup"><span data-stu-id="a979d-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
