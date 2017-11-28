## <a name="prerequisites"></a><span data-ttu-id="768fe-101">必要條件</span><span class="sxs-lookup"><span data-stu-id="768fe-101">Prerequisites</span></span>

<span data-ttu-id="768fe-102">若要完成此教學課程，您需要一個有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="768fe-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="768fe-103">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="768fe-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="768fe-104">如需詳細資訊，請參閱 [Azure 免費試用][lnk-free-trial]。</span><span class="sxs-lookup"><span data-stu-id="768fe-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="768fe-105">必要的軟體</span><span class="sxs-lookup"><span data-stu-id="768fe-105">Required software</span></span>

<span data-ttu-id="768fe-106">您需要透過桌上型電腦的 SSH 用戶端，才能從遠端存取 Intel NUC 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="768fe-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Intel NUC.</span></span>

- <span data-ttu-id="768fe-107">Windows 不包含 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="768fe-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="768fe-108">我們建議使用 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="768fe-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="768fe-109">大部分的 Linux 散發套件和 Mac OS 都包含命令列 SSH 公用程式。</span><span class="sxs-lookup"><span data-stu-id="768fe-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span>

### <a name="required-hardware"></a><span data-ttu-id="768fe-110">必要的硬體</span><span class="sxs-lookup"><span data-stu-id="768fe-110">Required hardware</span></span>

<span data-ttu-id="768fe-111">一部桌上型電腦，可讓您從遠端連線到 Intel NUC 上的命令列。</span><span class="sxs-lookup"><span data-stu-id="768fe-111">A desktop computer to enable you to connect remotely to the command line on the Intel NUC.</span></span>

<span data-ttu-id="768fe-112">[IoT 商業閘道套件][lnk-starter-kits]。</span><span class="sxs-lookup"><span data-stu-id="768fe-112">[IoT Commercial Gateway Kit][lnk-starter-kits].</span></span> <span data-ttu-id="768fe-113">本教學課程會使用套件中的下列項目：</span><span class="sxs-lookup"><span data-stu-id="768fe-113">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="768fe-114">Intel® NUC Kit DE3815TYKE 與 4G 記憶體和藍牙擴充卡</span><span class="sxs-lookup"><span data-stu-id="768fe-114">Intel® NUC Kit DE3815TYKE with 4G Memory and Bluetooth expansion card</span></span>
- <span data-ttu-id="768fe-115">電源配接器</span><span class="sxs-lookup"><span data-stu-id="768fe-115">Power adaptor</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/