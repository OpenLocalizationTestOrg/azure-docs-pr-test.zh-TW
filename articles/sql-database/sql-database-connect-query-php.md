---
title: "Azure SQL Database 的 aaaUse PHP tooquery |Microsoft 文件"
description: "本主題說明如何 toouse PHP toocreate 連接 tooan Azure SQL Database 和查詢使用 TRANSACT-SQL 陳述式的程式。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 4e71db4a-a 22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 5fc49dcc42ab07cc1bec554be39bdf08dbd6f75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-php-tooquery-an-azure-sql-database"></a>使用 PHP tooquery Azure SQL database

本快速入門教學課程示範如何 toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate 程式 tooconnect tooan Azure SQL 資料庫，將 TRANSACT-SQL 陳述式 tooquery 資料。

## <a name="prerequisites"></a>必要條件

toocomplete 此快速入門教學課程，請確定您擁有 hello 下列：

- Azure SQL Database。 本快速入門會使用 hello 資源建立在其中一個這些快速入門： 

   - [建立 DB - 入口網站](sql-database-get-started-portal.md)
   - [建立 DB - CLI](sql-database-get-started-cli.md)
   - [建立 DB - PowerShell](sql-database-get-started-powershell.md)

- A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。

- 您已安裝適用於您作業系統的 PHP 和相關軟體。

    - **MacOS**： 安裝 Homebrew 和 PHP，依序安裝 hello ODBC 驅動程式和 SQLCMD 和 hello PHP Driver for SQL Server。 請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/)。
    - **Ubuntu**： 安裝 PHP 和其他必要的封裝，然後再安裝 hello PHP Driver for SQL Server。 請參閱[步驟 1.2 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/)。
    - **Windows**： 安裝 hello 最新版本的 PHP 的 IIS Express，hello 最新版本的 IIS Express、 Chocolatey、 hello ODBC 驅動程式和 SQLCMD 中的 SQL Server 的 Microsoft 驅動程式。 請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/)。    

## <a name="sql-server-connection-information"></a>SQL Server 連線資訊

收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。 您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 
3. 在 hello**概觀**頁面為您的資料庫檢閱 hello 完整伺服器名稱 hello 下列影像所示。 您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. 如果忘記您的伺服器登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。     
    
## <a name="insert-code-tooquery-sql-database"></a>插入程式碼 tooquery SQL 資料庫

1. 在您慣用的文字編輯器中，建立新的檔案 **sqltest.php**。  

2. 以下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼的 hello 取代 hello 內容。

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes hello connection
   $conn = sqlsrv_connect($serverName, $connectionOptions);
   $tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
           FROM [SalesLT].[ProductCategory] pc
           JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid";
   $getResults= sqlsrv_query($conn, $tsql);
   echo ("Reading data from table" . PHP_EOL);
   if ($getResults == FALSE)
       echo (sqlsrv_errors());
   while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
   }
   sqlsrv_free_stmt($getResults);
   ?>
   ```

## <a name="run-hello-code"></a>執行 hello 程式碼

1. 在 hello 命令提示字元中執行下列命令的 hello:

   ```php
   php sqltest.php
   ```

2. 請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。

## <a name="next-steps"></a>後續步驟
- [設計您的第一個 Azure SQL Database](sql-database-design-first-database.md)
- [Microsoft PHP Drivers for SQL Server](https://github.com/Microsoft/msphpsql/)
- [回報問題或發問](https://github.com/Microsoft/msphpsql/issues)
