---
title: "Azure Cosmos DB: 使用 DocumentDB API 在.NET 中的 hello 開發 |Microsoft 文件"
description: "深入了解如何使用適用於.NET 的 Azure Cosmos DB 的 DocumentDB api toodevelop"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="370aa-103">使用 DocumentDB API 在.NET 中的 hello 開發 azure CosmosDB:</span><span class="sxs-lookup"><span data-stu-id="370aa-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="370aa-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="370aa-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="370aa-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="370aa-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="370aa-106">本教學課程示範如何 toocreate Azure Cosmos DB 帳戶使用 hello Azure 入口網站，並接著建立文件資料庫和集合[資料分割索引鍵](documentdb-partition-data.md#partition-keys)使用 hello [DocumentDB.NET API](documentdb-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="370aa-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="370aa-107">藉由定義資料分割索引鍵，當您建立集合時，您的應用程式已準備好 tooscale 毫不費力地隨著您的資料。</span><span class="sxs-lookup"><span data-stu-id="370aa-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="370aa-108">此教學課程涵蓋 hello 下列工作使用 hello [DocumentDB.NET API](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="370aa-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="370aa-109">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="370aa-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="370aa-110">建立具有分割區索引鍵的資料庫和集合</span><span class="sxs-lookup"><span data-stu-id="370aa-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="370aa-111">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="370aa-111">Create JSON documents</span></span>
> * <span data-ttu-id="370aa-112">更新文件</span><span class="sxs-lookup"><span data-stu-id="370aa-112">Update a document</span></span>
> * <span data-ttu-id="370aa-113">查詢已分割的集合</span><span class="sxs-lookup"><span data-stu-id="370aa-113">Query partitioned collections</span></span>
> * <span data-ttu-id="370aa-114">執行預存程序</span><span class="sxs-lookup"><span data-stu-id="370aa-114">Run stored procedures</span></span>
> * <span data-ttu-id="370aa-115">刪除文件</span><span class="sxs-lookup"><span data-stu-id="370aa-115">Delete a document</span></span>
> * <span data-ttu-id="370aa-116">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="370aa-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="370aa-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="370aa-117">Prerequisites</span></span>
<span data-ttu-id="370aa-118">請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="370aa-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="370aa-119">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="370aa-119">An active Azure account.</span></span> <span data-ttu-id="370aa-120">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="370aa-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="370aa-121">或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程，如果您想要 toouse 本機模擬的環境，供開發應用程式的 hello Azure DocumentDB 服務。</span><span class="sxs-lookup"><span data-stu-id="370aa-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="370aa-122">[Visual Studio](http://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="370aa-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="370aa-123">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="370aa-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="370aa-124">首先在 hello Azure 入口網站中建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="370aa-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="370aa-125">已經有 Azure Cosmos DB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="370aa-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="370aa-126">如果是這樣，跳過[設定您的 Visual Studio 方案](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="370aa-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="370aa-127">您是否已有 Azure DocumentDB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="370aa-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="370aa-128">如果因此，您的帳戶現在是 Azure Cosmos DB 帳戶，而且您可以向前跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="370aa-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="370aa-129">如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="370aa-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="370aa-130"><a id="SetupVS"></a>設定您的 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="370aa-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="370aa-131">在電腦上開啟 **Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="370aa-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="370aa-132">在 hello**檔案**功能表上，選取**新增**，然後選擇 **專案**。</span><span class="sxs-lookup"><span data-stu-id="370aa-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="370aa-133">在 hello**新專案**對話方塊中，選取**範本** / **Visual C#** / **主控台應用程式 (.NET Framework)**，命名您的專案，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="370aa-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="370aa-134">![Hello 新增專案 視窗的螢幕擷取畫面](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="370aa-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="370aa-135">在 [hello**方案總管] 中**，新主控台應用程式，也就是在您的 Visual Studio 方案，以滑鼠右鍵按一下，然後按一下**管理 NuGet 封裝...**</span><span class="sxs-lookup"><span data-stu-id="370aa-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![螢幕擷取畫面的權限 hello hello 專案的已按下功能表](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="370aa-137">在 hello **NuGet**索引標籤上，按一下 **瀏覽**，然後輸入**documentdb** hello 搜尋 方塊中。</span><span class="sxs-lookup"><span data-stu-id="370aa-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="370aa-138">在 hello 結果中尋找**Microsoft.Azure.DocumentDB**按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="370aa-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="370aa-139">hello 封裝識別碼 hello Azure Cosmos DB 用戶端程式庫是[Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)。</span><span class="sxs-lookup"><span data-stu-id="370aa-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="370aa-140">![尋找 Azure Cosmos DB 用戶端 SDK 的 NuGet 功能表 hello 的螢幕擷取畫面](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="370aa-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="370aa-141">如果您收到有關檢閱變更 toohello 方案，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="370aa-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="370aa-142">如果您收到關於接受授權的訊息，請按一下 [我接受]。</span><span class="sxs-lookup"><span data-stu-id="370aa-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="370aa-143"><a id="Connect"></a>加入參考 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="370aa-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="370aa-144">中這個教學課程提供 hello DocumentDB API 的程式碼片段所需 toocreate 和更新 Azure Cosmos DB 資源專案中的 hello 剩餘步驟。</span><span class="sxs-lookup"><span data-stu-id="370aa-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="370aa-145">首先，新增這些參考 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="370aa-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="370aa-146"><a id="add-references"></a>連接您的應用程式</span><span class="sxs-lookup"><span data-stu-id="370aa-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="370aa-147">接著，在應用程式中新增下列兩個常數和您的「用戶端」變數。</span><span class="sxs-lookup"><span data-stu-id="370aa-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="370aa-148">標頭然後回 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的端點 URL 和主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="370aa-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="370aa-149">hello 端點 URL 及主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。</span><span class="sxs-lookup"><span data-stu-id="370aa-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="370aa-150">在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，按一下 **金鑰**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="370aa-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="370aa-151">從 hello 入口網站複製 hello URI，並將它貼入`<your endpoint URL>`hello program.cs 檔案中。</span><span class="sxs-lookup"><span data-stu-id="370aa-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="370aa-152">複製 hello 從 hello 入口網站的主索引鍵，並將它貼入`<your primary key>`。</span><span class="sxs-lookup"><span data-stu-id="370aa-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="370aa-153">要確定 tooremove hello`<`和`>`從您的值。</span><span class="sxs-lookup"><span data-stu-id="370aa-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Hello Azure 入口網站的螢幕擷取畫面 hello NoSQL 教學課程 toocreate 使用 C# 主控台應用程式。](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="370aa-156"><a id="instantiate"></a>具現化 hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="370aa-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="370aa-157">現在，建立新的執行個體的 hello **DocumentClient**。</span><span class="sxs-lookup"><span data-stu-id="370aa-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="370aa-158"><a id="create-database"></a>建立資料庫</span><span class="sxs-lookup"><span data-stu-id="370aa-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="370aa-159">接下來，建立 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)使用 hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx)方法或[CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx)方法 hello **DocumentClient**類別從 hello [DocumentDB.NET SDK](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="370aa-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="370aa-160">資料庫是 hello 的 JSON 文件儲存分割於各個集合的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="370aa-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="370aa-161">選定分割區索引鍵</span><span class="sxs-lookup"><span data-stu-id="370aa-161">Decide on a partition key</span></span> 

<span data-ttu-id="370aa-162">集合是用來儲存文件的容器。</span><span class="sxs-lookup"><span data-stu-id="370aa-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="370aa-163">它們是邏輯資源，並且可以[跨一或多個實體分割區](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="370aa-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="370aa-164">A[資料分割索引鍵](documentdb-partition-data.md)是屬性 （或路徑） 內所使用的 toodistribute 文件之間 hello 伺服器或資料分割資料。</span><span class="sxs-lookup"><span data-stu-id="370aa-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="370aa-165">所有文件以 hello 相同的資料分割索引鍵會儲存在 hello 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="370aa-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="370aa-166">決定資料分割索引鍵是重要的決策 toomake 之前建立的集合。</span><span class="sxs-lookup"><span data-stu-id="370aa-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="370aa-167">資料分割索引鍵屬性 （或路徑） 都可以是您的文件中使用 Azure Cosmos DB toodistribute 您在多個伺服器或資料分割之間的資料。</span><span class="sxs-lookup"><span data-stu-id="370aa-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="370aa-168">Cosmos DB hello 資料分割索引鍵值的雜湊，並使用哪些 toostore hello 文件中的雜湊的 hello 結果 toodetermine hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="370aa-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="370aa-169">所有文件以 hello 相同的資料分割索引鍵會儲存在 hello 相同的資料分割，並在集合建立後，就無法變更資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="370aa-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="370aa-170">此教學課程中，我們會 tooset hello 資料分割索引鍵太`/deviceId`因此的 hello hello 的所有資料對於單一裝置儲存在單一資料分割中。</span><span class="sxs-lookup"><span data-stu-id="370aa-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="370aa-171">您想要 toochoose 具有大量的值，其中每個使用資料分割索引鍵在 hello 關於相同頻率 tooensure Cosmos DB 可以負載平衡資料成長以及達到 hello 全部輸送量，hello 集合。</span><span class="sxs-lookup"><span data-stu-id="370aa-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="370aa-172">如需有關資料分割的詳細資訊，請參閱[如何 toopartition 和小數位數，在 Azure Cosmos DB 嗎？](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="370aa-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="370aa-173"><a id="CreateColl"></a>建立集合</span><span class="sxs-lookup"><span data-stu-id="370aa-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="370aa-174">既然我們知道我們的資料分割索引鍵， `/deviceId`，可讓您建立[集合](documentdb-resources.md#collections)使用 hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx)方法或[CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="370aa-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="370aa-175">集合是 JSON 文件和任何相關 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="370aa-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="370aa-176">建立集合的定價顧慮，為您保留 Azure Cosmos db hello 應用程式 toocommunicate 的輸送量。</span><span class="sxs-lookup"><span data-stu-id="370aa-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="370aa-177">如需更多詳細資料，請瀏覽我們的[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="370aa-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="370aa-178">這個方法會 REST API 呼叫 tooAzure Cosmos DB 而且 hello 服務佈建的 hello 要求輸送量為基礎的資料分割數目。</span><span class="sxs-lookup"><span data-stu-id="370aa-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="370aa-179">您可以變更您的效能需求的發展使用 hello SDK 或 hello 集合中的 hello 輸送量[Azure 入口網站](set-throughput.md)。</span><span class="sxs-lookup"><span data-stu-id="370aa-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="370aa-180"><a id="CreateDoc"></a>建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="370aa-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="370aa-181">我們將把一些 JSON 文件插入到 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="370aa-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="370aa-182">A[文件](documentdb-resources.md#documents)可以建立使用 hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="370aa-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="370aa-183">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="370aa-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="370aa-184">此範例類別包含裝置讀取，且呼叫 tooCreateDocumentAsync tooinsert 讀入集合的新裝置。</span><span class="sxs-lookup"><span data-stu-id="370aa-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="370aa-185">讀取資料</span><span class="sxs-lookup"><span data-stu-id="370aa-185">Read data</span></span>

<span data-ttu-id="370aa-186">讓我們來讀取 hello 文件，其資料分割索引鍵並使用 hello ReadDocumentAsync 方法的識別碼。</span><span class="sxs-lookup"><span data-stu-id="370aa-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="370aa-187">請注意，hello 讀取包含 PartitionKey 值 (對應 toohello `x-ms-documentdb-partitionkey` hello REST API 中的要求標頭)。</span><span class="sxs-lookup"><span data-stu-id="370aa-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="370aa-188">更新資料</span><span class="sxs-lookup"><span data-stu-id="370aa-188">Update data</span></span>

<span data-ttu-id="370aa-189">現在讓我們先更新某些使用 hello ReplaceDocumentAsync 方法的資料。</span><span class="sxs-lookup"><span data-stu-id="370aa-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="370aa-190">刪除資料</span><span class="sxs-lookup"><span data-stu-id="370aa-190">Delete data</span></span>

<span data-ttu-id="370aa-191">現在可讓使用 hello DeleteDocumentAsync 方法刪除的資料分割索引鍵的文件和識別碼。</span><span class="sxs-lookup"><span data-stu-id="370aa-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="370aa-192">查詢已分割的集合</span><span class="sxs-lookup"><span data-stu-id="370aa-192">Query partitioned collections</span></span>

<span data-ttu-id="370aa-193">當您查詢資料分割的集合，Azure Cosmos DB 中的資料會自動路由 hello 對應 toohello 資料分割索引鍵值 （如果有的話），hello 篩選中指定的查詢 toohello 分割區。</span><span class="sxs-lookup"><span data-stu-id="370aa-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="370aa-194">例如，此查詢是路由的 toojust hello 磁碟分割包含 hello 資料分割索引鍵"XMS 0001"。</span><span class="sxs-lookup"><span data-stu-id="370aa-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="370aa-195">hello 下列查詢 hello 資料分割索引鍵 (DeviceId) 上沒有篩選器，視窗成扇形散開 tooall 分割區執行針對 hello 分割區索引。</span><span class="sxs-lookup"><span data-stu-id="370aa-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="370aa-196">請注意，您必須 toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` hello REST API 中) toohave hello SDK tooexecute 橫跨資料分割的查詢。</span><span class="sxs-lookup"><span data-stu-id="370aa-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="370aa-197">平行查詢執行</span><span class="sxs-lookup"><span data-stu-id="370aa-197">Parallel query execution</span></span>
<span data-ttu-id="370aa-198">hello Azure Cosmos DB DocumentDB Sdk 1.9.0 和上方支援平行查詢執行選項，可讓您 tooperform 低度延遲查詢針對資料分割的集合，即使他們需要 tootouch 大量的資料分割。</span><span class="sxs-lookup"><span data-stu-id="370aa-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="370aa-199">比方說，下列查詢的 hello 是以平行方式設定的 toorun 橫跨資料分割。</span><span class="sxs-lookup"><span data-stu-id="370aa-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="370aa-200">您可以管理執行平行查詢微調 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="370aa-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="370aa-201">藉由設定`MaxDegreeOfParallelism`，您可以控制 hello 程度的平行處理原則即 hello 同時網路連線 toohello 集合的資料分割數目上限。</span><span class="sxs-lookup"><span data-stu-id="370aa-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="370aa-202">如果您設定太-1，會將平行處理原則程度 hello 受 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="370aa-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="370aa-203">如果 hello`MaxDegreeOfParallelism`未指定或設定 too0，也就是 hello 預設值，會有單一網路連線 toohello 集合的資料分割。</span><span class="sxs-lookup"><span data-stu-id="370aa-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="370aa-204">您可藉由設定 `MaxBufferedItemCount`，來權衡取捨查詢延遲和用戶端記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="370aa-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="370aa-205">如果您省略這個參數，或將此設定太-1，由 hello SDK 管理 hello 平行查詢執行期間經過緩衝處理的項目數目。</span><span class="sxs-lookup"><span data-stu-id="370aa-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="370aa-206">指定 hello hello 集合的相同的州名，平行查詢會傳回結果中 hello 相同排序如同序列執行。</span><span class="sxs-lookup"><span data-stu-id="370aa-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="370aa-207">執行包含排序 （ORDER BY 和/或頂端） 的跨資料分割查詢，hello DocumentDB SDK 發出 hello 查詢，以平行方式在資料分割，並將部分已排序的結果，在 hello 用戶端端 tooproduce 全域排序結果。</span><span class="sxs-lookup"><span data-stu-id="370aa-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="370aa-208">執行預存程序</span><span class="sxs-lookup"><span data-stu-id="370aa-208">Execute stored procedures</span></span>
<span data-ttu-id="370aa-209">最後，您可以執行不可部分完成的交易，對文件以 hello 相同的裝置識別碼，例如： 如果您正在維護彙總，或藉由新增下列程式碼 tooyour 專案 hello hello 單一文件中的裝置最新狀態。</span><span class="sxs-lookup"><span data-stu-id="370aa-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="370aa-210">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="370aa-210">And that's it!</span></span> <span data-ttu-id="370aa-211">這些是 hello Azure Cosmos DB 應用程式使用資料分割索引鍵 tooefficiently 標尺資料發佈在資料分割之間的主要元件。</span><span class="sxs-lookup"><span data-stu-id="370aa-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="370aa-212">清除資源</span><span class="sxs-lookup"><span data-stu-id="370aa-212">Clean up resources</span></span>

<span data-ttu-id="370aa-213">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源，本教學課程以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="370aa-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="370aa-214">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="370aa-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="370aa-215">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="370aa-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="370aa-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="370aa-216">Next steps</span></span>

<span data-ttu-id="370aa-217">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="370aa-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="370aa-218">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="370aa-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="370aa-219">建立具有資料分割索引鍵的資料庫和集合</span><span class="sxs-lookup"><span data-stu-id="370aa-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="370aa-220">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="370aa-220">Created JSON documents</span></span>
> * <span data-ttu-id="370aa-221">更新文件</span><span class="sxs-lookup"><span data-stu-id="370aa-221">Updated a document</span></span>
> * <span data-ttu-id="370aa-222">查詢已分割的集合</span><span class="sxs-lookup"><span data-stu-id="370aa-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="370aa-223">執行預存程序</span><span class="sxs-lookup"><span data-stu-id="370aa-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="370aa-224">刪除文件</span><span class="sxs-lookup"><span data-stu-id="370aa-224">Deleted a document</span></span>
> * <span data-ttu-id="370aa-225">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="370aa-225">Deleted a database</span></span>

<span data-ttu-id="370aa-226">您現在可以繼續進行下一個教學課程 toohello 並匯入的其他資料 tooyour Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="370aa-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="370aa-227">將資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="370aa-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
