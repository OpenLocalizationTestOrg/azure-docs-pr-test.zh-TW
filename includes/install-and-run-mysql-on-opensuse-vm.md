
1. <span data-ttu-id="a3378-101">類型的 tooescalate 權限：</span><span class="sxs-lookup"><span data-stu-id="a3378-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="a3378-102">輸入您的密碼。</span><span class="sxs-lookup"><span data-stu-id="a3378-102">Enter your password.</span></span>
2. <span data-ttu-id="a3378-103">tooinstall MySQL Community 伺服器版本中，輸入：</span><span class="sxs-lookup"><span data-stu-id="a3378-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="a3378-104">等待 MySQL 進行下載和安裝。</span><span class="sxs-lookup"><span data-stu-id="a3378-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="a3378-105">tooset MySQL toostart hello 系統開機時，輸入：</span><span class="sxs-lookup"><span data-stu-id="a3378-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="a3378-106">此命令，手動啟動 hello MySQL 服務精靈 (mysqld):</span><span class="sxs-lookup"><span data-stu-id="a3378-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="a3378-107">hello MySQL 服務精靈，型別 toocheck hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="a3378-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="a3378-108">toostop hello MySQL 服務精靈中，輸入：</span><span class="sxs-lookup"><span data-stu-id="a3378-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="a3378-109">安裝完成後，hello MySQL 根密碼預設是空的。</span><span class="sxs-lookup"><span data-stu-id="a3378-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="a3378-110">建議您執行 **mysql\_secure\_installation**，該指令碼有助於保護 MySQL 的安全。</span><span class="sxs-lookup"><span data-stu-id="a3378-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="a3378-111">hello 指令碼會提示您 toochange hello MySQL 根密碼、 移除匿名使用者帳戶、 停用遠端根目錄登入，測試資料庫，重新載入 hello 權限的資料表。</span><span class="sxs-lookup"><span data-stu-id="a3378-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="a3378-112">我們建議您回答 [是] tooall 這些選項，並變更 hello 根密碼。</span><span class="sxs-lookup"><span data-stu-id="a3378-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="a3378-113">輸入此 toorun hello 指令碼 MySQL 安裝指令碼：</span><span class="sxs-lookup"><span data-stu-id="a3378-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="a3378-114">登入 tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="a3378-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="a3378-115">輸入 hello MySQL 根目錄 （您變更密碼 hello 上一個步驟中），然後您會看到提示，其中您可以發出 SQL 陳述式 toointeract 與 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a3378-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="a3378-116">toocreate 新的 MySQL 使用者，在 hello 執行 hello 下列**mysql >**提示：</span><span class="sxs-lookup"><span data-stu-id="a3378-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="a3378-117">請注意，hello 分號 （;） 結尾 hello hello 行會前所未有的結束 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="a3378-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="a3378-118">資料庫和授與 hello toocreate`mysqluser`使用者權限它問題 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a3378-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="a3378-119">請注意資料庫使用者名稱和密碼只能使用所連接 toohello 資料庫的指令碼。</span><span class="sxs-lookup"><span data-stu-id="a3378-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="a3378-120">資料庫名稱不一定代表實際的使用者帳戶 hello 系統上的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3378-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="a3378-121">從另一部電腦，型別中 toolog:</span><span class="sxs-lookup"><span data-stu-id="a3378-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="a3378-122">其中`ip-address`是 hello 電腦從這裡連接 tooMySQL hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a3378-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="a3378-123">tooexit hello MySQL 資料庫管理公用程式，輸入：</span><span class="sxs-lookup"><span data-stu-id="a3378-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="a3378-124">新增端點。</span><span class="sxs-lookup"><span data-stu-id="a3378-124">Add an endpoint</span></span>
1. <span data-ttu-id="a3378-125">安裝 MySQL 之後，您必須 tooconfigure 端點 tooaccess MySQL 遠端。</span><span class="sxs-lookup"><span data-stu-id="a3378-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="a3378-126">登入 toohello [Azure 傳統入口網站][AzurePortal]。</span><span class="sxs-lookup"><span data-stu-id="a3378-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="a3378-127">按一下**虛擬機器**，按一下新的虛擬機器 hello 名稱，然後按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="a3378-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="a3378-128">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="a3378-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="a3378-129">加入名為"MySQL"通訊協定端點**TCP**，和**公用**和**私人**的連接埠組太"3306"。</span><span class="sxs-lookup"><span data-stu-id="a3378-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="a3378-130">tooremotely 連接 toohello 虛擬機器從您的電腦類型：</span><span class="sxs-lookup"><span data-stu-id="a3378-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="a3378-131">例如，使用 hello 虛擬機器，我們建立本教學課程中，輸入此命令：</span><span class="sxs-lookup"><span data-stu-id="a3378-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
