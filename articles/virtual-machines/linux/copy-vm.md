---
title: "aaaCopy Linux VM，使用 Azure CLI 2.0 |Microsoft 文件"
description: "深入了解如何 toocreate Azure Linux VM 使用 Azure CLI 2.0 和管理磁碟的複本。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>使用 Azure CLI 2.0 和受控磁碟來建立 Azure Linux VM 的複本


本文章將示範如何 toocreate 一份您執行 Azure 虛擬機器 (VM) 使用 Linux hello Azure CLI 2.0 和 hello Azure Resource Manager 部署模型。 您也可以執行下列步驟以 hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

您也可以[上傳 VHD 並從中建立 VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="prerequisites"></a>必要條件


-   安裝 [Azure CLI 2.0](/cli/azure/install-az-cli2)

-   使用的 Azure 帳戶登入 tooan [az 登入](/cli/azure/#login)。

-   有 Azure VM toouse 為 hello 您複製的來源。

## <a name="step-1-stop-hello-source-vm"></a>步驟 1： 停止 hello 來源 VM


Deallocate hello 來源 VM 使用[az vm 解除配置](/cli/azure/vm#deallocate)。
hello 下列範例會取消配置 hello 名為 VM **myVM** hello 資源群組中**myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>步驟 2： 複製 hello 來源 VM


toocopy VM，您會建立一份 hello 基礎虛擬硬碟。 此程序會建立特殊的 VHD 做為受管理的磁碟包含 hello 來源 VM 相同的組態和 hello 的設定。

如需 Azure 受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。 

1.  列出每個 VM 和 hello 名稱含有其 OS 磁碟[az vm 清單](/cli/azure/vm#list)。 hello 下列範例會列出名為的資源群組中所有 Vm **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    hello 輸出是 toohello 類似下列範例程式碼：

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  使用磁碟管理來建立新的複製 hello 磁碟[az 磁碟建立](/cli/azure/disk#create)。 hello 下列範例會建立名為的磁碟**myCopiedDisk** hello 從受管理磁碟名為**myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  使用確認正在資源群組中的受管理的 hello 磁碟[az 磁碟清單](/cli/azure/disk#list)。 hello 下列範例會列出名為 「 hello 資源群組中的受管理的 hello 磁碟**myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  略過太[「 步驟 3： 設定虛擬網路 」](#step-3-set-up-a-virtual-network)。


## <a name="step-3-set-up-a-virtual-network"></a>步驟 3︰設定虛擬網路


hello 下列選擇性步驟建立新的虛擬網路、 子網路、 公用 IP 位址，與虛擬網路介面卡 (NIC)。

如果您複製 VM 疑難排解用途或其他部署，您可能不想 toouse 中現有的虛擬網路的 VM。

如果您想要複製 Vm toocreate 虛擬網路基礎結構，後續 hello 接下來的幾個步驟。 如果您不想 toocreate 虛擬網路，請略過太[步驟 4： 建立 VM](#step-4-create-a-vm)。

1.  使用建立虛擬網路的 hello [az 網路 vnet 建立](/cli/azure/network/vnet#create)。 hello 下列範例會建立虛擬網路，名為**myVnet**和名為的子網路**mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  使用 [az network public-ip create](/cli/azure/network/public-ip#create) 建立公用 IP。 hello 下列範例會建立名為公用 IP **myPublicIP** hello DNS 名稱是**mypublicdns**。 （hello DNS 名稱必須是唯一的因此提供唯一的名稱。)

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  建立 hello NIC 使用[az 網路 nic 建立](/cli/azure/network/nic#create)。
    hello 下列範例會建立名為的 NIC **myNic**的附加的 toothe **mySubnet**子網路：

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>步驟 4：建立 VM

您現在可以使用 [az vm create](/cli/azure/vm#create) 建立 VM。

指定 hello 複製為 hello OS 磁碟的受管理的磁碟 toouse (-附加 os 磁碟)，如下：

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>後續步驟

toolearn 如何 toouse Azure CLI toomanage 新的 VM，請參閱[hello Azure 資源管理員的 Azure CLI 命令](../azure-cli-arm-commands.md)。
