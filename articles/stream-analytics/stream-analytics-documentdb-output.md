---
title: "aaaJSON 輸出資料流分析 |Microsoft 文件"
description: "了解「串流分析」如何將 Azure Cosmos DB 設定為 JSON 輸出的目標，以針對非結構化 JSON 資料進行資料封存和低延遲查詢。"
keywords: "JSON 輸出"
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>將 Azure Cosmos DB 設定為串流分析的 JSON 輸出目標
「串流分析」可以將 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) 設定為 JSON 輸出的目標，讓您能夠針對非結構化的 JSON 資料進行資料封存和低延遲查詢。 本文件涵蓋實作這種組態的一些最佳作法。

對於熟悉 Cosmos DB，看看[Azure Cosmos DB 的學習路徑](https://azure.microsoft.com/documentation/learning-paths/documentdb/)tooget 啟動。 

注意：目前不支援 Mongo DB API 架構的 Cosmos DB 集合。 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>將 Cosmos DB 設定為輸出目標的基本概念
hello Azure Cosmos DB 輸出資料流分析可讓您處理結果，作為 JSON 輸出 Cosmos DB 清查到的資料流寫入。 資料流分析不會建立集合在資料庫中，而需要 toocreate 預先它們。 這是使 hello 計費成本 Cosmos DB 集合被透明 tooyou，和一致性，直接使用集合的容量，讓您可以微調 hello 效能，hello [Cosmos DB Api](https://msdn.microsoft.com/library/azure/dn781481.aspx)。 我們建議使用每個資料流工作 toologically 單獨一個 Cosmos DB 資料庫的資料流工作集合。

部分 hello Cosmos DB 集合選項如下所述。

## <a name="tune-consistency-availability-and-latency"></a>微調一致性、 可用性及延遲
toomatch 應用程式的需求，Cosmos DB 可讓您 toofine 微調 hello 資料庫、 集合和請之間的利弊得失一致性、 可用性和延遲。 您可以視案例針對讀取與寫入延遲所需的讀取一致性層級，來選擇資料庫帳戶上的一致性層級。 也根據預設，Cosmos DB 可讓每個 CRUD 作業 tooyour 集合上的索引同步。 這是另一個有用的選項 toocontrol hello 寫入/讀取 Cosmos DB 中的效能。 如需本主題的詳細資訊，請檢閱 hello[變更資料庫，然後查詢一致性層級](../documentdb/documentdb-consistency-levels.md)發行項。

## <a name="upserts-from-stream-analytics"></a>來自串流分析的 Upsert
以 Cosmos DB 的資料流分析整合可讓您 tooinsert 或更新記錄 Cosmos DB 集合根據指定的文件識別碼資料行中。 這也是參考的 tooas *Upsert*。

資料流分析會利用開放式 Upsert 做法，更新會只因為 tooa 文件識別碼衝突的插入失敗時。 此更新是由執行資料流分析為修補程式時，所以它可以讓部分更新 toohello 文件，也就是加上新的屬性或取代現有的屬性會以累加方式執行。 請注意，在 hello JSON 文件中的陣列內容值中的變更會導致 hello 整個陣列取得覆寫，也就是 hello 陣列不會進行合併。

## <a name="data-partitioning-in-cosmos-db"></a>Cosmos DB 中的資料分割
Cosmos DB[分割集合](../cosmos-db/partition-data.md)是建議的方法來將資料分割的 hello。 

對於單一 Cosmos DB 集合，串流分析仍可讓您 toopartition hello 查詢模式和應用程式的效能需求依據您的資料。 每個集合可能包含總 too10GB 的資料 （最大值），且目前沒有任何方式 tooscale 總 （或溢位） 集合。 向外延展，串流分析可讓您指定的前置詞 toowrite toomultiple 集合 （請參閱下方的使用方式詳細資料）。 串流分析會一致 hello[雜湊資料分割的解析程式](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx)hello 使用者為基礎的策略提供 PartitionKey 資料行 toopartition 其輸出記錄。 hello 以 hello hello 串流工作的開始時間在指定前置詞的集合數目做 hello 輸出資料分割計數，toowhich hello 工作寫入 tooin 平行 (Cosmos DB 集合 = 輸出資料分割)。 對於延遲索引只進行插入的單一集合，預期會有約每秒 0.4 MB 的寫入輸送量。 使用多個集合，可以讓您 tooachieve 較高的輸送量和更高的容量。

如果您在未來的 hello 想 tooincrease hello 資料分割計數，您可能需要 toostop 您的工作，重新分割 hello 資料從現有的集合成新的集合，然後再重新啟動 hello 資料流分析工作。 有關使用 PartitionResolver 與重新分割的詳細資料，以及範例程式碼，都會包含在後續的文章中。 hello 文章[資料分割和 Cosmos DB 中的縮放比例](../documentdb/documentdb-partition-data.md)也提供此詳細資料。

## <a name="cosmos-db-settings-for-json-output"></a>適用於 JSON 輸出的 Cosmos DB 設定
如果在「串流分析」中建立 Cosmos DB 作為輸出，將會產生如以下所示的資訊提示。 本節中的 hello 屬性定義的說明。

資料分割的集合 | 多個「單一資料分割」集合
---|---
![documentdb 串流分析輸出畫面](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![documentdb 串流分析輸出畫面](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> hello**多個 「 單一分割 」 集合**案例需要資料分割索引鍵，而且是支援的設定。 

* **輸出別名**– ASA 查詢中此輸出別名 toorefer  
* **帳戶名稱**– hello 名稱或端點的 hello Cosmos DB 帳戶的 URI。  
* **帳戶金鑰**– hello hello Cosmos DB 帳戶的共用的存取金鑰。  
* **資料庫**– hello Cosmos DB 資料庫名稱。  
* **集合名稱模式**– hello 集合名稱或其 hello 集合 toobe 使用模式。 可使用 hello {partition} 語彙基元，資料分割會從 0 開始建構 hello 集合名稱格式。 以下是有效的範例輸入：  
  1\) MyCollection – 必須要有一個名為 “MyCollection” 的集合存在。  
  2\) MyCollection{partition} – 這些集合必須存在 – "MyCollection0”、“MyCollection1”、“MyCollection2” 等，依此類推。  
* **資料分割索引鍵** - 選擇性。 只有當您在集合名稱模式中使用 {parition} 語彙基元時，才需要此索引鍵。 hello 輸出使用事件 toospecify hello 機碼中跨集合分割輸出的 hello 欄位名稱。 若為單一集合輸出，則可使用任何任意的輸出欄，例如 PartitionId。  
* **文件識別碼** ：可省略。 使用 toospecify hello 主索引鍵的 insert 或 update 作業所根據的輸出事件中的 hello 欄位 hello 名稱。  
