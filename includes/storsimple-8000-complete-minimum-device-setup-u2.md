<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a><span data-ttu-id="3eb3b-101">toocomplete hello 最小 StorSimple 裝置設定</span><span class="sxs-lookup"><span data-stu-id="3eb3b-101">toocomplete hello minimum StorSimple device setup</span></span>

   > [!NOTE]
   > <span data-ttu-id="3eb3b-102">Hello 最低裝置設定完成之後，您無法變更 hello 裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-102">You cannot change hello device name once hello minimum device setup is completed.</span></span>
   
1. <span data-ttu-id="3eb3b-103">從 hello 表格清單中的裝置 hello**裝置**刀鋒視窗中，選取，然後按一下您的裝置。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-103">From hello tabular listing of devices in hello **Devices** blade, select and click your device.</span></span> <span data-ttu-id="3eb3b-104">hello 裝置處於**已 tooset 準備註冊**狀態。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-104">hello device is in a **Ready tooset up** state.</span></span> <span data-ttu-id="3eb3b-105">hello**設定裝置**刀鋒視窗會開啟。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-105">hello **Configure device** blade opens up.</span></span>

     ![StorSimple 最小裝置設定網路介面](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. <span data-ttu-id="3eb3b-107">在 hello**設定裝置**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="3eb3b-107">In hello **Configure device** blade:</span></span>
   
   1. <span data-ttu-id="3eb3b-108">為裝置提供 [易記名稱]  。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-108">Supply a **friendly name** for your device.</span></span> <span data-ttu-id="3eb3b-109">hello 預設裝置名稱會反映 hello 裝置型號和序號等資訊。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-109">hello default device name reflects information such as hello device model and serial number.</span></span> <span data-ttu-id="3eb3b-110">您可以指派的易記名稱總 too64 字元 toomanage 您的裝置。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-110">You can assign a friendly name of up too64 characters toomanage your device.</span></span>
   2. <span data-ttu-id="3eb3b-111">設定 hello**時區**根據裝置正在部署中的 hello hello 地理位置。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-111">Set hello **time zone** based on hello geographic location in which hello device is being deployed.</span></span> <span data-ttu-id="3eb3b-112">裝置將針對所有排程作業使用這個時區。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-112">Your device uses this time zone for all scheduled operations.</span></span>
   3. <span data-ttu-id="3eb3b-113">在 hello **DATA 0 設定**:</span><span class="sxs-lookup"><span data-stu-id="3eb3b-113">Under hello **DATA 0 settings**:</span></span>

       1. <span data-ttu-id="3eb3b-114">您的 DATA 0 網路介面會顯示以 hello 啟用網路設定 IP、 子網路 （閘道） 透過 hello 安裝精靈設定。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-114">Your DATA 0 network interface shows as enabled with hello network settings (IP, subnet, gateway) configured via hello setup wizard.</span></span> <span data-ttu-id="3eb3b-115">也會針對雲端以及 iSCSI 將 DATA 0 自動啟用。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-115">DATA 0 is also automatically enabled for cloud as well as iSCSI.</span></span>

       2. <span data-ttu-id="3eb3b-116">提供 hello 固定 IP 位址，控制器 0 及控制器 1。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-116">Provide hello fixed IP addresses for Controller 0 and Controller 1.</span></span> <span data-ttu-id="3eb3b-117">**hello 控制器固定 IP 位址需要 toobe 釋放 Ip hello 可存取的子網路內 hello 裝置的 IP 位址。**</span><span class="sxs-lookup"><span data-stu-id="3eb3b-117">**hello controller fixed IP addresses need toobe free IPs within hello subnet accessible by hello device IP address.**</span></span> <span data-ttu-id="3eb3b-118">如果 hello DATA 0 介面設定了 IPv4，hello 固定 IP 位址需要 toobe hello IPv4 格式提供。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-118">If hello DATA 0 interface was configured for IPv4, hello fixed IP addresses need toobe provided in hello IPv4 format.</span></span> <span data-ttu-id="3eb3b-119">如果您提供 IPv6 設定的前置詞，hello 固定 IP 位址會自動填入這些欄位中。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-119">If you provided a prefix for IPv6 configuration, hello fixed IP addresses are populated automatically in these fields.</span></span>

            ![StorSimple 最小裝置設定網路介面](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            <span data-ttu-id="3eb3b-121">hello 固定 hello 控制站的 IP 位址可用來服務 hello 更新 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-121">hello fixed IP addresses for hello controller are used for servicing hello updates toohello device.</span></span> <span data-ttu-id="3eb3b-122">因此，hello 固定 Ip 必須可路由傳送，而且要能 tooconnect toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-122">Therefore, hello fixed IPs must be routable and able tooconnect toohello Internet.</span></span> <span data-ttu-id="3eb3b-123">您可以檢查您控制器固定的 Ip 可路由傳送使用 hello [Test-hcsmconnection] [ Test] cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-123">You can check that your fixed controller IPs are routable by using hello [Test-HcsmConnection][Test] cmdlet.</span></span> <span data-ttu-id="3eb3b-124">下列範例顯示固定控制器 Ip 路由的 toohello 網際網路並且可以存取的 hello hello Microsoft Update servers。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-124">hello following example shows fixed controller IPs are routed toohello Internet and can access hello Microsoft Update servers.</span></span>

            ![Test-HcsmConnection 顯示可路由傳送 IP](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. <span data-ttu-id="3eb3b-126">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-126">Click **OK**.</span></span> <span data-ttu-id="3eb3b-127">hello 裝置設定啟動。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-127">hello device configuration starts.</span></span> <span data-ttu-id="3eb3b-128">Hello 裝置設定完成時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-128">When hello device configuration is complete, you are notified.</span></span> <span data-ttu-id="3eb3b-129">hello 裝置狀態變更太**線上**在 hello**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3eb3b-129">hello device status changes too**Online** in hello **Devices** blade.</span></span>

    ![StorSimple 最小裝置設定網路介面](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
