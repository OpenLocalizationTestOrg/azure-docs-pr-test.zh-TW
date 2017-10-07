---
title: "aaaConnect tooAzure 使用 PHP PostgreSQL 資料庫 |Microsoft 文件"
description: "本快速入門會提供您可以使用 tooconnect 和 PostgreSQL 查詢從 Azure 資料庫的資料的 PHP 程式碼範例。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Azure PostgreSQL 資料庫： 使用 PHP tooconnect 和查詢資料
本快速入門示範如何使用 PostgreSQL 資料庫的 tooconnect tooan Azure [PHP](http://php.net/manual/intro-whatis.php)應用程式。 它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。 本文假設您熟悉開發使用 PHP，但是，您就可以新增 tooworking Azure PostgreSQL 資料庫。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [建立 DB - 入口網站](quickstart-create-server-database-portal.md)
- [建立 DB - Azure CLI](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>安裝 PHP
在自己的伺服器上安裝 PHP，或建立 Azure [Web 應用程式](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) (包括 PHP)。

### <a name="windows"></a>Windows
- 下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://windows.php.net/download#php-7.1)
- 安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.windows.php)進一步的組態
- hello 程式碼會使用 hello **pgsql** hello 的 PHP 安裝中包含的類別 (ext/php_pgsql.dll)。 
- 啟用的 hello **pgsql**延伸模組 來編輯 hello php.ini 組態檔通常位於`C:\Program Files\PHP\v7.1\php.ini`。 hello 設定檔應內嵌於 hello 文字`extension=php_pgsql.so`。 如果未顯示，新增 hello 文字，並儲存 hello 檔案。 如果 hello 文字，以分號前置詞，但標記為註文字取消註解 hello 藉由移除 hello 分號。

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- 下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://php.net/downloads.php) 
- 安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.unix.php)進一步的組態
- hello 程式碼會使用 hello **pgsql**類別 (php_pgsql.so)。 透過執行 `sudo apt-get install php-pgsql` 來進行安裝。
- 啟用的 hello **pgsql**延伸模組 來編輯 hello`/etc/php/7.0/mods-available/pgsql.ini`組態檔。 hello 設定檔應內嵌於 hello 文字`extension=php_pgsql.so`。 如果未顯示，新增 hello 文字，並儲存 hello 檔案。 如果 hello 文字，以分號前置詞，但標記為註文字取消註解 hello 藉由移除 hello 分號。

### <a name="macos"></a>MacOS
- 下載 [PHP 7.1.4 版本](http://php.net/downloads.php)
- 安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.macosx.php)進一步的組態

## <a name="get-connection-information"></a>取得連線資訊
取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**mypgserver 20170401**。
3. 按一下伺服器名稱，hello **mypgserver 20170401**。
4. 選取 hello 伺服器**概觀**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-php/1-connection-string.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。

## <a name="connect-and-create-a-table"></a>連線及建立資料表
使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式，後面接著**INSERT INTO** hello 資料表的 SQL 陳述式 tooadd 資料列。

hello 的程式碼呼叫方法[pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 資料庫。 然後它會呼叫方法[pg_query()](http://php.net/manual/en/function.pg-query.php)多次 toorun 數個命令，並[pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 詳細說明，如果每次時發生錯誤。 然後它會呼叫方法[pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 連線。

取代 hello `$host`， `$database`， `$user`，和`$password`參數以您自己的值。 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a>讀取資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。 

 hello 的程式碼呼叫方法[pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 資料庫。 然後它會呼叫方法[pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT 命令，在結果集中，保留 hello 結果和[pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 詳細說明，如果發生錯誤。  tooread hello 的結果集，方法[pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php)陣列中每個資料列和 hello 資料列擷取資料之後，在迴圈中，呼叫`$row`，且每個陣列的每個位置中的資料行的一個資料值。  toofree hello 的結果集，方法[pg_free_result()](http://php.net/manual/en/function.pg-free-result.php)呼叫。 然後它會呼叫方法[pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 連線。

取代 hello `$host`， `$database`， `$user`，和`$password`參數以您自己的值。 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。

hello 的程式碼呼叫方法[pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 資料庫。 然後它會呼叫方法[pg_query()](http://php.net/manual/en/function.pg-query.php) toorun 命令和[pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 詳細說明，如果發生錯誤。 然後它會呼叫方法[pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 連線。

取代 hello `$host`， `$database`， `$user`，和`$password`參數以您自己的值。 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。 

 hello 的程式碼呼叫方法[pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect 太 Azure PostgreSQL 資料庫。 然後它會呼叫方法[pg_query()](http://php.net/manual/en/function.pg-query.php) toorun 命令和[pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 詳細說明，如果發生錯誤。 然後它會呼叫方法[pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 連線。

取代 hello `$host`， `$database`， `$user`，和`$password`參數以您自己的值。 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [使用匯出和匯入來移轉資料庫](./howto-migrate-using-export-and-import.md)
