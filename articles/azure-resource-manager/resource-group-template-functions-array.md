---
title: "aaaAzure Resource Manager 範本函式-陣列和物件 |Microsoft 文件"
description: "描述使用陣列和物件的 Azure Resource Manager 範本中的 hello 函式 toouse。"
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
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="15bc5-103">Azure Resource Manager 範本的陣列和物件函式</span><span class="sxs-lookup"><span data-stu-id="15bc5-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="15bc5-104">Resource Manager 提供了幾個用來使用陣列和物件的函式。</span><span class="sxs-lookup"><span data-stu-id="15bc5-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="15bc5-105">array</span><span class="sxs-lookup"><span data-stu-id="15bc5-105">array</span></span>](#array)
* [<span data-ttu-id="15bc5-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="15bc5-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="15bc5-107">concat</span><span class="sxs-lookup"><span data-stu-id="15bc5-107">concat</span></span>](#concat)
* [<span data-ttu-id="15bc5-108">contains</span><span class="sxs-lookup"><span data-stu-id="15bc5-108">contains</span></span>](#contains)
* [<span data-ttu-id="15bc5-109">createArray</span><span class="sxs-lookup"><span data-stu-id="15bc5-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="15bc5-110">empty</span><span class="sxs-lookup"><span data-stu-id="15bc5-110">empty</span></span>](#empty)
* [<span data-ttu-id="15bc5-111">first</span><span class="sxs-lookup"><span data-stu-id="15bc5-111">first</span></span>](#first)
* [<span data-ttu-id="15bc5-112">intersection</span><span class="sxs-lookup"><span data-stu-id="15bc5-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="15bc5-113">json</span><span class="sxs-lookup"><span data-stu-id="15bc5-113">json</span></span>](#json)
* [<span data-ttu-id="15bc5-114">last</span><span class="sxs-lookup"><span data-stu-id="15bc5-114">last</span></span>](#last)
* [<span data-ttu-id="15bc5-115">length</span><span class="sxs-lookup"><span data-stu-id="15bc5-115">length</span></span>](#length)
* [<span data-ttu-id="15bc5-116">min</span><span class="sxs-lookup"><span data-stu-id="15bc5-116">min</span></span>](#min)
* [<span data-ttu-id="15bc5-117">max</span><span class="sxs-lookup"><span data-stu-id="15bc5-117">max</span></span>](#max)
* [<span data-ttu-id="15bc5-118">range</span><span class="sxs-lookup"><span data-stu-id="15bc5-118">range</span></span>](#range)
* [<span data-ttu-id="15bc5-119">skip</span><span class="sxs-lookup"><span data-stu-id="15bc5-119">skip</span></span>](#skip)
* [<span data-ttu-id="15bc5-120">take</span><span class="sxs-lookup"><span data-stu-id="15bc5-120">take</span></span>](#take)
* [<span data-ttu-id="15bc5-121">union</span><span class="sxs-lookup"><span data-stu-id="15bc5-121">union</span></span>](#union)

<span data-ttu-id="15bc5-122">請參閱 tooget 值，以分隔的字串值的陣列[分割](resource-group-template-functions-string.md#split)。</span><span class="sxs-lookup"><span data-stu-id="15bc5-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="15bc5-123">array</span><span class="sxs-lookup"><span data-stu-id="15bc5-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="15bc5-124">將轉換 hello 值 tooan 陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-125">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-125">Parameters</span></span>

| <span data-ttu-id="15bc5-126">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-126">Parameter</span></span> | <span data-ttu-id="15bc5-127">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-127">Required</span></span> | <span data-ttu-id="15bc5-128">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-128">Type</span></span> | <span data-ttu-id="15bc5-129">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="15bc5-130">convertToArray</span></span> |<span data-ttu-id="15bc5-131">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-131">Yes</span></span> |<span data-ttu-id="15bc5-132">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-132">int, string, array, or object</span></span> |<span data-ttu-id="15bc5-133">hello 值 tooconvert tooan 陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-134">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-134">Return value</span></span>

<span data-ttu-id="15bc5-135">陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-136">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-136">Example</span></span>

<span data-ttu-id="15bc5-137">hello 下列範例顯示如何 toouse hello 與不同類型的陣列函式。</span><span class="sxs-lookup"><span data-stu-id="15bc5-137">hello following example shows how toouse hello array function with different types.</span></span>

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

<span data-ttu-id="15bc5-138">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-139">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-139">Name</span></span> | <span data-ttu-id="15bc5-140">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-140">Type</span></span> | <span data-ttu-id="15bc5-141">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-142">intOutput</span></span> | <span data-ttu-id="15bc5-143">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-143">Array</span></span> | <span data-ttu-id="15bc5-144">[1]</span><span class="sxs-lookup"><span data-stu-id="15bc5-144">[1]</span></span> |
| <span data-ttu-id="15bc5-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-145">stringOutput</span></span> | <span data-ttu-id="15bc5-146">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-146">Array</span></span> | <span data-ttu-id="15bc5-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="15bc5-147">["a"]</span></span> |
| <span data-ttu-id="15bc5-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-148">objectOutput</span></span> | <span data-ttu-id="15bc5-149">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-149">Array</span></span> | <span data-ttu-id="15bc5-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="15bc5-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="15bc5-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="15bc5-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="15bc5-152">從 hello 參數中傳回第一個非 null 值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="15bc5-153">空白字串、空白陣列和空白物件不是 null。</span><span class="sxs-lookup"><span data-stu-id="15bc5-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-154">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-154">Parameters</span></span>

| <span data-ttu-id="15bc5-155">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-155">Parameter</span></span> | <span data-ttu-id="15bc5-156">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-156">Required</span></span> | <span data-ttu-id="15bc5-157">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-157">Type</span></span> | <span data-ttu-id="15bc5-158">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-159">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-159">arg1</span></span> |<span data-ttu-id="15bc5-160">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-160">Yes</span></span> |<span data-ttu-id="15bc5-161">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-161">int, string, array, or object</span></span> |<span data-ttu-id="15bc5-162">hello 第一個值 tootest 為 null 的。</span><span class="sxs-lookup"><span data-stu-id="15bc5-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="15bc5-163">其他引數</span><span class="sxs-lookup"><span data-stu-id="15bc5-163">additional args</span></span> |<span data-ttu-id="15bc5-164">否</span><span class="sxs-lookup"><span data-stu-id="15bc5-164">No</span></span> |<span data-ttu-id="15bc5-165">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-165">int, string, array, or object</span></span> |<span data-ttu-id="15bc5-166">將 tootest 額外的值為 null 的。</span><span class="sxs-lookup"><span data-stu-id="15bc5-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-167">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-167">Return value</span></span>

<span data-ttu-id="15bc5-168">hello hello 第一個非 null 參數值，它可以是字串、 int、 陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="15bc5-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="15bc5-169">如果所有參數都是 null，則傳回 null。</span><span class="sxs-lookup"><span data-stu-id="15bc5-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="15bc5-170">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-170">Example</span></span>

<span data-ttu-id="15bc5-171">hello 下列範例顯示不同用法 coalesce hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="15bc5-171">hello following example shows hello output from different uses of coalesce.</span></span>

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

<span data-ttu-id="15bc5-172">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-173">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-173">Name</span></span> | <span data-ttu-id="15bc5-174">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-174">Type</span></span> | <span data-ttu-id="15bc5-175">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-176">stringOutput</span></span> | <span data-ttu-id="15bc5-177">String</span><span class="sxs-lookup"><span data-stu-id="15bc5-177">String</span></span> | <span data-ttu-id="15bc5-178">預設值</span><span class="sxs-lookup"><span data-stu-id="15bc5-178">default</span></span> |
| <span data-ttu-id="15bc5-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-179">intOutput</span></span> | <span data-ttu-id="15bc5-180">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-180">Int</span></span> | <span data-ttu-id="15bc5-181">1</span><span class="sxs-lookup"><span data-stu-id="15bc5-181">1</span></span> |
| <span data-ttu-id="15bc5-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-182">objectOutput</span></span> | <span data-ttu-id="15bc5-183">Object</span><span class="sxs-lookup"><span data-stu-id="15bc5-183">Object</span></span> | <span data-ttu-id="15bc5-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="15bc5-184">{"first": "default"}</span></span> |
| <span data-ttu-id="15bc5-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-185">arrayOutput</span></span> | <span data-ttu-id="15bc5-186">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-186">Array</span></span> | <span data-ttu-id="15bc5-187">[1]</span><span class="sxs-lookup"><span data-stu-id="15bc5-187">[1]</span></span> |
| <span data-ttu-id="15bc5-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-188">emptyOutput</span></span> | <span data-ttu-id="15bc5-189">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-189">Bool</span></span> | <span data-ttu-id="15bc5-190">True</span><span class="sxs-lookup"><span data-stu-id="15bc5-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="15bc5-191">concat</span><span class="sxs-lookup"><span data-stu-id="15bc5-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="15bc5-192">結合多個陣列並傳回串連的 hello 陣列，或結合多個字串值，並傳回 hello 串連字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="15bc5-193">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-193">Parameters</span></span>

| <span data-ttu-id="15bc5-194">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-194">Parameter</span></span> | <span data-ttu-id="15bc5-195">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-195">Required</span></span> | <span data-ttu-id="15bc5-196">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-196">Type</span></span> | <span data-ttu-id="15bc5-197">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-198">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-198">arg1</span></span> |<span data-ttu-id="15bc5-199">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-199">Yes</span></span> |<span data-ttu-id="15bc5-200">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-200">array or string</span></span> |<span data-ttu-id="15bc5-201">hello 第一個陣列或字串串連。</span><span class="sxs-lookup"><span data-stu-id="15bc5-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="15bc5-202">其他引數</span><span class="sxs-lookup"><span data-stu-id="15bc5-202">additional arguments</span></span> |<span data-ttu-id="15bc5-203">否</span><span class="sxs-lookup"><span data-stu-id="15bc5-203">No</span></span> |<span data-ttu-id="15bc5-204">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-204">array or string</span></span> |<span data-ttu-id="15bc5-205">串連的其他陣列或字串 (循序順序)。</span><span class="sxs-lookup"><span data-stu-id="15bc5-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="15bc5-206">此函式可以接受任意數目的引數，並且可以接受字串或陣列以進行 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="15bc5-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="15bc5-207">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-207">Return value</span></span>
<span data-ttu-id="15bc5-208">串連值的字串或陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-209">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-209">Example</span></span>

<span data-ttu-id="15bc5-210">hello 下列範例顯示兩個 toocombine 的陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-210">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="15bc5-211">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-212">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-212">Name</span></span> | <span data-ttu-id="15bc5-213">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-213">Type</span></span> | <span data-ttu-id="15bc5-214">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-215">return</span><span class="sxs-lookup"><span data-stu-id="15bc5-215">return</span></span> | <span data-ttu-id="15bc5-216">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-216">Array</span></span> | <span data-ttu-id="15bc5-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="15bc5-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="15bc5-218">hello 下列範例將說明如何 toocombine 兩個字串值，並傳回串連的字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="15bc5-219">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-220">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-220">Name</span></span> | <span data-ttu-id="15bc5-221">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-221">Type</span></span> | <span data-ttu-id="15bc5-222">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-223">concatOutput</span></span> | <span data-ttu-id="15bc5-224">String</span><span class="sxs-lookup"><span data-stu-id="15bc5-224">String</span></span> | <span data-ttu-id="15bc5-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="15bc5-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="15bc5-226">contains</span><span class="sxs-lookup"><span data-stu-id="15bc5-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="15bc5-227">檢查陣列中是否包含值、物件中是否包含索引鍵，或字串中是否包含子字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-228">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-228">Parameters</span></span>

| <span data-ttu-id="15bc5-229">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-229">Parameter</span></span> | <span data-ttu-id="15bc5-230">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-230">Required</span></span> | <span data-ttu-id="15bc5-231">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-231">Type</span></span> | <span data-ttu-id="15bc5-232">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-233">container</span><span class="sxs-lookup"><span data-stu-id="15bc5-233">container</span></span> |<span data-ttu-id="15bc5-234">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-234">Yes</span></span> |<span data-ttu-id="15bc5-235">陣列、物件或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-235">array, object, or string</span></span> |<span data-ttu-id="15bc5-236">包含 hello 值 toofind hello 值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="15bc5-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="15bc5-237">itemToFind</span></span> |<span data-ttu-id="15bc5-238">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-238">Yes</span></span> |<span data-ttu-id="15bc5-239">字串或整數</span><span class="sxs-lookup"><span data-stu-id="15bc5-239">string or int</span></span> |<span data-ttu-id="15bc5-240">hello 值 toofind。</span><span class="sxs-lookup"><span data-stu-id="15bc5-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-241">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-241">Return value</span></span>

<span data-ttu-id="15bc5-242">**True** hello 項目是否找到則為**False**。</span><span class="sxs-lookup"><span data-stu-id="15bc5-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-243">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-243">Example</span></span>

<span data-ttu-id="15bc5-244">hello 下列範例顯示如何 toouse 包含與不同類型：</span><span class="sxs-lookup"><span data-stu-id="15bc5-244">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="15bc5-245">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-246">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-246">Name</span></span> | <span data-ttu-id="15bc5-247">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-247">Type</span></span> | <span data-ttu-id="15bc5-248">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="15bc5-249">stringTrue</span></span> | <span data-ttu-id="15bc5-250">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-250">Bool</span></span> | <span data-ttu-id="15bc5-251">True</span><span class="sxs-lookup"><span data-stu-id="15bc5-251">True</span></span> |
| <span data-ttu-id="15bc5-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="15bc5-252">stringFalse</span></span> | <span data-ttu-id="15bc5-253">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-253">Bool</span></span> | <span data-ttu-id="15bc5-254">False</span><span class="sxs-lookup"><span data-stu-id="15bc5-254">False</span></span> |
| <span data-ttu-id="15bc5-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="15bc5-255">objectTrue</span></span> | <span data-ttu-id="15bc5-256">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-256">Bool</span></span> | <span data-ttu-id="15bc5-257">True</span><span class="sxs-lookup"><span data-stu-id="15bc5-257">True</span></span> |
| <span data-ttu-id="15bc5-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="15bc5-258">objectFalse</span></span> | <span data-ttu-id="15bc5-259">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-259">Bool</span></span> | <span data-ttu-id="15bc5-260">False</span><span class="sxs-lookup"><span data-stu-id="15bc5-260">False</span></span> |
| <span data-ttu-id="15bc5-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="15bc5-261">arrayTrue</span></span> | <span data-ttu-id="15bc5-262">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-262">Bool</span></span> | <span data-ttu-id="15bc5-263">True</span><span class="sxs-lookup"><span data-stu-id="15bc5-263">True</span></span> |
| <span data-ttu-id="15bc5-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="15bc5-264">arrayFalse</span></span> | <span data-ttu-id="15bc5-265">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-265">Bool</span></span> | <span data-ttu-id="15bc5-266">False</span><span class="sxs-lookup"><span data-stu-id="15bc5-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="15bc5-267">createarray</span><span class="sxs-lookup"><span data-stu-id="15bc5-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="15bc5-268">建立從 hello 參數的陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-269">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-269">Parameters</span></span>

| <span data-ttu-id="15bc5-270">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-270">Parameter</span></span> | <span data-ttu-id="15bc5-271">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-271">Required</span></span> | <span data-ttu-id="15bc5-272">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-272">Type</span></span> | <span data-ttu-id="15bc5-273">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-274">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-274">arg1</span></span> |<span data-ttu-id="15bc5-275">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-275">Yes</span></span> |<span data-ttu-id="15bc5-276">字串、整數、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="15bc5-277">hello hello 陣列中的第一個值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="15bc5-278">其他引數</span><span class="sxs-lookup"><span data-stu-id="15bc5-278">additional arguments</span></span> |<span data-ttu-id="15bc5-279">否</span><span class="sxs-lookup"><span data-stu-id="15bc5-279">No</span></span> |<span data-ttu-id="15bc5-280">字串、整數、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="15bc5-281">Hello 陣列中的其他值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-282">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-282">Return value</span></span>

<span data-ttu-id="15bc5-283">陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-284">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-284">Example</span></span>

<span data-ttu-id="15bc5-285">下列範例會示範如何 hello toouse createArray 與不同類型：</span><span class="sxs-lookup"><span data-stu-id="15bc5-285">hello following example shows how toouse createArray with different types:</span></span>

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

<span data-ttu-id="15bc5-286">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-287">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-287">Name</span></span> | <span data-ttu-id="15bc5-288">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-288">Type</span></span> | <span data-ttu-id="15bc5-289">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="15bc5-290">stringArray</span></span> | <span data-ttu-id="15bc5-291">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-291">Array</span></span> | <span data-ttu-id="15bc5-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="15bc5-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="15bc5-293">intArray</span><span class="sxs-lookup"><span data-stu-id="15bc5-293">intArray</span></span> | <span data-ttu-id="15bc5-294">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-294">Array</span></span> | <span data-ttu-id="15bc5-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="15bc5-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="15bc5-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="15bc5-296">objectArray</span></span> | <span data-ttu-id="15bc5-297">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-297">Array</span></span> | <span data-ttu-id="15bc5-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="15bc5-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="15bc5-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="15bc5-299">arrayArray</span></span> | <span data-ttu-id="15bc5-300">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-300">Array</span></span> | <span data-ttu-id="15bc5-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="15bc5-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="15bc5-302">empty</span><span class="sxs-lookup"><span data-stu-id="15bc5-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="15bc5-303">判斷陣列、物件或字串是否空白。</span><span class="sxs-lookup"><span data-stu-id="15bc5-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-304">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-304">Parameters</span></span>

| <span data-ttu-id="15bc5-305">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-305">Parameter</span></span> | <span data-ttu-id="15bc5-306">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-306">Required</span></span> | <span data-ttu-id="15bc5-307">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-307">Type</span></span> | <span data-ttu-id="15bc5-308">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="15bc5-309">itemToTest</span></span> |<span data-ttu-id="15bc5-310">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-310">Yes</span></span> |<span data-ttu-id="15bc5-311">陣列、物件或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-311">array, object, or string</span></span> |<span data-ttu-id="15bc5-312">hello 值 toocheck，如果是空白。</span><span class="sxs-lookup"><span data-stu-id="15bc5-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-313">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-313">Return value</span></span>

<span data-ttu-id="15bc5-314">傳回**True** hello 值是空的否則如果**False**。</span><span class="sxs-lookup"><span data-stu-id="15bc5-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-315">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-315">Example</span></span>

<span data-ttu-id="15bc5-316">下列範例會檢查是否是空的陣列、 物件和字串 hello。</span><span class="sxs-lookup"><span data-stu-id="15bc5-316">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="15bc5-317">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-318">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-318">Name</span></span> | <span data-ttu-id="15bc5-319">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-319">Type</span></span> | <span data-ttu-id="15bc5-320">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="15bc5-321">arrayEmpty</span></span> | <span data-ttu-id="15bc5-322">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-322">Bool</span></span> | <span data-ttu-id="15bc5-323">True</span><span class="sxs-lookup"><span data-stu-id="15bc5-323">True</span></span> |
| <span data-ttu-id="15bc5-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="15bc5-324">objectEmpty</span></span> | <span data-ttu-id="15bc5-325">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-325">Bool</span></span> | <span data-ttu-id="15bc5-326">True</span><span class="sxs-lookup"><span data-stu-id="15bc5-326">True</span></span> |
| <span data-ttu-id="15bc5-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="15bc5-327">stringEmpty</span></span> | <span data-ttu-id="15bc5-328">Bool</span><span class="sxs-lookup"><span data-stu-id="15bc5-328">Bool</span></span> | <span data-ttu-id="15bc5-329">True</span><span class="sxs-lookup"><span data-stu-id="15bc5-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="15bc5-330">first</span><span class="sxs-lookup"><span data-stu-id="15bc5-330">first</span></span>
`first(arg1)`

<span data-ttu-id="15bc5-331">傳回 hello hello 陣列的第一個項目或 hello 字串的第一個字元。</span><span class="sxs-lookup"><span data-stu-id="15bc5-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-332">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-332">Parameters</span></span>

| <span data-ttu-id="15bc5-333">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-333">Parameter</span></span> | <span data-ttu-id="15bc5-334">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-334">Required</span></span> | <span data-ttu-id="15bc5-335">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-335">Type</span></span> | <span data-ttu-id="15bc5-336">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-337">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-337">arg1</span></span> |<span data-ttu-id="15bc5-338">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-338">Yes</span></span> |<span data-ttu-id="15bc5-339">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-339">array or string</span></span> |<span data-ttu-id="15bc5-340">hello 值 tooretrieve hello 第一個項目或字元。</span><span class="sxs-lookup"><span data-stu-id="15bc5-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-341">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-341">Return value</span></span>

<span data-ttu-id="15bc5-342">hello hello 在陣列中，第一個項目類型 （字串、 int、 陣列或物件） 或 hello 第一個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-343">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-343">Example</span></span>

<span data-ttu-id="15bc5-344">hello 下列範例顯示如何 toouse hello 與陣列和字串的第一個函式。</span><span class="sxs-lookup"><span data-stu-id="15bc5-344">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="15bc5-345">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-346">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-346">Name</span></span> | <span data-ttu-id="15bc5-347">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-347">Type</span></span> | <span data-ttu-id="15bc5-348">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-349">arrayOutput</span></span> | <span data-ttu-id="15bc5-350">String</span><span class="sxs-lookup"><span data-stu-id="15bc5-350">String</span></span> | <span data-ttu-id="15bc5-351">one</span><span class="sxs-lookup"><span data-stu-id="15bc5-351">one</span></span> |
| <span data-ttu-id="15bc5-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-352">stringOutput</span></span> | <span data-ttu-id="15bc5-353">String</span><span class="sxs-lookup"><span data-stu-id="15bc5-353">String</span></span> | <span data-ttu-id="15bc5-354">O</span><span class="sxs-lookup"><span data-stu-id="15bc5-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="15bc5-355">交集</span><span class="sxs-lookup"><span data-stu-id="15bc5-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="15bc5-356">從 hello 參數中傳回的單一陣列或物件 hello 通用項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-357">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-357">Parameters</span></span>

| <span data-ttu-id="15bc5-358">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-358">Parameter</span></span> | <span data-ttu-id="15bc5-359">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-359">Required</span></span> | <span data-ttu-id="15bc5-360">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-360">Type</span></span> | <span data-ttu-id="15bc5-361">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-362">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-362">arg1</span></span> |<span data-ttu-id="15bc5-363">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-363">Yes</span></span> |<span data-ttu-id="15bc5-364">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-364">array or object</span></span> |<span data-ttu-id="15bc5-365">hello 第一個值 toouse 尋找通用項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="15bc5-366">arg2</span><span class="sxs-lookup"><span data-stu-id="15bc5-366">arg2</span></span> |<span data-ttu-id="15bc5-367">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-367">Yes</span></span> |<span data-ttu-id="15bc5-368">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-368">array or object</span></span> |<span data-ttu-id="15bc5-369">hello 第二個值 toouse 尋找通用項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="15bc5-370">其他引數</span><span class="sxs-lookup"><span data-stu-id="15bc5-370">additional arguments</span></span> |<span data-ttu-id="15bc5-371">否</span><span class="sxs-lookup"><span data-stu-id="15bc5-371">No</span></span> |<span data-ttu-id="15bc5-372">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-372">array or object</span></span> |<span data-ttu-id="15bc5-373">其他值 toouse 尋找通用項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-374">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-374">Return value</span></span>

<span data-ttu-id="15bc5-375">陣列或物件與 hello 通用項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-376">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-376">Example</span></span>

<span data-ttu-id="15bc5-377">下列範例會顯示與 toouse 交集的陣列和物件 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="15bc5-378">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-379">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-379">Name</span></span> | <span data-ttu-id="15bc5-380">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-380">Type</span></span> | <span data-ttu-id="15bc5-381">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-382">objectOutput</span></span> | <span data-ttu-id="15bc5-383">Object</span><span class="sxs-lookup"><span data-stu-id="15bc5-383">Object</span></span> | <span data-ttu-id="15bc5-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="15bc5-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="15bc5-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-385">arrayOutput</span></span> | <span data-ttu-id="15bc5-386">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-386">Array</span></span> | <span data-ttu-id="15bc5-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="15bc5-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="15bc5-388">json</span><span class="sxs-lookup"><span data-stu-id="15bc5-388">json</span></span>
`json(arg1)`

<span data-ttu-id="15bc5-389">傳回 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="15bc5-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-390">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-390">Parameters</span></span>

| <span data-ttu-id="15bc5-391">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-391">Parameter</span></span> | <span data-ttu-id="15bc5-392">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-392">Required</span></span> | <span data-ttu-id="15bc5-393">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-393">Type</span></span> | <span data-ttu-id="15bc5-394">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-395">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-395">arg1</span></span> |<span data-ttu-id="15bc5-396">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-396">Yes</span></span> |<span data-ttu-id="15bc5-397">字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-397">string</span></span> |<span data-ttu-id="15bc5-398">hello 值 tooconvert tooJSON。</span><span class="sxs-lookup"><span data-stu-id="15bc5-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="15bc5-399">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-399">Return value</span></span>

<span data-ttu-id="15bc5-400">字串或空的物件，指定從 hello 的 hello JSON 物件時**null**指定。</span><span class="sxs-lookup"><span data-stu-id="15bc5-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-401">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-401">Example</span></span>

<span data-ttu-id="15bc5-402">下列範例會顯示與 toouse 交集的陣列和物件 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

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

<span data-ttu-id="15bc5-403">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-404">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-404">Name</span></span> | <span data-ttu-id="15bc5-405">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-405">Type</span></span> | <span data-ttu-id="15bc5-406">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-407">jsonOutput</span></span> | <span data-ttu-id="15bc5-408">Object</span><span class="sxs-lookup"><span data-stu-id="15bc5-408">Object</span></span> | <span data-ttu-id="15bc5-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="15bc5-409">{"a": "b"}</span></span> |
| <span data-ttu-id="15bc5-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-410">nullOutput</span></span> | <span data-ttu-id="15bc5-411">Boolean</span><span class="sxs-lookup"><span data-stu-id="15bc5-411">Boolean</span></span> | <span data-ttu-id="15bc5-412">True</span><span class="sxs-lookup"><span data-stu-id="15bc5-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="15bc5-413">last</span><span class="sxs-lookup"><span data-stu-id="15bc5-413">last</span></span>
`last (arg1)`

<span data-ttu-id="15bc5-414">傳回 hello hello 陣列的最後一個項目或 hello 字串的最後一個字元。</span><span class="sxs-lookup"><span data-stu-id="15bc5-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-415">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-415">Parameters</span></span>

| <span data-ttu-id="15bc5-416">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-416">Parameter</span></span> | <span data-ttu-id="15bc5-417">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-417">Required</span></span> | <span data-ttu-id="15bc5-418">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-418">Type</span></span> | <span data-ttu-id="15bc5-419">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-420">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-420">arg1</span></span> |<span data-ttu-id="15bc5-421">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-421">Yes</span></span> |<span data-ttu-id="15bc5-422">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-422">array or string</span></span> |<span data-ttu-id="15bc5-423">hello 值 tooretrieve hello 最後一個項目或字元。</span><span class="sxs-lookup"><span data-stu-id="15bc5-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-424">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-424">Return value</span></span>

<span data-ttu-id="15bc5-425">hello hello 在陣列中，最後一個項目類型 （字串、 int、 陣列或物件） 或 hello 最後一個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-426">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-426">Example</span></span>

<span data-ttu-id="15bc5-427">hello 下列範例顯示如何 toouse hello 與陣列和字串的最後一個函式。</span><span class="sxs-lookup"><span data-stu-id="15bc5-427">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="15bc5-428">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-429">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-429">Name</span></span> | <span data-ttu-id="15bc5-430">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-430">Type</span></span> | <span data-ttu-id="15bc5-431">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-432">arrayOutput</span></span> | <span data-ttu-id="15bc5-433">String</span><span class="sxs-lookup"><span data-stu-id="15bc5-433">String</span></span> | <span data-ttu-id="15bc5-434">three</span><span class="sxs-lookup"><span data-stu-id="15bc5-434">three</span></span> |
| <span data-ttu-id="15bc5-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-435">stringOutput</span></span> | <span data-ttu-id="15bc5-436">String</span><span class="sxs-lookup"><span data-stu-id="15bc5-436">String</span></span> | <span data-ttu-id="15bc5-437">e</span><span class="sxs-lookup"><span data-stu-id="15bc5-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="15bc5-438">length</span><span class="sxs-lookup"><span data-stu-id="15bc5-438">length</span></span>
`length(arg1)`

<span data-ttu-id="15bc5-439">傳回 hello 的元素數目，為陣列或字串中的字元。</span><span class="sxs-lookup"><span data-stu-id="15bc5-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-440">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-440">Parameters</span></span>

| <span data-ttu-id="15bc5-441">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-441">Parameter</span></span> | <span data-ttu-id="15bc5-442">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-442">Required</span></span> | <span data-ttu-id="15bc5-443">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-443">Type</span></span> | <span data-ttu-id="15bc5-444">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-445">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-445">arg1</span></span> |<span data-ttu-id="15bc5-446">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-446">Yes</span></span> |<span data-ttu-id="15bc5-447">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-447">array or string</span></span> |<span data-ttu-id="15bc5-448">hello 取得 hello 元素數的陣列 toouse 或 hello 字串 toouse 取得 hello 的字元數。</span><span class="sxs-lookup"><span data-stu-id="15bc5-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-449">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-449">Return value</span></span>

<span data-ttu-id="15bc5-450">整數。</span><span class="sxs-lookup"><span data-stu-id="15bc5-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="15bc5-451">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-451">Example</span></span>

<span data-ttu-id="15bc5-452">下列範例會示範如何 hello toouse 與陣列和字串的長度：</span><span class="sxs-lookup"><span data-stu-id="15bc5-452">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="15bc5-453">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-454">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-454">Name</span></span> | <span data-ttu-id="15bc5-455">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-455">Type</span></span> | <span data-ttu-id="15bc5-456">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="15bc5-457">arrayLength</span></span> | <span data-ttu-id="15bc5-458">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-458">Int</span></span> | <span data-ttu-id="15bc5-459">3</span><span class="sxs-lookup"><span data-stu-id="15bc5-459">3</span></span> |
| <span data-ttu-id="15bc5-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="15bc5-460">stringLength</span></span> | <span data-ttu-id="15bc5-461">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-461">Int</span></span> | <span data-ttu-id="15bc5-462">13</span><span class="sxs-lookup"><span data-stu-id="15bc5-462">13</span></span> |

<span data-ttu-id="15bc5-463">建立資源時，您可以使用此函式以陣列 toospecify hello 的反覆項目數目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="15bc5-464">在下列範例的 hello，hello 參數**siteNames**建立 hello 網站時，會參考名稱 toouse tooan 陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="15bc5-465">如需有關在此陣列中使用函式的詳細資訊，請參閱 [在 Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="15bc5-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="15bc5-466">Min</span><span class="sxs-lookup"><span data-stu-id="15bc5-466">min</span></span>
`min(arg1)`

<span data-ttu-id="15bc5-467">傳回 hello 從整數的陣列或以逗號分隔的整數清單的最小值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-468">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-468">Parameters</span></span>

| <span data-ttu-id="15bc5-469">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-469">Parameter</span></span> | <span data-ttu-id="15bc5-470">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-470">Required</span></span> | <span data-ttu-id="15bc5-471">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-471">Type</span></span> | <span data-ttu-id="15bc5-472">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-473">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-473">arg1</span></span> |<span data-ttu-id="15bc5-474">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-474">Yes</span></span> |<span data-ttu-id="15bc5-475">整數的陣列，或以逗號分隔的整數清單</span><span class="sxs-lookup"><span data-stu-id="15bc5-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="15bc5-476">hello 集合 tooget hello 最小值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-477">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-477">Return value</span></span>

<span data-ttu-id="15bc5-478">整數，代表 hello 最小值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-479">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-479">Example</span></span>

<span data-ttu-id="15bc5-480">下列範例會示範如何 hello toouse 最小值與整數清單和陣列：</span><span class="sxs-lookup"><span data-stu-id="15bc5-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="15bc5-481">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-482">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-482">Name</span></span> | <span data-ttu-id="15bc5-483">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-483">Type</span></span> | <span data-ttu-id="15bc5-484">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-485">arrayOutput</span></span> | <span data-ttu-id="15bc5-486">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-486">Int</span></span> | <span data-ttu-id="15bc5-487">0</span><span class="sxs-lookup"><span data-stu-id="15bc5-487">0</span></span> |
| <span data-ttu-id="15bc5-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-488">intOutput</span></span> | <span data-ttu-id="15bc5-489">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-489">Int</span></span> | <span data-ttu-id="15bc5-490">0</span><span class="sxs-lookup"><span data-stu-id="15bc5-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="15bc5-491">max</span><span class="sxs-lookup"><span data-stu-id="15bc5-491">max</span></span>
`max(arg1)`

<span data-ttu-id="15bc5-492">傳回 hello 從整數的陣列或以逗號分隔的整數清單的最大值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-493">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-493">Parameters</span></span>

| <span data-ttu-id="15bc5-494">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-494">Parameter</span></span> | <span data-ttu-id="15bc5-495">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-495">Required</span></span> | <span data-ttu-id="15bc5-496">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-496">Type</span></span> | <span data-ttu-id="15bc5-497">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-498">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-498">arg1</span></span> |<span data-ttu-id="15bc5-499">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-499">Yes</span></span> |<span data-ttu-id="15bc5-500">整數的陣列，或以逗號分隔的整數清單</span><span class="sxs-lookup"><span data-stu-id="15bc5-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="15bc5-501">hello 集合 tooget hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-502">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-502">Return value</span></span>

<span data-ttu-id="15bc5-503">整數，代表 hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="15bc5-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-504">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-504">Example</span></span>

<span data-ttu-id="15bc5-505">下列範例會示範如何 hello toouse 陣列與整數清單的最大值：</span><span class="sxs-lookup"><span data-stu-id="15bc5-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="15bc5-506">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-507">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-507">Name</span></span> | <span data-ttu-id="15bc5-508">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-508">Type</span></span> | <span data-ttu-id="15bc5-509">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-510">arrayOutput</span></span> | <span data-ttu-id="15bc5-511">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-511">Int</span></span> | <span data-ttu-id="15bc5-512">5</span><span class="sxs-lookup"><span data-stu-id="15bc5-512">5</span></span> |
| <span data-ttu-id="15bc5-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-513">intOutput</span></span> | <span data-ttu-id="15bc5-514">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-514">Int</span></span> | <span data-ttu-id="15bc5-515">5</span><span class="sxs-lookup"><span data-stu-id="15bc5-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="15bc5-516">range</span><span class="sxs-lookup"><span data-stu-id="15bc5-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="15bc5-517">從起始整數建立整數陣列，且其中包含一些項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-518">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-518">Parameters</span></span>

| <span data-ttu-id="15bc5-519">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-519">Parameter</span></span> | <span data-ttu-id="15bc5-520">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-520">Required</span></span> | <span data-ttu-id="15bc5-521">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-521">Type</span></span> | <span data-ttu-id="15bc5-522">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="15bc5-523">startingInteger</span></span> |<span data-ttu-id="15bc5-524">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-524">Yes</span></span> |<span data-ttu-id="15bc5-525">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-525">int</span></span> |<span data-ttu-id="15bc5-526">hello hello 陣列中的第一個整數。</span><span class="sxs-lookup"><span data-stu-id="15bc5-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="15bc5-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="15bc5-527">numberofElements</span></span> |<span data-ttu-id="15bc5-528">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-528">Yes</span></span> |<span data-ttu-id="15bc5-529">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-529">int</span></span> |<span data-ttu-id="15bc5-530">hello hello 陣列中的整數數目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-531">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-531">Return value</span></span>

<span data-ttu-id="15bc5-532">整數陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-533">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-533">Example</span></span>

<span data-ttu-id="15bc5-534">hello 下列範例顯示如何 toouse hello 範圍函式：</span><span class="sxs-lookup"><span data-stu-id="15bc5-534">hello following example shows how toouse hello range function:</span></span>

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

<span data-ttu-id="15bc5-535">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-536">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-536">Name</span></span> | <span data-ttu-id="15bc5-537">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-537">Type</span></span> | <span data-ttu-id="15bc5-538">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-539">rangeOutput</span></span> | <span data-ttu-id="15bc5-540">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-540">Array</span></span> | <span data-ttu-id="15bc5-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="15bc5-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="15bc5-542">skip</span><span class="sxs-lookup"><span data-stu-id="15bc5-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="15bc5-543">Hello hello 陣列中指定數目或 hello hello 字串中指定數字之後會傳回所有 hello 字元的字串之後，傳回所有 hello 元素的陣列。</span><span class="sxs-lookup"><span data-stu-id="15bc5-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-544">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-544">Parameters</span></span>

| <span data-ttu-id="15bc5-545">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-545">Parameter</span></span> | <span data-ttu-id="15bc5-546">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-546">Required</span></span> | <span data-ttu-id="15bc5-547">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-547">Type</span></span> | <span data-ttu-id="15bc5-548">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="15bc5-549">originalValue</span></span> |<span data-ttu-id="15bc5-550">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-550">Yes</span></span> |<span data-ttu-id="15bc5-551">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-551">array or string</span></span> |<span data-ttu-id="15bc5-552">hello 陣列或字串 toouse 跳過。</span><span class="sxs-lookup"><span data-stu-id="15bc5-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="15bc5-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="15bc5-553">numberToSkip</span></span> |<span data-ttu-id="15bc5-554">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-554">Yes</span></span> |<span data-ttu-id="15bc5-555">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-555">int</span></span> |<span data-ttu-id="15bc5-556">hello tooskip 項目或字元數目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="15bc5-557">如果此值為 0 或更少，所有 hello 項目，或傳回 hello 值中的字元。</span><span class="sxs-lookup"><span data-stu-id="15bc5-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="15bc5-558">如果大於 hello hello 陣列或字串的長度，就會傳回空陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-559">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-559">Return value</span></span>

<span data-ttu-id="15bc5-560">陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-561">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-561">Example</span></span>

<span data-ttu-id="15bc5-562">下列範例會略過 hello hello hello 陣列中指定的項目數目和 hello 的字串中指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="15bc5-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="15bc5-563">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-564">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-564">Name</span></span> | <span data-ttu-id="15bc5-565">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-565">Type</span></span> | <span data-ttu-id="15bc5-566">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-567">arrayOutput</span></span> | <span data-ttu-id="15bc5-568">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-568">Array</span></span> | <span data-ttu-id="15bc5-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="15bc5-569">["three"]</span></span> |
| <span data-ttu-id="15bc5-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-570">stringOutput</span></span> | <span data-ttu-id="15bc5-571">String</span><span class="sxs-lookup"><span data-stu-id="15bc5-571">String</span></span> | <span data-ttu-id="15bc5-572">two three</span><span class="sxs-lookup"><span data-stu-id="15bc5-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="15bc5-573">take</span><span class="sxs-lookup"><span data-stu-id="15bc5-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="15bc5-574">傳回以 hello 陣列指定的項目數從 hello hello 陣列的開頭或字串 hello 與指定的 hello hello 字串的開頭字元數。</span><span class="sxs-lookup"><span data-stu-id="15bc5-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-575">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-575">Parameters</span></span>

| <span data-ttu-id="15bc5-576">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-576">Parameter</span></span> | <span data-ttu-id="15bc5-577">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-577">Required</span></span> | <span data-ttu-id="15bc5-578">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-578">Type</span></span> | <span data-ttu-id="15bc5-579">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="15bc5-580">originalValue</span></span> |<span data-ttu-id="15bc5-581">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-581">Yes</span></span> |<span data-ttu-id="15bc5-582">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="15bc5-582">array or string</span></span> |<span data-ttu-id="15bc5-583">hello 陣列或字串 tootake hello 中的項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="15bc5-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="15bc5-584">numberToTake</span></span> |<span data-ttu-id="15bc5-585">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-585">Yes</span></span> |<span data-ttu-id="15bc5-586">int</span><span class="sxs-lookup"><span data-stu-id="15bc5-586">int</span></span> |<span data-ttu-id="15bc5-587">hello tootake 項目或字元數目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="15bc5-588">如果此值為 0 或更小的值，則會傳回空白陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="15bc5-589">如果它大於指定之陣列或字串 hello hello 長度，則會傳回所有 hello 陣列或字串中的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-590">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-590">Return value</span></span>

<span data-ttu-id="15bc5-591">陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="15bc5-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-592">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-592">Example</span></span>

<span data-ttu-id="15bc5-593">下列範例會採用 hello hello 指定 hello 陣列中的項目和從字串的字元數目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="15bc5-594">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-595">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-595">Name</span></span> | <span data-ttu-id="15bc5-596">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-596">Type</span></span> | <span data-ttu-id="15bc5-597">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-598">arrayOutput</span></span> | <span data-ttu-id="15bc5-599">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-599">Array</span></span> | <span data-ttu-id="15bc5-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="15bc5-600">["one", "two"]</span></span> |
| <span data-ttu-id="15bc5-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-601">stringOutput</span></span> | <span data-ttu-id="15bc5-602">String</span><span class="sxs-lookup"><span data-stu-id="15bc5-602">String</span></span> | <span data-ttu-id="15bc5-603">on</span><span class="sxs-lookup"><span data-stu-id="15bc5-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="15bc5-604">union</span><span class="sxs-lookup"><span data-stu-id="15bc5-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="15bc5-605">從 hello 參數中傳回的單一陣列或物件的所有項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="15bc5-606">重複的值或索引鍵只會納入一次。</span><span class="sxs-lookup"><span data-stu-id="15bc5-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="15bc5-607">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-607">Parameters</span></span>

| <span data-ttu-id="15bc5-608">參數</span><span class="sxs-lookup"><span data-stu-id="15bc5-608">Parameter</span></span> | <span data-ttu-id="15bc5-609">必要</span><span class="sxs-lookup"><span data-stu-id="15bc5-609">Required</span></span> | <span data-ttu-id="15bc5-610">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-610">Type</span></span> | <span data-ttu-id="15bc5-611">說明</span><span class="sxs-lookup"><span data-stu-id="15bc5-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="15bc5-612">arg1</span><span class="sxs-lookup"><span data-stu-id="15bc5-612">arg1</span></span> |<span data-ttu-id="15bc5-613">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-613">Yes</span></span> |<span data-ttu-id="15bc5-614">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-614">array or object</span></span> |<span data-ttu-id="15bc5-615">hello 第一個值 toouse 加入項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="15bc5-616">arg2</span><span class="sxs-lookup"><span data-stu-id="15bc5-616">arg2</span></span> |<span data-ttu-id="15bc5-617">是</span><span class="sxs-lookup"><span data-stu-id="15bc5-617">Yes</span></span> |<span data-ttu-id="15bc5-618">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-618">array or object</span></span> |<span data-ttu-id="15bc5-619">hello 第二個值 toouse 加入項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="15bc5-620">其他引數</span><span class="sxs-lookup"><span data-stu-id="15bc5-620">additional arguments</span></span> |<span data-ttu-id="15bc5-621">否</span><span class="sxs-lookup"><span data-stu-id="15bc5-621">No</span></span> |<span data-ttu-id="15bc5-622">陣列或物件</span><span class="sxs-lookup"><span data-stu-id="15bc5-622">array or object</span></span> |<span data-ttu-id="15bc5-623">其他值 toouse 加入項目。</span><span class="sxs-lookup"><span data-stu-id="15bc5-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="15bc5-624">傳回值</span><span class="sxs-lookup"><span data-stu-id="15bc5-624">Return value</span></span>

<span data-ttu-id="15bc5-625">陣列或物件。</span><span class="sxs-lookup"><span data-stu-id="15bc5-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="15bc5-626">範例</span><span class="sxs-lookup"><span data-stu-id="15bc5-626">Example</span></span>

<span data-ttu-id="15bc5-627">下列範例所示 toouse 聯集的陣列和物件 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-627">hello following example shows how toouse union with arrays and objects:</span></span>

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

<span data-ttu-id="15bc5-628">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="15bc5-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="15bc5-629">名稱</span><span class="sxs-lookup"><span data-stu-id="15bc5-629">Name</span></span> | <span data-ttu-id="15bc5-630">類型</span><span class="sxs-lookup"><span data-stu-id="15bc5-630">Type</span></span> | <span data-ttu-id="15bc5-631">值</span><span class="sxs-lookup"><span data-stu-id="15bc5-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="15bc5-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-632">objectOutput</span></span> | <span data-ttu-id="15bc5-633">Object</span><span class="sxs-lookup"><span data-stu-id="15bc5-633">Object</span></span> | <span data-ttu-id="15bc5-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="15bc5-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="15bc5-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="15bc5-635">arrayOutput</span></span> | <span data-ttu-id="15bc5-636">陣列</span><span class="sxs-lookup"><span data-stu-id="15bc5-636">Array</span></span> | <span data-ttu-id="15bc5-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="15bc5-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="15bc5-638">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15bc5-638">Next steps</span></span>
* <span data-ttu-id="15bc5-639">如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="15bc5-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="15bc5-640">toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="15bc5-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="15bc5-641">tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="15bc5-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="15bc5-642">toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="15bc5-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

