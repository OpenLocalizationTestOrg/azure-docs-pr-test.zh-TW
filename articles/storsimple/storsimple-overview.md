---
title: "aaaStorSimple 8000 系列解決方案概觀 |Microsoft 文件"
description: "描述 StorSimple 分層、 hello 裝置、 虛擬裝置、 服務和儲存體管理，並介紹用 StorSimple 中的重要詞彙。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>StorSimple 8000 系列：混合式雲端存放解決方案
## <a name="overview"></a>概觀
歡迎使用 tooMicrosoft Azure StorSimple、 整合式儲存體解決方案，可管理儲存在內部部署裝置與 Microsoft Azure 雲端儲存體之間的工作。 StorSimple 是有效率、 符合成本效益且可輕鬆地管理儲存體區域網路 (SAN) 解決方案，可消除許多 hello 問題和企業儲存體和資料保護與相關聯的費用。 它會使用專屬 StorSimple 8000 系列裝置 hello、 與雲端服務整合，並提供管理工具的一組所有企業存放裝置，包括雲端儲存體的整體檢視。 （hello hello Microsoft Azure 網站上發行的 StorSimple 部署資訊適用於 tooStorSimple 8000 系列的裝置。 如果您使用 StorSimple 5000 7000 系列裝置，請移至太[StorSimple 說明](http://onlinehelp.storsimple.com/)。)

StorSimple 使用[存放裝置階層處理](#automatic-storage-tiering)toomanage 跨不同的儲存媒體中儲存資料。 hello 目前的工作集是儲存在內部固態磁碟機 (Ssd)、 較不常使用的資料會儲存在硬碟機 (Hdd) 和封存資料推入 toohello 雲端。 此外，StorSimple 使用重複資料刪除，而且會耗用壓縮 tooreduce hello hello 資料的儲存體數量。 如需詳細資訊，請移至太[重複資料刪除和壓縮](#deduplication-and-compression)。 如需其他的主要詞彙和概念 hello StorSimple 8000 系列文件中所用的定義，請移過[StorSimple 詞彙](#storsimple-terminology)hello 本文結尾處。

此外 toostorage 管理 StorSimple 資料保護功能允許您 toocreate 隨和排定的備份及它們在本機或 hello 雲端加以儲存。 備份在 hello 增量快照形式，這表示可以是建立並快速還原。 雲端快照可能在災害復原案例中非常重要，因為它們取代次要儲存體系統 （例如磁帶備份），並可讓您 toorestore 資料 tooyour 資料中心或 tooalternate 站台有必要。

![影片圖示](./media/storsimple-overview/video_icon.png) 監看式 hello 視訊的快速簡介 tooMicrosoft Azure StorSimple。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>為何要使用 StorSimple？
hello 下表描述的一些 hello Microsoft Azure StorSimple 提供的主要優點。

| 功能 | 優點 |
| --- | --- |
| 透明整合 |使用 hello iSCSI 通訊協定 tooinvisibly 連結資料儲存設備。 這可以確保在 hello datacenter 的 hello 雲端中存放的資料，或在遠端伺服器上會出現 toobe 儲存在單一位置。 |
| 降低儲存成本 |配置足夠的本機或雲端儲存體 toomeet 目前的需求，且擴充雲端儲存體只在必要時。 它進一步減少儲存需求和支出藉由消除 hello 的多餘版本相同的資料 （重複資料刪除） 並使用壓縮。 |
| 簡化儲存管理 |提供系統管理工具 tooconfigure 及管理儲存的資料在內部，在遠端伺服器上，並在 hello 雲端中。 此外，您可以從 Microsoft Management Console (MMC) 嵌入式管理單元來管理備份和還原功能。|
| 改進災害復原和提高合規性 |不需要延長復原時間。 相反地，它會在需要時還原資料。 這表示正常作業可以在最少干擾的情況下繼續執行。 此外，您可以設定原則 toospecify 備份排程和資料保留。 |
| 資料行動性 |資料上傳 tooMicrosoft Azure 雲端服務可以從其他站台復原和移轉目的而進行存取。 此外，您可以在 Microsoft Azure 中執行的虛擬機器 (Vm) 上使用 StorSimple tooconfigure StorSimple 雲端應用程式。 hello Vm 然後可以基於測試或復原使用虛擬裝置 tooaccess 儲存資料。 |
| 業務持續性 |可讓 StorSimple 5000 7000 系列使用者 toomigrate 其資料 tooa StorSimple 8000 系列裝置。 |
| Hello Azure 政府入口網站中的可用性 |StorSimple 可在 hello Azure 政府入口網站。 如需詳細資訊，請參閱[部署在內部部署 StorSimple 裝置 hello 政府入口網站中的](storsimple-8000-deployment-walkthrough-gov-u2.md)。 |
| 資料保護與可用性 |hello StorSimple 8000 系列支援區域備援儲存體 (ZRS)，在加法 tooLocally 備援儲存體 (LRS) 和地理備援儲存體 (GRS)。 參照太[Azure 儲存體備援選項這篇文章](https://azure.microsoft.com/documentation/articles/storage-redundancy/)如 ZRS 詳細資料。 |
| 重要應用程式的支援 |StorSimple 可讓您找出適當的磁碟區為固定在本機後者又可確保重要應用程式所需的資料不是階層式的 toohello 雲端。 本機固定磁碟區沒有主旨 toocloud 延遲或連線問題。 如需本機固定磁碟區的詳細資訊，請參閱[使用 hello StorSimple 裝置管理員服務 toomanage 磁碟區](storsimple-8000-manage-volumes-u2.md)。 |
| 低延遲和高效能 |您可以建立利用 hello 高效能、 低延遲功能的 Azure 高階儲存體的雲端應用裝置。 如需 StorSimple 進階雲端設備的詳細資訊，請參閱[部署和管理 Azure 中的 StorSimple 雲端設備](storsimple-8000-cloud-appliance-u2.md)。 |


## <a name="storsimple-components"></a>StorSimple 元件
hello Microsoft Azure StorSimple 解決方案包含下列元件的 hello:

* **Microsoft Azure StorSimple 裝置** - 包含 SSD 和 HDD 的內部部署混合式存放裝置陣列，提供備援控制器和自動容錯移轉功能。 hello 控制器管理儲存體分層，將目前使用 （或活躍） 資料存放在本機儲存體 （在 hello 裝置或內部部署伺服器），移動較不常用的資料 toohello 雲端時。
* **StorSimple 雲端應用裝置**– 也稱為 hello StorSimple 虛擬應用裝置，這是複寫 hello 架構的 hello StorSimple 裝置的軟體版本和的 hello 實體混合式儲存裝置的大部分功能。 Azure 的虛擬機器中的單一節點上，執行 hello StorSimple 雲端應用裝置。 可利用 Azure 進階儲存體帳戶的高階虛擬裝置可在 Update 2 及更新版本中使用。
* **StorSimple 裝置管理員服務**-的 hello 可讓您從單一 web 介面管理 StorSimple 裝置或 StorSimple 雲端應用裝置的 Azure 入口網站的延伸模組。 您可以使用 hello StorSimple 裝置管理員服務 toocreate 和管理服務、 檢視和管理裝置、 檢視警示、 管理磁碟區，以及檢視和管理備份原則與 hello 備份類別目錄。
* **Windows PowerShell for StorSimple** – 命令列介面，您可以使用 toomanage hello StorSimple 裝置。 Windows PowerShell for StorSimple 的功能可讓您 tooregister StorSimple 裝置、 在裝置上設定 hello 網路介面、 安裝特定類型的更新、 裝置藉由存取 hello 支援工作階段，進行疑難排解和變更 hello裝置狀態。 連接 toohello 序列主控台或使用 Windows PowerShell 遠端功能，您可以存取 Windows PowerShell for StorSimple。
* **Azure PowerShell StorSimple cmdlet** – Windows PowerShell cmdlet 可讓您從 hello 命令列的 tooautomate 服務層級和移轉工作的集合。 如 for StorSimple hello Azure PowerShell cmdlet 的相關資訊，請移至 toohello [cmdlet 參考](/powershell/module/azure/?view=azuresmps-3.7.0#azure)。
* **StorSimple Snapshot Manager** – MMC 嵌入式管理單元，使用磁碟區群組與 hello Windows 磁碟區陰影複製服務 toogenerate 應用程式一致備份。 此外，您可以使用 StorSimple Snapshot Manager toocreate 備份排程及複製或還原磁碟區。
* **StorSimple Adapter for SharePoint** -一種工具，以透明的方式擴充 tooSharePoint 伺服器陣列，Microsoft Azure StorSimple 儲存體和資料保護在檢視和管理從 hello SharePoint 管理中心，讓 StorSimple 儲存體系統管理入口網站。

hello 圖提供 hello Microsoft Azure StorSimple 架構的高階檢視和元件。

![StorSimple 架構](./media/storsimple-overview/overview-big-picture.png)

hello 下列各節描述每個元件會更詳細地並解釋 hello 方案如何排列資料、 配置儲存體，並可協助管理儲存體及資料保護。 hello 最後一節提供一些 hello 重要詞彙和概念相關的 tooStorSimple 元件，以及其管理的定義。

## <a name="storsimple-device"></a>StorSimple 裝置
hello Microsoft Azure StorSimple 裝置是在內部部署混合式儲存體陣列提供主要儲存體與儲存在其上的 iSCSI 存取 toodata。 它會管理雲端存放裝置的通訊，以及協助 tooensure hello 安全性和儲存在 Microsoft Azure StorSimple 方案 hello 上所有資料的機密性。

hello StorSimple 裝置包括 Ssd 和硬碟機 Hdd，以及支援叢集和自動容錯移轉。 它包含共用處理器、共用儲存體，以及兩個鏡像控制站。 每個控制站提供 hello 下列：

* 連接 tooa 主機電腦
* 向上 toosix 網路連接埠 tooconnect toohello 區域網路 (LAN)
* 硬體監控
* 即使電源中斷仍會保留資訊的靜態隨機存取記憶體 (NVRAM)
* 叢集感知更新 toomanage 容錯移轉叢集中的伺服器上的軟體更新，使 hello 更新具有最小或不會影響服務可用性
* 叢集服務 (如後端叢集般運作) 可提供高可用性，並將 HDD 或 SSD 故障或離線時可能會發生的任何負面影響降到最低

不論在任何時間點，只會有一個作用中的控制器。 Hello 主動控制器失效，如果 hello 第二個控制站會自動啟動。

如需詳細資訊，請移至太[StorSimple 硬體元件與狀態](storsimple-8000-monitor-hardware-status.md)。

## <a name="storsimple-cloud-appliance"></a>StorSimple 雲端設備
您可以使用 StorSimple toocreate 複寫 hello 架構和功能的 hello 實體混合式儲存裝置的雲端應用裝置。 Azure 的虛擬機器中的單一節點上，執行 hello StorSimple 雲端應用裝置 (也稱為 hello StorSimple 虛擬應用裝置)。 (雲端設備只能建立在 Azure 虛擬機器上。 您無法在 StorSimple 裝置或在內部部署伺服器上建立虛擬裝置)。

hello 雲端應用裝置具有下列功能的 hello:

* 它模仿實體裝置，並可提供 iSCSI 介面 toovirtual 機器 hello 雲端中。
* 您可以建立 hello 雲端中的無限的數量的雲端應用裝置，並在必要時將其開啟和關閉。
* 可協助您模擬災害復原、開發和測試案例中的內部部署環境，並可協助從備份進行項目層級的擷取。

hello StorSimple 雲端應用裝置有兩個模型： hello 8010 裝置 （之前稱為 hello 1100 模型） 和 hello 8020 裝置。 hello 8010 裝置都有最大容量為 30 TB。 hello 8020 裝置，利用 Azure 高階儲存體，有 64 TB 的最大容量。 (在本機層中，Azure 進階儲存體會將資料儲存在 SSD 上，而標準儲存體會將資料儲存在 HDD 上。)請注意，您必須擁有 Azure 高階儲存體帳戶 toouse premium 儲存體。 如需 premium 儲存體的詳細資訊，請移至太[高階儲存體： Azure 虛擬機器工作負載的高效能儲存體](../storage/common/storage-premium-storage.md)。

如需 hello StorSimple 雲端應用裝置的詳細資訊，請移至太[部署及管理在 Azure StorSimple 雲端應用裝置](storsimple-8000-cloud-appliance-u2.md)。

## <a name="storsimple-device-manager-service"></a>StorSimple 裝置管理員服務
Microsoft Azure StorSimple 提供的 web 架構使用者介面 (hello StorSimple 裝置管理員服務)，可讓您 toocentrally 管理資料中心和雲端存放裝置。 您可以使用下列工作的 hello StorSimple 裝置管理員服務 tooperform hello:

* 進行 StorSimple 裝置的系統設定。
* 進行和管理 StorSimple 裝置的安全性設定。
* 設定雲端認證和屬性。
* 設定和管理伺服器上的磁碟區。
* 設定磁碟區群組。
* 備份和還原資料。
* 監視效能。
* 檢閱系統設定，並識別可能發生的問題。

您可以使用 hello StorSimple 裝置管理員服務 tooperform 需要系統停機時，例如初始安裝和安裝的更新除外的所有管理工作。

如需詳細資訊，請移至太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

## <a name="windows-powershell-for-storsimple"></a>Windows PowerShell for StorSimple
Windows PowerShell for StorSimple 提供的命令列介面，您可以使用 toocreate 和管理 hello Microsoft Azure StorSimple 服務和設定和監視 StorSimple 裝置。 它會是 Windows PowerShell 型的命令列介面，其中包含可管理 StorSimple 裝置的專用 Cmdlet。 Windows PowerShell for StorSimple 的功能可讓您：

* 註冊裝置。
* 在裝置上設定 hello 網路介面。
* 安裝特定類型的更新。
* 疑難排解您的裝置存取 hello 支援工作階段。
* Hello 裝置狀態變更。

您可以存取 Windows PowerShell for StorSimple 序列主控台 （在主機上的電腦直接連線 toohello 裝置） 或從遠端使用 Windows PowerShell 遠端功能。 請注意，只能 hello 序列主控台上完成一些適用於 StorSimple 工作，例如初始裝置註冊的 Windows PowerShell。

如需詳細資訊，請移至太[使用 Windows PowerShell for StorSimple tooadminister 裝置](storsimple-8000-windows-powershell-administration.md)。

## <a name="azure-powershell-storsimple-cmdlets"></a>Azure PowerShell StorSimple Cmdlet
hello Azure PowerShell StorSimple cmdlet 是 Windows PowerShell cmdlet 可讓您 tooautomate 服務層級和 hello 命令列移轉工作的集合。 如 for StorSimple hello Azure PowerShell cmdlet 的相關資訊，請移至 toohello [cmdlet 參考](/powershell/module/azure/?view=azuresmps-3.7.0)。

## <a name="storsimple-snapshot-manager"></a>StorSimple Snapshot Manager
StorSimple Snapshot Manager 是 Microsoft Management Console (MMC) 嵌入式管理單元，您可以使用 toocreate 一致，時間點備份複本的本機和雲端資料。 hello 嵌入式管理單元執行 Windows Server 型主機上。 您可以使用 StorSimple Snapshot Manager 進行下列作業：

* 設定、備份及刪除磁碟區。
* 設定磁碟區群組 tooensure 該備份資料是應用程式一致。
* 管理備份原則，讓資料是在預先決定的排程備份並儲存在指定的位置 （本機或 hello 雲端中）。
* 還原磁碟區和個別檔案。

備份會擷取快照集，以記錄 hello 所做的變更，因為 hello 最後一個快照時，需要儲存空間遠少於完整備份。 您可以建立備份排程或視需要進行立即備份。 此外，您可以使用 StorSimple Snapshot Manager tooestablish 保留原則可控制將儲存快照集數目。 如果您之後需要 toorestore 資料從備份、 的 StorSimple Snapshot Manager 可讓您選取從 hello 類別目錄的本機或雲端快照。 

如果發生損毀，或如果您需要 toorestore 資料，因為其他原因，StorSimple Snapshot Manager 將它還原以累加方式在需要時。 還原資料，不需要還原的檔案、 更換設備或移動作業 tooanother 站台時關閉 hello 整個系統。

如需詳細資訊，請移至太[什麼是 StorSimple Snapshot Manager？](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>StorSimple Adapter for SharePoint
Microsoft Azure StorSimple 包括 hello StorSimple Adapter for SharePoint，會明確地將 StorSimple 儲存體和資料保護擴充功能 tooSharePoint 伺服器陣列的選用元件。 hello 配接器搭配遠端 Blob 儲存 (RBS) 提供者和 hello SQL Server RBS 功能，可讓您 toomove Blob tooa 備份伺服器 hello Microsoft Azure StorSimple 系統。 Microsoft Azure StorSimple 然後 hello BLOB 資料儲存在本機或 hello 雲端使用量為基礎。

hello StorSimple Adapter for SharePoint 是與 hello SharePoint 管理中心入口網站中管理。 因此，SharePoint 管理仍然是集中進行，而所有儲存都體形 toobe hello SharePoint 伺服陣列中。

如需詳細資訊，請移至太[StorSimple Adapter for SharePoint](storsimple-adapter-for-sharepoint.md)。 

## <a name="storage-management-technologies"></a>儲存體管理技術
此外，toohello 專用 StorSimple 裝置、 虛擬裝置，以及其他元件，Microsoft Azure StorSimple 使用下列軟體技術 tooprovide 快速存取 toodata 和 tooreduce 存放裝置耗用量的 hello:

* [自動儲存體分層](#automatic-storage-tiering) 
* [精簡佈建](#thin-provisioning) 
* [重複資料刪除和壓縮](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>自動儲存體分層
Microsoft Azure StorSimple 自動排列依據目前使用量、 年齡和關聯性 tooother 資料的邏輯層中的資料。 為大多數作用中儲存在本機，小於作用中時，以及非使用中的資料自動的資料移轉 toohello 雲端。 hello 下列圖表說明此儲存方法。

![StorSimple 儲存層](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

tooenable 快速存取，StorSimple 儲存經常使用的資料 （熱資料） 在 Ssd 上 hello StorSimple 裝置中。 它會儲存偶爾使用的資料 （暖資料） 在 hello 裝置或在 hello 資料中心的伺服器上的 Hdd 上。 它移動非作用中的資料，備份的資料，以及資料保留封存或相容性目的 toohello 雲端。 

> [!NOTE]
> 在 Update 2 或更新版本，您可以指定為本機固定磁碟區，在此情況下 hello 資料會保留在 hello 本機裝置，而且也無法分層 toohello 雲端。 


StorSimple 會隨著使用模式變更而調整並重新排列資料和儲存體指派。 例如，某些資訊在經過一段時間之後可能會變成不常使用。 當它變得愈來愈少時，它從 Ssd tooHDDs 然後 toohello 雲端移轉。 如果相同資料再次變成作用中，則移轉後 toohello 存放裝置。

hello 存放裝置階層處理程序，如下所示：

1. 系統管理員設定 Microsoft Azure 雲端儲存體帳戶。
2. hello 管理員會使用 hello 序列主控台及 hello StorSimple 裝置管理員服務 （在執行 hello Azure 入口網站） tooconfigure hello 裝置和檔案伺服器，建立磁碟區和資料保護原則。 在內部部署機器 （例如檔案伺服器） 使用 hello Internet Small Computer System Interface (iSCSI) tooaccess hello StorSimple 裝置。
3. 一開始，StorSimple 儲存資料的 hello 裝置 hello 快速 SSD 層上。
4. 為 hello SSD 層方法容量，StorSimple deduplicates 和壓縮 hello 最舊的資料區塊，並將它們移 toohello HDD 層。
5. Hello HDD 層方法容量，以 StorSimple 加密 hello 最舊的資料區塊，並將它們傳送安全地透過 HTTPS toohello Microsoft Azure 儲存體帳戶。
6. Microsoft Azure 建立 hello 資料的多個複本在其資料中心和遠端資料中心，確保災害發生時，可以復原 hello 資料。
7. 當 hello 檔案伺服器要求 hello 雲端中儲存資料時，StorSimple 順暢地將它傳回並將複本儲存在 hello SSD 層的 hello StorSimple 裝置上。

#### <a name="how-storsimple-manages-cloud-data"></a>StorSimple 管理雲端資料的方式

StorSimple deduplicates 客戶資料的所有 hello 快照集和 hello 主要資料 （由主機寫入的資料）。 雖然重複資料刪除適合用來儲存空間效率，但更能 hello 的 「 什麼 」 hello 定域機組中複雜的問題。 hello 分層式的主要資料與 hello 快照集資料彼此重疊。 Hello 雲端資料的單一區塊做為階層式的主要資料，而且也在幾個快照集所參考。 每個雲端快照集可確保所有 hello 時間點資料的複本已鎖定到 hello 的雲端，刪除該快照集之前。

沒有參考 toothat 資料時，資料則只會刪除從 hello 雲端。 例如，如果我們建立 hello StorSimple 裝置中，然後刪除某些主要資料的雲端快照的 hello 的所有資料，我們會看到 hello_主要資料_立即卸除。 hello_雲端資料_包括 hello 階層式的資料和 hello 備份、 保留 hello 相同。 這是因為沒有仍然參考 hello 雲端資料的快照集。 Hello 雲端之後刪除快照集 （和參考的任何其他快照集 hello 相同的資料），雲端耗用量卸除。 我們在移除雲端資料之前，會檢查已無快照集仍參考該資料。 此程序稱為_回收_和 hello 裝置上正在執行背景服務。 移除雲端的資料不會立即當 hello 記憶體回收收集服務檢查有其他參考 toothat hello 刪除之前的資料。 記憶體回收的 hello 速度取決於 hello 總數的快照集和 hello 總資料。 一般而言，hello 雲端資料會清除少於一週內。


### <a name="thin-provisioning"></a>精簡佈建
精簡佈建是一種虛擬化技術，可用的存放裝置會出現 tooexceed 實體資源。 而是會預先保留足夠的儲存空間，StorSimple 會使用精簡佈建 tooallocate 剛好足夠空間 toomeet 目前的需求。 hello 彈性本質的雲端儲存體促進這種方法，因為 StorSimple 可以增加或減少雲端儲存體 toomeet 需求的變更。

> [!NOTE]
> 本機固定磁碟區不會精簡佈建。 建立 hello 磁碟區時，完整的佈建配置 tooa 僅本機磁碟區的存放裝置。


### <a name="deduplication-and-compression"></a>重複資料刪除和壓縮
Microsoft Azure StorSimple 使用重複資料刪除和資料壓縮 toofurther 降低儲存需求。

重複資料刪除可減少 hello 整體儲存藉由消除備援 hello 儲存資料集中的資料量。 當資訊變更時，StorSimple 會忽略 hello 保持不變的資料，並擷取只 hello 變更。 此外，StorSimple 可減少 hello 儲存的資料量，識別並移除不必要的資訊。 

> [!NOTE]
> 本機固定磁碟區上的資料不會進行重複資料刪除或壓縮。 不過，本機固定磁碟區的備份會進行重複資料刪除和壓縮。


## <a name="storsimple-workload-summary"></a>StorSimple 工作負載摘要
支援的 hello StorSimple 工作負載的摘要是下面製成資料表。

| 案例 | 工作負載 | 支援 | 限制 | 版本 |
| --- | --- | --- | --- | --- |
| 共同作業 |檔案共用 |是 | |所有版本 |
| 共同作業 |分散式檔案共用 |是 | |所有版本 |
| 共同作業 |SharePoint |是* |只有使用固定在本機的磁碟區時才支援 |Update 2 和更新版本 |
| 封存 |簡易檔案封存 |是 | |所有版本 |
| 虛擬化 |虛擬機器 |是* |只有使用固定在本機的磁碟區時才支援 |Update 2 和更新版本 |
| 資料庫 |SQL |是* |只有使用固定在本機的磁碟區時才支援 |Update 2 和更新版本 |
| 視訊監視 |視訊監視 |是* |StorSimple 裝置在專用的唯一 toothis 工作負載時，支援 |Update 2 和更新版本 |
| 備份 |主要目標備份 |是* |StorSimple 裝置在專用的唯一 toothis 工作負載時，支援 |Update 3 和更新版本 |
| 備份 |次要目標備份 |是* |StorSimple 裝置在專用的唯一 toothis 工作負載時，支援 |Update 3 和更新版本 |

是&#42; - 應套用解決方案指導方針和限制。

StorSimple 8000 系列裝置不支援下列工作負載的 hello。 如果部署於 StorSimple，這些工作負載將導致產生不支援的組態。

* 醫學造影
* Exchange
* VDI
* Oracle
* SAP
* 巨量資料
* 內容發佈
* 從 SCSI 開機

以下是 hello StorSimple 支援基礎結構元件的清單。

| 案例 | 工作負載 | 支援 | 限制 | 版本 |
| --- | --- | --- | --- | --- |
| 一般 |ExpressRoute |是 | |所有版本 |
| 一般 |DataCore FC |是* |使用 DataCore SANsymphony 時支援 |所有版本 |
| 一般 |DFSR |是* |只有使用固定在本機的磁碟區時才支援 |所有版本 |
| 一般 |編製索引 |是* |階層式磁碟區，僅支援中繼資料索引 (無資料)。<br>針對固定在本機的磁碟區，支援完整索引。 |所有版本 |
| 一般 |防毒 |是* |針對階層式磁碟區，只支援在開啟和關閉時進行掃描。<br> 針對固定在本機的磁碟區，支援完整掃描。 |所有版本 |

是&#42; - 應套用解決方案指導方針和限制。

以下是 StorSimple toobuild 解決方案可搭配其他軟體的清單。

| 工作負載類型 | 與 StorSimple 搭配使用的軟體 | 支援的版本|連結 toosolution 指南| 
| --- | --- | --- | --- |
| 備份目標 |Veeam |Veeam v 9 及更新版本 |[使用 StorSimple 做為 Veeam 的備份目標](storsimple-configure-backup-target-veeam.md)|
| 備份目標 |Veritas Backup Exec |Backup Exec 16 及更新版本 |[使用 StorSimple 做為 Backup Exec 的備份目標](storsimple-configure-backup-target-using-backup-exec.md)|
| 備份目標 |Veritas NetBackup |NetBackup 7.7.x 及更新版本  |[使用 StorSimple 做為 NetBackup 的備份目標](storsimple-configure-backuptarget-netbackup.md)|
| 通用檔案共用 <br></br> 共同作業 |Talon  |[StorSimple 搭配 Talon](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>StorSimple 詞彙
在部署之前您的 Microsoft Azure StorSimple 解決方案，我們建議您檢閱 hello 下列詞彙和定義。

### <a name="key-terms-and-definitions"></a>重要詞彙和定義
| 術語 (首字母縮寫或縮寫) | 說明 |
| --- | --- |
| 存取控制記錄 (ACR) |決定哪些主機可連接 tooit 您 Microsoft Azure StorSimple 裝置上的磁碟區相關聯的記錄。 hello 項決定根據 hello iSCSI 合格名稱 (IQN) 的資料連線 tooyour StorSimple 裝置 hello 主機 （包含在 hello ACR）。 |
| AES 256 |加密資料，從 hello 雲端移動 tooand 256 位元進階加密標準 (AES) 演算法。 |
| 配置單位大小 (AUS) |hello 最小磁碟空間可配置量 toohold 檔案在您的 Windows 檔案系統中。 如果檔案大小不是 hello 叢集大小的偶數倍數，額外的空間必須是使用的 toohold hello 檔案 (向上 toohello hello 叢集大小) 導致喪失空間和 hello 硬碟的分散程度。 <br>hello 建議 Azure StorSimple 磁碟區的 AUS 是 64 KB，因為它很適合的 hello 重複資料刪除演算法。 |
| 自動儲存體分層 |會自動移動較不作用中的資料從 Ssd tooHDDs 然後 tooa 層 hello 雲端，然後再啟用 從中央使用者介面的所有儲存體管理。 |
| 備份類別目錄 |備份，通常與 hello 應用程式類型所使用的集合。 這個集合會顯示在 hello hello StorSimple 裝置管理員服務 UI 的 [備份類別目錄] 刀鋒視窗。 |
| 備份類別目錄檔案 |包含一份目前儲存在 hello 備份資料庫的 StorSimple Snapshot Manager 中可用的快照集檔案。 |
| 備份原則 |選取的磁碟區、 備份類型以及可讓您在預先定義的排程的 toocreate 備份時間。 |
| 二進位大型物件 (BLOB) |二進位資料的集合，而這些二進位資料會在資料庫管理系統中儲存為單一實體。 BLOB 通常是影像、音訊或其他多媒體物件，但是有時二進位可執行程式碼會儲存為 BLOB。 |
| Challenge Handshake 驗證通訊協定 (CHAP) |Tooauthenticate hello 的對等的共用密碼或秘密的 hello 對等為基礎的連接使用的通訊協定。 CHAP 可以是單向或雙向。 使用單向 CHAP 時，hello 目標驗證啟動器。 相互 CHAP 要求 hello 目標驗證啟動器 hello 和該 hello 起始端驗證 hello 目標。 |
| 複製 |磁碟區的重複複本。 |
| 雲端即層次 (CaaT) |雲端儲存體整合成為 hello 儲存體架構內的一層，使所有儲存都體形 toobe 一個企業儲存體網路的一部分。 |
| 雲端服務提供者 (CSP) |雲端運算服務的提供者。 |
| 雲端快照 |Hello 雲端中儲存的磁碟區資料的時間點複本。 雲端快照相當 tooa 快照式複寫不同的異地儲存系統上。 雲端快照在災害復原案例中特別有用。 |
| 雲端儲存體加密金鑰 |密碼或使用您的裝置 toohello 雲端由傳送您 StorSimple 裝置 tooaccess hello 加密資料的索引鍵。 |
| 叢集感知更新 |管理容錯移轉叢集中的伺服器上的軟體更新，以便 hello 更新具有最小或不會影響服務可用性。 |
| 資料路徑 |功能單位的集合，而這些功能單位會執行互連的資料處理作業。 |
| 停用 |雲端服務之間的關聯線 hello hello StorSimple 裝置與 hello 之間連線的永久性動作。 Hello 裝置的雲端快照之後此程序會保留，可複製或用於災害復原。 |
| 磁碟鏡像 |複寫邏輯磁碟區個別硬碟上的磁碟機中即時 tooensure 持續可用性。 |
| 動態磁碟鏡像 |複寫動態磁碟上的邏輯磁碟區。 |
| 動態磁碟 |磁碟區格式使用 hello 邏輯磁碟管理員 (LDM) toostore 和管理跨多個實體磁碟的資料。 動態磁碟可以放大的 tooprovide 更多可用空間。 |
| 擴充的磁碟群 (EBOD) 機箱 |Microsoft Azure StorSimple 裝置的次要機箱，其中包含額外的硬碟來提供額外的儲存體。 |
| 豐富佈建 |傳統存放裝置佈建的儲存體中配置空間根據預期需求 （，通常超過目前需求的 hello）。 另請參閱 *精簡佈建*。 |
| 硬碟 (HDD) |使用旋轉盤 toostore 資料的磁碟機。 |
| 混合式雲端儲存體 |使用本機和異地資源 (包括雲端儲存體) 的儲存體架構。 |
| Internet Small Computer System Interface (iSCSI) |用於連結資料儲存設備或設施的網際網路通訊協定 (IP) 型儲存體網路標準。 |
| iSCSI 啟動器 |軟體元件，可讓執行 Windows tooconnect tooan 外部 iSCSI 型儲存體網路的主機電腦。 |
| iSCSI 合格名稱 (IQN) |識別 iSCSI 目標或啟動器的唯一名稱。 |
| iSCSI 目標 |一種軟體元件，可在存放區域網路中提供集中式 iSCSI 磁碟子系統。 |
| 即時封存 |儲存體中的封存資料可存取的方法 （它不儲存在異地在磁帶，例如） 的所有 hello 時間。 Microsoft Azure StorSimple 使用即時封存。 |
| 固定在本機的磁碟區 |磁碟區位於 hello 裝置上，而且永遠不會分層 toohello 雲端。 |
| 本機快照 |儲存在 hello Microsoft Azure StorSimple 裝置的磁碟區資料的時間點複本。 |
| Microsoft Azure StorSimple |功能強大的解決方案，包含資料中心儲存體應用裝置和軟體，讓 IT 組織 tooleverage 雲端儲存體好像資料中心儲存體。 StorSimple 可簡化資料保護和資料管理的方式，同時降低成本。 hello 方案合併透過與 hello 雲端的緊密整合的主要儲存體、 封存、 備份及災害復原 (DR)。 藉由結合企業級平台上的 SAN 儲存體和雲端資料管理，StorSimple 裝置啟用了所有儲存體相關需求的速度、簡化及可靠性。 |
| 電源和冷卻模組 (PCM) |您的 StorSimple 裝置 hello 電源和冷卻風扇，hello 所組成的硬體元件，因此 hello 電源和冷卻模組的名稱。 hello hello 裝置的主要機箱有兩個 764W Pcm，而 hello EBOD 機箱有兩個 580W Pcm。 |
| 主要機箱 |您的 StorSimple 裝置包含 hello 應用程式平台控制站的主要機箱。 |
| 復原時間目標 (RTO) |完全在損毀之後還原 hello 應該耗用在商務程序或系統之前的時間量上限。 |
| 序列連接 SCSI (SAS) |硬碟 (HDD) 的類型。 |
| 服務資料加密金鑰 |索引鍵進行可用 tooany 新 StorSimple 裝置會註冊以 hello StorSimple 裝置管理員服務。 hello StorSimple 裝置管理員服務與 hello 裝置之間傳送的 hello 組態資料會使用公開金鑰進行加密，然後僅在使用私密金鑰的 hello 裝置上進行解密。 服務資料加密金鑰可讓 hello 服務 tooobtain 此私密金鑰來解密。 |
| 服務註冊金鑰 |索引鍵，可協助向 hello StorSimple 裝置 hello StorSimple 裝置管理員服務使其出現在 hello Azure 入口網站進行未來管理動作。 |
| Small Computer System Interface (SCSI) |一組實際連接電腦並在它們之間傳送資料的標準。 |
| 固態硬碟 (SSD) |沒有包含任何移動組件的磁碟；例如，快閃磁碟機。 |
| storage account |一組存取認證連結 tooyour 儲存體帳戶指定的雲端服務提供者。 |
| StorSimple Adapter for SharePoint |Microsoft Azure StorSimple 元件，會明確地將 StorSimple 儲存體和資料保護延伸 tooSharePoint 伺服器陣列。 |
| StorSimple 裝置管理員服務 |擴充功能在您的 Azure StorSimple 內部部署和虛擬裝置 hello toomanage 可讓您的 Azure 入口網站。 |
| StorSimple Snapshot Manager |一種 Microsoft Management Console (MMC) 嵌入式管理單元，用於管理 Microsoft Azure StorSimple 中的備份和還原作業。 |
| 進行備份 |允許 hello 使用者 tootake 互動式備份的磁碟區的功能。 它是替代方法來取得手動備份的磁碟區為相對於 tootaking 自動化的備份透過定義的原則。 |
| 精簡佈建 |最佳化的 hello 可用儲存空間會使用儲存體系統中的 hello 效率的方法。 在精簡佈建 hello 最小空間所需的每個使用者在任何指定時間的多位使用者間配置 hello 儲存體。 另請參閱 *豐富佈建*。 |
| 分層 |排列依據目前使用量、 年齡和關聯性 tooother 資料的邏輯群組中的資料。 StorSimple 會自動排列各層的資料。 |
| 磁碟區 |Hello 磁碟機形式呈現的邏輯儲存體區域。 StorSimple 磁碟區對應 toohello 所 hello 主機，包括透過 iSCSI 和 StorSimple 裝置 hello 使用探索到掛接的磁碟區。 |
| 磁碟區容器 |磁碟區及套用 toothem hello 設定的群組。 StorSimple 裝置中分組為磁碟區容器的所有磁碟區。 磁碟區容器設定包括儲存體帳戶、 加密設定的資料傳送 toocloud 與相關聯的加密金鑰，以及牽涉 hello 雲端的作業所耗用的頻寬。 |
| 磁碟區群組 |在 StorSimple Snapshot Manager 中，磁碟區群組是設定的磁碟區 toofacilitate 備份處理的集合。 |
| 磁碟區陰影複製服務 (VSS) |藉由與 VSS 感知應用程式 toocoordinate hello 建立增量快照通訊促進應用程式一致性的 Windows Server 作業系統服務。 VSS 可確保取得快照時，會暫時停 hello 應用程式。 |
| Windows PowerShell for StorSimple |Windows powershell 命令列介面使用 toooperate 和管理您的 StorSimple 裝置。 保留一些 hello 的 Windows PowerShell 的基本功能，這個介面具有專為管理 StorSimple 裝置的其他專用的 cmdlet。 |

## <a name="next-steps"></a>後續步驟
深入了解 [StorSimple 安全性](storsimple-8000-security.md)。

