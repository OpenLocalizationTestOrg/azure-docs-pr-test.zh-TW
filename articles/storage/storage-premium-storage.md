---
title: "aaaHigh 效能 Premium 儲存體和 Azure 受管理磁碟 vm |Microsoft 文件"
description: "深入了解 Azure VM 高效能進階儲存體與受控磁碟。 Azure DS 系列、DSv2 系列、GS 系列和 Fs 系列 VM 支援進階儲存體。"
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 2474fa75116fe394672fde48520441fa80cf434f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>VM 高效能進階儲存體與受控磁碟
針對輸入/輸出 (I/O) 工作負載大的虛擬機器 (VM)，Azure 進階儲存體可提供高效能、低延遲的磁碟支援。 使用進階儲存體的 VM 磁碟會將資料儲存在固態硬碟 (SSD) 上。 tootake 優點的 hello 速度和效能的高階儲存體磁碟，您可以移轉現有的 VM 磁碟 tooPremium 儲存體。

在 Azure 中，您可以附加數個 premium 儲存體磁碟 tooa VM。 使用多個磁碟，可讓您註冊 too256 TB 的每個 VM 的存放裝置的應用程式。 使用 Premium 儲存體，您的應用程式可以達到 80,000 秒 I/O 作業 (IOPS) 每個 VM 和 too2，000 秒 mb (MB/s) 每個 VM 上的磁碟輸送量。 讀取作業的延遲極低。

使用 Premium 儲存體，Azure 會提供 hello 能力 tootruly 增益 shift 嚴苛企業應用程式類似 Dynamics AX、 Dynamics CRM、 Exchange Server、 SAP Business Suite，以及 SharePoint 伺服器陣列 toohello 雲端。 您可以在應用程式中執行強調效能、需要持續高效能和低延遲的資料庫工作負載，例如 SQL Server、Oracle、MongoDB、MySQL 和 Redis。

> [!NOTE]
> Hello 應用程式的最佳效能，我們建議您移轉任何需要高 IOPS tooPremium 儲存體的 VM 磁碟。 如果您的磁碟不需要高 IOPS，您可以將其保存在標準 Azure 儲存體中以控制成本。 在標準儲存體中，VM 磁碟會資料會儲存在硬碟機 (HDD) 而非 SSD 上。
> 

Azure 提供兩種方式 toocreate 高階儲存體磁碟的 Vm:

* **非受控磁碟**

    hello 原始方法是 toouse unmanaged 磁碟。 未受管理的磁碟，您可以管理 hello 儲存體帳戶，您會使用對應 tooyour VM 磁碟的 toostore hello 虛擬硬碟 (VHD) 檔案。 VHD 檔案會以分頁 Blob 的形式儲存在 Azure 儲存體帳戶中。 

* **受控磁碟**

    當您選擇[Azure 受管理磁碟](storage-managed-disks-overview.md)，Azure 管理您使用的 VM 磁碟的 hello 儲存體帳戶。 指定 hello 磁碟類型 （高階或標準） 以及您需要的 hello 磁碟 hello 大小。 Azure 會建立，並會為您管理 hello 磁碟。 您不需要 tooworry 有關置於您維持在延展性限制內使用的儲存體帳戶的多個儲存體帳戶 tooensure hello 磁碟。 Azure 會為您處理。

我們建議您選擇的受管理的磁碟，tootake 利用其許多功能。

高階儲存體，以啟動 tooget[建立免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。 

移轉您現有的 Vm tooPremium 儲存體的詳細資訊，請參閱[從 unmanaged 的磁碟 toomanaged 磁碟轉換為 Windows VM](../virtual-machines/virtual-machines-windows-convert-unmanaged-to-managed-disks.md)或[從 unmanaged 的磁碟 toomanaged 磁碟轉換 Linux VM](../virtual-machines/linux/convert-unmanaged-to-managed-disks.md)。

> [!NOTE]
> 進階儲存體可在大部分地區使用。 Hello 清單的區域，在[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services)，看看 hello 所在的區域支援高階支援大小系列 Vm (DS 系列、 DSV2 系列 GS 系列和 Fs 系列 Vm) 支援。
> 

## <a name="features"></a>特性

以下是一些進階儲存體的 hello 功能：

* **進階儲存體磁碟**

    Premium 儲存體支援的 VM 磁碟可以是附加 toospecific 大小系列 Vm。 進階儲存體支援 DS 系列、DSv2 系列、GS 系列、Ls 系列和 Fs 系列 VM。 您可以選擇七種磁碟大小：P4 (32GB)、P6 (64GB)、P10 (128GB)、P20 (512GB)、P30 (1024GB)、P40 (2048GB)、P50 (4095GB)。 受控磁碟至今僅支援 P4 和 P6 磁碟大小。 每個磁碟大小都有自己的效能規格。 根據您的應用程式需求，您可以附加一或多個磁碟 tooyour VM。 我們將描述更詳細地 hello 規格[高階儲存體延展性和效能目標](#scalability-and-performance-targets)。

* **進階分頁 Blob**

    進階儲存體支援分頁 Blob。 使用分頁 blob toostore 持續、 未受管理磁碟的高階儲存體中的 Vm。 不同於標準 Azure 儲存體，進階儲存體不支援區塊 Blob、附加 Blob、檔案、資料表或佇列。 Premium 分頁 blob 支援六個的大小從 P10 tooP50 和 P60 (8191GiB)。 P60 Premium 分頁 blob 不支援的 toobe 附加為 VM 磁碟。 

    任何放在進階儲存體帳戶中的物件都會是分頁 Blob。 hello 分頁 blob 貼齊的 hello tooone 支援佈建的大小。 這就是為什麼進階儲存體帳戶不是 toobe 用 toostore 小 blob。

* **進階儲存體帳戶**

    toostart 使用進階儲存體中，建立未受管理磁碟的 premium 儲存體帳戶。 在 hello [Azure 入口網站](https://portal.azure.com)，toocreate premium 儲存體帳戶中，選擇 hello **Premium**效能層。 選取 hello**本機備援儲存體 (LRS)** replication 選項。 您也可以建立進階儲存體帳戶 hello 類型設定太**Premium_LRS**其中一種 hello 下列位置：
    * [儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (2014-02-14 版或更新版本)
    * [服務管理 REST API](http://msdn.microsoft.com/library/azure/ee460799.aspx) (2014-10-01 版或更新版本；適用於傳統部署)
    * [Azure 儲存體資源提供者 REST API](https://docs.microsoft.com/rest/api/storagerp)(適用於 Azure Resource Manager 部署)
    * [Azure PowerShell](../powershell-install-configure.md) (0.8.10 版或更新版本)

    toolearn 需 premium 儲存體帳戶限制，請參閱[高階儲存體延展性和效能目標](#premium-storage-scalability-and-performance-targets)。

* **進階本地備援儲存體**

    進階儲存體帳戶做為 hello 複寫選項支援本機備援儲存體。 本機備援儲存體會保留三份 hello 資料，在單一區域。 針對區域性災害復原，您必須使用 [Azure 備份](../backup/backup-introduction-to-azure-backup.md)來備份位於不同區域的 VM 磁碟。 您也必須使用與 hello 備份保存庫的地理備援儲存體 (GRS) 帳戶。 

    Azure 會使用儲存體帳戶作為非受控磁碟的容器。 當您建立具有非受控磁碟的 Azure DS 系列、DSv2 系列、GS 系列或 Fs 系列 VM，並選取進階儲存體帳戶時，您的作業系統和資料磁碟會儲存在該儲存體帳戶中。

## <a name="supported-vms"></a>支援的 VM
進階儲存體支援 DS 系列、DSv2 系列、GS 系列、Ls 系列和 Fs 系列 VM。 這些 VM 類型可搭配標準和進階儲存體磁碟使用。 您不能將進階儲存體磁碟與不能和進階儲存體相容的 VM 系列搭配使用。

如需 Azure 中的 VM 類型和大小資訊 (適用於 Windows)，請參閱 [Windows VM 大小](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 如需 Azure 中的 VM 類型和大小資訊 (適用於 Linux)，請參閱 [ VM 大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

以下是一些 hello DS 系列、 DSv2 系列 GS 系列 hello 功能 Ls 系列和 Fs 系列 Vm:

* **雲端服務**

    您可以加入包含只 DS 系列 Vm 的 DS 系列 Vm tooa 雲端服務。 請勿將 DS 系列 Vm tooan 現有雲端服務，其 DS 系列 Vm 以外任何類型。 您可以移轉現有 Vhd tooa 新雲端服務執行只 DS 系列 Vm。 如果您想 toouse hello hello 新雲端服務裝載 DS 系列 Vm，使用的相同虛擬 IP 位址[保留的 IP 位址](../virtual-network/virtual-networks-instance-level-public-ip.md)。 GS 系列 Vm 可以加入 tooan 現有的雲端服務具有僅 GS 系列 Vm。

* **作業系統磁碟**

    您可以設定進階儲存體 VM toouse 高階或標準作業系統磁碟。 Hello 達到最佳體驗效果，我們建議使用 Premium 儲存體為基礎的作業系統磁碟。

* **資料磁碟**

    您可以使用 premium 和 standard 磁碟在 hello 相同 Premium 儲存體的 VM。 使用 Premium 儲存體，您可以佈建 VM，並將數個永續性資料磁碟 toohello VM。 如有需要 tooincrease hello 容量和效能的 hello 磁碟區，您可以等量分割您的磁碟。

    > [!NOTE]
    > 如果您使用[儲存空間](http://technet.microsoft.com/library/hh831739.aspx)來等量分割進階儲存體資料磁碟，應將儲存體空間設定為每個使用的磁碟各 1 資料行。 否則，整體 hello 等量磁碟區的效能可能會低於預期的流量分配因為跨 hello 磁碟。 根據預設，在 [伺服器管理員] 中，您可以設定 too8 磁碟上的資料行。 如果您有 8 個以上的磁碟，請使用 PowerShell toocreate hello 磁碟區。 手動指定資料行的 hello 的數目。 否則，hello 伺服器管理員 UI 會繼續 toouse 8 資料行，即使您有更多磁碟。 例如，如果您在單一等量磁碟區組有 32 個磁碟，請指定 32 個資料行。 資料行的 toospecify hello 數目 hello 虛擬磁碟的用途，在 hello [New-virtualdisk](http://technet.microsoft.com/library/hh848643.aspx) PowerShell 指令程式，使用 hello *NumberOfColumns*參數。 如需詳細資訊，請參閱[儲存體空間概觀](http://technet.microsoft.com/library/hh831739.aspx)和[儲存體空間常見問題集](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx)。
    >
    > 

* **快取**

    支援進階儲存體的 hello 大小數列中的 Vm 具有高的輸送量和延遲的唯一快取功能。 快取功能的 hello 超過基礎 premium 儲存體磁碟效能。 您可以設定太快取在高階儲存體磁碟上的原則 hello 磁碟**ReadOnly**， **ReadWrite**，或**無**。 hello 預設磁碟快取原則是**ReadOnly**所有高階資料磁碟和**ReadWrite**針對作業系統磁碟。 為了達到最佳效能，您的應用程式，使用 hello 正確快取設定。 例如，若為大量讀取或唯讀資料磁碟，SQL Server 資料檔案，例如設定 hello 磁碟太快取原則**ReadOnly**。 寫入繁重或唯寫的資料磁碟，例如 SQL Server 記錄檔，設定太快取原則的 hello 磁碟**無**。 toolearn 進一步了解最佳化您的設計，進階儲存體，請參閱[進階儲存體設計以取得效能](storage-premium-storage-performance.md)。

* **分析**

    tooanalyze 中進階儲存體，使用磁碟的 VM 效能開啟 VM 診斷在 hello [Azure 入口網站](https://portal.azure.com)。 如需詳細資訊，請參閱[使用 Azure 診斷擴充功能監視 Azure VM](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/) 

    toosee 磁碟效能、 使用作業系統為基礎的工具，例如[Windows 效能監視器](https://technet.microsoft.com/library/cc749249.aspx)用於 Windows Vm，hello [iostat](http://linux.die.net/man/1/iostat)命令適用於 Linux Vm。

* **VM 規模限制和效能**

    每個支援進階儲存體的 VM 大小的小數位數限制和 IOPS、 頻寬和 hello 數目可以連接每個 VM 磁碟的效能規格。 當您使用進階儲存體磁碟的 vm 時，請確定有足夠的 IOPS 與您的 VM toodrive 磁碟流量的頻寬。

    例如，STANDARD_DS1 VM 有 32 MB/秒的專用頻寬可運送進階儲存體磁碟流量。 P10 進階儲存體磁碟可以提供 100 MB/秒的頻寬。 如果附加的 toothis VM P10 premium 儲存體磁碟，它可以只向上 too32 MB/s。 它不能使用的 hello 可提供最大值 100 MB/s hello P10 磁碟。

    目前，hello hello DS 系列中的最大 VM 是 hello Standard_DS15_v2。 hello Standard_DS15_v2 可以註冊 too960 MB/s 提供在所有磁碟。 hello hello GS 系列中的最大 VM 為 hello Standard_GS5。 hello Standard_GS5 可以提供向上 too2，000 MB/s 在所有磁碟。

    請注意，這些限制僅適用於磁碟流量。 這些限制不包含快取點擊和網路流量。 VM 網路流量可使用各別的頻寬。 網路流量的頻寬與不同高階儲存體磁碟所使用的專用的 hello 頻寬。

    Hello 最新相關資訊最大 IOPS 及輸送量 （頻寬） 的進階儲存體支援的 Vm，請參閱[Windows VM 大小](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[Linux VM 大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

    如需 premium 儲存體磁碟和其 IOPS 及輸送量限制的詳細資訊，請參閱 hello hello 下一節中的資料表。

## <a name="scalability-and-performance-targets"></a>擴充和效能目標
在本節中，我們會說明 hello 延展性和效能目標 tooconsider，當您使用進階儲存體。

進階儲存體帳戶有下列延展性目標的 hello:

| 總帳戶容量 | 本地備援儲存體帳戶總頻寬 |
| --- | --- | 
| 磁碟容量：35 TB <br>快照容量：10 TB | 向上 too50 十億位元的每秒輸入<sup>1</sup> + 輸出<sup>2</sup> |

<sup>1</sup>傳送 tooa 儲存體帳戶的所有資料 （要求）

<sup>2</sup> 從儲存體帳戶接收的所有資料 (回應)

如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。

如果您使用進階儲存體帳戶未受管理的磁碟，而且您的應用程式超過 hello 延展性目標的單一儲存體帳戶，您可能想 toomigrate toomanaged 磁碟。 如果您不想 toomigrate toomanaged 磁碟，請建置應用程式 toouse 多個儲存體帳戶。 然後將資料分散到那些儲存體帳戶。 例如，如果您想 tooattach 51 TB 磁碟跨多個 Vm，分散到兩個儲存體帳戶。 35 TB 為 hello 單一高階儲存體帳戶的限制。 請務必確認單一進階儲存體帳戶的佈建磁碟決不超過 35 TB。

### <a name="premium-storage-disk-limits"></a>進階儲存體磁碟限制
當您佈建的 premium 儲存體磁碟 hello hello 磁碟大小會決定 hello 最大 IOPS 及輸送量 （頻寬）。 Azure 提供七種類型的進階儲存體磁碟：P4 (僅限受控磁碟)、P6 (僅限受控磁碟)、P10、P20、P30、P40 和 P50。 每個進階儲存體磁碟類型都有特定的 IOPS 和輸送量限制。 Hello 磁碟類型的限制詳述於下表中的 hello:

| 進階磁碟類型  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 磁碟大小           | 32 GB| 64 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| 每一磁碟的 IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| 每一磁碟的輸送量 | 每秒 25 MB  | 每秒 50 MB  | 每秒 100 MB | 每秒 150 MB | 每秒 200 MB | 每秒 250 MB | 每秒 250 MB | 

> [!NOTE]
> 請確定您 VM toodrive 磁碟的流量，提供足夠的頻寬是中所述[高階儲存體支援 Vm](#premium-storage-supported-vms)。 否則，您的磁碟輸送量和 IOPS 會受條件約束的 toolower 值。 最大輸送量和 IOPS 取決於 hello VM 限制，不能在 hello 磁碟限制 hello 前面表格中所述。  
> 
> 

以下是一些有關進階儲存體延展性和效能目標的重要事項 tooknow:

* **佈建的容量和效能**

    當您佈建 premium 儲存體磁碟，不同於標準的儲存體，您會保證 hello 容量、 IOPS 及輸送量該磁碟。 例如，如果您建立 P50 磁碟，Azure 會為該磁碟佈建 4,095 GB 儲存體容量、7,500 IOPS 和 250 MB/秒的輸送量。 您的應用程式可以使用全部或一部分 hello 容量和效能。

* **磁碟大小**

    Azure 對應 hello 最接近的 premium 儲存體磁碟的選項，因為 hello 前面一節中的 hello 表中所指定的磁碟大小 （無條件進位） toohello。 例如，100 GB 的磁碟大小會分類為 P10 選項。 它可以執行向上 too500 IOPS 與 too100 MB/s 輸送量設定。 同樣地，400 GB 的磁碟會分類為 P20。 它可以執行 too2，300 IOPS，150 MB/s 輸送量設定。
    
    > [!NOTE]
    > 您可以輕鬆增加 hello 的現有磁碟的大小。 例如，您可能想 30 GB 的磁碟 too128 GB 或甚至 too1 TB tooincrease hello 大小。 或者，您可能想 tooconvert P20 磁碟 tooa P30 磁碟因為您需要更多容量或多個 IOPS 及輸送量。 
    > 
 
* **I/O 大小**

    hello I/O 大小為 256 KB。 如果正在傳輸的 hello 資料是少於 256 KB，則會視為 1 個 I/O 單位。 較大的 I/O 大小則會視為大小是 256 KB 的多個 I/O。 例如，1,100 KB 的 I/O 會視為 5 個 I/O 單位。

* **輸送量**

    hello 輸送量限制包括寫入 toohello 磁碟，並包含不由 hello 快取的磁碟讀取的作業。 例如，P10 磁碟具有每一磁碟 100 MB/秒的輸送量。 有效輸送量 P10 磁碟的一些範例是以 hello 下表所示：

    | 每個 P10 磁碟的輸送量上限 | 來自磁碟的非快取讀取 | 非快取寫入 toodisk |
    | --- | --- | --- |
    | 100 MB/秒 | 100 MB/秒 | 0 |
    | 100 MB/秒 | 0 | 100 MB/秒 |
    | 100 MB/秒 | 60 MB/秒 | 40 MB/秒 |

* **快取點擊**

    快取叫用不會受到 hello IOPS 或輸送量 hello 磁碟配置。 例如，當您使用的資料磁碟**ReadOnly**支援進階儲存體，所服務的 hello 快取讀取的 VM 上設定快取不主旨 toohello IOPS 及輸送量 caps 的 hello 磁碟。 如果磁碟的 hello 工作負載主要是讀取時，您可能會很高的輸送量。 hello 快取是主體 tooseparate IOPS 及輸送量限制在 hello VM 層級，根據 hello VM 大小。 DS 系列 VM 大約有 4000 IOPS，而快取與本機 SSD I/O 是每個核心 33 MB/秒的輸送量。 GS 系列 VM 有 5000 IOPS 的限制，而快取與本機 SSD I/O 是每個核心 50 MB/秒的輸送量。 

## <a name="throttling"></a>節流
節流設定可能會發生，如果您的應用程式的 IOPS 或輸送量超過 premium 儲存體磁碟配置的 hello 限制。 節流也可能是如果您在 hello VM 上的所有磁碟的總磁碟流量超過 hello 供 hello VM 的磁碟頻寬限制。 tooavoid 節流，我們建議您的暫止的 hello 磁碟的 I/O 要求的 hello 數目限制。 使用限制，根據您已佈建，hello 磁碟的延展性和效能目標以及 hello 磁碟頻寬可用 toohello VM。  

當它設計您的應用程式可以達到 hello 最低延遲 tooavoid 節流。 不過，如果 hello 擱置中的 hello 磁碟的 I/O 要求的數目太小，您的應用程式無法利用 hello 的最大 IOPS 及輸送量層級是可用 toohello 磁碟。

hello 遵循範例示範如何 toocalculate 節流層級。 所有計算都是以 256 KB 的 I/O 單位大小為基礎。

### <a name="example-1"></a>範例 1
在 P10 磁碟上，您的應用程式一秒內已處理 495 個 16 KB 大小的 I/O 單位。 hello I/O 單位會視為 495 IOPS。 如果您嘗試在 2 MB I/O 第二個 hello 相同，hello I/O 單位總數等於 too495 + 8 的 IOPS。 這是因為 2 MB I/O = 2048 KB/256 KB = 8 I/O 單位時 hello I/O 單位大小 256 KB。 因為 495 + 8 hello 總和超過 hello 磁碟 hello 500 IOPS 限制，節流就會發生。

### <a name="example-2"></a>範例 2
在 P10 磁碟上，您的應用程式已處理 400 個 256 KB 大小的 I/O 單位。 hello 耗用的總頻寬 （400 &#215; 256） / 1024 KB = 100 MB/s。 P10 磁碟的輸送量限制為 100 MB/秒。 如果您的應用程式嘗試 tooperform 更多 I/O 作業的第二個，它已節流，因為它超過 hello 配置限制。

### <a name="example-3"></a>範例 3
DS4 VM 連接了兩個 P30 磁碟。 每個 P30 磁碟有 200 MB/秒的輸送量。 不過，DS4 VM 有256 MB/秒的磁碟總頻寬容量。 您不能上的磁碟機這兩個已連接的磁碟 toohello 最大輸送量在 hello 這個 DS4 VM 相同的時間。 tooresolve，您也可以承受 200 MB 的流量/一個磁碟上的是 s 和 56 MB/s 在 hello 其他磁碟。 如果磁碟流量 hello 總和超過 256 MB/s，磁碟流量已節流。

> [!NOTE]
> 如果磁碟流量大多包含小型的 I/O 大小，您的應用程式可能會達到 hello hello 輸送量限制之前的 IOPS 限制。 不過，如果 hello 磁碟流量大多包含大型的 I/O 大小，您的應用程式可能會達到 hello 輸送量限制第一次，而非 hello IOPS 限制。 您可以使用最佳 I/O 大小，將應用程式 IOPS 和輸送量的容量最大化。 此外，您可以限制 hello 暫止數目的磁碟 I/O 要求。
> 

toolearn 更多有關設計的高效能使用高階儲存體，請參閱[進階儲存體設計以取得效能](storage-premium-storage-performance.md)。

## <a name="snapshots-and-copy-blob"></a>快照與複製 Blob

toohello 儲存體服務，hello VHD 檔案是分頁 blob。 您可以使用分頁 blob 的快照集，並將它們複製 tooanother 位置，例如 tooa 不同儲存體帳戶。

### <a name="unmanaged-disks"></a>非受控磁碟

建立[增量快照](storage-incremental-snapshots.md)unmanaged 的高階磁碟 hello 相同的標準儲存體中使用快照集的方式。 高階儲存體支援本機備援儲存體做為 hello 複寫選項。 我們建議您建立快照集，然後複製 hello 快照 tooa 異地備援的標準儲存體帳戶。 如需詳細資訊，請參閱 [Azure 儲存體備援選項](storage-redundancy.md)。

如果磁碟已附加的 tooa VM，不允許某些 hello 磁碟上的應用程式開發介面作業。 例如，您無法執行[複製 Blob](/rest/api/storageservices/Copy-Blob)作業於 blob 如果 hello 磁碟已附加 tooa VM。 相反地，使用 hello 第一次建立 blob 的快照集[快照集 Blob](/rest/api/storageservices/Snapshot-Blob) REST API。 然後，執行 hello[複製 Blob](/rest/api/storageservices/Copy-Blob) hello 快照 toocopy hello 的附加磁碟。 或者，您可以卸離 hello 磁碟，然後再執行任何必要的作業。

hello 下列限制適用於 toopremium 儲存體 blob 快照集：

| 進階儲存體限制 | 值 |
| --- | --- |
| 每個 Blob 的快照數目上限 | 100 |
| 快照集的儲存體帳戶容量<br>(僅包含快照集中的資料。 不包含基本 Blob 中的資料)。 | 10 TB |
| 連續快照之間的時間下限 | 10 分鐘 |

toomaintain 異地備援您快照集副本，您可以複製快照集從 premium 儲存體帳戶 tooa 異地備援的標準儲存體帳戶使用 AzCopy 或複製 Blob。 如需詳細資訊，請參閱[傳輸資料與 hello AzCopy 命令列公用程式](storage-use-azcopy.md)和[複製 Blob](/rest/api/storageservices/Copy-Blob)。

如需對進階儲存體帳戶中分頁 Blob 執行 REST 作業的詳細資訊，請參閱[使用 Azure 進階儲存體的 Blob 服務作業](http://go.microsoft.com/fwlink/?LinkId=521969)。

### <a name="managed-disks"></a>受控磁碟

受管理磁碟的快照集是 hello 受管理磁碟的唯讀副本。 hello 快照都會儲存為標準的受管理磁碟。 [增量快照](storage-incremental-snapshots.md)目前不支援受控磁碟。 toolearn tootake 受管理的磁碟，快照集如何查看[建立副本儲存為 Azure 受管理的 VHD 磁碟在 Windows 中使用受管理的快照集](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md)或[建立副本儲存為 Azure 受管理的 VHD 磁碟使用受管理在 Linux 中的快照集](../virtual-machines/linux/snapshot-copy-managed-disk.md)。

如果受管理的磁碟附加的 tooa VM，不允許某些 hello 磁碟上的應用程式開發介面作業。 比方說，您無法在附加的 tooa VM hello 磁碟時，產生共用的存取簽章 (SAS) tooperform 複製作業。 相反地，第一次建立 hello 磁碟的快照集，然後再執行 hello hello 快照集副本。 或者，您可以卸離 hello 磁碟，並接著產生 SAS tooperform hello 複製作業。


## <a name="premium-storage-for-linux-vms"></a>適用於 Linux Vm 的進階儲存體
您可以使用下列資訊 toohelp 您設定您的 Linux Vm，高階儲存體中的 hello:

tooachieve 延展性目標高階儲存體中的所有進階儲存體磁碟與快都取設定太**ReadOnly**或**無**，掛接 hello 檔案系統時，您必須停用 「 屏障 」。 因為 hello 寫入 toopremium 存放磁碟是永久性的這些快取設定，您不需要在此案例中的障礙。 Hello 寫入的要求已成功完成時，資料已寫入 toohello 持續性存放區。 toodisable 「 屏障 」，可使用其中一個 hello 下列方法。 選擇您的檔案系統的其中一個 hello:
  
* 如**reiserFS**，toodisable 障礙使用 hello`barrier=none`裝載選項。 (使用 tooenable 障礙`barrier=flush`。)
* 如**ext3/ext4**，toodisable 障礙使用 hello`barrier=0`裝載選項。 (使用 tooenable 障礙`barrier=1`。)
* 如**XFS**，toodisable 障礙使用 hello`nobarrier`裝載選項。 (使用 tooenable 障礙`barrier`。)
* 高階儲存體磁碟快取設定太**ReadWrite**，啟用寫入的持久性的障礙。
* 讓磁碟區標籤 toopersist hello VM 重新啟動後您必須更新 /etc/fstab hello 通用唯一識別碼 (UUID) 參考 toohello 磁碟。 如需詳細資訊，請參閱[新增受管理的磁碟 tooa Linux VM](../virtual-machines/linux/add-disk.md)。

下列 Linux 散發套件 hello Azure 高階儲存體的已經驗證過。 取得較佳的效能和穩定性進階儲存體，我們建議您升級的這些版本中，至少您 Vm tooone (tooa 或更新版本)。 某些 hello 版本需要 azure hello 最新 Linux Integration Services (LIS)，v4.0。 toodownload 並安裝散發，請遵循 hello hello 下表中所列的連結。 當我們完成驗證，我們會加入 toohello 的影像清單。 請注意，我們的驗證顯示每個映像的效能各有所不同。 效能取決於工作負載特性和映像上的設定。 不同的映像已針對不同種類的工作負載進行調整。

| 配送映像 | 版本 | 支援的核心 | 詳細資料 |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-server-20150123-en-us-30GB |
| Debian | 7.x、8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| suse-sles-12-priority-v20150213 <br> suse-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5、6.6、6.7、7.0 | &nbsp; | [LIS4 (必要)](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *請參閱 hello 下一節中的附註* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 (建議使用) ](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *請參閱 hello 下一節中的附註* |
| Red Hat Enterprise Linux (RHEL) | 6.8+、7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 或 RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 或 RHCK w/[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 或 RHCK w/[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>Openlogic CentOS 的 LIS 驅動程式

如果您正在 OpenLogic CentOS Vm，請執行下列命令 tooinstall hello 最新驅動程式的 hello:

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

tooactivate hello 新驅動程式，重新啟動 hello 電腦。

## <a name="pricing-and-billing"></a>價格和計費

當您使用進階儲存體時，適用於 hello 遵循計費考量：

* **進階儲存體磁碟和 Blob 大小**

    Premium 儲存體磁碟或 blob 的計費取決於 hello 佈建的 hello 磁碟或 blob 的大小。 Azure 對應 hello （無條件進位） 佈建的大小 toohello 最接近的 premium 儲存體磁碟的選項。 如需詳細資訊，請參閱中的 hello 表格[高階儲存體延展性和效能目標](#premium-storage-scalability-and-performance-targets)。 支援每個磁碟對應 tooa 佈建磁碟大小，並據此計費。 對於所有已佈建的磁碟計費每小時按比例 hello 高階儲存體供應項目的使用 hello 每月價格。 比方說，如果您佈建 P10 磁碟，並刪除 20 小時後，您所要支付 hello P10 計算按比例分配的 too20 小時供應項目。 這是不論 hello 實際寫入的資料數量 toohello 磁碟或 hello IOPS 及輸送量使用。

* **進階非受控磁碟快照集**

    不受管理的高階磁碟上的快照集所要支付 hello hello 快照集所使用的額外容量。 如需有關快照的詳細資訊，請參閱[建立 Blob 的快照](/rest/api/storageservices/Snapshot-Blob)。

* **進階受控磁碟快照集**

    受管理磁碟的快照集是 hello 磁碟的唯讀副本。 hello 磁碟儲存為標準的受管理磁碟。 為標準受管理的磁碟，快照集成本 hello 相同。 比方說，如果您採用 128 GB premium 的受管理磁碟的快照集，hello 成本 hello 快照集是相等 tooa 128 GB 的標準受管理的磁碟。  

* **輸出資料傳輸**

    [輸出資料傳輸](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure 資料中心送出的資料) 會產生頻寬使用量費用。

如需進階儲存體、進階儲存體支援的 VM 和受控磁碟的價格詳細資訊，請參閱以下文章：

* [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)
* [虛擬機器價格](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [受控磁碟價格](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Azure 備份支援 

針對區域性災害復原，您必須使用 [Azure 備份](../backup/backup-introduction-to-azure-backup.md)來備份位於不同區域的 VM 磁碟，並以 GRS 儲存體帳戶作為備份保存庫。

toocreate 以時間為基礎的備份、 簡單的 VM 還原與備份保留原則的備份作業使用 Azure Backup。 您可以搭配非受控和受控磁碟使用備份。 如需詳細資訊，請參閱 [適用於 VM 的 Azure 備份與非受控磁碟](../backup/backup-azure-vms-first-look-arm.md)和[適用於 VM 的 Azure 備份與受控磁碟](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)。 

## <a name="next-steps"></a>後續步驟
如需 Premium 儲存體的詳細資訊，請參閱下列文章 hello。

### <a name="design-and-implement-with-premium-storage"></a>使用進階儲存體進行設計和實作
* [使用進階儲存體設計高效能](storage-premium-storage-performance.md)
* [進階儲存體的 Blob 儲存體作業](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>作業指引
* [移轉 tooAzure 高階儲存體](storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>部落格文章
* [Azure 進階儲存體正式推出](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [發表 hello GS 系列： 新增支援進階儲存體 toohello，最大 hello 公用雲端中的 Vm](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
