---
title: "aaaAzure 記錄分析中的網路分析解決方案 |Microsoft 文件"
description: "您可以使用 hello 記錄分析 tooreview Azure 網路安全性群組記錄檔及 Azure 應用程式閘道記錄檔中的 Azure 網路分析解決方案。"
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
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="de0d1-103">Log Analytics 中的 Azure 網路監視解決方案</span><span class="sxs-lookup"><span data-stu-id="de0d1-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="de0d1-104">記錄分析會提供下列用於監視您的網路解決方案的 hello:</span><span class="sxs-lookup"><span data-stu-id="de0d1-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="de0d1-105">網路效能監視器 (NPM) 以</span><span class="sxs-lookup"><span data-stu-id="de0d1-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="de0d1-106">您的網路監視 hello 健全狀況</span><span class="sxs-lookup"><span data-stu-id="de0d1-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="de0d1-107">Azure 應用程式閘道分析 tooreview</span><span class="sxs-lookup"><span data-stu-id="de0d1-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="de0d1-108">Azure 應用程式閘道記錄檔</span><span class="sxs-lookup"><span data-stu-id="de0d1-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="de0d1-109">Azure 應用程式閘道計量</span><span class="sxs-lookup"><span data-stu-id="de0d1-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="de0d1-110">Azure 網路安全性群組分析 tooreview</span><span class="sxs-lookup"><span data-stu-id="de0d1-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="de0d1-111">Azure 網路安全性群組記錄檔</span><span class="sxs-lookup"><span data-stu-id="de0d1-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="de0d1-112">網路效能監視器 (NPM)</span><span class="sxs-lookup"><span data-stu-id="de0d1-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="de0d1-113">hello[網路效能監視器](log-analytics-network-performance-monitor.md)管理解決方案是網路監視解決方案，可監視 hello 健全狀況、 可用性和網路的連線。</span><span class="sxs-lookup"><span data-stu-id="de0d1-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="de0d1-114">它是使用的 toomonitor 之間的連線：</span><span class="sxs-lookup"><span data-stu-id="de0d1-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="de0d1-115">公用雲端與內部部署環境</span><span class="sxs-lookup"><span data-stu-id="de0d1-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="de0d1-116">資料中心與使用者地點 (分公司)</span><span class="sxs-lookup"><span data-stu-id="de0d1-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="de0d1-117">裝載多層式應用程式各層的子網路。</span><span class="sxs-lookup"><span data-stu-id="de0d1-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="de0d1-118">如需詳細資訊，請參閱[網路效能監視器](log-analytics-network-performance-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="de0d1-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="de0d1-119">Azure 應用程式閘道和網路安全性群組分析</span><span class="sxs-lookup"><span data-stu-id="de0d1-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="de0d1-120">toouse hello 方案：</span><span class="sxs-lookup"><span data-stu-id="de0d1-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="de0d1-121">新增 hello 管理方案 tooLog 分析，並</span><span class="sxs-lookup"><span data-stu-id="de0d1-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="de0d1-122">啟用診斷 toodirect hello 診斷 tooa 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="de0d1-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="de0d1-123">不需要 toowrite hello 記錄 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="de0d1-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="de0d1-124">您可以啟用診斷和 hello 對應之方案的一或兩個應用程式閘道和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="de0d1-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="de0d1-125">如果您不要啟用診斷記錄的特定資源類型，但安裝 hello 解決方案，hello 儀表板刀鋒視窗，該資源是空白，並顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="de0d1-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="de0d1-126">在年 1 月 2017 hello 會支援從應用程式閘道和網路安全性群組 tooLog 分析變更傳送記錄檔的方式。</span><span class="sxs-lookup"><span data-stu-id="de0d1-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="de0d1-127">如果您看到 hello **（已過時） 的 Azure 網路分析**方案中，參考太[hello 舊的網路分析解決方案從移轉](#migrating-from-the-old-networking-analytics-solution)步驟中，您需要 toofollow。</span><span class="sxs-lookup"><span data-stu-id="de0d1-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="de0d1-128">檢閱 Azure 網路資料集合詳細資料</span><span class="sxs-lookup"><span data-stu-id="de0d1-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="de0d1-129">hello Azure 應用程式閘道分析與 hello 網路安全性群組分析管理解決方案會直接從 Azure 應用程式閘道和網路安全性群組收集診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="de0d1-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="de0d1-130">不必要的 toowrite hello 記錄 tooAzure Blob 儲存體，而且沒有代理程式需要的資料收集。</span><span class="sxs-lookup"><span data-stu-id="de0d1-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="de0d1-131">hello 下表顯示資料收集方法，以及如何針對 Azure 應用程式閘道分析和 hello 網路安全性群組分析收集資料的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="de0d1-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="de0d1-132">平台</span><span class="sxs-lookup"><span data-stu-id="de0d1-132">Platform</span></span> | <span data-ttu-id="de0d1-133">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="de0d1-133">Direct agent</span></span> | <span data-ttu-id="de0d1-134">Systems Center Operations Manager 代理程式</span><span class="sxs-lookup"><span data-stu-id="de0d1-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="de0d1-135">Azure</span><span class="sxs-lookup"><span data-stu-id="de0d1-135">Azure</span></span> | <span data-ttu-id="de0d1-136">是否需要 Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="de0d1-136">Operations Manager required?</span></span> | <span data-ttu-id="de0d1-137">透過管理群組傳送的 Operations Manager 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="de0d1-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="de0d1-138">收集頻率</span><span class="sxs-lookup"><span data-stu-id="de0d1-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="de0d1-139">Azure</span><span class="sxs-lookup"><span data-stu-id="de0d1-139">Azure</span></span> |  |  |<span data-ttu-id="de0d1-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="de0d1-140">&#8226;</span></span> |  |  |<span data-ttu-id="de0d1-141">登入時</span><span class="sxs-lookup"><span data-stu-id="de0d1-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="de0d1-142">Log Analytics 中的 Azure 應用程式閘道分析解決方案</span><span class="sxs-lookup"><span data-stu-id="de0d1-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Azure 應用程式閘道分析符號](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="de0d1-144">應用程式閘道可支援下列記錄檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="de0d1-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="de0d1-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="de0d1-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="de0d1-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="de0d1-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="de0d1-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="de0d1-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="de0d1-148">應用程式閘道可支援下列度量的 hello:</span><span class="sxs-lookup"><span data-stu-id="de0d1-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="de0d1-149">5 分鐘輸送量</span><span class="sxs-lookup"><span data-stu-id="de0d1-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="de0d1-150">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="de0d1-150">Install and configure hello solution</span></span>
<span data-ttu-id="de0d1-151">使用下列指示 tooinstall hello，並設定 hello Azure 應用程式閘道分析解決方案：</span><span class="sxs-lookup"><span data-stu-id="de0d1-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="de0d1-152">啟用從 hello Azure 應用程式閘道分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="de0d1-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="de0d1-153">啟用診斷記錄的 hello[應用程式閘道](../application-gateway/application-gateway-diagnostics.md)想 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="de0d1-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="de0d1-154">啟用 hello 入口網站中的 Azure 應用程式閘道診斷</span><span class="sxs-lookup"><span data-stu-id="de0d1-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="de0d1-155">在 [hello Azure 入口網站，瀏覽 toohello 應用程式閘道資源 toomonitor</span><span class="sxs-lookup"><span data-stu-id="de0d1-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="de0d1-156">選取*診斷記錄檔*tooopen hello 遵循頁面</span><span class="sxs-lookup"><span data-stu-id="de0d1-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure 應用程式閘道資源的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="de0d1-158">按一下*開啟診斷*tooopen hello 遵循頁面</span><span class="sxs-lookup"><span data-stu-id="de0d1-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure 應用程式閘道資源的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="de0d1-160">診斷，tooturn 按一下*上*下*狀態*</span><span class="sxs-lookup"><span data-stu-id="de0d1-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="de0d1-161">按一下 [hello] 核取方塊*傳送 tooLog 分析*</span><span class="sxs-lookup"><span data-stu-id="de0d1-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="de0d1-162">選取現有的 Log Analytics 工作區，或建立工作區</span><span class="sxs-lookup"><span data-stu-id="de0d1-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="de0d1-163">按一下下方的核取方塊 hello**記錄**hello 記錄類型 toocollect 的每個</span><span class="sxs-lookup"><span data-stu-id="de0d1-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="de0d1-164">按一下*儲存*tooenable hello 記錄診斷 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="de0d1-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="de0d1-165">使用 PowerShell 啟用 Azure 網路診斷</span><span class="sxs-lookup"><span data-stu-id="de0d1-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="de0d1-166">下列 PowerShell 指令碼的 hello 提供的範例 tooenable 應用程式閘道的診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="de0d1-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="de0d1-167">使用 Azure 應用程式閘道分析</span><span class="sxs-lookup"><span data-stu-id="de0d1-167">Use Azure Application Gateway analytics</span></span>
![Azure 應用程式閘道分析圖格的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="de0d1-169">按一下 hello 之後**Azure 應用程式閘道分析**磚上 hello 概觀，您可以檢視記錄檔的摘要，而且然後鑽研 toodetails hello 下列類別：</span><span class="sxs-lookup"><span data-stu-id="de0d1-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="de0d1-170">應用程式閘道存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="de0d1-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="de0d1-171">應用程式閘道存取記錄檔的用戶端和伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="de0d1-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="de0d1-172">每個應用程式閘道的每小時要求數</span><span class="sxs-lookup"><span data-stu-id="de0d1-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="de0d1-173">每個應用程式閘道的每小時失敗要求數</span><span class="sxs-lookup"><span data-stu-id="de0d1-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="de0d1-174">應用程式閘道依使用者代理程式分類的錯誤</span><span class="sxs-lookup"><span data-stu-id="de0d1-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="de0d1-175">應用程式閘道效能</span><span class="sxs-lookup"><span data-stu-id="de0d1-175">Application Gateway performance</span></span>
  * <span data-ttu-id="de0d1-176">應用程式閘道的主機健康狀態</span><span class="sxs-lookup"><span data-stu-id="de0d1-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="de0d1-177">應用程式閘道失敗要求的最大和第 95 個百分位數</span><span class="sxs-lookup"><span data-stu-id="de0d1-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Azure 應用程式閘道分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Azure 應用程式閘道分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="de0d1-180">在 [hello **Azure 應用程式閘道分析**儀表板，檢閱其中一個 hello 分頁中的 hello 摘要資訊，然後按一下其中一個 tooview 詳細 hello 記錄搜尋] 頁面上的資訊。</span><span class="sxs-lookup"><span data-stu-id="de0d1-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="de0d1-181">在任何 hello 記錄搜尋] 頁面中，您可以按時間、 詳細的結果和您的記錄搜尋記錄來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="de0d1-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="de0d1-182">您也可以篩選由 facet toonarrow hello 結果。</span><span class="sxs-lookup"><span data-stu-id="de0d1-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="de0d1-183">Log Analytics 中的 Azure 網路安全性群組分析解決方案</span><span class="sxs-lookup"><span data-stu-id="de0d1-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Azure 網路安全性群組分析符號](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="de0d1-185">網路安全性群組的相關支援下列記錄檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="de0d1-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="de0d1-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="de0d1-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="de0d1-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="de0d1-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="de0d1-188">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="de0d1-188">Install and configure hello solution</span></span>
<span data-ttu-id="de0d1-189">使用下列指示 tooinstall hello 和 hello Azure 網路分析解決方案設定：</span><span class="sxs-lookup"><span data-stu-id="de0d1-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="de0d1-190">啟用從 hello Azure 網路安全性群組分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="de0d1-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="de0d1-191">啟用診斷記錄的 hello[網路安全性群組](../virtual-network/virtual-network-nsg-manage-log.md)想 toomonitor 資源。</span><span class="sxs-lookup"><span data-stu-id="de0d1-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="de0d1-192">Azure 網路安全性群組中啟用診斷 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="de0d1-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="de0d1-193">在 [hello Azure 入口網站，瀏覽 toohello 網路安全性群組資源 toomonitor</span><span class="sxs-lookup"><span data-stu-id="de0d1-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="de0d1-194">選取*診斷記錄檔*tooopen hello 遵循頁面</span><span class="sxs-lookup"><span data-stu-id="de0d1-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure 網路安全性群組資源的影像](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="de0d1-196">按一下*開啟診斷*tooopen hello 遵循頁面</span><span class="sxs-lookup"><span data-stu-id="de0d1-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure 網路安全性群組資源的影像](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="de0d1-198">診斷，tooturn 按一下*上*下*狀態*</span><span class="sxs-lookup"><span data-stu-id="de0d1-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="de0d1-199">按一下 [hello] 核取方塊*傳送 tooLog 分析*</span><span class="sxs-lookup"><span data-stu-id="de0d1-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="de0d1-200">選取現有的 Log Analytics 工作區，或建立工作區</span><span class="sxs-lookup"><span data-stu-id="de0d1-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="de0d1-201">按一下下方的核取方塊 hello**記錄**hello 記錄類型 toocollect 的每個</span><span class="sxs-lookup"><span data-stu-id="de0d1-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="de0d1-202">按一下*儲存*tooenable hello 記錄診斷 tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="de0d1-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="de0d1-203">使用 PowerShell 啟用 Azure 網路診斷</span><span class="sxs-lookup"><span data-stu-id="de0d1-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="de0d1-204">下列 PowerShell 指令碼的 hello 提供的範例 tooenable 的網路安全性群組診斷記錄</span><span class="sxs-lookup"><span data-stu-id="de0d1-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="de0d1-205">使用 Azure 網路安全性群組分析</span><span class="sxs-lookup"><span data-stu-id="de0d1-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="de0d1-206">按一下 hello 之後**Azure 網路安全性群組分析**磚上 hello 概觀，您可以檢視記錄檔的摘要，而且然後鑽研 toodetails hello 下列類別：</span><span class="sxs-lookup"><span data-stu-id="de0d1-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="de0d1-207">網路安全性群組封鎖流量</span><span class="sxs-lookup"><span data-stu-id="de0d1-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="de0d1-208">網路安全性群組規則與封鎖流量</span><span class="sxs-lookup"><span data-stu-id="de0d1-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="de0d1-209">MAC 位址與封鎖流量</span><span class="sxs-lookup"><span data-stu-id="de0d1-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="de0d1-210">網路安全性群組允許流量</span><span class="sxs-lookup"><span data-stu-id="de0d1-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="de0d1-211">網路安全性群組規則與允許流量</span><span class="sxs-lookup"><span data-stu-id="de0d1-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="de0d1-212">MAC 位址與允許流量</span><span class="sxs-lookup"><span data-stu-id="de0d1-212">MAC addresses with allowed flows</span></span>

![Azure 網路安全性群組分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Azure 網路安全性群組分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="de0d1-215">在 [hello **Azure 網路安全性群組分析**儀表板，檢閱其中一個 hello 分頁中的 hello 摘要資訊，然後按一下其中一個 tooview 詳細 hello 記錄搜尋] 頁面上的資訊。</span><span class="sxs-lookup"><span data-stu-id="de0d1-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="de0d1-216">在任何 hello 記錄搜尋] 頁面中，您可以按時間、 詳細的結果和您的記錄搜尋記錄來檢視結果。</span><span class="sxs-lookup"><span data-stu-id="de0d1-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="de0d1-217">您也可以篩選由 facet toonarrow hello 結果。</span><span class="sxs-lookup"><span data-stu-id="de0d1-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="de0d1-218">從 hello 舊的網路分析解決方案移轉</span><span class="sxs-lookup"><span data-stu-id="de0d1-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="de0d1-219">在年 1 月 2017 hello 會支援從 Azure 應用程式閘道和 Azure 網路安全性群組 tooLog 分析變更傳送記錄檔的方式。</span><span class="sxs-lookup"><span data-stu-id="de0d1-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="de0d1-220">這些變更會提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="de0d1-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="de0d1-221">記錄檔寫入直接 tooLog 分析 hello 不需要 toouse 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="de0d1-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="de0d1-222">從記錄檔時的 hello 時間延遲越少產生 toothem 可以使用這個記錄分析</span><span class="sxs-lookup"><span data-stu-id="de0d1-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="de0d1-223">較少的組態步驟</span><span class="sxs-lookup"><span data-stu-id="de0d1-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="de0d1-224">所有 Azure 診斷類型的通用格式</span><span class="sxs-lookup"><span data-stu-id="de0d1-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="de0d1-225">toouse hello 更新方案：</span><span class="sxs-lookup"><span data-stu-id="de0d1-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="de0d1-226">設定診斷 toobe 寄件者直接 tooLog 分析 Azure 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="de0d1-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="de0d1-227">設定寄件者直接 tooLog 分析 Azure 網路安全性群組診斷 toobe</span><span class="sxs-lookup"><span data-stu-id="de0d1-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="de0d1-228">啟用 hello *Azure 應用程式閘道分析*和 hello *Azure 網路安全性群組分析*方案使用 hello 程序中所述[中的新增記錄分析解決方案hello 解決方案資源庫](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="de0d1-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="de0d1-229">更新任何已儲存的查詢、 儀表板或警示 toouse hello 新的資料類型</span><span class="sxs-lookup"><span data-stu-id="de0d1-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="de0d1-230">類型為 tooAzureDiagnostics。</span><span class="sxs-lookup"><span data-stu-id="de0d1-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="de0d1-231">您可以使用 hello ResourceType toofilter tooAzure 網路記錄檔。</span><span class="sxs-lookup"><span data-stu-id="de0d1-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="de0d1-232">不要使用：</span><span class="sxs-lookup"><span data-stu-id="de0d1-232">Instead of:</span></span> | <span data-ttu-id="de0d1-233">使用︰</span><span class="sxs-lookup"><span data-stu-id="de0d1-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="de0d1-234">如有後置字元的任何欄位\_s， \_d 或\_g hello 名稱，變更 hello 第一個字元 toolower 案例中</span><span class="sxs-lookup"><span data-stu-id="de0d1-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="de0d1-235">如有後的置字元的任何欄位\_o 在 [名稱] hello 資料會分成根據 hello 巢狀欄位名稱的個別欄位。</span><span class="sxs-lookup"><span data-stu-id="de0d1-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="de0d1-236">移除 hello *Azure 網路分析 （已過時）*方案。</span><span class="sxs-lookup"><span data-stu-id="de0d1-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="de0d1-237">如果您是使用 PowerShell，請使用 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="de0d1-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="de0d1-238">Hello 新方案中看不到 hello 變更之前，收集資料。</span><span class="sxs-lookup"><span data-stu-id="de0d1-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="de0d1-239">您可以繼續 tooquery，針對使用此資料 hello 舊的類型和欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="de0d1-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="de0d1-240">疑難排解</span><span class="sxs-lookup"><span data-stu-id="de0d1-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="de0d1-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de0d1-241">Next steps</span></span>
* <span data-ttu-id="de0d1-242">使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 Azure 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="de0d1-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
