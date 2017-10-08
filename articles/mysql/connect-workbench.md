---
title: "從 MySQL Workbench MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門提供 hello 步驟 toouse MySQL Workbench tooconnect 和查詢資料從 Azure 資料庫的 MySQL。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="ae25a-103">Azure 資料庫的 MySQL： 使用 MySQL Workbench tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="ae25a-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="ae25a-104">本快速入門示範如何使用 MySQL tooconnect tooan Azure Database hello MySQL Workbench 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae25a-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ae25a-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="ae25a-105">Prerequisites</span></span>
<span data-ttu-id="ae25a-106">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="ae25a-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="ae25a-107">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ae25a-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="ae25a-108">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ae25a-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="ae25a-109">安裝 MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="ae25a-109">Install MySQL Workbench</span></span>
<span data-ttu-id="ae25a-110">下載並安裝在您的電腦上的 MySQL Workbench [hello MySQL 網站](https://dev.mysql.com/downloads/workbench/)。</span><span class="sxs-lookup"><span data-stu-id="ae25a-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="ae25a-111">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="ae25a-111">Get connection information</span></span>
<span data-ttu-id="ae25a-112">取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ae25a-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="ae25a-113">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="ae25a-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="ae25a-114">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="ae25a-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="ae25a-115">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="ae25a-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="ae25a-116">按一下 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="ae25a-116">Click hello server name.</span></span>

4. <span data-ttu-id="ae25a-117">選取 hello 伺服器**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="ae25a-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="ae25a-118">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="ae25a-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Azure Database for MySQL 伺服器名稱](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="ae25a-120">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="ae25a-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="ae25a-121">使用 MySQL Workbench toohello 伺服器連接</span><span class="sxs-lookup"><span data-stu-id="ae25a-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="ae25a-122">使用 hello GUI 工具 MySQL Workbench tooconnect tooAzure MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="ae25a-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="ae25a-123">啟動 hello MySQL 工作臺電腦上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae25a-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="ae25a-124">在**設定新連線**對話方塊方塊中，輸入下列資訊在 hello hello**參數** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="ae25a-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![設定新連線](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="ae25a-126">**設定**</span><span class="sxs-lookup"><span data-stu-id="ae25a-126">**Setting**</span></span> | <span data-ttu-id="ae25a-127">**建議的值**</span><span class="sxs-lookup"><span data-stu-id="ae25a-127">**Suggested value**</span></span> | <span data-ttu-id="ae25a-128">**欄位描述**</span><span class="sxs-lookup"><span data-stu-id="ae25a-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="ae25a-129">連線名稱</span><span class="sxs-lookup"><span data-stu-id="ae25a-129">Connection Name</span></span> | <span data-ttu-id="ae25a-130">示範連線</span><span class="sxs-lookup"><span data-stu-id="ae25a-130">Demo Connection</span></span> | <span data-ttu-id="ae25a-131">指定此連線的標籤。</span><span class="sxs-lookup"><span data-stu-id="ae25a-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="ae25a-132">連線方式</span><span class="sxs-lookup"><span data-stu-id="ae25a-132">Connection Method</span></span> | <span data-ttu-id="ae25a-133">標準 (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="ae25a-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="ae25a-134">標準 (TCP/IP) 就足夠了。</span><span class="sxs-lookup"><span data-stu-id="ae25a-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="ae25a-135">主機名稱</span><span class="sxs-lookup"><span data-stu-id="ae25a-135">Hostname</span></span> | <span data-ttu-id="ae25a-136">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="ae25a-136">*server name*</span></span> | <span data-ttu-id="ae25a-137">指定您 hello Azure 資料庫的 MySQL 稍早建立時所用的 hello 的伺服器名稱值。</span><span class="sxs-lookup"><span data-stu-id="ae25a-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="ae25a-138">顯示的範例伺服器是 myserver4demo.mysql.database.azure.com。使用 hello 完整的網域名稱 (\*。 mysql.database.azure.com) hello 範例所示。</span><span class="sxs-lookup"><span data-stu-id="ae25a-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="ae25a-139">如果您不記得您的伺服器名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ae25a-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="ae25a-140">Port</span><span class="sxs-lookup"><span data-stu-id="ae25a-140">Port</span></span> | <span data-ttu-id="ae25a-141">3306</span><span class="sxs-lookup"><span data-stu-id="ae25a-141">3306</span></span> | <span data-ttu-id="ae25a-142">一律使用連接埠 3306 的 MySQL 連接 tooAzure 資料庫時。</span><span class="sxs-lookup"><span data-stu-id="ae25a-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="ae25a-143">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="ae25a-143">Username</span></span> |  <span data-ttu-id="ae25a-144">伺服器管理員登入名稱</span><span class="sxs-lookup"><span data-stu-id="ae25a-144">*server admin login name*</span></span> | <span data-ttu-id="ae25a-145">輸入的 hello 伺服器系統管理員登入密碼時您建立 hello Azure 資料庫的 MySQL 稍早所提供。</span><span class="sxs-lookup"><span data-stu-id="ae25a-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="ae25a-146">我們的範例使用者名稱為 myadmin@myserver4demo。</span><span class="sxs-lookup"><span data-stu-id="ae25a-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="ae25a-147">如果您不記得 hello 使用者名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ae25a-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="ae25a-148">hello 格式是 *username@servername* 。</span><span class="sxs-lookup"><span data-stu-id="ae25a-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="ae25a-149">密碼</span><span class="sxs-lookup"><span data-stu-id="ae25a-149">Password</span></span> | <span data-ttu-id="ae25a-150">您的密碼</span><span class="sxs-lookup"><span data-stu-id="ae25a-150">your password</span></span> | <span data-ttu-id="ae25a-151">按一下**保存庫中的存放區...**按鈕 toosave hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="ae25a-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="ae25a-152">按一下**測試連接**tootest 如果已正確設定所有參數。</span><span class="sxs-lookup"><span data-stu-id="ae25a-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="ae25a-153">按一下**確定**toosave hello 連線。</span><span class="sxs-lookup"><span data-stu-id="ae25a-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="ae25a-154">在 hello 清單**MySQL 連線**，按一下 hello 圖格對應 tooyour 伺服器，然後等候 hello 連接 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ae25a-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="ae25a-155">新的 SQL 索引標籤隨即開啟並出現空白的編輯器，可供您輸入查詢。</span><span class="sxs-lookup"><span data-stu-id="ae25a-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae25a-156">根據預設，需要 SSL 連線安全性，而且會在適用於 MySQL 伺服器的 Azure 資料庫上強制執行。</span><span class="sxs-lookup"><span data-stu-id="ae25a-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="ae25a-157">通常則 MySQL Workbench tooconnect tooyour 伺服器需要使用 SSL 憑證沒有其他組態。</span><span class="sxs-lookup"><span data-stu-id="ae25a-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="ae25a-158">如需有關 SSL 的詳細資訊，請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](./howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="ae25a-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="ae25a-159">如果您需要 toodisable SSL，請瀏覽 hello Azure 入口網站，然後按一下 hello 連線安全性頁面 toodisable hello 強制的 SSL 連接切換按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae25a-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="ae25a-160">建立資料表、將資料插入、讀取資料、更新資料、刪除資料</span><span class="sxs-lookup"><span data-stu-id="ae25a-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="ae25a-161">複製並貼到空白的 [SQL] 索引標籤 tooillustrate 一些範例資料的 hello 範例 SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="ae25a-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="ae25a-162">這段程式碼會建立名為 quickstartdb 的空白資料庫，然後會建立名為 inventory 的範例資料表。</span><span class="sxs-lookup"><span data-stu-id="ae25a-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="ae25a-163">它會插入一些資料列，然後讀取 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="ae25a-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="ae25a-164">會變更 hello 資料與 update 陳述式，並在讀取 hello 資料列一次。</span><span class="sxs-lookup"><span data-stu-id="ae25a-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="ae25a-165">最後會刪除資料列，然後再次讀取 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="ae25a-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
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

    <span data-ttu-id="ae25a-166">執行完畢後，hello 螢幕擷取畫面會顯示 hello SQL 程式碼的範例 SQL Workbench 和 hello 輸出中。</span><span class="sxs-lookup"><span data-stu-id="ae25a-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![MySQL Workbench [SQL] 索引標籤 toorun SQL 程式碼範例](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="ae25a-168">toorun hello 範例 SQL 程式碼中，按一下 [lightening 閃電圖示的 hello hello 工具列中的 hello **SQL 檔案**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ae25a-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="ae25a-169">請注意 hello 三個索引標籤式的導致 hello**結果方格**hello 頁面 hello 中間區段。</span><span class="sxs-lookup"><span data-stu-id="ae25a-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="ae25a-170">請注意 hello**輸出**在 hello hello 頁面底部的清單。</span><span class="sxs-lookup"><span data-stu-id="ae25a-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="ae25a-171">顯示每個命令的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="ae25a-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="ae25a-172">現在，您用於使用 MySQL Workbench MySQL tooAzure 資料庫連接並查詢使用 hello SQL 語言的資料。</span><span class="sxs-lookup"><span data-stu-id="ae25a-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae25a-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae25a-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ae25a-174">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="ae25a-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
