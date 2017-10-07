---
title: "aaaAzure Cosmos DB 規模和效能測試 |Microsoft 文件"
description: "了解 tooperform 的調整規模和效能測試以 Azure Cosmos DB"
keywords: "效能測試"
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Azure Cosmos DB 的效能和規模測試
效能和規模測試是應用程式開發過程中的關鍵步驟。 對於許多應用程式，hello 資料庫層次都有重大影響 hello 整體效能和延展性，且因此效能的重要元件測試。 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是為了能夠彈性延展及獲得可預測的效能而建置，因此非常適合需要高效能資料庫層的應用程式。 

這篇文章適合做為針對其 Cosmos DB 工作負載實作效能測試套件或針對高效能應用程式案例評估 Cosmos DB 之開發人員的參考。 其主要著重在隔離的效能測試的 hello 資料庫，但也包含 實際執行應用程式的最佳作法。

閱讀這篇文章之後, 您將無法 tooanswer hello 下列問題：   

* 哪裡可以找到可供進行 Cosmos DB 效能測試的範例 .NET 用戶端應用程式？ 
* 如何藉由 Cosmos DB 從我的用戶端應用程式達到高輸送量層級？

tooget 啟動程式碼時，請下載 hello 專案從[Azure Cosmos DB 效能測試的範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)。 

> [!NOTE]
> 此應用程式的 hello 目標是 toodemonstrate 解壓縮從 Cosmos DB 更佳的效能較少的用戶端電腦的最佳作法。 這是不會進行 hello 服務，可以調整 limitlessly toodemonstrate hello 尖峰容量。
> 
> 

如果您要尋找用戶端設定選項 tooimprove Cosmos DB 的效能，請參閱[Azure Cosmos DB 效能祕訣](performance-tips.md)。

## <a name="run-hello-performance-testing-application"></a>執行 hello 效能測試應用程式
hello 最快方式 tooget 啟動，而且 toocompile 執行的 hello.NET 範例下, 面 hello 步驟中所述。 您也可以檢閱 hello 原始程式碼，並實作類似組態 tooyour 自己的用戶端應用程式。

**步驟 1:**下載 hello 專案從[Azure Cosmos DB 效能測試的範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)，或 「 分叉 」 hello GitHub 儲存機制。

**步驟 2:**修改的端點 Url、 AuthorizationKey、 CollectionThroughput 和 DocumentTemplate （選擇性） 在 App.config 中的 hello 設定。

> [!NOTE]
> 之前佈建具有高輸送量的集合，請參閱 toohello[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)tooestimate hello 成本，每個集合。 Azure 的 Cosmos db-storage 帳單和獨立每小時，因此您可以藉由刪除或降低 Azure Cosmos DB 集合 hello 輸送量測試後節省成本的輸送量。
> 
> 

**步驟 3:**編譯及執行 hello 主控台應用程式從 hello 命令列。 您應該會看到類似 hello 下列輸出：

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**步驟 4 （如有必要）：** hello 輸送量報告 （RU/秒） 從 hello 工具應該 hello 相同或高於 hello hello 集合的佈建的輸送量。 否則，請增加 hello DegreeOfParallelism 少量遞增的方式可協助您達到 hello。 如果您的用戶端應用程式中的 hello 輸送量會停滯不前，啟動 hello 應用程式的多個執行個體上 hello 相同或不同的電腦將協助您達到佈建的 hello hello 跨不同的執行個體。 如果您需要這個步驟的說明，請撰寫一封電子郵件tooaskcosmosdb@microsoft.com或提出支援票證從 hello [Azure 入口網站](https://portal.azure.com)。

一旦您擁有 hello 應用程式執行時，您可以嘗試不同[編製索引原則](indexing-policies.md)和[一致性層級](consistency-levels.md)toounderstand 其對輸送量和延遲的影響。 您也可以檢閱 hello 原始程式碼，並實作類似的設定 tooyour 自己的測試套件或實際執行應用程式。

## <a name="next-steps"></a>後續步驟
在這篇文章中，我們探討了如何使用 .NET 主控台應用程式來執行 Cosmos DB 的相關效能和規模測試。 請如需使用 Azure Cosmos DB 的詳細資訊，參閱下列 toohello 連結。

* [Azure Cosmos DB 效能測試範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [用戶端設定選項 tooimprove Azure Cosmos DB 效能](performance-tips.md)
* [Azure Cosmos DB 中的伺服器端資料分割](partition-data.md)


