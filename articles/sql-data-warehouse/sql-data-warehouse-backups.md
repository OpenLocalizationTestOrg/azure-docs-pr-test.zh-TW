---
title: "aaaAzure SQL 資料倉儲備份快照，異地備援 |Microsoft 文件"
description: "了解 SQL 資料倉儲內建的資料庫備份可讓您 toorestore Azure SQL 資料倉儲 tooa 還原點不同的地理區域。"
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a>SQL 資料倉儲備份
SQL 資料倉儲備份提供本機和異地備份做為其資料倉儲備份功能的一部份。 這些包括 Azure 儲存體 Blob 快照集和異地備援儲存體。 使用資料倉儲備份 toorestore 資料倉儲 tooa 還原點在 hello 主要區域中，或還原 tooa 不同的地理區域。 本文說明 hello 細節 SQL 資料倉儲中的備份。

## <a name="what-is-a-data-warehouse-backup"></a>什麼是資料倉儲備份？
在資料倉儲備份，hello 資料，您可以使用 toorestore 資料倉儲 tooa 特定時間。  由於 SQL 資料倉儲是一個分散式系統，所以一個資料倉儲備份是由儲存在 Azure Blob 中的許多檔案組成。 

資料庫備份可保護資料免於意外損毀或刪除，是商務持續性和災害復原策略中不可或缺的一部分。 如需詳細資訊，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)。

## <a name="data-redundancy"></a>資料備援
SQL 資料倉儲會透過將您的資料儲存在本地備援 (LRS) Azure 進階儲存體來保護您的資料。 此 Azure 儲存體功能會將多份同步 hello 資料儲存在 hello 本機資料中心 tooguarantee 透明資料保護中，如果當地語系化的失敗。 資料備援可確保您的資料在發生基礎結構問題 (例如磁碟故障等) 時能夠存留。 資料備援可利用容錯和高可用性基礎結構來確保商務持續性。

toolearn 程式的詳細資訊：

* Azure 高階儲存體，請參閱[簡介 tooAzure 高階儲存體](../storage/common/storage-premium-storage.md)。
* 本地備援儲存體，請參閱 [Azure 儲存體複寫](../storage/common/storage-redundancy.md#locally-redundant-storage)。

## <a name="azure-storage-blob-snapshots"></a>Azure 儲存體 Blob 快照集
使用 Azure 高階儲存體的優點，作為 SQL 資料倉儲會在本機使用 Azure 儲存體 Blob 快照集 toobackup hello 資料倉儲。 您可以還原資料倉儲 tooa 快照集還原點。 快照集至少每八個小時會啟動，並且可供使用七天。  

toolearn 程式的詳細資訊：

* Azure Blob 快照集，請參閱[建立 Blob 快照集](../storage/blobs/storage-blob-snapshots.md)。

## <a name="geo-redundant-backups"></a>異地備援備份
每 24 小時，SQL 資料倉儲儲存在標準儲存體中的 hello 完整的資料倉儲。 hello 完整的資料倉儲建立 toomatch hello hello 最後一個快照集。 hello 標準儲存體所屬 tooa 地理備援儲存體帳戶，具有讀取存取權 (RA-GRS)。 hello Azure 儲存體 RA-GRS 功能複寫 hello 備份檔案 tooa[成對的資料中心](../best-practices-availability-paired-regions.md)。 此地理複寫可確保萬一您無法存取主要區域中的 hello 快照集，您可以還原資料倉儲。 

這項功能為預設開啟。 如果您不想 toouse 異地備援備份，您也可以 [退出] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn)。 

> [!NOTE]
> 在 Azure 儲存體，hello 詞彙*複寫*參考從一個位置 tooanother toocopying 檔案。 SQL 的*資料庫複寫*參考 tookeeping toomultiple 次要資料庫與主要資料庫同步處理。 
> 
> 

> [!NOTE]
> 您無法選擇退出 DWU 9000 和 DWU 18000 的異地備援備份。 
>
> 

toolearn 程式的詳細資訊：

* 異地備援儲存體，請參閱 [Azure 儲存體複寫](../storage/common/storage-redundancy.md)。
* RA-GRS 儲存體：請參閱 [讀取權限異地備援儲存體](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)。

## <a name="data-warehouse-backup-schedule-and-retention-period"></a>資料倉儲備份排程與保留期限
SQL 資料倉儲線上資料倉儲上建立快照集，每隔四種 tooeight 小時和每一個快照集七天的保留。 您可以還原您的線上資料庫 tooone hello 還原點 hello 在過去七天內。 

toosee hello 最後一個快照集啟動時，您的線上 SQL 資料倉儲上執行此查詢。 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

如果您需要 tooretain 快照集的時間超過七天，您可以還原還原點 tooa 新的資料倉儲。 Hello 還原完成之後，SQL 資料倉儲會啟動 hello 新的資料倉儲上建立快照集。 如果您不要進行變更 toohello 新的資料倉儲，hello 快照集保持空白，因此 hello 快照成本最少。 您也可以暫停 hello 資料庫 tookeep SQL 資料倉儲無法建立快照集。

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a>發生什麼事 toomy 備份保留我的資料倉儲暫停時？
暫停資料倉儲時，SQL 資料倉儲不會建立快照集，快照集也不會過期。 暫停 hello 資料倉儲時，不會變更 hello 快照集存在時間。 快照集保留根據 hello 資料倉儲已上線，不是行事曆日期的 hello 天數。

例如，如果快照集啟動月 1 日下午 4 點，且 hello 資料倉儲在下午 4 點暫停年 10 月 3 hello 快照就是兩天。 每當 hello 資料倉儲上線 hello 快照集是兩天。 如果 hello 資料倉儲上線年 10 月 5 日下午 4 點，hello 快照集就會是舊的兩天，而會保留 5 天。

Hello 資料倉儲回到線上時，SQL 資料倉儲繼續新的快照集，且他們皆已超過七天的資料過期的快照集。

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a>Hello 保留期限的已卸除的資料倉儲的時間？
資料倉儲放置時，會儲存七天 hello 資料倉儲和 hello 快照集，然後移除。 您可以還原 hello 資料倉儲 tooany hello 儲存還原點。

> [!IMPORTANT]
> 如果您刪除邏輯的 SQL server 執行個體，也會一併刪除屬於 toohello 執行個體的所有資料庫，且無法復原。 您無法還原已刪除的伺服器。
> 
> 

## <a name="data-warehouse-backup-costs"></a>資料倉儲備份成本
hello 總成本的您的主要資料倉儲和七天的 Azure Blob 快照集是圓角的 toohello 最接近的 TB。 例如，如果您的資料倉儲是 1.5 TB hello 快照使用 100 GB，您所要支付 2 TB 的資料至 Azure 高階儲存體費率。 

> [!NOTE]
> 每個快照集是空的一開始，而且會隨著您進行變更 toohello 主要資料倉儲。 所有快照集的大小增加為 hello 資料倉儲的變更。 因此，快照集的 hello 儲存體成本成長變動的相應 toohello 率。
> 
> 

如果您正在使用異地備援儲存體，您會收到個別的儲存體收費項目。 hello 地理備援儲存體是費率支付費用 hello 標準讀取權限地理備援儲存體 (RA-GRS)。

如需 SQL 資料倉儲價格的相關詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。

## <a name="using-database-backups"></a>使用資料庫備份
hello 的 SQL 資料倉儲備份的主要用途是 toorestore hello 資料倉儲 tooone hello 還原點 hello 保留期限內。  

* toorestore SQL 資料倉儲，請參閱[還原 SQL 資料倉儲](sql-data-warehouse-restore-database-overview.md)。

## <a name="related-topics"></a>相關主題
### <a name="scenarios"></a>案例
* 如需商務持續性概觀，請參閱[商務持續性概觀](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

* toorestore 資料倉儲，請參閱[還原 SQL 資料倉儲](sql-data-warehouse-restore-database-overview.md)

<!-- ### Tutorials -->

