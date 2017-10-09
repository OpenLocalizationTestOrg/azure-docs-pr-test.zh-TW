## <a name="prerequisites"></a><span data-ttu-id="6de1f-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="6de1f-101">Prerequisites</span></span>

<span data-ttu-id="6de1f-102">toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6de1f-102">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6de1f-103">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6de1f-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6de1f-104">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="6de1f-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="6de1f-105">必要的軟體</span><span class="sxs-lookup"><span data-stu-id="6de1f-105">Required software</span></span>

<span data-ttu-id="6de1f-106">需要 SSH 用戶端上您 tooremotely 存取 hello 命令列 hello 覆盆子 Pi 您桌面的電腦 tooenable。</span><span class="sxs-lookup"><span data-stu-id="6de1f-106">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="6de1f-107">Windows 不包含 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6de1f-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="6de1f-108">我們建議使用 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="6de1f-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="6de1f-109">多數 Linux 散發套件和 Mac OS 包含 hello 命令列 SSH 公用程式。</span><span class="sxs-lookup"><span data-stu-id="6de1f-109">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="6de1f-110">如需詳細資訊，請參閱[使用 Linux 或 Mac OS 的 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)。</span><span class="sxs-lookup"><span data-stu-id="6de1f-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="6de1f-111">必要的硬體</span><span class="sxs-lookup"><span data-stu-id="6de1f-111">Required hardware</span></span>

<span data-ttu-id="6de1f-112">桌上型電腦 tooenable 您 tooconnect 遠端 toohello 命令列上 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="6de1f-112">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="6de1f-113">[適用於 Raspberry Pi 3 的 Microsoft IoT 入門套件][lnk-starter-kits]或對等的元件。</span><span class="sxs-lookup"><span data-stu-id="6de1f-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="6de1f-114">本教學課程使用下列項目從 hello 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="6de1f-114">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="6de1f-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="6de1f-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="6de1f-116">MicroSD 卡 (具有 NOOBS)</span><span class="sxs-lookup"><span data-stu-id="6de1f-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="6de1f-117">USB Mini 連接線</span><span class="sxs-lookup"><span data-stu-id="6de1f-117">A USB Mini cable</span></span>
- <span data-ttu-id="6de1f-118">乙太網路連接線</span><span class="sxs-lookup"><span data-stu-id="6de1f-118">An Ethernet cable</span></span>
- <span data-ttu-id="6de1f-119">BME280 感應器</span><span class="sxs-lookup"><span data-stu-id="6de1f-119">BME280 sensor</span></span>
- <span data-ttu-id="6de1f-120">試驗電路板</span><span class="sxs-lookup"><span data-stu-id="6de1f-120">Breadboard</span></span>
- <span data-ttu-id="6de1f-121">跳線</span><span class="sxs-lookup"><span data-stu-id="6de1f-121">Jumper wires</span></span>
- <span data-ttu-id="6de1f-122">電阻器</span><span class="sxs-lookup"><span data-stu-id="6de1f-122">Resistors</span></span>
- <span data-ttu-id="6de1f-123">LED</span><span class="sxs-lookup"><span data-stu-id="6de1f-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/