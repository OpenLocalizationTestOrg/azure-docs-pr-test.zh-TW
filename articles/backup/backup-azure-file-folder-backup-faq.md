---
title: "aaaAzure 備份代理程式常見問題集 |Microsoft 文件"
description: "關於回答 toocommon 問題： 如何 hello Azure 備份代理程式的運作方式、 備份和保留的限制。"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "備份和災害復原; 備份服務"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Hello Azure 備份代理程式的相關問題
這篇文章有解答 toocommon 問題 toohelp 快速了解 hello Azure 備份代理程式元件。 在某些 hello 解答，會有連結 toohello 文件具有完整的資訊。 您也可以張貼疑問 hello Azure 備份服務在 hello[討論區論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)。

## <a name="configure-backup"></a>設定備份
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>哪裡可以下載最新 Azure Backup agent hello？ <br/>
您可以下載 hello 最新的代理程式來備份 Windows Server、 System Center DPM 或 Windows 用戶端，從[這裡](http://aka.ms/azurebackup_agent)。 如果您想 tooback 的虛擬機器，請使用 hello VM 代理程式 」 （會自動安裝 hello 適當擴充功能）。 hello VM 代理程式已存在於建立 hello Azure 組件庫的虛擬機器上。

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>設定 hello Azure Backup agent，我提示的 tooenter hello 保存庫認證。 保存庫認證是否過期？
是，hello 保存庫認證會在 48 小時後過期。 如果 hello 檔案到期，登入 toohello Azure 入口網站並下載 hello 保存庫認證檔案從您的保存庫。

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>我可以從何種類型的磁碟機備份檔案和資料夾？ <br/>
您無法備份下列磁碟區的磁碟機/hello:

* 卸除式媒體：所有備份項目來源必須報告為固定式。
* 唯讀磁碟區： hello 磁碟區必須可供 hello 磁碟區陰影複製服務 (VSS) toofunction 寫入。
* 離線的磁碟區： hello 磁碟區必須在線上，VSS toofunction。
* 網路共用： hello 磁碟區必須是本機 toohello 伺服器 toobe 使用線上備份執行備份。
* 受 Bitlocker 保護的磁碟區： hello 磁碟區必須先解除鎖定 hello 備份可能會發生。
* 檔案系統識別： NTFS 是 hello 支援唯一的檔案系統。

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>我可以從伺服器備份何種類型的檔案和資料夾？<br/>
支援下列類型的 hello:

* 已加密
* 已壓縮
* 疏鬆
* 已壓縮 + 疏鬆
* 永久連結：不支援並略過
* 重新分析點：不支援並略過
* 已加密 + 疏鬆：不支援並略過
* 已壓縮資料流：不支援並略過
* 疏鬆資料流：不支援並略過

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>可以安裝 hello Azure 備份代理程式已經 hello Azure 備份服務使用 hello VM 延伸模組所支援的 Azure VM 上嗎？ <br/>
當然。 Azure 備份提供 VM 層級備份就 Azure vm 使用 hello VM 延伸模組。 hello 客體 Windows 作業系統上 tooprotect 檔案和資料夾安裝 hello Azure Backup agent 在 hello 客體 Windows 作業系統上。

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>可以安裝 hello Azure 備份代理程式上的 Azure VM tooback 檔案及資料夾上 hello Azure VM 所提供的暫存儲存體嗎？ <br/>
是。 Hello 客體 Windows 作業系統上安裝 hello Azure 備份代理程式和備份檔案和資料夾 tootemporary 儲存體。 一旦抹除暫存儲存體資料，備份工作就會失敗。此外，如果 hello 暫存資料都已刪除，您可以只還原 toonon 揮發性儲存體。

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>Hello hello 快取資料夾的最低大小需求為何？ <br/>
hello hello 快取資料夾大小會決定 hello 要備份的資料量。 快取資料夾應該是空間的 5 %hello 所需來儲存資料。

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>如何註冊我的伺服器 tooanother 資料中心？<br/>
備份資料會傳送 hello 保存庫 toowhich 已註冊的 toohello 資料中心。 hello 最簡單方式 toochange hello datacenter toouninstall hello 代理程式並重新安裝 hello 代理程式並註冊 tooa 新的保存庫所屬 toodesired 資料中心。

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Hello Azure 備份代理程式工作使用 Windows Server 2012 重複資料刪除的伺服器嗎？ <br/>
是。 準備 hello 備份作業時，hello 代理程式服務將重複資料刪除的 hello 資料 toonormal 資料轉換。 然後最佳化用於備份的 hello 資料、 加密 hello 資料，並接著會傳送 hello 加密資料 toohello 線上備份服務。

## <a name="backup"></a>備份
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>如何變更 hello 快取位置指定 hello Azure 備份代理程式？<br/>
使用下列清單 toochange hello 快取位置中的 hello。

1. 停止 hello 備份引擎藉由執行下列命令，在提升權限的命令提示字元中的 hello:

    ```PS C:\> Net stop obengine``` 
  
2. 不會移動 hello 檔案。 相反地，複製 hello 快取空間資料夾 tooa 不同的磁碟機具有足夠空間。 確認備份使用新的快取空間 hello hello 之後，就可以移除 hello 原始的快取空間。
3. 更新下列登錄項目與 hello 路徑 toohello 新快取空間資料夾 hello。<br/>

    | 登錄路徑 | 登錄金鑰 | 值 |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*「新的快取資料夾位置」* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*「新的快取資料夾位置」* |

4. 重新啟動 hello 備份引擎，藉由執行下列命令，在提升權限的命令提示字元中的 hello:

    ```PS C:\> Net start obengine```

一旦建立 hello 備份順利完成在 hello 新快取位置中，您可以移除 hello 原始的快取資料夾。


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>我可以在放置 hello Azure Backup Agent toowork 如預期般的 hello 快取資料夾？<br/>
hello hello 快取資料夾的下列位置不建議使用：

* 網路共用或卸除式媒體： hello 快取資料夾必須是本機 toohello 伺服器需要使用線上備份進行備份。 不支援網路位置或卸除式媒體，例如 USB 磁碟機。
* 離線的磁碟區： hello 快取資料夾必須在線上，預期的備份使用 Azure Backup Agent。

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>有不支援的任何屬性的 hello 快取資料夾嗎？<br/>
hello 下列屬性或其組合不支援為 hello 快取資料夾：

* 已加密
* 已刪除重複資料
* 已壓縮
* 疏鬆
* 重新分析點

hello 快取資料夾和 hello 中繼資料 VHD 並沒有 hello hello Azure 備份代理程式的必要屬性。

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>有一個方式 tooadjust hello 頻寬總量 hello 備份服務使用嗎？<br/>
  是，使用 hello**變更屬性**hello Backup Agent tooadjust 頻寬的選項。 您可以調整 hello 成長的頻寬和 hello 的時間，當您使用的頻寬量。 如需逐步指示，請參閱**[啟用網路節流](backup-configure-vault.md#enable-network-throttling)**。

## <a name="manage-backups"></a>管理備份
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>如果我重新命名 Windows 伺服器的備份資料 tooAzure，怎樣？<br/>
當您重新命名伺服器時，所有目前設定的備份都會停止。
Hello 備份保存庫中註冊 hello 伺服器 hello 新名稱。 Hello 保存庫中註冊 hello 新名稱，hello 的第一個備份作業時，*完整*備份。 如果您需要 toorecover 資料備份 toohello 保存庫與 hello 舊的伺服器名稱，請使用 hello [**另一部伺服器**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine)選項在 hello**復原資料**精靈。

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>可以使用 Azure 備份代理程式的備份原則中指定的 hello 最大的檔案路徑長度為何？ <br/>
Azure 備份代理程式依存於 NTFS。 hello [filepath 長度規格會受到 hello Windows API](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths)。 如果您想要 tooprotect hello 檔案的檔案路徑長度超過所允許的 hello Windows API，備份 hello 父資料夾或 hello 磁碟機。  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>使用 Azure 備份代理程式時，Azure 備份原則的檔案路徑中允許哪些字元？ <br>
 Azure 備份代理程式依存於 NTFS。 它可讓 [NTFS 支援的字元](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) 成為檔案規格的一部分。 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>我收到 hello 警告時，「 Azure 備份尚未設定此伺服器 」，即使設定備份原則 <br/>
Hello hello 本機伺服器上儲存的備份排程設定不的 hello 與相同 hello hello 備份保存庫中儲存的設定時，就會發生這個警告。 當伺服器 hello 或 hello 設定已復原的 tooa 已知良好的狀態時，hello 備份排程可能會失去同步處理。 如果您收到這個警告，[重新設定備份原則的 hello](backup-azure-manage-windows-server.md)然後**立即執行備份**tooresynchronize hello 本機伺服器與 Azure。
