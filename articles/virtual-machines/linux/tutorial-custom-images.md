---
title: "aaaCreate 自訂 VM 映像以 hello Azure CLI |Microsoft 文件"
description: "教學課程-建立自訂的 VM 映像，使用 Azure CLI hello。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>建立 Azure VM 使用 hello CLI 的自訂映像

自訂映像類似 Marketplace 映像，但您要自行建立它們。 自訂映像可以使用的 toobootstrap 組態，例如預先載入應用程式、 應用程式設定和其他作業系統設定。 在本教學課程中，您將建立自己的 Azure 虛擬機器自訂映像。 您會了解如何：

> [!div class="checklist"]
> * 取消佈建及一般化 VM
> * 建立自訂映像
> * 從自訂映像建立 VM
> * 列出您的訂用帳戶中的所有 hello 映像
> * 删除映像


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="before-you-begin"></a>開始之前

下列的 hello 步驟詳細說明 tootake 現有的 VM 並開啟它的可重複使用的自訂映像，您可以使用 toocreate 新 VM 執行個體。

在本教學課程 toocomplete hello 範例中的，您必須擁有現有的虛擬機器。 如有需要，這個[指令碼範例](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md)可以為您建立一部虛擬機器。 當工作透過 hello 教學課程中，取代 hello 資源群組和 VM 名稱在需要時。

## <a name="create-a-custom-image"></a>建立自訂映像

toocreate 虛擬機器的映像，您需要 tooprepare hello VM 和解除佈建、 解除配置，然後將標示 hello 來源為一般化 VM。 一次 hello 已經準備好 VM，您可以建立映像。

### <a name="deprovision-hello-vm"></a>取消佈建 VM hello 

藉由移除電腦特定的資訊來解除佈建一般化 hello VM。 這項通則可讓可能 toodeploy 許多 Vm 從單一映像。 在解除佈建，hello 主機名稱就會重設太*localhost.localdomain*。 SSH 主機金鑰、名稱伺服器設定、根密碼及快取的 DHCP 租用也會一併刪除。

toodeprovision hello VM，使用 hello Azure VM 代理程式 (waagent)。 hello Azure VM 代理程式安裝在 hello VM 上，及管理佈建和互動 hello Azure 網狀架構控制器。 如需詳細資訊，請參閱 hello [Azure Linux 代理程式使用者指南](agent-user-guide.md)。

連接 tooyour VM 使用 SSH 和執行的 hello 命令 toodeprovision hello VM。 以 hello`+user`引數、 hello 最後一個佈建的使用者帳戶和任何相關聯的資料也會一併刪除。 Hello 範例 IP 位址取代成您的 VM hello 公用 IP 位址。

SSH toohello VM。
```bash
ssh azureuser@52.174.34.95
```
取消佈建 hello VM。

```bash
sudo waagent -deprovision+user -force
```
關閉 hello SSH 工作階段。

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>解除配置，並將標示為一般化 VM hello

toocreate 映像，hello VM 需要 toobe 取消配置。 解除配置 hello VM 使用[az vm 解除配置](/cli//azure/vm#deallocate)。 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

最後，將 hello hello VM 狀態設定為與一般化[az vm 一般化](/cli//azure/vm#generalize)如此 hello Azure 平台才會知道的 hello VM 已一般化。 您只能從一般化的 VM 建立映像。
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>建立 hello 映像

現在您可以使用，以建立 hello VM 的映像[az 映像建立](/cli//azure/image#create)。 hello 下列範例會建立名為映像*myImage*從名為 VM *myVM*。
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>從 hello 映像建立 Vm

既然您具有映像，您可以建立一或多個新的 Vm 從 hello 映像使用[az vm 建立](/cli/azure/vm#create)。 hello 下列範例會建立名為的 VM *myVMfromImage*從名為 「 hello 」 映像*myImage*。

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>映像管理 

以下是一些範例的映像的一般管理工作以及 toocomplete 它們使用 Azure CLI hello。

以資料表格式依名稱列出所有映像。

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

删除映像。 此範例中刪除 hello 名為映像*myOldImage*從 hello *myResourceGroup*。

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>後續步驟

您在本教學課程中建立了自訂 VM 映像。 您已了解如何︰

> [!div class="checklist"]
> * 取消佈建及一般化 VM
> * 建立自訂映像
> * 從自訂映像建立 VM
> * 列出您的訂用帳戶中的所有 hello 映像
> * 删除映像

前進 toohello 下一個教學課程的 toolearn 有關高可用性虛擬機器。

> [!div class="nextstepaction"]
> [建立高可用性 VM](tutorial-availability-sets.md)。

