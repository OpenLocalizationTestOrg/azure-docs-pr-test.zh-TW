---
title: "使用 Sysdig 監視 Azure Container Service 叢集 | Microsoft Docs"
description: "使用 Sysdig 監視 Azure 容器服務叢集。"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器，DC/OS，Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: e61001161e632a5d2e513107e30f1eaf06103989
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="d3af2-104">使用 Sysdig 監視 Azure 容器服務叢集</span><span class="sxs-lookup"><span data-stu-id="d3af2-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="d3af2-105">本文中，我們會將 Sysdig 代理程式部署到 Azure 容器服務叢集中的所有代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="d3af2-105">In this article, we will deploy Sysdig agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="d3af2-106">您需要 Sysdig 帳戶以進行這項設定。</span><span class="sxs-lookup"><span data-stu-id="d3af2-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d3af2-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="d3af2-107">Prerequisites</span></span>
<span data-ttu-id="d3af2-108">[部署](container-service-deployment.md)和[連接](../container-service-connect.md) Azure Container Service 所設定的叢集。</span><span class="sxs-lookup"><span data-stu-id="d3af2-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="d3af2-109">瀏覽 [Marathon UI](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="d3af2-109">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="d3af2-110">移至 [http://app.sysdigcloud.com](http://app.sysdigcloud.com) 設定 Sysdig 雲端帳戶。</span><span class="sxs-lookup"><span data-stu-id="d3af2-110">Go to [http://app.sysdigcloud.com](http://app.sysdigcloud.com) to set up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="d3af2-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="d3af2-111">Sysdig</span></span>
<span data-ttu-id="d3af2-112">Sysdig 是一項監視服務，可讓您在叢集內監視您的容器。</span><span class="sxs-lookup"><span data-stu-id="d3af2-112">Sysdig is a monitoring service that allows you to monitor your containers within your cluster.</span></span> <span data-ttu-id="d3af2-113">Sysdig 以協助疑難排解而知名，不過 Sysdig 也具有針對 CPU、網路功能、記憶體和 I/O 的基本監視計量。</span><span class="sxs-lookup"><span data-stu-id="d3af2-113">Sysdig is known to help with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="d3af2-114">Sysdig 讓您更容易查看哪些容器作用最密集或基本上使用最多記憶體和 CPU。</span><span class="sxs-lookup"><span data-stu-id="d3af2-114">Sysdig makes it easy to see which containers are working the hardest or essentially using the most memory and CPU.</span></span> <span data-ttu-id="d3af2-115">此檢視位於 [概觀] 一節中，目前是 Beta 版。</span><span class="sxs-lookup"><span data-stu-id="d3af2-115">This view is in the “Overview” section, which is currently in beta.</span></span> 

![Sysdig UI](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="d3af2-117">使用 Marathon 設定 Sysdig 部署</span><span class="sxs-lookup"><span data-stu-id="d3af2-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="d3af2-118">這些步驟將說明如何使用 Marathon 設定並將 Sysdig 應用程式部署到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="d3af2-118">These steps will show you how to configure and deploy Sysdig applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="d3af2-119">透過 [http://localhost:80/](http://localhost:80/) 存取 DC/OS UI。在 DC/OS UI 中瀏覽至位於左下方的「Universe」，然後搜尋「Sysdig」。</span><span class="sxs-lookup"><span data-stu-id="d3af2-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to the "Universe", which is on the bottom left and then search for "Sysdig."</span></span>

![DC/OS Universe 中的 Sysdig](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="d3af2-121">現在，若要完成設定需要 Sysdig 雲端帳戶或免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d3af2-121">Now to complete the configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="d3af2-122">登入至 Sysdig 雲端網站後，按一下使用者名稱，在頁面上應該會看到「存取金鑰」。</span><span class="sxs-lookup"><span data-stu-id="d3af2-122">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Sysdig API 金鑰](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="d3af2-124">接下來將存取金鑰輸入到 DC/OS Universe 中的 Sysdig 設定。</span><span class="sxs-lookup"><span data-stu-id="d3af2-124">Next enter your Access Key into the Sysdig configuration within the DC/OS Universe.</span></span> 

![DC/OS Universe 中的 Sysdig 設定](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="d3af2-126">現在將執行個體設為 10000000，每當一個新節點新增至叢集時，Sysdig 會自動將代理程式部署到該新節點。</span><span class="sxs-lookup"><span data-stu-id="d3af2-126">Now set the instances to 10000000 so whenever a new node is added to the cluster Sysdig will automatically deploy an agent to that new node.</span></span> <span data-ttu-id="d3af2-127">這是過渡性解決方案，用以確保 Sysdig 會部署到叢集內的所有新代理程式。</span><span class="sxs-lookup"><span data-stu-id="d3af2-127">This is an interim solution to make sure Sysdig will deploy to all new agents within the cluster.</span></span> 

![DC/OS Universe 中的 Sysdig 設定 - 執行個體](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="d3af2-129">安裝套件之後回到 Sysdig UI，您就可以瀏覽叢集內不同的容器使用情況計量。</span><span class="sxs-lookup"><span data-stu-id="d3af2-129">Once you've installed the package navigate back to the Sysdig UI and you'll be able to explore the different usage metrics for the containers within your cluster.</span></span> 

<span data-ttu-id="d3af2-130">您也可以透過[新的儀表板精靈](https://app.sysdigcloud.com/#/dashboards/new)來安裝 Mesos 和 Marathon 專用儀表板。</span><span class="sxs-lookup"><span data-stu-id="d3af2-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
