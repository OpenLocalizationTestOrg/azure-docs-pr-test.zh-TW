<!--author=alkohli last changed: 11/07/16 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="1d28f-101">透過 Azure 入口網站安裝更新</span><span class="sxs-lookup"><span data-stu-id="1d28f-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="1d28f-102">移至您的 StorSimple 裝置管理員，然後選取 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="1d28f-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="1d28f-103">從連接到您服務的裝置清單中，選取並按一下您想要更新的裝置。</span><span class="sxs-lookup"><span data-stu-id="1d28f-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate1m.png) 

2. <span data-ttu-id="1d28f-105">在 [設定] 刀鋒視窗中，按一下 [裝置更新]。</span><span class="sxs-lookup"><span data-stu-id="1d28f-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate2m.png)  

3. <span data-ttu-id="1d28f-107">如有軟體更新可用，您會看到一則訊息。</span><span class="sxs-lookup"><span data-stu-id="1d28f-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="1d28f-108">若要檢查更新，您也可以按一下 [掃描]。</span><span class="sxs-lookup"><span data-stu-id="1d28f-108">To check for updates, you can also click **Scan**.</span></span>

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate3m.png)

    <span data-ttu-id="1d28f-110">當掃瞄啟動且成功完成時，系統將會通知您。</span><span class="sxs-lookup"><span data-stu-id="1d28f-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate5m.png)

4. <span data-ttu-id="1d28f-112">在掃描更新之後，按一下 [下載更新]。</span><span class="sxs-lookup"><span data-stu-id="1d28f-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate6m.png)

5. <span data-ttu-id="1d28f-114">在 [新的更新] 刀鋒視窗中，於下載完成之後檢閱資訊，您必須確認安裝。</span><span class="sxs-lookup"><span data-stu-id="1d28f-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="1d28f-115">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1d28f-115">Click **OK**.</span></span>

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate7m.png)

6. <span data-ttu-id="1d28f-117">當上傳啟動且成功完成時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="1d28f-117">You are notified when the upload starts and completes successfully.</span></span>

     ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate8m.png)

5. <span data-ttu-id="1d28f-119">在 [裝置更新] 刀鋒視窗中，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="1d28f-119">In the **Device updates** blade, click **Install**.</span></span>

     ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate11m.png)   

6. <span data-ttu-id="1d28f-121">在 [新的更新] 刀鋒視窗中，系統會提醒您更新將造成運作中斷。</span><span class="sxs-lookup"><span data-stu-id="1d28f-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="1d28f-122">由於虛擬陣列是單一節點裝置，因此裝置會在更新之後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="1d28f-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="1d28f-123">這會中斷任何進行中的 IO。</span><span class="sxs-lookup"><span data-stu-id="1d28f-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="1d28f-124">按一下 [確定] 以安裝更新。</span><span class="sxs-lookup"><span data-stu-id="1d28f-124">Click **OK** to install the updates.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate12m.png) 

7. <span data-ttu-id="1d28f-126">安裝工作開始時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="1d28f-126">You are notified when the install job starts.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate13m.png)

8.  <span data-ttu-id="1d28f-128">在安裝工作成功完成之後，按一下 [裝置更新] 刀鋒視窗中的 [檢視工作] 連結來監視安裝。</span><span class="sxs-lookup"><span data-stu-id="1d28f-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate15m.png)

    <span data-ttu-id="1d28f-130">這會將您帶往 [安裝更新] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1d28f-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="1d28f-131">您可以在此處檢視有關工作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1d28f-131">You can view detailed information about the job here.</span></span>

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate16m.png)

9. <span data-ttu-id="1d28f-133">成功安裝更新之後，您會在 [裝置更新] 刀鋒視窗中看見關於此效果的訊息。</span><span class="sxs-lookup"><span data-stu-id="1d28f-133">After the updates are successfully installed, you see a message to this effect in the Device updates blade.</span></span> <span data-ttu-id="1d28f-134">軟體版本也會變更為 **10.0.10288.0**。</span><span class="sxs-lookup"><span data-stu-id="1d28f-134">The software version also changes to **10.0.10288.0**.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate17m.png)