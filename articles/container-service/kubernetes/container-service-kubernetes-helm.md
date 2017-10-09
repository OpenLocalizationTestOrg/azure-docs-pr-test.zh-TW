---
title: "在 Azure Kubernetes 頭盔 aaaDeploy 容器 |Microsoft 文件"
description: "Hello 頭盔封裝工具 toodeploy 容器的叢集上使用 Kubernetes Azure 容器服務"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>在 Kubernetes 叢集上使用頭盔 toodeploy 容器 

[頭盔](https://github.com/kubernetes/helm/)是開放原始碼封裝的工具，可協助您安裝和管理 hello Kubernetes 應用程式生命週期。 例如 Apt get 和 Yum 類似 tooLinux 封裝管理員，頭盔是使用的 toomanage Kubernetes 圖表，也就是預先設定的 Kubernetes 資源的封裝。 本文章將示範如何 toowork 與頭盔 Kubernetes 叢集上部署在 Azure 容器服務中。

Helm 包含兩個元件︰ 
* hello**頭盔 CLI**是本機或 hello 雲端中執行您的電腦的用戶端  

* **Tiller**是 hello Kubernetes 叢集上執行及管理 hello Kubernetes 應用程式的生命週期的伺服器 
 
## <a name="prerequisites"></a>必要條件

* 在 Azure Container Service 中[建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)

* 在本機[安裝和設定 `kubectl`](../container-service-connect.md)

* 在本機[安裝 Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md)

## <a name="helm-basics"></a>Helm 基本概念 

tooview 有關 hello Kubernetes 叢集您安裝 Tiller 與部署您的應用程式，輸入下列命令的 hello:

```bash
kubectl cluster-info 
```
![kubectl 叢集資訊](./media/container-service-kubernetes-helm/clusterinfo.png)
 
安裝頭盔之後，輸入下列命令的 hello Tiller 安裝 Kubernetes 叢集上：

```bash
helm init --upgrade
```
順利完成，您會看到類似 hello 下列輸出：

![Tiller 安裝](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview hello 頭盔中的所有圖表可用 hello 儲存機制，型別 hello 下列都命令：

```bash 
helm search 
```

您會看到類似 hello 下列輸出：

![Helm 搜尋](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate hello 圖表 tooget hello 最新版本中，輸入：

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>部署 Nginx 輸入控制器圖表 
 
toodeploy Nginx 輸入控制器圖表中，輸入單一命令：

```bash
helm install stable/nginx-ingress 
```
![部署輸入控制器](./media/container-service-kubernetes-helm/nginx-ingress.png)

如果您輸入`kubectl get svc`tooview 您 hello 叢集執行的所有服務，都看到 toohello 輸入控制站指派的 IP 位址。 (雖然 hello 分派正在進行中，您會看到`<pending>`。 它需要數分鐘 toocomplete。） 

Hello IP 位址指派之後，瀏覽 toohello hello 外部 IP 位址 toosee hello Nginx 後端執行值。 
 
![輸入 IP 位址](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee 一份圖表在叢集上安裝，類型：

```bash
helm list 
```

您可以 hello 將命令縮寫太`helm ls`。
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>部署 MariaDB 圖表和用戶端

現在部署 MariaDB 圖表和 MariaDB 用戶端 tooconnect toohello 資料庫。

toodeploy hello MariaDB 圖表，下列命令的型別 hello:

```bash
helm install --name v1 stable/mariadb
```

其中 `--name` 是用於標示版本的標記。

> [!TIP]
> 如果 hello 部署失敗，執行`helm repo update`並再試一次。
>
 
 
tooview 所有 hello 圖表都部署在您的叢集類型：

```bash 
helm list
```
 
tooview 所有部署執行您在叢集上，都輸入：

```bash
kubectl get deployments 
``` 
 
 
最後，toorun pod tooaccess hello 用戶端類型：

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
tooconnect toohello 用戶端，下列命令、 取代型別 hello `v1-mariadb` hello 名稱，為您的部署：

```bash
sudo mysql –h v1-mariadb
```
 
 
您現在可以使用標準 SQL 命令 toocreate 資料庫、 資料表等。例如，`Create DATABASE testdb1;` 會建立空白資料庫。 
 
 
 
## <a name="next-steps"></a>後續步驟

* 如需管理 Kubernetes 圖表的詳細資訊，請參閱 hello[頭盔文件](https://github.com/kubernetes/helm/blob/master/docs/index.md)。 

