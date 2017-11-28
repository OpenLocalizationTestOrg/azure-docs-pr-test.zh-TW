---
title: "Azure Cosmos DB: 開發以 hello 表格 API 在.NET |Microsoft 文件"
description: "深入了解如何使用適用於.NET 的 Azure Cosmos DB 的資料表 api toodevelop"
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
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="5b9ae-103">開發以 hello 表格 API 在.NET 的 azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="5b9ae-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="5b9ae-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="5b9ae-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="5b9ae-106">本教學課程涵蓋 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="5b9ae-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="5b9ae-107">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="5b9ae-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="5b9ae-108">啟用在 hello app.config 檔案中的功能</span><span class="sxs-lookup"><span data-stu-id="5b9ae-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="5b9ae-109">建立資料表，使用 hello[表格 API](table-introduction.md) （預覽）</span><span class="sxs-lookup"><span data-stu-id="5b9ae-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="5b9ae-110">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="5b9ae-111">插入實體批次</span><span class="sxs-lookup"><span data-stu-id="5b9ae-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="5b9ae-112">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="5b9ae-113">使用自動次要索引來查詢實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="5b9ae-114">取代實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-114">Replace an entity</span></span> 
> * <span data-ttu-id="5b9ae-115">刪除實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-115">Delete an entity</span></span> 
> * <span data-ttu-id="5b9ae-116">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="5b9ae-117">Azure Cosmos DB 中的資料表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="5b9ae-118">Azure 的 Cosmos DB 會提供 hello[表格 API](table-introduction.md) （預覽） 的需要無結構描述設計的索引鍵-值存放區的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="5b9ae-119">[Azure 資料表儲存體](../storage/common/storage-introduction.md)Sdk 和 REST Api 可以使用以 Azure Cosmos DB toowork。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="5b9ae-120">您可以使用 Azure Cosmos DB toocreate 資料表具有高輸送量需求。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="5b9ae-121">Azure Cosmos DB 支援輸送量最佳化資料表 (非正式的名稱為「進階資料表」)，目前是公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="5b9ae-122">您可以繼續 toouse 資料表具有高的儲存體與較低的輸送量需求的 Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="5b9ae-123">Azure Cosmos DB 將介紹支援儲存體最佳化的資料表，在未來的更新中，與現有和新的 Azure 資料表儲存體帳戶會順暢地升級 tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="5b9ae-124">如果您目前使用 Azure 資料表儲存體，您可以獲得下列的好處與 hello 「 高階資料表 」 預覽 hello:</span><span class="sxs-lookup"><span data-stu-id="5b9ae-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="5b9ae-125">具有多路連接及[自動和手動容錯移轉](regional-failover.md)的完備[全域散發](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="5b9ae-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="5b9ae-126">支援所有屬性 (次要索引) 之無從驗證結構描述的自動索引編製，以及快速查詢</span><span class="sxs-lookup"><span data-stu-id="5b9ae-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="5b9ae-127">支援在任意數目的區域[獨立調整儲存體和輸送量](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="5b9ae-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="5b9ae-128">支援[專用的輸送量，每個資料表](request-units.md)，可以調整百 toomillions 每秒的要求</span><span class="sxs-lookup"><span data-stu-id="5b9ae-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="5b9ae-129">支援[五個可微調的一致性層級](consistency-levels.md)tootrade 關閉可用性、 延遲和一致性根據您的應用程式需求</span><span class="sxs-lookup"><span data-stu-id="5b9ae-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="5b9ae-130">在多個單一區域和能力 tooadd 99.99%可用性的高可用性、 區域和[領先業界全面 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)一般可用性</span><span class="sxs-lookup"><span data-stu-id="5b9ae-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="5b9ae-131">使用 hello 現有 Azure 儲存體.NET SDK 與任何程式碼變更 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="5b9ae-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="5b9ae-132">Hello 在預覽期間，Azure Cosmos DB 支援 hello 資料表使用 hello.NET SDK 的 API。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="5b9ae-133">您可以下載 hello [Azure 儲存體預覽 SDK](https://aka.ms/premiumtablenuget) NuGet，從具有 hello 相同的類別和方法簽章為 hello [Azure 儲存體 SDK](https://www.nuget.org/packages/WindowsAzure.Storage)，但是也可以連接使用 hello tooAzure Cosmos DB 帳戶應用程式開發介面的資料表。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="5b9ae-134">toolearn 進一步了解複雜的 Azure 資料表儲存體工作，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5b9ae-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="5b9ae-135">簡介 tooAzure Cosmos DB： 表格 API</span><span class="sxs-lookup"><span data-stu-id="5b9ae-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="5b9ae-136">hello 有關可用的應用程式開發介面的完整詳細資料的資料表服務參考文件[.NET 參考的儲存體用戶端程式庫](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="5b9ae-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="5b9ae-137">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="5b9ae-137">About this tutorial</span></span>
<span data-ttu-id="5b9ae-138">本教學課程的開發人員熟悉 hello Azure 資料表儲存體 SDK，並希望 toouse hello premium 功能正在使用 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="5b9ae-139">它基礎[開始使用適用於.NET 的 Azure 資料表儲存體使用](table-storage-how-to-use-dotnet.md)，並示範如何 tootake 利用額外的功能讓次要索引，佈建的輸送量，多重主目錄。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="5b9ae-140">我們將討論如何 toouse hello Azure 入口網站 toocreate Azure Cosmos DB 帳戶，然後建置並部署資料表的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="5b9ae-141">此外，也逐步解說 .NET 範例，這些範例可用來建立和刪除資料表，以及插入、更新、刪除和查詢資料表資料。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="5b9ae-142">如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="5b9ae-143">請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="5b9ae-144">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="5b9ae-144">Create a database account</span></span>

<span data-ttu-id="5b9ae-145">首先在 hello Azure 入口網站中建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="5b9ae-146">已經有 Azure Cosmos DB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="5b9ae-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="5b9ae-147">如果是這樣，跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="5b9ae-148">您是否已有 Azure DocumentDB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="5b9ae-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="5b9ae-149">如果因此，您的帳戶現在是 Azure Cosmos DB 帳戶，而且您可以向前跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="5b9ae-150">如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="5b9ae-151">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="5b9ae-151">Clone hello sample application</span></span>

<span data-ttu-id="5b9ae-152">現在讓我們來複製資料表中的應用程式 github 設定 hello 連接字串，並執行它。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="5b9ae-153">開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="5b9ae-154">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="5b9ae-155">然後在 Visual Studio 中開啟 hello 方案檔。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="5b9ae-156">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="5b9ae-156">Update your connection string</span></span>

<span data-ttu-id="5b9ae-157">現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="5b9ae-158">在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="5b9ae-159">您將使用在 hello 螢幕 toocopy hello 連接字串 hello 右邊 hello 複製按鈕到 hello 下一個步驟中的 hello app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="5b9ae-160">在 Visual Studio 中，開啟 hello app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="5b9ae-161">從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello hello 帳戶鍵 app.config 中的值。使用先前建立的帳戶名稱在 app.config 中的 hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="5b9ae-162">toouse 標準 Azure 資料表儲存體與此應用程式，您需要 toochange hello 連接字串中的`app.config file`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="5b9ae-163">Azure 儲存體主索引鍵做為資料表帳戶名稱和金鑰使用 hello 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="5b9ae-164">建置和部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5b9ae-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="5b9ae-165">在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="5b9ae-166">在 hello NuGet**瀏覽**方塊中，輸入***WindowsAzure.Storage PremiumTable***。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="5b9ae-167">請選取 [包括發行前版本]。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="5b9ae-168">從 hello 結果中，安裝 hello **WindowsAzure.Storage PremiumTable**選擇 hello 預覽版`0.0.1-preview`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="5b9ae-169">此動作會安裝 hello Azure 資料表儲存體封裝和所有相依性。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="5b9ae-170">按一下 CTRL + F5 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="5b9ae-171">您現在可以返回 tooData 總管和看到查詢、 修改及使用此資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="5b9ae-172">此應用程式與 Azure Cosmos DB 模擬器，您只需要 toochange hello 連接字串中的 toouse `app.config file`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="5b9ae-173">使用模擬器 hello 最大值。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="5b9ae-174">Azure Cosmos DB 功能</span><span class="sxs-lookup"><span data-stu-id="5b9ae-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="5b9ae-175">Azure Cosmos DB 支援多種 hello Azure 資料表儲存體 API 中所沒有的功能。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="5b9ae-176">hello 新功能可透過啟用 hello 下列`appSettings`組態值。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="5b9ae-177">我們並未導入任何新簽章或多載 toohello 預覽 Azure 儲存體 SDK。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="5b9ae-178">這可讓您 tooconnect tooboth standard 和 premium 資料表和工作和其他 Azure 儲存體服務，例如 Blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="5b9ae-179">Key</span><span class="sxs-lookup"><span data-stu-id="5b9ae-179">Key</span></span> | <span data-ttu-id="5b9ae-180">說明</span><span class="sxs-lookup"><span data-stu-id="5b9ae-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5b9ae-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="5b9ae-181">TableConnectionMode</span></span>  | <span data-ttu-id="5b9ae-182">Azure Cosmos DB 支援兩種連線模式。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="5b9ae-183">在`Gateway`模式中，要求一律會 toohello Azure Cosmos DB 閘道，將它轉送 toohello 對應資料分割。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="5b9ae-184">在`Direct`連線模式 hello 用戶端擷取的資料表 toopartitions hello 對應，並將要求直接針對資料分割。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="5b9ae-185">我們建議`Direct`，hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="5b9ae-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="5b9ae-186">TableConnectionProtocol</span></span> | <span data-ttu-id="5b9ae-187">Azure Cosmos DB 支援兩種連線通訊協定 - `Https` 和 `Tcp`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="5b9ae-188">`Tcp`是 hello 預設值，而且建議使用，因為它更精簡。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="5b9ae-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="5b9ae-189">TablePreferredLocations</span></span> | <span data-ttu-id="5b9ae-190">供讀取使用的慣用 (多路連接) 位置逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="5b9ae-191">每個 Azure Cosmos DB 帳戶都可以與 1-30 個以上的區域建立關聯。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="5b9ae-192">每個用戶端執行個體可以針對低度延遲讀取 hello 慣用順序指定這些區域的子集。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="5b9ae-193">必須使用命名 hello 區及其[顯示名稱](https://msdn.microsoft.com/library/azure/gg441293.aspx)，例如`West US`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="5b9ae-194">另請參閱[多路連接 API](tutorial-global-distribution-table.md)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="5b9ae-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="5b9ae-195">TableConsistencyLevel</span></span> | <span data-ttu-id="5b9ae-196">您可以在五個定義完善的一致性層級之間做選擇，以在延遲、一致性及可用性之間做取捨：`Strong`、`Session`、`Bounded-Staleness`、`ConsistentPrefix` 及 `Eventual`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="5b9ae-197">預設值為 `Session`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-197">Default is `Session`.</span></span> <span data-ttu-id="5b9ae-198">hello 所選擇的一致性層級可讓多區域龐大的顯著的效能差異。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="5b9ae-199">如需詳細資料，請參閱[一致性層級](consistency-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="5b9ae-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="5b9ae-200">TableThroughput</span></span> | <span data-ttu-id="5b9ae-201">表示每秒要求單位 (RU) 中的 hello 資料表所保留的輸送量。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="5b9ae-202">單一資料表可支援每秒數億個 RU。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="5b9ae-203">請參閱[要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="5b9ae-204">預設值為 `400`</span><span class="sxs-lookup"><span data-stu-id="5b9ae-204">Default is `400`</span></span> |
| <span data-ttu-id="5b9ae-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="5b9ae-205">TableIndexingPolicy</span></span> | <span data-ttu-id="5b9ae-206">對資料表內所有資料行進行一致且自動的次要索引編製</span><span class="sxs-lookup"><span data-stu-id="5b9ae-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="5b9ae-207">JSON 字串合格 toohello 編製索引原則規格。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="5b9ae-208">請參閱[編製索引原則](indexing-policies.md)toosee 如何變更檢索原則 tooinclude/排除特定資料行。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="5b9ae-209">自動編製所有屬性 (字串的雜湊，以及數字的範圍) 的索引</span><span class="sxs-lookup"><span data-stu-id="5b9ae-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="5b9ae-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="5b9ae-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="5b9ae-211">設定 hello 的每個資料表至單一反覆存取的查詢傳回的項目數上限。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="5b9ae-212">預設值是`-1`，可讓 Azure Cosmos DB 以動態方式判斷 hello 值在執行階段。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="5b9ae-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="5b9ae-213">TableQueryEnableScan</span></span> | <span data-ttu-id="5b9ae-214">如果 hello 查詢無法使用 hello 索引的任何篩選，然後執行還是透過掃描。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="5b9ae-215">預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-215">Default is `false`.</span></span>|
| <span data-ttu-id="5b9ae-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="5b9ae-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="5b9ae-217">hello 執行跨資料分割查詢的平行處理原則程度。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="5b9ae-218">`0`與任何預先提取，序列`1`序列與預先提取，且平行處理原則增加 hello 率較高的數值。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="5b9ae-219">預設值是`-1`，可讓 Azure Cosmos DB 以動態方式判斷 hello 值在執行階段。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="5b9ae-220">toochange hello 預設值，開啟 hello`app.config`從 Visual Studio 中的 [方案總管] 的檔案。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="5b9ae-221">新增的 hello hello 內容`<appSettings>`如下所示的項目。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="5b9ae-222">取代`account-name`hello 儲存體帳戶名稱和`account-key`與您的帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="5b9ae-223">讓我們進行快速檢閱 hello 應用程式中的情況。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="5b9ae-224">開啟 hello`Program.cs`檔案，並尋找這行程式碼建立 hello 表格資源。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="5b9ae-225">建立 hello 資料表用戶端</span><span class="sxs-lookup"><span data-stu-id="5b9ae-225">Create hello table client</span></span>
<span data-ttu-id="5b9ae-226">您初始化`CloudTableClient`tooconnect toohello 資料表帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="5b9ae-227">此用戶端使用 hello 初始化`TableConnectionMode`， `TableConnectionProtocol`， `TableConsistencyLevel`，和`TablePreferredLocations`組態值，如果 hello 應用程式設定中指定。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="5b9ae-228">建立資料表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-228">Create a table</span></span>
<span data-ttu-id="5b9ae-229">然後，您需使用 `CloudTable` 來建立資料表。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="5b9ae-230">Azure Cosmos DB 中的資料表可以獨立擴充，以儲存體和輸送量、 和資料分割由自動 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="5b9ae-231">Azure Cosmos DB 同時支援固定大小和無限制的資料表。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="5b9ae-232">如需詳細資料，請參閱 [Azure Cosmos DB 中的資料分割](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="5b9ae-233">在資料表的建立方式方面有重大的差異。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="5b9ae-234">Azure Cosmos DB 會保留輸送量，而不像 Azure 儲存體針對交易是採用以耗用量為基礎的模型。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="5b9ae-235">hello 保留模型具有兩個主要優點：</span><span class="sxs-lookup"><span data-stu-id="5b9ae-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="5b9ae-236">您的輸送量是專用/已保留的，因此當您的要求率正好在或低於所佈建的輸送量時，一律不會進行節流</span><span class="sxs-lookup"><span data-stu-id="5b9ae-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="5b9ae-237">hello 保留模型較為[符合成本效益的輸送量為主的工作負載](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="5b9ae-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="5b9ae-238">您可以藉由設定 hello 設定來設定 hello 預設輸送量`TableThroughput`以每秒 RU （要求單位）。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="5b9ae-239">讀取 1 KB 實體會正規化為 1 RU 和其他作業都是正規化的 tooa 固定 RU 值根據其 CPU、 記憶體和 IOPS 的耗用量。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="5b9ae-240">深入了解 [Azure Cosmos DB 中的要求單位](request-units.md)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5b9ae-241">當資料表儲存體 SDK 目前不支援修改的輸送量時，您可以立即使用隨時 hello Azure 入口網站或 Azure CLI 變更 hello 輸送量。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="5b9ae-242">接著，我們會逐步解說 hello 簡單讀取及寫入使用 hello Azure 資料表儲存體 SDK (CRUD) 作業。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="5b9ae-243">本教學課程會示範 Azure Cosmos DB 所提供之可預測的低個位數毫秒延遲和快速查詢。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="5b9ae-244">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-244">Add an entity tooa table</span></span>
<span data-ttu-id="5b9ae-245">Azure 資料表儲存體中的實體擴充 hello`TableEntity`類別，而且必須具有`PartitionKey`和`RowKey`屬性。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="5b9ae-246">以下是一個客戶實體的範例定義。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="5b9ae-247">下列程式碼片段的 hello 顯示實體與 tooinsert hello Azure 儲存體 SDK 的方式。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="5b9ae-248">Azure Cosmos DB 可供任何規模的低延遲保證 hello 世界各地。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="5b9ae-249">寫入完成 < 15 ms p99 在與大約是 6 ms p50 執行的應用程式在 hello 與 hello Azure Cosmos DB 帳戶相同的區域。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="5b9ae-250">和這段期間寫入的 hello 事實的帳戶都已認可後 toohello 用戶端之後才它們會以同步方式進行複寫，內容經過永久認可之後，所有的內容會建立索引。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="5b9ae-251">hello Azure Cosmos DB 資料表 API 為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="5b9ae-252">公開上市 hello p99 延遲保證備份 Sla，如其他 Azure Cosmos DB Api 的。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="5b9ae-253">插入實體批次</span><span class="sxs-lookup"><span data-stu-id="5b9ae-253">Insert a batch of entities</span></span>
<span data-ttu-id="5b9ae-254">Azure 資料表儲存體支援批次作業 API，可讓您結合更新、 刪除和插入 hello 相同的單一批次作業。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="5b9ae-255">Azure Cosmos DB 沒有的某些 hello 限制 hello 批次 API 上作為 Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="5b9ae-256">例如，您可以執行多次讀取批次內，您可以執行多個寫入 toohello 內批次中的相同實體和每個批次的 100 個作業中沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="5b9ae-257">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-257">Retrieve a single entity</span></span>
<span data-ttu-id="5b9ae-258">擷取 （取得），在 Cosmos Azure DB 中完成 < 10 毫秒在 p99 和 ~ 1 毫秒中 p50 在 hello 相同 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="5b9ae-259">您可以新增多區域 tooyour 帳戶針對低度延遲讀取，並藉由設定部署應用程式從其區域 （「 多路連接 」） 的 tooread `TablePreferredLocations`。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="5b9ae-260">您可以擷取單一實體，使用下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b9ae-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="5b9ae-261">若要了解多路連接 API，請參閱[使用多個區域進行開發](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="5b9ae-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="5b9ae-262">使用自動次要索引來查詢實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="5b9ae-263">您可以使用 hello 查詢資料表`TableQuery`類別。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="5b9ae-264">Azure Cosmos DB 具有寫入最佳化資料庫引擎，可自動為您資料表中的所有資料行編製索引。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="5b9ae-265">在 Azure Cosmos DB 索引時，是無從驗證 tooschema。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="5b9ae-266">因此，即使您的結構描述不同之間的資料列，或經過一段時間發展，hello 結構描述，它會自動索引。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="5b9ae-267">由於 Azure Cosmos DB 支援自動次要索引，針對任何屬性的查詢可以使用 hello 索引，而且有效率地提供。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

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

<span data-ttu-id="5b9ae-268">在預覽中，Azure Cosmos DB 支援 hello 同樣的查詢與 hello 表格 API 的 Azure 資料表儲存體的功能。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="5b9ae-269">Azure Cosmos DB 也支援排序、彙總、地理空間查詢、階層及各種不同的內建函式。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="5b9ae-270">在未來的服務更新中的 hello 資料表 API 中，將會提供 hello 額外的功能。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="5b9ae-271">如需這些功能的概觀，請參閱 [Azure Cosmos DB 查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="5b9ae-272">取代實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-272">Replace an entity</span></span>
<span data-ttu-id="5b9ae-273">tooupdate 實體，擷取與 hello 表格服務，修改 hello 實體物件，然後再儲存 hello 變更變回 toohello 表格服務。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="5b9ae-274">hello 下列程式碼變更現有的客戶電話號碼。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="5b9ae-275">同樣地，您也可以執行 `InsertOrMerge` 或 `Merge` 作業。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="5b9ae-276">刪除實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-276">Delete an entity</span></span>
<span data-ttu-id="5b9ae-277">您已在使用 hello 擷取之後，您可以輕鬆地刪除實體的更新實體顯示的相同模式。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="5b9ae-278">下列程式碼的 hello 擷取，並刪除一個 customer 實體。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="5b9ae-279">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-279">Delete a table</span></span>
<span data-ttu-id="5b9ae-280">最後，下列程式碼範例的 hello 會從儲存體帳戶刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="5b9ae-281">您可使用 Azure Cosmos DB 來立即刪除並重新建立資料表。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="5b9ae-282">清除資源</span><span class="sxs-lookup"><span data-stu-id="5b9ae-282">Clean up resources</span></span> 

<span data-ttu-id="5b9ae-283">如果您不打算 toocontinue toouse 此應用程式，使用下列步驟 toodelete hello Azure 入口網站在此教學課程所建立的所有資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="5b9ae-284">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="5b9ae-285">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5b9ae-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b9ae-286">Next steps</span></span>

<span data-ttu-id="5b9ae-287">在本教學課程中，我們涵蓋 tooget 啟動 hello 表格 API 搭配使用 Azure Cosmos DB 的方式，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="5b9ae-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="5b9ae-288">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="5b9ae-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="5b9ae-289">Hello app.config 檔案中啟用的功能</span><span class="sxs-lookup"><span data-stu-id="5b9ae-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="5b9ae-290">建立資料表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-290">Created a table</span></span> 
> * <span data-ttu-id="5b9ae-291">加入實體 tooa 表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="5b9ae-292">插入一批實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="5b9ae-293">擷取單一實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="5b9ae-294">使用自動次要索引來查詢實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="5b9ae-295">取代實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-295">Replaced an entity</span></span> 
> * <span data-ttu-id="5b9ae-296">刪除實體</span><span class="sxs-lookup"><span data-stu-id="5b9ae-296">Deleted an entity</span></span> 
> * <span data-ttu-id="5b9ae-297">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="5b9ae-297">Deleted a table</span></span>  

<span data-ttu-id="5b9ae-298">您現在可以繼續 toohello 下一個教學課程，並深入了解查詢資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="5b9ae-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5b9ae-299">查詢以 hello 表格 API</span><span class="sxs-lookup"><span data-stu-id="5b9ae-299">Query with hello Table API</span></span>](tutorial-query-table.md)
