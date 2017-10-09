> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4fcc-101">Linux</span><span class="sxs-lookup"><span data-stu-id="d4fcc-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [<span data-ttu-id="d4fcc-102">Windows</span><span class="sxs-lookup"><span data-stu-id="d4fcc-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

<span data-ttu-id="d4fcc-103">這個逐步解說中的 hello[模擬裝置雲端上傳範例]為您示範如何 toouse [Azure IoT 邊緣][ lnk-sdk]從模擬 toosend 裝置到雲端遙測 tooIoT 中樞裝置。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-103">This walkthrough of hello [Simulated Device Cloud Upload sample] shows you how toouse [Azure IoT Edge][lnk-sdk] toosend device-to-cloud telemetry tooIoT Hub from simulated devices.</span></span>

<span data-ttu-id="d4fcc-104">本逐步解說涵蓋下列項目：</span><span class="sxs-lookup"><span data-stu-id="d4fcc-104">This walkthrough covers:</span></span>

* <span data-ttu-id="d4fcc-105">**架構**: hello 的架構資訊[模擬裝置雲端上傳範例]。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-105">**Architecture**: architectural information about hello [Simulated Device Cloud Upload sample].</span></span>
* <span data-ttu-id="d4fcc-106">**建置並執行**: hello 步驟需要的 toobuild 和執行的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-106">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="d4fcc-107">架構</span><span class="sxs-lookup"><span data-stu-id="d4fcc-107">Architecture</span></span>

<span data-ttu-id="d4fcc-108">hello[模擬裝置雲端上傳範例]顯示 toocreate 傳送遙測資料閘道如何模擬裝置 tooan IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-108">hello [Simulated Device Cloud Upload sample] shows how toocreate a gateway that sends telemetry from simulated devices tooan IoT hub.</span></span> <span data-ttu-id="d4fcc-109">裝置可能無法 tooconnect 直接 tooIoT 中樞因為 hello 裝置：</span><span class="sxs-lookup"><span data-stu-id="d4fcc-109">A device may not be able tooconnect directly tooIoT Hub because hello device:</span></span>

* <span data-ttu-id="d4fcc-110">未使用 IoT 中樞所了解的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-110">Does not use a communications protocol understood by IoT Hub.</span></span>
* <span data-ttu-id="d4fcc-111">不是十分聰明 tooremember hello 分派識別 tooit IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-111">Is not smart enough tooremember hello identity assigned tooit by IoT Hub.</span></span>

<span data-ttu-id="d4fcc-112">IoT 邊緣閘道可以解決這些問題中 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="d4fcc-112">An IoT Edge gateway can solve these problems in hello following ways:</span></span>

* <span data-ttu-id="d4fcc-113">hello 閘道了解 hello hello 裝置使用的通訊協定、 收到 hello 裝置從裝置到雲端遙測和轉送這些訊息 tooIoT 集線器使用了解的 hello IoT 中樞通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-113">hello gateway understands hello protocol used by hello device, receives device-to-cloud telemetry from hello device, and forwards those messages tooIoT Hub using a protocol understood by hello IoT hub.</span></span>

* <span data-ttu-id="d4fcc-114">hello 閘道對應 IoT 中樞識別 toodevices，並會作為 proxy，當裝置傳送訊息 tooIoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-114">hello gateway maps IoT Hub identities toodevices and acts as a proxy when a device sends messages tooIoT Hub.</span></span>

<span data-ttu-id="d4fcc-115">hello 下列圖表顯示 hello hello 範例的主要元件，包括 hello IoT 邊緣模組：</span><span class="sxs-lookup"><span data-stu-id="d4fcc-115">hello following diagram shows hello main components of hello sample, including hello IoT Edge modules:</span></span>

![][1]

<span data-ttu-id="d4fcc-116">hello 模組不會將訊息直接 tooeach 其他。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-116">hello modules do not pass messages directly tooeach other.</span></span> <span data-ttu-id="d4fcc-117">hello 模組發佈訊息 tooan 內部 broker 傳送 hello 訊息 toohello 其他模組使用的訂用帳戶的機制。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-117">hello modules publish messages tooan internal broker that delivers hello messages toohello other modules using a subscription mechanism.</span></span> <span data-ttu-id="d4fcc-118">如需詳細資訊，請參閱[開始使用 Azure IoT Edge][lnk-gw-getstarted]。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-118">For more information, see [Get started with Azure IoT Edge][lnk-gw-getstarted].</span></span>

### <a name="protocol-ingestion-module"></a><span data-ttu-id="d4fcc-119">通訊協定擷取模組</span><span class="sxs-lookup"><span data-stu-id="d4fcc-119">Protocol ingestion module</span></span>

<span data-ttu-id="d4fcc-120">此模組為起點來接收資料，並從裝置透過 hello 閘道，並置於 hello 雲端 hello。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-120">This module is hello starting point for receiving data from devices, through hello gateway, and into hello cloud.</span></span> <span data-ttu-id="d4fcc-121">在 hello 模組 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="d4fcc-121">In hello sample, hello module:</span></span>

1. <span data-ttu-id="d4fcc-122">建立模擬溫度資料。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-122">Creates simulated temperature data.</span></span> <span data-ttu-id="d4fcc-123">如果您使用實體裝置，hello 模組會讀取資料，從這些實體裝置。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-123">If you use physical devices, hello module reads data from those physical devices.</span></span>
1. <span data-ttu-id="d4fcc-124">建立訊息。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-124">Creates a message.</span></span>
1. <span data-ttu-id="d4fcc-125">模擬的 hello 溫度資料放入 hello 訊息內容。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-125">Places hello simulated temperature data into hello message content.</span></span>
1. <span data-ttu-id="d4fcc-126">加入具有假的 MAC 位址 toohello 訊息的屬性。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-126">Adds a property with a fake MAC address toohello message.</span></span>
1. <span data-ttu-id="d4fcc-127">讓 hello 訊息可用 toohello 下一個模組中的 hello 鏈結。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-127">Makes hello message available toohello next module in hello chain.</span></span>

<span data-ttu-id="d4fcc-128">呼叫 hello 模組**通訊協定 X 擷取**hello 在上圖中稱為**模擬的裝置**hello 原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-128">hello module called **Protocol X ingestion** in hello previous diagram is called **Simulated device** in hello source code.</span></span>

### <a name="mac-lt-gt-iot-hub-id-module"></a><span data-ttu-id="d4fcc-129">MAC &lt;-&gt; IoT 中樞識別碼模組</span><span class="sxs-lookup"><span data-stu-id="d4fcc-129">MAC &lt;-&gt; IoT Hub ID module</span></span>

<span data-ttu-id="d4fcc-130">此模組會掃描具有 Mac 位址屬性的訊息。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-130">This module scans for messages that have a Mac address property.</span></span> <span data-ttu-id="d4fcc-131">在 hello 範例中，hello 通訊協定擷取模組會將 hello MAC 位址屬性。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-131">In hello sample, hello protocol ingestion module adds hello MAC address property.</span></span> <span data-ttu-id="d4fcc-132">如果 hello 模組發現這類屬性，就會加入 IoT 中樞裝置金鑰 toohello 訊息的另一個屬性。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-132">If hello module finds such a property, it adds another property with an IoT Hub device key toohello message.</span></span> <span data-ttu-id="d4fcc-133">hello 模組然後讓 hello 鏈結中的 hello 訊息可用 toohello 下一個模組。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-133">hello module then makes hello message available toohello next module in hello chain.</span></span>

<span data-ttu-id="d4fcc-134">hello 開發人員設定 MAC 位址與 IoT 中樞識別 tooassociate hello 模擬裝置與 IoT 中樞裝置身分識別之間的對應。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-134">hello developer sets up a mapping between MAC addresses and IoT Hub identities tooassociate hello simulated devices with IoT Hub device identities.</span></span> <span data-ttu-id="d4fcc-135">hello 開發人員 hello 模組組態的一部分，請以手動方式加入 hello 對應。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-135">hello developer adds hello mapping manually as part of hello module configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="d4fcc-136">此範例使用 MAC 位址作為唯一裝置識別碼，並將它與 IoT 中樞裝置身分識別相互關聯。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-136">This sample uses a MAC address as a unique device identifier and correlates it with an IoT Hub device identity.</span></span> <span data-ttu-id="d4fcc-137">不過，您可以撰寫使用不同唯一識別碼的專屬模組。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-137">However, you can write your own module that uses a different unique identifier.</span></span> <span data-ttu-id="d4fcc-138">例如，您的裝置可能會有唯一的數列數字或 hello 遙測資料可能包含重複的內嵌的裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-138">For example, your devices may have unique serial numbers or hello telemetry data may include a unique embedded device name.</span></span>

### <a name="iot-hub-communication-module"></a><span data-ttu-id="d4fcc-139">IoT 中樞通訊模組</span><span class="sxs-lookup"><span data-stu-id="d4fcc-139">IoT Hub communication module</span></span>

<span data-ttu-id="d4fcc-140">此模組會採用與 IoT 中樞的訊息已指派 hello 前一個模組的裝置屬性。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-140">This module takes messages with an IoT Hub device key property that was assigned by hello previous module.</span></span> <span data-ttu-id="d4fcc-141">hello 模組會傳送 hello 訊息內容 tooIoT 集線器使用 hello HTTP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-141">hello module sends hello message content tooIoT Hub using hello HTTP protocol.</span></span> <span data-ttu-id="d4fcc-142">HTTP 是 hello 的了解三種通訊協定的 IoT 中樞的其中一個。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-142">HTTP is one of hello three protocols understood by IoT Hub.</span></span>

<span data-ttu-id="d4fcc-143">而不是開啟的每個模擬裝置的連線，此模組會從 hello 閘道 toohello IoT 中樞開啟單一 HTTP 連線。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-143">Instead of opening a connection for each simulated device, this module opens a single HTTP connection from hello gateway toohello IoT hub.</span></span> <span data-ttu-id="d4fcc-144">hello 模組然後信號分離透過該連線的所有 hello 模擬裝置的連線。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-144">hello module then multiplexes connections from all hello simulated devices over that connection.</span></span> <span data-ttu-id="d4fcc-145">這個方法可讓單一閘道 tooconnect 許多更多裝置。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-145">This approach enables a single gateway tooconnect many more devices.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="d4fcc-146">開始之前</span><span class="sxs-lookup"><span data-stu-id="d4fcc-146">Before you get started</span></span>

<span data-ttu-id="d4fcc-147">開始之前，您必須：</span><span class="sxs-lookup"><span data-stu-id="d4fcc-147">Before you get started, you must:</span></span>

* <span data-ttu-id="d4fcc-148">[建立 IoT 中樞][ lnk-create-hub]在您 Azure 訂用帳戶，您需要集線器 toocomplete hello 名稱本逐步解說。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-148">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="d4fcc-149">如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-149">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="d4fcc-150">加入兩個裝置 tooyour IoT 中樞，並記下其識別碼及裝置機碼。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-150">Add two devices tooyour IoT hub and make a note of their ids and device keys.</span></span> <span data-ttu-id="d4fcc-151">您可以使用 hello[裝置總管][ lnk-device-explorer]或[iot 中樞總管][ lnk-iothub-explorer]工具 tooadd hello 中建立您的裝置 toohello IoT 中樞上一個步驟，並擷取其索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d4fcc-151">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool tooadd your devices toohello IoT hub you created in hello previous step and retrieve their keys.</span></span>

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[模擬裝置雲端上傳範例]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md