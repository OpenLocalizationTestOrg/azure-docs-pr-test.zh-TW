## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="9e99a-101">檢視 hello 方案儀表板</span><span class="sxs-lookup"><span data-stu-id="9e99a-101">View hello solution dashboard</span></span>

<span data-ttu-id="9e99a-102">hello 方案儀表板可讓您 toomanage hello 部署方案。</span><span class="sxs-lookup"><span data-stu-id="9e99a-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="9e99a-103">例如，您可以檢視遙測、新增裝置及叫用方法。</span><span class="sxs-lookup"><span data-stu-id="9e99a-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="9e99a-104">當 hello 佈建已完成，且您預先設定的解決方案 hello 磚指出**準備**，選擇**啟動**tooopen 遠端監視方案入口網站中的新索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9e99a-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![啟動 hello 預先設定的解決方案][img-launch-solution]

1. <span data-ttu-id="9e99a-106">根據預設，hello 方案入口網站會顯示 hello*儀表板*。</span><span class="sxs-lookup"><span data-stu-id="9e99a-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="9e99a-107">您可以瀏覽 tooother hello 方案入口網站左側 hello hello 頁面使用 hello 功能表區域。</span><span class="sxs-lookup"><span data-stu-id="9e99a-107">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![遠端監視預先設定解決方案儀表板][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="9e99a-109">新增裝置</span><span class="sxs-lookup"><span data-stu-id="9e99a-109">Add a device</span></span>

<span data-ttu-id="9e99a-110">提供裝置 tooconnect toohello 預先設定的解決方案，它必須將自己識別 tooIoT 集線器使用有效的認證。</span><span class="sxs-lookup"><span data-stu-id="9e99a-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="9e99a-111">您可以擷取 hello 裝置認證從 hello 方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="9e99a-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="9e99a-112">您稍後在本教學課程中，用戶端應用程式包含 hello 裝置認證。</span><span class="sxs-lookup"><span data-stu-id="9e99a-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="9e99a-113">如果您尚未這樣做，請加入自訂裝置 tooyour 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="9e99a-113">If you haven't already done so, add a custom device tooyour remote monitoring solution.</span></span> <span data-ttu-id="9e99a-114">完成下列步驟 hello 方案儀表板中的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e99a-114">Complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="9e99a-115">在 hello 左下角的 hello 儀表板，按一下 **新增裝置**。</span><span class="sxs-lookup"><span data-stu-id="9e99a-115">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![新增裝置][1]

1. <span data-ttu-id="9e99a-117">在 hello**自訂裝置** 面板中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="9e99a-117">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![新增自訂裝置][2]

1. <span data-ttu-id="9e99a-119">選擇 [讓我定義自己的裝置識別碼]。</span><span class="sxs-lookup"><span data-stu-id="9e99a-119">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="9e99a-120">輸入裝置識別碼，例如**rasppi**，按一下 **檢查識別碼**tooverify 您您尚未使用您在方案中 hello 名稱，然後按一下**建立**tooprovision hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="9e99a-120">Enter a Device ID such as **rasppi**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![新增裝置識別碼][3]

1. <span data-ttu-id="9e99a-122">請注意 hello 裝置認證 (**裝置識別碼**， **IoT 中樞的主機名稱**，和**裝置金鑰**)。</span><span class="sxs-lookup"><span data-stu-id="9e99a-122">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="9e99a-123">用戶端應用程式上 hello 覆盆子 Pi 需要這些值 tooconnect toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="9e99a-123">Your client application on hello Raspberry Pi needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="9e99a-124">然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="9e99a-124">Then click **Done**.</span></span>

    ![檢視裝置認證][4]

1. <span data-ttu-id="9e99a-126">Hello hello 方案儀表板中的裝置清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="9e99a-126">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="9e99a-127">然後，在 hello**裝置詳細資料**] 面板中，按一下 [**啟用裝置**。</span><span class="sxs-lookup"><span data-stu-id="9e99a-127">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="9e99a-128">您的裝置 hello 狀態現在是**執行**。</span><span class="sxs-lookup"><span data-stu-id="9e99a-128">hello status of your device is now **Running**.</span></span> <span data-ttu-id="9e99a-129">hello 遠端監視解決方案現在可以從您的裝置接收遙測，並叫用 hello 裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="9e99a-129">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-raspberry-pi-kit-view-solution/launch.png
[img-menu]: media/iot-suite-raspberry-pi-kit-view-solution/menu.png
[1]: media/iot-suite-raspberry-pi-kit-view-solution/suite0.png
[2]: media/iot-suite-raspberry-pi-kit-view-solution/suite1.png
[3]: media/iot-suite-raspberry-pi-kit-view-solution/suite2.png
[4]: media/iot-suite-raspberry-pi-kit-view-solution/suite3.png