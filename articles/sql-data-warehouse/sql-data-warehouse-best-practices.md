---
title: "Azure SQL 資料倉儲的 aaaBest 作法 |Microsoft 文件"
description: "開發 Azure SQL 資料倉儲的解決方案時應該知道的建議和最佳作法。 這些可協助您成功。"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Azure SQL 資料倉儲最佳做法
這篇文章是許多可協助您從 Azure SQL 資料倉儲 tooachieve 達到最佳效能的最佳作法的集合。  本文中的 hello 概念有些基本簡便 tooexplain、 更進階的其他概念和我們剛 scratch hello 介面在本文中。  hello 本文的目的是 toogive 您為您的重要區域 toofocus 一些基本指導方針和 tooraise 感知建置您的資料倉儲。  每個區段為您介紹 tooa 概念，以及您 toomore 詳細文章更深層的封面 hello 概念然後點。

如果您剛開始使用 Azure SQL 資料倉儲，千萬別讓這篇文章嚇到您。  hello 主題 hello 序列是大部分是在 hello 依重要性的順序。  如果您開始將焦點放在 hello 先一些概念，您會在良好的圖形。  當您更熟悉 SQL 資料倉儲且能運用自如，再回來看看其他概念。  不會讓所有項目長 toomake 意義。

## <a name="reduce-cost-with-pause-and-scale"></a>利用暫停和調整來降低成本
SQL 資料倉儲的重要功能是 hello 能力 toopause 時您不使用它，它會阻止 hello 計費的計算資源。  Hello 能力 tooscale 資源是另一個重要的功能。  暫停和縮放比例即可透過 hello Azure 入口網站或透過 PowerShell 命令。  熟悉這些功能時不使用時，它們可大幅減少您的資料倉儲 hello 成本。  如果您一定想要您的資料倉儲可存取，您可能想 tooconsider 規模 toohello 最小的大小，DW100，而不是暫停。

另請參閱[暫停計算資源][Pause compute resources]、[繼續計算資源][Resume compute resources]、[調整計算資源]。

## <a name="drain-transactions-before-pausing-or-scaling"></a>暫停或調整之前先清空交易
當您暫停或調整您的 SQL 資料倉儲時，幕後 hello 起始 hello 時，您的查詢已取消暫停或調整規模要求。  取消簡單的 SELECT 查詢是快速的作業花費 toopause 幾乎沒有影響 toohello 時間及調整您的執行個體。  不過，交易的查詢，修改您的資料或 hello 結構的 hello 資料，可能不能 toostop 快速。  **顧名思義，交易性查詢必須完全完成或回復變更。**  正在復原交易式的查詢所完成的 hello 工作可能需要長時間，或甚至更長，比 hello 原始變更 hello 查詢已套用，因為。  例如，如果您取消已刪除資料列和一小時已執行的查詢，可能會需要 hello 系統小時 tooinsert 後 hello 資料列已刪除。  如果您執行 暫停 或 縮放比例，而交易中，您暫停，或者縮放比例可能看起來很 tootake 很長的時間因為暫停調整擁有 hello 復原 toocomplete 的 toowait 才能繼續。

另請參閱[了解交易][Understanding transactions]、[最佳化交易][Optimizing transactions]

## <a name="maintain-statistics"></a>維護統計資料
不同於 SQL Server (會自動偵測資料行並建立或更新資料行上的統計資料)，SQL 資料倉儲需要手動維護統計資料。  雖然我們計劃 toochange 這在未來，如現在您會想 toomaintain hello SQL 資料倉儲計劃您的統計資料 tooensure hello 進行最佳化。  hello 最佳化工具所建立的 hello 計劃，才適合 hello 可用的統計資料。  **每個資料行上建立取樣的統計資料是簡單的方式 tooget 入門統計資料。**  它是同樣重要 tooupdate 統計資料會大幅變更，就可能發生 tooyour 資料。  保守的作法可能 tooupdate 統計資料每日或每次載入之後。  總是會有效能與 hello 成本 toocreate 和更新統計資料之間的取捨。 如果您發現所需花費太長 toomaintain 所有統計資料，您可能想 tootry toobe 更具選擇性有關哪些資料行具有統計資料或資料行需要頻繁的更新。  例如，您可能會想 tooupdate 日期資料行，其中新的值可能會加入、 每日。 **您將可以 hello 最大效益，，具有資料行包含在聯結中，使用 hello 子句資料行找到和 GROUP BY 中的資料行的統計資料。**

另請參閱[管理資料表的統計資料][Manage table statistics]、[CREATE STATISTICS][CREATE STATISTICS]、[UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>將 INSERT 陳述式群組為批次
一次性負載 tooa 小型資料表的 INSERT 陳述式或甚至查閱定期重新載入可能會正常執行，針對您的需求與陳述式類似`INSERT INTO MyLookup VALUES (1, 'Type 1')`。  不過，如果您需要 tooload 成千上萬的 hello 整天的資料列，您可能會發現，單一插入就無法跟上。  相反地，開發您的程序，讓他們撰寫 tooa 檔案，並另一個處理序定期出現，並載入此檔案。

另請參閱 [INSERT][INSERT]

## <a name="use-polybase-tooload-and-export-data-quickly"></a>快速地使用 PolyBase tooload 和匯出資料
SQL 資料倉儲支援透過數種工具 (包括 Azure Data Factory、PolyBase、BCP) 來載入及匯出資料。  若是小量的資料，效能不是那麼重要，任何工具都可以滿足您的需求。  不過，當您載入或匯出大量資料或者需要快速效能，PolyBase 是 hello 最好的選擇。  PolyBase 是設計的 tooleverage hello MPP （大量平行處理） 架構的 SQL 資料倉儲會因此載入，且任何其他工具匯出的資料範圍。  您可使用 CTAS 或 INSERT INTO 來執行 PolyBase 載入。  **使用 CTAS 可以減少交易記錄和 hello 最快方式 tooload 您的資料。**  Azure Data Factory 也支援 PolyBase 載入。  PolyBase 支援各種不同的檔案格式，包括 Gzip 檔案。  **toomaximize 輸送量使用 gzip 文字檔案時，中斷檔案為 60 或多個檔案 toomaximize 平行處理原則的負載。**  如需更快的總輸送量，請考慮同時載入資料。

另請參閱[載入資料][Load data]、[PolyBase 使用指南][Guide for using PolyBase]、[Azure SQL 資料倉儲載入模式和策略][Azure SQL Data Warehouse loading patterns and strategies]、[使用 Azure Data Factory 載入資料][Load Data with Azure Data Factory]、[使用 Azure Data Factory 移動資料][Move data with Azure Data Factory]、[CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]、[Create table as select (CTAS)][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>載入並查詢外部資料表
Polybase，也稱為外部資料表，可以是 hello 最快方式 tooload 資料，但並非最佳的查詢。 SQL 資料倉儲 Polybase 資料表目前僅支援 Azure blob 檔案。 這些檔案沒有任何支援的計算資源。  如此一來，SQL 資料倉儲無法卸載此工作，因此必須 hello 整個檔案來讀取 tootempdb 順序 tooread hello 資料中的將它載入。  因此，如果您有數個將會查詢此資料的查詢時，它會更好的 tooload 這項資料一次，且有使用 hello 本機資料表的查詢。

另請參閱[使用 PolyBase 的指南][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>雜湊分散大型資料表
根據預設，資料表是以「循環配置資源」方式分散。  這可讓啟動建立資料表，而不需要其資料表應該要如何散發的 toodecide 使用者 tooget 輕鬆。  循環配置資源的資料表在某些工作負載中執行良好，但某些狀況下選取分散資料行的執行效能會更好。  兩個大型事實資料表會聯結時時發佈的資料行的資料表將會遠優於循環配置資源表格 hello 最常見範例。  例如，如果您有 orders 資料表中，已發佈 order_id 和 [異動] 資料表，也會散佈 order_id，由上 order_id 聯結 orders 資料表 tooyour 交易資料表時，此查詢會變成傳遞查詢，這表示我們免除資料移動作業。  較少的步驟代表較快的查詢。  較少的資料移動也會讓查詢更快。  這項說明只而已 hello 介面。 當載入分散式的資料表，請確定，內送的資料並未排序 hello 散發索引鍵上因為這會減慢您載入。  請參閱下方的 hello 對許多更多詳細資料，在選取散發資料行如何改善效能，以及如何連結 toodefine 分散式 hello 的建立資料表陳述式的 WITH 子句中資料表。

另請參閱[資料表概觀][Table overview]、[資料表散發][Table distribution]、[選取資料表散發][Selecting table distribution]、[CREATE TABLE][CREATE TABLE]、[CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>不要過度執行資料分割
雖然資料分割可以讓資料維護變得有效率 (透過分割切換或最佳化掃描將分割消除)，太多的資料分割會讓查詢變慢。  通常在 SQL Server 上運作良好的高資料粒度分割策略，可能無法在 SQL 資料倉儲上運作良好。  有太多資料分割在每個資料分割是否超過 1 百萬個資料列，也可以減少叢集資料行存放區索引的 hello 效能。  請記住，hello 幕後 SQL 資料倉儲分割您的資料為您為 60 的資料庫，因此如果您建立 100 個資料分割資料表，這實際上會導致 6000 的資料分割。  每個工作負載是不同的因此 hello 最佳的建議是 tooexperiment 與 toosee 最適合您的工作負載的分割區。  請考慮比您的 SQL Server 上運作良好的資料粒度更低的粒度。  例如，考慮使用每週或每月資料分割，而不是每日資料分割。

另請參閱[資料表分割][Table partitioning]

## <a name="minimize-transaction-sizes"></a>將交易大小最小化
在交易中執行的 INSERT、UPDATE、DELETE 陳述式，失敗時必須回復。  toominimize hello 可能很長的回復，將交易規模盡可能降到最低。  這可以透過將 INSERT、UPDATE、DELETE 陳述式分成小部分來達成。  例如，如果您希望 tootake 1 小時，盡可能插入，分成 hello 插入 4 個部分，會在 15 分鐘每個執行。  利用特殊採用最低限度記錄的情況，例如 CTAS、 TRUNCATE、 DROP TABLE 或插入 tooempty 資料表 tooreduce 回復的風險。  另一個方式 tooeliminate 回復為 toouse 僅中繼資料作業，例如資料分割切換資料管理。  比方說，而不是比在 2001 年 10 月中的 hello order_date 所在的資料表中執行 DELETE 陳述式 toodelete 所有資料列，您無法分割資料的每個月後再切換移出 hello 具有空的分割區從另一個資料表之資料的資料分割 （請參閱 ALTER資料表範例）。  未分割的資料表，請考慮使用您想要在資料表中的 tookeep CTAS toowrite hello 資料，而不是使用 DELETE。  如果 CTAS 採用 hello 相同的時間量，因為它有很少的交易記錄，而且必要時可以快速地取消是較安全的作業 toorun。

另請參閱[了解交易][Understanding transactions]、[最佳化交易][Optimizing transactions]、[資料表分割][Table partitioning]、[TRUNCATE TABLE][TRUNCATE TABLE]、[ALTER TABLE][ALTER TABLE]、[Create table as select (CTAS)][Create table as select (CTAS)]

## <a name="use-hello-smallest-possible-column-size"></a>使用 hello 最小的可能資料行大小
在定義的 DDL 時，使用 hello 最小支援資料類型將您的資料將可改善查詢效能。  這對 CHAR 和 VARCHAR 資料行尤其重要。  如果資料行中的 hello 最長值為 25 個字元，然後為 VARCHAR(25) 定義您的資料行。  應避免定義所有字元資料行 tooa 較大的預設長度。  此外，將資料行定義為 VARCHAR (當它只需要這樣的大小時) 而非 NVARCHAR。

另請參閱[資料表概觀][Table overview]、[資料表的資料類型][Table data types]、[CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>針對暫時性資料使用暫存堆積資料表
當您暫時包括登陸 SQL 資料倉儲上的資料時，您可能會發現使用堆積的資料表會進行更快 hello 整體程序。  如果您載入它之前執行多個轉換、 載入 hello tooheap 資料表將會比載入 hello 資料 tooa 快很多的資料只有 toostage 叢集資料行存放區資料表。  此外，載入資料 tooa 暫存資料表也將載入速度比將載入資料表 toopermanent 儲存體。  暫存資料表以"#"開頭，而且只存取 hello 工作階段的建立，因此可能只在少數情況下運作。   堆積資料表定義 hello WITH 子句的 CREATE TABLE 中。  如果您使用暫存資料表，請太記得 toocreate 該暫存資料表上的統計資料。

另請參閱[暫存資料表][Temporary tables]、[CREATE TABLE][CREATE TABLE]、[CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>將叢集資料行存放區資料表最佳化
叢集資料行存放區索引是其中一種 hello 最有效率的方式，您可以將資料儲存在 Azure SQL 資料倉儲中。  根據預設，SQL 資料倉儲中的資料表會建立為「叢集資料行存放區」。  tooget hello 最佳的效能資料行存放區資料表，擁有良好的區段高品質的查詢會很重要。  當資料列寫 toocolumnstore 資料表，記憶體不足的壓力時，資料行存放區區段品質可能會降低。  壓縮的資料列群組中的資料列數目可以測量區段品質。  請參閱 hello[編製索引的品質不佳的資料行存放區的原因][ Causes of poor columnstore index quality]在 hello[資料表索引][ Table indexes]文章的逐步指示偵測及改善叢集資料行存放區資料表的區段品質。  高品質資料行存放區區段很重要，因為它是個不錯的主意 toouse 使用者 id 在 hello 中型或大型的資源類別來載入資料。  hello 較少 Dwu 您使用，hello 較大 hello 資源類別會想 tooassign tooyour 載入使用者。

因為資料行存放區資料表通常不會將資料推送至壓縮的資料行存放區區段直到超過 1 百萬個資料列，每個資料表，而且每個 SQL 資料倉儲資料表已分割到 60 個資料表，以根據經驗法則，資料行存放區資料表不會獲益的查詢除非 hello 資料表有超過 60 百萬個資料列。  對於具有少於 60 百萬個資料列資料表，它可能會進行任何有意義 toohave 資料行存放區索引。  但也無傷大雅。  此外，如果您要分割您的資料，您會想 tooconsider 每個資料分割將需要 toohave 1 百萬個資料列 toobenefit 從叢集資料行存放區索引。  如果資料表有 100 個資料分割，則必須從叢集資料行存放區 toohave 至少 6 10 億個資料列 toobenefit (60 分佈 * 100 個資料分割 * 1 百萬個資料列)。  如果在此範例中，您的資料表並沒有 6 10 億個資料列，減少 hello 資料分割數目，或請考慮改用堆積資料表。  它也可能值得實驗 toosee 如果次要索引的堆積資料表，而不是資料行存放區資料表以獲得更佳的效能。  資料行存放區資料表尚不支援次要索引。

查詢資料行存放區資料表時，查詢將會執行速度如果您選取只 hello 您需要資料行。  

另請參閱[資料表索引][Table indexes]、[資料行存放區索引指南][Columnstore indexes guide]、[重建資料行存放區索引][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>使用較大的資源類別 tooimprove 查詢效能
SQL 資料倉儲會使用資源群組方式 tooallocate 記憶體 tooqueries 做。  超出 hello 方塊中，會指定所有使用者授與 100 MB 的每個散發記憶體 toohello 小型資源類別。  由於總是會有 60 的分佈和每個散發有至少 100 MB，系統寬 hello 總記憶體配置是 6000 MB 或低於 6 GB。  某些查詢，例如大型聯結或載入 tooclustered 資料行存放區資料表，會從較大的記憶體配置中獲益。  有些查詢，像是純掃描，則沒有任何好處。  在 hello 翻轉端，使用較大的資源類別會影響並行存取，所以您會想 tootake 這之前將所有使用者 tooa 大型的資源類別的考量。

另請參閱[並行存取和工作負載管理][Concurrency and workload management]

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>使用較小的資源類別 tooIncrease 並行
您會注意到使用者查詢似乎 toohave 長時間的延遲，可能是，如果您的使用者在較大的資源類別中執行，以及耗用大量的並行插槽造成其他查詢 tooqueue 向上。  toosee 使用者查詢會排入佇列，如果執行`SELECT * FROM sys.dm_pdw_waits`toosee 如果傳回任何資料列。

另請參閱[並行存取和工作負載管理][Concurrency and workload management]、[sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>使用 Dmv toomonitor 和最佳化查詢
SQL 資料倉儲已可使用的 toomonitor 查詢執行數個 Dmv。  hello 監視下列文件引導上於執行 hello 細節 toolook 如何查詢的逐步指示。  tooquickly 尋找這些 Dmv 查詢，您的查詢使用 hello 標籤選項可協助。

另請參閱[使用 DMV 監視工作負載][Monitor your workload using DMVs]、[LABEL][LABEL]、[OPTION][OPTION]、[sys.dm_exec_sessions][sys.dm_exec_sessions]、[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests]、[sys.dm_pdw_request_steps][sys.dm_pdw_request_steps]、[sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests]、[sys.dm_pdw_dms_workers]、[DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN]、[sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>其他資源
另請參閱[疑難排解][Troubleshooting]一文中的常見問題和解決方案。

如果您沒有看到您所尋找的本文中，請嘗試使用 hello 「 搜尋文件 」 hello 左邊的這個頁面 toosearch 所有 hello Azure SQL 資料倉儲文件。  hello [Azure SQL 資料倉儲 MSDN 論壇][ Azure SQL Data Warehouse MSDN Forum]您 tooask 問題 tooother 使用者和 toohello SQL 資料倉儲產品群組已建立做為位置。  我們會主動監視您的問題會有所解答，藉由另一位使用者或其中一個我們此論壇 tooensure。  如果您偏好 tooask 的堆疊溢位問題，我們也有[Azure SQL 資料倉儲堆疊溢位論壇][Azure SQL Data Warehouse Stack Overflow Forum]。

最後，請不要使用 hello [Azure SQL 資料倉儲意見][ Azure SQL Data Warehouse Feedback]頁面 toomake 功能要求。  加入您的要求或票選其他要求確實可協助我們決定功能的優先順序。

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[調整計算資源]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
