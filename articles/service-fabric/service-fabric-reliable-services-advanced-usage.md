---
title: "Reliable Services 的進階用法 | Microsoft Docs"
description: "深入了解 Service Fabric 的 Reliable Services 的進階用法，以在服務中增加彈性。"
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: a87924faaf5c6c43716b06b6d70ab5100c61f097
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-usage-of-the-reliable-services-programming-model"></a><span data-ttu-id="850bf-103">可靠服務程式設計模型的進階用法</span><span class="sxs-lookup"><span data-stu-id="850bf-103">Advanced usage of the Reliable Services programming model</span></span>
<span data-ttu-id="850bf-104">Azure Service Fabric 可簡化撰寫和管理可靠的無狀態與具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="850bf-104">Azure Service Fabric simplifies writing and managing reliable stateless and stateful services.</span></span> <span data-ttu-id="850bf-105">本指南會討論到 Reliable Services 的進階用法，以在您的服務中取得更多控制權和彈性。</span><span class="sxs-lookup"><span data-stu-id="850bf-105">This guide talks about advanced usages of Reliable Services to gain more control and flexibility over your services.</span></span> <span data-ttu-id="850bf-106">在閱讀這份指南之前，請您先熟悉＜ [可靠的服務程式設計模型](service-fabric-reliable-services-introduction.md)＞。</span><span class="sxs-lookup"><span data-stu-id="850bf-106">Prior to reading this guide, familiarize yourself with [the Reliable Services programming model](service-fabric-reliable-services-introduction.md).</span></span>

<span data-ttu-id="850bf-107">可設定狀態與無狀態服務有使用者程式碼的兩個主要進入點：</span><span class="sxs-lookup"><span data-stu-id="850bf-107">Both stateful and stateless services have two primary entry points for user code:</span></span>

* <span data-ttu-id="850bf-108">`RunAsync(C#) / runAsync(Java)` 是服務程式碼的一般用途進入點。</span><span class="sxs-lookup"><span data-stu-id="850bf-108">`RunAsync(C#) / runAsync(Java)` is a general-purpose entry point for your service code.</span></span>
* <span data-ttu-id="850bf-109">`CreateServiceReplicaListeners(C#)` 和 `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` 適用於開啟用戶端要求的通訊接聽程式。</span><span class="sxs-lookup"><span data-stu-id="850bf-109">`CreateServiceReplicaListeners(C#)` and `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` is for opening communication listeners for client requests.</span></span>

<span data-ttu-id="850bf-110">對於大部分服務而言，這些兩個進入點已足夠。</span><span class="sxs-lookup"><span data-stu-id="850bf-110">For most services, these two entry points are sufficient.</span></span> <span data-ttu-id="850bf-111">在少數情況下，需要更充分掌控服務的命週期時，可以使用其他生命週期事件。</span><span class="sxs-lookup"><span data-stu-id="850bf-111">In rare cases when more control over a service's lifecycle is required, additional lifecycle events are available.</span></span>

## <a name="stateless-service-instance-lifecycle"></a><span data-ttu-id="850bf-112">無狀態服務執行個體生命週期</span><span class="sxs-lookup"><span data-stu-id="850bf-112">Stateless service instance lifecycle</span></span>
<span data-ttu-id="850bf-113">無狀態服務的生命週期非常簡單。</span><span class="sxs-lookup"><span data-stu-id="850bf-113">A stateless service's lifecycle is very simple.</span></span> <span data-ttu-id="850bf-114">無狀態服務只能開啟、關閉或中止。</span><span class="sxs-lookup"><span data-stu-id="850bf-114">A stateless service can only be opened, closed, or aborted.</span></span> <span data-ttu-id="850bf-115">無狀態服務中的 `RunAsync` 會在服務執行個體開啟時執行，並在服務執行個體關閉或中止時取消。</span><span class="sxs-lookup"><span data-stu-id="850bf-115">`RunAsync` in a stateless service is executed when a service instance is opened, and canceled when a service instance is closed or aborted.</span></span>

<span data-ttu-id="850bf-116">雖然 `RunAsync` 應該足以應付幾乎所有情況，但也可使用無狀態服務中的開啟、關閉和中止事件︰</span><span class="sxs-lookup"><span data-stu-id="850bf-116">Although `RunAsync` should be sufficient in almost all cases, the open, close, and abort events in a stateless service are also available:</span></span>

* <span data-ttu-id="850bf-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java` 即將使用無狀態服務執行個體時，會呼叫 OnOpenAsync。</span><span class="sxs-lookup"><span data-stu-id="850bf-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java` OnOpenAsync is called when the stateless service instance is about to be used.</span></span> <span data-ttu-id="850bf-118">這個階段可以啟動擴充服務的初始化作業。</span><span class="sxs-lookup"><span data-stu-id="850bf-118">Extended service initialization tasks can be started at this time.</span></span>
* <span data-ttu-id="850bf-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java` 無狀態服務執行個體即將正常關閉時，會呼叫 OnCloseAsync。</span><span class="sxs-lookup"><span data-stu-id="850bf-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java` OnCloseAsync is called when the stateless service instance is going to be gracefully shut down.</span></span> <span data-ttu-id="850bf-120">這可能在升級服務程式碼、因負載平衡而移動服務執行個體或偵測到暫時性失敗的時侯發生。</span><span class="sxs-lookup"><span data-stu-id="850bf-120">This can occur when the service's code is being upgraded, the service instance is being moved due to load balancing, or a transient fault is detected.</span></span> <span data-ttu-id="850bf-121">OnCloseAsync 可以用來安全地關閉任何資源、停止任何背景處理、完成外部狀態儲存或關閉現有的連接。</span><span class="sxs-lookup"><span data-stu-id="850bf-121">OnCloseAsync can be used to safely close any resources, stop any background processing, finish saving external state, or close down existing connections.</span></span>
* <span data-ttu-id="850bf-122">`void OnAbort() - C# / void onAbort() - Java` 正要強制關閉無狀態服務執行個體時，會呼叫 OnAbort。</span><span class="sxs-lookup"><span data-stu-id="850bf-122">`void OnAbort() - C# / void onAbort() - Java` OnAbort is called when the stateless service instance is being forcefully shut down.</span></span> <span data-ttu-id="850bf-123">這個一般會在於節點上偵測到永久錯誤，或因內部失敗而 Service Fabric 無法可靠地管理服務執行個體生命週期時呼叫。</span><span class="sxs-lookup"><span data-stu-id="850bf-123">This is generally called when a permanent fault is detected on the node, or when Service Fabric cannot reliably manage the service instance's lifecycle due to internal failures.</span></span>

## <a name="stateful-service-replica-lifecycle"></a><span data-ttu-id="850bf-124">具狀態服務複本生命週期</span><span class="sxs-lookup"><span data-stu-id="850bf-124">Stateful service replica lifecycle</span></span>

> [!NOTE]
> <span data-ttu-id="850bf-125">Java 中尚未支援具狀態 Reliable Services。</span><span class="sxs-lookup"><span data-stu-id="850bf-125">Stateful reliable services are not supported in Java yet.</span></span>
>
>

<span data-ttu-id="850bf-126">具狀態服務複本的生命週期比無狀態服務執行個體更為複雜。</span><span class="sxs-lookup"><span data-stu-id="850bf-126">A stateful service replica's lifecycle is much more complex than a stateless service instance.</span></span> <span data-ttu-id="850bf-127">除了開啟、關閉和中止事件，具狀態服務複本會在其生命週期內經歷角色變更。</span><span class="sxs-lookup"><span data-stu-id="850bf-127">In addition to open, close, and abort events, a stateful service replica undergoes role changes during its lifetime.</span></span> <span data-ttu-id="850bf-128">當具狀態服務複本變更角色時，會觸發 `OnChangeRoleAsync` 事件︰</span><span class="sxs-lookup"><span data-stu-id="850bf-128">When a stateful service replica changes role, the `OnChangeRoleAsync` event is triggered:</span></span>

* <span data-ttu-id="850bf-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)` OnChangeRoleAsync。</span><span class="sxs-lookup"><span data-stu-id="850bf-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)` OnChangeRoleAsync is called when the stateful service replica is changing role, for example to primary or secondary.</span></span> <span data-ttu-id="850bf-130">主要複本會獲得寫入狀態 (可建立並寫入可靠的集合)。</span><span class="sxs-lookup"><span data-stu-id="850bf-130">Primary replicas are given write status (are allowed to create and write to Reliable Collections).</span></span> <span data-ttu-id="850bf-131">次要複本則會獲得讀取狀態 (只能從現有的可靠集合讀取)。</span><span class="sxs-lookup"><span data-stu-id="850bf-131">Secondary replicas are given read status (can only read from existing Reliable Collections).</span></span> <span data-ttu-id="850bf-132">具狀態服務中的大部分工作會在主要複本執行。</span><span class="sxs-lookup"><span data-stu-id="850bf-132">Most work in a stateful service is performed at the primary replica.</span></span> <span data-ttu-id="850bf-133">次要複本可以執行唯讀驗證、產生報表、資料採礦或其他唯讀作業。</span><span class="sxs-lookup"><span data-stu-id="850bf-133">Secondary replicas can perform read-only validation, report generation, data mining, or other read-only jobs.</span></span>

<span data-ttu-id="850bf-134">在具狀態服務中，只有主要複本具有狀態的寫入權限，因此通常在服務正在執行實際工作時。</span><span class="sxs-lookup"><span data-stu-id="850bf-134">In a stateful service, only the primary replica has write access to state and thus is generally when the service is performing actual work.</span></span> <span data-ttu-id="850bf-135">只有在具狀態服務複本為主要複本時，才會執行具狀態服務中的 `RunAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="850bf-135">The `RunAsync` method in a stateful service is executed only when the stateful service replica is primary.</span></span> <span data-ttu-id="850bf-136">`RunAsync` 方法會在主要複本的角色變成非主要時，以及在關閉和中止事件期間取消。</span><span class="sxs-lookup"><span data-stu-id="850bf-136">The `RunAsync` method is canceled when a primary replica's role changes away from primary, as well as during the close and abort events.</span></span>

<span data-ttu-id="850bf-137">使用 `OnChangeRoleAsync` 事件可讓您視複本角色執行工作，以及回應角色變更。</span><span class="sxs-lookup"><span data-stu-id="850bf-137">Using the `OnChangeRoleAsync` event allows you to perform work depending on replica role as well as in response to role change.</span></span>

<span data-ttu-id="850bf-138">具狀態服務也會提供與無狀態服務相同的四個生命週期事件，並具有相同的語意和使用案例：</span><span class="sxs-lookup"><span data-stu-id="850bf-138">A stateful service also provides the same four lifecycle events as a stateless service, with the same semantics and use cases:</span></span>

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a><span data-ttu-id="850bf-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="850bf-139">Next steps</span></span>
<span data-ttu-id="850bf-140">如需更多與 Service Fabric 相關的進階主題，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="850bf-140">For more advanced topics related to Service Fabric, see the following articles:</span></span>

* [<span data-ttu-id="850bf-141">設定具狀態的 Reliable Services</span><span class="sxs-lookup"><span data-stu-id="850bf-141">Configuring stateful Reliable Services</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="850bf-142">Service Fabric 健康狀態簡介</span><span class="sxs-lookup"><span data-stu-id="850bf-142">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="850bf-143">使用系統健康狀態報告進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="850bf-143">Using system health reports for troubleshooting</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="850bf-144">使用 Service Fabric 叢集資源管理員設定服務</span><span class="sxs-lookup"><span data-stu-id="850bf-144">Configuring Services with the Service Fabric Cluster Resource Manager</span></span>](service-fabric-cluster-resource-manager-configure-services.md)
