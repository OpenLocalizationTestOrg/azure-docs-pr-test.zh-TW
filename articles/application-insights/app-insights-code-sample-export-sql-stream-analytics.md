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
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="1e20c-103">逐步解說： 使用資料流分析的 Application Insights 從匯出 tooSQL</span><span class="sxs-lookup"><span data-stu-id="1e20c-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="1e20c-104">本文將說明如何 toomove 遙測資料從[Azure Application Insights] [ start]到 Azure SQL database 使用[連續匯出][ export]和[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="1e20c-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="1e20c-105">連續匯出會以 JSON 格式將遙測資料移入 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e20c-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="1e20c-106">我們將會剖析使用 Azure Stream Analytics hello JSON 物件，並建立資料庫資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="1e20c-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="1e20c-107">(一般來說，連續匯出是 hello 方式 toodo 的 hello 遙測分析您的應用程式傳送 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="1e20c-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="1e20c-108">您無法調整此程式碼範例 toodo 匯出的 hello 遙測，例如資料彙總與其他項目。）</span><span class="sxs-lookup"><span data-stu-id="1e20c-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="1e20c-109">我們將開始 hello 假設您已經有您想要 toomonitor hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e20c-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="1e20c-110">在此範例中，我們將使用 hello 頁面檢視資料，但 hello 相同的模式可以輕易地延伸 tooother 資料類型，例如自訂事件和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1e20c-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="1e20c-111">新增 Application Insights tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="1e20c-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="1e20c-112">tooget 啟動：</span><span class="sxs-lookup"><span data-stu-id="1e20c-112">tooget started:</span></span>

1. <span data-ttu-id="1e20c-113">[為您的網頁設定 Application Insights](app-insights-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="1e20c-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="1e20c-114">(在此範例中，我們將焦點放在處理 hello 用戶端瀏覽器，從頁面檢視資料，但您可以也設定 Application Insights hello 伺服器端程式[Java](app-insights-java-get-started.md)或[ASP.NET](app-insights-asp-net.md)應用程式和處理序的要求相依性和其他伺服器遙測。)</span><span class="sxs-lookup"><span data-stu-id="1e20c-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="1e20c-115">發行應用程式，並觀察出現在 Application Insights 資源中的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="1e20c-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="1e20c-116">在 Azure 中建立儲存體</span><span class="sxs-lookup"><span data-stu-id="1e20c-116">Create storage in Azure</span></span>
<span data-ttu-id="1e20c-117">連續匯出一律會輸出資料 tooan Azure 儲存體帳戶，因此您必須先 toocreate hello 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e20c-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="1e20c-118">在 hello 您訂用帳戶中建立儲存體帳戶[Azure 入口網站][portal]。</span><span class="sxs-lookup"><span data-stu-id="1e20c-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![在 Azure 入口網站中，依序選擇 [新增]、[資料]、[儲存體]。](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="1e20c-122">建立容器</span><span class="sxs-lookup"><span data-stu-id="1e20c-122">Create a container</span></span>
   
    ![在 hello 新的存放裝置，選取容器，按一下 hello 容器磚，然後再新增](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="1e20c-124">複製 hello 儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="1e20c-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="1e20c-125">您將需要它很快就 tooset hello toohello 輸入資料流分析服務。</span><span class="sxs-lookup"><span data-stu-id="1e20c-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![在 hello 儲存體中，開啟 [設定] 索引鍵，並採取 hello 主要存取金鑰的副本](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="1e20c-127">啟動連續匯出 tooAzure 存放裝置</span><span class="sxs-lookup"><span data-stu-id="1e20c-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="1e20c-128">在 hello Azure 入口網站，瀏覽 toohello 您建立應用程式的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1e20c-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![依序選擇 [瀏覽]、[Application Insights]、您的應用程式](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="1e20c-130">建立連續匯出。</span><span class="sxs-lookup"><span data-stu-id="1e20c-130">Create a continuous export.</span></span>
   
    ![依序選擇 [設定]、[連續匯出]、[新增]](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="1e20c-132">選取您稍早建立的 hello 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="1e20c-132">Select hello storage account you created earlier:</span></span>

    ![設定 hello 匯出目的地](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="1e20c-134">設定您想要的 hello 事件類型 toosee:</span><span class="sxs-lookup"><span data-stu-id="1e20c-134">Set hello event types you want toosee:</span></span>

    ![選擇事件類型](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="1e20c-136">可讓一些資料累積。</span><span class="sxs-lookup"><span data-stu-id="1e20c-136">Let some data accumulate.</span></span> <span data-ttu-id="1e20c-137">請休息一下，讓其他人使用您的應用程式一段時間。</span><span class="sxs-lookup"><span data-stu-id="1e20c-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="1e20c-138">遙測資料會送過來，而您會在[計量瀏覽器](app-insights-metrics-explorer.md)中看到統計圖表，並在[診斷搜尋](app-insights-diagnostic-search.md)中看到個別事件。</span><span class="sxs-lookup"><span data-stu-id="1e20c-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="1e20c-139">也，hello 資料將匯出 tooyour 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1e20c-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="1e20c-140">檢查 hello 匯出資料，有兩種 hello 入口網站-選擇**瀏覽**，選取您的儲存體帳戶，然後**容器**-或 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="1e20c-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="1e20c-141">在 Visual Studio 中，依序選擇 [檢視] 和 [Cloud Explorer]，然後依序開啟 [Azure] 和 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="1e20c-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="1e20c-142">(如果您沒有此功能表選項，您需要 tooinstall hello Azure SDK： 開啟 hello 新增專案 對話方塊，並開啟 Visual C# / 雲端 / 取得 Microsoft Azure SDK for.NET。)</span><span class="sxs-lookup"><span data-stu-id="1e20c-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![在 Visual Studio 中，依序開啟 [Server Browser]、[Azure]、[儲存體]](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="1e20c-144">記下 hello hello 路徑名稱，衍生自 hello 應用程式名稱和檢測機碼的通用部分。</span><span class="sxs-lookup"><span data-stu-id="1e20c-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="1e20c-145">hello 事件會寫入 tooblob 檔案採用 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="1e20c-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="1e20c-146">每個檔案可能會包含一或多個事件。</span><span class="sxs-lookup"><span data-stu-id="1e20c-146">Each file may contain one or more events.</span></span> <span data-ttu-id="1e20c-147">因此我們想要 tooread hello 事件資料與篩選出 hello 我們想要的欄位。</span><span class="sxs-lookup"><span data-stu-id="1e20c-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="1e20c-148">我們無法使用 hello 資料執行的作業的所有類型，但是我們計劃今天 toouse Stream Analytics toomove hello 資料 tooa SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e20c-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="1e20c-149">可讓您輕鬆 toorun 許多有趣的查詢。</span><span class="sxs-lookup"><span data-stu-id="1e20c-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="1e20c-150">建立 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1e20c-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="1e20c-151">從您訂用帳戶再次開始[Azure 入口網站][portal]，建立 hello 資料庫 (以及新的伺服器，除非您已經有一個) toowhich 您會將寫入 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1e20c-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![[新增]、[資料]、[SQL]](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="1e20c-153">請確定該 hello 資料庫伺服器可讓您存取 tooAzure 服務：</span><span class="sxs-lookup"><span data-stu-id="1e20c-153">Make sure that hello database server allows access tooAzure services:</span></span>

![瀏覽、 伺服器、 您的伺服器、 設定、 防火牆，允許存取 tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="1e20c-155">在 Azure SQL Database 中建立資料表</span><span class="sxs-lookup"><span data-stu-id="1e20c-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="1e20c-156">連接 toohello hello 與慣用的管理工具的上一節中所建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e20c-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="1e20c-157">在本逐步解說中，我們將使用 [SQL Server 管理工具](https://msdn.microsoft.com/ms174173.aspx) (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="1e20c-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="1e20c-158">建立新的查詢，並執行下列 T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="1e20c-158">Create a new query, and execute hello following T-SQL:</span></span>

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

<span data-ttu-id="1e20c-159">在此範例中，我們會使用頁面檢視的資料。</span><span class="sxs-lookup"><span data-stu-id="1e20c-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="1e20c-160">toosee hello 提供的其他資料，檢查您的 JSON 輸出，然後查看 hello[匯出資料模型](app-insights-export-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1e20c-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="1e20c-161">建立 Azure 串流分析執行個體</span><span class="sxs-lookup"><span data-stu-id="1e20c-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="1e20c-162">從 hello[傳統 Azure 入口網站](https://manage.windowsazure.com/)、 選取 hello Azure Stream Analytics 服務，建立新的資料流分析工作：</span><span class="sxs-lookup"><span data-stu-id="1e20c-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="1e20c-163">建立 hello 新工作時，展開其詳細資料：</span><span class="sxs-lookup"><span data-stu-id="1e20c-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="1e20c-164">設定 Blob 位置</span><span class="sxs-lookup"><span data-stu-id="1e20c-164">Set blob location</span></span>
<span data-ttu-id="1e20c-165">設定從您的連續匯出 blob tootake 輸入：</span><span class="sxs-lookup"><span data-stu-id="1e20c-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="1e20c-166">現在您需要 hello 主要存取金鑰從您先前記下的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e20c-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="1e20c-167">將此設為 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="1e20c-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="1e20c-168">設定路徑前置詞模式</span><span class="sxs-lookup"><span data-stu-id="1e20c-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="1e20c-169">要確定 tooset hello 日期格式太**YYYY MM DD** (與**虛線**)。</span><span class="sxs-lookup"><span data-stu-id="1e20c-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="1e20c-170">hello 路徑前置詞模式會指定資料流分析 hello 儲存體中尋找 hello 輸入的檔的方式。</span><span class="sxs-lookup"><span data-stu-id="1e20c-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="1e20c-171">您需要 tooset 它 toocorrespond toohow 連續匯出儲存 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1e20c-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="1e20c-172">請設定如下：</span><span class="sxs-lookup"><span data-stu-id="1e20c-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="1e20c-173">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="1e20c-173">In this example:</span></span>

* <span data-ttu-id="1e20c-174">`webapplication27`這是 hello hello Application Insights 資源名稱**所有以小寫**。</span><span class="sxs-lookup"><span data-stu-id="1e20c-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="1e20c-175">`1234...`是 hello 的 hello Application Insights 資源的檢測金鑰**移除連字號與**。</span><span class="sxs-lookup"><span data-stu-id="1e20c-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="1e20c-176">`PageViews`hello 類型的資料，我們想 tooanalyze。</span><span class="sxs-lookup"><span data-stu-id="1e20c-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="1e20c-177">hello 可用的類型取決於您所設定的連續匯出的 hello 篩選。</span><span class="sxs-lookup"><span data-stu-id="1e20c-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="1e20c-178">檢查 hello 匯出的資料 toosee hello 其他可用的類型，並查看 hello[匯出資料模型](app-insights-export-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1e20c-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="1e20c-179">`/{date}/{time}` 是要依字面意思寫入資訊的格式。</span><span class="sxs-lookup"><span data-stu-id="1e20c-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="1e20c-180">tooget hello 名稱和 iKey 的 Application Insights 資源，其 [概觀] 頁面上，開啟 Essentials 或開啟 [設定]。</span><span class="sxs-lookup"><span data-stu-id="1e20c-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="1e20c-181">完成初始設定</span><span class="sxs-lookup"><span data-stu-id="1e20c-181">Finish initial setup</span></span>
<span data-ttu-id="1e20c-182">確認 hello 序列化格式：</span><span class="sxs-lookup"><span data-stu-id="1e20c-182">Confirm hello serialization format:</span></span>

![確認並關閉精靈](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="1e20c-184">關閉 hello 精靈，並等候 hello 設定 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1e20c-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="1e20c-185">使用 hello 範例函式 toocheck hello 輸入的路徑的設定正確。</span><span class="sxs-lookup"><span data-stu-id="1e20c-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="1e20c-186">如果失敗： 請檢查 hello hello 範例時間範圍，而您選擇的存放裝置中沒有資料。</span><span class="sxs-lookup"><span data-stu-id="1e20c-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="1e20c-187">編輯 hello 輸入的定義，請檢查設定 hello 儲存體帳戶的路徑前置詞，以及正確的日期格式。</span><span class="sxs-lookup"><span data-stu-id="1e20c-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="1e20c-188">設定查詢</span><span class="sxs-lookup"><span data-stu-id="1e20c-188">Set query</span></span>
<span data-ttu-id="1e20c-189">開啟 hello 查詢 > 一節：</span><span class="sxs-lookup"><span data-stu-id="1e20c-189">Open hello query section:</span></span>

![在串流分析中選取 [查詢]](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="1e20c-191">取代具有 hello 預設查詢：</span><span class="sxs-lookup"><span data-stu-id="1e20c-191">Replace hello default query with:</span></span>

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

<span data-ttu-id="1e20c-192">請注意，第一次 hello 幾個屬性都是特定 toopage 檢視資料。</span><span class="sxs-lookup"><span data-stu-id="1e20c-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="1e20c-193">其他遙測資料類型的匯出會有不同的屬性。</span><span class="sxs-lookup"><span data-stu-id="1e20c-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="1e20c-194">請參閱 hello[詳細 hello 屬性類型和值的資料模型參考。](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="1e20c-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="1e20c-195">設定輸出 toodatabase</span><span class="sxs-lookup"><span data-stu-id="1e20c-195">Set up output toodatabase</span></span>
<span data-ttu-id="1e20c-196">選取 SQL 做為 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="1e20c-196">Select SQL as hello output.</span></span>

![在串流分析中選取 [輸出]](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="1e20c-198">指定 hello SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e20c-198">Specify hello SQL database.</span></span>

![填入資料庫的 hello 詳細資料](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="1e20c-200">關閉 hello 精靈，並等候通知，設定 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="1e20c-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="1e20c-201">開始處理</span><span class="sxs-lookup"><span data-stu-id="1e20c-201">Start processing</span></span>
<span data-ttu-id="1e20c-202">開始從 hello 動作列 hello 工作：</span><span class="sxs-lookup"><span data-stu-id="1e20c-202">Start hello job from hello action bar:</span></span>

![在串流分析中，按一下 [開始]](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="1e20c-204">您可以選擇是否 toostart 處理 hello 資料起始從目前或 toostart 與先前的資料。</span><span class="sxs-lookup"><span data-stu-id="1e20c-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="1e20c-205">hello 後者是很有用，如果您有已經執行一段連續匯出。</span><span class="sxs-lookup"><span data-stu-id="1e20c-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![在串流分析中，按一下 [開始]](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="1e20c-207">幾分鐘後，請回到 tooSQL 伺服器管理工具，監看式中的 hello 資料流動。</span><span class="sxs-lookup"><span data-stu-id="1e20c-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="1e20c-208">例如，使用如下查詢：</span><span class="sxs-lookup"><span data-stu-id="1e20c-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="1e20c-209">相關文章</span><span class="sxs-lookup"><span data-stu-id="1e20c-209">Related articles</span></span>
* [<span data-ttu-id="1e20c-210">匯出 tooPowerBI 使用資料流分析</span><span class="sxs-lookup"><span data-stu-id="1e20c-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="1e20c-211">詳細的資料的模型 hello 屬性類型和值的參考。</span><span class="sxs-lookup"><span data-stu-id="1e20c-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="1e20c-212">Application Insights 中的連續匯出</span><span class="sxs-lookup"><span data-stu-id="1e20c-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="1e20c-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="1e20c-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

