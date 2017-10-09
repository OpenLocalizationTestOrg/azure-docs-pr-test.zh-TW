---
title: "在 Microsoft Azure 虛擬機器、 雲端服務和 Web 應用程式的自動調整規模的 aaaOverview |Microsoft 文件"
description: "Microsoft Azure 的自動調整概觀。 適用於 tooVirtual 機器、 雲端服務和 Web 應用程式。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a><span data-ttu-id="edd98-104">Microsoft Azure 虛擬機器、雲端服務和 Web Apps 的自動調整概觀</span><span class="sxs-lookup"><span data-stu-id="edd98-104">Overview of autoscale in Microsoft Azure Virtual Machines, Cloud Services, and Web Apps</span></span>
<span data-ttu-id="edd98-105">本文說明哪些 Microsoft Azure 自動調整規模，其優點，以及 tooget 如何開始使用它。</span><span class="sxs-lookup"><span data-stu-id="edd98-105">This article describes what Microsoft Azure autoscale is, its benefits, and how tooget started using it.</span></span>  

<span data-ttu-id="edd98-106">Azure 監視的自動調整規模太只適用於[虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)，[雲端服務](https://azure.microsoft.com/services/cloud-services/)，和[應用程式服務-Web 應用程式](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="edd98-106">Azure Monitor autoscale applies only too[Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>

> [!NOTE]
> <span data-ttu-id="edd98-107">Azure 有兩種自動調整方法。</span><span class="sxs-lookup"><span data-stu-id="edd98-107">Azure has two autoscale methods.</span></span> <span data-ttu-id="edd98-108">較舊版本的自動調整規模適用於 tooVirtual 機器 （可用性設定組）。</span><span class="sxs-lookup"><span data-stu-id="edd98-108">An older version of autoscale applies tooVirtual Machines (availability sets).</span></span> <span data-ttu-id="edd98-109">這項功能具有有限的支援，我們建議您移轉 toovirtual 機器小數位數設定為更快速且更可靠的自動調整規模的支援。</span><span class="sxs-lookup"><span data-stu-id="edd98-109">This feature has limited support and we recommend migrating toovirtual machine scale sets for faster and more reliable autoscale support.</span></span> <span data-ttu-id="edd98-110">本文章中隨附上如何 toouse hello 舊技術的連結。</span><span class="sxs-lookup"><span data-stu-id="edd98-110">A link on how toouse hello older technology is included in this article.</span></span>  
>
>

## <a name="what-is-autoscale"></a><span data-ttu-id="edd98-111">何謂自動調整？</span><span class="sxs-lookup"><span data-stu-id="edd98-111">What is autoscale?</span></span>
<span data-ttu-id="edd98-112">自動調整規模可讓您 toohave hello 適量的資源在您的應用程式上執行 toohandle hello 負載。</span><span class="sxs-lookup"><span data-stu-id="edd98-112">Autoscale allows you toohave hello right amount of resources running toohandle hello load on your application.</span></span> <span data-ttu-id="edd98-113">它可讓您 tooadd 資源 toohandle 增加的負載，而且也藉由移除資源，會有某些閒置節省成本。</span><span class="sxs-lookup"><span data-stu-id="edd98-113">It allows you tooadd resources toohandle increases in load and also save money by removing resources that are sitting idle.</span></span> <span data-ttu-id="edd98-114">您指定的執行個體 toorun 最小和最大數目和新增或移除 Vm 會自動根據一組規則。</span><span class="sxs-lookup"><span data-stu-id="edd98-114">You specify a minimum and maximum number of instances toorun and add or remove VMs automatically based on a set of rules.</span></span> <span data-ttu-id="edd98-115">設定下限可確保即使沒有負載應用程式也會一直執行。</span><span class="sxs-lookup"><span data-stu-id="edd98-115">Having a minimum makes sure your application is always running even under no load.</span></span> <span data-ttu-id="edd98-116">設定上限則可限制每小時可能產生的總成本。</span><span class="sxs-lookup"><span data-stu-id="edd98-116">Having a maximum limits your total possible hourly cost.</span></span> <span data-ttu-id="edd98-117">您可以使用您所建立的規則自動在這兩個極端值之間進行調整。</span><span class="sxs-lookup"><span data-stu-id="edd98-117">You automatically scale between these two extremes using rules you create.</span></span>

 ![說明自動調整。](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

<span data-ttu-id="edd98-120">符合規則條件時，就會觸發一個或多個自動調整動作。</span><span class="sxs-lookup"><span data-stu-id="edd98-120">When rule conditions are met, one or more autoscale actions are triggered.</span></span> <span data-ttu-id="edd98-121">您可以新增和移除 VM，或執行其他動作。</span><span class="sxs-lookup"><span data-stu-id="edd98-121">You can add and remove VMs, or perform other actions.</span></span> <span data-ttu-id="edd98-122">hello 概念圖顯示此程序。</span><span class="sxs-lookup"><span data-stu-id="edd98-122">hello following conceptual diagram shows this process.</span></span>  

 ![自動調整流程圖](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

<span data-ttu-id="edd98-124">hello 以下說明適用於 toohello hello 上圖中的部分。</span><span class="sxs-lookup"><span data-stu-id="edd98-124">hello following explanation applies toohello pieces of hello previous diagram.</span></span>   

## <a name="resource-metrics"></a><span data-ttu-id="edd98-125">資源計量</span><span class="sxs-lookup"><span data-stu-id="edd98-125">Resource Metrics</span></span>
<span data-ttu-id="edd98-126">資源會發出計量，這些計量稍後會由規則處理。</span><span class="sxs-lookup"><span data-stu-id="edd98-126">Resources emit metrics, these metrics are later processed by rules.</span></span> <span data-ttu-id="edd98-127">度量來自不同的方法。</span><span class="sxs-lookup"><span data-stu-id="edd98-127">Metrics come via different methods.</span></span>
<span data-ttu-id="edd98-128">虛擬機器級別集合會使用遙測資料從 Azure 診斷代理程式，而 Web 應用程式和雲端服務的遙測直接來自 hello Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="edd98-128">Virtual machine scale sets use telemetry data from Azure diagnostics agents whereas telemetry for Web apps and Cloud services comes directly from hello Azure Infrastructure.</span></span> <span data-ttu-id="edd98-129">一些常用的統計資料包括 CPU 使用率、記憶體使用量、執行緒計數、佇列長度和磁碟使用量。</span><span class="sxs-lookup"><span data-stu-id="edd98-129">Some commonly used statistics include CPU Usage, memory usage, thread counts, queue length, and disk usage.</span></span> <span data-ttu-id="edd98-130">如需可使用哪些遙測資料的清單，請參閱 [自動調整的常用度量](insights-autoscale-common-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="edd98-130">For a list of what telemetry data you can use, see [Autoscale Common Metrics](insights-autoscale-common-metrics.md).</span></span>

## <a name="custom-metrics"></a><span data-ttu-id="edd98-131">自訂計量</span><span class="sxs-lookup"><span data-stu-id="edd98-131">Custom Metrics</span></span>
<span data-ttu-id="edd98-132">您也可以運用自己自訂的計量 (由您的應用程式發出)。</span><span class="sxs-lookup"><span data-stu-id="edd98-132">You can also leverage your own custom metrics that your application(s) may be emitting.</span></span> <span data-ttu-id="edd98-133">如果您已設定您的應用程式 toosend 度量 tooApplication Insights，您可以利用是否這些度量 toomake 決策 tooscale 與否。</span><span class="sxs-lookup"><span data-stu-id="edd98-133">If you have configured your application(s) toosend metrics tooApplication Insights you can leverage those metrics toomake decisions on whether tooscale or not.</span></span> 

## <a name="time"></a><span data-ttu-id="edd98-134">時間</span><span class="sxs-lookup"><span data-stu-id="edd98-134">Time</span></span>
<span data-ttu-id="edd98-135">排程型規則是以 UTC 為基礎。</span><span class="sxs-lookup"><span data-stu-id="edd98-135">Schedule-based rules are based on UTC.</span></span> <span data-ttu-id="edd98-136">設定規則時必須正確設定時區。</span><span class="sxs-lookup"><span data-stu-id="edd98-136">You must set your time zone properly when setting up your rules.</span></span>  

## <a name="rules"></a><span data-ttu-id="edd98-137">規則</span><span class="sxs-lookup"><span data-stu-id="edd98-137">Rules</span></span>
<span data-ttu-id="edd98-138">hello 圖表會顯示一個自動調整規模規則，但您可以有多個。</span><span class="sxs-lookup"><span data-stu-id="edd98-138">hello diagram shows only one autoscale rule, but you can have many of them.</span></span> <span data-ttu-id="edd98-139">您可以視情況需要建立複雜的重疊規則。</span><span class="sxs-lookup"><span data-stu-id="edd98-139">You can create complex overlapping rules as needed for your situation.</span></span>  <span data-ttu-id="edd98-140">規則類型包含</span><span class="sxs-lookup"><span data-stu-id="edd98-140">Rule types include</span></span>  

* <span data-ttu-id="edd98-141">**度量型** - 例如，當 CPU 使用率高於 50% 時執行此動作。</span><span class="sxs-lookup"><span data-stu-id="edd98-141">**Metric-based** - For example, do this action when CPU usage is above 50%.</span></span>
* <span data-ttu-id="edd98-142">**時間型** - 例如，在指定時區的每星期六上午 8 點觸發 Webhook。</span><span class="sxs-lookup"><span data-stu-id="edd98-142">**Time-based** - For example, trigger a webhook every 8am on Saturday in a given time zone.</span></span>

<span data-ttu-id="edd98-143">度量型規則會測量應用程式負載，並根據該負載新增或移除 VM。</span><span class="sxs-lookup"><span data-stu-id="edd98-143">Metric-based rules measure application load and add or remove VMs based on that load.</span></span> <span data-ttu-id="edd98-144">排程為基礎的規則可讓您 tooscale 當您在負載查看時間模式，並想 tooscale 之前可能的負載增加或減少，就會發生。</span><span class="sxs-lookup"><span data-stu-id="edd98-144">Schedule-based rules allow you tooscale when you see time patterns in your load and want tooscale before a possible load increase or decrease occurs.</span></span>  

## <a name="actions-and-automation"></a><span data-ttu-id="edd98-145">動作與自動化</span><span class="sxs-lookup"><span data-stu-id="edd98-145">Actions and automation</span></span>
<span data-ttu-id="edd98-146">規則可以觸發一個或多個類型的動作。</span><span class="sxs-lookup"><span data-stu-id="edd98-146">Rules can trigger one or more types of actions.</span></span>

* <span data-ttu-id="edd98-147">**調整** - 將 VM 相應放大或相應縮小</span><span class="sxs-lookup"><span data-stu-id="edd98-147">**Scale** - Scale VMs in or out</span></span>
* <span data-ttu-id="edd98-148">**電子郵件**-傳送電子郵件 toosubscription admins、 共同管理員及/或您所指定的其他電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="edd98-148">**Email** - Send email toosubscription admins, co-admins, and/or additional email address you specify</span></span>
* <span data-ttu-id="edd98-149">**透過 Webhook 自動執行** - 呼叫 Webhook，以觸發 Azure 內部或外部的多個複雜動作。</span><span class="sxs-lookup"><span data-stu-id="edd98-149">**Automate via webhooks** - Call webhooks, which can trigger multiple complex actions inside or outside Azure.</span></span> <span data-ttu-id="edd98-150">在 Azure 內部，您可以啟動 Azure 自動化 Runbook、Azure 函數或 Azure 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="edd98-150">Inside Azure, you can start an Azure Automation runbook, Azure Function, or Azure Logic App.</span></span> <span data-ttu-id="edd98-151">Azure 外部的範例第三方 URL 包含 Slack 和 Twilio 等服務。</span><span class="sxs-lookup"><span data-stu-id="edd98-151">Example third-party URL outside Azure include services like Slack and Twilio.</span></span>

## <a name="autoscale-settings"></a><span data-ttu-id="edd98-152">自動調整設定</span><span class="sxs-lookup"><span data-stu-id="edd98-152">Autoscale Settings</span></span>
<span data-ttu-id="edd98-153">自動調整規模 hello 後使用的術語和結構。</span><span class="sxs-lookup"><span data-stu-id="edd98-153">Autoscale use hello following terminology and structure.</span></span>

- <span data-ttu-id="edd98-154">**自動調整規模設定**是否已讀取 hello 自動調整引擎 toodetermine tooscale 向上或向下。</span><span class="sxs-lookup"><span data-stu-id="edd98-154">An **autoscale setting** is read by hello autoscale engine toodetermine whether tooscale up or down.</span></span> <span data-ttu-id="edd98-155">它包含一個或多個設定檔，hello 目標資源，並通知設定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="edd98-155">It contains one or more profiles, information about hello target resource, and notification settings.</span></span>

    - <span data-ttu-id="edd98-156">**自動調整設定檔**結合了下列項目：</span><span class="sxs-lookup"><span data-stu-id="edd98-156">An **autoscale profile** is a combination of a:</span></span>

        - <span data-ttu-id="edd98-157">**容量設定**、 hello 最小值，最大值，表示和執行個體數目的預設值。</span><span class="sxs-lookup"><span data-stu-id="edd98-157">**capacity setting**, which indicates hello minimum, maximum, and default values for number of instances.</span></span>
        - <span data-ttu-id="edd98-158">**一組規則**，其中的每個規則包含觸發程序 (時間或度量) 和調整動作 (相應增加或相應減少)。</span><span class="sxs-lookup"><span data-stu-id="edd98-158">**set of rules**, each of which includes a trigger (time or metric) and a scale action (up or down).</span></span>
        - <span data-ttu-id="edd98-159">**循環**，會指出自動調整應該在何時讓此設定檔生效。</span><span class="sxs-lookup"><span data-stu-id="edd98-159">**recurrence**, which indicates when autoscale should put this profile into effect.</span></span>

        <span data-ttu-id="edd98-160">您可以有多個設定檔，可讓您 tootake care of 不同重疊的需求。</span><span class="sxs-lookup"><span data-stu-id="edd98-160">You can have multiple profiles, which allow you tootake care of different overlapping requirements.</span></span> <span data-ttu-id="edd98-161">您可以不同時間的日次或星期幾 hello，例如有不同的自動調整規模設定檔。</span><span class="sxs-lookup"><span data-stu-id="edd98-161">You can have different autoscale profiles for different times of day or days of hello week, for example.</span></span>

    - <span data-ttu-id="edd98-162">A**通知設定**定義自動調整規模事件發生根據滿足條件的其中一個 hello 自動調整規模設定的設定檔的 hello 準則時，應該就會發生何種通知。</span><span class="sxs-lookup"><span data-stu-id="edd98-162">A **notification setting** defines what notifications should occur when an autoscale event occurs based on satisfying hello criteria of one of hello autoscale setting’s profiles.</span></span> <span data-ttu-id="edd98-163">自動調整規模可通知一或多個電子郵件地址，或請呼叫 tooone 或多個 webhook。</span><span class="sxs-lookup"><span data-stu-id="edd98-163">Autoscale can notify one or more email addresses or make calls tooone or more webhooks.</span></span>


![Azure 自動調整設定、設定檔和規則結構](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

<span data-ttu-id="edd98-165">hello 可設定的欄位描述的完整清單位於 hello[自動調整規模 REST API](https://msdn.microsoft.com/library/dn931928.aspx)。</span><span class="sxs-lookup"><span data-stu-id="edd98-165">hello full list of configurable fields and descriptions is available in hello [Autoscale REST API](https://msdn.microsoft.com/library/dn931928.aspx).</span></span>

<span data-ttu-id="edd98-166">如需程式碼範例，請參閱</span><span class="sxs-lookup"><span data-stu-id="edd98-166">For code examples, see</span></span>

* [<span data-ttu-id="edd98-167">針對 VM 擴展集使用 Resource Manager 範本進行進階自動調整設定</span><span class="sxs-lookup"><span data-stu-id="edd98-167">Advanced Autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [<span data-ttu-id="edd98-168">自動調整 REST API</span><span class="sxs-lookup"><span data-stu-id="edd98-168">Autoscale REST API</span></span>](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a><span data-ttu-id="edd98-169">水平和垂直調整</span><span class="sxs-lookup"><span data-stu-id="edd98-169">Horizontal vs vertical scaling</span></span>
<span data-ttu-id="edd98-170">自動調整規模只縮放的水平 （「 出 」） 增加或減少 （「 位置 」） 中 VM 執行個體的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="edd98-170">Autoscale only scales horizontally, which is an increase ("out") or decrease ("in") in hello number of VM instances.</span></span>  <span data-ttu-id="edd98-171">水平是更有彈性在雲端的情況下它可讓您的 Vm toohandle 負載 toorun 潛在千分位。</span><span class="sxs-lookup"><span data-stu-id="edd98-171">Horizontal is more flexible in a cloud situation as it allows you toorun potentially thousands of VMs toohandle load.</span></span>

<span data-ttu-id="edd98-172">對比之下，垂直調整則不同。</span><span class="sxs-lookup"><span data-stu-id="edd98-172">In contrast, vertical scaling is different.</span></span> <span data-ttu-id="edd98-173">它會保持 hello 相同數目的 Vm，但讓 hello （「 向上 」） 更多或較少 （「 向下 」） 功能強大的 Vm。</span><span class="sxs-lookup"><span data-stu-id="edd98-173">It keeps hello same number of VMs, but makes hello VMs more ("up") or less ("down") powerful.</span></span> <span data-ttu-id="edd98-174">能力是以記憶體、CPU 速度、磁碟空間等項目來加以測量。垂直調整有更多限制。</span><span class="sxs-lookup"><span data-stu-id="edd98-174">Power is measured in memory, CPU speed, disk space, etc.  Vertical scaling has more limitations.</span></span> <span data-ttu-id="edd98-175">它會相依於較大的硬體，快速達到上限，且可能會因區域 hello 可用性。</span><span class="sxs-lookup"><span data-stu-id="edd98-175">It's dependent on hello availability of larger hardware, which quickly hits an upper limit and can vary by region.</span></span> <span data-ttu-id="edd98-176">垂直縮放比例通常也需要 VM toostop 並重新啟動。</span><span class="sxs-lookup"><span data-stu-id="edd98-176">Vertical scaling also usually requires a VM toostop and restart.</span></span>

<span data-ttu-id="edd98-177">如需詳細資訊，請參閱[使用 Azure 自動化垂直調整 Azure 虛擬機器](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="edd98-177">For more information, see [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="methods-of-access"></a><span data-ttu-id="edd98-178">存取方法</span><span class="sxs-lookup"><span data-stu-id="edd98-178">Methods of access</span></span>
<span data-ttu-id="edd98-179">您可以透過下列途徑設定自動調整</span><span class="sxs-lookup"><span data-stu-id="edd98-179">You can set up autoscale via</span></span>

* [<span data-ttu-id="edd98-180">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="edd98-180">Azure portal</span></span>](insights-how-to-scale.md)
* [<span data-ttu-id="edd98-181">PowerShell</span><span class="sxs-lookup"><span data-stu-id="edd98-181">PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [<span data-ttu-id="edd98-182">跨平台命令列介面 (CLI)</span><span class="sxs-lookup"><span data-stu-id="edd98-182">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md#autoscale)
* [<span data-ttu-id="edd98-183">Azure 監視器 REST API</span><span class="sxs-lookup"><span data-stu-id="edd98-183">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a><span data-ttu-id="edd98-184">支援的自動調整服務</span><span class="sxs-lookup"><span data-stu-id="edd98-184">Supported services for autoscale</span></span>
| <span data-ttu-id="edd98-185">服務</span><span class="sxs-lookup"><span data-stu-id="edd98-185">Service</span></span> | <span data-ttu-id="edd98-186">結構描述與文件</span><span class="sxs-lookup"><span data-stu-id="edd98-186">Schema & Docs</span></span> |
| --- | --- |
| <span data-ttu-id="edd98-187">Web Apps</span><span class="sxs-lookup"><span data-stu-id="edd98-187">Web Apps</span></span> |[<span data-ttu-id="edd98-188">調整 Web Apps</span><span class="sxs-lookup"><span data-stu-id="edd98-188">Scaling Web Apps</span></span>](insights-how-to-scale.md) |
| <span data-ttu-id="edd98-189">雲端服務</span><span class="sxs-lookup"><span data-stu-id="edd98-189">Cloud Services</span></span> |[<span data-ttu-id="edd98-190">自動調整雲端服務</span><span class="sxs-lookup"><span data-stu-id="edd98-190">Autoscale a Cloud Service</span></span>](../cloud-services/cloud-services-how-to-scale.md) |
| <span data-ttu-id="edd98-191">虛擬機器：傳統</span><span class="sxs-lookup"><span data-stu-id="edd98-191">Virtual Machines: Classic</span></span> |[<span data-ttu-id="edd98-192">調整傳統的虛擬機器可用性設定組</span><span class="sxs-lookup"><span data-stu-id="edd98-192">Scaling Classic Virtual Machine Availability Sets</span></span>](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| <span data-ttu-id="edd98-193">虛擬機器：Windows 擴展集</span><span class="sxs-lookup"><span data-stu-id="edd98-193">Virtual Machines: Windows Scale Sets</span></span> |[<span data-ttu-id="edd98-194">在 Windows 中調整虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="edd98-194">Scaling virtual machine scale sets in Windows</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| <span data-ttu-id="edd98-195">虛擬機器：Linux 擴展集</span><span class="sxs-lookup"><span data-stu-id="edd98-195">Virtual Machines: Linux Scale Sets</span></span> |[<span data-ttu-id="edd98-196">在 Linux 中調整虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="edd98-196">Scaling virtual machine scale sets in Linux</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| <span data-ttu-id="edd98-197">虛擬機器：Windows 範例</span><span class="sxs-lookup"><span data-stu-id="edd98-197">Virtual Machines: Windows Example</span></span> |[<span data-ttu-id="edd98-198">針對 VM 擴展集使用 Resource Manager 範本進行進階自動調整設定</span><span class="sxs-lookup"><span data-stu-id="edd98-198">Advanced Autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a><span data-ttu-id="edd98-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="edd98-199">Next steps</span></span>
<span data-ttu-id="edd98-200">深入了解自動調整規模，toolearn 使用自動調整規模逐步解說先前所列的 hello，或參閱 toohello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="edd98-200">toolearn more about autoscale, use hello Autoscale Walkthroughs listed previously or refer toohello following resources:</span></span>

* [<span data-ttu-id="edd98-201">Azure 監視器自動調整的常用度量</span><span class="sxs-lookup"><span data-stu-id="edd98-201">Azure Monitor autoscale common metrics</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="edd98-202">Azure 監視器自動調整的最佳作法</span><span class="sxs-lookup"><span data-stu-id="edd98-202">Best practices for Azure Monitor autoscale</span></span>](insights-autoscale-best-practices.md)
* [<span data-ttu-id="edd98-203">使用自動調整規模動作 toosend 電子郵件和 webhook 警示通知</span><span class="sxs-lookup"><span data-stu-id="edd98-203">Use autoscale actions toosend email and webhook alert notifications</span></span>](insights-autoscale-to-webhook-email.md)
* [<span data-ttu-id="edd98-204">自動調整 REST API</span><span class="sxs-lookup"><span data-stu-id="edd98-204">Autoscale REST API</span></span>](https://msdn.microsoft.com/library/dn931953.aspx)
* [<span data-ttu-id="edd98-205">排解虛擬機器擴展集自動調整的問題</span><span class="sxs-lookup"><span data-stu-id="edd98-205">Troubleshooting Virtual Machine Scale Sets Autoscale</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
