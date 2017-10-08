---
title: "Azure 備份︰從 Azure VM 備份復原檔案和資料夾 | Microsoft Docs"
description: "從 Azure 虛擬機器的復原點復原檔案"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "項目層級復原；從 Azure VM 備份檔案復原；從 Azure VM 中還原檔案"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>從 Azure 虛擬機器備份復原檔案

Azure 備份提供 hello 功能 toorestore [Azure Vm 和磁碟](./backup-azure-arm-restore-vms.md)從 Azure VM 的備份。 現在本文說明如何從 Azure VM 備份復原檔案和資料夾等項目。

> [!Note]
> 這項功能適用於 Azure Vm 部署使用 hello 資源管理員模型和受保護的 tooa 復原服務保存庫。
> 不支援從加密 VM 備份的檔案復原。
>

## <a name="mount-hello-volume-and-copy-files"></a>掛接 hello 磁碟區和複製檔案

1. 登入 hello [Azure 入口網站](http://portal.Azure.com)。 尋找 hello 相關復原服務保存庫以及所需的 hello 備份項目。

2. 在 hello 備份項目刀鋒視窗中，按一下 **檔案復原**

    ![開啟復原服務保存庫備份項目](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    hello**檔案復原**刀鋒視窗隨即開啟。

    ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. 從 hello**選取復原點**想下拉式功能表、 選取 hello 包含 hello 檔案的復原點。 根據預設，已選取 hello 最新的復原點。

4. 按一下**下載可執行檔**（適用於 Windows Azure VM) 或**下載指令碼**（適用於 Linux 的 Azure VM) toodownload hello 軟體，您將使用 toocopy 檔案從 hello 復原點。

  hello/指令碼可執行檔之間建立連接 hello 本機電腦，並指定 hello 復原點。

5. 您需要密碼 toorun hello 下載指令碼/可執行檔。 您可以從使用 hello 複製 按鈕旁邊 hello 產生密碼的 hello 入口網站複製 hello 密碼

    ![產生的密碼](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Hello 在電腦上您要 toorecover hello 檔案，執行 hello 可執行檔指令碼。 您必須以系統管理員認證來執行它。 如果您具有限制存取的電腦上執行 hello 指令碼，請確定沒有存取權：

    - download.microsoft.com
    - 用於 Azure VM 備份的 Azure 端點
    - 輸出連接埠 3260

   適用於 Linux，hello 指令碼需要 ' 開啟 iscsi' 和 'lshw' 元件 tooconnect toohello 復原點。 如果那些 hello 執行所在的電腦上不存在，它會要求權限 tooinstall hello 相關元件，並將它們安裝在同意時。
   
   輸入從 hello 入口網站，當系統提示您複製的 hello 密碼。 一旦 hello 有效的密碼輸入 hello 指令碼會連接 toohello 復原點。
      
    ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   您可以在任何具有 hello 相同 （或相容） 的作業系統，因為 hello 備份 VM 的電腦上執行 hello 指令碼。 請參閱 hello[相容 OS 資料表](backup-azure-restore-files-from-vm.md#compatible-os)相容的作業系統。 如果 hello 保護 Azure 虛擬機器會使用 Windows 儲存空間 （適用於 Windows Azure Vm) 或 LVM/RAID Arrays(for Linux VMs)，則您無法在執行 hello 可執行檔指令碼 hello 相同的虛擬機器。 相反地，在任何其他具有相容作業系統上的電腦執行它。

### <a name="compatible-os"></a>相容的作業系統

#### <a name="for-windows"></a>若為 Windows

下列表格顯示 hello 相容性伺服器和電腦的作業系統之間的 hello。 當復原檔案時，您無法還原不相容作業系統之間的檔案。

|伺服器作業系統 | 相容的用戶端作業系統  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>若為 Linux

在 Linux hello 基本的需求是 hello 機器 hello 指令碼在何處執行該 hello OS 應該支援 hello filesystem hello 的檔案存在於 hello 備份 Linux VM。 當選取的機器 toorun hello 指令碼時，請確定它有 hello 相容的作業系統與 hello 版本 hello 表中所述。

|Linux 作業系統 | 版本  |
| --------------- | ---- |
| Ubuntu | 12.04 和更新版本 |
| CentOS | 6.5 和更新版本  |
| RHEL | 6.7 和更新版本 |
| Debian | 7 和更新版本 |
| Oracle Linux | 6.4 和更新版本 |

hello 指令碼也需要 python 和撞元件 tooexecute 並安全地連線 toohello 復原點。

|元件 | 版本  |
| --------------- | ---- |
| Bash | 4 和更新版本 |
| Python | 2.6.6 和更新版本  |


### <a name="identifying-volumes"></a>識別磁碟區

#### <a name="for-windows"></a>若為 Windows

當您執行 hello 可執行時，hello 作業系統掛接 hello 新磁碟區，並指派磁碟機代號。 您可以使用 Windows 檔案總管或檔案總管 toobrowse 這些磁碟機。 hello 分派 toohello 磁碟區的磁碟機代號可能無法保留相同的字母為 hello 原始虛擬機器，不過，hello 磁碟區名稱的 hello。 比方說，如果 hello hello 原始虛擬機器上的磁碟區是 「 資料磁碟 (e:\)"，磁碟區，可以附加為 「 資料磁碟 ('任何可用的磁碟機代號':\) hello 本機電腦上。 瀏覽 hello 指令碼輸出中所述，直到您找到您的檔案/資料夾的所有磁碟區。  
       
   ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>若為 Linux

在 Linux 中 hello hello 復原點磁碟區會掛接的 toohello 資料夾 hello 指令碼執行的位置。 hello 附加磁碟、 磁碟區和 hello 相對應的掛接路徑會跟著顯示。 這些裝載路徑會顯示 toousers 具有根層級存取。 瀏覽 hello hello 指令碼輸出中所述的磁碟區。

  ![Linux [檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>關閉 hello 連接

識別 hello 檔案，並將它們複製 tooa 本機儲存體位置之後, 移除 （或取消掛接） hello 其他磁碟機。 toounmount hello 上的磁碟機，hello**檔案復原**刀鋒視窗 hello Azure 入口網站中的按一下**取消掛接磁碟**。

![取消掛接磁碟](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

一旦 hello 磁碟已卸載，您會收到訊息，讓您知道已順利完成。 如此您就可以移除 hello 磁碟可能需要幾分鐘，讓 hello 連接 toorefresh。

在 Linux 中切斷 hello 連接 toohello 復原點之後，hello OS 不 hello 對應的掛接路徑自動移除。 這些為 「 字串 」 磁碟區存在，且會顯示，但當您存取/寫入 hello 檔案時，擲回錯誤。 可以手動移除它們。 hello 指令碼執行時，會識別任何先前的復原點從現有的這類磁碟區，並在同意時將它們清除。

## <a name="special-configurations"></a>特殊的組態

### <a name="dynamic-disks"></a>動態磁碟

如果您無法執行 hello 可執行指令碼在 hello 已備份的 Azure VM 有跨越多個磁碟 （跨距與等量磁碟區） 和 （或） 容錯磁碟區 （鏡像與 RAID 5 磁碟區） 動態磁碟上的磁碟區 hello 相同的 VM。 相反地，在任何其他電腦相容的作業系統上執行 hello 可執行指令碼。

### <a name="windows-storage-spaces"></a>Windows 儲存空間

Windows 儲存空間是一種技術可讓您 toovirtualize 存放裝置的 Windows 儲存體中。 與 Windows 儲存空間中，您可以工業標準磁碟群組成儲存集區，然後再建立稱為儲存空間，從這些儲存集區中的 hello 可用空間的虛擬磁碟。

如果 hello Azure VM 備份會使用 Windows 儲存空間，則您無法執行 hello 可執行指令碼在 hello 相同的 VM。 相反地，在任何其他電腦相容的作業系統上執行 hello 可執行指令碼。

### <a name="lvmraid-arrays"></a>LVM/RAID 陣列

在 Linux、 邏輯磁碟區管理員 (LVM) 及/或軟體 RAID 陣列會是透過多個磁碟使用的 toomanage 邏輯磁碟區。 如果備份 Linux VM 的 hello 使用 LVM 及/或 RAID 陣列，您無法執行 hello 指令碼在 hello 相同的 VM。 改為執行任何其他電腦相容的作業系統上的 hello 指令碼，並可支援 hello VM 備份的檔案系統。

hello 指令碼輸出會顯示 hello LVM 和/或 RAID 陣列磁碟與 hello hello 分割區類型，如下所示的磁碟區

   ![Linux LVM 輸出刀鋒視窗](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
遵循 hello 需要 toobe 執行命令的 hello 使用者 toobring 這些資料分割線上。 

**若為 LVM 磁碟分割**

```
$ pvs <volume name as shown above in hello script output> 
```
這樣就會列出 hello 磁碟區群組名稱下的實體磁區。

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
這會列出所有邏輯磁碟區、名稱和其磁碟區群組中的路徑。

```
$ mount <LV path> </mountpath>
```
toomount hello 邏輯磁碟區 toohello 路徑您選擇。


**若為 RAID 陣列**

```
$ mdadm –detail –scan
```
這會顯示有關所有 RAID 磁碟的詳細資料。 hello 相關的 RAID 磁碟將會顯示為`/dev/mdm/<RAID array name in hello backed up VM>`

如果 hello RAID 磁碟有實體磁碟區，請使用 hello mount 命令。
```
$ mount [RAID Disk Path] [/mounthpath]
```

如上面所述的 LVM 磁碟分割與 hello hello RAID 磁碟名稱的磁碟區名稱，再依照此 RAID 磁碟是否設定中的另一個 LVM hello 相同的程序

## <a name="troubleshooting"></a>疑難排解

如果您從 hello 虛擬機器復原檔案時遇到問題，請檢查 hello 下表，如需詳細資訊。

| 錯誤訊息 / 案例 | 可能的原因 | 建議的動作 |
| ------------------------ | -------------- | ------------------ |
| Exe 輸出：*連接 toohello 目標的例外狀況* |指令碼不能 tooaccess hello 復原點 | 檢查是否 hello 機器符合上面所述的 hello 存取需求|  
|   Exe 輸出： *hello 目標已記錄在透過 ISCSI 工作階段。* |   hello 已經附加相同的電腦和 hello 磁碟機上已執行 hello 指令碼 |   hello hello 復原點磁碟區已連接。 可能未裝載以相同的磁碟機代號的 hello hello 原始 VM。 瀏覽所有 hello 可用的磁碟區在 hello 檔案總管 中的檔案 |
| Exe 輸出：*此指令碼無效，因為透過入口網站/超過 hello 12 hr 限制已解下 hello 磁碟。請從 hello 入口網站下載新的指令碼。* |    從 hello 入口網站或超過 hello 12 hr 限制已解下磁碟 hello |  此特定 exe 目前無效，無法執行。 如果您想 tooaccess hello 該復原點時間的檔案，請瀏覽新的 exe 的 hello 入口網站|
| Hello hello exe 執行所在的電腦上： hello 新磁碟區未卸載之後 hello 卸載按鈕 |    hello hello 機器上的 ISCSI 啟動器無法回應/重新整理其連線 toohello 目標及維護 hello 快取 |    等候一些分鐘之後按下 hello 卸載按鈕。 如果仍然無法卸載 hello 新磁碟區，請瀏覽 hello 的所有磁碟區。 不提供這個 hello 磁碟的強制執行 hello 啟動器 toorefresh hello 連接和 hello 磁碟區卸載並出現錯誤訊息|
| Exe 輸出： 指令碼執行成功，但 「 附加的新磁碟區 」 不會顯示在 hello 指令碼輸出 |   這是暫時性的錯誤   | hello 磁碟區就已附加之後。 開啟檔案總管 toobrowse。 如果您使用相同電腦的 hello 每次執行指令碼，請考慮重新啟動機器 hello 和 hello 清單應該會顯示在 hello 後續 exe 執行。 |
| Linux 特定： 無法 tooview hello 所需的磁碟區 | hello OS 的 hello 機器 hello 指令碼執行的位置可能無法辨識 hello 的 hello 備份 VM 的基礎檔案系統 | 檢查是否 hello 復原點已損毀一致或檔案一致。 如果檔案一致，請執行 hello 指令碼，在其作業系統辨識 hello 的另一部電腦上備份 VM 的檔案系統 |
| Windows 特定： 無法 tooview hello 所需的磁碟區 | hello 磁碟可能已附加，但未設定 hello 磁碟區 | 從 hello 磁碟管理 畫面中，找出 hello 額外的磁碟相關的 toohello 復原點。 如果任何這些磁碟處於離線狀態嘗試進行上線 hello 磁碟上按一下滑鼠右鍵，然後按一下 「 線上 」 狀態|
