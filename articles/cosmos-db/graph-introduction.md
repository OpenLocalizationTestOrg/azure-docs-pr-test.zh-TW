---
title: "簡介 tooAzure Cosmos DB Graph Api |Microsoft 文件"
description: "了解如何使用 Azure Cosmos DB toostore、 查詢和周遊大量圖形使用 hello hello Gremlin 圖形的查詢語言 Apache TinkerPop 的低延遲。"
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>簡介 tooAzure Cosmos DB: Graph API

[Azure Cosmos DB](introduction.md)是 hello 關鍵任務應用程式的 Microsoft 全域散發、 多模型資料庫服務。 提供 azure Cosmos DB[周全全域發佈](distribute-data-globally.md)，[彈性調整的輸送量與儲存體](partition-data.md)hello 99th 百分位數 在全球、 單一位數毫秒延遲[五個定義完善的一致性層級](consistency-levels.md)，而保證其高可用性，備份所[領先業界的 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)。 Azure Cosmos DB[自動索引資料](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)而不需要使用結構描述與索引管理 toodeal。 它是多重模型，可支援文件、索引鍵/值、圖表和單欄式資料模型。

![Gremlin、圖表和 Azure Cosmos DB](./media/graph-introduction/graph-gremlin.png)

hello Azure Cosmos DB Graph API 提供：

- 圖形模型化
- 周遊 API
- 周全的全域散發
- 少於 15 毫秒在 hello 99th 百分位數小於 10 毫秒延遲的讀取與儲存體和輸送量的彈性調整
- 透過立即查詢可用性自動編製索引
- 可調式一致性層級
- 完整的 SLA (包括 99.99% 可用性)

tooquery Azure Cosmos DB，您可以使用 hello [Apache TinkerPop](http://tinkerpop.apache.org)圖形周遊語言[Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps)，或是其他 TinkerPop 相容的圖形系統，像是[Apache Spark GraphX](spark-connector-graph.md).

這篇文章提供 hello Azure Cosmos DB Graph API 的概觀，並說明如何使用它 toostore 大量圖形使用數十億個頂點和邊緣。 您可以查詢毫秒延遲 hello 圖形，並輕鬆地持續改進 hello 圖形結構與結構描述。

## <a name="graph-database"></a>圖形資料庫
資料出現在 hello 真實世界自然連接。 傳統的資料模型化著重於實體。 對於許多應用程式，另外還有需要 toomodel 或 toomodel 實體和關聯性自然。

[圖形](http://mathworld.wolfram.com/Graph.html)是由[頂點](http://mathworld.wolfram.com/GraphVertex.html)和[邊緣](http://mathworld.wolfram.com/GraphEdge.html)組成的結構。 頂點和邊緣的屬性數量不限。 頂點代表特定的物件，例如人員、地點或事件。 邊緣代表頂點之間的關聯性。 比方說，某個人可能會知道其他人、參與某個事件，以及在最近前往某個位置。 屬性會快速 hello 頂點和邊緣的相關資訊。 屬性的例子包括具有名稱、年齡的頂點，以及具有時間戳記和/或加權的邊緣。 更正式的說，這種模型稱為[屬性圖表](http://tinkerpop.apache.org/docs/current/reference/#intro)。 Azure Cosmos DB 支援 hello 屬性圖形模型。

例如，hello 以下的範例使用者、 行動裝置、 興趣，與作業系統之間的圖形顯示關聯性。

![顯示人員、裝置和興趣的範例資料庫](./media/graph-introduction/sample-graph.png)

圖形會很有用 toounderstand 各種科學、 技術和商務中的資料集。 圖表資料庫可讓您自然又有效率地模型化和儲存圖表，很適合在許多案例中使用。 圖表資料庫通常是 NoSQL 資料庫，因為這些使用案例通常也需要結構描述彈性及快速的反覆運算。

圖表提供一種新穎又強大的資料模型化技術。 但此事本身並不足夠理由 toouse 圖形資料庫。 在許多涉及圖表周遊的使用案例和模式中，圖表遠遠勝過傳統的 SQL 和 NoSQL 資料庫。 在周遊多個關聯性時，例如好友的好友，此效能差異會更明顯。

您可以結合圖形演算法，深度優先搜尋、 廣度優先搜尋和 Dijkstra 的演算法、 社交網路、 內容管理、 geospatial，等各種網域中的 toosolve 問題等 hello 圖形資料庫提供的快速周遊和建議。

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>行星級圖表與 Azure Cosmos DB
Azure Cosmos DB 是完全受管理的圖形資料庫提供全域通訊群組，彈性的儲存體和輸送量、 自動編製索引和查詢，可微調的一致性層級，以及支援 hello TinkerPop 標準縮放比例。  

![Azure Cosmos DB 圖表架構](./media/graph-introduction/cosmosdb-graph-architecture.png)

Azure Cosmos 資料庫提供 hello 下列區分的功能相比 hello 市場 tooother 圖形資料庫：

* 可彈性調整的輸送量和儲存體

 Hello 真實世界中的圖形需要 tooscale 超出單一伺服器 hello 產能。 Azure Cosmos DB 可讓您順暢地在多部伺服器之間調整圖表。 您也可以調整獨立根據存取模式圖形的 hello 輸送量。 Azure Cosmos DB 支援可調整 toovirtually 圖形資料庫無限制的儲存體大小和佈建的輸送量。

* 多重區域複寫

 Azure Cosmos DB 無障礙地複寫您與您的帳戶相關聯的圖形資料 tooall 區域。 複寫可讓您需要全域存取 toodata toodevelop 應用程式。 有其代價 hello 方面的一致性、 可用性和效能和相對應的擔保。 Azure Cosmos DB 能透過多路連接 API 提供透明的區域性容錯移轉。 Hello 地球上，您可以彈性地調整輸送量與儲存體。

* 以熟悉的 Gremlin 語法快速查詢和周遊

 儲存異質頂點和邊緣，並透過熟悉的 Gremlin 語法查詢這些文件。 Azure Cosmos DB 會利用高度並行、 無鎖定、 記錄檔結構化索引技術 tooautomatically 索引的所有內容。 這項功能可讓豐富的即時查詢，而不 hello 周遊需要 toospecify 結構描述提示、 次要索引或檢視表。 深入了解[使用 Gremlin 查詢圖形](gremlin-support.md)。

* 受到完整管理

 Azure Cosmos DB 排除 hello 需要 toomanage 資料庫和機器資源。 以完全受管理的 Microsoft Azure 服務，您執行不需要 toomanage 虛擬機器、 部署和設定軟體、 管理縮放比例，或處理複雜的資料層升級。 每個圖表都會自動備份，以防區域性失敗。 您可以輕鬆地新增 Azure Cosmos DB 帳戶，並在需要時佈建容量，將精力投注在應用程式，不用浪費時間來操作和管理資料庫。

* 自動編製索引

 根據預設，Azure Cosmos DB 自動編製索引的節點和邊緣 hello 圖形中的內的所有 hello 屬性而且不預期或要求任何結構描述或建立的次要索引。

* Apache TinkerPop 相容性

 Azure Cosmos DB 原生支援 hello 開放原始碼 Apache TinkerPop 標準，而且可以與其他 TinkerPop 啟用圖形系統整合。 因此，您可以輕鬆地從另一個圖表資料庫移轉，例如 Titan 或 Neo4j，或搭配圖表分析架構一起使用 Azure Cosmos DB，例如 [Apache Spark GraphX](spark-connector-graph.md)。

* 可調式一致性層級

 從五個妥善定義的一致性層級 tooachieve 最佳取捨是一致性與效能之間選取。 針對查詢和讀取作業，Azure Cosmos DB 提供五個不同的一致性層級：強式、限定過期、工作階段、一致的前置和最終。 這些細微且妥善定義的一致性層級可讓您 toomake 之間的一致性、 可用性和延遲的聲音利弊。 進一步了解[toomaximize 可用性及效能的 DocumentDB 使用一致性層級](consistency-levels.md)。

Azure Cosmos DB 也可以使用多個模型，例如文件和圖形，在 hello 相同的容器資料庫。 您可以使用文件集合 toostore 圖形資料與文件並存。 您可以使用這兩個 SQL 查詢，透過 JSON 和 Gremlin 查詢 tooquery hello 相同的資料，以圖形方式。

## <a name="getting-started"></a>開始使用
您可以使用 hello Azure 命令列介面 (CLI)，Azure Powershell，或 hello graph API toocreate Azure Cosmos DB 帳戶支援的 Azure 入口網站。 建立帳戶之後，hello Azure 入口網站提供服務端點，例如`https://<youraccount>.graphs.azure.com`，可針對 Gremlin 提供 WebSocket 前端。 您可以設定您 TinkerPop 相容的工具，例如 hello [Gremin 主控台](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console)，tooconnect toothis 端點和建置應用程式在 Java、 Node.js 或任何 Gremlin 用戶端驅動程式。

hello 下表顯示常用 Gremlin 驅動程式可讓您針對 Azure Cosmos DB:

| 下載 | 文件 |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.js](https://www.npmjs.com/package/gremlin) |[Github 上的 Gremlin-JavaScript](https://github.com/jbmusso/gremlin-javascript) |
| [Gremlin 主控台](https://tinkerpop.apache.org/downloads.html) |[TinkerPop 文件](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Azure Cosmos DB 也會提供.NET 程式庫具有 Gremlin 擴充方法，在 hello 之上[Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)透過 NuGet。 此程式庫提供的 「 在處理序 」 Gremlin 伺服器，您可以使用 tooconnect 直接 tooDocumentDB 資料分割。

| 下載 | 文件 |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)，您可以使用 hello Graph API toodevelop，並在本機測試，而不需要建立 Azure 訂用帳戶，或支付任何費用。 當您滿意 hello 模擬器中您的應用程式運作時，您可以切換 toousing hello 雲端中的 Azure Cosmos DB 帳戶。

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Azure Cosmos DB 的圖表支援案例
以下是某些可以使用 Azure Cosmos DB 圖表支援的案例︰

* 社交網路

 藉由結合客戶相關資料和他們與其他人的互動，您可以開發個人化體驗、預測客戶行為，或將興趣雷同的人們聯繫在一起。 Azure Cosmos DB 可以使用的 toomanage 社交網路和追蹤客戶的喜好設定和資料。

* 推薦引擎

 此案例中通常會使用 hello 零售產業中。 藉由結合產品、使用者和使用者互動的相關資訊，例如購物、瀏覽或商品評價，您可以建立自訂的推薦。 hello 低延遲、 彈性延展，與原生支援 Azure Cosmos DB 圖形非常適合用來模型化這些互動。

* 地理空間

 電信、 邏輯和旅遊計劃中的許多應用程式需要 toofind 感興趣的區域內的位置，或兩個位置之間找出 hello 最短/最佳路線。 Azure Cosmos DB 很自然地可以解決這些問題。

* 物聯網

 Hello 網路和以圖形方式建立模型的 IoT 裝置之間的連線，您可以建置進一步了解您的裝置與資產的 hello 狀態，並了解如何 hello 網路的一個部分中的變更可能會影響另一個組件。

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解 graph 支援在 Azure Cosmos DB，請參閱：

* 開始使用 hello [Azure Cosmos DB 圖形教學課程](create-graph-dotnet.md)。
* 深入了解如何太[查詢圖形中使用 Gremlin Azure Cosmos DB](gremlin-support.md)。
