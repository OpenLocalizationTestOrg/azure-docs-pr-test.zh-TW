---
title: "Azure Cosmos DB：使用 .NET 搭配資料表 API 進行開發 | Microsoft Docs"
description: "了解如何使用 .NET 搭配 Azure Cosmos DB 的「資料表 API」進行開發"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 52cb5f2569b6c3a5301752b1e8bfb6cea13ff7f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="bbf3e-103">Azure Cosmos DB：使用 .NET 搭配資料表 API 進行開發</span><span class="sxs-lookup"><span data-stu-id="bbf3e-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="bbf3e-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="bbf3e-105">您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="bbf3e-106">本教學課程涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="bbf3e-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="bbf3e-107">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="bbf3e-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="bbf3e-108">在 app.config 檔案中啟用功能</span><span class="sxs-lookup"><span data-stu-id="bbf3e-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="bbf3e-109">使用[資料表 API](table-introduction.md) (預覽) 來建立資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-109">Create a table using the [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="bbf3e-110">將實體新增到資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="bbf3e-111">插入一批實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="bbf3e-112">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="bbf3e-113">使用自動次要索引來查詢實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="bbf3e-114">取代實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-114">Replace an entity</span></span> 
> * <span data-ttu-id="bbf3e-115">刪除實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-115">Delete an entity</span></span> 
> * <span data-ttu-id="bbf3e-116">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="bbf3e-117">Azure Cosmos DB 中的資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="bbf3e-118">Azure Cosmos DB 針對需要無結構描述設計之索引鍵-值存放區的應用程式，提供[資料表 API](table-introduction.md) (預覽)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-118">Azure Cosmos DB provides the [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="bbf3e-119">[Azure 資料表儲存體](../storage/common/storage-introduction.md) SDK 和 REST API 可用來與 Azure Cosmos DB 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used to work with Azure Cosmos DB.</span></span> <span data-ttu-id="bbf3e-120">您可以使用 Azure Cosmos DB 來建立具有高輸送量需求的資料表。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span> <span data-ttu-id="bbf3e-121">Azure Cosmos DB 支援輸送量最佳化資料表 (非正式的名稱為「進階資料表」)，目前是公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="bbf3e-122">針對具有高儲存體和較低輸送量需求的資料表，您可以繼續使用 Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-122">You can continue to use Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="bbf3e-123">Azure Cosmos DB 在未來的更新中將導入對儲存體最佳化資料表的支援，而現有和新的 Azure 資料表儲存體帳戶將會以無縫接軌的方式升級至 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded to Azure Cosmos DB.</span></span>

<span data-ttu-id="bbf3e-124">如果您目前使用 Azure 資料表儲存體，便可獲得「進階資料表」預覽版的下列優點：</span><span class="sxs-lookup"><span data-stu-id="bbf3e-124">If you currently use Azure Table storage, you gain the following benefits with the "premium table" preview:</span></span>

- <span data-ttu-id="bbf3e-125">具有多路連接及[自動和手動容錯移轉](regional-failover.md)的完備[全域散發](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="bbf3e-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="bbf3e-126">支援所有屬性 (次要索引) 之無從驗證結構描述的自動索引編製，以及快速查詢</span><span class="sxs-lookup"><span data-stu-id="bbf3e-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="bbf3e-127">支援在任意數目的區域[獨立調整儲存體和輸送量](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="bbf3e-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="bbf3e-128">支援[每一資料表有專用輸送量](request-units.md) (可從每秒數百個要求調整到數百萬個要求)</span><span class="sxs-lookup"><span data-stu-id="bbf3e-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="bbf3e-129">支援[五個可調整的一致性層級](consistency-levels.md)，可根據您應用程式的需求，進行可用性、延遲及一致性的取捨</span><span class="sxs-lookup"><span data-stu-id="bbf3e-129">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="bbf3e-130">單一區域內可達 99.99% 的可用性，並且能夠新增更多區域來提高可用性，以及在一般可用性上達到[業界頂尖的全面性 SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="bbf3e-130">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="bbf3e-131">可與現有的 Azure 儲存體 .NET SDK 搭配運作，不需對您的應用程式進行任何程式碼變更</span><span class="sxs-lookup"><span data-stu-id="bbf3e-131">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="bbf3e-132">在預覽版期間，Azure Cosmos DB 會使用 .NET SDK 來支援「資料表 API」。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-132">During the preview, Azure Cosmos DB supports the Table API using the .NET SDK.</span></span> <span data-ttu-id="bbf3e-133">您可以從 NuGet 下載 [Azure 儲存體預覽 SDK](https://aka.ms/premiumtablenuget)，此 SDK 具有與 [Azure 儲存體 SDK](https://www.nuget.org/packages/WindowsAzure.Storage) 相同的類別和方法簽章，但它也可以使用「資料表 API」來連線到 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-133">You can download the [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has the same classes and method signatures as the [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="bbf3e-134">若要深入了解複雜的 Azure 資料表儲存體工作，請參閱：</span><span class="sxs-lookup"><span data-stu-id="bbf3e-134">To learn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="bbf3e-135">Azure Cosmos DB 簡介：資料表 API</span><span class="sxs-lookup"><span data-stu-id="bbf3e-135">Introduction to Azure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="bbf3e-136">「資料表」服務參考文件，以取得關可用 API 的完整詳細資料：[適用於 .NET 的儲存體用戶端程式庫](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="bbf3e-136">The Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="bbf3e-137">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="bbf3e-137">About this tutorial</span></span>
<span data-ttu-id="bbf3e-138">本教學課程的對象是熟悉 Azure 資料表儲存體 SDK 且想要使用 Azure Cosmos DB 所提供之進階功能的開發人員。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-138">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="bbf3e-139">本教學課程是以[以 .NET 開始使用 Azure 表格儲存體](table-storage-how-to-use-dotnet.md)為基礎，並說明如何利用額外的功能，例如次要索引、佈建的輸送量及多路連接。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="bbf3e-140">我們涵蓋了如何使用 Azure 入口網站來建立 Azure Cosmos DB 帳戶，然後建置和部署「資料表」應用程式。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-140">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="bbf3e-141">此外，也逐步解說 .NET 範例，這些範例可用來建立和刪除資料表，以及插入、更新、刪除和查詢資料表資料。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="bbf3e-142">如果尚未安裝 Visual Studio 2017，您可以下載並使用「免費的」[Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-142">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bbf3e-143">務必在 Visual Studio 設定期間啟用 **Azure 開發**。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-143">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="bbf3e-144">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="bbf3e-144">Create a database account</span></span>

<span data-ttu-id="bbf3e-145">我們將從在 Azure 入口網站中建立 Azure Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-145">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="bbf3e-146">已經有 Azure Cosmos DB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="bbf3e-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="bbf3e-147">如果是，請直接跳到[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-147">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="bbf3e-148">您是否已有 Azure DocumentDB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="bbf3e-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="bbf3e-149">如果是，您的帳戶現在會是 Azure Cosmos DB 帳戶，且您可以直接跳到[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="bbf3e-150">如果您使用「Azure Cosmos DB 模擬器」，請依照 [Azure Cosmos DB 模擬器](local-emulator.md)的步驟來設定模擬器，然後直接跳到[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-150">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting to any location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="bbf3e-151">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="bbf3e-151">Clone the sample application</span></span>

<span data-ttu-id="bbf3e-152">現在，我們將從 Github 複製「資料表」應用程式、設定連接字串，然後執行它。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-152">Now let's clone a Table app from github, set the connection string, and run it.</span></span>

1. <span data-ttu-id="bbf3e-153">開啟 Git 終端機視窗 (例如 Git Bash)，然後使用 `cd` 來切換到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-153">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="bbf3e-154">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-154">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="bbf3e-155">然後在 Visual Studio 中開啟方案檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-155">Then open the solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="bbf3e-156">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="bbf3e-156">Update your connection string</span></span>

<span data-ttu-id="bbf3e-157">現在，返回 Azure 入口網站以取得連接字串資訊，並將它複製到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="bbf3e-158">在 [Azure 入口網站](http://portal.azure.com/)中，於您 Azure Cosmos DB 帳戶的左側瀏覽區中，按一下 [金鑰]，然後按一下 [讀寫金鑰]。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-158">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="bbf3e-159">在下一個步驟中，您將使用畫面右側的複製按鈕，將連接字串複製到 app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-159">You'll use the copy buttons on the right side of the screen to copy the connection string into the app.config file in the next step.</span></span>

2. <span data-ttu-id="bbf3e-160">在 Visual Studio 中，開啟 app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-160">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="bbf3e-161">從入口網站複製您的 URI 值 (使用 [複製] 按鈕)，然後將它設定為 app.config 中 account-key 的值。將先前建立的帳戶名稱用於 app.config 中的 account-name。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-161">Copy your URI value from the portal (using the copy button) and make it the value of the account-key in app.config. Use the account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="bbf3e-162">若要使用此應用程式搭配標準的「Azure 資料表儲存體」，您必須變更 `app.config file`中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-162">To use this app with standard Azure Table Storage, you need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="bbf3e-163">使用帳戶名稱作為資料表帳戶名稱，使用金鑰作為「Azure 儲存體」主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-163">Use the account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="bbf3e-164">建置並部署應用程式</span><span class="sxs-lookup"><span data-stu-id="bbf3e-164">Build and deploy the app</span></span>
1. <span data-ttu-id="bbf3e-165">在 Visual Studio 中，於 [方案總管] 中的專案上按一下滑鼠右鍵，然後按一下 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-165">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="bbf3e-166">在 NuGet [瀏覽] 方塊中，輸入 ***WindowsAzure.Storage-PremiumTable***。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-166">In the NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="bbf3e-167">請選取 [包括發行前版本]。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="bbf3e-168">從結果中，安裝 **WindowsAzure.Storage-PremiumTable** 並選擇預覽組建 `0.0.1-preview`。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-168">From the results, install the **WindowsAzure.Storage-PremiumTable** and choose the preview build `0.0.1-preview`.</span></span> <span data-ttu-id="bbf3e-169">此動作會安裝 Azure 資料表儲存體套件及所有相依項目。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-169">This action installs the Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="bbf3e-170">按 CTRL + F5 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-170">Click CTRL + F5 to run the application.</span></span> 

<span data-ttu-id="bbf3e-171">您現在可以返回 [資料總管]，以查看查詢、修改及使用此資料表資料。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-171">You can now go back to Data Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="bbf3e-172">若要使用此應用程式搭配「Azure Cosmos DB 模擬器」，只需變更 `app.config file` 中的連接字串即可。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-172">To use this app with an Azure Cosmos DB Emulator, you just need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="bbf3e-173">請將下列值用於模擬器。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-173">Use the below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="bbf3e-174">Azure Cosmos DB 功能</span><span class="sxs-lookup"><span data-stu-id="bbf3e-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="bbf3e-175">Azure Cosmos DB 支援一些 Azure 資料表儲存體 API 中未提供的功能。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-175">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> <span data-ttu-id="bbf3e-176">您可以透過下列 `appSettings` 組態值啟用新的功能。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-176">The new functionality can be enabled via the following `appSettings` configuration values.</span></span> <span data-ttu-id="bbf3e-177">我們並未在預覽版「Azure 儲存體 SDK」中導入任何新的簽章或多載。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-177">We did not introduce any new signatures or overloads to the preview Azure Storage SDK.</span></span> <span data-ttu-id="bbf3e-178">這讓您既可連線到標準資料表也可連線到進階資料表，以及與其他「Azure 儲存體」服務 (例如 Blob 和佇列) 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-178">This allows you to connect to both standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="bbf3e-179">索引鍵</span><span class="sxs-lookup"><span data-stu-id="bbf3e-179">Key</span></span> | <span data-ttu-id="bbf3e-180">說明</span><span class="sxs-lookup"><span data-stu-id="bbf3e-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bbf3e-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="bbf3e-181">TableConnectionMode</span></span>  | <span data-ttu-id="bbf3e-182">Azure Cosmos DB 支援兩種連線模式。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="bbf3e-183">在 `Gateway` 模式下，一律是對 Azure Cosmos DB 閘道提出要求，閘道會將要求轉送到對應的資料分割區。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-183">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="bbf3e-184">在 `Direct` 連線模式下，用戶端會擷取資料表與分割的對應，而提出要求時，則是直接對資料分割區提出。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-184">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="bbf3e-185">我們建議使用預設的 `Direct`。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-185">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="bbf3e-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="bbf3e-186">TableConnectionProtocol</span></span> | <span data-ttu-id="bbf3e-187">Azure Cosmos DB 支援兩種連線通訊協定 - `Https` 和 `Tcp`。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="bbf3e-188">`Tcp` 是預設值，也是建議使用的通訊協定，因為它較精簡。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-188">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="bbf3e-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="bbf3e-189">TablePreferredLocations</span></span> | <span data-ttu-id="bbf3e-190">供讀取使用的慣用 (多路連接) 位置逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="bbf3e-191">每個 Azure Cosmos DB 帳戶都可以與 1-30 個以上的區域建立關聯。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="bbf3e-192">每個用戶端執行個體可以依慣用順序指定這些區域的子集，供低延遲讀取使用。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-192">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="bbf3e-193">指定這些區域時，必須使用其[顯示名稱](https://msdn.microsoft.com/library/azure/gg441293.aspx)，例如 `West US`。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-193">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="bbf3e-194">另請參閱[多路連接 API](tutorial-global-distribution-table.md)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="bbf3e-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="bbf3e-195">TableConsistencyLevel</span></span> | <span data-ttu-id="bbf3e-196">您可以在五個定義完善的一致性層級之間做選擇，以在延遲、一致性及可用性之間做取捨：`Strong`、`Session`、`Bounded-Staleness`、`ConsistentPrefix` 及 `Eventual`。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="bbf3e-197">預設值為 `Session`。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-197">Default is `Session`.</span></span> <span data-ttu-id="bbf3e-198">一致性層級的選擇會在多區域設定中造成明顯的效能差異。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-198">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="bbf3e-199">如需詳細資料，請參閱[一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="bbf3e-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="bbf3e-200">TableThroughput</span></span> | <span data-ttu-id="bbf3e-201">以每秒要求單位 (RU) 表示的資料表保留輸送量。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-201">Reserved throughput for the table expressed in request units (RU) per second.</span></span> <span data-ttu-id="bbf3e-202">單一資料表可支援每秒數億個 RU。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="bbf3e-203">請參閱[要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="bbf3e-204">預設值為 `400`</span><span class="sxs-lookup"><span data-stu-id="bbf3e-204">Default is `400`</span></span> |
| <span data-ttu-id="bbf3e-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="bbf3e-205">TableIndexingPolicy</span></span> | <span data-ttu-id="bbf3e-206">對資料表內所有資料行進行一致且自動的次要索引編製</span><span class="sxs-lookup"><span data-stu-id="bbf3e-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="bbf3e-207">符合索引編製原則規格的 JSON 字串。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-207">JSON string conforming to the indexing policy specification.</span></span> <span data-ttu-id="bbf3e-208">若要了解如何變更索引編製原則以包含/排除特定資料行，請參閱[索引編製原則](indexing-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-208">See [Indexing Policy](indexing-policies.md) to see how you can change indexing policy to include/exclude specific columns.</span></span> | <span data-ttu-id="bbf3e-209">自動編製所有屬性 (字串的雜湊，以及數字的範圍) 的索引</span><span class="sxs-lookup"><span data-stu-id="bbf3e-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="bbf3e-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="bbf3e-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="bbf3e-211">設定單一來回行程中每一資料表查詢所傳回的項目數上限。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-211">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="bbf3e-212">預設值為 `-1`，這會讓 Azure Cosmos DB 在執行階段動態決定值。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="bbf3e-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="bbf3e-213">TableQueryEnableScan</span></span> | <span data-ttu-id="bbf3e-214">如果查詢無法針對任何篩選使用索引，則無論如何還是透過掃描執行它。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-214">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="bbf3e-215">預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-215">Default is `false`.</span></span>|
| <span data-ttu-id="bbf3e-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="bbf3e-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="bbf3e-217">用於執行跨分割區查詢的平行處理程度。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-217">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="bbf3e-218">`0` 為循序且不預先擷取，`1` 為循序並預先擷取，而值越高代表平行程度也越高。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="bbf3e-219">預設值為 `-1`，這會讓 Azure Cosmos DB 在執行階段動態決定值。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="bbf3e-220">若要變更預設值，請從 Visual Studio 中的 [方案總管] 開啟 `app.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-220">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="bbf3e-221">如下所示，加入 `<appSettings>` 元素的內容。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-221">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="bbf3e-222">以您的儲存體帳戶名稱取代 `account-name`，並以您的帳戶存取金鑰取代 `account-key`。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-222">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="bbf3e-223">讓我們快速檢閱應用程式中發生了什麼。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-223">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="bbf3e-224">請開啟 `Program.cs` 檔案，您會發現這些程式碼行建立「資料表」資源。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-224">Open the `Program.cs` file and you find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="bbf3e-225">建立資料表用戶端</span><span class="sxs-lookup"><span data-stu-id="bbf3e-225">Create the table client</span></span>
<span data-ttu-id="bbf3e-226">您需將 `CloudTableClient` 初始化以連線到資料表帳戶。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-226">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="bbf3e-227">將此用戶端初始化時，會使用 `TableConnectionMode`、`TableConnectionProtocol`、`TableConsistencyLevel` 及 `TablePreferredLocations` 組態值 (如果在應用程式設定中指定)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-227">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="bbf3e-228">建立資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-228">Create a table</span></span>
<span data-ttu-id="bbf3e-229">然後，您需使用 `CloudTable` 來建立資料表。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="bbf3e-230">Azure Cosmos DB 中的「資料表」可以就儲存體和輸送量方面獨立調整，而資料分割則是由服務自動處理。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="bbf3e-231">Azure Cosmos DB 同時支援固定大小和無限制的資料表。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="bbf3e-232">如需詳細資料，請參閱 [Azure Cosmos DB 中的資料分割](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="bbf3e-233">在資料表的建立方式方面有重大的差異。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="bbf3e-234">Azure Cosmos DB 會保留輸送量，而不像 Azure 儲存體針對交易是採用以耗用量為基礎的模型。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="bbf3e-235">保留模型有兩個主要的優點：</span><span class="sxs-lookup"><span data-stu-id="bbf3e-235">The reservation model has two key benefits:</span></span>

* <span data-ttu-id="bbf3e-236">您的輸送量是專用/已保留的，因此當您的要求率正好在或低於所佈建的輸送量時，一律不會進行節流</span><span class="sxs-lookup"><span data-stu-id="bbf3e-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="bbf3e-237">保留模型[對輸送量大的工作負載來說較符合成本效益](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="bbf3e-237">The reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="bbf3e-238">您可以設定以每秒 RU (要求單位) 表示的 `TableThroughput` 設定，來設定預設輸送量。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-238">You can configure the default throughput by configuring the setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="bbf3e-239">讀值為 1-KB 的實體會標準化為 1 RU，其他作業則會根據其 CPU、記憶體及 IOPS 耗用量來標準化為固定的 RU 值。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="bbf3e-240">深入了解 [Azure Cosmos DB 中的要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bbf3e-241">雖然資料表儲存體 SDK 目前不支援修改輸送量，但是您可以使用 Azure 入口網站或 Azure CLI 來隨時立即變更輸送量。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-241">While Table storage SDK does not currently support modifying throughput, you can change the throughput instantaneously at any time using the Azure portal or Azure CLI.</span></span>

<span data-ttu-id="bbf3e-242">接著，我們將逐步解說如何使用 Azure 資料表儲存體 SDK 來進行簡單的讀寫 (CRUD) 作業。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-242">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="bbf3e-243">本教學課程會示範 Azure Cosmos DB 所提供之可預測的低個位數毫秒延遲和快速查詢。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="bbf3e-244">將實體新增到資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-244">Add an entity to a table</span></span>
<span data-ttu-id="bbf3e-245">Azure 資料表儲存體中的實體會從 `TableEntity` 類別延伸，並且必須具有 `PartitionKey` 和 `RowKey` 屬性。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-245">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="bbf3e-246">以下是一個客戶實體的範例定義。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="bbf3e-247">下列程式碼片段說明如何使用 Azure 儲存體 SDK 來插入實體。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-247">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="bbf3e-248">Azure Cosmos DB 的設計目的是要為世界各地、不論任何規模都確保低延遲。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="bbf3e-249">針對執行區域在與 Azure Cosmos DB 帳戶相同區域的應用程式，寫入在 P99 是 15 毫秒內完成，在 P50 則是大約 6 毫秒完成。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="bbf3e-250">而這個持續時間說明了一個事實，就是寫入只有在同步複寫、永久認可且所有內容都已編製索引之後，才會認可回用戶端。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-250">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="bbf3e-251">Azure Cosmos DB 的「資料表 API」為預覽版。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-251">The Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="bbf3e-252">到正式運作時，P99 延遲保證會像其他 Azure Cosmos DB API 一樣由 SLA 作為後盾。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-252">At general availability, the p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="bbf3e-253">插入一批實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-253">Insert a batch of entities</span></span>
<span data-ttu-id="bbf3e-254">Azure 資料表儲存體支援批次作業 API，可讓您將更新、刪除及插入結合在同一個批次作業中。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same single batch operation.</span></span> <span data-ttu-id="bbf3e-255">Azure Cosmos DB 沒有像 Azure 資料表儲存體對批次 API 的一些限制。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-255">Azure Cosmos DB does not have some of the limitations on the batch API as Azure Table storage.</span></span> <span data-ttu-id="bbf3e-256">例如，您可以在一個批次內執行多次讀取，可以在一個批次內對相同的實體執行多次寫入，而且沒有每一批次 100 個作業的限制。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-256">For example, you can perform multiple reads within a batch, you can perform multiple writes to the same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="bbf3e-257">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-257">Retrieve a single entity</span></span>
<span data-ttu-id="bbf3e-258">相同 Azure 區域內 Azure Cosmos DB 中的 擷取 (GET) 在 P99 是 10 毫秒內完成，在 P50 則是大約 1 毫秒完成。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="bbf3e-259">您可以視所需的區域數量，將多個區域新增到您的帳戶來提供低延遲的讀取，並透過設定 `TablePreferredLocations` 將應用程式部署成從其本機區域 (多路連接) 讀取。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-259">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="bbf3e-260">您可以使用下列程式碼片段來擷取單一實體：</span><span class="sxs-lookup"><span data-stu-id="bbf3e-260">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="bbf3e-261">若要了解多路連接 API，請參閱[使用多個區域進行開發](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="bbf3e-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="bbf3e-262">使用自動次要索引來查詢實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="bbf3e-263">您可以使用 `TableQuery` 類別來查詢資料表。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-263">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="bbf3e-264">Azure Cosmos DB 具有寫入最佳化資料庫引擎，可自動為您資料表中的所有資料行編製索引。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="bbf3e-265">Azure Cosmos DB 中的索引編製是不驗證結構描述的。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-265">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="bbf3e-266">因此，即使資料列之間的結構描述不同，或結構描述隨著時間演變，仍然會自動編製索引。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-266">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="bbf3e-267">由於 Azure Cosmos DB 支援自動次要索引，因此對任何屬性的查詢都可使用該索引並有效率地獲得服務。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="bbf3e-268">在預覽版中，Azure Cosmos DB 支援的「資料表 API」查詢功能與 Azure 資料表儲存體相同。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-268">In preview, Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="bbf3e-269">Azure Cosmos DB 也支援排序、彙總、地理空間查詢、階層及各種不同的內建函式。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="bbf3e-270">在未來的服務更新中，將會在資料表 API 中提供額外的功能。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-270">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="bbf3e-271">如需這些功能的概觀，請參閱 [Azure Cosmos DB 查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="bbf3e-272">取代實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-272">Replace an entity</span></span>
<span data-ttu-id="bbf3e-273">若要更新實體，從資料表服務擷取實體、修改實體物件，然後將變更儲存回資料表服務。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-273">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="bbf3e-274">下列程式碼會變更現有客戶的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-274">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="bbf3e-275">同樣地，您也可以執行 `InsertOrMerge` 或 `Merge` 作業。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="bbf3e-276">刪除實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-276">Delete an entity</span></span>
<span data-ttu-id="bbf3e-277">使用更新實體時所展示的相同方法，輕鬆地在擷取實體後將其刪除。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-277">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="bbf3e-278">下列程式碼會擷取並刪除客戶實體。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-278">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="bbf3e-279">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-279">Delete a table</span></span>
<span data-ttu-id="bbf3e-280">最後，下列程式碼範例會從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-280">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="bbf3e-281">您可使用 Azure Cosmos DB 來立即刪除並重新建立資料表。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="bbf3e-282">清除資源</span><span class="sxs-lookup"><span data-stu-id="bbf3e-282">Clean up resources</span></span> 

<span data-ttu-id="bbf3e-283">如果您將不繼續使用此應用程式，請使用下列步驟，在 Azure 入口網站中刪除本教學課程所建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-283">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>   

1. <span data-ttu-id="bbf3e-284">從 Azure 入口網站的左側功能表中，按一下 [資源群組]，然後按一下您所建立資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-284">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span>  
2. <span data-ttu-id="bbf3e-285">在資源群組頁面上，按一下 [刪除]，在文字方塊中輸入要刪除之資源的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-285">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bbf3e-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bbf3e-286">Next steps</span></span>

<span data-ttu-id="bbf3e-287">在本教學課程中，我們涵蓋了如何開始使用 Azure Cosmos DB 搭配「資料表 API」，而您已經完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="bbf3e-287">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="bbf3e-288">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="bbf3e-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="bbf3e-289">在 app.config 檔案中啟用功能</span><span class="sxs-lookup"><span data-stu-id="bbf3e-289">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="bbf3e-290">建立資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-290">Created a table</span></span> 
> * <span data-ttu-id="bbf3e-291">將實體新增到資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-291">Added an entity to a table</span></span> 
> * <span data-ttu-id="bbf3e-292">插入一批實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="bbf3e-293">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="bbf3e-294">使用自動次要索引來查詢實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="bbf3e-295">取代實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-295">Replaced an entity</span></span> 
> * <span data-ttu-id="bbf3e-296">刪除實體</span><span class="sxs-lookup"><span data-stu-id="bbf3e-296">Deleted an entity</span></span> 
> * <span data-ttu-id="bbf3e-297">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="bbf3e-297">Deleted a table</span></span>  

<span data-ttu-id="bbf3e-298">您現在可以繼續進行到下一個教學課程，以進一步了解如何查詢資料表資料。</span><span class="sxs-lookup"><span data-stu-id="bbf3e-298">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbf3e-299">使用資料表 API 進行查詢</span><span class="sxs-lookup"><span data-stu-id="bbf3e-299">Query with the Table API</span></span>](tutorial-query-table.md)
