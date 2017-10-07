---
title: "簡介 tooAzure Cosmos DB: API for MongoDB。 |Microsoft 文件"
description: "了解如何使用 Azure Cosmos DB toostore 和查詢的 JSON 文件具有低度延遲使用大量磁碟區 hello 受歡迎的 OSS MongoDB Api。"
keywords: "MongoDB 是什麼"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>簡介 tooAzure Cosmos DB: API for MongoDB。

[Azure Cosmos DB](../cosmos-db/introduction.md) 是 Microsoft 全域發佈的多模型資料庫服務，適用於任務關鍵性應用程式。 提供 azure Cosmos DB[周全全域發佈](distribute-data-globally.md)，[彈性調整的輸送量與儲存體](partition-data.md)hello 99th 百分位數 在全球、 單一位數毫秒延遲[五個定義完善的一致性層級](consistency-levels.md)，而保證其高可用性，所有支援[領先業界的 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)。 Azure Cosmos DB[自動索引資料](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)而不需要使用結構描述與索引管理 toodeal。 它是多重模型，可支援文件、索引鍵/值、圖表和單欄式資料模型。 

![Azure Cosmos DB：MongoDB API](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Cosmos DB 資料庫可以當做 hello 資料存放區針對所撰寫的應用程式[MongoDB](https://docs.mongodb.com/manual/introduction/)。 這表示，使用現有的[驅動程式](https://docs.mongodb.org/ecosystem/drivers/)，針對 MongoDB 所撰寫的應用程式現在可與 Cosmos DB 通訊，並使用 Cosmos DB 資料庫而非 MongoDB 資料庫。 在許多情況下，您可以切換使用 MongoDB tooCosmos DB 只要變更連接字串。 使用這項功能，您可以輕鬆建置和執行的 MongoDB 資料庫應用程式，在 hello Azure 雲端與 Azure Cosmos DB 的全域發佈和[完整業界領先的 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db)，同時繼續 toouse 熟悉技術和工具 for MongoDB。


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>使用 Azure Cosmos DB MongoDB 應用程式的 hello 優點為何？

**可彈性擴充的輸送量與儲存體：**輕鬆地向上延展或向您 MongoDB 資料庫 toomeet 需要您的應用程式。 您的資料會儲存在固態硬碟 (SSD) 中以便獲得可預測的低延遲。 Cosmos DB 支援可調整 toovirtually MongoDB 集合無限制的儲存體大小和佈建的輸送量。 隨著應用程式的成長，您可以依據可預測的效能彈性且順暢地調整 Cosmos DB。 

**多區域複寫：** Cosmos DB 會明確地將複寫您資料 tooall 區域，您已與您 MongoDB 帳戶關聯，讓您同時提供之間的權衡取捨完全需要全域存取 toodata toodevelop 應用程式一致性、 可用性和效能，所有的相對應的擔保。 Cosmos DB hello 地球提供透明區域的容錯移轉多路連接的應用程式開發介面，和 hello 能力 tooelastically 標尺輸送量與儲存體。 請參閱[將資料分散到全球](distribute-data-globally.md)以深入了解。

**MongoDB 相容性**︰您可以使用現有的 MongoDB 專業知識、應用程式程式碼和工具。 您可以使用 MongoDB 開發應用程式，並將其部署 tooproduction 使用 hello 完全受管理的全域散發的 Cosmos 資料庫服務。

**沒有伺服器管理**： 您沒有 toomanage 並調整 MongoDB 資料庫。 Cosmos DB 是完全受管理的服務，這表示您沒有 toomanage 任何基礎結構或虛擬機器自己。 Cosmos DB 可在 30 個以上的 [Azure 區域](https://azure.microsoft.com/regions/services/)中使用。

**可微調的一致性層級：**從 5 中的選取正確定義的一致性與效能之間的一致性層級 tooachieve 最佳取捨。 針對查詢和讀取作業，Cosmos DB 提供五個不同的一致性層級：強式、限定過期、工作階段、一致的前置和最終。 這些細微且妥善定義的一致性層級可讓您 toomake 音效之間的利弊得失一致性、 可用性和延遲。 進一步了解[toomaximize 可用性和效能，使用一致性層級](consistency-levels.md)。

**自動索引**： 根據預設，Cosmos DB 自動 MongoDB 資料庫中的文件內的所有 hello 屬性編製都索引並不預期或要求任何結構描述或建立次要索引。

**企業級**-Azure Cosmos DB 中的本機和區域失敗 hello 朝支援多個本機複本 toodeliver 99.99%可用性與資料保護。 Azure Cosmos DB 有企業級的[合規性認證 (英文)](https://www.microsoft.com/trustcenter) 和安全性功能。 

在這段 Azure Friday 影片中，和 Scott Hanselman 與 Azure Cosmos DB 工程總經理 Kirill Gavrylyuk 一起深入了解。

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>如何啟動 tooget

請遵循 hello MongoDB 快速入門 toocreate Cosmos DB 帳戶和移轉您現有的 Mongo DB 應用程式 toouse Cosmos DB，或建立新的：

* [移轉現有的 Node.js MongoDB Web 應用程式](create-mongodb-nodejs.md)。
* [建置 MongoDB API web 應用程式的.NET 和 hello Azure 入口網站](create-mongodb-dotnet.md)
* [建置 MongoDB API 主控台應用程式使用 Java 和 hello Azure 入口網站](create-mongodb-java.md)

## <a name="next-steps"></a>後續步驟

關於 Azure Cosmos DB 的 MongoDB API 的資訊已整合至 hello 整體 Azure Cosmos DB 文件，但以下是一些您一開始的指標 tooget:

* 請遵循 hello [tooa MongoDB 帳戶連接](connect-mongodb-account.md)教學課程 toolearn 如何 tooget 您帳戶的連接字串資訊。
* 請遵循 hello[使用 MongoChef 搭配 Azure Cosmos DB](mongodb-mongochef.md)教學課程 toolearn 如何 toocreate Azure Cosmos DB 資料庫與 MongoChef MongoDB 應用程式之間的連線。
* 請遵循 hello[移轉與通訊協定 support for MongoDB。 資料 tooAzure Cosmos DB](mongodb-migrate.md)教學課程 tooimport MongoDB 資料庫中的使用您資料 tooan 應用程式開發介面。
* 連接 MongoDB 帳戶使用的 API tooan [Robomongo](mongodb-robomongo.md)。
* 了解您的作業使用以 hello 多少 RUs [GetLastRequestStatistics 命令和 hello Azure 入口網站的度量](request-units.md#GetLastRequestStatistics)。
* 了解如何太[設定讀取全域散發的應用程式喜好設定](../cosmos-db/tutorial-global-distribution-mongodb.md)。
