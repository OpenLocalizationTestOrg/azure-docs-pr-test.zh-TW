---
title: "aaaResource 管理員樣板函式 |Microsoft 文件"
description: "描述 hello 函式 toouse Azure Resource Manager 範本 tooretrieve 值，與字串和數字，並擷取部署的資訊。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="871bf-103">Azure 資源管理員範本函數</span><span class="sxs-lookup"><span data-stu-id="871bf-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="871bf-104">本主題描述所有您可以使用 Azure Resource Manager 範本中的 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="871bf-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="871bf-105">您要在範本中新增函式，方法是分別將它們以括弧括住：`[` 和 `]`。</span><span class="sxs-lookup"><span data-stu-id="871bf-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="871bf-106">在部署期間，會評估 hello 運算式。</span><span class="sxs-lookup"><span data-stu-id="871bf-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="871bf-107">寫入字串常值，同時 hello 運算式的評估 hello 結果可以是不同的 JSON 型別，例如陣列、 物件或整數。</span><span class="sxs-lookup"><span data-stu-id="871bf-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="871bf-108">和在 JavaScript 中相同，函式呼叫的格式為 `functionName(arg1,arg2,arg3)`。</span><span class="sxs-lookup"><span data-stu-id="871bf-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="871bf-109">您可以使用 hello 點和 [index] 運算子，以參考屬性。</span><span class="sxs-lookup"><span data-stu-id="871bf-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="871bf-110">範本運算式不能超過 24,576 個字元。</span><span class="sxs-lookup"><span data-stu-id="871bf-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="871bf-111">範本函數和其參數不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="871bf-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="871bf-112">例如，資源管理員會解析**variables('var1')**和**VARIABLES('VAR1')**為 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="871bf-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="871bf-113">評估時，除非用戶 hello 函式會修改 （例如 toUpper 或 toLower） 的情況下，hello 函式會保留 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="871bf-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="871bf-114">特定資源類型可能有與評估函式方式無關的大小寫需求。</span><span class="sxs-lookup"><span data-stu-id="871bf-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="871bf-115">陣列和物件函式</span><span class="sxs-lookup"><span data-stu-id="871bf-115">Array and object functions</span></span>
<span data-ttu-id="871bf-116">Resource Manager 提供了幾個用來使用陣列和物件的函式。</span><span class="sxs-lookup"><span data-stu-id="871bf-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="871bf-117">array</span><span class="sxs-lookup"><span data-stu-id="871bf-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="871bf-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="871bf-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="871bf-119">concat</span><span class="sxs-lookup"><span data-stu-id="871bf-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="871bf-120">contains</span><span class="sxs-lookup"><span data-stu-id="871bf-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="871bf-121">createArray</span><span class="sxs-lookup"><span data-stu-id="871bf-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="871bf-122">empty</span><span class="sxs-lookup"><span data-stu-id="871bf-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="871bf-123">first</span><span class="sxs-lookup"><span data-stu-id="871bf-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="871bf-124">intersection</span><span class="sxs-lookup"><span data-stu-id="871bf-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="871bf-125">json</span><span class="sxs-lookup"><span data-stu-id="871bf-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="871bf-126">last</span><span class="sxs-lookup"><span data-stu-id="871bf-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="871bf-127">length</span><span class="sxs-lookup"><span data-stu-id="871bf-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="871bf-128">min</span><span class="sxs-lookup"><span data-stu-id="871bf-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="871bf-129">max</span><span class="sxs-lookup"><span data-stu-id="871bf-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="871bf-130">range</span><span class="sxs-lookup"><span data-stu-id="871bf-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="871bf-131">skip</span><span class="sxs-lookup"><span data-stu-id="871bf-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="871bf-132">take</span><span class="sxs-lookup"><span data-stu-id="871bf-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="871bf-133">union</span><span class="sxs-lookup"><span data-stu-id="871bf-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="871bf-134">比較函式</span><span class="sxs-lookup"><span data-stu-id="871bf-134">Comparison functions</span></span>
<span data-ttu-id="871bf-135">Resource Manager 提供了幾個可在範本中進行比較的函式。</span><span class="sxs-lookup"><span data-stu-id="871bf-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="871bf-136">equals</span><span class="sxs-lookup"><span data-stu-id="871bf-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="871bf-137">less</span><span class="sxs-lookup"><span data-stu-id="871bf-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="871bf-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="871bf-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="871bf-139">greater</span><span class="sxs-lookup"><span data-stu-id="871bf-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="871bf-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="871bf-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="871bf-141">部署值函式</span><span class="sxs-lookup"><span data-stu-id="871bf-141">Deployment value functions</span></span>
<span data-ttu-id="871bf-142">資源管理員提供 hello 下列函數來取得從 hello 範本的區段值和值相關的 toohello 部署：</span><span class="sxs-lookup"><span data-stu-id="871bf-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="871bf-143">部署</span><span class="sxs-lookup"><span data-stu-id="871bf-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="871bf-144">參數</span><span class="sxs-lookup"><span data-stu-id="871bf-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="871bf-145">變數</span><span class="sxs-lookup"><span data-stu-id="871bf-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="871bf-146">邏輯函式</span><span class="sxs-lookup"><span data-stu-id="871bf-146">Logical functions</span></span>
<span data-ttu-id="871bf-147">資源管理員提供下列函數使用的邏輯條件的 hello:</span><span class="sxs-lookup"><span data-stu-id="871bf-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="871bf-148">and</span><span class="sxs-lookup"><span data-stu-id="871bf-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="871bf-149">bool</span><span class="sxs-lookup"><span data-stu-id="871bf-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="871bf-150">if</span><span class="sxs-lookup"><span data-stu-id="871bf-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="871bf-151">not</span><span class="sxs-lookup"><span data-stu-id="871bf-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="871bf-152">or</span><span class="sxs-lookup"><span data-stu-id="871bf-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="871bf-153">數值函式</span><span class="sxs-lookup"><span data-stu-id="871bf-153">Numeric functions</span></span>
<span data-ttu-id="871bf-154">資源管理員提供 hello 遵循使用整數的功能：</span><span class="sxs-lookup"><span data-stu-id="871bf-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="871bf-155">新增</span><span class="sxs-lookup"><span data-stu-id="871bf-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="871bf-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="871bf-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="871bf-157">div</span><span class="sxs-lookup"><span data-stu-id="871bf-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="871bf-158">float</span><span class="sxs-lookup"><span data-stu-id="871bf-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="871bf-159">int</span><span class="sxs-lookup"><span data-stu-id="871bf-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="871bf-160">min</span><span class="sxs-lookup"><span data-stu-id="871bf-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="871bf-161">max</span><span class="sxs-lookup"><span data-stu-id="871bf-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="871bf-162">mod</span><span class="sxs-lookup"><span data-stu-id="871bf-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="871bf-163">mul</span><span class="sxs-lookup"><span data-stu-id="871bf-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="871bf-164">sub</span><span class="sxs-lookup"><span data-stu-id="871bf-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="871bf-165">資源函式</span><span class="sxs-lookup"><span data-stu-id="871bf-165">Resource functions</span></span>
<span data-ttu-id="871bf-166">資源管理員提供下列函數來取得資源值 hello:</span><span class="sxs-lookup"><span data-stu-id="871bf-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="871bf-167">listKeys 和 list{Value}</span><span class="sxs-lookup"><span data-stu-id="871bf-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="871bf-168">提供者</span><span class="sxs-lookup"><span data-stu-id="871bf-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="871bf-169">reference</span><span class="sxs-lookup"><span data-stu-id="871bf-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="871bf-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="871bf-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="871bf-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="871bf-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="871bf-172">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="871bf-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="871bf-173">字串函數</span><span class="sxs-lookup"><span data-stu-id="871bf-173">String functions</span></span>
<span data-ttu-id="871bf-174">資源管理員提供下列函數使用字串 hello:</span><span class="sxs-lookup"><span data-stu-id="871bf-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="871bf-175">base64</span><span class="sxs-lookup"><span data-stu-id="871bf-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="871bf-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="871bf-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="871bf-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="871bf-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="871bf-178">concat</span><span class="sxs-lookup"><span data-stu-id="871bf-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="871bf-179">contains</span><span class="sxs-lookup"><span data-stu-id="871bf-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="871bf-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="871bf-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="871bf-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="871bf-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="871bf-182">empty</span><span class="sxs-lookup"><span data-stu-id="871bf-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="871bf-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="871bf-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="871bf-184">first</span><span class="sxs-lookup"><span data-stu-id="871bf-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="871bf-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="871bf-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="871bf-186">last</span><span class="sxs-lookup"><span data-stu-id="871bf-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="871bf-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="871bf-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="871bf-188">length</span><span class="sxs-lookup"><span data-stu-id="871bf-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="871bf-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="871bf-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="871bf-190">replace</span><span class="sxs-lookup"><span data-stu-id="871bf-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="871bf-191">skip</span><span class="sxs-lookup"><span data-stu-id="871bf-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="871bf-192">分割</span><span class="sxs-lookup"><span data-stu-id="871bf-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="871bf-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="871bf-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="871bf-194">字串</span><span class="sxs-lookup"><span data-stu-id="871bf-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="871bf-195">substring</span><span class="sxs-lookup"><span data-stu-id="871bf-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="871bf-196">take</span><span class="sxs-lookup"><span data-stu-id="871bf-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="871bf-197">toLower</span><span class="sxs-lookup"><span data-stu-id="871bf-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="871bf-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="871bf-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="871bf-199">修剪</span><span class="sxs-lookup"><span data-stu-id="871bf-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="871bf-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="871bf-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="871bf-201">uri</span><span class="sxs-lookup"><span data-stu-id="871bf-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="871bf-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="871bf-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="871bf-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="871bf-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="871bf-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="871bf-204">Next steps</span></span>
* <span data-ttu-id="871bf-205">如需 Azure Resource Manager 範本中的 hello 各節的說明，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="871bf-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="871bf-206">toomerge 多個範本，請參閱[使用連結的範本與 Azure 資源管理員](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="871bf-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="871bf-207">tooiterate 指定次數時建立的資源類型，請參閱[Azure 資源管理員中建立多個執行個體的資源](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="871bf-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="871bf-208">toosee 如何 toodeploy hello 範本建立之後，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="871bf-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

