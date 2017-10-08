---
title: "Azure 備份伺服器 aaaTroubleshoot |Microsoft 文件"
description: "針對安裝、註冊 Azure 備份伺服器以及備份和還原應用程式工作負載進行疑難排解"
services: backup
documentationcenter: 
author: pvrk
manager: shreeshd
editor: 
ms.assetid: 2d73c349-0fc8-4ca8-afd8-8c9029cb8524
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pullabhk;markgal;
ms.openlocfilehash: 2386cfcfbf7cc686b5c051d2e1a3a884481ccdc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-server"></a>針對 Azure 備份伺服器進行疑難排解

您可以疑難排解 Azure 備份伺服器使用資訊列在下表中的 hello 時發生錯誤。


## <a name="installation-issues"></a>安裝問題

| 作業 | 錯誤詳細資料 | 因應措施 |
|-----------|---------------|------------|
|安裝 | 安裝程式無法更新登錄中繼資料。 此更新失敗，可能會導致 tooover 使用量的存放裝置耗用量。 tooavoid 此請更新 hello 修剪 ReFS 登錄項目。 | 調整 SYSTEM\CurrentControlSet\Control\FileSystem\RefsEnableInlineTrim hello 登錄機碼。 設定 hello 值 Dword too1。 |
|安裝 | 安裝程式無法更新登錄中繼資料。 此更新失敗，可能會導致 tooover 使用量的存放裝置耗用量。 tooavoid 此請更新 hello 磁碟區 SnapOptimization 登錄項目。 | 建立 hello 登錄機碼，SOFTWARE\Microsoft 資料保護 Manager\Configuration\VolSnapOptimization\WriteIds，以空的字串值。 |

## <a name="registration-and-agent-related-issues"></a>註冊與代理程式相關問題
| 作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 註冊 tooa 保存庫 | 提供的保存庫認證無效。 hello 檔案可能已損毀或沒有不 hello 與復原服務相關聯的最新認證 | toofix 這個錯誤： <ol><li> 下載 hello 保存庫中的 hello 最新的認證檔案，並再試一次 <br>(或)</li> <li> 如果上述動作 hello 未解決問題，請嘗試下載 hello 認證 tooa 不同的本機目錄或建立新的保存庫 <br>(或)</li> <li> 請嘗試更新 hello 日期和時間設定，如中所述[這篇部落格](https://azure.microsoft.com/blog/troubleshooting-common-configuration-issues-with-azure-backup/) <br>(或)</li> <li> 檢查 c:\windows\temp 是否有超過 65000 個檔案。 移動過時檔案 tooanother 位置，或刪除 hello hello Temp 資料夾中的項目 <br>(或)</li> <li> 請檢查憑證的 hello 狀態 <br> a. 開啟 「 管理的電腦憑證 」 （在 hello 控制台) <br> b. 展開 hello 「 個人 」 節點，其 「 憑證 」 的子節點 <br> c.  移除 hello 憑證 [Windows Azure Tools] <br> d. 重試 hello Azure 備份用戶端中的 hello 註冊 <br> (或) </li> <li> 檢查是否已備有任何群組原則 </li></ol> |
| 推入代理程式 tooprotected 伺服器 | hello 代理程式作業失敗，因為發生通訊錯誤，以 hello DPM 代理程式協調員服務上\<伺服器名稱 > | **如果不適用於建議動作顯示 hello 產品中的 hello**， <ol><li> 如果您要連結來自不受信任網域的電腦，請遵循[這些](https://technet.microsoft.com/library/hh757801(v=sc.12).aspx)步驟 <br> (或) </li><li> 如果您將連接從受信任網域的電腦時，使用中所述的 hello 步驟疑難排解[這篇部落格](https://blogs.technet.microsoft.com/dpm/2012/02/06/data-protection-manager-agent-network-troubleshooting/) <br>(或)</li><li> 嘗試停用防毒來作為疑難排解步驟。 如果它解析 hello 問題時，修改 hello 防毒設定為 [本文] 中的建議 (https://technet.microsoft.com/library/hh757911.aspx)</li></ol> |
| 推入代理程式 tooprotected 伺服器 | 指定伺服器 hello 認證不正確 | **如果不適用於建議動作顯示 hello 產品中的 hello**， <br> 再試一次 tooinstall hello 保護代理程式中所指定的 hello 實際執行伺服器上手動[這篇文章](https://technet.microsoft.com/library/hh758186(v=sc.12).aspx#BKMK_Manual)|
| Azure 備份代理程式已無法 tooconnect toohello Azure Backup 服務 (識別碼： 100050) | hello Azure 備份代理程式已無法 tooconnect toohello Azure 備份服務。 | **如果不適用於建議動作顯示 hello 產品中的 hello**， <br>1.從提升權限的提示字元中執行下列命令︰psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"。這會開啟 IE 視窗。 <br/> 2.移 tooTools]-> [網際網路選項]-> [連接]-> [LAN 設定。 <br/> 3.確認系統帳戶的 Proxy 設定。 設定 Proxy IP 和連接埠。 <br/> 4.關閉 Internet Explorer。|
| Azure 備份代理程式安裝失敗 | hello Microsoft Azure 復原服務安裝失敗。 Hello Microsoft Azure Recovery Services 安裝 toohello 系統所做的所有變更都已經都還原。 (ID：4024) | 手動安裝 Azure 代理程式


## <a name="configuring-protection-group"></a>設定保護群組
| 作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 設定保護群組 | DPM 無法列舉受保護電腦 (受保護的電腦名稱) 上的應用程式元件 | 按一下 重新整理' hello hello 相關的資料來源/元件層級設定保護群組 UI 畫面 |
| 設定保護群組 | 無法 tooconfigure 保護 | 如果 SQL server hello 受保護的伺服器，請檢查是否 sysadmin 角色權限已提供 toohello 系統帳戶 ntauthority\system （新增） hello 受保護的電腦上所述[這篇文章](https://technet.microsoft.com/library/hh757977(v=sc.12).aspx)
| 設定保護群組 | Hello 針對此保護群組的存放集區中沒有足夠的可用空間 | hello 可加入 toohello 存放集區磁碟[不應包含資料分割](https://technet.microsoft.com/library/hh758075(v=sc.12).aspx)。 刪除 hello 磁碟上的任何現有磁碟區，然後再加入 toohello 存放集區|
| 原則變更 |無法修改 hello 備份原則。 錯誤： hello 目前的作業失敗，因為 tooan 內部服務錯誤 [0x29834]。 請稍後重試 hello 作業。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 |**原因：**<br/>當安全性設定已啟用時，您嘗試 tooreduce 下方 hello 上述指定的最小值的保留範圍而您位於不受支援的版本 （如下 MAB 版本 2.0.9052 和 Azure 備份伺服器 update 1），就會出現此錯誤。 <br/>**建議的動作：**<br/> 在此情況下，您應該設定上述 hello 最小保留期限指定 （每日、 四週每週、 每月或一年安排每年的三週七天） 的保留期限 tooproceed 與原則相關的更新。 （選擇性） 慣用的方法是 tooupdate 備份代理程式和 Azure 備份伺服器 tooleverage 所有 hello 安全性更新。 |

## <a name="backup"></a>備份
| 作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 備份 | 複本不一致 | 您可以找到更多詳細的複本不一致的問題和相關的建議的 hello 原因[這裡](https://technet.microsoft.com/library/cc161593.aspx) <br> <ol><li> 如果是系統狀態/BMR 備份，請檢查受保護伺服器上是否已安裝 Windows Server Backup </li><li> 檢查相關的空間 DPM 存放裝置的問題上 hello DPM/MABS 伺服器集區，並配置存放裝置，視需要 </li><li> 檢查 hello hello hello 受保護伺服器上的磁碟區陰影複製服務狀態。 如果是在停用的狀態手動設定該 toostart 和 hello 伺服器上啟動 hello 服務。 然後返回 toohello DPM/MABS 主控台，並開始 hello 同步處理與一致性檢查。</li></ol>|
| 備份 | Hello 工作執行時發生未預期的錯誤、 hello 裝置尚未就緒 | **如果不適用於建議動作顯示 hello 產品中的 hello**， <br> <ol><li>Hello hello 保護群組中的項目上設定 hello 陰影複製儲存空間 toounlimited 並執行 hello 一致性檢查 <br></li> (或) <li>請嘗試刪除 hello 現有保護群組，並建立多個新的 – 每個個別項目在它的其中一個</li></ol> |
| 備份 | 如果您正在備份系統狀態，請確認是否有足夠的可用空間在 hello 受保護的電腦 toostore hello 系統狀態備份 | <ol><li>請確認該 hello WSB hello 受保護的電腦上已安裝</li><li>確認足夠的空間，會顯示 hello 受保護的電腦上，對於 hello 系統狀態： hello 最簡單的方式 toodo 這是 toogo toohello 受保護的電腦，開啟 WSB 並按一下 透過 hello 選取項目和選取 BMR。 hello UI 然後會告訴您這個需要多少空間時。 開啟 WSB -> 本機備份 -> 備份排程 -> 選取備份設定 -> 完整伺服器 (大小會顯示出來)。 使用此大小進行驗證。</li></ol>
| 備份 | 線上復原點建立失敗 | 如果 hello 錯誤訊息如下:"Windows Azure 備份代理程式已無法 toocreate hello 選取的快照集磁碟區 」，請嘗試增加複本和復原點磁碟區中的 hello 空間。
| 備份 | 線上復原點建立失敗 | 如果 hello 錯誤訊息如下:"hello Windows Azure Backup Agent 無法連線 toohello OBEngine 服務 」，請確認 OBEngine 存在 hello hello 電腦上執行的服務清單中的 hello。 如果 hello OBEngine 服務未執行使用 hello"net start OBEngine"命令 toostart hello OBEngine 服務。
| 備份 | 線上復原點建立失敗 | 如果 hello 錯誤訊息如下:"hello 加密複雜密碼，此伺服器未設定。 請設定加密複雜密碼」，請嘗試設定加密複雜密碼。 如果作業失敗， <br> <ol><li>檢查 hello 臨時位置是否存在與否。 具有名稱"ScratchLocation"hello 登錄 HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config 中所述的 hello 位置應存在。</li><li> 如果 hello 臨時位置存在，請嘗試重新註冊使用 hello 舊的複雜密碼。 **每當您設定加密複雜密碼時，請將它儲存在安全的位置**</li><ol>
| 備份 | BMR 的備份失敗 | BMR 大小很大，如果移動某些應用程式檔案 tooOS 磁碟機後再重試 |
| 備份 | 存取檔案/共用資料夾時發生錯誤 | 請嘗試修改 hello 防毒設定為建議[這裡](https://technet.microsoft.com/library/hh757911.aspx)|
| 備份 | VMware VM 的線上復原點建立作業失敗。 DPM 嘗試 tooget 變更追蹤資訊時發生錯誤，請從 VMware。 ErrorCode - FileFaultFault (ID 33621 ) |  1.在 VMWare 上的重設的 hello ctk hello 影響 Vm <br/> 檢查獨立磁碟不在 VMWare 上 <br/> 停止保護受影響的 hello Vm，然後重新保護與重新整理 按鈕 <br/> 針對受影響的 hello Vm 執行副本|


## <a name="change-passphrase"></a>變更複雜密碼
| 作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 變更複雜密碼 |輸入的安全性 PIN 碼不正確。 提供 hello 正確的安全性 pin 碼 toocomplete 這項作業。 |**原因：**<br/> 當您在執行重要作業 (例如變更複雜密碼) 時輸入無效或已到期的安全性 PIN 碼時，就會出現此錯誤。 <br/>**建議的動作：**<br/> toocomplete hello 作業，您必須輸入有效的安全性 pin 碼。 tooget hello 的 PIN，登入 tooAzure 入口網站並瀏覽 tooRecovery 服務保存庫 > 設定 > 內容 > 產生安全性 pin 碼。 使用這個 PIN toochange 複雜密碼。 |
| 變更複雜密碼 |作業失敗。 識別碼：120002 |**原因：**<br/>當安全性設定已啟用，toochange 複雜密碼再試一次，而您在位於不受支援版本，就會出現此錯誤。<br/>**建議的動作：**<br/> toochange 複雜密碼，您必須第一個更新備份代理程式 toominimum 版本最小 2.0.9052 和 Azure 備份伺服器 toominimum 更新 1，然後輸入有效的安全性 pin 碼。 tooget hello 的 PIN，登入 tooAzure 入口網站並瀏覽 tooRecovery 服務保存庫 > 設定 > 內容 > 產生安全性 pin 碼。 使用這個 PIN toochange 複雜密碼。 |


## <a name="configure-email-notifications"></a>設定電子郵件通知
| 作業 | 錯誤詳細資料 | 因應措施 |
| --- | --- | --- |
| 嘗試 tooset 使用 Office365 帳戶的電子郵件通知。 | 取得錯誤 ID：2013| **原因：**<br/> 嘗試 toouse Office 365 帳戶 <br/> **建議的動作：**<br/> hello 首先 tooensure 是 「 允許匿名轉送上接收連接器 」 為您的 DPM 伺服器已在 Exchange 上的設定。 以下是連結如何 tooconfigure 這： http://technet.microsoft.com/en-us/library/bb232021.aspx <br/> 如果您無法使用內部的 SMTP 轉送，而且需要使用 Office 365 伺服器 tooset，您可以設定 IIS toobe 轉送這個。 <br/> 您將需要 tooconfigure hello DPM 伺服器 toobe 無法 toorelay hello SMTP tooO365 使用 IIS https://technet.microsoft.com/en-us/library/aa995718(v=exchg.65).aspx toosetup IIS toorelay tooO365 <br/> 重要事項： 在步驟 3-> g-> 第二部分，是確定 toouseuser@domain.com格式並不網域 \ 使用者 <br/> 點，則 DPM toouse 為 SMTP 伺服器，連接埠 587 hello 本機伺服器名稱，然後 hello 應該來自 hello 電子郵件的使用者電子郵件。 <br/> hello 使用者名稱和密碼 hello DPM SMTP 設定 頁面上的應該 hello DPM 所在的網域中的網域帳戶。 <br/> 注意： 在變更 hello SMTP 伺服器位址，請將 hello 變更 toonew 設定、 關閉 hello 設定方塊然後再重新開啟 toobe 確定它會反映 hello 新值。  只要變更，並測試將不一定會 hello 新設定讓測試這種方式是最佳作法。 <br/> 在此程序期間的任何時間，您可以清除這些設定關閉 DPM 主控台，並編輯下列登錄機碼的 hello:<br/> HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Notification\ <br/> 刪除 SMTPPassword 和 SMTPUserName 索引鍵。 <br/> 您可以將它們加回去 hello UI 時再次啟動。
