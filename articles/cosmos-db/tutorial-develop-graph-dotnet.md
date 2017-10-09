---
title: "Azure Cosmos DB: 使用 Graph API 在.NET 中的 hello 開發 |Microsoft 文件"
description: "深入了解如何使用適用於.NET 的 Azure Cosmos DB 的 DocumentDB api toodevelop"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="18f83-103">使用 Graph API 在.NET 中的 hello 開發 azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="18f83-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="18f83-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="18f83-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="18f83-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="18f83-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="18f83-106">本教學課程示範如何使用您建立 Azure Cosmos DB 帳戶 toocreate hello Azure 入口網站以及如何 toocreate 圖形資料庫和容器。</span><span class="sxs-lookup"><span data-stu-id="18f83-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="18f83-107">然後 hello 應用程式與使用 hello 的四個人員建立簡單的社交網路[Graph API](graph-sdk-dotnet.md) （預覽），則會周遊和查詢使用 Gremlin hello 圖形。</span><span class="sxs-lookup"><span data-stu-id="18f83-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="18f83-108">本教學課程涵蓋 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="18f83-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18f83-109">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="18f83-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="18f83-110">建立圖形資料庫和容器</span><span class="sxs-lookup"><span data-stu-id="18f83-110">Create a graph database and container</span></span>
> * <span data-ttu-id="18f83-111">將頂點和邊緣 too.NET 物件序列化</span><span class="sxs-lookup"><span data-stu-id="18f83-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="18f83-112">新增頂點和邊緣</span><span class="sxs-lookup"><span data-stu-id="18f83-112">Add vertices and edges</span></span>
> * <span data-ttu-id="18f83-113">使用 Gremlin 查詢 hello 圖形</span><span class="sxs-lookup"><span data-stu-id="18f83-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="18f83-114">Azure Cosmos DB 中的圖形</span><span class="sxs-lookup"><span data-stu-id="18f83-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="18f83-115">您可以使用 Azure Cosmos DB toocreate、 更新和查詢圖形使用 hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md)程式庫。</span><span class="sxs-lookup"><span data-stu-id="18f83-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="18f83-116">hello Microsoft.Azure.Graph 程式庫提供單一的擴充方法`CreateGremlinQuery<T>`之上 hello`DocumentClient`類別 tooexecute Gremlin 查詢。</span><span class="sxs-lookup"><span data-stu-id="18f83-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="18f83-117">Gremlin 是一個函式程式設計語言，可支援寫入作業 (DML) 及查詢和周遊作業。</span><span class="sxs-lookup"><span data-stu-id="18f83-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="18f83-118">我們將討論幾個範例在這個發行項 tooget Gremlin 與您開始使用。</span><span class="sxs-lookup"><span data-stu-id="18f83-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="18f83-119">如需 Azure Cosmos DB 中可用之 Gremlin 功能的詳細逐步解說，請參閱 [Gremlin 查詢](gremlin-support.md)。</span><span class="sxs-lookup"><span data-stu-id="18f83-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="18f83-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="18f83-120">Prerequisites</span></span>
<span data-ttu-id="18f83-121">請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="18f83-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="18f83-122">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="18f83-122">An active Azure account.</span></span> <span data-ttu-id="18f83-123">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="18f83-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="18f83-124">或者，您可以使用 hello [Azure DocumentDB 模擬器](local-emulator.md)本教學課程。</span><span class="sxs-lookup"><span data-stu-id="18f83-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="18f83-125">[Visual Studio](http://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="18f83-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="18f83-126">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="18f83-126">Create database account</span></span>

<span data-ttu-id="18f83-127">首先在 hello Azure 入口網站中建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="18f83-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="18f83-128">已經有 Azure Cosmos DB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="18f83-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="18f83-129">如果是這樣，跳過[設定您的 Visual Studio 方案](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="18f83-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="18f83-130">您是否已有 Azure DocumentDB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="18f83-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="18f83-131">如果因此，您的帳戶現在是 Azure Cosmos DB 帳戶，而且您可以向前跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="18f83-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="18f83-132">如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="18f83-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="18f83-133"><a id="SetupVS"></a>設定您的 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="18f83-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="18f83-134">在電腦上開啟 **Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="18f83-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="18f83-135">在 hello**檔案**功能表上，選取**新增**，然後選擇 **專案**。</span><span class="sxs-lookup"><span data-stu-id="18f83-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="18f83-136">在 hello**新專案**對話方塊中，選取**範本** / **Visual C#** / **主控台應用程式 (.NET Framework)**，命名您的專案，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="18f83-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="18f83-137">在 [hello**方案總管] 中**，新主控台應用程式，也就是在您的 Visual Studio 方案，以滑鼠右鍵按一下，然後按一下**管理 NuGet 封裝...**</span><span class="sxs-lookup"><span data-stu-id="18f83-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="18f83-138">在 hello **NuGet**索引標籤上，按一下 **瀏覽**，和型別**Microsoft.Azure.Graphs** hello 搜尋方塊中，核取 hello 中**包含發行前版本**.</span><span class="sxs-lookup"><span data-stu-id="18f83-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="18f83-139">在 hello 結果中尋找**Microsoft.Azure.Graphs**按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="18f83-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="18f83-140">如果您收到有關檢閱變更 toohello 方案，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="18f83-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="18f83-141">如果您收到關於接受授權的訊息，請按一下 [我接受]。</span><span class="sxs-lookup"><span data-stu-id="18f83-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="18f83-142">hello`Microsoft.Azure.Graphs`程式庫提供單一的擴充方法`CreateGremlinQuery<T>`執行 Gremlin 作業。</span><span class="sxs-lookup"><span data-stu-id="18f83-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="18f83-143">Gremlin 是一個函式程式設計語言，可支援寫入作業 (DML) 及查詢和周遊作業。</span><span class="sxs-lookup"><span data-stu-id="18f83-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="18f83-144">我們將討論幾個範例在這個發行項 tooget Gremlin 與您開始使用。</span><span class="sxs-lookup"><span data-stu-id="18f83-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="18f83-145">如需 Azure Cosmos DB 中 Gremlin 功能的詳細逐步解說，請參閱 [Gremlin 查詢](gremlin-support.md)。</span><span class="sxs-lookup"><span data-stu-id="18f83-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="18f83-146"><a id="add-references"></a>連接您的應用程式</span><span class="sxs-lookup"><span data-stu-id="18f83-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="18f83-147">在應用程式中新增下列兩個常數和您的「用戶端」變數。</span><span class="sxs-lookup"><span data-stu-id="18f83-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="18f83-148">接下來，head 回 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的端點 URL 和主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="18f83-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="18f83-149">hello 端點 URL 及主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。</span><span class="sxs-lookup"><span data-stu-id="18f83-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="18f83-150">在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，按一下 **金鑰**，然後按一下**讀寫金鑰**。</span><span class="sxs-lookup"><span data-stu-id="18f83-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="18f83-151">從 hello 入口網站複製 hello URI，並將它貼入`Endpoint`上述的 hello 端點屬性中。</span><span class="sxs-lookup"><span data-stu-id="18f83-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="18f83-152">然後複本 hello 從 hello 入口網站的主索引鍵，並將它貼到 hello`AuthKey`上述的屬性。</span><span class="sxs-lookup"><span data-stu-id="18f83-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="18f83-153">![Hello Azure 入口網站的螢幕擷取畫面使用 hello 教學課程 toocreate C# 應用程式。</span><span class="sxs-lookup"><span data-stu-id="18f83-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="18f83-154">金鑰] 按鈕上反白顯示 hello Azure Cosmos DB 導覽和 hello URI 與主索引鍵的值上反白顯示 hello 金鑰刀鋒視窗會顯示 Azure Cosmos DB 帳戶 hello] [金鑰]</span><span class="sxs-lookup"><span data-stu-id="18f83-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="18f83-155"><a id="instantiate"></a>具現化 hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="18f83-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="18f83-156">接下來，建立新的執行個體的 hello **DocumentClient**。</span><span class="sxs-lookup"><span data-stu-id="18f83-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="18f83-157"><a id="create-database"></a>建立資料庫</span><span class="sxs-lookup"><span data-stu-id="18f83-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="18f83-158">現在，建立 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)使用 hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx)方法或[CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx)方法 hello **DocumentClient**類別從 hello [DocumentDB.NET SDK](documentdb-sdk-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="18f83-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="18f83-159">建立圖形</span><span class="sxs-lookup"><span data-stu-id="18f83-159">Create a graph</span></span> 

<span data-ttu-id="18f83-160">接下來，建立的圖形容器，藉由使用 hello hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx)方法或[CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="18f83-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="18f83-161">集合是圖形實體的容器。</span><span class="sxs-lookup"><span data-stu-id="18f83-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="18f83-162"><a id="serializing"></a>將頂點和邊緣 too.NET 物件序列化</span><span class="sxs-lookup"><span data-stu-id="18f83-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="18f83-163">Azure 的 Cosmos DB 使用 hello [GraphSON 電傳格式](gremlin-support.md)，其定義所在的頂點，邊緣、 和屬性的 JSON 結構描述。</span><span class="sxs-lookup"><span data-stu-id="18f83-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="18f83-164">hello Azure Cosmos DB.NET SDK 包含 JSON.NET 做為相依性，而這讓我們 tooserialize/還原序列化 GraphSON 我們可以在程式碼中使用的.NET 物件。</span><span class="sxs-lookup"><span data-stu-id="18f83-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="18f83-165">我們將使用一個包含 4 個人的簡單社交網路來作為範例。</span><span class="sxs-lookup"><span data-stu-id="18f83-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="18f83-166">我們會審視如何 toocreate`Person`頂點，新增`Knows`之間關聯性，則查詢和周遊 hello 圖形 toofind"朋友的朋友叫什麼 」 關聯性。</span><span class="sxs-lookup"><span data-stu-id="18f83-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="18f83-167">hello`Microsoft.Azure.Graphs.Elements`命名空間提供`Vertex`， `Edge`，`Property`和`VertexProperty`GraphSON 回應 toowell 定義.NET 物件還原序列化的類別。</span><span class="sxs-lookup"><span data-stu-id="18f83-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="18f83-168">使用 CreateGremlinQuery 來執行 Gremlin</span><span class="sxs-lookup"><span data-stu-id="18f83-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="18f83-169">Gremlin (例如 SQL) 支援讀取、寫入及查詢作業。</span><span class="sxs-lookup"><span data-stu-id="18f83-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="18f83-170">例如，hello 下列程式碼片段示範如何 toocreate 頂點，邊緣、 執行使用的某些查詢範例`CreateGremlinQuery<T>`，並以非同步方式逐一查看使用這些結果`ExecuteNextAsync`和 ' HasMoreResults。</span><span class="sxs-lookup"><span data-stu-id="18f83-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="18f83-171">新增頂點和邊緣</span><span class="sxs-lookup"><span data-stu-id="18f83-171">Add vertices and edges</span></span>

<span data-ttu-id="18f83-172">讓我們看看顯示的 hello 前面一節更詳細的 hello Gremlin 陳述式。</span><span class="sxs-lookup"><span data-stu-id="18f83-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="18f83-173">首先，我們會使用 Gremlin 的 `addV` 方法來新增一些頂點。</span><span class="sxs-lookup"><span data-stu-id="18f83-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="18f83-174">比方說，hello 下列程式碼片段會建立類型"Person"，"Thomas Andersen"頂點具有屬性的名字、 姓氏和年齡。</span><span class="sxs-lookup"><span data-stu-id="18f83-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="18f83-175">然後，我們會使用 Gremlin 的 `addE` 方法在這些頂點之間建立一些邊緣。</span><span class="sxs-lookup"><span data-stu-id="18f83-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="18f83-176">我們可以使用 Gremlin 中的 `properties` 步驟來更新現有的頂點。</span><span class="sxs-lookup"><span data-stu-id="18f83-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="18f83-177">我們會略過 hello 呼叫 tooexecute hello 查詢透過`HasMoreResults`和`ExecuteNextAsync`hello 範例 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="18f83-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="18f83-178">您可以使用 Gremlin 的 `drop` 步驟來卸除邊緣和頂點。</span><span class="sxs-lookup"><span data-stu-id="18f83-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="18f83-179">以下是程式碼片段顯示如何 toodelete 的頂點和邊緣。</span><span class="sxs-lookup"><span data-stu-id="18f83-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="18f83-180">請注意，卸除頂點執行 hello 串聯刪除相關聯的邊緣。</span><span class="sxs-lookup"><span data-stu-id="18f83-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="18f83-181">查詢 hello 圖形</span><span class="sxs-lookup"><span data-stu-id="18f83-181">Query hello graph</span></span>

<span data-ttu-id="18f83-182">您也可以使用 Gremlin 來執行查詢和周遊。</span><span class="sxs-lookup"><span data-stu-id="18f83-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="18f83-183">例如，下列程式碼片段的 hello 顯示如何 toocount hello 的 hello 圖形中的頂點數目：</span><span class="sxs-lookup"><span data-stu-id="18f83-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="18f83-184">您可以執行使用 Gremlin 的篩選`has`和`hasLabel`步驟，並將它們結合使用`and`， `or`，和`not`toobuild 更複雜的篩選：</span><span class="sxs-lookup"><span data-stu-id="18f83-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="18f83-185">您可以投影中使用 hello hello 查詢結果的特定屬性`values`步驟：</span><span class="sxs-lookup"><span data-stu-id="18f83-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="18f83-186">到目前為止，我們只看到可在任何資料庫中運作的查詢運算子。</span><span class="sxs-lookup"><span data-stu-id="18f83-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="18f83-187">您需要 toonavigate toorelated 邊緣和頂點圖形進行快速且有效率的周遊作業。</span><span class="sxs-lookup"><span data-stu-id="18f83-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="18f83-188">我們將尋找 Thomas 的所有朋友。</span><span class="sxs-lookup"><span data-stu-id="18f83-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="18f83-189">要執行此作業使用 Gremlin 的`outE`逐步的 toofind 所有 hello-都邊緣從 Thomas、，然後從使用 Gremlin 的那些都邊緣周遊 toohello 中-頂點`inV`步驟：</span><span class="sxs-lookup"><span data-stu-id="18f83-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="18f83-190">hello 下一個查詢會執行兩個躍點 toofind Thomas'"朋友的朋友 」，藉由呼叫的所有`outE`和`inV`兩次。</span><span class="sxs-lookup"><span data-stu-id="18f83-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="18f83-191">您可以建立更複雜的查詢，並實作功能強大的圖形周遊邏輯使用 Gremlin，包括混合的篩選運算式中，執行迴圈使用 hello`loop`步驟中，實作條件式使用巡覽及 hello`choose`步驟。</span><span class="sxs-lookup"><span data-stu-id="18f83-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="18f83-192">深入了解您可以透過 [Gremlin 支援](gremlin-support.md)來執行哪些操作！</span><span class="sxs-lookup"><span data-stu-id="18f83-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="18f83-193">這樣就大功告成了，您已完成此 Azure Cosmos DB 教學課程！</span><span class="sxs-lookup"><span data-stu-id="18f83-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="18f83-194">清除資源</span><span class="sxs-lookup"><span data-stu-id="18f83-194">Clean up resources</span></span>

<span data-ttu-id="18f83-195">如果您不打算 toocontinue toouse 此應用程式，使用下列步驟 toodelete hello Azure 入口網站在此教學課程所建立的所有資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="18f83-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="18f83-196">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="18f83-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="18f83-197">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="18f83-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18f83-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18f83-198">Next Steps</span></span>

<span data-ttu-id="18f83-199">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="18f83-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18f83-200">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="18f83-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="18f83-201">建立圖形資料庫和容器</span><span class="sxs-lookup"><span data-stu-id="18f83-201">Created a graph database and container</span></span>
> * <span data-ttu-id="18f83-202">序列化的頂點和邊緣 too.NET 物件</span><span class="sxs-lookup"><span data-stu-id="18f83-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="18f83-203">新增頂點和邊緣</span><span class="sxs-lookup"><span data-stu-id="18f83-203">Added vertices and edges</span></span>
> * <span data-ttu-id="18f83-204">使用 Gremlin 查詢的 hello 圖形</span><span class="sxs-lookup"><span data-stu-id="18f83-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="18f83-205">您現在可以使用 Gremlin 來建置更複雜的查詢和實作強大的圖形周遊邏輯。</span><span class="sxs-lookup"><span data-stu-id="18f83-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="18f83-206">使用 Gremlin 進行查詢</span><span class="sxs-lookup"><span data-stu-id="18f83-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
