---
title: "aaaUse Azure Cosmos DB 的應用程式開發介面的 MongoDB toobuild web 應用程式 |Microsoft 文件"
description: "Azure Cosmos DB 教學課程會建立使用 MongoDB hello API 線上資料庫 web 應用程式。"
keywords: "mongodb 範例"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="63907-104">Azure Cosmos DB： 連接 tooa MongoDB 應用程式使用.NET</span><span class="sxs-lookup"><span data-stu-id="63907-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="63907-105">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="63907-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="63907-106">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="63907-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="63907-107">本教學課程示範如何 toocreate Azure Cosmos DB 帳戶使用 hello Azure 入口網站和 toocreate 資料庫集合 toostore 使用和資料的 hello [MongoDB API](mongodb-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="63907-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="63907-108">本教學課程涵蓋 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="63907-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="63907-109">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="63907-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="63907-110">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="63907-110">Update your connection string</span></span>
> * <span data-ttu-id="63907-111">在虛擬機器上建立 MongoDB 應用程式</span><span class="sxs-lookup"><span data-stu-id="63907-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="63907-112">建立資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="63907-112">Create a database account</span></span>

<span data-ttu-id="63907-113">首先在 hello Azure 入口網站中建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="63907-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="63907-114">已經有 Azure Cosmos DB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="63907-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="63907-115">如果是這樣，跳過[設定您的 Visual Studio 方案](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="63907-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="63907-116">您是否已有 Azure DocumentDB 帳戶？</span><span class="sxs-lookup"><span data-stu-id="63907-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="63907-117">如果因此，您的帳戶現在是 Azure Cosmos DB 帳戶，而且您可以向前跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="63907-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="63907-118">如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="63907-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="63907-119">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="63907-119">Update your connection string</span></span>

1. <span data-ttu-id="63907-120">在 Azure 入口網站中 hello hello **Azure Cosmos DB**頁面上，選取 hello API MongoDB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="63907-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="63907-121">Hello 左列中的 hello 帳戶 刀鋒視窗，按一下**快速入門**。</span><span class="sxs-lookup"><span data-stu-id="63907-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="63907-122">選擇您的平台 (*.NET 驅動程式*、*Node.js 驅動程式*、*MongoDB 殼層*、*Java 驅動程式*、*Python 驅動程式*)。</span><span class="sxs-lookup"><span data-stu-id="63907-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="63907-123">如果您沒有看到您的驅動程式或工具被列出，別擔心，我們會持續加入更多連線程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="63907-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="63907-124">複製並貼入 MongoDB 應用程式，hello 程式碼片段，而且您準備好 toogo。</span><span class="sxs-lookup"><span data-stu-id="63907-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="63907-125">設定您的 MongoDB 應用程式</span><span class="sxs-lookup"><span data-stu-id="63907-125">Set up your MongoDB app</span></span>

<span data-ttu-id="63907-126">您可以使用 hello[連接 tooMongoDB 虛擬機器上執行的 Azure 中建立 web 應用程式](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md)教學課程，以最少的修改，tooquickly 安裝 MongoDB 應用程式 (請在本機或已發行的 tooan Azure web 應用程式)，連接 MongoDB 帳戶 tooan API。</span><span class="sxs-lookup"><span data-stu-id="63907-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="63907-127">請遵循 hello 的教學課程中，有一項修改。</span><span class="sxs-lookup"><span data-stu-id="63907-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="63907-128">Hello Dal.cs 程式碼取代這：</span><span class="sxs-lookup"><span data-stu-id="63907-128">Replace hello Dal.cs code with this:</span></span>

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }
   
            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }
   
            private IMongoCollection<MyTask> GetTasksCollection()
            {
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
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
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
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            # region IDisposable
   
            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }
   
            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. <span data-ttu-id="63907-129">修改 hello hello hello Azure 入口網站中的索引鍵 頁面中的下列每個帳戶設定 hello Dal.cs 檔案中的變數：</span><span class="sxs-lookup"><span data-stu-id="63907-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="63907-130">使用 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="63907-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="63907-131">清除資源</span><span class="sxs-lookup"><span data-stu-id="63907-131">Clean up resources</span></span>

<span data-ttu-id="63907-132">如果您不打算 toocontinue toouse 此應用程式，使用下列步驟 toodelete hello Azure 入口網站在此教學課程所建立的所有資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="63907-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="63907-133">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="63907-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="63907-134">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="63907-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63907-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63907-135">Next steps</span></span>

<span data-ttu-id="63907-136">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="63907-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="63907-137">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="63907-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="63907-138">更新您的連接字串</span><span class="sxs-lookup"><span data-stu-id="63907-138">Update your connection string</span></span>
> * <span data-ttu-id="63907-139">在虛擬機器上建立 MongoDB 應用程式</span><span class="sxs-lookup"><span data-stu-id="63907-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="63907-140">您可以繼續進行下一個教學課程 toohello 並匯入您 MongoDB 資料 tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="63907-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="63907-141">將 MongoDB 資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="63907-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

