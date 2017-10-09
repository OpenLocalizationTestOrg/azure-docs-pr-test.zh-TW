---
title: "從 CSV aaaLoad 資料檔案儲存到 Azure SQL Database (bcp) |Microsoft 文件"
description: "若是較小的資料大小，會使用 bcp tooimport 資料至 Azure SQL Database。"
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>將資料從 CSV 載入 Azure SQL Database (一般檔案)
您可以使用從 CSV 檔案的 hello bcp 命令列公用程式 tooimport 資料至 Azure SQL Database。

## <a name="before-you-begin"></a>開始之前
### <a name="prerequisites"></a>必要條件
toocomplete hello 步驟在本文中，您需要：

* Azure SQL Database 邏輯伺服器和資料庫
* hello bcp 命令列公用程式安裝
* hello sqlcmd 命令列公用程式安裝

您可以下載 hello bcp 和 sqlcmd 公用程式從 hello [Microsoft Download Center][Microsoft Download Center]。

### <a name="data-in-ascii-or-utf-16-format"></a>ASCII 或 UTF-16 格式的資料
如果您嘗試本教學課程使用您自己的資料，您的資料需要 toouse hello ASCII 或因為 bcp 不支援 utf-8，utf-16 編碼方式。 

## <a name="1-create-a-destination-table"></a>1.建立目的資料表
SQL Database 中的資料表定義為 hello 目的地資料表中。 hello hello 資料表中的資料行必須對應 toohello 每一個資料列的資料檔案。

toocreate 資料表中，開啟命令提示字元，並使用 sqlcmd.exe toorun hello 下列命令：

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
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

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3.將資料載入 hello
tooload hello 資料，開啟命令提示字元，並執行下列命令，為伺服器名稱、 資料庫名稱、 使用者名稱和密碼的 hello 值取代您自己的資訊 hello。

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

使用此資料已載入正確的命令 tooverify hello

```bcp
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

## <a name="next-steps"></a>後續步驟
toomigrate SQL Server 資料庫，請參閱[SQL Server 資料庫移轉](sql-database-cloud-migrate.md)。

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
