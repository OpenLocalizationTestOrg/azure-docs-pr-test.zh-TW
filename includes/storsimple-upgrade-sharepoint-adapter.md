<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>升級 SharePoint 2010 tooSharePoint 2013，然後再安裝 sharepoint 的 hello StorSomple 配接器
> [!IMPORTANT]
> 任何先前移 tooexternal 儲存體透過 RBS hello 升級完成之前，將無法使用的檔案和 hello RBS 功能會啟用一次。 toolimit 使用者影響，執行任何升級或重新安裝已規劃的維護期間。
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>SharePoint 2010 tooupgrade tooSharePoint 2013，然後安裝 hello 配接器
1. Hello SharePoint 2010 伺服陣列中注意 hello BLOB 儲存路徑 hello 外部化 Blob 和 hello 內容資料庫啟用 RBS。 
2. 安裝和設定 hello 新 SharePoint 2013 伺服器陣列。 
3. 從 hello SharePoint 2010 伺服陣列 toohello 新 SharePoint 2013 伺服器陣列中，移動資料庫、 應用程式和網站集合。 如需相關指示，請移至太[hello 升級程序 tooSharePoint 2013 概觀](https://technet.microsoft.com/library/cc262483.aspx)。
4. 安裝 hello StorSimple Adapter for SharePoint hello 新伺服器陣列上。 跳過[安裝 hello StorSimple Adapter for SharePoint](#install-the-storsimple-adapter-for-sharepoint)程序。
5. 使用您在步驟 1 記下的 hello 資訊，請啟用的 hello 相同設定的內容資料庫，並提供的 hello hello SharePoint 2010 安裝在相同的 BLOB 存放區的路徑所使用的 RBS。 跳過[設定 RBS](#configure-rbs)程序。 完成此步驟之後，先前外部化的檔案必須能夠存取 hello 新伺服器陣列。 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>升級 hello StorSimple Adapter for SharePoint
> [!IMPORTANT]
> 您應該排定此升級 toooccur hello 下列原因計劃的維護期間：
> 
> * 先前外部化的內容將無法使用 hello 配接器重新安裝之前。
> * 任何上傳內容 toohello 站台之後，您解除安裝 hello 舊版 hello StorSimple Adapter for SharePoint，但在安裝新版本 hello 之前, 將儲存在 hello 內容資料庫。 安裝 hello 新配接器之後，您將需要指定 toomove 該內容 toohello StorSimple 裝置。 您可以使用 hello Microsoft` RBS Migrate()` SharePoint toomigrate hello 內容所隨附的 PowerShell cmdlet。 如需詳細資訊，請參閱 [將內容移入或移出 RBS](https://technet.microsoft.com/library/ff628255.aspx)。 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>tooupgrade hello StorSimple Adapter for SharePoint
1. 解除安裝 hello 舊版 StorSimple Adapter for SharePoint。
   
   > [!NOTE]
   > 這會自動在 hello 內容資料庫上停用 RBS。 不過，現有的 Blob 會保留在 hello StorSimple 裝置。 由於 RBS 已停用，而且 hello Blob 有尚未移轉後 toohello 內容資料庫，對於這些 Blob 的任何要求將會失敗。 
   > 
   > 
2. 安裝 hello 新的 StorSimple Adapter for SharePoint。 hello 新配接器會自動辨識先前啟用或停用 RBS hello 內容資料庫，並將使用 hello 先前的設定。

