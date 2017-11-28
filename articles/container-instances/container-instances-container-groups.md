---
title: "Azure Container Instances 容器群組"
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
ms.openlocfilehash: 25eab41c3f0c986bcce33123f86f4c9638b77191
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="7163d-103">Azure Container Instances 中的容器群組</span><span class="sxs-lookup"><span data-stu-id="7163d-103">Container Groups in Azure Container Instances</span></span>

<span data-ttu-id="7163d-104">在 Azure Container Instances 中，最上層的資源就是容器群組。</span><span class="sxs-lookup"><span data-stu-id="7163d-104">The top-level resource in Azure Container Instances is a container group.</span></span> <span data-ttu-id="7163d-105">本文說明容器群組為何，以及這些群組能夠實現哪些類型的案例。</span><span class="sxs-lookup"><span data-stu-id="7163d-105">This article describes what container groups are and what types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="7163d-106">容器群組的運作方式</span><span class="sxs-lookup"><span data-stu-id="7163d-106">How a container group works</span></span>

<span data-ttu-id="7163d-107">容器群組是容器的集合，這些容器會排程在相同的主機電腦上，並共用生命週期、區域網路和存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7163d-107">A container group is a collection of containers that get scheduled on the same host machine and share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="7163d-108">容器群組類似於 [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) 和 [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/) 中的 *Pod* 概念。</span><span class="sxs-lookup"><span data-stu-id="7163d-108">It is similar to the concept of a *pod* in [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).</span></span>

<span data-ttu-id="7163d-109">下圖舉例說明包含多個容器的容器群組。</span><span class="sxs-lookup"><span data-stu-id="7163d-109">The following diagram shows an example of a container group that includes multiple containers.</span></span>

![容器群組範例][container-groups-example]

<span data-ttu-id="7163d-111">請注意：</span><span class="sxs-lookup"><span data-stu-id="7163d-111">Note that:</span></span>

- <span data-ttu-id="7163d-112">此群組排程在單一主機電腦上。</span><span class="sxs-lookup"><span data-stu-id="7163d-112">The group is scheduled on a single host machine.</span></span>
- <span data-ttu-id="7163d-113">此群組會公開單一的公用 IP 位址，以及一個公開的連接埠。</span><span class="sxs-lookup"><span data-stu-id="7163d-113">The group exposes a single public IP address, with one exposed port.</span></span>
- <span data-ttu-id="7163d-114">此群組是由兩個容器所組成。</span><span class="sxs-lookup"><span data-stu-id="7163d-114">The group is made up of two containers.</span></span> <span data-ttu-id="7163d-115">一個容器接聽連接埠 80，另一個容器接聽連接埠 5000。</span><span class="sxs-lookup"><span data-stu-id="7163d-115">One container listens on port 80, while the other listens on port 5000.</span></span>
- <span data-ttu-id="7163d-116">此群組包含兩個 Azure 檔案共用來作為磁碟區掛接，而且每個容器會在本機掛接其中一個共用。</span><span class="sxs-lookup"><span data-stu-id="7163d-116">The group includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

### <a name="networking"></a><span data-ttu-id="7163d-117">網路</span><span class="sxs-lookup"><span data-stu-id="7163d-117">Networking</span></span>

<span data-ttu-id="7163d-118">容器群組會共用 IP 位址以及該 IP 位址上的連接埠命名空間。</span><span class="sxs-lookup"><span data-stu-id="7163d-118">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="7163d-119">若要讓外部用戶端能夠連線到該群組內的容器，您必須從該容器公開該 IP 位址上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="7163d-119">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="7163d-120">群組內的容器會共用連接埠命名空間，因此不支援連接埠對應。</span><span class="sxs-lookup"><span data-stu-id="7163d-120">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="7163d-121">群組內的容器可以在它們已公開的連接埠上透過 localhost 彼此連線，即使這些連接埠並未在群組的 IP 位址上對外公開也是如此。</span><span class="sxs-lookup"><span data-stu-id="7163d-121">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

### <a name="storage"></a><span data-ttu-id="7163d-122">儲存體</span><span class="sxs-lookup"><span data-stu-id="7163d-122">Storage</span></span>

<span data-ttu-id="7163d-123">您可以指定要在容器群組內掛接的外部磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7163d-123">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="7163d-124">您可以將這些磁碟區對應到群組之個別容器內的特定路徑。</span><span class="sxs-lookup"><span data-stu-id="7163d-124">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="7163d-125">常見案例</span><span class="sxs-lookup"><span data-stu-id="7163d-125">Common scenarios</span></span>

<span data-ttu-id="7163d-126">如果您想要將單一功能的工作分割成少量的容器映像，以便由不同小組來提供並讓這些映像具有不同的資源需求，則多個容器的群組會很實用。</span><span class="sxs-lookup"><span data-stu-id="7163d-126">Multi-container groups are useful in cases where you want to divide up a single functional task into a small number of container images, which can be delivered by different teams and have separate resource requirements.</span></span> <span data-ttu-id="7163d-127">使用範例可能包括：</span><span class="sxs-lookup"><span data-stu-id="7163d-127">Example usage could include:</span></span>

- <span data-ttu-id="7163d-128">一個應用程式容器和一個記錄容器。</span><span class="sxs-lookup"><span data-stu-id="7163d-128">An application container and a logging container.</span></span> <span data-ttu-id="7163d-129">記錄容器收集主應用程式所輸出的記錄和計量，並將這些資料寫入到長期存放區。</span><span class="sxs-lookup"><span data-stu-id="7163d-129">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
- <span data-ttu-id="7163d-130">一個應用程式和一個監視容器。</span><span class="sxs-lookup"><span data-stu-id="7163d-130">An application and a monitoring container.</span></span> <span data-ttu-id="7163d-131">監視容器會定期地向應用程式發出要求，以確保它會保持執行狀態並正確回應，如果沒有正確回應則引發警示。</span><span class="sxs-lookup"><span data-stu-id="7163d-131">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly and raises an alert if it's not.</span></span>
- <span data-ttu-id="7163d-132">一個容器提供 Web 應用程式，一個容器從原始檔控制提取最新內容。</span><span class="sxs-lookup"><span data-stu-id="7163d-132">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7163d-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7163d-133">Next steps</span></span>

<span data-ttu-id="7163d-134">了解如何使用 Azure Resource Manager 範本來[部署多個容器的群組](container-instances-multi-container-group.md)。</span><span class="sxs-lookup"><span data-stu-id="7163d-134">Learn how to [deploy a multi-container group](container-instances-multi-container-group.md) with an Azure Resource Manager template.</span></span>

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png