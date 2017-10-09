## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="6f5a8-101">準備您的 Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="6f5a8-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="6f5a8-102">安裝 Raspbian</span><span class="sxs-lookup"><span data-stu-id="6f5a8-102">Install Raspbian</span></span>

<span data-ttu-id="6f5a8-103">如果這是 hello 用覆盆子 Pi 的第一次，您會需要 tooinstall hello Raspbian 使用作業系統 NOOBS hello 套件中包含的 hello SD 卡上。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="6f5a8-104">hello[覆盆子 Pi 軟體指南][ lnk-install-raspbian]描述如何 tooinstall 覆盆子 Pi 上的作業系統。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="6f5a8-105">本教學課程假設您已安裝 hello Raspbian 作業系統覆盆子 pi。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="6f5a8-106">包含在 hello hello sd 記憶卡[覆盆子 Pi 3 的 Microsoft Azure IoT 入門套件][ lnk-starter-kits]已經有 NOOBS 安裝。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="6f5a8-107">您可以開機 hello 覆盆子 Pi 從這張介面卡，並選擇 tooinstall hello Raspbian OS。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

<span data-ttu-id="6f5a8-108">您需要 toocomplete hello 硬體安裝程式：</span><span class="sxs-lookup"><span data-stu-id="6f5a8-108">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="6f5a8-109">連接 hello 套件中包含您覆盆子 Pi toohello 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-109">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="6f5a8-110">您覆盆子 Pi tooyour 的網路連線使用包含在您的套件中的 hello 乙太網路纜線。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-110">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="6f5a8-111">或者，您可以為 Raspberry Pi 設定[無線連線能力][lnk-pi-wireless]。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="6f5a8-112">您現在已完成覆盆子 Pi 的 hello 硬體安裝。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-112">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="6f5a8-113">登入及存取 hello 終端機</span><span class="sxs-lookup"><span data-stu-id="6f5a8-113">Sign in and access hello terminal</span></span>

<span data-ttu-id="6f5a8-114">您有兩個選項 tooaccess 終端機環境覆盆子 Pi 上：</span><span class="sxs-lookup"><span data-stu-id="6f5a8-114">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="6f5a8-115">如果您有鍵盤，監視連線的 tooyour 覆盆子 Pi，您可以使用 hello Raspbian GUI tooaccess 終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-115">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="6f5a8-116">從您桌面的電腦使用 SSH 您覆盆子 pi hello 命令列存取。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-116">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="6f5a8-117">在 hello GUI 中的終端機視窗</span><span class="sxs-lookup"><span data-stu-id="6f5a8-117">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="6f5a8-118">Raspbian hello 預設認證是使用者名稱**pi**和密碼**覆盆子**。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-118">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="6f5a8-119">您可以在 hello 工作列 hello GUI 中，啟動 hello**終端機**使用 hello 圖示看起來像監視器公用程式。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-119">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="6f5a8-120">使用 SSH 登入</span><span class="sxs-lookup"><span data-stu-id="6f5a8-120">Sign in with SSH</span></span>

<span data-ttu-id="6f5a8-121">您可以使用 SSH 的命令列存取 tooyour 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-121">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="6f5a8-122">hello 文章[SSH (Secure Shell)] [ lnk-pi-ssh]描述如何 tooconfigure SSH 您覆盆子 pi，以及如何從 tooconnect [Windows] [ lnk-ssh-windows]或[Linux 和 Mac OS][lnk-ssh-linux]。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-122">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="6f5a8-123">以使用者名稱 **pi** 和密碼 **raspberry** 登入。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="6f5a8-124">選擇性︰共用 Raspberry Pi 上的資料夾</span><span class="sxs-lookup"><span data-stu-id="6f5a8-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="6f5a8-125">或者，您可能想覆盆子 pi tooshare 資料夾與您的桌面環境。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-125">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="6f5a8-126">共用資料夾可讓您 toouse 慣用桌面的文字編輯器 (例如[Visual Studio Code](https://code.visualstudio.com/)或[適文字](http://www.sublimetext.com/)) tooedit 檔案，而不是使用您覆盆子 pi`nano`或`vi`.</span><span class="sxs-lookup"><span data-stu-id="6f5a8-126">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="6f5a8-127">隨 Windows 資料夾 tooshare Samba 上設定伺服器 hello 覆盆子 Pi。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-127">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="6f5a8-128">或者，使用內建的 hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) SFTP 用戶端在桌面上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6f5a8-128">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/