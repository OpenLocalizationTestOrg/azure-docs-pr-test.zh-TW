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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>Azure 資料庫的 MySQL： 使用 PHP tooconnect 和查詢資料
本快速入門示範如何使用 MySQL 資料庫的 tooconnect tooan Azure [PHP](http://php.net/manual/intro-whatis.php)應用程式。 它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。 本文假設您已熟悉使用 PHP 開發的但是，您就可以與 MySQL 的 Azure 資料庫的新 tooworking。

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a>安裝 PHP
在自己的伺服器上安裝 PHP，或建立 Azure [Web 應用程式](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) (包括 PHP)。

### <a name="macos"></a>MacOS
- 下載 [PHP 7.1.4 版本](http://php.net/downloads.php)
- 安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.macosx.php)進一步的組態

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- 下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://php.net/downloads.php)
- 安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.unix.php)進一步的組態

### <a name="windows"></a>Windows
- 下載 [PHP 7.1.4 非執行緒安全 (x64) 版本](http://windows.php.net/download#php-7.1)
- 安裝 PHP 和參考 toohello [PHP 手冊](http://php.net/manual/install.windows.php)進一步的組態

## <a name="get-connection-information"></a>取得連線資訊
取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. Hello 左窗格中，按一下 **所有資源**，然後搜尋您所建立的 hello server (例如， **myserver4demo**)。
3. 按一下 hello 伺服器名稱。
4. 選取 hello 伺服器**屬性**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。
 ![Azure Database for MySQL 伺服器名稱](./media/connect-php/1_server-properties-name-login.png)
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。

## <a name="connect-and-create-a-table"></a>連線及建立資料表
使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式。 

hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。 程式碼呼叫方法的 hello [mysqli_init](http://php.net/manual/mysqli.init.php)和[mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL。 然後它會呼叫方法[mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello 查詢。 然後它會呼叫方法[mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello 連線。

Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。 

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

## <a name="insert-data"></a>插入資料
使用 hello 下列程式碼 tooconnect，並將插入的資料使用**插入**SQL 陳述式。

hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。 hello 程式碼會使用方法[mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate 備妥的 insert 陳述式，則繫結 hello 參數使用方法的每個插入資料行值[mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)。 hello 程式碼會執行使用方法的 hello 陳述式[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php)之後關閉 hello 使用方法的陳述式和[mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)。

Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。 

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

## <a name="read-data"></a>讀取資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。  hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。 hello 程式碼會使用方法[mysqli_query](http://php.net/manual/mysqli.query.php)執行 hello sql 查詢，並使用[mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php)方法 toofetch hello 產生的資料列。

Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。 

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

## <a name="update-data"></a>更新資料
使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。

hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。 hello 程式碼會使用方法[mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate 備妥的 update 陳述式，會接著繫結使用方法的每個更新的資料行值的 hello 參數[mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)。 hello 程式碼會執行使用方法的 hello 陳述式[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php)之後關閉 hello 使用方法的陳述式和[mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)。

Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。 

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


## <a name="delete-data"></a>刪除資料
使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。 

hello 程式碼會使用 hello **MySQL 改善擴充**(mysqli) 包含在 PHP 中的類別。 hello 程式碼會使用方法[mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate 備妥 delete 陳述式，則繫結 hello hello 參數位置使用方法的 hello 陳述式中的子句[mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php)。 hello 程式碼會執行使用方法的 hello 陳述式[mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php)之後關閉 hello 使用方法的陳述式和[mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php)。

Hello 主機、 使用者名稱、 密碼和 db_name 參數取代為您自己的值。 

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

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [在 Azure 中建置 PHP 和 MySQL Web 應用程式](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
