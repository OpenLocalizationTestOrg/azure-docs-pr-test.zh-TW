---
title: "在 Azure 中的 Linux VM 的磁碟 tooa aaaAttach |Microsoft 文件"
description: "了解如何 tooattach 資料磁碟 tooa Linux VM 使用 hello 傳統部署模型，並初始化 hello 磁碟，讓它可供使用"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>如何 tooAttach 資料磁碟 tooa Linux 虛擬機器
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 請參閱如何太[將使用 hello Resource Manager 部署模型的資料磁碟連接](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

您可以附加空磁碟及包含資料 tooyour Azure Vm 的磁碟。 這兩種類型的磁碟都是位於 Azure 儲存體帳戶中的 .vhd 檔案。 新增的任何磁碟 tooa Linux 機器，附加 hello 磁碟之後，您需要 tooinitialize 和格式化它，讓它可供使用。 附加空磁碟和磁碟如何 toothen 初始化及格式化新的磁碟已經包含資料 tooyour Vm，以及此發行項詳細資料。

> [!NOTE]
> 它是最佳的作法 toouse 其中一個或多個個別磁碟 toostore 虛擬機器的資料。 當您建立 Azure 虛擬機器時，它會有作業系統磁碟和暫存磁碟。 **請勿使用 hello 暫存磁碟 toostore 永續性資料。** 正如 hello 名，它會提供暫存儲存位置。 它並不提供備援或備份，因為它不在 Azure 儲存體內。
> hello 暫存磁碟通常由 hello Azure Linux 代理程式管理，且自動掛接太**/mnt/retention/ 資源**(或**/mnt** Ubuntu 映像上)。 在 hello 另一方面，資料磁碟可能會命名為 hello Linux 核心類似`/dev/sdc`，而且您需要 toopartition，格式化及裝載此資源。 請參閱 hello [Azure Linux 代理程式使用者指南][ Agent]如需詳細資訊。
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>在 Linux 中初始化新的資料磁碟
1. SSH tooyour VM。 如需詳細資訊，請參閱[如何 tooa 執行 Linux 的虛擬機器上的 toolog][Logon]。
2. 接下來您需要 hello 資料磁碟 tooinitialize toofind hello 裝置識別碼。 有兩種方式 toodo 的：
   
    SCSI 裝置 hello 中的 Grep a) 記錄，例如 hello 下列命令：
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    針對最近 Ubuntu 分佈，您可能需要 toouse`sudo grep SCSI /var/log/syslog`因為太記錄`/var/log/messages`預設可能會停用。
   
    您可以找到 hello hello 最後一個資料磁碟的 hello 訊息中，會顯示已加入的識別項。
   
    ![收到 hello 磁碟訊息](./media/attach-disk/scsidisklog.png)
   
    或
   
    b） 使用 hello`lsscsi`命令 toofind 出 hello 裝置識別碼。`lsscsi`可以透過安裝`yum install lsscsi`（Red hat 基底散發套件） 或`apt-get install lsscsi`（Debian 依據分佈）。 您可以找到您要尋找的 hello 磁碟其*lun*或**邏輯單元編號**。 例如，hello *lun*如您所連接的 hello 磁碟可以輕鬆地看到從`azure vm disk list <virtual-machine>`為：

    ```azurecli
    azure vm disk list myVM
    ```

    hello 輸出是類似 toohello 下列：

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    比較此資料與 hello 輸出`lsscsi`hello 相同範例虛擬機器：
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    hello hello tuple 中每個資料列中的最後一個號碼為 hello *lun*。 如需詳細資訊，請參閱 `man lsscsi` 。
3. 在 hello 提示字元中輸入下列命令 toocreate hello 您的裝置：
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. 出現提示時，輸入 **n**  toocreate 分割區。

    ![建立裝置](./media/attach-disk/fdisknewpartition.png)

5. 出現提示時，輸入**p** toomake hello 分割 hello 主要磁碟分割。 型別**1** toomake 它 hello 第一個資料分割，，然後輸入 hello 磁柱輸入 tooaccept hello 預設值。 在某些系統，可先顯示 hello hello 預設值並 hello 最後的磁區，而不是 hello 磁柱。 您可以選擇 tooaccept 這些預設值。

    ![建立磁碟分割](./media/attach-disk/fdisknewpartdetails.png)


6. 型別**p** toosee hello 詳細 hello 磁碟分割。

    ![列出磁碟資訊](./media/attach-disk/fdiskpartitiondetails.png)


7. 型別**w** toowrite hello hello 磁碟設定。

    ![寫入 hello 磁碟上的變更](./media/attach-disk/fdiskwritedisk.png)

8. 現在您可以在 hello 新磁碟分割上建立 hello 檔案系統。 附加 hello 分割區編號 toohello 裝置識別碼 (在下列範例中的 hello `/dev/sdc1`)。 hello 下列範例會建立 ext4 磁碟分割上 /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![建立檔案系統](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > SuSE Linux Enterprise 11 系統針對 ext4 檔案系統只支援唯讀存取。 如需這些系統，建議 tooformat hello 新的檔案系統為 ext3，而不是 ext4。

9. 讓目錄 toomount hello 新的檔案系統，如下所示：
   
    ```bash
    sudo mkdir /datadrive
    ```

10. 最後您掛接 hello 磁碟機，如下所示：
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    hello 資料磁碟現在已準備好 toouse 為**/datadrive**。
   
    ![建立 hello 目錄及掛接 hello 磁碟](./media/attach-disk/mkdirandmount.png)

11. 加入 hello 新磁碟機太/等/fstab:
   
    重新開機，它必須加入 toohello /etc/fstab 檔案之後，會自動掛接 tooensure hello 磁碟機。 此外，強烈建議 /etc/fstab toorefer toohello 磁碟機，而不是只有 hello 裝置名稱 (也就是 /dev/sdc1) 中使用該 hello UUID （全域唯一識別碼）。 使用 hello UUID 可避免 hello 正在掛接的 tooa 如果 hello OS 開機期間偵測到磁碟錯誤，而且任何剩餘的資料磁碟，然後在其中指派那些裝置識別碼指定的位置不正確的磁碟。 toofind hello UUID hello 新磁碟機，您可以使用 hello **blkid**公用程式：
   
    ```bash
    sudo -i blkid
    ```
   
    hello 輸出看起來類似下列範例的 toohello:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > 不當編輯 hello **/etc/hosts fstab**檔案可能會導致系統無法重新啟動。 如果不確定，請參閱 toohello 發佈文件，以取得 tooproperly 如何編輯此檔案的詳細資訊。 也建議在編輯之前建立的 hello /etc/fstab 檔案的備份。

    接下來，開啟 hello **/etc/hosts fstab**文字編輯器中的檔案：

    ```bash
    sudo vi /etc/fstab
    ```

    在此範例中，我們使用 hello UUID 值 hello 新**/開發/sdc1** hello 先前步驟中，與 hello 掛接點中所建立的裝置**/datadrive**。 加入下列行 toohello 結尾 hello hello **/etc/hosts fstab**檔案：

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    或者，在 SuSE Linux 為基礎的系統上，您可能需要 toouse 稍有不同的格式：

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > hello`nofail`選項可確保即使 hello 檔案系統已損毀或不存在 hello 磁碟，這是在開機時，VM 啟動該 hello。 如果沒有這個選項，您可能會遇到行為中所述[無法 SSH tooLinux VM 到期 tooFSTAB 錯誤](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)。

    您現在可以測試 hello 檔案系統已裝載卸載，並再重新掛載 hello 檔案系統，也就利用正常 hello 範例掛接點`/datadrive`建立 hello 中稍早步驟：

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    如果 hello`mount`命令會產生錯誤，請檢查檔 hello /etc/hosts fstab 正確語法。 如果還有建立其他資料磁碟機或磁碟分割，也請分別在 /etc/fstab 中分別輸入它們。

    請使用這個命令可寫入 hello 磁碟機：

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > 接著移除資料磁碟，而不編輯 fstab 可能會導致 hello VM toofail tooboot。 如果這是常見的發生次數，多數散發提供任一 hello`nofail`及/或`nobootwait`fstab 選項，可讓系統 tooboot，即使 hello 磁碟失敗 toomount 在開機時。 請查閱散發套件的文件，以取得這些參數的相關資訊。

### <a name="trimunmap-support-for-linux-in-azure"></a>Azure 中 Linux 的 TRIM/UNMAP 支援
某些 Linux 核心支援 TRIM/UNMAP 作業 toodiscard hello 磁碟上未使用的區塊。 這些運算全都是主要適用於標準儲存體 tooinform 刪除頁面的 Azure 不再有效，以及可以捨棄。 如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。

有兩種 tooenable TRIM 支援在 Linux VM 中。 像往常一樣，參閱您的發佈 hello 建議的方法包括：

* 使用 hello`discard`掛接中的選項`/etc/fstab`，例如：

    ```sh
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
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>後續步驟
閱讀更多關於使用 Linux VM hello 下列文章中：

* [如何 toolog tooa 執行 Linux 的虛擬機器上][Logon]
* [如何 toodetach 來自 Linux 虛擬機器的磁碟](detach-disk.md)
* [使用 Azure CLI hello 與 hello 傳統部署模型](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [在 Azure 中的 Linux VM 上設定 RAID](../configure-raid.md)
* [設定 Azure 中 Linux VM 的 LVM](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
