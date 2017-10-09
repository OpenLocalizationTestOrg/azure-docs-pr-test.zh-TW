---
title: "Azure IaaS 磁碟 aaaBackup 和災害復原 |Microsoft 文件"
description: "在本文中，我們將說明如何備份和災害復原 (DR) 的 IaaS 虛擬機器 (Vm) 的 tooplan 和 Azure 中的磁碟。 本文件涵蓋受控磁碟和非受控磁碟"
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: luywang
ms.openlocfilehash: 49b0e7732d6df9407e1e44d9af2500c99a85b37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-disaster-recovery-for-azure-iaas-disks"></a>Azure IaaS 磁碟的備份和災害復原

在本文中，我們將說明如何備份和災害復原 (DR) 的 IaaS 虛擬機器 (Vm) 的 tooplan 和 Azure 中的磁碟。 本文件涵蓋受控磁碟和非受控磁碟。

我們會先討論 hello 內建容錯功能在 hello Azure 平台，協助防範本機失敗。 然後，我們將討論未完全涵蓋 hello 內建功能，這是此文件所定址的 hello 主要主題 hello 災害案例。 我們也將示範幾個工作負載案例範例，其中可能會有不同的備份和 DR 考量。 接著會檢閱 IaaS 磁碟的可能 DR 解決方案。 

## <a name="introduction"></a>簡介

hello Azure 平台會使用各種方法以獲得備援與錯誤容錯 toohelp 保護客戶從硬體失敗，可能會發生。 本機失敗可能包括將虛擬磁碟的 hello 資料的一部分或失敗的 SSD 或 HDD 儲存在該伺服器的 Azure 儲存體伺服器電腦的問題。 這種隔離的硬體元件故障可能發生在正常作業期間，並且 hello 平台是設計的 toobe 彈性 toothese 失敗。 重大災害可能會導致大量儲存體伺服器或整個資料中心失敗或無法存取。 當您的 Vm 和磁碟，正常保護從當地語系化失敗時，額外的步驟是必要的 tooprotect 區域全災難性失敗 （例如重大的災害） 可能會影響您的 VM 和磁碟從您的工作負載。

此外 toohello 的平台失敗的可能性，與 hello 客戶應用程式或資料發生問題。 比方說，您的應用程式的新版本可能會不小心讓中斷變更 toohello 資料。 在此情況下，您可能想 toorevert hello 應用程式和 hello 資料 tooa 先前的版本包含 hello 最後一個已知的良好狀態。 這需要維護定期備份。

地區的災害復原，您必須備份您 IaaS VM 磁碟 tooa 不同的區域。 

讓我們先回顧可用來處理當地語系化失敗的一些方法，再檢視備份和 DR 選項。

### <a name="azure-iaas-resiliency"></a>Azure IaaS 復原

*恢復功能*參考 toohello 容錯硬體元件中發生一般失敗。 恢復功能是從失敗的 hello 能力 toorecover 和繼續 toofunction。 它不是如何避免失敗，但回應 toofailures 可避免停機時間或資料遺失的方式。 hello 的恢復功能的目標是 tooreturn hello 應用程式 tooa 完全正常運作狀態發生失敗。 Azure 虛擬機器和磁碟屬於設計的 toobe 彈性 toocommon 硬體錯誤。 讓我們看看如何 hello Azure IaaS 平台提供此恢復功能。

虛擬機器主要在於兩個部分: （1） 的計算伺服器，以及 （2) hello 永續性磁碟。 同時會影響虛擬機器的 hello 容錯功能。

如果裝載 VM 的 hello Azure 計算主機伺服器遇到硬體失敗 （此為罕見），Azure 會是另一部伺服器上的設計的 tooautomatically 還原 hello VM。 如果發生這種情況，就會發生重新開機，並 hello VM 一段時間後，將會備份。 Azure 會自動偵測這種硬體故障並執行復原 toohelp 確保 hello 客戶 VM 儘速將可以使用。

之 IaaS 磁碟的相關資料持續性相當重要 hello 永續性儲存體的平台。 Azure 客戶有 IaaS 上執行的重要的商務應用程式，而且它們相依於 hello hello 資料持續性。 Azure 設計這些 IaaS 磁碟保護的方式是在本機儲存三份資料的備援複本，並提供高持久性以防範本機失敗。 如果其中一個 hello 保存您的磁碟的硬體元件失敗，因為有兩個額外複本 toosupport 磁碟要求，就不受影響您的 VM。 即使兩個不同的硬體元件支援的磁碟在失敗 hello 相同可以正常運作 （這會是非常罕見） 的時間。 toohelp 確保我們永遠維護三份複本，hello Azure 儲存體服務會自動產生 hello 背景中資料的新副本，如果其中一個 hello 三個複本變成無法使用。 因此，它不能與 Azure 磁碟的容錯功能的必要 toouse RAID。 簡單的 RAID 0 設定應該足以應付如果等量磁碟 hello 必要 toocreate 較大的磁碟區。

由於此結構，**Azure 為 IaaS 磁碟一致地提供企業級持久性，其[年度失敗率](https://en.wikipedia.org/wiki/Annualized_failure_rate)為零，領先業界。**

硬體故障 hello 上的計算裝載或 hello 儲存體中的平台有時可能會導致暫時無法使用的 vm hello 所涵蓋的 hello [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) VM 可用性。 Azure 也提供領先業界的 SLA，適用於使用進階儲存體磁碟的單一 VM 執行個體。

toosafeguard 停機 toohello 暫時無法使用磁碟或 VM 的應用程式工作負載，客戶可以利用[可用性設定組](../../virtual-machines/windows/manage-availability.md)。 可用性設定組中的兩個或多個虛擬機器提供 hello 應用程式的備援性。 Azure 會接著在具有不同電源、網路和伺服器元件的個別容錯網域中，建立這些 VM 和磁碟。 因此，當地語系化的硬體失敗通常不會影響在 hello hello 在設定中的多個 Vm 同時，為您的應用程式提供高可用性。 它會被視為好的作法 toouse 可用性設定組需要高可用性時。 如需詳細資訊，請參閱詳述如下的 hello 嚴重損壞修復層面。

### <a name="backup-and-disaster-recovery"></a>備份和災害復原

災害復原 (DR) 是從少見，但主要事件的 hello 能力 toorecover： 非暫時性、 寬位小數位數的失敗，例如會影響整個地區的服務中斷。 災害復原包括資料備份和封存，而且可能包括手動操作，例如從備份中還原資料庫。

hello Azure 平台的內建保護當地語系化故障可能無法完全保護 hello Vm/磁碟在 hello 的重大的災害而造成大型中斷的情況下。 這包括資料中心遇到颶風、地震、火災，或大規模硬體裝置失敗等重大事件。 此外，您可能會失敗，因為 tooapplication 或資料的問題。

toohelp 保護您的 IaaS 工作負載從中斷，您應該規劃備援性和備份 tooenable 復原。 災害復原，您應該規劃備援及在遠離 hello 主要站台不同的地理位置的備份。 這有助於確保您的備份不會受到 hello 原本影響 hello VM 或磁碟的相同事件。 如需詳細資訊，請參閱 [Disaster recovery for Azure applications](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications) (Azure 應用程式的災害復原)。

您的 DR 考量可能包括下列方面的 hello:

1. 高可用性 (HA) 是執行不需顯著停機的狀況良好的 hello 應用程式 toocontinue hello 能力。 「 狀況良好的狀態 」 是指 hello 應用程式有回應，，和使用者可以連接 toohello 應用程式，並與其互動。 特定的關鍵任務應用程式和資料庫可能需要的 toobe 可用一律，即使在 hello 平台也會失敗。 這些工作負載，您可能需要 tooplan hello 應用程式，以及 hello 資料的複本。

2. 資料持久性： 在某些情況下，hello 主要考量確定 hello 資料會保留在嚴重損壞的 hello 案例。 因此，您可能需要在不同的網站上有資料備份。 針對這類工作負載，您可能不需要完整的備援性 hello 應用程式，但 hello 磁碟的定期備份。

## <a name="backup-and-dr-scenarios"></a>備份和 DR 案例

讓我們看看應用程式工作負載案例和規劃災害復原的 hello 考量的一些典型的例子。

### <a name="scenario-1-major-database-solutions"></a>案例 1：主要資料庫解決方案

假設有一個可支援高可用性的生產環境資料庫伺服器，例如 SQL Server 或 Oracle。 重要的生產環境應用程式和使用者都相依於此資料庫。 此系統的 hello 災害復原計劃可能會需要 toosupport hello 下列需求：

1. 資料必須是受保護且可復原的。
2.  伺服器必須可供使用。

這可能需要維護不同的區域，以當作備份中的 hello 資料庫的複本。 根據伺服器的可用性和資料修復的 hello 需求，hello 方案可能涉及主動-主動或主動-被動複本網站 tooperiodic 的離線備份 hello 資料。 SQL Server 和 Oracle 等關聯式資料庫提供各種複寫選項。 若是 SQL Server，可使用 [SQL Server Always On 可用性群組](https://msdn.microsoft.com/library/hh510230.aspx)來取得高可用性。

MongoDB 之類的 NoSQL 資料庫也支援以[複本](https://docs.mongodb.com/manual/replication/)進行備援。 可以使用 hello 複本以提供高可用性。

### <a name="scenario-2-a-cluster-of-redundant-vms"></a>案例 2：備援 VM 的叢集

假設有一個由 VM 的叢集所處理的工作負載提供備援和負載平衡。 其中一個範例是區域中所部署的 Cassandra 叢集。 此架構類型已在該區域內提供高層級的備援。 不過，從區域的層級失敗 tooprotect hello 工作負載，您應該考慮分配 hello 叢集跨兩個區域或進行定期備份 tooanother 區域。

### <a name="scenario-3-iaas-application-workload"></a>案例 3：IaaS 應用程式工作負載

這可能是在 Azure VM 上執行的一般生產環境工作負載。 例如，它可能是 web 伺服器或檔案伺服器 hello 內容與站台的其他資源。 它也可能是 hello VM 磁碟儲存其資料、 資源和應用程式狀態在 VM 上執行自訂商務應用程式。 在此情況下，很重要 toomake 確定您定期進行備份。 備份頻率應根據 hello hello VM 工作負載的本質。 比方說，如果 hello 應用程式每天執行，而且會修改的資料，然後 hello 應該進行備份的每個小時。

另一個範例是，報表伺服器從其他來源提取資料並產生彙總報表。 此 VM 或磁碟遺失的問題會導致 toohello 遺失 hello 報表。 不過，它可能會報告處理程序，並重新產生 hello 輸出可能 toorerun hello。 在此情況下，您實際上不需要資料遺失，即使 hello 報表伺服器叫用時與損毀，因此您可能會有較高等級的容許的遺失 hello hello 報表伺服器上的資料的一部分。 在此情況下，較不頻繁的備份是選項 tooreduce hello 成本。

### <a name="scenario-4-iaas-application-data-issues"></a>案例 4：IaaS 應用程式資料問題

您有一個應用程式，可計算、維護及提供重要商用資料，例如價格資訊。 您的應用程式的新版本有軟體錯誤，錯誤地計算 hello 定價，而損毀的 hello hello 平台所提供現有商務資料。 在這裡，hello 最好的做法就是 toorevert toohello 舊版 hello 應用程式和 hello 資料第一次。 tooenable，採取定期備份您的系統。

## <a name="disaster-recovery-solution-azure-backup-service"></a>災害復原解決方案：Azure 備份服務

[Azure 備份服務](https://azure.microsoft.com/services/backup/)可用來進行備份和 DR，並適用於[受控磁碟](../../virtual-machines/windows/managed-disks-overview.md)和[非受控磁碟](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks)。 您可以建立具有以時間為基礎的備份、簡易 VM 還原，以及備份保留原則的備份工作。 

如果您使用[Premium 儲存體磁碟](storage-premium-storage.md)，[管理磁碟](../../virtual-machines/windows/managed-disks-overview.md)，或其他磁碟類型，以 hello[本機備援儲存體 (LRS)](storage-redundancy.md#locally-redundant-storage)選項時，它是特別重要 tooleverage定期的 DR 備份。 Azure 備份以供長期保存您復原服務保存庫儲存 hello 資料。 選擇 hello[地理備援儲存體 (GRS)](storage-redundancy.md#geo-redundant-storage)選項 hello 備份復原服務保存庫。 如此可確保備份是避免複寫的 tooa 不同 Azure 區域從地區的災害防護。

如[Unmanaged 磁碟](../../virtual-machines/windows/about-disks-and-vhds.md#unmanaged-disks)，您可以使用 IaaS 磁碟 hello LRS 儲存體類型，但確定已啟用 Azure Backup 以 hello GRS hello 復原服務保存庫的選項。

**如果您使用 hello [GRS](storage-redundancy.md#geo-redundant-storage)/[RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)選項為未受管理磁碟，您仍需要一致的快照集備份和 DR 能力。** 您必須使用 [Azure 備份服務](https://azure.microsoft.com/services/backup/)或[一致性快照](#alternative-solution-consistent-snapshots)。

hello 以下是 dr 解決方案的摘要。

| 案例 | 自動複寫 | DR 解決方案 |
| --- | --- | --- |
| 進階儲存體磁碟 | 本地 ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure 備份](https://azure.microsoft.com/services/backup/) |
| *受控磁碟* | 本地 ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure 備份](https://azure.microsoft.com/services/backup/) |
| 非受控 LRS 磁碟 | 本地 ([LRS](storage-redundancy.md#locally-redundant-storage)) | [Azure 備份](https://azure.microsoft.com/services/backup/) |
| 非受控 GRS 磁碟 | 跨區域 ([GRS](storage-redundancy.md#geo-redundant-storage)) | [Azure 備份](https://azure.microsoft.com/services/backup/)<br/>[一致性快照](#alternative-solution-consistent-snapshots) |
| 非受控 RA-GRS 磁碟 | 跨區域 ([RA-GRS](storage-redundancy.md#read-access-geo-redundant-storage)) | [Azure 備份](https://azure.microsoft.com/services/backup/)<br/>[一致性快照](#alternative-solution-consistent-snapshots) |

最高可用性可以藉由符合透過 hello 使用受管理磁碟及 Azure Backup 可用性設定組。 如果您使用非受控磁碟，您仍然可以使用 Azure 備份進行 DR。 如果您無法 toouse Azure 備份，然後採取[一致的快照集](#alternative-solution-consistent-snapshots)後面的章節中所述是備份和 DR 的替代方案。

應用程式或基礎結構層級的高可用性、備份和 DR 選項如下所示：

| *Level* | 高可用性   | 備份/DR |
| --- | --- | --- |
| *應用程式* | SQL Always On | Azure 備份 |
| 基礎結構  | 可用性設定組  | 使用一致性快照的 GRS |

### <a name="using-hello-azure-backup-service"></a>使用 hello Azure 備份服務

[Azure 備份](../../backup/backup-azure-vms-introduction.md)可以備份您的 Vm 執行 Windows 或 Linux toohello Azure 復原服務保存庫。 備份和還原業務關鍵資料更為複雜業務關鍵資料必須備份時產生的 hello 執行資料的 hello 應用程式的 hello 事實。 tooaddress，Azure 備份提供的 Microsoft 工作負載所使用的資料已正確寫入 toostorage hello 磁碟區陰影服務 (VSS) tooensure 應用程式一致的備份。 適用於 Linux Vm 檔案一致的備份是可行的因為 Linux 沒有功能相等 tooVSS。

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-1.png)   

當 Azure Backup 在 hello 排定時間起始備份工作時，它就會觸發 hello 備份延伸模組安裝在 hello VM tootake 時間點快照集。 在擷取快照當時搭配 hello 虛擬機器中的 hello 磁碟 VSS tooget 一致的快照集而不需要 tooshut 它關閉。 hello VM 中的 hello 備份擴充功能排清所有寫入之前取得的所有 hello 磁碟 hello 一致的快照集。 Hello 快照之後，Azure Backup toohello 備份保存庫會傳送 hello 資料。 toomake hello 備份程序更有效率，hello 服務識別，以及傳輸只有 hello 區塊的 hello 上次備份之後已變更的資料。


toorestore，您可以檢視 hello 透過 Azure 備份的可用備份，並再啟動還原。 您可以建立和還原 hello 透過 Azure 備份[Azure 入口網站](https://portal.azure.com/)，[使用 PowerShell](../../backup/backup-azure-vms-automation.md )，或使用 hello [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install)。 如需詳細資訊，請參閱＜Azure 備份＞。

### <a name="steps-tooenable-backup"></a>步驟 tooEnable 備份

hello 下列步驟會使用 hello Vm 的常用的 tooenable 備份[Azure 入口網站](https://portal.azure.com/)。 視您實際情況而定，會有一些變化。 請參閱 toohello [Azure Backup](../../backup/backup-azure-vms-introduction.md)文件的完整詳細資料。 Azure 備份也[支援 VM 與受控磁碟](https://azure.microsoft.com/blog/azure-managed-disk-backup/)。

1.  復原服務保存庫建立 VM，使用下列步驟的 hello:

    a.  使用 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽的所有資源，並尋找 「 復原服務保存庫 」。

    b.  Hello 上復原服務保存庫 功能表中，按一下 新增 並遵循 hello 步驟 toocreate hello 中新的保存庫與 hello VM 相同的區域。 比方說，如果您的 VM 位於美國西部地區，選擇美國西部 hello 保存庫。

2.  確認新建立的保存庫的 hello 的 hello 儲存體複寫。 toodo 從 hello 復原服務保存庫刀鋒視窗，然後移至 toohello 設定/備份設定，存取 hello 保存庫。 確定預設會選取 hello GRS 選項。 這可確保您的保存庫會自動複寫的 tooa 次要資料中心。 例如，您在美國西部的保存庫會自動複寫的 tooEast 美國。

3.  設定 hello 備份原則，並選取從 hello hello VM 相同的 UI。

4.  請確定 hello hello VM 安裝備份代理程式。 使用 Azure 資源庫映像建立 VM 時，如果是已安裝 hello 備份代理程式。 否則 （也就是如果您正在使用的自訂映像），也使用指示[hello 虛擬機器上的安裝 hello VM 代理程式](../../backup/backup-azure-arm-vms-prepare.md#install-the-vm-agent-on-the-virtual-machine)。

5.  請確定該 hello VM 允許 hello 備份服務 toofunction 的網路連線。 請遵循[網路連線](../../backup/backup-azure-arm-vms-prepare.md#network-connectivity)的這些指示。

6.  一旦完成上述步驟 hello，hello 備份將會執行定期 hello 備份原則中所指定。 如有必要，您可以觸發 hello 第一次備份，以手動方式從 hello hello Azure 入口網站上的保存庫儀表板。

如需自動化 Azure Backup 使用指令碼，請參閱太[VM 備份的 PowerShell 指令程式](../../backup/backup-azure-vms-automation.md)。

### <a name="steps-for-recovery"></a>復原步驟

如果您需要 toorepair 或重新建立 VM 時，您可以從任何 hello hello 保存庫中的備份復原點還原 hello VM。 有幾個不同的選項執行 hello 復原：

1.  您可以建立新的 VM 作為已備份 VM 的時間點表示。

2.  您可以還原 hello 磁碟，然後使用 hello VM toocustomize hello 範本並重建 hello 還原 VM。 

請參閱指示太[使用 Azure 入口網站 toorestore 虛擬機器](../../backup/backup-azure-arm-restore-vms.md#restoring-a-vm-during-azure-datacenter-disaster)。 hello 文件也會說明 hello 還原備份 Vm toohello 成對的資料中心使用異地備援的備份保存庫在 hello 的 hello 主要資料中心的災害案例中的特定步驟。 在此情況下，Azure Backup 會使用從 hello 次要區域 toocreate hello 還原虛擬機器的 hello 計算服務。

您也可以使用 PowerShell 來[還原 VM](../../backup/backup-azure-vms-automation.md#restore-an-azure-vm)，或[從還原的磁碟建立新的 VM](../../backup/backup-azure-vms-automation.md#create-a-vm-from-restored-disks)。

## <a name="alternative-solution-consistent-snapshots"></a>替代解決方案：一致性快照

如果您無法 toouse hello Azure Backup 服務，您可以實作自己的備份機制使用快照集。 它是複雜的 toocreate 一致的快照集由 VM 使用的所有磁碟，然後再複寫這些快照集 tooanother 區域。 基於這個理由，Azure 會考慮更好的選項，比建置自訂解決方案運用 hello 備份服務。 如果您使用 GRS/RA-GRS 儲存體的磁碟，快照集將會自動複寫的 tooa 次要資料中心。 如果您使用 LRS 儲存體的磁碟，您將自己需要 tooreplicate hello 資料。 如需詳細資訊，請參閱[以增量快照備份 Azure 非受控 VM 磁碟](../../virtual-machines/windows/incremental-snapshots.md)。

快照集是物件在特定時間點的表示。 快照集將會產生計費的 hello 增量資料大小的 hello 它保存。 如需詳細資訊，請參閱[建立 Blob 快照集](../blobs/storage-blob-snapshots.md)。

### <a name="creating-snapshots-while-hello-vm-is-running"></a>建立快照集時 hello VM 正在執行

時，您可以採取快照集隨時 hello VM 正在執行，如果仍有正在串流處理 toohello 磁碟的資料，而且 hello 快照集可能包含部分中的作業。 此外，如果涉及多個磁碟，hello 的不同磁碟的快照集可能會發生在不同的時間，這表示這些快照集可能不一致。 等量磁碟區特別會有此問題，如果在備份期間發生變更，其中所包含的檔案可能會損毀。

tooavoid 這種情況下，hello 備份程序必須實作 hello 下列步驟：

1.  凍結所有 hello 磁碟

2.  排清所有暫止的寫入 hello

3.  然後，[建立 blob 的快照集](../blobs/storage-blob-snapshots.md)針對所有 hello 磁碟

某些 Windows 應用程式，例如 SQL Server 提供的協調備份機制，透過 VSS toocreate 應用程式一致備份。 On Linux，您可以使用 fsfreeze 這類工具來協調 hello 磁碟，將會提供檔案一致的備份，但是應用程式不一致的快照集。 此程序很複雜，因此您應該考慮使用 [Azure 備份](../../backup/backup-azure-vms-introduction.md)，或是已實作此作業的協力廠商備份解決方案。

hello 上述程序將會導致協調所有 hello VM 磁碟，代表特定時間點檢視 hello VM 的快照集的集合。 這是備份的還原點的 hello VM。 您可以重複 hello 程序，在排定的時間間隔 toocreate 定期備份。 請參閱以下的 hello 步驟太[複製 hello 備份 tooanother 區域](#copy-the-snapshots-to-another-region)dr。

### <a name="creating-snapshots-while-hello-vm-is-offline"></a>建立快照集時 hello VM 處於離線狀態

另一個選項 toocreate 一致的備份正在關機而關閉 hello VM 和擷取 blob 的每個磁碟的快照集。 這比協調執行中 VM 的快照集更容易，但需要停機幾分鐘。 若要進行此程序，請遵循下列步驟：

1. 關閉 hello VM。

2. 建立每個 VHD Blob 的快照集，只需幾秒鐘的時間。

    toocreate 快照集，您可以使用[PowerShell](storage-powershell-guide-full.md#how-to-manage-azure-blob-snapshots)，hello [Azure 儲存體的 Rest API](https://msdn.microsoft.com/library/azure/ee691971.aspx)， [Azure CLI](https://docs.microsoft.com/azure/xplat-cli-install)，或其中一個 hello Azure 儲存體用戶端程式庫例如[hello.NET 的儲存體用戶端程式庫](https://msdn.microsoft.com/library/azure/hh488361.aspx)。

3. 啟動 hello VM，結束 hello 停機時間。 通常在幾分鐘內完成 hello 整個程序。

此程序會產生所有 hello 磁碟，提供 hello VM 備份的還原點的一致快照的集合。 請參閱下面的 hello 步驟 toocopy hello 快照 tooanother 區域 dr。

### <a name="copy-hello-snapshots-tooanother-region"></a>複製 hello 快照 tooanother 區域

建立單獨的 hello 快照集可能無法完全 dr。 您也必須將複寫 hello 快照集備份 tooanother 區域。

如果您使用 GRS 或 RA-GRS 的磁碟，然後 hello 快照集都會複寫的 toohello 次要區域自動。 可能有幾分鐘的延遲 hello 複寫之前，如果 hello 主要資料中心停機 hello 快照集完成複寫之前，您將無法從 hello 次要資料中心可以 tooaccess hello 快照集。 這個 hello 可能性很小。

> [!Note] 
> 只需 GRS 或 RA-GRS 帳戶中的 hello 磁碟不會保護 hello VM 從損毀。 您還必須建立一致性快照或使用 Azure 備份。 這是必要的 toorecover VM tooa 一致的狀態。

如果您使用 LRS，則必須建立 hello 快照集之後，立即複製 hello 快照 tooa 不同儲存體帳戶。 hello 複製目標可能是 LRS 儲存體帳戶在不同區域中，導致遠端的區域中的 hello 複製。 您也可以在 hello 複製 hello 快照 tooan RA-GRS 儲存體帳戶相同的區域。 在此情況下，hello 快照集將會延遲複寫的 toohello 遠端次要區域。 您的備份會 hello 複製和複寫完成之後，受保護從 hello 主要站台的損毀。

toocopy dr 您增量快照有效率地檢閱中的 hello 指示[備份 Azure 增量快照集的未受管理的 VM 磁碟](../../virtual-machines/windows/incremental-snapshots.md)。

![](./media/storage-backup-and-disaster-recovery-for-azure-iaas-disks/backup-and-disaster-recovery-for-azure-iaas-disks-2.png)   

### <a name="recovery-from-snapshots"></a>從快照集復原

tooretrieve 快照集，將它複製 toomake 新的 blob。 如果您從 hello 主要帳戶複製 hello 快照集，您可以複製 hello hello 快照集，因此還原 hello 磁碟 toohello 快照集; toohello 基底 blob 之上快照集這稱為升級 hello 快照集。 如果您從次要帳戶 （在 hello 的 RA-GRS） 複製 hello 快照集備份，則必須複製 tooa 主要帳戶。 您可以將快照集複製[使用 PowerShell](storage-powershell-guide-full.md#how-to-copy-a-snapshot-of-a-blob)或使用 hello AzCopy 公用程式。 如需詳細資訊，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。

在 hello 案例的 Vm 中有多個磁碟，您必須複製所有屬於相同協調的 hello hello 快照集還原點。 一旦您複製 hello 快照 toowritable VHD blob，您可以使用 hello blob toorecreate 使用 hello 範本 hello VM 的 VM。

## <a name="other-options"></a>其他選項

### <a name="sql-server"></a>SQL Server

在 VM 中執行的 SQL Server 有它自己的內建功能 toobackup 您 SQL Server 資料庫 tooAzure Blob 儲存體或檔案共用。 如果 GRS 或 RA-GRS hello 儲存體帳戶，您可以使用存取 hello 儲存體帳戶的次要資料中心的災害，hello 事件中的這些備份 hello 相同的限制，如先前所討論。 如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的備份與還原](../../virtual-machines/windows/sql/virtual-machines-windows-sql-backup-recovery.md)。 在加法 toobackup 與還原、 [SQL Server Alwayson 可用性群組](../../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md)可以維護次要複本的資料庫 toogreatly 減少 hello 災害復原時間。

## <a name="other-considerations"></a>其他考量

這篇文章討論如何 toobackup 或採取快照集的 Vm 和其磁碟 toosupport 災害復原，以及如何 toouse 這些 toorecover。 使用 hello Azure Resource Manager 模型時，許多人範本 toocreate 其 Vm 和其他基礎結構在 Azure 中使用。 您可以使用範本 toocreate 具有 hello VM 相同的設定每一次。 如果您使用自訂映像建立 Vm 時，您也必須確定您的映像受到使用 RA-GRS 帳戶 toostore 它們。

因此，備份程序可能包含下列兩項：

1. 備份 hello 資料 （磁碟）
2. 備份 hello 組態 （範本、 自訂映像）

視您選擇 hello 備份選項，您可能必須 hello 資料和 hello 組態 toohandle hello 備份或 hello 備份服務可能會為您處理所有作業。

## <a name="appendix---understanding-hello-impact-of-lrs-grs-and-ra-grs"></a>附錄-了解的 LRS、 GRS 與 RA-GRS hello 影響

對於 Azure 中的儲存體帳戶而言，有三種資料備援類型可視為與災害復原相關，那就是本地備援 (LRS)、異地備援 (GRS) 或具有讀取權限的異地備援 (RA-GRS)。 

本機備援儲存體 (LRS) 會保留三份 hello hello 中的資料相同的資料中心。 在撰寫 hello 資料時，傳回成功之前 toohello 呼叫端，因此您知道它們完全相同，會更新所有三個複本。 您的磁碟不受本機失敗，因為它是非常不可能，會在 hello 影響所有的三個複本相同的時間。 LRS 的 hello 案例中，在沒有任何的地理備援性，因此 hello 磁碟無法防止可能會影響整個資料中心或儲存體單位的嚴重失敗。

GRS 和 RA-GRS，三份資料會保留在 hello 主要區域中 （由您已選取），而對應的次要區域 （設定 azure） 中保留三份詳細資料。 例如，如果您將資料儲存在美國西部、 hello 資料會複寫的 tooEast 美國。 這是以非同步的方式，且更新 toohello 主要與次要之間有一些延遲。 Hello 磁碟 hello 次要站台上的複本都符合每個磁碟為基礎 （hello 延遲），但可能不同步的多個作用中磁碟的複本**彼此**。 需要 toohave 跨多個磁碟、 一致的快照集一致的複本。

hello GRS 和 RA-GRS 之間的主要差異在於含 RA-GRS，您可以閱讀 hello 次要複本在任何時間。 如果沒有將 hello 主要區域中的 hello 資料呈現為無法存取的問題，hello Azure 團隊會讓每個投入時間 toorestore 存取。 雖然主要 hello 已關閉，如果您有啟用 RA-GRS，您可以存取 hello hello 次要資料中心中的資料。 因此，如果您計劃從 hello 複本 tooread hello 主要時無法存取，然後 RA-GRS 應該考量。

如果證明 toobe 顯著的中斷，hello Azure 團隊可能會觸發地理容錯移轉，然後變更 hello 主要 DNS 項目 toopoint toosecondary 儲存體。 此時，如果您有任一個 GRS 或 RA-GRS 啟用，您可以存取使用 toobe hello 次要的 hello 區域中的 hello 資料。 換句話說，如果您的儲存體帳戶是 GRS 和有問題，您可以存取 hello 次要儲存體地理容錯移轉時。

如需詳細資訊，請參閱[如果 Azure 儲存體中斷，就會發生何種 toodo](storage-disaster-recovery-guidance.md)。 

請注意，Microsoft 會控制是否發生容錯移轉。 容錯移轉不是針對每個儲存體帳戶所控制，因此不會由個別客戶來決定。 tooimplement 災害復原的特定儲存體帳戶或虛擬機器的磁碟，您必須使用先前所述，本文章中的 hello 技巧。
