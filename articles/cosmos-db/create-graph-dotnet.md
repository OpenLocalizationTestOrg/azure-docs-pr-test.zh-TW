---
title: "使用圖形 API 來建置 Azure Cosmos DB .NET 應用程式 | Microsoft Docs"
description: "提供可用來連線及查詢 Azure Cosmos DB 的 .NET 程式碼範例"
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
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: a973b81ea5b06c5826cc31c399aae9dec43f5b72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-the-graph-api"></a><span data-ttu-id="1a7aa-103">Azure Cosmos DB：使用圖形 API 來建置 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="1a7aa-103">Azure Cosmos DB: Build a .NET application using the Graph API</span></span>

<span data-ttu-id="1a7aa-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1a7aa-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="1a7aa-106">本快速入門會示範如何使用 Azure 入口網站建立 Azure Cosmos DB 帳戶、資料庫和圖形 (容器)。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-106">This quick start demonstrates how to create an Azure Cosmos DB account, database, and graph (container) using the Azure portal.</span></span> <span data-ttu-id="1a7aa-107">您會接著建置和執行以[圖形 API](graph-sdk-dotnet.md) (預覽) 為基礎的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-107">You then build and run a console app built on the [Graph API](graph-sdk-dotnet.md) (preview).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="1a7aa-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="1a7aa-108">Prerequisites</span></span>

<span data-ttu-id="1a7aa-109">如果尚未安裝 Visual Studio 2017，您可以下載並使用**免費的** [Visual Studio 2017 Community 版本](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="1a7aa-110">務必在 Visual Studio 設定期間啟用 **Azure 開發**。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="1a7aa-111">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="1a7aa-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="1a7aa-112">新增圖形</span><span class="sxs-lookup"><span data-stu-id="1a7aa-112">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="1a7aa-113">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="1a7aa-113">Clone the sample application</span></span>

<span data-ttu-id="1a7aa-114">現在，我們將從 Github 複製圖形 API 應用程式、設定連接字串，然後執行它。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-114">Now let's clone a Graph API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="1a7aa-115">您會看到，以程式設計方式來處理資料有多麼的容易。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-115">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="1a7aa-116">開啟 Git 終端機視窗 (例如 Git Bash)，然後使用 `cd` 來切換到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-116">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="1a7aa-117">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-117">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. <span data-ttu-id="1a7aa-118">然後開啟 Visual Studio 並開啟方案檔案。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-118">Then open Visual Studio and open the solution file.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="1a7aa-119">檢閱程式碼</span><span class="sxs-lookup"><span data-stu-id="1a7aa-119">Review the code</span></span>

<span data-ttu-id="1a7aa-120">讓我們快速檢閱應用程式中所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-120">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="1a7aa-121">請開啟 Program.cs 檔案，您會發現這些程式碼行建立 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-121">Open the Program.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="1a7aa-122">已初始化 DocumentClient。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-122">The DocumentClient is initialized.</span></span> <span data-ttu-id="1a7aa-123">在預覽中，我們在 Azure Cosmos DB 用戶端上新增了圖形擴充 API。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-123">In the preview, we added a graph extension API on the Azure Cosmos DB client.</span></span> <span data-ttu-id="1a7aa-124">我們正努力開發與 Azure Cosmos DB 用戶端和資源分離的獨立圖形用戶端。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-124">We are working on a standalone graph client decoupled from the Azure Cosmos DB client and resources.</span></span>

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* <span data-ttu-id="1a7aa-125">已建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-125">A new database is created.</span></span>

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* <span data-ttu-id="1a7aa-126">已建立新圖形。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-126">A new graph is created.</span></span>

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* <span data-ttu-id="1a7aa-127">已使用 `CreateGremlinQuery` 方法執行一系列的 Gremlin 步驟。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-127">A series of Gremlin steps are executed using the `CreateGremlinQuery` method.</span></span>

    ```csharp
    // The CreateGremlinQuery method extensions allow you to execute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="1a7aa-128">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="1a7aa-128">Update your connection string</span></span>

<span data-ttu-id="1a7aa-129">現在，返回 Azure 入口網站以取得連接字串資訊，並將它複製到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="1a7aa-130">在 Visual Studio 2017 中，開啟 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-130">In Visual Studio 2017, open the App.config file.</span></span> 

2. <span data-ttu-id="1a7aa-131">在 Azure 入口網站的 Azure Cosmos DB 帳戶中，按一下左側瀏覽區中的 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-131">In the Azure portal, in your Azure Cosmos DB account, click **Keys** in the left navigation.</span></span> 

    ![在 Azure 入口網站的 [金鑰] 頁面上檢視並複製主要金鑰](./media/create-graph-dotnet/keys.png)

3. <span data-ttu-id="1a7aa-133">從入口網站複製您的 [URI] 值，並使它成為 App.config 中的端點金鑰值。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-133">Copy your **URI** value from the portal and make it the value of the Endpoint key in App.config.</span></span> <span data-ttu-id="1a7aa-134">您可以使用上面螢幕擷取畫面中所示的複製按鈕來複製此值。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-134">You can use the copy button as shown in the preceding screenshot to copy the value.</span></span>

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. <span data-ttu-id="1a7aa-135">從入口網站複製您的**主要金鑰**，並使它成為 App.config 中的 AuthKey 金鑰值，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-135">Copy your **PRIMARY KEY** value from the portal, and make it the value of the AuthKey key in App.config, then save your changes.</span></span> 

    `<add key="AuthKey" value="FILLME" />`

<span data-ttu-id="1a7aa-136">您現已更新應用程式，使其具有與 Azure Cosmos DB 通訊所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-136">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-console-app"></a><span data-ttu-id="1a7aa-137">執行主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="1a7aa-137">Run the console app</span></span>

1. <span data-ttu-id="1a7aa-138">在 Visual Studio 中，於 [方案總管] 中的 [GraphGetStarted] 專案上按一下滑鼠右鍵，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-138">In Visual Studio, right-click on the **GraphGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="1a7aa-139">在 NuGet 的 [瀏覽] 方塊中，輸入 Microsoft.Azure.Graphs，並勾選 [包括發行前版本] 方塊。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-139">In the NuGet **Browse** box, type *Microsoft.Azure.Graphs* and check the **Includes prerelease** box.</span></span> 

3. <span data-ttu-id="1a7aa-140">從結果中，安裝 **Microsoft.Azure.Graphs** 程式庫。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-140">From the results, install the **Microsoft.Azure.Graphs** library.</span></span> <span data-ttu-id="1a7aa-141">這會安裝 Azure Cosmos DB 圖形擴充程式庫套件以及所有相依性。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-141">This installs the Azure Cosmos DB graph extension library package and all dependencies.</span></span>

    <span data-ttu-id="1a7aa-142">如果您收到關於檢閱方案變更的訊息，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-142">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="1a7aa-143">如果您收到關於接受授權的訊息，請按一下 [我接受]。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-143">If you get a message about license acceptance, click **I accept**.</span></span>

4. <span data-ttu-id="1a7aa-144">按 CTRL + F5 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-144">Click CTRL + F5 to run the application.</span></span>

   <span data-ttu-id="1a7aa-145">主控台視窗會顯示將要新增至圖形的頂點和邊緣。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-145">The console window displays the vertexes and edges being added to the graph.</span></span> <span data-ttu-id="1a7aa-146">當指令碼完成時，請按兩次 ENTER 以關閉主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-146">When the script completes, press ENTER twice to close the console window.</span></span> 

## <a name="browse-using-the-data-explorer"></a><span data-ttu-id="1a7aa-147">使用資料總管進行瀏覽</span><span class="sxs-lookup"><span data-stu-id="1a7aa-147">Browse using the Data Explorer</span></span>

<span data-ttu-id="1a7aa-148">您現在可以回到 Azure 入口網站中的 [資料總管]，瀏覽及查詢新的圖形資料。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-148">You can now go back to Data Explorer in the Azure portal and browse and query your new graph data.</span></span>

1. <span data-ttu-id="1a7aa-149">在 [資料總管] 中，新的資料庫會出現在 [圖形] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-149">In Data Explorer, the new database appears in the Graphs pane.</span></span> <span data-ttu-id="1a7aa-150">展開 [graphdb]、[graphcollz]，然後按一下 [圖形]。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-150">Expand **graphdb**, **graphcollz**, and then click **Graph**.</span></span>

2. <span data-ttu-id="1a7aa-151">按一下 [套用篩選條件] 按鈕，以使用預設查詢來檢視圖形中的所有頂點。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-151">Click the **Apply Filter** button to use the default query to view all the verticies in the graph.</span></span> <span data-ttu-id="1a7aa-152">範例應用程式所產生的資料會顯示在 [圖形] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-152">The data generated by the sample app is displayed in the Graphs pane.</span></span>

    <span data-ttu-id="1a7aa-153">您可以縮放圖形、展開圖形顯示空間、新增其他頂點，並在顯示介面上移動頂點。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-153">You can zoom in and out of the graph, you can expand the graph display space, add additional verticies, and move verticies on the display surface.</span></span>

    ![在 Azure 入口網站的資料總管中檢視圖形](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="1a7aa-155">在 Azure 入口網站中檢閱 SLA</span><span class="sxs-lookup"><span data-stu-id="1a7aa-155">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1a7aa-156">清除資源</span><span class="sxs-lookup"><span data-stu-id="1a7aa-156">Clean up resources</span></span>

<span data-ttu-id="1a7aa-157">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="1a7aa-157">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="1a7aa-158">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-158">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="1a7aa-159">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-159">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a7aa-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a7aa-160">Next steps</span></span>

<span data-ttu-id="1a7aa-161">在本快速入門中，您已了解如何建立 Azure Cosmos DB 帳戶、如何使用 [資料總管] 來建立圖形，以及如何執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-161">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="1a7aa-162">您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。</span><span class="sxs-lookup"><span data-stu-id="1a7aa-162">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1a7aa-163">使用 Gremlin 進行查詢</span><span class="sxs-lookup"><span data-stu-id="1a7aa-163">Query using Gremlin</span></span>](tutorial-query-graph.md)

