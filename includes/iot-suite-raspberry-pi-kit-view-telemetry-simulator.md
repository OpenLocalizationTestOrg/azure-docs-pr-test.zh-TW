## <a name="view-the-telemetry"></a><span data-ttu-id="0d39d-101">檢視遙測資料</span><span class="sxs-lookup"><span data-stu-id="0d39d-101">View the telemetry</span></span>

<span data-ttu-id="0d39d-102">Raspberry Pi 現在會將遙測資料傳送至遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="0d39d-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="0d39d-103">您可以在解決方案儀表板上檢視遙測資料。</span><span class="sxs-lookup"><span data-stu-id="0d39d-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="0d39d-104">您也可以從解決方案儀表板將訊息傳送至 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="0d39d-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="0d39d-105">瀏覽至解決方案儀表板。</span><span class="sxs-lookup"><span data-stu-id="0d39d-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="0d39d-106">在 [要檢視的裝置] 下拉式清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="0d39d-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="0d39d-107">來自 Raspberry Pi 的遙測資料會顯示在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="0d39d-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![顯示來自 Raspberry Pi 的遙測資料][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="0d39d-109">在裝置上採取行動</span><span class="sxs-lookup"><span data-stu-id="0d39d-109">Act on the device</span></span>

<span data-ttu-id="0d39d-110">從解決方案儀表板，您可以在 Raspberry Pi 上叫用方法。</span><span class="sxs-lookup"><span data-stu-id="0d39d-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="0d39d-111">當 Raspberry Pi 連線到遠端監視解決方案時，它會傳送所支援方法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0d39d-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="0d39d-112">在解決方案儀表板中，按一下 [裝置] 以造訪 [裝置] 頁面。</span><span class="sxs-lookup"><span data-stu-id="0d39d-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="0d39d-113">在 [裝置清單] 中選取您的 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="0d39d-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="0d39d-114">然後選擇 [方法]：</span><span class="sxs-lookup"><span data-stu-id="0d39d-114">Then choose **Methods**:</span></span>

    ![在儀表板中列出裝置][img-list-devices]

- <span data-ttu-id="0d39d-116">在 [叫用方法] 頁面上，選擇 [方法] 下拉式清單中的 [LightBlink]。</span><span class="sxs-lookup"><span data-stu-id="0d39d-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="0d39d-117">選擇 [InvokeMethod]。</span><span class="sxs-lookup"><span data-stu-id="0d39d-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="0d39d-118">模擬器會在 Raspberry Pi 的主控台中列印一則訊息。</span><span class="sxs-lookup"><span data-stu-id="0d39d-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="0d39d-119">Raspberry Pi 上的應用程式會將通知傳回解決方案儀表板︰</span><span class="sxs-lookup"><span data-stu-id="0d39d-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![顯示方法歷程記錄][img-method-history]

- <span data-ttu-id="0d39d-121">您可以使用 **ChangeLightStatus** 方法並將 **LightStatusValue** 設定為 **1** (開啟) 或 **0** (關閉)，以開啟和關閉 LED。</span><span class="sxs-lookup"><span data-stu-id="0d39d-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="0d39d-122">如果讓遠端監視解決方案繼續在您的 Azure 帳戶中執行，您需支付其執行期間的費用。</span><span class="sxs-lookup"><span data-stu-id="0d39d-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="0d39d-123">如需將遠端監視解決方案執行時的耗用量降低的詳細資訊，請參閱[設定 Azure IoT 套件預先設定的解決方案以供示範][lnk-demo-config]。</span><span class="sxs-lookup"><span data-stu-id="0d39d-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="0d39d-124">使用完畢時，從您的 Azure 帳戶刪除預先設定的解決方案。</span><span class="sxs-lookup"><span data-stu-id="0d39d-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md