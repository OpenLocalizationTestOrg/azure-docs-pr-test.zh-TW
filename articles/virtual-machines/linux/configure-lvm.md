---
title: "在執行 Linux 的虛擬機器上的 aaaConfigure LVM |Microsoft 文件"
description: "深入了解如何在 Azure 中 Linux 上 LVM tooconfigure。"
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>設定 Azure 中 Linux VM 的 LVM
本文將討論如何在 Azure 虛擬機器 tooconfigure 邏輯磁碟區管理員 (LVM)。 雖然可行 tooconfigure LVM 的任何磁碟附加 toohello 虛擬機器，預設不會有映像的大部分雲端 LVM 上設定 hello 作業系統磁碟。 這是重複的磁碟區群組的 tooprevent 問題如果 hello 作業系統磁碟時附加 tooanother hello 的 VM 相同的分佈和類型，也就是在復原案例。 因此，建議您使用只 toouse LVM hello 資料磁碟上。

## <a name="linear-vs-striped-logical-volumes"></a>線性與等量邏輯磁碟區
LVM 可以是使用的 toocombine 到單一存放磁碟區的實體磁碟的數量。 根據預設 LVM 通常會建立線性的邏輯磁碟區，這表示 hello 實體儲存體串連在一起。 在此情況下讀取/寫入作業通常只會傳送 tooa 單一磁碟。 相反地，我們也可以建立等量邏輯磁碟區讀取和寫入是分散式的 toomultiple hello 磁碟區群組 (也就是類似 tooRAID0) 中所包含的磁碟。 基於效能的考量，很可能您會想 toostripe 邏輯磁碟區，以便讀取和寫入利用所有連接的資料磁碟。

本文件將說明如何 toocombine 數個資料磁碟到單一磁碟區群組中，然後再建立等量邏輯磁碟區。 有些一般化的 toowork 大部分分佈，則 hello 步驟。 在大部分情況下 hello 公用程式和管理 LVM 在 Azure 上的工作流程不是本質上不同於其他環境。 像往常一樣，也請向您的 Linux 廠商洽詢搭配特定散發套件使用 LVM 的文件和最佳做法。

## <a name="attaching-data-disks"></a>連接資料磁碟
其中一個通常會想 toostart 有兩個或多個空的資料磁碟時使用 LVM。 根據您的 IO 需求，您可以選擇儲存在我們的標準儲存體，與總 too500 IO/每個磁碟或使用向上 too5000 IO/每個磁碟 ps 我們高階儲存體 ps tooattach 磁碟。 本文會深入說明如何 tooprovision 和附加資料磁碟 tooa Linux 虛擬機器。 請參閱 hello Microsoft Azure 文件[連接磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需有關如何 tooattach 空的資料磁碟在 Azure 上 tooa Linux 虛擬機器的詳細指示。

## <a name="install-hello-lvm-utilities"></a>安裝 hello LVM 公用程式
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL、CentOS 和 Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 和 openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    SLES11 上則必須同時編輯`/etc/sysconfig/lvm`並設定`LVM_ACTIVATED_ON_DISCOVERED`太 「 啟用 」:

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>設定 LVM
本指南中，我們將假設您已經附加三個資料磁碟，我們將參照 tooas `/dev/sdc`，`/dev/sdd`和`/dev/sde`。 請注意，這些可能不一定 hello 在 VM 中的相同路徑名稱。 您可以執行 '`sudo fdisk -l`' 或類似的命令 toolist 可用的磁碟。

1. 準備 hello 實體磁碟區：

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. 建立磁碟區群組。 在此範例中，我們正在撥打 hello 磁碟區群組`data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. 建立 hello 邏輯磁碟區。 hello 命令以下我們會建立單一的邏輯磁碟區，以呼叫`data-lv01`toospan hello 整個磁碟區群組，但請注意，它也是可行的 toocreate hello 磁碟區群組中的多個邏輯磁碟區。

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Hello 邏輯磁碟區格式化

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > SLES11 請使用 `-t ext3` 而不是 ext4。 SLES11 僅支援唯讀存取 tooext4 檔案系統。

## <a name="add-hello-new-file-system-tooetcfstab"></a>新增 hello 新檔案系統太/等/fstab
> [!IMPORTANT]
> 不當編輯 hello`/etc/fstab`檔案可能會導致系統無法重新啟動。 如果不確定，請參閱 toohello 發佈文件 tooproperly 如何編輯此檔案的詳細資訊。 它也是建議的 hello 備份`/etc/fstab`編輯之前建立檔案。

1. 建立新的檔案系統，所需的 hello 掛接點，例如：

    ```bash  
    sudo mkdir /data
    ```

2. 找出 hello 邏輯磁碟區路徑

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. 開啟`/etc/fstab`文字編輯器中，為新增項目 hello 新的檔案系統，例如：

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    然後，儲存並關閉 `/etc/fstab`。

4. 測試該 hello`/etc/fstab`輸入是否正確：

    ```bash    
    sudo mount -a
    ```

    如果此命令會產生錯誤訊息請檢查在 hello hello 語法`/etc/fstab`檔案。
   
    接下來執行 hello`mount`命令 tooensure hello 檔案系統已裝載：

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (選擇性) 保全 `/etc/fstab`中的開機參數
   
    許多發行包含任一 hello`nobootwait`或`nofail`掛接參數可能會加入 toohello`/etc/fstab`檔案。 這些參數時掛接特定檔案系統允許的失敗，並允許 hello Linux 系統 toocontinue tooboot，即使它是無法 tooproperly 掛接 hello RAID 檔案系統。 請如需這些參數的詳細資訊，參閱 tooyour 發佈文件。
   
    範例 (Ubuntu)：

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>TRIM/UNMAP 支援
某些 Linux 核心支援 TRIM/UNMAP 作業 toodiscard hello 磁碟上未使用的區塊。 這些運算全都是主要適用於標準儲存體 tooinform 刪除頁面的 Azure 不再有效，以及可以捨棄。 如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。

有兩種 tooenable TRIM 支援在 Linux VM 中。 像往常一樣，參閱您的發佈 hello 建議的方法包括：

- 使用 hello`discard`掛接中的選項`/etc/fstab`，例如：

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- 在某些情況下 hello`discard`選項可能會影響效能。 或者，您可以在其中執行 hello`fstrim`命令手動從 hello 命令列，或將它加入 tooyour crontab toorun 定期：

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
