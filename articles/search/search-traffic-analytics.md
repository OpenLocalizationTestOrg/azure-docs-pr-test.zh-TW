---
title: "Azure 搜尋服務流量分析 aaaSearch |Microsoft 文件"
description: "針對 Azure 搜尋中，在 Microsoft Azure，toounlock 深入了解您的使用者和您的資料上裝載的雲端搜尋服務中啟用搜尋服務流量分析。"
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a>什麼是搜尋流量分析
搜尋流量分析是一種模式，可用來實作搜尋服務的意見反應管道。 此模式描述 hello 必要的資料和 toocollect 使用 Application Insights，監視業界領導者 services 如何在多個平台。

搜尋流量分析可讓您掌握您的搜尋服務，並深入分析您的使用者及其行為。 有關於使用者的選擇的資料，是進一步改善您的搜尋經驗和 tooback hello 結果並不是所關閉的可能 toomake 決策。

Azure 搜尋會提供整合 Azure Application Insights 和 Power BI tooprovide 深入了解監視和追蹤的遙測解決方案。 因為與 Azure 搜尋之間的互動是只能透過 Api，必須實作 hello 遙測 hello 開發人員所使用的搜尋，此頁面中的 hello 指示。

## <a name="identify-hello-relevant-search-data"></a>識別 hello 相關搜尋資料

toohave 實用的搜尋度量資訊，它是必要 toolog 某些訊號 hello hello 搜尋應用程式的使用者。 這些信號表示使用者感興趣，而且這些考量相關 tootheir 需要的內容。

搜尋流量分析需要兩個訊號︰

1. 使用者產生的搜尋事件︰僅使用者所起始的搜尋查詢才有趣。 搜尋使用要求 toopopulate facet，其他內容或任何內部的資訊，並不重要，而且它們會扭曲並偏差的結果。

2. 按一下 [事件] 使用者產生： 所按下此文件中，我們 tooa 使用者選取搜尋查詢所傳回的特定搜尋結果。 點選通常表示文件為特定搜尋查詢的相關結果。

藉由連結相互關聯識別碼的搜尋，然後按一下事件，很可能 tooanalyze hello 行為，您的應用程式上的使用者。 這些搜尋 insights 是不可能 tooobtain 與搜尋流量記錄。

## <a name="how-tooimplement-search-traffic-analytics"></a>Tooimplement 如何搜尋服務流量分析

hello 訊號述 hello 上述 hello 使用者互動時，必須從 hello 搜尋應用程式收集 > 一節。 Application Insights 是可延伸的監視解決方案，適用於多個平台，並具有彈性的檢測選項。 Application Insights 的使用方式，可讓您充分利用 hello Power BI 搜尋所建立的報表資料的 Azure 搜尋 toomake hello 分析更容易。

在 hello[入口網站](https://portal.azure.com)Azure 搜尋服務，hello 搜尋流量分析分頁的頁面包含對下列這個遙測模式小祕技。 您也可以選取或建立 Application Insights 資源，並請參閱 hello 必要資料，在一個地方。

![搜尋流量分析指示][1]

### <a name="1-select-an-application-insights-resource"></a>1.選取 Application Insights 資源

您需要 tooselect Application Insights 資源 toouse，或者如果沒有已經建立一個。 您可以使用具有已在使用 toolog hello 需要自訂事件的資源。

在建立新的 Application Insights 資源時，所有應用程式類型都適用於這種情況。 選取 hello 其中一個最符合您所使用的 hello 平台。

您建立 hello 遙測用戶端應用程式需要 hello 檢測金鑰。 收到 hello Application Insights 入口網站儀表板，或您可以從取得 hello 搜尋服務流量分析 頁面上，選取您想要 toouse hello 執行個體。

### <a name="2-instrument-your-application"></a>2.檢測應用程式

在此階段，其中您檢測您自己的搜尋應用程式，使用上述步驟您在建立的 hello hello Application Insights 資源。 Toothis 程序有四個步驟：

**I.建立用戶端遙測**這是傳送事件 toohello Application Insights 資源的 hello 物件。

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

如需其他語言與平台，請參閱 hello 完成[清單](https://docs.microsoft.com/azure/application-insights/app-insights-platforms)。

**II.要求相互關聯的搜尋識別碼**toocorrelate 搜尋要求按下，它是必要的 toohave 關聯這兩個相異事件的相互關聯識別碼。 當您使用標頭進行要求時，Azure 搜尋服務會為您提供搜尋識別碼︰

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III.記錄搜尋事件**

搜尋要求發給使用者時，每次您應該記錄，做為搜尋事件具有下列結構描述上的 Application Insights 自訂事件的 hello:

**ServiceName**: （字串） 搜尋服務名稱**SearchId**: hello 搜尋查詢 (guid) 唯一識別項 （傳入 hello 搜尋回應） **IndexName**: （字串） 搜尋服務的索引查詢 toobe **QueryTerms**: hello 使用者所輸入的 （字串） 的搜尋詞彙**ResultCount**: (int) 所傳回的文件的數目 （傳入 hello 搜尋回應） **ScoringProfile**: hello 計分設定檔，如果有任何名稱 （字串）

> [!NOTE]
> 要求計數上產生的使用者查詢，藉由新增 $count = true tooyour 搜尋查詢。 請在[這裡](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)參閱詳細資訊
>

> [!NOTE]
> 請記住 tooonly 由使用者所產生的記錄搜尋查詢。
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV.記錄點選事件**

每當使用者點選文件時，必須記錄這個訊號才可進行搜尋分析。 使用下列結構描述的 hello Application Insights 自訂事件 toolog 這些事件：

**ServiceName**: （字串） 搜尋服務名稱**SearchId**: hello 相關的搜尋查詢 (guid) 唯一識別項**DocId**: （字串） 的文件識別碼**位置**: hello 搜尋中的 hello 文件的排列次序，(int) 結果頁面

> [!NOTE]
> 位置是指 toohello 基線應用程式中的順序。 您是免費 tooset 此數字，只要它一律已 hello 相同 tooallow 進行比較。
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3.使用 Power BI Desktop 進行分析

在檢測您的應用程式並驗證您的應用程式已正確連接的 tooApplication Insights 之後，您可以使用預先定義的範本建立的 Power BI desktop 的 Azure 搜尋。
此範本包含圖表和資料表可協助您讓較明智的決策 tooimprove，您的搜尋效能及相關性。

tooinstantiate hello Power BI 桌面範本，您需要三組 Application Insights 的相關資訊。 當您選取 hello 資源 toouse 時，可以在 hello 搜尋服務流量分析 頁面上，找到這項資料

![Application Insights 資料，在刀鋒視窗中搜尋服務流量分析 hello][2]

Hello Power BI 桌面範本中所包含的度量：

*   按一下 透過速率 (CTR): 使用者按一下總搜尋特定的文件 toohello 數的比率。
*   無點選搜尋︰註冊無點選的熱門查詢詞彙
*   最按一下文件： 過去 24 小時、 7 天和 30 天內最按下的文件依識別碼 hello。
*   常用的詞彙文件組： hello 按一下同一份文件，會導致的條款依點選。
*   時間 tooclick： 按一下會按照 hello 搜尋查詢之後的時間

![從 Application Insights 讀取的 Power BI 範本][3]


## <a name="next-steps"></a>後續步驟
檢測您的搜尋應用程式 tooget 功能強大且深入資料有關您的搜尋服務。

您可以在[這裡](https://go.microsoft.com/fwlink/?linkid=842905)找到 Application Insights 的詳細資訊。 請瀏覽 Application Insights[定價頁面](https://azure.microsoft.com/pricing/details/application-insights/)toolearn 深入了解其不同服務層。

深入了解如何建立令人讚嘆的報告。 如需詳細資訊，請參閱[開始使用 Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/)

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
