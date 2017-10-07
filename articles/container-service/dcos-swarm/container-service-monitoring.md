---
title: "aaaMonitor Azure DC/OS 叢集 Datadog |Microsoft 文件"
description: "使用 Datadog 監視 Azure 容器服務叢集。 使用 hello DC/OS web UI toodeploy hello Datadog 代理程式 tooyour 叢集。"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="34bc3-105">使用 Datadog 監視 Azure Container Service DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="34bc3-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="34bc3-106">本文章中我們將部署 Datadog 代理程式 tooall hello 代理程式節點 Azure 容器服務叢集中。</span><span class="sxs-lookup"><span data-stu-id="34bc3-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="34bc3-107">您將需要 Datadog 帳戶以進行這項設定。</span><span class="sxs-lookup"><span data-stu-id="34bc3-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="34bc3-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="34bc3-108">Prerequisites</span></span>
<span data-ttu-id="34bc3-109">[部署](container-service-deployment.md)和[連接](../container-service-connect.md) Azure Container Service 所設定的叢集。</span><span class="sxs-lookup"><span data-stu-id="34bc3-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="34bc3-110">瀏覽 hello[馬拉松 UI](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="34bc3-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="34bc3-111">跳過[http://datadoghq.com](http://datadoghq.com) tooset Datadog 帳戶。</span><span class="sxs-lookup"><span data-stu-id="34bc3-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="34bc3-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="34bc3-112">Datadog</span></span>
<span data-ttu-id="34bc3-113">Datadog 是一項監視服務，會從 Azure 容器服務叢集內的容器收集監視資料。</span><span class="sxs-lookup"><span data-stu-id="34bc3-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="34bc3-114">Datadog 有 Docker 整合儀表板，可供您查看容器內的特定度量。</span><span class="sxs-lookup"><span data-stu-id="34bc3-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="34bc3-115">從容器收集到的度量會依 CPU、記憶體、網路和 I/O 來加以整理。</span><span class="sxs-lookup"><span data-stu-id="34bc3-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="34bc3-116">Datadog 會將度量分割成容器和映像。</span><span class="sxs-lookup"><span data-stu-id="34bc3-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="34bc3-117">舉例來說，哪些 hello cpu 使用量低於似乎 UI。</span><span class="sxs-lookup"><span data-stu-id="34bc3-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Datadog UI](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="34bc3-119">使用 Marathon 設定 Datadog 部署</span><span class="sxs-lookup"><span data-stu-id="34bc3-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="34bc3-120">這些步驟將示範如何 tooconfigure 和部署與馬拉松 Datadog 應用程式 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="34bc3-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="34bc3-121">透過 [http://localhost:80/](http://localhost:80/)存取 DC/OS UI。</span><span class="sxs-lookup"><span data-stu-id="34bc3-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="34bc3-122">一次在 hello DC/OS UI 導覽 toohello"Universe"，這位於 hello 下由然後搜尋 「 Datadog"並按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="34bc3-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Hello DC/OS Universe 內 Datadog 封裝](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="34bc3-124">現在 toocomplete hello 設定，您需要 Datadog 帳戶或免費的試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="34bc3-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="34bc3-125">一旦您登入 toohello Datadog 網站中看起來 toohello 左邊，並移 tooIntegrations-> 然後[Api](https://app.datadoghq.com/account/settings#api)。</span><span class="sxs-lookup"><span data-stu-id="34bc3-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Datadog API 金鑰](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="34bc3-127">接下來 hello Datadog 組態 hello DC/OS Universe 內輸入您的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="34bc3-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![在 hello DC/OS Universe Datadog 組態](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="34bc3-129">Hello 上述組態中執行個體已設定 too10000000，所以每當新的節點加入 toohello 叢集 Datadog 就會自動部署的代理程式 toothat 節點。</span><span class="sxs-lookup"><span data-stu-id="34bc3-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="34bc3-130">這是過渡解決方案。</span><span class="sxs-lookup"><span data-stu-id="34bc3-130">This is an interim solution.</span></span> <span data-ttu-id="34bc3-131">一旦您已安裝 hello 封裝應該回復 toohello Datadog 網站瀏覽並尋找"[儀表板](https://app.datadoghq.com/dash/list)。 」</span><span class="sxs-lookup"><span data-stu-id="34bc3-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="34bc3-132">從該處，您會看到自訂和整合儀表板。</span><span class="sxs-lookup"><span data-stu-id="34bc3-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="34bc3-133">hello [Docker 儀表板](https://app.datadoghq.com/screen/integration/docker)會有所有的 hello 容器度量，您必須監視您的叢集。</span><span class="sxs-lookup"><span data-stu-id="34bc3-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

