## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="11a8f-101">準備您的 Intel NUC</span><span class="sxs-lookup"><span data-stu-id="11a8f-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="11a8f-102">您需要 toocomplete hello 硬體安裝程式：</span><span class="sxs-lookup"><span data-stu-id="11a8f-102">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="11a8f-103">連接 hello 套件中包含您 Intel NUC toohello 電源供應器。</span><span class="sxs-lookup"><span data-stu-id="11a8f-103">Connect your Intel NUC toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="11a8f-104">連接 Intel NUC tooyour 網路使用乙太網路纜線。</span><span class="sxs-lookup"><span data-stu-id="11a8f-104">Connect your Intel NUC tooyour network using an Ethernet cable.</span></span>

<span data-ttu-id="11a8f-105">您現在已完成 Intel NUC 閘道裝置 hello 硬體的安裝。</span><span class="sxs-lookup"><span data-stu-id="11a8f-105">You have now completed hello hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="11a8f-106">登入及存取 hello 終端機</span><span class="sxs-lookup"><span data-stu-id="11a8f-106">Sign in and access hello terminal</span></span>

<span data-ttu-id="11a8f-107">您有兩個選項 tooaccess 終端機環境 Intel NUC 上：</span><span class="sxs-lookup"><span data-stu-id="11a8f-107">You have two options tooaccess a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="11a8f-108">如果您有鍵盤，監視連線的 tooyour Intel NUC，您可以直接存取 hello 殼層。</span><span class="sxs-lookup"><span data-stu-id="11a8f-108">If you have a keyboard and monitor connected tooyour Intel NUC, you can access hello shell directly.</span></span> <span data-ttu-id="11a8f-109">hello 預設認證是使用者名稱**根**和密碼**根**。</span><span class="sxs-lookup"><span data-stu-id="11a8f-109">hello default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="11a8f-110">從您桌面的電腦使用 SSH 您 Intel NUC 上存取 hello 殼層。</span><span class="sxs-lookup"><span data-stu-id="11a8f-110">Access hello shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="11a8f-111">使用 SSH 登入</span><span class="sxs-lookup"><span data-stu-id="11a8f-111">Sign in with SSH</span></span>

<span data-ttu-id="11a8f-112">使用 SSH toosign，您需要 Intel NUC hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="11a8f-112">toosign in with SSH, you need hello IP address of your Intel NUC.</span></span> <span data-ttu-id="11a8f-113">如果您有鍵盤，監視連線的 tooyour Intel NUC 使用 hello`ifconfig`命令 toofind hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="11a8f-113">If you have a keyboard and monitor connected tooyour Intel NUC, use hello `ifconfig` command toofind hello IP address.</span></span> <span data-ttu-id="11a8f-114">或者，連線 tooyour 路由器 toolist hello 位址的網路上的裝置。</span><span class="sxs-lookup"><span data-stu-id="11a8f-114">Alternatively, connect tooyour router toolist hello addresses of devices on your network.</span></span>

<span data-ttu-id="11a8f-115">以使用者名稱 **root** 和密碼 **root** 登入。</span><span class="sxs-lookup"><span data-stu-id="11a8f-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="11a8f-116">選擇性︰共用 Intel NUC 上的資料夾</span><span class="sxs-lookup"><span data-stu-id="11a8f-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="11a8f-117">（選擇性） 您可能想在 Intel NUC tooshare 資料夾與您的桌面環境。</span><span class="sxs-lookup"><span data-stu-id="11a8f-117">Optionally, you may want tooshare a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="11a8f-118">共用資料夾可讓您 toouse 慣用桌面的文字編輯器 (例如[Visual Studio Code](https://code.visualstudio.com/)或[適文字](http://www.sublimetext.com/)) tooedit 檔案而不是使用您 Intel NUC`nano`或`vi`.</span><span class="sxs-lookup"><span data-stu-id="11a8f-118">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="11a8f-119">tooshare 資料夾，以使用 Windows hello Intel NUC 上設定 Samba 伺服器。</span><span class="sxs-lookup"><span data-stu-id="11a8f-119">tooshare a folder with Windows, configure a Samba server on hello Intel NUC.</span></span> <span data-ttu-id="11a8f-120">或者，使用 hello SFTP 伺服器 hello Intel NUC 具有 SFTP 用戶端上您桌面的電腦上。</span><span class="sxs-lookup"><span data-stu-id="11a8f-120">Alternatively, use hello SFTP server on hello Intel NUC with an SFTP client on your desktop machine.</span></span>
