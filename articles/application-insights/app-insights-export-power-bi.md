---
title: "從 Application Insights aaaExport tooPower BI |Microsoft 文件"
description: "Analytics 查詢可以在 Power BI 中顯示。"
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="bee5a-103">從 Application Insights 提供 Power BI</span><span class="sxs-lookup"><span data-stu-id="bee5a-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="bee5a-104">[Power BI](http://www.powerbi.com/) 是一套商務分析工具，可協助您分析資料及分享見解。</span><span class="sxs-lookup"><span data-stu-id="bee5a-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="bee5a-105">每個裝置上都提供豐富的儀表板。</span><span class="sxs-lookup"><span data-stu-id="bee5a-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="bee5a-106">您可以結合許多來源的資料，包含來自 [Azure Application Insights](app-insights-overview.md) 的「分析」查詢。</span><span class="sxs-lookup"><span data-stu-id="bee5a-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="bee5a-107">有三種建議的方法，是要將 Application Insights 資料 tooPower BI 匯出。</span><span class="sxs-lookup"><span data-stu-id="bee5a-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="bee5a-108">您可以單獨或一起使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="bee5a-108">You can use them separately or together.</span></span>

* <span data-ttu-id="bee5a-109">[**Power BI 配接器**](#power-pi-adapter) - 從您的應用程式設定完整的遙測儀表板。</span><span class="sxs-lookup"><span data-stu-id="bee5a-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="bee5a-110">hello 組圖表預先定義的但您可以從任何其他來源加入您自己的查詢。</span><span class="sxs-lookup"><span data-stu-id="bee5a-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="bee5a-111">[**匯出分析查詢**](#export-analytics-queries) -撰寫任何查詢，您想要使用分析，並將它匯出 tooPower BI。</span><span class="sxs-lookup"><span data-stu-id="bee5a-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="bee5a-112">您可以將此查詢和任何其他資料一起放在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="bee5a-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="bee5a-113">[**連續匯出和資料流分析**](app-insights-export-stream-analytics.md) -這項作業包括多個工作 tooset 組成。</span><span class="sxs-lookup"><span data-stu-id="bee5a-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="bee5a-114">如果您長時間希望 tookeep 資料時，就會很有用。</span><span class="sxs-lookup"><span data-stu-id="bee5a-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="bee5a-115">否則，hello 其他方法建議使用。</span><span class="sxs-lookup"><span data-stu-id="bee5a-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="bee5a-116">Power BI 配接器</span><span class="sxs-lookup"><span data-stu-id="bee5a-116">Power BI adapter</span></span>
<span data-ttu-id="bee5a-117">這個方法會為您建立完整的遙測儀表板。</span><span class="sxs-lookup"><span data-stu-id="bee5a-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="bee5a-118">hello 初始資料集預先定義的但您可以加入更多資料 tooit。</span><span class="sxs-lookup"><span data-stu-id="bee5a-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="bee5a-119">取得 hello 配接器</span><span class="sxs-lookup"><span data-stu-id="bee5a-119">Get hello adapter</span></span>
1. <span data-ttu-id="bee5a-120">登入太[Power BI](https://app.powerbi.com/)。</span><span class="sxs-lookup"><span data-stu-id="bee5a-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="bee5a-121">依序開啟 [取得資料]、[服務] 和 [Application Insights]</span><span class="sxs-lookup"><span data-stu-id="bee5a-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![取自 Application Insights 資料來源](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="bee5a-123">提供 Application Insights 資源 「 hello 」 詳細的資料。</span><span class="sxs-lookup"><span data-stu-id="bee5a-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![取自 Application Insights 資料來源](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="bee5a-125">等候一分鐘或兩個進行 hello 資料 toobe 匯入。</span><span class="sxs-lookup"><span data-stu-id="bee5a-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Power BI 配接器](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="bee5a-127">您可以編輯 hello 儀表板，與其他來源，以及分析查詢結合 hello Application Insights 圖表。</span><span class="sxs-lookup"><span data-stu-id="bee5a-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="bee5a-128">還有一個視覺效果資源庫，您可以從中取得更多圖表，且每個圖表都有您可以設定的參數。</span><span class="sxs-lookup"><span data-stu-id="bee5a-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="bee5a-129">Hello 初始匯入、 hello 儀表板及報表 hello 之後繼續執行每日 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="bee5a-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="bee5a-130">您可以控制 hello hello 資料集上的重新整理排程。</span><span class="sxs-lookup"><span data-stu-id="bee5a-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="bee5a-131">匯出 Analytics 查詢</span><span class="sxs-lookup"><span data-stu-id="bee5a-131">Export Analytics queries</span></span>
<span data-ttu-id="bee5a-132">此路由可讓您 toowrite 任何分析，您查詢，然後再匯出該 tooa Power BI 儀表板。</span><span class="sxs-lookup"><span data-stu-id="bee5a-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="bee5a-133">（您可以新增 toohello hello 配接器所建立的儀表板）。</span><span class="sxs-lookup"><span data-stu-id="bee5a-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="bee5a-134">一次︰安裝 Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="bee5a-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="bee5a-135">tooimport Application Insights 查詢，並使用 hello 桌面版本的 Power BI。</span><span class="sxs-lookup"><span data-stu-id="bee5a-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="bee5a-136">但是，然後您可以將其發行 toohello web 或 tooyour Power BI 雲端工作區。</span><span class="sxs-lookup"><span data-stu-id="bee5a-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="bee5a-137">安裝 [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/)。</span><span class="sxs-lookup"><span data-stu-id="bee5a-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="bee5a-138">匯出 Analytics 查詢</span><span class="sxs-lookup"><span data-stu-id="bee5a-138">Export an Analytics query</span></span>
1. <span data-ttu-id="bee5a-139">[開啟 Analytics 並撰寫查詢](app-insights-analytics-tour.md)。</span><span class="sxs-lookup"><span data-stu-id="bee5a-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="bee5a-140">測試和精簡 hello 的查詢，直到您滿意 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="bee5a-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="bee5a-141">**請確定該回合正確在分析之前將它匯出的 hello 查詢。**</span><span class="sxs-lookup"><span data-stu-id="bee5a-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="bee5a-142">在 hello**匯出**功能表上，選擇**Power BI (M)**。</span><span class="sxs-lookup"><span data-stu-id="bee5a-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="bee5a-143">儲存 hello 文字檔案。</span><span class="sxs-lookup"><span data-stu-id="bee5a-143">Save hello text file.</span></span>
   
    ![匯出 Power BI 查詢](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="bee5a-145">在 Power BI Desktop 選取**取得資料，空白查詢**然後在 hello 中查詢下方 編輯器 中，**檢視**選取**進階查詢編輯器**。</span><span class="sxs-lookup"><span data-stu-id="bee5a-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="bee5a-146">貼上至匯出的 hello M 語言指令碼 hello 進階查詢編輯器。</span><span class="sxs-lookup"><span data-stu-id="bee5a-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![進階查詢編輯器](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="bee5a-148">您可能必須 tooprovide 認證 tooallow Power BI tooaccess Azure。</span><span class="sxs-lookup"><span data-stu-id="bee5a-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="bee5a-149">使用 「 組織帳戶 」 toosign 使用 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bee5a-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![提供 Azure 認證 tooenable Power BI toorun Application Insights 查詢](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="bee5a-151">（如果您需要 tooverify hello 認證時，使用 hello 資料來源設定 功能表命令在 hello 查詢編輯器中。</span><span class="sxs-lookup"><span data-stu-id="bee5a-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="bee5a-152">需要注意您使用 Azure，這可能會不同於您的認證，Power bi toospecify hello 認證）。</span><span class="sxs-lookup"><span data-stu-id="bee5a-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="bee5a-153">選擇您的查詢的視覺效果，然後選取 hello 和欄位的 x 軸、 y 軸，切割維度。</span><span class="sxs-lookup"><span data-stu-id="bee5a-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![選取視覺效果](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="bee5a-155">發行報表 tooyour Power BI 雲端工作區。</span><span class="sxs-lookup"><span data-stu-id="bee5a-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="bee5a-156">您可以從該處將同步版本內嵌至其他網頁。</span><span class="sxs-lookup"><span data-stu-id="bee5a-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![選取視覺效果](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="bee5a-158">在時間間隔，以手動方式重新整理 hello 報表，或設定排定的重新整理 hello 選項 頁面上。</span><span class="sxs-lookup"><span data-stu-id="bee5a-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bee5a-159">疑難排解</span><span class="sxs-lookup"><span data-stu-id="bee5a-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="bee5a-160">401 或 403 未經授權</span><span class="sxs-lookup"><span data-stu-id="bee5a-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="bee5a-161">如果您的重新整理權杖尚未更新，可能會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="bee5a-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="bee5a-162">您仍然可以存取這些步驟 tooensure 再試一次。</span><span class="sxs-lookup"><span data-stu-id="bee5a-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="bee5a-163">如果您沒有存取 refershing hello 認證無法運作，請開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="bee5a-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="bee5a-164">登入 hello Azure 入口網站，並確定您可以存取 hello 資源</span><span class="sxs-lookup"><span data-stu-id="bee5a-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="bee5a-165">嘗試 hello 儀表板的 toorefresh hello 認證</span><span class="sxs-lookup"><span data-stu-id="bee5a-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="bee5a-166">502 錯誤的閘道</span><span class="sxs-lookup"><span data-stu-id="bee5a-166">502 Bad Gateway</span></span>
<span data-ttu-id="bee5a-167">這通常是傳回太多資料的分析查詢所導致。</span><span class="sxs-lookup"><span data-stu-id="bee5a-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="bee5a-168">您應該嘗試使用較小的時間範圍或使用 hello[前](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago)或[startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek)僅限函式[專案](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator)hello 您需要的欄位。</span><span class="sxs-lookup"><span data-stu-id="bee5a-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="bee5a-169">如果降低 hello 來自 hello 分析查詢的資料集不符合您需求您應該考慮使用 hello [API](https://dev.applicationinsights.io/documentation/overview) toopull 較大的資料集。</span><span class="sxs-lookup"><span data-stu-id="bee5a-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="bee5a-170">以下是如何 tooconvert hello M 查詢匯出 toouse hello API 上的指示。</span><span class="sxs-lookup"><span data-stu-id="bee5a-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="bee5a-171">建立 [API 金鑰](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="bee5a-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="bee5a-172">更新 hello Power BI 的 M 指令碼來取代分析從匯出的 hello ARM AI api 的 URL （請參閱下面的範例）</span><span class="sxs-lookup"><span data-stu-id="bee5a-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="bee5a-173">將 **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="bee5a-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="bee5a-174">取代為 **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="bee5a-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="bee5a-175">最後，更新認證 toobasic，並使用您的 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="bee5a-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="bee5a-176">**現有的指令碼**</span><span class="sxs-lookup"><span data-stu-id="bee5a-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="bee5a-177">**更新的指令碼**</span><span class="sxs-lookup"><span data-stu-id="bee5a-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="bee5a-178">關於取樣</span><span class="sxs-lookup"><span data-stu-id="bee5a-178">About sampling</span></span>
<span data-ttu-id="bee5a-179">如果您的應用程式傳送大量資料，hello 調整取樣功能可能會運作，並傳送您遙測的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="bee5a-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="bee5a-180">hello 也是如此，如果您已經手動設定取樣 hello SDK 或擷取。</span><span class="sxs-lookup"><span data-stu-id="bee5a-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="bee5a-181">深入了解取樣。</span><span class="sxs-lookup"><span data-stu-id="bee5a-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="bee5a-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bee5a-182">Next steps</span></span>
* [<span data-ttu-id="bee5a-183">Power BI - 了解</span><span class="sxs-lookup"><span data-stu-id="bee5a-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="bee5a-184">Analytics 教學課程</span><span class="sxs-lookup"><span data-stu-id="bee5a-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

