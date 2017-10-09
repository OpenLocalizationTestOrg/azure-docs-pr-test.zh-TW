### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a><span data-ttu-id="a7696-101">判斷 hello hello 虛擬機器的 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="a7696-101">Determine hello DNS name of hello virtual machine</span></span>
<span data-ttu-id="a7696-102">tooconnect toohello SQL Server Database Engine 從另一部電腦，您必須知道 hello 網域名稱系統 (DNS) hello 虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="a7696-102">tooconnect toohello SQL Server Database Engine from another computer, you must know hello Domain Name System (DNS) name of hello virtual machine.</span></span> <span data-ttu-id="a7696-103">（這是 hello 名稱 hello 網際網路使用 tooidentify hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a7696-103">(This is hello name hello internet uses tooidentify hello virtual machine.</span></span> <span data-ttu-id="a7696-104">您可以使用 hello IP 位址，但當 Azure 基於冗餘或維護移動資源時，可能會變更 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a7696-104">You can use hello IP address, but hello IP address might change when Azure moves resources for redundancy or maintenance.</span></span> <span data-ttu-id="a7696-105">hello DNS 名稱將會是穩定，因為它可能會重新導向 tooa 新的 IP 位址。)</span><span class="sxs-lookup"><span data-stu-id="a7696-105">hello DNS name will be stable because it can be redirected tooa new IP address.)</span></span>  

1. <span data-ttu-id="a7696-106">在 hello Azure 入口網站 （或從 hello 上一個步驟），選取**虛擬機器 （傳統）**。</span><span class="sxs-lookup"><span data-stu-id="a7696-106">In hello Azure Portal (or from hello previous step), select **Virtual machines (classic)**.</span></span>
2. <span data-ttu-id="a7696-107">選取您的 SQL VM。</span><span class="sxs-lookup"><span data-stu-id="a7696-107">Select your SQL VM.</span></span>
3. <span data-ttu-id="a7696-108">在 hello**虛擬機器**刀鋒視窗，複製 hello **DNS 名稱**hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a7696-108">On hello **Virtual machine** blade, copy hello **DNS name** for hello virtual machine.</span></span>
   
    ![DNS 名稱](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="a7696-110">從另一部電腦連接 toohello Database Engine</span><span class="sxs-lookup"><span data-stu-id="a7696-110">Connect toohello Database Engine from another computer</span></span>
1. <span data-ttu-id="a7696-111">在電腦上連接 toohello 網際網路上，開啟 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="a7696-111">On a computer connected toohello internet, open SQL Server Management Studio.</span></span>
2. <span data-ttu-id="a7696-112">在 hello**連接 tooServer**或**連接 tooDatabase 引擎**對話方塊中的，在 hello**伺服器名稱**方塊中，輸入 hello 虛擬機器 （決定 hello hello DNS 名稱前一項工作） 和公用端點連接埠號碼格式的 hello *DNSName，portnumber*例如**mysqlvm.cloudapp.net,57500**。</span><span class="sxs-lookup"><span data-stu-id="a7696-112">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, in hello **Server name** box, enter hello DNS name of hello virtual machine (determined in hello previous task) and a public endpoint port number in hello format of *DNSName,portnumber* such as **mysqlvm.cloudapp.net,57500**.</span></span>
   
    ![使用 SSMS 進行連線](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    <span data-ttu-id="a7696-114">如果您不記得 hello 公用端點連接埠號碼先前所建立，您可以在 hello**端點**區域 hello**虛擬機器**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a7696-114">If you don't remember hello public endpoint port number you previously created, you can find it in hello **Endpoints** area of hello **Virtual machine** blade.</span></span>
   
    ![公用連接埠](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. <span data-ttu-id="a7696-116">在 hello**驗證**方塊中，選取**SQL Server 驗證**。</span><span class="sxs-lookup"><span data-stu-id="a7696-116">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>
4. <span data-ttu-id="a7696-117">在 hello**登入**中，輸入您在稍早的工作中建立登入的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="a7696-117">In hello **Login** box, type hello name of a login that you created in an earlier task.</span></span>
5. <span data-ttu-id="a7696-118">在 [hello**密碼**] 方塊中，輸入 hello 密碼 hello 登入您在稍早的工作中建立。</span><span class="sxs-lookup"><span data-stu-id="a7696-118">In hello **Password** box, type hello password of hello login that you create in an earlier task.</span></span>
6. <span data-ttu-id="a7696-119">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="a7696-119">Click **Connect**.</span></span>

