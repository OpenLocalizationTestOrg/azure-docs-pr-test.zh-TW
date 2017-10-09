---
title: "aaaAzure 資源管理員範本函式-邏輯 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 toodetermine 邏輯值中的 hello 函式 toouse。"
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="274ac-103">Azure Resource Manager 範本的邏輯函式</span><span class="sxs-lookup"><span data-stu-id="274ac-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="274ac-104">Resource Manager 提供了幾個用來在範本中進行比較的函式。</span><span class="sxs-lookup"><span data-stu-id="274ac-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="274ac-105">and</span><span class="sxs-lookup"><span data-stu-id="274ac-105">and</span></span>](#and)
* [<span data-ttu-id="274ac-106">bool</span><span class="sxs-lookup"><span data-stu-id="274ac-106">bool</span></span>](#bool)
* [<span data-ttu-id="274ac-107">if</span><span class="sxs-lookup"><span data-stu-id="274ac-107">if</span></span>](#if)
* [<span data-ttu-id="274ac-108">not</span><span class="sxs-lookup"><span data-stu-id="274ac-108">not</span></span>](#not)
* [<span data-ttu-id="274ac-109">or</span><span class="sxs-lookup"><span data-stu-id="274ac-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="274ac-110">和</span><span class="sxs-lookup"><span data-stu-id="274ac-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="274ac-111">檢查兩個參數值是否為 true。</span><span class="sxs-lookup"><span data-stu-id="274ac-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="274ac-112">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-112">Parameters</span></span>

| <span data-ttu-id="274ac-113">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-113">Parameter</span></span> | <span data-ttu-id="274ac-114">必要</span><span class="sxs-lookup"><span data-stu-id="274ac-114">Required</span></span> | <span data-ttu-id="274ac-115">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-115">Type</span></span> | <span data-ttu-id="274ac-116">說明</span><span class="sxs-lookup"><span data-stu-id="274ac-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="274ac-117">arg1</span><span class="sxs-lookup"><span data-stu-id="274ac-117">arg1</span></span> |<span data-ttu-id="274ac-118">是</span><span class="sxs-lookup"><span data-stu-id="274ac-118">Yes</span></span> |<span data-ttu-id="274ac-119">布林值</span><span class="sxs-lookup"><span data-stu-id="274ac-119">boolean</span></span> |<span data-ttu-id="274ac-120">hello 第一個值 toocheck 是否為 true。</span><span class="sxs-lookup"><span data-stu-id="274ac-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="274ac-121">arg2</span><span class="sxs-lookup"><span data-stu-id="274ac-121">arg2</span></span> |<span data-ttu-id="274ac-122">是</span><span class="sxs-lookup"><span data-stu-id="274ac-122">Yes</span></span> |<span data-ttu-id="274ac-123">布林值</span><span class="sxs-lookup"><span data-stu-id="274ac-123">boolean</span></span> |<span data-ttu-id="274ac-124">hello 第二個值 toocheck 是否為 true。</span><span class="sxs-lookup"><span data-stu-id="274ac-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="274ac-125">傳回值</span><span class="sxs-lookup"><span data-stu-id="274ac-125">Return value</span></span>

<span data-ttu-id="274ac-126">如果兩個值都是 true，則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="274ac-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="274ac-127">範例</span><span class="sxs-lookup"><span data-stu-id="274ac-127">Examples</span></span>

<span data-ttu-id="274ac-128">下列範例會示範如何 hello toouse 邏輯函式。</span><span class="sxs-lookup"><span data-stu-id="274ac-128">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="274ac-129">上述範例中的 hello hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="274ac-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="274ac-130">名稱</span><span class="sxs-lookup"><span data-stu-id="274ac-130">Name</span></span> | <span data-ttu-id="274ac-131">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-131">Type</span></span> | <span data-ttu-id="274ac-132">值</span><span class="sxs-lookup"><span data-stu-id="274ac-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="274ac-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-133">andExampleOutput</span></span> | <span data-ttu-id="274ac-134">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-134">Bool</span></span> | <span data-ttu-id="274ac-135">False</span><span class="sxs-lookup"><span data-stu-id="274ac-135">False</span></span> |
| <span data-ttu-id="274ac-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-136">orExampleOutput</span></span> | <span data-ttu-id="274ac-137">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-137">Bool</span></span> | <span data-ttu-id="274ac-138">True</span><span class="sxs-lookup"><span data-stu-id="274ac-138">True</span></span> |
| <span data-ttu-id="274ac-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-139">notExampleOutput</span></span> | <span data-ttu-id="274ac-140">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-140">Bool</span></span> | <span data-ttu-id="274ac-141">False</span><span class="sxs-lookup"><span data-stu-id="274ac-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="274ac-142">布林</span><span class="sxs-lookup"><span data-stu-id="274ac-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="274ac-143">轉換 hello 參數 tooa 布林值。</span><span class="sxs-lookup"><span data-stu-id="274ac-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="274ac-144">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-144">Parameters</span></span>

| <span data-ttu-id="274ac-145">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-145">Parameter</span></span> | <span data-ttu-id="274ac-146">必要</span><span class="sxs-lookup"><span data-stu-id="274ac-146">Required</span></span> | <span data-ttu-id="274ac-147">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-147">Type</span></span> | <span data-ttu-id="274ac-148">說明</span><span class="sxs-lookup"><span data-stu-id="274ac-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="274ac-149">arg1</span><span class="sxs-lookup"><span data-stu-id="274ac-149">arg1</span></span> |<span data-ttu-id="274ac-150">是</span><span class="sxs-lookup"><span data-stu-id="274ac-150">Yes</span></span> |<span data-ttu-id="274ac-151">字串或整數</span><span class="sxs-lookup"><span data-stu-id="274ac-151">string or int</span></span> |<span data-ttu-id="274ac-152">hello 值 tooconvert tooa 布林值。</span><span class="sxs-lookup"><span data-stu-id="274ac-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="274ac-153">傳回值</span><span class="sxs-lookup"><span data-stu-id="274ac-153">Return value</span></span>
<span data-ttu-id="274ac-154">Hello 的布林值轉換值。</span><span class="sxs-lookup"><span data-stu-id="274ac-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="274ac-155">範例</span><span class="sxs-lookup"><span data-stu-id="274ac-155">Examples</span></span>

<span data-ttu-id="274ac-156">下列範例會示範如何 hello toouse bool 的字串或整數。</span><span class="sxs-lookup"><span data-stu-id="274ac-156">hello following example shows how toouse bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="274ac-157">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="274ac-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="274ac-158">名稱</span><span class="sxs-lookup"><span data-stu-id="274ac-158">Name</span></span> | <span data-ttu-id="274ac-159">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-159">Type</span></span> | <span data-ttu-id="274ac-160">值</span><span class="sxs-lookup"><span data-stu-id="274ac-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="274ac-161">trueString</span><span class="sxs-lookup"><span data-stu-id="274ac-161">trueString</span></span> | <span data-ttu-id="274ac-162">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-162">Bool</span></span> | <span data-ttu-id="274ac-163">True</span><span class="sxs-lookup"><span data-stu-id="274ac-163">True</span></span> |
| <span data-ttu-id="274ac-164">falseString</span><span class="sxs-lookup"><span data-stu-id="274ac-164">falseString</span></span> | <span data-ttu-id="274ac-165">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-165">Bool</span></span> | <span data-ttu-id="274ac-166">False</span><span class="sxs-lookup"><span data-stu-id="274ac-166">False</span></span> |
| <span data-ttu-id="274ac-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="274ac-167">trueInt</span></span> | <span data-ttu-id="274ac-168">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-168">Bool</span></span> | <span data-ttu-id="274ac-169">True</span><span class="sxs-lookup"><span data-stu-id="274ac-169">True</span></span> |
| <span data-ttu-id="274ac-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="274ac-170">falseInt</span></span> | <span data-ttu-id="274ac-171">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-171">Bool</span></span> | <span data-ttu-id="274ac-172">False</span><span class="sxs-lookup"><span data-stu-id="274ac-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="274ac-173">if</span><span class="sxs-lookup"><span data-stu-id="274ac-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="274ac-174">根據條件是 true 或 false 傳回值。</span><span class="sxs-lookup"><span data-stu-id="274ac-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="274ac-175">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-175">Parameters</span></span>

| <span data-ttu-id="274ac-176">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-176">Parameter</span></span> | <span data-ttu-id="274ac-177">必要</span><span class="sxs-lookup"><span data-stu-id="274ac-177">Required</span></span> | <span data-ttu-id="274ac-178">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-178">Type</span></span> | <span data-ttu-id="274ac-179">說明</span><span class="sxs-lookup"><span data-stu-id="274ac-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="274ac-180">condition</span><span class="sxs-lookup"><span data-stu-id="274ac-180">condition</span></span> |<span data-ttu-id="274ac-181">是</span><span class="sxs-lookup"><span data-stu-id="274ac-181">Yes</span></span> |<span data-ttu-id="274ac-182">布林值</span><span class="sxs-lookup"><span data-stu-id="274ac-182">boolean</span></span> |<span data-ttu-id="274ac-183">hello 值 toocheck，是否為 true。</span><span class="sxs-lookup"><span data-stu-id="274ac-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="274ac-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="274ac-184">trueValue</span></span> |<span data-ttu-id="274ac-185">是</span><span class="sxs-lookup"><span data-stu-id="274ac-185">Yes</span></span> | <span data-ttu-id="274ac-186">字串、int、物件或陣列</span><span class="sxs-lookup"><span data-stu-id="274ac-186">string, int, object, or array</span></span> |<span data-ttu-id="274ac-187">hello 值 tooreturn hello 條件為 true 時。</span><span class="sxs-lookup"><span data-stu-id="274ac-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="274ac-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="274ac-188">falseValue</span></span> |<span data-ttu-id="274ac-189">是</span><span class="sxs-lookup"><span data-stu-id="274ac-189">Yes</span></span> | <span data-ttu-id="274ac-190">字串、int、物件或陣列</span><span class="sxs-lookup"><span data-stu-id="274ac-190">string, int, object, or array</span></span> |<span data-ttu-id="274ac-191">hello 值 tooreturn 時 hello 條件為 false。</span><span class="sxs-lookup"><span data-stu-id="274ac-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="274ac-192">傳回值</span><span class="sxs-lookup"><span data-stu-id="274ac-192">Return value</span></span>

<span data-ttu-id="274ac-193">當第一個參數是 **True** 時，傳回第二個參數；否則會傳回第三個參數。</span><span class="sxs-lookup"><span data-stu-id="274ac-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="274ac-194">備註</span><span class="sxs-lookup"><span data-stu-id="274ac-194">Remarks</span></span>

<span data-ttu-id="274ac-195">您可以使用這個函式 tooconditionally 集合之資源屬性。</span><span class="sxs-lookup"><span data-stu-id="274ac-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="274ac-196">hello 下列範例不完整的範本，但是它會顯示 hello 相關部分，有條件地設定 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="274ac-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="274ac-197">範例</span><span class="sxs-lookup"><span data-stu-id="274ac-197">Examples</span></span>

<span data-ttu-id="274ac-198">下列範例會示範如何 hello toouse hello`if`函式。</span><span class="sxs-lookup"><span data-stu-id="274ac-198">hello following example shows how toouse hello `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="274ac-199">上述範例中的 hello hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="274ac-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="274ac-200">名稱</span><span class="sxs-lookup"><span data-stu-id="274ac-200">Name</span></span> | <span data-ttu-id="274ac-201">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-201">Type</span></span> | <span data-ttu-id="274ac-202">值</span><span class="sxs-lookup"><span data-stu-id="274ac-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="274ac-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-203">yesOutput</span></span> | <span data-ttu-id="274ac-204">String</span><span class="sxs-lookup"><span data-stu-id="274ac-204">String</span></span> | <span data-ttu-id="274ac-205">yes</span><span class="sxs-lookup"><span data-stu-id="274ac-205">yes</span></span> |
| <span data-ttu-id="274ac-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-206">noOutput</span></span> | <span data-ttu-id="274ac-207">String</span><span class="sxs-lookup"><span data-stu-id="274ac-207">String</span></span> | <span data-ttu-id="274ac-208">no</span><span class="sxs-lookup"><span data-stu-id="274ac-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="274ac-209">否</span><span class="sxs-lookup"><span data-stu-id="274ac-209">not</span></span>
`not(arg1)`

<span data-ttu-id="274ac-210">將轉換的布林值 tooits 相反值。</span><span class="sxs-lookup"><span data-stu-id="274ac-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="274ac-211">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-211">Parameters</span></span>

| <span data-ttu-id="274ac-212">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-212">Parameter</span></span> | <span data-ttu-id="274ac-213">必要</span><span class="sxs-lookup"><span data-stu-id="274ac-213">Required</span></span> | <span data-ttu-id="274ac-214">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-214">Type</span></span> | <span data-ttu-id="274ac-215">說明</span><span class="sxs-lookup"><span data-stu-id="274ac-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="274ac-216">arg1</span><span class="sxs-lookup"><span data-stu-id="274ac-216">arg1</span></span> |<span data-ttu-id="274ac-217">是</span><span class="sxs-lookup"><span data-stu-id="274ac-217">Yes</span></span> |<span data-ttu-id="274ac-218">布林值</span><span class="sxs-lookup"><span data-stu-id="274ac-218">boolean</span></span> |<span data-ttu-id="274ac-219">hello 值 tooconvert。</span><span class="sxs-lookup"><span data-stu-id="274ac-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="274ac-220">傳回值</span><span class="sxs-lookup"><span data-stu-id="274ac-220">Return value</span></span>

<span data-ttu-id="274ac-221">當參數是 **False** 時，傳回 **True**。</span><span class="sxs-lookup"><span data-stu-id="274ac-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="274ac-222">當參數是 **True** 時，傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="274ac-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="274ac-223">範例</span><span class="sxs-lookup"><span data-stu-id="274ac-223">Examples</span></span>

<span data-ttu-id="274ac-224">下列範例會示範如何 hello toouse 邏輯函式。</span><span class="sxs-lookup"><span data-stu-id="274ac-224">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="274ac-225">上述範例中的 hello hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="274ac-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="274ac-226">名稱</span><span class="sxs-lookup"><span data-stu-id="274ac-226">Name</span></span> | <span data-ttu-id="274ac-227">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-227">Type</span></span> | <span data-ttu-id="274ac-228">值</span><span class="sxs-lookup"><span data-stu-id="274ac-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="274ac-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-229">andExampleOutput</span></span> | <span data-ttu-id="274ac-230">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-230">Bool</span></span> | <span data-ttu-id="274ac-231">False</span><span class="sxs-lookup"><span data-stu-id="274ac-231">False</span></span> |
| <span data-ttu-id="274ac-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-232">orExampleOutput</span></span> | <span data-ttu-id="274ac-233">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-233">Bool</span></span> | <span data-ttu-id="274ac-234">True</span><span class="sxs-lookup"><span data-stu-id="274ac-234">True</span></span> |
| <span data-ttu-id="274ac-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-235">notExampleOutput</span></span> | <span data-ttu-id="274ac-236">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-236">Bool</span></span> | <span data-ttu-id="274ac-237">False</span><span class="sxs-lookup"><span data-stu-id="274ac-237">False</span></span> |

<span data-ttu-id="274ac-238">hello 下列範例會使用**不**與[等於](resource-group-template-functions-comparison.md#equals)。</span><span class="sxs-lookup"><span data-stu-id="274ac-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="274ac-239">上述範例中的 hello hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="274ac-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="274ac-240">名稱</span><span class="sxs-lookup"><span data-stu-id="274ac-240">Name</span></span> | <span data-ttu-id="274ac-241">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-241">Type</span></span> | <span data-ttu-id="274ac-242">值</span><span class="sxs-lookup"><span data-stu-id="274ac-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="274ac-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="274ac-243">checkNotEquals</span></span> | <span data-ttu-id="274ac-244">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-244">Bool</span></span> | <span data-ttu-id="274ac-245">True</span><span class="sxs-lookup"><span data-stu-id="274ac-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="274ac-246">或</span><span class="sxs-lookup"><span data-stu-id="274ac-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="274ac-247">檢查任一個參數值是否為 true。</span><span class="sxs-lookup"><span data-stu-id="274ac-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="274ac-248">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-248">Parameters</span></span>

| <span data-ttu-id="274ac-249">參數</span><span class="sxs-lookup"><span data-stu-id="274ac-249">Parameter</span></span> | <span data-ttu-id="274ac-250">必要</span><span class="sxs-lookup"><span data-stu-id="274ac-250">Required</span></span> | <span data-ttu-id="274ac-251">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-251">Type</span></span> | <span data-ttu-id="274ac-252">說明</span><span class="sxs-lookup"><span data-stu-id="274ac-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="274ac-253">arg1</span><span class="sxs-lookup"><span data-stu-id="274ac-253">arg1</span></span> |<span data-ttu-id="274ac-254">是</span><span class="sxs-lookup"><span data-stu-id="274ac-254">Yes</span></span> |<span data-ttu-id="274ac-255">布林值</span><span class="sxs-lookup"><span data-stu-id="274ac-255">boolean</span></span> |<span data-ttu-id="274ac-256">hello 第一個值 toocheck 是否為 true。</span><span class="sxs-lookup"><span data-stu-id="274ac-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="274ac-257">arg2</span><span class="sxs-lookup"><span data-stu-id="274ac-257">arg2</span></span> |<span data-ttu-id="274ac-258">是</span><span class="sxs-lookup"><span data-stu-id="274ac-258">Yes</span></span> |<span data-ttu-id="274ac-259">布林值</span><span class="sxs-lookup"><span data-stu-id="274ac-259">boolean</span></span> |<span data-ttu-id="274ac-260">hello 第二個值 toocheck 是否為 true。</span><span class="sxs-lookup"><span data-stu-id="274ac-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="274ac-261">傳回值</span><span class="sxs-lookup"><span data-stu-id="274ac-261">Return value</span></span>

<span data-ttu-id="274ac-262">如果任一值為 ture，傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="274ac-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="274ac-263">範例</span><span class="sxs-lookup"><span data-stu-id="274ac-263">Examples</span></span>

<span data-ttu-id="274ac-264">下列範例會示範如何 hello toouse 邏輯函式。</span><span class="sxs-lookup"><span data-stu-id="274ac-264">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="274ac-265">上述範例中的 hello hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="274ac-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="274ac-266">名稱</span><span class="sxs-lookup"><span data-stu-id="274ac-266">Name</span></span> | <span data-ttu-id="274ac-267">類型</span><span class="sxs-lookup"><span data-stu-id="274ac-267">Type</span></span> | <span data-ttu-id="274ac-268">值</span><span class="sxs-lookup"><span data-stu-id="274ac-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="274ac-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-269">andExampleOutput</span></span> | <span data-ttu-id="274ac-270">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-270">Bool</span></span> | <span data-ttu-id="274ac-271">False</span><span class="sxs-lookup"><span data-stu-id="274ac-271">False</span></span> |
| <span data-ttu-id="274ac-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-272">orExampleOutput</span></span> | <span data-ttu-id="274ac-273">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-273">Bool</span></span> | <span data-ttu-id="274ac-274">True</span><span class="sxs-lookup"><span data-stu-id="274ac-274">True</span></span> |
| <span data-ttu-id="274ac-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="274ac-275">notExampleOutput</span></span> | <span data-ttu-id="274ac-276">Bool</span><span class="sxs-lookup"><span data-stu-id="274ac-276">Bool</span></span> | <span data-ttu-id="274ac-277">False</span><span class="sxs-lookup"><span data-stu-id="274ac-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="274ac-278">後續步驟</span><span class="sxs-lookup"><span data-stu-id="274ac-278">Next steps</span></span>
* <span data-ttu-id="274ac-279">如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="274ac-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="274ac-280">toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="274ac-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="274ac-281">tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="274ac-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="274ac-282">toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="274ac-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

