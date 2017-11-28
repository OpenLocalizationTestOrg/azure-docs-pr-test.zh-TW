### <span data-ttu-id="7b220-101"><a name="gwipnoconnection"></a>修改區域網路閘道 IP 位址 - 沒有閘道連線</span><span class="sxs-lookup"><span data-stu-id="7b220-101"><a name="gwipnoconnection"></a> To modify the local network gateway IP address - no gateway connection</span></span>

<span data-ttu-id="7b220-102">使用範例來修改沒有閘道連線的區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="7b220-102">Use the example to modify a local network gateway that does not have a gateway connection.</span></span> <span data-ttu-id="7b220-103">修改此值時，您也可以同時修改位址首碼。</span><span class="sxs-lookup"><span data-stu-id="7b220-103">When modifying this value, you can also modify the address prefixes at the same time.</span></span>

1. <span data-ttu-id="7b220-104">在 [區域網路閘道] 資源的 [設定] 區段中，按一下 [組態]。</span><span class="sxs-lookup"><span data-stu-id="7b220-104">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="7b220-105">在 [IP 位址] 方塊中，修改 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7b220-105">In the **IP address** box, modify the IP address.</span></span>
3. <span data-ttu-id="7b220-106">按一下 [儲存]  來儲存這些設定。</span><span class="sxs-lookup"><span data-stu-id="7b220-106">Click **Save** to save the settings.</span></span>

### <span data-ttu-id="7b220-107"><a name="gwipwithconnection"></a>修改區域網路閘道 IP 位址 - 現有閘道連線</span><span class="sxs-lookup"><span data-stu-id="7b220-107"><a name="gwipwithconnection"></a>To modify the local network gateway gateway IP address - existing gateway connection</span></span>

<span data-ttu-id="7b220-108">若要修改具有連線的區域網路閘道，您必須先移除連線。</span><span class="sxs-lookup"><span data-stu-id="7b220-108">To modify a local network gateway that has a connection, you need to first remove the connection.</span></span> <span data-ttu-id="7b220-109">連線移除之後，您可以修改閘道 IP 位址，然後重新建立新連線。</span><span class="sxs-lookup"><span data-stu-id="7b220-109">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="7b220-110">您也可以同時修改位址首碼。</span><span class="sxs-lookup"><span data-stu-id="7b220-110">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="7b220-111">這會導致您 VPN 連線的停機時間。</span><span class="sxs-lookup"><span data-stu-id="7b220-111">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="7b220-112">修改閘道 IP 位址時，您不需要刪除 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="7b220-112">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="7b220-113">您只需要移除連線。</span><span class="sxs-lookup"><span data-stu-id="7b220-113">You only need to remove the connection.</span></span>
 
#### <a name="1-remove-the-connection"></a><span data-ttu-id="7b220-114">1.移除連線。</span><span class="sxs-lookup"><span data-stu-id="7b220-114">1. Remove the connection.</span></span>

1. <span data-ttu-id="7b220-115">在 [區域網路閘道] 資源的 [設定] 區段中，按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="7b220-115">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="7b220-116">按一下連線那一行上的 [...]，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="7b220-116">Click the **...** on the line for the connection, then click **Delete**.</span></span>
3. <span data-ttu-id="7b220-117">按一下 [Save]  儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="7b220-117">Click **Save** to save your settings.</span></span>

#### <a name="2-modify-the-ip-address"></a><span data-ttu-id="7b220-118">2.修改 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7b220-118">2. Modify the IP address.</span></span>

<span data-ttu-id="7b220-119">您也可以同時修改位址首碼。</span><span class="sxs-lookup"><span data-stu-id="7b220-119">You can also modify the address prefixes at the same time.</span></span>

1. <span data-ttu-id="7b220-120">在 [IP 位址] 方塊中，修改 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7b220-120">In the **IP address** box, modify the IP address.</span></span>
2. <span data-ttu-id="7b220-121">按一下 [儲存]  來儲存這些設定。</span><span class="sxs-lookup"><span data-stu-id="7b220-121">Click **Save** to save the settings.</span></span>

#### <a name="3-recreate-the-connection"></a><span data-ttu-id="7b220-122">3.重新建立連線。</span><span class="sxs-lookup"><span data-stu-id="7b220-122">3. Recreate the connection.</span></span>

1. <span data-ttu-id="7b220-123">瀏覽至您 VNet 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="7b220-123">Navigate to the Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="7b220-124">(而非區域網路閘道。)</span><span class="sxs-lookup"><span data-stu-id="7b220-124">(Not the Local Network Gateway.)</span></span>
2. <span data-ttu-id="7b220-125">在 [虛擬網路閘道] 的 [設定] 區段中，按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="7b220-125">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="7b220-126">按一下 [+新增] 以開啟 [新增連線] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7b220-126">Click the **+ Add** to open the **Add connection** blade.</span></span>
4. <span data-ttu-id="7b220-127">重新建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="7b220-127">Recreate your connection.</span></span>
5. <span data-ttu-id="7b220-128">按一下 [確定] 來建立連線。</span><span class="sxs-lookup"><span data-stu-id="7b220-128">Click **OK** to create the connection.</span></span>