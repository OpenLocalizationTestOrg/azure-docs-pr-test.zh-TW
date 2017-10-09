### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="5e367-101">設定 DNS 標籤 hello 公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5e367-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="5e367-102">tooconnect toohello SQL Server Database Engine 從 hello 網際網路，請考慮建立 DNS 索引標籤的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5e367-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="5e367-103">您可以連線的 IP 位址，但 hello DNS 標籤建立 A 記錄，更容易 tooidentify 並摘要 hello 基礎公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5e367-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="5e367-104">如果您計劃 tooonly 連接 toohello SQL Server 執行個體 hello 相同 DNS 標籤不需要虛擬網路或只會在本機。</span><span class="sxs-lookup"><span data-stu-id="5e367-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="5e367-105">先選取 toocreate DNS 標籤**虛擬機器**hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5e367-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="5e367-106">選取您的 SQL Server VM toobring 其內容。</span><span class="sxs-lookup"><span data-stu-id="5e367-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="5e367-107">在 [hello 虛擬機器概觀] 中，選取您**公用 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="5e367-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![公用 IP 位址](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="5e367-109">在您的公用 IP 位址的 hello 屬性，依序展開**組態**。</span><span class="sxs-lookup"><span data-stu-id="5e367-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="5e367-110">輸入 DNS 標籤名稱。</span><span class="sxs-lookup"><span data-stu-id="5e367-110">Enter a DNS Label name.</span></span> <span data-ttu-id="5e367-111">這個名稱是可以直接是使用的 tooconnect tooyour SQL Server VM 的名稱而不是使用 IP 位址的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="5e367-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="5e367-112">按一下 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e367-112">Click hello **Save** button.</span></span>

    ![DNS 標籤](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="5e367-114">從另一部電腦連接 toohello Database Engine</span><span class="sxs-lookup"><span data-stu-id="5e367-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="5e367-115">在電腦上連接 toohello 網際網路上，開啟 SQL Server Management Studio (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="5e367-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="5e367-116">如果您沒有 SQL Server Management Studio，您可以在[這裡](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)下載。</span><span class="sxs-lookup"><span data-stu-id="5e367-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="5e367-117">在 hello**連接 tooServer**或**連接 tooDatabase 引擎**對話方塊中，編輯 hello**伺服器名稱**值。</span><span class="sxs-lookup"><span data-stu-id="5e367-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="5e367-118">輸入 hello IP 位址或 hello （決定 hello 先前工作中） 的虛擬機器的完整 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="5e367-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="5e367-119">您也可以新增逗號並提供 SQL Server 的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="5e367-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="5e367-120">例如： `mysqlvmlabel.eastus.cloudapp.azure.com,1433`。</span><span class="sxs-lookup"><span data-stu-id="5e367-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="5e367-121">在 hello**驗證**方塊中，選取**SQL Server 驗證**。</span><span class="sxs-lookup"><span data-stu-id="5e367-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="5e367-122">在 [hello**登入**] 方塊中，輸入 hello 名稱的有效 SQL 登入。</span><span class="sxs-lookup"><span data-stu-id="5e367-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="5e367-123">在 [hello**密碼**] 方塊中，輸入 hello 密碼 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="5e367-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="5e367-124">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="5e367-124">Click **Connect**.</span></span>

    ![SSMS 連線](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)