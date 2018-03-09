---
title: "使用 Docker API 管理 Azure Swarm 叢集"
description: "在 Azure Container Service 中將容器部署至 Docker Swarm 叢集"
services: container-service
author: rgardler
manager: madhana
ms.service: container-service
ms.topic: article
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 3f8d18bc053bc303ab124ba38c8621d4ee2e8cb8
ms.sourcegitcommit: 694e40a193980dea1e2f945471071f11030d5641
ms.translationtype: MTE
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2018
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="542db-103">使用 Docker Swarm 管理容器</span><span class="sxs-lookup"><span data-stu-id="542db-103">Container management with Docker Swarm</span></span>

<span data-ttu-id="542db-104">Docker Swarm 提供跨一組匯集的 Docker 主機來部署容器化工作負載的環境。</span><span class="sxs-lookup"><span data-stu-id="542db-104">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="542db-105">Docker Swarm 使用原生 Docker API。</span><span class="sxs-lookup"><span data-stu-id="542db-105">Docker Swarm uses the native Docker API.</span></span> <span data-ttu-id="542db-106">用來管理 Docker Swarm 上容器的工作流程與在單一容器主機時的工作流程幾乎相同。</span><span class="sxs-lookup"><span data-stu-id="542db-106">The workflow for managing containers on a Docker Swarm is almost identical to what it would be on a single container host.</span></span> <span data-ttu-id="542db-107">本文件提供在 Docker Swarm 的 Azure 容器服務執行個體中部署容器化工作負載的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="542db-107">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="542db-108">如需有關 Docker Swarm 的更深入文件，請參閱 [Docker.com 上的 Docker Swarm](https://docs.docker.com/swarm/)。</span><span class="sxs-lookup"><span data-stu-id="542db-108">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="542db-109">本文件中之練習的先決條件︰</span><span class="sxs-lookup"><span data-stu-id="542db-109">Prerequisites to the exercises in this document:</span></span>

[<span data-ttu-id="542db-110">在 Azure 容器服務中建立 Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="542db-110">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="542db-111">連接到 Azure 容器服務中的 Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="542db-111">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="542db-112">部署新容器</span><span class="sxs-lookup"><span data-stu-id="542db-112">Deploy a new container</span></span>
<span data-ttu-id="542db-113">若要在 Docker Swarm 中建立新容器，請使用 `docker run` 命令 (確定您已根據上述必要條件開啟主機的 SSH 通道)。</span><span class="sxs-lookup"><span data-stu-id="542db-113">To create a new container in the Docker Swarm, use the `docker run` command (ensuring that you have opened an SSH tunnel to the masters as per the prerequisites above).</span></span> <span data-ttu-id="542db-114">此範例會從 `yeasy/simple-web` 映像建立容器：</span><span class="sxs-lookup"><span data-stu-id="542db-114">This example creates a container from the `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="542db-115">建立容器之後，使用 `docker ps` 傳回容器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="542db-115">After the container has been created, use `docker ps` to return information about the container.</span></span> <span data-ttu-id="542db-116">請注意，這裡會列出裝載容器的 Swarm 代理程式：</span><span class="sxs-lookup"><span data-stu-id="542db-116">Notice here that the Swarm agent that is hosting the container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="542db-117">您現在可以透過 Swarm 代理程式負載平衡器的公用 DNS 名稱來存取此容器中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="542db-117">You can now access the application that is running in this container through the public DNS name of the Swarm agent load balancer.</span></span> <span data-ttu-id="542db-118">您可在 Azure 入口網站中找到此資訊：</span><span class="sxs-lookup"><span data-stu-id="542db-118">You can find this information in the Azure portal:</span></span>  

![實際瀏覽結果](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="542db-120">根據預設，Load Balancer 開啟連接埠 80、8080 和 443。</span><span class="sxs-lookup"><span data-stu-id="542db-120">By default the Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="542db-121">如果您想要在另一個連接埠上連接，您必須在 Azure Load Balancer 上針對代理程式集區開啟該連接埠。</span><span class="sxs-lookup"><span data-stu-id="542db-121">If you want to connect on another port you will need to open that port on the Azure Load Balancer for the Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="542db-122">部署多個容器</span><span class="sxs-lookup"><span data-stu-id="542db-122">Deploy multiple containers</span></span>
<span data-ttu-id="542db-123">藉由多次執行 'docker run' 來啟動多個容器時，您可以使用 `docker ps` 命令來查看容器執行所在的主機。</span><span class="sxs-lookup"><span data-stu-id="542db-123">As multiple containers are started, by executing 'docker run' multiple times, you can use the `docker ps` command to see which hosts the containers are running on.</span></span> <span data-ttu-id="542db-124">在以下範例中，三個容器平均分散在三個 Swarm 代理程式中：</span><span class="sxs-lookup"><span data-stu-id="542db-124">In the example below, three containers are spread evenly across the three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="542db-125">使用 Docker Compose 來部署容器</span><span class="sxs-lookup"><span data-stu-id="542db-125">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="542db-126">您可以使用 Docker Compose 來自動部署和設定多個容器。</span><span class="sxs-lookup"><span data-stu-id="542db-126">You can use Docker Compose to automate the deployment and configuration of multiple containers.</span></span> <span data-ttu-id="542db-127">若要這麼做，請確定已建立安全殼層 (SSH) 通道，並已設定 DOCKER_HOST 變數 (請參閱上述的必要元件)。</span><span class="sxs-lookup"><span data-stu-id="542db-127">To do so, ensure that a Secure Shell (SSH) tunnel has been created and that the DOCKER_HOST variable has been set (see the pre-requisites above).</span></span>

<span data-ttu-id="542db-128">在您的本機系統上建立 docker-compose.yml 檔案。</span><span class="sxs-lookup"><span data-stu-id="542db-128">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="542db-129">若要這樣做，請使用此 [範例](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml)。</span><span class="sxs-lookup"><span data-stu-id="542db-129">To do this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="542db-130">執行 `docker-compose up -d` 以啟動容器部署：</span><span class="sxs-lookup"><span data-stu-id="542db-130">Run `docker-compose up -d` to start the container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="542db-131">最後，將會傳回執行中容器的清單。</span><span class="sxs-lookup"><span data-stu-id="542db-131">Finally, the list of running containers will be returned.</span></span> <span data-ttu-id="542db-132">這份清單會反映使用 Docker Compose 所部署的容器︰</span><span class="sxs-lookup"><span data-stu-id="542db-132">This list reflects the containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="542db-133">當然，您可以使用 `docker-compose ps`，只檢查 `compose.yml` 檔案中定義的容器。</span><span class="sxs-lookup"><span data-stu-id="542db-133">Naturally, you can use `docker-compose ps` to examine only the containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="542db-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="542db-134">Next steps</span></span>
[<span data-ttu-id="542db-135">深入了解 Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="542db-135">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

