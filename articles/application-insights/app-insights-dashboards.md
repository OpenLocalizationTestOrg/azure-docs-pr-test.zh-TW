---
title: "aaaDashboards 及瀏覽方式 hello Azure Application Insights |Microsoft 文件"
description: "建立重要 APM 圖表和查詢的檢視。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="4662a-103">瀏覽和 hello Application Insights 入口網站的儀表板</span><span class="sxs-lookup"><span data-stu-id="4662a-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="4662a-104">之後[設定您的專案上的 Application Insights](app-insights-overview.md)，您的應用程式效能和使用方式相關的遙測資料會出現在您的專案中 hello 的 Application Insights 資源[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4662a-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="4662a-105">尋找遙測</span><span class="sxs-lookup"><span data-stu-id="4662a-105">Find your telemetry</span></span>
<span data-ttu-id="4662a-106">登入 toohello [Azure 入口網站](https://portal.azure.com)並瀏覽 toohello 您建立應用程式的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="4662a-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![按一下 [瀏覽]，選取 [Application Insights]，然後選取您的應用程式。](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="4662a-108">應用程式的 hello 概觀刀鋒視窗 （頁） 顯示 hello 金鑰診斷度量資訊的應用程式的摘要，且閘道 toohello hello 入口網站的其他功能。</span><span class="sxs-lookup"><span data-stu-id="4662a-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![主要路由 tooview 您遙測](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="4662a-110">您可以自訂任何 hello 圖表和方格，並將其釘選 tooa 儀表板。</span><span class="sxs-lookup"><span data-stu-id="4662a-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="4662a-111">這樣一來，您可以匯集 hello 金鑰遙測來自不同的應用程式中央的儀表板上。</span><span class="sxs-lookup"><span data-stu-id="4662a-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="4662a-112">儀表板</span><span class="sxs-lookup"><span data-stu-id="4662a-112">Dashboards</span></span>
<span data-ttu-id="4662a-113">hello 首先之後，您看到您登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)是儀表板。</span><span class="sxs-lookup"><span data-stu-id="4662a-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="4662a-114">這裡您可以將一起 hello 圖表，在所有的 Azure 資源，包括遙測資料都是最重要的 tooyou [Azure Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4662a-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![自訂的儀表板。](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="4662a-116">**瀏覽 toospecific 資源**例如 Application Insights 中的應用程式： 使用 hello 左的工具列。</span><span class="sxs-lookup"><span data-stu-id="4662a-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="4662a-117">**傳回 toohello 目前儀表板**，或切換 tooother 最近檢視： 使用 hello 下拉式功能表在左上方。</span><span class="sxs-lookup"><span data-stu-id="4662a-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="4662a-118">**切換儀表板**： 使用 hello 下拉式功能表 hello 儀表板標題</span><span class="sxs-lookup"><span data-stu-id="4662a-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="4662a-119">**建立、 編輯和共用儀表板**hello 儀表板工具列中。</span><span class="sxs-lookup"><span data-stu-id="4662a-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="4662a-120">**編輯 hello 儀表板**： 將滑鼠停留在磚，然後使用其上方列 toomove，自訂，或將它移除。</span><span class="sxs-lookup"><span data-stu-id="4662a-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="4662a-121">新增 tooa 儀表板</span><span class="sxs-lookup"><span data-stu-id="4662a-121">Add tooa dashboard</span></span>
<span data-ttu-id="4662a-122">如果您要尋找在刀鋒視窗或圖表的特別有趣的集合，您可以釘選一份 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="4662a-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="4662a-123">您將會在下次返回該處時見到它。</span><span class="sxs-lookup"><span data-stu-id="4662a-123">You'll see it next time you return there.</span></span>

![toopin 圖表中，將滑鼠停留，，然後按一下"…"hello 標頭中。](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="4662a-125">釘選圖表 toodashboard。</span><span class="sxs-lookup"><span data-stu-id="4662a-125">Pin chart toodashboard.</span></span> <span data-ttu-id="4662a-126">一份 hello 圖表會顯示 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="4662a-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="4662a-127">Pin hello 整個刀鋒視窗 toohello 儀表板-它會顯示 hello 儀表板上為您可以按一下磚。</span><span class="sxs-lookup"><span data-stu-id="4662a-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="4662a-128">按一下 hello 左上的角 tooreturn toohello 目前儀表板。</span><span class="sxs-lookup"><span data-stu-id="4662a-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="4662a-129">然後您可以使用 hello 下拉式功能表 tooreturn toohello 目前的檢視。</span><span class="sxs-lookup"><span data-stu-id="4662a-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="4662a-130">請注意，圖表會分組為圖格︰一個圖格中可包含多個圖表。</span><span class="sxs-lookup"><span data-stu-id="4662a-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="4662a-131">您釘選 hello 整個磚 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="4662a-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="4662a-132">hello 圖表會自動重新整理的頻率取決於 hello 圖表的時間範圍：</span><span class="sxs-lookup"><span data-stu-id="4662a-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="4662a-133">時間範圍向上 too1 小時： 重新整理每隔 5 分鐘</span><span class="sxs-lookup"><span data-stu-id="4662a-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="4662a-134">介於 1-24 小時的時間範圍：每隔 15 分鐘重新整理一次</span><span class="sxs-lookup"><span data-stu-id="4662a-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="4662a-135">超過 24 小時的時間範圍：(時間範圍)/60</span><span class="sxs-lookup"><span data-stu-id="4662a-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="4662a-136">在分析中釘選任何查詢</span><span class="sxs-lookup"><span data-stu-id="4662a-136">Pin any query in Analytics</span></span>
<span data-ttu-id="4662a-137">您也可以[釘選分析](app-insights-analytics-using.md#pin-to-dashboard)圖表 tooa[共用](#share-dashboards-with-your-team)儀表板。</span><span class="sxs-lookup"><span data-stu-id="4662a-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="4662a-138">這可讓您 tooadd 任何任意的查詢，連同 hello 標準度量的圖表。</span><span class="sxs-lookup"><span data-stu-id="4662a-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="4662a-139">系統會每小時自動重新計算結果。</span><span class="sxs-lookup"><span data-stu-id="4662a-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="4662a-140">立即按一下 hello 圖表 toorecalculate hello 重新整理圖示。</span><span class="sxs-lookup"><span data-stu-id="4662a-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="4662a-141">(瀏覽器重新整理並不會重新計算)。</span><span class="sxs-lookup"><span data-stu-id="4662a-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="4662a-142">調整 hello 儀表板上的磚</span><span class="sxs-lookup"><span data-stu-id="4662a-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="4662a-143">Hello 儀表板上並排顯示之後，您就可以進行調整。</span><span class="sxs-lookup"><span data-stu-id="4662a-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![將滑鼠停留在圖表中順序 tooedit 它。](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="4662a-145">新增圖表 toohello 磚。</span><span class="sxs-lookup"><span data-stu-id="4662a-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="4662a-146">設定 hello 公制，群組的維度和圖表的樣式 （表格、 圖形）。</span><span class="sxs-lookup"><span data-stu-id="4662a-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="4662a-147">拖曳橫跨 hello 圖表 toozoom按一下 hello 復原按鈕 tooreset hello timespan。hello 磚上設定 hello 圖表的篩選屬性。</span><span class="sxs-lookup"><span data-stu-id="4662a-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="4662a-148">設定圖格的標題。</span><span class="sxs-lookup"><span data-stu-id="4662a-148">Set tile title.</span></span>

<span data-ttu-id="4662a-149">從計量瀏覽器刀鋒釘選的圖格，編輯選項會比從 [概觀] 刀鋒視窗釘選的圖格多。</span><span class="sxs-lookup"><span data-stu-id="4662a-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="4662a-150">hello 原始您釘選的磚才不會受到您的編輯。</span><span class="sxs-lookup"><span data-stu-id="4662a-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="4662a-151">切換儀表板</span><span class="sxs-lookup"><span data-stu-id="4662a-151">Switch between dashboards</span></span>
<span data-ttu-id="4662a-152">您可以儲存多個儀表板並在之間進行切換。</span><span class="sxs-lookup"><span data-stu-id="4662a-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="4662a-153">當您釘選圖表或刀鋒視窗中時，這些被加入 toohello 目前儀表板。</span><span class="sxs-lookup"><span data-stu-id="4662a-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![tooswitch 之間儀表板，按一下儀表板，然後選取 已儲存的儀表板。](./media/app-insights-dashboards/32.png)

<span data-ttu-id="4662a-157">例如，您可能必須以全螢幕顯示 hello 小組室，和另一個用於一般開發中的一個儀表板。</span><span class="sxs-lookup"><span data-stu-id="4662a-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="4662a-158">Hello 儀表板，在刀鋒視窗會顯示為圖格： toogo toohello 刀鋒視窗中按一下它。</span><span class="sxs-lookup"><span data-stu-id="4662a-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="4662a-159">圖表會複寫其原始位置中的 hello 圖表。</span><span class="sxs-lookup"><span data-stu-id="4662a-159">A chart replicates hello chart in its original location.</span></span>

![按一下它所代表的磚 tooopen hello 刀鋒視窗](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="4662a-161">共用儀表板</span><span class="sxs-lookup"><span data-stu-id="4662a-161">Share dashboards</span></span>
<span data-ttu-id="4662a-162">建立儀表板之後，您可以與其他使用者共用它。</span><span class="sxs-lookup"><span data-stu-id="4662a-162">When you've created a dashboard, you can share it with other users.</span></span>

![在 hello 儀表板標題中，按一下 共用](./media/app-insights-dashboards/41.png)

<span data-ttu-id="4662a-164">深入了解 [角色和存取控制](app-insights-resources-roles-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="4662a-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="4662a-165">應用程式導覽</span><span class="sxs-lookup"><span data-stu-id="4662a-165">App navigation</span></span>
<span data-ttu-id="4662a-166">hello 概觀刀鋒視窗 hello 閘道 toomore 資訊是有關您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4662a-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="4662a-167">**任何圖表或圖格**-按一下任何磚或圖表 toosee 有關它會顯示其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4662a-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="4662a-168">概觀刀鋒視窗按鈕</span><span class="sxs-lookup"><span data-stu-id="4662a-168">Overview blade buttons</span></span>
![概觀刀鋒視窗頂端導覽列](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="4662a-170">[**計量瀏覽器**](app-insights-metrics-explorer.md) - 建立自己的效能和使用量圖表。</span><span class="sxs-lookup"><span data-stu-id="4662a-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="4662a-171">[**搜尋**](app-insights-diagnostic-search.md) - 調查事件的特定執行個體，例如要求、例外狀況或記錄檔案追蹤。</span><span class="sxs-lookup"><span data-stu-id="4662a-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="4662a-172">[**分析**](app-insights-analytics.md) - 遙測的強大查詢。</span><span class="sxs-lookup"><span data-stu-id="4662a-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="4662a-173">**時間範圍**-調整 hello hello 刀鋒視窗上的所有 hello 圖表所顯示的範圍。</span><span class="sxs-lookup"><span data-stu-id="4662a-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="4662a-174">**刪除**-刪除此應用程式的 hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="4662a-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="4662a-175">您應該也請移除您的應用程式程式碼中的 hello Application Insights 套件或編輯 hello[檢測金鑰](app-insights-create-new-resource.md#copy-the-instrumentation-key)在您的應用程式 toodirect 遙測 tooa 不同 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="4662a-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="4662a-176">Essentials 索引標籤</span><span class="sxs-lookup"><span data-stu-id="4662a-176">Essentials tab</span></span>
* <span data-ttu-id="4662a-177">[檢測金鑰](app-insights-create-new-resource.md#copy-the-instrumentation-key) - 識別此應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="4662a-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="4662a-178">價格 - 提供功能並設定磁碟區上限。</span><span class="sxs-lookup"><span data-stu-id="4662a-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="4662a-179">應用程式導覽列</span><span class="sxs-lookup"><span data-stu-id="4662a-179">App navigation bar</span></span>
![左導覽列](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="4662a-181">**概觀**-傳回 toohello 應用程式概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4662a-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="4662a-182">**活動記錄檔** - 警示與 Azure 系統管理事件。</span><span class="sxs-lookup"><span data-stu-id="4662a-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="4662a-183">[**存取控制**](app-insights-resources-roles-access-control.md) -提供存取 tooteam 成員等等。</span><span class="sxs-lookup"><span data-stu-id="4662a-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="4662a-184">[**標記**](../azure-resource-manager/resource-group-using-tags.md) -使用標記 toogroup 與其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="4662a-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="4662a-185">調查</span><span class="sxs-lookup"><span data-stu-id="4662a-185">INVESTIGATE</span></span>

* <span data-ttu-id="4662a-186">[**應用程式對應**](app-insights-app-map.md) -作用中的地圖顯示 hello 元件的應用程式時，衍生自 hello 相依性資訊。</span><span class="sxs-lookup"><span data-stu-id="4662a-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="4662a-187">[**智慧型偵測**](app-insights-proactive-diagnostics.md) - 檢閱最近的效能警示。</span><span class="sxs-lookup"><span data-stu-id="4662a-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="4662a-188">[**即時串流**](app-insights-live-stream.md) - 一組固定且幾近即時的計量，在部署新組建或偵錯時非常實用。</span><span class="sxs-lookup"><span data-stu-id="4662a-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="4662a-189">[**可用性 / Web 測試**](app-insights-monitor-web-app-availability.md) -傳送一般要求 tooyour web 應用程式從 hello world.* 周圍</span><span class="sxs-lookup"><span data-stu-id="4662a-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="4662a-190">[**失敗、 效能**](app-insights-web-monitor-performance.md) -例外狀況、 失敗率和回應時間要求 tooyour 應用程式和從您的應用程式的要求太[相依性](app-insights-asp-net-dependencies.md)。</span><span class="sxs-lookup"><span data-stu-id="4662a-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="4662a-191">[**效能**](app-insights-web-monitor-performance.md) - 回應時間、相依性回應時間。</span><span class="sxs-lookup"><span data-stu-id="4662a-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="4662a-192">[伺服器](app-insights-web-monitor-performance.md) - 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4662a-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="4662a-193">當您 [安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)時適用。</span><span class="sxs-lookup"><span data-stu-id="4662a-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="4662a-194">**瀏覽器** - 頁面檢視和 AJAX 效能。</span><span class="sxs-lookup"><span data-stu-id="4662a-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="4662a-195">當您 [檢測網頁](app-insights-javascript.md)時適用。</span><span class="sxs-lookup"><span data-stu-id="4662a-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="4662a-196">**使用量** - 頁面檢視、使用者和工作階段計數。</span><span class="sxs-lookup"><span data-stu-id="4662a-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="4662a-197">當您 [檢測網頁](app-insights-javascript.md)時適用。</span><span class="sxs-lookup"><span data-stu-id="4662a-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="4662a-198">設定</span><span class="sxs-lookup"><span data-stu-id="4662a-198">CONFIGURE</span></span>

* <span data-ttu-id="4662a-199">**開始使用** - 內嵌教學課程。</span><span class="sxs-lookup"><span data-stu-id="4662a-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="4662a-200">**屬性** - 檢測金鑰、訂用帳戶和資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="4662a-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="4662a-201">[警示](app-insights-alerts.md) - 計量警示組態。</span><span class="sxs-lookup"><span data-stu-id="4662a-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="4662a-202">[連續匯出](app-insights-export-telemetry.md)-設定匯出的遙測 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4662a-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="4662a-203">[效能測試](app-insights-monitor-web-app-availability.md#performance-tests) - 設定您的網站上的模擬負載。</span><span class="sxs-lookup"><span data-stu-id="4662a-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="4662a-204">[配額和價格](app-insights-pricing.md)和[擷取取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="4662a-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="4662a-205">**應用程式開發介面存取**-建立[版本註解](app-insights-annotations.md)和 hello 資料存取 API。</span><span class="sxs-lookup"><span data-stu-id="4662a-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="4662a-206">[**工作項目**](app-insights-diagnostic-search.md#create-work-item) -連接 tooa 工作追蹤系統，好讓您可以建立 bug 時檢查遙測。</span><span class="sxs-lookup"><span data-stu-id="4662a-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="4662a-207">設定</span><span class="sxs-lookup"><span data-stu-id="4662a-207">SETTINGS</span></span>

* <span data-ttu-id="4662a-208">[**鎖定**](../azure-resource-manager/resource-group-lock-resources.md) -鎖定 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="4662a-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="4662a-209">[**自動化指令碼**](app-insights-powershell.md) -匯出的 hello Azure 資源的定義，以便您可以將它當做範本 toocreate 新資源。</span><span class="sxs-lookup"><span data-stu-id="4662a-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="4662a-210">影片</span><span class="sxs-lookup"><span data-stu-id="4662a-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="4662a-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4662a-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="4662a-212">計量瀏覽器</span><span class="sxs-lookup"><span data-stu-id="4662a-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="4662a-213">篩選與分割計量</span><span class="sxs-lookup"><span data-stu-id="4662a-213">Filter and segment metrics</span></span> |![搜尋範例](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="4662a-215">診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="4662a-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="4662a-216">尋找和檢查事件、相關的事件，並建立 Bug</span><span class="sxs-lookup"><span data-stu-id="4662a-216">Find and inspect events, related events, and create bugs</span></span> |![搜尋範例](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="4662a-218">分析</span><span class="sxs-lookup"><span data-stu-id="4662a-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="4662a-219">功能強大的查詢語言</span><span class="sxs-lookup"><span data-stu-id="4662a-219">Powerful query language</span></span> |![搜尋範例](./media/app-insights-dashboards/63.png) |
