## <a name="prerequisites"></a><span data-ttu-id="6f2f0-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="6f2f0-101">Prerequisites</span></span>

<span data-ttu-id="6f2f0-102">若要完成此教學課程，您需要一個有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6f2f0-103">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6f2f0-104">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="6f2f0-105">必要的軟體</span><span class="sxs-lookup"><span data-stu-id="6f2f0-105">Required software</span></span>

<span data-ttu-id="6f2f0-106">您需要透過桌上型電腦上的 SSH 用戶端，才能從遠端存取 Raspberry Pi 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="6f2f0-107">Windows 不包含 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="6f2f0-108">我們建議使用 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="6f2f0-109">大部分的 Linux 散發套件和 Mac OS 都包含命令列 SSH 公用程式。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="6f2f0-110">如需詳細資訊，請參閱[使用 Linux 或 Mac OS 的 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="6f2f0-111">必要的硬體</span><span class="sxs-lookup"><span data-stu-id="6f2f0-111">Required hardware</span></span>

<span data-ttu-id="6f2f0-112">一部桌上型電腦，可讓您從遠端連線到 Raspberry Pi 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-112">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="6f2f0-113">[適用於 Raspberry Pi 3 的 Microsoft IoT 入門套件][lnk-starter-kits]或對等的元件。</span><span class="sxs-lookup"><span data-stu-id="6f2f0-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="6f2f0-114">本教學課程會使用套件中的下列項目：</span><span class="sxs-lookup"><span data-stu-id="6f2f0-114">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="6f2f0-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="6f2f0-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="6f2f0-116">MicroSD 卡 (具有 NOOBS)</span><span class="sxs-lookup"><span data-stu-id="6f2f0-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="6f2f0-117">USB Mini 連接線</span><span class="sxs-lookup"><span data-stu-id="6f2f0-117">A USB Mini cable</span></span>
- <span data-ttu-id="6f2f0-118">乙太網路連接線</span><span class="sxs-lookup"><span data-stu-id="6f2f0-118">An Ethernet cable</span></span>
- <span data-ttu-id="6f2f0-119">BME280 感應器</span><span class="sxs-lookup"><span data-stu-id="6f2f0-119">BME280 sensor</span></span>
- <span data-ttu-id="6f2f0-120">試驗電路板</span><span class="sxs-lookup"><span data-stu-id="6f2f0-120">Breadboard</span></span>
- <span data-ttu-id="6f2f0-121">跳線</span><span class="sxs-lookup"><span data-stu-id="6f2f0-121">Jumper wires</span></span>
- <span data-ttu-id="6f2f0-122">電阻器</span><span class="sxs-lookup"><span data-stu-id="6f2f0-122">Resistors</span></span>
- <span data-ttu-id="6f2f0-123">LED</span><span class="sxs-lookup"><span data-stu-id="6f2f0-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/