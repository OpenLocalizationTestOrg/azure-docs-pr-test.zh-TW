---
title: "aaaApplication Azure Application Insights 中的對應 |Microsoft 文件"
description: "Hello 應用程式元件之間的相依性的視覺化呈現方式標示 Kpi 和警示。"
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="a6f8d-103">Application Insights 的應用程式對應</span><span class="sxs-lookup"><span data-stu-id="a6f8d-103">Application Map in Application Insights</span></span>
<span data-ttu-id="a6f8d-104">在[Azure Application Insights](app-insights-overview.md)，應用程式對應為 visual hello 相依性關聯性的應用程式元件的版面配置。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="a6f8d-105">每個元件顯示 Kpi toohelp 負載、 效能、 失敗和警示，例如您找出任何造成效能問題或失敗的元件。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="a6f8d-106">您可以按一下任何元件 toomore 從詳細的診斷，例如 Application Insights 事件。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="a6f8d-107">如果您的應用程式使用 Azure 服務，您也可以按一下透過 tooAzure 診斷，例如 SQL Database Advisor 的建議。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="a6f8d-108">類似其他圖表中，您可以釘選的應用程式對應 toohello Azure 儀表板，可完整運作。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="a6f8d-109">開啟 hello 應用程式對應</span><span class="sxs-lookup"><span data-stu-id="a6f8d-109">Open hello application map</span></span>
<span data-ttu-id="a6f8d-110">從您的應用程式的 hello 概觀刀鋒視窗開啟 hello 對應：</span><span class="sxs-lookup"><span data-stu-id="a6f8d-110">Open hello map from hello overview blade for your application:</span></span>

![開啟應用程式對應](./media/app-insights-app-map/01.png)

![應用程式對應](./media/app-insights-app-map/02.png)

<span data-ttu-id="a6f8d-113">hello 對應可顯示：</span><span class="sxs-lookup"><span data-stu-id="a6f8d-113">hello map shows:</span></span>

* <span data-ttu-id="a6f8d-114">可用性集合</span><span class="sxs-lookup"><span data-stu-id="a6f8d-114">Availability tests</span></span>
* <span data-ttu-id="a6f8d-115">用戶端元件 （使用 JavaScript SDK hello 監視）</span><span class="sxs-lookup"><span data-stu-id="a6f8d-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="a6f8d-116">伺服器端元件</span><span class="sxs-lookup"><span data-stu-id="a6f8d-116">Server-side component</span></span>
* <span data-ttu-id="a6f8d-117">Hello 用戶端和伺服器元件的相依性</span><span class="sxs-lookup"><span data-stu-id="a6f8d-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="a6f8d-118">您可以展開與摺疊相依性連結群組︰</span><span class="sxs-lookup"><span data-stu-id="a6f8d-118">You can expand and collapse dependency link groups:</span></span>

![摺疊](./media/app-insights-app-map/03.png)

<span data-ttu-id="a6f8d-120">如果您有某種類型 (SQL、HTTP 等) 的許多相依性，它們可能會以群組方式出現。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![群組的相依性](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="a6f8d-122">找出問題</span><span class="sxs-lookup"><span data-stu-id="a6f8d-122">Spot problems</span></span>
<span data-ttu-id="a6f8d-123">每個節點都有相關的效能指標，例如 hello 負載、 效能和失敗率，該元件。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="a6f8d-124">警告圖示會點出可能的問題。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="a6f8d-125">橘色的警告表示要求、頁面檢視或相依性呼叫發生失敗。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="a6f8d-126">紅色表示失敗率大於 5 %。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="a6f8d-127">如果您想 tooadjust 這些閾值，請開啟 [選項]。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-127">If you want tooadjust these thresholds, open Options.</span></span>

![失敗圖示](./media/app-insights-app-map/04.png)

<span data-ttu-id="a6f8d-129">也會出現作用中警示︰</span><span class="sxs-lookup"><span data-stu-id="a6f8d-129">Active alerts also show up:</span></span> 

![作用中警示](./media/app-insights-app-map/05.png)

<span data-ttu-id="a6f8d-131">如果您使用 SQL Azure，當系統有如何改善效能的建議時，便會出現圖示。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Azure 建議](./media/app-insights-app-map/06.png)

<span data-ttu-id="a6f8d-133">按一下任何圖示 tooget 更多詳細資料：</span><span class="sxs-lookup"><span data-stu-id="a6f8d-133">Click any icon tooget more details:</span></span>

![Azure 建議](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="a6f8d-135">診斷點選連結</span><span class="sxs-lookup"><span data-stu-id="a6f8d-135">Diagnostic click through</span></span>
<span data-ttu-id="a6f8d-136">每一個 hello 節點 hello 地圖上提供目標的點選連結，以診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="a6f8d-137">hello 選項 hello hello 節點類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-137">hello options vary depending on hello type of hello node.</span></span>

![伺服器選項](./media/app-insights-app-map/09.png)

<span data-ttu-id="a6f8d-139">Azure 中主控的元件，hello 選項包括 toothem 直接連結。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="a6f8d-140">篩選和時間範圍</span><span class="sxs-lookup"><span data-stu-id="a6f8d-140">Filters and time range</span></span>
<span data-ttu-id="a6f8d-141">根據預設，hello 對應摘要說明可用的 hello 選擇時間範圍內的所有 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="a6f8d-142">但是，可以先篩選 tooinclude 只在特定作業名稱或相依性。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="a6f8d-143">作業名稱︰這包括頁面檢視和伺服器端要求類型。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="a6f8d-144">使用此選項，hello 地圖顯示 hello hello 只 hello 選取作業的伺服器/用戶端節點上的 KPI。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="a6f8d-145">它會顯示在這些特定作業的 hello 內容中呼叫 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="a6f8d-146">相依性的主檔名： 這包括 hello AJAX 瀏覽器的相依性和伺服器端的相依性。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="a6f8d-147">如果您要報告自訂相依性遙測，以 hello TrackDependency API，它們也出現在這裡。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="a6f8d-148">您可以選取 hello 相依性 tooshow hello 地圖上。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="a6f8d-149">目前這個選項不會篩選 hello 伺服器端要求或 hello 用戶端的分頁檢視。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![設定篩選](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="a6f8d-151">儲存篩選</span><span class="sxs-lookup"><span data-stu-id="a6f8d-151">Save filters</span></span>
<span data-ttu-id="a6f8d-152">toosave hello 篩選已套用，針 hello 篩選過的檢視拖曳至[儀表板](app-insights-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Pin toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="a6f8d-154">錯誤窗格</span><span class="sxs-lookup"><span data-stu-id="a6f8d-154">Error pane</span></span>
<span data-ttu-id="a6f8d-155">當您按一下 hello map 中的節點時，錯誤窗格會顯示在 hello 彙總失敗，該節點的右側。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="a6f8d-156">失敗會先依作業識別碼群組，然後再依問題識別碼群組。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![錯誤窗格](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="a6f8d-158">按一下 上失敗，會在 toohello 發生失敗的最新執行個體。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="a6f8d-159">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="a6f8d-159">Resource health</span></span>
<span data-ttu-id="a6f8d-160">對於某些資源類型，資源健全狀況會顯示在 hello hello 錯誤窗格頂端。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="a6f8d-161">例如，按一下 [SQL] 節點會顯示 hello 資料庫健康狀態與任何已引發的警示。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![資源健康情況](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="a6f8d-163">您可以按一下 hello 資源名稱 tooview 標準概觀度量該資源。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="a6f8d-164">端對端系統應用程式對應</span><span class="sxs-lookup"><span data-stu-id="a6f8d-164">End-to-end system app maps</span></span>

<span data-ttu-id="a6f8d-165">*需要 SDK 2.3 版或更新版本*</span><span class="sxs-lookup"><span data-stu-id="a6f8d-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="a6f8d-166">如果您的應用程式具有數個元件-例如後, 端服務此外 toohello web 應用程式層，則您可以顯示所有在一個整合式應用程式對應。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![設定篩選](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="a6f8d-168">hello 應用程式對應尋找遵循以 hello Application Insights SDK 安裝的伺服器之間進行的任何 HTTP 相依性呼叫的伺服器節點。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="a6f8d-169">每個 Application Insights 資源會假設 toocontain 一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="a6f8d-170">多角色應用程式對應 (預覽)</span><span class="sxs-lookup"><span data-stu-id="a6f8d-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="a6f8d-171">hello 預覽多角色應用程式對應功能可讓您 toouse hello 應用程式對應具有多個伺服器傳送資料 toohello 相同的 Application Insights 資源 / 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="a6f8d-172">Hello 對應中的伺服器分散 hello cloud_RoleName 屬性遙測項目上。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="a6f8d-173">設定*多角色應用程式對應*太*上*從 hello 預覽刀鋒視窗 tooenable 這項設定。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="a6f8d-174">在微服務應用程式，或在其他案例中，您 toocorrelate 事件在單一的 Application Insights 資源內的多部伺服器，可能需要這種方法。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="a6f8d-175">影片</span><span class="sxs-lookup"><span data-stu-id="a6f8d-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="a6f8d-176">意見反應</span><span class="sxs-lookup"><span data-stu-id="a6f8d-176">Feedback</span></span>
<span data-ttu-id="a6f8d-177">請透過提供意見反應 hello 入口網站的意見反應 選項。</span><span class="sxs-lookup"><span data-stu-id="a6f8d-177">Please provide feedback through hello portal feedback option.</span></span>

![MapLink-1 影像](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="a6f8d-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6f8d-179">Next steps</span></span>

* [<span data-ttu-id="a6f8d-180">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a6f8d-180">Azure portal</span></span>](https://portal.azure.com)
