---
title: "適用於工作負載管理的資源類別 - Azure SQL 資料倉儲 | Microsoft Docs"
description: "在 Azure SQL 資料倉儲中，使用資源類別來管理並行和適用於查詢之計算資源的指引。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 122646f73b6e4e7c62eb0e6d4b6672b603d8acb2
ms.sourcegitcommit: b979d446ccbe0224109f71b3948d6235eb04a967
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2017
---
# <a name="resource-classes-for-workload-management"></a>適用於工作負載管理的資源類別
在 Azure SQL 資料倉儲中，使用資源類別來管理同時執行的並行查詢數目以及適用於查詢之計算資源的指引。
 
## <a name="what-is-workload-management"></a>什麼是工作負載管理？
工作負載管理是將所有查詢的整體效能最佳化的能力。 精心調整的工作負載會有效率地執行查詢和載入作業，而不論它們是否為計算密集型或 IO 密集型的作業。 

SQL 資料倉儲會針對多使用者環境提供工作負載管理功能。 資料倉儲不適用於多租用戶工作負載。

## <a name="what-are-resource-classes"></a>什麼是資源類別？
資源類別是預先決定來控管查詢執行的資源限制。 SQL 資料倉儲會根據資源類別來限制每個查詢的計算資源。 

資源類別有助於您管理資料倉儲工作負載的整體效能。有效率地使用資源類別，可協助您管理工作負載，方法是在同時執行的查詢數目和指派給每個查詢的計算資源上設定限制。 

- 較小的資源類別使用較少的計算資源，但會啟用更好的整體查詢並行
- 較大的資源類別提供更多的計算資源，但會限制查詢並行

資源類別是專為資料管理和操作活動而設計的。 如果有大型聯結和排序，部分非常複雜的查詢也很有助益，因為系統會在記憶體中執行查詢，而不會溢出到磁碟。

下列作業都受到資源類別所控管：

* INSERT-SELECT、UPDATE、DELETE
* SELECT (當查詢使用者資料表時)
* ALTER INDEX - REBUILD 或 REORGANIZE
* ALTER TABLE REBUILD
* CREATE INDEX
* CREATE CLUSTERED COLUMNSTORE INDEX
* CREATE TABLE AS SELECT (CTAS)
* 載入資料
* 資料移動服務 (DMS) 進行的資料移動作業

> [!NOTE]  
> 動態管理檢視 (DMV) 或其他系統檢視上的 SELECT 陳述式不受任何並行限制所控管。 不論在系統上執行的查詢數目多寡，您都可監視該系統。
> 
> 

## <a name="static-and-dynamic-resource-classes"></a>靜態和動態的資源類別

有兩種類型的資源類別：動態和靜態。

- **靜態資源類別**會配置相同數量的記憶體，而不論目前的服務等級為何，這會以[資料倉儲單位](what-is-a-data-warehouse-unit-dwu-cdwu.md)來測量。 這個靜態配置表示在較大的服務等級上，您可以在每個資源類別中執行更多查詢。  靜態資源類別會命名為 staticrc10、staticrc20、staticrc30、staticrc40、staticrc50、staticrc60、staticrc70 和 staticrc80。 這些資源類別最適合增加資源類別以取得額外計算資源的解決方案。

- **動態資源類別**會根據目前的服務等級來配置數量不一的記憶體。 當您相應增加為較大的服務等級時，查詢會自動獲得更多記憶體。 動態資源類別會命名為 smallrc、mediumrc、largerc 和 xlargerc。 這些資源類別最適合增加計算規模以取得額外資源的解決方案。 

[效能層級](performance-tiers.md)會使用相同的資源類別名稱，但具有不同的[記憶體和並行規格](performance-tiers.md)。 


## <a name="assigning-resource-classes"></a>指派資源類別

資源類別會藉由將使用者指派給資料庫角色來實作。 當使用者執行查詢時，查詢會利用使用者的資源類別來執行。 例如，當使用者為 smallrc 或 staticrc10 資料庫角色的成員時，他們的查詢會利用少量記憶體來執行。 當資料庫使用者為 xlargerc 或 staticrc80 資料庫角色的成員時，他們的查詢會利用大量記憶體來執行。 

若要增加使用者的資源類別，請使用預存程序 [sp_addrolemember](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) \(英文\)。 

```sql
EXEC sp_addrolemember 'largerc', 'loaduser';
```

若要減少資源類別，使用 [sp_droprolemember](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql) \(英文\)。  

```sql
EXEC sp_droprolemember 'largerc', 'loaduser';
```

服務管理員的資源類別是固定且無法變更的。  服務管理員是在佈建程序期間建立的使用者。

### <a name="default-resource-class"></a>預設的資源類別
根據預設，每位使用者都是小型資源類別 **smallrc** 的成員。 

### <a name="resource-class-precedence"></a>資源類別優先順序
使用者可以是多個資源類別的成員。 當使用者屬於多個資源類別時：

- 動態資源類別的優先順序高於靜態資源類別。 例如，如果使用者是 mediumrc (動態) 和 staticrc80 (靜態) 的成員，查詢會使用 mediumrc 來執行。
- 較大資源類別的優先順序高於較小資源類別。 例如，如果使用者是 mediumrc 和 largerc 的成員，查詢會使用 largerc 來執行。 同樣地，如果使用者是 staticrc20 和 statirc80 的成員，查詢會使用 staticrc80 資源配置來執行。

### <a name="queries-exempt-from-resource-classes"></a>從資源類別中排除的查詢
儘管使用者是較大資源類別的成員，有些查詢還是一律會在 smallrc 資源類別中執行。 這些排除的查詢不會計入並行限制。 例如，如果並行限制為 16，許多使用者可以從系統檢視中選取，而不會影響可用的並行位置。

下列陳述式會從資源類別中排除，且一律在 smallrc 中執行：

* CREATE 或 DROP TABLE
* ALTER TABLE ...SWITCH、SPLIT 或 MERGE PARTITION
* ALTER INDEX DISABLE
* DROP INDEX
* CREATE、UPDATE 或 DROP STATISTICS
* TRUNCATE TABLE
* ALTER AUTHORIZATION
* CREATE LOGIN
* CREATE、ALTER 或 DROP USER
* CREATE、ALTER 或 DROP PROCEDURE
* CREATE 或 DROP VIEW
* INSERT VALUES
* 從系統檢視和 DMV 來 SELECT
* EXPLAIN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

## <a name="recommendations"></a>建議
我們建議您建立專用於執行特定類型之查詢或載入作業的使用者。 接著，為該使用者指定永久性資源類別，而不是頻繁地變更資源類別。 假設靜態資源類別在工作負載上提供更好的整體控制，我們也建議在考慮動態資源類別之前先使用那些類別。

### <a name="resource-classes-for-load-users"></a>載入使用者適用的資源類別
`CREATE TABLE` 預設會使用叢集的資料行存放區索引。 將資料壓縮到資料行存放區索引是記憶體密集型作業，而記憶體壓力會降低索引品質。 因此，您最可能在載入資料時需要較高的資源類別。 若要確保載入具有足夠的記憶體，您可以建立要指定來執行載入的使用者，並將該使用者指派給較高的資源類別。

若要有效率地處理載入，所需的記憶體取決於所載入之資料表的性質和資料大小。 如需有關記憶體需求的詳細資訊，請參閱[將資料列群組品質最大化](sql-data-warehouse-memory-optimizations-for-columnstore-compression.md)。

一旦您決定記憶體需求之後，請選擇是否要將載入使用者指派給靜態或動態資源類別。

- 當資料表記憶體需求落在特定範圍內時，請使用靜態資源類別。 載入會使用適當的記憶體來執行。 當您調整資料倉儲時，載入不需要更多記憶體。 記憶體配置藉由使用靜態資源類別來維持一致。 這種一致性可節省記憶體，並允許同時執行多個查詢。 我們建議新的解決方案先使用靜態資源類別，因為這些提供更好的控制。
- 當資料表記憶體需求相當廣泛時，請使用動態資源類別。 載入所需的記憶體可能比目前的 DWU 或 cDWU 層級提供的更多。 因此，調整資料倉儲會將更多記憶體新增至載入作業，讓載入能夠執行得更快。

### <a name="resource-classes-for-queries"></a>查詢適用的資源類別

某些查詢需要大量計算，有些則不用。  

- 當查詢很複雜，但不需高度並行處理時，請選擇動態資源類別。  例如，產生每日或每週報表，偶爾需要使用資源。 如果報表正在處理大量資料，則調整資料倉儲會為使用者現有的資源類別提供更多記憶體。
- 若對資源的預期一整天都不一樣，請選擇靜態資源類別。 例如，當許多人查詢資料倉儲時，靜態資源類別會運作得很好。 調整資料倉儲時，不會變更配置給使用者的記憶體量。 因此，可以在系統上平行執行更多查詢。

選取要授與的適當記憶體取決於許多因素，例如，查詢的資料量、資料表結構描述的性質，以及各種聯結、選取和群組述詞。 一般來說，配置更多的記憶體讓查詢能夠更快完成，但會減少整體並行能力。 如果您不在意並行能力，則超額配置記憶體不會損害輸送量。 

若要調整效能，請使用不同的資源類別。 下一節提供可協助您找出最佳資源類別的預存程序。

## <a name="example-code-for-finding-the-best-resource-class"></a>尋找最佳資源類別的範例程式碼
 
您可以使用下列預存程序，找出在給定 SLO 時要對每個資源類別授與的並行存取能力和記憶體，以及在給定資源類別時最適合非分割 CCI 資料表上的記憶體密集 CCI 作業使用的最接近資源類別：

以下是此預存程序的用途：  
1. 在指定的 SLO，查看對每個資源類別授與的並行和記憶體。 使用者必須同時為結構描述和 tablename 提供 NULL，如此範例所示。  
2. 在指定的資源類別，查看最適合非分割 CCI 資料表上的記憶體密集型 CCI 作業 (載入、複製資料表、重建索引等) 使用的最接近資源類別。 此預存程序會使用資料表結構描述來找出所需授與的記憶體。

### <a name="dependencies--restrictions"></a>相依性及限制：
- 此預存程序並非設計來計算分割 CCI 資料表的記憶體需求。    
- 此預存程序不會針對 CTAS/INSERT-SELECT 的 SELECT 部分考慮記憶體需求，而會假設它是一個 SELECT。
- 此預存程序會使用暫存資料表，可在此預存程序建立所在的工作階段中使用。    
- 此預存程序仰賴目前的供應項目 (例如，硬體組態、DMS 組態)，如果其中有任何變更，則此預存程序就無法正確運作。  
- 此預存程序仰賴目前提供的並行限制，如果限制有任何變更，則此預存程序就無法正確運作。  
- 此預存程序仰賴現有的資源類別供應項目，如果有任何變更，則此預存程序就無法正確運作。  

>  [!NOTE]  
>  如果您在使用所提供的參數來執行預存程序後沒有獲得輸出，則可能有兩種情況。 <br />1.DW 參數包含無效的 SLO 值 <br />2.或者，對於資料表上的 CCI 作業，沒有任何相符的資源類別。 <br />例如，在 DW100，可供授與的最高記憶體為 400 MB，但資料表結構描述的寬度卻足以跨過 400 MB 的需求。
      
### <a name="usage-example"></a>使用範例：
語法：  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU: 提供 NULL 參數以從資料倉儲資料庫擷取目前的 DWU，或是以 'DW100' 的形式提供任何受支援的 DWU
2. @SCHEMA_NAME: 提供資料表的結構描述名稱
3. @TABLE_NAME: 提供相關的資料表名稱

執行此預存程序的範例：  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

下列陳述式會建立要在前述範例中使用的 Table1。
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

### <a name="stored-procedure-definition"></a>預存程序定義

```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(@DWU VARCHAR(7),
 @SCHEMA_NAME VARCHAR(128),
 @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for the current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need to supply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temp table (CTAS) to hold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping to their corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```




## <a name="next-steps"></a>後續步驟
如需管理資料庫使用者和安全性的詳細資訊，請參閱[保護 SQL 資料倉儲中的資料庫][Secure a database in SQL Data Warehouse]。 如需較大資源類別如何改善叢集資料行存放區索引品質的詳細資訊，請參閱[資料行存放區壓縮的記憶體最佳化](sql-data-warehouse-memory-optimizations-for-columnstore-compression.md)。

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Rebuilding indexes to improve segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
