---
title: "快速入門 - 適用於 Linux 的 Azure Docker CE 叢集 | Microsoft Docs"
description: "快速了解如何在 Azure Container Service 中使用 Azure CLI 建立適用於 Linux 容器的 Docker CE 叢集。"
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
ms.openlocfilehash: 7b8336e3865e7032e3ee0d5e4ee712bcb95aa4b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="6de3b-103">部署 Docker CE 叢集</span><span class="sxs-lookup"><span data-stu-id="6de3b-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="6de3b-104">本快速入門中會使用 Azure CLI 來部署 Docker CE 叢集。</span><span class="sxs-lookup"><span data-stu-id="6de3b-104">In this quick start, a Docker CE cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="6de3b-105">接著，在叢集上部署和執行多容器應用程式，其中包含 Web 前端和 Redis 執行個體。</span><span class="sxs-lookup"><span data-stu-id="6de3b-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="6de3b-106">完成後，即可透過網際網路來存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="6de3b-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="6de3b-107">Azure Container Service 上的 Docker CE 處於預覽狀態，**不得用於生產工作負載**。</span><span class="sxs-lookup"><span data-stu-id="6de3b-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="6de3b-108">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="6de3b-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="6de3b-109">如果您選擇在本機安裝和使用 CLI，本快速入門會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6de3b-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6de3b-110">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="6de3b-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="6de3b-111">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6de3b-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="6de3b-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="6de3b-112">Create a resource group</span></span>

<span data-ttu-id="6de3b-113">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="6de3b-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6de3b-114">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="6de3b-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="6de3b-115">下列範例會在 ukwest 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6de3b-115">The following example creates a resource group named *myResourceGroup* in the *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="6de3b-116">輸出：</span><span class="sxs-lookup"><span data-stu-id="6de3b-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="6de3b-117">建立 Docker Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="6de3b-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="6de3b-118">使用 [az acs create](/cli/azure/acs#create) 命令，在 Azure Container Service 中建立 Docker CE 叢集。</span><span class="sxs-lookup"><span data-stu-id="6de3b-118">Create a Docker CE cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="6de3b-119">下列範例會建立一個名為 mySwarmCluster 的叢集，其中包含一個 Linux 主要節點和三個 Linux 代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="6de3b-119">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="6de3b-120">幾分鐘之後，此命令就會完成，並以 json 格式傳回叢集的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6de3b-120">After several minutes, the command completes and returns json formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="6de3b-121">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="6de3b-121">Connect to the cluster</span></span>

<span data-ttu-id="6de3b-122">在本快速入門中，您需要 Docker Swarm 主機和 Docker 代理程式集區的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="6de3b-122">Throughout this quick start, you need the FQDN of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="6de3b-123">執行下列命令以傳回主機和代理程式 FQDN。</span><span class="sxs-lookup"><span data-stu-id="6de3b-123">Run the following command to return both the master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="6de3b-124">輸出：</span><span class="sxs-lookup"><span data-stu-id="6de3b-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="6de3b-125">建立 Swarm 主機的 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="6de3b-125">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="6de3b-126">以 Swarm 主機的 FQDN 位址取代 `MasterFQDN`。</span><span class="sxs-lookup"><span data-stu-id="6de3b-126">Replace `MasterFQDN` with the FQDN address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="6de3b-127">設定 `DOCKER_HOST` 環境變數。</span><span class="sxs-lookup"><span data-stu-id="6de3b-127">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="6de3b-128">這可讓您對 Docker Swarm 執行 Docker 命令，而不需指定主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6de3b-128">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="6de3b-129">您現在已經準備好在 Docker Swarm 上執行 Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="6de3b-129">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="6de3b-130">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6de3b-130">Run the application</span></span>

<span data-ttu-id="6de3b-131">建立名為 `azure-vote.yaml` 的檔案，並將下列內容複製到其中。</span><span class="sxs-lookup"><span data-stu-id="6de3b-131">Create a file named `azure-vote.yaml` and copy the following content into it.</span></span>


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

<span data-ttu-id="6de3b-132">執行 [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) 命令來建立 Azure 投票服務。</span><span class="sxs-lookup"><span data-stu-id="6de3b-132">Run the [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command to create the Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="6de3b-133">輸出：</span><span class="sxs-lookup"><span data-stu-id="6de3b-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="6de3b-134">使用 [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) 命令來傳回應用程式的部署狀態。</span><span class="sxs-lookup"><span data-stu-id="6de3b-134">Use the [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command to return the deployment status of the application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="6de3b-135">一旦每項服務的 `CURRENT STATE` 成為 `Running`，應用程式便已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="6de3b-135">Once the `CURRENT STATE` of each service is `Running`, the application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-the-application"></a><span data-ttu-id="6de3b-136">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="6de3b-136">Test the application</span></span>

<span data-ttu-id="6de3b-137">瀏覽至 Swarm 代理程式集區的 FQDN，以測試 Azure 投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="6de3b-137">Browse to the FQDN of the Swarm agent pool to test out the Azure Vote application.</span></span>

![瀏覽至 Azure 投票的影像](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="6de3b-139">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="6de3b-139">Delete cluster</span></span>
<span data-ttu-id="6de3b-140">若不再需要叢集，您可以使用 [az group delete](/cli/azure/group#delete) 命令來移除資源群組、容器服務和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="6de3b-140">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="6de3b-141">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="6de3b-141">Get the code</span></span>

<span data-ttu-id="6de3b-142">在本快速入門中，預先建立的容器映像已用來建立 Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="6de3b-142">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="6de3b-143">在 GitHub 上可取得相關的應用程式程式碼、Dockerfile 和 Compose 檔案。</span><span class="sxs-lookup"><span data-stu-id="6de3b-143">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="6de3b-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="6de3b-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="6de3b-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6de3b-145">Next steps</span></span>

<span data-ttu-id="6de3b-146">在本快速入門中，您已部署 Docker Swarm 叢集，並將多容器應用程式部署到此叢集。</span><span class="sxs-lookup"><span data-stu-id="6de3b-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="6de3b-147">若要了解如何整合 Docker Swarm 與 Visual Studio Team Services，請繼續進行搭配 Docker Swarm 和 VSTS 的 CI/CD。</span><span class="sxs-lookup"><span data-stu-id="6de3b-147">To learn about integrating Docker warm with Visual Studio Team Services, continue to the CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6de3b-148">搭配 Docker Swarm 和 VSTS 的 CI/CD</span><span class="sxs-lookup"><span data-stu-id="6de3b-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)