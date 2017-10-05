---
title: "VS Code：在 Azure SQL Database 中連接和查詢資料 | Microsoft Docs"
description: "了解如何使用 Visual Studio Code 在 Azure 上連接到 SQL Database。 然後，執行 TRANSACT-SQL (T-SQL) 陳述式來查詢和編輯資料。"
metacanonical: 
keywords: "連線到 SQL Database"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: 4076b1e7ab3a70009217a1deff72da4bff0dc871
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-use-visual-studio-code-to-connect-and-query-data"></a><span data-ttu-id="c42d1-105">Azure SQL Database︰使用 Visual Studio Code 連接及查詢資料</span><span class="sxs-lookup"><span data-stu-id="c42d1-105">Azure SQL Database: Use Visual Studio Code to connect and query data</span></span>

<span data-ttu-id="c42d1-106">[Visual Studio Code](https://code.visualstudio.com/docs) 是一個圖形化程式碼編輯器，適用於支援擴充功能的 Linux、macOS 和 Windows，包括可供查詢 Microsoft SQL Server、Azure SQL Database 和 SQL 資料倉儲的 [mssql extension](https://aka.ms/mssql-marketplace)。</span><span class="sxs-lookup"><span data-stu-id="c42d1-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="c42d1-107">此快速入門示範如何使用 Visual Studio Code 來連線至 Azure SQL Database，然後使用 Transact-SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="c42d1-107">This quick start demonstrates how to use Visual Studio Code to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c42d1-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c42d1-108">Prerequisites</span></span>

<span data-ttu-id="c42d1-109">本快速入門可做為在其中一個快速入門中建立之資源的起點︰</span><span class="sxs-lookup"><span data-stu-id="c42d1-109">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="c42d1-110">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="c42d1-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="c42d1-111">建立 DB - CLI</span><span class="sxs-lookup"><span data-stu-id="c42d1-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="c42d1-112">建立 DB - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c42d1-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="c42d1-113">開始之前，確定您已安裝最新版的 [Visual Studio Code](https://code.visualstudio.com/Download) 並已載入 [mssql 擴充功能](https://aka.ms/mssql-marketplace)。</span><span class="sxs-lookup"><span data-stu-id="c42d1-113">Before you start, make sure you have installed the newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded the [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="c42d1-114">如需 mssql 擴充功能的安裝指引，請參閱[安裝 VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code)和[適用於 Visual Studio Code 的 mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)。</span><span class="sxs-lookup"><span data-stu-id="c42d1-114">For installation guidance for the mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="c42d1-115">設定 VS Code</span><span class="sxs-lookup"><span data-stu-id="c42d1-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="c42d1-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="c42d1-116">**Mac OS**</span></span>
<span data-ttu-id="c42d1-117">對於 macOS，您必須安裝 OpenSSL，這是 mssql 擴充功能使用之 DotNet Core 的必要條件。</span><span class="sxs-lookup"><span data-stu-id="c42d1-117">For macOS, you need to install OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="c42d1-118">開啟您的終端機，並輸入下列命令以安裝 **brew** 和 **OpenSSL**。</span><span class="sxs-lookup"><span data-stu-id="c42d1-118">Open your terminal and enter the following commands to install **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="c42d1-119">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="c42d1-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="c42d1-120">不需要特別設定。</span><span class="sxs-lookup"><span data-stu-id="c42d1-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="c42d1-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="c42d1-121">**Windows**</span></span>

<span data-ttu-id="c42d1-122">不需要特別設定。</span><span class="sxs-lookup"><span data-stu-id="c42d1-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="c42d1-123">SQL Server 連線資訊</span><span class="sxs-lookup"><span data-stu-id="c42d1-123">SQL server connection information</span></span>

<span data-ttu-id="c42d1-124">取得連線到 Azure SQL Database 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="c42d1-124">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="c42d1-125">您在下一個程序中需要完整的伺服器名稱、資料庫名稱和登入資訊。</span><span class="sxs-lookup"><span data-stu-id="c42d1-125">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="c42d1-126">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="c42d1-126">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c42d1-127">從左側功能表中選取 [SQL Database]，按一下 [SQL Database]頁面上您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c42d1-127">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="c42d1-128">在您資料庫的 [概觀] 頁面上，檢閱如下圖所示的完整伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="c42d1-128">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="c42d1-129">您可以將滑鼠移至伺服器名稱上，以帶出 [按一下以複製] 選項。</span><span class="sxs-lookup"><span data-stu-id="c42d1-129">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![連線資訊](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="c42d1-131">如果您忘記 Azure SQL Database 伺服器的登入資訊，請瀏覽至 [SQL Database 伺服器] 頁面來檢視伺服器系統管理員名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="c42d1-131">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="set-language-mode-to-sql"></a><span data-ttu-id="c42d1-132">將語言模式設定為 SQL</span><span class="sxs-lookup"><span data-stu-id="c42d1-132">Set language mode to SQL</span></span>

<span data-ttu-id="c42d1-133">在 Visual Studio Code 中將語言模式設定為 **SQL**，以啟用 mssql 命令和 T-SQL IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="c42d1-133">Set the language mode is set to **SQL** in Visual Studio Code to enable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="c42d1-134">開啟新的 Visual Studio Code 視窗。</span><span class="sxs-lookup"><span data-stu-id="c42d1-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="c42d1-135">按一下狀態列右下角的 [純文字]。</span><span class="sxs-lookup"><span data-stu-id="c42d1-135">Click **Plain Text** in the lower right-hand corner of the status bar.</span></span>
3. <span data-ttu-id="c42d1-136">在開啟的 [選取語言模式] 下拉式功能表中，輸入 **SQL**，然後按 **ENTER** 將語言模式設定為 SQL。</span><span class="sxs-lookup"><span data-stu-id="c42d1-136">In the **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** to set the language mode to SQL.</span></span> 

   ![SQL 語言模式](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-to-your-database"></a><span data-ttu-id="c42d1-138">連接到您的資料庫</span><span class="sxs-lookup"><span data-stu-id="c42d1-138">Connect to your database</span></span>

<span data-ttu-id="c42d1-139">使用 Visual Studio Code 建立對 Azure SQL Database 伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="c42d1-139">Use Visual Studio Code to establish a connection to your Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c42d1-140">在繼續之前，確定您已備妥伺服器、資料庫和登入資訊。</span><span class="sxs-lookup"><span data-stu-id="c42d1-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="c42d1-141">開始輸入連線設定檔資訊後，如果您的焦點變換自 Visual Studio Code，則必須重新開始建立連線設定檔。</span><span class="sxs-lookup"><span data-stu-id="c42d1-141">Once you begin entering the connection profile information, if you change your focus from Visual Studio Code, you have to restart creating the connection profile.</span></span>
>

1. <span data-ttu-id="c42d1-142">在 VS Code 中，按 **CTRL+SHIFT+P** (或 **F1**) 以開啟命令選擇區。</span><span class="sxs-lookup"><span data-stu-id="c42d1-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) to open the Command Palette.</span></span>

2. <span data-ttu-id="c42d1-143">輸入 **sqlcon** 並且按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="c42d1-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="c42d1-144">按 **ENTER** 以選取 [建立連線設定檔]。</span><span class="sxs-lookup"><span data-stu-id="c42d1-144">Press **ENTER** to select **Create Connection Profile**.</span></span> <span data-ttu-id="c42d1-145">這會為您的 SQL Server 執行個體建立連線設定檔。</span><span class="sxs-lookup"><span data-stu-id="c42d1-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="c42d1-146">請依照提示指定新連線設定檔的連線屬性。</span><span class="sxs-lookup"><span data-stu-id="c42d1-146">Follow the prompts to specify the connection properties for the new connection profile.</span></span> <span data-ttu-id="c42d1-147">指定每個值之後，按 **ENTER** 繼續。</span><span class="sxs-lookup"><span data-stu-id="c42d1-147">After specifying each value, press **ENTER** to continue.</span></span> 

   | <span data-ttu-id="c42d1-148">設定</span><span class="sxs-lookup"><span data-stu-id="c42d1-148">Setting</span></span>       | <span data-ttu-id="c42d1-149">建議的值</span><span class="sxs-lookup"><span data-stu-id="c42d1-149">Suggested value</span></span> | <span data-ttu-id="c42d1-150">說明</span><span class="sxs-lookup"><span data-stu-id="c42d1-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="c42d1-151">**伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="c42d1-151">**Server name</span></span> | <span data-ttu-id="c42d1-152">完整伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="c42d1-152">The fully qualified server name</span></span> | <span data-ttu-id="c42d1-153">此名稱應該類似這樣︰**mynewserver20170313.database.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="c42d1-153">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="c42d1-154">**資料庫名稱**</span><span class="sxs-lookup"><span data-stu-id="c42d1-154">**Database name**</span></span> | <span data-ttu-id="c42d1-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="c42d1-155">mySampleDatabase</span></span> | <span data-ttu-id="c42d1-156">所要連線的目標資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="c42d1-156">The name of the database to which to connect.</span></span> |
   | <span data-ttu-id="c42d1-157">**驗證**</span><span class="sxs-lookup"><span data-stu-id="c42d1-157">**Authentication**</span></span> | <span data-ttu-id="c42d1-158">SQL 登入</span><span class="sxs-lookup"><span data-stu-id="c42d1-158">SQL Login</span></span>| <span data-ttu-id="c42d1-159">在本教學課程中，我們只設定了 SQL 驗證這個驗證類型。</span><span class="sxs-lookup"><span data-stu-id="c42d1-159">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="c42d1-160">**使用者名稱**</span><span class="sxs-lookup"><span data-stu-id="c42d1-160">**User name**</span></span> | <span data-ttu-id="c42d1-161">伺服器管理帳戶</span><span class="sxs-lookup"><span data-stu-id="c42d1-161">The server admin account</span></span> | <span data-ttu-id="c42d1-162">這是您在建立伺服器時所指定的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c42d1-162">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="c42d1-163">**密碼 (SQL 登入)**</span><span class="sxs-lookup"><span data-stu-id="c42d1-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="c42d1-164">伺服器管理帳戶的密碼</span><span class="sxs-lookup"><span data-stu-id="c42d1-164">The password for your server admin account</span></span> | <span data-ttu-id="c42d1-165">這是您在建立伺服器時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="c42d1-165">This is the password that you specified when you created the server.</span></span> |
   | <span data-ttu-id="c42d1-166">**儲存密碼？**</span><span class="sxs-lookup"><span data-stu-id="c42d1-166">**Save Password?**</span></span> | <span data-ttu-id="c42d1-167">是或否</span><span class="sxs-lookup"><span data-stu-id="c42d1-167">Yes or No</span></span> | <span data-ttu-id="c42d1-168">如果您不希望每次都要輸入密碼，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="c42d1-168">Select Yes if you do not want to enter the password each time.</span></span> |
   | <span data-ttu-id="c42d1-169">**輸入這個設定檔的名稱**</span><span class="sxs-lookup"><span data-stu-id="c42d1-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="c42d1-170">設定檔名稱，例如 **mySampleDatabase**</span><span class="sxs-lookup"><span data-stu-id="c42d1-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="c42d1-171">儲存設定檔名稱可讓您在後續登入時加快連線速度。</span><span class="sxs-lookup"><span data-stu-id="c42d1-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="c42d1-172">按 **ESC** 鍵來關閉通知已建立並連接設定檔的資訊訊息。</span><span class="sxs-lookup"><span data-stu-id="c42d1-172">Press the **ESC** key to close the info message that informs you that the profile is created and connected.</span></span>

6. <span data-ttu-id="c42d1-173">在狀態列中確認您的連線。</span><span class="sxs-lookup"><span data-stu-id="c42d1-173">Verify your connection in the status bar.</span></span>

   ![連線狀態](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="c42d1-175">查詢資料</span><span class="sxs-lookup"><span data-stu-id="c42d1-175">Query data</span></span>

<span data-ttu-id="c42d1-176">使用下列程式碼，可藉由使用 [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL 陳述式來依照類別查詢前 20 項產品。</span><span class="sxs-lookup"><span data-stu-id="c42d1-176">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="c42d1-177">在 [編輯器] 視窗中，於空白查詢視窗中輸入下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="c42d1-177">In the **Editor** window, enter the following query in the empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="c42d1-178">按 **CTRL+SHIFT+E** 來擷取 Product 和 ProductCategory 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="c42d1-178">Press **CTRL+SHIFT+E** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![查詢](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="c42d1-180">插入資料</span><span class="sxs-lookup"><span data-stu-id="c42d1-180">Insert data</span></span>

<span data-ttu-id="c42d1-181">使用下列程式碼，藉由使用 [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL 陳述式將新產品插入 SalesLT.Product 資料表中。</span><span class="sxs-lookup"><span data-stu-id="c42d1-181">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="c42d1-182">在 [編輯器] 視窗中，刪除先前的查詢並輸入下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="c42d1-182">In the **Editor** window, delete the previous query and enter the following query:</span></span>

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

2. <span data-ttu-id="c42d1-183">按 **CTRL+SHIFT+E** 以在 Product 資料表中插入新資料列。</span><span class="sxs-lookup"><span data-stu-id="c42d1-183">Press **CTRL+SHIFT+E** to insert a new row in the Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="c42d1-184">更新資料</span><span class="sxs-lookup"><span data-stu-id="c42d1-184">Update data</span></span>

<span data-ttu-id="c42d1-185">使用下列程式碼，藉由使用 [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL 陳述式更新您先前新增的產品。</span><span class="sxs-lookup"><span data-stu-id="c42d1-185">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="c42d1-186">在 [編輯器] 視窗中，刪除先前的查詢並輸入下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="c42d1-186">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="c42d1-187">按 **CTRL+SHIFT+E** 以在 Product 資料表中更新指定的資料列。</span><span class="sxs-lookup"><span data-stu-id="c42d1-187">Press **CTRL+SHIFT+E** to update the specified row in the Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="c42d1-188">刪除資料</span><span class="sxs-lookup"><span data-stu-id="c42d1-188">Delete data</span></span>

<span data-ttu-id="c42d1-189">使用下列程式碼，藉由使用 [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL 陳述式刪除您先前新增的產品。</span><span class="sxs-lookup"><span data-stu-id="c42d1-189">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="c42d1-190">在 [編輯器] 視窗中，刪除先前的查詢並輸入下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="c42d1-190">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="c42d1-191">按 **CTRL+SHIFT+E** 以在 Product 資料表中刪除指定的資料列。</span><span class="sxs-lookup"><span data-stu-id="c42d1-191">Press **CTRL+SHIFT+E** to delete the specified row in the Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c42d1-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c42d1-192">Next steps</span></span>

- <span data-ttu-id="c42d1-193">若要使用 SQL Server Management Studio 來連線和查詢，請參閱[使用 SSMS 連線及查詢](sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="c42d1-193">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="c42d1-194">如需有關使用 Visual Studio Code 的 MSDN 雜誌文章，請參閱[使用 MSSQL 擴充功能建立資料庫 IDE 部落格文章](https://msdn.microsoft.com/magazine/mt809115)。</span><span class="sxs-lookup"><span data-stu-id="c42d1-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
