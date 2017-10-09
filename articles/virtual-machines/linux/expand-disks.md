---
title: "aaaExpand 虛擬硬碟在 Azure 中的 Linux VM 上 |Microsoft 文件"
description: "了解如何 tooexpand 虛擬硬碟與 Linux VM 上 hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>如何 tooexpand 虛擬硬碟與 Linux VM 上 hello Azure CLI
hello hello 作業系統 (OS) 的預設虛擬硬碟大小通常是 30 GB 在 Azure 中 Linux 虛擬機器 (VM) 上。 您可以[加入資料磁碟](add-disk.md)tooprovide 額外的儲存空間，但是您可能希望 tooexpand 的現有資料磁碟。 這篇文章說明 tooexpand 針對 Linux VM 以 hello Azure CLI 2.0 所管理的磁碟。 您也可以展開與 hello hello unmanaged OS 磁碟[Azure CLI 1.0](expand-disks-nodejs.md)。

> [!WARNING]
> 在執行磁碟調整大小作業前，務必備份資料。 如需詳細資訊，請參閱[在 Azure 中備份 Linux 虛擬機器](tutorial-backup-vms.md)。

## <a name="expand-disk"></a>擴充磁碟
請確定您擁有 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

本文需要 Azure 中存有一個虛擬機器，且該虛擬機器至少掛載一個已備妥使用的資料磁碟。 如果您還沒有可使用的虛擬機器，請參閱[建立並準備掛載有資料磁碟的虛擬機器](tutorial-manage-disks.md#create-and-attach-disks)。

Hello 在下列範例中，會取代您自己的值範例參數名稱。 範例參數名稱包含 myResourceGroup 與 myVM。

1. 虛擬硬碟上的作業無法執行以 hello VM 執行。 使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置您的 VM。 hello 下列範例會取消配置 hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`不會釋放 hello 計算資源。 toorelease 計算資源，請使用`az vm deallocate`。 必須解除配置 hello VM tooexpand hello 虛擬硬碟。

2. 使用 [az disk list](/cli/azure/disk#list) 來檢視資源群組中的受控磁碟清單。 hello 下列範例顯示的受管理的磁碟清單 hello 資源群組中名為*myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    展開所需的磁碟 hello 與[az 磁碟更新](/cli/azure/disk#update)。 hello 下列範例會展開 hello 受管理的磁碟，名為*myDataDisk* toobe *200*Gb 大小：

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > 當您展開受管理的磁碟時，更新的 hello 大小會是對應的 toohello 最接近的受管理的磁碟大小。 Hello 受管理的可用磁碟大小與層級的資料表，請參閱[Azure 受管理磁碟概觀-定價和計費](../windows/managed-disks-overview.md#pricing-and-billing)。

3. 使用 [az vm create](/cli/azure/vm#start) 啟動 VM。 下列範例開始 hello hello 名為 VM *myVM* hello 資源群組中名為*myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM 與 hello 適當的認證。 您可以取得具有您 VM 的 hello 公用 IP 位址[az vm 顯示](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. toouse hello 展開磁碟時，您需要 tooexpand hello 基礎磁碟分割及檔案系統。

    a. 如果已掛上，取消掛接 hello 磁碟：

    ```bash
    sudo umount /dev/sdc1
    ```

    b. 使用`parted`tooview 磁碟資訊並調整大小 hello 磁碟分割：

    ```bash
    sudo parted /dev/sdc
    ```

    檢視與 hello 現有磁碟分割配置的相關資訊`print`。 hello 輸出類似 toohello 之後，範例中，會顯示 hello 基礎磁碟的大小是 215 Gb:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. 展開的資料分割 hello 和`resizepart`。 輸入 hello 分割區編號， *1*，和 hello 新資料分割的大小：

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit，輸入`quit`

5. Hello 調整大小的磁碟分割，以確認與 hello 分割區一致性`e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. 現在調整與 hello filesystem `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. 掛接 hello 分割 toohello 預期的位置，例如`/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. tooverify hello 作業系統磁碟大小已經過調整，請使用`df -h`。 下列範例輸出的 hello 顯示 hello 資料磁碟機， */開發/sdc1*，現在為 200 GB:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>後續步驟
如果您需要額外的存放裝置，您也[新增資料磁碟 tooa Linux VM](add-disk.md)。 如需磁碟加密的詳細資訊，請參閱[使用 Linux VM 上的加密磁碟 hello Azure CLI](encrypt-disks.md)。
