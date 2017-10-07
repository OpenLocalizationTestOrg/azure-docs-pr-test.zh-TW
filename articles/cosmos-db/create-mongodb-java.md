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
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Azure Cosmos DB： 建置 MongoDB API 主控台應用程式使用 Java 和 hello Azure 入口網站

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。 然後會建置並部署 hello 上建置主控台應用程式[MongoDB Java 驅動程式](https://docs.mongodb.com/ecosystem/drivers/java/)。 

## <a name="prerequisites"></a>必要條件

* 您可以執行此範例之前，您必須擁有下列必要條件 hello:
   * JDK 1.7+ (如果您沒有 JDK 則執行 `apt-get install default-jdk`)
   * Maven (如果您沒有 Maven 則執行 `apt-get install maven`)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>新增集合

將新資料庫命名為 **db**，以即將新集合命名為 **coll**。

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們從 github，複製 MongoDB API 應用程式設定 hello 連接字串，並執行它。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. 然後在 Visual Studio 中開啟 hello 方案檔。 

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello`Program.cs`檔案，您會發現這行程式碼建立 hello Azure Cosmos DB 資源。 

* hello DocumentClient 會初始化。

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* 已建立新的資料庫和集合。

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* 已使用 `MongoCollection.insertOne` 插入一些文件

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* 已使用 `MongoCollection.find` 執行一些查詢

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. Hello 帳戶，從選取**快速入門**，選取 Java 中，然後複製 hello 連接字串 tooyour 剪貼簿

2. 開啟 hello`Program.java`檔案中，取代 hello 連接字串中的 hello 引數 toohello MongoClientURI 建構函式。 您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 
    
## <a name="run-hello-console-app"></a>執行 hello 主控台應用程式

1. 執行`mvn package`終端機 tooinstall 中所需的 npm 模組

2. 執行`mvn exec:java -D exec.mainClass=GetStarted.Program`中終端機 toostart Java 應用程式。

您現在可以使用[Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery、 修改及使用這個新的資料。

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立使用 hello 資料總管集合，並執行主控台應用程式。 您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。 

> [!div class="nextstepaction"]
> [將 MongoDB 資料匯入到 Azure Cosmos DB](mongodb-migrate.md)


