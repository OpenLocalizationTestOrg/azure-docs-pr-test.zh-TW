---
title: "Azure 上的 Service Fabric 概觀 | Microsoft Docs"
description: "組成多個微服務以提供調整和恢復功能的 Service Fabric 概觀。 Service Fabric 是一種分散式系統平台，用來建置可調整、可靠且輕鬆管理的雲端應用程式。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 32e84984a61bb54ea459826f191de7fc25fc2158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-azure-service-fabric"></a><span data-ttu-id="5c6f9-104">Azure Service Fabric 概觀</span><span class="sxs-lookup"><span data-stu-id="5c6f9-104">Overview of Azure Service Fabric</span></span>
<span data-ttu-id="5c6f9-105">Azure Service Fabric 是一個分散式系統平台，可讓您輕鬆封裝、部署及管理可調整和可信賴的微服務與容器。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-105">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span> <span data-ttu-id="5c6f9-106">Service Fabric 也解決了開發及管理雲端原生應用程式時所面臨的重大挑戰。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-106">Service Fabric also addresses the significant challenges in developing and managing cloud native applications.</span></span> <span data-ttu-id="5c6f9-107">開發人員與管理員能夠避免複雜的基礎結構問題，專注於實作關鍵且嚴格要求之可調整、可信賴且可管理的工作負載。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-107">Developers and administrators can avoid complex infrastructure problems and focus on implementing mission-critical, demanding workloads that are scalable, reliable, and manageable.</span></span> <span data-ttu-id="5c6f9-108">Service Fabric 代表新一代的平台，可用於建置及管理這些在容器中執行的企業級、第一層雲端級別應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-108">Service Fabric represents the next-generation platform for building and managing these enterprise-class, tier-1, cloud-scale applications running in containers.</span></span>

<span data-ttu-id="5c6f9-109">此短片將介紹 Service Fabric 和微服務：<center><a target="_blank" href="https://aka.ms/servicefabricvideo"></span><span class="sxs-lookup"><span data-stu-id="5c6f9-109">This short video introduces Service Fabric and microservices: <center><a target="_blank" href="https://aka.ms/servicefabricvideo"></span></span>  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a><span data-ttu-id="5c6f9-110">由微服務組成的應用程式</span><span class="sxs-lookup"><span data-stu-id="5c6f9-110">Applications composed of microservices</span></span> 
<span data-ttu-id="5c6f9-111">Service Fabric 可讓您建置及管理由微服務組成的應用程式，這類應用程式可調整且可靠，並以高密度方式在共用的機器集區 (稱為叢集) 上執行。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-111">Service Fabric enables you to build and manage scalable and reliable applications composed of microservices that run at high density on a shared pool of machines, which is referred to as a cluster.</span></span> <span data-ttu-id="5c6f9-112">它提供精密、輕量的執行階段，可建置在容器中執行之分散式、可調整的無狀態和具狀態微服務。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-112">It provides a sophisticated, lightweight runtime to build distributed, scalable, stateless, and stateful microservices running in containers.</span></span> <span data-ttu-id="5c6f9-113">此外，還提供完整的應用程式管理功能，可佈建、部署、監視、升級/修補及刪除已部署的應用程式，包括容器化服務。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-113">It also provides comprehensive application management capabilities to provision, deploy, monitor, upgrade/patch, and delete deployed applications including containerized services.</span></span>

<span data-ttu-id="5c6f9-114">Service Fabric 提供技術支援給現今許多 Microsoft 服務，包括 Azure SQL Database、Azure Cosmos DB、Cortana、Microsoft Power BI、Microsoft Intune、「Azure 事件中樞」、「Azure IoT 中樞」、Dynamics 365、「商務用 Skype」以及許多核心 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-114">Service Fabric powers many Microsoft services today, including Azure SQL Database, Azure Cosmos DB, Cortana, Microsoft Power BI, Microsoft Intune, Azure Event Hubs, Azure IoT Hub, Dynamics 365, Skype for Business, and many core Azure services.</span></span>

<span data-ttu-id="5c6f9-115">Service Fabric 是針對建立雲端原生服務量身打造而成，此類服務可視需要以小規模開始，接著擴充為包含成千上萬個機器的大規模服務。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-115">Service Fabric is tailored to create cloud native services that can start small, as needed, and grow to massive scale with hundreds or thousands of machines.</span></span>

<span data-ttu-id="5c6f9-116">現今的網際網路級別服務是使用微服務建立。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-116">Today's Internet-scale services are built of microservices.</span></span> <span data-ttu-id="5c6f9-117">微服務範例包括通訊協定閘道器、使用者設定檔、購物車、清查處理、佇列和快取。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-117">Examples of microservices include protocol gateways, user profiles, shopping carts, inventory processing, queues, and caches.</span></span> <span data-ttu-id="5c6f9-118">Service Fabric 是一個微服務平台，為可以是無狀態或具狀態的每個微服務 (或容器) 都提供一個唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-118">Service Fabric is a microservices platform that gives every microservice (or container) a unique name that can be either stateless or stateful.</span></span>

<span data-ttu-id="5c6f9-119">Service Fabric 為由微服務組成的應用程式，提供完整的執行階段與生命週期管理功能。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-119">Service Fabric provides comprehensive runtime and lifecycle management capabilities to applications that are composed of these microservices.</span></span> <span data-ttu-id="5c6f9-120">其將微服務裝載在容器中，這些容器部署在整個 Service Fabric 叢集之中並已啟動。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-120">It hosts microservices inside containers that are deployed and activated across the Service Fabric cluster.</span></span> <span data-ttu-id="5c6f9-121">從虛擬機器改成用容器，可讓密度極為大幅地增加。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-121">A move from virtual machines to containers makes possible an order-of-magnitude increase in density.</span></span> <span data-ttu-id="5c6f9-122">同樣地，當您從容器移至這些容器中的微服務時，也可讓密度再提升一個量級。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-122">Similarly, another order of magnitude in density becomes possible when you move from containers to microservices in these containers.</span></span> <span data-ttu-id="5c6f9-123">例如，單一 Azure SQL Database 叢集是由數百個機器所組成，這些機器執行數萬個容器，而容器總共裝載了數十萬個資料庫。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-123">For example, a single cluster for Azure SQL Database comprises hundreds of machines running tens of thousands of containers that host a total of hundreds of thousands of databases.</span></span> <span data-ttu-id="5c6f9-124">每個資料庫都是 Service Fabric 的可設定狀態微服務。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-124">Each database is a Service Fabric stateful microservice.</span></span> 

<span data-ttu-id="5c6f9-125">如需有關微服務方法的詳細資訊，請閱讀 [為何要用微服務方式建置應用程式？](service-fabric-overview-microservices.md)</span><span class="sxs-lookup"><span data-stu-id="5c6f9-125">For more on the microservices approach, read [Why a microservices approach to building applications?](service-fabric-overview-microservices.md)</span></span>

## <a name="container-deployment-and-orchestration"></a><span data-ttu-id="5c6f9-126">容器部署和協調流程</span><span class="sxs-lookup"><span data-stu-id="5c6f9-126">Container deployment and orchestration</span></span>
<span data-ttu-id="5c6f9-127">Service Fabric 是將微服務部署至整個機器叢集的 Microsoft [容器協調者](service-fabric-cluster-resource-manager-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-127">Service Fabric is Microsoft's [container orchestrator](service-fabric-cluster-resource-manager-introduction.md) deploying microservices across a cluster of machines.</span></span> <span data-ttu-id="5c6f9-128">微服務的開發方式有許多種，從使用 [Service Fabric 程式設計模型](service-fabric-choose-framework.md)、[ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)，到部署[您選擇的任何程式碼](service-fabric-deploy-existing-app.md)，應有盡有。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-128">Microservices can be developed in many ways from using the [Service Fabric programming models](service-fabric-choose-framework.md), [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), to deploying [any code of your choice](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="5c6f9-129">重要的是，您可以在相同應用程式中同時混合容器中的服務和處理序中的服務。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-129">Importantly, you can mix both services in processes and services in containers in the same application.</span></span> <span data-ttu-id="5c6f9-130">如果您只是想要[部署和管理容器](service-fabric-containers-overview.md)，則 Service Fabric 作為容器協調者是一個最佳選擇。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-130">If you just want to [deploy and manage containers](service-fabric-containers-overview.md), Service Fabric is a perfect choice as a container orchestrator.</span></span>

## <a name="any-os-any-cloud"></a><span data-ttu-id="5c6f9-131">任何 OS、任何雲端</span><span class="sxs-lookup"><span data-stu-id="5c6f9-131">Any OS, any cloud</span></span>
<span data-ttu-id="5c6f9-132">Service Fabric 可在任何環境執行。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-132">Service Fabric runs everywhere.</span></span> <span data-ttu-id="5c6f9-133">您可以在許多環境 (包括 Azure 或內部部署、Windows Server 上或 Linux 上) 建立 Service Fabric 的叢集。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-133">You can create clusters for Service Fabric in many environments, including Azure or on premises, on Windows Server, or on Linux.</span></span> <span data-ttu-id="5c6f9-134">您甚至可以在其他公用雲端上建立叢集。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-134">You can even create clusters on other public clouds.</span></span> <span data-ttu-id="5c6f9-135">此外，SDK 中的開發環境與生產環境「完全相同」，不涉及任何模擬器。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-135">In addition, the development environment in the SDK is **identical** to the production environment, with no emulators involved.</span></span> <span data-ttu-id="5c6f9-136">換句話說，在本機開發叢集上執行的項目，也會部署到其他環境中的叢集。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-136">In other words, what runs on your local development cluster deploys to the clusters in other environments.</span></span>

![Service Fabric 平台][Image1]

<span data-ttu-id="5c6f9-138">如需建立叢集內部部署的詳細資訊，請參閱[在 Windows Server 或 Linux 上建立叢集](service-fabric-deploy-anywhere.md)，或是[透過 Azure 入口網站](service-fabric-cluster-creation-via-portal.md)針對 Azure 建立叢集。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-138">For more information on creating clusters on-premises, read [creating a cluster on Windows Server or Linux](service-fabric-deploy-anywhere.md) or for Azure creating a cluster [via the Azure portal](service-fabric-cluster-creation-via-portal.md).</span></span>

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a><span data-ttu-id="5c6f9-139">Service Fabric 的無狀態與具狀態微服務</span><span class="sxs-lookup"><span data-stu-id="5c6f9-139">Stateless and stateful microservices for Service Fabric</span></span>
<span data-ttu-id="5c6f9-140">Service Fabric 可讓您建置由微服務或容器組成的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-140">Service Fabric enables you to build applications that consist of microservices or containers.</span></span> <span data-ttu-id="5c6f9-141">無狀態微服務 (如通訊協定閘道器、Web Proxy) 不會維護要求之外的可變動狀態及來自服務的回應。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-141">Stateless microservices (such as protocol gateways and web proxies) do not maintain a mutable state outside a request and its response from the service.</span></span> <span data-ttu-id="5c6f9-142">Azure 雲端服務背景工作角色即為無狀態服務的範例。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-142">Azure Cloud Services worker roles are an example of a stateless service.</span></span> <span data-ttu-id="5c6f9-143">可設定狀態的微服務 (如使用者帳戶、資料庫、裝置、購物車、佇列) 會維護要求及其回應外的可變動授權狀態。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-143">Stateful microservices (such as user accounts, databases, devices, shopping carts, and queues) maintain a mutable, authoritative state beyond the request and its response.</span></span> <span data-ttu-id="5c6f9-144">現今的網際網路級別應用程式包含無狀態與可設定狀態微服務的組合。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-144">Today's Internet-scale applications consist of a combination of stateless and stateful microservices.</span></span> 

<span data-ttu-id="5c6f9-145">Service Fabric 的主要區別在於，它強烈著重在建置具狀態服務，不論是使用[內建的程式設計模型](service-fabric-choose-framework.md)，還是使用容器化具狀態服務來建置。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-145">A key differentation with Service Fabric is its strong focus on building stateful services, either with the [built-in programming models ](service-fabric-choose-framework.md) or with  containerized stateful services.</span></span> <span data-ttu-id="5c6f9-146">[應用程式案例](service-fabric-application-scenarios.md)說明使用具狀態服務的案例。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-146">The [application scenarios](service-fabric-application-scenarios.md) describe the scenarios where stateful services are used.</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="5c6f9-147">應用程式生命週期管理</span><span class="sxs-lookup"><span data-stu-id="5c6f9-147">Application lifecycle management</span></span>
<span data-ttu-id="5c6f9-148">Service Fabric 可支援雲端應用程式 (包括容器) 的完整應用程式生命週期和 CI/CD。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-148">Service Fabric provides support for the full application lifecycle and CI/CD of cloud applications including containers.</span></span> <span data-ttu-id="5c6f9-149">此生命週期包括開發到部署、每日管理、維護，到最終的解除委任。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-149">This lifecycle includes development through deployment, daily management, and maintenance to eventual decommissioning.</span></span>

<span data-ttu-id="5c6f9-150">Service Fabric 應用程式生命週期管理讓應用程式管理員和 IT 操作員能夠使用簡單、低接觸的工作流程來佈建、部署、修補與監視應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-150">Service Fabric application lifecycle management capabilities enable application administrators and IT operators to use simple, low-touch workflows to provision, deploy, patch, and monitor applications.</span></span> <span data-ttu-id="5c6f9-151">這些內建的工作流程能大幅降低 IT 操作員的負擔，讓應用程式持續可用。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-151">These built-in workflows greatly reduce the burden on IT operators to keep applications continuously available.</span></span>

<span data-ttu-id="5c6f9-152">大多數應用程式都是由無狀態和具狀態微服務、容器及其他一起部署之可執行檔的組合所構成。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-152">Most applications consist of a combination of stateless and stateful microservices, containers, and other executables that are deployed together.</span></span> <span data-ttu-id="5c6f9-153">Service Fabric 在應用程式擁有強式型別，因此能夠部署多個應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-153">By having strong types on the applications, Service Fabric enables the deployment of multiple application instances.</span></span> <span data-ttu-id="5c6f9-154">每個執行個體都能獨立管理與升級。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-154">Each instance is managed and upgraded independently.</span></span> <span data-ttu-id="5c6f9-155">重要的是，Service Fabric 可以部署容器或任何可執行檔，並讓它們都變得可靠。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-155">Importantly, Service Fabric can deploy containers or any executables and make them reliable.</span></span> <span data-ttu-id="5c6f9-156">例如，Service Fabric 可以部署 .NET、ASP.NET Core、node.js、Windows 容器、Linux 容器、Java 虛擬機器、指令碼、Angular 或實際上任何構成您應用程式的項目。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-156">For example, Service Fabric can deploy .NET, ASP.NET Core, node.js, Windows containers, Linux containers, Java virtual machines, scripts, Angular, or literally anything that makes up your application.</span></span>

<span data-ttu-id="5c6f9-157">Service Fabric 已與 CI/CD 工具 (例如 [Visual Studio Team Services](https://www.visualstudio.com/team-services/)、[Jenkins](https://jenkins.io/index.html) 及 [Octopus Deploy](https://octopus.com/)) 整合，並且可與任何其他常用的 CI/CD 工具搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-157">Service Fabric is integrated with CI/CD tools such as [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Jenkins](https://jenkins.io/index.html), and [Octopus Deploy](https://octopus.com/) and can be used with any other popular CI/CD tool.</span></span>

<span data-ttu-id="5c6f9-158">如需應用程式生命週期管理的詳細資訊，請參閱[應用程式生命週期](service-fabric-application-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-158">For more information about application lifecycle management, read [Application lifecycle](service-fabric-application-lifecycle.md).</span></span> <span data-ttu-id="5c6f9-159">如需有關如何部署任何程式碼的詳細資訊，請參閱[部署可體可執行檔](service-fabric-deploy-existing-app.md)。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-159">For more about how to deploy any code, see [deploy a guest executable](service-fabric-deploy-existing-app.md).</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="5c6f9-160">主要功能</span><span class="sxs-lookup"><span data-stu-id="5c6f9-160">Key capabilities</span></span>
<span data-ttu-id="5c6f9-161">藉由使用 Service Fabric，您可以：</span><span class="sxs-lookup"><span data-stu-id="5c6f9-161">By using Service Fabric, you can:</span></span>

* <span data-ttu-id="5c6f9-162">部署至 Azure，或部署至執行 Windows 或 Linux 的內部部署資料中心，且程式碼零變更。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-162">Deploy to Azure or to on-premises datacenters that run Windows or Linux with zero code changes.</span></span> <span data-ttu-id="5c6f9-163">只要撰寫一次，就能夠在任何地方部署至任何 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-163">Write once, and then deploy anywhere to any Service Fabric cluster.</span></span>
* <span data-ttu-id="5c6f9-164">使用 Service Fabric 程式設計模型、容器或任何程式碼，來開發由微服務所組成的可調整應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-164">Develop scalable applications that are composed of microservices by using the Service Fabric programming models, containers, or any code.</span></span>
* <span data-ttu-id="5c6f9-165">開發高度可靠的無狀態與可設定狀態微服務。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-165">Develop highly reliable stateless and stateful microservices.</span></span> <span data-ttu-id="5c6f9-166">使用具狀態微服務來簡化應用程式的設計。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-166">Simplify the design of your application by using stateful microservices.</span></span> 
* <span data-ttu-id="5c6f9-167">使用新奇的 Reliable Actors 程式設計模型，來建立具有獨立性程式碼與狀態的雲端物件。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-167">Use the novel Reliable Actors programming model to create cloud objects with self contained code and state.</span></span>
* <span data-ttu-id="5c6f9-168">部署並協調包含 Windows 容器和 Linux 容器的容器。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-168">Deploy and orchestrate containers that include Windows containers and Linux containers.</span></span> <span data-ttu-id="5c6f9-169">Service Fabric 是一個資料感知、具狀態的容器協調者。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-169">Service Fabric is a data aware, stateful, container orchestrator.</span></span>
* <span data-ttu-id="5c6f9-170">以每部機器上數百或數千個應用程式或容器的高密度方式，快速部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-170">Deploy applications in seconds, at high density with hundreds or thousands of applications or containers per machine.</span></span>
* <span data-ttu-id="5c6f9-171">並列部署相同應用程式的不同版本，並獨立升級每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-171">Deploy different versions of the same application side by side, and upgrade each application independently.</span></span>
* <span data-ttu-id="5c6f9-172">無須停機即可管理應用程式的生命週期，包括重大升級與非重大升級。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-172">Manage the lifecycle of your applications without any downtime, including breaking and nonbreaking upgrades.</span></span>
* <span data-ttu-id="5c6f9-173">相應放大或相應縮小叢集中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-173">Scale out or scale in the number of nodes in a cluster.</span></span> <span data-ttu-id="5c6f9-174">隨著您調整節點，應用程式也會自動調整。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-174">As you scale nodes, your applications automatically scale.</span></span>
* <span data-ttu-id="5c6f9-175">監視和診斷應用程式的健全狀況，並設定用來執行自動修復的原則。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-175">Monitor and diagnose the health of your applications and set policies for performing automatic repairs.</span></span>
* <span data-ttu-id="5c6f9-176">監看資源平衡器協調整個叢集的應用程式重新分配。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-176">Watch the resource balancer orchestrate the redistribution of applications across the cluster.</span></span> <span data-ttu-id="5c6f9-177">Service Fabric 會從失敗中復原，並會根據可用資源將負載分佈最佳化。</span><span class="sxs-lookup"><span data-stu-id="5c6f9-177">Service Fabric recovers from failures and optimizes the distribution of load based on available resources.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="5c6f9-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c6f9-178">Next steps</span></span>
* <span data-ttu-id="5c6f9-179">其他資訊：</span><span class="sxs-lookup"><span data-stu-id="5c6f9-179">For more information:</span></span>
  * [<span data-ttu-id="5c6f9-180">為何要用微服務方式建置應用程式？</span><span class="sxs-lookup"><span data-stu-id="5c6f9-180">Why a microservices approach to building applications?</span></span>](service-fabric-overview-microservices.md)
  * [<span data-ttu-id="5c6f9-181">術語概觀</span><span class="sxs-lookup"><span data-stu-id="5c6f9-181">Terminology overview</span></span>](service-fabric-technical-overview.md)
* <span data-ttu-id="5c6f9-182">設定 Service Fabric [開發環境](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="5c6f9-182">Setting up your Service Fabric [development environment](service-fabric-get-started.md)</span></span>  
* <span data-ttu-id="5c6f9-183">了解 [Service Fabric 支援選項](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="5c6f9-183">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png