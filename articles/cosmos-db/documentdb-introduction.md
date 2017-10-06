---
title: "Azure Cosmos DB：DocumentDB API | Microsoft Docs"
description: "了解如何使用 Azure Cosmos DB toostore 和查詢大量磁碟區的 JSON 文件，以及在使用 SQL 和 JavaScript 的低延遲。"
keywords: "JSON 資料庫，文件資料庫"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>簡介 tooAzure Cosmos DB: DocumentDB API

[Azure Cosmos DB](introduction.md) 是 Microsoft 全域發佈的多模型資料庫服務，適用於任務關鍵性應用程式。 提供 azure Cosmos DB[周全全域發佈](distribute-data-globally.md)，[彈性調整的輸送量與儲存體](partition-data.md)hello 99th 百分位數 在全球、 單一位數毫秒延遲[五個定義完善的一致性層級](consistency-levels.md)，而保證其高可用性，所有支援[領先業界的 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)。 Azure Cosmos DB[自動索引資料](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)而不需要使用結構描述與索引管理 toodeal。 它是多重模型，可支援文件、索引鍵/值、圖表和單欄式資料模型。 

![Azure DocumentDB API](./media/documentdb-introduction/cosmosdb-documentdb.png) 

以 hello DocumentDB API，Azure Cosmos DB 會提供豐富並熟悉[SQL 的查詢功能](documentdb-sql-query.md)的無結構描述的 JSON 資料的一致低延遲。 在本文中，我們提供的概觀，hello Azure Cosmos DB 的 DocumentDB API，以及如何使用它 toostore JSON 資料的大量磁碟區、 內毫秒延遲的順序來查詢它們和輕鬆發展 hello 結構描述。 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>Azure Cosmos DB 提供哪些功能和主要功能？
Azure 的 Cosmos DB，透過 hello DocumentDB API 提供下列主要功能和優點 hello:

* **可彈性擴充的輸送量與儲存體：**輕鬆地向上延展或向您的 JSON 資料庫 toomeet 調整應用程式需要。 您的資料會儲存在固態硬碟 (SSD) 中以便獲得可預測的低延遲。 Azure Cosmos DB 支援容器，將 JSON 資料儲存稱為集合，可以調整 toovirtually 無限制的儲存體大小和佈建的輸送量。 隨著應用程式的成長，您可以依據可預測的效能彈性且順暢地調整 Azure Cosmos DB。 


* **多區域複寫：** Azure Cosmos DB 以透明的方式會複製您已與您 Azure Cosmos DB 帳戶關聯，讓您 toodevelop 需要應用程式，全域存取 toodata 同時提供您資料 tooall 區域取捨一致性、 可用性和效能，所有的相對應的擔保。 Azure Cosmos DB hello 地球提供透明區域的容錯移轉多路連接的應用程式開發介面，和 hello 能力 tooelastically 標尺輸送量與儲存體。 深入了解[使用 Azure Cosmos DB 全域發佈資料](distribute-data-globally.md)。

* **運用常見的 SQL 語法進行特定查詢：**儲存異質 JSON 文件，並透過常見的 SQL 語法來查詢這些文件。 Azure Cosmos DB 利用可用的高度並行，鎖定、 記錄檔結構化索引技術 tooautomatically 索引文件的所有內容。 這可讓豐富的即時查詢，而不 hello 需要 toospecify 結構描述提示、 次要索引或檢視表。 深入了解[查詢 Azure Cosmos DB](documentdb-sql-query.md)。 
* **Hello 資料庫中的 JavaScript 執行：** Express 預存程序、 觸發程序，以及使用標準 JavaScript 的使用者定義函數 (Udf) 的應用程式邏輯。 這樣您的應用程式邏輯 toooperate 資料而不需擔心 hello hello 應用程式與 hello 資料庫結構描述不符。 hello DocumentDB API 提供完整的交易式 JavaScript 應用程式邏輯，直接在 hello 資料庫引擎執行。 JavaScript hello 深層整合啟用 hello 執行插入、 取代、 DELETE 和 SELECT 作業從 JavaScript 程式中的為隔離的交易。 在 [DocumentDB 伺服器端程式設計](programming.md)中深入了解。

* **可微調的一致性層級：**從 5 中的選取正確定義的一致性與效能之間的一致性層級 tooachieve 最佳取捨。 針對查詢和讀取作業，Azure Cosmos DB 提供五個不同的一致性層級：強式、限定過期、工作階段、一致的前置和最終。 這些細微且妥善定義的一致性層級可讓您 toomake 音效之間的利弊得失一致性、 可用性和延遲。 進一步了解[toomaximize 可用性和效能，使用一致性層級](consistency-levels.md)。

* **完全管理：**消除 hello 需要 toomanage 資料庫和機器資源。 為完全受管理的 Microsoft Azure 服務時，沒有不需要 toomanage 虛擬機器、 部署和設定軟體、 管理縮放比例，或處理複雜的資料層升級。 每個資料庫都會自動進行備份，防範區域性失敗。 您可以輕鬆地新增 Azure Cosmos DB 帳戶，並視需要可讓您在您的應用程式，而不是操作和管理您的資料庫上的 toofocus 佈建的容量。 

* **開放式設計：** 使用現有技能和工具讓您快速上手。 針對 hello DocumentDB API 是簡單、 容易實行的而且不需要您 tooadopt 新工具或遵守 toocustom 延伸 tooJSON 或 JavaScript 程式設計。 您可以存取所有 hello 資料庫功能，包括 CRUD、 查詢和處理透過簡單的 RESTful HTTP 介面的 JavaScript。 hello DocumentDB API 提供最高值項目在其上的資料庫功能時，採用現有的格式、 語言和標準。

* **自動索引：**根據預設，Azure Cosmos DB 自動 hello 資料庫中的所有 hello 文件編製都索引並不預期或要求任何結構描述或建立次要索引。 不想 tooindex 的所有項目嗎？ 別擔心，您也可以 [選擇退出 JSON 檔案中的路徑](indexing-policies.md) 。

* **變更摘要的支援：**變更摘要會提供 Azure Cosmos DB 中的集合已修改它們的 hello 順序中的文件的已排序的清單。 此摘要可以使用的順序 tooreplicate 資料中修改 toodata toolisten、 觸發程序 API 呼叫或執行更新的資料流處理。 變更摘要就會自動啟用，且容易 toouse:[深入了解變更摘要](https://docs.microsoft.com/azure/cosmos-db/change-feed)。 

## <a name="data-management"></a>您要如何管理以 hello DocumentDB API 的資料？
hello DocumentDB API 幫助您管理透過定義完善的資料庫資源的 JSON 資料。 這些資源會進行複寫來達到高可用性，並且會透過其邏輯 URI 來進行唯一定址。 hello DocumentDB API 提供簡單的 HTTP 型 RESTful 的程式設計模型的所有資源。 


hello Azure Cosmos DB 資料庫帳戶是唯一的命名空間，可讓您存取 tooAzure Cosmos DB。 您可以建立資料庫帳戶之前，您必須具有 Azure 訂用帳戶，可讓您存取 tooa 各種 Azure 服務。 

Azure Cosmos DB 內的所有資源都會加以建立模型，並儲存為 JSON 文件。 管理資源時，是以項目 (含有中繼資料的 JSON 文件) 和摘要 (即項目集合) 的形式來管理。 項目集包含在其各自的摘要內。

hello 圖顯示 hello hello Azure Cosmos DB 資源之間的關聯性：

![hello Azure Cosmos DB 中的資源之間的階層式關聯性][1] 

資料庫帳戶是由一組資料庫所組成，每個資料庫都包含多個集合，而集合可包含預存程序、觸發程序、UDF、文件和相關附件。 資料庫也有相關聯的使用者，每個都有一組權限 tooaccess 各種其他集合，預存程序、 觸發程序，Udf、 文件或附加檔案。 資料庫、使用者、權限和集合是系統所定義、具有已知結構描述的資源，而文件、預存程序、觸發程序、UDF 和附件則包含使用者定義的任意 JSON 內容。  

> [!NOTE]
> 因為 hello DocumentDB API 先前 hello Azure DocumentDB 服務為可用，您可以繼續 tooprovision，監視及管理透過 hello Azure 資源管理 REST API 建立的帳戶或使用的工具 hello Azure DocumentDB 或 Azure Cosmos DB資源名稱。 我們使用 hello 名稱交互參考 toohello Azure DocumentDB Api 時。 

## <a name="develop"></a>我要如何開發與 hello DocumentDB API 的應用程式？

Azure Cosmos DB 公開透過 hello 能夠提出 HTTP/HTTPS 要求的任何語言可以呼叫的 REST Api 資源。 此外，我們會提供數個常用的語言 hello DocumentDB API 程式庫。 hello 用戶端程式庫可簡化處理 hello 應用程式開發介面的處理詳細資料，例如位址快取、 例外狀況管理、 自動重試等等的許多層面。 程式庫目前有可供 hello 下列語言與平台：  

| 下載 | 文件 |
| --- | --- |
| [.NET SDK](http://go.microsoft.com/fwlink/?LinkID=402989) |[.NET 程式庫](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [Node.js SDK](http://go.microsoft.com/fwlink/?LinkID=402990) |[Node.js 程式庫](http://azure.github.io/azure-documentdb-node/) |
| [Java SDK](http://go.microsoft.com/fwlink/?LinkID=402380) |[Java 程式庫](/java/api/com.microsoft.azure.documentdb) |
| [JavaScript SDK](http://go.microsoft.com/fwlink/?LinkID=402991) |[JavaScript 程式庫](http://azure.github.io/azure-documentdb-js/) |
| n/a |[伺服器端 JavaScript SDK](http://azure.github.io/azure-documentdb-js-server/) |
| [Python SDK](https://pypi.python.org/pypi/pydocumentdb) |[Python 程式庫](http://azure.github.io/azure-documentdb-python/) |
| n/a | [適用於 MongoDB 的 API](mongodb-introduction.md)


使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)，您可以開發及測試您的應用程式在本機以 hello DocumentDB API，而不需要建立 Azure 訂用帳戶，或支付任何費用。 當您滿意您的應用程式在 hello 模擬器中運作時，您可以切換 toousing hello 雲端中的 Azure Cosmos DB 帳戶。

超出基本建立、 讀取、 更新和刪除作業，DocumentDB API 提供豐富的 SQL 查詢介面，用於擷取 JSON 文件和伺服器端支援，交易執行 JavaScript 應用程式邏輯的 hello。 hello 查詢和指令碼執行的介面都可透過所有平台程式庫，以及 hello REST Api。 

### <a name="sql-query"></a>SQL 查詢
hello DocumentDB API 支援查詢文件使用 SQL 語言，在 hello 根目錄為 JavaScript 型別系統，而且具有支援關聯式、 階層、 和空間查詢的運算式。 hello DocumentDB 查詢語言是簡單但功能強大介面 tooquery JSON 文件。 hello 語言支援的 ANSI SQL 文法子集，並將 JavaScript 物件、 陣列、 物件建構和函式引動過程的深度整合。 hello DocumentDB API 從 hello 開發人員提供其查詢模型，而不需要任何明確的結構描述或索引提示。

使用者定義函數 (Udf) 都可以註冊以 hello DocumentDB API 並參照一部分 SQL 查詢，因而擴充 hello 文法 toosupport 自訂應用程式邏輯。 這些 Udf 會為 JavaScript 程式撰寫，並在 hello 資料庫內執行。 

適用於.NET 開發人員，hello DocumentDB API [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx)也提供 LINQ 查詢提供者。 

### <a name="transactions-and-javascript-execution"></a>交易和 JavaScript 執行
hello DocumentDB API 可讓您 toowrite 應用程式邏輯，為具名完全以 JavaScript 撰寫的程式。 這些程式中註冊的集合，而且可以發出至指定集合中的 hello 文件上的資料庫作業。 JavaScript 可以註冊成觸發程序、預存程序或使用者定義函式 (UDF) 來供執行。 觸發程序和預存程序可以建立、 讀取、 更新和刪除文件，而沒有寫入權限 toohello 集合 hello 查詢執行邏輯的一部分執行的使用者定義函式。

Hello Cosmos DB 中的 JavaScript 執行是以關聯式資料庫系統，以做為 TRANSACT-SQL 的現代替代 JavaScript 所支援的 hello 概念模型。 所有 JavaScript 邏輯都是以隔離的快照在環境 ACID 交易內執行。 在其執行中，hello 過程期間如果 hello JavaScript 會擲回的例外狀況，然後 hello 整筆交易便會中止。

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>Azure Cosmos DB 上是否有任何線上課程？

是，Azure DocumentDB 上有 [Microsoft Virtual Academy](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847) 課程。 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>後續步驟
已經有 Azure 帳戶嗎？ 接著，您可以依照我們的[快速入門](../cosmos-db/create-documentdb-dotnet.md)開始使用 Azure Cosmos DB，這會逐步引導您建立帳戶及開始使用 Cosmos DB。

[1]: ./media/documentdb-introduction/json-database-resources1.png

