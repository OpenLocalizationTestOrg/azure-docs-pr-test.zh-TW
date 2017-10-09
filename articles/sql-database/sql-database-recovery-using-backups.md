---
title: "aaaRestore Azure SQL database 備份 |Microsoft 文件"
description: "深入了解，可讓您 tooroll 後的時間點還原 Azure SQL Database tooa 前一個點的時間 （向上 too35 天為單位）。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>使用自動資料庫備份復原 Azure SQL Database
SQL Database 針對使用[自動資料庫備份](sql-database-automated-backups.md)和[長期保留備份](sql-database-long-term-retention.md)進行資料庫復原，提供以下選項。 您可從資料庫備份還原至︰

* 新的資料庫上相同的邏輯伺服器復原的 hello tooa 指定 hello 保留期限內的時間點。 
* A 上的資料庫 hello 相同邏輯伺服器復原已刪除的資料庫的 toohello 刪除時間。
* 新的資料庫中的任何區域的任何邏輯伺服器上復原 toohello 點 hello 的最新每日備份在異地備援 blob 儲存體 (RA-GRS)。

> [!IMPORTANT]
> 在還原期間，您無法覆寫現有的資料庫。
>

您也可以使用[自動化資料庫備份](sql-database-automated-backups.md)toocreate[資料庫複製](sql-database-copy.md)的任何區域中的任何邏輯伺服器上。 

## <a name="recovery-time"></a>復原時間
hello 復原時間 toorestore 使用自動化的資料庫備份的資料庫由數個因素影響： 

* hello hello 資料庫大小
* hello hello 資料庫效能層級
* 交易記錄所涉及的 hello 數目
* hello 數量需要 toobe 活動重新執行 toorecover toohello 還原點
* hello 網路頻寬 hello 還原 tooa 不同的區域 
* hello hello 目標區域中所處理的並行的還原要求數目。 
  
  對於非常大型和/或作用中的資料庫，hello 還原可能需要數小時。 如果某區域中的中斷延長，其他區域可能要處理大量的異地還原要求。 當有許多要求時，hello 復原時間可能會增加該區域中的資料庫。 大多數資料庫還原會在 12 小時內完成。
  
沒有任何內建功能 toodo 大量還原。 hello [Azure SQL Database： 完整伺服器復原](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666)指令碼是一種完成這項工作的範例。

> [!IMPORTANT]
> toorecover 使用自動化備份，您必須是 hello hello 訂用帳戶中的 SQL Server 參與者角色的成員，或者是 hello 訂用帳戶擁有者。 您可以使用 hello Azure 入口網站、 PowerShell 或 REST API hello 進行復原。 您無法使用 Transact-SQL。 
> 

## <a name="point-in-time-restore"></a>還原時間點

您可以還原現有的資料庫 tooan 稍早的時間點為新的資料庫上 hello 相同邏輯伺服器使用 hello Azure 入口網站[PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase)，或使用 hello [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx)。 

> [!TIP]
> 顯示如何 tooperform 時間點還原的資料庫，請參閱範例 PowerShell 指令碼[還原 SQL 資料庫使用 PowerShell](scripts/sql-database-restore-database-powershell.md)。
>

hello 資料庫可以在還原的 tooany 服務層或效能層級，以及做為單一資料庫或彈性集區。 請確定 hello 邏輯伺服器上有足夠的資源，或在 hello 彈性集區 toowhich hello 資料庫會還原。 完成後，hello 還原資料庫是正常、 完全可存取的線上資料庫。 根據其服務層和效能層級的標準費率計費 hello 還原資料庫。 Hello 資料庫還原完成之前不會產生費用。

您通常會還原資料庫 tooan 稍早點進行復原。 時這麼做，您可以將 hello 做為 hello 原始資料庫的替代還原資料庫，或使用它從 tooretrieve 資料並更新 hello 原始資料庫。 

* ***資料庫取代：***如果 hello 還原資料庫用來取代 hello 原始資料庫，您應該確認 hello 效能層級和 （或) 是適當的服務層，並視 hello 資料庫的延展。 您可以重新命名 hello 原始資料庫，然後將 hello 還原資料庫 hello 原始名稱使用 T-SQL 中的 hello ALTER DATABASE 命令。 
* ***資料復原：***如果您計劃 tooretrieve hello 還原資料庫 toorecover 從使用者或應用程式錯誤的資料，您需要 toowrite 並從 hello 還原資料庫 toohello 執行 hello 必要的資料復原指令碼 tooextract 資料原始的資料庫。 雖然 hello 還原作業可能要花很長的時間 toocomplete，hello 還原資料庫中會顯示 hello 整個 hello 還原程序的資料庫清單。 如果您刪除 hello 資料庫 hello 還原期間，hello 還原作業會取消，且您不需付費 hello 未完成 hello 還原的資料庫。 

### <a name="azure-portal"></a>Azure 入口網站

在時間中使用 toorecover tooa 點 hello Azure 入口網站、 資料庫和按一下開啟 hello 頁面**還原**hello 工具列上。

![point-in-time-restore](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>還原已刪除的資料庫
您可以還原已刪除的資料庫 toohello 刪除時間的 hello 上已刪除的資料庫使用相同的邏輯伺服器 hello Azure 入口網站[PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase)，或使用 hello [REST (createMode = 還原)](https://msdn.microsoft.com/library/azure/mt163685.aspx)。 

> [!TIP]
> 如需範例 PowerShell 指令碼的顯示如何 toorestore 已刪除的資料庫，請參閱[還原 SQL 資料庫使用 PowerShell](scripts/sql-database-restore-database-powershell.md)。
>

> [!IMPORTANT]
> 如果您刪除 Azure SQL Database 伺服器執行個體，其所有資料庫也會一併刪除且無法加以復原。 目前不支援還原已刪除的伺服器。
> 

### <a name="azure-portal"></a>Azure 入口網站

已刪除的 toorecover 資料庫期間其[保留期限](sql-database-service-tiers.md)使用 hello Azure 入口網站開啟 hello 頁面為您的伺服器，並在 hello 作業區域中，按一下 **已刪除資料庫**。

![deleted-database-restore-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![deleted-database-restore-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>異地還原
您可以從 hello 最新地理複寫完整和差異備份來還原 SQL 資料庫的任何 Azure 區域中的任何伺服器上。 「 地理還原使用異地備援備份做為來源，而且可以是使用的 toorecover 即使 hello 資料庫或資料中心無法存取到期 tooan 中斷。 

地理還原 」 hello 預設復原選項，您無法使用資料庫時由於 hello hello 資料庫裝載的區域中的事件。 如果資料庫應用程式中無法使用區域結果中的大規模事件，您可以從任何其他區域中的 hello 異地備援備份 tooa 伺服器來還原資料庫。 當執行差異備份時，與時進行地理複寫 tooan Azure 之間的延遲不同區域中的 blob。 此類延遲可能會向上 tooan 小時，因此，如果發生損毀，有最長可能會 tooone 小時資料遺失。 hello 下列圖例顯示 hello 最新可用的備份在另一個地區 hello 資料庫的還原。

![異地還原](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> 如需範例 PowerShell 指令碼的顯示如何 tooperform 異地還原，請參閱[還原 SQL 資料庫使用 PowerShell](scripts/sql-database-restore-database-powershell.md)。
> 

目前不支援異地次要資料庫上的時間點復原。 只有在主要資料庫上才可進行時間點復原。 如需使用 「 地理還原 toorecover 從中斷的詳細資訊，請參閱[從中斷復原](sql-database-disaster-recovery.md)。

> [!IMPORTANT]
> 從備份復原為 hello 最基本的 hello 災害復原方案中使用 SQL Database 提供 hello 最長的 RPO 和預估復原時間 (ERT)。 對於使用基本資料庫的解決方案，常見且合理的 DR 解決方案是異地還原，且這個解決方案具有 12 小時的 ERT。 對於使用較大型標準或進階資料庫的解決方案，如果其需要縮短復原時間，您應該考慮使用[主動式異地複寫](sql-database-geo-replication-overview.md)。 作用中地理複寫會提供以較低的 RPO 和 ERT 程式它只會要求您起始容錯移轉 tooa 連續複寫的次要資料庫。 如需商務持續性選項的詳細資訊，請參閱[商務持續性概觀](sql-database-business-continuity.md)。
> 

### <a name="azure-portal"></a>Azure 入口網站

toogeo 還原資料庫時其[保留期限](sql-database-service-tiers.md)使用 hello Azure 入口網站，開啟 hello SQL Database 頁面，然後按一下**新增**。 在 [hello**選取來源**] 文字方塊中，選取**備份**。 Hello 區域中，您所選擇的 hello 伺服器上，指定 hello tooperform hello 復原備份。 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>使用自動備份以程式設計方式執行復原
如先前所討論，此外 toohello Azure 入口網站資料庫復原可以使用 Azure PowerShell 以程式設計方式執行或是 hello REST API。 hello 下表描述可用的命令 hello 集。

### <a name="powershell"></a>PowerShell
| Cmdlet | 說明 |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |取得一或多個資料庫。 |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | 取得可還原的已刪除資料庫。 |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |取得資料庫的異地備援備份。 |
| [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |還原 SQL Database。 |
|  | |

### <a name="rest-api"></a>REST API
| API | 說明 |
| --- | --- |
| [REST (createMode=Recovery)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |還原資料庫 |
| [取得建立或更新資料庫狀態](https://msdn.microsoft.com/library/azure/mt643934.aspx) |在還原作業期間傳回 hello 狀態 |
|  | |

## <a name="summary"></a>摘要
自動備份可在發生使用者和應用程式錯誤、意外刪除資料庫和長時間中斷時保護您的資料庫。 這項內建的功能適用於所有服務層和效能層級。 

## <a name="next-steps"></a>後續步驟
* 如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)
* toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)
* toolearn 有關長期備份的保留，請參閱[長期備份的保留](sql-database-long-term-retention.md)
* tooconfigure，管理和還原的使用 hello Azure 復原服務保存庫中的自動備份的長期保存從 Azure 入口網站，請參閱[設定和使用長期備份保留](sql-database-long-term-backup-retention-configure.md)。 
* toolearn 有關更快速的復原選項，請參閱[作用中地理複寫](sql-database-geo-replication-overview.md)  
