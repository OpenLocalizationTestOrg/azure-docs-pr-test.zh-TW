---
title: "將 Log Analytics 資料匯出至 Power BI | Microsoft Docs"
description: "Power BI 是 Microsoft 的雲端架構商務分析服務，能提供豐富的視覺效果和不同資料集的分析報告。  Log Analytics 可以持續將資料從 OMS 儲存機制匯出到 Power BI，讓您可以利用其視覺效果和分析工具。  本文說明如何在 Log Analytics 中設定查詢，自動定期匯出至 Power BI。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 98befb16d27387e8f65a27771a2a32c264119d74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="export-log-analytics-data-to-power-bi"></a><span data-ttu-id="609df-105">將 Log Analytics 資料匯出至 Power BI</span><span class="sxs-lookup"><span data-stu-id="609df-105">Export Log Analytics data to Power BI</span></span>

>[!NOTE]
> <span data-ttu-id="609df-106">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則將 Log Analytics 資料匯出至 Power BI 的程序就無法再運作。</span><span class="sxs-lookup"><span data-stu-id="609df-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data to Power BI will no longer work.</span></span>  <span data-ttu-id="609df-107">您在升級之前建立的任何現有排程將會變成停用。</span><span class="sxs-lookup"><span data-stu-id="609df-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="609df-108">升級之後，Azure Log Analytics 會使用與 Application Insights 相同的平台，您使用如同[將 Application Insights 查詢匯出至 Power BI 的程序](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)的相同程序，將 Log Analytics 查詢匯出至 Power BI。</span><span class="sxs-lookup"><span data-stu-id="609df-108">After upgrade, Azure Log Analytics uses the same platform as Application Insights, and you use the same process to export Log Analytics queries to Power BI as [the process to export Application Insights queries to Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="609df-109">您可以如該文章所述使用分析主控台，或者您可以選取記錄搜尋入口網站中畫面頂端的 [Power BI] 按鈕，來匯出查詢。</span><span class="sxs-lookup"><span data-stu-id="609df-109">You can either export the query using the Analytics console as described in that article, or you can select the **Power BI** button at the top of the screen in the Log Search portal.</span></span>



<span data-ttu-id="609df-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) 是 Microsoft 的雲端架構商務分析服務，能提供豐富的視覺效果和不同資料集的分析報告。</span><span class="sxs-lookup"><span data-stu-id="609df-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="609df-111">Log Analytics 可以自動將資料從 OMS 儲存機制匯出到 Power BI，讓您可以利用其視覺效果和分析工具。</span><span class="sxs-lookup"><span data-stu-id="609df-111">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="609df-112">當您使用 Log Analytics 設定 Power BI 時，會建立記錄查詢，以將結果匯出至 Power BI 中的對應資料集。</span><span class="sxs-lookup"><span data-stu-id="609df-112">When you configure Power BI with Log Analytics, you create log queries that export their results to corresponding datasets in Power BI.</span></span>  <span data-ttu-id="609df-113">查詢和匯出會繼續自動依您定義的排程執行，讓資料集與 Log Analytics 收集的最新資料保持一致。</span><span class="sxs-lookup"><span data-stu-id="609df-113">The query and export continues to automatically run on a schedule that you define to keep the dataset up to date with the latest data collected by Log Analytics.</span></span>

![Log Analytics 到 Power BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="609df-115">Power BI 排程</span><span class="sxs-lookup"><span data-stu-id="609df-115">Power BI Schedules</span></span>
<span data-ttu-id="609df-116">「Power BI 排程」  包含將一組資料從 OMS 儲存機制匯出至 Power BI 中對應資料集的記錄搜尋，還有定義這項搜尋執行頻率的排程，以維持資料集為最新狀態。</span><span class="sxs-lookup"><span data-stu-id="609df-116">A *Power BI Schedule* includes a log search that exports a set of data from the OMS repository to a corresponding dataset in Power BI and a schedule that defines how often this search is run to keep the dataset current.</span></span>

<span data-ttu-id="609df-117">資料集中的欄位會符合記錄搜尋所傳回記錄的屬性。</span><span class="sxs-lookup"><span data-stu-id="609df-117">The fields in the dataset will match the properties of the records returned by the log search.</span></span>  <span data-ttu-id="609df-118">如果搜尋傳回不同類型的記錄，則資料集將包含來自每個包含之記錄類型的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="609df-118">If the search returns records of different types then the dataset will include all of the properties from each of the included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="609df-119">最佳做法是使用會傳回原始資料的記錄搜尋查詢，而不要使用命令執行任何彙總，例如 [量值](log-analytics-search-reference.md#measure)。</span><span class="sxs-lookup"><span data-stu-id="609df-119">It is a best practice to use a log search query that returns raw data as opposed to performing any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="609df-120">您可以在 Power BI 中從原始資料執行任何彙總與計算。</span><span class="sxs-lookup"><span data-stu-id="609df-120">You can perform any aggregation and calculations in Power BI from the raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-to-power-bi"></a><span data-ttu-id="609df-121">將 OMS 工作區連接到 Power BI</span><span class="sxs-lookup"><span data-stu-id="609df-121">Connecting OMS workspace to Power BI</span></span>
<span data-ttu-id="609df-122">您必須使用下列程序將 OMS 工作區連接到 Power BI 帳戶，才能從 Log Analytics 匯出至 Power BI。</span><span class="sxs-lookup"><span data-stu-id="609df-122">Before you can export from Log Analytics to Power BI, you must connect your OMS workspace to your Power BI account using the following procedure.</span></span>  

1. <span data-ttu-id="609df-123">在 OMS 主控台中，按一下 [設定]  圖格。</span><span class="sxs-lookup"><span data-stu-id="609df-123">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="609df-124">選取 [帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="609df-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="609df-125">在 [工作區資訊] 區段中，按一下 [連接到 Power BI 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="609df-125">In the **Workspace Information** section click **Connect to Power BI Account**.</span></span>
4. <span data-ttu-id="609df-126">輸入 Power BI 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="609df-126">Enter the credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="609df-127">建立 Power BI 排程</span><span class="sxs-lookup"><span data-stu-id="609df-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="609df-128">使用下列程序為每個資料集建立 Power BI 排程。</span><span class="sxs-lookup"><span data-stu-id="609df-128">Create a Power BI Schedule for each dataset using the following procedure.</span></span>

1. <span data-ttu-id="609df-129">在 OMS 主控台中，按一下 [記錄檔搜尋]  圖格。</span><span class="sxs-lookup"><span data-stu-id="609df-129">In the OMS console click the **Log Search** tile.</span></span>
2. <span data-ttu-id="609df-130">輸入新的查詢或選取已儲存的搜尋，傳回您想要匯出至 **Power BI**的資料。</span><span class="sxs-lookup"><span data-stu-id="609df-130">Type in a new query or select a saved search that returns the data that you want to export to **Power BI**.</span></span>  
3. <span data-ttu-id="609df-131">按一下頁面頂端的 [Power BI] 按鈕，開啟 [Power BI] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="609df-131">Click the **Power BI** button at the top of the page to open the **Power BI** dialog.</span></span>
4. <span data-ttu-id="609df-132">提供下列資料表中的資訊，並按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="609df-132">Provide the information in the following table and click **Save**.</span></span>

| <span data-ttu-id="609df-133">屬性</span><span class="sxs-lookup"><span data-stu-id="609df-133">Property</span></span> | <span data-ttu-id="609df-134">說明</span><span class="sxs-lookup"><span data-stu-id="609df-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="609df-135">名稱</span><span class="sxs-lookup"><span data-stu-id="609df-135">Name</span></span> |<span data-ttu-id="609df-136">當您檢視 Power BI 排程清單時，用來識別排程的名稱。</span><span class="sxs-lookup"><span data-stu-id="609df-136">Name to identify the schedule when you view the list of Power BI schedules.</span></span> |
| <span data-ttu-id="609df-137">已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="609df-137">Saved Search</span></span> |<span data-ttu-id="609df-138">要執行的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="609df-138">The log search to run.</span></span>  <span data-ttu-id="609df-139">您可以選取目前的查詢，或從下拉式清單方塊中選取現有的已儲存搜尋。</span><span class="sxs-lookup"><span data-stu-id="609df-139">You can either select the current query or select an existing saved search from the dropdown box.</span></span> |
| <span data-ttu-id="609df-140">排程</span><span class="sxs-lookup"><span data-stu-id="609df-140">Schedule</span></span> |<span data-ttu-id="609df-141">執行已儲存的搜尋，並匯出至 Power BI 資料集的頻率。</span><span class="sxs-lookup"><span data-stu-id="609df-141">How often to run the saved search and export to the Power BI dataset.</span></span>  <span data-ttu-id="609df-142">值必須介於 15 分鐘到 24 小時之間。</span><span class="sxs-lookup"><span data-stu-id="609df-142">The value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="609df-143">資料集名稱</span><span class="sxs-lookup"><span data-stu-id="609df-143">Dataset Name</span></span> |<span data-ttu-id="609df-144">Power BI 中的資料集名稱。</span><span class="sxs-lookup"><span data-stu-id="609df-144">The name of the dataset in Power BI.</span></span>  <span data-ttu-id="609df-145">如果不存在便會建立，如果存在則會更新。</span><span class="sxs-lookup"><span data-stu-id="609df-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="609df-146">檢視和移除 Power BI 排程</span><span class="sxs-lookup"><span data-stu-id="609df-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="609df-147">使用下列程序檢視現有 Power BI 排程的清單。</span><span class="sxs-lookup"><span data-stu-id="609df-147">View the list of existing Power BI Schedules with the following procedure.</span></span>

1. <span data-ttu-id="609df-148">在 OMS 主控台中，按一下 [設定]  圖格。</span><span class="sxs-lookup"><span data-stu-id="609df-148">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="609df-149">選取 [Power BI] 。</span><span class="sxs-lookup"><span data-stu-id="609df-149">Select **Power BI**.</span></span>

<span data-ttu-id="609df-150">除了排程的詳細資訊之外，還會顯示過去一週執行排程的次數，以及上次同步處理的狀態。</span><span class="sxs-lookup"><span data-stu-id="609df-150">In addition to the details of the schedule, the number of times that the schedule has run in the past week and the status of the last sync are displayed.</span></span>  <span data-ttu-id="609df-151">如果在同步處理時發生錯誤，您可以按一下連結以執行記錄的記錄搜尋，以及錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="609df-151">If the sync encountered errors, you can click the link to run a log search for records with details of the error.</span></span>

<span data-ttu-id="609df-152">您可以按一下 [移除資料行] 中的 **X** 來移除排程。</span><span class="sxs-lookup"><span data-stu-id="609df-152">You can remove a schedule by clicking on the **X** in the **Remove column**.</span></span>  <span data-ttu-id="609df-153">您可以選取 [關閉] 來停用排程。</span><span class="sxs-lookup"><span data-stu-id="609df-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="609df-154">若要修改排程，您必須移除它，然後再以新的設定重新建立。</span><span class="sxs-lookup"><span data-stu-id="609df-154">To modify a schedule you must remove it and recreate it with the new settings.</span></span>

![Power BI 排程](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="609df-156">範例逐步解說</span><span class="sxs-lookup"><span data-stu-id="609df-156">Sample walkthrough</span></span>
<span data-ttu-id="609df-157">下一節逐步解說建立 Power BI 排程，並使用其資料集來建立簡單報表的範例。</span><span class="sxs-lookup"><span data-stu-id="609df-157">The following section walks through an example of creating a Power BI Schedule and using its dataset to create a simple report.</span></span>  <span data-ttu-id="609df-158">在此範例中，一組電腦的所有效能資料都匯出至 Power BI，然後會建立折線圖以顯示處理器使用率。</span><span class="sxs-lookup"><span data-stu-id="609df-158">In this example, all performance data for a set of computers is exported to Power BI and then a line graph is created to display processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="609df-159">建立記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="609df-159">Create log search</span></span>
<span data-ttu-id="609df-160">首先我們會建立記錄搜尋，尋找我們想要傳送至資料集的資料。</span><span class="sxs-lookup"><span data-stu-id="609df-160">We start by creating a log search for the data that we want to send to the dataset.</span></span>  <span data-ttu-id="609df-161">在此範例中，我們將使用一個查詢，傳回名稱開頭為 *srv*之電腦的所有效能資料。</span><span class="sxs-lookup"><span data-stu-id="609df-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Power BI 排程](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="609df-163">建立 Power BI 搜尋</span><span class="sxs-lookup"><span data-stu-id="609df-163">Create Power BI Search</span></span>
<span data-ttu-id="609df-164">我們按一下 [Power BI]  按鈕以開啟 [Power BI] 對話方塊，並提供必要的資訊。</span><span class="sxs-lookup"><span data-stu-id="609df-164">We click the **Power BI** button to open the Power BI dialog and provide the required information.</span></span>  <span data-ttu-id="609df-165">我們想要每小時執行一次此搜尋，並建立名為 *Contoso Perf*的資料集。</span><span class="sxs-lookup"><span data-stu-id="609df-165">We want this search to run once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="609df-166">由於我們已經開啟會建立我們所要資料的搜尋，因此我們針對 [已儲存的搜尋] 保留預設值「使用目前的搜尋查詢」。</span><span class="sxs-lookup"><span data-stu-id="609df-166">Since we already have the search open that creates the data we want, we keep the default of *Use current search query* for **Saved Search**.</span></span>

![Power BI 搜尋](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="609df-168">驗證 Power BI 搜尋</span><span class="sxs-lookup"><span data-stu-id="609df-168">Verify Power BI Search</span></span>
<span data-ttu-id="609df-169">為了驗證我們已正確建立排程，我們會在 OMS 儀表板的 [設定]  圖格中檢視 Power BI 搜尋的清單。</span><span class="sxs-lookup"><span data-stu-id="609df-169">To verify that we created the schedule correctly, we view the list of Power BI Searches under the **Settings** tile in the OMS dashboard.</span></span>  <span data-ttu-id="609df-170">我們稍候幾分鐘的時間，並重新整理此檢視，直到它報告已執行同步處理。</span><span class="sxs-lookup"><span data-stu-id="609df-170">We wait several minutes and refresh this view until it reports that the sync has been run.</span></span>

![Power BI 搜尋](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-the-dataset-in-power-bi"></a><span data-ttu-id="609df-172">在 Power BI 中驗證資料集</span><span class="sxs-lookup"><span data-stu-id="609df-172">Verify the dataset in Power BI</span></span>
<span data-ttu-id="609df-173">我們在 [powerbi.microsoft.com](http://powerbi.microsoft.com/) 登入我們的帳戶，並捲動至左窗格底部的 [資料集]。</span><span class="sxs-lookup"><span data-stu-id="609df-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll to **Datasets** at the bottom of the left pane.</span></span>  <span data-ttu-id="609df-174">我們可以看到已列出 *Contoso Perf* 資料集，表示我們的匯出已順利執行。</span><span class="sxs-lookup"><span data-stu-id="609df-174">We can see that the *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Power BI 資料集](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="609df-176">根據資料集建立報表</span><span class="sxs-lookup"><span data-stu-id="609df-176">Create report based on dataset</span></span>
<span data-ttu-id="609df-177">我們選取 **Contoso Perf** 資料集，然後按一下右邉 [欄位] 窗格中的 [結果]，檢視屬於此資料集的欄位。</span><span class="sxs-lookup"><span data-stu-id="609df-177">We select the **Contoso Perf** dataset and then click on **Results** in the **Fields** pane on the right to view the fields that are part of this dataset.</span></span>  <span data-ttu-id="609df-178">為了建立折線圖，顯示每一部電腦的處理器使用率，我們執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="609df-178">To create a line graph showing processor utilization for each computer, we perform the following actions.</span></span>

1. <span data-ttu-id="609df-179">選取折線圖視覺效果。</span><span class="sxs-lookup"><span data-stu-id="609df-179">Select the Line chart visualization.</span></span>
2. <span data-ttu-id="609df-180">將 **ObjectName** 拖放到 [報表層級篩選] 並勾選 [處理器]。</span><span class="sxs-lookup"><span data-stu-id="609df-180">Drag **ObjectName** to **Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="609df-181">將 **CounterName** 拖放到 [報表層級篩選] 並勾選 [% 處理器時間]。</span><span class="sxs-lookup"><span data-stu-id="609df-181">Drag **CounterName** to **Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="609df-182">將 **CounterValue** 拖放到 [值]。</span><span class="sxs-lookup"><span data-stu-id="609df-182">Drag **CounterValue** to **Values**.</span></span>
5. <span data-ttu-id="609df-183">將 **Computer** 拖放到 [圖例]。</span><span class="sxs-lookup"><span data-stu-id="609df-183">Drag **Computer** to **Legend**.</span></span>
6. <span data-ttu-id="609df-184">將 **TimeGenerated** 拖放到 [軸]。</span><span class="sxs-lookup"><span data-stu-id="609df-184">Drag **TimeGenerated** to **Axis**.</span></span>

<span data-ttu-id="609df-185">我們可以看到會顯示產生的折線圖，以及來自我們資料集的資料。</span><span class="sxs-lookup"><span data-stu-id="609df-185">We can see that the resulting line graph is displayed with the data from our dataset.</span></span>

![Power BI 折線圖](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-the-report"></a><span data-ttu-id="609df-187">儲存報表</span><span class="sxs-lookup"><span data-stu-id="609df-187">Save the report</span></span>
<span data-ttu-id="609df-188">我們在畫面頂端按一下 [儲存] 按鈕來儲存報表，並驗證它現在會列在左窗格中的 [報表] 區段中。</span><span class="sxs-lookup"><span data-stu-id="609df-188">We save the report by clicking on the Save button at the top of the screen and validate that it is now listed in the Reports section in the left pane.</span></span>

![Power BI 報表](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="609df-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="609df-190">Next steps</span></span>
* <span data-ttu-id="609df-191">深入了解 [記錄檔搜尋](log-analytics-log-searches.md) ，建置可以匯出至 Power BI 的查詢。</span><span class="sxs-lookup"><span data-stu-id="609df-191">Learn about [log searches](log-analytics-log-searches.md) to build queries that can be exported to Power BI.</span></span>
* <span data-ttu-id="609df-192">深入了解 [Power BI](http://powerbi.microsoft.com)，建置以 Log Analytics 匯出為基礎的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="609df-192">Learn more about [Power BI](http://powerbi.microsoft.com) to build visualizations based on Log Analytics exports.</span></span>
