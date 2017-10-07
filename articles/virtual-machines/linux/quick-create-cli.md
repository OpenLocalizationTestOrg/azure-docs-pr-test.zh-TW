---
title: "快速入門-aaaAzure 建立 VM CLI |Microsoft 文件"
description: "快速了解以 hello Azure CLI toocreate 虛擬機器。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>建立 Linux 虛擬機器以 hello Azure CLI

hello Azure CLI 會使用的 toocreate 和管理 Azure 資源，從 hello 命令列或指令碼中。 本指南將詳細說明使用 hello Azure CLI toodeploy 執行 Ubuntu server 的虛擬機器。 Hello 伺服器部署之後，建立 SSH 連線，以及 NGINX 網頁伺服器已安裝。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本快速入門會要求執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine

建立 VM 以 hello [az vm 建立](/cli/azure/vm#create)命令。 

hello 下列範例會建立名為的 VM *myVM*並建立 SSH 金鑰，如果它們原本不在預設索引鍵位置。 toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

建立 hello VM 後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。 記下 hello `publicIpAddress`。 此位址為使用的 tooaccess hello VM。

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>針對 Web 流量開啟連接埠 80 

依預設只能透過 SSH 連線至 Azure 中部署的 Linux 虛擬機器。 如果此 VM 將會 toobe web 伺服器，您需要從網際網路 hello tooopen 連接埠 80。 使用 hello [az vm 開啟通訊埠](/cli/azure/vm#open-port)命令 tooopen hello 所需的連接埠。  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>透過 SSH 連線到您的 VM

使用 hello 下列命令 toocreate 與 hello 虛擬機器的 SSH 工作階段。 請確定 tooreplace  *<publicIpAddress>*  hello 包含正確的虛擬機器的公用 IP 位址。  在上面的範例中，我們的 IP 位址是 40.68.254.142。

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>安裝 NGINX

使用 hello 以下撞指令碼 tooupdate 封裝來源，並安裝最新 NGINX 套件 hello。 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>檢視 hello NGINX 歡迎使用 頁面

現在從 hello 網際網路-VM 上開啟連接埠 80 與 NGINX 安裝中，您可以使用網頁瀏覽器，您的選擇 tooview hello 預設 NGINX 歡迎頁面。 要確定 toouse hello *publicIpAddress*您 toovisit hello 預設頁面上面所記載。 

![預設 NGINX 網站](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>清除資源

當不再需要您可以使用 hello [az 群組刪除](/cli/azure/group#delete)命令 tooremove hello 資源群組、 VM 和所有相關的資源。

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。 進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Linux Vm。


> [!div class="nextstepaction"]
> [Azure Linux 虛擬機器教學課程](./tutorial-manage-vm.md)
