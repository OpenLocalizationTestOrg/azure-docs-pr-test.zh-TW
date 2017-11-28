---
title: "在 OMS 記錄分析 aaaLog 搜尋 |Microsoft 文件"
description: "您要求記錄檔搜尋 tooretrieve 記錄分析中的任何資料。  本文描述新的記錄檔中記錄分析所使用的搜尋，並提供您之前建立一個需要 toounderstand 的概念。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a><span data-ttu-id="1ade8-104">了解 Log Analytics 中的記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="1ade8-104">Understanding log searches in Log Analytics</span></span>

> [!NOTE]
> <span data-ttu-id="1ade8-105">本文說明在使用新的查詢語言 hello Azure 記錄分析記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="1ade8-105">This article describes log searches in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="1ade8-106">您可以深入了解 hello 新語言，並取得 hello 程序 tooupgrade 在工作區[升級您的 Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="1ade8-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="1ade8-107">如果您的工作區尚未升級的 toohello 新的查詢語言，您應該參閱太[尋找資料記錄分析中使用記錄搜尋](log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="1ade8-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

<span data-ttu-id="1ade8-108">您要求記錄檔搜尋 tooretrieve 記錄分析中的任何資料。</span><span class="sxs-lookup"><span data-stu-id="1ade8-108">You require a log search tooretrieve any data from Log Analytics.</span></span>  <span data-ttu-id="1ade8-109">是否您正在分析 hello 入口網站中的資料，設定警示規則 toobe 通知的特定條件或擷取的資料使用 hello 記錄分析 API，您將使用您想要記錄檔搜尋 toospecify hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1ade8-109">Whether you're analyzing data in hello portal, configuring an alert rule toobe notified of a particular condition, or retrieving data using hello Log Analytics API, you will use a log search toospecify hello data you want.</span></span>  <span data-ttu-id="1ade8-110">本文說明記錄搜尋在 Log Analytics 中的使用方式，並且提供在建立之前應該了解的概念。</span><span class="sxs-lookup"><span data-stu-id="1ade8-110">This article describes how log searches are used in Log Analytics and provides concepts that should understand before creating one.</span></span> <span data-ttu-id="1ade8-111">請參閱 hello[後續步驟](#next-steps)如需建立和編輯的記錄搜尋詳細資料和 hello 查詢語言參考一節。</span><span class="sxs-lookup"><span data-stu-id="1ade8-111">See hello [Next steps](#next-steps) section for details on creating and editing log searches and for references on hello query language.</span></span>

## <a name="where-log-searches-are-used"></a><span data-ttu-id="1ade8-112">記錄搜尋的使用位置</span><span class="sxs-lookup"><span data-stu-id="1ade8-112">Where log searches are used</span></span>

<span data-ttu-id="1ade8-113">hello 不同的方式，您將使用中記錄分析記錄搜尋 hello 如下：</span><span class="sxs-lookup"><span data-stu-id="1ade8-113">hello different ways that you will use log searches in Log Analytics include hello following:</span></span>

- <span data-ttu-id="1ade8-114">**入口網站。**</span><span class="sxs-lookup"><span data-stu-id="1ade8-114">**Portals.**</span></span> <span data-ttu-id="1ade8-115">您可以執行互動式資料分析與 hello hello 儲存機制中[記錄搜尋入口網站](log-analytics-log-search-log-search-portal.md)或 hello [Advanced Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)。</span><span class="sxs-lookup"><span data-stu-id="1ade8-115">You can perform interactive analysis of data in hello repository with hello [Log Search portal](log-analytics-log-search-log-search-portal.md) or hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="1ade8-116">這可讓您 tooedit 您查詢及分析各種不同的格式和視覺效果中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="1ade8-116">This allows you tooedit your query and analyze hello results in a variety of formats and visualizations.</span></span>  <span data-ttu-id="1ade8-117">您所建立之大多數查詢會在其中一個 hello 入口網站中開始，然後再複製 [一旦您確認它如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="1ade8-117">Most queries that you create will start in one of hello portals and then copied once you verify that it works as expected.</span></span>
- <span data-ttu-id="1ade8-118">**警示規則。**</span><span class="sxs-lookup"><span data-stu-id="1ade8-118">**Alert rules.**</span></span> <span data-ttu-id="1ade8-119">[警示規則](log-analytics-alerts.md)會主動識別您的工作區中資料的問題。</span><span class="sxs-lookup"><span data-stu-id="1ade8-119">[Alert rules](log-analytics-alerts.md) proactively identify issues from data in your workspace.</span></span>  <span data-ttu-id="1ade8-120">每個警示規則是根據以固定間隔自動執行的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="1ade8-120">Each alert rule is based on a log search that is automatically run at regular intervals.</span></span>  <span data-ttu-id="1ade8-121">如果應該建立警示，hello 結果將會檢查的 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="1ade8-121">hello results are inspected toodetermine if an alert should be created.</span></span>
- <span data-ttu-id="1ade8-122">**檢視。**</span><span class="sxs-lookup"><span data-stu-id="1ade8-122">**Views.**</span></span>  <span data-ttu-id="1ade8-123">您可以建立視覺效果的資料包含在與使用者儀表板的 toobe[檢視表設計工具](log-analytics-view-designer.md)。</span><span class="sxs-lookup"><span data-stu-id="1ade8-123">You can create visualizations of data toobe included in user dashboards with [View Designer](log-analytics-view-designer.md).</span></span>  <span data-ttu-id="1ade8-124">記錄搜尋提供所使用的 hello 資料[磚](log-analytics-view-designer-tiles.md)和[視覺效果部分](log-analytics-view-designer-parts.md)各檢視中。</span><span class="sxs-lookup"><span data-stu-id="1ade8-124">Log searches provide hello data used by [tiles](log-analytics-view-designer-tiles.md) and [visualization parts](log-analytics-view-designer-parts.md) in each view.</span></span>  <span data-ttu-id="1ade8-125">您可以向下鑽研視覺效果部分 hello hello 資料記錄搜尋入口 tooperform 進一步分析。</span><span class="sxs-lookup"><span data-stu-id="1ade8-125">You can drill down from visualization parts into hello Log Search portal tooperform further analysis on hello data.</span></span>
- <span data-ttu-id="1ade8-126">**匯出。**</span><span class="sxs-lookup"><span data-stu-id="1ade8-126">**Export.**</span></span>  <span data-ttu-id="1ade8-127">當您從 hello 記錄分析工作區 tooExcel 匯出資料或[Power BI](log-analytics-powerbi.md)，建立記錄檔搜尋 toodefine hello 資料 tooexport。</span><span class="sxs-lookup"><span data-stu-id="1ade8-127">When you export data from hello Log Analytics workspace tooExcel or [Power BI](log-analytics-powerbi.md), you create a log search toodefine hello data tooexport.</span></span>
- <span data-ttu-id="1ade8-128">**Powershell。**</span><span class="sxs-lookup"><span data-stu-id="1ade8-128">**PowerShell.**</span></span> <span data-ttu-id="1ade8-129">您可以從命令列或使用 Azure 自動化 runbook 執行的 PowerShell 指令碼[Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve 記錄分析的資料。</span><span class="sxs-lookup"><span data-stu-id="1ade8-129">You can run a PowerShell script from a command line or an Azure Automation runbook that uses [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve data from Log Analytics.</span></span>  <span data-ttu-id="1ade8-130">此 cmdlet 需要查詢 toodetermine hello 資料 tooretrieve。</span><span class="sxs-lookup"><span data-stu-id="1ade8-130">This cmdlet requires a query toodetermine hello data tooretrieve.</span></span>
- <span data-ttu-id="1ade8-131">**Log Analytics API。**</span><span class="sxs-lookup"><span data-stu-id="1ade8-131">**Log Analytics API.**</span></span>  <span data-ttu-id="1ade8-132">hello[記錄分析記錄搜尋 API](log-analytics-log-search-api.md) tooretrieve 資料從 hello] 工作區可讓任何 REST API 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1ade8-132">hello [Log Analytics log search API](log-analytics-log-search-api.md) allows any REST API client tooretrieve data from hello workspace.</span></span>  <span data-ttu-id="1ade8-133">hello API 要求包含對記錄分析 toodetermine hello 資料 tooretrieve 所執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="1ade8-133">hello API request includes a query that is run against Log Analytics toodetermine hello data tooretrieve.</span></span>

![記錄檔搜尋](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a><span data-ttu-id="1ade8-135">Log Analytics 資料的組織方式</span><span class="sxs-lookup"><span data-stu-id="1ade8-135">How Log Analytics data is organized</span></span>
<span data-ttu-id="1ade8-136">當您建置查詢時，您先判斷哪些資料表有您要尋找的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1ade8-136">When you build a query, you start by determining which tables have hello data that you're looking for.</span></span> <span data-ttu-id="1ade8-137">每個[資料來源](log-analytics-data-sources.md)和[方案](../operations-management-suite/operations-management-suite-solutions.md)專用 hello 記錄分析工作區中的資料表中儲存其資料。</span><span class="sxs-lookup"><span data-stu-id="1ade8-137">Each [data source](log-analytics-data-sources.md) and [solution](../operations-management-suite/operations-management-suite-solutions.md) stores its data in dedicated tables in hello Log Analytics workspace.</span></span>  <span data-ttu-id="1ade8-138">針對每個資料來源和解決方案的文件包括 hello hello 資料類型，它會建立名稱和每個屬性的描述。</span><span class="sxs-lookup"><span data-stu-id="1ade8-138">Documentation for each data source and solution includes hello name of hello data type that it creates and a description of each of its properties.</span></span>     <span data-ttu-id="1ade8-139">許多查詢只需要從單一資料表的資料，但其他人可以使用各種不同的選項 tooinclude 資料從多個資料表。</span><span class="sxs-lookup"><span data-stu-id="1ade8-139">Many queries will only require data from a single tables, but others may use a variety of options tooinclude data from multiple tables.</span></span>

![資料表](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a><span data-ttu-id="1ade8-141">撰寫查詢</span><span class="sxs-lookup"><span data-stu-id="1ade8-141">Writing a query</span></span>
<span data-ttu-id="1ade8-142">Hello 核心的記錄檔中記錄分析搜尋是[廣泛的查詢語言](https://docs.loganalytics.io/)，可讓您擷取和分析資料，從各種不同的方式 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="1ade8-142">At hello core of log searches in Log Analytics is [an extensive query language](https://docs.loganalytics.io/) that lets you retrieve and analyze data from hello repository in a variety of ways.</span></span>  <span data-ttu-id="1ade8-143">這個相同的查詢語言用於 [Application Insights](../application-insights/app-insights-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="1ade8-143">This same query language is used for [Application Insights](../application-insights/app-insights-analytics.md).</span></span>  <span data-ttu-id="1ade8-144">了解 toowrite 查詢的記錄分析中的重要 toocreating 記錄搜尋的方式。</span><span class="sxs-lookup"><span data-stu-id="1ade8-144">Learning how toowrite a query is critical toocreating log searches in Log Analytics.</span></span>  <span data-ttu-id="1ade8-145">通常會先處理基本查詢，然後進行 toouse 更進階函式為您的需求變得更複雜。</span><span class="sxs-lookup"><span data-stu-id="1ade8-145">You'll typically start with basic queries and then progress toouse more advanced functions as your requirements become more complex.</span></span>

<span data-ttu-id="1ade8-146">hello 基本查詢結構是後面接著一系列的運算子，以縱線字元分隔的來源資料表`|`。</span><span class="sxs-lookup"><span data-stu-id="1ade8-146">hello basic structure of a query is a source table followed by a series of operators separated by a pipe character `|`.</span></span>  <span data-ttu-id="1ade8-147">您可以鏈結在一起的多個運算子 toorefine hello 資料，以及執行進階函式。</span><span class="sxs-lookup"><span data-stu-id="1ade8-147">You can chain together multiple operators toorefine hello data and perform advanced functions.</span></span>

<span data-ttu-id="1ade8-148">例如，假設您想 toofind hello 前的十個電腦以 hello 大部分的錯誤事件 hello 透過前一天。</span><span class="sxs-lookup"><span data-stu-id="1ade8-148">For example, suppose you wanted toofind hello top ten computers with hello most error events over hello past day.</span></span>

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

<span data-ttu-id="1ade8-149">或者，您想在 hello 最後一天中沒活動訊號的 toofind 電腦。</span><span class="sxs-lookup"><span data-stu-id="1ade8-149">Or maybe you want toofind computers that haven't had a heartbeat in hello last day.</span></span>

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

<span data-ttu-id="1ade8-150">如何折線圖與 hello 從過去一週的每一部電腦的處理器使用量？</span><span class="sxs-lookup"><span data-stu-id="1ade8-150">How about a line chart with hello processor utilization for each computer from last week?</span></span>

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

<span data-ttu-id="1ade8-151">您可以從 hello 的 hello 種類的資料，您正在使用，不論這些快速範例看到 hello 查詢的結構非常類似。</span><span class="sxs-lookup"><span data-stu-id="1ade8-151">You can see from these quick samples that regardless of hello kind of data that you're working with, hello structure of hello query is similar.</span></span>  <span data-ttu-id="1ade8-152">您可以細分它為不同的步驟，透過 hello 管線 toohello 下一個命令送出 hello 從一個命令產生的資料。</span><span class="sxs-lookup"><span data-stu-id="1ade8-152">You can break it down into distinct steps where hello resulting data from one command is sent through hello pipeline toohello next command.</span></span>

<span data-ttu-id="1ade8-153">如需包括教學課程和語言參考 hello Azure Log Analytics 查詢語言的完整文件，請參閱 hello [Azure Log Analytics 查詢語言文件](https://docs.loganalytics.io/)。</span><span class="sxs-lookup"><span data-stu-id="1ade8-153">For complete documentation on hello Azure Log Analytics query language including tutorials and language reference, see hello [Azure Log Analytics query language documentation](https://docs.loganalytics.io/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ade8-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1ade8-154">Next steps</span></span>

- <span data-ttu-id="1ade8-155">深入了解 hello[入口網站，您使用 toocreate 和編輯的記錄搜尋](log-analytics-log-search-portals.md)。</span><span class="sxs-lookup"><span data-stu-id="1ade8-155">Learn about hello [portals that you use toocreate and edit log searches](log-analytics-log-search-portals.md).</span></span>
- <span data-ttu-id="1ade8-156">簽出[上撰寫查詢的教學課程](https://go.microsoft.com/fwlink/?linkid=856078)使用 hello 新的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="1ade8-156">Check out a [tutorial on writing queries](https://go.microsoft.com/fwlink/?linkid=856078) using hello new query language.</span></span>
