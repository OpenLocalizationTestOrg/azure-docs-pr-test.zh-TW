---
title: "aaaAzure 備份伺服器保護系統狀態，並還原 toobare 金屬 |Microsoft 文件"
description: "使用 Azure 備份伺服器 tooback 系統狀態，並提供裸機復原 (BMR) 保護。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>將系統狀態備份和還原 toobare 金屬使用 Azure 備份伺服器

Azure 備份伺服器可備份系統狀態及提供裸機復原 (BMR) 保護。

*   **系統狀態備份**： 備份作業系統檔案，讓您可以在啟動電腦，但系統檔案和 hello 登錄遺失時復原。 系統狀態備份包含：
    * 網域成員：開機檔案、COM+ 類別註冊資料庫、登錄
    * 網域控制站：Windows Server Active Directory (NTDS)、開機檔案、 COM+ 類別註冊資料庫、登錄、系統磁碟區 (SYSVOL)
    * 執行叢集服務的電腦：叢集伺服器中繼資料
    * 執行憑證服務的電腦：憑證資料
* **裸機備份**：備份重要磁碟區上的作業系統檔案和所有資料 (使用者資料除外)。 根據定義，BMR 備份包括系統狀態備份。 當電腦無法啟動，而且您可以 toorecover 的所有項目，它會提供保護。

hello 下表摘要說明您可以備份及復原。 如需可使用系統狀態和 BMR 來加以保護之應用程式版本的詳細資訊，請參閱 [Azure 備份伺服器會備份哪些項目？](backup-mabs-protection-matrix.md)。

|備份|問題|從 Azure 備份伺服器的備份進行復原|從系統狀態的備份進行復原|BMR|
|----------|---------|---------------------------|------------------------------------|-------|
|**檔案資料**<br /><br />一般資料備份<br /><br />BMR/系統狀態備份|遺失檔案資料|Y|N|N|
|**檔案資料**<br /><br />Azure 備份伺服器的檔案資料備份<br /><br />BMR/系統狀態備份|作業系統遺失或損毀|N|Y|Y|
|**檔案資料**<br /><br />Azure 備份伺服器的檔案資料備份<br /><br />BMR/系統狀態備份|遺失伺服器 (資料磁碟區未受損)|N|N|Y|
|**檔案資料**<br /><br />Azure 備份伺服器的檔案資料備份<br /><br />BMR/系統狀態備份|遺失伺服器 (資料磁碟區也遺失)|Y|否|是 (先進行 BMR，接著進行所備份之檔案資料的一般復原)|
|**SharePoint 資料**：<br /><br />Azure 備份伺服器的伺服器陣列資料備份<br /><br />BMR/系統狀態備份|遺失網站、清單、清單項目、文件|Y|N|N|
|**SharePoint 資料**：<br /><br />Azure 備份伺服器的伺服器陣列資料備份<br /><br />BMR/系統狀態備份|作業系統遺失或損毀|N|Y|Y|
|**SharePoint 資料**：<br /><br />Azure 備份伺服器的伺服器陣列資料備份<br /><br />BMR/系統狀態備份|災害復原|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Azure 備份伺服器的 Hyper-V 主機或客體備份<br /><br />主機的 BMR/系統狀態備份|遺失 VM|Y|N|N|
|Hyper-V<br /><br />Azure 備份伺服器的 Hyper-V 主機或客體備份<br /><br />主機的 BMR/系統狀態備份|作業系統遺失或損毀|N|Y|Y|
|Hyper-V<br /><br />Azure 備份伺服器的 Hyper-V 主機或客體備份<br /><br />主機的 BMR/系統狀態備份|遺失 Hyper-V 主機 (VM 未受損)|N|N|Y|
|Hyper-V<br /><br />Azure 備份伺服器的 Hyper-V 主機或客體備份<br /><br />主機的 BMR/系統狀態備份|遺失 Hyper-V 主機 (VM 也遺失)|N|N|Y<br /><br />先進行 BMR，接著進行 Azure 備份伺服器一般復原|
|SQL Server/Exchange<br /><br />Azure 備份伺服器應用程式備份<br /><br />BMR/系統狀態備份|遺失應用程式資料|Y|N|N|
|SQL Server/Exchange<br /><br />Azure 備份伺服器應用程式備份<br /><br />BMR/系統狀態備份|作業系統遺失或損毀|N|y|Y|
|SQL Server/Exchange<br /><br />Azure 備份伺服器應用程式備份<br /><br />BMR/系統狀態備份|遺失伺服器 (資料庫/交易記錄未受損)|N|N|Y|
|SQL Server/Exchange<br /><br />Azure 備份伺服器應用程式備份<br /><br />BMR/系統狀態備份|遺失伺服器 (資料庫/交易記錄也遺失)|N|N|Y<br /><br />先進行 BMR 復原，接著進行 Azure 備份伺服器一般復原|

## <a name="how-system-state-backup-works"></a>系統狀態備份的運作方式

執行系統狀態備份，備份的伺服器通訊 hello 伺服器系統狀態的備份與 Windows Server Backup toorequest。 根據預設，備份伺服器和 Windows Server Backup 使用 hello 磁碟機有 hello 最多可用空間。 此磁碟機的相關資訊會儲存在 hello PSDataSourceConfig.xml 檔案。 這是 Windows Server Backup 使用備份的 hello 磁碟機。

您可以自訂 hello 備份伺服器使用 hello 系統狀態備份的磁碟機。 Hello 受保護伺服器上移 tooC:\Program Files\Microsoft 資料保護 Manager\MABS\Datasources。 開啟 hello PSDataSourceConfig.xml 檔案進行編輯。 變更 hello \<FilesToProtect\> hello 磁碟機代號的值。 儲存並關閉 hello 檔案。 如果保護群組設定的 hello 電腦 tooprotect hello 系統狀態時，請執行一致性檢查。 如果會產生警示，選取**修改保護群組**hello 警示與 hello 然後完成精靈 中。 然後，再執行一次一致性檢查。

請注意，是否 hello 保護伺服器是在叢集中，則可能的叢集磁碟會被選為 hello 與 hello 最多可用空間的磁碟機。 如果該磁碟機擁有權已交換的 tooanother 節點，執行系統狀態備份和 hello 磁碟機不能使用 hello 備份會失敗。 在此案例中，修改 PSDataSourceConfig.xml toopoint tooa 本機磁碟機。

接下來，Windows Server Backup 建立 hello 根目錄 hello 還原資料夾中名為 WindowsImageBackup 資料夾。 Windows Server Backup 建立 hello 備份時，所有的 hello 資料放在這個資料夾中。 Hello 備份完成時，hello 檔案是傳送的 toohello 備份伺服器的電腦。 請注意下列資訊的 hello:

* 這個資料夾及其內容未清除 hello 備份或傳送完成時。 這個 hello 最佳方式 toothink 是，hello 所保留的空間 hello 下一次備份完成。
* 每次進行備份時，會建立 hello 資料夾。 hello 日期和時間戳記會反映 hello 最後一次系統狀態備份的時間。

## <a name="bmr-backup"></a>BMR 備份

用於執行 BMR （包括系統狀態備份），hello 備份工作都被儲存直接 tooa 共用 hello 備份伺服器電腦上。 它不會儲存 tooa 資料夾 hello 受保護伺服器上。

備份伺服器呼叫 Windows Server Backup，並共用該 BMR 備份的 hello 複本磁碟區。 在此情況下，它不會告訴 hello 最多可用空間的 Windows Server Backup toouse hello 磁碟機。 相反地，它會使用所建立的 hello 共用 hello 作業。

Hello 備份完成時，hello 檔案是傳送的 toohello 備份伺服器的電腦。 記錄會儲存在 C:\Windows\Logs\WindowsServerBackup 中。

## <a name="prerequisites-and-limitations"></a>必要條件和限制

-   執行 Windows Server 2003 的電腦或執行用戶端作業系統的電腦皆不支援 BMR。

-   您無法保護 BMR 和系統狀態的 hello 相同不同保護群組中的電腦。

-   備份伺服器電腦無法讓自己受到 BMR 保護。

-   BMR 不支援短期保護 tootape （磁碟到磁帶或 D2T）。 支援長期的儲存體 tootape （磁碟到磁碟-到-磁帶或 D2D2T）。

-   BMR 保護，必須 hello 受保護的電腦上安裝 Windows Server Backup。

-   若是 BMR 保護，不同於系統狀態保護，備份伺服器沒有任何空間需求 hello 受保護的電腦上。 Windows Server Backup 直接傳輸備份 toohello 備份伺服器的電腦。 hello 備份傳輸作業不會出現在備份伺服器 hello**作業**檢視。

-   備份伺服器會保留 30 GB 的 hello 複本磁碟區上的空間，用於執行 BMR。 您可以變更這 hello**磁碟配置**hello 修改保護群組精靈 中，或使用 hello Get-datasourcediskallocation 和 Set-datasourcediskallocation PowerShell 指令程式的頁面。 Hello 復原點磁碟區 BMR 保護需要約 6 GB 以保留五天。
    * 請注意，您無法減少 hello 複本磁碟區大小 tooless 15 GB 以上。
    * 備份伺服器不會計算 hello hello BMR 資料來源大小。 它會假設所有伺服器都有 30 GB。 變更您環境中預期的 BMR 備份 hello 大小為基礎的 hello 值。 BMR 備份的 hello 大小可以大致上計算 hello 使用空間的總和為所有重要磁碟區上。 重要磁碟區 = 開機磁碟區 + 系統磁碟區 + 裝載系統狀態資料的磁碟區，例如 Active Directory。

-   如果您變更從系統狀態保護 tooBMR 保護，BMR 保護需要較少的空間上 hello*復原點磁碟區*。 不過，hello hello 磁碟區上的額外空間是無法回收。 您可以手動壓縮 hello hello 上的磁碟區大小**修改磁碟配置**hello 修改保護群組精靈或使用 hello Get-datasourcediskallocation 和 Set-datasourcediskallocation PowerShell 指令程式的頁面。

    如果您變更從系統狀態保護 tooBMR 保護，BMR 保護所需要更多空間 hello*複本磁碟區*。 hello 磁碟區會自動延伸。 如果您想 toochange hello 預設空間配置，請使用 hello Modify-diskallocation PowerShell cmdlet。

-   如果您從 BMR 保護 toosystem 狀態 」 保護變更時，您需要更多空間 hello 復原點磁碟區。 備份伺服器可能 tooautomatically 增加 hello 音量再試一次。 如果 hello 存放集區中沒有足夠的空間，就會發生錯誤。

    如果您從 BMR 保護 toosystem 狀態 」 保護變更時，您會需要 hello 受保護的電腦上的空間。 這是因為系統狀態保護會先將寫入 hello 複本 toohello 本機電腦，再將其傳輸 toohello 備份伺服器的電腦。

## <a name="before-you-begin"></a>開始之前

1.  **部署 Azure 備份伺服器**。 請確認您是否已正確地部署備份伺服器。 如需詳細資訊，請參閱：
    * [Azure 備份伺服器的系統需求](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [備份伺服器保護對照表](backup-mabs-protection-matrix.md)

2.  **設定儲存體**。 您可以將備份資料儲存在磁碟上，在磁帶上，並透過 Azure hello 雲端。 如需詳細資訊，請參閱[準備資料儲存體](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage)。

3.  **設定 hello 保護代理程式**。 您想 tooback hello 電腦上安裝 hello 保護代理程式。 如需詳細資訊，請參閱[hello DPM 保護代理程式部署](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent)。

## <a name="back-up-system-state-and-bare-metal"></a>備份系統狀態和裸機
設定保護群組，如[部署保護群組](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups)所述。 請注意，您無法保護 BMR 和系統狀態的 hello 相同不同群組中的電腦。 此外，當您選取 BMR 時，系統會自動啟用系統狀態。


1.  在 hello 備份伺服器系統管理員主控台中，選取 tooopen hello 建立新保護群組精靈**保護** > **動作** > **建立保護群組**。

2.  在 hello**選取保護群組類型**頁面上，選取**伺服器**，然後選取**下一步**。

3.  在 hello**選擇群組成員**頁面上，展開 hello 電腦，然後選取  **BMR**或**系統狀態**。

    請記住，您不能保護 hello 的 BMR 和系統狀態不同群組中的同一部電腦。 此外，當您選取 BMR 時，系統會自動啟用系統狀態。 如需詳細資訊，請參閱[部署保護群組](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups)。

4.  在 hello**選擇資料保護方式**頁面上，選取您要如何 toohandle 短期和長期備份。 短期備份永遠都會 toodisk 第一次，並可 hello 從 hello 磁碟 toohello Azure 備份雲端藉由使用 Azure 備份 （短期或長期）。 替代 toolong 詞彙備份 toohello 雲端是 tooset 長期備份 tooa 獨立磁帶裝置或磁帶媒體櫃已連接 tooBackup 伺服器上。

5.  在 hello**選取短期目標**頁面上，選取您想 tooback tooshort 詞彙在磁碟上的存放裝置的方式：
    1. 如**保留範圍**，選取您想 tookeep hello 資料磁碟上的時間長度。 
    2. 如**同步處理頻率**，選取您想 toorun 增量備份 toodisk 的頻率。 如果您不想 tooset 備份的時間間隔，您可以檢查 hello**恰好在復原點之前**選項。 備份伺服器將會在每個復原點的排程時間前一刻執行快速而完整的備份。

6.  如果您想 toostore 磁帶上的資料進行長期儲存，在 hello**指定長期目標**頁面上，選取您想 tookeep 磁帶資料 （1-99 年） 的時間長度。 
    1. 如**備份頻率**，選取頻率備份 tootape 應該執行。 hello 頻率是以您所選取的 hello 保留範圍為基礎：
        * 當 hello 保留範圍是 1-99 年時，您可以選取每日、 每週、 每兩週、 每月、 每季、 半年或每年備份 toooccur。
        * 當 hello 保留範圍是 1-11 個月時，您可以選取每日、 每週、 每兩週或每月備份 toooccur。
        * 當 hello 保留範圍是 1-4 週時，您可以選取每日或每週備份 toooccur。

    2. 在 hello**選取磁帶和媒體櫃詳細資料**頁面上，選取 hello 磁帶和媒體櫃 toouse，以及資料是否應該壓縮並加密。

7.  在 hello**檢閱磁碟配置**頁面上，檢閱 hello 存放集區磁碟空間配置的 hello 保護群組。

    1. **資料大小總計**是 hello 要 tooback hello 資料大小。
    2. **在 Azure 備份伺服器上佈建的磁碟空間 toobe** hello 空間 hello 保護群組建議備份伺服器。 備份伺服器選擇 hello 理想備份磁碟區根據 hello 設定。 不過，您可以編輯中的 hello 備份磁碟區選擇**磁碟配置詳細資料**。 
    3. 針對工作負載，在 hello 下拉功能表中，選取 hello 慣用儲存體。 編輯變更 hello 值**總儲存體**和**可用的儲存體**在 hello**可用的磁碟儲存體**窗格。 Underprovisioned 的空間是 hello 備份伺服器，建議您將加入 toohello tooensure smooth 備份磁碟區的儲存體的數量。

8.  在 hello**選擇複本建立方式**頁面上，選取您想 toohandle hello 完整的資料初始複寫的方式。 如果您選擇 tooreplicate hello 網路上時，我們建議您選擇離峰時間。 對於大量資料或網路狀況不佳，請考慮複寫 hello 資料離線使用卸除式媒體。

9. 在 hello**選擇一致性檢查選項**頁面上，選取您想 tooautomate 一致性檢查的方式。 只有當複本資料變得不一致，或根據排程時您可以選擇指定 toorun 檢查。 如果您不想 tooconfigure 自動一致性檢查，您可以隨時執行手動檢查。 手動檢查，在 hello toorun**保護**區域 hello 備份伺服器系統管理員主控台中，以滑鼠右鍵按一下 hello 保護群組，然後選取**執行一致性檢查**。

10. 如果您已選取 tooback toohello 雲端上的使用 Azure Backup，在 hello**指定線上保護資料**頁面上，確定您選取您想要向上 tooAzure tooback hello 工作負載。

11. 在 hello**指定線上備份排程**頁面上，選取增量備份頻率 tooAzure 就會發生。 您可以排程備份 toorun 每日、 週、 月和年，並選取 hello 日期和時間應該在其中執行。 向上一天 tootwice 才能進行備份。 每次執行備份資料的復原點是在 Azure 中從建立 hello hello hello 備份伺服器磁碟上儲存的備份資料的副本。

12. 在 hello**指定線上保留原則**頁面上，選取 hello 從 hello 每日、 每週、 每月和每年執行備份所建立的復原點保留在 Azure 中的方式。

13. 在 hello**選擇線上複寫**頁面上，選取 hello 完整的資料初始複寫的進行方式。 您可以透過 hello 網路複寫，或執行離線備份 （離線植入）。 離線備份會使用 hello Azure 匯入功能。 如需詳細資訊，請參閱 [Azure Backup 中的離線備份工作流程](backup-azure-backup-import-export.md)。

14. 在 hello**摘要**頁面上，檢閱您的設定。 選取後**建立群組**，hello 資料初始複寫，就會發生。 當資料複寫完成時，在 [hello**狀態**] 頁面上，hello 保護群組狀態是**確定**。 接著會備份每 hello 保護群組設定。

## <a name="recover-system-state-or-bmr"></a>復原系統狀態或 BMR
您可以復原 BMR 或系統狀態 tooa 網路位置。 如果您已備份 BMR，請使用 Windows 修復環境 (WinRE) toostart 系統並將它連接 toohello 網路。 然後，使用 Windows Server Backup toorecover hello 網路位置。 如果您已備份系統狀態，只要使用 Windows Server Backup toorecover hello 網路位置。

### <a name="restore-bmr"></a>還原 BMR
Hello 備份伺服器電腦上執行復原：

1.  在 hello**復原**窗格中，尋找您想 toorecover，，然後選取 hello 電腦**裸機復原**。

2.  可用的復原點會以粗體表示 hello 行事曆上。 選取您想 toouse hello 復原點的 hello 日期和時間。

3.  在 hello**選取復原類型**頁面上，選取**複製 tooa 網路資料夾。**

4.  在 hello**指定目的地**頁面上，選取您想要 toocopy hello 資料。 請記住該 hello 選的目的地 toohave 需要足夠的空間。 我們建議您建立新的資料夾。

5.  在 hello**指定復原選項**頁面上，選取 hello 安全性設定 tooapply。 然後，選取您要讓 toouse 存放區域網路 (SAN) 為基礎的硬體快照集，更快速的復原。 (這是一個選項，只有當您擁有可用，此功能的 SAN 和 hello 能力 toocreate 並分割複本 toomake 它可寫入。 此外，hello 受保護的電腦和備份伺服器電腦必須連線的 toohello 相同的網路。)

6.  設定通知選項。 在 hello**確認**頁面上，選取**復原**。

設定 hello 共用位置：

1.  在 hello 還原位置，移 toohello hello 備份的資料夾。

2.  共用 hello 的資料夾 WindowsImageBackup 上的一層，使 hello hello 共用資料夾的根目錄 hello WindowsImageBackup 資料夾。 如果不這麼做，還原將找不到 hello 備份。 使用 Windows 修復環境 (WinRE) tooconnect，您必須可以存取在 WinRE 中與 hello 正確的 IP 位址和認證的共用。

Hello 系統還原：

1.  啟動 hello 電腦，您想要還原的 hello 系統使用 hello Windows DVD toorestore hello 映像。

2.  在 hello 第一個頁面上，確認語言及地區設定。 在 hello**安裝**頁面上，選取**修復您的電腦**。

3.  在 hello**系統修復選項**頁面上，選取**使用您稍早建立的系統映像將電腦還原**。

4.  在 hello**選取系統映像備份**頁面上，選取**選取系統映像** > **進階** > **系統的搜尋hello 網路上的映像**。 如果出現警告，請選取 [是]。 移 toohello 共用路徑、 輸入 hello 認證，然後選取 hello 復原點。 此動作會掃描出該復原點中可用的特定備份。 選取您想 toouse hello 復原點。

5.  在 hello**選擇如何 toorestore hello 備份**頁面上，選取**格式化並重新分割磁碟**。 在 hello 下一個頁面上，確認設定。 

6.  toobegin hello 還原中，選取**完成**。 系統需要重新啟動。

### <a name="restore-system-state"></a>還原系統狀態

在備份伺服器中執行復原：

1.  在 [hello**復原**] 窗格中，尋找您想 toorecover，，然後選取 hello 電腦**裸機復原**。

2.  可用的復原點會以粗體表示 hello 行事曆上。 選取您想 toouse hello 復原點的 hello 日期和時間。

3.  在 hello**選取復原類型**頁面上，選取**複製 tooa 網路資料夾**。

4.  在 hello**指定目的地**頁面上，選取您要 toocopy hello 資料。 請記住該 hello 選的目的地需要足夠的空間。 我們建議您建立新的資料夾。

5.  在 hello**指定復原選項**頁面上，選取 hello 安全性設定 tooapply。 然後，選取您想要更快速的復原 toouse SAN 型硬體快照集。 (這是一個選項，只有當您擁有這項功能的 SAN 和 hello 能力 toocreate 並分割複本 toomake 它可寫入。 此外，hello 受保護的電腦和備份伺服器的伺服器必須連接的 toohello 相同的網路。)

6.  設定通知選項。 在 hello**確認**頁面上，選取**復原**。

執行 Windows Server Backup：

1.  選取 [動作] > [復原] > [此伺服器] > [下一步]。

2.  選取**另一部伺服器**，選取 hello**指定位置類型**頁面，然後再選取**遠端共用資料夾**。 輸入 hello 路徑 toohello 資料夾含有 hello 復原點。

3.  在 hello**選取復原類型**頁面上，選取**系統狀態**。 

4. 在 hello**選取系統狀態復原的位置**頁面上，選取**原始位置**。

5.  在 hello**確認**頁面上，選取**復原**。 Hello 還原之後重新啟動伺服器 hello。

6.  您也可以在命令提示字元執行 hello 系統狀態還原。 toodo，啟動 Windows Server Backup 想 toorecover hello 電腦上。 tooget hello 版本識別碼，在命令提示字元中，輸入：```wbadmin get versions -backuptarget \<servername\sharename\>```

    使用 hello 版本識別項 toostart hello 系統狀態還原。 在 hello 命令提示字元中輸入：```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    確認您想 toostart hello 復原。 您可以看到 hello 命令提示字元 視窗中的 hello 程序。 系統會建立還原記錄。 Hello 還原之後重新啟動伺服器 hello。

