> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e865-101">Linux</span><span class="sxs-lookup"><span data-stu-id="5e865-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [<span data-ttu-id="5e865-102">Windows</span><span class="sxs-lookup"><span data-stu-id="5e865-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

<span data-ttu-id="5e865-103">[Simulated Device Cloud Upload 範例]的這個逐步解說示範如何使用 [Azure IoT Edge][lnk-sdk]，將裝置到雲端遙測從模擬裝置傳送到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5e865-103">This walkthrough of the [Simulated Device Cloud Upload sample] shows you how to use [Azure IoT Edge][lnk-sdk] to send device-to-cloud telemetry to IoT Hub from simulated devices.</span></span>

<span data-ttu-id="5e865-104">本逐步解說涵蓋下列項目：</span><span class="sxs-lookup"><span data-stu-id="5e865-104">This walkthrough covers:</span></span>

* <span data-ttu-id="5e865-105">**架構**：[Simulated Device Cloud Upload 範例]的架構資訊。</span><span class="sxs-lookup"><span data-stu-id="5e865-105">**Architecture**: architectural information about the [Simulated Device Cloud Upload sample].</span></span>
* <span data-ttu-id="5e865-106">**建置和執行**︰建置和執行範例所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="5e865-106">**Build and run**: the steps required to build and run the sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="5e865-107">架構</span><span class="sxs-lookup"><span data-stu-id="5e865-107">Architecture</span></span>

<span data-ttu-id="5e865-108">[Simulated Device Cloud Upload 範例]示範如何建立閘道，以將遙測從模擬裝置傳送到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5e865-108">The [Simulated Device Cloud Upload sample] shows how to create a gateway that sends telemetry from simulated devices to an IoT hub.</span></span> <span data-ttu-id="5e865-109">裝置可能無法直接連線到 IoT 中樞的原因如下：</span><span class="sxs-lookup"><span data-stu-id="5e865-109">A device may not be able to connect directly to IoT Hub because the device:</span></span>

* <span data-ttu-id="5e865-110">未使用 IoT 中樞所了解的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="5e865-110">Does not use a communications protocol understood by IoT Hub.</span></span>
* <span data-ttu-id="5e865-111">不夠聰明，無法記住 IoT 中樞指派給它的身分識別。</span><span class="sxs-lookup"><span data-stu-id="5e865-111">Is not smart enough to remember the identity assigned to it by IoT Hub.</span></span>

<span data-ttu-id="5e865-112">IoT Edge 閘道可以下列方式解決這些問題：</span><span class="sxs-lookup"><span data-stu-id="5e865-112">An IoT Edge gateway can solve these problems in the following ways:</span></span>

* <span data-ttu-id="5e865-113">閘道了解裝置所使用的通訊協定、從裝置接收裝置到雲端遙測，並使用 IoT 中樞所了解的通訊協定將這些訊息轉送到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5e865-113">The gateway understands the protocol used by the device, receives device-to-cloud telemetry from the device, and forwards those messages to IoT Hub using a protocol understood by the IoT hub.</span></span>

* <span data-ttu-id="5e865-114">閘道將 IoT 中樞身分識別對應到裝置，並且會在裝置將訊息傳送到 IoT 中樞時作為 proxy。</span><span class="sxs-lookup"><span data-stu-id="5e865-114">The gateway maps IoT Hub identities to devices and acts as a proxy when a device sends messages to IoT Hub.</span></span>

<span data-ttu-id="5e865-115">下圖顯示範例的主要元件 (包含 IoT Edge 模組)︰</span><span class="sxs-lookup"><span data-stu-id="5e865-115">The following diagram shows the main components of the sample, including the IoT Edge modules:</span></span>

![][1]

<span data-ttu-id="5e865-116">模組不會彼此直接傳遞訊息。</span><span class="sxs-lookup"><span data-stu-id="5e865-116">The modules do not pass messages directly to each other.</span></span> <span data-ttu-id="5e865-117">模組會將訊息發佈到內部訊息代理程式，而內部代理程式會使用訂用帳戶機制將訊息傳遞到其他模組。</span><span class="sxs-lookup"><span data-stu-id="5e865-117">The modules publish messages to an internal broker that delivers the messages to the other modules using a subscription mechanism.</span></span> <span data-ttu-id="5e865-118">如需詳細資訊，請參閱[開始使用 Azure IoT Edge][lnk-gw-getstarted]。</span><span class="sxs-lookup"><span data-stu-id="5e865-118">For more information, see [Get started with Azure IoT Edge][lnk-gw-getstarted].</span></span>

### <a name="protocol-ingestion-module"></a><span data-ttu-id="5e865-119">通訊協定擷取模組</span><span class="sxs-lookup"><span data-stu-id="5e865-119">Protocol ingestion module</span></span>

<span data-ttu-id="5e865-120">此模組是一個起點，能透過閘道從裝置取得資料，以及將資料傳遞到雲端。</span><span class="sxs-lookup"><span data-stu-id="5e865-120">This module is the starting point for receiving data from devices, through the gateway, and into the cloud.</span></span> <span data-ttu-id="5e865-121">在範例中，模組會：</span><span class="sxs-lookup"><span data-stu-id="5e865-121">In the sample, the module:</span></span>

1. <span data-ttu-id="5e865-122">建立模擬溫度資料。</span><span class="sxs-lookup"><span data-stu-id="5e865-122">Creates simulated temperature data.</span></span> <span data-ttu-id="5e865-123">如果您是使用實際裝置，此模組會讀取這些裝置中的資料。</span><span class="sxs-lookup"><span data-stu-id="5e865-123">If you use physical devices, the module reads data from those physical devices.</span></span>
1. <span data-ttu-id="5e865-124">建立訊息。</span><span class="sxs-lookup"><span data-stu-id="5e865-124">Creates a message.</span></span>
1. <span data-ttu-id="5e865-125">將模擬溫度資料放到訊息內容。</span><span class="sxs-lookup"><span data-stu-id="5e865-125">Places the simulated temperature data into the message content.</span></span>
1. <span data-ttu-id="5e865-126">將包含假 MAC 位址的屬性新增至訊息。</span><span class="sxs-lookup"><span data-stu-id="5e865-126">Adds a property with a fake MAC address to the message.</span></span>
1. <span data-ttu-id="5e865-127">讓訊息可供鏈結中的下一個模組使用。</span><span class="sxs-lookup"><span data-stu-id="5e865-127">Makes the message available to the next module in the chain.</span></span>

<span data-ttu-id="5e865-128">在原始程式碼中，上圖中的**通訊協定 X 擷取**模組稱為**模擬裝置**。</span><span class="sxs-lookup"><span data-stu-id="5e865-128">The module called **Protocol X ingestion** in the previous diagram is called **Simulated device** in the source code.</span></span>

### <a name="mac-lt-gt-iot-hub-id-module"></a><span data-ttu-id="5e865-129">MAC &lt;-&gt; IoT 中樞識別碼模組</span><span class="sxs-lookup"><span data-stu-id="5e865-129">MAC &lt;-&gt; IoT Hub ID module</span></span>

<span data-ttu-id="5e865-130">此模組會掃描具有 Mac 位址屬性的訊息。</span><span class="sxs-lookup"><span data-stu-id="5e865-130">This module scans for messages that have a Mac address property.</span></span> <span data-ttu-id="5e865-131">在範例中，通訊協定擷取模組會新增 MAC 位址屬性。</span><span class="sxs-lookup"><span data-stu-id="5e865-131">In the sample, the protocol ingestion module adds the MAC address property.</span></span> <span data-ttu-id="5e865-132">如果模組發現這類屬性，就會將包含 IoT 中樞裝置索引鍵的另一個屬性新增到訊息。</span><span class="sxs-lookup"><span data-stu-id="5e865-132">If the module finds such a property, it adds another property with an IoT Hub device key to the message.</span></span> <span data-ttu-id="5e865-133">接著，模組會讓訊息可供鏈結中的下一個模組使用。</span><span class="sxs-lookup"><span data-stu-id="5e865-133">The module then makes the message available to the next module in the chain.</span></span>

<span data-ttu-id="5e865-134">開發人員會設定 MAC 位址與 IoT 中樞身分識別之間的對應，將模擬的裝置與 IoT 中樞裝置身分識別建立關聯。</span><span class="sxs-lookup"><span data-stu-id="5e865-134">The developer sets up a mapping between MAC addresses and IoT Hub identities to associate the simulated devices with IoT Hub device identities.</span></span> <span data-ttu-id="5e865-135">開發人員會以手動新增對應，作為模組設定的一部分。</span><span class="sxs-lookup"><span data-stu-id="5e865-135">The developer adds the mapping manually as part of the module configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="5e865-136">此範例使用 MAC 位址作為唯一裝置識別碼，並將它與 IoT 中樞裝置身分識別相互關聯。</span><span class="sxs-lookup"><span data-stu-id="5e865-136">This sample uses a MAC address as a unique device identifier and correlates it with an IoT Hub device identity.</span></span> <span data-ttu-id="5e865-137">不過，您可以撰寫使用不同唯一識別碼的專屬模組。</span><span class="sxs-lookup"><span data-stu-id="5e865-137">However, you can write your own module that uses a different unique identifier.</span></span> <span data-ttu-id="5e865-138">例如，您的裝置可能會有唯一的序號，或是遙測資料可能包含唯一的內嵌裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="5e865-138">For example, your devices may have unique serial numbers or the telemetry data may include a unique embedded device name.</span></span>

### <a name="iot-hub-communication-module"></a><span data-ttu-id="5e865-139">IoT 中樞通訊模組</span><span class="sxs-lookup"><span data-stu-id="5e865-139">IoT Hub communication module</span></span>

<span data-ttu-id="5e865-140">此模組所採用的訊息包含 IoT 中樞裝置索引鍵屬性，已由前一個模組指定。</span><span class="sxs-lookup"><span data-stu-id="5e865-140">This module takes messages with an IoT Hub device key property that was assigned by the previous module.</span></span> <span data-ttu-id="5e865-141">此模組會使用 HTTP 通訊協定，將訊息內容傳送到 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="5e865-141">The module sends the message content to IoT Hub using the HTTP protocol.</span></span> <span data-ttu-id="5e865-142">HTTP 是 IoT 中樞所了解的三種通訊協定中的其中一種。</span><span class="sxs-lookup"><span data-stu-id="5e865-142">HTTP is one of the three protocols understood by IoT Hub.</span></span>

<span data-ttu-id="5e865-143">此模組不會開啟每個模擬裝置的連線，而是會開啟從閘道至 IoT 中樞的單一 HTTP 連線。</span><span class="sxs-lookup"><span data-stu-id="5e865-143">Instead of opening a connection for each simulated device, this module opens a single HTTP connection from the gateway to the IoT hub.</span></span> <span data-ttu-id="5e865-144">接著，模組會透過該連線，從所有的模擬裝置進行多工連線。</span><span class="sxs-lookup"><span data-stu-id="5e865-144">The module then multiplexes connections from all the simulated devices over that connection.</span></span> <span data-ttu-id="5e865-145">這個方法可讓單一閘道連線許多其他裝置。</span><span class="sxs-lookup"><span data-stu-id="5e865-145">This approach enables a single gateway to connect many more devices.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="5e865-146">開始之前</span><span class="sxs-lookup"><span data-stu-id="5e865-146">Before you get started</span></span>

<span data-ttu-id="5e865-147">開始之前，您必須：</span><span class="sxs-lookup"><span data-stu-id="5e865-147">Before you get started, you must:</span></span>

* <span data-ttu-id="5e865-148">於 Azure 訂用帳戶中[建立 IoT 中樞][lnk-create-hub]時，您需要中樞名稱才能完成此逐步解說。</span><span class="sxs-lookup"><span data-stu-id="5e865-148">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need the name of your hub to complete this walkthrough.</span></span> <span data-ttu-id="5e865-149">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="5e865-149">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="5e865-150">將兩個裝置加入 IoT 中樞中，並記下其識別碼和裝置金鑰。</span><span class="sxs-lookup"><span data-stu-id="5e865-150">Add two devices to your IoT hub and make a note of their ids and device keys.</span></span> <span data-ttu-id="5e865-151">您可以使用[裝置總管][lnk-device-explorer]或 [iothub-explorer][lnk-iothub-explorer] 工具，將您的裝置新增到在上一個步驟中建立的 IoT 中樞並擷取其金鑰。</span><span class="sxs-lookup"><span data-stu-id="5e865-151">You can use the [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool to add your devices to the IoT hub you created in the previous step and retrieve their keys.</span></span>

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
<span data-ttu-id="5e865-152">[Simulated Device Cloud Upload 範例]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md</span><span class="sxs-lookup"><span data-stu-id="5e865-152">[Simulated Device Cloud Upload sample]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md</span></span>
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md