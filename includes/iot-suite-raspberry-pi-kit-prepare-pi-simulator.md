## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="b983c-101">準備您的 Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="b983c-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="b983c-102">安裝 Raspbian</span><span class="sxs-lookup"><span data-stu-id="b983c-102">Install Raspbian</span></span>

<span data-ttu-id="b983c-103">如果這是您第一次使用 Raspberry Pi，您需要使用套件內含 SD 卡上的 NOOBS 來安裝 Raspbian 作業系統。</span><span class="sxs-lookup"><span data-stu-id="b983c-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="b983c-104">[Raspberry Pi 軟體指南][lnk-install-raspbian]說明如何在 Raspberry Pi 上安裝作業系統。</span><span class="sxs-lookup"><span data-stu-id="b983c-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="b983c-105">本教學課程假設您已在 Raspberry Pi 上安裝 Raspbian 作業系統。</span><span class="sxs-lookup"><span data-stu-id="b983c-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="b983c-106">[適用於 Raspberry Pi 3 的 Microsoft Azure IoT 入門套件][lnk-starter-kits]內含的 SD 卡已安裝 NOOBS。</span><span class="sxs-lookup"><span data-stu-id="b983c-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="b983c-107">您可以從這張卡啟動 Raspberry Pi，並選擇安裝 Raspbian OS。</span><span class="sxs-lookup"><span data-stu-id="b983c-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

<span data-ttu-id="b983c-108">若要完成硬體設定，您需要︰</span><span class="sxs-lookup"><span data-stu-id="b983c-108">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="b983c-109">將 Raspberry Pi 連線至套件內含的電源供應器。</span><span class="sxs-lookup"><span data-stu-id="b983c-109">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="b983c-110">使用套件內含的乙太網路連接線，將 Raspberry Pi 連線至您的網路。</span><span class="sxs-lookup"><span data-stu-id="b983c-110">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="b983c-111">或者，您可以為 Raspberry Pi 設定[無線連線能力][lnk-pi-wireless]。</span><span class="sxs-lookup"><span data-stu-id="b983c-111">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="b983c-112">您現在已完成 Raspberry Pi 的硬體設定。</span><span class="sxs-lookup"><span data-stu-id="b983c-112">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="b983c-113">登入及存取終端機</span><span class="sxs-lookup"><span data-stu-id="b983c-113">Sign in and access the terminal</span></span>

<span data-ttu-id="b983c-114">您有兩個選項可存取 Raspberry Pi 上的終端機環境︰</span><span class="sxs-lookup"><span data-stu-id="b983c-114">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="b983c-115">如果您的 Raspberry Pi 已連接鍵盤與監視器，您可以使用 Raspbian GUI 來存取終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="b983c-115">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="b983c-116">使用 SSH 從您的桌上型電腦存取 Raspberry Pi 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="b983c-116">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="b983c-117">在 GUI 中使用終端機視窗</span><span class="sxs-lookup"><span data-stu-id="b983c-117">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="b983c-118">Raspbian 的預設認證是使用者名稱 **pi** 和密碼 **raspberry**。</span><span class="sxs-lookup"><span data-stu-id="b983c-118">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="b983c-119">在 GUI 的工作列中，您可以使用看似監視器的圖示來啟動 **Terminal** 公用程式。</span><span class="sxs-lookup"><span data-stu-id="b983c-119">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="b983c-120">使用 SSH 登入</span><span class="sxs-lookup"><span data-stu-id="b983c-120">Sign in with SSH</span></span>

<span data-ttu-id="b983c-121">您可以使用命令列的 SSH 存取 Raspberry Pi。</span><span class="sxs-lookup"><span data-stu-id="b983c-121">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="b983c-122">[SSH (安全殼層)][lnk-pi-ssh] 一文說明如何在 Raspberry Pi 上設定 SSH，以及如何從 [Windows][lnk-ssh-windows] 或 [Linux 和 Mac OS][lnk-ssh-linux] 連接。</span><span class="sxs-lookup"><span data-stu-id="b983c-122">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="b983c-123">以使用者名稱 **pi** 和密碼 **raspberry** 登入。</span><span class="sxs-lookup"><span data-stu-id="b983c-123">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="b983c-124">選擇性︰共用 Raspberry Pi 上的資料夾</span><span class="sxs-lookup"><span data-stu-id="b983c-124">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="b983c-125">選擇性地，您可能想要與您的桌上型電腦環境共用 Raspberry Pi 上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b983c-125">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="b983c-126">共用資料夾可讓您使用慣用的桌上型電腦文字編輯器 (例如 [Visual Studio Code](https://code.visualstudio.com/) 或 [Sublime Text](http://www.sublimetext.com/)) 來編輯 Raspberry Pi 上的檔案，而不是使用 `nano` 或 `vi`。</span><span class="sxs-lookup"><span data-stu-id="b983c-126">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="b983c-127">若要與 Windows 共用資料夾，請在 Raspberry Pi 上設定 Samba 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b983c-127">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="b983c-128">或者，使用內建 [SFTP](https://www.raspberrypi.org/documentation/remote-access/) 伺服器搭配桌上型電腦上的 SFTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b983c-128">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/