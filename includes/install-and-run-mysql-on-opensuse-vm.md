
1. 類型的 tooescalate 權限：
   
        sudo -s
   
    輸入您的密碼。
2. tooinstall MySQL Community 伺服器版本中，輸入：
   
        zypper install mysql-community-server
   
    等待 MySQL 進行下載和安裝。
3. tooset MySQL toostart hello 系統開機時，輸入：
   
        insserv mysql
4. 此命令，手動啟動 hello MySQL 服務精靈 (mysqld):
   
        rcmysql start
   
    hello MySQL 服務精靈，型別 toocheck hello 狀態：
   
        rcmysql status
   
    toostop hello MySQL 服務精靈中，輸入：
   
        rcmysql stop
   
   > [!IMPORTANT]
   > 安裝完成後，hello MySQL 根密碼預設是空的。 建議您執行 **mysql\_secure\_installation**，該指令碼有助於保護 MySQL 的安全。 hello 指令碼會提示您 toochange hello MySQL 根密碼、 移除匿名使用者帳戶、 停用遠端根目錄登入，測試資料庫，重新載入 hello 權限的資料表。 我們建議您回答 [是] tooall 這些選項，並變更 hello 根密碼。
   > 
   > 
5. 輸入此 toorun hello 指令碼 MySQL 安裝指令碼：
   
        mysql_secure_installation
6. 登入 tooMySQL:
   
        mysql -u root -p
   
    輸入 hello MySQL 根目錄 （您變更密碼 hello 上一個步驟中），然後您會看到提示，其中您可以發出 SQL 陳述式 toointeract 與 hello 資料庫。
7. toocreate 新的 MySQL 使用者，在 hello 執行 hello 下列**mysql >**提示：
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    請注意，hello 分號 （;） 結尾 hello hello 行會前所未有的結束 hello 命令。
8. 資料庫和授與 hello toocreate`mysqluser`使用者權限它問題 hello 下列命令：
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    請注意資料庫使用者名稱和密碼只能使用所連接 toohello 資料庫的指令碼。  資料庫名稱不一定代表實際的使用者帳戶 hello 系統上的使用者帳戶。
9. 從另一部電腦，型別中 toolog:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    其中`ip-address`是 hello 電腦從這裡連接 tooMySQL hello IP 位址。
10. tooexit hello MySQL 資料庫管理公用程式，輸入：
    
        quit

## <a name="add-an-endpoint"></a>新增端點。
1. 安裝 MySQL 之後，您必須 tooconfigure 端點 tooaccess MySQL 遠端。 登入 toohello [Azure 傳統入口網站][AzurePortal]。 按一下**虛擬機器**，按一下新的虛擬機器 hello 名稱，然後按一下**端點**。
2. 按一下**新增**hello hello 頁底端。
3. 加入名為"MySQL"通訊協定端點**TCP**，和**公用**和**私人**的連接埠組太"3306"。
4. tooremotely 連接 toohello 虛擬機器從您的電腦類型：
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    例如，使用 hello 虛擬機器，我們建立本教學課程中，輸入此命令：
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
