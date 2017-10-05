---
title: "Azure Application Insights 的應用程式對應 | Microsoft Docs"
description: "應用程式元件之間的相依性視覺化呈現方式，其中會標示 KPI 和警示。"
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
ms.openlocfilehash: 207526b7a675f92134d045ebefb9a372749bce92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="adf12-103">Application Insights 的應用程式對應</span><span class="sxs-lookup"><span data-stu-id="adf12-103">Application Map in Application Insights</span></span>
<span data-ttu-id="adf12-104">在 [Azure Application Insights](app-insights-overview.md) 中，應用程式對應是應用程式元件相依性關係的視覺化版面配置。</span><span class="sxs-lookup"><span data-stu-id="adf12-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of the dependency relationships of your application components.</span></span> <span data-ttu-id="adf12-105">每個元件都會顯示負載、效能、失敗和警示等 KPI，以協助您找出任何造成效能問題或失敗的元件。</span><span class="sxs-lookup"><span data-stu-id="adf12-105">Each component shows KPIs such as load, performance, failures, and alerts, to help you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="adf12-106">您可以從任何元件逐一點選至更詳細的診斷，例如 Application Insights 事件。</span><span class="sxs-lookup"><span data-stu-id="adf12-106">You can click through from any component to more detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="adf12-107">如果您的應用程式使用 Azure 服務，您也可以逐一點選 Azure 診斷，例如 SQL 資料庫建議程式的建議。</span><span class="sxs-lookup"><span data-stu-id="adf12-107">If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="adf12-108">和其他圖表一樣，您可以將應用程式對應釘選至 Azure 儀表板，而其功能仍可完整運作。</span><span class="sxs-lookup"><span data-stu-id="adf12-108">Like other charts, you can pin an application map to the Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-the-application-map"></a><span data-ttu-id="adf12-109">開啟應用程式對應</span><span class="sxs-lookup"><span data-stu-id="adf12-109">Open the application map</span></span>
<span data-ttu-id="adf12-110">從應用程式的概觀刀鋒視窗中開啟對應︰</span><span class="sxs-lookup"><span data-stu-id="adf12-110">Open the map from the overview blade for your application:</span></span>

![開啟應用程式對應](./media/app-insights-app-map/01.png)

![應用程式對應](./media/app-insights-app-map/02.png)

<span data-ttu-id="adf12-113">此對應會顯示︰</span><span class="sxs-lookup"><span data-stu-id="adf12-113">The map shows:</span></span>

* <span data-ttu-id="adf12-114">可用性集合</span><span class="sxs-lookup"><span data-stu-id="adf12-114">Availability tests</span></span>
* <span data-ttu-id="adf12-115">用戶端元件 (使用 JavaScript SDK 監視)</span><span class="sxs-lookup"><span data-stu-id="adf12-115">Client-side component (monitored with the JavaScript SDK)</span></span>
* <span data-ttu-id="adf12-116">伺服器端元件</span><span class="sxs-lookup"><span data-stu-id="adf12-116">Server-side component</span></span>
* <span data-ttu-id="adf12-117">用戶端和伺服器元件的相依性</span><span class="sxs-lookup"><span data-stu-id="adf12-117">Dependencies of the client and server components</span></span>

<span data-ttu-id="adf12-118">您可以展開與摺疊相依性連結群組︰</span><span class="sxs-lookup"><span data-stu-id="adf12-118">You can expand and collapse dependency link groups:</span></span>

![摺疊](./media/app-insights-app-map/03.png)

<span data-ttu-id="adf12-120">如果您有某種類型 (SQL、HTTP 等) 的許多相依性，它們可能會以群組方式出現。</span><span class="sxs-lookup"><span data-stu-id="adf12-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![群組的相依性](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="adf12-122">找出問題</span><span class="sxs-lookup"><span data-stu-id="adf12-122">Spot problems</span></span>
<span data-ttu-id="adf12-123">每個節點都有相關的效能指標，例如該元件的負載、效能和失敗率。</span><span class="sxs-lookup"><span data-stu-id="adf12-123">Each node has relevant performance indicators, such as the load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="adf12-124">警告圖示會點出可能的問題。</span><span class="sxs-lookup"><span data-stu-id="adf12-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="adf12-125">橘色的警告表示要求、頁面檢視或相依性呼叫發生失敗。</span><span class="sxs-lookup"><span data-stu-id="adf12-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="adf12-126">紅色表示失敗率大於 5 %。</span><span class="sxs-lookup"><span data-stu-id="adf12-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="adf12-127">如果您想要調整這些閾值，請開啟 [選項]。</span><span class="sxs-lookup"><span data-stu-id="adf12-127">If you want to adjust these thresholds, open Options.</span></span>

![失敗圖示](./media/app-insights-app-map/04.png)

<span data-ttu-id="adf12-129">也會出現作用中警示︰</span><span class="sxs-lookup"><span data-stu-id="adf12-129">Active alerts also show up:</span></span> 

![作用中警示](./media/app-insights-app-map/05.png)

<span data-ttu-id="adf12-131">如果您使用 SQL Azure，當系統有如何改善效能的建議時，便會出現圖示。</span><span class="sxs-lookup"><span data-stu-id="adf12-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Azure 建議](./media/app-insights-app-map/06.png)

<span data-ttu-id="adf12-133">按一下任何圖示即可取得詳細資料：</span><span class="sxs-lookup"><span data-stu-id="adf12-133">Click any icon to get more details:</span></span>

![Azure 建議](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="adf12-135">診斷點選連結</span><span class="sxs-lookup"><span data-stu-id="adf12-135">Diagnostic click through</span></span>
<span data-ttu-id="adf12-136">對應上的每個節點都會提供以診斷做為目標的點選連結。</span><span class="sxs-lookup"><span data-stu-id="adf12-136">Each of the nodes on the map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="adf12-137">這些選項會隨節點類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="adf12-137">The options vary depending on the type of the node.</span></span>

![伺服器選項](./media/app-insights-app-map/09.png)

<span data-ttu-id="adf12-139">對於裝載在 Azure 中的元件，這些選項包括元件的直接連結。</span><span class="sxs-lookup"><span data-stu-id="adf12-139">For components that are hosted in Azure, the options include direct links to them.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="adf12-140">篩選和時間範圍</span><span class="sxs-lookup"><span data-stu-id="adf12-140">Filters and time range</span></span>
<span data-ttu-id="adf12-141">根據預設，對應中會摘要列出選定時間範圍內的所有可用資料。</span><span class="sxs-lookup"><span data-stu-id="adf12-141">By default, the map summarizes all the data available for the chosen time range.</span></span> <span data-ttu-id="adf12-142">但是，您可以透過篩選，使其只包含特定作業名稱或相依性。</span><span class="sxs-lookup"><span data-stu-id="adf12-142">But you can filter it to include only specific operation names or dependencies.</span></span>

* <span data-ttu-id="adf12-143">作業名稱︰這包括頁面檢視和伺服器端要求類型。</span><span class="sxs-lookup"><span data-stu-id="adf12-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="adf12-144">使用此選項時，對應中只會顯示伺服器端/用戶端節點上所選作業的 KPI。</span><span class="sxs-lookup"><span data-stu-id="adf12-144">With this option, the map shows the KPI on the server/client-side node for the selected operations only.</span></span> <span data-ttu-id="adf12-145">它會顯示在這些特定作業內容中呼叫的相依性。</span><span class="sxs-lookup"><span data-stu-id="adf12-145">It shows the dependencies called in the context of those specific operations.</span></span>
* <span data-ttu-id="adf12-146">相依性基底名稱︰這包括 AJAX 瀏覽器相依性和伺服器端相依性。</span><span class="sxs-lookup"><span data-stu-id="adf12-146">Dependency base name: This includes the AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="adf12-147">如果您使用 TrackDependency API 來報告自訂相依性遙測，這些資料也會在此出現。</span><span class="sxs-lookup"><span data-stu-id="adf12-147">If you report custom dependency telemetry with the TrackDependency API, they also appear here.</span></span> <span data-ttu-id="adf12-148">您可以選取要顯示在對應中的相依性。</span><span class="sxs-lookup"><span data-stu-id="adf12-148">You can select the dependencies to show on the map.</span></span> <span data-ttu-id="adf12-149">此選取項目目前不會篩選伺服器端要求或用戶端頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="adf12-149">Currently this selection does not filter the server-side requests, or the client-side page views.</span></span>

![設定篩選](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="adf12-151">儲存篩選</span><span class="sxs-lookup"><span data-stu-id="adf12-151">Save filters</span></span>
<span data-ttu-id="adf12-152">若要儲存您已套用的篩選，請將篩選後的檢視釘選到 [儀表板](app-insights-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="adf12-152">To save the filters you have applied, pin the filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![釘選到儀表板](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="adf12-154">錯誤窗格</span><span class="sxs-lookup"><span data-stu-id="adf12-154">Error pane</span></span>
<span data-ttu-id="adf12-155">當您按一下對應中的節點時，會在右側顯示錯誤窗格，將該節點的失敗進行彙總。</span><span class="sxs-lookup"><span data-stu-id="adf12-155">When you click a node in the map, an error pane is displayed on the right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="adf12-156">失敗會先依作業識別碼群組，然後再依問題識別碼群組。</span><span class="sxs-lookup"><span data-stu-id="adf12-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![錯誤窗格](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="adf12-158">按一下失敗可前往該失敗的最新範例。</span><span class="sxs-lookup"><span data-stu-id="adf12-158">Clicking on a failure takes you to the most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="adf12-159">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="adf12-159">Resource health</span></span>
<span data-ttu-id="adf12-160">對於某些資源類型，資源健康狀態會顯示在 [錯誤] 窗格的頂端。</span><span class="sxs-lookup"><span data-stu-id="adf12-160">For some resource types, resource health is displayed at the top of the error pane.</span></span> <span data-ttu-id="adf12-161">例如，按一下 SQL 節點會顯示資料庫的健康狀態和所發出的任何警示。</span><span class="sxs-lookup"><span data-stu-id="adf12-161">For example, clicking a SQL node will show the database health and any alerts that have fired.</span></span>

![資源健康情況](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="adf12-163">您可以按一下資源名稱來檢視該資源的標準概觀計量。</span><span class="sxs-lookup"><span data-stu-id="adf12-163">You can click the resource name to view standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="adf12-164">端對端系統應用程式對應</span><span class="sxs-lookup"><span data-stu-id="adf12-164">End-to-end system app maps</span></span>

<span data-ttu-id="adf12-165">*需要 SDK 2.3 版或更新版本*</span><span class="sxs-lookup"><span data-stu-id="adf12-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="adf12-166">如果您的應用程式有多個元件 (例如 Web 應用程式以外的後端服務)，則可以在一個整合式應用程式對應上顯示所有元件。</span><span class="sxs-lookup"><span data-stu-id="adf12-166">If your application has several components - for example, a back-end service in addition to the web app - then you can show them all on one integrated app map.</span></span>

![設定篩選](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="adf12-168">應用程式對應會尋找伺服器節點，方法是遵循已安裝 Application Insights SDK 的伺服器之間所發出的任何 HTTP 相依性呼叫。</span><span class="sxs-lookup"><span data-stu-id="adf12-168">The app map finds server nodes by following any HTTP dependency calls made between servers with the Application Insights SDK installed.</span></span> <span data-ttu-id="adf12-169">會假設每個 Application Insights 資源都包含一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="adf12-169">Each Application Insights resource is assumed to contain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="adf12-170">多角色應用程式對應 (預覽)</span><span class="sxs-lookup"><span data-stu-id="adf12-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="adf12-171">預覽多角色應用程式對應功能可讓您使用應用程式對應搭配多部伺服器，將資料傳送至相同的 Application Insights  / 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="adf12-171">The preview multi-role app map feature allows you to use the app map with multiple servers sending data to the same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="adf12-172">對應中的伺服器會依遙測項目上的 cloud_RoleName 屬性進行區隔。</span><span class="sxs-lookup"><span data-stu-id="adf12-172">Servers in the map are segmented by the cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="adf12-173">從 [預覽] 刀鋒視窗將 [多角色應用程式對應]設為 [開啟]，可啟用這項設定。</span><span class="sxs-lookup"><span data-stu-id="adf12-173">Set *Multi-role Application Map* to *On* from the Previews blade to enable this configuration.</span></span>

<span data-ttu-id="adf12-174">在微服務應用程式，或在您要於單一 Application Insights 資源內將多部伺服器之間的事件相互關聯的其他情況下，可能需要這種方法。</span><span class="sxs-lookup"><span data-stu-id="adf12-174">This approach may be desired in a micro-services application, or in other scenarios where you want to correlate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="adf12-175">影片</span><span class="sxs-lookup"><span data-stu-id="adf12-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="adf12-176">意見反應</span><span class="sxs-lookup"><span data-stu-id="adf12-176">Feedback</span></span>
<span data-ttu-id="adf12-177">請透過入口網站的意見反應選項提供意見反應。</span><span class="sxs-lookup"><span data-stu-id="adf12-177">Please provide feedback through the portal feedback option.</span></span>

![MapLink-1 影像](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="adf12-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="adf12-179">Next steps</span></span>

* [<span data-ttu-id="adf12-180">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="adf12-180">Azure portal</span></span>](https://portal.azure.com)
