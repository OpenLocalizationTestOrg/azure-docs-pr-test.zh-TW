<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> 變更 toohello StorSimple Adapter for SharePoint 的 RBS 組態時，您必須登入所屬 toohello Domain Admins 群組的使用者帳戶。 此外，您必須從 hello 管理中心為相同主機上執行瀏覽器存取 hello 組態 頁面。
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure RBS
1. 開啟 hello SharePoint 管理中心 頁面上，並瀏覽過**系統設定**。 
2. 在 hello **Azure StorSimple**區段中，按一下**設定 StorSimple 介面卡**。
   
    ![設定 StorSimple 介面卡 hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. 在 hello**設定 StorSimple 介面卡**頁面：
   
   1. 請確定該 hello**啟用編輯路徑**選取核取方塊。
   2. 在 [hello] 文字方塊中，輸入 hello 通用命名慣例 (UNC) 路徑 hello BLOB 存放區。
      
      > [!NOTE]
      > hello BLOB 存放區磁碟區必須裝載在 hello StorSimple 裝置上設定 iSCSI 磁碟區。

   3. 按一下 hello**啟用**每個遠端存放裝置需 tooconfigure hello 內容資料庫下方的按鈕。
      
      > [!NOTE]
      > hello BLOB 存放區必須共用且可存取所有的 web 前端 (WFE) 伺服器，而且已針對 hello SharePoint 伺服器陣列的 hello 使用者帳戶必須具有存取 toohello 共用。
      
      ![啟用 hello RBS 提供者](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      當您啟用或停用 RBS 時，也會看到下列訊息的 hello。
      
      ![設定 StorSimple Adapter 啟用停用](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. 按一下 hello**更新**按鈕 tooapply hello 組態。 當您按一下 hello**更新**按鈕 hello RBS 設定狀態將會更新所有 WFE 伺服器，和 hello 整個伺服器陣列將會啟用 RBS 功能。 hello 下訊息隨即出現。
      
      ![配接器組態訊息](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > 如果您使用非常大量的資料庫 （大於 200 個） 的 SharePoint 伺服器陣列設定 RBS，hello SharePoint 管理中心內的網頁可能會逾時。如果發生此情況，請重新整理 hello 頁面。 這不會影響 hello 設定程序。

4. 確認 hello 組態：
   
   1. 登入 toohello SharePoint 管理中心網站，並瀏覽 toohello**設定 StorSimple 介面卡**頁面。
   2. 請檢查 hello 設定詳細資料 toomake 確定它們符合您輸入的 hello 設定。 
5. 確認 RBS 正確地運作：
   
   1. 上傳文件 tooSharePoint。 
   2. 您設定瀏覽 toohello UNC 路徑。 請確定已建立 hello RBS 目錄結構，而且它包含 hello 上傳的物件。
6. （選擇性）您可以使用 Microsoft RBS hello `Migrate()` SharePoint toomigrate 現有 BLOB 內容 toohello StorSimple 裝置所隨附的 PowerShell cmdlet。 如需詳細資訊，請參閱[入或移出 RBS SharePoint 2013 中，將內容移轉][ 6]或[將內容移轉到或移出 RBS (SharePoint Foundation 2010)] [7].
7. （選擇性）在測試安裝上，您可以確認，hello Blob 移出 hello 內容資料庫，如下所示： 
   
   1. 啟動 SQL Management Studio
   2. 執行 hello ListBlobsInDB_2010.sql 或 ListBlobsInDB_2013.sql 查詢，如下所示。
      
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
      
      如果已正確地設定 RBS，NULL 值應該會出現在已上傳並使用 RBS 順利外部化的任何物件的 hello SizeOfContentInDB 資料行。
8. （選擇性）之後您設定 RBS 並將所有 BLOB 內容 toohello StorSimple 裝置，您可以都移動 hello 內容資料庫 toohello 裝置。 如果您選擇 toomove hello 內容資料庫，我們建議您在主要磁碟區的 hello 裝置上設定 hello 內容資料庫儲存體。 然後，使用建立 SQL Server 最佳做法 toomigrate hello 內容資料庫 toohello StorSimple 裝置。 
   
   > [!NOTE]
   > （它不支援 hello 5000 或 7000 系列） hello StorSimple 8000 系列才支援移動 hello 內容資料庫 toohello 裝置。
   
   如果您儲存的 Blob 和內容資料庫的 hello hello StorSimple 裝置上的不同磁碟區中，我們建議它們設定在 hello 相同的磁碟區容器。 這樣可確保它們將一起進行備份。
   
   > [!WARNING]
   > 如果您尚未啟用 RBS，我們不建議移 hello 內容資料庫 toohello StorSimple 裝置。 這是未經過測試的設定。
   
9. 移 toohello 下一個步驟：[設定記憶體回收](#configure-garbage-collection)。

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
