> [!div class="op_single_selector"]
> * [<span data-ttu-id="7da4a-101">裝置︰Node.js 服務︰Node.js</span><span class="sxs-lookup"><span data-stu-id="7da4a-101">Device: Node.js Service: Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [<span data-ttu-id="7da4a-102">裝置︰Node.js 服務︰C#</span><span class="sxs-lookup"><span data-stu-id="7da4a-102">Device: Node.js Service: C#</span></span>](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [<span data-ttu-id="7da4a-103">裝置︰Java 服務︰Java</span><span class="sxs-lookup"><span data-stu-id="7da4a-103">Device: Java Service: Java</span></span>](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

<span data-ttu-id="7da4a-104">後端應用程式可以使用 Azure IoT 中樞基本類型，例如[裝置兩個][ lnk-devtwin]和[直接方法][lnk-c2dmethod]，tooremotely 啟動及監視裝置管理行動裝置上。</span><span class="sxs-lookup"><span data-stu-id="7da4a-104">Back-end apps can use Azure IoT Hub primitives, such as [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod], tooremotely start and monitor device management actions on devices.</span></span> <span data-ttu-id="7da4a-105">本教學課程會示範如何在後端應用程式和裝置的應用程式可以搭配 tooinitiate 和監視使用 IoT 中樞的遠端裝置重新開機。</span><span class="sxs-lookup"><span data-stu-id="7da4a-105">This tutorial shows you how a back-end app and a device app can work together tooinitiate and monitor a remote device reboot using IoT Hub.</span></span>

<span data-ttu-id="7da4a-106">從 hello 雲端中的後端應用程式使用直接的方法 tooinitiate 裝置管理動作 （例如重新開機，原廠重設和韌體更新）。</span><span class="sxs-lookup"><span data-stu-id="7da4a-106">Use a direct method tooinitiate device management actions (such as reboot, factory reset, and firmware update) from a back-end app in hello cloud.</span></span> <span data-ttu-id="7da4a-107">裝置 hello 負責：</span><span class="sxs-lookup"><span data-stu-id="7da4a-107">hello device is responsible for:</span></span>

* <span data-ttu-id="7da4a-108">處理從 IoT 中樞傳送嗨方法要求。</span><span class="sxs-lookup"><span data-stu-id="7da4a-108">Handling hello method request sent from IoT Hub.</span></span>
* <span data-ttu-id="7da4a-109">初始化 hello 裝置 hello 對應裝置的特定動作。</span><span class="sxs-lookup"><span data-stu-id="7da4a-109">Initiating hello corresponding device-specific action on hello device.</span></span>
* <span data-ttu-id="7da4a-110">提供狀態更新，透過*報告屬性*tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7da4a-110">Providing status updates through *reported properties* tooIoT Hub.</span></span>

<span data-ttu-id="7da4a-111">您可以使用後端應用程式中 hello 雲端 toorun 裝置兩個查詢 tooreport hello 進度您裝置的管理動作。</span><span class="sxs-lookup"><span data-stu-id="7da4a-111">You can use a back-end app in hello cloud toorun device twin queries tooreport on hello progress of your device management actions.</span></span>

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
