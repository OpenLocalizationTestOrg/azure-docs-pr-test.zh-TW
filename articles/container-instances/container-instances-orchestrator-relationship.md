---
title: "aaaAzure 容器執行個體和容器協調流程"
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
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="f0ccc-103">Azure 容器執行個體和容器 Orchestrator</span><span class="sxs-lookup"><span data-stu-id="f0ccc-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="f0ccc-104">由於規模較小和應用程式方向的緣故，容器很適合用於敏捷式傳遞環境和微服務式架構。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="f0ccc-105">自動化及管理大量的容器，以及它們如何互動的 hello 工作即稱為*協調流程*。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="f0ccc-106">熱門容器 orchestrators 包括 Kubernetes、 DC/OS，和 Docker Swarm，均可取得 hello [Azure 容器服務](https://docs.microsoft.com/azure/container-service/)。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="f0ccc-107">Azure 容器執行個體提供了一些 hello 基本排程的協調流程的平台功能，但並未涵蓋這些平台提供，實際上為互補與其 hello 高價值服務。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="f0ccc-108">本文說明 hello Azure 容器執行個體的處理，並與其互動容器 orchestrators 可能會填滿範圍。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="f0ccc-109">傳統協調流程</span><span class="sxs-lookup"><span data-stu-id="f0ccc-109">Traditional orchestration</span></span>

<span data-ttu-id="f0ccc-110">hello 的協調流程的標準定義包括 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="f0ccc-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="f0ccc-111">**排程**： 指定的容器映像和資源要求，尋找哪些 toorun hello 容器上的適當電腦。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="f0ccc-112">**親和性/反親和性**：指定一組容器應該在彼此附近執行 (以獲取效能) 或是彼此離得夠遠來執行 (以獲得可用性)。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="f0ccc-113">**健康情況監視**：監視容器的失敗，並自動為容器重新排程。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="f0ccc-114">**容錯移轉**： 每部機器上執行的項目追蹤的重新排程要從失敗的機器 toohealthy 節點的容器。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="f0ccc-115">**調整**： 新增或移除容器執行個體 toomatch 視需要手動或自動。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="f0ccc-116">**網路**： 提供的重疊網路容器 toocommunicate 協調跨越多部主機電腦。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="f0ccc-117">**服務探索**： 容器 toolocate 彼此會自動啟用視為即使主機電腦之間移動，而且變更 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="f0ccc-118">**協調應用程式升級**： 管理容器升級 tooavoid 應用程式停機時間，以及如果發生問題時啟用回復。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="f0ccc-119">使用 Azure 容器執行個體的協調流程：分層式方法</span><span class="sxs-lookup"><span data-stu-id="f0ccc-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="f0ccc-120">Azure 容器執行個體啟用的分層的方式 tooorchestration，提供所有 hello 排程和管理功能時，需要 toorun 單一容器中，允許 orchestrator 平台 toomanage 多容器工作，其最上層。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="f0ccc-121">因為所有基礎容器執行個體的基礎結構的 hello Azure 所管理，orchestrator 平台不需要與單一容器尋找適當的主機上的機器哪些 toorun tooconcern 本身。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="f0ccc-122">hello 雲端的 hello 彈性可確保一永遠可用。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="f0ccc-123">相反地，hello orchestrator 可以專注於簡化多容器架構，包括縮放比例和協調的升級 hello 開發的 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="f0ccc-124">可能的案例</span><span class="sxs-lookup"><span data-stu-id="f0ccc-124">Potential scenarios</span></span>

<span data-ttu-id="f0ccc-125">雖然 Orchestrator 與 Azure 容器執行個體的整合技術仍未成熟，但我們預期可能會出現幾個不同的環境：</span><span class="sxs-lookup"><span data-stu-id="f0ccc-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="f0ccc-126">獨佔的容器執行個體協調流程</span><span class="sxs-lookup"><span data-stu-id="f0ccc-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="f0ccc-127">因為他們快速地啟動，並由 hello 開立其帳單的第二個，以獨佔方式基礎環境 Azure 容器執行個體提供最快方式 tooget hello 啟動和 toodeal 很大的不同的工作負載。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="f0ccc-128">結合容器執行個體和虛擬機器中的容器</span><span class="sxs-lookup"><span data-stu-id="f0ccc-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="f0ccc-129">長時間執行的穩定工作負載，來協調容器在叢集中的專用虛擬機器通常會是成本比執行中的 hello 相同容器與容器的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="f0ccc-130">不過，容器執行個體提供快速擴展和收縮具有未預期的或存留較短使用量高峰您整體容量 toodeal 的最佳解決方案。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="f0ccc-131">而不是擴充的虛擬機器在叢集中的 hello 數目，則部署到這些電腦的其他容器，hello orchestrator 可以只是排程 hello 使用容器執行個體的其他容器，然後刪除它們，當它們沒有不再需要。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="f0ccc-132">實作範例：Kubernetes 的 Azure 容器執行個體連接器</span><span class="sxs-lookup"><span data-stu-id="f0ccc-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="f0ccc-133">toodemonstrate 容器協調流程平台如何整合 Azure 容器執行個體，我們已開始建置[Kubernetes 範例連接器][aci-connector-k8s]。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="f0ccc-134">針對 Kubernetes 模擬 hello hello 連接器[kubelet] [ kubelet-doc]做為節點向無限制的空間，並分派 hello 建立[pod] [pod-doc] Azure 容器執行個體中的容器群組。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="f0ccc-135">其他 orchestrators 連接器無法建立同樣的整合平台基本型別 toocombine hello 電源的 hello orchestrator API hello 速度和簡化管理 Azure 容器執行個體中的容器。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="f0ccc-136">hello ACI 連接器 Kubernetes 是*實驗*不應在生產環境中使用。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0ccc-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0ccc-137">Next steps</span></span>

<span data-ttu-id="f0ccc-138">您的第一個容器建立 Azure 容器使用與執行個體 hello[快速入門指南](container-instances-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="f0ccc-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/