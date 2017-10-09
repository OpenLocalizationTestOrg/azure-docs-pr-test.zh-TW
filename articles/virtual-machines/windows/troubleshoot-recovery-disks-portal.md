---
title: "Windows hello Azure 入口網站的疑難排解 VM 的 aaaUse |Microsoft 文件"
description: "了解如何 tootroubleshoot Windows 虛擬機器問題在 Azure 中的連接 hello OS 磁碟 tooa 復原 VM 使用 hello Azure 入口網站"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>疑難排解 Windows VM，藉由附加 hello OS 磁碟 tooa 復原 VM 使用 hello Azure 入口網站
如果 Windows 虛擬機器 (VM) 在 Azure 中會發生開機或磁碟錯誤，您可能需要 tooperform 疑難排解 hello 虛擬硬碟上本身的步驟。 常見範例是防止 hello VM 可以 tooboot 成功失敗的應用程式更新。 本文詳細說明如何 toouse hello Azure 入口網站 tooconnect 虛擬硬碟磁碟 tooanother Windows VM toofix 任何錯誤，然後重新建立原始 VM。

## <a name="recovery-process-overview"></a>復原程序概觀
hello 疑難排解程序如下所示：

1. 刪除 hello VM 遇到問題，保留 hello 虛擬硬碟。
2. 附加和掛接 hello Windows VM 的虛擬硬碟 tooanother 供疑難排解之用。
3. 連接 toohello 疑難排解 VM。 編輯檔案，或在 hello 原始虛擬硬碟上執行任何工具 toofix 問題。
4. 取消掛接並卸離 hello 虛擬硬碟從 hello 疑難排解 VM。
5. 使用建立 VM hello 原始虛擬硬碟。


## <a name="determine-boot-issues"></a>判斷開機問題
為什麼您的 VM 不能 tooboot 正確，toodetermine 檢查 hello 開機診斷 VM 螢幕擷取畫面。 常見的例子是應用程式更新無效，或因為刪除或移動基礎虛擬硬碟。

在 hello 入口網站中選取您的 VM，然後捲動 toohello**支援 + 疑難排解**> 一節。 按一下**開機診斷**tooview hello 螢幕擷取畫面。 請注意，任何特定的錯誤訊息或錯誤碼 toohelp 判斷 hello VM 為何發生問題。 hello 下列範例示範正在等候停止服務的 VM:

![檢視 VM 開機診斷主控台記錄](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

您也可以按一下**螢幕擷取畫面**toodownload hello VM 螢幕擷取畫面的擷取。


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

1. 開啟 遠端桌面連線 tooyour VM。 Hello 入口網站中選取您的 VM，然後按一下**連接**。 下載並開啟 hello RDP 連接檔案。 輸入認證 toolog tooyour VM 中如下所示：

    ![登入 tooyour VM 使用遠端桌面](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. 開啟 [伺服器管理員]，然後選取 [檔案和存放服務]。 

    ![選取伺服器管理員內的檔案和存放服務](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. 自動偵測並附加 hello 資料磁碟。 toosee hello 一份連接磁碟上，選取**磁碟**。 您可以選取您的資料磁碟 tooview 磁碟區的資訊，包括 hello 磁碟機代號。 下列範例顯示 hello 連接資料磁碟和使用 hello **f:**:

    ![伺服器管理員中的已連接磁碟和磁碟區資訊](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a>修正原始虛擬硬碟的問題
與 hello 現有虛擬硬碟掛接，您現在可以執行任何維護和疑難排解步驟，視需要。 一旦解決 hello 問題之後，繼續進行步驟 hello。


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>卸載並中斷連結原始虛擬硬碟
一旦解決的錯誤，卸離 hello 現有虛擬硬碟從您疑難排解的 VM。 您無法使用虛擬硬碟與任何其他 VM，直到釋放附加 hello 疑難排解 VM 的虛擬硬碟 toohello hello 租用。

1. Hello RDP 工作階段 tooyour VM，從開啟**伺服器管理員**，然後選取**檔案和存放服務**:

    ![在伺服器管理員中選取檔案和存放服務](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. 依序選取 [磁碟] 及您的資料磁碟。 在資料磁碟上按一下滑鼠右鍵，然後選取 [離線]：

    ![設定為離線的伺服器管理員 中的 hello 資料磁碟](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. 現在您可以卸離 hello 虛擬硬碟從 hello VM。 Hello Azure 入口網站中選取您的 VM，然後按一下**磁碟**。 選取您現有的虛擬硬碟，然後按一下中斷連結：

    ![將現有虛擬硬碟中斷連結](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    請等到 hello VM 已成功中斷 hello 資料磁碟連結才能繼續。

## <a name="create-vm-from-original-hard-disk"></a>從原始硬碟建立 VM
toocreate 原始虛擬硬碟，從 VM 使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)。 hello 範本會將 VM 部署到現有的虛擬網路，使用從 hello hello VHD URL 稍早的命令。 按一下 hello**部署 tooAzure**按鈕，如下所示：

![從 Github 的範本部署 VM](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

hello 範本會載入至 hello 部署的 Azure 入口網站。 輸入您新的 VM 和現有的 Azure 資源的 hello 名稱，然後貼上 hello URL tooyour 現有虛擬硬碟。 toobegin hello 部署中，按一下 **購買**:

![從範本部署 VM](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>重新啟用開機診斷
當您從 hello 現有虛擬硬碟建立 VM 時，開機診斷可能不會自動啟用。 toocheck hello 的開機診斷狀態，然後開啟有需要在 hello 入口網站中選取您的 VM。 在 [監視] 底下，按一下 [診斷設定]。 確定 hello 狀態**上**，太接下來 hello 核取記號和**開機診斷**已選取。 如果有進行任何變更，請按一下 [儲存]：

![更新開機診斷設定](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>後續步驟
如果您有連接 tooyour VM 的問題，請參閱[疑難排解 RDP 連線 tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Windows VM 上的應用程式連線問題進行疑難排解](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

如需使用 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。