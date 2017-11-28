---
title: "aaaBuild Azure Cosmos DB Node.js 應用程式使用 Graph API |Microsoft 文件"
description: "顯示您可以使用 tooconnect tooand Node.js 的程式碼範例會查詢 Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="9cd4b-103">Azure Cosmos DB：使用圖形 API 來建置 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="9cd4b-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="9cd4b-104">Azure 的 Cosmos DB 是來自 Microsoft 的全域散發的 hello 多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-104">Azure Cosmos DB is hello globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="9cd4b-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="9cd4b-106">快速入門本文示範如何 toocreate Azure Cosmos DB 說明 Graph API （預覽）、 資料庫和圖形使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-106">This quick-start article demonstrates how toocreate an Azure Cosmos DB account for Graph API (preview), database, and graph by using hello Azure portal.</span></span> <span data-ttu-id="9cd4b-107">然後建置並執行主控台應用程式使用 hello 開放原始碼[Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure)驅動程式。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-107">You then build and run a console app by using hello open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="9cd4b-108">hello npm 模組`gremlin-secure`是修改的版`gremlin`模組，但是有 SSL 和 SASL Azure Cosmos DB 連接所需的支援。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-108">hello npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="9cd4b-109">原始程式碼位於 [GitHub](https://github.com/CosmosDB/gremlin-javascript)。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="9cd4b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9cd4b-110">Prerequisites</span></span>

<span data-ttu-id="9cd4b-111">您可以執行此範例之前，您必須擁有下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="9cd4b-111">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="9cd4b-112">[Node.js](https://nodejs.org/en/) 0.10.29 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="9cd4b-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="9cd4b-113">Git</span><span class="sxs-lookup"><span data-stu-id="9cd4b-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="9cd4b-114">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="9cd4b-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="9cd4b-115">新增圖形</span><span class="sxs-lookup"><span data-stu-id="9cd4b-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="9cd4b-116">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="9cd4b-116">Clone hello sample application</span></span>

<span data-ttu-id="9cd4b-117">現在讓我們從 GitHub，複製 Graph API 應用程式設定 hello 連接字串，並執行它。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-117">Now let's clone a Graph API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="9cd4b-118">您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-118">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="9cd4b-119">開啟 Git 終端機視窗，例如 Git Bash，並將變更 (透過`cd`命令) tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) tooa working directory.</span></span>  

2. <span data-ttu-id="9cd4b-120">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="9cd4b-121">開啟 Visual Studio 中的 hello 方案檔。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-121">Open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="9cd4b-122">檢閱 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="9cd4b-122">Review hello code</span></span>

<span data-ttu-id="9cd4b-123">讓我們進行快速檢閱 hello 應用程式中的情況。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-123">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="9cd4b-124">開啟 hello`app.js`檔案，而且您會發現下列幾行程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-124">Open hello `app.js` file, and you'll find hello following lines of code.</span></span> 

* <span data-ttu-id="9cd4b-125">hello Gremlin 用戶端會建立。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-125">hello Gremlin client is created.</span></span>

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  <span data-ttu-id="9cd4b-126">hello 組態都位於`config.js`，我們在 hello 下列區段中編輯。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-126">hello configurations are all in `config.js`, which we edit in hello following section.</span></span>

* <span data-ttu-id="9cd4b-127">一系列的 Gremlin 步驟會執行以 hello`client.execute`方法。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-127">A series of Gremlin steps are executed with hello `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="9cd4b-128">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="9cd4b-128">Update your connection string</span></span>

1. <span data-ttu-id="9cd4b-129">開啟 hello config.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-129">Open hello config.js file.</span></span> 

2. <span data-ttu-id="9cd4b-130">在 config.js，填入 hello config.endpoint 金鑰以 hello **Gremlin URI**值從 hello**概觀**hello Azure 入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-130">In config.js, fill in hello config.endpoint key with hello **Gremlin URI** value from hello **Overview** page of hello Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="9cd4b-132">如果 hello **Gremlin URI**值是空的您可以從 hello 產生 hello 值**金鑰**hello 使用入口網站中，hello 頁面**URI**移除 https:// 以及變更的值文件 toographs。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-132">If hello **Gremlin URI** value is blank, you can generate hello value from hello **Keys** page in hello portal, using hello **URI** value, removing https://, and changing documents toographs.</span></span>

   <span data-ttu-id="9cd4b-133">hello Gremlin 端點必須只有 hello 主機名稱，如果沒有 hello 通訊協定/連接埠號碼，例如`mygraphdb.graphs.azure.com`(不`https://mygraphdb.graphs.azure.com`或`mygraphdb.graphs.azure.com:433`)。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-133">hello Gremlin endpoint must be only hello host name without hello protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="9cd4b-134">在 config.js，填入 hello config.primaryKey 值入 hello**主索引鍵**值從 hello**金鑰**hello Azure 入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-134">In config.js, fill in hello config.primaryKey value in with hello **Primary Key** value from hello **Keys** page of hello Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![hello Azure 入口網站的索引鍵刀鋒伺服器](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="9cd4b-136">輸入 hello 資料庫名稱，以及 config.database 和 config.collection hello 值 （容器） 的圖形名稱。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-136">Enter hello database name, and graph (container) name for hello value of config.database and config.collection.</span></span> 

<span data-ttu-id="9cd4b-137">您完成的 config.js 檔案範例應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="9cd4b-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a><span data-ttu-id="9cd4b-138">執行 hello 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="9cd4b-138">Run hello console app</span></span>

1. <span data-ttu-id="9cd4b-139">開啟 終端機視窗，並變更 (透過`cd`命令) toohello hello 專案中所包含的 hello package.json 檔案的安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-139">Open a terminal window and change (via `cd` command) toohello installation directory for hello package.json file that's included in hello project.</span></span>  

2. <span data-ttu-id="9cd4b-140">執行`npm install`tooinstall hello 所需的 npm 模組，包括`gremlin-secure`。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-140">Run `npm install` tooinstall hello required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="9cd4b-141">執行`node app.js`中終端機 toostart 應用程式節點。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-141">Run `node app.js` in a terminal toostart your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="9cd4b-142">使用資料總管進行瀏覽</span><span class="sxs-lookup"><span data-stu-id="9cd4b-142">Browse with Data Explorer</span></span>

<span data-ttu-id="9cd4b-143">現在可以移回 tooData 總管在 Azure 入口網站 tooview hello、 查詢、 修改及使用新的圖形資料。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-143">You can now go back tooData Explorer in hello Azure portal tooview, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="9cd4b-144">在 Data 總管 hello 新資料庫會出現在 hello**圖形**窗格。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-144">In Data Explorer, hello new database appears in hello **Graphs** pane.</span></span> <span data-ttu-id="9cd4b-145">展開 hello 資料庫，後面接著 hello 集合，然後按一下 **圖形**。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-145">Expand hello database, followed by hello collection, then click **Graph**.</span></span>

<span data-ttu-id="9cd4b-146">hello hello 範例應用程式所產生的資料會顯示在 hello hello 內的下一個窗格**圖形**索引標籤上，當您按一下**套用篩選**。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-146">hello data generated by hello sample app is displayed in hello next pane within hello **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="9cd4b-147">請嘗試完成`g.V()`與`.has('firstName', 'Thomas')`tootest hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` tootest hello filter.</span></span> <span data-ttu-id="9cd4b-148">請注意 hello 值會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-148">Do note that hello value is case sensitive.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="9cd4b-149">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="9cd4b-149">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="9cd4b-150">清除資源</span><span class="sxs-lookup"><span data-stu-id="9cd4b-150">Clean up your resources</span></span>

<span data-ttu-id="9cd4b-151">如果您不打算使用此應用程式的 toocontinue，刪除您建立這份文件中執行 hello 下列的所有資源：</span><span class="sxs-lookup"><span data-stu-id="9cd4b-151">If you do not plan toocontinue using this app, delete all resources that you created in this article by doing hello following:</span></span> 

1. <span data-ttu-id="9cd4b-152">在 hello Azure 入口網站，在 hello 左的導覽功能表上，按一下 **資源群組**，然後按一下您所建立的 hello 資源 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-152">In hello Azure portal, on hello left navigation menu, click **Resource groups**, and then click hello name of hello resource that you created.</span></span> 
2. <span data-ttu-id="9cd4b-153">在資源群組頁面上，按一下 **刪除**，輸入 hello hello 資源 toobe 刪除，名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-153">On your resource group page, click **Delete**, type hello name of hello resource toobe deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cd4b-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9cd4b-154">Next steps</span></span>

<span data-ttu-id="9cd4b-155">在本文中，您學到如何 toocreate Azure Cosmos DB 帳戶，使用資料總管 中，建立的圖形和執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-155">In this article, you've learned how toocreate an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="9cd4b-156">您現在可以使用 Gremlin 來建置更複雜的查詢，以及實作強大的圖形周遊邏輯。</span><span class="sxs-lookup"><span data-stu-id="9cd4b-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9cd4b-157">使用 Gremlin 進行查詢</span><span class="sxs-lookup"><span data-stu-id="9cd4b-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
