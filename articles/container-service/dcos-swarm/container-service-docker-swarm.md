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
# <a name="container-management-with-docker-swarm"></a>使用 Docker Swarm 管理容器
Docker Swarm 提供跨一組匯集的 Docker 主機來部署容器化工作負載的環境。 Docker 群集使用 hello 原生 Docker 的 API。 管理容器上的 Docker Swarm 的 hello 工作流程是將在單一容器主機的 toowhat 幾乎完全相同。 本文件提供在 Docker Swarm 的 Azure 容器服務執行個體中部署容器化工作負載的簡單範例。 如需有關 Docker Swarm 的更深入文件，請參閱 [Docker.com 上的 Docker Swarm](https://docs.docker.com/swarm/)。

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

這份文件中的必要條件 toohello 練習：

[在 Azure 容器服務中建立 Swarm 叢集](container-service-deployment.md)

[連接與 Azure 容器服務中的 hello 群集叢集](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>部署新容器
toocreate hello Docker Swarm，在新的容器使用 hello `docker run` （確保您已開啟根據上述必要條件 hello SSH 通道 toohello 母片） 的命令。 這個範例會建立容器，從 hello`yeasy/simple-web`映像：

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

建立 hello 容器之後，使用`docker ps`tooreturn hello 容器的資訊。 請注意，這裡裝載 hello 容器該 hello 群集代理程式會列出：

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

您現在可以存取執行 hello 公開 DNS 名稱的 hello 群集代理程式負載平衡器透過此容器中的 hello 應用程式。 您可以在 hello Azure 入口網站中找到這項資訊：  

![實際瀏覽結果](./media/container-service-docker-swarm/real-visit.jpg)  

根據預設 hello 負載平衡器的連接埠 80、 8080 和 443 開啟。 如果您想在另一個連接埠上的 tooconnect 您需要 tooopen hello Azure 負載平衡器上的該連接埠 hello 代理程式集區。

## <a name="deploy-multiple-containers"></a>部署多個容器
啟動多個容器，藉由執行 'docker run' 多次，您可以使用 hello`docker ps`命令 toosee 裝載 hello 容器上執行。 在 hello 下列範例中，三個容器分散到平均 hello 三個群集代理程式：  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>使用 Docker Compose 來部署容器
您可以使用 Docker Compose tooautomate hello 部署和設定多個容器。 已建立安全殼層 (SSH) 通道，且已設定該 hello DOCKER_HOST 變數 （請參閱 hello 上述的必要元件），因此，請確定 toodo。

在您的本機系統上建立 docker-compose.yml 檔案。 toodo，以此[範例](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml)。

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

執行`docker-compose up -d`toostart hello 容器部署：

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

最後，將會傳回執行中容器的 hello 清單。 這份清單會反映透過 Docker Compose 已部署的 hello 容器：

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

當然，您可以使用`docker-compose ps`tooexamine 只 hello 容器中定義您`compose.yml`檔案。

## <a name="next-steps"></a>後續步驟
[深入了解 Docker Swarm](https://docs.docker.com/swarm/)

