---
title: "在 Azure Kubernetes 中運用 Helm 部署容器 |Microsoft Docs"
description: "使用 Helm 封裝工具， 在 Azure Container Service 中將容器部署在 Kubernetes 叢集"
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
ms.openlocfilehash: 3cfcc5abbee03ca8fbbec4e4eae711e7c2d9deae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-helm-to-deploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="0d056-103">使用 Helm 在 Kubernetes 叢集部署容器</span><span class="sxs-lookup"><span data-stu-id="0d056-103">Use Helm to deploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="0d056-104">[Helm](https://github.com/kubernetes/helm/) 是開放原始碼的封裝工具，可協助您安裝和管理 Kubernetes 應用程式的生命週期。</span><span class="sxs-lookup"><span data-stu-id="0d056-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="0d056-105">Helm 類似於 Apt-get 和 Yum 等 Linux 封裝管理工具，可用於管理 Kubernetes 圖表 (即預先設定的 Kubernetes 資源封裝)。</span><span class="sxs-lookup"><span data-stu-id="0d056-105">Similar to Linux package managers such as Apt-get and Yum, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="0d056-106">本文將說明如何在部署於 Azure Container Service 中的 Kubernetes 叢集使用 Helm。</span><span class="sxs-lookup"><span data-stu-id="0d056-106">This article shows you how to work with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="0d056-107">Helm 包含兩個元件︰</span><span class="sxs-lookup"><span data-stu-id="0d056-107">Helm has two components:</span></span> 
* <span data-ttu-id="0d056-108">Helm CLI是在本機或雲端執行的用戶端</span><span class="sxs-lookup"><span data-stu-id="0d056-108">The **Helm CLI** is a client that runs on your machine locally or in the cloud</span></span>  

* <span data-ttu-id="0d056-109">Tiller是在 Kubernetes 叢集執行的伺服器，管理 Kubernetes 應用程式的生命週期</span><span class="sxs-lookup"><span data-stu-id="0d056-109">**Tiller** is a server that runs on the Kubernetes cluster and manages the lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="0d056-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d056-110">Prerequisites</span></span>

* <span data-ttu-id="0d056-111">在 Azure Container Service 中[建立 Kubernetes 叢集](container-service-kubernetes-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="0d056-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="0d056-112">在本機[安裝和設定 `kubectl`](../container-service-connect.md)</span><span class="sxs-lookup"><span data-stu-id="0d056-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="0d056-113">在本機[安裝 Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md)</span><span class="sxs-lookup"><span data-stu-id="0d056-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="0d056-114">Helm 基本概念</span><span class="sxs-lookup"><span data-stu-id="0d056-114">Helm basics</span></span> 

<span data-ttu-id="0d056-115">若要檢視您安裝 Tiller 及部署您應用程式的 Kubernetes 叢集的相關資訊，請輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="0d056-115">To view information about the Kubernetes cluster that you are installing Tiller and deploying your applications to, type the following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl 叢集資訊](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="0d056-117">安裝 Helm 之後，輸入下列命令，便可在 Kubernetes 叢集安裝 Tiller︰</span><span class="sxs-lookup"><span data-stu-id="0d056-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing the following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="0d056-118">順利完成後，您會看到如下所示的輸出︰</span><span class="sxs-lookup"><span data-stu-id="0d056-118">When it completes successfully, you see output like the following:</span></span>

![Tiller 安裝](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="0d056-120">若要檢視存放庫中所有的 Helm 圖表，輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="0d056-120">To view all the Helm charts available in the repository, type the following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="0d056-121">您應該會看到如以下的輸出：</span><span class="sxs-lookup"><span data-stu-id="0d056-121">You see output like the following:</span></span>

![Helm 搜尋](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="0d056-123">若要更新圖表以取得最新版本，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="0d056-123">To update the charts to get the latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="0d056-124">部署 Nginx 輸入控制器圖表</span><span class="sxs-lookup"><span data-stu-id="0d056-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="0d056-125">若要部署 Nginx 輸入控制器圖表，請輸入單一命令︰</span><span class="sxs-lookup"><span data-stu-id="0d056-125">To deploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![部署輸入控制器](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="0d056-127">如果您輸入 `kubectl get svc` 來檢視所有在叢集執行的服務，您會看到 IP 位址指派至輸入控制器。</span><span class="sxs-lookup"><span data-stu-id="0d056-127">If you type `kubectl get svc` to view all services that are running on the cluster, you see that an IP address is assigned to the ingress controller.</span></span> <span data-ttu-id="0d056-128">(如果指派進行中，您會看到 `<pending>`。</span><span class="sxs-lookup"><span data-stu-id="0d056-128">(While the assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="0d056-129">它需要幾分鐘來完成。)</span><span class="sxs-lookup"><span data-stu-id="0d056-129">It takes a couple of minutes to complete.)</span></span> 

<span data-ttu-id="0d056-130">指派 IP 位址後，瀏覽至外部 IP 位址的值，以查看 Nginx 後端執行。</span><span class="sxs-lookup"><span data-stu-id="0d056-130">After the IP address is assigned, navigate to the value of the external IP address to see the Nginx backend running.</span></span> 
 
![輸入 IP 位址](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="0d056-132">若要查看安裝於叢集上的圖表清單，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="0d056-132">To see a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="0d056-133">您可以將命令縮寫成 `helm ls`。</span><span class="sxs-lookup"><span data-stu-id="0d056-133">You can abbreviate the command to `helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="0d056-134">部署 MariaDB 圖表和用戶端</span><span class="sxs-lookup"><span data-stu-id="0d056-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="0d056-135">現在部署 MariaDB 圖表和 MariaDB 用戶端來連接至資料庫。</span><span class="sxs-lookup"><span data-stu-id="0d056-135">Now deploy a MariaDB chart and a MariaDB client to connect to the database.</span></span>

<span data-ttu-id="0d056-136">若要部署 MariaDB 圖表，輸入下列命令︰</span><span class="sxs-lookup"><span data-stu-id="0d056-136">To deploy the MariaDB chart, type the following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="0d056-137">其中 `--name` 是用於標示版本的標記。</span><span class="sxs-lookup"><span data-stu-id="0d056-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="0d056-138">如果部署失敗，執行 `helm repo update`，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="0d056-138">If the deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="0d056-139">若要檢視部署在叢集中的所有圖表，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="0d056-139">To view all the charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="0d056-140">若要檢視執行在叢集中的所有部署，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="0d056-140">To view all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="0d056-141">最後，若要執行 Pod 來存取用戶端，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="0d056-141">Finally, to run a pod to access the client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="0d056-142">若要連接至用戶端，請輸入下列命令，將 `v1-mariadb` 更換為您的部署名稱︰</span><span class="sxs-lookup"><span data-stu-id="0d056-142">To connect to the client, type the following command, replacing `v1-mariadb` with the name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="0d056-143">您現在可以使用標準 SQL 命令來建立資料庫、資料表等。例如，`Create DATABASE testdb1;` 會建立空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="0d056-143">You can now use standard SQL commands to create databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="0d056-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d056-144">Next steps</span></span>

* <span data-ttu-id="0d056-145">如需管理 Kubernetes 圖表的詳細資訊，請參閱[Helm 文件](https://github.com/kubernetes/helm/blob/master/docs/index.md)。</span><span class="sxs-lookup"><span data-stu-id="0d056-145">For more information about managing Kubernetes charts, see the [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

