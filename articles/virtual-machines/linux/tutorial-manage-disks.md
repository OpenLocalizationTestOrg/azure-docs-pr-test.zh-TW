---
title: "aaaManage Azure 磁碟以 hello Azure CLI |Microsoft 文件"
description: "教學課程-管理 Azure 磁碟以 hello Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>管理 Azure 磁碟以 hello Azure CLI

Azure 虛擬機器使用的磁碟 toostore hello Vm 作業系統、 應用程式和資料。 建立 VM 時，重要 toochoose 磁碟大小和設定適當的 toohello 預期工作負載。 本教學課程涵蓋部署和管理 VM 磁碟。 您將了解：

> [!div class="checklist"]
> * OS 磁碟和暫存磁碟
> * 資料磁碟
> * 標準和進階磁碟
> * 磁碟效能
> * 連結及準備資料磁碟
> * 調整磁碟的大小
> * 磁碟快照集


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="default-azure-disks"></a>預設 Azure 磁碟

建立 Azure 虛擬機器時，兩個磁碟會自動附加的 toohello 虛擬機器。 

**作業系統磁碟**-作業系統磁碟可以 too1 tb 向上調整大小和主機 hello Vm 的作業系統。 hello OS 磁碟標示*/開發/sda*預設。 hello 磁碟快取的 hello 作業系統磁碟組態已針對 OS 效能最佳化。 此設定，因為 hello OS 磁碟**不應該**裝載應用程式或資料。 請對應用程式和資料使用資料磁碟，本文稍後會詳細說明。 

**暫存磁碟**-暫存磁碟使用固態磁碟機上 hello hello VM 為相同的 Azure 主機。 暫存磁碟的效能非常好，可用於暫存資料處理等作業。 不過，如果 hello VM 移動的 tooa 新主機，就會移除儲存在暫存磁碟上的任何資料。 hello hello 暫存磁碟的大小取決於 hello VM 大小。 暫存磁碟會標示為 /dev/sdb，其掛接點為 /mnt。

### <a name="temporary-disk-sizes"></a>暫存磁碟大小

| 類型 | VM 大小 | 暫存磁碟大小上限 (GB) |
|----|----|----|
| [一般用途](sizes-general.md) | A 和 D 系列 | 800 |
| [計算最佳化](sizes-compute.md) | F 系列 | 800 |
| [記憶體最佳化](../virtual-machines-windows-sizes-memory.md) | D 和 G 系列 | 6144 |
| [儲存體最佳化](../virtual-machines-windows-sizes-storage.md) | L 系列 | 5630 |
| [GPU](sizes-gpu.md) | N 系列 | 1440 |
| [高效能](sizes-hpc.md) | A 和 H 系列 | 2000 |

## <a name="azure-data-disks"></a>Azure 資料磁碟

您可以新增額外資料磁碟，以便安裝應用程式和儲存資料。 資料磁碟應使用於任何需要持久且有回應之資料儲存體的情況。 每個資料磁碟的最大容量為 1 TB。 hello hello 虛擬機器大小會決定資料磁碟數目可為附加的 tooa VM。 每個 VM 核心可以連結兩個資料磁碟。 

### <a name="max-data-disks-per-vm"></a>每部 VM 的資料磁碟上限

| 類型 | VM 大小 | 每部 VM 的資料磁碟上限 |
|----|----|----|
| [一般用途](sizes-general.md) | A 和 D 系列 | 32 |
| [計算最佳化](sizes-compute.md) | F 系列 | 32 |
| [記憶體最佳化](../virtual-machines-windows-sizes-memory.md) | D 和 G 系列 | 64 |
| [儲存體最佳化](../virtual-machines-windows-sizes-storage.md) | L 系列 | 64 |
| [GPU](sizes-gpu.md) | N 系列 | 48 |
| [高效能](sizes-hpc.md) | A 和 H 系列 | 32 |

## <a name="vm-disk-types"></a>VM 磁碟類型

Azure 提供兩種類型的磁碟。

### <a name="standard-disk"></a>標準磁碟

標準儲存體是以 HDD 為後盾，既可提供符合成本效益的儲存體，又可保有效能。 標準磁碟適合用於具成本效益的開發和測試工作負載。

### <a name="premium-disk"></a>進階磁碟

進階磁碟是以 SSD 為基礎的高效能、低延遲磁碟為後盾。 最適合用於執行生產工作負載的 VM。 進階儲存體支援 DS 系列、DSv2 系列、GS 系列和 FS 系列 VM。 高階磁碟都是以三種類型 (P10，P20，P30)，hello hello 磁碟大小會決定 hello 磁碟類型。 選取時，磁碟大小 hello 值會無條件進位 toohello 下一個類型。 例如，如果 hello 磁碟大小小於 128 GB，hello 磁碟類型為 P10。 如果 hello 磁碟大小為 512 GB 129 GB 之間，hello 大小是 P20。 任何超過 512 GB hello 大小是 P30。

### <a name="premium-disk-performance"></a>進階磁碟效能

|進階儲存體磁碟類型 | P10 | P20 | P30 |
| --- | --- | --- | --- |
| 磁碟大小 (上調) | 128 GB | 512 GB | 1,024 GB (1 TB) |
| 每一磁碟的 IOPS 上限 | 500 | 2,300 | 5,000 |
每一磁碟的輸送量 | 100 MB/秒 | 150 MB/秒 | 200 MB/秒 |

雖然資料表上方的 hello 會識別每個磁碟的最大 IOPS 較高的效能等級可藉由多個資料磁碟條狀配置。 例如，Standard_GS5 VM 最高可達到 80,000 IOPS。 如需每部 VM 的最大 IOPS 詳細資訊，請參閱 [Linux VM 大小](sizes.md)。

## <a name="create-and-attach-disks"></a>建立和連結磁碟

可以建立資料磁碟，並將其附加到 VM 建立時或 tooan 現有 VM。

### <a name="attach-disk-at-vm-creation"></a>在建立 VM 時連結磁碟

建立資源群組以 hello [az 群組建立](https://docs.microsoft.com/cli/azure/group#create)命令。 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

建立 VM 使用 hello [az vm 建立]( /cli/azure/vm#create)命令。 hello`--datadisk-sizes-gb`引數是使用的 toospecify 應該建立額外的磁碟，並附加 toohello 虛擬機器。 toocreate 和連接一個以上的磁碟，請使用空格分隔的磁碟大小值清單。 在下列範例的 hello，VM 會建立使用兩個資料磁碟時，這兩個 128 GB。 Hello 磁碟大小為 128 GB，因為這些磁碟都設定為 P10s，提供每個磁碟的最大 500 IOPS。

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>附加磁碟 tooexisting VM

toocreate 並附加新磁碟 tooan 現有的虛擬機器，請使用 hello [az vm 磁碟附加](/cli/azure/vm/disk#attach)命令。 hello 下列範例會建立 premium 磁碟，128 gb 的大小，並將其附加的 toohello hello 最後一個步驟中建立的 VM。

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>準備資料磁碟

一旦磁碟已附加的 toohello 虛擬機器，必須設定 toobe toouse hello 磁碟 hello 作業系統。 hello 下列範例顯示如何 toomanually 設定的磁碟。 使用 cloud-init (涵蓋於[稍後的教學課程](./tutorial-automate-vm-deployment.md)中) 也可以將此程序自動化。

### <a name="manual-configuration"></a>手動設定

建立 SSH 連線與 hello 虛擬機器。 Hello hello 虛擬機器的公用 IP 取代 hello 範例 IP 位址。

```azurecli-interactive 
ssh 52.174.34.95
```

分割磁碟 hello `fdisk`。

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

寫入檔案系統 toohello 磁碟分割使用 hello`mkfs`命令。

```bash
sudo mkfs -t ext4 /dev/sdc1
```

掛接 hello 新磁碟，使其在 hello 作業系統中存取。

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

hello 磁碟現在可以存取透過 hello *datadrive*掛接點，您可以藉由執行 hello 驗證`df -h`命令。 

```bash
df -h
```

hello 輸出會顯示 hello 新磁碟機上有掛載*/datadrive*。

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

hello 磁碟機的 tooensure 會重新掛上重新開機後，必須將它加入 toohello */etc/hosts fstab*檔案。 開始以 hello hello 的 hello 磁碟 UUID 吧，toodo`blkid`公用程式。

```bash
sudo -i blkid
```

hello 輸出會顯示 hello 的 hello 磁碟 UUID`/dev/sdc1`在此情況下。

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

新增下列 toohello 列類似 toohello */etc/hosts fstab*檔案。 也請注意，使用 barrier=0 可以停用寫入屏障，此組態可以改善磁碟效能。 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

既然 hello 磁碟已設定，關閉 hello SSH 工作階段。

```bash
exit
```

## <a name="resize-vm-disk"></a>調整 VM 磁碟的大小

一旦部署 VM 的大小可以增加 hello 作業系統磁碟或任何附加的資料磁碟。 當需要更多儲存空間或更高 （P10、 P20、 P30） 時，增加 hello 大小是磁碟的效能的有益的。 請注意，磁碟的大小不能減少。

增加磁碟大小，hello 識別碼前後需要 hello 磁碟的名稱。 使用 hello [az 磁碟清單](/cli/azure/vm/disk#list)命令 tooreturn 所有磁碟區在資源群組。 請注意 hello 磁碟名稱希望 tooresize。

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

hello VM 也必須已解除配置。 使用 hello [az vm 解除配置]( /cli/azure/vm#deallocate)命令 toostop 及取消配置 hello VM。

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

使用 hello [az 磁碟更新](/cli/azure/vm/disk#update)命令 tooresize hello 磁碟。 此範例會調整大小的磁碟，名為*myDataDisk* too1 tb。

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

Hello 的調整大小作業完成後，請啟動 hello VM。

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

如果作業系統磁碟的 hello 調整大小時會自動展開 hello 磁碟分割。 如果您已調整大小的資料磁碟，任何目前的資料分割需要 toobe hello Vm 作業系統中，展開節點。

## <a name="snapshot-azure-disks"></a>建立 Azure 磁碟快照集

取得磁碟的快照集建立 hello 磁碟的讀取，時間點複本。 Azure VM 的快照集可用於快速進行組態變更之前儲存 hello VM 的狀態。 在 hello 事件 hello 組態變更證明 toobe 討厭，可以使用 hello 快照還原 VM 狀態。 當 VM 有多個磁碟時，快照時每個磁碟與 hello 無關的其他人。 進行應用程式一致備份，請考慮在執行磁碟快照集之前停止 hello VM。 或者，使用 hello [Azure 備份服務](/azure/backup/)，這可讓您 tooperform 自動化的 hello VM 正在執行時進行備份。

### <a name="create-snapshot"></a>建立快照集

之前建立的虛擬機器磁碟的快照，hello 識別碼或名稱 hello 磁碟的需要。 使用 hello [az vm 顯示](https://docs.microsoft.com/en-us/cli/azure/vm#show)命令 tooreturn hello 磁碟識別碼。在此範例中，hello 磁碟識別碼儲存在變數，使其可以用於在稍後的步驟。

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

您已經有 hello 識別碼 hello 虛擬機器磁碟，hello 下列命令會建立 hello 磁碟的快照集。

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>從快照集建立磁碟

這個快照可轉換成使用的 toorecreate hello 虛擬機器磁碟。

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>從快照集還原虛擬機器

刪除 hello 現有虛擬機器 toodemonstrate 虛擬機器復原。 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

建立新的虛擬機器從 hello 快照集磁碟。

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>重新連結資料磁碟

所有的資料磁碟都必須重新附加 toobe toohello 虛擬機器。

首先尋找 hello 資料磁碟名稱使用 hello [az 磁碟清單](https://docs.microsoft.com/cli/azure/disk#list)命令。 此範例中的位置 hello hello 磁碟中名為的變數名稱*datadisk*，hello 下一個步驟中所用。

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

使用 hello [az vm 磁碟附加](https://docs.microsoft.com/cli/azure/vm/disk#attach)命令 tooattach hello 磁碟。

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解 VM 磁碟的相關主題，像是：

> [!div class="checklist"]
> * OS 磁碟和暫存磁碟
> * 資料磁碟
> * 標準和進階磁碟
> * 磁碟效能
> * 連結及準備資料磁碟
> * 調整磁碟的大小
> * 磁碟快照集

前進 toohello 下一個教學課程的 toolearn 自動化 VM 組態。

> [!div class="nextstepaction"]
> [自動設定 VM](./tutorial-automate-vm-deployment.md)
