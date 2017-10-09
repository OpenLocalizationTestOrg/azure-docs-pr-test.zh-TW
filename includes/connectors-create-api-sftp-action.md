既然您已加入觸發程序，其時間 toodo 一些有趣的 hello hello 觸發程序所產生的資料。 請遵循這些步驟 tooadd hello **SFTP-擷取資料夾**動作。 如果符合 hello 條件定義，此動作將會擷取 hello 檔案的內容。 

tooconfigure hello 這個動作，您需要下列資訊 tooprovide hello。 您會發現它是做為某些 hello hello 新檔案的屬性輸入 hello 觸發程序所產生的簡單 toouse 資料：

| SFTP - 擷取資料夾屬性 | 說明 |
| --- | --- |
| 來源封存檔案路徑 |這是 hello hello 解壓縮的檔案路徑。 您可以選取其中一個 hello 語彙基元從較早的動作，或瀏覽 hello SFTP 伺服器 toofind hello 檔案路徑。 |
| 目的地資料夾路徑 |這是 hello 放置 hello 解壓縮檔案的路徑。 您可以選取其中一個 hello 語彙基元從較早的動作為 hello 目的地路徑或瀏覽 hello SFTP 伺服器並選取路徑。 |
| 覆寫？ |如果檔案以 hello 相同名稱，如 hello 擷取的檔案位於 hello 目的地資料夾路徑，如果應該覆寫 hello 現有檔案，或不會指示。 |

讓我們開始吧新增 hello 動作 tooextract hello 檔案，如果先前定義的 hello 條件的評估太*True*。 

1. 選取 [新增動作] 。        
   ![SFTP 動作條件圖像 6](./media/connectors-create-api-sftp/condition-6.png)   
2. 選取 hello **SFTP-擷取資料夾**動作      
   ![SFTP 動作條件圖像 7](./media/connectors-create-api-sftp/condition-7.png)   
3. 選取**來源封存檔案路徑**              
   ![SFTP 動作條件圖像 9](./media/connectors-create-api-sftp/condition-9.png)   
4. 選取 hello**檔案路徑**語彙基元。 這表示您將使用 hello hello 來源封存檔案路徑中找到的觸發程序的 hello 檔案 hello 檔案路徑。           
   ![SFTP 動作條件圖像 10](./media/connectors-create-api-sftp/condition-10.png)   
5. 選取**目的地資料夾路徑**           
   ![SFTP 動作條件圖像 11](./media/connectors-create-api-sftp/condition-11.png)   
6. 選取 hello**檔案路徑**語彙基元。 這表示您將使用 hello 觸發程序為 hello 目的地路徑找到 hello 解壓縮檔案的 hello 檔案 hello 檔案路徑。   
7. 輸入*\ExtractedFile*在 hello**目的地資料夾路徑**控制項。 只在 hello 目的地資料夾路徑控制項中的 hello 檔案路徑語彙基元之後執行這項操作。         
   ![SFTP 動作條件圖像 12](./media/connectors-create-api-sftp/condition-12.png)   
8. 輸入*True* hello 中 **覆寫嗎？*現有的檔案應該會覆寫，如果它們有相同的名稱，為 hello hello 的控制項 tooindicate 解壓縮的檔案。      
   ![SFTP 動作條件圖像 13](./media/connectors-create-api-sftp/condition-13.png)   
9. 儲存 hello 變更 tooyour 工作流程  

