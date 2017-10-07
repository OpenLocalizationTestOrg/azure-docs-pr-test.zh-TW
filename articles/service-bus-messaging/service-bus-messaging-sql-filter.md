---
title: "服務匯流排 SQLFilter 語法參考 aaaAzure |Microsoft 文件"
description: "SQLFilter 文法的詳細資料。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="334d4-103">SQLFilter 語法</span><span class="sxs-lookup"><span data-stu-id="334d4-103">SQLFilter syntax</span></span>

<span data-ttu-id="334d4-104">A *SqlFilter* hello 的執行個體[SqlFilter 類別](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)，並代表 SQL 語言為基礎的篩選條件運算式，就會根據評估[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)。</span><span class="sxs-lookup"><span data-stu-id="334d4-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="334d4-105">SqlFilter 支援 hello sql-92 標準的子集。</span><span class="sxs-lookup"><span data-stu-id="334d4-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="334d4-106">本主題列出 SqlFilter 文法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="334d4-106">This topic lists details about SqlFilter grammar.</span></span>  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a><span data-ttu-id="334d4-107">引數</span><span class="sxs-lookup"><span data-stu-id="334d4-107">Arguments</span></span>  
  
-   <span data-ttu-id="334d4-108">`<scope>`是選擇性的字串表示的 hello hello 範圍`<property_name>`。</span><span class="sxs-lookup"><span data-stu-id="334d4-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="334d4-109">有效值為 `sys` 或 `user`。</span><span class="sxs-lookup"><span data-stu-id="334d4-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="334d4-110">hello`sys`值表示系統範圍其中`<property_name>`是 hello 的公用屬性名稱[BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)。</span><span class="sxs-lookup"><span data-stu-id="334d4-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="334d4-111">`user`表示使用者領域其中`<property_name>`hello 的索引鍵[BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)字典。</span><span class="sxs-lookup"><span data-stu-id="334d4-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="334d4-112">`user`範圍是 hello 預設範圍，如果`<scope>`未指定。</span><span class="sxs-lookup"><span data-stu-id="334d4-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="334d4-113">備註</span><span class="sxs-lookup"><span data-stu-id="334d4-113">Remarks</span></span>

<span data-ttu-id="334d4-114">嘗試 tooaccess 不存在系統的屬性時，發生錯誤時，嘗試 tooaccess 不存在使用者屬性不是錯誤。</span><span class="sxs-lookup"><span data-stu-id="334d4-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="334d4-115">反之，不存在的使用者屬性會內部評估為未知的值。</span><span class="sxs-lookup"><span data-stu-id="334d4-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="334d4-116">未知的值在運算子評估期間會特別處理。</span><span class="sxs-lookup"><span data-stu-id="334d4-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="334d4-117">property_name</span><span class="sxs-lookup"><span data-stu-id="334d4-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="334d4-118">引數</span><span class="sxs-lookup"><span data-stu-id="334d4-118">Arguments</span></span>  

 <span data-ttu-id="334d4-119">`<regular_identifier>`hello 所代表的字串是下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="334d4-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="334d4-120">此文法表示任何以字母為開頭且後面跟著一或多個底線/字母/數字的字串。</span><span class="sxs-lookup"><span data-stu-id="334d4-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="334d4-121">`[:IsLetter:]` 表示分類為 Unicode 字母的任何 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="334d4-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="334d4-122">如果 `c` 為 Unicode 字母，`System.Char.IsLetter(c)` 會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="334d4-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="334d4-123">`[:IsDigit:]` 表示分類為十進位數字的任何 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="334d4-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="334d4-124">如果 `c` 為 Unicode 數字，`System.Char.IsDigit(c)` 會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="334d4-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="334d4-125">`<regular_identifier>` 不能是保留的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="334d4-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="334d4-126">`<delimited_identifier>` 是使用左/右方括弧 ([]) 括住的任何字串。</span><span class="sxs-lookup"><span data-stu-id="334d4-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="334d4-127">右方括弧會以兩個右方括弧代表。</span><span class="sxs-lookup"><span data-stu-id="334d4-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="334d4-128">hello 以下是範例`<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="334d4-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="334d4-129">`<quoted_identifier>` 是以雙引號括住的任何字串。</span><span class="sxs-lookup"><span data-stu-id="334d4-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="334d4-130">識別項中的雙引號會以兩個雙引號表示。</span><span class="sxs-lookup"><span data-stu-id="334d4-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="334d4-131">不建議 toouse 引號識別項，因為它容易混淆與字串常數。</span><span class="sxs-lookup"><span data-stu-id="334d4-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="334d4-132">盡可能使用分隔的識別碼。</span><span class="sxs-lookup"><span data-stu-id="334d4-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="334d4-133">hello 的範例如下的`<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="334d4-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="334d4-134">模式</span><span class="sxs-lookup"><span data-stu-id="334d4-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="334d4-135">備註</span><span class="sxs-lookup"><span data-stu-id="334d4-135">Remarks</span></span>
  
<span data-ttu-id="334d4-136">`<pattern>` 必須是評估為字串的運算式。</span><span class="sxs-lookup"><span data-stu-id="334d4-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="334d4-137">它會當做模式中使用 LIKE 運算子的 hello。</span><span class="sxs-lookup"><span data-stu-id="334d4-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="334d4-138">它可以包含下列萬用字元 hello:</span><span class="sxs-lookup"><span data-stu-id="334d4-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="334d4-139">`%`︰任何零或多個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="334d4-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="334d4-140">`_`︰任何單一字元。</span><span class="sxs-lookup"><span data-stu-id="334d4-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="334d4-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="334d4-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="334d4-142">備註</span><span class="sxs-lookup"><span data-stu-id="334d4-142">Remarks</span></span>  

<span data-ttu-id="334d4-143">`<escape_char>` 必須是評估為字串為 1 的運算式。</span><span class="sxs-lookup"><span data-stu-id="334d4-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="334d4-144">它會當做逸出字元使用 LIKE 運算子的 hello。</span><span class="sxs-lookup"><span data-stu-id="334d4-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="334d4-145">例如，`property LIKE 'ABC\%' ESCAPE '\'` 符合 `ABC%` 而不是以 `ABC`開頭的字串。</span><span class="sxs-lookup"><span data-stu-id="334d4-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="334d4-146">常數</span><span class="sxs-lookup"><span data-stu-id="334d4-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="334d4-147">引數</span><span class="sxs-lookup"><span data-stu-id="334d4-147">Arguments</span></span>  
  
-   <span data-ttu-id="334d4-148">`<integer_constant>` 是數字的字串，不會以引號括住且不包含小數點。</span><span class="sxs-lookup"><span data-stu-id="334d4-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="334d4-149">hello 值會儲存為`System.Int64`就內部而言，並遵循 hello 相同範圍。</span><span class="sxs-lookup"><span data-stu-id="334d4-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="334d4-150">這些是長常數的範例：</span><span class="sxs-lookup"><span data-stu-id="334d4-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="334d4-151">`<decimal_constant>` 是數字的字串，不會以引號括住，且包含小數點。</span><span class="sxs-lookup"><span data-stu-id="334d4-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="334d4-152">hello 值會儲存為`System.Double`就內部而言，然後遵循 hello 相同的範圍精確度。</span><span class="sxs-lookup"><span data-stu-id="334d4-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="334d4-153">在未來版本中，這個數字可能會儲存在不同的資料型別 toosupport 確切數目語意，因此您不應該依賴 hello 事實 hello 基礎資料類型是`System.Double`如`<decimal_constant>`。</span><span class="sxs-lookup"><span data-stu-id="334d4-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="334d4-154">hello 以下是十進位常數的範例：</span><span class="sxs-lookup"><span data-stu-id="334d4-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="334d4-155">`<approximate_number_constant>` 是以科學記號標記法撰寫的數字。</span><span class="sxs-lookup"><span data-stu-id="334d4-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="334d4-156">hello 值會儲存為`System.Double`就內部而言，然後遵循 hello 相同的範圍精確度。</span><span class="sxs-lookup"><span data-stu-id="334d4-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="334d4-157">hello 以下是近似的數值常數的範例：</span><span class="sxs-lookup"><span data-stu-id="334d4-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="334d4-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="334d4-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="334d4-159">備註</span><span class="sxs-lookup"><span data-stu-id="334d4-159">Remarks</span></span>  

<span data-ttu-id="334d4-160">布林常數 hello 關鍵字來表示**TRUE**或**FALSE**。</span><span class="sxs-lookup"><span data-stu-id="334d4-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="334d4-161">hello 值會儲存為`System.Boolean`。</span><span class="sxs-lookup"><span data-stu-id="334d4-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="334d4-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="334d4-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="334d4-163">備註</span><span class="sxs-lookup"><span data-stu-id="334d4-163">Remarks</span></span>  

<span data-ttu-id="334d4-164">字串常數會以單引號括住，且包含任何有效的 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="334d4-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="334d4-165">內嵌在字串常數中的單引號會以兩個單引號表示。</span><span class="sxs-lookup"><span data-stu-id="334d4-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="334d4-166">函式</span><span class="sxs-lookup"><span data-stu-id="334d4-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="334d4-167">備註</span><span class="sxs-lookup"><span data-stu-id="334d4-167">Remarks</span></span>
  
<span data-ttu-id="334d4-168">hello`newid()`函式會傳回**System.Guid**產生 hello`System.Guid.NewGuid()`方法。</span><span class="sxs-lookup"><span data-stu-id="334d4-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="334d4-169">hello`property(name)`函式會傳回所參考的 hello 屬性 hello 值`name`。</span><span class="sxs-lookup"><span data-stu-id="334d4-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="334d4-170">hello`name`值可以是任何有效的運算式會傳回字串值。</span><span class="sxs-lookup"><span data-stu-id="334d4-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="334d4-171">考量</span><span class="sxs-lookup"><span data-stu-id="334d4-171">Considerations</span></span>
  
<span data-ttu-id="334d4-172">請考慮下列 hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)語意：</span><span class="sxs-lookup"><span data-stu-id="334d4-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="334d4-173">屬性名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="334d4-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="334d4-174">後接 C# 的運算子儘可能隱含轉換語意。</span><span class="sxs-lookup"><span data-stu-id="334d4-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="334d4-175">系統屬性為 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 執行個體中公開的公用屬性。</span><span class="sxs-lookup"><span data-stu-id="334d4-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="334d4-176">請考慮下列 hello`IS [NOT] NULL`語意：</span><span class="sxs-lookup"><span data-stu-id="334d4-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="334d4-177">`property IS NULL`會評估為`true`如果任一個 hello 屬性不存在或 hello 屬性的值是`null`。</span><span class="sxs-lookup"><span data-stu-id="334d4-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="334d4-178">屬性評估語意</span><span class="sxs-lookup"><span data-stu-id="334d4-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="334d4-179">不存在的系統屬性會擲回嘗試 tooevaluate [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception)例外狀況。</span><span class="sxs-lookup"><span data-stu-id="334d4-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="334d4-180">不存在的屬性會在內部評估為**未知**。</span><span class="sxs-lookup"><span data-stu-id="334d4-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="334d4-181">算術運算子的未知評估︰</span><span class="sxs-lookup"><span data-stu-id="334d4-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="334d4-182">二元運算子，如果是 hello 左側和 （或) 右側的運算元會評估為**未知**，hello 結果是**未知**。</span><span class="sxs-lookup"><span data-stu-id="334d4-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="334d4-183">一元運算子，如果運算元會評估為**未知**，hello 結果是**未知**。</span><span class="sxs-lookup"><span data-stu-id="334d4-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="334d4-184">二進位比較運算子的未知評估︰</span><span class="sxs-lookup"><span data-stu-id="334d4-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="334d4-185">如果是 hello 左側和 （或) 右側的運算元會評估為**未知**，hello 結果是**未知**。</span><span class="sxs-lookup"><span data-stu-id="334d4-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="334d4-186">`[NOT] LIKE` 中的未知評估：</span><span class="sxs-lookup"><span data-stu-id="334d4-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="334d4-187">如果任何運算元評估為**未知**，hello 結果是**未知**。</span><span class="sxs-lookup"><span data-stu-id="334d4-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="334d4-188">`[NOT] IN` 中的未知評估：</span><span class="sxs-lookup"><span data-stu-id="334d4-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="334d4-189">如果評估為左運算元的 hello**未知**，hello 結果是**未知**。</span><span class="sxs-lookup"><span data-stu-id="334d4-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="334d4-190">**AND** 運算子的未知評估︰</span><span class="sxs-lookup"><span data-stu-id="334d4-190">Unknown evaluation in **AND** operator:</span></span>  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 <span data-ttu-id="334d4-191">**OR** 運算子的未知評估︰</span><span class="sxs-lookup"><span data-stu-id="334d4-191">Unknown evaluation in **OR** operator:</span></span>  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="334d4-192">運算子繫結語意</span><span class="sxs-lookup"><span data-stu-id="334d4-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="334d4-193">比較運算子，例如`>`， `>=`， `<`， `<=`， `!=`，和`=`後續 hello 相同語意與 hello C# 運算子中的資料繫結輸入促銷和隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="334d4-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="334d4-194">算術運算子，例如`+`， `-`， `*`， `/`，和`%`後續 hello 相同語意與 hello C# 運算子中的資料繫結輸入促銷和隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="334d4-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="334d4-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="334d4-195">Next steps</span></span>

- [<span data-ttu-id="334d4-196">SQLFilter 類別</span><span class="sxs-lookup"><span data-stu-id="334d4-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="334d4-197">SQLRuleAction 類別</span><span class="sxs-lookup"><span data-stu-id="334d4-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)