---
title: "aaaAzure 容器執行個體容器群組"
description: "了解容器群組在 Azure Container Instances 中的運作方式"
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
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="f7180-103">Azure Container Instances 中的容器群組</span><span class="sxs-lookup"><span data-stu-id="f7180-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="f7180-104">hello Azure 容器執行個體中的最上層資源是容器群組。</span><span class="sxs-lookup"><span data-stu-id="f7180-104">hello top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="f7180-105">本文說明容器群組為何，以及這些群組能夠實現哪些類型的案例。</span><span class="sxs-lookup"><span data-stu-id="f7180-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="f7180-106">容器群組的運作方式</span><span class="sxs-lookup"><span data-stu-id="f7180-106">How a container group works</span></span>

<span data-ttu-id="f7180-107">容器群組是集合的 hello 取得排程的容器相同的主機電腦和共用的生命週期、 區域網路和存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f7180-107">A container group is a collection of containers that get scheduled on hello same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="f7180-108">它是類似 toohello 概念的*pod*中[Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/)和[DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/)。</span><span class="sxs-lookup"><span data-stu-id="f7180-108">It is similar toohello concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="f7180-109">hello 下圖顯示包含多個容器的容器群組的範例。</span><span class="sxs-lookup"><span data-stu-id="f7180-109">hello following diagram shows an example of a container group that includes multiple containers.</span></span>

![容器群組範例][container-groups-example]

<span data-ttu-id="f7180-111">請注意：</span><span class="sxs-lookup"><span data-stu-id="f7180-111">Note that:</span></span>

- <span data-ttu-id="f7180-112">hello 群組會排定在單一主機上。</span><span class="sxs-lookup"><span data-stu-id="f7180-112">hello group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="f7180-113">hello 群組會公開單一公用 IP 位址，與一個公開的連接埠。</span><span class="sxs-lookup"><span data-stu-id="f7180-113">hello group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="f7180-114">hello 群組是由兩個容器所組成。</span><span class="sxs-lookup"><span data-stu-id="f7180-114">hello group is made up of two containers.</span></span> <span data-ttu-id="f7180-115">一個容器會接聽通訊埠 80，而其他 hello 接聽通訊埠 5000。</span><span class="sxs-lookup"><span data-stu-id="f7180-115">One container listens on port 80, while hello other listens on port 5000.</span></span>
- <span data-ttu-id="f7180-116">hello 群組包含兩個 Azure 檔案共用做為磁碟區掛接，而且每個容器裝載其中一個本機 hello 共用。</span><span class="sxs-lookup"><span data-stu-id="f7180-116">hello group includes two Azure file shares as volume mounts, and each container mounts one of hello shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="f7180-117">網路</span><span class="sxs-lookup"><span data-stu-id="f7180-117">Networking</span></span>

<span data-ttu-id="f7180-118">容器群組會共用 IP 位址以及該 IP 位址上的連接埠命名空間。</span><span class="sxs-lookup"><span data-stu-id="f7180-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="f7180-119">tooenable 外部用戶端 tooreach hello 群組內的容器，您必須公開 hello IP 位址和 hello 容器中的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="f7180-119">tooenable external clients tooreach a container within hello group, you must expose hello port on hello IP address and from hello container.</span></span> <span data-ttu-id="f7180-120">因為 hello 群組內的容器共用連接埠的命名空間，所以不支援連接埠對應。</span><span class="sxs-lookup"><span data-stu-id="f7180-120">Because containers within hello group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="f7180-121">群組內的容器可以連線到彼此上 hello localhost 透過它們公開的連接埠即使這些連接埠不會公開外部 hello 群組的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f7180-121">Containers within a group can reach each other via localhost on hello ports that they have exposed, even if those ports are not exposed externally on hello group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="f7180-122">儲存體</span><span class="sxs-lookup"><span data-stu-id="f7180-122">Storage</span></span>

<span data-ttu-id="f7180-123">您可以指定外部磁碟區 toomount 容器群組內。</span><span class="sxs-lookup"><span data-stu-id="f7180-123">You can specify external volumes toomount within a container group.</span></span> <span data-ttu-id="f7180-124">您可以將這些磁碟區對應到特定群組中的 hello 個別容器內的路徑。</span><span class="sxs-lookup"><span data-stu-id="f7180-124">You can map those volumes into specific paths within hello individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="f7180-125">常見案例</span><span class="sxs-lookup"><span data-stu-id="f7180-125">Common scenarios</span></span>

<span data-ttu-id="f7180-126">多個容器群組是在您想 toodivide 組成的單一功能的工作到容器映像，也可以由不同小組傳遞，有不同的資源需求數少的情況下很有用。</span><span class="sxs-lookup"><span data-stu-id="f7180-126">Multi-container groups are useful in cases where you want toodivide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="f7180-127">使用範例可能包括：</span><span class="sxs-lookup"><span data-stu-id="f7180-127">Example usage could include:</span></span>

- <span data-ttu-id="f7180-128">一個應用程式容器和一個記錄容器。</span><span class="sxs-lookup"><span data-stu-id="f7180-128">An application container and a logging container.</span></span> <span data-ttu-id="f7180-129">hello 記錄容器會收集 hello 記錄和度量輸出 hello 主應用程式，並將其寫入 toolong 長期的儲存體。</span><span class="sxs-lookup"><span data-stu-id="f7180-129">hello logging container collects hello logs and metrics output by hello main application and writes them toolong-term storage.</span></span>
- <span data-ttu-id="f7180-130">一個應用程式和一個監視容器。</span><span class="sxs-lookup"><span data-stu-id="f7180-130">An application and a monitoring container.</span></span> <span data-ttu-id="f7180-131">定期監視容器 hello 可讓要求 toohello 應用程式 tooensure 它正在執行，並正確回應，並引發警示，如果不是。</span><span class="sxs-lookup"><span data-stu-id="f7180-131">hello monitoring container periodically makes a request toohello application tooensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="f7180-132">處理 web 應用程式的容器和容器提取 hello 從原始檔控制的最新內容。</span><span class="sxs-lookup"><span data-stu-id="f7180-132">A container serving a web application and a container pulling hello latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7180-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7180-133">Next steps</span></span>

<span data-ttu-id="f7180-134">了解如何太[部署多個容器群組](container-instances-multi-container-group.md)與 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="f7180-134">Learn how too[deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png