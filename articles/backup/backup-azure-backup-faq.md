---
title: "aaaAzure 備份常見問題集 |Microsoft 文件"
description: "回答 toocommon 問題相關： Azure Backup 功能，包括復原服務保存庫，它可以將備份、 它的運作方式、 加密，與限制。 "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份和災害復原; 備份服務"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Hello Azure 備份服務有關的問題
這篇文章有解答 toocommon 問題 toohelp 快速了解 hello Azure 備份的元件。 在某些 hello 解答，會有連結 toohello 文件具有完整的資訊。 您也可以按一下 Azure 備份的相關詢問問題**註解**（toohello 右）。 註解會出現在這篇文章的 hello 底部。 需要的 toocomment Livefyre 帳戶。 您也可以張貼疑問 hello Azure 備份服務在 hello[討論區論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)。

tooquickly 掃描 hello 章節，在本文中，使用在 hello 連結 toohello 右側，**本文**。


## <a name="recovery-services-vault"></a>復原服務保存庫

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>是否有任何可以在每個 Azure 訂用帳戶中建立的保存庫的 hello 數目限制？ <br/>
是。 自 2016 年 9 月起，您可以為每個訂用帳戶建立 25 個復原服務或保存庫。 您可以將每個 Azure 備份的每個訂閱的支援區域的保存庫，建立 too25 復原服務。 如果您需要其他保存庫，請建立其他訂用帳戶。

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>有的可以針對每個保存庫註冊的伺服器/機器 hello 數目的限制嗎？ <br/>
是，您可以註冊一個保存庫 too50 電腦。 Azure IaaS 虛擬機器，hello 限制為 200 的 Vm，每個保存庫。 如果您需要 tooregister 更多電腦，建立另一個保存庫。

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>如果我的組織有一個備份保存庫，如何在還原資料時隔離某一部伺服器與另一部伺服器的資料？<br/>
所有伺服器，可以復原保存庫相同的已註冊的 toohello 都 hello 其他伺服器所備份的資料*使用都 hello 同一組複雜密碼*。 如果您有伺服器的備份資料想 tooisolate 來自您組織中其他伺服器，這些伺服器使用指定的複雜密碼。 例如，人力資源伺服器可能使用一組加密複雜密碼，而會計伺服器使用另一組，並且儲存體伺服器使用第三組。

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>我可以在訂用帳戶之間「移轉」備份資料或保存庫嗎？ <br/>
否。 hello 保存庫建立訂用帳戶層級，而且不能重新指派的 tooanother 訂用帳戶，一旦建立之後。

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>復原服務保存庫是以 Resource Manager 為基礎。 備份保存庫 (傳統模式) 是否仍受支援？ <br/>
所有現有的備份保存庫中 hello[傳統入口網站](https://manage.windowsazure.com)繼續 toobe 支援。 不過，您無法再使用 hello 傳統入口網站 toodeploy 新備份保存庫。 Microsoft 建議所有部署使用復原服務保存庫，因為未來的增強功能 tooRecovery 服務保存庫，只會套用。 如果您嘗試 toocreate hello 傳統入口網站中的備份保存庫，您將會重新導向的 toohello [Azure 入口網站](https://portal.azure.com)。

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>可以移轉備份保存庫 tooa 復原服務保存庫嗎？ <br/>
不幸的是不可以，您無法移轉復原服務保存庫備份保存庫 tooa hello 內容。 我們正著手新增這項功能，但目前仍未提供。

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>我已在備份保存庫中備份我的傳統 VM。 我的 Vm 將從傳統模式 tooResource 管理員模式移轉和復原服務保存庫來保護它們？
當您移動 hello VM 從傳統 tooResource 管理員模式下，傳統備份保存庫中的 VM 復原點不自動移轉 tooa 復原服務保存庫。 請遵循這些步驟 tootransfer 您 VM 的備份：

1. 在 hello 備份保存庫中，移 toohello**受保護項目**索引標籤並選取 hello VM。 按一下[停止保護](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)。 讓 [刪除相關聯的備份資料] 選項保持 [未核取] 狀態。
2. 刪除 hello VM hello 快照集備份/擴充功能。
3. 從傳統模式 tooResource 管理員模式移轉 hello 虛擬機器。 請確定 hello 儲存體和網路資訊也是對應的 toohello 虛擬機器移轉 tooResource 管理員模式。
4. 建立復原服務保存庫和設定虛擬機器使用的備份在 hello 移轉**備份**在保存庫儀表板頂端的動作。 詳細資訊，在備份 VM tooa 復原服務保存庫，請參閱 hello 文章[保護與復原服務保存庫的 Azure Vm](backup-azure-vms-first-look-arm.md)。

## <a name="azure-backup-agent"></a>Azure 備份代理程式
問題的詳細清單會出現在 [Azure 檔案資料夾備份的常見問題集](backup-azure-file-folder-backup-faq.md)

## <a name="azure-vm-backup"></a>Azure VM 備份
問題的詳細清單會出現在 [Azure VM 備份的常見問題集](backup-azure-vm-backup-faq.md)

## <a name="back-up-vmware-servers"></a>備份到 VMware 伺服器

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>我可以備份 VMware vCenter 伺服器 tooAzure 嗎？

是。 您可以使用 Azure 備份伺服器 tooback VMware vCenter 和 ESXi tooAzure。 Hello 支援 VMware 版本上的資訊，請參閱 hello 文章[Azure 備份伺服器保護矩陣](backup-mabs-protection-matrix.md)。 如需逐步指示，請參閱[VMware 伺服器使用 Azure 備份伺服器 tooback](backup-azure-backup-server-vmware.md)。


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Azure 備份伺服器和 System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>我可以使用 Azure 備份伺服器 toocreate 裸機復原 (BMR) 備份實體伺服器？ <br/>
是。

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>可以註冊我的 DPM 伺服器 toomultiple 保存庫？ <br/>
否。 DPM 或 MABS 伺服器可以是已註冊的 tooonly 一個保存庫。

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>支援的 System Center Data Protection Manager 版本為何？ <br/>
我們建議您安裝 hello[最新](http://aka.ms/azurebackup_agent)hello 最新更新彙總套件 (UR) 的 System Center Data Protection Manager (DPM) 上的 Azure 備份代理程式。 2016 年 8 月更新彙總套件 11 為 hello 最新的更新。

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>我已安裝 Azure Backup agent tooprotect 我的檔案和資料夾。 可以使用 Azure 備份代理程式 tooprotect 在內部部署應用程式/VM 工作負載 tooAzure 現在安裝 System Center DPM toowork 嗎？ <br/>
toouse Azure Backup 與 System Center Data Protection Manager (DPM)，第一次安裝 DPM，然後再安裝 Azure Backup agent。 依此順序安裝 hello Azure Backup 元件，可確保 hello Azure Backup agent 可搭配 DPM。 不建議您安裝的 hello Azure 備份代理程式後再安裝 DPM 或支援。


## <a name="how-azure-backup-works"></a>Azure 備份的運作方式
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>一旦啟動後取消備份工作，如果是 hello 傳輸備份資料刪除嗎？ <br/>
否。 傳送 hello 保存庫，到 hello 備份工作已取消之前, 的所有資料會都保持在 hello 保存庫。 Azure Backup 採用檢查點機制 toooccasionally 新增檢查點期間 toohello 備份資料 hello 備份。 Hello 備份資料中有檢查點，因為 hello 下一個備份程序可以驗證 hello 檔案的完整性，hello。 hello 的下一個備份作業會累加 toohello 先前備份的資料。 增量備份只會傳送新增或變更資料，相當於 toobetter 頻寬使用量。

如果您取消 Azure VM 的備份工作，則會忽略任何傳輸的資料。 hello 的下一個備份作業會從 hello 最後一個成功備份作業中傳送增量資料。

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>備份作業可排程的時間和次數是否有限制？<br/>
是。 您可以在 Windows Server 或向上 toothree 時間 / 日期的 Windows 工作站上執行備份作業。 您可以備份作業上執行 System Center DPM 向上 tootwice 一天。 您一天可以執行 IaaS VM 的備份作業一次。 您可以使用 Windows Server 或 Windows 工作站 toospecify 排程原則的 hello 每日或每週排程。 使用 System Center DPM 時，您可以指定每日、每週、每月和每年排程。

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>為什麼會小於 hello 資料我的備份復原服務保存庫的 hello 傳輸資料 toohello hello 大小？<br/>
 從 Azure Backup Agent SCDPM 或 Azure 備份伺服器，備份的所有 hello 資料壓縮，然後加密後再傳輸。 一旦套用 hello 壓縮和加密時，hello hello 備份保存庫中的資料會是較小的 30-40%。

## <a name="what-can-i-back-up"></a>我可以備份什麼
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Azure 備份支援哪些作業系統？ <br/>
Azure Backup 支援下列作業系統的備份清單的 hello： 檔案與資料夾，以及工作負載的應用程式使用 Azure 備份伺服器和 System Center Data Protection Manager (DPM) 保護。

| 作業系統 | 平台 | SKU |
|:--- | --- |:--- |
| Windows 8 和最新的 SP |64 位元 |Enterprise、Pro |
| Windows 7 和最新的 SP |64 位元 |Ultimate、Enterprise、Professional、Home Premium、Home Basic、Starter |
| Windows 8.1 和最新的 SP |64 位元 |Enterprise、Pro |
| Windows 10 |64 位元 |企業版、專業版、家用版 |
| Windows Server 2016 |64 位元 |Standard、Datacenter、Essentials |
| Windows Server 2012 R2 和最新的 SP |64 位元 |Standard、Datacenter、Foundation |
| Windows Server 2012 和最新的 SP |64 位元 |Datacenter、Foundation、Standard |
| Windows Storage Server 2016 和最新的 SP |64 位元 |Standard、Workgroup | 
| Windows Storage Server 2012 R2 和最新的 SP |64 位元 |Standard、Workgroup |
| Windows Storage Server 2012 和最新的 SP |64 位元 |Standard、Workgroup |
| Windows Server 2012 R2 和最新的 SP |64 位元 |Essential |
| Windows Server 2008 R2 SP1 |64 位元 |Standard、Enterprise、Datacenter、Foundation |
| Windows Server 2008 SP2 |64 位元 |Standard、Enterprise、Datacenter、Foundation |

**Azure VM 備份：**

* **Linux**：Azure 備份支援 [Azure 所背書的散發套件清單](../virtual-machines/linux/endorsed-distros.md) ，但核心作業系統 Linux 除外。  其他提到-您-擁有-Linux 散發套件也可能會運作，只要 hello VM 代理程式位於 hello 虛擬機器和 Python 存在的支援。
* **Windows Server**：不支援比 Windows Server 2008 R2 更舊的版本。


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>每個要備份的資料來源的 hello 大小是否有限制？ <br/>
的資料可以備份 tooa 保存庫的 hello 量沒有限制。 Azure 備份限制 hello hello 資料來源的大小上限，不過，這些限制很大。 從 2015 年 8 月開始 hello hello 支援作業系統的資料來源的大小上限為：

| S.No | 作業系統 | 資料來源的大小上限 |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 或更新版本 |54,400 GB |
| 2 |Windows 8 或更新版本 |54,400 GB |
| 3 |Windows Server 2008、Windows Server 2008 R2 |1700 GB |
| 4 |Windows 7 |1700 GB |

hello 下表說明如何判斷每個資料來源的大小。

| 資料來源 | 詳細資料 |
|:---:|:--- |
| 磁碟區 |正在從伺服器或用戶端電腦的單一磁碟區備份的資料量 hello |
| Hyper-V 虛擬機器 |資料的所有 hello Vhd hello 虛擬機器進行備份的總和 |
| Microsoft SQL Server 資料庫 |要備份的單一 SQL 資料庫大小的大小 |
| Microsoft SharePoint |要備份在 SharePoint 伺服陣列中的 hello 內容和組態資料庫的總和 |
| Microsoft Exchange |在要備份的 Exchange Server 中所有 Exchange 資料庫的總和 |
| BMR/系統狀態 |每個個別的 BMR 或系統狀態備份的 hello 機器的複本 |

Azure VM 備份的每個 VM 最多可以有 too16 資料磁碟搭配每個資料磁碟大小 1023 GB 或更少。 

## <a name="retention-policy-and-recovery-points"></a>保留原則和復原點
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>是否有適用於 DPM 的 hello 保留原則與 Windows 伺服器/用戶端之間的差 （亦即，DPM 不在 「 Windows 伺服器 」）？<br/>
否，DPM 和 Windows Server/用戶端均有每日、每週、每月和每年保留原則。

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>我可以選擇性設定保留原則，例如設定每週和每日，但不包含每年和每月嗎？<br/>
是，hello Azure 備份保留結構可讓您 toohave 定義 hello 保留原則，根據您的需求的完整彈性。

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>我可以在下午 6:00「排程備份」，並在不同的時間指定「保留原則」嗎？<br/>
不可以。 保留原則僅能套用在復原點上。 在下列映像的 hello，hello 保留原則被指定在 12 am 和下午 6 點間取得的備份。 <br/>

![排程備份和保留](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>如果是長時間，備份會保留下來，花費更多時間 toorecover 較舊的資料點？ <br/>
否-hello 時間 toorecover hello 最舊或 hello 最新的點是 hello 相同。 每個復原點的功能就像一個完整的復原點。

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>如果每個復原點是類似完整的點，它確實會影響 hello 總計計費備份儲存體？<br/>
典型的長期保留復原點產品會將備份資料儲存為完整的復原點。 hello 完整點是儲存體*效率不佳*但更容易更快速的 toorestore 和。 增量備份是儲存體*有效率*但要求您 toorestore 鏈結的資料，而這會影響復原時間。 Azure 備份儲存體架構可讓您 hello 兩者之優點的最佳的方式儲存對於快速還原資料，以及產生低儲存體成本。 此資料儲存方法可確保有效率地使用您的輸入和輸出頻寬。 這兩個 hello 一段時間的資料儲存體和 hello 所需 toorecover hello 資料時，會保留 tooa 最小。 深入了解[增量備份](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/)有何效用。

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>有可建立復原點的 hello 數目的限制嗎？<br/>
您可以建立註冊 too9999 復原點，每個受保護的執行個體。 電腦、 伺服器 （實體或虛擬） 或總資料 tooAzure 設定的工作負載 tooback 受保護的執行個體。 如需詳細資訊，請參閱的 hello 說明[備份和保留](./backup-introduction-to-azure-backup.md#backup-and-retention)，和[什麼是受保護的執行個體](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)？

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>備份 tooAzure hello 資料可以執行多少復原？<br/>
從 Azure 備份復原的 hello 數目沒有限制。

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>還原資料時，請勿我支付 hello 輸出流量從 Azure 嗎？ <br/>
否。 您的復原可以使用，且您不需付費 hello 輸出流量。

## <a name="azure-backup-encryption"></a>Azure 備份加密
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>傳送加密的 tooAzure hello 資料嗎？ <br/>
是。 Hello 內部 SCDPM/伺服器/用戶端電腦上使用 AES256 加密資料，並透過安全的 HTTPS 連結傳送 hello 資料。

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>位於 Azure 也以加密方式 hello 備份資料？<br/>
是。 hello 資料傳送 tooAzure 仍會維持加密 （靜止）。 Microsoft 不會解密 hello 在任何時間點的備份資料。 備份時的 Azure VM，Azure Backup 會依賴 hello 虛擬機器的加密。 例如，如果使用 Azure 磁碟加密或一些其他加密技術來加密您的 VM，Azure Backup 會使用該加密 toosecure 您的資料。

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>什麼是加密金鑰的 hello 最小長度使用 tooencrypt 備份資料？ <br/>
hello 加密金鑰應該至少 16 個字元，當您使用 Azure 備份代理程式。 對於 Azure Vm 中沒有 Azure KeyVault 所使用的索引鍵的任何限制 toolength。 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>如果我找不到 hello 加密金鑰會怎樣？ 我可以復原 hello 資料 （或者） 可以 Microsoft 復原 hello 資料嗎？ <br/>
hello 索引鍵使用的 tooencrypt hello 備份資料存在於只在 hello 客戶內部部署。 Microsoft 不會維持在 Azure 中的複本，而且沒有任何存取 toohello 金鑰。 如果 hello 客戶 misplaces hello 金鑰，Microsoft 無法復原 hello 備份資料。
