<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="fde53-101">在此程序中，您將會：</span><span class="sxs-lookup"><span data-stu-id="fde53-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="fde53-102">[準備執行維護程式可執行檔](#to-prepare-to-run-the-maintainer) 。</span><span class="sxs-lookup"><span data-stu-id="fde53-102">[Prepare to run the Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="fde53-103">[為立即刪除遺棄的 BLOB 準備內容資料庫和資源回收筒](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs)。</span><span class="sxs-lookup"><span data-stu-id="fde53-103">[Prepare the content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="fde53-104">[執行 Maintainer.exe](#to-run-the-maintainer)。</span><span class="sxs-lookup"><span data-stu-id="fde53-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="fde53-105">[還原內容資料庫和資源回收筒設定](#to-revert-the-content-database-and-recycle-bin-settings)。</span><span class="sxs-lookup"><span data-stu-id="fde53-105">[Revert the content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="to-prepare-to-run-the-maintainer"></a><span data-ttu-id="fde53-106">準備執行維護程式</span><span class="sxs-lookup"><span data-stu-id="fde53-106">To prepare to run the Maintainer</span></span>
1. <span data-ttu-id="fde53-107">在 Web 前端伺服器上，以系統管理員身分開啟 SharePoint 2013 管理命令介面。</span><span class="sxs-lookup"><span data-stu-id="fde53-107">On the Web front-end server, open the SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="fde53-108">瀏覽至資料夾開機磁碟機:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span><span class="sxs-lookup"><span data-stu-id="fde53-108">Navigate to the folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="fde53-109">將 **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** 重新命名為 **web.config**。</span><span class="sxs-lookup"><span data-stu-id="fde53-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** to **web.config**.</span></span>
4. <span data-ttu-id="fde53-110">使用 `aspnet_regiis -pdf connectionStrings` 解密 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="fde53-110">Use `aspnet_regiis -pdf connectionStrings` to decrypt the web.config file.</span></span>
5. <span data-ttu-id="fde53-111">在解密的 web.config 檔案中的 `connectionStrings` 節點下，為您的 SQL Server 執行個體和內容資料庫名稱新增連接字串。</span><span class="sxs-lookup"><span data-stu-id="fde53-111">In the decrypted web.config file, under the `connectionStrings` node, add the connection string for your SQL server instance and the content database name.</span></span> <span data-ttu-id="fde53-112">請參閱下列範例。</span><span class="sxs-lookup"><span data-stu-id="fde53-112">See the following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="fde53-113">使用 `aspnet_regiis –pef connectionStrings` 重新加密 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="fde53-113">Use `aspnet_regiis –pef connectionStrings` to re-encrypt the web.config file.</span></span> 
7. <span data-ttu-id="fde53-114">將 web.config 重新命名為 Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config。</span><span class="sxs-lookup"><span data-stu-id="fde53-114">Rename web.config to Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs"></a><span data-ttu-id="fde53-115">為立即刪除被遺棄的 BLOB 準備內容資料庫和資源回收筒</span><span class="sxs-lookup"><span data-stu-id="fde53-115">To prepare the content database and Recycle Bin to immediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="fde53-116">在 SQL Server 上的 SQL Management Studio 中，為目標內容資料庫執行下列更新查詢：</span><span class="sxs-lookup"><span data-stu-id="fde53-116">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="fde53-117">在 Web 前端伺服器上的**管理中心**下，為所需的內容資料庫編輯 **Web 應用程式一般設定**以暫時停用資源回收筒。</span><span class="sxs-lookup"><span data-stu-id="fde53-117">On the web front-end server, under **Central Administration**, edit the **Web Application General Settings** for the desired content database to temporarily disable the Recycle Bin.</span></span> <span data-ttu-id="fde53-118">這個動作將同時清空任何相關網站集合的資源回收筒。</span><span class="sxs-lookup"><span data-stu-id="fde53-118">This action will also empty the Recycle Bin for any related site collections.</span></span> <span data-ttu-id="fde53-119">若要這樣做，請按一下 [管理中心]  ->  [應用程式管理]  ->  [Web 應用程式 (管理 Web 應用程式)]  ->  [SharePoint - 80]  ->  [一般應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="fde53-119">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="fde53-120">將**資源回收筒狀態**設為 **關閉**。</span><span class="sxs-lookup"><span data-stu-id="fde53-120">Set the **Recycle Bin Status** to **OFF**.</span></span>
   
    ![Web 應用程式一般設定](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="to-run-the-maintainer"></a><span data-ttu-id="fde53-122">執行維護程式</span><span class="sxs-lookup"><span data-stu-id="fde53-122">To run the Maintainer</span></span>
* <span data-ttu-id="fde53-123">在 web 前端伺服器上的 SharePoint 2013 管理命令介面中，執行維護程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fde53-123">On the web front-end server, in the SharePoint 2013 Management Shell, run the Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="fde53-124">此時 StorSimple 只支援 `GarbageCollection` 作業。</span><span class="sxs-lookup"><span data-stu-id="fde53-124">Only the `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="fde53-125">此外請注意，針對 Microsoft.Data.SqlRemoteBlobs.Maintainer.exe 所發出的參數會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="fde53-125">Also note that the parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="to-revert-the-content-database-and-recycle-bin-settings"></a><span data-ttu-id="fde53-126">還原內容資料庫和資源回收筒設定</span><span class="sxs-lookup"><span data-stu-id="fde53-126">To revert the content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="fde53-127">在 SQL Server 上的 SQL Management Studio 中，為目標內容資料庫執行下列更新查詢：</span><span class="sxs-lookup"><span data-stu-id="fde53-127">On the SQL Server, in SQL Management Studio, run the following update queries for the target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="fde53-128">在 Web 前端伺服器上的**管理中心**中，為所需的內容資料庫編輯 **Web 應用程式一般設定**以重新啟用資源回收筒。</span><span class="sxs-lookup"><span data-stu-id="fde53-128">On the web front-end server, in **Central Administration**, edit the **Web Application General Settings** for the desired content database to re-enable the Recycle Bin.</span></span> <span data-ttu-id="fde53-129">若要這樣做，請按一下 [管理中心]  ->  [應用程式管理]  ->  [Web 應用程式 (管理 Web 應用程式)]  ->  [SharePoint - 80]  ->  [一般應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="fde53-129">To do this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="fde53-130">將資源回收筒狀態設為**開啟**。</span><span class="sxs-lookup"><span data-stu-id="fde53-130">Set the Recycle Bin Status to **ON**.</span></span>

