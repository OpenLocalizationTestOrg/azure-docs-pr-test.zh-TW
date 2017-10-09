---
title: "aaaLoad 平衡在 Azure 中的 Kubernetes 容器 |Microsoft 文件"
description: "在 Azure Container Service 中由外部連接並針對 Kubernetes 叢集內的多個容器進行負載平衡。"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, 微服務, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>在 Azure Container Service 中針對 Kubernetes 叢集內的容器進行負載平衡 
本文將介紹在 Azure Container Service 中 Kubernetes 叢集內進行負載平衡。 負載平衡 hello 服務提供外部存取的 IP 位址，並將散發代理程式 Vm 中執行的 hello pod 之間的網路流量。

您可以設定 Kubernetes 服務 toouse [Azure 負載平衡器](../../load-balancer/load-balancer-overview.md)toomanage 外部網路 (TCP) 流量。 透過其他設定，便可以達成 HTTP 或 HTTPS 流量 (或更進階的案例) 的負載平衡和路由。

## <a name="prerequisites"></a>必要條件
* 在 Azure Container Service 中[部署 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)
* [將用戶端連線](../container-service-connect.md)tooyour 叢集

## <a name="azure-load-balancer"></a>Azure Load Balancer

根據預設，Kubernetes 叢集部署在 Azure 容器服務包括 Vm hello 代理程式 」 的網際網路對向 Azure 負載平衡器。 （個別負載平衡器資源 hello 主要 Vm 的設定）。Azure Load Balancer 是第 4 層負載平衡器。 目前，hello 負載平衡器只會支援 TCP 流量 Kubernetes 中。

建立 Kubernetes 服務時，您可以自動設定 hello Azure 負載平衡器 tooallow 存取 toohello 服務。 tooconfigure hello 負載平衡器集 hello 服務`type`太`LoadBalancer`。 hello 負載平衡器會建立規則 toomap 公用 IP 位址和連接埠號碼的連入服務流量 toohello 私人 IP 位址和連接埠號碼 hello pod 的代理程式 Vm 中 （反之亦然回應流量）。 

 下列兩個範例顯示如何 tooset hello Kubernetes 服務`type`太`LoadBalancer`。 （之後嘗試 hello 範例中，刪除 hello 部署如果不再需要）。

### <a name="example-use-hello-kubectl-expose-command"></a>範例： 使用 hello`kubectl expose`命令 
hello [Kubernetes 逐步解說](container-service-kubernetes-walkthrough.md)包含的範例 tooexpose 服務以 hello`kubectl expose`命令及其`--type=LoadBalancer`旗標。 Hello 步驟如下：

1. 啟動新的容器部署。 例如，hello 下列命令啟動新的部署呼叫`mynginx`。 hello 部署包含三個容器，根據 hello Nginx 網頁伺服器 hello Docker 映像。

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. 請確認正在 hello 容器。 例如，如果您查詢的 hello 容器`kubectl get pods`，您會看到類似 toohello 下列輸出：

    ![取得 Nginx 容器](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure hello 負載平衡器 tooaccept 外部流量 toohello 部署，執行`kubectl expose`與`--type=LoadBalancer`。 hello 下列命令會公開連接埠 80 上的 hello Nginx 伺服器：

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. 型別`kubectl get svc`toosee hello hello 叢集中的 hello 服務狀態。 雖然 hello 負載平衡器設定 hello 規則 hello `EXTERNAL-IP` hello 的服務，會顯示為`<pending>`。 請稍候幾分鐘設定 hello 外部 IP 位址： 

    ![設定 Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. 請確認您可以存取位於 hello 外部 IP 位址的 hello 服務。 例如，開啟所顯示的網頁瀏覽器 toohello IP 位址。 hello 瀏覽器會顯示執行其中 hello 容器中的 hello Nginx 網頁伺服器。 或者，執行的 hello`curl`或`wget`命令。 例如：

    ```
    curl 13.82.93.130
    ```

    您應該會看到如下的輸出：

    ![使用 curl 存取 Nginx](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. hello Azure 負載平衡器，請移 toohello toosee hello 組態[Azure 入口網站](https://portal.azure.com)。

7. 瀏覽的容器服務叢集中的 hello 資源群組，然後選取 hello hello 代理程式 Vm 的負載平衡器。 其名稱應該 hello 與 hello 容器服務相同。 (不選擇 hello hello 主要節點的負載平衡器，其名稱包含一個 hello **master lb**。) 

    ![資源群組中的負載平衡器](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. toosee hello 詳細資料的 hello 負載平衡器組態，按一下**負載平衡規則**和 hello hello 規則的設定名稱。

    ![負載平衡器規則](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>範例： 指定`type: LoadBalancer`hello 服務組態檔中

如果您部署 Kubernetes 容器應用程式從 YAML 或 JSON[服務組態檔](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file)，加入下列行 toohello 服務規格的 hello 來指定外部負載平衡器：

```YAML
 "type": "LoadBalancer"
``` 



hello 下列步驟使用 hello Kubernetes[訪客簿範例](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook)。 此範例是以 Redis 和 PHP Docker 映像為基礎的多層式 Web 應用程式。 您可以在 hello 服務組態檔中指定該 hello 前端 PHP 伺服器使用 hello Azure 負載平衡器。

1. 下載 hello 檔案`guestbook-all-in-one.yaml`從[GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one)。 
2. 瀏覽 hello `spec` hello`frontend`服務。
3. Hello 行取消註解`type: LoadBalancer`。

    ![服務組態中的負載平衡器](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. 儲存 hello 檔案，並部署 hello 應用程式藉由執行下列命令的 hello:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. 型別`kubectl get svc`toosee hello hello 叢集中的 hello 服務狀態。 雖然 hello 負載平衡器設定 hello 規則 hello`EXTERNAL-IP`的 hello`frontend`服務會顯示為`<pending>`。 請稍候幾分鐘設定 hello 外部 IP 位址： 

    ![設定 Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. 請確認您可以存取位於 hello 外部 IP 位址的 hello 服務。 例如，您可以開啟網頁瀏覽器 toohello 外部 IP 位址的 hello 服務。

    ![外部存取訪客留言](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    您可以加入訪客留言項目。

7. hello Azure 負載平衡器，瀏覽 hello 中的 hello 叢集 hello 負載平衡器資源 toosee hello 組態[Azure 入口網站](https://portal.azure.com)。 請參閱 hello hello 前一個範例中的步驟。

### <a name="considerations"></a>考量

* Hello 負載平衡器規則的建立會以非同步方式時發生，並且在 hello 服務會發行有關佈建的 hello 平衡器資訊`status.loadBalancer`欄位。
* 每個服務會自動指派自己 hello 負載平衡器中的虛擬 IP 位址。
* 如果您想 tooreach hello 負載平衡器 DNS 名稱時，使用您的網域服務提供者 toocreate hello 規則的 IP 位址的 DNS 名稱。

## <a name="http-or-https-traffic"></a>HTTP 或 HTTPS 流量

tooload 平衡 HTTP 或 HTTPS 流量 toocontainer web 應用程式和管理的傳輸層安全性 (TLS) 憑證，您可以使用 hello Kubernetes[輸入](https://kubernetes.io/docs/user-guide/ingress/)資源。 輸入是規則以允許傳入的連接 tooreach hello 叢集服務的集合。 輸入資源 toowork，hello Kubernetes 叢集必須有[輸入控制器](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers)執行。

Azure Container Service 不會自動實作 Kubernetes 輸入控制器。 有數個控制器實作可供使用。 目前，hello [Nginx 輸入控制器](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx)建議 tooconfigure 輸入規則和負載平衡 HTTP 及 HTTPS 流量。 

如需詳細資訊，請參閱 hello [Nginx 輸入控制器文件集](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md)。

> [!IMPORTANT]
> 當 Azure 容器服務中使用 hello Nginx 輸入控制站，您必須公開 hello 控制站部署成與服務`type: LoadBalancer`。 這會設定 hello Azure 負載平衡器 tooroute 流量 toohello 控制站。 如需詳細資訊，請參閱 hello 上一節。


## <a name="next-steps"></a>後續步驟

* 請參閱 hello [Kubernetes 負載平衡器文件](https://kubernetes.io/docs/user-guide/load-balancer/)
* 深入了解 [Kubernetes 輸入和輸入控制器 (英文)](https://kubernetes.io/docs/user-guide/ingress/)
* 請參閱 [Kubernetes 範例 (英文)](https://github.com/kubernetes/kubernetes/tree/master/examples)

