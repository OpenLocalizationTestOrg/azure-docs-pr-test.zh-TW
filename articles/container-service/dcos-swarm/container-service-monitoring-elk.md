---
title: "aaaMonitor Azure DC/OS 叢集-ELK 堆疊 |Microsoft 文件"
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
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="8881f-104">使用 ELK 監視 Azure Container Service 叢集</span><span class="sxs-lookup"><span data-stu-id="8881f-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="8881f-105">在本文中，我們將示範如何 toodeploy hello ELK (Elasticsearch，Logstash，Kibana) 堆疊 Azure 容器服務中的 DC/OS 叢集上。</span><span class="sxs-lookup"><span data-stu-id="8881f-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8881f-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="8881f-106">Prerequisites</span></span>
<span data-ttu-id="8881f-107">[部署](container-service-deployment.md)並[連接](../container-service-connect.md) Azure Container Service 所設定的 DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="8881f-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="8881f-108">瀏覽 hello DC/OS 儀表板和馬拉松服務[這裡](container-service-mesos-marathon-ui.md)。</span><span class="sxs-lookup"><span data-stu-id="8881f-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="8881f-109">也會安裝 hello[馬拉松負載平衡器](container-service-load-balancing.md)。</span><span class="sxs-lookup"><span data-stu-id="8881f-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="8881f-110">ELK (Elasticsearch、Logstash、Kibana)</span><span class="sxs-lookup"><span data-stu-id="8881f-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="8881f-111">ELK 堆疊是 Elasticsearch，Logstash，組合 Kibana，提供結束 tooend 堆疊，可以和使用的 toomonitor 分析您的叢集中的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8881f-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="8881f-112">DC/OS 叢集上設定 hello ELK 堆疊</span><span class="sxs-lookup"><span data-stu-id="8881f-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="8881f-113">存取您的 DC/OS UI 透過[http://localhost:80 /](http://localhost:80/)一次在 hello DC/OS UI 導覽太**Universe**。</span><span class="sxs-lookup"><span data-stu-id="8881f-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="8881f-114">搜尋並安裝 Elasticsearch、 Logstash 和 Kibana 從 hello DC/OS Universe 和的特定順序。</span><span class="sxs-lookup"><span data-stu-id="8881f-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="8881f-115">您可以進一步了解組態如果您 toohello**進階安裝**連結。</span><span class="sxs-lookup"><span data-stu-id="8881f-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="8881f-119">一次 hello ELK 容器和啟動並執行的是，您需要存取透過馬拉松 LB tooenable Kibana toobe。</span><span class="sxs-lookup"><span data-stu-id="8881f-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="8881f-120">瀏覽過**服務** > **kibana**，然後按一下**編輯**如下所示。</span><span class="sxs-lookup"><span data-stu-id="8881f-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="8881f-122">切換太**JSON 模式**和捲動 toohello 標籤 > 一節。</span><span class="sxs-lookup"><span data-stu-id="8881f-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="8881f-123">您需要 tooadd`"HAPROXY_GROUP": "external"`項目所示下方。</span><span class="sxs-lookup"><span data-stu-id="8881f-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="8881f-124">按一下 [Deploy changes (部署變更)] 之後，容器會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="8881f-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="8881f-126">如果您想要 tooverify 該 Kibana 註冊為 hello haproxy 等儀表板中的服務，haproxy 等連接埠 9090 上執行時，需要 tooopen 連接埠 9090 hello 代理程式的叢集上。</span><span class="sxs-lookup"><span data-stu-id="8881f-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="8881f-127">根據預設，我們開啟連接埠 80、 8080，並在 443 hello DC/OS 代理程式的叢集。</span><span class="sxs-lookup"><span data-stu-id="8881f-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="8881f-128">指示 tooopen 連接埠，並提供公用存取會提供[這裡](container-service-enable-public-access.md)。</span><span class="sxs-lookup"><span data-stu-id="8881f-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="8881f-129">tooaccess hello haproxy 等儀表板，在開啟 hello 馬拉松 LB 管理介面： `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`。</span><span class="sxs-lookup"><span data-stu-id="8881f-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="8881f-130">一旦您瀏覽 toohello URL，如下所示，您應該看到 hello haproxy 等儀表板，您應該看到 Kibana 服務項目。</span><span class="sxs-lookup"><span data-stu-id="8881f-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="8881f-132">tooaccess hello Kibana 儀表板，將連接埠 5601 部署時，您需要 tooopen 連接埠 5601。</span><span class="sxs-lookup"><span data-stu-id="8881f-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="8881f-133">遵循[這裡](container-service-enable-public-access.md)的指示。</span><span class="sxs-lookup"><span data-stu-id="8881f-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="8881f-134">然後開啟 在 hello Kibana 儀表板： `http://localhost:5601`。</span><span class="sxs-lookup"><span data-stu-id="8881f-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8881f-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8881f-135">Next steps</span></span>

* <span data-ttu-id="8881f-136">如需系統和應用程式記錄檔轉送與設定的相關資訊，請參閱 [DC/OS 中使用 ELK 的記錄檔管理 (英文)](https://docs.mesosphere.com/1.8/administration/logging/elk/)。</span><span class="sxs-lookup"><span data-stu-id="8881f-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="8881f-137">toofilter 記錄，請參閱 < [ELK 篩選記錄檔](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/)。</span><span class="sxs-lookup"><span data-stu-id="8881f-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

