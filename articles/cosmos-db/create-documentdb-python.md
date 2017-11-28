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
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="0c48b-103">Azure Cosmos DB： 建置 DocumentDB API 應用程式使用 Python 和 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0c48b-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="0c48b-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="0c48b-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="0c48b-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="0c48b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="0c48b-106">本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0c48b-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="0c48b-107">然後建置並執行主控台應用程式根據 hello [DocumentDB Python API](documentdb-sdk-python.md)。</span><span class="sxs-lookup"><span data-stu-id="0c48b-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c48b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="0c48b-108">Prerequisites</span></span>

* <span data-ttu-id="0c48b-109">您可以執行此範例之前，您必須擁有下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="0c48b-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="0c48b-110">[Visual Studio 2015](http://www.visualstudio.com/) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0c48b-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="0c48b-111">[GitHub](http://microsoft.github.io/PTVS/)的 Python Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0c48b-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="0c48b-112">本教學課程使用 Python Tools for VS 2015。</span><span class="sxs-lookup"><span data-stu-id="0c48b-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="0c48b-113">來自 [python.org](https://www.python.org/downloads/release/python-2712/) 的 Python 2.7</span><span class="sxs-lookup"><span data-stu-id="0c48b-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="0c48b-114">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="0c48b-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="0c48b-115">新增集合</span><span class="sxs-lookup"><span data-stu-id="0c48b-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="0c48b-116">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="0c48b-116">Clone hello sample application</span></span>

<span data-ttu-id="0c48b-117">現在讓我們從 github，複製 DocumentDB API 應用程式設定 hello 連接字串，並執行它。</span><span class="sxs-lookup"><span data-stu-id="0c48b-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="0c48b-118">您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="0c48b-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="0c48b-119">開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="0c48b-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="0c48b-120">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="0c48b-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="0c48b-121">檢閱 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="0c48b-121">Review hello code</span></span>

<span data-ttu-id="0c48b-122">讓我們進行快速檢閱 hello 應用程式中的情況。</span><span class="sxs-lookup"><span data-stu-id="0c48b-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="0c48b-123">開啟 hello DocumentDBGetStarted.py 檔案，而且您會發現這行程式碼建立 hello Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="0c48b-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="0c48b-124">hello DocumentClient 會初始化。</span><span class="sxs-lookup"><span data-stu-id="0c48b-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="0c48b-125">已建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="0c48b-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="0c48b-126">已建立新集合。</span><span class="sxs-lookup"><span data-stu-id="0c48b-126">A new collection is created.</span></span>

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

* <span data-ttu-id="0c48b-127">已建立一些文件。</span><span class="sxs-lookup"><span data-stu-id="0c48b-127">Some documents are created.</span></span>

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

* <span data-ttu-id="0c48b-128">已使用 SQL 執行查詢</span><span class="sxs-lookup"><span data-stu-id="0c48b-128">A query is performed using SQL</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="0c48b-129">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="0c48b-129">Update your connection string</span></span>

<span data-ttu-id="0c48b-130">現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c48b-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="0c48b-131">在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="0c48b-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="0c48b-132">您將使用 hello 複製按鈕 hello 右邊 hello 螢幕 toocopy hello URI 和主索引鍵到 hello `DocumentDBGetStarted.py` hello 下一個步驟中的檔案。</span><span class="sxs-lookup"><span data-stu-id="0c48b-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="0c48b-134">在開啟 hello`DocumentDBGetStarted.py`檔案。</span><span class="sxs-lookup"><span data-stu-id="0c48b-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="0c48b-135">從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello hello 端點中的索引鍵的值`DocumentDBGetStarted.py`。</span><span class="sxs-lookup"><span data-stu-id="0c48b-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="0c48b-136">然後從 hello 入口網站複製您的主索引鍵的值，並讓它 hello 值 hello`config.MASTERKEY`中`DocumentDBGetStarted.py`。</span><span class="sxs-lookup"><span data-stu-id="0c48b-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="0c48b-137">您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="0c48b-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="0c48b-138">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0c48b-138">Run hello app</span></span>
1. <span data-ttu-id="0c48b-139">在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**，請選取目前 Python 環境 hello，然後以滑鼠右鍵按一下。</span><span class="sxs-lookup"><span data-stu-id="0c48b-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="0c48b-140">選取 [安裝 Python 套件]，然後輸入 **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="0c48b-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="0c48b-141">執行 F5 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c48b-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="0c48b-142">您的應用程式會顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="0c48b-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="0c48b-143">您現在可以返回 tooData 總管和看到查詢、 修改及使用這個新的資料。</span><span class="sxs-lookup"><span data-stu-id="0c48b-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="0c48b-144">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="0c48b-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="0c48b-145">清除資源</span><span class="sxs-lookup"><span data-stu-id="0c48b-145">Clean up resources</span></span>

<span data-ttu-id="0c48b-146">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0c48b-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="0c48b-147">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="0c48b-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="0c48b-148">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="0c48b-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c48b-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c48b-149">Next steps</span></span>

<span data-ttu-id="0c48b-150">本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立集合，使用 hello 資料總管和執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c48b-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="0c48b-151">您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c48b-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="0c48b-152">資料匯入至 Azure Cosmos DB hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="0c48b-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


