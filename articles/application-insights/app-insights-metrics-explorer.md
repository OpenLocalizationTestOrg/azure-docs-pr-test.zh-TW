---
title: "aaaExploring 中 Azure Application Insights 計量 |Microsoft 文件"
description: "Toointerpret 圖上度量總管 中，以及如何 toocustomize 度量總管刀鋒視窗。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>在 Application Insights 中探索度量
[Application Insights][start] 中的度量為從您的應用程式傳送的遙測中的測量值和事件計數。 它們幫助您偵測效能問題，並觀察使用應用程式方式的趨勢。 標準度量的範圍很廣泛，而您也可以建立自己的自訂度量和事件。

度量和事件計數會顯示在彙總值 (例如總和、平均或計數) 的圖表中。

以下是一組範例圖表︰

![](./media/app-insights-metrics-explorer/01-overview.png)

Hello Application Insights 入口網站中找到 everywhere 度量圖表。 在大部分情況下，可以自訂它們，，您可以加入多個圖表 toohello 刀鋒視窗。 從 hello 概觀刀鋒視窗中，按一下 透過 toomore 詳細的圖表 （其中的標題，例如 「 伺服器 」），或按一下**計量瀏覽器**tooopen 您可以在其中建立自訂圖表的新刀鋒視窗。

## <a name="time-range"></a>時間範圍
您可以變更 hello hello 圖表或任何刀鋒視窗上的資料格中所涵蓋的時間範圍。

![開啟 hello 概觀刀鋒視窗中的 hello Azure 入口網站中的應用程式](./media/app-insights-metrics-explorer/03-range.png)

如果您預期的部分資料尚未出現，請按一下 [重新整理]。 圖表重新整理它們自己的間隔，但 hello 間隔更大的時間範圍較長時間。 它可以拖曳至圖表，需要一些時間，資料 toocome hello 分析管線。

toozoom 入部分圖表中，拖曳它：

![拖曳過圖表的一部分。](./media/app-insights-metrics-explorer/12-drag.png)

按一下 hello 復原縮放按鈕 toorestore 它。

## <a name="granularity-and-point-values"></a>資料粒度和點值
此時將滑鼠游標移 hello 圖表 toodisplay hello hello 度量值。

![Hello 滑鼠停留在圖表](./media/app-insights-metrics-explorer/02-focus.png)

在特定時間點的 hello 標準 hello 值是進行彙總 hello 前面取樣間隔。

hello 取樣間隔時間內或 「 資料粒度 」 會顯示在 hello hello 刀鋒視窗最上方。

![刀鋒視窗中的 hello 標頭。](./media/app-insights-metrics-explorer/11-grain.png)

您可以調整 hello 時間範圍 刀鋒視窗中的資料粒度 hello:

![刀鋒視窗中的 hello 標頭。](./media/app-insights-metrics-explorer/grain.png)

hello 資料粒度可用取決於您所選取的 hello 時間範圍。 hello 明確的資料粒度是替代項目 toohello 「 自動 」 資料粒度的 hello 時間範圍。


## <a name="editing-charts-and-grids"></a>編輯圖表和格線
tooadd 新的圖表 toohello 刀鋒視窗：

![在 [計量瀏覽器] 中，選擇 [加入圖表]](./media/app-insights-metrics-explorer/04-add.png)

選取**編輯**上現有或新的圖表 tooedit 什麼它會顯示：

![選取一或多個度量](./media/app-insights-metrics-explorer/08-select.png)

雖然可以一起顯示的 hello 組合的限制，您可以在圖表上，顯示多個度量。 當您選擇一個計量，某些 hello 其他人已停用。

如果您已編碼[自訂度量][ track]到應用程式 （呼叫 tooTrackMetric 和 TrackEvent） 就會列在此處。

## <a name="segment-your-data"></a>分段資料
您可以分割度量屬性-例如，toocompare 頁面檢視因不同作業系統的用戶端上。

選取圖表或格線、 切換群組，並挑選由屬性 toogroup:

![選取 [分組開啟]，然後在 [群組依據] 中選取屬性](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> 當您使用群組時，則 hello 區域和橫條圖類型會提供堆疊的顯示。 這是適合其中 hello 彙總方法為 Sum。 但是 hello 彙總類型的平均，選擇 hello 線條或格線顯示的型別。
>
>

如果您已編碼[自訂度量][ track]到應用程式和包含屬性值，您將無法 tooselect hello 清單中的 hello 屬性。

是 hello 圖太小，分割的資料嗎？ 調整其高度：

![調整 hello 滑桿](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>彙總類型
在預設的 hello 端 hello 圖例通常會顯示彙總的 hello 值段 hello hello 圖表。 如果您將滑鼠停留在 hello 圖表，則會在該點顯示 hello 值。

Hello 圖表上的每個資料點是收到 hello 上述取樣間隔或 「 資料粒度 」 中的 hello 資料值的彙總。 hello 資料粒度會顯示在頂端 hello hello 刀鋒視窗中，而且隨著 hello hello 圖表的整體的時幅。

度量可以用不同方式彙總：

* **計數**是收到 hello 取樣間隔中的 hello 事件的計數。 它用於事件，例如要求。 Hello 高度 hello 圖的變化表示 hello 速率 hello 事件就會發生變化。 但請注意，hello 數字的值變更時變更 hello 取樣間隔。
* **Sum**加總 hello 收到 hello 取樣間隔內或 hello 段 hello 圖表上的所有 hello 資料點的值。
* **平均**除以 hello 的 hello 收到 hello 間隔內的資料點的數目總和。
* **唯一** ：計數會用於使用者及帳戶的計數。 Hello 取樣間隔期間或在 hello 段 hello 圖表，hello 圖會顯示不同的使用者出現在該時間的 hello 計數。
* **%** - 每個彙總百分比版本只會搭配分段圖表使用。 too100%加總 hello 和 hello 圖表可顯示總計的不同元件的 hello 相對比重。

    ![百分比彙總](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>變更 hello 彙總類型

![編輯 hello 圖表，然後選取 彙總](./media/app-insights-metrics-explorer/05-aggregation.png)

當您建立新的圖表，或當所有的度量資訊會被取消選取時，會顯示 hello 預設方法，針對每個標準：

![取消選取所有度量 toosee hello 預設值](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>釘選 Y 軸 
根據預設圖表可顯示 Y 軸值從零到 hello 資料範圍，toogive hello 值的配量的視覺表示法中的最大值為止。 但在某些情況下以上 hello 配量可能很有趣 toovisually 檢查值的些微變更。 針對自訂類似此使用 hello y 軸範圍編輯功能 toopin hello y 軸最小值或最大值所需的位置。
按一下 [進階設定] 核取方塊 toobring 向上 hello y 軸範圍設定

![按一下 [進階設定]、選取 [自訂範圍]，然後指定最小值與最大值](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>篩選資料
將選取的屬性值的 toosee 只 hello 度量：

![按一下 [篩選器]，然後檢查一些值](./media/app-insights-metrics-explorer/19-filter.png)

如果您沒有選取任何特定屬性的值，它具有 hello 相同選取全部： 內容上沒有任何篩選條件。

請注意 hello 計算的事件，連同每個屬性值。 當您選取一個屬性的值時，hello 計算以及其他屬性的值會進行調整。

篩選會在刀鋒視窗上套用 tooall hello 圖表。 如果您想要不同的篩選器套用 toodifferent 圖表，建立並儲存不同的度量資訊的刀鋒視窗。 如果您想要可以使您可以看到它們彼此釘選不同刀鋒 toohello 儀表板的圖表。

### <a name="remove-bot-and-web-test-traffic"></a>移除 Bot 和 Web 測試流量
使用 hello 篩選**即時或綜合流量**並檢查**真實**。

您也可以依 **綜合流量的來源**篩選。

### <a name="tooadd-properties-toohello-filter-list"></a>tooadd 屬性 toohello 篩選器清單
您希望您自己選擇的類別 toofilter 遙測？ 例如，您可能將使用者劃分成不同的類別，且您想要依照這些類別來分割資料。

[建立您自己的屬性](app-insights-api-custom-events-metrics.md#properties)。 設定[遙測初始設定式](app-insights-api-custom-events-metrics.md#defaults)toohave 它出現在所有遙測-包括 hello 標準遙測傳送的不同 SDK 模組。

## <a name="edit-hello-chart-type"></a>編輯 hello 圖表類型
請注意您可以在格線與圖形之間切換：

![選取格線或圖表，然後選擇圖表類型](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>儲存您的度量刀鋒視窗
建立一些圖表後，請將它們儲存為我的最愛。 您可以選擇是否 tooshare 它與其他小組成員，如果您使用組織帳戶。

![選擇 [我的最愛]](./media/app-insights-metrics-explorer/21-favorite-save.png)

同樣地，toosee hello 刀鋒視窗**移 toohello 概觀刀鋒視窗**並開啟 [我的最愛]:

![在 hello 概觀刀鋒視窗中，選擇 我的最愛](./media/app-insights-metrics-explorer/22-favorite-get.png)

如果您儲存時，您可以選擇相對的時間範圍，將會與 hello 最新度量更新 hello 刀鋒視窗。 如果您選擇的絕對時間範圍，它會顯示 hello 每次相同的資料。

## <a name="reset-hello-blade"></a>重設 hello 刀鋒視窗
如果您編輯刀鋒視窗，但您希望然後 tooget 後 toohello 原始儲存集，只要按一下 重設。

![在頂端的公制總管 hello hello 按鈕](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>即時計量串流

如需更加立即的遙測檢視，請開啟[即時串流](app-insights-live-stream.md)。 大部分的度量資訊會需要幾分鐘的時間 tooappear，因為 hello 處理序的彙總。 相較之下，即時計量已針對低延遲進行最佳化。 

## <a name="set-alerts"></a>設定警示
收到的異常值的任何度量，電子郵件通知的 toobe 加入警示。 您可以選擇 toosend hello 電子郵件 toohello 帳戶系統管理員或 toospecific 電子郵件地址。

![在 [計量瀏覽器] 中，選擇 [警示規則]，然後選擇 [加入警示]](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[深入了解警示][alerts]。


## <a name="continuous-export"></a>連續匯出
如果您想要連續匯出資料，讓您能夠在外部加以處理，請考慮使用 [連續匯出](app-insights-export-telemetry.md)。

### <a name="power-bi"></a>Power BI
如果您想要有更豐富您的資料檢視，您可以[匯出 tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx)。

## <a name="analytics"></a>Analytics
[分析](app-insights-analytics.md)是更具彈性的方式 tooanalyze 您使用強大的查詢語言的遙測。 如果您想 toocombine 或計算結果的度量，或執行您的應用程式最近效能的深入瀏覽，請使用它。 

從度量的圖表，您可以按一下 hello 分析圖示 tooget 直接 toohello 相等分析查詢。

## <a name="troubleshooting"></a>疑難排解
*我看不到我的圖表上的任何資料。*

* 篩選會套用 tooall hello 圖表 hello 刀鋒視窗上。 請確定，而您要將焦點放在圖表上，您未設定排除在另一台的所有 hello 資料的篩選。

    如果您想在不同的圖表上 tooset 不同的篩選器，建立它們在不同的刀鋒視窗，將它們儲存成個別的 [我的最愛]。 如果您想，您可以將其釘選 toohello 儀表板，讓您可以看到它們彼此。
* 如果您未在 hello 度量定義的屬性來分組圖表，然後將不會有 hello 圖表上。 請嘗試清除 [分組依據]，或選擇不同的群組屬性。
* 效能資料 (CPU、IO 速率等等) 適用於 Java Web 服務、Windows 傳統型應用程式、[IIS Web 應用程式和服務 (若您安裝狀態監視器)](app-insights-monitor-performance-live-website-now.md) 和 [Azure 雲端服務](app-insights-azure.md)。 它不適用於 Azure 網站。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>後續步驟
* [使用 Application Insights 監視使用情況](app-insights-web-track-usage.md)
* [使用診斷搜尋](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
