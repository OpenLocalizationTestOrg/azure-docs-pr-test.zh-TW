
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="46262-101">toocreate 手動備份</span><span class="sxs-lookup"><span data-stu-id="46262-101">toocreate a manual backup</span></span>

1. <span data-ttu-id="46262-102">在 tooyour StorSimple 裝置管理員服務的 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="46262-102">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="46262-103">從 hello 表格清單中的裝置，選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="46262-103">From hello tabular listing of devices, select your device.</span></span> <span data-ttu-id="46262-104">跳過**設定 > 管理 > 的備份原則**。</span><span class="sxs-lookup"><span data-stu-id="46262-104">Go too**Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="46262-105">hello**的備份原則**刀鋒視窗會列出所有的 hello 備份原則以表格格式，包括要 tooback 的 hello 磁碟區的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="46262-105">hello **Backup policies** blade lists all hello backup policies in a tabular format, including hello policy for hello volume that you want tooback up.</span></span> <span data-ttu-id="46262-106">選取您想 tooback hello 磁碟區和以滑鼠右鍵按一下 tooinvoke hello 內容功能表相關聯的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="46262-106">Select hello policy associated with hello volume you want tooback up and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="46262-107">從 hello 下拉式清單中，選取**立即備份**。</span><span class="sxs-lookup"><span data-stu-id="46262-107">From hello dropdown list, select **Back up now**.</span></span>

    ![建立手動備份](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="46262-109">在 hello**立即備份**刀鋒視窗中，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="46262-109">In hello **Back up now** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="46262-110">選擇適當的 hello**快照類型**hello 下拉式清單中：**本機**快照集或**雲端**快照集。</span><span class="sxs-lookup"><span data-stu-id="46262-110">Choose hello appropriate **Snapshot type** from hello dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="46262-111">選取本機快照集可快速備份或還原，選取雲端快照集則可進行資料復原。</span><span class="sxs-lookup"><span data-stu-id="46262-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![建立手動備份](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="46262-113">按一下**確定**toostart 作業 toocreate 快照集。</span><span class="sxs-lookup"><span data-stu-id="46262-113">Click **OK** toostart a job toocreate a snapshot.</span></span> <span data-ttu-id="46262-114">已成功建立 hello 作業之後，您會看到在 hello hello 頁面最上方的通知。</span><span class="sxs-lookup"><span data-stu-id="46262-114">You will see a notification at hello top of hello page after hello job is successfully created.</span></span>

        ![建立手動備份](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="46262-116">toomonitor hello 作業中，按一下 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="46262-116">toomonitor hello job, click hello notification.</span></span> <span data-ttu-id="46262-117">這會帶您 toohello**作業**刀鋒視窗中，您可以檢視 hello 工作進度。</span><span class="sxs-lookup"><span data-stu-id="46262-117">This takes you toohello **Jobs** blade where you can view hello job progress.</span></span>


5. <span data-ttu-id="46262-118">Hello 備份工作完成之後，請繼續 toohello**備份類別目錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="46262-118">After hello backup job is finished, go toohello **Backup catalog** tab.</span></span>

6. <span data-ttu-id="46262-119">設定 hello 篩選選取項目 toohello 適當的裝置，備份原則，以及時間範圍。</span><span class="sxs-lookup"><span data-stu-id="46262-119">Set hello filter selections toohello appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="46262-120">備份組會顯示 hello 目錄中的 hello 清單應會顯示 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="46262-120">hello backup should appear in hello list of backup sets that is displayed in hello catalog.</span></span>

