---
title: "從 Application Insights 匯出至 Power BI | Microsoft Docs"
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
ms.openlocfilehash: 350a65b1c6432baf258e014c9e63133d2b29e34f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="2481f-103">從 Application Insights 提供 Power BI</span><span class="sxs-lookup"><span data-stu-id="2481f-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="2481f-104">[Power BI](http://www.powerbi.com/) 是一套商務分析工具，可協助您分析資料及分享見解。</span><span class="sxs-lookup"><span data-stu-id="2481f-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="2481f-105">每個裝置上都提供豐富的儀表板。</span><span class="sxs-lookup"><span data-stu-id="2481f-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="2481f-106">您可以結合許多來源的資料，包含來自 [Azure Application Insights](app-insights-overview.md) 的「分析」查詢。</span><span class="sxs-lookup"><span data-stu-id="2481f-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="2481f-107">有三種建議方法可將 Application Insights 資料匯出至 Power BI。</span><span class="sxs-lookup"><span data-stu-id="2481f-107">There are three recommended methods of exporting Application Insights data to Power BI.</span></span> <span data-ttu-id="2481f-108">您可以單獨或一起使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="2481f-108">You can use them separately or together.</span></span>

* <span data-ttu-id="2481f-109">[**Power BI 配接器**](#power-pi-adapter) - 從您的應用程式設定完整的遙測儀表板。</span><span class="sxs-lookup"><span data-stu-id="2481f-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="2481f-110">儀表板中已預先定義一組圖表，但您可以從任何其他來源新增您自己的查詢。</span><span class="sxs-lookup"><span data-stu-id="2481f-110">The set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="2481f-111">[**匯出 Analytics 查詢**](#export-analytics-queries) - 使用 Analytics 撰寫任何您想要的查詢，並將它匯出至 Power BI。</span><span class="sxs-lookup"><span data-stu-id="2481f-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it to Power BI.</span></span> <span data-ttu-id="2481f-112">您可以將此查詢和任何其他資料一起放在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="2481f-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="2481f-113">[**連續匯出和串流分析**](app-insights-export-stream-analytics.md) - 這牽涉到更多設定工作。</span><span class="sxs-lookup"><span data-stu-id="2481f-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work to set up.</span></span> <span data-ttu-id="2481f-114">如果您想要長期保留資料，此方法很有用。</span><span class="sxs-lookup"><span data-stu-id="2481f-114">It is useful if you want to keep your data for long periods.</span></span> <span data-ttu-id="2481f-115">否則，建議您使用其他方法。</span><span class="sxs-lookup"><span data-stu-id="2481f-115">Otherwise, the other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="2481f-116">Power BI 配接器</span><span class="sxs-lookup"><span data-stu-id="2481f-116">Power BI adapter</span></span>
<span data-ttu-id="2481f-117">這個方法會為您建立完整的遙測儀表板。</span><span class="sxs-lookup"><span data-stu-id="2481f-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="2481f-118">儀表板中已預先定義初始資料集，但您也可以在資料集中新增更多資料。</span><span class="sxs-lookup"><span data-stu-id="2481f-118">The initial data set is predefined, but you can add more data to it.</span></span>

### <a name="get-the-adapter"></a><span data-ttu-id="2481f-119">取得配接器</span><span class="sxs-lookup"><span data-stu-id="2481f-119">Get the adapter</span></span>
1. <span data-ttu-id="2481f-120">登入 [Power BI](https://app.powerbi.com/)。</span><span class="sxs-lookup"><span data-stu-id="2481f-120">Sign in to [Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="2481f-121">依序開啟 [取得資料]、[服務] 和 [Application Insights]</span><span class="sxs-lookup"><span data-stu-id="2481f-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![取自 Application Insights 資料來源](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="2481f-123">提供 Application Insights 資源的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2481f-123">Provide the details of your Application Insights resource.</span></span>
   
    ![取自 Application Insights 資料來源](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="2481f-125">等候一兩分鐘來匯入資料。</span><span class="sxs-lookup"><span data-stu-id="2481f-125">Wait a minute or two for the data to be imported.</span></span>
   
    ![Power BI 配接器](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="2481f-127">您可以編輯儀表板，將 Application Insights 圖表與其他來源的圖表以及 Analytics 查詢相結合。</span><span class="sxs-lookup"><span data-stu-id="2481f-127">You can edit the dashboard, combining the Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="2481f-128">還有一個視覺效果資源庫，您可以從中取得更多圖表，且每個圖表都有您可以設定的參數。</span><span class="sxs-lookup"><span data-stu-id="2481f-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="2481f-129">初始匯入之後，儀表板和報告會持續每日更新。</span><span class="sxs-lookup"><span data-stu-id="2481f-129">After the initial import, the dashboard and the reports continue to update daily.</span></span> <span data-ttu-id="2481f-130">您可以控制資料集上的重新整理排程。</span><span class="sxs-lookup"><span data-stu-id="2481f-130">You can control the refresh schedule on the dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="2481f-131">匯出 Analytics 查詢</span><span class="sxs-lookup"><span data-stu-id="2481f-131">Export Analytics queries</span></span>
<span data-ttu-id="2481f-132">此途徑可讓您撰寫您喜歡的任何 Analytics 查詢，然後將其匯出至 Power BI 儀表板 </span><span class="sxs-lookup"><span data-stu-id="2481f-132">This route allows you to write any Analytics query you like, and then export that to a Power BI dashboard.</span></span> <span data-ttu-id="2481f-133">(您可以新增至配接器所建立的儀表板)。</span><span class="sxs-lookup"><span data-stu-id="2481f-133">(You can add to the dashboard created by the adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="2481f-134">一次︰安裝 Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="2481f-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="2481f-135">若要匯入您的 Application Insights 查詢，您可以使用桌面版本的 Power BI。</span><span class="sxs-lookup"><span data-stu-id="2481f-135">To import your Application Insights query, you use the desktop version of Power BI.</span></span> <span data-ttu-id="2481f-136">但是，您接著可以將它發佈至 Web 或您的 Power BI 雲端工作區。</span><span class="sxs-lookup"><span data-stu-id="2481f-136">But then you can publish it to the web or to your Power BI cloud workspace.</span></span> 

<span data-ttu-id="2481f-137">安裝 [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/)。</span><span class="sxs-lookup"><span data-stu-id="2481f-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="2481f-138">匯出 Analytics 查詢</span><span class="sxs-lookup"><span data-stu-id="2481f-138">Export an Analytics query</span></span>
1. <span data-ttu-id="2481f-139">[開啟 Analytics 並撰寫查詢](app-insights-analytics-tour.md)。</span><span class="sxs-lookup"><span data-stu-id="2481f-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="2481f-140">測試並精簡查詢，直到您滿意結果。</span><span class="sxs-lookup"><span data-stu-id="2481f-140">Test and refine the query until you're happy with the results.</span></span>

   <span data-ttu-id="2481f-141">**請先確定查詢在「分析」中正確執行，再將它匯出。**</span><span class="sxs-lookup"><span data-stu-id="2481f-141">**Make sure that the query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="2481f-142">在 [匯出] 功能表上，選擇 [Power BI (M)]。</span><span class="sxs-lookup"><span data-stu-id="2481f-142">On the **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="2481f-143">儲存文字檔案。</span><span class="sxs-lookup"><span data-stu-id="2481f-143">Save the text file.</span></span>
   
    ![匯出 Power BI 查詢](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="2481f-145">在 Power BI Desktop 中選取 [取得資料]、[空白查詢]，然後在查詢編輯器中，於 [檢視] 底下選取 [進階查詢編輯器]。</span><span class="sxs-lookup"><span data-stu-id="2481f-145">In Power BI Desktop select **Get Data, Blank Query** and then in the query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="2481f-146">將匯出的 M 語言指令碼貼到進階查詢編輯器。</span><span class="sxs-lookup"><span data-stu-id="2481f-146">Paste the exported M Language script into the Advanced Query Editor.</span></span>

    ![進階查詢編輯器](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="2481f-148">您可能必須提供認證，才能讓 Power BI 得以存取 Azure。</span><span class="sxs-lookup"><span data-stu-id="2481f-148">You might have to provide credentials to allow Power BI to access Azure.</span></span> <span data-ttu-id="2481f-149">使用「組織帳戶」來以 Microsoft 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="2481f-149">Use 'organizational account' to sign in with your Microsoft account.</span></span>
   
    ![提供 Azure 認證，讓 Power BI 能夠執行您的 Application Insights 查詢](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="2481f-151">(如果您需要驗證認證，請使用「查詢編輯器」中的 [資料來源設定] 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="2481f-151">(If you need to verify the credentials, use the Data Source Settings menu command in the Query Editor.</span></span> <span data-ttu-id="2481f-152">指定用於 Azure 的認證時請小心，此認證有可能與您用於 Power BI 的認證不同)。</span><span class="sxs-lookup"><span data-stu-id="2481f-152">Take care to specify the credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="2481f-153">選擇查詢的視覺效果，然後選取 x 軸、y 軸與分割維度的欄位。</span><span class="sxs-lookup"><span data-stu-id="2481f-153">Choose a visualization for your query and select the fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![選取視覺效果](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="2481f-155">將報表發佈至 Power BI 雲端工作區。</span><span class="sxs-lookup"><span data-stu-id="2481f-155">Publish your report to your Power BI cloud workspace.</span></span> <span data-ttu-id="2481f-156">您可以從該處將同步版本內嵌至其他網頁。</span><span class="sxs-lookup"><span data-stu-id="2481f-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![選取視覺效果](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="2481f-158">不時手動重新整理報表，或在選項頁面上設定排定的重新整理。</span><span class="sxs-lookup"><span data-stu-id="2481f-158">Refresh the report manually at intervals, or set up a scheduled refresh on the options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2481f-159">疑難排解</span><span class="sxs-lookup"><span data-stu-id="2481f-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="2481f-160">401 或 403 未經授權</span><span class="sxs-lookup"><span data-stu-id="2481f-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="2481f-161">如果您的重新整理權杖尚未更新，可能會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="2481f-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="2481f-162">請嘗試下列步驟以確保您仍然具有存取權。</span><span class="sxs-lookup"><span data-stu-id="2481f-162">Try these steps to ensure you still have access.</span></span> <span data-ttu-id="2481f-163">如果您沒有存取權且重新整理認證沒有作用，請開啟支援票證。</span><span class="sxs-lookup"><span data-stu-id="2481f-163">If you do have access and refershing the credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="2481f-164">登入 Azure 入口網站，並確定您可以存取資源</span><span class="sxs-lookup"><span data-stu-id="2481f-164">Log into the Azure Portal and make sure you can access the resource</span></span>
2. <span data-ttu-id="2481f-165">嘗試重新整理儀表板的認證</span><span class="sxs-lookup"><span data-stu-id="2481f-165">Try to refresh the credentials for the Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="2481f-166">502 錯誤的閘道</span><span class="sxs-lookup"><span data-stu-id="2481f-166">502 Bad Gateway</span></span>
<span data-ttu-id="2481f-167">這通常是傳回太多資料的分析查詢所導致。</span><span class="sxs-lookup"><span data-stu-id="2481f-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="2481f-168">您應該嘗試使用較小的時間範圍，或使用 [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) 或 [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek)僅限函式[專案](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator)需要的欄位。</span><span class="sxs-lookup"><span data-stu-id="2481f-168">You should try using a smaller time range or by using the [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) the fields you need.</span></span>

<span data-ttu-id="2481f-169">如果減少來自分析查詢的資料集不符合您的需求，您應該考慮使用 [API](https://dev.applicationinsights.io/documentation/overview) 以提取較大的資料集。</span><span class="sxs-lookup"><span data-stu-id="2481f-169">If reducing the dataset coming from the Analytics query doesn't meet your requirements you should consider using the [API](https://dev.applicationinsights.io/documentation/overview) to pull a larger dataset.</span></span> <span data-ttu-id="2481f-170">以下是如何將 M-Query 匯出轉換為使用 API 的指示。</span><span class="sxs-lookup"><span data-stu-id="2481f-170">Here are instructions on how to convert the M-Query export to use the API.</span></span>

1. <span data-ttu-id="2481f-171">建立 [API 金鑰](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="2481f-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="2481f-172">更新您從分析匯出的 Power BI M 指令碼，方法是將 ARM URL 取代為 AI API (請參閱以下範例)</span><span class="sxs-lookup"><span data-stu-id="2481f-172">Update the Power BI M script that you exported from Analytics by replacing the ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="2481f-173">將 **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="2481f-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="2481f-174">取代為 **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="2481f-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="2481f-175">最後，將認證更新為基本，並且使用您的 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="2481f-175">Finally, update credentials to basic, and use your API Key</span></span>
  

<span data-ttu-id="2481f-176">**現有的指令碼**</span><span class="sxs-lookup"><span data-stu-id="2481f-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="2481f-177">**更新的指令碼**</span><span class="sxs-lookup"><span data-stu-id="2481f-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="2481f-178">關於取樣</span><span class="sxs-lookup"><span data-stu-id="2481f-178">About sampling</span></span>
<span data-ttu-id="2481f-179">如果應用程式會傳送大量資料，調適性取樣功能或許會運作，並只傳送一定百分比的遙測。</span><span class="sxs-lookup"><span data-stu-id="2481f-179">If your application sends a lot of data, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="2481f-180">如果您已經在 SDK 中或在擷取上手動設定取樣，也是如此。</span><span class="sxs-lookup"><span data-stu-id="2481f-180">The same is true if you have manually set sampling either in the SDK or on ingestion.</span></span> [<span data-ttu-id="2481f-181">深入了解取樣。</span><span class="sxs-lookup"><span data-stu-id="2481f-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="2481f-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2481f-182">Next steps</span></span>
* [<span data-ttu-id="2481f-183">Power BI - 了解</span><span class="sxs-lookup"><span data-stu-id="2481f-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="2481f-184">Analytics 教學課程</span><span class="sxs-lookup"><span data-stu-id="2481f-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

