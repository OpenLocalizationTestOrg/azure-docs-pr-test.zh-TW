既然您已加入條件，其時間 toodo 一些有趣的 hello hello 觸發程序所產生的資料。 請遵循這些步驟 tooadd hello **Salesforce-取得物件**動作。 這個動作會收到 hello 資料每次建立新的線索。 您也會加入第二個動作將會使用從 Salesforce-Get 物件動作 toosend hello hello 資料使用 Office 365 hello 連接器一封電子郵件。  

tooconfigure hello 這個動作，您需要下列資訊 tooprovide hello。 您會發現它是做為某些 hello hello 新檔案的屬性輸入 hello 觸發程序所產生的簡單 toouse 資料：

| 建立檔案屬性 | 說明 |
| --- | --- |
| 物件類型 |這是您感興趣的 Salesforce 物件 hello 型別。 範例包括潛在客戶、帳戶等。 |
| 物件識別碼 |這代表 hello 物件的識別碼。 |

1. 選取 [新增動作]  連結。 此隨即開啟 hello 搜尋方塊中，您可以搜尋的任何動作您希望 tootake。 以這個範例來說，感興趣的動作是 Salesforce 動作。      
   ![Salesforce 動作圖像 1](./media/connectors-create-api-salesforce/action-1.png)  
2. 輸入*salesforce*動作相關 toosalesforce 的 toosearch。
3. 選取**Salesforce-取得物件**hello 動作 tootake 如下。   **請注意**： 您將會是您的 Salesforce 帳戶如果您還沒有這麼做之前您邏輯應用程式 tooaccess 提示的 tooauthorize。    
   ![Salesforce 動作圖像 2](./media/connectors-create-api-salesforce/action-2.png)    
4. hello**取得物件**控制隨即開啟。  
5. 選取*導致*hello 物件類型。
6. 選取 hello**物件識別碼**控制項。
7. 選取**...** tooexpand hello 清單可以用於做為輸入動作的語彙基元。       
   ![Salesforce 動作圖像 3](./media/connectors-create-api-salesforce/action-3.png)    
8. 選取 [潛在客戶識別碼]  控制項。   
   ![Salesforce 動作圖像 4](./media/connectors-create-api-salesforce/action-4.png)     
9. 請注意該 hello 導致 ID 語彙基元現在位於物件識別碼的控制項，指出該 hello Get 物件動作將會搜尋負責人具有 ID 將會觸發此邏輯應用程式的潛在客戶的相等 toohello 負責人識別碼 hello。  
   ![Salesforce 動作圖像 5](./media/connectors-create-api-salesforce/action-5.png)  
10. 儲存您的工作。 您現在已完成，您加入 hello Get 物件動作 tooyour 邏輯應用程式。 您的「取得物件」控制項看起來應該會像這樣︰    
    ![Salesforce 動作圖像 6](./media/connectors-create-api-salesforce/action-6.png)  

既然您已加入動作 tooget 負責人，您可能想 toodo hello 新建負責人與一些有趣。 在企業中，您可能想 toosend 電子郵件 toonotify 通訊群組清單，確認已建立新的線索。 讓我們使用 hello Office 365 連接器 toosend 電子郵件以及一些來自 hello 新負責人物件在 Salesforce 中的 hello 相關資訊。  

1. 選取**將動作加入**然後輸入*電子郵件*hello 搜尋控制項中。 這樣會篩選相關的 toosending 及接收的電子郵件的 hello 動作 toothose。  
2. 選取 hello **Office 365 Outlook 的電子郵件傳送**清單項目。 如果您尚未建立*連接*tooyour Office 365 帳戶，您將會提示的 tooenter 您 Office 365 認證 toocreate 現在 it。 完成之後，hello**傳送電子郵件**控制隨即開啟。        
   ![Salesforce 動作圖像 7](./media/connectors-create-api-salesforce/action-7.png)  
3. 輸入您想要 toosend 電子郵件 tooin hello hello 電子郵件地址**至**控制項。
4. 在 hello**主旨**控制中，輸入*新會導致建立*-然後選取 hello*公司*語彙基元。 這會顯示 hello*公司*欄位從 hello 在 Salesforce 中建立新的負責人。  
5. 在 hello**主體**控制項，您可以的選取任何 hello 語彙基元與 hello 新負責人物件，而且您也可以輸入任何文字，您想要 toodisplay hello 主體中的 hello 電子郵件。 以下是範例：  
   ![Salesforce 動作圖像 8](./media/connectors-create-api-salesforce/action-8.png)   
6. 儲存您的工作流程。  

就這麼簡單。 您的邏輯應用程式現在已完成。  

現在，您可以測試應用程式邏輯： 在 Salesforce 中建立新的負責人符合您所建立的 hello 條件。  如果您完全按照本逐步解說操作，就只要建立一個電子郵件地址包含 *amazon.com* 的新潛在客戶即可。 幾秒之後，就觸發應用程式邏輯並 hello 結果可能看起來類似 toothis:  
![Salesforce 動作圖像 9](./media/connectors-create-api-salesforce/action-9.png)  

