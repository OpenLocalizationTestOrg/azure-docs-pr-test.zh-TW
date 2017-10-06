---
title: "Azure CosmosDB︰使用 Xamarin 和 Facebook 驗證建置 Web 應用程式 | Microsoft Docs"
description: "提供.NET 程式碼範例中，您可以使用 tooconnect tooand 查詢 Azure Cosmos DB"
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
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="7a9b4-103">Azure CosmosDB︰使用 .NET、Xamarin 和 Facebook 驗證建置 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a9b4-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="7a9b4-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7a9b4-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7a9b4-106">本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="7a9b4-107">然後會建置並部署 hello 上建置 todo 清單 web 應用程式[DocumentDB.NET API](documentdb-sdk-dotnet.md)， [Xamarin](https://www.xamarin.com/)，和 hello Azure Cosmos DB 授權引擎。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="7a9b4-108">hello todo 清單 web 應用程式實作每個使用者資料的模式，可讓使用者使用 Facebook 驗證的 toologin 和管理他們自己 toodo 項目。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a9b4-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a9b4-109">Prerequisites</span></span>

<span data-ttu-id="7a9b4-110">如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="7a9b4-111">請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="7a9b4-112">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="7a9b4-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="7a9b4-113">新增集合</span><span class="sxs-lookup"><span data-stu-id="7a9b4-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="7a9b4-114">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="7a9b4-114">Clone hello sample application</span></span>

<span data-ttu-id="7a9b4-115">現在讓我們從 github，複製 DocumentDB API 應用程式設定 hello 連接字串，並執行它。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="7a9b4-116">您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="7a9b4-117">開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="7a9b4-118">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="7a9b4-119">從 Visual Studio 中的 hello samples/xamarin/UserItems/xamarin.forms 資料夾，然後開啟 hello DocumentDBTodo.sln 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="7a9b4-120">檢閱 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="7a9b4-120">Review hello code</span></span>

<span data-ttu-id="7a9b4-121">hello hello Xamarin 資料夾中的程式碼包含：</span><span class="sxs-lookup"><span data-stu-id="7a9b4-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="7a9b4-122">Xamarin 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-122">Xamarin app.</span></span> <span data-ttu-id="7a9b4-123">hello 應用程式儲存在名為 UserItems 的分割區集合中的 hello 使用者的 todo 項目。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="7a9b4-124">資源權杖訊息代理程式 API。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-124">Resource token broker API.</span></span> <span data-ttu-id="7a9b4-125">簡單的 ASP.NET Web API toobroker Azure Cosmos DB 資源語彙基元 toohello 登入的 hello 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="7a9b4-126">資源語彙基元是存留較短的存取權杖，hello 應用程式提供 hello 存取 toohello 登入使用者的資料。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="7a9b4-127">hello 驗證和資料流程以 hello 如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="7a9b4-128">hello UserItems 集合會透過 hello 資料分割索引鍵 ' / userid'。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="7a9b4-129">指定集合的資料分割索引鍵可讓 Azure Cosmos DB tooscale 無限 hello 數字的使用者和項目會成長。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="7a9b4-130">hello Xamarin 應用程式可讓使用者 toologin 使用 Facebook 的認證。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="7a9b4-131">hello Xamarin 應用程式使用 Facebook 存取權杖 tooauthenticate 具有 ResourceTokenBroker 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="7a9b4-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="7a9b4-132">hello 資源語彙基元 broker API 驗證 hello 要求使用應用程式服務驗證功能，並要求 Azure Cosmos DB 資源權杖的讀取/寫入存取 tooall 文件共用 hello 經驗證的使用者資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="7a9b4-133">資源語彙基元 broker 傳回 hello 資源語彙基元 toohello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="7a9b4-134">hello 應用程式存取使用 hello 資源語彙基元的 hello 使用者的 todo 項目。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![具有範例資料的待辦事項應用程式](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="7a9b4-136">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="7a9b4-136">Update your connection string</span></span>

<span data-ttu-id="7a9b4-137">現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="7a9b4-138">在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="7a9b4-139">您將使用 hello 複製按鈕右邊 hello hello 螢幕 toocopy hello URI 和主索引鍵到 hello hello 下一個步驟中的 Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="7a9b4-141">在 Visual Studio 2017，開啟 hello hello azure-documentdb-dotnet/範例/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker 資料夾中的 Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="7a9b4-142">從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello hello accountUrl Web.config 中的值。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="7a9b4-143">然後從 hello 入口網站複製您的主索引鍵的值，並讓它 hello hello accountKey Web.congif 中的值。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="7a9b4-144">您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="7a9b4-145">建置和部署 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a9b4-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="7a9b4-146">在 hello Azure 入口網站，建立應用程式服務網站 toohost hello 資源語彙基元 broker 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="7a9b4-147">在 hello Azure 入口網站，開啟 hello hello 資源語彙基元 broker API 網站的 應用程式設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="7a9b4-148">填寫下列應用程式設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a9b4-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="7a9b4-149">accountUrl-hello Azure Cosmos DB 帳戶 URL 從您的 Azure Cosmos DB 帳戶 hello 金鑰 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="7a9b4-150">accountKey-hello Azure Cosmos DB 帳戶從您的 Azure Cosmos DB 帳戶 hello 金鑰 索引標籤的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="7a9b4-151">已建立之資料庫和集合的 databaseId 和 collectionId</span><span class="sxs-lookup"><span data-stu-id="7a9b4-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="7a9b4-152">發行 hello ResourceTokenBroker 方案 tooyour 建立網站。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="7a9b4-153">開啟 hello Xamarin 專案，並瀏覽 tooTodoItemManager.cs。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="7a9b4-154">填寫 accountURL、 collectionId、 databaseId，以及 resourceTokenBrokerURL hello 值為 hello 資源語彙基元 broker 網站 hello 基底的 https url。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="7a9b4-155">完整的 hello[如何 tooconfigure 您 App Service 應用程式 toouse Facebook 登入](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)教學課程 toosetup Facebook 驗證和設定 hello ResourceTokenBroker 網站。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="7a9b4-156">執行 hello Xamarin 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="7a9b4-157">在 hello Azure 入口網站中檢視 Sla</span><span class="sxs-lookup"><span data-stu-id="7a9b4-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7a9b4-158">清除資源</span><span class="sxs-lookup"><span data-stu-id="7a9b4-158">Clean up resources</span></span>

<span data-ttu-id="7a9b4-159">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7a9b4-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="7a9b4-160">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您剛才建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="7a9b4-161">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a9b4-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a9b4-162">Next steps</span></span>

<span data-ttu-id="7a9b4-163">本快速入門中，您已經學會 toocreate Azure Cosmos DB 帳戶，建立集合，使用 hello 資料總管和建置和部署的 Xamarin 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="7a9b4-164">您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a9b4-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a9b4-165">將資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7a9b4-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
