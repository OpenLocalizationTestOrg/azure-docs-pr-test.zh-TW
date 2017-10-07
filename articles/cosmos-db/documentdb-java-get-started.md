---
title: "NoSQL 教學課程：適用於 Azure Cosmos DB Java SDK 的 DocumentDB API | Microsoft Docs"
description: "建立線上資料庫和 Java 主控台應用程式使用的 NoSQL 教學課程 hello Azure Cosmos DB DocumentDB API。 Azure DocumentDB 是 JSON 的 NoSQL 資料庫。"
keywords: "nosql 教學課程, 線上資料庫, java 主控台應用程式"
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="62bf5-105">NoSQL 教學課程：建置 DocumentDB API Java 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="62bf5-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62bf5-106">.NET</span><span class="sxs-lookup"><span data-stu-id="62bf5-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="62bf5-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="62bf5-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="62bf5-108">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="62bf5-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="62bf5-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="62bf5-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="62bf5-110">Java</span><span class="sxs-lookup"><span data-stu-id="62bf5-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="62bf5-111">C++</span><span class="sxs-lookup"><span data-stu-id="62bf5-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="62bf5-112"> 褖畫惎 toohello NoSQL 教學課程中的 hello Azure Cosmos DB Java sdk DocumentDB API ！</span><span class="sxs-lookup"><span data-stu-id="62bf5-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="62bf5-113">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="62bf5-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="62bf5-114">我們會說明︰</span><span class="sxs-lookup"><span data-stu-id="62bf5-114">We cover:</span></span>

* <span data-ttu-id="62bf5-115">建立及連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="62bf5-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="62bf5-116">設定 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="62bf5-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="62bf5-117">建立線上資料庫</span><span class="sxs-lookup"><span data-stu-id="62bf5-117">Creating an online database</span></span>
* <span data-ttu-id="62bf5-118">建立集合</span><span class="sxs-lookup"><span data-stu-id="62bf5-118">Creating a collection</span></span>
* <span data-ttu-id="62bf5-119">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="62bf5-119">Creating JSON documents</span></span>
* <span data-ttu-id="62bf5-120">查詢 hello 集合</span><span class="sxs-lookup"><span data-stu-id="62bf5-120">Querying hello collection</span></span>
* <span data-ttu-id="62bf5-121">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="62bf5-121">Creating JSON documents</span></span>
* <span data-ttu-id="62bf5-122">查詢 hello 集合</span><span class="sxs-lookup"><span data-stu-id="62bf5-122">Querying hello collection</span></span>
* <span data-ttu-id="62bf5-123">取代文件</span><span class="sxs-lookup"><span data-stu-id="62bf5-123">Replacing a document</span></span>
* <span data-ttu-id="62bf5-124">刪除文件</span><span class="sxs-lookup"><span data-stu-id="62bf5-124">Deleting a document</span></span>
* <span data-ttu-id="62bf5-125">刪除 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="62bf5-125">Deleting hello database</span></span>

<span data-ttu-id="62bf5-126">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="62bf5-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62bf5-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="62bf5-127">Prerequisites</span></span>
<span data-ttu-id="62bf5-128">請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="62bf5-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="62bf5-129">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="62bf5-129">An active Azure account.</span></span> <span data-ttu-id="62bf5-130">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="62bf5-131">或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程。</span><span class="sxs-lookup"><span data-stu-id="62bf5-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="62bf5-132">Git</span><span class="sxs-lookup"><span data-stu-id="62bf5-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="62bf5-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="62bf5-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="62bf5-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="62bf5-135">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="62bf5-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="62bf5-136">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="62bf5-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="62bf5-137">如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[複製 hello GitHub 專案](#GitClone)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="62bf5-138">如果您使用 hello Azure Cosmos DB 模擬器，請依照下列步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)tooset hello 模擬器並跳過[複製 hello GitHub 專案](#GitClone)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="62bf5-139"><a id="GitClone"></a>步驟 2： 複製 hello GitHub 專案</span><span class="sxs-lookup"><span data-stu-id="62bf5-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="62bf5-140">您可以藉由複製 hello GitHub 儲存機制開始[開始使用 Azure Cosmos DB 和 Java](https://github.com/Azure-Samples/documentdb-java-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="62bf5-141">例如，從本機目錄執行下列 tooretrieve hello 範例專案在本機的 hello。</span><span class="sxs-lookup"><span data-stu-id="62bf5-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="62bf5-142">hello 目錄包含`pom.xml`hello 專案和`src`包含 Java 程式碼來源包括資料夾`Program.java`會顯示如何執行簡單作業之 Azure Cosmos DB 建立像文件及查詢內的資料集合。</span><span class="sxs-lookup"><span data-stu-id="62bf5-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="62bf5-143">hello`pom.xml`包含相依性 hello [DocumentDB Java SDK 上 Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="62bf5-144"><a id="Connect"></a>步驟 3： 連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="62bf5-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="62bf5-145">接下來，head 回 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的端點和主要的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="62bf5-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="62bf5-146">hello Azure Cosmos DB 端點和主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。</span><span class="sxs-lookup"><span data-stu-id="62bf5-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="62bf5-147">在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，然後按一下**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="62bf5-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="62bf5-148">從 hello 入口網站複製 hello URI，並將它貼入`https://FILLME.documents.azure.com`hello Program.java 檔案中。</span><span class="sxs-lookup"><span data-stu-id="62bf5-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="62bf5-149">複製 hello 從 hello 入口網站的主索引鍵，並將它貼入`FILLME`。</span><span class="sxs-lookup"><span data-stu-id="62bf5-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Hello hello NoSQL 教學課程 toocreate Java 主控台應用程式所使用的 Azure 入口網站的螢幕擷取畫面。][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="62bf5-152">步驟 4：建立資料庫</span><span class="sxs-lookup"><span data-stu-id="62bf5-152">Step 4: Create a database</span></span>
<span data-ttu-id="62bf5-153">您的 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)可以建立使用 hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="62bf5-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="62bf5-154">資料庫是 hello 的 JSON 文件儲存分割於各個集合的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="62bf5-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="62bf5-155"><a id="CreateColl"></a>步驟 5：建立集合</span><span class="sxs-lookup"><span data-stu-id="62bf5-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="62bf5-156">**createCollection** 會建立含有保留輸送量且具有價格含意的新集合。</span><span class="sxs-lookup"><span data-stu-id="62bf5-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="62bf5-157">如需詳細資訊，請造訪[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="62bf5-158">A[集合](documentdb-resources.md#collections)可以建立使用 hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="62bf5-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="62bf5-159">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="62bf5-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="62bf5-160"><a id="CreateDoc"></a>步驟 6：建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="62bf5-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="62bf5-161">A[文件](documentdb-resources.md#documents)可以建立使用 hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="62bf5-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="62bf5-162">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="62bf5-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="62bf5-163">現在可插入一或多份文件。</span><span class="sxs-lookup"><span data-stu-id="62bf5-163">We can now insert one or more documents.</span></span> <span data-ttu-id="62bf5-164">如果您已經有您想要 toostore 資料庫中的資料，您可以使用 Azure Cosmos DB 的[資料移轉工具](import-data.md)tooimport hello 資料插入資料庫。</span><span class="sxs-lookup"><span data-stu-id="62bf5-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![以圖表顯示的 hello 階層式關聯性，hello 帳戶、 hello 線上資料庫、 hello 集合和 hello hello NoSQL 教學課程 toocreate Java 主控台應用程式所使用的文件之間](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="62bf5-166"><a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="62bf5-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="62bf5-167">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="62bf5-168">下列範例程式碼的 hello 顯示 tooquery Azure Cosmos DB 中的文件以 hello 使用 SQL 語法[queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments)方法。</span><span class="sxs-lookup"><span data-stu-id="62bf5-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="62bf5-169"><a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="62bf5-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="62bf5-170">Azure Cosmos DB 支援更新的 JSON 文件使用 hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument)方法。</span><span class="sxs-lookup"><span data-stu-id="62bf5-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="62bf5-171"><a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="62bf5-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="62bf5-172">同樣地，Azure Cosmos DB 支援刪除使用 hello 的 JSON 文件[deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument)方法。</span><span class="sxs-lookup"><span data-stu-id="62bf5-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="62bf5-173"><a id="DeleteDatabase"></a>步驟 10： 刪除 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="62bf5-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="62bf5-174">正在刪除建立 hello 資料庫移除 hello 資料庫和所有子系資源 （集合、 文件）。</span><span class="sxs-lookup"><span data-stu-id="62bf5-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="62bf5-175"><a id="Run"></a>步驟 11：一起執行您的 Java 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="62bf5-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="62bf5-176">toorun hello 應用程式從 hello 主控台，瀏覽 toohello 專案資料夾，然後使用 Maven 編譯：</span><span class="sxs-lookup"><span data-stu-id="62bf5-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="62bf5-177">執行`mvn package`從 Maven 下載 hello 最新 Azure Cosmos 資料程式庫，並產生`GetStarted-0.0.1-SNAPSHOT.jar`。</span><span class="sxs-lookup"><span data-stu-id="62bf5-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="62bf5-178">藉由執行，然後執行 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="62bf5-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="62bf5-179">恭喜！</span><span class="sxs-lookup"><span data-stu-id="62bf5-179">Congratulations!</span></span> <span data-ttu-id="62bf5-180">您已經完成本 NoSQL 教學課程，並擁有運作中的 Java 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="62bf5-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="62bf5-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62bf5-181">Next steps</span></span>
* <span data-ttu-id="62bf5-182">想要 Java Web 應用程式教學課程嗎？</span><span class="sxs-lookup"><span data-stu-id="62bf5-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="62bf5-183">請參閱[使用 Azure Cosmos DB 以 Java 建置 Web 應用程式](documentdb-java-application.md)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="62bf5-184">了解如何太[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="62bf5-185">執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="62bf5-186">深入了解 hello hello hello 開發一節中的程式設計模型[Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="62bf5-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
