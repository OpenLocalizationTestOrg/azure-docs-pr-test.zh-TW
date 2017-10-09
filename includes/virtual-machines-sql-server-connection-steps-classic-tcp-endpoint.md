### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a><span data-ttu-id="b3149-101">建立 hello 虛擬機器的 TCP 端點</span><span class="sxs-lookup"><span data-stu-id="b3149-101">Create a TCP endpoint for hello virtual machine</span></span>
<span data-ttu-id="b3149-102">順序 tooaccess hello 從 SQL Server 在網際網路、 hello 虛擬機器必須能夠端點 toolisten，內送 TCP 通訊。</span><span class="sxs-lookup"><span data-stu-id="b3149-102">In order tooaccess SQL Server from hello internet, hello virtual machine must have an endpoint toolisten for incoming TCP communication.</span></span> <span data-ttu-id="b3149-103">這個 Azure 組態步驟，指示內送 TCP 連接埠流量 tooa TCP 通訊埠是可存取 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3149-103">This Azure configuration step, directs incoming TCP port traffic tooa TCP port that is accessible toohello virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="b3149-104">如果您要在 hello 連接相同雲端服務或虛擬網路，您不需要 toocreate 可公開存取的端點。</span><span class="sxs-lookup"><span data-stu-id="b3149-104">If you are connecting within hello same cloud service or virtual network, you do not have toocreate a publically accessible endpoint.</span></span> <span data-ttu-id="b3149-105">在此情況下，您無法繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="b3149-105">In that case, you could continue toohello next step.</span></span> <span data-ttu-id="b3149-106">如需詳細資訊，請參閱[連接案例](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios)。</span><span class="sxs-lookup"><span data-stu-id="b3149-106">For more information, see [Connection Scenarios](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).</span></span>
> 
> 

1. <span data-ttu-id="b3149-107">在 hello Azure 入口網站，選取 **虛擬機器 （傳統）**。</span><span class="sxs-lookup"><span data-stu-id="b3149-107">On hello Azure Portal, select **Virtual machines (classic)**.</span></span>
2. <span data-ttu-id="b3149-108">然後選取您的 SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3149-108">Then select you SQL Server virtual machine.</span></span>
3. <span data-ttu-id="b3149-109">選取**端點**，然後按一下hello**新增**在 hello hello 端點刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3149-109">Select **Endpoints**, and then click hello **Add** button at hello top of hello Endpoints blade.</span></span>
   
    ![建立端點的入口網站步驟](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. <span data-ttu-id="b3149-111">在 hello**加入端點**刀鋒視窗中，提供**名稱**SQLEndpoint 等。</span><span class="sxs-lookup"><span data-stu-id="b3149-111">On hello **Add Endpoint** blade, provide a **Name** such as SQLEndpoint.</span></span>
5. <span data-ttu-id="b3149-112">選取**TCP** hello**通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="b3149-112">Select **TCP** for hello **Protocol**.</span></span>
6. <span data-ttu-id="b3149-113">對於 [公用連接埠]，請指定連接埠號碼，例如 **57500**。</span><span class="sxs-lookup"><span data-stu-id="b3149-113">For **Public port**, specify a port number such as **57500**.</span></span>
7. <span data-ttu-id="b3149-114">如**私用連接埠**，指定 SQL Server 接聽連接埠，其預設太**1433年**。</span><span class="sxs-lookup"><span data-stu-id="b3149-114">For **Private port**, specify SQL Server's listening port, which defaults too**1433**.</span></span>
8. <span data-ttu-id="b3149-115">按一下**確定**toocreate hello 端點。</span><span class="sxs-lookup"><span data-stu-id="b3149-115">Click **Ok** toocreate hello endpoint.</span></span>

