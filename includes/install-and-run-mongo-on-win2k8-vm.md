<span data-ttu-id="6b750-101">請遵循這些步驟 tooinstall，並在執行 Windows Server 的虛擬機器上執行 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="6b750-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b750-102">MongoDB 安全性功能，例如驗證和 IP 位址繫結，均非預設為已啟用。</span><span class="sxs-lookup"><span data-stu-id="6b750-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="6b750-103">部署 MongoDB tooa 生產環境之前，應該啟用安全性功能。</span><span class="sxs-lookup"><span data-stu-id="6b750-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="6b750-104">如需詳細資訊，請參閱[安全性和驗證](http://www.mongodb.org/display/DOCS/Security+and+Authentication)。</span><span class="sxs-lookup"><span data-stu-id="6b750-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="6b750-105">您已連接 toohello 虛擬機器使用遠端桌面之後，開啟 Internet Explorer 從 hello**啟動**hello 虛擬機器上的功能表。</span><span class="sxs-lookup"><span data-stu-id="6b750-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="6b750-106">選取 hello**工具**hello 右上角的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6b750-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="6b750-107">在**網際網路選項**，選取 hello**安全性**索引標籤，然後選取 hello**信任的網站**圖示，最後按一下 hello**網站**按鈕。</span><span class="sxs-lookup"><span data-stu-id="6b750-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="6b750-108">新增*https://\*。 mongodb.org* toohello 信任的網站清單。</span><span class="sxs-lookup"><span data-stu-id="6b750-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="6b750-109">跳過[下載-MongoDB](https://www.mongodb.com/download-center#community)。</span><span class="sxs-lookup"><span data-stu-id="6b750-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="6b750-110">尋找 hello**目前的穩定版本**的**Community 伺服器**，請選取最新 hello **64 位元**hello Windows 資料行中的版本。</span><span class="sxs-lookup"><span data-stu-id="6b750-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="6b750-111">下載，然後執行 hello MSI 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="6b750-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="6b750-112">MongoDB 通常會安裝在 C:\Program Files\MongoDB。</span><span class="sxs-lookup"><span data-stu-id="6b750-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="6b750-113">在 hello 桌面搜尋環境變數，並加入 hello MongoDB 二進位檔路徑 toohello 路徑的變數。</span><span class="sxs-lookup"><span data-stu-id="6b750-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="6b750-114">例如，您可能會發現在 C:\Program Files\MongoDB\Server\3.4\bin hello 二進位檔在電腦上。</span><span class="sxs-lookup"><span data-stu-id="6b750-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="6b750-115">在 hello 資料磁碟中建立 MongoDB 資料和記錄檔目錄 (例如磁碟機**f:**) 在 hello 先前步驟中所建立。</span><span class="sxs-lookup"><span data-stu-id="6b750-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="6b750-116">從**啟動**，選取**命令提示字元**tooopen 命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="6b750-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="6b750-117">輸入：</span><span class="sxs-lookup"><span data-stu-id="6b750-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="6b750-118">toorun hello 資料庫，請執行：</span><span class="sxs-lookup"><span data-stu-id="6b750-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="6b750-119">所有的記錄訊息會導向的 toohello *F:\MongoLogs\mongolog.log*檔為 mongod.exe 伺服器會啟動並 preallocates 日誌檔案。</span><span class="sxs-lookup"><span data-stu-id="6b750-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="6b750-120">它可能需要幾分鐘 MongoDB toopreallocate hello 日誌檔案，並開始接聽連接。</span><span class="sxs-lookup"><span data-stu-id="6b750-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="6b750-121">hello 命令提示字元會保持專注在此工作上 MongoDB 執行個體正在執行時。</span><span class="sxs-lookup"><span data-stu-id="6b750-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="6b750-122">toostart hello MongoDB 系統管理命令介面開啟從另一個 [命令] 視窗**啟動**和型別 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="6b750-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="6b750-123">hello 資料庫會建立 hello 插入。</span><span class="sxs-lookup"><span data-stu-id="6b750-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="6b750-124">或者，您可以利用服務形式安裝 mongod.exe：</span><span class="sxs-lookup"><span data-stu-id="6b750-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="6b750-125">隨即安裝一個名為 MongoDB 的服務，其說明為 "Mongo DB"。</span><span class="sxs-lookup"><span data-stu-id="6b750-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="6b750-126">hello`--logpath`選項必須是使用的 toospecify 記錄檔，因為 hello 執行服務沒有命令視窗 toodisplay 輸出。</span><span class="sxs-lookup"><span data-stu-id="6b750-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="6b750-127">hello`--logappend`選項會指定 hello 服務重新啟動導致輸出 tooappend toohello 現有記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6b750-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="6b750-128">hello`--dbpath`選項會指定 hello hello 資料目錄位置。</span><span class="sxs-lookup"><span data-stu-id="6b750-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="6b750-129">如需更多服務相關的命令列選項，請參閱[服務相關的命令列選項][MongoWindowsSvcOptions]。</span><span class="sxs-lookup"><span data-stu-id="6b750-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="6b750-130">toostart hello 服務，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6b750-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="6b750-131">現在，MongoDB 已安裝並執行，您需要 tooopen Windows 防火牆中的連接埠，您可以從遠端連接 tooMongoDB。</span><span class="sxs-lookup"><span data-stu-id="6b750-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="6b750-132">從 hello**啟動**功能表上，選取**系統管理工具**然後**具有進階安全性的 Windows 防火牆**。</span><span class="sxs-lookup"><span data-stu-id="6b750-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="6b750-133">a） hello 左窗格中，選取**輸入規則**。</span><span class="sxs-lookup"><span data-stu-id="6b750-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="6b750-134">在 hello**動作**窗格右方，hello 選取**新增規則...**.</span><span class="sxs-lookup"><span data-stu-id="6b750-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Windows 防火牆][Image1]

    <span data-ttu-id="6b750-136">b） 在 hello**新增輸入規則精靈**，選取**連接埠**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="6b750-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows 防火牆][Image2]

    <span data-ttu-id="6b750-138">c) 選取 [TCP] 以及 [指定本機連接埠]。</span><span class="sxs-lookup"><span data-stu-id="6b750-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="6b750-139">指定 「 27017 」 （hello 預設連接埠接聽 MongoDB） 的連接埠，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="6b750-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows 防火牆][Image3]

    <span data-ttu-id="6b750-141">d） 選取**允許 hello 連線**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="6b750-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Windows 防火牆][Image4]

    <span data-ttu-id="6b750-143">e) 再次按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="6b750-143">e) Click **Next** again.</span></span>

    ![Windows 防火牆][Image5]

    <span data-ttu-id="6b750-145">f） 指定 hello 規則名稱，例如"MongoPort 」，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="6b750-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows 防火牆][Image6]

12. <span data-ttu-id="6b750-147">如果您未設定端點 for MongoDB。 建立 hello 虛擬機器時，您可以立即進行。</span><span class="sxs-lookup"><span data-stu-id="6b750-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="6b750-148">您需要 hello 防火牆規則和 hello 端點 toobe 無法 tooconnect tooMongoDB 遠端。</span><span class="sxs-lookup"><span data-stu-id="6b750-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="6b750-149">在 hello Azure 入口網站，按一下 **虛擬機器 （傳統）**，按一下新的虛擬機器 hello 名稱，然後按一下**端點**。</span><span class="sxs-lookup"><span data-stu-id="6b750-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![端點][Image7]

13. <span data-ttu-id="6b750-151">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="6b750-151">Click **Add**.</span></span>

14. <span data-ttu-id="6b750-152">新增名稱"Mongo"，通訊協定的端點**TCP**，，兩者均**公用**和**私用**連接埠組太"27017 的 」。</span><span class="sxs-lookup"><span data-stu-id="6b750-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="6b750-153">開啟此連接埠可讓 MongoDB toobe 遠端存取。</span><span class="sxs-lookup"><span data-stu-id="6b750-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![端點][Image9]

> [!NOTE]
> <span data-ttu-id="6b750-155">hello 連接埠 27017 是使用 MongoDB hello 預設通訊埠。</span><span class="sxs-lookup"><span data-stu-id="6b750-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="6b750-156">您可以變更此預設連接埠指定 hello`--port`啟動 hello mongod.exe 伺服器時的參數。</span><span class="sxs-lookup"><span data-stu-id="6b750-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="6b750-157">請確定 toogive hello hello 防火牆中的相同連接埠號碼和 hello hello 上述指示中的"Mongo"端點。</span><span class="sxs-lookup"><span data-stu-id="6b750-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
