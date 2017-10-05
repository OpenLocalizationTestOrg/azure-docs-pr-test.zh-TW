---
title: "從 MySQL Workbench 連線到 Azure Database for MySQL | Microsoft Docs"
description: "本快速入門提供的步驟，可以使用 MySQL Workbench 來連線及查詢 Azure Database for MySQL 的資料。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: 20a1f31ce42abb924504c4008f85420fc49aec89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a><span data-ttu-id="58a8d-103">Azure Database for MySQL︰使用 MySQL Workbench 來連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="58a8d-103">Azure Database for MySQL: Use MySQL Workbench to connect and query data</span></span>
<span data-ttu-id="58a8d-104">本快速入門示範如何使用 MySQL Workbench 應用程式來連線到 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="58a8d-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using the MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="58a8d-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="58a8d-105">Prerequisites</span></span>
<span data-ttu-id="58a8d-106">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="58a8d-106">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="58a8d-107">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="58a8d-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="58a8d-108">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="58a8d-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="58a8d-109">安裝 MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="58a8d-109">Install MySQL Workbench</span></span>
<span data-ttu-id="58a8d-110">從 [MySQL 網站](https://dev.mysql.com/downloads/workbench/)下載 MySQL Workbench，並安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="58a8d-110">Download and install MySQL Workbench on your computer from [the MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="58a8d-111">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="58a8d-111">Get connection information</span></span>
<span data-ttu-id="58a8d-112">取得連線到 Azure Database for MySQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="58a8d-112">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="58a8d-113">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="58a8d-113">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="58a8d-114">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="58a8d-114">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="58a8d-115">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您所建立的伺服器，例如 **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="58a8d-115">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="58a8d-116">按一下伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="58a8d-116">Click the server name.</span></span>

4. <span data-ttu-id="58a8d-117">選取伺服器的 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="58a8d-117">Select the server's **Properties** page.</span></span> <span data-ttu-id="58a8d-118">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="58a8d-118">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Azure Database for MySQL 伺服器名稱](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="58a8d-120">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面來檢視伺服器管理員登入名稱，並視需要重設密碼。</span><span class="sxs-lookup"><span data-stu-id="58a8d-120">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-to-the-server-using-mysql-workbench"></a><span data-ttu-id="58a8d-121">使用 MySQL Workbench 來連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="58a8d-121">Connect to the server using MySQL Workbench</span></span> 
<span data-ttu-id="58a8d-122">若要使用 GUI 工具 MySQL Workbench 連線到 Azure MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="58a8d-122">To connect to Azure MySQL server using the GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="58a8d-123">在您的電腦上啟動 MySQL Workbench 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58a8d-123">Launch the MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="58a8d-124">在 [設定新連線] 對話方塊的 [參數] 索引標籤上輸入下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="58a8d-124">In **Setup New Connection** dialog box, enter the following information on the **Parameters** tab:</span></span>

    ![設定新連線](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="58a8d-126">**設定**</span><span class="sxs-lookup"><span data-stu-id="58a8d-126">**Setting**</span></span> | <span data-ttu-id="58a8d-127">**建議的值**</span><span class="sxs-lookup"><span data-stu-id="58a8d-127">**Suggested value**</span></span> | <span data-ttu-id="58a8d-128">**欄位描述**</span><span class="sxs-lookup"><span data-stu-id="58a8d-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="58a8d-129">連線名稱</span><span class="sxs-lookup"><span data-stu-id="58a8d-129">Connection Name</span></span> | <span data-ttu-id="58a8d-130">示範連線</span><span class="sxs-lookup"><span data-stu-id="58a8d-130">Demo Connection</span></span> | <span data-ttu-id="58a8d-131">指定此連線的標籤。</span><span class="sxs-lookup"><span data-stu-id="58a8d-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="58a8d-132">連線方式</span><span class="sxs-lookup"><span data-stu-id="58a8d-132">Connection Method</span></span> | <span data-ttu-id="58a8d-133">標準 (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="58a8d-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="58a8d-134">標準 (TCP/IP) 就足夠了。</span><span class="sxs-lookup"><span data-stu-id="58a8d-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="58a8d-135">主機名稱</span><span class="sxs-lookup"><span data-stu-id="58a8d-135">Hostname</span></span> | <span data-ttu-id="58a8d-136">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="58a8d-136">*server name*</span></span> | <span data-ttu-id="58a8d-137">指定您稍早建立 Azure Database for MySQL 時所使用的伺服器名稱值。</span><span class="sxs-lookup"><span data-stu-id="58a8d-137">Specify the server name value that was used when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="58a8d-138">顯示的範例伺服器是 myserver4demo.mysql.database.azure.com。使用如範例所示的完整網域名稱 (\*.mysql.database.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="58a8d-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use the fully qualified domain name (\*.mysql.database.azure.com) as shown in the example.</span></span> <span data-ttu-id="58a8d-139">如果您不記得您的伺服器名稱，請依照上一節中的步驟執行，以取得連線資訊。</span><span class="sxs-lookup"><span data-stu-id="58a8d-139">Follow the steps in the previous section to get the connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="58a8d-140">Port</span><span class="sxs-lookup"><span data-stu-id="58a8d-140">Port</span></span> | <span data-ttu-id="58a8d-141">3306</span><span class="sxs-lookup"><span data-stu-id="58a8d-141">3306</span></span> | <span data-ttu-id="58a8d-142">連線至 Azure Database for MySQL 時一律使用連接埠 3306。</span><span class="sxs-lookup"><span data-stu-id="58a8d-142">Always use port 3306 when connecting to Azure Database for MySQL.</span></span> |
    | <span data-ttu-id="58a8d-143">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="58a8d-143">Username</span></span> |  <span data-ttu-id="58a8d-144">伺服器管理員登入名稱</span><span class="sxs-lookup"><span data-stu-id="58a8d-144">*server admin login name*</span></span> | <span data-ttu-id="58a8d-145">輸入您稍早建立 Azure Database for MySQL 時所提供的伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="58a8d-145">Type in the server admin login username supplied when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="58a8d-146">我們的範例使用者名稱為 myadmin@myserver4demo。</span><span class="sxs-lookup"><span data-stu-id="58a8d-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="58a8d-147">如果您不記得使用者名稱，請依照上一節中的步驟執行，以取得連線資訊。</span><span class="sxs-lookup"><span data-stu-id="58a8d-147">Follow the steps in the previous section to get the connection information if you do not remember the username.</span></span> <span data-ttu-id="58a8d-148">格式為 *username@servername*。</span><span class="sxs-lookup"><span data-stu-id="58a8d-148">The format is *username@servername*.</span></span>
    | <span data-ttu-id="58a8d-149">密碼</span><span class="sxs-lookup"><span data-stu-id="58a8d-149">Password</span></span> | <span data-ttu-id="58a8d-150">您的密碼</span><span class="sxs-lookup"><span data-stu-id="58a8d-150">your password</span></span> | <span data-ttu-id="58a8d-151">按一下 [儲存在保存庫...] 按鈕以儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="58a8d-151">Click **Store in Vault...** button to save the password.</span></span> |

3.   <span data-ttu-id="58a8d-152">按一下 [測試連線] 以測試所有參數是否都已設定正確。</span><span class="sxs-lookup"><span data-stu-id="58a8d-152">Click **Test Connection** to test if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="58a8d-153">按一下 [確定] 可儲存連線。</span><span class="sxs-lookup"><span data-stu-id="58a8d-153">Click **OK** to save the connection.</span></span> 

5.   <span data-ttu-id="58a8d-154">在 [MySQL 連線] 清單中，按一下對應至您伺服器的圖格，並等候建立連線。</span><span class="sxs-lookup"><span data-stu-id="58a8d-154">In the listing of **MySQL Connections**, click the tile corresponding to your server and wait for the connection to be established.</span></span>

6.   <span data-ttu-id="58a8d-155">新的 SQL 索引標籤隨即開啟並出現空白的編輯器，可供您輸入查詢。</span><span class="sxs-lookup"><span data-stu-id="58a8d-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="58a8d-156">根據預設，需要 SSL 連線安全性，而且會在適用於 MySQL 伺服器的 Azure 資料庫上強制執行。</span><span class="sxs-lookup"><span data-stu-id="58a8d-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="58a8d-157">一般而言，您不需要對 SSL 憑證進行其他設定，就能讓 MySQL Workbench 連線到您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="58a8d-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench to connect to your server.</span></span> <span data-ttu-id="58a8d-158">如需 SSL 的詳細資訊，請參閱[在您的應用程式中設定 SSL 連線能力，以安全地連線至適用於 MySQL 的 Azure 資料庫](./howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="58a8d-158">For more information on SSL, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="58a8d-159">如果您需要停用 SSL，請前往 Azure 入口網站，然後按一下 [連線安全性] 頁面，以停用 [強制執行 SSL 連線] 切換按鈕。</span><span class="sxs-lookup"><span data-stu-id="58a8d-159">If you need to disable SSL, visit the Azure portal and click the Connection security page to disable the Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="58a8d-160">建立資料表、將資料插入、讀取資料、更新資料、刪除資料</span><span class="sxs-lookup"><span data-stu-id="58a8d-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="58a8d-161">將範例 SQL 程式碼複製並貼到空白的 SQL 索引標籤，來說明某些範例資料。</span><span class="sxs-lookup"><span data-stu-id="58a8d-161">Copy and paste the sample SQL code into a blank SQL tab to illustrate some sample data.</span></span>

    <span data-ttu-id="58a8d-162">這段程式碼會建立名為 quickstartdb 的空白資料庫，然後會建立名為 inventory 的範例資料表。</span><span class="sxs-lookup"><span data-stu-id="58a8d-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="58a8d-163">它會插入一些資料列，然後讀取資料列。</span><span class="sxs-lookup"><span data-stu-id="58a8d-163">It inserts some rows, then reads the rows.</span></span> <span data-ttu-id="58a8d-164">它會使用 update 陳述式將資料進行變更，並再次讀取資料列。</span><span class="sxs-lookup"><span data-stu-id="58a8d-164">It changes the data with an update statement, and reads the rows again.</span></span> <span data-ttu-id="58a8d-165">最後會刪除資料列，然後再次讀取資料列。</span><span class="sxs-lookup"><span data-stu-id="58a8d-165">Finally it deletes a row, and reads the rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="58a8d-166">執行完畢後，螢幕擷取畫面會在 SQL Workbench 中顯示 SQL 程式碼的範例和輸出。</span><span class="sxs-lookup"><span data-stu-id="58a8d-166">The screenshot shows an example of the SQL code in SQL Workbench and the output after it has been run.</span></span>
    
    ![執行範例 SQL 程式碼的 MySQL Workbench SQL 索引標籤](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="58a8d-168">若要執行範例 SQL 程式碼，請在 [SQL 檔案] 索引標籤的工具列中按一下閃電圖示。</span><span class="sxs-lookup"><span data-stu-id="58a8d-168">To run the sample SQL Code, click the lightening bolt icon in the toolbar of the **SQL File** tab.</span></span>
3. <span data-ttu-id="58a8d-169">請注意頁面中間的 [結果方格] 區段中的三個索引標籤式結果。</span><span class="sxs-lookup"><span data-stu-id="58a8d-169">Notice the three tabbed results in the **Result Grid** section in the middle of the page.</span></span> 
4. <span data-ttu-id="58a8d-170">請注意頁面底部的 [輸出] 清單。</span><span class="sxs-lookup"><span data-stu-id="58a8d-170">Notice the **Output** list at the bottom of the page.</span></span> <span data-ttu-id="58a8d-171">隨即顯示每個命令的狀態。</span><span class="sxs-lookup"><span data-stu-id="58a8d-171">The status of each command is shown.</span></span> 

<span data-ttu-id="58a8d-172">現在，您已使用 MySQL Workbench 連線到 Azure Database for MySQL，並使用 SQL 語言查詢資料。</span><span class="sxs-lookup"><span data-stu-id="58a8d-172">Now, you have connected to Azure Database for MySQL using MySQL Workbench, and have queried data using the SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58a8d-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58a8d-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="58a8d-174">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="58a8d-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
