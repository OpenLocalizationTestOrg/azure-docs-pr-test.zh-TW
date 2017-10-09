既然您已加入觸發程序，其時間 toodo 一些有趣的 hello hello 觸發程序所產生的資料。 請遵循這些步驟 tooadd hello **SharePoint Online-建立檔案**動作。 這個動作會建立檔案在 SharePoint Online 中每個時間 hello 新項目引發觸發程序。 

tooconfigure hello 這個動作，您需要下列資訊 tooprovide hello。 為您提供這項資訊，您會發現它是做為某些 hello hello 新檔案的屬性輸入 hello 觸發程序所產生的簡單 toouse 資料：

| 建立檔案屬性 | 說明 |
| --- | --- |
| 網站 URL |這是 hello 的 hello toocreate hello 新檔案的 SharePoint Online 網站的 URL。 從顯示的 hello 清單中選取 hello 站台。 |
| 資料夾路徑 |這是 hello 資料夾 （在 hello hello 先前步驟中選取的網站 URL) 放置 hello 新檔案。 瀏覽及選取 hello 資料夾。 |
| 檔案名稱 |這是要建立 hello 檔案 hello 名稱。 |
| 檔案內容 |hello 寫入 toohello 檔案的內容。 |

1. 選取**+ 新增步驟**tooadd hello 動作。  
   ![SharePoint Online 動作圖像 1](./media/connectors-create-api-sharepointonline/action-1.png)  
2. 選取 hello**將動作加入**連結。 此隨即開啟 hello 搜尋方塊中，您可以搜尋的任何動作您希望 tootake。 以這個範例來說，感興趣的動作是 SharePoint 動作。    
   ![SharePoint Online 動作圖像 2](./media/connectors-create-api-sharepointonline/action-2.png)    
3. 輸入*sharepoint*動作相關 tooSharePoint 的 toosearch。
4. 選取**SharePoint Online-建立檔案**hello 動作 tootake 如下。   **請注意**： 您將會提示的 tooauthorize SharePoint 帳戶如果您沒有建立連線 tooSharePoint 線上先前您邏輯應用程式 tooaccess。    
   ![SharePoint Online 動作圖像 3](./media/connectors-create-api-sharepointonline/action-3.png)    
5. hello**建立檔案**控制隨即開啟。   
   ![SharePoint Online 動作圖像 4](./media/connectors-create-api-sharepointonline/action-4.png)     
6. 選取**網站 URL**和瀏覽 toofind hello 站台 toocreate hello 檔案的位置。     
   ![SharePoint Online 動作圖像 5](./media/connectors-create-api-sharepointonline/action-5.png)  
7. 選取**資料夾路徑**和瀏覽 toofind hello 資料夾放置 hello 新檔案。  
   ![SharePoint Online 動作圖像 6](./media/connectors-create-api-sharepointonline/action-6.png)  
8. 選取 hello**檔案名稱**控制，然後輸入 hello 名稱要 toocreate 的 hello 檔案。 在這裡，您可以直接輸入 hello 檔案名稱，或者您可以使用任何 hello 屬性從您先前建立的 hello 觸發程序。 您可以從 hello 清單中選取屬性**從新的項目建立時的輸出**。 這份清單是唯一的顯示，當您選取 hello 之後**檔案名稱**控制項。 在此 walkthough，我選取的 ID (hello 新清單項目中的 hello ID) 做為 hello hello 由 hello 所建立的檔案名稱**SharePoint Online-建立檔案**動作。    
   ![SharePoint Online 動作圖像 7](./media/connectors-create-api-sharepointonline/action-7.png)  
9. 選取 hello**檔案內容**控制，然後輸入 hello toohello 檔案，將會建立將寫入的內容。 如需 hello 檔案內容，請注意您可以使用任何 hello 屬性從您先前建立的 hello 觸發程序。 只要從顯示 hello 清單中選取 hello 屬性。 或者，您可以輸入 hello**檔案內容**直接在 hello 控制項的文字。 在此範例中，我選取了一些屬性，並在每個屬性之間加入空格和連字號。        
   ![SharePoint Online 動作圖像 8](./media/connectors-create-api-sharepointonline/action-8.png)  
10. 儲存 hello 變更 tooyour 工作流程  
11. 恭喜，您現在有新的項目加入 tooa SharePoint Online 清單時，會觸發完全正常運作的邏輯應用程式。 hello 應用程式接著會建立檔案，使用某些 hello 屬性從 hello 新清單項目。  您現在可以測試它，藉由建立新的項目 hello SharePoint 清單中。 

