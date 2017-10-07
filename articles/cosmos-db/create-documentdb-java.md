---
title: "使用 Java 的 Azure Cosmos DB 文件資料庫 aaaCreate |Microsoft 文件 |Microsoft 文件 '"
description: "提供 Java 程式碼範例，您可以使用 tooconnect tooand 查詢 hello Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="c19a3-103">Azure Cosmos DB： 建立文件資料庫使用 Java 和 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c19a3-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="c19a3-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="c19a3-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c19a3-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="c19a3-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c19a3-106">本快速入門建立文件資料庫使用的 Azure Cosmos DB hello Azure 入口網站的工具。</span><span class="sxs-lookup"><span data-stu-id="c19a3-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="c19a3-107">本快速入門也會顯示如何 tooquickly 建立 Java 主控台應用程式使用 hello [DocumentDB Java API](documentdb-sdk-java.md)。</span><span class="sxs-lookup"><span data-stu-id="c19a3-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="c19a3-108">本快速入門中的 hello 指示之後只能在能夠執行 Java 任何作業系統上。</span><span class="sxs-lookup"><span data-stu-id="c19a3-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="c19a3-109">完成本快速入門會熟悉建立和修改文件以 hello UI 或以程式設計的方式，無論是您的喜好設定的資料庫資源。</span><span class="sxs-lookup"><span data-stu-id="c19a3-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c19a3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c19a3-110">Prerequisites</span></span>

* [<span data-ttu-id="c19a3-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="c19a3-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="c19a3-112">在 Ubuntu，執行`apt-get install default-jdk`tooinstall hello JDK。</span><span class="sxs-lookup"><span data-stu-id="c19a3-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="c19a3-113">為確定 tooset hello JAVA_HOME 環境變數 toopoint toohello hello JDK 安裝的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c19a3-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="c19a3-114">[下載](http://maven.apache.org/download.cgi)和[安裝 ](http://maven.apache.org/install.html) [Maven](http://maven.apache.org/) 二進位封存檔</span><span class="sxs-lookup"><span data-stu-id="c19a3-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="c19a3-115">您可以執行 Ubuntu， `apt-get install maven` tooinstall Maven。</span><span class="sxs-lookup"><span data-stu-id="c19a3-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="c19a3-116">Git</span><span class="sxs-lookup"><span data-stu-id="c19a3-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="c19a3-117">您可以執行 Ubuntu， `sudo apt-get install git` tooinstall Git。</span><span class="sxs-lookup"><span data-stu-id="c19a3-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="c19a3-118">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="c19a3-118">Create a database account</span></span>

<span data-ttu-id="c19a3-119">您可以建立文件資料庫之前，您會需要 toocreate (DocumentDB) SQL database 帳戶與 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="c19a3-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="c19a3-120">新增集合</span><span class="sxs-lookup"><span data-stu-id="c19a3-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="c19a3-121">新增範例資料</span><span class="sxs-lookup"><span data-stu-id="c19a3-121">Add sample data</span></span>

<span data-ttu-id="c19a3-122">您現在可以新增使用資料總管資料 tooyour 新集合。</span><span class="sxs-lookup"><span data-stu-id="c19a3-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="c19a3-123">在 Data 總管 hello 新資料庫會出現在 hello 集合 窗格。</span><span class="sxs-lookup"><span data-stu-id="c19a3-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="c19a3-124">展開 hello**工作**資料庫中，展開 hello**項目**集合中，按一下 **文件**，然後按一下**新文件**。</span><span class="sxs-lookup"><span data-stu-id="c19a3-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Hello Azure 入口網站中，資料檔案總管中建立新文件](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="c19a3-126">現在加入文件 toohello 集合具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="c19a3-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="c19a3-127">一旦您已經新增 hello json toohello**文件**索引標籤上，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="c19a3-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![複製中 json 資料，並將其 hello Azure 入口網站中按一下 儲存資料檔案總管中](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="c19a3-129">建立並儲存多個一份文件，您可以在該處插入 hello 的唯一值`id`屬性，並適當地 hello 其他屬性的變更。</span><span class="sxs-lookup"><span data-stu-id="c19a3-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="c19a3-130">新文件可擁有您想要的任何結構，因為 Azure Cosmos DB 不會對您的資料強加任何結構描述。</span><span class="sxs-lookup"><span data-stu-id="c19a3-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="c19a3-131">您可以現在使用中的查詢資料總管 tooretrieve 資料即可 hello**編輯篩選**和**套用篩選**按鈕。</span><span class="sxs-lookup"><span data-stu-id="c19a3-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="c19a3-132">根據預設，使用資料總管`SELECT * FROM c`tooretrieve 所有文件 hello 集合，但您可以變更該 tooa 不同[SQL 查詢](documentdb-sql-query.md)，例如`SELECT * FROM c ORDER BY c._ts DESC`，tooreturn 所有 hello 文件，以遞減順序都基礎依時間戳記。</span><span class="sxs-lookup"><span data-stu-id="c19a3-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="c19a3-133">您也可以使用資料總管 toocreate 預存程序，Udf，觸發程序 tooperform 伺服器端商務邏輯也做為標尺的輸送量。</span><span class="sxs-lookup"><span data-stu-id="c19a3-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="c19a3-134">資料總管會公開所有 hello 程式設計的內建資料存取提供 hello Api，但提供讓您輕鬆存取 tooyour 資料 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c19a3-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="c19a3-135">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="c19a3-135">Clone hello sample application</span></span>

<span data-ttu-id="c19a3-136">現在讓我們來切換 tooworking 與程式碼。</span><span class="sxs-lookup"><span data-stu-id="c19a3-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="c19a3-137">讓我們複製從 GitHub 設定 hello 連接字串，並執行它的 DocumentDB API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c19a3-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="c19a3-138">您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="c19a3-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="c19a3-139">開啟 git 終端機視窗，例如 git bash 和`CD`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="c19a3-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="c19a3-140">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="c19a3-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="c19a3-141">檢閱 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="c19a3-141">Review hello code</span></span>

<span data-ttu-id="c19a3-142">讓我們進行快速檢閱 hello 應用程式中的情況。</span><span class="sxs-lookup"><span data-stu-id="c19a3-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="c19a3-143">開啟 hello `Program.java` hello \src\GetStarted 資料夾中的檔案，並尋找這行程式碼建立 hello Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="c19a3-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="c19a3-144">hello`DocumentClient`已初始化。</span><span class="sxs-lookup"><span data-stu-id="c19a3-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="c19a3-145">已建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="c19a3-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="c19a3-146">已建立新集合。</span><span class="sxs-lookup"><span data-stu-id="c19a3-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="c19a3-147">已建立一些文件。</span><span class="sxs-lookup"><span data-stu-id="c19a3-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="c19a3-148">已透過 JSON 執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="c19a3-148">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="c19a3-149">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="c19a3-149">Update your connection string</span></span>

<span data-ttu-id="c19a3-150">現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c19a3-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="c19a3-151">這可讓您的應用程式 toocommunicate 裝載資料庫。</span><span class="sxs-lookup"><span data-stu-id="c19a3-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="c19a3-152">在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="c19a3-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="c19a3-153">您將使用 hello 複製按鈕 hello 右邊 hello 螢幕 toocopy hello URI 和主索引鍵到 hello `Program.java` hello 下一個步驟中的檔案。</span><span class="sxs-lookup"><span data-stu-id="c19a3-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="c19a3-155">在開啟的 hello`Program.java`檔案、 URI 值複製 （使用 hello [複製] 按鈕） 的 hello 入口網站，並讓它 hello hello 端點 toohello DocumentClient 建構函式中的值`Program.java`。</span><span class="sxs-lookup"><span data-stu-id="c19a3-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="c19a3-156">從 hello 入口網站複製您的主索引鍵的值，然後將它貼入"FILLME"，因此 hello hello DocumentClient 建構函式中的第二個參數。</span><span class="sxs-lookup"><span data-stu-id="c19a3-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="c19a3-157">您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="c19a3-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="c19a3-158">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c19a3-158">Run hello app</span></span>

1. <span data-ttu-id="c19a3-159">在 hello git 終端機視窗， `cd` toohello azure-cosmos-db-documentdb-java-getting-started 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c19a3-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="c19a3-160">在 hello git 終端機視窗，輸入`mvn package`tooinstall hello 需要 Java 封裝。</span><span class="sxs-lookup"><span data-stu-id="c19a3-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="c19a3-161">Hello git 終端機視窗，在執行`mvn exec:java -D exec.mainClass=GetStarted.Program`在 hello 終端機視窗 toostart Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c19a3-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="c19a3-162">在 hello 終端機視窗中，您會收到 hello 的 FamilyDB 建立資料庫的通知和 toopress 金鑰 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="c19a3-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="c19a3-163">按索引鍵 toocreate hello 資料庫，然後切換 toohello 資料總管，您會看到它現在包含 FamilyDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c19a3-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="c19a3-164">繼續 toopress 金鑰 toocreate hello 集合和 hello 文件，然後執行查詢。</span><span class="sxs-lookup"><span data-stu-id="c19a3-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="c19a3-165">Hello 專案完成時，會從您的帳戶刪除 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="c19a3-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="c19a3-167">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="c19a3-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c19a3-168">清除資源</span><span class="sxs-lookup"><span data-stu-id="c19a3-168">Clean up resources</span></span>

<span data-ttu-id="c19a3-169">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c19a3-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="c19a3-170">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="c19a3-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="c19a3-171">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="c19a3-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c19a3-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c19a3-172">Next steps</span></span>

<span data-ttu-id="c19a3-173">本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶、 文件資料庫，以及使用 hello 資料總管 中，並執行應用程式 toodo 集合以程式設計方式 hello 相同的動作。</span><span class="sxs-lookup"><span data-stu-id="c19a3-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="c19a3-174">您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c19a3-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c19a3-175">將資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c19a3-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


