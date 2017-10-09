## <a name="view-hello-telemetry"></a><span data-ttu-id="df4fb-101">檢視 hello 遙測</span><span class="sxs-lookup"><span data-stu-id="df4fb-101">View hello telemetry</span></span>

<span data-ttu-id="df4fb-102">hello 覆盆子 Pi 現在正要傳送遙測 toohello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="df4fb-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="df4fb-103">您可以檢視 hello 遙測 hello 方案儀表板上。</span><span class="sxs-lookup"><span data-stu-id="df4fb-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="df4fb-104">您也可以傳送訊息 tooyour 覆盆子 Pi 從 hello 方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="df4fb-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="df4fb-105">瀏覽 toohello 方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="df4fb-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="df4fb-106">選取您的裝置在 hello**裝置 tooView**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="df4fb-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="df4fb-107">從 hello hello 遙測覆盆子 Pi 顯示 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="df4fb-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![顯示 hello 覆盆子 Pi 的遙測][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a><span data-ttu-id="df4fb-109">初始化 hello 韌體更新</span><span class="sxs-lookup"><span data-stu-id="df4fb-109">Initiate hello firmware update</span></span>

<span data-ttu-id="df4fb-110">hello 韌體更新程序上下載及安裝更新的版的 hello 裝置用戶端應用程式 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="df4fb-110">hello firmware update process downloads and installs an updated version of hello device client application on hello Raspberry Pi.</span></span> <span data-ttu-id="df4fb-111">如需 hello 韌體更新程序的詳細資訊，請參閱 hello 韌體更新模式中的 hello 描述[裝置管理概觀與 IoT 中樞][lnk-update-pattern]。</span><span class="sxs-lookup"><span data-stu-id="df4fb-111">For more information about hello firmware update process, see hello description of hello firmware update pattern in [Overview of device management with IoT Hub][lnk-update-pattern].</span></span>

<span data-ttu-id="df4fb-112">您可以叫用 hello 裝置上的方法，以起始 hello 韌體更新程序。</span><span class="sxs-lookup"><span data-stu-id="df4fb-112">You initiate hello firmware update process by invoking a method on hello device.</span></span> <span data-ttu-id="df4fb-113">這個方法是非同步的並傳回 hello 更新程序一開始。</span><span class="sxs-lookup"><span data-stu-id="df4fb-113">This method is asynchronous, and returns as soon as hello update process begins.</span></span> <span data-ttu-id="df4fb-114">hello 裝置會使用有關 hello hello 更新進度報告屬性 toonotify hello 方案。</span><span class="sxs-lookup"><span data-stu-id="df4fb-114">hello device uses reported properties toonotify hello solution about hello progress of hello update.</span></span>

<span data-ttu-id="df4fb-115">您在您的覆盆子 Pi 從 hello 方案儀表板上叫用方法。</span><span class="sxs-lookup"><span data-stu-id="df4fb-115">You invoke methods on your Raspberry Pi from hello solution dashboard.</span></span> <span data-ttu-id="df4fb-116">當 hello 覆盆子 Pi 第一次連接 toohello 遠端監視解決方案時，它會傳送 hello 方法，它支援的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="df4fb-116">When hello Raspberry Pi first connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span> 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
