---
title: "檢視 Azure Web Apps 分析資料 | Microsoft Docs"
description: "您可以使用 Azure Web Apps 分析解決方案在所有 Azure Web 應用程式資源之間收集不同的計量，以深入了解 Azure Web 應用程式。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: f480188c46f16473bf294c857cd07e3cec5dc0ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a><span data-ttu-id="2a5e2-103">檢視所有 Azure Web 應用程式資源之間的計量分析資料</span><span class="sxs-lookup"><span data-stu-id="2a5e2-103">View analytic data for metrics across all your Azure Web App resources</span></span>

<span data-ttu-id="2a5e2-104">![Web Apps 符號](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)</span><span class="sxs-lookup"><span data-stu-id="2a5e2-104">![Web Apps symbol](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)</span></span>  
<span data-ttu-id="2a5e2-105">Azure Web Apps 分析 (預覽) 解決方案會收集所有 Azure Web 應用程式資源之間的不同計量，以深入了解 [Azure Web Apps](../app-service-web/app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-105">The Azure Web Apps Analytics (Preview) solution provides insights into your [Azure Web Apps](../app-service-web/app-service-web-overview.md) by collecting different metrics across all your Azure Web App resources.</span></span> <span data-ttu-id="2a5e2-106">透過此解決方案，您可以分析與搜尋 Web 應用程式資源計量資料。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-106">With the solution, you can analyze and search for web app resource metric data.</span></span>

<span data-ttu-id="2a5e2-107">使用此解決方案，您可以檢視：</span><span class="sxs-lookup"><span data-stu-id="2a5e2-107">Using the solution, you can view the:</span></span>

- <span data-ttu-id="2a5e2-108">回應時間最長的 Web Apps 排行榜</span><span class="sxs-lookup"><span data-stu-id="2a5e2-108">Top Web Apps with the highest response time</span></span>
- <span data-ttu-id="2a5e2-109">整個 Web Apps 間的要求數，包括成功與失敗的要求</span><span class="sxs-lookup"><span data-stu-id="2a5e2-109">Number of requests across your Web Apps, including successful and failed requests</span></span>
- <span data-ttu-id="2a5e2-110">傳入和傳出流量最高的 Web Apps 排行榜</span><span class="sxs-lookup"><span data-stu-id="2a5e2-110">Top Web Apps with highest incoming and outgoing traffic</span></span>
- <span data-ttu-id="2a5e2-111">CPU 與記憶體使用率最高的服務方案排行榜</span><span class="sxs-lookup"><span data-stu-id="2a5e2-111">Top service plans with high CPU and memory utilization</span></span>
- <span data-ttu-id="2a5e2-112">Azure Web Apps 活動記錄作業</span><span class="sxs-lookup"><span data-stu-id="2a5e2-112">Azure Web Apps activity log operations</span></span>

## <a name="connected-sources"></a><span data-ttu-id="2a5e2-113">連接的來源</span><span class="sxs-lookup"><span data-stu-id="2a5e2-113">Connected sources</span></span>

<span data-ttu-id="2a5e2-114">不同於大部分其他 Log Analytics 解決方案，代理程式不會收集 Azure Web Apps 的資料。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-114">Unlike most other Log Analytics solutions, data isn't collected for Azure Web Apps by agents.</span></span> <span data-ttu-id="2a5e2-115">解決方案使用的所有資料直接來自於 Azure。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-115">All data used by the solution comes directly from Azure.</span></span>

| <span data-ttu-id="2a5e2-116">連接的來源</span><span class="sxs-lookup"><span data-stu-id="2a5e2-116">Connected Source</span></span> | <span data-ttu-id="2a5e2-117">支援</span><span class="sxs-lookup"><span data-stu-id="2a5e2-117">Supported</span></span> | <span data-ttu-id="2a5e2-118">說明</span><span class="sxs-lookup"><span data-stu-id="2a5e2-118">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="2a5e2-119">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="2a5e2-119">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="2a5e2-120">否</span><span class="sxs-lookup"><span data-stu-id="2a5e2-120">No</span></span> | <span data-ttu-id="2a5e2-121">解決方案不會收集來自 Windows 代理程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-121">The solution does not collect information from Windows agents.</span></span> |
| [<span data-ttu-id="2a5e2-122">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="2a5e2-122">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="2a5e2-123">否</span><span class="sxs-lookup"><span data-stu-id="2a5e2-123">No</span></span> | <span data-ttu-id="2a5e2-124">解決方案不會收集來自 Linux 代理程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-124">The solution does not collect information from Linux agents.</span></span> |
| [<span data-ttu-id="2a5e2-125">SCOM 管理群組</span><span class="sxs-lookup"><span data-stu-id="2a5e2-125">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="2a5e2-126">否</span><span class="sxs-lookup"><span data-stu-id="2a5e2-126">No</span></span> | <span data-ttu-id="2a5e2-127">解決方案不會收集來自連線 SCOM 管理群組的代理程式之中的資訊。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-127">The solution does not collect information from agents in a connected SCOM management group.</span></span> |
| [<span data-ttu-id="2a5e2-128">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="2a5e2-128">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="2a5e2-129">否</span><span class="sxs-lookup"><span data-stu-id="2a5e2-129">No</span></span> | <span data-ttu-id="2a5e2-130">解決方案不會收集來自 Azure 儲存體的資訊。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-130">The solution does not collection information from Azure storage.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="2a5e2-131">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a5e2-131">Prerequisites</span></span>

- <span data-ttu-id="2a5e2-132">若要存取 Azure Web 應用程式資源計量資訊，您必須有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-132">To access Azure Web App resource metric information, you must have an Azure subscription.</span></span>

## <a name="configuration"></a><span data-ttu-id="2a5e2-133">組態</span><span class="sxs-lookup"><span data-stu-id="2a5e2-133">Configuration</span></span>

<span data-ttu-id="2a5e2-134">執行下列步驟為您的工作區設定 Azure Web Apps 分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-134">Perform the following steps to configure the Azure Web Apps Analytics solution for your workspaces.</span></span>

1. <span data-ttu-id="2a5e2-135">從 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) 或使用[從方案庫加入 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，啟用 Azure Web Apps 分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-135">Enable the Azure Web Apps Analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="2a5e2-136">[使用 PowerShell 允許 Azure 資源計量記錄至 OMS (Enable Azure resource metrics logging to OMS using PowerShell)](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell)。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-136">[Enable Azure resource metrics logging to OMS using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).</span></span>

<span data-ttu-id="2a5e2-137">Azure Web Apps 分析解決方案會從 Azure 收集兩組計量：</span><span class="sxs-lookup"><span data-stu-id="2a5e2-137">The Azure Web Apps Analytics solution collects two set of metrics from Azure:</span></span>

- <span data-ttu-id="2a5e2-138">Azure Web Apps 計量</span><span class="sxs-lookup"><span data-stu-id="2a5e2-138">Azure Web Apps metrics</span></span>
  - <span data-ttu-id="2a5e2-139">平均記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="2a5e2-139">Average Memory Working Set</span></span>
  - <span data-ttu-id="2a5e2-140">平均回應時間</span><span class="sxs-lookup"><span data-stu-id="2a5e2-140">Average Response Time</span></span>
  - <span data-ttu-id="2a5e2-141">已接收/傳送的位元組</span><span class="sxs-lookup"><span data-stu-id="2a5e2-141">Bytes Received/Sent</span></span>
  - <span data-ttu-id="2a5e2-142">CPU 時間</span><span class="sxs-lookup"><span data-stu-id="2a5e2-142">CPU Time</span></span>
  - <span data-ttu-id="2a5e2-143">要求</span><span class="sxs-lookup"><span data-stu-id="2a5e2-143">Requests</span></span>
  - <span data-ttu-id="2a5e2-144">記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="2a5e2-144">Memory Working Set</span></span>
  - <span data-ttu-id="2a5e2-145">Httpxxx</span><span class="sxs-lookup"><span data-stu-id="2a5e2-145">Httpxxx</span></span>
- <span data-ttu-id="2a5e2-146">App Service 方案計量</span><span class="sxs-lookup"><span data-stu-id="2a5e2-146">App Service Plan metrics</span></span>
  - <span data-ttu-id="2a5e2-147">已接收/傳送的位元組</span><span class="sxs-lookup"><span data-stu-id="2a5e2-147">Bytes Received/Sent</span></span>
  - <span data-ttu-id="2a5e2-148">CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="2a5e2-148">CPU Percentage</span></span>
  - <span data-ttu-id="2a5e2-149">磁碟佇列長度</span><span class="sxs-lookup"><span data-stu-id="2a5e2-149">Disk Queue Length</span></span>
  - <span data-ttu-id="2a5e2-150">Http 佇列長度</span><span class="sxs-lookup"><span data-stu-id="2a5e2-150">Http Queue Length</span></span>
  - <span data-ttu-id="2a5e2-151">記憶體百分比</span><span class="sxs-lookup"><span data-stu-id="2a5e2-151">Memory Percentage</span></span>

<span data-ttu-id="2a5e2-152">如果您使用的是專用的服務方案，則只會收集 App Service 方案計量。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-152">App Service Plan metrics are only collected if you are using a dedicated service plan.</span></span> <span data-ttu-id="2a5e2-153">這不適用於免費或共用的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-153">This doesn't apply to free or shared App Service plans.</span></span>

<span data-ttu-id="2a5e2-154">如果您使用 OMS 入口網站新增解決方案，會看見下列圖格。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-154">If you add the solution using the OMS portal, you'll see the following tile.</span></span> <span data-ttu-id="2a5e2-155">您必須[使用 PowerShell 允許 Azure 資源計量記錄至 OMS (enable Azure resource metrics logging to OMS using PowerShell)](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell)。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-155">You need to [enable Azure resource metrics logging to OMS using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).</span></span>

![執行評估通知](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

<span data-ttu-id="2a5e2-157">在您設定解決方案後，資料應會在 15 分鐘內開始流向您的工作區。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-157">After you configure the solution, data should start flowing to your workspace within 15 minutes.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="2a5e2-158">使用解決方案</span><span class="sxs-lookup"><span data-stu-id="2a5e2-158">Using the solution</span></span>

<span data-ttu-id="2a5e2-159">當您將 Azure Web Apps 分析解決方案新增至工作區時，[Azure Web Apps 分析] 圖格會新增至 [概觀] 儀表板。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-159">When you add the Azure Web Apps Analytics solution to your workspace, the **Azure Web Apps Analytics** tile is added to your Overview dashboard.</span></span> <span data-ttu-id="2a5e2-160">此圖格會顯示該解決方案在您的 Azure 訂用帳戶中可存取的 Azure Web Apps 數目。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-160">This tile displays a count of the number of Azure Web Apps that the solution has access to in your Azure subscription.</span></span>

![Azure Web Apps 分析圖格](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a><span data-ttu-id="2a5e2-162">檢視 Azure Web Apps 分析資訊</span><span class="sxs-lookup"><span data-stu-id="2a5e2-162">View Azure Web Apps Analytics information</span></span>

<span data-ttu-id="2a5e2-163">按一下 [Azure Web Apps 分析] 圖格開啟 [Azure Web Apps 分析] 儀表板。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-163">Click the **Azure Web Apps Analytics** tile to open the **Azure Web Apps Analytics** dashboard.</span></span> <span data-ttu-id="2a5e2-164">此儀表板包含下表中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-164">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="2a5e2-165">每個刀鋒視窗會針對所指定的範圍與時間範圍，列出最多 10 個符合該刀鋒視窗準則的項目。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-165">Each blade lists up to ten items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="2a5e2-166">您可以按一下刀鋒視窗底部的 [查看全部]，或按一下刀鋒視窗標頭，以執行記錄搜尋來傳回所有記錄。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-166">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| <span data-ttu-id="2a5e2-167">資料欄</span><span class="sxs-lookup"><span data-stu-id="2a5e2-167">Column</span></span> | <span data-ttu-id="2a5e2-168">說明</span><span class="sxs-lookup"><span data-stu-id="2a5e2-168">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a5e2-169">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="2a5e2-169">Azure Webapps</span></span> |   |
| <span data-ttu-id="2a5e2-170">Web Apps 要求趨勢</span><span class="sxs-lookup"><span data-stu-id="2a5e2-170">Web Apps Request Trends</span></span> | <span data-ttu-id="2a5e2-171">針對您已選取的日期範圍顯示 Web Apps 要求趨勢的折線圖，並顯示前十名 Web 要求清單。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-171">Shows a line chart of the Web Apps request trend for the date range that you have selected and shows a list of the top ten web requests.</span></span> <span data-ttu-id="2a5e2-172">按一下折線圖可執行記錄搜尋，以搜尋 <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code></span><span class="sxs-lookup"><span data-stu-id="2a5e2-172">Click the line chart to run a log search for <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code></span></span> <br><span data-ttu-id="2a5e2-173">按一下 Web 要求項目可執行記錄搜尋，以搜尋所要求的 Web 要求計量趨勢。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-173">Click a web request item to run a log search for the web request metric trend that request.</span></span> |
| <span data-ttu-id="2a5e2-174">Web Apps 回應時間</span><span class="sxs-lookup"><span data-stu-id="2a5e2-174">Web Apps Response Time</span></span> | <span data-ttu-id="2a5e2-175">針對您所選取的日期範圍，顯示 Web Apps 回應時間的折線圖。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-175">Shows a line chart of the Web Apps response time for the date range that you have selected.</span></span> <span data-ttu-id="2a5e2-176">另外也顯示前十名 Web Apps 回應時間清單。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-176">Also shows a list a list of the top ten Web Apps response times.</span></span> <span data-ttu-id="2a5e2-177">按一下該圖表可執行記錄搜尋，以搜尋 <code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code></span><span class="sxs-lookup"><span data-stu-id="2a5e2-177">Click the chart to run a log search for <code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code></span></span><br> <span data-ttu-id="2a5e2-178">按一下某個 Web 應用程式可執行記錄搜尋，以傳回該 Web 應用程式的回應時間。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-178">Click on a Web App to run a log search returning response times for the Web App.</span></span> |
| <span data-ttu-id="2a5e2-179">Web Apps 流量</span><span class="sxs-lookup"><span data-stu-id="2a5e2-179">Web Apps Traffic</span></span> | <span data-ttu-id="2a5e2-180">顯示 Web Apps 流量 (MB) 的折線圖，並列出 Web Apps 流量排行榜。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-180">Shows a line chart for Web Apps traffic, in MB and lists the top Web Apps traffic.</span></span> <span data-ttu-id="2a5e2-181">按一下該圖表可執行記錄搜尋，以搜尋 <code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code></span><span class="sxs-lookup"><span data-stu-id="2a5e2-181">Click the chart to run a log search for <code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code></span></span><br> <span data-ttu-id="2a5e2-182">它會顯示過去一分鐘有流量的所有 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-182">It shows all Web Apps with traffic for the last minute.</span></span> <span data-ttu-id="2a5e2-183">按一下某個 Web 應用程式可執行記錄搜尋，以顯示針對該 Web 應用程式收到與傳送的位元組數。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-183">Click a Web App to run a log search showing bytes received and sent for the Web App.</span></span> |
| <span data-ttu-id="2a5e2-184">Azure App Service 方案</span><span class="sxs-lookup"><span data-stu-id="2a5e2-184">Azure App Service Plans</span></span> |   |
| <span data-ttu-id="2a5e2-185">CPU 使用率 &gt; 80% 的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="2a5e2-185">App Service Plans with CPU utilization &gt; 80%</span></span> | <span data-ttu-id="2a5e2-186">顯示 CPU 使用率大於 80% 的 App Service 方案總數，並依 CPU 使用率列出前 10 名 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-186">Shows the total number of App Service Plans that have CPU utilization greater than 80% and lists the top 10 App Service Plans by CPU utilization.</span></span> <span data-ttu-id="2a5e2-187">按一下總數區可執行記錄搜尋，以搜尋 <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code></span><span class="sxs-lookup"><span data-stu-id="2a5e2-187">Click the total area to run a log search for <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code></span></span><br> <span data-ttu-id="2a5e2-188">它會顯示 App Service 方案清單及其平均 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-188">It shows a list of your App Service Plans and their average CPU utilization.</span></span> <span data-ttu-id="2a5e2-189">按一下某個 App Service 方案可執行記錄搜尋，以顯示平均 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-189">Click an App Service Plan to run a log search showing its average CPU utilization.</span></span> |
| <span data-ttu-id="2a5e2-190">記憶體使用率 &gt; 80% 的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="2a5e2-190">App Service Plans with memory utilization &gt; 80%</span></span> | <span data-ttu-id="2a5e2-191">顯示記憶體使用率大於 80% 的 App Service 方案總數，並依記憶體使用率列出前 10 名 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-191">Shows the total number of App Service Plans that have memory utilization greater than 80% and lists the top 10 App Service Plans by memory utilization.</span></span> <span data-ttu-id="2a5e2-192">按一下總數區可執行記錄搜尋，以搜尋 <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code></span><span class="sxs-lookup"><span data-stu-id="2a5e2-192">Click the total area to run a log search for <code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code></span></span><br> <span data-ttu-id="2a5e2-193">它會顯示 App Service 方案清單及其平均記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-193">It shows a list of your App Service Plans and their average memory utilization.</span></span> <span data-ttu-id="2a5e2-194">按一下某個 App Service 方案可執行記錄搜尋，以顯示其平均記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-194">Click an App Service Plan to run a log search showing its average memory utilization.</span></span> |
| <span data-ttu-id="2a5e2-195">Azure Web Apps 活動記錄</span><span class="sxs-lookup"><span data-stu-id="2a5e2-195">Azure Web Apps Activity Logs</span></span> |   |
| <span data-ttu-id="2a5e2-196">Azure Web Apps 活動稽核</span><span class="sxs-lookup"><span data-stu-id="2a5e2-196">Azure Web Apps Activity Audit</span></span> | <span data-ttu-id="2a5e2-197">顯示有[活動記錄](log-analytics-activity.md)的 Web Apps 總數，並列出前 10 名的活動記錄作業。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-197">Shows the total number of Web Apps with [activity logs](log-analytics-activity.md) and lists the top 10 activity log operations.</span></span> <span data-ttu-id="2a5e2-198">按一下總數區可執行記錄搜尋，以搜尋 <code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code></span><span class="sxs-lookup"><span data-stu-id="2a5e2-198">Click the total area to run a log search for <code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code></span></span><br> <span data-ttu-id="2a5e2-199">它會顯示活動記錄作業清單。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-199">It shows a list of the activity log operations.</span></span> <span data-ttu-id="2a5e2-200">按一下活動記錄作業可記錄搜尋，以列出作業記錄。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-200">Click an activity log operation to run a log search that lists the records for the operation.</span></span> |



### <a name="azure-web-apps"></a><span data-ttu-id="2a5e2-201">Azure Web Apps </span><span class="sxs-lookup"><span data-stu-id="2a5e2-201">Azure Web Apps</span></span>

<span data-ttu-id="2a5e2-202">在儀表板中，您可以向下鑽研以深入了解您的 Web Apps 計量。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-202">In the dashboard, you can drill down to get more insight into your Web Apps metrics.</span></span> <span data-ttu-id="2a5e2-203">這第一組刀鋒視窗會顯示 Web Apps 要求的趨勢、錯誤數目 (例如 HTTP404)、流量，以及一段時間的平均回應時間。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-203">This first set of blades show the trend of the Web Apps requests, number of errors (for example, HTTP404), traffic, and average response time over time.</span></span> <span data-ttu-id="2a5e2-204">它也會顯示不同 Web Apps 的這些計量細目。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-204">It also shows a breakdown of those metrics for different Web Apps.</span></span>

![Azure Web Apps 刀鋒視窗](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

<span data-ttu-id="2a5e2-206">顯示該資料的主要原因是讓您可以識別回應時間最長的 Web 應用程式，並調查找出根本原因。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-206">A primary reason for showing you that data is so that you can identify a Web App with high response time and investigate to find the root cause.</span></span> <span data-ttu-id="2a5e2-207">此外也會套用臨界值限制，幫助您更容易找出有問題之處。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-207">A threshold limit is also applied to help you more easily identify the ones with issues.</span></span>

- <span data-ttu-id="2a5e2-208">紅色的 Web Apps 其回應時間超過 1 秒。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-208">Web Apps shown in red have response time higher than 1 second.</span></span>
- <span data-ttu-id="2a5e2-209">橘色的 Web Apps 其回應時間超過 0.7 秒，不到 1 秒。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-209">Web Apps shown in orange have a response time higher than 0.7 second and less than 1 second.</span></span>
- <span data-ttu-id="2a5e2-210">綠色的 Web Apps 其回應時間不到 0.7 秒。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-210">Web Apps shown in green have a response time less than 0.7 second.</span></span>

<span data-ttu-id="2a5e2-211">在下列記錄搜尋範例影像中，您可以看到 *anugup3* Web 應用程式的回應時間遠多於其他的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-211">In the following log search example image, you can see that the *anugup3* web app had a much higher response time than the other web apps.</span></span>

![記錄搜尋範例](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a><span data-ttu-id="2a5e2-213">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="2a5e2-213">App Service Plans</span></span>

<span data-ttu-id="2a5e2-214">如果您使用專用的服務方案，則亦可收集您 App Service 方案的計量。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-214">If you are using dedicated Service Plans, you can also collect metrics for your App Service Plans.</span></span> <span data-ttu-id="2a5e2-215">在這個檢視中，您會看到 CPU 或記憶體使用率高 (&gt; 80%) 的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-215">In this view, you see your App Service Plans with high CPU or Memory utilization (&gt; 80%).</span></span> <span data-ttu-id="2a5e2-216">此外，也會顯示記憶體或 CPU 使用率高的應用程式服務排行榜。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-216">It also shows you the top App services with high Memory or CPU utilization.</span></span> <span data-ttu-id="2a5e2-217">同樣地會套用臨界值限制，來幫助您更容易找出有問題的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-217">Similarly, a threshold limit is applied to help you more easily identify the ones with issues.</span></span>

- <span data-ttu-id="2a5e2-218">紅色的 App Service 方案其 CPU/記憶體使用率高於 80%。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-218">App Service Plans shown in red have a CPU/Memory utilization higher than 80%.</span></span>
- <span data-ttu-id="2a5e2-219">橘色的 App Service 方案其 CPU/記憶體使用率高於 60%，低於 80%。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-219">App Service Plans shown in orange have a CPU/Memory utilization higher than 60% and lower than 80%.</span></span>
- <span data-ttu-id="2a5e2-220">綠色的 App Service 方案其 CPU/記憶體使用率低於 60%。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-220">App Service Plans shown in green have a CPU/Memory utilization lower than 60%.</span></span>

![Azure App Service 方案刀鋒視窗](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a><span data-ttu-id="2a5e2-222">Azure Web Apps 記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="2a5e2-222">Azure Web Apps log searches</span></span>

<span data-ttu-id="2a5e2-223">**熱門 Azure Web Apps 搜尋查詢清單**顯示 Web Apps 的所有相關活動記錄，讓您深入了解在您 Web Apps 資源上執行的作業。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-223">The **List of Popular Azure Web Apps Search queries** shows you all the related activity logs for Web Apps, which provides insights into the operations that were performed on your Web Apps resources.</span></span> <span data-ttu-id="2a5e2-224">此外也會列出所有相關的作業，以及其發生的次數。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-224">It also lists all the related operations and the number of times they have occurred.</span></span>

<span data-ttu-id="2a5e2-225">您可以從使用任何的記錄搜尋查詢開始，來輕鬆建立警示。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-225">Using any of the log search queries as a starting point, you can easily create an alert.</span></span> <span data-ttu-id="2a5e2-226">例如，您可能會想要在計量平均回應時間超過 1 秒時即建立警示。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-226">For example, you might want to create an alert when a metric's average response time is greater than every 1 second.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a5e2-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a5e2-227">Next steps</span></span>

- <span data-ttu-id="2a5e2-228">建立特定計量的[警示](log-analytics-alerts-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-228">Create an [alert](log-analytics-alerts-creating.md) for a specific metric.</span></span>
- <span data-ttu-id="2a5e2-229">使用[記錄搜尋](log-analytics-log-searches.md)檢視活動記錄的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2a5e2-229">Use [Log Search](log-analytics-log-searches.md) to view detailed information from your activity logs.</span></span>
