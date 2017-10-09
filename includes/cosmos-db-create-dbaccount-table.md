1. 在新視窗中，登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 左窗格中，按一下 **新增**，按一下 **資料庫**，，然後在**Azure Cosmos DB**，按一下**建立**。
   
   ![Hello 反白顯示更多服務與 Azure Cosmos DB 的 Azure 入口網站的螢幕擷取畫面](./media/cosmos-db-create-dbaccount-table/create-nosql-db-databases-json-tutorial-1.png)

3. 在 hello**新帳戶**刀鋒視窗中，指定 hello hello Azure Cosmos DB 帳戶所需的組態。 

    在使用 Azure Cosmos DB 時，您可以選擇下列四種程式設計模型的其中一種︰Gremlin (圖形)、MongoDB、SQL (DocumentDB) 和資料表 (索引鍵-值)。 
    
    在這個快速入門我們將會針對程式設計 hello 資料表 API 讓您將選擇**資料表 （索引鍵-值）**填寫 hello 表單。 但是，如果您有用於社交媒體應用程式的圖形資料、來自目錄應用程式的文件資料，或從 MongoDB 應用程式移轉而來的資料，請了解 Azure Cosmos DB 可以提供高度可用、全域分散式的資料庫服務平台來供您所有的任務關鍵性應用程式使用。

    填寫 hello 新帳戶 刀鋒視窗使用 hello 螢幕擷取畫面中的 hello 資訊作為指南。 您會選擇唯一的值，當您設定您的帳戶，讓您的值不完全符合 hello 螢幕擷取畫面。 
 
    ![Hello 新 Azure Cosmos DB 刀鋒視窗的螢幕擷取畫面](./media/cosmos-db-create-dbaccount-table/create-nosql-db-databases-json-tutorial-2.png)

    設定|建議的值|說明
    ---|---|---
    ID|唯一值|唯一的名稱，您可以選擇 tooidentify hello Azure Cosmos DB 帳戶。 *documents.azure.com*附加的 toohello 識別碼您提供 toocreate URI，因此，請使用唯一的但可辨識的識別碼。 hello 識別碼可能只包含小寫字母、 數字和 hello '-' 字元，而且必須介於 3 到 50 個字元之間。
    API|資料表 (索引鍵-值)|我們將程式設計 hello[表格 API](../articles/cosmos-db/table-introduction.md)本文稍後。|
    訂用帳戶|*您的訂用帳戶*|hello 的 toouse hello Azure Cosmos DB 帳戶的 Azure 訂用帳戶。 
    資源群組|*相同的值做為識別碼 hello*|hello 新資源群組名稱為您的帳戶的。 為了簡單起見，您可以使用名稱相同的 hello 做為您的識別碼。 
    位置|*hello 區域最接近 tooyour 使用者*|hello 地理位置在哪一個 toohost Azure Cosmos DB 帳戶。 選擇 hello 位置最靠近 tooyour 使用者 toogive 它們 hello 最快的存取 toohello 資料。   

4. 按一下**建立**toocreate hello 帳戶。
5. 在 [hello] 工具列上按一下**通知**toomonitor hello 部署程序。

    ![「部署已啟動」通知](./media/cosmos-db-create-dbaccount-table/notification.png)

6.  Hello 部署完畢後，請開啟 hello hello 從新的帳戶所有資源都磚。 

    ![DocumentDB 帳戶上的所有資源都磚的 hello](./media/cosmos-db-create-dbaccount-table/all-resources.png)
