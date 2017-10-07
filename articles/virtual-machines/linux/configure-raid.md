---
title: "aaaConfigure 軟體上執行 Linux 的虛擬機器的 RAID |Microsoft 文件"
description: "了解 toouse mdadm tooconfigure RAID 在 Azure 中 Linux 上的方式。"
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a>在 Linux 上設定軟體 RAID
常見的案例 toouse 軟體 RAID Linux 虛擬機器上處於 Azure toopresent 多個連接的資料磁碟做為單一的 RAID 裝置。 通常這可以使用的 tooimprove 效能，以及允許針對改善輸送量比較 toousing 只有單一磁碟。

## <a name="attaching-data-disks"></a>連接資料磁碟
兩個或多個空的資料磁碟都需要的 tooconfigure RAID 裝置。  hello 建立 RAID 裝置的主要原因是磁碟的 tooimprove 效能 IO。  根據您的 IO 需求，您可以選擇儲存在我們的標準儲存體，與總 too500 IO/每個磁碟或使用向上 too5000 IO/每個磁碟 ps 我們高階儲存體 ps tooattach 磁碟。 這篇文章不會深入說明如何 tooprovision 和附加資料磁碟 tooa Linux 虛擬機器。  請參閱 hello Microsoft Azure 文件[連接磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需有關如何 tooattach 空的資料磁碟在 Azure 上 tooa Linux 虛擬機器的詳細指示。

## <a name="install-hello-mdadm-utility"></a>安裝 hello mdadm 公用程式
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS & Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES 和 openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>建立 hello 磁碟分割
在本範例中，我們會在 /dev/sdc 上建立單一磁碟分割。 會呼叫 /dev/sdc1 hello 新磁碟分割。

1. 啟動`fdisk`toobegin 建立資料分割

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. 按下 'n' 個在 hello 提示 toocreate  **n**新增磁碟分割：

    ```bash
    Command (m for help): n
    ```

3. 接下來，請按 'p' toocreate **p**主要磁碟分割：

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. 按下 '1' tooselect 資料分割編號 1:

    ```bash
    Partition number (1-4): 1
    ```

5. 選取 hello 起點 hello 新磁碟分割或按`<enter>`tooaccept hello 預設 tooplace hello 資料分割的 hello hello 磁碟機上的可用空間 hello 開頭：

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. 選取 hello hello 分割區，例如型別 '+10G' toocreate 10 gb 的磁碟分割大小。 或者，按下`<enter>`建立單一磁碟分割跨越 hello 整個磁碟機的：

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. 接下來，變更 hello 識別碼和**t**hello hello 預設值的資料分割的類型識別碼 '83' (Linux) tooID 'fd' （Linux raid 自動）：

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. 最後，撰寫 hello 資料分割資料表 toohello 磁碟機，並結束 fdisk:

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>建立 hello RAID 陣列
1. 下列範例將"等量磁碟區 」 （RAID 層級 0） 三個資料分割位於三個不同的資料磁碟 （sdc1、 sdd1、 sde1） hello。  執行此命令之後，即會建立一個名為 **/dev/md127** 的新 RAID 裝置。 也請注意，是否這些資料磁碟我們先前屬於另一個無用的 RAID 陣列可能需要 tooadd hello`--force`參數 toohello`mdadm`命令：

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. 在 hello 新 RAID 裝置上建立 hello 檔案系統
   
    a. **CentOS、Oracle Linux、SLES 12、openSUSE 和 Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11** - 啟用 boot.md 並建立 mdadm.conf

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > 在 SUSE 系統上進行這些變更之後，可能需要重新開機。 針對 SLES 12，這在並 *非* 必要步驟。
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>新增 hello 新檔案系統太/等/fstab
> [!IMPORTANT]
> 不當編輯 hello /etc/fstab 檔案可能會導致系統無法重新啟動。 如果不確定，請參閱 toohello 發佈文件，以取得 tooproperly 如何編輯此檔案的詳細資訊。 也建議在編輯之前建立的 hello /etc/fstab 檔案的備份。

1. 建立新的檔案系統，所需的 hello 掛接點，例如：

    ```bash
    sudo mkdir /data
    ```
2. 當編輯 /etc/fstab，hello **UUID**應使用的 tooreference hello 檔案系統，而不是 hello 裝置名稱。  使用 hello `blkid` hello 新的檔案系統的公用程式 toodetermine hello UUID:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. 在文字編輯器中開啟 /etc/fstab 並新增 hello 新的檔案系統的項目，例如：

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    或者，在 **SLES 11** 上：

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    接著，儲存並關閉 /etc/fstab。

4. 測試該 hello /etc/fstab 輸入正確：

    ```bash  
    sudo mount -a
    ```

    如果此命令會產生錯誤訊息中，請檢查 hello /etc/fstab 檔案中的 hello 語法。
   
    接下來執行 hello`mount`命令 tooensure hello 檔案系統已裝載：

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (選擇性) 保全開機參數
   
    **fstab 組態**
   
    許多發行包含任一 hello`nobootwait`或`nofail`掛接參數可能會加入 toohello /etc/hosts fstab 檔案。 這些參數時掛接特定檔案系統允許的失敗，並允許 hello Linux 系統 toocontinue tooboot，即使它是無法 tooproperly 掛接 hello RAID 檔案系統。 如需這些參數的詳細資訊，請參閱 tooyour 發佈文件。
   
    範例 (Ubuntu)：

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Linux 開機參數**
   
    加法 toohello 上述參數，在 hello 核心參數 」`bootdegraded=true`」 可以讓 hello 系統 tooboot，即使 hello RAID 會被視為已損毀，或降級，例如，如果不小心從 hello 虛擬機器移除資料磁碟機。 依預設，這也會造成無法開機的系統。
   
    請參閱上 tooproperly 如何編輯核心參數 tooyour 發佈文件。 比方說，在 CentOS、 Oracle Linux （SLES 11） 的許多發行這些參數可能加入手動 toohello"`/boot/grub/menu.lst`"檔案。  在 Ubuntu 上這個參數可以加入 toohello`GRUB_CMDLINE_LINUX_DEFAULT`變數上"/ 等/預設/幼蟲"。


## <a name="trimunmap-support"></a>TRIM/UNMAP 支援
某些 Linux 核心支援 TRIM/UNMAP 作業 toodiscard hello 磁碟上未使用的區塊。 這些運算全都是主要適用於標準儲存體 tooinform 刪除頁面的 Azure 不再有效，以及可以捨棄。 如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。

> [!NOTE]
> 如果 hello 陣列 hello 區塊大小設定 tooless hello 預設 (512 KB) 比 RAID 可能不會發出捨棄命令。 這是因為 hello 取消對應 hello 主機上的資料粒度也是 512 KB。 如果您修改透過 mdadm 的 hello 陣列的區塊大小`--chunk=`hello 核心，則可能會忽略參數，則 TRIM/取消要求。

有兩種 tooenable TRIM 支援在 Linux VM 中。 像往常一樣，參閱您的發佈 hello 建議的方法包括：

- 使用 hello`discard`掛接中的選項`/etc/fstab`，例如：

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- 在某些情況下 hello`discard`選項可能會影響效能。 或者，您可以在其中執行 hello`fstrim`命令手動從 hello 命令列，或將它加入 tooyour crontab toorun 定期：

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
