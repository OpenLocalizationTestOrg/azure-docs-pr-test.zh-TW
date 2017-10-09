---
title: "Azure SQL Database 的 aaaUse Node.js tooquery |Microsoft 文件"
description: "本主題說明如何 toouse Node.js toocreate 連接 tooan Azure SQL Database 和查詢使用 TRANSACT-SQL 陳述式的程式。"
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
ms.openlocfilehash: 3870130a486c218eafeb9cf792a4275de7fd6551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-nodejs-tooquery-an-azure-sql-database"></a><span data-ttu-id="db695-103">使用 Node.js tooquery Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="db695-103">Use Node.js tooquery an Azure SQL database</span></span>

<span data-ttu-id="db695-104">本快速入門教學課程示範如何 toouse [Node.js](https://nodejs.org/en/) toocreate 程式 tooconnect tooan Azure SQL 資料庫，將 TRANSACT-SQL 陳述式 tooquery 資料。</span><span class="sxs-lookup"><span data-stu-id="db695-104">This quick start tutorial demonstrates how toouse [Node.js](https://nodejs.org/en/) toocreate a program tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db695-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="db695-105">Prerequisites</span></span>

<span data-ttu-id="db695-106">toocomplete 此快速入門教學課程，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="db695-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="db695-107">Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="db695-107">An Azure SQL database.</span></span> <span data-ttu-id="db695-108">本快速入門會使用 hello 資源建立在其中一個這些快速入門：</span><span class="sxs-lookup"><span data-stu-id="db695-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="db695-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="db695-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="db695-110">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="db695-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="db695-111">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="db695-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="db695-112">A[伺服器層級防火牆規則](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)您使用此快速入門教學課程中的 hello 電腦 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="db695-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="db695-113">您已安裝適用於您作業系統的 Node.js 和相關軟體。</span><span class="sxs-lookup"><span data-stu-id="db695-113">You have installed Node.js and related software for your operating system.</span></span>
    - <span data-ttu-id="db695-114">**MacOS**： 安裝 Homebrew 和 Node.js，然後再安裝 hello ODBC 驅動程式和 SQLCMD。</span><span class="sxs-lookup"><span data-stu-id="db695-114">**MacOS**: Install Homebrew and Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="db695-115">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/)。</span><span class="sxs-lookup"><span data-stu-id="db695-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/mac/).</span></span>
    - <span data-ttu-id="db695-116">**Ubuntu**： 安裝 Node.js，然後再安裝 hello ODBC 驅動程式和 SQLCMD。</span><span class="sxs-lookup"><span data-stu-id="db695-116">**Ubuntu**: Install Node.js, and then install hello ODBC driver and SQLCMD.</span></span> <span data-ttu-id="db695-117">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="db695-117">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu/) .</span></span>
    - <span data-ttu-id="db695-118">**Windows**： 安裝 Chocolatey 和 Node.js，然後再安裝 hello ODBC 驅動程式和 SQL CMD.</span><span class="sxs-lookup"><span data-stu-id="db695-118">**Windows**: Install Chocolatey and Node.js, and then install hello ODBC driver and SQL CMD.</span></span> <span data-ttu-id="db695-119">請參閱[步驟 1.2 和 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/)。</span><span class="sxs-lookup"><span data-stu-id="db695-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/node/windows/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="db695-120">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="db695-120">SQL server connection information</span></span>

<span data-ttu-id="db695-121">收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="db695-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="db695-122">您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="db695-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="db695-123">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="db695-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="db695-124">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="db695-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="db695-125">在 hello**概觀**頁面為您的資料庫檢閱 hello 完整伺服器名稱 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="db695-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="db695-126">您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。</span><span class="sxs-lookup"><span data-stu-id="db695-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="db695-128">如果您的 Azure SQL Database 伺服器忘記 hello 登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="db695-128">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db695-129">防火牆規則必須可供您執行本教學課程中的 hello 電腦的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="db695-129">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="db695-130">如果您在不同電腦上或有不同的公用 IP 位址，建立[伺服器層級防火牆規則使用 hello Azure 入口網站](sql-database-get-started-portal.md#create-a-server-level-firewall-rule)。</span><span class="sxs-lookup"><span data-stu-id="db695-130">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 

## <a name="create-a-nodejs-project"></a><span data-ttu-id="db695-131">建立 Node.js 專案</span><span class="sxs-lookup"><span data-stu-id="db695-131">Create a Node.js project</span></span>

<span data-ttu-id="db695-132">開啟命令提示字元，並建立名為 sqltest 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="db695-132">Open a command prompt and create a folder named *sqltest*.</span></span> <span data-ttu-id="db695-133">瀏覽您建立並執行下列命令的 hello toohello 資料夾：</span><span class="sxs-lookup"><span data-stu-id="db695-133">Navigate toohello folder you created and run hello following command:</span></span>

    
    npm init -y
    npm install tedious
    npm install async
    

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="db695-134">插入程式碼 tooquery SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="db695-134">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="db695-135">在您的開發環境或慣用的文字編輯器中，建立新的檔案 **sqltest.js**。</span><span class="sxs-lookup"><span data-stu-id="db695-135">In your development environment or favorite text editor, create a new file, **sqltest.js**.</span></span>

2. <span data-ttu-id="db695-136">以下列程式碼並新增值 hello 適當伺服器、 資料庫、 使用者及密碼的 hello 取代 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="db695-136">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```js
   var Connection = require('tedious').Connection;
   var Request = require('tedious').Request;

   // Create connection toodatabase
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

   // Attempt tooconnect and execute queries if connection goes through
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
      { console.log('Reading rows from hello Table...');

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

## <a name="run-hello-code"></a><span data-ttu-id="db695-137">執行 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="db695-137">Run hello code</span></span>

1. <span data-ttu-id="db695-138">在 hello 命令提示字元中執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="db695-138">At hello command prompt, run hello following commands:</span></span>

   ```js
   node sqltest.js
   ```

2. <span data-ttu-id="db695-139">請確認 hello 前 20 個資料列會傳回，，然後關閉 hello 應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="db695-139">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db695-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db695-140">Next steps</span></span>

- <span data-ttu-id="db695-141">深入了解 hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span><span class="sxs-lookup"><span data-stu-id="db695-141">Learn about hello [Microsoft Node.js Driver for SQL Server](https://docs.microsoft.com/sql/connect/node-js/node-js-driver-for-sql-server/)</span></span>
- <span data-ttu-id="db695-142">了解如何太[連接及查詢 Azure SQL database 使用.NET core](sql-database-connect-query-dotnet-core.md) Windows/Linux/macOS 上。</span><span class="sxs-lookup"><span data-stu-id="db695-142">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="db695-143">深入了解[開始使用 Windows/Linux/macOS 使用 hello 命令列上的.NET Core](/dotnet/core/tutorials/using-with-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="db695-143">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="db695-144">了解如何太[設計第一個 Azure SQL database 使用 SSMS](sql-database-design-first-database.md)或[設計第一個 Azure SQL database 使用.NET](sql-database-design-first-database-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="db695-144">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="db695-145">了解如何太[連接和查詢使用 SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="db695-145">Learn how too[Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="db695-146">了解如何太[連接和使用 Visual Studio 程式碼查詢](sql-database-connect-query-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="db695-146">Learn how too[Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>


