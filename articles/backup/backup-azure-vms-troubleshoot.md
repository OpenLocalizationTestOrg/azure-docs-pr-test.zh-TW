---
title: "使用 Azure 虛擬機器的 aaaTroubleshoot 備份錯誤 |Microsoft 文件"
description: "Azure 虛擬機器備份與還原的疑難排解"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 73214212-57a4-4b57-a2e2-eaf9d7fde67f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: trinadhk;markgal;jpallavi;
ms.openlocfilehash: 9224c47e02b52688adcba5876c674c88502557c6
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

## <a name="backup"></a>備份
| 錯誤詳細資料 | 因應措施 |
| --- | --- |
| 因為 VM 已不存在，無法執行 hello 作業。 - 停止保護虛擬機器，但不刪除備份資料。 http://go.microsoft.com/fwlink/?LinkId=808124 有更多詳細資料 |這會 hello 主要 VM 已刪除，但 hello 備份原則仍會繼續針對 VM tooback 查閱。 toofix 這個錯誤： <ol><li> 重新建立以 hello hello 虛擬機器相同的名稱和相同的資源群組名稱 [雲端服務名稱]<br>(或)</li><li> 停止保護虛擬機器，不論刪除 hello 備份資料。 [更多詳細資料](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| 快照集作業失敗，因為 toono hello 虛擬機器層上的網路連線，請確定 VM 具有網路存取權。 快照集 toosucceed 請白名單的 Azure 資料中心 IP 範圍，或設定網路存取的 proxy 伺服器。 如需詳細資訊，請參閱太 http://go.microsoft.com/fwlink/?LinkId=800034。 如果您已經使用 Proxy 伺服器，請確定已正確設定 Proxy 伺服器設定 | 拒絕 hello 虛擬機器上的 hello 連出網際網路連線時，會擲回這個錯誤。 VM 的快照集延伸模組 tootake hello 虛擬機器的基礎磁碟的快照集需要網際網路連線。 [進一步了解](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine)上 toofix 快照失敗，因為 tooblocked 網路存取的方式。 |
| VM 代理程式 」 無法 toocommunicate 以 hello Azure 備份服務。 -確認 hello VM 具有網路連線和 hello VM 代理程式是最新且正在執行。 如需詳細資訊，請參閱太 http://go.microsoft.com/fwlink/?LinkId=800034 |如果以 hello VM 代理程式問題，或網路存取 toohello Azure 基礎結構會封鎖在某些方面，會擲回這個錯誤。 [深入了解](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vm-agent-unable-to-communicate-with-azure-backup)如何進行 VM 快照集問題偵錯。<br> 如果 hello VM 代理程式不會造成任何問題，然後重新啟動 hello VM。 有些時候不正確的 VM 狀態可能會造成問題，並重設 hello VM 重新啟動此 「 不正確的狀態 」。 |
| VM 處於 「 失敗 」 佈建狀態-請重新啟動 hello VM，並確定 VM 處於執行中或關機的狀態，備份該 hello | 這發生在其中一個 hello 延伸失敗導致 VM 狀態 toobe failed 佈建狀態。 移 tooextensions 清單並查看是否有失敗的延伸模組移除它，請嘗試重新啟動 hello 虛擬機器。 如果所有延伸模組都是處於執行狀態，請檢查 VM 代理程式服務是否正在執行。 否則，請重新啟動 hello VM 代理程式服務。 | 
| VMSnapshot 延伸作業失敗的受管理的磁碟-請重試 hello 備份作業。 如果 hello 問題重複出現，請依照下列指示 'http://go.microsoft.com/fwlink/?LinkId=800034' hello。 如果進一步失敗，請連絡 Microsoft 支援 | Azure 備份服務無法 tootrigger 快照集時發生此錯誤。 [深入了解](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vmsnapshot-extension-operation-failed)如何進行 VM 快照集問題偵錯。 |
| 可能未複製 hello hello 虛擬機器的快照，因為 tooinsufficient hello 儲存體帳戶-可用空間確定儲存體帳戶中沒有對等的可用空間 toohello hello 高階儲存體磁碟上的資料附加 toohello 虛擬機器 | 如果 premium Vm，我們要複製 hello 快照集 toostorage 帳戶。 這是 toomake 確定備份管理流量，在快照集運作，並不會限制使用高階磁碟的 IOPS 可用 toohello 應用程式的 hello 數目。 Microsoft 建議您配置只達 50%的 hello 總儲存體帳戶的空間，因此 hello Azure 備份服務可以複製此複製的位置，在儲存體帳戶 toohello 保存庫中的 hello 快照 toostorage 帳戶和傳送資料。 | 
| 無法 tooperform hello 操作，因為 hello VM 代理程式沒有回應 |如果以 hello VM 代理程式問題，或網路存取 toohello Azure 基礎結構會封鎖在某些方面，會擲回這個錯誤。 適用於 Windows Vm，請檢查 hello VM 代理程式服務和 hello 代理程式是否會出現在 [控制台] 中的程式中的服務狀態。 請嘗試移除 hello 程式從控制項面板和重新安裝 hello 代理程式所述[下方](#vm-agent)。 重新安裝之後 hello 代理程式，會觸發臨機操作備份 tooverify。 |
| 復原服務擴充作業失敗。 -請請先確定最新的虛擬機器代理程式已存在於 hello 虛擬機器，且代理程式服務正在執行。 請重試備份作業，如果失敗，請連絡 Microsoft 支援服務。 |VM 代理程式過期時會擲回這個錯誤。 請參閱下 tooupdate hello VM 代理程式的 「 更新 hello VM 代理程式 」 一節。 |
| 虛擬機器不存在。 - 請確定該虛擬機器存在，或選取不同的虛擬機器。 |這會 hello 主要 VM 已刪除，但 hello 備份原則仍會繼續 toolook VM tooperform 備份。 toofix 這個錯誤： <ol><li> 重新建立以 hello hello 虛擬機器相同的名稱和相同的資源群組名稱 [雲端服務名稱]<br>(或)<br></li><li>停止保護 hello 虛擬機器而不刪除 hello 備份資料。 [更多詳細資料](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| 命令執行失敗。 另一項作業目前正在此項目上進行。 Hello 先前的作業完成後之前，請稍候，然後重試 |在 hello VM 上現有的備份正在執行，而且 hello 現有作業執行時，無法啟動新的工作。 |
| 從 hello 備份保存庫複製 Vhd 已逾時-請重試 hello 作業在幾分鐘的時間。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 | 會發生這種情況是如果在儲存體端暫時性錯誤，或備份服務未取得來自裝載 hello VM 內逾時期間 toovault 順序 tootransfer 資料中的儲存體帳戶足夠的 IOPS。 確定您在設定備份時已遵循[最佳作法](backup-azure-vms-introduction.md#best-practices)。 請嘗試移動 VM，就不會載入 tooa 不同的儲存體帳戶，然後重試備份。|
| 備份失敗，發生內部錯誤-請重試 hello 作業在幾分鐘的時間。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務 |這個錯誤的發生原因有 2 個： <ol><li> 存取 hello VM 存放裝置中沒有的暫時性問題。 請檢查[Azure 狀態](https://azure.microsoft.com/en-us/status/)toosee 是否有任何進行中的問題相關 toocompute、 儲存或 hello 區域中的網路功能。 一旦 hello 問題已解決，然後重試 hello 備份工作。 <li>hello 原始 VM 已經被刪除，因此無法進行 hello 復原點。 tookeep hello 備份資料的已刪除的 VM，但移除 hello 備份錯誤： 取消保護 hello VM，然後選擇 hello 選項 tookeep hello 資料。 這個動作停止 hello 已排定的備份工作與 hello 週期性的錯誤訊息。 |
| 無法在 hello 選取項目上的 tooinstall hello Azure 復原服務擴充功能-hello VM 代理程式 hello Azure 復原服務延伸模組的必要條件。 安裝 hello Azure VM 代理程式並重新啟動 hello 註冊作業 |<ol> <li>檢查 hello VM 代理程式是否已正確安裝。 <li>確定已正確設定 hello VM 組態上的 hello 旗標。</ol> [深入了解](#validating-vm-agent-installation)關於安裝 hello VM 代理程式，及如何 toovalidate hello VM 代理程式安裝。 |
| 擴充功能安裝失敗，錯誤碼 hello 「 COM + 無法 tootalk toohello Microsoft Distributed Transaction Coordinator |這通常表示未執行 hello COM + 服務。 請連絡 Microsoft 支援服務來協助解決此問題。 |
| 快照集作業失敗，發生 hello VSS 作業錯誤 「 此磁碟機已由 BitLocker 磁碟機加密鎖定。 您必須解除鎖定這個磁碟機從 hello 控制台。 |關閉 BitLocker 的 hello VM 上的所有磁碟機，並觀察 hello VSS 問題是否已解決 |
| VM 目前的狀態不允許備份。 |<ul><li>檢查 VM 是否處於「執行中」與「關閉」之間的暫時性狀態。 如果是，等候其中一個 hello VM 狀態 toobe 和觸發程序一次備份。 <li> 如果 hello VM Linux VM，使用 [安全性增強 Linux] 核心模組，您需要 tooexclude hello Linux 代理程式的路徑 (_/var/lib/waagent_) 安全性原則 toomake 確定備份副檔名取得已安裝。  |
| 找不到 Azure 虛擬機器。 |這會 hello 主要 VM 已刪除，但 hello 備份原則會針對 VM tooperform toolook 繼續備份。 toofix 這個錯誤： <ol><li>重新建立以 hello hello 虛擬機器相同的名稱和相同的資源群組名稱 [雲端服務名稱] <br>(或) <li> 停用 hello 備份工作將不會建立此 VM 的保護。 </ol> |
| Hello 虛擬機器上沒有虛擬機器代理程式-請安裝任何必要條件和 hello VM 代理程式，然後再重新啟動 hello 作業。 |[深入了解](#vm-agent)有關安裝 VM 代理程式，以及如何 toovalidate hello VM 代理程式安裝。 |
| 快照集作業失敗，因為 tooVSS 寫入器處於錯誤狀態 |您需要 toorestart （磁碟區陰影複製服務） 的 VSS 寫入器處於不正常的狀態。 tooachieve，從提升權限的命令提示字元中執行_vssadmin 清單寫入器_。 輸出會包含所有 VSS 寫入器和其狀態。 對於每個狀態不是「[1] 穩定」的 VSS 寫入器，請從提升權限的命令提示字元執行下列命令，重新啟動 VSS 寫入器：<br> _net stop serviceName_ <br> _net start serviceName_|
| 快照集作業失敗，因為 hello 組態 tooa 剖析失敗 |這會因 toochanged hello MachineKeys 目錄上的權限： _%systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br>請執行下列命令，並確認 MachineKeys 目錄的權限是預設的︰<br>_icacls %systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br><br> 預設權限是︰<br>Everyone:(R,W) <br>BUILTIN\Administrators:(F)<br><br>如果您發現 MachineKeys 目錄預設值不同的權限，請遵照下列步驟 toocorrect 權限刪除 hello 憑證，觸發 hello 備份。<ol><li>修正 MachineKeys 目錄上的權限。<br>Hello 目錄上使用總管安全性屬性和進階安全性設定，重設權限回 toohello 預設值，移除任何額外 （比預設值） 的使用者物件 hello 目錄，並確保該 hello '每個人都' 有特殊的權限存取權：<br>-列出資料夾/讀取資料 <br>-讀取屬性 <br>-讀取擴充屬性 <br>-建立檔案/寫入資料 <br>-建立資料夾/附加資料<br>-寫入屬性<br>-寫入擴充屬性<br>-讀取權限<br><br><li>刪除 [發給] 欄位 = "Windows Azure Service Management for Extensions" 或 "Windows Azure CRP Certificate Generator" 的所有憑證。<ul><li>[開啟 [憑證 (本機電腦)] 主控台](https://msdn.microsoft.com/library/ms788967(v=vs.110).aspx)<li>刪除 [發給] 欄位 = "Windows Azure Service Management for Extensions" 或 "Windows Azure CRP Certificate Generator" 的所有憑證 (在 [個人] -> [憑證] 下)。</ul><li>觸發 VM 備份。 </ol>|
| 驗證失敗，因為虛擬機器單獨以 BEK 進行加密。 只會對同時使用 BEK 和 KEK 加密的虛擬機器啟用備份。 |虛擬機器應該使用「BitLocker 加密金鑰」和「金鑰加密金鑰」進行加密。 之後，應該啟用備份。 |
| Azure 備份服務沒有足夠的權限 tooKey 保存庫適用於備份的加密虛擬機器。 |應使用 [PowerShell 文件](backup-azure-vms-automation.md)的**啟用備份**區段中所述的步驟，在 PowerShell 中向備份服務提供這些權限。 |
|安裝的快照集失敗，發生錯誤的擴充功能-COM + 是無法 tootalk toohello Microsoft Distributed Transaction Coordinator | 請再試一次 toostart windows 服務 「 COM + 系統應用程式 」 (從提升權限的命令提示字元- _net 啟動 COMSysApp_)。 <br>如果在啟動時失敗，請遵循下列步驟︰<ol><li> 驗證服務 」 分散式交易協調器 」 hello 登入帳戶是 「 網路服務 」。 如果不存在，請將它變更太 「 網路服務 」，重新啟動此服務，然後再次嘗試 toostart 服務 「 COM + 系統應用程式 」。 '<li>如果仍然失敗 toostart，解除安裝/安裝服務 」 分散式交易協調器 」 依照下列步驟：<br> -停止 hello MSDTC 服務<br> - 開啟命令提示字元 (cmd) <br> - 執行命令 “msdtc -uninstall” <br> - 執行命令 “msdtc -install” <br> -開始 hello MSDTC 服務<li>啟動 Windows 服務 "COM+ System Application"，啟動之後，從入口網站觸發備份。</ol> |
|  快照集作業失敗，因為 tooCOM + 錯誤 | hello 建議的動作是 toorestart windows 服務 「 COM + 系統應用程式 」 (從提升權限的命令提示字元- _net 啟動 COMSysApp_)。 如果 hello 問題持續發生，請重新啟動 hello VM。 如果重新啟動 VM 沒有幫助的 hello，請嘗試[移除 hello VMSnapshot 延伸](https://docs.microsoft.com/en-us/azure/backup/backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout#cause-3-the-backup-extension-fails-to-update-or-load)和手動觸發 hello 備份。 |
| 失敗 toofreeze 其中一個或多個掛接點 hello VM tootake 檔案系統一致性快照集 | 使用下列步驟的 hello: <ol><li>檢查使用的所有已掛接裝置 hello 檔案系統狀態_'tune2fs'_命令。<br> 例如：tune2fs -l /dev/sdb1 \| grep "Filesystem state" <li>取消掛接適用於 filesystem 的狀態不是使用全新的 hello 裝置_'umount'_命令 <li> 使用 _'fsck'_ 命令對這些裝置執行 FileSystemConsistency 檢查 <li> 再次掛接 hello 裝置，然後再試一次備份。</ol> |
| 快照集作業失敗，因為在建立安全的網路通訊通道 toofailure | <ol><Li> 在提高權限的模式中執行 regedit.exe，開啟登錄編輯程式。 <li> 識別系統中存在的所有 .NetFramework 版本。 它們是底下的登錄機碼"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft"hello 階層 <li> 針對登錄機碼中的每個 .NetFramework，新增下列機碼︰ <br> "SchUseStrongCrypto"=dword:00000001 </ol>|
| 快照集作業失敗，因為在安裝 Visual c + + 可轉散發套件適用於 Visual Studio 2012 toofailure | 瀏覽 tooC:\Packages\Plugins\Microsoft.Azure.RecoveryServices.VMSnapshot\agentVersion，並安裝 vcredist2012_x64。 請確定登錄機碼值，允許此服務的安裝設定 toocorrect 值也就是登錄機碼值_HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Msiserver_設定 too3 並不是 4。 如果您仍遇到安裝問題，請從提高權限的命令提示字元執行 _MSIEXEC /UNREGISTER_，再執行 _MSIEXEC /REGISTER_，以重新啟動安裝服務。  |


## <a name="jobs"></a>作業
| 錯誤詳細資料 | 因應措施 |
| --- | --- |
| 此工作類型不支援取消-hello 作業完成之前，請稍候。 |None |
| hello 工作不處於可取消的狀態-hello 作業完成之前，請稍候。 <br>或<br> hello 選取的工作不處於可取消的狀態-請等候 hello 作業 toocomplete。 |在所有的可能性，幾乎完成 hello 作業。 請 hello 工作完成之前，稍候。|
| 無法取消 hello 工作，因為它不在進行中-也就是進行中的工作只支援取消。 請嘗試取消進行中的工作。 |這是因為 tooa 暫時性狀態。 等候數分鐘，然後重試 hello 取消作業。 |
| 失敗的 toocancel hello 作業-請等候工作完成。 |None |

## <a name="restore"></a>還原
| 錯誤詳細資料 | 因應措施 |
| --- | --- |
| 還原失敗並發生雲端內部錯誤 |<ol><li>您嘗試 toorestore 的雲端服務 toowhich 已設定 DNS 設定。 您可以檢查 <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>如果設定了 Address，這表示已設定 DNS 設定。<br> <li>正在雲端服務 toowhich tooyou toorestore 設有 ReservedIP 與雲端服務中的現有 Vm 處於停止狀態。<br>您可以使用下列 powershell Cmdlet，來檢查雲端服務是否具有保留的 IP：<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>您正嘗試 toorestore toosame 雲端服務中的下列特殊的網路設定與虛擬機器。 <br>- 負載平衡器組態下的虛擬機器 (內部與外部)<br>- 具有多個保留 IP 的虛擬機器<br>- 具有多個 NIC 的虛擬機器<br>請在 hello UI 中選取 新的雲端服務，或請參閱太[還原考量](backup-azure-arm-restore-vms.md#restoring-vms-with-special-network-configurations)使用特殊的網路組態的 vm。</ol> |
| 選取的 hello DNS 名稱已有人-請指定不同的 DNS 名稱，然後再試一次。 |hello 此 DNS 名稱是指 toohello 雲端服務名稱 (通常以結束。.cloudapp.net)。 這需要 toobe 唯一。 如果您遇到這個錯誤，您會在還原期間需要 toochoose 不同的 VM 名稱。 <br><br> 只有 toousers 的 hello Azure 入口網站時，會顯示此錯誤。 hello 透過 PowerShell 的還原作業將會成功，因為它只還原 hello 磁碟並不會建立 hello VM。 當 hello VM 由您明確建立 hello 磁碟還原作業之後，將會面臨 hello 錯誤。 |
| hello 指定的虛擬網路組態不正確-請指定不同的虛擬網路組態，並再試一次。 |None |
| 雲端服務會使用保留的 IP，不符合 hello 正在還原的 hello 虛擬機器設定-請指定不同的雲端服務，不使用保留的 IP，或選擇其他復原點 toorestore 從指定的 hello。 |None |
| 雲端服務已達到重試 hello 操作藉由指定不同的雲端服務或使用現有端點的輸入結束點的數目限制。 |None |
| 備份保存庫與目標儲存體帳戶位於兩個不同的區域-請指定在還原作業中的 hello 儲存體帳戶處於 hello 與 hello 備份保存庫相同的 Azure 區域。 |None |
| 儲存體帳戶指定 hello 還原作業的不支援-只基本/標準儲存體帳戶與本機備援或異地備援複寫設定支援。 請選取支援的儲存體帳戶 |None |
| 還原作業指定的儲存體帳戶類型不在線上-請確定在還原作業中指定的 hello 儲存體帳戶已連線 |這可能會發生，因為發生暫時性錯誤，在 Azure 儲存體或 tooan 中斷。 請選擇另一個儲存體帳戶。 |
| 已達到資源群組配額-請從 Azure 入口網站刪除一些資源群組，或連絡 Azure 支援 tooincrease hello 限制。 |None |
| 選取的子網路不存在：請選取已存在的子網路 |None |
| 備份服務您的訂用帳戶中沒有授權 tooaccess 資源。 |tooresolve 使用 > 一節中所述的步驟，先還原磁碟**磁碟備份還原**中[選擇 VM 還原組態](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)。 之後，請使用 PowerShell 步驟中所述[從還原的硬碟建立 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 完整 VM 從還原的磁碟。 |

## <a name="backup-or-restore-taking-time"></a>備份或還原很花時間
如果您發現備份 (超過 12小時) 或還原 (超過 6小時) 很花時間：
* 了解[因素造成 toobackup 時間](backup-azure-vms-introduction.md#total-vm-backup-time)和[因素造成 toorestore 時間](backup-azure-vms-introduction.md#total-restore-time)。
* 請務必遵循[備份最佳做法](backup-azure-vms-introduction.md#best-practices)。 

## <a name="vm-agent"></a>VM 代理程式
### <a name="setting-up-hello-vm-agent"></a>Hello VM 代理程式設定
一般而言，hello VM 代理程式已有 Vm 中建立的 hello Azure 圖庫中。 不過，從內部部署資料中心移轉的虛擬機器沒有 hello 安裝 VM 代理程式。 對於這類的 Vm，hello VM 代理程式需要明確安裝 toobe。

若為 Windows VM：

* 下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 您需要系統管理員權限 toocomplete hello 安裝。
* 針對傳統虛擬機器，[更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。 資源管理員虛擬機器不需要此步驟。

如為 Linux VM：

* 從發佈存放庫安裝最新版。 我們「強烈建議」只透過發佈存放庫安裝代理程式。 如需封裝名稱的詳細資訊，請參閱太[Linux 代理程式儲存機制](https://github.com/Azure/WALinuxAgent) 
* 對於傳統的 Vm，[更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。 資源管理員虛擬機器不需要此步驟。

### <a name="updating-hello-vm-agent"></a>更新 hello VM 代理程式
若為 Windows VM：

* 更新 hello VM 代理程式的很簡單，重新安裝 hello [VM 代理程式二進位檔](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 不過，您需要 tooensure hello VM 代理程式正在更新時執行任何備份作業。

如為 Linux VM：

* 依 hello 指示[更新 Linux VM 代理程式](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
我們**強烈建議**只透過發佈存放庫更新代理程式。 我們不建議從直接 github 下載 hello 代理程式程式碼及更新它。 如果最新的代理程式不是適用於您的散發，請聯繫 toodistribution 支援，如需有關指示 tooinstall 最新的代理程式。 您可以在 github 存放庫中檢查最新的 [Windows Azure Linux 代理程式](https://github.com/Azure/WALinuxAgent/releases)資訊。

### <a name="validating-vm-agent-installation"></a>驗證 VM 代理程式安裝
如何針對 toocheck hello Windows Vm 上的 VM 代理程式版本：

1. 登入 toohello Azure 虛擬機器，並瀏覽 toohello 資料夾*C:\WindowsAzure\Packages*。 您應該尋找 hello WaAppAgent.exe 檔案存在。
2. 以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，然後選取 hello**詳細資料**hello 產品版本 索引標籤 欄位應該是 2.6.1198.718 或更高版本

## <a name="troubleshoot-vm-snapshot-issues"></a>疑難排解 VM 快照問題
VM 備份依賴發出 toounderlying 儲存體的快照集命令。 在執行快照集工作中沒有這存取 toostorage 或延遲，可能會導致 hello 備份工作 toofail。 hello 下列可能會導致快照集工作失敗。

1. 網路存取 tooStorage 會封鎖使用 NSG<br>
    進一步了解如何太[啟用網路存取](backup-azure-vms-prepare.md#network-connectivity)tooStorage 使用其中一個允許的 Ip 或透過 proxy 伺服器的清單。
2. 已設定 SQL Server 備份的 VM 會造成快照工作延遲  <br>
   根據預設，VM 備份會核發 Windows VM 上的 VSS 完整備份。 在執行 SQL Server 且已設定 SQL Server 備份的 VM 上，這可能造成快照執行延遲。 如果您因為快照的問題而遇到備份失敗，請設定下列登錄機碼。

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
   "USEVSSCOPYBACKUP"="TRUE"
   ```
3. VM 狀態報告不正確，因為 RDP 中的 VM 關機。  <br>
   如果您已關閉 hello RDP 中的虛擬機器，請檢查 hello 入口網站中 VM 狀態會正確反映。 如果沒有，請關閉 VM 儀表板中使用 「 關閉 」 選項入口網站中的 hello VM。
4. 如果超過四個 Vm 共用 hello 相同雲端服務，因此可以不超過四個 VM 備份啟動的 hello 備份時間設定多個備份原則 toostage hello 相同的時間。 請嘗試 toospread hello 備份開始時間原則之間的距離一小時。
5. VM 正在以高 CPU/記憶體執行。<br>
   如果 hello 虛擬機器正在以高 CPU usage(>90%) 或記憶體，快照集工作已排入佇列、 延遲和最終將會取得逾時。在此情況下，請嘗試隨選備份。

<br>

## <a name="networking"></a>網路
如同所有擴充功能，備份延伸模組需要存取公用網際網路 toowork toohello。 不需要存取 toohello 公用網際網路可能會出現不同的方式：

* hello 延伸模組安裝可能會失敗
* hello 備份作業 （例如磁碟快照集） 可能會失敗
* 顯示 hello 狀態 hello 備份作業可能會失敗

已經以 hello 需要解析網際網路的公用位址[這裡](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx)。 您的 hello VNET 需要 toocheck hello DNS 設定，並確定 Azure Uri 可以解決該 hello。

完成 hello 名稱解析為正確，存取 Azure Ip 也必須提供 toobe toohello。 toounblock 存取 toohello Azure 基礎結構，請遵循下列步驟進行：

1. 白名單 hello Azure 資料中心 IP 範圍。
   * 取得 hello 清單[Azure 資料中心 Ip](https://www.microsoft.com/download/details.aspx?id=41653) toobe 白名單。
   * 解除封鎖 hello Ip 使用 hello[新增 NetRoute](https://technet.microsoft.com/library/hh826148.aspx) cmdlet。 在提升權限 （以系統管理員身分執行） 的 PowerShell 視窗執行這個指令程式 hello Azure VM 中。
   * （如果有的話就地） 加入規則 toohello NSG tooallow 存取 toohello Ip。
2. 建立 HTTP 流量 tooflow 的路徑
   * 如果您有一些網路限制之後 （網路安全性群組，例如） 部署 HTTP proxy 伺服器 tooroute hello 流量。 您可以在找到 HTTP Proxy 伺服器的步驟 toodeploy[這裡](backup-azure-vms-prepare.md#network-connectivity)。
   * （如果有的話就地） 加入規則 toohello NSG tooallow 存取 toohello 網際網路從 hello HTTP Proxy。

> [!NOTE]
> IaaS VM 備份 toowork 的 hello 客體內，就必須啟用 DHCP。  如果您需要靜態私人 ip 位址，您應該透過 hello 平台來進行設定。 hello 內啟用 VM 應該保持的 hello 的 DHCP 選項。
> 請參閱有關 [設定靜態內部私人 IP 位址](../virtual-network/virtual-networks-reserved-private-ip.md)的詳細資訊。
>
>
