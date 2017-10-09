> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d961-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="7d961-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [<span data-ttu-id="7d961-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="7d961-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [<span data-ttu-id="7d961-103">C#</span><span class="sxs-lookup"><span data-stu-id="7d961-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [<span data-ttu-id="7d961-104">Java</span><span class="sxs-lookup"><span data-stu-id="7d961-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

<span data-ttu-id="7d961-105">Azure IoT 中樞是一項完全受管理的服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="7d961-105">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="7d961-106">先前的教學課程 ([開始使用 IoT 中樞]和[傳送雲端到裝置訊息與 IoT 中樞]) 說明 hello 基本裝置到雲端 」 和 「 雲端到裝置訊息功能的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="7d961-106">Previous tutorials ([Get started with IoT Hub] and [Send Cloud-to-Device messages with IoT Hub]) illustrate hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="7d961-107">IoT 中樞也可讓您 hello 能力 tooinvoke 非持續性方法，從 hello 雲端的裝置上。</span><span class="sxs-lookup"><span data-stu-id="7d961-107">IoT Hub also gives you hello ability tooinvoke non-durable methods on devices from hello cloud.</span></span> <span data-ttu-id="7d961-108">直接方法表示要求-回覆互動 HTTP 呼叫成功或失敗 （之後立即使用者指定的逾時），裝置類似 tooan toolet hello 使用者知道的 hello 呼叫 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="7d961-108">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout) toolet hello user know hello status of hello call.</span></span> <span data-ttu-id="7d961-109">[叫用的裝置上直接方法][ lnk-devguide-methods]描述更詳細的直接方法，並提供指引 toouse 時直接方法，而不是雲端到裝置訊息或想要的屬性。</span><span class="sxs-lookup"><span data-stu-id="7d961-109">[Invoke a direct method on a device][lnk-devguide-methods] describes direct methods in more detail and offers guidance about when toouse direct methods rather than cloud-to-device messages or desired properties.</span></span>

<span data-ttu-id="7d961-110">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="7d961-110">This tutorial shows you how to:</span></span>

* <span data-ttu-id="7d961-111">使用 hello Azure 入口網站 toocreate IoT 中樞，並在您的 IoT 中樞中建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="7d961-111">Use hello Azure portal toocreate an IoT hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="7d961-112">建立直接的方法可以呼叫 hello 雲端之模擬的裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d961-112">Create a simulated device app that has a direct method which can be called by hello cloud.</span></span>
* <span data-ttu-id="7d961-113">建立主控台應用程式會呼叫 hello 模擬的裝置的應用程式透過您的 IoT 中樞中的直接的方法。</span><span class="sxs-lookup"><span data-stu-id="7d961-113">Create a console app that calls a direct method in hello simulated device app through your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="7d961-114">在這個階段，直接的方法都是只有裝置上支援的 tooIoT 集線器使用連線的 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7d961-114">At this time, direct methods are only supported on devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="7d961-115">請參閱 toohello [MQTT 支援][ lnk-devguide-mqtt]文章的指示現有裝置的應用程式 toouse tooconvert MQTT。</span><span class="sxs-lookup"><span data-stu-id="7d961-115">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[傳送雲端到裝置訊息與 IoT 中樞]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[開始使用 IoT 中樞]: ../articles/iot-hub/iot-hub-node-node-getstarted.md