---
title: "NoSQL 教學課程：適用於 Azure Cosmos DB Java SDK 的 DocumentDB API | Microsoft Docs"
description: "NoSQL 教學課程，將使用適用於 Azure Cosmos DB 的 DocumentDB API 來建立線上資料庫以及 Java 主控台應用程式。 Azure DocumentDB 是 JSON 的 NoSQL 資料庫。"
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
ms.openlocfilehash: 5c4bcda308f001572e1c34e991616fc209250a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="9ecc4-105">NoSQL 教學課程：建置 DocumentDB API Java 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="9ecc4-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ecc4-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9ecc4-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="9ecc4-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="9ecc4-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="9ecc4-108">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="9ecc4-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="9ecc4-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="9ecc4-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="9ecc4-110">Java</span><span class="sxs-lookup"><span data-stu-id="9ecc4-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="9ecc4-111">C++</span><span class="sxs-lookup"><span data-stu-id="9ecc4-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="9ecc4-112">歡迎使用適用於 Azure Cosmos DB Java SDK 之 DocumentDB API 的 NoSQL 教學課程！</span><span class="sxs-lookup"><span data-stu-id="9ecc4-112">Welcome to the NoSQL tutorial for the DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="9ecc4-113">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="9ecc4-114">我們會說明︰</span><span class="sxs-lookup"><span data-stu-id="9ecc4-114">We cover:</span></span>

* <span data-ttu-id="9ecc4-115">建立及連線至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="9ecc4-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="9ecc4-116">設定 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="9ecc4-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="9ecc4-117">建立線上資料庫</span><span class="sxs-lookup"><span data-stu-id="9ecc4-117">Creating an online database</span></span>
* <span data-ttu-id="9ecc4-118">建立集合</span><span class="sxs-lookup"><span data-stu-id="9ecc4-118">Creating a collection</span></span>
* <span data-ttu-id="9ecc4-119">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="9ecc4-119">Creating JSON documents</span></span>
* <span data-ttu-id="9ecc4-120">查詢集合</span><span class="sxs-lookup"><span data-stu-id="9ecc4-120">Querying the collection</span></span>
* <span data-ttu-id="9ecc4-121">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="9ecc4-121">Creating JSON documents</span></span>
* <span data-ttu-id="9ecc4-122">查詢集合</span><span class="sxs-lookup"><span data-stu-id="9ecc4-122">Querying the collection</span></span>
* <span data-ttu-id="9ecc4-123">取代文件</span><span class="sxs-lookup"><span data-stu-id="9ecc4-123">Replacing a document</span></span>
* <span data-ttu-id="9ecc4-124">刪除文件</span><span class="sxs-lookup"><span data-stu-id="9ecc4-124">Deleting a document</span></span>
* <span data-ttu-id="9ecc4-125">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="9ecc4-125">Deleting the database</span></span>

<span data-ttu-id="9ecc4-126">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="9ecc4-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ecc4-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="9ecc4-127">Prerequisites</span></span>
<span data-ttu-id="9ecc4-128">請確定您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="9ecc4-128">Make sure you have the following:</span></span>

* <span data-ttu-id="9ecc4-129">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-129">An active Azure account.</span></span> <span data-ttu-id="9ecc4-130">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="9ecc4-131">或者，您可以使用 [Azure Cosmos DB 模擬器](local-emulator.md)來進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-131">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="9ecc4-132">Git</span><span class="sxs-lookup"><span data-stu-id="9ecc4-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="9ecc4-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="9ecc4-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="9ecc4-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="9ecc4-135">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="9ecc4-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="9ecc4-136">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="9ecc4-137">如果您已經擁有想要使用的帳戶，就可以跳到[複製 GitHub 專案](#GitClone)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="9ecc4-138">如果您是使用 Azure Cosmos DB 模擬器，請遵循 [Azure Cosmos DB 模擬器](local-emulator.md)的步驟來設定模擬器，並請直接跳到[複製 GitHub 專案](#GitClone)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="9ecc4-139"><a id="GitClone"></a>步驟 2︰複製 GitHub 專案</span><span class="sxs-lookup"><span data-stu-id="9ecc4-139"><a id="GitClone"></a>Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="9ecc4-140">您可以先從複製[開始使用 Azure Cosmos DB 和 Java](https://github.com/Azure-Samples/documentdb-java-getting-started) 的 GitHub 存放庫著手。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-140">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="9ecc4-141">例如，請從本機目錄執行下列命令將範例專案擷取到本機。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="9ecc4-142">目錄中包含專案的 `pom.xml` 和 `src` 資料夾，此資料夾中所含的 Java 原始程式碼包括 `Program.java`)，它會顯示如何使用 Azure Cosmos DB 執行簡單的作業，例如建立文件和查詢集合內的資料。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="9ecc4-143">`pom.xml` 包含 [Maven 上的 DocumentDB Java SDK](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb) 上的相依性。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="9ecc4-144"><a id="Connect"></a>步驟 3：連線至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="9ecc4-144"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="9ecc4-145">接下來，回到 [Azure 入口網站](https://portal.azure.com)擷取您的端點和主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="9ecc4-146">必須提供 Azure Cosmos DB 端點 URL 和主要金鑰，您的應用程式才能了解所要連線的位置，而 Azure Cosmos DB 才會信任您的應用程式連線。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-146">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="9ecc4-147">在 Azure 入口網站中，瀏覽至 Azure Cosmos DB 帳戶，然後按一下 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-147">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="9ecc4-148">從入口網站複製 URI，並將它貼到 Program.java 檔案的 `https://FILLME.documents.azure.com` 中。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-148">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="9ecc4-149">然後從入口網站複製主要金鑰，並將它貼到 `FILLME`中。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-149">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![NoSQL 教學課程用來建立 Java 主控台應用程式之 Azure 入口網站的螢幕擷取畫面。][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="9ecc4-152">步驟 4：建立資料庫</span><span class="sxs-lookup"><span data-stu-id="9ecc4-152">Step 4: Create a database</span></span>
<span data-ttu-id="9ecc4-153">可以使用 **DocumentClient** 類別的 [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) 方法建立 Azure Cosmos DB [資料庫](documentdb-resources.md#databases)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="9ecc4-154">資料庫是分割給多個集合之 JSON 文件儲存體的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="9ecc4-155"><a id="CreateColl"></a>步驟 5：建立集合</span><span class="sxs-lookup"><span data-stu-id="9ecc4-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="9ecc4-156">**createCollection** 會建立含有保留輸送量且具有價格含意的新集合。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="9ecc4-157">如需詳細資訊，請造訪[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="9ecc4-158">可以使用 **DocumentClient** 類別的 [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) 方法建立[集合](documentdb-resources.md#collections)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="9ecc4-159">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="9ecc4-160"><a id="CreateDoc"></a>步驟 6：建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="9ecc4-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="9ecc4-161">您可以使用 **DocumentClient** 類別的 [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) 方法來建立[文件](documentdb-resources.md#documents)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="9ecc4-162">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="9ecc4-163">現在可插入一或多份文件。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-163">We can now insert one or more documents.</span></span> <span data-ttu-id="9ecc4-164">如果您已經有想要儲存於資料庫中的資料，就可以使用 Azure Cosmos DB 的[資料移轉工具](import-data.md)，將資料匯入資料庫中。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-164">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

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

![說明 NoSQL 教學課程用來建立 Java 主控台應用程式之帳戶、線上資料庫、集合和文件之間階層式關聯性的圖表](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="9ecc4-166"><a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="9ecc4-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="9ecc4-167">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="9ecc4-168">下列範例程式碼示範如何使用 SQL 語法與 [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) 方法來查詢 Azure Cosmos DB 中的文件。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-168">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="9ecc4-169"><a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="9ecc4-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="9ecc4-170">Azure Cosmos DB 支援使用 [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) 方法來更新 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-170">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="9ecc4-171"><a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="9ecc4-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="9ecc4-172">同樣地，Azure Cosmos DB 支援使用 [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) 方法來將 JSON 文件刪除。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-172">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="9ecc4-173"><a id="DeleteDatabase"></a>步驟 10：刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="9ecc4-173"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="9ecc4-174">刪除已建立的資料庫會移除資料庫和所有子系資源 (集合、文件等)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="9ecc4-175"><a id="Run"></a>步驟 11：一起執行您的 Java 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="9ecc4-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="9ecc4-176">若要從主控台執行應用程式，瀏覽至專案資料夾並使用 Maven 進行編譯：</span><span class="sxs-lookup"><span data-stu-id="9ecc4-176">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="9ecc4-177">執行 `mvn package` 會從 Maven 下載最新的 Azure Cosmos DB 文件庫，並產生 `GetStarted-0.0.1-SNAPSHOT.jar`。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-177">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="9ecc4-178">然後執行下列命令來執行應用程式︰</span><span class="sxs-lookup"><span data-stu-id="9ecc4-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="9ecc4-179">恭喜！</span><span class="sxs-lookup"><span data-stu-id="9ecc4-179">Congratulations!</span></span> <span data-ttu-id="9ecc4-180">您已經完成本 NoSQL 教學課程，並擁有運作中的 Java 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="9ecc4-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ecc4-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ecc4-181">Next steps</span></span>
* <span data-ttu-id="9ecc4-182">想要 Java Web 應用程式教學課程嗎？</span><span class="sxs-lookup"><span data-stu-id="9ecc4-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="9ecc4-183">請參閱[使用 Azure Cosmos DB 以 Java 建置 Web 應用程式](documentdb-java-application.md)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="9ecc4-184">了解如何[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-184">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="9ecc4-185">在 [Query Playground](https://www.documentdb.com/sql/demo)中，針對範例資料集執行查詢。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="9ecc4-186">如需深入了解程式設計模型，請參閱 [Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)中的＜開發＞一節。</span><span class="sxs-lookup"><span data-stu-id="9ecc4-186">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
