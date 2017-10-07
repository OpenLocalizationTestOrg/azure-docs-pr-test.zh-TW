---
title: "Linux VM 疑難排解 hello Azure 入口網站中的 aaaUse |Microsoft 文件"
description: "了解如何連接 hello OS 磁碟 tooa 復原 VM 使用 tootroubleshoot Linux 虛擬機器問題 hello Azure 入口網站"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>疑難排解 Linux VM，藉由附加 hello OS 磁碟 tooa 復原 VM 使用 hello Azure 入口網站
如果您的 Linux 虛擬機器 (VM) 會發生開機或磁碟錯誤，您可能需要 tooperform 疑難排解 hello 虛擬硬碟上本身的步驟。 常見範例是無效的項目中`/etc/fstab`，防止 hello VM 可以 tooboot 成功。 本文詳細說明如何 toouse hello Azure 入口網站 tooconnect 虛擬硬碟磁碟 tooanother Linux VM toofix 任何錯誤，然後重新建立原始 VM。

## <a name="recovery-process-overview"></a>復原程序概觀
hello 疑難排解程序如下所示：

1. 刪除 hello VM 遇到問題，保留 hello 虛擬硬碟。
2. 附加和掛接 hello Linux VM 的虛擬硬碟 tooanother 供疑難排解之用。
3. 連接 toohello 疑難排解 VM。 編輯檔案，或在 hello 原始虛擬硬碟上執行任何工具 toofix 問題。
4. 取消掛接並卸離 hello 虛擬硬碟從 hello 疑難排解 VM。
5. 使用建立 VM hello 原始虛擬硬碟。


## <a name="determine-boot-issues"></a>判斷開機問題
檢查 hello 開機診斷和 VM 螢幕擷取畫面 toodetermine 為什麼您的 VM 不能 tooboot 正確。 常見的例子是 `/etc/fstab` 中的項目無效，或因為刪除或移動基礎虛擬硬碟。

在 hello 入口網站中選取您的 VM，然後捲動 toohello**支援 + 疑難排解**> 一節。 按一下**開機診斷**tooview hello 主控台訊息資料流處理，從您的 VM。 如果您可以判斷為什麼 hello VM 發生問題，檢閱 hello 主控台記錄 toosee。 hello 下列範例顯示處於維護模式且需要手動互動卡的 VM:

![檢視 VM 開機診斷主控台記錄](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

您也可以按一下**螢幕擷取畫面**hello 頂端的 hello 開機診斷記錄 toodownload hello VM 螢幕擷取畫面的擷取。


## <a name="view-existing-virtual-hard-disk-details"></a>檢視現有的虛擬硬碟詳細資料
您可以將附加您的虛擬硬碟 tooanother VM 之前，您會需要 tooidentify hello hello 虛擬硬碟 (VHD) 名稱。 

從 hello 入口網站中，選取您的資源群組，然後選取您的儲存體帳戶。 按一下**Blob**，如下列範例中的 hello:

![選取儲存體 Blob](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

一般來說，您會有一個名為 **vhds** 的容器，以儲存虛擬硬碟。 選取 hello 容器 tooview 虛擬硬碟的清單。 請注意您的 VHD hello 名稱 （hello 前置詞通常是您 VM hello 名稱）：

![識別儲存體容器中的 VHD](./media/troubleshoot-recovery-disks-portal/storage-container.png)

從 hello 清單中選取現有虛擬硬碟，並複製 hello 步驟中使用的 hello URL:

![複製現有的虛擬硬碟 URL](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>刪除現有的 VM
虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。 虛擬硬碟是存放 hello 作業系統本身、 應用程式和組態的位置。 hello VM 本身是定義 hello 大小或位置，並參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC) 的只是中繼資料。 每個虛擬硬碟已連接時，指派租用 tooa VM。 雖然可以附加和卸離 hello VM 正在執行時，即使資料磁碟，除非刪除 hello VM 資源無法中斷 hello 作業系統磁碟。 hello 租用會繼續 tooassociate hello OS 磁碟 vm，即使該 VM 是處於已停止和取消配置狀態。

hello 第一個步驟 toorecover VM 是 toodelete hello VM 資源本身。 刪除 hello VM 離開您的儲存體帳戶中的 hello 虛擬硬碟。 刪除 VM hello 之後, 您附加 hello 虛擬硬碟 tooanother VM tootroubleshoot，並解決 hello 錯誤。

選取您的 VM 在 hello 入口網站，然後按一下 **刪除**:

![顯示開機錯誤的 VM 開機診斷螢幕擷取畫面](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

請等到完成刪除附加 hello 虛擬硬碟 tooanother VM 之前 hello VM。 hello 租用 hello 虛擬硬碟關聯 hello VM 需要 toobe 附加 hello 虛擬硬碟 tooanother VM 之前釋出。


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>附加現有的虛擬硬碟 tooanother VM
如 hello 接下來的幾個步驟，您可以使用另一個 VM 供疑難排解之用。 附加 hello 疑難排解 VM toobe 無法 toobrowse 現有虛擬硬碟 toothis 並編輯 hello 磁碟的內容。 此程序可讓您 toocorrect 任何組態錯誤或檢閱其他應用程式或系統記錄檔，例如。 選擇或建立另一個 VM toouse 供疑難排解之用。

1. 從 hello 入口網站中，選取您的資源群組，然後選取您疑難排解的 VM。 選取 磁碟，然後按一下連結現有項目：

    ![將 hello 入口網站中的現有磁碟](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect 現有虛擬硬碟，按一下  **VHD 檔案**:

    ![瀏覽現有 VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. 選取儲存體帳戶和容器，然後按一下您現有的 VHD。 按一下 hello**選取**按鈕 tooconfirm 您選擇：

    ![選取現有 VHD](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. 您現在已選取的 VHD，然後按一下**確定**tooattach hello 現有虛擬硬碟：

    ![確認連結現有虛擬硬碟](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. 幾秒之後，hello**磁碟**vm 的窗格會列出您現有虛擬硬碟連接當做資料磁碟：

    ![現有虛擬硬碟已連結為資料磁碟](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>掛接 hello 連接的資料磁碟

> [!NOTE]
> hello 下列範例詳細說明 hello Ubuntu 虛擬機器上所需的步驟。 如果您使用不同的 Linux distro，例如 Red Hat Enterprise Linux 或 SUSE，hello 記錄檔位置和`mount`命令可能會稍有不同。 如需您特定 distro hello 命令中的適當變更，請參閱 toohello 文件。

1. SSH tooyour 疑難排解 VM 使用 hello 適當的認證。 如果這個磁碟是 hello 第一個資料磁碟附加 tooyour 疑難排解 VM，它可能連線太`/dev/sdc`。 使用`dmseg`toolist 連接的磁碟：

    ```bash
    dmesg | grep SCSI
    ```
    hello 輸出是 toohello 類似下列範例程式碼：

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    在上述範例中的 hello，hello OS 磁碟位於`/dev/sda`和 hello 暫存磁碟提供給每個 VM 位於`/dev/sdb`。 如果您有多個資料磁碟，它們應該是位於 `/dev/sdd`、`/dev/sde`，依此類推。

2. 建立目錄 toomount 您現有的虛擬硬碟。 hello 下列範例會建立一個名為目錄`troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. 如果您在現有的虛擬硬碟上有多個資料分割，裝載所需的 hello 磁碟分割。 hello 下列範例會 hello 第一個主要磁碟分割在`/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > 最佳作法是 toomount 資料磁碟上的 Vm 在 Azure 中使用 hello hello 虛擬硬碟的通用唯一識別碼 (UUID)。 針對這個簡短的疑難排解案例，不需要掛接 hello 虛擬硬碟使用 hello UUID。 但是，在正常使用，編輯`/etc/fstab`toomount 虛擬硬碟使用的裝置名稱，而非可能會造成 UUID hello VM toofail tooboot。


## <a name="fix-issues-on-original-virtual-hard-disk"></a>修正原始虛擬硬碟的問題
與 hello 現有虛擬硬碟掛接，您現在可以執行任何維護和疑難排解步驟，視需要。 一旦解決 hello 問題之後，繼續進行步驟 hello。

## <a name="unmount-and-detach-original-virtual-hard-disk"></a>卸載並中斷連結原始虛擬硬碟
一旦解決的錯誤，卸離 hello 現有虛擬硬碟從您疑難排解的 VM。 您無法使用虛擬硬碟與任何其他 VM，直到釋放附加 hello 疑難排解 VM 的虛擬硬碟 toohello hello 租用。

1. 從 hello SSH 工作階段 tooyour 疑難排解 VM，卸載 hello 現有虛擬硬碟。 第一次變更超出您掛接點的 hello 父目錄：

    ```bash
    cd /
    ```

    現在取消掛接 hello 現有虛擬硬碟。 hello 下例取消掛接在 hello 裝置`/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. 現在您可以卸離 hello 虛擬硬碟從 hello VM。 Hello 入口網站中選取您的 VM，然後按一下**磁碟**。 選取您現有的虛擬硬碟，然後按一下中斷連結：

    ![將現有虛擬硬碟中斷連結](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    請等到 hello VM 已成功中斷 hello 資料磁碟連結才能繼續。

## <a name="create-vm-from-original-hard-disk"></a>從原始硬碟建立 VM
toocreate 原始虛擬硬碟，從 VM 使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)。 hello 範本會將 VM 部署到現有的虛擬網路，使用從 hello hello VHD URL 稍早的命令。 按一下 hello**部署 tooAzure**按鈕，如下所示：

![從來自 GitHub 的範本部署 VM](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

hello 範本會載入至 hello 部署的 Azure 入口網站。 輸入您新的 VM 和現有的 Azure 資源的 hello 名稱，然後貼上 hello URL tooyour 現有虛擬硬碟。 toobegin hello 部署中，按一下 **購買**:

![從範本部署 VM](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>重新啟用開機診斷
當您從 hello 現有虛擬硬碟建立 VM 時，開機診斷可能不會自動啟用。 toocheck hello 的開機診斷狀態，然後開啟有需要在 hello 入口網站中選取您的 VM。 在 [監視] 底下，按一下 [診斷設定]。 確定 hello 狀態**上**，太接下來 hello 核取記號和**開機診斷**已選取。 如果有進行任何變更，請按一下 [儲存]：

![更新開機診斷設定](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>後續步驟
如果您有連接 tooyour VM 的問題，請參閱[疑難排解 SSH 連線 tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Linux VM 上的應用程式連線問題進行疑難排解](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

如需使用 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
