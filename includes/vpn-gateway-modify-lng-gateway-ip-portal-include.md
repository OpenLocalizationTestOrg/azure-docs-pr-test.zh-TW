### <span data-ttu-id="b48b3-101"><a name="gwipnoconnection"></a>toomodify hello 區域網路閘道 IP 位址沒有閘道連線</span><span class="sxs-lookup"><span data-stu-id="b48b3-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway IP address - no gateway connection</span></span>

<span data-ttu-id="b48b3-102">使用 hello 範例 toomodify 沒有閘道連線的區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b48b3-102">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span> <span data-ttu-id="b48b3-103">當修改這個值，您也可以修改在 hello hello 位址前置詞相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b48b3-103">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span>

1. <span data-ttu-id="b48b3-104">在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。</span><span class="sxs-lookup"><span data-stu-id="b48b3-104">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="b48b3-105">在 hello **IP 位址**方塊中，修改 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b48b3-105">In hello **IP address** box, modify hello IP address.</span></span>
3. <span data-ttu-id="b48b3-106">按一下**儲存**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="b48b3-106">Click **Save** toosave hello settings.</span></span>

### <span data-ttu-id="b48b3-107"><a name="gwipwithconnection"></a>toomodify hello 區域網路閘道閘道 IP 位址-現有的閘道連線</span><span class="sxs-lookup"><span data-stu-id="b48b3-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway gateway IP address - existing gateway connection</span></span>

<span data-ttu-id="b48b3-108">toomodify 已連接的區域網路閘道，您需要 toofirst 移除 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b48b3-108">toomodify a local network gateway that has a connection, you need toofirst remove hello connection.</span></span> <span data-ttu-id="b48b3-109">移除 hello 連線之後，您可以修改 hello 閘道 IP 位址，並重新建立新的連接。</span><span class="sxs-lookup"><span data-stu-id="b48b3-109">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="b48b3-110">您也可以修改在 hello hello 位址前置詞相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b48b3-110">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="b48b3-111">這會導致您 VPN 連線的停機時間。</span><span class="sxs-lookup"><span data-stu-id="b48b3-111">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="b48b3-112">當修改 hello 閘道 IP 位址，您不需要 toodelete hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="b48b3-112">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="b48b3-113">您只需要 tooremove hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b48b3-113">You only need tooremove hello connection.</span></span>
 
#### <a name="1-remove-hello-connection"></a><span data-ttu-id="b48b3-114">1.移除 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b48b3-114">1. Remove hello connection.</span></span>

1. <span data-ttu-id="b48b3-115">在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**連線**。</span><span class="sxs-lookup"><span data-stu-id="b48b3-115">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="b48b3-116">按一下 hello **...**該行 hello hello 連線，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b48b3-116">Click hello **...** on hello line for hello connection, then click **Delete**.</span></span>
3. <span data-ttu-id="b48b3-117">按一下**儲存**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="b48b3-117">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-ip-address"></a><span data-ttu-id="b48b3-118">2.修改 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b48b3-118">2. Modify hello IP address.</span></span>

<span data-ttu-id="b48b3-119">您也可以修改在 hello hello 位址前置詞相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b48b3-119">You can also modify hello address prefixes at hello same time.</span></span>

1. <span data-ttu-id="b48b3-120">在 hello **IP 位址**方塊中，修改 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b48b3-120">In hello **IP address** box, modify hello IP address.</span></span>
2. <span data-ttu-id="b48b3-121">按一下**儲存**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="b48b3-121">Click **Save** toosave hello settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="b48b3-122">3.重新建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b48b3-122">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="b48b3-123">瀏覽您的 VNet toohello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b48b3-123">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="b48b3-124">(不 hello 本機網路閘道。)</span><span class="sxs-lookup"><span data-stu-id="b48b3-124">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="b48b3-125">在 hello 虛擬網路閘道，在 hello**設定**區段中，按一下**連線**。</span><span class="sxs-lookup"><span data-stu-id="b48b3-125">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="b48b3-126">按一下 hello **+ 加**tooopen hello**加入連接**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b48b3-126">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="b48b3-127">重新建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="b48b3-127">Recreate your connection.</span></span>
5. <span data-ttu-id="b48b3-128">按一下**確定**toocreate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b48b3-128">Click **OK** toocreate hello connection.</span></span>
