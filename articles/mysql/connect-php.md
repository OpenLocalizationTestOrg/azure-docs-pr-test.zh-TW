---
title: "用於從 PHP MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門會提供數個 PHP 程式碼範例，您可以使用 tooconnect 和查詢資料從 Azure 資料庫的 MySQL。"
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="4fc01-103">Azure 資料庫的 MySQL： 使用 PHP tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="4fc01-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="4fc01-104">本快速入門示範如何使用 MySQL 資料庫的 tooconnect tooan Azure [PHP](http://php.net/manual/intro-whatis.php)應用程式。</span><span class="sxs-lookup"><span data-stu-id="4fc01-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="4fc01-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="4fc01-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="4fc01-106">本文假設您已熟悉使用 PHP 開發的但是，您就可以與 MySQL 的 Azure 資料庫的新 tooworking。</span><span class="sxs-lookup"><span data-stu-id="4fc01-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fc01-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="4fc01-107">Prerequisites</span></span>
<span data-ttu-id="4fc01-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="4fc01-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4fc01-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="4fc01-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4fc01-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="4fc01-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="4fc01-111">安裝 PHP</span><span class="sxs-lookup"><span data-stu-id="4fc01-111">Install PHP</span></span>
<span data-ttu-id="4fc01-112">在自己的伺服器上安裝 PHP，或建立 Azure [Web 應用程式](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) (包括 PHP)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="4fc01-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="4fc01-113">MacOS</span></span>
- <span data-ttu-id="4fc01-114">下載 [PHP 7.1.4 版本](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="4fc01-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="4fc01-115">安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.macosx.php)進一步的組態</span><span class="sxs-lookup"><span data-stu-id="4fc01-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="4fc01-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="4fc01-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="4fc01-117">下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="4fc01-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="4fc01-118">安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.unix.php)進一步的組態</span><span class="sxs-lookup"><span data-stu-id="4fc01-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="4fc01-119">Windows</span><span class="sxs-lookup"><span data-stu-id="4fc01-119">Windows</span></span>
- <span data-ttu-id="4fc01-120">下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="4fc01-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="4fc01-121">安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.windows.php)進一步的組態</span><span class="sxs-lookup"><span data-stu-id="4fc01-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4fc01-122">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="4fc01-122">Get connection information</span></span>
<span data-ttu-id="4fc01-123">取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4fc01-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="4fc01-124">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="4fc01-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4fc01-125">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4fc01-126">Hello 左窗格中，按一下 **所有資源**，然後搜尋您所建立的 hello server (例如， **myserver4demo**)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="4fc01-127">按一下 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="4fc01-127">Click hello server name.</span></span>
4. <span data-ttu-id="4fc01-128">選取 hello 伺服器**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="4fc01-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="4fc01-129">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="4fc01-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4fc01-130">![Azure Database for MySQL 伺服器名稱](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4fc01-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="4fc01-131">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="4fc01-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="4fc01-132">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="4fc01-132">Connect and create a table</span></span>
<span data-ttu-id="4fc01-133">使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="4fc01-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="4fc01-134">hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。</span><span class="sxs-lookup"><span data-stu-id="4fc01-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4fc01-135">程式碼呼叫方法的 hello [mysqli_init](http://php.net/manual/mysqli.init.php)和[mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL。</span><span class="sxs-lookup"><span data-stu-id="4fc01-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="4fc01-136">然後它會呼叫方法[mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4fc01-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="4fc01-137">然後它會呼叫方法[mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello 連線。</span><span class="sxs-lookup"><span data-stu-id="4fc01-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="4fc01-138">Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="4fc01-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
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

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="4fc01-139">插入資料</span><span class="sxs-lookup"><span data-stu-id="4fc01-139">Insert data</span></span>
<span data-ttu-id="4fc01-140">使用 hello 下列程式碼 tooconnect，並將插入的資料使用**插入**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="4fc01-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="4fc01-141">hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。</span><span class="sxs-lookup"><span data-stu-id="4fc01-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4fc01-142">hello 程式碼會使用方法[mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate 備妥的 insert 陳述式，則繫結 hello 參數使用方法的每個插入資料行值[mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="4fc01-143">hello 程式碼會執行使用方法的 hello 陳述式[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php)之後關閉 hello 使用方法的陳述式和[mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="4fc01-144">Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="4fc01-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
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

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="4fc01-145">讀取資料</span><span class="sxs-lookup"><span data-stu-id="4fc01-145">Read data</span></span>
<span data-ttu-id="4fc01-146">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="4fc01-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="4fc01-147">hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。</span><span class="sxs-lookup"><span data-stu-id="4fc01-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4fc01-148">hello 程式碼會使用方法[mysqli_query](http://php.net/manual/mysqli.query.php)執行 hello sql 查詢，並使用[mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php)方法 toofetch hello 產生的資料列。</span><span class="sxs-lookup"><span data-stu-id="4fc01-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="4fc01-149">Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="4fc01-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="4fc01-150">更新資料</span><span class="sxs-lookup"><span data-stu-id="4fc01-150">Update data</span></span>
<span data-ttu-id="4fc01-151">使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="4fc01-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="4fc01-152">hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。</span><span class="sxs-lookup"><span data-stu-id="4fc01-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4fc01-153">hello 程式碼會使用方法[mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate 備妥的 update 陳述式，會接著繫結使用方法的每個更新的資料行值的 hello 參數[mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="4fc01-154">hello 程式碼會執行使用方法的 hello 陳述式[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php)之後關閉 hello 使用方法的陳述式和[mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="4fc01-155">Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="4fc01-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="4fc01-156">刪除資料</span><span class="sxs-lookup"><span data-stu-id="4fc01-156">Delete data</span></span>
<span data-ttu-id="4fc01-157">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="4fc01-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="4fc01-158">hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。</span><span class="sxs-lookup"><span data-stu-id="4fc01-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4fc01-159">hello 程式碼會使用方法[mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate 備妥 delete 陳述式，則繫結 hello hello 參數位置使用方法的 hello 陳述式中的子句[mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="4fc01-160">hello 程式碼會執行使用方法的 hello 陳述式[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php)之後關閉 hello 使用方法的陳述式和[mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)。</span><span class="sxs-lookup"><span data-stu-id="4fc01-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="4fc01-161">Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="4fc01-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="4fc01-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4fc01-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4fc01-163">在 Azure 中建置 PHP 和 MySQL Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4fc01-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
