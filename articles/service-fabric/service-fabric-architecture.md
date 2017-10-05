---
title: "Azure Service Fabric 的架構 | Microsoft Docs"
description: "Service Fabric 是一種分散式系統平台，用來建置可調整、可靠且輕鬆管理的雲端應用程式。 本文章說明 Service Fabric 的架構。"
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 3cf019bf9a08574c984e92985452df438f3eeb77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-architecture"></a><span data-ttu-id="3d867-104">Service Fabric 架構</span><span class="sxs-lookup"><span data-stu-id="3d867-104">Service Fabric architecture</span></span>
<span data-ttu-id="3d867-105">Service Fabric 是使用分層的子系統所建置。</span><span class="sxs-lookup"><span data-stu-id="3d867-105">Service Fabric is built with layered subsystems.</span></span> <span data-ttu-id="3d867-106">這些子系統可讓您撰寫的應用程式為：</span><span class="sxs-lookup"><span data-stu-id="3d867-106">These subsystems enable you to write applications that are:</span></span>

* <span data-ttu-id="3d867-107">高可用性</span><span class="sxs-lookup"><span data-stu-id="3d867-107">Highly available</span></span>
* <span data-ttu-id="3d867-108">可調整</span><span class="sxs-lookup"><span data-stu-id="3d867-108">Scalable</span></span>
* <span data-ttu-id="3d867-109">可管理</span><span class="sxs-lookup"><span data-stu-id="3d867-109">Manageable</span></span>
* <span data-ttu-id="3d867-110">可測試</span><span class="sxs-lookup"><span data-stu-id="3d867-110">Testable</span></span>

<span data-ttu-id="3d867-111">下圖顯示 Service Fabric 的主要子系統。</span><span class="sxs-lookup"><span data-stu-id="3d867-111">The following diagram shows the major subsystems of Service Fabric.</span></span>

![Service Fabric 架構的圖表](media/service-fabric-architecture/service-fabric-architecture.png)

<span data-ttu-id="3d867-113">在分散式系統中，能夠叢集中的節點之間安全地進行通訊非常重要。</span><span class="sxs-lookup"><span data-stu-id="3d867-113">In a distributed system, the ability to securely communicate between nodes in a cluster is crucial.</span></span> <span data-ttu-id="3d867-114">堆疊的基底為傳輸子系統，可讓您安全地在節點之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="3d867-114">At the base of the stack is the transport subsystem, which provides secure communication between nodes.</span></span> <span data-ttu-id="3d867-115">傳輸子系統上方即為同盟子系統，會將不同的節點叢集成單一實體 (稱為叢集)，讓 Service Fabric 可以偵測失敗、執行前置選擇，以及提供一致的路由。</span><span class="sxs-lookup"><span data-stu-id="3d867-115">Above the transport subsystem lies the federation subsystem, which clusters the different nodes into a single entity (named clusters) so that Service Fabric can detect failures, perform leader election, and provide consistent routing.</span></span> <span data-ttu-id="3d867-116">可靠性子系統，即同盟子系統的最上層，負責透過如複寫、資源管理和容錯移轉等機制，提供 Service Fabric 服務的可靠性。</span><span class="sxs-lookup"><span data-stu-id="3d867-116">The reliability subsystem, layered on top of the federation subsystem, is responsible for the reliability of Service Fabric services through mechanisms such as replication, resource management, and failover.</span></span> <span data-ttu-id="3d867-117">同盟子系統也以主控和啟用子系統為基礎，用來管理單一節點上的應用程式生命週期。</span><span class="sxs-lookup"><span data-stu-id="3d867-117">The federation subsystem also underlies the hosting and activation subsystem, which manages the lifecycle of an application on a single node.</span></span> <span data-ttu-id="3d867-118">管理子系統會管理應用程式和服務的生命週期。</span><span class="sxs-lookup"><span data-stu-id="3d867-118">The management subsystem manages the lifecycle of applications and services.</span></span> <span data-ttu-id="3d867-119">可測試性子系統可協助應用程式開發人員在將應用程式和服務部署至生產環境的前後，透過模擬錯誤測試其服務。</span><span class="sxs-lookup"><span data-stu-id="3d867-119">The testability subsystem helps application developers test their services through simulated faults before and after deploying applications and services to production environments.</span></span> <span data-ttu-id="3d867-120">Service Fabric 可以透過其通訊子系統解析服務位置。</span><span class="sxs-lookup"><span data-stu-id="3d867-120">Service Fabric provides the ability to resolve service locations through its communication subsystem.</span></span> <span data-ttu-id="3d867-121">公開給開發人員的應用程式設計模型與啟用工具的應用程式模型位於這些子系統的最上層。</span><span class="sxs-lookup"><span data-stu-id="3d867-121">The application programming models exposed to developers are layered on top of these subsystems along with the application model to enable tooling.</span></span>

## <a name="transport-subsystem"></a><span data-ttu-id="3d867-122">傳輸子系統</span><span class="sxs-lookup"><span data-stu-id="3d867-122">Transport subsystem</span></span>
<span data-ttu-id="3d867-123">傳輸子系統會實作點對點資料包通訊通道。</span><span class="sxs-lookup"><span data-stu-id="3d867-123">The transport subsystem implements a point-to-point datagram communication channel.</span></span> <span data-ttu-id="3d867-124">此通道用於 Service Fabric 叢集內，以及 Service Fabric 叢集與用戶端之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="3d867-124">This channel is used for communication within service fabric clusters and communication between the service fabric cluster and clients.</span></span> <span data-ttu-id="3d867-125">它支援單向和要求/回覆通訊模式，可在同盟層提供實作廣播和多點傳送的基礎。</span><span class="sxs-lookup"><span data-stu-id="3d867-125">It supports one-way and request-reply communication patterns, which provides the basis for implementing broadcast and multicast in the Federation layer.</span></span> <span data-ttu-id="3d867-126">傳輸子系統使用 X509 憑證或 Windows 安全性來確保通訊安全。</span><span class="sxs-lookup"><span data-stu-id="3d867-126">The transport subsystem secures communication by using X509 certificates or Windows security.</span></span> <span data-ttu-id="3d867-127">此子系統供 Service Fabric 內部使用，並非由應用程式設計的開發人員直接存取。</span><span class="sxs-lookup"><span data-stu-id="3d867-127">This subsystem is used internally by Service Fabric and is not directly accessible to developers for application programming.</span></span>

## <a name="federation-subsystem"></a><span data-ttu-id="3d867-128">同盟子系統</span><span class="sxs-lookup"><span data-stu-id="3d867-128">Federation subsystem</span></span>
<span data-ttu-id="3d867-129">為了理解分散式系統中的節點集，您需要系統的一致檢視。</span><span class="sxs-lookup"><span data-stu-id="3d867-129">In order to reason about a set of nodes in a distributed system, you need to have a consistent view of the system.</span></span> <span data-ttu-id="3d867-130">同盟子系統會使用傳輸子系統所提供的通訊基本功能，並將不同節點結合至單一的整合節點以便於理解。</span><span class="sxs-lookup"><span data-stu-id="3d867-130">The federation subsystem uses the communication primitives provided by the transport subsystem and stitches the various nodes into a single unified cluster that it can reason about.</span></span> <span data-ttu-id="3d867-131">其提供其他子系統所需的的分散式系統基本功能，包含失敗偵測、前置選擇，以及一致的路由。</span><span class="sxs-lookup"><span data-stu-id="3d867-131">It provides the distributed systems primitives needed by the other subsystems - failure detection, leader election, and consistent routing.</span></span> <span data-ttu-id="3d867-132">同盟子系統使用 128 位元的權杖空間建置於分散式雜湊資料表的頂端。</span><span class="sxs-lookup"><span data-stu-id="3d867-132">The federation subsystem is built on top of distributed hash tables with a 128-bit token space.</span></span> <span data-ttu-id="3d867-133">此子系統會在節點上建立環狀拓撲，而環中的每個節點皆會針對擁有權來配置權杖空間的子集。</span><span class="sxs-lookup"><span data-stu-id="3d867-133">The subsystem creates a ring topology over the nodes, with each node in the ring being allocated a subset of the token space for ownership.</span></span> <span data-ttu-id="3d867-134">為了進行失敗偵測，分層會使用根據活動訊號和仲裁的租用機制。</span><span class="sxs-lookup"><span data-stu-id="3d867-134">For failure detection, the layer uses a leasing mechanism based on heart beating and arbitration.</span></span> <span data-ttu-id="3d867-135">同盟子系統也會透過複雜的聯結和分離的通訊協定，確保在任何時間內僅存在單一權杖擁有者。</span><span class="sxs-lookup"><span data-stu-id="3d867-135">The federation subsystem also guarantees through intricate join and departure protocols that only a single owner of a token exists at any time.</span></span> <span data-ttu-id="3d867-136">如此可提供前置選擇和一致的路由保證。</span><span class="sxs-lookup"><span data-stu-id="3d867-136">This provides leader election and consistent routing guarantees.</span></span>

## <a name="reliability-subsystem"></a><span data-ttu-id="3d867-137">可靠性子系統</span><span class="sxs-lookup"><span data-stu-id="3d867-137">Reliability subsystem</span></span>
<span data-ttu-id="3d867-138">可靠性子系統提供一種機制，可透過使用「複寫器」、「容錯移轉管理員」以及「資源平衡器」，讓 Service Fabric 服務的狀態具有高可用性。</span><span class="sxs-lookup"><span data-stu-id="3d867-138">The reliability subsystem provides the mechanism to make the state of a Service Fabric service highly available through the use of the *Replicator*, *Failover Manager*, and *Resource Balancer*.</span></span>

* <span data-ttu-id="3d867-139">複寫器可確保主要服務複本中的狀態變更會自動複寫至次要複本，以便在服務複本集中維護主要和次要複本之間的一致性。</span><span class="sxs-lookup"><span data-stu-id="3d867-139">The Replicator ensures that state changes in the primary service replica will automatically be replicated to secondary replicas, maintaining consistency between the primary and secondary replicas in a service replica set.</span></span> <span data-ttu-id="3d867-140">複寫器負責在複本集中的複本之間進行仲裁管理。</span><span class="sxs-lookup"><span data-stu-id="3d867-140">The replicator is responsible for quorum management among the replicas in the replica set.</span></span> <span data-ttu-id="3d867-141">其會與容錯移轉單元互動，以取得要複寫的作業清單，且重新設定代理程式會提供複本集的組態。</span><span class="sxs-lookup"><span data-stu-id="3d867-141">It interacts with the failover unit to get the list of operations to replicate, and the reconfiguration agent provides it with the configuration of the replica set.</span></span> <span data-ttu-id="3d867-142">該組態指出需要複寫作業的複本。</span><span class="sxs-lookup"><span data-stu-id="3d867-142">That configuration indicates which replicas the operations need to be replicated.</span></span> <span data-ttu-id="3d867-143">Service Fabric 會提供稱為網狀架構複寫器的預設複寫器，可由程式撰寫模型 API 用來使服務狀態具有高可用性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="3d867-143">Service Fabric provides a default replicator called Fabric Replicator, which can be used by the programming model API to make the service state highly available and reliable.</span></span>
* <span data-ttu-id="3d867-144">容錯移轉管理員可確保當節點加入至叢集或從叢集移除節點時，負載會在可用的節點上自動重新分配。</span><span class="sxs-lookup"><span data-stu-id="3d867-144">The Failover Manager ensures that when nodes are added to or removed from the cluster, the load is automatically redistributed across the available nodes.</span></span> <span data-ttu-id="3d867-145">如果叢集中的節點失敗，叢集會自動重新設定服務複本以維護可用性。</span><span class="sxs-lookup"><span data-stu-id="3d867-145">If a node in the cluster fails, the cluster will automatically reconfigure the service replicas to maintain availability.</span></span>
* <span data-ttu-id="3d867-146">Resource Manager 會將服務複本置於叢集中的失敗網域，並確保所有的容錯移轉單元正常運作。</span><span class="sxs-lookup"><span data-stu-id="3d867-146">The Resource Manager places service replicas across failure domain in the cluster and ensures that all failover units are operational.</span></span> <span data-ttu-id="3d867-147">Resource Manager 也會在叢集節點的基礎共用集區上平衡服務資源，以便達到最佳的統一負載分佈。</span><span class="sxs-lookup"><span data-stu-id="3d867-147">The Resource Manager also balances service resources across the underlying shared pool of cluster nodes to achieve optimal uniform load distribution.</span></span>

## <a name="management-subsystem"></a><span data-ttu-id="3d867-148">管理子系統</span><span class="sxs-lookup"><span data-stu-id="3d867-148">Management subsystem</span></span>
<span data-ttu-id="3d867-149">管理子系統提供端對端服務和應用程式生命週期管理。</span><span class="sxs-lookup"><span data-stu-id="3d867-149">The management subsystem provides end-to-end service and application lifecycle management.</span></span> <span data-ttu-id="3d867-150">PowerShell Cmdlet 和系統管理 API 可讓您佈建、部署、修補、升級和解除佈建應用程式，而不減損可用性。</span><span class="sxs-lookup"><span data-stu-id="3d867-150">PowerShell cmdlets and administrative APIs enable you to provision, deploy, patch, upgrade, and de-provision applications without loss of availability.</span></span> <span data-ttu-id="3d867-151">管理子系統會透過下列服務來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="3d867-151">The management subsystem performs this through the following services.</span></span>

* <span data-ttu-id="3d867-152">**叢集管理員**：這是用來與容錯移轉管理員互動的主要服務，從可靠性到根據服務放置條件約束將應用程式放置在節點上。</span><span class="sxs-lookup"><span data-stu-id="3d867-152">**Cluster Manager**: This is the primary service that interacts with the Failover Manager from reliability to place the applications on the nodes based on the service placement constraints.</span></span> <span data-ttu-id="3d867-153">容錯移轉子系統中的 Resource Manager 可確保永遠遵循條件約束。</span><span class="sxs-lookup"><span data-stu-id="3d867-153">The Resource Manager in failover subsystem ensures that the constraints are never broken.</span></span> <span data-ttu-id="3d867-154">叢集管理員會在從佈建到解除佈建的範圍內，管理應用程式的生命週期。</span><span class="sxs-lookup"><span data-stu-id="3d867-154">The cluster manager manages the lifecycle of the applications from provision to de-provision.</span></span> <span data-ttu-id="3d867-155">它會與健康狀態管理員整合，以便從語意上的健康狀態觀點，確保在升級期間不會減損應用程式的可用性。</span><span class="sxs-lookup"><span data-stu-id="3d867-155">It integrates with the health manager to ensure that application availability is not lost from a semantic health perspective during upgrades.</span></span>
* <span data-ttu-id="3d867-156">**健康狀態管理員**：此服務會啟用應用程式、服務和叢集實體的健康狀態監視。</span><span class="sxs-lookup"><span data-stu-id="3d867-156">**Health Manager**: This service enables health monitoring of applications, services, and cluster entities.</span></span> <span data-ttu-id="3d867-157">叢集實體 (例如節點、服務分割和複本) 可以報告健康狀態資訊，然後彙總至集中式健康狀態資料存放區。</span><span class="sxs-lookup"><span data-stu-id="3d867-157">Cluster entities (such as nodes, service partitions, and replicas) can report health information, which is then aggregated into the centralized health store.</span></span> <span data-ttu-id="3d867-158">此健康狀態資訊可提供服務的整體時間點健康狀態快照和分散在叢集中多個節點的節點，可讓您採取任何需要的修正動作。</span><span class="sxs-lookup"><span data-stu-id="3d867-158">This health information provides an overall point-in-time health snapshot of the services and nodes distributed across multiple nodes in the cluster, enabling you to take any needed corrective actions.</span></span> <span data-ttu-id="3d867-159">健康狀態查詢 API 可讓您查詢向健康狀態子系統報告的健康狀態事件。</span><span class="sxs-lookup"><span data-stu-id="3d867-159">Health query APIs enable you to query the health events reported to the health subsystem.</span></span> <span data-ttu-id="3d867-160">健康狀態查詢 API 會傳回儲存在健康狀態資料存放區中的原始健康狀態資料，或針對特定叢集實體傳回經過彙總、解譯的健康狀態資料。</span><span class="sxs-lookup"><span data-stu-id="3d867-160">The health query APIs return the raw health data stored in the health store or the aggregated, interpreted health data for a specific cluster entity.</span></span>
* <span data-ttu-id="3d867-161">**映像存放區**：此服務會提供應用程式二進位檔的儲存體和發佈。</span><span class="sxs-lookup"><span data-stu-id="3d867-161">**Image Store**: This service provides storage and distribution of the application binaries.</span></span> <span data-ttu-id="3d867-162">此服務會提供簡易的分散式檔案存放區，應用程式可在其中進行上傳和下載。</span><span class="sxs-lookup"><span data-stu-id="3d867-162">This service provides a simple distributed file store where the applications are uploaded to and downloaded from.</span></span>

## <a name="hosting-subsystem"></a><span data-ttu-id="3d867-163">主控子系統</span><span class="sxs-lookup"><span data-stu-id="3d867-163">Hosting subsystem</span></span>
<span data-ttu-id="3d867-164">叢集管理員會通知主控子系統 (在每個節點上執行) 需要針對特定節點進行管理的服務。</span><span class="sxs-lookup"><span data-stu-id="3d867-164">The cluster manager informs the hosting subsystem (running on each node) which services it needs to manage for a particular node.</span></span> <span data-ttu-id="3d867-165">主控子系統接著會管理該節點上的應用程式生命週期。</span><span class="sxs-lookup"><span data-stu-id="3d867-165">The hosting subsystem then manages the lifecycle of the application on that node.</span></span> <span data-ttu-id="3d867-166">其會與可靠性和健康狀態元件互動，以確保複本放置於正確位置且健康狀態良好。</span><span class="sxs-lookup"><span data-stu-id="3d867-166">It interacts with the reliability and health components to ensure that the replicas are properly placed and are healthy.</span></span>

## <a name="communication-subsystem"></a><span data-ttu-id="3d867-167">通訊子系統</span><span class="sxs-lookup"><span data-stu-id="3d867-167">Communication subsystem</span></span>
<span data-ttu-id="3d867-168">此子系統會在叢集內提供可靠訊息，並透過命名服務提供服務探索。</span><span class="sxs-lookup"><span data-stu-id="3d867-168">This subsystem provides reliable messaging within the cluster and service discovery through the Naming service.</span></span> <span data-ttu-id="3d867-169">命名服務會將服務名稱解析至叢集中的位置，並可讓使用者能夠管理服務名稱和屬性。</span><span class="sxs-lookup"><span data-stu-id="3d867-169">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="3d867-170">用戶端可以使用命名服務，與叢集中的任何節點安全地進行通訊，以便解析服務名稱和擷取服務中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3d867-170">Using the Naming service, clients can securely communicate with any node in the cluster to resolve a service name and retrieve service metadata.</span></span> <span data-ttu-id="3d867-171">Service Fabric 的使用者可以使用簡易命名用戶端 API，開發能夠解析目前網路位置的服務和用戶端，而不受節點動態或重新調整大小的叢集的限制。</span><span class="sxs-lookup"><span data-stu-id="3d867-171">Using a simple Naming client API, users of Service Fabric can develop services and clients capable of resolving the current network location despite node dynamism or the re-sizing of the cluster.</span></span>

## <a name="testability-subsystem"></a><span data-ttu-id="3d867-172">可測試性子系統</span><span class="sxs-lookup"><span data-stu-id="3d867-172">Testability subsystem</span></span>
<span data-ttu-id="3d867-173">可測試性是一組工具套件，專門用來測試建置於 Service Fabric 上的服務。</span><span class="sxs-lookup"><span data-stu-id="3d867-173">Testability is a suite of tools specifically designed for testing services built on Service Fabric.</span></span> <span data-ttu-id="3d867-174">這些工具可讓開發人員輕鬆誘發有意義的錯誤及執行測試案例，並使用受控制的安全方式，執行及驗證服務在其生命週期會發生的各種狀態和轉換情形。</span><span class="sxs-lookup"><span data-stu-id="3d867-174">The tools let a developer easily induce meaningful faults and run test scenarios to exercise and validate the numerous states and transitions that a service will experience throughout its lifetime, all in a controlled and safe manner.</span></span> <span data-ttu-id="3d867-175">可測試性也會提供一種機制，透過執行較長時間的測試，逐一查看各種可能的失敗，而不會減損可用性。</span><span class="sxs-lookup"><span data-stu-id="3d867-175">Testability also provides a mechanism to run longer tests that can iterate through various possible failures without losing availability.</span></span> <span data-ttu-id="3d867-176">如此可為您提供生產環境中的測試。</span><span class="sxs-lookup"><span data-stu-id="3d867-176">This provides you with a test-in-production environment.</span></span>
