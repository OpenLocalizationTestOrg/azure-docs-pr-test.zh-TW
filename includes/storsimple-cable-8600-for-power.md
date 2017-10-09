<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a><span data-ttu-id="494c0-101">toocable 裝置的電源</span><span class="sxs-lookup"><span data-stu-id="494c0-101">toocable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="494c0-102">在 StorSimple 裝置上的兩個機箱都包括備援 PCM。</span><span class="sxs-lookup"><span data-stu-id="494c0-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="494c0-103">對於每個機箱，hello Pcm 必須安裝並連接 toodifferent 電源來源 tooensure 高可用性。</span><span class="sxs-lookup"><span data-stu-id="494c0-103">For each enclosure, hello PCMs must be installed and connected toodifferent power sources tooensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="494c0-104">請確定 hello 上所有的 hello Pcm 的電源開關是在 hello OFF 位置。</span><span class="sxs-lookup"><span data-stu-id="494c0-104">Make sure that hello power switches on all hello PCMs are in hello OFF position.</span></span>
2. <span data-ttu-id="494c0-105">在 hello 主要機箱，以連接 hello 電源線 tooboth Pcm。</span><span class="sxs-lookup"><span data-stu-id="494c0-105">On hello primary enclosure, connect hello power cords tooboth PCMs.</span></span> <span data-ttu-id="494c0-106">hello 電源佈線下方的圖表中以紅色識別 hello 電源線。</span><span class="sxs-lookup"><span data-stu-id="494c0-106">hello power cords are identified in red in hello power cabling diagram, below.</span></span>
3. <span data-ttu-id="494c0-107">請確定的 hello hello 主要機箱使用不同的電源上兩個 Pcm。</span><span class="sxs-lookup"><span data-stu-id="494c0-107">Make sure that hello two PCMs on hello primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="494c0-108">附加 hello 電源線 toohello 開機 hello 發佈架式 hello 電源佈線圖表所示。</span><span class="sxs-lookup"><span data-stu-id="494c0-108">Attach hello power cords toohello power on hello rack distribution units as shown in hello power cabling diagram.</span></span>
5. <span data-ttu-id="494c0-109">針對 hello EBOD 機箱重複步驟 2 到 4。</span><span class="sxs-lookup"><span data-stu-id="494c0-109">Repeat steps 2 through 4 for hello EBOD enclosure.</span></span>
6. <span data-ttu-id="494c0-110">開啟 hello EBOD 機箱電源開關撥 hello 上每個 PCM toohello 開啟 」 位置。</span><span class="sxs-lookup"><span data-stu-id="494c0-110">Turn on hello EBOD enclosure by flipping hello power switch on each PCM toohello ON position.</span></span>
7. <span data-ttu-id="494c0-111">請確認該 hello EBOD 機箱已開啟藉由檢查上 hello hello EBOD 控制器背面的綠色 hello Led 已開啟。</span><span class="sxs-lookup"><span data-stu-id="494c0-111">Verify that hello EBOD enclosure is turned on by checking that hello green LEDs on hello back of hello EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="494c0-112">開啟主要機箱 hello 翻轉每個 PCM 開關 toohello 開啟 」 位置。</span><span class="sxs-lookup"><span data-stu-id="494c0-112">Turn on hello primary enclosure by flipping each PCM switch toohello ON position.</span></span>
9. <span data-ttu-id="494c0-113">請確認 hello 系統上透過確保 hello 裝置控制器 Led 已開啟。</span><span class="sxs-lookup"><span data-stu-id="494c0-113">Verify that hello system is on by ensuring hello device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="494c0-114">請確定 hello hello EBOD 控制器與 hello 裝置控制器之間的連線是作用中驗證 hello 四個 Led 下一步 toohello SAS 連接埠 hello EBOD 控制器上的為綠色。</span><span class="sxs-lookup"><span data-stu-id="494c0-114">Make sure that hello connection between hello EBOD controller and hello device controller is active by verifying that hello four LEDs next toohello SAS port on hello EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="494c0-115">tooensure 系統的高可用性，建議您嚴格遵守 toohello 電源佈線配置 hello 下列圖表所示。</span><span class="sxs-lookup"><span data-stu-id="494c0-115">tooensure high availability for your system, we recommend that you strictly adhere toohello power cabling scheme shown in hello following diagram.</span></span>
    > 
    > 
    
    ![將您的 4U 裝置接上纜線，以取得電源](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="494c0-117">**電源佈線**</span><span class="sxs-lookup"><span data-stu-id="494c0-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="494c0-118">標籤</span><span class="sxs-lookup"><span data-stu-id="494c0-118">Label</span></span> | <span data-ttu-id="494c0-119">說明</span><span class="sxs-lookup"><span data-stu-id="494c0-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="494c0-120">1</span><span class="sxs-lookup"><span data-stu-id="494c0-120">1</span></span> |<span data-ttu-id="494c0-121">主要機箱</span><span class="sxs-lookup"><span data-stu-id="494c0-121">Primary enclosure</span></span> |
    | <span data-ttu-id="494c0-122">2</span><span class="sxs-lookup"><span data-stu-id="494c0-122">2</span></span> |<span data-ttu-id="494c0-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="494c0-123">PCM 0</span></span> |
    | <span data-ttu-id="494c0-124">3</span><span class="sxs-lookup"><span data-stu-id="494c0-124">3</span></span> |<span data-ttu-id="494c0-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="494c0-125">PCM 1</span></span> |
    | <span data-ttu-id="494c0-126">4</span><span class="sxs-lookup"><span data-stu-id="494c0-126">4</span></span> |<span data-ttu-id="494c0-127">控制器 0</span><span class="sxs-lookup"><span data-stu-id="494c0-127">Controller 0</span></span> |
    | <span data-ttu-id="494c0-128">5</span><span class="sxs-lookup"><span data-stu-id="494c0-128">5</span></span> |<span data-ttu-id="494c0-129">控制器 1</span><span class="sxs-lookup"><span data-stu-id="494c0-129">Controller 1</span></span> |
    | <span data-ttu-id="494c0-130">6</span><span class="sxs-lookup"><span data-stu-id="494c0-130">6</span></span> |<span data-ttu-id="494c0-131">EBOD 控制器 0</span><span class="sxs-lookup"><span data-stu-id="494c0-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="494c0-132">7</span><span class="sxs-lookup"><span data-stu-id="494c0-132">7</span></span> |<span data-ttu-id="494c0-133">EBOD 控制器 1</span><span class="sxs-lookup"><span data-stu-id="494c0-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="494c0-134">8</span><span class="sxs-lookup"><span data-stu-id="494c0-134">8</span></span> |<span data-ttu-id="494c0-135">EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="494c0-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="494c0-136">9</span><span class="sxs-lookup"><span data-stu-id="494c0-136">9</span></span> |<span data-ttu-id="494c0-137">PDU</span><span class="sxs-lookup"><span data-stu-id="494c0-137">PDUs</span></span> |

