---
title: "從 Azure Application Insights 匯出 tooSQL |Microsoft 文件"
description: "連續匯出 Application Insights 資料 tooSQL 使用資料流分析。"
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a>逐步解說： 使用資料流分析的 Application Insights 從匯出 tooSQL
本文將說明如何 toomove 遙測資料從[Azure Application Insights] [ start]到 Azure SQL database 使用[連續匯出][ export]和[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)。 

連續匯出會以 JSON 格式將遙測資料移入 Azure 儲存體。 我們將會剖析使用 Azure Stream Analytics hello JSON 物件，並建立資料庫資料表中的資料列。

(一般來說，連續匯出是 hello 方式 toodo 的 hello 遙測分析您的應用程式傳送 tooApplication 深入資訊。 您無法調整此程式碼範例 toodo 匯出的 hello 遙測，例如資料彙總與其他項目。）

我們將開始 hello 假設您已經有您想要 toomonitor hello 應用程式。

在此範例中，我們將使用 hello 頁面檢視資料，但 hello 相同的模式可以輕易地延伸 tooother 資料類型，例如自訂事件和例外狀況。 

## <a name="add-application-insights-tooyour-application"></a>新增 Application Insights tooyour 應用程式
tooget 啟動：

1. [為您的網頁設定 Application Insights](app-insights-javascript.md)。 
   
    (在此範例中，我們將焦點放在處理 hello 用戶端瀏覽器，從頁面檢視資料，但您可以也設定 Application Insights hello 伺服器端程式[Java](app-insights-java-get-started.md)或[ASP.NET](app-insights-asp-net.md)應用程式和處理序的要求相依性和其他伺服器遙測。)
2. 發行應用程式，並觀察出現在 Application Insights 資源中的遙測資料。

## <a name="create-storage-in-azure"></a>在 Azure 中建立儲存體
連續匯出一律會輸出資料 tooan Azure 儲存體帳戶，因此您必須先 toocreate hello 儲存體。

1. 在 hello 您訂用帳戶中建立儲存體帳戶[Azure 入口網站][portal]。
   
    ![在 Azure 入口網站中，依序選擇 [新增]、[資料]、[儲存體]。 選取 [傳統]，然後選擇 [建立]。 提供儲存體的名稱。](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. 建立容器
   
    ![在 hello 新的存放裝置，選取容器，按一下 hello 容器磚，然後再新增](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. 複製 hello 儲存體存取金鑰
   
    您將需要它很快就 tooset hello toohello 輸入資料流分析服務。
   
    ![在 hello 儲存體中，開啟 [設定] 索引鍵，並採取 hello 主要存取金鑰的副本](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a>啟動連續匯出 tooAzure 存放裝置
1. 在 hello Azure 入口網站，瀏覽 toohello 您建立應用程式的 Application Insights 資源。
   
    ![依序選擇 [瀏覽]、[Application Insights]、您的應用程式](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. 建立連續匯出。
   
    ![依序選擇 [設定]、[連續匯出]、[新增]](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    選取您稍早建立的 hello 儲存體帳戶：

    ![設定 hello 匯出目的地](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    設定您想要的 hello 事件類型 toosee:

    ![選擇事件類型](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. 可讓一些資料累積。 請休息一下，讓其他人使用您的應用程式一段時間。 遙測資料會送過來，而您會在[計量瀏覽器](app-insights-metrics-explorer.md)中看到統計圖表，並在[診斷搜尋](app-insights-diagnostic-search.md)中看到個別事件。 
   
    也，hello 資料將匯出 tooyour 儲存體。 
2. 檢查 hello 匯出資料，有兩種 hello 入口網站-選擇**瀏覽**，選取您的儲存體帳戶，然後**容器**-或 Visual Studio 中。 在 Visual Studio 中，依序選擇 [檢視] 和 [Cloud Explorer]，然後依序開啟 [Azure] 和 [儲存體]。 (如果您沒有此功能表選項，您需要 tooinstall hello Azure SDK： 開啟 hello 新增專案 對話方塊，並開啟 Visual C# / 雲端 / 取得 Microsoft Azure SDK for.NET。)
   
    ![在 Visual Studio 中，依序開啟 [Server Browser]、[Azure]、[儲存體]](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    記下 hello hello 路徑名稱，衍生自 hello 應用程式名稱和檢測機碼的通用部分。 

hello 事件會寫入 tooblob 檔案採用 JSON 格式。 每個檔案可能會包含一或多個事件。 因此我們想要 tooread hello 事件資料與篩選出 hello 我們想要的欄位。 我們無法使用 hello 資料執行的作業的所有類型，但是我們計劃今天 toouse Stream Analytics toomove hello 資料 tooa SQL 資料庫。 可讓您輕鬆 toorun 許多有趣的查詢。

## <a name="create-an-azure-sql-database"></a>建立 Azure SQL Database
從您訂用帳戶再次開始[Azure 入口網站][portal]，建立 hello 資料庫 (以及新的伺服器，除非您已經有一個) toowhich 您會將寫入 hello 資料。

![[新增]、[資料]、[SQL]](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

請確定該 hello 資料庫伺服器可讓您存取 tooAzure 服務：

![瀏覽、 伺服器、 您的伺服器、 設定、 防火牆，允許存取 tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a>在 Azure SQL Database 中建立資料表
連接 toohello hello 與慣用的管理工具的上一節中所建立的資料庫。 在本逐步解說中，我們將使用 [SQL Server 管理工具](https://msdn.microsoft.com/ms174173.aspx) (SSMS)。

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

建立新的查詢，並執行下列 T-SQL hello:

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

在此範例中，我們會使用頁面檢視的資料。 toosee hello 提供的其他資料，檢查您的 JSON 輸出，然後查看 hello[匯出資料模型](app-insights-export-data-model.md)。

## <a name="create-an-azure-stream-analytics-instance"></a>建立 Azure 串流分析執行個體
從 hello[傳統 Azure 入口網站](https://manage.windowsazure.com/)、 選取 hello Azure Stream Analytics 服務，建立新的資料流分析工作：

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

建立 hello 新工作時，展開其詳細資料：

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a>設定 Blob 位置
設定從您的連續匯出 blob tootake 輸入：

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

現在您需要 hello 主要存取金鑰從您先前記下的儲存體帳戶。 將此設為 hello 儲存體帳戶金鑰。

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a>設定路徑前置詞模式
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

要確定 tooset hello 日期格式太**YYYY MM DD** (與**虛線**)。

hello 路徑前置詞模式會指定資料流分析 hello 儲存體中尋找 hello 輸入的檔的方式。 您需要 tooset 它 toocorrespond toohow 連續匯出儲存 hello 資料。 請設定如下：

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

在此範例中：

* `webapplication27`這是 hello hello Application Insights 資源名稱**所有以小寫**。 
* `1234...`是 hello 的 hello Application Insights 資源的檢測金鑰**移除連字號與**。 
* `PageViews`hello 類型的資料，我們想 tooanalyze。 hello 可用的類型取決於您所設定的連續匯出的 hello 篩選。 檢查 hello 匯出的資料 toosee hello 其他可用的類型，並查看 hello[匯出資料模型](app-insights-export-data-model.md)。
* `/{date}/{time}` 是要依字面意思寫入資訊的格式。

tooget hello 名稱和 iKey 的 Application Insights 資源，其 [概觀] 頁面上，開啟 Essentials 或開啟 [設定]。

#### <a name="finish-initial-setup"></a>完成初始設定
確認 hello 序列化格式：

![確認並關閉精靈](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

關閉 hello 精靈，並等候 hello 設定 toocomplete。

> [!TIP]
> 使用 hello 範例函式 toocheck hello 輸入的路徑的設定正確。 如果失敗： 請檢查 hello hello 範例時間範圍，而您選擇的存放裝置中沒有資料。 編輯 hello 輸入的定義，請檢查設定 hello 儲存體帳戶的路徑前置詞，以及正確的日期格式。
> 
> 

## <a name="set-query"></a>設定查詢
開啟 hello 查詢 > 一節：

![在串流分析中選取 [查詢]](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

取代具有 hello 預設查詢：

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

請注意，第一次 hello 幾個屬性都是特定 toopage 檢視資料。 其他遙測資料類型的匯出會有不同的屬性。 請參閱 hello[詳細 hello 屬性類型和值的資料模型參考。](app-insights-export-data-model.md)

## <a name="set-up-output-toodatabase"></a>設定輸出 toodatabase
選取 SQL 做為 hello 輸出。

![在串流分析中選取 [輸出]](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

指定 hello SQL 資料庫。

![填入資料庫的 hello 詳細資料](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

關閉 hello 精靈，並等候通知，設定 hello 輸出。

## <a name="start-processing"></a>開始處理
開始從 hello 動作列 hello 工作：

![在串流分析中，按一下 [開始]](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

您可以選擇是否 toostart 處理 hello 資料起始從目前或 toostart 與先前的資料。 hello 後者是很有用，如果您有已經執行一段連續匯出。

![在串流分析中，按一下 [開始]](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

幾分鐘後，請回到 tooSQL 伺服器管理工具，監看式中的 hello 資料流動。 例如，使用如下查詢：

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a>相關文章
* [匯出 tooPowerBI 使用資料流分析](app-insights-export-power-bi.md)
* [詳細的資料的模型 hello 屬性類型和值的參考。](app-insights-export-data-model.md)
* [Application Insights 中的連續匯出](app-insights-export-telemetry.md)
* [Application Insights](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

