---
title: "aaaAzure Cosmos DB 常見問題集 |Microsoft 文件"
description: "取得 Azure Cosmos DB 分散、 多模型資料庫服務的相關常見問題的解答 toofrequently。 了解產能、效能層級和調整。"
keywords: "資料庫問題, 常見問題集, Database questions, frequently asked questions, documentdb, azure, Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Azure Cosmos DB 常見問題集
## <a name="azure-cosmos-db-fundamentals"></a>Azure Cosmos DB 基本概念
### <a name="what-is-azure-cosmos-db"></a>什麼是 Azure Cosmos DB？
Azure Cosmos DB 是一種可進行全域複寫的多模型資料庫服務，可在無結構描述的資料上進行豐富的查詢、協助提供可設定且可靠的效能，並支援快速開發。 它是所有可以透過完成受管理的平台受到 hello 電源且連線到 Microsoft azure。 

Azure Cosmos DB hello 解決方案 web、 行動、 遊戲，並 IoT 應用程式時可預測的輸送量，高可用性，低延遲及無結構描述的資料模型是關鍵需求。 它能提供結構描述的彈性和豐富的編製索引能力，並利用整合式 JavaScript 來包含多文件交易式支援。 

如需更多資料庫問題、 解答和指示來部署和使用這項服務，請參閱 hello [Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/cosmos-db/)。

### <a name="what-happened-toodocumentdb"></a>哪些情形的 tooDocumentDB？
hello DocumentDB API 是其中一個 Azure Cosmos DB 的 hello 支援應用程式開發介面和資料模型。 此外，Azure Cosmos DB 支援使用圖形 API (預覽)、資料表 API (預覽) 和 MongoDB API。 如需詳細資訊，請參閱 [DocumentDB 客戶的問題](#moving-to-cosmos-db)。

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>如何在 hello Azure 入口網站中取得 toomy DocumentDB 帳戶？
在 hello Azure 入口網站，hello 左窗格中的 hello Azure Cosmos DB 圖示。 如果您在之前的 DocumentDB 帳戶，現在您有 Azure Cosmos DB 帳戶，沒有變更 tooyour 計費。

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>什麼是 Azure Cosmos DB 的 hello 一般使用案例？
Azure Cosmos DB 是新的 web、 行動、 遊戲中，很好的選擇，並且 IoT 應用程式自動標尺的效能預測性，其中快速毫秒回應時間、 順序和 hello 能力 tooquery 無結構描述的資料很重要。 Azure Cosmos DB 本身 toorapid 開發及支援 hello 的應用程式資料模型的連續重複項目。 管理使用者產生之內容和資料的應用程式，就是 [Azure Cosmos DB 的常見使用案例](use-cases.md)。 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Azure Cosmos DB 如何提供可預測的效能？
A[要求單位](request-units.md)(RU) 是在 Azure Cosmos DB 輸送量 hello 量值。 1 RU 輸送量對應 toohello hello GET 1 KB 文件的輸送量。 在 Azure Cosmos DB，包括讀取、 寫入、 SQL 查詢和預存程序執行每個作業的 hello 所需的輸送量 toocomplete hello 作業根據決定性 RU 值。 您可以就單一 RU 計量來思考，而不是思考 CPU、IO 和記憶體以及它們分別如何影響您的應用程式輸送量。

您可以按照每秒輸送量 RU 的佈建輸送量保留每個 Azure Cosmos DB 容器。 對於任何規模的應用程式，您可以建立個別要求 toomeasure 基準其 RU 值，並佈建的所有要求的要求單位容器 toohandle hello 總計。 您也可以向上延展或容器的輸送量調降規模為您的應用程式 evolve hello 需求。 如需要求單位的詳細資訊以及協助判斷您的容器需求時，請參閱[估計輸送量需求](request-units.md#estimating-throughput-needs)，然後再次嘗試 hello[輸送量計算機](https://www.documentdb.com/capacityplanner)。 hello 詞彙*容器*這裡指的是 toorefers tooa DocumentDB API 集合，Graph API 圖形、 MongoDB API 集合，而且資料表 API 資料表。 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>Azure Cosmos DB 如何支援各種資料模型，例如索引鍵/值、單欄式資料、文件和圖形？

文件索引鍵/值 （資料表），單欄式，並根據模型是所有原生支援因為 hello ARS （原子、 記錄和順序） 而設計的 Azure Cosmos DB 的圖形資料。 原子、 記錄及序列可以輕易地對應和預計 toovarious 資料模型。 hello 的 Api 子集的模型會提供權限現在 （DocumentDB、 MongoDB、 資料表和圖形應用程式開發介面） 和其他特定 tooadditional 資料模型可以在 hello 未來。

Azure Cosmos DB 具有結構描述無從驗證索引引擎能夠自動它內嵌而不需要任何結構描述或 hello 位開發人員的次要索引的所有 hello 資料編製都索引。 hello 引擎依賴分離 hello hello 索引與查詢處理子系統的儲存配置的邏輯索引版面配置 （反向以及單欄式，樹狀目錄） 的一組。 Cosmos DB 也都有 hello 能力 toosupport 一組網路通訊協定和 Api 可延伸的方式並將它們轉譯有效率地 toohello 核心資料模型 （1） 和 hello 邏輯索引配置 （2） 讓您唯一可以原生支援多個資料模型.

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>Azure Cosmos DB 符合 HIPAA 規範嗎？
是，Azure Cosmos DB 符合 HIPAA 規範。 HIPAA 建立 hello 的需求使用洩漏和保護的個別辨識健全狀況資訊。 如需詳細資訊，請參閱 hello [Microsoft 信任中心](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA)。

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>什麼是 Azure Cosmos DB hello 儲存限制？
沒有任何限制 toohello 總數量容器可以儲存在 Azure Cosmos DB 的資料。

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>什麼是 Azure Cosmos DB hello 輸送量限制？
沒有任何限制 toohello 總量的容器可以支援 Azure Cosmos DB 的輸送量。 hello 重要概念是 toodistribute 您的工作負載大致平均分配在之中夠大的數字的資料分割索引鍵。

### <a name="how-much-does-azure-cosmos-db-cost"></a>Azure Cosmos DB 的費用是多少？
如需詳細資訊，請參閱 toohello [Azure 定價詳細資料的 Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/)頁面。 Azure DB Cosmos 使用費用取決於已佈建的容器，hello 時數的 hello 數目 hello 容器仍在線上，以及 hello 佈建輸送量為每一個容器。 hello 詞彙*容器*這裡指的是 toohello DocumentDB API 集合，Graph API 圖形、 MongoDB API 集合，而且資料表 API 資料表。 

### <a name="is-a-free-account-available"></a>有免費的帳戶嗎？
如果您是新 tooAzure，您可以申請[免費的 Azure 帳戶](https://azure.microsoft.com/free/)，可讓您 30 天和信用額度 tootry 所有 hello Azure 服務。 如果您有 Visual Studio 訂閱，您也適合[免費的 Azure 信用額度](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)toouse 任何 Azure 服務上的。 

您也可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)toodevelop 和測試您的應用程式在本機的釋出，而不需要建立 Azure 訂用帳戶。 當您滿意 hello Azure Cosmos DB 模擬器中您的應用程式運作時，您可以切換 toousing hello 雲端中的 Azure Cosmos DB 帳戶。

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>如何取得 Azure Cosmos DB 的其他協助？
如果您需要協助時，連接上 toous[堆疊溢位](http://stackoverflow.com/questions/tagged/azure-cosmosdb)或 hello [MSDN 論壇](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)，或透過傳送郵件太排程與 hello Azure Cosmos DB 工程小組的 1 對 1 交談[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>設定 Azure Cosmos DB
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>如何註冊 Azure Cosmos DB？
Hello Azure 入口網站中使用 azure Cosmos DB。 首先，請註冊 Azure 訂用帳戶。 您註冊之後，您可以加入 DocumentDB API，Graph API （預覽）、 表格 API （預覽） 或 MongoDB API 帳戶 tooyour Azure 訂用帳戶。

### <a name="what-is-a-master-key"></a>什麼是主要金鑰？
主要金鑰是安全性權杖的 tooaccess 帳戶的所有資源。 個人與 hello 索引鍵的 hello 資料庫有讀取和寫入存取 tooall 資源。 分配主要金鑰時，務必謹慎。 hello 主要的主要金鑰和次要的主索引鍵位於 hello**金鑰**刀鋒視窗中的 hello [Azure 入口網站][azure-portal]。 如需金鑰的詳細資訊，請參閱 [檢視、複製和重新產生存取金鑰](manage-account.md#keys)。

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>可以設定 PreferredLocations hello 區域有哪些？ 
hello PreferredLocations 值可以設定的 hello Azure tooany Cosmos DB 可用的區域。 如需可用區域的清單，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>是否有任何我時應注意的 hello world hello Azure 資料中心透過之間分散資料？ 
Azure Cosmos DB 存在於所有的 Azure 區域，為指定的 hello [Azure 區域](https://azure.microsoft.com/regions/)頁面。 因為它是 hello 核心服務，每個新的資料中心有 Azure Cosmos DB 存在。 

設定區域時，請記住 Azure Cosmos DB 涉及主權和政府雲端。 也就是如果您在主權區域中建立帳戶，便無法覆寫到該主權區域之外的位置。 同樣地，您也無法從外部帳戶覆寫到其他主權位置。 

## <a name="develop-against-hello-documentdb-api"></a>針對 hello DocumentDB API 進行開發

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>如何開始針對 hello DocumentDB API 進行開發
Microsoft DocumentDB API 位於 hello [Azure 入口網站][azure-portal]。 首先，您必須註冊 Azure 訂用帳戶。 一旦您註冊 Azure 訂用帳戶 」 時，您可以加入 DocumentDB API 容器 tooyour Azure 訂用帳戶。 如需加入 Azure Cosmos DB 帳戶的相關指示，請參閱[建立 Azure Cosmos DB 資料庫帳戶](create-documentdb-dotnet.md#create-account)。 如果您在 hello 過去在 DocumentDB 帳戶，現在您有 Azure Cosmos DB 帳戶。 

[SDK](documentdb-sdk-dotnet.md) 適用於 .NET、Python、Node.js、JavaScript 和 Java。 開發人員也可以使用 hello [RESTful HTTP Api](/rest/api/documentdb/) toointeract Azure Cosmos DB 不同平台和語言的資源。

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>可以存取某些現成的範例 tooget 開始嗎？
Hello DocumentDB API 的範例[.NET](documentdb-dotnet-samples.md)， [Java](https://github.com/Azure/azure-documentdb-java)， [Node.js](documentdb-nodejs-samples.md)，和[Python](documentdb-python-samples.md) Sdk 可在 GitHub 上。


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>Hello DocumentDB API 資料庫支援無結構描述的資料嗎？
是，hello DocumentDB API 可讓應用程式 toostore 任意 JSON 文件不含結構描述定義或提示。 立即供查詢，透過 hello Azure Cosmos DB SQL 查詢介面資料。  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>Hello DocumentDB API 支援 ACID 交易？
是，hello DocumentDB API 支援跨文件表示為 JavaScript 預存程序和觸發程序的交易。 交易範圍 tooa 每個集合內的單一資料分割和 ACID 做為 「 所有或任何內容，」 語意來執行其他同時執行的程式碼和使用者要求與隔離。 透過 hello 伺服器端執行的 JavaScript 應用程式程式碼擲回例外狀況時，會回復 hello 整個交易。 如需交易的詳細資訊，請參閱 [資料庫程式交易](programming.md#database-program-transactions)。

### <a name="what-is-a-collection"></a>什麼是集合？
集合是一組文件及其相關聯的 JavaScript 應用程式邏輯。 集合是一個可計費的實體，其中 hello[成本](performance-levels.md)取決於 hello 輸送量，而且使用的存放裝置。 集合可以跨一個或多個資料分割伺服器，而且可以延展 toohandle 幾乎沒有限制的磁碟區的儲存體或輸送量。

集合也是 Azure Cosmos DB hello 計費實體。 每個集合中每小時計費，hello 佈建輸送量為基礎而使用儲存空間。 如需詳細資訊，請參閱 [Azure Cosmos DB 價格](https://azure.microsoft.com/pricing/details/cosmos-db/)。 

### <a name="how-do-i-create-a-database"></a>我如何建立資料庫？
您可以建立資料庫使用 hello [Azure 入口網站](https://portal.azure.com)中所述，[加入集合](create-documentdb-dotnet.md#create-collection)，其中一個 hello [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)，或 hello [REST Api](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>我如何設定使用者和權限？
您可以建立使用者和權限，使用其中一種 hello [Cosmos DB API Sdk](documentdb-sdk-dotnet.md)或 hello [REST Api](/rest/api/documentdb/)。  

### <a name="does-hello-documentdb-api-support-sql"></a>Hello DocumentDB API 支援 SQL？
hello SQL 查詢語言是 hello SQL 所支援的查詢功能的加強的子集。 hello Azure Cosmos DB SQL 查詢語言提供豐富的階層式和關係運算子和透過 JavaScript 為基礎、 使用者定義函數 (Udf) 的擴充性。 JSON 的文法可讓模型當做加上標籤的節點，可供 hello Azure Cosmos DB 自動索引技術與 Azure Cosmos DB 的 hello SQL 查詢方言的樹狀結構的 JSON 文件。 使用 SQL 文法的相關資訊，請參閱 hello [QueryDocumentDB] [ query]發行項。

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>嗎? hello DocumentDB API 支援 SQL 彙總函式
hello DocumentDB API 支援透過彙總函式的任何規模的低度延遲彙總`COUNT`， `MIN`， `MAX`， `AVG`，和`SUM`透過 hello SQL 文法。 如需詳細資訊，請參閱[彙總函式](documentdb-sql-query.md#Aggregates)。

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>如何 hello DocumentDB API 會提供並行？
hello DocumentDB API 支援透過 HTTP 實體標記或 Etag 的開放式並行存取控制 (OCC)。 每個 DocumentDB API 資源的 ETag，且每次更新文件 hello ETag 設定 hello 伺服器上。 hello ETag 標頭和 hello 目前的值會包含在所有的回應訊息中。 Etag 可以搭配 hello If-match 標頭 tooallow hello 伺服器 toodecide 是否應該更新資源。 hello If-match 值為 hello ETag 值 toobe 核對。 如果 hello ETag 值符合 hello 伺服器 ETag 值，則會更新 hello 資源。 Hello 伺服器 hello ETag 不再是最新的如果拒絕 hello 作業與 「 HTTP 412 先決條件失敗 」 回應程式碼。 hello 用戶端時，然後重新擷取 hello 資源 tooacquire hello 目前的 ETag 值為 hello 資源。 此外，Etag 可以搭配 hello 如果 If-none-Match 標頭 toodetermine 是否需要重新擷取資源。

在.NET 中，使用 hello 的 toouse 開放式並行存取[AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx)類別。 如需.NET 範例，請參閱[Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs)在 GitHub 上的 hello DocumentManagement 範例。

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>如何執行 hello DocumentDB API 中的交易？
hello DocumentDB API 支援語言整合透過 JavaScript 預存程序和觸發程序的交易。 指令碼內的所有資料庫作業都會在快照隔離的情況下執行。 如果它是單一資料分割集合，是已設定領域的 toohello 集合 hello 執行。 Hello 集合分割，如果是已設定領域與 hello toodocuments hello 執行 hello 集合中相同資料分割索引鍵的值。 Hello 文件版本 (Etag) 的快照集是在 hello hello 交易開始時採取，並已認可才會成功 hello 指令碼。 如果 hello JavaScript 擲回錯誤，hello 交易會復原。 如需詳細資訊，請參閱 [Azure Cosmos DB 的伺服器端 JavaScript 程式設計](programming.md)。

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>如何將大量文件插入 Cosmos DB？
您可以利用任一種方式將文件大量插入 Azure Cosmos DB：

* hello 資料移轉工具中所述[資料庫移轉工具，Azure Cosmos DB](import-data.md)。
* 預存程序，如 [Azure Cosmos DB 的伺服器端 JavaScript 程式設計](programming.md)中所述。

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>Hello DocumentDB API 支援是快取的資源連結？
是，因為 Azure Cosmos DB 是一項 RESTful 服務，資源連結是固定不變且可快取的。 DocumentDB API 用戶端可以讀取針對任何類似資源的文件或集合的指定 「 如果 If-none-Match"標頭，然後再更新他們的本機複本之後 hello 伺服器版本已經變更。

### <a name="is-a-local-instance-of-documentdb-api-available"></a>DocumentDB API 的本機執行個體可供使用嗎？
是。 hello [Azure Cosmos DB 模擬器](local-emulator.md)提供高逼真度的模擬 hello Cosmos 資料庫服務。 它支援相同 tooAzure Cosmos DB，包括支援建立及查詢 JSON 文件中，佈建的功能和擴充集合，以及執行預存程序和觸發程序。 您可以開發和測試應用程式使用 hello Azure Cosmos DB 模擬器，及藉由變更 Azure Cosmos DB toohello 連接端點的單一組態部署 tooAzure 全域的縮放比例。

## <a name="develop-against-hello-api-for-mongodb"></a>針對 hello API 進行開發 for MongoDB。
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>何謂 hello Azure Cosmos DB API for MongoDB。
hello for MongoDB。 Azure Cosmos DB API 是相容性層級，可讓應用程式 tooeasily 並無障礙地溝通 hello 原生 Azure Cosmos DB 資料庫引擎，透過現有、 社群支援 Apache MongoDB Api 和驅動程式。 開發人員現在可以使用現有 MongoDB 工具鏈結和技術 toobuild 應用程式來充分利用 Azure Cosmos DB。 開發人員受益於 hello 的獨特功能 Azure Cosmos DB，其中包括自動編製索引、 備份維護，以備份的服務等級協定 (Sla)，以及等等。

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>如何連接 toomy API MongoDB 資料庫？
hello 最快方式 tooconnect toohello Azure Cosmos DB API MongoDB 是透過 toohello toohead [Azure 入口網站](https://portal.azure.com)。 移 tooyour 帳戶，然後在 hello 左的導覽功能表上，按一下**快速入門**。 快速入門是 hello 最佳方式 tooget 程式碼片段 tooconnect tooyour 資料庫。 

Azure Cosmos DB 會強制執行嚴格的安全性需求和標準。 Azure DB Cosmos 帳戶需要驗證，並且透過 SSL 的安全通訊，因此請確定 toouse TLSv1.2。

如需詳細資訊，請參閱[連接 MongoDB 資料庫 tooyour API](connect-mongodb-account.md)。

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>API for MongoDB 資料庫是否有其他錯誤碼？
在加法 toohello 常見 MongoDB 的錯誤碼，hello MongoDB API 會有它自己的特定錯誤碼：


| 錯誤               | 代碼  | 說明  | 方案  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | 使用的要求單位的 hello 總數已超過 hello 集合的 hello 佈建的要求單位率，並已節流處理。 | 請考慮調整 hello 輸送量 hello 集合而使之 hello Azure 入口網站，或重試一次。 |
| ExceededMemoryLimit | 16501 | 為多租用戶的服務，hello 作業已超過用戶端 hello 記憶體分配。 | 減少透過更嚴格的查詢準則的 hello 作業 hello 範圍，或連絡支援從 hello [Azure 入口網站](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。 <br><br>範例：*&nbsp;&nbsp;&nbsp;&nbsp;db.getCollection('users').aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>開發以 hello 表格 API （預覽）

### <a name="terms"></a>詞彙 
hello Azure Cosmos DB： 表格 API （預覽） 的資料表支援在建置 2017年宣佈參考 Azure Cosmos db toohello premium 供應項目。 

hello 標準資料表 SDK 是現有 Azure 儲存體資料表 hello SDK。 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>如何使用 hello 新表格 API （預覽） 供應項目？ 
hello Azure Cosmos DB 資料表 API 位於 hello [Azure 入口網站][azure-portal]。 首先，您必須註冊 Azure 訂用帳戶。 您註冊之後，您可以新增 Azure Cosmos DB 資料表 API 帳戶 tooyour Azure 的訂用帳戶，然後再加入資料表 tooyour 帳戶。 

在 hello 預覽期間，當[Sdk](../cosmos-db/table-sdk-dotnet.md)是適用於.NET，您可以開始完成 hello[表格 API](../cosmos-db/create-table-dotnet.md)快速入門文件。

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>是否需要新的 SDK toouse hello 表格 API （預覽）？ 
是，hello [Windows Azure 儲存體 Premium 資料表 （預覽） SDK](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable)可在 NuGet 上取得。 其他資訊位於 hello [Azure Cosmos DB 資料表.NET API： 下載和版本資訊](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md)頁面。 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>我要如何提供有關 hello SDK 或 bug 的意見反應？
您可以將任何 hello 下列方式提供意見反應：

* [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [MSDN 論壇](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>什麼是 hello 連接字串，我需要 toouse tooconnect toohello 表格 API （預覽）？
hello 連接字串是：
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
您可以從 hello Azure 入口網站中 hello 金鑰 頁面上，以取得 hello 連接字串。 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>如何覆寫 hello hello 新資料表 API （預覽） 中的 hello 要求選項的組態設定？
如需組態設定的相關資訊，請參閱 [Azure Cosmos DB 功能](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities)。 您可以在 hello hello 用戶端應用程式中的 appSettings 區段中加入 tooapp.config 變更 hello 設定。

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>對於使用 hello 現有標準資料表 SDK 的客戶上有任何變更嗎？
無。 沒有任何變更的現有或新客戶使用 hello 現有標準資料表 SDK。 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>如何檢視資料表的資料會儲存在 Azure Cosmos DB hello 表格 API (review) 搭配使用？ 
您可以使用 hello Azure 入口網站 toobrowse hello 資料。 您也可以使用 hello 資料表 API （預覽） 程式碼或 hello hello 下一步回應中所述的工具。 

### <a name="which-tools-work-with-hello-table-api-preview"></a>與 hello 表格 API （預覽） 搭配使用哪些工具？ 
您可以使用 Azure 總管 (0.8.9) hello 較舊版本。

工具與 hello 彈性 tootake hello 格式指定的連接字串之前可支援 hello 表格 API （預覽）。 在 hello 上提供一份資料表工具[Azure 儲存體用戶端工具](../storage/common/storage-explorers.md)頁面。 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>PowerShell 或 Azure CLI 會使用 hello 新資料表的 API （預覽）？
我們計劃適用於 PowerShell 和 Azure CLI tooadd 支援表格 API （預覽）。 

### <a name="is-hello-concurrency-on-operations-controlled"></a>是 hello 並行控制的作業？
是，透過 hello 使用 hello ETag 機制提供開放式並行存取。 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>Hello OData 查詢模型，可支援實體？ 
是，hello 表格 API （預覽） 支援 OData 查詢和 LINQ 查詢。 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>我可以連接 toohello 標準 Azure 資料表和 hello 新 premium 資料表應用程式開發介面 （預覽） 方式，並排在 hello 相同的應用程式嗎？ 
是，您可以藉由建立兩個不同的執行個體 hello CloudTableClient，每個指向連接 tooits 擁有透過 hello 連接字串的 URI。

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>我要如何移轉現有 Azure 資料表儲存體應用程式 toothis 新供應項目？
hello 新表格 API 供應項目上現有資料表儲存體的資料，請連絡 tootake 利用[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com)。 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>什麼是這項服務的 hello 藍圖，以及何時會提供其他標準資料表 API 功能？
我們計劃 tooadd 支援 SAS 權杖、 ServiceContext、 統計資料、 用戶端端加密、 分析和其他功能，當我們繼續朝向 GA 您可以在 [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api) (英文) 上提供意見反應給我們。 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>如何為 hello 儲存體大小進行這項服務，如果我開頭，例如擴充 *n*  GB 的資料和資料會隨著時間成長 too1 TB 嗎？ 
Azure 的 Cosmos DB 是設計的 tooprovide 無限制的儲存體透過 hello 使用水平延展。 hello 服務才能監視，並有效地增加存放裝置。 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>如何監視 hello 表格 API （預覽） 供應項目？
您可以使用 hello 表格 API （預覽）**度量**窗格 toomonitor 要求和儲存體使用量。 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>如何計算 hello 輸送量我所需要？
您可以使用 hello 容量估計工具 toocalculate hello hello 作業具有所需的 TableThroughput。 如需詳細資訊，請參閱[估算要求單位和資料儲存體 (英文)](https://www.documentdb.com/capacityplanner)。 一般情況下，您可以表示為 JSON 實體，並提供您的作業中的 hello 數字。 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>我可以使用 hello 表格 API 使用 hello 模擬器在本機的 SDK （預覽）？
是，您可以使用與 hello 本機模擬器，當您使用的資料表應用程式開發介面 （預覽） hello hello 新的 SDK。 toodownload 新的模擬器，請移太[使用 hello Azure Cosmos DB 模擬器進行本機開發和測試](local-emulator.md)。 hello StorageConnectionString app.config 中的值需要 toobe:

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>現有的應用程式可以處理 hello 表格 API （預覽） 嗎？ 
hello hello 介面區表格 API （預覽） 是與現有的 Azure 標準資料表跨 hello SDK 建立、 刪除、 更新和查詢作業中 hello.NET API 的 hello 相容。 請確定您具有資料列索引鍵，因為 hello 表格 API （預覽） 需要資料分割索引鍵和資料列索引鍵。 我們也計劃 tooadd 需 SDK 的支援，當我們繼續向此服務供應項目的 GA。

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>我需要 toomigrate 我現有的 Azure 資料表為基礎的應用程式 toohello 新的 SDK，如果不想 toouse hello 資料表 API （預覽） 功能？
否，您可以建立和使用現有的標準資料表資產，而不會產生任何形式的中斷。 不過，如果您未使用 hello 新資料表的 API （預覽），就無法發揮 hello 自動索引、 hello 其他一致性選項或全域發佈。 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>如何新增 hello premium 跨多個區域的 Azure 資料表 API （預覽） 中的 hello 資料的複寫？
您可以使用 hello Azure Cosmos DB 入口網站的[全域的複寫設定](tutorial-global-distribution-documentdb.md#portal)tooadd 適用於您的應用程式的區域。 toodevelop 全域散發的應用程式，您也應該加入 hello PreferredLocation 資訊組 toohello 區域提供讀取的低延遲的應用程式。 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>如何變更 hello hello premium 表格 API （預覽） 中的 hello 帳戶的主要寫入區域？
您可以使用 hello Azure Cosmos DB 全域複寫入口網站窗格 tooadd 區域，並接著容錯移轉 toohello 需要區域。 如需指示，請參閱[使用多區域 Azure Cosmos DB 帳戶進行開發](regional-failover.md)。 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>當我散發資料時，如何設定慣用的讀取區域以取得低延遲？ 
從本機位置 hello、 讀取 toohelp hello app.config 檔案中使用 hello PreferredLocation 金鑰。 對於現有的應用程式，hello 表格 API （預覽） 擲回錯誤，如果 LocationMode 設定。 因為 hello premium 表格 API （預覽） 挑選 hello app.config 檔案的這項資訊，請移除該程式碼。 如需詳細資訊，請參閱 [Azure Cosmos DB 功能](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities)。

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>如何應考慮 hello 表格 API （預覽） 中的一致性層級？ 
Azure Cosmos DB 可在一致性、高可用性及延遲之間提供完全合乎邏輯的取捨。 Azure Cosmos 資料庫提供五個一致性層級 tooTable API （預覽） 開發人員，讓您可以選擇在 hello 資料表層級的 hello 右一致性模型，並讓個別要求 hello 資料時。 當用戶端連線時，它可以指定一致性層級。 您可以變更透過 hello hello TableConsistencyLevel 機碼值的 hello app.config 設定 hello 層級。 

hello 表格 API （預覽） 提供低延遲讀取與 「 讀取您自己寫入 」 與 hello 預設工作階段一致性。 如需詳細資訊，請參閱[一致性層級](consistency-levels.md)。 

根據預設，Azure 資料表儲存體提供區域內的強式一致性和 Eventual hello 次要位置中的一致性。 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>Azure Cosmos DB 提供的一致性層級是否比標準資料表多？
是，如需如何從 hello toobenefit 分散 Azure Cosmos DB 性質，請參閱[一致性層級](consistency-levels.md)。 因為 hello 一致性層級提供保證，您可以放心地使用。 如需詳細資訊，請參閱 [Azure Cosmos DB 功能](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities)。

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>啟用全域發佈時，時間長度需要 tooreplicate hello 資料？
我們認可 hello 永久 hello 本機區域資料，並推送 hello 資料 tooother 區域，立即會在幾毫秒為單位。 此複寫為僅相依於 hello 來回時間 (RTT)，hello 資料中心。 toolearn 深入了解 hello 全域發佈功能的 Azure Cosmos DB，請參閱[Azure Cosmos DB： 在 Azure 上的全域分散式的資料庫服務](distribute-data-globally.md)。

### <a name="can-hello-read-request-consistency-level-be-changed"></a>可以變更 hello 讀取的要求一致性層級嗎？
以 Azure Cosmos DB，您可以在 hello 容器層級設定 hello 一致性層級 （在 hello 資料表）。 藉由使用 hello SDK，您可以藉由提供 hello 值 TableConsistencyLevel hello app.config 檔案中的索引鍵變更 hello 層級。 hello 可能的值為： 強式、 繫結失效，工作階段、 一致的首碼，然後 Eventual。 如需詳細資訊，請參閱 [Azure Cosmos DB 中的 Tunable 資料一致性層級](consistency-levels.md)。 hello 重要概念是，您無法將 hello 要求一致性層級超過 hello 資料表 hello 設定。 例如，您無法在強式設定 hello Eventual hello 資料表的一致性層級和 hello 要求一致性層級。 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>如何 hello 進階表格 API （預覽） 帳戶處理容錯移轉如果區域關閉？ 
hello premium 表格 API （預覽） 借用的 Azure Cosmos DB hello 全域散發的平台。 tooensure 應用程式可以容忍資料中心停機時間，啟用 hello Azure Cosmos DB 入口網站中的 hello 帳戶至少一個多個區域[開發以多區域 Azure Cosmos DB 帳戶](regional-failover.md)。 您也可以使用 hello 入口網站來設定 「 hello 區域的 hello 優先順序[開發以多區域 Azure Cosmos DB 帳戶](regional-failover.md)。 

您可以加入多區域 hello 帳戶並控制它可能無法透過 tooby 提供容錯移轉優先權。 當然，toouse hello 資料庫，您需要 tooprovide 那里應用程式。 如果您這樣做，您的客戶就不會經歷停機時間。 hello client SDK 會自動隸屬。 也就是說，它可以偵測已關閉，而且自動容錯移轉 toohello 新區域的 hello 區域。

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>已啟用備份的 hello premium 表格 API （預覽）
是，hello premium 表格 API （預覽） 借用 hello 平台的 Azure Cosmos DB 備份。 備份會自動執行。 如需詳細資訊，請參閱[使用 Azure Cosmos DB 進行線上備份及還原](online-backup-and-restore.md)。

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Hello 表格 API （預覽） 沒有預設索引的實體的所有屬性嗎？
是，根據預設，它會為實體的所有屬性編製索引。 如需詳細資訊，請參閱 [Azure Cosmos DB：索引編製原則](indexing-policies.md)。 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>這代表沒有 toocreate 多個索引 toosatisfy hello 查詢嗎？ 
是，Azure Cosmos DB 會為所有屬性提供自動編製索引，而不需任何結構描述定義。 這項自動化會釋出開發人員 toofocus hello 應用程式而不是在索引建立及管理。 如需詳細資訊，請參閱 [Azure Cosmos DB：索引編製原則](indexing-policies.md)。

### <a name="can-i-change-hello-indexing-policy"></a>可以變更 hello 編製索引原則嗎？
是，您可以藉由提供 hello 索引定義變更 hello 編製索引原則。 如需詳細資訊，請參閱 [Azure Cosmos DB 功能](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities)。 您需要 tooproperly 編碼和逸出 hello 設定。 

在字串 hello app.config 檔中的 json 格式：
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>做為平台的 azure Cosmos DB 似乎 toohave 許多功能，例如排序、 彙總、 階層和其他功能。 您將會加入這些功能 toohello 資料表應用程式開發介面嗎？ 
在預覽中，hello 表格 API 提供 hello 相同查詢 Azure 資料表儲存體的功能。 Azure Cosmos DB 也支援排序、彙總、地理空間查詢、階層及各種不同的內建函式。 我們將提供在未來的服務更新中的 hello 資料表 API 中的其他功能。 如需詳細資訊，請參閱[適用於 Azure Cosmos DB DocumentDB API 的 SQL 查詢](../documentdb/documentdb-sql-query.md)。
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>我何時應該變更 TableThroughput hello 表格 API （預覽）？
任一 hello 下列條件時，您應該變更 TableThroughput:
* 您要執行的擷取、 轉換及載入 (ETL) 的資料，或者您想 tooupload 大量資料在短時間內。 
* 您需要更多的輸送量，從在 hello 後端 hello 容器。 比方說，您會看到使用 hello 輸送量大於 hello 佈建的輸送量，，您會節流。 如需詳細資訊，請參閱[設定 Azure Cosmos DB 容器輸送量](set-throughput.md)。

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>我可以向上延展或縮小 hello 輸送量我表格 API （預覽） 的資料表嗎？ 
是，您可以使用 hello Azure Cosmos DB 入口網站的標尺窗格 tooscale hello 輸送量。 如需詳細資訊，請參閱[設定輸送量](set-throughput.md)。

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>新佈建的資料表是否有預設的 TableThroughput 設定？
是，如果您不會覆寫透過 app.config hello TableThroughput，請勿使用預先建立的容器中 Azure Cosmos DB hello 服務會建立資料表輸送量為 400。
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>有任何變更的現有客戶的 hello 標準資料表 API 定價嗎？
無。 對於現有的標準資料表 API 客戶，沒有任何價格上的變更。 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Hello 價格如何計算 hello 表格 API （預覽）？ 
hello 價格取決於配置 TableThroughput hello。 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>如何處理供應項目資料表 API （預覽） 中的 hello 資料表上發生的任何節流？ 
如果 hello 要求速率超過 hello 佈建輸送量為 hello 基礎容器 hello 容量，您會收到錯誤，並重試 hello SDK 將 hello 呼叫藉由套用 hello 重試原則。

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>為什麼需要 toochoose 除了 hello premium 表格 API （預覽） 提供的 Azure Cosmos DB PartitionKey 和 RowKey tootake 利用輸送量？
Azure Cosmos DB 容器設定預設輸送量，如果您未提供一個 hello app.config 檔案中。 

Azure Cosmos DB 能提供效能和延遲上的保證，限定作業時的上限。 Hello 引擎可以強制執行控管 hello 租用戶的作業時，可能此保證。 設定 TableThroughput，可確保您收到 hello 保證輸送量和延遲，因為 hello 平台保留這個容量，而且不保證作業成功。 

藉由使用 hello 輸送量規格，您可以彈性地變更它 toobenefit 從您的應用程式的 hello 季節性、 符合 hello 輸送量需求，並節省成本。

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>Azure 儲存體 SDK 已對我而言，非常便宜，我支付只有 toostore hello 資料，因此很少查詢。 hello 新 Azure Cosmos DB 供應項目看起來 toobe 充電我即使我沒有執行單一交易或儲存的任何項目。 可以請您說明嗎？

Azure 的 Cosmos DB 是設計的 toobe 一種全域散發的 SLA 為基礎的系統，與保證可用性、 延遲和輸送量。 當您保留 Azure Cosmos DB 中的輸送量時，這樣會保證，不同於其他系統的 hello 輸送量。 Azure Cosmos DB 會提供客戶要求的其他功能，如次要索引和全域散發。 Hello 預覽期間，我們提供輸送量最佳化的模型，以及最後，我們計劃 tooprovide 儲存體最佳化模型 toomeet 我們的客戶需求。 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>將資料嵌入資料表儲存體時，我從未收過「配額已滿」通知 (包括資料分割已滿)。 以 hello 表格 API （預覽），不要收到這則訊息。 這項服務的限制我和我強制 toochange 我現有的應用程式嗎？

Azure Cosmos DB 是 SLA 型系統，它提供無限制的調整和延遲、輸送量、可用性、一致性保證。 tooensure 保證高階效能，請確定您的資料大小和索引是容易管理及擴充。 hello 數量的實體或每個資料分割索引鍵的項目上的 hello 10 GB 限制為 tooensure 我們提供絕佳的查閱和查詢效能。 您的應用程式可甚至也針對 Azure 儲存體進行調整的 tooensure，我們建議您*不*建立熱的分割區儲存一個資料分割中的所有資訊和查詢它。 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>因此 PartitionKey 和 RowKey 仍然需要與 hello 表格 API （預覽）？ 
是。 由於 hello 表面區域的 hello 表格 API （預覽） 是類似的 hello 資料表儲存體 SDK toothat，hello 資料分割索引鍵提供有效率的方式 toodistribute hello 資料。 hello 資料列索引鍵是磁碟分割內唯一的。 hello 資料列索引鍵需求 toobe 存在，而且不可為 null 做為在 hello standard SDK。 RowKey hello 長度為 255 個位元組，且 PartitionKey hello 長度 100 個位元組 （推出 toobe 增加 too1 kb 為單位）。 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Hello hello 表格 API （預覽） 的錯誤訊息有哪些？
這個預覽是與 hello 標準資料表相容，因為大部分的 hello 錯誤會對應 toohello hello 標準資料表中的錯誤。 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>為什麼沒有取得受到節流當我嘗試 toocreate 許多中資料表的一個接著一個 hello 表格 API （預覽）？
Azure Cosmos DB 是 SLA 型系統，可提供延遲、輸送量、可用性及一致性的保證。 因為它已佈建的系統，它會保留資源 tooguarantee 這些需求。 偵測並節流 hello 快速率建立的資料表。 我們建議您查看 hello 率建立的資料表，並降低 tooless 比每分鐘的 5。 請記住該 hello 表格 API （預覽） 是佈建的系統。 hello 目前佈建時，您將開始 toopay 它。 

## <a name="develop-against-hello-graph-api-preview"></a>開發 hello Graph API （預覽）
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>如何套用 Graph API （預覽） tooAzure Cosmos DB hello 的功能？
您可以使用 Graph API （預覽） 延伸模組程式庫 tooapply hello 功能。 這個程式庫稱為 Microsoft Azure 圖形，您可以在 NuGet 上取得。 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>看來您支援 hello Gremlin 圖形周遊語言。 您是否計劃 tooadd 更多的形式的查詢？
是，我們計劃 tooadd hello 未來中查詢的其他機制。 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>如何使用 hello 新 Graph API （預覽） 供應項目？ 
tooget 已啟動，完成 hello [Graph API](../cosmos-db/create-graph-dotnet.md)快速入門文件。

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>DocumentDB 客戶的問題
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>為什麼要移動 tooAzure Cosmos DB？ 

Azure Cosmos DB 是 hello 下一個大的展現分散，在標尺雲端資料庫中。 DocumentDB 客戶，您現在可以存取 toohello 突破性系統和 Azure Cosmos DB 所提供的功能。

Azure Cosmos DB 入門 」 專案佛羅倫斯"2010 tooaddress hello 痛苦點中面臨的開發人員建置 Microsoft 內部的大型應用程式。 hello 挑戰建置全域散發的應用程式並不是唯一 tooMicrosoft，因此我們 hello 第一代的這項技術用於 2015 tooAzure 開發人員在進行 Azure DocumentDB hello 形式。 

從那時候起，我們便已新增一些功能並引進重要的全新功能。 Azure 的 Cosmos DB 是 hello 結果。 在這個版本中，DocumentDB 客戶 (與其資料) 會自動無縫轉換為 Azure Cosmos DB 客戶。 這些功能是在 hello 部分 hello 核心 database engine，以及全域發佈、 彈性的延展性和領先業界、 完整的 Sla。 具體來說，我們已逐漸發展 hello Azure Cosmos DB 資料庫引擎 tooefficiently 對應所有常用的資料模型、 型別系統和應用程式開發介面 toohello 基礎資料模型的 Azure Cosmos DB。 

hello 目前這項工作的開發人員面對現象是 hello 新支援[Gremlin](../cosmos-db/graph-introduction.md)和[資料表儲存體 Api](../cosmos-db/table-introduction.md)。 也是只 hello 開頭。 我們計劃 tooadd 其他常用的應用程式開發介面和較新的資料模型經過一段時間，與效能和全域大規模的儲存體中的更多進階功能。 

它是重要出該 hello DocumentDB toopoint [SQL 用語](../documentdb/documentdb-sql-query.md)一直其中一個 hello 許多應用程式開發介面支援基礎 Azure Cosmos DB 該 hello。 使用完全受管理的服務，例如 Azure Cosmos DB 的開發人員，hello 介面 toohello 服務為 hello hello 服務所公開的 Api。 現有的 DocumentDB 客戶絲毫沒有改變。 在 Azure Cosmos DB 中，您會取得完全相同的 SQL，DocumentDB API 提供的 hello。 現在 （和中 hello 未來），您可以存取先前無法存取的其他功能 

接續工作的另一個現象是 hello 擴充基礎全域和彈性的輸送量與儲存體的延展性。 我們強化了數個基本 toohello 全域通訊子系統。 其中一個 hello 許多這類的開發人員對向功能是 hello 一致的前置詞一致性模型，讓總計的五個妥善定義的一致性模型。 我們將會在時機成熟時發行許多更有趣的功能。 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>怎麼我需要 toodo tooensure DocumentDB 資源，繼續在 Azure Cosmos DB 上 toorun？

您需要 toomake 沒有變更完全。 DocumentDB 資源現在 Azure Cosmos DB 資源，而且在此動作發生時，有的 hello 服務不中斷。

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>變更的作用為何需要與 Azure Cosmos DB 我的應用程式 toowork toomake 嗎？

沒有任何變更 toomake。 類別、命名空間和 NuGet 套件名稱均未變更。 一如往常，我們建議您保留您的 Sdk 向上 toodate tootake 利用 hello 最新功能和增強功能。 

### <a name="whats-changed-in-hello-azure-portal"></a>Hello Azure 入口網站中變更什麼？

DocumentDB 不會顯示 hello 入口網站中為一項 Azure 服務。 在其位置是新的 Azure Cosmos DB 圖示，hello 下列影像所示。 您可繼續使用所有的集合，就跟之前沒兩樣，且依然可調整輸送量、變更一致性及監視 SLA。 hello 資料總管 （預覽） 功能已增強。 您可以立即檢視和編輯文件、 建立和執行查詢，並使用預存程序、 觸發程序和 UDF 一個頁面上，從 hello 下列影像所示： 

![hello Azure Cosmos DB 集合刀鋒視窗](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>是否有變更 toopricing？

否，hello Azure Cosmos DB 的應用程式的執行成本會 hello 相同，如前。

### <a name="are-there-changes-toohello-slas"></a>是否有變更 toohello Sla？

否，hello 可用性 Sla、 一致性、 延遲及輸送量不會變更，而且仍會顯示 hello 入口網站中。 如需詳細資訊，請參閱 [Azure Cosmos DB 的 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/)。
   
![具有範例資料的待辦事項應用程式](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
