---
title: "aaaAzure 容器服務教學課程-管理 DC/OS |Microsoft 文件"
description: "Azure Container Service 教學課程 - 管理 DC/OS"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, 容器, 微服務, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Azure Container Service 教學課程 - 管理 DC/OS

DC/OS 所提供的分散式平台可執行現代及容器化的應用程式。 透過 Azure Container Service 可簡單又快速地佈建生產環境就緒 DC/OS 叢集。 DC/OS 叢集並執行基本的工作負載需要 toodeploy 此快速入門詳細資料的基本步驟。

> [!div class="checklist"]
> * 建立 ACS DC/OS 叢集
> * Toohello 叢集連線
> * 安裝 hello DC/OS CLI
> * 部署應用程式 toohello 叢集
> * 調整 hello 叢集上的應用程式
> * 調整 hello DC/OS 叢集節點
> * DC/OS 的基本管理
> * 刪除 hello DC/OS 叢集

本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="create-dcos-cluster"></a>建立 DC/OS 叢集

首先，建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *westeurope*位置。

```azurecli
az group create --name myResourceGroup --location westeurope
```

接下來，建立 hello DC/OS 叢集[az acs 建立](/cli/azure/acs#create)命令。

hello 下列範例會建立名為 DC/OS 叢集*myDCOSCluster*並建立 SSH 金鑰，如果它們尚不存在。 toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

幾分鐘之後，hello 命令完成，且傳回 hello 部署的相關資訊。

## <a name="connect-toodcos-cluster"></a>TooDC/OS 叢集連線

一旦建立 DC/OS 叢集之後，可透過 SSH 通道加以存取。 執行下列命令 tooreturn hello 公用 IP 位址的 hello DC/OS master hello。 此 IP 位址是儲存在變數中，而且用於 hello 下一個步驟。

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate hello SSH 通道，執行下列命令的 hello 並遵循螢幕上指示 hello。 如果連接埠 80 已在使用中，hello 命令將會失敗。 更新 hello 通道連接埠 tooone 不在使用中，例如`85:localhost:80`。 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>安裝 DC/OS CLI

安裝使用 hello hello DC/OS cli [az acs dcos 安裝 cli](/azure/acs/dcos#install-cli)命令。 如果您使用 Azure CloudShell，hello DC/OS CLI 已安裝。 如果您執行 hello Azure CLI macOS 或 Linux 上，您可能需要具有 sudo toorun hello 命令。

```azurecli
az acs dcos install-cli
```

之前可使用 CLI 來與 hello 叢集 hello，它必須設定的 toouse hello SSH 通道。 toodo 因此，執行下列命令，如有需要調整 hello 連接埠的 hello。

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>執行應用程式

hello 預設排程 ACS DC/OS 叢集中的機制是馬拉松。 馬拉松是使用的 toostart 的應用程式，並管理 hello hello hello DC/OS 叢集上的應用程式狀態。 tooschedule 馬拉松，透過應用程式建立名為**馬拉松 app.json**，並複製 hello 遵循到其中的內容。 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

執行下列命令 tooschedule hello 應用程式 toorun hello DC/OS 叢集上的 hello。

```azurecli
dcos marathon app add marathon-app.json
```

hello 應用程式中，執行下列命令的 hello toosee hello 部署狀態。

```azurecli
dcos marathon app list
```

當 hello**工作**資料行值會從切換*0/1*太*1/1*，應用程式部署已完成。

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>調整 Marathon 應用程式

在 hello 前一個範例中，建立單一執行個體的應用程式。 此部署，以便 hello 應用程式的三個執行個體可用，開啟 hello tooupdate**馬拉松 app.json**檔案，並更新 hello 執行個體屬性 too3。

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

更新 hello 應用程式使用 hello`dcos marathon app update`命令。

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

hello 應用程式中，執行下列命令的 hello toosee hello 部署狀態。

```azurecli
dcos marathon app list
```

當 hello**工作**資料行值會從切換*1/3*太*3/1*，應用程式部署已完成。

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>執行網際網路可存取應用程式

hello ACS DC/OS 叢集包含兩個節點集合，可存取在上一個公用 hello 網際網路，並不能存取在其中一個私用 hello 網際網路。 hello 預設集是 hello 私用的節點，這使用於 hello 最後一個範例。

應用程式存取 toomake hello 網際網路，將其部署 toohello 公用節點集。 toodo，授與 hello`acceptedResourceRoles`物件的值`slave_public`。

建立名為**nginx public.json**並複製 hello 遵循到其中的內容。

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

執行下列命令 tooschedule hello 應用程式 toorun hello DC/OS 叢集上的 hello。

```azurecli 
dcos marathon app add nginx-public.json
```

收到 hello 公用 IP 位址的 hello DC/OS 公用叢集代理程式。

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

瀏覽 toothis 位址傳回 hello 預設 NGINX 站台。

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>調整 DC/OS 叢集

在 hello 上述範例中，應用程式會是縮放的 toomultiple 執行個體。 hello DC/OS 基礎結構也可以縮放的 tooprovide 更多或更少計算容量。 這是以 hello [az acs 調整]()命令。 

toosee hello 目前計數的 DC/OS 代理程式，使用 hello [az acs 顯示](/cli/azure/acs#show)命令。

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease hello 計數 too5，請使用 hello [az acs 調整](/cli/azure/acs#scale)命令。 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>刪除 DC/OS 叢集

當不再需要您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 DC/OS 叢集，以及所有相關的資源。

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已經學會基本的 DC/OS 管理工作，包括 hello 下列有關。 

> [!div class="checklist"]
> * 建立 ACS DC/OS 叢集
> * Toohello 叢集連線
> * 安裝 hello DC/OS CLI
> * 部署應用程式 toohello 叢集
> * 調整 hello 叢集上的應用程式
> * 調整 hello DC/OS 叢集節點
> * 刪除 hello DC/OS 叢集

進階 toohello 下一個教學課程 toolearn 有關負載平衡的應用程式在 Azure 上的 DC/OS。 

> [!div class="nextstepaction"]
> [負載平衡應用程式](container-service-load-balancing.md)