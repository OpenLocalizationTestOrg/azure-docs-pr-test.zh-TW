---
title: "aaaMonitor Azure DC/OS 叢集 Dynatrace |Microsoft 文件"
description: "使用 Dynatrace 監視 Azure Container Service DC/OS 叢集。 部署 hello Dynatrace OneAgent 使用 hello DC/OS 儀表板。"
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "容器，DC/OS，Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="7055b-105">使用 Dynatrace SaaS/Managed 監視 Azure Container Service DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="7055b-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="7055b-106">在本文中，我們會示範如何 toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor 所有 hello Azure 容器服務叢集中的代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="7055b-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="7055b-107">您需要 Dynatrace SaaS/Managed 帳戶以進行這項設定。</span><span class="sxs-lookup"><span data-stu-id="7055b-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="7055b-108">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="7055b-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="7055b-109">Dynatrace 是高動態容器和叢集環境適用的雲端原生監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="7055b-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="7055b-110">它可讓您 toobetter 最佳化您的容器部署和配置的記憶體使用即時使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="7055b-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="7055b-111">其藉由提供自動化基準、問題相互關聯和根本原因偵測，就能夠自動查明應用程式和基礎結構問題。</span><span class="sxs-lookup"><span data-stu-id="7055b-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="7055b-112">hello 以下圖顯示 hello Dynatrace UI:</span><span class="sxs-lookup"><span data-stu-id="7055b-112">hello following figure shows hello Dynatrace UI:</span></span>

![Dynatrace UI](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="7055b-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="7055b-114">Prerequisites</span></span> 
<span data-ttu-id="7055b-115">[部署](container-service-deployment.md)和[連接](./../container-service-connect.md)tooa Azure 容器服務所設定的叢集。</span><span class="sxs-lookup"><span data-stu-id="7055b-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="7055b-116">瀏覽 hello[馬拉松 UI](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="7055b-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="7055b-117">跳過[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset Dynatrace SaaS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7055b-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="7055b-118">使用 Marathon 設定 Dynatrace 部署</span><span class="sxs-lookup"><span data-stu-id="7055b-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="7055b-119">這些步驟顯示如何 tooconfigure 和部署與馬拉松 Dynatrace 應用程式 tooyour 叢集。</span><span class="sxs-lookup"><span data-stu-id="7055b-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="7055b-120">透過 [http://localhost:80/](http://localhost:80/)存取 DC/OS UI。</span><span class="sxs-lookup"><span data-stu-id="7055b-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="7055b-121">一次在 hello DC/OS UI 中，瀏覽 toohello **Universe**索引標籤，然後搜尋**Dynatrace**。</span><span class="sxs-lookup"><span data-stu-id="7055b-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![DC/OS Universe 中的 Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="7055b-123">toocomplete hello 組態中，您需要 Dynatrace SaaS 帳戶或免費的試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7055b-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="7055b-124">一旦您登入 hello Dynatrace 儀表板，選取**部署 Dynatrace**。</span><span class="sxs-lookup"><span data-stu-id="7055b-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Dynatrace 設定 PaaS 整合](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="7055b-126">在 hello 頁面上，選取  **PaaS 整合**。</span><span class="sxs-lookup"><span data-stu-id="7055b-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Dynatrace API 權杖](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="7055b-128">輸入您的 API 語彙基元 hello Dynatrace OneAgent 組態 hello DC/OS Universe 內。</span><span class="sxs-lookup"><span data-stu-id="7055b-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![在 hello DC/OS Universe Dynatrace OneAgent 組態](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="7055b-130">Toohello 數目設定 hello 執行個體的節點中，您想 toorun。</span><span class="sxs-lookup"><span data-stu-id="7055b-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="7055b-131">設定較高數字也有效，但是 DC/OS 將會繼續嘗試 toofind 的新執行個體一直該數目的實際。</span><span class="sxs-lookup"><span data-stu-id="7055b-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="7055b-132">如果您想要的話，您也可以設定類似 1000000 這個 tooa 值。</span><span class="sxs-lookup"><span data-stu-id="7055b-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="7055b-133">在此情況下，每當 toohello 叢集時，會加入新的節點，Dynatrace 自動將部署代理程式 toothat 新節點，hello 價格的 DC/OS 不斷地嘗試 toodeploy 進一步執行個體。</span><span class="sxs-lookup"><span data-stu-id="7055b-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Dynatrace hello DC/OS Universe-執行個體中的組態](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="7055b-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7055b-135">Next steps</span></span>

<span data-ttu-id="7055b-136">一旦您已安裝 hello 封裝，請瀏覽後 toohello Dynatrace 儀表板。</span><span class="sxs-lookup"><span data-stu-id="7055b-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="7055b-137">您可以在您的叢集探索 hello 容器 hello 不同的使用計量。</span><span class="sxs-lookup"><span data-stu-id="7055b-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
