<!--author=alkohli last changed: 01/18/17 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="ed41e-101">透過 Azure 入口網站安裝更新</span><span class="sxs-lookup"><span data-stu-id="ed41e-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="ed41e-102">移至您的 StorSimple 裝置管理員，然後選取 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ed41e-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="ed41e-103">從連接到您服務的裝置清單中，選取並按一下您想要更新的裝置。</span><span class="sxs-lookup"><span data-stu-id="ed41e-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate1m.png) 

2. <span data-ttu-id="ed41e-105">在 [設定] 刀鋒視窗中，按一下 [裝置更新]。</span><span class="sxs-lookup"><span data-stu-id="ed41e-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate2m.png)  

3. <span data-ttu-id="ed41e-107">如有軟體更新可用，您會看到一則訊息。</span><span class="sxs-lookup"><span data-stu-id="ed41e-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="ed41e-108">若要檢查更新，您也可以按一下 [掃描]。</span><span class="sxs-lookup"><span data-stu-id="ed41e-108">To check for updates, you can also click **Scan**.</span></span>

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate3m1.png)

    <span data-ttu-id="ed41e-110">當掃瞄啟動且成功完成時，系統將會通知您。</span><span class="sxs-lookup"><span data-stu-id="ed41e-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate5m.png)

4. <span data-ttu-id="ed41e-112">在掃描更新之後，按一下 [下載更新]。</span><span class="sxs-lookup"><span data-stu-id="ed41e-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate6m.png)

5. <span data-ttu-id="ed41e-114">在 [新的更新] 刀鋒視窗中，於下載完成之後檢閱資訊，您必須確認安裝。</span><span class="sxs-lookup"><span data-stu-id="ed41e-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="ed41e-115">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ed41e-115">Click **OK**.</span></span>

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate7m.png)

6. <span data-ttu-id="ed41e-117">當上傳啟動且成功完成時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="ed41e-117">You are notified when the upload starts and completes successfully.</span></span>

     ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate8m.png)

5. <span data-ttu-id="ed41e-119">在 [裝置更新] 刀鋒視窗中，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="ed41e-119">In the **Device updates** blade, click **Install**.</span></span>

     ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate11m1.png)   

6. <span data-ttu-id="ed41e-121">在 [新的更新] 刀鋒視窗中，系統會提醒您更新將造成運作中斷。</span><span class="sxs-lookup"><span data-stu-id="ed41e-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="ed41e-122">由於虛擬陣列是單一節點裝置，因此裝置會在更新之後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="ed41e-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="ed41e-123">這會中斷任何進行中的 IO。</span><span class="sxs-lookup"><span data-stu-id="ed41e-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="ed41e-124">按一下 [確定] 以安裝更新。</span><span class="sxs-lookup"><span data-stu-id="ed41e-124">Click **OK** to install the updates.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate12m.png) 

7. <span data-ttu-id="ed41e-126">安裝工作開始時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="ed41e-126">You are notified when the install job starts.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate13m.png)

8.  <span data-ttu-id="ed41e-128">在安裝工作成功完成之後，按一下 [裝置更新] 刀鋒視窗中的 [檢視工作] 連結來監視安裝。</span><span class="sxs-lookup"><span data-stu-id="ed41e-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate15m1.png)

    <span data-ttu-id="ed41e-130">這會將您帶往 [安裝更新] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ed41e-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="ed41e-131">您可以在此處檢視有關工作的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ed41e-131">You can view detailed information about the job here.</span></span>

    ![更新裝置](../includes/media/storsimple-virtual-array-install-update-via-portal-04/azupdate16m1.png)

9. <span data-ttu-id="ed41e-133">成功安裝更新之後，您會在 [裝置更新] 刀鋒視窗中看見關於此效果的訊息。</span><span class="sxs-lookup"><span data-stu-id="ed41e-133">After the updates are successfully installed, you see a message to this effect in the **Device updates** blade.</span></span> 