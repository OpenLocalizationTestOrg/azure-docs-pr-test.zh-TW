---
title: "Azure CosmosDB︰使用 Golang 和 Azure 入口網站建置 MongoDB API 主控台應用程式 | Microsoft Docs"
description: "提供可用來連線及查詢 Azure Cosmos DB 的 Golang 程式碼範例"
services: cosmos-db
author: Durgaprasad-Budhwani
manager: jhubbard
editor: mimig1
ms.service: cosmos-db
ms.topic: hero-article
ms.date: 07/21/2017
ms.author: mimig
ms.openlocfilehash: 9461a5d86b321fd02167379ba8751d44a861ebc2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-the-azure-portal"></a><span data-ttu-id="7f61d-103">Azure CosmosDB︰使用 Golang 和 Azure 入口網站建置 MongoDB API 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="7f61d-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and the Azure portal</span></span>

<span data-ttu-id="7f61d-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="7f61d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7f61d-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="7f61d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="7f61d-106">本快速入門示範如何使用以 [Golang](https://golang.org/) 撰寫的現有 [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) 應用程式，並將它連線到可支援 MongoDB 用戶端連線的 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f61d-106">This quick-start demonstrates how to use an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it to your Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="7f61d-107">換句話說，您的 Golang 應用程式只知道它使用 MongoDB API 連線到資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f61d-107">In other words, your Golang application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="7f61d-108">對於資料儲存在 Azure Cosmos DB 中的應用程式而言是透明的。</span><span class="sxs-lookup"><span data-stu-id="7f61d-108">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f61d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="7f61d-109">Prerequisites</span></span>

- <span data-ttu-id="7f61d-110">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f61d-110">An Azure subscription.</span></span> <span data-ttu-id="7f61d-111">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free) 。</span><span class="sxs-lookup"><span data-stu-id="7f61d-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="7f61d-112">[Go](https://golang.org/) 語言的 [Go](https://golang.org/dl/) 和基本知識。</span><span class="sxs-lookup"><span data-stu-id="7f61d-112">[Go](https://golang.org/dl/) and a basic knowledge of the [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="7f61d-113">IDE — Jetbrains 的 [Gogland](https://www.jetbrains.com/go/)、Microsoft 的 [Visual Studio 程式碼](https://code.visualstudio.com/) 或 [Atom](https://atom.io/)。</span><span class="sxs-lookup"><span data-stu-id="7f61d-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="7f61d-114">在本教學課程中，我是使用 Goglang。</span><span class="sxs-lookup"><span data-stu-id="7f61d-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="7f61d-115">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="7f61d-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="7f61d-116">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="7f61d-116">Clone the sample application</span></span>

<span data-ttu-id="7f61d-117">複製範例應用程式並安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="7f61d-117">Clone the sample application and install the required packages.</span></span>

1. <span data-ttu-id="7f61d-118">在 GOROOT\src 資料夾 (預設為 C:\Go\) 內建立名為 CosmosDBSample 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7f61d-118">Create a folder named CosmosDBSample inside the GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="7f61d-119">使用 git 終端機視窗 (例如 git bash) 執行下列命令，將範例存放庫複製到 CosmosDBSample 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7f61d-119">Run the following command using a git terminal window such as git bash to clone the sample repository into the CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="7f61d-120">執行下列命令以取得 mgo 套件。</span><span class="sxs-lookup"><span data-stu-id="7f61d-120">Run the following command to get the mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="7f61d-121">[mgo](http://labix.org/mgo) 驅動程式 (發音為 mango) 是 [Go 語言](http://golang.org/)的 [MongoDB](http://www.mongodb.org/) 驅動程式，它可在非常簡單且符合標準 Go 慣用語的 API 之下實作豐富且經過妥善測試的精選功能。</span><span class="sxs-lookup"><span data-stu-id="7f61d-121">The [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for the [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="7f61d-122">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="7f61d-122">Update your connection string</span></span>

<span data-ttu-id="7f61d-123">現在，返回 Azure 入口網站以取得連接字串資訊，並將它複製到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7f61d-123">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="7f61d-124">按一下左側導覽功能表中的 [快速入門]，然後按一下 [其他] 以檢視 Go 應用程式所需的連接字串資訊。</span><span class="sxs-lookup"><span data-stu-id="7f61d-124">Click **Quick start** in the left navigation menu, and then click **Other** to view the connection string information required by the Go application.</span></span>

2. <span data-ttu-id="7f61d-125">在 Goglang 中，開啟 GOROOT\CosmosDBSample 目錄中的 main.go 檔案，並從 Azure 入口網站使用連接字串資訊來更新下列程式碼行，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="7f61d-125">In Goglang, open the main.go file in the GOROOT\CosmosDBSample directory and update the following lines of code using the connection string information from the Azure portal as shown in the following screenshot.</span></span> 

    <span data-ttu-id="7f61d-126">在 Azure 入口網站的連接字串窗格中，資料庫名稱是 [主機] 值的前置詞。</span><span class="sxs-lookup"><span data-stu-id="7f61d-126">The Database name is the prefix of the **Host** value in the Azure portal connection string pane.</span></span> <span data-ttu-id="7f61d-127">針對下圖中顯示的帳戶，資料庫名稱是 golang-coach。</span><span class="sxs-lookup"><span data-stu-id="7f61d-127">For the account shown in the image below, the Database name is golang-coach.</span></span>

    ```go
    Database: "The prefix of the Host value in the Azure portal",
    Username: "The Username in the Azure portal",
    Password: "The Password in the Azure portal",
    ```

    ![Azure 入口網站中的 [快速入門] 窗格、顯示連接字串資訊的 [其他] 索引標籤](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="7f61d-129">儲存 main.go 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f61d-129">Save the main.go file.</span></span>

## <a name="review-the-code"></a><span data-ttu-id="7f61d-130">檢閱程式碼</span><span class="sxs-lookup"><span data-stu-id="7f61d-130">Review the code</span></span>

<span data-ttu-id="7f61d-131">讓我們快速檢閱 main.go 檔案中所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="7f61d-131">Let's make a quick review of what's happening in the main.go file.</span></span> 

### <a name="connecting-the-go-app-to-azure-cosmos-db"></a><span data-ttu-id="7f61d-132">將 Go 應用程式連線到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7f61d-132">Connecting the Go app to Azure Cosmos DB</span></span>

<span data-ttu-id="7f61d-133">Azure Cosmos DB 支援啟用 SSL 的 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="7f61d-133">Azure Cosmos DB supports the SSL-enabled MongoDB.</span></span> <span data-ttu-id="7f61d-134">若要連線至啟用 SSL 的 MongoDB，您需要在 [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo) 中定義 **DialServer** 函式，並利用 [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) 函式執行連線。</span><span class="sxs-lookup"><span data-stu-id="7f61d-134">To connect to an SSL-enabled MongoDB, you need to define the **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of the [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function to perform the connection.</span></span>

<span data-ttu-id="7f61d-135">下列 Golang 程式碼片段會透過 Azure Cosmos DB MongoDB API 連線到 Go 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f61d-135">The following Golang code snippet connects the Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="7f61d-136">DialInfo 類別保存可供建立 MongoDB 叢集之工作階段的選項。</span><span class="sxs-lookup"><span data-stu-id="7f61d-136">The *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

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
// to our Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect to mongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes the session safety mode.
// If the safe parameter is nil, the session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. The unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="7f61d-137">沒有 SSL 連線時會使用 **mgo.Dial()** 方法。</span><span class="sxs-lookup"><span data-stu-id="7f61d-137">The **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="7f61d-138">SSL 連線需使用 **mgo.DialWithInfo()** 方法。</span><span class="sxs-lookup"><span data-stu-id="7f61d-138">For an SSL connection, the **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="7f61d-139">**DialWIthInfo{}** 物件的執行個體用來建立工作階段物件。</span><span class="sxs-lookup"><span data-stu-id="7f61d-139">An instance of the **DialWIthInfo{}** object is used to create the session object.</span></span> <span data-ttu-id="7f61d-140">一旦建立工作階段，您就可以使用下列程式碼片段來存取集合：</span><span class="sxs-lookup"><span data-stu-id="7f61d-140">Once the session is established, you can access the collection by using the following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="7f61d-141">建立文件</span><span class="sxs-lookup"><span data-stu-id="7f61d-141">Create a document</span></span>

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

### <a name="query-or-read-a-document"></a><span data-ttu-id="7f61d-142">查詢或閱讀文件</span><span class="sxs-lookup"><span data-stu-id="7f61d-142">Query or read a document</span></span>

<span data-ttu-id="7f61d-143">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富查詢。</span><span class="sxs-lookup"><span data-stu-id="7f61d-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="7f61d-144">下列範例程式碼示範您可以針對集合中之文件執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="7f61d-144">The following sample code shows a query that you can run against the documents in your collection.</span></span>

```go
// Get a Document from the collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="7f61d-145">更新文件</span><span class="sxs-lookup"><span data-stu-id="7f61d-145">Update a document</span></span>

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

### <a name="delete-a-document"></a><span data-ttu-id="7f61d-146">刪除文件</span><span class="sxs-lookup"><span data-stu-id="7f61d-146">Delete a document</span></span>

<span data-ttu-id="7f61d-147">Azure Cosmos DB 支援刪除 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="7f61d-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-the-app"></a><span data-ttu-id="7f61d-148">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="7f61d-148">Run the app</span></span>

1. <span data-ttu-id="7f61d-149">在 Goglang 中，確定您的 GOPATH (可在 [檔案]、[設定]、[Go]、[GOPATH] 之下取得) 包含 gopkg 的安裝位置，預設為 USERPROFILE\go。</span><span class="sxs-lookup"><span data-stu-id="7f61d-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include the location in which the gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="7f61d-150">將可刪除文件的程式碼行 (行 91-96) 註解化，以便在執行應用程式後查看文件。</span><span class="sxs-lookup"><span data-stu-id="7f61d-150">Comment out the lines that delete the document, lines 91-96, so that you can see the document after running the app.</span></span>
3. <span data-ttu-id="7f61d-151">在 Goglang 中，按一下 [執行]，然後按一下 [執行 [建置 main.go 並執行]]。</span><span class="sxs-lookup"><span data-stu-id="7f61d-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="7f61d-152">應用程式會完成並顯示在[建立文件](#create-document)中建立之文件的說明。</span><span class="sxs-lookup"><span data-stu-id="7f61d-152">The app finishes and displays the description of the document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![顯示應用程式輸出的 Goglang](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="7f61d-154">在資料總管中檢閱您的文件</span><span class="sxs-lookup"><span data-stu-id="7f61d-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="7f61d-155">回到 Azure 入口網站，以在 [資料總管] 中查看您的文件。</span><span class="sxs-lookup"><span data-stu-id="7f61d-155">Go back to the Azure portal to see your document in Data Explorer.</span></span>

1. <span data-ttu-id="7f61d-156">按一下左側瀏覽功能表中的 [資料總管 (預覽)]，展開 [golang-coach]、[套件]，然後按一下 [文件]。</span><span class="sxs-lookup"><span data-stu-id="7f61d-156">Click **Data Explorer (Preview)** in the left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="7f61d-157">在 [文件] 索引標籤上，按一下 \_id 以在右窗格中顯示文件。</span><span class="sxs-lookup"><span data-stu-id="7f61d-157">In the **Documents** tab, click the \_id to display the document in the right pane.</span></span> 

    ![顯示新建文件的資料總管](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="7f61d-159">您可以接著使用內嵌的文件並按一下 [更新] 來儲存它。</span><span class="sxs-lookup"><span data-stu-id="7f61d-159">You can then work with the document inline and click **Update** to save it.</span></span> <span data-ttu-id="7f61d-160">您也可以刪除文件，或建立新的文件或查詢。</span><span class="sxs-lookup"><span data-stu-id="7f61d-160">You can also delete the document, or create new documents or queries.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="7f61d-161">在 Azure 入口網站中檢閱 SLA</span><span class="sxs-lookup"><span data-stu-id="7f61d-161">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7f61d-162">清除資源</span><span class="sxs-lookup"><span data-stu-id="7f61d-162">Clean up resources</span></span>

<span data-ttu-id="7f61d-163">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="7f61d-163">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="7f61d-164">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="7f61d-164">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="7f61d-165">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="7f61d-165">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f61d-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f61d-166">Next steps</span></span>

<span data-ttu-id="7f61d-167">在本快速入門中，您已了解如何建立 Azure Cosmos DB 帳戶，以及如何使用適用於 MongoDB 的 API 來執行 Golang 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f61d-167">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Golang app using the API for MongoDB.</span></span> <span data-ttu-id="7f61d-168">您現在可以將其他資料匯入到 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f61d-168">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f61d-169">將資料匯入 MongoDB API 的 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7f61d-169">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)
