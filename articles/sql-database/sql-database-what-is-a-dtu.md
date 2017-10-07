---
title: "SQL Database：DTU 是什麼？ | Microsoft Docs"
description: "了解 Azure SQL Database 交易單元是什麼。"
keywords: "資料庫選項, 資料庫效能"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: CarlRabeler
ms.assetid: 89e3e9ce-2eeb-4949-b40f-6fc3bf520538
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 04/13/2017
ms.author: carlrab
ms.openlocfilehash: ba1fe580b32826259edaf6c8dc124faaf5b3d234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-database-transaction-units-dtus-and-elastic-database-transaction-units-edtus"></a>說明資料庫交易單位 (DTU) 和彈性資料庫交易單位 (eDTU)
本文說明資料庫交易單位 (Dtu) 和彈性資料庫交易單位 (Edtu) 及您叫用時，會發生什麼事 hello 最大 Dtu 或是 Edtu。  

## <a name="what-are-database-transaction-units-dtus"></a>何謂資料庫交易單位 (DTU)
單一 Azure SQL database 在特定的效能層級內[服務層](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels)，Microsoft 保證特定層級的資源，該資料庫 （獨立於任何其他資料庫 hello Azure 雲端中），並提供可預測的效能層級。 此資源數量會計算為資料庫交易單位 (DTU) 數量，且為 CPU、記憶體、I/O (資料與交易記錄 I/O) 的混合測量。 原本由 hello 這些資源之間的比率[OLTP 基準測試工作負載](sql-database-benchmark-overview.md)設計 toobe 典型的真實世界 OLTP 工作負載。 您的工作負載超過任何這些資源的 hello 數量，您的輸送量時，節流-產生速度較慢的效能和逾時。 您的工作負載所使用的 hello 資源不會影響 hello 資源可用 tooother hello Azure 的雲端中的 SQL 資料庫和 hello 的其他工作負載所使用的資源不會影響 hello 資源可用 tooyour SQL 資料庫。

![週框方塊](./media/sql-database-what-is-a-dtu/bounding-box.png)

Dtu 是最適用於了解 hello 相對資源數量不同的效能層級的 Azure SQL Database 服務層之間。 例如，藉由增加 hello 資料庫效能層級加倍 hello Dtu 等同 toodoubling hello 一組資源可用 toothat 資料庫。 例如，相較於具有 5 個 DTU 的 Basic 資料庫，具有 1750 個 DTU 的 Premium P11 資料庫可提供 350 倍的 DTU 計算能力。  

toogain 深入探索您的工作負載使用 hello (DTU) 的資源耗用量[Azure SQL 資料庫查詢效能深入解析](sql-database-query-performance.md)至：

- 識別 hello 排名最前面查詢依 CPU/期間執行計數可能會改善效能進行微調。 例如，I/O 密集的查詢可能會受益的 hello 使用[記憶體中最佳化技巧](sql-database-in-memory.md)toomake 更有效地使用 hello 可用記憶體，在某些服務層和效能層級。
- 向下鑽研至 hello 詳細資料的查詢、 檢視其文字和資源使用量的歷程記錄。
- 存取效能微調建議，其會顯示 [SQL Database Advisor](sql-database-advisor.md) 執行的動作。

您可以[來變更服務層](sql-database-service-tiers.md)隨時以最少停機時間 tooyour 應用程式 （通常平均底下 4 秒）。 許多企業和應用程式，所能 toocreate 資料庫以及撥隨選效能向上或向下即已足夠，特別是如果使用模式是相對的可預測。 但是，如果您有無法預期的使用模式，它可更難 toomanage 成本和商務模型。 此案例中，您可以使用彈性集區與 hello 集區中的多個資料庫所共用的 Edtu 數目。

![簡介 tooSQL 資料庫： 單一資料庫依階層和層級的 Dtu](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

## <a name="what-are-elastic-database-transaction-units-edtus"></a>何謂彈性資料庫交易單位 (eDTU)
而是提供的一組專用的資源 (Dtu) tooa 遊客不論是否不需要的 SQL 資料庫，您可以將至[彈性集區](sql-database-elastic-pool.md)上共用的資源集區的 SQL Database 伺服器在這些資料庫。 彈性資料庫交易單位或 Edtu 所測量的彈性集區中的 hello 共用資源。 彈性集區提供符合成本效益的簡單解決方案 toomanage hello 效能目標的多個有不同的廣泛的資料庫和無法預期的使用模式。 彈性集區，您可保證沒有一個資料庫使用的所有 hello 資源在 hello 集區和的資源有最小數量一律為彈性集區中的可用 tooa 資料庫。 如需詳細資訊，請參閱[彈性集區](sql-database-elastic-pool.md)。

![簡介 tooSQL 資料庫： Edtu 依階層和層級](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

集區以固定價格提供固定數目的 eDTU。 Hello 彈性集區中的個別資料庫會提供 hello 彈性 tooauto 延展 hello 設定界限內。 負載過重，雖然在淺色負載下的資料庫耗用小於底下沒有負載的資料庫使用沒有 Edtu toohello 點設定資料庫時，可以使用 Edtu toomeet 需求。 藉由佈建 hello 整個集區的資源，而非每個資料庫、 管理工作經過簡化而且您擁有 hello 集區的可預測的預算。

其他的 Edtu 可以加入 tooan 現有集區，而不會影響任何資料庫的停機時間與 hello 集區中的 hello 資料庫上。 同樣地，如果不再需要額外 eDTU，則隨時可以從現有集區中移除。 您可以加入或減去資料庫 toohello 集區，或限制 hello 數量的 Edtu 資料庫可用於在高載量 tooreserve Edtu 其他資料庫。 如果資料庫會如預期般使用資源，您可以將它移出 hello 集區並將它設定為其所需的資源的可預測量的單一資料庫。

## <a name="how-can-i-determine-hello-number-of-dtus-needed-by-my-workload"></a>如何判斷我的工作負載所需的 Dtu 的 hello 數目？
如果您要尋找 toomigrate 現有內部部署或 SQL Server 虛擬機器工作負載 tooAzure SQL 資料庫，您可以使用 hello [DTU 計算機](http://dtucalculator.azurewebsites.net/)所需的 Dtu tooapproximate hello 數目。 您可以使用現有的 Azure SQL Database 工作負載[SQL 資料庫查詢效能深入解析](sql-database-query-performance.md)toounderstand 如何您資料庫資源耗用量 (Dtu) tooget 深入探索 toooptimize 您的工作負載。 您也可以使用 hello [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) DMV tooget hello 資源耗用量資訊 hello 最後一個小時。 或者，hello 目錄檢視[sys.resource_stats](http://msdn.microsoft.com/library/dn269979.aspx)可以也是查詢的 tooget hello 相同的資料 hello 過去 14 天，雖然在五分鐘的平均較低精確度。

## <a name="how-do-i-know-if-i-could-benefit-from-an-elastic-pool-of-resources"></a>如何得知我能受益於彈性資源集區？
集區適合於具備特定使用模式的大量資料庫。 針對指定的資料庫，此模式的特徵是低平均使用量與相對不頻繁的使用量高峰。 SQL Database 會自動評估 hello 歷史資源使用量中現有的 SQL 資料庫伺服器的資料庫，並且建議 hello Azure 入口網站中的 hello 適當的集區組態。 如需詳細資訊，請參閱 [何時應該使用彈性集區？](sql-database-elastic-pool.md)

## <a name="what-happens-when-i-hit-my-maximum-dtus"></a>當我達到 DTU 上限時會發生什麼狀況
制定效能層級和管的 tooprovide hello 所需資源 toorun 資料庫工作負載向上 toohello 允許您選取的服務層/效能層級的最大限制。 如果您的工作負載叫用其中一種資料 CPU/IO/Log IO 限制 hello 限制，您在 hello 最大的允許層級繼續 tooreceive hello 資源，但可能 toosee 增加延遲對於您的查詢。 這些限制不會導致任何錯誤，但而是會降低 hello 工作負載，除非 hello 緩慢的問題變得嚴重，查詢開始時間。如果您達到最大允許並行使用者工作階段/要求 (背景工作執行緒) 的限制，您會看到明確的錯誤。 如需 CPU、記憶體、資料 I/O 和交易記錄檔 I/O 以外的資源限制資訊，請參閱 [Azure SQL Database 資源限制](sql-database-resource-limits.md) 。

## <a name="next-steps"></a>後續步驟
* 請參閱[服務層](sql-database-service-tiers.md)hello 的 dtu 數及可用與彈性集區的單一資料庫的 edtu 數目上的資訊。
* 如需 CPU、記憶體、資料 I/O 和交易記錄檔 I/O 以外的資源限制資訊，請參閱 [Azure SQL Database 資源限制](sql-database-resource-limits.md) 。
* 請參閱[SQL 資料庫查詢效能深入解析](sql-database-query-performance.md)toounderstand (Dtu) 取用。
* 請參閱[SQL Database 基準測試概觀](sql-database-benchmark-overview.md)toounderstand hello 方法背後 hello OLTP 基準測試工作負載使用 toodetermine hello DTU blend。
