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
# <a name="use-php-tooquery-an-azure-sql-database"></a><span data-ttu-id="2e227-103">使用 PHP tooquery Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="2e227-103">Use PHP tooquery an Azure SQL database</span></span>

<span data-ttu-id="2e227-104">本快速入門教學課程示範如何 toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate 程式 tooconnect tooan Azure SQL 資料庫，將 TRANSACT-SQL 陳述式 tooquery 資料。</span><span class="sxs-lookup"><span data-stu-id="2e227-104">This quick start tutorial demonstrates how toouse [PHP](http://php.net/manual/en/intro-whatis.php) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e227-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="2e227-105">Prerequisites</span></span>

<span data-ttu-id="2e227-106">toocomplete 此快速入門教學課程，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2e227-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="2e227-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="2e227-107">An Azure SQL database.</span></span> <span data-ttu-id="2e227-108">本快速入門會使用 hello 資源建立在其中一個這些快速入門：</span><span class="sxs-lookup"><span data-stu-id="2e227-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="2e227-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="2e227-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="2e227-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="2e227-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="2e227-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e227-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="2e227-112">A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2e227-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="2e227-113">您已安裝適用於您作業系統的 PHP 和相關軟體。</span><span class="sxs-lookup"><span data-stu-id="2e227-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="2e227-114">**MacOS**： 安裝 Homebrew 和 PHP，依序安裝 hello ODBC 驅動程式和 SQLCMD 和 hello PHP Driver for SQL Server。</span><span class="sxs-lookup"><span data-stu-id="2e227-114">**MacOS**: Install Homebrew and PHP, install hello ODBC driver and SQLCMD, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="2e227-115">請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/)。</span><span class="sxs-lookup"><span data-stu-id="2e227-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="2e227-116">**Ubuntu**： 安裝 PHP 和其他必要的封裝，然後再安裝 hello PHP Driver for SQL Server。</span><span class="sxs-lookup"><span data-stu-id="2e227-116">**Ubuntu**:  Install PHP and other required packages, and then install hello PHP Driver for SQL Server.</span></span> <span data-ttu-id="2e227-117">請參閱[步驟 1.2 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="2e227-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="2e227-118">**Windows**： 安裝 hello 最新版本的 PHP 的 IIS Express，hello 最新版本的 IIS Express、 Chocolatey、 hello ODBC 驅動程式和 SQLCMD 中的 SQL Server 的 Microsoft 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="2e227-118">**Windows**: Install hello newest version of PHP for IIS Express, hello newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, hello ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="2e227-119">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/)。</span><span class="sxs-lookup"><span data-stu-id="2e227-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="2e227-120">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="2e227-120">SQL server connection information</span></span>

<span data-ttu-id="2e227-121">收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="2e227-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="2e227-122">您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="2e227-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="2e227-123">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="2e227-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2e227-124">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="2e227-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="2e227-125">在 hello**概觀**頁面為您的資料庫檢閱 hello 完整伺服器名稱 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="2e227-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="2e227-126">您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。</span><span class="sxs-lookup"><span data-stu-id="2e227-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="2e227-128">如果忘記您的伺服器登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="2e227-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="2e227-129">插入程式碼 tooquery SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="2e227-129">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="2e227-130">在您慣用的文字編輯器中，建立新的檔案 **sqltest.php**。</span><span class="sxs-lookup"><span data-stu-id="2e227-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="2e227-131">以下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼的 hello 取代 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="2e227-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="2e227-132">執行 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="2e227-132">Run hello code</span></span>

1. <span data-ttu-id="2e227-133">在 hello 命令提示字元中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e227-133">At hello command prompt, run hello following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="2e227-134">請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="2e227-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e227-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e227-135">Next steps</span></span>
- [<span data-ttu-id="2e227-136">設計您的第一個 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="2e227-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="2e227-137">Microsoft PHP Drivers for SQL Server</span><span class="sxs-lookup"><span data-stu-id="2e227-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="2e227-138">回報問題或發問</span><span class="sxs-lookup"><span data-stu-id="2e227-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
