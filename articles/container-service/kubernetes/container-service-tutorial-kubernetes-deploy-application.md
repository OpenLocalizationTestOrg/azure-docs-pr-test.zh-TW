---
title: "aaaAzure 容器服務教學課程-部署的應用程式 |Microsoft 文件"
description: "Azure Container Service 教學課程 - 部署應用程式"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="c287c-104">在 Kubernetes 中執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c287c-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="c287c-105">在本教學課程 (七個章節的第四部分) 中，已在 Kubernetes 叢集中部署一個應用程式範例。</span><span class="sxs-lookup"><span data-stu-id="c287c-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="c287c-106">完成的步驟包括：</span><span class="sxs-lookup"><span data-stu-id="c287c-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c287c-107">下載 Kubernetes 資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="c287c-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="c287c-108">在 Kubernetes 中執行應用程式</span><span class="sxs-lookup"><span data-stu-id="c287c-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="c287c-109">測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c287c-109">Test hello application</span></span>

<span data-ttu-id="c287c-110">在後續教學課程中，此應用程式會向外延展，更新，而且 Operations Management Suite 設定 toomonitor hello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="c287c-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="c287c-111">本教學課程假設 Kubernetes 概念的基本了解、 Kubernetes 的詳細資訊請參閱 hello [Kubernetes 文件](https://kubernetes.io/docs/home/)。</span><span class="sxs-lookup"><span data-stu-id="c287c-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c287c-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="c287c-112">Before you begin</span></span>

<span data-ttu-id="c287c-113">在上一個教學課程中，應用程式封裝成容器映像、 此映像上傳的 tooAzure 容器登錄中，並已建立 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="c287c-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="c287c-114">如果您有未完成這些步驟，並希望沿著 toofollow，傳回太[教學課程 1 – 建立容器映像](./container-service-tutorial-kubernetes-prepare-app.md)。</span><span class="sxs-lookup"><span data-stu-id="c287c-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="c287c-115">本教學課程至少需要一個 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="c287c-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="c287c-116">取得資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="c287c-116">Get manifest file</span></span>

<span data-ttu-id="c287c-117">針對此教學課程，會使用 Kubernetes 資訊清單來部署 [Kubernetes 物件](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)。</span><span class="sxs-lookup"><span data-stu-id="c287c-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="c287c-118">Kubernetes 資訊清單為 YAML 或 JSON 格式的檔案，包含 Kubernetes 物件部署和設定指示。</span><span class="sxs-lookup"><span data-stu-id="c287c-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="c287c-119">使用 hello Azure 投票應用程式儲存機制中，這已在上一個教學課程中複製此教學課程中的 hello 應用程式資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="c287c-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="c287c-120">如果您尚未這樣做，請使用下列命令的 hello 複製 hello 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="c287c-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="c287c-121">hello 遵循 hello 複製儲存機制的目錄中找到 hello 資訊清單檔案。</span><span class="sxs-lookup"><span data-stu-id="c287c-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="c287c-122">更新資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="c287c-122">Update manifest file</span></span>

<span data-ttu-id="c287c-123">如果使用 Azure 容器登錄中 toostore hello 容器映像，hello 資訊清單需求 toobe 更新 hello loginServer 的 ACR 名稱。</span><span class="sxs-lookup"><span data-stu-id="c287c-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="c287c-124">取得 hello ACR 登入伺服器名稱以 hello [az acr 清單](/cli/azure/acr#list)命令。</span><span class="sxs-lookup"><span data-stu-id="c287c-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="c287c-125">hello 範例資訊清單已預先建立的儲存機制名稱*microsoft*。</span><span class="sxs-lookup"><span data-stu-id="c287c-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="c287c-126">使用任何文字編輯器 中，開啟 hello 檔案和取代 hello *microsoft* hello 登入伺服器名稱為您的 ACR 的執行個體的值。</span><span class="sxs-lookup"><span data-stu-id="c287c-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="c287c-127">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="c287c-127">Deploy application</span></span>

<span data-ttu-id="c287c-128">使用 hello [kubectl 建立](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create)命令 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c287c-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="c287c-129">此命令剖析 hello 資訊清單檔案，並建立 hello 定義 Kubernetes 物件。</span><span class="sxs-lookup"><span data-stu-id="c287c-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="c287c-130">輸出：</span><span class="sxs-lookup"><span data-stu-id="c287c-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="c287c-131">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="c287c-131">Test application</span></span>

<span data-ttu-id="c287c-132">A [Kubernetes 服務](https://kubernetes.io/docs/concepts/services-networking/service/)建立 hello 應用程式 toohello 公開網際網路。</span><span class="sxs-lookup"><span data-stu-id="c287c-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="c287c-133">此程序需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c287c-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="c287c-134">toomonitor 進度，使用 hello [kubectl 取得服務](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681)命令與 hello`--watch`引數。</span><span class="sxs-lookup"><span data-stu-id="c287c-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="c287c-135">一開始，hello**外部 IP** hello *azure 投票前*服務會顯示為*暫止*。</span><span class="sxs-lookup"><span data-stu-id="c287c-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="c287c-136">一旦 hello 外部 IP 位址已從*暫止*tooan *IP 位址*，使用`CTRL-C`toostop hello kubectl 監看式程序。</span><span class="sxs-lookup"><span data-stu-id="c287c-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="c287c-137">toosee hello 應用程式中，瀏覽 toohello 外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c287c-137">toosee hello application, browse toohello external IP address.</span></span>

![Azure 上 Kubernetes 叢集的影像](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="c287c-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c287c-139">Next steps</span></span>

<span data-ttu-id="c287c-140">在本教學課程，hello Azure 投票應用程式已部署的 tooan Azure 容器服務 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="c287c-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="c287c-141">完成的工作包括：</span><span class="sxs-lookup"><span data-stu-id="c287c-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="c287c-142">下載 Kubernetes 資訊清單檔</span><span class="sxs-lookup"><span data-stu-id="c287c-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="c287c-143">執行 Kubernetes hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c287c-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="c287c-144">已測試的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c287c-144">Tested hello application</span></span>

<span data-ttu-id="c287c-145">前進 toohello 下一個教學課程的 toolearn 調整規模的 Kubernetes 應用程式 」 和 「 hello 基礎 Kubernetes 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="c287c-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c287c-146">調整 Kubernetes 應用程式和基礎結構</span><span class="sxs-lookup"><span data-stu-id="c287c-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)