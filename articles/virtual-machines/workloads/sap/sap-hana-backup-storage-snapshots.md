---
title: "aaaSAP HANA Azure 備份為基礎儲存快照集 |Microsoft 文件"
description: "備份 Azure 虛擬機器上的 SAP HANA 有兩種主要做法，本文涵蓋以儲存體快照集為基礎的 SAP HANA 備份"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>以儲存體快照集為基礎的 SAP HANA 備份

## <a name="introduction"></a>簡介

這是與 SAP HANA 備份相關的三篇系列文章的其中一篇。 [備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md)上開始使用提供的概觀和資訊和[SAP HANA Azure 備份檔案層級上](sap-hana-backup-file-level.md)涵蓋 hello 以檔案為基礎的備份選項。

當使用單一執行個體全部的一個示範系統的 VM 備份的功能，其中一個應該考慮而不是管理在 hello 作業系統層級的 HANA 備份 VM 備份。 替代方式是 tootake Azure blob 快照集 toocreate 份個別的虛擬磁碟，也就是附加的 tooa 虛擬機器，然後保留 hello HANA 資料檔案。 但是，關鍵在於當建立 VM 的備份或磁碟快照時 hello 系統已啟動並執行應用程式一致性。 請參閱_建立儲存體的快照集時，SAP HANA 資料一致性_hello 相關文件中[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md)。 SAP HANA 有個功能支援這類的儲存體快照集。

## <a name="sap-hana-snapshots"></a>SAP HANA 快照集

SAP HANA 中有個功能支援建立儲存體快照集。 不過，年 12 月從 2016年開始，沒有限制 toosingle 容器系統。 多租用戶容器設定不支援這類資料庫快照集 (請參閱[建立儲存體快照集 (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm))。

其運作如下：

- 起始 hello SAP HANA 快照集，準備儲存快照集
- 執行 hello 儲存快照集 (快照集，例如 Azure blob)
- 確認 hello SAP HANA 快照集

![這個螢幕擷取畫面顯示透過 SQL 陳述式建立的 SAP HANA 資料快照集](media/sap-hana-backup-storage-snapshots/image011.png)

這個螢幕擷取畫面顯示透過 SQL 陳述式建立的 SAP HANA 資料快照集。

![hello 然後快照集也會出現在 SAP HANA Studio 中的 hello 備份類別目錄](media/sap-hana-backup-storage-snapshots/image012.png)

hello 然後快照集也會出現在 SAP HANA Studio 中的 hello 備份類別目錄。

![在磁碟上，hello 快照集顯示在 hello SAP HANA 資料目錄](media/sap-hana-backup-storage-snapshots/image013.png)

在磁碟上，hello 快照會在顯示 hello SAP HANA 資料目錄。

其中一個有 tooensure hello 檔案系統一致性也會保證在 SAP HANA hello 快照準備模式時，執行 hello 儲存快照集之前。 請參閱_建立儲存體的快照集時，SAP HANA 資料一致性_hello 相關文件中[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md)。

一旦完成 hello 儲存快照集後，就會是重要 tooconfirm hello SAP HANA 快照集。 沒有對應的 SQL 陳述式 toorun： 備份資料關閉快照集 (請參閱[備份資料關閉快照集陳述式 （備份和復原）](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm))。

> [!IMPORTANT]
> 確認 hello HANA 快照集。 因為太&quot;上寫入複製&quot;SAP HANA 可能需要額外的磁碟空間，在快照集準備模式中，而且不可能 toostart 新的備份之前確認 hello SAP HANA 快照集。

## <a name="hana-vm-backup-via-azure-backup-service"></a>透過 Azure 備份服務備份 HANA VM

年 12 月從 2016年開始，不是適用於 Linux Vm hello hello Azure 備份服務的備份代理程式。 使用 Azure 備份 toomake hello 檔案/目錄層級，其中會複製 SAP HANA 備份檔案 tooa Windows VM，然後使用 hello 備份代理程式。 否則，完整 Linux VM 備份是可透過 hello Azure Backup 服務。 請參閱[中 Azure Backup 功能概觀 hello](../../../backup/backup-introduction-to-azure-backup.md) toofind 深入了解。

hello Azure 備份服務提供選項 tooback，並還原 VM。 此服務和其運作方式的詳細資訊可以在 hello 文章中找到[規劃 VM 備份基礎結構在 Azure 中的](../../../backup/backup-azure-vms-introduction.md)。

有兩個重要的考量，根據 toothat 發行項：

_&quot;針對 Linux 虛擬機器，檔案一致的備份是可行的因為 Linux 沒有對等平台 tooVSS。&quot;_

_&quot;應用程式需要 tooimplement 自己&quot;v-table 修正&quot;機制 hello 上的還原資料。&quot;_

因此，一個具有 toomake 確定 hello 備份啟動時，SAP HANA 是一致的狀態，在磁碟上。 請參閱_SAP HANA 快照_hello 文件稍早所述。 但是當 SAP HANA 保持在此快照集準備模式中時，還有潛在的問題。 如需詳細資訊，請參閱[建立儲存體快照集 (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)。

這篇文章中提到︰

_&quot;強烈建議 tooconfirm 或已在建立之後儘速放棄儲存體的快照集。正在準備 hello 儲存快照集，或建立，hello 時遭到凍結時快照集相關的資料。在 hello 快照集相關的資料仍已凍結，仍可以進行變更 hello 資料庫中。這類變更不會凍結變更的快照集相關的資料 toobe hello。相反地，hello 變更寫入 toopositions hello 分開 hello 儲存快照集的資料區域中。變更也會寫入 toohello 記錄檔。不過，hello 長 hello 快照相關資料會保留已凍結，hello 多個資料磁碟區可以成長的 hello。&quot;_

Azure 備份會負責 hello 檔案系統一致性，透過 Azure VM 擴充功能。 這些擴充功能沒有獨立版本，只能結合 Azure 備份服務使用。 不過，它仍然是需求 toomanage SAP HANA 快照 tooguarantee 應用程式一致性。

Azure 備份有兩個主要階段︰

- 建立快照集
- 傳送資料 toovault

一旦完成 hello Azure 備份服務階段的快照，所以無法確認 hello SAP HANA 快照集。 可能需要幾分鐘的時間 toosee hello Azure 入口網站中。

![此圖將顯示在 Azure 備份服務的 hello 備份工作清單的一部分](media/sap-hana-backup-storage-snapshots/image014.png)

此圖顯示 hello Azure Backup 服務，這是使用的 tooback hello HANA 測試 VM 的備份工作清單的一部分。

![tooshow hello 工作詳細資料，按一下 hello hello Azure 入口網站中的備份工作](media/sap-hana-backup-storage-snapshots/image015.png)

tooshow hello 工作詳細資料，按一下 hello hello Azure 入口網站中的備份作業。 在這裡，其中一個可以看到 hello 兩個階段。 可能需要幾分鐘的時間之前為已完成，它會顯示 hello 快照集 」 階段。 大部分的 hello 時間花在 hello 資料傳輸的階段。

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>透過 Azure 備份服務進行 HANA VM 自動備份

一旦完成 hello Azure Backup 的快照集階段，如稍早所述但很有幫助 tooconsider 自動化，因為系統管理員可能無法監視 hello hello Azure 入口網站中的備份工作清單，其中一個無法手動確認 hello SAP HANA 快照集。

以下說明如何透過 Azure PowerShell Cmdlet 達成。

![建立 hello 名稱 hana backup vault 的 Azure 備份服務](media/sap-hana-backup-storage-snapshots/image016.png)

Azure Backup 服務建立 hello 名稱&quot;hana-備份-保存庫。&quot; hello PS 命令**Get AzureRmRecoveryServicesVault-命名 hana 備份保存庫**擷取 hello 對應的物件。 這是物件然後 hello 下圖所示，使用的 tooset hello 備份內容。

![Hello 備份工作正在進行中的使用者可以檢查](media/sap-hana-backup-storage-snapshots/image017.png)

之後設定 hello 正確內容中，一個可檢查 hello 備份工作目前正在進行，然後尋找其工作詳細資料。 hello 項子工作清單顯示是否 hello 快照 hello Azure 備份的工作階段已完成：

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![在迴圈直到結果 tooCompleted 輪詢 hello 值](media/sap-hana-backup-storage-snapshots/image018.png)

一旦 hello 工作詳細資料儲存在變數中，它是只需 PS 語法 tooget toohello 第一個陣列的項目，並擷取 hello 狀態值。 toocomplete hello 自動化指令碼，直到迴圈中的輪詢 hello 值會太&quot;已完成。&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>透過 Azure 備份服務的 HANA 授權金鑰和 VM 還原

hello Azure 備份服務是設計的 toocreate 新的 VM 進行還原。 沒有計畫就在此時 toodo&quot;就地&quot;還原現有的 Azure VM。

![此圖將顯示 hello Azure 入口網站中的 hello Azure 服務的 hello 還原選項](media/sap-hana-backup-storage-snapshots/image019.png)

此圖會顯示 hello Azure 入口網站中的 hello Azure 服務的 hello 還原選項。 其中一個可以選擇在還原期間建立的 VM，或還原 hello 磁碟。 還原 hello 磁碟，之後仍然需要有 toocreate 其最上層的新 VM。 每當建立新的 VM 取得 Azure 的 hello 唯一 VM 識別碼變更 (請參閱[存取和使用 Azure VM 的唯一識別碼](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/))。

![此圖將顯示 hello Azure VM 的唯一識別碼之前和之後透過 Azure 備份服務的 hello 還原](media/sap-hana-backup-storage-snapshots/image020.png)

透過 Azure 備份服務的 hello 還原前後，此圖會顯示 hello Azure VM 的唯一識別碼。 hello SAP 硬體，該金鑰用於 SAP 的授權，使用此唯一 VM 識別碼。 因此，新的 SAP 授權有 toobe VM 還原之後才安裝。

期間 hello 建立這個備份指南在預覽模式中輸入新的 Azure 備份功能。 它可讓檔案層級還原，根據拍攝 hello VM 備份的 hello VM 快照集。 這可避免 hello 需要 toodeploy 新的 VM，因此唯一 VM 識別碼會保留 hello hello 相同，而且無須任何新的 SAP HANA 授權金鑰。 有關這項功能的詳細文件，將會在經過完整測試之後提供。

Azure 備份將最終允許備份的個別 Azure 的虛擬磁碟，加上檔案及目錄內 hello VM。 Azure 備份的主要優點是其所有 hello 備份，毋需 toodo 儲存 hello 客戶的管理它。 如果還原有必要，Azure 備份將會選取 hello 正確備份 toouse。

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>透過手動磁碟快照集進行 SAP HANA VM 備份

而不是使用 hello Azure Backup 服務，其中一個可以設定個別的備份解決方案，藉由建立的手動透過 PowerShell 的 Azure Vhd blob 快照集。 請參閱[使用 blob 快照集，使用 PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) hello 步驟的說明。

它提供更大的彈性，但無法解析 hello 本文件稍早所述的問題：

- 您仍然必須確定 SAP HANA 處於一致的狀態
- 無法覆寫 hello 作業系統磁碟，即使有的 hello VM 解除配置的錯誤訊息因為租用。 僅適用於之後刪除 hello VM，而這樣會導致 tooa 新唯一 VM 識別碼和 hello 需要 tooinstall 新的 SAP 授權。

![它是可能 toorestore 只有 hello 資料磁碟的 Azure VM](media/sap-hana-backup-storage-snapshots/image021.png)

它可能 toorestore 只有 hello 資料磁碟的 Azure VM，避免取得新的唯一 VM 識別碼 hello 問題，因此，失效 hello SAP 授權：

- Hello 測試兩個 Azure 資料磁碟已附加的 tooa VM，並在其上已定義的軟體 RAID 
- 已經利用 SAP HANA 快照集功能確認的 SAP HANA 處於一致的狀態
- 檔案系統凍結 (請參閱_建立儲存體的快照集時，SAP HANA 資料一致性_hello 相關文件中[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md))
- 從這兩個資料磁碟建立 blob 快照集
- 檔案系統解除凍結
- 確認 SAP HANA 快照集
- toorestore hello 資料磁碟，hello VM 已關閉，而這兩個磁碟中斷連結
- Hello 磁碟中斷連結之後才已被覆寫 hello 先前的 blob 快照集
- 附加 hello 還原虛擬磁碟，然後再次 toohello VM
- 起始 hello VM hello 軟體 RAID 可以正常運作正常，而且已設定回 toohello blob 上的所有快照集時間之後
- HANA 已設定回 toohello HANA 快照集

如果資料可能 tooshut 向 SAP HANA hello blob 快照集之前，會是較不複雜 hello 程序。 在此情況下，其中一個無法略過 hello HANA 快照集，如果沒有其他正在進行的作業在 hello 系統中，也略過 hello 檔案系統凍結。 增加的複雜度進入 hello 圖片時，它需要 toodo 快照集的所有項目仍在線上運作。 請參閱_建立儲存體的快照集時，SAP HANA 資料一致性_hello 相關文件中[備份指南的 SAP HANA Azure 虛擬機器上](sap-hana-backup-guide.md)。

## <a name="next-steps"></a>後續步驟
* [Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)提供快速入門的概觀和詳細資訊。
* [SAP HANA 備份為基礎的檔案層級](sap-hana-backup-file-level.md)涵蓋 hello 以檔案為基礎的備份選項。
* toolearn tooestablish 高可用性和 Azure （大型執行個體） 上的 SAP HANA 災害復原計劃的看到[SAP HANA （大型執行個體） 高可用性和災害復原在 Azure 上的](hana-overview-high-availability-disaster-recovery.md)。
