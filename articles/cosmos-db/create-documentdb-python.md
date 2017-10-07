---
title: "Azure Cosmos DB： 建置的應用程式使用 Python 和 hello DocumentDB API |Microsoft 文件"
description: "提供的 Python 程式碼範例，您可以使用 tooconnect tooand 查詢 hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a>Azure Cosmos DB： 建置 DocumentDB API 應用程式使用 Python 和 hello Azure 入口網站

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。 然後建置並執行主控台應用程式根據 hello [DocumentDB Python API](documentdb-sdk-python.md)。

## <a name="prerequisites"></a>必要條件

* 您可以執行此範例之前，您必須擁有下列必要條件 hello:
    * [Visual Studio 2015](http://www.visualstudio.com/) 或更新版本。
    * [GitHub](http://microsoft.github.io/PTVS/)的 Python Tools for Visual Studio。 本教學課程使用 Python Tools for VS 2015。
    * 來自 [python.org](https://www.python.org/downloads/release/python-2712/) 的 Python 2.7

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>新增集合

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們從 github，複製 DocumentDB API 應用程式設定 hello 連接字串，並執行它。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello DocumentDBGetStarted.py 檔案，而且您會發現這行程式碼建立 hello Azure Cosmos DB 資源。 


* hello DocumentClient 會初始化。

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* 已建立新資料庫。

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* 已建立新集合。

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* 已建立一些文件。

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* 已使用 SQL 執行查詢

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. 在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。 您將使用 hello 複製按鈕 hello 右邊 hello 螢幕 toocopy hello URI 和主索引鍵到 hello `DocumentDBGetStarted.py` hello 下一個步驟中的檔案。

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-dotnet/keys.png)

2. 在開啟 hello`DocumentDBGetStarted.py`檔案。 

3. 從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello hello 端點中的索引鍵的值`DocumentDBGetStarted.py`。 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. 然後從 hello 入口網站複製您的主索引鍵的值，並讓它 hello 值 hello`config.MASTERKEY`中`DocumentDBGetStarted.py`。 您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a>執行 hello 應用程式
1. 在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**，請選取目前 Python 環境 hello，然後以滑鼠右鍵按一下。

2. 選取 [安裝 Python 套件]，然後輸入 **pydocumentdb**

3. 執行 F5 toorun hello 應用程式。 您的應用程式會顯示在瀏覽器中。 

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
> [資料匯入至 Azure Cosmos DB hello DocumentDB API](import-data.md)


