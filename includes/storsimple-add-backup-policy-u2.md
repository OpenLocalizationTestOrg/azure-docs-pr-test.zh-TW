<!--author=v-sharos last changed: 11/06/15-->

#### <a name="to-add-a-storsimple-backup-policy"></a><span data-ttu-id="9c169-101">若要新增 StorSimple 備份原則</span><span class="sxs-lookup"><span data-stu-id="9c169-101">To add a StorSimple backup policy</span></span>
1. <span data-ttu-id="9c169-102">在裝置的 [快速入門] 頁面上，按一下 [備份原則] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9c169-102">On the device **Quick Start** page, click the **Backup Policies** tab.</span></span> <span data-ttu-id="9c169-103">這會將您帶到 [ **備份原則** ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="9c169-103">This will take you to the **Backup Policies** page.</span></span>
2. <span data-ttu-id="9c169-104">在頁面底部，按一下 [新增]  ，以啟動 [新增備份原則精靈]。</span><span class="sxs-lookup"><span data-stu-id="9c169-104">At the bottom of the page, click **Add** to start the Add Backup Policy wizard.</span></span>
   
    ![新增備份原則 1](./media/storsimple-add-backup-policy-u2/AddBackupPolicy1.png)
3. <span data-ttu-id="9c169-106">在 [新增備份原則] 對話方塊的 [定義備份原則]，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9c169-106">In the **Add Backup Policy** dialog box, under **Define your backup policy**, do the following:</span></span>
   
   1. <span data-ttu-id="9c169-107">指定包含 3 到 150 個字元的備份原則名稱。</span><span class="sxs-lookup"><span data-stu-id="9c169-107">Specify a backup policy name that contains between 3 and 150 characters.</span></span>
   2. <span data-ttu-id="9c169-108">按一下核取方塊，將一或多個磁碟區指派給此備份原則。</span><span class="sxs-lookup"><span data-stu-id="9c169-108">Click the check box(es) to assign one or more volumes to this backup policy.</span></span> <span data-ttu-id="9c169-109">請注意，您無法選取使用不同雲端服務提供者的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9c169-109">Note that you cannot select volumes that use different cloud service providers.</span></span> <span data-ttu-id="9c169-110">如果您使用多個雲端服務提供者，清單將會依據您的第一個選擇，顯示只屬於該雲端服務提供者的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9c169-110">If you are using multiple cloud service providers, based on your first selection, the list will show volumes belonging to only that cloud service provider.</span></span> <span data-ttu-id="9c169-111">這可讓您群組磁碟區只屬於快照集中的一個雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="9c169-111">This will allow you to group volumes belonging to a single cloud service provider in a snapshot.</span></span>
   3. <span data-ttu-id="9c169-112">按一下箭頭圖示 </span><span class="sxs-lookup"><span data-stu-id="9c169-112">Click the arrow icon</span></span> ![箭號圖示](./media/storsimple-add-backup-policy-u2/HCS_ArrowIcon-include.png) <span data-ttu-id="9c169-114">以移至下一頁。</span><span class="sxs-lookup"><span data-stu-id="9c169-114">to go to the next page.</span></span>
      
      ![新增備份原則 2](./media/storsimple-add-backup-policy-u2/AddBackupPolicy2.png)
4. <span data-ttu-id="9c169-116">在 [定義排程] 下執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9c169-116">Under **Define a schedule**, do the following:</span></span>
   
   1. <span data-ttu-id="9c169-117">在 [備份的類型] 方塊中，從下拉式清單中選取 [雲端快照集] 或 [本機快照集]。</span><span class="sxs-lookup"><span data-stu-id="9c169-117">In the **Type of Backup** box, select **Cloud Snapshot** or **Local Snapshot** from the drop-down list.</span></span>
   2. <span data-ttu-id="9c169-118">指定備份的頻率 (指定數字，然後從下拉式清單中選擇 [天] 或 [週])。</span><span class="sxs-lookup"><span data-stu-id="9c169-118">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list).</span></span>
   3. <span data-ttu-id="9c169-119">輸入保留排程。</span><span class="sxs-lookup"><span data-stu-id="9c169-119">Enter a retention schedule.</span></span>
   4. <span data-ttu-id="9c169-120">輸入備份原則的開始日期與時間。</span><span class="sxs-lookup"><span data-stu-id="9c169-120">Enter a time and date for the backup policy to begin.</span></span>  
   5. <span data-ttu-id="9c169-121">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="9c169-121">Click the check icon</span></span> ![核取圖示](./media/storsimple-add-backup-policy-u2/HCS_CheckIcon-include.png) <span data-ttu-id="9c169-123">以儲存原則。</span><span class="sxs-lookup"><span data-stu-id="9c169-123">to save the policy.</span></span>

<span data-ttu-id="9c169-124">新加入的原則將會以表格式檢視顯示在 [ **備份原則** ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="9c169-124">The newly added policy will be displayed in the tabular view on the **Backup Policies** page.</span></span>

