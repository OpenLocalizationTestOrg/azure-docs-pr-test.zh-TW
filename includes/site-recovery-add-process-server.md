1. <span data-ttu-id="bdeb0-101">啟動 Azure 站台復原 UnifiedSetup.exe hello</span><span class="sxs-lookup"><span data-stu-id="bdeb0-101">Launch hello Azure Site Recovery UnifiedSetup.exe</span></span>
2. <span data-ttu-id="bdeb0-102">在**開始之前**，選取**新增額外的處理序伺服器 tooscale 出部署**。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-102">In **Before you begin**, select **Add additional process servers tooscale out deployment**.</span></span>

  ![新增處理序伺服器](./media/site-recovery-add-process-server/ps-page-1.png)

3. <span data-ttu-id="bdeb0-104">在**組態伺服器詳細資料**、 指定 hello hello 組態伺服器 IP 位址和 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-104">In **Configuration Server Details**, specify hello IP address of hello Configuration Server, and hello passphrase.</span></span>

  ![新增處理序伺服器 2](./media/site-recovery-add-process-server/ps-page-2.png)
4. <span data-ttu-id="bdeb0-106">在**網際網路設定**，指定如何在 hello 組態伺服器上執行的提供者透過連接 tooAzure Site Recovery 的 hello hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-106">In **Internet Settings**, specify how hello Provider running on hello Configuration Server connects tooAzure Site Recovery over hello Internet.</span></span>

  ![新增處理序伺服器 3](./media/site-recovery-add-process-server/ps-page-3.png)

   * <span data-ttu-id="bdeb0-108">如果您想 tooconnect 要與目前在 hello 機器設定的 hello proxy 時，選取**利用現有的 proxy 設定連線**。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-108">If you want tooconnect with hello proxy that's currently set up on hello machine, select **Connect with existing proxy settings**.</span></span>
   * <span data-ttu-id="bdeb0-109">若要直接 hello 提供者 tooconnect，選取**不使用 proxy 直接連線**。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-109">If you want hello Provider tooconnect directly, select **Connect directly without a proxy**.</span></span>
   * <span data-ttu-id="bdeb0-110">如果 hello 現有 proxy 需要驗證，或是您想要 hello 提供者連接 toouse 自訂 proxy，請選取**使用自訂 proxy 設定連線**。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-110">If hello existing proxy requires authentication, or if you want toouse a custom proxy for hello Provider connection, select **Connect with custom proxy settings**.</span></span>

     * <span data-ttu-id="bdeb0-111">如果您使用自訂 proxy，您需要 toospecify hello 位址、 連接埠，以及認證。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-111">If you use a custom proxy, you need toospecify hello address, port, and credentials.</span></span>
     * <span data-ttu-id="bdeb0-112">如果您使用 proxy，您應該已經允許存取 toohello 服務 url。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-112">If you're using a proxy, you should have already allowed access toohello service urls.</span></span>

5. <span data-ttu-id="bdeb0-113">在**必要條件檢查**，安裝程式會執行檢查 toomake 確定，可以執行安裝。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-113">In **Prerequisites Check**, Setup runs a check toomake sure that installation can run.</span></span> <span data-ttu-id="bdeb0-114">如果出現有關 hello 警告**通用時間同步處理檢查**，驗證 hello 系統時鐘的 hello 時間 (**日期和時間**設定) hello 相同與 hello 時區。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-114">If a warning appears about hello **Global time sync check**, verify that hello time on hello system clock (**Date and Time** settings) is hello same as hello time zone.</span></span>

     ![新增處理序伺服器 4](./media/site-recovery-add-process-server/ps-page-4.png)

6. <span data-ttu-id="bdeb0-116">在**環境詳細資料**，選取是否要 tooreplicate VMware Vm。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-116">In **Environment Details**, select whether you're going tooreplicate VMware VMs.</span></span> <span data-ttu-id="bdeb0-117">如果是的話，安裝程式會檢查是否已安裝 PowerCLI 6.0。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-117">If you are, then setup checks that PowerCLI 6.0 is installed.</span></span>

     ![新增處理序伺服器 5](./media/site-recovery-add-process-server/ps-page-5.png)

7. <span data-ttu-id="bdeb0-119">在**安裝位置**，選取您想 tooinstall hello 二進位檔和 hello 快取儲存。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-119">In **Install Location**, select where you want tooinstall hello binaries and store hello cache.</span></span> <span data-ttu-id="bdeb0-120">您選取的 hello 磁碟機必須有至少 5 GB 的可用磁碟空間，但我們建議至少 600 GB 的可用空間的快取磁碟機。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-120">hello drive you select must have at least 5 GB of disk space available, but we recommend a cache drive with at least 600 GB of free space.</span></span>
     <span data-ttu-id="bdeb0-121">![新增處理序伺服器 5](./media/site-recovery-add-process-server/ps-page-6.png)</span><span class="sxs-lookup"><span data-stu-id="bdeb0-121">![Add process server 5](./media/site-recovery-add-process-server/ps-page-6.png)</span></span>

8. <span data-ttu-id="bdeb0-122">在**網路選取項目**、 指定 hello 接聽程式 （網路介面卡和 SSL 連接埠） 上的 hello 設定伺服器傳送及接收複寫資料。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-122">In **Network Selection**, specify hello listener (network adapter and SSL port) on which hello Configuration Server sends and receives replication data.</span></span> <span data-ttu-id="bdeb0-123">連接埠 9443 hello 預設連接埠，用來傳送和接收複寫流量，但您可以修改此連接埠號碼 toosuit 您環境的需求。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-123">Port 9443 is hello default port used for sending and receiving replication traffic, but you can modify this port number toosuit your environment's requirements.</span></span> <span data-ttu-id="bdeb0-124">在加法 toohello 連接埠 9443，我們也會開啟 web 伺服器 tooorchestrate 複寫作業所使用的連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-124">In addition toohello port 9443, we also open port 443, which is used by a web server tooorchestrate replication operations.</span></span> <span data-ttu-id="bdeb0-125">請勿使用連接埠 443 來傳送或接收複寫流量。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-125">Do not use Port 443 for sending or receiving replication traffic.</span></span>

     ![新增處理序伺服器 6](./media/site-recovery-add-process-server/ps-page-7.png)
9. <span data-ttu-id="bdeb0-127">在**摘要**，檢閱 hello 資訊，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-127">In **Summary**, review hello information and click **Install**.</span></span> <span data-ttu-id="bdeb0-128">安裝完成時，會產生複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-128">When installation finishes, a passphrase is generated.</span></span> <span data-ttu-id="bdeb0-129">在您啟用複寫時會需要它，所以請將它複製並保存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="bdeb0-129">You will need this when you enable replication, so copy it and keep it in a secure location.</span></span>

     ![新增處理序伺服器 7](./media/site-recovery-add-process-server/ps-page-8.png)
