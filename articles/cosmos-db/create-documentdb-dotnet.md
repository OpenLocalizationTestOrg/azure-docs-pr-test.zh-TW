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
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="6fdc6-103">Azure Cosmos DB： 建置 DocumentDB API web 應用程式的.NET 和 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6fdc6-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="6fdc6-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="6fdc6-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="6fdc6-106">本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="6fdc6-107">然後會建置並部署 hello 上建置 todo 清單 web 應用程式[DocumentDB.NET API](documentdb-sdk-dotnet.md)hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![具有範例資料的待辦事項應用程式](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="6fdc6-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="6fdc6-109">Prerequisites</span></span>

<span data-ttu-id="6fdc6-110">如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="6fdc6-111">請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="6fdc6-112">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="6fdc6-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="6fdc6-113">新增集合</span><span class="sxs-lookup"><span data-stu-id="6fdc6-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="6fdc6-114">新增範例資料</span><span class="sxs-lookup"><span data-stu-id="6fdc6-114">Add sample data</span></span>

<span data-ttu-id="6fdc6-115">您現在可以新增使用資料總管資料 tooyour 新集合。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="6fdc6-116">在 Data 總管 hello 新資料庫會出現在 hello 集合 窗格。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="6fdc6-117">展開 hello**工作**資料庫中，展開 hello**項目**集合中，按一下 **文件**，然後按一下**新文件**。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Hello Azure 入口網站中，資料檔案總管中建立新文件](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="6fdc6-119">現在加入文件 toohello 集合具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="6fdc6-120">一旦您已經新增 hello json toohello**文件**索引標籤上，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![複製中 json 資料，並將其 hello Azure 入口網站中按一下 儲存資料檔案總管中](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="6fdc6-122">建立並儲存多個一份文件，您可以在該處插入 hello 的唯一值`id`屬性，並適當地 hello 其他屬性的變更。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="6fdc6-123">新文件可擁有您想要的任何結構，因為 Azure Cosmos DB 不會對您的資料強加任何結構描述。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="6fdc6-124">您現在可以使用資料總管 tooretrieve 中的查詢資料。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="6fdc6-125">根據預設，使用資料總管`SELECT * FROM c`tooretrieve 所有文件 hello 集合，但您可以變更該 tooa 不同[SQL 查詢](documentdb-sql-query.md)，例如`SELECT * FROM c ORDER BY c._ts DESC`，tooreturn 所有 hello 文件，以遞減順序都基礎依時間戳記。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="6fdc6-126">您也可以使用資料總管 toocreate 預存程序，Udf，觸發程序 tooperform 伺服器端商務邏輯也做為標尺的輸送量。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="6fdc6-127">資料總管會公開所有 hello 程式設計的內建資料存取提供 hello Api，但提供讓您輕鬆存取 tooyour 資料 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="6fdc6-128">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="6fdc6-128">Clone hello sample application</span></span>

<span data-ttu-id="6fdc6-129">現在讓我們來切換 tooworking 與程式碼。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="6fdc6-130">讓我們複製從 GitHub 設定 hello 連接字串，並執行它的 DocumentDB API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="6fdc6-131">您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="6fdc6-132">開啟 git 終端機視窗，例如 git bash 和`CD`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="6fdc6-133">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="6fdc6-134">然後在 Visual Studio 中開啟 hello todo 方案檔。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="6fdc6-135">檢閱 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="6fdc6-135">Review hello code</span></span>

<span data-ttu-id="6fdc6-136">讓我們進行快速檢閱 hello 應用程式中的情況。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="6fdc6-137">開啟 hello DocumentDBRepository.cs 檔案，而且您會發現這行程式碼建立 hello Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="6fdc6-138">hello DocumentClient 會初始化該行 73。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="6fdc6-139">已在行 88 上建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="6fdc6-140">已在行 107 上建立新集合。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="6fdc6-141">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="6fdc6-141">Update your connection string</span></span>

<span data-ttu-id="6fdc6-142">現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="6fdc6-143">在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="6fdc6-144">您將使用 hello 複製按鈕右邊 hello hello 螢幕 toocopy hello URI 和主索引鍵到 hello hello 下一個步驟中的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="6fdc6-146">在 Visual Studio 2017，開啟 hello web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="6fdc6-147">從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello web.config 中的 hello 端點索引鍵的值。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="6fdc6-148">然後從 hello 入口網站複製您的主索引鍵的值，並讓它 hello hello authKey web.config 中的值。您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="6fdc6-149">執行 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6fdc6-149">Run hello web app</span></span>
1. <span data-ttu-id="6fdc6-150">在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="6fdc6-151">在 hello NuGet**瀏覽**方塊中，輸入*DocumentDB*。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="6fdc6-152">從 hello 結果中，安裝 hello **Microsoft.Azure.DocumentDB**程式庫。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="6fdc6-153">這會安裝 hello Microsoft.Azure.DocumentDB 封裝，以及所有相依性。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="6fdc6-154">按一下 CTRL + F5 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="6fdc6-155">您的應用程式會顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="6fdc6-156">按一下**新建**在 hello 瀏覽器，並在您的待辦事項應用程式中建立一些新的工作。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![具有範例資料的待辦事項應用程式](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="6fdc6-158">您現在可以返回 tooData 總管和看到查詢、 修改及使用這個新的資料。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="6fdc6-159">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="6fdc6-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="6fdc6-160">清除資源</span><span class="sxs-lookup"><span data-stu-id="6fdc6-160">Clean up resources</span></span>

<span data-ttu-id="6fdc6-161">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6fdc6-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="6fdc6-162">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="6fdc6-163">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fdc6-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6fdc6-164">Next steps</span></span>

<span data-ttu-id="6fdc6-165">本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立集合，使用 hello 資料總管和執行 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="6fdc6-166">您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6fdc6-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6fdc6-167">將資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6fdc6-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


