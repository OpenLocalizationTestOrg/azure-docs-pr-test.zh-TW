---
title: "Azure Cosmos DB：開始使用 DocumentDB API .NET Core 教學課程 | Microsoft Docs"
description: "教學課程中建立線上資料庫與 C# 主控台應用程式使用 hello Azure Cosmos DB DocumentDB API.NET Core SDK。"
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a>Azure Cosmos DB： 開始使用 DocumentDB API hello 和.NET 核心
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

歡迎使用 toohello Azure Cosmos DB 開始使用.NET Core 教學課程的 DocumentDB API ！ 完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。

本文將討論：

* 建立及連接 tooan Azure Cosmos DB 帳戶
* 設定 Visual Studio 方案
* 建立線上資料庫
* 建立集合
* 建立 JSON 文件
* 查詢 hello 集合
* 取代文件
* 刪除文件
* 刪除 hello 資料庫

沒有時間嗎？ 別擔心！ hello 完整解決方案位於[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)。 跳 toohello[取得 hello 完整的解決方案 > 一節](#GetSolution)快速的指示。

Xamarin iOS、 Android 或表單想 toobuild DocumentDB API 和.NET Core SDK 的應用程式使用 hello？ 請參閱[使用 Xamarin 和 Azure Cosmos DB 建置行動應用程式](mobile-apps-with-xamarin.md)。

> [!NOTE]
> hello Azure Cosmos DB.NET Core SDK 在本教學課程中使用尚未與通用 Windows 平台 (UWP) 應用程式相容。 如需 hello 支援 UWP 應用程式的.NET Core SDK 預覽版本，傳送電子郵件太[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。

讓我們開始吧！

## <a name="prerequisites"></a>必要條件
請確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。 
    * 或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程。
* [Visual Studio 2017](https://www.visualstudio.com/vs/) 
    * 如果您使用在 MacOS 或 Lunix 上，您可以藉由安裝 hello 開發.NET Core 應用程式，從命令列 hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) hello 平台，您所選擇。 
    * 如果您使用 Windows 上，您可以藉由安裝 hello 開發.NET Core 應用程式，從命令列 hello [.NET Core SDK](https://www.microsoft.com/net/core#windows)。 
    * 您可以使用自己的編輯器，也可以下載適用於 Windows、Linux 和 MacOS 的免費 [Visual Studio Code](https://code.visualstudio.com/)。 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>步驟 1：建立 Azure Cosmos DB 帳戶
讓我們來建立 Azure Cosmos DB 帳戶。 如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[安裝 Visual Studio 方案](#SetupVS)。 如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[安裝 Visual Studio 方案](#SetupVS)。

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>步驟 2：設定您的 Visual Studio 方案
1. 在電腦上開啟 **Visual Studio 2017**。
2. 在 hello**檔案**功能表上，選取**新增**，然後選擇 **專案**。
3. 在 hello**新專案**對話方塊中，選取**範本** / **Visual C#** / **.NET Core** /**主控台應用程式 (.NET Core)**，命名您的專案**DocumentDBGettingStarted**，然後按一下**確定**。

   ![Hello 新增專案 視窗的螢幕擷取畫面](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. 在 [hello**方案總管] 中**，以滑鼠右鍵按一下**DocumentDBGettingStarted**。
5. 而不需離開 hello 功能表，然後按一下 **管理 NuGet 封裝...**.

   ![螢幕擷取畫面的權限 hello hello 專案的已按下功能表](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. 在 hello **NuGet**索引標籤上，按一下 **瀏覽**頂端的 hello 視窗，然後輸入 hello **azure documentdb** hello 搜尋 方塊中。
7. 在 hello 結果中尋找**Microsoft.Azure.DocumentDB.Core**按一下**安裝**。
   hello 封裝識別碼 hello DocumentDB.NET Core 的用戶端程式庫是[Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)。 如果您是以此 .NET Core NuGet 套件不支援的 .NET Framework 版本 (例如 net461) 為目標，則使用 [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)，其支援 .NET Framework 4.5 以後的所有 .NET Framework 版本。
8. Hello 提示出現時，在接受 hello NuGet 封裝安裝與 hello 授權合約。

太棒了！ 現在我們完成 hello 安裝程式，讓我們開始撰寫一些程式碼。 您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)找到本教學課程的完整程式碼專案。

## <a id="Connect"></a>步驟 3： 連接 tooan Azure Cosmos DB 帳戶
首先，加入下列參考應用程式的 C#，hello Program.cs 檔案中的 toohello 開頭：

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> 在順序 toocomplete 本教學課程，請確認您新增上述 hello 相依性。

現在，在「public class Program」之下加入下列兩個常數和您的「client」變數。

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

接下來，前端 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的 URI 與主索引鍵。 hello Azure Cosmos DB URI 及主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。

在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，然後按一下**金鑰**。

從 hello 入口網站複製 hello URI，並將它貼入`<your endpoint URI>`hello program.cs 檔案中。 複製 hello 從 hello 入口網站的主索引鍵，並將它貼入`<your key>`。 如果您使用 hello Azure Cosmos DB 模擬器，使用`https://localhost:8081`hello 端點，以及從 hello 妥善定義的授權金鑰[如何使用 toodevelop hello Azure Cosmos DB 模擬器](local-emulator.md)。 請確定 tooremove hello < 和 > 但保留 hello 雙引號括住您的端點和金鑰。

![Hello hello NoSQL 教學課程 toocreate C# 主控台應用程式所使用的 Azure 入口網站的螢幕擷取畫面。 帳戶，反白顯示，hello 活躍 hello 反白顯示 hello Azure Cosmos DB 帳戶刀鋒視窗上的 [金鑰] 按鈕和 hello URI、 主索引鍵和次要索引鍵的值上反白顯示 hello 金鑰刀鋒視窗會顯示 Azure Cosmos DB][keys]

讓我們先 hello 取得啟動應用程式所建立的新執行個體的 hello **DocumentClient**。

以下 hello **Main**方法中，新增此呼叫的非同步工作**GetStartedDemo**，它會具現化新**DocumentClient**。

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

新增 hello 下列程式碼 toorun 將您的非同步工作，從您**Main**方法。 hello **Main**方法將會攔截例外狀況，並將它們寫入 toohello 主控台。

```csharp
static void Main(string[] args)
{
        // ADD THIS PART tooYOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key tooexit.");
                Console.ReadKey();
        }
```

按 hello **DocumentDBGettingStarted**按鈕 toobuild 並執行 hello 應用程式。

恭喜！ 您已成功連接 tooan Azure Cosmos DB 帳戶，現在讓我們看一下使用 Azure Cosmos DB 資源。  

## <a name="step-4-create-a-database"></a>步驟 4：建立資料庫
您新增 hello 程式碼建立資料庫前，將撰寫 toohello 主控台的協助程式方法。

複製並貼上 hello **WriteToConsoleAndPromptToContinue**下方 hello 方法**GetStartedDemo**方法。

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

您的 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)可以建立使用 hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx)方法 hello **DocumentClient**類別。 資料庫是 hello 的 JSON 文件儲存分割於各個集合的邏輯容器。

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**底下建立 hello 用戶端的方法。 這會建立名為 FamilyDB 的資料庫。

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。

恭喜！ 您已成功建立 Azure Cosmos DB 資料庫。  

## <a id="CreateColl"></a>步驟 5：建立集合
> [!WARNING]
> **CreateDocumentCollectionAsync** 會建立含有保留輸送量且具有價格含意的新集合。 如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。

A[集合](documentdb-resources.md#collections)可以建立使用 hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx)方法 hello **DocumentClient**類別。 集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 資料庫建立的方法。 這會建立名為 FamilyCollection_oa 的文件集合。

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。

恭喜！ 您已成功建立 Azure Cosmos DB 文件集合。  

## <a id="CreateDoc"></a>步驟 6：建立 JSON 文件
A[文件](documentdb-resources.md#documents)可以建立使用 hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx)方法 hello **DocumentClient**類別。 文件會是使用者定義的 (任意) JSON 內容。 現在可插入一或多份文件。 如果您已經有您想要 toostore 資料庫中的資料，您可以使用 Azure Cosmos DB 的[資料移轉工具](import-data.md)。

首先，我們需要 toocreate**系列**表示儲存在 Azure Cosmos DB，在此範例中的物件類別。 我們也會建立 **Family** 內使用的 **Parent**、**Child**、**Pet**、**Address** 子類別。 請注意，文件必須將 **Id** 屬性序列化為 JSON 中的**識別碼**。 加入 hello 之後 hello 遵循內部的子類別來建立這些類別**GetStartedDemo**方法。

複製並貼上 hello**系列**，**父**，**子**，**寵物**，和**位址**類別下方hello **WriteToConsoleAndPromptToContinue**方法。

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key toocontinue ...");
    Console.ReadKey();
}

// ADD THIS PART tooYOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

複製並貼上 hello **CreateFamilyDocumentIfNotExists**下方方法您**CreateDocumentCollectionIfNotExists**方法。

```csharp
// ADD THIS PART tooYOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

然後插入兩個文件，分別指派給 hello Andersen 系列 hello Wakefield 系列。

複製並貼上 hello 程式碼所示`// ADD THIS PART tooYOUR CODE`tooyour **GetStartedDemo**底下建立 hello 文件集合的方法。

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。

恭喜！ 您已成功建立兩個 Azure Cosmos DB 文件。  

![以圖表顯示的 hello 階層式關聯性，hello 帳戶、 hello 線上資料庫、 hello 集合和 hello hello NoSQL 教學課程 toocreate C# 主控台應用程式所使用的文件之間](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源
Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。  hello 下列程式碼範例示範各種查詢-使用這兩個 Azure Cosmos DB SQL 語法，以及 LINQ-我們能夠針對執行 hello 我們插入 hello 上一個步驟中的文件。

複製並貼上 hello **ExecuteSimpleQuery**下方方法您**CreateFamilyDocumentIfNotExists**方法。

```csharp
// ADD THIS PART tooYOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find hello Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute hello same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 建立第二個文件的方法。

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。

恭喜！ 您已成功查詢 Azure Cosmos DB 集合。

hello 下列圖表說明 hello Azure Cosmos DB SQL 查詢語法稱為 hello 集合針對您建立的方式，與 hello 相同邏輯適用於 toohello LINQ 查詢。

![圖表說明 hello 範圍和 hello 查詢的意義由 hello NoSQL 教學課程 toocreate C# 主控台應用程式](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

hello [FROM](documentdb-sql-query.md#FromClause)關鍵字是選擇性的 hello 查詢，因為 Azure Cosmos DB 查詢已設定領域的 tooa 單一集合。 因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。 DocumentDB 會推斷家族、 根或 hello 變數名稱您已選擇，依預設參考 hello 目前集合。

## <a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件
Azure Cosmos DB 支援取代 JSON 文件。  

複製並貼上 hello **ReplaceFamilyDocument**下方方法您**ExecuteSimpleQuery**方法。

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 查詢執行的方法。 這樣將會取代 hello 文件之後, 執行 hello 相同再次查詢 tooview hello 變更文件。

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。

恭喜！ 您已成功取代 Azure Cosmos DB 文件。

## <a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件
Azure Cosmos DB 支援刪除 JSON 文件。  

複製並貼上 hello **DeleteFamilyDocument**下方方法您**ReplaceFamilyDocument**方法。

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 第二個查詢執行的方法。

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。

恭喜！ 您已成功刪除 Azure Cosmos DB 文件。

## <a id="DeleteDatabase"></a>步驟 10： 刪除 hello 資料庫
正在刪除 hello 已建立的資料庫將會移除 hello 資料庫和所有子系資源 （集合、 文件）。

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 文件的方法刪除 toodelete hello 整個資料庫和所有子系的資源。

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。

恭喜！ 您已成功刪除 Azure Cosmos DB 資料庫。

## <a id="Run"></a>步驟 11：一起執行您的 C# 主控台應用程式！
按 hello **DocumentDBGettingStarted** Visual Studio 中偵錯模式 toobuild hello 應用程式中的按鈕。

您應該會看到 hello 輸出 hello 主控台視窗中啟動應用程式取得。 hello 輸出會顯示 hello hello 結果我們加入，而且必須符合以下的 hello 範例文字的查詢。

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
Press any key toocontinue ...
Created Family Andersen.1
Press any key toocontinue ...
Created Family Wakefield.7
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key tooexit.
```

恭喜！ 您已經完成 hello 教學課程，有一個使用 C# 主控台應用程式 ！

## <a id="GetSolution"></a>取得 hello 完整的教學課程解決方案
包含所有在本文中的 hello 範例 toobuild hello GetStarted 方案，您將需要 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。
* [Azure Cosmos DB 帳戶][create-documentdb-dotnet.md#create-account]。
* hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) GitHub 上有可用的解決方案。

toorestore hello 參考 toohello DocumentDB API 針對 Azure Cosmos DB.NET Core SDK 在 Visual Studio 中，以滑鼠右鍵按一下 hello **GetStarted**方案在方案總管 中，然後按一下**啟用 NuGet 封裝還原**. 接下來，在 hello Program.cs 檔案中，更新 hello 的端點 Url 和 AuthorizationKey 值中所述[tooan Azure Cosmos DB 帳戶連接](#Connect)。

## <a name="next-steps"></a>後續步驟
* 需要更複雜的 ASP.NET MVC 教學課程嗎？ 請參閱 [ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-dotnet-application.md)。
* 想 toodevelop Xamarin iOS、 Android 或表單應用程式使用 Azure Cosmos DB.NET Core sdk hello DocumentDB API 嗎？ 請參閱[使用 Xamarin 和 Azure Cosmos DB 建置行動應用程式](mobile-apps-with-xamarin.md)。
* 想 tooperform 規模和效能測試以 Azure Cosmos DB 嗎？ 請參閱 [Azure Cosmos DB 的效能和級別測試](performance-testing.md)
* 了解如何太[監視 Azure Cosmos DB 要求、 使用方式，以及儲存體](monitor-accounts.md)。
* 執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。
* toolearn 進一步了解 hello 的程式設計模型，請參閱[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
