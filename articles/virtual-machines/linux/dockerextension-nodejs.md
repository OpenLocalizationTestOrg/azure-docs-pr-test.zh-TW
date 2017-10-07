---
title: "以 hello Azure CLI 1.0 aaaUse hello Azure Docker VM 擴充功能 |Microsoft 文件"
description: "了解如何 toouse hello Docker VM 擴充功能 tooquickly 和安全地部署在 Azure 中使用資源管理員範本 Docker 環境。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>使用以 hello Azure CLI 1.0 hello Docker VM 擴充功能在 Azure 中建立 Docker 環境
Docker 是常用的容器管理和映像的平台，可讓您 tooquickly Linux （和 Windows 以及） 上的容器使用。 在 Azure 中，有各種方式，您可以部署 Docker 根據 tooyour 需求。 本文著重在使用 hello Docker VM 擴充功能和 Azure Resource Manager 範本。 

如需有關 hello 不同部署方法，包括使用 Docker 機器和 Azure 容器服務，請參閱下列文章 hello:

* tooquickly 原型應用程式，您可以建立單一的 Docker 主機使用[Docker 機器](docker-machine.md)。
* 對於規模較大且更穩定的環境，您可以使用 hello Azure Docker VM 擴充功能，也支援[Docker Compose](https://docs.docker.com/compose/overview/) toogenerate 一致的容器部署。 本文詳細說明使用 hello Azure Docker VM 擴充功能。
* toobuild 備妥、 可擴充式環境中提供其他的排程和管理工具，您可以部署[Azure 容器服務上的 Docker Swarm 叢集](../../container-service/dcos-swarm/container-service-deployment.md)。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#azure-docker-vm-extension-overview) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](dockerextension.md) -hello 資源管理部署模型我們下一個層代 CLI 

## <a name="azure-docker-vm-extension-overview"></a>Azure Docker VM 延伸模組概觀
hello Azure Docker VM 擴充功能中安裝和設定 hello Docker 精靈、 Docker 用戶端，和 Docker Compose Linux 虛擬機器 (VM)。 藉由使用 hello Azure Docker VM 擴充功能，您有更多的控制與比只需使用 Docker 機器，或自行建立 hello Docker 主機的功能。 這些其他功能，例如[Docker Compose](https://docs.docker.com/compose/overview/)，建立適用於更穩固的開發人員或實際執行環境的 hello Azure Docker VM 擴充功能。

Azure 資源管理員範本定義環境的 hello 整個結構。 範本 toocreate 可讓您和設定資源，例如 hello Docker 主機 Vm、 儲存體、 以角色為基礎的存取控制 (RBAC) 和診斷。 您可以重複使用這些範本 toocreate 其他部署，以一致的方式。 如需 Azure Resource Manager 和範本的詳細資訊，請參閱 [Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>部署具有 hello Azure Docker VM 擴充功能的範本
讓我們來使用現有的快速入門範本 toocreate 使用 hello Azure Docker VM 擴充功能 tooinstall Ubuntu VM，並設定 hello Docker 主機。 您可以檢視以下 hello 範本：[簡單 Ubuntu VM 部署使用 Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)。 

您需要 hello[最新的 Azure CLI](../../cli-install-nodejs.md)安裝並登入，如下所示使用 hello Resource Manager 模式：

```azurecli
azure config mode arm
```

部署 hello 範本使用 hello Azure CLI，並指定 hello 範本 URI。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *uswest*位置。 使用您自己的資源群組名稱和位置，如下所示︰

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

回答 hello 提示 tooname 儲存體帳戶，提供使用者名稱和密碼，並提供 DNS 名稱。 hello 輸出是 toohello 類似下列範例程式碼：

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

hello Azure CLI 傳回您 toohello 提示只有幾秒鐘後，但仍會建立您的 Docker 主機，並設定 hello Azure Docker VM 擴充功能。 花幾分鐘，讓 hello 部署 toofinish。 您可以檢視關於使用 hello hello Docker 主機狀態的詳細資料`azure vm show`命令。

hello 下列範例會檢查 hello 狀態 hello 名為 VM *myDockerVM* （hello hello 範本中的預設名稱-不要變更這個名稱） 在 hello 資源群組中名為*myResourceGroup*。 輸入 hello hello hello 前面步驟中建立的資源群組名稱：

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

hello 的 hello 輸出`azure vm show`命令是 toohello 類似下列範例：

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

靠近 hello 頂端的 hello 輸出，請參閱 hello **ProvisioningState**的 hello VM。 這會顯示當*Succeeded*、 hello 部署已完成，而且可以 SSH toohello VM。

Hello 結尾 hello 輸出朝*FQDN*顯示 hello Docker 主機完整的網域名稱。 此 FQDN 會是您的使用中其他步驟的 hello tooSSH tooyour Docker 主機。

## <a name="deploy-your-first-nginx-container"></a>部署您的第一個 nginx 容器
一次 hello 部署已完成，SSH tooyour 新 Docker 主機從本機電腦。 請輸入您自己的使用者名稱和 FQDN，如下所示︰

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

登入 toohello Docker 主機之後，我們先執行 nginx 容器：

```bash
sudo docker run -d -p 80:80 nginx
```

hello 輸出是下載 hello nginx 映像時，下列範例類似 toohello 和啟動容器：

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

檢查您的 Docker 主機上執行的如下所示的 hello 容器 hello 狀態：

```bash
sudo docker ps
```

hello 輸出是下列範例類似 toohello，顯示該 hello nginx 容器正在執行且 TCP 連接埠 80 和 443，被轉送：

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

toosee 您的容器，在動作中，開啟網頁瀏覽器並輸入您的 Docker 主機 hello FQDN 名稱：

![執行 ngnix 容器](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Azure Docker VM 延伸模組範本參考
hello 前一個範例會使用現有的快速入門範本。 您也可以使用您自己的資源管理員範本部署 hello Azure Docker VM 擴充功能。 toodo，加入下列 tooyour 資源管理員範本，定義 hello hello *vmName* VM 的適當地：

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

如需更詳細的 Resource Manager 範本使用逐步解說，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。

## <a name="next-steps"></a>後續步驟
您可能會希望太[設定 hello Docker daemon TCP 通訊埠](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket)，了解[Docker 安全性](https://docs.docker.com/engine/security/security/)，部署使用的容器或[Docker Compose](https://docs.docker.com/compose/overview/)。 如需有關 hello Azure Docker VM 擴充功能本身的詳細資訊，請參閱 hello [GitHub 專案](https://github.com/Azure/azure-docker-extension/)。

閱讀有關 hello 其他 Docker 部署 Azure 中的選項的詳細資訊：

* [使用 Docker 電腦以 hello Azure 驅動程式](docker-machine.md)  
* [開始使用 Docker 和撰寫 toodefine 和 Azure 虛擬機器上執行多個容器應用程式](docker-compose-quickstart.md)。
* [部署 Azure 容器服務叢集](../../container-service/dcos-swarm/container-service-deployment.md)

