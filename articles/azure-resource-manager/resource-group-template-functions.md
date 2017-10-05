---
title: "Resource Manager 範本函數 | Microsoft Docs"
description: "描述要在 Azure 資源管理員範本中用來擷取值、搭配字串和數字使用，並擷取部署資訊的函數。"
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
ms.openlocfilehash: 1324bed07e991e9d84cb6832afe78bdb2d3348fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="b1196-103">Azure 資源管理員範本函數</span><span class="sxs-lookup"><span data-stu-id="b1196-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="b1196-104">本主題描述您可以在Azure Resource Manager 範本中使用的所有函式。</span><span class="sxs-lookup"><span data-stu-id="b1196-104">This topic describes all the functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="b1196-105">您要在範本中新增函式，方法是分別將它們以括弧括住：`[` 和 `]`。</span><span class="sxs-lookup"><span data-stu-id="b1196-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="b1196-106">在部署期間，會評估運算式。</span><span class="sxs-lookup"><span data-stu-id="b1196-106">The expression is evaluated during deployment.</span></span> <span data-ttu-id="b1196-107">雖然是以字串常值撰寫，評估運算式的結果，可能會是不同的 JSON 類型 (例如陣列、物件或整數)。</span><span class="sxs-lookup"><span data-stu-id="b1196-107">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="b1196-108">和在 JavaScript 中相同，函式呼叫的格式為 `functionName(arg1,arg2,arg3)`。</span><span class="sxs-lookup"><span data-stu-id="b1196-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="b1196-109">您可以使用點與 [index] 運算子來參考屬性。</span><span class="sxs-lookup"><span data-stu-id="b1196-109">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="b1196-110">範本運算式不能超過 24,576 個字元。</span><span class="sxs-lookup"><span data-stu-id="b1196-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="b1196-111">範本函數和其參數不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="b1196-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="b1196-112">例如，Resource Manager 在解析 **variables('var1')** 和 **VARIABLES('VAR1')** 時，會將它們視為相同。</span><span class="sxs-lookup"><span data-stu-id="b1196-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as the same.</span></span> <span data-ttu-id="b1196-113">評估時，除非函式明確修改大小寫 (例如 toUpper 或 toLower)，否則函式將會保留大小寫。</span><span class="sxs-lookup"><span data-stu-id="b1196-113">When evaluated, unless the function expressly modifies case (such as toUpper or toLower), the function preserves the case.</span></span> <span data-ttu-id="b1196-114">特定資源類型可能有與評估函式方式無關的大小寫需求。</span><span class="sxs-lookup"><span data-stu-id="b1196-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

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

## <a name="array-and-object-functions"></a><span data-ttu-id="b1196-115">陣列和物件函式</span><span class="sxs-lookup"><span data-stu-id="b1196-115">Array and object functions</span></span>
<span data-ttu-id="b1196-116">Resource Manager 提供了幾個用來使用陣列和物件的函式。</span><span class="sxs-lookup"><span data-stu-id="b1196-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="b1196-117">array</span><span class="sxs-lookup"><span data-stu-id="b1196-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="b1196-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="b1196-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="b1196-119">concat</span><span class="sxs-lookup"><span data-stu-id="b1196-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="b1196-120">contains</span><span class="sxs-lookup"><span data-stu-id="b1196-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="b1196-121">createArray</span><span class="sxs-lookup"><span data-stu-id="b1196-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="b1196-122">empty</span><span class="sxs-lookup"><span data-stu-id="b1196-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="b1196-123">first</span><span class="sxs-lookup"><span data-stu-id="b1196-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="b1196-124">intersection</span><span class="sxs-lookup"><span data-stu-id="b1196-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="b1196-125">json</span><span class="sxs-lookup"><span data-stu-id="b1196-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="b1196-126">last</span><span class="sxs-lookup"><span data-stu-id="b1196-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="b1196-127">length</span><span class="sxs-lookup"><span data-stu-id="b1196-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="b1196-128">min</span><span class="sxs-lookup"><span data-stu-id="b1196-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="b1196-129">max</span><span class="sxs-lookup"><span data-stu-id="b1196-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="b1196-130">range</span><span class="sxs-lookup"><span data-stu-id="b1196-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="b1196-131">skip</span><span class="sxs-lookup"><span data-stu-id="b1196-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="b1196-132">take</span><span class="sxs-lookup"><span data-stu-id="b1196-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="b1196-133">union</span><span class="sxs-lookup"><span data-stu-id="b1196-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="b1196-134">比較函式</span><span class="sxs-lookup"><span data-stu-id="b1196-134">Comparison functions</span></span>
<span data-ttu-id="b1196-135">Resource Manager 提供了幾個可在範本中進行比較的函式。</span><span class="sxs-lookup"><span data-stu-id="b1196-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="b1196-136">equals</span><span class="sxs-lookup"><span data-stu-id="b1196-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="b1196-137">less</span><span class="sxs-lookup"><span data-stu-id="b1196-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="b1196-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="b1196-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="b1196-139">greater</span><span class="sxs-lookup"><span data-stu-id="b1196-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="b1196-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="b1196-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="b1196-141">部署值函式</span><span class="sxs-lookup"><span data-stu-id="b1196-141">Deployment value functions</span></span>
<span data-ttu-id="b1196-142">資源管理員提供下列函式，以從與部署相關的範本和值的區段中取得值：</span><span class="sxs-lookup"><span data-stu-id="b1196-142">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="b1196-143">部署</span><span class="sxs-lookup"><span data-stu-id="b1196-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="b1196-144">參數</span><span class="sxs-lookup"><span data-stu-id="b1196-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="b1196-145">變數</span><span class="sxs-lookup"><span data-stu-id="b1196-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

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

## <a name="logical-functions"></a><span data-ttu-id="b1196-146">邏輯函式</span><span class="sxs-lookup"><span data-stu-id="b1196-146">Logical functions</span></span>
<span data-ttu-id="b1196-147">Resource Manager 提供下列函式以使用邏輯條件：</span><span class="sxs-lookup"><span data-stu-id="b1196-147">Resource Manager provides the following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="b1196-148">and</span><span class="sxs-lookup"><span data-stu-id="b1196-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="b1196-149">bool</span><span class="sxs-lookup"><span data-stu-id="b1196-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="b1196-150">if</span><span class="sxs-lookup"><span data-stu-id="b1196-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="b1196-151">not</span><span class="sxs-lookup"><span data-stu-id="b1196-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="b1196-152">or</span><span class="sxs-lookup"><span data-stu-id="b1196-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="b1196-153">數值函式</span><span class="sxs-lookup"><span data-stu-id="b1196-153">Numeric functions</span></span>
<span data-ttu-id="b1196-154">資源管理員提供下列函式以使用整數：</span><span class="sxs-lookup"><span data-stu-id="b1196-154">Resource Manager provides the following functions for working with integers:</span></span>

* [<span data-ttu-id="b1196-155">新增</span><span class="sxs-lookup"><span data-stu-id="b1196-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="b1196-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="b1196-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="b1196-157">div</span><span class="sxs-lookup"><span data-stu-id="b1196-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="b1196-158">float</span><span class="sxs-lookup"><span data-stu-id="b1196-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="b1196-159">int</span><span class="sxs-lookup"><span data-stu-id="b1196-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="b1196-160">min</span><span class="sxs-lookup"><span data-stu-id="b1196-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="b1196-161">max</span><span class="sxs-lookup"><span data-stu-id="b1196-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="b1196-162">mod</span><span class="sxs-lookup"><span data-stu-id="b1196-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="b1196-163">mul</span><span class="sxs-lookup"><span data-stu-id="b1196-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="b1196-164">sub</span><span class="sxs-lookup"><span data-stu-id="b1196-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="b1196-165">資源函式</span><span class="sxs-lookup"><span data-stu-id="b1196-165">Resource functions</span></span>
<span data-ttu-id="b1196-166">資源管理員提供下列函式以取得資源值：</span><span class="sxs-lookup"><span data-stu-id="b1196-166">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="b1196-167">listKeys 和 list{Value}</span><span class="sxs-lookup"><span data-stu-id="b1196-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="b1196-168">提供者</span><span class="sxs-lookup"><span data-stu-id="b1196-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="b1196-169">reference</span><span class="sxs-lookup"><span data-stu-id="b1196-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="b1196-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="b1196-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="b1196-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="b1196-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="b1196-172">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b1196-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

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

## <a name="string-functions"></a><span data-ttu-id="b1196-173">字串函數</span><span class="sxs-lookup"><span data-stu-id="b1196-173">String functions</span></span>
<span data-ttu-id="b1196-174">資源管理員提供下列函式以使用字串：</span><span class="sxs-lookup"><span data-stu-id="b1196-174">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="b1196-175">base64</span><span class="sxs-lookup"><span data-stu-id="b1196-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="b1196-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="b1196-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="b1196-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="b1196-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="b1196-178">concat</span><span class="sxs-lookup"><span data-stu-id="b1196-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="b1196-179">contains</span><span class="sxs-lookup"><span data-stu-id="b1196-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="b1196-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="b1196-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="b1196-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="b1196-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="b1196-182">empty</span><span class="sxs-lookup"><span data-stu-id="b1196-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="b1196-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="b1196-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="b1196-184">first</span><span class="sxs-lookup"><span data-stu-id="b1196-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="b1196-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="b1196-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="b1196-186">last</span><span class="sxs-lookup"><span data-stu-id="b1196-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="b1196-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="b1196-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="b1196-188">length</span><span class="sxs-lookup"><span data-stu-id="b1196-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="b1196-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="b1196-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="b1196-190">replace</span><span class="sxs-lookup"><span data-stu-id="b1196-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="b1196-191">skip</span><span class="sxs-lookup"><span data-stu-id="b1196-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="b1196-192">分割</span><span class="sxs-lookup"><span data-stu-id="b1196-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="b1196-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="b1196-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="b1196-194">字串</span><span class="sxs-lookup"><span data-stu-id="b1196-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="b1196-195">substring</span><span class="sxs-lookup"><span data-stu-id="b1196-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="b1196-196">take</span><span class="sxs-lookup"><span data-stu-id="b1196-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="b1196-197">toLower</span><span class="sxs-lookup"><span data-stu-id="b1196-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="b1196-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="b1196-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="b1196-199">修剪</span><span class="sxs-lookup"><span data-stu-id="b1196-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="b1196-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="b1196-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="b1196-201">uri</span><span class="sxs-lookup"><span data-stu-id="b1196-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="b1196-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="b1196-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="b1196-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="b1196-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="b1196-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1196-204">Next steps</span></span>
* <span data-ttu-id="b1196-205">如需有關 Azure 資源管理員範本中各區段的說明，請參閱 [編寫 Azure 資源管理員範本](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="b1196-205">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="b1196-206">若要合併多個範本，請參閱 [透過 Azure 資源管理員使用連結的範本](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="b1196-206">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="b1196-207">建立資源類型時若要逐一查看指定的次數，請參閱 [在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="b1196-207">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="b1196-208">若要了解如何部署已建立的範本，請參閱[使用 Azure 資源管理員範本部署應用程式](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="b1196-208">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

