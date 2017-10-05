---
title: "使用 Java 建立 Azure Cosmos DB 文件資料庫 | Microsoft Docs'"
description: "提供 Java 程式碼範例，您可用來連線及查詢 Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: df1a25d703a7b8082bdabb4f7d593cb005d416fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-the-azure-portal"></a><span data-ttu-id="15a87-103">Azure Cosmos DB︰使用 Java 和 Azure 入口網站建立文件資料庫</span><span class="sxs-lookup"><span data-stu-id="15a87-103">Azure Cosmos DB: Create a document database using Java and the Azure portal</span></span>

<span data-ttu-id="15a87-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="15a87-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="15a87-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="15a87-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="15a87-106">本快速入門會使用 Azure Cosmos DB 適用的 Azure 入口網站工具建立文件資料庫。</span><span class="sxs-lookup"><span data-stu-id="15a87-106">This quickstart creates a document database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="15a87-107">本快速入門也會顯示如何使用 [DocumentDB Java API](documentdb-sdk-java.md) 快速建立 Java 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="15a87-107">This quickstart also shows you how to quickly create a Java console app using the [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="15a87-108">本快速入門中的指示可運用在任何足以執行 Java 應用程式的作業系統上。</span><span class="sxs-lookup"><span data-stu-id="15a87-108">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="15a87-109">完成本快速入門，您就會熟悉在 UI 中或以程式設計的方式建立和修改文件資料庫資源 (不論您偏好哪種方式)。</span><span class="sxs-lookup"><span data-stu-id="15a87-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either the UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15a87-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="15a87-110">Prerequisites</span></span>

* [<span data-ttu-id="15a87-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="15a87-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="15a87-112">在 Ubuntu 上，執行 `apt-get install default-jdk` 來安裝 JDK。</span><span class="sxs-lookup"><span data-stu-id="15a87-112">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="15a87-113">務必設定 JAVA_HOME 環境變數，以指向 JDK 安裝所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="15a87-113">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="15a87-114">[下載](http://maven.apache.org/download.cgi)和[安裝 ](http://maven.apache.org/install.html) [Maven](http://maven.apache.org/) 二進位封存檔</span><span class="sxs-lookup"><span data-stu-id="15a87-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="15a87-115">在 Ubuntu 上，您可以執行 `apt-get install maven` 來安裝 Maven。</span><span class="sxs-lookup"><span data-stu-id="15a87-115">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="15a87-116">Git</span><span class="sxs-lookup"><span data-stu-id="15a87-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="15a87-117">在 Ubuntu 上，您可以執行 `sudo apt-get install git` 來安裝 Git。</span><span class="sxs-lookup"><span data-stu-id="15a87-117">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="15a87-118">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="15a87-118">Create a database account</span></span>

<span data-ttu-id="15a87-119">您必須先使用 Azure Cosmos DB 建立 SQL (DocumentDB) 資料庫帳戶，才可以建立文件資料庫。</span><span class="sxs-lookup"><span data-stu-id="15a87-119">Before you can create a document database, you need to create a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="15a87-120">新增集合</span><span class="sxs-lookup"><span data-stu-id="15a87-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="15a87-121">新增範例資料</span><span class="sxs-lookup"><span data-stu-id="15a87-121">Add sample data</span></span>

<span data-ttu-id="15a87-122">您現在可以使用 [資料總管] 將資料新增至您的新集合。</span><span class="sxs-lookup"><span data-stu-id="15a87-122">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="15a87-123">在 [資料總管] 中，新的資料庫會出現在 [集合] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="15a87-123">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="15a87-124">依序展開 [工作] 資料庫、[項目] 集合，按一下 [文件]，然後按一下 [新增文件]。</span><span class="sxs-lookup"><span data-stu-id="15a87-124">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![在 Azure 入口網站的 [資料總管] 中建立新文件](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="15a87-126">現在將文件新增至具有下列結構的集合。</span><span class="sxs-lookup"><span data-stu-id="15a87-126">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="15a87-127">將 json 新增至 [文件] 索引標籤後，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="15a87-127">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![將 json 資料複製在 Azure 入口網站的 [資料總管] 中並按一下 [儲存]](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="15a87-129">多建立並儲存一份文件，以便在其中插入 `id` 屬性的唯一值，並適當變更其他屬性。</span><span class="sxs-lookup"><span data-stu-id="15a87-129">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="15a87-130">新文件可擁有您想要的任何結構，因為 Azure Cosmos DB 不會對您的資料強加任何結構描述。</span><span class="sxs-lookup"><span data-stu-id="15a87-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="15a87-131">現在按一下 [編輯篩選條件] 和 [套用篩選條件] 按鈕，即可在 [資料總管] 中使用查詢來擷取您的資料。</span><span class="sxs-lookup"><span data-stu-id="15a87-131">You can now use queries in Data Explorer to retrieve your data by clicking the **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="15a87-132">[資料總管] 預設會使用 `SELECT * FROM c` 來擷取集合中的所有文件，但您可以將其變更為不同的 [SQL 查詢](documentdb-sql-query.md) (例如 `SELECT * FROM c ORDER BY c._ts DESC`)，以根據時間戳記按遞減順序傳回所有的文件。</span><span class="sxs-lookup"><span data-stu-id="15a87-132">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="15a87-133">您也可以使用 [資料總管] 來建立預存程序、UDF 和觸發程序，以執行伺服器端商務邏輯及調整輸送量。</span><span class="sxs-lookup"><span data-stu-id="15a87-133">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="15a87-134">[資料總管] 會公開 API 中所有可用的內建程式設計資料存取，但可讓您在 Azure 入口網站中輕鬆存取您的資料。</span><span class="sxs-lookup"><span data-stu-id="15a87-134">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="15a87-135">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="15a87-135">Clone the sample application</span></span>

<span data-ttu-id="15a87-136">現在讓我們切換為使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="15a87-136">Now let's switch to working with code.</span></span> <span data-ttu-id="15a87-137">我們會從 GitHub 複製 DocumentDB API 應用程式、設定連接字串，然後執行它。</span><span class="sxs-lookup"><span data-stu-id="15a87-137">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="15a87-138">您會看到，以程式設計方式來處理資料有多麼的容易。</span><span class="sxs-lookup"><span data-stu-id="15a87-138">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="15a87-139">開啟 Git 終端機視窗 (例如 Git Bash)，然後使用 `CD` 來切換到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="15a87-139">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="15a87-140">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="15a87-140">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="15a87-141">檢閱程式碼</span><span class="sxs-lookup"><span data-stu-id="15a87-141">Review the code</span></span>

<span data-ttu-id="15a87-142">讓我們快速檢閱應用程式中所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="15a87-142">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="15a87-143">開啟 \src\GetStarted 資料夾中的 `Program.java` 檔案，並尋找建立 Azure Cosmos DB 資源的這些程式碼行。</span><span class="sxs-lookup"><span data-stu-id="15a87-143">Open the `Program.java` file from the \src\GetStarted folder, and find these lines of code that create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="15a87-144">已初始化 `DocumentClient`。</span><span class="sxs-lookup"><span data-stu-id="15a87-144">The `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="15a87-145">已建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="15a87-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="15a87-146">已建立新集合。</span><span class="sxs-lookup"><span data-stu-id="15a87-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="15a87-147">已建立一些文件。</span><span class="sxs-lookup"><span data-stu-id="15a87-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written to Azure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="15a87-148">已透過 JSON 執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="15a87-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="15a87-149">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="15a87-149">Update your connection string</span></span>

<span data-ttu-id="15a87-150">現在，返回 Azure 入口網站以取得連接字串資訊，並將它複製到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="15a87-150">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="15a87-151">這可讓您的應用程式與裝載的資料庫通訊。</span><span class="sxs-lookup"><span data-stu-id="15a87-151">This will enable your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="15a87-152">在 [Azure 入口網站](http://portal.azure.com/)中，於您 Azure Cosmos DB 帳戶的左側瀏覽區中，按一下 [金鑰]，然後按一下 [讀寫金鑰]。</span><span class="sxs-lookup"><span data-stu-id="15a87-152">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="15a87-153">在下一個步驟中，您將使用畫面右側的複製按鈕，將 URI 和主要金鑰複製到 `Program.java` 檔案。</span><span class="sxs-lookup"><span data-stu-id="15a87-153">You'll use the copy buttons on the right side of the screen to copy the URI and PRIMARY KEY into the `Program.java` file in the next step.</span></span>

    ![在 Azure 入口網站的 [金鑰] 刀鋒視窗中檢視並複製存取金鑰](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="15a87-155">在開啟的 `Program.java` 檔案中，從入口網站複製您的 URI 值 (使用 [複製] 按鈕)，並使它成為 `Program.java` 中 DocumentClient 建構函式的端點值。</span><span class="sxs-lookup"><span data-stu-id="15a87-155">In the open `Program.java` file, copy your URI value from the portal (using the copy button) and make it the value of the endpoint to the DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="15a87-156">然後，從入口網站複製您的主要金鑰值並將它貼在 “FILLME” 上，使其成為 DocumentClient 建構函式中的第二個參數。</span><span class="sxs-lookup"><span data-stu-id="15a87-156">Then copy your PRIMARY KEY value from the portal and paste it over “FILLME”, making it the second parameter in the DocumentClient constructor.</span></span> <span data-ttu-id="15a87-157">您現已更新應用程式，使其具有與 Azure Cosmos DB 通訊所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="15a87-157">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-app"></a><span data-ttu-id="15a87-158">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="15a87-158">Run the app</span></span>

1. <span data-ttu-id="15a87-159">在 git 終端機視窗中，`cd` 至 azure-cosmos-db-documentdb-java-getting-started 資料夾。</span><span class="sxs-lookup"><span data-stu-id="15a87-159">In the git terminal window, `cd` to the azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="15a87-160">在 git 終端機視窗中，輸入 `mvn package` 以安裝必要的 Java 套件。</span><span class="sxs-lookup"><span data-stu-id="15a87-160">In the git terminal window, type `mvn package` to install the required Java packages.</span></span>

3. <span data-ttu-id="15a87-161">在 git 終端機視窗中，於終端機視窗中執行 `mvn exec:java -D exec.mainClass=GetStarted.Program` 以啟動您的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="15a87-161">In the git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in the terminal window to start your Java application.</span></span>

    <span data-ttu-id="15a87-162">在終端機視窗中，您會收到表示已建立 FamilyDB 資料庫的通知，並按任一鍵繼續。</span><span class="sxs-lookup"><span data-stu-id="15a87-162">In the terminal window, you'll receive notification that the FamilyDB database was created, and to press a key to continue.</span></span> <span data-ttu-id="15a87-163">按任一鍵來建立資料庫，然後切換到 [資料總管]，您會看到它現在包含 FamilyDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="15a87-163">Press a key to create the database, then switch to the Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="15a87-164">繼續按按鍵來建立集合和文件，然後執行查詢。</span><span class="sxs-lookup"><span data-stu-id="15a87-164">Continue to press keys to create the collection and the documents and then perform a query.</span></span> <span data-ttu-id="15a87-165">當專案完成時，便會從您的帳戶中刪除資源。</span><span class="sxs-lookup"><span data-stu-id="15a87-165">When the project completes, the resources are deleted from your account.</span></span> 

    ![在 Azure 入口網站的 [金鑰] 刀鋒視窗中檢視並複製存取金鑰](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="15a87-167">在 Azure 入口網站中檢閱 SLA</span><span class="sxs-lookup"><span data-stu-id="15a87-167">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="15a87-168">清除資源</span><span class="sxs-lookup"><span data-stu-id="15a87-168">Clean up resources</span></span>

<span data-ttu-id="15a87-169">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="15a87-169">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="15a87-170">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="15a87-170">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="15a87-171">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="15a87-171">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15a87-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15a87-172">Next steps</span></span>

<span data-ttu-id="15a87-173">在本快速入門中，您已了解如何使用 [資料總管] 來建立 Azure Cosmos DB 帳戶、文件資料庫和集合，以及如何執行應用程式來以程式設計方式執行同樣的作業。</span><span class="sxs-lookup"><span data-stu-id="15a87-173">In this quickstart, you've learned how to create an Azure Cosmos DB account, document database, and collection using the Data Explorer, and run an app to do the same thing programmatically.</span></span> <span data-ttu-id="15a87-174">您現在可以將其他資料匯入到 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="15a87-174">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="15a87-175">將資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="15a87-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


