---
title: "aaaAzure 資源管理員範本函式-比較 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 toocompare 值中的 hello 函式 toouse。"
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="310c5-103">Azure Resource Manager 範本的比較函式</span><span class="sxs-lookup"><span data-stu-id="310c5-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="310c5-104">Resource Manager 提供了幾個用來在範本中進行比較的函式。</span><span class="sxs-lookup"><span data-stu-id="310c5-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="310c5-105">equals</span><span class="sxs-lookup"><span data-stu-id="310c5-105">equals</span></span>](#equals)
* [<span data-ttu-id="310c5-106">greater</span><span class="sxs-lookup"><span data-stu-id="310c5-106">greater</span></span>](#greater)
* [<span data-ttu-id="310c5-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="310c5-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="310c5-108">less</span><span class="sxs-lookup"><span data-stu-id="310c5-108">less</span></span>](#less)
* [<span data-ttu-id="310c5-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="310c5-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="310c5-110">equals</span><span class="sxs-lookup"><span data-stu-id="310c5-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="310c5-111">檢查兩個值是否彼此相等。</span><span class="sxs-lookup"><span data-stu-id="310c5-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="310c5-112">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-112">Parameters</span></span>

| <span data-ttu-id="310c5-113">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-113">Parameter</span></span> | <span data-ttu-id="310c5-114">必要</span><span class="sxs-lookup"><span data-stu-id="310c5-114">Required</span></span> | <span data-ttu-id="310c5-115">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-115">Type</span></span> | <span data-ttu-id="310c5-116">說明</span><span class="sxs-lookup"><span data-stu-id="310c5-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="310c5-117">arg1</span><span class="sxs-lookup"><span data-stu-id="310c5-117">arg1</span></span> |<span data-ttu-id="310c5-118">是</span><span class="sxs-lookup"><span data-stu-id="310c5-118">Yes</span></span> |<span data-ttu-id="310c5-119">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="310c5-119">int, string, array, or object</span></span> |<span data-ttu-id="310c5-120">hello 第一個值 toocheck 相等。</span><span class="sxs-lookup"><span data-stu-id="310c5-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="310c5-121">arg2</span><span class="sxs-lookup"><span data-stu-id="310c5-121">arg2</span></span> |<span data-ttu-id="310c5-122">是</span><span class="sxs-lookup"><span data-stu-id="310c5-122">Yes</span></span> |<span data-ttu-id="310c5-123">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="310c5-123">int, string, array, or object</span></span> |<span data-ttu-id="310c5-124">hello 第二個值 toocheck 相等。</span><span class="sxs-lookup"><span data-stu-id="310c5-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="310c5-125">傳回值</span><span class="sxs-lookup"><span data-stu-id="310c5-125">Return value</span></span>

<span data-ttu-id="310c5-126">傳回**True** hello 值是否相等; 否則**False**。</span><span class="sxs-lookup"><span data-stu-id="310c5-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="310c5-127">備註</span><span class="sxs-lookup"><span data-stu-id="310c5-127">Remarks</span></span>

<span data-ttu-id="310c5-128">hello equals 函式常用以 hello`condition`元素 tootest 是否部署資源。</span><span class="sxs-lookup"><span data-stu-id="310c5-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="310c5-129">範例</span><span class="sxs-lookup"><span data-stu-id="310c5-129">Example</span></span>

<span data-ttu-id="310c5-130">hello 範例範本會檢查不同類型的值相等。</span><span class="sxs-lookup"><span data-stu-id="310c5-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="310c5-131">所有的 hello 預設值為 true，則傳回。</span><span class="sxs-lookup"><span data-stu-id="310c5-131">All hello default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="310c5-132">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="310c5-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="310c5-133">名稱</span><span class="sxs-lookup"><span data-stu-id="310c5-133">Name</span></span> | <span data-ttu-id="310c5-134">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-134">Type</span></span> | <span data-ttu-id="310c5-135">值</span><span class="sxs-lookup"><span data-stu-id="310c5-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="310c5-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="310c5-136">checkInts</span></span> | <span data-ttu-id="310c5-137">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-137">Bool</span></span> | <span data-ttu-id="310c5-138">True</span><span class="sxs-lookup"><span data-stu-id="310c5-138">True</span></span> |
| <span data-ttu-id="310c5-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="310c5-139">checkStrings</span></span> | <span data-ttu-id="310c5-140">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-140">Bool</span></span> | <span data-ttu-id="310c5-141">True</span><span class="sxs-lookup"><span data-stu-id="310c5-141">True</span></span> |
| <span data-ttu-id="310c5-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="310c5-142">checkArrays</span></span> | <span data-ttu-id="310c5-143">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-143">Bool</span></span> | <span data-ttu-id="310c5-144">True</span><span class="sxs-lookup"><span data-stu-id="310c5-144">True</span></span> |
| <span data-ttu-id="310c5-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="310c5-145">checkObjects</span></span> | <span data-ttu-id="310c5-146">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-146">Bool</span></span> | <span data-ttu-id="310c5-147">True</span><span class="sxs-lookup"><span data-stu-id="310c5-147">True</span></span> |


<span data-ttu-id="310c5-148">hello 下列範例會使用[不](resource-group-template-functions-logical.md#not)與**等於**。</span><span class="sxs-lookup"><span data-stu-id="310c5-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="310c5-149">上述範例中的 hello hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="310c5-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="310c5-150">名稱</span><span class="sxs-lookup"><span data-stu-id="310c5-150">Name</span></span> | <span data-ttu-id="310c5-151">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-151">Type</span></span> | <span data-ttu-id="310c5-152">值</span><span class="sxs-lookup"><span data-stu-id="310c5-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="310c5-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="310c5-153">checkNotEquals</span></span> | <span data-ttu-id="310c5-154">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-154">Bool</span></span> | <span data-ttu-id="310c5-155">True</span><span class="sxs-lookup"><span data-stu-id="310c5-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="310c5-156">greater</span><span class="sxs-lookup"><span data-stu-id="310c5-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="310c5-157">檢查是否大於第二個值的 hello hello 第一個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="310c5-158">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-158">Parameters</span></span>

| <span data-ttu-id="310c5-159">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-159">Parameter</span></span> | <span data-ttu-id="310c5-160">必要</span><span class="sxs-lookup"><span data-stu-id="310c5-160">Required</span></span> | <span data-ttu-id="310c5-161">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-161">Type</span></span> | <span data-ttu-id="310c5-162">說明</span><span class="sxs-lookup"><span data-stu-id="310c5-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="310c5-163">arg1</span><span class="sxs-lookup"><span data-stu-id="310c5-163">arg1</span></span> |<span data-ttu-id="310c5-164">是</span><span class="sxs-lookup"><span data-stu-id="310c5-164">Yes</span></span> |<span data-ttu-id="310c5-165">整數或字串</span><span class="sxs-lookup"><span data-stu-id="310c5-165">int or string</span></span> |<span data-ttu-id="310c5-166">hello hello 大於比較的第一個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="310c5-167">arg2</span><span class="sxs-lookup"><span data-stu-id="310c5-167">arg2</span></span> |<span data-ttu-id="310c5-168">是</span><span class="sxs-lookup"><span data-stu-id="310c5-168">Yes</span></span> |<span data-ttu-id="310c5-169">整數或字串</span><span class="sxs-lookup"><span data-stu-id="310c5-169">int or string</span></span> |<span data-ttu-id="310c5-170">hello hello 大於比較的第二個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="310c5-171">傳回值</span><span class="sxs-lookup"><span data-stu-id="310c5-171">Return value</span></span>

<span data-ttu-id="310c5-172">傳回**True** hello 第一個值是大於 hello 第二個值; 否則如果**False**。</span><span class="sxs-lookup"><span data-stu-id="310c5-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="310c5-173">範例</span><span class="sxs-lookup"><span data-stu-id="310c5-173">Example</span></span>

<span data-ttu-id="310c5-174">hello 範例範本會檢查 hello 某個值是否大於 hello 其他。</span><span class="sxs-lookup"><span data-stu-id="310c5-174">hello example template checks whether hello one value is greater than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="310c5-175">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="310c5-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="310c5-176">名稱</span><span class="sxs-lookup"><span data-stu-id="310c5-176">Name</span></span> | <span data-ttu-id="310c5-177">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-177">Type</span></span> | <span data-ttu-id="310c5-178">值</span><span class="sxs-lookup"><span data-stu-id="310c5-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="310c5-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="310c5-179">checkInts</span></span> | <span data-ttu-id="310c5-180">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-180">Bool</span></span> | <span data-ttu-id="310c5-181">False</span><span class="sxs-lookup"><span data-stu-id="310c5-181">False</span></span> |
| <span data-ttu-id="310c5-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="310c5-182">checkStrings</span></span> | <span data-ttu-id="310c5-183">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-183">Bool</span></span> | <span data-ttu-id="310c5-184">True</span><span class="sxs-lookup"><span data-stu-id="310c5-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="310c5-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="310c5-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="310c5-186">檢查 hello 第一個值是否大於或等於 toohello 第二個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="310c5-187">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-187">Parameters</span></span>

| <span data-ttu-id="310c5-188">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-188">Parameter</span></span> | <span data-ttu-id="310c5-189">必要</span><span class="sxs-lookup"><span data-stu-id="310c5-189">Required</span></span> | <span data-ttu-id="310c5-190">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-190">Type</span></span> | <span data-ttu-id="310c5-191">說明</span><span class="sxs-lookup"><span data-stu-id="310c5-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="310c5-192">arg1</span><span class="sxs-lookup"><span data-stu-id="310c5-192">arg1</span></span> |<span data-ttu-id="310c5-193">是</span><span class="sxs-lookup"><span data-stu-id="310c5-193">Yes</span></span> |<span data-ttu-id="310c5-194">整數或字串</span><span class="sxs-lookup"><span data-stu-id="310c5-194">int or string</span></span> |<span data-ttu-id="310c5-195">hello hello 大於或等於比較的第一個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="310c5-196">arg2</span><span class="sxs-lookup"><span data-stu-id="310c5-196">arg2</span></span> |<span data-ttu-id="310c5-197">是</span><span class="sxs-lookup"><span data-stu-id="310c5-197">Yes</span></span> |<span data-ttu-id="310c5-198">整數或字串</span><span class="sxs-lookup"><span data-stu-id="310c5-198">int or string</span></span> |<span data-ttu-id="310c5-199">hello hello 大於或等於比較的第二個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="310c5-200">傳回值</span><span class="sxs-lookup"><span data-stu-id="310c5-200">Return value</span></span>

<span data-ttu-id="310c5-201">傳回**True** hello 第一個值是否大於或等於 toohello 第二個值; 否則**False**。</span><span class="sxs-lookup"><span data-stu-id="310c5-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="310c5-202">範例</span><span class="sxs-lookup"><span data-stu-id="310c5-202">Example</span></span>

<span data-ttu-id="310c5-203">hello 範例範本會在 hello 的一個值是否大於或等於 toohello 其他檢查。</span><span class="sxs-lookup"><span data-stu-id="310c5-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="310c5-204">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="310c5-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="310c5-205">名稱</span><span class="sxs-lookup"><span data-stu-id="310c5-205">Name</span></span> | <span data-ttu-id="310c5-206">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-206">Type</span></span> | <span data-ttu-id="310c5-207">值</span><span class="sxs-lookup"><span data-stu-id="310c5-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="310c5-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="310c5-208">checkInts</span></span> | <span data-ttu-id="310c5-209">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-209">Bool</span></span> | <span data-ttu-id="310c5-210">False</span><span class="sxs-lookup"><span data-stu-id="310c5-210">False</span></span> |
| <span data-ttu-id="310c5-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="310c5-211">checkStrings</span></span> | <span data-ttu-id="310c5-212">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-212">Bool</span></span> | <span data-ttu-id="310c5-213">True</span><span class="sxs-lookup"><span data-stu-id="310c5-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="310c5-214">less</span><span class="sxs-lookup"><span data-stu-id="310c5-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="310c5-215">檢查是否 hello 第一個值小於 hello 第二個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="310c5-216">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-216">Parameters</span></span>

| <span data-ttu-id="310c5-217">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-217">Parameter</span></span> | <span data-ttu-id="310c5-218">必要</span><span class="sxs-lookup"><span data-stu-id="310c5-218">Required</span></span> | <span data-ttu-id="310c5-219">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-219">Type</span></span> | <span data-ttu-id="310c5-220">說明</span><span class="sxs-lookup"><span data-stu-id="310c5-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="310c5-221">arg1</span><span class="sxs-lookup"><span data-stu-id="310c5-221">arg1</span></span> |<span data-ttu-id="310c5-222">是</span><span class="sxs-lookup"><span data-stu-id="310c5-222">Yes</span></span> |<span data-ttu-id="310c5-223">整數或字串</span><span class="sxs-lookup"><span data-stu-id="310c5-223">int or string</span></span> |<span data-ttu-id="310c5-224">hello hello 小於比較的第一個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="310c5-225">arg2</span><span class="sxs-lookup"><span data-stu-id="310c5-225">arg2</span></span> |<span data-ttu-id="310c5-226">是</span><span class="sxs-lookup"><span data-stu-id="310c5-226">Yes</span></span> |<span data-ttu-id="310c5-227">整數或字串</span><span class="sxs-lookup"><span data-stu-id="310c5-227">int or string</span></span> |<span data-ttu-id="310c5-228">hello hello 小於比較的第二個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="310c5-229">傳回值</span><span class="sxs-lookup"><span data-stu-id="310c5-229">Return value</span></span>

<span data-ttu-id="310c5-230">傳回**True** hello 第一個值是否小於 hello 第二個值; 否則**False**。</span><span class="sxs-lookup"><span data-stu-id="310c5-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="310c5-231">範例</span><span class="sxs-lookup"><span data-stu-id="310c5-231">Example</span></span>

<span data-ttu-id="310c5-232">hello 範例範本會檢查 hello 某個值是否小於其他 hello。</span><span class="sxs-lookup"><span data-stu-id="310c5-232">hello example template checks whether hello one value is less than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="310c5-233">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="310c5-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="310c5-234">名稱</span><span class="sxs-lookup"><span data-stu-id="310c5-234">Name</span></span> | <span data-ttu-id="310c5-235">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-235">Type</span></span> | <span data-ttu-id="310c5-236">值</span><span class="sxs-lookup"><span data-stu-id="310c5-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="310c5-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="310c5-237">checkInts</span></span> | <span data-ttu-id="310c5-238">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-238">Bool</span></span> | <span data-ttu-id="310c5-239">True</span><span class="sxs-lookup"><span data-stu-id="310c5-239">True</span></span> |
| <span data-ttu-id="310c5-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="310c5-240">checkStrings</span></span> | <span data-ttu-id="310c5-241">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-241">Bool</span></span> | <span data-ttu-id="310c5-242">False</span><span class="sxs-lookup"><span data-stu-id="310c5-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="310c5-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="310c5-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="310c5-244">檢查 hello 第一個值是否小於或等於 toohello 第二個值。</span><span class="sxs-lookup"><span data-stu-id="310c5-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="310c5-245">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-245">Parameters</span></span>

| <span data-ttu-id="310c5-246">參數</span><span class="sxs-lookup"><span data-stu-id="310c5-246">Parameter</span></span> | <span data-ttu-id="310c5-247">必要</span><span class="sxs-lookup"><span data-stu-id="310c5-247">Required</span></span> | <span data-ttu-id="310c5-248">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-248">Type</span></span> | <span data-ttu-id="310c5-249">說明</span><span class="sxs-lookup"><span data-stu-id="310c5-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="310c5-250">arg1</span><span class="sxs-lookup"><span data-stu-id="310c5-250">arg1</span></span> |<span data-ttu-id="310c5-251">是</span><span class="sxs-lookup"><span data-stu-id="310c5-251">Yes</span></span> |<span data-ttu-id="310c5-252">整數或字串</span><span class="sxs-lookup"><span data-stu-id="310c5-252">int or string</span></span> |<span data-ttu-id="310c5-253">hello hello 較少的第一個值或等號比較。</span><span class="sxs-lookup"><span data-stu-id="310c5-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="310c5-254">arg2</span><span class="sxs-lookup"><span data-stu-id="310c5-254">arg2</span></span> |<span data-ttu-id="310c5-255">是</span><span class="sxs-lookup"><span data-stu-id="310c5-255">Yes</span></span> |<span data-ttu-id="310c5-256">整數或字串</span><span class="sxs-lookup"><span data-stu-id="310c5-256">int or string</span></span> |<span data-ttu-id="310c5-257">hello hello 小於第二個值或等號比較。</span><span class="sxs-lookup"><span data-stu-id="310c5-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="310c5-258">傳回值</span><span class="sxs-lookup"><span data-stu-id="310c5-258">Return value</span></span>

<span data-ttu-id="310c5-259">傳回**True** hello 第一個值是否小於或等於 toohello 第二個值，否則**False**。</span><span class="sxs-lookup"><span data-stu-id="310c5-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="310c5-260">範例</span><span class="sxs-lookup"><span data-stu-id="310c5-260">Example</span></span>

<span data-ttu-id="310c5-261">hello 範例範本會檢查 hello 某個值是否小於或等於其他 toohello。</span><span class="sxs-lookup"><span data-stu-id="310c5-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="310c5-262">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="310c5-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="310c5-263">名稱</span><span class="sxs-lookup"><span data-stu-id="310c5-263">Name</span></span> | <span data-ttu-id="310c5-264">類型</span><span class="sxs-lookup"><span data-stu-id="310c5-264">Type</span></span> | <span data-ttu-id="310c5-265">值</span><span class="sxs-lookup"><span data-stu-id="310c5-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="310c5-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="310c5-266">checkInts</span></span> | <span data-ttu-id="310c5-267">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-267">Bool</span></span> | <span data-ttu-id="310c5-268">True</span><span class="sxs-lookup"><span data-stu-id="310c5-268">True</span></span> |
| <span data-ttu-id="310c5-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="310c5-269">checkStrings</span></span> | <span data-ttu-id="310c5-270">Bool</span><span class="sxs-lookup"><span data-stu-id="310c5-270">Bool</span></span> | <span data-ttu-id="310c5-271">False</span><span class="sxs-lookup"><span data-stu-id="310c5-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="310c5-272">後續步驟</span><span class="sxs-lookup"><span data-stu-id="310c5-272">Next steps</span></span>
* <span data-ttu-id="310c5-273">如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="310c5-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="310c5-274">toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="310c5-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="310c5-275">tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="310c5-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="310c5-276">toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="310c5-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

