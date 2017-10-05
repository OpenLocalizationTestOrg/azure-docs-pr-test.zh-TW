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
ms.openlocfilehash: c182cc2062ada40029504de5b2b64b021c614ce6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a><span data-ttu-id="e4c84-104">Service Fabric Testability 案例：服務通訊</span><span class="sxs-lookup"><span data-stu-id="e4c84-104">Service Fabric testability scenarios: Service communication</span></span>
<span data-ttu-id="e4c84-105">微服務及服務導向的架構樣式會在 Azure Service Fabric 中自然出現。</span><span class="sxs-lookup"><span data-stu-id="e4c84-105">Microservices and service-oriented architectural styles surface naturally in Azure Service Fabric.</span></span> <span data-ttu-id="e4c84-106">在這些類型的分散式架構中，元件化的微服務應用程式通常是由需要彼此通訊的多個服務所組成。</span><span class="sxs-lookup"><span data-stu-id="e4c84-106">In these types of distributed architectures, componentized microservice applications are typically composed of multiple services that need to talk to each other.</span></span> <span data-ttu-id="e4c84-107">即使在最簡單的情況下，您通常至少會有一個無狀態網路服務及一個可設定狀態的資料儲存服務需要相互通訊。</span><span class="sxs-lookup"><span data-stu-id="e4c84-107">In even the simplest cases, you generally have at least a stateless web service and a stateful data storage service that need to communicate.</span></span>

<span data-ttu-id="e4c84-108">服務之間的通訊是整合應用程式的重要環節，因為各服務會向其他服務公開遠端 API。</span><span class="sxs-lookup"><span data-stu-id="e4c84-108">Service-to-service communication is a critical integration point of an application, because each service exposes a remote API to other services.</span></span> <span data-ttu-id="e4c84-109">與 I/O 相關的一組 API 界限通常需要謹慎處理，且需經過大量測試和驗證。</span><span class="sxs-lookup"><span data-stu-id="e4c84-109">Working with a set of API boundaries that involves I/O generally requires some care, with a good amount of testing and validation.</span></span>

<span data-ttu-id="e4c84-110">若要在分散式系統中，將這些服務界限連接起來，有許多方面都需要謹慎考量：</span><span class="sxs-lookup"><span data-stu-id="e4c84-110">There are numerous considerations to make when these service boundaries are wired together in a distributed system:</span></span>

* <span data-ttu-id="e4c84-111">傳輸通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e4c84-111">*Transport protocol*.</span></span> <span data-ttu-id="e4c84-112">您要使用 HTTP 以提供更優異的互通性，還是自訂的二進位通訊協定，以應付最大的輸送量？</span><span class="sxs-lookup"><span data-stu-id="e4c84-112">Will you use HTTP for increased interoperability, or a custom binary protocol for maximum throughput?</span></span>
* <span data-ttu-id="e4c84-113">錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="e4c84-113">*Error handling*.</span></span> <span data-ttu-id="e4c84-114">如何處理永久性和暫時性錯誤？</span><span class="sxs-lookup"><span data-stu-id="e4c84-114">How will permanent and transient errors be handled?</span></span> <span data-ttu-id="e4c84-115">當服務移至另一個節點時，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="e4c84-115">What will happen when a service moves to a different node?</span></span>
* <span data-ttu-id="e4c84-116">逾時與延遲。</span><span class="sxs-lookup"><span data-stu-id="e4c84-116">*Timeouts and latency*.</span></span> <span data-ttu-id="e4c84-117">在多層式應用程式中，各服務層將如何透過堆疊處理延遲，為使用者順暢提供服務？</span><span class="sxs-lookup"><span data-stu-id="e4c84-117">In multitiered applications, how will each service layer handle latency through the stack and to the user?</span></span>

<span data-ttu-id="e4c84-118">不論您使用 Service Fabric 提供的其中一種內建服務通訊元件，或者您選擇自行建立，測試服務之間的互動永遠是確保應用程式復原能力的重要部分。</span><span class="sxs-lookup"><span data-stu-id="e4c84-118">Whether you use one of the built-in service communication components provided by Service Fabric or you build your own, testing the interactions between your services is critical to ensuring resiliency in your application.</span></span>

## <a name="prepare-for-services-to-move"></a><span data-ttu-id="e4c84-119">準備讓服務移動</span><span class="sxs-lookup"><span data-stu-id="e4c84-119">Prepare for services to move</span></span>
<span data-ttu-id="e4c84-120">服務執行個體經過一段時間後可能會移動。</span><span class="sxs-lookup"><span data-stu-id="e4c84-120">Service instances may move around over time.</span></span> <span data-ttu-id="e4c84-121">尤其在它們設有負載度量，以自訂最佳資源平衡時更是如此。</span><span class="sxs-lookup"><span data-stu-id="e4c84-121">This is especially true when they are configured with load metrics for custom-tailored optimal resource balancing.</span></span> <span data-ttu-id="e4c84-122">即使在升級、容錯移轉、向外延展及其他分散式系統存留時間內發生的各種情況期間，Service Fabric 都可以移動您的服務執行個體以最大化其可用性。</span><span class="sxs-lookup"><span data-stu-id="e4c84-122">Service Fabric moves your service instances to maximize their availability even during upgrades, failovers, scale-out, and other situations that occur over the lifetime of a distributed system.</span></span>

<span data-ttu-id="e4c84-123">由於服務會在叢集中移動，您的用戶端和其他服務應在與服務通訊時準備就緒，以因應兩種案例：</span><span class="sxs-lookup"><span data-stu-id="e4c84-123">As services move around in the cluster, your clients and other services should be prepared to handle two scenarios when they talk to a service:</span></span>

* <span data-ttu-id="e4c84-124">在您最後一次與服務執行個體或分割區複本通訊後，其中一項即已移動過。</span><span class="sxs-lookup"><span data-stu-id="e4c84-124">The service instance or partition replica has moved since the last time you talked to it.</span></span> <span data-ttu-id="e4c84-125">正常情況下，這是服務生命週期的一部分，而且應該會在應用程式的存留期間發生。</span><span class="sxs-lookup"><span data-stu-id="e4c84-125">This is a normal part of a service lifecycle, and it should be expected to happen during the lifetime of your application.</span></span>
* <span data-ttu-id="e4c84-126">服務執行個體或分割區複本正在移動。</span><span class="sxs-lookup"><span data-stu-id="e4c84-126">The service instance or partition replica is in the process of moving.</span></span> <span data-ttu-id="e4c84-127">在 Service Fabric 中，雖然服務在節點間容錯移轉的速度相當快速，但若服務通訊元件太慢而無法啟動，可能會對可用性造成延遲。</span><span class="sxs-lookup"><span data-stu-id="e4c84-127">Although failover of a service from one node to another occurs very quickly in Service Fabric, there may be a delay in availability if the communication component of your service is slow to start.</span></span>

<span data-ttu-id="e4c84-128">妥善處理這些案例，對於系統流暢運作至關重要。</span><span class="sxs-lookup"><span data-stu-id="e4c84-128">Handling these scenarios gracefully is important for a smooth-running system.</span></span> <span data-ttu-id="e4c84-129">若要這樣做，請注意下列事項：</span><span class="sxs-lookup"><span data-stu-id="e4c84-129">To do so, keep in mind that:</span></span>

* <span data-ttu-id="e4c84-130">可連接的各項服務都有「位址」  可接聽 (例如 HTTP 或 WebSockets)。</span><span class="sxs-lookup"><span data-stu-id="e4c84-130">Every service that can be connected to has an *address* that it listens on (for example, HTTP or WebSockets).</span></span> <span data-ttu-id="e4c84-131">當服務執行個體或分割移動時，其位址端點會變更。</span><span class="sxs-lookup"><span data-stu-id="e4c84-131">When a service instance or partition moves, its address endpoint changes.</span></span> <span data-ttu-id="e4c84-132">(它會移至具有不同 IP 位址的不同節點。)如果使用內建的通訊元件，這些元件會為您處理重新解析服務位址。</span><span class="sxs-lookup"><span data-stu-id="e4c84-132">(It moves to a different node with a different IP address.) If you're using the built-in communication components, they will handle re-resolving service addresses for you.</span></span>
* <span data-ttu-id="e4c84-133">當服務執行個體再次開啟接聽程式時，服務延遲時間可能會短暫增加。</span><span class="sxs-lookup"><span data-stu-id="e4c84-133">There may be a temporary increase in service latency as the service instance starts up its listener again.</span></span> <span data-ttu-id="e4c84-134">這需取決於服務在服務執行個體移動後開啟接聽程式的速度。</span><span class="sxs-lookup"><span data-stu-id="e4c84-134">This depends on how quickly the service opens the listener after the service instance is moved.</span></span>
* <span data-ttu-id="e4c84-135">必須先關閉任何現有的連線，然後等服務於新的節點上開啟之後再重新開啟。</span><span class="sxs-lookup"><span data-stu-id="e4c84-135">Any existing connections need to be closed and reopened after the service opens on a new node.</span></span> <span data-ttu-id="e4c84-136">妥善關閉節點或重新開啟，可讓現有連線擁有足夠時間正常關閉。</span><span class="sxs-lookup"><span data-stu-id="e4c84-136">A graceful node shutdown or restart allows time for existing connections to be shut down gracefully.</span></span>

### <a name="test-it-move-service-instances"></a><span data-ttu-id="e4c84-137">測試：移動服務執行個體</span><span class="sxs-lookup"><span data-stu-id="e4c84-137">Test it: Move service instances</span></span>
<span data-ttu-id="e4c84-138">藉由使用 Service Fabric 的 Testability 工具，您可以撰寫測試案例，以不同方式測試這些情況：</span><span class="sxs-lookup"><span data-stu-id="e4c84-138">By using Service Fabric's testability tools, you can author a test scenario to test these situations in different ways:</span></span>

1. <span data-ttu-id="e4c84-139">移動具狀態服務的主要複本。</span><span class="sxs-lookup"><span data-stu-id="e4c84-139">Move a stateful service's primary replica.</span></span>
   
    <span data-ttu-id="e4c84-140">具狀態服務分割區的主要複本會因為諸多原因而移動。</span><span class="sxs-lookup"><span data-stu-id="e4c84-140">The primary replica of a stateful service partition can be moved for any number of reasons.</span></span> <span data-ttu-id="e4c84-141">以此鎖定特定分割區的主要複本，以便透過高度受控制的方式，查看服務回應移動的情形。</span><span class="sxs-lookup"><span data-stu-id="e4c84-141">Use this to target the primary replica of a specific partition to see how your services react to the move in a very controlled manner.</span></span>
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. <span data-ttu-id="e4c84-142">停止節點。</span><span class="sxs-lookup"><span data-stu-id="e4c84-142">Stop a node.</span></span>
   
    <span data-ttu-id="e4c84-143">節點停止後，Service Fabric 會將該節點上所有服務執行個體或分割區，移動至叢集中其他可用的其中一個節點。</span><span class="sxs-lookup"><span data-stu-id="e4c84-143">When a node is stopped, Service Fabric moves all of the service instances or partitions that were on that node to one of the other available nodes in the cluster.</span></span> <span data-ttu-id="e4c84-144">以此測試節點從叢集中遺失，且該節點上的所有服務執行個體及複本都必須移動的情況。</span><span class="sxs-lookup"><span data-stu-id="e4c84-144">Use this to test a situation where a node is lost from your cluster and all of the service instances and replicas on that node have to move.</span></span>
   
    <span data-ttu-id="e4c84-145">您可以使用 PowerShell **Stop-ServiceFabricNode** Cmdlet 來停止節點：</span><span class="sxs-lookup"><span data-stu-id="e4c84-145">You can stop a node by using the PowerShell **Stop-ServiceFabricNode** cmdlet:</span></span>
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a><span data-ttu-id="e4c84-146">維護服務可用性</span><span class="sxs-lookup"><span data-stu-id="e4c84-146">Maintain service availability</span></span>
<span data-ttu-id="e4c84-147">做為平台，Service Fabric 專為服務提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="e4c84-147">As a platform, Service Fabric is designed to provide high availability of your services.</span></span> <span data-ttu-id="e4c84-148">但是在極端情況下，基礎結構的基礎問題仍可能導致無法使用服務。</span><span class="sxs-lookup"><span data-stu-id="e4c84-148">But in extreme cases, underlying infrastructure problems can still cause unavailability.</span></span> <span data-ttu-id="e4c84-149">請務必也測試這些情況。</span><span class="sxs-lookup"><span data-stu-id="e4c84-149">It is important to test for these scenarios, too.</span></span>

<span data-ttu-id="e4c84-150">具狀態服務會使用仲裁式系統來複寫狀態，藉以達到高可用性。</span><span class="sxs-lookup"><span data-stu-id="e4c84-150">Stateful services use a quorum-based system to replicate state for high availability.</span></span> <span data-ttu-id="e4c84-151">換句話說，必須要能使用複本仲裁，才能執行寫入作業。</span><span class="sxs-lookup"><span data-stu-id="e4c84-151">This means that a quorum of replicas needs to be available to perform write operations.</span></span> <span data-ttu-id="e4c84-152">在極罕見情況下，例如大規模的硬體故障，有可能無法使用複本仲裁。</span><span class="sxs-lookup"><span data-stu-id="e4c84-152">In rare cases, such as a widespread hardware failure, a quorum of replicas may not be available.</span></span> <span data-ttu-id="e4c84-153">在這些情況下，您將無法執行寫入作業，但仍能執行讀取作業。</span><span class="sxs-lookup"><span data-stu-id="e4c84-153">In these cases, you will not be able to perform write operations, but you will still be able to perform read operations.</span></span>

### <a name="test-it-write-operation-unavailability"></a><span data-ttu-id="e4c84-154">測試：撰寫作業無法使用</span><span class="sxs-lookup"><span data-stu-id="e4c84-154">Test it: Write operation unavailability</span></span>
<span data-ttu-id="e4c84-155">藉由使用 Service Fabric 中的 testability 工具，您可以插入引發仲裁遺失的錯誤做為測試。</span><span class="sxs-lookup"><span data-stu-id="e4c84-155">By using the testability tools in Service Fabric, you can inject a fault that induces quorum loss as a test.</span></span> <span data-ttu-id="e4c84-156">雖然這樣的案例極為罕見，但仰賴具狀態狀態服務的用戶端和服務務必做好準備，以處理無法要求執行寫入作業的各種情況。</span><span class="sxs-lookup"><span data-stu-id="e4c84-156">Although such a scenario is rare, it is important that clients and services that depend on a stateful service are prepared to handle situations where they cannot make write requests to it.</span></span> <span data-ttu-id="e4c84-157">具狀態服務本身也應了解發生這種情況的可能性，並能依正常程序與呼叫者通訊。</span><span class="sxs-lookup"><span data-stu-id="e4c84-157">It is also important that the stateful service itself is aware of this possibility and can gracefully communicate it to callers.</span></span>

<span data-ttu-id="e4c84-158">您可以藉由使用 **Invoke-ServiceFabricPartitionQuorumLoss PowerShell** Cmdlet 引發仲裁遺失：</span><span class="sxs-lookup"><span data-stu-id="e4c84-158">You can induce quorum loss by using the PowerShell **Invoke-ServiceFabricPartitionQuorumLoss** cmdlet:</span></span>

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

<span data-ttu-id="e4c84-159">在此範例中，我們將 `QuorumLossMode` 設為 `QuorumReplicas`，以便在引發仲裁遺失時，不會關閉所有複本。</span><span class="sxs-lookup"><span data-stu-id="e4c84-159">In this example, we set `QuorumLossMode` to `QuorumReplicas` to indicate that we want to induce quorum loss without taking down all replicas.</span></span> <span data-ttu-id="e4c84-160">如此才能正常執行讀取作業。</span><span class="sxs-lookup"><span data-stu-id="e4c84-160">This way, read operations are still possible.</span></span> <span data-ttu-id="e4c84-161">若要測試整個分割區都無法使用的案例，您可將此參數設定為 `AllReplicas`。</span><span class="sxs-lookup"><span data-stu-id="e4c84-161">To test a scenario where an entire partition is unavailable, you can set this switch to `AllReplicas`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4c84-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4c84-162">Next steps</span></span>
[<span data-ttu-id="e4c84-163">深入了解 Testability 動作</span><span class="sxs-lookup"><span data-stu-id="e4c84-163">Learn more about testability actions</span></span>](service-fabric-testability-actions.md)

[<span data-ttu-id="e4c84-164">深入了解 Testability 案例</span><span class="sxs-lookup"><span data-stu-id="e4c84-164">Learn more about testability scenarios</span></span>](service-fabric-testability-scenarios.md)

