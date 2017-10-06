---
title: "aaaAzure 容器服務教學課程-小數位數的應用程式 |Microsoft 文件"
description: "Azure Container Service 教學課程 - 調整應用程式"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="30851-104">調整 Kubernetes Pod 和 Kubernetes 基礎結構</span><span class="sxs-lookup"><span data-stu-id="30851-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="30851-105">如果您已依照已 hello 教學課程，Azure 容器服務中有可運作的 Kubernetes 叢集，而且您已部署的 hello Azure 投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="30851-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="30851-106">在本教學課程一部分五 7，您可以擴充 hello 應用程式中的 hello pod，然後再次嘗試 pod 自動調整。</span><span class="sxs-lookup"><span data-stu-id="30851-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="30851-107">您也了解 Azure VM 代理程式節點 toochange tooscale hello 數目 hello 叢集的容量，以裝載工作負載的方式。</span><span class="sxs-lookup"><span data-stu-id="30851-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="30851-108">完成的工作包括：</span><span class="sxs-lookup"><span data-stu-id="30851-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30851-109">手動調整 Kubernetes Pod</span><span class="sxs-lookup"><span data-stu-id="30851-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="30851-110">設定自動調整規模 pod 執行 hello 應用程式前端</span><span class="sxs-lookup"><span data-stu-id="30851-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="30851-111">調整 hello Kubernetes Azure 代理程式節點</span><span class="sxs-lookup"><span data-stu-id="30851-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="30851-112">在後續教學課程中，hello Azure 投票應用程式會更新，而且 Operations Management Suite 設定 toomonitor hello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="30851-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="30851-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="30851-113">Before you begin</span></span>

<span data-ttu-id="30851-114">在上一個教學課程中，應用程式封裝成容器映像，此映像上載 tooAzure 容器登錄中，並建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="30851-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="30851-115">hello 應用程式然後 hello Kubernetes 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="30851-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="30851-116">如果您有未完成這些步驟，並希望沿著 toofollow，傳回 toohello[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="30851-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="30851-117">本教學課程至少需要一個含有執行中應用程式的 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="30851-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="30851-118">手動調整 Pod</span><span class="sxs-lookup"><span data-stu-id="30851-118">Manually scale pods</span></span>

<span data-ttu-id="30851-119">到目前為止，hello Azure 投票前端和 Redis 執行個體已部署，每個都有單一複本。</span><span class="sxs-lookup"><span data-stu-id="30851-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="30851-120">tooverify，執行 hello [kubectl 取得](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get)命令。</span><span class="sxs-lookup"><span data-stu-id="30851-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="30851-121">輸出：</span><span class="sxs-lookup"><span data-stu-id="30851-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="30851-122">手動變更 hello 數目在 hello pod`azure-vote-front`部署使用 hello [kubectl 標尺](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale)命令。</span><span class="sxs-lookup"><span data-stu-id="30851-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="30851-123">這個範例會增加 hello 數字 too5。</span><span class="sxs-lookup"><span data-stu-id="30851-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="30851-124">執行[kubectl 取得 pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify Kubernetes 建立 hello pod。</span><span class="sxs-lookup"><span data-stu-id="30851-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="30851-125">約一分鐘之後, 執行的其他 pod 的 hello:</span><span class="sxs-lookup"><span data-stu-id="30851-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="30851-126">輸出：</span><span class="sxs-lookup"><span data-stu-id="30851-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="30851-127">自動調整 Pod</span><span class="sxs-lookup"><span data-stu-id="30851-127">Autoscale pods</span></span>

<span data-ttu-id="30851-128">Kubernetes 支援[水平的 pod 自動調整](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)tooadjust hello 數目 pod 根據 CPU 使用率或其他部署中選取的度量。</span><span class="sxs-lookup"><span data-stu-id="30851-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="30851-129">toouse hello autoscaler，CPU 要求與定義的限制，必須具有您 pod。</span><span class="sxs-lookup"><span data-stu-id="30851-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="30851-130">在 hello`azure-vote-front`部署 hello 前端容器要求 0.25 CPU，且長度限制為 0.5 的 CPU。</span><span class="sxs-lookup"><span data-stu-id="30851-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="30851-131">hello 設定如下：</span><span class="sxs-lookup"><span data-stu-id="30851-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="30851-132">hello 下列範例會使用 hello [kubectl 自動調整規模](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale)命令 tooautoscale hello 數目在 hello pod`azure-vote-front`部署。</span><span class="sxs-lookup"><span data-stu-id="30851-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="30851-133">在這裡，如果 CPU 使用率超過 50%，hello autoscaler 會增加 hello pod tooa 最多 10 個。</span><span class="sxs-lookup"><span data-stu-id="30851-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="30851-134">hello autoscaler，執行下列命令的 hello toosee hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="30851-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="30851-135">輸出：</span><span class="sxs-lookup"><span data-stu-id="30851-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="30851-136">請稍候幾分鐘，且最負載 hello Azure 投票應用程式，hello pod 複本的數目會自動減少 too3。</span><span class="sxs-lookup"><span data-stu-id="30851-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="30851-137">標尺 hello 代理程式</span><span class="sxs-lookup"><span data-stu-id="30851-137">Scale hello agents</span></span>

<span data-ttu-id="30851-138">如果您建立使用 hello 上一個教學課程中的預設指令 Kubernetes 叢集時，它會有三個代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="30851-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="30851-139">如果您計劃您的叢集更多或較少的容器工作負載，您可以手動調整 hello 代理程式數目。</span><span class="sxs-lookup"><span data-stu-id="30851-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="30851-140">使用 hello [az acs 調整](/cli/azure/acs#scale)命令，然後指定代理程式的 hello 數目以 hello`--new-agent-count`參數。</span><span class="sxs-lookup"><span data-stu-id="30851-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="30851-141">hello 下列範例會增加 hello 數目名為 hello Kubernetes 叢集中的代理程式節點 too4 *myK8sCluster*。</span><span class="sxs-lookup"><span data-stu-id="30851-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="30851-142">hello 命令會使用幾個分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="30851-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="30851-143">hello 命令輸出會顯示代理程式的 hello 號碼節點中的 hello 值`agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="30851-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="30851-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30851-144">Next steps</span></span>

<span data-ttu-id="30851-145">在本教學課程中，您已在 Kubernetes 叢集中使用不同的調整功能。</span><span class="sxs-lookup"><span data-stu-id="30851-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="30851-146">涵蓋的工作包括：</span><span class="sxs-lookup"><span data-stu-id="30851-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30851-147">手動調整 Kubernetes Pod</span><span class="sxs-lookup"><span data-stu-id="30851-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="30851-148">設定自動調整規模 pod 執行 hello 應用程式前端</span><span class="sxs-lookup"><span data-stu-id="30851-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="30851-149">調整 hello Kubernetes Azure 代理程式節點</span><span class="sxs-lookup"><span data-stu-id="30851-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="30851-150">前進 toohello 下一個教學課程的 toolearn 有關更新中 Kubernetes 應用程式。</span><span class="sxs-lookup"><span data-stu-id="30851-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="30851-151">更新 Kubernetes 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="30851-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

