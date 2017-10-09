---
title: "事件的 Windows Azure 中的 Vm aaaScheduled |Microsoft 文件"
description: "您的 Windows 虛擬機器上使用 hello Azure 中繼資料服務，進行排程的事件。"
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="89c7e-103">Azure 中繼資料服務：Windows VM 的已排定事件 (預覽)</span><span class="sxs-lookup"><span data-stu-id="89c7e-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="89c7e-104">預覽是可用 tooyou 對貴用戶同意 toohello 使用條款 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="89c7e-105">如需詳細資訊，請參閱 [Microsoft Azure 預覽版增補使用條款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)。</span><span class="sxs-lookup"><span data-stu-id="89c7e-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="89c7e-106">排程的事件是在 hello Azure 中繼資料服務的 hello 子服務。</span><span class="sxs-lookup"><span data-stu-id="89c7e-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="89c7e-107">其會呈現即將發生的事件 (例如，重新開機) 相關資訊，以便應用程式做好準備並限制中斷造成的影響。</span><span class="sxs-lookup"><span data-stu-id="89c7e-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="89c7e-108">它適用於所有 Azure 虛擬機器類型 (包括 PaaS 和 IaaS)。</span><span class="sxs-lookup"><span data-stu-id="89c7e-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="89c7e-109">排程的事件可讓您虛擬機器階段 tooperform 預防工作 toominimize hello 效果的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="89c7e-110">排定的事件適用於 Linux 和 Window VM。</span><span class="sxs-lookup"><span data-stu-id="89c7e-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="89c7e-111">如需 Linux 上已排定事件的資訊，請參閱 [Linux VM 的已排定事件](../windows/scheduled-events.md)。</span><span class="sxs-lookup"><span data-stu-id="89c7e-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="89c7e-112">為什麼要使用排定的事件？</span><span class="sxs-lookup"><span data-stu-id="89c7e-112">Why Scheduled Events?</span></span>

<span data-ttu-id="89c7e-113">與排程的事件，您可以採取步驟的平台 intiated 維護或使用者啟動的動作 toolimit hello 影響您的服務。</span><span class="sxs-lookup"><span data-stu-id="89c7e-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="89c7e-114">多個執行個體的工作負載，可以使用複寫技術 toomaintain 狀態，可能容易遭受 toooutages 發生多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="89c7e-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="89c7e-115">例如中斷可能會導致耗費資源的工作 (例如，重建索引) 或甚至是複本遺失。</span><span class="sxs-lookup"><span data-stu-id="89c7e-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="89c7e-116">在其他許多情況下，hello 整體服務可用性，可以改善執行的非失誤性關機順序，例如完成 （或取消） 進行中的交易，重新指派工作 tooother Vm hello 叢集中 （手動容錯移轉），或移除 hello從網路負載平衡器集區的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="89c7e-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="89c7e-117">一些情況下，通知系統管理員有關即將發生的事件，或將記錄這類事件協助改善 hello hello 雲端中裝載的應用程式的服務性。</span><span class="sxs-lookup"><span data-stu-id="89c7e-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="89c7e-118">Azure 服務中繼資料介面排程的事件中 hello 下列使用案例：</span><span class="sxs-lookup"><span data-stu-id="89c7e-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="89c7e-119">平台起始的維護 (例如，主機作業系統推出)</span><span class="sxs-lookup"><span data-stu-id="89c7e-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="89c7e-120">使用者起始的呼叫 (例如，使用者重新啟動或重新部署 VM)</span><span class="sxs-lookup"><span data-stu-id="89c7e-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="89c7e-121">hello 基本概念</span><span class="sxs-lookup"><span data-stu-id="89c7e-121">hello basics</span></span>  

<span data-ttu-id="89c7e-122">Azure 的中繼資料服務會公開執行使用從 hello VM 中存取 REST 端點的虛擬機器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="89c7e-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="89c7e-123">hello 資訊可透過路由的內部 IP，讓它不會顯示 hello VM 之外。</span><span class="sxs-lookup"><span data-stu-id="89c7e-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="89c7e-124">Scope</span><span class="sxs-lookup"><span data-stu-id="89c7e-124">Scope</span></span>
<span data-ttu-id="89c7e-125">排程的事件會呈現的 tooall 雲端服務中的虛擬機器或 tooall 可用性設定組中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="89c7e-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="89c7e-126">如此一來，您應該檢查 hello`Resources`欄位中的 Vm 會影響 toobe hello 事件 tooidentify。</span><span class="sxs-lookup"><span data-stu-id="89c7e-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="89c7e-127">探索 hello 端點</span><span class="sxs-lookup"><span data-stu-id="89c7e-127">Discovering hello endpoint</span></span>
<span data-ttu-id="89c7e-128">在虛擬機器建立虛擬網路 (VNet) 中的位置 hello 的情況下，hello 中繼資料服務可以使用靜態路由的內部 ip 位址，從`169.254.169.254`。</span><span class="sxs-lookup"><span data-stu-id="89c7e-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="89c7e-129">如果 hello 虛擬機器不虛擬網路，hello 預設情況下，雲端服務和傳統的 Vm 中建立額外的邏輯是必要的 toodiscover hello 端點 toouse。</span><span class="sxs-lookup"><span data-stu-id="89c7e-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="89c7e-130">請參閱 toothis 範例 toolearn 如何太[探索 hello 主機端點](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)。</span><span class="sxs-lookup"><span data-stu-id="89c7e-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="89c7e-131">版本控制</span><span class="sxs-lookup"><span data-stu-id="89c7e-131">Versioning</span></span> 
<span data-ttu-id="89c7e-132">hello 執行個體中繼資料服務已進行版本設定。</span><span class="sxs-lookup"><span data-stu-id="89c7e-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="89c7e-133">版本都是必要項，而 hello 目前版本為`2017-03-01`。</span><span class="sxs-lookup"><span data-stu-id="89c7e-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="89c7e-134">預覽舊版的排程為 hello 的 api 版本 {最新} 支援的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="89c7e-135">不再支援這種格式，而且將在未來的 hello 中被取代。</span><span class="sxs-lookup"><span data-stu-id="89c7e-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="89c7e-136">使用標頭</span><span class="sxs-lookup"><span data-stu-id="89c7e-136">Using headers</span></span>
<span data-ttu-id="89c7e-137">當您查詢 hello 中繼資料服務時，您必須提供 hello 標頭`Metadata: true`tooensure hello 要求不小心重新導向。</span><span class="sxs-lookup"><span data-stu-id="89c7e-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="89c7e-138">啟用排定的事件</span><span class="sxs-lookup"><span data-stu-id="89c7e-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="89c7e-139">hello 進行排程的事件，要求第一次 Azure 隱含啟用 hello 功能在您的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="89c7e-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="89c7e-140">如此一來，您應該預期延遲的回應中的總 tootwo 分鐘您第一次呼叫。</span><span class="sxs-lookup"><span data-stu-id="89c7e-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="89c7e-141">使用者起始的維護</span><span class="sxs-lookup"><span data-stu-id="89c7e-141">User initiated maintenance</span></span>
<span data-ttu-id="89c7e-142">使用者啟動的虛擬機器維護透過 hello Azure 入口網站應用程式開發介面、 CLI 或 PowerShell 導致排程的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="89c7e-143">這可讓您在應用程式中的 tootest hello 維護準備邏輯，並允許使用者起始維護您的應用程式 tooprepare。</span><span class="sxs-lookup"><span data-stu-id="89c7e-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="89c7e-144">重新啟動虛擬機器會排定 `Reboot` 類型的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="89c7e-145">重新部署虛擬機器會排定 `Redeploy` 類型的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="89c7e-146">目前最多可同時排程 10 個使用者起始的維護作業。</span><span class="sxs-lookup"><span data-stu-id="89c7e-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="89c7e-147">「排定的事件」正式運作之前，將會放寬這項限制。</span><span class="sxs-lookup"><span data-stu-id="89c7e-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="89c7e-148">使用者起始的維護會導致「排程的事件」，這個狀況目前尚無法設定。</span><span class="sxs-lookup"><span data-stu-id="89c7e-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="89c7e-149">預計在未來版本中，將可針對此狀況作設定。</span><span class="sxs-lookup"><span data-stu-id="89c7e-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="89c7e-150">使用 hello API</span><span class="sxs-lookup"><span data-stu-id="89c7e-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="89c7e-151">查詢事件</span><span class="sxs-lookup"><span data-stu-id="89c7e-151">Query for events</span></span>
<span data-ttu-id="89c7e-152">您可以查詢排程的事件只是藉由呼叫 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="89c7e-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="89c7e-153">回應包含排定的事件陣列。</span><span class="sxs-lookup"><span data-stu-id="89c7e-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="89c7e-154">空白陣列表示目前沒有任何排定的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="89c7e-155">萬一 hello 回應 hello 中排程的事件，包含陣列的事件：</span><span class="sxs-lookup"><span data-stu-id="89c7e-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="89c7e-156">事件屬性</span><span class="sxs-lookup"><span data-stu-id="89c7e-156">Event properties</span></span>
|<span data-ttu-id="89c7e-157">屬性</span><span class="sxs-lookup"><span data-stu-id="89c7e-157">Property</span></span>  |  <span data-ttu-id="89c7e-158">說明</span><span class="sxs-lookup"><span data-stu-id="89c7e-158">Description</span></span> |
| - | - |
| <span data-ttu-id="89c7e-159">EventId</span><span class="sxs-lookup"><span data-stu-id="89c7e-159">EventId</span></span> | <span data-ttu-id="89c7e-160">此事件的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="89c7e-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="89c7e-161">範例：</span><span class="sxs-lookup"><span data-stu-id="89c7e-161">Example:</span></span> <br><ul><li><span data-ttu-id="89c7e-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="89c7e-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="89c7e-163">EventType</span><span class="sxs-lookup"><span data-stu-id="89c7e-163">EventType</span></span> | <span data-ttu-id="89c7e-164">此事件造成的影響。</span><span class="sxs-lookup"><span data-stu-id="89c7e-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="89c7e-165">值：</span><span class="sxs-lookup"><span data-stu-id="89c7e-165">Values:</span></span> <br><ul><li> <span data-ttu-id="89c7e-166">`Freeze`: hello 虛擬機器是排程的 toopause 幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="89c7e-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="89c7e-167">hello CPU 已暫停，但不會影響到記憶體中，開啟的檔案或網路連線。</span><span class="sxs-lookup"><span data-stu-id="89c7e-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="89c7e-168">`Reboot`: hello 已排定重新開機的虛擬機器 （非持續性記憶體是遺失）。</span><span class="sxs-lookup"><span data-stu-id="89c7e-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="89c7e-169">`Redeploy`: hello 虛擬機器是排程的 toomove tooanother 節點 （暫時磁碟會遺失）。</span><span class="sxs-lookup"><span data-stu-id="89c7e-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="89c7e-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="89c7e-170">ResourceType</span></span> | <span data-ttu-id="89c7e-171">受此事件影響的資源類型。</span><span class="sxs-lookup"><span data-stu-id="89c7e-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="89c7e-172">值：</span><span class="sxs-lookup"><span data-stu-id="89c7e-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="89c7e-173">資源</span><span class="sxs-lookup"><span data-stu-id="89c7e-173">Resources</span></span>| <span data-ttu-id="89c7e-174">受此事件影響的資源清單。</span><span class="sxs-lookup"><span data-stu-id="89c7e-174">List of resources this event impacts.</span></span> <span data-ttu-id="89c7e-175">這從最多一個保證 toocontain 機器[更新網域](manage-availability.md)，但不是能包含 hello UD 中的所有機器。</span><span class="sxs-lookup"><span data-stu-id="89c7e-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="89c7e-176">範例：</span><span class="sxs-lookup"><span data-stu-id="89c7e-176">Example:</span></span> <br><ul><li> <span data-ttu-id="89c7e-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="89c7e-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="89c7e-178">事件狀態</span><span class="sxs-lookup"><span data-stu-id="89c7e-178">Event Status</span></span> | <span data-ttu-id="89c7e-179">此事件的狀態。</span><span class="sxs-lookup"><span data-stu-id="89c7e-179">Status of this event.</span></span> <br><br> <span data-ttu-id="89c7e-180">值：</span><span class="sxs-lookup"><span data-stu-id="89c7e-180">Values:</span></span> <ul><li><span data-ttu-id="89c7e-181">`Scheduled`： 此事件是排程的 toostart hello hello 中指定的時間之後`NotBefore`屬性。</span><span class="sxs-lookup"><span data-stu-id="89c7e-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="89c7e-182">`Started`︰已啟動事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="89c7e-183">否`Completed`或曾經提供類似的狀態; hello 事件完成時，將不會再傳回 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="89c7e-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="89c7e-184">NotBefore</span></span>| <span data-ttu-id="89c7e-185">自此之後可能會啟動此事件的時間。</span><span class="sxs-lookup"><span data-stu-id="89c7e-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="89c7e-186">範例：</span><span class="sxs-lookup"><span data-stu-id="89c7e-186">Example:</span></span> <br><ul><li> <span data-ttu-id="89c7e-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="89c7e-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="89c7e-188">事件排定</span><span class="sxs-lookup"><span data-stu-id="89c7e-188">Event scheduling</span></span>
<span data-ttu-id="89c7e-189">每個事件已排程的時間在未來的 hello 最小數量取決於事件類型。</span><span class="sxs-lookup"><span data-stu-id="89c7e-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="89c7e-190">事件的 `NotBefore` 屬性會反映這個時間。</span><span class="sxs-lookup"><span data-stu-id="89c7e-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="89c7e-191">EventType</span><span class="sxs-lookup"><span data-stu-id="89c7e-191">EventType</span></span>  | <span data-ttu-id="89c7e-192">最短時間通知</span><span class="sxs-lookup"><span data-stu-id="89c7e-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="89c7e-193">凍結</span><span class="sxs-lookup"><span data-stu-id="89c7e-193">Freeze</span></span>| <span data-ttu-id="89c7e-194">15 分鐘</span><span class="sxs-lookup"><span data-stu-id="89c7e-194">15 minutes</span></span> |
| <span data-ttu-id="89c7e-195">重新啟動</span><span class="sxs-lookup"><span data-stu-id="89c7e-195">Reboot</span></span> | <span data-ttu-id="89c7e-196">15 分鐘</span><span class="sxs-lookup"><span data-stu-id="89c7e-196">15 minutes</span></span> |
| <span data-ttu-id="89c7e-197">重新部署</span><span class="sxs-lookup"><span data-stu-id="89c7e-197">Redeploy</span></span> | <span data-ttu-id="89c7e-198">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="89c7e-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="89c7e-199">啟動事件</span><span class="sxs-lookup"><span data-stu-id="89c7e-199">Starting an event</span></span> 

<span data-ttu-id="89c7e-200">一旦您已學到的即將發生的事件，並完成您的邏輯非失誤性關機，您可以藉由核准 hello 未處理的事件`POST`呼叫 toohello 中繼資料服務，以 hello `EventId`。</span><span class="sxs-lookup"><span data-stu-id="89c7e-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="89c7e-201">這表示它可以縮短 hello 最小通知 tooAzure 的時間 （可能的話）。</span><span class="sxs-lookup"><span data-stu-id="89c7e-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="89c7e-202">用來認可事件會允許所有 hello 事件 tooproceed `Resources` hello 事件中不只是 hello 會 hello 事件認可的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="89c7e-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="89c7e-203">您可能會因此選擇 tooelect 可能越簡單越 hello hello 中的第一部機器的指引 toocoordinate hello 通知`Resources`欄位。</span><span class="sxs-lookup"><span data-stu-id="89c7e-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="89c7e-204">PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="89c7e-204">PowerShell sample</span></span> 

<span data-ttu-id="89c7e-205">hello 下列查詢範例 hello 排程的事件的中繼資料服務和核准每個未處理的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="89c7e-206">C\# 範例</span><span class="sxs-lookup"><span data-stu-id="89c7e-206">C\# sample</span></span> 

<span data-ttu-id="89c7e-207">hello 下列範例是簡單的用戶端與 hello 中繼資料服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="89c7e-207">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="89c7e-208">可以使用下列資料結構的 hello 表示排程的事件：</span><span class="sxs-lookup"><span data-stu-id="89c7e-208">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="89c7e-209">hello 下列查詢範例 hello 排程的事件的中繼資料服務和核准每個未處理的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-209">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="89c7e-210">Python 範例</span><span class="sxs-lookup"><span data-stu-id="89c7e-210">Python sample</span></span> 

<span data-ttu-id="89c7e-211">hello 下列查詢範例 hello 排程的事件的中繼資料服務和核准每個未處理的事件。</span><span class="sxs-lookup"><span data-stu-id="89c7e-211">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="89c7e-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89c7e-212">Next steps</span></span> 

- <span data-ttu-id="89c7e-213">深入了解 hello Api 可在 hello[執行個體中繼資料服務](instance-metadata-service.md)。</span><span class="sxs-lookup"><span data-stu-id="89c7e-213">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="89c7e-214">了解 [Azure 中 Windows 虛擬機器預定進行的維修](planned-maintenance.md)。</span><span class="sxs-lookup"><span data-stu-id="89c7e-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

