### <a name="prerequisites"></a>必要條件
* Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)
* [Azure SQL Database](../articles/sql-database/sql-database-get-started.md)以及其連接資訊，包括 hello 伺服器名稱、 資料庫名稱和使用者名稱/密碼。 這項資訊包含在 hello SQL 資料庫連接字串：
  
    Server=tcp:*yoursqlservername*.database.windows.net,1433;Initial Catalog=*yourqldbname*;Persist Security Info=False;User ID={your_username};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
  
    深入了解 [Azure SQL Database](https://azure.microsoft.com/services/sql-database)。

> [!NOTE]
> 當您建立 Azure SQL Database 時，您也可以建立隨附 SQL hello 範例資料庫。 
> 
> 

之前使用 Azure SQL Database 邏輯應用程式中，連接 tooyour SQL 資料庫。 您可以輕鬆地在 hello Azure 入口網站應用程式邏輯中。  

連接的 tooyour Azure SQL Database 使用 hello 下列步驟：  

1. 建立邏輯應用程式。 在 hello Logic Apps 設計工具加入觸發程序，然後再加入動作。 選取**顯示 Microsoft managed Api**在 hello 下拉式清單中，然後輸入"sql"hello [搜尋] 方塊中。 選取其中一個 hello 動作：  
   
    ![SQL Azure 連接建立步驟](./media/connectors-create-api-sqlazure/sql-actions.png)
2. 如果您先前尚未建立任何連線 tooSQL 資料庫，會提示您輸入 hello 連接詳細資料：  
   
    ![SQL Azure 連接建立步驟](./media/connectors-create-api-sqlazure/connection-details.png) 
3. 輸入 hello SQL 資料庫詳細資料。 具有星號的屬性為必要項目。
   
   | 屬性 | 詳細資料 |
   | --- | --- |
   | 透過閘道連線 |讓此屬性保持未核取狀態。 當連接 tooan 內部部署 SQL Server，會使用這項目。 |
   | 連線名稱 * |為連接器輸入任何名稱。 |
   | SQL Server 名稱 * |輸入 hello 伺服器名稱。這會像下面*servername.database.windows.net*。 hello 伺服器名稱會顯示在 hello hello Azure 入口網站中的 SQL 資料庫屬性，並且也會顯示 hello 連接字串中。 |
   | SQL Database 名稱 * |輸入 hello 您提供給您的 SQL 資料庫的名稱。 這會列在 hello hello 連接字串中的 SQL 資料庫屬性： Initial Catalog =*yoursqldbname*。 |
   | 使用者名稱 * |輸入 hello hello SQL 資料庫建立時，您建立的使用者名稱。 這會列在 hello hello Azure 入口網站中的 SQL 資料庫屬性。 |
   | 密碼 * |輸入 hello hello SQL 資料庫建立時，您建立的密碼。 |
   
    這些認證是使用的 tooauthorize 您邏輯應用程式 tooconnect，並存取 SQL 資料。 完成後，您的連線詳細資料看起來類似 toohello 下列：  
   
    ![SQL Azure 連接建立步驟](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. 選取 [ **建立**]。 
5. 請注意 hello 連線已建立。 現在，繼續進行其他 hello 邏輯應用程式中的步驟： 
   
    ![SQL Azure 連接建立步驟](./media/connectors-create-api-sqlazure/table.png)

