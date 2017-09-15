#### <a name="to-create-public-endpoints-on-the-virtual-device"></a><span data-ttu-id="b16b2-101">在虛擬裝置上建立公用端點</span><span class="sxs-lookup"><span data-stu-id="b16b2-101">To create public endpoints on the virtual device</span></span>

1. <span data-ttu-id="b16b2-102">登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="b16b2-102">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="b16b2-103">按一下 [虛擬機器] ，然後選取想要用來做為虛擬裝置的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b16b2-103">Click **Virtual Machines**, and then select the virtual machine that is being used as your virtual device.</span></span>
3. <span data-ttu-id="b16b2-104">按一下 [端點] 。</span><span class="sxs-lookup"><span data-stu-id="b16b2-104">Click **Endpoints**.</span></span> <span data-ttu-id="b16b2-105">[端點] 頁面會列出虛擬機器的所有端點。</span><span class="sxs-lookup"><span data-stu-id="b16b2-105">The **Endpoints** page lists all endpoints for the virtual machine.</span></span>
4. <span data-ttu-id="b16b2-106">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="b16b2-106">Click **Add**.</span></span> <span data-ttu-id="b16b2-107">新增端點  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="b16b2-107">The **Add Endpoint** dialog box appears.</span></span> <span data-ttu-id="b16b2-108">按一下箭頭以繼續。</span><span class="sxs-lookup"><span data-stu-id="b16b2-108">Click the arrow to continue.</span></span>
5. <span data-ttu-id="b16b2-109">針對 [名稱]，為端點輸入下列名稱：**WinRMHttps**。</span><span class="sxs-lookup"><span data-stu-id="b16b2-109">For the **Name**, type the following name for the endpoint: **WinRMHttps**.</span></span>
6. <span data-ttu-id="b16b2-110">將 [TCP] 指定為 [通訊協定]。</span><span class="sxs-lookup"><span data-stu-id="b16b2-110">For the **Protocol**, specify **TCP**.</span></span>
7. <span data-ttu-id="b16b2-111">針對 [公用連接埠] ，輸入要用於連線的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="b16b2-111">For the **Public Port**, type the port numbers that you want to use for the connection.</span></span>
8. <span data-ttu-id="b16b2-112">針對 [私人連接埠]，輸入 **5986**。</span><span class="sxs-lookup"><span data-stu-id="b16b2-112">For the **Private Port**, type **5986**.</span></span>
9. <span data-ttu-id="b16b2-113">按一下核取記號以建立端點。</span><span class="sxs-lookup"><span data-stu-id="b16b2-113">Click the check mark to create the endpoint.</span></span>

<span data-ttu-id="b16b2-114">建立端點之後，您可以檢視其詳細資料，以確認公用虛擬 IP (VIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="b16b2-114">After the endpoint is created, you can view its details to determine the Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="b16b2-115">請記下此位址。</span><span class="sxs-lookup"><span data-stu-id="b16b2-115">Record this address.</span></span>

