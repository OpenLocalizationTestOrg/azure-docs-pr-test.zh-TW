---
title: "快速入門 - 適用於 Linux 的 Azure Docker Swarm 叢集 | Microsoft Docs"
description: "快速了解如何在 Azure Container Service 中使用 Azure CLI 建立適用於 Linux 容器的 Docker Swarm 叢集。"
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
ms.openlocfilehash: 1d10c347795227ed056a95d1bcd4aff82af7b876
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="ee8f4-103">部署 Docker Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="ee8f4-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="ee8f4-104">本快速入門中會使用 Azure CLI 來部署 Docker Swarm 叢集。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-104">In this quick start, a Docker Swarm cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="ee8f4-105">接著，在叢集上部署和執行多容器應用程式，其中包含 Web 前端和 Redis 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="ee8f4-106">完成後，即可透過網際網路來存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="ee8f4-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="ee8f4-108">本快速入門需要您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-108">This quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ee8f4-109">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="ee8f4-110">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ee8f4-111">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="ee8f4-111">Create a resource group</span></span>

<span data-ttu-id="ee8f4-112">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ee8f4-113">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="ee8f4-114">下列範例會在 westus 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-114">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="ee8f4-115">輸出：</span><span class="sxs-lookup"><span data-stu-id="ee8f4-115">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="ee8f4-116">建立 Docker Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="ee8f4-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="ee8f4-117">使用 [az acs create](/cli/azure/acs#create) 命令，在 Azure Container Service 中建立 Docker Swarm 叢集。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-117">Create a Docker Swarm cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="ee8f4-118">下列範例會建立一個名為 mySwarmCluster 的叢集，其中包含一個 Linux 主要節點和三個 Linux 代理程式節點。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-118">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="ee8f4-119">幾分鐘之後，此命令就會完成，並以 json 格式傳回叢集的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-119">After several minutes, the command completes and returns json formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="ee8f4-120">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="ee8f4-120">Connect to the cluster</span></span>

<span data-ttu-id="ee8f4-121">在本快速入門中，您需要 Docker Swarm 主機和 Docker 代理程式集區的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-121">Throughout this quick start, you need the IP address of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="ee8f4-122">執行下列命令以傳回這兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-122">Run the following command to return both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="ee8f4-123">輸出：</span><span class="sxs-lookup"><span data-stu-id="ee8f4-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="ee8f4-124">建立 Swarm 主機的 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-124">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="ee8f4-125">以 Swarm 主機的 IP 位址取代 `IPAddress`。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-125">Replace `IPAddress` with the IP address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="ee8f4-126">設定 `DOCKER_HOST` 環境變數。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-126">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="ee8f4-127">這可讓您對 Docker Swarm 執行 Docker 命令，而不需指定主機名稱。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-127">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="ee8f4-128">您現在已經準備好在 Docker Swarm 上執行 Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-128">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="ee8f4-129">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ee8f4-129">Run the application</span></span>

<span data-ttu-id="ee8f4-130">建立名為 `docker-compose.yaml` 的檔案，並將下列內容複製到其中。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-130">Create a file named `docker-compose.yaml` and copy the following content into it.</span></span>

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

<span data-ttu-id="ee8f4-131">請執行下列命令來建立 Azure 投票服務。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-131">Run the following command to create the Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="ee8f4-132">輸出：</span><span class="sxs-lookup"><span data-stu-id="ee8f4-132">Output:</span></span>

```bash
Creating network "user_default" with the default driver
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

## <a name="test-the-application"></a><span data-ttu-id="ee8f4-133">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="ee8f4-133">Test the application</span></span>

<span data-ttu-id="ee8f4-134">瀏覽至 Swarm 代理程式集區的 IP 位址，以測試 Azure 投票應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-134">Browse to the IP address of the Swarm agent pool to test out the Azure Vote application.</span></span>

![瀏覽至 Azure 投票的影像](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="ee8f4-136">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="ee8f4-136">Delete cluster</span></span>
<span data-ttu-id="ee8f4-137">若不再需要叢集，您可以使用 [az group delete](/cli/azure/group#delete) 命令來移除資源群組、容器服務和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-137">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="ee8f4-138">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="ee8f4-138">Get the code</span></span>

<span data-ttu-id="ee8f4-139">在本快速入門中，預先建立的容器映像已用來建立 Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-139">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="ee8f4-140">在 GitHub 上可取得相關的應用程式程式碼、Dockerfile 和 Compose 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-140">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="ee8f4-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="ee8f4-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="ee8f4-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee8f4-142">Next steps</span></span>

<span data-ttu-id="ee8f4-143">在本快速入門中，您已部署 Docker Swarm 叢集，並將多容器應用程式部署到此叢集。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="ee8f4-144">若要了解如何整合 Docker Swarm 與 Visual Studio Team Services，請繼續進行搭配 Docker Swarm 和 VSTS 的 CI/CD。</span><span class="sxs-lookup"><span data-stu-id="ee8f4-144">To learn about integrating Docker warm with Visual Studio Team Services, continue to the CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee8f4-145">搭配 Docker Swarm 和 VSTS 的 CI/CD</span><span class="sxs-lookup"><span data-stu-id="ee8f4-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)