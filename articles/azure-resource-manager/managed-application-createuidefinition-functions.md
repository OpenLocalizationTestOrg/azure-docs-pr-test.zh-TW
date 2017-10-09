---
title: "aaaAzure 受管理的應用程式建立使用者定義函式 |Microsoft 文件"
description: "描述 hello 函式 toouse 建構 Azure 受管理的應用程式的 UI 定義時"
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
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="b8928-103">CreateUiDefinition 函式</span><span class="sxs-lookup"><span data-stu-id="b8928-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="b8928-104">本章節包含所有支援的函式的 CreateUiDefinition hello 簽的章。</span><span class="sxs-lookup"><span data-stu-id="b8928-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="b8928-105">toouse 函式，範圍陳述式 hello 宣告使用方括號。</span><span class="sxs-lookup"><span data-stu-id="b8928-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="b8928-106">例如：</span><span class="sxs-lookup"><span data-stu-id="b8928-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="b8928-107">您可以參考字串和其他函式做為函式的參數，但必須以單引號括住字串。</span><span class="sxs-lookup"><span data-stu-id="b8928-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="b8928-108">例如：</span><span class="sxs-lookup"><span data-stu-id="b8928-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="b8928-109">情況適用時，您可以使用 hello 點運算子來參考的 hello 函式輸出的屬性。</span><span class="sxs-lookup"><span data-stu-id="b8928-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="b8928-110">例如：</span><span class="sxs-lookup"><span data-stu-id="b8928-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="b8928-111">參考函式</span><span class="sxs-lookup"><span data-stu-id="b8928-111">Referencing functions</span></span>
<span data-ttu-id="b8928-112">這些函式可從 hello 屬性或內容 CreateUiDefinition 使用的 tooreference 輸出。</span><span class="sxs-lookup"><span data-stu-id="b8928-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="b8928-113">basics</span><span class="sxs-lookup"><span data-stu-id="b8928-113">basics</span></span>
<span data-ttu-id="b8928-114">傳回 hello 輸出值 hello 基本概念步所定義的項目。</span><span class="sxs-lookup"><span data-stu-id="b8928-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="b8928-115">hello 下列範例會傳回名為 「 hello 」 項目 hello 輸出`foo`在 hello 基本步驟：</span><span class="sxs-lookup"><span data-stu-id="b8928-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="b8928-116">steps</span><span class="sxs-lookup"><span data-stu-id="b8928-116">steps</span></span>
<span data-ttu-id="b8928-117">傳回 hello 輸出值 hello 指定步所定義的項目。</span><span class="sxs-lookup"><span data-stu-id="b8928-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="b8928-118">tooget hello 輸出值的項目在 hello 基本步驟中，使用`basics()`改為。</span><span class="sxs-lookup"><span data-stu-id="b8928-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="b8928-119">hello 下列範例會傳回名為 「 hello 」 項目 hello 輸出`bar`在名為 hello 步驟`foo`:</span><span class="sxs-lookup"><span data-stu-id="b8928-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="b8928-120">location</span><span class="sxs-lookup"><span data-stu-id="b8928-120">location</span></span>
<span data-ttu-id="b8928-121">傳回選取 hello 基本步驟或 hello 目前內容中的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="b8928-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="b8928-122">hello 下列範例會傳回`"westus"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="b8928-123">字串函數</span><span class="sxs-lookup"><span data-stu-id="b8928-123">String functions</span></span>
<span data-ttu-id="b8928-124">這些函式只能搭配 JSON 字串使用。</span><span class="sxs-lookup"><span data-stu-id="b8928-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="b8928-125">concat</span><span class="sxs-lookup"><span data-stu-id="b8928-125">concat</span></span>
<span data-ttu-id="b8928-126">串連一或多個字串。</span><span class="sxs-lookup"><span data-stu-id="b8928-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="b8928-127">例如，如果 hello 輸出值`element1`如果`"bar"`，則此範例會傳回字串 hello `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="b8928-128">substring</span><span class="sxs-lookup"><span data-stu-id="b8928-128">substring</span></span>
<span data-ttu-id="b8928-129">傳回字串 hello 的 hello 子指定的字串。</span><span class="sxs-lookup"><span data-stu-id="b8928-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="b8928-130">hello 子字串 hello 指定索引處開始，且已 hello 指定長度。</span><span class="sxs-lookup"><span data-stu-id="b8928-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="b8928-131">hello 下列範例會傳回`"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="b8928-132">取代</span><span class="sxs-lookup"><span data-stu-id="b8928-132">replace</span></span>
<span data-ttu-id="b8928-133">傳回字串中的所有出現的 hello hello 目前字串中指定的字串會取代另一個字串。</span><span class="sxs-lookup"><span data-stu-id="b8928-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="b8928-134">hello 下列範例會傳回`"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="b8928-135">GUID</span><span class="sxs-lookup"><span data-stu-id="b8928-135">guid</span></span>
<span data-ttu-id="b8928-136">產生全域唯一字串 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="b8928-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="b8928-137">hello 下列範例會傳回`"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="b8928-138">toLower</span><span class="sxs-lookup"><span data-stu-id="b8928-138">toLower</span></span>
<span data-ttu-id="b8928-139">傳回轉換字串 toolowercase。</span><span class="sxs-lookup"><span data-stu-id="b8928-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="b8928-140">hello 下列範例會傳回`"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="b8928-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="b8928-141">toUpper</span></span>
<span data-ttu-id="b8928-142">傳回轉換字串 toouppercase。</span><span class="sxs-lookup"><span data-stu-id="b8928-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="b8928-143">hello 下列範例會傳回`"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="b8928-144">集合函式</span><span class="sxs-lookup"><span data-stu-id="b8928-144">Collection functions</span></span>
<span data-ttu-id="b8928-145">這些函式可以搭配集合使用，例如 JSON 字串、陣列和物件。</span><span class="sxs-lookup"><span data-stu-id="b8928-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="b8928-146">contains</span><span class="sxs-lookup"><span data-stu-id="b8928-146">contains</span></span>
<span data-ttu-id="b8928-147">傳回`true`如果字串包含 hello 指定子字串，包含陣列 hello 指定值，或是物件包含 hello 指定之索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b8928-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="b8928-148">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="b8928-148">Example 1: string</span></span>
<span data-ttu-id="b8928-149">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="b8928-150">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="b8928-150">Example 2: array</span></span>
<span data-ttu-id="b8928-151">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="b8928-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="b8928-152">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="b8928-153">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="b8928-153">Example 3: object</span></span>
<span data-ttu-id="b8928-154">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="b8928-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="b8928-155">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="b8928-156">length</span><span class="sxs-lookup"><span data-stu-id="b8928-156">length</span></span>
<span data-ttu-id="b8928-157">傳回字串、 在陣列中，值的 hello 數目或物件中的索引鍵的 hello 數目的 hello 的字元數。</span><span class="sxs-lookup"><span data-stu-id="b8928-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="b8928-158">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="b8928-158">Example 1: string</span></span>
<span data-ttu-id="b8928-159">hello 下列範例會傳回`6`:</span><span class="sxs-lookup"><span data-stu-id="b8928-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="b8928-160">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="b8928-160">Example 2: array</span></span>
<span data-ttu-id="b8928-161">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="b8928-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="b8928-162">hello 下列範例會傳回`3`:</span><span class="sxs-lookup"><span data-stu-id="b8928-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="b8928-163">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="b8928-163">Example 3: object</span></span>
<span data-ttu-id="b8928-164">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="b8928-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="b8928-165">hello 下列範例會傳回`2`:</span><span class="sxs-lookup"><span data-stu-id="b8928-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="b8928-166">empty</span><span class="sxs-lookup"><span data-stu-id="b8928-166">empty</span></span>
<span data-ttu-id="b8928-167">傳回`true`hello 字串、 陣列或物件為 null 或空白。</span><span class="sxs-lookup"><span data-stu-id="b8928-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="b8928-168">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="b8928-168">Example 1: string</span></span>
<span data-ttu-id="b8928-169">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="b8928-170">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="b8928-170">Example 2: array</span></span>
<span data-ttu-id="b8928-171">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="b8928-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="b8928-172">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="b8928-173">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="b8928-173">Example 3: object</span></span>
<span data-ttu-id="b8928-174">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="b8928-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="b8928-175">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="b8928-176">範例 4：null 和未定義</span><span class="sxs-lookup"><span data-stu-id="b8928-176">Example 4: null and undefined</span></span>
<span data-ttu-id="b8928-177">假設 `element1` 為 `null` 或未定義。</span><span class="sxs-lookup"><span data-stu-id="b8928-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="b8928-178">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="b8928-179">first</span><span class="sxs-lookup"><span data-stu-id="b8928-179">first</span></span>
<span data-ttu-id="b8928-180">傳回的 hello hello 第一個字元指定的字串。第一個值，指定陣列 hello;或 hello 第一個索引鍵和 hello 指定之物件的值。</span><span class="sxs-lookup"><span data-stu-id="b8928-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="b8928-181">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="b8928-181">Example 1: string</span></span>
<span data-ttu-id="b8928-182">hello 下列範例會傳回`"f"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="b8928-183">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="b8928-183">Example 2: array</span></span>
<span data-ttu-id="b8928-184">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="b8928-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="b8928-185">hello 下列範例會傳回`1`:</span><span class="sxs-lookup"><span data-stu-id="b8928-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="b8928-186">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="b8928-186">Example 3: object</span></span>
<span data-ttu-id="b8928-187">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="b8928-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="b8928-188">hello 下列範例會傳回`{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="b8928-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="b8928-189">last</span><span class="sxs-lookup"><span data-stu-id="b8928-189">last</span></span>
<span data-ttu-id="b8928-190">傳回指定的 hello 的 hello 最後一個字元字串，hello hello 指定的陣列，最後一個值或 hello 最後一個索引鍵和 hello 指定之物件的值。</span><span class="sxs-lookup"><span data-stu-id="b8928-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="b8928-191">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="b8928-191">Example 1: string</span></span>
<span data-ttu-id="b8928-192">hello 下列範例會傳回`"r"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="b8928-193">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="b8928-193">Example 2: array</span></span>
<span data-ttu-id="b8928-194">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="b8928-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="b8928-195">hello 下列範例會傳回`2`:</span><span class="sxs-lookup"><span data-stu-id="b8928-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="b8928-196">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="b8928-196">Example 3: object</span></span>
<span data-ttu-id="b8928-197">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="b8928-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="b8928-198">hello 下列範例會傳回`{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="b8928-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="b8928-199">take</span><span class="sxs-lookup"><span data-stu-id="b8928-199">take</span></span>
<span data-ttu-id="b8928-200">傳回的連續字元 hello hello 字串的開頭指定的數目、 指定從 hello 陣列的 hello 開始的連續值的數目或指定連續索引鍵和值的數目從 hello 開頭 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="b8928-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="b8928-201">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="b8928-201">Example 1: string</span></span>
<span data-ttu-id="b8928-202">hello 下列範例會傳回`"foo"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="b8928-203">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="b8928-203">Example 2: array</span></span>
<span data-ttu-id="b8928-204">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="b8928-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="b8928-205">hello 下列範例會傳回`[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="b8928-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="b8928-206">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="b8928-206">Example 3: object</span></span>
<span data-ttu-id="b8928-207">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="b8928-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="b8928-208">hello 下列範例會傳回`{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="b8928-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="b8928-209">skip</span><span class="sxs-lookup"><span data-stu-id="b8928-209">skip</span></span>
<span data-ttu-id="b8928-210">略過指定的數目的項目集合中，然後傳回其餘項 hello。</span><span class="sxs-lookup"><span data-stu-id="b8928-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="b8928-211">範例 1︰字串</span><span class="sxs-lookup"><span data-stu-id="b8928-211">Example 1: string</span></span>
<span data-ttu-id="b8928-212">hello 下列範例會傳回`"bar"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="b8928-213">範例 2︰陣列</span><span class="sxs-lookup"><span data-stu-id="b8928-213">Example 2: array</span></span>
<span data-ttu-id="b8928-214">假設 `element1` 傳回 `[1, 2, 3]`。</span><span class="sxs-lookup"><span data-stu-id="b8928-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="b8928-215">hello 下列範例會傳回`[3]`:</span><span class="sxs-lookup"><span data-stu-id="b8928-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="b8928-216">範例 3︰物件</span><span class="sxs-lookup"><span data-stu-id="b8928-216">Example 3: object</span></span>
<span data-ttu-id="b8928-217">假設 `element1` 傳回：</span><span class="sxs-lookup"><span data-stu-id="b8928-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="b8928-218">hello 下列範例會傳回`{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="b8928-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="b8928-219">邏輯函式</span><span class="sxs-lookup"><span data-stu-id="b8928-219">Logical functions</span></span>
<span data-ttu-id="b8928-220">這些函式可在條件中使用。</span><span class="sxs-lookup"><span data-stu-id="b8928-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="b8928-221">有些函式可能不支援所有 JSON 資料類型。</span><span class="sxs-lookup"><span data-stu-id="b8928-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="b8928-222">equals</span><span class="sxs-lookup"><span data-stu-id="b8928-222">equals</span></span>
<span data-ttu-id="b8928-223">傳回`true`如果這兩個參數都有相同的類型和值的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8928-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="b8928-224">此函式支援所有 JSON 資料類型。</span><span class="sxs-lookup"><span data-stu-id="b8928-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="b8928-225">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="b8928-226">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="b8928-227">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="b8928-228">less</span><span class="sxs-lookup"><span data-stu-id="b8928-228">less</span></span>
<span data-ttu-id="b8928-229">傳回`true`如果 hello 第一個參數是絕對小於 hello 第二個參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="b8928-230">此函式只支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="b8928-231">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="b8928-232">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="b8928-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="b8928-233">lessOrEquals</span></span>
<span data-ttu-id="b8928-234">傳回`true`hello 第一個參數是否小於或等於 toohello 第二個參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="b8928-235">此函式只支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="b8928-236">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="b8928-237">greater</span><span class="sxs-lookup"><span data-stu-id="b8928-237">greater</span></span>
<span data-ttu-id="b8928-238">傳回`true`hello 第一個參數是否嚴格大於 hello 第二個參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="b8928-239">此函式只支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="b8928-240">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="b8928-241">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="b8928-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="b8928-242">greaterOrEquals</span></span>
<span data-ttu-id="b8928-243">傳回`true`hello 第一個參數是否大於或等於 toohello 第二個參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="b8928-244">此函式只支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="b8928-245">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="b8928-246">和</span><span class="sxs-lookup"><span data-stu-id="b8928-246">and</span></span>
<span data-ttu-id="b8928-247">傳回`true`如果 hello 的所有參數都評估太`true`。</span><span class="sxs-lookup"><span data-stu-id="b8928-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="b8928-248">此函式只支援布林值類型的兩個或多個參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="b8928-249">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="b8928-250">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="b8928-251">或</span><span class="sxs-lookup"><span data-stu-id="b8928-251">or</span></span>
<span data-ttu-id="b8928-252">傳回`true`如果至少一個 hello 參數太評估`true`。</span><span class="sxs-lookup"><span data-stu-id="b8928-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="b8928-253">此函式只支援布林值類型的兩個或多個參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="b8928-254">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="b8928-255">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="b8928-256">否</span><span class="sxs-lookup"><span data-stu-id="b8928-256">not</span></span>
<span data-ttu-id="b8928-257">傳回`true`如果太評估 hello 參數`false`。</span><span class="sxs-lookup"><span data-stu-id="b8928-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="b8928-258">此函式只支援布林值類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="b8928-259">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="b8928-260">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="b8928-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="b8928-261">coalesce</span></span>
<span data-ttu-id="b8928-262">傳回 hello hello 第一個非 null 參數的值。</span><span class="sxs-lookup"><span data-stu-id="b8928-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="b8928-263">此函式支援所有 JSON 資料類型。</span><span class="sxs-lookup"><span data-stu-id="b8928-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="b8928-264">假設 `element1` 和 `element2` 為未定義。</span><span class="sxs-lookup"><span data-stu-id="b8928-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="b8928-265">hello 下列範例會傳回`"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="b8928-266">轉換函式</span><span class="sxs-lookup"><span data-stu-id="b8928-266">Conversion functions</span></span>
<span data-ttu-id="b8928-267">這些函式可使用的 tooconvert JSON 資料類型和編碼之間的值。</span><span class="sxs-lookup"><span data-stu-id="b8928-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="b8928-268">int</span><span class="sxs-lookup"><span data-stu-id="b8928-268">int</span></span>
<span data-ttu-id="b8928-269">Hello 參數 tooan 整數轉換。</span><span class="sxs-lookup"><span data-stu-id="b8928-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="b8928-270">此函式支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="b8928-271">hello 下列範例會傳回`1`:</span><span class="sxs-lookup"><span data-stu-id="b8928-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="b8928-272">hello 下列範例會傳回`2`:</span><span class="sxs-lookup"><span data-stu-id="b8928-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="b8928-273">float</span><span class="sxs-lookup"><span data-stu-id="b8928-273">float</span></span>
<span data-ttu-id="b8928-274">將轉換 hello 參數 tooa 浮點數。</span><span class="sxs-lookup"><span data-stu-id="b8928-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="b8928-275">此函式支援數值和字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="b8928-276">hello 下列範例會傳回`1.0`:</span><span class="sxs-lookup"><span data-stu-id="b8928-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="b8928-277">hello 下列範例會傳回`2.9`:</span><span class="sxs-lookup"><span data-stu-id="b8928-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="b8928-278">字串</span><span class="sxs-lookup"><span data-stu-id="b8928-278">string</span></span>
<span data-ttu-id="b8928-279">將 hello 參數 tooa 字串轉換。</span><span class="sxs-lookup"><span data-stu-id="b8928-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="b8928-280">此函式支援所有 JSON 資料類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="b8928-281">hello 下列範例會傳回`"1"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="b8928-282">hello 下列範例會傳回`"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="b8928-283">hello 下列範例會傳回`"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="b8928-284">hello 下列範例會傳回`"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="b8928-285">布林</span><span class="sxs-lookup"><span data-stu-id="b8928-285">bool</span></span>
<span data-ttu-id="b8928-286">將轉換 hello 參數 tooa 布林值。</span><span class="sxs-lookup"><span data-stu-id="b8928-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="b8928-287">此函式支援數值、字串和布林值類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="b8928-288">在 JavaScript 中，以外的任何值類似 tooBooleans`0`或`'false'`傳回`true`。</span><span class="sxs-lookup"><span data-stu-id="b8928-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="b8928-289">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="b8928-290">hello 下列範例會傳回`false`:</span><span class="sxs-lookup"><span data-stu-id="b8928-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="b8928-291">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="b8928-292">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="b8928-293">parse</span><span class="sxs-lookup"><span data-stu-id="b8928-293">parse</span></span>
<span data-ttu-id="b8928-294">將 hello 參數 tooa 原生類型轉換。</span><span class="sxs-lookup"><span data-stu-id="b8928-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="b8928-295">換句話說，此函式是 hello 反`string()`。</span><span class="sxs-lookup"><span data-stu-id="b8928-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="b8928-296">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="b8928-297">hello 下列範例會傳回`1`:</span><span class="sxs-lookup"><span data-stu-id="b8928-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="b8928-298">hello 下列範例會傳回`true`:</span><span class="sxs-lookup"><span data-stu-id="b8928-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="b8928-299">hello 下列範例會傳回`[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="b8928-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="b8928-300">hello 下列範例會傳回`{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="b8928-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="b8928-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="b8928-301">encodeBase64</span></span>
<span data-ttu-id="b8928-302">將編碼 hello 參數 tooa base 64 編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="b8928-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="b8928-303">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="b8928-304">hello 下列範例會傳回`"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="b8928-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="b8928-305">decodeBase64</span></span>
<span data-ttu-id="b8928-306">將解碼 hello 參數從 base 64 編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="b8928-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="b8928-307">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="b8928-308">hello 下列範例會傳回`"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="b8928-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="b8928-309">encodeUriComponent</span></span>
<span data-ttu-id="b8928-310">Hello 參數 tooa URL 編碼的字串編碼。</span><span class="sxs-lookup"><span data-stu-id="b8928-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="b8928-311">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="b8928-312">hello 下列範例會傳回`"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="b8928-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="b8928-313">decodeUriComponent</span></span>
<span data-ttu-id="b8928-314">將解碼的 URL 編碼字串 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="b8928-315">此函式只支援字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b8928-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="b8928-316">hello 下列範例會傳回`"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="b8928-317">數學函式</span><span class="sxs-lookup"><span data-stu-id="b8928-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="b8928-318">新增</span><span class="sxs-lookup"><span data-stu-id="b8928-318">add</span></span>
<span data-ttu-id="b8928-319">將兩個數字，並傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="b8928-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="b8928-320">hello 下列範例會傳回`3`:</span><span class="sxs-lookup"><span data-stu-id="b8928-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="b8928-321">sub</span><span class="sxs-lookup"><span data-stu-id="b8928-321">sub</span></span>
<span data-ttu-id="b8928-322">Hello hello 第一個數字，從第二個數字相減，並傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="b8928-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="b8928-323">hello 下列範例會傳回`1`:</span><span class="sxs-lookup"><span data-stu-id="b8928-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="b8928-324">mul</span><span class="sxs-lookup"><span data-stu-id="b8928-324">mul</span></span>
<span data-ttu-id="b8928-325">兩個數字，並傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="b8928-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="b8928-326">hello 下列範例會傳回`6`:</span><span class="sxs-lookup"><span data-stu-id="b8928-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="b8928-327">div</span><span class="sxs-lookup"><span data-stu-id="b8928-327">div</span></span>
<span data-ttu-id="b8928-328">第一個 hello hello 第二個數字，數字除以，並傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="b8928-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="b8928-329">hello 結果都是整數。</span><span class="sxs-lookup"><span data-stu-id="b8928-329">hello result is always an integer.</span></span>

<span data-ttu-id="b8928-330">hello 下列範例會傳回`2`:</span><span class="sxs-lookup"><span data-stu-id="b8928-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="b8928-331">mod</span><span class="sxs-lookup"><span data-stu-id="b8928-331">mod</span></span>
<span data-ttu-id="b8928-332">第一個 hello hello 第二個數字，數字除以，並傳回 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="b8928-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="b8928-333">hello 下列範例會傳回`0`:</span><span class="sxs-lookup"><span data-stu-id="b8928-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="b8928-334">hello 下列範例會傳回`2`:</span><span class="sxs-lookup"><span data-stu-id="b8928-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="b8928-335">Min</span><span class="sxs-lookup"><span data-stu-id="b8928-335">min</span></span>
<span data-ttu-id="b8928-336">傳回 hello hello 兩個數字的小。</span><span class="sxs-lookup"><span data-stu-id="b8928-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="b8928-337">hello 下列範例會傳回`1`:</span><span class="sxs-lookup"><span data-stu-id="b8928-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="b8928-338">max</span><span class="sxs-lookup"><span data-stu-id="b8928-338">max</span></span>
<span data-ttu-id="b8928-339">傳回 hello hello 兩個數字的較大。</span><span class="sxs-lookup"><span data-stu-id="b8928-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="b8928-340">hello 下列範例會傳回`2`:</span><span class="sxs-lookup"><span data-stu-id="b8928-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="b8928-341">range</span><span class="sxs-lookup"><span data-stu-id="b8928-341">range</span></span>
<span data-ttu-id="b8928-342">產生的整數類資料序列內 hello 的數字指定的範圍。</span><span class="sxs-lookup"><span data-stu-id="b8928-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="b8928-343">hello 下列範例會傳回`[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="b8928-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="b8928-344">rand</span><span class="sxs-lookup"><span data-stu-id="b8928-344">rand</span></span>
<span data-ttu-id="b8928-345">傳回隨機整數的數字 hello 內指定的範圍。</span><span class="sxs-lookup"><span data-stu-id="b8928-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="b8928-346">此函式不會產生密碼編譯安全的隨機數字。</span><span class="sxs-lookup"><span data-stu-id="b8928-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="b8928-347">hello 下列範例會傳回`42`:</span><span class="sxs-lookup"><span data-stu-id="b8928-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="b8928-348">floor</span><span class="sxs-lookup"><span data-stu-id="b8928-348">floor</span></span>
<span data-ttu-id="b8928-349">傳回小於或等於 hello 最大整數 toohello 指定數字。</span><span class="sxs-lookup"><span data-stu-id="b8928-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="b8928-350">hello 下列範例會傳回`3`:</span><span class="sxs-lookup"><span data-stu-id="b8928-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="b8928-351">ceil</span><span class="sxs-lookup"><span data-stu-id="b8928-351">ceil</span></span>
<span data-ttu-id="b8928-352">傳回 hello 最大的整數大於或等於 toohello 指定數字。</span><span class="sxs-lookup"><span data-stu-id="b8928-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="b8928-353">hello 下列範例會傳回`4`:</span><span class="sxs-lookup"><span data-stu-id="b8928-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="b8928-354">日期函式</span><span class="sxs-lookup"><span data-stu-id="b8928-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="b8928-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="b8928-355">utcNow</span></span>
<span data-ttu-id="b8928-356">傳回字串 hello hello 本機電腦上目前的日期和時間的 ISO 8601 格式。</span><span class="sxs-lookup"><span data-stu-id="b8928-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="b8928-357">hello 下列範例會傳回`"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="b8928-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="b8928-358">addSeconds</span></span>
<span data-ttu-id="b8928-359">將整數秒 toohello 指定時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b8928-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="b8928-360">hello 下列範例會傳回`"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="b8928-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="b8928-361">addMinutes</span></span>
<span data-ttu-id="b8928-362">將整數分鐘 toohello 指定時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b8928-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="b8928-363">hello 下列範例會傳回`"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="b8928-364">addHours</span><span class="sxs-lookup"><span data-stu-id="b8928-364">addHours</span></span>
<span data-ttu-id="b8928-365">將整數的數字的時數 toohello 指定時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b8928-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="b8928-366">hello 下列範例會傳回`"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="b8928-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="b8928-367">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8928-367">Next steps</span></span>
* <span data-ttu-id="b8928-368">如簡介 tooAzure 資源管理員，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b8928-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

