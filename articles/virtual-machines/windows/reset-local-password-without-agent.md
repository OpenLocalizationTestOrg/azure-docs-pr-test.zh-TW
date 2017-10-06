---
title: "沒有 Azure 代理程式的本機 Windows 密碼 aaaReset |Microsoft 文件"
description: "如何 tooreset hello 與本機 Windows 使用者帳戶的密碼時 hello Azure 客體代理程式未安裝或在 VM 上正常運作"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>如何 tooreset 本機 Windows 密碼做為 Azure VM
您可以使用 hello 在 Azure 中 VM 的 hello 本機 Windows 密碼重設[Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)提供 hello Azure 客體代理程式安裝。 這個方法是 hello 主要方式 tooreset Azure VM 的密碼。 如果您使用 hello Azure 客體代理程式沒有回應，或上傳自訂映像之後失敗 tooinstall 遇到問題，您可以手動重設 Windows 密碼。 這篇文章說明如何藉由附加的本機帳戶密碼 tooreset hello 來源 OS 虛擬磁碟 tooanother VM。 

> [!WARNING]
> 只能使用此程序做為最後手段。 永遠嘗試使用 hello 密碼 tooreset [Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)第一次。
> 
> 

## <a name="overview-of-hello-process"></a>Hello 程序概觀
執行本機密碼，沒有存取 toohello Azure 客體代理程式時，針對 Windows VM 在 Azure 中重設 hello 核心步驟如下所示：

* 刪除 hello 來源 VM。 hello 虛擬磁碟會保留。
* 附加 hello 來源 VM 之 OS 磁碟 tooanother VM 上 hello Azure 訂用帳戶內的相同位置。 此 VM 是參照的 tooas hello 疑難排解 VM。
* 使用 hello 疑難排解 VM 建立 hello 來源 VM 之 OS 磁碟上的某些組態檔。
* 卸離 hello 疑難排解 VM 中的 hello VM 之 OS 磁碟。
* 使用資源管理員範本 toocreate 使用 hello 原始虛擬磁碟的 VM。
* 當 hello 新 VM 馮鰹氶 a hello 設定檔會建立所需的 hello 使用者更新 hello 密碼。

## <a name="detailed-steps"></a>詳細步驟
永遠嘗試使用 hello 密碼 tooreset [Azure 入口網站或 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)之前嘗試 hello 下列步驟。 在開始之前，確定您有 VM 的備份。 

1. 刪除 hello 影響 VM 在 Azure 入口網站中。 正在刪除 hello VM 只會刪除 hello hello VM 在 Azure 中的 hello 參考中繼資料。 hello VM 刪除時，會保留 hello 虛擬磁碟：
   
   * 選取 hello VM hello Azure 入口網站中的按一下*刪除*:
     
     ![刪除現有的 VM](./media/reset-local-password-without-agent/delete_vm.png)
2. 附加 hello 來源 VM 之 OS 磁碟 toohello 疑難排解 VM。 hello 疑難排解 VM 必須在 hello 與 hello 來源 VM 之 OS 磁碟相同的區域 (例如`West US`):
   
   * 選取 VM 疑難排解 hello Azure 入口網站中的 hello。 按一下 [磁碟] | [連接現有項目]：
     
     ![連接現有磁碟](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     選取*VHD 檔案*，然後選取包含您的來源 VM 的 hello 儲存體帳戶：
     
     ![選取儲存體帳戶](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     選取 hello 來源容器。 hello 來源容器是通常*vhd*:
     
     ![選取儲存體容器](./media/reset-local-password-without-agent/disks_select_container.png)
     
     選取 hello OS vhd tooattach。 按一下*選取*toocomplete hello 程序：
     
     ![選取來源虛擬磁碟](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. 連接 toohello 疑難排解使用遠端桌面的 VM，並確認看見 hello 來源 VM 之 OS 磁碟：
   
   * 選取 hello 疑難排解 hello Azure 入口網站中的 VM，然後按一下*連接*。
   * 開啟下載的 hello RDP 檔案。 輸入 hello 使用者名稱和密碼的 hello 疑難排解 VM。
   * 在檔案總管 中，尋找您所連接的 hello 資料磁碟。 如果 hello 來源 VM 的 VHD 是 hello 唯一的資料磁碟附加 toohello 疑難排解 VM，它應該 hello f： 磁碟機：
     
     ![檢視連接的資料磁碟](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. 建立`gpt.ini`中`\Windows\System32\GroupPolicy`hello 來源 VM 的磁碟機上 （如果存在 gpt.ini，重新命名 toogpt.ini.bak）：
   
   > [!WARNING]
   > 請確定，不會無意建立下列檔案中 C:\Windows hello、 hello hello 疑難排解 VM 的作業系統磁碟機。 建立 hello 下列來源當做資料磁碟所連接的 VM 的 hello 作業系統磁碟機中的檔案。
   > 
   > 
   
   * 新增下列幾行到 hello hello`gpt.ini`您建立的檔案：
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![建立 gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. 在 `\Windows\System32\GroupPolicy\Machine\Scripts` 中建立 `scripts.ini`。 確定已顯示隱藏的資料夾。 如有需要建立 hello`Machine`或`Scripts`資料夾。
   
   * 新增下列幾行 hello hello`scripts.ini`您建立的檔案：
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![建立 scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. 建立`FixAzureVM.cmd`中`\Windows\System32`以下列內容，取代 hello`<username>`和`<newpassword>`以您自己的值：
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![建立 FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    定義 hello 新密碼時，必須符合您的 vm 設定 hello 密碼複雜性需求。
7. 在 Azure 入口網站中卸離 hello hello 疑難排解 VM 磁碟：
   
   * 選取 VM 疑難排解 hello Azure 入口網站中的 hello*磁碟*。
   * 選取 hello 資料磁碟附加在步驟 2 中，按一下*卸離*:
     
     ![卸離磁碟](./media/reset-local-password-without-agent/detach_disk.png)
8. 建立 VM 之前，取得 hello URI tooyour 來源作業系統磁碟：
   
   * 選取 hello hello Azure 入口網站中的儲存體帳戶，請按一下*Blob*。
   * 選取 hello 容器。 hello 來源容器是通常*vhd*:
     
     ![選取儲存體帳戶 Blob](./media/reset-local-password-without-agent/select_storage_details.png)
     
     選取您 VM OS VHD 的來源，然後按一下 hello*複製*按鈕的下一個 toohello *URL*名稱：
     
     ![複製磁碟 URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. 從 hello 來源 VM 之 OS 磁碟中建立 VM:
   
   * 使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)toocreate 將 VM 從特定的 VHD。 按一下 hello`Deploy tooAzure`按鈕 tooopen hello 與 hello 樣板化詳細資料，擴展您的 Azure 入口網站。
   * 如果您想 tooretain hello VM 的 hello 先前設定時，選取*編輯範本*tooprovide 現有 VNet、 子網路、 網路介面卡或公用 IP。
   * 在 hello`OSDISKVHDURI`參數文字方塊中，貼上您的來源 VHD URI 取得 hello 前面步驟中的 hello:
     
     ![從範本建立 VM](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. 新的 VM 正在執行中的 hello 之後, 連接 toohello hello hello 中所指定的新密碼與使用遠端桌面的 VM`FixAzureVM.cmd`指令碼。
11. 從遠端工作階段 toohello 新的 VM，移除 hello 下列檔案 tooclean hello 環境：
    
    * 從 %windir%\System32
      * 移除 FixAzureVM.cmd
    * 從 %windir%\System32\GroupPolicy\Machine\
      * 移除 scripts.ini
    * 從 %windir%\System32\GroupPolicy
      * 移除 gpt.ini （如果 gpt.ini 存在之前，但您重新命名了 toogpt.ini.bak，重新命名 hello.bak 檔案後 toogpt.ini）

## <a name="next-steps"></a>後續步驟
如果您仍然無法連線使用遠端桌面，請參閱 hello [RDP 疑難排解指南](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 hello[詳細的疑難排解指南 RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)查看疑難排解方法，而不是特定的步驟。 您也可以[開啟 Azure 支援要求](https://azure.microsoft.com/support/options/)，以取得實際操作協助。

