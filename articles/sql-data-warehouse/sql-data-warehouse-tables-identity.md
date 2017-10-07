---
title: "aaaCreate surrogate 索引鍵使用的識別 |Microsoft 文件"
description: "了解 toouse 識別 toocreate 代理程式資料表上的索引鍵。"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>使用 IDENTITY 建立 Surrogate 索引鍵
> [!div class="op_single_selector"]
> * [概觀][Overview]
> * [資料類型][Data Types]
> * [散發][Distribute]
> * [索引][Index]
> * [資料分割][Partition]
> * [統計資料][Statistics]
> * [暫存][Temporary]
> * [身分識別][Identity]
> 
> 

它們在設計資料倉儲模型時，許多資料建模者喜歡 toocreate surrogate 索引鍵，其資料表上。 您可以使用 hello 識別屬性 tooachieve 此目標只是和有效率的方法而不會影響載入效能。 

## <a name="get-started-with-identity"></a>開始使用 IDENTITY
您可以將資料表定義為具有 hello IDENTITY 屬性，當您初次建立 hello 資料表使用 「 類似 toohello 後面的陳述式的語法：

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

然後您可以使用`INSERT..SELECT`toopopulate hello 資料表。

## <a name="behavior"></a>行為
hello 識別屬性是設計出 tooscale 跨所有 hello 分佈，而不會影響載入效能 hello 資料倉儲中。 因此，身分識別的 hello 實作會導向達成這些目標。 本章節強調 hello 細節的 hello 實作 toohelp 您瞭解這些更完整。  

### <a name="allocation-of-values"></a>值的配置
hello IDENTITY 屬性並不保證 hello 順序中的 hello 配置 surrogate 值，其會反映的 SQL Server 和 Azure SQL Database 的 hello 行為。 不過，在 Azure SQL 資料倉儲中，更唸成 hello 缺乏保證。 

hello 下列範例會示範：

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

在上述範例中的 hello，兩個資料列處於發佈 1。 hello 第一個資料列資料行有 hello surrogate 值為 1 `C1`，而且 hello 第二個資料列 61 hello surrogate 值。 兩個這些值所產生的 hello IDENTITY 屬性。 不過，不是連續的 hello 值 hello 配置。 這是設計的行為。

### <a name="skewed-data"></a>偏斜資料 
hello hello 資料類型的值範圍會平均分散 hello 分佈。 如果資料的誤用因分散式的資料表，然後 hello 可用 toohello 資料型別可能會耗盡不當的值範圍。 比方說，如果所有的 hello 資料最後會在單一通訊中，然後有效 hello 資料表有存取 tooonly 一個 sixtieth hello hello 資料類型值。 基於這個理由，hello IDENTITY 屬性太有限`INT`和`BIGINT`資料型別。

### <a name="selectinto"></a>SELECT..INTO
到新的資料表選取現有的身分識別資料行時，hello 新資料行就會繼承 hello IDENTITY 屬性，除非其中一個 hello 下列條件成立：
- hello SELECT 陳述式包含聯結。
- 多個 SELECT 陳述式使用 UNION 進行聯結。
- hello 身分識別資料行被列一次以上 hello 選取清單中。
- hello 身分識別資料行是運算式的一部分。
    
如果任何一個條件為 true，hello 資料行建立成 NOT NULL 而非繼承 hello IDENTITY 屬性。

### <a name="create-table-as-select"></a>CREATE TABLE AS SELECT
建立資料表 AS 選取 (CTAS) 如下所示 hello 相同的 SQL Server 行為，以便進行 SELECT 記錄...到。 不過，您無法 hello hello 資料行定義中指定的 IDENTITY 屬性`CREATE TABLE`hello 陳述式的一部分。 您也無法使用 hello IDENTITY 函數在 hello `SELECT` hello CTAS 的一部分。 toopopulate 資料表，您需要 toouse `CREATE TABLE` toodefine hello 表格後面`INSERT..SELECT`toopopulate 它。

## <a name="explicitly-insert-values-into-an-identity-column"></a>明確地將值插入 IDENTITY 資料行 
SQL 資料倉儲支援 `SET IDENTITY_INSERT <your table> ON|OFF` 語法。 您可以使用此語法 tooexplicitly 插入值到 hello 識別資料行。

許多資料建模者像 toouse 預先定義的負值特定值維度中的資料列。 例如，-1 hello 或 「 未知的成員 」 資料列。 

hello 下一個指令碼會示範 tooexplicitly 利用 SET IDENTITY_INSERT 所新增的這個資料列：

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>使用 IDENTITY 將資料載入資料表

hello 的 hello IDENTITY 屬性的目前狀態有某些含意 tooyour 資料載入程式碼。 本節會重點說明使用 IDENTITY 將資料載入資料表的一些基本模式。 

### <a name="load-data-with-polybase"></a>使用 PolyBase 載入資料
tooload 資料到資料表和產生 surrogate 索引鍵使用的識別、 建立 hello 資料表，然後使用 INSERT...SELECT 或 INSERT...值 tooperform hello 負載。

hello 下列範例會反白顯示 hello 基本模式：
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> 不可能 toouse`CREATE TABLE AS SELECT`目前時將資料載入資料表之 IDENTITY 資料行。
> 

如需有關使用 hello 大量複製程式 (BCP) 工具來載入資料的詳細資訊，請參閱下列文章 hello:

- [使用 PolyBase 載入][]
- [PolyBase 最佳做法][]

### <a name="load-data-with-bcp"></a>使用 BCP 載入資料
BCP 就會是命令列工具，您可以使用 tooload 資料到 SQL 資料倉儲。 其中一個參數 (-E) 將資料載入資料表之 IDENTITY 資料行時，控制項 hello BCP 的行為。 

指定-E 時，識別持有 hello hello 資料行的輸入檔中的 hello 值都會保留下來。 如果-E 是*不*指定，則會忽略此資料行中的 hello 值。 如果不包含 hello 識別資料行，則 hello 資料被載入以正常的。 hello 值會產生根據 toohello 遞增和種子原則 hello 屬性。

如需有關使用 BCP 來載入資料的詳細資訊，請參閱下列文章 hello:

- [使用 BCP 載入][]
- [MSDN 中的 BCP][]

## <a name="catalog-views"></a>目錄檢視
SQL 資料倉儲支援 hello`sys.identity_columns`目錄檢視。 這個檢視可以使用的 tooidentify 具有 hello IDENTITY 屬性的資料行。

toohelp 深入了解 hello 資料庫結構描述，這個範例會示範如何 toointegrate`sys.identity_columns`與其他系統目錄檢視：

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>限制
hello 識別屬性不能在下列案例的 hello:
- 其中 hello 資料行資料類型不是 INT 或 BIGINT
- 其中 hello 資料行也是 hello 散發索引鍵
- Hello 資料表所在的外部資料表 

SQL 資料倉儲中不支援下列相關函式的 hello:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>工作

本節提供範例程式碼，當您使用識別欄位時，您可以使用 tooperform 一般工作。

> [!NOTE] 
> 資料行 C1 是在下列工作的所有 hello hello 身分識別。
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>找到資料表的配置 hello 最高值
使用 hello`MAX()`函式的分散式資料表配置 toodetermine hello 最大值：

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>尋找 hello 種子和遞增值 hello IDENTITY 屬性
您可以使用 hello 目錄檢視 toodiscover hello 識別遞增和種子組態值的資料表使用下列查詢的 hello: 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>後續步驟

* toolearn 進一步了解開發資料表，請參閱[資料表概觀][Overview]，[資料表的資料型別][Data Types]，[散發資料表][ Distribute]，[索引資料表][Index]，[分割資料表][Partition]，和[暫存資料表][Temporary]。 
* 如需最佳做法的詳細資訊，請參閱 [SQL 資料倉儲最佳做法][SQL Data Warehouse Best Practices]。  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[使用 bcp 載入]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[使用 PolyBase 載入]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[PolyBase 最佳做法]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[MSDN 中的 bcp]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
