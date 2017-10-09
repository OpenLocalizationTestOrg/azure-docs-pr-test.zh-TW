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
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Azure Container Service DC/OS 叢集上具備 Vamp 的 Canary 版本微服務

在本逐步解說中，我們會在具備 DC/OS 叢集的 Azure Container Service 上設定 Vamp。 我們加那利版本 hello Vamp 示範服務 」 sava 」，並解決不相容的 Firefox hello 服務套用智慧的流量篩選。 

> [!TIP] 
> 在本逐步解說 Vamp 叢集上執行的 DC/OS，但您也可以使用 Vamp Kubernetes 為 hello 協調者。
>

## <a name="about-canary-releases-and-vamp"></a>關於 Canary 版本與 Vamp


[Canary 版本](https://martinfowler.com/bliki/CanaryRelease.html)是諸如 Netflix、Facebook 和 Spotify 等創新組織所採用的智慧型部署策略。 它是個很適切的方法，因為它能減少問題、引入網路安全性，並提升創新技術。 那為什麼並非所有公司都使用它？ 擴充 CI/CD 管線 tooinclude 加那利策略會增加複雜性，而且需要更詳盡的 devops 知識和經驗。 這是足夠 tooblock 小公司與企業深入見解它們甚至開始之前。 

[Vamp](http://vamp.io/)是設計的開放原始碼系統 tooease 這項轉換，並讓加那利釋放功能 tooyour 慣用容器排程器。 Vamp 的 Canary 功能並不僅是以百分比為基礎的發行。 可篩選及分散於各種不同的條件，例如 tootarget 特定使用者、 IP 範圍或裝置上的流量。 Vamp 會追蹤和分析效能計量，允許以實際資料作為基礎進行自動化。 您可以設定錯誤的自動復原，或以負載或延遲作為基礎，將個別服務變化進行調整。

## <a name="set-up-azure-container-service-with-dcos"></a>使用 DC/OS 設定 Azure Container Service



1. 使用一個主機和兩個預設大小的代理程式來[部署 DC/OS 叢集](container-service-deployment.md)。 

2. [建立的 SSH 通道](../container-service-connect.md)tooconnect toohello DC/OS 叢集。 本文假設您建立通道 toohello 本機通訊埠 80 上的叢集。


## <a name="set-up-vamp"></a>設定 Vamp

既然您已執行的 DC/OS 叢集，您可以安裝 Vamp 從 hello DC/OS UI (http://localhost:80)。 

![DC/OS UI](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

會在兩個階段中完成安裝︰

1. **部署 Elasticsearch**。

2. 然後**部署 Vamp**安裝 hello Vamp DC/OS universe 套件。

### <a name="deploy-elasticsearch"></a>部署 Elasticsearch

Vamp 需要 Elasticsearch 來進行計量收集和彙總。 您可以使用 hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy 相容的 Vamp Elasticsearch 堆疊。

1. 在 hello DC/OS UI，移過**服務**按一下**部署服務**。

2. 選取**JSON 模式**從 hello**部署新服務**快顯。

  ![選取 JSON 模式](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. 下列 JSON hello 中貼上。 此設定為 1 GB 的 RAM 與 hello Elasticsearch 連接埠上的基本健全狀況檢查執行 hello 容器。
  
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
  

3. 按一下 [ **部署**]。

  DC/OS 部署 hello Elasticsearch 容器。 您可以在 hello 上追蹤進度**服務**頁面。  

  ![部署 e?Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>部署 Vamp

一旦 Elasticsearch 報告為**執行**，您可以加入 hello Vamp DC/OS Universe 封裝。 

1. 跳過**Universe**並搜尋**vamp**。 
  ![DC/OS Universe 上的 Vamp](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. 按一下**安裝**下一步 toohello vamp 封裝，然後選擇 **進階安裝**。

3. 向下捲動並輸入下列 elasticsearch url hello: `http://elasticsearch.marathon.mesos:9200`。 

  ![輸入 Elasticsearch URL](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. 按一下**檢閱和安裝**，然後按一下 **安裝**toostart hello 部署。  

  DC/OS 會部署所有必要的 Vamp 元件。 您可以在 hello 上追蹤進度**服務**頁面。
  
  ![部署 Vamp 作為 Universe 套件](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. 一旦完成部署之後，您可以存取 hello Vamp UI:

  ![DC/OS 上的 Vamp 服務](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp UI](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>部署您的第一個服務

現在該 Vamp 已啟動並且執行中，請從藍圖部署服務。 

最簡單的形式， [Vamp 藍圖](http://vamp.io/documentation/using-vamp/blueprints/)描述 hello 端點 （閘道）、 叢集，以及服務 toodeploy。 Vamp 使用叢集 toogroup 不同的各樣 hello 相同服務成邏輯群組加那利釋出或 A / B 測試。  

此案例中使用的範例整合型應用程式稱為 [**sava**](https://github.com/magneticio/sava)，為 1.0 版。 hello monolith 會封裝在 Docker 容器，也就是在 Docker Hub magneticio/sava:1.0.0 下。 hello 應用程式通常會執行連接埠 8080，但是您想要在此情況下連接埠 9050 tooexpose。 部署使用簡單的藍圖 Vamp 透過 hello 應用程式。

1. 跳過**部署**。

2. 按一下 [新增] 。

3. 貼上的下列 hello 藍圖 YAML。 此藍圖所包含的一個叢集只有一個服務變化，我們將在稍後步驟中進行變更︰

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

4. 按一下 [儲存] 。 Vamp 起始 hello 部署。

hello 部署會列在 hello**部署**頁面。 按一下 hello 部署 toomonitor 其狀態。

![Vamp UI - 部署 sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Vamp UI 中的 sava 服務](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

建立這兩個閘道，這會列在 hello**閘道**頁面：

* 執行服務 （連接埠 9050） 穩定端點 tooaccess hello 
* 受 Vamp 管理的內部閘道 (稍後將詳細說明此閘道)。 

![Vamp UI - sava 閘道](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

hello sava 服務現在已部署，但是您無法存取，外部因為 hello Azure 負載平衡器並不知道 tooforward 流量 tooit 尚未。 tooaccess hello 服務，更新 hello Azure 網路組態。


## <a name="update-hello-azure-network-configuration"></a>更新 hello Azure 網路組態

Vamp hello DC/OS 代理程式節點，公開連接埠 9050 穩定端點上的已部署的 hello sava 服務。 從外部 hello DC/OS 叢集中的 tooaccess hello 服務進行下列變更 toohello Azure 網路組態，在叢集部署的 hello: 

1. **設定 hello Azure 負載平衡器**hello 代理程式 (hello 名為資源**dcos 代理程式-lb xxxx**) 以健全狀況探查和規則 tooforward 流量在連接埠 9050 toohello sava 執行個體上的。 

2. **更新 hello 網路安全性群組**hello 公用代理程式 (hello 名為資源**XXXX-代理程式-公用-nsg-XXXX**) 連接埠 9050 tooallow 流量。

使用這些工作的詳細的步驟 toocomplete hello Azure 入口網站，請參閱[啟用公用存取 tooan Azure 容器服務應用程式](container-service-enable-public-access.md)。 針對所有連接埠設定指定連接埠 9050。


一旦建立的所有項目，請移 toohello**概觀**刀鋒視窗中的 hello DC/OS 代理程式負載平衡器 (hello 名為資源**dcos 代理程式-lb xxxx**)。 尋找 hello**公用 IP 位址**，並使用連接埠 9050 hello 位址 tooaccess sava。

![Azure 入口網站 - 取得公用 IP 位址](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>執行 Canary 版本

假設您有此應用程式的新版本，您想 toocanary 發行至實際執行環境。 您將它當做 magneticio/sava:1.1.0 容器化並準備好 toogo。 Vamp 可讓您輕鬆地將新的服務 toohello 執行部署。 這些 「 合併 」 服務會與 hello hello 叢集中現有的服務一起部署，而指派的權數為 0%。 沒有流量是新合併的 tooa 路由的服務，直到您調整 hello 流量分配。 hello Vamp UI 中的 hello 加權滑桿可讓您完全控制 hello 分佈，以便進行累加式調整 (加那利 release) 或立即回復。

### <a name="merge-a-new-service-variant"></a>合併新的服務變化

toomerge hello 新 sava 1.1 的服務以執行部署的 hello:

1. 在 hello Vamp UI 中，按一下 **藍圖**。

2. 按一下**新增**和貼上的下列 hello 藍圖 YAML： 此藍圖描述新的服務變數 (sava: 1.1.0) toodeploy hello 現有叢集 (sava_cluster) 內。

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
  
3. 按一下 [儲存] 。 儲存並且列在 hello hello 藍圖**藍圖**頁面。

4. 開啟 hello hello sava: 1.1 藍圖，然後按一下 [動作] 功能表**合併至**。

  ![Vamp UI - 藍圖](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. 選取 hello **sava**部署，然後按一下**合併**。

  ![Vamp UI-合併藍圖 toodeployment](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp 部署 hello 新 sava: 1.1.0 服務 variant hello 藍圖連同 sava: 1.0.0 hello 中所述**sava_cluster**的 hello 執行部署。 

![Vamp UI - 更新的 sava 部署](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

hello **sava/sava_cluster/webport**閘道 （hello 叢集端點），也會更新，新加入路由 toohello 部署 sava: 1.1.0。 此時，沒有流量路由傳送這裡 (hello**加權**設定 too0%)。

![Vamp UI - 叢集閘道](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Canary 版本

這兩個版本的 sava 部署在 hello 相同叢集，請調整移動 hello 這兩者之間的流量 hello 分佈**加權**滑桿。

1. 按一下![Vamp UI-編輯](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png)下一步太**加權**。

2. 設定 hello 加權發佈 too50%/50%並按一下**儲存**。

  ![Vamp UI - 閘道權數滑桿](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. 返回 tooyour 瀏覽器，並重新整理 hello sava 頁面數次。 hello sava 應用程式現在會 sava: 1.0 頁面和 sava: 1.1 頁面之間切換。

  ![將 sava1.0 和 sava1.1 服務進行交替](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > 這個替代 hello 頁面的最適合搭配 hello"Incognito 」 或 「 匿名 」 模式，在瀏覽器因為 hello 快取的靜態資產。
  >

### <a name="filter-traffic"></a>篩選流量

假設您在部署之後發現 sava:1.1.0 中發生不相容，而造成 Firefox 瀏覽器中的顯示問題。 您可以設定 Vamp toofilter 連入流量，並指示所有 Firefox 使用者都回 toohello 已知穩定 sava: 1.0.0。 此篩選條件立即解析 hello Firefox 使用者的干擾，同時其他人仍繼續 tooenjoy hello 優點 hello 改善 sava: 1.1.0。

Vamp 使用**條件**toofilter 流量之間閘道的路由。 流量會先經過篩選，而且導向相應 toohello 套用條件 tooeach 路由。 所有剩餘的流量會分散根據 toohello 閘道權重設定。

您可以建立條件 toofilter Firefox 的所有使用者，並將他們導向 toohello 舊 sava: 1.0.0:

1. 在 hello sava/sava_cluster/webport**閘道**頁面上，按一下![Vamp UI-編輯](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png)tooadd**條件**toohello 路由 sava/sava_cluster/sava:1.0.0/webport。 

2. 輸入 hello 條件**使用者代理程式 = = Firefox**按一下![Vamp UI-儲存](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png)。

  Vamp hello 將條件加入與預設長度為 0%。 toostart 篩選流量，您需要 tooadjust hello 條件強度。

3. 按一下![Vamp UI-編輯](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png)toochange hello**強度**套用 toohello 條件。
 
4. 設定 hello**強度**too100%按一下![Vamp UI-儲存](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png)toosave。

  Vamp 現在會傳送 hello 條件 （所有 Firefox 使用者） toosava:1.0.0 比對的所有流量。

  ![Vamp UI-套用條件 toogateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. 最後，hello 閘道加權 toosend 所有剩餘的流量 （所有非 Firefox 使用者） toohello 新 sava: 1.1.0 調整。 按一下![Vamp UI-編輯](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png)下一步太**加權**，以及設定 hello 加權散發，因此導向的 toohello 路由 sava/sava_cluster/sava:1.1.0/webport 100%。

  導向的 toohello 新 sava: 1.1.0 的現在不會篩選 hello 條件的所有流量都。

6. toosee hello 篩選條件在動作中，開啟兩個不同的瀏覽器 （一個 Firefox 及其他瀏覽器），並同時從存取 hello sava 服務。 Firefox 的所有要求會都傳送 toosava:1.0.0，而所有其他瀏覽器會導向的 toosava:1.1.0。

  ![Vamp UI - 篩選流量](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>總結

本文是快速介紹 tooVamp DC/OS 叢集上。 首先，你 Vamp 和執行在您 Azure 容器服務 DC/OS 叢集中，部署與 Vamp 藍圖，服務和存取在 hello 公開端點 （閘道）。

我們也觸及 Vamp 的某些功能強大的功能： 合併新服務 variant toohello 執行部署，而且導入它以累加的方式，則篩選流量 tooresolve 已知不相容。


## <a name="next-steps"></a>後續步驟

* 了解如何管理透過 hello Vamp 動作[Vamp REST API](http://vamp.io/documentation/api/api-reference/)。

* 在 Node.js 中建置 Vamp 自動化指令碼，並以 [Vamp 工作流程](http://vamp.io/documentation/tutorials/create-a-workflow/)來執行這些指令碼。

* 請參閱其他 [VAMP 教學課程](http://vamp.io/documentation/tutorials/overview/)。

