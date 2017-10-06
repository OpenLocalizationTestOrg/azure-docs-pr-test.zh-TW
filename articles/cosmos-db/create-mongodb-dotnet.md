---
title: "Azure Cosmos DB： 建置 web 應用程式的.NET 和 hello MongoDB API |Microsoft 文件"
description: "提供.NET 程式碼範例，您可以使用 tooconnect tooand 查詢 hello Azure Cosmos DB MongoDB API"
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB： 建置 MongoDB API web 應用程式的.NET 和 hello Azure 入口網站

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。 然後會建置並部署 hello 上建立工作清單 web 應用程式[MongoDB.NET 驅動程式](https://docs.mongodb.com/ecosystem/drivers/csharp/)。 

## <a name="prerequisites"></a>必要條件

如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。 請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們從 github，複製 MongoDB API 應用程式設定 hello 連接字串，並執行它。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. 然後在 Visual Studio 中開啟 hello 方案檔。 

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello **Dal.cs**下 hello 檔案**DAL**目錄，您會發現這行程式碼建立 hello Azure Cosmos DB 資源。 

* 初始化 hello Mongo 用戶端。

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* 擷取 hello 資料庫與 hello 集合。

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* 擷取所有文件。

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. 在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**連接字串**，然後按一下**讀寫金鑰**。 您將使用 hello 複製按鈕右邊 hello hello 螢幕 toocopy hello 使用者名稱、 密碼和主機到 hello 下一個步驟中的 hello Dal.cs 檔案。

2. 開啟 hello **Dal.cs**檔案在 hello **DAL**目錄。 

3. 複製您**username**來自 hello 入口網站 （使用 hello [複製] 按鈕） 的值，並將其 hello 值 hello**使用者名稱**中您**Dal.cs**檔案。 

4. 然後將複製程式**主機**值從 hello 入口網站，並將其 hello hello 值**主機**中您**Dal.cs**檔案。 

5. 最後將複製程式**密碼**值從 hello 入口網站，並將其 hello 值 hello**密碼**中您**Dal.cs**檔案。 

您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 
    
## <a name="run-hello-web-app"></a>執行 hello web 應用程式

1. 在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**，然後按一下**管理 NuGet 封裝**。 

2. 在 hello NuGet**瀏覽**方塊中，輸入*MongoDB.Driver*。

3. 從 hello 結果中，安裝 hello **MongoDB.Driver**程式庫。 這會安裝 hello MongoDB.Driver 封裝，以及所有相依性。

4. 按一下 CTRL + F5 toorun hello 應用程式。 您的應用程式會顯示在瀏覽器中。 

5. 按一下**建立**入 hello 瀏覽器，並建立工作清單應用程式中的幾項新工作。

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶和執行 web 應用程式使用 hello API MongoDB。 您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。 

> [!div class="nextstepaction"]
> [資料匯入至 Azure Cosmos DB hello MongoDB 應用程式開發介面](mongodb-migrate.md)

