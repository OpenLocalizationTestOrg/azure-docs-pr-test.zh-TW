---
title: "aaaConnect 應用程式 tooAzure MySQL 資料庫 |Microsoft 文件"
description: "本文件列出 hello 目前支援的連接字串 tooconnect 應用程式與 Azure 資料庫的 MySQL，包括 ADO.NET (C#)、 JDBC、 Node.js、 ODBC、 PHP、 Python 和 Ruby。"
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a><span data-ttu-id="73c22-103">Tooconnect 應用程式 tooAzure 如何針對 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="73c22-103">How tooconnect applications tooAzure Database for MySQL</span></span>
<span data-ttu-id="73c22-104">本文件列出 hello 支援的 Azure 資料庫的 MySQL，以及範本和範例連接字串類型。</span><span class="sxs-lookup"><span data-stu-id="73c22-104">This document lists hello connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="73c22-105">在連接字串中，您可以使用不同的參數和不同的設定。</span><span class="sxs-lookup"><span data-stu-id="73c22-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="73c22-106">tooobtain hello 憑證，請參閱[如何 tooconfigure SSL](./howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="73c22-106">tooobtain hello certificate, see [How tooconfigure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="73c22-107">{your_host} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="73c22-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="73c22-108">{your_user}@{servername} = 正確驗證的 userID 格式。</span><span class="sxs-lookup"><span data-stu-id="73c22-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="73c22-109">使用剛 hello 使用者識別碼，將導致 hello 驗證 toofail。</span><span class="sxs-lookup"><span data-stu-id="73c22-109">Using just hello userID will cause hello authentication toofail.</span></span>

## <a name="adonet"></a><span data-ttu-id="73c22-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="73c22-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="73c22-111">在此範例中，是 hello 伺服器名稱`myserver4demo`，資料庫名稱是`wpdb`，使用者名稱為`WPAdmin`，密碼是`mypassword!2`。</span><span class="sxs-lookup"><span data-stu-id="73c22-111">In this example, hello server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="73c22-112">然後，hello 連接字串應該：</span><span class="sxs-lookup"><span data-stu-id="73c22-112">Then, hello connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="73c22-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="73c22-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="73c22-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="73c22-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="73c22-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="73c22-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="73c22-116">PHP</span><span class="sxs-lookup"><span data-stu-id="73c22-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="73c22-117">Python</span><span class="sxs-lookup"><span data-stu-id="73c22-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="73c22-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="73c22-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a><span data-ttu-id="73c22-119">從 hello Azure 入口網站取得 hello 連線字串詳細資料</span><span class="sxs-lookup"><span data-stu-id="73c22-119">Get hello connection string details from hello Azure portal</span></span>
<span data-ttu-id="73c22-120">在 hello [Azure 入口網站](https://portal.azure.com)，請 tooyour Azure 資料庫的 MySQL server，然後按一下**連接字串**tooget 您的字串清單執行個體： ![hello 連接字串 窗格中 helloAzure 入口網站](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="73c22-120">In hello [Azure portal](https://portal.azure.com), go tooyour Azure Database for MySQL server, and then click **Connection strings** tooget your string list for your instance: ![hello Connection strings pane in hello Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="73c22-121">hello 字串提供詳細資料，例如 hello 驅動程式、 伺服器和其他資料庫的連接參數。</span><span class="sxs-lookup"><span data-stu-id="73c22-121">hello string provides details such as hello driver, server, and other database connection parameters.</span></span> <span data-ttu-id="73c22-122">使用您自己的參數 (例如資料庫名稱、密碼等) 修改這些範例。</span><span class="sxs-lookup"><span data-stu-id="73c22-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="73c22-123">然後，您可以使用此字串 tooconnect toohello 伺服器 」，從您的程式碼和應用程式。</span><span class="sxs-lookup"><span data-stu-id="73c22-123">You can then use this string tooconnect toohello server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73c22-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73c22-124">Next steps</span></span>
- <span data-ttu-id="73c22-125">如需有關連線程式庫的詳細資訊，請參閱[概念 - 連線程式庫](./concepts-connection-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="73c22-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
