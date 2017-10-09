---
title: "aaaMonitor Azure 容器服務叢集 Sysdig |Microsoft 文件"
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
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="b05fc-104">使用 Sysdig 監視 Azure 容器服務叢集</span><span class="sxs-lookup"><span data-stu-id="b05fc-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="b05fc-105">在本文中，我們將部署 Sysdig 代理程式 tooall hello 代理程式節點 Azure 容器服務叢集中。</span><span class="sxs-lookup"><span data-stu-id="b05fc-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="b05fc-106">您需要 Sysdig 帳戶以進行這項設定。</span><span class="sxs-lookup"><span data-stu-id="b05fc-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b05fc-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="b05fc-107">Prerequisites</span></span>
<span data-ttu-id="b05fc-108">[部署](container-service-deployment.md)和[連接](../container-service-connect.md) Azure Container Service 所設定的叢集。</span><span class="sxs-lookup"><span data-stu-id="b05fc-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="b05fc-109">瀏覽 hello[馬拉松 UI](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="b05fc-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="b05fc-110">跳過[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset Sysdig 雲端帳戶。</span><span class="sxs-lookup"><span data-stu-id="b05fc-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="b05fc-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="b05fc-111">Sysdig</span></span>
<span data-ttu-id="b05fc-112">Sysdig 是監視服務，可讓您 toomonitor 您在叢集內的容器。</span><span class="sxs-lookup"><span data-stu-id="b05fc-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="b05fc-113">Sysdig 已知 toohelp 進行疑難排解，但是它也有基本的監視度量的 CPU、 網路、 記憶體和 I/O。</span><span class="sxs-lookup"><span data-stu-id="b05fc-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="b05fc-114">使得的容器使用的簡單 toosee Sysdig hello hardest 或基本上使用 hello 大部分的記憶體和 CPU。</span><span class="sxs-lookup"><span data-stu-id="b05fc-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="b05fc-115">此檢視位於 hello beta 中的 < 概觀 > 一節。</span><span class="sxs-lookup"><span data-stu-id="b05fc-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![Sysdig UI](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="b05fc-117">使用 Marathon 設定 Sysdig 部署</span><span class="sxs-lookup"><span data-stu-id="b05fc-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="b05fc-118">這些步驟將示範如何 tooconfigure 和部署與馬拉松 Sysdig 應用程式 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="b05fc-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="b05fc-119">存取您的 DC/OS UI 透過[http://localhost:80 /](http://localhost:80/)一次在 hello DC/OS UI 瀏覽的 toohello"Universe"，這位於 hello 下，然後搜尋 「 Sysdig。 」</span><span class="sxs-lookup"><span data-stu-id="b05fc-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![DC/OS Universe 中的 Sysdig](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="b05fc-121">現在 toocomplete hello 組態需要 Sysdig 雲端帳戶或免費的試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b05fc-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="b05fc-122">一旦您登入 toohello Sysdig 雲端網站，按一下您的使用者名稱，然後在 hello 頁面上您應該會看到您的 「 存取金鑰 」。</span><span class="sxs-lookup"><span data-stu-id="b05fc-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig API 金鑰](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="b05fc-124">接下來 hello Sysdig 組態 hello DC/OS Universe 內輸入您的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="b05fc-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![在 hello DC/OS Universe Sysdig 組態](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="b05fc-126">現在設定 hello 執行個體 too10000000 toohello 叢集 Sysdig 加入新的節點時就會自動部署代理程式以便 toothat 新節點。</span><span class="sxs-lookup"><span data-stu-id="b05fc-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="b05fc-127">這是過渡期解決方案 toomake 確定 Sysdig 將部署 tooall hello 叢集內的新代理程式。</span><span class="sxs-lookup"><span data-stu-id="b05fc-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Sysdig hello DC/OS Universe-執行個體中的組態](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="b05fc-129">一旦您已安裝 hello 封裝瀏覽後 toohello Sysdig UI，然後您會在您的叢集內 hello 容器可以 tooexplore hello 不同的使用情況標準。</span><span class="sxs-lookup"><span data-stu-id="b05fc-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="b05fc-130">您也可以透過[新的儀表板精靈](https://app.sysdigcloud.com/#/dashboards/new)來安裝 Mesos 和 Marathon 專用儀表板。</span><span class="sxs-lookup"><span data-stu-id="b05fc-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
