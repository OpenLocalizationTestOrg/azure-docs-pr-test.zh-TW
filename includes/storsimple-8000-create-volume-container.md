<!--author=alkohli last changed: 06/22/17-->

#### <a name="toocreate-a-volume-container"></a><span data-ttu-id="3f52c-101">toocreate 磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="3f52c-101">toocreate a volume container</span></span>
1. <span data-ttu-id="3f52c-102">移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="3f52c-102">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="3f52c-103">從 hello 表格式 hello 裝置的清單，選取，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="3f52c-103">From hello tabular listing of hello devices, select and click a device.</span></span> 

    ![磁碟區容器刀鋒視窗](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="3f52c-105">在 hello 裝置儀表板中，按一下  **+ 新增磁碟區容器**</span><span class="sxs-lookup"><span data-stu-id="3f52c-105">In hello device dashboard, click **+ Add volume container**</span></span>

    ![磁碟區容器刀鋒視窗](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="3f52c-107">在 hello**新增磁碟區容器**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="3f52c-107">In hello **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="3f52c-108">hello 裝置會自動選取。</span><span class="sxs-lookup"><span data-stu-id="3f52c-108">hello device is automatically selected.</span></span>
   2. <span data-ttu-id="3f52c-109">提供磁碟區容器的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="3f52c-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="3f52c-110">hello 名稱必須是 3 too32 個字元長。</span><span class="sxs-lookup"><span data-stu-id="3f52c-110">hello name must be 3 too32 characters long.</span></span> <span data-ttu-id="3f52c-111">一旦建立磁碟區容器，您就無法將它重新命名。</span><span class="sxs-lookup"><span data-stu-id="3f52c-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="3f52c-112">選取**啟用雲端儲存體加密**tooenable hello 傳送的資料從 hello 裝置 toohello 雲端的加密。</span><span class="sxs-lookup"><span data-stu-id="3f52c-112">Select **Enable Cloud Storage Encryption** tooenable encryption of hello data sent from hello device toohello cloud.</span></span>
   4. <span data-ttu-id="3f52c-113">提供並確認**雲端儲存體加密金鑰**也就是 too32 長度 8 個字元。</span><span class="sxs-lookup"><span data-stu-id="3f52c-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 too32 characters long.</span></span> <span data-ttu-id="3f52c-114">Hello 裝置 tooaccess 加密資料會使用此金鑰。</span><span class="sxs-lookup"><span data-stu-id="3f52c-114">This key is used by hello device tooaccess encrypted data.</span></span>
   5. <span data-ttu-id="3f52c-115">選取**儲存體帳戶**tooassociate 與此磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="3f52c-115">Select a **Storage Account** tooassociate with this volume container.</span></span> <span data-ttu-id="3f52c-116">您可以選擇現有的儲存體帳戶或在服務建立 hello 時產生的 hello 預設帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f52c-116">You can choose an existing storage account or hello default account that is generated at hello time of service creation.</span></span> <span data-ttu-id="3f52c-117">您也可以使用 hello**新增**選項 toospecify 不是儲存體帳戶連結 toothis 服務訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f52c-117">You can also use hello **Add new** option toospecify a storage account that is not linked toothis service subscription.</span></span>
   6. <span data-ttu-id="3f52c-118">選取**Unlimited**在 hello**指定頻寬**下拉式清單，如果您想 tooconsume 所有 hello 可用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="3f52c-118">Select **Unlimited** in hello **Specify bandwidth** drop-down list if you wish tooconsume all hello available bandwidth.</span></span> <span data-ttu-id="3f52c-119">您也可以太設定此選項**自訂**tooemploy 頻寬控制，並指定 1 Mbps 到 1,000 Mbps 之間的值。</span><span class="sxs-lookup"><span data-stu-id="3f52c-119">You can also set this option too**Custom** tooemploy bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="3f52c-120">如果您有可用的頻寬使用量資訊，您可能會根據指定的排程可以 tooallocate 頻寬**選取頻寬範本**。</span><span class="sxs-lookup"><span data-stu-id="3f52c-120">If you have your bandwidth usage information available, you may be able tooallocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="3f52c-121">如逐步程序，請移至太[新增頻寬範本](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template)。</span><span class="sxs-lookup"><span data-stu-id="3f52c-121">For a step-by-step procedure, go too[Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![磁碟區容器刀鋒視窗](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="3f52c-123">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3f52c-123">Click **Create**.</span></span>

        ![磁碟區容器刀鋒視窗](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="3f52c-125">已成功建立 hello 磁碟區容器時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="3f52c-125">You are notified when hello volume container is successfully created.</span></span>

       ![磁碟區容器建立通知](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="3f52c-127">hello 新建立的磁碟區容器會列在 磁碟區容器，為您的裝置 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="3f52c-127">hello newly created volume container is listed in hello list of volume containers for your device.</span></span>

   ![新增磁碟區容器刀鋒視窗](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


