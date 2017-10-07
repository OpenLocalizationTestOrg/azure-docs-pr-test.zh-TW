---
title: "aaaAzure Cosmos DB Python 應用程式開發介面，SDK 與資源 |Microsoft 文件"
description: "了解 hello Python API 和 SDK 包括發行日期、 停用日期和 hello Azure Cosmos DB Python SDK 的每個版本之間所做的變更。"
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>Azure Cosmos DB Python SDK︰版本資訊與資源
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

<tr><td>**下載 SDK**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**API 文件**</td><td>[Python API 參考文件](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**SDK 安裝指示**</td><td>[SDK 安裝指示](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**參與 tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**快速入門**</td><td>[開始使用 Python SDK hello](documentdb-python-application.md)</td></tr>

<tr><td>**目前支援的平台**</td><td>[Python 2.7](https://www.python.org/downloads/) 和 [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>版本資訊
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* 已新增對新一致性層級 ConsistentPrefix 的支援。


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* 新增彙總查詢的支援 (COUNT、MIN、MAX、SUM 和 AVG)。
* 新增針對 Cosmos DB 模擬器執行時停用 SSL 驗證的選項。
* 移除相依要求模組 toobe 完全 2.10.0 hello 限制。
* 降低從 10,100 RU/秒 too2500 RU/秒的分割區集合最小的輸送量。
* 在預存程序執行期間，加入支援指令碼記錄功能。
* REST API 版本太當 ' 2017年-01-19' 在此版本。

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* 變更幅度 toodocumentation 註解。

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* 新增 Python 3.5 的支援。
* 新增使用要求模組的連接集區支援。
* 新增工作階段一致性的支援。
* 新增對已分割集合的 TOP/ORDERBY 查詢支援。

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* 新加入已節流處理要求的重試原則支援。 (已節流處理的要求會收到要求率太大的例外狀況，即錯誤碼 429。)根據預設，Azure Cosmos DB 重試 9 次針對每個要求時遇到錯誤碼 429，接受 hello 回應標頭中的 hello retryAfter 時間。 固定的重試間隔時間現在可以設定為 hello RetryOptions 屬性一部分 hello ConnectionPolicy 物件上如果您想要 tooignore hello retryAfter 時間伺服器傳回的 hello 重試之間。 Azure Cosmos DB 現在會等候 30 秒 （不論是重試計數） 正在進行節流，並傳回錯誤碼 429 hello 回應的每個要求的最大值。 此時也可以在 hello RetryOptions 屬性 ConnectionPolicy 物件上的已覆寫。
* Cosmos DB 現在傳回 x ms-節流閥-重試的計數和 x-ms-throttle-retry-wait-time-ms hello 回應標頭中每個要求 toodenote hello 節流重試計數和 hello cummulative 時間 hello 要求 hello 重試之間等候。
* 移除的 hello RetryPolicy 類別和 hello 對應屬性 (retry_policy) hello document_client 類別上公開，並且改為引進公開 hello RetryOptions 屬性可以使用的 toooverride ConnectionPolicy 類別上 RetryOptions 類別某些 hello 預設重試選項。

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* 加入的 hello 支援多重地區資料庫帳戶。

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* 加入的 hello 支援時間 tooLive(TTL) 功能的文件。

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Bug 修正相關 tooserver 端分割 tooallow partitionkey 路徑中的特殊字元。

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* 實作[已分割的集合](partition-data.md)和[使用者定義的效能等級](performance-levels.md)。 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* 將雜湊和範圍加入資料分割的解析程式 tooassist 與跨多個資料分割的分區化應用程式。

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* 實作 Upsert。 新的 UpsertXXX 方法加入 toosupport Upsert 功能。
* 實作以識別碼為基礎的路由。 不需變更公用 API，所有變更皆為內部變更。

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* 支援地理空間索引。
* 驗證所有資源的識別碼屬性。 資源的識別碼不能包含 ?、/、#、\, 字元，或以空格作為結尾。
* 加入新的標頭 「 索引轉換進行 」 tooResourceResponse。

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* 實作 V2 索引原則。

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* 支援 Proxy 連線。

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* GA SDK。

## <a name="release--retirement-dates"></a>發行和停用日期
Microsoft 提供通知的最少**12 個月**之前淘汰順序 toosmooth hello 轉換 tooa 較新/支援版本的 SDK。

新功能和功能與最佳化僅加入 toohello 目前 SDK，因此建議，您一律升級 toohello 最新版本 SDK 盡早。 

Hello 服務，將會拒絕任何要求 tooCosmos 使用已停用的 SDK 的 DB。

> [!WARNING]
> 所有版本的 hello Azure DocumentDB SDK for Python 先前 tooversion **1.0.0**將會遭到淘汰**2016 年 2 月 29 日**。 
> 
> 

<br/>

| 版本 | 發行日期 | 停用日期 |
| --- | --- | --- |
| [2.2.0](#2.2.0) |2017 年 5 月 10 日 |--- |
| [2.1.0](#2.1.0) |2017 年 5 月 1 日 |--- |
| [2.0.1](#2.0.1) |2016 年 10 月 30 日 |--- |
| [2.0.0](#2.0.0) |2016 年 9 月 29 日 |--- |
| [1.9.0](#1.9.0) |2016 年 7 月 7 日 |--- |
| [1.8.0](#1.8.0) |2016 年 6 月 14 日 |--- |
| [1.7.0](#1.7.0) |2016 年 4 月 26 日 |--- |
| [1.6.1](#1.6.1) |2016 年 4 月 8 日 |--- |
| [1.6.0](#1.6.0) |2016 年 3 月 29 日 |--- |
| [1.5.0](#1.5.0) |2016 年 1 月 3 日 |--- |
| [1.4.2](#1.4.2) |2015 年 10 月 6 日 |--- |
| [1.4.1](#1.4.1) |2015 年 10 月 6 日 |--- |
| [1.2.0](#1.2.0) |2015 年 8 月 6 日 |--- |
| [1.1.0](#1.1.0) |2015 年 7 月 9 日 |--- |
| [1.0.1](#1.0.1) |2015 年 5 月 25 日 |--- |
| [1.0.0](#1.0.0) |2015 年 4 月 7 日 |--- |
| 0.9.4-prelease |2015 年 1 月 14 日 |2016 年 2 月 29 日 |
| 0.9.3-prelease |2014 年 12 月 9 日 |2016 年 2 月 29 日 |
| 0.9.2-prelease |2014 年 11 月 25 日 |2016 年 2 月 29 日 |
| 0.9.1-prelease |2014 年 9 月 23 日 |2016 年 2 月 29 日 |
| 0.9.0-prelease |2014 年 8 月 21 日 |2016 年 2 月 29 日 |

## <a name="faq"></a>常見問題集
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>另請參閱
請參閱深入了解 Cosmos DB toolearn [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)服務頁面。 

