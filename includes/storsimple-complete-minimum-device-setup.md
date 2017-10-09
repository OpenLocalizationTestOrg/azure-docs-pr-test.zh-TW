<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a><span data-ttu-id="84642-101">toocomplete hello 最小 StorSimple 裝置設定</span><span class="sxs-lookup"><span data-stu-id="84642-101">toocomplete hello minimum StorSimple device setup</span></span>
1. <span data-ttu-id="84642-102">在 hello**裝置**頁面上，選取 hello 裝置，請按一下 hello 箭頭 hello 裝置名稱 toogo toohello 特定裝置頁面。</span><span class="sxs-lookup"><span data-stu-id="84642-102">In hello **Devices** page, select hello device, click hello arrow against hello device name toogo toohello specific device page.</span></span> 
   
    ![裝置上線時的裝置頁面](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. <span data-ttu-id="84642-104">按一下 [快速入門圖示![快速入門] 圖示](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png)tooaccess hello 裝置快速入門頁面。</span><span class="sxs-lookup"><span data-stu-id="84642-104">Click quick start icon ![Quick Start Icon](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) tooaccess hello device quick start page.</span></span> <span data-ttu-id="84642-105">按一下**完成裝置設定**toostart hello**設定裝置**精靈。</span><span class="sxs-lookup"><span data-stu-id="84642-105">Click **Complete device setup** toostart hello **Configure device** wizard.</span></span>
   
    ![StorSimple 快速啟動頁面](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. <span data-ttu-id="84642-107">在 hello**基本設定**頁面上，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="84642-107">On hello **Basic Settings** page, do hello following:</span></span>
   
   1. <span data-ttu-id="84642-108">為裝置提供 [易記名稱]  。</span><span class="sxs-lookup"><span data-stu-id="84642-108">Supply a **friendly name** for your device.</span></span> <span data-ttu-id="84642-109">hello 預設裝置名稱會反映 hello 裝置型號和序號等資訊。</span><span class="sxs-lookup"><span data-stu-id="84642-109">hello default device name reflects information such as hello device model and serial number.</span></span> <span data-ttu-id="84642-110">您可以指派的易記名稱總 too64 字元 toomanage 您的裝置。</span><span class="sxs-lookup"><span data-stu-id="84642-110">You can assign a friendly name of up too64 characters toomanage your device.</span></span>
   2. <span data-ttu-id="84642-111">設定 hello**時區**根據裝置正在部署中的 hello hello 地理位置。</span><span class="sxs-lookup"><span data-stu-id="84642-111">Set hello **time zone** based on hello geographic location in which hello device is being deployed.</span></span> <span data-ttu-id="84642-112">裝置將針對所有排程的操作使用這個時區。</span><span class="sxs-lookup"><span data-stu-id="84642-112">Your device will use this time zone for all scheduled operations.</span></span>
   3. <span data-ttu-id="84642-113">在 [DNS 設定] 下方，提供 [次要 DNS 伺服器] 的位址。</span><span class="sxs-lookup"><span data-stu-id="84642-113">Under **DNS Settings**, provide an address for your **Secondary DNS Server**.</span></span> <span data-ttu-id="84642-114">如果您使用 IPv6 時，會根據 hello hello Windows PowerShell 介面中提供的 IPv6 首碼填入 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="84642-114">If you are using IPv6, hello field will be populated based on hello IPv6 prefix provided in hello Windows PowerShell interface.</span></span> 
      <span data-ttu-id="84642-115">如果未設定次要 DNS 伺服器 hello，則不會允許 toosave 裝置組態。</span><span class="sxs-lookup"><span data-stu-id="84642-115">If hello secondary DNS server is not configured, you will not be allowed toosave your device configuration.</span></span>
   4. <span data-ttu-id="84642-116">在啟用 iSCSI 的介面下方，至少啟用一個適用於 iSCSI 的網路。</span><span class="sxs-lookup"><span data-stu-id="84642-116">Under iSCSI enabled interfaces, enable at least one network for iSCSI.</span></span> <span data-ttu-id="84642-117">至少一個網路介面必須 toobe 具備雲端功能，且有一個介面具有 toobe iSCSI 功能。</span><span class="sxs-lookup"><span data-stu-id="84642-117">At least one network interface needs toobe cloud-enabled and one interface needs toobe iSCSI-enabled.</span></span> <span data-ttu-id="84642-118">DATA 0 會自動具備雲端功能。</span><span class="sxs-lookup"><span data-stu-id="84642-118">DATA 0 is automatically cloud-enabled.</span></span>
      
      ![StorSimple 最小裝置設定基本設定](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. <span data-ttu-id="84642-120">按一下 hello 箭號圖示。</span><span class="sxs-lookup"><span data-stu-id="84642-120">Click hello arrow icon.</span></span> ![StorSimple 箭頭圖示](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. <span data-ttu-id="84642-122">在 hello**網路介面**頁面上，提供 hello 固定 IP 位址，控制器 0 及控制器 1。</span><span class="sxs-lookup"><span data-stu-id="84642-122">On hello **Network Interfaces** page, provide hello fixed IP addresses for Controller 0 and Controller 1.</span></span> <span data-ttu-id="84642-123">如果 hello DATA 0 介面設定了 IPv4，hello 固定 IP 位址需要 toobe hello IPv4 格式提供。</span><span class="sxs-lookup"><span data-stu-id="84642-123">If hello DATA 0 interface was configured for IPv4, hello fixed IP addresses need toobe provided in hello IPv4 format.</span></span> <span data-ttu-id="84642-124">如果您提供 IPv6 設定的前置詞，hello 固定 IP 位址會自動填入這些欄位中。</span><span class="sxs-lookup"><span data-stu-id="84642-124">If you provided a prefix for IPv6 configuration, hello fixed IP addresses will be populated automatically in these fields.</span></span>

    > [!NOTE] 
    > - <span data-ttu-id="84642-125">hello 控制器固定 IP 位址需要 toobe 釋放 Ip hello 可存取的子網路內 hello 裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="84642-125">hello controller fixed IP addresses need toobe free IPs within hello subnet accessible by hello device IP address.</span></span>
    > - <span data-ttu-id="84642-126">hello 固定 hello 控制站的 IP 位址用於服務 hello 更新 toohello 裝置，並因此 hello 固定 Ip 必須可路由傳送，而且要能 tooconnect toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="84642-126">hello fixed IP addresses for hello controller are used for servicing hello updates toohello device, and therefore hello fixed IPs must be routable and able tooconnect toohello Internet.</span></span>

    ![StorSimple 最小裝置設定網路介面](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. <span data-ttu-id="84642-128">按一下核取圖示，hello ![StorSimple 核取圖示](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png)。</span><span class="sxs-lookup"><span data-stu-id="84642-128">Click hello check icon ![StorSimple check icon](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).</span></span>
   <span data-ttu-id="84642-129">您將會傳回 toohello 裝置**快速入門**頁面。</span><span class="sxs-lookup"><span data-stu-id="84642-129">You will return toohello device **Quick Start** page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="84642-130">您可以修改所有 hello 其他裝置設定隨時藉由存取 hello**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="84642-130">You can modify all hello other device settings at any time by accessing hello **Configure** page.</span></span>
   > 
   > 

<span data-ttu-id="84642-131">![提供的影片](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="84642-131">![Video available](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="84642-132">toowatch 的視訊，示範如何 toocomplete hello 最低裝置設定 中，按一下[這裡](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/)。</span><span class="sxs-lookup"><span data-stu-id="84642-132">toowatch a video that demonstrates how toocomplete hello minimum device setup, click [here](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).</span></span>

