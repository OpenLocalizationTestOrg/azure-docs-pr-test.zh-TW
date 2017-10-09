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
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="e8674-103">在 Kubernetes 叢集上使用頭盔 toodeploy 容器</span><span class="sxs-lookup"><span data-stu-id="e8674-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="e8674-104">[頭盔](https://github.com/kubernetes/helm/)是開放原始碼封裝的工具，可協助您安裝和管理 hello Kubernetes 應用程式生命週期。</span><span class="sxs-lookup"><span data-stu-id="e8674-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="e8674-105">例如 Apt get 和 Yum 類似 tooLinux 封裝管理員，頭盔是使用的 toomanage Kubernetes 圖表，也就是預先設定的 Kubernetes 資源的封裝。</span><span class="sxs-lookup"><span data-stu-id="e8674-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="e8674-106">本文章將示範如何 toowork 與頭盔 Kubernetes 叢集上部署在 Azure 容器服務中。</span><span class="sxs-lookup"><span data-stu-id="e8674-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="e8674-107">Helm 包含兩個元件︰</span><span class="sxs-lookup"><span data-stu-id="e8674-107">Helm has two components:</span></span> 
* <span data-ttu-id="e8674-108">hello**頭盔 CLI**是本機或 hello 雲端中執行您的電腦的用戶端</span><span class="sxs-lookup"><span data-stu-id="e8674-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="e8674-109">**Tiller**是 hello Kubernetes 叢集上執行及管理 hello Kubernetes 應用程式的生命週期的伺服器</span><span class="sxs-lookup"><span data-stu-id="e8674-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="e8674-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e8674-110">Prerequisites</span></span>

* <span data-ttu-id="e8674-111">在 Azure Container Service 中[建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="e8674-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="e8674-112">在本機[安裝和設定 `kubectl`](../container-service-connect.md)</span><span class="sxs-lookup"><span data-stu-id="e8674-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="e8674-113">在本機[安裝 Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md)</span><span class="sxs-lookup"><span data-stu-id="e8674-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="e8674-114">Helm 基本概念</span><span class="sxs-lookup"><span data-stu-id="e8674-114">Helm basics</span></span> 

<span data-ttu-id="e8674-115">tooview 有關 hello Kubernetes 叢集您安裝 Tiller 與部署您的應用程式，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="e8674-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl 叢集資訊](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="e8674-117">安裝頭盔之後，輸入下列命令的 hello Tiller 安裝 Kubernetes 叢集上：</span><span class="sxs-lookup"><span data-stu-id="e8674-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="e8674-118">順利完成，您會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e8674-118">When it completes successfully, you see output like hello following:</span></span>

![Tiller 安裝](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="e8674-120">tooview hello 頭盔中的所有圖表可用 hello 儲存機制，型別 hello 下列都命令：</span><span class="sxs-lookup"><span data-stu-id="e8674-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="e8674-121">您會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e8674-121">You see output like hello following:</span></span>

![Helm 搜尋](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="e8674-123">tooupdate hello 圖表 tooget hello 最新版本中，輸入：</span><span class="sxs-lookup"><span data-stu-id="e8674-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="e8674-124">部署 Nginx 輸入控制器圖表</span><span class="sxs-lookup"><span data-stu-id="e8674-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="e8674-125">toodeploy Nginx 輸入控制器圖表中，輸入單一命令：</span><span class="sxs-lookup"><span data-stu-id="e8674-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![部署輸入控制器](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="e8674-127">如果您輸入`kubectl get svc`tooview 您 hello 叢集執行的所有服務，都看到 toohello 輸入控制站指派的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e8674-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="e8674-128">(雖然 hello 分派正在進行中，您會看到`<pending>`。</span><span class="sxs-lookup"><span data-stu-id="e8674-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="e8674-129">它需要數分鐘 toocomplete。）</span><span class="sxs-lookup"><span data-stu-id="e8674-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="e8674-130">Hello IP 位址指派之後，瀏覽 toohello hello 外部 IP 位址 toosee hello Nginx 後端執行值。</span><span class="sxs-lookup"><span data-stu-id="e8674-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![輸入 IP 位址](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="e8674-132">toosee 一份圖表在叢集上安裝，類型：</span><span class="sxs-lookup"><span data-stu-id="e8674-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="e8674-133">您可以 hello 將命令縮寫太`helm ls`。</span><span class="sxs-lookup"><span data-stu-id="e8674-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="e8674-134">部署 MariaDB 圖表和用戶端</span><span class="sxs-lookup"><span data-stu-id="e8674-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="e8674-135">現在部署 MariaDB 圖表和 MariaDB 用戶端 tooconnect toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e8674-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="e8674-136">toodeploy hello MariaDB 圖表，下列命令的型別 hello:</span><span class="sxs-lookup"><span data-stu-id="e8674-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="e8674-137">其中 `--name` 是用於標示版本的標記。</span><span class="sxs-lookup"><span data-stu-id="e8674-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="e8674-138">如果 hello 部署失敗，執行`helm repo update`並再試一次。</span><span class="sxs-lookup"><span data-stu-id="e8674-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="e8674-139">tooview 所有 hello 圖表都部署在您的叢集類型：</span><span class="sxs-lookup"><span data-stu-id="e8674-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="e8674-140">tooview 所有部署執行您在叢集上，都輸入：</span><span class="sxs-lookup"><span data-stu-id="e8674-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="e8674-141">最後，toorun pod tooaccess hello 用戶端類型：</span><span class="sxs-lookup"><span data-stu-id="e8674-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="e8674-142">tooconnect toohello 用戶端，下列命令、 取代型別 hello `v1-mariadb` hello 名稱，為您的部署：</span><span class="sxs-lookup"><span data-stu-id="e8674-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="e8674-143">您現在可以使用標準 SQL 命令 toocreate 資料庫、 資料表等。例如，`Create DATABASE testdb1;` 會建立空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="e8674-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="e8674-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8674-144">Next steps</span></span>

* <span data-ttu-id="e8674-145">如需管理 Kubernetes 圖表的詳細資訊，請參閱 hello[頭盔文件](https://github.com/kubernetes/helm/blob/master/docs/index.md)。</span><span class="sxs-lookup"><span data-stu-id="e8674-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

