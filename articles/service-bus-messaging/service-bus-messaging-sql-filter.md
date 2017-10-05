---
title: "Azure 服務匯流排 SQLFilter 語法參考 | Microsoft Docs"
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
ms.openlocfilehash: 3aaec8f9b6a3bbcf814f771405c3b589de6f7ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="e9ce6-103">SQLFilter 語法</span><span class="sxs-lookup"><span data-stu-id="e9ce6-103">SQLFilter syntax</span></span>

<span data-ttu-id="e9ce6-104">*SqlFilter* 為 [SqlFilter Class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 的執行個體，代表對 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 進行評估之以 SQL 語言為基礎的篩選條件運算式。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-104">A *SqlFilter* is an instance of the [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="e9ce6-105">SqlFilter 支援 SQL-92 標準的子集。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="e9ce6-106">本主題列出 SqlFilter 文法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="e9ce6-107">引數</span><span class="sxs-lookup"><span data-stu-id="e9ce6-107">Arguments</span></span>  
  
-   <span data-ttu-id="e9ce6-108">`<scope>` 是表示 `<property_name>` 範圍的選擇性字串。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="e9ce6-109">有效值為 `sys` 或 `user`。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="e9ce6-110">`sys` 值表示系統範圍，當中 `<property_name>` 為 [BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)的公用屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="e9ce6-111">`user` 表示使用者範圍，當中 `<property_name>` 為 [BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)字典的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="e9ce6-112">如果 `<scope>` 未指定，則 `user` 範圍是預設範圍。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="e9ce6-113">備註</span><span class="sxs-lookup"><span data-stu-id="e9ce6-113">Remarks</span></span>

<span data-ttu-id="e9ce6-114">嘗試存取不存在的系統屬性時會發生錯誤，而嘗試存取不存在的使用者屬性時不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="e9ce6-115">反之，不存在的使用者屬性會內部評估為未知的值。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="e9ce6-116">未知的值在運算子評估期間會特別處理。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="e9ce6-117">property_name</span><span class="sxs-lookup"><span data-stu-id="e9ce6-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="e9ce6-118">引數</span><span class="sxs-lookup"><span data-stu-id="e9ce6-118">Arguments</span></span>  

 <span data-ttu-id="e9ce6-119">`<regular_identifier>` 是由下列規則運算式所表示的字串︰</span><span class="sxs-lookup"><span data-stu-id="e9ce6-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="e9ce6-120">此文法表示任何以字母為開頭且後面跟著一或多個底線/字母/數字的字串。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="e9ce6-121">`[:IsLetter:]` 表示分類為 Unicode 字母的任何 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="e9ce6-122">如果 `c` 為 Unicode 字母，`System.Char.IsLetter(c)` 會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="e9ce6-123">`[:IsDigit:]` 表示分類為十進位數字的任何 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="e9ce6-124">如果 `c` 為 Unicode 數字，`System.Char.IsDigit(c)` 會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="e9ce6-125">`<regular_identifier>` 不能是保留的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="e9ce6-126">`<delimited_identifier>` 是使用左/右方括弧 ([]) 括住的任何字串。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="e9ce6-127">右方括弧會以兩個右方括弧代表。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="e9ce6-128">以下為 `<delimited_identifier>`的範例：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="e9ce6-129">`<quoted_identifier>` 是以雙引號括住的任何字串。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="e9ce6-130">識別項中的雙引號會以兩個雙引號表示。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="e9ce6-131">不建議使用引號識別項，因為它容易與字串常數造成混淆。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="e9ce6-132">盡可能使用分隔的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="e9ce6-133">以下是 `<quoted_identifier>` 的範例：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="e9ce6-134">模式</span><span class="sxs-lookup"><span data-stu-id="e9ce6-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="e9ce6-135">備註</span><span class="sxs-lookup"><span data-stu-id="e9ce6-135">Remarks</span></span>
  
<span data-ttu-id="e9ce6-136">`<pattern>` 必須是評估為字串的運算式。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="e9ce6-137">它會用來做為 LIKE 運算子的模式。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="e9ce6-138">它可以包含下列萬用字元︰</span><span class="sxs-lookup"><span data-stu-id="e9ce6-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="e9ce6-139">`%`︰任何零或多個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="e9ce6-140">`_`︰任何單一字元。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="e9ce6-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="e9ce6-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="e9ce6-142">備註</span><span class="sxs-lookup"><span data-stu-id="e9ce6-142">Remarks</span></span>  

<span data-ttu-id="e9ce6-143">`<escape_char>` 必須是評估為字串為 1 的運算式。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="e9ce6-144">它會用來做為 LIKE 運算子的逸出字元。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="e9ce6-145">例如，`property LIKE 'ABC\%' ESCAPE '\'` 符合 `ABC%` 而不是以 `ABC`開頭的字串。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="e9ce6-146">常數</span><span class="sxs-lookup"><span data-stu-id="e9ce6-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="e9ce6-147">引數</span><span class="sxs-lookup"><span data-stu-id="e9ce6-147">Arguments</span></span>  
  
-   <span data-ttu-id="e9ce6-148">`<integer_constant>` 是數字的字串，不會以引號括住且不包含小數點。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="e9ce6-149">值會在內部儲存為 `System.Int64`，並遵循相同的範圍。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="e9ce6-150">這些是長常數的範例：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="e9ce6-151">`<decimal_constant>` 是數字的字串，不會以引號括住，且包含小數點。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="e9ce6-152">值會在內部儲存為 `System.Double`，並遵循相同的範圍/精確度。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="e9ce6-153">在未來版本中，這個數字可能會以不同的資料類型儲存，以支援實際數字的語意，因此您不應依賴 `<decimal_constant>` 的基本資料型別是 `System.Double`。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="e9ce6-154">以下是十進位常數的範例：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="e9ce6-155">`<approximate_number_constant>` 是以科學記號標記法撰寫的數字。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="e9ce6-156">值會在內部儲存為 `System.Double`，並遵循相同的範圍/精確度。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="e9ce6-157">以下是大約數字常數的範例：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="e9ce6-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="e9ce6-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="e9ce6-159">備註</span><span class="sxs-lookup"><span data-stu-id="e9ce6-159">Remarks</span></span>  

<span data-ttu-id="e9ce6-160">布林值常數由關鍵字 **TRUE** 或 **FALSE** 代表。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="e9ce6-161">值會儲存為 `System.Boolean`。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="e9ce6-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="e9ce6-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="e9ce6-163">備註</span><span class="sxs-lookup"><span data-stu-id="e9ce6-163">Remarks</span></span>  

<span data-ttu-id="e9ce6-164">字串常數會以單引號括住，且包含任何有效的 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="e9ce6-165">內嵌在字串常數中的單引號會以兩個單引號表示。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="e9ce6-166">函式</span><span class="sxs-lookup"><span data-stu-id="e9ce6-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="e9ce6-167">備註</span><span class="sxs-lookup"><span data-stu-id="e9ce6-167">Remarks</span></span>
  
<span data-ttu-id="e9ce6-168">`newid()` 函式會傳回由 `System.Guid.NewGuid()` 方法所產生的 **System.Guid**。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="e9ce6-169">`property(name)` 函式會傳回 `name`所參考的屬性值 。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="e9ce6-170">`name` 可以是任何會傳回字串值的有效運算式。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="e9ce6-171">考量</span><span class="sxs-lookup"><span data-stu-id="e9ce6-171">Considerations</span></span>
  
<span data-ttu-id="e9ce6-172">請考慮下列 [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 語意：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="e9ce6-173">屬性名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="e9ce6-174">後接 C# 的運算子儘可能隱含轉換語意。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="e9ce6-175">系統屬性為 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 執行個體中公開的公用屬性。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="e9ce6-176">考量以下 `IS [NOT] NULL` 語意：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="e9ce6-177">如果屬性不存在或屬性的值是 `null`，`property IS NULL` 會評估為 `true`。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="e9ce6-178">屬性評估語意</span><span class="sxs-lookup"><span data-stu-id="e9ce6-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="e9ce6-179">嘗試評估不存在的系統屬性會擲回 [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-179">An attempt to evaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="e9ce6-180">不存在的屬性會在內部評估為**未知**。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="e9ce6-181">算術運算子的未知評估︰</span><span class="sxs-lookup"><span data-stu-id="e9ce6-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="e9ce6-182">針對二進位運算子，如果左和/或右邊的運算元評估為**未知**，則結果為**未知**。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="e9ce6-183">針對一元運算子，如果運算元評估為**未知**，則結果為**未知**。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="e9ce6-184">二進位比較運算子的未知評估︰</span><span class="sxs-lookup"><span data-stu-id="e9ce6-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="e9ce6-185">如果左和/或右邊的運算元評估為**未知**，則結果為**未知**。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="e9ce6-186">`[NOT] LIKE` 中的未知評估：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="e9ce6-187">如果任何運算元評估為**未知**，則結果為**未知**。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-187">If any operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="e9ce6-188">`[NOT] IN` 中的未知評估：</span><span class="sxs-lookup"><span data-stu-id="e9ce6-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="e9ce6-189">如果左運算元評估為**未知**，則結果為**未知**。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-189">If the left operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="e9ce6-190">**AND** 運算子的未知評估︰</span><span class="sxs-lookup"><span data-stu-id="e9ce6-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="e9ce6-191">**OR** 運算子的未知評估︰</span><span class="sxs-lookup"><span data-stu-id="e9ce6-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="e9ce6-192">運算子繫結語意</span><span class="sxs-lookup"><span data-stu-id="e9ce6-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="e9ce6-193">`>`、`>=`、`<`、`<=`、`!=` 和 `=` 等比較運算子會遵循與資料類型升級和隱含轉換中的 C# 運算子繫結相同的語意。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="e9ce6-194">`+`、`-`、`*`、`/` 和 `%` 等算術運算子會遵循與資料類型升級和隱含轉換中的 C# 運算子繫結相同的語意。</span><span class="sxs-lookup"><span data-stu-id="e9ce6-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9ce6-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9ce6-195">Next steps</span></span>

- [<span data-ttu-id="e9ce6-196">SQLFilter 類別</span><span class="sxs-lookup"><span data-stu-id="e9ce6-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="e9ce6-197">SQLRuleAction 類別</span><span class="sxs-lookup"><span data-stu-id="e9ce6-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)