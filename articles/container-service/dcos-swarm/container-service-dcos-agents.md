---
title: "Azure 容器服務 aaaDC/OS 代理程式集區 |Microsoft 文件"
description: "Hello 公用和私用的代理程式集區與 Azure 容器服務 DC/OS 叢集的運作方式"
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
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a><span data-ttu-id="608b2-104">Azure Container Service 的 DC/OS 代理程式集區</span><span class="sxs-lookup"><span data-stu-id="608b2-104">DC/OS agent pools for Azure Container Service</span></span>
<span data-ttu-id="608b2-105">Azure Container Service 中的 DC/OS 叢集包含兩個集區中的代理程式節點，即公用集區和私用集區。</span><span class="sxs-lookup"><span data-stu-id="608b2-105">DC/OS clusters in Azure Container Service contain agent nodes in two pools, a public pool and a private pool.</span></span> <span data-ttu-id="608b2-106">應用程式可以部署 tooeither 集區，會影響您的容器服務在電腦之間的存取範圍。</span><span class="sxs-lookup"><span data-stu-id="608b2-106">An application can be deployed tooeither pool, affecting accessibility between machines in your container service.</span></span> <span data-ttu-id="608b2-107">hello 機器可以是公開的 toohello 網際網路 （公用） 或保留內部 （私用）。</span><span class="sxs-lookup"><span data-stu-id="608b2-107">hello machines can be exposed toohello internet (public) or kept internal (private).</span></span> <span data-ttu-id="608b2-108">本文簡短概述為什麼會有公用集區和私用集區。</span><span class="sxs-lookup"><span data-stu-id="608b2-108">This article gives a brief overview of why there are public and private pools.</span></span>


* <span data-ttu-id="608b2-109">**私用代理程式**：私用代理程式節點會透過非可路由網路來執行。</span><span class="sxs-lookup"><span data-stu-id="608b2-109">**Private agents**: Private agent nodes run through a non-routable network.</span></span> <span data-ttu-id="608b2-110">從 hello 管理區域，或透過 hello 公用區域邊緣路由器，才可存取此網路。</span><span class="sxs-lookup"><span data-stu-id="608b2-110">This network is only accessible from hello admin zone or through hello public zone edge router.</span></span> <span data-ttu-id="608b2-111">根據預設，DC/OS 會在私用代理程式節點上啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="608b2-111">By default, DC/OS launches apps on private agent nodes.</span></span> 

* <span data-ttu-id="608b2-112">**公用代理程式**：公用代理程式節點會透過可公開存取的網路執行 DC/OS 應用程式和服務。</span><span class="sxs-lookup"><span data-stu-id="608b2-112">**Public agents**: Public agent nodes run DC/OS apps and services through a publicly accessible network.</span></span> 

<span data-ttu-id="608b2-113">如需 DC/OS 網路安全性的詳細資訊，請參閱 hello [DC/OS 文件](https://dcos.io/docs/1.7/administration/securing-your-cluster/)。</span><span class="sxs-lookup"><span data-stu-id="608b2-113">For more information about DC/OS network security, see hello [DC/OS documentation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).</span></span>

## <a name="deploy-agent-pools"></a><span data-ttu-id="608b2-114">部署代理程式集區</span><span class="sxs-lookup"><span data-stu-id="608b2-114">Deploy agent pools</span></span>

<span data-ttu-id="608b2-115">hello DC/OS 代理程式集區中的 Azure 容器服務會建立，如下所示：</span><span class="sxs-lookup"><span data-stu-id="608b2-115">hello DC/OS agent pools In Azure Container Service are created as follows:</span></span>

* <span data-ttu-id="608b2-116">hello**私用的集區**包含 hello 號碼的代理程式節點可以指定何時您[部署 hello DC/OS 叢集](container-service-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="608b2-116">hello **private pool** contains hello number of agent nodes that you specify when you [deploy hello DC/OS cluster](container-service-deployment.md).</span></span> 

* <span data-ttu-id="608b2-117">hello**公用集區**一開始包含預先定義的代理程式節點數。</span><span class="sxs-lookup"><span data-stu-id="608b2-117">hello **public pool** initially contains a predetermined number of agent nodes.</span></span> <span data-ttu-id="608b2-118">Hello DC/OS 叢集已佈建時，會自動加入此集區。</span><span class="sxs-lookup"><span data-stu-id="608b2-118">This pool is added automatically when hello DC/OS cluster is provisioned.</span></span>

<span data-ttu-id="608b2-119">hello 私用，而 hello 公用集區是 Azure 虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="608b2-119">hello private pool and hello public pool are Azure virtual machine scale sets.</span></span> <span data-ttu-id="608b2-120">您可以在部署後調整這些集區的大小。</span><span class="sxs-lookup"><span data-stu-id="608b2-120">You can resize these pools after deployment.</span></span>

## <a name="use-agent-pools"></a><span data-ttu-id="608b2-121">使用代理程式集區</span><span class="sxs-lookup"><span data-stu-id="608b2-121">Use agent pools</span></span>
<span data-ttu-id="608b2-122">根據預設，**馬拉松**部署任何新的應用程式 toohello*私人*代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="608b2-122">By default, **Marathon** deploys any new application toohello *private* agent nodes.</span></span> <span data-ttu-id="608b2-123">您必須部署 hello 應用程式 toohello tooexplicitly*公用*hello hello 應用程式建立期間的節點。</span><span class="sxs-lookup"><span data-stu-id="608b2-123">You have tooexplicitly deploy hello application toohello *public* nodes during hello creation of hello application.</span></span> <span data-ttu-id="608b2-124">選取 hello**選擇性**索引標籤並輸入**slave_public** hello**接受資源角色**值。</span><span class="sxs-lookup"><span data-stu-id="608b2-124">Select hello **Optional** tab and enter **slave_public** for hello **Accepted Resource Roles** value.</span></span> <span data-ttu-id="608b2-125">此程序會說明[這裡](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container)在 hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/)文件。</span><span class="sxs-lookup"><span data-stu-id="608b2-125">This process is documented [here](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) and in hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="608b2-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="608b2-126">Next steps</span></span>
* <span data-ttu-id="608b2-127">深入了解如何[管理 DC/OS 容器](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="608b2-127">Read more about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

* <span data-ttu-id="608b2-128">了解如何太[開啟 hello 防火牆](container-service-enable-public-access.md)Azure tooallow 公用存取 tooyour DC/OS 容器所提供。</span><span class="sxs-lookup"><span data-stu-id="608b2-128">Learn how too[open hello firewall](container-service-enable-public-access.md) provided by Azure tooallow public access tooyour DC/OS containers.</span></span>

