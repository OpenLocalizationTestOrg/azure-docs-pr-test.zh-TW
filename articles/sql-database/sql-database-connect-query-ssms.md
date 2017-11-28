---
title: "SSMS: 在 Azure SQL Database 中連接和查詢資料 | Microsoft Docs"
description: "了解如何使用 SQL Server Management Studio (SSMS) 在 Azure 上連接到 SQL Database。 然後，執行 TRANSACT-SQL (T-SQL) 陳述式來查詢和編輯資料。"
metacanonical: 
keywords: "連接到 sql database,sql server management studio"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 2835a72fc90d1fd39af73c6907648908e5d9fdeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-to-connect-and-query-data"></a><span data-ttu-id="4084f-105">Azure SQL Database：使用 SQL Server Management Studio 連接及查詢資料</span><span class="sxs-lookup"><span data-stu-id="4084f-105">Azure SQL Database: Use SQL Server Management Studio to connect and query data</span></span>

<span data-ttu-id="4084f-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) 是整合式的環境，可用來管理任何 SQL 基礎結構，範圍從 Microsoft Windows 的 SQL Server 到 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4084f-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server to SQL Database for Microsoft Windows.</span></span> <span data-ttu-id="4084f-107">此快速入門示範如何使用 SSMS 來連線至 Azure SQL Database，然後使用 Transact-SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="4084f-107">This quick start demonstrates how to use SSMS to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4084f-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="4084f-108">Prerequisites</span></span>

<span data-ttu-id="4084f-109">本快速入門可做為在其中一個快速入門中建立之資源的起點︰</span><span class="sxs-lookup"><span data-stu-id="4084f-109">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="4084f-110">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="4084f-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="4084f-111">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="4084f-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="4084f-112">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="4084f-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="4084f-113">開始之前，確定您已安裝最新版的 [SSMS](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4084f-113">Before you start, make sure you have installed the newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="4084f-114">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="4084f-114">SQL server connection information</span></span>

<span data-ttu-id="4084f-115">取得連線到 Azure SQL Database 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="4084f-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="4084f-116">您在下一個程序中需要完整的伺服器名稱、資料庫名稱和登入資訊。</span><span class="sxs-lookup"><span data-stu-id="4084f-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="4084f-117">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="4084f-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4084f-118">從左側功能表中選取 [SQL Database]，按一下 [SQL Database]頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4084f-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="4084f-119">在您資料庫的 [概觀] 頁面上，檢閱如下圖所示的完整伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="4084f-119">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span></span> <span data-ttu-id="4084f-120">您可以將滑鼠移至伺服器名稱上，以帶出 [按一下以複製] 選項。</span><span class="sxs-lookup"><span data-stu-id="4084f-120">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![連線資訊](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="4084f-122">如果您忘記 Azure SQL Database 伺服器的登入資訊，請瀏覽至 [SQL Database 伺服器] 頁面來檢視伺服器系統管理員名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="4084f-122">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="connect-to-your-database"></a><span data-ttu-id="4084f-123">連接到您的資料庫</span><span class="sxs-lookup"><span data-stu-id="4084f-123">Connect to your database</span></span>

<span data-ttu-id="4084f-124">使用 SQL Server Management Studio (SSMS) 建立對 Azure SQL Database 伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="4084f-124">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4084f-125">Azure SQL Database 邏輯伺服器會接聽連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="4084f-125">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="4084f-126">如果您嘗試從公司防火牆連線至 Azure SQL Database 邏輯伺服器，則必須在公司防火牆中開啟此連接埠，您才能成功連線。</span><span class="sxs-lookup"><span data-stu-id="4084f-126">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

1. <span data-ttu-id="4084f-127">開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="4084f-127">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="4084f-128">在 [連接到伺服器] 對話方塊中，輸入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="4084f-128">In the **Connect to Server** dialog box, enter the following information:</span></span>

   | <span data-ttu-id="4084f-129">設定</span><span class="sxs-lookup"><span data-stu-id="4084f-129">Setting</span></span>       | <span data-ttu-id="4084f-130">建議的值</span><span class="sxs-lookup"><span data-stu-id="4084f-130">Suggested value</span></span> | <span data-ttu-id="4084f-131">說明</span><span class="sxs-lookup"><span data-stu-id="4084f-131">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="4084f-132">**伺服器類型**</span><span class="sxs-lookup"><span data-stu-id="4084f-132">**Server type**</span></span> | <span data-ttu-id="4084f-133">資料庫引擎</span><span class="sxs-lookup"><span data-stu-id="4084f-133">Database engine</span></span> | <span data-ttu-id="4084f-134">需要此值。</span><span class="sxs-lookup"><span data-stu-id="4084f-134">This value is required.</span></span> |
   | <span data-ttu-id="4084f-135">**伺服器名稱**</span><span class="sxs-lookup"><span data-stu-id="4084f-135">**Server name**</span></span> | <span data-ttu-id="4084f-136">完整伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="4084f-136">The fully qualified server name</span></span> | <span data-ttu-id="4084f-137">此名稱應該類似這樣︰**mynewserver20170313.database.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="4084f-137">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="4084f-138">**驗證**</span><span class="sxs-lookup"><span data-stu-id="4084f-138">**Authentication**</span></span> | <span data-ttu-id="4084f-139">SQL Server 驗證</span><span class="sxs-lookup"><span data-stu-id="4084f-139">SQL Server Authentication</span></span> | <span data-ttu-id="4084f-140">在本教學課程中，我們只設定了 SQL 驗證這個驗證類型。</span><span class="sxs-lookup"><span data-stu-id="4084f-140">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="4084f-141">**登入**</span><span class="sxs-lookup"><span data-stu-id="4084f-141">**Login**</span></span> | <span data-ttu-id="4084f-142">伺服器管理帳戶</span><span class="sxs-lookup"><span data-stu-id="4084f-142">The server admin account</span></span> | <span data-ttu-id="4084f-143">這是您在建立伺服器時所指定的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4084f-143">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="4084f-144">**密碼**</span><span class="sxs-lookup"><span data-stu-id="4084f-144">**Password**</span></span> | <span data-ttu-id="4084f-145">伺服器管理帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="4084f-145">The password for your server admin account</span></span> | <span data-ttu-id="4084f-146">這是您在建立伺服器時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="4084f-146">This is the password that you specified when you created the server.</span></span> |

   ![連接到伺服器](./media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="4084f-148">按一下 [連接到伺服器] 對話方塊中的 [選項]。</span><span class="sxs-lookup"><span data-stu-id="4084f-148">Click **Options** in the **Connect to server** dialog box.</span></span> <span data-ttu-id="4084f-149">在 [連線到資料庫] 區段中，輸入 **mySampleDatabase** 以連線到這個資料庫。</span><span class="sxs-lookup"><span data-stu-id="4084f-149">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span></span>

   ![連線到伺服器上的 DB](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="4084f-151">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="4084f-151">Click **Connect**.</span></span> <span data-ttu-id="4084f-152">[物件總管] 視窗隨即在 SSMS 中開啟。</span><span class="sxs-lookup"><span data-stu-id="4084f-152">The Object Explorer window opens in SSMS.</span></span> 

   ![已連接到伺服器](./media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="4084f-154">在 [物件總管] 中，展開 [資料庫]，然後展開 [mySampleDatabase] 以檢視範例資料庫中的物件。</span><span class="sxs-lookup"><span data-stu-id="4084f-154">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="4084f-155">查詢資料</span><span class="sxs-lookup"><span data-stu-id="4084f-155">Query data</span></span>

<span data-ttu-id="4084f-156">使用下列程式碼，可藉由使用 [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL 陳述式來依照類別查詢前 20 項產品。</span><span class="sxs-lookup"><span data-stu-id="4084f-156">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4084f-157">在 [物件總管] 中，於 **mySampleDatabase** 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="4084f-157">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="4084f-158">隨即開啟已連線到您資料庫的空白查詢視窗。</span><span class="sxs-lookup"><span data-stu-id="4084f-158">A blank query window opens that is connected to your database.</span></span>
2. <span data-ttu-id="4084f-159">在查詢視窗中，輸入下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="4084f-159">In the query window, enter the following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="4084f-160">在工具列上，按一下 [執行] 來擷取 Product 和 ProductCategory 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="4084f-160">On the toolbar, click **Execute** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="4084f-162">插入資料</span><span class="sxs-lookup"><span data-stu-id="4084f-162">Insert data</span></span>

<span data-ttu-id="4084f-163">使用下列程式碼，藉由使用 [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL 陳述式將新產品插入 SalesLT.Product 資料表中。</span><span class="sxs-lookup"><span data-stu-id="4084f-163">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4084f-164">在查詢視窗中，以下列查詢取代先前的查詢︰</span><span class="sxs-lookup"><span data-stu-id="4084f-164">In the query window, replace the previous query with the following query:</span></span>

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. <span data-ttu-id="4084f-165">在工具列上，按一下 [執行] 以在Product 資料表中插入新資料列。</span><span class="sxs-lookup"><span data-stu-id="4084f-165">On the toolbar, click **Execute**  to insert a new row in the Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="4084f-166">更新資料</span><span class="sxs-lookup"><span data-stu-id="4084f-166">Update data</span></span>

<span data-ttu-id="4084f-167">使用下列程式碼，藉由使用 [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL 陳述式更新您先前新增的產品。</span><span class="sxs-lookup"><span data-stu-id="4084f-167">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4084f-168">在查詢視窗中，以下列查詢取代先前的查詢︰</span><span class="sxs-lookup"><span data-stu-id="4084f-168">In the query window, replace the previous query with the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="4084f-169">在工具列上，按一下 [執行] 以在Product 資料表中更新指定的資料列。</span><span class="sxs-lookup"><span data-stu-id="4084f-169">On the toolbar, click **Execute** to update the specified row in the Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="4084f-170">刪除資料</span><span class="sxs-lookup"><span data-stu-id="4084f-170">Delete data</span></span>

<span data-ttu-id="4084f-171">使用下列程式碼，藉由使用 [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL 陳述式刪除您先前新增的產品。</span><span class="sxs-lookup"><span data-stu-id="4084f-171">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="4084f-172">在查詢視窗中，以下列查詢取代先前的查詢︰</span><span class="sxs-lookup"><span data-stu-id="4084f-172">In the query window, replace the previous query with the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="4084f-173">在工具列上，按一下 [執行] 以在Product 資料表中刪除指定的資料列。</span><span class="sxs-lookup"><span data-stu-id="4084f-173">On the toolbar, click **Execute** to delete the specified row in the Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="4084f-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4084f-174">Next steps</span></span>

- <span data-ttu-id="4084f-175">關於使用 Transact-SQL 建立及管理伺服器和資料庫，請參閱[深入了解 Azure SQL Database 伺服器和資料庫](sql-database-servers-databases.md)。</span><span class="sxs-lookup"><span data-stu-id="4084f-175">To learn about creating and managing servers and databases with Transact-SQL, see [Learn about Azure SQL Database servers and databases](sql-database-servers-databases.md).</span></span>
- <span data-ttu-id="4084f-176">如需有關 SSMS 的資訊，請參閱 [使用 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4084f-176">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="4084f-177">若要使用 Visual Studio Code 進行連線和查詢，請參閱[使用 Visual Studio Code 進行連線和查詢](sql-database-connect-query-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="4084f-177">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="4084f-178">若要使用 .NET 進行連線和查詢，請參閱[使用 .NET 進行連線和查詢](sql-database-connect-query-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="4084f-178">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="4084f-179">若要使用 PHP 進行連線和查詢，請參閱[使用 PHP 進行連線和查詢](sql-database-connect-query-php.md)。</span><span class="sxs-lookup"><span data-stu-id="4084f-179">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="4084f-180">若要使用 Node.js 進行連線和查詢，請參閱[使用 Node.js 進行連線和查詢](sql-database-connect-query-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="4084f-180">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="4084f-181">若要使用 Java 進行連線和查詢，請參閱[使用 Java 進行連線和查詢](sql-database-connect-query-java.md)。</span><span class="sxs-lookup"><span data-stu-id="4084f-181">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="4084f-182">若要使用 Python 進行連線和查詢，請參閱[使用 Python 進行連線和查詢](sql-database-connect-query-python.md)。</span><span class="sxs-lookup"><span data-stu-id="4084f-182">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="4084f-183">若要使用 Ruby 進行連線和查詢，請參閱[使用 Ruby 進行連線和查詢](sql-database-connect-query-ruby.md)。</span><span class="sxs-lookup"><span data-stu-id="4084f-183">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
