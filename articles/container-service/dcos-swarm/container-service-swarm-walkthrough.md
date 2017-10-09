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
# <a name="deploy-docker-swarm-cluster"></a>部署 Docker Swarm 叢集

在這個快速入門，Docker Swarm 叢集中使用 hello Azure CLI 部署。 然後部署並 hello 叢集上執行多個容器應用程式，其中包含 web 前端和 Redis 執行個體。 Hello 應用程式完成後，會透過可存取網際網路的 hello。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

本快速入門需要執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。

## <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯群組。

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *uswest*位置。

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

輸出：

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

## <a name="create-docker-swarm-cluster"></a>建立 Docker Swarm 叢集

在 Azure 容器服務中建立 Docker Swarm 叢集以 hello [az acs 建立](/cli/azure/acs#create)命令。 

hello 下列範例會建立名為叢集*mySwarmCluster*一個 Linux 的主要節點和三個 Linux 代理程式節點。

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

幾分鐘之後，hello 命令完成，並傳回 hello 叢集的 json 格式資訊。

## <a name="connect-toohello-cluster"></a>Toohello 叢集連線

在這個快速入門中，您需要 hello hello Docker Swarm master 和 hello Docker 代理程式集區的 IP 位址。 執行下列命令 tooreturn hello 兩個 IP 位址。


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

輸出：

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

建立 SSH 通道 toohello 群集 master。 取代`IPAddress`hello hello 群集的主要 IP 位址。

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

設定 hello`DOCKER_HOST`環境變數。 這可讓您針對 hello Docker Swarm toorun docker 命令而不需要 toospecify hello hello 主機名稱。

```bash
export DOCKER_HOST=:2375
```

現在您已經準備就緒 toorun hello Docker Swarm 上的 Docker 服務。


## <a name="run-hello-application"></a>執行 hello 應用程式

建立名為`docker-compose.yaml`並複製 hello 遵循到其中的內容。

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

執行下列命令 toocreate hello Azure 投票服務的 hello。

```bash
docker-compose up -d
```

輸出：

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

## <a name="test-hello-application"></a>測試 hello 應用程式

瀏覽 toohello 的 hello 群集代理程式集區 tootest 出 hello Azure 投票應用程式的 IP 位址。

![瀏覽 tooAzure 投票的映像](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>刪除叢集
當不再需要 hello 叢集時，您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 容器服務，以及所有相關的資源。

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>取得 hello 程式碼

在這個快速入門中，預先建立的容器映像已使用的 toocreate Docker 服務。 hello 相關應用程式程式碼，Dockerfile 中，且可在 GitHub 上編輯檔案。

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>後續步驟

在這個快速入門中，您可以部署 Docker Swarm 叢集並部署多個容器應用程式 tooit。

有關使用 Visual Studio Team Services，整合 Docker 暖 toolearn 繼續 toohello CI/CD 與 Docker Swarm VSTS。

> [!div class="nextstepaction"]
> [搭配 Docker Swarm 和 VSTS 的 CI/CD](./container-service-docker-swarm-setup-ci-cd.md)