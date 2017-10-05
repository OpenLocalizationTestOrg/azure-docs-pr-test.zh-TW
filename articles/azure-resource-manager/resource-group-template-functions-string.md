---
title: "Azure Resource Manager 範本函式 - 字串 | Microsoft Docs"
description: "描述 Azure Resource Manager 範本中用來使用字串的函式。"
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
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="1dac9-103">Azure Resource Manager 範本的字串函式</span><span class="sxs-lookup"><span data-stu-id="1dac9-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="1dac9-104">資源管理員提供下列函式以使用字串：</span><span class="sxs-lookup"><span data-stu-id="1dac9-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="1dac9-105">base64</span><span class="sxs-lookup"><span data-stu-id="1dac9-105">base64</span></span>](#base64)
* [<span data-ttu-id="1dac9-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="1dac9-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="1dac9-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="1dac9-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="1dac9-108">concat</span><span class="sxs-lookup"><span data-stu-id="1dac9-108">concat</span></span>](#concat)
* [<span data-ttu-id="1dac9-109">contains</span><span class="sxs-lookup"><span data-stu-id="1dac9-109">contains</span></span>](#contains)
* [<span data-ttu-id="1dac9-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="1dac9-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="1dac9-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="1dac9-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="1dac9-112">empty</span><span class="sxs-lookup"><span data-stu-id="1dac9-112">empty</span></span>](#empty)
* [<span data-ttu-id="1dac9-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="1dac9-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="1dac9-114">first</span><span class="sxs-lookup"><span data-stu-id="1dac9-114">first</span></span>](#first)
* [<span data-ttu-id="1dac9-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="1dac9-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="1dac9-116">last</span><span class="sxs-lookup"><span data-stu-id="1dac9-116">last</span></span>](#last)
* [<span data-ttu-id="1dac9-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="1dac9-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="1dac9-118">length</span><span class="sxs-lookup"><span data-stu-id="1dac9-118">length</span></span>](#length)
* [<span data-ttu-id="1dac9-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="1dac9-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="1dac9-120">replace</span><span class="sxs-lookup"><span data-stu-id="1dac9-120">replace</span></span>](#replace)
* [<span data-ttu-id="1dac9-121">skip</span><span class="sxs-lookup"><span data-stu-id="1dac9-121">skip</span></span>](#skip)
* [<span data-ttu-id="1dac9-122">分割</span><span class="sxs-lookup"><span data-stu-id="1dac9-122">split</span></span>](#split)
* [<span data-ttu-id="1dac9-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="1dac9-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="1dac9-124">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-124">string</span></span>](#string)
* [<span data-ttu-id="1dac9-125">substring</span><span class="sxs-lookup"><span data-stu-id="1dac9-125">substring</span></span>](#substring)
* [<span data-ttu-id="1dac9-126">take</span><span class="sxs-lookup"><span data-stu-id="1dac9-126">take</span></span>](#take)
* [<span data-ttu-id="1dac9-127">toLower</span><span class="sxs-lookup"><span data-stu-id="1dac9-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="1dac9-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="1dac9-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="1dac9-129">修剪</span><span class="sxs-lookup"><span data-stu-id="1dac9-129">trim</span></span>](#trim)
* [<span data-ttu-id="1dac9-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="1dac9-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="1dac9-131">uri</span><span class="sxs-lookup"><span data-stu-id="1dac9-131">uri</span></span>](#uri)
* [<span data-ttu-id="1dac9-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="1dac9-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="1dac9-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="1dac9-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="1dac9-134">base64</span><span class="sxs-lookup"><span data-stu-id="1dac9-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="1dac9-135">傳回輸入字串的 base64 表示法。</span><span class="sxs-lookup"><span data-stu-id="1dac9-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-136">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-136">Parameters</span></span>

| <span data-ttu-id="1dac9-137">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-137">Parameter</span></span> | <span data-ttu-id="1dac9-138">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-138">Required</span></span> | <span data-ttu-id="1dac9-139">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-139">Type</span></span> | <span data-ttu-id="1dac9-140">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-141">inputString</span><span class="sxs-lookup"><span data-stu-id="1dac9-141">inputString</span></span> |<span data-ttu-id="1dac9-142">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-142">Yes</span></span> |<span data-ttu-id="1dac9-143">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-143">string</span></span> |<span data-ttu-id="1dac9-144">要以 base64 表示法傳回的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-145">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-145">Return value</span></span>

<span data-ttu-id="1dac9-146">字串，包含 base64 表示法。</span><span class="sxs-lookup"><span data-stu-id="1dac9-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-147">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-147">Examples</span></span>

<span data-ttu-id="1dac9-148">下列範例顯示如何使用 base64 函式。</span><span class="sxs-lookup"><span data-stu-id="1dac9-148">The following example shows how to use the base64 function.</span></span>

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

<span data-ttu-id="1dac9-149">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-150">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-150">Name</span></span> | <span data-ttu-id="1dac9-151">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-151">Type</span></span> | <span data-ttu-id="1dac9-152">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="1dac9-153">base64Output</span></span> | <span data-ttu-id="1dac9-154">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-154">String</span></span> | <span data-ttu-id="1dac9-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="1dac9-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="1dac9-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-156">toStringOutput</span></span> | <span data-ttu-id="1dac9-157">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-157">String</span></span> | <span data-ttu-id="1dac9-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="1dac9-158">one, two, three</span></span> |
| <span data-ttu-id="1dac9-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-159">toJsonOutput</span></span> | <span data-ttu-id="1dac9-160">Object</span><span class="sxs-lookup"><span data-stu-id="1dac9-160">Object</span></span> | <span data-ttu-id="1dac9-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="1dac9-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="1dac9-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="1dac9-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="1dac9-163">將 base64 表示法轉換為 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="1dac9-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-164">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-164">Parameters</span></span>

| <span data-ttu-id="1dac9-165">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-165">Parameter</span></span> | <span data-ttu-id="1dac9-166">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-166">Required</span></span> | <span data-ttu-id="1dac9-167">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-167">Type</span></span> | <span data-ttu-id="1dac9-168">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="1dac9-169">base64Value</span></span> |<span data-ttu-id="1dac9-170">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-170">Yes</span></span> |<span data-ttu-id="1dac9-171">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-171">string</span></span> |<span data-ttu-id="1dac9-172">要轉換為 JSON 物件的 base64 表示法。</span><span class="sxs-lookup"><span data-stu-id="1dac9-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-173">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-173">Return value</span></span>

<span data-ttu-id="1dac9-174">JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="1dac9-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-175">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-175">Examples</span></span>

<span data-ttu-id="1dac9-176">下列範例會使用 base64ToJson 函式來轉換 base64 值︰</span><span class="sxs-lookup"><span data-stu-id="1dac9-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

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

<span data-ttu-id="1dac9-177">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-178">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-178">Name</span></span> | <span data-ttu-id="1dac9-179">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-179">Type</span></span> | <span data-ttu-id="1dac9-180">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="1dac9-181">base64Output</span></span> | <span data-ttu-id="1dac9-182">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-182">String</span></span> | <span data-ttu-id="1dac9-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="1dac9-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="1dac9-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-184">toStringOutput</span></span> | <span data-ttu-id="1dac9-185">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-185">String</span></span> | <span data-ttu-id="1dac9-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="1dac9-186">one, two, three</span></span> |
| <span data-ttu-id="1dac9-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-187">toJsonOutput</span></span> | <span data-ttu-id="1dac9-188">Object</span><span class="sxs-lookup"><span data-stu-id="1dac9-188">Object</span></span> | <span data-ttu-id="1dac9-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="1dac9-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="1dac9-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="1dac9-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="1dac9-191">將 base64 表示法轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-192">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-192">Parameters</span></span>

| <span data-ttu-id="1dac9-193">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-193">Parameter</span></span> | <span data-ttu-id="1dac9-194">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-194">Required</span></span> | <span data-ttu-id="1dac9-195">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-195">Type</span></span> | <span data-ttu-id="1dac9-196">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="1dac9-197">base64Value</span></span> |<span data-ttu-id="1dac9-198">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-198">Yes</span></span> |<span data-ttu-id="1dac9-199">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-199">string</span></span> |<span data-ttu-id="1dac9-200">要轉換為字串的 base64 表示法。</span><span class="sxs-lookup"><span data-stu-id="1dac9-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-201">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-201">Return value</span></span>

<span data-ttu-id="1dac9-202">轉換後之 base64 值的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-203">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-203">Examples</span></span>

<span data-ttu-id="1dac9-204">下列範例會使用 base64ToString 函式來轉換 base64 值︰</span><span class="sxs-lookup"><span data-stu-id="1dac9-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

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

<span data-ttu-id="1dac9-205">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-206">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-206">Name</span></span> | <span data-ttu-id="1dac9-207">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-207">Type</span></span> | <span data-ttu-id="1dac9-208">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="1dac9-209">base64Output</span></span> | <span data-ttu-id="1dac9-210">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-210">String</span></span> | <span data-ttu-id="1dac9-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="1dac9-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="1dac9-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-212">toStringOutput</span></span> | <span data-ttu-id="1dac9-213">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-213">String</span></span> | <span data-ttu-id="1dac9-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="1dac9-214">one, two, three</span></span> |
| <span data-ttu-id="1dac9-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-215">toJsonOutput</span></span> | <span data-ttu-id="1dac9-216">Object</span><span class="sxs-lookup"><span data-stu-id="1dac9-216">Object</span></span> | <span data-ttu-id="1dac9-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="1dac9-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="1dac9-218">concat</span><span class="sxs-lookup"><span data-stu-id="1dac9-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="1dac9-219">結合多個字串值並傳回串連字串，或結合多個陣列並傳回串連陣列。</span><span class="sxs-lookup"><span data-stu-id="1dac9-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-220">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-220">Parameters</span></span>

| <span data-ttu-id="1dac9-221">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-221">Parameter</span></span> | <span data-ttu-id="1dac9-222">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-222">Required</span></span> | <span data-ttu-id="1dac9-223">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-223">Type</span></span> | <span data-ttu-id="1dac9-224">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-225">arg1</span><span class="sxs-lookup"><span data-stu-id="1dac9-225">arg1</span></span> |<span data-ttu-id="1dac9-226">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-226">Yes</span></span> |<span data-ttu-id="1dac9-227">字串或陣列</span><span class="sxs-lookup"><span data-stu-id="1dac9-227">string or array</span></span> |<span data-ttu-id="1dac9-228">串連的第一個值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="1dac9-229">其他引數</span><span class="sxs-lookup"><span data-stu-id="1dac9-229">additional arguments</span></span> |<span data-ttu-id="1dac9-230">否</span><span class="sxs-lookup"><span data-stu-id="1dac9-230">No</span></span> |<span data-ttu-id="1dac9-231">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-231">string</span></span> |<span data-ttu-id="1dac9-232">串連的其他值 (循序順序)。</span><span class="sxs-lookup"><span data-stu-id="1dac9-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-233">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-233">Return value</span></span>
<span data-ttu-id="1dac9-234">串連值的字串或陣列。</span><span class="sxs-lookup"><span data-stu-id="1dac9-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-235">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-235">Examples</span></span>

<span data-ttu-id="1dac9-236">下列範例顯示如何結合兩個字串值並傳回串連字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="1dac9-237">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-238">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-238">Name</span></span> | <span data-ttu-id="1dac9-239">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-239">Type</span></span> | <span data-ttu-id="1dac9-240">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-241">concatOutput</span></span> | <span data-ttu-id="1dac9-242">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-242">String</span></span> | <span data-ttu-id="1dac9-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="1dac9-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="1dac9-244">下一個範例顯示如何結合兩個陣列。</span><span class="sxs-lookup"><span data-stu-id="1dac9-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="1dac9-245">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-246">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-246">Name</span></span> | <span data-ttu-id="1dac9-247">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-247">Type</span></span> | <span data-ttu-id="1dac9-248">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-249">return</span><span class="sxs-lookup"><span data-stu-id="1dac9-249">return</span></span> | <span data-ttu-id="1dac9-250">陣列</span><span class="sxs-lookup"><span data-stu-id="1dac9-250">Array</span></span> | <span data-ttu-id="1dac9-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="1dac9-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="1dac9-252">contains</span><span class="sxs-lookup"><span data-stu-id="1dac9-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="1dac9-253">檢查陣列中是否包含值、物件中是否包含索引鍵，或字串中是否包含子字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-254">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-254">Parameters</span></span>

| <span data-ttu-id="1dac9-255">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-255">Parameter</span></span> | <span data-ttu-id="1dac9-256">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-256">Required</span></span> | <span data-ttu-id="1dac9-257">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-257">Type</span></span> | <span data-ttu-id="1dac9-258">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-259">container</span><span class="sxs-lookup"><span data-stu-id="1dac9-259">container</span></span> |<span data-ttu-id="1dac9-260">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-260">Yes</span></span> |<span data-ttu-id="1dac9-261">陣列、物件或字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-261">array, object, or string</span></span> |<span data-ttu-id="1dac9-262">其中包含要尋找之值的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="1dac9-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="1dac9-263">itemToFind</span></span> |<span data-ttu-id="1dac9-264">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-264">Yes</span></span> |<span data-ttu-id="1dac9-265">字串或整數</span><span class="sxs-lookup"><span data-stu-id="1dac9-265">string or int</span></span> |<span data-ttu-id="1dac9-266">要尋找的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-267">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-267">Return value</span></span>

<span data-ttu-id="1dac9-268">找到項目則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="1dac9-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-269">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-269">Examples</span></span>

<span data-ttu-id="1dac9-270">下列範例顯示如何使用不同類型的 contains：</span><span class="sxs-lookup"><span data-stu-id="1dac9-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="1dac9-271">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-272">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-272">Name</span></span> | <span data-ttu-id="1dac9-273">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-273">Type</span></span> | <span data-ttu-id="1dac9-274">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-275">stringTrue</span></span> | <span data-ttu-id="1dac9-276">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-276">Bool</span></span> | <span data-ttu-id="1dac9-277">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-277">True</span></span> |
| <span data-ttu-id="1dac9-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="1dac9-278">stringFalse</span></span> | <span data-ttu-id="1dac9-279">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-279">Bool</span></span> | <span data-ttu-id="1dac9-280">False</span><span class="sxs-lookup"><span data-stu-id="1dac9-280">False</span></span> |
| <span data-ttu-id="1dac9-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-281">objectTrue</span></span> | <span data-ttu-id="1dac9-282">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-282">Bool</span></span> | <span data-ttu-id="1dac9-283">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-283">True</span></span> |
| <span data-ttu-id="1dac9-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="1dac9-284">objectFalse</span></span> | <span data-ttu-id="1dac9-285">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-285">Bool</span></span> | <span data-ttu-id="1dac9-286">False</span><span class="sxs-lookup"><span data-stu-id="1dac9-286">False</span></span> |
| <span data-ttu-id="1dac9-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-287">arrayTrue</span></span> | <span data-ttu-id="1dac9-288">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-288">Bool</span></span> | <span data-ttu-id="1dac9-289">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-289">True</span></span> |
| <span data-ttu-id="1dac9-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="1dac9-290">arrayFalse</span></span> | <span data-ttu-id="1dac9-291">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-291">Bool</span></span> | <span data-ttu-id="1dac9-292">False</span><span class="sxs-lookup"><span data-stu-id="1dac9-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="1dac9-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="1dac9-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="1dac9-294">將值轉換為資料 URI。</span><span class="sxs-lookup"><span data-stu-id="1dac9-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-295">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-295">Parameters</span></span>

| <span data-ttu-id="1dac9-296">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-296">Parameter</span></span> | <span data-ttu-id="1dac9-297">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-297">Required</span></span> | <span data-ttu-id="1dac9-298">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-298">Type</span></span> | <span data-ttu-id="1dac9-299">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="1dac9-300">stringToConvert</span></span> |<span data-ttu-id="1dac9-301">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-301">Yes</span></span> |<span data-ttu-id="1dac9-302">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-302">string</span></span> |<span data-ttu-id="1dac9-303">要轉換為資料 URI 的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-304">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-304">Return value</span></span>

<span data-ttu-id="1dac9-305">格式化為資料 URI 的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-306">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-306">Examples</span></span>

<span data-ttu-id="1dac9-307">下列範例會將值轉換為資料 URI，並將資料 URI 轉換為字串︰</span><span class="sxs-lookup"><span data-stu-id="1dac9-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

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

<span data-ttu-id="1dac9-308">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-309">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-309">Name</span></span> | <span data-ttu-id="1dac9-310">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-310">Type</span></span> | <span data-ttu-id="1dac9-311">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-312">dataUriOutput</span></span> | <span data-ttu-id="1dac9-313">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-313">String</span></span> | <span data-ttu-id="1dac9-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="1dac9-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="1dac9-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-315">toStringOutput</span></span> | <span data-ttu-id="1dac9-316">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-316">String</span></span> | <span data-ttu-id="1dac9-317">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="1dac9-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="1dac9-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="1dac9-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="1dac9-319">將資料 URI 格式化值轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-320">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-320">Parameters</span></span>

| <span data-ttu-id="1dac9-321">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-321">Parameter</span></span> | <span data-ttu-id="1dac9-322">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-322">Required</span></span> | <span data-ttu-id="1dac9-323">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-323">Type</span></span> | <span data-ttu-id="1dac9-324">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="1dac9-325">dataUriToConvert</span></span> |<span data-ttu-id="1dac9-326">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-326">Yes</span></span> |<span data-ttu-id="1dac9-327">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-327">string</span></span> |<span data-ttu-id="1dac9-328">要轉換的資料 URI 值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-329">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-329">Return value</span></span>

<span data-ttu-id="1dac9-330">字串，包含已轉換的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-331">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-331">Examples</span></span>

<span data-ttu-id="1dac9-332">下列範例會將值轉換為資料 URI，並將資料 URI 轉換為字串︰</span><span class="sxs-lookup"><span data-stu-id="1dac9-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

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

<span data-ttu-id="1dac9-333">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-334">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-334">Name</span></span> | <span data-ttu-id="1dac9-335">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-335">Type</span></span> | <span data-ttu-id="1dac9-336">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-337">dataUriOutput</span></span> | <span data-ttu-id="1dac9-338">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-338">String</span></span> | <span data-ttu-id="1dac9-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="1dac9-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="1dac9-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-340">toStringOutput</span></span> | <span data-ttu-id="1dac9-341">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-341">String</span></span> | <span data-ttu-id="1dac9-342">Hello, World!</span><span class="sxs-lookup"><span data-stu-id="1dac9-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="1dac9-343">empty</span><span class="sxs-lookup"><span data-stu-id="1dac9-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="1dac9-344">判斷陣列、物件或字串是否空白。</span><span class="sxs-lookup"><span data-stu-id="1dac9-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-345">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-345">Parameters</span></span>

| <span data-ttu-id="1dac9-346">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-346">Parameter</span></span> | <span data-ttu-id="1dac9-347">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-347">Required</span></span> | <span data-ttu-id="1dac9-348">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-348">Type</span></span> | <span data-ttu-id="1dac9-349">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="1dac9-350">itemToTest</span></span> |<span data-ttu-id="1dac9-351">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-351">Yes</span></span> |<span data-ttu-id="1dac9-352">陣列、物件或字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-352">array, object, or string</span></span> |<span data-ttu-id="1dac9-353">要檢查其是否為空白的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-354">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-354">Return value</span></span>

<span data-ttu-id="1dac9-355">如果值空白則傳回 **True**，否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="1dac9-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-356">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-356">Examples</span></span>

<span data-ttu-id="1dac9-357">下列範例會檢查陣列、物件和字串是否空白。</span><span class="sxs-lookup"><span data-stu-id="1dac9-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="1dac9-358">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-359">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-359">Name</span></span> | <span data-ttu-id="1dac9-360">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-360">Type</span></span> | <span data-ttu-id="1dac9-361">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="1dac9-362">arrayEmpty</span></span> | <span data-ttu-id="1dac9-363">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-363">Bool</span></span> | <span data-ttu-id="1dac9-364">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-364">True</span></span> |
| <span data-ttu-id="1dac9-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="1dac9-365">objectEmpty</span></span> | <span data-ttu-id="1dac9-366">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-366">Bool</span></span> | <span data-ttu-id="1dac9-367">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-367">True</span></span> |
| <span data-ttu-id="1dac9-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="1dac9-368">stringEmpty</span></span> | <span data-ttu-id="1dac9-369">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-369">Bool</span></span> | <span data-ttu-id="1dac9-370">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="1dac9-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="1dac9-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="1dac9-372">判斷字串結尾是否為值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="1dac9-373">此比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-374">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-374">Parameters</span></span>

| <span data-ttu-id="1dac9-375">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-375">Parameter</span></span> | <span data-ttu-id="1dac9-376">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-376">Required</span></span> | <span data-ttu-id="1dac9-377">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-377">Type</span></span> | <span data-ttu-id="1dac9-378">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="1dac9-379">stringToSearch</span></span> |<span data-ttu-id="1dac9-380">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-380">Yes</span></span> |<span data-ttu-id="1dac9-381">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-381">string</span></span> |<span data-ttu-id="1dac9-382">其中包含要尋找之項目的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="1dac9-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="1dac9-383">stringToFind</span></span> |<span data-ttu-id="1dac9-384">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-384">Yes</span></span> |<span data-ttu-id="1dac9-385">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-385">string</span></span> |<span data-ttu-id="1dac9-386">要尋找的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-387">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-387">Return value</span></span>

<span data-ttu-id="1dac9-388">如果最後一個字元或字串字元與該值相符，則傳回 **True**；否則會傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="1dac9-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-389">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-389">Examples</span></span>

<span data-ttu-id="1dac9-390">下列範例顯示如何使用 startsWith 和 endsWith 函式：</span><span class="sxs-lookup"><span data-stu-id="1dac9-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="1dac9-391">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-392">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-392">Name</span></span> | <span data-ttu-id="1dac9-393">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-393">Type</span></span> | <span data-ttu-id="1dac9-394">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-395">startsTrue</span></span> | <span data-ttu-id="1dac9-396">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-396">Bool</span></span> | <span data-ttu-id="1dac9-397">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-397">True</span></span> |
| <span data-ttu-id="1dac9-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-398">startsCapTrue</span></span> | <span data-ttu-id="1dac9-399">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-399">Bool</span></span> | <span data-ttu-id="1dac9-400">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-400">True</span></span> |
| <span data-ttu-id="1dac9-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="1dac9-401">startsFalse</span></span> | <span data-ttu-id="1dac9-402">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-402">Bool</span></span> | <span data-ttu-id="1dac9-403">False</span><span class="sxs-lookup"><span data-stu-id="1dac9-403">False</span></span> |
| <span data-ttu-id="1dac9-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-404">endsTrue</span></span> | <span data-ttu-id="1dac9-405">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-405">Bool</span></span> | <span data-ttu-id="1dac9-406">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-406">True</span></span> |
| <span data-ttu-id="1dac9-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-407">endsCapTrue</span></span> | <span data-ttu-id="1dac9-408">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-408">Bool</span></span> | <span data-ttu-id="1dac9-409">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-409">True</span></span> |
| <span data-ttu-id="1dac9-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="1dac9-410">endsFalse</span></span> | <span data-ttu-id="1dac9-411">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-411">Bool</span></span> | <span data-ttu-id="1dac9-412">False</span><span class="sxs-lookup"><span data-stu-id="1dac9-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="1dac9-413">first</span><span class="sxs-lookup"><span data-stu-id="1dac9-413">first</span></span>
`first(arg1)`

<span data-ttu-id="1dac9-414">傳回字串的第一個字元或陣列的第一個元素。</span><span class="sxs-lookup"><span data-stu-id="1dac9-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-415">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-415">Parameters</span></span>

| <span data-ttu-id="1dac9-416">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-416">Parameter</span></span> | <span data-ttu-id="1dac9-417">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-417">Required</span></span> | <span data-ttu-id="1dac9-418">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-418">Type</span></span> | <span data-ttu-id="1dac9-419">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-420">arg1</span><span class="sxs-lookup"><span data-stu-id="1dac9-420">arg1</span></span> |<span data-ttu-id="1dac9-421">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-421">Yes</span></span> |<span data-ttu-id="1dac9-422">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-422">array or string</span></span> |<span data-ttu-id="1dac9-423">要擷取其第一個元素或字元的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-424">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-424">Return value</span></span>

<span data-ttu-id="1dac9-425">陣列中第一個字元的字串或第一個元素的類型 (字串、整數、陣列或物件)。</span><span class="sxs-lookup"><span data-stu-id="1dac9-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-426">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-426">Examples</span></span>

<span data-ttu-id="1dac9-427">下列範例顯示如何搭配使用 first 函式與陣列和字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="1dac9-428">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-429">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-429">Name</span></span> | <span data-ttu-id="1dac9-430">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-430">Type</span></span> | <span data-ttu-id="1dac9-431">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-432">arrayOutput</span></span> | <span data-ttu-id="1dac9-433">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-433">String</span></span> | <span data-ttu-id="1dac9-434">one</span><span class="sxs-lookup"><span data-stu-id="1dac9-434">one</span></span> |
| <span data-ttu-id="1dac9-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-435">stringOutput</span></span> | <span data-ttu-id="1dac9-436">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-436">String</span></span> | <span data-ttu-id="1dac9-437">O</span><span class="sxs-lookup"><span data-stu-id="1dac9-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="1dac9-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="1dac9-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="1dac9-439">傳回值在字串內的第一個位置。</span><span class="sxs-lookup"><span data-stu-id="1dac9-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="1dac9-440">此比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-441">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-441">Parameters</span></span>

| <span data-ttu-id="1dac9-442">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-442">Parameter</span></span> | <span data-ttu-id="1dac9-443">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-443">Required</span></span> | <span data-ttu-id="1dac9-444">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-444">Type</span></span> | <span data-ttu-id="1dac9-445">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="1dac9-446">stringToSearch</span></span> |<span data-ttu-id="1dac9-447">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-447">Yes</span></span> |<span data-ttu-id="1dac9-448">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-448">string</span></span> |<span data-ttu-id="1dac9-449">其中包含要尋找之項目的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="1dac9-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="1dac9-450">stringToFind</span></span> |<span data-ttu-id="1dac9-451">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-451">Yes</span></span> |<span data-ttu-id="1dac9-452">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-452">string</span></span> |<span data-ttu-id="1dac9-453">要尋找的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-454">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-454">Return value</span></span>

<span data-ttu-id="1dac9-455">整數，代表要尋找之項目的位置。</span><span class="sxs-lookup"><span data-stu-id="1dac9-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="1dac9-456">此值是以零為起始。</span><span class="sxs-lookup"><span data-stu-id="1dac9-456">The value is zero-based.</span></span> <span data-ttu-id="1dac9-457">如果找不到項目，則傳回 -1。</span><span class="sxs-lookup"><span data-stu-id="1dac9-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-458">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-458">Examples</span></span>

<span data-ttu-id="1dac9-459">下列範例顯示如何使用 indexOf 和 lastIndexOf 函式：</span><span class="sxs-lookup"><span data-stu-id="1dac9-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="1dac9-460">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-461">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-461">Name</span></span> | <span data-ttu-id="1dac9-462">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-462">Type</span></span> | <span data-ttu-id="1dac9-463">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-464">firstT</span><span class="sxs-lookup"><span data-stu-id="1dac9-464">firstT</span></span> | <span data-ttu-id="1dac9-465">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-465">Int</span></span> | <span data-ttu-id="1dac9-466">0</span><span class="sxs-lookup"><span data-stu-id="1dac9-466">0</span></span> |
| <span data-ttu-id="1dac9-467">lastT</span><span class="sxs-lookup"><span data-stu-id="1dac9-467">lastT</span></span> | <span data-ttu-id="1dac9-468">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-468">Int</span></span> | <span data-ttu-id="1dac9-469">3</span><span class="sxs-lookup"><span data-stu-id="1dac9-469">3</span></span> |
| <span data-ttu-id="1dac9-470">firstString</span><span class="sxs-lookup"><span data-stu-id="1dac9-470">firstString</span></span> | <span data-ttu-id="1dac9-471">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-471">Int</span></span> | <span data-ttu-id="1dac9-472">2</span><span class="sxs-lookup"><span data-stu-id="1dac9-472">2</span></span> |
| <span data-ttu-id="1dac9-473">lastString</span><span class="sxs-lookup"><span data-stu-id="1dac9-473">lastString</span></span> | <span data-ttu-id="1dac9-474">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-474">Int</span></span> | <span data-ttu-id="1dac9-475">0</span><span class="sxs-lookup"><span data-stu-id="1dac9-475">0</span></span> |
| <span data-ttu-id="1dac9-476">notFound</span><span class="sxs-lookup"><span data-stu-id="1dac9-476">notFound</span></span> | <span data-ttu-id="1dac9-477">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-477">Int</span></span> | <span data-ttu-id="1dac9-478">-1</span><span class="sxs-lookup"><span data-stu-id="1dac9-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="1dac9-479">last</span><span class="sxs-lookup"><span data-stu-id="1dac9-479">last</span></span>
`last (arg1)`

<span data-ttu-id="1dac9-480">傳回字串的最後一個字元或陣列的最後一個元素。</span><span class="sxs-lookup"><span data-stu-id="1dac9-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-481">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-481">Parameters</span></span>

| <span data-ttu-id="1dac9-482">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-482">Parameter</span></span> | <span data-ttu-id="1dac9-483">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-483">Required</span></span> | <span data-ttu-id="1dac9-484">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-484">Type</span></span> | <span data-ttu-id="1dac9-485">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-486">arg1</span><span class="sxs-lookup"><span data-stu-id="1dac9-486">arg1</span></span> |<span data-ttu-id="1dac9-487">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-487">Yes</span></span> |<span data-ttu-id="1dac9-488">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-488">array or string</span></span> |<span data-ttu-id="1dac9-489">要擷取其最後一個元素或字元的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-490">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-490">Return value</span></span>

<span data-ttu-id="1dac9-491">陣列中最後一個字元的字串，或最後一個元素的類型 (字串、整數、陣列或物件)。</span><span class="sxs-lookup"><span data-stu-id="1dac9-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-492">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-492">Examples</span></span>

<span data-ttu-id="1dac9-493">下列範例顯示如何搭配使用 last 函式與陣列和字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="1dac9-494">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-495">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-495">Name</span></span> | <span data-ttu-id="1dac9-496">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-496">Type</span></span> | <span data-ttu-id="1dac9-497">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-498">arrayOutput</span></span> | <span data-ttu-id="1dac9-499">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-499">String</span></span> | <span data-ttu-id="1dac9-500">three</span><span class="sxs-lookup"><span data-stu-id="1dac9-500">three</span></span> |
| <span data-ttu-id="1dac9-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-501">stringOutput</span></span> | <span data-ttu-id="1dac9-502">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-502">String</span></span> | <span data-ttu-id="1dac9-503">e</span><span class="sxs-lookup"><span data-stu-id="1dac9-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="1dac9-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="1dac9-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="1dac9-505">傳回值在字串內的最後一個位置。</span><span class="sxs-lookup"><span data-stu-id="1dac9-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="1dac9-506">此比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-507">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-507">Parameters</span></span>

| <span data-ttu-id="1dac9-508">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-508">Parameter</span></span> | <span data-ttu-id="1dac9-509">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-509">Required</span></span> | <span data-ttu-id="1dac9-510">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-510">Type</span></span> | <span data-ttu-id="1dac9-511">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="1dac9-512">stringToSearch</span></span> |<span data-ttu-id="1dac9-513">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-513">Yes</span></span> |<span data-ttu-id="1dac9-514">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-514">string</span></span> |<span data-ttu-id="1dac9-515">其中包含要尋找之項目的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="1dac9-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="1dac9-516">stringToFind</span></span> |<span data-ttu-id="1dac9-517">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-517">Yes</span></span> |<span data-ttu-id="1dac9-518">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-518">string</span></span> |<span data-ttu-id="1dac9-519">要尋找的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-520">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-520">Return value</span></span>

<span data-ttu-id="1dac9-521">整數，代表要尋找之項目的最後一個位置。</span><span class="sxs-lookup"><span data-stu-id="1dac9-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="1dac9-522">此值是以零為起始。</span><span class="sxs-lookup"><span data-stu-id="1dac9-522">The value is zero-based.</span></span> <span data-ttu-id="1dac9-523">如果找不到項目，則傳回 -1。</span><span class="sxs-lookup"><span data-stu-id="1dac9-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-524">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-524">Examples</span></span>

<span data-ttu-id="1dac9-525">下列範例顯示如何使用 indexOf 和 lastIndexOf 函式：</span><span class="sxs-lookup"><span data-stu-id="1dac9-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="1dac9-526">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-527">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-527">Name</span></span> | <span data-ttu-id="1dac9-528">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-528">Type</span></span> | <span data-ttu-id="1dac9-529">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-530">firstT</span><span class="sxs-lookup"><span data-stu-id="1dac9-530">firstT</span></span> | <span data-ttu-id="1dac9-531">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-531">Int</span></span> | <span data-ttu-id="1dac9-532">0</span><span class="sxs-lookup"><span data-stu-id="1dac9-532">0</span></span> |
| <span data-ttu-id="1dac9-533">lastT</span><span class="sxs-lookup"><span data-stu-id="1dac9-533">lastT</span></span> | <span data-ttu-id="1dac9-534">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-534">Int</span></span> | <span data-ttu-id="1dac9-535">3</span><span class="sxs-lookup"><span data-stu-id="1dac9-535">3</span></span> |
| <span data-ttu-id="1dac9-536">firstString</span><span class="sxs-lookup"><span data-stu-id="1dac9-536">firstString</span></span> | <span data-ttu-id="1dac9-537">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-537">Int</span></span> | <span data-ttu-id="1dac9-538">2</span><span class="sxs-lookup"><span data-stu-id="1dac9-538">2</span></span> |
| <span data-ttu-id="1dac9-539">lastString</span><span class="sxs-lookup"><span data-stu-id="1dac9-539">lastString</span></span> | <span data-ttu-id="1dac9-540">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-540">Int</span></span> | <span data-ttu-id="1dac9-541">0</span><span class="sxs-lookup"><span data-stu-id="1dac9-541">0</span></span> |
| <span data-ttu-id="1dac9-542">notFound</span><span class="sxs-lookup"><span data-stu-id="1dac9-542">notFound</span></span> | <span data-ttu-id="1dac9-543">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-543">Int</span></span> | <span data-ttu-id="1dac9-544">-1</span><span class="sxs-lookup"><span data-stu-id="1dac9-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="1dac9-545">length</span><span class="sxs-lookup"><span data-stu-id="1dac9-545">length</span></span>
`length(string)`

<span data-ttu-id="1dac9-546">傳回字串中的字元數目或陣列中的元素數目。</span><span class="sxs-lookup"><span data-stu-id="1dac9-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-547">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-547">Parameters</span></span>

| <span data-ttu-id="1dac9-548">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-548">Parameter</span></span> | <span data-ttu-id="1dac9-549">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-549">Required</span></span> | <span data-ttu-id="1dac9-550">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-550">Type</span></span> | <span data-ttu-id="1dac9-551">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-552">arg1</span><span class="sxs-lookup"><span data-stu-id="1dac9-552">arg1</span></span> |<span data-ttu-id="1dac9-553">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-553">Yes</span></span> |<span data-ttu-id="1dac9-554">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-554">array or string</span></span> |<span data-ttu-id="1dac9-555">要用來取得元素數目的陣列，或用來取得字元數目的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-556">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-556">Return value</span></span>

<span data-ttu-id="1dac9-557">整數。</span><span class="sxs-lookup"><span data-stu-id="1dac9-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="1dac9-558">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-558">Examples</span></span>

<span data-ttu-id="1dac9-559">下列範例顯示如何搭配使用 length 與陣列和字串：</span><span class="sxs-lookup"><span data-stu-id="1dac9-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="1dac9-560">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-561">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-561">Name</span></span> | <span data-ttu-id="1dac9-562">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-562">Type</span></span> | <span data-ttu-id="1dac9-563">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="1dac9-564">arrayLength</span></span> | <span data-ttu-id="1dac9-565">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-565">Int</span></span> | <span data-ttu-id="1dac9-566">3</span><span class="sxs-lookup"><span data-stu-id="1dac9-566">3</span></span> |
| <span data-ttu-id="1dac9-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="1dac9-567">stringLength</span></span> | <span data-ttu-id="1dac9-568">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-568">Int</span></span> | <span data-ttu-id="1dac9-569">13</span><span class="sxs-lookup"><span data-stu-id="1dac9-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="1dac9-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="1dac9-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="1dac9-571">藉由將字元新增至左邊，直到到達指定的總長度，以傳回靠右對齊的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-572">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-572">Parameters</span></span>

| <span data-ttu-id="1dac9-573">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-573">Parameter</span></span> | <span data-ttu-id="1dac9-574">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-574">Required</span></span> | <span data-ttu-id="1dac9-575">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-575">Type</span></span> | <span data-ttu-id="1dac9-576">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="1dac9-577">valueToPad</span></span> |<span data-ttu-id="1dac9-578">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-578">Yes</span></span> |<span data-ttu-id="1dac9-579">字串或整數</span><span class="sxs-lookup"><span data-stu-id="1dac9-579">string or int</span></span> |<span data-ttu-id="1dac9-580">要靠右對齊的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-580">The value to right-align.</span></span> |
| <span data-ttu-id="1dac9-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="1dac9-581">totalLength</span></span> |<span data-ttu-id="1dac9-582">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-582">Yes</span></span> |<span data-ttu-id="1dac9-583">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-583">int</span></span> |<span data-ttu-id="1dac9-584">傳回字串中的字元總數。</span><span class="sxs-lookup"><span data-stu-id="1dac9-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="1dac9-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="1dac9-585">paddingCharacter</span></span> |<span data-ttu-id="1dac9-586">否</span><span class="sxs-lookup"><span data-stu-id="1dac9-586">No</span></span> |<span data-ttu-id="1dac9-587">單一字元</span><span class="sxs-lookup"><span data-stu-id="1dac9-587">single character</span></span> |<span data-ttu-id="1dac9-588">要用於左側填補直到達到總長度的字元。</span><span class="sxs-lookup"><span data-stu-id="1dac9-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="1dac9-589">預設值是空格。</span><span class="sxs-lookup"><span data-stu-id="1dac9-589">The default value is a space.</span></span> |

<span data-ttu-id="1dac9-590">如果原始字串長度超過要填補的字元數，則不會新增任何字元。</span><span class="sxs-lookup"><span data-stu-id="1dac9-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="1dac9-591">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-591">Return value</span></span>

<span data-ttu-id="1dac9-592">至少含有指定字元數的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-593">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-593">Examples</span></span>

<span data-ttu-id="1dac9-594">下列範例顯示如何藉由新增「零」字元直到符合字元總數，以填補使用者提供的參數值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

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

<span data-ttu-id="1dac9-595">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-596">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-596">Name</span></span> | <span data-ttu-id="1dac9-597">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-597">Type</span></span> | <span data-ttu-id="1dac9-598">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-599">stringOutput</span></span> | <span data-ttu-id="1dac9-600">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-600">String</span></span> | <span data-ttu-id="1dac9-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="1dac9-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="1dac9-602">取代</span><span class="sxs-lookup"><span data-stu-id="1dac9-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="1dac9-603">傳回具備由另一個字串取代的一個字串之所有執行個體的新字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-604">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-604">Parameters</span></span>

| <span data-ttu-id="1dac9-605">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-605">Parameter</span></span> | <span data-ttu-id="1dac9-606">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-606">Required</span></span> | <span data-ttu-id="1dac9-607">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-607">Type</span></span> | <span data-ttu-id="1dac9-608">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-609">originalString</span><span class="sxs-lookup"><span data-stu-id="1dac9-609">originalString</span></span> |<span data-ttu-id="1dac9-610">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-610">Yes</span></span> |<span data-ttu-id="1dac9-611">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-611">string</span></span> |<span data-ttu-id="1dac9-612">具備由另一個字串取代的一個字串之所有執行個體的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="1dac9-613">oldString</span><span class="sxs-lookup"><span data-stu-id="1dac9-613">oldString</span></span> |<span data-ttu-id="1dac9-614">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-614">Yes</span></span> |<span data-ttu-id="1dac9-615">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-615">string</span></span> |<span data-ttu-id="1dac9-616">要從原始字串中移除的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="1dac9-617">newString</span><span class="sxs-lookup"><span data-stu-id="1dac9-617">newString</span></span> |<span data-ttu-id="1dac9-618">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-618">Yes</span></span> |<span data-ttu-id="1dac9-619">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-619">string</span></span> |<span data-ttu-id="1dac9-620">要新增來取代移除之字串的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-621">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-621">Return value</span></span>

<span data-ttu-id="1dac9-622">具有已取代字元的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-623">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-623">Examples</span></span>

<span data-ttu-id="1dac9-624">下列範例會示範如何從使用者提供的字串中將所有的連字號移除，以及如何使用另一個字串來取代一部分的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

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

<span data-ttu-id="1dac9-625">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-626">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-626">Name</span></span> | <span data-ttu-id="1dac9-627">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-627">Type</span></span> | <span data-ttu-id="1dac9-628">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-629">firstOutput</span></span> | <span data-ttu-id="1dac9-630">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-630">String</span></span> | <span data-ttu-id="1dac9-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="1dac9-631">1231231234</span></span> |
| <span data-ttu-id="1dac9-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-632">secodeOutput</span></span> | <span data-ttu-id="1dac9-633">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-633">String</span></span> | <span data-ttu-id="1dac9-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="1dac9-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="1dac9-635">skip</span><span class="sxs-lookup"><span data-stu-id="1dac9-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="1dac9-636">傳回位於指定字元數目之後的所有字元所組成的字串，或傳回位於指定元素數目之後的所有元素所形成的陣列。</span><span class="sxs-lookup"><span data-stu-id="1dac9-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-637">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-637">Parameters</span></span>

| <span data-ttu-id="1dac9-638">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-638">Parameter</span></span> | <span data-ttu-id="1dac9-639">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-639">Required</span></span> | <span data-ttu-id="1dac9-640">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-640">Type</span></span> | <span data-ttu-id="1dac9-641">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="1dac9-642">originalValue</span></span> |<span data-ttu-id="1dac9-643">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-643">Yes</span></span> |<span data-ttu-id="1dac9-644">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-644">array or string</span></span> |<span data-ttu-id="1dac9-645">要用於略過的陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="1dac9-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="1dac9-646">numberToSkip</span></span> |<span data-ttu-id="1dac9-647">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-647">Yes</span></span> |<span data-ttu-id="1dac9-648">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-648">int</span></span> |<span data-ttu-id="1dac9-649">要略過的元素或字元數。</span><span class="sxs-lookup"><span data-stu-id="1dac9-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="1dac9-650">如果此值為 0 或更小的值，則會傳回值內的所有元素或字元。</span><span class="sxs-lookup"><span data-stu-id="1dac9-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="1dac9-651">如果此值大於陣列或字串的長度，則會傳回空白陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-652">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-652">Return value</span></span>

<span data-ttu-id="1dac9-653">陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-654">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-654">Examples</span></span>

<span data-ttu-id="1dac9-655">下列範例會略過陣列中指定的元素數目，以及字串中指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="1dac9-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="1dac9-656">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-657">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-657">Name</span></span> | <span data-ttu-id="1dac9-658">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-658">Type</span></span> | <span data-ttu-id="1dac9-659">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-660">arrayOutput</span></span> | <span data-ttu-id="1dac9-661">陣列</span><span class="sxs-lookup"><span data-stu-id="1dac9-661">Array</span></span> | <span data-ttu-id="1dac9-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="1dac9-662">["three"]</span></span> |
| <span data-ttu-id="1dac9-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-663">stringOutput</span></span> | <span data-ttu-id="1dac9-664">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-664">String</span></span> | <span data-ttu-id="1dac9-665">two three</span><span class="sxs-lookup"><span data-stu-id="1dac9-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="1dac9-666">split</span><span class="sxs-lookup"><span data-stu-id="1dac9-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="1dac9-667">傳回包含輸入字串之子字串的字串陣列，其中的子字串已使用指定的分隔符號分隔。</span><span class="sxs-lookup"><span data-stu-id="1dac9-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-668">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-668">Parameters</span></span>

| <span data-ttu-id="1dac9-669">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-669">Parameter</span></span> | <span data-ttu-id="1dac9-670">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-670">Required</span></span> | <span data-ttu-id="1dac9-671">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-671">Type</span></span> | <span data-ttu-id="1dac9-672">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-673">inputString</span><span class="sxs-lookup"><span data-stu-id="1dac9-673">inputString</span></span> |<span data-ttu-id="1dac9-674">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-674">Yes</span></span> |<span data-ttu-id="1dac9-675">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-675">string</span></span> |<span data-ttu-id="1dac9-676">要分割的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-676">The string to split.</span></span> |
| <span data-ttu-id="1dac9-677">分隔符號</span><span class="sxs-lookup"><span data-stu-id="1dac9-677">delimiter</span></span> |<span data-ttu-id="1dac9-678">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-678">Yes</span></span> |<span data-ttu-id="1dac9-679">字串或字串陣列</span><span class="sxs-lookup"><span data-stu-id="1dac9-679">string or array of strings</span></span> |<span data-ttu-id="1dac9-680">用於分割字串的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="1dac9-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-681">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-681">Return value</span></span>

<span data-ttu-id="1dac9-682">字串的陣列。</span><span class="sxs-lookup"><span data-stu-id="1dac9-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-683">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-683">Examples</span></span>

<span data-ttu-id="1dac9-684">下列範例會分割輸入字串，所使用的分割字元為逗號或分號。</span><span class="sxs-lookup"><span data-stu-id="1dac9-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="1dac9-685">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-686">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-686">Name</span></span> | <span data-ttu-id="1dac9-687">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-687">Type</span></span> | <span data-ttu-id="1dac9-688">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-689">firstOutput</span></span> | <span data-ttu-id="1dac9-690">陣列</span><span class="sxs-lookup"><span data-stu-id="1dac9-690">Array</span></span> | <span data-ttu-id="1dac9-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="1dac9-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="1dac9-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-692">secondOutput</span></span> | <span data-ttu-id="1dac9-693">陣列</span><span class="sxs-lookup"><span data-stu-id="1dac9-693">Array</span></span> | <span data-ttu-id="1dac9-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="1dac9-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="1dac9-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="1dac9-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="1dac9-696">判斷字串開頭是否為值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="1dac9-697">此比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-698">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-698">Parameters</span></span>

| <span data-ttu-id="1dac9-699">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-699">Parameter</span></span> | <span data-ttu-id="1dac9-700">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-700">Required</span></span> | <span data-ttu-id="1dac9-701">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-701">Type</span></span> | <span data-ttu-id="1dac9-702">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="1dac9-703">stringToSearch</span></span> |<span data-ttu-id="1dac9-704">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-704">Yes</span></span> |<span data-ttu-id="1dac9-705">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-705">string</span></span> |<span data-ttu-id="1dac9-706">其中包含要尋找之項目的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="1dac9-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="1dac9-707">stringToFind</span></span> |<span data-ttu-id="1dac9-708">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-708">Yes</span></span> |<span data-ttu-id="1dac9-709">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-709">string</span></span> |<span data-ttu-id="1dac9-710">要尋找的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-711">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-711">Return value</span></span>

<span data-ttu-id="1dac9-712">如果第一個字元或字串字元與該值相符，則傳回 **True**；否則傳回 **False**。</span><span class="sxs-lookup"><span data-stu-id="1dac9-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-713">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-713">Examples</span></span>

<span data-ttu-id="1dac9-714">下列範例顯示如何使用 startsWith 和 endsWith 函式：</span><span class="sxs-lookup"><span data-stu-id="1dac9-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="1dac9-715">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-716">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-716">Name</span></span> | <span data-ttu-id="1dac9-717">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-717">Type</span></span> | <span data-ttu-id="1dac9-718">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-719">startsTrue</span></span> | <span data-ttu-id="1dac9-720">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-720">Bool</span></span> | <span data-ttu-id="1dac9-721">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-721">True</span></span> |
| <span data-ttu-id="1dac9-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-722">startsCapTrue</span></span> | <span data-ttu-id="1dac9-723">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-723">Bool</span></span> | <span data-ttu-id="1dac9-724">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-724">True</span></span> |
| <span data-ttu-id="1dac9-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="1dac9-725">startsFalse</span></span> | <span data-ttu-id="1dac9-726">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-726">Bool</span></span> | <span data-ttu-id="1dac9-727">False</span><span class="sxs-lookup"><span data-stu-id="1dac9-727">False</span></span> |
| <span data-ttu-id="1dac9-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-728">endsTrue</span></span> | <span data-ttu-id="1dac9-729">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-729">Bool</span></span> | <span data-ttu-id="1dac9-730">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-730">True</span></span> |
| <span data-ttu-id="1dac9-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="1dac9-731">endsCapTrue</span></span> | <span data-ttu-id="1dac9-732">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-732">Bool</span></span> | <span data-ttu-id="1dac9-733">True</span><span class="sxs-lookup"><span data-stu-id="1dac9-733">True</span></span> |
| <span data-ttu-id="1dac9-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="1dac9-734">endsFalse</span></span> | <span data-ttu-id="1dac9-735">Bool</span><span class="sxs-lookup"><span data-stu-id="1dac9-735">Bool</span></span> | <span data-ttu-id="1dac9-736">False</span><span class="sxs-lookup"><span data-stu-id="1dac9-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="1dac9-737">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="1dac9-738">將指定的值轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-739">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-739">Parameters</span></span>

| <span data-ttu-id="1dac9-740">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-740">Parameter</span></span> | <span data-ttu-id="1dac9-741">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-741">Required</span></span> | <span data-ttu-id="1dac9-742">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-742">Type</span></span> | <span data-ttu-id="1dac9-743">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="1dac9-744">valueToConvert</span></span> |<span data-ttu-id="1dac9-745">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-745">Yes</span></span> | <span data-ttu-id="1dac9-746">任意</span><span class="sxs-lookup"><span data-stu-id="1dac9-746">Any</span></span> |<span data-ttu-id="1dac9-747">要轉換成字串的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-747">The value to convert to string.</span></span> <span data-ttu-id="1dac9-748">任何類型的值均可轉換，包括物件和陣列。</span><span class="sxs-lookup"><span data-stu-id="1dac9-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-749">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-749">Return value</span></span>

<span data-ttu-id="1dac9-750">轉換值的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-751">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-751">Examples</span></span>

<span data-ttu-id="1dac9-752">下列範例顯示如何將不同類型的值轉換為字串︰</span><span class="sxs-lookup"><span data-stu-id="1dac9-752">The following example shows how to convert different types of values to strings:</span></span>

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

<span data-ttu-id="1dac9-753">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-754">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-754">Name</span></span> | <span data-ttu-id="1dac9-755">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-755">Type</span></span> | <span data-ttu-id="1dac9-756">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-757">objectOutput</span></span> | <span data-ttu-id="1dac9-758">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-758">String</span></span> | <span data-ttu-id="1dac9-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="1dac9-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="1dac9-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-760">arrayOutput</span></span> | <span data-ttu-id="1dac9-761">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-761">String</span></span> | <span data-ttu-id="1dac9-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="1dac9-762">["a","b","c"]</span></span> |
| <span data-ttu-id="1dac9-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-763">intOutput</span></span> | <span data-ttu-id="1dac9-764">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-764">String</span></span> | <span data-ttu-id="1dac9-765">5</span><span class="sxs-lookup"><span data-stu-id="1dac9-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="1dac9-766">substring</span><span class="sxs-lookup"><span data-stu-id="1dac9-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="1dac9-767">傳回起始於指定字元位置的子字串，其中包含指定的字元數。</span><span class="sxs-lookup"><span data-stu-id="1dac9-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-768">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-768">Parameters</span></span>

| <span data-ttu-id="1dac9-769">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-769">Parameter</span></span> | <span data-ttu-id="1dac9-770">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-770">Required</span></span> | <span data-ttu-id="1dac9-771">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-771">Type</span></span> | <span data-ttu-id="1dac9-772">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="1dac9-773">stringToParse</span></span> |<span data-ttu-id="1dac9-774">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-774">Yes</span></span> |<span data-ttu-id="1dac9-775">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-775">string</span></span> |<span data-ttu-id="1dac9-776">要用來擷取子字串的原始字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="1dac9-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="1dac9-777">startIndex</span></span> |<span data-ttu-id="1dac9-778">否</span><span class="sxs-lookup"><span data-stu-id="1dac9-778">No</span></span> |<span data-ttu-id="1dac9-779">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-779">int</span></span> |<span data-ttu-id="1dac9-780">起始字元位置為零的子字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="1dac9-781">length</span><span class="sxs-lookup"><span data-stu-id="1dac9-781">length</span></span> |<span data-ttu-id="1dac9-782">否</span><span class="sxs-lookup"><span data-stu-id="1dac9-782">No</span></span> |<span data-ttu-id="1dac9-783">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-783">int</span></span> |<span data-ttu-id="1dac9-784">子字串的字元數。</span><span class="sxs-lookup"><span data-stu-id="1dac9-784">The number of characters for the substring.</span></span> <span data-ttu-id="1dac9-785">必須參考字串內的位置。</span><span class="sxs-lookup"><span data-stu-id="1dac9-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-786">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-786">Return value</span></span>

<span data-ttu-id="1dac9-787">子字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="1dac9-788">備註</span><span class="sxs-lookup"><span data-stu-id="1dac9-788">Remarks</span></span>

<span data-ttu-id="1dac9-789">子字串延伸超過字串的結尾時，此函式會失敗。</span><span class="sxs-lookup"><span data-stu-id="1dac9-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="1dac9-790">下列範例會失敗，並出現錯誤「索引與長度參數必須參考字串內的位置。</span><span class="sxs-lookup"><span data-stu-id="1dac9-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="1dac9-791">索引參數: '0'，長度參數: '11'，字串參數的長度: '10'。」。</span><span class="sxs-lookup"><span data-stu-id="1dac9-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="1dac9-792">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-792">Examples</span></span>

<span data-ttu-id="1dac9-793">下列範例會從參數中擷取子字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-793">The following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="1dac9-794">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-795">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-795">Name</span></span> | <span data-ttu-id="1dac9-796">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-796">Type</span></span> | <span data-ttu-id="1dac9-797">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-798">substringOutput</span></span> | <span data-ttu-id="1dac9-799">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-799">String</span></span> | <span data-ttu-id="1dac9-800">two</span><span class="sxs-lookup"><span data-stu-id="1dac9-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="1dac9-801">take</span><span class="sxs-lookup"><span data-stu-id="1dac9-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="1dac9-802">傳回由字串開頭的指定字元數目所形成的字串，或傳回由陣列開頭的指定元素數目所組成的陣列。</span><span class="sxs-lookup"><span data-stu-id="1dac9-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-803">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-803">Parameters</span></span>

| <span data-ttu-id="1dac9-804">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-804">Parameter</span></span> | <span data-ttu-id="1dac9-805">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-805">Required</span></span> | <span data-ttu-id="1dac9-806">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-806">Type</span></span> | <span data-ttu-id="1dac9-807">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="1dac9-808">originalValue</span></span> |<span data-ttu-id="1dac9-809">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-809">Yes</span></span> |<span data-ttu-id="1dac9-810">陣列或字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-810">array or string</span></span> |<span data-ttu-id="1dac9-811">要從其中擷取元素的陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="1dac9-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="1dac9-812">numberToTake</span></span> |<span data-ttu-id="1dac9-813">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-813">Yes</span></span> |<span data-ttu-id="1dac9-814">int</span><span class="sxs-lookup"><span data-stu-id="1dac9-814">int</span></span> |<span data-ttu-id="1dac9-815">要擷取的元素或字元數。</span><span class="sxs-lookup"><span data-stu-id="1dac9-815">The number of elements or characters to take.</span></span> <span data-ttu-id="1dac9-816">如果此值為 0 或更小的值，則會傳回空白陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="1dac9-817">如果此值大於給定陣列或字串的長度，則會傳回陣列或字串中的所有元素。</span><span class="sxs-lookup"><span data-stu-id="1dac9-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-818">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-818">Return value</span></span>

<span data-ttu-id="1dac9-819">陣列或字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-820">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-820">Examples</span></span>

<span data-ttu-id="1dac9-821">下列範例會從陣列中取得指定的元素數目，以及從字串中取得指定的字元數目。</span><span class="sxs-lookup"><span data-stu-id="1dac9-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="1dac9-822">上述範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-823">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-823">Name</span></span> | <span data-ttu-id="1dac9-824">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-824">Type</span></span> | <span data-ttu-id="1dac9-825">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-826">arrayOutput</span></span> | <span data-ttu-id="1dac9-827">陣列</span><span class="sxs-lookup"><span data-stu-id="1dac9-827">Array</span></span> | <span data-ttu-id="1dac9-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="1dac9-828">["one", "two"]</span></span> |
| <span data-ttu-id="1dac9-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-829">stringOutput</span></span> | <span data-ttu-id="1dac9-830">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-830">String</span></span> | <span data-ttu-id="1dac9-831">on</span><span class="sxs-lookup"><span data-stu-id="1dac9-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="1dac9-832">toLower</span><span class="sxs-lookup"><span data-stu-id="1dac9-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="1dac9-833">將指定的字串轉換為小寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-834">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-834">Parameters</span></span>

| <span data-ttu-id="1dac9-835">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-835">Parameter</span></span> | <span data-ttu-id="1dac9-836">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-836">Required</span></span> | <span data-ttu-id="1dac9-837">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-837">Type</span></span> | <span data-ttu-id="1dac9-838">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="1dac9-839">stringToChange</span></span> |<span data-ttu-id="1dac9-840">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-840">Yes</span></span> |<span data-ttu-id="1dac9-841">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-841">string</span></span> |<span data-ttu-id="1dac9-842">要轉換成小寫字母的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-843">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-843">Return value</span></span>

<span data-ttu-id="1dac9-844">字串已轉換成小寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-845">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-845">Examples</span></span>

<span data-ttu-id="1dac9-846">下列範例會將參數值轉換為小寫和大寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-846">The following example converts a parameter value to lower case and to upper case.</span></span>

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

<span data-ttu-id="1dac9-847">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-848">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-848">Name</span></span> | <span data-ttu-id="1dac9-849">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-849">Type</span></span> | <span data-ttu-id="1dac9-850">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-851">toLowerOutput</span></span> | <span data-ttu-id="1dac9-852">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-852">String</span></span> | <span data-ttu-id="1dac9-853">one two three</span><span class="sxs-lookup"><span data-stu-id="1dac9-853">one two three</span></span> |
| <span data-ttu-id="1dac9-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-854">toUpperOutput</span></span> | <span data-ttu-id="1dac9-855">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-855">String</span></span> | <span data-ttu-id="1dac9-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="1dac9-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="1dac9-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="1dac9-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="1dac9-858">將指定的字串轉換為大寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-859">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-859">Parameters</span></span>

| <span data-ttu-id="1dac9-860">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-860">Parameter</span></span> | <span data-ttu-id="1dac9-861">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-861">Required</span></span> | <span data-ttu-id="1dac9-862">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-862">Type</span></span> | <span data-ttu-id="1dac9-863">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="1dac9-864">stringToChange</span></span> |<span data-ttu-id="1dac9-865">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-865">Yes</span></span> |<span data-ttu-id="1dac9-866">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-866">string</span></span> |<span data-ttu-id="1dac9-867">要轉換成大寫字母的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-868">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-868">Return value</span></span>

<span data-ttu-id="1dac9-869">字串已轉換成大寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-870">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-870">Examples</span></span>

<span data-ttu-id="1dac9-871">下列範例會將參數值轉換為小寫和大寫。</span><span class="sxs-lookup"><span data-stu-id="1dac9-871">The following example converts a parameter value to lower case and to upper case.</span></span>

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

<span data-ttu-id="1dac9-872">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-873">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-873">Name</span></span> | <span data-ttu-id="1dac9-874">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-874">Type</span></span> | <span data-ttu-id="1dac9-875">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-876">toLowerOutput</span></span> | <span data-ttu-id="1dac9-877">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-877">String</span></span> | <span data-ttu-id="1dac9-878">one two three</span><span class="sxs-lookup"><span data-stu-id="1dac9-878">one two three</span></span> |
| <span data-ttu-id="1dac9-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-879">toUpperOutput</span></span> | <span data-ttu-id="1dac9-880">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-880">String</span></span> | <span data-ttu-id="1dac9-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="1dac9-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="1dac9-882">修剪</span><span class="sxs-lookup"><span data-stu-id="1dac9-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="1dac9-883">從指定的字串中移除所有開頭和尾端空白字元。</span><span class="sxs-lookup"><span data-stu-id="1dac9-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-884">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-884">Parameters</span></span>

| <span data-ttu-id="1dac9-885">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-885">Parameter</span></span> | <span data-ttu-id="1dac9-886">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-886">Required</span></span> | <span data-ttu-id="1dac9-887">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-887">Type</span></span> | <span data-ttu-id="1dac9-888">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="1dac9-889">stringToTrim</span></span> |<span data-ttu-id="1dac9-890">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-890">Yes</span></span> |<span data-ttu-id="1dac9-891">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-891">string</span></span> |<span data-ttu-id="1dac9-892">要修剪的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-893">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-893">Return value</span></span>

<span data-ttu-id="1dac9-894">沒有開頭和尾端空白字元的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-895">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-895">Examples</span></span>

<span data-ttu-id="1dac9-896">下列範例會修剪參數的空白字元。</span><span class="sxs-lookup"><span data-stu-id="1dac9-896">The following example trims the white-space characters from the parameter.</span></span>

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

<span data-ttu-id="1dac9-897">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-898">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-898">Name</span></span> | <span data-ttu-id="1dac9-899">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-899">Type</span></span> | <span data-ttu-id="1dac9-900">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-901">傳回</span><span class="sxs-lookup"><span data-stu-id="1dac9-901">return</span></span> | <span data-ttu-id="1dac9-902">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-902">String</span></span> | <span data-ttu-id="1dac9-903">one two three</span><span class="sxs-lookup"><span data-stu-id="1dac9-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="1dac9-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="1dac9-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="1dac9-905">根據當作參數提供的值，建立具決定性的雜湊字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="1dac9-906">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-906">Parameters</span></span>

| <span data-ttu-id="1dac9-907">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-907">Parameter</span></span> | <span data-ttu-id="1dac9-908">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-908">Required</span></span> | <span data-ttu-id="1dac9-909">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-909">Type</span></span> | <span data-ttu-id="1dac9-910">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-911">baseString</span><span class="sxs-lookup"><span data-stu-id="1dac9-911">baseString</span></span> |<span data-ttu-id="1dac9-912">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-912">Yes</span></span> |<span data-ttu-id="1dac9-913">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-913">string</span></span> |<span data-ttu-id="1dac9-914">雜湊函式中用來建立唯一字串的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="1dac9-915">視需要，也會使用其他參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-915">additional parameters as needed</span></span> |<span data-ttu-id="1dac9-916">否</span><span class="sxs-lookup"><span data-stu-id="1dac9-916">No</span></span> |<span data-ttu-id="1dac9-917">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-917">string</span></span> |<span data-ttu-id="1dac9-918">您可以視需要新增多個字串，來建立指定唯一性層級的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="1dac9-919">備註</span><span class="sxs-lookup"><span data-stu-id="1dac9-919">Remarks</span></span>

<span data-ttu-id="1dac9-920">當您需要建立資源的唯一名稱時，這個函式很有幫助。</span><span class="sxs-lookup"><span data-stu-id="1dac9-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="1dac9-921">您提供限制結果唯一性範圍的參數值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="1dac9-922">您可以指定名稱對於訂用帳戶、資源群組或部署是否唯一。</span><span class="sxs-lookup"><span data-stu-id="1dac9-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="1dac9-923">傳回的值不是隨機字串，而是雜湊函式的結果。</span><span class="sxs-lookup"><span data-stu-id="1dac9-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="1dac9-924">傳回的值為 13 個字元長。</span><span class="sxs-lookup"><span data-stu-id="1dac9-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="1dac9-925">它不是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="1dac9-925">It is not globally unique.</span></span> <span data-ttu-id="1dac9-926">建議您將值與來自命名慣例的前置詞結合，建立有意義的名稱。</span><span class="sxs-lookup"><span data-stu-id="1dac9-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="1dac9-927">下列範例顯示傳回值的格式。</span><span class="sxs-lookup"><span data-stu-id="1dac9-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="1dac9-928">依提供的參數而改變的實際值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="1dac9-929">下列範例顯示如何使用 uniqueString 來建立常用層級的唯一值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="1dac9-930">在訂用帳戶範圍內是唯一</span><span class="sxs-lookup"><span data-stu-id="1dac9-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="1dac9-931">在資源群組範圍內是唯一</span><span class="sxs-lookup"><span data-stu-id="1dac9-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="1dac9-932">在資源群組的部署範圍內是唯一</span><span class="sxs-lookup"><span data-stu-id="1dac9-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="1dac9-933">下列範例顯示如何根據您的資源群組建立儲存體帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="1dac9-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="1dac9-934">在資源群組內，如果名稱是以相同方式建構，就不是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="1dac9-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="1dac9-935">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-935">Return value</span></span>

<span data-ttu-id="1dac9-936">包含 13 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-937">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-937">Examples</span></span>

<span data-ttu-id="1dac9-938">下列範例會從 uniquestring 傳回結果：</span><span class="sxs-lookup"><span data-stu-id="1dac9-938">The following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="1dac9-939">uri</span><span class="sxs-lookup"><span data-stu-id="1dac9-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="1dac9-940">藉由結合 baseUri 和 relativeUri 字串建立絕對 URI。</span><span class="sxs-lookup"><span data-stu-id="1dac9-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-941">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-941">Parameters</span></span>

| <span data-ttu-id="1dac9-942">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-942">Parameter</span></span> | <span data-ttu-id="1dac9-943">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-943">Required</span></span> | <span data-ttu-id="1dac9-944">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-944">Type</span></span> | <span data-ttu-id="1dac9-945">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="1dac9-946">baseUri</span></span> |<span data-ttu-id="1dac9-947">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-947">Yes</span></span> |<span data-ttu-id="1dac9-948">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-948">string</span></span> |<span data-ttu-id="1dac9-949">基底 uri 的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-949">The base uri string.</span></span> |
| <span data-ttu-id="1dac9-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="1dac9-950">relativeUri</span></span> |<span data-ttu-id="1dac9-951">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-951">Yes</span></span> |<span data-ttu-id="1dac9-952">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-952">string</span></span> |<span data-ttu-id="1dac9-953">要加入至基底 uri 字串的相對 uri 字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="1dac9-954">**baseUri** 參數的值可包含特定檔案，但在建構 URI 時只會使用基底路徑。</span><span class="sxs-lookup"><span data-stu-id="1dac9-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="1dac9-955">例如，將 `http://contoso.com/resources/azuredeploy.json` 作為 baseUri 參數傳遞時，會產生 `http://contoso.com/resources/` 的基底 URI。</span><span class="sxs-lookup"><span data-stu-id="1dac9-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="1dac9-956">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-956">Return value</span></span>

<span data-ttu-id="1dac9-957">字串，代表基底和相對值的絕對 URI。</span><span class="sxs-lookup"><span data-stu-id="1dac9-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-958">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-958">Examples</span></span>

<span data-ttu-id="1dac9-959">下列範例顯示如何根據上層範本的值建構巢狀範本的連結。</span><span class="sxs-lookup"><span data-stu-id="1dac9-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="1dac9-960">下列範例顯示如何使用 uri、uriComponent 和 uriComponentToString：</span><span class="sxs-lookup"><span data-stu-id="1dac9-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="1dac9-961">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-962">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-962">Name</span></span> | <span data-ttu-id="1dac9-963">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-963">Type</span></span> | <span data-ttu-id="1dac9-964">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-965">uriOutput</span></span> | <span data-ttu-id="1dac9-966">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-966">String</span></span> | <span data-ttu-id="1dac9-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="1dac9-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-968">componentOutput</span></span> | <span data-ttu-id="1dac9-969">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-969">String</span></span> | <span data-ttu-id="1dac9-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="1dac9-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-971">toStringOutput</span></span> | <span data-ttu-id="1dac9-972">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-972">String</span></span> | <span data-ttu-id="1dac9-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="1dac9-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="1dac9-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="1dac9-975">將 URI 編碼。</span><span class="sxs-lookup"><span data-stu-id="1dac9-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-976">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-976">Parameters</span></span>

| <span data-ttu-id="1dac9-977">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-977">Parameter</span></span> | <span data-ttu-id="1dac9-978">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-978">Required</span></span> | <span data-ttu-id="1dac9-979">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-979">Type</span></span> | <span data-ttu-id="1dac9-980">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="1dac9-981">stringToEncode</span></span> |<span data-ttu-id="1dac9-982">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-982">Yes</span></span> |<span data-ttu-id="1dac9-983">字串</span><span class="sxs-lookup"><span data-stu-id="1dac9-983">string</span></span> |<span data-ttu-id="1dac9-984">要編碼的值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-985">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-985">Return value</span></span>

<span data-ttu-id="1dac9-986">URI 編碼值的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-987">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-987">Examples</span></span>

<span data-ttu-id="1dac9-988">下列範例顯示如何使用 uri、uriComponent 和 uriComponentToString：</span><span class="sxs-lookup"><span data-stu-id="1dac9-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="1dac9-989">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-990">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-990">Name</span></span> | <span data-ttu-id="1dac9-991">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-991">Type</span></span> | <span data-ttu-id="1dac9-992">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-993">uriOutput</span></span> | <span data-ttu-id="1dac9-994">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-994">String</span></span> | <span data-ttu-id="1dac9-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="1dac9-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-996">componentOutput</span></span> | <span data-ttu-id="1dac9-997">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-997">String</span></span> | <span data-ttu-id="1dac9-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="1dac9-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-999">toStringOutput</span></span> | <span data-ttu-id="1dac9-1000">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-1000">String</span></span> | <span data-ttu-id="1dac9-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="1dac9-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="1dac9-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="1dac9-1003">傳回 URI 編碼值的字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="1dac9-1004">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-1004">Parameters</span></span>

| <span data-ttu-id="1dac9-1005">參數</span><span class="sxs-lookup"><span data-stu-id="1dac9-1005">Parameter</span></span> | <span data-ttu-id="1dac9-1006">必要</span><span class="sxs-lookup"><span data-stu-id="1dac9-1006">Required</span></span> | <span data-ttu-id="1dac9-1007">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-1007">Type</span></span> | <span data-ttu-id="1dac9-1008">說明</span><span class="sxs-lookup"><span data-stu-id="1dac9-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="1dac9-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="1dac9-1009">uriEncodedString</span></span> |<span data-ttu-id="1dac9-1010">是</span><span class="sxs-lookup"><span data-stu-id="1dac9-1010">Yes</span></span> |<span data-ttu-id="1dac9-1011">string</span><span class="sxs-lookup"><span data-stu-id="1dac9-1011">string</span></span> |<span data-ttu-id="1dac9-1012">要轉換為字串的 URI 編碼值。</span><span class="sxs-lookup"><span data-stu-id="1dac9-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="1dac9-1013">傳回值</span><span class="sxs-lookup"><span data-stu-id="1dac9-1013">Return value</span></span>

<span data-ttu-id="1dac9-1014">URI 編碼值的解碼字串。</span><span class="sxs-lookup"><span data-stu-id="1dac9-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="1dac9-1015">範例</span><span class="sxs-lookup"><span data-stu-id="1dac9-1015">Examples</span></span>

<span data-ttu-id="1dac9-1016">下列範例顯示如何使用 uri、uriComponent 和 uriComponentToString：</span><span class="sxs-lookup"><span data-stu-id="1dac9-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="1dac9-1017">先前範例中具有預設值的輸出如下：</span><span class="sxs-lookup"><span data-stu-id="1dac9-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="1dac9-1018">名稱</span><span class="sxs-lookup"><span data-stu-id="1dac9-1018">Name</span></span> | <span data-ttu-id="1dac9-1019">類型</span><span class="sxs-lookup"><span data-stu-id="1dac9-1019">Type</span></span> | <span data-ttu-id="1dac9-1020">值</span><span class="sxs-lookup"><span data-stu-id="1dac9-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="1dac9-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-1021">uriOutput</span></span> | <span data-ttu-id="1dac9-1022">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-1022">String</span></span> | <span data-ttu-id="1dac9-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="1dac9-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-1024">componentOutput</span></span> | <span data-ttu-id="1dac9-1025">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-1025">String</span></span> | <span data-ttu-id="1dac9-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="1dac9-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="1dac9-1027">toStringOutput</span></span> | <span data-ttu-id="1dac9-1028">String</span><span class="sxs-lookup"><span data-stu-id="1dac9-1028">String</span></span> | <span data-ttu-id="1dac9-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1dac9-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1dac9-1030">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1dac9-1030">Next steps</span></span>
* <span data-ttu-id="1dac9-1031">如需有關 Azure Resource Manager 範本中各區段的說明，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="1dac9-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="1dac9-1032">若要合併多個範本，請參閱[透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="1dac9-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="1dac9-1033">若要依指定的次數重複建立資源類型，請參閱 [在 Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="1dac9-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="1dac9-1034">若要了解如何部署已建立的範本，請參閱[使用 Azure Resource Manager 範本部署應用程式](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="1dac9-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

