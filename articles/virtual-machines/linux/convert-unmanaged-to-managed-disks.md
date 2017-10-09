---
title: "在 Azure 中 Linux 虛擬機器，從 unmanaged aaaConvert 磁碟 toomanaged 磁碟-Azure 受管理磁碟 |Microsoft 文件"
description: "Tooconvert unmanaged 的磁碟 toomanaged 從 Linux VM 磁碟 hello Resource Manager 部署模型中使用 Azure CLI 2.0 的方式"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>從 unmanaged 的磁碟 toomanaged 磁碟轉換 Linux 虛擬機器

如果您有現有 Linux 虛擬機器 (Vm)，並且使用未受管理的磁碟，您可以將透過 hello hello Vm toouse 管理磁碟轉換[Azure 受管理磁碟](../windows/managed-disks-overview.md)服務。 此程序轉換 hello OS 磁碟和任何連接的資料磁碟。

本文章將示範如何使用 tooconvert Vm hello Azure CLI。 如果您需要 tooinstall，或將它升級，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。 

## <a name="before-you-begin"></a>開始之前

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>轉換單一執行個體 VM
本章節涵蓋 tooconvert 單一執行個體中未受管理的 Azure Vm 磁碟 toomanaged 磁碟的方式。 （如果您的 Vm 可用性設定組中，請參閱 hello 下一節）。您可以使用此程序 tooconvert hello Vm 從高階 (SSD) 不受管理磁碟 toopremium 管理磁碟，或從標準 (HDD) 不受管理磁碟 toostandard 管理磁碟。

1. 使用解除配置 hello VM [az vm 解除配置](/cli/azure/vm#deallocate)。 hello 下列範例會取消配置 hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. 使用轉換 hello VM toomanaged 磁碟[az vm 轉換](/cli/azure/vm#convert)。 下列程序會將轉換的 hello hello 名為 VM `myVM`，包括 hello OS 磁碟和任何資料磁碟：

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. 使用 hello 轉換 toomanaged 磁碟後啟動 hello VM [az vm 啟動](/cli/azure/vm#start)。 下列範例開始 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`。

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>轉換可用性設定組中的 VM

如果您想要 tooconvert toomanaged 磁碟都在可用性設定組中的 hello Vm，您必須先管理 tooconvert hello 可用性集 tooa 可用性設定組。

在轉換 hello 可用性設定組之前，必須取消配置 hello 可用性設定組中的所有 Vm。 計劃 tooconvert hello 可用性之後的所有 Vm toomanaged 磁碟都設定本身已受管理的轉換的 tooa 可用性設定都組。 然後，啟動所有 hello Vm，並持續正常運作。

1. 使用 [az vm availability-set list](/cli/azure/vm/availability-set#list) 來列出可用性設定組中的所有 VM。 hello 下列範例會列出所有 Vm hello 可用性設定組具名`myAvailabilitySet`hello 資源群組中名為`myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. 解除配置使用的所有 hello Vm [az vm 解除都配置](/cli/azure/vm#deallocate)。 hello 下列範例會取消配置 hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. 轉換 hello 可用性設定組使用[az vm 的可用性設定組轉換](/cli/azure/vm/availability-set#convert)。 hello 下列範例會將轉換 hello 可用性設定組具名`myAvailabilitySet`hello 資源群組中名為`myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. 使用轉換所有 hello Vm toomanaged 磁碟[az vm 都轉換](/cli/azure/vm#convert)。 下列程序會將轉換的 hello hello 名為 VM `myVM`，包括 hello OS 磁碟和任何資料磁碟：

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. 啟動所有 hello Vm hello 轉換 toomanaged 磁碟之後，使用[az vm 都啟動](/cli/azure/vm#start)。 下列範例開始 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>後續步驟
如需儲存體選項的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。
