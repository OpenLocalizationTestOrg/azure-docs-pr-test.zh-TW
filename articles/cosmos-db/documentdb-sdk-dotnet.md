---
title: "aaaAzure Cosmos DB.NET SDK 與資源 |Microsoft 文件"
description: ".NET API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB.NET SDK 的每個版本之間所做的變更，深入了解 hello。"
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>Azure Cosmos DB .NET SDK：下載和版本資訊
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

<tr><td>**SDK 下載**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**API 文件**</td><td>[.NET API 參考文件](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**範例**</td><td>[.NET 程式碼範例](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**快速入門**</td><td>[開始使用 hello Azure Cosmos DB.NET SDK](documentdb-get-started.md)</td></tr>

<tr><td>**Web 應用程式教學課程**</td><td>[使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-dotnet-application.md)</td></tr>

<tr><td>**目前支援的架構**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>版本資訊

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* PartitionKeyRangeId FeedOption 的查詢結果 tooa 特定的資料分割索引鍵的範圍值的範圍設定為已加入的支援。 
* StartTime 為 ChangeFeedOption toostart hello 變更尋找該時間之後所新增的支援。

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Hello JsonSerializable 類別可能會造成堆疊溢位例外狀況中修正的問題。

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   已修正的問題，需要重新編譯的 hello 應用程式到期的 JsonSerializerSettings toohello 簡介做 hello DocumentClient 建構函式中為選擇性參數。
* 標示的 hello DocumentClient 建構函式已經過時 hello ConnectionPolicy 和 ConsistencyLevel 參數的預設值的最後一個參數 tooallow JsonSerializerSettings 參數中傳遞時需要 JsonSerializerSettings。

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   已新增對 [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 具現化時指定自訂 JsonSerializerSettings 的支援。

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   針對不支援 SSE4 指令的 x64 電腦，已修正執行 Azure Cosmos DB API 查詢時，這類電腦會擲回 SEHException 的問題。

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   已新增對新一致性層級 ConsistentPrefix 的支援。
*   已新增對個別資料分割之查詢計量的支援。
*   限制查詢的 hello 接續 token 的 hello 大小新增的支援。
*   已新增對失敗要求進行更詳細追蹤的支援。
*   Hello SDK 中進行一些效能改進。

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* 在功能上與 1.13.3 相同。 已有一些內部變更。

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* 在功能上與 1.13.2 相同。 已有一些內部變更。

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* 修正忽略 hello PartitionKey 值的彙總查詢 FeedOptions 中提供的問題。
* 修正在執行移動途中跨資料分割 Order By 查詢期間，進行資料分割管理的透明處理時發生的問題。

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* 修正造成死結的某些資料 hello 非同步 Api ASP.NET 內容中使用時的問題。

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* 修正 toomake SDK 更多彈性 tooautomatic 容錯移轉，在某些情況下的。

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* 偶爾會造成 WebException 可解決問題的修正： 無法解析 hello 遠端名稱。
* 加入的 hello 支援直接讀取藉由新增新的多載 tooReadDocumentAsync API 的具類型的文件。

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* 新增彙總查詢的 LINQ 支援 (COUNT、MIN、MAX、SUM 和 AVG)。
* 為記憶體流失問題的事件處理常式的 hello 使用所造成的 hello ConnectionPolicy 物件解決問題。
* 修正使用 ETag 時 UpsertAttachmentAsync 無法運作的問題。
* 修正根據字串欄位排序時交叉資料分割排序依據查詢接續無法運作的問題。

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* 新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。 請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。
* 降低從 10,100 RU/秒 too2500 RU/秒的分割區集合最小的輸送量。

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* 其中某些 hello 跨資料分割查詢在 hello 32 位元主控件程序失敗的問題的修正。
* 其中 hello 工作階段的容器不更新與 hello 閘道模式中的失敗要求的語彙基元可解決問題的修正。
* 修正縱向選取中具有 UDF 呼叫的查詢在某些案例中失敗的問題。
* 用戶端端效能修正增加 hello 讀寫 hello 要求輸送量。

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* 其中 hello 工作階段的容器不更新與 hello 語彙基元可解決問題的修正失敗的要求。
* 在 32 位元主控件程序中的 hello SDK toowork 加入的支援。 請注意，若使用跨分割區查詢，建議您使用 64 位元主機處理以獲得改進的效能。
* 改進關於 IN 運算式中涉及大量分割區索引鍵值之查詢案例的效能。
* 文件集合讀取要求，當 PopulateQuotaInfo 要求選項設定，請填入 hello ResourceResponse 中的各種資源配額統計資料。

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Hello CreateDocumentCollectionIfNotExistsAsync API 1.11.0 中導入的小效能修正程式。
* 效能修正在 hello SDK 涉及高度並行要求的情形。

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* 支援新的類別和方法 tooprocess hello[變更摘要](change-feed.md)集合內的文件。
* 支援跨資料分割繼續查詢和改善跨資料分割查詢的一些效能。
* 新增 CreateDatabaseIfNotExistsAsync 和 CreateDocumentCollectionIfNotExistsAsync 方法。
* 針對下列系統函式支援 LINQ︰IsDefined、IsNull 和 IsPrimitive。
* 搭配有 project.json 工具的專案使用 hello Nuget 封裝時，請修正自動 binplacing 的 Microsoft.Azure.Documents.ServiceInterop.dll 和 DocumentDB.Spatial.Sql.dll 組件 tooapplication 的 bin 資料夾。
* 支援發出用戶端 ETW 追蹤，其可在偵錯案例中幫上忙。

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* 新增分割集合的直接連線支援。
* 經改善 hello 繫結失效的一致性層級的效能。
* 新增為異地隔離空間查詢指定集合索引編製原則時的 Polygon 和 LineString 資料類型。
* 新增轉譯述詞時對 StringEnumConverter、IsoDateTimeConverter、UnixDateTimeConverter 的 LINQ 支援。
* 多項 SDK 錯誤修正。

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* 已修正的問題，造成的 hello 遵循 NotFoundException: hello 讀取工作階段不是供 hello 輸入工作階段權杖。 查詢 hello 讀取地區之地理分散的帳戶時，在某些情況下發生此例外狀況。
* 公開 hello ResourceResponse 類別，讓直接存取 toohello 基礎資料流從回應中的 hello ResponseStream 屬性。

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* 修改過的 hello ResourceResponse、 FeedResponse、 StoredProcedureResponse 和 MediaResponse 類別 tooimplement hello 對應公用介面，以便它們可以模仿的測試為導向的部署 (TDD)。
* 修正了使用自訂 JsonSerializerSettings 物件來序列化資料時，會造成資料分割索引鍵標頭格式不正確的問題。

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* 已修正的問題造成長時間執行的查詢 toofail 發生錯誤： 授權權杖無效，無法在 hello 目前的時間。
* 固定移除問題 hello 原始 SqlParameterCollection 從跨資料分割 top/排序依據查詢。

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* 已新增分割集合的平行查詢支援。
* 已新增分割集合的跨資料分割 ORDER BY 和 TOP 查詢支援。
* 遺漏參考 tooDocumentDB.Spatial.Sql.dll 和 Microsoft.Azure.Documents.ServiceInterop.dll 參考參考 toohello Azure Cosmos DB Nuget 套件的 Azure Cosmos DB 專案時所需的固定的 hello。
* 固定的 hello 能力 toouse LINQ 中使用使用者定義函數時的不同類型的參數。 
* 修正 bug 的全球複寫帳戶其中 Upsert 呼叫已導向的 tooread 位置，而非寫入位置。
* 遺漏了加入的方法 toohello IDocumentClient 介面： 
  * UpsertAttachmentAsync 方法，會接受 mediaStream 及選項做為參數
  * CreateAttachmentAsync 方法，會接受選項做為參數
  * CreateOfferQuery 方法，會接受 querySpec 做為參數
* 非密封的 hello IDocumentClient 介面中公開的公用類別。

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* 加入的 hello 支援多重地區資料庫帳戶。
* 新增在已節流處理的要求上進行重試的支援。  使用者可以自訂 hello 重試次數和 hello 最大等待時間藉由設定 hello ConnectionPolicy.RetryOptions 屬性。
* 加入新的 IDocumentClient 介面定義所有 DocumenClient 屬性及方法的 hello 簽章。  這項變更的一部分，也變更 hello DocumentClient 類別本身建立 IQueryable 和 IOrderedQueryable toomethods 的擴充方法。
* 新增組態選項 tooset hello ServicePoint.ConnectionLimit 特定 Azure Cosmos DB 端點 Uri。  使用 ConnectionPolicy.MaxConnectionLimit toochange hello 預設值，它會設定 too50。
* 已淘汰 IPartitionResolver 及其實作。  現在不支援 IPartitionResolver。 建議您針對更高的儲存體和輸送量使用分割集合。

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* 加入多載 tooUri 型 ExecuteStoredProcedureAsync 方法採用 RequestOptions 做為參數。

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* 加入時間 toolive (TTL) 支援的文件。

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* 修正 .NET SDK 的 Nuget 封裝錯誤，可供封裝為 Azure 雲端服務解決方案的一部分。

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* 實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[固定]**查詢 Azure DB Cosmos 端點就會擲回: ' System.Net.Http.HttpRequestException： 複製內容 tooa 資料流時發生錯誤 '。

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* 擴充的 LINQ 支援包括新的分頁、條件式運算式以及範圍比較的運算子。
  * 進行 LINQ 運算子 tooenable 選取前行為
  * CompareTo 運算子 tooenable 字串範圍比較
  * 條件式 (?) 與聯合運算子 (??)
* **[已修正]** 將模型投射與 LINQ 查詢中的 Where-In 結合使用時發生 ArgumentOutOfRangeException。 [#81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[固定]**如果選取不是最後一個運算式 hello hello LINQ 提供者假設投射，而且產生 SELECT * 不正確。  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* 實作 Upsert、新增 UpsertXXXAsync 方法
* 所有要求的效能改進
* LINQ 提供者支援字串的條件式、聯合和 CompareTo 方法
* **[固定]** LINQ 提供者--> 實作是否包含在清單 toogenerate 方法 hello 上 IEnumerable 和陣列相同的 SQL
* **[固定]** BackoffRetryUtility 使用 hello 相同的 HttpRequestMessage，而不要建立新的重試
* **[已過時]** UriFactory.CreateCollection --> 現應使用 UriFactory.CreateDocumentCollection

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[已修正]** 使用非 en 文化特性資訊時 (例如 nl-NL 等) 的當地語系化問題。 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* 已新增以識別碼為基礎的路由
  * 新的 UriFactory helper tooassist 建構 ID 為基礎的資源連結
  * 在 URI 中 DocumentClient tootake 上的新多載
* LINQ 中新增用於地理空間的 IsValid() 和 isvaliddetailed ()
* 增強的 LINQ 提供者支援：
  * **算術** - Abs、Acos、Asin、Atan、Ceiling、Cos、Exp、Floor、Log、Log10、Pow、Round、Sign、Sin、Sqrt、Tan、Truncate
  * **字串** - Concat、Contains、EndsWith、IndexOf、Count、ToLower、TrimStart、Replace、Reverse、TrimEnd、StartsWith、SubString、ToUpper
  * **陣列** - Concat、Contains、Count
  * **IN** 運算子

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* 新增修改索引編製原則的支援。
  * DocumentClient 中新的 ReplaceDocumentCollectionAsync 方法
  * ResourceResponse 中新的 IndexTransformationProgress 屬性<T>可追蹤索引原則變更的百分比進度
  * DocumentCollection.IndexingPolicy 現在可變動
* 新增空間索引編製和查詢的支援。
  * 新的 Microsoft.Azure.Documents.Spatial 命名空間，可序列化/還原序列化空間類型，例如 Point 和 Polygon
  * 新的 SpatialIndex 類別，可對儲存在 Cosmos DB 中的 GeoJSON 資料編製索引
* **[已修正]**：從 LINQ 運算式產生的 SQL 查詢不正確 [#38](https://github.com/Azure/azure-documentdb-net/issues/38) \(英文\)。

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* 已新增對 Newtonsoft.Json v5.0.7 的相依性。
* Order By 做的變更 toosupport:
  
  * LINQ 提供者支援 OrderBy() 或 OrderByDescending()
  * IndexingPolicy toosupport Order By 
    
    **可能使得舊程式碼無法運作的變更** 
    
    如果您有現有的程式碼以自訂的編製索引原則，會佈建集合，您現有的程式碼需要 toobe 更新 toosupport hello 新 IndexingPolicy 類別。 如果您沒有自訂的索引原則，這個變更不會影響到您。

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* 加入的資料分割使用 hello 新 HashPartitionResolver 和 RangePartitionResolver 類別和 hello ipartitionresolver 型支援。
* 已新增 DataContract 序列化。
* 已新增 LINQ 提供者中的 GUID 支援。
* 已新增 LINQ 中的 UDF 支援。

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>發行和停用日期
Microsoft 至少提供通知**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。

新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議您，您一律升級 toohello 最新版本 SDK 盡早。 

Hello 服務將會拒絕任何要求 tooAzure Cosmos DB 使用已淘汰的 SDK。

<br/>

| 版本 | 發行日期 | 停用日期 |
| --- | --- | --- |
| [1.17.0](#1.17.0) |2017 年 8 月 10 日 |--- |
| [1.16.1](#1.16.1) |2017 年 8 月 7 日 |--- |
| [1.16.0](#1.16.0) |2017 年 8 月 2 日 |--- |
| [1.15.0](#1.15.0) |2017 年 6 月 30 日 |--- |
| [1.14.1](#1.14.1) |2017 年 5 月 23 日 |--- |
| [1.14.0](#1.14.0) |2017 年 5 月 10 日 |--- |
| [1.13.4](#1.13.4) |2017 年 5 月 09 日 |--- |
| [1.13.3](#1.13.3) |2017 年 5 月 06 日 |--- |
| [1.13.2](#1.13.2) |2017 年 4 月 19 日 |--- |
| [1.13.1](#1.13.1) |2017 年 3 月 29 日 |--- |
| [1.13.0](#1.13.0) |2017 年 3 月 24 日 |--- |
| [1.12.2](#1.12.2) |2017 年 3 月 20 日 |--- |
| [1.12.1](#1.12.1) |2017 年 3 月 14 日 |--- |
| [1.12.0](#1.12.0) |2017 年 2 月 15 日 |--- |
| [1.11.4](#1.11.4) |2017 年 2 月 6 日 |--- |
| [1.11.3](#1.11.3) |2017 年 1 月 26 日 |--- |
| [1.11.1](#1.11.1) |2016 年 12 月 21 日 |--- |
| [1.11.0](#1.11.0) |2016 年 12 月 8 日 |--- |
| [1.10.0](#1.10.0) |2016 年 9 月 27 日 |--- |
| [1.9.5](#1.9.5) |2016 年 9 月 1 日 |--- |
| [1.9.4](#1.9.4) |2016 年 8 月 24 日 |--- |
| [1.9.3](#1.9.3) |2016 年 8 月 15 日 |--- |
| [1.9.2](#1.9.2) |2016 年 7 月 23 日 |--- |
| [1.8.0](#1.8.0) |2016 年 6 月 14 日 |--- |
| [1.7.1](#1.7.1) |2016 年 5 月 6 日 |--- |
| [1.7.0](#1.7.0) |2016 年 4 月 26 日 |--- |
| [1.6.3](#1.6.3) |2016 年 4 月 8 日 |--- |
| [1.6.2](#1.6.2) |2016 年 3 月 29 日 |--- |
| [1.5.3](#1.5.3) |2016 年 2 月 19 日 |--- |
| [1.5.2](#1.5.2) |2015 年 12 月 14 日 |--- |
| [1.5.1](#1.5.1) |2015 年 11 月 23 日 |--- |
| [1.5.0](#1.5.0) |2015 年 10 月 5 日 |--- |
| [1.4.1](#1.4.1) |2015 年 8 月 25 日 |--- |
| [1.4.0](#1.4.0) |2015 年 8 月 13 日 |--- |
| [1.3.0](#1.3.0) |2015 年 8 月 5 日 |--- |
| [1.2.0](#1.2.0) |2015 年 7 月 6 日 |--- |
| [1.1.0](#1.1.0) |2015 年 4 月 30 日 |--- |
| [1.0.0](#1.0.0) |2015 年 4 月 8 日 |--- |


## <a name="faq"></a>常見問題集
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>另請參閱
請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。 

