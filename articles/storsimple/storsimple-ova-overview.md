---
title: "aaaMicrosoft Azure StorSimple Virtual Array 概觀 |Microsoft 文件"
description: "描述 hello StorSimple Virtual Array，整合式儲存體解決方案，可管理內部部署虛擬陣列和 Microsoft Azure 雲端儲存體之間的儲存工作。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>簡介 toohello StorSimple Virtual Array
## <a name="overview"></a>概觀
Microsoft Azure StorSimple Virtual Array hello 是整合式儲存體解決方案，可管理內部部署虛擬陣列執行於 hypervisor，Microsoft Azure 雲端儲存體之間的儲存工作。 hello 虛擬陣列是有效率、 符合成本效益且容易管理的檔案伺服器或 iSCSI 伺服器解決方案，可避免許多問題 hello 和企業儲存體和資料保護與相關聯的費用。 hello 虛擬陣列是特別適合用於遠端辦公室/分公司案例。

本主題概略說明 hello 虛擬陣列-這裡有一些其他資源：

* 如需最佳做法，請參閱 [StorSimple Virtual Array 的最佳做法](storsimple-ova-best-practices.md)。
* 如需 hello StorSimple 8000 系列裝置的概觀，請移至太[StorSimple 8000 系列： 混合式雲端解決方案](storsimple-overview.md)。 
* Hello StorSimple 5000 7000 系列裝置的相關資訊，請太[StorSimple 線上說明](http://onlinehelp.storsimple.com/)。

hello 虛擬陣列支援 hello iSCSI 或伺服器訊息區塊 (SMB) 通訊協定。 它會在現有的 hypervisor 基礎結構上執行並提供分層 toohello 雲端、 雲端備份，快速還原、 項目層級復原和災害復原功能。

hello 下表摘要說明 hello StorSimple Virtual Array hello 重要的功能。

| 功能 | StorSimple Virtual Array |
| --- | --- |
| 安裝需求 |使用虛擬化基礎結構 (Hyper-V 或 VMware) |
| Availability |單一節點 |
| 總容量 (包括雲端) |設定每個虛擬陣列 too64 TB 可用容量 |
| 本機容量 |每個虛擬陣列 (需要 tooprovision 500 GB too8 TB 的磁碟空間) 390 GB too6.4 TB 可用容量 |
| 原生通訊協定 |iSCSI 或 SMB |
| 復原時間目標 (RTO) |iSCSI：少於 2 分鐘 (不論大小為何) |
| 復原點目標 (RPO) |每日備份和隨選備份 |
| 儲存體分層 |使用熱對應 toodetermine 哪些資料應該分層 in 或 out |
| 支援 |Hello 供應商所支援的虛擬化基礎結構 |
| 效能 |會視基礎結構而異 |
| 資料行動性 |可以還原 toohello 同一部裝置或執行項目層級復原 （檔案伺服器） |
| 儲存層 |本機 Hypervisor 儲存體和雲端 |
| 共用大小 |階層式： 向上 too20 TB;固定在本機： 向上 too2 TB |
| 磁碟區大小 |階層式： 500GB too5 TB;固定在本機： 50 GB too500 GB |
| 磁碟區大小 |階層式： 向上 too5 TB;固定在本機： 向上 too500 GB |
| 快照集 |當機時保持一致 |
| 項目層級復原 |是；使用者可以從共用還原 |

## <a name="why-use-storsimple"></a>為何要使用 StorSimple？
StorSimple 連接使用者與伺服器 tooAzure 儲存體，以分鐘為單位，與未修改的應用程式。

hello 下表描述的一些 hello 主要優點 StorSimple Virtual Array 解決方案提供該 hello。

| 功能 | 優點 |
| --- | --- |
| 透明整合 |hello 虛擬陣列支援 hello iSCSI 或 hello SMB 通訊協定。 hello hello 本機層與 hello 雲端層之間的資料移動是順暢且透明 toohello 使用者。 |
| 降低儲存成本 |StorSimple、 您佈建足夠本機儲存體 toomeet 目前的需求最常使用的 hello 熱資料。 隨著儲存體需求的成長，StorSimple 會將冷資料分層至符合成本效益的雲端儲存體。 hello 資料重複資料刪除，且壓縮傳送 toohello 雲端之前，先 toofurther 減少儲存需求和支出。 |
| 簡化儲存管理 |StorSimple 提供使用 StorSimple 裝置管理員 toomanage hello 雲端中的集中的管理多個裝置。 |
| 改進災害復原和提高合規性 |StorSimple 協助立即還原 hello 中繼資料，並視需要還原 hello 資料更快速的災害復原。 這表示正常作業可以在最少干擾的情況下繼續執行。 |
| 資料行動性 |階層式的 toohello 雲端可從其他站台進行復原和移轉的資料。 請注意，您可以還原資料只有 toohello 原始虛擬陣列。 不過，您可以使用災害復原功能 toorestore hello 整個虛擬陣列 tooanother 虛擬陣列。 |

## <a name="storsimple-workload-summary"></a>StorSimple 工作負載摘要

下表顯示所支援 StorSimple 工作負載的摘要。

|案例     |工作負載     |支援      |限制               |
|-------------|-------------|---------------|---------------------------|
|ROBO 共同作業 |檔案共用     |是      |請參閱[檔案伺服器的上限](storsimple-ova-limits.md)。<br></br>請參閱[支援 SMB 版的系統需求](storsimple-ova-system-requirements.md)。| 所有版本     |

## <a name="workflows"></a>工作流程
hello StorSimple Virtual Array 是特別適用於下列工作流程的 hello:

* [雲端儲存體管理](#cloud-based-storage-management)
* [與位置無關的備份](#location-independent-backup)
* [資料保護和災害復原](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>雲端儲存體管理
您可以使用 hello 和多個位置中 hello Azure 入口網站 toomanage 資料儲存在多個裝置上執行的 StorSimple 裝置管理員服務。 這在分散式分公司案例中特別有用。 請注意，您必須建立 hello StorSimple 裝置管理員服務 toomanage 虛擬陣列和實體 StorSimple 裝置的不同執行個體。 也請注意該 hello 虛擬陣列現在使用 hello 新版 Azure 入口網站，而不是 hello Azure 傳統入口網站。

![雲端儲存體管理](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>與位置無關的備份
Hello 虛擬陣列，雲端快照集提供的位置無關的時間點複本磁碟區或共用。 預設會啟用雲端快照集，並且無法停用。 所有磁碟區與共用會備份在 hello 相同時間透過單一的每日備份原則，而且您可以隨時依需要額外的臨機操作備份。

### <a name="data-protection-and-disaster-recovery"></a>資料保護和災害復原
hello 虛擬陣列支援下列資料保護和災害復原案例的 hello:

* **磁碟區或共用的還原**– hello 還原做為新的工作流程 toorecover 磁碟區或共用。 使用此方法 toorecover hello 整個磁碟區或共用。
* **項目層級復原**– 共用允許簡化的存取 toorecent 備份。 您可以輕鬆地復原個別檔案特殊*.backup* hello 雲端中可用的資料夾。 這個還原功能是由使用者所驅動，而且不需要系統管理介入。
* **嚴重損壞修復**– 使用 hello 容錯移轉功能 toorecover 所有磁碟區或共用 tooa 新虛擬陣列。 建立 hello 新的虛擬陣列，並向 hello StorSimple 裝置管理員服務，然後容錯移轉 hello 原始虛擬陣列。 hello 新的虛擬陣列則會假設為 hello 佈建資源。 

## <a name="storsimple-virtual-array-components"></a>StorSimple Virtual Array 元件
hello 虛擬陣列包含下列元件的 hello:

* [虛擬陣列](#virtual-array) – 一種以虛擬化環境或 Hypervisor 中所佈建之虛擬機器為基礎的混合式雲端存放裝置。  
* [StorSimple 裝置管理員服務](#storsimple-device-manager-service)-的 hello 可讓您從單一 web 介面，您可以從不同地理位置存取管理一或多個 StorSimple 裝置的 Azure 入口網站的延伸模組。 您可以使用 hello StorSimple 裝置管理員服務 toocreate 和管理服務、 檢視和管理裝置和警示，以及管理磁碟區、 共用與現有的快照集。
* [本機 web 使用者介面](#local-web-user-interface)– 網頁的 UI 使用的 tooconfigure hello 裝置，使其可以連接 toohello 區域網路，然後將 hello 裝置註冊 hello StorSimple 裝置管理員服務。 
* [命令列介面](#command-line-interface)– 可讓您的支援工作階段的 toostart hello 虛擬陣列上的 Windows PowerShell 介面。
  hello 下列各節描述每個元件會更詳細地並解釋 hello 方案如何排列資料、 配置儲存體，並可協助管理儲存體及資料保護。

### <a name="virtual-array"></a>虛擬陣列
hello 虛擬陣列是提供主要儲存體，管理雲端存放裝置的通訊並協助 tooensure hello 安全性與機密性的所有資料儲存在 hello 裝置上的單一節點存放裝置解決方案。

hello 虛擬陣列有一個可供下載的模型。 hello 虛擬陣列都有的最大容量 6.4 TB 的 hello 裝置 （8 TB 的基礎儲存體需求），包括 64 TB 雲端存放裝置。 

hello 虛擬陣列有 hello 下列功能：

* 符合成本效益。 使用現有的虛擬化基礎結構，而且可以部署於現有 Hyper-V 或 VMware Hypervisor 上。
* 它位於 hello 資料中心，並可設定 iSCSI 伺服器或檔案伺服器。 
* 它會與 hello 雲端整合。
* 備份會儲存在 hello 雲端中，這可以加速災害復原，並簡化項目層級復原 (ILR)。 
* 您可以套用更新 toohello 虛擬陣列，就如同您可以將它們套用 tooa 實體裝置。

> [!NOTE]
> 無法展開虛擬陣列。 因此，當您建立 hello 虛擬陣列是重要的 tooprovision 適當存放裝置。 
> 
> 

### <a name="storsimple-device-manager-service"></a>StorSimple 裝置管理員服務
Microsoft Azure StorSimple 提供網頁型使用者介面，hello 可讓您 toocentrally StorSimple 裝置管理員服務管理 StorSimple 儲存體。 您可以使用下列工作的 hello StorSimple 裝置管理員服務 tooperform hello:

* 透過單一服務管理多個 StorSimple Virtual Array。 
* 進行和管理 StorSimple Virtual Array 的安全性設定。 （hello 雲端中的加密會相依於 Microsoft Azure 應用程式開發介面）。
* 設定儲存體帳戶認證和屬性。
* 設定和管理磁碟區或共用。
* 備份和還原磁碟區或共用上的資料。
* 監視效能。
* 檢閱系統設定，並識別可能發生的問題。

您使用 hello StorSimple 裝置管理員服務 tooperform 每日管理的虛擬陣列。

如需詳細資訊，請移至太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-virtual-array-manager-service-administration.md)。

### <a name="local-web-user-interface"></a>本機 Web 使用者介面
hello 虛擬陣列包含網頁使用者介面，用於一次性的組態與 hello 裝置 hello StorSimple 裝置 Manager 服務註冊。 您可以使用它 tooshut 關閉和重新啟動 hello 虛擬陣列、 執行診斷測試、 軟體更新、 變更 hello 裝置系統管理員密碼、 檢視系統記錄檔，並連絡 Microsoft 支援服務 toofile 服務要求。 

如需使用 hello 網頁使用者介面，請移過[使用 hello 網頁 UI tooadminister 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。

### <a name="command-line-interface"></a>命令列介面
hello 包含 Windows PowerShell 介面可讓您向 Microsoft 支援的支援工作階段的 tooinitiate，讓它們可以協助您疑難排解並解決您的虛擬陣列，可能會遇到的問題。

## <a name="storage-management-technologies"></a>儲存體管理技術
此外 toohello 虛擬陣列和其他元件，hello 的 StorSimple 解決方案會使用 hello 下列軟體技術 tooprovide 快速存取 tooimportant 資料、 降低存放裝置耗用量，以及保護資料儲存在您的虛擬陣列：

* [自動儲存體分層](#automatic-storage-tiering) 
* [固定在本機的共用和磁碟區](#locally-pinned-shares-and-volumes)
* [重複資料刪除和壓縮資料層或 toohello 雲端備份](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [排程和隨選備份](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>自動儲存體分層
hello 虛擬陣列 hello 虛擬陣列和 hello 雲端間使用新的分層機制 toomanage 儲存資料。 有兩個層： hello 的本機虛擬陣列和 Azure 雲端儲存體。 hello StorSimple Virtual Array 自動將資料排列成 hello 熱門地圖，它會追蹤目前的使用方式、 年齡和關聯性 tooother 資料為基礎的層級。 大部分使用中 （最熱） 會儲存在本機，而較不作用中和非使用中的資料，則會自動的資料移轉 toohello 雲端。 （所有的備份會儲存在 hello 雲端）。StorSimple 會隨著使用模式變更而調整並重新排列資料和儲存體指派。 例如，某些資訊在經過一段時間之後可能會變成不常使用。 當它變得愈來愈少時，它被分層出 toohello 雲端。 如果相同資料再次變成作用中，它被分層 toohello 存放裝置陣列中。

特定階層共用或磁碟區的資料保證它自己的本機層空間。 （大約 10%的 hello 總佈建的空間的共用或磁碟區）。 雖然這會減少可用的存放裝置 hello hello 虛擬陣列，該共用或磁碟區上，它可確保，分層一個共用或磁碟區將不會影響其他共用或磁碟區的 hello 階層處理需求。 因此在上一個共用或磁碟區非常忙碌的工作負載無法強制所有其他工作負載 toohello 雲端。 

![自動儲存體分層](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> 您可以指定為本機固定磁碟區，在此情況下 hello 資料會保留在 hello 虛擬陣列，且永遠不會分層 toohello 雲端。 如需詳細資訊，請移至太[固定在本機的共用與磁碟區](#locally-pinned-shares-and-volumes)。
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>固定在本機的共用和磁碟區
您可以建立適當的固定在本機共用和磁碟區。 這項功能可確保重要應用程式所需的資料會保留在 hello 虛擬陣列，而且永遠不會分層 toohello 雲端。 固定在本機的共用與磁碟區有 hello 下列功能： 

* 它們並非主體 toocloud 延遲或連線問題。
* 依然受益於 StorSimple 雲端備份和災害復原功能。

您可以將固定在本機的共用或磁碟區還原為階層式，或將階層式共用或磁碟區還原為固定在本機。 

如需有關本機固定磁碟區的詳細資訊，請移太[使用 hello StorSimple 裝置管理員服務 toomanage 磁碟區](storsimple-virtual-array-manage-volumes.md)。

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>重複資料刪除和壓縮資料層或 toohello 雲端備份
StorSimple 使用重複資料刪除和資料壓縮 toofurther 降低 hello 雲端中的儲存需求。 重複資料刪除可減少 hello 整體儲存藉由消除備援 hello 儲存資料集中的資料量。 當資訊變更時，StorSimple 會忽略 hello 保持不變的資料，並擷取只 hello 變更。 此外，StorSimple 可減少 hello 儲存的資料量，識別並移除重複的資訊。 

> [!NOTE]
> 資料儲存在 hello 虛擬陣列不是重複資料刪除或壓縮。 所有重複資料刪除和 hello 資料會傳送 toohello 雲端之前，會進行壓縮。
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>排程和隨選備份
StorSimple 資料保護功能可讓您 toocreate 視備份。 此外，預設備份排程可確保每日備份資料。 備份會執行增量快照儲存在 hello 雲端中的 hello 形式。 快照集，只 hello 變更記錄 hello 上次備份之後，可以建立並快速還原。 這些快照集可能在災害復原案例中非常重要，因為它們取代次要儲存體系統 （例如磁帶備份），並可讓您 toorestore 資料 tooyour 資料中心或 tooalternate 站台有必要。

## <a name="next-steps"></a>後續步驟
了解如何太[準備 hello 虛擬陣列入口網站](storsimple-virtual-array-deploy1-portal-prep.md)。

