---
title: "Microsoft Azure 中的計量概觀 | Microsoft Docs"
description: "Microsoft Azure 中的度量及其用法概觀"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 3aff83ab2c157a18f4af6200a79bae7e5d6f0ea2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="a65be-103">Microsoft Azure 中的度量概觀</span><span class="sxs-lookup"><span data-stu-id="a65be-103">Overview of metrics in Microsoft Azure</span></span>
<span data-ttu-id="a65be-104">本文章說明何謂 Microsoft Azure 中的度量、其優點，以及如何開始使用它們。</span><span class="sxs-lookup"><span data-stu-id="a65be-104">This article describes what metrics are in Microsoft Azure, their benefits, and how to start using them.</span></span>  

## <a name="what-are-metrics"></a><span data-ttu-id="a65be-105">何謂度量？</span><span class="sxs-lookup"><span data-stu-id="a65be-105">What are metrics?</span></span>
<span data-ttu-id="a65be-106">Azure 監視器可讓您取用遙測來查看您 Azure 工作負載的效能與健全狀況。</span><span class="sxs-lookup"><span data-stu-id="a65be-106">Azure Monitor enables you to consume telemetry to gain visibility into the performance and health of your workloads on Azure.</span></span> <span data-ttu-id="a65be-107">Azure 遙測資料最重要的類型是由大多數 Azure 資源所發出的度量 (也稱為效能計數器)。</span><span class="sxs-lookup"><span data-stu-id="a65be-107">The most important type of Azure telemetry data is the metrics (also called performance counters) emitted by most Azure resources.</span></span> <span data-ttu-id="a65be-108">Azure 監視器提供數種方式可設定及取用這些度量進行監視與疑難排解。</span><span class="sxs-lookup"><span data-stu-id="a65be-108">Azure Monitor provides several ways to configure and consume these metrics for monitoring and troubleshooting.</span></span>

## <a name="what-can-you-do-with-metrics"></a><span data-ttu-id="a65be-109">度量能讓您做什麼？</span><span class="sxs-lookup"><span data-stu-id="a65be-109">What can you do with metrics?</span></span>
<span data-ttu-id="a65be-110">度量是遙測的寶貴來源，可讓您執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="a65be-110">Metrics are a valuable source of telemetry and enable you to do the following tasks:</span></span>

* <span data-ttu-id="a65be-111">**追蹤資源** (例如 VM、網站或邏輯應用程式) 的效能，方法是在入口網站圖表上繪製其度量，並將該圖表釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="a65be-111">**Track the performance** of your resource (such as a VM, website, or logic app) by plotting its metrics on a portal chart and pinning that chart to a dashboard.</span></span>
* <span data-ttu-id="a65be-112">**取得問題的通知**，該問題在度量超出特定的閾值時會影響資源的效能。</span><span class="sxs-lookup"><span data-stu-id="a65be-112">**Get notified of an issue** that impacts the performance of your resource when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="a65be-113">**設定自動化動作**，例如自動調整資源，或在度量超出特定的閾值時觸發 Runbook。</span><span class="sxs-lookup"><span data-stu-id="a65be-113">**Configure automated actions**, such as autoscaling a resource or firing a runbook when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="a65be-114">**執行進階分析**或報告您資源的效能或使用量趨勢。</span><span class="sxs-lookup"><span data-stu-id="a65be-114">**Perform advanced analytics** or reporting on performance or usage trends of your resource.</span></span>
* <span data-ttu-id="a65be-115">**封存**您資源的效能或健全狀況歷程記錄以用於**相容性或稽核**。</span><span class="sxs-lookup"><span data-stu-id="a65be-115">**Archive** the performance or health history of your resource **for compliance or auditing** purposes.</span></span>

## <a name="what-are-the-characteristics-of-metrics"></a><span data-ttu-id="a65be-116">度量有哪些特性？</span><span class="sxs-lookup"><span data-stu-id="a65be-116">What are the characteristics of metrics?</span></span>
<span data-ttu-id="a65be-117">度量具有下列特性︰</span><span class="sxs-lookup"><span data-stu-id="a65be-117">Metrics have the following characteristics:</span></span>

* <span data-ttu-id="a65be-118">所有度量皆有**一分鐘的頻率**。</span><span class="sxs-lookup"><span data-stu-id="a65be-118">All metrics have **one-minute frequency**.</span></span> <span data-ttu-id="a65be-119">您每分鐘會從您的資源收到度量值，讓您可幾乎即時地看到資源的狀態和健全狀況。</span><span class="sxs-lookup"><span data-stu-id="a65be-119">You receive a metric value every minute from your resource, giving you near real-time visibility into the state and health of your resource.</span></span>
* <span data-ttu-id="a65be-120">度量**可立即使用**。</span><span class="sxs-lookup"><span data-stu-id="a65be-120">Metrics are **available immediately**.</span></span> <span data-ttu-id="a65be-121">您不需要選擇加入或設定其他診斷。</span><span class="sxs-lookup"><span data-stu-id="a65be-121">You don't need to opt in or set up additional diagnostics.</span></span>
* <span data-ttu-id="a65be-122">您可以針對每個度量存取 **30 天的歷程記錄** 。</span><span class="sxs-lookup"><span data-stu-id="a65be-122">You can access **30 days of history** for each metric.</span></span> <span data-ttu-id="a65be-123">您可以快速查看最近和每個月的資源效能或健全狀況趨勢。</span><span class="sxs-lookup"><span data-stu-id="a65be-123">You can quickly look at the recent and monthly trends in the performance or health of your resource.</span></span>

<span data-ttu-id="a65be-124">您也可以：</span><span class="sxs-lookup"><span data-stu-id="a65be-124">You can also:</span></span>

* <span data-ttu-id="a65be-125">設定當度量超出您設定的閾值時，**會傳送通知或採取自動化動作的度量警示規則**。</span><span class="sxs-lookup"><span data-stu-id="a65be-125">Configure a metric **alert rule that sends a notification or takes automated action** when the metric crosses the threshold that you have set.</span></span> <span data-ttu-id="a65be-126">自動調整是一種特殊的自動化動作，可讓您相應放大資源來符合您網站或計算資源的連入要求或負載。</span><span class="sxs-lookup"><span data-stu-id="a65be-126">Autoscale is a special automated action that enables you to scale out your resource to meet incoming requests or loads on your website or computing resources.</span></span> <span data-ttu-id="a65be-127">您可以設定自動調整設定規則，根據超出閾值的度量相應縮小或放大。</span><span class="sxs-lookup"><span data-stu-id="a65be-127">You can configure an Autoscale setting rule to scale in or out based on a metric crossing a threshold.</span></span>

* <span data-ttu-id="a65be-128">**路由**所有度量至 Application Insights 或 Log Analytics (OMS)，以啟用即時分析、搜尋及自訂來自您資源的度量資料警示。</span><span class="sxs-lookup"><span data-stu-id="a65be-128">**Route** all metrics Application Insights or Log Analytics (OMS) to enable instant analytics, search, and custom alerting on metrics data from your resources.</span></span> <span data-ttu-id="a65be-129">您也可以串流度量到事件中樞，可讓您將它們路由至 Azure 串流分析或自訂應用程式，以進行近乎即時的分析。</span><span class="sxs-lookup"><span data-stu-id="a65be-129">You can also stream metrics to an Event Hub, enabling you to then route them to Azure Stream Analytics or to custom apps for near-real time analysis.</span></span> <span data-ttu-id="a65be-130">您需要設定使用診斷設定的事件中樞串流。</span><span class="sxs-lookup"><span data-stu-id="a65be-130">You set up Event Hub streaming using diagnostic settings.</span></span>

* <span data-ttu-id="a65be-131">**將度量封存至儲存體**來延長保留時間或將度量用於離線報告。</span><span class="sxs-lookup"><span data-stu-id="a65be-131">**Archive metrics to storage** for longer retention or use them for offline reporting.</span></span> <span data-ttu-id="a65be-132">當您設定資源的診斷設定時，可以將度量路由至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a65be-132">You can route your metrics to Azure Blob storage when you configure diagnostic settings for your resource.</span></span>

* <span data-ttu-id="a65be-133">當您選取資源並在圖表上繪製度量時，透過 Azure 入口網站輕鬆探索、存取及**檢視所有度量**。</span><span class="sxs-lookup"><span data-stu-id="a65be-133">Easily discover, access, and **view all metrics** via the Azure portal when you select a resource and plot the metrics on a chart.</span></span>

* <span data-ttu-id="a65be-134">透過新的 Azure 監視器 REST API **取用**度量。</span><span class="sxs-lookup"><span data-stu-id="a65be-134">**Consume** the metrics via the new Azure Monitor REST APIs.</span></span>

* <span data-ttu-id="a65be-135">使用 PowerShell Cmdlet 或跨平台 REST API **查詢**度量。</span><span class="sxs-lookup"><span data-stu-id="a65be-135">**Query** metrics by using the PowerShell cmdlets or the Cross-Platform REST API.</span></span>

  ![Azure 監視器中的度量路由](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-the-portal"></a><span data-ttu-id="a65be-137">透過入口網站存取度量</span><span class="sxs-lookup"><span data-stu-id="a65be-137">Access metrics via the portal</span></span>
<span data-ttu-id="a65be-138">以下是如何使用 Azure 入口網站建立度量圖表的快速逐步解說。</span><span class="sxs-lookup"><span data-stu-id="a65be-138">Following is a quick walkthrough of how to create a metric chart by using the Azure portal.</span></span>

### <a name="to-view-metrics-after-creating-a-resource"></a><span data-ttu-id="a65be-139">建立資源之後檢視度量</span><span class="sxs-lookup"><span data-stu-id="a65be-139">To view metrics after creating a resource</span></span>
1. <span data-ttu-id="a65be-140">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a65be-140">Open the Azure portal.</span></span>
2. <span data-ttu-id="a65be-141">建立 Azure App Service 網站。</span><span class="sxs-lookup"><span data-stu-id="a65be-141">Create an Azure App Service website.</span></span>
3. <span data-ttu-id="a65be-142">建立網站之後，移至網站的 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a65be-142">After you create a website, go to the **Overview** blade of the website.</span></span>
4. <span data-ttu-id="a65be-143">您可以用 [監視] 圖格的形式檢視新度量。</span><span class="sxs-lookup"><span data-stu-id="a65be-143">You can view new metrics as a **Monitoring** tile.</span></span> <span data-ttu-id="a65be-144">您可以接著編輯圖格並選取更多度量。</span><span class="sxs-lookup"><span data-stu-id="a65be-144">You can then edit the tile and select more metrics.</span></span>

   ![Azure 監視器中的資源度量](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="to-access-all-metrics-in-a-single-place"></a><span data-ttu-id="a65be-146">在單一位置存取所有度量</span><span class="sxs-lookup"><span data-stu-id="a65be-146">To access all metrics in a single place</span></span>
1. <span data-ttu-id="a65be-147">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a65be-147">Open the Azure portal.</span></span>
2. <span data-ttu-id="a65be-148">瀏覽至新的 [監視] 索引標籤，然後選取其下方的 [度量] 選項。</span><span class="sxs-lookup"><span data-stu-id="a65be-148">Navigate to the new **Monitor** tab, and then and select the **Metrics** option underneath it.</span></span>
3. <span data-ttu-id="a65be-149">從下拉式清單選取您的訂用帳戶、資源群組和資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="a65be-149">Select your subscription, resource group, and the name of the resource from the drop-down list.</span></span>
4. <span data-ttu-id="a65be-150">檢視可用的度量清單。</span><span class="sxs-lookup"><span data-stu-id="a65be-150">View the available metrics list.</span></span> <span data-ttu-id="a65be-151">然後選取您感興趣的度量並繪製它。</span><span class="sxs-lookup"><span data-stu-id="a65be-151">Then select the metric you are interested in and plot it.</span></span>
5. <span data-ttu-id="a65be-152">您可以按一下右上角的 [釘選]，將它釘選至儀表板。</span><span class="sxs-lookup"><span data-stu-id="a65be-152">You can pin it to the dashboard by clicking the pin on the upper-right corner.</span></span>

   ![在 Azure 監視器中的單一位置存取所有度量](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> <span data-ttu-id="a65be-154">您可以從 VM (以 Azure Resource Manager 為基礎) 存取主機層級的度量和虛擬機器擴展集，而不需要任何額外的診斷設定。</span><span class="sxs-lookup"><span data-stu-id="a65be-154">You can access host-level metrics from VMs (Azure Resource Manager-based) and virtual machine scale sets without any additional diagnostic setup.</span></span> <span data-ttu-id="a65be-155">這些新的主機層級度量可供 Windows 和 Linux 執行個體使用。</span><span class="sxs-lookup"><span data-stu-id="a65be-155">These new host-level metrics are available for Windows and Linux instances.</span></span> <span data-ttu-id="a65be-156">這些度量不會與您在 VM 或虛擬機器擴展集上開啟 Azure 診斷時具有存取權的客體 OS 層級度量混淆。</span><span class="sxs-lookup"><span data-stu-id="a65be-156">These metrics are not to be confused with the Guest-OS-level metrics that you have access to when you turn on Azure Diagnostics on your VMs or virtual machine scale sets.</span></span> <span data-ttu-id="a65be-157">若要深入了解如何設定診斷，請參閱[什麼是 Microsoft Azure 診斷](../azure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="a65be-157">To learn more about configuring Diagnostics, see [What is Microsoft Azure Diagnostics](../azure-diagnostics.md).</span></span>
>
>

## <a name="access-metrics-via-the-rest-api"></a><span data-ttu-id="a65be-158">透過 REST API 存取度量</span><span class="sxs-lookup"><span data-stu-id="a65be-158">Access metrics via the REST API</span></span>
<span data-ttu-id="a65be-159">可以透過 Azure 監視器 API 存取 Azure 度量。</span><span class="sxs-lookup"><span data-stu-id="a65be-159">Azure Metrics can be accessed via the Azure Monitor APIs.</span></span> <span data-ttu-id="a65be-160">有兩個 API 可協助您探索及存取度量：</span><span class="sxs-lookup"><span data-stu-id="a65be-160">There are two APIs that help you discover and access metrics:</span></span>

* <span data-ttu-id="a65be-161">使用 [Azure 監視器度量定義 REST API](https://msdn.microsoft.com/library/mt743621.aspx) 來存取可供服務使用的度量清單。</span><span class="sxs-lookup"><span data-stu-id="a65be-161">Use the [Azure Monitor Metric definitions REST API](https://msdn.microsoft.com/library/mt743621.aspx) to access the list of metrics that are available for a service.</span></span>
* <span data-ttu-id="a65be-162">使用 [Azure 監視器度量 REST API](https://msdn.microsoft.com/library/mt743622.aspx) 來存取實際的度量資料。</span><span class="sxs-lookup"><span data-stu-id="a65be-162">Use the [Azure Monitor Metrics REST API](https://msdn.microsoft.com/library/mt743622.aspx) to access the actual metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="a65be-163">本文章透過 Azure 資源的 [新度量 API](https://msdn.microsoft.com/library/dn931930.aspx) 涵蓋度量。</span><span class="sxs-lookup"><span data-stu-id="a65be-163">This article covers the metrics via the [new API for metrics](https://msdn.microsoft.com/library/dn931930.aspx) for Azure resources.</span></span> <span data-ttu-id="a65be-164">新度量定義 API 的 API 版本為 2016-03-01，度量 API 的版本為 2016-09-01。</span><span class="sxs-lookup"><span data-stu-id="a65be-164">The API version for the new metric definitions API is 2016-03-01 and the version for metrics API is 2016-09-01.</span></span> <span data-ttu-id="a65be-165">可以使用 API 版本 2014-04-01 存取舊版的度量定義和度量。</span><span class="sxs-lookup"><span data-stu-id="a65be-165">The legacy metric definitions and metrics can be accessed with the API version 2014-04-01.</span></span>
>
>

<span data-ttu-id="a65be-166">如需使用 Azure 監視器 REST API 的更詳細逐步解說，請參閱 [Azure 監視器 REST API 逐步解說](monitoring-rest-api-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="a65be-166">For a more detailed walkthrough using the Azure Monitor REST APIs, see [Azure Monitor REST API walkthrough](monitoring-rest-api-walkthrough.md).</span></span>

## <a name="export-metrics"></a><span data-ttu-id="a65be-167">匯出度量</span><span class="sxs-lookup"><span data-stu-id="a65be-167">Export metrics</span></span>
<span data-ttu-id="a65be-168">您可以移至 [監視] 索引標籤下的 [診斷設定] 刀鋒視窗，並檢視度量的匯出選項。</span><span class="sxs-lookup"><span data-stu-id="a65be-168">You can go to the **Diagnostics settings** blade under the **Monitor** tab and view the export options for metrics.</span></span> <span data-ttu-id="a65be-169">針對本文中先前所述的使用案例，您可以選取要傳送至 Blob 儲存體、Azure 事件中樞或 OMS 的度量 (和診斷記錄檔)。</span><span class="sxs-lookup"><span data-stu-id="a65be-169">You can select metrics (and diagnostic logs) to be routed to Blob storage, to Azure Event Hubs, or to OMS for use-cases that were mentioned previously in this article.</span></span>

 ![在 Azure 監視器中匯出度量選項](./media/monitoring-overview-metrics/MetricsOverview3.png)

<span data-ttu-id="a65be-171">您可以透過 Resource Manager 範本、[PowerShell](insights-powershell-samples.md)、[Azure CLI](insights-cli-samples.md) 或 [REST API](https://msdn.microsoft.com/library/dn931943.aspx) 來進行設定。</span><span class="sxs-lookup"><span data-stu-id="a65be-171">You can configure this via Resource Manager templates, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), or [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span>

## <a name="take-action-on-metrics"></a><span data-ttu-id="a65be-172">對度量採取動作</span><span class="sxs-lookup"><span data-stu-id="a65be-172">Take action on metrics</span></span>
<span data-ttu-id="a65be-173">若要收到通知或對度量資料採取自動化的動作，您可以設定警示規則或 [自動調整] 設定。</span><span class="sxs-lookup"><span data-stu-id="a65be-173">To receive notifications or take automated actions on metric data, you can configure alert rules or Autoscale settings.</span></span>

### <a name="configure-alert-rules"></a><span data-ttu-id="a65be-174">設定警示規則</span><span class="sxs-lookup"><span data-stu-id="a65be-174">Configure alert rules</span></span>
<span data-ttu-id="a65be-175">您可以設定度量的警示規則。</span><span class="sxs-lookup"><span data-stu-id="a65be-175">You can configure alert rules on metrics.</span></span> <span data-ttu-id="a65be-176">這些警示規則可以檢查度量是否已超過某個臨界值，</span><span class="sxs-lookup"><span data-stu-id="a65be-176">These alert rules can check if a metric has crossed a certain threshold.</span></span> <span data-ttu-id="a65be-177">然後透過電子郵件通知您，或引發可用來執行任何自訂指令碼的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="a65be-177">They can then notify you via email or fire a webhook that can be used to run any custom script.</span></span> <span data-ttu-id="a65be-178">您也可以使用 Webhook 來設定第三方產品整合。</span><span class="sxs-lookup"><span data-stu-id="a65be-178">You can also use the webhook to configure third-party product integrations.</span></span>

 ![Azure 監視器中的度量和警示規則](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a><span data-ttu-id="a65be-180">自動調整您的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="a65be-180">Autoscale your Azure resources</span></span>
<span data-ttu-id="a65be-181">某些 Azure 資源可支援相應放大或縮小多個執行個體，以便處理您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="a65be-181">Some Azure resources support the scaling out or in of multiple instances to handle your workloads.</span></span> <span data-ttu-id="a65be-182">自動調整可套用至 App Service (Web Apps)、虛擬機器擴展集和傳統 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="a65be-182">Autoscale applies to App Service (Web Apps), virtual machine scale sets, and classic Azure Cloud Services.</span></span> <span data-ttu-id="a65be-183">您可以設定自動調整規則，以在影響您工作負載的特定度量超出您所指定的閾值時相應放大或縮小。</span><span class="sxs-lookup"><span data-stu-id="a65be-183">You can configure Autoscale rules to scale out or in when a certain metric that impacts your workload crosses a threshold that you specify.</span></span> <span data-ttu-id="a65be-184">如需詳細資訊，請參閱 [自動調整的概觀](monitoring-overview-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="a65be-184">For more information, see [Overview of autoscaling](monitoring-overview-autoscale.md).</span></span>

 ![Azure 監視器中的度量和自動調整](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a><span data-ttu-id="a65be-186">了解支援的服務和度量</span><span class="sxs-lookup"><span data-stu-id="a65be-186">Learn about supported services and metrics</span></span>
<span data-ttu-id="a65be-187">Azure 監視器是新的度量基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a65be-187">Azure Monitor is a new metrics infrastructure.</span></span> <span data-ttu-id="a65be-188">它支援下列 Azure 入口網站中的 Azure 服務和新版本的 Azure 監視器 API︰</span><span class="sxs-lookup"><span data-stu-id="a65be-188">It supports the following Azure services in the Azure portal and the new version of the Azure Monitor API:</span></span>

* <span data-ttu-id="a65be-189">VM (Azure Resource Manager 架構)</span><span class="sxs-lookup"><span data-stu-id="a65be-189">VMs (Azure Resource Manager-based)</span></span>
* <span data-ttu-id="a65be-190">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="a65be-190">Virtual machine scale sets</span></span>
* <span data-ttu-id="a65be-191">Batch</span><span class="sxs-lookup"><span data-stu-id="a65be-191">Batch</span></span>
* <span data-ttu-id="a65be-192">事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="a65be-192">Event Hubs namespace</span></span>
* <span data-ttu-id="a65be-193">服務匯流排命名空間 (僅限進階 SKU)</span><span class="sxs-lookup"><span data-stu-id="a65be-193">Service Bus namespace (premium SKU only)</span></span>
* <span data-ttu-id="a65be-194">SQL Database (第 12 版)</span><span class="sxs-lookup"><span data-stu-id="a65be-194">SQL Database (version 12)</span></span>
* <span data-ttu-id="a65be-195">SQL 彈性集區</span><span class="sxs-lookup"><span data-stu-id="a65be-195">Elastic SQL Pool</span></span>
* <span data-ttu-id="a65be-196">網站</span><span class="sxs-lookup"><span data-stu-id="a65be-196">Websites</span></span>
* <span data-ttu-id="a65be-197">Web 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="a65be-197">Web server farms</span></span>
* <span data-ttu-id="a65be-198">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a65be-198">Logic Apps</span></span>
* <span data-ttu-id="a65be-199">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="a65be-199">IoT hubs</span></span>
* <span data-ttu-id="a65be-200">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="a65be-200">Redis Cache</span></span>
* <span data-ttu-id="a65be-201">網路：應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a65be-201">Networking: Application gateways</span></span>
* <span data-ttu-id="a65be-202">搜尋</span><span class="sxs-lookup"><span data-stu-id="a65be-202">Search</span></span>

<span data-ttu-id="a65be-203">您可以在 [Azure 監視器度量--每個資源類型支援的度量](monitoring-supported-metrics.md)檢視所有支援服務及其度量的詳細清單。</span><span class="sxs-lookup"><span data-stu-id="a65be-203">You can view a detailed list of all the supported services and their metrics at [Azure Monitor metrics--supported metrics per resource type](monitoring-supported-metrics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a65be-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a65be-204">Next steps</span></span>
<span data-ttu-id="a65be-205">請參閱這整篇文章的連結。</span><span class="sxs-lookup"><span data-stu-id="a65be-205">Refer to the links throughout this article.</span></span> <span data-ttu-id="a65be-206">此外，請了解：</span><span class="sxs-lookup"><span data-stu-id="a65be-206">Additionally, learn about:</span></span>  

* [<span data-ttu-id="a65be-207">自動調整規模的常用計量</span><span class="sxs-lookup"><span data-stu-id="a65be-207">Common metrics for autoscaling</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="a65be-208">如何建立警示規則</span><span class="sxs-lookup"><span data-stu-id="a65be-208">How to create alert rules</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="a65be-209">使用 Log Analytics 分析來自 Azure 儲存體的記錄</span><span class="sxs-lookup"><span data-stu-id="a65be-209">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
