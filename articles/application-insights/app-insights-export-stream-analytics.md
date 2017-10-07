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
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="94721-103">使用資料流分析 tooprocess 匯出的資料從 Application Insights</span><span class="sxs-lookup"><span data-stu-id="94721-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="94721-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) hello 處理資料的理想工具[匯出從 Application Insights](app-insights-export-telemetry.md)。</span><span class="sxs-lookup"><span data-stu-id="94721-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="94721-105">串流分析可以從各種來源提取資料。</span><span class="sxs-lookup"><span data-stu-id="94721-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="94721-106">它可以轉換和篩選 hello 資料，然後路由 tooa 各種不同的接收。</span><span class="sxs-lookup"><span data-stu-id="94721-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="94721-107">在此範例中，我們將建立配接器接受資料從 Application Insights，重新命名和處理一些 hello 欄位，並將它使用管線傳送到 Power BI。</span><span class="sxs-lookup"><span data-stu-id="94721-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="94721-108">有更妥善、 輕鬆地[toodisplay Power BI 中的 Application Insights 資料的建議方法](app-insights-export-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="94721-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="94721-109">hello 如下圖所示的路徑是只是範例 tooillustrate tooprocess 匯出資料的方式。</span><span class="sxs-lookup"><span data-stu-id="94721-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![透過 SA tooPBI 匯出的區塊圖](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="94721-111">在 Azure 中建立儲存體</span><span class="sxs-lookup"><span data-stu-id="94721-111">Create storage in Azure</span></span>
<span data-ttu-id="94721-112">連續匯出一律會輸出資料 tooan Azure 儲存體帳戶，因此您必須先 toocreate hello 儲存體。</span><span class="sxs-lookup"><span data-stu-id="94721-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="94721-113">在 hello 您訂用帳戶中建立 「 傳統 」 的儲存體帳戶[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="94721-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![在 Azure 入口網站中，依序選擇 [新增]、[資料]、[儲存體]](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="94721-115">建立容器</span><span class="sxs-lookup"><span data-stu-id="94721-115">Create a container</span></span>
   
    ![在 hello 新的存放裝置，選取容器，按一下 hello 容器磚，然後再新增](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="94721-117">複製 hello 儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="94721-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="94721-118">您將需要它很快就 tooset hello toohello 輸入資料流分析服務。</span><span class="sxs-lookup"><span data-stu-id="94721-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![在 hello 儲存體中，開啟 [設定] 索引鍵，並採取 hello 主要存取金鑰的副本](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="94721-120">啟動連續匯出 tooAzure 存放裝置</span><span class="sxs-lookup"><span data-stu-id="94721-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="94721-121">[連續匯出](app-insights-export-telemetry.md) 會將資料從 Application Insights 移入 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="94721-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="94721-122">在 hello Azure 入口網站，瀏覽 toohello 您建立應用程式的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="94721-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![依序選擇 [瀏覽]、[Application Insights]、您的應用程式](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="94721-124">建立連續匯出。</span><span class="sxs-lookup"><span data-stu-id="94721-124">Create a continuous export.</span></span>
   
    ![依序選擇 [設定]、[連續匯出]、[新增]](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="94721-126">選取您稍早建立的 hello 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="94721-126">Select hello storage account you created earlier:</span></span>

    ![設定 hello 匯出目的地](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="94721-128">設定您想要的 hello 事件類型 toosee:</span><span class="sxs-lookup"><span data-stu-id="94721-128">Set hello event types you want toosee:</span></span>

    ![選擇事件類型](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="94721-130">可讓一些資料累積。</span><span class="sxs-lookup"><span data-stu-id="94721-130">Let some data accumulate.</span></span> <span data-ttu-id="94721-131">請休息一下，讓其他人使用您的應用程式一段時間。</span><span class="sxs-lookup"><span data-stu-id="94721-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="94721-132">遙測資料會送過來，而您會在[計量瀏覽器](app-insights-metrics-explorer.md)中看到統計圖表，並在[診斷搜尋](app-insights-diagnostic-search.md)中看到個別事件。</span><span class="sxs-lookup"><span data-stu-id="94721-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="94721-133">也，hello 資料將匯出 tooyour 儲存體。</span><span class="sxs-lookup"><span data-stu-id="94721-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="94721-134">檢查 hello 匯出資料。</span><span class="sxs-lookup"><span data-stu-id="94721-134">Inspect hello exported data.</span></span> <span data-ttu-id="94721-135">在 Visual Studio 中，依序選擇 [檢視] 和 [Cloud Explorer]，然後依序開啟 [Azure] 和 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="94721-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="94721-136">(如果您沒有此功能表選項，您需要 tooinstall hello Azure SDK： 開啟 hello 新增專案 對話方塊，並開啟 Visual C# / 雲端 / 取得 Microsoft Azure SDK for.NET。)</span><span class="sxs-lookup"><span data-stu-id="94721-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="94721-137">記下 hello hello 路徑名稱，衍生自 hello 應用程式名稱和檢測機碼的通用部分。</span><span class="sxs-lookup"><span data-stu-id="94721-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="94721-138">hello 事件會寫入 tooblob 檔案採用 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="94721-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="94721-139">每個檔案可能會包含一或多個事件。</span><span class="sxs-lookup"><span data-stu-id="94721-139">Each file may contain one or more events.</span></span> <span data-ttu-id="94721-140">因此我們想要 tooread hello 事件資料與篩選出 hello 我們想要的欄位。</span><span class="sxs-lookup"><span data-stu-id="94721-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="94721-141">我們無法使用 hello 資料執行的作業的所有類型，但是我們計劃今天 toouse Stream Analytics toopipe hello 資料 tooPower BI。</span><span class="sxs-lookup"><span data-stu-id="94721-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="94721-142">建立 Azure 串流分析執行個體</span><span class="sxs-lookup"><span data-stu-id="94721-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="94721-143">從 hello[傳統 Azure 入口網站](https://manage.windowsazure.com/)、 選取 hello Azure Stream Analytics 服務，建立新的資料流分析工作：</span><span class="sxs-lookup"><span data-stu-id="94721-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="94721-144">建立 hello 新工作時，展開其詳細資料：</span><span class="sxs-lookup"><span data-stu-id="94721-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="94721-145">設定 Blob 位置</span><span class="sxs-lookup"><span data-stu-id="94721-145">Set blob location</span></span>
<span data-ttu-id="94721-146">設定從您的連續匯出 blob tootake 輸入：</span><span class="sxs-lookup"><span data-stu-id="94721-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="94721-147">現在您需要 hello 主要存取金鑰從您先前記下的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="94721-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="94721-148">將此設為 hello 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="94721-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="94721-149">設定路徑前置詞模式</span><span class="sxs-lookup"><span data-stu-id="94721-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="94721-150">**為確定 tooset hello 日期格式 tooYYYY-MM-DD （使用連字號）。**</span><span class="sxs-lookup"><span data-stu-id="94721-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="94721-151">hello 路徑前置詞模式會指定資料流分析 hello 儲存體中找到 hello 輸入的檔案的所在。</span><span class="sxs-lookup"><span data-stu-id="94721-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="94721-152">您需要 tooset 它 toocorrespond toohow 連續匯出儲存 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="94721-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="94721-153">請設定如下：</span><span class="sxs-lookup"><span data-stu-id="94721-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="94721-154">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="94721-154">In this example:</span></span>

* <span data-ttu-id="94721-155">`webapplication27`這是 hello hello Application Insights 資源名稱**小寫**。</span><span class="sxs-lookup"><span data-stu-id="94721-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="94721-156">`1234...`是 hello 的 hello Application Insights 資源的檢測金鑰**省略虛線**。</span><span class="sxs-lookup"><span data-stu-id="94721-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="94721-157">`PageViews`hello 類型要 tooanalyze 的資料。</span><span class="sxs-lookup"><span data-stu-id="94721-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="94721-158">hello 可用的類型取決於您所設定的連續匯出的 hello 篩選。</span><span class="sxs-lookup"><span data-stu-id="94721-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="94721-159">檢查 hello 匯出的資料 toosee hello 其他可用的類型，並查看 hello[匯出資料模型](app-insights-export-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="94721-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="94721-160">`/{date}/{time}` 是要依字面意思寫入資訊的格式。</span><span class="sxs-lookup"><span data-stu-id="94721-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="94721-161">檢查儲存體 hello toomake，確定您取得 hello 路徑正確。</span><span class="sxs-lookup"><span data-stu-id="94721-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="94721-162">完成初始設定</span><span class="sxs-lookup"><span data-stu-id="94721-162">Finish initial setup</span></span>
<span data-ttu-id="94721-163">確認 hello 序列化格式：</span><span class="sxs-lookup"><span data-stu-id="94721-163">Confirm hello serialization format:</span></span>

![確認並關閉精靈](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="94721-165">關閉 hello 精靈，並等候 hello 設定 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="94721-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="94721-166">使用 hello 範例命令 toodownload 一些資料。</span><span class="sxs-lookup"><span data-stu-id="94721-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="94721-167">將其保留為測試範例 toodebug 您的查詢。</span><span class="sxs-lookup"><span data-stu-id="94721-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="94721-168">設定 hello 輸出</span><span class="sxs-lookup"><span data-stu-id="94721-168">Set hello output</span></span>
<span data-ttu-id="94721-169">現在，選取您的工作並設定 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="94721-169">Now select your job and set hello output.</span></span>

![選取 hello 新通道，然後按一下 輸出、 新增、 Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="94721-171">提供您**公司或學校帳戶**tooauthorize Stream Analytics tooaccess Power BI 資源。</span><span class="sxs-lookup"><span data-stu-id="94721-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="94721-172">然後自創 hello 輸出以及 hello 目標 Power BI 資料集和資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="94721-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![創建三個名稱](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="94721-174">設定 hello 查詢</span><span class="sxs-lookup"><span data-stu-id="94721-174">Set hello query</span></span>
<span data-ttu-id="94721-175">hello 查詢會管理從輸入 toooutput hello 轉譯。</span><span class="sxs-lookup"><span data-stu-id="94721-175">hello query governs hello translation from input toooutput.</span></span>

![選取 hello 作業，然後按一下 [查詢]。](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="94721-178">使用 hello 測試函式 toocheck 收到 hello 右輸出。</span><span class="sxs-lookup"><span data-stu-id="94721-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="94721-179">讓您從 hello 輸入頁面所採用的 hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="94721-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="94721-180">查詢事件 toodisplay 計數</span><span class="sxs-lookup"><span data-stu-id="94721-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="94721-181">貼上此查詢：</span><span class="sxs-lookup"><span data-stu-id="94721-181">Paste this query:</span></span>

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

* <span data-ttu-id="94721-182">匯出輸入是我們指定 toohello 資料流輸入 hello 別名</span><span class="sxs-lookup"><span data-stu-id="94721-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="94721-183">pbi 輸出是我們所定義的 hello 輸出別名</span><span class="sxs-lookup"><span data-stu-id="94721-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="94721-184">我們使用[外部套用 GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx)在巢狀的 JSON arrray hello 事件名稱，所以。</span><span class="sxs-lookup"><span data-stu-id="94721-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="94721-185">然後選取來挑選 hello hello 事件名稱，連同 hello hello 時段中具有該名稱的執行個體數目的計數。</span><span class="sxs-lookup"><span data-stu-id="94721-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="94721-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx)子句 hello 項目分組為 1 分鐘的時間週期。</span><span class="sxs-lookup"><span data-stu-id="94721-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="94721-187">查詢 toodisplay 度量值</span><span class="sxs-lookup"><span data-stu-id="94721-187">Query toodisplay metric values</span></span>
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

* <span data-ttu-id="94721-188">此查詢向內切入 hello 度量遙測 tooget hello 事件時間和 hello 公制值。</span><span class="sxs-lookup"><span data-stu-id="94721-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="94721-189">hello 度量值位於陣列中，因此我們使用 hello 外部套用 GetElements 模式 tooextract hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="94721-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="94721-190">「 myMetric 「 在此情況下是 hello hello 度量名稱。</span><span class="sxs-lookup"><span data-stu-id="94721-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="94721-191">查詢 tooinclude 值的維度屬性</span><span class="sxs-lookup"><span data-stu-id="94721-191">Query tooinclude values of dimension properties</span></span>
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

* <span data-ttu-id="94721-192">此查詢包括不含特定維度在 hello 維度陣列中的固定索引根據的 hello 維度屬性的值。</span><span class="sxs-lookup"><span data-stu-id="94721-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="94721-193">執行 hello 工作</span><span class="sxs-lookup"><span data-stu-id="94721-193">Run hello job</span></span>
<span data-ttu-id="94721-194">您可以在 hello toostart hello 作業不能超過選取日期。</span><span class="sxs-lookup"><span data-stu-id="94721-194">You can select a date in hello past toostart hello job from.</span></span> 

![選取 hello 作業，然後按一下 [查詢]。](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="94721-197">請等到 hello 工作正在執行。</span><span class="sxs-lookup"><span data-stu-id="94721-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="94721-198">在 Power BI 中查看結果</span><span class="sxs-lookup"><span data-stu-id="94721-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="94721-199">有更妥善、 輕鬆地[toodisplay Power BI 中的 Application Insights 資料的建議方法](app-insights-export-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="94721-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="94721-200">hello 如下圖所示的路徑是只是範例 tooillustrate tooprocess 匯出資料的方式。</span><span class="sxs-lookup"><span data-stu-id="94721-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="94721-201">開啟 Power BI 與您的工作或學校帳戶，並選取 hello 資料集和您定義為 hello output hello 資料流分析作業的資料表。</span><span class="sxs-lookup"><span data-stu-id="94721-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![在 Power BI 中，選取您的資料集和欄位。](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="94721-203">現在您可以使用報告中的此資料集和 [Power BI](https://powerbi.microsoft.com)中的儀表板。</span><span class="sxs-lookup"><span data-stu-id="94721-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![在 Power BI 中，選取您的資料集和欄位。](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="94721-205">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="94721-205">No data?</span></span>
* <span data-ttu-id="94721-206">請檢查您[集 hello 日期格式](#set-path-prefix-pattern)正確 tooYYYY-MM-DD （使用連字號）。</span><span class="sxs-lookup"><span data-stu-id="94721-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="94721-207">影片</span><span class="sxs-lookup"><span data-stu-id="94721-207">Video</span></span>
<span data-ttu-id="94721-208">Noam Ben Zeev 顯示 tooprocess 匯出使用資料流分析資料的方式。</span><span class="sxs-lookup"><span data-stu-id="94721-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="94721-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94721-209">Next steps</span></span>
* [<span data-ttu-id="94721-210">連續匯出</span><span class="sxs-lookup"><span data-stu-id="94721-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="94721-211">詳細的資料的模型 hello 屬性類型和值的參考。</span><span class="sxs-lookup"><span data-stu-id="94721-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="94721-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="94721-212">Application Insights</span></span>](app-insights-overview.md)

