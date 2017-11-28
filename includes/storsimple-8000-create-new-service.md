<!--author=alkohli last changed:02/10/2017-->


#### <a name="to-create-a-new-service"></a><span data-ttu-id="800c1-101">建立新服務</span><span class="sxs-lookup"><span data-stu-id="800c1-101">To create a new service</span></span>

1. <span data-ttu-id="800c1-102">使用您的 Microsoft 帳戶認證以登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="800c1-102">Use your Microsoft account credentials to log on to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="800c1-103">在 Azure 入口網站中，按一下 [+]，然後在 Marketplace 中按一下 [查看全部]。</span><span class="sxs-lookup"><span data-stu-id="800c1-103">In the Azure portal, click **+** and then in the marketplace, click **See all**.</span></span>

    ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman1.png)

    <span data-ttu-id="800c1-105">搜尋 [StorSimple 實體]。</span><span class="sxs-lookup"><span data-stu-id="800c1-105">Search for _StorSimple Physical_.</span></span> <span data-ttu-id="800c1-106">選取並按一下 [StorSimple 實體裝置系列]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="800c1-106">Select and click **StorSimple Physical Device Series** and then click **Create**.</span></span> <span data-ttu-id="800c1-107">或者，在 Azure 入口網站中按一下 [+]，然後在 [儲存體]按一下 [StorSimple 實體裝置系列]。</span><span class="sxs-lookup"><span data-stu-id="800c1-107">Alternatively, in the Azure portal click **+** and then under **Storage**, click **StorSimple Physical Device Series**.</span></span>

    ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. <span data-ttu-id="800c1-109">在 [StorSimple 裝置管理員] 刀鋒視窗中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="800c1-109">In the **StorSimple Device Manager** blade, do the following steps:</span></span>
   
   1. <span data-ttu-id="800c1-110">為服務提供唯一的**資源名稱** 。</span><span class="sxs-lookup"><span data-stu-id="800c1-110">Supply a unique **Resource name** for your service.</span></span> <span data-ttu-id="800c1-111">這個名聲是可用來識別服務的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="800c1-111">This name is a friendly name that can be used to identify the service.</span></span> <span data-ttu-id="800c1-112">名稱長度可介於 2 到 50 個字元之間，且可以是字母、數字和連字號。</span><span class="sxs-lookup"><span data-stu-id="800c1-112">The name can have between 2 and 50 characters that can be letters, numbers, and hyphens.</span></span> <span data-ttu-id="800c1-113">名稱必須以字母或數字為開頭或結尾。</span><span class="sxs-lookup"><span data-stu-id="800c1-113">The name must start and end with a letter or a number.</span></span>

   2. <span data-ttu-id="800c1-114">從下拉式清單選擇 [訂用帳戶]  。</span><span class="sxs-lookup"><span data-stu-id="800c1-114">Choose a **Subscription** from the drop-down list.</span></span> <span data-ttu-id="800c1-115">訂用帳戶會連結到您的帳單帳戶。</span><span class="sxs-lookup"><span data-stu-id="800c1-115">The subscription is linked to your billing account.</span></span> <span data-ttu-id="800c1-116">如果您只擁有一個訂用帳戶，則此欄位不存在。</span><span class="sxs-lookup"><span data-stu-id="800c1-116">This field is not present if you have only one subscription.</span></span>

   3. <span data-ttu-id="800c1-117">針對**資源群組**，**使用現有群組**或**建立新的群組**。</span><span class="sxs-lookup"><span data-stu-id="800c1-117">For **Resource group**, **Use existing** or **Create new** group.</span></span> <span data-ttu-id="800c1-118">如需詳細資訊，請參閱 [Azure 資源群組](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/)。</span><span class="sxs-lookup"><span data-stu-id="800c1-118">For more information, see [Azure resource groups](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).</span></span>
   
   4. <span data-ttu-id="800c1-119">提供服務的 [位置]  。</span><span class="sxs-lookup"><span data-stu-id="800c1-119">Supply a **Location** for your service.</span></span> <span data-ttu-id="800c1-120">一般而言，請選擇最接近您想要部署裝置之地理區域的位置。</span><span class="sxs-lookup"><span data-stu-id="800c1-120">In general, choose a location closest to the geographical region where you want to deploy your device.</span></span> <span data-ttu-id="800c1-121">您可能也需要計入下列考量因素：</span><span class="sxs-lookup"><span data-stu-id="800c1-121">You may also want to factor in the following considerations:</span></span> 
      
      * <span data-ttu-id="800c1-122">如果您在 Azure 中有工作負載，且想要與您的 StorSimple 裝置部署，請使用該資料中心。</span><span class="sxs-lookup"><span data-stu-id="800c1-122">If you have existing workloads in Azure that you also intend to deploy with your StorSimple device, you should use that datacenter.</span></span>
      * <span data-ttu-id="800c1-123">您的 StorSimple 裝置管理員服務和 Azure 儲存體可以位於兩個不同的位置。</span><span class="sxs-lookup"><span data-stu-id="800c1-123">Your StorSimple Device Manager service and Azure storage can be in two separate locations.</span></span> <span data-ttu-id="800c1-124">如此一來，您需要分別建立 StorSimple 裝置管理員和 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="800c1-124">In such a case, you are required to create the StorSimple Device Manager and Azure storage account separately.</span></span> <span data-ttu-id="800c1-125">若要建立 Azure 儲存體帳戶，請前往 Azure 入口網站中的 [Azure 儲存體服務]，依[建立 Azure 儲存體帳戶](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="800c1-125">To create an Azure storage account, go to the Azure Storage service in the Azure portal and follow the steps in [Create an Azure Storage account](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="800c1-126">建立此帳戶之後，請依[設定服務的新儲存體帳戶](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service)中的步驟，將此帳戶新增到 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="800c1-126">After you create this account, add it to the StorSimple Device Manager service by following the steps in [Configure a new storage account for the service](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).</span></span>

   5. <span data-ttu-id="800c1-127">選取 [建立新的儲存體帳戶]  ，自動建立具有此服務的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="800c1-127">Select **Create a new storage account** to automatically create a storage account with the service.</span></span> <span data-ttu-id="800c1-128">指定此儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="800c1-128">Specify a name for this storage account.</span></span> <span data-ttu-id="800c1-129">如果您需要將資料放在不同的位置，取消核取此方塊。</span><span class="sxs-lookup"><span data-stu-id="800c1-129">If you need your data in a different location, uncheck this box.</span></span>

   6. <span data-ttu-id="800c1-130">如果您想在儀表板上快速連結到此服務，請勾選 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="800c1-130">Check **Pin to dashboard** if you want a quick link to this service on your dashboard.</span></span>
      
   7. <span data-ttu-id="800c1-131">按一下 [建立] 以建立 StorSimple 裝置管理員。</span><span class="sxs-lookup"><span data-stu-id="800c1-131">Click **Create** to create the StorSimple Device Manager.</span></span>

       ![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
<span data-ttu-id="800c1-133">服務建立需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="800c1-133">The service creation takes a few minutes.</span></span> <span data-ttu-id="800c1-134">成功建立服務之後，您會看到通知，並隨即開啟新的服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="800c1-134">After the service is successfully created, you will see a notification and the new service blade opens up.</span></span>
   
![建立 StorSimple 裝置管理員](./media/storsimple-8000-create-new-service/createssdevman5.png)


