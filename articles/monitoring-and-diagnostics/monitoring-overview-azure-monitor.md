---
title: "aaaAzure 監視器概觀 |Microsoft 文件"
description: "Azure 監視器會收集用於警示、webhook、自動調整，以及自動化的統計資料。 文章也會列出其他 Microsoft 監視選項。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a><span data-ttu-id="4f856-104">Azure 監視器的概觀</span><span class="sxs-lookup"><span data-stu-id="4f856-104">Overview of Azure Monitor</span></span>
<span data-ttu-id="4f856-105">本文章提供 hello Azure 監視 Microsoft Azure 服務的概觀。</span><span class="sxs-lookup"><span data-stu-id="4f856-105">This article provides an overview of hello Azure Monitor service in Microsoft Azure.</span></span> <span data-ttu-id="4f856-106">其中也會討論 Azure 監視器沒有以及提供如何指標 tooadditional 相關資訊 toouse Azure 監視器。</span><span class="sxs-lookup"><span data-stu-id="4f856-106">It discusses what Azure Monitor does and provides pointers tooadditional information on how toouse Azure Monitor.</span></span>  <span data-ttu-id="4f856-107">如果您偏好的影片介紹，請參閱這篇文章 hello 底部的下一個步驟連結。</span><span class="sxs-lookup"><span data-stu-id="4f856-107">If you prefer a video introduction, see Next steps links at hello bottom of this article.</span></span> 

## <a name="why-monitor-your-application-or-system"></a><span data-ttu-id="4f856-108">為什麼要監視您的應用程式或系統</span><span class="sxs-lookup"><span data-stu-id="4f856-108">Why monitor your application or system</span></span>
<span data-ttu-id="4f856-109">雲端應用程式相當複雜，且具有許多移動組件。</span><span class="sxs-lookup"><span data-stu-id="4f856-109">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="4f856-110">監視提供您的應用程式保持啟動的資料 tooensure 和狀況良好的狀態中執行。</span><span class="sxs-lookup"><span data-stu-id="4f856-110">Monitoring provides data tooensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="4f856-111">它也可協助您 toostave 關閉潛在的問題或過去的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="4f856-111">It also helps you toostave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="4f856-112">此外，您可以使用監視資料 toogain 深入了解有關應用程式。</span><span class="sxs-lookup"><span data-stu-id="4f856-112">In addition, you can use monitoring data toogain deep insights about your application.</span></span> <span data-ttu-id="4f856-113">該知識可以幫助您 tooimprove 應用程式效能或可維護性，或自動化需要手動介入的動作。</span><span class="sxs-lookup"><span data-stu-id="4f856-113">That knowledge can help you tooimprove application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a><span data-ttu-id="4f856-114">Azure 監視器及 Microsoft 的其他監視產品</span><span class="sxs-lookup"><span data-stu-id="4f856-114">Azure Monitor and Microsoft's other monitoring products</span></span>
<span data-ttu-id="4f856-115">Azure 監視器可針對 Microsoft Azure 中的大多數服務提供基本等級的基礎結構計量與記錄。</span><span class="sxs-lookup"><span data-stu-id="4f856-115">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="4f856-116">請勿尚未將其資料放到 Azure 監視的 azure 服務會將它放那里 hello 在未來。</span><span class="sxs-lookup"><span data-stu-id="4f856-116">Azure services that do not yet put their data into Azure Monitor will put it there in hello future.</span></span>

<span data-ttu-id="4f856-117">Microsoft 隨附額外的產品和服務，可針對同時擁有內部部署安裝的開發人員、DevOps 及 IT Ops 提供其他監視功能。</span><span class="sxs-lookup"><span data-stu-id="4f856-117">Microsoft ships additional products and services that provide additional monitoring capabilities for developers, DevOps, or IT Ops that also have on-premises installations.</span></span> <span data-ttu-id="4f856-118">如需概觀及了解這些不同產品和服務如何一起運作的相關資訊，請參閱 [Microsoft Azure 中的監視](monitoring-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4f856-118">For an overview and understanding of how these different products and services work together, see [Monitoring in Microsoft Azure](monitoring-overview.md).</span></span>

## <a name="monitoring-sources---compute"></a><span data-ttu-id="4f856-119">監視來源：計算</span><span class="sxs-lookup"><span data-stu-id="4f856-119">Monitoring Sources - Compute</span></span>

![非計算資源的監視與診斷模型](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

<span data-ttu-id="4f856-121">包含 hello 計算服務</span><span class="sxs-lookup"><span data-stu-id="4f856-121">hello Compute services include</span></span> 
- <span data-ttu-id="4f856-122">雲端服務</span><span class="sxs-lookup"><span data-stu-id="4f856-122">Cloud Services</span></span> 
- <span data-ttu-id="4f856-123">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4f856-123">Virtual Machines</span></span> 
- <span data-ttu-id="4f856-124">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="4f856-124">Virtual Machine scale sets</span></span> 
- <span data-ttu-id="4f856-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4f856-125">Service Fabric</span></span>

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a><span data-ttu-id="4f856-126">應用程式 - 診斷記錄檔、應用程式記錄檔及計量</span><span class="sxs-lookup"><span data-stu-id="4f856-126">Application - Diagnostics Logs, Application Logs, and Metrics</span></span>
<span data-ttu-id="4f856-127">應用程式可以 hello 計算模型中的 hello 客體作業系統上執行。</span><span class="sxs-lookup"><span data-stu-id="4f856-127">Applications can run on top of hello Guest OS in hello compute model.</span></span> <span data-ttu-id="4f856-128">它們會發出自己的記錄檔和計量集合。</span><span class="sxs-lookup"><span data-stu-id="4f856-128">They emit their own set of logs and metrics.</span></span> <span data-ttu-id="4f856-129">Azure 監視依賴 hello Azure 診斷擴充功能 （Windows 或 Linux） toocollect 大部分的應用程式層級度量和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4f856-129">Azure Monitor relies on hello Azure diagnostics extension (Windows or Linux) toocollect most application level metrics and logs.</span></span> <span data-ttu-id="4f856-130">hello 類型包括</span><span class="sxs-lookup"><span data-stu-id="4f856-130">hello types include</span></span>

* <span data-ttu-id="4f856-131">效能計數器</span><span class="sxs-lookup"><span data-stu-id="4f856-131">Performance counters</span></span>
* <span data-ttu-id="4f856-132">應用程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="4f856-132">Application Logs</span></span>
* <span data-ttu-id="4f856-133">Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="4f856-133">Windows Event Logs</span></span>
* <span data-ttu-id="4f856-134">.NET 事件來源</span><span class="sxs-lookup"><span data-stu-id="4f856-134">.NET Event Source</span></span>
* <span data-ttu-id="4f856-135">IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="4f856-135">IIS Logs</span></span>
* <span data-ttu-id="4f856-136">以資訊清單為基礎的 ETW</span><span class="sxs-lookup"><span data-stu-id="4f856-136">Manifest based ETW</span></span>
* <span data-ttu-id="4f856-137">損毀傾印</span><span class="sxs-lookup"><span data-stu-id="4f856-137">Crash Dumps</span></span>
* <span data-ttu-id="4f856-138">客戶錯誤記錄檔</span><span class="sxs-lookup"><span data-stu-id="4f856-138">Customer Error Logs</span></span>

<span data-ttu-id="4f856-139">沒有 hello 診斷擴充功能，只有幾個計量，例如 CPU 使用量可用。</span><span class="sxs-lookup"><span data-stu-id="4f856-139">Without hello diagnostics extension, only a few metrics like CPU usage are available.</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="4f856-140">主機和客體 VM 計量</span><span class="sxs-lookup"><span data-stu-id="4f856-140">Host and Guest VM metrics</span></span>
<span data-ttu-id="4f856-141">hello 先前所列的計算資源都有專用的主機 VM 和客體作業系統與它們互動。</span><span class="sxs-lookup"><span data-stu-id="4f856-141">hello previously listed compute resources have a dedicated host VM and guest OS they interact with.</span></span> <span data-ttu-id="4f856-142">hello 主機 VM 和客體作業系統是根 VM 的 hello 對等項目和 hello HYPER-V hypervisor 模型中的客體 VM。</span><span class="sxs-lookup"><span data-stu-id="4f856-142">hello host VM and guest OS are hello equivalent of root VM and guest VM in hello Hyper-V hypervisor model.</span></span> <span data-ttu-id="4f856-143">您可以同時收集這兩者的計量。</span><span class="sxs-lookup"><span data-stu-id="4f856-143">You can collect metrics on both.</span></span> <span data-ttu-id="4f856-144">您也可以在 hello 客體作業系統上收集診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4f856-144">You can also collect diagnostics logs on hello guest OS.</span></span>   

### <a name="activity-log"></a><span data-ttu-id="4f856-145">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="4f856-145">Activity Log</span></span>
<span data-ttu-id="4f856-146">您可以在 hello Azure 基礎結構所偵測到您資源的相關資訊的搜尋 hello （先前稱為操作或稽核記錄檔） 的活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4f856-146">You can search hello Activity Log (previously called Operational or Audit Logs) for information about your resource as seen by hello Azure infrastructure.</span></span> <span data-ttu-id="4f856-147">hello 記錄包含資源時所建立或終結的時間等資訊。</span><span class="sxs-lookup"><span data-stu-id="4f856-147">hello log contains information such as times when resources are created or destroyed.</span></span>  <span data-ttu-id="4f856-148">如需詳細資訊，請參閱[活動記錄概觀](monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="4f856-148">For more information, see [Overview of Activity Log](monitoring-overview-activity-logs.md).</span></span> 

## <a name="monitoring-sources---everything-else"></a><span data-ttu-id="4f856-149">監視來源：其他項目</span><span class="sxs-lookup"><span data-stu-id="4f856-149">Monitoring Sources - everything else</span></span>

![計算資源的監視與診斷模型](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a><span data-ttu-id="4f856-151">資源 - 計量和診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="4f856-151">Resource - Metrics and Diagnostics Logs</span></span>
<span data-ttu-id="4f856-152">可收集度量和診斷的記錄檔會根據 hello 資源類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4f856-152">Collectable metrics and diagnostics logs vary based on hello resource type.</span></span> <span data-ttu-id="4f856-153">比方說，Web 應用程式會提供對 hello 磁碟 IO 和百分比的 CPU 統計資料。</span><span class="sxs-lookup"><span data-stu-id="4f856-153">For example, Web Apps provides statistics on hello Disk IO and Percent CPU.</span></span> <span data-ttu-id="4f856-154">服務匯流排佇列沒有那些計量，而是改為提供佇列大小和訊息輸送量等計量。</span><span class="sxs-lookup"><span data-stu-id="4f856-154">Those metrics don't exist for a Service Bus queue, which instead provides metrics like queue size and message throughput.</span></span> <span data-ttu-id="4f856-155">[支援的計量](monitoring-supported-metrics.md)中提供可針對每個資源收集的計量清單。</span><span class="sxs-lookup"><span data-stu-id="4f856-155">A list of collectable metrics for each resource is available at [supported metrics](monitoring-supported-metrics.md).</span></span> 

### <a name="host-and-guest-vm-metrics"></a><span data-ttu-id="4f856-156">主機和客體 VM 計量</span><span class="sxs-lookup"><span data-stu-id="4f856-156">Host and Guest VM metrics</span></span>
<span data-ttu-id="4f856-157">您的資源和特定主機或客體 VM 之間不一定具有 1:1 的對應，因此沒有計量可供使用。</span><span class="sxs-lookup"><span data-stu-id="4f856-157">There is not necessarily a 1:1 mapping between your resource and a particular Host or Guest VM so metrics are not available.</span></span>

### <a name="activity-log"></a><span data-ttu-id="4f856-158">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="4f856-158">Activity Log</span></span>
<span data-ttu-id="4f856-159">hello 活動記錄檔是 hello 與計算資源相同。</span><span class="sxs-lookup"><span data-stu-id="4f856-159">hello activity log is hello same as for compute resources.</span></span>  

## <a name="uses-for-monitoring-data"></a><span data-ttu-id="4f856-160">監視資料的用途</span><span class="sxs-lookup"><span data-stu-id="4f856-160">Uses for Monitoring Data</span></span>
<span data-ttu-id="4f856-161">一旦您收集資料，您可以執行 hello 與其依照 Azure 監視器</span><span class="sxs-lookup"><span data-stu-id="4f856-161">Once you collect your data, you can do hello following with it in Azure Monitor</span></span>

### <a name="route"></a><span data-ttu-id="4f856-162">路由</span><span class="sxs-lookup"><span data-stu-id="4f856-162">Route</span></span>
<span data-ttu-id="4f856-163">您可以串流即時監視資料 tooother 位置。</span><span class="sxs-lookup"><span data-stu-id="4f856-163">You can stream monitoring data tooother locations in real time.</span></span>

<span data-ttu-id="4f856-164">範例包括：</span><span class="sxs-lookup"><span data-stu-id="4f856-164">Examples include:</span></span>

- <span data-ttu-id="4f856-165">傳送 tooApplication Insights，因此您可以使用其更豐富的視覺效果與分析工具。</span><span class="sxs-lookup"><span data-stu-id="4f856-165">Send tooApplication Insights so you can use its richer visualization and analysis tools.</span></span>
- <span data-ttu-id="4f856-166">傳送 tooEvent 中心，因此您可以在路由 toothird 廠商工具。</span><span class="sxs-lookup"><span data-stu-id="4f856-166">Send tooEvent Hubs so you can route toothird-party tools.</span></span> 

### <a name="store-and-archive"></a><span data-ttu-id="4f856-167">儲存與封存</span><span class="sxs-lookup"><span data-stu-id="4f856-167">Store and Archive</span></span>
<span data-ttu-id="4f856-168">某些監視資料已經在 Azure 監視器中儲存一段時間且可供使用。</span><span class="sxs-lookup"><span data-stu-id="4f856-168">Some monitoring data is already stored and available in Azure Monitor for a set amount of time.</span></span> 
- <span data-ttu-id="4f856-169">計量會儲存 30 天。</span><span class="sxs-lookup"><span data-stu-id="4f856-169">Metrics are stored for 30 days.</span></span> 
- <span data-ttu-id="4f856-170">活動記錄項目會儲存 90 天。</span><span class="sxs-lookup"><span data-stu-id="4f856-170">Activity log entries are stored for 90 days.</span></span> 
- <span data-ttu-id="4f856-171">診斷記錄完全不會儲存。</span><span class="sxs-lookup"><span data-stu-id="4f856-171">Diagnostics logs are not stored at all.</span></span> 

<span data-ttu-id="4f856-172">如果您想要 toostore 資料超過 hello 上面所列的時間週期，您可以使用 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4f856-172">If you want toostore data longer than hello time periods listed above, you can use an Azure storage.</span></span> <span data-ttu-id="4f856-173">監視資料會根據您設定的保留原則，保留於您的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="4f856-173">Monitoring data is kept in your storage acccount based on a retention policy you set.</span></span> <span data-ttu-id="4f856-174">您需要資料所佔用的 Azure 儲存體中的 hello 空間 hello 的 toopay。</span><span class="sxs-lookup"><span data-stu-id="4f856-174">You do have toopay for hello space hello data takes up in Azure storage.</span></span> 

<span data-ttu-id="4f856-175">幾個方式 toouse 這項資料：</span><span class="sxs-lookup"><span data-stu-id="4f856-175">A few ways toouse this data:</span></span>

- <span data-ttu-id="4f856-176">資料寫入後，您可以讓其他位於 Azure 之內或之外的工具讀取該資料並加以處理。</span><span class="sxs-lookup"><span data-stu-id="4f856-176">Once written, you can have other tools within or outside of Azure read it and process it.</span></span>
- <span data-ttu-id="4f856-177">您下載 hello 資料在本機上的本機封存，或變更您保留原則 hello 雲端 tookeep 資料中的很長的時間。</span><span class="sxs-lookup"><span data-stu-id="4f856-177">You download hello data locally for a local archive or change your retention policy in hello cloud tookeep data for extended periods of time.</span></span>  
- <span data-ttu-id="4f856-178">將 hello 資料保留在 Azure 儲存體無限期地進行封存。</span><span class="sxs-lookup"><span data-stu-id="4f856-178">You leave hello data in Azure storage indefinitely for archive purposes.</span></span> 

### <a name="query"></a><span data-ttu-id="4f856-179">查詢</span><span class="sxs-lookup"><span data-stu-id="4f856-179">Query</span></span>
<span data-ttu-id="4f856-180">您可以使用 hello Azure 監視 REST API，跨平台命令列介面 (CLI) 命令，PowerShell cmdlet 或 hello.NET SDK tooaccess hello hello 系統或 Azure 儲存體中的資料</span><span class="sxs-lookup"><span data-stu-id="4f856-180">You can use hello Azure Monitor REST API, cross platform Command-Line Interface (CLI) commands, PowerShell cmdlets, or hello .NET SDK tooaccess hello data in hello system or Azure storage</span></span>

<span data-ttu-id="4f856-181">範例包括：</span><span class="sxs-lookup"><span data-stu-id="4f856-181">Examples include:</span></span>

* <span data-ttu-id="4f856-182">針對您所撰寫的自訂監視應用程式取得資料</span><span class="sxs-lookup"><span data-stu-id="4f856-182">Getting data for a custom monitoring application you have written</span></span>
* <span data-ttu-id="4f856-183">建立自訂查詢，並傳送該資料 tooa 第三方應用程式。</span><span class="sxs-lookup"><span data-stu-id="4f856-183">Creating custom queries and sending that data tooa third-party application.</span></span>

### <a name="visualize"></a><span data-ttu-id="4f856-184">視覺化</span><span class="sxs-lookup"><span data-stu-id="4f856-184">Visualize</span></span>
<span data-ttu-id="4f856-185">視覺化您的監視資料圖形和圖表，可協助您找到趨勢比 hello 資料本身，尋找更快。</span><span class="sxs-lookup"><span data-stu-id="4f856-185">Visualizing your monitoring data in graphics and charts helps you find trends quicker than looking through hello data itself.</span></span>  

<span data-ttu-id="4f856-186">幾個視覺化方法包括︰</span><span class="sxs-lookup"><span data-stu-id="4f856-186">A few visualization methods include:</span></span>

* <span data-ttu-id="4f856-187">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4f856-187">Use hello Azure portal</span></span>
* <span data-ttu-id="4f856-188">路由資料 tooAzure Application Insights</span><span class="sxs-lookup"><span data-stu-id="4f856-188">Route data tooAzure Application Insights</span></span>
* <span data-ttu-id="4f856-189">路由資料 tooMicrosoft PowerBI</span><span class="sxs-lookup"><span data-stu-id="4f856-189">Route data tooMicrosoft PowerBI</span></span>
* <span data-ttu-id="4f856-190">路由 hello tooa 協力廠商視覺效果工具使用資料是即時資料流，或從 Azure 儲存體中封存讀取擁有 hello 工具</span><span class="sxs-lookup"><span data-stu-id="4f856-190">Route hello data tooa third-party visualization tool using either live streaming or by having hello tool read from an archive in Azure storage</span></span>


### <a name="automate"></a><span data-ttu-id="4f856-191">自動化</span><span class="sxs-lookup"><span data-stu-id="4f856-191">Automate</span></span>
<span data-ttu-id="4f856-192">您可以使用監視資料 tootrigger 警示，或甚至整個處理程序。</span><span class="sxs-lookup"><span data-stu-id="4f856-192">You can use monitoring data tootrigger alerts or even whole processes.</span></span> <span data-ttu-id="4f856-193">範例包括：</span><span class="sxs-lookup"><span data-stu-id="4f856-193">Examples include:</span></span>

* <span data-ttu-id="4f856-194">使用資料 tooautoscale 運算執行個體向上或向下根據應用程式負載。</span><span class="sxs-lookup"><span data-stu-id="4f856-194">Use data tooautoscale compute instances up or down based on application load.</span></span>
* <span data-ttu-id="4f856-195">在某個計量超過預先定義的臨界值時傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="4f856-195">Send emails when a metric crosses a predetermined threshold.</span></span>
* <span data-ttu-id="4f856-196">呼叫 web URL (webhook) tooexecute Azure 外部系統中的動作</span><span class="sxs-lookup"><span data-stu-id="4f856-196">Call a web URL (webhook) tooexecute an action in a system outside of Azure</span></span>
* <span data-ttu-id="4f856-197">在 Azure 自動化 tooperform 任何各種工作啟動 runbook</span><span class="sxs-lookup"><span data-stu-id="4f856-197">Start a runbook in Azure automation tooperform any variety of tasks</span></span>

## <a name="methods-of-accessing-azure-monitor"></a><span data-ttu-id="4f856-198">存取 Azure 監視器的方法</span><span class="sxs-lookup"><span data-stu-id="4f856-198">Methods of accessing Azure Monitor</span></span>
<span data-ttu-id="4f856-199">一般情況下，您可以操作資料追蹤功能、 路由及使用其中一種 hello 遵循方法擷取。</span><span class="sxs-lookup"><span data-stu-id="4f856-199">In general, you can manipulate data tracking, routing, and retrieval using one of hello following methods.</span></span> <span data-ttu-id="4f856-200">並非所有方法都適用所有動作或資料類型。</span><span class="sxs-lookup"><span data-stu-id="4f856-200">Not all methods are available for all actions or data types.</span></span>

* [<span data-ttu-id="4f856-201">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4f856-201">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="4f856-202">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f856-202">PowerShell</span></span>](insights-powershell-samples.md)  
* [<span data-ttu-id="4f856-203">跨平台命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="4f856-203">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md)
* [<span data-ttu-id="4f856-204">REST API</span><span class="sxs-lookup"><span data-stu-id="4f856-204">REST API</span></span>](https://docs.microsoft.com/rest/api/monitor/)
* [<span data-ttu-id="4f856-205">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="4f856-205">.NET SDK</span></span>](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a><span data-ttu-id="4f856-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f856-206">Next steps</span></span>
<span data-ttu-id="4f856-207">深入了解</span><span class="sxs-lookup"><span data-stu-id="4f856-207">Learn more about</span></span>
- <span data-ttu-id="4f856-208">僅 Azure 監視器的影片逐步解說位於</span><span class="sxs-lookup"><span data-stu-id="4f856-208">A video walkthrough of just Azure Monitor is available at</span></span>  
<span data-ttu-id="4f856-209">[開始使用 Azure 監視器](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor)。</span><span class="sxs-lookup"><span data-stu-id="4f856-209">[Get Started with Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor).</span></span> <span data-ttu-id="4f856-210">在[探索 Microsoft Azure 監視和診斷 (英文)](https://channel9.msdn.com/events/Ignite/2016/BRK2234) 和[來自 Ignite 2016 的 Azure 監視器影片 (英文)](https://myignite.microsoft.com/videos/4977) 可取得額外影片，該影片說明您可以使用 Azure 監視器的案例</span><span class="sxs-lookup"><span data-stu-id="4f856-210">An additional video explaining a scenario where you can use Azure Monitor is available at [Explore Microsoft Azure monitoring and diagnostics](https://channel9.msdn.com/events/Ignite/2016/BRK2234) and [Azure Monitor in a video from Ignite 2016](https://myignite.microsoft.com/videos/4977)</span></span>
- <span data-ttu-id="4f856-211">透過 hello Azure 監視器 介面中執行[開始使用 Azure 監視器](monitoring-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="4f856-211">Run through hello Azure Monitor interface in [Getting Started with Azure Monitor](monitoring-get-started.md)</span></span>
- <span data-ttu-id="4f856-212">設定 hello [Azure 診斷延伸模組](../azure-diagnostics.md)集或 Service Fabric 應用程式，如果您正嘗試 toodiagnose 問題，您的雲端服務，虛擬機器中擴充虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4f856-212">Set up hello [Azure Diagnostics Extensions](../azure-diagnostics.md) if you are attempting toodiagnose problems in your Cloud Service, Virtual Machine, Virtual machine scale sets, or Service Fabric application.</span></span>
- <span data-ttu-id="4f856-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/)如果您在應用程式服務 Web 應用程式中嘗試 toodiagnostic 問題。</span><span class="sxs-lookup"><span data-stu-id="4f856-213">[Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) if you are trying toodiagnostic problems in your App Service Web app.</span></span>
- <span data-ttu-id="4f856-214">[疑難排解 Azure 儲存體](../storage/common/storage-e2e-troubleshooting.md) </span><span class="sxs-lookup"><span data-stu-id="4f856-214">[Troubleshooting Azure Storage](../storage/common/storage-e2e-troubleshooting.md) when using Storage Blobs, Tables, or Queues</span></span>
- <span data-ttu-id="4f856-215">[記錄分析](https://azure.microsoft.com/documentation/services/log-analytics/)和 hello [Operations Management Suite](https://www.microsoft.com/oms/)</span><span class="sxs-lookup"><span data-stu-id="4f856-215">[Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) and hello [Operations Management Suite](https://www.microsoft.com/oms/)</span></span>
