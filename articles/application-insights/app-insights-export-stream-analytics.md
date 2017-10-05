---
title: "使用 Azure Application Insights 中的串流分析匯出 | Microsoft Docs"
description: "串流分析可以持續轉換、篩選和路由傳送您從 Application Insights 匯出的資料。"
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
ms.openlocfilehash: 6a84d8ff67c420ce712de905ab1172632502a863
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="6809a-103">使用串流分析來處理從 Application Insights 匯出的資料</span><span class="sxs-lookup"><span data-stu-id="6809a-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="6809a-104">[Azure 串流分析](https://azure.microsoft.com/services/stream-analytics/)是處理[從 Application Insights 匯出](app-insights-export-telemetry.md)之資料的理想工具。</span><span class="sxs-lookup"><span data-stu-id="6809a-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="6809a-105">串流分析可以從各種來源提取資料。</span><span class="sxs-lookup"><span data-stu-id="6809a-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="6809a-106">它可以轉換和篩選資料，然後將它路由傳送至各種接收。</span><span class="sxs-lookup"><span data-stu-id="6809a-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="6809a-107">在此範例中，將建立配接器，以從 Application Insights 取得資料、重新命名與處理某些欄位，以及透過管線將它傳送到 Power BI。</span><span class="sxs-lookup"><span data-stu-id="6809a-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="6809a-108">[在 Power BI 中顯示 Application Insights 資料的建議方式](app-insights-export-power-bi.md)更好也更容易。</span><span class="sxs-lookup"><span data-stu-id="6809a-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="6809a-109">這裡所述的路徑只是說明如何處理所匯出資料的範例。</span><span class="sxs-lookup"><span data-stu-id="6809a-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![透過 SA 匯出至 PBI 的區塊圖](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="6809a-111">在 Azure 中建立儲存體</span><span class="sxs-lookup"><span data-stu-id="6809a-111">Create storage in Azure</span></span>
<span data-ttu-id="6809a-112">連續匯出一律會將資料輸出至 Azure 儲存體帳戶，因此您必須先建立儲存體。</span><span class="sxs-lookup"><span data-stu-id="6809a-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="6809a-113">在 [Azure 入口網站](https://portal.azure.com)的訂用帳戶中建立「傳統」儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6809a-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![在 Azure 入口網站中，依序選擇 [新增]、[資料]、[儲存體]](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="6809a-115">建立容器</span><span class="sxs-lookup"><span data-stu-id="6809a-115">Create a container</span></span>
   
    ![在新的儲存體中，選取 [容器]，按一下容器磚，然後按一下 [新增]](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="6809a-117">複製儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="6809a-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="6809a-118">稍後您會需要使用它來設定串流分析服務的輸入。</span><span class="sxs-lookup"><span data-stu-id="6809a-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![在儲存體中，依序開啟 [設定]、[金鑰]，然後複製主要存取金鑰](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="6809a-120">啟動對 Azure 儲存體的連續匯出</span><span class="sxs-lookup"><span data-stu-id="6809a-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="6809a-121">[連續匯出](app-insights-export-telemetry.md) 會將資料從 Application Insights 移入 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6809a-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="6809a-122">在 Azure 入口網站中，瀏覽至您為應用程式建立的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="6809a-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![依序選擇 [瀏覽]、[Application Insights]、您的應用程式](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="6809a-124">建立連續匯出。</span><span class="sxs-lookup"><span data-stu-id="6809a-124">Create a continuous export.</span></span>
   
    ![依序選擇 [設定]、[連續匯出]、[新增]](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="6809a-126">選取您稍早建立的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="6809a-126">Select the storage account you created earlier:</span></span>

    ![設定匯出目的地](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="6809a-128">設定您想要查看的事件類型：</span><span class="sxs-lookup"><span data-stu-id="6809a-128">Set the event types you want to see:</span></span>

    ![選擇事件類型](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="6809a-130">可讓一些資料累積。</span><span class="sxs-lookup"><span data-stu-id="6809a-130">Let some data accumulate.</span></span> <span data-ttu-id="6809a-131">請休息一下，讓其他人使用您的應用程式一段時間。</span><span class="sxs-lookup"><span data-stu-id="6809a-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="6809a-132">遙測資料會送過來，而您會在[計量瀏覽器](app-insights-metrics-explorer.md)中看到統計圖表，並在[診斷搜尋](app-insights-diagnostic-search.md)中看到個別事件。</span><span class="sxs-lookup"><span data-stu-id="6809a-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="6809a-133">此外，資料會匯出至您的儲存體。</span><span class="sxs-lookup"><span data-stu-id="6809a-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="6809a-134">檢查匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="6809a-134">Inspect the exported data.</span></span> <span data-ttu-id="6809a-135">在 Visual Studio 中，依序選擇 [檢視] 和 [Cloud Explorer]，然後依序開啟 [Azure] 和 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="6809a-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="6809a-136">(如果您沒有此功能表選項，您需要安裝 Azure SDK：開啟 [新增專案] 對話方塊，然後開啟 [Visual C#] / [Cloud] / [取得 Microsoft Azure SDK for .NET]。)</span><span class="sxs-lookup"><span data-stu-id="6809a-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="6809a-137">記下衍生自應用程式名稱和檢測金鑰之路徑名稱的共同部分。</span><span class="sxs-lookup"><span data-stu-id="6809a-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="6809a-138">事件會以 JSON 格式寫入至 Blob 檔案。</span><span class="sxs-lookup"><span data-stu-id="6809a-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="6809a-139">每個檔案可能會包含一或多個事件。</span><span class="sxs-lookup"><span data-stu-id="6809a-139">Each file may contain one or more events.</span></span> <span data-ttu-id="6809a-140">因此我們想要讀取事件資料，並篩選出需要的欄位。</span><span class="sxs-lookup"><span data-stu-id="6809a-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="6809a-141">該處有用這些資料所能做到的所有事情種類，但我們現在計劃要使用串流分析將資料傳送至 Power BI。</span><span class="sxs-lookup"><span data-stu-id="6809a-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="6809a-142">建立 Azure 串流分析執行個體</span><span class="sxs-lookup"><span data-stu-id="6809a-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="6809a-143">在 [傳統 Azure 入口網站](https://manage.windowsazure.com/)中，選取 Azure 串流分析服務，然後建立新的串流分析工作：</span><span class="sxs-lookup"><span data-stu-id="6809a-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="6809a-144">建立新工作後，請展開其詳細資料：</span><span class="sxs-lookup"><span data-stu-id="6809a-144">When the new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="6809a-145">設定 Blob 位置</span><span class="sxs-lookup"><span data-stu-id="6809a-145">Set blob location</span></span>
<span data-ttu-id="6809a-146">將此設定為從您的連續匯出 Blob 接收輸入：</span><span class="sxs-lookup"><span data-stu-id="6809a-146">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="6809a-147">現在您需要儲存體帳戶的主要存取金鑰 (您已在稍早記下此金鑰)。</span><span class="sxs-lookup"><span data-stu-id="6809a-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="6809a-148">請將此金鑰設為儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="6809a-148">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="6809a-149">設定路徑前置詞模式</span><span class="sxs-lookup"><span data-stu-id="6809a-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="6809a-150">**請務必將 [日期格式] 設為 [YYYY-MM-DD] \(含連接號)。**</span><span class="sxs-lookup"><span data-stu-id="6809a-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="6809a-151">路徑前置詞模式會指定串流分析在存放區中尋找輸入檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="6809a-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="6809a-152">您需要將它設定為與連續匯出儲存資料的方式相對應。</span><span class="sxs-lookup"><span data-stu-id="6809a-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="6809a-153">請設定如下：</span><span class="sxs-lookup"><span data-stu-id="6809a-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="6809a-154">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="6809a-154">In this example:</span></span>

* <span data-ttu-id="6809a-155">`webapplication27` 是 Application Insights 資源名稱，**全部小寫**。</span><span class="sxs-lookup"><span data-stu-id="6809a-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="6809a-156">`1234...` 是 Application Insights 資源的檢測金鑰， **省略破折號**。</span><span class="sxs-lookup"><span data-stu-id="6809a-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="6809a-157">`PageViews` 是您想要分析的資料類型。</span><span class="sxs-lookup"><span data-stu-id="6809a-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="6809a-158">可用的類型取決於您在「連續匯出」中設定的篩選。</span><span class="sxs-lookup"><span data-stu-id="6809a-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="6809a-159">檢查匯出的資料以查看其他可用的類型，並查看 [匯出資料模型](app-insights-export-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6809a-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="6809a-160">`/{date}/{time}` 是要依字面意思寫入資訊的格式。</span><span class="sxs-lookup"><span data-stu-id="6809a-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="6809a-161">檢查儲存區以確定您取得正確的路徑。</span><span class="sxs-lookup"><span data-stu-id="6809a-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="6809a-162">完成初始設定</span><span class="sxs-lookup"><span data-stu-id="6809a-162">Finish initial setup</span></span>
<span data-ttu-id="6809a-163">確認序列化格式：</span><span class="sxs-lookup"><span data-stu-id="6809a-163">Confirm the serialization format:</span></span>

![確認並關閉精靈](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="6809a-165">關閉精靈，並等候設定完成。</span><span class="sxs-lookup"><span data-stu-id="6809a-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="6809a-166">您可以使用範例命令來下載一些資料。</span><span class="sxs-lookup"><span data-stu-id="6809a-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="6809a-167">將其保留下來做為偵錯查詢的測試範例。</span><span class="sxs-lookup"><span data-stu-id="6809a-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="6809a-168">設定輸出</span><span class="sxs-lookup"><span data-stu-id="6809a-168">Set the output</span></span>
<span data-ttu-id="6809a-169">現在選取您的工作並設定輸出。</span><span class="sxs-lookup"><span data-stu-id="6809a-169">Now select your job and set the output.</span></span>

![選取新的通道，依序按一下 [輸出]、[新增]、[Power BI]](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="6809a-171">提供您的 **工作或學校帳戶** 來授權串流分析存取您的 Power BI 資源。</span><span class="sxs-lookup"><span data-stu-id="6809a-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="6809a-172">接著自創一個輸出的名稱，以及目標 Power BI 資料集和資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="6809a-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![創建三個名稱](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="6809a-174">設定查詢</span><span class="sxs-lookup"><span data-stu-id="6809a-174">Set the query</span></span>
<span data-ttu-id="6809a-175">查詢會控管從輸入到輸出的轉譯。</span><span class="sxs-lookup"><span data-stu-id="6809a-175">The query governs the translation from input to output.</span></span>

![選取工作並按一下 [查詢]。](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="6809a-178">使用測試函式來確認您取得正確的輸出。</span><span class="sxs-lookup"><span data-stu-id="6809a-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="6809a-179">填入您從輸入頁面所採用的範例資料。</span><span class="sxs-lookup"><span data-stu-id="6809a-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="6809a-180">顯示事件計數的查詢</span><span class="sxs-lookup"><span data-stu-id="6809a-180">Query to display counts of events</span></span>
<span data-ttu-id="6809a-181">貼上此查詢：</span><span class="sxs-lookup"><span data-stu-id="6809a-181">Paste this query:</span></span>

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

* <span data-ttu-id="6809a-182">export-input 是我們提供給串流輸入的別名</span><span class="sxs-lookup"><span data-stu-id="6809a-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="6809a-183">pbi-output 是我們所定義的輸出別名</span><span class="sxs-lookup"><span data-stu-id="6809a-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="6809a-184">我們會使用 [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) ，因為事件名稱是在巢狀 JSON 陣列中。</span><span class="sxs-lookup"><span data-stu-id="6809a-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="6809a-185">然後 Select 會取用事件名稱，以及時間週期內具有該名稱之執行個體數目的計數。</span><span class="sxs-lookup"><span data-stu-id="6809a-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="6809a-186">[Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) 子句會將項目分組到 1 分鐘的時間週期內。</span><span class="sxs-lookup"><span data-stu-id="6809a-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="6809a-187">顯示度量值的查詢</span><span class="sxs-lookup"><span data-stu-id="6809a-187">Query to display metric values</span></span>
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

* <span data-ttu-id="6809a-188">此查詢會切入度量遙測，來取得事件時間和度量值。</span><span class="sxs-lookup"><span data-stu-id="6809a-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="6809a-189">度量值位於陣列中，因此我們使用 OUTER APPLY GetElements 模式來擷取資料列。</span><span class="sxs-lookup"><span data-stu-id="6809a-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="6809a-190">在此情況下，"myMetric" 是度量的名稱。</span><span class="sxs-lookup"><span data-stu-id="6809a-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="6809a-191">包含維度屬性值的查詢</span><span class="sxs-lookup"><span data-stu-id="6809a-191">Query to include values of dimension properties</span></span>
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

* <span data-ttu-id="6809a-192">此查詢包括維度屬性值，而不需根據陣列索引中固定索引的特定維度。</span><span class="sxs-lookup"><span data-stu-id="6809a-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="6809a-193">執行工作</span><span class="sxs-lookup"><span data-stu-id="6809a-193">Run the job</span></span>
<span data-ttu-id="6809a-194">您可以選取一個啟動工作的過去日期。</span><span class="sxs-lookup"><span data-stu-id="6809a-194">You can select a date in the past to start the job from.</span></span> 

![選取工作並按一下 [查詢]。](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="6809a-197">請等候直到作業執行。</span><span class="sxs-lookup"><span data-stu-id="6809a-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="6809a-198">在 Power BI 中查看結果</span><span class="sxs-lookup"><span data-stu-id="6809a-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="6809a-199">[在 Power BI 中顯示 Application Insights 資料的建議方式](app-insights-export-power-bi.md)更好也更容易。</span><span class="sxs-lookup"><span data-stu-id="6809a-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="6809a-200">這裡所述的路徑只是說明如何處理所匯出資料的範例。</span><span class="sxs-lookup"><span data-stu-id="6809a-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="6809a-201">以您的工作或學校帳戶開啟 Power BI，並選取您定義為串流分析工作輸出的資料集與資料表。</span><span class="sxs-lookup"><span data-stu-id="6809a-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![在 Power BI 中，選取您的資料集和欄位。](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="6809a-203">現在您可以使用報告中的此資料集和 [Power BI](https://powerbi.microsoft.com)中的儀表板。</span><span class="sxs-lookup"><span data-stu-id="6809a-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![在 Power BI 中，選取您的資料集和欄位。](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="6809a-205">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="6809a-205">No data?</span></span>
* <span data-ttu-id="6809a-206">請檢查是否正確 [設定日期格式](#set-path-prefix-pattern) ：YYYY-MM-DD (含連接號)。</span><span class="sxs-lookup"><span data-stu-id="6809a-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="6809a-207">影片</span><span class="sxs-lookup"><span data-stu-id="6809a-207">Video</span></span>
<span data-ttu-id="6809a-208">Noam Ben Zeev 示範如何使用串流分析來處理匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="6809a-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6809a-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6809a-209">Next steps</span></span>
* [<span data-ttu-id="6809a-210">連續匯出</span><span class="sxs-lookup"><span data-stu-id="6809a-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="6809a-211">屬性類型和值的詳細資料模型參考。</span><span class="sxs-lookup"><span data-stu-id="6809a-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="6809a-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="6809a-212">Application Insights</span></span>](app-insights-overview.md)

