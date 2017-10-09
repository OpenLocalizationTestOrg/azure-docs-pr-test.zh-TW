> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4e44-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="a4e44-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="a4e44-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="a4e44-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="a4e44-103">C#</span><span class="sxs-lookup"><span data-stu-id="a4e44-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="a4e44-104">Java</span><span class="sxs-lookup"><span data-stu-id="a4e44-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="a4e44-105">「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="a4e44-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="a4e44-106">IoT 中樞保存每個裝置連接 tooit 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="a4e44-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="a4e44-107">使用裝置對應項可以：</span><span class="sxs-lookup"><span data-stu-id="a4e44-107">Use device twins to:</span></span>

* <span data-ttu-id="a4e44-108">從您的解決方案後端儲存裝置中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a4e44-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="a4e44-109">報告目前的狀態資訊，例如可用的功能和條件 （例如，hello 連線使用方式），從您的裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="a4e44-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="a4e44-110">同步處理長時間執行工作流程 （例如韌體和組態更新） 裝置的應用程式與後端應用程式之間的 hello 的狀態。</span><span class="sxs-lookup"><span data-stu-id="a4e44-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="a4e44-111">查詢裝置中繼資料、組態或狀態。</span><span class="sxs-lookup"><span data-stu-id="a4e44-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="a4e44-112">裝置對應項是設計來進行同步處理和查詢裝置組態和條件。</span><span class="sxs-lookup"><span data-stu-id="a4e44-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="a4e44-113">有關在中找到 toouse 裝置雙[了解裝置雙][lnk-twins]。</span><span class="sxs-lookup"><span data-stu-id="a4e44-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="a4e44-114">裝置對應項會儲存在 IoT 中樞，並且包含︰</span><span class="sxs-lookup"><span data-stu-id="a4e44-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="a4e44-115">*標記*，只能由 hello 方案後端; 存取裝置中繼資料</span><span class="sxs-lookup"><span data-stu-id="a4e44-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="a4e44-116">*所需屬性*，JSON 物件的可修改由 hello 解決方案回結束作業，並觀察 hello 裝置的應用程式; 以及</span><span class="sxs-lookup"><span data-stu-id="a4e44-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="a4e44-117">*報告內容*，hello 裝置應用程式的可修改、 可讀性更高的 hello 方案後端的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="a4e44-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="a4e44-118">標籤和屬性不能包含陣列，但物件可以是巢狀的。</span><span class="sxs-lookup"><span data-stu-id="a4e44-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="a4e44-119">此外，hello 方案後端可以查詢裝置雙根據所有 hello 上述資料。</span><span class="sxs-lookup"><span data-stu-id="a4e44-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="a4e44-120">請參閱太[了解裝置雙][ lnk-twins]如需有關裝置雙和 toohello [IoT 中樞的查詢語言][ lnk-query]參考用於查詢。</span><span class="sxs-lookup"><span data-stu-id="a4e44-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="a4e44-121">此時，裝置雙都只連接 tooIoT 中樞的裝置可以存取使用 hello MQTT 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a4e44-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="a4e44-122">請參閱 toohello [MQTT 支援][ lnk-devguide-mqtt]文章的指示現有裝置的應用程式 toouse tooconvert MQTT。</span><span class="sxs-lookup"><span data-stu-id="a4e44-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="a4e44-123">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="a4e44-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a4e44-124">建立後端應用程式，將它新增*標記*tooa 裝置的兩個，並報告其連線的模擬的裝置應用程式通道為*報告屬性*上 hello 裝置兩個。</span><span class="sxs-lookup"><span data-stu-id="a4e44-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="a4e44-125">查詢從 hello 標記與先前建立的屬性上使用篩選器後端應用程式的裝置。</span><span class="sxs-lookup"><span data-stu-id="a4e44-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md