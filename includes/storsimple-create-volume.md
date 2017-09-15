<!--author=SharS last changed: 02/04/2016-->

#### <a name="to-create-a-volume"></a><span data-ttu-id="1f359-101">建立磁碟區</span><span class="sxs-lookup"><span data-stu-id="1f359-101">To create a volume</span></span>
1. <span data-ttu-id="1f359-102">在裝置的 [快速入門] 頁面上，按一下 [新增磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="1f359-102">On the device **Quick Start** page, click **Add a volume**.</span></span> <span data-ttu-id="1f359-103">這樣會啟動 [新增磁碟區] 精靈。</span><span class="sxs-lookup"><span data-stu-id="1f359-103">This starts the Add a volume wizard.</span></span>
2. <span data-ttu-id="1f359-104">在 [新增磁碟區精靈] 的 [基本設定] 下，執行列動作：</span><span class="sxs-lookup"><span data-stu-id="1f359-104">In the Add a volume wizard, under **Basic Settings**, do the following:</span></span>
   
   1. <span data-ttu-id="1f359-105">輸入磁碟區的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="1f359-105">Supply a **Name** for your volume.</span></span>
   2. <span data-ttu-id="1f359-106">為磁碟區指定 [佈建的容量]  (GB 或 TB)。</span><span class="sxs-lookup"><span data-stu-id="1f359-106">Specify the **Provisioned Capacity** for your volume in GB or TB.</span></span> <span data-ttu-id="1f359-107">實體裝置的磁碟區容量必須介於 1 GB 到 64 TB 之間。</span><span class="sxs-lookup"><span data-stu-id="1f359-107">The volume capacity must be between 1 GB and 64 TB for a physical device.</span></span>
   3. <span data-ttu-id="1f359-108">在下拉式清單中，為磁碟區選取 [使用類型]  。</span><span class="sxs-lookup"><span data-stu-id="1f359-108">On the drop-down list, select the **Usage Type** for your volume.</span></span> 
   4. <span data-ttu-id="1f359-109">如果您將此磁碟區用於封存資料，請選取 [ **將此磁碟區用於較不常存取的封存資料** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1f359-109">If you are using this volume for archival data, select the **Use this volume for less frequently accessed archival data** check box.</span></span> <span data-ttu-id="1f359-110">對於所有其他使用案例，只需選取 [ **階層式磁碟區**]。</span><span class="sxs-lookup"><span data-stu-id="1f359-110">For all other use cases, simply select **Tiered Volume**.</span></span> <span data-ttu-id="1f359-111">(階層式磁碟區之前稱為主要磁碟區)。</span><span class="sxs-lookup"><span data-stu-id="1f359-111">(Tiered volumes were formerly called primary volumes).</span></span>
      
        ![新增磁碟區](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. <span data-ttu-id="1f359-113">按一下箭頭圖示 </span><span class="sxs-lookup"><span data-stu-id="1f359-113">Click the arrow icon</span></span> ![arrow-icon](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) <span data-ttu-id="1f359-115">以移至下一頁。</span><span class="sxs-lookup"><span data-stu-id="1f359-115">to go to the next page.</span></span>
3. <span data-ttu-id="1f359-116">在 [其他設定]  對話方塊中，加入新的存取控制記錄 (ACR)：</span><span class="sxs-lookup"><span data-stu-id="1f359-116">In the **Additional Settings** dialog box, add a new access control record (ACR):</span></span>
   
   1. <span data-ttu-id="1f359-117">提供 ACR 的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="1f359-117">Supply a **Name** for your ACR.</span></span>
   2. <span data-ttu-id="1f359-118">在 [iSCSI 啟動器名稱] 下方，提供 Windows 主機的 iSCSI 完整格式名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="1f359-118">Under **iSCSI Initiator Name**, provide the iSCSI Qualified Name (IQN) of your Windows host.</span></span> <span data-ttu-id="1f359-119">如果沒有 IQN，請移至 [取得 Windows Server 主機的 IQN] [](#get-the-iqn-of-a-windows-server-host)。</span><span class="sxs-lookup"><span data-stu-id="1f359-119">If you don't have the IQN, go to [Get the IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span></span>
   3. <span data-ttu-id="1f359-120">建議選取 [ **啟用此磁碟區的預設備份** ] 核取方塊啟用預設備份。</span><span class="sxs-lookup"><span data-stu-id="1f359-120">We recommend that you enable a default backup by selecting the **Enable a default backup for this volume** check box.</span></span> <span data-ttu-id="1f359-121">預設備份將會建立原則，在每天的 22:30 (裝置時間) 執行，並建立此磁碟區的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="1f359-121">The default backup will create a policy that executes at 22:30 each day (device time) and creates a cloud snapshot of this volume.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="1f359-122">在此處啟用備份之後，就無法加以還原。</span><span class="sxs-lookup"><span data-stu-id="1f359-122">After the backup is enabled here, it cannot be reverted.</span></span> <span data-ttu-id="1f359-123">您必須編輯磁碟區，才能修改此設定。</span><span class="sxs-lookup"><span data-stu-id="1f359-123">You will need to edit the volume to modify this setting.</span></span>
      > 
      > 
      
        ![新增磁碟區](./media/storsimple-create-volume/AddVolume2-include.png)
4. <span data-ttu-id="1f359-125">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="1f359-125">Click the check icon</span></span> ![核取圖示](./media/storsimple-create-volume/HCS_CheckIcon-include.png)<span data-ttu-id="1f359-127">。</span><span class="sxs-lookup"><span data-stu-id="1f359-127">.</span></span> <span data-ttu-id="1f359-128">使用指定的設定來建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1f359-128">A volume will be created with the specified settings.</span></span>

<span data-ttu-id="1f359-129">![提供的影片](./media/storsimple-create-volume/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="1f359-129">![Video available](./media/storsimple-create-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="1f359-130">若要觀看影片示範如何建立 StorSimple 磁碟區，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/)。</span><span class="sxs-lookup"><span data-stu-id="1f359-130">To watch a video that demonstrates how to create a StorSimple volume, click [here](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).</span></span>

