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
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="4d8be-104">Azure Cosmos DB：開始使用 DocumentDB API 教學課程</span><span class="sxs-lookup"><span data-stu-id="4d8be-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d8be-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4d8be-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="4d8be-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4d8be-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="4d8be-107">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="4d8be-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="4d8be-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="4d8be-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="4d8be-109">Java</span><span class="sxs-lookup"><span data-stu-id="4d8be-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="4d8be-110">C++</span><span class="sxs-lookup"><span data-stu-id="4d8be-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="4d8be-111">歡迎使用 toohello Azure Cosmos DB DocumentDB API 快速入門教學課程 ！</span><span class="sxs-lookup"><span data-stu-id="4d8be-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="4d8be-112">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="4d8be-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="4d8be-113">本文將討論：</span><span class="sxs-lookup"><span data-stu-id="4d8be-113">We'll cover:</span></span>

* <span data-ttu-id="4d8be-114">建立及連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="4d8be-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="4d8be-115">設定 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="4d8be-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="4d8be-116">建立線上資料庫</span><span class="sxs-lookup"><span data-stu-id="4d8be-116">Creating an online database</span></span>
* <span data-ttu-id="4d8be-117">建立集合</span><span class="sxs-lookup"><span data-stu-id="4d8be-117">Creating a collection</span></span>
* <span data-ttu-id="4d8be-118">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="4d8be-118">Creating JSON documents</span></span>
* <span data-ttu-id="4d8be-119">查詢 hello 集合</span><span class="sxs-lookup"><span data-stu-id="4d8be-119">Querying hello collection</span></span>
* <span data-ttu-id="4d8be-120">取代文件</span><span class="sxs-lookup"><span data-stu-id="4d8be-120">Replacing a document</span></span>
* <span data-ttu-id="4d8be-121">刪除文件</span><span class="sxs-lookup"><span data-stu-id="4d8be-121">Deleting a document</span></span>
* <span data-ttu-id="4d8be-122">刪除 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="4d8be-122">Deleting hello database</span></span>

<span data-ttu-id="4d8be-123">沒有時間嗎？</span><span class="sxs-lookup"><span data-stu-id="4d8be-123">Don't have time?</span></span> <span data-ttu-id="4d8be-124">別擔心！</span><span class="sxs-lookup"><span data-stu-id="4d8be-124">Don't worry!</span></span> <span data-ttu-id="4d8be-125">hello 完整解決方案位於[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="4d8be-126">跳 toohello[取得 hello 完成 NoSQL 教學課程解決方案區段](#GetSolution)快速的指示。</span><span class="sxs-lookup"><span data-stu-id="4d8be-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="4d8be-127">之後，請使用 hello 投票按鈕 hello 上方或下方的這個頁面 toogive 我們意見反應。</span><span class="sxs-lookup"><span data-stu-id="4d8be-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="4d8be-128">如果您希望我們 toocontact 您直接，認為您的電子郵件地址可用 tooinclude 註解中。</span><span class="sxs-lookup"><span data-stu-id="4d8be-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="4d8be-129">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="4d8be-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d8be-130">必要條件</span><span class="sxs-lookup"><span data-stu-id="4d8be-130">Prerequisites</span></span>
<span data-ttu-id="4d8be-131">請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4d8be-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="4d8be-132">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d8be-132">An active Azure account.</span></span> <span data-ttu-id="4d8be-133">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="4d8be-134">或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程。</span><span class="sxs-lookup"><span data-stu-id="4d8be-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="4d8be-135">[Visual Studio Community 2017](http://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="4d8be-136">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="4d8be-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="4d8be-137">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d8be-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="4d8be-138">如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[安裝 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="4d8be-139">如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[安裝 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="4d8be-140"><a id="SetupVS"></a>步驟 2：設定您的 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="4d8be-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="4d8be-141">在電腦上開啟 **Visual Studio 2017**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="4d8be-142">在 hello**檔案**功能表上，選取**新增**，然後選擇 **專案**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="4d8be-143">在 hello**新專案**對話方塊中，選取**範本** / **Visual C#** / **主控台應用程式**，名稱您的專案，並再按**確定**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="4d8be-144">![Hello 新增專案 視窗的螢幕擷取畫面](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="4d8be-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="4d8be-145">在 [hello**方案總管] 中**，新主控台應用程式，也就是在您的 Visual Studio 方案，以滑鼠右鍵按一下，然後按一下**管理 NuGet 封裝...**</span><span class="sxs-lookup"><span data-stu-id="4d8be-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![螢幕擷取畫面的權限 hello hello 專案的已按下功能表](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="4d8be-147">在 hello **Nuget**索引標籤上，按一下 **瀏覽**，然後輸入**azure documentdb** hello 搜尋 方塊中。</span><span class="sxs-lookup"><span data-stu-id="4d8be-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="4d8be-148">在 hello 結果中尋找**Microsoft.Azure.DocumentDB**按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="4d8be-149">hello 封裝識別碼 hello Azure Cosmos DB DocumentDB API 用戶端程式庫是[Microsoft Azure DocumentDB 用戶端程式庫](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="4d8be-150">![尋找 Azure Cosmos DB 用戶端 SDK 的 Nuget 功能表 hello 的螢幕擷取畫面](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="4d8be-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="4d8be-151">如果您取得有關檢閱變更 toohello 解決方案的訊息，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="4d8be-152">如果您收到關於接受授權的訊息，請按一下 [我接受]。</span><span class="sxs-lookup"><span data-stu-id="4d8be-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="4d8be-153">太棒了！</span><span class="sxs-lookup"><span data-stu-id="4d8be-153">Great!</span></span> <span data-ttu-id="4d8be-154">現在我們完成 hello 安裝程式，讓我們開始撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="4d8be-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="4d8be-155">您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs)找到本教學課程的完整程式碼專案。</span><span class="sxs-lookup"><span data-stu-id="4d8be-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="4d8be-156"><a id="Connect"></a>步驟 3： 連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="4d8be-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="4d8be-157">首先，加入下列參考應用程式的 C#，hello Program.cs 檔案中的 toohello 開頭：</span><span class="sxs-lookup"><span data-stu-id="4d8be-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="4d8be-158">在順序 toocomplete hello 教學課程中，請確定您加入上述 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="4d8be-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="4d8be-159">現在，在「public class Program」之下加入下列兩個常數和您的「client」變數。</span><span class="sxs-lookup"><span data-stu-id="4d8be-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="4d8be-160">接下來，head 回 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的端點 URL 和主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="4d8be-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="4d8be-161">hello 端點 URL 及主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。</span><span class="sxs-lookup"><span data-stu-id="4d8be-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="4d8be-162">在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，然後按一下**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="4d8be-163">從 hello 入口網站複製 hello URI，並將它貼入`<your endpoint URL>`hello program.cs 檔案中。</span><span class="sxs-lookup"><span data-stu-id="4d8be-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="4d8be-164">複製 hello 從 hello 入口網站的主索引鍵，並將它貼入`<your primary key>`。</span><span class="sxs-lookup"><span data-stu-id="4d8be-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Hello hello NoSQL 教學課程 toocreate C# 主控台應用程式所使用的 Azure 入口網站的螢幕擷取畫面。][keys]

<span data-ttu-id="4d8be-167">接下來，我們會先 hello 應用程式建立的新執行個體的 hello **DocumentClient**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="4d8be-168">以下 hello **Main**方法中，新增此呼叫的非同步工作**GetStartedDemo**，它會具現化新**DocumentClient**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="4d8be-169">新增 hello 下列程式碼 toorun 將您的非同步工作，從您**Main**方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="4d8be-170">hello **Main**方法將會攔截例外狀況，並將它們寫入 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="4d8be-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="4d8be-171">按**F5** toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8be-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="4d8be-172">hello 主控台視窗輸出會顯示 hello 訊息`End of demo, press any key tooexit.`確認已 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="4d8be-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="4d8be-173">然後，您可以關閉 hello 主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="4d8be-173">You can then close hello console window.</span></span> 

<span data-ttu-id="4d8be-174">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-174">Congratulations!</span></span> <span data-ttu-id="4d8be-175">您已成功連接 tooan Azure Cosmos DB 帳戶，現在讓我們看一下使用 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="4d8be-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="4d8be-176">步驟 4：建立資料庫</span><span class="sxs-lookup"><span data-stu-id="4d8be-176">Step 4: Create a database</span></span>
<span data-ttu-id="4d8be-177">您新增 hello 程式碼建立資料庫前，將撰寫 toohello 主控台的協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="4d8be-178">複製並貼上 hello **WriteToConsoleAndPromptToContinue**方法之後 hello **GetStartedDemo**方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="4d8be-179">您的 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)可以建立使用 hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="4d8be-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="4d8be-180">資料庫是 hello 的 JSON 文件儲存分割於各個集合的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="4d8be-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="4d8be-181">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 用戶端建立之後的方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="4d8be-182">這會建立名為 FamilyDB 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d8be-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="4d8be-183">按**F5** toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8be-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="4d8be-184">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-184">Congratulations!</span></span> <span data-ttu-id="4d8be-185">您已成功建立 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d8be-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="4d8be-186"><a id="CreateColl"></a>步驟 5：建立集合</span><span class="sxs-lookup"><span data-stu-id="4d8be-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="4d8be-187">**CreateDocumentCollectionIfNotExistsAsync** 會建立含有保留輸送量且具有價格含意的新集合。</span><span class="sxs-lookup"><span data-stu-id="4d8be-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="4d8be-188">如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="4d8be-189">A[集合](documentdb-resources.md#collections)可以建立使用 hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="4d8be-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="4d8be-190">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="4d8be-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="4d8be-191">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 建立資料庫之後的方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="4d8be-192">這會建立名為 FamilyCollection 的文件集合。</span><span class="sxs-lookup"><span data-stu-id="4d8be-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="4d8be-193">按**F5** toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8be-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="4d8be-194">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-194">Congratulations!</span></span> <span data-ttu-id="4d8be-195">您已成功建立 Azure Cosmos DB 文件集合。</span><span class="sxs-lookup"><span data-stu-id="4d8be-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="4d8be-196"><a id="CreateDoc"></a>步驟 6：建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="4d8be-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="4d8be-197">A[文件](documentdb-resources.md#documents)可以建立使用 hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="4d8be-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="4d8be-198">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="4d8be-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="4d8be-199">現在可插入一或多份文件。</span><span class="sxs-lookup"><span data-stu-id="4d8be-199">We can now insert one or more documents.</span></span> <span data-ttu-id="4d8be-200">如果您已經有您想要 toostore 資料庫中的資料，您可以使用 hello Azure Cosmos DB[資料移轉工具](import-data.md)tooimport hello 資料插入資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d8be-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="4d8be-201">首先，我們需要 toocreate**系列**表示儲存在 Azure Cosmos DB，在此範例中的物件類別。</span><span class="sxs-lookup"><span data-stu-id="4d8be-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="4d8be-202">我們也會建立 **Family** 內使用的 **Parent**、**Child**、**Pet**、**Address** 子類別。</span><span class="sxs-lookup"><span data-stu-id="4d8be-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="4d8be-203">請注意，文件必須將 **Id** 屬性序列化為 JSON 中的**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="4d8be-204">加入 hello 之後 hello 遵循內部的子類別來建立這些類別**GetStartedDemo**方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="4d8be-205">複製並貼上 hello**系列**，**父**，**子**，**寵物**，和**位址**之後 hello 類別**WriteToConsoleAndPromptToContinue**方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="4d8be-206">複製並貼上 hello **CreateFamilyDocumentIfNotExists**下方方法您**位址**類別。</span><span class="sxs-lookup"><span data-stu-id="4d8be-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="4d8be-207">然後插入兩個文件，分別指派給 hello Andersen 系列 hello Wakefield 系列。</span><span class="sxs-lookup"><span data-stu-id="4d8be-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="4d8be-208">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 文件集合建立後的方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

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

<span data-ttu-id="4d8be-209">按**F5** toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8be-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="4d8be-210">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-210">Congratulations!</span></span> <span data-ttu-id="4d8be-211">您已成功建立兩個 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="4d8be-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![以圖表顯示的 hello 階層式關聯性，hello 帳戶、 hello 線上資料庫、 hello 集合和 hello hello NoSQL 教學課程 toocreate C# 主控台應用程式所使用的文件之間](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="4d8be-213"><a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="4d8be-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="4d8be-214">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="4d8be-215">hello 下列程式碼範例示範各種查詢-使用這兩個 Azure Cosmos DB SQL 語法，以及 LINQ-我們能夠針對執行 hello 我們插入 hello 上一個步驟中的文件。</span><span class="sxs-lookup"><span data-stu-id="4d8be-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="4d8be-216">複製並貼上 hello **ExecuteSimpleQuery**方法之後您**CreateFamilyDocumentIfNotExists**方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="4d8be-217">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 第二個文件建立之後的方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="4d8be-218">按**F5** toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8be-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="4d8be-219">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-219">Congratulations!</span></span> <span data-ttu-id="4d8be-220">您已成功查詢 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="4d8be-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="4d8be-221">hello 下列圖表說明 hello Azure Cosmos DB SQL 查詢語法稱為 hello 集合針對您建立的方式，與 hello 相同邏輯適用於 toohello LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="4d8be-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![圖表說明 hello 範圍和 hello 查詢的意義由 hello NoSQL 教學課程 toocreate C# 主控台應用程式](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="4d8be-223">hello [FROM](documentdb-sql-query.md#FromClause)關鍵字是選擇性的 hello 查詢，因為 Azure Cosmos DB 查詢已設定領域的 tooa 單一集合。</span><span class="sxs-lookup"><span data-stu-id="4d8be-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="4d8be-224">因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。</span><span class="sxs-lookup"><span data-stu-id="4d8be-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="4d8be-225">Azure Cosmos DB 會推斷家族、 根或 hello 變數名稱您已選擇，依預設參考 hello 目前集合。</span><span class="sxs-lookup"><span data-stu-id="4d8be-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="4d8be-226"><a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="4d8be-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="4d8be-227">Azure Cosmos DB 支援取代 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="4d8be-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="4d8be-228">複製並貼上 hello **ReplaceFamilyDocument**方法之後您**ExecuteSimpleQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="4d8be-229">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 查詢執行之後，在 hello hello 方法結尾處的方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="4d8be-230">這樣將會取代 hello 文件之後, 執行 hello 相同再次查詢 tooview hello 變更文件。</span><span class="sxs-lookup"><span data-stu-id="4d8be-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="4d8be-231">按**F5** toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8be-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="4d8be-232">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-232">Congratulations!</span></span> <span data-ttu-id="4d8be-233">您已成功取代 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="4d8be-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="4d8be-234"><a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="4d8be-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="4d8be-235">Azure Cosmos DB 支援刪除 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="4d8be-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="4d8be-236">複製並貼上 hello **DeleteFamilyDocument**方法之後您**ReplaceFamilyDocument**方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="4d8be-237">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo** hello 第二個查詢執行後，在 hello hello 方法結尾處的方法。</span><span class="sxs-lookup"><span data-stu-id="4d8be-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="4d8be-238">按**F5** toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8be-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="4d8be-239">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-239">Congratulations!</span></span> <span data-ttu-id="4d8be-240">您已成功刪除 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="4d8be-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="4d8be-241"><a id="DeleteDatabase"></a>步驟 10： 刪除 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="4d8be-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="4d8be-242">正在刪除 hello 已建立的資料庫將會移除 hello 資料庫和所有子系資源 （集合、 文件）。</span><span class="sxs-lookup"><span data-stu-id="4d8be-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="4d8be-243">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**方法 hello 文件之後刪除 toodelete hello 整個資料庫和所有子系的資源。</span><span class="sxs-lookup"><span data-stu-id="4d8be-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="4d8be-244">按**F5** toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8be-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="4d8be-245">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-245">Congratulations!</span></span> <span data-ttu-id="4d8be-246">您已成功刪除 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d8be-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="4d8be-247"><a id="Run"></a>步驟 11：一起執行您的 C# 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="4d8be-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="4d8be-248">在 Visual Studio 中偵錯模式 toobuild hello 應用程式中按 F5。</span><span class="sxs-lookup"><span data-stu-id="4d8be-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="4d8be-249">您應該會看到 hello 輸出在主控台視窗中啟動應用程式取得。</span><span class="sxs-lookup"><span data-stu-id="4d8be-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="4d8be-250">hello 輸出會顯示 hello hello 結果我們加入，而且必須符合以下的 hello 範例文字的查詢。</span><span class="sxs-lookup"><span data-stu-id="4d8be-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

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

<span data-ttu-id="4d8be-251">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8be-251">Congratulations!</span></span> <span data-ttu-id="4d8be-252">您已經完成 hello 教學課程，有一個使用 C# 主控台應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="4d8be-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="4d8be-253"><a id="GetSolution"></a>取得 hello 完整的教學課程解決方案</span><span class="sxs-lookup"><span data-stu-id="4d8be-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="4d8be-254">如果您沒有在這個教學課程中或只想 toodownload hello 程式碼範例中步驟 toocomplete hello 的時間，就可以從[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="4d8be-255">toobuild hello GetStarted 方案，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4d8be-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="4d8be-256">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d8be-256">An active Azure account.</span></span> <span data-ttu-id="4d8be-257">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="4d8be-258">[Azure Cosmos DB 帳戶][cosmos-db-create-account]。</span><span class="sxs-lookup"><span data-stu-id="4d8be-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="4d8be-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) GitHub 上有可用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4d8be-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="4d8be-260">toorestore hello 參考 toohello Azure Cosmos DB.NET SDK 在 Visual Studio 中，以滑鼠右鍵按一下 hello **GetStarted**方案在方案總管 中，然後按一下**啟用 NuGet 封裝還原**。</span><span class="sxs-lookup"><span data-stu-id="4d8be-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="4d8be-261">接下來，在 hello App.config 檔案中，更新 hello 的端點 Url 和 AuthorizationKey 值中所述[tooan Azure Cosmos DB 帳戶連接](#Connect)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="4d8be-262">建置就這麼容易，繼續努力！</span><span class="sxs-lookup"><span data-stu-id="4d8be-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="4d8be-263">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d8be-263">Next steps</span></span>
* <span data-ttu-id="4d8be-264">需要更複雜的 ASP.NET MVC 教學課程嗎？</span><span class="sxs-lookup"><span data-stu-id="4d8be-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="4d8be-265">請參閱 [ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-dotnet-application.md)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="4d8be-266">想 tooperform 規模和效能測試以 Azure Cosmos DB 嗎？</span><span class="sxs-lookup"><span data-stu-id="4d8be-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="4d8be-267">請參閱 [Azure Cosmos DB 的效能和級別測試](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="4d8be-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="4d8be-268">了解如何太[監控 Azure Cosmos DB 要求、 使用方式，與儲存體](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="4d8be-269">執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="4d8be-270">toolearn 深入了解 Azure Cosmos DB，請參閱[歡迎 tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)。</span><span class="sxs-lookup"><span data-stu-id="4d8be-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
