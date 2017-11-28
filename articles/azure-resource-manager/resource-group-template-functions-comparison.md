---
title: "Azure Resource Manager 範本函式 - 比較 | Microsoft Docs"
description: "描述 Azure Resource Manager 範本中用來比較值的函式。"
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
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="f1548-103">Azure Resource Manager 範本的比較函式</span><span class="sxs-lookup"><span data-stu-id="f1548-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="f1548-104">Resource Manager 提供了幾個用來在範本中進行比較的函式。</span><span class="sxs-lookup"><span data-stu-id="f1548-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="f1548-105">equals</span><span class="sxs-lookup"><span data-stu-id="f1548-105">equals</span></span>](#equals)
* [<span data-ttu-id="f1548-106">greater</span><span class="sxs-lookup"><span data-stu-id="f1548-106">greater</span></span>](#greater)
* [<span data-ttu-id="f1548-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="f1548-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="f1548-108">less</span><span class="sxs-lookup"><span data-stu-id="f1548-108">less</span></span>](#less)
* [<span data-ttu-id="f1548-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="f1548-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="f1548-110">equals</span><span class="sxs-lookup"><span data-stu-id="f1548-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="f1548-111">檢查兩個值是否彼此相等。</span><span class="sxs-lookup"><span data-stu-id="f1548-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="f1548-112">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-112">Parameters</span></span>

| <span data-ttu-id="f1548-113">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-113">Parameter</span></span> | <span data-ttu-id="f1548-114">必要</span><span class="sxs-lookup"><span data-stu-id="f1548-114">Required</span></span> | <span data-ttu-id="f1548-115">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-115">Type</span></span> | <span data-ttu-id="f1548-116">說明</span><span class="sxs-lookup"><span data-stu-id="f1548-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f1548-117">arg1</span><span class="sxs-lookup"><span data-stu-id="f1548-117">arg1</span></span> |<span data-ttu-id="f1548-118">是</span><span class="sxs-lookup"><span data-stu-id="f1548-118">Yes</span></span> |<span data-ttu-id="f1548-119">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="f1548-119">int, string, array, or object</span></span> |<span data-ttu-id="f1548-120">要檢查是否相等的第一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="f1548-121">arg2</span><span class="sxs-lookup"><span data-stu-id="f1548-121">arg2</span></span> |<span data-ttu-id="f1548-122">是</span><span class="sxs-lookup"><span data-stu-id="f1548-122">Yes</span></span> |<span data-ttu-id="f1548-123">整數、字串、陣列或物件</span><span class="sxs-lookup"><span data-stu-id="f1548-123">int, string, array, or object</span></span> |<span data-ttu-id="f1548-124">要檢查是否相等的第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f1548-125">傳回值</span><span class="sxs-lookup"><span data-stu-id="f1548-125">Return value</span></span>

<span data-ttu-id="f1548-126">如果值相等則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="f1548-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="f1548-127">備註</span><span class="sxs-lookup"><span data-stu-id="f1548-127">Remarks</span></span>

<span data-ttu-id="f1548-128">equals 函式通常會搭配 `condition` 元素，用來測試是否已部署資源。</span><span class="sxs-lookup"><span data-stu-id="f1548-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="f1548-129">範例</span><span class="sxs-lookup"><span data-stu-id="f1548-129">Example</span></span>

<span data-ttu-id="f1548-130">範本範例會檢查不同類型的值是否相等。</span><span class="sxs-lookup"><span data-stu-id="f1548-130">The example template checks different types of values for equality.</span></span> <span data-ttu-id="f1548-131">所有預設值都會傳回 True。</span><span class="sxs-lookup"><span data-stu-id="f1548-131">All the default values return True.</span></span>

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

<span data-ttu-id="f1548-132">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f1548-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="f1548-133">名稱</span><span class="sxs-lookup"><span data-stu-id="f1548-133">Name</span></span> | <span data-ttu-id="f1548-134">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-134">Type</span></span> | <span data-ttu-id="f1548-135">值</span><span class="sxs-lookup"><span data-stu-id="f1548-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f1548-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="f1548-136">checkInts</span></span> | <span data-ttu-id="f1548-137">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-137">Bool</span></span> | <span data-ttu-id="f1548-138">True</span><span class="sxs-lookup"><span data-stu-id="f1548-138">True</span></span> |
| <span data-ttu-id="f1548-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="f1548-139">checkStrings</span></span> | <span data-ttu-id="f1548-140">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-140">Bool</span></span> | <span data-ttu-id="f1548-141">True</span><span class="sxs-lookup"><span data-stu-id="f1548-141">True</span></span> |
| <span data-ttu-id="f1548-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="f1548-142">checkArrays</span></span> | <span data-ttu-id="f1548-143">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-143">Bool</span></span> | <span data-ttu-id="f1548-144">True</span><span class="sxs-lookup"><span data-stu-id="f1548-144">True</span></span> |
| <span data-ttu-id="f1548-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="f1548-145">checkObjects</span></span> | <span data-ttu-id="f1548-146">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-146">Bool</span></span> | <span data-ttu-id="f1548-147">True</span><span class="sxs-lookup"><span data-stu-id="f1548-147">True</span></span> |


<span data-ttu-id="f1548-148">下列範例使用 [not](resource-group-template-functions-logical.md#not) 搭配 **equals**。</span><span class="sxs-lookup"><span data-stu-id="f1548-148">The following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="f1548-149">前述範例的輸出為：</span><span class="sxs-lookup"><span data-stu-id="f1548-149">The output from the preceding example is:</span></span>

| <span data-ttu-id="f1548-150">名稱</span><span class="sxs-lookup"><span data-stu-id="f1548-150">Name</span></span> | <span data-ttu-id="f1548-151">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-151">Type</span></span> | <span data-ttu-id="f1548-152">值</span><span class="sxs-lookup"><span data-stu-id="f1548-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f1548-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="f1548-153">checkNotEquals</span></span> | <span data-ttu-id="f1548-154">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-154">Bool</span></span> | <span data-ttu-id="f1548-155">True</span><span class="sxs-lookup"><span data-stu-id="f1548-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="f1548-156">greater</span><span class="sxs-lookup"><span data-stu-id="f1548-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="f1548-157">檢查第一個值是否大於第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-157">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="f1548-158">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-158">Parameters</span></span>

| <span data-ttu-id="f1548-159">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-159">Parameter</span></span> | <span data-ttu-id="f1548-160">必要</span><span class="sxs-lookup"><span data-stu-id="f1548-160">Required</span></span> | <span data-ttu-id="f1548-161">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-161">Type</span></span> | <span data-ttu-id="f1548-162">說明</span><span class="sxs-lookup"><span data-stu-id="f1548-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f1548-163">arg1</span><span class="sxs-lookup"><span data-stu-id="f1548-163">arg1</span></span> |<span data-ttu-id="f1548-164">是</span><span class="sxs-lookup"><span data-stu-id="f1548-164">Yes</span></span> |<span data-ttu-id="f1548-165">整數或字串</span><span class="sxs-lookup"><span data-stu-id="f1548-165">int or string</span></span> |<span data-ttu-id="f1548-166">用於大於比較的第一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-166">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="f1548-167">arg2</span><span class="sxs-lookup"><span data-stu-id="f1548-167">arg2</span></span> |<span data-ttu-id="f1548-168">是</span><span class="sxs-lookup"><span data-stu-id="f1548-168">Yes</span></span> |<span data-ttu-id="f1548-169">整數或字串</span><span class="sxs-lookup"><span data-stu-id="f1548-169">int or string</span></span> |<span data-ttu-id="f1548-170">用於大於比較的第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-170">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f1548-171">傳回值</span><span class="sxs-lookup"><span data-stu-id="f1548-171">Return value</span></span>

<span data-ttu-id="f1548-172">如果第一個值大於第二個值則傳回 **True**，否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="f1548-172">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="f1548-173">範例</span><span class="sxs-lookup"><span data-stu-id="f1548-173">Example</span></span>

<span data-ttu-id="f1548-174">範本範例會檢查某個值是否大於另一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-174">The example template checks whether the one value is greater than the other.</span></span>

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

<span data-ttu-id="f1548-175">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f1548-175">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="f1548-176">名稱</span><span class="sxs-lookup"><span data-stu-id="f1548-176">Name</span></span> | <span data-ttu-id="f1548-177">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-177">Type</span></span> | <span data-ttu-id="f1548-178">值</span><span class="sxs-lookup"><span data-stu-id="f1548-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f1548-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="f1548-179">checkInts</span></span> | <span data-ttu-id="f1548-180">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-180">Bool</span></span> | <span data-ttu-id="f1548-181">False</span><span class="sxs-lookup"><span data-stu-id="f1548-181">False</span></span> |
| <span data-ttu-id="f1548-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="f1548-182">checkStrings</span></span> | <span data-ttu-id="f1548-183">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-183">Bool</span></span> | <span data-ttu-id="f1548-184">True</span><span class="sxs-lookup"><span data-stu-id="f1548-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="f1548-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="f1548-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="f1548-186">檢查第一個值是否大於或等於第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-186">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="f1548-187">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-187">Parameters</span></span>

| <span data-ttu-id="f1548-188">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-188">Parameter</span></span> | <span data-ttu-id="f1548-189">必要</span><span class="sxs-lookup"><span data-stu-id="f1548-189">Required</span></span> | <span data-ttu-id="f1548-190">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-190">Type</span></span> | <span data-ttu-id="f1548-191">說明</span><span class="sxs-lookup"><span data-stu-id="f1548-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f1548-192">arg1</span><span class="sxs-lookup"><span data-stu-id="f1548-192">arg1</span></span> |<span data-ttu-id="f1548-193">是</span><span class="sxs-lookup"><span data-stu-id="f1548-193">Yes</span></span> |<span data-ttu-id="f1548-194">整數或字串</span><span class="sxs-lookup"><span data-stu-id="f1548-194">int or string</span></span> |<span data-ttu-id="f1548-195">用於大於或等於比較的第一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-195">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="f1548-196">arg2</span><span class="sxs-lookup"><span data-stu-id="f1548-196">arg2</span></span> |<span data-ttu-id="f1548-197">是</span><span class="sxs-lookup"><span data-stu-id="f1548-197">Yes</span></span> |<span data-ttu-id="f1548-198">整數或字串</span><span class="sxs-lookup"><span data-stu-id="f1548-198">int or string</span></span> |<span data-ttu-id="f1548-199">用於大於或等於比較的第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-199">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f1548-200">傳回值</span><span class="sxs-lookup"><span data-stu-id="f1548-200">Return value</span></span>

<span data-ttu-id="f1548-201">如果第一個值大於或等於第二個值則傳回 **True**，否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="f1548-201">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="f1548-202">範例</span><span class="sxs-lookup"><span data-stu-id="f1548-202">Example</span></span>

<span data-ttu-id="f1548-203">範本範例會檢查某個值是否大於或等於另一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-203">The example template checks whether the one value is greater than or equal to the other.</span></span>

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

<span data-ttu-id="f1548-204">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f1548-204">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="f1548-205">名稱</span><span class="sxs-lookup"><span data-stu-id="f1548-205">Name</span></span> | <span data-ttu-id="f1548-206">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-206">Type</span></span> | <span data-ttu-id="f1548-207">值</span><span class="sxs-lookup"><span data-stu-id="f1548-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f1548-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="f1548-208">checkInts</span></span> | <span data-ttu-id="f1548-209">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-209">Bool</span></span> | <span data-ttu-id="f1548-210">False</span><span class="sxs-lookup"><span data-stu-id="f1548-210">False</span></span> |
| <span data-ttu-id="f1548-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="f1548-211">checkStrings</span></span> | <span data-ttu-id="f1548-212">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-212">Bool</span></span> | <span data-ttu-id="f1548-213">True</span><span class="sxs-lookup"><span data-stu-id="f1548-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="f1548-214">less</span><span class="sxs-lookup"><span data-stu-id="f1548-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="f1548-215">檢查第一個值是否小於第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-215">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="f1548-216">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-216">Parameters</span></span>

| <span data-ttu-id="f1548-217">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-217">Parameter</span></span> | <span data-ttu-id="f1548-218">必要</span><span class="sxs-lookup"><span data-stu-id="f1548-218">Required</span></span> | <span data-ttu-id="f1548-219">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-219">Type</span></span> | <span data-ttu-id="f1548-220">說明</span><span class="sxs-lookup"><span data-stu-id="f1548-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f1548-221">arg1</span><span class="sxs-lookup"><span data-stu-id="f1548-221">arg1</span></span> |<span data-ttu-id="f1548-222">是</span><span class="sxs-lookup"><span data-stu-id="f1548-222">Yes</span></span> |<span data-ttu-id="f1548-223">整數或字串</span><span class="sxs-lookup"><span data-stu-id="f1548-223">int or string</span></span> |<span data-ttu-id="f1548-224">用於小於比較的第一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-224">The first value for the less comparison.</span></span> |
| <span data-ttu-id="f1548-225">arg2</span><span class="sxs-lookup"><span data-stu-id="f1548-225">arg2</span></span> |<span data-ttu-id="f1548-226">是</span><span class="sxs-lookup"><span data-stu-id="f1548-226">Yes</span></span> |<span data-ttu-id="f1548-227">整數或字串</span><span class="sxs-lookup"><span data-stu-id="f1548-227">int or string</span></span> |<span data-ttu-id="f1548-228">用於小於比較的第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-228">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f1548-229">傳回值</span><span class="sxs-lookup"><span data-stu-id="f1548-229">Return value</span></span>

<span data-ttu-id="f1548-230">如果第一個值小於第二個值則傳回 **True**，否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="f1548-230">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="f1548-231">範例</span><span class="sxs-lookup"><span data-stu-id="f1548-231">Example</span></span>

<span data-ttu-id="f1548-232">範本範例會檢查某個值是否小於另一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-232">The example template checks whether the one value is less than the other.</span></span>

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

<span data-ttu-id="f1548-233">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f1548-233">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="f1548-234">名稱</span><span class="sxs-lookup"><span data-stu-id="f1548-234">Name</span></span> | <span data-ttu-id="f1548-235">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-235">Type</span></span> | <span data-ttu-id="f1548-236">值</span><span class="sxs-lookup"><span data-stu-id="f1548-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f1548-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="f1548-237">checkInts</span></span> | <span data-ttu-id="f1548-238">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-238">Bool</span></span> | <span data-ttu-id="f1548-239">True</span><span class="sxs-lookup"><span data-stu-id="f1548-239">True</span></span> |
| <span data-ttu-id="f1548-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="f1548-240">checkStrings</span></span> | <span data-ttu-id="f1548-241">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-241">Bool</span></span> | <span data-ttu-id="f1548-242">False</span><span class="sxs-lookup"><span data-stu-id="f1548-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="f1548-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="f1548-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="f1548-244">檢查第一個值是否小於或等於第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-244">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="f1548-245">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-245">Parameters</span></span>

| <span data-ttu-id="f1548-246">參數</span><span class="sxs-lookup"><span data-stu-id="f1548-246">Parameter</span></span> | <span data-ttu-id="f1548-247">必要</span><span class="sxs-lookup"><span data-stu-id="f1548-247">Required</span></span> | <span data-ttu-id="f1548-248">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-248">Type</span></span> | <span data-ttu-id="f1548-249">說明</span><span class="sxs-lookup"><span data-stu-id="f1548-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f1548-250">arg1</span><span class="sxs-lookup"><span data-stu-id="f1548-250">arg1</span></span> |<span data-ttu-id="f1548-251">是</span><span class="sxs-lookup"><span data-stu-id="f1548-251">Yes</span></span> |<span data-ttu-id="f1548-252">整數或字串</span><span class="sxs-lookup"><span data-stu-id="f1548-252">int or string</span></span> |<span data-ttu-id="f1548-253">用於小於或等於比較的第一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-253">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="f1548-254">arg2</span><span class="sxs-lookup"><span data-stu-id="f1548-254">arg2</span></span> |<span data-ttu-id="f1548-255">是</span><span class="sxs-lookup"><span data-stu-id="f1548-255">Yes</span></span> |<span data-ttu-id="f1548-256">整數或字串</span><span class="sxs-lookup"><span data-stu-id="f1548-256">int or string</span></span> |<span data-ttu-id="f1548-257">用於小於或等於比較的第二個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-257">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="f1548-258">傳回值</span><span class="sxs-lookup"><span data-stu-id="f1548-258">Return value</span></span>

<span data-ttu-id="f1548-259">如果第一個值小於或等於第二個值則傳回 **True**，否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="f1548-259">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="f1548-260">範例</span><span class="sxs-lookup"><span data-stu-id="f1548-260">Example</span></span>

<span data-ttu-id="f1548-261">範本範例會檢查某個值是否小於或等於另一個值。</span><span class="sxs-lookup"><span data-stu-id="f1548-261">The example template checks whether the one value is less than or equal to the other.</span></span>

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

<span data-ttu-id="f1548-262">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f1548-262">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="f1548-263">名稱</span><span class="sxs-lookup"><span data-stu-id="f1548-263">Name</span></span> | <span data-ttu-id="f1548-264">類型</span><span class="sxs-lookup"><span data-stu-id="f1548-264">Type</span></span> | <span data-ttu-id="f1548-265">值</span><span class="sxs-lookup"><span data-stu-id="f1548-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="f1548-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="f1548-266">checkInts</span></span> | <span data-ttu-id="f1548-267">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-267">Bool</span></span> | <span data-ttu-id="f1548-268">True</span><span class="sxs-lookup"><span data-stu-id="f1548-268">True</span></span> |
| <span data-ttu-id="f1548-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="f1548-269">checkStrings</span></span> | <span data-ttu-id="f1548-270">Bool</span><span class="sxs-lookup"><span data-stu-id="f1548-270">Bool</span></span> | <span data-ttu-id="f1548-271">False</span><span class="sxs-lookup"><span data-stu-id="f1548-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="f1548-272">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1548-272">Next steps</span></span>
* <span data-ttu-id="f1548-273">如需有關 Azure Resource Manager 範本中各區段的說明，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="f1548-273">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f1548-274">若要合併多個範本，請參閱[透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="f1548-274">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="f1548-275">若要依指定的次數重複建立資源類型，請參閱 [在 Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="f1548-275">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="f1548-276">若要了解如何部署已建立的範本，請參閱[使用 Azure Resource Manager 範本部署應用程式](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="f1548-276">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

