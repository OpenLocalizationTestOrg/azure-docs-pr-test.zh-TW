---
title: "aaaWhat 是 Azure 備份？ | Microsoft Docs"
description: "使用 Azure Backup tooback 並還原資料和工作負載從 Windows Server、 Windows 工作站、 System Center DPM 伺服器和 Azure 虛擬機器。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份與還原；復原服務；備份解決方案"
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>在 Azure Backup 中的 hello 功能的概觀
Azure 備份是 hello Azure 服務，您可以使用最大 tooback （或保護） 和還原您 hello Microsoft 雲端中的資料。 Azure 備份將以一個可靠、安全及具成本競爭力的雲端架構解決方案，取代您現有的內部部署或異地備份解決方案。 Azure 備份提供多個元件，您可以下載並在 hello 適當的電腦上部署伺服器，或在 hello 雲端中。 hello 元件或代理程式，您部署取決於您想要 tooprotect。 Azure 備份的所有元件 （不論是否您要保護資料的內部或 hello 雲端中） 都可以使用的 tooback 資料 tooa 復原服務保存庫在 Azure 中設定。 請參閱 hello [Azure Backup 元件資料表](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use)（本文稍後） 如需哪些元件 toouse tooprotect 特定資料、 應用程式或工作負載。

[觀看 Azure 備份的影片概觀](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>為何使用 Azure 備份？
傳統備份解決方案進化 tootreat hello 雲端做為端點或靜態儲存體目的地，類似 toodisks 或磁帶。 雖然這種方法很簡單，它是有限且未充分利用基礎雲端平台，將轉譯 tooan 昂貴、 效率不佳的解決方案。 因為您得到支付 hello 錯誤的儲存體或您不需要的儲存體的類型，則其他方案都很昂貴。 其他方案多半效率不佳，因為它們不提供您 hello 類型或在需要時，儲存體數量，或系統管理工作需要太多時間。 相反地，Azure 備份則提供下列主要優點：

**自動儲存管理**： 混合式環境通常需要異質儲存區-某些內部部署，而且在 hello 雲端。 使用 Azure 備份，使用內部部署儲存體裝置無需成本。 Azure 備份會自動配置和管理備份儲存體，且採用使用時付費制。 付款做為-您為使用的方法，您只需支付您所使用的 hello 儲存體。 如需詳細資訊，請參閱 hello [Azure 定價文章](https://azure.microsoft.com/pricing/details/backup)。

**無限制的縮放比例**-Azure Backup 使用 hello 基礎電源，並無限制的小數位數 hello Azure 雲端 toodeliver 高可用性-不需要維護或監視的負荷。 您可以設定警示 tooprovide 資訊事件，但是您不需要高可用性的相關 tooworry hello 雲端中的資料。

**多個儲存體選項** - 高可用性的其中一環是儲存體複寫。 Azure 備份提供兩種複寫類型：[本地備援儲存體](../storage/common/storage-redundancy.md#locally-redundant-storage)和[異地備援儲存體](../storage/common/storage-redundancy.md#geo-redundant-storage)。 選擇根據需求 hello 備份儲存體選項：

* 本機備援儲存體 (LRS) 會將資料複寫三次 （它會建立三份資料） 在 hello 的成對資料中心相同的區域。 LRS 是保護資料免於本機硬體失敗的低成本選項。

* 地理備援儲存體 (GRS) 會將複寫您的資料 tooa 次要區域 （相距甚遠 hello hello 來源資料的主要位置）。 GRS 的價格高於 LRS，但它為您的資料提供更高層級的持久性，即使遭受區域性停電也不影響。

**無限制的資料傳輸**-Azure Backup 不會限制 hello 數量傳入或傳出資料傳輸。 Azure 備份也不會進行收費 hello 資料傳輸。 不過，如果您使用 hello Azure 匯入/匯出服務 tooimport 大量資料時，會與輸入的資料相關聯成本。 如需這項成本的詳細資訊，請參閱 [Azure Backup 中的離線備份工作流程](backup-azure-backup-import-export.md)。 輸出資料是指 toodata 還原作業期間傳輸自復原服務保存庫。

**資料加密**-資料加密可讓安全傳輸和儲存體 hello 公用雲端中的資料。 儲存在本機，hello 加密複雜密碼，並永遠不會在傳送或儲存在 Azure 中。 如果它是任何必要 toorestore hello 資料，只有您有加密複雜密碼，或索引鍵。

**應用程式一致備份**-備份檔案伺服器、 虛擬機器或 SQL 資料庫，您是否需要 tooknow 復原點有所有必要資料 toorestore hello 備份複本。 Azure 備份提供應用程式一致備份，以確保其他修正並不是所需的 toorestore hello 資料。 還原應用程式一致的資料可縮短 hello 還原時間，可讓您 tooquickly 傳回 tooa 執行中狀態。

**長期保留**-而不是切換從磁碟 tootape 和移動 hello 磁帶 tooan 離站位置的備份複本，您可以使用 Azure 的短期和長期的保留。 Azure 不會限制 hello 時間長度的資料會保留在備份或復原服務保存庫。 只要您喜歡，就可以將資料保留在保存庫中。 Azure 備份的每個受保護執行個體上限為 9999 個復原點。 請參閱 hello[備份和保留](backup-introduction-to-azure-backup.md#backup-and-retention)本文，如需說明這項限制可能會如何影響您的備份需求 > 一節。  

## <a name="which-azure-backup-components-should-i-use"></a>我該使用哪一個 Azure 備份元件？
如果您不確定哪一個 Azure Backup 元件適用於您的需求，請參閱下表，如需您可以保護每個元件的 hello。 hello Azure 入口網站提供內建 hello 入口網站中，您逐步選取 hello 元件 toodownload 和部署的 tooguide 精靈。 hello 精靈，這是 hello 復原服務保存庫建立的一部分，會引導您完成選取備份目標，然後選擇 hello 資料或應用程式 tooprotect hello 步驟。

| 元件 | 優點 | 限制 | 什麼會受到保護？ | 備份會儲存在哪裡？ |
| --- | --- | --- | --- | --- |
| Azure 備份 (MARS) 代理程式 |<li>備份的檔案和資料夾儲存在實體或虛擬 Windows OS (VM 可以位於內部部署或 Azure 中)<li>不需任何個別的備份伺服器。 |<li>每天備份 3 次 <li>不會感知應用程式；僅有檔案、資料夾和磁碟區層級還原， <li>  不支援 Linux。 |<li>檔案、 <li>資料夾 |復原服務保存庫 |
| System Center DPM |<li>應用程式感知快照集 (VSS)<li>當完整彈性 tootake 備份<li>復原細微度 (全部)<li>可以使用復原服務保存庫<li>Hyper-V 和 VMware VM 的 Linux 支援 <li>使用 DPM 2012 R2 備份並還原 VMware VM |無法備份 Oracle 工作負載。|<li>檔案、 <li>資料夾、<li> 磁碟區、 <li>VM、<li> 應用程式、<li> 工作負載 |<li>復原服務保存庫、<li> 本機連接的磁碟、<li>  磁帶 (僅限內部部署) |
| Azure 備份伺服器 |<li>應用程式感知快照集 (VSS)<li>當完整彈性 tootake 備份<li>復原細微度 (全部)<li>可以使用復原服務保存庫<li>Hyper-V 和 VMware VM 的 Linux 支援<li>備份和還原 VMware VM <li>不需要 System Center 授權 |<li>無法備份 Oracle 工作負載。<li>一律需要即時 Azure 訂用帳戶<li>不支援磁帶備份 |<li>檔案、 <li>資料夾、<li> 磁碟區、 <li>VM、<li> 應用程式、<li> 工作負載 |<li>復原服務保存庫、<li> 本機連接的磁碟 |
| Azure IaaS VM 備份 |<li>適用於 Windows/Linux 的原生備份<li>不需使用特定代理程式安裝<li>不需要備份基礎結構的網狀架構層級備份 |<li>VM 每天備份一次 <li>只在磁碟層級還原 VM<li>無法備份內部部署 |<li>VM、 <li>所有磁碟 (使用 PowerShell) |<p>復原服務保存庫</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>每個元件的 hello 部署案例有哪些？
| 元件 | 可以在 Azure 中部署嗎？ | 可以在內部部署嗎？ | 支援的目標儲存體 |
| --- | --- | --- | --- |
| Azure 備份 (MARS) 代理程式 |<p>**是**</p> <p>hello Azure 備份代理程式可以部署在 Azure 中執行任何 Windows Server VM 上。</p> |<p>**是**</p> <p>hello 備份代理程式可以在任何 Windows Server VM 或實體機器上部署。</p> |<p>復原服務保存庫</p> |
| System Center DPM |<p>**是**</p><p>深入了解[如何 tooprotect 工作負載在 Azure 中的使用 System Center DPM](backup-azure-dpm-introduction.md)。</p> |<p>**是**</p> <p>深入了解[如何 tooprotect 工作負載和資料中心中的 Vm](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager)。</p> |<p>本機連接的磁碟、</p> <p>復原服務保存庫、</p> <p>磁帶 (僅限內部部署)</p> |
| Azure 備份伺服器 |<p>**是**</p><p>深入了解[如何 tooprotect 工作負載在 Azure 中的使用 Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)。</p> |<p>**是**</p> <p>深入了解[如何 tooprotect 工作負載在 Azure 中的使用 Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)。</p> |<p>本機連接的磁碟、</p> <p>復原服務保存庫</p> |
| Azure IaaS VM 備份 |<p>**是**</p><p>Azure 網狀架構的一部分</p><p>適用於[備份 Azure 基礎結構即服務 (IaaS) 虛擬機器](backup-azure-vms-introduction.md)。</p> |<p>**否**</p> <p>使用資料中心中的虛擬機器上的 System Center DPM tooback。</p> |<p>復原服務保存庫</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>可以備份哪些應用程式和工作負載？
下表中的 hello 提供 hello 資料並可以使用 Azure Backup 保護工作負載的矩陣。 hello Azure 備份解決方案的資料行具有該解決方案的連結 toohello 部署文件。 Azure 備份的每個元件皆可以部署在傳統 (Service Manager 部署) 或 Resource Manager 部署模型的環境中。

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| 資料或工作負載 | 來源環境 | Azure 備份方案 |
| --- | --- | --- |
| 檔案和資料夾 |Windows Server |<p>[Azure 備份代理程式](backup-configure-vault.md)、</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) （+ hello Azure 備份代理程式），</p> <p>[Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)（包括 hello Azure 備份代理程式）</p> |
| 檔案和資料夾 |Windows 電腦 |<p>[Azure 備份代理程式](backup-configure-vault.md)、</p> <p>[System Center DPM](backup-azure-dpm-introduction.md) （+ hello Azure 備份代理程式），</p> <p>[Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)（包括 hello Azure 備份代理程式）</p> |
| Hyper-V 虛擬機器 (Windows) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) （+ hello Azure 備份代理程式），</p> <p>[Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)（包括 hello Azure 備份代理程式）</p> |
| Hyper-V 虛擬機器 (Linux) |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) （+ hello Azure 備份代理程式），</p> <p>[Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)（包括 hello Azure 備份代理程式）</p> |
| 連接字串 |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) （+ hello Azure 備份代理程式），</p> <p>[Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)（包括 hello Azure 備份代理程式）</p> |
| Microsoft SharePoint |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) （+ hello Azure 備份代理程式），</p> <p>[Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)（包括 hello Azure 備份代理程式）</p> |
| Microsoft Exchange |Windows Server |<p>[System Center DPM](backup-azure-backup-sql.md) （+ hello Azure 備份代理程式），</p> <p>[Azure 備份伺服器](backup-azure-microsoft-azure-backup.md)（包括 hello Azure 備份代理程式）</p> |
| Azure IaaS VM (Windows) |在 Azure 中執行 |[Azure 備份 (VM 延伸模組)](backup-azure-vms-introduction.md) |
| Azure IaaS VM (Linux) |在 Azure 中執行 |[Azure 備份 (VM 延伸模組)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>支援 Linux
hello 下表顯示 hello 支援適用於 Linux 的 Azure 備份元件。  

| 元件 | Linux (Azure 背書) 支援 |
| --- | --- |
| Azure 備份 (MARS) 代理程式 |否 (僅限 Windows 代理程式) |
| System Center DPM |<li> Hyper-V 和 VMWare 上 Linux 來賓 VM 的檔案一致性備份<br/> <li> Hyper-V 和 VMWare Linux 來賓 VM 的 VM 還原 </br> </br>  *不適用於 Azure VM 的檔案一致性備份* <br/> |
| Azure 備份伺服器 |<li>Hyper-V 和 VMWare 上 Linux 來賓 VM 的檔案一致性備份<br/> <li> Hyper-V 和 VMWare Linux 來賓 VM 的 VM 還原 </br></br> *不適用於 Azure VM 的檔案一致性備份*  |
| Azure IaaS VM 備份 |使用[前置指令碼和後置指令碼架構](backup-azure-linux-app-consistent.md)的應用程式一致備份<br/> [細微檔案復原](backup-azure-restore-files-from-vm.md)<br/> [還原所有的 VM 磁碟](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [VM 還原](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>使用進階儲存體 VM 與 Azure 備份
Azure 備份可保護進階儲存體 VM。 Azure 高階儲存體是固態硬碟 (SSD) 為基礎儲存體設計 toosupport O 為大量工作負載。 進階儲存體非常適合用於虛擬機器 (VM) 工作負載。 如需 Premium 儲存體的詳細資訊，請參閱 hello 文章[高階儲存體： Azure 虛擬機器工作負載的高效能儲存體](../storage/common/storage-premium-storage.md)。

### <a name="back-up-premium-storage-vms"></a>備份進階儲存體 VM
Premium 儲存體的 Vm，hello Backup service 的備份會建立暫存的暫存位置，而名為 「 azure 備份-，"hello Premium 儲存體帳戶中。 預備位置 hello 大小是 hello 的等於 toohello hello 復原點的快照集大小。 請務必 hello 高階儲存體帳戶有足夠的可用空間 tooaccommodate hello 暫存臨時位置。 如需詳細資訊，請參閱 hello 文章[premium 儲存體限制](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)。 一旦 hello 備份工作完成時，會刪除預備位置的 hello。 hello hello 預備位置所使用的儲存體的價格是一致的所有[Premium 儲存體定價](../storage/common/storage-premium-storage.md#pricing-and-billing)。

> [!NOTE]
> 請勿修改或編輯 hello 預備位置。
>
>

### <a name="restore-premium-storage-vms"></a>還原進階儲存體 VM
Premium 儲存體 Vm 就能還原的 tooeither 高階儲存體或 toonormal 儲存體。 還原 Premium 儲存體 VM 復原點後 tooPremium 儲存體是 hello 還原的一般程序。 不過，它可以是符合成本效益 toorestore Premium 儲存體 VM 的復原點 toostandard 儲存體。 如果您需要從 hello VM 檔案的子集，則可以使用這種類型的還原。

## <a name="using-managed-disk-vms-with-azure-backup"></a>搭配使用受控磁碟 VM 與 Azure 備份
Azure 備份可保護受控磁碟 VM。 受控磁碟可讓您免於管理虛擬機器的儲存體帳戶，並可大幅簡化 VM 佈建。

### <a name="back-up-managed-disk-vms"></a>備份受控磁碟 VM
受控磁碟上的 VM 備份與 Resource Manager VM 備份沒有任何差異。 Hello Azure 入口網站，您可以設定 hello 直接從 hello 檢視虛擬機器的備份工作或從 hello 復原服務保存庫 檢視。 您可以透過以受控磁碟為基礎的 RestorePoint 集合來備份受控磁碟上的 VM。 Azure 備份也支援備份使用 Azure 磁碟加密 (ADE) 加密的受控磁碟 VM。

### <a name="restore-managed-disk-vms"></a>還原受控磁碟 VM
Azure Backup 可讓您 toorestore 完成 VM 與受管理的磁碟，或還原受管理磁碟 tooa 儲存體帳戶。 Azure 管理受管理的 hello 磁碟 hello 還原程序。 您 （hello 客戶） 來管理 hello hello 還原程序過程中建立的儲存體帳戶。 當還原管理加密的 Vm 時，hello VM 的金鑰和密碼應存在於 hello 金鑰保存庫之前 toostarting hello 還原作業。

## <a name="what-are-hello-features-of-each-backup-component"></a>每個備份元件 hello 功能有哪些？
hello 下列各節提供摘要說明 hello 可用性或支援的每個 Azure 備份 」 元件中的各種功能的資料表。 請參閱下列其他支援或詳細資料的每個資料表的 hello 資訊。

### <a name="storage"></a>儲存體
| 功能 | Azure 備份代理程式 | System Center DPM | Azure 備份伺服器 | Azure IaaS VM 備份 |
| --- | --- | --- | --- | --- |
| 復原服務保存庫 |![是][green] |![是][green] |![是][green] |![是][green] |
| 磁碟儲存體 | |![是][green] |![是][green] | |
| 磁帶儲存體 | |![是][green] | | |
| 壓縮 <br/>(在復原服務保存庫中) |![是][green] |![是][green] |![是][green] | |
| 增量備份 |![是][green] |![是][green] |![是][green] |![是][green] |
| 磁碟重複資料刪除 | |![部分][yellow] |![部分][yellow] | | |

![資料表索引鍵](./media/backup-introduction-to-azure-backup/table-key.png)

hello 復原服務保存庫是 hello 慣用儲存體目標，所有元件。 System Center DPM 和 Azure 備份伺服器也提供 hello 選項 toohave 的本機磁碟的複本。 不過，System Center DPM 提供 hello 選項 toowrite 資料 tooa 磁帶存放裝置。

#### <a name="compression"></a>壓縮
備份會進行壓縮 tooreduce hello 所需的儲存體空間。 不使用壓縮的 hello 唯一元件是 hello VM 擴充功能。 所有的備份資料，從您的儲存體帳戶 toohello 復原服務保存庫中的 hello VM 延伸模組複製 hello 相同的區域。 不使用壓縮傳送嗨資料時。 稍微傳送 hello 未壓縮的資料會擴大 hello 儲存體使用。 不過，未壓縮可讓更快速的還原，請儲存 hello 資料，如果您需要該復原點。


#### <a name="disk-deduplication"></a>磁碟重複資料刪除
當您在 [HYPER-V 虛擬機器上](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx)部署 System Center DPM 或 Azure 備份伺服器時，可以充分利用重複資料刪除。 Windows Server 虛擬硬碟 (Vhd) 的附加的 toohello 做為備份儲存體的虛擬機器上執行重複資料刪除功能 （在 hello 主機層級）。

> [!NOTE]
> 重複資料刪除不適用於任何在 Azure 中的備份元件。 當 System Center DPM 及備份伺服器部署在 Azure 中時，連接 VM 不能被重複資料刪除的 toohello hello 儲存體磁碟。
>
>

### <a name="incremental-backup-explained"></a>增量備份的說明
每個 Azure 備份的元件可支援增量備份，不論 hello 目標存放裝置 （磁碟、 磁帶、 復原服務保存庫）。 增量備份可確保備份存放區以及時間有效率，由傳送 hello 上次備份之後所做的變更。

#### <a name="comparing-full-differential-and-incremental-backup"></a>比較完整、差異和增量備份

每一種備份方法的儲存體耗用量、復原時間目標 (RTO) 以及網路耗用量都有所不同。 tookeep hello 備份擁有權總成本 (TCO) 下的，您需要 toounderstand 如何 toochoose hello 最佳備份解決方案。 下列映像的 hello 比較完整備份、 差異備份，以及增量備份。 在 hello 映像，A 由 10 個儲存體所組成的資料來源會封鎖 A1 A10 的每月備份。 區塊 A2、 A3、 A4、 和 A9 hello 中第一個月的變更，並封鎖 hello A5 變更下個月。

![圖中顯示備份方法的比較](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

與**完整備份**，每個備份的複本包含 hello 整個資料來源。 完整備份會在每次傳輸備份複本時，耗用大量網路頻寬和儲存體。

**差異備份**hello 封鎖 hello 初始完整備份之後，會導致較少量的網路和存放裝置耗用量的變更只會儲存。 差異備份不會保留未變更資料的備援複本。 不過，因為 hello 維持不變，後續的備份之間的資料區塊會傳輸並儲存，差異備份會沒有效率。 Hello 第二個月，變更的區塊 A2、 A3、 A4、 和 A9 群組的備份。 在 hello 第三個月，這些相同的區塊會備份一次，以及已變更的區塊 A5。 變更的區塊的 hello 繼續 toobe 必須等到 hello 下次完整備份會備份。

**增量備份**來儲存 hello 前一個備份之後變更過的資料只有 hello 區塊達到儲存體和網路的高效率。 使用增量備份，無須 tootake 定期完整備份。 在 hello 範例中，第一個月，取得完整備份的 hello hello 之後 A2、 A3、 A4、 和 A9 標示為已變更的區塊變更，並傳送 hello 第二個月。 在 hello 第三個月，只變更的區塊 A5 是標示，並傳送。 移動較少的資料可節省儲存體和網路資源，進而降低 TCO。   

### <a name="security"></a>安全性
| 功能 | Azure 備份代理程式 | System Center DPM | Azure 備份伺服器 | Azure IaaS VM 備份 |
| --- | --- | --- | --- | --- |
| 網路安全性<br/> (tooAzure) |![是][green] |![是][green] |![是][green] |![部分][yellow] |
| 資料安全性<br/> (在 Azure 中) |![是][green] |![是][green] |![是][green] |![部分][yellow] |

![資料表索引鍵](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>網路安全性
從您的伺服器 toohello 復原服務保存庫的所有備份流量加密使用進階加密標準 256。 hello 備份資料會透過安全的 HTTPS 連結來傳送。 hello 備份資料也會以加密形式 hello 復原服務保存庫中儲存。 Hello Azure 客戶，您只有 hello 複雜密碼 toounlock 這項資料。 Microsoft 無法解密 hello 在任何時間點的備份資料。

> [!WARNING]
> 一旦您建立 hello 復原服務保存庫時，只有您才能存取 toohello 加密金鑰。 Microsoft 永遠不會維護一份您的加密金鑰，並沒有存取 toohello 索引鍵。 如果 hello 金鑰放錯位置，Microsoft 無法復原 hello 備份資料。
>
>

#### <a name="data-security"></a>資料安全性
備份 Azure Vm 需要設定加密*內*hello 虛擬機器。 在 Windows 虛擬機器上使用 BitLocker，而在 Linux 虛擬機器上使用 **dm-crypt** 。 Azure 備份不會自動加密來自此路徑的備份資料。

### <a name="network"></a>網路
| 功能 | Azure 備份代理程式 | System Center DPM | Azure 備份伺服器 | Azure IaaS VM 備份 |
| --- | --- | --- | --- | --- |
| 網路壓縮 <br/>(太**備份伺服器**) | |![是][green] |![是][green] | |
| 網路壓縮 <br/>(太**復原服務保存庫**) |![是][green] |![是][green] |![是][green] | |
| 網路通訊協定 <br/>(太**備份伺服器**) | |TCP |TCP | |
| 網路通訊協定 <br/>(太**復原服務保存庫**) |HTTPS |HTTPS |HTTPS |HTTPS |

![資料表索引鍵](./media/backup-introduction-to-azure-backup/table-key-2.png)

hello （在 hello IaaS VM) 上的 VM 延伸模組讀取 hello 資料直接從 hello Azure 儲存體帳戶透過 hello 儲存網路，如此就不需要 toocompress 這個流量。

如果您使用 System Center DPM 伺服器或 Azure 備份伺服器備份的次要伺服器時，壓縮 hello 資料從 hello 主要伺服器 toohello 備份伺服器。 在備份 tooDPM 或 Azure 備份伺服器之前先壓縮資料，可以節省頻寬。

#### <a name="network-throttling"></a>網路節流
hello Azure Backup agent 提供了網路節流設定，可讓您 toocontrol 資料傳輸期間的網路頻寬使用方式。 節流可以是很有幫助，如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量。 節流資料傳送套用 tooback 組成，並還原活動。

## <a name="backup-and-retention"></a>備份和保留

Azure 備份每個*受保護的執行個體*上限為 9999 個復原點 (也稱為備份複本或快照集)。 電腦、 伺服器 （實體或虛擬） 或總資料 tooAzure 設定的工作負載 tooback 受保護的執行個體。 如需詳細資訊，請參閱 hello 區段中，[什麼是受保護的執行個體](backup-introduction-to-azure-backup.md#what-is-a-protected-instance)。 儲存資料的備份複本之後，執行個體就會受到保護。 hello 資料的備份複本是 hello 保護。 如果 hello 來源資料已遺失或損毀，hello 備份無法還原 hello 來源資料。 hello 下表顯示 hello 最大的備份頻率為每個元件。 您的備份原則設定會決定取用 hello 復原點的速度。 比方說，如果您每天建立復原點，則在用完之前可以保留復原點 27 年。如果您採用每月復原點，您可保留復原點之前即用盡 833 年。hello 備份服務不會在復原點上設定到期時間限制。

|  | Azure 備份代理程式 | System Center DPM | Azure 備份伺服器 | Azure IaaS VM 備份 |
| --- | --- | --- | --- | --- |
| 備份頻率<br/> （tooRecovery 服務保存庫） |每天備份 3 次 |每天備份 2 次 |每天備份 2 次 |每天備份 1 次 |
| 備份頻率<br/> (toodisk) |不適用 |<li>每隔 15 分鐘 (SQL Server) <li>每隔 1 小時 (其他工作負載) |<li>每隔 15 分鐘 (SQL Server) <li>每隔 1 小時 (其他工作負載)</p> |不適用 |
| 保留選項 |每日、每週、每月、每年 |每日、每週、每月、每年 |每日、每週、每月、每年 |每日、每週、每月、每年 |
| 每個受保護執行個體的最大復原點 |9999|9999|9999|9999|
| 最大保留期間 |依照備份頻率而定 |依照備份頻率而定 |依照備份頻率而定 |依照備份頻率而定 |
| 本機磁碟上的復原點 |不適用 |<li>64 (檔案伺服器)、<li>448 (應用程式伺服器) |<li>64 (檔案伺服器)、<li>448 (應用程式伺服器) |不適用 |
| 磁帶上的復原點 |不適用 |無限 |不適用 |不適用 |

## <a name="what-is-a-protected-instance"></a>什麼是受保護的執行個體
泛型參照 tooa Windows 電腦、 伺服器 （實體或虛擬） 或已設定的 tooback tooAzure 上的 SQL database 的受保護的執行個體。 一旦設定 hello 電腦、 伺服器或資料庫的備份原則，並建立一份備份 hello 資料保護執行個體。 後續份 hello 備份資料 （這稱為復原點） 的受保護執行個體，請增加 hello 耗用儲存體數量。 您可以建立註冊 too9999 復原點的受保護的執行個體。 如果您從儲存體刪除復原點，它不會計算 hello 9999 的復原點總數。
受保護的執行個體的一些常見的範例是虛擬機器、 應用程式伺服器、 資料庫和執行 hello Windows 作業系統的個人電腦。 例如：

* 執行的虛擬機器 hello HYPER-V 或 Azure IaaS hypervisor 網狀架構。 hello hello 虛擬機器客體作業系統可以是 Windows Server 或 Linux。
* 應用程式伺服器： hello 應用程式伺服器可以是實體或虛擬機器執行 Windows Server 和工作負載且需要 toobe 備份的資料。 常見的工作負載是 Microsoft SQL Server、 Microsoft Exchange server、 Microsoft SharePoint server 和 Windows Server 上的 hello 檔案伺服器角色。 tooback 這些工作負載備份需要 System Center Data Protection Manager (DPM) 或 Azure 備份伺服器。
* 個人電腦、 工作站上或執行 Windows 作業系統 hello 的膝上型電腦。


## <a name="what-is-a-recovery-services-vault"></a>什麼是復原服務保存庫？
復原服務保存庫是在 Azure 中的線上存放區實體使用 toohold 資料，例如備份、 復原點，以及備份原則。 您可以使用 復原服務保存庫 toohold 備份資料的 Azure 服務和內部部署伺服器和工作站。 復原服務保存庫讓您輕鬆 tooorganize 備份資料，可能降低管理負擔降到最低。 您可以在訂用帳戶中建立所需數量的復原服務保存庫。

備份保存庫，採用 Azure 服務管理員，已 hello 第一版的 hello 保存庫。 復原服務保存庫，新增 hello Azure 資源管理員的模型功能，其中的 hello hello 保存庫的第二個版本。 請參閱 hello[復原服務保存庫概觀文章](backup-azure-recovery-services-vault-overview.md)hello 功能差異的完整說明。 您不能再建立使用 hello 入口 toocreate 備份保存庫，但仍支援備份保存庫。

> [!IMPORTANT]
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> **2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。 <br/> **在 2017 年 11 月 1 日以前**：
>- 任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Azure 備份與 Azure Site Recovery 有何不同？
Azure 備份與 Azure Site Recovery 類似，這兩個服務皆可備份資料及還原資料。 不過，這些服務各有不同的用途，可在您的企業中提供業務持續性和災害復原。 使用 Azure Backup tooprotect 並還原資料更細微的層級。 比方說，如果在膝上型電腦上的展示檔損毀，您會使用 Azure Backup toorestore hello 簡報。 如果您想 tooreplicate hello 設定和在 VM 上的資料，另一個資料中心之間，使用 Azure Site Recovery。

Azure Backup 保護資料的內部和 hello 雲端中。 Azure Site Recovery 可協調虛擬機器和實體伺服器的複寫、容錯移轉及容錯回復。 這兩項服務很重要，因為您的災害復原解決方案需要 tookeep 資料安全且更容易修復 （備份）*和*發生中斷時，保留您的工作負載可以使用 （站台復原）。

hello 下列概念可協助您做出重要決定周圍備份和災害復原。

| 概念 | 詳細資料 | 備份 | 災害復原 (DR) |
| --- | --- | --- | --- |
| 復原點目標 (RPO) |如果復原需求 toobe 完成的可接受資料遺失的 hello 數量。 |備份解決方案在其可接受的 RPO 有寬廣的變化性。 虛擬機器備份的 RPO 通常為 1 天，而資料庫備份的 RPO 只需 15 分鐘。 |災害復原解決方案的 RPO 很低。 hello DR 複本可以後面幾秒鐘或幾分鐘的時間。 |
| 復原時間目標 (RTO) |hello 花費 toocomplete 復原或還原的時間量。 |由於 hello 較大的 RPO，hello 少量資料的備份解決方案需要 tooprocess 是通常更高，這會導致 toolonger Rto。 例如，可能需要天 toorestore 磁帶，取決於 hello 時間花在離站位置 tootransport hello 磁帶中的資料。 |災害復原解決方案有較小的 Rto，因為它們是更多的同步與 hello 來源。 Toobe 處理需要較少的變更。 |
| 保留 |需要儲存 toobe 多久資料 |在需要作業復原的情況下 (資料損毀、不小心刪除檔案、作業系統失敗)，備份資料通常會保留 30 天或更短。<br>相容性的觀點而言，資料可能需要 toobe 儲存數個月甚至數年。 在這類情況下，最理想的方式是將備份資料封存。 |災害復原需求只操作的復原資料，這通常需要幾個小時 （含） 以上 tooa 一天。 Hello 細項資料擷取在 DR 解決方案中使用，因為不建議使用供長期保存的 DR 資料。 |

## <a name="next-steps"></a>後續步驟
在 Azure 中使用下列詳細的逐步指示保護 Windows Server 上的資料，或保護虛擬機器 (VM) 的教學課程的 hello 的其中一個：

* [備份檔案和資料夾](backup-try-azure-backup-in-10-mins.md)
* [備份 Azure 虛擬機器](backup-azure-vms-first-look-arm.md)

如需保護其他工作負載的詳細資訊，請參閱這些文件︰

* [備份 Windows 伺服器](backup-configure-vault.md)
* [備份應用程式工作負載](backup-azure-microsoft-azure-backup.md)
* [備份 Azure IaaS VM](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
