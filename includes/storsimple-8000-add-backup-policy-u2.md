<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-add-a-storsimple-backup-policy"></a><span data-ttu-id="8c954-101">若要新增 StorSimple 備份原則</span><span class="sxs-lookup"><span data-stu-id="8c954-101">To add a StorSimple backup policy</span></span>

1. <span data-ttu-id="8c954-102">請移至 StorSimple 裝置，並按一下 [備份原則]。</span><span class="sxs-lookup"><span data-stu-id="8c954-102">Go to your StorSimple device and click **Backup policy**.</span></span>

2. <span data-ttu-id="8c954-103">在 [備份原則] 刀鋒視窗中，從命令列按一下 [+ 新增原則]。</span><span class="sxs-lookup"><span data-stu-id="8c954-103">In the **Backup policy** blade, click **+ Add policy** from the command bar.</span></span>
   
    ![新增備份原則](./media/storsimple-8000-add-backup-policy-u2/addbupol1.png)

3. <span data-ttu-id="8c954-105">在 [建立備份原則] 刀鋒視窗中，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="8c954-105">In the **Create backup policy** blade, do the following steps:</span></span>
   
   1. <span data-ttu-id="8c954-106">[選取裝置] 會根據您所選取的裝置自動填入。</span><span class="sxs-lookup"><span data-stu-id="8c954-106">**Select device** is automatically populated based on the device you selected.</span></span>
   
   2. <span data-ttu-id="8c954-107">指定包含 3 到 150 個字元的備份**原則名稱**。</span><span class="sxs-lookup"><span data-stu-id="8c954-107">Specify a backup **Policy name** that contains between 3 and 150 characters.</span></span> <span data-ttu-id="8c954-108">建立原則之後，您就無法重新命名原則。</span><span class="sxs-lookup"><span data-stu-id="8c954-108">Once the policy is created, you cannot rename the policy.</span></span>
       
   3. <span data-ttu-id="8c954-109">若要將磁碟區指派給此備份原則，請選取 [新增磁碟區]，然後從表格式的磁碟區清單中按一下核取方塊，將一或多個磁碟區指派給此備份原則。</span><span class="sxs-lookup"><span data-stu-id="8c954-109">To assign volumes to this backup policy, select **Add volumes** and then from the tabular listing of volumes, click the check box(es) to assign one or more volumes to this backup policy.</span></span>

       ![新增備份原則](./media/storsimple-8000-add-backup-policy-u2/addbupol2.png)

   4. <span data-ttu-id="8c954-111">若要定義此備份原則的排程，請按一下 [第一個排程]，然後修改下列參數︰</span><span class="sxs-lookup"><span data-stu-id="8c954-111">To define a schedule for this backup policy, click **First schedule** and then modify the following parameters:</span></span>

       ![新增備份原則](./media/storsimple-8000-add-backup-policy-u2/addbupol3.png)

       1. <span data-ttu-id="8c954-113">針對 [快照集類型]，請選取 [雲端] 或 [本機]。</span><span class="sxs-lookup"><span data-stu-id="8c954-113">For **Snapshot type**, select **Cloud** or **Local**.</span></span>

       2. <span data-ttu-id="8c954-114">指定備份的頻率 (指定數字)，然後從下拉式清單中選擇 [天] 或 [週] 。</span><span class="sxs-lookup"><span data-stu-id="8c954-114">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list.</span></span>

       3. <span data-ttu-id="8c954-115">輸入保留排程。</span><span class="sxs-lookup"><span data-stu-id="8c954-115">Enter a retention schedule.</span></span>

       4. <span data-ttu-id="8c954-116">輸入備份原則的開始日期與時間。</span><span class="sxs-lookup"><span data-stu-id="8c954-116">Enter a time and date for the backup policy to begin.</span></span>

       5. <span data-ttu-id="8c954-117">按一下 [確定] 可定義排程。</span><span class="sxs-lookup"><span data-stu-id="8c954-117">Click **OK** to define the schedule.</span></span>

   5. <span data-ttu-id="8c954-118">按一下 [建立] 可建立備份原則。</span><span class="sxs-lookup"><span data-stu-id="8c954-118">Click **Create** to create a backup policy.</span></span>

       ![新增備份原則](./media/storsimple-8000-add-backup-policy-u2/addbupol4.png)
   
   6. <span data-ttu-id="8c954-120">建立備份原則時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="8c954-120">You are notified when the backup policy is created.</span></span> <span data-ttu-id="8c954-121">新增的原則會以表格式檢視顯示在 [備份原則] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8c954-121">The newly added policy is displayed in the tabular view on the **Backup Policy** blade.</span></span>

       ![新增備份原則](./media/storsimple-8000-add-backup-policy-u2/addbupol7.png)

