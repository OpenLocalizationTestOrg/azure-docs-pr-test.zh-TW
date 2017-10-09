## <a name="log-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站

登入 toohello [Azure 入口網站](https://portal.azure.com/)。

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a>建立空白的 SQL database 使用 hello Azure 入口網站

Azure SQL Database 會使用一組定義的[計算和儲存體資源](../articles/sql-database/sql-database-service-tiers.md)建立。 hello 資料庫內建立[Azure 資源群組](../articles/azure-resource-manager/resource-group-overview.md)和[Azure SQL Database 邏輯伺服器](../articles/sql-database/sql-database-features.md)。 

請遵循這些步驟 toocreate 空白的 SQL 資料庫。 

1. 按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。

2. 選取**資料庫**從 hello**新增**頁面上，並選取**SQL Database**從 hello**資料庫**頁面。 

   ![建立空白資料庫](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. 填寫 hello SQL Database 表單以下列資訊，hello hello 前面影像所示：   

   | 設定 | 建議的值 | 說明 |
   | --------| --------------- | ----------- | 
   | **資料庫名稱** | mySampleDatabase | 如需有效的資料庫名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。 | 
   | **訂用帳戶** | 您的訂用帳戶  | 如需訂用帳戶的詳細資訊，請參閱[訂用帳戶](https://account.windowsazure.com/Subscriptions)。 |
   | **資源群組** | myResourceGroup | 如需有效的資源群組名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。 |
   | **選取來源** | 空白資料庫 | 指定應建立空白資料庫。 |
   ||||

4. 按一下**伺服器**toocreate 及設定新的伺服器，為您新的資料庫。 填寫 hello**表單的新伺服器**以 hello 下列資訊： 

   | 設定 | 建議的值 | 說明 |
   | --------| --------------- | ----------- | 
   | **伺服器名稱** | 任何全域唯一名稱。 | 如需有效的伺服器名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。 | 
   | **伺服器管理員登入** | 任何有效名稱。 | 如需有效的登入名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。|
   | **密碼** | 任何有效密碼。 | 您的密碼必須至少為八個字元，且必須包含下列類別目錄的 hello 的其中三種字元： 大寫字母、 小寫字元、 數字和非英數字元。 |
   | **位置** | 任何有效位置。 | 如需區域的相關資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。 |
   ||||

   ![建立資料庫伺服器](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. 按一下 [選取] 。

6. 按一下**定價層**toospecify hello 服務層和效能層級的新資料庫。 針對此快速入門，選取 [20 DTUs (20 個 DTU)] 和 [250] GB 儲存體。

   ![建立資料庫-s1](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. 按一下 [Apply (套用)] 。  

8. 選取**定序**hello （適用於此教學課程中，使用 hello 預設值） 的空白資料庫。 如需定序的詳細資訊，請參閱[定序](https://docs.microsoft.com/sql/t-sql/statements/collations)。

9. 按一下**建立**tooprovision hello 資料庫。 提供有關分鐘半 toocomplete 採用。 

10. 在 [hello] 工具列上按一下**通知**toomonitor hello 部署程序。

   ![通知](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a>建立使用 hello Azure 入口網站的伺服器層級防火牆規則

hello SQL Database 服務會在 hello 伺服器層級建立防火牆。 一開始 hello 防火牆會阻止外部工具和應用程式從 toohello 伺服器或 tooany hello 伺服器上的資料庫連接。 之後建立 tooopen 特定 IP 位址的防火牆規則允許的連線。 請遵循這些步驟 toocreate [SQL Database 伺服器層級防火牆規則](../articles/sql-database/sql-database-firewall-configure.md)用戶端的 IP 位址和 tooenable hello SQL Database 防火牆的 IP 位址僅透過外部連線能力。 


> [!NOTE]
> Azure SQL Database 會透過連接埠 1433 通訊。 只有在您的網路的 hello 防火牆允許經由連接埠 1433年傳出流量之後，您可以連接 tooSQL 資料庫。


1. Hello 部署完成之後，請按一下**SQL 資料庫**從 hello 左側功能表，然後按一下**mySampleDatabase**上 hello **SQL 資料庫**頁面。 hello 概觀 頁面的資料庫會開啟，顯示您 hello 完全符合規定的伺服器名稱 (例如**mynewserver20170313.database.windows.net**)，並提供進一步組態的選項。 將這個完整伺服器名稱複製起來，以供稍後使用。

   > [!IMPORTANT]
   > 您需要此完整的伺服器名稱 tooconnect tooyour 伺服器和其後續的快速入門中的資料庫。
   > 

   ![伺服器名稱](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. 按一下**設定伺服器防火牆**hello 工具列 hello 如上圖所示。 hello**防火牆設定**hello SQL 資料庫伺服器 頁面隨即開啟。 

   ![伺服器防火牆規則](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. 按一下**新增用戶端 IP** hello 工具列 tooadd 上目前的 IP 位址 tooa 新防火牆規則。 防火牆規則可以針對單一 IP 位址或 IP 位址範圍開啟連接埠 1433。

4. 按一下 [儲存] 。 為開啟通訊埠 1433 hello 邏輯伺服器上的目前的 IP 位址建立伺服器層級防火牆規則。

   ![設定伺服器防火牆規則](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. 按一下**確定**，然後關閉 hello**防火牆設定**頁面。

您現在可以使用工具，例如 SQL Server Management Studio (SSMS) 連接 toohello Azure SQL Database 伺服器和資料庫。 hello 連接是來自此 IP 位址，並使用先前建立的 hello 伺服器系統管理員帳戶。


> [!IMPORTANT]
> 根據預設，透過 hello SQL Database 防火牆會啟用所有 Azure 服務。 按一下**OFF**上所有的 Azure 服務的這個頁面 toodisable。


## <a name="get-connection-string-values-using-hello-azure-portal"></a>取得使用 hello Azure 入口網站的連接字串值

取得 hello Azure 入口網站中的 hello Azure SQL Database 伺服器的完整的伺服器名稱。 您使用 hello 完整的伺服器名稱 tooconnect tooyour 伺服器使用 SQL Server Management Studio。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。

2. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 

3. 在 [hello **Essentials** hello Azure 入口網站頁面，為您的資料庫中] 窗格找到並複製 hello**伺服器名稱**。

   ![連線資訊](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
