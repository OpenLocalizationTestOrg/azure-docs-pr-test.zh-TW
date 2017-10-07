---
title: "aaaSQL 資料倉儲容量限制 |Microsoft 文件"
description: "SQL 資料倉儲的連接、資料庫、資料表及查詢最大值。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>SQL 資料倉儲容量限制
hello 表包含 hello Azure SQL 資料倉儲的各種元件所允許的最大值。

## <a name="workload-management"></a>工作負載管理
| 類別 | 說明 | 最大值 |
|:--- |:--- |:--- |
| [資料倉儲單位 (DWU)][Data Warehouse Units (DWU)] |單一 SQL 資料倉儲的最大 DWU |6000 |
| [資料倉儲單位 (DWU)][Data Warehouse Units (DWU)] |單一 SQL Server 的最大 DWU |預設為 6000<br/><br/> 根據預設，每個 SQL server (例如 myserver.database.windows.net) 有向上 too6000 DWU 讓 45,000 DTU 配額。 此配額僅是安全限制。 您可以增加配額所[建立支援票證][ creating a support ticket] ，然後選取*配額*hello 要求類型。  toocalculate 您 DTU 需要 multiply hello 7.5 的 DWU 所需的 hello 總計。 您可以在 hello 入口網站中檢視您目前的 DTU 耗用量的 hello SQL server 刀鋒視窗。 已暫停且未暫停資料庫會計入 hello DTU 配額。 |
| 資料庫連接 |同時開啟的工作階段 |1024<br/><br/>我們支援最多 1024年作用中連線，其中每一個都可以送出 hello 要求 tooa SQL 資料倉儲資料庫相同的時間。 請注意，有 hello 實際上可以同時執行的查詢數目限制。 當超過 hello 並行限制時，hello 要求便會進入內部佇列，它在等候 toobe 處理。 |
| 資料庫連接 |準備陳述式的最大記憶體 |20 MB |
| [工作負載管理][Workload management] |並行查詢上限 |32<br/><br/> 根據預設，SQL 資料倉儲可以執行最多 32 並行查詢和佇列剩餘查詢。<br/><br/>當使用者被指派 tooa 較高的資源類別，或以低的 DWU 設定 SQL 資料倉儲時，可能會降低 hello 並行層級。 某些查詢，例如 DMV 查詢，一律允許 toorun。 |
| [Tempdb][Tempdb] |Tempdb 的大小上限 |每一 DW100 399 GB。 因此在 DWU1000 Tempdb 是可調整大小的 too3.99 TB |

## <a name="database-objects"></a>資料庫物件
| 類別 | 說明 | 最大值 |
|:--- |:--- |:--- |
| 資料庫 |大小上限 |在磁碟上壓縮後 240 TB<br/><br/>此空間是獨立的 tempdb 或記錄檔空間，因此此空間是專用的 toopermanent 資料表。  叢集資料行存放區壓縮估計為 5 X。  此壓縮可允許 hello 資料庫 toogrow tooapproximately 1 PB 的所有資料表時，叢集資料行存放區 （hello 預設資料表類型）。 |
| 資料表 |大小上限 |磁碟上壓縮後 60 TB |
| 資料表 |每個資料庫的資料表 |20 億 |
| 資料表 |每個資料表的資料行 |1024 個資料行 |
| 資料表 |每個資料行的位元組 |相依於資料行[資料類型][data type]。  char 資料類型的限制為 8000、nvarchar 為 4000 或 MAX 資料類型為 2 GB。 |
| 資料表 |每個資料列的位元組，已定義的大小 |8060 個位元組<br/><br/>hello 計算不限數目的每個資料列的位元組是 hello 中相同的方式，因為它具有頁面壓縮適用於 SQL Server。 SQL Server，例如 SQL 資料倉儲支援資料列溢位儲存，好讓**可變長度資料行**toobe off-row 發送。 當可變長度的資料列會推入同資料列時，只有 24 位元組的根會儲存在 hello 主要記錄中。 如需詳細資訊，請參閱 hello[資料列溢位 Data Exceeding 8] [ Row-Overflow Data Exceeding 8 KB] MSDN 文章。 |
| 資料表 |每個資料表的資料分割 |15,000<br/><br/>我們建議您針對高效能、 hello 數目降到最低的資料分割您需要時仍可支援您的業務需求。 Hello 為分割區數目增加時，hello 額外負荷資料定義語言 (DDL) 以及資料操作語言 (DML) 作業，並會成長會導致效能變慢。 |
| 資料表 |每個資料分割界限值的字元。 |4000 |
| 索引 |每個資料表的非叢集索引。 |999<br/><br/>適用於僅限 toorowstore 資料表。 |
| 索引 |每個資料表的叢集索引。 |1<br><br/>適用於 tooboth 資料列存放區和資料行存放區資料表。 |
| 索引 |索引鍵的大小。 |900 個位元組。<br/><br/>適用於僅限 toorowstore 索引。<br/><br/>如果 hello hello 資料行中的現有資料沒有超過 900 個位元組，建立 hello 索引時，可以建立超過 900 個位元組的大小上限的 varchar 資料行的索引。 不過，稍後插入或更新動作會導致 hello 大小總計 tooexceed 900 個位元組的 hello 資料行上將會失敗。 |
| 索引 |每個索引的索引鍵資料行。 |16<br/><br/>適用於僅限 toorowstore 索引。 叢集資料行存放區索引包含所有資料行。 |
| 統計資料 |Hello 的大小會結合資料行值。 |900 個位元組。 |
| 統計資料 |每個統計資料物件的資料行。 |32 |
| 統計資料 |每個資料表的資料行上建立的統計資料。 |30,000 |
| 預存程序 |最大巢狀層級。 |8 |
| 檢視 |每個檢視表的資料行 |1,024 |

## <a name="loads"></a>載入
| 類別 | 說明 | 最大值 |
|:--- |:--- |:--- |
| PolyBase 載入 |每列 MB 數 |1<br/><br/>Polybase 載入有限的 tooloading 列小於 1 MB，而且無法載入 tooVARCHR(MAX)，nvarchar （max） 或 varbinary （max）。<br/><br/> |

## <a name="queries"></a>查詢
| 類別 | 說明 | 最大值 |
|:--- |:--- |:--- |
| 查詢 |使用者資料表上已排入佇列的查詢。 |1000 |
| 查詢 |系統檢視表上的並行查詢。 |100 |
| 查詢 |系統檢視表上已排入佇列的查詢 |1000 |
| 查詢 |參數個數上限 |2098 |
| 批次 |大小上限 |65,536*4096 |
| SELECT 結果 |每個資料列的資料行 |4096<br/><br/>您絕對不能超過 4096 個每個資料行中 hello 的資料列選取結果。 不保證一定可以有 4096 個。 如果 hello 查詢計劃需要暫存資料表，可能適用每個資料表最大的 hello 1024 個資料行。 |
| SELECT |巢狀子查詢 |32<br/><br/>SELECT 陳述式中一律不超過 32 個巢狀子查詢。 不保證一定可以有 32 個。 例如，聯結可以中導入子查詢 hello 查詢計劃。 hello 數目的子查詢也會受到可用記憶體。 |
| SELECT |每個 JOIN 的資料行 |1024 個資料行<br/><br/>您絕對不能超過 1024 個資料行中 hello 聯結。 不保證一定可以有 1024 個。 如果 hello 聯結計畫需要的資料行多於 hello 聯結結果與暫存資料表，hello 1024 限制適用於 toohello 暫存資料表。 |
| SELECT |每個 GROUP BY 資料行的位元組。 |8060<br/><br/>hello hello GROUP BY 子句中的資料行不能超過 8060 個位元組。 |
| SELECT |每個 ORDER BY 資料行的位元組 |8060 個位元組。<br/><br/>hello hello ORDER BY 子句中的資料行不能超過 8060 個位元組。 |
| 每個陳述式的識別項和常數 |參考的識別項和常數個數。 |65,535<br/><br/>SQL 資料倉儲將識別項和常數，可包含單一查詢的運算式中的 hello 數目限制。 此限制為 65,535。 超過此數字會導致 SQL Server 錯誤 8632。 如需詳細資訊，請參閱[內部錯誤：到達運算式服務的限制][Internal error: An expression services limit has been reached]。 |

## <a name="metadata"></a>中繼資料
| 系統檢視表 | 最大資料列數 |
|:--- |:--- |
| sys.dm_pdw_component_health_alerts |10,000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |SQL 的要求總數的 hello 最近的 1000 DMS 背景工作。 |
| sys.dm_pdw_errors |10,000 |
| sys.dm_pdw_exec_requests |10,000 |
| sys.dm_pdw_exec_sessions |10,000 |
| sys.dm_pdw_request_steps |步驟會儲存在 sys.dm_pdw_exec_requests 的 hello 最近的 1000 SQL 要求總數。 |
| sys.dm_pdw_os_event_logs |10,000 |
| sys.dm_pdw_sql_requests |hello 最近 1000 SQL 要求 sys.dm_pdw_exec_requests 中儲存。 |

## <a name="next-steps"></a>後續步驟
如需更多的參考資訊，請參閱 [SQL 資料倉儲參考概觀][SQL Data Warehouse reference overview]。

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
