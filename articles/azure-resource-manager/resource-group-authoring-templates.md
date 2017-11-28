---
title: "aaaAzure 資源管理員範本結構和語法 |Microsoft 文件"
description: "描述 hello 結構以及使用 JSON 的宣告式語法的 Azure Resource Manager 範本的屬性。"
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
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="d4dd1-103">了解 hello 結構和語法的 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="d4dd1-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="d4dd1-104">本主題描述 Azure Resource Manager 範本 hello 結構。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="d4dd1-105">它會呈現 hello 的範本和 hello 可用屬性的這些章節中的各區段。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="d4dd1-106">hello 範本包含 JSON 和您可以為您的部署使用 tooconstruct 值的運算式。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="d4dd1-107">如需建立範本的逐步教學課程，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="d4dd1-108">範本格式</span><span class="sxs-lookup"><span data-stu-id="d4dd1-108">Template format</span></span>
<span data-ttu-id="d4dd1-109">在最簡單的結構中，範本包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d4dd1-109">In its simplest structure, a template contains hello following elements:</span></span>

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

| <span data-ttu-id="d4dd1-110">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d4dd1-110">Element name</span></span> | <span data-ttu-id="d4dd1-111">必要</span><span class="sxs-lookup"><span data-stu-id="d4dd1-111">Required</span></span> | <span data-ttu-id="d4dd1-112">說明</span><span class="sxs-lookup"><span data-stu-id="d4dd1-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4dd1-113">$schema</span><span class="sxs-lookup"><span data-stu-id="d4dd1-113">$schema</span></span> |<span data-ttu-id="d4dd1-114">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-114">Yes</span></span> |<span data-ttu-id="d4dd1-115">描述 hello hello 範本語言版本的 hello JSON 結構描述檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="d4dd1-116">使用 hello hello 前面範例所示的 URL。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="d4dd1-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="d4dd1-117">contentVersion</span></span> |<span data-ttu-id="d4dd1-118">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-118">Yes</span></span> |<span data-ttu-id="d4dd1-119">Hello 範本 （例如 1.0.0.0) 的版本。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="d4dd1-120">您可以為此元素提供任何值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-120">You can provide any value for this element.</span></span> <span data-ttu-id="d4dd1-121">在部署時使用 hello 範本的資源，這個值可以是使用的 toomake 確定已使用該 hello 是正確的範本。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="d4dd1-122">參數</span><span class="sxs-lookup"><span data-stu-id="d4dd1-122">parameters</span></span> |<span data-ttu-id="d4dd1-123">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-123">No</span></span> |<span data-ttu-id="d4dd1-124">部署時所提供的值執行 toocustomize 資源部署。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="d4dd1-125">variables</span><span class="sxs-lookup"><span data-stu-id="d4dd1-125">variables</span></span> |<span data-ttu-id="d4dd1-126">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-126">No</span></span> |<span data-ttu-id="d4dd1-127">會做為 JSON 片段 hello 範本 toosimplify 範本語言運算式中的值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="d4dd1-128">resources</span><span class="sxs-lookup"><span data-stu-id="d4dd1-128">resources</span></span> |<span data-ttu-id="d4dd1-129">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-129">Yes</span></span> |<span data-ttu-id="d4dd1-130">在資源群組中部署或更新的資源類型。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="d4dd1-131">outputs</span><span class="sxs-lookup"><span data-stu-id="d4dd1-131">outputs</span></span> |<span data-ttu-id="d4dd1-132">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-132">No</span></span> |<span data-ttu-id="d4dd1-133">部署後傳回的值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="d4dd1-134">每個元素都包含可以設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-134">Each element contains properties you can set.</span></span> <span data-ttu-id="d4dd1-135">下列範例中的 hello 包含 hello 範本的完整語法：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-135">hello following example contains hello full syntax for a template:</span></span>

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
                "description": "<description-of-hello parameter>" 
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

<span data-ttu-id="d4dd1-136">我們會檢查在本主題稍後的更詳細的 hello 範本 hello 區段。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="d4dd1-137">運算式和函式</span><span class="sxs-lookup"><span data-stu-id="d4dd1-137">Expressions and functions</span></span>
<span data-ttu-id="d4dd1-138">hello 的 hello 範本的基本語法為 JSON。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="d4dd1-139">不過，運算式和函數延伸 hello 範本內可用的 hello JSON 值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="d4dd1-140">運算式撰寫 JSON 字串常值內的第一個和最後一個字元是 hello 方括號：`[`和`]`分別。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="d4dd1-141">部署 hello 範本時，會評估 hello hello 運算式值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="d4dd1-142">寫入字串常值，同時 hello 運算式的評估 hello 結果可以是不同的 JSON 型別，例如陣列或根據 hello 實際運算式的整數。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="d4dd1-143">常值字串的開頭是括號 toohave `[`，而不是將它解譯為運算式，請加入一個額外的括號 toostart hello 字串`[[`。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="d4dd1-144">一般而言，您可以使用運算式的函式 tooperform 作業，用來設定 hello 部署和作業。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="d4dd1-145">和在 JavaScript 中相同，函式呼叫的格式為 `functionName(arg1,arg2,arg3)`。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="d4dd1-146">您可以使用 hello 點和 [index] 運算子，以參考屬性。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="d4dd1-147">下列範例中的 hello 顯示的 toouse 建構時，數個函數的值：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="d4dd1-148">Hello 的樣板函式的完整清單，請參閱[Azure Resource Manager 範本函式](resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="d4dd1-149">參數</span><span class="sxs-lookup"><span data-stu-id="d4dd1-149">Parameters</span></span>
<span data-ttu-id="d4dd1-150">在 hello 參數區段中的 hello 範本，您可以指定部署時，您可以輸入哪些值 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="d4dd1-151">這些參數值可讓您 toocustomize hello 部署 （例如開發、 測試和生產環境） 的特定環境提供量身訂做的值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="d4dd1-152">在範本中，沒有 tooprovide 參數，但不含參數範本會一律將部署 hello 與相同資源 hello 相同的名稱、 位置及內容。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="d4dd1-153">您可以定義參數以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-153">You define parameters with hello following structure:</span></span>

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
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="d4dd1-154">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d4dd1-154">Element name</span></span> | <span data-ttu-id="d4dd1-155">必要</span><span class="sxs-lookup"><span data-stu-id="d4dd1-155">Required</span></span> | <span data-ttu-id="d4dd1-156">說明</span><span class="sxs-lookup"><span data-stu-id="d4dd1-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4dd1-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="d4dd1-157">parameterName</span></span> |<span data-ttu-id="d4dd1-158">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-158">Yes</span></span> |<span data-ttu-id="d4dd1-159">Hello 參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-159">Name of hello parameter.</span></span> <span data-ttu-id="d4dd1-160">必須是有效的 JavaScript 識別碼。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="d4dd1-161">type</span><span class="sxs-lookup"><span data-stu-id="d4dd1-161">type</span></span> |<span data-ttu-id="d4dd1-162">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-162">Yes</span></span> |<span data-ttu-id="d4dd1-163">Hello 參數值的類型。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-163">Type of hello parameter value.</span></span> <span data-ttu-id="d4dd1-164">在此資料表之後，請參閱 hello 允許類型清單。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="d4dd1-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="d4dd1-165">defaultValue</span></span> |<span data-ttu-id="d4dd1-166">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-166">No</span></span> |<span data-ttu-id="d4dd1-167">Hello 參數，如果未不提供任何值為 hello 參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="d4dd1-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="d4dd1-168">allowedValues</span></span> |<span data-ttu-id="d4dd1-169">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-169">No</span></span> |<span data-ttu-id="d4dd1-170">允許的值為 hello 參數 toomake 確定係 hello 右值的陣列。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="d4dd1-171">minValue</span><span class="sxs-lookup"><span data-stu-id="d4dd1-171">minValue</span></span> |<span data-ttu-id="d4dd1-172">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-172">No</span></span> |<span data-ttu-id="d4dd1-173">hello int 型別參數的最小值，這個值都包含在內。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="d4dd1-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="d4dd1-174">maxValue</span></span> |<span data-ttu-id="d4dd1-175">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-175">No</span></span> |<span data-ttu-id="d4dd1-176">hello int 型別參數的最大值，這個值都包含在內。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="d4dd1-177">minLength</span><span class="sxs-lookup"><span data-stu-id="d4dd1-177">minLength</span></span> |<span data-ttu-id="d4dd1-178">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-178">No</span></span> |<span data-ttu-id="d4dd1-179">hello 的最小長度字串、 secureString 和陣列型別參數，這個值都包含在內。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="d4dd1-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="d4dd1-180">maxLength</span></span> |<span data-ttu-id="d4dd1-181">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-181">No</span></span> |<span data-ttu-id="d4dd1-182">hello 最大長度字串、 secureString 和陣列型別參數，這個值都包含在內。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="d4dd1-183">說明</span><span class="sxs-lookup"><span data-stu-id="d4dd1-183">description</span></span> |<span data-ttu-id="d4dd1-184">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-184">No</span></span> |<span data-ttu-id="d4dd1-185">Toousers 透過 hello 入口網站顯示 hello 參數的描述。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="d4dd1-186">hello 允許的類型和值如下：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="d4dd1-187">**字串**</span><span class="sxs-lookup"><span data-stu-id="d4dd1-187">**string**</span></span>
* <span data-ttu-id="d4dd1-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="d4dd1-188">**secureString**</span></span>
* <span data-ttu-id="d4dd1-189">**int**</span><span class="sxs-lookup"><span data-stu-id="d4dd1-189">**int**</span></span>
* <span data-ttu-id="d4dd1-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="d4dd1-190">**bool**</span></span>
* <span data-ttu-id="d4dd1-191">**object**</span><span class="sxs-lookup"><span data-stu-id="d4dd1-191">**object**</span></span> 
* <span data-ttu-id="d4dd1-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="d4dd1-192">**secureObject**</span></span>
* <span data-ttu-id="d4dd1-193">**array**</span><span class="sxs-lookup"><span data-stu-id="d4dd1-193">**array**</span></span>

<span data-ttu-id="d4dd1-194">toospecify 參數為選擇性，提供預設值 （可以是空字串）。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="d4dd1-195">如果您在範本符合 hello 命令 toodeploy hello 範本中的參數中指定參數名稱，沒有關於 hello 所提供的值可能模稜兩可。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="d4dd1-196">資源管理員會藉由新增 hello 後置解析混淆**FromTemplate** toohello 樣板參數。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="d4dd1-197">例如，如果您包含名為的參數**ResourceGroupName**在範本中，與衝突 hello **ResourceGroupName**中 hello 參數[新 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="d4dd1-198">在部署期間，您會提示的 tooprovide 值**ResourceGroupNameFromTemplate**。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="d4dd1-199">一般情況下，您應該避免混淆，未指名參數，以做為部署作業所使用的參數名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="d4dd1-200">所有密碼、 金鑰和其他機密資料，則應該使用 hello **secureString**型別。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="d4dd1-201">如果您在 JSON 物件傳送機密資料，使用 hello **secureObject**型別。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="d4dd1-202">部署資源後，無法讀取類型為 secureString 或 secureObject 的範本參數。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="d4dd1-203">例如，hello hello 部署歷程記錄中的下列項目會顯示 hello 值對字串和物件，但對 secureString 和 secureObject。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![show deployment values](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="d4dd1-205">下列範例會示範如何 hello toodefine 參數：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-205">hello following example shows how toodefine parameters:</span></span>

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

<span data-ttu-id="d4dd1-206">如何 tooinput hello 參數值在部署期間，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="d4dd1-207">變數</span><span class="sxs-lookup"><span data-stu-id="d4dd1-207">Variables</span></span>
<span data-ttu-id="d4dd1-208">在 hello 變數區段中，您可以建構可用的值在您的範本。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="d4dd1-209">您不需要 toodefine 變數，但是它們通常範本減少簡化複雜運算式。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="d4dd1-210">您可以定義變數以下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="d4dd1-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="d4dd1-211">下列範例會示範如何 hello toodefine 建構自兩個參數值的變數：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="d4dd1-212">hello 下一個範例顯示的變數是複雜的 JSON 型別和從其他變數建構的變數：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="d4dd1-213">資源</span><span class="sxs-lookup"><span data-stu-id="d4dd1-213">Resources</span></span>
<span data-ttu-id="d4dd1-214">在 hello 資源區段中，您可以定義 hello 資源是已部署或更新。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="d4dd1-215">本章節變得複雜，因為您必須了解 hello 類型與您要部署 tooprovide hello 正確的值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="d4dd1-216">如需 hello 特定資源值 （Microsoft.authorization、 類型和屬性），您需要 tooset，請參閱[Azure Resource Manager 範本中定義的資源](/azure/templates/)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="d4dd1-217">您可以定義資源以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-217">You define resources with hello following structure:</span></span>

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

| <span data-ttu-id="d4dd1-218">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d4dd1-218">Element name</span></span> | <span data-ttu-id="d4dd1-219">必要</span><span class="sxs-lookup"><span data-stu-id="d4dd1-219">Required</span></span> | <span data-ttu-id="d4dd1-220">說明</span><span class="sxs-lookup"><span data-stu-id="d4dd1-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4dd1-221">condition</span><span class="sxs-lookup"><span data-stu-id="d4dd1-221">condition</span></span> | <span data-ttu-id="d4dd1-222">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-222">No</span></span> | <span data-ttu-id="d4dd1-223">布林值，指出是否要部署 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="d4dd1-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d4dd1-224">apiVersion</span></span> |<span data-ttu-id="d4dd1-225">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-225">Yes</span></span> |<span data-ttu-id="d4dd1-226">Hello REST API toouse 建立 hello 資源的版本。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="d4dd1-227">類型</span><span class="sxs-lookup"><span data-stu-id="d4dd1-227">type</span></span> |<span data-ttu-id="d4dd1-228">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-228">Yes</span></span> |<span data-ttu-id="d4dd1-229">Hello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-229">Type of hello resource.</span></span> <span data-ttu-id="d4dd1-230">這個值是 hello hello 資源提供者和 hello 資源類型的命名空間的組合 (例如**microsoft.storage /**)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="d4dd1-231">名稱</span><span class="sxs-lookup"><span data-stu-id="d4dd1-231">name</span></span> |<span data-ttu-id="d4dd1-232">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-232">Yes</span></span> |<span data-ttu-id="d4dd1-233">Hello 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-233">Name of hello resource.</span></span> <span data-ttu-id="d4dd1-234">hello 名稱必須遵照 RFC3986 中定義的 URI 元件限制。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="d4dd1-235">此外，Azure hello 資源名稱 toooutside 合作對象所公開的服務驗證 hello 名稱 toomake 確定它不是嘗試 toospoof 其他身分識別。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="d4dd1-236">location</span><span class="sxs-lookup"><span data-stu-id="d4dd1-236">location</span></span> |<span data-ttu-id="d4dd1-237">視情況而異</span><span class="sxs-lookup"><span data-stu-id="d4dd1-237">Varies</span></span> |<span data-ttu-id="d4dd1-238">提供資源的 hello 的支援的地理位置。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="d4dd1-239">您可以選取任何 hello 可用的位置，但通常它使意義 toopick 是關閉 tooyour 使用者。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="d4dd1-240">通常，也是合理 tooplace 資源彼此互動 hello 中相同的區域。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="d4dd1-241">大部分的資源類型都需要有位置，但某些類型 (例如角色指派) 不需要位置。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="d4dd1-242">請參閱[設定 Azure Resource Manager 範本中的資源位置](resource-manager-template-location.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="d4dd1-243">tags</span><span class="sxs-lookup"><span data-stu-id="d4dd1-243">tags</span></span> |<span data-ttu-id="d4dd1-244">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-244">No</span></span> |<span data-ttu-id="d4dd1-245">Hello 資源相關聯的標記。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="d4dd1-246">請參閱[標記 Azure Resource Manager 範本中的資源](resource-manager-template-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="d4dd1-247">comments</span><span class="sxs-lookup"><span data-stu-id="d4dd1-247">comments</span></span> |<span data-ttu-id="d4dd1-248">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-248">No</span></span> |<span data-ttu-id="d4dd1-249">記錄您的範本中的 hello 資源便箋</span><span class="sxs-lookup"><span data-stu-id="d4dd1-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="d4dd1-250">copy</span><span class="sxs-lookup"><span data-stu-id="d4dd1-250">copy</span></span> |<span data-ttu-id="d4dd1-251">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-251">No</span></span> |<span data-ttu-id="d4dd1-252">如果需要多個執行個體，則 hello 資源 toocreate 數目。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="d4dd1-253">hello 預設模式是平行處理。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-253">hello default mode is parallel.</span></span> <span data-ttu-id="d4dd1-254">指定序列的模式，當您不想要所有或 hello 資源 toodeploy hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="d4dd1-255">如需詳細資訊，請參閱[在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="d4dd1-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="d4dd1-256">dependsOn</span></span> |<span data-ttu-id="d4dd1-257">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-257">No</span></span> |<span data-ttu-id="d4dd1-258">在部署這項資源之前必須部署的資源。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="d4dd1-259">資源管理員會評估 hello 資源之間的相依性，並將它們部署在 hello 正確的順序。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="d4dd1-260">資源若不互相依賴，則會平行部署資源。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="d4dd1-261">hello 值可以是以逗號分隔的清單資源名稱或資源的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="d4dd1-262">只會列出此範本中已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="d4dd1-263">此範本中未定義的資源必須已經存在。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="d4dd1-264">避免加入不必要的相依性，因為可能會降低部署速度並產生循環相依性。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="d4dd1-265">如需設定相依性的指引，請參閱[定義 Azure Resource Manager 範本中的相依性](resource-group-define-dependencies.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="d4dd1-266">properties</span><span class="sxs-lookup"><span data-stu-id="d4dd1-266">properties</span></span> |<span data-ttu-id="d4dd1-267">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-267">No</span></span> |<span data-ttu-id="d4dd1-268">資源特定的組態設定。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="d4dd1-269">hello hello 屬性值是 hello 做為您提供 hello 要求主體中的 hello REST API 作業 （PUT 方法） toocreate hello 資源 hello 值相同。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="d4dd1-270">您也可以指定複製陣列 toocreate 屬性的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="d4dd1-271">如需詳細資訊，請參閱[在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="d4dd1-272">resources</span><span class="sxs-lookup"><span data-stu-id="d4dd1-272">resources</span></span> |<span data-ttu-id="d4dd1-273">否</span><span class="sxs-lookup"><span data-stu-id="d4dd1-273">No</span></span> |<span data-ttu-id="d4dd1-274">正在定義的 hello 資源而定的子資源。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="d4dd1-275">僅提供所允許的 hello hello 父資源結構描述的資源類型。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="d4dd1-276">hello hello 子資源的完整型別包含 hello 父資源類型，例如**Microsoft.Web/sites/extensions**。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="d4dd1-277">沒有隱含 hello 父資源上的相依性。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="d4dd1-278">您必須明確定義該相依性。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="d4dd1-279">hello 資源區段包含 hello 資源 toodeploy 的陣列。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="d4dd1-280">在每個資源內，您也可以定義子資源陣列。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="d4dd1-281">因此，您的 resources 區段可能會有類似以下的結構：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="d4dd1-282">如需定義子資源的詳細資訊，請參閱[在 Resource Manager 範本中設定子資源的名稱和類型](resource-manager-template-child-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="d4dd1-283">hello**條件**項目會指定是否要部署 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="d4dd1-284">此項目的 hello 值解析 tootrue 或 false。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="d4dd1-285">比方說，toospecify 是否在部署新的儲存體帳戶時，使用：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="d4dd1-286">如需使用新的或現有資源的範例，請參閱[新的或現有條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="d4dd1-287">toospecify 是否以密碼或 SSH 金鑰部署虛擬機器定義兩個版本的 hello 虛擬機器在您的範本並使用**條件**toodifferentiate 使用量。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="d4dd1-288">傳遞的參數會指定哪一個案例 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

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

<span data-ttu-id="d4dd1-289">如需使用密碼或 SSH 金鑰 toodeploy 虛擬機器的範例，請參閱[使用者名稱或 SSH 條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="d4dd1-290">輸出</span><span class="sxs-lookup"><span data-stu-id="d4dd1-290">Outputs</span></span>
<span data-ttu-id="d4dd1-291">在 hello 輸出區段中，您可以指定從部署所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="d4dd1-292">例如，您可能會傳回 hello URI tooaccess 已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="d4dd1-293">hello 下列範例顯示輸出定義 hello 的結構：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="d4dd1-294">元素名稱</span><span class="sxs-lookup"><span data-stu-id="d4dd1-294">Element name</span></span> | <span data-ttu-id="d4dd1-295">必要</span><span class="sxs-lookup"><span data-stu-id="d4dd1-295">Required</span></span> | <span data-ttu-id="d4dd1-296">說明</span><span class="sxs-lookup"><span data-stu-id="d4dd1-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d4dd1-297">outputName</span><span class="sxs-lookup"><span data-stu-id="d4dd1-297">outputName</span></span> |<span data-ttu-id="d4dd1-298">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-298">Yes</span></span> |<span data-ttu-id="d4dd1-299">Hello 輸出值的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-299">Name of hello output value.</span></span> <span data-ttu-id="d4dd1-300">必須是有效的 JavaScript 識別碼。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="d4dd1-301">type</span><span class="sxs-lookup"><span data-stu-id="d4dd1-301">type</span></span> |<span data-ttu-id="d4dd1-302">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-302">Yes</span></span> |<span data-ttu-id="d4dd1-303">Hello 輸出值的類型。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-303">Type of hello output value.</span></span> <span data-ttu-id="d4dd1-304">輸出值支援在 hello 相同類型做為範本的輸入參數。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="d4dd1-305">value</span><span class="sxs-lookup"><span data-stu-id="d4dd1-305">value</span></span> |<span data-ttu-id="d4dd1-306">是</span><span class="sxs-lookup"><span data-stu-id="d4dd1-306">Yes</span></span> |<span data-ttu-id="d4dd1-307">評估並傳回做為輸出值的範本語言運算式。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="d4dd1-308">hello 下列範例顯示傳回 hello 輸出區段中的值。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="d4dd1-309">如需使用輸出的相關資訊，請參閱 [Azure Resource Manager 範本中的共用狀態](best-practices-resource-manager-state.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="d4dd1-310">範本限制</span><span class="sxs-lookup"><span data-stu-id="d4dd1-310">Template limits</span></span>

<span data-ttu-id="d4dd1-311">Hello 大小限制的範本 too1 MB，而每個參數檔案 too64 KB。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="d4dd1-312">它已擴充與反覆的資源定義和變數和參數值之後，hello 1 MB 的限制會套用 hello 範本 toohello 最終狀態。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="d4dd1-313">您也受限於：</span><span class="sxs-lookup"><span data-stu-id="d4dd1-313">You are also limited to:</span></span>

* <span data-ttu-id="d4dd1-314">256 個參數</span><span class="sxs-lookup"><span data-stu-id="d4dd1-314">256 parameters</span></span>
* <span data-ttu-id="d4dd1-315">256 個變數</span><span class="sxs-lookup"><span data-stu-id="d4dd1-315">256 variables</span></span>
* <span data-ttu-id="d4dd1-316">800 個資源 (包括複本計數)</span><span class="sxs-lookup"><span data-stu-id="d4dd1-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="d4dd1-317">64 個輸出值</span><span class="sxs-lookup"><span data-stu-id="d4dd1-317">64 output values</span></span>
* <span data-ttu-id="d4dd1-318">範本運算式中的 24,576 個字元</span><span class="sxs-lookup"><span data-stu-id="d4dd1-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="d4dd1-319">使用巢狀範本，即可超出一些範本限制。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="d4dd1-320">如需詳細資訊，請參閱[在部署 Azure 資源時使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="d4dd1-321">tooreduce hello 數目的參數、 變數或輸出，您可以結合數個值的物件。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="d4dd1-322">如需詳細資訊，請參閱[物件作為參數](resource-manager-objects-as-parameters.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4dd1-323">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4dd1-323">Next steps</span></span>
* <span data-ttu-id="d4dd1-324">tooview 完成範本的許多不同類型的方案，請參閱 hello [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="d4dd1-325">如需您可以使用從範本中的 hello 函式的詳細資訊，請參閱[Azure 資源管理員範本函式](resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="d4dd1-326">toocombine 多個範本，在部署期間，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="d4dd1-327">您可能需要 toouse 資源存在於不同的資源群組內。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="d4dd1-328">這案例常見於使用多個資源群組之間所共用的儲存體帳戶或虛擬網路時。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="d4dd1-329">如需詳細資訊，請參閱 hello [resourceId 函數](resource-group-template-functions-resource.md#resourceid)。</span><span class="sxs-lookup"><span data-stu-id="d4dd1-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
