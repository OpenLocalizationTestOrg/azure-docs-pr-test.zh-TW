<!--author=alkohli last changed: 9/17/15-->

#### <a name="to-complete-the-minimum-storsimple-device-setup"></a><span data-ttu-id="5871c-101">完成最小的 StorSimple 裝置安裝</span><span class="sxs-lookup"><span data-stu-id="5871c-101">To complete the minimum StorSimple device setup</span></span>
1. <span data-ttu-id="5871c-102">在 [裝置]  頁面上，選取裝置、按一下針對裝置名稱的箭頭，移至特定裝置頁面。</span><span class="sxs-lookup"><span data-stu-id="5871c-102">In the **Devices** page, select the device, click the arrow against the device name to go to the specific device page.</span></span> 
   
    ![裝置上線時的裝置頁面](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. <span data-ttu-id="5871c-104">按一下快速啟動圖示 ![快速啟動圖示](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) 存取裝置的快速啟動頁面。</span><span class="sxs-lookup"><span data-stu-id="5871c-104">Click quick start icon ![Quick Start Icon](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) to access the device quick start page.</span></span> <span data-ttu-id="5871c-105">按一下 [完成裝置設定] 以啟動**設定裝置**精靈。</span><span class="sxs-lookup"><span data-stu-id="5871c-105">Click **Complete device setup** to start the **Configure device** wizard.</span></span>
   
    ![StorSimple 快速啟動頁面](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. <span data-ttu-id="5871c-107">在 [基本設定]  頁面上，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="5871c-107">On the **Basic Settings** page, do the following:</span></span>
   
   1. <span data-ttu-id="5871c-108">為裝置提供 [易記名稱]  。</span><span class="sxs-lookup"><span data-stu-id="5871c-108">Supply a **friendly name** for your device.</span></span> <span data-ttu-id="5871c-109">預設的裝置名稱會反映裝置型號及序號等資訊。</span><span class="sxs-lookup"><span data-stu-id="5871c-109">The default device name reflects information such as the device model and serial number.</span></span> <span data-ttu-id="5871c-110">您最多可為易記名稱指定 64 個字元來管理您的裝置。</span><span class="sxs-lookup"><span data-stu-id="5871c-110">You can assign a friendly name of up to 64 characters to manage your device.</span></span>
   2. <span data-ttu-id="5871c-111">根據部署裝置的地理位置來設定 [時區]  。</span><span class="sxs-lookup"><span data-stu-id="5871c-111">Set the **time zone** based on the geographic location in which the device is being deployed.</span></span> <span data-ttu-id="5871c-112">裝置將針對所有排程的操作使用這個時區。</span><span class="sxs-lookup"><span data-stu-id="5871c-112">Your device will use this time zone for all scheduled operations.</span></span>
   3. <span data-ttu-id="5871c-113">在 [DNS 設定] 下方，提供 [次要 DNS 伺服器] 的位址。</span><span class="sxs-lookup"><span data-stu-id="5871c-113">Under **DNS Settings**, provide an address for your **Secondary DNS Server**.</span></span> <span data-ttu-id="5871c-114">如果您使用的是 IPv6，將根據 Windows PowerShell 介面中提供的 IPv6 首碼來填入欄位。</span><span class="sxs-lookup"><span data-stu-id="5871c-114">If you are using IPv6, the field will be populated based on the IPv6 prefix provided in the Windows PowerShell interface.</span></span> 
      <span data-ttu-id="5871c-115">如果未設定次要 DNS 伺服器，您將無法儲存裝置設定。</span><span class="sxs-lookup"><span data-stu-id="5871c-115">If the secondary DNS server is not configured, you will not be allowed to save your device configuration.</span></span>
   4. <span data-ttu-id="5871c-116">在啟用 iSCSI 的介面下方，至少啟用一個適用於 iSCSI 的網路。</span><span class="sxs-lookup"><span data-stu-id="5871c-116">Under iSCSI enabled interfaces, enable at least one network for iSCSI.</span></span> <span data-ttu-id="5871c-117">至少有一個網路介面必須具備雲端功能，而且有一個介面必須是已啟用 iSCSI 的介面。</span><span class="sxs-lookup"><span data-stu-id="5871c-117">At least one network interface needs to be cloud-enabled and one interface needs to be iSCSI-enabled.</span></span> <span data-ttu-id="5871c-118">DATA 0 會自動具備雲端功能。</span><span class="sxs-lookup"><span data-stu-id="5871c-118">DATA 0 is automatically cloud-enabled.</span></span>
      
      ![StorSimple 最小裝置設定基本設定](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. <span data-ttu-id="5871c-120">按一下箭頭圖示。</span><span class="sxs-lookup"><span data-stu-id="5871c-120">Click the arrow icon.</span></span> ![StorSimple 箭頭圖示](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. <span data-ttu-id="5871c-122">在 [網路介面]  頁面上，提供控制站 0 和控制站 1 的固定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5871c-122">On the **Network Interfaces** page, provide the fixed IP addresses for Controller 0 and Controller 1.</span></span> <span data-ttu-id="5871c-123">如果 DATA 0 介面是針對 IPv4 所設定，就必須以 IPv4 格式提供固定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5871c-123">If the DATA 0 interface was configured for IPv4, the fixed IP addresses need to be provided in the IPv4 format.</span></span> <span data-ttu-id="5871c-124">如果您提供適用於 IPv6 設定的首碼，則固定的 IP 位址將自動填入這些欄位中。</span><span class="sxs-lookup"><span data-stu-id="5871c-124">If you provided a prefix for IPv6 configuration, the fixed IP addresses will be populated automatically in these fields.</span></span>

    > [!NOTE] 
    > - <span data-ttu-id="5871c-125">控制站的固定 IP 位址必須是裝置 IP 位址可存取的子網路內的可用 IP。</span><span class="sxs-lookup"><span data-stu-id="5871c-125">The controller fixed IP addresses need to be free IPs within the subnet accessible by the device IP address.</span></span>
    > - <span data-ttu-id="5871c-126">適用於控制站的固定 IP 位址可用來為裝置提供更新，因此，固定的 IP 必須可路由傳送，而且能夠連線到網際網路。</span><span class="sxs-lookup"><span data-stu-id="5871c-126">The fixed IP addresses for the controller are used for servicing the updates to the device, and therefore the fixed IPs must be routable and able to connect to the Internet.</span></span>

    ![StorSimple 最小裝置設定網路介面](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. <span data-ttu-id="5871c-128">按一下核取圖示 ![StorSimple 核取圖示](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png)的位址。</span><span class="sxs-lookup"><span data-stu-id="5871c-128">Click the check icon ![StorSimple check icon](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).</span></span>
   <span data-ttu-id="5871c-129">您將會回到裝置的 [快速入門]  頁面。</span><span class="sxs-lookup"><span data-stu-id="5871c-129">You will return to the device **Quick Start** page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5871c-130">您可以隨時存取  **設定** 頁面。</span><span class="sxs-lookup"><span data-stu-id="5871c-130">You can modify all the other device settings at any time by accessing the **Configure** page.</span></span>
   > 
   > 

<span data-ttu-id="5871c-131">![提供的影片](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="5871c-131">![Video available](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="5871c-132">若要觀看影片示範如何完成最小量裝置設定，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/)。</span><span class="sxs-lookup"><span data-stu-id="5871c-132">To watch a video that demonstrates how to complete the minimum device setup, click [here](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).</span></span>

