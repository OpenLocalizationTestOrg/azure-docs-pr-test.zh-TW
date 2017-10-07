---
title: "使用 Azure Application Insights 從資料流分析 aaaExport |Microsoft 文件"
description: "資料流分析可以持續轉換、 篩選和路由 hello 資料匯出從 Application Insights。"
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>使用資料流分析 tooprocess 匯出的資料從 Application Insights
[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) hello 處理資料的理想工具[匯出從 Application Insights](app-insights-export-telemetry.md)。 串流分析可以從各種來源提取資料。 它可以轉換和篩選 hello 資料，然後路由 tooa 各種不同的接收。

在此範例中，我們將建立配接器接受資料從 Application Insights，重新命名和處理一些 hello 欄位，並將它使用管線傳送到 Power BI。

> [!WARNING]
> 有更妥善、 輕鬆地[toodisplay Power BI 中的 Application Insights 資料的建議方法](app-insights-export-power-bi.md)。 hello 如下圖所示的路徑是只是範例 tooillustrate tooprocess 匯出資料的方式。
> 
> 

![透過 SA tooPBI 匯出的區塊圖](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>在 Azure 中建立儲存體
連續匯出一律會輸出資料 tooan Azure 儲存體帳戶，因此您必須先 toocreate hello 儲存體。

1. 在 hello 您訂用帳戶中建立 「 傳統 」 的儲存體帳戶[Azure 入口網站](https://portal.azure.com)。
   
   ![在 Azure 入口網站中，依序選擇 [新增]、[資料]、[儲存體]](./media/app-insights-export-stream-analytics/030.png)
2. 建立容器
   
    ![在 hello 新的存放裝置，選取容器，按一下 hello 容器磚，然後再新增](./media/app-insights-export-stream-analytics/040.png)
3. 複製 hello 儲存體存取金鑰
   
    您將需要它很快就 tooset hello toohello 輸入資料流分析服務。
   
    ![在 hello 儲存體中，開啟 [設定] 索引鍵，並採取 hello 主要存取金鑰的副本](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>啟動連續匯出 tooAzure 存放裝置
[連續匯出](app-insights-export-telemetry.md) 會將資料從 Application Insights 移入 Azure 儲存體。

1. 在 hello Azure 入口網站，瀏覽 toohello 您建立應用程式的 Application Insights 資源。
   
    ![依序選擇 [瀏覽]、[Application Insights]、您的應用程式](./media/app-insights-export-stream-analytics/050.png)
2. 建立連續匯出。
   
    ![依序選擇 [設定]、[連續匯出]、[新增]](./media/app-insights-export-stream-analytics/060.png)

    選取您稍早建立的 hello 儲存體帳戶：

    ![設定 hello 匯出目的地](./media/app-insights-export-stream-analytics/070.png)

    設定您想要的 hello 事件類型 toosee:

    ![選擇事件類型](./media/app-insights-export-stream-analytics/080.png)

1. 可讓一些資料累積。 請休息一下，讓其他人使用您的應用程式一段時間。 遙測資料會送過來，而您會在[計量瀏覽器](app-insights-metrics-explorer.md)中看到統計圖表，並在[診斷搜尋](app-insights-diagnostic-search.md)中看到個別事件。 
   
    也，hello 資料將匯出 tooyour 儲存體。 
2. 檢查 hello 匯出資料。 在 Visual Studio 中，依序選擇 [檢視] 和 [Cloud Explorer]，然後依序開啟 [Azure] 和 [儲存體]。 (如果您沒有此功能表選項，您需要 tooinstall hello Azure SDK： 開啟 hello 新增專案 對話方塊，並開啟 Visual C# / 雲端 / 取得 Microsoft Azure SDK for.NET。)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    記下 hello hello 路徑名稱，衍生自 hello 應用程式名稱和檢測機碼的通用部分。 

hello 事件會寫入 tooblob 檔案採用 JSON 格式。 每個檔案可能會包含一或多個事件。 因此我們想要 tooread hello 事件資料與篩選出 hello 我們想要的欄位。 我們無法使用 hello 資料執行的作業的所有類型，但是我們計劃今天 toouse Stream Analytics toopipe hello 資料 tooPower BI。

## <a name="create-an-azure-stream-analytics-instance"></a>建立 Azure 串流分析執行個體
從 hello[傳統 Azure 入口網站](https://manage.windowsazure.com/)、 選取 hello Azure Stream Analytics 服務，建立新的資料流分析工作：

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

建立 hello 新工作時，展開其詳細資料：

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>設定 Blob 位置
設定從您的連續匯出 blob tootake 輸入：

![](./media/app-insights-export-stream-analytics/120.png)

現在您需要 hello 主要存取金鑰從您先前記下的儲存體帳戶。 將此設為 hello 儲存體帳戶金鑰。

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>設定路徑前置詞模式
![](./media/app-insights-export-stream-analytics/140.png)

**為確定 tooset hello 日期格式 tooYYYY-MM-DD （使用連字號）。**

hello 路徑前置詞模式會指定資料流分析 hello 儲存體中找到 hello 輸入的檔案的所在。 您需要 tooset 它 toocorrespond toohow 連續匯出儲存 hello 資料。 請設定如下：

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

在此範例中：

* `webapplication27`這是 hello hello Application Insights 資源名稱**小寫**。
* `1234...`是 hello 的 hello Application Insights 資源的檢測金鑰**省略虛線**。 
* `PageViews`hello 類型要 tooanalyze 的資料。 hello 可用的類型取決於您所設定的連續匯出的 hello 篩選。 檢查 hello 匯出的資料 toosee hello 其他可用的類型，並查看 hello[匯出資料模型](app-insights-export-data-model.md)。
* `/{date}/{time}` 是要依字面意思寫入資訊的格式。

> [!NOTE]
> 檢查儲存體 hello toomake，確定您取得 hello 路徑正確。
> 
> 

### <a name="finish-initial-setup"></a>完成初始設定
確認 hello 序列化格式：

![確認並關閉精靈](./media/app-insights-export-stream-analytics/150.png)

關閉 hello 精靈，並等候 hello 設定 toocomplete。

> [!TIP]
> 使用 hello 範例命令 toodownload 一些資料。 將其保留為測試範例 toodebug 您的查詢。
> 
> 

## <a name="set-hello-output"></a>設定 hello 輸出
現在，選取您的工作並設定 hello 輸出。

![選取 hello 新通道，然後按一下 輸出、 新增、 Power BI](./media/app-insights-export-stream-analytics/160.png)

提供您**公司或學校帳戶**tooauthorize Stream Analytics tooaccess Power BI 資源。 然後自創 hello 輸出以及 hello 目標 Power BI 資料集和資料表的名稱。

![創建三個名稱](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>設定 hello 查詢
hello 查詢會管理從輸入 toooutput hello 轉譯。

![選取 hello 作業，然後按一下 [查詢]。 貼上下列 hello 範例。](./media/app-insights-export-stream-analytics/180.png)

使用 hello 測試函式 toocheck 收到 hello 右輸出。 讓您從 hello 輸入頁面所採用的 hello 範例資料。 

### <a name="query-toodisplay-counts-of-events"></a>查詢事件 toodisplay 計數
貼上此查詢：

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* 匯出輸入是我們指定 toohello 資料流輸入 hello 別名
* pbi 輸出是我們所定義的 hello 輸出別名
* 我們使用[外部套用 GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx)在巢狀的 JSON arrray hello 事件名稱，所以。 然後選取來挑選 hello hello 事件名稱，連同 hello hello 時段中具有該名稱的執行個體數目的計數。 hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx)子句 hello 項目分組為 1 分鐘的時間週期。

### <a name="query-toodisplay-metric-values"></a>查詢 toodisplay 度量值
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* 此查詢向內切入 hello 度量遙測 tooget hello 事件時間和 hello 公制值。 hello 度量值位於陣列中，因此我們使用 hello 外部套用 GetElements 模式 tooextract hello 資料列。 「 myMetric 「 在此情況下是 hello hello 度量名稱。 

### <a name="query-tooinclude-values-of-dimension-properties"></a>查詢 tooinclude 值的維度屬性
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* 此查詢包括不含特定維度在 hello 維度陣列中的固定索引根據的 hello 維度屬性的值。

## <a name="run-hello-job"></a>執行 hello 工作
您可以在 hello toostart hello 作業不能超過選取日期。 

![選取 hello 作業，然後按一下 [查詢]。 貼上下列 hello 範例。](./media/app-insights-export-stream-analytics/190.png)

請等到 hello 工作正在執行。

## <a name="see-results-in-power-bi"></a>在 Power BI 中查看結果
> [!WARNING]
> 有更妥善、 輕鬆地[toodisplay Power BI 中的 Application Insights 資料的建議方法](app-insights-export-power-bi.md)。 hello 如下圖所示的路徑是只是範例 tooillustrate tooprocess 匯出資料的方式。
> 
> 

開啟 Power BI 與您的工作或學校帳戶，並選取 hello 資料集和您定義為 hello output hello 資料流分析作業的資料表。

![在 Power BI 中，選取您的資料集和欄位。](./media/app-insights-export-stream-analytics/200.png)

現在您可以使用報告中的此資料集和 [Power BI](https://powerbi.microsoft.com)中的儀表板。

![在 Power BI 中，選取您的資料集和欄位。](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>沒有資料？
* 請檢查您[集 hello 日期格式](#set-path-prefix-pattern)正確 tooYYYY-MM-DD （使用連字號）。

## <a name="video"></a>影片
Noam Ben Zeev 顯示 tooprocess 匯出使用資料流分析資料的方式。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>後續步驟
* [連續匯出](app-insights-export-telemetry.md)
* [詳細的資料的模型 hello 屬性類型和值的參考。](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

