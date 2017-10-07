---
title: "雲端服務和服務網狀架構之間的 aaaDifferences |Microsoft 文件"
description: "概念的概觀，移轉的雲端服務 tooService 網狀架構的應用程式。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a><span data-ttu-id="14741-103">深入了解雲端服務和服務網狀架構的 hello 差異，然後再移轉應用程式。</span><span class="sxs-lookup"><span data-stu-id="14741-103">Learn about hello differences between Cloud Services and Service Fabric before migrating applications.</span></span>
<span data-ttu-id="14741-104">Microsoft Azure Service Fabric 是可高度擴充、 可靠的分散式應用程式的 hello 新一代雲端應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="14741-104">Microsoft Azure Service Fabric is hello next-generation cloud application platform for highly scalable, highly reliable distributed applications.</span></span> <span data-ttu-id="14741-105">其中導入了許多封裝、部署、更新及管理分散式雲端應用程式的新功能。</span><span class="sxs-lookup"><span data-stu-id="14741-105">It introduces many new features for packaging, deploying, upgrading, and managing distributed cloud applications.</span></span> 

<span data-ttu-id="14741-106">這是從雲端服務 tooService 網狀架構入門指南 toomigrating 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14741-106">This is an introductory guide toomigrating applications from Cloud Services tooService Fabric.</span></span> <span data-ttu-id="14741-107">內容著重於雲端服務與 Service Fabric 之間的架構及設計差異。</span><span class="sxs-lookup"><span data-stu-id="14741-107">It focuses primarily on architectural and design differences between Cloud Services and Service Fabric.</span></span>

## <a name="applications-and-infrastructure"></a><span data-ttu-id="14741-108">應用程式與基礎結構</span><span class="sxs-lookup"><span data-stu-id="14741-108">Applications and infrastructure</span></span>
<span data-ttu-id="14741-109">雲端服務和服務網狀架構基本差別在於 hello Vm、 工作負載和應用程式之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="14741-109">A fundamental difference between Cloud Services and Service Fabric is hello relationship between VMs, workloads, and applications.</span></span> <span data-ttu-id="14741-110">Hello 程式碼撰寫 tooperform 特定工作，或提供服務的工作負載的定義。</span><span class="sxs-lookup"><span data-stu-id="14741-110">A workload here is defined as hello code you write tooperform a specific task or provide a service.</span></span>

* <span data-ttu-id="14741-111">**雲端服務的重點是將應用程式部署為 VM。**</span><span class="sxs-lookup"><span data-stu-id="14741-111">**Cloud Services is about deploying applications as VMs.**</span></span> <span data-ttu-id="14741-112">hello 您撰寫的程式碼是緊密結合的 tooa VM 執行個體，例如 Web 或背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="14741-112">hello code you write is tightly coupled tooa VM instance, such as a Web or Worker Role.</span></span> <span data-ttu-id="14741-113">toodeploy 雲端服務中的工作負載 toodeploy 其中一個或多個 VM 執行個體執行的 hello 工作負載。</span><span class="sxs-lookup"><span data-stu-id="14741-113">toodeploy a workload in Cloud Services is toodeploy one or more VM instances that run hello workload.</span></span> <span data-ttu-id="14741-114">應用程式與 VM 沒有區別，因此對於應用程式也沒有正式的定義。</span><span class="sxs-lookup"><span data-stu-id="14741-114">There is no separation of applications and VMs, and so there is no formal definition of an application.</span></span> <span data-ttu-id="14741-115">應用程式可以視為雲端服務部署中的一組 Web 或背景工作角色，或是整個雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="14741-115">An application can be thought of as a set of Web or Worker Role instances within a Cloud Services deployment or as an entire Cloud Services deployment.</span></span> <span data-ttu-id="14741-116">在此範例中，應用程式會顯示為一組角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="14741-116">In this example, an application is shown as a set of role instances.</span></span>

![雲端服務應用程式和拓撲][1]

* <span data-ttu-id="14741-118">**Service Fabric 是關於部署應用程式 tooexisting Vm 或 Windows 或 Linux 上執行 Service Fabric 的機器。**</span><span class="sxs-lookup"><span data-stu-id="14741-118">**Service Fabric is about deploying applications tooexisting VMs or machines running Service Fabric on Windows or Linux.**</span></span> <span data-ttu-id="14741-119">您撰寫的 hello 服務是從基礎基礎結構，抽象的 hello Service Fabric 應用程式平台，好讓應用程式可以部署的 toomultiple 環境的 hello 完全解除解合。</span><span class="sxs-lookup"><span data-stu-id="14741-119">hello services you write are completely decoupled from hello underlying infrastructure, which is abstracted away by hello Service Fabric application platform, so an application can be deployed toomultiple environments.</span></span> <span data-ttu-id="14741-120">工作負載服務網狀架構中稱為 「 服務 」，而一或多個服務會一起 hello Service Fabric 應用程式平台執行的正式定義應用程式中。</span><span class="sxs-lookup"><span data-stu-id="14741-120">A workload in Service Fabric is called a "service," and one or more services are grouped in a formally-defined application that runs on hello Service Fabric application platform.</span></span> <span data-ttu-id="14741-121">多個應用程式可以是已部署的 tooa 單一 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="14741-121">Multiple applications can be deployed tooa single Service Fabric cluster.</span></span>

![Service Fabric 應用程式和拓撲][2]

<span data-ttu-id="14741-123">Service Fabric 本身是在 Windows 或 Linux 執行的應用程式平台層，而雲端服務是用來部署受 Azure 管理且連接工作負載的 VM。</span><span class="sxs-lookup"><span data-stu-id="14741-123">Service Fabric itself is an application platform layer that runs on Windows or Linux, whereas Cloud Services is a system for deploying Azure-managed VMs with workloads attached.</span></span>
<span data-ttu-id="14741-124">hello Service Fabric 應用程式模型有許多優點：</span><span class="sxs-lookup"><span data-stu-id="14741-124">hello Service Fabric application model has a number of advantages:</span></span>

* <span data-ttu-id="14741-125">部署快速。</span><span class="sxs-lookup"><span data-stu-id="14741-125">Fast deployment times.</span></span> <span data-ttu-id="14741-126">建立 VM 執行個體可能非常耗時。</span><span class="sxs-lookup"><span data-stu-id="14741-126">Creating VM instances can be time consuming.</span></span> <span data-ttu-id="14741-127">在 Service Fabric 一旦 tooform 叢集，主控 hello Service Fabric 應用程式平台，只會部署 Vm。</span><span class="sxs-lookup"><span data-stu-id="14741-127">In Service Fabric, VMs are only deployed once tooform a cluster that hosts hello Service Fabric application platform.</span></span> <span data-ttu-id="14741-128">從該點上，應用程式封裝可以非常快速地是已部署的 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="14741-128">From that point on, application packages can be deployed toohello cluster very quickly.</span></span>
* <span data-ttu-id="14741-129">高密度裝載。</span><span class="sxs-lookup"><span data-stu-id="14741-129">High-density hosting.</span></span> <span data-ttu-id="14741-130">在雲端服務中，一個背景工作角色 VM 裝載一個工作負載。</span><span class="sxs-lookup"><span data-stu-id="14741-130">In Cloud Services, a Worker Role VM hosts one workload.</span></span> <span data-ttu-id="14741-131">在 Service Fabric 應用程式的不同的 hello Vm 加以執行，這表示您可以部署大量的應用程式 tooa 少數幾個 Vm，可降低整體成本較大的部署。</span><span class="sxs-lookup"><span data-stu-id="14741-131">In Service Fabric, applications are separate from hello VMs that run them, meaning you can deploy a large number of applications tooa small number of VMs, which can lower overall cost for larger deployments.</span></span>
* <span data-ttu-id="14741-132">hello Service Fabric 平台可以執行任何位置，具有 Windows Server 或 Linux 機器，它是 Azure 或內部部署。</span><span class="sxs-lookup"><span data-stu-id="14741-132">hello Service Fabric platform can run anywhere that has Windows Server or Linux machines, whether it's Azure or on-premises.</span></span> <span data-ttu-id="14741-133">hello 平台透過 hello 基礎結構提供一個抽象層，讓您的應用程式可以在不同的環境中執行。</span><span class="sxs-lookup"><span data-stu-id="14741-133">hello platform provides an abstraction layer over hello underlying infrastructure so your application can run on different environments.</span></span> 
* <span data-ttu-id="14741-134">管理分散式應用程式。</span><span class="sxs-lookup"><span data-stu-id="14741-134">Distributed application management.</span></span> <span data-ttu-id="14741-135">Service Fabric 是平台，不只裝載分散式應用程式，但也可協助管理其生命週期獨立 hello 裝載 VM 或電腦生命週期。</span><span class="sxs-lookup"><span data-stu-id="14741-135">Service Fabric is a platform that not only hosts distributed applications, but also helps manage their lifecycle independently of hello hosting VM or machine lifecycle.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="14741-136">應用程式架構</span><span class="sxs-lookup"><span data-stu-id="14741-136">Application architecture</span></span>
<span data-ttu-id="14741-137">hello 架構的雲端服務應用程式通常包括許多外部服務相依性，例如服務匯流排、 Azure 資料表和 Blob 儲存體、 SQL、 Redis，和其他人 toomanage hello 狀態和資料的應用程式和網站之間的通訊和雲端服務部署中的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="14741-137">hello architecture of a Cloud Services application usually includes numerous external service dependencies, such as Service Bus, Azure Table and Blob Storage, SQL, Redis, and others toomanage hello state and data of an application and communication between Web and Worker Roles in a Cloud Services deployment.</span></span> <span data-ttu-id="14741-138">完整雲端服務應用程式的範例如下：</span><span class="sxs-lookup"><span data-stu-id="14741-138">An example of a complete Cloud Services application might look like this:</span></span>  

![雲端服務架構][9]

<span data-ttu-id="14741-140">Service Fabric 應用程式也可以選擇 toouse hello 相同的外部服務的完整應用程式中。</span><span class="sxs-lookup"><span data-stu-id="14741-140">Service Fabric applications can also choose toouse hello same external services in a complete application.</span></span> <span data-ttu-id="14741-141">使用此雲端服務架構的範例，hello 簡單的移轉路徑從雲端服務 tooService 網狀架構是 tooreplace 僅 hello 雲端服務部署 Service Fabric 應用程式，保留 hello 整體架構 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="14741-141">Using this example Cloud Services architecture, hello simplest migration path from Cloud Services tooService Fabric is tooreplace only hello Cloud Services deployment with a Service Fabric application, keeping hello overall architecture hello same.</span></span> <span data-ttu-id="14741-142">hello Web 和背景工作角色可以是移植的 tooService Fabric 無狀態服務以最少的程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="14741-142">hello Web and Worker Roles can be ported tooService Fabric stateless services with minimal code changes.</span></span>

![簡單移轉後的 Service Fabric 架構][10]

<span data-ttu-id="14741-144">在這個階段，hello 系統應該繼續 toowork 如常 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="14741-144">At this stage, hello system should continue toowork hello same as before.</span></span> <span data-ttu-id="14741-145">善加利用 Service Fabric 的具狀態服務，若適用則外部狀態存放區可初始化為具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="14741-145">Taking advantage of Service Fabric's stateful features, external state stores can be internalized as stateful services where applicable.</span></span> <span data-ttu-id="14741-146">這是比更為複雜的簡易移轉，Web 和背景工作角色 tooService 網狀架構無狀態服務，因為它需要撰寫自訂之前 hello 外部服務一樣，提供對等的功能 tooyour 應用程式的服務。</span><span class="sxs-lookup"><span data-stu-id="14741-146">This is more involved than a simple migration of Web and Worker Roles tooService Fabric stateless services, as it requires writing custom services that provide equivalent functionality tooyour application as hello external services did before.</span></span> <span data-ttu-id="14741-147">這樣做的 hello 優點包括：</span><span class="sxs-lookup"><span data-stu-id="14741-147">hello benefits of doing so include:</span></span> 

* <span data-ttu-id="14741-148">移除外部相依性</span><span class="sxs-lookup"><span data-stu-id="14741-148">Removing external dependencies</span></span> 
* <span data-ttu-id="14741-149">統一的 hello 部署、 管理及升級模型。</span><span class="sxs-lookup"><span data-stu-id="14741-149">Unifying hello deployment, management, and upgrade models.</span></span> 

<span data-ttu-id="14741-150">初始化這些服務的基礎結構之結果的範例如下：</span><span class="sxs-lookup"><span data-stu-id="14741-150">An example resulting architecture of internalizing these services could look like this:</span></span>

![完整移轉後的 Service Fabric 架構][11]

## <a name="communication-and-workflow"></a><span data-ttu-id="14741-152">通訊與工作流程</span><span class="sxs-lookup"><span data-stu-id="14741-152">Communication and workflow</span></span>
<span data-ttu-id="14741-153">大部分的雲端服務應用程式由一個以上的層組成。</span><span class="sxs-lookup"><span data-stu-id="14741-153">Most Cloud Service applications consist of more than one tier.</span></span> <span data-ttu-id="14741-154">同樣地，Service Fabric 應用程式由一個以上的服務組成 (通常是許多服務)。</span><span class="sxs-lookup"><span data-stu-id="14741-154">Similarly, a Service Fabric application consists of more than one service (typically many services).</span></span> <span data-ttu-id="14741-155">二種常見的通訊模型為直接通訊及透過外部耐久性儲存體。</span><span class="sxs-lookup"><span data-stu-id="14741-155">Two common communication models are direct communication and via an external durable storage.</span></span>

### <a name="direct-communication"></a><span data-ttu-id="14741-156">直接通訊</span><span class="sxs-lookup"><span data-stu-id="14741-156">Direct communication</span></span>
<span data-ttu-id="14741-157">使用直接通訊，層之間可以透過各自所公開的端點直接通訊。</span><span class="sxs-lookup"><span data-stu-id="14741-157">With direct communication, tiers can communicate directly through endpoint exposed by each tier.</span></span> <span data-ttu-id="14741-158">在無狀態的環境，例如雲端服務，此表示選取的 VM 角色執行個體可以隨機或 toobalance 循環配置資源負載，而連線 tooits 端點直接。</span><span class="sxs-lookup"><span data-stu-id="14741-158">In stateless environments such as Cloud Services, this means selecting an instance of a VM role, either randomly or round-robin toobalance load, and connecting tooits endpoint directly.</span></span>

![雲端服務直接通訊][5]

 <span data-ttu-id="14741-160">直接通訊是 Service Fabric 中常見的通訊模型。</span><span class="sxs-lookup"><span data-stu-id="14741-160">Direct communication is a common communication model in Service Fabric.</span></span> <span data-ttu-id="14741-161">hello Service Fabric 和雲端服務之間的主要差異是雲端服務中您連線 tooa VM，而您可以在 Service Fabric 連線 tooa 服務。</span><span class="sxs-lookup"><span data-stu-id="14741-161">hello key difference between Service Fabric and Cloud Services is that in Cloud Services you connect tooa VM, whereas in Service Fabric you connect tooa service.</span></span> <span data-ttu-id="14741-162">這是重要差異，原因如下：</span><span class="sxs-lookup"><span data-stu-id="14741-162">This is an important distinction for a couple reasons:</span></span>

* <span data-ttu-id="14741-163">在 Service Fabric 服務未繫結的 toohello Vm 中裝載這些;服務可能移動在 hello 叢集中，而且事實上，周圍的預期的 toomove 基於各種原因： 資源平衡、 容錯移轉、 應用程式和基礎結構升級和放置或載入條件約束。</span><span class="sxs-lookup"><span data-stu-id="14741-163">Services in Service Fabric are not bound toohello VMs that host them; services may move around in hello cluster, and in fact, are expected toomove around for various reasons: Resource balancing, failover, application and infrastructure upgrades, and placement or load constraints.</span></span> <span data-ttu-id="14741-164">這表示服務執行個體的位址可隨時變更。</span><span class="sxs-lookup"><span data-stu-id="14741-164">This means a service instance's address can change at any time.</span></span> 
* <span data-ttu-id="14741-165">Service Fabric 中的 VM 可以託管多個服務，且每個有獨特的端點。</span><span class="sxs-lookup"><span data-stu-id="14741-165">A VM in Service Fabric can host multiple services, each with unique endpoints.</span></span>

<span data-ttu-id="14741-166">Service Fabric 提供服務探索機制，稱為 hello 命名服務，可以使用的 tooresolve 服務的端點位址。</span><span class="sxs-lookup"><span data-stu-id="14741-166">Service Fabric provides a service discovery mechanism, called hello Naming Service, which can be used tooresolve endpoint addresses of services.</span></span> 

![Service Fabric 直接通訊][6]

### <a name="queues"></a><span data-ttu-id="14741-168">佇列</span><span class="sxs-lookup"><span data-stu-id="14741-168">Queues</span></span>
<span data-ttu-id="14741-169">在無狀態的環境，例如雲端服務的各層之間常見的通訊機制是 toouse 外部儲存體佇列 toodurably 儲存從某一層 tooanother 的工作。</span><span class="sxs-lookup"><span data-stu-id="14741-169">A common communication mechanism between tiers in stateless environments such as Cloud Services is toouse an external storage queue toodurably store work tasks from one tier tooanother.</span></span> <span data-ttu-id="14741-170">常見的案例是傳送作業 tooan Azure 佇列的 web 層或服務匯流排背景工作角色執行個體可以清除佇列並處理 hello 作業的位置。</span><span class="sxs-lookup"><span data-stu-id="14741-170">A common scenario is a web tier that sends jobs tooan Azure Queue or Service Bus where Worker Role instances can dequeue and process hello jobs.</span></span>

![雲端服務佇列通訊][7]

<span data-ttu-id="14741-172">相同的通訊模式可用於 Service Fabric hello。</span><span class="sxs-lookup"><span data-stu-id="14741-172">hello same communication model can be used in Service Fabric.</span></span> <span data-ttu-id="14741-173">移轉現有的雲端服務應用程式 tooService 網狀架構時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="14741-173">This can be useful when migrating an existing Cloud Services application tooService Fabric.</span></span> 

![Service Fabric 直接通訊][8]

## <a name="next-steps"></a><span data-ttu-id="14741-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14741-175">Next Steps</span></span>
<span data-ttu-id="14741-176">hello 簡單的移轉路徑，從 網狀架構是 tooreplace 只 hello Service Fabric 應用程式，讓雲端服務部署 hello 整體架構的應用程式大致上的雲端服務 tooService hello 相同。</span><span class="sxs-lookup"><span data-stu-id="14741-176">hello simplest migration path from Cloud Services tooService Fabric is tooreplace only hello Cloud Services deployment with a Service Fabric application, keeping hello overall architecture of your application roughly hello same.</span></span> <span data-ttu-id="14741-177">hello 下列文章提供的指引 toohelp 轉換 Web 或背景工作角色 tooa Service Fabric 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="14741-177">hello following article provides a guide toohelp convert a Web or Worker Role tooa Service Fabric stateless service.</span></span>

* [<span data-ttu-id="14741-178">簡單的移轉： 轉換 Web 或背景工作角色 tooa Service Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="14741-178">Simple migration: convert a Web or Worker Role tooa Service Fabric stateless service</span></span>](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
