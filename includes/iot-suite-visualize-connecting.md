## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="6ed54-101">Hello 儀表板中檢視裝置遙測</span><span class="sxs-lookup"><span data-stu-id="6ed54-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="6ed54-102">在遠端監視解決方案可讓您 tooview hello 遙測您的裝置傳送 tooIoT 中樞 hello hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="6ed54-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="6ed54-103">在瀏覽器中傳回 toohello 遠端監視方案儀表板，按一下 **裝置**在 hello 左側面板 toonavigate toohello**裝置清單**。</span><span class="sxs-lookup"><span data-stu-id="6ed54-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="6ed54-104">在 hello**裝置清單**，您應該會看到您的裝置 hello 狀態是**執行**。</span><span class="sxs-lookup"><span data-stu-id="6ed54-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="6ed54-105">如果沒有，請按一下**啟用裝置**在 hello**裝置詳細資料**面板。</span><span class="sxs-lookup"><span data-stu-id="6ed54-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![檢視裝置狀態][18]
3. <span data-ttu-id="6ed54-107">按一下**儀表板**tooreturn toohello 儀表板中，選取您的裝置在 hello**裝置 tooView**下拉式 tooview 其遙測。</span><span class="sxs-lookup"><span data-stu-id="6ed54-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="6ed54-108">來自 hello 範例應用程式的 hello 遙測是 50 個單位的內部溫度、 55 單位外部溫度和溼度的 50 個單位。</span><span class="sxs-lookup"><span data-stu-id="6ed54-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![檢視裝置遙測資料][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="6ed54-110">在裝置上叫用方法</span><span class="sxs-lookup"><span data-stu-id="6ed54-110">Invoke a method on your device</span></span>
<span data-ttu-id="6ed54-111">hello 遠端監視解決方案中的 hello 儀表板可讓您透過 IoT 中樞裝置上的 tooinvoke 方法。</span><span class="sxs-lookup"><span data-stu-id="6ed54-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="6ed54-112">比方說，在遠端監視解決方案的 hello 您可以叫用方法 toosimulate 重新開機裝置。</span><span class="sxs-lookup"><span data-stu-id="6ed54-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="6ed54-113">Hello 遠端監視方案儀表板中，按一下 **裝置**在 hello 左側面板 toonavigate toohello**裝置清單**。</span><span class="sxs-lookup"><span data-stu-id="6ed54-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="6ed54-114">按一下**裝置識別碼**裝置 hello**裝置清單**。</span><span class="sxs-lookup"><span data-stu-id="6ed54-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="6ed54-115">在 hello**裝置詳細資料** 面板中，按一下 **方法**。</span><span class="sxs-lookup"><span data-stu-id="6ed54-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![裝置方法][13]
4. <span data-ttu-id="6ed54-117">在 hello**方法**下拉式清單中，選取**InitiateFirmwareUpdate**，然後在**FWPACKAGEURI**輸入空的 URL。</span><span class="sxs-lookup"><span data-stu-id="6ed54-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="6ed54-118">按一下**叫用方法**toocall hello 方法 hello 裝置上的。</span><span class="sxs-lookup"><span data-stu-id="6ed54-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![叫用裝置方法][14]
   

5. <span data-ttu-id="6ed54-120">您會看到 hello 主控台 hello 裝置處理 hello 方法時，執行您裝置的程式碼中的訊息。</span><span class="sxs-lookup"><span data-stu-id="6ed54-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="6ed54-121">hello 方法結果的 hello hello 方案入口網站新增 toohello 歷程記錄：</span><span class="sxs-lookup"><span data-stu-id="6ed54-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![檢視方法歷程記錄][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="6ed54-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ed54-123">Next steps</span></span>
<span data-ttu-id="6ed54-124">hello 文章[預先設定的自訂方案][ lnk-customize]描述一些您可以擴充此範例的方法。</span><span class="sxs-lookup"><span data-stu-id="6ed54-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="6ed54-125">可能的延伸模組包括使用真實的感應器和實作其他命令。</span><span class="sxs-lookup"><span data-stu-id="6ed54-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="6ed54-126">您可以進一步了解 hello [hello azureiotsuite.com 網站的權限][lnk-permissions]。</span><span class="sxs-lookup"><span data-stu-id="6ed54-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
