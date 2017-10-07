---
title: "aaaOperating Azure SQL Database 中的查詢存放區"
description: "了解如何 toooperate hello Azure SQL Database 中的查詢存放區"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>作業 hello Azure SQL Database 中的查詢存放區
Azure 中的查詢存放區是完全受管理的資料庫功能，可持續收集及呈現有關所有查詢的詳細歷程記錄資訊。 您可以將有關查詢存放區視為類似 tooan 飛機的飛行資料記錄器，大幅簡化了查詢效能進行疑難排解的雲端和內部部署客戶。 這篇文章說明在 Azure 中操作查詢存放區的特定層面。 您可以使用此預先收集的查詢資料，快速地診斷並解決效能問題，因此能夠花更多時間專注於業務上。 

查詢存放區已自 2015 年 11 月在 Azure SQL Database 中 [通用版本上市](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) 。 查詢存放區是 hello 基礎效能分析及調整功能，例如[SQL 資料庫建議程式與效能儀表板](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)。 在發行這篇文章的 hello 時刻，查詢存放區正在執行中 200,000 以上的使用者資料庫，在 Azure 中，收集查詢相關的幾個月，而不中斷的資訊。

> [!IMPORTANT]
> Microsoft 是啟用查詢存放區的所有 Azure SQL 資料庫 （現有和新） hello 處理程序中。 
> 
> 

## <a name="optimal-query-store-configuration"></a>最佳查詢存放區組態
本章節描述最佳組態的預設值設計的 tooensure 作業可靠的 hello 查詢存放區和相依的功能，例如[SQL 資料庫建議程式與效能儀表板](https://azure.microsoft.com/updates/sqldatabaseadvisorga/)。 預設組態已針對持續收集資料最佳化，也就是在 OFF/READ_ONLY 狀態花費最少的時間。

| 組態 | 說明 | 預設值 | 註解 |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |指定查詢存放區可能需要 z 客戶資料庫內部的 hello 資料空間的 hello 上限 |100 |對新資料庫強制執行 |
| INTERVAL_LENGTH_MINUTES |定義彙總和保存查詢計畫所收集到的執行階段統計資料的時段大小。 對於此組態定義的一段時間，每個使用中的查詢計劃最多會有一個資料列 |60 |對新資料庫強制執行 |
| STALE_QUERY_THRESHOLD_DAYS |以時間為基礎的清除原則，可控制保存的執行階段統計資料和非使用中查詢的 hello 保留期限 |30 |對新資料庫和具有先前的預設值 (367) 的資料庫強制執行 |
| SIZE_BASED_CLEANUP_MODE |指定是否自動清除資料都發生在查詢存放區資料的大小接近 hello 限制 |AUTO |對所有資料庫強制執行 |
| QUERY_CAPTURE_MODE |指定是否會追蹤所有查詢或只有查詢的子集 |AUTO |對所有資料庫強制執行 |
| FLUSH_INTERVAL_SECONDS |指定最長期間的擷取執行階段統計資料會保留在記憶體中之前排清 toodisk |900 |對新資料庫強制執行 |
|  | | | |

> [!IMPORTANT]
> 在查詢存放區啟用 （請參閱上述的重要附註） 的所有 Azure SQL 資料庫中的 hello 最後階段中，會自動套用這些預設值。 之後設定此燈，Azure SQL Database 不變更組態值設定的客戶，除非它們產生負面影響主要工作負載或可靠的 hello 查詢存放區的作業。
> 
> 

如果您想 toostay 的自訂設定，請使用[使用查詢存放區選項的 ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) toorevert 組態 toohello 先前的狀態。 簽出[hello 查詢存放區的最佳做法](https://msdn.microsoft.com/library/mt604821.aspx)順序 toolearn 如何頂端選擇最佳的組態參數。

## <a name="next-steps"></a>後續步驟
[SQL Database 效能深入解析](sql-database-performance.md)

## <a name="additional-resources"></a>其他資源
詳細的資訊簽出 hello 下列文章：

* [您的資料庫的航班資料錄製器](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [監視效能所使用的 hello 查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx)
* [查詢存放區使用案例](https://msdn.microsoft.com/library/mt614796.aspx)
* [監視效能所使用的 hello 查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx) 

