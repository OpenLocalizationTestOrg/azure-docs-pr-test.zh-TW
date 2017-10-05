---
title: "Azure 中的 SQLRuleAction 語法參考 | Microsoft Docs"
description: "SQLRuleAction 文法的詳細資料。"
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
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 7379b7f58563675f28d77928d933c0d9c7992e71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="9088c-103">SQLRuleAction 語法</span><span class="sxs-lookup"><span data-stu-id="9088c-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="9088c-104">*SqlRuleAction* 是 [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) 類別的執行個體，代表對 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)執行的以 SQL 語言為基礎之語法所撰寫的動作集。</span><span class="sxs-lookup"><span data-stu-id="9088c-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="9088c-105">本主題列出 SQL 規則動作文法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9088c-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
## <a name="arguments"></a><span data-ttu-id="9088c-106">引數</span><span class="sxs-lookup"><span data-stu-id="9088c-106">Arguments</span></span>  
  
-   <span data-ttu-id="9088c-107">`<scope>` 是表示 `<property_name>` 範圍的選擇性字串。</span><span class="sxs-lookup"><span data-stu-id="9088c-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="9088c-108">有效值為 `sys` 或 `user`。</span><span class="sxs-lookup"><span data-stu-id="9088c-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="9088c-109">`sys` 值表示系統範圍，當中 `<property_name>` 為 [BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)的公用屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="9088c-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="9088c-110">`user` 表示使用者範圍，當中 `<property_name>` 為 [BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)字典的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9088c-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="9088c-111">如果 `<scope>` 未指定，則 `user` 範圍是預設範圍。</span><span class="sxs-lookup"><span data-stu-id="9088c-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="9088c-112">備註</span><span class="sxs-lookup"><span data-stu-id="9088c-112">Remarks</span></span>  

<span data-ttu-id="9088c-113">嘗試存取不存在的系統屬性時會發生錯誤，而嘗試存取不存在的使用者屬性時不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="9088c-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="9088c-114">反之，不存在的使用者屬性會內部評估為未知的值。</span><span class="sxs-lookup"><span data-stu-id="9088c-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="9088c-115">未知的值在運算子評估期間會特別處理。</span><span class="sxs-lookup"><span data-stu-id="9088c-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="9088c-116">property_name</span><span class="sxs-lookup"><span data-stu-id="9088c-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="9088c-117">引數</span><span class="sxs-lookup"><span data-stu-id="9088c-117">Arguments</span></span>  
 <span data-ttu-id="9088c-118">`<regular_identifier>` 是由下列規則運算式所表示的字串︰</span><span class="sxs-lookup"><span data-stu-id="9088c-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="9088c-119">這表示任何以字母為開頭且後面跟著一或多個底線/字母/數字的字串。</span><span class="sxs-lookup"><span data-stu-id="9088c-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="9088c-120">`[:IsLetter:]` 表示分類為 Unicode 字母的任何 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="9088c-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="9088c-121">如果 `c` 為 Unicode 字母，`System.Char.IsLetter(c)` 會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="9088c-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="9088c-122">`[:IsDigit:]` 表示分類為十進位數字的任何 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="9088c-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="9088c-123">如果 `c` 為 Unicode 數字，`System.Char.IsDigit(c)` 會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="9088c-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="9088c-124">`<regular_identifier>` 不能是保留的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="9088c-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="9088c-125">`<delimited_identifier>` 是使用左/右方括弧 ([]) 括住的任何字串。</span><span class="sxs-lookup"><span data-stu-id="9088c-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="9088c-126">右方括弧會以兩個右方括弧代表。</span><span class="sxs-lookup"><span data-stu-id="9088c-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="9088c-127">以下為 `<delimited_identifier>`的範例：</span><span class="sxs-lookup"><span data-stu-id="9088c-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="9088c-128">`<quoted_identifier>` 是以雙引號括住的任何字串。</span><span class="sxs-lookup"><span data-stu-id="9088c-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="9088c-129">識別項中的雙引號會以兩個雙引號表示。</span><span class="sxs-lookup"><span data-stu-id="9088c-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="9088c-130">不建議使用引號識別項，因為它容易與字串常數造成混淆。</span><span class="sxs-lookup"><span data-stu-id="9088c-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="9088c-131">盡可能使用分隔的識別碼。</span><span class="sxs-lookup"><span data-stu-id="9088c-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="9088c-132">以下是 `<quoted_identifier>` 的範例：</span><span class="sxs-lookup"><span data-stu-id="9088c-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="9088c-133">模式</span><span class="sxs-lookup"><span data-stu-id="9088c-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9088c-134">備註</span><span class="sxs-lookup"><span data-stu-id="9088c-134">Remarks</span></span>
  
 <span data-ttu-id="9088c-135">`<pattern>` 必須是評估為字串的運算式。</span><span class="sxs-lookup"><span data-stu-id="9088c-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="9088c-136">它會用來做為 LIKE 運算子的模式。</span><span class="sxs-lookup"><span data-stu-id="9088c-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="9088c-137">它可以包含下列萬用字元︰</span><span class="sxs-lookup"><span data-stu-id="9088c-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="9088c-138">`%`︰任何零或多個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="9088c-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="9088c-139">`_`︰任何單一字元。</span><span class="sxs-lookup"><span data-stu-id="9088c-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="9088c-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="9088c-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9088c-141">備註</span><span class="sxs-lookup"><span data-stu-id="9088c-141">Remarks</span></span>
  
 <span data-ttu-id="9088c-142">`<escape_char>` 必須是評估為字串為 1 的運算式。</span><span class="sxs-lookup"><span data-stu-id="9088c-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="9088c-143">它會用來做為 LIKE 運算子的逸出字元。</span><span class="sxs-lookup"><span data-stu-id="9088c-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="9088c-144">例如，`property LIKE 'ABC\%' ESCAPE '\'` 符合 `ABC%` 而不是以 `ABC`開頭的字串。</span><span class="sxs-lookup"><span data-stu-id="9088c-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="9088c-145">常數</span><span class="sxs-lookup"><span data-stu-id="9088c-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="9088c-146">引數</span><span class="sxs-lookup"><span data-stu-id="9088c-146">Arguments</span></span>  
  
-   <span data-ttu-id="9088c-147">`<integer_constant>` 是數字的字串，不會以引號括住且不包含小數點。</span><span class="sxs-lookup"><span data-stu-id="9088c-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="9088c-148">值會在內部儲存為 `System.Int64`，並遵循相同的範圍。</span><span class="sxs-lookup"><span data-stu-id="9088c-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="9088c-149">以下為長常數的範例：</span><span class="sxs-lookup"><span data-stu-id="9088c-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="9088c-150">`<decimal_constant>` 是數字的字串，不會以引號括住，且包含小數點。</span><span class="sxs-lookup"><span data-stu-id="9088c-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="9088c-151">值會在內部儲存為 `System.Double`，並遵循相同的範圍/精確度。</span><span class="sxs-lookup"><span data-stu-id="9088c-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="9088c-152">在未來版本中，這個數字可能會以不同的資料類型儲存，以支援實際數字的語意，因此您不應依賴 `<decimal_constant>` 的基本資料型別是 `System.Double`。</span><span class="sxs-lookup"><span data-stu-id="9088c-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="9088c-153">以下是十進位常數的範例：</span><span class="sxs-lookup"><span data-stu-id="9088c-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="9088c-154">`<approximate_number_constant>` 是以科學記號標記法撰寫的數字。</span><span class="sxs-lookup"><span data-stu-id="9088c-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="9088c-155">值會在內部儲存為 `System.Double`，並遵循相同的範圍/精確度。</span><span class="sxs-lookup"><span data-stu-id="9088c-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="9088c-156">以下是大約數字常數的範例：</span><span class="sxs-lookup"><span data-stu-id="9088c-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="9088c-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="9088c-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="9088c-158">備註</span><span class="sxs-lookup"><span data-stu-id="9088c-158">Remarks</span></span>
  
<span data-ttu-id="9088c-159">布林值常數由關鍵字 `TRUE` 或 `FALSE` 代表。</span><span class="sxs-lookup"><span data-stu-id="9088c-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="9088c-160">值會儲存為 `System.Boolean`。</span><span class="sxs-lookup"><span data-stu-id="9088c-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="9088c-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="9088c-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="9088c-162">備註</span><span class="sxs-lookup"><span data-stu-id="9088c-162">Remarks</span></span>
  
<span data-ttu-id="9088c-163">字串常數會以單引號括住，且包含任何有效的 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="9088c-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="9088c-164">內嵌在字串常數中的單引號會以兩個單引號表示。</span><span class="sxs-lookup"><span data-stu-id="9088c-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="9088c-165">函式</span><span class="sxs-lookup"><span data-stu-id="9088c-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="9088c-166">備註</span><span class="sxs-lookup"><span data-stu-id="9088c-166">Remarks</span></span>  

<span data-ttu-id="9088c-167">`newid()` 函式會傳回由 `System.Guid.NewGuid()` 方法所產生的 **System.Guid**。</span><span class="sxs-lookup"><span data-stu-id="9088c-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="9088c-168">`property(name)` 函式會傳回 `name`所參考的屬性值 。</span><span class="sxs-lookup"><span data-stu-id="9088c-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="9088c-169">`name` 可以是任何會傳回字串值的有效運算式。</span><span class="sxs-lookup"><span data-stu-id="9088c-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="9088c-170">考量</span><span class="sxs-lookup"><span data-stu-id="9088c-170">Considerations</span></span>

- <span data-ttu-id="9088c-171">SET 是用來建立新的屬性或更新現有屬性的值。</span><span class="sxs-lookup"><span data-stu-id="9088c-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="9088c-172">REMOVE 是用來移除屬性。</span><span class="sxs-lookup"><span data-stu-id="9088c-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="9088c-173">當運算式類型和現有的屬性型別不同時，SET 會盡可能執行隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="9088c-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="9088c-174">如果參考不存在的系統屬性，動作就會失敗。</span><span class="sxs-lookup"><span data-stu-id="9088c-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="9088c-175">如果參考不存在的使用者屬性，動作就不會失敗。</span><span class="sxs-lookup"><span data-stu-id="9088c-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="9088c-176">不存在的使用者屬性會內部評估為「不明」，評估運算子時遵循與 [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) 相同的語意。</span><span class="sxs-lookup"><span data-stu-id="9088c-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9088c-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9088c-177">Next steps</span></span>

- [<span data-ttu-id="9088c-178">SQLRuleAction 類別</span><span class="sxs-lookup"><span data-stu-id="9088c-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="9088c-179">SQLFilter 類別</span><span class="sxs-lookup"><span data-stu-id="9088c-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
