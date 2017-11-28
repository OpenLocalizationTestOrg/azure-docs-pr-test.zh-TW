---
title: "aaaAzure 容器服務教學課程-部署叢集 |Microsoft 文件"
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
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="277db-104">在 Azure Container Service 中部署 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="277db-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="277db-105">Kubernetes 會提供容器化應用程式的分散式平台。</span><span class="sxs-lookup"><span data-stu-id="277db-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="277db-106">透過 Azure Container Service，可簡單又快速地佈建生產環境就緒 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="277db-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="277db-107">在本教學課程的第 3 和第 7 部分中，已部署一個 Azure Container Service Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="277db-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="277db-108">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="277db-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="277db-109">部署 Kubernetes ACS 叢集</span><span class="sxs-lookup"><span data-stu-id="277db-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="277db-110">Hello Kubernetes CLI (kubectl) 的安裝</span><span class="sxs-lookup"><span data-stu-id="277db-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="277db-111">設定 kubectl</span><span class="sxs-lookup"><span data-stu-id="277db-111">Configuration of kubectl</span></span>

<span data-ttu-id="277db-112">在後續教學課程中，hello Azure 投票應用程式是部署 toohello 叢集中，縮放，更新，且 Operations Management Suite 設定的 toomonitor hello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="277db-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="277db-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="277db-113">Before you begin</span></span>

<span data-ttu-id="277db-114">在上一個教學課程中，容器映像建立和上傳 tooan Azure 容器登錄中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="277db-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="277db-115">如果您有未完成這些步驟，並希望沿著 toofollow，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="277db-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="277db-116">建立 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="277db-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="277db-117">在 hello[上一個教學課程](./container-service-tutorial-kubernetes-prepare-acr.md)，資源群組名稱*myResourceGroup*所建立。</span><span class="sxs-lookup"><span data-stu-id="277db-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="277db-118">如果您尚未這樣做，請立即建立此資源群組。</span><span class="sxs-lookup"><span data-stu-id="277db-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="277db-119">在 Azure 容器服務中建立 Kubernetes 叢集以 hello [az acs 建立](/cli/azure/acs#create)命令。</span><span class="sxs-lookup"><span data-stu-id="277db-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="277db-120">hello 下列範例會建立名為叢集*myK8sCluster*一個 Linux 的主要節點和三個 Linux 代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="277db-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="277db-121">幾分鐘之後，hello 命令完成，並傳回 json 格式化的 hello ACS 部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="277db-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="277db-122">安裝 hello kubectl CLI</span><span class="sxs-lookup"><span data-stu-id="277db-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="277db-123">從用戶端電腦，使用叢集的 tooconnect toohello Kubernetes [kubectl](https://kubernetes.io/docs/user-guide/kubectl/)，hello Kubernetes 命令列用戶端。</span><span class="sxs-lookup"><span data-stu-id="277db-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="277db-124">如果您是使用 Azure CloudShell，就已安裝 `kubectl`。</span><span class="sxs-lookup"><span data-stu-id="277db-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="277db-125">如果您想 tooinstall 它在本機，使用 hello [az acs kubernetes 安裝 cli](/cli/azure/acs/kubernetes#install-cli)命令。</span><span class="sxs-lookup"><span data-stu-id="277db-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="277db-126">如果執行 Linux 或 macOS 中，您可能需要具有 sudo toorun。</span><span class="sxs-lookup"><span data-stu-id="277db-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="277db-127">在 Windows 上，請確定您的殼層已經是以系統管理員身分執行。</span><span class="sxs-lookup"><span data-stu-id="277db-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="277db-128">在 Windows 中，是預設安裝中 hello *c:\program files (x86)\kubectl.exe*。</span><span class="sxs-lookup"><span data-stu-id="277db-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="277db-129">您可能需要 tooadd 此檔案 toohello Windows 路徑。</span><span class="sxs-lookup"><span data-stu-id="277db-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="277db-130">使用 kubectl 連線</span><span class="sxs-lookup"><span data-stu-id="277db-130">Connect with kubectl</span></span>

<span data-ttu-id="277db-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes 叢集，請執行 hello [az acs kubernetes 取得認證](/cli/azure/acs/kubernetes#get-credentials)命令。</span><span class="sxs-lookup"><span data-stu-id="277db-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="277db-132">tooverify hello 連接 tooyour 叢集，請執行 hello [kubectl 取得節點](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get)命令。</span><span class="sxs-lookup"><span data-stu-id="277db-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="277db-133">輸出：</span><span class="sxs-lookup"><span data-stu-id="277db-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="277db-134">完成教學課程時，您的 ACS Kubernetes 叢集便已可供工作負載使用。</span><span class="sxs-lookup"><span data-stu-id="277db-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="277db-135">在後續教學課程中，多重容器應用程式是部署的 toothis 叢集時，向外延展、 更新和監視。</span><span class="sxs-lookup"><span data-stu-id="277db-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="277db-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="277db-136">Next steps</span></span>

<span data-ttu-id="277db-137">在本教學課程中，已部署一個 Azure Container Service Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="277db-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="277db-138">已完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="277db-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="277db-139">已部署 Kubernetes ACS 叢集</span><span class="sxs-lookup"><span data-stu-id="277db-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="277db-140">已安裝的 hello Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="277db-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="277db-141">已設定 kubectl</span><span class="sxs-lookup"><span data-stu-id="277db-141">Configured kubectl</span></span>

<span data-ttu-id="277db-142">前進 toohello 下一個教學課程的 toolearn 有關 hello 叢集上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="277db-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="277db-143">在 Kubernetes 中部署應用程式</span><span class="sxs-lookup"><span data-stu-id="277db-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
