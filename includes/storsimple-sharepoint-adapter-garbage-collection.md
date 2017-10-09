<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="6638e-101">在此程序中，您將會：</span><span class="sxs-lookup"><span data-stu-id="6638e-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="6638e-102">[準備 toorun hello 維護程式可執行檔](#to-prepare-to-run-the-maintainer)。</span><span class="sxs-lookup"><span data-stu-id="6638e-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="6638e-103">[準備立即刪除被遺棄的 Blob 中的 hello 內容資料庫和資源回收筒](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs)。</span><span class="sxs-lookup"><span data-stu-id="6638e-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="6638e-104">[執行 Maintainer.exe](#to-run-the-maintainer)。</span><span class="sxs-lookup"><span data-stu-id="6638e-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="6638e-105">[還原 hello 內容資料庫和資源回收筒設定](#to-revert-the-content-database-and-recycle-bin-settings)。</span><span class="sxs-lookup"><span data-stu-id="6638e-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="6638e-106">tooprepare toorun hello 維護程式</span><span class="sxs-lookup"><span data-stu-id="6638e-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="6638e-107">Hello Web 前端伺服器上系統管理員身分開啟 hello SharePoint 2013 管理命令介面。</span><span class="sxs-lookup"><span data-stu-id="6638e-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="6638e-108">瀏覽 toohello 資料夾*開機磁碟機*: \Program Files\Microsoft SQL 遠端 Blob 儲存體 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="6638e-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="6638e-109">重新命名**Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config**太**web.config**。</span><span class="sxs-lookup"><span data-stu-id="6638e-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="6638e-110">使用`aspnet_regiis -pdf connectionStrings`toodecrypt hello web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="6638e-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="6638e-111">在 hello 解密的 web.config 檔案中，在 hello `connectionStrings`  節點，加入您的 SQL server 執行個體的 hello 連接字串和 hello 內容資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="6638e-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="6638e-112">請參閱下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="6638e-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="6638e-113">使用`aspnet_regiis –pef connectionStrings`toore-hello web.config 檔案加密。</span><span class="sxs-lookup"><span data-stu-id="6638e-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="6638e-114">重新命名 web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config。</span><span class="sxs-lookup"><span data-stu-id="6638e-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="6638e-115">tooprepare hello 內容資料庫和資源回收筒 tooimmediately 刪除被遺棄的 Blob</span><span class="sxs-lookup"><span data-stu-id="6638e-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="6638e-116">Hello 在 SQL Management Studio 中的 SQL Server 上執行下列 hello 目標內容資料庫的更新查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="6638e-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="6638e-117">在 hello web 前端伺服器，下方**管理中心**，編輯 hello **Web 應用程式的一般設定**的 hello 預期內容資料庫 tootemporarily 停用 hello 資源回收筒。</span><span class="sxs-lookup"><span data-stu-id="6638e-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="6638e-118">這個動作也會空白 hello 資源回收筒，任何相關的站台集合。</span><span class="sxs-lookup"><span data-stu-id="6638e-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="6638e-119">toodo 此，依序按一下**管理中心** -> **應用程式管理** -> **Web 應用程式 （管理 web 應用程式）**  -> **SharePoint-80** -> **一般應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="6638e-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="6638e-120">設定 hello**資源回收筒狀態**太**OFF**。</span><span class="sxs-lookup"><span data-stu-id="6638e-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Web 應用程式一般設定](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="6638e-122">toorun hello 維護程式</span><span class="sxs-lookup"><span data-stu-id="6638e-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="6638e-123">Hello web 前端伺服器上在 hello SharePoint 2013 管理命令介面執行 hello 維護程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6638e-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="6638e-124">只有 hello`GarbageCollection`此時 for StorSimple 支援作業。</span><span class="sxs-lookup"><span data-stu-id="6638e-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="6638e-125">也請注意發出 Microsoft.Data.SqlRemoteBlobs.Maintainer.exe hello 參數會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6638e-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="6638e-126">toorevert hello 內容資料庫和資源回收筒設定</span><span class="sxs-lookup"><span data-stu-id="6638e-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="6638e-127">Hello 在 SQL Management Studio 中的 SQL Server 上執行下列 hello 目標內容資料庫的更新查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="6638e-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="6638e-128">Hello web 前端伺服器上在**管理中心**，編輯 hello **Web 應用程式的一般設定**的 hello 預期內容資料庫 toore 啟用 hello 資源回收筒。</span><span class="sxs-lookup"><span data-stu-id="6638e-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="6638e-129">toodo 此，依序按一下**管理中心** -> **應用程式管理** -> **Web 應用程式 （管理 web 應用程式）**  -> **SharePoint-80** -> **一般應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="6638e-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="6638e-130">設定資源回收筒狀態 hello 得**ON**。</span><span class="sxs-lookup"><span data-stu-id="6638e-130">Set hello Recycle Bin Status too**ON**.</span></span>

