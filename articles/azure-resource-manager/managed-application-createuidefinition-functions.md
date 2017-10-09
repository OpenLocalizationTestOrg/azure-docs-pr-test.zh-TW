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
# <a name="createuidefinition-functions"></a>CreateUiDefinition 函式
本章節包含所有支援的函式的 CreateUiDefinition hello 簽的章。

toouse 函式，範圍陳述式 hello 宣告使用方括號。 例如：

```json
"[function()]"
```

您可以參考字串和其他函式做為函式的參數，但必須以單引號括住字串。 例如：

```json
"[fn1(fn2(), 'foobar')]"
```

情況適用時，您可以使用 hello 點運算子來參考的 hello 函式輸出的屬性。 例如：

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>參考函式
這些函式可從 hello 屬性或內容 CreateUiDefinition 使用的 tooreference 輸出。

### <a name="basics"></a>basics
傳回 hello 輸出值 hello 基本概念步所定義的項目。

hello 下列範例會傳回名為 「 hello 」 項目 hello 輸出`foo`在 hello 基本步驟：

```json
"[basics('foo')]"
```

### <a name="steps"></a>steps
傳回 hello 輸出值 hello 指定步所定義的項目。 tooget hello 輸出值的項目在 hello 基本步驟中，使用`basics()`改為。

hello 下列範例會傳回名為 「 hello 」 項目 hello 輸出`bar`在名為 hello 步驟`foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
傳回選取 hello 基本步驟或 hello 目前內容中的 hello 位置。

hello 下列範例會傳回`"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>字串函數
這些函式只能搭配 JSON 字串使用。

### <a name="concat"></a>concat
串連一或多個字串。

例如，如果 hello 輸出值`element1`如果`"bar"`，則此範例會傳回字串 hello `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
傳回字串 hello 的 hello 子指定的字串。 hello 子字串 hello 指定索引處開始，且已 hello 指定長度。

hello 下列範例會傳回`"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>取代
傳回字串中的所有出現的 hello hello 目前字串中指定的字串會取代另一個字串。

hello 下列範例會傳回`"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>GUID
產生全域唯一字串 (GUID)。

hello 下列範例會傳回`"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
傳回轉換字串 toolowercase。

hello 下列範例會傳回`"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
傳回轉換字串 toouppercase。

hello 下列範例會傳回`"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>集合函式
這些函式可以搭配集合使用，例如 JSON 字串、陣列和物件。

### <a name="contains"></a>contains
傳回`true`如果字串包含 hello 指定子字串，包含陣列 hello 指定值，或是物件包含 hello 指定之索引鍵。

#### <a name="example-1-string"></a>範例 1︰字串
hello 下列範例會傳回`true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>範例 2︰陣列
假設 `element1` 傳回 `[1, 2, 3]`。 hello 下列範例會傳回`false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>範例 3︰物件
假設 `element1` 傳回：

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 下列範例會傳回`true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>length
傳回字串、 在陣列中，值的 hello 數目或物件中的索引鍵的 hello 數目的 hello 的字元數。

#### <a name="example-1-string"></a>範例 1︰字串
hello 下列範例會傳回`6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>範例 2︰陣列
假設 `element1` 傳回 `[1, 2, 3]`。 hello 下列範例會傳回`3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>範例 3︰物件
假設 `element1` 傳回：

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 下列範例會傳回`2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>empty
傳回`true`hello 字串、 陣列或物件為 null 或空白。

#### <a name="example-1-string"></a>範例 1︰字串
hello 下列範例會傳回`true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>範例 2︰陣列
假設 `element1` 傳回 `[1, 2, 3]`。 hello 下列範例會傳回`false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>範例 3︰物件
假設 `element1` 傳回：

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 下列範例會傳回`false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>範例 4：null 和未定義
假設 `element1` 為 `null` 或未定義。 hello 下列範例會傳回`true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>first
傳回的 hello hello 第一個字元指定的字串。第一個值，指定陣列 hello;或 hello 第一個索引鍵和 hello 指定之物件的值。

#### <a name="example-1-string"></a>範例 1︰字串
hello 下列範例會傳回`"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>範例 2︰陣列
假設 `element1` 傳回 `[1, 2, 3]`。 hello 下列範例會傳回`1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>範例 3︰物件
假設 `element1` 傳回：

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
hello 下列範例會傳回`{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>last
傳回指定的 hello 的 hello 最後一個字元字串，hello hello 指定的陣列，最後一個值或 hello 最後一個索引鍵和 hello 指定之物件的值。

#### <a name="example-1-string"></a>範例 1︰字串
hello 下列範例會傳回`"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>範例 2︰陣列
假設 `element1` 傳回 `[1, 2, 3]`。 hello 下列範例會傳回`2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>範例 3︰物件
假設 `element1` 傳回：

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 下列範例會傳回`{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>take
傳回的連續字元 hello hello 字串的開頭指定的數目、 指定從 hello 陣列的 hello 開始的連續值的數目或指定連續索引鍵和值的數目從 hello 開頭 hello 物件。

#### <a name="example-1-string"></a>範例 1︰字串
hello 下列範例會傳回`"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>範例 2︰陣列
假設 `element1` 傳回 `[1, 2, 3]`。 hello 下列範例會傳回`[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>範例 3︰物件
假設 `element1` 傳回：

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

hello 下列範例會傳回`{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>skip
略過指定的數目的項目集合中，然後傳回其餘項 hello。

#### <a name="example-1-string"></a>範例 1︰字串
hello 下列範例會傳回`"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>範例 2︰陣列
假設 `element1` 傳回 `[1, 2, 3]`。 hello 下列範例會傳回`[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>範例 3︰物件
假設 `element1` 傳回：

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
hello 下列範例會傳回`{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>邏輯函式
這些函式可在條件中使用。 有些函式可能不支援所有 JSON 資料類型。

### <a name="equals"></a>equals
傳回`true`如果這兩個參數都有相同的類型和值的 hello。 此函式支援所有 JSON 資料類型。

hello 下列範例會傳回`true`:

```json
"[equals(0, 0)]"
```

hello 下列範例會傳回`true`:

```json
"[equals('foo', 'foo')]"
```

hello 下列範例會傳回`false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>less
傳回`true`如果 hello 第一個參數是絕對小於 hello 第二個參數。 此函式只支援數值和字串類型的參數。

hello 下列範例會傳回`true`:

```json
"[less(1, 2)]"
```

hello 下列範例會傳回`false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
傳回`true`hello 第一個參數是否小於或等於 toohello 第二個參數。 此函式只支援數值和字串類型的參數。

hello 下列範例會傳回`true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>greater
傳回`true`hello 第一個參數是否嚴格大於 hello 第二個參數。 此函式只支援數值和字串類型的參數。

hello 下列範例會傳回`false`:

```json
"[greater(1, 2)]"
```

hello 下列範例會傳回`true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
傳回`true`hello 第一個參數是否大於或等於 toohello 第二個參數。 此函式只支援數值和字串類型的參數。

hello 下列範例會傳回`true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>和
傳回`true`如果 hello 的所有參數都評估太`true`。 此函式只支援布林值類型的兩個或多個參數。

hello 下列範例會傳回`true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

hello 下列範例會傳回`false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>或
傳回`true`如果至少一個 hello 參數太評估`true`。 此函式只支援布林值類型的兩個或多個參數。

hello 下列範例會傳回`true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

hello 下列範例會傳回`true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>否
傳回`true`如果太評估 hello 參數`false`。 此函式只支援布林值類型的參數。

hello 下列範例會傳回`true`:

```json
"[not(false)]"
```

hello 下列範例會傳回`false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>coalesce
傳回 hello hello 第一個非 null 參數的值。 此函式支援所有 JSON 資料類型。

假設 `element1` 和 `element2` 為未定義。 hello 下列範例會傳回`"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>轉換函式
這些函式可使用的 tooconvert JSON 資料類型和編碼之間的值。

### <a name="int"></a>int
Hello 參數 tooan 整數轉換。 此函式支援數值和字串類型的參數。

hello 下列範例會傳回`1`:

```json
"[int('1')]"
```

hello 下列範例會傳回`2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>float
將轉換 hello 參數 tooa 浮點數。 此函式支援數值和字串類型的參數。

hello 下列範例會傳回`1.0`:

```json
"[float('1.0')]"
```

hello 下列範例會傳回`2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>字串
將 hello 參數 tooa 字串轉換。 此函式支援所有 JSON 資料類型的參數。

hello 下列範例會傳回`"1"`:

```json
"[string(1)]"
```

hello 下列範例會傳回`"2.9"`:

```json
"[string(2.9)]"
```

hello 下列範例會傳回`"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

hello 下列範例會傳回`"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>布林
將轉換 hello 參數 tooa 布林值。 此函式支援數值、字串和布林值類型的參數。 在 JavaScript 中，以外的任何值類似 tooBooleans`0`或`'false'`傳回`true`。

hello 下列範例會傳回`true`:

```json
"[bool(1)]"
```

hello 下列範例會傳回`false`:

```json
"[bool(0)]"
```

hello 下列範例會傳回`true`:

```json
"[bool(true)]"
```

hello 下列範例會傳回`true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>parse
將 hello 參數 tooa 原生類型轉換。 換句話說，此函式是 hello 反`string()`。 此函式只支援字串類型的參數。

hello 下列範例會傳回`1`:

```json
"[parse('1')]"
```

hello 下列範例會傳回`true`:

```json
"[parse('true')]"
```

hello 下列範例會傳回`[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

hello 下列範例會傳回`{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
將編碼 hello 參數 tooa base 64 編碼的字串。 此函式只支援字串類型的參數。

hello 下列範例會傳回`"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
將解碼 hello 參數從 base 64 編碼的字串。 此函式只支援字串類型的參數。

hello 下列範例會傳回`"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeUriComponent
Hello 參數 tooa URL 編碼的字串編碼。 此函式只支援字串類型的參數。

hello 下列範例會傳回`"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeUriComponent
將解碼的 URL 編碼字串 hello 參數。 此函式只支援字串類型的參數。

hello 下列範例會傳回`"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>數學函式
### <a name="add"></a>新增
將兩個數字，並傳回 hello 結果。

hello 下列範例會傳回`3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>sub
Hello hello 第一個數字，從第二個數字相減，並傳回 hello 結果。

hello 下列範例會傳回`1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
兩個數字，並傳回 hello 結果。

hello 下列範例會傳回`6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
第一個 hello hello 第二個數字，數字除以，並傳回 hello 結果。 hello 結果都是整數。

hello 下列範例會傳回`2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod
第一個 hello hello 第二個數字，數字除以，並傳回 hello 其餘部分。

hello 下列範例會傳回`0`:

```json
"[mod(6, 3)]"
```

hello 下列範例會傳回`2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>Min
傳回 hello hello 兩個數字的小。

hello 下列範例會傳回`1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>max
傳回 hello hello 兩個數字的較大。

hello 下列範例會傳回`2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>range
產生的整數類資料序列內 hello 的數字指定的範圍。

hello 下列範例會傳回`[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
傳回隨機整數的數字 hello 內指定的範圍。 此函式不會產生密碼編譯安全的隨機數字。

hello 下列範例會傳回`42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>floor
傳回小於或等於 hello 最大整數 toohello 指定數字。

hello 下列範例會傳回`3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
傳回 hello 最大的整數大於或等於 toohello 指定數字。

hello 下列範例會傳回`4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>日期函式
### <a name="utcnow"></a>utcNow
傳回字串 hello hello 本機電腦上目前的日期和時間的 ISO 8601 格式。

hello 下列範例會傳回`"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addSeconds
將整數秒 toohello 指定時間戳記。

hello 下列範例會傳回`"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
將整數分鐘 toohello 指定時間戳記。

hello 下列範例會傳回`"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
將整數的數字的時數 toohello 指定時間戳記。

hello 下列範例會傳回`"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>後續步驟
* 如簡介 tooAzure 資源管理員，請參閱[Azure 資源管理員概觀](resource-group-overview.md)。

