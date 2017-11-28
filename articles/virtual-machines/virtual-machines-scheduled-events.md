---
title: "排定的事件與 Azure 的中繼資料服務 | Microsoft Docs"
description: "在具影響力的事件發生之前，對虛擬機器上的這類事件做出回應。"
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
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: 793803bfc12059a68ec881da9de37116f7a0eb8c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="614d6-103">Azure 中繼資料服務 - 排定的事件 (預覽)</span><span class="sxs-lookup"><span data-stu-id="614d6-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="614d6-104">若您同意使用規定即可取得預覽。</span><span class="sxs-lookup"><span data-stu-id="614d6-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="614d6-105">如需詳細資訊，請參閱 [Microsoft Azure 預覽版增補使用條款](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)。</span><span class="sxs-lookup"><span data-stu-id="614d6-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="614d6-106">排定的事件是 Azure 中繼資料服務下的其中一項子服務，</span><span class="sxs-lookup"><span data-stu-id="614d6-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="614d6-107">其會呈現即將發生的事件 (例如，重新開機) 相關資訊，以便應用程式做好準備並限制中斷造成的影響。</span><span class="sxs-lookup"><span data-stu-id="614d6-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="614d6-108">它適用於所有 Azure 虛擬機器類型 (包括 PaaS 和 IaaS)。</span><span class="sxs-lookup"><span data-stu-id="614d6-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="614d6-109">排定的事件讓虛擬機器有時間執行預防性工作，以將事件的影響降至最低。</span><span class="sxs-lookup"><span data-stu-id="614d6-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="614d6-110">簡介 - 為何使用排定的事件？</span><span class="sxs-lookup"><span data-stu-id="614d6-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="614d6-111">使用排定的事件時，您可以採取措施，限制平台起始的維護及使用者起始的動作對服務造成的影響。</span><span class="sxs-lookup"><span data-stu-id="614d6-111">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="614d6-112">當多個執行個體間發生中斷時，多重執行個體的工作負載 (其使用複寫技術來維護狀態) 可能非常容易受到牽連。</span><span class="sxs-lookup"><span data-stu-id="614d6-112">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="614d6-113">例如中斷可能會導致耗費資源的工作 (例如，重建索引) 或甚至是複本遺失。</span><span class="sxs-lookup"><span data-stu-id="614d6-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="614d6-114">在其他許多情況下，使用正常關機順序可改善整體服務可用性，例如完成 (或取消) 進行中的交易、重新指派工作給叢集中的其他 VM (手動容錯移轉)，或從網路負載平衡器集區移除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="614d6-114">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="614d6-115">而在某些情況下，通知系統管理員有關即將發生的事件，或記錄這類事件，都有助改善裝載於雲端之應用程式的服務性。</span><span class="sxs-lookup"><span data-stu-id="614d6-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="614d6-116">Azure 中繼資料服務會在下列使用案例中呈現排定的事件︰</span><span class="sxs-lookup"><span data-stu-id="614d6-116">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="614d6-117">平台起始的維護 (例如，主機作業系統推出)</span><span class="sxs-lookup"><span data-stu-id="614d6-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="614d6-118">使用者起始的呼叫 (例如，使用者重新啟動或重新部署 VM)</span><span class="sxs-lookup"><span data-stu-id="614d6-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---the-basics"></a><span data-ttu-id="614d6-119">排定的事件 - 基本概念</span><span class="sxs-lookup"><span data-stu-id="614d6-119">Scheduled Events - The Basics</span></span>  

<span data-ttu-id="614d6-120">如果您是使用可由 VM 內存取的 REST 端點來執行虛擬機器，Azure 中繼資料服務會公開這類相關資訊。</span><span class="sxs-lookup"><span data-stu-id="614d6-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="614d6-121">這項資訊是透過無法路由傳送的 IP 取得，因此不會在 VM 之外公開。</span><span class="sxs-lookup"><span data-stu-id="614d6-121">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="614d6-122">Scope</span><span class="sxs-lookup"><span data-stu-id="614d6-122">Scope</span></span>
<span data-ttu-id="614d6-123">排定的事件會對雲端服務中的所有虛擬機器或可用性設定組中的所有虛擬機器呈現。</span><span class="sxs-lookup"><span data-stu-id="614d6-123">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="614d6-124">因此，您應該檢查事件中的 `Resources` 欄位以找出哪些 VM 即將受到影響。</span><span class="sxs-lookup"><span data-stu-id="614d6-124">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="614d6-125">探索端點</span><span class="sxs-lookup"><span data-stu-id="614d6-125">Discovering the Endpoint</span></span>
<span data-ttu-id="614d6-126">如果虛擬機器是在虛擬網路 (VNet) 中建立的情況下，可從無法路由傳送的靜態 IP (`169.254.169.254`) 取得中繼資料服務。</span><span class="sxs-lookup"><span data-stu-id="614d6-126">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="614d6-127">如果虛擬機器不是在虛擬網路中建立，則針對雲端服務和傳統 VM 的預設案例，需要其他邏輯來探索可使用的端點。</span><span class="sxs-lookup"><span data-stu-id="614d6-127">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="614d6-128">請參閱此範例以了解如何[探索主機端點](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)。</span><span class="sxs-lookup"><span data-stu-id="614d6-128">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="614d6-129">版本控制</span><span class="sxs-lookup"><span data-stu-id="614d6-129">Versioning</span></span> 
<span data-ttu-id="614d6-130">執行個體中繼資料服務已建立版本。</span><span class="sxs-lookup"><span data-stu-id="614d6-130">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="614d6-131">版本是必要項目，且目前版本為 `2017-03-01`。</span><span class="sxs-lookup"><span data-stu-id="614d6-131">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="614d6-132">先前排定事件的預覽版支援作為 API 版本的 {latest}。</span><span class="sxs-lookup"><span data-stu-id="614d6-132">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="614d6-133">此格式將不再受到支援且之後會遭到取代。</span><span class="sxs-lookup"><span data-stu-id="614d6-133">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="614d6-134">使用標頭</span><span class="sxs-lookup"><span data-stu-id="614d6-134">Using Headers</span></span>
<span data-ttu-id="614d6-135">查詢中繼資料服務時，您必須提供 `Metadata: true` 標頭以免不小心重新導向要求。</span><span class="sxs-lookup"><span data-stu-id="614d6-135">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="614d6-136">啟用排定的事件</span><span class="sxs-lookup"><span data-stu-id="614d6-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="614d6-137">第一次要求排定的事件時，Azure 會在您的虛擬機器上隱含啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="614d6-137">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="614d6-138">因此，您可能會在第一次呼叫中遇到長達兩分鐘的延遲回應。</span><span class="sxs-lookup"><span data-stu-id="614d6-138">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="614d6-139">使用者起始的維護</span><span class="sxs-lookup"><span data-stu-id="614d6-139">User Initiated Maintenance</span></span>
<span data-ttu-id="614d6-140">使用者透過 Azure 入口網站、API、CLI 或 PowerShell 起始的虛擬機器維護，將會產生「排程的事件」。</span><span class="sxs-lookup"><span data-stu-id="614d6-140">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="614d6-141">這可讓您測試應用程式中的維護準備邏輯，讓應用程式可以為使用者啟動的維護預作準備。</span><span class="sxs-lookup"><span data-stu-id="614d6-141">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="614d6-142">重新啟動虛擬機器將會排程 `Reboot` 類型的事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="614d6-143">重新部署虛擬機器將會排程 `Redeploy` 類型的事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="614d6-144">目前最多可同時排程 10 個使用者起始的維護作業。</span><span class="sxs-lookup"><span data-stu-id="614d6-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="614d6-145">「排程的事件」正式運作之前，將會放寬這項限制。</span><span class="sxs-lookup"><span data-stu-id="614d6-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="614d6-146">使用者起始的維護會導致「排程的事件」，這個狀況目前尚無法設定。</span><span class="sxs-lookup"><span data-stu-id="614d6-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="614d6-147">預計在未來版本中，將可針對此狀況作設定。</span><span class="sxs-lookup"><span data-stu-id="614d6-147">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="614d6-148">使用 API</span><span class="sxs-lookup"><span data-stu-id="614d6-148">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="614d6-149">查詢事件</span><span class="sxs-lookup"><span data-stu-id="614d6-149">Query for events</span></span>
<span data-ttu-id="614d6-150">您只要進行下列呼叫，即可查詢排定的事件：</span><span class="sxs-lookup"><span data-stu-id="614d6-150">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="614d6-151">回應包含排定的事件陣列。</span><span class="sxs-lookup"><span data-stu-id="614d6-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="614d6-152">空白陣列表示目前沒有任何排定的事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="614d6-153">在有排定事件的情況下，回應會包含事件陣列︰</span><span class="sxs-lookup"><span data-stu-id="614d6-153">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="614d6-154">事件屬性</span><span class="sxs-lookup"><span data-stu-id="614d6-154">Event Properties</span></span>
|<span data-ttu-id="614d6-155">屬性</span><span class="sxs-lookup"><span data-stu-id="614d6-155">Property</span></span>  |  <span data-ttu-id="614d6-156">說明</span><span class="sxs-lookup"><span data-stu-id="614d6-156">Description</span></span> |
| - | - |
| <span data-ttu-id="614d6-157">EventId</span><span class="sxs-lookup"><span data-stu-id="614d6-157">EventId</span></span> | <span data-ttu-id="614d6-158">此事件的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="614d6-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="614d6-159">範例：</span><span class="sxs-lookup"><span data-stu-id="614d6-159">Example:</span></span> <br><ul><li><span data-ttu-id="614d6-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="614d6-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="614d6-161">EventType</span><span class="sxs-lookup"><span data-stu-id="614d6-161">EventType</span></span> | <span data-ttu-id="614d6-162">此事件造成的影響。</span><span class="sxs-lookup"><span data-stu-id="614d6-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="614d6-163">值：</span><span class="sxs-lookup"><span data-stu-id="614d6-163">Values:</span></span> <br><ul><li> <span data-ttu-id="614d6-164">`Freeze`︰虛擬機器已排定會暫停幾秒鐘。</span><span class="sxs-lookup"><span data-stu-id="614d6-164">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="614d6-165">CPU 會暫止，但不會影響記憶體、開啟的檔案或網路連線。</span><span class="sxs-lookup"><span data-stu-id="614d6-165">The CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="614d6-166">`Reboot`：虛擬機器已排定要重新開機 (非持續性記憶體都會遺失)。</span><span class="sxs-lookup"><span data-stu-id="614d6-166">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="614d6-167">`Redeploy`︰虛擬機器已排定要移至另一個節點 (暫時磁碟都會遺失)。</span><span class="sxs-lookup"><span data-stu-id="614d6-167">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="614d6-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="614d6-168">ResourceType</span></span> | <span data-ttu-id="614d6-169">受此事件影響的資源類型。</span><span class="sxs-lookup"><span data-stu-id="614d6-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="614d6-170">值：</span><span class="sxs-lookup"><span data-stu-id="614d6-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="614d6-171">資源</span><span class="sxs-lookup"><span data-stu-id="614d6-171">Resources</span></span>| <span data-ttu-id="614d6-172">受此事件影響的資源清單。</span><span class="sxs-lookup"><span data-stu-id="614d6-172">List of resources this event impacts.</span></span> <span data-ttu-id="614d6-173">其中最多只能包含來自一個[更新網域](windows/manage-availability.md)的機器，但不能包含更新網域中的所有機器。</span><span class="sxs-lookup"><span data-stu-id="614d6-173">This is guaranteed to contain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="614d6-174">範例：</span><span class="sxs-lookup"><span data-stu-id="614d6-174">Example:</span></span> <br><ul><li> <span data-ttu-id="614d6-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="614d6-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="614d6-176">事件狀態</span><span class="sxs-lookup"><span data-stu-id="614d6-176">Event Status</span></span> | <span data-ttu-id="614d6-177">此事件的狀態。</span><span class="sxs-lookup"><span data-stu-id="614d6-177">Status of this event.</span></span> <br><br> <span data-ttu-id="614d6-178">值：</span><span class="sxs-lookup"><span data-stu-id="614d6-178">Values:</span></span> <ul><li><span data-ttu-id="614d6-179">`Scheduled`︰此事件已排定在 `NotBefore` 屬性所指定的時間之後啟動。</span><span class="sxs-lookup"><span data-stu-id="614d6-179">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="614d6-180">`Started`︰已啟動事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="614d6-181">如果未提供任何 `Completed` 或類似的狀態，事件完成時，將不會再傳回事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-181">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="614d6-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="614d6-182">NotBefore</span></span>| <span data-ttu-id="614d6-183">自此之後可能會啟動此事件的時間。</span><span class="sxs-lookup"><span data-stu-id="614d6-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="614d6-184">範例：</span><span class="sxs-lookup"><span data-stu-id="614d6-184">Example:</span></span> <br><ul><li> <span data-ttu-id="614d6-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="614d6-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="614d6-186">事件排程</span><span class="sxs-lookup"><span data-stu-id="614d6-186">Event Scheduling</span></span>
<span data-ttu-id="614d6-187">系統會根據事件類型，為每個事件在未來安排最少的時間量。</span><span class="sxs-lookup"><span data-stu-id="614d6-187">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="614d6-188">事件的 `NotBefore` 屬性會反映這個時間。</span><span class="sxs-lookup"><span data-stu-id="614d6-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="614d6-189">EventType</span><span class="sxs-lookup"><span data-stu-id="614d6-189">EventType</span></span>  | <span data-ttu-id="614d6-190">最短時間通知</span><span class="sxs-lookup"><span data-stu-id="614d6-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="614d6-191">凍結</span><span class="sxs-lookup"><span data-stu-id="614d6-191">Freeze</span></span>| <span data-ttu-id="614d6-192">15 分鐘</span><span class="sxs-lookup"><span data-stu-id="614d6-192">15 minutes</span></span> |
| <span data-ttu-id="614d6-193">重新啟動</span><span class="sxs-lookup"><span data-stu-id="614d6-193">Reboot</span></span> | <span data-ttu-id="614d6-194">15 分鐘</span><span class="sxs-lookup"><span data-stu-id="614d6-194">15 minutes</span></span> |
| <span data-ttu-id="614d6-195">重新部署</span><span class="sxs-lookup"><span data-stu-id="614d6-195">Redeploy</span></span> | <span data-ttu-id="614d6-196">10 分鐘</span><span class="sxs-lookup"><span data-stu-id="614d6-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="614d6-197">啟動事件 (加速)</span><span class="sxs-lookup"><span data-stu-id="614d6-197">Starting an event (expedite)</span></span>

<span data-ttu-id="614d6-198">在您得知即將發生的事件，並完成正常關機邏輯之後，即可使用 `EventId` 向中繼資料服務進行 `POST` 呼叫，以核准未處理的事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="614d6-199">對 Azure 來說，這意謂著它可以將通知時間縮到最短 (可能的話)。</span><span class="sxs-lookup"><span data-stu-id="614d6-199">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="614d6-200">認可事件時，即會允許事件中所有 `Resources` 的事件繼續進行，而不僅是認可此事件的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="614d6-200">Acknowledging a event will allow the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="614d6-201">因此，您可以選擇一個領導者來協調認可；最簡單的方法是選擇 `Resources` 欄位的第一部機器。</span><span class="sxs-lookup"><span data-stu-id="614d6-201">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="614d6-202">範例</span><span class="sxs-lookup"><span data-stu-id="614d6-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="614d6-203">PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="614d6-203">PowerShell Sample</span></span> 

<span data-ttu-id="614d6-204">下列範例會查詢中繼資料服務來找出已排定的事件，並核准每個未處理的事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-204">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
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


### <a name="c-sample"></a><span data-ttu-id="614d6-205">C\# 範例</span><span class="sxs-lookup"><span data-stu-id="614d6-205">C\# Sample</span></span> 

<span data-ttu-id="614d6-206">下列範例是用來與中繼資料服務進行通訊的簡單用戶端。</span><span class="sxs-lookup"><span data-stu-id="614d6-206">The following sample is of a simple client that communicates with the metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up the scheduled events URI for a VNET-enabled VM
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

<span data-ttu-id="614d6-207">您可以使用下列資料結構來代表排定的事件：</span><span class="sxs-lookup"><span data-stu-id="614d6-207">Scheduled Events can be represented using the following data structures:</span></span>

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

<span data-ttu-id="614d6-208">下列範例會查詢中繼資料服務來找出已排定的事件，並核准每個未處理的事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-208">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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
            Console.WriteLine("Press Enter to approve executing events\n");
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

            Console.WriteLine("Complete. Press enter to repeat\n\n");
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

### <a name="python-sample"></a><span data-ttu-id="614d6-209">Python 範例</span><span class="sxs-lookup"><span data-stu-id="614d6-209">Python Sample</span></span> 

<span data-ttu-id="614d6-210">下列範例會查詢中繼資料服務來找出已排定的事件，並核准每個未處理的事件。</span><span class="sxs-lookup"><span data-stu-id="614d6-210">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="614d6-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="614d6-211">Next Steps</span></span> 

- <span data-ttu-id="614d6-212">深入了解[執行個體中繼資料服務](virtual-machines-instancemetadataservice-overview.md)中提供的 API。</span><span class="sxs-lookup"><span data-stu-id="614d6-212">Read more about the APIs available in the [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="614d6-213">了解 [Azure 中 Windows 虛擬機器預定進行的維修](windows/planned-maintenance.md)。</span><span class="sxs-lookup"><span data-stu-id="614d6-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="614d6-214">了解 [Azure 中 Linux 虛擬機器預定進行的維修](linux/planned-maintenance.md)。</span><span class="sxs-lookup"><span data-stu-id="614d6-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
