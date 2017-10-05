---
title: "將應用程式連線至適用於 MySQL 的 Azure 資料庫 | Microsoft Docs"
description: "本文件列出目前支援讓應用程式與「適用於 MySQL 的 Azure 資料庫」連線的所有連接字串，包括 ADO.NET (C#)、JDBC、Node.js、ODBC、PHP、Python 和 Ruby。"
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: 2f40da41bcfda7e35f6fc63ead5d055246ab390c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a><span data-ttu-id="7657f-103">如何將應用程式連線至適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="7657f-103">How to connect applications to Azure Database for MySQL</span></span>
<span data-ttu-id="7657f-104">本文件列出「適用於 MySQL 的 Azure 資料庫」支援的連接字串類型，以及範本和範例。</span><span class="sxs-lookup"><span data-stu-id="7657f-104">This document lists the connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="7657f-105">在連接字串中，您可以使用不同的參數和不同的設定。</span><span class="sxs-lookup"><span data-stu-id="7657f-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="7657f-106">若要取得憑證，請參閱[如何設定 SSL](./howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="7657f-106">To obtain the certificate, see [How to configure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="7657f-107">{your_host} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="7657f-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="7657f-108">{your_user}@{servername} = 正確驗證的 userID 格式。</span><span class="sxs-lookup"><span data-stu-id="7657f-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="7657f-109">只使用 userID 將會導致驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="7657f-109">Using just the userID will cause the authentication to fail.</span></span>

## <a name="adonet"></a><span data-ttu-id="7657f-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="7657f-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="7657f-111">在此範例中，伺服器名稱是 `myserver4demo`、資料庫名稱是 `wpdb`、使用者名稱是 `WPAdmin`、密碼是 `mypassword!2`。</span><span class="sxs-lookup"><span data-stu-id="7657f-111">In this example, the server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="7657f-112">所以，連接字串應該為：</span><span class="sxs-lookup"><span data-stu-id="7657f-112">Then, the connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="7657f-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="7657f-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="7657f-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="7657f-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="7657f-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="7657f-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="7657f-116">PHP</span><span class="sxs-lookup"><span data-stu-id="7657f-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="7657f-117">Python</span><span class="sxs-lookup"><span data-stu-id="7657f-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="7657f-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="7657f-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a><span data-ttu-id="7657f-119">從 Azure 入口網站取得連接字串詳細資料</span><span class="sxs-lookup"><span data-stu-id="7657f-119">Get the connection string details from the Azure portal</span></span>
<span data-ttu-id="7657f-120">在 [Azure 入口網站](https://portal.azure.com)中，移至適用於 MySQL 伺服器的 Azure 資料庫，然後按一下 [連接字串] 以取得您的執行個體的字串清單︰![Azure 入口網站中的 [連接字串] 窗格](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="7657f-120">In the [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL server, and then click **Connection strings** to get your string list for your instance: ![The Connection strings pane in the Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="7657f-121">此字串會提供詳細資料，例如驅動程式、伺服器和其他資料庫連線參數。</span><span class="sxs-lookup"><span data-stu-id="7657f-121">The string provides details such as the driver, server, and other database connection parameters.</span></span> <span data-ttu-id="7657f-122">使用您自己的參數 (例如資料庫名稱、密碼等) 修改這些範例。</span><span class="sxs-lookup"><span data-stu-id="7657f-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="7657f-123">接著，您可以使用這個字串從您的程式碼和應用程式連接到伺服器。</span><span class="sxs-lookup"><span data-stu-id="7657f-123">You can then use this string to connect to the server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7657f-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7657f-124">Next steps</span></span>
- <span data-ttu-id="7657f-125">如需有關連線程式庫的詳細資訊，請參閱[概念 - 連線程式庫](./concepts-connection-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="7657f-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
