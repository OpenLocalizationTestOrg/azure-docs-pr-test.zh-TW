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
# <a name="sqlruleaction-syntax"></a>SQLRuleAction 語法

A *SqlRuleAction* hello 的執行個體[SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)類別，而代表 SQL 語言撰寫的動作集基礎的語法，將會針對執行[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
本主題列出 hello SQL 規則動作文法的詳細資料。  
  
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
  
## <a name="arguments"></a>引數  
  
-   `<scope>`是選擇性的字串表示的 hello hello 範圍`<property_name>`。 有效值為 `sys` 或 `user`。 hello`sys`值表示系統範圍其中`<property_name>`是 hello 的公用屬性名稱[BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)。 `user`表示使用者領域其中`<property_name>`hello 的索引鍵[BrokeredMessage 類別](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)字典。 `user`範圍是 hello 預設範圍，如果`<scope>`未指定。  
  
### <a name="remarks"></a>備註  

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
  
 這表示任何以字母為開頭且後面跟著一或多個底線/字母/數字的字串。  
  
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
  
     hello 以下是長時間常數的範例：  
  
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
  
布林常數 hello 關鍵字來表示`TRUE`或`FALSE`。 hello 值會儲存為`System.Boolean`。  
  
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

- 集合是使用的 toocreate 現有屬性的新屬性或更新 hello 值。
- 移除是使用的 tooremove 屬性。
- 設定會在 hello 運算式型別和 hello 現有的屬性類型是不同時盡可能執行隱含轉換。
- 如果參考不存在的系統屬性，動作就會失敗。
- 如果參考不存在的使用者屬性，動作就不會失敗。
- 在內部不存在使用者屬性評估為 「 不明 」，下列 hello 相同的語意[SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)評估運算子時。

## <a name="next-steps"></a>後續步驟

- [SQLRuleAction 類別](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [SQLFilter 類別](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
