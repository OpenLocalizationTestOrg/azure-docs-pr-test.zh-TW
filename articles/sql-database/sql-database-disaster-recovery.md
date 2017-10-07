---
title: "aaaSQL Database 災害復原 |Microsoft 文件"
description: "了解如何 toorecover 資料庫地區資料中心中斷或發生錯誤 hello Azure SQL Database 作用中地理複寫及異地復原功能。"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>還原次要的 Azure SQL Database 或容錯移轉 tooa
Azure SQL Database 提供下列功能從中斷復原 hello:

* [主動式異地複寫](sql-database-geo-replication-overview.md)
* [異地還原](sql-database-recovery-using-backups.md#point-in-time-restore)

toolearn 有關業務持續性案例和 hello 功能支援這些案例中，請參閱[業務續航力](sql-database-business-continuity.md)。

### <a name="prepare-for-hello-event-of-an-outage"></a>準備中斷的 hello 事件
對於成功使用作用中地理複寫或異地備援備份復原 tooanother 資料區時，您需要 tooprepare 中另一個資料中心中斷 toobecome hello 新的主要伺服器的伺服器應該 hello 需要發生，以及具有妥善定義的步驟已歸檔，並經過測試 tooensure smooth 復原。 這些準備步驟包括︰

* 識別在另一個區域 toobecome hello 新的主要伺服器中的 hello 邏輯伺服器。 使用中的異地複寫，這會是至少一個，或許每一個 hello 次要伺服器。 地理還原，這通常是伺服器在 hello[配對的區域](../best-practices-availability-paired-regions.md)hello 資料庫所在的區域。
* 識別，並選擇性地定義，hello 伺服器層級防火牆規則，需要在使用者 tooaccess hello 新的主要資料庫。
* 決定要如何 tooredirect 使用者 toohello 新的主要伺服器，例如變更連接字串，或是變更 DNS 項目。
* 識別，並選擇性地建立，hello 登入必須存在於 hello master 資料庫 hello 新主要伺服器上，並且確定這些登入適當的權限 hello master 資料庫中，如果有的話。 如需詳細資訊，請參閱 [災害復原後的 SQL Database 安全性](sql-database-geo-replication-security-config.md)
* 識別需要 toobe 更新的 toomap toohello 新的主要資料庫的警示規則。
* Hello 目前的主要資料庫上的文件 hello 稽核設定
* 執行 [災害復原演練](sql-database-disaster-recovery-drills.md)。 toosimulate 異地還原的中斷，您可以刪除或重新命名 hello 來源資料庫 toocause 應用程式連線失敗。 toosimulate 中斷的作用中地理複寫，您可以停用 hello web 應用程式或連接的虛擬機器 toohello 資料庫或容錯移轉 hello 資料庫 toocause 應用程式連線失敗。

## <a name="when-tooinitiate-recovery"></a>當 tooinitiate 復原
hello 復原作業會影響 hello 應用程式。 它需要變更 hello SQL 連接字串或使用 DNS 的重新導向，並可能導致資料永久遺失。 因此，它應該在完成時，才 hello 中斷可能 toolast 超過您的應用程式復原時間目標。 當 hello 的應用程式部署的 tooproduction 您應該執行的 hello 應用程式健全狀況規則監視，並使用 hello 下列 hello 復原的點 tooassert 已獲得保證的資料：

1. 從 hello 應用程式層 toohello 資料庫永久的連線失敗。
2. hello Azure 入口網站在 hello 廣泛的影響區域中顯示事件的相關警示。
3. hello Azure SQL Database 伺服器標示為降級狀態。

根據您應用程式容錯 toodowntime 和可能的商務負擔，您可以考慮 hello 下列修復選項。

使用 hello[取得可復原的資料庫](https://msdn.microsoft.com/library/dn800985.aspx)(*LastAvailableBackupDate*) tooget hello 最新的地理複寫的還原點。

## <a name="wait-for-service-recovery"></a>等候服務復原
hello Azure 團隊工作努力 toorestore 服務可用性為快速越好，但根據 hello 根本原因可能需要數小時或天。  如果您的應用程式可以容忍您只可以等候 hello 復原 toocomplete 顯著的停機時間。 在此情況下，您不需要採取任何動作。 您可以看到 hello 目前服務的狀態上我們[Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)。 Hello 區域 hello 復原後將還原應用程式的可用性。

## <a name="fail-over-toogeo-replicated-secondary-database"></a>容錯移轉 toogeo 複寫的次要資料庫
如果您應用程式的停機可能會導致商務責任，您應該在應用程式中使用異地複寫的資料庫。 它可讓 hello 應用程式 tooquickly 還原可用性不同的區域發生中斷。 了解如何太[設定異地複寫](sql-database-geo-replication-portal.md)。

hello toorestore 可用性資料庫，您需要 tooinitiate hello 容錯移轉 toohello 異地備援次要使用其中一種支援的 hello 方法。

使用其中一種下列指南 toofail tooa 異地備援的次要資料庫上的 hello:

* [容錯移轉 tooa 異地備援次要資料庫使用 Azure 入口網站](sql-database-geo-replication-portal.md)
* [容錯移轉 tooa 異地備援的次要資料庫使用 PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [容錯移轉 tooa 異地備援次要資料庫使用 T-SQL](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>使用異地還原進行復原
如果您的應用程式停機時間並不會導致商務責任您可以使用[異地還原](sql-database-recovery-using-backups.md)方法 toorecover 為您的應用程式資料庫。 從其最新的異地備援備份建立 hello 資料庫的複本。

## <a name="configure-your-database-after-recovery"></a>在復原之後設定資料庫
如果您使用地理複寫容錯移轉或異地還原 toorecover 從中斷，您必須確定 hello 連線 toohello 新的資料庫已正確設定，以便可以繼續 hello 一般應用程式函式。 這是復原的資料庫的實際執行的工作 tooget 的檢查清單。

### <a name="update-connection-strings"></a>更新連接字串
因為您已復原的資料庫會位於不同的伺服器，您需要 tooupdate 應用程式的連接字串 toopoint toothat 伺服器。

如需有關如何變更連接字串的詳細資訊，請參閱適當的開發語言 hello 您[連線庫](sql-database-libraries.md)。

### <a name="configure-firewall-rules"></a>設定防火牆規則
您需要 toomake 確定 hello 防火牆規則設定伺服器和 hello 資料庫相符項目上的 hello 主要伺服器與主要資料庫上的設定。 如需詳細資訊，請參閱 [如何：進行防火牆設定 (Azure SQL Database)](sql-database-configure-firewall-settings.md)。

### <a name="configure-logins-and-database-users"></a>設定登入和資料庫使用者
您必須確定所有應用程式所使用的 hello 登入都存在 hello 伺服器裝載您復原的資料庫上 toomake。 如需詳細資訊，請參閱[異地複寫的安全性設定](sql-database-geo-replication-security-config.md)。

> [!NOTE]
> 您應該在災害復原演練期間設定和測試伺服器防火牆規則與登入 (及其權限)。 這些伺服器層級物件，而且其設定可能無法使用 hello 中斷期間。
> 
> 

### <a name="setup-telemetry-alerts"></a>設定遙測警示
您需要 toomake 確定您現有的警示規則設定是更新的 toomap toohello 復原的資料庫與 hello 不同的伺服器。

如需有關資料庫警示規則的詳細資訊，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)和[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。

### <a name="enable-auditing"></a>啟用稽核
如果稽核為必要的 tooaccess 您的資料庫，您需要 tooenable hello 資料庫復原後的稽核。 如需詳細資訊，請參閱[資料庫稽核 (英文)](sql-database-auditing.md)。

## <a name="next-steps"></a>後續步驟
* toolearn 有關自動化 Azure SQL Database 備份，請參閱[SQL 資料庫自動備份](sql-database-automated-backups.md)
* toolearn 有關業務持續性設計及修復案例，請參閱[持續性案例](sql-database-business-continuity.md)
* toolearn 有關使用自動的備份進行復原，請參閱[hello 服務起始的備份還原的資料庫](sql-database-recovery-using-backups.md)

