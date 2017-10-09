---
title: "在 Azure Log Analytics aaaUsing hello 記錄搜尋入口網站 |Microsoft 文件"
description: "本文包含的教學課程，描述如何 toocreate 記錄搜尋並分析資料儲存在您使用 hello 記錄搜尋入口網站的記錄分析工作區中。  hello 教學課程包含 tooreturn 不同類型的資料執行一些簡單的查詢和分析的結果。"
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
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="16244-104">在 Azure Log Analytics 使用 hello 記錄搜尋入口網站中建立的記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="16244-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="16244-105">本文說明 hello Azure Log Analytics 使用 hello 新的查詢語言中的記錄搜尋入口網站。</span><span class="sxs-lookup"><span data-stu-id="16244-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="16244-106">您可以深入了解 hello 新語言，並取得 hello 程序 tooupgrade 在工作區[升級您的 Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="16244-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="16244-107">如果您的工作區尚未升級的 toohello 新的查詢語言，您應該參閱太[尋找資料記錄分析中使用記錄搜尋](log-analytics-log-searches.md)hello 最新版 hello 記錄搜尋入口網站上的資訊。</span><span class="sxs-lookup"><span data-stu-id="16244-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="16244-108">本文包含的教學課程，描述如何 toocreate 記錄搜尋並分析資料儲存在您使用 hello 記錄搜尋入口網站的記錄分析工作區中。</span><span class="sxs-lookup"><span data-stu-id="16244-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="16244-109">hello 教學課程包含 tooreturn 不同類型的資料執行一些簡單的查詢和分析的結果。</span><span class="sxs-lookup"><span data-stu-id="16244-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="16244-110">它著重在 hello 修改 hello 查詢，而不是直接修改的記錄搜尋入口網站中的功能。</span><span class="sxs-lookup"><span data-stu-id="16244-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="16244-111">如需直接編輯 hello 查詢的詳細資訊，請參閱 hello[查詢語言參考](https://go.microsoft.com/fwlink/?linkid=856079)。</span><span class="sxs-lookup"><span data-stu-id="16244-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="16244-112">toocreate 搜尋在 hello Advanced Analytics 入口網站，而不是 hello 記錄搜尋入口網站，請參閱[hello Analytics 入口網站使用者入門](https://go.microsoft.com/fwlink/?linkid=856587)。</span><span class="sxs-lookup"><span data-stu-id="16244-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="16244-113">這兩個入口網站使用 hello 相同語言 tooaccess hello hello 記錄分析工作區中的相同資料的查詢。</span><span class="sxs-lookup"><span data-stu-id="16244-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16244-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="16244-114">Prerequisites</span></span>
<span data-ttu-id="16244-115">本教學課程假設您已經有產生的資料為 hello 查詢 tooanalyze 的至少一個已連接來源的記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="16244-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="16244-116">如果您沒有工作區，您可以建立一份免費使用 hello 程序在[開始記錄分析工作區使用](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="16244-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="16244-117">連線至少一個[Windows 代理程式](log-analytics-windows-agents.md)或一個[Linux 代理程式](log-analytics-linux-agents.md)toohello 工作區。</span><span class="sxs-lookup"><span data-stu-id="16244-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="16244-118">開啟 hello 記錄搜尋入口網站</span><span class="sxs-lookup"><span data-stu-id="16244-118">Open hello Log Search portal</span></span>
<span data-ttu-id="16244-119">首先開啟 hello 記錄搜尋入口網站。</span><span class="sxs-lookup"><span data-stu-id="16244-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="16244-120">您可以在 hello Azure 入口網站或 hello OMS 入口網站存取它。</span><span class="sxs-lookup"><span data-stu-id="16244-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="16244-121">開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="16244-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="16244-122">瀏覽 tooLog 分析，然後選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="16244-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="16244-123">請選取**記錄搜尋**在 hello Azure 入口網站或啟動 hello OMS 入口網站選取 toostay **OMS 入口網站**，然後按一下hello 記錄搜尋 按鈕。</span><span class="sxs-lookup"><span data-stu-id="16244-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![記錄檔搜尋按鈕](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="16244-125">建立簡單搜尋</span><span class="sxs-lookup"><span data-stu-id="16244-125">Create a simple search</span></span>
<span data-ttu-id="16244-126">最快方式 tooretrieve hello 與某些資料 toowork 是簡單的查詢，傳回資料表中的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="16244-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="16244-127">如果您有任何 Windows 或 Linux 用戶端連線的 tooyour 工作區，然後您就有可能是 hello 事件 (Windows) 或 Syslog (Linux) 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="16244-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="16244-128">輸入一個 hello 遵循 hello [搜尋] 方塊中的查詢，然後按一下 hello [搜尋] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="16244-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="16244-129">中的 hello 預設清單檢視中，傳回資料，您可以看到所傳回的總記錄數。</span><span class="sxs-lookup"><span data-stu-id="16244-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![簡單查詢](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="16244-131">只有 hello 每一筆記錄的第一個幾個屬性會顯示。</span><span class="sxs-lookup"><span data-stu-id="16244-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="16244-132">按一下**顯示更多**toodisplay 特定記錄的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="16244-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![記錄詳細資料](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="16244-134">設定 hello 時間範圍</span><span class="sxs-lookup"><span data-stu-id="16244-134">Set hello time scope</span></span>
<span data-ttu-id="16244-135">記錄分析所收集的每一筆記錄有**TimeGenerated**建立該 hello 記錄屬性，其中包含 hello 日期和時間。</span><span class="sxs-lookup"><span data-stu-id="16244-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="16244-136">Hello 記錄搜尋入口網站中的查詢只傳回記錄**TimeGenerated** hello hello 左邊囉 」 畫面顯示的時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="16244-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="16244-137">選取 hello 下拉式清單中，或修改 hello 滑桿，您可以變更 hello 時間篩選器。</span><span class="sxs-lookup"><span data-stu-id="16244-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="16244-138">hello 滑桿顯示橫條圖來顯示 hello 相對 hello 範圍內的每個時間區段的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="16244-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="16244-139">此區段會因 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="16244-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="16244-140">hello 預設時間範圍是**1 天**。</span><span class="sxs-lookup"><span data-stu-id="16244-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="16244-141">變更此值太**7 天**，應該增加 hello 的總記錄數。</span><span class="sxs-lookup"><span data-stu-id="16244-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![日期時間範圍](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="16244-143">篩選查詢結果的 hello</span><span class="sxs-lookup"><span data-stu-id="16244-143">Filter results of hello query</span></span>
<span data-ttu-id="16244-144">Hello 囉 」 畫面的左下的方是它可讓您篩選 toohello 查詢，而不需要直接修改它的 tooadd hello 篩選 窗格。</span><span class="sxs-lookup"><span data-stu-id="16244-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="16244-145">傳回的 hello 記錄的數個屬性會顯示其記錄的計數與與其前十個值。</span><span class="sxs-lookup"><span data-stu-id="16244-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="16244-146">如果您正在使用**事件**，選取 hello 核取方塊旁太**錯誤**下**EVENTLEVELNAME**。</span><span class="sxs-lookup"><span data-stu-id="16244-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="16244-147">如果您正在使用**Syslog**，選取 hello 核取方塊旁太**err**下**嚴重性層級**。</span><span class="sxs-lookup"><span data-stu-id="16244-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="16244-148">這樣會變更 hello 查詢的下列 toolimit hello hello tooone 結果 tooerror 事件。</span><span class="sxs-lookup"><span data-stu-id="16244-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="16244-150">新增屬性 toohello 篩選 窗格選取**新增 toofilters**從 hello 屬性功能表上的其中一個 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="16244-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![新增 toofilter 功能表](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="16244-152">您可以設定相同選取篩選器的 hello**篩選**想 toofilter hello 屬性功能表中的 hello 值的記錄。</span><span class="sxs-lookup"><span data-stu-id="16244-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="16244-153">您只需要 hello**篩選**內容的名稱以藍色的選項。</span><span class="sxs-lookup"><span data-stu-id="16244-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="16244-154">這些是可搜尋的欄位，已針對搜尋條件編列索引。</span><span class="sxs-lookup"><span data-stu-id="16244-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="16244-155">灰色的欄位是*任意可搜尋的文字*欄位只有 hello**顯示參考**選項。</span><span class="sxs-lookup"><span data-stu-id="16244-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="16244-156">此選項會傳回在任何屬性中具有該值的記錄。</span><span class="sxs-lookup"><span data-stu-id="16244-156">This option returns records that have that value in any property.</span></span>

![篩選功能表](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="16244-158">您可以藉由選取 hello 群組上的單一屬性的 hello 結果**分組**hello 記錄功能表中的選項。</span><span class="sxs-lookup"><span data-stu-id="16244-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="16244-159">這會新增[摘要](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator)hello 結果顯示在圖表中的運算子 tooyour 查詢。</span><span class="sxs-lookup"><span data-stu-id="16244-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="16244-160">您可以群組在一個以上的屬性，但您直接需要 tooedit hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="16244-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="16244-161">選取 hello 記錄功能表下一步 hello hello**電腦**屬性，並選取**Group by 'Computer'**。</span><span class="sxs-lookup"><span data-stu-id="16244-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![依電腦分組](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="16244-163">處理結果</span><span class="sxs-lookup"><span data-stu-id="16244-163">Work with results</span></span>
<span data-ttu-id="16244-164">hello 記錄搜尋入口網站有各種不同的功能使用 hello 查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="16244-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="16244-165">您可以排序、 篩選和群組結果 tooanalyze hello 資料而不需修改 hello 實際查詢。</span><span class="sxs-lookup"><span data-stu-id="16244-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="16244-166">根據預設，不會排序查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="16244-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="16244-167">tooview hello 表單資料的資料表提供其他選項用來篩選和排序，按一下**資料表**。</span><span class="sxs-lookup"><span data-stu-id="16244-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![資料表檢視](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="16244-169">按一下記錄 tooview hello 詳細資料，該記錄 hello 箭號。</span><span class="sxs-lookup"><span data-stu-id="16244-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![排序結果](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="16244-171">按一下資料行標題，對欄位進行排序。</span><span class="sxs-lookup"><span data-stu-id="16244-171">Sort on any field by clicking on its column header.</span></span>

![排序結果](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="16244-173">篩選 hello hello 按一下 hello 篩選按鈕，並提供篩選條件的資料行中的特定值的結果。</span><span class="sxs-lookup"><span data-stu-id="16244-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![篩選結果](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="16244-175">藉由拖曳其資料行標題 toohello 結果的頂端 hello 分組的資料行上。</span><span class="sxs-lookup"><span data-stu-id="16244-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="16244-176">您可以在多個欄位上分組拖曳多個資料行 toohello 頂端。</span><span class="sxs-lookup"><span data-stu-id="16244-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![群組結果](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="16244-178">使用效能資料</span><span class="sxs-lookup"><span data-stu-id="16244-178">Work with performance data</span></span>
<span data-ttu-id="16244-179">針對 Windows 和 Linux 代理程式的效能資料會儲存在 hello 記錄分析工作區中 hello**效能**資料表。</span><span class="sxs-lookup"><span data-stu-id="16244-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="16244-180">效能記錄看起來就像其他任何記錄，我們可以撰寫會傳回所有效能記錄的簡單查詢，就像使用事件一樣。</span><span class="sxs-lookup"><span data-stu-id="16244-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![效能資料](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="16244-182">針對所有效能物件和計數器傳回數百萬筆記錄並不太實用。</span><span class="sxs-lookup"><span data-stu-id="16244-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="16244-183">您可以使用相同的方法，您使用上述 toofilter hello 資料或只是輸入 hello 下列查詢的 hello 直接在 hello 記錄搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="16244-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="16244-184">這對於 Windows 和 Linux 電腦都只會傳回處理器使用率記錄。</span><span class="sxs-lookup"><span data-stu-id="16244-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![處理器使用率](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="16244-186">這會限制 hello 資料 tooa 特定計數器，但它仍不會將它放入的形式，尤其有用。</span><span class="sxs-lookup"><span data-stu-id="16244-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="16244-187">您可以在折線圖中顯示 hello 資料，但首先必須 toogroup 它的電腦和 TimeGenerated。</span><span class="sxs-lookup"><span data-stu-id="16244-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="16244-188">toogroup 上多個欄位，您需要 toomodify hello 查詢直接管理，因此修改 hello 查詢 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="16244-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="16244-189">這會使用 hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg())函式上 hello **CounterValue**每個小時內的屬性 toocalculate hello 平均值。</span><span class="sxs-lookup"><span data-stu-id="16244-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![效能資料圖表](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="16244-191">既然 hello 資料適當分組，您就可以顯示視覺圖表中加入 hello[呈現](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator)運算子。</span><span class="sxs-lookup"><span data-stu-id="16244-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![折線圖](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="16244-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="16244-193">Next steps</span></span>

- <span data-ttu-id="16244-194">深入了解在 hello 記錄分析查詢語言[hello Analytics 入口網站使用者入門](https://go.microsoft.com/fwlink/?linkid=856079)。</span><span class="sxs-lookup"><span data-stu-id="16244-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="16244-195">逐步解說的教學課程使用 hello [Advanced Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)可讓您 toorun hello 相同的查詢及存取 hello 與 hello 記錄搜尋入口網站相同的資料。</span><span class="sxs-lookup"><span data-stu-id="16244-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
