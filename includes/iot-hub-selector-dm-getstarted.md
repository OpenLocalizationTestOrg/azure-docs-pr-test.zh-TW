> [!div class="op_single_selector"]
> * [<span data-ttu-id="eedd6-101">裝置︰Node.js 服務︰Node.js</span><span class="sxs-lookup"><span data-stu-id="eedd6-101">Device: Node.js Service: Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [<span data-ttu-id="eedd6-102">裝置︰Node.js 服務︰C#</span><span class="sxs-lookup"><span data-stu-id="eedd6-102">Device: Node.js Service: C#</span></span>](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [<span data-ttu-id="eedd6-103">裝置︰Java 服務︰Java</span><span class="sxs-lookup"><span data-stu-id="eedd6-103">Device: Java Service: Java</span></span>](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

<span data-ttu-id="eedd6-104">後端應用程式可以使用 Azure IoT 中樞基元 (例如[裝置對應項][lnk-devtwin]和[直接方法][lnk-c2dmethod])，從遠端啟動並監視裝置上的裝置管理動作。</span><span class="sxs-lookup"><span data-stu-id="eedd6-104">Back-end apps can use Azure IoT Hub primitives, such as [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod], to remotely start and monitor device management actions on devices.</span></span> <span data-ttu-id="eedd6-105">本教學課程會示範後端應用程式和裝置應用程式如何共同運作，以使用 IoT 中樞初始化和監視遠端裝置重新啟動。</span><span class="sxs-lookup"><span data-stu-id="eedd6-105">This tutorial shows you how a back-end app and a device app can work together to initiate and monitor a remote device reboot using IoT Hub.</span></span>

<span data-ttu-id="eedd6-106">使用直接方法從雲端中的後端應用程式起始裝置管理動作 (例如重新啟動、恢復出廠預設值，以及韌體更新)。</span><span class="sxs-lookup"><span data-stu-id="eedd6-106">Use a direct method to initiate device management actions (such as reboot, factory reset, and firmware update) from a back-end app in the cloud.</span></span> <span data-ttu-id="eedd6-107">該裝置將負責：</span><span class="sxs-lookup"><span data-stu-id="eedd6-107">The device is responsible for:</span></span>

* <span data-ttu-id="eedd6-108">處理從 IoT 中樞傳送的方法要求。</span><span class="sxs-lookup"><span data-stu-id="eedd6-108">Handling the method request sent from IoT Hub.</span></span>
* <span data-ttu-id="eedd6-109">在裝置上初始化相對應的裝置特定動作。</span><span class="sxs-lookup"><span data-stu-id="eedd6-109">Initiating the corresponding device-specific action on the device.</span></span>
* <span data-ttu-id="eedd6-110">透過針對 IoT 中樞的*報告屬性*提供狀態更新。</span><span class="sxs-lookup"><span data-stu-id="eedd6-110">Providing status updates through *reported properties* to IoT Hub.</span></span>

<span data-ttu-id="eedd6-111">您可以在雲端中使用後端 App 來執行裝置對應項查詢，以報告裝置管理動作的進度。</span><span class="sxs-lookup"><span data-stu-id="eedd6-111">You can use a back-end app in the cloud to run device twin queries to report on the progress of your device management actions.</span></span>

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
