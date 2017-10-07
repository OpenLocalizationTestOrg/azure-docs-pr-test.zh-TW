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
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB： 建立文件資料庫使用 Java 和 hello Azure 入口網站

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門建立文件資料庫使用的 Azure Cosmos DB hello Azure 入口網站的工具。 本快速入門也會顯示如何 tooquickly 建立 Java 主控台應用程式使用 hello [DocumentDB Java API](documentdb-sdk-java.md)。 本快速入門中的 hello 指示之後只能在能夠執行 Java 任何作業系統上。 完成本快速入門會熟悉建立和修改文件以 hello UI 或以程式設計的方式，無論是您的喜好設定的資料庫資源。

## <a name="prerequisites"></a>必要條件

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * 在 Ubuntu，執行`apt-get install default-jdk`tooinstall hello JDK。
    * 為確定 tooset hello JAVA_HOME 環境變數 toopoint toohello hello JDK 安裝的資料夾。
* [下載](http://maven.apache.org/download.cgi)和[安裝 ](http://maven.apache.org/install.html) [Maven](http://maven.apache.org/) 二進位封存檔
    * 您可以執行 Ubuntu， `apt-get install maven` tooinstall Maven。
* [Git](https://www.git-scm.com/)
    * 您可以執行 Ubuntu， `sudo apt-get install git` tooinstall Git。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

您可以建立文件資料庫之前，您會需要 toocreate (DocumentDB) SQL database 帳戶與 Azure Cosmos DB。

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>新增集合

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>新增範例資料

您現在可以新增使用資料總管資料 tooyour 新集合。

1. 在 Data 總管 hello 新資料庫會出現在 hello 集合 窗格。 展開 hello**工作**資料庫中，展開 hello**項目**集合中，按一下 **文件**，然後按一下**新文件**。 

   ![Hello Azure 入口網站中，資料檔案總管中建立新文件](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. 現在加入文件 toohello 集合具有下列結構的 hello。

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. 一旦您已經新增 hello json toohello**文件**索引標籤上，按一下 **儲存**。

    ![複製中 json 資料，並將其 hello Azure 入口網站中按一下 儲存資料檔案總管中](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  建立並儲存多個一份文件，您可以在該處插入 hello 的唯一值`id`屬性，並適當地 hello 其他屬性的變更。 新文件可擁有您想要的任何結構，因為 Azure Cosmos DB 不會對您的資料強加任何結構描述。

     您可以現在使用中的查詢資料總管 tooretrieve 資料即可 hello**編輯篩選**和**套用篩選**按鈕。 根據預設，使用資料總管`SELECT * FROM c`tooretrieve 所有文件 hello 集合，但您可以變更該 tooa 不同[SQL 查詢](documentdb-sql-query.md)，例如`SELECT * FROM c ORDER BY c._ts DESC`，tooreturn 所有 hello 文件，以遞減順序都基礎依時間戳記。 
 
     您也可以使用資料總管 toocreate 預存程序，Udf，觸發程序 tooperform 伺服器端商務邏輯也做為標尺的輸送量。 資料總管會公開所有 hello 程式設計的內建資料存取提供 hello Api，但提供讓您輕鬆存取 tooyour 資料 hello Azure 入口網站中。

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們來切換 tooworking 與程式碼。 讓我們複製從 GitHub 設定 hello 連接字串，並執行它的 DocumentDB API 應用程式。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`CD`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello `Program.java` hello \src\GetStarted 資料夾中的檔案，並尋找這行程式碼建立 hello Azure Cosmos DB 資源。 

* hello`DocumentClient`已初始化。

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* 已建立新資料庫。

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* 已建立新集合。

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* 已建立一些文件。

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* 已透過 JSON 執行 SQL 查詢。

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

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。 這可讓您的應用程式 toocommunicate 裝載資料庫。

1. 在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。 您將使用 hello 複製按鈕 hello 右邊 hello 螢幕 toocopy hello URI 和主索引鍵到 hello `Program.java` hello 下一個步驟中的檔案。

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-dotnet/keys.png)

2. 在開啟的 hello`Program.java`檔案、 URI 值複製 （使用 hello [複製] 按鈕） 的 hello 入口網站，並讓它 hello hello 端點 toohello DocumentClient 建構函式中的值`Program.java`。 

    `"https://FILLME.documents.azure.com"`

4. 從 hello 入口網站複製您的主索引鍵的值，然後將它貼入"FILLME"，因此 hello hello DocumentClient 建構函式中的第二個參數。 您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 
    
## <a name="run-hello-app"></a>執行 hello 應用程式

1. 在 hello git 終端機視窗， `cd` toohello azure-cosmos-db-documentdb-java-getting-started 資料夾。

2. 在 hello git 終端機視窗，輸入`mvn package`tooinstall hello 需要 Java 封裝。

3. Hello git 終端機視窗，在執行`mvn exec:java -D exec.mainClass=GetStarted.Program`在 hello 終端機視窗 toostart Java 應用程式。

    在 hello 終端機視窗中，您會收到 hello 的 FamilyDB 建立資料庫的通知和 toopress 金鑰 toocontinue。 按索引鍵 toocreate hello 資料庫，然後切換 toohello 資料總管，您會看到它現在包含 FamilyDB 資料庫。 繼續 toopress 金鑰 toocreate hello 集合和 hello 文件，然後執行查詢。 Hello 專案完成時，會從您的帳戶刪除 hello 資源。 

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶、 文件資料庫，以及使用 hello 資料總管 中，並執行應用程式 toodo 集合以程式設計方式 hello 相同的動作。 您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。 

> [!div class="nextstepaction"]
> [將資料匯入到 Azure Cosmos DB](import-data.md)


