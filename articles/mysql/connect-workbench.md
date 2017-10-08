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
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>Azure 資料庫的 MySQL： 使用 MySQL Workbench tooconnect 和查詢資料
本快速入門示範如何使用 MySQL tooconnect tooan Azure Database hello MySQL Workbench 應用程式。 

## <a name="prerequisites"></a>必要條件
本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：
- [使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>安裝 MySQL Workbench
下載並安裝在您的電腦上的 MySQL Workbench [hello MySQL 網站](https://dev.mysql.com/downloads/workbench/)。

## <a name="get-connection-information"></a>取得連線資訊
取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。 您需要 hello 完整的伺服器名稱和登入認證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。

2. 在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**myserver4demo**。

3. 按一下 hello 伺服器名稱。

4. 選取 hello 伺服器**屬性**頁面。 請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。

 ![Azure Database for MySQL 伺服器名稱](./media/connect-workbench/1-server-properties-name-login.png)
 
5. 如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。

## <a name="connect-toohello-server-using-mysql-workbench"></a>使用 MySQL Workbench toohello 伺服器連接 
使用 hello GUI 工具 MySQL Workbench tooconnect tooAzure MySQL 伺服器：

1.  啟動 hello MySQL 工作臺電腦上的應用程式。 

2.  在**設定新連線**對話方塊方塊中，輸入下列資訊在 hello hello**參數** 索引標籤：

    ![設定新連線](./media/connect-workbench/2-setup-new-connection.png)

    | **設定** | **建議的值** | **欄位描述** |
    |---|---|---|
    |   連線名稱 | 示範連線 | 指定此連線的標籤。 |
    | 連線方式 | 標準 (TCP/IP) | 標準 (TCP/IP) 就足夠了。 |
    | 主機名稱 | 伺服器名稱 | 指定您 hello Azure 資料庫的 MySQL 稍早建立時所用的 hello 的伺服器名稱值。 顯示的範例伺服器是 myserver4demo.mysql.database.azure.com。使用 hello 完整的網域名稱 (\*。 mysql.database.azure.com) hello 範例所示。 如果您不記得您的伺服器名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。  |
    | Port | 3306 | 一律使用連接埠 3306 的 MySQL 連接 tooAzure 資料庫時。 |
    | 使用者名稱 |  伺服器管理員登入名稱 | 輸入的 hello 伺服器系統管理員登入密碼時您建立 hello Azure 資料庫的 MySQL 稍早所提供。 我們的範例使用者名稱為 myadmin@myserver4demo。 如果您不記得 hello 使用者名稱，請遵循 hello 前一個區段 tooget hello 連接資訊中的 hello 步驟。 hello 格式是 *username@servername* 。
    | 密碼 | 您的密碼 | 按一下**保存庫中的存放區...**按鈕 toosave hello 密碼。 |

3.   按一下**測試連接**tootest 如果已正確設定所有參數。 

4.   按一下**確定**toosave hello 連線。 

5.   在 hello 清單**MySQL 連線**，按一下 hello 圖格對應 tooyour 伺服器，然後等候 hello 連接 toobe 建立。

6.   新的 SQL 索引標籤隨即開啟並出現空白的編輯器，可供您輸入查詢。

    > [!NOTE]
    > 根據預設，需要 SSL 連線安全性，而且會在適用於 MySQL 伺服器的 Azure 資料庫上強制執行。 通常則 MySQL Workbench tooconnect tooyour 伺服器需要使用 SSL 憑證沒有其他組態。 如需有關 SSL 的詳細資訊，請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](./howto-configure-ssl.md)。  如果您需要 toodisable SSL，請瀏覽 hello Azure 入口網站，然後按一下 hello 連線安全性頁面 toodisable hello 強制的 SSL 連接切換按鈕。

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>建立資料表、將資料插入、讀取資料、更新資料、刪除資料
1. 複製並貼到空白的 [SQL] 索引標籤 tooillustrate 一些範例資料的 hello 範例 SQL 程式碼。

    這段程式碼會建立名為 quickstartdb 的空白資料庫，然後會建立名為 inventory 的範例資料表。 它會插入一些資料列，然後讀取 hello 資料列。 會變更 hello 資料與 update 陳述式，並在讀取 hello 資料列一次。 最後會刪除資料列，然後再次讀取 hello 資料列。
    
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

    執行完畢後，hello 螢幕擷取畫面會顯示 hello SQL 程式碼的範例 SQL Workbench 和 hello 輸出中。
    
    ![MySQL Workbench [SQL] 索引標籤 toorun SQL 程式碼範例](media/connect-workbench/3-workbench-sql-tab.png)

2. toorun hello 範例 SQL 程式碼中，按一下 [lightening 閃電圖示的 hello hello 工具列中的 hello **SQL 檔案**] 索引標籤。
3. 請注意 hello 三個索引標籤式的導致 hello**結果方格**hello 頁面 hello 中間區段。 
4. 請注意 hello**輸出**在 hello hello 頁面底部的清單。 顯示每個命令的 hello 狀態。 

現在，您用於使用 MySQL Workbench MySQL tooAzure 資料庫連接並查詢使用 hello SQL 語言的資料。

## <a name="next-steps"></a>後續步驟
> [!div class="nextstepaction"]
> [使用匯出和匯入來移轉資料庫](./concepts-migrate-import-export.md)
