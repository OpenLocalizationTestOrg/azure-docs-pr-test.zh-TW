---
title: "使用 CLI 2.0 在 Azure 中 Linux VM 的映像 aaaCapture |Microsoft 文件"
description: "擷取映像，如需使用 Azure CLI 2.0 hello 的大型部署 Azure VM toouse。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>如何 toocreate 的虛擬機器或 VHD 映像

<!-- generalize, image - extended version of hello tutorial-->

toocreate 多個副本在 Azure 中，虛擬機器 (VM) toouse 擷取 hello VM 映像或 hello OS VHD。 toocreate 映像，您需要移除個人的帳戶資訊，使其更安全的 toodeploy 多次。 在您解除佈建現有 VM 的步驟 hello，取消配置並建立映像。 您可以使用此映像 toocreate Vm 之間的任何資源群組，您的訂用帳戶內。

如果您想要備份或偵錯，toocreate 現有的 Linux VM 的複本或特定的 Linux VHD 從內部部署 VM 上傳，請參閱[上傳並從自訂的磁碟映像建立 Linux VM](upload-vhd.md)。  

您也可以使用**Packer** toocreate 您的自訂設定。 如需有關使用 Packer 的詳細資訊，請參閱[toouse Packer toocreate Linux 虛擬機器在 Azure 中的映像](build-image-with-packer.md)。


## <a name="before-you-begin"></a>開始之前
請確定您符合下列必要條件 hello:

* 您必須使用受管理的磁碟 hello Resource Manager 部署模型中建立 Azure VM。 如果您尚未建立 Linux VM，您可以使用 hello[入口網站](quick-create-portal.md)，hello [Azure CLI](quick-create-cli.md)，或[資源管理員範本](create-ssh-secured-vm-from-template.md)。 設定 VM，視 hello。 例如，[新增資料磁碟](add-disk.md)、套用更新，並安裝應用程式。 

* 您也需要 toohave hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

## <a name="quick-commands"></a>快速命令

本主題，適用於測試的簡化版本的評估，或深入了解 Azure 中的 Vm，請參閱[建立自訂映像的 Azure VM 使用 hello CLI](tutorial-custom-images.md)。


## <a name="step-1-deprovision-hello-vm"></a>步驟 1： 解除佈建 VM hello
您解除佈建 hello hello Azure VM 代理程式、 toodelete 機器特定檔案和資料所使用的 VM。 使用 hello`waagent`命令與 hello *-取消佈建 + 使用者*您來源 Linux VM 上的參數。 如需詳細資訊，請參閱 hello [Azure Linux 代理程式使用者指南](../windows/agent-user-guide.md)。

1. 連接 tooyour 使用 SSH 用戶端的 Linux VM。
2. 在 hello SSH 視窗中，輸入下列命令的 hello:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > 只有執行此命令在 VM 上的您想 toocapture 做為映像。 它並不保證清除所有的機密資訊的 hello 映像，或適用於轉散發。 hello *+ 使用者*參數也會移除 hello 最後一個佈建的使用者帳戶。 如果您想 tookeep hello VM 中的帳戶認證，只要使用*-取消佈建*就地 tooleave hello 使用者帳戶。
 
3. 型別**y** toocontinue。 您可以新增 hello **-強制**參數 tooavoid 此確認步驟。
4. Hello 命令完成之後，請輸入**結束**。 此步驟會關閉 hello SSH 用戶端。

## <a name="step-2-create-vm-image"></a>步驟 2：建立 VM 映像
使用 Azure CLI 2.0 hello toomark hello VM 一般化，擷取 hello 映像。 在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。

1. 解除配置 hello 解除與佈建的 VM [az vm 解除配置](/cli//azure/vm#deallocate)。 hello 下列範例會取消配置 hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. 標記 hello 工作者角色是與一般化[az vm 一般化](/cli//azure/vm#generalize)。 下列範例標記 hello hello VM 名為 hello *myVM* hello 資源群組中名為*myResourceGroup*為一般化：
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. 現在建立 hello VM 資源的映像[az 映像建立](/cli//azure/image#create)。 hello 下列範例會建立名為映像*myImage* hello 資源群組中名為*myResourceGroup*使用名為 hello VM 資源*myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > hello 映像中建立 hello 相同資源群組，做為來源 VM。 您可以從此映像，在您訂用帳戶的任何資源群組中建立 VM。 管理的觀點而言，您可能希望 toocreate 您 VM 資源和影像的特定資源群組。

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>步驟 3： 從 hello 擷取映像建立 VM
使用您建立與 hello 映像建立 VM [az vm 建立](/cli/azure/vm#create)。 hello 下列範例會建立名為的 VM *myVMDeployed*從名為 「 hello 」 映像*myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>建立另一個資源群組中的 hello VM 

您可以從某個映像，在您訂用帳戶的任何資源群組中建立 VM。 toocreate 比 hello 影像的不同資源群組中的 VM 指定 hello 完整資源識別碼 tooyour 映像。 使用[az 影像清單](/cli/azure/image#list)tooview 映像清單。 hello 輸出是 toohello 類似下列範例程式碼：

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

hello 下列範例會使用[az vm 建立](/cli/azure/vm#create)toocreate 比藉由指定 hello 的影像資源識別碼 hello 來源影像的不同資源群組中的 VM:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>步驟 4： 驗證 hello 部署

現在 SSH toohello 建立虛擬機器您 tooverify hello 部署並開始使用 hello 新的 VM。 透過 SSH，tooconnect 尋找具有您 VM 的 hello IP 位址或者 FQDN [az vm 顯示](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>後續步驟
您可以從來源 VM 映像建立多個 VM。 如果您需要 toomake 變更 tooyour 映像： 

- 從映像建立 VM。
- 進行任何更新或組態變更。
- 請遵循 hello 步驟再次 toodeprovision、 取消、 一般化，和建立映像。
- 在日後的部署中使用這個新映像。 如有需要，刪除 hello 原始映像。

如需有關如何管理您的 Vm 以 hello CLI 的詳細資訊，請參閱[Azure CLI 2.0](/cli/azure/overview)。
