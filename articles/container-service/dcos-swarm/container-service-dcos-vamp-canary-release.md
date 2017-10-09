---
title: "在 Azure DC/OS 叢集 Vamp aaaCanary 發行 |Microsoft 文件"
description: "Toouse Vamp toocanary 發行服務的方式，並套用智慧篩選 Azure 容器服務 DC/OS 叢集上的流量"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="7ceb3-103">Azure Container Service DC/OS 叢集上具備 Vamp 的 Canary 版本微服務</span><span class="sxs-lookup"><span data-stu-id="7ceb3-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="7ceb3-104">在本逐步解說中，我們會在具備 DC/OS 叢集的 Azure Container Service 上設定 Vamp。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="7ceb3-105">我們加那利版本 hello Vamp 示範服務 」 sava 」，並解決不相容的 Firefox hello 服務套用智慧的流量篩選。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="7ceb3-106">在本逐步解說 Vamp 叢集上執行的 DC/OS，但您也可以使用 Vamp Kubernetes 為 hello 協調者。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="7ceb3-107">關於 Canary 版本與 Vamp</span><span class="sxs-lookup"><span data-stu-id="7ceb3-107">About canary releases and Vamp</span></span>


<span data-ttu-id="7ceb3-108">[Canary 版本](https://martinfowler.com/bliki/CanaryRelease.html)是諸如 Netflix、Facebook 和 Spotify 等創新組織所採用的智慧型部署策略。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="7ceb3-109">它是個很適切的方法，因為它能減少問題、引入網路安全性，並提升創新技術。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="7ceb3-110">那為什麼並非所有公司都使用它？</span><span class="sxs-lookup"><span data-stu-id="7ceb3-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="7ceb3-111">擴充 CI/CD 管線 tooinclude 加那利策略會增加複雜性，而且需要更詳盡的 devops 知識和經驗。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="7ceb3-112">這是足夠 tooblock 小公司與企業深入見解它們甚至開始之前。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="7ceb3-113">[Vamp](http://vamp.io/)是設計的開放原始碼系統 tooease 這項轉換，並讓加那利釋放功能 tooyour 慣用容器排程器。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="7ceb3-114">Vamp 的 Canary 功能並不僅是以百分比為基礎的發行。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="7ceb3-115">可篩選及分散於各種不同的條件，例如 tootarget 特定使用者、 IP 範圍或裝置上的流量。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="7ceb3-116">Vamp 會追蹤和分析效能計量，允許以實際資料作為基礎進行自動化。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="7ceb3-117">您可以設定錯誤的自動復原，或以負載或延遲作為基礎，將個別服務變化進行調整。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="7ceb3-118">使用 DC/OS 設定 Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7ceb3-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="7ceb3-119">使用一個主機和兩個預設大小的代理程式來[部署 DC/OS 叢集](container-service-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="7ceb3-120">[建立的 SSH 通道](../container-service-connect.md)tooconnect toohello DC/OS 叢集。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="7ceb3-121">本文假設您建立通道 toohello 本機通訊埠 80 上的叢集。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="7ceb3-122">設定 Vamp</span><span class="sxs-lookup"><span data-stu-id="7ceb3-122">Set up Vamp</span></span>

<span data-ttu-id="7ceb3-123">既然您已執行的 DC/OS 叢集，您可以安裝 Vamp 從 hello DC/OS UI (http://localhost:80)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![DC/OS UI](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="7ceb3-125">會在兩個階段中完成安裝︰</span><span class="sxs-lookup"><span data-stu-id="7ceb3-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="7ceb3-126">**部署 Elasticsearch**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="7ceb3-127">然後**部署 Vamp**安裝 hello Vamp DC/OS universe 套件。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="7ceb3-128">部署 Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="7ceb3-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="7ceb3-129">Vamp 需要 Elasticsearch 來進行計量收集和彙總。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="7ceb3-130">您可以使用 hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy 相容的 Vamp Elasticsearch 堆疊。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="7ceb3-131">在 hello DC/OS UI，移過**服務**按一下**部署服務**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="7ceb3-132">選取**JSON 模式**從 hello**部署新服務**快顯。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![選取 JSON 模式](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="7ceb3-134">下列 JSON hello 中貼上。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-134">Paste in hello following JSON.</span></span> <span data-ttu-id="7ceb3-135">此設定為 1 GB 的 RAM 與 hello Elasticsearch 連接埠上的基本健全狀況檢查執行 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="7ceb3-136">按一下 [ **部署**]。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-136">Click **Deploy**.</span></span>

  <span data-ttu-id="7ceb3-137">DC/OS 部署 hello Elasticsearch 容器。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="7ceb3-138">您可以在 hello 上追蹤進度**服務**頁面。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-138">You can track progress on hello **Services** page.</span></span>  

  ![部署 e?Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="7ceb3-140">部署 Vamp</span><span class="sxs-lookup"><span data-stu-id="7ceb3-140">Deploy Vamp</span></span>

<span data-ttu-id="7ceb3-141">一旦 Elasticsearch 報告為**執行**，您可以加入 hello Vamp DC/OS Universe 封裝。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="7ceb3-142">跳過**Universe**並搜尋**vamp**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="7ceb3-143">![DC/OS Universe 上的 Vamp](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="7ceb3-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="7ceb3-144">按一下**安裝**下一步 toohello vamp 封裝，然後選擇 **進階安裝**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="7ceb3-145">向下捲動並輸入下列 elasticsearch url hello: `http://elasticsearch.marathon.mesos:9200`。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![輸入 Elasticsearch URL](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="7ceb3-147">按一下**檢閱和安裝**，然後按一下 **安裝**toostart hello 部署。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="7ceb3-148">DC/OS 會部署所有必要的 Vamp 元件。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="7ceb3-149">您可以在 hello 上追蹤進度**服務**頁面。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-149">You can track progress on hello **Services** page.</span></span>
  
  ![部署 Vamp 作為 Universe 套件](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="7ceb3-151">一旦完成部署之後，您可以存取 hello Vamp UI:</span><span class="sxs-lookup"><span data-stu-id="7ceb3-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![DC/OS 上的 Vamp 服務](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp UI](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="7ceb3-154">部署您的第一個服務</span><span class="sxs-lookup"><span data-stu-id="7ceb3-154">Deploy your first service</span></span>

<span data-ttu-id="7ceb3-155">現在該 Vamp 已啟動並且執行中，請從藍圖部署服務。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="7ceb3-156">最簡單的形式， [Vamp 藍圖](http://vamp.io/documentation/using-vamp/blueprints/)描述 hello 端點 （閘道）、 叢集，以及服務 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="7ceb3-157">Vamp 使用叢集 toogroup 不同的各樣 hello 相同服務成邏輯群組加那利釋出或 A / B 測試。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="7ceb3-158">此案例中使用的範例整合型應用程式稱為 [**sava**](https://github.com/magneticio/sava)，為 1.0 版。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="7ceb3-159">hello monolith 會封裝在 Docker 容器，也就是在 Docker Hub magneticio/sava:1.0.0 下。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="7ceb3-160">hello 應用程式通常會執行連接埠 8080，但是您想要在此情況下連接埠 9050 tooexpose。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="7ceb3-161">部署使用簡單的藍圖 Vamp 透過 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="7ceb3-162">跳過**部署**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="7ceb3-163">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-163">Click **Add**.</span></span>

3. <span data-ttu-id="7ceb3-164">貼上的下列 hello 藍圖 YAML。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="7ceb3-165">此藍圖所包含的一個叢集只有一個服務變化，我們將在稍後步驟中進行變更︰</span><span class="sxs-lookup"><span data-stu-id="7ceb3-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="7ceb3-166">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-166">Click **Save**.</span></span> <span data-ttu-id="7ceb3-167">Vamp 起始 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="7ceb3-168">hello 部署會列在 hello**部署**頁面。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="7ceb3-169">按一下 hello 部署 toomonitor 其狀態。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-169">Click hello deployment toomonitor its status.</span></span>

![Vamp UI - 部署 sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Vamp UI 中的 sava 服務](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="7ceb3-172">建立這兩個閘道，這會列在 hello**閘道**頁面：</span><span class="sxs-lookup"><span data-stu-id="7ceb3-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="7ceb3-173">執行服務 （連接埠 9050） 穩定端點 tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="7ceb3-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="7ceb3-174">受 Vamp 管理的內部閘道 (稍後將詳細說明此閘道)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Vamp UI - sava 閘道](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="7ceb3-176">hello sava 服務現在已部署，但是您無法存取，外部因為 hello Azure 負載平衡器並不知道 tooforward 流量 tooit 尚未。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="7ceb3-177">tooaccess hello 服務，更新 hello Azure 網路組態。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="7ceb3-178">更新 hello Azure 網路組態</span><span class="sxs-lookup"><span data-stu-id="7ceb3-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="7ceb3-179">Vamp hello DC/OS 代理程式節點，公開連接埠 9050 穩定端點上的已部署的 hello sava 服務。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="7ceb3-180">從外部 hello DC/OS 叢集中的 tooaccess hello 服務進行下列變更 toohello Azure 網路組態，在叢集部署的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ceb3-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="7ceb3-181">**設定 hello Azure 負載平衡器**hello 代理程式 (hello 名為資源**dcos 代理程式-lb xxxx**) 以健全狀況探查和規則 tooforward 流量在連接埠 9050 toohello sava 執行個體上的。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="7ceb3-182">**更新 hello 網路安全性群組**hello 公用代理程式 (hello 名為資源**XXXX-代理程式-公用-nsg-XXXX**) 連接埠 9050 tooallow 流量。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="7ceb3-183">使用這些工作的詳細的步驟 toocomplete hello Azure 入口網站，請參閱[啟用公用存取 tooan Azure 容器服務應用程式](container-service-enable-public-access.md)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="7ceb3-184">針對所有連接埠設定指定連接埠 9050。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="7ceb3-185">一旦建立的所有項目，請移 toohello**概觀**刀鋒視窗中的 hello DC/OS 代理程式負載平衡器 (hello 名為資源**dcos 代理程式-lb xxxx**)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="7ceb3-186">尋找 hello**公用 IP 位址**，並使用連接埠 9050 hello 位址 tooaccess sava。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Azure 入口網站 - 取得公用 IP 位址](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="7ceb3-189">執行 Canary 版本</span><span class="sxs-lookup"><span data-stu-id="7ceb3-189">Run a canary release</span></span>

<span data-ttu-id="7ceb3-190">假設您有此應用程式的新版本，您想 toocanary 發行至實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="7ceb3-191">您將它當做 magneticio/sava:1.1.0 容器化並準備好 toogo。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="7ceb3-192">Vamp 可讓您輕鬆地將新的服務 toohello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="7ceb3-193">這些 「 合併 」 服務會與 hello hello 叢集中現有的服務一起部署，而指派的權數為 0%。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="7ceb3-194">沒有流量是新合併的 tooa 路由的服務，直到您調整 hello 流量分配。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="7ceb3-195">hello Vamp UI 中的 hello 加權滑桿可讓您完全控制 hello 分佈，以便進行累加式調整 (加那利 release) 或立即回復。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="7ceb3-196">合併新的服務變化</span><span class="sxs-lookup"><span data-stu-id="7ceb3-196">Merge a new service variant</span></span>

<span data-ttu-id="7ceb3-197">toomerge hello 新 sava 1.1 的服務以執行部署的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ceb3-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="7ceb3-198">在 hello Vamp UI 中，按一下 **藍圖**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="7ceb3-199">按一下**新增**和貼上的下列 hello 藍圖 YAML： 此藍圖描述新的服務變數 (sava: 1.1.0) toodeploy hello 現有叢集 (sava_cluster) 內。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="7ceb3-200">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-200">Click **Save**.</span></span> <span data-ttu-id="7ceb3-201">儲存並且列在 hello hello 藍圖**藍圖**頁面。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="7ceb3-202">開啟 hello hello sava: 1.1 藍圖，然後按一下 [動作] 功能表**合併至**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Vamp UI - 藍圖](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="7ceb3-204">選取 hello **sava**部署，然後按一下**合併**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![Vamp UI-合併藍圖 toodeployment](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="7ceb3-206">Vamp 部署 hello 新 sava: 1.1.0 服務 variant hello 藍圖連同 sava: 1.0.0 hello 中所述**sava_cluster**的 hello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![Vamp UI - 更新的 sava 部署](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="7ceb3-208">hello **sava/sava_cluster/webport**閘道 （hello 叢集端點），也會更新，新加入路由 toohello 部署 sava: 1.1.0。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="7ceb3-209">此時，沒有流量路由傳送這裡 (hello**加權**設定 too0%)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![Vamp UI - 叢集閘道](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="7ceb3-211">Canary 版本</span><span class="sxs-lookup"><span data-stu-id="7ceb3-211">Canary release</span></span>

<span data-ttu-id="7ceb3-212">這兩個版本的 sava 部署在 hello 相同叢集，請調整移動 hello 這兩者之間的流量 hello 分佈**加權**滑桿。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="7ceb3-213">按一下![Vamp UI-編輯](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png)下一步太**加權**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="7ceb3-214">設定 hello 加權發佈 too50%/50%並按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![Vamp UI - 閘道權數滑桿](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="7ceb3-216">返回 tooyour 瀏覽器，並重新整理 hello sava 頁面數次。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="7ceb3-217">hello sava 應用程式現在會 sava: 1.0 頁面和 sava: 1.1 頁面之間切換。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![將 sava1.0 和 sava1.1 服務進行交替](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="7ceb3-219">這個替代 hello 頁面的最適合搭配 hello"Incognito 」 或 「 匿名 」 模式，在瀏覽器因為 hello 快取的靜態資產。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="7ceb3-220">篩選流量</span><span class="sxs-lookup"><span data-stu-id="7ceb3-220">Filter traffic</span></span>

<span data-ttu-id="7ceb3-221">假設您在部署之後發現 sava:1.1.0 中發生不相容，而造成 Firefox 瀏覽器中的顯示問題。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="7ceb3-222">您可以設定 Vamp toofilter 連入流量，並指示所有 Firefox 使用者都回 toohello 已知穩定 sava: 1.0.0。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="7ceb3-223">此篩選條件立即解析 hello Firefox 使用者的干擾，同時其他人仍繼續 tooenjoy hello 優點 hello 改善 sava: 1.1.0。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="7ceb3-224">Vamp 使用**條件**toofilter 流量之間閘道的路由。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="7ceb3-225">流量會先經過篩選，而且導向相應 toohello 套用條件 tooeach 路由。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="7ceb3-226">所有剩餘的流量會分散根據 toohello 閘道權重設定。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="7ceb3-227">您可以建立條件 toofilter Firefox 的所有使用者，並將他們導向 toohello 舊 sava: 1.0.0:</span><span class="sxs-lookup"><span data-stu-id="7ceb3-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="7ceb3-228">在 hello sava/sava_cluster/webport**閘道**頁面上，按一下![Vamp UI-編輯](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png)tooadd**條件**toohello 路由 sava/sava_cluster/sava:1.0.0/webport。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="7ceb3-229">輸入 hello 條件**使用者代理程式 = = Firefox**按一下![Vamp UI-儲存](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="7ceb3-230">Vamp hello 將條件加入與預設長度為 0%。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="7ceb3-231">toostart 篩選流量，您需要 tooadjust hello 條件強度。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="7ceb3-232">按一下![Vamp UI-編輯](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png)toochange hello**強度**套用 toohello 條件。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="7ceb3-233">設定 hello**強度**too100%按一下![Vamp UI-儲存](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png)toosave。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="7ceb3-234">Vamp 現在會傳送 hello 條件 （所有 Firefox 使用者） toosava:1.0.0 比對的所有流量。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![Vamp UI-套用條件 toogateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="7ceb3-236">最後，hello 閘道加權 toosend 所有剩餘的流量 （所有非 Firefox 使用者） toohello 新 sava: 1.1.0 調整。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="7ceb3-237">按一下![Vamp UI-編輯](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png)下一步太**加權**，以及設定 hello 加權散發，因此導向的 toohello 路由 sava/sava_cluster/sava:1.1.0/webport 100%。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="7ceb3-238">導向的 toohello 新 sava: 1.1.0 的現在不會篩選 hello 條件的所有流量都。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="7ceb3-239">toosee hello 篩選條件在動作中，開啟兩個不同的瀏覽器 （一個 Firefox 及其他瀏覽器），並同時從存取 hello sava 服務。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="7ceb3-240">Firefox 的所有要求會都傳送 toosava:1.0.0，而所有其他瀏覽器會導向的 toosava:1.1.0。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![Vamp UI - 篩選流量](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="7ceb3-242">總結</span><span class="sxs-lookup"><span data-stu-id="7ceb3-242">Summing up</span></span>

<span data-ttu-id="7ceb3-243">本文是快速介紹 tooVamp DC/OS 叢集上。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="7ceb3-244">首先，你 Vamp 和執行在您 Azure 容器服務 DC/OS 叢集中，部署與 Vamp 藍圖，服務和存取在 hello 公開端點 （閘道）。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="7ceb3-245">我們也觸及 Vamp 的某些功能強大的功能： 合併新服務 variant toohello 執行部署，而且導入它以累加的方式，則篩選流量 tooresolve 已知不相容。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7ceb3-246">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ceb3-246">Next steps</span></span>

* <span data-ttu-id="7ceb3-247">了解如何管理透過 hello Vamp 動作[Vamp REST API](http://vamp.io/documentation/api/api-reference/)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="7ceb3-248">在 Node.js 中建置 Vamp 自動化指令碼，並以 [Vamp 工作流程](http://vamp.io/documentation/tutorials/create-a-workflow/)來執行這些指令碼。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="7ceb3-249">請參閱其他 [VAMP 教學課程](http://vamp.io/documentation/tutorials/overview/)。</span><span class="sxs-lookup"><span data-stu-id="7ceb3-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

