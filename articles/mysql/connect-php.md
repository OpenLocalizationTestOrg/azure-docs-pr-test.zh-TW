---
title: "從 PHP 連線到 Azure Database for MySQL | Microsoft Docs"
description: "本快速入門提供數個 PHP 程式碼範例，您可用於從 Azure Database for MySQL 連線及查詢資料。"
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 59da1ab9e76685d7ed0c4415ef99578c982e956c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-database-for-mysql-use-php-to-connect-and-query-data"></a><span data-ttu-id="e4716-103">Azure Database for MySQL︰使用 PHP 來連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="e4716-103">Azure Database for MySQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="e4716-104">本快速入門示範如何使用 [PHP](http://php.net/manual/intro-whatis.php) 應用程式來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="e4716-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="e4716-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="e4716-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="e4716-106">本文假設您已熟悉使用 PHP 進行開發，但不熟悉 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="e4716-106">This article assumes you are familiar with development using PHP, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4716-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="e4716-107">Prerequisites</span></span>
<span data-ttu-id="e4716-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="e4716-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e4716-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="e4716-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="e4716-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="e4716-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="e4716-111">安裝 PHP</span><span class="sxs-lookup"><span data-stu-id="e4716-111">Install PHP</span></span>
<span data-ttu-id="e4716-112">在自己的伺服器上安裝 PHP，或建立 Azure [Web 應用程式](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) (包括 PHP)。</span><span class="sxs-lookup"><span data-stu-id="e4716-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="e4716-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="e4716-113">MacOS</span></span>
- <span data-ttu-id="e4716-114">下載 [PHP 7.1.4 版本](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="e4716-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="e4716-115">安裝 PHP 並參考 [PHP 手冊](http://php.net/manual/install.macosx.php)以便進一步設定</span><span class="sxs-lookup"><span data-stu-id="e4716-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="e4716-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e4716-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="e4716-117">下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="e4716-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="e4716-118">安裝 PHP 並參考 [PHP 手冊](http://php.net/manual/install.unix.php)以便進一步設定</span><span class="sxs-lookup"><span data-stu-id="e4716-118">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="e4716-119">Windows</span><span class="sxs-lookup"><span data-stu-id="e4716-119">Windows</span></span>
- <span data-ttu-id="e4716-120">下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="e4716-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="e4716-121">安裝 PHP 並參考 [PHP 手冊](http://php.net/manual/install.windows.php)以便進一步設定</span><span class="sxs-lookup"><span data-stu-id="e4716-121">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="e4716-122">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="e4716-122">Get connection information</span></span>
<span data-ttu-id="e4716-123">取得連線到 Azure Database for MySQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="e4716-123">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="e4716-124">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="e4716-124">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e4716-125">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="e4716-125">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e4716-126">在左側窗格中，按一下 [所有資源]，然後搜尋您所建立的伺服器 (例如 **myserver4demo**)。</span><span class="sxs-lookup"><span data-stu-id="e4716-126">In the left pane, click **All resources**, and then search for the server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="e4716-127">按一下伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="e4716-127">Click the server name.</span></span>
4. <span data-ttu-id="e4716-128">選取伺服器的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="e4716-128">Select the server's **Properties** page.</span></span> <span data-ttu-id="e4716-129">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="e4716-129">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e4716-130">![Azure Database for MySQL 伺服器名稱](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="e4716-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="e4716-131">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="e4716-131">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="e4716-132">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="e4716-132">Connect and create a table</span></span>
<span data-ttu-id="e4716-133">使用下列程式碼搭配 **CREATE TABLE** SQL 陳述式來連線和建立資料表。</span><span class="sxs-lookup"><span data-stu-id="e4716-133">Use the following code to connect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="e4716-134">程式碼會使用 PHP 內含的 **MySQL 改良擴充功能** (mysqli) 類別。</span><span class="sxs-lookup"><span data-stu-id="e4716-134">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e4716-135">程式碼會呼叫 [mysqli_init](http://php.net/manual/mysqli.init.php) 和 [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) 方法來連線到 MySQL。</span><span class="sxs-lookup"><span data-stu-id="e4716-135">The code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) to connect to MySQL.</span></span> <span data-ttu-id="e4716-136">然後它會呼叫 [mysqli_query](http://php.net/manual/mysqli.query.php) 方法來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="e4716-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) to run the query.</span></span> <span data-ttu-id="e4716-137">然後它會呼叫 [mysqli_close](http://php.net/manual/mysqli.close.php) 方法來關閉連線。</span><span class="sxs-lookup"><span data-stu-id="e4716-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) to close the connection.</span></span>

<span data-ttu-id="e4716-138">以自己的值取代主機、使用者名稱、密碼和 db_name 參數。</span><span class="sxs-lookup"><span data-stu-id="e4716-138">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

// Run the create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="e4716-139">插入資料</span><span class="sxs-lookup"><span data-stu-id="e4716-139">Insert data</span></span>
<span data-ttu-id="e4716-140">使用下列程式碼搭配 **INSERT** SQL 陳述式來連線和插入資料。</span><span class="sxs-lookup"><span data-stu-id="e4716-140">Use the following code to connect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="e4716-141">程式碼會使用 PHP 內含的 **MySQL 改良擴充功能** (mysqli) 類別。</span><span class="sxs-lookup"><span data-stu-id="e4716-141">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e4716-142">程式碼會使用 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) 方法來建立已備妥的 insert 陳述式，然後使用 [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) 方法來繫結每個插入資料行值的參數。</span><span class="sxs-lookup"><span data-stu-id="e4716-142">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared insert statement, then binds the parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="e4716-143">程式碼會使用 [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 方法執行陳述式，之後使用 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) 方法關閉陳述式。</span><span class="sxs-lookup"><span data-stu-id="e4716-143">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="e4716-144">以自己的值取代主機、使用者名稱、密碼和 db_name 參數。</span><span class="sxs-lookup"><span data-stu-id="e4716-144">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close the connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="e4716-145">讀取資料</span><span class="sxs-lookup"><span data-stu-id="e4716-145">Read data</span></span>
<span data-ttu-id="e4716-146">使用下列程式碼搭配 **SELECT** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="e4716-146">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="e4716-147">程式碼會使用 PHP 內含的 **MySQL 改良擴充功能** (mysqli) 類別。</span><span class="sxs-lookup"><span data-stu-id="e4716-147">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e4716-148">程式碼會使用 [mysqli_query](http://php.net/manual/mysqli.query.php) 方法執行 sql 查詢，並使用 [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) 方法來擷取結果資料列。</span><span class="sxs-lookup"><span data-stu-id="e4716-148">The code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform the sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method to fetch the resulting rows.</span></span>

<span data-ttu-id="e4716-149">以自己的值取代主機、使用者名稱、密碼和 db_name 參數。</span><span class="sxs-lookup"><span data-stu-id="e4716-149">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="e4716-150">更新資料</span><span class="sxs-lookup"><span data-stu-id="e4716-150">Update data</span></span>
<span data-ttu-id="e4716-151">使用下列程式碼搭配 **UPDATE** SQL 陳述式來連線和更新資料。</span><span class="sxs-lookup"><span data-stu-id="e4716-151">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="e4716-152">程式碼會使用 PHP 內含的 **MySQL 改良擴充功能** (mysqli) 類別。</span><span class="sxs-lookup"><span data-stu-id="e4716-152">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e4716-153">程式碼會使用 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) 方法來建立已備妥的 update 陳述式，然後使用 [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) 方法來繫結每個更新資料行值的參數。</span><span class="sxs-lookup"><span data-stu-id="e4716-153">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared update statement, then binds the parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="e4716-154">程式碼會使用 [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 方法執行陳述式，之後使用 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) 方法關閉陳述式。</span><span class="sxs-lookup"><span data-stu-id="e4716-154">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="e4716-155">以自己的值取代主機、使用者名稱、密碼和 db_name 參數。</span><span class="sxs-lookup"><span data-stu-id="e4716-155">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close the connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="e4716-156">刪除資料</span><span class="sxs-lookup"><span data-stu-id="e4716-156">Delete data</span></span>
<span data-ttu-id="e4716-157">使用下列程式碼搭配 **DELETE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="e4716-157">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="e4716-158">程式碼會使用 PHP 內含的 **MySQL 改良擴充功能** (mysqli) 類別。</span><span class="sxs-lookup"><span data-stu-id="e4716-158">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="e4716-159">程式碼會使用 [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) 方法來建立已備妥的 delete 陳述式，然後使用 [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php) 方法來繫結陳述式中 where 子句的參數。</span><span class="sxs-lookup"><span data-stu-id="e4716-159">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared delete statement, then binds the parameters for the where clause in the statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="e4716-160">程式碼會使用 [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) 方法執行陳述式，之後使用 [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php) 方法關閉陳述式。</span><span class="sxs-lookup"><span data-stu-id="e4716-160">The code runs the statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="e4716-161">以自己的值取代主機、使用者名稱、密碼和 db_name 參數。</span><span class="sxs-lookup"><span data-stu-id="e4716-161">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="e4716-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e4716-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e4716-163">在 Azure 中建置 PHP 和 MySQL Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="e4716-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
