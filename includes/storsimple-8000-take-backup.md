<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="e4704-101">tootake 備份</span><span class="sxs-lookup"><span data-stu-id="e4704-101">tootake a backup</span></span>

1. <span data-ttu-id="e4704-102">移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="e4704-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="e4704-103">從 hello 表格清單中的裝置，選取並按一下您的裝置，然後按一下**所有設定**。</span><span class="sxs-lookup"><span data-stu-id="e4704-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="e4704-104">在 hello**設定**刀鋒視窗中，跳過**設定 > 管理 > 備份原則**。</span><span class="sxs-lookup"><span data-stu-id="e4704-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="e4704-106">在 hello**備份原則**刀鋒視窗中，按一下  **+ 加入原則**。</span><span class="sxs-lookup"><span data-stu-id="e4704-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="e4704-108">在 hello**建立備份原則**刀鋒視窗中，提供包含 3 到 150 個字元，備份原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="e4704-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="e4704-109">選取備份的 hello 磁碟區 toobe。</span><span class="sxs-lookup"><span data-stu-id="e4704-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="e4704-110">如果您選取多個磁碟區，這些磁碟區會分組在一起 toocreate 損毀一致備份。</span><span class="sxs-lookup"><span data-stu-id="e4704-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="e4704-112">在 [新增第一個排程] 刀鋒視窗中︰</span><span class="sxs-lookup"><span data-stu-id="e4704-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="e4704-113">選取備份 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="e4704-113">Select hello type of backup.</span></span> <span data-ttu-id="e4704-114">針對更快速的還原，請選取 [本機] 快照集。</span><span class="sxs-lookup"><span data-stu-id="e4704-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="e4704-115">針對資料復原，請選取 [雲端] 快照集。</span><span class="sxs-lookup"><span data-stu-id="e4704-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="e4704-116">指定分鐘、 小時、 天或週中的 hello 備份頻率。</span><span class="sxs-lookup"><span data-stu-id="e4704-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="e4704-117">選取保留時間。</span><span class="sxs-lookup"><span data-stu-id="e4704-117">Select a retention time.</span></span> <span data-ttu-id="e4704-118">hello 保留選項取決於 hello 備份頻率。</span><span class="sxs-lookup"><span data-stu-id="e4704-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="e4704-119">比方說，每日原則的 hello 保留可以指定在數週，而每月原則的保留是以月為單位。</span><span class="sxs-lookup"><span data-stu-id="e4704-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="e4704-120">選取 hello 啟動 hello 備份原則的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="e4704-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="e4704-121">按一下**確定**toocreate hello 備份原則。</span><span class="sxs-lookup"><span data-stu-id="e4704-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="e4704-123">按一下**建立**toostart hello 建立備份原則。</span><span class="sxs-lookup"><span data-stu-id="e4704-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="e4704-124">已成功建立 hello 備份原則時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="e4704-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="e4704-125">hello 備份原則清單也會更新。</span><span class="sxs-lookup"><span data-stu-id="e4704-125">hello list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="e4704-127">您現在擁有的備份原則會建立磁碟區資料的排程備份。</span><span class="sxs-lookup"><span data-stu-id="e4704-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




