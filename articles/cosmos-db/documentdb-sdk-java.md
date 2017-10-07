---
title: "Azure Cosmos DB：DocumentDB Java API、SDK 和資源 | Microsoft Docs"
description: "了解 hello Java API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB DocumentDB Java SDK 的每個版本之間所做的變更。"
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a>Azure Cosmos DB：DocumentDB Java SDK 版本資訊與資源
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

<tr><td>**SDK 下載**</td><td>[Maven](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td>**API 文件**</td><td>[Java API 參考文件](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td>**參與 tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td>**快速入門**</td><td>[開始使用 hello Java SDK](documentdb-java-get-started.md)</td></tr>

<tr><td>**Web 應用程式教學課程**</td><td>[使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-java-application.md)</td></tr>

<tr><td>**目前支援的執行階段**</td><td>[JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a>版本資訊

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* 在資料分割期間處理的重大錯誤修正 toorequest 分割。
* 已修正的問題，以強式 hello 和 BoundedStaleness 一致性層級。

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* 已新增對新一致性層級 ConsistentPrefix 的支援。
* 已修正工作階段模式中讀取集合的錯誤。

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* 已啟用對低至 2,500 RU/秒且以 100 RU/秒遞增量進行調整之資料分割集合的支援。
* 這可能導致 NullRef 例外狀況，在某些查詢中的 hello 原生組件中修正的 bug。

### <a name="a-name196196"></a><a name="1.9.6"/>1.9.6
* 在 hello 查詢引擎組態閘道模式可能會造成例外狀況的查詢中修正的 bug。
* 修正 hello 可能會導致 「 找不到擁有者資源 」 的例外狀況要求在集合建立後立即的工作階段容器中的幾個 bug。

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* 新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。 請參閱[彙總支援](documentdb-sql-query.md#Aggregates)。
* 新增變更摘要的支援。
* 新增透過 RequestOptions.setPopulateQuotaInfo 收集配額資訊的支援。
* 新增透過 RequestOptions.setScriptLoggingEnabled 進行預存程序指令碼記錄的支援。
* 修正發生節流閥失敗時，DirectHttps 模式的查詢可能會停止回應的錯誤。
* 修正工作階段一致性模式中的錯誤。
* 修正當要求率過高時，可能在 HttpContext 中造成 NullReferenceException 的錯誤。
* 改善 DirectHttps 模式的效能。

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* 在 ConnectionPolicy.setProxy() API 加入簡單的用戶端執行個體 Proxy 支援。
* 加入的 DocumentClient.close() API tooproperly 關閉 DocumentClient 執行個體。
* 在直接連線模式，而不是 hello 閘道的 hello 原生組件從類別衍生 hello 查詢計劃中的改進的查詢效能。
* 設定 FAIL_ON_UNKNOWN_PROPERTIES = false，因此使用者不需要在其 POJO JsonIgnoreProperties toodefine。
* 重構記錄 toouse SLF4J。
* 修正一致性讀取器中的其他幾個 Bug。

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Hello 連接管理 tooprevent 連接中的流失直接連線模式中修正的 bug。
* 修正的 bug hello 最上層查詢中，它可能會擲回 「 NullReferenece 例外狀況。
* 藉由減少 hello hello 內部快取的網路呼叫數目的提升的效能。
* 在 DocumentClientException 中的 ActivityID 和要求 URI 中加入狀態碼以協助疑難排解。

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* 穩定性 hello 連線的管理中修正的問題。

### <a name="a-name191191"></a><a name="1.9.1"/>1.9.1
* 新增對 BoundedStaleness 一致性層級的支援。
* 新增對已分割集合之 CRUD 作業的直接連線支援。
* 修正以 SQL 查詢資料庫時發生的錯誤。
* Hello，工作階段權杖可能未正確設定的工作階段快取中修正的 bug。

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* 新增對跨資料分割平行查詢的支援。
* 新增對已分割集合的 TOP/ORDER BY 查詢支援。
* 新增對強式一致性的支援。
* 新增對使用直接連線時之名稱型要求的支援。
* 固定的 toomake ActivityId 保持一致所有要求重試次數。
* 修正的 bug 時重新建立 hello 與集合相關 toohello 工作階段快取相同的名稱。
* 新增為異地隔離空間查詢指定集合索引編製原則時的 Polygon 和 LineString 資料類型。
* 修正適用於 Java 1.8 之 Java Doc 的錯誤。

### <a name="a-name181181"></a><a name="1.8.1"/>1.8.1
* PartitionKeyDefinitionMap 中修正的 bug toocache 單一分割區集合並不進行額外提取資料分割索引鍵的要求。
* 提供不正確的資料分割索引鍵值時，請修正 bug toonot 重試。

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* 加入的 hello 支援多重地區資料庫帳戶。
* 新增的支援選項 toocustomize hello max 節流的要求上的自動重試重試次數和最大值重試等候時間。  請參閱 RetryOptions 和 ConnectionPolicy.getRetryOptions()。
* 已淘汰以 IPartitionResolver 為基礎的自訂分割程式碼。 請針對更高的儲存體和輸送量使用分割集合。

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* 新加入節流的重試原則支援。  

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* 加入時間 toolive (TTL) 支援的文件。

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* 實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* HashPartitionResolver toogenerate 雜湊值和其他 Sdk 一致由小到大 toobe 中修正的 bug。

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* 將雜湊和範圍加入資料分割的解析程式 tooassist 與跨多個資料分割的分區化應用程式。

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* 實作 Upsert。 新的 upsertXXX 方法加入 toosupport Upsert 功能。
* 實作以識別碼為基礎的路由。 不需變更公用 API，所有變更皆為內部變更。

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* 發行已略過 toobring 對齊方式，與其他 Sdk 版本號碼

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* 支援地理空間索引
* 驗證所有資源的識別碼屬性。 資源的識別碼不能包含 ?、/、#、\, 字元，或以空格作為結尾。
* 加入新的標頭 「 索引轉換進行 」 tooResourceResponse。

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* 實作 V2 索引原則

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK

## <a name="release--retirement-dates"></a>發行和停用日期
Microsoft 提供通知的最少**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。

新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議，您一律升級 toohello 最新版本 SDK 盡早。

Hello 服務，將會拒絕任何要求 tooCosmos 使用已停用的 SDK 的 DB。

> [!WARNING]
> 所有版本的 hello DocumentDB SDK for Java 先前 tooversion **1.0.0**將會遭到淘汰**2016 年 2 月 29 日**。
> 
> 

<br/>

| 版本 | 發行日期 | 停用日期 |
| --- | --- | --- |
| [1.12.0](#1.12.0) |2017 年 7 月 11 日 |--- |
| [1.11.0](#1.11.0) |2017 年 5 月 10 日 |--- |
| [1.10.0](#1.10.0) |2017 年 3 月 11 日 |--- |
| [1.9.6](#1.9.6) |2017 年 2 月 21 日 |--- |
| [1.9.5](#1.9.5) |2017 年 1 月 31 日 |--- |
| [1.9.4](#1.9.4) |2016 年 11 月24 日 |--- |
| [1.9.3](#1.9.3) |2016 年 10 月 30 日 |--- |
| [1.9.2](#1.9.2) |2016 年 10 月 28 日 |--- |
| [1.9.1](#1.9.1) |2016 年 10 月 26 日 |--- |
| [1.9.0](#1.9.0) |2016 年 10 月 3 日 |--- |
| [1.8.1](#1.8.1) |2016 年 6 月 30 日 |--- |
| [1.8.0](#1.8.0) |2016 年 6 月 14 日 |--- |
| [1.7.1](#1.7.1) |2016 年 4 月 30 日 |--- |
| [1.7.0](#1.7.0) |2016 年 4 月 27 日 |--- |
| [1.6.0](#1.6.0) |2016 年 3 月 29 日 |--- |
| [1.5.1](#1.5.1) |2015 年 12 月 31 日 |--- |
| [1.5.0](#1.5.0) |2015 年 12 月 4 日 |--- |
| [1.4.0](#1.4.0) |2015 年 10 月 5 日 |--- |
| [1.3.0](#1.3.0) |2015 年 10 月 5 日 |--- |
| [1.2.0](#1.2.0) |2015 年 8 月 5 日 |--- |
| [1.1.0](#1.1.0) |2015 年 7 月 9 日 |--- |
| [1.0.1](#1.0.1) |2015 年 5 月 12 日 |--- |
| [1.0.0](#1.0.0) |2015 年 4 月 7 日 |--- |
| 0.9.5-prelease |2015 年 3 月 9 日 |2016 年 2 月 29 日 |
| 0.9.4-prelease |2015 年 2 月 17 日 |2016 年 2 月 29 日 |
| 0.9.3-prelease |2015 年 1 月 13 日 |2016 年 2 月 29 日 |
| 0.9.2-prelease |2014 年 12 月 19 日 |2016 年 2 月 29 日 |
| 0.9.1-prelease |2014 年 12 月 19 日 |2016 年 2 月 29 日 |
| 0.9.0-prelease |2014 年 12 月 10日 |2016 年 2 月 29 日 |

## <a name="faq"></a>常見問題集
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>另請參閱
請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。

