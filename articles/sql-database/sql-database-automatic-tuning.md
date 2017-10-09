---
title: "aaaSQL 資料庫-自動調整 |Microsoft 文件"
description: "SQL Database 會分析 SQL 查詢，並自動調整 toouser 工作負載。"
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>自動微調

Azure SQL Database 是完全受管理的資料服務，以監視 hello hello 資料庫上執行，但可以自動提升 hello 工作負載效能的查詢。 Azure SQL Database 具有內建智慧機制可以自動調整及改善查詢效能，透過動態調整 hello 資料庫 tooyour 工作負載。 Azure SQL Database 中的自動調整可能會對 Azure SQL Database toooptimize 效能的查詢，您可以啟用 hello 最重要功能之一。

請參閱這篇文章 hello 步驟太[啟用自動調整](sql-database-automatic-tuning-enable.md)使用 hello Azure 入口網站。

## <a name="why-automatic-tuning"></a>為何需要自動調整？

其中一個傳統資料庫管理中的 hello 主要工作正在監視 hello 工作負載，識別重要的 SQL 查詢的索引，應該會新增 tooimprove 效能，而很少使用的索引。 Azure SQL Database 提供深入了解 hello 查詢和索引，您需要 toomonitor。 不過，持續監視資料庫是冗長乏味的艱辛工作，尤其是在處理許多資料庫時。 管理大量的資料庫可能是不可能 toodo 有效率地甚至具有所有可用的工具和 Azure SQL Database 和 Azure 入口網站提供的報表。 而不是監視，並手動調整您的資料庫，您可能會考慮委派一些 hello 監視及調整動作 tooAzure SQL Database 使用自動調整功能。 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>自動調整的運作方式為何？

Azure SQL Database 有連續的效能監視與分析程序，經常藉以了解您的工作負載特性的 hello 與識別潛在的問題和增強功能。

![自動調整程序](./media/sql-database-automatic-tuning/tuning-process.png)

Azure SQL Database toodynamically 調整 tooyour 工作負載，藉由尋找哪些索引和計劃可能會改善您的工作負載的效能和功能索引，此程序讓會影響您的工作負載。 根據這些調查結果，自動調整會套用可改善工作負載效能的調整動作。 此外，Azure SQL Database 會持續監視，可提升您的工作負載的效能的自動調整 tooensure 所做的任何變更之後的效能。 未能改善效能的任何動作都會自動還原。 這個驗證程序是一項重要功能，可確保所做的自動調整的任何變更不會降低 hello 工作負載效能。

Azure SQL Database 中有兩個可用的自動調整層面：

 -  **自動索引管理**：識別您的資料庫中應該新增的索引，以及應該移除的索引。
 -  **自動計劃更正** (即將推出，已可用於 SQL Server 2017)：識別有問題的計劃並修正 SQL 計劃效能問題。

## <a name="automatic-index-management"></a>自動索引管理

在 Azure SQL 資料庫中，因為 Azure SQL Database 會了解您的工作負載，並確保永遠以最佳方式為資料編製索引，所以索引管理很簡單。 您的工作負載要達到最佳效能，有適當的索引設計非常重要，而且自動索引管理可以協助您將索引最佳化。 自動索引管理可以是在資料庫中不正確的索引，修正效能問題或維護和改善 hello 現有資料庫結構描述的索引。 

### <a name="why-do-you-need-index-management"></a>為什麼需要索引管理？

索引加速一些您從 hello 資料表; 讀取資料的查詢不過，它們會減慢 hello 查詢更新資料。 您需要 toocarefully toocreate 索引和資料行需要在 tooinclude hello 索引時分析。 某些索引在一段時間後可能不再需要。 因此，您會需要 tooperiodically 找出並卸除 hello 索引不會帶來任何益處。 如果您選擇忽略 hello 未使用的索引、 更新資料的 hello 查詢的效能會降低而沒有任何好處 hello 查詢讀取的資料。 未使用的索引也會影響整體系統效能的 hello，因為其他的更新需要不必要的記錄。

尋找 hello 組最佳的索引可改善效能的 hello 從資料表讀取資料，以及對更新的影響降到最低的查詢可能會需要連續且複雜的分析。

Azure SQL Database 會使用內建智慧和分析查詢，請識別索引會針對目前的工作負載，最佳的進階的規則和 hello 索引可能會移除。 Azure SQL Database 可確保您已最佳化讀取資料的 hello 查詢的索引所需的最小集合，而最小化 hello 會影響到 hello 其他查詢。

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>如何 tooidentify 索引您的資料庫中變更該需要 toobe 嗎？

Azure SQL Database 讓索引管理程序變得容易。 而不是手動工作負載分析及監視索引的 hello 冗長程序，Azure SQL Database 分析您的工作負載，找出 hello 查詢可能與新的索引，更快速執行並找出未使用或重複的索引。 如需找出應變更的索引詳細資訊，可在 [Azure 入口網站中的尋找索引建議](sql-database-advisor-portal.md)中找到。

### <a name="automatic-index-management-considerations"></a>自動索引管理考量

如果您發現 hello 內建規則改善 hello 對資料庫效能，您可能會讓 Azure SQL database 會自動管理您的索引。

動作需要 toocreate Azure SQL Database 中的必要索引可能會耗用資源，並暫時影響工作負載效能。 toominimize hello 影響工作負載的效能，Azure SQL Database 上建立索引的任何索引管理作業尋找 hello 適當的時間間隔。 微調動作就會延後，如果 hello 資料庫需要的資源 tooexecute 您的工作負載，並啟動時 hello 資料庫有足夠的資源運用於 hello 維護工作。 自動索引管理中的其中一項重要功能是一種確認的 hello 動作。 當 Azure SQL Database 建立或卸除索引時，監視的處理序會分析您的工作負載 tooverify hello 動作更佳的 hello 效能的效能。 如果它未使顯著改進 – hello 動作才會立即還原。 如此一來，Azure SQL Database 可確保自動採取的動作不會影響工作負載的效能。 索引建立的自動調整是透明 hello hello 基礎結構描述上的維護作業。 結構描述變更，例如卸除或重新命名資料行不會自動建立索引的 hello 與否被封鎖。 Azure SQL Database 自動建立的索引會在與之相關的資料表或資料行遭到卸除時立即卸除。

## <a name="automatic-plan-choice-correction"></a>自動計劃選擇更正

自動計劃更正為 SQL Server 2017 CTP2.0 中新增的自動調整功能，可識別行為異常的 SQL 計劃。 這個自動調整選項即將在 Azure SQL Database 推出。 如需詳細資訊，可在[自動調整 SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning) 中找到。

## <a name="next-steps"></a>後續步驟

- 自動調整 Azure SQL Database，然後讓自動 tooenable 完全微調功能管理您的工作負載，請參閱[啟用自動調整](sql-database-automatic-tuning-enable.md)。
- toouse 手動微調，您可以檢閱[微調建議，在 Azure 入口網站中的](sql-database-advisor-portal.md)並手動套用 hello 改善查詢效能的項目。
