---
title: "aaaDesign 指導複寫的資料表-Azure SQL 資料倉儲 |Microsoft 文件"
description: "針對在「Azure SQL 資料倉儲」結構描述中設計複寫資料表提供建議。"
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a>在 Azure SQL 資料倉儲中使用複寫資料表的設計指引
本文針對在「SQL 資料倉儲」結構描述中設計複寫資料表提供建議。 使用這些建議 tooimprove 查詢效能降低資料移動和查詢的複雜性。

> [!NOTE]
> hello 複寫的資料表功能目前處於公開預覽狀態。 某些行為是主體 toochange。
> 

## <a name="prerequisites"></a>必要條件
本文假設您已熟悉「SQL 資料倉儲」中的資料散發和資料移動概念。  如需詳細資訊，請參閱[分散式資料](sql-data-warehouse-distributed-data.md)。 

資料表設計的一部分，了解最大的資料，及其如何 hello 查詢資料。  例如，請思考一下下列問題：

- 大小是 hello 資料表？   
- Hello 資料表重新整理的頻率？   
- 我是否在資料倉儲中有事實資料表和維度資料表？   

## <a name="what-is-a-replicated-table"></a>什麼是複寫資料表？
複寫的資料表有 hello 資料表可存取的完整複本，每個計算節點上。 複寫資料表中移除計算節點，然後再聯結或彙總之間的 hello 需要 tootransfer 資料。 Hello 資料表有多個複本，因為複寫的資料表時效果最佳 hello 資料表大小會小於 2 GB 壓縮。

hello 圖顯示可供存取每個計算節點上的複寫的資料表。 在 SQL 資料倉儲、 hello 複寫的資料表會是每個計算節點上的完整複製的 tooa 散發資料庫。 

![複寫的資料表](media/guidance-for-using-replicated-tables/replicated-table.png "複寫的資料表")  

複寫資料表適用於星型結構描述中的小型維度資料表。 維度資料表通常都使得 toostore 可行的大小，並維護多個複本。 維度會儲存變更緩慢的描述性資料，例如客戶名稱和地址，以及產品詳細資料。 hello 緩時變 hello 資料的本質會導致 toofewer 重建的 hello 複寫的資料表。 

在下列情況下，請考慮使用複寫資料表：

- 在磁碟上的 hello 資料表大小為小於 2 GB，不論 hello 的資料列數目。 toofind hello 的資料表大小，您可以使用 hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql)命令： `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`。 
- hello 資料表用於聯結需要移動資料。 例如上分散雜湊資料表, 的聯結時 hello 聯結的資料行不是 hello 相同的散發資料行需要資料移動。 如果其中一個 hello 雜湊散發資料表很小，請考慮複寫的資料表。 循環配置資源資料表上的聯結需要進行資料移動。 建議您在大多數情況下都使用複寫資料表，而不要使用循環配置資源資料表。 


請考慮將轉換的現有分散式資料表 tooa 複寫的資料表：

- 查詢計劃使用廣播 hello 資料 tooall hello 計算節點的資料移動作業。 hello BroadcastMoveOperation 昂貴，而且會降低查詢效能。 tooview 資料移動作業，在查詢計畫中，使用[sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql)。
 
複寫的資料表可能不會產生最佳查詢效能 hello 時：

- hello 資料表有頻繁的插入、 更新和刪除作業。 這些資料操作語言 (DML) 作業需要重建 hello 複寫資料表。 經常重建會導致效能變差。
- hello 資料倉儲會經常調整。 調整資料倉儲變更 hello 運算節點數目，而造成重建。
- hello 資料表有大量的資料行，但資料作業通常存取只有少數資料行。 在此案例中，而不是複寫 hello 整份資料表，它可能會更有效率的 toohash 散發 hello 資料表，然後 hello 經常存取的資料行上建立索引。 當查詢需要的資料移動，SQL 資料倉儲，只在 hello 移動資料要求資料行。 



## <a name="use-replicated-tables-with-simple-query-predicates"></a>使用複寫資料表搭配簡單查詢述詞
您選擇 toodistribute 或複寫資料表之前，請考慮 hello 您計劃 toorun hello 資料表的查詢類型。 請儘可能

- 針對含有簡單查詢述詞 (例如相等比較或不等比較) 的查詢使用複寫資料表。
- 針對含有複雜查詢述詞 (例如相似或不相似) 的查詢使用分散式資料表。

Hello 工作會分散到所有的 hello 運算節點時，則需要大量 CPU 的查詢會具有最佳。 例如，以在資料表的每個資料列上執行計算的查詢來說，在複寫資料表上執行會比在分散式資料表上執行效能更佳。 儲存複寫的資料表中每個計算節點上的完整，因此需要大量 CPU 的查詢，針對複寫的資料表會針對 hello 整份資料表上執行的每個計算節點。 hello 額外的計算會降低查詢效能。

例如，此查詢含有複雜的述詞。  當供應者是分散式資料表而不是複寫資料表時，它的執行速度較快。 在此範例中，供應者可以是雜湊分散式或循環配置資源分散式資料表。

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a>轉換現有的循環配置資源資料表 tooreplicated 資料表
如果您已經有循環配置資源的資料表，我們建議將它們轉換 tooreplicated 資料表符合本文所述的準則。 複寫的資料表循環配置資源資料表改善效能，因為它們不需要進行資料移動的 hello 需要。  循環配置資源資料表針對聯結一律需要進行資料移動。 

這個範例會使用[CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory 資料表 tooa 複寫資料表。 不論 DimSalesTerritory 是雜湊分散式還是循環配置資源資料表，此範例都有效。

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a>循環配置資源與複寫之查詢效能比較範例 

複寫的資料表不為聯結需要移動任何資料，因為 hello 整份資料表已經存在每個計算節點上。 如果 hello 維度資料表是分散式循環配置資源，聯結會在完整 tooeach 計算節點複製 hello 維度資料表。 toomove hello 資料，hello 查詢計劃包含呼叫 BroadcastMoveOperation 作業。 這類資料移動作業會降低查詢效能，而使用複寫資料表則可免除這類作業。 tooview 查詢計畫的步驟，使用 hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql)系統目錄檢視。 

例如，下列查詢針對 hello AdventureWorks 結構描述中，在 hello` FactInternetSales`資料表是雜湊散發。 hello`DimDate`和`DimSalesTerritory`資料表為較小的維度資料表。 此查詢會傳回 2004年會計年度北美地區的 hello 總銷售額：
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
我們已將 `DimDate` 和 `DimSalesTerritory` 重新建立成循環配置資源資料表。 如此一來，hello 查詢示範了下列查詢計劃，具有多個廣播移動作業的 hello: 
 
![循環配置資源的查詢計劃](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

重新建立`DimDate`和`DimSalesTerritory`做為複寫資料表，並再次執行 hello 查詢。 hello 產生查詢計劃是較短，而且未有任何廣播移動。

![複寫的查詢計劃](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a>修改複寫資料表時的效能考量
SQL 資料倉儲實作複寫的資料表，藉由維護 hello 資料表的主要版本。 它會複製 hello 主要版本 tooone 每個計算節點上的散發資料庫。 變更時，SQL 資料倉儲會先更新 hello 主要資料表。 然後，它會需要重建 hello 資料表每個計算節點上。 複寫資料表的重建包含複製 hello 資料表 tooeach 計算節點，然後再重建 hello 索引。

在執行下列動作之後，必須進行重建：
- 載入或修改資料
- hello 資料倉儲是縮放的 tooa 不同的 DWU 設定
- 更新資料表定義

在執行下列動作之後，不須進行重建：
- 暫停作業
- 繼續作業

在修改資料之後，立即 hello 重建不會發生。 相反地，就會觸發 hello 重建 hello 從 hello 資料表選取查詢的第一次。  Hello 初始 select 陳述式中從 hello 資料表是步驟 toorebuild hello 複寫的資料表。  Hello 重建 hello 查詢中進行設定，因為 hello 影響 toohello 初始 select 陳述式可能是重大 hello hello 資料表大小而定。  如果需要重建涉及多個複寫的資料表時，每個複本就會以序列方式重建 hello 陳述式中的步驟。  toomaintain 資料一致性的 hello hello 重建時複寫的資料表的獨佔鎖定在 hello 資料表取得。  hello 鎖定會防止所有存取 toohello 表 hello 重建 hello 持續期間。 

### <a name="use-indexes-conservatively"></a>謹慎地使用索引
標準索引作法適用於 tooreplicated 資料表。 SQL 資料倉儲重建 hello 重建一部分的每個複寫的資料表索引。 Hello 效能改善超過 hello 成本重建 hello 索引時，只使用索引。  
 
### <a name="batch-data-loads"></a>批次資料載入
當資料載入複寫資料表中，以重試 toominimize 重建一起批次處理載入。 執行 select 陳述式之前執行所有批次的 hello 負載。

例如，以下載入模式會從四個來源載入資料，然後叫用四次重建。 

- 從來源 1 載入。
- Select 陳述式觸發重建 1。
- 從來源 2 載入。
- Select 陳述式觸發重建 2。
- 從來源 3 載入。
- Select 陳述式觸發重建 3。
- 從來源 4 載入。
- Select 陳述式觸發重建 4。

例如，以下載入模式會從四個來源載入資料，但只會叫用一次重建。

- 從來源 1 載入。
- 從來源 2 載入。
- 從來源 3 載入。
- 從來源 4 載入。
- Select 陳述式觸發重建。


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a>在批次載入後重建複寫資料表
tooensure 一致的查詢執行時間，建議使用強制重新整理 hello 複寫資料表的批次載入之後。 否則，hello 第一個查詢必須等候 hello 資料表 toorefresh 包含重建 hello 索引。 根據 hello 大小和受影響的複寫資料表的數目，hello 效能的影響可能十分顯著。  

此查詢會使用 hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello 複寫已修改，但不重新建立資料表。

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
執行陳述式之後 hello 上述輸出中的每個資料表上的 hello tooforce 重建。 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a>後續步驟 
toocreate 複寫的資料表，請使用其中一個陳述式：

- [CREATE TABLE (Azure SQL 資料倉儲)](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [CREATE TABLE AS SELECT (Azure SQL 資料倉儲)](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

如需分散式資料表的概觀，請參閱[分散式資料表](sql-data-warehouse-tables-distribute.md)。



