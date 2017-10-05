---
title: "Log Analytics 中的 Azure 網路分析解決方案 | Microsoft Docs"
description: "您可以使用 Log Analytics 中的 Azure 網路分析解決方案，以檢閱 Azure 網路安全性群組記錄檔和 Azure 應用程式閘道記錄檔。"
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 06b67322b3812a668a515ecc357171ede1d85441
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="7d604-103">Log Analytics 中的 Azure 網路監視解決方案</span><span class="sxs-lookup"><span data-stu-id="7d604-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="7d604-104">Log Analytics 提供下列解決方案來監視您的網路︰</span><span class="sxs-lookup"><span data-stu-id="7d604-104">Log Analytics offers the following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="7d604-105">網路效能監視器 (NPM) 以</span><span class="sxs-lookup"><span data-stu-id="7d604-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="7d604-106">監視網路的健康狀態</span><span class="sxs-lookup"><span data-stu-id="7d604-106">Monitor the health of your network</span></span>
* <span data-ttu-id="7d604-107">要檢閱的 Azure 應用程式閘道分析</span><span class="sxs-lookup"><span data-stu-id="7d604-107">Azure Application Gateway analytics to review</span></span>
 * <span data-ttu-id="7d604-108">Azure 應用程式閘道記錄檔</span><span class="sxs-lookup"><span data-stu-id="7d604-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="7d604-109">Azure 應用程式閘道計量</span><span class="sxs-lookup"><span data-stu-id="7d604-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="7d604-110">要檢閱的 Azure 網路安全性群組分析</span><span class="sxs-lookup"><span data-stu-id="7d604-110">Azure Network Security Group analytics to review</span></span>
 * <span data-ttu-id="7d604-111">Azure 網路安全性群組記錄檔</span><span class="sxs-lookup"><span data-stu-id="7d604-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="7d604-112">網路效能監視器 (NPM)</span><span class="sxs-lookup"><span data-stu-id="7d604-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="7d604-113">[網路效能監視器](log-analytics-network-performance-monitor.md)管理解決方案是網路監視解決方案，可監視網路的健康狀態、可用性和連線能力。</span><span class="sxs-lookup"><span data-stu-id="7d604-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span></span>  <span data-ttu-id="7d604-114">可用來監視下列項目之間的連線能力︰</span><span class="sxs-lookup"><span data-stu-id="7d604-114">It is used to monitor connectivity between:</span></span>

* <span data-ttu-id="7d604-115">公用雲端與內部部署環境</span><span class="sxs-lookup"><span data-stu-id="7d604-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="7d604-116">資料中心與使用者地點 (分公司)</span><span class="sxs-lookup"><span data-stu-id="7d604-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="7d604-117">裝載多層式應用程式各層的子網路。</span><span class="sxs-lookup"><span data-stu-id="7d604-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="7d604-118">如需詳細資訊，請參閱[網路效能監視器](log-analytics-network-performance-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="7d604-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="7d604-119">Azure 應用程式閘道和網路安全性群組分析</span><span class="sxs-lookup"><span data-stu-id="7d604-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="7d604-120">若要使用解決方案：</span><span class="sxs-lookup"><span data-stu-id="7d604-120">To use the solutions:</span></span>
1. <span data-ttu-id="7d604-121">將管理解決方案新增至 Log Analytics，以及</span><span class="sxs-lookup"><span data-stu-id="7d604-121">Add the management solution to Log Analytics, and</span></span>
2. <span data-ttu-id="7d604-122">啟用診斷功能以將診斷導向 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="7d604-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="7d604-123">不需要將記錄寫入 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7d604-123">It is not necessary to write the logs to Azure Blob storage.</span></span>

<span data-ttu-id="7d604-124">您可以針對應用程式閘道和網路安全性群組其中之一 (或兩者) 啟用診斷與對應的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7d604-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="7d604-125">如果您沒有針對特定資源類型啟用診斷記錄，但是安裝了解決方案，該資源的儀表板刀鋒視窗會是空白，並顯示一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7d604-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="7d604-126">從 2017 年 1 月開始，從應用程式閘道和網路安全性群組傳送記錄到 Log Analytics 的支援方式已變更。</span><span class="sxs-lookup"><span data-stu-id="7d604-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="7d604-127">如果您看到 **Azure 網路分析 (已過時)** 解決方案，請參閱[從舊的網路分析解決方案進行移轉](#migrating-from-the-old-networking-analytics-solution)，以取得您必須遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="7d604-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="7d604-128">檢閱 Azure 網路資料集合詳細資料</span><span class="sxs-lookup"><span data-stu-id="7d604-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="7d604-129">Azure 應用程式閘道分析和網路安全性群組分析管理解決方案，會直接從 Azure 應用程式閘道和網路安全性群組收集診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="7d604-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="7d604-130">不需要將記錄寫入 Azure Blob 儲存體，也不需要代理程式來收集資料。</span><span class="sxs-lookup"><span data-stu-id="7d604-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="7d604-131">下表顯示資料收集方法，與其他有關如何針對 Azure 應用程式閘道分析和網路安全性群組分析收集資料的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7d604-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span></span>

| <span data-ttu-id="7d604-132">平台</span><span class="sxs-lookup"><span data-stu-id="7d604-132">Platform</span></span> | <span data-ttu-id="7d604-133">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="7d604-133">Direct agent</span></span> | <span data-ttu-id="7d604-134">Systems Center Operations Manager 代理程式</span><span class="sxs-lookup"><span data-stu-id="7d604-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="7d604-135">Azure</span><span class="sxs-lookup"><span data-stu-id="7d604-135">Azure</span></span> | <span data-ttu-id="7d604-136">是否需要 Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="7d604-136">Operations Manager required?</span></span> | <span data-ttu-id="7d604-137">透過管理群組傳送的 Operations Manager 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="7d604-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="7d604-138">收集頻率</span><span class="sxs-lookup"><span data-stu-id="7d604-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="7d604-139">Azure</span><span class="sxs-lookup"><span data-stu-id="7d604-139">Azure</span></span> |  |  |<span data-ttu-id="7d604-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="7d604-140">&#8226;</span></span> |  |  |<span data-ttu-id="7d604-141">登入時</span><span class="sxs-lookup"><span data-stu-id="7d604-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="7d604-142">Log Analytics 中的 Azure 應用程式閘道分析解決方案</span><span class="sxs-lookup"><span data-stu-id="7d604-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Azure 應用程式閘道分析符號](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="7d604-144">應用程式閘道支援下列記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="7d604-144">The following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="7d604-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="7d604-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="7d604-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="7d604-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="7d604-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="7d604-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="7d604-148">應用程式閘道支援下列度量︰</span><span class="sxs-lookup"><span data-stu-id="7d604-148">The following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="7d604-149">5 分鐘輸送量</span><span class="sxs-lookup"><span data-stu-id="7d604-149">5 minute throughput</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="7d604-150">安裝和設定解決方案</span><span class="sxs-lookup"><span data-stu-id="7d604-150">Install and configure the solution</span></span>
<span data-ttu-id="7d604-151">使用下列指示來安裝和設定 Azure 應用程式閘道分析解決方案：</span><span class="sxs-lookup"><span data-stu-id="7d604-151">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="7d604-152">從 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) 或使用[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，啟用 Azure 應用程式閘道分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="7d604-152">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="7d604-153">針對您想要監視的[應用程式閘道](../application-gateway/application-gateway-diagnostics.md)啟用診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="7d604-153">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a><span data-ttu-id="7d604-154">在入口網站中啟用 Azure 應用程式閘道診斷</span><span class="sxs-lookup"><span data-stu-id="7d604-154">Enable Azure Application Gateway diagnostics in the portal</span></span>

1. <span data-ttu-id="7d604-155">在 Azure 入口網站中，瀏覽至要監視的應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="7d604-155">In the Azure portal, navigate to the Application Gateway resource to monitor</span></span>
2. <span data-ttu-id="7d604-156">選取 [診斷記錄] 以開啟下列頁面</span><span class="sxs-lookup"><span data-stu-id="7d604-156">Select *Diagnostics logs* to open the following page</span></span>

   ![Azure 應用程式閘道資源的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="7d604-158">按一下 [開啟診斷] 以開啟下列頁面</span><span class="sxs-lookup"><span data-stu-id="7d604-158">Click *Turn on diagnostics* to open the following page</span></span>

   ![Azure 應用程式閘道資源的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="7d604-160">若要開啟診斷，請按一下 [狀態] 下的 [開啟]</span><span class="sxs-lookup"><span data-stu-id="7d604-160">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="7d604-161">按一下 [傳送到 Log Analytics] 核取方塊</span><span class="sxs-lookup"><span data-stu-id="7d604-161">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="7d604-162">選取現有的 Log Analytics 工作區，或建立工作區</span><span class="sxs-lookup"><span data-stu-id="7d604-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="7d604-163">針對每一個要收集的記錄類型，按一下 [記錄] 下的核取方塊</span><span class="sxs-lookup"><span data-stu-id="7d604-163">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="7d604-164">按一下 [儲存] 以啟用 Log Analytics 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="7d604-164">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="7d604-165">使用 PowerShell 啟用 Azure 網路診斷</span><span class="sxs-lookup"><span data-stu-id="7d604-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="7d604-166">下列 PowerShell 指令碼示範如何啟用應用程式閘道診斷記錄的範例。</span><span class="sxs-lookup"><span data-stu-id="7d604-166">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="7d604-167">使用 Azure 應用程式閘道分析</span><span class="sxs-lookup"><span data-stu-id="7d604-167">Use Azure Application Gateway analytics</span></span>
![Azure 應用程式閘道分析圖格的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="7d604-169">在您按一下 [概觀] 上的 [Azure 應用程式閘道分析] 圖格之後，您可以檢視記錄摘要，然後深入探索下列類別的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="7d604-169">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="7d604-170">應用程式閘道存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="7d604-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="7d604-171">應用程式閘道存取記錄檔的用戶端和伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="7d604-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="7d604-172">每個應用程式閘道的每小時要求數</span><span class="sxs-lookup"><span data-stu-id="7d604-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="7d604-173">每個應用程式閘道的每小時失敗要求數</span><span class="sxs-lookup"><span data-stu-id="7d604-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="7d604-174">應用程式閘道依使用者代理程式分類的錯誤</span><span class="sxs-lookup"><span data-stu-id="7d604-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="7d604-175">應用程式閘道效能</span><span class="sxs-lookup"><span data-stu-id="7d604-175">Application Gateway performance</span></span>
  * <span data-ttu-id="7d604-176">應用程式閘道的主機健康狀態</span><span class="sxs-lookup"><span data-stu-id="7d604-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="7d604-177">應用程式閘道失敗要求的最大和第 95 個百分位數</span><span class="sxs-lookup"><span data-stu-id="7d604-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Azure 應用程式閘道分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Azure 應用程式閘道分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="7d604-180">在 [Azure 應用程式閘道分析] 儀表板上，檢閱其中一個刀鋒視窗中的摘要資訊，然後按一下其中一個以在記錄搜尋頁面中檢視詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7d604-180">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="7d604-181">您可以在任何 [記錄搜尋] 頁面上，按時間、詳細結果和您的記錄搜尋記錄來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="7d604-181">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="7d604-182">您也可以按 Facet 篩選以縮減結果。</span><span class="sxs-lookup"><span data-stu-id="7d604-182">You can also filter by facets to narrow the results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="7d604-183">Log Analytics 中的 Azure 網路安全性群組分析解決方案</span><span class="sxs-lookup"><span data-stu-id="7d604-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Azure 網路安全性群組分析符號](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="7d604-185">網路安全性群組支援下列記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="7d604-185">The following logs are supported for network security groups:</span></span>

* <span data-ttu-id="7d604-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="7d604-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="7d604-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="7d604-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="7d604-188">安裝和設定解決方案</span><span class="sxs-lookup"><span data-stu-id="7d604-188">Install and configure the solution</span></span>
<span data-ttu-id="7d604-189">使用下列指示來安裝和設定 Azure 網路分析解決方案︰</span><span class="sxs-lookup"><span data-stu-id="7d604-189">Use the following instructions to install and configure the Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="7d604-190">從 [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) 或使用[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，啟用 Azure 網路安全性群組分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="7d604-190">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="7d604-191">針對您想要監視的[網路安全性群組](../virtual-network/virtual-network-nsg-manage-log.md)資源啟用診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="7d604-191">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a><span data-ttu-id="7d604-192">在入口網站中啟用 Azure 網路安全性群組診斷</span><span class="sxs-lookup"><span data-stu-id="7d604-192">Enable Azure network security group diagnostics in the portal</span></span>

1. <span data-ttu-id="7d604-193">在 Azure 入口網站中，瀏覽至要監視的網路安全性群組資源</span><span class="sxs-lookup"><span data-stu-id="7d604-193">In the Azure portal, navigate to the Network Security Group resource to monitor</span></span>
2. <span data-ttu-id="7d604-194">選取 [診斷記錄] 以開啟下列頁面</span><span class="sxs-lookup"><span data-stu-id="7d604-194">Select *Diagnostics logs* to open the following page</span></span>

   ![Azure 網路安全性群組資源的影像](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="7d604-196">按一下 [開啟診斷] 以開啟下列頁面</span><span class="sxs-lookup"><span data-stu-id="7d604-196">Click *Turn on diagnostics* to open the following page</span></span>

   ![Azure 網路安全性群組資源的影像](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="7d604-198">若要開啟診斷，請按一下 [狀態] 下的 [開啟]</span><span class="sxs-lookup"><span data-stu-id="7d604-198">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="7d604-199">按一下 [傳送到 Log Analytics] 核取方塊</span><span class="sxs-lookup"><span data-stu-id="7d604-199">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="7d604-200">選取現有的 Log Analytics 工作區，或建立工作區</span><span class="sxs-lookup"><span data-stu-id="7d604-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="7d604-201">針對每一個要收集的記錄類型，按一下 [記錄] 下的核取方塊</span><span class="sxs-lookup"><span data-stu-id="7d604-201">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="7d604-202">按一下 [儲存] 以啟用 Log Analytics 的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="7d604-202">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="7d604-203">使用 PowerShell 啟用 Azure 網路診斷</span><span class="sxs-lookup"><span data-stu-id="7d604-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="7d604-204">下列 PowerShell 指令碼提供如何啟用網路安全性群組診斷記錄的範例</span><span class="sxs-lookup"><span data-stu-id="7d604-204">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="7d604-205">使用 Azure 網路安全性群組分析</span><span class="sxs-lookup"><span data-stu-id="7d604-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="7d604-206">在您按一下 [概觀] 上的 [Azure 網路安全性群組分析] 圖格之後，您可以檢視記錄摘要，然後深入探索下列類別的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="7d604-206">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="7d604-207">網路安全性群組封鎖流量</span><span class="sxs-lookup"><span data-stu-id="7d604-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="7d604-208">網路安全性群組規則與封鎖流量</span><span class="sxs-lookup"><span data-stu-id="7d604-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="7d604-209">MAC 位址與封鎖流量</span><span class="sxs-lookup"><span data-stu-id="7d604-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="7d604-210">網路安全性群組允許流量</span><span class="sxs-lookup"><span data-stu-id="7d604-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="7d604-211">網路安全性群組規則與允許流量</span><span class="sxs-lookup"><span data-stu-id="7d604-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="7d604-212">MAC 位址與允許流量</span><span class="sxs-lookup"><span data-stu-id="7d604-212">MAC addresses with allowed flows</span></span>

![Azure 網路安全性群組分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Azure 網路安全性群組分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="7d604-215">在 [Azure 網路安全性群組分析] 儀表板上，檢閱其中一個刀鋒視窗中的摘要資訊，然後按一下其中一個以在記錄搜尋頁面中檢視詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7d604-215">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="7d604-216">您可以在任何 [記錄搜尋] 頁面上，按時間、詳細結果和您的記錄搜尋記錄來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="7d604-216">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="7d604-217">您也可以按 Facet 篩選以縮減結果。</span><span class="sxs-lookup"><span data-stu-id="7d604-217">You can also filter by facets to narrow the results.</span></span>

## <a name="migrating-from-the-old-networking-analytics-solution"></a><span data-ttu-id="7d604-218">從舊的網路分析解決方案進行移轉</span><span class="sxs-lookup"><span data-stu-id="7d604-218">Migrating from the old Networking Analytics solution</span></span>
<span data-ttu-id="7d604-219">從 2017 年 1 月開始，從 Azure 應用程式閘道和 Azure 網路安全性群組傳送記錄到 Log Analytics 的支援方式已變更。</span><span class="sxs-lookup"><span data-stu-id="7d604-219">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="7d604-220">這些變更可提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="7d604-220">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="7d604-221">記錄會直接寫入 Log Analytics，而不需要使用儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7d604-221">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="7d604-222">當 Log Analytics 中具有產生的記錄時，延遲會變得較低</span><span class="sxs-lookup"><span data-stu-id="7d604-222">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="7d604-223">較少的組態步驟</span><span class="sxs-lookup"><span data-stu-id="7d604-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="7d604-224">所有 Azure 診斷類型的通用格式</span><span class="sxs-lookup"><span data-stu-id="7d604-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="7d604-225">若要使用更新的解決方案：</span><span class="sxs-lookup"><span data-stu-id="7d604-225">To use the updated solutions:</span></span>

1. [<span data-ttu-id="7d604-226">將診斷設定為直接從 Azure 應用程式閘道傳送到 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7d604-226">Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="7d604-227">將診斷設定為直接從 Azure 網路安全性群組傳送到 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="7d604-227">Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="7d604-228">使用[從方案庫新增 Log Analytics 解決方案](log-analytics-add-solutions.md)中所述的程序，啟用「Azure 應用程式閘道分析」和「Azure 網路安全性群組分析」解決方案</span><span class="sxs-lookup"><span data-stu-id="7d604-228">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="7d604-229">更新任何已儲存的查詢、儀表板或警示，以使用新的資料類型</span><span class="sxs-lookup"><span data-stu-id="7d604-229">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="7d604-230">類型是 AzureDiagnostics。</span><span class="sxs-lookup"><span data-stu-id="7d604-230">Type is to AzureDiagnostics.</span></span> <span data-ttu-id="7d604-231">您可以使用 ResourceType 來篩選 Azure 網路記錄。</span><span class="sxs-lookup"><span data-stu-id="7d604-231">You can use the ResourceType to filter to Azure networking logs.</span></span>

    | <span data-ttu-id="7d604-232">不要使用：</span><span class="sxs-lookup"><span data-stu-id="7d604-232">Instead of:</span></span> | <span data-ttu-id="7d604-233">使用︰</span><span class="sxs-lookup"><span data-stu-id="7d604-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="7d604-234">針對任何名稱尾碼有 \_s、\_d 或 \_g 的欄位，請將第一個字元變更為小寫</span><span class="sxs-lookup"><span data-stu-id="7d604-234">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
   + <span data-ttu-id="7d604-235">針對任何名稱尾碼有 \_o 的欄位，資料會根據巢狀欄位名稱分割為個別欄位。</span><span class="sxs-lookup"><span data-stu-id="7d604-235">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span>
4. <span data-ttu-id="7d604-236">移除 *Azure 網路分析 (已過時)* 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7d604-236">Remove the *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="7d604-237">如果您是使用 PowerShell，請使用 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="7d604-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="7d604-238">在變更之前所收集的資料不會顯示在新的解決方案中。</span><span class="sxs-lookup"><span data-stu-id="7d604-238">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="7d604-239">您可以繼續使用舊的類型和欄位名稱查詢此資料。</span><span class="sxs-lookup"><span data-stu-id="7d604-239">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7d604-240">疑難排解</span><span class="sxs-lookup"><span data-stu-id="7d604-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="7d604-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d604-241">Next steps</span></span>
* <span data-ttu-id="7d604-242">使用 [Log Analytics 中的記錄搜尋](log-analytics-log-searches.md)檢視詳細的 Azure 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="7d604-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span></span>
