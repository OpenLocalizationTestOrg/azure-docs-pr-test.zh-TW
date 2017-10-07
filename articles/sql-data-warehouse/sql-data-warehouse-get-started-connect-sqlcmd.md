---
title: "aaaConnect tooAzure SQL 資料倉儲 sqlcmd |Microsoft 文件"
description: "使用 [sqlcmd] [sqlcmd] 命令列公用程式 tooconnect tooand 查詢 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a>使用 sqlcmd 連接 tooSQL 資料倉儲
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

使用[sqlcmd] [ sqlcmd]命令列公用程式 tooconnect tooand 查詢 Azure SQL 資料倉儲。  

## <a name="1-connect"></a>1.連線
tooget 入門[sqlcmd][sqlcmd]，開啟 hello 命令提示字元並輸入**sqlcmd**後面接著 hello SQL 資料倉儲資料庫的連接字串。 hello 連接字串需要下列參數的 hello:

* **伺服器 (-S):**伺服器 hello 形式`<`伺服器名稱`>`。.database.windows.net
* **資料庫 (-d)：** 資料庫名稱。
* **啟用引號識別碼 (-I):**引號識別項必須是啟用的 tooconnect tooa SQL 資料倉儲執行個體。

toouse SQL Server 驗證，您需要 tooadd hello 使用者名稱/密碼參數：

* **使用者 (-U):** hello 表單中的伺服器使用者`<`使用者`>`
* **密碼 (-P):** hello 使用者相關聯的密碼。

例如，您的連接字串可能會看起來像 hello 下列：

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

toouse Azure Active Directory 整合式驗證，您需要 tooadd hello Azure Active Directory 參數：

* **Azure Active Directory 驗證 (-G)：** 使用 Azure Active Directory 進行驗證

例如，您的連接字串可能會看起來像 hello 下列：

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> 您需要[啟用 Azure Active Directory 驗證](sql-data-warehouse-authentication.md)tooauthenticate 使用 Active Directory。
> 
> 

## <a name="2-query"></a>2.查詢
連線之後，您可以發出任何支援的 TRANSACT-SQL 陳述式，針對 hello 執行個體。  此範例會在互動模式中提交查詢。

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

這些下面的範例會示範如何使用 hello-Q 選項或以管線傳送 SQL toosqlcmd 批次模式來執行您的查詢。

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>後續步驟
請參閱[sqlcmd 文件][ sqlcmd]如需詳細資訊在 sqlcmd 中可用的 hello 選項的詳細資料。

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
