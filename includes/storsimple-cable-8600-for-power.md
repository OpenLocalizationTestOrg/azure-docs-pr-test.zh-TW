<!--author=alkohli last changed: 9/16/15-->


#### <a name="to-cable-your-device-for-power"></a><span data-ttu-id="209f9-101">將您的裝置接上纜線，以取得電源</span><span class="sxs-lookup"><span data-stu-id="209f9-101">To cable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="209f9-102">在 StorSimple 裝置上的兩個機箱都包括備援 PCM。</span><span class="sxs-lookup"><span data-stu-id="209f9-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="209f9-103">針對每個機箱，PCM 都必須安裝，並且連接到不同的電源來源，以確保高可用性。</span><span class="sxs-lookup"><span data-stu-id="209f9-103">For each enclosure, the PCMs must be installed and connected to different power sources to ensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="209f9-104">請確定所有 PCM 上的電源開關是在 OFF (關閉) 位置。</span><span class="sxs-lookup"><span data-stu-id="209f9-104">Make sure that the power switches on all the PCMs are in the OFF position.</span></span>
2. <span data-ttu-id="209f9-105">在主要機箱上，將電源線連接至兩個 PCM。</span><span class="sxs-lookup"><span data-stu-id="209f9-105">On the primary enclosure, connect the power cords to both PCMs.</span></span> <span data-ttu-id="209f9-106">在底下的電源佈線圖表中以紅色識別電源線。</span><span class="sxs-lookup"><span data-stu-id="209f9-106">The power cords are identified in red in the power cabling diagram, below.</span></span>
3. <span data-ttu-id="209f9-107">確定主要機箱上的兩個 PCM 使用不同的電源來源。</span><span class="sxs-lookup"><span data-stu-id="209f9-107">Make sure that the two PCMs on the primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="209f9-108">將電源線連接至機架電源分配單元，如電源佈線圖表所示。</span><span class="sxs-lookup"><span data-stu-id="209f9-108">Attach the power cords to the power on the rack distribution units as shown in the power cabling diagram.</span></span>
5. <span data-ttu-id="209f9-109">針對 EBOD 機箱重複步驟 2 到 4。</span><span class="sxs-lookup"><span data-stu-id="209f9-109">Repeat steps 2 through 4 for the EBOD enclosure.</span></span>
6. <span data-ttu-id="209f9-110">將每個 PCM 上的電源開關切換到 ON (開啟) 位置，以開啟 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="209f9-110">Turn on the EBOD enclosure by flipping the power switch on each PCM to the ON position.</span></span>
7. <span data-ttu-id="209f9-111">確認 EBOD 機箱已開啟，方法是檢查 EBOD 控制器背面的綠色 LED 已開啟。</span><span class="sxs-lookup"><span data-stu-id="209f9-111">Verify that the EBOD enclosure is turned on by checking that the green LEDs on the back of the EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="209f9-112">將每個 PCM 的電源開關切換到 ON (開啟) 位置，以開啟主要機箱。</span><span class="sxs-lookup"><span data-stu-id="209f9-112">Turn on the primary enclosure by flipping each PCM switch to the ON position.</span></span>
9. <span data-ttu-id="209f9-113">確認系統已開啟，方法是確定裝置控制器 LED 已開啟。</span><span class="sxs-lookup"><span data-stu-id="209f9-113">Verify that the system is on by ensuring the device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="209f9-114">確定 EBOD 控制器和裝置控制站之間的連線為作用中，方法是確認 EBOD 控制器上 SAS 連接埠旁邊的 4 個 LED 是綠色。</span><span class="sxs-lookup"><span data-stu-id="209f9-114">Make sure that the connection between the EBOD controller and the device controller is active by verifying that the four LEDs next to the SAS port on the EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="209f9-115">若要確保系統的高可用性，我們建議您嚴格遵守電源佈線配置，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="209f9-115">To ensure high availability for your system, we recommend that you strictly adhere to the power cabling scheme shown in the following diagram.</span></span>
    > 
    > 
    
    ![將您的 4U 裝置接上纜線，以取得電源](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="209f9-117">**電源佈線**</span><span class="sxs-lookup"><span data-stu-id="209f9-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="209f9-118">標籤</span><span class="sxs-lookup"><span data-stu-id="209f9-118">Label</span></span> | <span data-ttu-id="209f9-119">說明</span><span class="sxs-lookup"><span data-stu-id="209f9-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="209f9-120">1</span><span class="sxs-lookup"><span data-stu-id="209f9-120">1</span></span> |<span data-ttu-id="209f9-121">主要機箱</span><span class="sxs-lookup"><span data-stu-id="209f9-121">Primary enclosure</span></span> |
    | <span data-ttu-id="209f9-122">2</span><span class="sxs-lookup"><span data-stu-id="209f9-122">2</span></span> |<span data-ttu-id="209f9-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="209f9-123">PCM 0</span></span> |
    | <span data-ttu-id="209f9-124">3</span><span class="sxs-lookup"><span data-stu-id="209f9-124">3</span></span> |<span data-ttu-id="209f9-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="209f9-125">PCM 1</span></span> |
    | <span data-ttu-id="209f9-126">4</span><span class="sxs-lookup"><span data-stu-id="209f9-126">4</span></span> |<span data-ttu-id="209f9-127">控制器 0</span><span class="sxs-lookup"><span data-stu-id="209f9-127">Controller 0</span></span> |
    | <span data-ttu-id="209f9-128">5</span><span class="sxs-lookup"><span data-stu-id="209f9-128">5</span></span> |<span data-ttu-id="209f9-129">控制器 1</span><span class="sxs-lookup"><span data-stu-id="209f9-129">Controller 1</span></span> |
    | <span data-ttu-id="209f9-130">6</span><span class="sxs-lookup"><span data-stu-id="209f9-130">6</span></span> |<span data-ttu-id="209f9-131">EBOD 控制器 0</span><span class="sxs-lookup"><span data-stu-id="209f9-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="209f9-132">7</span><span class="sxs-lookup"><span data-stu-id="209f9-132">7</span></span> |<span data-ttu-id="209f9-133">EBOD 控制器 1</span><span class="sxs-lookup"><span data-stu-id="209f9-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="209f9-134">8</span><span class="sxs-lookup"><span data-stu-id="209f9-134">8</span></span> |<span data-ttu-id="209f9-135">EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="209f9-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="209f9-136">9</span><span class="sxs-lookup"><span data-stu-id="209f9-136">9</span></span> |<span data-ttu-id="209f9-137">PDU</span><span class="sxs-lookup"><span data-stu-id="209f9-137">PDUs</span></span> |

