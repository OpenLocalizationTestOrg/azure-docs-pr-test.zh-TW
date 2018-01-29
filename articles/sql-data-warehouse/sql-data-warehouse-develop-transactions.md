---
title: "SQL 資料倉儲中的交易 | Microsoft Docs"
description: "在 Azure SQL 資料倉儲中實作交易以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 29d53e18539f2c24dd64090b2ac6f9dd4c783961
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>SQL 資料倉儲中的交易
如您所預期，SQL 資料倉儲支援交易做為資料倉儲工作負載的一部分。 不過，為了確保 SQL 資料倉儲的效能維持在一定的程度，某些功能會受到限制 (相較於 SQL Server)。 本文特別強調差異，並列出其他交易。 

## <a name="transaction-isolation-levels"></a>交易隔離層級
SQL 資料倉儲實作 ACID 交易。 不過，交易支援的隔離僅限於 `READ UNCOMMITTED` ，這無法變更。 您可以實作許多編碼方法，以避免中途讀取 (dirty read) 資料 (如果您對此有所考量的話)。 大多數受歡迎的方法會運用 CTAS 和資料表分割切換 (通常也稱為滑動視窗模式)，以防止使用者查詢仍正準備中的資料。 預先篩選資料的檢視也是常用的方法。  

## <a name="transaction-size"></a>交易大小
單一資料修改交易的大小是有限制的。 「每個散發」都會套用目前的限制。 因此，將限制乘以散發計數可算出總配置。 若要大致估計交易中的資料列總數，請將散發容量除以每個資料列的大小總計。 針對可變動的長度資料行，請考慮取得平均資料行長度，而不是使用大小上限。

在下表中，已進行下列假設：

* 已發生的資料平均散發 
* 平均資料列長度是 250 個位元組

| [DWU][DWU] | 每個散發的容量 (GiB) | 散發的數目 | 交易大小上限 (GiB) | 每個散發的資料列數 | 每個交易的資料列數上限 |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4,000,000 |240,000,000 |
| DW200 |1.5 |60 |90 |6,000,000 |360,000,000 |
| DW300 |2.25 |60 |135 |9,000,000 |540,000,000 |
| DW400 |3 |60 |180 |12,000,000 |720,000,000 |
| DW500 |3.75 |60 |225 |15,000,000 |900,000,000 |
| DW600 |4.5 |60 |270 |18,000,000 |1,080,000,000 |
| DW1000 |7.5 |60 |450 |30,000,000 |1,800,000,000 |
| DW1200 |9 |60 |540 |36,000,000 |2,160,000,000 |
| DW1500 |11.25 |60 |675 |45,000,000 |2,700,000,000 |
| DW2000 |15 |60 |900 |60,000,000 |3,600,000,000 |
| DW3000 |22.5 |60 |1,350 |90,000,000 |5,400,000,000 |
| DW6000 |45 |60 |2,700 |180,000,000 |10,800,000,000 |

系統會針對每個交易或作業套用交易大小限制。 它不會套用到所有並行交易。 因此允許每一個交易在記錄檔中寫入這個資料量。 

若要最佳化寫入記錄的資料量並降到最低，請參閱[交易的最佳做法][Transactions best practices]一文。

> [!WARNING]
> 交易大小上限僅可針對 HASH 或 ROUND_ROBIN 散發資料表 (資料會平均分佈) 來達成。 如果交易是以扭曲方式將資料寫入散發，則可能會在到達交易大小上限之前就先達到限制。
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>交易狀態
SQL 資料倉儲會使用 XACT_STATE() 函式 (採用值 -2) 來報告失敗的交易。 這表示交易已失敗並標示為僅可復原

> [!NOTE]
> XACT_STATE 函式使用 -2 表示失敗的交易，以代表 SQL Server 中不同的行為。 SQL Server 使用值 -1 來代表無法認可的交易。 SQL Server 可以容忍交易內的某些錯誤，而不需將其標示為無法認可。 例如， `SELECT 1/0` 會導致錯誤，但不會強制交易進入無法認可的狀態。 SQL Server 也允許讀取無法認可的交易。 不過，SQL 資料倉儲不會讓您這樣做作。 如果 SQL 資料倉儲交易內部發生錯誤，就會自動進入 -2 狀態，而且您不能進行任何進一步的 Select 陳述式，直到陳述式回復為止。 因此，檢查您的應用程式程式碼是否使用 XACT_STATE() 就相當重要，因為您可能需要修改程式碼。
> 
> 

比方說，在 SQL Server 中，您可能會看到類似這樣的交易：

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

如果您將您的程式碼保持原狀 (如上方所示)，您將會收到下列錯誤訊息：

Msg 111233, Level 16, State 1, Line 1 111233;目前的交易已經中止，並已回復任何暫止的變更。 原因︰處於僅限復原狀態中的交易，未在使用 DDL、DML 或 SELECT 陳述式之前明確復原。

您也不會收到 ERROR_* 函式的輸出。

SQL 資料倉儲中的程式碼需要稍微變更：

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

目前已觀察到預期的行為。 已管理交易中的錯誤，且 ERROR_* 函式提供了預期的值。

唯一的變更就是交易的 `ROLLBACK` 必須在讀取 `CATCH` 區塊中的錯誤資訊之前發生。

## <a name="errorline-function"></a>Error_Line() 函式
另外值得注意的是，SQL 資料倉儲不會實作或支援 ERROR_LINE() 函式。 如果您的程式碼中有此函式，您必須將它移除才能符合 SQL 資料倉儲。 在程式碼中使用查詢標籤，而不需實作對等的功能。 如需這項功能的詳細資料，請參閱 [LABEL][LABEL] 一文。

## <a name="using-throw-and-raiserror"></a>使用 THROW 和 RAISERROR
THROW 是在 SQL 資料倉儲中引發例外狀況的新式作法，但也支援 RAISERROR。 不過，有一些值得注意的差異。

* 對於 THROW，使用者定義的錯誤訊息數目不能在 100,000 - 150,000 範圍內
* RAISERROR 錯誤訊息固定為 50,000
* 不支援使用 sys.messages

## <a name="limitiations"></a>限制
SQL 資料倉儲有一些與交易相關的其他限制。

如下所示：

* 沒有分散式交易
* 不允許巢狀交易
* 不允許儲存點
* 沒有具名的交易
* 沒有標示的交易
* 使用者定義的交易內部不支援 DDL，例如 `CREATE TABLE`

## <a name="next-steps"></a>後續步驟
若要深入了解最佳化交易，請參閱[交易的最佳做法][Transactions best practices]。  若要深入了解其他 SQL 資料倉儲最佳作法，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse best practices]。

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
