> [!div class="op_single_selector"]
> * [<span data-ttu-id="170bb-101">Linux</span><span class="sxs-lookup"><span data-stu-id="170bb-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="170bb-102">Windows</span><span class="sxs-lookup"><span data-stu-id="170bb-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="170bb-103">本文提供 [Hello World 範例程式碼][lnk-helloworld-sample]的詳細逐步解說，來說明 [Azure IoT Edge][lnk-iot-edge] 架構的基本元件。</span><span class="sxs-lookup"><span data-stu-id="170bb-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="170bb-104">此範例使用 Azure IoT Edge，建置每五秒即將 "hello world" 訊息記錄到檔案的簡單閘道。</span><span class="sxs-lookup"><span data-stu-id="170bb-104">The sample uses the Azure IoT Edge to build a simple gateway that logs a "hello world" message to a file every five seconds.</span></span>

<span data-ttu-id="170bb-105">本逐步解說涵蓋下列項目：</span><span class="sxs-lookup"><span data-stu-id="170bb-105">This walkthrough covers:</span></span>

* <span data-ttu-id="170bb-106">**Hello World 範例架構**︰描述 [Azure IoT Edge 架構概念][lnk-edge-concepts]套用到 Hello World 範例的方式，以及元件如何彼此搭配運作。</span><span class="sxs-lookup"><span data-stu-id="170bb-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply to the Hello World sample and how the components fit together.</span></span>
* <span data-ttu-id="170bb-107">**如何建置範例**︰建置範例所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="170bb-107">**How to build the sample**: The steps required to build the sample.</span></span>
* <span data-ttu-id="170bb-108">**如何執行範例**︰執行範例所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="170bb-108">**How to run the sample**: The steps required to run the sample.</span></span> 
* <span data-ttu-id="170bb-109">**典型輸出**：執行範例時所預期的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="170bb-109">**Typical output**: An example of the output to expect when you run the sample.</span></span>
* <span data-ttu-id="170bb-110">**程式碼片段**︰程式碼片段集合，顯示 Hello World 範例如何實作重要 IoT Edge 閘道元件。</span><span class="sxs-lookup"><span data-stu-id="170bb-110">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="170bb-111">Hello World 範例架構</span><span class="sxs-lookup"><span data-stu-id="170bb-111">Hello World sample architecture</span></span>
<span data-ttu-id="170bb-112">Hello World 範例說明上節中所述的概念。</span><span class="sxs-lookup"><span data-stu-id="170bb-112">The Hello World sample illustrates the concepts described in the previous section.</span></span> <span data-ttu-id="170bb-113">Hello World 範例會實作管線由兩個 IoT Edge 模組所構成的 IoT Edge 閘道︰</span><span class="sxs-lookup"><span data-stu-id="170bb-113">The Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="170bb-114">「Hello World」  模組每五秒會建立一則訊息，並將其傳遞到 Logger 模組。</span><span class="sxs-lookup"><span data-stu-id="170bb-114">The *hello world* module creates a message every five seconds and passes it to the logger module.</span></span>
* <span data-ttu-id="170bb-115">「Logger」  模組會將所收到的訊息寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="170bb-115">The *logger* module writes the messages it receives to a file.</span></span>

![使用 Azure IoT Edge 所建置之 Hello World 範例的架構][4]

<span data-ttu-id="170bb-117">如上節所述，Hello World 模組不會每五秒將訊息直接傳遞到 Logger 模組。</span><span class="sxs-lookup"><span data-stu-id="170bb-117">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span></span> <span data-ttu-id="170bb-118">而是每五秒將訊息發佈到訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="170bb-118">Instead, it publishes a message to the broker every five seconds.</span></span>

<span data-ttu-id="170bb-119">Logger 模組會接收來自訊息代理程式的訊息並對其採取動作，以將訊息的內容寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="170bb-119">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span></span>

<span data-ttu-id="170bb-120">Logger 模組只會取用來自訊息代理程式的訊息，永遠不會對訊息代理程式發佈新訊息。</span><span class="sxs-lookup"><span data-stu-id="170bb-120">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span></span>

![訊息代理程式如何在 Azure IoT Edge 的模組之間路由傳送訊息][5]

<span data-ttu-id="170bb-122">上圖顯示 Hello World 範例的架構，以及實作[儲存機制][lnk-iot-edge]中範例不同部分之來源檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="170bb-122">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-iot-edge].</span></span> <span data-ttu-id="170bb-123">自行探索程式碼，或使用下面的程式碼片段作為指南。</span><span class="sxs-lookup"><span data-stu-id="170bb-123">Explore the code on your own, or use the code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md