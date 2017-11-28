---
title: "在 Azure Log Analytics 中使用記錄搜尋入口網站 | Microsoft Docs"
description: "本文包含一篇教學課程，說明如何使用記錄搜尋入口網站來建立記錄搜尋，以及分析儲存在 Log Analytics 工作區的資料。  教學課程包含執行一些簡單查詢以傳回不同類型的資料並分析結果。"
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
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 6fc556ceb34cde26d5f3789a2397cdaa34b0b84d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="7e388-104">在 Azure Log Analytics 中使用記錄搜尋入口網站來建立記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="7e388-104">Create log searches in Azure Log Analytics using the Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="7e388-105">本文會說明 Azure Log Analytics 中使用新查詢語言的記錄搜尋入口網站。</span><span class="sxs-lookup"><span data-stu-id="7e388-105">This article describes the Log Search portal in Azure Log Analytics using the new query language.</span></span>  <span data-ttu-id="7e388-106">您可以在[將 Azure Log Analytics 工作區升級為新的記錄搜尋](log-analytics-log-search-upgrade.md)中，深入了解新的語言，並且取得升級工作區的程序。</span><span class="sxs-lookup"><span data-stu-id="7e388-106">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="7e388-107">如果您的工作區尚未升級為新的查詢語言，您應該參閱[在 Log Analytics 中使用記錄搜尋以尋找資料](log-analytics-log-searches.md)，以取得記錄搜尋入口網站目前版本的資訊。</span><span class="sxs-lookup"><span data-stu-id="7e388-107">If your workspace hasn't been upgraded to the new query language, you should refer to [Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on the current version of the Log Search portal.</span></span>

<span data-ttu-id="7e388-108">本文包含一篇教學課程，說明如何使用記錄搜尋入口網站來建立記錄搜尋，以及分析儲存在 Log Analytics 工作區的資料。</span><span class="sxs-lookup"><span data-stu-id="7e388-108">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="7e388-109">教學課程包含執行一些簡單查詢以傳回不同類型的資料並分析結果。</span><span class="sxs-lookup"><span data-stu-id="7e388-109">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="7e388-110">其著重在記錄搜尋入口網站的功能，可修改查詢內容卻不必直接修改查詢本身。</span><span class="sxs-lookup"><span data-stu-id="7e388-110">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="7e388-111">如需直接編輯查詢的詳細資訊，請參閱[查詢語言參考](https://go.microsoft.com/fwlink/?linkid=856079)。</span><span class="sxs-lookup"><span data-stu-id="7e388-111">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="7e388-112">若要在進階 Analytics 入口網站 (而非記錄搜尋入口網站) 中建立搜尋，請參閱 [Analytics 入口網站的使用者入門](https://go.microsoft.com/fwlink/?linkid=856587)。</span><span class="sxs-lookup"><span data-stu-id="7e388-112">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="7e388-113">這兩個入口網站使用相同的查詢語言在 Log Analytics 工作區中存取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="7e388-113">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e388-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="7e388-114">Prerequisites</span></span>
<span data-ttu-id="7e388-115">本教學課程假設您已擁有 Log Analytics 工作區，且其具有至少一個連線來源以產生供查詢分析的資料。</span><span class="sxs-lookup"><span data-stu-id="7e388-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="7e388-116">如果您沒有工作區，可以使用[開始使用 Log Analytics 工作區](log-analytics-get-started.md)的程序來建立免費工作區。</span><span class="sxs-lookup"><span data-stu-id="7e388-116">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="7e388-117">至少將一個 [Windows 代理程式](log-analytics-windows-agents.md)或一個 [Linux 代理程式](log-analytics-linux-agents.md)連線到工作區。</span><span class="sxs-lookup"><span data-stu-id="7e388-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="7e388-118">開啟記錄搜尋入口網站</span><span class="sxs-lookup"><span data-stu-id="7e388-118">Open the Log Search portal</span></span>
<span data-ttu-id="7e388-119">從開啟記錄搜尋入口網站開始。</span><span class="sxs-lookup"><span data-stu-id="7e388-119">Start by opening the Log Search portal.</span></span>  <span data-ttu-id="7e388-120">您可以在 Azure 入口網站或 OMS 入口網站存取它。</span><span class="sxs-lookup"><span data-stu-id="7e388-120">You can access it in either the Azure portal or the OMS portal.</span></span>

1. <span data-ttu-id="7e388-121">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7e388-121">Open the Azure portal.</span></span>
2. <span data-ttu-id="7e388-122">瀏覽至 Log Analytics 並選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="7e388-122">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="7e388-123">請選取 [記錄搜尋] 以停留在 Azure 入口網站，或選取 [OMS 入口網站] 來啟動 OMS 入口網站，然後按一下 [記錄搜尋] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7e388-123">Either select **Log Search** to stay in the Azure portal or launch the OMS portal by selecting **OMS Portal** and then clicking the Log Search button.</span></span>

![記錄檔搜尋按鈕](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="7e388-125">建立簡單搜尋</span><span class="sxs-lookup"><span data-stu-id="7e388-125">Create a simple search</span></span>
<span data-ttu-id="7e388-126">若要擷取某些資料來使用，最快的方式是使用會傳回資料表中所有記錄的簡單查詢。</span><span class="sxs-lookup"><span data-stu-id="7e388-126">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="7e388-127">如果有任何 Windows 或 Linux 用戶端連線到您的工作區，則您會擁有事件 (Windows) 或 Syslog (Linux) 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="7e388-127">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="7e388-128">在搜尋方塊中輸入以下其中一項查詢，然後按一下搜尋按鈕。</span><span class="sxs-lookup"><span data-stu-id="7e388-128">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="7e388-129">資料會傳回到預設清單檢視中，您可以看到傳回的記錄總數。</span><span class="sxs-lookup"><span data-stu-id="7e388-129">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![簡單查詢](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="7e388-131">每筆記錄只會顯示前幾個屬性。</span><span class="sxs-lookup"><span data-stu-id="7e388-131">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="7e388-132">按一下 [顯示更多] 以顯示特定記錄的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="7e388-132">Click **show more** to display all properties for a particular record.</span></span>

![記錄詳細資料](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="7e388-134">設定時間範圍</span><span class="sxs-lookup"><span data-stu-id="7e388-134">Set the time scope</span></span>
<span data-ttu-id="7e388-135">Log Analytics 所收集的每一筆記錄都有 **TimeGenerated** 屬性，其包含記錄建立的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="7e388-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="7e388-136">記錄搜尋入口網站中的查詢只會傳回 **TimeGenerated** 在時間範圍內的記錄，時間範圍會顯示在畫面左側。</span><span class="sxs-lookup"><span data-stu-id="7e388-136">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="7e388-137">您可以選取下拉式清單或修改滑桿來變更時間篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7e388-137">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="7e388-138">滑桿會顯示出直條圖，圖中則顯示時間範圍內每個區段的相對記錄數目。</span><span class="sxs-lookup"><span data-stu-id="7e388-138">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="7e388-139">區段會依範圍而有所不同。</span><span class="sxs-lookup"><span data-stu-id="7e388-139">This segment will vary depending on the range.</span></span>

<span data-ttu-id="7e388-140">預設時間範圍是 **1 天**。</span><span class="sxs-lookup"><span data-stu-id="7e388-140">The default time scope is **1 day**.</span></span>  <span data-ttu-id="7e388-141">將此值變更為 **7 天**，則記錄總數應該會增加。</span><span class="sxs-lookup"><span data-stu-id="7e388-141">Change this value to **7 days**, and the total number of records should increase.</span></span>

![日期時間範圍](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="7e388-143">篩選查詢結果</span><span class="sxs-lookup"><span data-stu-id="7e388-143">Filter results of the query</span></span>
<span data-ttu-id="7e388-144">畫面左側是篩選窗格，可讓您新增篩選條件到查詢中，而不需要直接修改查詢。</span><span class="sxs-lookup"><span data-stu-id="7e388-144">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="7e388-145">會顯示傳回記錄的多個屬性及其前十個值與記錄計數。</span><span class="sxs-lookup"><span data-stu-id="7e388-145">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="7e388-146">如果您使用的是**事件**，選取 [EVENTLEVELNAME] 下方 [錯誤] 旁的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7e388-146">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="7e388-147">如果您使用的是 **Syslog**，選取 [SEVERITYLEVEL] 下方 [錯誤] 旁的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7e388-147">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="7e388-148">這會將查詢變更為下列其中一個，以將結果限制為錯誤事件。</span><span class="sxs-lookup"><span data-stu-id="7e388-148">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![篩選器](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="7e388-150">從其中一個記錄的屬性功能表中選取 [新增至篩選器]，將屬性新增至篩選窗格。</span><span class="sxs-lookup"><span data-stu-id="7e388-150">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![新增至篩選功能表](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="7e388-152">您可以從記錄的屬性功能表選取具有所要篩選值的 [篩選]，以設定相同的篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7e388-152">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="7e388-153">只有名稱是藍色的屬性才有 [篩選] 選項。</span><span class="sxs-lookup"><span data-stu-id="7e388-153">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="7e388-154">這些是可搜尋的欄位，已針對搜尋條件編列索引。</span><span class="sxs-lookup"><span data-stu-id="7e388-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="7e388-155">灰色的欄位是「自然語言檢索搜尋旗標」欄位，只有 [顯示參考] 選項。</span><span class="sxs-lookup"><span data-stu-id="7e388-155">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="7e388-156">此選項會傳回在任何屬性中具有該值的記錄。</span><span class="sxs-lookup"><span data-stu-id="7e388-156">This option returns records that have that value in any property.</span></span>

![篩選功能表](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="7e388-158">您可以選取記錄功能表中的 [分組依據] 選項，在單一屬性上群組結果。</span><span class="sxs-lookup"><span data-stu-id="7e388-158">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="7e388-159">這會將[摘要](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator)運算子新增到查詢中，可在圖表中顯示結果。</span><span class="sxs-lookup"><span data-stu-id="7e388-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="7e388-160">您可以群組一個以上的屬性，但需要直接編輯查詢。</span><span class="sxs-lookup"><span data-stu-id="7e388-160">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="7e388-161">選取**電腦**屬性旁的記錄功能表，並選取 [依「電腦」分組]。</span><span class="sxs-lookup"><span data-stu-id="7e388-161">Select the record menu next the the **Computer** property and select **Group by 'Computer'**.</span></span>  

![依電腦分組](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="7e388-163">處理結果</span><span class="sxs-lookup"><span data-stu-id="7e388-163">Work with results</span></span>
<span data-ttu-id="7e388-164">記錄搜尋入口網站有各種功能，以供使用查詢結果。</span><span class="sxs-lookup"><span data-stu-id="7e388-164">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="7e388-165">您可以排序、篩選和群組結果來分析資料，而不需修改實際的查詢。</span><span class="sxs-lookup"><span data-stu-id="7e388-165">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="7e388-166">根據預設，不會排序查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="7e388-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="7e388-167">若要以可提供其他篩選和排序選項的資料表形式來檢視資料，按一下 [資料表]。</span><span class="sxs-lookup"><span data-stu-id="7e388-167">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![資料表檢視](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="7e388-169">按一下記錄旁的箭號以檢視該記錄的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7e388-169">Click the arrow by a record to view the details for that record.</span></span>

![排序結果](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="7e388-171">按一下資料行標題，對欄位進行排序。</span><span class="sxs-lookup"><span data-stu-id="7e388-171">Sort on any field by clicking on its column header.</span></span>

![排序結果](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="7e388-173">按一下篩選按鈕並提供篩選條件，以篩選出資料行中具特定值的結果。</span><span class="sxs-lookup"><span data-stu-id="7e388-173">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![篩選結果](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="7e388-175">將資料行標題拖曳至結果上方，以群組資料行。</span><span class="sxs-lookup"><span data-stu-id="7e388-175">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="7e388-176">您可以將多個資料行拖曳至上方，以群組多個欄位。</span><span class="sxs-lookup"><span data-stu-id="7e388-176">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![群組結果](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="7e388-178">使用效能資料</span><span class="sxs-lookup"><span data-stu-id="7e388-178">Work with performance data</span></span>
<span data-ttu-id="7e388-179">Windows 和 Linux 代理程式的效能資料都儲存在 Log Analytics 工作區的**效能**資料表中。</span><span class="sxs-lookup"><span data-stu-id="7e388-179">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="7e388-180">效能記錄看起來就像其他任何記錄，我們可以撰寫會傳回所有效能記錄的簡單查詢，就像使用事件一樣。</span><span class="sxs-lookup"><span data-stu-id="7e388-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![效能資料](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="7e388-182">針對所有效能物件和計數器傳回數百萬筆記錄並不太實用。</span><span class="sxs-lookup"><span data-stu-id="7e388-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="7e388-183">您可以使用與上述相同的方法來篩選資料，或直接在 [記錄搜尋] 方塊中輸入下列查詢。</span><span class="sxs-lookup"><span data-stu-id="7e388-183">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="7e388-184">這對於 Windows 和 Linux 電腦都只會傳回處理器使用率記錄。</span><span class="sxs-lookup"><span data-stu-id="7e388-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![處理器使用率](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="7e388-186">這可讓資料限制在特定的計數器，但仍無法以非常實用的形式來呈現資料。</span><span class="sxs-lookup"><span data-stu-id="7e388-186">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="7e388-187">您可透過折線圖顯示資料，但首先需要以 [電腦] 與 [TimeGenerated] 進行群組。</span><span class="sxs-lookup"><span data-stu-id="7e388-187">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="7e388-188">若要群組多個欄位，您需要直接修改查詢，因此，請將查詢修改如下。</span><span class="sxs-lookup"><span data-stu-id="7e388-188">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="7e388-189">這是在 **CounterValue** 屬性上使用 [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) 函式來計算每小時的平均值。</span><span class="sxs-lookup"><span data-stu-id="7e388-189">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![效能資料圖表](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="7e388-191">資料既已適當分組，您可以新增[轉譯](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator)運算子，以視覺圖表來顯示資料。</span><span class="sxs-lookup"><span data-stu-id="7e388-191">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![折線圖](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="7e388-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e388-193">Next steps</span></span>

- <span data-ttu-id="7e388-194">在 [Analytics 入口網站的使用者入門](https://go.microsoft.com/fwlink/?linkid=856079)中深入了解 Log Analytics 查詢語言。</span><span class="sxs-lookup"><span data-stu-id="7e388-194">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="7e388-195">使用[進階 Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)的教學課程逐步引導，其可讓您執行相同的查詢及存取相同的資料，如同記錄搜尋入口網站。</span><span class="sxs-lookup"><span data-stu-id="7e388-195">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>
