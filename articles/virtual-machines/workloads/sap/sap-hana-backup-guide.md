---
title: "aaaBackup 指南的 SAP HANA Azure 虛擬機器上 |Microsoft 文件"
description: "SAP HANA 備份指南說明備份 Azure 虛擬機器上 SAP HANA 的兩種主要做法"
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
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Azure 虛擬機器上的 SAP HANA 備份指南

## <a name="getting-started"></a>開始使用

Azure 虛擬機器上執行的 SAP hana hello 備份指南只會描述 Azure 相關的主題。 針對一般 SAP HANA 備份相關項目，請查看 hello SAP HANA 文件 (請參閱_SAP HANA 備份文件_本文稍後的)。

hello 這篇文章的焦點是兩種主要備份可能性 SAP HANA Azure 虛擬機器上：

- HANA 備份 toohello 檔案系統中 Azure Linux 虛擬機器 (請參閱[SAP HANA Azure 備份檔案層級上](sap-hana-backup-file-level.md))
- HANA 備份為基礎儲存體使用手動 hello Azure 儲存體 blob 快照集功能的快照集或 Azure 備份服務 (請參閱[SAP HANA 備份為基礎儲存快照集](sap-hana-backup-storage-snapshots.md))

SAP HANA 提供 API，可讓協力廠商備份工具 toointegrate 直接與 SAP HANA 的備份。 （這是不在本指南的 hello 範圍內）。根據此 API，目前 SAP HANA 與 Azure 備份服務沒有任何直接整合。

SAP HANA 正式支援 Azure VM 類型 GS5 上做為單一執行個體的額外限制 tooOLAP 工作負載 (請參閱[尋找認證 IaaS 平台](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)hello SAP 網站上)。 這篇文章將會更新為新的供應項目，您就可以使用 Azure 上的 SAP HANA。

Azure 上另外還有一個 SAP HANA 的混合式解決方案，其中的 SAP HANA 是在實體伺服器上非虛擬化的執行。 不過，此 SAP HANA Azure 備份指南涵蓋純 Azure 環境，即 SAP HANA 在 Azure VM 中執行，而不是 SAP HANA 在「大型執行個體」&quot;&quot;上執行。針對此備份解決方案在「大型執行個體」&quot;&quot;上執行以儲存體快照集為基礎的備份，如需詳細資訊請參閱 [Azure 上的 SAP HANA (大型執行個體) 概觀和架構](hana-overview-architecture.md)。

Azure 上支援的 SAP 產品資訊可在 [SAP Note 1928533](https://launchpad.support.sap.com/#/notes/1928533) 之中找到。

hello 下列三個圖表概觀 hello SAP HANA 備份目前使用原生的 Azure 功能的選項，也會顯示三個潛在未來備份的案例。 hello 相關文章[SAP HANA Azure 備份檔案層級上](sap-hana-backup-file-level.md)和[SAP HANA 備份為基礎儲存快照集](sap-hana-backup-storage-snapshots.md)說明這些選項的詳細資料，包括適用於 SAP 的大小和效能考量HANA 備份多重數 tb 的大小。

![此圖將顯示兩種可能性儲存 hello 目前 VM 狀態](media/sap-hana-backup-guide/image001.png)

此圖顯示 hello 可能性儲存 hello 目前 VM 的狀態，已透過 Azure 備份服務或 VM 磁碟的手動快照集。 這種方法，也為 &#39; 沒有 toomanage SAP HANA 備份。 hello 挑戰的 hello 磁碟快照集是案例的檔案系統一致性，且應用程式一致的磁碟狀態。 hello 章節中的 hello 一致性主題會討論_建立儲存體的快照集時，SAP HANA 資料一致性_本文稍後。 功能以及限制的 Azure 備份服務相關的 tooSAP HANA 備份也將在本文稍後討論。

![此圖將顯示選項，以取得 SAP HANA 檔案內 hello VM 備份](media/sap-hana-backup-guide/image002.png)

此圖中顯示選項取得 hello VM，在 SAP HANA 檔案備份，然後再將 HANA 備份檔案的地方使用不同的工具。 建立 HANA 備份需要的時間比以快照集為基礎的備份解決方案更多，但具有整體性與一致性的優點。 本文稍後將提供更詳細的說明。

![此圖顯示未來可能的 SAP HANA 備份案例](media/sap-hana-backup-guide/image003.png)

此圖顯示未來可能的 SAP HANA 備份案例。 如果 SAP HANA 允許從次要複寫建立備份，會加入額外的備份策略選項。 目前不可能根據 tooa hello SAP HANA Wiki 中的文章：

_&quot;它是在 hello 次要端可能 tootake 備份嗎？_

_否，目前您只能取得資料和記錄備份 hello 主要端上。如果已啟用自動記錄備份之後接管 toohello 次要端，, 自動將那里寫入 hello 記錄備份。&quot;_

## <a name="sap-resources-for-hana-backup"></a>HANA 備份的 SAP 資源

### <a name="sap-hana-backup-documentation"></a>SAP HANA 備份文件

- [簡介 tooSAP HANA 管理](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [規劃備份和復原策略](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)
- [使用 ABAP DBACOCKPIT 排程 HANA 備份](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html)
- [排程資料備份 (SAP HANA Cockpit)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm)
- [SAP Note 1642148](https://launchpad.support.sap.com/#/notes/1642148) 中的 SAP HANA 備份常見問題集
- [SAP Note 2039883](https://launchpad.support.sap.com/#/notes/2039883) 中的 SAP HANA 資料庫和儲存體快照集的常見問題集
- [SAP Note 1820529](https://launchpad.support.sap.com/#/notes/1820529) 中的不適用於備份和復原的網路檔案系統

### <a name="why-sap-hana-backup"></a>為什麼要使用 SAP HANA 備份？

Azure 儲存體提供可用性和可靠性 hello 現成 (請參閱[簡介 tooMicrosoft Azure 儲存體](../../../storage/common/storage-introduction.md)如需有關 Azure 儲存體)。

最小值的 hello&quot;備份&quot;是 toorely 上 hello Azure Sla，保留 hello Azure Vhd 附加的 toohello SAP HANA 伺服器 VM 上的 SAP HANA 資料和記錄檔。 這個方法會涵蓋 VM 失敗，但不是可能損害 toohello SAP HANA 資料和記錄檔或邏輯錯誤，例如不小心刪除資料或檔案。 備份也是基於合規性或法律因素而有其必要。 簡單地說，一定需要 SAP HANA 備份。

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>如何 tooverify 正確性的 SAP HANA 備份
使用儲存體快照集時，建議在不同的系統上執行測試還原。 此方法提供方式 tooensure 備份符合預期的備份和還原工作的正確和內部程序。 雖然這是嚴重的障礙內部，它是 hello 定域機組中的更容易 tooaccomplish 方法所需的資源暫時提供此用途的。

請記住，光是簡單執行還原，然後確認 HANA 有在執行是不夠的。 在理想情況下，其中一個應該執行資料表的一致性檢查 toobe 確定該 hello 還原資料庫很好。 SAP HANA 提供數種一致性檢查，如 [SAP Note 1977584](https://launchpad.support.sap.com/#/notes/1977584) 中所述。

Hello 資料表的一致性檢查的相關資訊也可以在 hello SAP 網站上找到[資料表和類別目錄一致性檢查](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b)。

若是進行標準檔案備份，則不需要測試還原。 有兩個 SAP HANA 工具可協助的 toocheck 可用的備份進行還原： hdbbackupdiag 和 hdbbackupcheck。 如需有關這些工具的資訊，請參閱[手動檢查是否有可能復原](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm)。

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>比較 HANA 備份與儲存體快照集的優缺點

SAP 規定 &#39; t 給予喜好設定 tooeither HANA 備份與儲存快照集。 它會列出其優缺點，因此一個可以判斷哪些 toouse 視 hello 情況和可用的存放裝置技術而定 (請參閱[規劃您的備份和復原策略](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm))。

在 Azure 中，注意 hello 事實的 hello Azure blob 快照集功能不 &#39; 保證檔案系統一致性的 t (請參閱[使用 blob 快照集，使用 PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/))。 hello 下一節_建立儲存體的快照集時，SAP HANA 資料一致性_，討論有關這項功能的一些考量。

此外，有一個具有 toounderstand hello 的計費方式，本文章中所述經常使用 blob 快照集時：[了解如何快照 snapshots Accrue Charges](/rest/api/storageservices/understanding-how-snapshots-accrue-charges)— 它目前 &#39; t 明顯做為使用 Azure虛擬磁碟。

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>建立儲存體快照集時，SAP HANA 資料的一致性

建立儲存體快照集時，檔案系統和應用程式的一致性是複雜的問題。 要向 SAP HANA tooshut hello 最簡單方式 tooavoid 問題或甚至 hello 整個虛擬機器。 關機在示範或原型，或甚至開發系統上也許可行，但不是生產系統的選項。

在 Azure 上、 其中一個有 tookeep 記住 hello Azure blob 快照集功能不 &#39; t 保證檔案系統一致性。 它會正常運作但是使用 hello SAP HANA 快照集功能，只要沒有相關的只是單一的虛擬磁碟。 但即使是使用單一磁碟，其他項目有 toobe 檢查。 [SAP Note 2039883](https://launchpad.support.sap.com/#/notes/2039883) 中有關於透過儲存體快照集進行 SAP HANA 備份的重要資訊。 例如，它會提及，hello XFS 檔案系統，它是必要的 toorun **xfs\_凍結**啟動儲存體 tooguarantee 一致性的快照集之前 (請參閱[xfs\_freeze(8)-Linux 攔截頁面](https://linux.die.net/man/8/xfs_freeze)如需詳細資訊**xfs\_凍結**)。

一致性的 hello 主題會成為在單一檔案系統位置跨越多個磁碟/磁碟區的情況下甚至更具挑戰性。 例如，使用 mdadm 或 LVM 和串接。 hello 狀態上面所提 SAP 附註：

_&quot;但是請記住以下幾點 hello 儲存系統具有 tooguarantee I/O 一致性，建立每個 SAP HANA 資料磁碟區的儲存體快照集時，也就是 SAP HANA 服務特定的資料磁碟區的快照必須是不可部分完成的作業。&quot;_

假設 XFS 檔案系統跨越四個 Azure 的虛擬磁碟，hello 下列步驟提供一致的快照集，表示 hello HANA 資料區域：

- 準備 HANA 快照集
- 凍結 hello 檔案系統 (例如，使用**xfs\_凍結**)
- 在 Azure 上建立所有必要的 blob 快照集
- 取消凍結 hello 檔案系統
- 確認 hello HANA 快照集

建議是 toouse hello 上述程序中所有的情況下 toobe hello 安全的理由，不論檔案系統上。 或者，如果是單一磁碟或串接，透過 mdadm 或 LVM 跨多個磁碟。

很重要的 tooconfirm hello HANA 快照集。 到期 toohello&quot;上寫入複製&quot;SAP HANA 可能不需要額外的磁碟空間，而在此模式準備快照集。 它 &#39; s 也不可能 toostart 新的備份之前確認 hello SAP HANA 快照集。

Azure 備份服務會使用 Azure VM 延伸模組 tootake care of hello 檔案系統一致性。 這些 VM 擴充功能無法獨立使用。 其中一個仍然有 toomanage SAP HANA 一致性。 請參閱相關文件 hello[檔案層級上的 SAP HANA Azure Backup](sap-hana-backup-file-level.md)如需詳細資訊。

### <a name="sap-hana-backup-scheduling-strategy"></a>SAP HANA 備份排程策略

hello SAP HANA 文章[規劃您的備份和復原策略](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)狀態的基本計劃 toodo 備份：

- 儲存體快照集 (每天)
- 使用檔案或 bacint 格式進行完整的資料備份 (每週一次)
- 自動記錄備份

您可以選擇完全不進行儲存體快照集；可利用 HANA 差別備份來準備它們，例如增量或差異備份 (請參閱[差別備份](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm))。

hello HANA 系統管理指南提供的範例清單。 建議您一次使用下列的備份順序的 hello 復原 SAP HANA tooa 特定點：

1. 完整資料備份
2. 差異備份
3. 增量備份 1
4. 增量備份 2
5. 記錄備份

關於 toowhen 和特定的備份類型應該發生的頻率的確切排程，則不可能 toogive 一般指導方針 — 它是太客戶，而多少資料變更會發生在 hello 系統而定。 一個基本從 SAP 端，可視為一般指引，建議 toomake 一個完整 HANA 備份每週一次。
有關記錄檔備份，請參閱 hello SAP HANA 文件[記錄備份](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm)。

SAP 也建議您某些環境的 hello 備份類別目錄 tookeep 維護從無限成長 (請參閱[備份類別目錄和備份存放例行性](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm))。

### <a name="sap-hana-configuration-files"></a>SAP HANA 組態檔

中的 hello 常見問題集中所述[SAP 附註 1642148](https://launchpad.support.sap.com/#/notes/1642148)，hello SAP HANA 組態檔不是標準的 HANA 備份的一部分。 它們不是基本 toorestore 系統。 hello 還原之後無法手動變更 hello HANA 組態。 萬一其中一個希望 tooget hello 相同的自訂組態 hello 還原程序，它是必要 tooback hello HANA 組態檔案分開。

如果標準 HANA 備份即將 tooa 專用 HANA 備份的檔案系統，其中也無法複製 hello 設定檔 toohello 相同備份的檔案系統，並再複製所有要一起 toohello 儲存體目的地的項目很棒的 blob 儲存體。

### <a name="sap-hana-cockpit"></a>SAP HANA Cockpit

SAP HANA Cockpit 提供監視和管理 SAP HANA 透過瀏覽器的 hello 的可能性。 它也可讓處理的 SAP HANA 備份，並因此可做為替代 tooSAP HANA Studio 及 ABAP DBACOCKPIT (請參閱[SAP HANA Cockpit](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm)如需詳細資訊)。

![此圖將顯示 hello SAP HANA Cockpit 資料庫管理畫面](media/sap-hana-backup-guide/image004.png)

此圖顯示 hello SAP HANA Cockpit 資料庫管理畫面及 hello 上剩餘的 hello 備份 磚。 文件都看到 hello 備份磚登入帳戶需要適當的使用者權限。

![備份正在進行時，可以在 SAP HANA Cockpit 中監視備份](media/sap-hana-backup-guide/image005.png)

它們會持續進行，並在它完成時，所有的 hello 備份詳細資料可用時，可以在 SAP HANA Cockpit 監視備份。

![在 Azure SLES 12 VM 及 Gnome 桌面上使用 Firefox 的範例](media/sap-hana-backup-guide/image006.png)

從 Windows Azure VM 進行 hello 上一個螢幕擷取畫面。 這一個是 Gnome 桌面搭配 Azure SLES 12 VM 使用 Firefox 的範例。 它會顯示 hello 選項 toodefine SAP HANA 備份排程在 SAP HANA Cockpit。 也可以看到其中一個，日期/時間做為前置詞 hello 備份檔案的建議。 在 SAP HANA Studio hello 預設前置詞是&quot;完成\_資料\_備份&quot;時執行的完整檔案備份。 建議使用唯一的前置詞。

### <a name="sap-hana-backup-encryption"></a>SAP HANA 備份的加密

SAP HANA 提供加密資料和記錄的功能。 如果未加密 SAP HANA 資料和記錄檔，然後 hello 備份也不會加密。 它已啟動 toohello 客戶 toouse 某種形式的協力廠商解決方案 tooencrypt hello SAP HANA 備份。 請參閱[資料和記錄檔磁碟區加密](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm)toofind SAP HANA 加密深入了解。

在 Microsoft Azure 客戶無法使用 hello IaaS VM 加密功能 tooencrypt。 比方說，其中一個可以使用專用的資料磁碟附加的 toohello VM，而是使用的 toostore SAP HANA 備份，接著建立這些磁碟的複本。

Azure 備份服務可以處理加密的 Vm 磁碟 (請參閱[tooback 向上及還原加密使用 Azure 備份的虛擬機器](../../../backup/backup-azure-vms-encryption.md))。

另一個選項可能會 toomaintain hello SAP HANA VM 和其磁碟未加密，而且 hello SAP HANA 備份檔案儲存在加密已啟用的儲存體帳戶 (請參閱[Azure 儲存體服務加密待用資料](../../../storage/common/storage-service-encryption.md)).

## <a name="test-setup"></a>測試設定

### <a name="test-virtual-machine-on-azure"></a>測試 Azure 上的虛擬機器

SAP HANA GS5 Azure VM 中的安裝用於 hello 下列備份/還原測試。

![此圖顯示一部分 hello hello HANA 測試 VM 的 Azure 入口網站總覽](media/sap-hana-backup-guide/image007.png)

此圖中顯示部分 hello hello HANA 測試 VM 的 Azure 入口網站的概觀。

### <a name="test-backup-size"></a>測試備份大小

![此圖取自 HANA Studio 中的 hello 備份主控台，並顯示 hello 備份檔案大小為 229 GB hello HANA 索引伺服器](media/sap-hana-backup-guide/image008.png)

空的資料表已填滿資料 tooget 與備份的資料大小總計超過 200 GB tooderive 實際的效能資料。 hello 圖取自 HANA Studio 中的 hello 備份主控台，並顯示 hello 備份檔案大小為 229 GB hello HANA 索引伺服器。 Hello 測試中，使用 hello 預設備份前置詞"COMPLETE_DATA_BACKUP 「 SAP HANA Studio 中。 在實際生產系統中，應該定義更實用的前置詞。 SAP HANA Cockpit 的建議是日期/時間。

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>測試工具 toocopy 直接檔案 tooAzure 儲存體

tootransfer SAP HANA 備份檔案直接 tooAzure blob 儲存體或 Azure 的檔案共用，hello blobxfer 工具已使用，因為它支援目標，以及它可以輕鬆地整合到自動化指令碼，因為 tooits 命令列介面。 hello blobxfer 工具 」 可於[GitHub](https://github.com/Azure/blobxfer)。

### <a name="test-backup-size-estimation"></a>測試備份大小估計

它是 SAP HANA 的重要 tooestimate hello 備份大小。 此預估值的定義 hello 備份檔案大小上限的備份檔案數目，有助於 tooimprove 效能到期 tooparallelism 期間檔案複製。 (詳情稍後在本文中會加以說明。)其中也必須決定 toodo 完整備份或差異備份 （增量或差異）。

幸運的是，沒有簡單的 SQL 陳述式來估計 hello hello 備份檔案大小：**選取\*從 M\_備份\_大小\_估計**(請參閱[評估 hello 空間需要在 hello 檔案系統的一種資料備份](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm))。

![此 SQL 陳述式的 hello 輸出符合幾乎完全 hello 實際大小 hello 完整的資料上的備份磁碟](media/sap-hana-backup-guide/image009.png)

如 hello 測試系統，此 SQL 陳述式的 hello 輸出符合幾乎完全 hello 實際大小 hello 完整的資料上的備份磁碟。

### <a name="test-hana-backup-file-size"></a>測試 HANA 備份檔案大小

![hello HANA Studio 備份主控台可讓一個 toorestrict hello 檔案大小上限的 HANA 備份檔案](media/sap-hana-backup-guide/image010.png)

hello HANA Studio 備份主控台可讓一個 toorestrict hello 檔案大小上限的 HANA 備份檔案。 在 hello 範例環境中，該功能可讓多個較小的備份檔案而不是一個 230 GB 的備份檔案的可能 tooget。 較小的檔案大小對效能有顯著的影響 (請參閱相關文件 hello[檔案層級上的 SAP HANA Azure Backup](sap-hana-backup-file-level.md))。

## <a name="summary"></a>摘要

根據 hello 下表顯示的 Azure 虛擬機器上執行的 SAP HANA 資料庫解決方案 tooback 優缺點 hello 測試結果。

**備份 SAP HANA toohello 檔案系統和複製備份之後檔案 toohello 最後的備份目的地**

|方案                                           |優點                                 |缺點                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|將 HANA 備份保留在 VM 磁碟上                      |沒有額外的管理工作     |耗盡本機 VM 磁碟空間           |
|Blobxfer 工具 toocopy 備份檔案 tooblob 儲存體 |平行處理原則 toocopy 多個檔案、 選擇 toouse 酷炫的 blob 儲存體 | 需額外維護工具和自訂指令碼 | 
|透過 Powershell 或 CLI 進行 blob 複製                    |不需要額外的工具，透過 Azure Powershell 或 CLI 即可完成 |手動程序，客戶有 tootake care of 指令碼和管理的複製 blob 還原|
|複製 tooNFS 共用                                  |備份檔案，而不會影響 hello HANA 伺服器上的其他 VM 上的後續處理|複製程序緩慢|
|Blobxfer 複製 tooAzure 檔案服務                |不會耗盡本機 VM 磁碟上的空間|HANA 備份不支援直接寫入、檔案共用目前的大小限制為 5 TB|
|Azure 備份代理程式                                 | 會是較佳的解決方案         | 目前無法在 Linux 上使用    |



**以儲存體快照集為基礎的 SAP HANA 備份**

|方案                                           |優點                                 |缺點                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Azure 備份服務                               | 允許以 blob 快照集為基礎備份 VM | 當不使用檔案層級還原，需要 hello 建立新的 VM hello 還原程序，表示然後 hello 需要新的 SAP HANA 授權金鑰|
|手動 blob 快照集                              | 彈性 toocreate 和還原特定 VM 磁碟而不需要變更 hello VM 的唯一識別碼|所有的手動工作，已由 hello 客戶 toobe|

## <a name="next-steps"></a>後續步驟
* [SAP HANA Azure 備份檔案層級上](sap-hana-backup-file-level.md)hello 以檔案為基礎的備份選項的描述。
* [SAP HANA 備份為基礎儲存快照集](sap-hana-backup-storage-snapshots.md)hello 儲存快照集式備份選項的描述。
* toolearn tooestablish 高可用性和 Azure （大型執行個體） 上的 SAP HANA 災害復原計劃的看到[SAP HANA （大型執行個體） 高可用性和災害復原在 Azure 上的](hana-overview-high-availability-disaster-recovery.md)。
