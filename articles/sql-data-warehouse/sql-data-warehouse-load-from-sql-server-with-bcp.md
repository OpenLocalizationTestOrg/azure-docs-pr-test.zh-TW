---
title: "aaaLoad 資料從 SQL Server 到 Azure SQL 資料倉儲 (bcp) |Microsoft 文件"
description: "對於小型資料大小，使用 bcp tooexport 資料從 SQL Server tooflat 檔案和資料匯入 hello 直接在 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>將資料從 SQL Server 載入 Azure SQL 資料倉儲 (一般檔案)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

對於小型資料集，您可以使用 hello bcp 命令列公用程式 tooexport 資料從 SQL Server，並再將其載入直接 tooAzure SQL 資料倉儲。

在本教學課程中，您將使用 bcp 來：

* 從 SQL Server 匯出的資料表，使用 hello bcp 命令 （或建立簡單的範例檔案）
* Hello 資料表匯入從一般檔案 tooSQL 資料倉儲。
* 建立 hello 載入資料的統計資料。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>開始之前
### <a name="prerequisites"></a>必要條件
在本教學課程 toostep，您需要：

* SQL 資料倉儲資料庫
* hello bcp 命令列公用程式安裝
* hello sqlcmd 命令列公用程式安裝

您可以下載 hello bcp 和 sqlcmd 公用程式從 hello [Microsoft Download Center][Microsoft Download Center]。

### <a name="data-in-ascii-or-utf-16-format"></a>ASCII 或 UTF-16 格式的資料
如果您嘗試本教學課程使用您自己的資料，您的資料需要 toouse hello ASCII 或因為 bcp 不支援 utf-8，utf-16 編碼方式。 

PolyBase 支援 UTF-8，但尚未支援 UTF-16。 請注意，是否您想要使用 PolyBase toocombine bcp 就會需要 tootransform hello 資料 tooUTF-8，從 SQL Server 匯出之後。 

## <a name="1-create-a-destination-table"></a>1.建立目的資料表
定義將 hello 負載 hello 目的地資料表的 SQL 資料倉儲中的資料表。 hello hello 資料表中的資料行必須對應 toohello 每一個資料列的資料檔案。

toocreate 資料表中，開啟命令提示字元，並使用 sqlcmd.exe toorun hello 下列命令：

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a>2.建立來源資料檔
開啟 [記事本] 及複製 hello 下列行資料到新的文字檔，然後儲存此檔案 tooyour 本機暫存目錄中，C:\Temp\DimDate2.txt。 此資料是 ASCII 格式。

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

（選擇性） tooexport 您自己的資料從 SQL Server 資料庫，開啟命令提示字元並執行下列命令的 hello。 使用您自己的資訊取代 TableName、ServerName、DatabaseName、Username 和 Password。

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3.將資料載入 hello
tooload hello 資料，開啟命令提示字元，並執行下列命令，為伺服器名稱、 資料庫名稱、 使用者名稱和密碼的 hello 值取代您自己的資訊 hello。

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

使用此資料已載入正確的命令 tooverify hello

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

hello 結果看起來應該像這樣：

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

## <a name="4-create-statistics"></a>4.建立統計資料
SQL 資料倉儲尚未支援自動建立或自動更新統計資料。 tooget hello 最佳查詢效能，很重要 toocreate 統計資料的所有資料表的所有資料行上 hello 第一次載入或之後 hello 資料會發生任何大量變更。 如需統計資料的詳細說明，請參閱[統計資料][Statistics]。 

Hello 執行的下列命令 toocreate 您載入新的資料表上的統計資料。

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5.從 SQL 資料倉儲匯出資料
玩看，您可以匯出只載入 SQL 資料倉儲從傳回的 hello 資料。  hello 命令 tooexport 完全 hello 與匯出從 SQL Server 相同。

不過，沒有 hello 結果上的差異。 因為 hello 資料會儲存 SQL 資料倉儲內的分散式位置中，當您匯出資料的每個計算節點將它寫入資料 toohello 輸出檔。 hello hello 輸出檔案中的 hello 資料順序是可能 toobe 不同 hello hello 中的資料順序 hello 輸入檔。

### <a name="export-a-table-and-compare-exported-results"></a>匯出資料表和比較匯出的結果
toosee hello 匯出的資料，開啟命令提示字元並執行此命令使用您自己的參數。 為 hello Azure 邏輯的 SQL Server 名稱。

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
您可以確認資料已正確開啟 hello 新檔案匯出的 hello。 hello 檔案中的 hello 資料應符合下列的 hello 文字，但可能會以不同的順序排序：

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-hello-results-of-a-query"></a>匯出 hello 查詢的結果
您可以使用 hello **queryout**函式的 bcp tooexport hello 查詢的結果，而不要匯出 hello 整份資料表。 

## <a name="next-steps"></a>後續步驟
如需載入的概觀，請參閱[將資料載入 SQL 資料倉儲][Load data into SQL Data Warehouse]。
如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。
如需有關在 SQL 資料倉儲上建立資料表的詳細資訊，請參閱[資料表概觀][Table Overview]或 [CREATE TABLE 語法][CREATE TABLE syntax]。

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
