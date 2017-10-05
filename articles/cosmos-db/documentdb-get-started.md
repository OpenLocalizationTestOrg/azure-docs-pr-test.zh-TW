---
title: "Azure Cosmos DB：開始使用 DocumentDB API 教學課程 | Microsoft Docs"
description: "本教學課程將使用 DocumentDB API 來建立線上資料庫，以及 C# 主控台應用程式。"
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
ms.openlocfilehash: 72f66081a6409f980ec6bca5188f585489245a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="69459-104">Azure Cosmos DB：開始使用 DocumentDB API 教學課程</span><span class="sxs-lookup"><span data-stu-id="69459-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69459-105">.NET</span><span class="sxs-lookup"><span data-stu-id="69459-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="69459-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="69459-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="69459-107">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="69459-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="69459-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="69459-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="69459-109">Java</span><span class="sxs-lookup"><span data-stu-id="69459-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="69459-110">C++</span><span class="sxs-lookup"><span data-stu-id="69459-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="69459-111">歡迎使用 Azure Cosmos DB DocumentDB API 入門教學課程！</span><span class="sxs-lookup"><span data-stu-id="69459-111">Welcome to the Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="69459-112">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="69459-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="69459-113">本文將討論：</span><span class="sxs-lookup"><span data-stu-id="69459-113">We'll cover:</span></span>

* <span data-ttu-id="69459-114">建立及連線至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="69459-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="69459-115">設定 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="69459-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="69459-116">建立線上資料庫</span><span class="sxs-lookup"><span data-stu-id="69459-116">Creating an online database</span></span>
* <span data-ttu-id="69459-117">建立集合</span><span class="sxs-lookup"><span data-stu-id="69459-117">Creating a collection</span></span>
* <span data-ttu-id="69459-118">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="69459-118">Creating JSON documents</span></span>
* <span data-ttu-id="69459-119">查詢集合</span><span class="sxs-lookup"><span data-stu-id="69459-119">Querying the collection</span></span>
* <span data-ttu-id="69459-120">取代文件</span><span class="sxs-lookup"><span data-stu-id="69459-120">Replacing a document</span></span>
* <span data-ttu-id="69459-121">刪除文件</span><span class="sxs-lookup"><span data-stu-id="69459-121">Deleting a document</span></span>
* <span data-ttu-id="69459-122">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="69459-122">Deleting the database</span></span>

<span data-ttu-id="69459-123">沒有時間嗎？</span><span class="sxs-lookup"><span data-stu-id="69459-123">Don't have time?</span></span> <span data-ttu-id="69459-124">別擔心！</span><span class="sxs-lookup"><span data-stu-id="69459-124">Don't worry!</span></span> <span data-ttu-id="69459-125">您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)上找到完整的方案。</span><span class="sxs-lookup"><span data-stu-id="69459-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="69459-126">請跳至 [取得完整的 NoSQL 教學課程解決方案](#GetSolution)一節，以取得簡要指示。</span><span class="sxs-lookup"><span data-stu-id="69459-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="69459-127">之後，請使用此頁面頂端或底部的投票按鈕，將意見反應提供給我們。</span><span class="sxs-lookup"><span data-stu-id="69459-127">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="69459-128">如果想要我們直接與您連絡，歡迎在留言中留下電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="69459-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="69459-129">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="69459-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69459-130">必要條件</span><span class="sxs-lookup"><span data-stu-id="69459-130">Prerequisites</span></span>
<span data-ttu-id="69459-131">請確定您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="69459-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="69459-132">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="69459-132">An active Azure account.</span></span> <span data-ttu-id="69459-133">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="69459-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="69459-134">或者，您可以使用 [Azure Cosmos DB 模擬器](local-emulator.md)來進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="69459-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="69459-135">[Visual Studio Community 2017](http://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="69459-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="69459-136">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="69459-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="69459-137">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="69459-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="69459-138">如果您已經擁有想要使用的帳戶，就可以跳到 [設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="69459-138">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="69459-139">如果您是使用「Azure Cosmos DB 模擬器」，請依照 [Azure Cosmos DB 模擬器](local-emulator.md)的步驟來設定模擬器，然後直接跳到[設定您的 Visual Studio 解決方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="69459-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="69459-140"><a id="SetupVS"></a>步驟 2：設定您的 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="69459-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="69459-141">在電腦上開啟 **Visual Studio 2017**。</span><span class="sxs-lookup"><span data-stu-id="69459-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="69459-142">從 [檔案] 功能表中，選取 [新增]，然後選擇 [專案]。</span><span class="sxs-lookup"><span data-stu-id="69459-142">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="69459-143">在 [新增專案]  對話方塊中，依序選取 [範本] / [Visual C#] / [主控台應用程式]、為專案命名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="69459-143">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="69459-144">![[新增專案] 視窗的螢幕擷取畫面](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="69459-144">![Screen shot of the New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="69459-145">在 [方案總管] 中，以滑鼠右鍵按一下 Visual Studio 方案底下的新主控台應用程式，然後按一下 [管理 NuGet 套件...]</span><span class="sxs-lookup"><span data-stu-id="69459-145">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![專案的滑鼠右鍵功能表的螢幕擷取畫面](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="69459-147">在 [Nuget] 索引標籤中按一下 [瀏覽]，然後在搜尋方塊中輸入 **azure documentdb**。</span><span class="sxs-lookup"><span data-stu-id="69459-147">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="69459-148">在結果中尋找 [Microsoft.Azure.DocumentDB]，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="69459-148">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="69459-149">「Azure Cosmos DB DocumentDB API 用戶端程式庫」的套件識別碼是 [Microsoft Azure DocumentDB 用戶端程式庫](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)。</span><span class="sxs-lookup"><span data-stu-id="69459-149">The package ID for the Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="69459-150">![用於尋找「Azure Cosmos DB 用戶端 SDK」之「NuGet 功能表」的螢幕擷取畫面](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="69459-150">![Screen shot of the Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="69459-151">如果您收到關於檢閱方案變更的訊息，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="69459-151">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="69459-152">如果您收到關於接受授權的訊息，請按一下 [我接受]。</span><span class="sxs-lookup"><span data-stu-id="69459-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="69459-153">太棒了！</span><span class="sxs-lookup"><span data-stu-id="69459-153">Great!</span></span> <span data-ttu-id="69459-154">現在已完成安裝程式，讓我們開始撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="69459-154">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="69459-155">您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs)找到本教學課程的完整程式碼專案。</span><span class="sxs-lookup"><span data-stu-id="69459-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="69459-156"><a id="Connect"></a>步驟 3：連接至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="69459-156"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="69459-157">首先，在 Program.cs 檔案中，將這些參考新增到 C# 應用程式的開頭：</span><span class="sxs-lookup"><span data-stu-id="69459-157">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="69459-158">若要完成此教學課程，請務必新增上述的相依性。</span><span class="sxs-lookup"><span data-stu-id="69459-158">In order to complete the tutorial, make sure you add the dependencies above.</span></span>
> 
> 

<span data-ttu-id="69459-159">現在，在「public class Program」之下加入下列兩個常數和您的「client」變數。</span><span class="sxs-lookup"><span data-stu-id="69459-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="69459-160">接下來，回到 [Azure 入口網站](https://portal.azure.com)擷取您的端點 URL 和主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="69459-160">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="69459-161">必須提供端點 URL 和主要金鑰，您的應用程式才能了解所要連線的位置，以及使 Azure Cosmos DB 信任您的應用程式連線。</span><span class="sxs-lookup"><span data-stu-id="69459-161">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="69459-162">在 Azure 入口網站中，瀏覽至 Azure Cosmos DB 帳戶，然後按一下 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="69459-162">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="69459-163">從入口網站複製 URI，並將它貼到 program.cs 檔案的 `<your endpoint URL>` 中。</span><span class="sxs-lookup"><span data-stu-id="69459-163">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="69459-164">然後從入口網站複製主要金鑰，並將它貼到 `<your primary key>`中。</span><span class="sxs-lookup"><span data-stu-id="69459-164">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![NoSQL 教學課程用來建立 C# 主控台應用程式之 Azure 入口網站的螢幕擷取畫面。][keys]

<span data-ttu-id="69459-167">接下來，我們會建立 **DocumentClient** 的新執行個體，以啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-167">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="69459-168">在 **Main** 方法底下，加入 **GetStartedDemo** 這個新的非同步工作，以將新的 **DocumentClient** 具現化。</span><span class="sxs-lookup"><span data-stu-id="69459-168">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="69459-169">加入下列程式碼，以從 **Main** 方法執行非同步工作。</span><span class="sxs-lookup"><span data-stu-id="69459-169">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="69459-170">**Main** 方法會攔截例外狀況並將它們寫入主控台。</span><span class="sxs-lookup"><span data-stu-id="69459-170">The **Main** method will catch exceptions and write them to the console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART TO YOUR CODE
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
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }

<span data-ttu-id="69459-171">按 **F5** 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-171">Press **F5** to run your application.</span></span> <span data-ttu-id="69459-172">主控台視窗輸出會顯示 `End of demo, press any key to exit.` 訊息，確認已進行連線。</span><span class="sxs-lookup"><span data-stu-id="69459-172">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="69459-173">您可以接著關閉主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="69459-173">You can then close the console window.</span></span> 

<span data-ttu-id="69459-174">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-174">Congratulations!</span></span> <span data-ttu-id="69459-175">您已成功連接至 Azure Cosmos DB 帳戶，現在讓我們看看如何使用 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="69459-175">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="69459-176">步驟 4：建立資料庫</span><span class="sxs-lookup"><span data-stu-id="69459-176">Step 4: Create a database</span></span>
<span data-ttu-id="69459-177">在您新增用於建立資料庫的程式碼之前，請新增用於寫入主控台的協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="69459-177">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="69459-178">複製 **WriteToConsoleAndPromptToContinue** 方法並貼到 **GetStartedDemo** 方法之後。</span><span class="sxs-lookup"><span data-stu-id="69459-178">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="69459-179">可以使用 **DocumentClient** 類別的 [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) 方法來建立 Azure Cosmos DB [資料庫](documentdb-resources.md#databases)。</span><span class="sxs-lookup"><span data-stu-id="69459-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="69459-180">資料庫是分割給多個集合之 JSON 文件儲存體的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="69459-180">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="69459-181">複製下列程式碼並貼到 **GetStartedDemo** 方法的用戶端建立之後。</span><span class="sxs-lookup"><span data-stu-id="69459-181">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="69459-182">這會建立名為 FamilyDB 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="69459-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="69459-183">按 **F5** 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-183">Press **F5** to run your application.</span></span>

<span data-ttu-id="69459-184">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-184">Congratulations!</span></span> <span data-ttu-id="69459-185">您已成功建立 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="69459-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="69459-186"><a id="CreateColl"></a>步驟 5：建立集合</span><span class="sxs-lookup"><span data-stu-id="69459-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="69459-187">**CreateDocumentCollectionIfNotExistsAsync** 會建立含有保留輸送量且具有價格含意的新集合。</span><span class="sxs-lookup"><span data-stu-id="69459-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="69459-188">如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="69459-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="69459-189">您可以使用 **DocumentClient** 類別的 [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) 方法建立[集合](documentdb-resources.md#collections)。</span><span class="sxs-lookup"><span data-stu-id="69459-189">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="69459-190">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="69459-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="69459-191">複製下列程式碼並貼到 **GetStartedDemo** 方法的資料庫建立之後。</span><span class="sxs-lookup"><span data-stu-id="69459-191">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="69459-192">這會建立名為 FamilyCollection 的文件集合。</span><span class="sxs-lookup"><span data-stu-id="69459-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="69459-193">按 **F5** 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-193">Press **F5** to run your application.</span></span>

<span data-ttu-id="69459-194">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-194">Congratulations!</span></span> <span data-ttu-id="69459-195">您已成功建立 Azure Cosmos DB 文件集合。</span><span class="sxs-lookup"><span data-stu-id="69459-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="69459-196"><a id="CreateDoc"></a>步驟 6：建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="69459-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="69459-197">您可以使用 **DocumentClient** 類別的 [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) 方法來建立[文件](documentdb-resources.md#documents)。</span><span class="sxs-lookup"><span data-stu-id="69459-197">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="69459-198">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="69459-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="69459-199">現在可插入一或多份文件。</span><span class="sxs-lookup"><span data-stu-id="69459-199">We can now insert one or more documents.</span></span> <span data-ttu-id="69459-200">如果您已經有想要儲存於資料庫中的資料，就可以使用 Azure Cosmos DB 的[資料移轉工具](import-data.md)，將資料匯入資料庫中。</span><span class="sxs-lookup"><span data-stu-id="69459-200">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="69459-201">首先，我們需要建立 **Family** 類別，以代表此範例中儲存在 Azure Cosmos DB 內的物件。</span><span class="sxs-lookup"><span data-stu-id="69459-201">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="69459-202">我們也會建立 **Family** 內使用的 **Parent**、**Child**、**Pet**、**Address** 子類別。</span><span class="sxs-lookup"><span data-stu-id="69459-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="69459-203">請注意，文件必須將 **Id** 屬性序列化為 JSON 中的**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="69459-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="69459-204">藉由在 **GetStartedDemo** 方法之後加入下列內部子類別來建立這些類別。</span><span class="sxs-lookup"><span data-stu-id="69459-204">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="69459-205">複製 **Family**、**Parent**、**Child**、**Pet** 和 **Address** 類別並貼到 **WriteToConsoleAndPromptToContinue** 方法之後。</span><span class="sxs-lookup"><span data-stu-id="69459-205">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="69459-206">複製 **CreateFamilyDocumentIfNotExists** 方法並貼到 [位址] 類別之下。</span><span class="sxs-lookup"><span data-stu-id="69459-206">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="69459-207">插入兩個文件，一個給 Andersen 家族，另一個給 Wakefield 家族。</span><span class="sxs-lookup"><span data-stu-id="69459-207">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="69459-208">複製下列程式碼並貼到 **GetStartedDemo** 方法的文件集合建立之後。</span><span class="sxs-lookup"><span data-stu-id="69459-208">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="69459-209">按 **F5** 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-209">Press **F5** to run your application.</span></span>

<span data-ttu-id="69459-210">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-210">Congratulations!</span></span> <span data-ttu-id="69459-211">您已成功建立兩個 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="69459-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![說明 NoSQL 教學課程用來建立 C# 主控台應用程式之帳戶、線上資料庫、集合和文件之間階層式關聯性的圖表](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="69459-213"><a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="69459-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="69459-214">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="69459-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="69459-215">下列範例程式碼示範各種查詢，同時使用可在我們於前一個步驟中所插入文件上執行的 Azure Cosmos DB SQL 語法和 LINQ。</span><span class="sxs-lookup"><span data-stu-id="69459-215">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="69459-216">複製 **ExecuteSimpleQuery** 方法並貼到 **CreateFamilyDocumentIfNotExists** 方法之後。</span><span class="sxs-lookup"><span data-stu-id="69459-216">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find the Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute the same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="69459-217">複製下列程式碼並貼到 **GetStartedDemo** 方法的次要文件建立之後。</span><span class="sxs-lookup"><span data-stu-id="69459-217">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="69459-218">按 **F5** 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-218">Press **F5** to run your application.</span></span>

<span data-ttu-id="69459-219">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-219">Congratulations!</span></span> <span data-ttu-id="69459-220">您已成功查詢 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="69459-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="69459-221">下圖說明如何針對您所建立的集合呼叫 Azure Cosmos DB SQL 查詢語法，相同邏輯也可以套用至 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="69459-221">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![說明 NoSQL 教學課程用來建立 C# 主控台應用程式之查詢的範圍和意義的圖表](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="69459-223">因為 Azure Cosmos DB 查詢已侷限於單一集合，所以查詢中的 [FROM](documentdb-sql-query.md#FromClause) 關鍵字是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="69459-223">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="69459-224">因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。</span><span class="sxs-lookup"><span data-stu-id="69459-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="69459-225">依預設，Azure Cosmos DB 會推斷該 Families、root 或您選擇的變數名稱來參考目前的集合。</span><span class="sxs-lookup"><span data-stu-id="69459-225">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="69459-226"><a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="69459-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="69459-227">Azure Cosmos DB 支援取代 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="69459-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="69459-228">複製 **ReplaceFamilyDocument** 方法並貼到 **ExecuteSimpleQuery** 方法之後。</span><span class="sxs-lookup"><span data-stu-id="69459-228">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="69459-229">複製下列程式碼並貼到 **GetStartedDemo** 方法的查詢執行之後 (在方法的結尾)。</span><span class="sxs-lookup"><span data-stu-id="69459-229">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="69459-230">取代文件後，此程式碼會再次執行相同的查詢以檢視變更後的文件。</span><span class="sxs-lookup"><span data-stu-id="69459-230">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="69459-231">按 **F5** 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-231">Press **F5** to run your application.</span></span>

<span data-ttu-id="69459-232">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-232">Congratulations!</span></span> <span data-ttu-id="69459-233">您已成功取代 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="69459-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="69459-234"><a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="69459-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="69459-235">Azure Cosmos DB 支援刪除 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="69459-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="69459-236">複製 **DeleteFamilyDocument** 方法並貼到 **ReplaceFamilyDocument** 方法之後。</span><span class="sxs-lookup"><span data-stu-id="69459-236">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="69459-237">複製下列程式碼並貼到 **GetStartedDemo** 方法的第二個查詢執行之後 (在方法的結尾)。</span><span class="sxs-lookup"><span data-stu-id="69459-237">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="69459-238">按 **F5** 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-238">Press **F5** to run your application.</span></span>

<span data-ttu-id="69459-239">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-239">Congratulations!</span></span> <span data-ttu-id="69459-240">您已成功刪除 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="69459-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="69459-241"><a id="DeleteDatabase"></a>步驟 10：刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="69459-241"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="69459-242">刪除已建立的資料庫將會移除資料庫和所有子系資源 (集合、文件等)。</span><span class="sxs-lookup"><span data-stu-id="69459-242">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="69459-243">複製下列程式碼並貼到 **GetStartedDemo** 方法的文件刪除之後，以刪除整個資料庫和所有子系資源。</span><span class="sxs-lookup"><span data-stu-id="69459-243">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="69459-244">按 **F5** 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-244">Press **F5** to run your application.</span></span>

<span data-ttu-id="69459-245">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-245">Congratulations!</span></span> <span data-ttu-id="69459-246">您已成功刪除 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="69459-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="69459-247"><a id="Run"></a>步驟 11：一起執行您的 C# 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="69459-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="69459-248">在 Visual Studio 中按 F5，即可在偵錯模式下建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="69459-248">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="69459-249">您應該會在主控台視窗中看到入門應用程式的輸出。</span><span class="sxs-lookup"><span data-stu-id="69459-249">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="69459-250">輸出將會顯示新增的查詢結果，而且應該符合以下的範例文字。</span><span class="sxs-lookup"><span data-stu-id="69459-250">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
    Press any key to continue ...
    Created Family Andersen.1
    Press any key to continue ...
    Created Family Wakefield.7
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key to exit.

<span data-ttu-id="69459-251">恭喜！</span><span class="sxs-lookup"><span data-stu-id="69459-251">Congratulations!</span></span> <span data-ttu-id="69459-252">您已經完成本教學課程，並擁有運作中的 C# 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="69459-252">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="69459-253"><a id="GetSolution"></a>取得完整的教學課程解決方案</span><span class="sxs-lookup"><span data-stu-id="69459-253"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="69459-254">如果您沒有時間完成本教學課程中的步驟，或只想要下載程式碼範例，您可以從 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) 取得程式碼。</span><span class="sxs-lookup"><span data-stu-id="69459-254">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="69459-255">若要建置 GetStarted 方案，您將需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="69459-255">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="69459-256">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="69459-256">An active Azure account.</span></span> <span data-ttu-id="69459-257">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="69459-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="69459-258">[Azure Cosmos DB 帳戶][cosmos-db-create-account]。</span><span class="sxs-lookup"><span data-stu-id="69459-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="69459-259">您可以在 GitHub 上找到 [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) 方案。</span><span class="sxs-lookup"><span data-stu-id="69459-259">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="69459-260">若要在 Visual Studio 中還原 Azure Cosmos DB .NET SDK 的參考，請在 [方案總管] 的 **GetStarted** 方案上按一下滑鼠右鍵，然後按一下 [啟用 NuGet 套件還原]。</span><span class="sxs-lookup"><span data-stu-id="69459-260">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="69459-261">接下來，在 App.config 檔案中更新 EndpointUrl 和 AuthorizationKey 值，如[連線至 Azure Cosmos DB 帳戶](#Connect)中所述。</span><span class="sxs-lookup"><span data-stu-id="69459-261">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="69459-262">建置就這麼容易，繼續努力！</span><span class="sxs-lookup"><span data-stu-id="69459-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="69459-263">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69459-263">Next steps</span></span>
* <span data-ttu-id="69459-264">需要更複雜的 ASP.NET MVC 教學課程嗎？</span><span class="sxs-lookup"><span data-stu-id="69459-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="69459-265">請參閱 [ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-dotnet-application.md)。</span><span class="sxs-lookup"><span data-stu-id="69459-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="69459-266">需要使用 Azure Cosmos DB 來執行規模和效能測試嗎？</span><span class="sxs-lookup"><span data-stu-id="69459-266">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="69459-267">請參閱 [Azure Cosmos DB 的效能和級別測試](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="69459-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="69459-268">了解如何[監視 Azure Cosmos DB 要求、使用量及儲存體](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="69459-268">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="69459-269">在 [Query Playground](https://www.documentdb.com/sql/demo)中，針對範例資料集執行查詢。</span><span class="sxs-lookup"><span data-stu-id="69459-269">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="69459-270">若要深入了解 Azure Cosmos DB，請參閱[歡迎使用 Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)。</span><span class="sxs-lookup"><span data-stu-id="69459-270">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
