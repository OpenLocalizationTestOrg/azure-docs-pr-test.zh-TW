<!--author=SharS last changed: 9/17/15-->

在此程序中，您將會：

1. [準備 toorun hello 維護程式可執行檔](#to-prepare-to-run-the-maintainer)。
2. [準備立即刪除被遺棄的 Blob 中的 hello 內容資料庫和資源回收筒](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs)。
3. [執行 Maintainer.exe](#to-run-the-maintainer)。
4. [還原 hello 內容資料庫和資源回收筒設定](#to-revert-the-content-database-and-recycle-bin-settings)。

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun hello 維護程式
1. Hello Web 前端伺服器上系統管理員身分開啟 hello SharePoint 2013 管理命令介面。
2. 瀏覽 toohello 資料夾*開機磁碟機*: \Program Files\Microsoft SQL 遠端 Blob 儲存體 10.50\Maintainer\.
3. 重新命名**Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config**太**web.config**。
4. 使用`aspnet_regiis -pdf connectionStrings`toodecrypt hello web.config 檔案。
5. 在 hello 解密的 web.config 檔案中，在 hello `connectionStrings`  節點，加入您的 SQL server 執行個體的 hello 連接字串和 hello 內容資料庫名稱。 請參閱下列範例中的 hello。
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. 使用`aspnet_regiis –pef connectionStrings`toore-hello web.config 檔案加密。 
7. 重新命名 web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config。 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>tooprepare hello 內容資料庫和資源回收筒 tooimmediately 刪除被遺棄的 Blob
1. Hello 在 SQL Management Studio 中的 SQL Server 上執行下列 hello 目標內容資料庫的更新查詢的 hello: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. 在 hello web 前端伺服器，下方**管理中心**，編輯 hello **Web 應用程式的一般設定**的 hello 預期內容資料庫 tootemporarily 停用 hello 資源回收筒。 這個動作也會空白 hello 資源回收筒，任何相關的站台集合。 toodo 此，依序按一下**管理中心** -> **應用程式管理** -> **Web 應用程式 （管理 web 應用程式）**  -> **SharePoint-80** -> **一般應用程式設定**。 設定 hello**資源回收筒狀態**太**OFF**。
   
    ![Web 應用程式一般設定](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>toorun hello 維護程式
* Hello web 前端伺服器上在 hello SharePoint 2013 管理命令介面執行 hello 維護程式，如下所示：
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > 只有 hello`GarbageCollection`此時 for StorSimple 支援作業。 也請注意發出 Microsoft.Data.SqlRemoteBlobs.Maintainer.exe hello 參數會區分大小寫。 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>toorevert hello 內容資料庫和資源回收筒設定
1. Hello 在 SQL Management Studio 中的 SQL Server 上執行下列 hello 目標內容資料庫的更新查詢的 hello:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. Hello web 前端伺服器上在**管理中心**，編輯 hello **Web 應用程式的一般設定**的 hello 預期內容資料庫 toore 啟用 hello 資源回收筒。 toodo 此，依序按一下**管理中心** -> **應用程式管理** -> **Web 應用程式 （管理 web 應用程式）**  -> **SharePoint-80** -> **一般應用程式設定**。 設定資源回收筒狀態 hello 得**ON**。

