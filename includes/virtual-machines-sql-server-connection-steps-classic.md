### <a name="determine-the-dns-name-of-the-virtual-machine"></a><span data-ttu-id="9b008-101">決定虛擬機器的 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="9b008-101">Determine the DNS name of the virtual machine</span></span>
<span data-ttu-id="9b008-102">若要從另一部電腦連接 SQL Server Database Engine，您必須知道虛擬機器的網域名稱系統 (DNS) 名稱。</span><span class="sxs-lookup"><span data-stu-id="9b008-102">To connect to the SQL Server Database Engine from another computer, you must know the Domain Name System (DNS) name of the virtual machine.</span></span> <span data-ttu-id="9b008-103">(這是網際網路用來識別虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="9b008-103">(This is the name the internet uses to identify the virtual machine.</span></span> <span data-ttu-id="9b008-104">您可以使用 IP 位址，不過當 Azure 因備援或維護而移動資源時，IP 位址可能會改變。</span><span class="sxs-lookup"><span data-stu-id="9b008-104">You can use the IP address, but the IP address might change when Azure moves resources for redundancy or maintenance.</span></span> <span data-ttu-id="9b008-105">DNS 名稱是穩定的，因為它可以重新導向新的 IP 位址。)</span><span class="sxs-lookup"><span data-stu-id="9b008-105">The DNS name will be stable because it can be redirected to a new IP address.)</span></span>  

1. <span data-ttu-id="9b008-106">在 Azure 入口網站 (或前一個步驟) 中選取 [虛擬機器 (傳統)] 。</span><span class="sxs-lookup"><span data-stu-id="9b008-106">In the Azure Portal (or from the previous step), select **Virtual machines (classic)**.</span></span>
2. <span data-ttu-id="9b008-107">選取您的 SQL VM。</span><span class="sxs-lookup"><span data-stu-id="9b008-107">Select your SQL VM.</span></span>
3. <span data-ttu-id="9b008-108">在 [虛擬機器] 刀鋒視窗上，複製虛擬機器的 [DNS 名稱]。</span><span class="sxs-lookup"><span data-stu-id="9b008-108">On the **Virtual machine** blade, copy the **DNS name** for the virtual machine.</span></span>
   
    ![DNS 名稱](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="9b008-110">從另一部電腦連接 Database Engine</span><span class="sxs-lookup"><span data-stu-id="9b008-110">Connect to the Database Engine from another computer</span></span>
1. <span data-ttu-id="9b008-111">在連接網際網路的電腦上開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="9b008-111">On a computer connected to the internet, open SQL Server Management Studio.</span></span>
2. <span data-ttu-id="9b008-112">在 [連接到伺服器] 或 [連接到 Database Engine] 對話方塊的 [伺服器名稱] 方塊中，輸入虛擬機器的 DNS 名稱 (於上一個工作中決定) 和 *DNSName,portnumber* 格式的公用端點連接埠名稱 (如 **mysqlvm.cloudapp.net,57500**)。</span><span class="sxs-lookup"><span data-stu-id="9b008-112">In the **Connect to Server** or **Connect to Database Engine** dialog box, in the **Server name** box, enter the DNS name of the virtual machine (determined in the previous task) and a public endpoint port number in the format of *DNSName,portnumber* such as **mysqlvm.cloudapp.net,57500**.</span></span>
   
    ![使用 SSMS 進行連線](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    <span data-ttu-id="9b008-114">如果您不記得之前建立的公用端點連接埠號碼您可以在 [虛擬機器] 刀鋒視窗的 [端點] 區域中找到。</span><span class="sxs-lookup"><span data-stu-id="9b008-114">If you don't remember the public endpoint port number you previously created, you can find it in the **Endpoints** area of the **Virtual machine** blade.</span></span>
   
    ![公用連接埠](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. <span data-ttu-id="9b008-116">在 [驗證] 方塊中，選取 [SQL Server 驗證]。</span><span class="sxs-lookup"><span data-stu-id="9b008-116">In the **Authentication** box, select **SQL Server Authentication**.</span></span>
4. <span data-ttu-id="9b008-117">在 [登入]  方塊中，輸入於先前工作中建立之登入的名稱。</span><span class="sxs-lookup"><span data-stu-id="9b008-117">In the **Login** box, type the name of a login that you created in an earlier task.</span></span>
5. <span data-ttu-id="9b008-118">在 [密碼]  方塊中，輸入於先前工作中建立之登入的密碼。</span><span class="sxs-lookup"><span data-stu-id="9b008-118">In the **Password** box, type the password of the login that you create in an earlier task.</span></span>
6. <span data-ttu-id="9b008-119">按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="9b008-119">Click **Connect**.</span></span>

