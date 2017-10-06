---
title: "aaaIntroduction tooAzure Cosmos DB 的表格 API |Microsoft 文件"
description: "了解如何使用 Azure Cosmos DB toostore 和大量查詢使用低度延遲的索引鍵-值資料磁碟區 hello 受歡迎的 OSS MongoDB Api。"
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>簡介 tooAzure Cosmos DB： 表格 API

[Azure Cosmos DB](introduction.md) 是 Microsoft 全域發佈的多模型資料庫服務，適用於任務關鍵性應用程式。 提供 azure Cosmos DB[周全全域發佈](distribute-data-globally.md)，[彈性調整的輸送量與儲存體](partition-data.md)hello 99th 百分位數 在全球、 單一位數毫秒延遲[五個定義完善的一致性層級](consistency-levels.md)，而保證其高可用性，所有支援[領先業界的 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)。 Azure Cosmos DB[自動索引資料](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)而不需要使用結構描述與索引管理 toodeal。 它是多重模型，可支援文件、索引鍵/值、圖表和單欄式資料模型。 

![Azure 表格儲存體 API 和 Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

Azure 的 Cosmos DB 會提供 hello 資料表 API （預覽） 的應用程式，需要使用彈性的結構描述、 可預測的效能、 全域發佈和高輸送量的索引鍵-值存放區。 hello 表格 API 提供 hello 與 Azure 資料表儲存體，相同的功能但利用 hello hello Azure Cosmos 資料庫引擎的優點。 

您可以繼續 toouse 資料表具有高的儲存體與較低的輸送量需求的 Azure 資料表儲存體。 Azure Cosmos DB 將介紹支援儲存體最佳化的資料表，在未來的更新中，與現有和新的 Azure 資料表儲存體帳戶將會升級 tooAzure Cosmos DB。

## <a name="premium-and-standard-table-apis"></a>進階和標準資料表 API
如果您目前使用 Azure 資料表儲存體，您可以獲得下列優點移動 tooAzure Cosmos DB 的 「 高階資料表 」 預覽 hello:

|  | Azure 表格儲存體 | Azure Cosmos DB：表格儲存體 (預覽) |
| --- | --- | --- |
| 延遲 | 快速，但延遲沒有上限 | 單一位數表示毫秒延遲讀取和寫入，備份與 < 10 毫秒延遲讀取和 < 15 毫秒的延遲寫入在 hello 99th 百分位數 在 hello 世界各地的任何標尺， |
| Throughput | 高延展性，但不是專用的輸送量模型。 資料表每秒 20,000 個作業的延展性限制 | 高延展性且[每個資料表都有專用的保留輸送量](request-units.md) (由 SLA 支援)。 帳戶沒有輸送量上限，而且支援每個資料表每秒 > 1 千萬個作業 |
| 全域散發 | 具有一個選擇性 HA 可讀取次要讀取區域的單一區域。 您無法起始容錯移轉 | [周全全域發佈](distribute-data-globally.md)從一個 too30 + 區域，支援[自動和手動容錯移轉](regional-failover.md)在 hello 世界各地的任何時間 |
| 編製索引 | PartitionKey 和 RowKey 只有主要索引。 沒有次要索引 | 對所有屬性自動執行完整的編製索引，但沒有索引管理 |
| 查詢 | 查詢執行作業會使用主索引鍵的索引，要不然會進行掃描。 | 查詢可以利用自動編製屬性的索引，加快查詢速度。 Azure Cosmos DB 的資料庫引擎能夠支援彙總、地理空間以及排序。 |
| 一致性 | 主要區域達到「強一致性」，次要地區達到「最終一致性」 | [五個妥善定義的一致性層級](consistency-levels.md)tootrade 關閉可用性、 延遲、 輸送量和一致性根據您的應用程式需求 |
| 價格 | 儲存體最佳化  | 輸送量最佳化 |
| SLA | 99.9% 的可用性 | 在多個單一區域和能力 tooadd 99.99%可用性提高可用性的區域。 在一般可用性上達到[業界頂尖的全面性 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/) |

## <a name="how-tooget-started"></a>如何啟動 tooget

建立 hello Azure Cosmos DB 帳戶[Azure 入口網站](https://portal.azure.com)，並開始使用我們[表格 API 使用適用於.NET 的快速入門](create-table-dotnet.md)。 

## <a name="next-steps"></a>後續步驟

以下是一些您一開始的指標 tooget:
* [建置使用 hello 表格 API 的.NET 應用程式](create-table-dotnet.md)
* [開發以 hello.NET 中的資料表應用程式開發介面](tutorial-develop-table-dotnet.md)
* [使用 hello 表格 API 來查詢資料表資料](tutorial-query-table.md)
* [如何使用全域發佈 toosetup Azure Cosmos DB hello 表格 API](tutorial-global-distribution-table.md)
* [適用於 .NET 的 Azure Cosmos DB 資料表 API SDK](table-sdk-dotnet.md)
