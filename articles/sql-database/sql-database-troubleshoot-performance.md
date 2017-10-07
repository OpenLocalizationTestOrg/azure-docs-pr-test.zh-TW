---
title: "aaaMonitoring （& s) 效能調整-Azure SQL Database |Microsoft 文件"
description: "透過評估和改進來調整 Azure SQL Database 效能的秘訣。"
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: "sql 效能調整，資料庫效能調整，sql 效能調整秘訣，sql 資料庫效能調整"
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a>監視和效能微調

Azure SQL Database 自動管理，而且有彈性的資料服務，您可以輕鬆地監視使用量、 新增或移除資源 （CPU、 記憶體、 io），尋找可以改善效能，您的資料庫，或讓資料庫調整 tooyour 工作負載的建議和自動讓效能最佳化。

本文提供 Azure SQL Database 中可用的監視和效能微調選項概觀。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a>針對資料庫效能進行監視和疑難排解

Azure SQL Database 可讓您 tooeasily 監視資料庫的使用量，以及識別可能造成 hello 效能問題的查詢。 您可以使用 Azure 入口網站或系統檢視來監視資料庫效能。 您有下列選項來監視和疑難排解資料庫效能的 hello:

1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下  **SQL 資料庫**選取 hello 資料庫，然後使用 hello 監視圖表 toolook 接近其最大的資源。 預設會顯示 DTU 耗用量。 按一下**編輯**toochange hello 時間範圍和顯示的值。
2. 使用[查詢效能深入解析](sql-database-query-performance.md)tooidentify hello 查詢花費的最 hello 的資源。
3. 您可以使用動態管理檢視 (Dmv)，擴充的事件 (`XEvents`)，和 hello 即時 SSMS tooget 效能參數中的查詢存放區。

請參閱 hello[效能指引主題](sql-database-performance-guidance.md)toofind 技術，您就可以使用 Azure SQL Database 的 tooimprove 效能，如果您找出使用這些報表或檢視表的一些問題。

> [!IMPORTANT] 
> 建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。 [更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。
>

## <a name="optimize-database-tooimprove-performance"></a>最佳化資料庫 tooimprove 效能

Azure SQL Database 可讓您 tooidentify 機會 tooimprove 和最佳化查詢效能，而不變更資源，藉由檢閱[效能微調建議](sql-database-advisor.md)。 遺漏索引與查詢最佳化不足是資料庫效能不佳的常見原因。 您可以套用您的工作負載這些微調建議 tooimprove 效能。
您也可以讓的 Azure SQL database 太[自動最佳化查詢效能](sql-database-automatic-tuning.md)藉由套用所有識別的建議，並確認它們改善資料庫效能。 您可以使用下列選項 tooimprove 對資料庫效能的 hello:

1. 使用[SQL Database Advisor](sql-database-advisor-portal.md) tooview 建立和卸除索引、 參數化查詢，以及修正結構描述問題的建議。
2. [啟用自動調整](sql-database-automatic-tuning-enable.md)並讓 Azure SQL Database 自動修正發現的效能問題。

## <a name="improving-database-performance-with-more-resources"></a>使用更多資源提升資料庫效能

最後，如果沒有可採取動作的項目，可以改善您資料庫的效能，您可以變更 hello Azure SQL Database 中可用的資源數量。 您可以指派更多資源，藉由變更 hello[服務層](sql-database-service-tiers.md)獨立的資料庫，或在任何時間增加彈性集區的 edtu 數 （hello）。
1. 您可以為獨立資料庫[來變更服務層](sql-database-service-tiers.md)隨 tooimprove 資料庫效能。
2. 針對多個資料庫，請考慮使用[彈性集區](sql-database-elastic-pool-guidance.md)tooscale 資源自動。

## <a name="tune-and-refactor-application-or-database-code"></a>調整和重構應用程式或資料庫程式碼

您可以變更應用程式程式碼 toomore 最佳的方式使用 hello 資料庫、 變更索引、 強制執行計劃，或使用 toomanually 調整 hello 資料庫 tooyour 工作負載的提示。 尋找一些指導方針和秘訣手動調整或重寫 hello hello 碼[效能指引主題](sql-database-performance-guidance.md)發行項。


## <a name="next-steps"></a>後續步驟

- 自動調整 Azure SQL Database，然後讓自動 tooenable 完全微調功能管理您的工作負載，請參閱[啟用自動調整](sql-database-automatic-tuning-enable.md)。
- toouse 手動微調，您可以檢閱[微調建議，在 Azure 入口網站中的](sql-database-advisor-portal.md)並手動套用 hello 改善查詢效能的項目。
- 變更 [Azure SQL Database 服務層](sql-database-performance-guidance.md)來變更資料庫中可用的資源