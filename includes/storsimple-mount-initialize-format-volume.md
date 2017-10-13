<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a><span data-ttu-id="66c66-101">toomount、 初始化及格式化磁碟區</span><span class="sxs-lookup"><span data-stu-id="66c66-101">toomount, initialize, and format a volume</span></span>
1. <span data-ttu-id="66c66-102">啟動 hello Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="66c66-102">Start hello Microsoft iSCSI initiator.</span></span>
2. <span data-ttu-id="66c66-103">在 hello **iSCSI 啟動器屬性**視窗的 hello**探索**索引標籤上，按一下 **探索入口網站**。</span><span class="sxs-lookup"><span data-stu-id="66c66-103">In hello **iSCSI Initiator Properties** window, on hello **Discovery** tab, click **Discover Portal**.</span></span>
3. <span data-ttu-id="66c66-104">在 hello**探索目標入口網站**對話方塊中，提供啟用 iSCSI 的網路介面，hello IP 位址，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="66c66-104">In hello **Discover Target Portal** dialog box, supply hello IP address of your iSCSI-enabled network interface, and then click **OK**.</span></span> 
4. <span data-ttu-id="66c66-105">在 hello **iSCSI 啟動器屬性**視窗的 hello**目標**索引標籤上，找出 hello**探索目標**。</span><span class="sxs-lookup"><span data-stu-id="66c66-105">In hello **iSCSI Initiator Properties** window, on hello **Targets** tab, locate hello **Discovered targets**.</span></span> <span data-ttu-id="66c66-106">hello 裝置狀態應顯示為**Inactive**。</span><span class="sxs-lookup"><span data-stu-id="66c66-106">hello device status should appear as **Inactive**.</span></span>
5. <span data-ttu-id="66c66-107">選取 hello 目標裝置，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="66c66-107">Select hello target device and then click **Connect**.</span></span> <span data-ttu-id="66c66-108">Hello 裝置連線之後，應該也變更 hello 狀態**Connected**。</span><span class="sxs-lookup"><span data-stu-id="66c66-108">After hello device is connected, hello status should change too**Connected**.</span></span> <span data-ttu-id="66c66-109">(如需有關使用 hello Microsoft iSCSI 啟動器的詳細資訊，請參閱[安裝和設定 Microsoft iSCSI 啟動器][1])。</span><span class="sxs-lookup"><span data-stu-id="66c66-109">(For more information about using hello Microsoft iSCSI initiator, see [Installing and Configuring Microsoft iSCSI Initiator][1]).</span></span>
6. <span data-ttu-id="66c66-110">在 Windows 主機上，按 hello Windows 爦羆坫 + X、，然後按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="66c66-110">On your Windows host, press hello Windows Logo key + X, and then click **Run**.</span></span> 
7. <span data-ttu-id="66c66-111">在 [hello**執行**] 對話方塊中，輸入**Diskmgmt.msc**。</span><span class="sxs-lookup"><span data-stu-id="66c66-111">In hello **Run** dialog box, type **Diskmgmt.msc**.</span></span> <span data-ttu-id="66c66-112">按一下**確定**，和 hello**磁碟管理**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="66c66-112">Click **OK**, and hello **Disk Management** dialog box will appear.</span></span> <span data-ttu-id="66c66-113">hello 右窗格會顯示 hello 磁碟區在主機上。</span><span class="sxs-lookup"><span data-stu-id="66c66-113">hello right pane will show hello volumes on your host.</span></span>
8. <span data-ttu-id="66c66-114">在 hello**磁碟管理**，hello 掛接的磁碟區將會出現視窗 hello 下列圖例所示。</span><span class="sxs-lookup"><span data-stu-id="66c66-114">In hello **Disk Management** window, hello mounted volumes will appear as shown in hello following illustration.</span></span> <span data-ttu-id="66c66-115">以滑鼠右鍵按一下探索到的 hello 磁碟區 （按一下 hello 磁碟名稱），然後按一下**線上**。</span><span class="sxs-lookup"><span data-stu-id="66c66-115">Right-click hello discovered volume (click hello disk name), and then click **Online**.</span></span>
   
     ![初始化格式化磁碟區](./media/storsimple-mount-initialize-format-volume/HCS_InitializeFormatVolume-include.png) 
9. <span data-ttu-id="66c66-117">以滑鼠右鍵按一下 hello 磁碟區 （按一下 hello 磁碟名稱），然後按一下**初始化**。</span><span class="sxs-lookup"><span data-stu-id="66c66-117">Right-click hello volume (click hello disk name) again, and then click **Initialize**.</span></span>
10. <span data-ttu-id="66c66-118">tooformat 簡單磁碟區中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="66c66-118">tooformat a simple volume, perform hello following steps:</span></span>
    
    1. <span data-ttu-id="66c66-119">選取 hello 磁碟區，以滑鼠右鍵按一下 （按一下 hello 右側區域），然後按一下**新增簡單磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="66c66-119">Select hello volume, right-click it (click hello right area), and click **New Simple Volume**.</span></span>
    2. <span data-ttu-id="66c66-120">在 hello 新增簡單磁碟區精靈中，指定 hello 磁碟區大小和磁碟機代號並設定 hello 磁碟區為 NTFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="66c66-120">In hello New Simple Volume wizard, specify hello volume size and drive letter and configure hello volume as an NTFS file system.</span></span>
    3. <span data-ttu-id="66c66-121">指定 64 KB 的配置單位大小。</span><span class="sxs-lookup"><span data-stu-id="66c66-121">Specify a 64 KB allocation unit size.</span></span> <span data-ttu-id="66c66-122">此配置單位大小適用於使用 hello StorSimple 解決方案中的 hello 重複資料刪除演算法。</span><span class="sxs-lookup"><span data-stu-id="66c66-122">This allocation unit size works well with hello deduplication algorithms used in hello StorSimple solution.</span></span>
    4. <span data-ttu-id="66c66-123">執行快速格式化。</span><span class="sxs-lookup"><span data-stu-id="66c66-123">Perform a quick format.</span></span>

<span data-ttu-id="66c66-124">![提供的影片](./media/storsimple-mount-initialize-format-volume/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="66c66-124">![Video available](./media/storsimple-mount-initialize-format-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="66c66-125">toowatch 的影片示範如何 toomount、 初始化、 和格式的 StorSimple 磁碟區中，按一下[這裡](https://azure.microsoft.com/documentation/videos/mount-initialize-and-format-a-storsimple-volume/)。</span><span class="sxs-lookup"><span data-stu-id="66c66-125">toowatch a video that demonstrates how toomount, initialize, and format a StorSimple volume, click [here](https://azure.microsoft.com/documentation/videos/mount-initialize-and-format-a-storsimple-volume/).</span></span>

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx