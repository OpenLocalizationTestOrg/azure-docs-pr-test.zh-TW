> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab483-101">Windows 上的 C</span><span class="sxs-lookup"><span data-stu-id="ab483-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="ab483-102">Linux 上的 C</span><span class="sxs-lookup"><span data-stu-id="ab483-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="ab483-103">Node.js</span><span class="sxs-lookup"><span data-stu-id="ab483-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="ab483-104">案例概觀</span><span class="sxs-lookup"><span data-stu-id="ab483-104">Scenario overview</span></span>
<span data-ttu-id="ab483-105">在此案例中，您會建立傳送嗨遵循遙測 toohello 遠端監視的裝置[預先設定的解決方案][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="ab483-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="ab483-106">外部溫度</span><span class="sxs-lookup"><span data-stu-id="ab483-106">External temperature</span></span>
* <span data-ttu-id="ab483-107">內部溫度</span><span class="sxs-lookup"><span data-stu-id="ab483-107">Internal temperature</span></span>
* <span data-ttu-id="ab483-108">溼度</span><span class="sxs-lookup"><span data-stu-id="ab483-108">Humidity</span></span>

<span data-ttu-id="ab483-109">為了簡單起見，hello hello 裝置上的程式碼會產生範例值，但我們鼓勵您 tooextend hello 範例實際感應器 tooyour 裝置連接和傳送實際的遙測。</span><span class="sxs-lookup"><span data-stu-id="ab483-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="ab483-110">hello 裝置也是可以 toorespond toomethods hello 方案儀表板從叫用，且想要設定 hello 方案儀表板中的屬性值。</span><span class="sxs-lookup"><span data-stu-id="ab483-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="ab483-111">toocomplete 本教學課程中，您需要使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ab483-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="ab483-112">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ab483-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ab483-113">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="ab483-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ab483-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="ab483-114">Before you start</span></span>
<span data-ttu-id="ab483-115">在您為裝置撰寫任何程式碼之前，您必須先佈建遠端監視預先設定解決方案，並在該解決方案中佈建新的自訂裝置。</span><span class="sxs-lookup"><span data-stu-id="ab483-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ab483-116">佈建遠端監視預先設定解決方案</span><span class="sxs-lookup"><span data-stu-id="ab483-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="ab483-117">您在本教學課程中建立的 hello 裝置傳送嗨資料 tooan 執行個體[遠端監視][ lnk-remote-monitoring]預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="ab483-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="ab483-118">如果您沒有已佈建 hello 遠端監視您的 Azure 帳戶中預先設定的解決方案，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab483-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="ab483-119">在 hello <https://www.azureiotsuite.com/>頁面上，按一下 **+**  toocreate 方案。</span><span class="sxs-lookup"><span data-stu-id="ab483-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="ab483-120">按一下**選取**上 hello**遠端監視**面板 toocreate 您的方案。</span><span class="sxs-lookup"><span data-stu-id="ab483-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="ab483-121">在 hello**建立遠端監視解決方案**頁面上，輸入**方案名稱**您選擇的選取 hello**區域**toodeploy，再選取 hello Azure訂用帳戶 toowant toouse。</span><span class="sxs-lookup"><span data-stu-id="ab483-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="ab483-122">按一下 [建立解決方案] 。</span><span class="sxs-lookup"><span data-stu-id="ab483-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="ab483-123">等待直到 hello 佈建程序完成。</span><span class="sxs-lookup"><span data-stu-id="ab483-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="ab483-124">預先設定的 hello 解決方案會使用可計費的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="ab483-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="ab483-125">請務必 tooremove hello 預先設定的方案，從您的訂用帳戶，當您在與其 tooavoid 任何不必要的費用。</span><span class="sxs-lookup"><span data-stu-id="ab483-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="ab483-126">您可以完整移除預先設定的方案從您的訂用帳戶瀏覽 hello <https://www.azureiotsuite.com/>頁面。</span><span class="sxs-lookup"><span data-stu-id="ab483-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="ab483-127">Hello 佈建 hello 遠端監視解決方案的程序完成時，請按一下**啟動**tooopen hello 方案儀表板在您的瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="ab483-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![解決方案儀表板][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="ab483-129">佈建您的裝置 hello 遠端監視解決方案中</span><span class="sxs-lookup"><span data-stu-id="ab483-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="ab483-130">如果您已經在解決方案中佈建裝置，則可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="ab483-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="ab483-131">當您建立 hello 用戶端應用程式時，您會需要 tooknow hello 裝置認證。</span><span class="sxs-lookup"><span data-stu-id="ab483-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="ab483-132">提供裝置 tooconnect toohello 預先設定的解決方案，它必須將自己識別 tooIoT 集線器使用有效的認證。</span><span class="sxs-lookup"><span data-stu-id="ab483-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="ab483-133">您可以擷取 hello 裝置認證從 hello 方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="ab483-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="ab483-134">您稍後在本教學課程中，用戶端應用程式包含 hello 裝置認證。</span><span class="sxs-lookup"><span data-stu-id="ab483-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="ab483-135">tooadd 裝置 tooyour 遠端監視解決方案，下列的完整 hello hello 方案儀表板中的步驟：</span><span class="sxs-lookup"><span data-stu-id="ab483-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="ab483-136">在 hello 左下角的 hello 儀表板，按一下 **新增裝置**。</span><span class="sxs-lookup"><span data-stu-id="ab483-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![新增裝置][1]
2. <span data-ttu-id="ab483-138">在 hello**自訂裝置** 面板中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="ab483-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![新增自訂裝置][2]
3. <span data-ttu-id="ab483-140">選擇 [讓我定義自己的裝置識別碼]。</span><span class="sxs-lookup"><span data-stu-id="ab483-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="ab483-141">輸入裝置識別碼，例如**mydevice**，按一下 **檢查識別碼**tooverify 還未在使用中，該名稱，然後按一下**建立**tooprovision hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="ab483-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![新增裝置識別碼][3]
4. <span data-ttu-id="ab483-143">請注意 hello 裝置認證 （裝置識別碼、 IoT 中樞的主機名稱、 和裝置金鑰）。</span><span class="sxs-lookup"><span data-stu-id="ab483-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="ab483-144">用戶端應用程式需要這些值 tooconnect toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="ab483-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="ab483-145">然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="ab483-145">Then click **Done**.</span></span>
   
    ![檢視裝置認證][4]
5. <span data-ttu-id="ab483-147">Hello hello 方案儀表板中的裝置清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="ab483-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="ab483-148">然後，在 hello**裝置詳細資料**] 面板中，按一下 [**啟用裝置**。</span><span class="sxs-lookup"><span data-stu-id="ab483-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="ab483-149">您的裝置 hello 狀態現在是**執行**。</span><span class="sxs-lookup"><span data-stu-id="ab483-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="ab483-150">hello 遠端監視解決方案現在可以從您的裝置接收遙測，並叫用 hello 裝置上的方法。</span><span class="sxs-lookup"><span data-stu-id="ab483-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/