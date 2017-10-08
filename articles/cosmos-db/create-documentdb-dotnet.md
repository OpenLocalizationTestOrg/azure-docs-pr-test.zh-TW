---
title: "Azure Cosmos DB： 建置 web 應用程式的.NET 和 hello DocumentDB API |Microsoft 文件"
description: "提供.NET 程式碼範例，您可以使用 tooconnect tooand 查詢 hello Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB： 建置 DocumentDB API web 應用程式的.NET 和 hello Azure 入口網站

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。 然後會建置並部署 hello 上建置 todo 清單 web 應用程式[DocumentDB.NET API](documentdb-sdk-dotnet.md)hello 下列螢幕擷取畫面所示。 

![具有範例資料的待辦事項應用程式](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>必要條件

如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。 請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
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

     您現在可以使用資料總管 tooretrieve 中的查詢資料。 根據預設，使用資料總管`SELECT * FROM c`tooretrieve 所有文件 hello 集合，但您可以變更該 tooa 不同[SQL 查詢](documentdb-sql-query.md)，例如`SELECT * FROM c ORDER BY c._ts DESC`，tooreturn 所有 hello 文件，以遞減順序都基礎依時間戳記。
 
     您也可以使用資料總管 toocreate 預存程序，Udf，觸發程序 tooperform 伺服器端商務邏輯也做為標尺的輸送量。 資料總管會公開所有 hello 程式設計的內建資料存取提供 hello Api，但提供讓您輕鬆存取 tooyour 資料 hello Azure 入口網站中。

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們來切換 tooworking 與程式碼。 讓我們複製從 GitHub 設定 hello 連接字串，並執行它的 DocumentDB API 應用程式。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`CD`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. 然後在 Visual Studio 中開啟 hello todo 方案檔。 

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello DocumentDBRepository.cs 檔案，而且您會發現這行程式碼建立 hello Azure Cosmos DB 資源。 

* hello DocumentClient 會初始化該行 73。

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* 已在行 88 上建立新資料庫。

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* 已在行 107 上建立新集合。

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. 在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。 您將使用 hello 複製按鈕右邊 hello hello 螢幕 toocopy hello URI 和主索引鍵到 hello hello 下一個步驟中的 web.config 檔案。

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-dotnet/keys.png)

2. 在 Visual Studio 2017，開啟 hello web.config 檔案。 

3. 從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello web.config 中的 hello 端點索引鍵的值。 

    `<add key="endpoint" value="FILLME" />`

4. 然後從 hello 入口網站複製您的主索引鍵的值，並讓它 hello hello authKey web.config 中的值。您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>執行 hello web 應用程式
1. 在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**，然後按一下**管理 NuGet 封裝**。 

2. 在 hello NuGet**瀏覽**方塊中，輸入*DocumentDB*。

3. 從 hello 結果中，安裝 hello **Microsoft.Azure.DocumentDB**程式庫。 這會安裝 hello Microsoft.Azure.DocumentDB 封裝，以及所有相依性。

4. 按一下 CTRL + F5 toorun hello 應用程式。 您的應用程式會顯示在瀏覽器中。 

5. 按一下**新建**在 hello 瀏覽器，並在您的待辦事項應用程式中建立一些新的工作。

   ![具有範例資料的待辦事項應用程式](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

您現在可以返回 tooData 總管和看到查詢、 修改及使用這個新的資料。 

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立集合，使用 hello 資料總管和執行 web 應用程式。 您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。 

> [!div class="nextstepaction"]
> [將資料匯入到 Azure Cosmos DB](import-data.md)


