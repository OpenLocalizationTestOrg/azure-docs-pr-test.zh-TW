<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a><span data-ttu-id="e3551-101">toocreate 磁碟區</span><span class="sxs-lookup"><span data-stu-id="e3551-101">toocreate a volume</span></span>
1. <span data-ttu-id="e3551-102">Hello 裝置上**快速入門**頁面上，按一下**加入磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="e3551-102">On hello device **Quick Start** page, click **Add a volume**.</span></span> <span data-ttu-id="e3551-103">這樣會啟動 hello 新增磁碟區精靈。</span><span class="sxs-lookup"><span data-stu-id="e3551-103">This starts hello Add a volume wizard.</span></span>
2. <span data-ttu-id="e3551-104">在 [hello 新增磁碟區精靈] 中，在**基本設定**，不要遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="e3551-104">In hello Add a volume wizard, under **Basic Settings**, do hello following:</span></span>
   
   1. <span data-ttu-id="e3551-105">輸入磁碟區的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="e3551-105">Supply a **Name** for your volume.</span></span>
   2. <span data-ttu-id="e3551-106">指定 hello**佈建的容量**以 GB 或 TB 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e3551-106">Specify hello **Provisioned Capacity** for your volume in GB or TB.</span></span> <span data-ttu-id="e3551-107">hello 磁碟區容量必須介於 1 GB 到 64 TB 之間的實體裝置。</span><span class="sxs-lookup"><span data-stu-id="e3551-107">hello volume capacity must be between 1 GB and 64 TB for a physical device.</span></span>
   3. <span data-ttu-id="e3551-108">在 hello 下拉式清單中，選取 hello**使用類型**磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e3551-108">On hello drop-down list, select hello **Usage Type** for your volume.</span></span> 
   4. <span data-ttu-id="e3551-109">如果您使用此磁碟區的封存資料，請選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e3551-109">If you are using this volume for archival data, select hello **Use this volume for less frequently accessed archival data** check box.</span></span> <span data-ttu-id="e3551-110">對於所有其他使用案例，只需選取 [ **階層式磁碟區**]。</span><span class="sxs-lookup"><span data-stu-id="e3551-110">For all other use cases, simply select **Tiered Volume**.</span></span> <span data-ttu-id="e3551-111">(階層式磁碟區之前稱為主要磁碟區)。</span><span class="sxs-lookup"><span data-stu-id="e3551-111">(Tiered volumes were formerly called primary volumes).</span></span>
      
        ![新增磁碟區](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. <span data-ttu-id="e3551-113">按一下 [hello] 箭號圖示</span><span class="sxs-lookup"><span data-stu-id="e3551-113">Click hello arrow icon</span></span> ![arrow-icon](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) <span data-ttu-id="e3551-115">toogo toohello 下一個頁面。</span><span class="sxs-lookup"><span data-stu-id="e3551-115">toogo toohello next page.</span></span>
3. <span data-ttu-id="e3551-116">在 hello**其他設定**對話方塊中，新增新的存取控制記錄 (ACR):</span><span class="sxs-lookup"><span data-stu-id="e3551-116">In hello **Additional Settings** dialog box, add a new access control record (ACR):</span></span>
   
   1. <span data-ttu-id="e3551-117">提供 ACR 的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="e3551-117">Supply a **Name** for your ACR.</span></span>
   2. <span data-ttu-id="e3551-118">在下**iSCSI 啟動器名稱**，提供 hello iSCSI 合格名稱 (IQN) 的 Windows 主機。</span><span class="sxs-lookup"><span data-stu-id="e3551-118">Under **iSCSI Initiator Name**, provide hello iSCSI Qualified Name (IQN) of your Windows host.</span></span> <span data-ttu-id="e3551-119">如果您沒有 hello IQN，請移至太[Get hello Windows Server 主機的 IQN](#get-the-iqn-of-a-windows-server-host)。</span><span class="sxs-lookup"><span data-stu-id="e3551-119">If you don't have hello IQN, go too[Get hello IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span></span>
   3. <span data-ttu-id="e3551-120">我們建議您藉由選取 hello 啟用預設備份**啟用此磁碟區的預設備份**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e3551-120">We recommend that you enable a default backup by selecting hello **Enable a default backup for this volume** check box.</span></span> <span data-ttu-id="e3551-121">hello 預設備份會建立原則，在 22:30 （裝置時間） 的每一天執行，並建立此磁碟區的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="e3551-121">hello default backup will create a policy that executes at 22:30 each day (device time) and creates a cloud snapshot of this volume.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e3551-122">Hello 備份在此處啟用後，即無法回復。</span><span class="sxs-lookup"><span data-stu-id="e3551-122">After hello backup is enabled here, it cannot be reverted.</span></span> <span data-ttu-id="e3551-123">您將需要 tooedit hello 磁碟區 toomodify 這項設定。</span><span class="sxs-lookup"><span data-stu-id="e3551-123">You will need tooedit hello volume toomodify this setting.</span></span>
      > 
      > 
      
        ![新增磁碟區](./media/storsimple-create-volume/AddVolume2-include.png)
4. <span data-ttu-id="e3551-125">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="e3551-125">Click hello check icon</span></span> ![核取圖示](./media/storsimple-create-volume/HCS_CheckIcon-include.png)<span data-ttu-id="e3551-127">.</span><span class="sxs-lookup"><span data-stu-id="e3551-127">.</span></span> <span data-ttu-id="e3551-128">將指定的 hello 與建立磁碟區設定。</span><span class="sxs-lookup"><span data-stu-id="e3551-128">A volume will be created with hello specified settings.</span></span>

<span data-ttu-id="e3551-129">![提供的影片](./media/storsimple-create-volume/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="e3551-129">![Video available](./media/storsimple-create-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="e3551-130">toowatch 的視訊示範，如何 toocreate StorSimple 磁碟區，按一下[這裡](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/)。</span><span class="sxs-lookup"><span data-stu-id="e3551-130">toowatch a video that demonstrates how toocreate a StorSimple volume, click [here](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).</span></span>

