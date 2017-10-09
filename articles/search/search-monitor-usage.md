---
title: "aaaMonitor 使用量和 Azure 搜尋服務中的統計資料 |Microsoft 文件"
description: "追蹤 Azure 搜尋服務 (Microsoft Azure 上之託管的雲端搜尋服務) 的資源耗用量和索引大小。"
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>監視 Azure 搜尋服務

Azure 搜尋服務提供各種資源，可追蹤搜尋服務的使用情形和效能。 它可讓您存取 toometrics、 記錄、 索引統計資料，以及用於 Power BI 延伸監視功能。 本文說明如何 tooenable hello 不同的監視策略以及如何 toointerpret hello 產生的資料。

## <a name="azure-search-metrics"></a>Azure 搜尋服務計量
計量可讓您近乎即時地掌握您的搜尋服務，並可供每個服務使用，不需要額外設定。 它們可讓您追蹤的服務，以向上 too30 天 hello 效能。

Azure 搜尋服務會收集三個不同計量的資料︰

* 搜尋延遲： 時間 hello 搜尋服務所需 tooprocess 搜尋查詢，每分鐘彙總。
* 每秒搜尋查詢 (QPS)︰每秒接收的搜尋查詢數 (每分鐘彙總一次)。
* 節流的搜尋查詢百分比︰已節流處理的搜尋查詢百分比 (每分鐘彙總一次)。

![QPS 活動的螢幕擷取畫面][1]

### <a name="set-up-alerts"></a>設定警示
Hello 度量的詳細資料頁面中，您可以設定警示 tootrigger 電子郵件通知或自動化的動作當度量超出您已定義的臨界值時。

如需度量的詳細資訊，請檢查 hello Azure 監視器上的完整文件。  

## <a name="how-tootrack-resource-usage"></a>如何 tootrack 資源使用狀況
追蹤 hello 成長的索引和文件大小，可協助您主動才按下您所建立的服務的 hello 上限調整容量。 您可以在 hello 入口網站或使用 hello REST API 以程式設計方式執行這項操作。

### <a name="using-hello-portal"></a>使用 hello 入口網站

toomonitor 資源使用狀況 檢視中 hello hello 計數和統計資料為您的服務[入口網站](https://portal.azure.com)。

1. 登入 toohello[入口網站](https://portal.azure.com)。
2. 開啟您的 Azure 搜尋服務的 hello 服務儀表板。 圖格 hello 服務可以找到 hello 首頁上，或您可以瀏覽 toohello 服務從瀏覽 hello JumpBar 上。

hello 使用區段包括計量器，告訴您哪些部分可用的資源目前正在使用中。 如需每個服務的索引、文件和儲存體限制資訊，請參閱[服務限制](search-limits-quotas-capacity.md)。

  ![使用量圖格][2]

> [!NOTE]
> hello 上方螢幕擷取畫面的 hello 免費服務，其中的一個複本上限和每個，資料分割，以及主機 3 索引、 10000 的文件或 50 MB 的資料，何者較早。 在「基本」或「標準」層所建立的服務會有較大的服務限制。 如需選擇層的詳細資訊，請參閱[選擇層或 SKU](search-sku-tier.md)。
>
>

### <a name="using-hello-rest-api"></a>使用 hello REST API
Hello Azure 搜尋 REST API 和 hello.NET SDK 提供以程式設計方式存取 tooservice 度量。  如果您使用[索引子](https://msdn.microsoft.com/library/azure/dn946891.aspx)tooload 從 Azure SQL Database 或 Azure Cosmos DB 的索引，其他應用程式開發介面是您所需要的可用 tooget hello 數字。

* [取得索引統計資料](/rest/api/searchservice/get-index-statistics)
* [文件計數](/rest/api/searchservice/count-documents)
* [取得索引子狀態](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Tooexport 的記錄檔和度量

您可以匯出 hello 作業記錄的 hello 前面一節中所述的 hello 度量您服務與 hello 未經處理資料。 作業記錄檔可讓您知道如何 hello 服務正在使用，而且可以從 Power BI 取用資料時複製 tooa 儲存體帳戶。 Azure 搜尋服務會針對此用途提供監視 Power BI 內容套件。


### <a name="enabling-monitoring"></a>啟用監視
開啟您的 Azure 搜尋服務中 hello [Azure 入口網站](http://portal.azure.com)hello 啟用監視 選項底下。

選擇 hello 資料想 tooexport： 記錄檔、 度量或兩者。 您可以將它複製 tooa 儲存體帳戶、 傳送 tooan 事件中心或將它匯出 tooLog 分析。

![如何在 hello 入口網站中監視 tooenable][3]

使用 PowerShell 或 hello Azure CLI tooenable hello 參閱[這裡](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs)。

### <a name="logs-and-metrics-schemas"></a>記錄和計量的結構描述
當 hello 資料是複製的 tooa 儲存體帳戶，hello 資料會格式化為 JSON 和它的兩個容器中的位置：

* insights-logs-operationlogs：適用於搜尋流量記錄
* insights-metrics-pt1m：適用於計量

每個容器每小時會有一個 Blob。

範例路徑： `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>記錄檔結構描述
hello 記錄檔 blob 會包含您的搜尋服務流量記錄。
每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。
每個 blob 已記錄在 hello 期間發生的所有 hello 作業相同的小時。

| 名稱 | 類型 | 範例 | 注意事項 |
| --- | --- | --- | --- |
| 分析 |datetime |"2015-12-07T00:00:43.6872559Z" |Hello 作業的時間戳記 |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/> MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |您的 ResourceId |
| operationName |string |"Query.Search" |hello hello 作業名稱 |
| operationVersion |string |"2015-02-28" |hello api 版本使用 |
| category |string |"OperationLogs" |常數 |
| resultType |string |"Success" |可能的值：Success 或 Failure |
| resultSignature |int |200 |HTTP 結果碼 |
| durationMS |int |50 |以毫秒為單位的 hello 作業的持續時間 |
| 屬性 |物件 |請參閱下表中的 hello |包含作業特定資料的物件 |

**屬性結構描述**
| 名稱 | 類型 | 範例 | 注意事項 |
| --- | --- | --- | --- |
| 說明 |string |"GET /indexes('content')/docs" |hello 作業的端點 |
| 查詢 |string |"?search=AzureSearch&$count=true&api-version=2015-02-28" |hello 查詢參數 |
| 文件 |int |42 |處理的文件數目 |
| IndexName |string |"testindex" |Hello 與 hello 作業相關聯的索引名稱 |

#### <a name="metrics-schema"></a>度量結構描述
| 名稱 | 類型 | 範例 | 注意事項 |
| --- | --- | --- | --- |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/>MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |您的資源識別碼 |
| metricName |string |"Latency" |hello hello 度量名稱 |
| 分析 |datetime |"2015-12-07T00:00:43.6872559Z" |hello 作業的時間戳記 |
| average |int |64 |hello 原始範例 hello 度量的時間間隔中的 hello 平均值 |
| minimum |int |37 |hello 的 hello 度量的時間間隔中的 hello 原始樣本的最小值 |
| maximum |int |78 |hello 的 hello 度量的時間間隔中的 hello 原始樣本的最大值 |
| total |int |258 |hello 總計值的 hello hello 度量的時間間隔的未經處理的範例 |
| 計數 |int |4 |原始樣本的 hello 數目使用 toogenerate hello 度量 |
| timegrain |string |"PT1M" |hello 時間粒紋 hello ISO 8601 標準 |

每隔一分鐘就會回報所有計量。 每個度量會顯示每分鐘的最小值、最大值和平均值。

Hello SearchQueriesPerSecond 度量，最小值為 hello 註冊該分鐘內每秒的搜尋查詢的最小值。 hello 一樣 toohello 最大值。 平均，是彙總的 hello hello 整個分鐘之間。
考慮這種情況下，在一分鐘期間： 58 秒的平均負載，後面接著一個的第二個為 hello SearchQueriesPerSecond，最大值的高負載，而且最後一秒，使用只有一個查詢，是最小的 hello。

ThrottledSearchQueriesPercentage，最小值、 最大值、 平均和總計，所有擁有 hello 相同的值： hello 的搜尋查詢，從搜尋查詢，一分鐘期間的 hello 總數已節流的百分比。

## <a name="analyzing-your-data-with-power-bi"></a>使用 Power BI 來分析資料

我們建議您使用[Power BI](https://powerbi.microsoft.com) tooexplore 及視覺化您的資料。 您可以輕鬆地連接 tooyour Azure 儲存體帳戶並快速地開始分析您的資料。

Azure 搜尋提供一種[Power BI 內容套件](https://app.powerbi.com/getdata/services/azure-search)，可讓您 toomonitor 並了解您的搜尋流量與預先定義的圖表和資料表。 它包含一組 Power BI 報表自動 tooyour 資料連接，並提供您的搜尋服務相關的視覺化內容。 如需詳細資訊，請參閱 hello[內容套件說明頁面](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/)。

![Azure 搜尋服務的 Power BI 儀表板][4]

## <a name="next-steps"></a>後續步驟
檢閱[調整複本和資料分割](search-limits-quotas-capacity.md)如需如何 toobalance hello 配置的資料分割和複本的現有服務的指引。

如需服務管理的詳細資訊，請瀏覽[在 Microsoft Azure 上管理搜尋服務](search-manage.md)，或[效能和最佳化](search-performance-optimization.md)以取得微調指引。

深入了解如何建立令人讚嘆的報告。 如需詳細資訊，請參閱[開始使用 Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
