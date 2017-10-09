
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)http://portal.azure.com/ 在。
2. 在 hello 左邊的橫幅中，按一下 **瀏覽所有**。 hello**瀏覽**刀鋒視窗會顯示。
3. 捲動並按一下 [SQL Server] 。 hello **SQL 伺服器**刀鋒視窗會顯示。
   
    ![Hello 入口網站中尋找您的 Azure SQL Database 伺服器][b21-FindServerInPortal]
4. 為了方便起見，按一下 hello 控制項上稍早 hello 最小化**瀏覽**刀鋒視窗。
5. 在 hello 篩選文字方塊中，開始輸入 hello 伺服器的名稱。 即會顯示您的資料列。
6. 按一下您的伺服器 hello 資料列。 即會顯示您伺服器的刀鋒視窗。
7. 在伺服器刀鋒視窗中，按一下 [設定] 。 hello**設定**刀鋒視窗會顯示。
8. 按一下 [防火牆] 。 hello**防火牆設定**刀鋒視窗會顯示。
   
    ![按一下 [設定] > [防火牆]。][b31-SettingsFirewallNavig]
9. 按一下 [加入用戶端 IP] 。 Hello 第一個文字方塊中輸入新規則的名稱。
10. 型別在 hello 低和高 IP 位址，針對您想要的 hello 範圍值 tooenable。
    
    * 它可以是很方便 toohave hello 低值結尾為**.0**和 hello 與高**.255**。
    
    ![新增 IP 位址範圍 tooallow][b41-AddRange]
11. 按一下 [儲存] 。

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
