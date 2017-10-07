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
# <a name="sqlfilter-syntax"></a>SQLFilter 語法

A *SqlFilter* hello 的執行個體[SqlFilter 類別](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)，並代表 SQL 語言為基礎的篩選條件運算式，就會根據評估[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)。 SqlFilter 支援 hello sql-92 標準的子集。  
  
 本主題列出 SqlFilter 文法的詳細資料。  
  
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
  
## <a name="arguments"></a>引數  
  
-   `<scope>`是選擇性的字串表示的 hello hello 範圍`<property_name>`。 有效值為 `sys` 或 `user`。 hello`sys`值表示系統範圍其中`<property_name>`是 hello 的公用屬性名稱[BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)。 `user`表示使用者領域其中`<property_name>`hello 的索引鍵[BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)字典。 `user`範圍是 hello 預設範圍，如果`<scope>`未指定。  
  
## <a name="remarks"></a>備註

嘗試 tooaccess 不存在系統的屬性時，發生錯誤時，嘗試 tooaccess 不存在使用者屬性不是錯誤。 反之，不存在的使用者屬性會內部評估為未知的值。 未知的值在運算子評估期間會特別處理。  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>引數  

 `<regular_identifier>`hello 所代表的字串是下列規則運算式：  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
此文法表示任何以字母為開頭且後面跟著一或多個底線/字母/數字的字串。  
  
`[:IsLetter:]` 表示分類為 Unicode 字母的任何 Unicode 字元。 如果 `c` 為 Unicode 字母，`System.Char.IsLetter(c)` 會傳回 `true`。  
  
`[:IsDigit:]` 表示分類為十進位數字的任何 Unicode 字元。 如果 `c` 為 Unicode 數字，`System.Char.IsDigit(c)` 會傳回 `true`。  
  
`<regular_identifier>` 不能是保留的關鍵字。  
  
`<delimited_identifier>` 是使用左/右方括弧 ([]) 括住的任何字串。 右方括弧會以兩個右方括弧代表。 hello 以下是範例`<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>` 是以雙引號括住的任何字串。 識別項中的雙引號會以兩個雙引號表示。 不建議 toouse 引號識別項，因為它容易混淆與字串常數。 盡可能使用分隔的識別碼。 hello 的範例如下的`<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>模式  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>備註
  
`<pattern>` 必須是評估為字串的運算式。 它會當做模式中使用 LIKE 運算子的 hello。      它可以包含下列萬用字元 hello:  
  
-   `%`︰任何零或多個字元的字串。  
  
-   `_`︰任何單一字元。  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>備註  

`<escape_char>` 必須是評估為字串為 1 的運算式。 它會當做逸出字元使用 LIKE 運算子的 hello。  
  
 例如，`property LIKE 'ABC\%' ESCAPE '\'` 符合 `ABC%` 而不是以 `ABC`開頭的字串。  
  
## <a name="constant"></a>常數  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>引數  
  
-   `<integer_constant>` 是數字的字串，不會以引號括住且不包含小數點。 hello 值會儲存為`System.Int64`就內部而言，並遵循 hello 相同範圍。  
  
     這些是長常數的範例：  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>` 是數字的字串，不會以引號括住，且包含小數點。 hello 值會儲存為`System.Double`就內部而言，然後遵循 hello 相同的範圍精確度。  
  
     在未來版本中，這個數字可能會儲存在不同的資料型別 toosupport 確切數目語意，因此您不應該依賴 hello 事實 hello 基礎資料類型是`System.Double`如`<decimal_constant>`。  
  
     hello 以下是十進位常數的範例：  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>` 是以科學記號標記法撰寫的數字。 hello 值會儲存為`System.Double`就內部而言，然後遵循 hello 相同的範圍精確度。 hello 以下是近似的數值常數的範例：  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>備註  

布林常數 hello 關鍵字來表示**TRUE**或**FALSE**。 hello 值會儲存為`System.Boolean`。  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>備註  

字串常數會以單引號括住，且包含任何有效的 Unicode 字元。 內嵌在字串常數中的單引號會以兩個單引號表示。  
  
## <a name="function"></a>函式  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>備註
  
hello`newid()`函式會傳回**System.Guid**產生 hello`System.Guid.NewGuid()`方法。  
  
hello`property(name)`函式會傳回所參考的 hello 屬性 hello 值`name`。 hello`name`值可以是任何有效的運算式會傳回字串值。  
  
## <a name="considerations"></a>考量
  
請考慮下列 hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)語意：  
  
-   屬性名稱不區分大小寫。  
  
-   後接 C# 的運算子儘可能隱含轉換語意。  
  
-   系統屬性為 [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) 執行個體中公開的公用屬性。  
  
    請考慮下列 hello`IS [NOT] NULL`語意：  
  
    -   `property IS NULL`會評估為`true`如果任一個 hello 屬性不存在或 hello 屬性的值是`null`。  
  
### <a name="property-evaluation-semantics"></a>屬性評估語意  
  
-   不存在的系統屬性會擲回嘗試 tooevaluate [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception)例外狀況。  
  
-   不存在的屬性會在內部評估為**未知**。  
  
 算術運算子的未知評估︰  
  
-   二元運算子，如果是 hello 左側和 （或) 右側的運算元會評估為**未知**，hello 結果是**未知**。  
  
-   一元運算子，如果運算元會評估為**未知**，hello 結果是**未知**。  
  
 二進位比較運算子的未知評估︰  
  
-   如果是 hello 左側和 （或) 右側的運算元會評估為**未知**，hello 結果是**未知**。  
  
 `[NOT] LIKE` 中的未知評估：  
  
-   如果任何運算元評估為**未知**，hello 結果是**未知**。  
  
 `[NOT] IN` 中的未知評估：  
  
-   如果評估為左運算元的 hello**未知**，hello 結果是**未知**。  
  
 **AND** 運算子的未知評估︰  
  
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
  
 **OR** 運算子的未知評估︰  
  
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
  
### <a name="operator-binding-semantics"></a>運算子繫結語意
  
-   比較運算子，例如`>`， `>=`， `<`， `<=`， `!=`，和`=`後續 hello 相同語意與 hello C# 運算子中的資料繫結輸入促銷和隱含轉換。  
  
-   算術運算子，例如`+`， `-`， `*`， `/`，和`%`後續 hello 相同語意與 hello C# 運算子中的資料繫結輸入促銷和隱含轉換。

## <a name="next-steps"></a>後續步驟

- [SQLFilter 類別](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [SQLRuleAction 類別](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)