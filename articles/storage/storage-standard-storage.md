---
title: "aaaHD 基礎符合成本效益標準儲存體和 Azure VM 磁碟 |Microsoft 文件"
description: "討論符合成本效益的標準儲存體及非受控和受控 VM 磁碟。"
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c454c61254c6b160bdf2cd39ea3319452e3e4898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>符合成本效益的標準儲存體及非受控和受控 Azure VM 磁碟

如果 VM 執行的工作負載不在乎延遲，Azure 標準儲存體可以提供可靠、低成本的磁碟支援。 它也支援 blob、資料表、佇列和檔案。 使用標準儲存體，hello 資料會儲存在硬碟機 (Hdd)。 使用 VM 時，您可以對開發/測試案例和較不重要的工作負載使用標準儲存體磁碟，而對關鍵任務的實際執行應用程式使用進階儲存體磁碟。 所有 Azure 區域中都可以使用標準儲存體。 

本文將著重在 hello 使用標準儲存體的 VM 磁碟。 如需 hello 使用的儲存體的 blob、 資料表、 佇列和檔案，請參閱 toohello[簡介 tooStorage](storage-introduction.md)。

## <a name="disk-types"></a>磁碟類型

有兩種方式 toocreate 標準 Azure Vm 磁碟：

**Unmanaged 磁碟**： 這是您用來管理 hello 儲存體帳戶使用 toostore hello VHD 檔案對應 toohello VM 磁碟 hello 原始方法。 VHD 檔案會以分頁 Blob 的形式儲存在儲存體帳戶中。 未受管理的磁碟可以是附加的 tooany Azure VM 大小，包括主要是使用進階儲存體，例如 hello DSv2 及 GS 系列的 hello Vm。 Azure Vm 支援附加數個標準磁碟，讓向上 too256 TB 的每個 VM 的存放空間。

[**受管理的 azure 磁碟**](storage-managed-disks-overview.md)： 這項功能會管理 hello 用於 hello VM 磁碟為您的儲存體帳戶。 您指定 hello 類型 （高階或標準） 和大小的磁碟，您需要以及 Azure 會建立，並會為您管理 hello 磁碟。 您不需要跨多個儲存體帳戶的順序 tooensure 您維持在 hello hello 儲存體帳戶的延展性限制內放置 hello 磁碟的相關 tooworry--Azure 會為您處理的。

即使這兩種類型的磁碟可用，建議使用受管理磁碟 tootake 利用其許多功能。

tooget 開始使用 Azure 標準儲存體，請瀏覽[免費開始](https://azure.microsoft.com/pricing/free-trial/)。 

如需有關如何 toocreate 擁有管理磁碟 VM，請參閱下列 hello 的其中一個詳細文章。

* [使用 Resource Manager 和 PowerShell 建立 VM](../virtual-machines/virtual-machines-windows-ps-create.md)
* [建立 Linux VM，使用 Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md)

## <a name="standard-storage-features"></a>標準儲存體功能 

讓我們看看一些 hello 的標準儲存體的功能。 如需詳細資訊，請參閱[簡介 tooAzure 儲存體](storage-introduction.md)。

**標準儲存體**：Azure 標準儲存體支援 Azure 磁碟、Azure Blob、Azure 檔案儲存體、Azure 資料表和 Azure 佇列。 toouse 標準儲存體服務，會啟動[建立 Azure 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)。

**標準儲存體磁碟：**標準儲存體磁碟可以是附加 tooall 包括使用進階儲存體，例如 hello DSv2 及 GS 系列大小系列 Vm 的 Azure Vm。 標準儲存體磁碟只能附加的 tooone VM。 不過，您可以附加一或多個這些磁碟 tooa VM，總 toohello 定義該 VM 大小的最大磁碟計數。 在 hello 遵循標準儲存體延展性和效能目標上一節，我們將說明詳細的 hello 規格。 

**標準的分頁 blob**： 標準的分頁 blob 使用的 toohold 永續性磁碟的 Vm，而且也可以存取直接透過如同其他類型的 Azure Blob 的其餘部分。 [分頁 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)是已最佳化隨機讀取和寫入作業的一組 512 位元組分頁。 

**儲存體複寫︰**在大部分區域，標準儲存體帳戶中的資料可以在本地複寫，或跨多個資料中心進行異地複寫。 可供複寫的 hello 四種可本機備援儲存體 (LRS)、 區域備援儲存體 (ZRS)、 地理備援儲存體 (GRS) 和讀取權限的地理備援儲存體 (RA-GRS)。 標準儲存體中的受控磁碟目前只支援本地備援儲存體 (LRS)。 如需詳細資訊，請參閱[儲存體複寫](storage-redundancy.md)。

## <a name="scalability-and-performance-targets"></a>擴充和效能目標

在本節中，我們將說明使用標準儲存體時，需要 tooconsider hello 延展性和效能目標。

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>帳戶限制 – 不會套用 toomanaged 磁碟

| **Resource** | **預設限制** |
|--------------|-------------------|
| 每一儲存體帳戶的 TB  | 500 TB |
| 每一儲存體帳戶的輸入上限<sup>1</sup> (美國地區) | 如果啟用 GRS/ZRS，則為 10 Gbps，LRS 為 20 Gbps |
| 每一儲存體帳戶的輸出上限<sup>1</sup> (美國地區) | 如果啟用 RA-GRS/GRS/ZRS，則為 20 Gbps，LRS 為 30 Gbps |
| 每一儲存體帳戶的輸入上限<sup>1</sup> (歐洲和亞洲地區) | 如果啟用 GRS/ZRS，則為 5 Gbps，LRS 為 10 Gbps |
| 每一儲存體帳戶的輸出上限<sup>1</sup> (歐洲和亞洲地區) | 如果啟用 RA-GRS/GRS/ZRS，則為 10 Gbps，LRS 為 15 Gbps |
| 每一儲存體帳戶的總要求率 (假設 1KB 物件大小) | Too20、 000 IOPS、 每秒的實體或每秒的訊息 |

<sup>1</sup>輸入指的是正在傳送 tooa 儲存體帳戶的 tooall 資料 （要求）。 輸出是指從儲存體帳戶接收的 tooall 資料 （回應）。

如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。

如果 hello 應用程式需要超過 hello 延展性目標的單一儲存體帳戶，請建置應用程式 toouse 多個儲存體帳戶，這些儲存體帳戶間分割您的資料。 或者，您可以 Azure 受管理磁碟及 Azure 將會管理 hello 資料分割和為您的資料放置。

### <a name="standard-disks-limits"></a>標準磁碟限制

這與 Premium 磁碟 hello 輸入/輸出作業數 (iops) 和輸送量 （頻寬） 的標準磁碟不會佈建。 hello 標準磁碟的效能會隨著 hello VM 大小 toowhich hello 磁碟連接時，不 toohello 的 hello 磁碟的大小。 您可以預期 tooachieve 向上 toohello hello 表中所列的效能限制。

**標準磁碟限制 (受控和非受控)**

| **VM 層**            | **基本層 VM** | **標準層 VM** |
|------------------------|-------------------|----------------------|
| 最大磁碟大小          | 4095 GB           | 4095 GB              |
| 每一磁碟的 IOPS 上限為 8 KB | 向上 too300         | 向上 too500            |
| 每一磁碟的最大頻寬 (MB/秒) | 向上 too60 MB/s     | 向上 too60 MB/s        |

如果您的工作負載需要高效能、低延遲磁碟支援，您應該考慮使用進階儲存體。 tooknow 更多優點高階儲存體，請瀏覽[高效能高階儲存體和 Azure VM 磁碟](storage-premium-storage.md)。 

## <a name="snapshots-and-copy-blob"></a>快照集和複製 Blob

toohello 儲存體服務，hello VHD 檔案是分頁 blob。 您可以使用分頁 blob 的快照集，並將它們複製 tooanother 位置，例如不同的儲存體帳戶。

### <a name="unmanaged-disks"></a>非受控磁碟

您可以建立[增量快照](storage-incremental-snapshots.md)的未受管理的標準磁碟區在 hello 相同標準儲存體中使用快照集的方式。 我們建議您建立快照集，然後將這些快照集 tooa 異地備援的標準儲存體帳戶複製，如果您的來源磁碟是本機備援儲存體帳戶中。 如需詳細資訊，請參閱 [Azure 儲存體備援選項](storage-redundancy.md)。

如果磁碟已附加的 tooa VM，某些應用程式開發介面作業不允許在 hello 磁碟上。 例如，您無法執行[複製 Blob](/rest/api/storageservices/Copy-Blob)只要 hello 磁碟是該 blob 上的作業附加 tooa VM。 相反地，使用 hello 第一次建立 blob 的快照集[快照集 Blob](/rest/api/storageservices/Snapshot-Blob) REST API 方法，然後再執行 hello[複製 Blob](/rest/api/storageservices/Copy-Blob) hello 快照 toocopy hello 的附加磁碟。 或者，您可以卸離 hello 磁碟，然後再執行任何必要的作業。

toomaintain 異地備援您快照集副本，您可以複製快照集從本機備援儲存體帳戶 tooa 異地備援的標準儲存體帳戶使用 AzCopy 或複製 Blob。 如需詳細資訊，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)和[複製 Blob](/rest/api/storageservices/Copy-Blob)。

如需對標準儲存體帳戶中的分頁 Blob 執行 REST 作業的詳細資訊，請參閱 [Azure 儲存體服務 REST API](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference)。

### <a name="managed-disks"></a>受控磁碟

受管理磁碟的快照集是以標準的受管理磁碟的形式儲存 hello 受管理磁碟的唯讀副本。 增量快照目前不支援針對受管理的磁碟，但將在未來的 hello 支援。

如果受管理的磁碟附加的 tooa VM，某些應用程式開發介面作業不允許在 hello 磁碟上。 比方說，您無法在附加的 tooa VM hello 磁碟時，產生共用的存取簽章 (SAS) tooperform 複製作業。 相反地，第一次建立 hello 磁碟的快照集，然後再執行 hello hello 快照集副本。 或者，您可以卸離 hello 磁碟，並接著產生共用的存取簽章 (SAS) tooperform hello 複製作業。

## <a name="pricing-and-billing"></a>價格和計費

當使用標準儲存體，hello 計費適用下列考量：

* 標準儲存體非受控磁碟/資料大小 
* 標準受控磁碟
* 標準儲存體快照集
* 輸出資料傳輸
* 交易

**Unmanaged 儲存資料和磁碟大小：**未受管理的磁碟及其他資料 （blob、 資料表、 佇列和檔案），則需收費僅 hello 您使用的空間數量。 例如，如果您有的 VM，其分頁 blob 佈建為 127 GB，但是 hello VM 其實只能使用 10 GB 的空間，您將支付 10 GB 的空間。 我們支援向上 too8191 GB，標準儲存體和標準 unmanaged 的磁碟，向上 too4095 GB。 

**管理磁碟：**受管理磁碟會依 hello 佈建大小計費。 如果您的磁碟已佈建為 10 GB 的磁碟，而且您只使用 5 GB，您將仍然支付 hello 佈建大小為 10 GB。

**快照集**: hello hello 快照集所使用的額外容量付費的標準磁碟的快照集。 如需有關快照的資訊，請參閱[建立 Blob 的快照](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)。

**輸出資料傳輸**： [輸出資料傳輸](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure 資料中心送出的資料) 會產生頻寬使用量費用。

**交易**：在標準儲存體上，Azure 每 100000 筆交易會收取 $0.0036。 交易包含這兩個讀取和寫入作業 toostorage。

如需標準儲存體、虛擬機器和受控磁碟價格的詳細資訊，請參閱：

* [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)
* [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [受控磁碟價格](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Azure 備份服務支援 

您可以使用 Azure 備份來備份具有非受控磁碟的虛擬機器。 [其他詳細資訊](../backup/backup-azure-vms-first-look-arm.md)。

您也可以使用與管理磁碟 toocreate 備份作業的 hello Azure 備份服務時間為基礎的備份、 VM 還原與備份保留原則。 如需深入了解，請參閱[針對具有受控磁碟的 VM 使用 Azure 備份服務](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)。

## <a name="next-steps"></a>後續步驟

* [簡介 tooAzure 儲存體](storage-introduction.md)

* [建立儲存體帳戶](storage-create-storage-account.md)

* [受控磁碟概觀](storage-managed-disks-overview.md)

* [使用 Resource Manager 和 PowerShell 建立 VM](../virtual-machines/virtual-machines-windows-ps-create.md)

* [建立 Linux VM，使用 Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md)
