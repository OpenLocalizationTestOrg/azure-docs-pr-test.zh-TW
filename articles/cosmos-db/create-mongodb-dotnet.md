---
title: "Azure Cosmos DB： 建置 web 應用程式的.NET 和 hello MongoDB API |Microsoft 文件"
description: "提供.NET 程式碼範例，您可以使用 tooconnect tooand 查詢 hello Azure Cosmos DB MongoDB API"
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="2a468-103">Azure Cosmos DB： 建置 MongoDB API web 應用程式的.NET 和 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2a468-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="2a468-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="2a468-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="2a468-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="2a468-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="2a468-106">本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2a468-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="2a468-107">然後會建置並部署 hello 上建立工作清單 web 應用程式[MongoDB.NET 驅動程式](https://docs.mongodb.com/ecosystem/drivers/csharp/)。</span><span class="sxs-lookup"><span data-stu-id="2a468-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2a468-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a468-108">Prerequisites</span></span>

<span data-ttu-id="2a468-109">如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="2a468-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="2a468-110">請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。</span><span class="sxs-lookup"><span data-stu-id="2a468-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="2a468-111">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="2a468-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="2a468-112">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="2a468-112">Clone hello sample application</span></span>

<span data-ttu-id="2a468-113">現在讓我們從 github，複製 MongoDB API 應用程式設定 hello 連接字串，並執行它。</span><span class="sxs-lookup"><span data-stu-id="2a468-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="2a468-114">您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="2a468-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="2a468-115">開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="2a468-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="2a468-116">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="2a468-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="2a468-117">然後在 Visual Studio 中開啟 hello 方案檔。</span><span class="sxs-lookup"><span data-stu-id="2a468-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="2a468-118">檢閱 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="2a468-118">Review hello code</span></span>

<span data-ttu-id="2a468-119">讓我們進行快速檢閱 hello 應用程式中的情況。</span><span class="sxs-lookup"><span data-stu-id="2a468-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="2a468-120">開啟 hello **Dal.cs**下 hello 檔案**DAL**目錄，您會發現這行程式碼建立 hello Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="2a468-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="2a468-121">初始化 hello Mongo 用戶端。</span><span class="sxs-lookup"><span data-stu-id="2a468-121">Initialize hello Mongo Client.</span></span>

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

* <span data-ttu-id="2a468-122">擷取 hello 資料庫與 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="2a468-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="2a468-123">擷取所有文件。</span><span class="sxs-lookup"><span data-stu-id="2a468-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="2a468-124">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="2a468-124">Update your connection string</span></span>

<span data-ttu-id="2a468-125">現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a468-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="2a468-126">在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**連接字串**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="2a468-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="2a468-127">您將使用 hello 複製按鈕右邊 hello hello 螢幕 toocopy hello 使用者名稱、 密碼和主機到 hello 下一個步驟中的 hello Dal.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="2a468-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="2a468-128">開啟 hello **Dal.cs**檔案在 hello **DAL**目錄。</span><span class="sxs-lookup"><span data-stu-id="2a468-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="2a468-129">複製您**username**來自 hello 入口網站 （使用 hello [複製] 按鈕） 的值，並將其 hello 值 hello**使用者名稱**中您**Dal.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="2a468-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="2a468-130">然後將複製程式**主機**值從 hello 入口網站，並將其 hello hello 值**主機**中您**Dal.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="2a468-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="2a468-131">最後將複製程式**密碼**值從 hello 入口網站，並將其 hello 值 hello**密碼**中您**Dal.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="2a468-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="2a468-132">您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="2a468-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="2a468-133">執行 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2a468-133">Run hello web app</span></span>

1. <span data-ttu-id="2a468-134">在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="2a468-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="2a468-135">在 hello NuGet**瀏覽**方塊中，輸入*MongoDB.Driver*。</span><span class="sxs-lookup"><span data-stu-id="2a468-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="2a468-136">從 hello 結果中，安裝 hello **MongoDB.Driver**程式庫。</span><span class="sxs-lookup"><span data-stu-id="2a468-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="2a468-137">這會安裝 hello MongoDB.Driver 封裝，以及所有相依性。</span><span class="sxs-lookup"><span data-stu-id="2a468-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="2a468-138">按一下 CTRL + F5 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a468-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="2a468-139">您的應用程式會顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="2a468-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="2a468-140">按一下**建立**入 hello 瀏覽器，並建立工作清單應用程式中的幾項新工作。</span><span class="sxs-lookup"><span data-stu-id="2a468-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="2a468-141">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="2a468-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="2a468-142">清除資源</span><span class="sxs-lookup"><span data-stu-id="2a468-142">Clean up resources</span></span>

<span data-ttu-id="2a468-143">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2a468-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="2a468-144">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2a468-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="2a468-145">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="2a468-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a468-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a468-146">Next steps</span></span>

<span data-ttu-id="2a468-147">本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶和執行 web 應用程式使用 hello API MongoDB。</span><span class="sxs-lookup"><span data-stu-id="2a468-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="2a468-148">您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2a468-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a468-149">資料匯入至 Azure Cosmos DB hello MongoDB 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="2a468-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

