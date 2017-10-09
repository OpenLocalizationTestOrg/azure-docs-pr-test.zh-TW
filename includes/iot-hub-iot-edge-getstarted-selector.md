> [!div class="op_single_selector"]
> * [<span data-ttu-id="de2c1-101">Linux</span><span class="sxs-lookup"><span data-stu-id="de2c1-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="de2c1-102">Windows</span><span class="sxs-lookup"><span data-stu-id="de2c1-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="de2c1-103">本文章提供詳細的逐步解說的 hello [Hello World 範例程式碼][ lnk-helloworld-sample] tooillustrate hello 的基礎元件 hello [Azure IoT 邊緣][lnk-iot-edge]架構。</span><span class="sxs-lookup"><span data-stu-id="de2c1-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="de2c1-104">hello 範例會使用 hello Azure IoT 邊緣 toobuild 記錄"hello world"訊息 tooa 檔每五秒的簡單閘道。</span><span class="sxs-lookup"><span data-stu-id="de2c1-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="de2c1-105">本逐步解說涵蓋下列項目：</span><span class="sxs-lookup"><span data-stu-id="de2c1-105">This walkthrough covers:</span></span>

* <span data-ttu-id="de2c1-106">**Hello World 範例架構**： 描述如何[Azure IoT 邊緣架構概念][ lnk-edge-concepts]套用 toohello Hello World 範例與 hello 元件一起。</span><span class="sxs-lookup"><span data-stu-id="de2c1-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="de2c1-107">**如何 toobuild hello 範例**: hello 步驟需要的 toobuild hello 範例。</span><span class="sxs-lookup"><span data-stu-id="de2c1-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="de2c1-108">**如何 toorun hello 範例**: hello 步驟需要的 toorun hello 範例。</span><span class="sxs-lookup"><span data-stu-id="de2c1-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="de2c1-109">**一般輸出**: hello 的範例輸出 tooexpect，當您執行 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="de2c1-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="de2c1-110">**程式碼片段**： 集合的程式碼片段 tooshow hello Hello World 範例如何實作主要 IoT 邊緣閘道元件。</span><span class="sxs-lookup"><span data-stu-id="de2c1-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="de2c1-111">Hello World 範例架構</span><span class="sxs-lookup"><span data-stu-id="de2c1-111">Hello World sample architecture</span></span>
<span data-ttu-id="de2c1-112">hello Hello World 範例說明 hello 概念 hello 上一節中所述。</span><span class="sxs-lookup"><span data-stu-id="de2c1-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="de2c1-113">hello Hello World 範例會實作兩個 IoT 邊緣模組所組成的管線 IoT 邊緣閘道：</span><span class="sxs-lookup"><span data-stu-id="de2c1-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="de2c1-114">hello *hello world*模組建立每五秒的訊息，並將其傳遞 toohello 記錄器模組。</span><span class="sxs-lookup"><span data-stu-id="de2c1-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="de2c1-115">hello*記錄器*模組寫入 hello 訊息接收 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="de2c1-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![使用 Azure IoT Edge 所建置之 Hello World 範例的架構][4]

<span data-ttu-id="de2c1-117">Hello 上一節所述，模組未通過的 Hello World hello 訊息直接 toohello 記錄器模組每五秒。</span><span class="sxs-lookup"><span data-stu-id="de2c1-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="de2c1-118">相反地，發行訊息 toohello broker 每五秒。</span><span class="sxs-lookup"><span data-stu-id="de2c1-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="de2c1-119">hello 記錄器模組從 hello 代理人收到 hello 訊息，並可運作時，寫入 hello 的 hello 訊息 tooa 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="de2c1-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="de2c1-120">hello 記錄器模組只會消耗 hello broker 的訊息，永遠不會將發佈新訊息 toohello broker。</span><span class="sxs-lookup"><span data-stu-id="de2c1-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Hello broker 將模組中 Azure IoT 邊緣之間的訊息的路由][5]

<span data-ttu-id="de2c1-122">hello 上圖顯示 hello 架構 hello Hello World 範例與 hello 相對路徑 toohello 原始程式檔在 hello 實作不同部分的 hello 範例[儲存機制][lnk-iot-edge]。</span><span class="sxs-lookup"><span data-stu-id="de2c1-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="de2c1-123">自行瀏覽 hello 程式碼，或使用 hello 如下的程式碼片段做為指南。</span><span class="sxs-lookup"><span data-stu-id="de2c1-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md