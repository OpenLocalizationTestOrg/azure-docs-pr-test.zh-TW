---
title: "Azure Cosmos DB： 建置 Node.js 應用程式和 hello DocumentDB API |Microsoft 文件"
description: "顯示 Node.js 的程式碼範例，您可以使用 tooconnect tooand 查詢 hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a>Azure Cosmos DB： 建置 Node.js DocumentDB API 應用程式和 hello Azure 入口網站

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。 然後建置並執行主控台應用程式根據 hello [DocumentDB Node.js 應用程式開發介面](documentdb-sdk-node.md)。

## <a name="prerequisites"></a>必要條件

* 您可以執行此範例之前，您必須擁有下列必要條件 hello:
    * [Node.js](https://nodejs.org/en/) v0.10.29 版或更高版本
    * [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>新增集合

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們從 github，複製 DocumentDB API 應用程式設定 hello 連接字串，並執行它。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`CD`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello`app.js`檔案，並尋找這行程式碼建立 hello Azure Cosmos DB 資源。 

* hello`documentClient`已初始化。

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* 已建立新資料庫。

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* 已建立新集合。

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* 已建立一些文件。

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* 已透過 JSON 執行 SQL 查詢。

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. 在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。 您將使用 hello 複製按鈕 hello 右邊 hello 螢幕 toocopy hello URI 和主索引鍵到 hello `config.js` hello 下一個步驟中的檔案。

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-dotnet/keys.png)

2. 在開啟 hello`config.js`檔案。 

3. 從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello hello 端點中的索引鍵的值`config.js`。 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. 然後從 hello 入口網站複製您的主索引鍵的值，並讓它 hello 值 hello`config.primaryKey`中`config.js`。 您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a>執行 hello 應用程式
1. 執行`npm install`終端機 tooinstall 中所需的 npm 模組

2. 執行`node app.js`中終端機 toostart 應用程式節點。

您現在可以返回 tooData 總管和看到查詢、 修改及使用這個新的資料。 

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立集合，使用 hello 資料總管和執行應用程式。 您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。 

> [!div class="nextstepaction"]
> [將資料匯入到 Azure Cosmos DB](import-data.md)


