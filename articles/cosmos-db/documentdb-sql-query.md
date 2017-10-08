---
title: "Azure Cosmos DB DocumentDB api aaaSQL 查詢 |Microsoft 文件"
description: "了解 Azure Cosmos DB 的 SQL 語法、資料庫概念及 SQL 查詢。 SQL 可作為 Azure Cosmos DB 中的 JSON 查詢語言。"
keywords: "sql 語法, sql 查詢, sql 查詢, json 查詢語言, 資料庫概念和 sql 查詢, 彙總函式"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢
Microsoft Azure Cosmos DB 支援使用 SQL (結構化查詢語言) 作為 JSON 查詢語言來查詢文件。 Cosmos DB 確實無結構描述。 由於其承諾 toohello JSON 資料模型直接在 hello 資料庫引擎內，它會提供自動編製索引的 JSON 文件而不需要明確的結構描述或建立次要索引。 

時設計 Cosmos DB hello 查詢語言，我們必須記住兩個目標：

* 而不是 ¬ 新的 JSON 查詢語言，我們想 toosupport SQL。 SQL 是一種 hello 最熟悉且常用查詢的語言。 Cosmos DB SQL 提供一個正式的程式設計模型，可在 JSON 文件上進行豐富的查詢。
* 做為能夠直接在 hello 資料庫引擎中執行 JavaScript 的 JSON 文件資料庫，我們想 toouse JavaScript 的程式設計模型為 hello 基礎的查詢語言。 在 JavaScript 的型別系統、 運算式評估，以及函式引動過程根目錄為 hello DocumentDB API SQL。 這除了其他功能之外，還進而提供自然程式設計模型來進行關聯式投射、跨 JSON 文件的階層式導覽、自我聯結、空間查詢，以及叫用完全以 JavaScript 撰寫的使用者定義函式 (UDF)。 

我們相信，這些功能 hello 應用程式與 hello 資料庫之間的索引鍵 tooreducing hello 人事而很重要的開發人員的生產力。

我們建議您藉由監看下列影片，其中 Aravind Ramachandran 顯示 Cosmos 資料庫 （linq） 功能，hello 和造訪開始使用我們[查詢遊樂場](http://www.documentdb.com/sql/demo)，其中您可以試用 Cosmos DB 而執行 SQL 查詢我們的資料集。

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

然後，傳回 toothis 文章中，我們開始使用 SQL 查詢教學課程會引導您進行一些簡單的 JSON 文件和 SQL 命令的位置。

## <a id="GettingStarted"></a>開始在 Cosmos DB 中使用 SQL 命令
toosee Cosmos DB SQL 在運作，讓我們以幾個簡單的 JSON 文件開頭並逐步引導一些簡單的查詢，對它。 請考慮有關兩個家族的這兩份 JSON 文件。 以 Cosmos DB，我們不需要 toocreate 任何結構描述或次要索引明確。 我們只需要 tooinsert hello JSON 文件 tooa Cosmos DB 集合和後續查詢。 這裡我們有簡單的 JSON 文件 hello Andersen 系列、 hello 父系、 子系 （和其寵物） 地址和註冊資訊。 hello 文件具有字串、 數字、 布林值、 陣列和巢狀的屬性。 

**文件**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

以下是第二份具有些微差異的文件：使用 `givenName` 和 `familyName` 來取代 `firstName` 和 `lastName`。

**文件**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

現在讓我們來試試幾個查詢針對此資料 toounderstand hello 的某些索引鍵 DocumentDB API SQL 層面。 Hello 下列查詢會傳回 hello 文件符合 hello 識別碼 欄位的位置，例如`AndersenFamily`。 因為它是`SELECT *`，hello 查詢的 hello 輸出是 hello 完整的 JSON 文件：

**查詢**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**結果**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


現在請試想 hello 案例，我們需要 tooreformat hello 不同組織結構的 JSON 輸出的位置。 此專案的新 JSON 物件包含兩個選取的欄位，名稱與城市時 hello 地址的縣 （市） 名稱相同的 hello hello 狀態查詢。 在此情況下，"NY, NY" 相符。

**查詢**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**結果**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


hello 下一個查詢會傳回所有 hello 指定名稱的子系中 hello 系列，其識別碼符合`WakefieldFamily`的居住地的 hello 縣 （市） 排序。

**查詢**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**結果**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


我們希望 toodraw 注意 tooa hello Cosmos DB 值得注意幾個層面查詢語言，瀏覽到目前為止，我們已看到 hello 範例：  

* 因為 DocumentDB API SQL 的處理對象是 JSON 值，所以它處理的是樹狀形式的實體，而不是資料列和資料行。 因此，hello 語言可讓您像參考 toonodes 任意深度，在 hello 樹狀結構的`Node1.Node2.Node3…..Nodem`，類似 toorelational SQL 參考 toohello 兩個組件參考的`<table>.<column>`。   
* hello 結構化查詢語言適用於無結構描述資料。 因此，動態 hello 類型系統的需求 toobe 繫結。 hello 相同的運算式可能會產生不同的文件上不同類型。 hello 查詢的結果是有效的 JSON 值，但不是保證 toobe 固定的結構描述。  
* Cosmos DB 只支援嚴謹的 JSON 文件。 這表示 hello 類型系統和運算式都是受限制的 toodeal 只能使用 JSON 類型。 請參閱 toohello [JSON 規格](http://www.json.org/)如需詳細資訊。  
* Cosmos DB 集合是 JSON 文件的無結構描述容器。 內含項目而不是主索引鍵和外部索引鍵的關聯，會隱含擷取內部與跨文件集合中的資料實體中的 hello 關聯。 這是值得按照本文件稍後所討論的 hello 文件內部聯結的重要層面。

## <a id="Indexing"></a> Cosmos DB 索引編製
我們 hello DocumentDB API SQL 語法之前，值得瀏覽索引設計 Cosmos DB 中的 hello。 

資料庫索引 hello 用途是 tooserve 各種表單和 （如 CPU 和輸入/輸出） 的最小的資源耗用量的圖形中的查詢，同時提供良好的輸送量和低延遲。 通常，hello 所選擇的 hello 正確索引，來查詢資料庫需要許多規劃和試驗。 這個方法會造成無結構描述資料庫 hello 資料不符合 tooa 嚴格的結構描述和快速發展的其中一項挑戰。 

因此，當我們設計 hello Cosmos DB 索引子系統，我們會設定 hello 下列目標：

* 索引文件，而不需要結構描述： hello 索引子系統不需要任何結構描述資訊或提出任何假設結構描述的 hello 文件。 
* 支援的有效率、 豐富的階層式，和關聯式查詢： hello 索引支援 hello Cosmos DB 查詢語言，包括支援階層式和關聯式投影。
* 支援持續性磁碟區的寫入 in face of 一致的查詢： 針對高寫入輸送量工作負載使用一致的查詢，hello 索引會以累加的方式，有效率，且在線上在更新持續的磁碟區的寫入 hello 字體。 hello 一致的索引更新為在 hello 一致性層級中的 hello 設定使用者 hello 文件服務的重要 tooserve hello 查詢。
* 多租用戶的支援： 跨租用戶中指定的資源控管 hello 保留為基礎的模型，索引不會執行更新的系統資源 （CPU、 記憶體和輸入/輸出作業每秒） 配置每個複本 hello 預算。 
* 儲存體效率： 成本效益的 hello 磁碟上儲存額外負荷 hello 索引是限制與可預測。 這是非常重要，因為 Cosmos DB 讓 hello 開發人員 toomake 成本考量取捨索引關聯 toohello 查詢效能的額外負荷。  

請參閱 toohello [Azure Cosmos DB 範例](https://github.com/Azure/azure-documentdb-net)msdn 範例顯示如何 tooconfigure hello 集合的編製索引原則。 我們現在可以使用到 hello 的 hello Azure Cosmos DB SQL 語法的詳細資料。

## <a id="Basics"></a>Azure Cosmos DB SQL 查詢的基本概念
根據 ANSI-SQL 標準，每個查詢都會包含 SELECT 子句以及選擇性的 FROM 和 WHERE 子句。 一般而言，每個查詢，會列舉 hello FROM 子句中的 hello 來源。 然後 hello 篩選中的 WHERE 子句會套用至 hello 來源 tooretrieve hello JSON 文件的子集。 最後，使用 hello SELECT 子句 tooproject hello 要求 hello 中的 JSON 值選取清單。

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>FROM 子句
hello`FROM <from_specification>`子句是選擇性的除非 hello 來源經過篩選，或稍後在 hello 查詢。 這個子句 hello 用途是查詢必須運作時的 hello toospecify hello 資料來源。 Hello 整個集合通常是 hello 來源，但其中一個可以改為指定 hello 集合的子集。 

查詢類似`SELECT * FROM Families`表示 hello 整個系列集合是透過哪些 tooenumerate hello 來源。 根的特殊識別項可以是使用的 toorepresent hello 集合，而不是使用 hello 集合名稱。 hello 下列清單包含每個查詢會強制執行的 hello 規則：

* hello 集合可以是別名，例如`SELECT f.id FROM Families AS f`或只是`SELECT f.id FROM Families f`。 這裡`f`hello 方法相當於`Families`。 `AS`這是選擇性的關鍵字 tooalias hello 識別碼。
* 一次別名 hello 原始來源無法繫結。 例如，`SELECT Families.id FROM Families f`的語法無效，因為無法再解析 hello 識別碼 」 系列 」。
* 需要 toobe 參考的所有屬性必須都是完整名稱。 在嚴格的結構描述是否遵循 hello 不存在，這是強制的 tooavoid 任何模稜兩可的繫結。 因此，`SELECT id FROM Families f`自 hello 屬性的語法無效`id`未繫結。

### <a name="subdocuments"></a>子文件
hello 來源也可以降低的 tooa 較小的子集。 比方說，tooenumerating 每份文件樹狀子目錄，hello subroot 無法再變成 hello 來源 hello 下列範例所示：

**查詢**

    SELECT * 
    FROM Families.children

**結果**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

雖然上述範例中的 hello 做 hello 來源使用陣列，物件也可用為 hello 來源，此為 hello 下列範例中所示： 任何有效的 JSON 值 （未定義），可以在 hello 來源考慮納入 hello 結果hello 查詢。 如果還沒有某些系列`address.state`值，會將它們排除 hello 查詢結果中。

**查詢**

    SELECT * 
    FROM Families.address.state

**結果**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>WHERE 子句
hello WHERE 子句 (**`WHERE <filter_condition>`**) 是選擇性的。 它會指定 hello 條件 hello hello 來源所提供的 JSON 文件必須符合在順序 toobe 納入 hello 結果的一部分。 任何 JSON 文件都必須評估 hello 指定條件太"true"toobe hello 結果列入考量。 hello 子句供順序 toodetermine hello 絕對最小的子集可以屬於 hello 結果的來源文件中的 hello 索引圖層的情況。 

hello 下列查詢會要求包含一個 name 屬性，其值的文件`AndersenFamily`。 名稱屬性，沒有任何其他文件或 hello 值不符合`AndersenFamily`排除。 

**查詢**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**結果**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


hello 前一個範例示範簡單的等號查詢。 DocumentDB API SQL 也支援各種純量運算式。 hello 最常使用的是二進位和一元的運算式。 從 hello 來源 JSON 物件的屬性參考也是有效的運算式。 

下列二元運算子的 hello 目前支援，並可用於查詢中 hello 遵循範例所示：  

<table>
<tr>
<td>算術</td>    
<td>+、-、*、/、%</td>
</tr>
<tr>
<td>位元</td>    
<td>|、&、^、<<、>>、>>> (右移位並填滿零)</td>
</tr>
<tr>
<td>邏輯</td>
<td>AND、OR、NOT</td>
</tr>
<tr>
<td>比較</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>String</td>    
<td>|| (串連)</td>
</tr>
</table>  


讓我們了解一些使用二元運算子的查詢。

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


hello 一元運算子 +、-、 ~ 不會也支援，而且可以用於在查詢中 hello 下列範例所示：

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



此外 toobinary 和一元運算子，屬性也允許的參考。 例如，`SELECT * FROM Families f WHERE f.isRegistered`傳回 hello 包含 hello 屬性的 JSON 文件`isRegistered`會 hello 屬性的值等於 toohello JSON`true`值。 任何其他值 (false、 null、 未定義， `<number>`， `<string>`， `<object>`，`<array>`等等) 會導致 hello 結果會排除 toohello 來源文件。 

### <a name="equality-and-comparison-operators"></a>相等和比較運算子
hello 下表顯示 hello 結果相等比較 DocumentDB API SQL 中任何兩個 JSON 類型。

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>運算子</strong>
         </td>
         <td valign="top">
            <strong>Undefined</strong>
         </td>
         <td valign="top">
            <strong>Null</strong>
         </td>
         <td valign="top">
            <strong>布林值</strong>
         </td>
         <td valign="top">
            <strong>數字</strong>
         </td>
         <td valign="top">
            <strong>字串</strong>
         </td>
         <td valign="top">
            <strong>物件</strong>
         </td>
         <td valign="top">
            <strong>陣列</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Undefined<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Null<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>正常</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>布林值<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>正常</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>數字<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>正常</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>字串<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>正常</strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>物件<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>正常</strong>
         </td>
         <td valign="top">
Undefined </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>陣列<strong>
         </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
Undefined </td>
         <td valign="top">
            <strong>正常</strong>
         </td>
      </tr>
   </tbody>
</table>

針對其他的比較運算子，例如 >，> =、 ！ =、 < 和 < =、 hello 適用下列規則：   

* 不同類型的比較會導致 Undefined。
* 兩個物件或兩個陣列之間的比較會導致 Undefined。   

如果 hello hello hello 篩選中的純量運算式的結果會是未定義，hello 對應文件就不會包含在 hello 結果，因為未定義不會以邏輯方式等同太"true"。

### <a name="between-keyword"></a>BETWEEN 關鍵字
您也可以使用 ANSI SQL 中的 hello BETWEEN 關鍵字 tooexpress 查詢如值的範圍。 BETWEEN 可用於字串或數字。

例如，此查詢會傳回所有系列的文件中的 hello 第一個子系等級是 1-5 （兩者皆包含） 之間。 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

不同於在 ANSI SQL，您也可以使用 hello BETWEEN 子句類似 hello 下列範例中的 hello FROM 子句中。

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

更快的查詢執行時間，請記得 toocreate 會使用針對任何數值屬性/路徑篩選 hello BETWEEN 子句中的範圍索引類型編製索引原則。 

hello 之間使用 BETWEEN DocumentDB API 和 ANSI SQL 中的主要差異是，你可以針對混合類型的屬性範圍查詢 – 例如，您可能必須是數字 (5) 「 等級 」，在某些文件和其他項目 (「 grade4") 中的字串。 在這些情況下，像是在 JavaScript 中，比較兩個不同類型結果，在 「 定義 」 和 hello 文件將會略過。

### <a name="logical-and-or-and-not-operators"></a>邏輯 (AND、OR 和 NOT) 運算子
邏輯運算子的運算對象是布林值。 這些運算子 hello 邏輯事實資料表是以 hello 下表所示。

| 或 | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |True |True |
| False |True |False |Undefined |
| Undefined |True |Undefined |Undefined |

| AND | True | False | Undefined |
| --- | --- | --- | --- |
| True |True |False |Undefined |
| False |False |False |False |
| Undefined |Undefined |False |Undefined |

| NOT |  |
| --- | --- |
| True |False |
| False |True |
| Undefined |Undefined |

### <a name="in-keyword"></a>IN 關鍵字
可以使用的 toocheck hello IN 關鍵字，是否指定的值符合清單中的任何值。 比方說，此查詢會傳回所有系列的文件識別碼 hello 其中是其中一個"WakefieldFamily"或"AndersenFamily"。 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

這個範例會傳回所有文件位置 hello 狀態可以是任何 hello 指定值。

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>三元 (?) 和聯合 (??) 運算子
hello 三元和 Coalesce 運算子可以是使用的 toobuild 條件運算式，類似 toopopular 程式設計語言，例如 C# 和 JavaScript。 

時建構新 JSON 屬性上 hello 飛 hello 三元 （？） 運算子可以是非常實用。 比方說，現在您可以撰寫查詢 tooclassify hello 類別層級到人類可讀取的格式，例如初學者/中繼/進階如下所示。

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

您也可以巢狀 hello 呼叫 toohello 運算子類似下列的 hello 查詢中。

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

做為與其他查詢運算子，如果 hello hello 條件運算式中參考的屬性已遺失在任何文件，或如果要比較的 hello 類型不同，則這些文件會排除 hello 查詢結果中。

hello Coalesce （？） 運算子可以是 （也稱為 tooefficiently 核取用於 hello 是否有屬性 已定義) 於文件中。 針對半結構化或混合類型的資料執行查詢時，這非常有用。 例如，此查詢傳回 hello"lastName"如果存在或使用 「 姓氏 」 hello 如果它不存在。

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>加上引號的屬性存取子
您也可以存取屬性使用 hello 加上引號的屬性運算子`[]`。 例如， `SELECT c.grade` and `SELECT c["grade"]` 是相等的。 這個語法時，您需要 tooescape 屬性，可包含空格、 特殊字元，或發生 tooshare hello 相同的名稱，以 SQL 關鍵字或保留的字。

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>SELECT 子句
hello SELECT 子句 (**`SELECT <select_list>`**) 是必要項，指定哪些值會從擷取 hello 查詢一樣在 ANSI SQL。 已篩選之上 hello 來源文件的 hello 子集會傳遞到 hello 投影階段中，其中 hello 指定擷取 JSON 值，並建構新的 JSON 物件時，針對每個輸入傳遞至其本身。 

下列範例中的 hello 顯示一般的 SELECT 查詢。 

**查詢**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**結果**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>巢狀屬性
在下列範例的 hello，我們會將兩個巢狀的屬性投射`f.address.state`和`f.address.city`。

**查詢**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**結果**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


投影也支援 JSON 運算式 hello 下列範例所示：

**查詢**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**結果**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


讓我們看看 hello 角色`$1`這裡。 hello`SELECT`子句需要 toocreate JSON 物件，但由於未不提供任何索引鍵，則我們會使用隱含引數的變數名稱開頭為`$1`。 例如，此查詢會傳回兩個隱含引數變數，名稱為 `$1` 和 `$2`。

**查詢**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**結果**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>別名
現在讓我們來擴充 hello 上述範例與明確的別名的值。 因為是 hello 關鍵字用於別名。 它是選擇性的投影出 hello 做為第二個值時顯示`NameInfo`。 

萬一查詢有兩個屬性，以 hello 相同的名稱，別名必須是一或兩個 hello 屬性，因此它們會明確地區分 hello 投影中使用的 toorename 結果。

**查詢**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**結果**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>純量運算式
此外 tooproperty 參考、 hello SELECT 子句也支援純量運算式，例如常數、 算術運算式、 邏輯運算式等等。例如，以下是簡單 "Hello World" 查詢。

**查詢**

    SELECT "Hello World"

**結果**

    [{
      "$1": "Hello World"
    }]


以下是使用純量運算式的較複雜範例。

**查詢**

    SELECT ((2 + 11 % 7)-2)/3    

**結果**

    [{
      "$1": 1.33333
    }]


在下列範例的 hello，hello hello 純量運算式的結果會是布林值。

**查詢**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**結果**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>物件和陣列建立
DocumentDB API SQL 的另一個重要功能是建立陣列/物件。 在 hello 前一個範例中，請注意，我們會建立新的 JSON 物件。 同樣地，其中也可以建構陣列 hello 遵循範例所示：

**查詢**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**結果**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>VALUE 關鍵字
hello**值**關鍵字，可提供方式 tooreturn JSON 值。 例如，如下所示傳回 hello 純量 hello 查詢`"Hello World"`而不是`{$1: "Hello World"}`。

**查詢**

    SELECT VALUE "Hello World"

**結果**

    [
      "Hello World"
    ]


hello 下列查詢會傳回不使用 hello hello JSON 值`"address"`hello 結果中的標籤。

**查詢**

    SELECT VALUE f.address
    FROM Families f    

**結果**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

hello 下列範例將擴充此 tooshow 如何 tooreturn JSON 基本值 （hello JSON 樹狀結構的 hello 分葉層級）。 

**查詢**

    SELECT VALUE f.address.state
    FROM Families f    

**結果**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>* 運算子
hello 特殊運算子 （*） 是支援的 tooproject hello 文件集是。 使用時，它必須只 hello 投射的欄位。 `SELECT * FROM Families f` 之類的查詢有效，`SELECT VALUE * FROM Families f ` 和 `SELECT *, f.id FROM Families f ` 則無效。

**查詢**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**結果**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>TOP 運算子
hello TOP 關鍵字可以用 toolimit hello 數目查詢的值。 當 TOP 與 hello ORDER BY 子句一起使用時，hello 結果集是有限的 toohello 第 n 個已排序的值;否則，它會傳回 hello 第 n 個結果中未定義的順序。 最佳做法，在 SELECT 陳述式，一律使用 ORDER BY 子句與 hello TOP 子句。 這是 hello toopredictably 指出哪些資料列受到 TOP 的唯一方式。 

**查詢**

    SELECT TOP 1 * 
    FROM Families f 

**結果**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

TOP 可以與常數值 (如上所示) 或使用參數化查詢的變數值搭配使用 。 如需詳細資訊，請參閱下方的參數化查詢。

### <a id="Aggregates"></a>彙總函式
您也可以執行彙總中 hello`SELECT`子句。 彙總函式會執行一組值的計算，然後傳回單一值。 例如，hello 下列查詢會傳回 hello 集合內的家族文件的 hello 的計數。

**查詢**

    SELECT COUNT(1) 
    FROM Families f 

**結果**

    [{
        "$1": 2
    }]

您也可以傳回 hello hello 純量值彙總使用 hello`VALUE`關鍵字。 比方說，hello 下列查詢會傳回值的 hello 計數以單一數字：

**查詢**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**結果**

    [ 2 ]

您也可以搭配篩選器執行彙總。 例如，hello 下列查詢會傳回文件以 hello 位址 hello 的計數 hello 華盛頓州。

**查詢**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**結果**

    [ 1 ]

hello 下表顯示 hello 清單支援的彙總函式在 DocumentDB API。 `SUM` 和 `AVG` 是對數值執行，而 `COUNT`、`MIN`和 `MAX` 則可對數字、字串、布林值和 null 執行。 

| 使用量 | 說明 |
|-------|-------------|
| COUNT | 傳回 hello hello 運算式中的項目數。 |
| SUM   | 傳回 hello hello 運算式中的所有 hello 值的總和。 |
| 最小值   | 傳回 hello hello 運算式中的最小值。 |
| 最大值   | 傳回 hello hello 運算式中的最大值。 |
| 平均   | 傳回 hello hello 運算式中的 hello 值的平均值。 |

也可在 hello 結果陣列反覆項目上執行彙總。 如需詳細資訊，請參閱[查詢中的陣列反覆運算](#Iteration)。

> [!NOTE]
> 當使用 hello Azure 入口網站查詢總管時，請注意，彙總查詢中可能傳回 hello 部分彙總的結果查詢 頁面。 hello Sdk 會產生單一的累計值，所有頁面。 
> 
> 為了 tooperform 彙總查詢，使用程式碼，您需要.NET SDK 1.12.0、.NET Core SDK 1.1.0 或 Java SDK 1.9.5 或更新版本。    
>

## <a id="OrderByClause"></a>ORDER BY 子句
像是在 ANSI SQL 中，您可以在查詢時包含選擇性的 Order By 子句。 hello 子句可以包含選擇性 ASC/DESC 引數 toospecify hello 訂單結果必須擷取。

例如，以下是擷取系列中的 hello 常駐城市名稱順序的查詢。

**查詢**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**結果**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

以下是系列中的建立日期以數字代表 hello epoch 時間，也就是，經過時間 1970 年 1 月 1，以秒為單位儲存的順序會擷取的查詢。

**查詢**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**結果**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>進階資料庫概念和 SQL 查詢

### <a id="Iteration"></a>反覆運算
新建構加入透過 hello **IN** DocumentDB API SQL tooprovide 支援逐一查看 JSON 陣列中的關鍵字。 hello FROM 來源反覆項目提供支援。 讓我們開始 hello 下列範例：

**查詢**

    SELECT * 
    FROM Families.children

**結果**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

現在讓我們看看另一個查詢，透過 hello 集合中的子系執行反覆項目。 請注意 hello 輸出陣列中的 hello 差異。 此範例會將`children`和 hello 結果扁平化單一陣列。  

**查詢**

    SELECT * 
    FROM c IN Families.children

**結果**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

這可以進一步使用的 toofilter hello 陣列 hello 下列範例所示的每個個別項目：

**查詢**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**結果**  

    [{
      "givenName": "Lisa"
    }]

您也可以透過 hello 結果陣列反覆項目執行彙總。 例如，hello 下列查詢會計算 hello 子系之間的所有家族數目。

**查詢**

    SELECT COUNT(child) 
    FROM child IN Families.children

**結果**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>聯結
在關聯式資料庫中，在資料表之間的 hello 需要 toojoin 很重要。 它的 hello 正規化的推論 toodesigning 邏輯結構描述。 反對 toothis，DocumentDB API 處理 hello 非正規化的資料模型的無結構描述的文件。 這是 hello 的邏輯對等的 「 自我聯結 」。

hello 語言支援的 hello 語法為 < from_source1 > 聯結 < from_source2 > 聯結...JOIN <from_sourceN>。 整體而言，這會傳回一組 **N**-Tuple (具有 **N** 個值的 Tuple)。 每個 Tuple 所擁有的值，都是將所有集合別名在其個別集合上反覆運算所產生。 換句話說，這是參與 hello 聯結 hello 集合的完整交叉乘積。

hello 下列範例顯示 hello JOIN 子句的運作方式。 在下列範例的 hello，hello 結果是空的因為 hello 交叉乘積，每份文件從來源和空的集合是空的。

**查詢**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**結果**  

    [{
    }]


在下列範例的 hello，hello 聯結是 hello 文件根與 hello 之間`children`subroot。 它是兩個 JSON 物件之間的交叉乘積。 因為我們處理 hello 子陣列的單一根節點，便無法生效 hello 聯結中子系是陣列的 hello 事實。 因此 hello 結果會包含只有兩個結果，因為 hello 交叉乘積，每份文件以 hello 陣列會產生剛好只有一個文件。

**查詢**

    SELECT f.id
    FROM Families f
    JOIN f.children

**結果**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


下列範例中的 hello 顯示傳統聯結：

**查詢**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**結果**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



hello 首先 toonote 為該 hello`from_source`的 hello**聯結**子句是迭代器。 因此，hello 流程在此情況下，如下所示如下：  

* 展開每一個子項目**c** hello 陣列中。
* 套用 hello 根 hello 文件的交叉乘積**f**每個子項目與**c** ，已扁平化 hello 第一個步驟中。
* 最後，專案 hello 根物件**f** name 單獨的屬性。 

hello 第一個文件 (`AndersenFamily`) 只包含一個子元素，所以 hello 結果集包含只有單一物件對應 toothis 文件。 hello 第二個文件 (`WakefieldFamily`) 包含兩個子系。 因此，hello 交叉乘積會產生不同的物件供每個子系，藉此產生兩個物件，其中每個子對應 toothis 文件中。 在這些文件中的欄位 hello 根 hello 相同，就像您會預期中的交叉乘積。

hello hello 聯結的實際公用程式是從 hello 交叉乘積中的圖形，否則為 tooform tuple tooproject 困難。 此外，我們看到在 hello 面範例中，您可以篩選的 tuple 的 hello 組合 hello，可讓使用者選擇整體的 hello tuple 符合條件。

**查詢**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**結果**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



這個範例是前面範例中，hello 的自然擴充功能，並執行兩個聯結。 因此，hello 交叉乘積可視為 hello 下列虛擬程式碼：

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily` 有一個小孩養了一隻寵物。 因此，hello 交叉乘積會產生一個資料列 (1\*1\*1) 從這一系列。 不過，WakefieldFamily 有兩個小孩，但只有一個小孩 "Jesse" 養了多隻寵物。 Jesse 有兩隻寵物。 因此 hello 交叉乘積產生 1\*1\*2 = 2 此系列中的資料列。

在 hello 下一個範例中，沒有額外的篩選`pet`。 這不包括所有 hello tuple hello 隻寵物的名字不 「 陰影 」。 請注意，我們會從陣列中，任何 hello tuple 的 hello 項篩選無法 toobuild tuple，以及專案 hello 項目的任何組合。 

**查詢**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**結果**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>JavaScript 整合
Azure Cosmos DB 預存程序和觸發程序方面的 hello 集合上直接執行 JavaScript 為基礎的應用程式邏輯提供程式設計模型。 這允許：

* 查詢中的 JavaScript 執行階段，直接在 hello 資料庫引擎內的 hello 深層整合必定集合的文件和能力 toodo 高效能交易 CRUD 作業。 
* 將控制流程、變數範圍限制、指派以及例外狀況處理基本類型與資料庫交易的整合自然模型化。 如需 Azure Cosmos DB 支援 JavaScript 整合的詳細資訊，請參閱 toohello JavaScript 伺服器端程式設計文件。

### <a id="UserDefinedFunctions"></a>使用者定義函式 (UDF)
Hello 已在這份文件中定義的型別，以及 DocumentDB API SQL 支援使用者定義函數 (UDF)。 特別是，純量 Udf 支援 hello 開發人員可以傳入零或多個引數並傳回單一引數結果回其中。 系統會檢查所有這些引數是否為合法的 JSON 值。  

hello DocumentDB API SQL 語法已擴充，使用這些使用者定義函式的 toosupport 自訂應用程式邏輯。 您可以向 DocumentDB API 註冊 UDF，然後在 SQL 查詢中參照它。 事實上，Udf 是 exquisitely hello 設計 toobe 查詢所叫用。 做為推論 toothis 的選擇，Udf 不含存取 toohello 內容物件的 hello 其他 JavaScript 有型別 （預存程序和觸發程序）。 因為查詢是以唯讀形式執行，所以可以在主要或次要複本上執行。 因此，Udf 是設計的 toorun 不像其他的 JavaScript 類型的次要複本上。

以下是如何在 hello Cosmos DB 之下的資料庫，特別是文件集合可以註冊 UDF 的範例。

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

hello 上述範例會建立的 UDF，其名稱是`REGEX_MATCH`。 它接受兩個的 JSON 字串值`input`和`pattern`和檢查，如果第二個 hello hello 模式中指定 hello 第一個相符項目使用 JavaScript 的 string.match() 函式。

我們現在可以在投射的查詢中使用此 UDF。 Udf 必須限定 hello 區分大小寫的前置詞"udf。 」 (當從查詢內呼叫時)。 

> [!NOTE]
> 先前 too3/17/2015，Cosmos DB 支援 UDF 呼叫沒有 hello"udf。 」 例如 SELECT REGEX_MATCH()。 這種呼叫模式已被取代。  
> 
> 

**查詢**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**結果**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

hello UDF 也可以用在篩選內 hello 面範例中，也限定 hello"udf。 」 中所示 前置詞來限定：

**查詢**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**結果**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


在本質上，UDF 是有效的純量運算式，而且可以用於投射和篩選。 

tooexpand hello 電源的 Udf 時，讓我們看看另一個範例使用條件式邏輯：

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


以下是範例，練習 hello UDF。

**查詢**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**結果**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


如 hello 上述範例展示，Udf 整合 hello 電源的 JavaScript 語言 hello DocumentDB API SQL tooprovide 非常豐富的可程式化介面 toodo 複雜程序、 條件式邏輯與 hello 的內建 JavaScript 執行階段的說明功能。

DocumentDB API SQL 提供 hello 引數 toohello Udf hello 來源中的每份文件在 hello 目前 （WHERE 子句或 SELECT 子句） 的階段處理 hello UDF。 hello 結果就會合併在順暢地 hello 整體執行管線。 如果 hello 屬性參照的 tooby hello UDF 參數不適用於 hello JSON 值 hello 參數會被視為未定義，並因此 hello UDF 引動過程會完全略過。 同樣地 hello hello UDF 未定義的結果，如果它不是包含 hello 結果中。 

總而言之，Udf 是 hello 查詢一部分的絕佳工具 toodo 複雜的商務邏輯。

### <a name="operator-evaluation"></a>運算子評估
Cosmos DB hello virtue 的 JSON 資料庫所繪製 parallels 與 JavaScript 運算子和評估語意。 雖然 Cosmos DB 嘗試 toopreserve JavaScript 語意 JSON 支援方面，hello 作業評估偏差在某些情況下。

在 DocumentDB API SQL 中，不同於傳統的 SQL 中 hello 類型的值通常之前，無法得知會從資料庫擷取 hello 值。 順序 tooefficiently 中執行查詢，大部分的 hello 運算子有嚴格的型別需求。 

與 JavaScript 不同，DocumentDB API SQL 並不會執行隱含轉換。 例如，類似 `SELECT * FROM Person p WHERE p.Age = 21` 的查詢會針對包含 Age 屬性且值為 21 的文件進行比對。 任何其他 Age 屬性符合字串 "21" 或其他可能之無限制變化 (例如 "021"、"21.0"、"0021"、"00021" 等等) 的文件，則不會成為比對的結果。 相反地，這是 toohello JavaScript hello 字串值的隱含轉換 toonumbers (根據運算子，例如: = =)。 這項選擇對 DocumentDB API SQL 中有效率的索引比對十分重要。 

## <a name="parameterized-sql-queries"></a>參數化 SQL 查詢
Cosmos DB 支援查詢參數以 hello 熟悉 @ 表示法來表示。 參數化 SQL 提供使用者輸入的健全處理和逸出，防止透過 SQL 插入式意外洩露資料。 

比方說，您可以撰寫查詢，將姓氏和地址 (州) 做為參數，然後根據使用者輸入，使用各種不同姓氏和地址 (州) 的值執行查詢。

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

此要求可以傳送 tooCosmos DB 做為參數化的 JSON 查詢類似如下所示。

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

hello 引數 tooTOP 可以設定使用參數化的查詢類似如下所示。

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

參數值可以是任何有效的 JSON (字串、數字、布林值、null，甚至是陣列或巢狀 JSON)。 此外，由於 Cosmos DB 並無結構描述，因此系統不會對照任何類型來驗證參數。

## <a id="BuiltinFunctions"></a>內建函數
Cosmos DB 也支援一些適用於一般作業的內建函式，這些函式可在像是使用者定義函式 (UDF) 之類的查詢內使用。

| 函式群組          | 作業                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| 數學函數  | ABS、CEILING、EXP、FLOOR、LOG、LOG10、POWER、ROUND、SIGN、SQRT、SQUARE、TRUNC、ACOS、ASIN、ATAN、ATN2、COS、COT、DEGREES、PI、RADIANS、SIN 和 TAN |
| 類型檢查函數 | IS_ARRAY、IS_BOOL、IS_NULL、IS_NUMBER、IS_OBJECT、IS_STRING、IS_DEFINED 和 IS_PRIMITIVE                                                           |
| 字串函數        | CONCAT、CONTAINS、ENDSWITH、INDEX_OF、LEFT、LENGTH、LOWER、LTRIM、REPLACE、REPLICATE、REVERSE、RIGHT、RTRIM、STARTSWITH、SUBSTRING 和 UPPER       |
| 陣列函數         | ARRAY_CONCAT、ARRAY_CONTAINS、ARRAY_LENGTH 和 ARRAY_SLICE                                                                                         |
| 空間函數       | ST_DISTANCE、ST_WITHIN、ST_INTERSECTS、ST_ISVALID 和 ST_ISVALIDDETAILED                                                                           | 

如果您目前使用的使用者定義的函數 (UDF) 已可使用內建函式，您就應該使用 hello 對應內建函式，為即將 toobe 快速 toorun 以及其他更多有效。 

### <a name="mathematical-functions"></a>數學函數
hello 數學函數會執行計算，根據輸入值會作為引數，且傳回數字的值。 以下是支援的內建數學函數資料表。


| 使用量 | 說明 |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS (num_expr)](#bk_abs) | 傳回 hello 絕對 （正） 值 hello 指定數值運算式。 |
| [CEILING (num_expr)](#bk_ceiling) | 傳回 hello 最小整數值大於或等於，hello 指定數值運算式。 |
| [FLOOR (num_expr)](#bk_floor) | 傳回小於 hello 最大整數 toohello 或等於指定數值運算式。 |
| [EXP (num_expr)](#bk_exp) | 傳回 hello 指數的 hello 指定數值運算式。 |
| [LOG (num_expr [,base])](#bk_log) | 傳回 hello 自然對數的 hello 指定數值運算式，或是使用 hello hello 對數指定基底 |
| [LOG10 (num_expr)](#bk_log10) | 傳回 hello 基底 10 對數值 hello 指定數值運算式。 |
| [ROUND (num_expr)](#bk_round) | 傳回數值，捨入的 toohello 最接近的整數值。 |
| [TRUNC (num_expr)](#bk_trunc) | 傳回數值，截斷的 toohello 最接近的整數值。 |
| [SQRT (num_expr)](#bk_sqrt) | 傳回 hello 平方根 hello 指定數值運算式。 |
| [SQUARE (num_expr)](#bk_square) | 傳回 hello 方形的 hello 指定數值運算式。 |
| [POWER (num_expr, num_expr)](#bk_power) | 指定了數值運算式 toohello 值指定傳回 hello 冪 hello。 |
| [SIGN (num_expr)](#bk_sign) | 傳回 hello 號 （-1，0，1） 的值 hello 指定數值運算式。 |
| [ACOS (num_expr)](#bk_acos) | 傳回 hello 的角度，以弧度為單位，它的餘弦為 hello 指定數值運算式。也稱為反餘弦值。 |
| [ASIN (num_expr)](#bk_asin) | 傳回 hello 的角度，以弧度為單位，其正弦值為 hello 指定數值運算式。 這也稱為反正弦值。 |
| [ATAN (num_expr)](#bk_atan) | 傳回 hello 的角度，以弧度為單位，其正切為 hello 指定數值運算式。 這也稱為反正切值。 |
| [ATN2 (num_expr)](#bk_atn2) | 傳回 hello hello 正數 x 軸與 hello 光線從 hello toohello 原點 （y，x） 之間，弧度的角度，其中 x 和 y 是兩個指定的浮點運算式的 hello hello 值。 |
| [COS (num_expr)](#bk_cos) | 傳回 hello 三角餘弦函數 hello 指定旋轉的角度，以弧度為單位，hello 中指定的運算式。 |
| [COT (num_expr)](#bk_cot) | 傳回 hello 三角餘切函數 hello 指定旋轉的角度，以弧度為單位，在 hello 指定數值運算式。 |
| [DEGREES (num_expr)](#bk_degrees) | 傳回 hello 以度為單位的角度以弧度為單位指定的對應角度。 |
| [PI ()](#bk_pi) | 傳回 hello PI 的常數值。 |
| [RADIANS (num_expr)](#bk_radians) | 當您輸入數值運算式 (以度為單位) 時，傳回弧度。 |
| [SIN (num_expr)](#bk_sin) | 傳回 hello 三角正弦函數 hello 指定旋轉的角度，以弧度為單位，hello 中指定的運算式。 |
| [TAN (num_expr)](#bk_tan) | 傳回 hello 正切 hello 輸入運算式，hello 中指定的運算式。 |

例如，您現在可以執行類似 hello 下列查詢：

**查詢**

    SELECT VALUE ABS(-4)

**結果**

    [4]

hello Cosmos DB 函式比較 tooANSI SQL 之間的主要差異在於它們是設計的 toowork 與無結構描述和混合的結構描述資料。 比方說，如果您有的文件，其中 hello 大小屬性遺漏，或非數值像 「 不明 」，然後 hello 文件會透過，略過而不是傳回錯誤。

### <a name="type-checking-functions"></a>類型檢查函數
hello 類型檢查函數可讓您 toocheck hello SQL 查詢中運算式型別。 類型檢查函數可以在變數或未知時，使用 hello 立即 toodetermine hello 類型的文件內的屬性。 以下是支援的內建類型檢查函數資料表。

<table>
<tr>
  <td><strong>用法</strong></td>
  <td><strong>說明</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></td>
  <td>傳回布林值，指出是否 hello hello 值型別陣列。</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></td>
  <td>傳回布林值，指出是否 hello hello 值型別布林值。</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></td>
  <td>傳回布林值，指出 hello hello 值型別是否為 null。</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></td>
  <td>傳回布林值，指出是否 hello hello 值型別數字。</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></td>
  <td>傳回布林值，指出是否 hello hello 值型別一個 JSON 物件。</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></td>
  <td>傳回布林值，指出是否 hello hello 值型別為字串。</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></td>
  <td>傳回布林值，指出如果 hello 尚未指派屬性值。</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></td>
  <td>傳回布林值，指出是否 hello hello 值類型字串、 數字、 布林值或 null。</td>
</tr>

</table>

使用這些函式，您現在可以執行類似 hello 下列查詢：

**查詢**

    SELECT VALUE IS_NUMBER(-4)

**結果**

    [true]

### <a name="string-functions"></a>字串函數
hello 下列純量函數的字串輸入值來執行作業並傳回字串、 數值或布林值。 以下是內建字串函數的資料表：

| 使用量 | 說明 |
| --- | --- |
| [LENGTH (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |指定字串運算式的字元為單位的 hello 傳回 hello 數目 |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |傳回字串 hello 因產生的串連兩個或多個字串值。 |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |傳回字串運算式的一部分。 |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |傳回布林值，指出是否 hello 第一個字串運算式的結尾 hello 第二個 |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |傳回布林值，指出是否 hello 第一個字串運算式的結尾 hello 第二個 |
| [CONTAINS (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |傳回布林值，指出是否 hello 第一個字串運算式中第二個包含 hello。 |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |傳回開始 hello 內 hello 第一個指定的字串運算式，則為-1 hello 第二個字串運算式的第一次出現的位置，如果找不到 hello 字串 hello。 |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |傳回 hello 字串的左側的組件以 hello 指定字元數。 |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |傳回 hello 權限屬於字串 hello 與指定字元的數。 |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |傳回移除開頭空白之後的字串運算式。 |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |傳回截斷所有結尾空白之後的字串運算式。 |
| [LOWER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |傳回將大寫字元資料 toolowercase 轉換後的字串運算式。 |
| [UPPER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |傳回將小寫字元資料 toouppercase 轉換後的字串運算式。 |
| [REPLACE (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |使用其他字串值取代指定的字串值的所有項目。 |
| [REPLICATE (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |將字串值重複指定的次數。 |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |傳回字串值的 hello 反向順序。 |

使用這些函式，您現在可以執行類似 hello 下列查詢。 例如，您可以傳回 hello 系列名稱以大寫，如下所示：

**查詢**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**結果**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

或串連字串，如下列範例所示：

**查詢**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**結果**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


字串函式也可用在 hello 其中子句 toofilter 結果，如同下列範例中的 hello:

**查詢**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**結果**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>陣列函數
下列純量函數的 hello 執行作業陣列輸入的值和傳回數值、 布林值或陣列值。 以下是內建陣列函數的資料表：

| 使用量 | 說明 |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |傳回 hello 項目數的 hello 指定陣列運算式。 |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |傳回陣列，其中是 hello 結果串連兩個以上陣列值。 |
| [ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |傳回布林值，指出 hello 陣列中是否包含 hello 指定的值。 可以指定完整或部分，是否才 hello 比對。 |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |傳回陣列運算式的一部分。 |

陣列的函式可使用的 toomanipulate 陣列在 JSON 中。 例如，以下是其中 hello 父系的其中一個是 「 循環配置資源 Wakefield"會傳回所有文件的查詢。 

**查詢**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**結果**

    [{
      "id": "WakefieldFamily"
    }]

您可以指定相符的項目 hello 陣列中的部分片段。 hello 下列查詢會尋找所有父系使用 hello`givenName`的`Robin`。

**查詢**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**結果**

    [{
      "id": "WakefieldFamily"
    }]


以下是另一個範例，其使用 ARRAY_LENGTH tooget hello 每個系列的子系數目。

**查詢**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**結果**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>空間函數
Cosmos DB 支援 hello 下列開放式地理空間協會 (OGC) 的地理空間查詢內建函式。 

<table>
<tr>
  <td><strong>用法</strong></td>
  <td><strong>說明</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr、point_expr)</td>
  <td>傳回兩個 hello GeoJSON 點、 多邊形或 LineString 運算式之間的 hello 距離。</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr、polygon_expr)</td>
  <td>傳回指示 hello 第一個 GeoJSON 物件 （點、 多邊形或 LineString） 是否在 hello 第二個 GeoJSON 物件 （點、 多邊形或 LineString） 的布林運算式。</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>傳回指出是否要交叉 hello 兩個指定的 GeoJSON 物件 （點、 多邊形或 LineString） 的布林運算式。</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>傳回布林值，指出 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式是否有效。</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>傳回包含布林值，如果 hello 指定 GeoJSON 點、 多邊形或 LineString 運算式的 JSON 值有效，而且如果無效，此外 hello 原因，表示為字串值。</td>
</tr>
</table>

空間函式可使用的 tooperform 鄰近查詢空間資料。 例如，以下是 hello 的可傳回所有的系列文件，30 公里內指定的位置使用 hello ST_DISTANCE 內建函式的查詢。 

**查詢**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**結果**

    [{
      "id": "WakefieldFamily"
    }]

如需有關 Cosmos DB 中的地理空間支援詳細資料，請參閱[使用 Azure Cosmos DB 中的地理空間資料](geospatial.md)。 Cosmos db 包裝空間的函式和 hello SQL 語法。 現在讓我們看看如何 LINQ 查詢的運作方式以及它如何與 hello 語法互動我們看到了到目前為止。

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
LINQ 是一種 .NET 程式設計模型，此模型會將運算表示為對物件串流的查詢。 Cosmos DB 藉由使用 LINQ 的用戶端程式庫 toointerface 促進 JSON 和.NET 物件之間的轉換，並從 LINQ 子集的對應查詢 tooCosmos DB 查詢。 

hello 下圖顯示 hello 架構支援使用 Cosmos DB LINQ 查詢。  使用 hello Cosmos DB 用戶端，開發人員可以建立**IQueryable**物件直接查詢 hello Cosmos DB 查詢提供者，然後會將 hello LINQ 查詢轉譯成 Cosmos DB 查詢。 hello 查詢然後會以 JSON 格式傳遞 toohello Cosmos DB 伺服器 tooretrieve 一組結果。 hello 傳回結果為已還原序列化成資料流，hello 用戶端上的.NET 物件。

![使用 DocumentDB API 來支援 LINQ 查詢的架構：SQL 語法、JSON 查詢語言、資料庫概念及 SQL 查詢][1]

### <a name="net-and-json-mapping"></a>.NET 和 JSON 對應
為自然階層 hello.NET 物件和 JSON 文件之間的對應-對應每個資料成員欄位 tooa JSON 物件，其中是 hello 欄位名稱對應 toohello 「 金鑰 」 部分 hello 物件和 hello 「 值 」 組件是以遞迴方式對應 toohello 值 hello 物件一部分。 請考慮下列範例中的 hello: hello 系列物件建立對應的 toohello JSON 文件如下所示。 且反之亦然，hello JSON 文件對應的反向 tooa.NET 物件。

**C# 類別**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>LINQ tooSQL 轉譯
hello Cosmos DB 查詢提供者從 LINQ 查詢執行最佳的投入時間對應到 Cosmos DB SQL 查詢。 在下列描述 hello，我們假設 hello 讀者具備 「 基本的認識 LINQ。

首先，hello 型別系統，我們支援所有 JSON 基本型別 – 數值類型、 布林值、 字串和 null。 只支援這些 JSON 類型。 下列純量運算式的 hello 支援。

* 常值-將常數值的 hello 基本資料類型包括次 hello hello 查詢都會進行評估。
* 屬性/陣列索引運算式 – 這些運算式參考物件或陣列元素 toohello 的屬性。
  
     family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable
* 算術運算式：這些包括數值和布林值的一般算術運算式。 Hello 完整清單，請參閱 toohello SQL 規格。
  
     2 * family.children[0].grade;    x + y;
* 字串比較運算式-這些包括比較字串值 toosome 常數字串值。  
  
     mother.familyName == "Smith";    child.givenName == s; //s is a string variable
* 物件/陣列建立運算式：這些運算式傳回複合值類型或匿名類型的物件，或是這類物件的陣列。 這些值可以是巢狀值。
  
     new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //含有兩個欄位的匿名類型              
     new int[] { 3, child.grade, 5 };

### <a id="SupportedLinqOperators"></a>支援的 LINQ 運算子清單
以下是支援的 LINQ 運算子 hello LINQ 提供者隨附 hello DocumentDB.NET SDK 中的清單。

* **選取**： 投影轉譯 toohello SQL SELECT 包括物件建構
* **其中**： 轉譯 toohello SQL WHERE，篩選器，並支援之間轉譯 & &、 | | 和 ！ toohello SQL 運算子
* **SelectMany**： 可讓陣列 toohello SQL JOIN 子句的回溯。 可以是陣列項目上的使用的 toochain/巢狀運算式 toofilter
* **OrderBy 和 OrderByDescending**： 轉譯 tooORDER BY 遞增/遞減
* 彙總的 **Count**、**Sum**、**Min**、**Max** 與 **Average** 運算子，以及其非同步對應項 **CountAsync**、**SumAsync**、**MinAsync**、**MaxAsync** 與 **AverageAsync**。
* **CompareTo**： 轉譯 toorange 比較。 通常用於字串，因為字串在 .NET 中是無法比較的
* **採取**： 轉譯 toohello SQL TOP 來限制查詢結果
* **數學函式**： 支援從轉譯。網路的 Abs，Acos、 Asin、 Atan、 Ceiling、 Cos、 Exp、 Floor、 記錄、 Log10、 Pow、 循、 符號、 Sin、 Sqrt、 Tan、 截斷 toohello 對等 SQL 內建函式。
* **字串函數**： 支援從轉譯。網路的 Concat、 Contains、 EndsWith、 IndexOf、 計數、 ToLower、 TrimStart、 取代、 反向、 TrimEnd、 StartsWith、 子字串，ToUpper toohello 對等 SQL 內建函式。
* **陣列函數**： 支援從轉譯。網路的 Concat、 Contains 和計數 toohello 對等 SQL 內建函式。
* **Geospatial 擴充函式**： 支援從虛設常式方法距離內 IsValid、 轉譯和 IsValidDetailed toohello 對等 SQL 內建函式。
* **使用者定義函式延伸模組函數**： 支援轉譯 hello 從虛設常式方法 UserDefinedFunctionProvider.Invoke toohello 對應使用者定義函式。
* **其他**: hello 的轉譯聯合的支援和條件式運算子。 可以翻譯 Contains tooString CONTAINS、 ARRAY_CONTAINS 或 hello SQL 中的，視內容而定。

### <a name="sql-query-operators"></a>SQL 查詢運算子
以下是一些範例，說明如何某些 hello 標準 LINQ 查詢運算子轉譯 tooCosmos DB 查詢。

#### <a name="select-operator"></a>Select 運算子
hello 語法`input.Select(x => f(x))`，其中`f`是純量運算式。

**LINQ Lambda 運算式**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**LINQ Lambda 運算式**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**LINQ Lambda 運算式**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>SelectMany 運算子
hello 語法`input.SelectMany(x => f(x))`，其中`f`是傳回的集合類型的純量運算式。

**LINQ Lambda 運算式**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Where 運算子
hello 語法`input.Where(x => f(x))`，其中`f`是純量運算式，它會傳回布林值。

**LINQ Lambda 運算式**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**LINQ Lambda 運算式**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>複合 SQL 查詢
hello 上方運算子可以是組成的 tooform 功能更強大的查詢。 由於 Cosmos DB 支援巢狀的集合，hello 組合可以串連或巢狀。

#### <a name="concatenation"></a>串連
hello 語法`input(.|.SelectMany())(.Select()|.Where())*`。 串連查詢的開頭可以是選用的 `SelectMany` 查詢，其後接著多個 `Select` 或 `Where` 運算子。

**LINQ Lambda 運算式**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**LINQ Lambda 運算式**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**LINQ Lambda 運算式**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**LINQ Lambda 運算式**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>巢狀
hello 語法`input.SelectMany(x=>x.Q())`其中 Q 是`Select`， `SelectMany`，或`Where`運算子。

在巢狀查詢中，hello 內部查詢是套用的 tooeach hello 外部集合項目。 有一個重要功能是該 hello 內部查詢可以參考 toohello 欄位 hello 集合中的元素 hello 外部像自我聯結。

**LINQ Lambda 運算式**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**LINQ Lambda 運算式**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**LINQ Lambda 運算式**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>執行 SQL 查詢
Cosmos DB 公開資源的方式是透過 REST API，任何能夠發出 HTTP/HTTPS 要求的語言都可呼叫此 API。 此外，Cosmos DB 還為數種熱門語言 (例如 .NET、Node.js、JavaScript 和 Python) 提供程式設計程式庫。 hello REST API 和 hello 所有的各種程式庫支援透過 SQL 查詢。 hello.NET SDK 支援 LINQ 查詢此外 tooSQL。

hello 下列範例顯示如何 toocreate 查詢並將它送出針對 Cosmos DB 資料庫帳戶。

### <a id="RestAPI"></a>REST API
Cosmos DB 提供透過 HTTP 的開放 RESTful 程式設計模型。 可以使用 Azure 訂用帳戶佈建資料庫帳戶。 hello Cosmos DB 資源模型包含一組帳戶資料庫，每一個都是可使用的邏輯與穩定 URI 定址的資源。 一組資源是參照的 tooas 本文件摘要。 資料庫帳戶包含一組資料庫，而每個資料庫都包含多個集合，且各集合因此會包含文件、UDF 和其他資源類型。

hello 基本互動模型，這些資源是透過 hello HTTP 動詞命令 GET、 PUT、 POST 和 DELETE 與標準解譯。 hello POST 動詞命令用來建立新的資源、 執行預存程序或發出 Cosmos DB 查詢。 查詢一律是唯讀作業，而且沒有任何副作用。

hello 下列範例顯示 DocumentDB API 查詢對集合，其中包含 hello 兩份範例文件到目前為止已檢閱過的文章。 hello 查詢會有一個簡單的篩選 hello JSON 名稱屬性上。 請記下的 hello hello 使用`x-ms-documentdb-isquery`和內容類型： `application/query+json` hello 作業的標頭 toodenote 是查詢。

**要求**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**結果**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


hello 第二個範例示範更複雜的查詢會傳回從 hello 聯結的多個結果。

**要求**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**結果**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


如果查詢的結果無法納入單一頁面的結果，則 hello REST API 會傳回接續 token，透過 hello`x-ms-continuation-token`回應標頭。 用戶端可以對結果分頁中後續的結果包含 hello 標頭。 每個分頁結果的 hello 數目也可以透過 hello`x-ms-max-item-count`標頭。 如果 hello 指定的查詢的彙總函式類似`COUNT`，然後 hello 查詢頁面可能傳回的結果 hello 頁面部分彙總的值。 hello 用戶端必須透過這些結果 tooproduce hello 最終結果，例如執行第二個層級彙總、 加總 hello 傳回 hello 個別頁面 tooreturn hello 總計數的計數。

查詢，使用 hello toomanage hello 資料一致性原則`x-ms-consistency-level`REST API 的所有要求標頭。 工作階段一致性，就需要的 tooalso 回應 hello 最新`x-ms-session-token`hello 查詢要求的 Cookie 標頭。 hello 查詢的集合的編製索引原則可能也會影響查詢結果的 hello 一致性。 Hello 預設檢索原則設定，針對集合 hello 索引一定是目前與 hello 文件內容和查詢結果符合 hello 選擇資料的一致性。 如果 hello 檢索原則是比較不嚴謹的 tooLazy，查詢可以傳回過時的結果。 如需詳細資訊，請參閱 [Azure Cosmos DB 的一致性層級][consistency-levels]。

如果設定的 hello hello 集合上的編製索引原則無法支援 hello 指定的查詢，hello Azure Cosmos DB 伺服器就會傳回 400 「 不正確的要求 」。 針對範圍查詢 (針對雜湊 (相等) 查閱所設定的路徑) 以及明確地排除不進行編製索引的路徑，會傳回此訊息。 hello`x-ms-documentdb-query-enable-scan`標頭無法使用索引時，可以是指定的 tooallow hello 查詢 tooperform 掃描。

您也可以設定於查詢執行取得詳細的度量`x-ms-documentdb-populatequerymetrics`標頭太`True`。 如需詳細資訊，請參閱[適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢計量](documentdb-sql-query-metrics.md)。

### <a id="DotNetSdk"></a>C# (.NET) SDK
hello.NET SDK 支援 LINQ 和 SQL 查詢。 hello 下列範例顯示如何 tooperform hello 簡單的篩選條件查詢早導入這份文件。

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


此範例會比較每個文件內的兩個屬性是否相等，以及使用匿名投射。 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


hello 下一個範例顯示聯結，透過 LINQ SelectMany 表示。

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



hello.NET 用戶端自動逐一查看查詢結果，如上所示的 hello foreach 區塊中的所有 hello 頁面。 hello 查詢 hello REST API > 一節中導入的選項也會出現在 hello.NET SDK 使用 hello`FeedOptions`和`FeedResponse`hello CreateDocumentQuery 方法中的類別。 可以使用 hello 控制 hello 頁數`MaxItemCount`設定。 

您可以建立，以同時也可以明確控制分頁`IDocumentQueryable`使用 hello`IQueryable`物件，然後藉由讀取` ResponseContinuationToken`值並將其傳遞回為`RequestContinuationToken`中`FeedOptions`。 `EnableScanInQuery`可設定 tooenable 掃描 hello 查詢無法支援所設定的 hello 編製索引原則時。 對於資料分割的集合，您可以使用`PartitionKey`toorun hello 查詢針對單一資料分割 （雖然 Cosmos DB 可以自動擷取此從 hello 查詢文字），和`EnableCrossPartitionQuery`toorun 查詢可能需要 toobe 執行多個資料分割。 

請參閱太[Azure Cosmos DB 的.NET 範例](https://github.com/Azure/azure-documentdb-net)如需其他範例包含查詢。 

### <a id="JavaScriptServerSideApi"></a>JavaScript 伺服器端 API
Cosmos DB 提供程式設計模型使用預存程序和觸發程序的 hello 集合上直接執行 JavaScript 為基礎的應用程式邏輯。 hello JavaScript 邏輯在集合層級註冊可以再發出 hello 文件的指定集合的 hello hello 作業的資料庫作業。 這些作業會包裝在環境 ACID 交易中。

hello 下列範例示範如何在 hello JavaScript 伺服器 API toomake toouse hello queryDocuments 查詢從內部預存程序和觸發程序。

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>參考
1. [簡介 tooAzure Cosmos DB][introduction]
2. [Azure Cosmos DB SQL 規格](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Azure Cosmos DB .NET 範例](https://github.com/Azure/azure-documentdb-net)
4. [Azure Cosmos DB 一致性層級][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. Javascript 規格 [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. 大型資料庫的查詢評估技術 [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. 平行關聯式資料庫系統中的查詢處理 (IEEE Computer Society Press，1994 年)
11. Lu, Ooi, Tan, 平行關聯式資料庫系統中的查詢處理 (IEEE Computer Society Press，1994 年)。
12. Christopher Olston、Benjamin Reed、Utkarsh Srivastava、Ravi Kumar、Andrew Tomkins：Pig Latin：資料處理的 Not-So-Foreign 語言，SIGMOD 2008。
13. G. Graefe。 hello 串聯，聯集的架構，會在查詢最佳化。 IEEE Data Eng. Bull., 18(3): 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md