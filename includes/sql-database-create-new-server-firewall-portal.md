
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="502c9-101">在 hello Azure 入口網站中建立伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="502c9-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="502c9-102">在 hello SQL 伺服器刀鋒視窗中，在 設定 上按一下**防火牆**hello SQL server 的 tooopen hello 防火牆刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="502c9-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="502c9-103">檢閱顯示 hello 用戶端 IP 位址及驗證這是您在 hello 使用您選擇的瀏覽器的網際網路上的 IP 位址 （要求 「 什麼是我的 IP 位址）。</span><span class="sxs-lookup"><span data-stu-id="502c9-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="502c9-104">偶爾會因為各種原因而不相符。</span><span class="sxs-lookup"><span data-stu-id="502c9-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="502c9-105">假設符合 hello IP 位址，按一下**新增用戶端 IP** hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="502c9-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![新增用戶端 IP](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="502c9-107">您可以開啟 hello hello 伺服器 tooa 單一 IP 位址上的 SQL Database 防火牆或整個範圍的位址。</span><span class="sxs-lookup"><span data-stu-id="502c9-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="502c9-108">開啟 hello 防火牆啟用 SQL 系統管理員和使用者 toologin tooany 資料庫 hello 伺服器 toowhich 它們具有有效的認證。</span><span class="sxs-lookup"><span data-stu-id="502c9-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="502c9-109">按一下**儲存**在 hello 工具列 toosave 此伺服器層級防火牆規則，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="502c9-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![新增用戶端 IP](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="502c9-111">如需教學課程，請參閱 [SQL Database 教學課程︰建立伺服器、伺服器層級防火牆規則、範例資料庫、資料庫層級防火牆規則，以及與 SQL Server 連接](../articles/sql-database/sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="502c9-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
