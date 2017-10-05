---
title: "Azure CosmosDB︰使用 .NET 和 MongoDB API 建置 Web 應用程式 | Microsoft Docs"
description: "提供 .NET 程式碼範例，您可用來連線及查詢 Azure Cosmos DB MongoDB API"
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
ms.openlocfilehash: 2d30bec75d701b1fd55355d1e139350b6d828c9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="c0e09-103">Azure CosmosDB︰使用 .NET 和 Azure 入口網站建置 MongoDB API Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c0e09-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="c0e09-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="c0e09-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c0e09-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="c0e09-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c0e09-106">本快速入門會示範如何使用 Azure 入口網站建立 Azure Cosmos DB 帳戶、文件資料庫和集合。</span><span class="sxs-lookup"><span data-stu-id="c0e09-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="c0e09-107">您會接著建置和部署以 [MongoDB .NET 驅動程式](https://docs.mongodb.com/ecosystem/drivers/csharp/)為基礎的工作清單 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0e09-107">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c0e09-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c0e09-108">Prerequisites</span></span>

<span data-ttu-id="c0e09-109">如果尚未安裝 Visual Studio 2017，您可以下載並使用**免費的** [Visual Studio 2017 Community 版本](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="c0e09-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="c0e09-110">務必在 Visual Studio 設定期間啟用 **Azure 開發**。</span><span class="sxs-lookup"><span data-stu-id="c0e09-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="c0e09-111">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="c0e09-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="c0e09-112">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="c0e09-112">Clone the sample application</span></span>

<span data-ttu-id="c0e09-113">現在，我們將從 Github 複製 MongoDB API 應用程式、設定連接字串，然後執行它。</span><span class="sxs-lookup"><span data-stu-id="c0e09-113">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="c0e09-114">您會看到，以程式設計方式來處理資料有多麼的容易。</span><span class="sxs-lookup"><span data-stu-id="c0e09-114">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="c0e09-115">開啟 Git 終端機視窗 (例如 Git Bash)，然後使用 `cd` 來切換到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="c0e09-115">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="c0e09-116">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="c0e09-116">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="c0e09-117">然後在 Visual Studio 中開啟方案檔案。</span><span class="sxs-lookup"><span data-stu-id="c0e09-117">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="c0e09-118">檢閱程式碼</span><span class="sxs-lookup"><span data-stu-id="c0e09-118">Review the code</span></span>

<span data-ttu-id="c0e09-119">讓我們快速檢閱應用程式中所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="c0e09-119">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="c0e09-120">請開啟 **DAL** 目錄之下的 **Dal.cs** 檔案，您會發現這些程式碼行會建立 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="c0e09-120">Open the **Dal.cs** file under the **DAL** directory and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="c0e09-121">初始化 Mongo 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c0e09-121">Initialize the Mongo Client.</span></span>

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

* <span data-ttu-id="c0e09-122">擷取資料庫和集合。</span><span class="sxs-lookup"><span data-stu-id="c0e09-122">Retrieve the database and the collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="c0e09-123">擷取所有文件。</span><span class="sxs-lookup"><span data-stu-id="c0e09-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="c0e09-124">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="c0e09-124">Update your connection string</span></span>

<span data-ttu-id="c0e09-125">現在，返回 Azure 入口網站以取得連接字串資訊，並將它複製到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="c0e09-125">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="c0e09-126">在 [Azure 入口網站](http://portal.azure.com/)中，於您 Azure Cosmos DB 帳戶的左側瀏覽區中，按一下 [連接字串]，然後按一下 [讀寫金鑰]。</span><span class="sxs-lookup"><span data-stu-id="c0e09-126">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="c0e09-127">在下一個步驟中，您將使用畫面右側的複製按鈕，將使用者名稱、密碼和主機複製到 Dal.cs 檔案中。</span><span class="sxs-lookup"><span data-stu-id="c0e09-127">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="c0e09-128">開啟 **DAL** 目錄中的 **Dal.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="c0e09-128">Open the **Dal.cs** file in the **DAL** directory.</span></span> 

3. <span data-ttu-id="c0e09-129">從入口網站複製您的 **username** 值 (使用 [複製] 按鈕)，並使它成為 **Dal.cs** 檔案中的 **username** 值。</span><span class="sxs-lookup"><span data-stu-id="c0e09-129">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="c0e09-130">然後從入口網站複製您的 **host** 值，並使它成為 **Dal.cs** 檔案中的 **host** 值。</span><span class="sxs-lookup"><span data-stu-id="c0e09-130">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="c0e09-131">最後從入口網站複製您的 **password** 值，並使它成為 **Dal.cs** 檔案中的 **password** 值。</span><span class="sxs-lookup"><span data-stu-id="c0e09-131">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="c0e09-132">您現已更新應用程式，使其具有與 Azure Cosmos DB 通訊所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="c0e09-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-web-app"></a><span data-ttu-id="c0e09-133">執行 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c0e09-133">Run the web app</span></span>

1. <span data-ttu-id="c0e09-134">在 Visual Studio 中，於 [方案總管] 中的專案上按一下滑鼠右鍵，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="c0e09-134">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="c0e09-135">在 NuGet [瀏覽] 方塊中，輸入 MongoDB.Driver。</span><span class="sxs-lookup"><span data-stu-id="c0e09-135">In the NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="c0e09-136">從結果中，安裝 **MongoDB.Driver** 程式庫。</span><span class="sxs-lookup"><span data-stu-id="c0e09-136">From the results, install the **MongoDB.Driver** library.</span></span> <span data-ttu-id="c0e09-137">這會安裝 MongoDB.Driver 套件以及所有相依性。</span><span class="sxs-lookup"><span data-stu-id="c0e09-137">This installs the MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="c0e09-138">按 CTRL + F5 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0e09-138">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="c0e09-139">您的應用程式會顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="c0e09-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="c0e09-140">按一下瀏覽器中的 [建立]，然後在您的工作清單應用程式中建立一些新工作。</span><span class="sxs-lookup"><span data-stu-id="c0e09-140">Click **Create** in the browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="c0e09-141">在 Azure 入口網站中檢閱 SLA</span><span class="sxs-lookup"><span data-stu-id="c0e09-141">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c0e09-142">清除資源</span><span class="sxs-lookup"><span data-stu-id="c0e09-142">Clean up resources</span></span>

<span data-ttu-id="c0e09-143">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="c0e09-143">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="c0e09-144">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="c0e09-144">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="c0e09-145">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c0e09-145">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0e09-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0e09-146">Next steps</span></span>

<span data-ttu-id="c0e09-147">在本快速入門中，您已了解如何建立 Azure Cosmos DB 帳戶，以及如何使用適用於 MongoDB 的 API 來執行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0e09-147">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span></span> <span data-ttu-id="c0e09-148">您現在可以將其他資料匯入到 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c0e09-148">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0e09-149">將資料匯入 MongoDB API 的 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c0e09-149">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)

