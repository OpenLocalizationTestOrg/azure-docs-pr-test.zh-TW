---
title: "使用 .PHP 查詢 Azure SQL Database | Microsoft Docs"
description: "本主題說明如何使用 PHP 來建立連線到 Azure SQL Database 的程式，並使用 Transact-SQL 陳述式查詢。"
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
ms.openlocfilehash: 3a43472ad2be4a0fd6f7126f72433acd8b5f25fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-php-to-query-an-azure-sql-database"></a><span data-ttu-id="a4f36-103">使用 PHP 查詢 Azure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="a4f36-103">Use PHP to query an Azure SQL database</span></span>

<span data-ttu-id="a4f36-104">此快速入門教學課程示範如何使用 [PHP](http://php.net/manual/en/intro-whatis.php) 來建立程式以連線至 Azure SQL 資料庫，並使用 Transact-SQL 陳述式來查詢資料。</span><span class="sxs-lookup"><span data-stu-id="a4f36-104">This quick start tutorial demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4f36-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="a4f36-105">Prerequisites</span></span>

<span data-ttu-id="a4f36-106">若要完成本快速入門教學課程，請確定您具有下列項目︰</span><span class="sxs-lookup"><span data-stu-id="a4f36-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="a4f36-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="a4f36-107">An Azure SQL database.</span></span> <span data-ttu-id="a4f36-108">本快速入門使用其中一個快速入門建立的資源︰</span><span class="sxs-lookup"><span data-stu-id="a4f36-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="a4f36-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="a4f36-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="a4f36-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="a4f36-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="a4f36-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4f36-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="a4f36-112">在此快速入門教學課程中，您所使用電腦的公用 IP 位址[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="a4f36-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="a4f36-113">您已安裝適用於您作業系統的 PHP 和相關軟體。</span><span class="sxs-lookup"><span data-stu-id="a4f36-113">You have installed PHP and related software for your operating system.</span></span>

    - <span data-ttu-id="a4f36-114">**MacOS**：安裝 Homebrew 和 PHP，安裝 ODBC 驅動程式和 SQLCMD，然後再安裝 PHP Driver for SQL Server。</span><span class="sxs-lookup"><span data-stu-id="a4f36-114">**MacOS**: Install Homebrew and PHP, install the ODBC driver and SQLCMD, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="a4f36-115">請參閱[步驟 1.2、1.3 和 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/)。</span><span class="sxs-lookup"><span data-stu-id="a4f36-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/mac/).</span></span>
    - <span data-ttu-id="a4f36-116">**Ubuntu**：安裝 PHP 和其他必要的套件，然後安裝 PHP Driver for SQL Server。</span><span class="sxs-lookup"><span data-stu-id="a4f36-116">**Ubuntu**:  Install PHP and other required packages, and then install the PHP Driver for SQL Server.</span></span> <span data-ttu-id="a4f36-117">請參閱[步驟 1.2 和 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="a4f36-117">See [Steps 1.2 and 2.1](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/).</span></span>
    - <span data-ttu-id="a4f36-118">**Windows**：安裝 PHP for IIS Express 的最新版本、Microsoft Drivers for SQL Server in IIS Express 的最新版本、Chocolatey、ODBC 驅動程式，以及 SQLCMD。</span><span class="sxs-lookup"><span data-stu-id="a4f36-118">**Windows**: Install the newest version of PHP for IIS Express, the newest version of Microsoft Drivers for SQL Server in IIS Express, Chocolatey, the ODBC driver, and SQLCMD.</span></span> <span data-ttu-id="a4f36-119">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/)。</span><span class="sxs-lookup"><span data-stu-id="a4f36-119">See [Steps 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/php/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="a4f36-120">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="a4f36-120">SQL server connection information</span></span>

<span data-ttu-id="a4f36-121">取得連線到 Azure SQL Database 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="a4f36-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="a4f36-122">您在下一個程序中需要完整的伺服器名稱、資料庫名稱和登入資訊。</span><span class="sxs-lookup"><span data-stu-id="a4f36-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="a4f36-123">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="a4f36-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a4f36-124">從左側功能表中選取 [SQL Database]，按一下 [SQL Database]頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a4f36-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="a4f36-125">在您資料庫的 [概觀] 頁面上，檢閱如下圖所示的完整伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="a4f36-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="a4f36-126">您可以將滑鼠移至伺服器名稱上，以帶出 [按一下以複製] 選項。</span><span class="sxs-lookup"><span data-stu-id="a4f36-126">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="a4f36-128">如果您忘記伺服器登入資訊，請瀏覽至 [SQL Database 伺服器] 頁面來檢視伺服器系統管理員名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="a4f36-128">If you forget your server login information, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="a4f36-129">插入程式碼以查詢 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="a4f36-129">Insert code to query SQL database</span></span>

1. <span data-ttu-id="a4f36-130">在您慣用的文字編輯器中，建立新的檔案 **sqltest.php**。</span><span class="sxs-lookup"><span data-stu-id="a4f36-130">In your favorite text editor, create a new file, **sqltest.php**.</span></span>  

2. <span data-ttu-id="a4f36-131">使用下列程式碼取代內容，並為您的伺服器、資料庫、使用者和密碼新增適當的值。</span><span class="sxs-lookup"><span data-stu-id="a4f36-131">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```PHP
   <?php
   $serverName = "your_server.database.windows.net";
   $connectionOptions = array(
       "Database" => "your_database",
       "Uid" => "your_username",
       "PWD" => "your_password"
   );
   //Establishes the connection
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

## <a name="run-the-code"></a><span data-ttu-id="a4f36-132">執行程式碼</span><span class="sxs-lookup"><span data-stu-id="a4f36-132">Run the code</span></span>

1. <span data-ttu-id="a4f36-133">在命令提示字元中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a4f36-133">At the command prompt, run the following commands:</span></span>

   ```php
   php sqltest.php
   ```

2. <span data-ttu-id="a4f36-134">請確認前 20 個資料列已傳回，然後關閉應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="a4f36-134">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4f36-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4f36-135">Next steps</span></span>
- [<span data-ttu-id="a4f36-136">設計您的第一個 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a4f36-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="a4f36-137">Microsoft PHP Drivers for SQL Server</span><span class="sxs-lookup"><span data-stu-id="a4f36-137">Microsoft PHP Drivers for SQL Server</span></span>](https://github.com/Microsoft/msphpsql/)
- [<span data-ttu-id="a4f36-138">回報問題或發問</span><span class="sxs-lookup"><span data-stu-id="a4f36-138">Report issues or ask questions</span></span>](https://github.com/Microsoft/msphpsql/issues)
