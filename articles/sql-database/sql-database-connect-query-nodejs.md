---
title: "使用 Node.js 查詢 Azure SQL Database | Microsoft Docs"
description: "本主題說明如何使用 Node.js 來建立連線到 Azure SQL Database 的程式，並使用 Transact-SQL 陳述式查詢。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 53f70e37-5eb4-400d-972e-dd7ea0caacd4
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 1907a95df9132c059d7985b6d5cd913536bf3403
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-nodejs-to-query-an-azure-sql-database"></a><span data-ttu-id="aa005-103">使用 Node.js 查詢 Azure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="aa005-103">Use Node.js to query an Azure SQL database</span></span>

<span data-ttu-id="aa005-104">此快速入門教學課程示範如何使用 [Node.js](https://nodejs.org/en/) 來建立程式以連線至 Azure SQL 資料庫，並使用 Transact-SQL 陳述式來查詢資料。</span><span class="sxs-lookup"><span data-stu-id="aa005-104">This quick start tutorial demonstrates how to use [Node.js](https://nodejs.org/en/) to create a program to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa005-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="aa005-105">Prerequisites</span></span>

<span data-ttu-id="aa005-106">若要完成本快速入門教學課程，請確定您具有下列項目︰</span><span class="sxs-lookup"><span data-stu-id="aa005-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="aa005-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="aa005-107">An Azure SQL database.</span></span> <span data-ttu-id="aa005-108">本快速入門使用其中一個快速入門建立的資源︰</span><span class="sxs-lookup"><span data-stu-id="aa005-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="aa005-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="aa005-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="aa005-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="aa005-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="aa005-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa005-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="aa005-112">在此快速入門教學課程中，您所使用電腦的公用 IP 位址[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="aa005-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="aa005-113">您已安裝適用於您作業系統的 Node.js 和相關軟體。</span><span class="sxs-lookup"><span data-stu-id="aa005-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="aa005-114">**MacOS**：安裝 Homebrew 和 Node.js，然後安裝 ODBC 驅動程式和 SQLCMD。</span><span class="sxs-lookup"><span data-stu-id="aa005-114">**MacOS**: Install Homebrew and Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="aa005-115">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/)。</span><span class="sxs-lookup"><span data-stu-id="aa005-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="aa005-116">**Ubuntu**：安裝 Node.js，然後安裝 ODBC 驅動程式和 SQLCMD。</span><span class="sxs-lookup"><span data-stu-id="aa005-116">**Ubuntu**: Install Node.js, and then install the ODBC driver and SQLCMD.</span></span> <span data-ttu-id="aa005-117">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="aa005-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="aa005-118">**Windows**：安裝 Chocolatey 和 Node.js，然後安裝 ODBC 驅動程式和 SQLCMD。</span><span class="sxs-lookup"><span data-stu-id="aa005-118">**Windows**: Install Chocolatey and Node.js, and then install the ODBC driver and SQL CMD.</span></span> <span data-ttu-id="aa005-119">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/)。</span><span class="sxs-lookup"><span data-stu-id="aa005-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="aa005-120">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="aa005-120">SQL server connection information</span></span>

<span data-ttu-id="aa005-121">取得連線到 Azure SQL Database 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="aa005-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="aa005-122">您在下一個程序中需要完整的伺服器名稱、資料庫名稱和登入資訊。</span><span class="sxs-lookup"><span data-stu-id="aa005-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="aa005-123">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="aa005-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="aa005-124">從左側功能表中選取 [SQL Database]，按一下 [SQL Database]頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="aa005-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="aa005-125">在您資料庫的 [概觀] 頁面上，檢閱如下圖所示的完整伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="aa005-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="aa005-126">您可以將滑鼠移至伺服器名稱上，以帶出 [按一下以複製] 選項。</span><span class="sxs-lookup"><span data-stu-id="aa005-126">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="aa005-128">如果您忘記 Azure SQL Database 伺服器的登入資訊，請瀏覽至 [SQL Database 伺服器] 頁面來檢視伺服器系統管理員名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="aa005-128">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa005-129">在您執行本教學課程的電腦上，公用 IP 位址必須有防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="aa005-129">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="aa005-130">如果您在不同電腦上或有不同的公用 IP 位址，請建立[使用 Azure 入口網站的伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="aa005-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="aa005-131">建立 Node.js 專案</span><span class="sxs-lookup"><span data-stu-id="aa005-131">Create a Node.js project</span></span>

<span data-ttu-id="aa005-132">開啟命令提示字元，並建立名為 sqltest 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="aa005-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="aa005-133">瀏覽至您建立的資料夾中，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="aa005-133">Navigate to the folder you created and run the following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="aa005-134">插入程式碼以查詢 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="aa005-134">Insert code to query SQL database</span></span>

1. <span data-ttu-id="aa005-135">在您的開發環境或慣用的文字編輯器中，建立新的檔案 **sqltest.js**。</span><span class="sxs-lookup"><span data-stu-id="aa005-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="aa005-136">使用下列程式碼取代內容，並為您的伺服器、資料庫、使用者和密碼新增適當的值。</span><span class="sxs-lookup"><span data-stu-id="aa005-136">Replace the contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection to database
   var config = 
      {
        userName: 'someuser', // update me
        password: 'somepassword', // update me
        server: 'edmacasqlserver.database.windows.net', // update me
        options: 
           {
              database: 'somedb' //update me
              , encrypt: true
           }
      }
   var connection = new Connection(config);

   // Attempt to connect and execute queries if connection goes through
   connection.on('connect', function(err) 
      {
        if (err) 
          {
             console.log(err)
          }
       else
          {
              queryDatabase()
          }
      }
    );

   function queryDatabase()
      { console.log('Reading rows from the Table...');

          // Read all rows from table
        request = new Request(
             "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid",
                function(err, rowCount, rows) 
                   {
                       console.log(rowCount + ' row(s) returned');
                       process.exit();
                   }
               );
    
        request.on('row', function(columns) {
           columns.forEach(function(column) {
               console.log("%s\t%s", column.metadata.colName, column.value);
            });
                });
        connection.execSql(request);
      }
```

## <a name="run-the-code"></a><span data-ttu-id="aa005-137">執行程式碼</span><span class="sxs-lookup"><span data-stu-id="aa005-137">Run the code</span></span>

1. <span data-ttu-id="aa005-138">在命令提示字元中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="aa005-138">At the command prompt, run the following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="aa005-139">請確認前 20 個資料列已傳回，然後關閉應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="aa005-139">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa005-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa005-140">Next steps</span></span>

- <span data-ttu-id="aa005-141">了解 [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="aa005-141">Learn about the [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="aa005-142">了解如何在 Windows/Linux/macOS 中[使用 .NET Core 來連線及查詢 Azure SQL 資料庫](sql-database-connect-query-dotnet-core.md)。</span><span class="sxs-lookup"><span data-stu-id="aa005-142">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="aa005-143">了解 [使用命令列以開始使用在 Windows/Linux/macOS 上的 .NET Core](/dotnet/core/tutorials/using-with-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="aa005-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="aa005-144">深入了解如何[使用 SSMS 設計您的第一個 Azure SQL 資料庫](sql-database-design-first-database.md)或[使用 .NET 設計您的第一個 Azure SQL 資料庫](sql-database-design-first-database-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="aa005-144">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="aa005-145">了解如何[使用 SSMS 連線及查詢](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="aa005-145">Learn how to [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="aa005-146">了解如何[使用 Visual Studio Code 連線及查詢](sql-database-connect-query-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="aa005-146">Learn how to [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


