---
title: "aaaTroubleshoot Azure 備份傳統入口網站中的錯誤 |Microsoft 文件"
description: "疑難排解 Azure 備份和還原 hello 傳統入口網站中的 Azure 虛擬機器。"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Azure 虛擬機器備份的疑難排解
> [!div class="op_single_selector"]
> * [復原服務保存庫](backup-azure-vms-troubleshoot.md)
> * [備份保存庫](backup-azure-vms-troubleshoot-classic.md)
>
>

您可以疑難排解資訊搭配使用 Azure Backup 中 hello 下表所列時發生錯誤。

## <a name="discovery"></a>探索
| 備份作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 探索 |無法 toodiscover 新和項目-Microsoft Azure Backup 發生內部錯誤。 等候幾分鐘的時間，然後再次嘗試 hello 操作。 |在 15 分鐘之後，重試 hello 探索程序。 |
| 探索 |無法 toodiscover 新項目 – 另一個作業正在進行中的探索。 請 hello 目前的探索作業完成之前，稍候。 |None |

## <a name="register"></a>註冊
| 備份作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 註冊 |附加 toohello 虛擬機器超過 hello 支援限制的資料磁碟數目-請中斷連接此虛擬機器，然後重試 hello 作業的某些資料磁碟。 Azure 的備份支援向上 too16 資料磁碟附加 tooan Azure 虛擬機器進行備份 |None |
| 註冊 |Microsoft Azure 備份發生內部錯誤-稍候幾分鐘的時間，然後再試一次 hello 作業。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 |您可以取得此錯誤，因為不支援的 hello 遵循 tooone 組態的 VM 上 Premium LRS。 <br> 進階儲存體 VM 可以使用復原服務保存庫來進行備份。 [深入了解](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| 註冊 |因為安裝代理程式作業逾時而註冊失敗 |確認是否支援 hello hello 虛擬機器的 OS 版本。 |
| 註冊 |命令執行失敗 - 另一項作業正在此項目上進行。 請 hello 先前的作業完成之前，稍候 |None |
| 註冊 |不支援備份在進階儲存體中儲存虛擬硬碟的虛擬機器 |None |
| 註冊 |虛擬機器代理程式不存在於 hello 虛擬機器-請安裝 hello 所需的必要條件，VM 代理程式並重新啟動 hello 作業。 |[深入了解](#vm-agent)有關安裝 VM 代理程式，以及如何 toovalidate hello VM 代理程式安裝。 |

## <a name="backup"></a>備份
| 備份作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 備份 |無法與 hello VM 代理程式的快照集的狀態進行通訊。 快照 VM 子工作已逾時。-請查看 hello 疑難排解指南如何 tooresolve 這。 |如果以 hello VM 代理程式問題，或網路存取 toohello Azure 基礎結構會封鎖在某些方面，會擲回這個錯誤。 深入了解如何 [偵錯 VM 快照集問題](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md)。 <br> 如果 hello VM 代理程式不會造成任何問題，然後重新啟動 hello VM。 有些時候不正確的 VM 狀態可能會造成問題，重新啟動 hello VM 並重設這 「 不正確的狀態 」 |
| 備份 |備份失敗，發生內部錯誤-請重試 hello 作業在幾分鐘的時間。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務 |請檢查存取 VM 儲存體時是否有暫時性的問題。 請檢查[Azure 狀態](https://azure.microsoft.com/en-us/status/)toosee 如果沒有任何進行中的發行相關的 toocompute/儲存體/網路 hello 區域中。 請降低重試 hello 備份張貼問題。 |
| 備份 |因為 VM 已不存在，無法執行 hello 作業。 |無法執行備份，因為 hello VM 設定備份已經刪除。 請將 tooProtected 項目 檢視來停止進一步的備份，並選取 受保護的項目，然後按一下 停止保護。 您可以選取 [保留備份資料] 選項來保留資料。 您可以在稍後從 [已註冊的項目] 檢視按一下 [設定保護]，以繼續保護此虛擬機器 |
| 備份 |失敗的 tooinstall hello hello 選取項目-VM 代理程式上的 Azure 復原服務延伸模組是 Azure 復原服務延伸模組的必要條件。 請安裝 hello Azure VM 代理程式，並重新啟動 hello 註冊作業 |<ol> <li>檢查 hello VM 代理程式是否已正確安裝。 <li>請確定該 hello hello VM 組態上的旗標已正確設定。</ol> [深入了解](#validating-vm-agent-installation)有關安裝 VM 代理程式，以及如何 toovalidate hello VM 代理程式安裝。 |
| 備份 |命令執行失敗 - 另一項作業目前正在此項目上進行。 Hello 先前的作業完成後之前，請稍候，然後重試 |現有的備份或還原作業的 hello VM 正在執行，而且 hello 現有作業執行時，無法啟動新的工作。 |
| 備份 |擴充功能安裝失敗，錯誤碼 hello 「 COM + 無法 tootalk toohello Microsoft Distributed Transaction Coordinator |這通常表示未執行 hello COM + 服務。 請連絡 Microsoft 支援服務來協助解決此問題。 |
| 備份 |快照集作業失敗，發生 hello VSS 作業錯誤 「 此磁碟機已由 BitLocker 磁碟機加密鎖定。 您必須至 [控制台] 解除鎖定這個磁碟機。 |關閉 BitLocker 的 hello VM 上的所有磁碟機，並觀察 hello VSS 問題是否已解決 |
| 備份 |不支援備份在進階儲存體中儲存虛擬硬碟的虛擬機器 |None |
| 備份 |找不到 Azure 虛擬機器。 |這會 hello 主要 VM 已刪除，但 hello 備份原則仍會繼續 toolook VM tooperform 備份。 toofix 這個錯誤： <ol><li>重新建立以 hello hello 虛擬機器相同的名稱和相同的資源群組名稱 [雲端服務名稱] <br>(或) <li> 停用此 VM 的保護，以免觸發後續的備份。 </ol> |
| 備份 |虛擬機器代理程式不存在於 hello 虛擬機器-請安裝 hello 所需的必要條件，VM 代理程式並重新啟動 hello 作業。 |[深入了解](#vm-agent)有關安裝 VM 代理程式，以及如何 toovalidate hello VM 代理程式安裝。 |

## <a name="jobs"></a>工作
| 作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 取消工作 |此工作類型不支援取消-hello 作業完成之前，請稍候。 |None |
| 取消工作 |hello 工作不處於可取消的狀態-hello 作業完成之前，請稍候。 <br>或<br> hello 選取的工作不處於可取消的狀態-請等候 hello 作業 toocomplete。 |在所有的可能性，幾乎已完成 hello 作業;請 hello 作業完成之前，稍候 |
| 取消工作 |無法取消 hello 工作，因為它不在進行中-也就是進行中的工作只支援取消。 請嘗試取消進行中的工作。 |這是因為 tooa 暫時性狀態。 等候數分鐘，然後重試 hello 取消作業 |
| 取消工作 |失敗的 toocancel hello 作業-請等候作業完成。 |None |

## <a name="restore"></a>還原
| 作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 還原 |還原失敗並發生雲端內部錯誤 |<ol><li>您嘗試 toorestore 的雲端服務 toowhich 已設定 DNS 設定。 您可以檢查 <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>如果設定了 Address，這表示已設定 DNS 設定。<br> <li>正在雲端服務 toowhich tooyou toorestore 設有 ReservedIP 與雲端服務中的現有 Vm 處於停止狀態。<br>您可以使用下列 powershell Cmdlet，來檢查雲端服務是否具有保留的 IP：<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>您正嘗試 toorestore toosame 雲端服務中的下列特殊的網路設定與虛擬機器。 <br>- 負載平衡器組態下的虛擬機器 (內部與外部)<br>- 具有多個保留 IP 的虛擬機器<br>- 具有多個 NIC 的虛擬機器<br>請在 hello UI 中選取 新的雲端服務，或請參閱太[還原考量](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations)vm 使用特殊的網路組態</ol> |
| 還原 |選取的 hello DNS 名稱已有人-請指定不同的 DNS 名稱，然後再試一次。 |hello 此 DNS 名稱是指 toohello 雲端服務名稱 (通常以結束。.cloudapp.net)。 這需要 toobe 唯一。 如果您遇到這個錯誤，您會在還原期間需要 toochoose 不同的 VM 名稱。 <br><br> 只有 toousers 的 hello Azure 入口網站時，會顯示此錯誤。 hello 透過 PowerShell 的還原作業成功，因為它只還原 hello 磁碟並不會建立 hello VM。 當 hello VM 由您明確建立 hello 磁碟還原作業之後，將會面臨 hello 錯誤。 |
| 還原 |hello 指定的虛擬網路組態不正確-請指定不同的虛擬網路組態，並再試一次。 |None |
| 還原 |雲端服務會使用保留的 IP，這不符合 hello 虛擬機器正在還原的 hello 組態-請指定不同的雲端服務並未使用保留的 IP，或選擇另一個復原點 toorestore 從指定的 hello。 |None |
| 還原 |雲端服務已達到重試 hello 操作藉由指定不同的雲端服務或使用現有端點的輸入結束點的數目限制。 |None |
| 還原 |備份保存庫與目標儲存體帳戶位於兩個不同的區域-請指定在還原作業中的 hello 儲存體帳戶處於 hello 與 hello 備份保存庫相同的 Azure 區域。 |None |
| 還原 |儲存體帳戶指定 hello 還原作業的不支援-只基本/標準儲存體帳戶與本機備援或異地備援複寫設定支援。 請選取支援的儲存體帳戶 |None |
| 還原 |還原作業指定的儲存體帳戶類型不在線上-請確定在還原作業中指定的 hello 儲存體帳戶已連線 |這可能會發生，因為發生暫時性錯誤，在 Azure 儲存體或 tooan 中斷。 請選擇另一個儲存體帳戶。 |
| 還原 |已達到資源群組配額-請從 Azure 入口網站刪除一些資源群組，或連絡 Azure 支援 tooincrease hello 限制。 |None |
| 還原 |選取的子網路不存在：請選取已存在的子網路 |None |

## <a name="policy"></a>原則
| 作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 建立原則 |失敗的 toocreate hello 原則-請減少 hello 保留選擇 toocontinue 原則設定。 |None |

## <a name="vm-agent"></a>VM 代理程式
### <a name="setting-up-hello-vm-agent"></a>Hello VM 代理程式設定
一般而言，hello VM 代理程式已有 Vm 中建立的 hello Azure 圖庫中。 不過，從內部部署資料中心移轉的虛擬機器沒有 hello 安裝 VM 代理程式。 對於這類的 Vm，hello VM 代理程式需要明確安裝 toobe。 深入了解[現有的 VM 上安裝 hello VM 代理程式](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)。

若為 Windows VM：

* 下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 您需要系統管理員權限 toocomplete hello 安裝。
* [更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。

如為 Linux VM：

* 從 GitHub 安裝最新版 [Linux 代理程式](https://github.com/Azure/WALinuxAgent) 。
* [更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。

### <a name="updating-hello-vm-agent"></a>更新 hello VM 代理程式
若為 Windows VM：

* 更新 hello VM 代理程式的很簡單，重新安裝 hello [VM 代理程式二進位檔](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 不過，您需要 tooensure hello VM 代理程式正在更新時執行任何備份作業。

如為 Linux VM：

* 依 hello 指示[更新 Linux VM 代理程式](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

### <a name="validating-vm-agent-installation"></a>驗證 VM 代理程式安裝
如何針對 toocheck hello Windows Vm 上的 VM 代理程式版本：

1. 登入 toohello Azure 虛擬機器，並瀏覽 toohello 資料夾*C:\WindowsAzure\Packages*。 您應該尋找 hello WaAppAgent.exe 檔案存在。
2. 以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，然後選取 hello**詳細資料**hello 產品版本 索引標籤 欄位應該是 2.6.1198.718 或更高版本
