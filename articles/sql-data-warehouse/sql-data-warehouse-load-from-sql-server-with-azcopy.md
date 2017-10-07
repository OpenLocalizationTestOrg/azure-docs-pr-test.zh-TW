---
title: "aaaLoad 資料從 SQL Server 到 Azure SQL 資料倉儲 (PolyBase) |Microsoft 文件"
description: "您可以使用 bcp tooexport 資料從 SQL Server tooflat 檔案、 AZCopy tooimport 資料 tooAzure blob 儲存體和 PolyBase tooingest hello 資料至 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a>將資料從 SQL Server 載入 Azure SQL 資料倉儲 (AZCopy)
使用 bcp 並從 SQL Server tooAzure blob 儲存體的 AZCopy 命令列公用程式 tooload 資料。 再使用 PolyBase 或 Azure Data Factory tooload hello 資料到 Azure SQL 資料倉儲。 

## <a name="prerequisites"></a>必要條件
在本教學課程 toostep，您需要：

* SQL 資料倉儲資料庫
* hello bcp 命令列公用程式安裝
* hello SQLCMD 命令列公用程式安裝

> [!NOTE]
> 您可以下載 hello bcp 和 sqlcmd 公用程式從 hello [Microsoft Download Center][Microsoft Download Center]。
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>將資料匯入 SQL 資料倉儲
在本教學課程中，您將 Azure SQL 資料倉儲中建立資料表並 hello 資料表將資料匯入。

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>步驟 1：在 Azure SQL 資料倉儲中建立資料表
從命令提示字元中，使用下列查詢 toocreate 資料表執行個體上的 sqlcmd toorun hello:

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

> [!NOTE]
> 請參閱[資料表概觀][ Table Overview]或[CREATE TABLE 語法][ CREATE TABLE syntax]如需有關 SQL 資料倉儲與 hello 上建立資料表 hello WITH 子句中可用的選項。
> 
> 

### <a name="step-2-create-a-source-data-file"></a>步驟 2：建立來源資料檔
開啟 [記事本] 及複製 hello 下列行資料到新的文字檔，然後儲存此檔案 tooyour 本機暫存目錄中，C:\Temp\DimDate2.txt。

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

> [!NOTE]
> 它是重要的 tooremember 該 bcp.exe 不支援 hello utf-8 的檔案編碼方式。 使用 bcp.exe 時，請使用 ASCII 檔案或 UTF-16 編碼的檔案。
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>步驟 3： 連接及匯入 hello 資料
您可以使用 bcp，來連接並使用下列命令並將 hello 值做為適當的 hello hello 資料匯入項目：

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

您可以確認資料已由執行下列查詢中使用 sqlcmd hello 載入的 hello:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

這應該會傳回下列結果 hello:

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

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>步驟 4：建立新載入資料的統計資料
Azure 資料倉儲尚未支援自動建立或自動更新統計資料。 在順序 tooget hello 達到最佳效能從您的查詢，請務必在所有資料表的所有資料行上建立統計資料，hello 第一次載入之後或 hello 資料會發生任何大量變更。 統計資料的詳細說明，請參閱 hello[統計資料][ Statistics] hello 開發一組主題中的主題。 以下是 toocreate hello 資料表的統計資料如何載入在此範例中的快速範例

執行 hello sqlcmd 提示字元中的下列 CREATE STATISTICS 陳述式：

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>從 SQL 資料倉儲匯出資料
在本教學課程中，您將從 Azure SQL 資料倉儲中的資料表建立資料檔案。 我們會將 hello 資料前面 tooa 稱為 DimDate2_export.txt 新資料檔案所建立的匯出。

### <a name="step-1-export-hello-data"></a>步驟 1： 匯出 hello 資料
使用 hello bcp 公用程式，您可以連接及匯出資料使用下列命令並將 hello 值做為適當的 hello:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
您可以確認資料已正確開啟 hello 新檔案匯出的 hello。 hello 檔案中的 hello 資料應符合下列的 hello 文字：

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

> [!NOTE]
> 因為分散式系統的 toohello 本質，hello 資料順序可能不是相同 hello 跨 SQL 資料倉儲資料庫。 另一個選項是 toouse hello **queryout**函式的 bcp toowrite 查詢擷取而不匯出 hello 整份資料表。
> 
> 

## <a name="next-steps"></a>後續步驟
如需載入的概觀，請參閱[將資料載入 SQL 資料倉儲][Load data into SQL Data Warehouse]。
如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。

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
