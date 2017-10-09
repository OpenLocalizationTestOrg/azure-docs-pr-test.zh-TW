<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a><span data-ttu-id="ab4ac-101">tooadd StorSimple 8000 系列 Update 1.0 的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ab4ac-101">tooadd a storage account in StorSimple 8000 Series Update 1.0</span></span>
1. <span data-ttu-id="ab4ac-102">Hello StorSimple Manager 服務登陸頁面，選取您的服務，然後按兩下。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-102">On hello StorSimple Manager service landing page, select your service and double-click it.</span></span> <span data-ttu-id="ab4ac-103">這會帶您 toohello**快速入門**頁面。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-103">This will take you toohello **Quick Start** page.</span></span> <span data-ttu-id="ab4ac-104">選取 hello**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-104">Select hello **Configure** page.</span></span>
2. <span data-ttu-id="ab4ac-105">按一下 [新增/編輯儲存體帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-105">Click **Add/edit storage account**.</span></span>
3. <span data-ttu-id="ab4ac-106">在 hello**新增/編輯儲存體帳戶**對話方塊中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-106">In hello **Add/Edit Storage Account** dialog box, click **Add new**.</span></span>
4. <span data-ttu-id="ab4ac-107">在 hello**提供者**hello 欄位時，選取適當的雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-107">In hello **Provider** field, select hello appropriate cloud service provider.</span></span> <span data-ttu-id="ab4ac-108">hello 支援提供者是 Azure、 Amazon S3、 RR、 HP 與 OpenStack Amazon S3。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-108">hello supported providers are Azure, Amazon S3, Amazon S3 with RRS, HP and OpenStack.</span></span> <span data-ttu-id="ab4ac-109">指定 hello 認證和 hello 與 hello 儲存體帳戶的雲端服務提供者相關聯的位置。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-109">Specify hello credentials and hello location associated with hello storage account of your cloud service providers.</span></span> <span data-ttu-id="ab4ac-110">提供認證的 hello 欄位將會不同視您所指定的 hello 雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-110">hello fields presented for credentials will be different depending upon hello cloud service provider you have specified.</span></span> 
   
   * <span data-ttu-id="ab4ac-111">如果您已選取 Azure 為您的雲端服務提供者，提供 hello**名稱**和主要的 hello**便捷鍵**Microsoft Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-111">If you have selected Azure as your cloud service provider, supply hello **Name** and hello primary **Access Key** for your Microsoft Azure storage account.</span></span> <span data-ttu-id="ab4ac-112">Azure 帳戶時，就會自動填入 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-112">For an Azure account, hello location will be automatically populated.</span></span>
     
        ![新增 Azure 儲存體帳戶](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * <span data-ttu-id="ab4ac-114">如果您選取 Amazon S3 或具有 RRS 的 Amazon S3 ，請提供易記的 [儲存體帳戶名稱]、[存取金鑰] 及 [祕密金鑰]。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-114">If you have selected Amazon S3 or Amazon S3 with RRS, provide a friendly **Storage Account name**, **Access Key**, and **Secret Key**.</span></span> <span data-ttu-id="ab4ac-115">Amazon S3 和 Amazon S3 的 RR，支援下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab4ac-115">For Amazon S3 and Amazon S3 with RRS, hello following locations are supported:</span></span>
     
     * <span data-ttu-id="ab4ac-116">美國標準</span><span class="sxs-lookup"><span data-stu-id="ab4ac-116">US Standard</span></span>
     * <span data-ttu-id="ab4ac-117">美國西部 (奧勒岡)</span><span class="sxs-lookup"><span data-stu-id="ab4ac-117">US West (Oregon)</span></span>
     * <span data-ttu-id="ab4ac-118">美國西部 (北加州)</span><span class="sxs-lookup"><span data-stu-id="ab4ac-118">US West (Northern California)</span></span>
     * <span data-ttu-id="ab4ac-119">歐盟 (愛爾蘭)</span><span class="sxs-lookup"><span data-stu-id="ab4ac-119">EU (Ireland)</span></span>
     * <span data-ttu-id="ab4ac-120">亞太地區 (新加坡)</span><span class="sxs-lookup"><span data-stu-id="ab4ac-120">Asia Pacific (Singapore)</span></span>
     * <span data-ttu-id="ab4ac-121">亞太地區 (雪梨)</span><span class="sxs-lookup"><span data-stu-id="ab4ac-121">Asia Pacific (Sydney)</span></span>
     * <span data-ttu-id="ab4ac-122">亞太地區 (東京)</span><span class="sxs-lookup"><span data-stu-id="ab4ac-122">Asia Pacific (Tokyo)</span></span>
     * <span data-ttu-id="ab4ac-123">南美洲 (聖保羅)</span><span class="sxs-lookup"><span data-stu-id="ab4ac-123">South America (Sao Paulo)</span></span>
       
       ![新增 Amazon 儲存體帳戶](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * <span data-ttu-id="ab4ac-125">如果您選取 HP 做為您的雲端服務提供者，請提供易記的 [儲存體帳戶名稱]、[租用戶識別碼]、[使用者名稱] 及[密碼]。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-125">If you have selected HP as your cloud service provider, supply a friendly **Storage Account Name**, **Tenant ID**, **Username**, and **Password**.</span></span> <span data-ttu-id="ab4ac-126">HP、 支援的下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="ab4ac-126">For HP, hello following locations are supported:</span></span>
     
     * <span data-ttu-id="ab4ac-127">美國東部</span><span class="sxs-lookup"><span data-stu-id="ab4ac-127">US East</span></span>
     * <span data-ttu-id="ab4ac-128">美國西部</span><span class="sxs-lookup"><span data-stu-id="ab4ac-128">US West</span></span>
       
       ![新增 HP 儲存體帳戶](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * <span data-ttu-id="ab4ac-130">如果您選取 **Openstack** 做為您的雲端服務提供者，請提供 [主機名稱]、[存取金鑰] 及 [秘密金鑰]。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-130">If you have selected **Openstack** as your cloud service provider, provide a **Hostname**, **Access Key**, and **Secret Key**.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="ab4ac-131">對於所有 hello 雲端服務提供者，但不包括 Azure、 允許的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-131">For all hello cloud service providers, excluding Azure, a friendly name is allowed.</span></span> <span data-ttu-id="ab4ac-132">您可以使用不同的易記名稱，並使用相同的認證設定的 hello 建立一個以上的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-132">You can use different friendly names and create more than one storage account with hello same set of credentials.</span></span>
     > 
     > 
     
        ![新增 Openstack 儲存體帳戶](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. <span data-ttu-id="ab4ac-134">選取**啟用 SSL 模式**toocreate 裝置與 hello 雲端之間的網路通訊的安全通道。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-134">Select **Enable SSL Mode** toocreate a secure channel for network communication between your device and hello cloud.</span></span> <span data-ttu-id="ab4ac-135">清除 hello**啟用 SSL 模式**核取方塊，才在私人雲端內操作。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-135">Clear hello **Enable SSL Mode** check box only if you are operating within a private cloud.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ab4ac-136">如果您使用 HP 做為您的提供者，將一律啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-136">If you are using HP as your provider, SSL will always be enabled.</span></span>
   > 
   > 
6. <span data-ttu-id="ab4ac-137">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="ab4ac-137">Click hello check icon</span></span> ![核取圖示](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png)<span data-ttu-id="ab4ac-139">.</span><span class="sxs-lookup"><span data-stu-id="ab4ac-139">.</span></span> <span data-ttu-id="ab4ac-140">已成功建立 hello 儲存體帳戶後，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-140">You will be notified after hello storage account is successfully created.</span></span>
7. <span data-ttu-id="ab4ac-141">hello 新建立的儲存體帳戶將會顯示在 hello**設定**頁面**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-141">hello newly created storage account will be displayed on hello **Configure** page under **Storage accounts**.</span></span> <span data-ttu-id="ab4ac-142">按一下**儲存**toosave hello 新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-142">Click **Save** toosave hello new storage account.</span></span> <span data-ttu-id="ab4ac-143">系統提示您進行確認時，按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="ab4ac-143">Click **OK** when prompted for confirmation.</span></span>

