---
title: "Azure 容器執行個體和容器協調流程"
description: "了解 Azure 容器執行個體與容器 Orchestrator 的互動方式"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cbb558a92d565759c8dc7d2693960955eb053b0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="7d174-103">Azure 容器執行個體和容器 Orchestrator</span><span class="sxs-lookup"><span data-stu-id="7d174-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="7d174-104">由於規模較小和應用程式方向的緣故，容器很適合用於敏捷式傳遞環境和微服務式架構。</span><span class="sxs-lookup"><span data-stu-id="7d174-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="7d174-105">自動執行和管理大量容器以及其互動方式的工作稱為「協調流程」。</span><span class="sxs-lookup"><span data-stu-id="7d174-105">The task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="7d174-106">熱門的容器 Orchestrator (包括 Kubernetes、DC/OS 和 Docker Swarm) 全都可在 [Azure Container Service](https://docs.microsoft.com/azure/container-service/) 中取得。</span><span class="sxs-lookup"><span data-stu-id="7d174-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="7d174-107">Azure 容器執行個體提供了一些基本的協調流程平台排程功能，但它並未涵蓋這些平台所提供的較高價值服務，因此事實上可與這些平台互補。</span><span class="sxs-lookup"><span data-stu-id="7d174-107">Azure Container Instances provides some of the basic scheduling capabilities of orchestration platforms, but it does not cover the higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="7d174-108">本文說明 Azure 容器執行個體所能處理的項目範圍，以及完整的容器 Orchestrator 如何與其互動。</span><span class="sxs-lookup"><span data-stu-id="7d174-108">This article describes the scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="7d174-109">傳統協調流程</span><span class="sxs-lookup"><span data-stu-id="7d174-109">Traditional orchestration</span></span>

<span data-ttu-id="7d174-110">協調流程的標準定義包含下列工作：</span><span class="sxs-lookup"><span data-stu-id="7d174-110">The standard definition of orchestration includes the following tasks:</span></span>

- <span data-ttu-id="7d174-111">**排程**：在給定容器映像和資源要求的情況下，尋找適合用來執行容器的電腦。</span><span class="sxs-lookup"><span data-stu-id="7d174-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which to run the container.</span></span>
- <span data-ttu-id="7d174-112">**親和性/反親和性**：指定一組容器應該在彼此附近執行 (以獲取效能) 或是彼此離得夠遠來執行 (以獲得可用性)。</span><span class="sxs-lookup"><span data-stu-id="7d174-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="7d174-113">**健康情況監視**：監視容器的失敗，並自動為容器重新排程。</span><span class="sxs-lookup"><span data-stu-id="7d174-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="7d174-114">**容錯移轉**：追蹤每部電腦上執行的項目，並將容器從失敗的電腦重新排程到狀況良好的節點。</span><span class="sxs-lookup"><span data-stu-id="7d174-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines to healthy nodes.</span></span>
- <span data-ttu-id="7d174-115">**調整**：以手動或自動方式新增或移除容器執行個體以符合需求。</span><span class="sxs-lookup"><span data-stu-id="7d174-115">**Scaling**: Add or remove container instances to match demand, either manually or automatically.</span></span>
- <span data-ttu-id="7d174-116">**網路**：提供重疊的網路以協調容器，讓它們跨越多部主機電腦彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="7d174-116">**Networking**: Provide an overlay network for coordinating containers to communicate across multiple host machines.</span></span>
- <span data-ttu-id="7d174-117">**服務探索**：讓容器可以自動找到彼此，即使它們移到不同的主機電腦和變更 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7d174-117">**Service discovery**: Enable containers to locate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="7d174-118">**協調的應用程式升級**：管理容器的升級以避免應用程式停機，並可在發生錯誤時復原。</span><span class="sxs-lookup"><span data-stu-id="7d174-118">**Coordinated application upgrades**: Manage container upgrades to avoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="7d174-119">使用 Azure 容器執行個體的協調流程：分層式方法</span><span class="sxs-lookup"><span data-stu-id="7d174-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="7d174-120">Azure 容器執行個體可提供分層式協調流程方法，提供執行單一容器所需的所有排程和管理功能，同時讓 Orchestrator 平台管理在其上執行的多個容器工作。</span><span class="sxs-lookup"><span data-stu-id="7d174-120">Azure Container Instances enables a layered approach to orchestration, providing all of the scheduling and management capabilities required to run a single container, while allowing orchestrator platforms to manage multi-container tasks on top of it.</span></span>

<span data-ttu-id="7d174-121">容器執行個體的所有基礎結構皆由 Azure 負責管理，因此 Orchestrator 平台本身不需要擔心如何尋找用來執行單一容器的適當主機電腦。</span><span class="sxs-lookup"><span data-stu-id="7d174-121">Because all of the underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need to concern itself with finding an appropriate host machine on which to run a single container.</span></span> <span data-ttu-id="7d174-122">雲端的彈性可確保永遠有適當的主機電腦可供使用。</span><span class="sxs-lookup"><span data-stu-id="7d174-122">The elasticity of the cloud ensures that one is always available.</span></span> <span data-ttu-id="7d174-123">相反地，Orchestrator 可以專注於簡化多容器架構開發的工作，包括調整作業與協調的升級。</span><span class="sxs-lookup"><span data-stu-id="7d174-123">Instead, the orchestrator can focus on the tasks that simplify the development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="7d174-124">可能的案例</span><span class="sxs-lookup"><span data-stu-id="7d174-124">Potential scenarios</span></span>

<span data-ttu-id="7d174-125">雖然 Orchestrator 與 Azure 容器執行個體的整合技術仍未成熟，但我們預期可能會出現幾個不同的環境：</span><span class="sxs-lookup"><span data-stu-id="7d174-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="7d174-126">獨佔的容器執行個體協調流程</span><span class="sxs-lookup"><span data-stu-id="7d174-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="7d174-127">因為這些執行個體啟動速度快且依秒計費，以獨佔方式立基於 Azure 容器執行個體的環境可提供最快的方法來開始使用，並處理高度變化的工作負載。</span><span class="sxs-lookup"><span data-stu-id="7d174-127">Because they start quickly and bill by the second, an environment based exclusively on Azure Container Instances offers the fastest way to get started and to deal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="7d174-128">結合容器執行個體和虛擬機器中的容器</span><span class="sxs-lookup"><span data-stu-id="7d174-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="7d174-129">針對長時間執行的穩定工作負載，協調專用虛擬機器叢集中的容器所需的成本，一般會比使用容器執行個體來執行相同容器還低。</span><span class="sxs-lookup"><span data-stu-id="7d174-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running the same containers with Container Instances.</span></span> <span data-ttu-id="7d174-130">不過，容器執行個體能提供絕佳的解決方案來快速擴展和收縮整體容量，以處理未預期的使用量或短暫出現的高峰使用量。</span><span class="sxs-lookup"><span data-stu-id="7d174-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity to deal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="7d174-131">Orchestrator 可以直接排程使用容器執行個體的其他容器，並在不再需要時加以刪除，而不是相應放大叢集中的虛擬機器數目，然後將其他容器部署到這些電腦。</span><span class="sxs-lookup"><span data-stu-id="7d174-131">Rather than scaling out the number of virtual machines in your cluster, then deploying additional containers onto those machines, the orchestrator can simply schedule the additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="7d174-132">實作範例：Kubernetes 的 Azure 容器執行個體連接器</span><span class="sxs-lookup"><span data-stu-id="7d174-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="7d174-133">為了示範容器協調流程平台如何與 Azure 容器執行個體整合，我們已開始建置 [Kubernetes 的連接器範例][aci-connector-k8s]。</span><span class="sxs-lookup"><span data-stu-id="7d174-133">To demonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="7d174-134">Kubernetes 的連接器會模擬 [kubelet][kubelet-doc]，方法是註冊為具有無限容量的節點，並將 [Pod][pod-doc] 的建立分派為 Azure 容器執行個體中的容器群組。</span><span class="sxs-lookup"><span data-stu-id="7d174-134">The connector for Kubernetes mimics the [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching the creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="7d174-135">其他 Orchestrator 的連接器可以同樣方式建置來與平台基本項目整合，以結合 Orchestrator API 的能力與在 Azure 容器執行個體中管理容器的速度和簡便性。</span><span class="sxs-lookup"><span data-stu-id="7d174-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives to combine the power of the orchestrator API with the speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="7d174-136">Kubernetes 的 ACI 連接器是「實驗性的」，不應用在生產環境中。</span><span class="sxs-lookup"><span data-stu-id="7d174-136">The ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d174-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d174-137">Next steps</span></span>

<span data-ttu-id="7d174-138">使用[快速入門指南](container-instances-quickstart.md)對 Azure 容器執行個體建立您的第一個容器。</span><span class="sxs-lookup"><span data-stu-id="7d174-138">Create your first container with Azure Container Instances using the [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/