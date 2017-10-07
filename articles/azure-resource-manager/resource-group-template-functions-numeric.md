---
title: "aaaAzure 資源管理員範本函式-數值 |Microsoft 文件"
description: "描述 Azure Resource Manager 範本 toowork 中的 hello 函式 toouse 數字。"
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="e5e48-103">Azure Resource Manager 範本的數值函式</span><span class="sxs-lookup"><span data-stu-id="e5e48-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="e5e48-104">資源管理員提供 hello 遵循使用整數的功能：</span><span class="sxs-lookup"><span data-stu-id="e5e48-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="e5e48-105">新增</span><span class="sxs-lookup"><span data-stu-id="e5e48-105">add</span></span>](#add)
* [<span data-ttu-id="e5e48-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="e5e48-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="e5e48-107">div</span><span class="sxs-lookup"><span data-stu-id="e5e48-107">div</span></span>](#div)
* [<span data-ttu-id="e5e48-108">float</span><span class="sxs-lookup"><span data-stu-id="e5e48-108">float</span></span>](#float)
* [<span data-ttu-id="e5e48-109">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-109">int</span></span>](#int)
* [<span data-ttu-id="e5e48-110">min</span><span class="sxs-lookup"><span data-stu-id="e5e48-110">min</span></span>](#min)
* [<span data-ttu-id="e5e48-111">max</span><span class="sxs-lookup"><span data-stu-id="e5e48-111">max</span></span>](#max)
* [<span data-ttu-id="e5e48-112">mod</span><span class="sxs-lookup"><span data-stu-id="e5e48-112">mod</span></span>](#mod)
* [<span data-ttu-id="e5e48-113">mul</span><span class="sxs-lookup"><span data-stu-id="e5e48-113">mul</span></span>](#mul)
* [<span data-ttu-id="e5e48-114">sub</span><span class="sxs-lookup"><span data-stu-id="e5e48-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="e5e48-115">新增</span><span class="sxs-lookup"><span data-stu-id="e5e48-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="e5e48-116">傳回 hello hello 兩個提供整數相加的總和。</span><span class="sxs-lookup"><span data-stu-id="e5e48-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-117">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-117">Parameters</span></span>

| <span data-ttu-id="e5e48-118">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-118">Parameter</span></span> | <span data-ttu-id="e5e48-119">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-119">Required</span></span> | <span data-ttu-id="e5e48-120">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-120">Type</span></span> | <span data-ttu-id="e5e48-121">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="e5e48-122">operand1</span><span class="sxs-lookup"><span data-stu-id="e5e48-122">operand1</span></span> |<span data-ttu-id="e5e48-123">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-123">Yes</span></span> |<span data-ttu-id="e5e48-124">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-124">int</span></span> |<span data-ttu-id="e5e48-125">第一個數字 tooadd。</span><span class="sxs-lookup"><span data-stu-id="e5e48-125">First number tooadd.</span></span> |
|<span data-ttu-id="e5e48-126">operand2</span><span class="sxs-lookup"><span data-stu-id="e5e48-126">operand2</span></span> |<span data-ttu-id="e5e48-127">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-127">Yes</span></span> |<span data-ttu-id="e5e48-128">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-128">int</span></span> |<span data-ttu-id="e5e48-129">第二個數值 tooadd。</span><span class="sxs-lookup"><span data-stu-id="e5e48-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-130">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-130">Return value</span></span>

<span data-ttu-id="e5e48-131">包含 hello 參數的 hello 總和的整數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-132">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-132">Example</span></span>

<span data-ttu-id="e5e48-133">下列範例中的 hello 新增兩個參數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="e5e48-134">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="e5e48-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="e5e48-135">名稱</span><span class="sxs-lookup"><span data-stu-id="e5e48-135">Name</span></span> | <span data-ttu-id="e5e48-136">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-136">Type</span></span> | <span data-ttu-id="e5e48-137">值</span><span class="sxs-lookup"><span data-stu-id="e5e48-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e5e48-138">addResult</span><span class="sxs-lookup"><span data-stu-id="e5e48-138">addResult</span></span> | <span data-ttu-id="e5e48-139">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-139">Int</span></span> | <span data-ttu-id="e5e48-140">8</span><span class="sxs-lookup"><span data-stu-id="e5e48-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="e5e48-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="e5e48-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="e5e48-142">傳回 hello 反覆項目迴圈的索引。</span><span class="sxs-lookup"><span data-stu-id="e5e48-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="e5e48-143">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-143">Parameters</span></span>

| <span data-ttu-id="e5e48-144">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-144">Parameter</span></span> | <span data-ttu-id="e5e48-145">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-145">Required</span></span> | <span data-ttu-id="e5e48-146">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-146">Type</span></span> | <span data-ttu-id="e5e48-147">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-148">loopName</span><span class="sxs-lookup"><span data-stu-id="e5e48-148">loopName</span></span> | <span data-ttu-id="e5e48-149">否</span><span class="sxs-lookup"><span data-stu-id="e5e48-149">No</span></span> | <span data-ttu-id="e5e48-150">字串</span><span class="sxs-lookup"><span data-stu-id="e5e48-150">string</span></span> | <span data-ttu-id="e5e48-151">hello hello 迴圈的名稱取得 hello 反覆項目。</span><span class="sxs-lookup"><span data-stu-id="e5e48-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="e5e48-152">Offset</span><span class="sxs-lookup"><span data-stu-id="e5e48-152">offset</span></span> |<span data-ttu-id="e5e48-153">否</span><span class="sxs-lookup"><span data-stu-id="e5e48-153">No</span></span> |<span data-ttu-id="e5e48-154">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-154">int</span></span> |<span data-ttu-id="e5e48-155">hello 號碼 tooadd toohello 以零為起始的反覆項目值。</span><span class="sxs-lookup"><span data-stu-id="e5e48-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="e5e48-156">備註</span><span class="sxs-lookup"><span data-stu-id="e5e48-156">Remarks</span></span>

<span data-ttu-id="e5e48-157">這個函式一律搭配 **copy** 物件使用。</span><span class="sxs-lookup"><span data-stu-id="e5e48-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="e5e48-158">如果未不提供任何值，如**位移**，會傳回 hello 目前反覆項目值。</span><span class="sxs-lookup"><span data-stu-id="e5e48-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="e5e48-159">hello 反覆項目值從零開始。</span><span class="sxs-lookup"><span data-stu-id="e5e48-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="e5e48-160">hello **loopName**屬性可讓您 toospecify 是否 copyIndex tooa 資源反覆項目或屬性反覆項目參考。</span><span class="sxs-lookup"><span data-stu-id="e5e48-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="e5e48-161">如果未不提供任何值，如**loopName**，會使用 hello 目前資源類型反覆項目。</span><span class="sxs-lookup"><span data-stu-id="e5e48-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="e5e48-162">逐一查看屬性時，請提供 **loopName** 的值。</span><span class="sxs-lookup"><span data-stu-id="e5e48-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="e5e48-163">如需如何使用 **copyIndex**的完整範例，請參閱 [在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="e5e48-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-164">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-164">Example</span></span>

<span data-ttu-id="e5e48-165">hello 下列範例會顯示複製迴圈和 hello 索引值包含在 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="e5e48-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="e5e48-166">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-166">Return value</span></span>

<span data-ttu-id="e5e48-167">整數，代表 hello hello 反覆項目目前的索引。</span><span class="sxs-lookup"><span data-stu-id="e5e48-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="e5e48-168">div</span><span class="sxs-lookup"><span data-stu-id="e5e48-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="e5e48-169">傳回 hello hello 兩個提供整數的整數除法。</span><span class="sxs-lookup"><span data-stu-id="e5e48-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-170">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-170">Parameters</span></span>

| <span data-ttu-id="e5e48-171">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-171">Parameter</span></span> | <span data-ttu-id="e5e48-172">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-172">Required</span></span> | <span data-ttu-id="e5e48-173">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-173">Type</span></span> | <span data-ttu-id="e5e48-174">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-175">operand1</span><span class="sxs-lookup"><span data-stu-id="e5e48-175">operand1</span></span> |<span data-ttu-id="e5e48-176">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-176">Yes</span></span> |<span data-ttu-id="e5e48-177">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-177">int</span></span> |<span data-ttu-id="e5e48-178">hello 分割的數目。</span><span class="sxs-lookup"><span data-stu-id="e5e48-178">hello number being divided.</span></span> |
| <span data-ttu-id="e5e48-179">operand2</span><span class="sxs-lookup"><span data-stu-id="e5e48-179">operand2</span></span> |<span data-ttu-id="e5e48-180">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-180">Yes</span></span> |<span data-ttu-id="e5e48-181">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-181">int</span></span> |<span data-ttu-id="e5e48-182">是使用的 toodivide hello 數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-182">hello number that is used toodivide.</span></span> <span data-ttu-id="e5e48-183">不能為 0。</span><span class="sxs-lookup"><span data-stu-id="e5e48-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-184">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-184">Return value</span></span>

<span data-ttu-id="e5e48-185">代表 hello 除整數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-186">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-186">Example</span></span>

<span data-ttu-id="e5e48-187">下列範例中的 hello 除以另一個參數的一個參數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-187">hello following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="e5e48-188">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="e5e48-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="e5e48-189">名稱</span><span class="sxs-lookup"><span data-stu-id="e5e48-189">Name</span></span> | <span data-ttu-id="e5e48-190">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-190">Type</span></span> | <span data-ttu-id="e5e48-191">值</span><span class="sxs-lookup"><span data-stu-id="e5e48-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e5e48-192">divResult</span><span class="sxs-lookup"><span data-stu-id="e5e48-192">divResult</span></span> | <span data-ttu-id="e5e48-193">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-193">Int</span></span> | <span data-ttu-id="e5e48-194">2</span><span class="sxs-lookup"><span data-stu-id="e5e48-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="e5e48-195">float</span><span class="sxs-lookup"><span data-stu-id="e5e48-195">float</span></span>
`float(arg1)`

<span data-ttu-id="e5e48-196">將轉換 hello 值 tooa 浮點數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="e5e48-197">將自訂參數傳遞 tooan 應用程式，例如邏輯應用程式時，只會使用這個函數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-198">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-198">Parameters</span></span>

| <span data-ttu-id="e5e48-199">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-199">Parameter</span></span> | <span data-ttu-id="e5e48-200">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-200">Required</span></span> | <span data-ttu-id="e5e48-201">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-201">Type</span></span> | <span data-ttu-id="e5e48-202">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-203">arg1</span><span class="sxs-lookup"><span data-stu-id="e5e48-203">arg1</span></span> |<span data-ttu-id="e5e48-204">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-204">Yes</span></span> |<span data-ttu-id="e5e48-205">字串或整數</span><span class="sxs-lookup"><span data-stu-id="e5e48-205">string or int</span></span> |<span data-ttu-id="e5e48-206">hello 值 tooconvert tooa 浮點數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-207">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-207">Return value</span></span>
<span data-ttu-id="e5e48-208">浮點數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-209">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-209">Example</span></span>

<span data-ttu-id="e5e48-210">hello 下列範例顯示如何 toouse float toopass 參數 tooa 邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="e5e48-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="e5e48-211">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="e5e48-212">將轉換 hello tooan 指定的值的整數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-213">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-213">Parameters</span></span>

| <span data-ttu-id="e5e48-214">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-214">Parameter</span></span> | <span data-ttu-id="e5e48-215">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-215">Required</span></span> | <span data-ttu-id="e5e48-216">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-216">Type</span></span> | <span data-ttu-id="e5e48-217">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="e5e48-218">valueToConvert</span></span> |<span data-ttu-id="e5e48-219">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-219">Yes</span></span> |<span data-ttu-id="e5e48-220">字串或整數</span><span class="sxs-lookup"><span data-stu-id="e5e48-220">string or int</span></span> |<span data-ttu-id="e5e48-221">hello 值 tooconvert tooan 整數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-222">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-222">Return value</span></span>

<span data-ttu-id="e5e48-223">Hello 轉換值的整數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-224">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-224">Example</span></span>

<span data-ttu-id="e5e48-225">hello 下列範例會將轉換 hello 使用者提供參數值 toointeger。</span><span class="sxs-lookup"><span data-stu-id="e5e48-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="e5e48-226">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="e5e48-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="e5e48-227">名稱</span><span class="sxs-lookup"><span data-stu-id="e5e48-227">Name</span></span> | <span data-ttu-id="e5e48-228">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-228">Type</span></span> | <span data-ttu-id="e5e48-229">值</span><span class="sxs-lookup"><span data-stu-id="e5e48-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e5e48-230">intResult</span><span class="sxs-lookup"><span data-stu-id="e5e48-230">intResult</span></span> | <span data-ttu-id="e5e48-231">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-231">Int</span></span> | <span data-ttu-id="e5e48-232">4</span><span class="sxs-lookup"><span data-stu-id="e5e48-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="e5e48-233">Min</span><span class="sxs-lookup"><span data-stu-id="e5e48-233">min</span></span>
`min (arg1)`

<span data-ttu-id="e5e48-234">傳回 hello 從整數的陣列或以逗號分隔的整數清單的最小值。</span><span class="sxs-lookup"><span data-stu-id="e5e48-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-235">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-235">Parameters</span></span>

| <span data-ttu-id="e5e48-236">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-236">Parameter</span></span> | <span data-ttu-id="e5e48-237">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-237">Required</span></span> | <span data-ttu-id="e5e48-238">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-238">Type</span></span> | <span data-ttu-id="e5e48-239">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-240">arg1</span><span class="sxs-lookup"><span data-stu-id="e5e48-240">arg1</span></span> |<span data-ttu-id="e5e48-241">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-241">Yes</span></span> |<span data-ttu-id="e5e48-242">整數的陣列，或以逗號分隔的整數清單</span><span class="sxs-lookup"><span data-stu-id="e5e48-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="e5e48-243">hello 集合 tooget hello 最小值。</span><span class="sxs-lookup"><span data-stu-id="e5e48-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-244">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-244">Return value</span></span>

<span data-ttu-id="e5e48-245">表示從 hello 集合的最小值的整數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-246">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-246">Example</span></span>

<span data-ttu-id="e5e48-247">下列範例會示範如何 hello toouse 最小值與整數清單和陣列：</span><span class="sxs-lookup"><span data-stu-id="e5e48-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="e5e48-248">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="e5e48-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="e5e48-249">名稱</span><span class="sxs-lookup"><span data-stu-id="e5e48-249">Name</span></span> | <span data-ttu-id="e5e48-250">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-250">Type</span></span> | <span data-ttu-id="e5e48-251">值</span><span class="sxs-lookup"><span data-stu-id="e5e48-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e5e48-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e5e48-252">arrayOutput</span></span> | <span data-ttu-id="e5e48-253">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-253">Int</span></span> | <span data-ttu-id="e5e48-254">0</span><span class="sxs-lookup"><span data-stu-id="e5e48-254">0</span></span> |
| <span data-ttu-id="e5e48-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="e5e48-255">intOutput</span></span> | <span data-ttu-id="e5e48-256">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-256">Int</span></span> | <span data-ttu-id="e5e48-257">0</span><span class="sxs-lookup"><span data-stu-id="e5e48-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="e5e48-258">max</span><span class="sxs-lookup"><span data-stu-id="e5e48-258">max</span></span>
`max (arg1)`

<span data-ttu-id="e5e48-259">傳回 hello 從整數的陣列或以逗號分隔的整數清單的最大值。</span><span class="sxs-lookup"><span data-stu-id="e5e48-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-260">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-260">Parameters</span></span>

| <span data-ttu-id="e5e48-261">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-261">Parameter</span></span> | <span data-ttu-id="e5e48-262">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-262">Required</span></span> | <span data-ttu-id="e5e48-263">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-263">Type</span></span> | <span data-ttu-id="e5e48-264">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-265">arg1</span><span class="sxs-lookup"><span data-stu-id="e5e48-265">arg1</span></span> |<span data-ttu-id="e5e48-266">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-266">Yes</span></span> |<span data-ttu-id="e5e48-267">整數的陣列，或以逗號分隔的整數清單</span><span class="sxs-lookup"><span data-stu-id="e5e48-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="e5e48-268">hello 集合 tooget hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="e5e48-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-269">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-269">Return value</span></span>

<span data-ttu-id="e5e48-270">整數，表示從 hello 集合 hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="e5e48-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-271">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-271">Example</span></span>

<span data-ttu-id="e5e48-272">下列範例會示範如何 hello toouse 陣列與整數清單的最大值：</span><span class="sxs-lookup"><span data-stu-id="e5e48-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="e5e48-273">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="e5e48-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="e5e48-274">名稱</span><span class="sxs-lookup"><span data-stu-id="e5e48-274">Name</span></span> | <span data-ttu-id="e5e48-275">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-275">Type</span></span> | <span data-ttu-id="e5e48-276">值</span><span class="sxs-lookup"><span data-stu-id="e5e48-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e5e48-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="e5e48-277">arrayOutput</span></span> | <span data-ttu-id="e5e48-278">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-278">Int</span></span> | <span data-ttu-id="e5e48-279">5</span><span class="sxs-lookup"><span data-stu-id="e5e48-279">5</span></span> |
| <span data-ttu-id="e5e48-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="e5e48-280">intOutput</span></span> | <span data-ttu-id="e5e48-281">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-281">Int</span></span> | <span data-ttu-id="e5e48-282">5</span><span class="sxs-lookup"><span data-stu-id="e5e48-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="e5e48-283">mod</span><span class="sxs-lookup"><span data-stu-id="e5e48-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="e5e48-284">傳回 hello hello 整數除法使用 hello 兩個提供的整數餘數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-285">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-285">Parameters</span></span>

| <span data-ttu-id="e5e48-286">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-286">Parameter</span></span> | <span data-ttu-id="e5e48-287">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-287">Required</span></span> | <span data-ttu-id="e5e48-288">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-288">Type</span></span> | <span data-ttu-id="e5e48-289">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-290">operand1</span><span class="sxs-lookup"><span data-stu-id="e5e48-290">operand1</span></span> |<span data-ttu-id="e5e48-291">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-291">Yes</span></span> |<span data-ttu-id="e5e48-292">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-292">int</span></span> |<span data-ttu-id="e5e48-293">hello 分割的數目。</span><span class="sxs-lookup"><span data-stu-id="e5e48-293">hello number being divided.</span></span> |
| <span data-ttu-id="e5e48-294">operand2</span><span class="sxs-lookup"><span data-stu-id="e5e48-294">operand2</span></span> |<span data-ttu-id="e5e48-295">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-295">Yes</span></span> |<span data-ttu-id="e5e48-296">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-296">int</span></span> |<span data-ttu-id="e5e48-297">hello 數字，其使用的 toodivide，不能為 0。</span><span class="sxs-lookup"><span data-stu-id="e5e48-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-298">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-298">Return value</span></span>
<span data-ttu-id="e5e48-299">整數代表 hello 餘數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-300">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-300">Example</span></span>

<span data-ttu-id="e5e48-301">hello 下列範例會傳回 hello 餘數由另一個參數的一個參數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="e5e48-302">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="e5e48-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="e5e48-303">名稱</span><span class="sxs-lookup"><span data-stu-id="e5e48-303">Name</span></span> | <span data-ttu-id="e5e48-304">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-304">Type</span></span> | <span data-ttu-id="e5e48-305">值</span><span class="sxs-lookup"><span data-stu-id="e5e48-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e5e48-306">modResult</span><span class="sxs-lookup"><span data-stu-id="e5e48-306">modResult</span></span> | <span data-ttu-id="e5e48-307">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-307">Int</span></span> | <span data-ttu-id="e5e48-308">1</span><span class="sxs-lookup"><span data-stu-id="e5e48-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="e5e48-309">mul</span><span class="sxs-lookup"><span data-stu-id="e5e48-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="e5e48-310">傳回 hello 乘法 hello 兩個提供的整數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-311">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-311">Parameters</span></span>

| <span data-ttu-id="e5e48-312">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-312">Parameter</span></span> | <span data-ttu-id="e5e48-313">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-313">Required</span></span> | <span data-ttu-id="e5e48-314">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-314">Type</span></span> | <span data-ttu-id="e5e48-315">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-316">operand1</span><span class="sxs-lookup"><span data-stu-id="e5e48-316">operand1</span></span> |<span data-ttu-id="e5e48-317">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-317">Yes</span></span> |<span data-ttu-id="e5e48-318">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-318">int</span></span> |<span data-ttu-id="e5e48-319">第一個數字 toomultiply。</span><span class="sxs-lookup"><span data-stu-id="e5e48-319">First number toomultiply.</span></span> |
| <span data-ttu-id="e5e48-320">operand2</span><span class="sxs-lookup"><span data-stu-id="e5e48-320">operand2</span></span> |<span data-ttu-id="e5e48-321">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-321">Yes</span></span> |<span data-ttu-id="e5e48-322">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-322">int</span></span> |<span data-ttu-id="e5e48-323">第二個數值 toomultiply。</span><span class="sxs-lookup"><span data-stu-id="e5e48-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-324">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-324">Return value</span></span>

<span data-ttu-id="e5e48-325">整數代表 hello 乘法。</span><span class="sxs-lookup"><span data-stu-id="e5e48-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-326">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-326">Example</span></span>

<span data-ttu-id="e5e48-327">下列範例中的 hello 乘上另一個參數的一個參數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="e5e48-328">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="e5e48-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="e5e48-329">名稱</span><span class="sxs-lookup"><span data-stu-id="e5e48-329">Name</span></span> | <span data-ttu-id="e5e48-330">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-330">Type</span></span> | <span data-ttu-id="e5e48-331">值</span><span class="sxs-lookup"><span data-stu-id="e5e48-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e5e48-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="e5e48-332">mulResult</span></span> | <span data-ttu-id="e5e48-333">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-333">Int</span></span> | <span data-ttu-id="e5e48-334">15</span><span class="sxs-lookup"><span data-stu-id="e5e48-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="e5e48-335">sub</span><span class="sxs-lookup"><span data-stu-id="e5e48-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="e5e48-336">傳回 hello hello 兩個提供整數的減法運算。</span><span class="sxs-lookup"><span data-stu-id="e5e48-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="e5e48-337">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-337">Parameters</span></span>

| <span data-ttu-id="e5e48-338">參數</span><span class="sxs-lookup"><span data-stu-id="e5e48-338">Parameter</span></span> | <span data-ttu-id="e5e48-339">必要</span><span class="sxs-lookup"><span data-stu-id="e5e48-339">Required</span></span> | <span data-ttu-id="e5e48-340">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-340">Type</span></span> | <span data-ttu-id="e5e48-341">說明</span><span class="sxs-lookup"><span data-stu-id="e5e48-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e5e48-342">operand1</span><span class="sxs-lookup"><span data-stu-id="e5e48-342">operand1</span></span> |<span data-ttu-id="e5e48-343">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-343">Yes</span></span> |<span data-ttu-id="e5e48-344">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-344">int</span></span> |<span data-ttu-id="e5e48-345">hello 會減去的數字。</span><span class="sxs-lookup"><span data-stu-id="e5e48-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="e5e48-346">operand2</span><span class="sxs-lookup"><span data-stu-id="e5e48-346">operand2</span></span> |<span data-ttu-id="e5e48-347">是</span><span class="sxs-lookup"><span data-stu-id="e5e48-347">Yes</span></span> |<span data-ttu-id="e5e48-348">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-348">int</span></span> |<span data-ttu-id="e5e48-349">hello 減去的數字。</span><span class="sxs-lookup"><span data-stu-id="e5e48-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="e5e48-350">傳回值</span><span class="sxs-lookup"><span data-stu-id="e5e48-350">Return value</span></span>
<span data-ttu-id="e5e48-351">整數代表 hello 減法。</span><span class="sxs-lookup"><span data-stu-id="e5e48-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="e5e48-352">範例</span><span class="sxs-lookup"><span data-stu-id="e5e48-352">Example</span></span>

<span data-ttu-id="e5e48-353">下列範例中的 hello 減去一個參數從另一個參數。</span><span class="sxs-lookup"><span data-stu-id="e5e48-353">hello following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer toosubtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="e5e48-354">hello 輸出範例與 hello 預設值是從上述 hello:</span><span class="sxs-lookup"><span data-stu-id="e5e48-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="e5e48-355">名稱</span><span class="sxs-lookup"><span data-stu-id="e5e48-355">Name</span></span> | <span data-ttu-id="e5e48-356">類型</span><span class="sxs-lookup"><span data-stu-id="e5e48-356">Type</span></span> | <span data-ttu-id="e5e48-357">值</span><span class="sxs-lookup"><span data-stu-id="e5e48-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="e5e48-358">subResult</span><span class="sxs-lookup"><span data-stu-id="e5e48-358">subResult</span></span> | <span data-ttu-id="e5e48-359">int</span><span class="sxs-lookup"><span data-stu-id="e5e48-359">Int</span></span> | <span data-ttu-id="e5e48-360">4</span><span class="sxs-lookup"><span data-stu-id="e5e48-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e5e48-361">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5e48-361">Next steps</span></span>
* <span data-ttu-id="e5e48-362">如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="e5e48-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e5e48-363">toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="e5e48-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="e5e48-364">tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="e5e48-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="e5e48-365">toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="e5e48-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

