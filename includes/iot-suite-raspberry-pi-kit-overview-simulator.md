## <a name="overview"></a><span data-ttu-id="b8ae5-101">概觀</span><span class="sxs-lookup"><span data-stu-id="b8ae5-101">Overview</span></span>

<span data-ttu-id="b8ae5-102">在本教學課程中，您會完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b8ae5-102">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="b8ae5-103">將遠端監視預先設定解決方案的執行個體部署至您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-103">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="b8ae5-104">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="b8ae5-105">設定您的裝置，以便與您的電腦和遠端監視解決方案進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-105">Set up your device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="b8ae5-106">更新範例裝置程式碼以連線到遠端監視解決方案，並傳送您可以在解決方案儀表板上檢視的模擬遙測。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-106">Update the sample device code to connect to the remote monitoring solution, and send simulated telemetry that you can view on the solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8ae5-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="b8ae5-107">Prerequisites</span></span>

<span data-ttu-id="b8ae5-108">若要完成此教學課程，您需要一個有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-108">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ae5-109">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b8ae5-110">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="b8ae5-111">必要的軟體</span><span class="sxs-lookup"><span data-stu-id="b8ae5-111">Required software</span></span>

<span data-ttu-id="b8ae5-112">您需要透過桌上型電腦上的 SSH 用戶端，才能從遠端存取 Raspberry Pi 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-112">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="b8ae5-113">Windows 不包含 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="b8ae5-114">我們建議使用 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="b8ae5-115">大部分的 Linux 散發套件和 Mac OS 都包含命令列 SSH 公用程式。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-115">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="b8ae5-116">如需詳細資訊，請參閱[使用 Linux 或 Mac OS 的 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="b8ae5-117">必要的硬體</span><span class="sxs-lookup"><span data-stu-id="b8ae5-117">Required hardware</span></span>

<span data-ttu-id="b8ae5-118">一部桌上型電腦，可讓您從遠端連線到 Raspberry Pi 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-118">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="b8ae5-119">[適用於 Raspberry Pi 3 的 Microsoft IoT 入門套件][lnk-starter-kits]或對等的元件。</span><span class="sxs-lookup"><span data-stu-id="b8ae5-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="b8ae5-120">本教學課程會使用套件中的下列項目：</span><span class="sxs-lookup"><span data-stu-id="b8ae5-120">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="b8ae5-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="b8ae5-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="b8ae5-122">MicroSD 卡 (具有 NOOBS)</span><span class="sxs-lookup"><span data-stu-id="b8ae5-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="b8ae5-123">USB Mini 連接線</span><span class="sxs-lookup"><span data-stu-id="b8ae5-123">A USB Mini cable</span></span>
- <span data-ttu-id="b8ae5-124">乙太網路連接線</span><span class="sxs-lookup"><span data-stu-id="b8ae5-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/