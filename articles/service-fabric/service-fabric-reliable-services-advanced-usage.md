---
title: "可靠的服務使用量 aaaAdvanced |Microsoft 文件"
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
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a><span data-ttu-id="39ab2-103">進階的 hello 可靠服務程式設計模型使用方式</span><span class="sxs-lookup"><span data-stu-id="39ab2-103">Advanced usage of hello Reliable Services programming model</span></span>
<span data-ttu-id="39ab2-104">Azure Service Fabric 可簡化撰寫和管理可靠的無狀態與具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="39ab2-104">Azure Service Fabric simplifies writing and managing reliable stateless and stateful services.</span></span> <span data-ttu-id="39ab2-105">本指南示範的可靠服務 toogain 進階使用方式的相關更多控制權和彈性透過您的服務。</span><span class="sxs-lookup"><span data-stu-id="39ab2-105">This guide talks about advanced usages of Reliable Services toogain more control and flexibility over your services.</span></span> <span data-ttu-id="39ab2-106">此指南先前 tooreading，熟悉[hello 可靠服務程式設計模型](service-fabric-reliable-services-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="39ab2-106">Prior tooreading this guide, familiarize yourself with [hello Reliable Services programming model](service-fabric-reliable-services-introduction.md).</span></span>

<span data-ttu-id="39ab2-107">可設定狀態與無狀態服務有使用者程式碼的兩個主要進入點：</span><span class="sxs-lookup"><span data-stu-id="39ab2-107">Both stateful and stateless services have two primary entry points for user code:</span></span>

* <span data-ttu-id="39ab2-108">`RunAsync(C#) / runAsync(Java)` 是服務程式碼的一般用途進入點。</span><span class="sxs-lookup"><span data-stu-id="39ab2-108">`RunAsync(C#) / runAsync(Java)` is a general-purpose entry point for your service code.</span></span>
* <span data-ttu-id="39ab2-109">`CreateServiceReplicaListeners(C#)` 和 `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` 適用於開啟用戶端要求的通訊接聽程式。</span><span class="sxs-lookup"><span data-stu-id="39ab2-109">`CreateServiceReplicaListeners(C#)` and `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` is for opening communication listeners for client requests.</span></span>

<span data-ttu-id="39ab2-110">對於大部分服務而言，這些兩個進入點已足夠。</span><span class="sxs-lookup"><span data-stu-id="39ab2-110">For most services, these two entry points are sufficient.</span></span> <span data-ttu-id="39ab2-111">在少數情況下，需要更充分掌控服務的命週期時，可以使用其他生命週期事件。</span><span class="sxs-lookup"><span data-stu-id="39ab2-111">In rare cases when more control over a service's lifecycle is required, additional lifecycle events are available.</span></span>

## <a name="stateless-service-instance-lifecycle"></a><span data-ttu-id="39ab2-112">無狀態服務執行個體生命週期</span><span class="sxs-lookup"><span data-stu-id="39ab2-112">Stateless service instance lifecycle</span></span>
<span data-ttu-id="39ab2-113">無狀態服務的生命週期非常簡單。</span><span class="sxs-lookup"><span data-stu-id="39ab2-113">A stateless service's lifecycle is very simple.</span></span> <span data-ttu-id="39ab2-114">無狀態服務只能開啟、關閉或中止。</span><span class="sxs-lookup"><span data-stu-id="39ab2-114">A stateless service can only be opened, closed, or aborted.</span></span> <span data-ttu-id="39ab2-115">無狀態服務中的 `RunAsync` 會在服務執行個體開啟時執行，並在服務執行個體關閉或中止時取消。</span><span class="sxs-lookup"><span data-stu-id="39ab2-115">`RunAsync` in a stateless service is executed when a service instance is opened, and canceled when a service instance is closed or aborted.</span></span>

<span data-ttu-id="39ab2-116">雖然`RunAsync`應該很足夠中幾乎所有的情況下，hello 開啟時，關閉，並中止事件中無狀態服務也會提供：</span><span class="sxs-lookup"><span data-stu-id="39ab2-116">Although `RunAsync` should be sufficient in almost all cases, hello open, close, and abort events in a stateless service are also available:</span></span>

* <span data-ttu-id="39ab2-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`關於使用 toobe hello 無狀態服務執行個體時，會呼叫 OnOpenAsync。</span><span class="sxs-lookup"><span data-stu-id="39ab2-117">`Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java` OnOpenAsync is called when hello stateless service instance is about toobe used.</span></span> <span data-ttu-id="39ab2-118">這個階段可以啟動擴充服務的初始化作業。</span><span class="sxs-lookup"><span data-stu-id="39ab2-118">Extended service initialization tasks can be started at this time.</span></span>
* <span data-ttu-id="39ab2-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync 稱為 hello 無狀態服務執行個體即將 toobe 時正常關閉。</span><span class="sxs-lookup"><span data-stu-id="39ab2-119">`Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java` OnCloseAsync is called when hello stateless service instance is going toobe gracefully shut down.</span></span> <span data-ttu-id="39ab2-120">發生這個問題正在升級 hello 服務的程式碼、 tooload 平衡，因為正在移動 hello 服務執行個體或偵測到暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="39ab2-120">This can occur when hello service's code is being upgraded, hello service instance is being moved due tooload balancing, or a transient fault is detected.</span></span> <span data-ttu-id="39ab2-121">OnCloseAsync 可以關閉使用的 toosafely 任何資源，停止任何背景處理、 完成儲存外部的狀態，或關閉現有連接。</span><span class="sxs-lookup"><span data-stu-id="39ab2-121">OnCloseAsync can be used toosafely close any resources, stop any background processing, finish saving external state, or close down existing connections.</span></span>
* <span data-ttu-id="39ab2-122">`void OnAbort() - C# / void onAbort() - Java`OnAbort 稱為 hello 無狀態服務執行個體被強制關閉時。</span><span class="sxs-lookup"><span data-stu-id="39ab2-122">`void OnAbort() - C# / void onAbort() - Java` OnAbort is called when hello stateless service instance is being forcefully shut down.</span></span> <span data-ttu-id="39ab2-123">這通常稱為 hello 節點上偵測到永久錯誤時，或 Service Fabric 無法可靠地管理 hello 服務執行個體的生命週期到期 toointernal 失敗時。</span><span class="sxs-lookup"><span data-stu-id="39ab2-123">This is generally called when a permanent fault is detected on hello node, or when Service Fabric cannot reliably manage hello service instance's lifecycle due toointernal failures.</span></span>

## <a name="stateful-service-replica-lifecycle"></a><span data-ttu-id="39ab2-124">具狀態服務複本生命週期</span><span class="sxs-lookup"><span data-stu-id="39ab2-124">Stateful service replica lifecycle</span></span>

> [!NOTE]
> <span data-ttu-id="39ab2-125">Java 中尚未支援具狀態 Reliable Services。</span><span class="sxs-lookup"><span data-stu-id="39ab2-125">Stateful reliable services are not supported in Java yet.</span></span>
>
>

<span data-ttu-id="39ab2-126">具狀態服務複本的生命週期比無狀態服務執行個體更為複雜。</span><span class="sxs-lookup"><span data-stu-id="39ab2-126">A stateful service replica's lifecycle is much more complex than a stateless service instance.</span></span> <span data-ttu-id="39ab2-127">此外 tooopen，關閉並終止事件，可設定狀態的服務複本正在進行角色變更，在其存留期間。</span><span class="sxs-lookup"><span data-stu-id="39ab2-127">In addition tooopen, close, and abort events, a stateful service replica undergoes role changes during its lifetime.</span></span> <span data-ttu-id="39ab2-128">當具狀態服務複本變更角色時，hello`OnChangeRoleAsync`觸發事件：</span><span class="sxs-lookup"><span data-stu-id="39ab2-128">When a stateful service replica changes role, hello `OnChangeRoleAsync` event is triggered:</span></span>

* <span data-ttu-id="39ab2-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync 稱為 hello 可設定狀態的服務複本變更角色，例如 tooprimary 或次要資料庫時。</span><span class="sxs-lookup"><span data-stu-id="39ab2-129">`Task OnChangeRoleAsync(ReplicaRole, CancellationToken)` OnChangeRoleAsync is called when hello stateful service replica is changing role, for example tooprimary or secondary.</span></span> <span data-ttu-id="39ab2-130">主要複本可以寫入狀態 （允許 toocreate 和寫入 tooReliable 集合）。</span><span class="sxs-lookup"><span data-stu-id="39ab2-130">Primary replicas are given write status (are allowed toocreate and write tooReliable Collections).</span></span> <span data-ttu-id="39ab2-131">次要複本則會獲得讀取狀態 (只能從現有的可靠集合讀取)。</span><span class="sxs-lookup"><span data-stu-id="39ab2-131">Secondary replicas are given read status (can only read from existing Reliable Collections).</span></span> <span data-ttu-id="39ab2-132">可設定狀態的服務中的大多數工作是在 hello 主要複本執行。</span><span class="sxs-lookup"><span data-stu-id="39ab2-132">Most work in a stateful service is performed at hello primary replica.</span></span> <span data-ttu-id="39ab2-133">次要複本可以執行唯讀驗證、產生報表、資料採礦或其他唯讀作業。</span><span class="sxs-lookup"><span data-stu-id="39ab2-133">Secondary replicas can perform read-only validation, report generation, data mining, or other read-only jobs.</span></span>

<span data-ttu-id="39ab2-134">在可設定狀態的服務中，hello 主要複本會具有寫入權限 toostate，並因此通常是 hello 服務執行實際工作時。</span><span class="sxs-lookup"><span data-stu-id="39ab2-134">In a stateful service, only hello primary replica has write access toostate and thus is generally when hello service is performing actual work.</span></span> <span data-ttu-id="39ab2-135">hello`RunAsync`執行 hello 可設定狀態的服務複本為主要時，才可設定狀態的服務中的方法。</span><span class="sxs-lookup"><span data-stu-id="39ab2-135">hello `RunAsync` method in a stateful service is executed only when hello stateful service replica is primary.</span></span> <span data-ttu-id="39ab2-136">hello`RunAsync`方法取消當主要複本的角色變更從主要資料庫，以及在 hello 期間關閉，並中止事件。</span><span class="sxs-lookup"><span data-stu-id="39ab2-136">hello `RunAsync` method is canceled when a primary replica's role changes away from primary, as well as during hello close and abort events.</span></span>

<span data-ttu-id="39ab2-137">使用 hello`OnChangeRoleAsync`事件可讓您根據複本角色也如同回應 toorole 變更 tooperform 工作。</span><span class="sxs-lookup"><span data-stu-id="39ab2-137">Using hello `OnChangeRoleAsync` event allows you tooperform work depending on replica role as well as in response toorole change.</span></span>

<span data-ttu-id="39ab2-138">可設定狀態的服務並且提供其 hello 相同的四個週期事件為無狀態服務，與 hello 相同的語意，它使用案例：</span><span class="sxs-lookup"><span data-stu-id="39ab2-138">A stateful service also provides hello same four lifecycle events as a stateless service, with hello same semantics and use cases:</span></span>

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a><span data-ttu-id="39ab2-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39ab2-139">Next steps</span></span>
<span data-ttu-id="39ab2-140">更進階主題相關 tooService 網狀架構，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="39ab2-140">For more advanced topics related tooService Fabric, see hello following articles:</span></span>

* [<span data-ttu-id="39ab2-141">設定具狀態的 Reliable Services</span><span class="sxs-lookup"><span data-stu-id="39ab2-141">Configuring stateful Reliable Services</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="39ab2-142">Service Fabric 健康狀態簡介</span><span class="sxs-lookup"><span data-stu-id="39ab2-142">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="39ab2-143">使用系統健康狀態報告進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="39ab2-143">Using system health reports for troubleshooting</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="39ab2-144">設定服務以 hello Service Fabric 叢集資源管理員</span><span class="sxs-lookup"><span data-stu-id="39ab2-144">Configuring Services with hello Service Fabric Cluster Resource Manager</span></span>](service-fabric-cluster-resource-manager-configure-services.md)
