---
title: "Testability：服務通訊 | Microsoft Docs"
description: "服務之間的通訊是整合 Service Fabric 應用程式的重要環節。 本文討論設計考量及測試技巧。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a><span data-ttu-id="98b7b-104">Service Fabric Testability 案例：服務通訊</span><span class="sxs-lookup"><span data-stu-id="98b7b-104">Service Fabric testability scenarios: Service communication</span></span>
<span data-ttu-id="98b7b-105">微服務及服務導向的架構樣式會在 Azure Service Fabric 中自然出現。</span><span class="sxs-lookup"><span data-stu-id="98b7b-105">Microservices and service-oriented architectural styles surface naturally in Azure Service Fabric.</span></span> <span data-ttu-id="98b7b-106">在這些類型的分散式架構中，通常被組成需要 tootalk tooeach 其他的多個服務的元件化的微服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="98b7b-106">In these types of distributed architectures, componentized microservice applications are typically composed of multiple services that need tootalk tooeach other.</span></span> <span data-ttu-id="98b7b-107">在即使 hello 最簡單的情況下，您通常具有最少的無狀態 web 服務和需要 toocommunicate 可設定狀態的資料儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="98b7b-107">In even hello simplest cases, you generally have at least a stateless web service and a stateful data storage service that need toocommunicate.</span></span>

<span data-ttu-id="98b7b-108">服務對服務通訊是應用程式中，重要的整合點，因為每個服務會公開一種遠端 API tooother 服務。</span><span class="sxs-lookup"><span data-stu-id="98b7b-108">Service-to-service communication is a critical integration point of an application, because each service exposes a remote API tooother services.</span></span> <span data-ttu-id="98b7b-109">與 I/O 相關的一組 API 界限通常需要謹慎處理，且需經過大量測試和驗證。</span><span class="sxs-lookup"><span data-stu-id="98b7b-109">Working with a set of API boundaries that involves I/O generally requires some care, with a good amount of testing and validation.</span></span>

<span data-ttu-id="98b7b-110">這些服務界限在分散式系統連接在一起時，有許多考量 toomake:</span><span class="sxs-lookup"><span data-stu-id="98b7b-110">There are numerous considerations toomake when these service boundaries are wired together in a distributed system:</span></span>

* <span data-ttu-id="98b7b-111">傳輸通訊協定。</span><span class="sxs-lookup"><span data-stu-id="98b7b-111">*Transport protocol*.</span></span> <span data-ttu-id="98b7b-112">您要使用 HTTP 以提供更優異的互通性，還是自訂的二進位通訊協定，以應付最大的輸送量？</span><span class="sxs-lookup"><span data-stu-id="98b7b-112">Will you use HTTP for increased interoperability, or a custom binary protocol for maximum throughput?</span></span>
* <span data-ttu-id="98b7b-113">錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="98b7b-113">*Error handling*.</span></span> <span data-ttu-id="98b7b-114">如何處理永久性和暫時性錯誤？</span><span class="sxs-lookup"><span data-stu-id="98b7b-114">How will permanent and transient errors be handled?</span></span> <span data-ttu-id="98b7b-115">當服務移 tooa 另一個節點時，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="98b7b-115">What will happen when a service moves tooa different node?</span></span>
* <span data-ttu-id="98b7b-116">逾時與延遲。</span><span class="sxs-lookup"><span data-stu-id="98b7b-116">*Timeouts and latency*.</span></span> <span data-ttu-id="98b7b-117">在多層式應用程式如何將每個服務層處理 hello 堆疊和 toohello 使用者透過延遲？</span><span class="sxs-lookup"><span data-stu-id="98b7b-117">In multitiered applications, how will each service layer handle latency through hello stack and toohello user?</span></span>

<span data-ttu-id="98b7b-118">無論您使用其中一個 hello Service Fabric 所提供的內建的服務通訊元件，或是您建立您自己，測試您的服務之間的 hello 互動是您的應用程式中的重大 tooensuring 恢復功能。</span><span class="sxs-lookup"><span data-stu-id="98b7b-118">Whether you use one of hello built-in service communication components provided by Service Fabric or you build your own, testing hello interactions between your services is critical tooensuring resiliency in your application.</span></span>

## <a name="prepare-for-services-toomove"></a><span data-ttu-id="98b7b-119">準備服務 toomove</span><span class="sxs-lookup"><span data-stu-id="98b7b-119">Prepare for services toomove</span></span>
<span data-ttu-id="98b7b-120">服務執行個體經過一段時間後可能會移動。</span><span class="sxs-lookup"><span data-stu-id="98b7b-120">Service instances may move around over time.</span></span> <span data-ttu-id="98b7b-121">尤其在它們設有負載度量，以自訂最佳資源平衡時更是如此。</span><span class="sxs-lookup"><span data-stu-id="98b7b-121">This is especially true when they are configured with load metrics for custom-tailored optimal resource balancing.</span></span> <span data-ttu-id="98b7b-122">Service Fabric 移動期間升級、 容錯移轉、 向外延展和其他透過分散式系統的 hello 存留期間發生的情況下，即使您的服務執行個體 toomaximize 其可用性。</span><span class="sxs-lookup"><span data-stu-id="98b7b-122">Service Fabric moves your service instances toomaximize their availability even during upgrades, failovers, scale-out, and other situations that occur over hello lifetime of a distributed system.</span></span>

<span data-ttu-id="98b7b-123">服務移動 hello 叢集中，您的用戶端和其他服務時，應該已備妥的 toohandle 兩個案例進行討論 tooa 服務：</span><span class="sxs-lookup"><span data-stu-id="98b7b-123">As services move around in hello cluster, your clients and other services should be prepared toohandle two scenarios when they talk tooa service:</span></span>

* <span data-ttu-id="98b7b-124">hello 服務執行個體或資料分割複本已經因為 hello 討論 tooit 的最後一次。</span><span class="sxs-lookup"><span data-stu-id="98b7b-124">hello service instance or partition replica has moved since hello last time you talked tooit.</span></span> <span data-ttu-id="98b7b-125">這是服務生命週期的一部分，且應預期的 toohappen hello 應用程式的存留期間。</span><span class="sxs-lookup"><span data-stu-id="98b7b-125">This is a normal part of a service lifecycle, and it should be expected toohappen during hello lifetime of your application.</span></span>
* <span data-ttu-id="98b7b-126">hello 服務執行個體或資料分割複本處於移動的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="98b7b-126">hello service instance or partition replica is in hello process of moving.</span></span> <span data-ttu-id="98b7b-127">服務網狀架構中發生非常快速地從一個節點 tooanother 服務的容錯移轉，雖然可能會延遲可用性緩慢 toostart hello 通訊元件，您的服務時。</span><span class="sxs-lookup"><span data-stu-id="98b7b-127">Although failover of a service from one node tooanother occurs very quickly in Service Fabric, there may be a delay in availability if hello communication component of your service is slow toostart.</span></span>

<span data-ttu-id="98b7b-128">妥善處理這些案例，對於系統流暢運作至關重要。</span><span class="sxs-lookup"><span data-stu-id="98b7b-128">Handling these scenarios gracefully is important for a smooth-running system.</span></span> <span data-ttu-id="98b7b-129">toodo 因此，請記住，：</span><span class="sxs-lookup"><span data-stu-id="98b7b-129">toodo so, keep in mind that:</span></span>

* <span data-ttu-id="98b7b-130">每項服務可以連線的 toohas*位址*，它會接聽程式 （例如，HTTP 或 Websocket）。</span><span class="sxs-lookup"><span data-stu-id="98b7b-130">Every service that can be connected toohas an *address* that it listens on (for example, HTTP or WebSockets).</span></span> <span data-ttu-id="98b7b-131">當服務執行個體或分割移動時，其位址端點會變更。</span><span class="sxs-lookup"><span data-stu-id="98b7b-131">When a service instance or partition moves, its address endpoint changes.</span></span> <span data-ttu-id="98b7b-132">（它會移動 tooa 不同的節點，請使用不同的 IP 位址。）如果您使用 hello 的內建通訊的元件，將為您處理重新解決服務位址。</span><span class="sxs-lookup"><span data-stu-id="98b7b-132">(It moves tooa different node with a different IP address.) If you're using hello built-in communication components, they will handle re-resolving service addresses for you.</span></span>
* <span data-ttu-id="98b7b-133">可能有其接聽程式 hello 服務執行個體啟動為服務延遲暫時增加一次。</span><span class="sxs-lookup"><span data-stu-id="98b7b-133">There may be a temporary increase in service latency as hello service instance starts up its listener again.</span></span> <span data-ttu-id="98b7b-134">這取決於 hello 服務執行個體已經移動後 hello 服務開啟 hello 接聽程式的速度。</span><span class="sxs-lookup"><span data-stu-id="98b7b-134">This depends on how quickly hello service opens hello listener after hello service instance is moved.</span></span>
* <span data-ttu-id="98b7b-135">任何現有的連線需要 toobe 關閉並重新開啟 hello 服務開啟新的節點之後。</span><span class="sxs-lookup"><span data-stu-id="98b7b-135">Any existing connections need toobe closed and reopened after hello service opens on a new node.</span></span> <span data-ttu-id="98b7b-136">依正常程序中的節點關機或重新啟動允許正常關閉現有連接 toobe 的時間。</span><span class="sxs-lookup"><span data-stu-id="98b7b-136">A graceful node shutdown or restart allows time for existing connections toobe shut down gracefully.</span></span>

### <a name="test-it-move-service-instances"></a><span data-ttu-id="98b7b-137">測試：移動服務執行個體</span><span class="sxs-lookup"><span data-stu-id="98b7b-137">Test it: Move service instances</span></span>
<span data-ttu-id="98b7b-138">使用 Service Fabric 可測試性工具，您可以撰寫測試案例 tootest 這些情況下以不同的方式：</span><span class="sxs-lookup"><span data-stu-id="98b7b-138">By using Service Fabric's testability tools, you can author a test scenario tootest these situations in different ways:</span></span>

1. <span data-ttu-id="98b7b-139">移動具狀態服務的主要複本。</span><span class="sxs-lookup"><span data-stu-id="98b7b-139">Move a stateful service's primary replica.</span></span>
   
    <span data-ttu-id="98b7b-140">hello 可設定狀態的服務資料分割的主要複本可以移動的原因有許多。</span><span class="sxs-lookup"><span data-stu-id="98b7b-140">hello primary replica of a stateful service partition can be moved for any number of reasons.</span></span> <span data-ttu-id="98b7b-141">使用您的服務 react toohello 如何在受控制的方式移動特定資料分割 toosee 此 tootarget hello 主要複本。</span><span class="sxs-lookup"><span data-stu-id="98b7b-141">Use this tootarget hello primary replica of a specific partition toosee how your services react toohello move in a very controlled manner.</span></span>
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. <span data-ttu-id="98b7b-142">停止節點。</span><span class="sxs-lookup"><span data-stu-id="98b7b-142">Stop a node.</span></span>
   
    <span data-ttu-id="98b7b-143">在停止節點時，Service Fabric 移 hello 的所有服務執行個體或資料分割上的該節點 tooone hello hello 叢集中的其他可用節點。</span><span class="sxs-lookup"><span data-stu-id="98b7b-143">When a node is stopped, Service Fabric moves all of hello service instances or partitions that were on that node tooone of hello other available nodes in hello cluster.</span></span> <span data-ttu-id="98b7b-144">使用此 tootest 節點是從您的叢集遺失，和所有 hello 服務執行個體和該節點上的複本有 toomove 的情況。</span><span class="sxs-lookup"><span data-stu-id="98b7b-144">Use this tootest a situation where a node is lost from your cluster and all of hello service instances and replicas on that node have toomove.</span></span>
   
    <span data-ttu-id="98b7b-145">您可以藉由使用 hello PowerShell 停止節點**停止 ServiceFabricNode** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="98b7b-145">You can stop a node by using hello PowerShell **Stop-ServiceFabricNode** cmdlet:</span></span>
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a><span data-ttu-id="98b7b-146">維護服務可用性</span><span class="sxs-lookup"><span data-stu-id="98b7b-146">Maintain service availability</span></span>
<span data-ttu-id="98b7b-147">做為平台，Service Fabric 這項設計的 tooprovide 高可用性，您的服務。</span><span class="sxs-lookup"><span data-stu-id="98b7b-147">As a platform, Service Fabric is designed tooprovide high availability of your services.</span></span> <span data-ttu-id="98b7b-148">但是在極端情況下，基礎結構的基礎問題仍可能導致無法使用服務。</span><span class="sxs-lookup"><span data-stu-id="98b7b-148">But in extreme cases, underlying infrastructure problems can still cause unavailability.</span></span> <span data-ttu-id="98b7b-149">太重要 tootest 針對這些案例。</span><span class="sxs-lookup"><span data-stu-id="98b7b-149">It is important tootest for these scenarios, too.</span></span>

<span data-ttu-id="98b7b-150">可設定狀態的服務會使用以仲裁為基礎的系統 tooreplicate 狀態的高可用性。</span><span class="sxs-lookup"><span data-stu-id="98b7b-150">Stateful services use a quorum-based system tooreplicate state for high availability.</span></span> <span data-ttu-id="98b7b-151">這表示複本的仲裁必須 toobe 可用 tooperform 寫入作業。</span><span class="sxs-lookup"><span data-stu-id="98b7b-151">This means that a quorum of replicas needs toobe available tooperform write operations.</span></span> <span data-ttu-id="98b7b-152">在極罕見情況下，例如大規模的硬體故障，有可能無法使用複本仲裁。</span><span class="sxs-lookup"><span data-stu-id="98b7b-152">In rare cases, such as a widespread hardware failure, a quorum of replicas may not be available.</span></span> <span data-ttu-id="98b7b-153">在這些情況下，您將不會無法 tooperform 寫入作業，但是您仍然可以無法 tooperform 讀取的作業。</span><span class="sxs-lookup"><span data-stu-id="98b7b-153">In these cases, you will not be able tooperform write operations, but you will still be able tooperform read operations.</span></span>

### <a name="test-it-write-operation-unavailability"></a><span data-ttu-id="98b7b-154">測試：撰寫作業無法使用</span><span class="sxs-lookup"><span data-stu-id="98b7b-154">Test it: Write operation unavailability</span></span>
<span data-ttu-id="98b7b-155">使用 Service Fabric 中 hello 可測試性工具，您可以將插入其仲裁遺失，做為測試會引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="98b7b-155">By using hello testability tools in Service Fabric, you can inject a fault that induces quorum loss as a test.</span></span> <span data-ttu-id="98b7b-156">雖然這類案例中很少發生，請務必用戶端和服務可設定狀態服務所依賴的準備，它們無法做出寫入要求 tooit toohandle 情況。</span><span class="sxs-lookup"><span data-stu-id="98b7b-156">Although such a scenario is rare, it is important that clients and services that depend on a stateful service are prepared toohandle situations where they cannot make write requests tooit.</span></span> <span data-ttu-id="98b7b-157">也很重要，hello 可設定狀態服務本身是留意這個可能性，可以依正常程序進行通訊它 toocallers。</span><span class="sxs-lookup"><span data-stu-id="98b7b-157">It is also important that hello stateful service itself is aware of this possibility and can gracefully communicate it toocallers.</span></span>

<span data-ttu-id="98b7b-158">您可以使用 hello PowerShell 誘使仲裁遺失**Invoke ServiceFabricPartitionQuorumLoss** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="98b7b-158">You can induce quorum loss by using hello PowerShell **Invoke-ServiceFabricPartitionQuorumLoss** cmdlet:</span></span>

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

<span data-ttu-id="98b7b-159">在此範例中，我們設定`QuorumLossMode`太`QuorumReplicas`tooindicate 我們想 tooinduce 仲裁遺失而不需讓下所有複本。</span><span class="sxs-lookup"><span data-stu-id="98b7b-159">In this example, we set `QuorumLossMode` too`QuorumReplicas` tooindicate that we want tooinduce quorum loss without taking down all replicas.</span></span> <span data-ttu-id="98b7b-160">如此才能正常執行讀取作業。</span><span class="sxs-lookup"><span data-stu-id="98b7b-160">This way, read operations are still possible.</span></span> <span data-ttu-id="98b7b-161">tootest 案例，其中整個磁碟分割是無法使用，您可以設定此參數太`AllReplicas`。</span><span class="sxs-lookup"><span data-stu-id="98b7b-161">tootest a scenario where an entire partition is unavailable, you can set this switch too`AllReplicas`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98b7b-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98b7b-162">Next steps</span></span>
[<span data-ttu-id="98b7b-163">深入了解 Testability 動作</span><span class="sxs-lookup"><span data-stu-id="98b7b-163">Learn more about testability actions</span></span>](service-fabric-testability-actions.md)

[<span data-ttu-id="98b7b-164">深入了解 Testability 案例</span><span class="sxs-lookup"><span data-stu-id="98b7b-164">Learn more about testability scenarios</span></span>](service-fabric-testability-scenarios.md)

