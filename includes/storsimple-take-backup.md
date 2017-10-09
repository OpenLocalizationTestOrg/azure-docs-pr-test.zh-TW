<!--author=alkohli last changed: 9/17/15-->

### <a name="tootake-a-backup"></a><span data-ttu-id="a765e-101">tootake 備份</span><span class="sxs-lookup"><span data-stu-id="a765e-101">tootake a backup</span></span>
1. <span data-ttu-id="a765e-102">Hello 裝置上**快速入門**頁面上，按一下**新增備份原則**。</span><span class="sxs-lookup"><span data-stu-id="a765e-102">On hello device **Quick Start** page, click **Add a backup policy**.</span></span> <span data-ttu-id="a765e-103">這樣會啟動 hello 新增備份原則精靈。</span><span class="sxs-lookup"><span data-stu-id="a765e-103">This will start hello Add Backup Policy wizard.</span></span> 
2. <span data-ttu-id="a765e-104">在 hello**定義備份原則**頁面：</span><span class="sxs-lookup"><span data-stu-id="a765e-104">On hello **Define your backup policy** page:</span></span>
   
   1. <span data-ttu-id="a765e-105">為備份原則提供包含 3 到 150 個字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="a765e-105">Supply a name that contains between 3 and 150 characters for your backup policy.</span></span>
   2. <span data-ttu-id="a765e-106">選取備份的 hello 磁碟區 toobe。</span><span class="sxs-lookup"><span data-stu-id="a765e-106">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="a765e-107">如果您選取多個磁碟區，這些磁碟區將會分組在一起 toocreate 損毀一致備份。</span><span class="sxs-lookup"><span data-stu-id="a765e-107">If you select more than one volume, these volumes will be grouped together toocreate a crash-consistent backup.</span></span>
   3. <span data-ttu-id="a765e-108">按一下 [hello] 箭號圖示</span><span class="sxs-lookup"><span data-stu-id="a765e-108">Click hello arrow icon</span></span> ![arrow-icon](./media/storsimple-take-backup/HCS_ArrowIcon-include.png)<span data-ttu-id="a765e-110">。</span><span class="sxs-lookup"><span data-stu-id="a765e-110">.</span></span> 
      
      ![Add-backup-policy](./media/storsimple-take-backup/HCS_AddBackupPolicyWizard1M-include.png)
3. <span data-ttu-id="a765e-112">在 hello**定義排程**頁面：</span><span class="sxs-lookup"><span data-stu-id="a765e-112">On hello **Define a schedule** page:</span></span>
   
   1. <span data-ttu-id="a765e-113">從 hello 下拉式清單中選取備份 hello 的類型。</span><span class="sxs-lookup"><span data-stu-id="a765e-113">Select hello type of backup from hello drop-down list.</span></span> <span data-ttu-id="a765e-114">針對更快速的還原，選取 [本機快照] 。</span><span class="sxs-lookup"><span data-stu-id="a765e-114">For faster restores, select **Local Snapshot**.</span></span> <span data-ttu-id="a765e-115">針對資料恢復功能，選取 [雲端快照] 。</span><span class="sxs-lookup"><span data-stu-id="a765e-115">For data resiliency, select **Cloud Snapshot**.</span></span>
   2. <span data-ttu-id="a765e-116">指定分鐘、 小時、 天或週中的 hello 備份頻率。</span><span class="sxs-lookup"><span data-stu-id="a765e-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
   3. <span data-ttu-id="a765e-117">選取保留時間。</span><span class="sxs-lookup"><span data-stu-id="a765e-117">Select a retention time.</span></span> <span data-ttu-id="a765e-118">hello 保留選項取決於 hello 備份頻率。</span><span class="sxs-lookup"><span data-stu-id="a765e-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="a765e-119">比方說，每日原則的 hello 保留可以指定在數週，而每月原則的保留是以月為單位。</span><span class="sxs-lookup"><span data-stu-id="a765e-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
   4. <span data-ttu-id="a765e-120">選取 hello 啟動 hello 備份原則的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="a765e-120">Select hello starting time and date for hello backup policy.</span></span>
   5. <span data-ttu-id="a765e-121">選取 hello**啟用**核取方塊 tooenable hello 備份原則。</span><span class="sxs-lookup"><span data-stu-id="a765e-121">Select hello **Enable** check box tooenable hello backup policy.</span></span> 
   6. <span data-ttu-id="a765e-122">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="a765e-122">Click hello check icon</span></span> ![核取圖示](./media/storsimple-take-backup/HCS_CheckIcon-include.png) <span data-ttu-id="a765e-124">toosave hello 原則。</span><span class="sxs-lookup"><span data-stu-id="a765e-124">toosave hello policy.</span></span>
      
      ![Add-backup-policy](./media/storsimple-take-backup/HCS_AddBackupPolicyWizard2M-include.png)
      
      <span data-ttu-id="a765e-126">您現在擁有的備份原則將會建立磁碟區資料的排程備份。</span><span class="sxs-lookup"><span data-stu-id="a765e-126">You now have a backup policy that will create scheduled backups of your volume data.</span></span>

<span data-ttu-id="a765e-127">您已完成 hello 裝置組態。</span><span class="sxs-lookup"><span data-stu-id="a765e-127">You have completed hello device configuration.</span></span> 

<span data-ttu-id="a765e-128">![提供的影片](./media/storsimple-take-backup/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="a765e-128">![Video available](./media/storsimple-take-backup/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="a765e-129">toowatch 的視訊示範，如何 tootake StorSimple 備份時，按一下[這裡](https://azure.microsoft.com/documentation/videos/take-a-storsimple-backup/)。</span><span class="sxs-lookup"><span data-stu-id="a765e-129">toowatch a video that demonstrates how tootake a StorSimple backup, click [here](https://azure.microsoft.com/documentation/videos/take-a-storsimple-backup/).</span></span>

