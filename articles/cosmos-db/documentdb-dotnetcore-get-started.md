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
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="498d1-103">Azure Cosmos DB： 開始使用 DocumentDB API hello 和.NET 核心</span><span class="sxs-lookup"><span data-stu-id="498d1-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="498d1-104">.NET</span><span class="sxs-lookup"><span data-stu-id="498d1-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="498d1-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="498d1-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="498d1-106">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="498d1-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="498d1-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="498d1-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="498d1-108">Java</span><span class="sxs-lookup"><span data-stu-id="498d1-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="498d1-109">C++</span><span class="sxs-lookup"><span data-stu-id="498d1-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="498d1-110">歡迎使用 toohello Azure Cosmos DB 開始使用.NET Core 教學課程的 DocumentDB API ！</span><span class="sxs-lookup"><span data-stu-id="498d1-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="498d1-111">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="498d1-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="498d1-112">本文將討論：</span><span class="sxs-lookup"><span data-stu-id="498d1-112">We'll cover:</span></span>

* <span data-ttu-id="498d1-113">建立及連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="498d1-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="498d1-114">設定 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="498d1-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="498d1-115">建立線上資料庫</span><span class="sxs-lookup"><span data-stu-id="498d1-115">Creating an online database</span></span>
* <span data-ttu-id="498d1-116">建立集合</span><span class="sxs-lookup"><span data-stu-id="498d1-116">Creating a collection</span></span>
* <span data-ttu-id="498d1-117">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="498d1-117">Creating JSON documents</span></span>
* <span data-ttu-id="498d1-118">查詢 hello 集合</span><span class="sxs-lookup"><span data-stu-id="498d1-118">Querying hello collection</span></span>
* <span data-ttu-id="498d1-119">取代文件</span><span class="sxs-lookup"><span data-stu-id="498d1-119">Replacing a document</span></span>
* <span data-ttu-id="498d1-120">刪除文件</span><span class="sxs-lookup"><span data-stu-id="498d1-120">Deleting a document</span></span>
* <span data-ttu-id="498d1-121">刪除 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="498d1-121">Deleting hello database</span></span>

<span data-ttu-id="498d1-122">沒有時間嗎？</span><span class="sxs-lookup"><span data-stu-id="498d1-122">Don't have time?</span></span> <span data-ttu-id="498d1-123">別擔心！</span><span class="sxs-lookup"><span data-stu-id="498d1-123">Don't worry!</span></span> <span data-ttu-id="498d1-124">hello 完整解決方案位於[GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="498d1-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="498d1-125">跳 toohello[取得 hello 完整的解決方案 > 一節](#GetSolution)快速的指示。</span><span class="sxs-lookup"><span data-stu-id="498d1-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="498d1-126">Xamarin iOS、 Android 或表單想 toobuild DocumentDB API 和.NET Core SDK 的應用程式使用 hello？</span><span class="sxs-lookup"><span data-stu-id="498d1-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="498d1-127">請參閱[使用 Xamarin 和 Azure Cosmos DB 建置行動應用程式](mobile-apps-with-xamarin.md)。</span><span class="sxs-lookup"><span data-stu-id="498d1-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="498d1-128">hello Azure Cosmos DB.NET Core SDK 在本教學課程中使用尚未與通用 Windows 平台 (UWP) 應用程式相容。</span><span class="sxs-lookup"><span data-stu-id="498d1-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="498d1-129">如需 hello 支援 UWP 應用程式的.NET Core SDK 預覽版本，傳送電子郵件太[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="498d1-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="498d1-130">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="498d1-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="498d1-131">必要條件</span><span class="sxs-lookup"><span data-stu-id="498d1-131">Prerequisites</span></span>
<span data-ttu-id="498d1-132">請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="498d1-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="498d1-133">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="498d1-133">An active Azure account.</span></span> <span data-ttu-id="498d1-134">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="498d1-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="498d1-135">或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程。</span><span class="sxs-lookup"><span data-stu-id="498d1-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="498d1-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="498d1-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="498d1-137">如果您使用在 MacOS 或 Lunix 上，您可以藉由安裝 hello 開發.NET Core 應用程式，從命令列 hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) hello 平台，您所選擇。</span><span class="sxs-lookup"><span data-stu-id="498d1-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="498d1-138">如果您使用 Windows 上，您可以藉由安裝 hello 開發.NET Core 應用程式，從命令列 hello [.NET Core SDK](https://www.microsoft.com/net/core#windows)。</span><span class="sxs-lookup"><span data-stu-id="498d1-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="498d1-139">您可以使用自己的編輯器，也可以下載適用於 Windows、Linux 和 MacOS 的免費 [Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="498d1-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="498d1-140">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="498d1-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="498d1-141">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="498d1-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="498d1-142">如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[安裝 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="498d1-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="498d1-143">如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[安裝 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="498d1-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="498d1-144"><a id="SetupVS"></a>步驟 2：設定您的 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="498d1-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="498d1-145">在電腦上開啟 **Visual Studio 2017**。</span><span class="sxs-lookup"><span data-stu-id="498d1-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="498d1-146">在 hello**檔案**功能表上，選取**新增**，然後選擇 **專案**。</span><span class="sxs-lookup"><span data-stu-id="498d1-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="498d1-147">在 hello**新專案**對話方塊中，選取**範本** / **Visual C#** / **.NET Core** /**主控台應用程式 (.NET Core)**，命名您的專案**DocumentDBGettingStarted**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="498d1-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Hello 新增專案 視窗的螢幕擷取畫面](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="498d1-149">在 [hello**方案總管] 中**，以滑鼠右鍵按一下**DocumentDBGettingStarted**。</span><span class="sxs-lookup"><span data-stu-id="498d1-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="498d1-150">而不需離開 hello 功能表，然後按一下 **管理 NuGet 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="498d1-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![螢幕擷取畫面的權限 hello hello 專案的已按下功能表](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="498d1-152">在 hello **NuGet**索引標籤上，按一下 **瀏覽**頂端的 hello 視窗，然後輸入 hello **azure documentdb** hello 搜尋 方塊中。</span><span class="sxs-lookup"><span data-stu-id="498d1-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="498d1-153">在 hello 結果中尋找**Microsoft.Azure.DocumentDB.Core**按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="498d1-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="498d1-154">hello 封裝識別碼 hello DocumentDB.NET Core 的用戶端程式庫是[Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)。</span><span class="sxs-lookup"><span data-stu-id="498d1-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="498d1-155">如果您是以此 .NET Core NuGet 套件不支援的 .NET Framework 版本 (例如 net461) 為目標，則使用 [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)，其支援 .NET Framework 4.5 以後的所有 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="498d1-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="498d1-156">Hello 提示出現時，在接受 hello NuGet 封裝安裝與 hello 授權合約。</span><span class="sxs-lookup"><span data-stu-id="498d1-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="498d1-157">太棒了！</span><span class="sxs-lookup"><span data-stu-id="498d1-157">Great!</span></span> <span data-ttu-id="498d1-158">現在我們完成 hello 安裝程式，讓我們開始撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="498d1-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="498d1-159">您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)找到本教學課程的完整程式碼專案。</span><span class="sxs-lookup"><span data-stu-id="498d1-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="498d1-160"><a id="Connect"></a>步驟 3： 連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="498d1-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="498d1-161">首先，加入下列參考應用程式的 C#，hello Program.cs 檔案中的 toohello 開頭：</span><span class="sxs-lookup"><span data-stu-id="498d1-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

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
> <span data-ttu-id="498d1-162">在順序 toocomplete 本教學課程，請確認您新增上述 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="498d1-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="498d1-163">現在，在「public class Program」之下加入下列兩個常數和您的「client」變數。</span><span class="sxs-lookup"><span data-stu-id="498d1-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="498d1-164">接下來，前端 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的 URI 與主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="498d1-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="498d1-165">hello Azure Cosmos DB URI 及主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。</span><span class="sxs-lookup"><span data-stu-id="498d1-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="498d1-166">在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，然後按一下**金鑰**。</span><span class="sxs-lookup"><span data-stu-id="498d1-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="498d1-167">從 hello 入口網站複製 hello URI，並將它貼入`<your endpoint URI>`hello program.cs 檔案中。</span><span class="sxs-lookup"><span data-stu-id="498d1-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="498d1-168">複製 hello 從 hello 入口網站的主索引鍵，並將它貼入`<your key>`。</span><span class="sxs-lookup"><span data-stu-id="498d1-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="498d1-169">如果您使用 hello Azure Cosmos DB 模擬器，使用`https://localhost:8081`hello 端點，以及從 hello 妥善定義的授權金鑰[如何使用 toodevelop hello Azure Cosmos DB 模擬器](local-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="498d1-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="498d1-170">請確定 tooremove hello < 和 > 但保留 hello 雙引號括住您的端點和金鑰。</span><span class="sxs-lookup"><span data-stu-id="498d1-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Hello hello NoSQL 教學課程 toocreate C# 主控台應用程式所使用的 Azure 入口網站的螢幕擷取畫面。][keys]

<span data-ttu-id="498d1-173">讓我們先 hello 取得啟動應用程式所建立的新執行個體的 hello **DocumentClient**。</span><span class="sxs-lookup"><span data-stu-id="498d1-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="498d1-174">以下 hello **Main**方法中，新增此呼叫的非同步工作**GetStartedDemo**，它會具現化新**DocumentClient**。</span><span class="sxs-lookup"><span data-stu-id="498d1-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

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

<span data-ttu-id="498d1-175">新增 hello 下列程式碼 toorun 將您的非同步工作，從您**Main**方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="498d1-176">hello **Main**方法將會攔截例外狀況，並將它們寫入 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="498d1-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="498d1-177">按 hello **DocumentDBGettingStarted**按鈕 toobuild 並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="498d1-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="498d1-178">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-178">Congratulations!</span></span> <span data-ttu-id="498d1-179">您已成功連接 tooan Azure Cosmos DB 帳戶，現在讓我們看一下使用 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="498d1-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="498d1-180">步驟 4：建立資料庫</span><span class="sxs-lookup"><span data-stu-id="498d1-180">Step 4: Create a database</span></span>
<span data-ttu-id="498d1-181">您新增 hello 程式碼建立資料庫前，將撰寫 toohello 主控台的協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="498d1-182">複製並貼上 hello **WriteToConsoleAndPromptToContinue**下方 hello 方法**GetStartedDemo**方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="498d1-183">您的 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)可以建立使用 hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="498d1-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="498d1-184">資料庫是 hello 的 JSON 文件儲存分割於各個集合的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="498d1-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="498d1-185">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**底下建立 hello 用戶端的方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="498d1-186">這會建立名為 FamilyDB 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="498d1-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="498d1-187">按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="498d1-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="498d1-188">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-188">Congratulations!</span></span> <span data-ttu-id="498d1-189">您已成功建立 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="498d1-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="498d1-190"><a id="CreateColl"></a>步驟 5：建立集合</span><span class="sxs-lookup"><span data-stu-id="498d1-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="498d1-191">**CreateDocumentCollectionAsync** 會建立含有保留輸送量且具有價格含意的新集合。</span><span class="sxs-lookup"><span data-stu-id="498d1-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="498d1-192">如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="498d1-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="498d1-193">A[集合](documentdb-resources.md#collections)可以建立使用 hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="498d1-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="498d1-194">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="498d1-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="498d1-195">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 資料庫建立的方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="498d1-196">這會建立名為 FamilyCollection_oa 的文件集合。</span><span class="sxs-lookup"><span data-stu-id="498d1-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="498d1-197">按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="498d1-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="498d1-198">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-198">Congratulations!</span></span> <span data-ttu-id="498d1-199">您已成功建立 Azure Cosmos DB 文件集合。</span><span class="sxs-lookup"><span data-stu-id="498d1-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="498d1-200"><a id="CreateDoc"></a>步驟 6：建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="498d1-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="498d1-201">A[文件](documentdb-resources.md#documents)可以建立使用 hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx)方法 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="498d1-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="498d1-202">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="498d1-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="498d1-203">現在可插入一或多份文件。</span><span class="sxs-lookup"><span data-stu-id="498d1-203">We can now insert one or more documents.</span></span> <span data-ttu-id="498d1-204">如果您已經有您想要 toostore 資料庫中的資料，您可以使用 Azure Cosmos DB 的[資料移轉工具](import-data.md)。</span><span class="sxs-lookup"><span data-stu-id="498d1-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="498d1-205">首先，我們需要 toocreate**系列**表示儲存在 Azure Cosmos DB，在此範例中的物件類別。</span><span class="sxs-lookup"><span data-stu-id="498d1-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="498d1-206">我們也會建立 **Family** 內使用的 **Parent**、**Child**、**Pet**、**Address** 子類別。</span><span class="sxs-lookup"><span data-stu-id="498d1-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="498d1-207">請注意，文件必須將 **Id** 屬性序列化為 JSON 中的**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="498d1-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="498d1-208">加入 hello 之後 hello 遵循內部的子類別來建立這些類別**GetStartedDemo**方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="498d1-209">複製並貼上 hello**系列**，**父**，**子**，**寵物**，和**位址**類別下方hello **WriteToConsoleAndPromptToContinue**方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="498d1-210">複製並貼上 hello **CreateFamilyDocumentIfNotExists**下方方法您**CreateDocumentCollectionIfNotExists**方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

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

<span data-ttu-id="498d1-211">然後插入兩個文件，分別指派給 hello Andersen 系列 hello Wakefield 系列。</span><span class="sxs-lookup"><span data-stu-id="498d1-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="498d1-212">複製並貼上 hello 程式碼所示`// ADD THIS PART tooYOUR CODE`tooyour **GetStartedDemo**底下建立 hello 文件集合的方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

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

<span data-ttu-id="498d1-213">按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="498d1-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="498d1-214">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-214">Congratulations!</span></span> <span data-ttu-id="498d1-215">您已成功建立兩個 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="498d1-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![以圖表顯示的 hello 階層式關聯性，hello 帳戶、 hello 線上資料庫、 hello 集合和 hello hello NoSQL 教學課程 toocreate C# 主控台應用程式所使用的文件之間](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="498d1-217"><a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="498d1-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="498d1-218">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="498d1-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="498d1-219">hello 下列程式碼範例示範各種查詢-使用這兩個 Azure Cosmos DB SQL 語法，以及 LINQ-我們能夠針對執行 hello 我們插入 hello 上一個步驟中的文件。</span><span class="sxs-lookup"><span data-stu-id="498d1-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="498d1-220">複製並貼上 hello **ExecuteSimpleQuery**下方方法您**CreateFamilyDocumentIfNotExists**方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="498d1-221">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 建立第二個文件的方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="498d1-222">按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="498d1-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="498d1-223">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-223">Congratulations!</span></span> <span data-ttu-id="498d1-224">您已成功查詢 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="498d1-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="498d1-225">hello 下列圖表說明 hello Azure Cosmos DB SQL 查詢語法稱為 hello 集合針對您建立的方式，與 hello 相同邏輯適用於 toohello LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="498d1-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![圖表說明 hello 範圍和 hello 查詢的意義由 hello NoSQL 教學課程 toocreate C# 主控台應用程式](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="498d1-227">hello [FROM](documentdb-sql-query.md#FromClause)關鍵字是選擇性的 hello 查詢，因為 Azure Cosmos DB 查詢已設定領域的 tooa 單一集合。</span><span class="sxs-lookup"><span data-stu-id="498d1-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="498d1-228">因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。</span><span class="sxs-lookup"><span data-stu-id="498d1-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="498d1-229">DocumentDB 會推斷家族、 根或 hello 變數名稱您已選擇，依預設參考 hello 目前集合。</span><span class="sxs-lookup"><span data-stu-id="498d1-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="498d1-230"><a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="498d1-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="498d1-231">Azure Cosmos DB 支援取代 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="498d1-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="498d1-232">複製並貼上 hello **ReplaceFamilyDocument**下方方法您**ExecuteSimpleQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

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

<span data-ttu-id="498d1-233">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 查詢執行的方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="498d1-234">這樣將會取代 hello 文件之後, 執行 hello 相同再次查詢 tooview hello 變更文件。</span><span class="sxs-lookup"><span data-stu-id="498d1-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="498d1-235">按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="498d1-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="498d1-236">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-236">Congratulations!</span></span> <span data-ttu-id="498d1-237">您已成功取代 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="498d1-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="498d1-238"><a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="498d1-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="498d1-239">Azure Cosmos DB 支援刪除 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="498d1-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="498d1-240">複製並貼上 hello **DeleteFamilyDocument**下方方法您**ReplaceFamilyDocument**方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

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

<span data-ttu-id="498d1-241">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 第二個查詢執行的方法。</span><span class="sxs-lookup"><span data-stu-id="498d1-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="498d1-242">按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="498d1-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="498d1-243">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-243">Congratulations!</span></span> <span data-ttu-id="498d1-244">您已成功刪除 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="498d1-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="498d1-245"><a id="DeleteDatabase"></a>步驟 10： 刪除 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="498d1-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="498d1-246">正在刪除 hello 已建立的資料庫將會移除 hello 資料庫和所有子系資源 （集合、 文件）。</span><span class="sxs-lookup"><span data-stu-id="498d1-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="498d1-247">複製和貼上 hello 下列程式碼 tooyour **GetStartedDemo**下方 hello 文件的方法刪除 toodelete hello 整個資料庫和所有子系的資源。</span><span class="sxs-lookup"><span data-stu-id="498d1-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="498d1-248">按 hello **DocumentDBGettingStarted**按鈕 toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="498d1-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="498d1-249">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-249">Congratulations!</span></span> <span data-ttu-id="498d1-250">您已成功刪除 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="498d1-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="498d1-251"><a id="Run"></a>步驟 11：一起執行您的 C# 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="498d1-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="498d1-252">按 hello **DocumentDBGettingStarted** Visual Studio 中偵錯模式 toobuild hello 應用程式中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="498d1-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="498d1-253">您應該會看到 hello 輸出 hello 主控台視窗中啟動應用程式取得。</span><span class="sxs-lookup"><span data-stu-id="498d1-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="498d1-254">hello 輸出會顯示 hello hello 結果我們加入，而且必須符合以下的 hello 範例文字的查詢。</span><span class="sxs-lookup"><span data-stu-id="498d1-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

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

<span data-ttu-id="498d1-255">恭喜！</span><span class="sxs-lookup"><span data-stu-id="498d1-255">Congratulations!</span></span> <span data-ttu-id="498d1-256">您已經完成 hello 教學課程，有一個使用 C# 主控台應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="498d1-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="498d1-257"><a id="GetSolution"></a>取得 hello 完整的教學課程解決方案</span><span class="sxs-lookup"><span data-stu-id="498d1-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="498d1-258">包含所有在本文中的 hello 範例 toobuild hello GetStarted 方案，您將需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="498d1-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="498d1-259">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="498d1-259">An active Azure account.</span></span> <span data-ttu-id="498d1-260">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="498d1-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="498d1-261">[Azure Cosmos DB 帳戶][create-documentdb-dotnet.md#create-account]。</span><span class="sxs-lookup"><span data-stu-id="498d1-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="498d1-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) GitHub 上有可用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="498d1-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="498d1-263">toorestore hello 參考 toohello DocumentDB API 針對 Azure Cosmos DB.NET Core SDK 在 Visual Studio 中，以滑鼠右鍵按一下 hello **GetStarted**方案在方案總管 中，然後按一下**啟用 NuGet 封裝還原**.</span><span class="sxs-lookup"><span data-stu-id="498d1-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="498d1-264">接下來，在 hello Program.cs 檔案中，更新 hello 的端點 Url 和 AuthorizationKey 值中所述[tooan Azure Cosmos DB 帳戶連接](#Connect)。</span><span class="sxs-lookup"><span data-stu-id="498d1-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="498d1-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="498d1-265">Next steps</span></span>
* <span data-ttu-id="498d1-266">需要更複雜的 ASP.NET MVC 教學課程嗎？</span><span class="sxs-lookup"><span data-stu-id="498d1-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="498d1-267">請參閱 [ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-dotnet-application.md)。</span><span class="sxs-lookup"><span data-stu-id="498d1-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="498d1-268">想 toodevelop Xamarin iOS、 Android 或表單應用程式使用 Azure Cosmos DB.NET Core sdk hello DocumentDB API 嗎？</span><span class="sxs-lookup"><span data-stu-id="498d1-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="498d1-269">請參閱[使用 Xamarin 和 Azure Cosmos DB 建置行動應用程式](mobile-apps-with-xamarin.md)。</span><span class="sxs-lookup"><span data-stu-id="498d1-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="498d1-270">想 tooperform 規模和效能測試以 Azure Cosmos DB 嗎？</span><span class="sxs-lookup"><span data-stu-id="498d1-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="498d1-271">請參閱 [Azure Cosmos DB 的效能和級別測試](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="498d1-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="498d1-272">了解如何太[監視 Azure Cosmos DB 要求、 使用方式，以及儲存體](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="498d1-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="498d1-273">執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。</span><span class="sxs-lookup"><span data-stu-id="498d1-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="498d1-274">toolearn 進一步了解 hello 的程式設計模型，請參閱[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="498d1-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
