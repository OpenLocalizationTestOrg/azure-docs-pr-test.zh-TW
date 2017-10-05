---
title: "Azure CosmosDB︰使用 Python 和 DocumentDB API 建置應用程式 | Microsoft Docs"
description: "提供 Python 程式碼範例，您可用來連線及查詢 Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: 08d467ea27484e7d1d07d6c21b2e04b6525fbcd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-the-azure-portal"></a><span data-ttu-id="d5718-103">Azure CosmosDB︰使用 Python 和 Azure 入口網站建置 DocumentDB API 應用程式</span><span class="sxs-lookup"><span data-stu-id="d5718-103">Azure Cosmos DB: Build a DocumentDB API app with Python and the Azure portal</span></span>

<span data-ttu-id="d5718-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="d5718-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d5718-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="d5718-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="d5718-106">本快速入門會示範如何使用 Azure 入口網站建立 Azure Cosmos DB 帳戶、文件資料庫和集合。</span><span class="sxs-lookup"><span data-stu-id="d5718-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="d5718-107">您會接著建置和執行以 [DocumentDB Python API](documentdb-sdk-python.md) 為基礎的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5718-107">You then build and run a console app built on the [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5718-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="d5718-108">Prerequisites</span></span>

* <span data-ttu-id="d5718-109">您必須具備下列必要條件，才能執行此範例：</span><span class="sxs-lookup"><span data-stu-id="d5718-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="d5718-110">[Visual Studio 2015](http://www.visualstudio.com/) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d5718-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="d5718-111">[GitHub](http://microsoft.github.io/PTVS/)的 Python Tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d5718-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="d5718-112">本教學課程使用 Python Tools for VS 2015。</span><span class="sxs-lookup"><span data-stu-id="d5718-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="d5718-113">來自 [python.org](https://www.python.org/downloads/release/python-2712/) 的 Python 2.7</span><span class="sxs-lookup"><span data-stu-id="d5718-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="d5718-114">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="d5718-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="d5718-115">新增集合</span><span class="sxs-lookup"><span data-stu-id="d5718-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="d5718-116">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="d5718-116">Clone the sample application</span></span>

<span data-ttu-id="d5718-117">現在，我們將從 Github 複製 DocumentDB API 應用程式、設定連接字串，然後執行它。</span><span class="sxs-lookup"><span data-stu-id="d5718-117">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="d5718-118">您會看到，以程式設計方式來處理資料有多麼的容易。</span><span class="sxs-lookup"><span data-stu-id="d5718-118">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="d5718-119">開啟 Git 終端機視窗 (例如 Git Bash)，然後使用 `cd` 來切換到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="d5718-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="d5718-120">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="d5718-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-the-code"></a><span data-ttu-id="d5718-121">檢閱程式碼</span><span class="sxs-lookup"><span data-stu-id="d5718-121">Review the code</span></span>

<span data-ttu-id="d5718-122">讓我們快速檢閱應用程式中所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="d5718-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="d5718-123">請開啟 DocumentDBGetStarted.py 檔案，您會發現這些程式碼行會建立 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="d5718-123">Open the DocumentDBGetStarted.py file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="d5718-124">已初始化 DocumentClient。</span><span class="sxs-lookup"><span data-stu-id="d5718-124">The DocumentClient is initialized.</span></span>

    ```python
    # Initialize the Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="d5718-125">已建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5718-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="d5718-126">已建立新集合。</span><span class="sxs-lookup"><span data-stu-id="d5718-126">A new collection is created.</span></span>

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

* <span data-ttu-id="d5718-127">已建立一些文件。</span><span class="sxs-lookup"><span data-stu-id="d5718-127">Some documents are created.</span></span>

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

* <span data-ttu-id="d5718-128">已使用 SQL 執行查詢</span><span class="sxs-lookup"><span data-stu-id="d5718-128">A query is performed using SQL</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="d5718-129">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="d5718-129">Update your connection string</span></span>

<span data-ttu-id="d5718-130">現在，返回 Azure 入口網站以取得連接字串資訊，並將它複製到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d5718-130">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="d5718-131">在 [Azure 入口網站](http://portal.azure.com/)中，於您 Azure Cosmos DB 帳戶的左側瀏覽區中，按一下 [金鑰]，然後按一下 [讀寫金鑰]。</span><span class="sxs-lookup"><span data-stu-id="d5718-131">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="d5718-132">在下一個步驟中，您將使用畫面右側的複製按鈕，將 URI 和主要金鑰複製到 `DocumentDBGetStarted.py` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d5718-132">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `DocumentDBGetStarted.py` file in the next step.</span></span>

    ![在 Azure 入口網站的 [金鑰] 刀鋒視窗中檢視並複製存取金鑰](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="d5718-134">開啟 `DocumentDBGetStarted.py` 檔案。</span><span class="sxs-lookup"><span data-stu-id="d5718-134">In Open the `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="d5718-135">從入口網站複製您的 URI 值 (使用 [複製] 按鈕)，並使它成為 `DocumentDBGetStarted.py` 中的端點金鑰值。</span><span class="sxs-lookup"><span data-stu-id="d5718-135">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="d5718-136">然後，從入口網站複製您的主要金鑰值，並使它成為 `DocumentDBGetStarted.py` 中的 `config.MASTERKEY` 值。</span><span class="sxs-lookup"><span data-stu-id="d5718-136">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="d5718-137">您現已更新應用程式，使其具有與 Azure Cosmos DB 通訊所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="d5718-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="d5718-138">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d5718-138">Run the app</span></span>
1. <span data-ttu-id="d5718-139">在 Visual Studio 中，於 [方案總管] 中的專案上按一下滑鼠右鍵，選取目前的 Python 環境，然後按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="d5718-139">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span></span>

2. <span data-ttu-id="d5718-140">選取 [安裝 Python 套件]，然後輸入 **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="d5718-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="d5718-141">按 F5 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5718-141">Run F5 to run the application.</span></span> <span data-ttu-id="d5718-142">您的應用程式會顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="d5718-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="d5718-143">您現在可以返回 [資料總管]，以查看、查詢、修改及使用這項新資料。</span><span class="sxs-lookup"><span data-stu-id="d5718-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="d5718-144">在 Azure 入口網站中檢閱 SLA</span><span class="sxs-lookup"><span data-stu-id="d5718-144">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="d5718-145">清除資源</span><span class="sxs-lookup"><span data-stu-id="d5718-145">Clean up resources</span></span>

<span data-ttu-id="d5718-146">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="d5718-146">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="d5718-147">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5718-147">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="d5718-148">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="d5718-148">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5718-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5718-149">Next steps</span></span>

<span data-ttu-id="d5718-150">在本快速入門中，您已了解如何建立 Azure Cosmos DB 帳戶、如何使用 [資料總管] 建立集合，以及如何執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5718-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="d5718-151">您現在可以將其他資料匯入到 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5718-151">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5718-152">將資料匯入 DocumentDB API 的 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d5718-152">Import data into Azure Cosmos DB for the DocumentDB API</span></span>](import-data.md)


