1. <span data-ttu-id="a761a-101">執行 hello 整合安裝程式安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="a761a-101">Run hello Unified Setup installation file.</span></span>
2. <span data-ttu-id="a761a-102">在**在您開始前**，選取**hello 組態伺服器與處理序伺服器安裝**。</span><span class="sxs-lookup"><span data-stu-id="a761a-102">In **Before You Begin**, select **Install hello configuration server and process server**.</span></span>

    ![開始之前](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. <span data-ttu-id="a761a-104">在**第三方軟體授權**，按一下 **我接受**toodownload 並安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="a761a-104">In **Third Party Software License**, click **I Accept** toodownload and install MySQL.</span></span>

    ![協力廠商軟體](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. <span data-ttu-id="a761a-106">在**註冊**，選取您下載 hello 保存庫中的 hello 註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="a761a-106">In **Registration**, select hello registration key you downloaded from hello vault.</span></span>

    ![註冊](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. <span data-ttu-id="a761a-108">在**網際網路設定**，指定如何在 hello 組態伺服器上執行的提供者透過連接 tooAzure Site Recovery 的 hello hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="a761a-108">In **Internet Settings**, specify how hello Provider running on hello configuration server connects tooAzure Site Recovery over hello Internet.</span></span>

   <span data-ttu-id="a761a-109">a.</span><span class="sxs-lookup"><span data-stu-id="a761a-109">a.</span></span> <span data-ttu-id="a761a-110">如果您想 tooconnect 要與目前在 hello 機器設定的 hello proxy 時，選取**連線使用 proxy 伺服器的站台復原 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="a761a-110">If you want tooconnect with hello proxy that's currently set up on hello machine, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>

   <span data-ttu-id="a761a-111">b.</span><span class="sxs-lookup"><span data-stu-id="a761a-111">b.</span></span> <span data-ttu-id="a761a-112">若要直接 hello 提供者 tooconnect，選取**直接連接不使用 proxy 伺服器的站台復原 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="a761a-112">If you want hello Provider tooconnect directly, select **Connect directly tooAzure Site Recovery without a proxy server**.</span></span>

   <span data-ttu-id="a761a-113">c.</span><span class="sxs-lookup"><span data-stu-id="a761a-113">c.</span></span> <span data-ttu-id="a761a-114">如果 hello 現有 proxy 需要驗證，或是您想要 hello 提供者連接 toouse 自訂 proxy，請選取**使用自訂 proxy 設定連線**。</span><span class="sxs-lookup"><span data-stu-id="a761a-114">If hello existing proxy requires authentication, or if you want toouse a custom proxy for hello Provider connection, select **Connect with custom proxy settings**.</span></span>

     * <span data-ttu-id="a761a-115">如果您使用自訂 proxy，您需要 toospecify hello 位址、 連接埠，以及認證。</span><span class="sxs-lookup"><span data-stu-id="a761a-115">If you use a custom proxy, you need toospecify hello address, port, and credentials.</span></span>
     * <span data-ttu-id="a761a-116">如果您使用 proxy，您應該已經允許 hello Url 中所述[必要條件](#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="a761a-116">If you're using a proxy, you should have already allowed hello URLs described in [Prerequisites](#prerequisites).</span></span>

     ![防火牆](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. <span data-ttu-id="a761a-118">在**必要條件檢查**，安裝程式會執行檢查 toomake 確定，可以執行安裝。</span><span class="sxs-lookup"><span data-stu-id="a761a-118">In **Prerequisites Check**, Setup runs a check toomake sure that installation can run.</span></span> <span data-ttu-id="a761a-119">如果出現有關 hello 警告**通用時間同步處理檢查**，驗證 hello 系統時鐘的 hello 時間 (**日期和時間**設定) hello 相同與 hello 時區。</span><span class="sxs-lookup"><span data-stu-id="a761a-119">If a warning appears about hello **Global time sync check**, verify that hello time on hello system clock (**Date and Time** settings) is hello same as hello time zone.</span></span>

    ![必要條件](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. <span data-ttu-id="a761a-121">在**MySQL 組態**，建立記錄 toohello MySQL 伺服器執行個體上已安裝的認證。</span><span class="sxs-lookup"><span data-stu-id="a761a-121">In **MySQL Configuration**, create credentials for logging on toohello MySQL server instance that is installed.</span></span>

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. <span data-ttu-id="a761a-123">在**環境詳細資料**，選取是否要 tooreplicate VMware Vm。</span><span class="sxs-lookup"><span data-stu-id="a761a-123">In **Environment Details**, select whether you're going tooreplicate VMware VMs.</span></span> <span data-ttu-id="a761a-124">如果是的話，安裝程式就會檢查是否已安裝 PowerCLI 6.0。</span><span class="sxs-lookup"><span data-stu-id="a761a-124">If you are, then Setup checks that PowerCLI 6.0 is installed.</span></span>

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. <span data-ttu-id="a761a-126">在**安裝位置**，選取您想 tooinstall hello 二進位檔和 hello 快取儲存。</span><span class="sxs-lookup"><span data-stu-id="a761a-126">In **Install Location**, select where you want tooinstall hello binaries and store hello cache.</span></span> <span data-ttu-id="a761a-127">您選取的 hello 磁碟機必須有至少 5 GB 的可用磁碟空間，但我們建議至少 600 GB 的可用空間的快取磁碟機。</span><span class="sxs-lookup"><span data-stu-id="a761a-127">hello drive you select must have at least 5 GB of disk space available, but we recommend a cache drive with at least 600 GB of free space.</span></span>

    ![安裝位置](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. <span data-ttu-id="a761a-129">在**網路選取項目**、 指定 hello 接聽程式 （網路介面卡和 SSL 連接埠） 上的 hello 組態伺服器傳送及接收複寫資料。</span><span class="sxs-lookup"><span data-stu-id="a761a-129">In **Network Selection**, specify hello listener (network adapter and SSL port) on which hello configuration server sends and receives replication data.</span></span> <span data-ttu-id="a761a-130">連接埠 9443 hello 預設連接埠，用來傳送和接收複寫流量，但您可以修改此連接埠號碼 toosuit 您環境的需求。</span><span class="sxs-lookup"><span data-stu-id="a761a-130">Port 9443 is hello default port used for sending and receiving replication traffic, but you can modify this port number toosuit your environment's requirements.</span></span> <span data-ttu-id="a761a-131">在加法 toohello 連接埠 9443，我們也會開啟 web 伺服器 tooorchestrate 複寫作業所使用的連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="a761a-131">In addition toohello port 9443, we also open port 443, which is used by a web server tooorchestrate replication operations.</span></span> <span data-ttu-id="a761a-132">請勿使用連接埠 443 來傳送或接收複寫流量。</span><span class="sxs-lookup"><span data-stu-id="a761a-132">Do not use port 443 for sending or receiving replication traffic.</span></span>

    ![網路選擇](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. <span data-ttu-id="a761a-134">在**摘要**，檢閱 hello 資訊，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="a761a-134">In **Summary**, review hello information and click **Install**.</span></span> <span data-ttu-id="a761a-135">安裝完成時，會產生複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a761a-135">When installation finishes, a passphrase is generated.</span></span> <span data-ttu-id="a761a-136">在您啟用複寫時會需要它，所以請將它複製並保存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="a761a-136">You will need this when you enable replication, so copy it and keep it in a secure location.</span></span>

    ![摘要](./media/site-recovery-add-configuration-server/combined-wiz10.png)

<span data-ttu-id="a761a-138">Hello 伺服器註冊完成之後，會顯示在 hello**設定** > **伺服器**hello 保存庫中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a761a-138">After registration finishes, hello server is displayed on hello **Settings** > **Servers** blade in hello vault.</span></span>
