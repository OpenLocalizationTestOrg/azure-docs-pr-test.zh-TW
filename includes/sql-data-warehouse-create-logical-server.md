### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立新的邏輯 SQL server

1. 按一下 [新增]，搜尋**邏輯伺服器**，然後按 **ENTER**。

    ![搜尋邏輯伺服器](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. 選取 [SQL Server (邏輯伺服器)] 

    ![選取邏輯伺服器](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. 按一下**建立**tooopen hello 新 SQL Server （邏輯伺服器） 刀鋒視窗。

   <kbd>![開啟刀鋒視窗中的邏輯伺服器](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![邏輯伺服器刀鋒視窗](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. 在 hello SQL Server （邏輯伺服器） 刀鋒視窗中的伺服器名稱 文字方塊中，提供新的邏輯伺服器 hello 的有效名稱。 綠色核取記號指示您提供的名稱有效。
    
    ![新的伺服器名稱](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > hello 適用於您的新伺服器的完整格式的名稱將會 < your_server_name >。.database.windows.net。
    >
    
4. 在 hello 伺服器系統管理員登入文字方塊中，提供此伺服器 hello SQL 驗證登入的使用者名稱。 此登入稱為 hello 伺服器主體的登入。 綠色核取記號指示您提供的名稱有效。
    
    ![SQL 管理員登入](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. 在 hello**密碼**和**確認密碼**文字方塊中，提供 hello 伺服器主體的登入帳戶的密碼。 綠色核取記號指示您提供的密碼有效。
    
    ![SQL 管理員密碼](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. 選取您擁有的權限 toocreate 物件的訂閱。

    ![訂用帳戶](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. 在 hello 資源群組 文字方塊中，選取 **建立新**然後，在 hello 資源群組 文字方塊中，提供 hello 新的資源群組 （您也可以使用現有的資源群組如果您已經建立自己的其中一個） 的有效名稱。 綠色核取記號指示您提供的名稱有效。

    ![新的資源群組](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. 在 [hello**位置**] 文字方塊中，選取一個資料中心適當 tooyour 位置-例如"澳洲東部"。
    
    ![伺服器位置](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > hello 核取方塊**允許 azure 服務 tooaccess 伺服器**此刀鋒視窗上不能變更。 您可以變更此設定在 hello 伺服器防火牆刀鋒視窗上。 如需詳細資訊，請參閱[安全性入門](../articles/sql-database/sql-database-manage-servers-portal.md)。
    >
    
9. 按一下 [建立] 。

    ![建立按鈕](./media/sql-data-warehouse-create-logical-server/create.png)

