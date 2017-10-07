---
title: "aaaAzure Cosmos DB.NET Core API SDK 與資源 |Microsoft 文件"
description: ".NET Core API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB.NET Core SDK 的每個版本之間所做的變更，深入了解 hello。"
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>Azure Cosmos DB .NET Core SDK︰版本資訊與資源
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

<tr><td>**SDK 下載**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**API 文件**</td><td>[.NET API 參考文件](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**範例**</td><td>[.NET 程式碼範例](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**快速入門**</td><td>[開始使用 hello Azure Cosmos DB.NET Core SDK](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Web 應用程式教學課程**</td><td>[使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-dotnet-application.md)</td></tr>

<tr><td>**目前支援的架構**</td><td>[.NET Standard 1.6 和 .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>版本資訊

hello Azure Cosmos DB.NET Core SDK 已與 hello hello 最新版本的功能同位檢查[Cosmos DB AZURE.NET SDK](documentdb-sdk-dotnet.md)。

> [!NOTE] 
> hello Azure Cosmos DB.NET Core SDK 不尚未與通用 Windows 平台 (UWP) 應用程式相容。 如果您有興趣 hello.NET Core SDK 支援 UWP 應用程式，請傳送電子郵件太[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* PartitionKeyRangeId FeedOption 的查詢結果 tooa 特定的資料分割索引鍵的範圍值的範圍設定為已加入的支援。 
* StartTime 為 ChangeFeedOption toostart hello 變更尋找該時間之後所新增的支援。 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Hello JsonSerializable 類別可能會造成堆疊溢位例外狀況中修正的問題。

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   已新增對 [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 執行個體具現化時指定自訂 JsonSerializerSettings 的支援。

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   支援的.NET 標準 1.5 做為其中一個 hello 目標架構。

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   已修正當執行 Azure Cosmos DB 查詢時，受影響的 x64 機器不支援 SSE4 指令並且擲回 SEHException 的問題。

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   已新增對新一致性層級 ConsistentPrefix 的支援。
*   已新增對個別資料分割之查詢計量的支援。
*   限制查詢的 hello 接續 token 的 hello 大小新增的支援。
*   已新增對失敗要求進行更詳細追蹤的支援。
*   Hello SDK 中進行一些效能改進。

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* 修正忽略 hello PartitionKey 值的彙總查詢 FeedOptions 中提供的問題。
* 修正在執行移動途中跨資料分割 Order By 查詢期間，進行資料分割管理的透明處理時發生的問題。

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* 修正造成死結的某些資料 hello 非同步 Api ASP.NET 內容中使用時的問題。

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* 修正 toomake SDK 更多彈性 tooautomatic 容錯移轉，在某些情況下的。

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* 偶爾會造成 WebException 可解決問題的修正： 無法解析 hello 遠端名稱。
* 加入的 hello 支援直接讀取藉由新增新的多載 tooReadDocumentAsync API 的具類型的文件。

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* 新增彙總查詢的 LINQ 支援 (COUNT、MIN、MAX、SUM 和 AVG)。
* 為記憶體流失問題的事件處理常式的 hello 使用所造成的 hello ConnectionPolicy 物件解決問題。
* 修正使用 ETag 時 UpsertAttachmentAsync 無法運作的問題。
* 修正根據字串欄位排序時交叉資料分割排序依據查詢接續無法運作的問題。

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* 新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。 請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。
* 降低從 10,100 RU/秒 too2500 RU/秒的分割區集合最小的輸送量。

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

hello Azure Cosmos DB.NET Core SDK 可讓您 toobuild 快，跨平台[ASP.NET Core](https://www.asp.net/core)和[.NET Core](https://www.microsoft.com/net/core#windows) Windows、 Mac 和 Linux 上的應用程式 toorun。 hello 最新版本的 hello Azure Cosmos DB.NET Core SDK 是完全[Xamarin](https://www.xamarin.com)相容，而且是使用的 toobuild 目標應用程式的 iOS、 Android 和單聲道 (Linux)。  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

hello Azure Cosmos DB.NET Core 預覽 SDK 可讓您 toobuild 快，跨平台[ASP.NET Core](https://www.asp.net/core)和[.NET Core](https://www.microsoft.com/net/core#windows) Windows、 Mac 和 Linux 上的應用程式 toorun。

hello Azure Cosmos DB.NET Core 預覽 SDK 已與 hello hello 最新版本的功能同位檢查[Cosmos DB AZURE.NET SDK](documentdb-sdk-dotnet.md)並支援下列 hello:
* 所有[連接模式](performance-tips.md#networking)︰閘道器模式、直接 TCP 和 Direct HTTPs。 
* 所有[一致性層級](consistency-levels.md)︰強式、工作階段、限定過期和最終。
* [資料分割的集合](partition-data.md)。 
* [多重區域資料庫帳戶和異地複寫](distribute-data-globally.md)。

如果您有問題相關的 toothis SDK，張貼太[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb)，hello 中提出問題或[github 儲存機制](https://github.com/Azure/azure-documentdb-dotnet/issues)。 

## <a name="release--retirement-dates"></a>發行和停用日期

| 版本 | 發行日期 | 停用日期 |
| --- | --- | --- |
| [1.5.0](#1.5.0) |2017 年 8 月 10 日 |--- | 
| [1.4.1](#1.4.1) |2017 年 8 月 7 日 |--- |
| [1.4.0](#1.4.0) |2017 年 8 月 2 日 |--- |
| [1.3.2](#1.3.2) |2017 年 6 月 12 日 |--- |
| [1.3.1](#1.3.1) |2017 年 5 月 23 日 |--- |
| [1.3.0](#1.3.0) |2017 年 5 月 10 日 |--- |
| [1.2.2](#1.2.2) |2017 年 4 月 19 日 |--- |
| [1.2.1](#1.2.1) |2017 年 3 月 29 日 |--- |
| [1.2.0](#1.2.0) |2017 年 3 月 25 日 |--- |
| [1.1.2](#1.1.2) |2017 年 3 月 20 日 |--- |
| [1.1.1](#1.1.1) |2017 年 3 月 14 日 |--- |
| [1.1.0](#1.1.0) |2017 年 2 月 16 日 |--- |
| [1.0.0](#1.0.0) |2016 年 12 月 21 日 |--- |
| [0.1.0-preview](#0.1.0-preview) |2016 年 11 月 15 日 |2016 年 12 月 31 日 |

## <a name="see-also"></a>另請參閱
請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。 

