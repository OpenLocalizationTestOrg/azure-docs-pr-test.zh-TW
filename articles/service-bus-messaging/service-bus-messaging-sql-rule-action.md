---
title: "在 Azure 中的 aaaSQLRuleAction 語法參考 |Microsoft 文件"
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
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="1963c-103">SQLRuleAction 語法</span><span class="sxs-lookup"><span data-stu-id="1963c-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="1963c-104">A *SqlRuleAction* hello 的執行個體[SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)類別，而代表 SQL 語言撰寫的動作集基礎的語法，將會針對執行[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="1963c-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="1963c-105">本主題列出 hello SQL 規則動作文法的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1963c-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="1963c-106">引數</span><span class="sxs-lookup"><span data-stu-id="1963c-106">Arguments</span></span>  
  
-   <span data-ttu-id="1963c-107">`<scope>`是選擇性的字串表示的 hello hello 範圍`<property_name>`。</span><span class="sxs-lookup"><span data-stu-id="1963c-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="1963c-108">有效值為 `sys` 或 `user`。</span><span class="sxs-lookup"><span data-stu-id="1963c-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="1963c-109">hello`sys`值表示系統範圍其中`<property_name>`是 hello 的公用屬性名稱[BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)。</span><span class="sxs-lookup"><span data-stu-id="1963c-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="1963c-110">`user`表示使用者領域其中`<property_name>`hello 的索引鍵[BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)字典。</span><span class="sxs-lookup"><span data-stu-id="1963c-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="1963c-111">`user`範圍是 hello 預設範圍，如果`<scope>`未指定。</span><span class="sxs-lookup"><span data-stu-id="1963c-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="1963c-112">備註</span><span class="sxs-lookup"><span data-stu-id="1963c-112">Remarks</span></span>  

<span data-ttu-id="1963c-113">嘗試 tooaccess 不存在系統的屬性時，發生錯誤時，嘗試 tooaccess 不存在使用者屬性不是錯誤。</span><span class="sxs-lookup"><span data-stu-id="1963c-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="1963c-114">反之，不存在的使用者屬性會內部評估為未知的值。</span><span class="sxs-lookup"><span data-stu-id="1963c-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="1963c-115">未知的值在運算子評估期間會特別處理。</span><span class="sxs-lookup"><span data-stu-id="1963c-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="1963c-116">property_name</span><span class="sxs-lookup"><span data-stu-id="1963c-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="1963c-117">引數</span><span class="sxs-lookup"><span data-stu-id="1963c-117">Arguments</span></span>  
 <span data-ttu-id="1963c-118">`<regular_identifier>`hello 所代表的字串是下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="1963c-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="1963c-119">這表示任何以字母為開頭且後面跟著一或多個底線/字母/數字的字串。</span><span class="sxs-lookup"><span data-stu-id="1963c-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="1963c-120">`[:IsLetter:]` 表示分類為 Unicode 字母的任何 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="1963c-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="1963c-121">如果 `c` 為 Unicode 字母，`System.Char.IsLetter(c)` 會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="1963c-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="1963c-122">`[:IsDigit:]` 表示分類為十進位數字的任何 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="1963c-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="1963c-123">如果 `c` 為 Unicode 數字，`System.Char.IsDigit(c)` 會傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="1963c-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="1963c-124">`<regular_identifier>` 不能是保留的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="1963c-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="1963c-125">`<delimited_identifier>` 是使用左/右方括弧 ([]) 括住的任何字串。</span><span class="sxs-lookup"><span data-stu-id="1963c-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="1963c-126">右方括弧會以兩個右方括弧代表。</span><span class="sxs-lookup"><span data-stu-id="1963c-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="1963c-127">hello 以下是範例`<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="1963c-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="1963c-128">`<quoted_identifier>` 是以雙引號括住的任何字串。</span><span class="sxs-lookup"><span data-stu-id="1963c-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="1963c-129">識別項中的雙引號會以兩個雙引號表示。</span><span class="sxs-lookup"><span data-stu-id="1963c-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="1963c-130">不建議 toouse 引號識別項，因為它容易混淆與字串常數。</span><span class="sxs-lookup"><span data-stu-id="1963c-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="1963c-131">盡可能使用分隔的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1963c-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="1963c-132">hello 的範例如下的`<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="1963c-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="1963c-133">模式</span><span class="sxs-lookup"><span data-stu-id="1963c-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="1963c-134">備註</span><span class="sxs-lookup"><span data-stu-id="1963c-134">Remarks</span></span>
  
 <span data-ttu-id="1963c-135">`<pattern>` 必須是評估為字串的運算式。</span><span class="sxs-lookup"><span data-stu-id="1963c-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="1963c-136">它會當做模式中使用 LIKE 運算子的 hello。</span><span class="sxs-lookup"><span data-stu-id="1963c-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="1963c-137">它可以包含下列萬用字元 hello:</span><span class="sxs-lookup"><span data-stu-id="1963c-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="1963c-138">`%`︰任何零或多個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="1963c-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="1963c-139">`_`︰任何單一字元。</span><span class="sxs-lookup"><span data-stu-id="1963c-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="1963c-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="1963c-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="1963c-141">備註</span><span class="sxs-lookup"><span data-stu-id="1963c-141">Remarks</span></span>
  
 <span data-ttu-id="1963c-142">`<escape_char>` 必須是評估為字串為 1 的運算式。</span><span class="sxs-lookup"><span data-stu-id="1963c-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="1963c-143">它會當做逸出字元使用 LIKE 運算子的 hello。</span><span class="sxs-lookup"><span data-stu-id="1963c-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="1963c-144">例如，`property LIKE 'ABC\%' ESCAPE '\'` 符合 `ABC%` 而不是以 `ABC`開頭的字串。</span><span class="sxs-lookup"><span data-stu-id="1963c-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="1963c-145">常數</span><span class="sxs-lookup"><span data-stu-id="1963c-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="1963c-146">引數</span><span class="sxs-lookup"><span data-stu-id="1963c-146">Arguments</span></span>  
  
-   <span data-ttu-id="1963c-147">`<integer_constant>` 是數字的字串，不會以引號括住且不包含小數點。</span><span class="sxs-lookup"><span data-stu-id="1963c-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="1963c-148">hello 值會儲存為`System.Int64`就內部而言，並遵循 hello 相同範圍。</span><span class="sxs-lookup"><span data-stu-id="1963c-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="1963c-149">hello 以下是長時間常數的範例：</span><span class="sxs-lookup"><span data-stu-id="1963c-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="1963c-150">`<decimal_constant>` 是數字的字串，不會以引號括住，且包含小數點。</span><span class="sxs-lookup"><span data-stu-id="1963c-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="1963c-151">hello 值會儲存為`System.Double`就內部而言，然後遵循 hello 相同的範圍精確度。</span><span class="sxs-lookup"><span data-stu-id="1963c-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="1963c-152">在未來版本中，這個數字可能會儲存在不同的資料型別 toosupport 確切數目語意，因此您不應該依賴 hello 事實 hello 基礎資料類型是`System.Double`如`<decimal_constant>`。</span><span class="sxs-lookup"><span data-stu-id="1963c-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="1963c-153">hello 以下是十進位常數的範例：</span><span class="sxs-lookup"><span data-stu-id="1963c-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="1963c-154">`<approximate_number_constant>` 是以科學記號標記法撰寫的數字。</span><span class="sxs-lookup"><span data-stu-id="1963c-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="1963c-155">hello 值會儲存為`System.Double`就內部而言，然後遵循 hello 相同的範圍精確度。</span><span class="sxs-lookup"><span data-stu-id="1963c-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="1963c-156">hello 以下是近似的數值常數的範例：</span><span class="sxs-lookup"><span data-stu-id="1963c-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="1963c-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="1963c-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="1963c-158">備註</span><span class="sxs-lookup"><span data-stu-id="1963c-158">Remarks</span></span>
  
<span data-ttu-id="1963c-159">布林常數 hello 關鍵字來表示`TRUE`或`FALSE`。</span><span class="sxs-lookup"><span data-stu-id="1963c-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="1963c-160">hello 值會儲存為`System.Boolean`。</span><span class="sxs-lookup"><span data-stu-id="1963c-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="1963c-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="1963c-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="1963c-162">備註</span><span class="sxs-lookup"><span data-stu-id="1963c-162">Remarks</span></span>
  
<span data-ttu-id="1963c-163">字串常數會以單引號括住，且包含任何有效的 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="1963c-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="1963c-164">內嵌在字串常數中的單引號會以兩個單引號表示。</span><span class="sxs-lookup"><span data-stu-id="1963c-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="1963c-165">函式</span><span class="sxs-lookup"><span data-stu-id="1963c-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="1963c-166">備註</span><span class="sxs-lookup"><span data-stu-id="1963c-166">Remarks</span></span>  

<span data-ttu-id="1963c-167">hello`newid()`函式會傳回**System.Guid**產生 hello`System.Guid.NewGuid()`方法。</span><span class="sxs-lookup"><span data-stu-id="1963c-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="1963c-168">hello`property(name)`函式會傳回所參考的 hello 屬性 hello 值`name`。</span><span class="sxs-lookup"><span data-stu-id="1963c-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="1963c-169">hello`name`值可以是任何有效的運算式會傳回字串值。</span><span class="sxs-lookup"><span data-stu-id="1963c-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="1963c-170">考量</span><span class="sxs-lookup"><span data-stu-id="1963c-170">Considerations</span></span>

- <span data-ttu-id="1963c-171">集合是使用的 toocreate 現有屬性的新屬性或更新 hello 值。</span><span class="sxs-lookup"><span data-stu-id="1963c-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="1963c-172">移除是使用的 tooremove 屬性。</span><span class="sxs-lookup"><span data-stu-id="1963c-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="1963c-173">設定會在 hello 運算式型別和 hello 現有的屬性類型是不同時盡可能執行隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="1963c-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="1963c-174">如果參考不存在的系統屬性，動作就會失敗。</span><span class="sxs-lookup"><span data-stu-id="1963c-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="1963c-175">如果參考不存在的使用者屬性，動作就不會失敗。</span><span class="sxs-lookup"><span data-stu-id="1963c-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="1963c-176">在內部不存在使用者屬性評估為 「 不明 」，下列 hello 相同的語意[SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)評估運算子時。</span><span class="sxs-lookup"><span data-stu-id="1963c-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1963c-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1963c-177">Next steps</span></span>

- [<span data-ttu-id="1963c-178">SQLRuleAction 類別</span><span class="sxs-lookup"><span data-stu-id="1963c-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="1963c-179">SQLFilter 類別</span><span class="sxs-lookup"><span data-stu-id="1963c-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
