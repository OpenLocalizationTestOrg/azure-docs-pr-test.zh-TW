> [!div class="op_single_selector"]
> * [<span data-ttu-id="41173-101">Node.js</span><span class="sxs-lookup"><span data-stu-id="41173-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="41173-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="41173-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="41173-103">C#</span><span class="sxs-lookup"><span data-stu-id="41173-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="41173-104">Java</span><span class="sxs-lookup"><span data-stu-id="41173-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="41173-105">「裝置對應項」是存放裝置狀態資訊 (中繼資料、組態和條件) 的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="41173-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="41173-106">IoT 中樞會為其連線的每個裝置保存裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="41173-106">IoT Hub persists a device twin for each device that connects to it.</span></span>

<span data-ttu-id="41173-107">使用裝置對應項可以：</span><span class="sxs-lookup"><span data-stu-id="41173-107">Use device twins to:</span></span>

* <span data-ttu-id="41173-108">從您的解決方案後端儲存裝置中繼資料。</span><span class="sxs-lookup"><span data-stu-id="41173-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="41173-109">從您的裝置應用程式報告目前狀態資訊，例如可用功能和狀況 (例如，使用的連接方法)。</span><span class="sxs-lookup"><span data-stu-id="41173-109">Report current state information such as available capabilities and conditions (for example, the connectivity method used) from your device app.</span></span>
* <span data-ttu-id="41173-110">同步處理裝置應用程式與後端應用程式之間長時間執行之工作流程的狀態 (例如韌體和組態更新)。</span><span class="sxs-lookup"><span data-stu-id="41173-110">Synchronize the state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="41173-111">查詢裝置中繼資料、組態或狀態。</span><span class="sxs-lookup"><span data-stu-id="41173-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="41173-112">裝置對應項是設計來進行同步處理和查詢裝置組態和條件。</span><span class="sxs-lookup"><span data-stu-id="41173-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="41173-113">如需何時使用裝置對應項的詳細資訊，請參閱[了解裝置對應項][lnk-twins]。</span><span class="sxs-lookup"><span data-stu-id="41173-113">More informations on when to use device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="41173-114">裝置對應項會儲存在 IoT 中樞，並且包含︰</span><span class="sxs-lookup"><span data-stu-id="41173-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="41173-115">標籤，只有解決方案後端可存取裝置中繼資料；</span><span class="sxs-lookup"><span data-stu-id="41173-115">*tags*, device metadata accessible only by the solution back end;</span></span>
* <span data-ttu-id="41173-116">所需屬性，JSON 物件可由解決方案後端修改並且可由裝置應用程式觀察，以及</span><span class="sxs-lookup"><span data-stu-id="41173-116">*desired properties*, JSON objects modifiable by the solution back end and observable by the device app; and</span></span>
* <span data-ttu-id="41173-117">報告屬性，JSON 物件可由裝置應用程式修改並且可由解決方案後端讀取。</span><span class="sxs-lookup"><span data-stu-id="41173-117">*reported properties*, JSON objects modifiable by the device app and readable by the solution back end.</span></span> <span data-ttu-id="41173-118">標籤和屬性不能包含陣列，但物件可以是巢狀的。</span><span class="sxs-lookup"><span data-stu-id="41173-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="41173-119">此外，解決方案後端可以根據上述的所有資料查詢裝置對應項。</span><span class="sxs-lookup"><span data-stu-id="41173-119">Additionally, the solution back end can query device twins based on all the above data.</span></span>
<span data-ttu-id="41173-120">請參閱[了解裝置對應項][lnk-twins]以取得裝置對應項的詳細資訊，以及參閱 [IoT 中樞查詢語言][lnk-query]參考以進行查詢。</span><span class="sxs-lookup"><span data-stu-id="41173-120">Refer to [Understand device twins][lnk-twins] for more information about device twins, and to the [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="41173-121">目前，裝置對應項只能從使用 MQTT 通訊協定連線至 IoT 中樞的裝置存取。</span><span class="sxs-lookup"><span data-stu-id="41173-121">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="41173-122">請參閱 [MQTT 支援][lnk-devguide-mqtt]文章，以取得如何將現有裝置應用程式轉換為使用 MQTT 的指示。</span><span class="sxs-lookup"><span data-stu-id="41173-122">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>

<span data-ttu-id="41173-123">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="41173-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="41173-124">建立後端應用程式，將「標籤」新增至裝置對應項，以及建立模擬裝置應用程式，以裝置對應項上的「報告屬性」來報告其連線通道。</span><span class="sxs-lookup"><span data-stu-id="41173-124">Create a back-end app that adds *tags* to a device twin, and a simulated device app that reports its connectivity channel as a *reported property* on the device twin.</span></span>
* <span data-ttu-id="41173-125">使用先前建立的標籤和屬性上的篩選器，從您的後端應用程式查詢裝置。</span><span class="sxs-lookup"><span data-stu-id="41173-125">Query devices from your back-end app using filters on the tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md