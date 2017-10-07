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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="b01b6-103">Azure PostgreSQL 資料庫： 使用 PHP tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="b01b6-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="b01b6-104">本快速入門示範如何使用 PostgreSQL 資料庫的 tooconnect tooan Azure [PHP](http://php.net/manual/intro-whatis.php)應用程式。</span><span class="sxs-lookup"><span data-stu-id="b01b6-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="b01b6-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="b01b6-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="b01b6-106">本文假設您熟悉開發使用 PHP，但是，您就可以新增 tooworking Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b01b6-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b01b6-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="b01b6-107">Prerequisites</span></span>
<span data-ttu-id="b01b6-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="b01b6-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b01b6-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="b01b6-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="b01b6-110">建立 DB - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b01b6-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="b01b6-111">安裝 PHP</span><span class="sxs-lookup"><span data-stu-id="b01b6-111">Install PHP</span></span>
<span data-ttu-id="b01b6-112">在自己的伺服器上安裝 PHP，或建立 Azure [Web 應用程式](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) (包括 PHP)。</span><span class="sxs-lookup"><span data-stu-id="b01b6-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="b01b6-113">Windows</span><span class="sxs-lookup"><span data-stu-id="b01b6-113">Windows</span></span>
- <span data-ttu-id="b01b6-114">下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="b01b6-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="b01b6-115">安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.windows.php)進一步的組態</span><span class="sxs-lookup"><span data-stu-id="b01b6-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="b01b6-116">hello 程式碼會使用 hello **pgsql** hello 的 PHP 安裝中包含的類別 (ext/php_pgsql.dll)。</span><span class="sxs-lookup"><span data-stu-id="b01b6-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="b01b6-117">啟用的 hello **pgsql**延伸模組 來編輯 hello php.ini 組態檔通常位於`C:\Program Files\PHP\v7.1\php.ini`。</span><span class="sxs-lookup"><span data-stu-id="b01b6-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="b01b6-118">hello 設定檔應內嵌於 hello 文字`extension=php_pgsql.so`。</span><span class="sxs-lookup"><span data-stu-id="b01b6-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="b01b6-119">如果未顯示，新增 hello 文字，並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b01b6-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="b01b6-120">如果 hello 文字，以分號前置詞，但標記為註文字取消註解 hello 藉由移除 hello 分號。</span><span class="sxs-lookup"><span data-stu-id="b01b6-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="b01b6-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b01b6-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="b01b6-122">下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="b01b6-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="b01b6-123">安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.unix.php)進一步的組態</span><span class="sxs-lookup"><span data-stu-id="b01b6-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="b01b6-124">hello 程式碼會使用 hello **pgsql**類別 (php_pgsql.so)。</span><span class="sxs-lookup"><span data-stu-id="b01b6-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="b01b6-125">透過執行 `sudo apt-get install php-pgsql` 來進行安裝。</span><span class="sxs-lookup"><span data-stu-id="b01b6-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="b01b6-126">啟用的 hello **pgsql**延伸模組 來編輯 hello`/etc/php/7.0/mods-available/pgsql.ini`組態檔。</span><span class="sxs-lookup"><span data-stu-id="b01b6-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="b01b6-127">hello 設定檔應內嵌於 hello 文字`extension=php_pgsql.so`。</span><span class="sxs-lookup"><span data-stu-id="b01b6-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="b01b6-128">如果未顯示，新增 hello 文字，並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b01b6-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="b01b6-129">如果 hello 文字，以分號前置詞，但標記為註文字取消註解 hello 藉由移除 hello 分號。</span><span class="sxs-lookup"><span data-stu-id="b01b6-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="b01b6-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="b01b6-130">MacOS</span></span>
- <span data-ttu-id="b01b6-131">下載 [PHP 7.1.4 版本](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="b01b6-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="b01b6-132">安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.macosx.php)進一步的組態</span><span class="sxs-lookup"><span data-stu-id="b01b6-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b01b6-133">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="b01b6-133">Get connection information</span></span>
<span data-ttu-id="b01b6-134">取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b01b6-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="b01b6-135">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="b01b6-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b01b6-136">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b01b6-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b01b6-137">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="b01b6-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="b01b6-138">按一下伺服器名稱，hello **mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="b01b6-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="b01b6-139">選取 hello 伺服器**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="b01b6-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="b01b6-140">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="b01b6-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b01b6-141">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="b01b6-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="b01b6-142">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b01b6-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="b01b6-143">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="b01b6-143">Connect and create a table</span></span>
<span data-ttu-id="b01b6-144">使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式，後面接著**INSERT INTO** hello 資料表的 SQL 陳述式 tooadd 資料列。</span><span class="sxs-lookup"><span data-stu-id="b01b6-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="b01b6-145">hello 的程式碼呼叫方法[pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b01b6-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="b01b6-146">然後它會呼叫方法[pg_query()](http://php.net/manual/en/function.pg-query.php)多次 toorun 數個命令，並[pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 詳細說明，如果每次時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b01b6-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="b01b6-147">然後它會呼叫方法[pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b01b6-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="b01b6-148">取代 hello `$host`， `$database`， `$user`，和`$password`參數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="b01b6-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="b01b6-149">讀取資料</span><span class="sxs-lookup"><span data-stu-id="b01b6-149">Read data</span></span>
<span data-ttu-id="b01b6-150">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b01b6-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="b01b6-151">hello 的程式碼呼叫方法[pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b01b6-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="b01b6-152">然後它會呼叫方法[pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT 命令，在結果集中，保留 hello 結果和[pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 詳細說明，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b01b6-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="b01b6-153">tooread hello 的結果集，方法[pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php)陣列中每個資料列和 hello 資料列擷取資料之後，在迴圈中，呼叫`$row`，且每個陣列的每個位置中的資料行的一個資料值。</span><span class="sxs-lookup"><span data-stu-id="b01b6-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="b01b6-154">toofree hello 的結果集，方法[pg_free_result()](http://php.net/manual/en/function.pg-free-result.php)呼叫。</span><span class="sxs-lookup"><span data-stu-id="b01b6-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="b01b6-155">然後它會呼叫方法[pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b01b6-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="b01b6-156">取代 hello `$host`， `$database`， `$user`，和`$password`參數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="b01b6-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="b01b6-157">更新資料</span><span class="sxs-lookup"><span data-stu-id="b01b6-157">Update data</span></span>
<span data-ttu-id="b01b6-158">使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b01b6-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="b01b6-159">hello 的程式碼呼叫方法[pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b01b6-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="b01b6-160">然後它會呼叫方法[pg_query()](http://php.net/manual/en/function.pg-query.php) toorun 命令和[pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 詳細說明，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b01b6-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="b01b6-161">然後它會呼叫方法[pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b01b6-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="b01b6-162">取代 hello `$host`， `$database`， `$user`，和`$password`參數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="b01b6-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="b01b6-163">刪除資料</span><span class="sxs-lookup"><span data-stu-id="b01b6-163">Delete data</span></span>
<span data-ttu-id="b01b6-164">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b01b6-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="b01b6-165">hello 的程式碼呼叫方法[pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect 太 Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b01b6-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="b01b6-166">然後它會呼叫方法[pg_query()](http://php.net/manual/en/function.pg-query.php) toorun 命令和[pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello 詳細說明，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b01b6-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="b01b6-167">然後它會呼叫方法[pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b01b6-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="b01b6-168">取代 hello `$host`， `$database`， `$user`，和`$password`參數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="b01b6-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="b01b6-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b01b6-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b01b6-170">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="b01b6-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
