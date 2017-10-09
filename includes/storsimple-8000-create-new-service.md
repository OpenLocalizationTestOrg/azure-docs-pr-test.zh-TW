<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a><span data-ttu-id="321f9-101">toocreate 新的服務</span><span class="sxs-lookup"><span data-stu-id="321f9-101">toocreate a new service</span></span>

1. <span data-ttu-id="321f9-102">使用您的 Microsoft 帳戶認證 toolog toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="321f9-102">Use your Microsoft account credentials toolog on toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="321f9-103">在 hello Azure 入口網站，按一下   **+**  ，然後在 hello marketplace 按一下**查看所有**。</span><span class="sxs-lookup"><span data-stu-id="321f9-103">In hello Azure portal, click **+** and then in hello marketplace, click **See all**.</span></span>

    ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman1.png)

    <span data-ttu-id="321f9-105">搜尋 [StorSimple 實體]。</span><span class="sxs-lookup"><span data-stu-id="321f9-105">Search for _StorSimple Physical_.</span></span> <span data-ttu-id="321f9-106">選取並按一下 StorSimple 實體裝置系列，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="321f9-106">Select and click **StorSimple Physical Device Series** and then click **Create**.</span></span> <span data-ttu-id="321f9-107">或者，在 hello Azure 入口網站中按一下 **+**  ，然後在**儲存體**，按一下  **StorSimple 實體裝置系列**。</span><span class="sxs-lookup"><span data-stu-id="321f9-107">Alternatively, in hello Azure portal click **+** and then under **Storage**, click **StorSimple Physical Device Series**.</span></span>

    ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. <span data-ttu-id="321f9-109">在 hello **StorSimple 裝置管理員**刀鋒視窗中，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="321f9-109">In hello **StorSimple Device Manager** blade, do hello following steps:</span></span>
   
   1. <span data-ttu-id="321f9-110">為服務提供唯一的**資源名稱** 。</span><span class="sxs-lookup"><span data-stu-id="321f9-110">Supply a unique **Resource name** for your service.</span></span> <span data-ttu-id="321f9-111">這個名稱是易記的名稱可能是使用 tooidentify hello 服務。</span><span class="sxs-lookup"><span data-stu-id="321f9-111">This name is a friendly name that can be used tooidentify hello service.</span></span> <span data-ttu-id="321f9-112">hello 名稱只能有 2 到 50 個字元，可以是字母、 數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="321f9-112">hello name can have between 2 and 50 characters that can be letters, numbers, and hyphens.</span></span> <span data-ttu-id="321f9-113">hello 名稱必須啟動，並以字母或數字結尾。</span><span class="sxs-lookup"><span data-stu-id="321f9-113">hello name must start and end with a letter or a number.</span></span>

   2. <span data-ttu-id="321f9-114">選擇**訂用帳戶**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="321f9-114">Choose a **Subscription** from hello drop-down list.</span></span> <span data-ttu-id="321f9-115">計費帳戶連結的 tooyour hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="321f9-115">hello subscription is linked tooyour billing account.</span></span> <span data-ttu-id="321f9-116">如果您只擁有一個訂用帳戶，則此欄位不存在。</span><span class="sxs-lookup"><span data-stu-id="321f9-116">This field is not present if you have only one subscription.</span></span>

   3. <span data-ttu-id="321f9-117">針對**資源群組**，**使用現有群組**或**建立新的群組**。</span><span class="sxs-lookup"><span data-stu-id="321f9-117">For **Resource group**, **Use existing** or **Create new** group.</span></span> <span data-ttu-id="321f9-118">如需詳細資訊，請參閱 [Azure 資源群組](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/)。</span><span class="sxs-lookup"><span data-stu-id="321f9-118">For more information, see [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).</span></span>
   
   4. <span data-ttu-id="321f9-119">提供服務的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="321f9-119">Supply a **Location** for your service.</span></span> <span data-ttu-id="321f9-120">一般情況下，選擇位置最靠近 toohello 地理區域 toodeploy 希望您的裝置。</span><span class="sxs-lookup"><span data-stu-id="321f9-120">In general, choose a location closest toohello geographical region where you want toodeploy your device.</span></span> <span data-ttu-id="321f9-121">您也可以在下列考量 hello toofactor:</span><span class="sxs-lookup"><span data-stu-id="321f9-121">You may also want toofactor in hello following considerations:</span></span> 
      
      * <span data-ttu-id="321f9-122">如果您有現有的工作負載，您也想 toodeploy 與您的 StorSimple 裝置的 Azure 中，您應該使用該資料中心。</span><span class="sxs-lookup"><span data-stu-id="321f9-122">If you have existing workloads in Azure that you also intend toodeploy with your StorSimple device, you should use that datacenter.</span></span>
      * <span data-ttu-id="321f9-123">您的 StorSimple 裝置管理員服務和 Azure 儲存體可以位於兩個不同的位置。</span><span class="sxs-lookup"><span data-stu-id="321f9-123">Your StorSimple Device Manager service and Azure storage can be in two separate locations.</span></span> <span data-ttu-id="321f9-124">在這種情況下，您會需要的 toocreate hello StorSimple 裝置管理員和 Azure 儲存體帳戶分開。</span><span class="sxs-lookup"><span data-stu-id="321f9-124">In such a case, you are required toocreate hello StorSimple Device Manager and Azure storage account separately.</span></span> <span data-ttu-id="321f9-125">toocreate Azure 儲存體帳戶，請移 toohello hello Azure 入口網站中的 Azure 儲存體服務，並依照中的 hello 步驟[建立 Azure 儲存體帳戶](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="321f9-125">toocreate an Azure storage account, go toohello Azure Storage service in hello Azure portal and follow hello steps in [Create an Azure Storage account](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="321f9-126">建立此帳戶之後，將它加入 toohello StorSimple 裝置 Manager 服務中的 hello 步驟[設定新的儲存體帳戶 hello 服務](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service)。</span><span class="sxs-lookup"><span data-stu-id="321f9-126">After you create this account, add it toohello StorSimple Device Manager service by following hello steps in [Configure a new storage account for hello service](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).</span></span>

   5. <span data-ttu-id="321f9-127">選取**建立新的儲存體帳戶**tooautomatically 與 hello 服務建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="321f9-127">Select **Create a new storage account** tooautomatically create a storage account with hello service.</span></span> <span data-ttu-id="321f9-128">指定此儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="321f9-128">Specify a name for this storage account.</span></span> <span data-ttu-id="321f9-129">如果您需要將資料放在不同的位置，取消核取此方塊。</span><span class="sxs-lookup"><span data-stu-id="321f9-129">If you need your data in a different location, uncheck this box.</span></span>

   6. <span data-ttu-id="321f9-130">請檢查**Pin toodashboard**如果您想要快速連結 toothis 服務儀表板上。</span><span class="sxs-lookup"><span data-stu-id="321f9-130">Check **Pin toodashboard** if you want a quick link toothis service on your dashboard.</span></span>
      
   7. <span data-ttu-id="321f9-131">按一下**建立**toocreate hello StorSimple 裝置管理員。</span><span class="sxs-lookup"><span data-stu-id="321f9-131">Click **Create** toocreate hello StorSimple Device Manager.</span></span>

       ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
<span data-ttu-id="321f9-133">hello 服務建立作業需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="321f9-133">hello service creation takes a few minutes.</span></span> <span data-ttu-id="321f9-134">已成功建立 hello 服務之後，您會看到通知，而且 hello 新服務刀鋒視窗會開啟。</span><span class="sxs-lookup"><span data-stu-id="321f9-134">After hello service is successfully created, you will see a notification and hello new service blade opens up.</span></span>
   
![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman5.png)


