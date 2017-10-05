---
title: "Azure Container Service 教學課程 - 部署叢集 | Microsoft Docs"
description: "Azure Container Service 教學課程 - 部署叢集"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 472697c1f0c18859087d7b448e1786d85c27aca0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="778bd-104">在 Azure Container Service 中部署 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="778bd-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="778bd-105">Kubernetes 會提供容器化應用程式的分散式平台。</span><span class="sxs-lookup"><span data-stu-id="778bd-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="778bd-106">透過 Azure Container Service，可簡單又快速地佈建生產環境就緒 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="778bd-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="778bd-107">在本教學課程的第 3 和第 7 部分中，已部署一個 Azure Container Service Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="778bd-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="778bd-108">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="778bd-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="778bd-109">部署 Kubernetes ACS 叢集</span><span class="sxs-lookup"><span data-stu-id="778bd-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="778bd-110">安裝 Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="778bd-110">Installation of the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="778bd-111">設定 kubectl</span><span class="sxs-lookup"><span data-stu-id="778bd-111">Configuration of kubectl</span></span>

<span data-ttu-id="778bd-112">在後續的教學課程中，會相應放大、更新 Azure Vote 應用程式，且會將 Operations Management Suite 設定為監視 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="778bd-112">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="778bd-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="778bd-113">Before you begin</span></span>

<span data-ttu-id="778bd-114">在先前的教學課程中，已建立容器映像並上傳到 Azure Container Registry 執行個體。</span><span class="sxs-lookup"><span data-stu-id="778bd-114">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span></span> <span data-ttu-id="778bd-115">如果您尚未完成這些步驟，而想要跟著做，請回到[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="778bd-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="778bd-116">建立 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="778bd-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="778bd-117">在[上一個教學課程](./container-service-tutorial-kubernetes-prepare-acr.md)中，已建立名為 *myResourceGroup* 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="778bd-117">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="778bd-118">如果您尚未這樣做，請立即建立此資源群組。</span><span class="sxs-lookup"><span data-stu-id="778bd-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="778bd-119">使用 [az acs create](/cli/azure/acs#create) 命令，在 Azure Container Service 中建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="778bd-119">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="778bd-120">下列範例會建立一個名為 *myK8sCluster* 的叢集，其中包含一個 Linux 主要節點和三個 Linux 代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="778bd-120">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="778bd-121">幾分鐘之後，此命令就會完成，並以 json 格式傳回 ACS 部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="778bd-121">After several minutes, the command completes, and returns json formatted information about the ACS deployment.</span></span>

## <a name="install-the-kubectl-cli"></a><span data-ttu-id="778bd-122">安裝 kubectl CLI</span><span class="sxs-lookup"><span data-stu-id="778bd-122">Install the kubectl CLI</span></span>

<span data-ttu-id="778bd-123">若要從用戶端電腦連線到 Kubernetes 叢集，請使用 [kubectl](https://kubernetes.io/docs/user-guide/kubectl/) (Kubernetes 命令列用戶端)。</span><span class="sxs-lookup"><span data-stu-id="778bd-123">To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="778bd-124">如果您是使用 Azure CloudShell，就已安裝 `kubectl`。</span><span class="sxs-lookup"><span data-stu-id="778bd-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="778bd-125">如果您想要在本機進行安裝，請使用 [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) 命令。</span><span class="sxs-lookup"><span data-stu-id="778bd-125">If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="778bd-126">如果執行環境是 Linux 或 macOS，則可能需要使用 sudo 來執行。</span><span class="sxs-lookup"><span data-stu-id="778bd-126">If running in Linux or macOS, you may need to run with sudo.</span></span> <span data-ttu-id="778bd-127">在 Windows 上，請確定您的殼層已經是以系統管理員身分執行。</span><span class="sxs-lookup"><span data-stu-id="778bd-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="778bd-128">在 Windows 上，預設安裝是 *c:\program files (x86)\kubectl.exe*。</span><span class="sxs-lookup"><span data-stu-id="778bd-128">On Windows, the default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="778bd-129">您可能需要將此檔案新增到 Windows 路徑。</span><span class="sxs-lookup"><span data-stu-id="778bd-129">You may need to add this file to the Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="778bd-130">使用 kubectl 連線</span><span class="sxs-lookup"><span data-stu-id="778bd-130">Connect with kubectl</span></span>

<span data-ttu-id="778bd-131">若要將 `kubectl` 設定為連線到 Kubernetes 叢集，請執行 [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) 命令。</span><span class="sxs-lookup"><span data-stu-id="778bd-131">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="778bd-132">若要確認與叢集的連線，請執行 [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) 命令。</span><span class="sxs-lookup"><span data-stu-id="778bd-132">To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="778bd-133">輸出：</span><span class="sxs-lookup"><span data-stu-id="778bd-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="778bd-134">完成教學課程時，您的 ACS Kubernetes 叢集便已可供工作負載使用。</span><span class="sxs-lookup"><span data-stu-id="778bd-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="778bd-135">在後續的教學課程中，會將多容器應用程式部署到這個叢集、向外延展、更新，以及進行監視。</span><span class="sxs-lookup"><span data-stu-id="778bd-135">In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="778bd-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="778bd-136">Next steps</span></span>

<span data-ttu-id="778bd-137">在本教學課程中，已部署一個 Azure Container Service Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="778bd-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="778bd-138">已完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="778bd-138">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="778bd-139">已部署 Kubernetes ACS 叢集</span><span class="sxs-lookup"><span data-stu-id="778bd-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="778bd-140">已安裝 Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="778bd-140">Installed the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="778bd-141">已設定 kubectl</span><span class="sxs-lookup"><span data-stu-id="778bd-141">Configured kubectl</span></span>

<span data-ttu-id="778bd-142">請前往下一個教學課程，以了解如何在叢集上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="778bd-142">Advance to the next tutorial to learn about running application on the cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="778bd-143">在 Kubernetes 中部署應用程式</span><span class="sxs-lookup"><span data-stu-id="778bd-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)