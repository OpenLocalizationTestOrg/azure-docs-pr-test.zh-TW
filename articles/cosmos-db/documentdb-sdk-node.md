---
title: "aaaAzure Cosmos DB Node.js 應用程式開發介面，SDK 與資源 |Microsoft 文件"
description: "了解 hello Node.js API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB Node.js SDK 的每個版本之間所做的變更。"
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>Azure Cosmos DB Node.js SDK︰版本資訊與資源
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [.NET 變更摘要](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [REST 資源提供者](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**下載 SDK**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**API 文件**</td><td>[Node.js API 參考文件](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**SDK 安裝指示**</td><td>[安裝指示](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**參與 tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**範例**</td><td>[Node.js 程式碼範例](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**開始使用教學課程**</td><td>[開始使用 hello Node.js SDK](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Web 應用程式教學課程**</td><td>[使用 Azure Cosmos DB 來建置 Node.js Web 應用程式](documentdb-nodejs-application.md)</td></tr>

<tr><td>**目前支援的平台**</td><td> 
[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js v4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js v0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>版本資訊

### <a name="1.12.2"/>1.12.2</a>
*   修正的 npm 文件。

### <a name="1.12.1"/>1.12.1</a>
* 已修正 executeStoredProcedure 中的錯誤，其中涉及的文件有特殊 Unicode 字元 (LS、PS)。
* 修正的 bug，在處理文件以 hello 資料分割索引鍵中的 Unicode 字元。
* 支援固定的 hello 名稱媒體建立集合。 GitHub 問題 #114。
* 已修正權限授權權杖的支援。 GitHub 問題 #178。

### <a name="1.12.0"/>1.12.0</a>
* 新增對新[一致性層級](consistency-levels.md) ConsistentPrefix 的支援。
* 新增 UriFactory 的支援。
* 已修正 Unicode 支援錯誤。 GitHub 問題 #171。

### <a name="1.11.0"/>1.11.0</a>
* 加入的 hello 支援彙總查詢 （計數、 MIN、 MAX、 SUM 和 AVG）。
* 加入的 hello 選項控制的跨資料分割的查詢平行處理原則程度。
* 停用 SSL 驗證對 Azure Cosmos DB 模擬器執行時加入的 hello 選項。
* 降低從 10,100 RU/秒 too2500 RU/秒的分割區集合最小的輸送量。
* 固定的 hello 接續 token 的 bug 單一資料分割集合。 GitHub 問題 #107。
* 在處理單一參數為 0 的固定的 hello executeStoredProcedure bug。 GitHub 問題 #155。

### <a name="1.10.2"/>1.10.2</a>
* 固定的使用者代理程式標頭 tooinclude hello SDK 版本。
* 次要程式碼清除。

### <a name="1.10.1"/>1.10.1</a>
* 使用 hello SDK tootarget hello emulator(hostname=localhost) 時，請停用 SSL 驗證。
* 在預存程序執行期間，加入支援指令碼記錄功能。

### <a name="1.10.0"/>1.10.0</a>
* 新增對跨資料分割平行查詢的支援。
* 新增對已分割集合的 TOP/ORDER BY 查詢支援。

### <a name="1.9.0"/>1.9.0</a>
* 新加入已節流處理要求的重試原則支援。 (已節流處理的要求會收到要求率太大的例外狀況，即錯誤碼 429。)根據預設，Azure Cosmos DB 重試 9 次針對每個要求時遇到錯誤碼 429，接受 hello 回應標頭中的 hello retryAfter 時間。 固定的重試間隔時間現在可以設定為 hello RetryOptions 屬性一部分 hello ConnectionPolicy 物件上如果您想要 tooignore hello retryAfter 時間伺服器傳回的 hello 重試之間。 Azure Cosmos DB 現在會等候 30 秒 （不論是重試計數） 正在進行節流，並傳回錯誤碼 429 hello 回應的每個要求的最大值。 此時也會覆寫 hello RetryOptions ConnectionPolicy 物件上的屬性中。
* Cosmos DB 現在傳回 x ms-節流閥-重試的計數和 x-ms-throttle-retry-wait-time-ms hello 回應標頭中每個要求 toodenote hello 節流重試計數和 hello 累計時間 hello 要求 hello 重試之間等候。
* 已新增 hello RetryOptions 類別，公開 hello RetryOptions 屬性可以使用的 toooverride hello ConnectionPolicy 類別上某些 hello 預設重試選項。

### <a name="1.8.0"/>1.8.0</a>
* 加入的 hello 支援多重地區資料庫帳戶。

### <a name="1.7.0"/>1.7.0</a>
* 加入的 hello 支援時間 tooLive(TTL) 功能的文件。

### <a name="1.6.0"/>1.6.0</a>
* 實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。

### <a name="1.5.6"/>1.5.6</a>
* 修正的 RangePartitionResolver.resolveForRead bug 其中它未傳回 tooa 不正確的串連結果的到期的連結。

### <a name="1.5.5"/>1.5.5</a>
* 修正 hashParitionResolver resolveForRead()：所提供的資料分割索引鍵都未擲回例外狀況時，而不會傳回所有已註冊連結的清單。

### <a name="1.5.4"/>1.5.4</a>
* 修正問題[#100](https://github.com/Azure/azure-documentdb-node/issues/100) -專用 HTTPS 代理程式： 避免修改 Azure Cosmos DB 基於 hello 通用的代理程式。 所有的 hello lib 要求使用專用的代理程式。

### <a name="1.5.3"/>1.5.3</a>
* 修正問題 [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - 正確處理媒體識別碼中的連字號。

### <a name="1.5.2"/>1.5.2</a>
* 修正問題 [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter 接聽程式洩漏警告。

### <a name="1.5.1"/>1.5.1</a>
* 修正問題[#92](https://github.com/Azure/azure-documentdb-node/issues/90) -重新命名資料夾雜湊 toohash 區分大小寫的系統。

### <a name="1.5.0"/>1.5.0</a>
* 藉由新增雜湊和範圍分割解析程式來實作分區化支援。

### <a name="1.4.0"/>1.4.0</a>
* 實作 Upsert。 documentClient 上新的 upsertXXX 方法。

### <a name="1.3.0"/>1.3.0</a>
* 略過 toobring 對齊方式，與其他 Sdk 版本號碼。

### <a name="1.2.2"/>1.2.2</a>
* 分割 Q 承諾包裝函式 toonew 儲存機制。
* 更新 toopackage npm 登錄檔案。

### <a name="1.2.1"/>1.2.1</a>
* 實作以識別碼為基礎的路由。
* 修正問題 [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - 目前屬性與 current() 方法衝突。

### <a name="1.2.0"/>1.2.0</a>
* 新增對地理空間索引的支援。
* 驗證所有資源的識別碼屬性。 資源的識別碼不能包含 ?、/、#、&#47;&#47; 等字元，或在結尾處使用空格。
* 加入新的標頭 「 索引轉換進行 」 tooResourceResponse。

### <a name="1.1.0"/>1.1.0</a>
* 實作 V2 索引原則。

### <a name="1.0.3"/>1.0.3</a>
* 問題[#40](https://github.com/Azure/azure-documentdb-node/issues/40) -實作 eslint grunt hello 核心中的組態和保證 SDK。

### <a name="1.0.2"/>1.0.2</a>
* 問題 [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promise 包裝函式不包括標頭並發生錯誤。

### <a name="1.0.1"/>1.0.1</a>
* 藉由加入 readConflicts、 readConflictAsync 和 queryConflicts 能力 tooquery 衝突。
* 已更新 API 文件。
* 問題 [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync 錯誤。

### <a name="1.0.0"/>1.0.0</a>
* GA SDK。

## <a name="release--retirement-dates"></a>發行和停用日期
Microsoft 至少提供通知**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。

新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議您，您一律升級 toohello 最新版本 SDK 盡早。

使用已停用的 SDK 的 DB tooCosmos 是任何要求被拒絕 hello 服務。

<br/>

| 版本 | 發行日期 | 停用日期 |
| --- | --- | --- |
| [1.12.2](#1.12.2) |2017 年 8 月 10 日 |--- |
| [1.12.1](#1.12.1) |2017 年 8 月 10 日 |--- |
| [1.12.0](#1.12.0) |2017 年 5 月 10 日 |--- |
| [1.11.0](#1.11.0) |2017 年 3 月 16 日 |--- |
| [1.10.2](#1.10.2) |2017 年 1 月 27 日 |--- |
| [1.10.1](#1.10.1) |2016 年 12 月 22 日 |--- |
| [1.10.0](#1.10.0) |2016 年 10 月 3 日 |--- |
| [1.9.0](#1.9.0) |2016 年 7 月 7 日 |--- |
| [1.8.0](#1.8.0) |2016 年 6 月 14 日 |--- |
| [1.7.0](#1.7.0) |2016 年 4 月 26 日 |--- |
| [1.6.0](#1.6.0) |2016 年 3 月 29 日 |--- |
| [1.5.6](#1.5.6) |2016 年 3 月 8 日 |--- |
| [1.5.5](#1.5.5) |2016 年 2 月 2 日 |--- |
| [1.5.4](#1.5.4) |2016 年 2 月 1 日 |--- |
| [1.5.2](#1.5.2) |2016 年 1 月 26 日 |--- |
| [1.5.2](#1.5.2) |2016 年 1 月 22 日 |--- |
| [1.5.1](#1.5.1) |2016 年 1 月 4 日 |--- |
| [1.5.0](#1.5.0) |2015 年 12 月 31 日 |--- |
| [1.4.0](#1.4.0) |2015 年 10 月 6 日 |--- |
| [1.3.0](#1.3.0) |2015 年 10 月 6 日 |--- |
| [1.2.2](#1.2.2) |2015 年 9 月 10 日 |--- |
| [1.2.1](#1.2.1) |2015 年 8 月 15 日 |--- |
| [1.2.0](#1.2.0) |2015 年 8 月 5 日 |--- |
| [1.1.0](#1.1.0) |2015 年 7 月 9 日 |--- |
| [1.0.3](#1.0.3) |2015 年 6 月 4 日 |--- |
| [1.0.2](#1.0.2) |2015 年 5 月 23 日 |--- |
| [1.0.1](#1.0.1) |2015 年 5 月 15 日 |--- |
| [1.0.0](#1.0.0) |2015 年 4 月 8 日 |--- |

## <a name="faq"></a>常見問題集
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>另請參閱
請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。

