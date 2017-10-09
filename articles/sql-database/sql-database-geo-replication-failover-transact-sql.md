---
title: "TSQL：起始 Azure SQL Database 的容錯移轉 | Microsoft Docs"
description: "使用 Transact-SQL 為 Azure SQL Database 起始計劃性或非計劃性容錯移轉"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>使用 Transact-SQL 為 Azure SQL Database 起始計劃性或非計劃性容錯移轉

本文章將示範如何 tooinitiate 容錯移轉 tooa 使用 TRANSACT-SQL 的次要 SQL 資料庫。 tooconfigure 異地複寫，請參閱[for Azure SQL Database 設定異地複寫](sql-database-geo-replication-transact-sql.md)。

tooinitiate 容錯移轉時，您需要下列 hello:

* 為 DBManager hello 主要的登入
* 具有 db_ownership hello 本機資料庫，您會進行異地複寫
* DBManager 位於 hello 夥伴伺服器 toowhich 您將設定異地複寫
* 最新版的 SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> 建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。 [更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>初始化規劃的容錯移轉升級的次要資料庫 toobecome hello 新主要複本
您可以使用 hello **ALTER DATABASE**陳述式 toopromote 次要資料庫 toobecome hello 新主要複本在計劃的方式，降級 hello 現有主要 toobecome 次要資料庫。 Hello master 資料庫中的 hello 所在地理區域複寫的次要資料庫正在升級的 hello Azure SQL Database 邏輯伺服器上執行此陳述式。 這項功能規劃的容錯移轉，例如設計期間 hello DR 鑽研，而且需要該 hello 主要資料庫可以使用。

hello 命令會執行下列工作流程的 hello:

1. 交換器複寫 toosynchronous 模式，導致所有未完成的交易 toobe 暫時排清 toohello 次要資料庫，封鎖所有新的交易。
2. 交換器 hello hello hello 地理複寫合作關係中的兩個資料庫的角色。  

此順序可保證該 hello hello 角色切換，因此會發生資料不會遺失之前，同步處理兩個資料庫。 沒有在短期間這兩個資料庫是無法使用 （在 0 too25 秒 hello 順序） 而 hello 角色切換。 如果 hello 主要資料庫中有多個次要資料庫、 hello 命令將會自動重新設定 hello 其他次要 tooconnect toohello 新主要複本。  hello 整個作業花費時間小於一分鐘 toocomplete 在一般情況下。 如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。

使用下列步驟 tooinitiate 規劃的容錯移轉的 hello。

1. 在 Management Studio 中進行地理複寫的次要資料庫所在的 toohello Azure SQL Database 邏輯伺服器的連線。
2. 開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。
3. 使用下列 hello **ALTER DATABASE**陳述式 tooswitch hello 次要資料庫 toohello 主要角色。
   
        ALTER DATABASE <MyDB> FAILOVER;
4. 按一下**Execute** toorun hello 查詢。

> [!NOTE]
> 在極少數的情況下，很可能 hello 作業無法完成，而且可能會出現陷入不斷。 在此情況下，hello 使用者可以執行 hello 強制容錯移轉命令，並接受資料遺失。
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>初始化規劃的容錯移轉從 hello 主要資料庫 toohello 次要資料庫
您可以使用 hello **ALTER DATABASE**陳述式 toopromote 次要資料庫 toobecome hello 新的主要資料庫中未規劃的方式，強制 hello 現有主要 toobecome hello 降級次要一次當 hello主要資料庫已無法再使用。 Hello master 資料庫中的 hello 所在地理區域複寫的次要資料庫正在升級的 hello Azure SQL Database 邏輯伺服器上執行此陳述式。

當 hello 資料庫的還原可用性至關重要，而是可以接受的部分資料遺失時，這項功能可供災害復原。 叫用強制容錯移轉時，次要資料庫立即成為 hello 的主要資料庫，以及開始接受寫入交易，也會指定 hello。 Hello 原始的主要資料庫是無法 tooreconnect 與這個新的主要資料庫，因為在 hello 原始的主要資料庫會從增量備份和 hello 舊主要資料庫成為新主要資料庫 hello; 的次要資料庫接著，它是只 hello 新主要複本的同步處理複本。

不過，因為點中還原時間上不支援 hello 次要資料庫，如果 hello 使用者想認可 toorecover 資料 toohello 舊主要資料庫中有尚未複寫 toohello 新的主要資料庫發生 hello 強制容錯移轉之前hello 使用者將需要 tooengage 支援 toorecover 這遺失資料。

如果 hello 主要資料庫中有多個次要資料庫、 hello 命令將會自動重新設定 hello 其他次要 tooconnect toohello 新主要複本。

使用下列步驟 tooinitiate 未規劃的容錯移轉的 hello。

1. 在 Management Studio 中進行地理複寫的次要資料庫所在的 toohello Azure SQL Database 邏輯伺服器的連線。
2. 開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。
3. 使用下列 hello **ALTER DATABASE**陳述式 tooswitch hello 次要資料庫 toohello 主要角色。
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. 按一下**Execute** toorun hello 查詢。

> [!NOTE]
> 如果主要和次要資料庫已上線時，會發出 hello 命令將會變成 hello 舊的主要 hello 立即不進行資料同步處理新的次要資料庫。 如果是主要的 hello hello 命令發出部分資料遺失時認可的交易可能會發生。
> 
> 

## <a name="next-steps"></a>後續步驟
* 容錯移轉之後，確定已 hello 新主要複本上設定您的伺服器和資料庫的 hello 驗證需求。 如需詳細資訊，請參閱 [災害復原後的 SQL Database 安全性](sql-database-geo-replication-security-config.md)。
* 請參閱 toolearn 之後使用作用中地理複寫，包括前復原及復原後的步驟，以及執行災害復原訓練，災害復原[災害復原](sql-database-disaster-recovery.md)
* 如需 Sasha Nosov 有關主動式異地複寫的部落格文章，請參閱[新異地複寫功能要點](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)
* 設計雲端應用程式 toouse 作用中地理複寫的相關資訊，請參閱[設計雲端應用程式使用地理複寫的商務持續性](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* 如需使用主動式異地複寫與彈性集區的相關資訊，請參閱[彈性集區災害復原策略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)。
* 如需商務持續性的概觀，請參閱[商務持續性概觀](sql-database-business-continuity.md)

