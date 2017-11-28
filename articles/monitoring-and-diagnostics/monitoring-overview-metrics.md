---
title: "在 Microsoft Azure 中的度量的 aaaOverview |Microsoft 文件"
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
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="1489e-103">Microsoft Azure 中的度量概觀</span><span class="sxs-lookup"><span data-stu-id="1489e-103">Overview of metrics in Microsoft Azure</span></span>
<span data-ttu-id="1489e-104">本文章說明度量資訊是在 Microsoft Azure 中，其優點，以及如何使用它們的 toostart。</span><span class="sxs-lookup"><span data-stu-id="1489e-104">This article describes what metrics are in Microsoft Azure, their benefits, and how toostart using them.</span></span>  

## <a name="what-are-metrics"></a><span data-ttu-id="1489e-105">何謂度量？</span><span class="sxs-lookup"><span data-stu-id="1489e-105">What are metrics?</span></span>
<span data-ttu-id="1489e-106">Azure 監視器可讓您 tooconsume 遙測 toogain 掌握 hello 效能和您的工作負載在 Azure 上的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="1489e-106">Azure Monitor enables you tooconsume telemetry toogain visibility into hello performance and health of your workloads on Azure.</span></span> <span data-ttu-id="1489e-107">hello Azure 的遙測資料的最重要型別是 hello 度量 （也稱為效能計數器） 發出的大部分的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1489e-107">hello most important type of Azure telemetry data is hello metrics (also called performance counters) emitted by most Azure resources.</span></span> <span data-ttu-id="1489e-108">Azure 監視提供數種方式 tooconfigure，並使用監視和疑難排解這些度量資訊。</span><span class="sxs-lookup"><span data-stu-id="1489e-108">Azure Monitor provides several ways tooconfigure and consume these metrics for monitoring and troubleshooting.</span></span>

## <a name="what-can-you-do-with-metrics"></a><span data-ttu-id="1489e-109">度量能讓您做什麼？</span><span class="sxs-lookup"><span data-stu-id="1489e-109">What can you do with metrics?</span></span>
<span data-ttu-id="1489e-110">度量是重要的遙測資料來源，並啟用您 toodo hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="1489e-110">Metrics are a valuable source of telemetry and enable you toodo hello following tasks:</span></span>

* <span data-ttu-id="1489e-111">**追蹤 hello 效能**之資源 （例如 VM、 網站或邏輯應用程式） 繪製其入口網站的圖表上的度量，釘選圖表 tooa 儀表板。</span><span class="sxs-lookup"><span data-stu-id="1489e-111">**Track hello performance** of your resource (such as a VM, website, or logic app) by plotting its metrics on a portal chart and pinning that chart tooa dashboard.</span></span>
* <span data-ttu-id="1489e-112">**取得問題的通知**影響 hello 之資源的效能，當度量超出某個臨界值時。</span><span class="sxs-lookup"><span data-stu-id="1489e-112">**Get notified of an issue** that impacts hello performance of your resource when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="1489e-113">**設定自動化動作**，例如自動調整資源，或在度量超出特定的閾值時觸發 Runbook。</span><span class="sxs-lookup"><span data-stu-id="1489e-113">**Configure automated actions**, such as autoscaling a resource or firing a runbook when a metric crosses a certain threshold.</span></span>
* <span data-ttu-id="1489e-114">**執行進階分析**或報告您資源的效能或使用量趨勢。</span><span class="sxs-lookup"><span data-stu-id="1489e-114">**Perform advanced analytics** or reporting on performance or usage trends of your resource.</span></span>
* <span data-ttu-id="1489e-115">**封存**hello 之資源的效能或健全狀況歷程記錄**相容性或稽核**用途。</span><span class="sxs-lookup"><span data-stu-id="1489e-115">**Archive** hello performance or health history of your resource **for compliance or auditing** purposes.</span></span>

## <a name="what-are-hello-characteristics-of-metrics"></a><span data-ttu-id="1489e-116">度量的 hello 特性有哪些？</span><span class="sxs-lookup"><span data-stu-id="1489e-116">What are hello characteristics of metrics?</span></span>
<span data-ttu-id="1489e-117">度量具有下列特性的 hello:</span><span class="sxs-lookup"><span data-stu-id="1489e-117">Metrics have hello following characteristics:</span></span>

* <span data-ttu-id="1489e-118">所有度量皆有**一分鐘的頻率**。</span><span class="sxs-lookup"><span data-stu-id="1489e-118">All metrics have **one-minute frequency**.</span></span> <span data-ttu-id="1489e-119">您收到公制值每隔一分鐘從您的資源，提供您附近 hello 狀態和健全狀況之資源的即時可視性。</span><span class="sxs-lookup"><span data-stu-id="1489e-119">You receive a metric value every minute from your resource, giving you near real-time visibility into hello state and health of your resource.</span></span>
* <span data-ttu-id="1489e-120">度量**可立即使用**。</span><span class="sxs-lookup"><span data-stu-id="1489e-120">Metrics are **available immediately**.</span></span> <span data-ttu-id="1489e-121">您不需要 tooopt 中的，或將額外的診斷設定。</span><span class="sxs-lookup"><span data-stu-id="1489e-121">You don't need tooopt in or set up additional diagnostics.</span></span>
* <span data-ttu-id="1489e-122">您可以針對每個度量存取 **30 天的歷程記錄** 。</span><span class="sxs-lookup"><span data-stu-id="1489e-122">You can access **30 days of history** for each metric.</span></span> <span data-ttu-id="1489e-123">您可以快速查看 hello 最近和每月的趨勢 hello 效能或資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="1489e-123">You can quickly look at hello recent and monthly trends in hello performance or health of your resource.</span></span>

<span data-ttu-id="1489e-124">您也可以：</span><span class="sxs-lookup"><span data-stu-id="1489e-124">You can also:</span></span>

* <span data-ttu-id="1489e-125">設定度量**警示規則，傳送通知或採用自動化動作**hello 度量超出您設定的 hello 閾值的時。</span><span class="sxs-lookup"><span data-stu-id="1489e-125">Configure a metric **alert rule that sends a notification or takes automated action** when hello metric crosses hello threshold that you have set.</span></span> <span data-ttu-id="1489e-126">自動調整規模是一種特殊的自動化的動作，可讓 tooscale 資源 toomeet 的內送要求，或在您的網站或運算資源時載入。</span><span class="sxs-lookup"><span data-stu-id="1489e-126">Autoscale is a special automated action that enables you tooscale out your resource toomeet incoming requests or loads on your website or computing resources.</span></span> <span data-ttu-id="1489e-127">您可以設定自動調整規模設定規則 tooscale in 或 out 根據跨越臨界值的度量。</span><span class="sxs-lookup"><span data-stu-id="1489e-127">You can configure an Autoscale setting rule tooscale in or out based on a metric crossing a threshold.</span></span>

* <span data-ttu-id="1489e-128">**路由**所有度量 Application Insights 或記錄分析 (OMS) tooenable 立即分析、 搜尋和自訂警示的度量資料是來自您的資源。</span><span class="sxs-lookup"><span data-stu-id="1489e-128">**Route** all metrics Application Insights or Log Analytics (OMS) tooenable instant analytics, search, and custom alerting on metrics data from your resources.</span></span> <span data-ttu-id="1489e-129">您也可以串流處理度量 tooan 事件中心，讓您 toothen 將它們路由傳送 tooAzure 串流分析或 toocustom 幾乎是即時分析的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1489e-129">You can also stream metrics tooan Event Hub, enabling you toothen route them tooAzure Stream Analytics or toocustom apps for near-real time analysis.</span></span> <span data-ttu-id="1489e-130">您需要設定使用診斷設定的事件中樞串流。</span><span class="sxs-lookup"><span data-stu-id="1489e-130">You set up Event Hub streaming using diagnostic settings.</span></span>

* <span data-ttu-id="1489e-131">**封存計量 toostorage**較長的保留或用於產生離線報表。</span><span class="sxs-lookup"><span data-stu-id="1489e-131">**Archive metrics toostorage** for longer retention or use them for offline reporting.</span></span> <span data-ttu-id="1489e-132">當您設定您為資源的診斷設定時，您可以路由您度量 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="1489e-132">You can route your metrics tooAzure Blob storage when you configure diagnostic settings for your resource.</span></span>

* <span data-ttu-id="1489e-133">輕鬆地探索，存取，以及**檢視的所有度量**透過 hello Azure 入口網站，當您選取的資源，並繪製 hello 度量圖表上的。</span><span class="sxs-lookup"><span data-stu-id="1489e-133">Easily discover, access, and **view all metrics** via hello Azure portal when you select a resource and plot hello metrics on a chart.</span></span>

* <span data-ttu-id="1489e-134">**取用**透過 hello 度量 hello 新的 Azure 監視 REST Api。</span><span class="sxs-lookup"><span data-stu-id="1489e-134">**Consume** hello metrics via hello new Azure Monitor REST APIs.</span></span>

* <span data-ttu-id="1489e-135">**查詢**度量使用 hello PowerShell cmdlet 或 hello 跨平台 REST API。</span><span class="sxs-lookup"><span data-stu-id="1489e-135">**Query** metrics by using hello PowerShell cmdlets or hello Cross-Platform REST API.</span></span>

  ![Azure 監視器中的度量路由](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a><span data-ttu-id="1489e-137">透過 hello 入口網站存取的度量</span><span class="sxs-lookup"><span data-stu-id="1489e-137">Access metrics via hello portal</span></span>
<span data-ttu-id="1489e-138">以下是如何 toocreate 度量圖表使用 hello Azure 入口網站的快速逐步解說。</span><span class="sxs-lookup"><span data-stu-id="1489e-138">Following is a quick walkthrough of how toocreate a metric chart by using hello Azure portal.</span></span>

### <a name="tooview-metrics-after-creating-a-resource"></a><span data-ttu-id="1489e-139">建立資源之後 tooview 度量</span><span class="sxs-lookup"><span data-stu-id="1489e-139">tooview metrics after creating a resource</span></span>
1. <span data-ttu-id="1489e-140">開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1489e-140">Open hello Azure portal.</span></span>
2. <span data-ttu-id="1489e-141">建立 Azure App Service 網站。</span><span class="sxs-lookup"><span data-stu-id="1489e-141">Create an Azure App Service website.</span></span>
3. <span data-ttu-id="1489e-142">建立網站之後，請繼續 toohello**概觀**hello 網站的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1489e-142">After you create a website, go toohello **Overview** blade of hello website.</span></span>
4. <span data-ttu-id="1489e-143">您可以用 [監視] 圖格的形式檢視新度量。</span><span class="sxs-lookup"><span data-stu-id="1489e-143">You can view new metrics as a **Monitoring** tile.</span></span> <span data-ttu-id="1489e-144">然後，您可以編輯 hello 磚，並選取多個度量。</span><span class="sxs-lookup"><span data-stu-id="1489e-144">You can then edit hello tile and select more metrics.</span></span>

   ![Azure 監視器中的資源度量](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a><span data-ttu-id="1489e-146">tooaccess 在單一位置的所有標準</span><span class="sxs-lookup"><span data-stu-id="1489e-146">tooaccess all metrics in a single place</span></span>
1. <span data-ttu-id="1489e-147">開啟 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1489e-147">Open hello Azure portal.</span></span>
2. <span data-ttu-id="1489e-148">瀏覽新 toohello**監視器**索引標籤，然後再與選取的 hello**度量**其下方的選項。</span><span class="sxs-lookup"><span data-stu-id="1489e-148">Navigate toohello new **Monitor** tab, and then and select hello **Metrics** option underneath it.</span></span>
3. <span data-ttu-id="1489e-149">從 hello 下拉式清單中，選取您的訂用帳戶、 資源群組和 hello hello 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="1489e-149">Select your subscription, resource group, and hello name of hello resource from hello drop-down list.</span></span>
4. <span data-ttu-id="1489e-150">檢視 hello 可用的度量清單。</span><span class="sxs-lookup"><span data-stu-id="1489e-150">View hello available metrics list.</span></span> <span data-ttu-id="1489e-151">然後選取您感興趣，並繪製它的 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="1489e-151">Then select hello metric you are interested in and plot it.</span></span>
5. <span data-ttu-id="1489e-152">您可以釘選它 toohello 儀表板按一下 hello hello 右上角的釘選。</span><span class="sxs-lookup"><span data-stu-id="1489e-152">You can pin it toohello dashboard by clicking hello pin on hello upper-right corner.</span></span>

   ![在 Azure 監視器中的單一位置存取所有度量](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> <span data-ttu-id="1489e-154">您可以從 VM (以 Azure Resource Manager 為基礎) 存取主機層級的度量和虛擬機器擴展集，而不需要任何額外的診斷設定。</span><span class="sxs-lookup"><span data-stu-id="1489e-154">You can access host-level metrics from VMs (Azure Resource Manager-based) and virtual machine scale sets without any additional diagnostic setup.</span></span> <span data-ttu-id="1489e-155">這些新的主機層級度量可供 Windows 和 Linux 執行個體使用。</span><span class="sxs-lookup"><span data-stu-id="1489e-155">These new host-level metrics are available for Windows and Linux instances.</span></span> <span data-ttu-id="1489e-156">這些度量不 toobe hello 您擁有存取 toowhen 您開啟 Azure 診斷 Vm 或虛擬機器擴展集上的客體作業系統層級度量的問題感到困惑。</span><span class="sxs-lookup"><span data-stu-id="1489e-156">These metrics are not toobe confused with hello Guest-OS-level metrics that you have access toowhen you turn on Azure Diagnostics on your VMs or virtual machine scale sets.</span></span> <span data-ttu-id="1489e-157">toolearn 進一步了解設定診斷功能，請參閱[何謂 Microsoft Azure 診斷](../azure-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="1489e-157">toolearn more about configuring Diagnostics, see [What is Microsoft Azure Diagnostics](../azure-diagnostics.md).</span></span>
>
>

## <a name="access-metrics-via-hello-rest-api"></a><span data-ttu-id="1489e-158">透過 hello REST API 存取度量</span><span class="sxs-lookup"><span data-stu-id="1489e-158">Access metrics via hello REST API</span></span>
<span data-ttu-id="1489e-159">可透過 hello Azure 監視應用程式開發介面存取 azure 度量。</span><span class="sxs-lookup"><span data-stu-id="1489e-159">Azure Metrics can be accessed via hello Azure Monitor APIs.</span></span> <span data-ttu-id="1489e-160">有兩個 API 可協助您探索及存取度量：</span><span class="sxs-lookup"><span data-stu-id="1489e-160">There are two APIs that help you discover and access metrics:</span></span>

* <span data-ttu-id="1489e-161">使用 hello [Azure 監視的標準定義 REST API](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello 度量可用服務清單。</span><span class="sxs-lookup"><span data-stu-id="1489e-161">Use hello [Azure Monitor Metric definitions REST API](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello list of metrics that are available for a service.</span></span>
* <span data-ttu-id="1489e-162">使用 hello [Azure 監視度量 REST API](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello 實際度量資料。</span><span class="sxs-lookup"><span data-stu-id="1489e-162">Use hello [Azure Monitor Metrics REST API](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello actual metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="1489e-163">本文章涵蓋透過 hello hello 度量[標準的新 API](https://msdn.microsoft.com/library/dn931930.aspx) Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1489e-163">This article covers hello metrics via hello [new API for metrics](https://msdn.microsoft.com/library/dn931930.aspx) for Azure resources.</span></span> <span data-ttu-id="1489e-164">hello hello 新標準定義 API 的 API 版本是 2016年-03-01 和標準應用程式開發介面的 hello 版本是 2016年-09-01。</span><span class="sxs-lookup"><span data-stu-id="1489e-164">hello API version for hello new metric definitions API is 2016-03-01 and hello version for metrics API is 2016-09-01.</span></span> <span data-ttu-id="1489e-165">使用 hello 2014-04-01 版應用程式開發介面，可以存取 hello 舊版度量定義和度量。</span><span class="sxs-lookup"><span data-stu-id="1489e-165">hello legacy metric definitions and metrics can be accessed with hello API version 2014-04-01.</span></span>
>
>

<span data-ttu-id="1489e-166">如需使用 hello Azure 監視 REST Api 的詳細逐步解說，請參閱[Azure 監視 REST API 逐步解說](monitoring-rest-api-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="1489e-166">For a more detailed walkthrough using hello Azure Monitor REST APIs, see [Azure Monitor REST API walkthrough](monitoring-rest-api-walkthrough.md).</span></span>

## <a name="export-metrics"></a><span data-ttu-id="1489e-167">匯出度量</span><span class="sxs-lookup"><span data-stu-id="1489e-167">Export metrics</span></span>
<span data-ttu-id="1489e-168">您可以移 toohello**診斷設定**刀鋒視窗底下 hello**監視器**度量的索引標籤和檢視表 hello 匯出選項。</span><span class="sxs-lookup"><span data-stu-id="1489e-168">You can go toohello **Diagnostics settings** blade under hello **Monitor** tab and view hello export options for metrics.</span></span> <span data-ttu-id="1489e-169">您可以選取度量 （和診斷記錄檔） toobe 路由 tooBlob 儲存體、 tooAzure 事件中心或使用案例所提到的 tooOMS 先前在本文中。</span><span class="sxs-lookup"><span data-stu-id="1489e-169">You can select metrics (and diagnostic logs) toobe routed tooBlob storage, tooAzure Event Hubs, or tooOMS for use-cases that were mentioned previously in this article.</span></span>

 ![在 Azure 監視器中匯出度量選項](./media/monitoring-overview-metrics/MetricsOverview3.png)

<span data-ttu-id="1489e-171">您可以透過 Resource Manager 範本、[PowerShell](insights-powershell-samples.md)、[Azure CLI](insights-cli-samples.md) 或 [REST API](https://msdn.microsoft.com/library/dn931943.aspx) 來進行設定。</span><span class="sxs-lookup"><span data-stu-id="1489e-171">You can configure this via Resource Manager templates, [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), or [REST APIs](https://msdn.microsoft.com/library/dn931943.aspx).</span></span>

## <a name="take-action-on-metrics"></a><span data-ttu-id="1489e-172">對度量採取動作</span><span class="sxs-lookup"><span data-stu-id="1489e-172">Take action on metrics</span></span>
<span data-ttu-id="1489e-173">tooreceive 通知或採取自動動作的度量資料，您可以設定警示的規則或自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="1489e-173">tooreceive notifications or take automated actions on metric data, you can configure alert rules or Autoscale settings.</span></span>

### <a name="configure-alert-rules"></a><span data-ttu-id="1489e-174">設定警示規則</span><span class="sxs-lookup"><span data-stu-id="1489e-174">Configure alert rules</span></span>
<span data-ttu-id="1489e-175">您可以設定度量的警示規則。</span><span class="sxs-lookup"><span data-stu-id="1489e-175">You can configure alert rules on metrics.</span></span> <span data-ttu-id="1489e-176">這些警示規則可以檢查度量是否已超過某個臨界值，</span><span class="sxs-lookup"><span data-stu-id="1489e-176">These alert rules can check if a metric has crossed a certain threshold.</span></span> <span data-ttu-id="1489e-177">然後可以透過電子郵件通知您或任何自訂指令碼會引發可以是使用的 toorun webhook。</span><span class="sxs-lookup"><span data-stu-id="1489e-177">They can then notify you via email or fire a webhook that can be used toorun any custom script.</span></span> <span data-ttu-id="1489e-178">您也可以使用 hello webhook tooconfigure 第三方產品整合。</span><span class="sxs-lookup"><span data-stu-id="1489e-178">You can also use hello webhook tooconfigure third-party product integrations.</span></span>

 ![Azure 監視器中的度量和警示規則](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a><span data-ttu-id="1489e-180">自動調整您的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="1489e-180">Autoscale your Azure resources</span></span>
<span data-ttu-id="1489e-181">某些 Azure 資源支援 hello 的縮放比例出或多個執行個體 toohandle 您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="1489e-181">Some Azure resources support hello scaling out or in of multiple instances toohandle your workloads.</span></span> <span data-ttu-id="1489e-182">TooApp 服務 (Web 應用程式)、 虛擬機器擴展集和傳統的 Azure 雲端服務，適用於自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="1489e-182">Autoscale applies tooApp Service (Web Apps), virtual machine scale sets, and classic Azure Cloud Services.</span></span> <span data-ttu-id="1489e-183">當某些度量資訊會影響您的工作負載超出您所指定的臨界值時，您可以設定自動調整規模規則 tooscale 或放大。</span><span class="sxs-lookup"><span data-stu-id="1489e-183">You can configure Autoscale rules tooscale out or in when a certain metric that impacts your workload crosses a threshold that you specify.</span></span> <span data-ttu-id="1489e-184">如需詳細資訊，請參閱 [自動調整的概觀](monitoring-overview-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="1489e-184">For more information, see [Overview of autoscaling](monitoring-overview-autoscale.md).</span></span>

 ![Azure 監視器中的度量和自動調整](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a><span data-ttu-id="1489e-186">了解支援的服務和度量</span><span class="sxs-lookup"><span data-stu-id="1489e-186">Learn about supported services and metrics</span></span>
<span data-ttu-id="1489e-187">Azure 監視器是新的度量基礎結構。</span><span class="sxs-lookup"><span data-stu-id="1489e-187">Azure Monitor is a new metrics infrastructure.</span></span> <span data-ttu-id="1489e-188">它支援下列 hello Azure 入口網站與 hello 新版 hello Azure 監視應用程式開發介面中的 Azure 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="1489e-188">It supports hello following Azure services in hello Azure portal and hello new version of hello Azure Monitor API:</span></span>

* <span data-ttu-id="1489e-189">VM (Azure Resource Manager 架構)</span><span class="sxs-lookup"><span data-stu-id="1489e-189">VMs (Azure Resource Manager-based)</span></span>
* <span data-ttu-id="1489e-190">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="1489e-190">Virtual machine scale sets</span></span>
* <span data-ttu-id="1489e-191">Batch</span><span class="sxs-lookup"><span data-stu-id="1489e-191">Batch</span></span>
* <span data-ttu-id="1489e-192">事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="1489e-192">Event Hubs namespace</span></span>
* <span data-ttu-id="1489e-193">服務匯流排命名空間 (僅限進階 SKU)</span><span class="sxs-lookup"><span data-stu-id="1489e-193">Service Bus namespace (premium SKU only)</span></span>
* <span data-ttu-id="1489e-194">SQL Database (第 12 版)</span><span class="sxs-lookup"><span data-stu-id="1489e-194">SQL Database (version 12)</span></span>
* <span data-ttu-id="1489e-195">SQL 彈性集區</span><span class="sxs-lookup"><span data-stu-id="1489e-195">Elastic SQL Pool</span></span>
* <span data-ttu-id="1489e-196">網站</span><span class="sxs-lookup"><span data-stu-id="1489e-196">Websites</span></span>
* <span data-ttu-id="1489e-197">Web 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="1489e-197">Web server farms</span></span>
* <span data-ttu-id="1489e-198">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1489e-198">Logic Apps</span></span>
* <span data-ttu-id="1489e-199">IoT 中樞</span><span class="sxs-lookup"><span data-stu-id="1489e-199">IoT hubs</span></span>
* <span data-ttu-id="1489e-200">Redis 快取</span><span class="sxs-lookup"><span data-stu-id="1489e-200">Redis Cache</span></span>
* <span data-ttu-id="1489e-201">網路：應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1489e-201">Networking: Application gateways</span></span>
* <span data-ttu-id="1489e-202">搜尋</span><span class="sxs-lookup"><span data-stu-id="1489e-202">Search</span></span>

<span data-ttu-id="1489e-203">您可以檢視所有 hello 支援服務並在其度量的詳細的清單[Azure 監視度量-每個資源類型的支援度量](monitoring-supported-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="1489e-203">You can view a detailed list of all hello supported services and their metrics at [Azure Monitor metrics--supported metrics per resource type](monitoring-supported-metrics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1489e-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1489e-204">Next steps</span></span>
<span data-ttu-id="1489e-205">請參閱 toohello 整篇文章的連結。</span><span class="sxs-lookup"><span data-stu-id="1489e-205">Refer toohello links throughout this article.</span></span> <span data-ttu-id="1489e-206">此外，請了解：</span><span class="sxs-lookup"><span data-stu-id="1489e-206">Additionally, learn about:</span></span>  

* [<span data-ttu-id="1489e-207">自動調整規模的常用計量</span><span class="sxs-lookup"><span data-stu-id="1489e-207">Common metrics for autoscaling</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="1489e-208">如何 toocreate 警示規則</span><span class="sxs-lookup"><span data-stu-id="1489e-208">How toocreate alert rules</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="1489e-209">使用 Log Analytics 分析來自 Azure 儲存體的記錄</span><span class="sxs-lookup"><span data-stu-id="1489e-209">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
