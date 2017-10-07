---
title: "aaaIntroduction tooAzure Cosmos DB |Microsoft 文件"
description: "了解 Azure Cosmos DB。 這個全球散發的多模型資料庫是針對低延遲、彈性的延展性和高可用性所建置。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>歡迎使用 tooAzure Cosmos DB

Azure Cosmos DB 是 Microsoft 的全球散發多模型資料庫。 Hello 按一下按鈕，使用 Azure Cosmos DB 可讓您 tooelastically 和獨立延展輸送量與儲存體在任意數目的 Azure 地理區域。 它利用完整的[服務等級協定](https://aka.ms/acdbsla) (SLA) 提供了輸送量、延遲、可用性和一致性的保證，這是其他資料庫服務無法提供的。

![Azure Cosmos DB 是 Microsoft 的全球散發資料庫服務，包含彈性的相應放大、低延遲保證、五個一致性模型，以及完整保證的 SLA](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>受益於 Azure Cosmos DB 的解決方案

任何[web、 行動裝置、 遊戲和 IoT 應用程式](use-cases.md)上需要的 toohandle 大量的讀取和寫入[全域](distribute-data-globally.md)的各種不同的資料將受益於 Azure Cosmos DB 的低回應時間調整[保證](https://azure.microsoft.com/support/legal/sla/cosmos-db/)可用性、 高輸送量、 低延遲度及可微調的一致性。

## <a name="key-capabilities"></a>主要功能
為全域分散式的資料庫服務，Azure Cosmos DB 會提供下列功能 toohelp 建置可擴充、 高回應性的應用程式的 hello:

* **周全且立即可用的全域分散式資料庫**
    * 您可以[散發資料](distribute-data-globally.md)tooany 數目[Azure 區域](https://azure.microsoft.com/regions/)，以 hello[按鈕的按一下](tutorial-global-distribution-documentdb.md)。 這可讓您 tooput 其中您的使用者，請確保 hello 最低可能延遲 tooyour 客戶資料。 
    * 使用 Azure Cosmos DB 的多路連接的 Api，hello 應用程式一定會知道其中是 hello 最接近的區域，而將會傳送要求 toohello 最接近的資料中心。 這可能會有任何組態變更、 設定寫入區域和 rest 會為您處理許多讀取並 hello 的區域。

* **存取和查詢資料的多重資料模型與常用 API**
    * hello Azure Cosmos DB 上建立原生 atom 記錄順序 (ARS) 型的資料模型支援多個資料模型，包括但不是限於的 toodocument、 圖形、 索引鍵-值、 資料表和單欄式資料模型。
    * Sdk 提供多種語言支援下列資料模型的 hello 的 Api:
        * [DocumentDB API](documentdb-introduction.md)
        * [MongoDB API](mongodb-introduction.md)
        * [資料表 API](table-introduction.md)
        * [Graph (Gremlin) API](graph-introduction.md)
        * 其他資料模型即將登場 

* **全球性依需求彈性調整輸送量和儲存體**
    * 輕鬆地以[每秒](request-units.md)的細微度調整資料庫輸送量，並隨時依需求變更。 
    * 調整儲存體大小[以透明且自動](partition-data.md)toohandle now 及永遠您大小需求。

* **建置回應速度快和關鍵任務應用程式**
    * Azure Cosmos DB 可保證在 hello 的端對端低度延遲 99th 百分位數 tooits 客戶。 
    * 典型 1 KB 的項目，如 Cosmos DB 的讀取端對端延遲低於 10 毫秒與保證索引的寫入在 hello 99th 百分位數 底下 15 毫秒內 hello 相同 Azure 區域。 hello 中間延遲會大幅降低 （下 5 毫秒）。

* **確保「永遠可用」可用性**
    * 單一區域內的 99.99% 可用性。
    * 部署 tooany 數目[Azure 區域](https://azure.microsoft.com/regions)提高可用性。
    * 透過資料零遺失保證來[模擬一或多個區域的錯誤](regional-failover.md)。 

* **撰寫全域散發的應用程式，hello 以滑鼠右鍵的方式**
    * 五個[一致性模型](consistency-levels.md)模型提供廣泛的強式所有 hello 類似方式 tooNoSQL 的最終一致性，而且每個兩者之間的類似 SQL 的一致性。 
  
* **退款保證**
    * 保證快速取得您的資料，否則退款。 
    * 可用性、延遲、輸送量和一致性的[服務等級協定](https://aka.ms/acdbsla)。 

* **無資料庫結構描述/索引管理**
    * 不用再擔心維持您的資料庫結構描述和索引與您的應用程式結構描述之間的同步處理了。 我們完全不需要結構描述。 
    * Azure Cosmos 資料庫的資料庫引擎是完整的結構描述無關，因為它內嵌，而不需要任何結構描述或索引，並提供服務效能穩定的快速查詢的所有 hello 資料自動編製都索引。 

* **降低擁有權成本**
    * 五 tooten 次[更符合成本效益](https://aka.ms/cosmos-db-tco-paper)與未受管理的解決方案。
    * 比 DynamoDB 便宜三倍。

## <a name="capability-comparison"></a>功能比較

Azure 的 Cosmos DB 會提供 hello 的關聯式和非關聯式資料庫的最佳功能。

| 功能 | 關聯式資料庫   | 非關聯式 (NoSQL) 資料庫 |    Azure Cosmos DB |
| --- | --- | --- | --- |
| 全球發佈 | 否 | 否 | 是，在 30 個以上的區域中周全且立即可用的散發，具有多路連接的 API|
| 水平調整 | 否 | 是 | 是，您可以獨立調整儲存體和輸送量 | 
| 延遲保證 | 否 | 是 | 是，99% 的讀取 <10 毫秒和寫入 <15 毫秒 | 
| 高可用性 | 否 | 是 | 是，Cosmos DB 一律可用，具有 PACELC 取捨，並提供自動和手動容錯移轉選項|
| 資料模型 + API | 關聯式 + SQL | 多模型 + OSS API | 多模型 + SQL + OSS API (更多即將推出) |
| SLA | 是 | 否 | 是，延遲、輸送量、一致性、可用性的完整 SLA |


## <a name="next-steps"></a>後續步驟
透過下列其中一個快速入門開始使用 Azure Cosmos DB：

* [開始使用 Azure Cosmos DB 的 DocumentDB API](create-documentdb-dotnet.md)
* [開始使用 Azure Cosmos DB 的 MongoDB API](create-mongodb-nodejs.md)
* [開始使用 Azure Cosmos DB 的圖形 API](create-graph-dotnet.md)
* [開始使用 Azure Cosmos DB 的資料表 API](create-table-dotnet.md)
