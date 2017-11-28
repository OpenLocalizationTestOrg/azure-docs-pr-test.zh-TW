---
title: "Docker 的 api 叢集 aaaManage Azure 廣域 |Microsoft 文件"
description: "容器 tooa Docker Swarm 叢集部署在 Azure 容器服務"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker、容器、微服務、Mesos、Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="99f02-104">使用 Docker Swarm 管理容器</span><span class="sxs-lookup"><span data-stu-id="99f02-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="99f02-105">Docker Swarm 提供跨一組匯集的 Docker 主機來部署容器化工作負載的環境。</span><span class="sxs-lookup"><span data-stu-id="99f02-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="99f02-106">Docker 群集使用 hello 原生 Docker 的 API。</span><span class="sxs-lookup"><span data-stu-id="99f02-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="99f02-107">管理容器上的 Docker Swarm 的 hello 工作流程是將在單一容器主機的 toowhat 幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="99f02-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="99f02-108">本文件提供在 Docker Swarm 的 Azure 容器服務執行個體中部署容器化工作負載的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="99f02-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="99f02-109">如需有關 Docker Swarm 的更深入文件，請參閱 [Docker.com 上的 Docker Swarm](https://docs.docker.com/swarm/)。</span><span class="sxs-lookup"><span data-stu-id="99f02-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="99f02-110">這份文件中的必要條件 toohello 練習：</span><span class="sxs-lookup"><span data-stu-id="99f02-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="99f02-111">在 Azure 容器服務中建立 Swarm 叢集</span><span class="sxs-lookup"><span data-stu-id="99f02-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="99f02-112">連接與 Azure 容器服務中的 hello 群集叢集</span><span class="sxs-lookup"><span data-stu-id="99f02-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="99f02-113">部署新容器</span><span class="sxs-lookup"><span data-stu-id="99f02-113">Deploy a new container</span></span>
<span data-ttu-id="99f02-114">toocreate hello Docker Swarm，在新的容器使用 hello `docker run` （確保您已開啟根據上述必要條件 hello SSH 通道 toohello 母片） 的命令。</span><span class="sxs-lookup"><span data-stu-id="99f02-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="99f02-115">這個範例會建立容器，從 hello`yeasy/simple-web`映像：</span><span class="sxs-lookup"><span data-stu-id="99f02-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="99f02-116">建立 hello 容器之後，使用`docker ps`tooreturn hello 容器的資訊。</span><span class="sxs-lookup"><span data-stu-id="99f02-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="99f02-117">請注意，這裡裝載 hello 容器該 hello 群集代理程式會列出：</span><span class="sxs-lookup"><span data-stu-id="99f02-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="99f02-118">您現在可以存取執行 hello 公開 DNS 名稱的 hello 群集代理程式負載平衡器透過此容器中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99f02-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="99f02-119">您可以在 hello Azure 入口網站中找到這項資訊：</span><span class="sxs-lookup"><span data-stu-id="99f02-119">You can find this information in hello Azure portal:</span></span>  

![實際瀏覽結果](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="99f02-121">根據預設 hello 負載平衡器的連接埠 80、 8080 和 443 開啟。</span><span class="sxs-lookup"><span data-stu-id="99f02-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="99f02-122">如果您想在另一個連接埠上的 tooconnect 您需要 tooopen hello Azure 負載平衡器上的該連接埠 hello 代理程式集區。</span><span class="sxs-lookup"><span data-stu-id="99f02-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="99f02-123">部署多個容器</span><span class="sxs-lookup"><span data-stu-id="99f02-123">Deploy multiple containers</span></span>
<span data-ttu-id="99f02-124">啟動多個容器，藉由執行 'docker run' 多次，您可以使用 hello`docker ps`命令 toosee 裝載 hello 容器上執行。</span><span class="sxs-lookup"><span data-stu-id="99f02-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="99f02-125">在 hello 下列範例中，三個容器分散到平均 hello 三個群集代理程式：</span><span class="sxs-lookup"><span data-stu-id="99f02-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="99f02-126">使用 Docker Compose 來部署容器</span><span class="sxs-lookup"><span data-stu-id="99f02-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="99f02-127">您可以使用 Docker Compose tooautomate hello 部署和設定多個容器。</span><span class="sxs-lookup"><span data-stu-id="99f02-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="99f02-128">已建立安全殼層 (SSH) 通道，且已設定該 hello DOCKER_HOST 變數 （請參閱 hello 上述的必要元件），因此，請確定 toodo。</span><span class="sxs-lookup"><span data-stu-id="99f02-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="99f02-129">在您的本機系統上建立 docker-compose.yml 檔案。</span><span class="sxs-lookup"><span data-stu-id="99f02-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="99f02-130">toodo，以此[範例](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml)。</span><span class="sxs-lookup"><span data-stu-id="99f02-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

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

<span data-ttu-id="99f02-131">執行`docker-compose up -d`toostart hello 容器部署：</span><span class="sxs-lookup"><span data-stu-id="99f02-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

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

<span data-ttu-id="99f02-132">最後，將會傳回執行中容器的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="99f02-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="99f02-133">這份清單會反映透過 Docker Compose 已部署的 hello 容器：</span><span class="sxs-lookup"><span data-stu-id="99f02-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="99f02-134">當然，您可以使用`docker-compose ps`tooexamine 只 hello 容器中定義您`compose.yml`檔案。</span><span class="sxs-lookup"><span data-stu-id="99f02-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99f02-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99f02-135">Next steps</span></span>
[<span data-ttu-id="99f02-136">深入了解 Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="99f02-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

