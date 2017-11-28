<!--author=SharS last changed: 9/15/15-->

#### <a name="to-create-a-custom-backup-policy"></a><span data-ttu-id="a420a-101">若要建立自訂備份原則</span><span class="sxs-lookup"><span data-stu-id="a420a-101">To create a custom backup policy</span></span>
1. <span data-ttu-id="a420a-102">在 [裝置] 頁面上，按一下 [備份原則]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a420a-102">On the **Devices** page, click **Backup Policies** and then click **Add**.</span></span>
2. <span data-ttu-id="a420a-103">在 [新增備份原則] 對話方塊中，[定義備份原則] 之下：</span><span class="sxs-lookup"><span data-stu-id="a420a-103">In the **Add a backup policy** dialog box, under **Define your backup policy**:</span></span>
   
   1. <span data-ttu-id="a420a-104">指定備份原則名稱。</span><span class="sxs-lookup"><span data-stu-id="a420a-104">Specify a backup policy name.</span></span>
   2. <span data-ttu-id="a420a-105">選取要加入至這個原則的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a420a-105">Select the volumes to be added to this policy.</span></span> <span data-ttu-id="a420a-106">您可以從下拉式清單選擇磁碟區來加入多個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a420a-106">You can choose to add multiple volumes by selecting them from the drop-down list.</span></span>
   3. <span data-ttu-id="a420a-107">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="a420a-107">Click the check icon</span></span> ![核取圖示](./media/storsimple-add-backup-policy/HCS_CheckIcon-include.png)<span data-ttu-id="a420a-109">。</span><span class="sxs-lookup"><span data-stu-id="a420a-109">.</span></span>
      
      <span data-ttu-id="a420a-110">在成功建立原則之後，系統將會通知您。</span><span class="sxs-lookup"><span data-stu-id="a420a-110">You will be notified after the policy is created successfully.</span></span> <span data-ttu-id="a420a-111">備份原則頁面會同時更新，以顯示新建立的原則。</span><span class="sxs-lookup"><span data-stu-id="a420a-111">The backup policies page will also be updated to show the newly created policy.</span></span>
3. <span data-ttu-id="a420a-112">按一下原則名稱 (第一個資料行) 以深入了解您剛剛建立之原則的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a420a-112">Click the policy name (first column) to drill down into details of the policy you just created.</span></span>
4. <span data-ttu-id="a420a-113">按一下 [ **管理排程**]。</span><span class="sxs-lookup"><span data-stu-id="a420a-113">Click **manage schedules**.</span></span>
5. <span data-ttu-id="a420a-114">在 [ **管理排程** ] 對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="a420a-114">In the **Manage Schedules** dialog box:</span></span>
   
   1. <span data-ttu-id="a420a-115">選取 [ **新建** ] 以新增其他排程。</span><span class="sxs-lookup"><span data-stu-id="a420a-115">Select **Create new** to add another schedule.</span></span>
   2. <span data-ttu-id="a420a-116">從下拉式清單中。選擇備份類型為 [本機] 或 [雲端] 快照集。</span><span class="sxs-lookup"><span data-stu-id="a420a-116">From the drop-down list, choose the backup type as **local** or **cloud** snapshot.</span></span>
   3. <span data-ttu-id="a420a-117">指定備份頻率 (以分鐘、小時、天或週為單位)。</span><span class="sxs-lookup"><span data-stu-id="a420a-117">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
   4. <span data-ttu-id="a420a-118">選取保留期。</span><span class="sxs-lookup"><span data-stu-id="a420a-118">Select a retention.</span></span> <span data-ttu-id="a420a-119">保留選項會根據備份頻率而定。</span><span class="sxs-lookup"><span data-stu-id="a420a-119">The retention choices depend on the backup frequency.</span></span>
   5. <span data-ttu-id="a420a-120">選取原則的開始時間和日期。</span><span class="sxs-lookup"><span data-stu-id="a420a-120">Select the starting time and date for the policy.</span></span>
   6. <span data-ttu-id="a420a-121">選取核取方塊以啟用原則。</span><span class="sxs-lookup"><span data-stu-id="a420a-121">Select the check box to enable the policy.</span></span>
6. <span data-ttu-id="a420a-122">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="a420a-122">Click the check icon</span></span> ![核取圖示](./media/storsimple-add-backup-policy/HCS_CheckIcon-include.png) <span data-ttu-id="a420a-124">以完成。</span><span class="sxs-lookup"><span data-stu-id="a420a-124">to finish.</span></span>
7. <span data-ttu-id="a420a-125">您將返回原則詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a420a-125">You will return to the policy details.</span></span> <span data-ttu-id="a420a-126">按一下 [ **儲存** ] 儲存您對此原則所做的變更。</span><span class="sxs-lookup"><span data-stu-id="a420a-126">Click **Save** to save the changes you made to this policy.</span></span> <span data-ttu-id="a420a-127">當原則已儲存時將會通知您。</span><span class="sxs-lookup"><span data-stu-id="a420a-127">You will be notified when the policy has been saved.</span></span>
8. <span data-ttu-id="a420a-128">瀏覽回 [ **備份原則** ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="a420a-128">Navigate back to the **Backup Policies** page.</span></span> <span data-ttu-id="a420a-129">備份原則的表格式清單將會更新，以顯示已修改的原則。</span><span class="sxs-lookup"><span data-stu-id="a420a-129">The tabular listing of the backup policies will be updated to display the modified policy.</span></span>
   
    ![自訂備份原則](./media/storsimple-create-custom-backup-policy/HCS_CustomBackupPolicyM-include.png)<span data-ttu-id="a420a-131">。</span><span class="sxs-lookup"><span data-stu-id="a420a-131">.</span></span>

