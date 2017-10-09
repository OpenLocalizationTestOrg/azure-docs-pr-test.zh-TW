---
title: "aaaLoad 範例資料插入 SQL 資料倉儲 |Microsoft 文件"
description: "將範例資料載入 SQL 資料倉儲"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a>將範例資料載入 SQL 資料倉儲
請遵循這些簡單的步驟 tooload 和查詢 hello Adventure Works 範例資料庫。 這些指令碼會先使用 sqlcmd toorun SQL 將會建立資料表和檢視表。 一旦已建立資料表，hello 指令碼會使用 bcp tooload 資料。  如果您還沒有 sqlcmd 和 bcp 安裝，請遵循這些連結太[安裝 bcp] [ install bcp]和太[安裝 sqlcmd][install sqlcmd]。

## <a name="load-sample-data"></a>載入範例資料
1. 下載 hello [SQL 資料倉儲的 Adventure Works 範例指令碼][ Adventure Works Sample Scripts for SQL Data Warehouse] zip 檔案。
2. 解壓縮 hello 檔案從本機電腦上的已下載之 zip tooa 目錄。
3. 編輯 hello 解壓縮檔案 aw_create.bat，並設定下列在 hello hello 檔案頂端找到變數 hello。  為確定 tooleave hello"="hello 參數之間沒有空格。  以下是您可能會想看看如何編輯的範例。
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. 從 Windows 命令提示字元中，執行編輯的 hello aw_create.bat。  請確定您是在您儲存 aw_create.bat 您編輯的過的 hello 目錄。
   此指令碼將...
   
   * 卸除任何 Adventure Works 資料表或任何已存在資料庫中的檢視表
   * 建立 hello Adventure Works 資料表和檢視表
   * 使用 bcp 載入每個 Adventure Works 資料表
   * 驗證 hello Adventure Works 的每個資料表的資料列計數
   * 收集每個 Adventure Works 資料表之所有資料行上的統計資料

## <a name="query-sample-data"></a>查詢範例資料
一旦已經將某些範例資料載入您的 SQL 資料倉儲中，就可以快速地執行幾個查詢。  hello 中所述，toorun 查詢時，連接 tooyour 新建 Adventure Works 資料庫中使用 Visual Studio 和 SSDT 中，Azure SQL DW [Visual Studio 中的查詢][ query with Visual Studio]文件。

簡單的範例選取陳述式 tooget hello 員工的所有 hello 資訊：

```sql
SELECT * FROM DimEmployee;
```

每一天所有銷售使用建構，例如 GROUP BY toolook hello 總量在更複雜的查詢範例：

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

SELECT 與 WHERE 子句 toofilter 出訂單在特定日期之前的範例：

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

SQL 資料倉儲幾乎支援所有 SQL Server 支援的 T-SQL 建構。  所有的差異都記錄在[移轉程式碼][migrate code]文件中。

## <a name="next-steps"></a>後續步驟
既然您已有機會 tootry 某些查詢的範例資料，請參閱如何太[開發][develop]，[載入][load]，或[移轉][ migrate] tooSQL 資料倉儲。

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
