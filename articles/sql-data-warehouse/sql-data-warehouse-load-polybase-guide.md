---
title: "在 SQL 資料倉儲中使用 PolyBase aaaGuide |Microsoft 文件"
description: "在 SQL 資料倉儲案例中使用 PolyBase 的指導方針和建議。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>在 SQL 資料倉儲中使用 PolyBase 的指南
本指南提供在 SQL 資料倉儲中使用 PolyBase 的實用資訊。

tooget 啟動，請參閱 hello[載入資料，使用 PolyBase] [ Load data with PolyBase]教學課程。

## <a name="rotating-storage-keys"></a>替換儲存體金鑰
從時間 tootime 您會想 toochange hello 存取金鑰 tooyour blob 儲存體，基於安全性考量。

hello 最簡潔的方式 tooperform 這項工作是 toofollow 稱為 「 輪替 hello 金鑰 」 的程序。 您可能已經注意到您在 blob 儲存體帳戶有兩個儲存體金鑰。 如此一來您就可以轉換

替換 Azure 儲存體帳戶金鑰的程序只需要簡單的三個步驟

1. 建立第二個 hello 次要儲存體存取金鑰為基礎的資料庫範圍認證
2. 建立以新的認證為基礎的第二個外部資料來源
3. 卸除和建立 hello 指向 toohello 新的外部資料來源的外部資料表。

當您在移轉所有外部資料表 toohello 新外部資料來源，然後您可以執行 hello 會清除工作：

1. 卸除第一個外部資料來源
2. 卸除第一個資料庫範圍認證根據 hello 主要儲存體存取金鑰
3. 登入 Azure，並在下一次重新產生供 hello hello 主要存取金鑰

## <a name="query-azure-blob-storage-data"></a>查詢 Azure blob 儲存體資料
針對外部資料表進行查詢只使用 hello 資料表名稱，如同它是關聯式資料表。

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> 外部資料表上的查詢可能會失敗並 hello 錯誤*"查詢已中止--從外部來源讀取時達到 hello 拒絕臨界值上限 」*。 這表示您的外部資料包含 *「錯誤」* 記錄。 資料錄會被視為 '中途'，如果 hello 實際的資料型別/資料行數目不符合 hello 的 hello 外部資料表的資料行定義，或 hello 資料不符合 toohello 指定外部檔案格式。 toofix，確定您的外部資料表及外部檔案格式定義是否正確，且您的外部資料符合 toothese 定義。 如果外部資料記錄的子集有問題，您可以選擇 tooreject 這些記錄您查詢的使用中建立外部資料表 DDL hello 拒絕選項。
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>從 Azure blob 儲存體載入資料
這個範例會從 Azure blob 儲存體 tooSQL 資料倉儲資料庫載入資料。

將資料儲存在直接移除 hello 查詢的資料傳輸時間。 儲存資料與資料行存放區索引可提升 too10x 總的分析查詢的查詢效能。

這個範例會使用 hello CREATE TABLE AS SELECT 陳述式 tooload 資料。 hello 新資料表會繼承命名 hello 查詢中的 hello 資料行。 它會從 hello 外部資料表定義繼承 hello 這些資料行資料類型。

CREATE TABLE AS SELECT 是高 」 高效能 TRANSACT-SQL 陳述式將平行 tooall hello hello 資料載入計算節點 SQL 資料倉儲。  它原本針對 hello 大量平行處理 (MPP) 引擎 Analytics Platform System 所開發並已在 SQL 資料倉儲。

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

請參閱 [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)]。

## <a name="create-statistics-on-newly-loaded-data"></a>建立新載入資料的統計資料
Azure 資料倉儲尚未支援自動建立或自動更新統計資料。  在順序 tooget hello 達到最佳效能從您的查詢，請務必在所有資料表的所有資料行上建立統計資料，hello 第一次載入之後或 hello 資料會發生任何大量變更。  統計資料的詳細說明，請參閱 hello[統計資料][ Statistics] hello 開發一組主題中的主題。  以下是 toocreate hello 資料表的統計資料如何載入在此範例中的快速範例。

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>匯出資料 tooAzure blob 儲存體
本節說明如何從 SQL 資料倉儲 tooAzure tooexport 資料 blob 儲存體。 此範例使用 CREATE EXTERNAL TABLE AS SELECT 這是高高效能 TRANSACT-SQL 陳述式 tooexport hello 資料以平行方式從所有 hello 計算節點。

hello 下列範例會建立外部資料表 Weblogs2014 使用資料行定義和資料從 dbo。網誌資料表。 hello 外部資料表定義會儲存在 SQL 資料倉儲，而 hello hello SELECT 陳述式的結果匯出的 toohello"/ 封存/log2014 /"hello hello 資料來源所指定的 blob 容器下的目錄。 hello 資料會匯出 hello 指定的文字檔案格式。

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>隔離載入使用者
通常會需要 toohave 可以將資料載入 SQL DW 的多個使用者。 因為 hello [CREATE TABLE AS SELECT (TRANSACT-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)]需要控制 」 權限的 hello 資料庫您會得到多名使用者具有控制存取透過所有結構描述。 toolimit，您可以使用 hello 拒絕控制陳述式。

範例：考慮將資料庫結構描述 schema_A 用於 dept A 以及 schema_B 用於 dept B，讓資料庫使用者 user_A 和 user_B 個別成為 dept A 及 B 中載入的 PolyBase 之使用者。 這兩個使用者皆已獲得 CONTROL 資料庫權限。
A 和 B 現在鎖定使用拒絕其結構描述的結構描述的 hello 建立者：

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 與這個項目，user_A 和 user_B 應該現在會被鎖定 hello 從其他部門的結構描述。
 


## <a name="next-steps"></a>後續步驟
toolearn 有關移動資料 tooSQL 資料倉儲的詳細資訊，請參閱 「 hello[資料移轉概觀][data migration overview]。

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
