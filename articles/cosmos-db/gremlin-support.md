---
title: "aaaAzure Cosmos DB Gremlin 支援 |Microsoft 文件"
description: "深入了解 hello Gremlin 語言從 Apache TinkerPop 功能和步驟，而且可在 Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Azure Cosmos DB Gremlin graph 支援
Azure Cosmos DB 支援 [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps) \(英文\)，該圖形 API 是 [Apache Tinkerpop](http://tinkerpop.apache.org) \(英文\) 的圖形周遊語言，可用於建立圖表實體和執行圖表查詢作業。 您可以使用 hello Gremlin 語言 toocreate 圖形實體 （頂點和邊緣），修改這些實體內的屬性、 執行查詢和周遊，並刪除實體。 

Azure Cosmos DB 企業功能 toograph 會使資料庫變成。 其中包括全域散發、獨立調整儲存體和輸送量、可預測的個位數毫秒延遲、自動編製索引，以及 99.99% 的 SLA。 由於 Azure Cosmos DB 支援 TinkerPop/Gremlin，您可以輕鬆地移轉使用圖形的另一個資料庫，而不需要變更 toomake 程式碼撰寫的應用程式。 此外，憑藉 Gremlin 支援，Azure Cosmos DB 與啟用 TinkerPop 的分析架構緊密整合，例如 [Apache Spark GraphX](http://spark.apache.org/graphx/)。 

在本文中，我們提供快速的 Gremlin，逐步解說，並列舉 hello Gremlin 功能和支援的 Graph API 支援的 hello 預覽中的步驟。

## <a name="gremlin-by-example"></a>Gremlin 範例
我們將使用的查詢可以表示方式 Gremlin 範例圖形 toounderstand。 hello 下圖顯示商務應用程式管理使用者、 興趣及圖形的 hello 表單中的裝置相關資料。  

![顯示人員、裝置和興趣的範例資料庫](./media/gremlin-support/sample-graph.png) 

此圖表具有下列端點類型 （稱為 「 標籤 」 中 Gremlin） hello:

- 人員： hello 圖形有三個循環配置資源、 Thomas、 和 Ben 的人員
- 他們的興趣，請在此範例中，hello Football 遊戲的興趣：
- 人們會使用的裝置： hello 裝置
- 作業系統： hello hello 裝置作業系統上執行

我們代表 hello hello 遵循邊緣類型標籤透過這些實體之間的關聯性：

- 認識︰例如，「Thomas 認識 Robin」
- 有興趣： toorepresent hello 興趣的 hello 我們圖形中的人員，比方說，「 Ben 」 興趣足球
- RunsOS： 膝上型電腦執行 Windows OS hello
- 用法： toorepresent 個人的裝置使用。 例如，Robin 使用序號 77 的 Motorola 手機

針對使用 hello 此圖表，我們先執行某些作業[Gremlin 主控台](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console)。 您也可以執行這些作業 （Java、 Node.js、 Python 或.NET） 您選擇的 hello 平台中使用 Gremlin 驅動程式。  在探討 Azure Cosmos DB 中支援的項目之前，讓我們看看一些範例 tooget 熟悉 hello 語法。

首先，讓我們看看 CRUD。 hello 下列 Gremlin 陳述式會插入 hello"Thomas"頂點 hello 圖形：

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

接下來，hello Gremlin 陳述式之後插入 「 知道 」 的邊緣 Thomas 之間循環配置資源。

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

hello 下列查詢會傳回 hello"person"頂點其名字的遞減順序：
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

其中圖形發亮是當您需要 tooanswer 問題，例如 「 不要 Thomas friend 將用於哪些作業系統？"。 您可以從 hello graph 執行這個簡單的 Gremlin 周遊 tooget 該資訊：

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
現在，讓我們看看 Azure Cosmos DB 為 Gremlin 開發人員提供什麼功能。

## <a name="gremlin-features"></a>Gremlin 功能
TinkerPop 是一套涵蓋各種圖表技術的標準。 因此，它擁有標準術語 toodescribe 圖形提供者所提供哪些功能。 Azure Cosmos DB 提供持續、高度並行、可寫入的圖表資料庫，可分割至多個伺服器或叢集。 

hello 下表列出由 Azure Cosmos DB 實作 hello TinkerPop 功能： 

| 類別 | Azure Cosmos DB 實作 |  注意事項 | 
| --- | --- | --- |
| Graph 功能 | 在預覽中提供 Persistence 和 ConcurrentAccess。 設計的 toosupport 交易 | 電腦的方法可以實作透過 hello Spark 連接器。 |
| 變數功能 | 支援布林值、整數、位元組、Double、Float、整數、Long、字串 | 支援基本類型、透過資料模型而與複雜類型相容 |
| 頂點功能 | 支援 RemoveVertices、MetaProperties、AddVertices、MultiProperties、StringIds、UserSuppliedIds、AddProperty、RemoveProperty  | 支援建立、修改和刪除端點 |
| 頂點屬性功能 | StringIds、UserSuppliedIds、AddProperty、RemoveProperty、BooleanValues、ByteValues、DoubleValues、FloatValues、IntegerValues、LongValues、StringValues | 支援建立、修改和刪除頂點屬性 |
| 邊緣功能 | AddEges、RemoveEdges、StringIds、UserSuppliedIds、AddProperty、RemoveProperty | 支援建立、修改和刪除邊緣 |
| 邊緣屬性功能 | Properties、BooleanValues、ByteValues、DoubleValues、FloatValues、IntegerValues、LongValues、StringValues | 支援建立、修改和刪除邊緣屬性 |

## <a name="gremlin-wire-format-graphson"></a>Gremlin 電傳格式︰GraphSON

Azure 的 Cosmos DB 使用 hello [GraphSON 格式](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format)Gremlin 作業傳回的結果時。 GraphSON 是 hello Gremlin 標準格式來表示頂點，邊緣，並使用 JSON 屬性 （單一和多重值屬性）。 

例如，hello 下列程式碼片段顯示的頂點 GraphSON 表示*傳回 toohello 用戶端*從 Azure Cosmos DB。 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

hello 下列 GraphSON 用於頂點 hello 屬性︰

| 屬性 | 說明 |
| --- | --- |
| id | hello 識別碼 hello 頂點。 必須是唯一的 （在組合的 hello 值 _partition 如果適用） |
| 標籤 | hello 頂點的 hello 標籤。 這是選擇性的並使用 toodescribe hello 實體類型。 |
| 類型 | 使用的 toodistinguish 頂點從非圖形文件 |
| 屬性 | 使用者定義相關聯的屬性與 hello 頂點的封包。 每個屬性可以有多個值。 |
| _partition (可設定) | hello hello 頂點的資料分割索引鍵。 可以是使用圖表 tooscale toomultiple 伺服器 |
| outE | 這包含頂點的外邊緣清單。 儲存與頂點 hello 相鄰關係資訊可以周遊的執行速度。 邊緣會根據標籤而分組。 |

和 hello 邊緣包含下列資訊 toohelp 與瀏覽 tooother 部份 hello 圖形的 hello。

| 屬性 | 說明 |
| --- | --- |
| id | hello 識別碼 hello 邊緣。 必須是唯一的 （在組合的 hello 值 _partition 如果適用） |
| 標籤 | hello hello 邊緣標籤。 這個屬性是選擇性的並使用 toodescribe hello 關聯性類型。 |
| inV | 這包含特定邊緣的頂點清單。 Hello 邊緣儲存 hello 相鄰關係資訊可以周遊的執行速度。 頂點會根據標籤而分組。 |
| 屬性 | 使用者定義相關聯的屬性，與 hello 封包。 每個屬性可以有多個值。 |

每個屬性可以將多個值儲存在陣列中。 

| 屬性 | 說明 |
| --- | --- |
| value | hello hello 屬性值

## <a name="gremlin-partitioning"></a>Gremlin 分割

在 Azure Cosmos DB 中，圖表儲存在容器內，而容器可根據儲存體和輸送量 (以一般化每秒要求數表示) 而獨立調整。 每個容器必須定義一個選擇性但建議的資料分割索引鍵屬性，以決定相關資料的邏輯資料分割界限。 每個頂點/邊緣都必須有一個 `id` 屬性，此屬性在該資料分割索引鍵值內的實體之間是唯一的。 hello 詳細資料將會涵蓋[分割在 Azure Cosmos DB](partition-data.md)。

對於 Azure Cosmos DB 中跨越多個資料分割的圖形資料，Gremlin 作業可以順暢地運作。 不過，建議使用 toochoose 資料分割索引鍵，做為篩選條件，在查詢中，通常用於圖形具有許多相異值，以及類似的頻率存取這些值。 

## <a name="gremlin-steps"></a>Gremlin 步驟
現在讓我們看看 hello 受到 Azure Cosmos DB Gremlin 步驟。 如需 Gremlin 的完整參考，請參閱 [TinkerPop 參考](http://tinkerpop.apache.org/docs/current/reference)。

| 步驟 | 說明 | TinkerPop 3.2 文件 | 注意事項 |
| --- | --- | --- | --- |
| `addE` | 在兩個頂點之間新增邊緣 | [addE 步驟](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | 將頂點 toohello 圖形 | [addV 步驟](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest 所有 hello 周遊都傳回值 | [and 步驟](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | 步驟調變器 tooassign 變數 toohello 步驟輸出的 | [as 步驟](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | 搭配 `group` 和 `order` 一起使用的步驟調變器 | [by 步驟](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | 傳回 hello 傳回結果的第一個周遊 | [coalesce 步驟](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | 傳回常數值。 搭配 `coalesce` 使用| [constant 步驟](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | 傳回從 hello 周遊 hello 計數 | [count 步驟](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | 傳回移除重複項的 hello hello 值 | [dedup 步驟](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | 卸除 hello 值 （頂點/邊） | [drop 步驟](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | 做為計算 hello 彙總結果的屏障| [fold 步驟](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | 群組 hello 指定 hello 標籤為基礎的值| [group 步驟](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | 使用 toofilter 屬性、 頂點，以及邊緣。 支援 `hasLabel`、`hasId`、`hasNot` 和 `has` 變體。 | [has 步驟](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | 將值插入資料流| [inject 步驟](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | 使用 tooperform 使用布林運算式篩選 | [is 步驟](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | 用於 hello 周遊 toolimit 項目數目| [limit 步驟](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | 本機包裝一段周遊，類似 tooa 子查詢 | [local 步驟](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | 使用 tooproduce hello 否定篩選 | [not 步驟](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | 傳回 hello 的 hello 指定結果周遊，如果它所產生它所傳回的結果 else hello 呼叫項目 | [optional 步驟](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | 可確保至少一個 hello 周遊傳回值 | [or 步驟](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | 傳回結果中 hello 指定排序次序 | [order 步驟](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | 傳回 hello hello 周遊的完整路徑 | [path 步驟](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | 為對應的專案 hello 屬性 | [project 步驟](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Hello 傳回 hello 屬性指定標籤 | [properties 步驟](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | 篩選 toohello 指定值的範圍| [range 步驟](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Hello 的重複 hello 步驟指定的次數。 用於迴圈處理 | [repeat 步驟](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | 使用從 hello 周遊 toosample 結果 | [sample 步驟](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | 使用從 hello 周遊 tooproject 結果 |  [select 步驟](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | 用於非封鎖從 hello 周遊的彙總 | [store 步驟](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | 將頂點的路徑彙總至樹狀目錄 | [tree 步驟](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | 將迭代器展開為步驟| [unfold 步驟](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | 合併來自多個周遊的結果| [unfold 步驟](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | 包含所需的周遊頂點和邊緣之間的 hello 步驟`V`， `E`， `out`， `in`， `both`， `outE`， `inE`， `bothE`， `outV`， `inV`， `bothV`，和`otherV`的 | [vertex 步驟](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | 使用從 hello 周遊 toofilter 結果。 支援 `eq`、`neq`、`lt`、`lte`、`gt`、`gte` 和 `between` 運算子  | [where 步驟](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

根據預設，Azure Cosmos DB 的寫入最佳化引擎支援自動編製頂點和邊緣內所有屬性的索引。 因此，查詢具有篩選範圍查詢、 排序或彙總的任何屬性會處理從 hello 索引，並有效率地提供。 如需 Azure Cosmos DB 中索引運作方式的詳細資訊，請參閱[無從驗證結構描述的索引編製](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)一文。

## <a name="next-steps"></a>後續步驟
* [使用我們的 SDK](create-graph-dotnet.md) 開始建置圖表應用程式 
* 深入了解 [Azure Cosmos DB 的圖表支援](graph-introduction.md)
