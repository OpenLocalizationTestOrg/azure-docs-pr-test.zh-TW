---
title: "SSMS: 在 Azure SQL Database 中連接和查詢資料 | Microsoft Docs"
description: "深入了解如何 tooconnect tooSQL 資料庫在 Azure 上使用 SQL Server Management Studio (SSMS)。 然後，執行 TRANSACT-SQL (T-SQL) 陳述式 tooquery 和編輯資料。"
metacanonical: 
keywords: "連接 toosql 資料庫，sql server management studio"
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
ms.openlocfilehash: 769a3a1ecc34800bd345b64e89841f7147b144f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-sql-server-management-studio-tooconnect-and-query-data"></a><span data-ttu-id="b08a6-105">Azure SQL Database： 使用 SQL Server Management Studio tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="b08a6-105">Azure SQL Database: Use SQL Server Management Studio tooconnect and query data</span></span>

<span data-ttu-id="b08a6-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) 是用於管理任何 SQL 基礎結構，從 SQL Server tooSQL 資料庫的 Microsoft Windows 整合式的環境。</span><span class="sxs-lookup"><span data-stu-id="b08a6-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span> <span data-ttu-id="b08a6-107">本快速入門示範如何 toouse SSMS tooconnect tooan Azure SQL database，然後再使用 TRANSACT-SQL 陳述式 tooquery，插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="b08a6-107">This quick start demonstrates how toouse SSMS tooconnect tooan Azure SQL database, and then use Transact-SQL statements tooquery, insert, update, and delete data in hello database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b08a6-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="b08a6-108">Prerequisites</span></span>

<span data-ttu-id="b08a6-109">本快速入門會使用為其起始點 hello 的資源建立在其中一個這些快速入門：</span><span class="sxs-lookup"><span data-stu-id="b08a6-109">This quick start uses as its starting point hello resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="b08a6-110">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="b08a6-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="b08a6-111">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="b08a6-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="b08a6-112">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b08a6-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="b08a6-113">開始之前，請確定您已安裝最新版本的中 hello [SSMS](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-113">Before you start, make sure you have installed hello newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="b08a6-114">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="b08a6-114">SQL server connection information</span></span>

<span data-ttu-id="b08a6-115">收到 hello 連線所需的資訊 tooconnect toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="b08a6-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="b08a6-116">您需要 hello 完整的伺服器名稱、 資料庫名稱，以及 hello 下一個程序中的登入資訊。</span><span class="sxs-lookup"><span data-stu-id="b08a6-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="b08a6-117">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b08a6-118">選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="b08a6-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="b08a6-119">在 hello**概觀**為您的資料庫頁面上，檢閱 hello 完整的伺服器名稱，如 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="b08a6-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello image below.</span></span> <span data-ttu-id="b08a6-120">您可以將滑鼠停留在 hello 伺服器名稱 toobring 向上 hello**按一下 toocopy**選項。</span><span class="sxs-lookup"><span data-stu-id="b08a6-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>

   ![連線資訊](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="b08a6-122">如果您的 Azure SQL Database 伺服器忘記 hello 登入資訊，請瀏覽 toohello SQL 資料庫伺服器頁面 tooview hello 伺服器管理員的名稱，如有需要，重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b08a6-122">If you have forgotten hello login information for your Azure SQL Database server, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span> 

## <a name="connect-tooyour-database"></a><span data-ttu-id="b08a6-123">連接 tooyour 資料庫</span><span class="sxs-lookup"><span data-stu-id="b08a6-123">Connect tooyour database</span></span>

<span data-ttu-id="b08a6-124">使用 SQL Server Management Studio tooestablish 連接 tooyour Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b08a6-124">Use SQL Server Management Studio tooestablish a connection tooyour Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b08a6-125">Azure SQL Database 邏輯伺服器會接聽連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="b08a6-125">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="b08a6-126">如果您正嘗試 tooconnect tooan Azure SQL Database 邏輯伺服器從公司防火牆內，此連接埠必須在 hello 公司防火牆中開啟您 toosuccessfully 連線。</span><span class="sxs-lookup"><span data-stu-id="b08a6-126">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

1. <span data-ttu-id="b08a6-127">開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="b08a6-127">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="b08a6-128">在 hello**連接 tooServer**對話方塊方塊中，輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="b08a6-128">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="b08a6-129">設定</span><span class="sxs-lookup"><span data-stu-id="b08a6-129">Setting</span></span>       | <span data-ttu-id="b08a6-130">建議的值</span><span class="sxs-lookup"><span data-stu-id="b08a6-130">Suggested value</span></span> | <span data-ttu-id="b08a6-131">說明</span><span class="sxs-lookup"><span data-stu-id="b08a6-131">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="b08a6-132">**伺服器類型**</span><span class="sxs-lookup"><span data-stu-id="b08a6-132">**Server type**</span></span> | <span data-ttu-id="b08a6-133">資料庫引擎</span><span class="sxs-lookup"><span data-stu-id="b08a6-133">Database engine</span></span> | <span data-ttu-id="b08a6-134">需要此值。</span><span class="sxs-lookup"><span data-stu-id="b08a6-134">This value is required.</span></span> |
   | <span data-ttu-id="b08a6-135">**伺服器名稱**</span><span class="sxs-lookup"><span data-stu-id="b08a6-135">**Server name**</span></span> | <span data-ttu-id="b08a6-136">hello 完整的伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="b08a6-136">hello fully qualified server name</span></span> | <span data-ttu-id="b08a6-137">hello 名稱應該像下面這樣： **mynewserver20170313.database.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="b08a6-137">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="b08a6-138">**驗證**</span><span class="sxs-lookup"><span data-stu-id="b08a6-138">**Authentication**</span></span> | <span data-ttu-id="b08a6-139">SQL Server 驗證</span><span class="sxs-lookup"><span data-stu-id="b08a6-139">SQL Server Authentication</span></span> | <span data-ttu-id="b08a6-140">SQL 驗證是我們已在此教學課程中的 hello 唯一的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="b08a6-140">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="b08a6-141">**登入**</span><span class="sxs-lookup"><span data-stu-id="b08a6-141">**Login**</span></span> | <span data-ttu-id="b08a6-142">hello 伺服器系統管理員帳戶</span><span class="sxs-lookup"><span data-stu-id="b08a6-142">hello server admin account</span></span> | <span data-ttu-id="b08a6-143">這是您指定當您建立 hello 伺服器 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b08a6-143">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="b08a6-144">**密碼**</span><span class="sxs-lookup"><span data-stu-id="b08a6-144">**Password**</span></span> | <span data-ttu-id="b08a6-145">hello 伺服器系統管理員帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="b08a6-145">hello password for your server admin account</span></span> | <span data-ttu-id="b08a6-146">這是您指定當您建立 hello 伺服器 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b08a6-146">This is hello password that you specified when you created hello server.</span></span> |

   ![連接 tooserver](./media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="b08a6-148">按一下**選項**在 hello**連接 tooserver**  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b08a6-148">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="b08a6-149">在 hello**連接 toodatabase**區段中，輸入**mySampleDatabase** tooconnect toothis 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b08a6-149">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![連接的伺服器上的 toodb](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="b08a6-151">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="b08a6-151">Click **Connect**.</span></span> <span data-ttu-id="b08a6-152">在 SSMS 中，開啟 hello 物件總管 視窗。</span><span class="sxs-lookup"><span data-stu-id="b08a6-152">hello Object Explorer window opens in SSMS.</span></span> 

   ![連接的 tooserver](./media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="b08a6-154">在 物件總管 中，展開**資料庫**，然後展開  **mySampleDatabase** tooview hello 範例資料庫中的 hello 物件。</span><span class="sxs-lookup"><span data-stu-id="b08a6-154">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="b08a6-155">查詢資料</span><span class="sxs-lookup"><span data-stu-id="b08a6-155">Query data</span></span>

<span data-ttu-id="b08a6-156">使用 hello 下列程式碼 tooquery 的 hello 前 20 個產品類別目錄使用 hello[選取](https://msdn.microsoft.com/library/ms189499.aspx)TRANSACT-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b08a6-156">Use hello following code tooquery for hello top 20 products by category using hello [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="b08a6-157">在 物件總管 中，於 **mySampleDatabase** 上按一下滑鼠右鍵，然後按一下新增查詢。</span><span class="sxs-lookup"><span data-stu-id="b08a6-157">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="b08a6-158">空白查詢視窗，也就是開啟連接的 tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b08a6-158">A blank query window opens that is connected tooyour database.</span></span>
2. <span data-ttu-id="b08a6-159">在 hello 查詢視窗中，輸入下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="b08a6-159">In hello query window, enter hello following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="b08a6-160">在 [hello] 工具列上按一下**Execute** tooretrieve hello Product 和 ProductCategory 資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="b08a6-160">On hello toolbar, click **Execute** tooretrieve data from hello Product and ProductCategory tables.</span></span>

    ![query](./media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="b08a6-162">插入資料</span><span class="sxs-lookup"><span data-stu-id="b08a6-162">Insert data</span></span>

<span data-ttu-id="b08a6-163">使用 hello 下列程式碼會 tooinsert 新產品到 hello SalesLT.Product 資料表使用 hello[插入](https://msdn.microsoft.com/library/ms174335.aspx)TRANSACT-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b08a6-163">Use hello following code tooinsert a new product into hello SalesLT.Product table using hello [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="b08a6-164">在 hello 查詢視窗中，取代 hello 下列查詢中的 hello 上一個查詢：</span><span class="sxs-lookup"><span data-stu-id="b08a6-164">In hello query window, replace hello previous query with hello following query:</span></span>

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

2. <span data-ttu-id="b08a6-165">在 [hello] 工具列上按一下**Execute** tooinsert hello Product 資料表中的新資料列。</span><span class="sxs-lookup"><span data-stu-id="b08a6-165">On hello toolbar, click **Execute**  tooinsert a new row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="b08a6-166">更新資料</span><span class="sxs-lookup"><span data-stu-id="b08a6-166">Update data</span></span>

<span data-ttu-id="b08a6-167">使用 hello 下列程式碼 tooupdate hello 新產品您先前加入使用 hello[更新](https://msdn.microsoft.com/library/ms177523.aspx)TRANSACT-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b08a6-167">Use hello following code tooupdate hello new product that you previously added using hello [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="b08a6-168">在 hello 查詢視窗中，取代 hello 下列查詢中的 hello 上一個查詢：</span><span class="sxs-lookup"><span data-stu-id="b08a6-168">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="b08a6-169">在 [hello] 工具列上按一下**Execute** tooupdate hello 指定的資料列 hello Product 資料表中。</span><span class="sxs-lookup"><span data-stu-id="b08a6-169">On hello toolbar, click **Execute** tooupdate hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="b08a6-170">刪除資料</span><span class="sxs-lookup"><span data-stu-id="b08a6-170">Delete data</span></span>

<span data-ttu-id="b08a6-171">使用 hello 下列程式碼 toodelete hello 新產品您先前加入使用 hello[刪除](https://msdn.microsoft.com/library/ms189835.aspx)TRANSACT-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b08a6-171">Use hello following code toodelete hello new product that you previously added using hello [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="b08a6-172">在 hello 查詢視窗中，取代 hello 下列查詢中的 hello 上一個查詢：</span><span class="sxs-lookup"><span data-stu-id="b08a6-172">In hello query window, replace hello previous query with hello following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="b08a6-173">在 [hello] 工具列上按一下**Execute** toodelete hello 指定的資料列 hello Product 資料表中。</span><span class="sxs-lookup"><span data-stu-id="b08a6-173">On hello toolbar, click **Execute** toodelete hello specified row in hello Product table.</span></span>

    <img src="./media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="b08a6-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b08a6-174">Next steps</span></span>

- <span data-ttu-id="b08a6-175">toolearn 有關建立和管理伺服器和資料庫使用 TRANSACT-SQL，請參閱[深入了解 Azure SQL Database 伺服器和資料庫](sql-database-servers-databases.md)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-175">toolearn about creating and managing servers and databases with Transact-SQL, see [Learn about Azure SQL Database servers and databases](sql-database-servers-databases.md).</span></span>
- <span data-ttu-id="b08a6-176">如需有關 SSMS 的資訊，請參閱 [使用 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-176">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="b08a6-177">tooconnect 和查詢中使用 Visual Studio 程式碼，請參閱[連接和使用 Visual Studio 程式碼查詢](sql-database-connect-query-vscode.md)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-177">tooconnect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="b08a6-178">tooconnect 和查詢中使用.NET 中，請參閱[連接和查詢的.NET](sql-database-connect-query-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-178">tooconnect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="b08a6-179">tooconnect 及查詢使用 PHP 時，請參閱[連接和查詢使用 PHP](sql-database-connect-query-php.md)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-179">tooconnect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="b08a6-180">tooconnect 及查詢使用 Node.js，請參閱[連接和查詢使用 Node.js](sql-database-connect-query-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-180">tooconnect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="b08a6-181">tooconnect 及查詢使用 Java，請參閱[連接和查詢使用 Java](sql-database-connect-query-java.md)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-181">tooconnect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="b08a6-182">tooconnect 和查詢中使用 Python，請參閱[連接和查詢使用 Python](sql-database-connect-query-python.md)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-182">tooconnect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="b08a6-183">tooconnect 及查詢使用 Ruby，請參閱[連接和查詢 Ruby](sql-database-connect-query-ruby.md)。</span><span class="sxs-lookup"><span data-stu-id="b08a6-183">tooconnect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
