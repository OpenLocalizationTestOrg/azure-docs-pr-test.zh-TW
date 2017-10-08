---
title: "aaaAzure Cosmos DB 做為索引鍵值存放區 – 成本概觀 |Microsoft 文件"
description: "深入了解 hello 很低成本使用 Azure Cosmos DB 做為索引鍵值存放區。"
keywords: "金鑰值存放區"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>Azure Cosmos DB 做為金鑰值存放區 – 成本概觀

Azure Cosmos DB 是全域散發的多模型資料庫服務，可用來輕鬆建置具高可用性的大規模應用程式。 根據預設，Azure Cosmos DB 會自動索引它內嵌，有效率地所有 hello 資料。 這樣可在任何種類的資料上進行快速且一致的 [SQL](documentdb-sql-query.md) (和 [JavaScript](programming.md)) 查詢。 

本文章描述簡單寫入 Azure Cosmos DB hello 成本，並使用做為索引鍵/值存放區時，讀取作業。 寫入作業包括文件的插入、取代、刪除和更新插入。 除了保證 99.99%的高可用性，保證 Azure Cosmos DB 優惠 < 10 毫秒延遲讀取和 < hello （索引） 的 15 ms 延遲寫入分別在 hello 99th 百分位數。 

## <a name="why-we-use-request-units-rus"></a>為什麼我們要使用「要求單位」(RU)

Azure DB Cosmos 效能根據 hello 金額佈建[要求單位](request-units.md)(RU) hello 磁碟分割。 hello 佈建第二個資料粒度是和購買的俄文/sec] 與 [RUs/分鐘 ([不 toobe hello 每小時計費的問題感到困惑](https://azure.microsoft.com/pricing/details/cosmos-db/))。 RUs 應視為貨幣，可簡化 hello 佈建的 hello 應用程式所需的輸送量。 我們的客戶不需要 toothink 區別的讀取和寫入容量單位。 RUs hello 單一貨幣模型建立效率 tooshare 佈建的 hello 容量之間讀取和寫入。 此模型中佈建的容量可讓 hello 服務 tooprovide 可預測且一致的輸送量、 低延遲及高可用性保證。 最後，我們使用 RU toomodel 輸送量，但每個已佈建的 RU 也有定義的資源 （記憶體、 核心） 量。 RU/秒不只是 IOPS。

做為全域分散式的資料庫系統，Cosmos DB 是 hello 加法 toohigh 可用性中提供 SLA 延遲、 輸送量和一致性，只有 Azure 的服務。 您佈建的 hello 輸送量為套用的 tooeach 的 hello 與您的 Cosmos DB 資料庫帳戶相關聯的區域。 Cosmos DB 針對讀取，提供多個定義完善[一致性層級](consistency-levels.md)toochoose 從的。 

hello 下表顯示 hello 數目 RUs 必要的 tooperform 讀取和寫入根據文件大小 1 KB 到 100KBs 的交易。

|項目大小|1 次讀取|1 次寫入|
|-------------|------|-------|
|1 KB|1 RU|5 RU|
|100 KB|10 RU|50 RU|

## <a name="cost-of-reads-and-writes"></a>讀取和寫入的成本

如果您佈建 1,000 RU/秒，這數量 too3.6m RU/小時，並需要成本 $0.08 hello 小時 （在 hello 美國和歐洲）。 針對 1KB 大小的文件，這表示以您的佈建輸送量，您將會使用 3.6 百萬次讀取或 0.72 百萬次寫入 (3.6 百萬 RU / 5)。 正規化的 toomillion 讀取和寫入，hello 成本是 $0.022 /m 讀取 ($0.08 / 3.6) 和 m $0.111/寫入 ($0.08 / 0.72)。 每次成本 hello 1 千萬會變成最少 hello 下表所示。

|項目大小|1 百萬次讀取|1 百萬次寫入|
|-------------|-------|--------|
|1 KB|$0.022|$0.111|
|100 KB|$0.222|$1.111|


大部分的 hello 基本 blob 或物件儲存區服務費用 $0.40 每百萬個的讀取的交易和 $5 每百萬個寫入交易。 如果使用以最佳方式，Cosmos DB 可以 too98%成本比這些其他解決方案 （如 1 KB 的交易）。

## <a name="next-steps"></a>後續步驟

敬請期待最佳化 Azure Cosmos DB 資源佈建的新文章。 在同時，hello 覺得可用 toouse 我們[RU 計算機](https://www.documentdb.com/capacityplanner)。

