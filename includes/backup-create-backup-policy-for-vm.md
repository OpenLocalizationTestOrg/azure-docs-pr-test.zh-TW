## <a name="defining-a-backup-policy"></a><span data-ttu-id="556a0-101">定義備份原則</span><span class="sxs-lookup"><span data-stu-id="556a0-101">Defining a backup policy</span></span>
<span data-ttu-id="556a0-102">備份原則會定義當拍攝 hello 資料快照集時，與這些快照集的保留時間長度的矩陣。</span><span class="sxs-lookup"><span data-stu-id="556a0-102">A backup policy defines a matrix of when hello data snapshots are taken, and how long those snapshots are retained.</span></span> <span data-ttu-id="556a0-103">在定義 VM 的備份原則時，您可以「一天一次」 地觸發備份作業。</span><span class="sxs-lookup"><span data-stu-id="556a0-103">When defining a policy for backing up a VM, you can trigger a backup job *once a day*.</span></span> <span data-ttu-id="556a0-104">當您建立新的原則時，它是套用的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="556a0-104">When you create a new policy, it is applied toohello vault.</span></span> <span data-ttu-id="556a0-105">hello 備份原則介面看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="556a0-105">hello backup policy interface looks like this:</span></span>

![備份原則](./media/backup-create-policy-for-vms/backup-policy.png)

<span data-ttu-id="556a0-107">toocreate 原則：</span><span class="sxs-lookup"><span data-stu-id="556a0-107">toocreate a policy:</span></span>

1. <span data-ttu-id="556a0-108">輸入的名稱 hello**原則名稱**。</span><span class="sxs-lookup"><span data-stu-id="556a0-108">Enter a name for hello **Policy name**.</span></span>
2. <span data-ttu-id="556a0-109">資料快照可依 [每日] 或 [每週] 間隔來擷取。</span><span class="sxs-lookup"><span data-stu-id="556a0-109">Snapshots of your data can be taken at Daily or Weekly intervals.</span></span> <span data-ttu-id="556a0-110">使用 hello**備份頻率**下拉式功能表 toochoose 是否資料拍攝快照時，每日或每週。</span><span class="sxs-lookup"><span data-stu-id="556a0-110">Use hello **Backup Frequency** drop-down menu toochoose whether data snapshots are taken Daily or Weekly.</span></span>
   
   * <span data-ttu-id="556a0-111">如果您選擇每日間隔，用於 hello 快照 hello 反白顯示控制項 tooselect hello hello 一天的時間。</span><span class="sxs-lookup"><span data-stu-id="556a0-111">If you choose a Daily interval, use hello highlighted control tooselect hello time of hello day for hello snapshot.</span></span> <span data-ttu-id="556a0-112">toochange hello 小時的時間，取消選取 hello 小時，然後選取 hello 新小時。</span><span class="sxs-lookup"><span data-stu-id="556a0-112">toochange hello hour, de-select hello hour, and select hello new hour.</span></span>
     
     ![每日備份原則](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * <span data-ttu-id="556a0-114">如果您選擇以週為間隔，使用 hello 反白顯示的控制項，請 tooselect hello 天 hello 週和日 tootake hello 快照集的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="556a0-114">If you choose a Weekly interval, use hello highlighted controls tooselect hello day(s) of hello week, and hello time of day tootake hello snapshot.</span></span> <span data-ttu-id="556a0-115">在 hello 天功能表中，選取一或多個星期幾。</span><span class="sxs-lookup"><span data-stu-id="556a0-115">In hello day menu, select one or multiple days.</span></span> <span data-ttu-id="556a0-116">在 hello 小時功能表上，選取 一小時。</span><span class="sxs-lookup"><span data-stu-id="556a0-116">In hello hour menu, select one hour.</span></span> <span data-ttu-id="556a0-117">toochange hello 小時的時間，取消選取 hello 選的小時，然後選取 hello 新小時。</span><span class="sxs-lookup"><span data-stu-id="556a0-117">toochange hello hour, de-select hello selected hour, and select hello new hour.</span></span>
     
     ![每週備份原則](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. <span data-ttu-id="556a0-119">根據預設，會選取所有 [保留範圍]  選項。</span><span class="sxs-lookup"><span data-stu-id="556a0-119">By default, all **Retention Range** options are selected.</span></span> <span data-ttu-id="556a0-120">取消選取任何您不想 toouse 的保留範圍限制。</span><span class="sxs-lookup"><span data-stu-id="556a0-120">Uncheck any retention range limit you do not want toouse.</span></span> <span data-ttu-id="556a0-121">然後，指定 hello interval(s) toouse。</span><span class="sxs-lookup"><span data-stu-id="556a0-121">Then, specify hello interval(s) toouse.</span></span>
   
    <span data-ttu-id="556a0-122">每月和每年的保留範圍可讓您根據每週或每日增量 toospecify hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="556a0-122">Monthly and Yearly retention ranges allow you toospecify hello snapshots based on a weekly or daily increment.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="556a0-123">在保護 VM 時，備份作業會每天執行一次。</span><span class="sxs-lookup"><span data-stu-id="556a0-123">When protecting a VM, a backup job runs once a day.</span></span> <span data-ttu-id="556a0-124">當執行 hello 備份是 hello 相同的每個保留範圍的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="556a0-124">hello time when hello backup runs is hello same for each retention range.</span></span>
   > 
   > 
4. <span data-ttu-id="556a0-125">設定後 hello 原則的所有選項，請在 hello hello 刀鋒視窗頂端按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="556a0-125">After setting all options for hello policy, at hello top of hello blade click **Save**.</span></span>
   
    <span data-ttu-id="556a0-126">hello 新原則會立即套用的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="556a0-126">hello new policy is immediately applied toohello vault.</span></span>

