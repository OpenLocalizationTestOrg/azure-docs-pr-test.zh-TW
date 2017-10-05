---
title: "Azure Container Service 的 DC/OS 代理程式集區 | Microsoft Docs"
description: "公用和私用代理程式集區如何與 Azure Container Service DC/OS 叢集搭配運作"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: da4a196b1a73c78dfff7d8310edcc349b8d10665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="878d0-104">Azure Container Service 的 DC/OS 代理程式集區</span><span class="sxs-lookup"><span data-stu-id="878d0-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="878d0-105">Azure Container Service 中的 DC/OS 叢集包含兩個集區中的代理程式節點，即公用集區和私用集區。</span><span class="sxs-lookup"><span data-stu-id="878d0-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="878d0-106">您可以將應用程式部署到其中任一集區，以影響容器服務中電腦之間的存取性。</span><span class="sxs-lookup"><span data-stu-id="878d0-106">An application can be deployed to either pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="878d0-107">電腦可以公開至網際網路 (公用) 或保留在內部 (私用)。</span><span class="sxs-lookup"><span data-stu-id="878d0-107">The machines can be exposed to the internet (public) or kept internal (private).</span></span> <span data-ttu-id="878d0-108">本文簡短概述為什麼會有公用集區和私用集區。</span><span class="sxs-lookup"><span data-stu-id="878d0-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="878d0-109">**私用代理程式**：私用代理程式節點會透過非可路由網路來執行。</span><span class="sxs-lookup"><span data-stu-id="878d0-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="878d0-110">只有從系統管理區域或透過公用區域邊緣路由器才可存取此網路。</span><span class="sxs-lookup"><span data-stu-id="878d0-110">This network is only accessible from the admin zone or through the public zone edge router.</span></span> <span data-ttu-id="878d0-111">根據預設，DC/OS 會在私用代理程式節點上啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="878d0-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="878d0-112">**公用代理程式**：公用代理程式節點會透過可公開存取的網路執行 DC/OS 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="878d0-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="878d0-113">如需有關 DC/OS 網路安全性的詳細資訊，請參閱 [DC/OS 文件](https://dcos.io/docs/1.7/administration/securing-your-cluster/)。</span><span class="sxs-lookup"><span data-stu-id="878d0-113">For more information about DC/OS network security, see the [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="878d0-114">部署代理程式集區</span><span class="sxs-lookup"><span data-stu-id="878d0-114">Deploy agent pools</span></span>

<span data-ttu-id="878d0-115">Azure Container Service 中的 DC/OS 代理程式集區會以下列方式建立：</span><span class="sxs-lookup"><span data-stu-id="878d0-115">The DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="878d0-116">「私用集區」包含您[部署 DC/OS 叢集](container-service-deployment.md)時所指定數目的代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="878d0-116">The **private pool** contains the number of agent nodes that you specify when you [deploy the DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="878d0-117">「公用集區」一開始會包含所預先決定數目的代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="878d0-117">The **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="878d0-118">佈建 DC/OS 叢集時會自動新增此集區。</span><span class="sxs-lookup"><span data-stu-id="878d0-118">This pool is added automatically when the DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="878d0-119">私用集區和公用集區是 Azure 虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="878d0-119">The private pool and the public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="878d0-120">您可以在部署後調整這些集區的大小。</span><span class="sxs-lookup"><span data-stu-id="878d0-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="878d0-121">使用代理程式集區</span><span class="sxs-lookup"><span data-stu-id="878d0-121">Use agent pools</span></span>
<span data-ttu-id="878d0-122">根據預設，**Marathon** 會將任何新的應用程式部署至*私用*代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="878d0-122">By default, **Marathon** deploys any new application to the *private* agent nodes.</span></span> <span data-ttu-id="878d0-123">您必須在建立應用程式時，明確地將應用程式部署到「公用」節點。</span><span class="sxs-lookup"><span data-stu-id="878d0-123">You have to explicitly deploy the application to the *public* nodes during the creation of the application.</span></span> <span data-ttu-id="878d0-124">選取 [選用] 索引標籤，然後輸入 **slave_public** 做為 [接受的資源角色] 值。</span><span class="sxs-lookup"><span data-stu-id="878d0-124">Select the **Optional** tab and enter **slave_public** for the **Accepted Resource Roles** value.</span></span> <span data-ttu-id="878d0-125">[這裡](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container)和 [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) 文件中皆有此程序的記載。</span><span class="sxs-lookup"><span data-stu-id="878d0-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in the [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="878d0-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="878d0-126">Next steps</span></span>
* <span data-ttu-id="878d0-127">深入了解如何[管理 DC/OS 容器](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="878d0-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="878d0-128">了解如何[開啟 Azure 所提供的防火牆](container-service-enable-public-access.md)以允許公開存取您的 DC/OS 容器。</span><span class="sxs-lookup"><span data-stu-id="878d0-128">Learn how to [open the firewall](container-service-enable-public-access.md) provided by Azure to allow public access to your DC/OS containers.</span></span>

