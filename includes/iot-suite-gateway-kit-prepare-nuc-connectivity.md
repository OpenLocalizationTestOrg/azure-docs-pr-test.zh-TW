## <a name="prepare-your-intel-nuc"></a><span data-ttu-id="88f40-101">準備您的 Intel NUC</span><span class="sxs-lookup"><span data-stu-id="88f40-101">Prepare your Intel NUC</span></span>

<span data-ttu-id="88f40-102">若要完成硬體設定，您需要︰</span><span class="sxs-lookup"><span data-stu-id="88f40-102">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="88f40-103">將 Intel NUC 連線至套件內含的電源供應器。</span><span class="sxs-lookup"><span data-stu-id="88f40-103">Connect your Intel NUC to the power supply included in the kit.</span></span>
- <span data-ttu-id="88f40-104">使用乙太網路纜線將 Intel NUC 連線至您的網路。</span><span class="sxs-lookup"><span data-stu-id="88f40-104">Connect your Intel NUC to your network using an Ethernet cable.</span></span>

<span data-ttu-id="88f40-105">您現在已完成 Intel NUC 閘道裝置的硬體設定。</span><span class="sxs-lookup"><span data-stu-id="88f40-105">You have now completed the hardware setup of your Intel NUC gateway device.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="88f40-106">登入及存取終端機</span><span class="sxs-lookup"><span data-stu-id="88f40-106">Sign in and access the terminal</span></span>

<span data-ttu-id="88f40-107">您有兩種方式可存取 Intel NUC 上的終端機環境︰</span><span class="sxs-lookup"><span data-stu-id="88f40-107">You have two options to access a terminal environment on your Intel NUC:</span></span>

- <span data-ttu-id="88f40-108">如果您有連線至 Intel NUC 的鍵盤和監視器，就可以直接存取殼層。</span><span class="sxs-lookup"><span data-stu-id="88f40-108">If you have a keyboard and monitor connected to your Intel NUC, you can access the shell directly.</span></span> <span data-ttu-id="88f40-109">預設認證是使用者名稱 **root** 和密碼 **root**。</span><span class="sxs-lookup"><span data-stu-id="88f40-109">The default credentials are username **root** and password **root**.</span></span>

- <span data-ttu-id="88f40-110">使用桌上型電腦的 SSH 來存取 Intel NUC 上的殼層。</span><span class="sxs-lookup"><span data-stu-id="88f40-110">Access the shell on your Intel NUC using SSH from your desktop machine.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="88f40-111">使用 SSH 登入</span><span class="sxs-lookup"><span data-stu-id="88f40-111">Sign in with SSH</span></span>

<span data-ttu-id="88f40-112">若要使用 SSH 登入，您需要 Intel NUC 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="88f40-112">To sign in with SSH, you need the IP address of your Intel NUC.</span></span> <span data-ttu-id="88f40-113">如果您有連線至 Intel NUC 的鍵盤和監視器，請使用 `ifconfig` 命令來尋找 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="88f40-113">If you have a keyboard and monitor connected to your Intel NUC, use the `ifconfig` command to find the IP address.</span></span> <span data-ttu-id="88f40-114">或者，連線至您的路由器，將您網路上的裝置位址列出。</span><span class="sxs-lookup"><span data-stu-id="88f40-114">Alternatively, connect to your router to list the addresses of devices on your network.</span></span>

<span data-ttu-id="88f40-115">以使用者名稱 **root** 和密碼 **root** 登入。</span><span class="sxs-lookup"><span data-stu-id="88f40-115">Sign in with username **root** and password **root**.</span></span>

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a><span data-ttu-id="88f40-116">選擇性︰共用 Intel NUC 上的資料夾</span><span class="sxs-lookup"><span data-stu-id="88f40-116">Optional: Share a folder on your Intel NUC</span></span>

<span data-ttu-id="88f40-117">您可以與桌上型電腦環境共用 Intel NUC 上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="88f40-117">Optionally, you may want to share a folder on your Intel NUC with your desktop environment.</span></span> <span data-ttu-id="88f40-118">共用資料夾可讓您使用慣用的桌上型電腦文字編輯器 (例如 [Visual Studio Code](https://code.visualstudio.com/) 或 [Sublime Text](http://www.sublimetext.com/)) 來編輯 Intel NUC 上的檔案，而不是使用 `nano` 或 `vi`。</span><span class="sxs-lookup"><span data-stu-id="88f40-118">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Intel NUC instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="88f40-119">若要與 Windows 共用資料夾，請在 Intel NUC 上設定 Samba 伺服器。</span><span class="sxs-lookup"><span data-stu-id="88f40-119">To share a folder with Windows, configure a Samba server on the Intel NUC.</span></span> <span data-ttu-id="88f40-120">或者，使用 Intel NUC 上的 SFTP 伺服器搭配桌上型電腦上的 SFTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="88f40-120">Alternatively, use the SFTP server on the Intel NUC with an SFTP client on your desktop machine.</span></span>
