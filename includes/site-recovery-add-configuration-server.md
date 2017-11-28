1. <span data-ttu-id="9c6eb-101">執行統一安裝的安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-101">Run the Unified Setup installation file.</span></span>
2. <span data-ttu-id="9c6eb-102">在 [開始之前] 選取 [安裝設定伺服器和處理序伺服器]。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-102">In **Before You Begin**, select **Install the configuration server and process server**.</span></span>

    ![開始之前](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. <span data-ttu-id="9c6eb-104">在 [協力廠商軟體授權] 中，按一下 [我接受] 來下載並安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-104">In **Third Party Software License**, click **I Accept** to download and install MySQL.</span></span>

    ![協力廠商軟體](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. <span data-ttu-id="9c6eb-106">在 [註冊] 中，選取您從保存庫下載的註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-106">In **Registration**, select the registration key you downloaded from the vault.</span></span>

    ![註冊](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. <span data-ttu-id="9c6eb-108">在 [網際網路設定] 中，指定在設定伺服器上執行的 Provider 要如何透過網際網路連接到 Azure Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-108">In **Internet Settings**, specify how the Provider running on the configuration server connects to Azure Site Recovery over the Internet.</span></span>

   <span data-ttu-id="9c6eb-109">a.</span><span class="sxs-lookup"><span data-stu-id="9c6eb-109">a.</span></span> <span data-ttu-id="9c6eb-110">如果您想要使用電腦上目前設定的 Proxy 來連線，請選取 [使用 Proxy 伺服器連線至 Azure Site Recovery]。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-110">If you want to connect with the proxy that's currently set up on the machine, select **Connect to Azure Site Recovery using a proxy server**.</span></span>

   <span data-ttu-id="9c6eb-111">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-111">b.</span></span> <span data-ttu-id="9c6eb-112">如果您想要讓提供者直接連接，請選取 [不使用 Proxy 伺服器直接連線到 Azure Site Recovery]。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-112">If you want the Provider to connect directly, select **Connect directly to Azure Site Recovery without a proxy server**.</span></span>

   <span data-ttu-id="9c6eb-113">c.</span><span class="sxs-lookup"><span data-stu-id="9c6eb-113">c.</span></span> <span data-ttu-id="9c6eb-114">如果現有的 Proxy 需要驗證，或是您想要讓 Provider 使用自訂 Proxy 來連線，請選取 [以自訂 Proxy 設定連線]。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-114">If the existing proxy requires authentication, or if you want to use a custom proxy for the Provider connection, select **Connect with custom proxy settings**.</span></span>

     * <span data-ttu-id="9c6eb-115">如果您使用自訂 Proxy，您必須指定位址、連接埠以及認證。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-115">If you use a custom proxy, you need to specify the address, port, and credentials.</span></span>
     * <span data-ttu-id="9c6eb-116">如果您是使用 Proxy，應該已經允許[必要條件](#prerequisites)中所述的 URL。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-116">If you're using a proxy, you should have already allowed the URLs described in [Prerequisites](#prerequisites).</span></span>

     ![防火牆](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. <span data-ttu-id="9c6eb-118">在 [必要條件檢查] 中，安裝程式會執行檢查來確定可以執行安裝。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-118">In **Prerequisites Check**, Setup runs a check to make sure that installation can run.</span></span> <span data-ttu-id="9c6eb-119">如果出現有關「通用時間同步處理檢查」的警告，請確認系統時鐘上的時間 ([日期和時間] 設定) 與時區相同。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-119">If a warning appears about the **Global time sync check**, verify that the time on the system clock (**Date and Time** settings) is the same as the time zone.</span></span>

    ![必要條件](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. <span data-ttu-id="9c6eb-121">在 [MySQL 組態] 中，建立認證來登入已安裝的 MySQL 伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-121">In **MySQL Configuration**, create credentials for logging on to the MySQL server instance that is installed.</span></span>

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. <span data-ttu-id="9c6eb-123">在 [環境詳細資料] 中，選取您是否要複寫 VMware VM。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-123">In **Environment Details**, select whether you're going to replicate VMware VMs.</span></span> <span data-ttu-id="9c6eb-124">如果是的話，安裝程式就會檢查是否已安裝 PowerCLI 6.0。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-124">If you are, then Setup checks that PowerCLI 6.0 is installed.</span></span>

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. <span data-ttu-id="9c6eb-126">在 [安裝位置] 中，選取您要安裝二進位檔及儲存快取的位置。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-126">In **Install Location**, select where you want to install the binaries and store the cache.</span></span> <span data-ttu-id="9c6eb-127">您選取的磁碟機至少必須有 5 GB 的可用磁碟空間，但我們建議快取磁碟機至少有 600 GB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-127">The drive you select must have at least 5 GB of disk space available, but we recommend a cache drive with at least 600 GB of free space.</span></span>

    ![安裝位置](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. <span data-ttu-id="9c6eb-129">在 [網路選取] 中，指定設定伺服器用來傳送和接收複寫資料的接聽程式 (網路介面卡和 SSL 連接埠)。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-129">In **Network Selection**, specify the listener (network adapter and SSL port) on which the configuration server sends and receives replication data.</span></span> <span data-ttu-id="9c6eb-130">連接埠 9443 是用來傳送及接收複寫流量的預設連接埠，但您可以修改此連接埠號碼，以符合您的環境需求。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-130">Port 9443 is the default port used for sending and receiving replication traffic, but you can modify this port number to suit your environment's requirements.</span></span> <span data-ttu-id="9c6eb-131">除了連接埠 9443 之外，我們也會開啟網頁伺服器用來協調複寫作業的連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-131">In addition to the port 9443, we also open port 443, which is used by a web server to orchestrate replication operations.</span></span> <span data-ttu-id="9c6eb-132">請勿使用連接埠 443 來傳送或接收複寫流量。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-132">Do not use port 443 for sending or receiving replication traffic.</span></span>

    ![網路選擇](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. <span data-ttu-id="9c6eb-134">在 [摘要] 中檢閱資訊，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-134">In **Summary**, review the information and click **Install**.</span></span> <span data-ttu-id="9c6eb-135">安裝完成時，會產生複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-135">When installation finishes, a passphrase is generated.</span></span> <span data-ttu-id="9c6eb-136">在您啟用複寫時會需要它，所以請將它複製並保存在安全的位置。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-136">You will need this when you enable replication, so copy it and keep it in a secure location.</span></span>

    ![摘要](./media/site-recovery-add-configuration-server/combined-wiz10.png)

<span data-ttu-id="9c6eb-138">註冊完成後，伺服器會顯示在保存庫的 [設定]  >  刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="9c6eb-138">After registration finishes, the server is displayed on the **Settings** > **Servers** blade in the vault.</span></span>
