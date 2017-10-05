---
title: "使用資料表 API 來建置 Azure Cosmos DB .NET 應用程式 | Microsoft Docs"
description: "使用 .NET 來開始使用 Azure Cosmos DB 的資料表 API"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: 29e7eebda5177d6e852ef04ad82d9d38a8d30ed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-the-table-api"></a><span data-ttu-id="bf5c7-103">Azure Cosmos DB：使用資料表 API 來建置 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="bf5c7-103">Azure Cosmos DB: Build a .NET application using the Table API</span></span>

<span data-ttu-id="bf5c7-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="bf5c7-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="bf5c7-106">本快速入門會示範如何建立 Azure Cosmos DB 帳戶，並使用 Azure 入口網站在該帳戶內建立資料表。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-106">This quick start demonstrates how to create an Azure Cosmos DB account, and create a table within that account using the Azure portal.</span></span> <span data-ttu-id="bf5c7-107">接著，您要撰寫程式碼，將實體插入、更新和刪除，然後從 NuGet 使用新的 [Windows Azure 儲存體進階資料表](https://aka.ms/premiumtablenuget) (預覽版) 套件來執行一些查詢。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-107">You'll then write code to insert, update, and delete entities, and run some queries using the new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="bf5c7-108">此文件庫具有與公用 [Windows Azure 儲存體 SDK](https://www.nuget.org/packages/WindowsAzure.Storage) 相同的類別和方法簽章，但它也可以使用[資料表 API](table-introduction.md) (預覽版) 來連線到 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-108">This library has the same classes and method signatures as the public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has the ability to connect to Azure Cosmos DB accounts using the [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bf5c7-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="bf5c7-109">Prerequisites</span></span>

<span data-ttu-id="bf5c7-110">如果尚未安裝 Visual Studio 2017，您可以下載並使用**免費的** [Visual Studio 2017 Community 版本](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bf5c7-111">務必在 Visual Studio 設定期間啟用 **Azure 開發**。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="bf5c7-112">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="bf5c7-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="bf5c7-113">新增資料表</span><span class="sxs-lookup"><span data-stu-id="bf5c7-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="bf5c7-114">新增範例資料</span><span class="sxs-lookup"><span data-stu-id="bf5c7-114">Add sample data</span></span>

<span data-ttu-id="bf5c7-115">您現在可以使用資料總管 (預覽) 將資料新增至您的新資料表。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-115">You can now add data to your new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="bf5c7-116">在資料總管中，展開 **sample-table**，按一下 [實體]，然後按一下 [新增實體]。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![在 Azure 入口網站的 [資料總管] 中建立新實體](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="bf5c7-118">現在，將資料新增至 PartitionKey 值方塊和 RowKey 值方塊，然後按一下 [新增實體]。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-118">Now add data to the PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![為新的實體設定磁碟分割索引鍵和資料列索引鍵](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="bf5c7-120">您現在可以在資料表中新增更多實體、編輯實體，或在資料總管中查詢資料。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-120">You can now add more entities to your table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="bf5c7-121">資料總管也可供您調整輸送量，以及對資料表新增預存程序、使用者定義函式和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers to your table.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="bf5c7-122">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="bf5c7-122">Clone the sample application</span></span>

<span data-ttu-id="bf5c7-123">現在，我們將從 Github 複製「資料表」應用程式、設定連接字串，然後執行它。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-123">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="bf5c7-124">您會看到，以程式設計方式來處理資料有多麼的容易。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-124">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="bf5c7-125">開啟 Git 終端機視窗 (例如 Git Bash)，然後使用 `cd` 來切換到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-125">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="bf5c7-126">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-126">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="bf5c7-127">然後在 Visual Studio 中開啟方案檔案。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-127">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="bf5c7-128">檢閱程式碼</span><span class="sxs-lookup"><span data-stu-id="bf5c7-128">Review the code</span></span>

<span data-ttu-id="bf5c7-129">讓我們快速檢閱應用程式中所發生的事情。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-129">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="bf5c7-130">請開啟 Program.cs 檔案，您會發現這些程式碼行建立 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-130">Open the Program.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="bf5c7-131">已初始化 CloudTableClient。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-131">The CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="bf5c7-132">如果資料表不存在，將會建立資料表。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="bf5c7-133">已建立新的資料表容器。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-133">A new Table container is created.</span></span> <span data-ttu-id="bf5c7-134">您會注意到，這段程式碼與一般的 Azure 資料表儲存體 SDK 非常類似。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-134">You will notice this code very similar to regular Azure Table storage SDK.</span></span> 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="bf5c7-135">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="bf5c7-135">Update your connection string</span></span>

<span data-ttu-id="bf5c7-136">我們現在會更新連接字串資訊，讓您的應用程式可與 Azure Cosmos DB 通訊。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-136">Now we'll update the connection string information so your app can talk to Azure Cosmos DB.</span></span> 

1. <span data-ttu-id="bf5c7-137">在 Visual Studio 中，開啟 app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-137">In Visual Studio, open the app.config file.</span></span> 

2. <span data-ttu-id="bf5c7-138">在 [Azure 入口網站](http://portal.azure.com/)的 Azure Cosmos DB 左側導覽功能表中，按一下 [連接字串]。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-138">In the [Azure portal](http://portal.azure.com/), in the Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="bf5c7-139">然後在新的窗格中，按一下連接字串的複製按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-139">Then in the new pane click the copy button for the connection string.</span></span> 

    ![檢視及複製 [連接字串] 窗格中的端點和帳戶金鑰](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="bf5c7-141">將值貼到 app.config 檔案中，作為 PremiumStorageConnectionString 的值。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-141">Paste the value into the app.config file as the value of the PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="bf5c7-142">您可以讓 StandardStorageConnectionString 保持原狀。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-142">You can leave the StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="bf5c7-143">您現已更新應用程式，使其具有與 Azure Cosmos DB 通訊所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-143">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-web-app"></a><span data-ttu-id="bf5c7-144">執行 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="bf5c7-144">Run the web app</span></span>

1. <span data-ttu-id="bf5c7-145">在 Visual Studio 中，於 [方案總管] 中的 [PremiumTableGetStarted] 專案上按一下滑鼠右鍵，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-145">In Visual Studio, right-click on the **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="bf5c7-146">在 NuGet [瀏覽] 方塊中，輸入 *WindowsAzure.Storage-PremiumTable*。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-146">In the NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="bf5c7-147">請選取 [包括發行前版本] 方塊。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-147">Check the **Include prerelease** box.</span></span> 

4. <span data-ttu-id="bf5c7-148">從結果中，安裝 **WindowsAzure.Storage-PremiumTable** 程式庫。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-148">From the results, install the **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="bf5c7-149">這會安裝預覽版的 Azure Cosmos DB 資料表 API 套件以及所有相依性。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-149">This installs the preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="bf5c7-150">請注意，這個 NuGet 套件不同於 Azure 資料表儲存體所使用的 Windows Azure 儲存體套件。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-150">Note that this is a different NuGet package than the Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="bf5c7-151">按 CTRL + F5 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-151">Click CTRL + F5 to run the application.</span></span>

    <span data-ttu-id="bf5c7-152">主控台視窗會顯示將要在資料表中新增、擷取、查詢、取代和刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-152">The console window displays the data being added, retrieved, queried, replaced and deleted from the table.</span></span> <span data-ttu-id="bf5c7-153">當指令碼完成時，請任意鍵以關閉主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-153">When the script completes, press any key to close the console window.</span></span> 
    
    ![快速入門的主控台輸出](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="bf5c7-155">如果您想要在 [資料總管] 中查看新實體，只要將 program.cs 中的行 188-208 註解化，使其不會遭到刪除，然後再次執行範例。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-155">If you want to see the new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run the sample again.</span></span> 

    <span data-ttu-id="bf5c7-156">您現在可以回到 [資料總管]，按一下 [重新整理]，展開 [人員] 資料表並按一下 [實體]，然後使用此新資料。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-156">You can now go back to Data Explorer, click **Refresh**, expand the **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![在資料總管中新增實體](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="bf5c7-158">在 Azure 入口網站中檢閱 SLA</span><span class="sxs-lookup"><span data-stu-id="bf5c7-158">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="bf5c7-159">清除資源</span><span class="sxs-lookup"><span data-stu-id="bf5c7-159">Clean up resources</span></span>

<span data-ttu-id="bf5c7-160">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本快速入門所建立的所有資源：</span><span class="sxs-lookup"><span data-stu-id="bf5c7-160">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="bf5c7-161">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-161">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="bf5c7-162">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-162">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf5c7-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf5c7-163">Next steps</span></span>

<span data-ttu-id="bf5c7-164">在本快速入門中，您已了解如何建立 Azure Cosmos DB 帳戶、如何使用資料總管來建立資料表，以及如何執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-164">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="bf5c7-165">現在，您可以使用資料表 API 來查詢您的資料。</span><span class="sxs-lookup"><span data-stu-id="bf5c7-165">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf5c7-166">使用資料表 API 來進行查詢</span><span class="sxs-lookup"><span data-stu-id="bf5c7-166">Query using the Table API</span></span>](tutorial-query-table.md)

