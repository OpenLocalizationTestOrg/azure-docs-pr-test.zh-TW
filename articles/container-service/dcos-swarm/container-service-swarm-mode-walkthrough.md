---
title: "aaaQuickstart-適用於 Linux 的 Azure Docker CE 叢集 |Microsoft 文件"
description: "快速了解 toocreate Docker CE 叢集以 hello Azure CLI Azure 容器服務中的 Linux 容器。"
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="92055-103">部署 Docker CE 叢集</span><span class="sxs-lookup"><span data-stu-id="92055-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="92055-104">在這個快速入門，Docker CE 叢集已部署使用 Azure CLI hello。</span><span class="sxs-lookup"><span data-stu-id="92055-104">In this quick start, a Docker CE cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="92055-105">然後部署並 hello 叢集上執行多個容器應用程式，其中包含 web 前端和 Redis 執行個體。</span><span class="sxs-lookup"><span data-stu-id="92055-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="92055-106">Hello 應用程式完成後，會透過可存取網際網路的 hello。</span><span class="sxs-lookup"><span data-stu-id="92055-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="92055-107">Azure Container Service 上的 Docker CE 處於預覽狀態，**不得用於生產工作負載**。</span><span class="sxs-lookup"><span data-stu-id="92055-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="92055-108">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="92055-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="92055-109">如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="92055-109">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="92055-110">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="92055-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="92055-111">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="92055-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="92055-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="92055-112">Create a resource group</span></span>

<span data-ttu-id="92055-113">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="92055-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="92055-114">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="92055-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="92055-115">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *ukwest*位置。</span><span class="sxs-lookup"><span data-stu-id="92055-115">hello following example creates a resource group named *myResourceGroup* in hello *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="92055-116">輸出：</span><span class="sxs-lookup"><span data-stu-id="92055-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="92055-117">建立 Docker Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="92055-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="92055-118">在 Azure 容器服務中建立 Docker CE 叢集以 hello [az acs 建立](/cli/azure/acs#create)命令。</span><span class="sxs-lookup"><span data-stu-id="92055-118">Create a Docker CE cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="92055-119">hello 下列範例會建立名為叢集*mySwarmCluster*一個 Linux 的主要節點和三個 Linux 代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="92055-119">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="92055-120">幾分鐘之後，hello 命令完成，並傳回 hello 叢集的 json 格式資訊。</span><span class="sxs-lookup"><span data-stu-id="92055-120">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="92055-121">Toohello 叢集連線</span><span class="sxs-lookup"><span data-stu-id="92055-121">Connect toohello cluster</span></span>

<span data-ttu-id="92055-122">這個整個快速入門，您需要 hello hello Docker Swarm master 和 hello Docker 代理程式集區的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="92055-122">Throughout this quick start, you need hello FQDN of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="92055-123">執行下列命令 tooreturn 兩者 hello master 和代理程式的 Fqdn 的 hello。</span><span class="sxs-lookup"><span data-stu-id="92055-123">Run hello following command tooreturn both hello master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="92055-124">輸出：</span><span class="sxs-lookup"><span data-stu-id="92055-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="92055-125">建立 SSH 通道 toohello 群集 master。</span><span class="sxs-lookup"><span data-stu-id="92055-125">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="92055-126">取代`MasterFQDN`hello FQDN hello 群集主要地址。</span><span class="sxs-lookup"><span data-stu-id="92055-126">Replace `MasterFQDN` with hello FQDN address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="92055-127">設定 hello`DOCKER_HOST`環境變數。</span><span class="sxs-lookup"><span data-stu-id="92055-127">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="92055-128">這可讓您針對 hello Docker Swarm toorun docker 命令而不需要 toospecify hello hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="92055-128">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="92055-129">現在您已經準備就緒 toorun hello Docker Swarm 上的 Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="92055-129">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="92055-130">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="92055-130">Run hello application</span></span>

<span data-ttu-id="92055-131">建立名為`azure-vote.yaml`並複製 hello 遵循到其中的內容。</span><span class="sxs-lookup"><span data-stu-id="92055-131">Create a file named `azure-vote.yaml` and copy hello following content into it.</span></span>


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="92055-132">執行 hello [docker 堆疊部署](https://docs.docker.com/engine/reference/commandline/stack_deploy/)命令 toocreate hello Azure 投票服務。</span><span class="sxs-lookup"><span data-stu-id="92055-132">Run hello [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command toocreate hello Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="92055-133">輸出：</span><span class="sxs-lookup"><span data-stu-id="92055-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="92055-134">使用 hello [docker 堆疊 ps](https://docs.docker.com/engine/reference/commandline/stack_ps/)命令 tooreturn hello 部署狀態的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="92055-134">Use hello [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command tooreturn hello deployment status of hello application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="92055-135">一次 hello`CURRENT STATE`每個服務是`Running`，準備 hello 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="92055-135">Once hello `CURRENT STATE` of each service is `Running`, hello application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a><span data-ttu-id="92055-136">測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="92055-136">Test hello application</span></span>

<span data-ttu-id="92055-137">瀏覽 toohello hello 群集代理程式集區 tootest 出 hello Azure 投票應用程式的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="92055-137">Browse toohello FQDN of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![瀏覽 tooAzure 投票的映像](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="92055-139">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="92055-139">Delete cluster</span></span>
<span data-ttu-id="92055-140">當不再需要 hello 叢集時，您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 容器服務，以及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="92055-140">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="92055-141">取得 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="92055-141">Get hello code</span></span>

<span data-ttu-id="92055-142">在這個快速入門中，預先建立的容器映像已使用的 toocreate Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="92055-142">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="92055-143">hello 相關應用程式程式碼，Dockerfile 中，且可在 GitHub 上編輯檔案。</span><span class="sxs-lookup"><span data-stu-id="92055-143">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="92055-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="92055-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="92055-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92055-145">Next steps</span></span>

<span data-ttu-id="92055-146">在這個快速入門中，您可以部署 Docker Swarm 叢集並部署多個容器應用程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="92055-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="92055-147">有關使用 Visual Studio Team Services，整合 Docker 暖 toolearn 繼續 toohello CI/CD 與 Docker Swarm VSTS。</span><span class="sxs-lookup"><span data-stu-id="92055-147">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="92055-148">搭配 Docker Swarm 和 VSTS 的 CI/CD</span><span class="sxs-lookup"><span data-stu-id="92055-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)