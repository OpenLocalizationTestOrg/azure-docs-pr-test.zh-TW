---
title: "aaaQuickstart-適用於 Linux 的 Azure Docker Swarm 叢集 |Microsoft 文件"
description: "快速了解 toocreate 以 hello Azure CLI Azure 容器服務中的 Linux 容器的 Docker Swarm 叢集中。"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="c5368-103">部署 Docker Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="c5368-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="c5368-104">在這個快速入門，Docker Swarm 叢集中使用 hello Azure CLI 部署。</span><span class="sxs-lookup"><span data-stu-id="c5368-104">In this quick start, a Docker Swarm cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="c5368-105">然後部署並 hello 叢集上執行多個容器應用程式，其中包含 web 前端和 Redis 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c5368-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="c5368-106">Hello 應用程式完成後，會透過可存取網際網路的 hello。</span><span class="sxs-lookup"><span data-stu-id="c5368-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="c5368-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="c5368-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="c5368-108">本快速入門需要執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c5368-108">This quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c5368-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="c5368-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c5368-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="c5368-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="c5368-111">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="c5368-111">Create a resource group</span></span>

<span data-ttu-id="c5368-112">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="c5368-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c5368-113">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="c5368-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="c5368-114">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *uswest*位置。</span><span class="sxs-lookup"><span data-stu-id="c5368-114">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="c5368-115">輸出：</span><span class="sxs-lookup"><span data-stu-id="c5368-115">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="c5368-116">建立 Docker Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="c5368-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="c5368-117">在 Azure 容器服務中建立 Docker Swarm 叢集以 hello [az acs 建立](/cli/azure/acs#create)命令。</span><span class="sxs-lookup"><span data-stu-id="c5368-117">Create a Docker Swarm cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="c5368-118">hello 下列範例會建立名為叢集*mySwarmCluster*一個 Linux 的主要節點和三個 Linux 代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="c5368-118">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="c5368-119">幾分鐘之後，hello 命令完成，並傳回 hello 叢集的 json 格式資訊。</span><span class="sxs-lookup"><span data-stu-id="c5368-119">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="c5368-120">Toohello 叢集連線</span><span class="sxs-lookup"><span data-stu-id="c5368-120">Connect toohello cluster</span></span>

<span data-ttu-id="c5368-121">在這個快速入門中，您需要 hello hello Docker Swarm master 和 hello Docker 代理程式集區的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c5368-121">Throughout this quick start, you need hello IP address of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="c5368-122">執行下列命令 tooreturn hello 兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c5368-122">Run hello following command tooreturn both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="c5368-123">輸出：</span><span class="sxs-lookup"><span data-stu-id="c5368-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="c5368-124">建立 SSH 通道 toohello 群集 master。</span><span class="sxs-lookup"><span data-stu-id="c5368-124">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="c5368-125">取代`IPAddress`hello hello 群集的主要 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c5368-125">Replace `IPAddress` with hello IP address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="c5368-126">設定 hello`DOCKER_HOST`環境變數。</span><span class="sxs-lookup"><span data-stu-id="c5368-126">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="c5368-127">這可讓您針對 hello Docker Swarm toorun docker 命令而不需要 toospecify hello hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="c5368-127">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="c5368-128">現在您已經準備就緒 toorun hello Docker Swarm 上的 Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="c5368-128">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="c5368-129">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c5368-129">Run hello application</span></span>

<span data-ttu-id="c5368-130">建立名為`docker-compose.yaml`並複製 hello 遵循到其中的內容。</span><span class="sxs-lookup"><span data-stu-id="c5368-130">Create a file named `docker-compose.yaml` and copy hello following content into it.</span></span>

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="c5368-131">執行下列命令 toocreate hello Azure 投票服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="c5368-131">Run hello following command toocreate hello Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="c5368-132">輸出：</span><span class="sxs-lookup"><span data-stu-id="c5368-132">Output:</span></span>

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a><span data-ttu-id="c5368-133">測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c5368-133">Test hello application</span></span>

<span data-ttu-id="c5368-134">瀏覽 toohello 的 hello 群集代理程式集區 tootest 出 hello Azure 投票應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c5368-134">Browse toohello IP address of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![瀏覽 tooAzure 投票的映像](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="c5368-136">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="c5368-136">Delete cluster</span></span>
<span data-ttu-id="c5368-137">當不再需要 hello 叢集時，您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 容器服務，以及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="c5368-137">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="c5368-138">取得 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="c5368-138">Get hello code</span></span>

<span data-ttu-id="c5368-139">在這個快速入門中，預先建立的容器映像已使用的 toocreate Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="c5368-139">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="c5368-140">hello 相關應用程式程式碼，Dockerfile 中，且可在 GitHub 上編輯檔案。</span><span class="sxs-lookup"><span data-stu-id="c5368-140">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="c5368-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="c5368-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="c5368-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5368-142">Next steps</span></span>

<span data-ttu-id="c5368-143">在這個快速入門中，您可以部署 Docker Swarm 叢集並部署多個容器應用程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="c5368-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="c5368-144">有關使用 Visual Studio Team Services，整合 Docker 暖 toolearn 繼續 toohello CI/CD 與 Docker Swarm VSTS。</span><span class="sxs-lookup"><span data-stu-id="c5368-144">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c5368-145">搭配 Docker Swarm 和 VSTS 的 CI/CD</span><span class="sxs-lookup"><span data-stu-id="c5368-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)