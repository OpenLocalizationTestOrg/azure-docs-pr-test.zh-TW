---
title: "Azure 受管理的應用程式建立 UI 定義函式 | Microsoft Docs"
description: "描述建構 Azure 受管理應用程式的 UI 定義時要使用的函式"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 62ee10eb8e6f33cc4d828cf01b405c846bef8aa4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="22884-103">CreateUiDefinition 函式</span><span class="sxs-lookup"><span data-stu-id="22884-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="22884-104">本節包含 CreateUiDefinition 所有支援的函式的簽章。</span><span class="sxs-lookup"><span data-stu-id="22884-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="22884-105">若要使用函式，請使用方括弧括住宣告。</span><span class="sxs-lookup"><span data-stu-id="22884-105">To use a function, surround the declaration with square brackets.</span></span> <span data-ttu-id="22884-106">例如：</span><span class="sxs-lookup"><span data-stu-id="22884-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="22884-107">您可以參考字串和其他函式做為函式的參數，但必須以單引號括住字串。</span><span class="sxs-lookup"><span data-stu-id="22884-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="22884-108">例如：</span><span class="sxs-lookup"><span data-stu-id="22884-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="22884-109">如果適用，您可以使用點運算子參考函式輸出的屬性。</span><span class="sxs-lookup"><span data-stu-id="22884-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span></span> <span data-ttu-id="22884-110">例如：</span><span class="sxs-lookup"><span data-stu-id="22884-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="22884-111">參考函式</span><span class="sxs-lookup"><span data-stu-id="22884-111">Referencing functions</span></span>
<span data-ttu-id="22884-112">這些函式可以用來參考屬性的輸出或 CreateUiDefinition 的內容。</span><span class="sxs-lookup"><span data-stu-id="22884-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="22884-113">basics</span><span class="sxs-lookup"><span data-stu-id="22884-113">basics</span></span>
<span data-ttu-id="22884-114">傳回在 Basics 步驟中定義之元素的輸出值。</span><span class="sxs-lookup"><span data-stu-id="22884-114">Returns the output values of an element that is defined in the Basics step.</span></span>

<span data-ttu-id="22884-115">下列範例會傳回 Basics 步驟中名為 `foo` 之元素的輸出︰</span><span class="sxs-lookup"><span data-stu-id="22884-115">The following example returns the output of the element named `foo` in the Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="22884-116">steps</span><span class="sxs-lookup"><span data-stu-id="22884-116">steps</span></span>
<span data-ttu-id="22884-117">傳回在指定步驟中定義之元素的輸出值。</span><span class="sxs-lookup"><span data-stu-id="22884-117">Returns the output values of an element that is defined in the specified step.</span></span> <span data-ttu-id="22884-118">若要取得 Basics 步驟中元素的輸出值，請改用 `basics()`。</span><span class="sxs-lookup"><span data-stu-id="22884-118">To get the output values of elements in the Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="22884-119">下列範例會傳回名為 `foo` 之步驟中，名為 `bar` 之元素的輸出︰</span><span class="sxs-lookup"><span data-stu-id="22884-119">The following example returns the output of the element named `bar` in the step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="22884-120">location</span><span class="sxs-lookup"><span data-stu-id="22884-120">location</span></span>
<span data-ttu-id="22884-121">傳回在 Basics 步驟或目前內容中選取的位置。</span><span class="sxs-lookup"><span data-stu-id="22884-121">Returns the location selected in the Basics step or the current context.</span></span>

<span data-ttu-id="22884-122">下列範例可能會傳回 `"westus"`：</span><span class="sxs-lookup"><span data-stu-id="22884-122">The following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="22884-123">字串函數</span><span class="sxs-lookup"><span data-stu-id="22884-123">String functions</span></span>
<span data-ttu-id="22884-124">這些函式只能搭配 JSON 字串使用。</span><span class="sxs-lookup"><span data-stu-id="22884-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="22884-125">concat</span><span class="sxs-lookup"><span data-stu-id="22884-125">concat</span></span>
<span data-ttu-id="22884-126">串連一或多個字串。</span><span class="sxs-lookup"><span data-stu-id="22884-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="22884-127">例如，如果 `element1` 的輸出值為 `"bar"`，則此範例會傳回字串 `"foobar!"`：</span><span class="sxs-lookup"><span data-stu-id="22884-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="22884-128">substring</span><span class="sxs-lookup"><span data-stu-id="22884-128">substring</span></span>
<span data-ttu-id="22884-129">傳回指定字串的子字串。</span><span class="sxs-lookup"><span data-stu-id="22884-129">Returns the substring of the specified string.</span></span> <span data-ttu-id="22884-130">子字串從指定的索引處開始，而且有指定的長度。</span><span class="sxs-lookup"><span data-stu-id="22884-130">The substring starts at the specified index and has the specified length.</span></span>

<span data-ttu-id="22884-131">下列範例會傳回 `"ftw"`：</span><span class="sxs-lookup"><span data-stu-id="22884-131">The following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="22884-132">取代</span><span class="sxs-lookup"><span data-stu-id="22884-132">replace</span></span>
<span data-ttu-id="22884-133">傳回將目前字串中所有指定的字串取代成另一個字串的字串。</span><span class="sxs-lookup"><span data-stu-id="22884-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span></span>

<span data-ttu-id="22884-134">下列範例會傳回 `"Everything is awesome!"`：</span><span class="sxs-lookup"><span data-stu-id="22884-134">The following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="22884-135">GUID</span><span class="sxs-lookup"><span data-stu-id="22884-135">guid</span></span>
<span data-ttu-id="22884-136">產生全域唯一字串 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="22884-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="22884-137">下列範例可能會傳回 `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`：</span><span class="sxs-lookup"><span data-stu-id="22884-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="22884-138">toLower</span><span class="sxs-lookup"><span data-stu-id="22884-138">toLower</span></span>
<span data-ttu-id="22884-139">傳回轉換成小寫的字串。</span><span class="sxs-lookup"><span data-stu-id="22884-139">Returns a string converted to lowercase.</span></span>

<span data-ttu-id="22884-140">下列範例會傳回 `"foobar"`：</span><span class="sxs-lookup"><span data-stu-id="22884-140">The following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="22884-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="22884-141">toUpper</span></span>
<span data-ttu-id="22884-142">傳回轉換成大寫的字串。</span><span class="sxs-lookup"><span data-stu-id="22884-142">Returns a string converted to uppercase.</span></span>

<span data-ttu-id="22884-143">下列範例會傳回 `"FOOBAR"`：</span><span class="sxs-lookup"><span data-stu-id="22884-143">The following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="22884-144">集合函式</span><span class="sxs-lookup"><span data-stu-id="22884-144">Collection functions</span></span>
<span data-ttu-id="22884-145">這些函式可以搭配集合使用，例如 JSON 字串、陣列和物件。</span><span class="sxs-lookup"><span data-stu-id="22884-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="22884-146">contains</span><span class="sxs-lookup"><span data-stu-id="22884-146">contains</span></span>
<span data-ttu-id="22884-147">如果字串包含指定的子字串、陣列包含指定的值，或是物件包含指定的索引鍵，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="22884-148">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="22884-148">Example 1: string</span></span>
<span data-ttu-id="22884-149">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-149">The following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="22884-150">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="22884-150">Example 2: array</span></span>
<span data-ttu-id="22884-151">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="22884-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="22884-152">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-152">The following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="22884-153">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="22884-153">Example 3: object</span></span>
<span data-ttu-id="22884-154">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="22884-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="22884-155">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-155">The following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="22884-156">length</span><span class="sxs-lookup"><span data-stu-id="22884-156">length</span></span>
<span data-ttu-id="22884-157">傳回字串中的字元數目、陣列中的值數目或物件中的索引鍵數目。</span><span class="sxs-lookup"><span data-stu-id="22884-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="22884-158">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="22884-158">Example 1: string</span></span>
<span data-ttu-id="22884-159">下列範例會傳回 `6`：</span><span class="sxs-lookup"><span data-stu-id="22884-159">The following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="22884-160">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="22884-160">Example 2: array</span></span>
<span data-ttu-id="22884-161">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="22884-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="22884-162">下列範例會傳回 `3`：</span><span class="sxs-lookup"><span data-stu-id="22884-162">The following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="22884-163">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="22884-163">Example 3: object</span></span>
<span data-ttu-id="22884-164">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="22884-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="22884-165">下列範例會傳回 `2`：</span><span class="sxs-lookup"><span data-stu-id="22884-165">The following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="22884-166">empty</span><span class="sxs-lookup"><span data-stu-id="22884-166">empty</span></span>
<span data-ttu-id="22884-167">如果字串、陣列或物件為 null 或空白，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-167">Returns `true` if the string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="22884-168">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="22884-168">Example 1: string</span></span>
<span data-ttu-id="22884-169">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-169">The following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="22884-170">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="22884-170">Example 2: array</span></span>
<span data-ttu-id="22884-171">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="22884-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="22884-172">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-172">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="22884-173">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="22884-173">Example 3: object</span></span>
<span data-ttu-id="22884-174">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="22884-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="22884-175">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-175">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="22884-176">範例 4：null 和未定義</span><span class="sxs-lookup"><span data-stu-id="22884-176">Example 4: null and undefined</span></span>
<span data-ttu-id="22884-177">假設 `element1` 為 `null` 或未定義。</span><span class="sxs-lookup"><span data-stu-id="22884-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="22884-178">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-178">The following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="22884-179">first</span><span class="sxs-lookup"><span data-stu-id="22884-179">first</span></span>
<span data-ttu-id="22884-180">傳回指定字串的第一個字元、指定陣列的第一個值，或指定物件的第一個索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="22884-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="22884-181">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="22884-181">Example 1: string</span></span>
<span data-ttu-id="22884-182">下列範例會傳回 `"f"`：</span><span class="sxs-lookup"><span data-stu-id="22884-182">The following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="22884-183">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="22884-183">Example 2: array</span></span>
<span data-ttu-id="22884-184">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="22884-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="22884-185">下列範例會傳回 `1`：</span><span class="sxs-lookup"><span data-stu-id="22884-185">The following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="22884-186">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="22884-186">Example 3: object</span></span>
<span data-ttu-id="22884-187">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="22884-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="22884-188">下列範例會傳回 `{"key1": "foobar"}`：</span><span class="sxs-lookup"><span data-stu-id="22884-188">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="22884-189">last</span><span class="sxs-lookup"><span data-stu-id="22884-189">last</span></span>
<span data-ttu-id="22884-190">傳回指定字串的最後一個字元、指定陣列的最後一個值，或指定物件的最後一個索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="22884-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="22884-191">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="22884-191">Example 1: string</span></span>
<span data-ttu-id="22884-192">下列範例會傳回 `"r"`：</span><span class="sxs-lookup"><span data-stu-id="22884-192">The following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="22884-193">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="22884-193">Example 2: array</span></span>
<span data-ttu-id="22884-194">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="22884-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="22884-195">下列範例會傳回 `2`：</span><span class="sxs-lookup"><span data-stu-id="22884-195">The following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="22884-196">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="22884-196">Example 3: object</span></span>
<span data-ttu-id="22884-197">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="22884-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="22884-198">下列範例會傳回 `{"key2": "raboof"}`：</span><span class="sxs-lookup"><span data-stu-id="22884-198">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="22884-199">take</span><span class="sxs-lookup"><span data-stu-id="22884-199">take</span></span>
<span data-ttu-id="22884-200">傳回從字串開頭指定數目的連續字元、從陣列開頭指定數目的連續值，或從物件開頭指定數目的連續索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="22884-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="22884-201">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="22884-201">Example 1: string</span></span>
<span data-ttu-id="22884-202">下列範例會傳回 `"foo"`：</span><span class="sxs-lookup"><span data-stu-id="22884-202">The following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="22884-203">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="22884-203">Example 2: array</span></span>
<span data-ttu-id="22884-204">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="22884-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="22884-205">下列範例會傳回 `[1, 2]`：</span><span class="sxs-lookup"><span data-stu-id="22884-205">The following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="22884-206">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="22884-206">Example 3: object</span></span>
<span data-ttu-id="22884-207">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="22884-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="22884-208">下列範例會傳回 `{"key1": "foobar"}`：</span><span class="sxs-lookup"><span data-stu-id="22884-208">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="22884-209">skip</span><span class="sxs-lookup"><span data-stu-id="22884-209">skip</span></span>
<span data-ttu-id="22884-210">略過集合中指定數目的元素，然後傳回其餘的元素。</span><span class="sxs-lookup"><span data-stu-id="22884-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="22884-211">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="22884-211">Example 1: string</span></span>
<span data-ttu-id="22884-212">下列範例會傳回 `"bar"`：</span><span class="sxs-lookup"><span data-stu-id="22884-212">The following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="22884-213">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="22884-213">Example 2: array</span></span>
<span data-ttu-id="22884-214">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="22884-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="22884-215">下列範例會傳回 `[3]`：</span><span class="sxs-lookup"><span data-stu-id="22884-215">The following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="22884-216">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="22884-216">Example 3: object</span></span>
<span data-ttu-id="22884-217">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="22884-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="22884-218">下列範例會傳回 `{"key2": "raboof"}`：</span><span class="sxs-lookup"><span data-stu-id="22884-218">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="22884-219">邏輯函式</span><span class="sxs-lookup"><span data-stu-id="22884-219">Logical functions</span></span>
<span data-ttu-id="22884-220">這些函式可在條件中使用。</span><span class="sxs-lookup"><span data-stu-id="22884-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="22884-221">有些函式可能不支援所有 JSON 資料類型。</span><span class="sxs-lookup"><span data-stu-id="22884-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="22884-222">equals</span><span class="sxs-lookup"><span data-stu-id="22884-222">equals</span></span>
<span data-ttu-id="22884-223">如果這兩個參數有相同的類型和值，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-223">Returns `true` if both parameters have the same type and value.</span></span> <span data-ttu-id="22884-224">此函式支援所有 JSON 資料類型。</span><span class="sxs-lookup"><span data-stu-id="22884-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="22884-225">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-225">The following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="22884-226">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-226">The following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="22884-227">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-227">The following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="22884-228">less</span><span class="sxs-lookup"><span data-stu-id="22884-228">less</span></span>
<span data-ttu-id="22884-229">如果第一個參數小於第二個參數，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-229">Returns `true` if the first parameter is strictly less than the second parameter.</span></span> <span data-ttu-id="22884-230">此函式只支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="22884-231">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-231">The following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="22884-232">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-232">The following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="22884-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="22884-233">lessOrEquals</span></span>
<span data-ttu-id="22884-234">如果第一個參數小於或等於第二個參數，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span></span> <span data-ttu-id="22884-235">此函式只支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="22884-236">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-236">The following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="22884-237">greater</span><span class="sxs-lookup"><span data-stu-id="22884-237">greater</span></span>
<span data-ttu-id="22884-238">如果第一個參數大於第二個參數，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span></span> <span data-ttu-id="22884-239">此函式只支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="22884-240">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-240">The following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="22884-241">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-241">The following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="22884-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="22884-242">greaterOrEquals</span></span>
<span data-ttu-id="22884-243">如果第一個參數大於或等於第二個參數，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span></span> <span data-ttu-id="22884-244">此函式只支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="22884-245">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-245">The following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="22884-246">和</span><span class="sxs-lookup"><span data-stu-id="22884-246">and</span></span>
<span data-ttu-id="22884-247">如果所有參數都評估為 `true`，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-247">Returns `true` if all the parameters evaluate to `true`.</span></span> <span data-ttu-id="22884-248">此函式只支援布林值類型的兩個或多個參數。</span><span class="sxs-lookup"><span data-stu-id="22884-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="22884-249">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-249">The following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="22884-250">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-250">The following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="22884-251">或</span><span class="sxs-lookup"><span data-stu-id="22884-251">or</span></span>
<span data-ttu-id="22884-252">如果至少一個參數評估為 `true`，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-252">Returns `true` if at least one of the parameters evaluates to `true`.</span></span> <span data-ttu-id="22884-253">此函式只支援布林值類型的兩個或多個參數。</span><span class="sxs-lookup"><span data-stu-id="22884-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="22884-254">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-254">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="22884-255">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-255">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="22884-256">否</span><span class="sxs-lookup"><span data-stu-id="22884-256">not</span></span>
<span data-ttu-id="22884-257">如果參數評估為 `false`，則傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-257">Returns `true` if the parameter evaluates to `false`.</span></span> <span data-ttu-id="22884-258">此函式只支援布林值類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="22884-259">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-259">The following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="22884-260">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-260">The following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="22884-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="22884-261">coalesce</span></span>
<span data-ttu-id="22884-262">傳回第一個非 null 參數的值。</span><span class="sxs-lookup"><span data-stu-id="22884-262">Returns the value of the first non-null parameter.</span></span> <span data-ttu-id="22884-263">此函式支援所有 JSON 資料類型。</span><span class="sxs-lookup"><span data-stu-id="22884-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="22884-264">假設 `element1` 和 `element2` 為未定義。</span><span class="sxs-lookup"><span data-stu-id="22884-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="22884-265">下列範例會傳回 `"foobar"`：</span><span class="sxs-lookup"><span data-stu-id="22884-265">The following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="22884-266">轉換函式</span><span class="sxs-lookup"><span data-stu-id="22884-266">Conversion functions</span></span>
<span data-ttu-id="22884-267">這些函式可用來轉換 JSON 資料類型與編碼之間的值。</span><span class="sxs-lookup"><span data-stu-id="22884-267">These functions can be used to convert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="22884-268">int</span><span class="sxs-lookup"><span data-stu-id="22884-268">int</span></span>
<span data-ttu-id="22884-269">將參數轉換成整數。</span><span class="sxs-lookup"><span data-stu-id="22884-269">Converts the parameter to an integer.</span></span> <span data-ttu-id="22884-270">此函式支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="22884-271">下列範例會傳回 `1`：</span><span class="sxs-lookup"><span data-stu-id="22884-271">The following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="22884-272">下列範例會傳回 `2`：</span><span class="sxs-lookup"><span data-stu-id="22884-272">The following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="22884-273">float</span><span class="sxs-lookup"><span data-stu-id="22884-273">float</span></span>
<span data-ttu-id="22884-274">將參數轉換成浮點數。</span><span class="sxs-lookup"><span data-stu-id="22884-274">Converts the parameter to a floating-point.</span></span> <span data-ttu-id="22884-275">此函式支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="22884-276">下列範例會傳回 `1.0`：</span><span class="sxs-lookup"><span data-stu-id="22884-276">The following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="22884-277">下列範例會傳回 `2.9`：</span><span class="sxs-lookup"><span data-stu-id="22884-277">The following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="22884-278">字串</span><span class="sxs-lookup"><span data-stu-id="22884-278">string</span></span>
<span data-ttu-id="22884-279">將參數轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="22884-279">Converts the parameter to a string.</span></span> <span data-ttu-id="22884-280">此函式支援所有 JSON 資料類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="22884-281">下列範例會傳回 `"1"`：</span><span class="sxs-lookup"><span data-stu-id="22884-281">The following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="22884-282">下列範例會傳回 `"2.9"`：</span><span class="sxs-lookup"><span data-stu-id="22884-282">The following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="22884-283">下列範例會傳回 `"[1,2,3]"`：</span><span class="sxs-lookup"><span data-stu-id="22884-283">The following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="22884-284">下列範例會傳回 `"{"foo":"bar"}"`：</span><span class="sxs-lookup"><span data-stu-id="22884-284">The following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="22884-285">布林</span><span class="sxs-lookup"><span data-stu-id="22884-285">bool</span></span>
<span data-ttu-id="22884-286">將參數轉換成布林值。</span><span class="sxs-lookup"><span data-stu-id="22884-286">Converts the parameter to a Boolean.</span></span> <span data-ttu-id="22884-287">此函式支援數值、字串和布林值類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="22884-288">類似於 JavaScript 中的布林值，`0` 或 `'false'` 以外的任何值都會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="22884-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="22884-289">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-289">The following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="22884-290">下列範例會傳回 `false`：</span><span class="sxs-lookup"><span data-stu-id="22884-290">The following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="22884-291">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-291">The following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="22884-292">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-292">The following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="22884-293">parse</span><span class="sxs-lookup"><span data-stu-id="22884-293">parse</span></span>
<span data-ttu-id="22884-294">將參數轉換成原生類型。</span><span class="sxs-lookup"><span data-stu-id="22884-294">Converts the parameter to a native type.</span></span> <span data-ttu-id="22884-295">換句話說，此函式與 `string()` 相反。</span><span class="sxs-lookup"><span data-stu-id="22884-295">In other words, this function is the inverse of `string()`.</span></span> <span data-ttu-id="22884-296">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="22884-297">下列範例會傳回 `1`：</span><span class="sxs-lookup"><span data-stu-id="22884-297">The following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="22884-298">下列範例會傳回 `true`：</span><span class="sxs-lookup"><span data-stu-id="22884-298">The following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="22884-299">下列範例會傳回 `[1,2,3]`：</span><span class="sxs-lookup"><span data-stu-id="22884-299">The following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="22884-300">下列範例會傳回 `{"foo":"bar"}`：</span><span class="sxs-lookup"><span data-stu-id="22884-300">The following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="22884-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="22884-301">encodeBase64</span></span>
<span data-ttu-id="22884-302">將參數編碼為 base-64 編碼字串。</span><span class="sxs-lookup"><span data-stu-id="22884-302">Encodes the parameter to a base-64 encoded string.</span></span> <span data-ttu-id="22884-303">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="22884-304">下列範例會傳回 `"Zm9vYmFy"`：</span><span class="sxs-lookup"><span data-stu-id="22884-304">The following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="22884-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="22884-305">decodeBase64</span></span>
<span data-ttu-id="22884-306">將參數從 base-64 編碼字串解碼。</span><span class="sxs-lookup"><span data-stu-id="22884-306">Decodes the parameter from a base-64 encoded string.</span></span> <span data-ttu-id="22884-307">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="22884-308">下列範例會傳回 `"foobar"`：</span><span class="sxs-lookup"><span data-stu-id="22884-308">The following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="22884-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="22884-309">encodeUriComponent</span></span>
<span data-ttu-id="22884-310">將參數編碼為 URL 編碼字串。</span><span class="sxs-lookup"><span data-stu-id="22884-310">Encodes the parameter to a URL encoded string.</span></span> <span data-ttu-id="22884-311">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="22884-312">下列範例會傳回 `"https%3A%2F%2Fportal.azure.com%2F"`：</span><span class="sxs-lookup"><span data-stu-id="22884-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="22884-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="22884-313">decodeUriComponent</span></span>
<span data-ttu-id="22884-314">將參數從 URL 編碼字串解碼。</span><span class="sxs-lookup"><span data-stu-id="22884-314">Decodes the parameter from a URL encoded string.</span></span> <span data-ttu-id="22884-315">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="22884-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="22884-316">下列範例會傳回 `"https://portal.azure.com/"`：</span><span class="sxs-lookup"><span data-stu-id="22884-316">The following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="22884-317">數學函式</span><span class="sxs-lookup"><span data-stu-id="22884-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="22884-318">add</span><span class="sxs-lookup"><span data-stu-id="22884-318">add</span></span>
<span data-ttu-id="22884-319">將兩個數字相加，並傳回結果。</span><span class="sxs-lookup"><span data-stu-id="22884-319">Adds two numbers, and returns the result.</span></span>

<span data-ttu-id="22884-320">下列範例會傳回 `3`：</span><span class="sxs-lookup"><span data-stu-id="22884-320">The following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="22884-321">sub</span><span class="sxs-lookup"><span data-stu-id="22884-321">sub</span></span>
<span data-ttu-id="22884-322">將第一個數字減去第二個數字，並傳回結果。</span><span class="sxs-lookup"><span data-stu-id="22884-322">Subtracts the second number from the first number, and returns the result.</span></span>

<span data-ttu-id="22884-323">下列範例會傳回 `1`：</span><span class="sxs-lookup"><span data-stu-id="22884-323">The following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="22884-324">mul</span><span class="sxs-lookup"><span data-stu-id="22884-324">mul</span></span>
<span data-ttu-id="22884-325">將兩個數字相乘，並傳回結果。</span><span class="sxs-lookup"><span data-stu-id="22884-325">Multiplies two numbers, and returns the result.</span></span>

<span data-ttu-id="22884-326">下列範例會傳回 `6`：</span><span class="sxs-lookup"><span data-stu-id="22884-326">The following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="22884-327">div</span><span class="sxs-lookup"><span data-stu-id="22884-327">div</span></span>
<span data-ttu-id="22884-328">將第一個數字除以第二個數字，並傳回結果。</span><span class="sxs-lookup"><span data-stu-id="22884-328">Divides the first number by the second number, and returns the result.</span></span> <span data-ttu-id="22884-329">結果永遠是整數。</span><span class="sxs-lookup"><span data-stu-id="22884-329">The result is always an integer.</span></span>

<span data-ttu-id="22884-330">下列範例會傳回 `2`：</span><span class="sxs-lookup"><span data-stu-id="22884-330">The following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="22884-331">mod</span><span class="sxs-lookup"><span data-stu-id="22884-331">mod</span></span>
<span data-ttu-id="22884-332">將第一個數字除以第二個數字，並傳回餘數。</span><span class="sxs-lookup"><span data-stu-id="22884-332">Divides the first number by the second number, and returns the remainder.</span></span>

<span data-ttu-id="22884-333">下列範例會傳回 `0`：</span><span class="sxs-lookup"><span data-stu-id="22884-333">The following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="22884-334">下列範例會傳回 `2`：</span><span class="sxs-lookup"><span data-stu-id="22884-334">The following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="22884-335">min</span><span class="sxs-lookup"><span data-stu-id="22884-335">min</span></span>
<span data-ttu-id="22884-336">傳回兩個數字中較小的數字。</span><span class="sxs-lookup"><span data-stu-id="22884-336">Returns the small of the two numbers.</span></span>

<span data-ttu-id="22884-337">下列範例會傳回 `1`：</span><span class="sxs-lookup"><span data-stu-id="22884-337">The following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="22884-338">max</span><span class="sxs-lookup"><span data-stu-id="22884-338">max</span></span>
<span data-ttu-id="22884-339">傳回兩個數字中較大的數字。</span><span class="sxs-lookup"><span data-stu-id="22884-339">Returns the larger of the two numbers.</span></span>

<span data-ttu-id="22884-340">下列範例會傳回 `2`：</span><span class="sxs-lookup"><span data-stu-id="22884-340">The following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="22884-341">range</span><span class="sxs-lookup"><span data-stu-id="22884-341">range</span></span>
<span data-ttu-id="22884-342">產生指定範圍內的整數序列。</span><span class="sxs-lookup"><span data-stu-id="22884-342">Generates a sequence of integral numbers within the specified range.</span></span>

<span data-ttu-id="22884-343">下列範例會傳回 `[1,2,3]`：</span><span class="sxs-lookup"><span data-stu-id="22884-343">The following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="22884-344">rand</span><span class="sxs-lookup"><span data-stu-id="22884-344">rand</span></span>
<span data-ttu-id="22884-345">產生指定範圍內的隨機整數。</span><span class="sxs-lookup"><span data-stu-id="22884-345">Returns a random integral number within the specified range.</span></span> <span data-ttu-id="22884-346">此函式不會產生密碼編譯安全的隨機數字。</span><span class="sxs-lookup"><span data-stu-id="22884-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="22884-347">下列範例可能會傳回 `42`：</span><span class="sxs-lookup"><span data-stu-id="22884-347">The following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="22884-348">floor</span><span class="sxs-lookup"><span data-stu-id="22884-348">floor</span></span>
<span data-ttu-id="22884-349">傳回小於或等於指定數字的最大整數。</span><span class="sxs-lookup"><span data-stu-id="22884-349">Returns the largest integer less than or equal to the specified number.</span></span>

<span data-ttu-id="22884-350">下列範例會傳回 `3`：</span><span class="sxs-lookup"><span data-stu-id="22884-350">The following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="22884-351">ceil</span><span class="sxs-lookup"><span data-stu-id="22884-351">ceil</span></span>
<span data-ttu-id="22884-352">傳回大於或等於指定數字的最小整數。</span><span class="sxs-lookup"><span data-stu-id="22884-352">Returns the largest integer greater than or equal to the specified number.</span></span>

<span data-ttu-id="22884-353">下列範例會傳回 `4`：</span><span class="sxs-lookup"><span data-stu-id="22884-353">The following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="22884-354">日期函式</span><span class="sxs-lookup"><span data-stu-id="22884-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="22884-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="22884-355">utcNow</span></span>
<span data-ttu-id="22884-356">傳回本機電腦上目前日期和時間之 ISO 8601 格式的字串。</span><span class="sxs-lookup"><span data-stu-id="22884-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span></span>

<span data-ttu-id="22884-357">下列範例可能會傳回 `"1990-12-31T23:59:59.000Z"`：</span><span class="sxs-lookup"><span data-stu-id="22884-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="22884-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="22884-358">addSeconds</span></span>
<span data-ttu-id="22884-359">將指定的時間戳記加上整數秒數。</span><span class="sxs-lookup"><span data-stu-id="22884-359">Adds an integral number of seconds to the specified timestamp.</span></span>

<span data-ttu-id="22884-360">下列範例會傳回 `"1991-01-01T00:00:00.000Z"`：</span><span class="sxs-lookup"><span data-stu-id="22884-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="22884-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="22884-361">addMinutes</span></span>
<span data-ttu-id="22884-362">將指定的時間戳記加上整數分鐘數。</span><span class="sxs-lookup"><span data-stu-id="22884-362">Adds an integral number of minutes to the specified timestamp.</span></span>

<span data-ttu-id="22884-363">下列範例會傳回 `"1991-01-01T00:00:59.000Z"`：</span><span class="sxs-lookup"><span data-stu-id="22884-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="22884-364">addHours</span><span class="sxs-lookup"><span data-stu-id="22884-364">addHours</span></span>
<span data-ttu-id="22884-365">將指定的時間戳記加上整數小時數。</span><span class="sxs-lookup"><span data-stu-id="22884-365">Adds an integral number of hours to the specified timestamp.</span></span>

<span data-ttu-id="22884-366">下列範例會傳回 `"1991-01-01T00:59:59.000Z"`：</span><span class="sxs-lookup"><span data-stu-id="22884-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="22884-367">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22884-367">Next steps</span></span>
* <span data-ttu-id="22884-368">如需 Azure Resource Manager 的簡介，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="22884-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

