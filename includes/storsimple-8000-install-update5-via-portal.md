<!--author=alkohli last changed: 08/04/17-->

#### <a name="to-install-an-update-from-the-azure-portal"></a><span data-ttu-id="90477-101">從 Azure 入口網站安裝更新</span><span class="sxs-lookup"><span data-stu-id="90477-101">To install an update from the Azure portal</span></span>

1. <span data-ttu-id="90477-102">在 [StorSimple 服務] 頁面上，選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="90477-102">On the StorSimple service page, select your device.</span></span>

    ![選取裝置](./media/storsimple-8000-install-update5-via-portal/update1.png)

2. <span data-ttu-id="90477-104">瀏覽至 [裝置設定] > [裝置更新]。</span><span class="sxs-lookup"><span data-stu-id="90477-104">Navigate to **Device settings** > **Device updates**.</span></span>

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update5-via-portal/update2.png)

2. <span data-ttu-id="90477-106">有新的更新可用時，會顯示通知。</span><span class="sxs-lookup"><span data-stu-id="90477-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="90477-107">或者，在 [裝置更新] 刀鋒視窗中，按一下 [掃描更新]。</span><span class="sxs-lookup"><span data-stu-id="90477-107">Alternatively, in the **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="90477-108">系統會建立用來掃描可用更新的作業。</span><span class="sxs-lookup"><span data-stu-id="90477-108">A job is created to scan for available updates.</span></span> <span data-ttu-id="90477-109">當作業成功完成時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="90477-109">You are notified when the job completes successfully.</span></span>

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update5-via-portal/update3.png)

3. <span data-ttu-id="90477-111">我們建議您先檢閱版本資訊，然後再於裝置上套用更新。</span><span class="sxs-lookup"><span data-stu-id="90477-111">We recommend that you review the release notes before you apply an update on your device.</span></span> <span data-ttu-id="90477-112">若要套用更新，請按一下 [安裝更新]。</span><span class="sxs-lookup"><span data-stu-id="90477-112">To apply updates, click **Install updates**.</span></span> <span data-ttu-id="90477-113">在 [確認定期更新] 刀鋒視窗中，檢閱要完成的必要條件後，才能套用更新。</span><span class="sxs-lookup"><span data-stu-id="90477-113">In the **Confirm regular updates** blade, review the prerequisites to complete before you apply updates.</span></span> <span data-ttu-id="90477-114">選取核取方塊，指出您已準備好更新裝置，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="90477-114">Select the checkbox to indicate that you are ready to update the device and then click **Install**.</span></span>

    ![按一下 [裝置更新]](./media/storsimple-8000-install-update5-via-portal/update4.png)

6. <span data-ttu-id="90477-116">一組必要條件檢查會隨即開始。</span><span class="sxs-lookup"><span data-stu-id="90477-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="90477-117">這些檢查包括︰</span><span class="sxs-lookup"><span data-stu-id="90477-117">These checks include:</span></span>
   
   * <span data-ttu-id="90477-118">**控制器健康狀況檢查** ：確認這兩個裝置控制器的狀況良好且在線上。</span><span class="sxs-lookup"><span data-stu-id="90477-118">**Controller health checks** to verify that both the device controllers are healthy and online.</span></span>
   * <span data-ttu-id="90477-119">**硬體元件健康狀況檢查** ：確認您的 StorSimple 裝置上的所有硬體元件的狀況良好。</span><span class="sxs-lookup"><span data-stu-id="90477-119">**Hardware component health checks** to verify that all the hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="90477-120">**DATA 0 檢查** ：確認您的裝置已啟用 DATA 0。</span><span class="sxs-lookup"><span data-stu-id="90477-120">**DATA 0 checks** to verify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="90477-121">如果未啟用此介面，您必須啟用它，然後重試。</span><span class="sxs-lookup"><span data-stu-id="90477-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="90477-122">只在所有檢查都成功都完成時，才會下載並安裝更新。</span><span class="sxs-lookup"><span data-stu-id="90477-122">The update is downloaded and installed only if all the checks are successfully completed.</span></span> <span data-ttu-id="90477-123">當檢查進行時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="90477-123">You are notified when the checks are in progress.</span></span> <span data-ttu-id="90477-124">如果前置檢查失敗，系統將會提供您失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="90477-124">If the prechecks fail, then you will be provided with the reasons for failure.</span></span> <span data-ttu-id="90477-125">處理這些問題，然後重試作業。</span><span class="sxs-lookup"><span data-stu-id="90477-125">Address those issues and then retry the operation.</span></span> <span data-ttu-id="90477-126">如果您不能自行解決這些問題，您可能需要連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="90477-126">You may need to contact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="90477-127">前置檢查成功完成後，將會建立更新作業。</span><span class="sxs-lookup"><span data-stu-id="90477-127">After the prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="90477-128">成功建立更新作業時，系統將會通知您。</span><span class="sxs-lookup"><span data-stu-id="90477-128">You are notified when the update job is successfully created.</span></span>
   
    ![建立更新工作](./media/storsimple-8000-install-update5-via-portal/update6.png)
   
    <span data-ttu-id="90477-130">接著，更新會套用到您的裝置上。</span><span class="sxs-lookup"><span data-stu-id="90477-130">The update is then applied on your device.</span></span>

9. <span data-ttu-id="90477-131">更新需要幾個小時才能完成。</span><span class="sxs-lookup"><span data-stu-id="90477-131">The update takes a few hours to complete.</span></span> <span data-ttu-id="90477-132">隨時可選取更新工作並按一下 [詳細資料]  來檢視工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="90477-132">Select the update job and click **Details** to view the details of the job at any time.</span></span>

    ![建立更新工作](./media/storsimple-8000-install-update5-via-portal/update8.png)

     <span data-ttu-id="90477-134">您也可以從 [裝置設定] > [作業] 來監視更新作業的進度。</span><span class="sxs-lookup"><span data-stu-id="90477-134">You can also monitor the progress of the update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="90477-135">在 [作業] 刀鋒視窗中，您可以看到更新進度。</span><span class="sxs-lookup"><span data-stu-id="90477-135">On the **Jobs** blade, you can see the update progress.</span></span>

     ![建立更新工作](./media/storsimple-8000-install-update5-via-portal/update7.png)

10. <span data-ttu-id="90477-137">作業完成後，瀏覽至 [裝置設定] > [裝置更新]。</span><span class="sxs-lookup"><span data-stu-id="90477-137">After the job is complete, navigate to the **Device settings > Device updates**.</span></span> <span data-ttu-id="90477-138">現在應該已更新軟體版本。</span><span class="sxs-lookup"><span data-stu-id="90477-138">The software version should now be updated.</span></span>

