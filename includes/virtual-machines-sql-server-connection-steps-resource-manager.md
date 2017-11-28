### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="df3a0-101">設定公用 IP 位址的 DNS 標籤</span><span class="sxs-lookup"><span data-stu-id="df3a0-101">Configure a DNS Label for the public IP address</span></span>

<span data-ttu-id="df3a0-102">若要從網際網路連線到 SQL Server Database Engine，請考慮建立公用 IP 位址的 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="df3a0-102">To connect to the SQL Server Database Engine from the Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="df3a0-103">您可以經由 IP 位址連線，但 DNS 標籤可建立較容易識別的 A 記錄並擷取基礎公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="df3a0-103">You can connect by IP address, but the DNS Label creates an A Record that is easier to identify and abstracts the underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="df3a0-104">如果您計畫只連線到同一個虛擬網路中或只連線到本機的 SQL Server 執行個體，則不需要 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="df3a0-104">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>

<span data-ttu-id="df3a0-105">若要建立 DNS 標籤，請先在入口網站選取 [虛擬機器]  。</span><span class="sxs-lookup"><span data-stu-id="df3a0-105">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="df3a0-106">選取 SQL Server VM 以顯示其屬性。</span><span class="sxs-lookup"><span data-stu-id="df3a0-106">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="df3a0-107">在虛擬機器概觀中，選取您的 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="df3a0-107">In the virtual machine overview, select your **Public IP address**.</span></span>

    ![公用 IP 位址](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="df3a0-109">在公用 IP 位址屬性中，展開 [組態] 。</span><span class="sxs-lookup"><span data-stu-id="df3a0-109">In the properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="df3a0-110">輸入 DNS 標籤名稱。</span><span class="sxs-lookup"><span data-stu-id="df3a0-110">Enter a DNS Label name.</span></span> <span data-ttu-id="df3a0-111">此名稱是「A 紀錄」，可用來透過名稱 (而非直接透過 IP 位址) 連線到 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="df3a0-111">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="df3a0-112">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="df3a0-112">Click the **Save** button.</span></span>

    ![DNS 標籤](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="df3a0-114">從另一部電腦連接 Database Engine</span><span class="sxs-lookup"><span data-stu-id="df3a0-114">Connect to the Database Engine from another computer</span></span>

1. <span data-ttu-id="df3a0-115">在已連線網際網路的電腦上開啟 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="df3a0-115">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="df3a0-116">如果您沒有 SQL Server Management Studio，您可以在[這裡](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)下載。</span><span class="sxs-lookup"><span data-stu-id="df3a0-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="df3a0-117">在 [連接到伺服器] 或 [連接到 Database Engine] 對話方塊中，編輯 [伺服器名稱] 值。</span><span class="sxs-lookup"><span data-stu-id="df3a0-117">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="df3a0-118">輸入虛擬機器的 IP 位址或完整 DNS 名稱 (在前一項工作中決定)。</span><span class="sxs-lookup"><span data-stu-id="df3a0-118">Enter the IP address or full DNS name of the virtual machine (determined in the previous task).</span></span> <span data-ttu-id="df3a0-119">您也可以新增逗號並提供 SQL Server 的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="df3a0-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="df3a0-120">例如： `mysqlvmlabel.eastus.cloudapp.azure.com,1433`。</span><span class="sxs-lookup"><span data-stu-id="df3a0-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="df3a0-121">在 [驗證] 方塊中，選取 [SQL Server 驗證]。</span><span class="sxs-lookup"><span data-stu-id="df3a0-121">In the **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="df3a0-122">在 [登入]  方塊中，輸入有效的 SQL 登入名稱。</span><span class="sxs-lookup"><span data-stu-id="df3a0-122">In the **Login** box, type the name of a valid SQL login.</span></span>

1. <span data-ttu-id="df3a0-123">在 [密碼]  方塊中，輸入登入的密碼。</span><span class="sxs-lookup"><span data-stu-id="df3a0-123">In the **Password** box, type the password of the login.</span></span>

1. <span data-ttu-id="df3a0-124">按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="df3a0-124">Click **Connect**.</span></span>

    ![SSMS 連線](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)