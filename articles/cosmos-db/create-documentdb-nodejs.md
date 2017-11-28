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
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="b0a2d-103">Azure Cosmos DB： 建置 Node.js DocumentDB API 應用程式和 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b0a2d-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="b0a2d-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b0a2d-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b0a2d-106">本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="b0a2d-107">然後建置並執行主控台應用程式根據 hello [DocumentDB Node.js 應用程式開發介面](documentdb-sdk-node.md)。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0a2d-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="b0a2d-108">Prerequisites</span></span>

* <span data-ttu-id="b0a2d-109">您可以執行此範例之前，您必須擁有下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="b0a2d-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="b0a2d-110">[Node.js](https://nodejs.org/en/) v0.10.29 版或更高版本</span><span class="sxs-lookup"><span data-stu-id="b0a2d-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="b0a2d-111">Git</span><span class="sxs-lookup"><span data-stu-id="b0a2d-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b0a2d-112">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="b0a2d-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="b0a2d-113">新增集合</span><span class="sxs-lookup"><span data-stu-id="b0a2d-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="b0a2d-114">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="b0a2d-114">Clone hello sample application</span></span>

<span data-ttu-id="b0a2d-115">現在讓我們從 github，複製 DocumentDB API 應用程式設定 hello 連接字串，並執行它。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="b0a2d-116">您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="b0a2d-117">開啟 git 終端機視窗，例如 git bash 和`CD`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="b0a2d-118">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="b0a2d-119">檢閱 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="b0a2d-119">Review hello code</span></span>

<span data-ttu-id="b0a2d-120">讓我們進行快速檢閱 hello 應用程式中的情況。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="b0a2d-121">開啟 hello`app.js`檔案，並尋找這行程式碼建立 hello Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b0a2d-122">hello`documentClient`已初始化。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="b0a2d-123">已建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="b0a2d-124">已建立新集合。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="b0a2d-125">已建立一些文件。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="b0a2d-126">已透過 JSON 執行 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-126">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="b0a2d-127">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="b0a2d-127">Update your connection string</span></span>

<span data-ttu-id="b0a2d-128">現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="b0a2d-129">在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="b0a2d-130">您將使用 hello 複製按鈕 hello 右邊 hello 螢幕 toocopy hello URI 和主索引鍵到 hello `config.js` hello 下一個步驟中的檔案。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="b0a2d-132">在開啟 hello`config.js`檔案。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="b0a2d-133">從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello hello 端點中的索引鍵的值`config.js`。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="b0a2d-134">然後從 hello 入口網站複製您的主索引鍵的值，並讓它 hello 值 hello`config.primaryKey`中`config.js`。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="b0a2d-135">您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="b0a2d-136">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="b0a2d-136">Run hello app</span></span>
1. <span data-ttu-id="b0a2d-137">執行`npm install`終端機 tooinstall 中所需的 npm 模組</span><span class="sxs-lookup"><span data-stu-id="b0a2d-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="b0a2d-138">執行`node app.js`中終端機 toostart 應用程式節點。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="b0a2d-139">您現在可以返回 tooData 總管和看到查詢、 修改及使用這個新的資料。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="b0a2d-140">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="b0a2d-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b0a2d-141">清除資源</span><span class="sxs-lookup"><span data-stu-id="b0a2d-141">Clean up resources</span></span>

<span data-ttu-id="b0a2d-142">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b0a2d-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="b0a2d-143">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b0a2d-144">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0a2d-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0a2d-145">Next steps</span></span>

<span data-ttu-id="b0a2d-146">本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立集合，使用 hello 資料總管和執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="b0a2d-147">您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0a2d-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b0a2d-148">將資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b0a2d-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


