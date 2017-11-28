---
title: "Azure Cosmos DB： 建置主控台應用程式使用 Java 和 hello MongoDB API |Microsoft 文件"
description: "提供 Java 程式碼範例，您可以使用 tooconnect tooand 查詢 hello Azure Cosmos DB MongoDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="78c7a-103">Azure Cosmos DB： 建置 MongoDB API 主控台應用程式使用 Java 和 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="78c7a-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="78c7a-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="78c7a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="78c7a-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="78c7a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="78c7a-106">本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="78c7a-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="78c7a-107">然後會建置並部署 hello 上建置主控台應用程式[MongoDB Java 驅動程式](https://docs.mongodb.com/ecosystem/drivers/java/)。</span><span class="sxs-lookup"><span data-stu-id="78c7a-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="78c7a-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="78c7a-108">Prerequisites</span></span>

* <span data-ttu-id="78c7a-109">您可以執行此範例之前，您必須擁有下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="78c7a-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="78c7a-110">JDK 1.7+ (如果您沒有 JDK 則執行 `apt-get install default-jdk`)</span><span class="sxs-lookup"><span data-stu-id="78c7a-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="78c7a-111">Maven (如果您沒有 Maven 則執行 `apt-get install maven`)</span><span class="sxs-lookup"><span data-stu-id="78c7a-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="78c7a-112">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="78c7a-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="78c7a-113">新增集合</span><span class="sxs-lookup"><span data-stu-id="78c7a-113">Add a collection</span></span>

<span data-ttu-id="78c7a-114">將新資料庫命名為 **db**，以即將新集合命名為 **coll**。</span><span class="sxs-lookup"><span data-stu-id="78c7a-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="78c7a-115">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="78c7a-115">Clone hello sample application</span></span>

<span data-ttu-id="78c7a-116">現在讓我們從 github，複製 MongoDB API 應用程式設定 hello 連接字串，並執行它。</span><span class="sxs-lookup"><span data-stu-id="78c7a-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="78c7a-117">您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="78c7a-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="78c7a-118">開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="78c7a-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="78c7a-119">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="78c7a-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="78c7a-120">然後在 Visual Studio 中開啟 hello 方案檔。</span><span class="sxs-lookup"><span data-stu-id="78c7a-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="78c7a-121">檢閱 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="78c7a-121">Review hello code</span></span>

<span data-ttu-id="78c7a-122">讓我們進行快速檢閱 hello 應用程式中的情況。</span><span class="sxs-lookup"><span data-stu-id="78c7a-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="78c7a-123">開啟 hello`Program.cs`檔案，您會發現這行程式碼建立 hello Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="78c7a-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="78c7a-124">hello DocumentClient 會初始化。</span><span class="sxs-lookup"><span data-stu-id="78c7a-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="78c7a-125">已建立新的資料庫和集合。</span><span class="sxs-lookup"><span data-stu-id="78c7a-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="78c7a-126">已使用 `MongoCollection.insertOne` 插入一些文件</span><span class="sxs-lookup"><span data-stu-id="78c7a-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="78c7a-127">已使用 `MongoCollection.find` 執行一些查詢</span><span class="sxs-lookup"><span data-stu-id="78c7a-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="78c7a-128">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="78c7a-128">Update your connection string</span></span>

<span data-ttu-id="78c7a-129">現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="78c7a-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="78c7a-130">Hello 帳戶，從選取**快速入門**，選取 Java 中，然後複製 hello 連接字串 tooyour 剪貼簿</span><span class="sxs-lookup"><span data-stu-id="78c7a-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="78c7a-131">開啟 hello`Program.java`檔案中，取代 hello 連接字串中的 hello 引數 toohello MongoClientURI 建構函式。</span><span class="sxs-lookup"><span data-stu-id="78c7a-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="78c7a-132">您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="78c7a-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="78c7a-133">執行 hello 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="78c7a-133">Run hello console app</span></span>

1. <span data-ttu-id="78c7a-134">執行`mvn package`終端機 tooinstall 中所需的 npm 模組</span><span class="sxs-lookup"><span data-stu-id="78c7a-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="78c7a-135">執行`mvn exec:java -D exec.mainClass=GetStarted.Program`中終端機 toostart Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="78c7a-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="78c7a-136">您現在可以使用[Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery、 修改及使用這個新的資料。</span><span class="sxs-lookup"><span data-stu-id="78c7a-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="78c7a-137">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="78c7a-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="78c7a-138">清除資源</span><span class="sxs-lookup"><span data-stu-id="78c7a-138">Clean up resources</span></span>

<span data-ttu-id="78c7a-139">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="78c7a-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="78c7a-140">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="78c7a-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="78c7a-141">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="78c7a-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78c7a-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="78c7a-142">Next steps</span></span>

<span data-ttu-id="78c7a-143">本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立使用 hello 資料總管集合，並執行主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="78c7a-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="78c7a-144">您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="78c7a-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="78c7a-145">將 MongoDB 資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="78c7a-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


