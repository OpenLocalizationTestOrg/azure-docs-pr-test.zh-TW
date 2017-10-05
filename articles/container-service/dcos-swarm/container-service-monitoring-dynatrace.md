---
title: "監視 Azure DC/OS 叢集 - Dynatrace | Microsoft Docs"
description: "使用 Dynatrace 監視 Azure Container Service DC/OS 叢集。 使用 DC/OS 儀表板部署 Dynatrace OneAgent。"
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
ms.openlocfilehash: 6fa23728680779e33eda7bb9aa8a01b9cad9a82b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="04a5d-105">使用 Dynatrace SaaS/Managed 監視 Azure Container Service DC/OS 叢集</span><span class="sxs-lookup"><span data-stu-id="04a5d-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="04a5d-106">在本文中，我們會示範如何部署 [Dynatrace](https://www.dynatrace.com/) OneAgent，以監視 Azure Container Service 叢集中的所有代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="04a5d-106">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="04a5d-107">您需要 Dynatrace SaaS/Managed 帳戶以進行這項設定。</span><span class="sxs-lookup"><span data-stu-id="04a5d-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="04a5d-108">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="04a5d-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="04a5d-109">Dynatrace 是高動態容器和叢集環境適用的雲端原生監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="04a5d-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="04a5d-110">它可讓您使用即時使用量資料，進一步最佳化您的容器部署和記憶體配置。</span><span class="sxs-lookup"><span data-stu-id="04a5d-110">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="04a5d-111">其藉由提供自動化基準、問題相互關聯和根本原因偵測，就能夠自動查明應用程式和基礎結構問題。</span><span class="sxs-lookup"><span data-stu-id="04a5d-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="04a5d-112">下圖顯示 Dynatrace UI：</span><span class="sxs-lookup"><span data-stu-id="04a5d-112">The following figure shows the Dynatrace UI:</span></span>

![Dynatrace UI](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="04a5d-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="04a5d-114">Prerequisites</span></span> 
<span data-ttu-id="04a5d-115">[部署](container-service-deployment.md)和[連接](./../container-service-connect.md)至 Azure Container Service 所設定的叢集。</span><span class="sxs-lookup"><span data-stu-id="04a5d-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) to a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="04a5d-116">瀏覽 [Marathon UI](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="04a5d-116">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="04a5d-117">移至 [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) 以設定 Dynatrace SaaS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="04a5d-117">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="04a5d-118">使用 Marathon 設定 Dynatrace 部署</span><span class="sxs-lookup"><span data-stu-id="04a5d-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="04a5d-119">這些步驟示範如何使用 Marathon 設定 Dynatrace 應用程式並將它部署到您的叢集。</span><span class="sxs-lookup"><span data-stu-id="04a5d-119">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span></span>

1. <span data-ttu-id="04a5d-120">透過 [http://localhost:80/](http://localhost:80/)存取 DC/OS UI。</span><span class="sxs-lookup"><span data-stu-id="04a5d-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="04a5d-121">在進入 DC/OS UI 後，瀏覽至 **Universe**，然後搜尋 **Dynatrace**。</span><span class="sxs-lookup"><span data-stu-id="04a5d-121">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span></span>

    ![DC/OS Universe 中的 Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="04a5d-123">若要完成設定，您需要 Dynatrace SaaS 帳戶或免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="04a5d-123">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="04a5d-124">登入 Dynatrace 儀表板後，請選取 [部署 Dynatrace]。</span><span class="sxs-lookup"><span data-stu-id="04a5d-124">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Dynatrace 設定 PaaS 整合](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="04a5d-126">在頁面上，選取 [設定 PaaS 整合]。</span><span class="sxs-lookup"><span data-stu-id="04a5d-126">On the page, select **Set up PaaS integration**.</span></span> 

    ![Dynatrace API 權杖](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="04a5d-128">將 API 金鑰輸入到 DC/OS Universe 中的 Dynatrace OneAgent 組態。</span><span class="sxs-lookup"><span data-stu-id="04a5d-128">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span></span> 

    ![DC/OS Universe 中的 Dynatrace OneAgent 組態](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="04a5d-130">將執行個體設定為您想要執行的節點數目。</span><span class="sxs-lookup"><span data-stu-id="04a5d-130">Set the instances to the number of nodes you intend to run.</span></span> <span data-ttu-id="04a5d-131">設定較高的數目也可行，但 DC/OS 會繼續嘗試尋找新的執行個體，直到實際達到該數目為止。</span><span class="sxs-lookup"><span data-stu-id="04a5d-131">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span></span> <span data-ttu-id="04a5d-132">如果想要的話，您也可以將此設定為 1000000 之類的值。</span><span class="sxs-lookup"><span data-stu-id="04a5d-132">If you prefer, you can also set this to a value like 1000000.</span></span> <span data-ttu-id="04a5d-133">在此情況下，每當新節點新增到叢集時，Dynatrace 就會自動將代理程式部署到該新節點，並採用 DC/OS 不斷嘗試部署其他執行個體的價格。</span><span class="sxs-lookup"><span data-stu-id="04a5d-133">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span></span>

    ![DC/OS Universe 中的 Dynatrace 組態 - 執行個體](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="04a5d-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="04a5d-135">Next steps</span></span>

<span data-ttu-id="04a5d-136">一旦您安裝了套件，請瀏覽回到 Dynatrace 儀表板。</span><span class="sxs-lookup"><span data-stu-id="04a5d-136">Once you've installed the package, navigate back to the Dynatrace dashboard.</span></span> <span data-ttu-id="04a5d-137">您可以探索您的叢集中各容器的不同使用量計量。</span><span class="sxs-lookup"><span data-stu-id="04a5d-137">You can explore the different usage metrics for the containers within your cluster.</span></span> 