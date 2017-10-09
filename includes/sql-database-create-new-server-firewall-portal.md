
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立伺服器層級防火牆規則

1. 在 hello SQL 伺服器刀鋒視窗中，在 設定 上按一下**防火牆**hello SQL server 的 tooopen hello 防火牆刀鋒視窗。

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. 檢閱顯示 hello 用戶端 IP 位址及驗證這是您在 hello 使用您選擇的瀏覽器的網際網路上的 IP 位址 （要求 「 什麼是我的 IP 位址）。 偶爾會因為各種原因而不相符。

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. 假設符合 hello IP 位址，按一下**新增用戶端 IP** hello 工具列上。

    ![新增用戶端 IP](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > 您可以開啟 hello hello 伺服器 tooa 單一 IP 位址上的 SQL Database 防火牆或整個範圍的位址。 開啟 hello 防火牆啟用 SQL 系統管理員和使用者 toologin tooany 資料庫 hello 伺服器 toowhich 它們具有有效的認證。
    >

4. 按一下**儲存**在 hello 工具列 toosave 此伺服器層級防火牆規則，然後按一下**確定**。

    ![新增用戶端 IP](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> 如需教學課程，請參閱 [SQL Database 教學課程︰建立伺服器、伺服器層級防火牆規則、範例資料庫、資料庫層級防火牆規則，以及與 SQL Server 連接](../articles/sql-database/sql-database-get-started.md)。    
>
