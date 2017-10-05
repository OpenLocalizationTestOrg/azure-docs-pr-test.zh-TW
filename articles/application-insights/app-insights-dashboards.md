---
title: "Azure Application Insights 中的儀表板與導覽 | Microsoft Docs"
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
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="355a4-103">Application Insights 入口網站中的導覽與儀表板</span><span class="sxs-lookup"><span data-stu-id="355a4-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="355a4-104">[在您的專案上設定 Application Insights](app-insights-overview.md) 之後，有關應用程式效能和使用情況的遙測資料會出現在 [Azure 入口網站](https://portal.azure.com)之專案的 Application Insights 資源中。</span><span class="sxs-lookup"><span data-stu-id="355a4-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="355a4-105">尋找遙測</span><span class="sxs-lookup"><span data-stu-id="355a4-105">Find your telemetry</span></span>
<span data-ttu-id="355a4-106">登入 [Azure 入口網站](https://portal.azure.com)，並瀏覽至您為應用程式建立的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="355a4-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![按一下 [瀏覽]，選取 [Application Insights]，然後選取您的應用程式。](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="355a4-108">應用程式的 [概觀] 刀鋒視窗 (頁面) 會顯示您應用程式的關鍵診斷資料，且為入口網站其他功能的閘道。</span><span class="sxs-lookup"><span data-stu-id="355a4-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![檢視您的遙測的主要路由](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="355a4-110">您可以自訂任何圖表和格線，並將它們釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="355a4-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="355a4-111">如此一來，您就可以在中央儀表板上結合來自不同應用程式的重要遙測資料。</span><span class="sxs-lookup"><span data-stu-id="355a4-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="355a4-112">儀表板</span><span class="sxs-lookup"><span data-stu-id="355a4-112">Dashboards</span></span>
<span data-ttu-id="355a4-113">您登入 [Microsoft Azure 入口網站](https://portal.azure.com) 之後最先看到的是儀表板。</span><span class="sxs-lookup"><span data-stu-id="355a4-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="355a4-114">您可以在這裡將所有 Azure 資源中對您最重要的圖表結合在一起，包括來自 [Azure Application Insights](app-insights-overview.md) 的遙測。</span><span class="sxs-lookup"><span data-stu-id="355a4-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![自訂的儀表板。](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="355a4-116">**瀏覽至特定資源**，例如 Application Insights 中您的應用程式︰使用左列。</span><span class="sxs-lookup"><span data-stu-id="355a4-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="355a4-117">**回到目前的儀表板**，或切換至其他最近的檢視：使用左上方的下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="355a4-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="355a4-118">**切換儀表板**︰使用儀表板標題上的下拉式功能表</span><span class="sxs-lookup"><span data-stu-id="355a4-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="355a4-119">在儀表板工具列中**建立、編輯和共用儀表板**。</span><span class="sxs-lookup"><span data-stu-id="355a4-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="355a4-120">**編輯儀表板**：將滑鼠停留在圖格上，然後使用其頂端列加以移動、自訂或移除。</span><span class="sxs-lookup"><span data-stu-id="355a4-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="355a4-121">加入儀表板中</span><span class="sxs-lookup"><span data-stu-id="355a4-121">Add to a dashboard</span></span>
<span data-ttu-id="355a4-122">當您尋找特別感興趣的刀鋒視窗或一組圖表時，您可將其釘選一份到儀表板。</span><span class="sxs-lookup"><span data-stu-id="355a4-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="355a4-123">您將會在下次返回該處時見到它。</span><span class="sxs-lookup"><span data-stu-id="355a4-123">You'll see it next time you return there.</span></span>

![若要釘選圖表，可將滑鼠停留在其上方，然後按一下標頭中的 [...]。](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="355a4-125">將圖表釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="355a4-125">Pin chart to dashboard.</span></span> <span data-ttu-id="355a4-126">圖表的複本會出現在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="355a4-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="355a4-127">將整個刀鋒視窗釘選到儀表板 - 它會在儀表板上顯示為圖格以供您點選。</span><span class="sxs-lookup"><span data-stu-id="355a4-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="355a4-128">按一下左上角以返回目前的儀表板。</span><span class="sxs-lookup"><span data-stu-id="355a4-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="355a4-129">然後您可以使用下拉式功能表，返回目前的檢視。</span><span class="sxs-lookup"><span data-stu-id="355a4-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="355a4-130">請注意，圖表會分組為圖格︰一個圖格中可包含多個圖表。</span><span class="sxs-lookup"><span data-stu-id="355a4-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="355a4-131">您將整個圖格釘選至儀表板。</span><span class="sxs-lookup"><span data-stu-id="355a4-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="355a4-132">圖表會以取決於圖表時間範圍的頻率自動重新整理：</span><span class="sxs-lookup"><span data-stu-id="355a4-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="355a4-133">長達 1 小時的時間範圍：每隔 5 分鐘重新整理一次</span><span class="sxs-lookup"><span data-stu-id="355a4-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="355a4-134">介於 1-24 小時的時間範圍：每隔 15 分鐘重新整理一次</span><span class="sxs-lookup"><span data-stu-id="355a4-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="355a4-135">超過 24 小時的時間範圍：(時間範圍)/60</span><span class="sxs-lookup"><span data-stu-id="355a4-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="355a4-136">在分析中釘選任何查詢</span><span class="sxs-lookup"><span data-stu-id="355a4-136">Pin any query in Analytics</span></span>
<span data-ttu-id="355a4-137">您也可以[釘選分析](app-insights-analytics-using.md#pin-to-dashboard)圖表到[共用](#share-dashboards-with-your-team)儀表板。</span><span class="sxs-lookup"><span data-stu-id="355a4-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="355a4-138">這可讓您新增任意查詢以及標準度量的圖表。</span><span class="sxs-lookup"><span data-stu-id="355a4-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="355a4-139">系統會每小時自動重新計算結果。</span><span class="sxs-lookup"><span data-stu-id="355a4-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="355a4-140">按一下圖表上的 [重新整理] 圖示，即可立即重新計算。</span><span class="sxs-lookup"><span data-stu-id="355a4-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="355a4-141">(瀏覽器重新整理並不會重新計算)。</span><span class="sxs-lookup"><span data-stu-id="355a4-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="355a4-142">調整儀表板上的圖格</span><span class="sxs-lookup"><span data-stu-id="355a4-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="355a4-143">圖格在儀表板上之後，您就可以進行調整。</span><span class="sxs-lookup"><span data-stu-id="355a4-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![暫留在一個圖表，以進行編輯。](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="355a4-145">將圖表加入圖格中。</span><span class="sxs-lookup"><span data-stu-id="355a4-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="355a4-146">設定度量、分組依據的維度，和圖表的樣式 (資料表、圖形)。</span><span class="sxs-lookup"><span data-stu-id="355a4-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="355a4-147">拖曳圖表加以放大；按一下 [復原] 按鈕來重設時間範圍；在圖格上設定圖表的篩選屬性。</span><span class="sxs-lookup"><span data-stu-id="355a4-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="355a4-148">設定圖格的標題。</span><span class="sxs-lookup"><span data-stu-id="355a4-148">Set tile title.</span></span>

<span data-ttu-id="355a4-149">從計量瀏覽器刀鋒釘選的圖格，編輯選項會比從 [概觀] 刀鋒視窗釘選的圖格多。</span><span class="sxs-lookup"><span data-stu-id="355a4-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="355a4-150">您釘選的原始圖格不會受到您的編輯影響。</span><span class="sxs-lookup"><span data-stu-id="355a4-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="355a4-151">切換儀表板</span><span class="sxs-lookup"><span data-stu-id="355a4-151">Switch between dashboards</span></span>
<span data-ttu-id="355a4-152">您可以儲存多個儀表板並在之間進行切換。</span><span class="sxs-lookup"><span data-stu-id="355a4-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="355a4-153">當您釘選圖表或刀鋒視窗時，即會將它們加入目前的儀表板。</span><span class="sxs-lookup"><span data-stu-id="355a4-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![若要在儀表板間進行切換，按一下 [儀表板]，然後選取已儲存的儀表板。](./media/app-insights-dashboards/32.png)

<span data-ttu-id="355a4-157">例如，您可能必須使用一個儀表板，在小組室中以全螢幕顯示，並使用另一個儀表板進行一般開發。</span><span class="sxs-lookup"><span data-stu-id="355a4-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="355a4-158">在儀表板上，刀鋒視窗會顯示為磚：按一下即可移至刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="355a4-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="355a4-159">圖表會複製其原始位置中的圖表。</span><span class="sxs-lookup"><span data-stu-id="355a4-159">A chart replicates the chart in its original location.</span></span>

![按一下圖格以開啟它所代表的刀鋒視窗](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="355a4-161">共用儀表板</span><span class="sxs-lookup"><span data-stu-id="355a4-161">Share dashboards</span></span>
<span data-ttu-id="355a4-162">建立儀表板之後，您可以與其他使用者共用它。</span><span class="sxs-lookup"><span data-stu-id="355a4-162">When you've created a dashboard, you can share it with other users.</span></span>

![在儀表板標題中按一下 [共用]](./media/app-insights-dashboards/41.png)

<span data-ttu-id="355a4-164">深入了解 [角色和存取控制](app-insights-resources-roles-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="355a4-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="355a4-165">應用程式導覽</span><span class="sxs-lookup"><span data-stu-id="355a4-165">App navigation</span></span>
<span data-ttu-id="355a4-166">概觀刀鋒視窗是您的應用程式詳細資訊的閘道。</span><span class="sxs-lookup"><span data-stu-id="355a4-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="355a4-167">**任何圖表或圖格** - 按一下任何圖格或圖表，以查看更多關於其顯示內容的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="355a4-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="355a4-168">概觀刀鋒視窗按鈕</span><span class="sxs-lookup"><span data-stu-id="355a4-168">Overview blade buttons</span></span>
![概觀刀鋒視窗頂端導覽列](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="355a4-170">[**計量瀏覽器**](app-insights-metrics-explorer.md) - 建立自己的效能和使用量圖表。</span><span class="sxs-lookup"><span data-stu-id="355a4-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="355a4-171">[**搜尋**](app-insights-diagnostic-search.md) - 調查事件的特定執行個體，例如要求、例外狀況或記錄檔案追蹤。</span><span class="sxs-lookup"><span data-stu-id="355a4-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="355a4-172">[**分析**](app-insights-analytics.md) - 遙測的強大查詢。</span><span class="sxs-lookup"><span data-stu-id="355a4-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="355a4-173">**時間範圍** - 調整刀鋒視窗上所有圖表所顯示的範圍。</span><span class="sxs-lookup"><span data-stu-id="355a4-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="355a4-174">**刪除** - 刪除此應用程式的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="355a4-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="355a4-175">您應該也從您的應用程式程式碼中移除 Application Insights 套件，或編輯您應用程式中的[檢測金鑰](app-insights-create-new-resource.md#copy-the-instrumentation-key)，將遙測導向至不同的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="355a4-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="355a4-176">Essentials 索引標籤</span><span class="sxs-lookup"><span data-stu-id="355a4-176">Essentials tab</span></span>
* <span data-ttu-id="355a4-177">[檢測金鑰](app-insights-create-new-resource.md#copy-the-instrumentation-key) - 識別此應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="355a4-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="355a4-178">價格 - 提供功能並設定磁碟區上限。</span><span class="sxs-lookup"><span data-stu-id="355a4-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="355a4-179">應用程式導覽列</span><span class="sxs-lookup"><span data-stu-id="355a4-179">App navigation bar</span></span>
![左導覽列](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="355a4-181">**概觀** - 返回應用程式概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="355a4-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="355a4-182">**活動記錄檔** - 警示與 Azure 系統管理事件。</span><span class="sxs-lookup"><span data-stu-id="355a4-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="355a4-183">[**存取控制**](app-insights-resources-roles-access-control.md) - 將存取權提供給小組成員和其他人。</span><span class="sxs-lookup"><span data-stu-id="355a4-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="355a4-184">[**標籤**](../azure-resource-manager/resource-group-using-tags.md) - 使用標籤將您的應用程式與其他應用程式分組。</span><span class="sxs-lookup"><span data-stu-id="355a4-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="355a4-185">調查</span><span class="sxs-lookup"><span data-stu-id="355a4-185">INVESTIGATE</span></span>

* <span data-ttu-id="355a4-186">[**應用程式對應**](app-insights-app-map.md) - 顯示應用程式元件的使用中對應，其衍生自相依性資訊。</span><span class="sxs-lookup"><span data-stu-id="355a4-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="355a4-187">[**智慧型偵測**](app-insights-proactive-diagnostics.md) - 檢閱最近的效能警示。</span><span class="sxs-lookup"><span data-stu-id="355a4-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="355a4-188">[**即時串流**](app-insights-live-stream.md) - 一組固定且幾近即時的計量，在部署新組建或偵錯時非常實用。</span><span class="sxs-lookup"><span data-stu-id="355a4-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="355a4-189">[**可用性 / Web 測試**](app-insights-monitor-web-app-availability.md) - 從世界各地將一般要求傳送至您的 Web 應用程式。*</span><span class="sxs-lookup"><span data-stu-id="355a4-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="355a4-190">[**失敗、效能**](app-insights-web-monitor-performance.md) - 對您的應用程式提出的要求和您的應用程式對[相依項目](app-insights-asp-net-dependencies.md)提出的要求，其例外狀況、失敗率和回應時間。</span><span class="sxs-lookup"><span data-stu-id="355a4-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="355a4-191">[**效能**](app-insights-web-monitor-performance.md) - 回應時間、相依性回應時間。</span><span class="sxs-lookup"><span data-stu-id="355a4-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="355a4-192">[伺服器](app-insights-web-monitor-performance.md) - 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="355a4-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="355a4-193">當您 [安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)時適用。</span><span class="sxs-lookup"><span data-stu-id="355a4-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="355a4-194">**瀏覽器** - 頁面檢視和 AJAX 效能。</span><span class="sxs-lookup"><span data-stu-id="355a4-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="355a4-195">當您 [檢測網頁](app-insights-javascript.md)時適用。</span><span class="sxs-lookup"><span data-stu-id="355a4-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="355a4-196">**使用量** - 頁面檢視、使用者和工作階段計數。</span><span class="sxs-lookup"><span data-stu-id="355a4-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="355a4-197">當您 [檢測網頁](app-insights-javascript.md)時適用。</span><span class="sxs-lookup"><span data-stu-id="355a4-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="355a4-198">設定</span><span class="sxs-lookup"><span data-stu-id="355a4-198">CONFIGURE</span></span>

* <span data-ttu-id="355a4-199">**開始使用** - 內嵌教學課程。</span><span class="sxs-lookup"><span data-stu-id="355a4-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="355a4-200">**屬性** - 檢測金鑰、訂用帳戶和資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="355a4-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="355a4-201">[警示](app-insights-alerts.md) - 計量警示組態。</span><span class="sxs-lookup"><span data-stu-id="355a4-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="355a4-202">[連續匯出](app-insights-export-telemetry.md) - 設定將遙測匯出至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="355a4-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="355a4-203">[效能測試](app-insights-monitor-web-app-availability.md#performance-tests) - 設定您的網站上的模擬負載。</span><span class="sxs-lookup"><span data-stu-id="355a4-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="355a4-204">[配額和價格](app-insights-pricing.md)和[擷取取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="355a4-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="355a4-205">**API 存取** - 建立[版本註解](app-insights-annotations.md)以及資料存取 API。</span><span class="sxs-lookup"><span data-stu-id="355a4-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="355a4-206">[**工作項目**](app-insights-diagnostic-search.md#create-work-item) - 連線到工作追蹤系統，讓您可以在檢查遙測時建立 Bug。</span><span class="sxs-lookup"><span data-stu-id="355a4-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="355a4-207">設定</span><span class="sxs-lookup"><span data-stu-id="355a4-207">SETTINGS</span></span>

* <span data-ttu-id="355a4-208">[**鎖定**](../azure-resource-manager/resource-group-lock-resources.md) -鎖定 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="355a4-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="355a4-209">[**自動化指令碼**](app-insights-powershell.md) - 匯出 Azure 資源的定義，如此您就能用其做為範本來建立新資源。</span><span class="sxs-lookup"><span data-stu-id="355a4-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="355a4-210">影片</span><span class="sxs-lookup"><span data-stu-id="355a4-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="355a4-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="355a4-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="355a4-212">計量瀏覽器</span><span class="sxs-lookup"><span data-stu-id="355a4-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="355a4-213">篩選與分割計量</span><span class="sxs-lookup"><span data-stu-id="355a4-213">Filter and segment metrics</span></span> |![搜尋範例](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="355a4-215">診斷搜尋</span><span class="sxs-lookup"><span data-stu-id="355a4-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="355a4-216">尋找和檢查事件、相關的事件，並建立 Bug</span><span class="sxs-lookup"><span data-stu-id="355a4-216">Find and inspect events, related events, and create bugs</span></span> |![搜尋範例](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="355a4-218">分析</span><span class="sxs-lookup"><span data-stu-id="355a4-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="355a4-219">功能強大的查詢語言</span><span class="sxs-lookup"><span data-stu-id="355a4-219">Powerful query language</span></span> |![搜尋範例](./media/app-insights-dashboards/63.png) |
