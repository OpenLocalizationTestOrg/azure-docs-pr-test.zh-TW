---
title: "VM 高效能進階儲存體和 Azure 受控磁碟 | Microsoft Docs"
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
ms.openlocfilehash: 559753d7ff3da7e8b5dc8f976368a1d35dd6258b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>VM 高效能進階儲存體與受控磁碟
針對輸入/輸出 (I/O) 工作負載大的虛擬機器 (VM)，Azure 進階儲存體可提供高效能、低延遲的磁碟支援。 使用進階儲存體的 VM 磁碟會將資料儲存在固態硬碟 (SSD) 上。 您可以將現有 VM 磁碟移轉到進階儲存體，以利用進階儲存體磁碟的速度和效能。

在 Azure 中，您可以將多部進階儲存體磁碟連結至 VM。 使用多部磁碟可讓您的應用程式在每部 VM 上獲得最多 256 TB 的儲存空間。 透過進階儲存體，您的應用程式可在每部 VM 上達到每秒執行 80,000 I/O 作業 (IOPS)，以及每部 VM 上的磁碟輸送量達每秒 2,000 MB (MB/秒)。 讀取作業的延遲極低。

Azure 使用進階儲存體，提供您將要求較高的企業應用程式 (例如 Dynamics AX、Dynamics CRM、Exchange Server、SAP Business Suite 和 SharePoint 伺服器陣列) 隨即轉移至雲端的能力。 您可以在應用程式中執行強調效能、需要持續高效能和低延遲的資料庫工作負載，例如 SQL Server、Oracle、MongoDB、MySQL 和 Redis。

> [!NOTE]
> 為了發揮應用程式最佳效能，我們建議您將任何需要高 IOPS 的 VM 磁碟移轉到進階儲存體。 如果您的磁碟不需要高 IOPS，您可以將其保存在標準 Azure 儲存體中以控制成本。 在標準儲存體中，VM 磁碟會資料會儲存在硬碟機 (HDD) 而非 SSD 上。
> 

Azure 提供兩種建立 VM 進階儲存體磁碟的方法：

* **非受控磁碟**

    原始方法是使用非受控磁碟。 在非受控磁碟中，您可以管理用來儲存虛擬硬碟 (VHD) 檔案 (對應至您的 VM 磁碟) 的儲存體帳戶。 VHD 檔案會以分頁 Blob 的形式儲存在 Azure 儲存體帳戶中。 

* **受控磁碟**

    當您選擇 [Azure 受控磁碟](../../virtual-machines/windows/managed-disks-overview.md)時，Azure 就會管理您用於 VM 磁碟的儲存體帳戶。 您可以指定需要的磁碟類型 (進階或標準) 和磁碟大小。 Azure 會為您建立並管理該磁碟。 您不必擔心將磁碟分配在多個儲存體帳戶中，以確保維持在儲存體帳戶的延展性限制內。 Azure 會為您處理。

我們建議您選擇受控磁碟，以便運用其中多種功能。

若要開始使用進階儲存體，[請建立免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。 

如需將現有 VM 移轉到進階儲存體的詳細資訊，請參閱[將 Windows VM 從非受控磁碟轉換至控磁碟](../../virtual-machines/windows/convert-unmanaged-to-managed-disks.md)或[將 Linux VM 從非受控磁碟轉換至受控磁碟](../../virtual-machines/linux/convert-unmanaged-to-managed-disks.md)。

> [!NOTE]
> 進階儲存體可在大部分地區使用。 如需可用區域的清單，請在[依區域的 Azure 服務](https://azure.microsoft.com/regions/#services)中查看哪些區域支援受支援的進階支援大小系列 VM (DS 系列、DSV2 系列、GS 系列和 Fs 系列 Vm)。
> 

## <a name="features"></a>特性

以下是進階儲存體的一些功能：

* **進階儲存體磁碟**

    進階儲存體支援可連結至特定大小系列 VM 的 VM 磁碟。 進階儲存體支援 DS 系列、DSv2 系列、GS 系列、Ls 系列和 Fs 系列 VM。 您可以選擇七種磁碟大小：P4 (32GB)、P6 (64GB)、P10 (128GB)、P20 (512GB)、P30 (1024GB)、P40 (2048GB)、P50 (4095GB)。 受控磁碟至今僅支援 P4 和 P6 磁碟大小。 每個磁碟大小都有自己的效能規格。 端視您的應用程式需求而定，您可以將一或多個磁碟連結至您的 VM。 在[進階儲存體延展性和效能目標 ](#scalability-and-performance-targets)中，我們會更詳細地說明規格。

* **進階分頁 Blob**

    進階儲存體支援分頁 Blob。 可使用分頁 Blob 將 VM 的永續性非受控磁碟儲存在進階儲存體中。 不同於標準 Azure 儲存體，進階儲存體不支援區塊 Blob、附加 Blob、檔案、資料表或佇列。 進階分頁 Blob 支援六種大小，範圍從 P10 到 P50 以及 P60 (8191GiB)。 不支援連接 P60 進階分頁 Blob 作為 VM 磁碟。 

    任何放在進階儲存體帳戶中的物件都會是分頁 Blob。 分頁 Blob 會貼齊其中一個支援的佈建大小。 這就是進階儲存體帳戶不是用於儲存小型 Blob 的原因。

* **進階儲存體帳戶**

    若要開始使用進階儲存體，請為非受控磁碟建立進階儲存體帳戶。 若要在 [Azure 入口網站](https://portal.azure.com)中建立進階儲存體帳戶，請選擇**進階**效能層級。 選取 [本地備援儲存體 (LRS)] 複寫選項。 您也可以在以下其中一個位置中將類型設為 **Premium_LRS**，以建立進階儲存體帳戶：
    * [儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (2014-02-14 版或更新版本)
    * [服務管理 REST API](http://msdn.microsoft.com/library/azure/ee460799.aspx) (2014-10-01 版或更新版本；適用於傳統部署)
    * [Azure 儲存體資源提供者 REST API](https://docs.microsoft.com/rest/api/storagerp)(適用於 Azure Resource Manager 部署)
    * [Azure PowerShell](/powershell/azureps-cmdlets-docs.md) (0.8.10 版或更新版本)

    若要深入了解進階儲存體帳戶限制，請參閱[進階儲存體延展性和效能目標](#premium-storage-scalability-and-performance-targets)。

* **進階本地備援儲存體**

    進階儲存體帳戶僅支援本地備援儲存體作為複寫選項。 本地備援儲存體會在單一區域內保留三份資料副本。 針對區域性災害復原，您必須使用 [Azure 備份](../../backup/backup-introduction-to-azure-backup.md)來備份位於不同區域的 VM 磁碟。 您也必須使用異地備援儲存體 (GRS) 帳戶作為備份保存庫。 

    Azure 會使用儲存體帳戶作為非受控磁碟的容器。 當您建立具有非受控磁碟的 Azure DS 系列、DSv2 系列、GS 系列或 Fs 系列 VM，並選取進階儲存體帳戶時，您的作業系統和資料磁碟會儲存在該儲存體帳戶中。

## <a name="supported-vms"></a>支援的 VM
進階儲存體支援 DS 系列、DSv2 系列、GS 系列、Ls 系列和 Fs 系列 VM。 這些 VM 類型可搭配標準和進階儲存體磁碟使用。 您不能將進階儲存體磁碟與不能和進階儲存體相容的 VM 系列搭配使用。

如需 Azure 中的 VM 類型和大小資訊 (適用於 Windows)，請參閱 [Windows VM 大小](../../virtual-machines/virtual-machines-windows-sizes-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 如需 Azure 中的 VM 類型和大小資訊 (適用於 Linux)，請參閱 [ VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

以下是 DS 系列、DSv2 系列、GS 系列、Ls 系列及 Fs 系列 VM 的一些功能：

* **雲端服務**

    您可以將 DS 系列 VM 新增至只有 DS 系列 VM 的雲端服務。 請勿將 DS 系列 VM 新增至包含非 DS 系列類型 VM 的現有雲端服務。 您可以將現有的 VHD 移轉到僅執行 DS 系列 VM 的新雲端服務。 如果您想要為裝載 DS 系列 VM 的新雲端服務使用相同的虛擬 IP 位址，請使用[保留的 IP 位址](../../virtual-network/virtual-networks-instance-level-public-ip.md)。 GS 系列 VM 可以新增至僅執行 GS 系列 VM 的現有雲端服務。

* **作業系統磁碟**

    您可以將進階儲存體 VM 設定為使用進階或標準作業系統磁碟。 為獲得最佳體驗，我們建議使用進階儲存體型的作業系統磁碟。

* **資料磁碟**

    您可以在相同的進階儲存體 VM 中使用進階和標準磁碟。 使用進階儲存體，您可以佈建 VM 並將幾個永續性資料磁碟附加至 VM。 如有需要，您可以在磁碟上等量分割磁碟區以增加磁碟區的容量和效能。

    > [!NOTE]
    > 如果您使用[儲存空間](http://technet.microsoft.com/library/hh831739.aspx)來等量分割進階儲存體資料磁碟，應將儲存體空間設定為每個使用的磁碟各 1 資料行。 否則，等量磁碟區的整體效能可能會因為磁碟流量分配不平均而比預期的效能還低。 依預設，您可以在伺服器管理員中設定最多 8 個磁碟的資料行。 如果您有 8 個以上的磁碟，請使用 PowerShell 來建立磁碟區。 以手動方式指定資料行數目。 否則，即使您擁有更多磁碟，伺服器管理員 UI 還是會繼續使用 8 個資料行。 例如，如果您在單一等量磁碟區組有 32 個磁碟，請指定 32 個資料行。 若要指定虛擬磁碟所使用的資料行數目，您可以在 [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) PowerShell Cmdlet 中使用 *NumberOfColumns* 參數。 如需詳細資訊，請參閱[儲存體空間概觀](http://technet.microsoft.com/library/hh831739.aspx)和[儲存體空間常見問題集](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx)。
    >
    > 

* **快取**

    支援進階儲存體的大小系列 VM 有獨特的快取功能，在輸送量和延遲上有高層級的表現。 快取功能遠超過基礎進階儲存體磁碟的效能。 您可以在進階儲存體磁碟上將磁碟快取原則設定為 **ReadOnly**、**ReadWrite** 或 **None**。 所有進階資料磁碟的預設磁碟快取原則都是 **ReadOnly**，而作業系統磁碟的磁碟快取原則是 **ReadWrite**。 為獲得最佳的應用程式效能，請使用正確的快取設定。 例如，對於讀取繁重或唯讀資料磁碟 (如 SQL Server 資料檔)，將磁碟快取原則設定為 **ReadOnly**。 例如，對於寫入繁重或唯寫資料磁碟 (如 SQL Server 記錄檔)，將磁碟快取原則設定為 。 請參閱[使用進階儲存體設計高效能](storage-premium-storage-performance.md)，以深入了解如何最佳化進階儲存體。

* **分析**

    若要使用進階儲存體中的磁碟分析 VM 效能，請開啟 [Azure 入口網站](https://portal.azure.com)中的 VM 診斷。 如需詳細資訊，請參閱[使用 Azure 診斷擴充功能監視 Azure VM](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/) 

    若要查看磁碟效能，請使用作業系統工具，例如適用於 Windows VM 的 [Windows 效能監視器](https://technet.microsoft.com/library/cc749249.aspx)和適用於 Linux VM 的 [iostat](http://linux.die.net/man/1/iostat)。

* **VM 規模限制和效能**

    在 IOPS、頻寬及每個 VM 可連結的磁碟數目上，進階儲存體支援的每個 VM 大小都有規模限制和效能規格。 使用進階儲存體磁碟搭配 VM 時，請確定 VM 上有足夠的 IOPS 和頻寬可用來運送磁碟流量。

    例如，STANDARD_DS1 VM 有 32 MB/秒的專用頻寬可運送進階儲存體磁碟流量。 P10 進階儲存體磁碟可以提供 100 MB/秒的頻寬。 如果 P10 進階儲存體磁碟連結至此 VM，則最高只能達到 32 MB/秒。 無法使用 P10 磁碟可提供的 100 MB/秒上限。

    DS 系列中目前最大的 VM 是 Standard_DS15_v2。 Standard_DS15_v2 可以在所有磁碟上提供高達 960 MB/秒的速度。 GS 系列中最大的 VM 是 Standard_GS5。 Standard_GS5 可以在所有磁碟上提供高達 2,000 MB/秒的速度。

    請注意，這些限制僅適用於磁碟流量。 這些限制不包含快取點擊和網路流量。 VM 網路流量可使用各別的頻寬。 網路流量的頻寬與進階儲存體磁碟使用的專用頻寬不同。

    若想要針對進階儲存體支援的 VM，深入了解最新的 IOPS 和輸送量 (頻寬) 上限資訊，請參閱 [Windows VM 大小](/azure/virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或 [Linux VM 大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

    如需進階儲存體磁碟和其 IOPS 與輸送量限制的詳細資訊，請參閱下一節中的資料表。

## <a name="scalability-and-performance-targets"></a>擴充和效能目標
在這一節中，我們會說明使用進階儲存體時要考慮的延展性和效能目標。

進階儲存體帳戶有下列延展性目標：

| 總帳戶容量 | 本地備援儲存體帳戶總頻寬 |
| --- | --- | 
| 磁碟容量：35 TB <br>快照容量：10 TB | 每秒最多 50 GB (輸入 <sup>1</sup> + 輸出 <sup>2</sup> |

<sup>1</sup> 傳送至儲存體帳戶的所有資料 (要求)

<sup>2</sup> 從儲存體帳戶接收的所有資料 (回應)

如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。

如果您針對非受控磁碟使用進階儲存體帳戶，而您的應用程式超過單一儲存體帳戶的延展性目標，您可能會想要移轉至受控磁碟。 如果您不想要移轉至受控磁碟，請將應用程式建置為使用多個儲存體帳戶。 然後將資料分散到那些儲存體帳戶。 例如，如果您想要將 51 TB 的磁碟連結至多個 VM，可將其分散到兩個儲存體帳戶。 單一進階儲存體帳戶的限制是 35 TB。 請務必確認單一進階儲存體帳戶的佈建磁碟決不超過 35 TB。

### <a name="premium-storage-disk-limits"></a>進階儲存體磁碟限制
當您佈建進階儲存體磁碟時，磁碟的大小決定 IOPS 和輸送量 (頻寬) 上限。 Azure 提供七種類型的進階儲存體磁碟：P4 (僅限受控磁碟)、P6 (僅限受控磁碟)、P10、P20、P30、P40 和 P50。 每個進階儲存體磁碟類型都有特定的 IOPS 和輸送量限制。 磁碟類型的限制如下表說明︰

| 進階磁碟類型  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 磁碟大小           | 32 GB| 64 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| 每一磁碟的 IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| 每一磁碟的輸送量 | 每秒 25 MB  | 每秒 50 MB  | 每秒 100 MB | 每秒 150 MB | 每秒 200 MB | 每秒 250 MB | 每秒 250 MB | 

> [!NOTE]
> 請確定 VM 上有足夠的頻寬可用來輸送磁碟流量，如[進階儲存體支援的 VM](#premium-storage-supported-vms) 中所述。 否則，您的磁碟輸送量和 IOPS 會限制在較低的值。 最大輸送量和 IOPS 是根據 VM 的限制，不是在上表中所述的磁碟限制。  
> 
> 

以下是有關進階儲存體延展性和效能目標的一些重要須知︰

* **佈建的容量和效能**

    當您佈建進階儲存體磁碟時，不同於標準儲存體的是，您可獲得該磁碟的容量、IOPS 和輸送量保證。 例如，如果您建立 P50 磁碟，Azure 會為該磁碟佈建 4,095 GB 儲存體容量、7,500 IOPS 和 250 MB/秒的輸送量。 您的應用程式可以使用全部或部分的容量和效能。

* **磁碟大小**

    Azure 會將磁碟大小對應 (無條件進位) 至上節表格中最接近的進階儲存體磁碟選項。 例如，100 GB 的磁碟大小會分類為 P10 選項。 P10 可執行最多 500 IOPS，並包含最多 100 MB/秒的輸送量。 同樣地，400 GB 的磁碟會分類為 P20。 P20 可執行最多 2,300 IOPS，並包含 150 MB/秒的輸送量。
    
    > [!NOTE]
    > 您可以輕易增加現有磁碟的大小。 例如，您可以將 30 GB 磁碟的大小增加到 128 GB，甚至 1 TB。 或者，因為您需要更多容量或更多的 IOPS 和輸送量，您也可以將 P20 磁碟轉換為 P30 磁碟。 
    > 
 
* **I/O 大小**

    I/O 大小為 256 KB。 如果要傳送的資料少於 256 KB，會視為 1 個 I/O 單位。 較大的 I/O 大小則會視為大小是 256 KB 的多個 I/O。 例如，1,100 KB 的 I/O 會視為 5 個 I/O 單位。

* **輸送量**

    輸送量限制包含寫入至磁碟，以及包含不是透過快取執行的磁碟讀取作業。 例如，P10 磁碟具有每一磁碟 100 MB/秒的輸送量。 P10 磁碟的一些有效輸送量範例如下表所示：

    | 每個 P10 磁碟的輸送量上限 | 來自磁碟的非快取讀取 | 傳至磁碟的非快取寫入 |
    | --- | --- | --- |
    | 100 MB/秒 | 100 MB/秒 | 0 |
    | 100 MB/秒 | 0 | 100 MB/秒 |
    | 100 MB/秒 | 60 MB/秒 | 40 MB/秒 |

* **快取點擊**

    快取點擊不會受到磁碟配置 IOPS 或輸送量的限制。 例如，當您在進階儲存體支援的 VM 上使用具有 **ReadOnly**快取設定的資料磁碟時，從快取提供的「讀取數」並不受限於磁碟的 IOPS 和輸送量上限。 如果磁碟的工作負載是以讀取為主，您可以獲得極高的輸送量。 在 VM 層級上，根據 VM 大小，快取會受到不同的 IOPS 和輸送量限制。 DS 系列 VM 大約有 4000 IOPS，而快取與本機 SSD I/O 是每個核心 33 MB/秒的輸送量。 GS 系列 VM 有 5000 IOPS 的限制，而快取與本機 SSD I/O 是每個核心 50 MB/秒的輸送量。 

## <a name="throttling"></a>節流
如果您的應用程式 IOPS 或輸送量超過進階儲存體磁碟的配置限制，可能會發生節流。 也可能是因為 VM 上所有磁碟的總磁碟流量，超過 VM 上可用的磁碟頻寬，因而發生節流。 若要避免節流，我們建議您限制磁碟擱置 I/O 要求的數量限制。 請根據所佈建磁碟的延展性和效能目標，以及 VM 上可用的磁碟頻寬來使用限制。  

當您的應用程式設計為避免節流情況時，可以達到最低延遲。 但是，如果磁碟的擱置 I/O 要求數過小，您的應用程式便無法達到磁碟最大的 IOPS 和輸送量層級。

下列範例示範如何計算節流層級。 所有計算都是以 256 KB 的 I/O 單位大小為基礎。

### <a name="example-1"></a>範例 1
在 P10 磁碟上，您的應用程式一秒內已處理 495 個 16 KB 大小的 I/O 單位。 I/O 單位會視為 495 IOPS。 如果您在該秒內嘗試 2 MB 的 I/O，I/O 單位的總數會等於 495 + 8 IOPS。 這是因為當 I/O 單位大小是 256 KB 時，2 MB I/O = 2,048 KB / 256 KB = 8 個 I/O 單位。 因為 495 + 8 的總和超出磁碟 500 IOPS 的限制，因此會發生節流情況。

### <a name="example-2"></a>範例 2
在 P10 磁碟上，您的應用程式已處理 400 個 256 KB 大小的 I/O 單位。 耗用的總頻寬是 (400 &#215; 256) / 1,024 KB = 100 MB/秒。 P10 磁碟的輸送量限制為 100 MB/秒。 如果您的應用程式嘗試在該秒內執行更多 I/O 作業，便會發生節流情況，因為會超出配置的限制。

### <a name="example-3"></a>範例 3
DS4 VM 連接了兩個 P30 磁碟。 每個 P30 磁碟有 200 MB/秒的輸送量。 不過，DS4 VM 有256 MB/秒的磁碟總頻寬容量。 此 DS4 VM 上連結的磁碟無法同時達到最大的輸送量。 若要解決這個問題，您可以在一個磁碟上維持 200 MB/秒的流量，在另一個磁碟上維持 56 MB/秒的流量。 如果您的磁碟流量總和超過每秒 256 MB/秒，磁碟流量就會發生節流。

> [!NOTE]
> 如果磁碟流量大多包含小型 I/O，您的應用程式在達到輸送量限制前很可能會先達到 IOPS 限制。 但是，如果磁碟流量大多包含大型 I/O，您的應用程式可能會達到輸送量限制，而非 IOPS 限制。 您可以使用最佳 I/O 大小，將應用程式 IOPS 和輸送量的容量最大化。 此外，您可以限制磁碟的擱置 I/O 要求數目。
> 

若要了解如何使用進階儲存體設計高效能，請參閱[使用進階儲存體設計高效能](storage-premium-storage-performance.md)。

## <a name="snapshots-and-copy-blob"></a>快照與複製 Blob

對於儲存體服務而言，VHD 檔案是分頁 Blob。 您可以建立分頁 Blob 的快照集，然後複製到另一個位置，例如不同的儲存體帳戶。

### <a name="unmanaged-disks"></a>非受控磁碟

就像對標準儲存體使用快照集一樣，您可以使用相同方式為非受控進階磁碟建立[增量快照集](../../virtual-machines/windows/incremental-snapshots.md)。 進階儲存體僅支援本地備援儲存體作為複寫選項。 建議您建立快照，並將那些快照複製到異地備援的標準儲存體帳戶。 如需詳細資訊，請參閱 [Azure 儲存體備援選項](storage-redundancy.md)。

如果磁碟已連結至 VM，則磁碟上不允許某些 API 作業。 例如，如果磁碟連結至 VM，您就無法在該 Blob 上執行[複製 Blob](/rest/api/storageservices/Copy-Blob) 作業。 相反地，先使用[快照集 Blob](/rest/api/storageservices/Snapshot-Blob) REST API 來建立該 Blob 的快照集。 然後執行快照集的[複製 Blob](/rest/api/storageservices/Copy-Blob) 來複製連結的磁碟。 或者，您可以中斷連結磁碟，再執行任何必要的作業。

進階儲存體 Blob 快照集有下列限制︰

| 進階儲存體限制 | 值 |
| --- | --- |
| 每個 Blob 的快照數目上限 | 100 |
| 快照集的儲存體帳戶容量<br>(僅包含快照集中的資料。 不包含基本 Blob 中的資料)。 | 10 TB |
| 連續快照之間的時間下限 | 10 分鐘 |

若要維護快照集的異地備援副本，您可以使用 AzCopy 或「複製 Blob」，將進階儲存體帳戶中的快照複製到異地備援的標準儲存體帳戶。 如需詳細資訊，請參閱[使用 AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md)和[複製 Blob](/rest/api/storageservices/Copy-Blob)。

如需對進階儲存體帳戶中分頁 Blob 執行 REST 作業的詳細資訊，請參閱[使用 Azure 進階儲存體的 Blob 服務作業](http://go.microsoft.com/fwlink/?LinkId=521969)。

### <a name="managed-disks"></a>受控磁碟

受控磁碟的快照集是受控磁碟的唯讀複本。 快照集會儲存為標準受管理磁碟。 [增量快照](../../virtual-machines/windows/incremental-snapshots.md)目前不支援受控磁碟。 若要了解如何建立受控磁碟的快照集，請參閱[在 Windows 中使用受管理的快照集建立 VHD 的複本並儲存為 Azure 受控磁碟](../../virtual-machines/windows/snapshot-copy-managed-disk.md)或[在 Linux 中使用受管理的快照集建立 VHD 的複本並儲存為 Azure 受控磁碟](../../virtual-machines/linux/snapshot-copy-managed-disk.md)。

如果受控磁碟已連結至 VM，則磁碟上不允許某些 API 作業。 例如，當磁碟已附加至 VM 時，您無法產生共用存取簽章 (SAS) 來執行複製作業。 請先建立磁碟的快照集，再複製快照集。 或者，您可以中斷連結磁碟，然後產生 SAS 來執行複製作業。


## <a name="premium-storage-for-linux-vms"></a>適用於 Linux Vm 的進階儲存體
您可以使用下列資訊協助您在進階儲存體中設定 Linux VM：

對於快取設定為 **ReadOnly** 或 **None** 的所有 Premium 儲存體磁碟，若要達到進階儲存體的延展性目標，您必須在掛接檔案系統時停用 "barrier" (阻礙)。 此案例中您不需要阻礙，因為對這些快取設定而言，寫入進階儲存體磁碟是持久的。 寫入要求成功完成時，資料就已寫入永久性的存放區。 若要停用 "barrier" (阻礙)，請使用下列其中一種方法。 請選擇適用您檔案系統的方法︰
  
* 若是 **reiserFS**，請使用 `barrier=none` 掛接選項停用阻礙。 (若要啟用阻礙，請使用 `barrier=flush`。)
* 若是 **ext3/ext4**，請使用 `barrier=0` 掛接選項停用阻礙。 (若要啟用阻礙，請使用 `barrier=1`。)
* 若是 **XFS**，請使用 `nobarrier` 掛接選項停用阻礙。 (若要啟用阻礙，請使用 `barrier`。)
* 對於快取設定為 **ReadWrite** 的進階儲存體，請啟用寫入持續性的障礙。
* 對於要在 VM 重新開機後保存的磁碟機標籤，您必須以參考磁碟的通用唯一識別碼 (UUID) 更新 /etc/fstab。 如需詳細資訊，請參閱[將受控磁碟新增至 Linux VM](../../virtual-machines/linux/add-disk.md)。

下列 Linux 散發套件經過驗證，可使用 Azure 進階儲存體。 為獲得進階儲存體的最佳效能和穩定性，我們建議至少將您的 VM 升級到以下其中一個版本 (或更新版本)。 部分版本需要適用於 Azure 的最新 Linux Integration Services 4.0 版。 若要下載並安裝散發套件，請遵循下表所列的連結。 完成驗證時，我們會將映像新增至清單中。 請注意，我們的驗證顯示每個映像的效能各有所不同。 效能取決於工作負載特性和映像上的設定。 不同的映像已針對不同種類的工作負載進行調整。

| 配送映像 | 版本 | 支援的核心 | 詳細資料 |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-server-20150123-en-us-30GB |
| Debian | 7.x、8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| suse-sles-12-priority-v20150213 <br> suse-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5、6.6、6.7、7.0 | &nbsp; | [LIS4 (必要)](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *請參閱下一節中的附註* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 (建議使用) ](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *請參閱下一節中的附註* |
| Red Hat Enterprise Linux (RHEL) | 6.8+、7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 或 RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 或 RHCK w/[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 或 RHCK w/[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>Openlogic CentOS 的 LIS 驅動程式

如果您執行 OpenLogic CentOS VM，請執行下列命令以安裝最新的驅動程式：

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

若要啟動新的驅動程式，請重新啟動電腦。

## <a name="pricing-and-billing"></a>價格和計費

使用進階儲存體時，需考量下列計費資訊：

* **進階儲存體磁碟和 Blob 大小**

    進階儲存體磁碟或 Blob 的計費依據是磁碟或 Blob 得佈建大小。 Azure 會將佈建大小對應 (無條件進位) 至最接近的進階儲存體磁碟選項。 如需詳細資訊，請參閱[進階儲存體延展性和效能目標](#premium-storage-scalability-and-performance-targets)中的表格。 每一個磁碟對應至一個支援的佈建大小，並據此計費。 任何已佈建的磁碟都是使用每月的進階儲存體優惠價格，以每小時的方式計費。 例如，如果您在佈建完 P10 磁碟的 20 小時後刪除它，則會以 20 小時計算 P10 解決方案的費用。 這與寫入磁碟的實際資料量或使用的 IOPS 和輸送量無關。

* **進階非受控磁碟快照集**

    進階非受控磁碟上的快照集會因為額外使用的容量而產生費用。 如需有關快照的詳細資訊，請參閱[建立 Blob 的快照](/rest/api/storageservices/Snapshot-Blob)。

* **進階受控磁碟快照集**

    受控磁碟的快照集是該磁碟的唯讀複本。 磁碟會儲存為標準受控磁碟。 快照集的成本與標準受控磁碟相同。 例如，如果您建立 128 GB 進階受控磁碟的快照集，快照集的成本就等於 128 GB 標準受控磁碟的成本。  

* **輸出資料傳輸**

    [輸出資料傳輸](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure 資料中心送出的資料) 會產生頻寬使用量費用。

如需進階儲存體、進階儲存體支援的 VM 和受控磁碟的價格詳細資訊，請參閱以下文章：

* [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)
* [虛擬機器價格](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [受控磁碟價格](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Azure 備份支援 

針對區域性災害復原，您必須使用 [Azure 備份](../../backup/backup-introduction-to-azure-backup.md)來備份位於不同區域的 VM 磁碟，並以 GRS 儲存體帳戶作為備份保存庫。

若要建立具有以時間為基礎的備份、簡易 VM 還原，以及備份保留原則的備份作業，請使用 Azure 備份。 您可以搭配非受控和受控磁碟使用備份。 如需詳細資訊，請參閱 [適用於 VM 的 Azure 備份與非受控磁碟](../../backup/backup-azure-vms-first-look-arm.md)和[適用於 VM 的 Azure 備份與受控磁碟](../../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)。 

## <a name="next-steps"></a>後續步驟
如需進階儲存體的詳細資訊，請參閱下列文章。

### <a name="design-and-implement-with-premium-storage"></a>使用進階儲存體進行設計和實作
* [使用進階儲存體設計高效能](storage-premium-storage-performance.md)
* [進階儲存體的 Blob 儲存體作業](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>作業指引
* [移轉到 Azure 進階儲存體](../common/storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>部落格文章
* [Azure 進階儲存體正式推出](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [宣佈 GS 系列︰將進階儲存體支援加入至公用雲端中的最大 VM](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
