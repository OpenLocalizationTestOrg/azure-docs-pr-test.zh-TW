---
title: "aaaSAP HANA Azure Backup，在檔案層級上 |Microsoft 文件"
description: "備份 Azure 虛擬機器上的 SAP HANA 有兩種主要做法，本文涵蓋檔案層級的 SAP HANA Azure 備份"
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
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>檔案層級的 SAP HANA Azure 備份

## <a name="introduction"></a>簡介

這是與 SAP HANA 備份相關的三篇系列文章的其中一篇。 [備份指南的 SAP HANA Azure 虛擬機器上](./sap-hana-backup-guide.md)上開始使用提供的概觀和資訊和[SAP HANA 備份為基礎儲存快照集](./sap-hana-backup-storage-snapshots.md)涵蓋 hello 儲存快照集為基礎的備份選項。

查看 hello Azure VM 大小，其中一個就可以看到 GS5 允許 64 連接的資料磁碟。 在大型的 SAP HANA 系統中，大量磁碟可能已被資料和記錄檔佔據，可能還加上用於最佳磁碟 IO 輸送量的軟體 RAID。 然後 hello 問題是 toostore SAP HANA 備份無法填滿 hello 附加資料磁碟一段時間的檔案的位置？ 請參閱[在 Azure 中 Linux 虛擬機器的大小](../../linux/sizes.md)hello Azure VM 大小的資料表。

目前 SAP HANA 備份還沒有與 Azure 備份服務整合。 hello toomanage 備份/還原 hello 檔案層級是以檔案為基礎的備份透過 SAP HANA Studio 或透過 SAP HANA SQL 陳述式的標準方式。 詳細資訊請參閱 [SAP HANA SQL 和系統檢視參考](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf)。

![此圖將顯示在 SAP HANA Studio hello hello 備份的功能表項目對話方塊](media/sap-hana-backup-file-level/image022.png)

此圖會顯示在 SAP HANA Studio hello hello 備份的功能表項目 對話方塊。 當您選擇型別時&quot;檔案，&quot;一個 hello 檔案系統，SAP HANA 寫入 hello 備份檔案的位置中具有 toospecify 的路徑。 還原 hello 的運作方式相同。

雖然這項選擇聽起來簡單又直接，但仍有一些事要考量。 之前有提到，Azure 虛擬機器可連結的資料磁碟數目有限制。 不可能在 hello 檔案系統中的 hello VM，視 hello 資料庫和磁碟輸送量需求，其中可能包含軟體 hello 大小而定的容量 toostore SAP HANA 備份檔案 RAID 使用跨多個資料，等量磁碟。 在本文稍後提供多種選項，可用於在處理數 TB 資料時，移動這些備份檔案以及管理檔案大小限制和效能。

另一個可以不計總容量提供更多自由的選項是 Azure Blob 儲存體。 雖然單一 blob 也限制的 too1 TB，hello 的單一 blob 容器的總容量目前為 500 TB。 此外，它可讓客戶 hello choice tooselect 所謂&quot;cool&quot; blob 儲存體，具有成本效益。 如需非經常性 blob 儲存體的詳細資訊，請參閱 [Azure Blob 儲存體︰經常性存取與非經常性存取儲存層](../../../storage/blobs/storage-blob-storage-tiers.md)。

額外的安全，則可使用異地備援儲存體帳戶 toostore hello SAP HANA 備份。 如需儲存體帳戶複寫相關的詳細資料，請參閱 [Azure 儲存體複寫](../../../storage/common/storage-redundancy.md)。

一個人將 SAP HANA 備份專用的 VHD 放在異地複寫的專用備份儲存體帳戶。 否則一個無法複製 hello Vhd，以避免 hello SAP HANA 備份 tooa 異地備援儲存體帳戶或 tooa 儲存體帳戶位在不同的區域。

## <a name="azure-backup-agent"></a>Azure 備份代理程式

Azure 備份提供 hello 選項 toonot 只備份完整的 Vm，但也檔案及目錄透過 hello 備份代理程式，其具有 toobe hello 客體作業系統上安裝。 但年 12 月從 2016年開始，此代理程式只支援在 Windows 上 (請參閱[備份使用 hello Resource Manager 部署模型的 Windows 伺服器或用戶端 tooAzure](../../../backup/backup-configure-vault.md))。

因應措施 toofirst 複本 （例如，透過 SAMBA 共用） 的 SAP HANA 備份檔案 tooa 在 Azure 上的 Windows VM，然後從該處使用 hello Azure 備份代理程式。 雖然可行，它會增加複雜度和 hello 備份變慢或還原程序稍微到期 toohello hello Linux 與 hello Windows VM 之間的複製。 不建議 toofollow 這種方法。

## <a name="azure-blobxfer-utility-details"></a>Azure blobxfer 公用程式詳細資料

其中一個 toostore 目錄與 Azure 儲存體上的檔案，可以使用 CLI 或 PowerShell，或開發工具，使用其中一種 hello [Azure Sdk](https://azure.microsoft.com/downloads/)。 也有一個已備妥要使用公用程式，AzCopy，來複製資料 tooAzure 存放區，但是它只是 Windows (請參閱[hello AzCopy 命令列公用程式使用傳輸資料](../../../storage/common/storage-use-azcopy.md))。

因此，使用 blobxfer 來複製 SAP HANA 備份檔案。 blobxfer 是開放原始碼，可從 [GitHub](https://github.com/Azure/blobxfer) 取得，許多客戶在生產環境中使用它。 直接 tooeither Azure blob 儲存體或 Azure 的檔案共用，此工具可讓一個 toocopy 資料。 它也提供各種實用的功能，例如 md5 雜湊、複製含多個檔案的目錄時可使用自動平行處理原則。

## <a name="sap-hana-backup-performance"></a>SAP HANA 備份的效能

![在 SAP HANA Studio hello SAP HANA 備份主控台是這個螢幕擷取畫面](media/sap-hana-backup-file-level/image023.png)

在 SAP HANA Studio hello SAP HANA 備份主控台是這個螢幕擷取畫面。 約有 42 分鐘 toodo hello 備份所需的 hello 230 GB 單一標準的 Azure 儲存體磁碟上附加 toohello HANA VM 使用 XFS 檔案系統。

![這個螢幕擷取畫面的 YaST 位於 hello SAP HANA 測試 VM](media/sap-hana-backup-file-level/image024.png)

這個螢幕擷取畫面是 YaST hello SAP HANA 測試 VM 上。 一個可以如同先前所述，請參閱 SAP HANA 備份的 hello 1 TB 單一磁碟。 花費約有 42 分鐘 toobackup 230 GB。 此外，還連結了五個 200 GB 的磁碟並建立了軟體 RAID md0，而且在這五個 Azure 資料磁碟上串接。

![重複的 hello 相同的備份軟體 RAID 使用等量五個跨連結 Azure 標準儲存體資料磁碟](media/sap-hana-backup-file-level/image025.png)

重複 hello 相同的備份軟體 RAID 使用等量五個跨 42 分鐘 too10 分鐘後關閉附加 Azure 標準儲存體的資料磁碟回到 hello 備份時間。 hello 磁碟附加但不快取 toohello VM。 因此，明顯重要的磁碟寫入輸送量為 hello 備份時間。 其中一個無法再交換器 tooAzure premium 儲存體 toofurther 加速 hello 程序，以獲得最佳效能。 一般而言，生產系統應該使用 Azure 進階儲存體。

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>複製 SAP HANA 備份檔案 tooAzure blob 儲存體

2016 年 12 月的 hello 最佳選項 tooquickly 存放區 SAP HANA 備份檔案是 Azure blob 儲存體。 一個單一的 blob 容器已限制為 500 TB，滿足大多數的 SAP HANA 系統，在 Azure，tookeep 足夠 SAP HANA 備份 GS5 VM 中執行。 客戶有 hello 選擇&quot;熱&quot;和&quot;冷&quot;blob 儲存體 (請參閱[Azure Blob 儲存體： 熱和冷卻儲存層](../../../storage/blobs/storage-blob-storage-tiers.md))。

Hello blobxfer 工具，很容易 toocopy hello SAP HANA 備份檔案直接 tooAzure blob 儲存體。

![其中一個可以在此處查看完整的 SAP HANA 檔案備份的 hello 檔案](media/sap-hana-backup-file-level/image026.png)

其中一個可以在這裡看到 hello 檔案的完整的 SAP HANA 檔案備份。 有四個檔案而 hello 最大的一個有大約 230 GB。

![花費大約 3000 秒 toocopy hello 230 GB tooan Azure 標準儲存體帳戶 blob 容器](media/sap-hana-backup-file-level/image027.png)

不使用 md5 雜湊 hello 初始的測試中，花費的大約 3000 秒 toocopy hello 230 GB tooan Azure 標準儲存體帳戶 blob 容器。

![在這個螢幕擷取畫面，其中一個可以查看其外觀上 hello Azure 入口網站](media/sap-hana-backup-file-level/image028.png)

在這個螢幕擷取畫面，其中一個可以查看其外觀 hello Azure 入口網站上。 名為的 blob 容器&quot;sap-hana-備份&quot;已建立，而且包含 hello 四個 blob，代表 hello SAP HANA 備份檔案。 其中一個的大小約為 230 GB。

hello HANA Studio 備份主控台可讓一個 toorestrict hello 檔案大小上限的 HANA 備份檔案。 在 hello 範例環境中，它會藉由多個較小的備份檔案，而不是一個大型的 230 GB 檔案可能 toohave 提升效能。

![設定 hello 備份檔案大小限制 hello HANA 端規定 &#39; t 改善 hello 備份時間](media/sap-hana-backup-file-level/image029.png)

設定 hello 備份檔案大小限制 hello HANA 端規定 &#39; t 改善 hello 備份時間，，因為 hello 檔案會寫入循序圖中所示。 hello 檔案大小上限設定 too60 GB，因此 hello 備份單一檔案建立四個大型資料檔案，而不是 hello 230 GB。

![tootest 的平行處理原則的 hello blobxfer 工具 hello 檔案大小上限為 HANA 備份然後將其設定 too15 GB](media/sap-hana-backup-file-level/image030.png)

tootest 的平行處理原則的 hello blobxfer 工具 hello 檔案大小上限為 HANA 備份然後將其設定 too15 GB，導致 19 的備份檔案。 此設定從下 too875 秒的 3000 秒回到 blobxfer toocopy hello 230 GB tooAzure blob 儲存體的 hello 時間。

這個結果會因為 60 MB/秒的寫入 Azure blob toohello 限制。 透過多個 blob 的平行處理原則可以解決 hello 瓶頸，但沒有一個缺點： 增加效能的 hello blobxfer 工具 toocopy 這些 HANA 備份檔案 tooAzure blob 儲存體放負載 hello HANA VM 和 hello 網路上。 HANA 系統的作業會受影響。

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>在備份軟體 RAID 中進行 Azure 專用資料磁碟的 Blob 複製

不同於 hello 手動 VM 資料磁碟備份，在其中一個這種方法不會備份所有 hello 資料磁碟上的 VM toosave hello 整個 SAP 安裝，包括 HANA 資料 HANA 記錄檔和組態檔。 相反地，hello 概念是專用的 toohave 軟體 RAID 具有條狀配置跨多個 Azure 資料 Vhd 來儲存完整的 SAP HANA 檔案備份。 其中一個複製只有這些磁碟，其中有 hello SAP HANA 備份。 它們無法輕鬆地保存在專用的 HANA 備份儲存體帳戶，或附加專用 tooa&quot;備份管理 VM&quot;以便進一步處理。

![涉及的所有 Vhd 已都複製使用 hello * * 開始-azurestorageblobcopy * * PowerShell 命令](media/sap-hana-backup-file-level/image031.png)

涉及的所有 Vhd hello 備份 toohello 本機軟體 RAID 已完成之後，已都複製使用 hello**開始 azurestorageblobcopy** PowerShell 命令 (請參閱[開始 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy))。 它只會影響 hello 專用保持 hello 備份檔案的檔案系統，如有任何疑慮 hello 磁碟上的 SAP HANA 資料或記錄檔一致性。 此命令的優點是它的運作時 hello VM 仍然會保持連線。 toobe 特定的處理序寫入 toohello 備份等量集，可確定 toounmount 前面 hello blob 複製，並將其事後重新裝載。 或其中一個可以使用適當太&quot;凍結&quot;hello 檔案系統。 例如，透過 xfs\_hello XFS 檔案系統凍結。

![這個螢幕擷取畫面顯示 hello hello Azure 入口網站上的 vhd 容器中的 hello 的 blob 清單](media/sap-hana-backup-file-level/image032.png)

這個螢幕擷取畫面顯示 hello 的 blob 清單中 hello &quot;vhd&quot; hello Azure 入口網站上的容器。 hello 螢幕擷取畫面顯示 hello 五個 Vhd，其 toohello SAP HANA 伺服器 VM tooserve 做為附加 hello 軟體 RAID tookeep SAP HANA 備份檔案。 它也會顯示 hello 拍攝透過 hello blob 複製命令中的 5 個複本。

![為了測試用途，hello hello SAP HANA 備份軟體 RAID 磁碟副本是附加的 toohello 應用程式伺服器 VM](media/sap-hana-backup-file-level/image033.png)

為了測試用途，hello hello SAP HANA 備份軟體 RAID 磁碟副本是附加的 toohello 應用程式伺服器 VM。

![hello 應用程式伺服器 VM 關機 tooattach hello 磁碟複製](media/sap-hana-backup-file-level/image034.png)

hello 應用程式伺服器 VM 已關閉 tooattach hello 磁碟複本。 啟動之後 hello VM，hello 磁碟和 hello RAID 發現正確 （透過 UUID 掛接）。 Hello 掛接點遺失時，透過 hello YaST partitioner 建立時所。 之後 hello SAP HANA 備份檔案複製作業系統層級上變為可見。

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>將 SAP HANA tooNFS 共用的備份檔案複製

toolessen hello 對可能影響 hello SAP HANA 系統的效能或磁碟空間的觀點來看，一個可能會考慮 hello SAP HANA 備份檔案儲存在上對 NFS 共用。 技術上運作，但表示為 hello NFS 共用的 hello 主機使用第二個 Azure VM。 它不應該是較小的 VM 大小，因為 toohello VM 網路頻寬。 它會使意義上，然後關閉這 tooshut&quot;備份 VM&quot; ，並且只會讓它註冊執行 hello SAP HANA 備份。 NFS 上撰寫共用負載 hello 網路上和影響 hello SAP HANA 系統，但是只管理 hello 備份檔案，之後在 hello&quot;備份 VM&quot;就不會影響 hello SAP HANA 系統完全。

![從另一個 Azure VM 對 NFS 共用已掛接的 toohello SAP HANA 伺服器 VM](media/sap-hana-backup-file-level/image035.png)

tooverify hello NFS 使用大小寫，從另一個 Azure VM 對 NFS 共用已掛接的 toohello SAP HANA 伺服器 VM。 沒有套用任何特別的 NFS 微調。

![花費 1 小時 46 分鐘 toodo hello 備份直接](media/sap-hana-backup-file-level/image036.png)

hello NFS 共用已快速等量集，例如 hello SAP HANA 伺服器 hello 其中一個。 儘管如此，花費 1 小時到 46 分鐘 toodo hello hello NFS 共用，而不是 10 分鐘，直接在備份時寫入 tooa 本機條狀磁碟組。

![hello 或者未在 1 小時 43 分鐘更快](media/sap-hana-backup-file-level/image037.png)

hello 另一種進行備份 tooa 本機等量集，並且複製 toohello 作業系統層級的 NFS 共用 (簡單**cp avr**命令) 不是更快。 花了 1 小時 43 分鐘。

因此它的運作方式，但是效能不適合用來測試備份的 hello 230 GB。 若遇到數 TB 的資料，可能會更糟。

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>複製 SAP HANA 備份檔案 tooAzure 檔案服務

Azure 的檔案共用內 Azure Linux VM 的可能 toomount 它。 hello 文章[如何 toouse Linux 的 Azure 檔案儲存體](../../../storage/files/storage-how-to-use-files-linux.md)詳細說明如何 toodo 它。 請記住，目前 Azure 檔案共用有 5 TB 配額的限制，以及每個檔案 1 TB 的檔案大小限制。 如需儲存體限制的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](../../../storage/common/storage-scalability-targets.md) (英文)。

不過測試顯示，SAP HANA 備份目前不能直接搭配使用這種 CIFS 掛接。 在 [SAP Note 1820529](https://launchpad.support.sap.com/#/notes/1820529) (英文) 中也提到不建議使用 CIFS。

![此圖中 SAP HANA Studio 中的 hello 備份對話方塊會顯示錯誤](media/sap-hana-backup-file-level/image038.png)

此圖會顯示錯誤 hello 備份對話方塊，在 SAP HANA Studio 中，在嘗試 tooback 向上直接 tooa CIFS 裝載 Azure 的檔案共用時。 讓一個具有 toodo VM 檔案系統的標準 SAP HANA 備份第一次，，然後複製 hello 備份檔案從該處 tooAzure 檔案服務。

![此圖將顯示花費有關 929 秒 toocopy 19 SAP HANA 備份檔案](media/sap-hana-backup-file-level/image039.png)

此圖顯示所花費有關 929 秒 toocopy 19 SAP HANA 備份檔案的約略 230 GB toohello Azure 檔案共用的大小總計。

![hello SAP HANA VM 上的 hello 來源目錄結構已複製的 toohello Azure 檔案共用](media/sap-hana-backup-file-level/image040.png)

在這個螢幕擷取畫面，其中一個可以看到 hello SAP HANA VM 上的 hello 來源目錄結構已複製的 toohello Azure 檔案共用： 一個目錄 (hana\_備份\_fsl\_15 gb) 及 19 的個別備份檔案。

SAP HANA 檔案備份直接支援時，儲存在 Azure 檔案上的 SAP HANA 備份檔案可能是有趣的選項，在未來的 hello。 或時就有可能透過 NFS 的 toomount Azure 檔案，而且 hello 最大配額限制是相當高於 5 TB。

## <a name="next-steps"></a>後續步驟
* [Azure 虛擬機器上 SAP HANA 的備份指南](sap-hana-backup-guide.md)提供快速入門的概觀和詳細資訊。
* [SAP HANA 備份為基礎儲存快照集](sap-hana-backup-storage-snapshots.md)hello 儲存快照集式備份選項的描述。
* toolearn tooestablish 高可用性和 Azure （大型執行個體） 上的 SAP HANA 災害復原計劃的看到[SAP HANA （大型執行個體） 高可用性和災害復原在 Azure 上的](hana-overview-high-availability-disaster-recovery.md)。
