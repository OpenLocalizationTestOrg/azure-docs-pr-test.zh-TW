---
title: "雲端服務與 Service Fabric 之間的差異 | Microsoft Docs"
description: "這是將應用程式從雲端服務移轉到 Service Fabric 的概念性概觀。"
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
ms.openlocfilehash: 26c0256f6fa299551d92e9bcd058ca359d8c85b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-the-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a><span data-ttu-id="c8693-103">移轉應用程式之前，先了解「雲端服務」與 Service Fabric 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="c8693-103">Learn about the differences between Cloud Services and Service Fabric before migrating applications.</span></span>
<span data-ttu-id="c8693-104">Microsoft Azure Service Fabric 為次世代雲端應用程式平台，適用於高度可調整且高度可靠的分散式應用程式。</span><span class="sxs-lookup"><span data-stu-id="c8693-104">Microsoft Azure Service Fabric is the next-generation cloud application platform for highly scalable, highly reliable distributed applications.</span></span> <span data-ttu-id="c8693-105">其中導入了許多封裝、部署、更新及管理分散式雲端應用程式的新功能。</span><span class="sxs-lookup"><span data-stu-id="c8693-105">It introduces many new features for packaging, deploying, upgrading, and managing distributed cloud applications.</span></span> 

<span data-ttu-id="c8693-106">這是將應用程式從雲端服務移轉到 Service Fabric 的入門簡介。</span><span class="sxs-lookup"><span data-stu-id="c8693-106">This is an introductory guide to migrating applications from Cloud Services to Service Fabric.</span></span> <span data-ttu-id="c8693-107">內容著重於雲端服務與 Service Fabric 之間的架構及設計差異。</span><span class="sxs-lookup"><span data-stu-id="c8693-107">It focuses primarily on architectural and design differences between Cloud Services and Service Fabric.</span></span>

## <a name="applications-and-infrastructure"></a><span data-ttu-id="c8693-108">應用程式與基礎結構</span><span class="sxs-lookup"><span data-stu-id="c8693-108">Applications and infrastructure</span></span>
<span data-ttu-id="c8693-109">雲端服務與 Service Fabric 最基本的差異在於 VM、工作負載及應用程式之間的關係。</span><span class="sxs-lookup"><span data-stu-id="c8693-109">A fundamental difference between Cloud Services and Service Fabric is the relationship between VMs, workloads, and applications.</span></span> <span data-ttu-id="c8693-110">這裡的工作負載定義為您所撰寫來執行特定工作或提供服務的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8693-110">A workload here is defined as the code you write to perform a specific task or provide a service.</span></span>

* <span data-ttu-id="c8693-111">**雲端服務的重點是將應用程式部署為 VM。**</span><span class="sxs-lookup"><span data-stu-id="c8693-111">**Cloud Services is about deploying applications as VMs.**</span></span> <span data-ttu-id="c8693-112">您的程式碼緊密地與 VM 執行個體 (如 Web 或背景工作角色) 結合。</span><span class="sxs-lookup"><span data-stu-id="c8693-112">The code you write is tightly coupled to a VM instance, such as a Web or Worker Role.</span></span> <span data-ttu-id="c8693-113">在雲端服務中部署工作負載，即為部署一或多個執行該工作負載的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c8693-113">To deploy a workload in Cloud Services is to deploy one or more VM instances that run the workload.</span></span> <span data-ttu-id="c8693-114">應用程式與 VM 沒有區別，因此對於應用程式也沒有正式的定義。</span><span class="sxs-lookup"><span data-stu-id="c8693-114">There is no separation of applications and VMs, and so there is no formal definition of an application.</span></span> <span data-ttu-id="c8693-115">應用程式可以視為雲端服務部署中的一組 Web 或背景工作角色，或是整個雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="c8693-115">An application can be thought of as a set of Web or Worker Role instances within a Cloud Services deployment or as an entire Cloud Services deployment.</span></span> <span data-ttu-id="c8693-116">在此範例中，應用程式會顯示為一組角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="c8693-116">In this example, an application is shown as a set of role instances.</span></span>

![雲端服務應用程式和拓撲][1]

* <span data-ttu-id="c8693-118">**Service Fabric 的重點是將應用程式部署到現有的 VM 或執行 Service Fabric 的 Windows 或 Linux 電腦。**</span><span class="sxs-lookup"><span data-stu-id="c8693-118">**Service Fabric is about deploying applications to existing VMs or machines running Service Fabric on Windows or Linux.**</span></span> <span data-ttu-id="c8693-119">您撰寫的服務完全與背後的基礎服務分離 (由 Service Fabric 應用程式平台抽象化)，因此可以將應用程式部署在多個環境。</span><span class="sxs-lookup"><span data-stu-id="c8693-119">The services you write are completely decoupled from the underlying infrastructure, which is abstracted away by the Service Fabric application platform, so an application can be deployed to multiple environments.</span></span> <span data-ttu-id="c8693-120">Service Fabric 中的工作負載稱為「服務」，而一或多個服務會在 Service Fabric 應用程式平台上執行且正式定義的應用程式中形成群組。</span><span class="sxs-lookup"><span data-stu-id="c8693-120">A workload in Service Fabric is called a "service," and one or more services are grouped in a formally-defined application that runs on the Service Fabric application platform.</span></span> <span data-ttu-id="c8693-121">可將多個應用程式部署到單一的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="c8693-121">Multiple applications can be deployed to a single Service Fabric cluster.</span></span>

![Service Fabric 應用程式和拓撲][2]

<span data-ttu-id="c8693-123">Service Fabric 本身是在 Windows 或 Linux 執行的應用程式平台層，而雲端服務是用來部署受 Azure 管理且連接工作負載的 VM。</span><span class="sxs-lookup"><span data-stu-id="c8693-123">Service Fabric itself is an application platform layer that runs on Windows or Linux, whereas Cloud Services is a system for deploying Azure-managed VMs with workloads attached.</span></span>
<span data-ttu-id="c8693-124">Service Fabric 應用程式模型有許多優點：</span><span class="sxs-lookup"><span data-stu-id="c8693-124">The Service Fabric application model has a number of advantages:</span></span>

* <span data-ttu-id="c8693-125">部署快速。</span><span class="sxs-lookup"><span data-stu-id="c8693-125">Fast deployment times.</span></span> <span data-ttu-id="c8693-126">建立 VM 執行個體可能非常耗時。</span><span class="sxs-lookup"><span data-stu-id="c8693-126">Creating VM instances can be time consuming.</span></span> <span data-ttu-id="c8693-127">在 Service Fabric 中，只會部署一次 VM 以形成裝載 Service Fabric 應用程式平台的叢集。</span><span class="sxs-lookup"><span data-stu-id="c8693-127">In Service Fabric, VMs are only deployed once to form a cluster that hosts the Service Fabric application platform.</span></span> <span data-ttu-id="c8693-128">此後，應用程式封裝可快速部署到該叢集。</span><span class="sxs-lookup"><span data-stu-id="c8693-128">From that point on, application packages can be deployed to the cluster very quickly.</span></span>
* <span data-ttu-id="c8693-129">高密度裝載。</span><span class="sxs-lookup"><span data-stu-id="c8693-129">High-density hosting.</span></span> <span data-ttu-id="c8693-130">在雲端服務中，一個背景工作角色 VM 裝載一個工作負載。</span><span class="sxs-lookup"><span data-stu-id="c8693-130">In Cloud Services, a Worker Role VM hosts one workload.</span></span> <span data-ttu-id="c8693-131">在 Service Fabric 中，應用程式與執行它們的 VM 分離，表示您可以將大量的應用程式部署到小量的 VM，這樣可以降低大量部署的成本。</span><span class="sxs-lookup"><span data-stu-id="c8693-131">In Service Fabric, applications are separate from the VMs that run them, meaning you can deploy a large number of applications to a small number of VMs, which can lower overall cost for larger deployments.</span></span>
* <span data-ttu-id="c8693-132">Service Fabric 平台可在任何具備 Windows Server 或 Linux 電腦的位置執行，不論為 Azure 或內部部署。</span><span class="sxs-lookup"><span data-stu-id="c8693-132">The Service Fabric platform can run anywhere that has Windows Server or Linux machines, whether it's Azure or on-premises.</span></span> <span data-ttu-id="c8693-133">平台透過背後的基礎結構提供抽象層，因此您的應用程式可在不同環境執行。</span><span class="sxs-lookup"><span data-stu-id="c8693-133">The platform provides an abstraction layer over the underlying infrastructure so your application can run on different environments.</span></span> 
* <span data-ttu-id="c8693-134">管理分散式應用程式。</span><span class="sxs-lookup"><span data-stu-id="c8693-134">Distributed application management.</span></span> <span data-ttu-id="c8693-135">Service Fabric 這個平台不僅能裝載分散式應用程式，也協助獨立於主控 VM 或電腦生命週期之外管理其生命週期。</span><span class="sxs-lookup"><span data-stu-id="c8693-135">Service Fabric is a platform that not only hosts distributed applications, but also helps manage their lifecycle independently of the hosting VM or machine lifecycle.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="c8693-136">應用程式架構</span><span class="sxs-lookup"><span data-stu-id="c8693-136">Application architecture</span></span>
<span data-ttu-id="c8693-137">雲端服務應用程式的基礎結構通常包括數個外部服務相依性 (例如服務匯流排、Azure 資料表與 Blob 儲存體、SQL、Redis 等)，以管理應用程式的狀態及資料，並和在雲端服務部署中的 Web 及背景工作角色通訊。</span><span class="sxs-lookup"><span data-stu-id="c8693-137">The architecture of a Cloud Services application usually includes numerous external service dependencies, such as Service Bus, Azure Table and Blob Storage, SQL, Redis, and others to manage the state and data of an application and communication between Web and Worker Roles in a Cloud Services deployment.</span></span> <span data-ttu-id="c8693-138">完整雲端服務應用程式的範例如下：</span><span class="sxs-lookup"><span data-stu-id="c8693-138">An example of a complete Cloud Services application might look like this:</span></span>  

![雲端服務架構][9]

<span data-ttu-id="c8693-140">Service Fabric 應用程式也可以選擇在完整應用程式中使用同樣的外部服務。</span><span class="sxs-lookup"><span data-stu-id="c8693-140">Service Fabric applications can also choose to use the same external services in a complete application.</span></span> <span data-ttu-id="c8693-141">使用這個 Cloud Services 基礎結構範例，從雲端服務移轉到 Service Fabric 最簡單的路徑是，只將雲端服務部署以 Service Fabric 應用程式取代，整體基礎結構則保持相同。</span><span class="sxs-lookup"><span data-stu-id="c8693-141">Using this example Cloud Services architecture, the simplest migration path from Cloud Services to Service Fabric is to replace only the Cloud Services deployment with a Service Fabric application, keeping the overall architecture the same.</span></span> <span data-ttu-id="c8693-142">變更最少量的程式碼，即可將 Web 和背景工作角色移植到 Service Fabric 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="c8693-142">The Web and Worker Roles can be ported to Service Fabric stateless services with minimal code changes.</span></span>

![簡單移轉後的 Service Fabric 架構][10]

<span data-ttu-id="c8693-144">在這個階段，系統應該如先前般運作。</span><span class="sxs-lookup"><span data-stu-id="c8693-144">At this stage, the system should continue to work the same as before.</span></span> <span data-ttu-id="c8693-145">善加利用 Service Fabric 的具狀態服務，若適用則外部狀態存放區可初始化為具狀態服務。</span><span class="sxs-lookup"><span data-stu-id="c8693-145">Taking advantage of Service Fabric's stateful features, external state stores can be internalized as stateful services where applicable.</span></span> <span data-ttu-id="c8693-146">這比單純移轉 Web 和背景工作角色至 Service Fabric 無狀態服務更複雜，因為需要撰寫如先前外部服務為應用程式提供之相同功能性的自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="c8693-146">This is more involved than a simple migration of Web and Worker Roles to Service Fabric stateless services, as it requires writing custom services that provide equivalent functionality to your application as the external services did before.</span></span> <span data-ttu-id="c8693-147">這樣做的優點包括︰</span><span class="sxs-lookup"><span data-stu-id="c8693-147">The benefits of doing so include:</span></span> 

* <span data-ttu-id="c8693-148">移除外部相依性</span><span class="sxs-lookup"><span data-stu-id="c8693-148">Removing external dependencies</span></span> 
* <span data-ttu-id="c8693-149">統一部署、管理及升級模型。</span><span class="sxs-lookup"><span data-stu-id="c8693-149">Unifying the deployment, management, and upgrade models.</span></span> 

<span data-ttu-id="c8693-150">初始化這些服務的基礎結構之結果的範例如下：</span><span class="sxs-lookup"><span data-stu-id="c8693-150">An example resulting architecture of internalizing these services could look like this:</span></span>

![完整移轉後的 Service Fabric 架構][11]

## <a name="communication-and-workflow"></a><span data-ttu-id="c8693-152">通訊與工作流程</span><span class="sxs-lookup"><span data-stu-id="c8693-152">Communication and workflow</span></span>
<span data-ttu-id="c8693-153">大部分的雲端服務應用程式由一個以上的層組成。</span><span class="sxs-lookup"><span data-stu-id="c8693-153">Most Cloud Service applications consist of more than one tier.</span></span> <span data-ttu-id="c8693-154">同樣地，Service Fabric 應用程式由一個以上的服務組成 (通常是許多服務)。</span><span class="sxs-lookup"><span data-stu-id="c8693-154">Similarly, a Service Fabric application consists of more than one service (typically many services).</span></span> <span data-ttu-id="c8693-155">二種常見的通訊模型為直接通訊及透過外部耐久性儲存體。</span><span class="sxs-lookup"><span data-stu-id="c8693-155">Two common communication models are direct communication and via an external durable storage.</span></span>

### <a name="direct-communication"></a><span data-ttu-id="c8693-156">直接通訊</span><span class="sxs-lookup"><span data-stu-id="c8693-156">Direct communication</span></span>
<span data-ttu-id="c8693-157">使用直接通訊，層之間可以透過各自所公開的端點直接通訊。</span><span class="sxs-lookup"><span data-stu-id="c8693-157">With direct communication, tiers can communicate directly through endpoint exposed by each tier.</span></span> <span data-ttu-id="c8693-158">在無狀態的環境 (例如雲端服務) 中，這表示選取 VM 角色的執行個體 (不論是隨機或循環資源配置以平衡負載)，並直接連接到其端點。</span><span class="sxs-lookup"><span data-stu-id="c8693-158">In stateless environments such as Cloud Services, this means selecting an instance of a VM role, either randomly or round-robin to balance load, and connecting to its endpoint directly.</span></span>

![雲端服務直接通訊][5]

 <span data-ttu-id="c8693-160">直接通訊是 Service Fabric 中常見的通訊模型。</span><span class="sxs-lookup"><span data-stu-id="c8693-160">Direct communication is a common communication model in Service Fabric.</span></span> <span data-ttu-id="c8693-161">Service Fabric 和雲端服務的關鍵差異在於，在雲端服務中您是連接到 VM，而在 Service Fabric 中是連接到服務。</span><span class="sxs-lookup"><span data-stu-id="c8693-161">The key difference between Service Fabric and Cloud Services is that in Cloud Services you connect to a VM, whereas in Service Fabric you connect to a service.</span></span> <span data-ttu-id="c8693-162">這是重要差異，原因如下：</span><span class="sxs-lookup"><span data-stu-id="c8693-162">This is an important distinction for a couple reasons:</span></span>

* <span data-ttu-id="c8693-163">Service Fabric 中的服務不受限於裝載它們的 VM。服務可以在叢集中移動，且已預期會因為幾個原因而移動：資源平衡、容錯移轉、應用程式和基礎結構更新，以及位置或負載的限制。</span><span class="sxs-lookup"><span data-stu-id="c8693-163">Services in Service Fabric are not bound to the VMs that host them; services may move around in the cluster, and in fact, are expected to move around for various reasons: Resource balancing, failover, application and infrastructure upgrades, and placement or load constraints.</span></span> <span data-ttu-id="c8693-164">這表示服務執行個體的位址可隨時變更。</span><span class="sxs-lookup"><span data-stu-id="c8693-164">This means a service instance's address can change at any time.</span></span> 
* <span data-ttu-id="c8693-165">Service Fabric 中的 VM 可以託管多個服務，且每個有獨特的端點。</span><span class="sxs-lookup"><span data-stu-id="c8693-165">A VM in Service Fabric can host multiple services, each with unique endpoints.</span></span>

<span data-ttu-id="c8693-166">Service Fabric 提供服務探索機制 (稱為「名稱服務」)，可用來解析服務的端點位置。</span><span class="sxs-lookup"><span data-stu-id="c8693-166">Service Fabric provides a service discovery mechanism, called the Naming Service, which can be used to resolve endpoint addresses of services.</span></span> 

![Service Fabric 直接通訊][6]

### <a name="queues"></a><span data-ttu-id="c8693-168">佇列</span><span class="sxs-lookup"><span data-stu-id="c8693-168">Queues</span></span>
<span data-ttu-id="c8693-169">層與無狀態環境 (如雲端服務) 之間的常見通訊機制是使用外部儲存體佇列持久地儲存各層的工作狀態。</span><span class="sxs-lookup"><span data-stu-id="c8693-169">A common communication mechanism between tiers in stateless environments such as Cloud Services is to use an external storage queue to durably store work tasks from one tier to another.</span></span> <span data-ttu-id="c8693-170">常見的案例是 Web 層將作業傳送到背景工作角色執行個體可以清除佇列並處理作業的 Azure Queue 或服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="c8693-170">A common scenario is a web tier that sends jobs to an Azure Queue or Service Bus where Worker Role instances can dequeue and process the jobs.</span></span>

![雲端服務佇列通訊][7]

<span data-ttu-id="c8693-172">同樣的通訊模型可以用在 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="c8693-172">The same communication model can be used in Service Fabric.</span></span> <span data-ttu-id="c8693-173">這有助於將現有的雲端服務應用程式移轉到 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="c8693-173">This can be useful when migrating an existing Cloud Services application to Service Fabric.</span></span> 

![Service Fabric 直接通訊][8]

## <a name="next-steps"></a><span data-ttu-id="c8693-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8693-175">Next Steps</span></span>
<span data-ttu-id="c8693-176">從雲端服務移轉到 Service Fabric 最簡單的路徑是，只將雲端服務部署以 Service Fabric 應用程式取代，應用程式的整體基礎結構則大致上相同。</span><span class="sxs-lookup"><span data-stu-id="c8693-176">The simplest migration path from Cloud Services to Service Fabric is to replace only the Cloud Services deployment with a Service Fabric application, keeping the overall architecture of your application roughly the same.</span></span> <span data-ttu-id="c8693-177">下列文章提供指南，以協助將 Web 和背景工作角色移轉到 Service Fabric 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="c8693-177">The following article provides a guide to help convert a Web or Worker Role to a Service Fabric stateless service.</span></span>

* [<span data-ttu-id="c8693-178">簡單移轉：將 Web 或背景工作角色轉換到 Service Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="c8693-178">Simple migration: convert a Web or Worker Role to a Service Fabric stateless service</span></span>](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

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
