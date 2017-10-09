## <a name="overview"></a><span data-ttu-id="58fe3-101">概觀</span><span class="sxs-lookup"><span data-stu-id="58fe3-101">Overview</span></span>

<span data-ttu-id="58fe3-102">在本教學課程中，您完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="58fe3-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="58fe3-103">部署 hello 遠端監視預先設定的解決方案 tooyour Azure 訂用帳戶的執行個體。</span><span class="sxs-lookup"><span data-stu-id="58fe3-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="58fe3-104">這個步驟會自動部署並設定多個 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="58fe3-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="58fe3-105">設定您的裝置 toocommunicate 與您的電腦 hello 遠端監視解決方案。</span><span class="sxs-lookup"><span data-stu-id="58fe3-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="58fe3-106">更新 hello 範例裝置的程式碼 tooconnect toohello 遠端監視解決方案，並傳送嗨方案儀表板，您可以檢視的模擬的遙測。</span><span class="sxs-lookup"><span data-stu-id="58fe3-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58fe3-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="58fe3-107">Prerequisites</span></span>

<span data-ttu-id="58fe3-108">toocomplete 本教學課程中，您需要使用中的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="58fe3-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="58fe3-109">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="58fe3-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="58fe3-110">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="58fe3-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="58fe3-111">必要的軟體</span><span class="sxs-lookup"><span data-stu-id="58fe3-111">Required software</span></span>

<span data-ttu-id="58fe3-112">需要 SSH 用戶端上您 tooremotely 存取 hello 命令列 hello 覆盆子 Pi 您桌面的電腦 tooenable。</span><span class="sxs-lookup"><span data-stu-id="58fe3-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="58fe3-113">Windows 不包含 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="58fe3-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="58fe3-114">我們建議使用 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="58fe3-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="58fe3-115">多數 Linux 散發套件和 Mac OS 包含 hello 命令列 SSH 公用程式。</span><span class="sxs-lookup"><span data-stu-id="58fe3-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="58fe3-116">如需詳細資訊，請參閱[使用 Linux 或 Mac OS 的 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)。</span><span class="sxs-lookup"><span data-stu-id="58fe3-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="58fe3-117">必要的硬體</span><span class="sxs-lookup"><span data-stu-id="58fe3-117">Required hardware</span></span>

<span data-ttu-id="58fe3-118">桌上型電腦 tooenable 您 tooconnect 遠端 toohello 命令列上 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="58fe3-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="58fe3-119">[適用於 Raspberry Pi 3 的 Microsoft IoT 入門套件][lnk-starter-kits]或對等的元件。</span><span class="sxs-lookup"><span data-stu-id="58fe3-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="58fe3-120">本教學課程使用下列項目從 hello 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="58fe3-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="58fe3-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="58fe3-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="58fe3-122">MicroSD 卡 (具有 NOOBS)</span><span class="sxs-lookup"><span data-stu-id="58fe3-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="58fe3-123">USB Mini 連接線</span><span class="sxs-lookup"><span data-stu-id="58fe3-123">A USB Mini cable</span></span>
- <span data-ttu-id="58fe3-124">乙太網路連接線</span><span class="sxs-lookup"><span data-stu-id="58fe3-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/