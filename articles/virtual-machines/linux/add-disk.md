---
title: "磁碟 tooLinux VM 使用 aaaAdd hello Azure CLI |Microsoft 文件"
description: "了解 tooadd hello Azure CLI 1.0 和 2.0 的持續性磁碟 tooyour Linux VM。"
keywords: "linux 虛擬機器,新增資源磁碟"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a>新增磁碟 tooa Linux VM
本文將說明如何 tooattach 的永續性磁碟 tooyour VM，以便您可以保留您的資料-即使您的 VM 重新佈建由於 toomaintenance 或調整大小。 

## <a name="quick-commands"></a>快速命令
下列範例將 hello `50`GB 磁碟 toohello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:

toouse 管理磁碟：

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

toouse unmanaged 磁碟：

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>附加受控磁碟

使用受管理的磁碟可讓您在您的 Vm 和其磁碟上的 toofocus 而不需擔心 Azure 儲存體帳戶。 您可以快速地建立並附加受管理的磁碟 tooa VM 使用 hello 相同的 Azure 資源群組，或您可以建立任意數目的磁碟，然後將其連接。


### <a name="attach-a-new-disk-tooa-vm"></a>附加新的磁碟 tooa VM

如果您只需要新的磁碟，在您的 VM 上，您可以使用 hello`az vm disk attach`命令。

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>連接現有磁碟 

在許多情況下，您可以附加已建立的磁碟。 您首先尋找 hello 磁碟識別碼，然後將傳遞該 toohello`az vm disk attach`命令。 hello 下列範例會使用磁碟，以建立`az disk create -g myResourceGroup -n myDataDisk --size-gb 50`。

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

hello 輸出看起來類似下列 hello (您可以使用 hello`-o table`選項 tooany 命令 tooformat hello 輸出中的):

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a>附加非受控磁碟

正在將新的磁碟是如果您不介意在 hello 建立磁碟的快速 VM 相同儲存體帳戶。 型別`azure vm disk attach-new`toocreate 磁碟並將新 GB 的 VM。 如果您不會明確地識別儲存體帳戶，您所建立的任何磁碟置於 hello 相同作業系統磁碟的所在位置的儲存體帳戶。 下列範例將 hello `50`GB 磁碟 toohello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>連接 toohello Linux VM toomount hello 新磁碟
> [!NOTE]
> 本主題會連接 tooa VM 使用使用者名稱和密碼。 toouse 公用和私用金鑰組 toocommunicate 與您的 VM，請參閱[如何透過在 Azure 上的 Linux SSH tooUse](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 
> 
> 

您需要 tooSSH 到您的 Azure VM toopartition，格式，然後掛接您新的磁碟，因此 Linux VM 可以使用它。 如果您不熟悉連接**ssh**，hello 命令 hello 形式`ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`，如下圖所示 hello 下列：

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

輸出

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

既然您已經連接 tooyour VM，您準備好 tooattach 磁碟。  首先尋找 hello 磁碟、 使用`dmesg | grep SCSI`（hello 方法使用的 toodiscover 新磁碟而有所不同）。 在此案例中，它看起來如下：

```bash
dmesg | grep SCSI
```

輸出

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

在本主題的 hello 情況下，hello 和`sdc`磁碟就是我們想要的其中一個 hello。 現在分割 hello 磁碟`sudo fdisk /dev/sdc`-假設磁碟已在您的案例 hello `sdc`，並將它設為主要磁碟上磁碟分割 1，並接受 hello 其他預設值。

```bash
sudo fdisk /dev/sdc
```

輸出

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

輸入建立 hello 分割`p`在 hello 提示字元：

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

和寫入檔案系統 toohello 磁碟分割使用 hello **mkfs**命令，並指定檔案系統類型與 hello 裝置名稱。 在本主題中，我們將使用先前內容中的 `ext4` 和 `/dev/sdc1`：

```bash
sudo mkfs -t ext4 /dev/sdc1
```

輸出

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

現在我們可以建立目錄 toomount hello 檔案系統使用`mkdir`:

```bash
sudo mkdir /datadrive
```

和您掛接 hello 目錄使用`mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

hello 資料磁碟現在已準備好 toouse 為`/datadrive`。

```bash
ls
```

輸出

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

重新開機，它必須加入 toohello /etc/fstab 檔案之後，會自動掛接 tooensure hello 磁碟機。 此外，我們建議，hello UUID （全域唯一識別碼） 用於 /etc/fstab toorefer toohello 磁碟機而非只是 hello 裝置名稱 (例如， `/dev/sdc1`)。 如果 hello OS 開機期間，偵測磁碟錯誤，則使用 hello UUID 可避免 hello 正在掛接的 tooa 指定的位置不正確的磁碟。 其餘的資料磁碟則會被指派這些相同的裝置識別碼。 toofind hello UUID hello 新磁碟機，請使用 hello **blkid**公用程式：

```bash
sudo -i blkid
```

hello 輸出看起來類似 toohello 下列：

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> 不當編輯 hello **/etc/hosts fstab**檔案可能會導致系統無法重新啟動。 如果不確定，請參閱 toohello 發佈文件，以取得 tooproperly 如何編輯此檔案的詳細資訊。 也建議在編輯之前建立的 hello /etc/fstab 檔案的備份。
> 
> 

接下來，開啟 hello **/etc/hosts fstab**文字編輯器中的檔案：

```bash
sudo vi /etc/fstab
```

在此範例中，我們使用 hello UUID 值 hello 新**/開發/sdc1** hello 先前步驟中，與 hello 掛接點中所建立的裝置**/datadrive**。 加入下列行 toohello 結尾 hello hello **/etc/hosts fstab**檔案：

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> 稍後移除資料磁碟，而不編輯 fstab 可能會導致 hello VM toofail tooboot。 多數散發提供任一 hello`nofail`及/或`nobootwait`fstab 選項。 這些選項可讓系統 tooboot 即使 hello 磁碟失敗 toomount 在開機時。 請查閱散發套件的文件，以取得這些參數的相關資訊。
> 
> hello **nofail**選項可確保即使 hello 檔案系統已損毀或不存在 hello 磁碟，這是在開機時，VM 啟動該 hello。 如果沒有這個選項，您可能會遇到行為中所述[無法 SSH tooLinux VM 到期 tooFSTAB 錯誤](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>Azure 中 Linux 的 TRIM/UNMAP 支援
某些 Linux 核心支援 TRIM/UNMAP 作業 toodiscard hello 磁碟上未使用的區塊。 這是主要適用於標準儲存體 tooinform 刪除頁面的 Azure 不再有效，以及可以捨棄。 如果您建立大型檔案，然後再將它們刪除，這便可節省成本。

有兩種 tooenable TRIM 支援在 Linux VM 中。 像往常一樣，參閱您的發佈 hello 建議的方法包括：

* 使用 hello`discard`掛接中的選項`/etc/fstab`，例如：

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* 在某些情況下 hello`discard`選項可能會影響效能。 或者，您可以在其中執行 hello`fstrim`命令手動從 hello 命令列，或將它加入 tooyour crontab toorun 定期：
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>疑難排解
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>後續步驟
* 請記住，新的磁碟是不使用 toohello VM 是否它會重新啟動寫入該資訊 tooyour 除非[fstab](http://en.wikipedia.org/wiki/Fstab)檔案。
* tooensure Linux VM 已正確設定，檢閱 hello[最佳化您的 Linux 電腦效能](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)建議。
* 新增其他磁碟以擴充儲存體容量，並 [設定 RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 以提升效能。

