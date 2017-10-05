---
title: "Azure Resource Manager 範本函式 - 陣列和物件 | Microsoft Docs"
description: "描述 Azure Resource Manager 範本中用來使用陣列和物件的函式。"
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: 0bd9ec41761c9ce575f3bcf4d1f8e8578b83e01c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="e8d69-103">Azure Resource Manager 範本的陣列和物件函式</span><span class="sxs-lookup"><span data-stu-id="e8d69-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="e8d69-104">Resource Manager 提供了幾個用來使用陣列和物件的函式。</span><span class="sxs-lookup"><span data-stu-id="e8d69-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="e8d69-105">array</span><span class="sxs-lookup"><span data-stu-id="e8d69-105">array</span></span>](#array)
* [<span data-ttu-id="e8d69-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="e8d69-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="e8d69-107">concat</span><span class="sxs-lookup"><span data-stu-id="e8d69-107">concat</span></span>](#concat)
* [<span data-ttu-id="e8d69-108">contains</span><span class="sxs-lookup"><span data-stu-id="e8d69-108">contains</span></span>](#contains)
* [<span data-ttu-id="e8d69-109">createArray</span><span class="sxs-lookup"><span data-stu-id="e8d69-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="e8d69-110">empty</span><span class="sxs-lookup"><span data-stu-id="e8d69-110">empty</span></span>](#empty)
* [<span data-ttu-id="e8d69-111">first</span><span class="sxs-lookup"><span data-stu-id="e8d69-111">first</span></span>](#first)
* [<span data-ttu-id="e8d69-112">intersection</span><span class="sxs-lookup"><span data-stu-id="e8d69-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="e8d69-113">json</span><span class="sxs-lookup"><span data-stu-id="e8d69-113">json</span></span>](#json)
* [<span data-ttu-id="e8d69-114">last</span><span class="sxs-lookup"><span data-stu-id="e8d69-114">last</span></span>](#last)
* [<span data-ttu-id="e8d69-115">length</span><span class="sxs-lookup"><span data-stu-id="e8d69-115">length</span></span>](#length)
* [<span data-ttu-id="e8d69-116">min</span><span class="sxs-lookup"><span data-stu-id="e8d69-116">min</span></span>](#min)
* [<span data-ttu-id="e8d69-117">max</span><span class="sxs-lookup"><span data-stu-id="e8d69-117">max</span></span>](#max)
* [<span data-ttu-id="e8d69-118">range</span><span class="sxs-lookup"><span data-stu-id="e8d69-118">range</span></span>](#range)
* [<span data-ttu-id="e8d69-119">skip</span><span class="sxs-lookup"><span data-stu-id="e8d69-119">skip</span></span>](#skip)
* [<span data-ttu-id="e8d69-120">take</span><span class="sxs-lookup"><span data-stu-id="e8d69-120">take</span></span>](#take)
* [<span data-ttu-id="e8d69-121">union</span><span class="sxs-lookup"><span data-stu-id="e8d69-121">union</span></span>](#union)

<span data-ttu-id="e8d69-122">若要取得以值分隔的字串值陣列，請參閱 [分割](resource-group-template-functions-string.md#split)。</span><span class="sxs-lookup"><span data-stu-id="e8d69-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="e8d69-123">array</span><span class="sxs-lookup"><span data-stu-id="e8d69-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="e8d69-124">將值轉換為陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-125">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-125">Parameters</span></span>

| <span data-ttu-id="e8d69-126">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-126">Parameter</span></span> | <span data-ttu-id="e8d69-127">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-127">Required</span></span> | <span data-ttu-id="e8d69-128">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-128">Type</span></span> | <span data-ttu-id="e8d69-129">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="e8d69-130">convertToArray</span></span> |<span data-ttu-id="e8d69-131">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-131">Yes</span></span> |<span data-ttu-id="e8d69-132">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-132">int, string, array, or object</span></span> |<span data-ttu-id="e8d69-133">要轉換為陣列的值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-134">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-134">Return value</span></span>

<span data-ttu-id="e8d69-135">陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-136">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-136">Example</span></span>

<span data-ttu-id="e8d69-137">下列範例顯示如何使用不同類型的陣列函式。</span><span class="sxs-lookup"><span data-stu-id="e8d69-137">The following example shows how to use the array function with different types.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-138">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-139">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-139">Name</span></span> | <span data-ttu-id="e8d69-140">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-140">Type</span></span> | <span data-ttu-id="e8d69-141">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-142">intOutput</span></span> | <span data-ttu-id="e8d69-143">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-143">Array</span></span> | <span data-ttu-id="e8d69-144">[1]</span><span class="sxs-lookup"><span data-stu-id="e8d69-144">[1]</span></span> |
| <span data-ttu-id="e8d69-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-145">stringOutput</span></span> | <span data-ttu-id="e8d69-146">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-146">Array</span></span> | <span data-ttu-id="e8d69-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="e8d69-147">["a"]</span></span> |
| <span data-ttu-id="e8d69-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-148">objectOutput</span></span> | <span data-ttu-id="e8d69-149">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-149">Array</span></span> | <span data-ttu-id="e8d69-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="e8d69-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="e8d69-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="e8d69-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="e8d69-152">從參數中傳回第一個非 null 值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-152">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="e8d69-153">空白字串、空白陣列和空白物件不是 null。</span><span class="sxs-lookup"><span data-stu-id="e8d69-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-154">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-154">Parameters</span></span>

| <span data-ttu-id="e8d69-155">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-155">Parameter</span></span> | <span data-ttu-id="e8d69-156">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-156">Required</span></span> | <span data-ttu-id="e8d69-157">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-157">Type</span></span> | <span data-ttu-id="e8d69-158">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-159">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-159">arg1</span></span> |<span data-ttu-id="e8d69-160">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-160">Yes</span></span> |<span data-ttu-id="e8d69-161">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-161">int, string, array, or object</span></span> |<span data-ttu-id="e8d69-162">要測試是否為 null 的第一個值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-162">The first value to test for null.</span></span> |
| <span data-ttu-id="e8d69-163">其他引數</span><span class="sxs-lookup"><span data-stu-id="e8d69-163">additional args</span></span> |<span data-ttu-id="e8d69-164">否</span><span class="sxs-lookup"><span data-stu-id="e8d69-164">No</span></span> |<span data-ttu-id="e8d69-165">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-165">int, string, array, or object</span></span> |<span data-ttu-id="e8d69-166">要測試是否為 null 的其他值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-166">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-167">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-167">Return value</span></span>

<span data-ttu-id="e8d69-168">第一個非 null 參數的值，此值可為字串、整數、陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="e8d69-168">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="e8d69-169">如果所有參數都是 null，則傳回 null。</span><span class="sxs-lookup"><span data-stu-id="e8d69-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="e8d69-170">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-170">Example</span></span>

<span data-ttu-id="e8d69-171">下列範例顯示不同的聯合用法所得到的輸出。</span><span class="sxs-lookup"><span data-stu-id="e8d69-171">The following example shows the output from different uses of coalesce.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

<span data-ttu-id="e8d69-172">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-172">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-173">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-173">Name</span></span> | <span data-ttu-id="e8d69-174">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-174">Type</span></span> | <span data-ttu-id="e8d69-175">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-176">stringOutput</span></span> | <span data-ttu-id="e8d69-177">String</span><span class="sxs-lookup"><span data-stu-id="e8d69-177">String</span></span> | <span data-ttu-id="e8d69-178">預設值</span><span class="sxs-lookup"><span data-stu-id="e8d69-178">default</span></span> |
| <span data-ttu-id="e8d69-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-179">intOutput</span></span> | <span data-ttu-id="e8d69-180">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-180">Int</span></span> | <span data-ttu-id="e8d69-181">1</span><span class="sxs-lookup"><span data-stu-id="e8d69-181">1</span></span> |
| <span data-ttu-id="e8d69-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-182">objectOutput</span></span> | <span data-ttu-id="e8d69-183">Object</span><span class="sxs-lookup"><span data-stu-id="e8d69-183">Object</span></span> | <span data-ttu-id="e8d69-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="e8d69-184">{"first": "default"}</span></span> |
| <span data-ttu-id="e8d69-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-185">arrayOutput</span></span> | <span data-ttu-id="e8d69-186">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-186">Array</span></span> | <span data-ttu-id="e8d69-187">[1]</span><span class="sxs-lookup"><span data-stu-id="e8d69-187">[1]</span></span> |
| <span data-ttu-id="e8d69-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-188">emptyOutput</span></span> | <span data-ttu-id="e8d69-189">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-189">Bool</span></span> | <span data-ttu-id="e8d69-190">True</span><span class="sxs-lookup"><span data-stu-id="e8d69-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="e8d69-191">concat</span><span class="sxs-lookup"><span data-stu-id="e8d69-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="e8d69-192">結合多個陣列並傳回串連陣列，或結合多個字串值並傳回串連字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-192">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="e8d69-193">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-193">Parameters</span></span>

| <span data-ttu-id="e8d69-194">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-194">Parameter</span></span> | <span data-ttu-id="e8d69-195">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-195">Required</span></span> | <span data-ttu-id="e8d69-196">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-196">Type</span></span> | <span data-ttu-id="e8d69-197">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-198">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-198">arg1</span></span> |<span data-ttu-id="e8d69-199">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-199">Yes</span></span> |<span data-ttu-id="e8d69-200">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-200">array or string</span></span> |<span data-ttu-id="e8d69-201">串連的第一個陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-201">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="e8d69-202">其他引數</span><span class="sxs-lookup"><span data-stu-id="e8d69-202">additional arguments</span></span> |<span data-ttu-id="e8d69-203">否</span><span class="sxs-lookup"><span data-stu-id="e8d69-203">No</span></span> |<span data-ttu-id="e8d69-204">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-204">array or string</span></span> |<span data-ttu-id="e8d69-205">串連的其他陣列或字串 (循序順序)。</span><span class="sxs-lookup"><span data-stu-id="e8d69-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="e8d69-206">此函式可以接受任意數目的引數，並且可針對參數接受字串或陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-206">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="e8d69-207">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-207">Return value</span></span>
<span data-ttu-id="e8d69-208">串連值的字串或陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-209">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-209">Example</span></span>

<span data-ttu-id="e8d69-210">下一個範例顯示如何結合兩個陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-210">The following example shows how to combine two arrays.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-211">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-211">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-212">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-212">Name</span></span> | <span data-ttu-id="e8d69-213">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-213">Type</span></span> | <span data-ttu-id="e8d69-214">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-215">return</span><span class="sxs-lookup"><span data-stu-id="e8d69-215">return</span></span> | <span data-ttu-id="e8d69-216">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-216">Array</span></span> | <span data-ttu-id="e8d69-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="e8d69-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="e8d69-218">下列範例顯示如何結合兩個字串值並傳回串連字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-218">The following example shows how to combine two string values and return a concatenated string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="e8d69-219">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-219">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-220">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-220">Name</span></span> | <span data-ttu-id="e8d69-221">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-221">Type</span></span> | <span data-ttu-id="e8d69-222">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-223">concatOutput</span></span> | <span data-ttu-id="e8d69-224">String</span><span class="sxs-lookup"><span data-stu-id="e8d69-224">String</span></span> | <span data-ttu-id="e8d69-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="e8d69-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="e8d69-226">contains</span><span class="sxs-lookup"><span data-stu-id="e8d69-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="e8d69-227">檢查陣列中是否包含值、物件中是否包含索引鍵，或字串中是否包含子字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-228">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-228">Parameters</span></span>

| <span data-ttu-id="e8d69-229">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-229">Parameter</span></span> | <span data-ttu-id="e8d69-230">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-230">Required</span></span> | <span data-ttu-id="e8d69-231">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-231">Type</span></span> | <span data-ttu-id="e8d69-232">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-233">container</span><span class="sxs-lookup"><span data-stu-id="e8d69-233">container</span></span> |<span data-ttu-id="e8d69-234">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-234">Yes</span></span> |<span data-ttu-id="e8d69-235">陣列、物件或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-235">array, object, or string</span></span> |<span data-ttu-id="e8d69-236">其中包含要尋找之值的值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-236">The value that contains the value to find.</span></span> |
| <span data-ttu-id="e8d69-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="e8d69-237">itemToFind</span></span> |<span data-ttu-id="e8d69-238">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-238">Yes</span></span> |<span data-ttu-id="e8d69-239">字串或整數</span><span class="sxs-lookup"><span data-stu-id="e8d69-239">string or int</span></span> |<span data-ttu-id="e8d69-240">要尋找的值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-240">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-241">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-241">Return value</span></span>

<span data-ttu-id="e8d69-242">找到項目則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="e8d69-242">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-243">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-243">Example</span></span>

<span data-ttu-id="e8d69-244">下列範例顯示如何使用不同類型的 contains：</span><span class="sxs-lookup"><span data-stu-id="e8d69-244">The following example shows how to use contains with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

<span data-ttu-id="e8d69-245">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-246">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-246">Name</span></span> | <span data-ttu-id="e8d69-247">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-247">Type</span></span> | <span data-ttu-id="e8d69-248">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="e8d69-249">stringTrue</span></span> | <span data-ttu-id="e8d69-250">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-250">Bool</span></span> | <span data-ttu-id="e8d69-251">True</span><span class="sxs-lookup"><span data-stu-id="e8d69-251">True</span></span> |
| <span data-ttu-id="e8d69-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="e8d69-252">stringFalse</span></span> | <span data-ttu-id="e8d69-253">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-253">Bool</span></span> | <span data-ttu-id="e8d69-254">False</span><span class="sxs-lookup"><span data-stu-id="e8d69-254">False</span></span> |
| <span data-ttu-id="e8d69-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="e8d69-255">objectTrue</span></span> | <span data-ttu-id="e8d69-256">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-256">Bool</span></span> | <span data-ttu-id="e8d69-257">True</span><span class="sxs-lookup"><span data-stu-id="e8d69-257">True</span></span> |
| <span data-ttu-id="e8d69-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="e8d69-258">objectFalse</span></span> | <span data-ttu-id="e8d69-259">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-259">Bool</span></span> | <span data-ttu-id="e8d69-260">False</span><span class="sxs-lookup"><span data-stu-id="e8d69-260">False</span></span> |
| <span data-ttu-id="e8d69-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="e8d69-261">arrayTrue</span></span> | <span data-ttu-id="e8d69-262">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-262">Bool</span></span> | <span data-ttu-id="e8d69-263">True</span><span class="sxs-lookup"><span data-stu-id="e8d69-263">True</span></span> |
| <span data-ttu-id="e8d69-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="e8d69-264">arrayFalse</span></span> | <span data-ttu-id="e8d69-265">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-265">Bool</span></span> | <span data-ttu-id="e8d69-266">False</span><span class="sxs-lookup"><span data-stu-id="e8d69-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="e8d69-267">createarray</span><span class="sxs-lookup"><span data-stu-id="e8d69-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="e8d69-268">從參數建立陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-268">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-269">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-269">Parameters</span></span>

| <span data-ttu-id="e8d69-270">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-270">Parameter</span></span> | <span data-ttu-id="e8d69-271">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-271">Required</span></span> | <span data-ttu-id="e8d69-272">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-272">Type</span></span> | <span data-ttu-id="e8d69-273">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-274">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-274">arg1</span></span> |<span data-ttu-id="e8d69-275">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-275">Yes</span></span> |<span data-ttu-id="e8d69-276">字串、整數、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="e8d69-277">陣列中的第一個值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-277">The first value in the array.</span></span> |
| <span data-ttu-id="e8d69-278">其他引數</span><span class="sxs-lookup"><span data-stu-id="e8d69-278">additional arguments</span></span> |<span data-ttu-id="e8d69-279">否</span><span class="sxs-lookup"><span data-stu-id="e8d69-279">No</span></span> |<span data-ttu-id="e8d69-280">字串、整數、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="e8d69-281">陣列中的其他值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-281">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-282">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-282">Return value</span></span>

<span data-ttu-id="e8d69-283">陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-284">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-284">Example</span></span>

<span data-ttu-id="e8d69-285">下列範例顯示如何使用不同類型的 createArray：</span><span class="sxs-lookup"><span data-stu-id="e8d69-285">The following example shows how to use createArray with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-286">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-286">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-287">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-287">Name</span></span> | <span data-ttu-id="e8d69-288">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-288">Type</span></span> | <span data-ttu-id="e8d69-289">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="e8d69-290">stringArray</span></span> | <span data-ttu-id="e8d69-291">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-291">Array</span></span> | <span data-ttu-id="e8d69-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="e8d69-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="e8d69-293">intArray</span><span class="sxs-lookup"><span data-stu-id="e8d69-293">intArray</span></span> | <span data-ttu-id="e8d69-294">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-294">Array</span></span> | <span data-ttu-id="e8d69-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="e8d69-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="e8d69-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="e8d69-296">objectArray</span></span> | <span data-ttu-id="e8d69-297">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-297">Array</span></span> | <span data-ttu-id="e8d69-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="e8d69-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="e8d69-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="e8d69-299">arrayArray</span></span> | <span data-ttu-id="e8d69-300">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-300">Array</span></span> | <span data-ttu-id="e8d69-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="e8d69-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="e8d69-302">empty</span><span class="sxs-lookup"><span data-stu-id="e8d69-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="e8d69-303">判斷陣列、物件或字串是否空白。</span><span class="sxs-lookup"><span data-stu-id="e8d69-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-304">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-304">Parameters</span></span>

| <span data-ttu-id="e8d69-305">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-305">Parameter</span></span> | <span data-ttu-id="e8d69-306">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-306">Required</span></span> | <span data-ttu-id="e8d69-307">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-307">Type</span></span> | <span data-ttu-id="e8d69-308">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="e8d69-309">itemToTest</span></span> |<span data-ttu-id="e8d69-310">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-310">Yes</span></span> |<span data-ttu-id="e8d69-311">陣列、物件或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-311">array, object, or string</span></span> |<span data-ttu-id="e8d69-312">要檢查其是否為空白的值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-312">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-313">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-313">Return value</span></span>

<span data-ttu-id="e8d69-314">如果值空白則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="e8d69-314">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-315">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-315">Example</span></span>

<span data-ttu-id="e8d69-316">下列範例會檢查陣列、物件和字串是否空白。</span><span class="sxs-lookup"><span data-stu-id="e8d69-316">The following example checks whether an array, object, and string are empty.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-317">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-317">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-318">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-318">Name</span></span> | <span data-ttu-id="e8d69-319">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-319">Type</span></span> | <span data-ttu-id="e8d69-320">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="e8d69-321">arrayEmpty</span></span> | <span data-ttu-id="e8d69-322">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-322">Bool</span></span> | <span data-ttu-id="e8d69-323">True</span><span class="sxs-lookup"><span data-stu-id="e8d69-323">True</span></span> |
| <span data-ttu-id="e8d69-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="e8d69-324">objectEmpty</span></span> | <span data-ttu-id="e8d69-325">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-325">Bool</span></span> | <span data-ttu-id="e8d69-326">True</span><span class="sxs-lookup"><span data-stu-id="e8d69-326">True</span></span> |
| <span data-ttu-id="e8d69-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="e8d69-327">stringEmpty</span></span> | <span data-ttu-id="e8d69-328">Bool</span><span class="sxs-lookup"><span data-stu-id="e8d69-328">Bool</span></span> | <span data-ttu-id="e8d69-329">True</span><span class="sxs-lookup"><span data-stu-id="e8d69-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="e8d69-330">first</span><span class="sxs-lookup"><span data-stu-id="e8d69-330">first</span></span>
`first(arg1)`

<span data-ttu-id="e8d69-331">傳回陣列的第一個元素或字串的第一個字元。</span><span class="sxs-lookup"><span data-stu-id="e8d69-331">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-332">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-332">Parameters</span></span>

| <span data-ttu-id="e8d69-333">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-333">Parameter</span></span> | <span data-ttu-id="e8d69-334">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-334">Required</span></span> | <span data-ttu-id="e8d69-335">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-335">Type</span></span> | <span data-ttu-id="e8d69-336">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-337">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-337">arg1</span></span> |<span data-ttu-id="e8d69-338">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-338">Yes</span></span> |<span data-ttu-id="e8d69-339">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-339">array or string</span></span> |<span data-ttu-id="e8d69-340">要擷取其第一個元素或字元的值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-340">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-341">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-341">Return value</span></span>

<span data-ttu-id="e8d69-342">陣列中第一個元素的類型 (字串、整數、陣列或物件) 或字串的第一個字元。</span><span class="sxs-lookup"><span data-stu-id="e8d69-342">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-343">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-343">Example</span></span>

<span data-ttu-id="e8d69-344">下列範例顯示如何搭配使用 first 函式與陣列和字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-344">The following example shows how to use the first function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="e8d69-345">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-345">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-346">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-346">Name</span></span> | <span data-ttu-id="e8d69-347">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-347">Type</span></span> | <span data-ttu-id="e8d69-348">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-349">arrayOutput</span></span> | <span data-ttu-id="e8d69-350">String</span><span class="sxs-lookup"><span data-stu-id="e8d69-350">String</span></span> | <span data-ttu-id="e8d69-351">one</span><span class="sxs-lookup"><span data-stu-id="e8d69-351">one</span></span> |
| <span data-ttu-id="e8d69-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-352">stringOutput</span></span> | <span data-ttu-id="e8d69-353">String</span><span class="sxs-lookup"><span data-stu-id="e8d69-353">String</span></span> | <span data-ttu-id="e8d69-354">O</span><span class="sxs-lookup"><span data-stu-id="e8d69-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="e8d69-355">交集</span><span class="sxs-lookup"><span data-stu-id="e8d69-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="e8d69-356">從參數中傳回具有共同元素的單一陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="e8d69-356">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-357">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-357">Parameters</span></span>

| <span data-ttu-id="e8d69-358">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-358">Parameter</span></span> | <span data-ttu-id="e8d69-359">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-359">Required</span></span> | <span data-ttu-id="e8d69-360">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-360">Type</span></span> | <span data-ttu-id="e8d69-361">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-362">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-362">arg1</span></span> |<span data-ttu-id="e8d69-363">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-363">Yes</span></span> |<span data-ttu-id="e8d69-364">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-364">array or object</span></span> |<span data-ttu-id="e8d69-365">要用來尋找共同元素的第一個值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-365">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="e8d69-366">arg2</span><span class="sxs-lookup"><span data-stu-id="e8d69-366">arg2</span></span> |<span data-ttu-id="e8d69-367">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-367">Yes</span></span> |<span data-ttu-id="e8d69-368">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-368">array or object</span></span> |<span data-ttu-id="e8d69-369">要用來尋找共同元素的第二個值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-369">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="e8d69-370">其他引數</span><span class="sxs-lookup"><span data-stu-id="e8d69-370">additional arguments</span></span> |<span data-ttu-id="e8d69-371">否</span><span class="sxs-lookup"><span data-stu-id="e8d69-371">No</span></span> |<span data-ttu-id="e8d69-372">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-372">array or object</span></span> |<span data-ttu-id="e8d69-373">要用來尋找共同元素的其他值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-373">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-374">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-374">Return value</span></span>

<span data-ttu-id="e8d69-375">具有共同元素的陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="e8d69-375">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-376">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-376">Example</span></span>

<span data-ttu-id="e8d69-377">下列範例顯示如何搭配使用 intersection 與陣列和物件︰</span><span class="sxs-lookup"><span data-stu-id="e8d69-377">The following example shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-378">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-378">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-379">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-379">Name</span></span> | <span data-ttu-id="e8d69-380">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-380">Type</span></span> | <span data-ttu-id="e8d69-381">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-382">objectOutput</span></span> | <span data-ttu-id="e8d69-383">Object</span><span class="sxs-lookup"><span data-stu-id="e8d69-383">Object</span></span> | <span data-ttu-id="e8d69-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="e8d69-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="e8d69-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-385">arrayOutput</span></span> | <span data-ttu-id="e8d69-386">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-386">Array</span></span> | <span data-ttu-id="e8d69-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="e8d69-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="e8d69-388">json</span><span class="sxs-lookup"><span data-stu-id="e8d69-388">json</span></span>
`json(arg1)`

<span data-ttu-id="e8d69-389">傳回 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="e8d69-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-390">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-390">Parameters</span></span>

| <span data-ttu-id="e8d69-391">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-391">Parameter</span></span> | <span data-ttu-id="e8d69-392">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-392">Required</span></span> | <span data-ttu-id="e8d69-393">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-393">Type</span></span> | <span data-ttu-id="e8d69-394">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-395">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-395">arg1</span></span> |<span data-ttu-id="e8d69-396">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-396">Yes</span></span> |<span data-ttu-id="e8d69-397">字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-397">string</span></span> |<span data-ttu-id="e8d69-398">要轉換成 JSON 的值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-398">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="e8d69-399">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-399">Return value</span></span>

<span data-ttu-id="e8d69-400">來自指定字串的 JSON 物件，或指定 **null** 時為空物件。</span><span class="sxs-lookup"><span data-stu-id="e8d69-400">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-401">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-401">Example</span></span>

<span data-ttu-id="e8d69-402">下列範例顯示如何搭配使用 intersection 與陣列和物件︰</span><span class="sxs-lookup"><span data-stu-id="e8d69-402">The following example shows how to use intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-403">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-403">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-404">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-404">Name</span></span> | <span data-ttu-id="e8d69-405">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-405">Type</span></span> | <span data-ttu-id="e8d69-406">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-407">jsonOutput</span></span> | <span data-ttu-id="e8d69-408">Object</span><span class="sxs-lookup"><span data-stu-id="e8d69-408">Object</span></span> | <span data-ttu-id="e8d69-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="e8d69-409">{"a": "b"}</span></span> |
| <span data-ttu-id="e8d69-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-410">nullOutput</span></span> | <span data-ttu-id="e8d69-411">Boolean</span><span class="sxs-lookup"><span data-stu-id="e8d69-411">Boolean</span></span> | <span data-ttu-id="e8d69-412">True</span><span class="sxs-lookup"><span data-stu-id="e8d69-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="e8d69-413">last</span><span class="sxs-lookup"><span data-stu-id="e8d69-413">last</span></span>
`last (arg1)`

<span data-ttu-id="e8d69-414">傳回陣列的最後一個元素或字串的最後一個字元。</span><span class="sxs-lookup"><span data-stu-id="e8d69-414">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-415">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-415">Parameters</span></span>

| <span data-ttu-id="e8d69-416">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-416">Parameter</span></span> | <span data-ttu-id="e8d69-417">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-417">Required</span></span> | <span data-ttu-id="e8d69-418">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-418">Type</span></span> | <span data-ttu-id="e8d69-419">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-420">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-420">arg1</span></span> |<span data-ttu-id="e8d69-421">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-421">Yes</span></span> |<span data-ttu-id="e8d69-422">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-422">array or string</span></span> |<span data-ttu-id="e8d69-423">要擷取其最後一個元素或字元的值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-423">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-424">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-424">Return value</span></span>

<span data-ttu-id="e8d69-425">陣列中最後一個元素的類型 (字串、整數、陣列或物件) 或字串的最後一個字元。</span><span class="sxs-lookup"><span data-stu-id="e8d69-425">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-426">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-426">Example</span></span>

<span data-ttu-id="e8d69-427">下列範例顯示如何搭配使用 last 函式與陣列和字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-427">The following example shows how to use the last function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="e8d69-428">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-429">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-429">Name</span></span> | <span data-ttu-id="e8d69-430">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-430">Type</span></span> | <span data-ttu-id="e8d69-431">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-432">arrayOutput</span></span> | <span data-ttu-id="e8d69-433">String</span><span class="sxs-lookup"><span data-stu-id="e8d69-433">String</span></span> | <span data-ttu-id="e8d69-434">three</span><span class="sxs-lookup"><span data-stu-id="e8d69-434">three</span></span> |
| <span data-ttu-id="e8d69-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-435">stringOutput</span></span> | <span data-ttu-id="e8d69-436">String</span><span class="sxs-lookup"><span data-stu-id="e8d69-436">String</span></span> | <span data-ttu-id="e8d69-437">e</span><span class="sxs-lookup"><span data-stu-id="e8d69-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="e8d69-438">length</span><span class="sxs-lookup"><span data-stu-id="e8d69-438">length</span></span>
`length(arg1)`

<span data-ttu-id="e8d69-439">傳回陣列中的元素數目或字串中的字元數目。</span><span class="sxs-lookup"><span data-stu-id="e8d69-439">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-440">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-440">Parameters</span></span>

| <span data-ttu-id="e8d69-441">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-441">Parameter</span></span> | <span data-ttu-id="e8d69-442">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-442">Required</span></span> | <span data-ttu-id="e8d69-443">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-443">Type</span></span> | <span data-ttu-id="e8d69-444">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-445">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-445">arg1</span></span> |<span data-ttu-id="e8d69-446">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-446">Yes</span></span> |<span data-ttu-id="e8d69-447">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-447">array or string</span></span> |<span data-ttu-id="e8d69-448">要用來取得元素數目的陣列，或用來取得字元數目的字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-448">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-449">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-449">Return value</span></span>

<span data-ttu-id="e8d69-450">整數。</span><span class="sxs-lookup"><span data-stu-id="e8d69-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="e8d69-451">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-451">Example</span></span>

<span data-ttu-id="e8d69-452">下列範例顯示如何搭配使用 length 與陣列和字串：</span><span class="sxs-lookup"><span data-stu-id="e8d69-452">The following example shows how to use length with an array and string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-453">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-453">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-454">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-454">Name</span></span> | <span data-ttu-id="e8d69-455">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-455">Type</span></span> | <span data-ttu-id="e8d69-456">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="e8d69-457">arrayLength</span></span> | <span data-ttu-id="e8d69-458">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-458">Int</span></span> | <span data-ttu-id="e8d69-459">3</span><span class="sxs-lookup"><span data-stu-id="e8d69-459">3</span></span> |
| <span data-ttu-id="e8d69-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="e8d69-460">stringLength</span></span> | <span data-ttu-id="e8d69-461">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-461">Int</span></span> | <span data-ttu-id="e8d69-462">13</span><span class="sxs-lookup"><span data-stu-id="e8d69-462">13</span></span> |

<span data-ttu-id="e8d69-463">建立資源時，您可在陣列中使用此函式指定反覆運算的數量。</span><span class="sxs-lookup"><span data-stu-id="e8d69-463">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="e8d69-464">下列範例中，參數 **siteNames** 會參考在建立網站時要使用的名稱陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-464">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="e8d69-465">如需有關在此陣列中使用函式的詳細資訊，請參閱 [在 Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="e8d69-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="e8d69-466">Min</span><span class="sxs-lookup"><span data-stu-id="e8d69-466">min</span></span>
`min(arg1)`

<span data-ttu-id="e8d69-467">傳回整數陣列的最小值，或以逗號分隔的整數清單。</span><span class="sxs-lookup"><span data-stu-id="e8d69-467">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-468">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-468">Parameters</span></span>

| <span data-ttu-id="e8d69-469">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-469">Parameter</span></span> | <span data-ttu-id="e8d69-470">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-470">Required</span></span> | <span data-ttu-id="e8d69-471">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-471">Type</span></span> | <span data-ttu-id="e8d69-472">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-473">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-473">arg1</span></span> |<span data-ttu-id="e8d69-474">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-474">Yes</span></span> |<span data-ttu-id="e8d69-475">整數的陣列，或以逗號分隔的整數清單</span><span class="sxs-lookup"><span data-stu-id="e8d69-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="e8d69-476">要用來取得最小值的集合。</span><span class="sxs-lookup"><span data-stu-id="e8d69-476">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-477">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-477">Return value</span></span>

<span data-ttu-id="e8d69-478">代表最小值的整數。</span><span class="sxs-lookup"><span data-stu-id="e8d69-478">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-479">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-479">Example</span></span>

<span data-ttu-id="e8d69-480">下列範例顯示如何搭配使用 min 與陣列和整數清單：</span><span class="sxs-lookup"><span data-stu-id="e8d69-480">The following example shows how to use min with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="e8d69-481">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-481">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-482">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-482">Name</span></span> | <span data-ttu-id="e8d69-483">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-483">Type</span></span> | <span data-ttu-id="e8d69-484">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-485">arrayOutput</span></span> | <span data-ttu-id="e8d69-486">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-486">Int</span></span> | <span data-ttu-id="e8d69-487">0</span><span class="sxs-lookup"><span data-stu-id="e8d69-487">0</span></span> |
| <span data-ttu-id="e8d69-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-488">intOutput</span></span> | <span data-ttu-id="e8d69-489">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-489">Int</span></span> | <span data-ttu-id="e8d69-490">0</span><span class="sxs-lookup"><span data-stu-id="e8d69-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="e8d69-491">max</span><span class="sxs-lookup"><span data-stu-id="e8d69-491">max</span></span>
`max(arg1)`

<span data-ttu-id="e8d69-492">傳回整數陣列的最大值，或以逗號分隔的整數清單。</span><span class="sxs-lookup"><span data-stu-id="e8d69-492">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-493">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-493">Parameters</span></span>

| <span data-ttu-id="e8d69-494">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-494">Parameter</span></span> | <span data-ttu-id="e8d69-495">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-495">Required</span></span> | <span data-ttu-id="e8d69-496">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-496">Type</span></span> | <span data-ttu-id="e8d69-497">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-498">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-498">arg1</span></span> |<span data-ttu-id="e8d69-499">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-499">Yes</span></span> |<span data-ttu-id="e8d69-500">整數的陣列，或以逗號分隔的整數清單</span><span class="sxs-lookup"><span data-stu-id="e8d69-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="e8d69-501">要用來取得最大值的集合。</span><span class="sxs-lookup"><span data-stu-id="e8d69-501">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-502">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-502">Return value</span></span>

<span data-ttu-id="e8d69-503">代表最大值的整數。</span><span class="sxs-lookup"><span data-stu-id="e8d69-503">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-504">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-504">Example</span></span>

<span data-ttu-id="e8d69-505">下列範例顯示如何搭配使用 max 與陣列和整數清單：</span><span class="sxs-lookup"><span data-stu-id="e8d69-505">The following example shows how to use max with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="e8d69-506">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-506">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-507">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-507">Name</span></span> | <span data-ttu-id="e8d69-508">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-508">Type</span></span> | <span data-ttu-id="e8d69-509">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-510">arrayOutput</span></span> | <span data-ttu-id="e8d69-511">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-511">Int</span></span> | <span data-ttu-id="e8d69-512">5</span><span class="sxs-lookup"><span data-stu-id="e8d69-512">5</span></span> |
| <span data-ttu-id="e8d69-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-513">intOutput</span></span> | <span data-ttu-id="e8d69-514">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-514">Int</span></span> | <span data-ttu-id="e8d69-515">5</span><span class="sxs-lookup"><span data-stu-id="e8d69-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="e8d69-516">range</span><span class="sxs-lookup"><span data-stu-id="e8d69-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="e8d69-517">從起始整數建立整數陣列，且其中包含一些項目。</span><span class="sxs-lookup"><span data-stu-id="e8d69-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-518">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-518">Parameters</span></span>

| <span data-ttu-id="e8d69-519">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-519">Parameter</span></span> | <span data-ttu-id="e8d69-520">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-520">Required</span></span> | <span data-ttu-id="e8d69-521">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-521">Type</span></span> | <span data-ttu-id="e8d69-522">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="e8d69-523">startingInteger</span></span> |<span data-ttu-id="e8d69-524">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-524">Yes</span></span> |<span data-ttu-id="e8d69-525">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-525">int</span></span> |<span data-ttu-id="e8d69-526">陣列中的第一個整數。</span><span class="sxs-lookup"><span data-stu-id="e8d69-526">The first integer in the array.</span></span> |
| <span data-ttu-id="e8d69-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="e8d69-527">numberofElements</span></span> |<span data-ttu-id="e8d69-528">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-528">Yes</span></span> |<span data-ttu-id="e8d69-529">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-529">int</span></span> |<span data-ttu-id="e8d69-530">陣列中的整數數目。</span><span class="sxs-lookup"><span data-stu-id="e8d69-530">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-531">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-531">Return value</span></span>

<span data-ttu-id="e8d69-532">整數陣列。</span><span class="sxs-lookup"><span data-stu-id="e8d69-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-533">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-533">Example</span></span>

<span data-ttu-id="e8d69-534">下列範例顯示如何使用 range 函式：</span><span class="sxs-lookup"><span data-stu-id="e8d69-534">The following example shows how to use the range function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-535">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-535">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-536">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-536">Name</span></span> | <span data-ttu-id="e8d69-537">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-537">Type</span></span> | <span data-ttu-id="e8d69-538">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-539">rangeOutput</span></span> | <span data-ttu-id="e8d69-540">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-540">Array</span></span> | <span data-ttu-id="e8d69-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="e8d69-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="e8d69-542">skip</span><span class="sxs-lookup"><span data-stu-id="e8d69-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="e8d69-543">傳回陣列中位於指定數字之後的所有元素所形成的陣列，或傳回字串中位於指定數字之後的所有字元所組成的字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-543">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-544">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-544">Parameters</span></span>

| <span data-ttu-id="e8d69-545">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-545">Parameter</span></span> | <span data-ttu-id="e8d69-546">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-546">Required</span></span> | <span data-ttu-id="e8d69-547">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-547">Type</span></span> | <span data-ttu-id="e8d69-548">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="e8d69-549">originalValue</span></span> |<span data-ttu-id="e8d69-550">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-550">Yes</span></span> |<span data-ttu-id="e8d69-551">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-551">array or string</span></span> |<span data-ttu-id="e8d69-552">要用於略過的陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-552">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="e8d69-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="e8d69-553">numberToSkip</span></span> |<span data-ttu-id="e8d69-554">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-554">Yes</span></span> |<span data-ttu-id="e8d69-555">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-555">int</span></span> |<span data-ttu-id="e8d69-556">要略過的元素或字元數。</span><span class="sxs-lookup"><span data-stu-id="e8d69-556">The number of elements or characters to skip.</span></span> <span data-ttu-id="e8d69-557">如果此值為 0 或更小的值，則會傳回值內的所有元素或字元。</span><span class="sxs-lookup"><span data-stu-id="e8d69-557">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="e8d69-558">如果此值大於陣列或字串的長度，則會傳回空白陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-558">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-559">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-559">Return value</span></span>

<span data-ttu-id="e8d69-560">陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-561">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-561">Example</span></span>

<span data-ttu-id="e8d69-562">下列範例會略過陣列中指定的元素數目，以及字串中指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="e8d69-562">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-563">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-564">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-564">Name</span></span> | <span data-ttu-id="e8d69-565">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-565">Type</span></span> | <span data-ttu-id="e8d69-566">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-567">arrayOutput</span></span> | <span data-ttu-id="e8d69-568">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-568">Array</span></span> | <span data-ttu-id="e8d69-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="e8d69-569">["three"]</span></span> |
| <span data-ttu-id="e8d69-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-570">stringOutput</span></span> | <span data-ttu-id="e8d69-571">String</span><span class="sxs-lookup"><span data-stu-id="e8d69-571">String</span></span> | <span data-ttu-id="e8d69-572">two three</span><span class="sxs-lookup"><span data-stu-id="e8d69-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="e8d69-573">take</span><span class="sxs-lookup"><span data-stu-id="e8d69-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="e8d69-574">傳回由陣列開頭的指定元素數目所組成的陣列，或傳回由字串開頭的指定字元數目所形成的字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-574">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-575">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-575">Parameters</span></span>

| <span data-ttu-id="e8d69-576">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-576">Parameter</span></span> | <span data-ttu-id="e8d69-577">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-577">Required</span></span> | <span data-ttu-id="e8d69-578">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-578">Type</span></span> | <span data-ttu-id="e8d69-579">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="e8d69-580">originalValue</span></span> |<span data-ttu-id="e8d69-581">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-581">Yes</span></span> |<span data-ttu-id="e8d69-582">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="e8d69-582">array or string</span></span> |<span data-ttu-id="e8d69-583">要從其中擷取元素的陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-583">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="e8d69-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="e8d69-584">numberToTake</span></span> |<span data-ttu-id="e8d69-585">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-585">Yes</span></span> |<span data-ttu-id="e8d69-586">int</span><span class="sxs-lookup"><span data-stu-id="e8d69-586">int</span></span> |<span data-ttu-id="e8d69-587">要擷取的元素或字元數。</span><span class="sxs-lookup"><span data-stu-id="e8d69-587">The number of elements or characters to take.</span></span> <span data-ttu-id="e8d69-588">如果此值為 0 或更小的值，則會傳回空白陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="e8d69-589">如果此值大於給定陣列或字串的長度，則會傳回陣列或字串中的所有元素。</span><span class="sxs-lookup"><span data-stu-id="e8d69-589">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-590">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-590">Return value</span></span>

<span data-ttu-id="e8d69-591">陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="e8d69-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-592">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-592">Example</span></span>

<span data-ttu-id="e8d69-593">下列範例會從陣列中取得指定的元素數目，以及從字串中取得指定的字元數目。</span><span class="sxs-lookup"><span data-stu-id="e8d69-593">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-594">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-594">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-595">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-595">Name</span></span> | <span data-ttu-id="e8d69-596">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-596">Type</span></span> | <span data-ttu-id="e8d69-597">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-598">arrayOutput</span></span> | <span data-ttu-id="e8d69-599">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-599">Array</span></span> | <span data-ttu-id="e8d69-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="e8d69-600">["one", "two"]</span></span> |
| <span data-ttu-id="e8d69-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-601">stringOutput</span></span> | <span data-ttu-id="e8d69-602">String</span><span class="sxs-lookup"><span data-stu-id="e8d69-602">String</span></span> | <span data-ttu-id="e8d69-603">on</span><span class="sxs-lookup"><span data-stu-id="e8d69-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="e8d69-604">union</span><span class="sxs-lookup"><span data-stu-id="e8d69-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="e8d69-605">從參數中傳回具有所有元素的單一陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="e8d69-605">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="e8d69-606">重複的值或索引鍵只會納入一次。</span><span class="sxs-lookup"><span data-stu-id="e8d69-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="e8d69-607">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-607">Parameters</span></span>

| <span data-ttu-id="e8d69-608">參數</span><span class="sxs-lookup"><span data-stu-id="e8d69-608">Parameter</span></span> | <span data-ttu-id="e8d69-609">必要</span><span class="sxs-lookup"><span data-stu-id="e8d69-609">Required</span></span> | <span data-ttu-id="e8d69-610">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-610">Type</span></span> | <span data-ttu-id="e8d69-611">說明</span><span class="sxs-lookup"><span data-stu-id="e8d69-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8d69-612">arg1</span><span class="sxs-lookup"><span data-stu-id="e8d69-612">arg1</span></span> |<span data-ttu-id="e8d69-613">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-613">Yes</span></span> |<span data-ttu-id="e8d69-614">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-614">array or object</span></span> |<span data-ttu-id="e8d69-615">用來聯結元素的第一個值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-615">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="e8d69-616">arg2</span><span class="sxs-lookup"><span data-stu-id="e8d69-616">arg2</span></span> |<span data-ttu-id="e8d69-617">是</span><span class="sxs-lookup"><span data-stu-id="e8d69-617">Yes</span></span> |<span data-ttu-id="e8d69-618">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-618">array or object</span></span> |<span data-ttu-id="e8d69-619">用來聯結元素的第二個值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-619">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="e8d69-620">其他引數</span><span class="sxs-lookup"><span data-stu-id="e8d69-620">additional arguments</span></span> |<span data-ttu-id="e8d69-621">否</span><span class="sxs-lookup"><span data-stu-id="e8d69-621">No</span></span> |<span data-ttu-id="e8d69-622">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="e8d69-622">array or object</span></span> |<span data-ttu-id="e8d69-623">用來聯結元素的其他值。</span><span class="sxs-lookup"><span data-stu-id="e8d69-623">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e8d69-624">傳回值</span><span class="sxs-lookup"><span data-stu-id="e8d69-624">Return value</span></span>

<span data-ttu-id="e8d69-625">陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="e8d69-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="e8d69-626">範例</span><span class="sxs-lookup"><span data-stu-id="e8d69-626">Example</span></span>

<span data-ttu-id="e8d69-627">下列範例顯示如何搭配使用 union 與陣列和物件︰</span><span class="sxs-lookup"><span data-stu-id="e8d69-627">The following example shows how to use union with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="e8d69-628">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e8d69-628">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="e8d69-629">名稱</span><span class="sxs-lookup"><span data-stu-id="e8d69-629">Name</span></span> | <span data-ttu-id="e8d69-630">類型</span><span class="sxs-lookup"><span data-stu-id="e8d69-630">Type</span></span> | <span data-ttu-id="e8d69-631">值</span><span class="sxs-lookup"><span data-stu-id="e8d69-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e8d69-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-632">objectOutput</span></span> | <span data-ttu-id="e8d69-633">Object</span><span class="sxs-lookup"><span data-stu-id="e8d69-633">Object</span></span> | <span data-ttu-id="e8d69-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="e8d69-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="e8d69-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e8d69-635">arrayOutput</span></span> | <span data-ttu-id="e8d69-636">陣列</span><span class="sxs-lookup"><span data-stu-id="e8d69-636">Array</span></span> | <span data-ttu-id="e8d69-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="e8d69-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8d69-638">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8d69-638">Next steps</span></span>
* <span data-ttu-id="e8d69-639">如需有關 Azure Resource Manager 範本中各區段的說明，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="e8d69-639">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e8d69-640">若要合併多個範本，請參閱[透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="e8d69-640">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="e8d69-641">若要依指定的次數重複建立資源類型，請參閱 [在 Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="e8d69-641">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="e8d69-642">若要了解如何部署已建立的範本，請參閱[使用 Azure Resource Manager 範本部署應用程式](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="e8d69-642">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

