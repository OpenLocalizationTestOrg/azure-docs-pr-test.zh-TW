<span data-ttu-id="3e41b-101">遵循下列步驟，在執行 Windows Server 的虛擬機器上安裝並執行 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="3e41b-101">Follow these steps to install and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e41b-102">MongoDB 安全性功能，例如驗證和 IP 位址繫結，均非預設為已啟用。</span><span class="sxs-lookup"><span data-stu-id="3e41b-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="3e41b-103">安全性功能應該在將 MongoDB 部署到生產環境前加以啟用。</span><span class="sxs-lookup"><span data-stu-id="3e41b-103">Security features should be enabled before deploying MongoDB to a production environment.</span></span>  <span data-ttu-id="3e41b-104">如需詳細資訊，請參閱[安全性和驗證](http://www.mongodb.org/display/DOCS/Security+and+Authentication)。</span><span class="sxs-lookup"><span data-stu-id="3e41b-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="3e41b-105">使用遠端桌面連線到虛擬機器時，請從虛擬機器上的 [ **開始** ] 功能表中開啟 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="3e41b-105">After you've connected to the virtual machine using Remote Desktop, open Internet Explorer from the **Start** menu on the virtual machine.</span></span>
2. <span data-ttu-id="3e41b-106">選取右上方的 [工具]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3e41b-106">Select the **Tools** button in the upper right corner.</span></span>  <span data-ttu-id="3e41b-107">在 [網際網路選項] 中，選取 [安全性] 索引標籤，接著選取 [受信任的網站] 圖示，最後按一下 [網站] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3e41b-107">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon, and finally click the **Sites** button.</span></span> <span data-ttu-id="3e41b-108">將 *https://\*.mongodb.org* 新增至受信任的網站清單。</span><span class="sxs-lookup"><span data-stu-id="3e41b-108">Add *https://\*.mongodb.org* to the list of trusted sites.</span></span>
3. <span data-ttu-id="3e41b-109">移至[下載 - MongoDB](https://www.mongodb.com/download-center#community)。</span><span class="sxs-lookup"><span data-stu-id="3e41b-109">Go to [Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="3e41b-110">尋找**社群伺服器**的**目前穩定版本**，在 Windows 資料行中選取最新的 **64 位元**版本。</span><span class="sxs-lookup"><span data-stu-id="3e41b-110">Find the **Current Stable Release** of **Community Server**, select the latest **64-bit** version in the Windows column.</span></span> <span data-ttu-id="3e41b-111">進行下載，然後執行 MSI 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="3e41b-111">Download, then run the MSI installer.</span></span>
5. <span data-ttu-id="3e41b-112">MongoDB 通常會安裝在 C:\Program Files\MongoDB。</span><span class="sxs-lookup"><span data-stu-id="3e41b-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="3e41b-113">在桌面上搜尋環境變數，然後將 MongoDB 二進位檔路徑新增至 PATH 變數。</span><span class="sxs-lookup"><span data-stu-id="3e41b-113">Search for Environment Variables on the desktop and add the MongoDB binaries path to the PATH variable.</span></span> <span data-ttu-id="3e41b-114">例如，您可能會在電腦的 C:\Program Files\MongoDB\Server\3.4\bin 發現二進位檔。</span><span class="sxs-lookup"><span data-stu-id="3e41b-114">For example, you might find the binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="3e41b-115">在您在先前步驟中建立的資料磁碟中建立 MongoDB 資料和記錄目錄 (例如磁碟機 **F:**)。</span><span class="sxs-lookup"><span data-stu-id="3e41b-115">Create MongoDB data and log directories in the data disk (such as drive **F:**) you created in the preceding steps.</span></span> <span data-ttu-id="3e41b-116">在 [開始] 功能表中，選取 [命令提示字元] 以開啟命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="3e41b-116">From **Start**, select **Command Prompt** to open a command prompt window.</span></span>  <span data-ttu-id="3e41b-117">輸入：</span><span class="sxs-lookup"><span data-stu-id="3e41b-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="3e41b-118">若要執行資料庫，執行：</span><span class="sxs-lookup"><span data-stu-id="3e41b-118">To run the database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="3e41b-119">在 mongod.exe 伺服器啟動和預先配置日誌檔案時，所有記錄訊息都會傳送至 *F:\MongoLogs\mongolog.log* 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e41b-119">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="3e41b-120">MongoDB 可能需要花費數分鐘來預先配置日誌檔案，並開始接聽連線。</span><span class="sxs-lookup"><span data-stu-id="3e41b-120">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span></span> <span data-ttu-id="3e41b-121">當您的 MongoDB 執行個體正在執行時，命令提示字元會專注於這項工作。</span><span class="sxs-lookup"><span data-stu-id="3e41b-121">The command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="3e41b-122">若要啟動 MongoDB 管理殼層，請從 [開始] 功能表中開啟另一個命令視窗，並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="3e41b-122">To start the MongoDB administrative shell, open another command window from **Start** and type the following commands:</span></span>

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

    <span data-ttu-id="3e41b-123">資料庫由插入項目建立。</span><span class="sxs-lookup"><span data-stu-id="3e41b-123">The database is created by the insert.</span></span>
9. <span data-ttu-id="3e41b-124">或者，您可以利用服務形式安裝 mongod.exe：</span><span class="sxs-lookup"><span data-stu-id="3e41b-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="3e41b-125">隨即安裝一個名為 MongoDB 的服務，其說明為 "Mongo DB"。</span><span class="sxs-lookup"><span data-stu-id="3e41b-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="3e41b-126">`--logpath` 選項必須用來指定記錄檔，因為執行中的服務沒有命令視窗可以顯示輸出。</span><span class="sxs-lookup"><span data-stu-id="3e41b-126">The `--logpath` option must be used to specify a log file, since the running service does not have a command window to display output.</span></span>  <span data-ttu-id="3e41b-127">`--logappend` 選項指出重新啟動服務會導致輸出附加在現有的記錄檔案中。</span><span class="sxs-lookup"><span data-stu-id="3e41b-127">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>  <span data-ttu-id="3e41b-128">`--dbpath` 選項指出資料目錄的位置。</span><span class="sxs-lookup"><span data-stu-id="3e41b-128">The `--dbpath` option specifies the location of the data directory.</span></span> <span data-ttu-id="3e41b-129">如需更多服務相關的命令列選項，請參閱[服務相關的命令列選項][MongoWindowsSvcOptions]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="3e41b-130">若要啟動服務，請執行此命令：</span><span class="sxs-lookup"><span data-stu-id="3e41b-130">To start the service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="3e41b-131">現在，MongoDB 已安裝並正在執行，您必須在 Windows 防火牆中開啟一個連接埠，才能遠端連線至 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="3e41b-131">Now that MongoDB is installed and running, you need to open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span>  <span data-ttu-id="3e41b-132">在 [開始] 功能表中，選取 [管理員工具]，然後選取 [具備進階安全性的 Windows 防火牆]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-132">From the **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="3e41b-133">a) 在左側窗格中，選取 [內送規則]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-133">a) In the left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="3e41b-134">在右側的 [動作] 窗格中，選取 [新增規則...]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-134">In the **Actions** pane on the right, select **New Rule...**.</span></span>

    ![Windows 防火牆][Image1]

    <span data-ttu-id="3e41b-136">b) 在 [新內送規則精靈] 中，選取 [連接埠] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-136">b) In the **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows 防火牆][Image2]

    <span data-ttu-id="3e41b-138">c) 選取 [TCP] 以及 [指定本機連接埠]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="3e41b-139">指定連接埠為 "27017" (MongoDB 接聽的預設連接埠) 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-139">Specify a port of "27017" (the default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows 防火牆][Image3]

    <span data-ttu-id="3e41b-141">選取 [允許連線] 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-141">d) Select **Allow the connection** and click **Next**.</span></span>

    ![Windows 防火牆][Image4]

    <span data-ttu-id="3e41b-143">e) 再次按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-143">e) Click **Next** again.</span></span>

    ![Windows 防火牆][Image5]

    <span data-ttu-id="3e41b-145">f) 指定規則名稱，例如 "MongoPort"，並按一下 [結束]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-145">f) Specify a name for the rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows 防火牆][Image6]

12. <span data-ttu-id="3e41b-147">如果您在建立虛擬機器時沒有設定 MongoDB 的端點，您現在可以進行此動作。</span><span class="sxs-lookup"><span data-stu-id="3e41b-147">If you didn't configure an endpoint for MongoDB when you created the virtual machine, you can do it now.</span></span> <span data-ttu-id="3e41b-148">您需要防火牆規則和端點兩者，才能遠端連線至 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="3e41b-148">You need both the firewall rule and the endpoint to be able to connect to MongoDB remotely.</span></span>

  <span data-ttu-id="3e41b-149">在 Azure 入口網站中，依序按一下 [虛擬機器 (傳統)]、新虛擬機器的名稱以及 [端點]。</span><span class="sxs-lookup"><span data-stu-id="3e41b-149">In the Azure portal, click **Virtual Machines (classic)**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![端點][Image7]

13. <span data-ttu-id="3e41b-151">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="3e41b-151">Click **Add**.</span></span>

14. <span data-ttu-id="3e41b-152">新增名為 "Mongo" 的端點，通訊協定為 **TCP**，且**公開**以及**私人**連接埠均設為 "27017"。</span><span class="sxs-lookup"><span data-stu-id="3e41b-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set to "27017".</span></span> <span data-ttu-id="3e41b-153">開啟此連接埠可允許 MongoDB 遠端存取。</span><span class="sxs-lookup"><span data-stu-id="3e41b-153">Opening this port allows MongoDB to be accessed remotely.</span></span>

    ![端點][Image9]

> [!NOTE]
> <span data-ttu-id="3e41b-155">連接埠 27017 是 MongoDB 使用的預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="3e41b-155">The port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="3e41b-156">在啟動 mongod.exe 伺服器時指定 `--port` 參數，即可變更此預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="3e41b-156">You can change this default port by specifying the `--port` parameter when starting the mongod.exe server.</span></span> <span data-ttu-id="3e41b-157">請務必為先前指示中的防火牆和 "Mongo" 端點指定相同的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="3e41b-157">Make sure to give the same port number in the firewall and the "Mongo" endpoint in the preceding instructions.</span></span>
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
