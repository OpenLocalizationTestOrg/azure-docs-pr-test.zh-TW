<!--author=alkohli last changed: 07/07/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a><span data-ttu-id="c5d05-101">tooinstall 從 hello Azure 入口網站更新</span><span class="sxs-lookup"><span data-stu-id="c5d05-101">tooinstall an update from hello Azure portal</span></span>

1. <span data-ttu-id="c5d05-102">在 hello StorSimple 服務頁面上，選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="c5d05-102">On hello StorSimple service page, select your device.</span></span>

    ![選取裝置](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. <span data-ttu-id="c5d05-104">瀏覽過**裝置設定** > **裝置更新**。</span><span class="sxs-lookup"><span data-stu-id="c5d05-104">Navigate too**Device settings** > **Device updates**.</span></span>

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. <span data-ttu-id="c5d05-106">有新的更新可用時，會顯示通知。</span><span class="sxs-lookup"><span data-stu-id="c5d05-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="c5d05-107">或者，在 hello**裝置更新**刀鋒視窗中，按一下 **掃描更新**。</span><span class="sxs-lookup"><span data-stu-id="c5d05-107">Alternatively, in hello **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="c5d05-108">Tooscan 可用的更新時，會建立一個作業。</span><span class="sxs-lookup"><span data-stu-id="c5d05-108">A job is created tooscan for available updates.</span></span> <span data-ttu-id="c5d05-109">Hello 作業順利完成時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="c5d05-109">You are notified when hello job completes successfully.</span></span>

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. <span data-ttu-id="c5d05-111">我們建議您在裝置上套用更新之前，檢閱 hello 版本資訊。</span><span class="sxs-lookup"><span data-stu-id="c5d05-111">We recommend that you review hello release notes before you apply an update on your device.</span></span> <span data-ttu-id="c5d05-112">按一下 tooapply 更新**安裝更新**。</span><span class="sxs-lookup"><span data-stu-id="c5d05-112">tooapply updates, click **Install updates**.</span></span> <span data-ttu-id="c5d05-113">在 hello**確認定期更新**刀鋒視窗中，檢閱 hello 必要條件 toocomplete 然後再套用更新。</span><span class="sxs-lookup"><span data-stu-id="c5d05-113">In hello **Confirm regular updates** blade, review hello prerequisites toocomplete before you apply updates.</span></span> <span data-ttu-id="c5d05-114">選取您已準備好 tooupdate hello 裝置，然後按一下 hello 核取方塊 tooindicate**安裝**。</span><span class="sxs-lookup"><span data-stu-id="c5d05-114">Select hello checkbox tooindicate that you are ready tooupdate hello device and then click **Install**.</span></span>

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. <span data-ttu-id="c5d05-116">一組必要條件檢查會隨即開始。</span><span class="sxs-lookup"><span data-stu-id="c5d05-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="c5d05-117">這些檢查包括︰</span><span class="sxs-lookup"><span data-stu-id="c5d05-117">These checks include:</span></span>
   
   * <span data-ttu-id="c5d05-118">**控制器健康情況檢查**tooverify 兩者 hello 裝置控制器皆狀況良好並線上。</span><span class="sxs-lookup"><span data-stu-id="c5d05-118">**Controller health checks** tooverify that both hello device controllers are healthy and online.</span></span>
   * <span data-ttu-id="c5d05-119">**硬體元件健康情況檢查**tooverify 所有 hello StorSimple 裝置上的硬體元件均狀況良好。</span><span class="sxs-lookup"><span data-stu-id="c5d05-119">**Hardware component health checks** tooverify that all hello hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="c5d05-120">**檢查 DATA 0** tooverify DATA 0 已啟用您的裝置上。</span><span class="sxs-lookup"><span data-stu-id="c5d05-120">**DATA 0 checks** tooverify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="c5d05-121">如果未啟用此介面，您必須啟用它，然後重試。</span><span class="sxs-lookup"><span data-stu-id="c5d05-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="c5d05-122">下載並安裝所有的 hello 檢查成功完成時，才 hello 更新時。</span><span class="sxs-lookup"><span data-stu-id="c5d05-122">hello update is downloaded and installed only if all hello checks are successfully completed.</span></span> <span data-ttu-id="c5d05-123">Hello 檢查進行中時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="c5d05-123">You are notified when hello checks are in progress.</span></span> <span data-ttu-id="c5d05-124">如果 hello prechecks 失敗，您將會提供與 hello 失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="c5d05-124">If hello prechecks fail, then you will be provided with hello reasons for failure.</span></span> <span data-ttu-id="c5d05-125">解決這些問題，然後再重試 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="c5d05-125">Address those issues and then retry hello operation.</span></span> <span data-ttu-id="c5d05-126">如果您無法自行解決這些問題，您可能需要 toocontact Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="c5d05-126">You may need toocontact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="c5d05-127">Hello prechecks 成功完成之後，會建立更新工作。</span><span class="sxs-lookup"><span data-stu-id="c5d05-127">After hello prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="c5d05-128">已成功建立 hello 更新工作時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="c5d05-128">You are notified when hello update job is successfully created.</span></span>
   
    ![建立更新工作](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    <span data-ttu-id="c5d05-130">hello 更新然後會套用至您的裝置。</span><span class="sxs-lookup"><span data-stu-id="c5d05-130">hello update is then applied on your device.</span></span>

9. <span data-ttu-id="c5d05-131">hello 更新所需的幾個小時 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="c5d05-131">hello update takes a few hours toocomplete.</span></span> <span data-ttu-id="c5d05-132">選取 hello 更新工作，然後按一下**詳細資料**隨時 hello 工作 tooview hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c5d05-132">Select hello update job and click **Details** tooview hello details of hello job at any time.</span></span>

    ![建立更新工作](./media/storsimple-8000-install-update4-via-portal/update8.png)

     <span data-ttu-id="c5d05-134">您也可以監視 hello 更新作業，從 hello 進度**裝置設定 > 工作**。</span><span class="sxs-lookup"><span data-stu-id="c5d05-134">You can also monitor hello progress of hello update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="c5d05-135">在 hello**作業**刀鋒視窗中，您可以看到 hello 更新進度。</span><span class="sxs-lookup"><span data-stu-id="c5d05-135">On hello **Jobs** blade, you can see hello update progress.</span></span>

     ![建立更新工作](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. <span data-ttu-id="c5d05-137">Hello 工作完成後，瀏覽 toohello**裝置設定 > 裝置更新**。</span><span class="sxs-lookup"><span data-stu-id="c5d05-137">After hello job is complete, navigate toohello **Device settings > Device updates**.</span></span> <span data-ttu-id="c5d05-138">現在應該更新 hello 軟體版本。</span><span class="sxs-lookup"><span data-stu-id="c5d05-138">hello software version should now be updated.</span></span>

    ![建立更新工作](./media/storsimple-8000-install-update4-via-portal/update9.png)

