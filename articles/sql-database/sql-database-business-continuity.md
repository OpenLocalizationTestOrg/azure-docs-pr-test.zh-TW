---
title: "aaaCloud 業務持續性-資料庫復原的 SQL 資料庫 |Microsoft 文件"
description: "了解 Azure SQL Database 如何支援雲端商務持續性和資料庫復原，以及如何協助維持任務關鍵性雲端應用程式持續執行。"
keywords: "business continuity,cloud business continuity,database disaster recovery,database recovery,商務持續性,雲端商務持續性,資料庫災害復原,資料庫復原"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>使用 Azure SQL Database 的商務持續性概觀

本概觀說明 Azure SQL Database 提供業務續航力和災害復原的 hello 功能。 深入了解選項、 建議和教學課程，從干擾性事件可能會導致資料遺失，或造成無法使用您資料庫和應用程式 toobecome 進行復原。 使用者或應用程式的錯誤會影響資料完整性、 Azure 地區已中斷，或您的應用程式需要維護時，了解哪些 toodo。

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>SQL Database 功能，您可以使用 tooprovide 業務續航力

SQL Database 提供幾種商務持續性功能，包括自動備份和選用的資料庫複寫。 每個功能對於預估的復原時間 (ERT) 都有不同的特性，最近的交易都有可能遺失資料。 一旦您了解這些選項，就可以在其中選擇，而在大部分情況下，可以針對不同情況一起搭配使用。 當您開發業務續航力計劃，您需要 toounderstand hello 最大可接受的時間之前之後 hello 干擾性事件完全復原 hello 應用程式-這是您的復原時間目標 (RTO)。 您也需要 toounderstand hello 最大數量最新資料更新 （時間間隔） hello 應用程式可以容忍遺失時復原 hello 干擾性事件之後-這是您的復原點目標 (RPO)。

下列資料表比較 hello hello hello 三個最常見的案例 ERT 和 RPO。

| 功能 | 基本層 | 標準層 | 高階層 |
| --- | --- | --- | --- |
| 從備份進行時間點還原 |7 天內的任何還原點 |35 天內的任何還原點 |35 天內的任何還原點 |
| 從異地複寫備份進行異地還原 |ERT < 12 小時，RPO < 1 小時 |ERT < 12 小時，RPO < 1 小時 |ERT < 12 小時，RPO < 1 小時 |
| 從 Azure 備份保存庫還原 |ERT < 12 小時，RPO < 1 週 |ERT < 12 小時，RPO < 1 週 |ERT < 12 小時，RPO < 1 週 |
| 主動式異地複寫 |ERT < 30 秒，RPO < 5 秒 |ERT < 30 秒，RPO < 5 秒 |ERT < 30 秒，RPO < 5 秒 |

### <a name="use-database-backups-toorecover-a-database"></a>使用資料庫備份 toorecover 資料庫

SQL Database 會自動執行完整資料庫備份的組合每週、 每小時、 差異資料庫備份和交易記錄備份每隔五-十分鐘後 tooprotect 您免於資料遺失的業務。 這些備份會儲存 35 天 hello Standard 和 Premium 服務層中的資料庫則為 7 天 hello 基本服務層中的資料庫地理備援儲存體中。 如需詳細資訊，請參閱[服務層](sql-database-service-tiers.md)。 如果您的服務層的 hello 保留期限不符合您的業務需求，您可以保留期限，hello 由[變更 hello 服務層](sql-database-service-tiers.md)。 hello 完整和差異資料庫備份也是複寫的 tooa[成對的資料中心](../best-practices-availability-paired-regions.md)防止資料中心完全停止運作。 如需詳細資訊，請參閱[自動資料庫備份](sql-database-automated-backups.md)。

如果 hello 內建的保留期限是不夠的您的應用程式，您可以藉由設定資料庫長期保留原則來進行擴充。 如需詳細資訊，請參閱[長期保留](sql-database-long-term-retention.md)。

您可以使用這些自動資料庫備份 toorecover 各種干擾性事件，同時您資料中心和 tooanother 資料中心內的資料庫。 使用自動資料庫備份，hello 預估復原時間取決於數個因素，包括資料庫的復原 hello 相同的 hello 總數在 hello 相同的時間、 hello 資料庫大小、 hello 交易記錄大小和網路頻寬的區域。 hello 復原時間通常是不超過 12 小時。 復原時 tooanother 資料區域，hello 潛在資料遺失會是每小時的差異資料庫備份 hello 地理備援儲存體的有限的 too1 小時。

> [!IMPORTANT]
> toorecover 使用自動化備份，您必須是 hello SQL Server 參與者角色或 hello 訂用帳戶擁有者的成員-請參閱[RBAC： 內建角色](../active-directory/role-based-access-built-in-roles.md)。 您可以使用 hello Azure 入口網站、 PowerShell 或 REST API hello 進行復原。 您無法使用 Transact-SQL。
>

如果您的應用程式有下列狀況，可以使用自動備份做為您的商務持續性和復原機制︰

* 非關鍵性應用程式。
* 沒有繫結 SLA - 停機 24 小時或更長的時間不會衍生財務責任。
* 具有較低的資料變更 （每小時低交易） 率，並遺失 tooan 向上一小時的變更是可接受資料遺失。
* 成本有限。

如果您需要更快速的復原，請使用[主動式異地複寫](sql-database-geo-replication-overview.md) (會接著討論)。 如果您需要超過 35 天期間的 toobe 無法 toorecover 資料時，使用[長期備份的保留](sql-database-long-term-retention.md)。 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>使用作用中地理複寫 」 和 「 自動容錯移轉群組 （預覽版） tooreduce 復原時間與限制資料遺失相關聯的 recovery

此外 toousing 資料庫備份的資料庫復原業務中斷發生時，您可以使用[作用中地理複寫](sql-database-geo-replication-overview.md)tooconfigure 向上 toofour 可讀取次要區域中的資料庫 hello 資料庫 toohave 的程式選擇。 這些次要資料庫會保持與 hello 使用非同步複寫機制的主要資料庫同步。 這項功能是使用的 tooprotect 針對業務中斷發生資料中心中斷或應用程式在升級期間。 作用中地理複寫，也可以是唯讀查詢 toogeographically 分散的使用者使用的 tooprovide 提高查詢效能。

tooenable 自動化和透明容錯移轉，您應該組織到您進行地理複寫的資料庫群組使用 hello[自動容錯移轉群組](sql-database-geo-replication-overview.md)SQL Database （預覽） 功能。

如果 hello 主要資料庫會意外地離線或需要 tootake 離線維護活動，您可以快速升級次要 toobecome hello 主要 （也稱為 「 容錯移轉 」） 並設定應用程式 tooconnect toohello 升級主要。 如果您的應用程式連接 toohello 資料庫使用 hello 容錯移轉群組接聽程式，您不需要 toochange hello SQL 連接字串組態容錯移轉之後。 使用計劃性容錯移轉時，不會有任何資料遺失。 與未規劃的容錯移轉，可能會有一些少量到期 toohello 本質的非同步複寫的最新交易遺失資料。 使用自動容錯移轉群組 （預覽），您可以自訂 hello 容錯移轉原則 toominimize hello 潛在資料遺失。 容錯移轉之後，您可以稍後的容錯回復-相應 tooa 計劃或當 hello 資料中心再次上線。 在所有情況下，使用者體驗更少的停機時間，而且需要 tooreconnect。

> [!IMPORTANT]
> toouse 作用中地理複寫和自動容錯移轉群組 （預覽），您必須是 hello 訂用帳戶擁有者或 SQL Server 中具有系統管理權限。 您可以設定和容錯移轉使用 hello Azure 入口網站、 PowerShell 或 hello REST API 使用 Azure 訂用帳戶的權限，或使用 SQL Server 權限的 Transact SQL。
> 

如果您的應用程式符合下列任何準則，請使用主動式異地複寫和自動容錯移轉群組 (預覽版)：

* 是關鍵性應用程式。
* 具有服務等級協定 (SLA)，不允許 24 小時以上的停機時間。
* 停機可能會衍生財務責任。
* 具有很高的資料變更率，而且不接受遺失一個小時的資料。
* hello 額外的作用中地理複寫的成本低於 hello 潛在的財務損害賠償責任和關聯的商務遺失。

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>在使用者或應用程式錯誤之後復原資料庫
* 沒有人是完美的！ 使用者可能會不小心刪除某些資料、不小心卸除重要的資料表，或甚至是卸除整個資料庫。 或者，應用程式可能會不小心覆寫良好的資料不正確的資料，因為 tooan 應用程式的缺失。

在此案例中，以下是您的復原選項。

### <a name="perform-a-point-in-time-restore"></a>執行還原時間點
假設時間為 hello 資料庫的保留期限內，您可以使用 hello 自動化備份 toorecover 已知的恰當起點的時間，您資料庫 tooa 的複本。 Hello 資料庫還原後，您可以取代 hello 還原資料庫中的 hello 原始資料庫或 hello 還原資料所需的 hello 資料複製到 hello 原始資料庫。 如果 hello 資料庫使用作用中地理複寫，我們建議所需的 hello 資料複製到 hello 原始資料庫的 hello 還原複本。 如果您取代 hello 原始資料庫與 hello 還原資料庫時，您會需要 tooreconfigure，並重新同步處理作用中的地理複寫 （這可能要花費一段時間，大型資料庫）。

如需詳細資訊和詳細步驟，還原時間，使用 database tooa 點 hello Azure 入口網站，或使用 PowerShell，請參閱[時間點還原](sql-database-recovery-using-backups.md#point-in-time-restore)。 您無法使用 Transact-SQL 進行復原。

### <a name="restore-a-deleted-database"></a>還原已刪除的資料庫
如果 hello 資料庫已刪除，但尚未刪除 hello 邏輯伺服器，您可以還原刪除的 hello database toohello 點的已刪除。 這會還原資料庫備份的 toohello 邏輯已刪除的相同 SQL server。 您可以還原使用 hello 原始名稱，或提供新的名稱或 hello 還原資料庫。

如需詳細資訊以及詳細的步驟來還原已刪除的資料庫使用 hello Azure 入口網站或使用 PowerShell，請參閱[還原已刪除的資料庫](sql-database-recovery-using-backups.md#deleted-database-restore)。 您無法使用 Transact-SQL 進行還原。

> [!IMPORTANT]
> 如果刪除 hello 邏輯伺服器，就無法復原已刪除的資料庫。
>
>

### <a name="restore-from-azure-backup-vault"></a>從 Azure 備份保存庫還原
如果 hello 資料遺失的自動備份 hello 目前保留期間外，而設定供長期保存您的資料庫，您可以從 Azure 備份保存庫 tooa 新資料庫中的每週備份進行還原。 此時，您可以取代 hello 還原資料庫中的 hello 原始資料庫，或 hello 還原資料庫所需的 hello 資料複製到 hello 原始資料庫。 如果您需要 tooretrieve 較舊版本的資料庫先前 tooa 主要的應用程式升級時，滿足要求，以從稽核員或合法的順序，您可以建立使用儲存在 hello Azure 備份保存庫的完整備份的資料庫。  如需詳細資訊，請參閱[長期保存](sql-database-long-term-retention.md)。

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>從 Azure 地區資料中心中斷復原資料庫 tooanother 區域
<!-- Explain this scenario -->

雖然很罕見，但 Azure 資料中心也可能會有中斷的時候。 發生中斷時，可能只會讓業務中斷幾分鐘，也可能會持續幾小時。

* 其中一個選項是針對上線的資料庫 toocome toowait 上方 hello 資料中心完全停止運作時。 這適用於應用程式可以容忍 toohave hello 資料庫離線。 例如，開發專案或免費試用您不需要 toowork 上持續。 當資料中心中斷時，您不知道 hello 中斷可能時間長短，因此如果您不需要一段時間的資料庫，僅適用於此選項。
* 如果您使用的作用中地理複寫或 hello 復原資料庫，使用異地備援資料庫備份 （「 地理還原），另一個選項的是 tooeither 失敗 tooanother 資料區域。 容錯移轉只需要幾秒鐘的時間，而從備份復原資料庫則需要幾個小時。

當您採取動作時，要花多久您 toorecover，以及多少資料遺失，您會產生取決於您決定如何將 toouse 這些應用程式中的業務續航力功能。 事實上，您可以選擇 toouse 資料庫備份和應用程式的需求而定作用中地理複寫的組合。 若要探討使用這些商務持續性功能針對獨立資料庫和彈性集區進行應用程式設計時的考量，請參閱[設計雲端災害復原應用程式](sql-database-designing-cloud-solutions-for-disaster-recovery.md)和[彈性集區災害復原策略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)。

hello 下列各節提供使用資料庫備份或作用中地理複寫的 hello 步驟 toorecover 的概觀。 如需詳細步驟，包括規劃需求、 post 修復步驟和如何 toosimulate 中斷 tooperform 災害復原切入的相關資訊，請參閱[從中斷復原 SQL 資料庫](sql-database-disaster-recovery.md)。

### <a name="prepare-for-an-outage"></a>準備中斷
不論您使用 hello 業務續航力功能，您必須：

* 識別並準備 hello 目標伺服器，包括伺服器層級防火牆規則、 登入，以及 master 資料庫層級權限。
* 判斷如何 tooredirect 用戶端和用戶端應用程式 toohello 新伺服器
* 記錄其他相依性，例如稽核設定和警示

如果您沒有適當地準備，在容錯移轉或資料庫復原後讓應用程式上線將會多花費時間，而且也可能需要在有壓力的情況下進行疑難排解 - 這是不良的情況組合。

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>容錯移轉 tooa 異地備援的次要資料庫
若您使用作用中異地複寫和自動容錯移轉群組 (預覽版) 作為復原機制，則可設定自動容錯移轉原則或使用[手動容錯移轉](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database)。 一旦起始，hello 容錯移轉原因 hello 次要 toobecome hello 新的主要和準備 toorecord 新交易，以及回應 tooqueries-hello 尚未複寫的資料遺失最少的資料。 如需設計 hello 容錯移轉程序資訊，請參閱[設計的應用程式的雲端災害復原](sql-database-designing-cloud-solutions-for-disaster-recovery.md)。

> [!NOTE]
> Hello 資料中心再次上線時 hello 舊主要複本會自動重新連線 toohello 新主要複本，並會變成次要資料庫。 如果您需要 toorelocate hello 主要後 toohello 原始區域，您可以手動起始已規劃的容錯移轉 （回復）。 
> 

### <a name="perform-a-geo-restore"></a>執行異地還原
如果您使用自動備份搭配異地備援儲存體複寫作為復原機制，請[使用異地還原起始資料庫復原](sql-database-disaster-recovery.md#recover-using-geo-restore)。 復原通常會發生在 12 小時內-向上取決於當 hello tooone 小時的資料遺失的最後一個每小時的差異備份所建立和複寫。 Hello 復原完成，直到 hello 資料庫是無法 toorecord 任何交易，或是回應 tooany 查詢。 雖然這會還原資料庫 toohello 最後一個可用的點，還原時間 hello 地理次要 tooany 點目前不支援。

> [!NOTE]
> 如果您的應用程式切換 toohello 復原資料庫之前，hello 資料中心再次上線，您可以取消 hello 復原。  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>執行容錯移轉後/復原後工作
復原後的其中一種復原機制，您必須執行下列額外的工作，您的使用者和應用程式在備份之前，執行 hello:

* 重新導向用戶端與用戶端應用程式 toohello 新伺服器還原的資料庫
* 請確定適當的伺服器層級防火牆規則中進行使用者 tooconnect (或使用[資料庫層級防火牆](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* 確定有適當的登入和 master 資料庫層級權限 (或使用 [自主的使用者](https://msdn.microsoft.com/library/ff929188.aspx))
* 依適當情況設定稽核
* 依適當情況設定警示

## <a name="upgrade-an-application-with-minimal-downtime"></a>在最少停機時間的情況下升級應用程式
有時，應用程式會因為計劃性維護 (例如應用程式升級) 而必須離線。 [管理應用程式的升級](sql-database-manage-application-rolling-upgrade.md)描述如何 toouse 作用中地理複寫 tooenable 輪流升級期間將雲端應用程式 toominimize 停機時間升級，並提供復原路徑，如果發生錯誤。 

## <a name="next-steps"></a>後續步驟
如需獨立資料庫和彈性集區的應用程式設計考量探討，請參閱[設計雲端災害復原應用程式](sql-database-designing-cloud-solutions-for-disaster-recovery.md)和[彈性集區災害復原策略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)。
