---
title: "aaaExport 記錄分析資料 tooPower BI |Microsoft 文件"
description: "Power BI 是 Microsoft 的雲端架構商務分析服務，能提供豐富的視覺效果和不同資料集的分析報告。  記錄分析可以持續將資料匯出 hello OMS 儲存機制到 Power BI，您可以利用其視覺效果與分析工具。  本文說明如何 tooconfigure 查詢中的自動匯出 tooPower BI 定期記錄分析。"
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
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a><span data-ttu-id="c8908-105">匯出記錄分析資料 tooPower BI</span><span class="sxs-lookup"><span data-stu-id="c8908-105">Export Log Analytics data tooPower BI</span></span>

>[!NOTE]
> <span data-ttu-id="c8908-106">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則匯出記錄分析資料 tooPower BI 此程序將無法再運作。</span><span class="sxs-lookup"><span data-stu-id="c8908-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data tooPower BI will no longer work.</span></span>  <span data-ttu-id="c8908-107">您在升級之前建立的任何現有排程將會變成停用。</span><span class="sxs-lookup"><span data-stu-id="c8908-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="c8908-108">升級之後，Azure 記錄分析會使用 hello Application Insights 為相同的平台，而且您使用相同的處理序 tooexport 記錄分析查詢 tooPower 為 BI hello [hello 程序 tooexport Application Insights 查詢 tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)。</span><span class="sxs-lookup"><span data-stu-id="c8908-108">After upgrade, Azure Log Analytics uses hello same platform as Application Insights, and you use hello same process tooexport Log Analytics queries tooPower BI as [hello process tooexport Application Insights queries tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="c8908-109">您可以將匯出 hello 查詢使用 hello 分析主控台，如下所示該發行項，或者您可以選取 hello **Power BI** hello 畫面頂端的 hello hello 記錄搜尋入口網站中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c8908-109">You can either export hello query using hello Analytics console as described in that article, or you can select hello **Power BI** button at hello top of hello screen in hello Log Search portal.</span></span>



<span data-ttu-id="c8908-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) 是 Microsoft 的雲端架構商務分析服務，能提供豐富的視覺效果和不同資料集的分析報告。</span><span class="sxs-lookup"><span data-stu-id="c8908-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="c8908-111">記錄分析可以自動將資料匯出 hello OMS 儲存機制到 Power BI，您可以利用其視覺效果與分析工具。</span><span class="sxs-lookup"><span data-stu-id="c8908-111">Log Analytics can automatically export data from hello OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="c8908-112">當您設定 Power BI 與記錄分析時，您會建立匯出結果 toocorresponding 資料集在 Power BI 中的記錄查詢。</span><span class="sxs-lookup"><span data-stu-id="c8908-112">When you configure Power BI with Log Analytics, you create log queries that export their results toocorresponding datasets in Power BI.</span></span>  <span data-ttu-id="c8908-113">hello 查詢和匯出會繼續 tooautomatically hello 最新記錄分析所收集的資料定義總 toodate tookeep hello 資料集的排程執行。</span><span class="sxs-lookup"><span data-stu-id="c8908-113">hello query and export continues tooautomatically run on a schedule that you define tookeep hello dataset up toodate with hello latest data collected by Log Analytics.</span></span>

![記錄分析 tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="c8908-115">Power BI 排程</span><span class="sxs-lookup"><span data-stu-id="c8908-115">Power BI Schedules</span></span>
<span data-ttu-id="c8908-116">A *Power BI 排程*包含 hello OMS 儲存機制 tooa 對應中的資料集 Power BI 和排程，定義此搜尋會執行目前的 tookeep hello 資料集的頻率從匯出的資料集的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="c8908-116">A *Power BI Schedule* includes a log search that exports a set of data from hello OMS repository tooa corresponding dataset in Power BI and a schedule that defines how often this search is run tookeep hello dataset current.</span></span>

<span data-ttu-id="c8908-117">hello hello 資料集中的欄位會比對 hello 記錄 hello 記錄搜尋所傳回的 hello 的屬性。</span><span class="sxs-lookup"><span data-stu-id="c8908-117">hello fields in hello dataset will match hello properties of hello records returned by hello log search.</span></span>  <span data-ttu-id="c8908-118">如果 hello 搜尋傳回不同類型的記錄，則 hello 資料集將包含的所有記錄類型包含從每個 hello 的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="c8908-118">If hello search returns records of different types then hello dataset will include all of hello properties from each of hello included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="c8908-119">它是最佳的作法 toouse 傳回未經處理資料，但不要 tooperforming 為任何彙總，例如使用命令的記錄搜尋查詢[量值](log-analytics-search-reference.md#measure)。</span><span class="sxs-lookup"><span data-stu-id="c8908-119">It is a best practice toouse a log search query that returns raw data as opposed tooperforming any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="c8908-120">您可以在 Power BI 中執行任何彙總與計算，從 hello 未經處理資料。</span><span class="sxs-lookup"><span data-stu-id="c8908-120">You can perform any aggregation and calculations in Power BI from hello raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a><span data-ttu-id="c8908-121">連接的 OMS 工作區 tooPower BI</span><span class="sxs-lookup"><span data-stu-id="c8908-121">Connecting OMS workspace tooPower BI</span></span>
<span data-ttu-id="c8908-122">您可以從記錄分析 tooPower BI 匯出之前，您必須連接您的 OMS 工作區 tooyour Power BI 帳戶使用下列程序的 hello。</span><span class="sxs-lookup"><span data-stu-id="c8908-122">Before you can export from Log Analytics tooPower BI, you must connect your OMS workspace tooyour Power BI account using hello following procedure.</span></span>  

1. <span data-ttu-id="c8908-123">在 hello OMS 主控台中，按一下 hello**設定**磚。</span><span class="sxs-lookup"><span data-stu-id="c8908-123">In hello OMS console click hello **Settings** tile.</span></span>
2. <span data-ttu-id="c8908-124">選取 [帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="c8908-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="c8908-125">在 hello**工作區資訊**區段中，按一下**連接 tooPower BI 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="c8908-125">In hello **Workspace Information** section click **Connect tooPower BI Account**.</span></span>
4. <span data-ttu-id="c8908-126">輸入您的 Power BI 帳戶 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="c8908-126">Enter hello credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="c8908-127">建立 Power BI 排程</span><span class="sxs-lookup"><span data-stu-id="c8908-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="c8908-128">建立 Power BI 排程每個資料集使用下列程序的 hello。</span><span class="sxs-lookup"><span data-stu-id="c8908-128">Create a Power BI Schedule for each dataset using hello following procedure.</span></span>

1. <span data-ttu-id="c8908-129">在 hello OMS 主控台中，按一下 hello**記錄搜尋**磚。</span><span class="sxs-lookup"><span data-stu-id="c8908-129">In hello OMS console click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="c8908-130">在新的查詢中輸入或選取已儲存的搜尋傳回 hello 太想 tooexport 資料**Power BI**。</span><span class="sxs-lookup"><span data-stu-id="c8908-130">Type in a new query or select a saved search that returns hello data that you want tooexport too**Power BI**.</span></span>  
3. <span data-ttu-id="c8908-131">按一下 hello **Power BI**按鈕上方的 hello 頁面 tooopen hello hello **Power BI**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c8908-131">Click hello **Power BI** button at hello top of hello page tooopen hello **Power BI** dialog.</span></span>
4. <span data-ttu-id="c8908-132">提供在下列資料表，並按一下的 hello hello 資訊**儲存**。</span><span class="sxs-lookup"><span data-stu-id="c8908-132">Provide hello information in hello following table and click **Save**.</span></span>

| <span data-ttu-id="c8908-133">屬性</span><span class="sxs-lookup"><span data-stu-id="c8908-133">Property</span></span> | <span data-ttu-id="c8908-134">說明</span><span class="sxs-lookup"><span data-stu-id="c8908-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c8908-135">名稱</span><span class="sxs-lookup"><span data-stu-id="c8908-135">Name</span></span> |<span data-ttu-id="c8908-136">名稱 tooidentify hello 排定的時間檢視的 Power BI 排程 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="c8908-136">Name tooidentify hello schedule when you view hello list of Power BI schedules.</span></span> |
| <span data-ttu-id="c8908-137">已儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="c8908-137">Saved Search</span></span> |<span data-ttu-id="c8908-138">hello 記錄搜尋 toorun。</span><span class="sxs-lookup"><span data-stu-id="c8908-138">hello log search toorun.</span></span>  <span data-ttu-id="c8908-139">您可以選取 hello 目前的查詢，或從 hello 下拉式清單方塊中選取現有的儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="c8908-139">You can either select hello current query or select an existing saved search from hello dropdown box.</span></span> |
| <span data-ttu-id="c8908-140">排程</span><span class="sxs-lookup"><span data-stu-id="c8908-140">Schedule</span></span> |<span data-ttu-id="c8908-141">頻率 toorun hello 儲存搜尋及匯出 toohello Power BI 資料集。</span><span class="sxs-lookup"><span data-stu-id="c8908-141">How often toorun hello saved search and export toohello Power BI dataset.</span></span>  <span data-ttu-id="c8908-142">hello 值必須是 15 分鐘到 24 小時之間。</span><span class="sxs-lookup"><span data-stu-id="c8908-142">hello value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="c8908-143">資料集名稱</span><span class="sxs-lookup"><span data-stu-id="c8908-143">Dataset Name</span></span> |<span data-ttu-id="c8908-144">hello hello Power BI 中的資料集名稱。</span><span class="sxs-lookup"><span data-stu-id="c8908-144">hello name of hello dataset in Power BI.</span></span>  <span data-ttu-id="c8908-145">如果不存在便會建立，如果存在則會更新。</span><span class="sxs-lookup"><span data-stu-id="c8908-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="c8908-146">檢視和移除 Power BI 排程</span><span class="sxs-lookup"><span data-stu-id="c8908-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="c8908-147">檢視現有的 Power BI 排程，以下列程序的 hello 的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="c8908-147">View hello list of existing Power BI Schedules with hello following procedure.</span></span>

1. <span data-ttu-id="c8908-148">在 hello OMS 主控台中，按一下 hello**設定**磚。</span><span class="sxs-lookup"><span data-stu-id="c8908-148">In hello OMS console click hello **Settings** tile.</span></span>
2. <span data-ttu-id="c8908-149">選取 [Power BI] 。</span><span class="sxs-lookup"><span data-stu-id="c8908-149">Select **Power BI**.</span></span>

<span data-ttu-id="c8908-150">此外 toohello 詳細資料的 hello 排程、 過去一週執行 hello 的次數 hello 排程在 hello 和 hello hello 上次同步處理狀態會顯示。</span><span class="sxs-lookup"><span data-stu-id="c8908-150">In addition toohello details of hello schedule, hello number of times that hello schedule has run in hello past week and hello status of hello last sync are displayed.</span></span>  <span data-ttu-id="c8908-151">如果 hello 同步處理遇到錯誤，您可以按一下 hello 連結 toorun hello 錯誤的詳細資料與記錄的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="c8908-151">If hello sync encountered errors, you can click hello link toorun a log search for records with details of hello error.</span></span>

<span data-ttu-id="c8908-152">您可以在 hello 上的 移除排程**X**在 hello**移除資料行**。</span><span class="sxs-lookup"><span data-stu-id="c8908-152">You can remove a schedule by clicking on hello **X** in hello **Remove column**.</span></span>  <span data-ttu-id="c8908-153">您可以選取 [關閉] 來停用排程。</span><span class="sxs-lookup"><span data-stu-id="c8908-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="c8908-154">toomodify 排程必須移除並重新建立它的 hello 新設定。</span><span class="sxs-lookup"><span data-stu-id="c8908-154">toomodify a schedule you must remove it and recreate it with hello new settings.</span></span>

![Power BI 排程](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="c8908-156">範例逐步解說</span><span class="sxs-lookup"><span data-stu-id="c8908-156">Sample walkthrough</span></span>
<span data-ttu-id="c8908-157">hello 下一節逐步解說範例建立 Power BI 排程，並使用其資料集 toocreate 一份簡單報表。</span><span class="sxs-lookup"><span data-stu-id="c8908-157">hello following section walks through an example of creating a Power BI Schedule and using its dataset toocreate a simple report.</span></span>  <span data-ttu-id="c8908-158">在此範例中，一組電腦的所有效能資料都是匯出的 tooPower BI，而線條圖則都會建立 toodisplay 處理器使用率。</span><span class="sxs-lookup"><span data-stu-id="c8908-158">In this example, all performance data for a set of computers is exported tooPower BI and then a line graph is created toodisplay processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="c8908-159">建立記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="c8908-159">Create log search</span></span>
<span data-ttu-id="c8908-160">我們先建立 hello 資料，我們要 toosend toohello 資料集的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="c8908-160">We start by creating a log search for hello data that we want toosend toohello dataset.</span></span>  <span data-ttu-id="c8908-161">在此範例中，我們將使用一個查詢，傳回名稱開頭為 *srv*之電腦的所有效能資料。</span><span class="sxs-lookup"><span data-stu-id="c8908-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Power BI 排程](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="c8908-163">建立 Power BI 搜尋</span><span class="sxs-lookup"><span data-stu-id="c8908-163">Create Power BI Search</span></span>
<span data-ttu-id="c8908-164">我們按一下 hello **Power BI**按鈕 tooopen hello Power BI 對話方塊，並提供所需的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="c8908-164">We click hello **Power BI** button tooopen hello Power BI dialog and provide hello required information.</span></span>  <span data-ttu-id="c8908-165">我們想要每小時一次此搜尋 toorun 和建立資料集稱為*Contoso 效能*。</span><span class="sxs-lookup"><span data-stu-id="c8908-165">We want this search toorun once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="c8908-166">因為我們已經建立 hello 資料，我們想要的 hello 搜尋開啟，我們會保留 hello 預設值是*使用目前的搜尋查詢*如**已儲存搜尋**。</span><span class="sxs-lookup"><span data-stu-id="c8908-166">Since we already have hello search open that creates hello data we want, we keep hello default of *Use current search query* for **Saved Search**.</span></span>

![Power BI 搜尋](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="c8908-168">驗證 Power BI 搜尋</span><span class="sxs-lookup"><span data-stu-id="c8908-168">Verify Power BI Search</span></span>
<span data-ttu-id="c8908-169">tooverify 我們正確建立 hello 排程，我們會檢視 Power BI 搜尋下 hello hello 清單**設定**hello OMS 儀表板磚。</span><span class="sxs-lookup"><span data-stu-id="c8908-169">tooverify that we created hello schedule correctly, we view hello list of Power BI Searches under hello **Settings** tile in hello OMS dashboard.</span></span>  <span data-ttu-id="c8908-170">我們稍等幾分鐘，並重新整理此檢視，直到它會報告已執行 hello 同步處理。</span><span class="sxs-lookup"><span data-stu-id="c8908-170">We wait several minutes and refresh this view until it reports that hello sync has been run.</span></span>

![Power BI 搜尋](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a><span data-ttu-id="c8908-172">驗證 Power BI 中的 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="c8908-172">Verify hello dataset in Power BI</span></span>
<span data-ttu-id="c8908-173">我們會記錄在我們考量[powerbi.microsoft.com](http://powerbi.microsoft.com/)太捲動**資料集**在 hello hello 左窗格的底部。</span><span class="sxs-lookup"><span data-stu-id="c8908-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll too**Datasets** at hello bottom of hello left pane.</span></span>  <span data-ttu-id="c8908-174">我們可以看到該 hello *Contoso 效能*指出我們匯出已順利執行所列的資料集。</span><span class="sxs-lookup"><span data-stu-id="c8908-174">We can see that hello *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Power BI 資料集](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="c8908-176">根據資料集建立報表</span><span class="sxs-lookup"><span data-stu-id="c8908-176">Create report based on dataset</span></span>
<span data-ttu-id="c8908-177">我們選取 hello **Contoso 效能**資料集，然後按一下**結果**在 hello**欄位**屬於這個 dataset 的 hello 右 tooview hello 欄位 窗格。</span><span class="sxs-lookup"><span data-stu-id="c8908-177">We select hello **Contoso Perf** dataset and then click on **Results** in hello **Fields** pane on hello right tooview hello fields that are part of this dataset.</span></span>  <span data-ttu-id="c8908-178">toocreate 每一部電腦一行圖形顯示處理器使用率，我們會執行下列動作的 hello。</span><span class="sxs-lookup"><span data-stu-id="c8908-178">toocreate a line graph showing processor utilization for each computer, we perform hello following actions.</span></span>

1. <span data-ttu-id="c8908-179">選取 hello 行圖表視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c8908-179">Select hello Line chart visualization.</span></span>
2. <span data-ttu-id="c8908-180">拖曳**ObjectName**太**報表層級篩選**並檢查**處理器**。</span><span class="sxs-lookup"><span data-stu-id="c8908-180">Drag **ObjectName** too**Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="c8908-181">拖曳**CounterName**太**報表層級篩選**並檢查**%Processor Time**。</span><span class="sxs-lookup"><span data-stu-id="c8908-181">Drag **CounterName** too**Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="c8908-182">拖曳**CounterValue**太**值**。</span><span class="sxs-lookup"><span data-stu-id="c8908-182">Drag **CounterValue** too**Values**.</span></span>
5. <span data-ttu-id="c8908-183">拖曳**電腦**太**圖例**。</span><span class="sxs-lookup"><span data-stu-id="c8908-183">Drag **Computer** too**Legend**.</span></span>
6. <span data-ttu-id="c8908-184">拖曳**TimeGenerated**太**軸**。</span><span class="sxs-lookup"><span data-stu-id="c8908-184">Drag **TimeGenerated** too**Axis**.</span></span>

<span data-ttu-id="c8908-185">我們可以看到該 hello 產生折線圖會顯示 hello 我們的資料集的資料。</span><span class="sxs-lookup"><span data-stu-id="c8908-185">We can see that hello resulting line graph is displayed with hello data from our dataset.</span></span>

![Power BI 折線圖](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a><span data-ttu-id="c8908-187">儲存 hello 報表</span><span class="sxs-lookup"><span data-stu-id="c8908-187">Save hello report</span></span>
<span data-ttu-id="c8908-188">我們儲存按一下 hello hello 報告儲存在 hello 囉 」 畫面最上方的按鈕，並驗證它現在列在 hello hello 左窗格中的報表區段。</span><span class="sxs-lookup"><span data-stu-id="c8908-188">We save hello report by clicking on hello Save button at hello top of hello screen and validate that it is now listed in hello Reports section in hello left pane.</span></span>

![Power BI 報表](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="c8908-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8908-190">Next steps</span></span>
* <span data-ttu-id="c8908-191">深入了解[記錄搜尋](log-analytics-log-searches.md)toobuild 查詢可匯出 tooPower BI。</span><span class="sxs-lookup"><span data-stu-id="c8908-191">Learn about [log searches](log-analytics-log-searches.md) toobuild queries that can be exported tooPower BI.</span></span>
* <span data-ttu-id="c8908-192">深入了解[Power BI](http://powerbi.microsoft.com) toobuild 視覺效果是根據記錄分析的匯出。</span><span class="sxs-lookup"><span data-stu-id="c8908-192">Learn more about [Power BI](http://powerbi.microsoft.com) toobuild visualizations based on Log Analytics exports.</span></span>
