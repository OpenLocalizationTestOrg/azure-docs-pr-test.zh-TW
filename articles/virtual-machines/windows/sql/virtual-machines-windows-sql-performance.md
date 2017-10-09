---
title: "aaaPerformance Azure 中的 SQL Server 的最佳作法 |Microsoft 文件"
description: "提供將 Microsoft Azure VM 中 SQL Server 效能最佳化的最佳作法。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Azure 虛擬機器中的 SQL Server 效能最佳做法

## <a name="overview"></a>Overview

本主題提供將「Microsoft Azure 虛擬機器」中的 SQL Server 效能最佳化的最佳做法。 在 Azure 虛擬機器中執行 SQL Server，我們建議您繼續使用 hello 相同資料庫效能微調適用 tooSQL 伺服器在內部部署伺服器環境中的選項。 不過，在公用雲端中的關聯式資料庫的 hello 效能取決於許多因素，例如 hello 的虛擬機器和 hello 設定 hello 資料磁碟的大小。

建立 SQL Server 影像時[佈建 hello Azure 入口網站中的 Vm，請考慮](virtual-machines-windows-portal-sql-server-provision.md)。 SQL Server Vm 佈建 hello 入口網站與資源管理員中實作所有這些最佳做法，包括 hello 存放裝置設定。

本文著重於取得 hello*最佳*Azure Vm 上的 SQL Server 的效能。 如果您的工作負載需求較低，可能就不需要採用下列每一項最佳化條件。 評估以下建議時，請考慮您的效能需求和工作負載模式。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>快速檢查清單

hello 以下是為了達到最佳效能的 Azure 虛擬機器上的 SQL Server 的快速檢查清單：

| 領域 | 最佳化 |
| --- | --- |
| [VM 大小](#vm-size-guidance) |SQL Enterprise Edition 的 [DS3](../../virtual-machines-windows-sizes-memory.md) 或更高版本。<br/><br/>SQL Standard 和 Web Edition 的 [DS2](../../virtual-machines-windows-sizes-memory.md) 或更高版本。 |
| [儲存體](#storage-guidance) |使用[進階儲存體](../../../storage/common/storage-premium-storage.md)。 標準儲存體只建議用於開發/測試。<br/><br/>保留 hello[儲存體帳戶](../../../storage/common/storage-create-storage-account.md)與 hello 中的 SQL Server VM 相同的區域。<br/><br/>停用 Azure[地理備援儲存體](../../../storage/common/storage-redundancy.md)（地理複寫） hello 儲存體帳戶上。 |
| [磁碟](#disks-guidance) |使用至少 2 個 [P30 磁碟](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (1 個用於儲存記錄檔案，另 1 個用於儲存資料檔案和存放 TempDB)。<br/><br/>避免使用作業系統或暫存磁碟作為資料儲存體或進行記錄。<br/><br/>啟用 hello hello 資料檔和 TempDB 所裝載的磁碟上的讀取快取。<br/><br/>請勿啟用裝載 hello 記錄檔的磁碟上快取。<br/><br/>重要事項： 停止變更 hello Azure VM 磁碟的快取設定時的 hello SQL Server 服務。<br/><br/>等量分割多個 Azure 資料磁碟 tooget 提高 IO 輸送量。<br/><br/>以文件上記載的配置大小格式化。 |
| [I/O](#io-guidance) |啟用 [資料庫頁面壓縮] 功能　。<br/><br/>針對資料檔案，啟用 [立即檔案初始化] 功能。<br/><br/>限制或停用 hello 資料庫上的自動成長。<br/><br/>停用 autoshrink hello 資料庫上。<br/><br/>移動所有資料庫 toodata 磁碟，包括系統資料庫。<br/><br/>移動 SQL Server 錯誤記錄檔和追蹤檔案目錄 toodata 磁碟。<br/><br/>設定預設備份和資料庫檔案位置。<br/><br/>啟用鎖定的頁面。<br/><br/>套用 SQL Server 效能修正程式。 |
| [特定功能](#feature-specific-guidance) |將備份直接 tooblob 儲存體。 |

如需有關*如何*和*為什麼*toomake 這些最佳化，請檢閱 hello 詳細資料和下列各節將提供的指引。

## <a name="vm-size-guidance"></a>VM 大小指引

對於效能敏感應用程式，建議您使用 hello 下列[虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**：DS3 或更高版本
* **SQL Server Standard 和 Web Edition**：DS2 或更高版本

## <a name="storage-guidance"></a>儲存體指引

DS 系列 (以及 DSv2 系列和 GS 系列) VM 支援 [進階儲存體](../../../storage/common/storage-premium-storage.md)。 針對所有生產環境工作負載，建議使用進階儲存體。

> [!WARNING]
> 標準儲存體具有不同的延遲和頻寬，並建議僅用於開發/測試工作負載。 生產工作負載應該使用進階儲存體。

此外，我們建議您建立 Azure 儲存體帳戶，在 hello 與 SQL Server 虛擬機器 tooreduce 傳輸延遲的相同資料中心。 建立儲存體帳戶時，請停用 [異地複寫] 功能，因為跨多個磁碟時無法保證寫入順序一致。 請考慮另一個方法，在兩個 Azure 資料中心之間設定 SQL Server 災害復原技術。 如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 高可用性和災害復原](virtual-machines-windows-sql-high-availability-dr.md)。

## <a name="disks-guidance"></a>磁碟指引

Azure VM 上有三種主要的磁碟類型︰

* **作業系統磁碟**: hello 平台當您建立 Azure 虛擬機器時，將連接至少一個磁碟 (標示為 「 hello **C**磁碟機) toohello VM 的作業系統磁碟。 此磁碟是以分頁 Blob 的形式儲存於儲存體的 VHD。
* **暫存磁碟**: Azure 虛擬機器包含稱為 hello 暫存磁碟的另一個磁碟 (標示為 「 hello **D**： 磁碟機)。 這是可用來塗銷空間的 hello 節點上的磁碟。
* **資料磁碟**： 您也可以附加額外的磁碟 tooyour 虛擬機器做為資料磁碟，而且這些將會儲存在儲存體中做為分頁 blob。

hello 下列章節說明使用這些不同的磁碟的建議。

### <a name="operating-system-disk"></a>作業系統磁碟

作業系統磁碟是指可開機，並掛接為執行的作業系統版本，且標示為 **C** 磁碟機的 VHD。

快取原則 hello 作業系統磁碟上的預設值是**讀/寫**。 對於效能敏感應用程式，我們建議您使用資料磁碟而非 hello 作業系統磁碟。 請參閱以下的資料磁碟 hello 一節。

### <a name="temporary-disk"></a>暫存磁碟

hello 暫存磁碟機，標示為 「 hello **D**： 磁碟機，不是保存的 tooAzure blob 儲存體。 不會儲存您的使用者資料庫檔案或使用者交易記錄檔上 hello **D**： 磁碟機。

D 系列、 Dv2 系列和 G 系列 Vm，hello 這些 Vm 上的暫存磁碟機是以 SSD 為基礎。 如果您的工作負載 （例如，用於暫存物件或複雜聯結），大量使用 TempDB 儲存 TempDB 上 hello **D**磁碟機可能會導致較高的 TempDB 輸送量並降低 TempDB 延遲。

對於支援「進階儲存體」的 VM (DS 系列、DSv2 系列與 GS 系列)，建議您將 TempDB 儲存在支援「進階儲存體」且啟用讀取快取的磁碟上。 沒有例外狀況 toothis 建議的做法之一。如果 TempDB 使用量是密集寫入，您可以達到較高的效能 hello 本機上儲存 TempDB **D**磁碟機，這也是 ssd 這些機器的大小。

### <a name="data-disks"></a>資料磁碟

* **用於資料和記錄檔中的資料磁碟**： 最少使用 2 高階儲存體[P30 磁碟](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets)其中一個磁碟包含 hello 記錄檔，而其他 hello 包含 hello 資料和 TempDB 檔案。 每個高階儲存體磁碟提供許多 IOPs 與頻寬 (MB/s)，其大小，而定，hello 下列文章中所述：[使用進階儲存體磁碟](../../../storage/common/storage-premium-storage.md)。

* **磁碟等量分割**︰如需更多的輸送量，您可以新增其他資料磁碟，並使用「磁碟等量分割」。 toodetermine hello 資料磁碟數目，您需要 IOPS 和您的記錄檔，以及您的資料和 TempDB 檔案所需的頻寬 tooanalyze hello 數目。 請注意，不同的 VM 大小就會有不同的限制之 IOPs 及支援頻寬的 hello 數目，請參閱上每個 IOPS hello 資料表[VM 大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 使用下列指導方針的 hello:

  * 對於 Windows 8/Windows Server 2012 或更新版本，使用[儲存空間](https://technet.microsoft.com/library/hh831739.aspx)以 hello 指導方針：

      1. 設定 hello 交錯 （等量磁碟區大小） too64 KB （65536 個位元組） 針對 OLTP 工作負載和資料倉儲工作負載 tooavoid 效能影響由於 toopartition 對齊錯誤 256 KB （262144 位元組為單位）。 必須使用 PowerShell 來設定。
      1. 設定資料行數目 = 實體磁碟數量。 設定 8 個以上的磁碟 (不是伺服器管理員 UI) 時，使用 PowerShell。 

    例如，下列 PowerShell hello 建立新儲存集區以 hello 交錯大小 too64 KB hello 數目及資料行 too2:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Windows 2008 R2 或更早版本，您可以使用動態磁碟 （OS 等量磁碟區），而且 hello 等量磁碟區大小一律是 64 KB。 請注意，Windows 8/Windows Server 2012 已不再提供此選項。 詳細資訊，請參閱 hello 支援聲明[虛擬磁碟服務正轉換 tooWindows 存放管理 API](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx)。

  * 如果您的工作負載不需大量記錄及，且不需專屬於 IOP，您可以只設定一個儲存體集區。 否則，建立兩個儲存集區，一個用於 hello 記錄檔，另一個儲存集區 hello 資料檔和 TempDB。 判斷 hello 根據您的負載預期每個儲存體集區相關聯的磁碟數目。 請注意，各 VM 大小所允許連接的資料磁碟數量皆不同。 如需相關資訊，請參閱[虛擬機器的大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

  * 如果您不會使用進階儲存體 （開發/測試案例），hello 建議 tooadd hello 最大的資料磁碟數目受到您[VM 大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)並使用磁碟條狀配置。

* **快取原則**： 進階儲存體的資料磁碟，可讓您啟用僅裝載您的資料檔和 TempDB hello 資料磁碟的讀取快取。 如果您並非使用進階儲存體，請勿啟用任何資料磁碟上的任何快取功能。 如需設定磁碟快取，指示，請參閱下列主題中的 hello: [Set-azureosdisk](https://msdn.microsoft.com/library/azure/jj152847)和[Set-azuredatadisk](https://msdn.microsoft.com/library/azure/jj152851.aspx)。

  > [!WARNING]
  > 變更 Azure VM 的任何資料庫損毀磁碟 tooavoid hello 可能性 hello 快取設定，請停止 hello SQL Server 服務。

* **NTFS 配置單位大小**： 格式化時 hello 資料磁碟，建議您針對資料和記錄檔以及 TempDB 使用 64 KB 配置單位大小。

* **磁碟管理的最佳作法**： 當移除資料磁碟或變更其快取的內容型別時，則在 hello 變更期間停止 hello SQL Server 服務。 Hello 快取設定時在 hello OS 磁碟上變更 Azure 停止 hello VM、 變更 hello 快取類型，並重新啟動 hello VM。 當變更資料磁碟的 hello 快取設定時，未停止 hello VM，但 hello 資料磁碟中斷的 hello VM hello 期間變更，然後重新附加。

  > [!WARNING]
  > 失敗 toostop hello SQL Server 服務，這些作業期間可能會造成資料庫損毀。

## <a name="io-guidance"></a>I/O 指引

* 當您將平行處理應用程式和要求時，可達到 hello 的進階儲存體最佳的結果。 高階儲存體設計的情況下 hello IO 佇列深度大於 1，所以 （即使它們是需要大量的儲存體），您會看到單一執行緒序列的要求幾乎沒有任何效能提升。 比方說，這可能會影響效能分析工具，像是 SQLIO hello 單一執行緒測試結果。

* 請考慮使用 [資料庫頁面壓縮](https://msdn.microsoft.com/library/cc280449.aspx) 功能，其有助於改善 I/O 密集型工作負載的效能。 不過，hello 資料壓縮可能會增加 hello hello 資料庫伺服器上的 CPU 耗用量。

* 請考慮啟用立即檔案初始化 tooreduce hello 時間所需的初始檔案配置。 tootake 利用立即檔案初始化的方法，您可以授與 hello SQL Server (MSSQLSERVER) 服務帳戶的 SE_MANAGE_VOLUME_NAME，並將它加入 toohello**執行磁碟區維護工作**安全性原則。 如果您使用 azure 的 SQL Server 平台映像，hello 預設服務帳戶 (NT Service\MSSQLSERVER) 不會新增 toohello**執行磁碟區維護工作**安全性原則。 也就是說，SQL Server Azure 平台映像未啟用 [立即檔案初始化] 功能。 加入 hello SQL Server 服務帳戶 toohello 之後**執行磁碟區維護工作**安全性原則、 重新啟動 hello SQL Server 服務。 使用此功能時，可能有安全性考量。 如需詳細資訊，請參閱 [資料庫檔案初始化](https://msdn.microsoft.com/library/ms175935.aspx)。

* **自動成長**會被視為 toobe 只預期成長的偶發事件。 請勿每天使用「自動成長」功能，管理資料和記錄成長。 如果使用 autogrow，預先加大 hello 檔案使用 hello 大小參數。

* 請確定**autoshrink**是已停用的 tooavoid 不必要的負擔會嚴重影響效能。

* 移動所有資料庫 toodata 磁碟，包括系統資料庫。 如需詳細資訊，請參閱 [移動系統資料庫](https://msdn.microsoft.com/library/ms345408.aspx)。

* 移動 SQL Server 錯誤記錄檔和追蹤檔案目錄 toodata 磁碟。 在 SQL Server 組態管理員中，以滑鼠右鍵按一下您的 SQL Server 執行個體並選取內容，即可完成。 hello 錯誤記錄檔和追蹤檔案可變更設定中 hello**啟動參數**hello 中指定傾印目錄 索引標籤 hello**進階** 索引標籤 hello 下列螢幕擷取畫面顯示在哪裡的 toolookhello 錯誤記錄檔啟動參數。

    ![SQL ErrorLog 螢幕擷取畫面](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* 設定預設備份和資料庫檔案位置。 使用本主題中的 hello 建議，和 hello 伺服器屬性 視窗中的 hello 變更。 如需指示，請參閱[檢視或變更 hello 資料及記錄檔 (SQL Server Management Studio) 的預設位置](https://msdn.microsoft.com/library/dd206993.aspx)。 hello 下列螢幕擷取畫面示範 where toomake 這些變更。

    ![SQL 資料記錄和備份檔案](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* 啟用鎖定頁面 tooreduce IO 和任何分頁活動。 如需詳細資訊，請參閱[啟用 hello 鎖定記憶體分頁選項 (Windows)](https://msdn.microsoft.com/library/ms190730.aspx)。

* 如果您執行的是 SQL Server 2012，請安裝 Service Pack 1 累計更新 10。 當您執行 select into temporary table 陳述式 SQL Server 2012 中，此更新包含 hello I/O 效能不佳的修正程式。 如需相關資訊，請參閱此 [知識庫文章](http://support.microsoft.com/kb/2958012)。

* 將資料檔案傳輸至 Azure，或從 Azure 往外傳輸時，請考慮先壓縮所有資料檔案。

## <a name="feature-specific-guidance"></a>特定功能指引

有些部署作業可能會使用更進階的組態技術，提供額外的效能優點。 hello 下列清單強調一些可協助您 tooachieve 更佳的效能的 SQL Server 功能：

* **備份 tooAzure 儲存**： 當執行備份的 Azure 虛擬機器中執行的 SQL Server，您可以使用[SQL Server 備份 tooURL](https://msdn.microsoft.com/library/dn435916.aspx)。 這項功能是開始可用之 SQL Server 2012 SP1 CU2 和備份 toohello 附加資料磁碟的建議。 當您備份/還原至/自 Azure 儲存體，請遵循所提供的 hello 建議[SQL Server Backup tooURL 最佳作法和疑難排解及還原的備份儲存在 Azure 儲存體](https://msdn.microsoft.com/library/jj919149.aspx)。 您也可以使用 [Azure 虛擬機器中的 SQL Server 自動備份](virtual-machines-windows-sql-automated-backup.md)，自動執行這些備份作業。

    您可以使用先前 tooSQL Server 2012， [SQL Server 備份 tooAzure 工具](https://www.microsoft.com/download/details.aspx?id=40740)。 此工具可協助使用多個備份等量磁碟區目標 tooincrease 備份輸送量。

* **Azure 中的 SQL Server 資料檔案**：從 SQL Server 2014 開始提供 [Azure 中的 SQL Server 資料檔](https://msdn.microsoft.com/library/dn385720.aspx)這項新功能。 在 Azure 中執行具有資料檔案的 SQL Server 的效能與使用 Azure 資料磁碟的效能特性相當。

## <a name="next-steps"></a>後續步驟

如需安全性的最佳作法，請參閱 [Azure 虛擬機器中的 SQL Server 安全性考量](virtual-machines-windows-sql-security.md)。

請檢閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)中的其他「SQL Server 虛擬機器」主題。
