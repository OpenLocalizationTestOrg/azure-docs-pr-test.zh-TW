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
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>NoSQL 教學課程：建置 DocumentDB API Java 主控台應用程式
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

 褖畫惎 toohello NoSQL 教學課程中的 hello Azure Cosmos DB Java sdk DocumentDB API ！ 完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。

我們會說明︰

* 建立及連接 tooan Azure Cosmos DB 帳戶
* 設定 Visual Studio 方案
* 建立線上資料庫
* 建立集合
* 建立 JSON 文件
* 查詢 hello 集合
* 建立 JSON 文件
* 查詢 hello 集合
* 取代文件
* 刪除文件
* 刪除 hello 資料庫

讓我們開始吧！

## <a name="prerequisites"></a>必要條件
請確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。 或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程。
* [Git](https://git-scm.com/downloads)
* [Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>步驟 1：建立 Azure Cosmos DB 帳戶
讓我們來建立 Azure Cosmos DB 帳戶。 如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[複製 hello GitHub 專案](#GitClone)。 如果您使用 hello Azure Cosmos DB 模擬器，請依照下列步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)tooset hello 模擬器並跳過[複製 hello GitHub 專案](#GitClone)。

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>步驟 2： 複製 hello GitHub 專案
您可以藉由複製 hello GitHub 儲存機制開始[開始使用 Azure Cosmos DB 和 Java](https://github.com/Azure-Samples/documentdb-java-getting-started)。 例如，從本機目錄執行下列 tooretrieve hello 範例專案在本機的 hello。

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

hello 目錄包含`pom.xml`hello 專案和`src`包含 Java 程式碼來源包括資料夾`Program.java`會顯示如何執行簡單作業之 Azure Cosmos DB 建立像文件及查詢內的資料集合。 hello`pom.xml`包含相依性 hello [DocumentDB Java SDK 上 Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb)。

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>步驟 3： 連接 tooan Azure Cosmos DB 帳戶
接下來，head 回 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的端點和主要的主要金鑰。 hello Azure Cosmos DB 端點和主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。

在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，然後按一下**金鑰**。 從 hello 入口網站複製 hello URI，並將它貼入`https://FILLME.documents.azure.com`hello Program.java 檔案中。 複製 hello 從 hello 入口網站的主索引鍵，並將它貼入`FILLME`。

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Hello hello NoSQL 教學課程 toocreate Java 主控台應用程式所使用的 Azure 入口網站的螢幕擷取畫面。 帳戶，反白顯示，hello 活躍 hello 反白顯示 hello Azure Cosmos DB 帳戶刀鋒視窗上的 [金鑰] 按鈕和 hello URI、 主索引鍵和次要索引鍵的值上反白顯示 hello 金鑰刀鋒視窗會顯示 Azure Cosmos DB][keys]

## <a name="step-4-create-a-database"></a>步驟 4：建立資料庫
您的 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)可以建立使用 hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase)方法 hello **DocumentClient**類別。 資料庫是 hello 的 JSON 文件儲存分割於各個集合的邏輯容器。

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>步驟 5：建立集合
> [!WARNING]
> **createCollection** 會建立含有保留輸送量且具有價格含意的新集合。 如需詳細資訊，請造訪[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。
> 
> 

A[集合](documentdb-resources.md#collections)可以建立使用 hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection)方法 hello **DocumentClient**類別。 集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>步驟 6：建立 JSON 文件
A[文件](documentdb-resources.md#documents)可以建立使用 hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument)方法 hello **DocumentClient**類別。 文件會是使用者定義的 (任意) JSON 內容。 現在可插入一或多份文件。 如果您已經有您想要 toostore 資料庫中的資料，您可以使用 Azure Cosmos DB 的[資料移轉工具](import-data.md)tooimport hello 資料插入資料庫。

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

## <a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源
Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。  下列範例程式碼的 hello 顯示 tooquery Azure Cosmos DB 中的文件以 hello 使用 SQL 語法[queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments)方法。

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件
Azure Cosmos DB 支援更新的 JSON 文件使用 hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument)方法。

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件
同樣地，Azure Cosmos DB 支援刪除使用 hello 的 JSON 文件[deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument)方法。  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>步驟 10： 刪除 hello 資料庫
正在刪除建立 hello 資料庫移除 hello 資料庫和所有子系資源 （集合、 文件）。

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>步驟 11：一起執行您的 Java 主控台應用程式！
toorun hello 應用程式從 hello 主控台，瀏覽 toohello 專案資料夾，然後使用 Maven 編譯：
    
    mvn package

執行`mvn package`從 Maven 下載 hello 最新 Azure Cosmos 資料程式庫，並產生`GetStarted-0.0.1-SNAPSHOT.jar`。 藉由執行，然後執行 hello 應用程式：

    mvn exec:java -D exec.mainClass=GetStarted.Program

恭喜！ 您已經完成本 NoSQL 教學課程，並擁有運作中的 Java 主控台應用程式！

## <a name="next-steps"></a>後續步驟
* 想要 Java Web 應用程式教學課程嗎？ 請參閱[使用 Azure Cosmos DB 以 Java 建置 Web 應用程式](documentdb-java-application.md)。
* 了解如何太[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。
* 執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。
* 深入了解 hello hello hello 開發一節中的程式設計模型[Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)。

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
