## <a name="view-the-solution-dashboard"></a><span data-ttu-id="382a2-101">檢視解決方案儀表板</span><span class="sxs-lookup"><span data-stu-id="382a2-101">View the solution dashboard</span></span>

<span data-ttu-id="382a2-102">解決方案儀表板可讓您管理部署的解決方案。</span><span class="sxs-lookup"><span data-stu-id="382a2-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="382a2-103">例如，您可以檢視遙測、新增裝置及叫用方法。</span><span class="sxs-lookup"><span data-stu-id="382a2-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="382a2-104">當佈建完成且預先設定解決方案的圖格指示 [就緒] 時，選擇 [啟動] 以在新的索引標籤中開啟遠端監視解決方案入口網站。</span><span class="sxs-lookup"><span data-stu-id="382a2-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![啟動預先設定的解決方案][img-launch-solution]

1. <span data-ttu-id="382a2-106">根據預設，此解決方案入口網站會顯示儀表板。</span><span class="sxs-lookup"><span data-stu-id="382a2-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="382a2-107">使用頁面左側的功能表，瀏覽至解決方案入口網站的其他區域。</span><span class="sxs-lookup"><span data-stu-id="382a2-107">Navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![遠端監視預先設定解決方案儀表板][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="382a2-109">新增裝置</span><span class="sxs-lookup"><span data-stu-id="382a2-109">Add a device</span></span>

<span data-ttu-id="382a2-110">對於連線到預先設定解決方案的裝置，該裝置必須使用有效的認證向 IoT 中樞識別自己。</span><span class="sxs-lookup"><span data-stu-id="382a2-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="382a2-111">您會從解決方案儀表板收到裝置認證。</span><span class="sxs-lookup"><span data-stu-id="382a2-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="382a2-112">稍後在本教學課程中，您會將您的裝置認證包含在您的用戶端應用程式中。</span><span class="sxs-lookup"><span data-stu-id="382a2-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="382a2-113">若要在您的遠端監視解決方案中新增裝置，請在解決方案儀表板中完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="382a2-113">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="382a2-114">在儀表板左下角，按一下 [新增裝置] 。</span><span class="sxs-lookup"><span data-stu-id="382a2-114">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![新增裝置][1]

1. <span data-ttu-id="382a2-116">在 [自訂裝置] 面板中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="382a2-116">In the **Custom Device** panel, click **Add new**.</span></span>

   ![新增自訂裝置][2]

1. <span data-ttu-id="382a2-118">選擇 [讓我定義自己的裝置識別碼]。</span><span class="sxs-lookup"><span data-stu-id="382a2-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="382a2-119">輸入 [裝置識別碼]，例如 **device01**，按一下 [檢查識別碼] 以確認您尚未在解決方案中使用此名稱，然後按一下 [建立] 來佈建裝置。</span><span class="sxs-lookup"><span data-stu-id="382a2-119">Enter a Device ID such as **device01**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![新增裝置識別碼][3]

1. <span data-ttu-id="382a2-121">記下裝置認證 ([裝置識別碼]、[IoT 中樞主機名稱] 及 [裝置金鑰])。</span><span class="sxs-lookup"><span data-stu-id="382a2-121">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="382a2-122">Intel NUC 上的用戶端應用程式需要這些值，才能連線到遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="382a2-122">Your client application on the Intel NUC needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="382a2-123">然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="382a2-123">Then click **Done**.</span></span>

    ![檢視裝置認證][4]

1. <span data-ttu-id="382a2-125">從解決方案儀表板的裝置清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="382a2-125">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="382a2-126">然後，在 [裝置詳細資料] 面板中，按一下 [啟用裝置]。</span><span class="sxs-lookup"><span data-stu-id="382a2-126">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="382a2-127">裝置的狀態現在會是 [正在執行]。</span><span class="sxs-lookup"><span data-stu-id="382a2-127">The status of your device is now **Running**.</span></span> <span data-ttu-id="382a2-128">遠端監視解決方案現在已可從您的裝置接收遙測資料，並在該裝置上叫用方法。</span><span class="sxs-lookup"><span data-stu-id="382a2-128">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png