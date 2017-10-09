<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="f4085-101">變更 toohello StorSimple Adapter for SharePoint 的 RBS 組態時，您必須登入所屬 toohello Domain Admins 群組的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4085-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="f4085-102">此外，您必須從 hello 管理中心為相同主機上執行瀏覽器存取 hello 組態 頁面。</span><span class="sxs-lookup"><span data-stu-id="f4085-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="f4085-103">tooconfigure RBS</span><span class="sxs-lookup"><span data-stu-id="f4085-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="f4085-104">開啟 hello SharePoint 管理中心 頁面上，並瀏覽過**系統設定**。</span><span class="sxs-lookup"><span data-stu-id="f4085-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="f4085-105">在 hello **Azure StorSimple**區段中，按一下**設定 StorSimple 介面卡**。</span><span class="sxs-lookup"><span data-stu-id="f4085-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![設定 StorSimple 介面卡 hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="f4085-107">在 hello**設定 StorSimple 介面卡**頁面：</span><span class="sxs-lookup"><span data-stu-id="f4085-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="f4085-108">請確定該 hello**啟用編輯路徑**選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f4085-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="f4085-109">在 [hello] 文字方塊中，輸入 hello 通用命名慣例 (UNC) 路徑 hello BLOB 存放區。</span><span class="sxs-lookup"><span data-stu-id="f4085-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f4085-110">hello BLOB 存放區磁碟區必須裝載在 hello StorSimple 裝置上設定 iSCSI 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f4085-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="f4085-111">按一下 hello**啟用**每個遠端存放裝置需 tooconfigure hello 內容資料庫下方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="f4085-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f4085-112">hello BLOB 存放區必須共用且可存取所有的 web 前端 (WFE) 伺服器，而且已針對 hello SharePoint 伺服器陣列的 hello 使用者帳戶必須具有存取 toohello 共用。</span><span class="sxs-lookup"><span data-stu-id="f4085-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![啟用 hello RBS 提供者](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="f4085-114">當您啟用或停用 RBS 時，也會看到下列訊息的 hello。</span><span class="sxs-lookup"><span data-stu-id="f4085-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![設定 StorSimple Adapter 啟用停用](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="f4085-116">按一下 hello**更新**按鈕 tooapply hello 組態。</span><span class="sxs-lookup"><span data-stu-id="f4085-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="f4085-117">當您按一下 hello**更新**按鈕 hello RBS 設定狀態將會更新所有 WFE 伺服器，和 hello 整個伺服器陣列將會啟用 RBS 功能。</span><span class="sxs-lookup"><span data-stu-id="f4085-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="f4085-118">hello 下訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f4085-118">hello following message appears.</span></span>
      
      ![配接器組態訊息](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="f4085-120">如果您使用非常大量的資料庫 （大於 200 個） 的 SharePoint 伺服器陣列設定 RBS，hello SharePoint 管理中心內的網頁可能會逾時。如果發生此情況，請重新整理 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="f4085-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="f4085-121">這不會影響 hello 設定程序。</span><span class="sxs-lookup"><span data-stu-id="f4085-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="f4085-122">確認 hello 組態：</span><span class="sxs-lookup"><span data-stu-id="f4085-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="f4085-123">登入 toohello SharePoint 管理中心網站，並瀏覽 toohello**設定 StorSimple 介面卡**頁面。</span><span class="sxs-lookup"><span data-stu-id="f4085-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="f4085-124">請檢查 hello 設定詳細資料 toomake 確定它們符合您輸入的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="f4085-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="f4085-125">確認 RBS 正確地運作：</span><span class="sxs-lookup"><span data-stu-id="f4085-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="f4085-126">上傳文件 tooSharePoint。</span><span class="sxs-lookup"><span data-stu-id="f4085-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="f4085-127">您設定瀏覽 toohello UNC 路徑。</span><span class="sxs-lookup"><span data-stu-id="f4085-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="f4085-128">請確定已建立 hello RBS 目錄結構，而且它包含 hello 上傳的物件。</span><span class="sxs-lookup"><span data-stu-id="f4085-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="f4085-129">（選擇性）您可以使用 Microsoft RBS hello `Migrate()` SharePoint toomigrate 現有 BLOB 內容 toohello StorSimple 裝置所隨附的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f4085-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="f4085-130">如需詳細資訊，請參閱[入或移出 RBS SharePoint 2013 中，將內容移轉][ 6]或[將內容移轉到或移出 RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="f4085-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="f4085-131">（選擇性）在測試安裝上，您可以確認，hello Blob 移出 hello 內容資料庫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f4085-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="f4085-132">啟動 SQL Management Studio</span><span class="sxs-lookup"><span data-stu-id="f4085-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="f4085-133">執行 hello ListBlobsInDB_2010.sql 或 ListBlobsInDB_2013.sql 查詢，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f4085-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="f4085-134">如果已正確地設定 RBS，NULL 值應該會出現在已上傳並使用 RBS 順利外部化的任何物件的 hello SizeOfContentInDB 資料行。</span><span class="sxs-lookup"><span data-stu-id="f4085-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="f4085-135">（選擇性）之後您設定 RBS 並將所有 BLOB 內容 toohello StorSimple 裝置，您可以都移動 hello 內容資料庫 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4085-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="f4085-136">如果您選擇 toomove hello 內容資料庫，我們建議您在主要磁碟區的 hello 裝置上設定 hello 內容資料庫儲存體。</span><span class="sxs-lookup"><span data-stu-id="f4085-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="f4085-137">然後，使用建立 SQL Server 最佳做法 toomigrate hello 內容資料庫 toohello StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4085-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f4085-138">（它不支援 hello 5000 或 7000 系列） hello StorSimple 8000 系列才支援移動 hello 內容資料庫 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4085-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="f4085-139">如果您儲存的 Blob 和內容資料庫的 hello hello StorSimple 裝置上的不同磁碟區中，我們建議它們設定在 hello 相同的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="f4085-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="f4085-140">這樣可確保它們將一起進行備份。</span><span class="sxs-lookup"><span data-stu-id="f4085-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f4085-141">如果您尚未啟用 RBS，我們不建議移 hello 內容資料庫 toohello StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="f4085-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="f4085-142">這是未經過測試的設定。</span><span class="sxs-lookup"><span data-stu-id="f4085-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="f4085-143">移 toohello 下一個步驟：[設定記憶體回收](#configure-garbage-collection)。</span><span class="sxs-lookup"><span data-stu-id="f4085-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
