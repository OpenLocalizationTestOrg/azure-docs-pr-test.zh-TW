---
title: "aaaQuickstart-適用於 Windows Azure Kubernetes 叢集 |Microsoft 文件"
description: "快速了解 toocreate Kubernetes 叢集以 hello Azure CLI Azure 容器服務中的 Windows 容器。"
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="fe20d-103">部署適用於 Windows 容器的 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="fe20d-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="fe20d-104">hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="fe20d-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="fe20d-105">本指南詳細說明使用 hello Azure CLI toodeploy [Kubernetes](https://kubernetes.io/docs/home/)叢集[Azure 容器服務](../container-service-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="fe20d-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="fe20d-106">Hello 叢集部署之後，您與 hello Kubernetes 連接 tooit`kubectl`命令列工具，而且您部署您的第一個 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="fe20d-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="fe20d-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="fe20d-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fe20d-108">如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fe20d-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fe20d-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="fe20d-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fe20d-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="fe20d-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="fe20d-111">支援 Windows 容器在 Azure Container Service 上的 Kubernetes 處於預覽階段。</span><span class="sxs-lookup"><span data-stu-id="fe20d-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="fe20d-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="fe20d-112">Create a resource group</span></span>

<span data-ttu-id="fe20d-113">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="fe20d-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="fe20d-114">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="fe20d-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="fe20d-115">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。</span><span class="sxs-lookup"><span data-stu-id="fe20d-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="fe20d-116">建立 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="fe20d-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="fe20d-117">在 Azure 容器服務中建立 Kubernetes 叢集以 hello [az acs 建立](/cli/azure/acs#create)命令。</span><span class="sxs-lookup"><span data-stu-id="fe20d-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="fe20d-118">hello 下列範例會建立名為叢集*myK8sCluster*一個 Linux 的主要節點和兩個 Windows 代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="fe20d-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="fe20d-119">這個範例會建立 SSH 金鑰需要的 tooconnect toohello Linux 主要。</span><span class="sxs-lookup"><span data-stu-id="fe20d-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="fe20d-120">這個範例會使用*azureuser*系統管理使用者名稱和*myPassword12* hello hello Windows 節點上的密碼。</span><span class="sxs-lookup"><span data-stu-id="fe20d-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="fe20d-121">更新這些值 toosomething 適當 tooyour 環境。</span><span class="sxs-lookup"><span data-stu-id="fe20d-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="fe20d-122">幾分鐘之後，hello 命令會完成，並顯示您部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fe20d-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="fe20d-123">安裝 kubectl</span><span class="sxs-lookup"><span data-stu-id="fe20d-123">Install kubectl</span></span>

<span data-ttu-id="fe20d-124">從用戶端電腦，使用叢集的 tooconnect toohello Kubernetes [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/)，hello Kubernetes 命令列用戶端。</span><span class="sxs-lookup"><span data-stu-id="fe20d-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="fe20d-125">如果您是使用 Azure CloudShell，就已安裝 `kubectl`。</span><span class="sxs-lookup"><span data-stu-id="fe20d-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="fe20d-126">如果您想 tooinstall 它在本機，您可以使用 hello [az acs kubernetes 安裝 cli](/cli/azure/acs/kubernetes#install-cli)命令。</span><span class="sxs-lookup"><span data-stu-id="fe20d-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="fe20d-127">hello 下列 Azure CLI 範例安裝`kubectl`tooyour 系統。</span><span class="sxs-lookup"><span data-stu-id="fe20d-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="fe20d-128">在 Windows 上，以系統管理員身分執行此命令。</span><span class="sxs-lookup"><span data-stu-id="fe20d-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="fe20d-129">使用 kubectl 連線</span><span class="sxs-lookup"><span data-stu-id="fe20d-129">Connect with kubectl</span></span>

<span data-ttu-id="fe20d-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes 叢集，請執行 hello [az acs kubernetes 取得認證](/cli/azure/acs/kubernetes#get-credentials)命令。</span><span class="sxs-lookup"><span data-stu-id="fe20d-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="fe20d-131">hello 下列範例會下載 hello Kubernetes 叢集的叢集設定。</span><span class="sxs-lookup"><span data-stu-id="fe20d-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="fe20d-132">tooverify hello 連接 tooyour 叢集從您的電腦，再試一次執行：</span><span class="sxs-lookup"><span data-stu-id="fe20d-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="fe20d-133">`kubectl`列出 hello master 和代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="fe20d-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="fe20d-134">部署 Windows IIS 容器</span><span class="sxs-lookup"><span data-stu-id="fe20d-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="fe20d-135">您可以在 Kubernetes Pod 內執行 Docker 容器，其中包含一個或多個容器。</span><span class="sxs-lookup"><span data-stu-id="fe20d-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="fe20d-136">這個基本範例會使用 JSON 檔案 toospecify Microsoft Internet Information Server (IIS) 容器，並接著會建立使用 hello hello pod`kubctl apply`命令。</span><span class="sxs-lookup"><span data-stu-id="fe20d-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="fe20d-137">建立名為本機檔案`iis.json`和複製 hello 文字之後。</span><span class="sxs-lookup"><span data-stu-id="fe20d-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="fe20d-138">這個檔案會告知 Kubernetes toorun IIS Windows Server 2016 Nano Server 上，使用從公用容器映像[Docker Hub](https://hub.docker.com/r/nanoserver/iis/)。</span><span class="sxs-lookup"><span data-stu-id="fe20d-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="fe20d-139">hello 容器會使用連接埠 80，但一開始只有 hello 叢集網路中存取。</span><span class="sxs-lookup"><span data-stu-id="fe20d-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="fe20d-140">toostart hello pod，類型：</span><span class="sxs-lookup"><span data-stu-id="fe20d-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="fe20d-141">型別 tootrack hello 部署：</span><span class="sxs-lookup"><span data-stu-id="fe20d-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="fe20d-142">正在部署的 hello pod，hello 狀態即`ContainerCreating`。</span><span class="sxs-lookup"><span data-stu-id="fe20d-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="fe20d-143">可能需要幾分鐘，讓 hello 容器 tooenter hello`Running`狀態。</span><span class="sxs-lookup"><span data-stu-id="fe20d-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="fe20d-144">檢視 hello IIS [歡迎使用] 頁面</span><span class="sxs-lookup"><span data-stu-id="fe20d-144">View hello IIS welcome page</span></span>

<span data-ttu-id="fe20d-145">tooexpose hello pod toohello 世界公用 IP 位址，下列命令的型別 hello:</span><span class="sxs-lookup"><span data-stu-id="fe20d-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="fe20d-146">Kubernetes 會利用這個命令，建立服務和[Azure 負載平衡器規則](container-service-kubernetes-load-balancing.md)與 hello 服務的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fe20d-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="fe20d-147">執行下列命令 toosee hello 狀態 hello 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="fe20d-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="fe20d-148">一開始 hello IP 位址會顯示為`pending`。</span><span class="sxs-lookup"><span data-stu-id="fe20d-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="fe20d-149">請稍候幾分鐘 hello 外部 IP 位址的 hello `iis` pod 設定：</span><span class="sxs-lookup"><span data-stu-id="fe20d-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="fe20d-150">您可以使用網頁瀏覽器選擇 toosee hello 預設 IIS 歡迎使用頁面的外部 IP 位址為 hello:</span><span class="sxs-lookup"><span data-stu-id="fe20d-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![瀏覽 tooIIS 的映像](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="fe20d-152">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="fe20d-152">Delete cluster</span></span>
<span data-ttu-id="fe20d-153">當不再需要 hello 叢集時，您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 容器服務，以及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="fe20d-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="fe20d-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe20d-154">Next steps</span></span>

<span data-ttu-id="fe20d-155">在本快速入門中，您部署了 Kubernetes 叢集、與 `kubectl` 連線，並使用 IIS 容器部署了 Pod。</span><span class="sxs-lookup"><span data-stu-id="fe20d-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="fe20d-156">進一步了解 Azure 容器服務，toolearn 繼續 toohello Kubernetes 教學課程。</span><span class="sxs-lookup"><span data-stu-id="fe20d-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe20d-157">管理 ACS Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="fe20d-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
