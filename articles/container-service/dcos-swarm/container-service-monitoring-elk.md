---
title: "監視 Azure DC/OS 叢集 - ELK 堆疊 | Microsoft Docs"
description: "使用 ELK (Elasticsearch、Logstash 與 Kibana) 監視 Azure Container Service 中的 DC/OS 叢集。"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Containers, DC/OS, Azure, monitoring, elk, 容器, 監視"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: fcfa277cdd0f3cebc0fbbb23e771fb23ffbe2ca6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="7ea24-104">使用 ELK 監視 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="7ea24-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="7ea24-105">在此文章中，我們示範如何在 Azure Container Service 中的 DC/OS 叢集上部署 ELK (Elasticsearch、Logstash、Kibana) 堆疊。</span><span class="sxs-lookup"><span data-stu-id="7ea24-105">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7ea24-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ea24-106">Prerequisites</span></span>
<span data-ttu-id="7ea24-107">[部署](container-service-deployment.md)並[連接](../container-service-connect.md) Azure Container Service 所設定的 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ea24-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="7ea24-108">在[這裡](container-service-mesos-marathon-ui.md)探索探索 DC/OS 儀表板和 Marathon 服務。</span><span class="sxs-lookup"><span data-stu-id="7ea24-108">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="7ea24-109">同時也請安裝 [Marathon Load Balancer](container-service-load-balancing.md)。</span><span class="sxs-lookup"><span data-stu-id="7ea24-109">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="7ea24-110">ELK (Elasticsearch、Logstash、Kibana)</span><span class="sxs-lookup"><span data-stu-id="7ea24-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="7ea24-111">ELK 堆疊是 Elasticsearch、Logstash 和 Kibana 的組合，提供的端對端堆疊可以監視及分析叢集中的記錄。</span><span class="sxs-lookup"><span data-stu-id="7ea24-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span></span>

## <a name="configure-the-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="7ea24-112">在 DC/OS 叢集上設定 ELK 堆疊</span><span class="sxs-lookup"><span data-stu-id="7ea24-112">Configure the ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="7ea24-113">由 [http://localhost:80/](http://localhost:80/) 存取 DC/OS UI。開啟 DC/OS UI 之後，瀏覽到 [Universe]。</span><span class="sxs-lookup"><span data-stu-id="7ea24-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span></span> <span data-ttu-id="7ea24-114">請在 DC/OS Universe 搜尋並依序安裝 Elasticsearch、Logstash 及 Kibana。</span><span class="sxs-lookup"><span data-stu-id="7ea24-114">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="7ea24-115">如需組態的詳細資訊，您可以移至 [Advanced Installation (進階安裝)]連結。</span><span class="sxs-lookup"><span data-stu-id="7ea24-115">You can learn more about configuration if you go to the **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="7ea24-119">ELK 容器開始運作之後，您需要讓 Marathon-LB 能夠存取 Kibana。</span><span class="sxs-lookup"><span data-stu-id="7ea24-119">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span></span> <span data-ttu-id="7ea24-120">瀏覽到 [Services (服務)] > [kibana]，然後按一下 [Edit (編輯)]，如下圖。</span><span class="sxs-lookup"><span data-stu-id="7ea24-120">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="7ea24-122">切換成 [JSON mode (JSON 模式)]，並捲動到 labels 區段。</span><span class="sxs-lookup"><span data-stu-id="7ea24-122">Toggle to **JSON mode** and scroll down to the labels section.</span></span>
<span data-ttu-id="7ea24-123">您需要新增一個 `"HAPROXY_GROUP": "external"` 項目，如下圖。</span><span class="sxs-lookup"><span data-stu-id="7ea24-123">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="7ea24-124">按一下 [Deploy changes (部署變更)] 之後，容器會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="7ea24-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="7ea24-126">如果您想確認 Kibana 已經在 HAPROXY 儀表板中註冊為服務，您需要開啟代理程式叢集上的連接埠 9090，因為 HAPROXY 在連接埠 9090 執行。</span><span class="sxs-lookup"><span data-stu-id="7ea24-126">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="7ea24-127">根據預設，我們開啟 DC/OS 叢集中的接埠 80、8080 和 443。</span><span class="sxs-lookup"><span data-stu-id="7ea24-127">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span></span>
<span data-ttu-id="7ea24-128">[這裡](container-service-enable-public-access.md)有開啟連接埠並提供公開存取的指示。</span><span class="sxs-lookup"><span data-stu-id="7ea24-128">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="7ea24-129">若要存取 HAPROXY 儀表板，請開啟 Marathon-LB 系統管理員介面，網址是：`http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`。</span><span class="sxs-lookup"><span data-stu-id="7ea24-129">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="7ea24-130">瀏覽到該 URL 之後，您會看到如下圖的 HAPROXY 儀表板，也會看到 Kibana 的服務項目。</span><span class="sxs-lookup"><span data-stu-id="7ea24-130">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="7ea24-132">因為 Kibana 部署在連接埠 5601，所以您需要開啟連接埠 5601 才能存取 Kibana 儀表板。</span><span class="sxs-lookup"><span data-stu-id="7ea24-132">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span></span> <span data-ttu-id="7ea24-133">遵循[這裡](container-service-enable-public-access.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="7ea24-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="7ea24-134">然後開啟 Kibana 儀表板，網址是：`http://localhost:5601`。</span><span class="sxs-lookup"><span data-stu-id="7ea24-134">Then open the Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ea24-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ea24-135">Next steps</span></span>

* <span data-ttu-id="7ea24-136">如需系統和應用程式記錄檔轉送與設定的相關資訊，請參閱 [DC/OS 中使用 ELK 的記錄檔管理 (英文)](https://docs.mesosphere.com/1.8/administration/logging/elk/)。</span><span class="sxs-lookup"><span data-stu-id="7ea24-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="7ea24-137">若要篩選記錄檔，請參閱[使用 ELK 篩選記錄檔 (英文)](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/)。</span><span class="sxs-lookup"><span data-stu-id="7ea24-137">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

