---
title: "SQL 資料倉儲中的 aaaTransactions |Microsoft 文件"
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
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>SQL 資料倉儲中的交易
如您所預期，SQL 資料倉儲 hello 資料倉儲工作負載的部分支援的交易。 不過，SQL 資料倉儲的 tooensure hello 效能所維護的某些功能會受到限制時的小數位數比較的 tooSQL 伺服器。 本文章重點說明 hello 差異，並列出 hello 其他人。 

## <a name="transaction-isolation-levels"></a>交易隔離層級
SQL 資料倉儲實作 ACID 交易。 不過，hello hello 交易支援的隔離是限制太`READ UNCOMMITTED`，就無法變更。 您可以實作的一些程式碼撰寫 tooprevent dirty 讀取的資料，如果這是您的問題的方法。 hello 最受歡迎的方法會利用 CTAS 和資料表資料分割切換 （通常稱為 hello 滑動視窗模式） tooprevent 使用者查詢仍在準備資料。 檢視預先篩選 hello 資料也是常用的方法。  

## <a name="transaction-size"></a>交易大小
單一資料修改交易的大小是有限制的。 hello 現在會套用限制 「 每一通訊群組 」。 因此，hello 總計配置可以計算 hello 限制乘以 hello 發佈計數。 hello 交易中的資料列 tooapproximate hello 最大數目除以 hello 的每個資料列大小總計的 hello 發佈端點。 可變長度資料行，請考慮花費的平均資料行長度，而不是使用 hello 大小上限。

Hello hello 表有進行下列假設：

* 已發生的資料平均散發 
* hello 平均資料列長度是 250 個位元組

| [DWU][DWU] | 每個散發的容量 (GiB) | 散發的數目 | 交易大小上限 (GiB) | # 每發佈的資料列 | 每個交易的資料列數上限 |
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

hello 交易大小限制會套用每個交易或作業。 它不會套用到所有並行交易。 因此每個交易並允許 toowrite 資料 toohello 記錄此數量。 

toooptimize hello toohello 記錄檔中寫入的資料量降到最低，請參閱 toohello[交易的最佳作法][ Transactions best practices]發行項。

> [!WARNING]
> hello 交易大小僅可達成雜湊或 ROUND_ROBIN 分散式的資料表 hello 位置分散的 hello 資料最大值為偶數。 如果 hello 交易正在寫入的資料扭曲方式 toohello 分佈 hello 限制則可能 toobe 達到先前 toohello 最大交易大小。
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>交易狀態
SQL 資料倉儲會使用 hello XACT_STATE 函數 tooreport 失敗的交易使用 hello 值-2。 這表示 hello 交易失敗，且標示為進行僅復原

> [!NOTE]
> hello-2 的 hello XACT_STATE 函數 toodenote 失敗的交易代表不同的行為 tooSQL 伺服器使用。 SQL Server 使用 hello 值-1 toorepresent 認可的交易。 SQL Server 可以容忍某些錯誤，在交易內，而不需要 toobe 標示為認可。 例如， `SELECT 1/0` 會導致錯誤，但不會強制交易進入無法認可的狀態。 SQL Server 也允許 hello 認可的交易讀取。 不過，SQL 資料倉儲不會讓您這樣做作。 如果 SQL 資料倉儲交易內會發生錯誤，它會自動進入 hello-2 狀態，而且您不會無法 toomake 任何進一步 select 陳述式直到 hello 陳述式已回復。 因此，這是您的應用程式程式碼 toosee 如果它是使用 XACT_STATE 您可能需要修改 toomake 程式碼的重要 toocheck。
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

如果您離開您的程式碼，因為其值高於您會收到下列錯誤訊息的 hello:

Msg 111233，層級 16，狀態 1，行 1 111233; 目前交易已中止，而且任何暫止變更已復原的 hello。 原因︰處於僅限復原狀態中的交易，未在使用 DDL、DML 或 SELECT 陳述式之前明確復原。

您也不會收到 hello hello 錯誤 * 函式的輸出。

SQL 資料倉儲中 hello 的程式碼需要 toobe 稍有變更：

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

hello 預期的行為現在觀察到。 hello 交易中的 hello 錯誤並如預期般，hello 錯誤 * 函式提供的值。

所有已變更為該 hello `ROLLBACK` hello 的交易之前 toohappen hello 讀取 hello 錯誤的資訊在 hello`CATCH`區塊。

## <a name="errorline-function"></a>Error_Line() 函式
它也值得注意的是，SQL 資料倉儲不會實作或支援 hello error_line （） 函式。 如果此程式碼中有您需要 tooremove 它 toobe 符合 SQL 資料倉儲。 請改用您的程式碼中的查詢標籤 tooimplement 對等的功能。 請參閱 toohello[標籤][ LABEL]文件以取得更多詳細資料，這項功能。

## <a name="using-throw-and-raiserror"></a>使用 THROW 和 RAISERROR
THROW 是 hello 更現代實作引發 SQL 資料倉儲中的例外狀況，但也支援 RAISERROR。 有一些值得支付注意 toohowever 的一些差異。

* 使用者定義的數字不能在 hello 100000 150,000 範圍擲回的錯誤訊息
* RAISERROR 錯誤訊息固定為 50,000
* 不支援使用 sys.messages

## <a name="limitiations"></a>限制
SQL 資料倉儲確實有一些與 tootransactions 其他限制。

如下所示：

* 沒有分散式交易
* 不允許巢狀交易
* 不允許儲存點
* 沒有具名的交易
* 沒有標示的交易
* 使用者定義的交易內部不支援 DDL，例如 `CREATE TABLE`

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解最佳化交易，請參閱[交易的最佳作法][Transactions best practices]。  toolearn 有關其他 SQL 資料倉儲的最佳作法，請參閱[SQL 資料倉儲的最佳作法][SQL Data Warehouse best practices]。

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
