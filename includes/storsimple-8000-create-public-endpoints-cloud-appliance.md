#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="b62c2-101">toocreate hello 雲端應用裝置上的公用端點</span><span class="sxs-lookup"><span data-stu-id="b62c2-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="b62c2-102">登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b62c2-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="b62c2-103">跳過**虛擬機器**，然後選取並按一下 hello 作為您的雲端應用裝置的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b62c2-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="b62c2-104">您需要 toocreate 網路安全性 (nsg) 規則 toocontrol hello 流量的流量進出虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b62c2-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="b62c2-105">執行下列步驟 toocreate NSG 規則 hello。</span><span class="sxs-lookup"><span data-stu-id="b62c2-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="b62c2-106">選擇 [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="b62c2-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="b62c2-107">按一下 hello 預設網路安全性小組呈現。</span><span class="sxs-lookup"><span data-stu-id="b62c2-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="b62c2-108">選取 [輸入安全性規則]。</span><span class="sxs-lookup"><span data-stu-id="b62c2-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="b62c2-109">按一下**+ 加**toocreate 連入的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="b62c2-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="b62c2-110">在 [hello 新增連入的安全性規則] 刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="b62c2-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="b62c2-111">Hello**名稱**，輸入 hello 下列命名 hello 端點： WinRMHttps。</span><span class="sxs-lookup"><span data-stu-id="b62c2-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="b62c2-112">Hello**優先順序**，選取的數字小於 1000年 （即 hello hello 預設規則的優先順序）。</span><span class="sxs-lookup"><span data-stu-id="b62c2-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="b62c2-113">Hello 值越高，hello 優先順序。</span><span class="sxs-lookup"><span data-stu-id="b62c2-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="b62c2-114">設定 hello**來源**太**任何**。</span><span class="sxs-lookup"><span data-stu-id="b62c2-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="b62c2-115">Hello**服務**，選取**WinRM**。</span><span class="sxs-lookup"><span data-stu-id="b62c2-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="b62c2-116">hello**通訊協定**會自動設定太**TCP**和 hello**連接埠範圍**設定得**5986**。</span><span class="sxs-lookup"><span data-stu-id="b62c2-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="b62c2-117">按一下**確定**toocreate hello 規則。</span><span class="sxs-lookup"><span data-stu-id="b62c2-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="b62c2-118">最後一個步驟是的 tooassociate 群組與子網路或特定的網路介面的網路安全性。</span><span class="sxs-lookup"><span data-stu-id="b62c2-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="b62c2-119">執行下列步驟 tooassociate hello 您與子網路的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="b62c2-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="b62c2-120">跳過**子網路**。</span><span class="sxs-lookup"><span data-stu-id="b62c2-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="b62c2-121">按一下 [+ 關聯]。</span><span class="sxs-lookup"><span data-stu-id="b62c2-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="b62c2-122">選取您的虛擬網路，然後選取 hello 適當的子網路。</span><span class="sxs-lookup"><span data-stu-id="b62c2-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="b62c2-123">按一下**確定**toocreate hello 規則。</span><span class="sxs-lookup"><span data-stu-id="b62c2-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="b62c2-124">建立 hello 規則之後，您可以檢視其詳細資料 toodetermine hello 公用虛擬 IP (VIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="b62c2-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="b62c2-125">請記下此位址。</span><span class="sxs-lookup"><span data-stu-id="b62c2-125">Record this address.</span></span>


