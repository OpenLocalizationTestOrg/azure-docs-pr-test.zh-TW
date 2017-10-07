---
標題： aaa"Azure Cosmos DB： 建置與 Golang MongoDB API 主控台應用程式和 hello Azure 入口網站 |Microsoft 文件 」 描述： 顯示您可以使用 tooconnect tooand Golang 程式碼範例會查詢 Azure Cosmos DB 服務： cosmos db 作者： Durgaprasad Budhwani 管理員： jhubbard 編輯器： mimig1

ms.service: cosmos db ms.topic： 英雄文章 ms.date: 07/21/2017 ms.author: mimig
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a>Azure Cosmos DB： 建置與 Golang MongoDB API 主控台應用程式和 hello Azure 入口網站

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。

本快速入門示範如何將現有的 toouse [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction)撰寫應用程式[Golang](https://golang.org/)並將它連接 tooyour Azure Cosmos DB 資料庫支援 MongoDB 用戶端連線。

換句話說，Golang 應用程式只會知道它連接 tooa 資料庫使用 MongoDB Api。 是透明 toohello hello 資料的應用程式會儲存在 Azure Cosmos DB。

## <a name="prerequisites"></a>必要條件

- Azure 訂用帳戶。 如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free) 。
- [移](https://golang.org/dl/)hello 的基本知識和[移](https://golang.org/)語言。
- IDE — Jetbrains 的 [Gogland](https://www.jetbrains.com/go/)、Microsoft 的 [Visual Studio 程式碼](https://code.visualstudio.com/) 或 [Atom](https://atom.io/)。 在本教學課程中，我是使用 Goglang。

<a id="create-account"></a>
## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

複製 hello 範例應用程式，並安裝所需的 hello 封裝。

1. 建立預設為 C:\Go\ hello GOROOT\src 資料夾內名為 CosmosDBSample 資料夾。
2. 執行下列命令，例如 git bash tooclone hello 範例儲存機制使用 git 終端機視窗，into hello CosmosDBSample 資料夾 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  執行下列命令 tooget hello mgo 套件 hello。 

    ```
    go get gopkg.in/mgo.v2
    ```

hello [mgo](http://labix.org/mgo)驅動程式 (phishing 英文發音如為*mango*) 是[MongoDB](http://www.mongodb.org/) hello 驅動程式[移語言](http://golang.org/)實作 rich 而且也測試在下列標準 Go 慣用語非常簡單的 API 功能的選取範圍。

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. 按一下**快速入門**在 hello 左的導覽功能表，然後按一下**其他**hello 移至應用程式所需的 tooview hello 連接字串資訊。

2. 在 Goglang，hello GOROOT\CosmosDBSample 目錄中開啟 hello main.go 檔案並更新如下列幾行程式碼使用 hello Azure 入口網站中的 hello 連接字串資訊 hello 下列螢幕擷取畫面所示的 hello。 

    hello 資料庫名稱是 hello hello 前置詞**主機**hello Azure 入口網站的連接字串 窗格中的值。 Hello 帳戶 hello 圖所示，hello 資料庫名稱會是 golang 指導。

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![快速入門 窗格中，hello Azure 入口網站顯示 hello 連接字串資訊中的其他索引標籤](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. 儲存 hello main.go 檔案。

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello main.go 檔案中的情況。 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a>連接到應用程式 tooAzure Cosmos DB hello

Azure Cosmos DB 支援 hello 啟用 SSL MongoDB。 tooconnect tooan 啟用 SSL MongoDB，您需要 toodefine hello **DialServer**函式在[mgo。DialInfo](http://gopkg.in/mgo.v2#DialInfo)，並讓使用 hello [tls。*撥號*](http://golang.org/pkg/crypto/tls#Dial)函式 tooperform hello 連線。

遵循 Golang 程式碼片段的 hello 與 Azure Cosmos DB MongoDB API 連線 hello 移至應用程式。 hello *DialInfo*類別保存選項建立工作階段使用 MongoDB 的叢集。

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

hello **mgo。Dial()**方法可在沒有 SSL 連線。 SSL 連接，hello **mgo。DialWithInfo()**的方法。

執行個體的 hello **DialWIthInfo {}**物件是使用的 toocreate hello 工作階段物件。 一旦建立 hello 工作階段之後，您可以使用下列程式碼片段的 hello 存取 hello 集合：

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a>建立文件

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a>查詢或閱讀文件

Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富查詢。 hello 下列範例程式碼顯示您可以針對 hello 文件集合中執行的查詢。

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a>更新文件

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a>刪除文件

Azure Cosmos DB 支援刪除 JSON 文件。

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a>執行 hello 應用程式

1. 在 Goglang，確定您 GOPATH (適用於**檔案**，**設定**，**移**， **GOPATH**) 包含 hello 位置中的 hellogopkg 已安裝，也就是 USERPROFILE\go 預設。 
2. 使執行 hello 應用程式後，您可以看到 hello 文件註解刪除 hello 文件中，行 91 96 的 hello 行。
3. 在 Goglang 中，按一下 執行，然後按一下執行 建置 main.go 並執行。

    hello 應用程式完成，並顯示 hello 文件中建立 hello 描述[建立文件](#create-document)。
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang 顯示 hello 輸出的 hello 應用程式](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a>在資料總管中檢閱您的文件

請返回 Azure 入口網站 toosee toohello 資料總管文件。

1. 按一下**資料總管 （預覽）**在 hello 左的導覽功能表上，依序展開**golang 指導**，**封裝**，然後按一下**文件**。 在 hello**文件**索引標籤上，按一下 hello \_hello 右窗格中的識別碼 toodisplay hello 文件。 

    ![資料總管顯示 hello 新建立的文件](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. 您可以接著使用 hello 文件內嵌並按一下 **更新**toosave 它。 您也可以刪除 hello 文件，或建立新文件或查詢。

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶和執行 Golang 應用程式使用 hello API MongoDB。 您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。 

> [!div class="nextstepaction"]
> [資料匯入至 Azure Cosmos DB hello MongoDB 應用程式開發介面](mongodb-migrate.md)
