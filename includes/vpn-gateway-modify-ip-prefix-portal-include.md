### <span data-ttu-id="1bd4e-101"><a name="noconnection"></a>toomodify 區域網路閘道 IP 位址首碼不閘道連線</span><span class="sxs-lookup"><span data-stu-id="1bd4e-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="tooadd-additional-address-prefixes"></a><span data-ttu-id="1bd4e-102">tooadd 其他位址前置詞：</span><span class="sxs-lookup"><span data-stu-id="1bd4e-102">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="1bd4e-103">在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-103">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="1bd4e-104">新增 hello IP 位址空間中 hello*新增其他位址範圍*方塊。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-104">Add hello IP address space in hello *Add additional address range* box.</span></span>
3. <span data-ttu-id="1bd4e-105">按一下**儲存**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-105">Click **Save** toosave your settings.</span></span>

#### <a name="tooremove-address-prefixes"></a><span data-ttu-id="1bd4e-106">tooremove 位址首碼：</span><span class="sxs-lookup"><span data-stu-id="1bd4e-106">tooremove address prefixes:</span></span>

1. <span data-ttu-id="1bd4e-107">在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-107">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="1bd4e-108">按一下 hello **'...'**想 tooremove hello 包含 hello 前置詞的程式行。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-108">Click hello **'...'** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="1bd4e-109">按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-109">Click **Remove**.</span></span>
4. <span data-ttu-id="1bd4e-110">按一下**儲存**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-110">Click **Save** toosave your settings.</span></span>

### <span data-ttu-id="1bd4e-111"><a name="withconnection"></a>toomodify 區域網路閘道的 IP 位址首碼為現有的閘道連線</span><span class="sxs-lookup"><span data-stu-id="1bd4e-111"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="1bd4e-112">如果您有閘道連接和要 tooadd 或移除 hello IP 位址前置詞包含在您的本機網路閘道，您會需要 toodo hello 依照依順序的步驟。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-112">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="1bd4e-113">這會導致您 VPN 連線的停機時間。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="1bd4e-114">修改 IP 位址前置詞，您無須 toodelete hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-114">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="1bd4e-115">您只需要 tooremove hello 連線。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-115">You only need tooremove hello connection.</span></span>

#### <a name="1-remove-hello-connection"></a><span data-ttu-id="1bd4e-116">1.移除 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-116">1. Remove hello connection.</span></span>

1. <span data-ttu-id="1bd4e-117">在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**連線**。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-117">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="1bd4e-118">按一下 hello **...**在每個連線的 hello 一行，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-118">Click hello **...** on hello line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="1bd4e-119">按一下**儲存**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-119">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-address-prefixes"></a><span data-ttu-id="1bd4e-120">2.修改 hello 位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-120">2. Modify hello address prefixes.</span></span>

<span data-ttu-id="1bd4e-121">tooadd 其他位址前置詞：</span><span class="sxs-lookup"><span data-stu-id="1bd4e-121">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="1bd4e-122">在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-122">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="1bd4e-123">加入 hello IP 位址空間。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-123">Add hello IP address space.</span></span>
3. <span data-ttu-id="1bd4e-124">按一下**儲存**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-124">Click **Save** toosave your settings.</span></span>

<span data-ttu-id="1bd4e-125">tooremove 位址首碼：</span><span class="sxs-lookup"><span data-stu-id="1bd4e-125">tooremove address prefixes:</span></span>

1. <span data-ttu-id="1bd4e-126">在本機網路閘道資源，請在 hello hello**設定**區段中，按一下**組態**。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-126">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="1bd4e-127">按一下 hello **...**想 tooremove hello 包含 hello 前置詞的程式行。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-127">Click hello **...** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="1bd4e-128">按一下 [移除] 。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-128">Click **Remove**.</span></span>
4. <span data-ttu-id="1bd4e-129">按一下**儲存**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-129">Click **Save** toosave your settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="1bd4e-130">3.重新建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-130">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="1bd4e-131">瀏覽您的 VNet toohello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-131">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="1bd4e-132">(不 hello 本機網路閘道。)</span><span class="sxs-lookup"><span data-stu-id="1bd4e-132">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="1bd4e-133">在 hello 虛擬網路閘道，在 hello**設定**區段中，按一下**連線**。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-133">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="1bd4e-134">按一下 hello **+ 加**tooopen hello**加入連接**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-134">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="1bd4e-135">重新建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-135">Recreate your connection.</span></span>
5. <span data-ttu-id="1bd4e-136">按一下**確定**toocreate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="1bd4e-136">Click **OK** toocreate hello connection.</span></span>
