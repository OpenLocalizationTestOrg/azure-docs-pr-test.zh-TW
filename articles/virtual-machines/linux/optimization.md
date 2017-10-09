---
title: "aaaOptimize 您在 Azure 上的 Linux VM |Microsoft 文件"
description: "確定您已將您的 Linux VM，以獲得最佳效能，在 Azure 上設定某些最佳化提示 toomake 深入了解"
keywords: "linux 虛擬機器,虛擬機器 linux,ubuntu 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a>在 Azure 上最佳化 Linux VM
建立 Linux 虛擬機器 (VM) 是簡單 toodo 從 hello 命令列或從 hello 入口網站。 本教學課程會示範如何 tooensure 您設定它 toooptimize 其效能 hello Microsoft Azure 平台上。 本主題會使用 Ubuntu Server VM，但您也可以使用 [自己的映像做為範本](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)來建立 Linux 虛擬機器。  

## <a name="prerequisites"></a>必要條件
本主題假設您已具備有效的 Azure 訂用帳戶 ([註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/))，並且已在 Azure 訂用帳戶中佈建 VM。 請確定您擁有 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooyour 與 Azure 訂用帳戶[az 登入](/cli/azure/#login)之前[建立 VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="azure-os-disk"></a>Azure 作業系統磁碟
在 Azure 中建立 Linux VM 後，它有兩個相關聯的磁碟。 **/dev/sda** 是作業系統磁碟，**/dev/sdb** 是暫存磁碟。  請勿使用 hello 主要作業系統磁碟 (**/開發/sda**) 的 hello 作業系統，因為它以外的項目最適合用於快速 VM 開機時間，但未提供良好的效能，為您的工作負載。 您想要 tooattach 其中一個或多個磁碟 tooyour VM tooget 持續性和最佳化儲存體的資料。 

## <a name="adding-disks-for-size-and-performance-targets"></a>加入磁碟以達成大小和效能目標
根據 hello VM 大小，您可以附加 too16 額外的磁碟上 A 系列、 D 系列上的 32 磁碟和 G 系列電腦-每個向上 too1 TB 大小上的 64 部磁碟。 您可以根據空間和 IOps 需求加入額外的磁碟。 每個磁碟具有 500 IOps 效能的目標，標準儲存體及其上層 too5000 每個磁碟的 IOps Premium 儲存體。  如需進階儲存體磁碟的詳細資訊，請參閱[進階儲存體：Azure VM 的高效能儲存體](../../storage/common/storage-premium-storage.md)

tooachieve hello 其快取設定具有已設定的 tooeither Premium 儲存體磁碟上的最高 IOps **ReadOnly**或**無**，您必須停用**障礙**時在 Linux 中掛接 hello 檔案系統。 因為 hello 寫入 tooPremium 儲存備份的磁碟是永久性的這些快取設定不需要的障礙。

* 如果您使用**reiserFS**、 使用 hello 掛接選項停用障礙`barrier=none`(啟用的障礙，使用`barrier=flush`)
* 如果您使用**ext3/ext4**、 使用 hello 掛接選項停用障礙`barrier=0`(啟用的障礙，使用`barrier=1`)
* 如果您使用**XFS**、 使用 hello 掛接選項停用障礙`nobarrier`(啟用的障礙，使用 hello 選項`barrier`)

## <a name="unmanaged-storage-account-considerations"></a>非受控儲存體帳戶考量事項
當您使用 hello Azure CLI 2.0 來建立 VM 的 hello 的預設動作是 toouse Azure 受管理的磁碟。  這些磁碟都由 hello Azure 平台，而且不需要任何準備或位置 toostore 它們。  非受控磁碟需要儲存體帳戶，且具有一些額外的效能注意事項。  如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟概觀](../windows/managed-disks-overview.md)。  hello 下列各節概述效能考量僅當您使用未受管理的磁碟。  同樣地，hello 預設和建議的儲存體解決方案是 toouse 管理磁碟。

如果您建立未受管理磁碟 VM，請確定您將磁碟附加來自相同位於 hello 的儲存體帳戶與 VM tooensure 區域接近和網路延遲降至最低。  每個標準儲存體帳戶都有最高 20k 的 IOps 和 500 TB 大小的容量。  這項限制適用於出 tooapproximately 40 大量使用磁碟，包括 hello OS 磁碟和任何您所建立的資料磁碟。 進階儲存體帳戶沒有 IOps 上限，不過有 32 TB 的大小限制。 

當處理高 IOps 工作負載，而且您已選擇標準儲存體的磁碟時，您可能需要 toosplit hello 磁碟跨多個儲存體帳戶 toomake 確定不叫用的 hello 20,000 IOps 限制標準儲存體帳戶。 您的 VM 可以包含混合的磁碟跨不同的儲存體帳戶和儲存體帳戶類型 tooachieve 最佳的設定。
 

## <a name="your-vm-temporary-drive"></a>VM 暫存磁碟機
根據預設，當您建立 VM 時，Azure 會提供作業系統磁碟 (**/dev/sda**) 和暫存磁碟 (**/dev/sdb**)。  您加入的所有額外磁碟會顯示為 **/dev/sdc**、**/dev/sdd**、**/dev/sde**，依此類推。 暫存磁碟 (**/dev/sdb**) 上的所有資料均不具持久性，因此當 VM 調整大小、重新部署或維護等特定事件發生迫使 VM 重新啟動時，資料可能會遺失。  hello 大小與類型的暫存磁碟是您選擇在部署階段的相關的 toohello VM 大小。 Hello premium 大小 Vm （DS、 G 和 DS_V2 系列） hello 暫存磁碟機的所有備份的本機 SSD 的總 too48k IOps 的其他效能。 

## <a name="linux-swap-file"></a>Linux 交換檔
如果您的 Azure VM 從 Ubuntu 或 CoreOS 映像，您可以使用 CustomData toosend 雲端組態 toocloud init。 如果您[上傳自訂 Linux 映像](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，使用 cloud-init，您也可以使用 cloud-init 設定交換資料分割。

Ubuntu 雲端映像，您必須使用雲端 init tooconfigure hello 交換資料分割。 如需詳細資訊，請參閱 [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)。

沒有雲端 init 支援的映像，從 hello Azure Marketplace 部署的 VM 映像會有與 hello OS 整合的 Linux VM 代理程式。 此代理程式可讓您將 VM toointeract hello 與不同 Azure 服務。 假設您已部署的 hello Azure Marketplace 的標準映像，您就必須 toodo hello 遵循 toocorrectly 設定設定 Linux 交換檔：

找出和修改兩個項目在 hello **/etc/waagent.conf**檔案。 它們控制 hello 存在專用的交換檔案和 hello 分頁檔大小。 您要尋找 toomodify hello 參數`ResourceDisk.EnableSwap=N`和`ResourceDisk.SwapSizeMB=0` 

變更 hello 參數 toohello 下列設定：

* ResourceDisk.EnableSwap=Y
* ResourceDisk.SwapSizeMB={size MB toomeet 在您的需求。 

一旦您所做變更的 hello，您需要 toorestart hello waagent 或重新啟動 Linux VM tooreflect 這些變更。  您知道實作 hello 變更，而且交換檔已經建立，當您使用 hello`free`命令 tooview 可用空間。 hello 下列範例具有 512 MB 交換檔建立的結果修改 hello **waagent.conf**檔案：

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a>進階儲存體的 I/O 排程演算法
與 hello 2.6.18 Linux 核心，hello 預設 I/O 排程演算法已經從期限 tooCFQ （完全公平佇列演算法）。 對於隨機 I/O 模式，CFQ 與期限之間的效能差異並不明顯。  Ssd 磁碟 hello 磁碟 I/O 模式，主要是循序，切換回 toohello NOOP 或期限演算法可以達到較佳的 I/O 效能。

### <a name="view-hello-current-io-scheduler"></a>檢視 hello 目前 I/O 排程器
使用下列命令的 hello:  

```bash
cat /sys/block/sda/queue/scheduler
```

您會看到下列輸出，表示 hello 目前排程器。  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a>變更 hello 目前的裝置 (/ 開發/sda) 的排程演算法的 I/O
使用下列命令的 hello:  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> 單獨針對 **/dev/sda** 套用此設定不是很有用。 所有資料磁碟上設定了該位置循序 I/O 將優先於 hello I/O 模式。  

您應該會看到下列輸出，表示 hello **grub.cfg**已成功重建，且該 hello 預設排程器已更新的 tooNOOP。  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

Hello Redhat 發佈系列，您只需要 hello 下列命令：   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a>使用較高的軟體 RAID tooachieve 我 / Ops
如果您的工作負載需要更多的 IOps 比單一磁碟可提供，您會需要 toouse 軟體 RAID 組態的多個磁碟。 因為 Azure 已經執行 hello 本機網狀架構層級的磁碟復原，您會達成 hello 最高從 RAID 0 等量配置設定的效能層級。  佈建和 hello Azure 環境中建立磁碟，並將它們附加 tooyour Linux VM，資料分割、 格式化及裝載 hello 磁碟機之前。  需在 azure 中 Linux VM 上設定軟體 RAID 安裝程式的詳細資訊，請參閱 hello  **[Linux 上的 [設定軟體 RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)** 文件。

## <a name="next-steps"></a>後續步驟
請記住，所有的最佳化討論中，您需要 tooperform 測試之前和之後每個變更 toomeasure hello 影響 hello 項變更有。  最佳化是需要逐步進行的程序，這些程序會對環境中不同的機器產生不同的結果。  對某項組態有用的做法不見得適用於其他組態。

一些有用連結 tooadditional 的資源： 

* [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/common/storage-premium-storage.md)
* [Azure Linux 代理程式使用者指南](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [在 Azure Linux VM 上最佳化 MySQL 效能](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [在 Linux 上設定軟體 RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

