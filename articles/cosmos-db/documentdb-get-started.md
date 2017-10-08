---
title: "Azure Cosmos DB：開始使用 DocumentDB API 教學課程 | Microsoft Docs"
description: "教學課程中建立線上資料庫與 C# 主控台應用程式使用 hello DocumentDB API。"
keywords: "nosql 教學課程, 線上資料庫, c# 主控台應用程式"
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB：開始使用 DocumentDB API 教學課程
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

歡迎使用 toohello Azure Cosmos DB DocumentDB API 快速入門教學課程 ！ 完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。

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

沒有時間嗎？ 別擔心！ hello 完整解決方案位於[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)。 跳 toohello[取得 hello 完成 NoSQL 教學課程解決方案區段](#GetSolution)快速的指示。

之後，請使用 hello 投票按鈕 hello 上方或下方的這個頁面 toogive 我們意見反應。 如果您希望我們 toocontact 您直接，認為您的電子郵件地址可用 tooinclude 註解中。

讓我們開始吧！

## <a name="prerequisites"></a>必要條件
請確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。 
    * 或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程。
* [Visual Studio Community 2017](http://www.visualstudio.com/)。

## <a name="step-1-create-an-azure-cosmos-db-account"></a>步驟 1：建立 Azure Cosmos DB 帳戶
讓我們來建立 Azure Cosmos DB 帳戶。 如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[安裝 Visual Studio 方案](#SetupVS)。 如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[安裝 Visual Studio 方案](#SetupVS)。

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>步驟 2：設定您的 Visual Studio 方案
1. 在電腦上開啟 **Visual Studio 2017**。
2. 在 hello**檔案**功能表上，選取**新增**，然後選擇 **專案**。
3. 在 hello**新專案**對話方塊中，選取**範本** / **Visual C#** / **主控台應用程式**，名稱您的專案，並再按**確定**。
   ![Hello 新增專案 視窗的螢幕擷取畫面](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. 在 [hello**方案總管] 中**，新主控台應用程式，也就是在您的 Visual Studio 方案，以滑鼠右鍵按一下，然後按一下**管理 NuGet 封裝...**
    
    ![螢幕擷取畫面的權限 hello hello 專案的已按下功能表](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. 在 hello **Nuget**索引標籤上，按一下 **瀏覽**，然後輸入**azure documentdb** hello 搜尋 方塊中。
6. 在 hello 結果中尋找**Microsoft.Azure.DocumentDB**按一下**安裝**。
   hello 封裝識別碼 hello Azure Cosmos DB DocumentDB API 用戶端程式庫是[Microsoft Azure DocumentDB 用戶端程式庫](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)。
   ![尋找 Azure Cosmos DB 用戶端 SDK 的 Nuget 功能表 hello 的螢幕擷取畫面](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    如果您取得有關檢閱變更 toohello 解決方案的訊息，請按一下**確定**。 如果您收到關於接受授權的訊息，請按一下 [我接受]。

太棒了！ 現在我們完成 hello 安裝程式，讓我們開始撰寫一些程式碼。 您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs)找到本教學課程的完整程式碼專案。

## <a id="Connect"></a>步驟 3： 連接 tooan Azure Cosmos DB 帳戶
首先，加入下列參考應用程式的 C#，hello Program.cs 檔案中的 toohello 開頭：

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> 在順序 toocomplete hello 教學課程中，請確定您加入上述 hello 相依性。
> 
> 

現在，在「public class Program」之下加入下列兩個常數和您的「client」變數。

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

接下來，head 回 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的端點 URL 和主索引鍵。 hello 端點 URL 及主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。

在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，然後按一下**金鑰**。

從 hello 入口網站複製 hello URI，並將它貼入`<your endpoint URL>`hello program.cs 檔案中。 複製 hello 從 hello 入口網站的主索引鍵，並將它貼入`<your primary key>`。

![Hello hello NoSQL 教學課程 toocreate C# 主控台應用程式所使用的 Azure 入口網站的螢幕擷取畫面。 帳戶，反白顯示，hello 活躍 hello 反白顯示 hello Azure Cosmos DB 帳戶刀鋒視窗上的 [金鑰] 按鈕和 hello URI、 主索引鍵和次要索引鍵的值上反白顯示 hello 金鑰刀鋒視窗會顯示 Azure Cosmos DB][keys]

接下來，我們會先 hello 應用程式建立的新執行個體的 hello **DocumentClient**。

以下 hello **Main**方法中，新增此呼叫的非同步工作**GetStartedDemo**，它會具現化新**DocumentClient**。

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

新增 hello 下列程式碼 toorun 將您的非同步工作，從您**Main**方法。 hello **Main**方法將會攔截例外狀況，並將它們寫入 toohello 主控台。

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

按**F5** toorun 您的應用程式。 hello 主控台視窗輸出會顯示 hello 訊息`End of demo, press any key tooexit.`確認已 hello 連線。  然後，您可以關閉 hello 主控台視窗。 

恭喜！ 您已成功連接 tooan Azure Cosmos DB 帳戶，現在讓我們看一下使用 Azure Cosmos DB 資源。  

## <a name="step-4-create-a-database"></a>步驟 4：建立資料庫
您新增 hello 程式碼建立資料庫前，將撰寫 toohello 主控台的協助程式方法。

複製並貼上 hello **WriteToConsoleAndPromptToContinue**方法之後 hello **GetStartedDemo**方法。

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

您的 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)可以建立使用 hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx)方法 hello **DocumentClient**類別。 資料庫是 hello 的 JSON 文件儲存分割於各個集合的邏輯容器。

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 用戶端建立之後的方法。 這會建立名為 FamilyDB 的資料庫。

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

按**F5** toorun 您的應用程式。

恭喜！ 您已成功建立 Azure Cosmos DB 資料庫。  

## <a id="CreateColl"></a>步驟 5：建立集合
> [!WARNING]
> **CreateDocumentCollectionIfNotExistsAsync** 會建立含有保留輸送量且具有價格含意的新集合。 如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。
> 
> 

A[集合](documentdb-resources.md#collections)可以建立使用 hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx)方法 hello **DocumentClient**類別。 集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 建立資料庫之後的方法。 這會建立名為 FamilyCollection 的文件集合。

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

按**F5** toorun 您的應用程式。

恭喜！ 您已成功建立 Azure Cosmos DB 文件集合。  

## <a id="CreateDoc"></a>步驟 6：建立 JSON 文件
A[文件](documentdb-resources.md#documents)可以建立使用 hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx)方法 hello **DocumentClient**類別。 文件會是使用者定義的 (任意) JSON 內容。 現在可插入一或多份文件。 如果您已經有您想要 toostore 資料庫中的資料，您可以使用 hello Azure Cosmos DB[資料移轉工具](import-data.md)tooimport hello 資料插入資料庫。

首先，我們需要 toocreate**系列**表示儲存在 Azure Cosmos DB，在此範例中的物件類別。 我們也會建立 **Family** 內使用的 **Parent**、**Child**、**Pet**、**Address** 子類別。 請注意，文件必須將 **Id** 屬性序列化為 JSON 中的**識別碼**。 加入 hello 之後 hello 遵循內部的子類別來建立這些類別**GetStartedDemo**方法。

複製並貼上 hello**系列**，**父**，**子**，**寵物**，和**位址**之後 hello 類別**WriteToConsoleAndPromptToContinue**方法。

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

複製並貼上 hello **CreateFamilyDocumentIfNotExists**下方方法您**位址**類別。

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

然後插入兩個文件，分別指派給 hello Andersen 系列 hello Wakefield 系列。

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 文件集合建立後的方法。

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

按**F5** toorun 您的應用程式。

恭喜！ 您已成功建立兩個 Azure Cosmos DB 文件。  

![以圖表顯示的 hello 階層式關聯性，hello 帳戶、 hello 線上資料庫、 hello 集合和 hello hello NoSQL 教學課程 toocreate C# 主控台應用程式所使用的文件之間](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源
Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。  hello 下列程式碼範例示範各種查詢-使用這兩個 Azure Cosmos DB SQL 語法，以及 LINQ-我們能夠針對執行 hello 我們插入 hello 上一個步驟中的文件。

複製並貼上 hello **ExecuteSimpleQuery**方法之後您**CreateFamilyDocumentIfNotExists**方法。

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

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 第二個文件建立之後的方法。

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

按**F5** toorun 您的應用程式。

恭喜！ 您已成功查詢 Azure Cosmos DB 集合。

hello 下列圖表說明 hello Azure Cosmos DB SQL 查詢語法稱為 hello 集合針對您建立的方式，與 hello 相同邏輯適用於 toohello LINQ 查詢。

![圖表說明 hello 範圍和 hello 查詢的意義由 hello NoSQL 教學課程 toocreate C# 主控台應用程式](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

hello [FROM](documentdb-sql-query.md#FromClause)關鍵字是選擇性的 hello 查詢，因為 Azure Cosmos DB 查詢已設定領域的 tooa 單一集合。 因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。 Azure Cosmos DB 會推斷家族、 根或 hello 變數名稱您已選擇，依預設參考 hello 目前集合。

## <a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件
Azure Cosmos DB 支援取代 JSON 文件。  

複製並貼上 hello **ReplaceFamilyDocument**方法之後您**ExecuteSimpleQuery**方法。

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 查詢執行之後，在 hello hello 方法結尾處的方法。 這樣將會取代 hello 文件之後, 執行 hello 相同再次查詢 tooview hello 變更文件。

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

按**F5** toorun 您的應用程式。

恭喜！ 您已成功取代 Azure Cosmos DB 文件。

## <a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件
Azure Cosmos DB 支援刪除 JSON 文件。  

複製並貼上 hello **DeleteFamilyDocument**方法之後您**ReplaceFamilyDocument**方法。

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 第二個查詢執行後，在 hello hello 方法結尾處的方法。

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

按**F5** toorun 您的應用程式。

恭喜！ 您已成功刪除 Azure Cosmos DB 文件。

## <a id="DeleteDatabase"></a>步驟 10： 刪除 hello 資料庫
正在刪除 hello 已建立的資料庫將會移除 hello 資料庫和所有子系資源 （集合、 文件）。

複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**方法 hello 文件之後刪除 toodelete hello 整個資料庫和所有子系的資源。

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

按**F5** toorun 您的應用程式。

恭喜！ 您已成功刪除 Azure Cosmos DB 資料庫。

## <a id="Run"></a>步驟 11：一起執行您的 C# 主控台應用程式！
在 Visual Studio 中偵錯模式 toobuild hello 應用程式中按 F5。

您應該會看到 hello 輸出在主控台視窗中啟動應用程式取得。 hello 輸出會顯示 hello hello 結果我們加入，而且必須符合以下的 hello 範例文字的查詢。

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
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

恭喜！ 您已經完成 hello 教學課程，有一個使用 C# 主控台應用程式 ！

## <a id="GetSolution"></a>取得 hello 完整的教學課程解決方案
如果您沒有在這個教學課程中或只想 toodownload hello 程式碼範例中步驟 toocomplete hello 的時間，就可以從[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)。 

toobuild hello GetStarted 方案，您需要下列 hello:

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。
* [Azure Cosmos DB 帳戶][cosmos-db-create-account]。
* hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) GitHub 上有可用的解決方案。

toorestore hello 參考 toohello Azure Cosmos DB.NET SDK 在 Visual Studio 中，以滑鼠右鍵按一下 hello **GetStarted**方案在方案總管 中，然後按一下**啟用 NuGet 封裝還原**。 接下來，在 hello App.config 檔案中，更新 hello 的端點 Url 和 AuthorizationKey 值中所述[tooan Azure Cosmos DB 帳戶連接](#Connect)。

建置就這麼容易，繼續努力！


## <a name="next-steps"></a>後續步驟
* 需要更複雜的 ASP.NET MVC 教學課程嗎？ 請參閱 [ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-dotnet-application.md)。
* 想 tooperform 規模和效能測試以 Azure Cosmos DB 嗎？ 請參閱 [Azure Cosmos DB 的效能和級別測試](performance-testing.md)
* 了解如何太[監控 Azure Cosmos DB 要求、 使用方式，與儲存體](monitor-accounts.md)。
* 執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。
* toolearn 深入了解 Azure Cosmos DB，請參閱[歡迎 tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)。

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
