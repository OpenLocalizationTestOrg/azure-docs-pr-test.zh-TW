---
title: "資源管理員範本函式 aaaAzure-字串 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 toowork，字串中的 hello 函式 toouse。"
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="b508a-103">Azure Resource Manager 範本的字串函式</span><span class="sxs-lookup"><span data-stu-id="b508a-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="b508a-104">資源管理員提供下列函數使用字串 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="b508a-105">base64</span><span class="sxs-lookup"><span data-stu-id="b508a-105">base64</span></span>](#base64)
* [<span data-ttu-id="b508a-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="b508a-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="b508a-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="b508a-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="b508a-108">concat</span><span class="sxs-lookup"><span data-stu-id="b508a-108">concat</span></span>](#concat)
* [<span data-ttu-id="b508a-109">contains</span><span class="sxs-lookup"><span data-stu-id="b508a-109">contains</span></span>](#contains)
* [<span data-ttu-id="b508a-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="b508a-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="b508a-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="b508a-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="b508a-112">empty</span><span class="sxs-lookup"><span data-stu-id="b508a-112">empty</span></span>](#empty)
* [<span data-ttu-id="b508a-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="b508a-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="b508a-114">first</span><span class="sxs-lookup"><span data-stu-id="b508a-114">first</span></span>](#first)
* [<span data-ttu-id="b508a-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="b508a-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="b508a-116">last</span><span class="sxs-lookup"><span data-stu-id="b508a-116">last</span></span>](#last)
* [<span data-ttu-id="b508a-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="b508a-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="b508a-118">length</span><span class="sxs-lookup"><span data-stu-id="b508a-118">length</span></span>](#length)
* [<span data-ttu-id="b508a-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="b508a-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="b508a-120">replace</span><span class="sxs-lookup"><span data-stu-id="b508a-120">replace</span></span>](#replace)
* [<span data-ttu-id="b508a-121">skip</span><span class="sxs-lookup"><span data-stu-id="b508a-121">skip</span></span>](#skip)
* [<span data-ttu-id="b508a-122">分割</span><span class="sxs-lookup"><span data-stu-id="b508a-122">split</span></span>](#split)
* [<span data-ttu-id="b508a-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="b508a-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="b508a-124">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-124">string</span></span>](#string)
* [<span data-ttu-id="b508a-125">substring</span><span class="sxs-lookup"><span data-stu-id="b508a-125">substring</span></span>](#substring)
* [<span data-ttu-id="b508a-126">take</span><span class="sxs-lookup"><span data-stu-id="b508a-126">take</span></span>](#take)
* [<span data-ttu-id="b508a-127">toLower</span><span class="sxs-lookup"><span data-stu-id="b508a-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="b508a-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="b508a-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="b508a-129">修剪</span><span class="sxs-lookup"><span data-stu-id="b508a-129">trim</span></span>](#trim)
* [<span data-ttu-id="b508a-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="b508a-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="b508a-131">uri</span><span class="sxs-lookup"><span data-stu-id="b508a-131">uri</span></span>](#uri)
* [<span data-ttu-id="b508a-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="b508a-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="b508a-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="b508a-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="b508a-134">base64</span><span class="sxs-lookup"><span data-stu-id="b508a-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="b508a-135">傳回 hello hello 輸入字串的 base64 表示法。</span><span class="sxs-lookup"><span data-stu-id="b508a-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-136">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-136">Parameters</span></span>

| <span data-ttu-id="b508a-137">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-137">Parameter</span></span> | <span data-ttu-id="b508a-138">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-138">Required</span></span> | <span data-ttu-id="b508a-139">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-139">Type</span></span> | <span data-ttu-id="b508a-140">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-141">inputString</span><span class="sxs-lookup"><span data-stu-id="b508a-141">inputString</span></span> |<span data-ttu-id="b508a-142">是</span><span class="sxs-lookup"><span data-stu-id="b508a-142">Yes</span></span> |<span data-ttu-id="b508a-143">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-143">string</span></span> |<span data-ttu-id="b508a-144">hello 值 tooreturn 為 base64 表示法。</span><span class="sxs-lookup"><span data-stu-id="b508a-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-145">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-145">Return value</span></span>

<span data-ttu-id="b508a-146">字串，包含 hello base64 表示法。</span><span class="sxs-lookup"><span data-stu-id="b508a-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-147">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-147">Examples</span></span>

<span data-ttu-id="b508a-148">hello 下列範例顯示如何 toouse hello base64 函式。</span><span class="sxs-lookup"><span data-stu-id="b508a-148">hello following example shows how toouse hello base64 function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="b508a-149">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-150">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-150">Name</span></span> | <span data-ttu-id="b508a-151">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-151">Type</span></span> | <span data-ttu-id="b508a-152">值</span><span class="sxs-lookup"><span data-stu-id="b508a-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="b508a-153">base64Output</span></span> | <span data-ttu-id="b508a-154">String</span><span class="sxs-lookup"><span data-stu-id="b508a-154">String</span></span> | <span data-ttu-id="b508a-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="b508a-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="b508a-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-156">toStringOutput</span></span> | <span data-ttu-id="b508a-157">String</span><span class="sxs-lookup"><span data-stu-id="b508a-157">String</span></span> | <span data-ttu-id="b508a-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="b508a-158">one, two, three</span></span> |
| <span data-ttu-id="b508a-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-159">toJsonOutput</span></span> | <span data-ttu-id="b508a-160">Object</span><span class="sxs-lookup"><span data-stu-id="b508a-160">Object</span></span> | <span data-ttu-id="b508a-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="b508a-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="b508a-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="b508a-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="b508a-163">將轉換的 base64 表示法 tooa JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="b508a-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-164">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-164">Parameters</span></span>

| <span data-ttu-id="b508a-165">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-165">Parameter</span></span> | <span data-ttu-id="b508a-166">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-166">Required</span></span> | <span data-ttu-id="b508a-167">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-167">Type</span></span> | <span data-ttu-id="b508a-168">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="b508a-169">base64Value</span></span> |<span data-ttu-id="b508a-170">是</span><span class="sxs-lookup"><span data-stu-id="b508a-170">Yes</span></span> |<span data-ttu-id="b508a-171">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-171">string</span></span> |<span data-ttu-id="b508a-172">hello base64 表示法 tooconvert tooa JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="b508a-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-173">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-173">Return value</span></span>

<span data-ttu-id="b508a-174">JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="b508a-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-175">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-175">Examples</span></span>

<span data-ttu-id="b508a-176">hello 下列範例會使用 hello base64ToJson 函式 tooconvert base64 值：</span><span class="sxs-lookup"><span data-stu-id="b508a-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="b508a-177">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-178">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-178">Name</span></span> | <span data-ttu-id="b508a-179">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-179">Type</span></span> | <span data-ttu-id="b508a-180">值</span><span class="sxs-lookup"><span data-stu-id="b508a-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="b508a-181">base64Output</span></span> | <span data-ttu-id="b508a-182">String</span><span class="sxs-lookup"><span data-stu-id="b508a-182">String</span></span> | <span data-ttu-id="b508a-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="b508a-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="b508a-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-184">toStringOutput</span></span> | <span data-ttu-id="b508a-185">String</span><span class="sxs-lookup"><span data-stu-id="b508a-185">String</span></span> | <span data-ttu-id="b508a-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="b508a-186">one, two, three</span></span> |
| <span data-ttu-id="b508a-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-187">toJsonOutput</span></span> | <span data-ttu-id="b508a-188">Object</span><span class="sxs-lookup"><span data-stu-id="b508a-188">Object</span></span> | <span data-ttu-id="b508a-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="b508a-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="b508a-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="b508a-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="b508a-191">將 base64 表示法 tooa 字串轉換。</span><span class="sxs-lookup"><span data-stu-id="b508a-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-192">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-192">Parameters</span></span>

| <span data-ttu-id="b508a-193">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-193">Parameter</span></span> | <span data-ttu-id="b508a-194">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-194">Required</span></span> | <span data-ttu-id="b508a-195">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-195">Type</span></span> | <span data-ttu-id="b508a-196">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="b508a-197">base64Value</span></span> |<span data-ttu-id="b508a-198">是</span><span class="sxs-lookup"><span data-stu-id="b508a-198">Yes</span></span> |<span data-ttu-id="b508a-199">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-199">string</span></span> |<span data-ttu-id="b508a-200">hello base64 表示法 tooconvert tooa 字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-201">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-201">Return value</span></span>

<span data-ttu-id="b508a-202">已轉換字串 hello 的 base64 值。</span><span class="sxs-lookup"><span data-stu-id="b508a-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-203">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-203">Examples</span></span>

<span data-ttu-id="b508a-204">hello 下列範例會使用 hello base64ToString 函式 tooconvert base64 值：</span><span class="sxs-lookup"><span data-stu-id="b508a-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="b508a-205">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-206">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-206">Name</span></span> | <span data-ttu-id="b508a-207">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-207">Type</span></span> | <span data-ttu-id="b508a-208">值</span><span class="sxs-lookup"><span data-stu-id="b508a-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="b508a-209">base64Output</span></span> | <span data-ttu-id="b508a-210">String</span><span class="sxs-lookup"><span data-stu-id="b508a-210">String</span></span> | <span data-ttu-id="b508a-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="b508a-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="b508a-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-212">toStringOutput</span></span> | <span data-ttu-id="b508a-213">String</span><span class="sxs-lookup"><span data-stu-id="b508a-213">String</span></span> | <span data-ttu-id="b508a-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="b508a-214">one, two, three</span></span> |
| <span data-ttu-id="b508a-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-215">toJsonOutput</span></span> | <span data-ttu-id="b508a-216">Object</span><span class="sxs-lookup"><span data-stu-id="b508a-216">Object</span></span> | <span data-ttu-id="b508a-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="b508a-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="b508a-218">concat</span><span class="sxs-lookup"><span data-stu-id="b508a-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="b508a-219">結合多個字串值和傳回 hello 串連字串，或結合多個陣列並傳回串連的 hello 陣列。</span><span class="sxs-lookup"><span data-stu-id="b508a-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-220">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-220">Parameters</span></span>

| <span data-ttu-id="b508a-221">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-221">Parameter</span></span> | <span data-ttu-id="b508a-222">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-222">Required</span></span> | <span data-ttu-id="b508a-223">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-223">Type</span></span> | <span data-ttu-id="b508a-224">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-225">arg1</span><span class="sxs-lookup"><span data-stu-id="b508a-225">arg1</span></span> |<span data-ttu-id="b508a-226">是</span><span class="sxs-lookup"><span data-stu-id="b508a-226">Yes</span></span> |<span data-ttu-id="b508a-227">字串或陣列</span><span class="sxs-lookup"><span data-stu-id="b508a-227">string or array</span></span> |<span data-ttu-id="b508a-228">hello 串連的第一個值。</span><span class="sxs-lookup"><span data-stu-id="b508a-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="b508a-229">其他引數</span><span class="sxs-lookup"><span data-stu-id="b508a-229">additional arguments</span></span> |<span data-ttu-id="b508a-230">否</span><span class="sxs-lookup"><span data-stu-id="b508a-230">No</span></span> |<span data-ttu-id="b508a-231">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-231">string</span></span> |<span data-ttu-id="b508a-232">串連的其他值 (循序順序)。</span><span class="sxs-lookup"><span data-stu-id="b508a-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-233">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-233">Return value</span></span>
<span data-ttu-id="b508a-234">串連值的字串或陣列。</span><span class="sxs-lookup"><span data-stu-id="b508a-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-235">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-235">Examples</span></span>

<span data-ttu-id="b508a-236">hello 下列範例將說明如何 toocombine 兩個字串值，並傳回串連的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="b508a-237">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-238">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-238">Name</span></span> | <span data-ttu-id="b508a-239">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-239">Type</span></span> | <span data-ttu-id="b508a-240">值</span><span class="sxs-lookup"><span data-stu-id="b508a-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-241">concatOutput</span></span> | <span data-ttu-id="b508a-242">String</span><span class="sxs-lookup"><span data-stu-id="b508a-242">String</span></span> | <span data-ttu-id="b508a-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="b508a-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="b508a-244">hello 下列範例顯示兩個 toocombine 的陣列。</span><span class="sxs-lookup"><span data-stu-id="b508a-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="b508a-245">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-246">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-246">Name</span></span> | <span data-ttu-id="b508a-247">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-247">Type</span></span> | <span data-ttu-id="b508a-248">值</span><span class="sxs-lookup"><span data-stu-id="b508a-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-249">return</span><span class="sxs-lookup"><span data-stu-id="b508a-249">return</span></span> | <span data-ttu-id="b508a-250">陣列</span><span class="sxs-lookup"><span data-stu-id="b508a-250">Array</span></span> | <span data-ttu-id="b508a-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="b508a-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="b508a-252">contains</span><span class="sxs-lookup"><span data-stu-id="b508a-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="b508a-253">檢查陣列中是否包含值、物件中是否包含索引鍵，或字串中是否包含子字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-254">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-254">Parameters</span></span>

| <span data-ttu-id="b508a-255">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-255">Parameter</span></span> | <span data-ttu-id="b508a-256">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-256">Required</span></span> | <span data-ttu-id="b508a-257">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-257">Type</span></span> | <span data-ttu-id="b508a-258">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-259">container</span><span class="sxs-lookup"><span data-stu-id="b508a-259">container</span></span> |<span data-ttu-id="b508a-260">是</span><span class="sxs-lookup"><span data-stu-id="b508a-260">Yes</span></span> |<span data-ttu-id="b508a-261">陣列、物件或字串</span><span class="sxs-lookup"><span data-stu-id="b508a-261">array, object, or string</span></span> |<span data-ttu-id="b508a-262">包含 hello 值 toofind hello 值。</span><span class="sxs-lookup"><span data-stu-id="b508a-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="b508a-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="b508a-263">itemToFind</span></span> |<span data-ttu-id="b508a-264">是</span><span class="sxs-lookup"><span data-stu-id="b508a-264">Yes</span></span> |<span data-ttu-id="b508a-265">字串或整數</span><span class="sxs-lookup"><span data-stu-id="b508a-265">string or int</span></span> |<span data-ttu-id="b508a-266">hello 值 toofind。</span><span class="sxs-lookup"><span data-stu-id="b508a-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-267">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-267">Return value</span></span>

<span data-ttu-id="b508a-268">**True** hello 項目是否找到則為**False**。</span><span class="sxs-lookup"><span data-stu-id="b508a-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-269">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-269">Examples</span></span>

<span data-ttu-id="b508a-270">hello 下列範例顯示如何 toouse 包含與不同類型：</span><span class="sxs-lookup"><span data-stu-id="b508a-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="b508a-271">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-272">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-272">Name</span></span> | <span data-ttu-id="b508a-273">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-273">Type</span></span> | <span data-ttu-id="b508a-274">值</span><span class="sxs-lookup"><span data-stu-id="b508a-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-275">stringTrue</span></span> | <span data-ttu-id="b508a-276">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-276">Bool</span></span> | <span data-ttu-id="b508a-277">True</span><span class="sxs-lookup"><span data-stu-id="b508a-277">True</span></span> |
| <span data-ttu-id="b508a-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="b508a-278">stringFalse</span></span> | <span data-ttu-id="b508a-279">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-279">Bool</span></span> | <span data-ttu-id="b508a-280">False</span><span class="sxs-lookup"><span data-stu-id="b508a-280">False</span></span> |
| <span data-ttu-id="b508a-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-281">objectTrue</span></span> | <span data-ttu-id="b508a-282">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-282">Bool</span></span> | <span data-ttu-id="b508a-283">True</span><span class="sxs-lookup"><span data-stu-id="b508a-283">True</span></span> |
| <span data-ttu-id="b508a-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="b508a-284">objectFalse</span></span> | <span data-ttu-id="b508a-285">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-285">Bool</span></span> | <span data-ttu-id="b508a-286">False</span><span class="sxs-lookup"><span data-stu-id="b508a-286">False</span></span> |
| <span data-ttu-id="b508a-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-287">arrayTrue</span></span> | <span data-ttu-id="b508a-288">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-288">Bool</span></span> | <span data-ttu-id="b508a-289">True</span><span class="sxs-lookup"><span data-stu-id="b508a-289">True</span></span> |
| <span data-ttu-id="b508a-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="b508a-290">arrayFalse</span></span> | <span data-ttu-id="b508a-291">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-291">Bool</span></span> | <span data-ttu-id="b508a-292">False</span><span class="sxs-lookup"><span data-stu-id="b508a-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="b508a-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="b508a-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="b508a-294">將轉換值 tooa 資料 URI。</span><span class="sxs-lookup"><span data-stu-id="b508a-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-295">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-295">Parameters</span></span>

| <span data-ttu-id="b508a-296">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-296">Parameter</span></span> | <span data-ttu-id="b508a-297">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-297">Required</span></span> | <span data-ttu-id="b508a-298">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-298">Type</span></span> | <span data-ttu-id="b508a-299">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="b508a-300">stringToConvert</span></span> |<span data-ttu-id="b508a-301">是</span><span class="sxs-lookup"><span data-stu-id="b508a-301">Yes</span></span> |<span data-ttu-id="b508a-302">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-302">string</span></span> |<span data-ttu-id="b508a-303">hello 值 tooconvert tooa 資料 URI。</span><span class="sxs-lookup"><span data-stu-id="b508a-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-304">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-304">Return value</span></span>

<span data-ttu-id="b508a-305">格式化為資料 URI 的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-306">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-306">Examples</span></span>

<span data-ttu-id="b508a-307">下列範例中的 hello 值 tooa 資料 URI 轉換，並且將 URI tooa 字串資料轉換：</span><span class="sxs-lookup"><span data-stu-id="b508a-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="b508a-308">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-309">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-309">Name</span></span> | <span data-ttu-id="b508a-310">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-310">Type</span></span> | <span data-ttu-id="b508a-311">值</span><span class="sxs-lookup"><span data-stu-id="b508a-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-312">dataUriOutput</span></span> | <span data-ttu-id="b508a-313">String</span><span class="sxs-lookup"><span data-stu-id="b508a-313">String</span></span> | <span data-ttu-id="b508a-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="b508a-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="b508a-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-315">toStringOutput</span></span> | <span data-ttu-id="b508a-316">String</span><span class="sxs-lookup"><span data-stu-id="b508a-316">String</span></span> | <span data-ttu-id="b508a-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="b508a-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="b508a-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="b508a-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="b508a-319">轉換資料的 URI 格式化值 tooa 字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-320">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-320">Parameters</span></span>

| <span data-ttu-id="b508a-321">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-321">Parameter</span></span> | <span data-ttu-id="b508a-322">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-322">Required</span></span> | <span data-ttu-id="b508a-323">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-323">Type</span></span> | <span data-ttu-id="b508a-324">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="b508a-325">dataUriToConvert</span></span> |<span data-ttu-id="b508a-326">是</span><span class="sxs-lookup"><span data-stu-id="b508a-326">Yes</span></span> |<span data-ttu-id="b508a-327">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-327">string</span></span> |<span data-ttu-id="b508a-328">hello 資料 URI 值 tooconvert。</span><span class="sxs-lookup"><span data-stu-id="b508a-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-329">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-329">Return value</span></span>

<span data-ttu-id="b508a-330">字串，包含 hello 轉換值。</span><span class="sxs-lookup"><span data-stu-id="b508a-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-331">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-331">Examples</span></span>

<span data-ttu-id="b508a-332">下列範例中的 hello 值 tooa 資料 URI 轉換，並且將 URI tooa 字串資料轉換：</span><span class="sxs-lookup"><span data-stu-id="b508a-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="b508a-333">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-334">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-334">Name</span></span> | <span data-ttu-id="b508a-335">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-335">Type</span></span> | <span data-ttu-id="b508a-336">值</span><span class="sxs-lookup"><span data-stu-id="b508a-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-337">dataUriOutput</span></span> | <span data-ttu-id="b508a-338">String</span><span class="sxs-lookup"><span data-stu-id="b508a-338">String</span></span> | <span data-ttu-id="b508a-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="b508a-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="b508a-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-340">toStringOutput</span></span> | <span data-ttu-id="b508a-341">String</span><span class="sxs-lookup"><span data-stu-id="b508a-341">String</span></span> | <span data-ttu-id="b508a-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="b508a-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="b508a-343">empty</span><span class="sxs-lookup"><span data-stu-id="b508a-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="b508a-344">判斷陣列、物件或字串是否空白。</span><span class="sxs-lookup"><span data-stu-id="b508a-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-345">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-345">Parameters</span></span>

| <span data-ttu-id="b508a-346">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-346">Parameter</span></span> | <span data-ttu-id="b508a-347">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-347">Required</span></span> | <span data-ttu-id="b508a-348">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-348">Type</span></span> | <span data-ttu-id="b508a-349">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="b508a-350">itemToTest</span></span> |<span data-ttu-id="b508a-351">是</span><span class="sxs-lookup"><span data-stu-id="b508a-351">Yes</span></span> |<span data-ttu-id="b508a-352">陣列、物件或字串</span><span class="sxs-lookup"><span data-stu-id="b508a-352">array, object, or string</span></span> |<span data-ttu-id="b508a-353">hello 值 toocheck，如果是空白。</span><span class="sxs-lookup"><span data-stu-id="b508a-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-354">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-354">Return value</span></span>

<span data-ttu-id="b508a-355">傳回**True** hello 值是空的否則如果**False**。</span><span class="sxs-lookup"><span data-stu-id="b508a-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-356">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-356">Examples</span></span>

<span data-ttu-id="b508a-357">下列範例會檢查是否是空的陣列、 物件和字串 hello。</span><span class="sxs-lookup"><span data-stu-id="b508a-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="b508a-358">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-359">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-359">Name</span></span> | <span data-ttu-id="b508a-360">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-360">Type</span></span> | <span data-ttu-id="b508a-361">值</span><span class="sxs-lookup"><span data-stu-id="b508a-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="b508a-362">arrayEmpty</span></span> | <span data-ttu-id="b508a-363">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-363">Bool</span></span> | <span data-ttu-id="b508a-364">True</span><span class="sxs-lookup"><span data-stu-id="b508a-364">True</span></span> |
| <span data-ttu-id="b508a-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="b508a-365">objectEmpty</span></span> | <span data-ttu-id="b508a-366">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-366">Bool</span></span> | <span data-ttu-id="b508a-367">True</span><span class="sxs-lookup"><span data-stu-id="b508a-367">True</span></span> |
| <span data-ttu-id="b508a-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="b508a-368">stringEmpty</span></span> | <span data-ttu-id="b508a-369">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-369">Bool</span></span> | <span data-ttu-id="b508a-370">True</span><span class="sxs-lookup"><span data-stu-id="b508a-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="b508a-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="b508a-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="b508a-372">判斷字串結尾是否為值。</span><span class="sxs-lookup"><span data-stu-id="b508a-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="b508a-373">hello 比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="b508a-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-374">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-374">Parameters</span></span>

| <span data-ttu-id="b508a-375">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-375">Parameter</span></span> | <span data-ttu-id="b508a-376">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-376">Required</span></span> | <span data-ttu-id="b508a-377">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-377">Type</span></span> | <span data-ttu-id="b508a-378">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="b508a-379">stringToSearch</span></span> |<span data-ttu-id="b508a-380">是</span><span class="sxs-lookup"><span data-stu-id="b508a-380">Yes</span></span> |<span data-ttu-id="b508a-381">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-381">string</span></span> |<span data-ttu-id="b508a-382">包含 hello 項目 toofind hello 值。</span><span class="sxs-lookup"><span data-stu-id="b508a-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="b508a-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="b508a-383">stringToFind</span></span> |<span data-ttu-id="b508a-384">是</span><span class="sxs-lookup"><span data-stu-id="b508a-384">Yes</span></span> |<span data-ttu-id="b508a-385">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-385">string</span></span> |<span data-ttu-id="b508a-386">hello 值 toofind。</span><span class="sxs-lookup"><span data-stu-id="b508a-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-387">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-387">Return value</span></span>

<span data-ttu-id="b508a-388">**True** hello 最後一個字元或字元字串 hello 符合 hello 值; 否則**False**。</span><span class="sxs-lookup"><span data-stu-id="b508a-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-389">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-389">Examples</span></span>

<span data-ttu-id="b508a-390">hello 下列範例顯示如何 toouse hello startsWith 和 endsWith 函式：</span><span class="sxs-lookup"><span data-stu-id="b508a-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="b508a-391">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-392">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-392">Name</span></span> | <span data-ttu-id="b508a-393">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-393">Type</span></span> | <span data-ttu-id="b508a-394">值</span><span class="sxs-lookup"><span data-stu-id="b508a-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-395">startsTrue</span></span> | <span data-ttu-id="b508a-396">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-396">Bool</span></span> | <span data-ttu-id="b508a-397">True</span><span class="sxs-lookup"><span data-stu-id="b508a-397">True</span></span> |
| <span data-ttu-id="b508a-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-398">startsCapTrue</span></span> | <span data-ttu-id="b508a-399">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-399">Bool</span></span> | <span data-ttu-id="b508a-400">True</span><span class="sxs-lookup"><span data-stu-id="b508a-400">True</span></span> |
| <span data-ttu-id="b508a-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="b508a-401">startsFalse</span></span> | <span data-ttu-id="b508a-402">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-402">Bool</span></span> | <span data-ttu-id="b508a-403">False</span><span class="sxs-lookup"><span data-stu-id="b508a-403">False</span></span> |
| <span data-ttu-id="b508a-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-404">endsTrue</span></span> | <span data-ttu-id="b508a-405">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-405">Bool</span></span> | <span data-ttu-id="b508a-406">True</span><span class="sxs-lookup"><span data-stu-id="b508a-406">True</span></span> |
| <span data-ttu-id="b508a-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-407">endsCapTrue</span></span> | <span data-ttu-id="b508a-408">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-408">Bool</span></span> | <span data-ttu-id="b508a-409">True</span><span class="sxs-lookup"><span data-stu-id="b508a-409">True</span></span> |
| <span data-ttu-id="b508a-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="b508a-410">endsFalse</span></span> | <span data-ttu-id="b508a-411">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-411">Bool</span></span> | <span data-ttu-id="b508a-412">False</span><span class="sxs-lookup"><span data-stu-id="b508a-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="b508a-413">first</span><span class="sxs-lookup"><span data-stu-id="b508a-413">first</span></span>
`first(arg1)`

<span data-ttu-id="b508a-414">傳回 hello hello 字串的第一個字元或 hello 陣列的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="b508a-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-415">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-415">Parameters</span></span>

| <span data-ttu-id="b508a-416">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-416">Parameter</span></span> | <span data-ttu-id="b508a-417">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-417">Required</span></span> | <span data-ttu-id="b508a-418">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-418">Type</span></span> | <span data-ttu-id="b508a-419">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-420">arg1</span><span class="sxs-lookup"><span data-stu-id="b508a-420">arg1</span></span> |<span data-ttu-id="b508a-421">是</span><span class="sxs-lookup"><span data-stu-id="b508a-421">Yes</span></span> |<span data-ttu-id="b508a-422">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="b508a-422">array or string</span></span> |<span data-ttu-id="b508a-423">hello 值 tooretrieve hello 第一個項目或字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-424">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-424">Return value</span></span>

<span data-ttu-id="b508a-425">字串 hello 第一個字元或 hello 型別 （字串、 int、 陣列或物件） 的 hello 陣列中的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="b508a-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-426">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-426">Examples</span></span>

<span data-ttu-id="b508a-427">hello 下列範例顯示如何 toouse hello 與陣列和字串的第一個函式。</span><span class="sxs-lookup"><span data-stu-id="b508a-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="b508a-428">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-429">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-429">Name</span></span> | <span data-ttu-id="b508a-430">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-430">Type</span></span> | <span data-ttu-id="b508a-431">值</span><span class="sxs-lookup"><span data-stu-id="b508a-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-432">arrayOutput</span></span> | <span data-ttu-id="b508a-433">String</span><span class="sxs-lookup"><span data-stu-id="b508a-433">String</span></span> | <span data-ttu-id="b508a-434">one</span><span class="sxs-lookup"><span data-stu-id="b508a-434">one</span></span> |
| <span data-ttu-id="b508a-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-435">stringOutput</span></span> | <span data-ttu-id="b508a-436">String</span><span class="sxs-lookup"><span data-stu-id="b508a-436">String</span></span> | <span data-ttu-id="b508a-437">O</span><span class="sxs-lookup"><span data-stu-id="b508a-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="b508a-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="b508a-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="b508a-439">傳回 hello 值在字串內的第一個位置。</span><span class="sxs-lookup"><span data-stu-id="b508a-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="b508a-440">hello 比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="b508a-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-441">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-441">Parameters</span></span>

| <span data-ttu-id="b508a-442">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-442">Parameter</span></span> | <span data-ttu-id="b508a-443">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-443">Required</span></span> | <span data-ttu-id="b508a-444">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-444">Type</span></span> | <span data-ttu-id="b508a-445">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="b508a-446">stringToSearch</span></span> |<span data-ttu-id="b508a-447">是</span><span class="sxs-lookup"><span data-stu-id="b508a-447">Yes</span></span> |<span data-ttu-id="b508a-448">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-448">string</span></span> |<span data-ttu-id="b508a-449">包含 hello 項目 toofind hello 值。</span><span class="sxs-lookup"><span data-stu-id="b508a-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="b508a-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="b508a-450">stringToFind</span></span> |<span data-ttu-id="b508a-451">是</span><span class="sxs-lookup"><span data-stu-id="b508a-451">Yes</span></span> |<span data-ttu-id="b508a-452">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-452">string</span></span> |<span data-ttu-id="b508a-453">hello 值 toofind。</span><span class="sxs-lookup"><span data-stu-id="b508a-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-454">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-454">Return value</span></span>

<span data-ttu-id="b508a-455">整數，代表 hello 項目 toofind hello 位置。</span><span class="sxs-lookup"><span data-stu-id="b508a-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="b508a-456">hello 值是以零為起始的。</span><span class="sxs-lookup"><span data-stu-id="b508a-456">hello value is zero-based.</span></span> <span data-ttu-id="b508a-457">如果找不到 hello 項目，則傳回-1。</span><span class="sxs-lookup"><span data-stu-id="b508a-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-458">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-458">Examples</span></span>

<span data-ttu-id="b508a-459">hello 下列範例顯示如何 toouse hello indexOf 和 lastIndexOf 函式：</span><span class="sxs-lookup"><span data-stu-id="b508a-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="b508a-460">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-461">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-461">Name</span></span> | <span data-ttu-id="b508a-462">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-462">Type</span></span> | <span data-ttu-id="b508a-463">值</span><span class="sxs-lookup"><span data-stu-id="b508a-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-464">firstT</span><span class="sxs-lookup"><span data-stu-id="b508a-464">firstT</span></span> | <span data-ttu-id="b508a-465">int</span><span class="sxs-lookup"><span data-stu-id="b508a-465">Int</span></span> | <span data-ttu-id="b508a-466">0</span><span class="sxs-lookup"><span data-stu-id="b508a-466">0</span></span> |
| <span data-ttu-id="b508a-467">lastT</span><span class="sxs-lookup"><span data-stu-id="b508a-467">lastT</span></span> | <span data-ttu-id="b508a-468">int</span><span class="sxs-lookup"><span data-stu-id="b508a-468">Int</span></span> | <span data-ttu-id="b508a-469">3</span><span class="sxs-lookup"><span data-stu-id="b508a-469">3</span></span> |
| <span data-ttu-id="b508a-470">firstString</span><span class="sxs-lookup"><span data-stu-id="b508a-470">firstString</span></span> | <span data-ttu-id="b508a-471">int</span><span class="sxs-lookup"><span data-stu-id="b508a-471">Int</span></span> | <span data-ttu-id="b508a-472">2</span><span class="sxs-lookup"><span data-stu-id="b508a-472">2</span></span> |
| <span data-ttu-id="b508a-473">lastString</span><span class="sxs-lookup"><span data-stu-id="b508a-473">lastString</span></span> | <span data-ttu-id="b508a-474">int</span><span class="sxs-lookup"><span data-stu-id="b508a-474">Int</span></span> | <span data-ttu-id="b508a-475">0</span><span class="sxs-lookup"><span data-stu-id="b508a-475">0</span></span> |
| <span data-ttu-id="b508a-476">notFound</span><span class="sxs-lookup"><span data-stu-id="b508a-476">notFound</span></span> | <span data-ttu-id="b508a-477">int</span><span class="sxs-lookup"><span data-stu-id="b508a-477">Int</span></span> | <span data-ttu-id="b508a-478">-1</span><span class="sxs-lookup"><span data-stu-id="b508a-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="b508a-479">last</span><span class="sxs-lookup"><span data-stu-id="b508a-479">last</span></span>
`last (arg1)`

<span data-ttu-id="b508a-480">傳回最後一個 hello 字串的字元或 hello hello 陣列的最後一個項目。</span><span class="sxs-lookup"><span data-stu-id="b508a-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-481">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-481">Parameters</span></span>

| <span data-ttu-id="b508a-482">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-482">Parameter</span></span> | <span data-ttu-id="b508a-483">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-483">Required</span></span> | <span data-ttu-id="b508a-484">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-484">Type</span></span> | <span data-ttu-id="b508a-485">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-486">arg1</span><span class="sxs-lookup"><span data-stu-id="b508a-486">arg1</span></span> |<span data-ttu-id="b508a-487">是</span><span class="sxs-lookup"><span data-stu-id="b508a-487">Yes</span></span> |<span data-ttu-id="b508a-488">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="b508a-488">array or string</span></span> |<span data-ttu-id="b508a-489">hello 值 tooretrieve hello 最後一個項目或字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-490">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-490">Return value</span></span>

<span data-ttu-id="b508a-491">Hello 最後一個字元，或 hello 型別 （字串、 int、 陣列或物件） hello 陣列中的最後一個項目的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-492">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-492">Examples</span></span>

<span data-ttu-id="b508a-493">hello 下列範例顯示如何 toouse hello 與陣列和字串的最後一個函式。</span><span class="sxs-lookup"><span data-stu-id="b508a-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="b508a-494">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-495">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-495">Name</span></span> | <span data-ttu-id="b508a-496">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-496">Type</span></span> | <span data-ttu-id="b508a-497">值</span><span class="sxs-lookup"><span data-stu-id="b508a-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-498">arrayOutput</span></span> | <span data-ttu-id="b508a-499">String</span><span class="sxs-lookup"><span data-stu-id="b508a-499">String</span></span> | <span data-ttu-id="b508a-500">three</span><span class="sxs-lookup"><span data-stu-id="b508a-500">three</span></span> |
| <span data-ttu-id="b508a-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-501">stringOutput</span></span> | <span data-ttu-id="b508a-502">String</span><span class="sxs-lookup"><span data-stu-id="b508a-502">String</span></span> | <span data-ttu-id="b508a-503">e</span><span class="sxs-lookup"><span data-stu-id="b508a-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="b508a-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="b508a-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="b508a-505">傳回 hello 值在字串內的最後一個位置。</span><span class="sxs-lookup"><span data-stu-id="b508a-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="b508a-506">hello 比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="b508a-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-507">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-507">Parameters</span></span>

| <span data-ttu-id="b508a-508">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-508">Parameter</span></span> | <span data-ttu-id="b508a-509">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-509">Required</span></span> | <span data-ttu-id="b508a-510">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-510">Type</span></span> | <span data-ttu-id="b508a-511">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="b508a-512">stringToSearch</span></span> |<span data-ttu-id="b508a-513">是</span><span class="sxs-lookup"><span data-stu-id="b508a-513">Yes</span></span> |<span data-ttu-id="b508a-514">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-514">string</span></span> |<span data-ttu-id="b508a-515">包含 hello 項目 toofind hello 值。</span><span class="sxs-lookup"><span data-stu-id="b508a-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="b508a-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="b508a-516">stringToFind</span></span> |<span data-ttu-id="b508a-517">是</span><span class="sxs-lookup"><span data-stu-id="b508a-517">Yes</span></span> |<span data-ttu-id="b508a-518">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-518">string</span></span> |<span data-ttu-id="b508a-519">hello 值 toofind。</span><span class="sxs-lookup"><span data-stu-id="b508a-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-520">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-520">Return value</span></span>

<span data-ttu-id="b508a-521">整數，代表 hello 項目 toofind hello 最後一個位置。</span><span class="sxs-lookup"><span data-stu-id="b508a-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="b508a-522">hello 值是以零為起始的。</span><span class="sxs-lookup"><span data-stu-id="b508a-522">hello value is zero-based.</span></span> <span data-ttu-id="b508a-523">如果找不到 hello 項目，則傳回-1。</span><span class="sxs-lookup"><span data-stu-id="b508a-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-524">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-524">Examples</span></span>

<span data-ttu-id="b508a-525">hello 下列範例顯示如何 toouse hello indexOf 和 lastIndexOf 函式：</span><span class="sxs-lookup"><span data-stu-id="b508a-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="b508a-526">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-527">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-527">Name</span></span> | <span data-ttu-id="b508a-528">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-528">Type</span></span> | <span data-ttu-id="b508a-529">值</span><span class="sxs-lookup"><span data-stu-id="b508a-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-530">firstT</span><span class="sxs-lookup"><span data-stu-id="b508a-530">firstT</span></span> | <span data-ttu-id="b508a-531">int</span><span class="sxs-lookup"><span data-stu-id="b508a-531">Int</span></span> | <span data-ttu-id="b508a-532">0</span><span class="sxs-lookup"><span data-stu-id="b508a-532">0</span></span> |
| <span data-ttu-id="b508a-533">lastT</span><span class="sxs-lookup"><span data-stu-id="b508a-533">lastT</span></span> | <span data-ttu-id="b508a-534">int</span><span class="sxs-lookup"><span data-stu-id="b508a-534">Int</span></span> | <span data-ttu-id="b508a-535">3</span><span class="sxs-lookup"><span data-stu-id="b508a-535">3</span></span> |
| <span data-ttu-id="b508a-536">firstString</span><span class="sxs-lookup"><span data-stu-id="b508a-536">firstString</span></span> | <span data-ttu-id="b508a-537">int</span><span class="sxs-lookup"><span data-stu-id="b508a-537">Int</span></span> | <span data-ttu-id="b508a-538">2</span><span class="sxs-lookup"><span data-stu-id="b508a-538">2</span></span> |
| <span data-ttu-id="b508a-539">lastString</span><span class="sxs-lookup"><span data-stu-id="b508a-539">lastString</span></span> | <span data-ttu-id="b508a-540">int</span><span class="sxs-lookup"><span data-stu-id="b508a-540">Int</span></span> | <span data-ttu-id="b508a-541">0</span><span class="sxs-lookup"><span data-stu-id="b508a-541">0</span></span> |
| <span data-ttu-id="b508a-542">notFound</span><span class="sxs-lookup"><span data-stu-id="b508a-542">notFound</span></span> | <span data-ttu-id="b508a-543">int</span><span class="sxs-lookup"><span data-stu-id="b508a-543">Int</span></span> | <span data-ttu-id="b508a-544">-1</span><span class="sxs-lookup"><span data-stu-id="b508a-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="b508a-545">length</span><span class="sxs-lookup"><span data-stu-id="b508a-545">length</span></span>
`length(string)`

<span data-ttu-id="b508a-546">傳回字串或陣列中的項目中的 hello 的字元數。</span><span class="sxs-lookup"><span data-stu-id="b508a-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-547">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-547">Parameters</span></span>

| <span data-ttu-id="b508a-548">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-548">Parameter</span></span> | <span data-ttu-id="b508a-549">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-549">Required</span></span> | <span data-ttu-id="b508a-550">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-550">Type</span></span> | <span data-ttu-id="b508a-551">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-552">arg1</span><span class="sxs-lookup"><span data-stu-id="b508a-552">arg1</span></span> |<span data-ttu-id="b508a-553">是</span><span class="sxs-lookup"><span data-stu-id="b508a-553">Yes</span></span> |<span data-ttu-id="b508a-554">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="b508a-554">array or string</span></span> |<span data-ttu-id="b508a-555">hello 取得 hello 元素數的陣列 toouse 或 hello 字串 toouse 取得 hello 的字元數。</span><span class="sxs-lookup"><span data-stu-id="b508a-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-556">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-556">Return value</span></span>

<span data-ttu-id="b508a-557">整數。</span><span class="sxs-lookup"><span data-stu-id="b508a-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="b508a-558">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-558">Examples</span></span>

<span data-ttu-id="b508a-559">下列範例會示範如何 hello toouse 與陣列和字串的長度：</span><span class="sxs-lookup"><span data-stu-id="b508a-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="b508a-560">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-561">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-561">Name</span></span> | <span data-ttu-id="b508a-562">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-562">Type</span></span> | <span data-ttu-id="b508a-563">值</span><span class="sxs-lookup"><span data-stu-id="b508a-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="b508a-564">arrayLength</span></span> | <span data-ttu-id="b508a-565">int</span><span class="sxs-lookup"><span data-stu-id="b508a-565">Int</span></span> | <span data-ttu-id="b508a-566">3</span><span class="sxs-lookup"><span data-stu-id="b508a-566">3</span></span> |
| <span data-ttu-id="b508a-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="b508a-567">stringLength</span></span> | <span data-ttu-id="b508a-568">int</span><span class="sxs-lookup"><span data-stu-id="b508a-568">Int</span></span> | <span data-ttu-id="b508a-569">13</span><span class="sxs-lookup"><span data-stu-id="b508a-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="b508a-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="b508a-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="b508a-571">藉由新增直到到達 hello 總指定的長度的字元 toohello 左傳回靠右對齊的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-572">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-572">Parameters</span></span>

| <span data-ttu-id="b508a-573">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-573">Parameter</span></span> | <span data-ttu-id="b508a-574">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-574">Required</span></span> | <span data-ttu-id="b508a-575">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-575">Type</span></span> | <span data-ttu-id="b508a-576">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="b508a-577">valueToPad</span></span> |<span data-ttu-id="b508a-578">是</span><span class="sxs-lookup"><span data-stu-id="b508a-578">Yes</span></span> |<span data-ttu-id="b508a-579">字串或整數</span><span class="sxs-lookup"><span data-stu-id="b508a-579">string or int</span></span> |<span data-ttu-id="b508a-580">hello 值 tooright-對齊。</span><span class="sxs-lookup"><span data-stu-id="b508a-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="b508a-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="b508a-581">totalLength</span></span> |<span data-ttu-id="b508a-582">是</span><span class="sxs-lookup"><span data-stu-id="b508a-582">Yes</span></span> |<span data-ttu-id="b508a-583">int</span><span class="sxs-lookup"><span data-stu-id="b508a-583">int</span></span> |<span data-ttu-id="b508a-584">傳回字串 hello 總數目 hello 中的字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="b508a-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="b508a-585">paddingCharacter</span></span> |<span data-ttu-id="b508a-586">否</span><span class="sxs-lookup"><span data-stu-id="b508a-586">No</span></span> |<span data-ttu-id="b508a-587">單一字元</span><span class="sxs-lookup"><span data-stu-id="b508a-587">single character</span></span> |<span data-ttu-id="b508a-588">hello 字元 toouse 左填補 hello 總長度為止。</span><span class="sxs-lookup"><span data-stu-id="b508a-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="b508a-589">hello 預設值是一個空格。</span><span class="sxs-lookup"><span data-stu-id="b508a-589">hello default value is a space.</span></span> |

<span data-ttu-id="b508a-590">如果 hello 原始字串的長度超過 hello toopad 字元數目，就會不加入任何字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="b508a-591">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-591">Return value</span></span>

<span data-ttu-id="b508a-592">字串至少 hello 指定字元的數。</span><span class="sxs-lookup"><span data-stu-id="b508a-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-593">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-593">Examples</span></span>

<span data-ttu-id="b508a-594">hello 下列範例顯示如何 toopad hello 使用者提供參數值加 hello 零字元直到達到 hello 的總字元數。</span><span class="sxs-lookup"><span data-stu-id="b508a-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

<span data-ttu-id="b508a-595">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-596">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-596">Name</span></span> | <span data-ttu-id="b508a-597">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-597">Type</span></span> | <span data-ttu-id="b508a-598">值</span><span class="sxs-lookup"><span data-stu-id="b508a-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-599">stringOutput</span></span> | <span data-ttu-id="b508a-600">String</span><span class="sxs-lookup"><span data-stu-id="b508a-600">String</span></span> | <span data-ttu-id="b508a-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="b508a-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="b508a-602">取代</span><span class="sxs-lookup"><span data-stu-id="b508a-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="b508a-603">傳回具備由另一個字串取代的一個字串之所有執行個體的新字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-604">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-604">Parameters</span></span>

| <span data-ttu-id="b508a-605">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-605">Parameter</span></span> | <span data-ttu-id="b508a-606">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-606">Required</span></span> | <span data-ttu-id="b508a-607">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-607">Type</span></span> | <span data-ttu-id="b508a-608">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-609">originalString</span><span class="sxs-lookup"><span data-stu-id="b508a-609">originalString</span></span> |<span data-ttu-id="b508a-610">是</span><span class="sxs-lookup"><span data-stu-id="b508a-610">Yes</span></span> |<span data-ttu-id="b508a-611">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-611">string</span></span> |<span data-ttu-id="b508a-612">hello 具有一個字串，取代成另一個字串的所有執行個體的值。</span><span class="sxs-lookup"><span data-stu-id="b508a-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="b508a-613">oldString</span><span class="sxs-lookup"><span data-stu-id="b508a-613">oldString</span></span> |<span data-ttu-id="b508a-614">是</span><span class="sxs-lookup"><span data-stu-id="b508a-614">Yes</span></span> |<span data-ttu-id="b508a-615">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-615">string</span></span> |<span data-ttu-id="b508a-616">hello 字串 toobe 從 hello 原始字串中移除。</span><span class="sxs-lookup"><span data-stu-id="b508a-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="b508a-617">newString</span><span class="sxs-lookup"><span data-stu-id="b508a-617">newString</span></span> |<span data-ttu-id="b508a-618">是</span><span class="sxs-lookup"><span data-stu-id="b508a-618">Yes</span></span> |<span data-ttu-id="b508a-619">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-619">string</span></span> |<span data-ttu-id="b508a-620">取代 hello hello 字串 tooadd 移除字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-621">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-621">Return value</span></span>

<span data-ttu-id="b508a-622">Hello 的字串取代字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-623">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-623">Examples</span></span>

<span data-ttu-id="b508a-624">hello 下列範例會顯示所有 tooremove 都虛線從 hello 使用者提供的字串的方式和 tooreplace 一部分 hello 以另一個字串的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

<span data-ttu-id="b508a-625">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-626">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-626">Name</span></span> | <span data-ttu-id="b508a-627">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-627">Type</span></span> | <span data-ttu-id="b508a-628">值</span><span class="sxs-lookup"><span data-stu-id="b508a-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-629">firstOutput</span></span> | <span data-ttu-id="b508a-630">String</span><span class="sxs-lookup"><span data-stu-id="b508a-630">String</span></span> | <span data-ttu-id="b508a-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="b508a-631">1231231234</span></span> |
| <span data-ttu-id="b508a-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-632">secodeOutput</span></span> | <span data-ttu-id="b508a-633">String</span><span class="sxs-lookup"><span data-stu-id="b508a-633">String</span></span> | <span data-ttu-id="b508a-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="b508a-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="b508a-635">skip</span><span class="sxs-lookup"><span data-stu-id="b508a-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="b508a-636">Hello 會指定所有 hello 元素的字元數或陣列後 hello 都指定的項目數目之後，傳回所有 hello 字元的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-637">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-637">Parameters</span></span>

| <span data-ttu-id="b508a-638">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-638">Parameter</span></span> | <span data-ttu-id="b508a-639">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-639">Required</span></span> | <span data-ttu-id="b508a-640">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-640">Type</span></span> | <span data-ttu-id="b508a-641">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="b508a-642">originalValue</span></span> |<span data-ttu-id="b508a-643">是</span><span class="sxs-lookup"><span data-stu-id="b508a-643">Yes</span></span> |<span data-ttu-id="b508a-644">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="b508a-644">array or string</span></span> |<span data-ttu-id="b508a-645">hello 陣列或字串 toouse 跳過。</span><span class="sxs-lookup"><span data-stu-id="b508a-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="b508a-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="b508a-646">numberToSkip</span></span> |<span data-ttu-id="b508a-647">是</span><span class="sxs-lookup"><span data-stu-id="b508a-647">Yes</span></span> |<span data-ttu-id="b508a-648">int</span><span class="sxs-lookup"><span data-stu-id="b508a-648">int</span></span> |<span data-ttu-id="b508a-649">hello tooskip 項目或字元數目。</span><span class="sxs-lookup"><span data-stu-id="b508a-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="b508a-650">如果此值為 0 或更少，所有 hello 項目，或傳回 hello 值中的字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="b508a-651">如果大於 hello hello 陣列或字串的長度，就會傳回空陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-652">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-652">Return value</span></span>

<span data-ttu-id="b508a-653">陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-654">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-654">Examples</span></span>

<span data-ttu-id="b508a-655">下列範例會略過 hello hello hello 陣列中指定的項目數目和 hello 的字串中指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="b508a-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="b508a-656">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-657">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-657">Name</span></span> | <span data-ttu-id="b508a-658">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-658">Type</span></span> | <span data-ttu-id="b508a-659">值</span><span class="sxs-lookup"><span data-stu-id="b508a-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-660">arrayOutput</span></span> | <span data-ttu-id="b508a-661">陣列</span><span class="sxs-lookup"><span data-stu-id="b508a-661">Array</span></span> | <span data-ttu-id="b508a-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="b508a-662">["three"]</span></span> |
| <span data-ttu-id="b508a-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-663">stringOutput</span></span> | <span data-ttu-id="b508a-664">String</span><span class="sxs-lookup"><span data-stu-id="b508a-664">String</span></span> | <span data-ttu-id="b508a-665">two three</span><span class="sxs-lookup"><span data-stu-id="b508a-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="b508a-666">split</span><span class="sxs-lookup"><span data-stu-id="b508a-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="b508a-667">傳回字串陣列，其中包含 hello 子字串 hello 的輸入字串 hello 所分隔指定的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="b508a-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-668">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-668">Parameters</span></span>

| <span data-ttu-id="b508a-669">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-669">Parameter</span></span> | <span data-ttu-id="b508a-670">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-670">Required</span></span> | <span data-ttu-id="b508a-671">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-671">Type</span></span> | <span data-ttu-id="b508a-672">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-673">inputString</span><span class="sxs-lookup"><span data-stu-id="b508a-673">inputString</span></span> |<span data-ttu-id="b508a-674">是</span><span class="sxs-lookup"><span data-stu-id="b508a-674">Yes</span></span> |<span data-ttu-id="b508a-675">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-675">string</span></span> |<span data-ttu-id="b508a-676">hello 字串 toosplit。</span><span class="sxs-lookup"><span data-stu-id="b508a-676">hello string toosplit.</span></span> |
| <span data-ttu-id="b508a-677">分隔符號</span><span class="sxs-lookup"><span data-stu-id="b508a-677">delimiter</span></span> |<span data-ttu-id="b508a-678">是</span><span class="sxs-lookup"><span data-stu-id="b508a-678">Yes</span></span> |<span data-ttu-id="b508a-679">字串或字串陣列</span><span class="sxs-lookup"><span data-stu-id="b508a-679">string or array of strings</span></span> |<span data-ttu-id="b508a-680">將分割 hello 字串 hello 分隔符號 toouse。</span><span class="sxs-lookup"><span data-stu-id="b508a-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-681">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-681">Return value</span></span>

<span data-ttu-id="b508a-682">字串的陣列。</span><span class="sxs-lookup"><span data-stu-id="b508a-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-683">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-683">Examples</span></span>

<span data-ttu-id="b508a-684">hello 下例 hello 輸入的字串分割以逗點，並以逗號或分號分隔。</span><span class="sxs-lookup"><span data-stu-id="b508a-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

<span data-ttu-id="b508a-685">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-686">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-686">Name</span></span> | <span data-ttu-id="b508a-687">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-687">Type</span></span> | <span data-ttu-id="b508a-688">值</span><span class="sxs-lookup"><span data-stu-id="b508a-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-689">firstOutput</span></span> | <span data-ttu-id="b508a-690">陣列</span><span class="sxs-lookup"><span data-stu-id="b508a-690">Array</span></span> | <span data-ttu-id="b508a-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="b508a-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="b508a-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-692">secondOutput</span></span> | <span data-ttu-id="b508a-693">陣列</span><span class="sxs-lookup"><span data-stu-id="b508a-693">Array</span></span> | <span data-ttu-id="b508a-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="b508a-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="b508a-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="b508a-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="b508a-696">判斷字串開頭是否為值。</span><span class="sxs-lookup"><span data-stu-id="b508a-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="b508a-697">hello 比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="b508a-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-698">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-698">Parameters</span></span>

| <span data-ttu-id="b508a-699">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-699">Parameter</span></span> | <span data-ttu-id="b508a-700">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-700">Required</span></span> | <span data-ttu-id="b508a-701">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-701">Type</span></span> | <span data-ttu-id="b508a-702">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="b508a-703">stringToSearch</span></span> |<span data-ttu-id="b508a-704">是</span><span class="sxs-lookup"><span data-stu-id="b508a-704">Yes</span></span> |<span data-ttu-id="b508a-705">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-705">string</span></span> |<span data-ttu-id="b508a-706">包含 hello 項目 toofind hello 值。</span><span class="sxs-lookup"><span data-stu-id="b508a-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="b508a-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="b508a-707">stringToFind</span></span> |<span data-ttu-id="b508a-708">是</span><span class="sxs-lookup"><span data-stu-id="b508a-708">Yes</span></span> |<span data-ttu-id="b508a-709">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-709">string</span></span> |<span data-ttu-id="b508a-710">hello 值 toofind。</span><span class="sxs-lookup"><span data-stu-id="b508a-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-711">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-711">Return value</span></span>

<span data-ttu-id="b508a-712">**True** hello 第一個字元或字元字串 hello 符合 hello 值; 否則**False**。</span><span class="sxs-lookup"><span data-stu-id="b508a-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-713">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-713">Examples</span></span>

<span data-ttu-id="b508a-714">hello 下列範例顯示如何 toouse hello startsWith 和 endsWith 函式：</span><span class="sxs-lookup"><span data-stu-id="b508a-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="b508a-715">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-716">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-716">Name</span></span> | <span data-ttu-id="b508a-717">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-717">Type</span></span> | <span data-ttu-id="b508a-718">值</span><span class="sxs-lookup"><span data-stu-id="b508a-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-719">startsTrue</span></span> | <span data-ttu-id="b508a-720">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-720">Bool</span></span> | <span data-ttu-id="b508a-721">True</span><span class="sxs-lookup"><span data-stu-id="b508a-721">True</span></span> |
| <span data-ttu-id="b508a-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-722">startsCapTrue</span></span> | <span data-ttu-id="b508a-723">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-723">Bool</span></span> | <span data-ttu-id="b508a-724">True</span><span class="sxs-lookup"><span data-stu-id="b508a-724">True</span></span> |
| <span data-ttu-id="b508a-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="b508a-725">startsFalse</span></span> | <span data-ttu-id="b508a-726">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-726">Bool</span></span> | <span data-ttu-id="b508a-727">False</span><span class="sxs-lookup"><span data-stu-id="b508a-727">False</span></span> |
| <span data-ttu-id="b508a-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-728">endsTrue</span></span> | <span data-ttu-id="b508a-729">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-729">Bool</span></span> | <span data-ttu-id="b508a-730">True</span><span class="sxs-lookup"><span data-stu-id="b508a-730">True</span></span> |
| <span data-ttu-id="b508a-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="b508a-731">endsCapTrue</span></span> | <span data-ttu-id="b508a-732">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-732">Bool</span></span> | <span data-ttu-id="b508a-733">True</span><span class="sxs-lookup"><span data-stu-id="b508a-733">True</span></span> |
| <span data-ttu-id="b508a-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="b508a-734">endsFalse</span></span> | <span data-ttu-id="b508a-735">Bool</span><span class="sxs-lookup"><span data-stu-id="b508a-735">Bool</span></span> | <span data-ttu-id="b508a-736">False</span><span class="sxs-lookup"><span data-stu-id="b508a-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="b508a-737">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="b508a-738">轉換 hello 指定值 tooa 字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-739">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-739">Parameters</span></span>

| <span data-ttu-id="b508a-740">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-740">Parameter</span></span> | <span data-ttu-id="b508a-741">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-741">Required</span></span> | <span data-ttu-id="b508a-742">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-742">Type</span></span> | <span data-ttu-id="b508a-743">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="b508a-744">valueToConvert</span></span> |<span data-ttu-id="b508a-745">是</span><span class="sxs-lookup"><span data-stu-id="b508a-745">Yes</span></span> | <span data-ttu-id="b508a-746">任意</span><span class="sxs-lookup"><span data-stu-id="b508a-746">Any</span></span> |<span data-ttu-id="b508a-747">hello 值 tooconvert toostring。</span><span class="sxs-lookup"><span data-stu-id="b508a-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="b508a-748">任何類型的值均可轉換，包括物件和陣列。</span><span class="sxs-lookup"><span data-stu-id="b508a-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-749">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-749">Return value</span></span>

<span data-ttu-id="b508a-750">Hello 轉換值的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-751">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-751">Examples</span></span>

<span data-ttu-id="b508a-752">hello 下列範例顯示如何 tooconvert 不同類型的值 toostrings:</span><span class="sxs-lookup"><span data-stu-id="b508a-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

<span data-ttu-id="b508a-753">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-754">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-754">Name</span></span> | <span data-ttu-id="b508a-755">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-755">Type</span></span> | <span data-ttu-id="b508a-756">值</span><span class="sxs-lookup"><span data-stu-id="b508a-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-757">objectOutput</span></span> | <span data-ttu-id="b508a-758">String</span><span class="sxs-lookup"><span data-stu-id="b508a-758">String</span></span> | <span data-ttu-id="b508a-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="b508a-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="b508a-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-760">arrayOutput</span></span> | <span data-ttu-id="b508a-761">String</span><span class="sxs-lookup"><span data-stu-id="b508a-761">String</span></span> | <span data-ttu-id="b508a-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="b508a-762">["a","b","c"]</span></span> |
| <span data-ttu-id="b508a-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-763">intOutput</span></span> | <span data-ttu-id="b508a-764">String</span><span class="sxs-lookup"><span data-stu-id="b508a-764">String</span></span> | <span data-ttu-id="b508a-765">5</span><span class="sxs-lookup"><span data-stu-id="b508a-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="b508a-766">substring</span><span class="sxs-lookup"><span data-stu-id="b508a-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="b508a-767">傳回子字串開始於指定的 hello 字元位置，並包含 hello 指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="b508a-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-768">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-768">Parameters</span></span>

| <span data-ttu-id="b508a-769">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-769">Parameter</span></span> | <span data-ttu-id="b508a-770">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-770">Required</span></span> | <span data-ttu-id="b508a-771">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-771">Type</span></span> | <span data-ttu-id="b508a-772">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="b508a-773">stringToParse</span></span> |<span data-ttu-id="b508a-774">是</span><span class="sxs-lookup"><span data-stu-id="b508a-774">Yes</span></span> |<span data-ttu-id="b508a-775">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-775">string</span></span> |<span data-ttu-id="b508a-776">擷取子字串的哪個 hello hello 的原始字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="b508a-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="b508a-777">startIndex</span></span> |<span data-ttu-id="b508a-778">否</span><span class="sxs-lookup"><span data-stu-id="b508a-778">No</span></span> |<span data-ttu-id="b508a-779">int</span><span class="sxs-lookup"><span data-stu-id="b508a-779">int</span></span> |<span data-ttu-id="b508a-780">hello 以零為起始起始字元位置 hello 的子字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="b508a-781">length</span><span class="sxs-lookup"><span data-stu-id="b508a-781">length</span></span> |<span data-ttu-id="b508a-782">否</span><span class="sxs-lookup"><span data-stu-id="b508a-782">No</span></span> |<span data-ttu-id="b508a-783">int</span><span class="sxs-lookup"><span data-stu-id="b508a-783">int</span></span> |<span data-ttu-id="b508a-784">hello hello 的子字串的字元數。</span><span class="sxs-lookup"><span data-stu-id="b508a-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="b508a-785">必須參考 tooa hello 字串內的位置。</span><span class="sxs-lookup"><span data-stu-id="b508a-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-786">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-786">Return value</span></span>

<span data-ttu-id="b508a-787">hello 子字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="b508a-788">備註</span><span class="sxs-lookup"><span data-stu-id="b508a-788">Remarks</span></span>

<span data-ttu-id="b508a-789">hello 函式失敗時的子字串 hello 超出 hello hello 字串的結尾。</span><span class="sxs-lookup"><span data-stu-id="b508a-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="b508a-790">下列範例中的 hello 因 hello 錯誤 「 hello 索引和長度參數必須參考 tooa hello 字串內的位置。</span><span class="sxs-lookup"><span data-stu-id="b508a-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="b508a-791">hello 索引參數: '0'，hello 長度參數: '11' hello hello 字串參數的長度: '10'。 」。</span><span class="sxs-lookup"><span data-stu-id="b508a-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="b508a-792">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-792">Examples</span></span>

<span data-ttu-id="b508a-793">下列範例中的 hello 自參數來擷取子字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-793">hello following example extracts a substring from a parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="b508a-794">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-795">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-795">Name</span></span> | <span data-ttu-id="b508a-796">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-796">Type</span></span> | <span data-ttu-id="b508a-797">值</span><span class="sxs-lookup"><span data-stu-id="b508a-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-798">substringOutput</span></span> | <span data-ttu-id="b508a-799">String</span><span class="sxs-lookup"><span data-stu-id="b508a-799">String</span></span> | <span data-ttu-id="b508a-800">two</span><span class="sxs-lookup"><span data-stu-id="b508a-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="b508a-801">take</span><span class="sxs-lookup"><span data-stu-id="b508a-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="b508a-802">傳回字串 hello 與指定從 hello 開頭的字元數 hello 字串，或以 hello 陣列指定從 hello 開頭 hello 陣列元素數目。</span><span class="sxs-lookup"><span data-stu-id="b508a-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-803">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-803">Parameters</span></span>

| <span data-ttu-id="b508a-804">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-804">Parameter</span></span> | <span data-ttu-id="b508a-805">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-805">Required</span></span> | <span data-ttu-id="b508a-806">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-806">Type</span></span> | <span data-ttu-id="b508a-807">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="b508a-808">originalValue</span></span> |<span data-ttu-id="b508a-809">是</span><span class="sxs-lookup"><span data-stu-id="b508a-809">Yes</span></span> |<span data-ttu-id="b508a-810">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="b508a-810">array or string</span></span> |<span data-ttu-id="b508a-811">hello 陣列或字串 tootake hello 中的項目。</span><span class="sxs-lookup"><span data-stu-id="b508a-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="b508a-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="b508a-812">numberToTake</span></span> |<span data-ttu-id="b508a-813">是</span><span class="sxs-lookup"><span data-stu-id="b508a-813">Yes</span></span> |<span data-ttu-id="b508a-814">int</span><span class="sxs-lookup"><span data-stu-id="b508a-814">int</span></span> |<span data-ttu-id="b508a-815">hello tootake 項目或字元數目。</span><span class="sxs-lookup"><span data-stu-id="b508a-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="b508a-816">如果此值為 0 或更小的值，則會傳回空白陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="b508a-817">如果它大於指定之陣列或字串 hello hello 長度，則會傳回所有 hello 陣列或字串中的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="b508a-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-818">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-818">Return value</span></span>

<span data-ttu-id="b508a-819">陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-820">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-820">Examples</span></span>

<span data-ttu-id="b508a-821">下列範例會採用 hello hello 指定 hello 陣列中的項目和從字串的字元數目。</span><span class="sxs-lookup"><span data-stu-id="b508a-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="b508a-822">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-823">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-823">Name</span></span> | <span data-ttu-id="b508a-824">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-824">Type</span></span> | <span data-ttu-id="b508a-825">值</span><span class="sxs-lookup"><span data-stu-id="b508a-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-826">arrayOutput</span></span> | <span data-ttu-id="b508a-827">陣列</span><span class="sxs-lookup"><span data-stu-id="b508a-827">Array</span></span> | <span data-ttu-id="b508a-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="b508a-828">["one", "two"]</span></span> |
| <span data-ttu-id="b508a-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-829">stringOutput</span></span> | <span data-ttu-id="b508a-830">String</span><span class="sxs-lookup"><span data-stu-id="b508a-830">String</span></span> | <span data-ttu-id="b508a-831">on</span><span class="sxs-lookup"><span data-stu-id="b508a-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="b508a-832">toLower</span><span class="sxs-lookup"><span data-stu-id="b508a-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="b508a-833">轉換 hello 指定字串 toolower 案例。</span><span class="sxs-lookup"><span data-stu-id="b508a-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-834">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-834">Parameters</span></span>

| <span data-ttu-id="b508a-835">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-835">Parameter</span></span> | <span data-ttu-id="b508a-836">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-836">Required</span></span> | <span data-ttu-id="b508a-837">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-837">Type</span></span> | <span data-ttu-id="b508a-838">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="b508a-839">stringToChange</span></span> |<span data-ttu-id="b508a-840">是</span><span class="sxs-lookup"><span data-stu-id="b508a-840">Yes</span></span> |<span data-ttu-id="b508a-841">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-841">string</span></span> |<span data-ttu-id="b508a-842">hello 值 tooconvert toolower 案例。</span><span class="sxs-lookup"><span data-stu-id="b508a-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-843">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-843">Return value</span></span>

<span data-ttu-id="b508a-844">hello 字串轉換 toolower 案例。</span><span class="sxs-lookup"><span data-stu-id="b508a-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-845">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-845">Examples</span></span>

<span data-ttu-id="b508a-846">下列範例中的 hello 將轉換的參數值 toolower 案例和 tooupper 案例。</span><span class="sxs-lookup"><span data-stu-id="b508a-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="b508a-847">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-848">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-848">Name</span></span> | <span data-ttu-id="b508a-849">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-849">Type</span></span> | <span data-ttu-id="b508a-850">值</span><span class="sxs-lookup"><span data-stu-id="b508a-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-851">toLowerOutput</span></span> | <span data-ttu-id="b508a-852">String</span><span class="sxs-lookup"><span data-stu-id="b508a-852">String</span></span> | <span data-ttu-id="b508a-853">one two three</span><span class="sxs-lookup"><span data-stu-id="b508a-853">one two three</span></span> |
| <span data-ttu-id="b508a-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-854">toUpperOutput</span></span> | <span data-ttu-id="b508a-855">String</span><span class="sxs-lookup"><span data-stu-id="b508a-855">String</span></span> | <span data-ttu-id="b508a-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="b508a-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="b508a-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="b508a-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="b508a-858">轉換 hello 指定字串 tooupper 案例。</span><span class="sxs-lookup"><span data-stu-id="b508a-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-859">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-859">Parameters</span></span>

| <span data-ttu-id="b508a-860">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-860">Parameter</span></span> | <span data-ttu-id="b508a-861">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-861">Required</span></span> | <span data-ttu-id="b508a-862">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-862">Type</span></span> | <span data-ttu-id="b508a-863">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="b508a-864">stringToChange</span></span> |<span data-ttu-id="b508a-865">是</span><span class="sxs-lookup"><span data-stu-id="b508a-865">Yes</span></span> |<span data-ttu-id="b508a-866">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-866">string</span></span> |<span data-ttu-id="b508a-867">hello 值 tooconvert tooupper 案例。</span><span class="sxs-lookup"><span data-stu-id="b508a-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-868">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-868">Return value</span></span>

<span data-ttu-id="b508a-869">hello 字串轉換 tooupper 案例。</span><span class="sxs-lookup"><span data-stu-id="b508a-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-870">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-870">Examples</span></span>

<span data-ttu-id="b508a-871">下列範例中的 hello 將轉換的參數值 toolower 案例和 tooupper 案例。</span><span class="sxs-lookup"><span data-stu-id="b508a-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="b508a-872">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-873">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-873">Name</span></span> | <span data-ttu-id="b508a-874">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-874">Type</span></span> | <span data-ttu-id="b508a-875">值</span><span class="sxs-lookup"><span data-stu-id="b508a-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-876">toLowerOutput</span></span> | <span data-ttu-id="b508a-877">String</span><span class="sxs-lookup"><span data-stu-id="b508a-877">String</span></span> | <span data-ttu-id="b508a-878">one two three</span><span class="sxs-lookup"><span data-stu-id="b508a-878">one two three</span></span> |
| <span data-ttu-id="b508a-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-879">toUpperOutput</span></span> | <span data-ttu-id="b508a-880">String</span><span class="sxs-lookup"><span data-stu-id="b508a-880">String</span></span> | <span data-ttu-id="b508a-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="b508a-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="b508a-882">修剪</span><span class="sxs-lookup"><span data-stu-id="b508a-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="b508a-883">移除所有開頭和尾端空白字元 hello 從指定的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-884">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-884">Parameters</span></span>

| <span data-ttu-id="b508a-885">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-885">Parameter</span></span> | <span data-ttu-id="b508a-886">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-886">Required</span></span> | <span data-ttu-id="b508a-887">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-887">Type</span></span> | <span data-ttu-id="b508a-888">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="b508a-889">stringToTrim</span></span> |<span data-ttu-id="b508a-890">是</span><span class="sxs-lookup"><span data-stu-id="b508a-890">Yes</span></span> |<span data-ttu-id="b508a-891">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-891">string</span></span> |<span data-ttu-id="b508a-892">hello 值 tootrim。</span><span class="sxs-lookup"><span data-stu-id="b508a-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-893">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-893">Return value</span></span>

<span data-ttu-id="b508a-894">hello 不含字串開頭和尾端空白字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-895">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-895">Examples</span></span>

<span data-ttu-id="b508a-896">hello 下列範例會修剪 hello hello 參數的空格字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-896">hello following example trims hello white-space characters from hello parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="b508a-897">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-898">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-898">Name</span></span> | <span data-ttu-id="b508a-899">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-899">Type</span></span> | <span data-ttu-id="b508a-900">值</span><span class="sxs-lookup"><span data-stu-id="b508a-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-901">傳回</span><span class="sxs-lookup"><span data-stu-id="b508a-901">return</span></span> | <span data-ttu-id="b508a-902">String</span><span class="sxs-lookup"><span data-stu-id="b508a-902">String</span></span> | <span data-ttu-id="b508a-903">one two three</span><span class="sxs-lookup"><span data-stu-id="b508a-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="b508a-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="b508a-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="b508a-905">建立根據 hello 值做為參數提供具決定性的雜湊字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="b508a-906">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-906">Parameters</span></span>

| <span data-ttu-id="b508a-907">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-907">Parameter</span></span> | <span data-ttu-id="b508a-908">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-908">Required</span></span> | <span data-ttu-id="b508a-909">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-909">Type</span></span> | <span data-ttu-id="b508a-910">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-911">baseString</span><span class="sxs-lookup"><span data-stu-id="b508a-911">baseString</span></span> |<span data-ttu-id="b508a-912">是</span><span class="sxs-lookup"><span data-stu-id="b508a-912">Yes</span></span> |<span data-ttu-id="b508a-913">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-913">string</span></span> |<span data-ttu-id="b508a-914">hello 值用於 hello 雜湊函式 toocreate 的唯一字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="b508a-915">視需要，也會使用其他參數</span><span class="sxs-lookup"><span data-stu-id="b508a-915">additional parameters as needed</span></span> |<span data-ttu-id="b508a-916">否</span><span class="sxs-lookup"><span data-stu-id="b508a-916">No</span></span> |<span data-ttu-id="b508a-917">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-917">string</span></span> |<span data-ttu-id="b508a-918">您可以將許多字串為指定的唯一性 hello 層級的所需的 toocreate hello 值。</span><span class="sxs-lookup"><span data-stu-id="b508a-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="b508a-919">備註</span><span class="sxs-lookup"><span data-stu-id="b508a-919">Remarks</span></span>

<span data-ttu-id="b508a-920">當您需要 toocreate 資源的唯一名稱，此函式是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="b508a-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="b508a-921">您提供的唯一性的 hello 結果的 hello 範圍限制的參數值。</span><span class="sxs-lookup"><span data-stu-id="b508a-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="b508a-922">您可以指定 hello 名稱是否唯一下 toosubscription、 資源群組或部署。</span><span class="sxs-lookup"><span data-stu-id="b508a-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="b508a-923">hello 傳回值不是隨機的字串，但而 hello 雜湊函式的結果。</span><span class="sxs-lookup"><span data-stu-id="b508a-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="b508a-924">hello 傳回值為 13 個字元。</span><span class="sxs-lookup"><span data-stu-id="b508a-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="b508a-925">它不是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="b508a-925">It is not globally unique.</span></span> <span data-ttu-id="b508a-926">您可能想 toocombine hello 值與前置詞的命名慣例 toocreate 有意義的名稱。</span><span class="sxs-lookup"><span data-stu-id="b508a-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="b508a-927">hello 下列範例顯示 hello hello 傳回值格式。</span><span class="sxs-lookup"><span data-stu-id="b508a-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="b508a-928">hello 實際值會因 hello 提供的參數。</span><span class="sxs-lookup"><span data-stu-id="b508a-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="b508a-929">hello 遵循範例顯示如何 toouse uniqueString toocreate 的唯一值通常使用層級。</span><span class="sxs-lookup"><span data-stu-id="b508a-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="b508a-930">唯一的限定範圍的 toosubscription</span><span class="sxs-lookup"><span data-stu-id="b508a-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="b508a-931">唯一的限定範圍的 tooresource 群組</span><span class="sxs-lookup"><span data-stu-id="b508a-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="b508a-932">資源群組的唯一已設定領域的 toodeployment</span><span class="sxs-lookup"><span data-stu-id="b508a-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="b508a-933">hello 下列範例顯示如何 toocreate 儲存體帳戶的唯一名稱根據您的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b508a-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="b508a-934">Hello 資源群組內，hello 名稱不是唯一如果建構 hello 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="b508a-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="b508a-935">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-935">Return value</span></span>

<span data-ttu-id="b508a-936">包含 13 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-937">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-937">Examples</span></span>

<span data-ttu-id="b508a-938">下列範例中的 hello uniquestring 從傳回的結果：</span><span class="sxs-lookup"><span data-stu-id="b508a-938">hello following example returns results from uniquestring:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a><span data-ttu-id="b508a-939">uri</span><span class="sxs-lookup"><span data-stu-id="b508a-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="b508a-940">藉由結合 hello baseUri 和 hello relativeUri 字串建立的絕對 URI。</span><span class="sxs-lookup"><span data-stu-id="b508a-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-941">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-941">Parameters</span></span>

| <span data-ttu-id="b508a-942">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-942">Parameter</span></span> | <span data-ttu-id="b508a-943">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-943">Required</span></span> | <span data-ttu-id="b508a-944">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-944">Type</span></span> | <span data-ttu-id="b508a-945">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="b508a-946">baseUri</span></span> |<span data-ttu-id="b508a-947">是</span><span class="sxs-lookup"><span data-stu-id="b508a-947">Yes</span></span> |<span data-ttu-id="b508a-948">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-948">string</span></span> |<span data-ttu-id="b508a-949">hello 基底 uri 的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-949">hello base uri string.</span></span> |
| <span data-ttu-id="b508a-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="b508a-950">relativeUri</span></span> |<span data-ttu-id="b508a-951">是</span><span class="sxs-lookup"><span data-stu-id="b508a-951">Yes</span></span> |<span data-ttu-id="b508a-952">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-952">string</span></span> |<span data-ttu-id="b508a-953">hello 相對 uri 字串 tooadd toohello 基底 uri 字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="b508a-954">hello 值 hello **baseUri**參數可以包含特定的檔案，但建構 hello URI 時，系統會使用 hello 基底路徑。</span><span class="sxs-lookup"><span data-stu-id="b508a-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="b508a-955">例如，傳遞`http://contoso.com/resources/azuredeploy.json`做為基底 URI 中的 hello baseUri 參數結果`http://contoso.com/resources/`。</span><span class="sxs-lookup"><span data-stu-id="b508a-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="b508a-956">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-956">Return value</span></span>

<span data-ttu-id="b508a-957">字串，代表 hello hello 基底和相對值的絕對 URI。</span><span class="sxs-lookup"><span data-stu-id="b508a-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-958">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-958">Examples</span></span>

<span data-ttu-id="b508a-959">hello 下列範例顯示如何 tooconstruct 連結 tooa 巢狀的範本為基礎的 hello 父樣板的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="b508a-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="b508a-960">下列範例會示範如何 hello toouse uri，uriComponent，和 uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="b508a-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="b508a-961">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-962">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-962">Name</span></span> | <span data-ttu-id="b508a-963">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-963">Type</span></span> | <span data-ttu-id="b508a-964">值</span><span class="sxs-lookup"><span data-stu-id="b508a-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-965">uriOutput</span></span> | <span data-ttu-id="b508a-966">String</span><span class="sxs-lookup"><span data-stu-id="b508a-966">String</span></span> | <span data-ttu-id="b508a-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="b508a-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-968">componentOutput</span></span> | <span data-ttu-id="b508a-969">String</span><span class="sxs-lookup"><span data-stu-id="b508a-969">String</span></span> | <span data-ttu-id="b508a-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="b508a-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-971">toStringOutput</span></span> | <span data-ttu-id="b508a-972">String</span><span class="sxs-lookup"><span data-stu-id="b508a-972">String</span></span> | <span data-ttu-id="b508a-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="b508a-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="b508a-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="b508a-975">將 URI 編碼。</span><span class="sxs-lookup"><span data-stu-id="b508a-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-976">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-976">Parameters</span></span>

| <span data-ttu-id="b508a-977">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-977">Parameter</span></span> | <span data-ttu-id="b508a-978">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-978">Required</span></span> | <span data-ttu-id="b508a-979">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-979">Type</span></span> | <span data-ttu-id="b508a-980">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="b508a-981">stringToEncode</span></span> |<span data-ttu-id="b508a-982">是</span><span class="sxs-lookup"><span data-stu-id="b508a-982">Yes</span></span> |<span data-ttu-id="b508a-983">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-983">string</span></span> |<span data-ttu-id="b508a-984">hello 值 tooencode。</span><span class="sxs-lookup"><span data-stu-id="b508a-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-985">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-985">Return value</span></span>

<span data-ttu-id="b508a-986">Hello URI 的字串編碼值。</span><span class="sxs-lookup"><span data-stu-id="b508a-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-987">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-987">Examples</span></span>

<span data-ttu-id="b508a-988">下列範例會示範如何 hello toouse uri，uriComponent，和 uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="b508a-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="b508a-989">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-990">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-990">Name</span></span> | <span data-ttu-id="b508a-991">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-991">Type</span></span> | <span data-ttu-id="b508a-992">值</span><span class="sxs-lookup"><span data-stu-id="b508a-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-993">uriOutput</span></span> | <span data-ttu-id="b508a-994">String</span><span class="sxs-lookup"><span data-stu-id="b508a-994">String</span></span> | <span data-ttu-id="b508a-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="b508a-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-996">componentOutput</span></span> | <span data-ttu-id="b508a-997">String</span><span class="sxs-lookup"><span data-stu-id="b508a-997">String</span></span> | <span data-ttu-id="b508a-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="b508a-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-999">toStringOutput</span></span> | <span data-ttu-id="b508a-1000">String</span><span class="sxs-lookup"><span data-stu-id="b508a-1000">String</span></span> | <span data-ttu-id="b508a-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="b508a-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="b508a-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="b508a-1003">傳回 URI 編碼值的字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="b508a-1004">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-1004">Parameters</span></span>

| <span data-ttu-id="b508a-1005">參數</span><span class="sxs-lookup"><span data-stu-id="b508a-1005">Parameter</span></span> | <span data-ttu-id="b508a-1006">必要</span><span class="sxs-lookup"><span data-stu-id="b508a-1006">Required</span></span> | <span data-ttu-id="b508a-1007">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-1007">Type</span></span> | <span data-ttu-id="b508a-1008">說明</span><span class="sxs-lookup"><span data-stu-id="b508a-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b508a-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="b508a-1009">uriEncodedString</span></span> |<span data-ttu-id="b508a-1010">是</span><span class="sxs-lookup"><span data-stu-id="b508a-1010">Yes</span></span> |<span data-ttu-id="b508a-1011">字串</span><span class="sxs-lookup"><span data-stu-id="b508a-1011">string</span></span> |<span data-ttu-id="b508a-1012">hello URI 編碼值 tooconvert tooa 字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="b508a-1013">傳回值</span><span class="sxs-lookup"><span data-stu-id="b508a-1013">Return value</span></span>

<span data-ttu-id="b508a-1014">URI 編碼值的解碼字串。</span><span class="sxs-lookup"><span data-stu-id="b508a-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="b508a-1015">範例</span><span class="sxs-lookup"><span data-stu-id="b508a-1015">Examples</span></span>

<span data-ttu-id="b508a-1016">下列範例會示範如何 hello toouse uri，uriComponent，和 uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="b508a-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="b508a-1017">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="b508a-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="b508a-1018">名稱</span><span class="sxs-lookup"><span data-stu-id="b508a-1018">Name</span></span> | <span data-ttu-id="b508a-1019">類型</span><span class="sxs-lookup"><span data-stu-id="b508a-1019">Type</span></span> | <span data-ttu-id="b508a-1020">值</span><span class="sxs-lookup"><span data-stu-id="b508a-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="b508a-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-1021">uriOutput</span></span> | <span data-ttu-id="b508a-1022">String</span><span class="sxs-lookup"><span data-stu-id="b508a-1022">String</span></span> | <span data-ttu-id="b508a-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="b508a-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-1024">componentOutput</span></span> | <span data-ttu-id="b508a-1025">String</span><span class="sxs-lookup"><span data-stu-id="b508a-1025">String</span></span> | <span data-ttu-id="b508a-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="b508a-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="b508a-1027">toStringOutput</span></span> | <span data-ttu-id="b508a-1028">String</span><span class="sxs-lookup"><span data-stu-id="b508a-1028">String</span></span> | <span data-ttu-id="b508a-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b508a-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b508a-1030">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b508a-1030">Next steps</span></span>
* <span data-ttu-id="b508a-1031">如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="b508a-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="b508a-1032">toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="b508a-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="b508a-1033">tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="b508a-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="b508a-1034">toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="b508a-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

