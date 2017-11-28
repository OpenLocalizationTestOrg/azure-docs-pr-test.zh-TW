---
title: "Azure Cosmos DB：開始使用 DocumentDB API .NET Core 教學課程 | Microsoft Docs"
description: "本教學課程將使用 Azure Cosmos DB DocumentDB API .NET Core SDK，建立線上資料庫以及 C# 主控台應用程式。"
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
ms.openlocfilehash: 7536978bbb1e41b6484b66fd1b51c900fc3e545d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-documentdb-api-and-net-core"></a><span data-ttu-id="c593c-103">Azure Cosmos DB︰開始使用 DocumentDB API 與 .NET Core</span><span class="sxs-lookup"><span data-stu-id="c593c-103">Azure Cosmos DB: Getting started with the DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c593c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c593c-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="c593c-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c593c-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="c593c-106">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="c593c-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="c593c-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="c593c-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="c593c-108">Java</span><span class="sxs-lookup"><span data-stu-id="c593c-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="c593c-109">C++</span><span class="sxs-lookup"><span data-stu-id="c593c-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="c593c-110">歡迎使用 .NET Core 入門之適用於 Azure Cosmos DB 的 DocumentDB API 教學課程！</span><span class="sxs-lookup"><span data-stu-id="c593c-110">Welcome to the DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="c593c-111">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="c593c-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="c593c-112">本文將討論：</span><span class="sxs-lookup"><span data-stu-id="c593c-112">We'll cover:</span></span>

* <span data-ttu-id="c593c-113">建立及連線至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="c593c-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="c593c-114">設定 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="c593c-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="c593c-115">建立線上資料庫</span><span class="sxs-lookup"><span data-stu-id="c593c-115">Creating an online database</span></span>
* <span data-ttu-id="c593c-116">建立集合</span><span class="sxs-lookup"><span data-stu-id="c593c-116">Creating a collection</span></span>
* <span data-ttu-id="c593c-117">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="c593c-117">Creating JSON documents</span></span>
* <span data-ttu-id="c593c-118">查詢集合</span><span class="sxs-lookup"><span data-stu-id="c593c-118">Querying the collection</span></span>
* <span data-ttu-id="c593c-119">取代文件</span><span class="sxs-lookup"><span data-stu-id="c593c-119">Replacing a document</span></span>
* <span data-ttu-id="c593c-120">刪除文件</span><span class="sxs-lookup"><span data-stu-id="c593c-120">Deleting a document</span></span>
* <span data-ttu-id="c593c-121">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="c593c-121">Deleting the database</span></span>

<span data-ttu-id="c593c-122">沒有時間嗎？</span><span class="sxs-lookup"><span data-stu-id="c593c-122">Don't have time?</span></span> <span data-ttu-id="c593c-123">別擔心！</span><span class="sxs-lookup"><span data-stu-id="c593c-123">Don't worry!</span></span> <span data-ttu-id="c593c-124">您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)上找到完整的方案。</span><span class="sxs-lookup"><span data-stu-id="c593c-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="c593c-125">請跳至 [取得完整的解決方案](#GetSolution) 一節，以取得簡要指示。</span><span class="sxs-lookup"><span data-stu-id="c593c-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="c593c-126">想要使用 DocumentDB API 和 .NET Core SDK 建置 Xamarin iOS、Android 或 Forms 應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="c593c-126">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="c593c-127">請參閱[使用 Xamarin 和 Azure Cosmos DB 建置行動應用程式](mobile-apps-with-xamarin.md)。</span><span class="sxs-lookup"><span data-stu-id="c593c-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c593c-128">本教學課程中使用的 Azure Cosmos DB .NET Core SDK 尚未與通用 Windows 平台 (UWP) 應用程式相容。</span><span class="sxs-lookup"><span data-stu-id="c593c-128">The Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="c593c-129">如需可支援 UWP 應用程式的 .NET Core SDK 預覽版本，請傳送電子郵件至 [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="c593c-129">For a preview version of the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="c593c-130">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="c593c-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c593c-131">必要條件</span><span class="sxs-lookup"><span data-stu-id="c593c-131">Prerequisites</span></span>
<span data-ttu-id="c593c-132">請確定您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="c593c-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="c593c-133">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c593c-133">An active Azure account.</span></span> <span data-ttu-id="c593c-134">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="c593c-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="c593c-135">或者，您可以使用 [Azure Cosmos DB 模擬器](local-emulator.md)來進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="c593c-135">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="c593c-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c593c-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="c593c-137">如果您正在操作 MacOS 或 Linux，可以針對選定平台安裝 [.NET Core SDK](https://www.microsoft.com/net/core#macos)，以從命令列開發 .NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-137">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="c593c-138">如果您正在操作 Windows，可以安裝 [.NET Core SDK](https://www.microsoft.com/net/core#windows) 以從命令列開發 .NET Core 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-138">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="c593c-139">您可以使用自己的編輯器，也可以下載適用於 Windows、Linux 和 MacOS 的免費 [Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="c593c-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="c593c-140">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="c593c-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="c593c-141">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c593c-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="c593c-142">如果您已經擁有想要使用的帳戶，就可以跳到 [設定您的 Visual Studio 方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="c593c-142">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="c593c-143">如果您是使用「Azure Cosmos DB 模擬器」，請依照 [Azure Cosmos DB 模擬器](local-emulator.md)的步驟來設定模擬器，然後直接跳到[設定您的 Visual Studio 解決方案](#SetupVS)。</span><span class="sxs-lookup"><span data-stu-id="c593c-143">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="c593c-144"><a id="SetupVS"></a>步驟 2：設定您的 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="c593c-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="c593c-145">在電腦上開啟 **Visual Studio 2017**。</span><span class="sxs-lookup"><span data-stu-id="c593c-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="c593c-146">從 [檔案] 功能表中，選取 [新增]，然後選擇 [專案]。</span><span class="sxs-lookup"><span data-stu-id="c593c-146">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="c593c-147">在 [新增專案] 對話方塊中，依序選取 [範本] / [Visual C#] / [.NET Core]/[主控台應用程式 (.NET Core)]、將專案命名為 **DocumentDBGettingStarted**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c593c-147">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![[新增專案] 視窗的螢幕擷取畫面](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="c593c-149">在 [方案總管] 中，以滑鼠右鍵按一下 [DocumentDBGettingStarted]。</span><span class="sxs-lookup"><span data-stu-id="c593c-149">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="c593c-150">然後在無需離開功能表的情況下，按一下 [管理 NuGet 套件...]。</span><span class="sxs-lookup"><span data-stu-id="c593c-150">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![專案的滑鼠右鍵功能表的螢幕擷取畫面](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="c593c-152">在 [NuGet] 索引標籤中按一下視窗頂端的 [瀏覽]，然後在搜尋方塊中輸入 **azure documentdb**。</span><span class="sxs-lookup"><span data-stu-id="c593c-152">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="c593c-153">在結果中尋找 [Microsoft.Azure.DocumentDB.Core]，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="c593c-153">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="c593c-154">適用於 .NET Core 之 DocumentDB 用戶端程式庫的套件識別碼為 [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)。</span><span class="sxs-lookup"><span data-stu-id="c593c-154">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="c593c-155">如果您是以此 .NET Core NuGet 套件不支援的 .NET Framework 版本 (例如 net461) 為目標，則使用 [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)，其支援 .NET Framework 4.5 以後的所有 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="c593c-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="c593c-156">在提示字元中，接受 NuGet 套件安裝和授權合約。</span><span class="sxs-lookup"><span data-stu-id="c593c-156">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="c593c-157">太棒了！</span><span class="sxs-lookup"><span data-stu-id="c593c-157">Great!</span></span> <span data-ttu-id="c593c-158">現在已完成安裝程式，讓我們開始撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="c593c-158">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="c593c-159">您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)找到本教學課程的完整程式碼專案。</span><span class="sxs-lookup"><span data-stu-id="c593c-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="c593c-160"><a id="Connect"></a>步驟 3：連接至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="c593c-160"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="c593c-161">首先，在 Program.cs 檔案中，將這些參考新增到 C# 應用程式的開頭：</span><span class="sxs-lookup"><span data-stu-id="c593c-161">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="c593c-162">若要完成此教學課程，請務必新增上述的相依性。</span><span class="sxs-lookup"><span data-stu-id="c593c-162">In order to complete this tutorial, make sure you add the dependencies above.</span></span>

<span data-ttu-id="c593c-163">現在，在「public class Program」之下加入下列兩個常數和您的「client」變數。</span><span class="sxs-lookup"><span data-stu-id="c593c-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="c593c-164">接下來，前往 [Azure 入口網站](https://portal.azure.com) 擷取您的 URI 和主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="c593c-164">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="c593c-165">您必須提供 Azure Cosmos DB URI 和主要金鑰，您的應用程式才能了解要連接的位置，而 Azure Cosmos DB 才會信任您的應用程式連接。</span><span class="sxs-lookup"><span data-stu-id="c593c-165">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="c593c-166">在 Azure 入口網站中，瀏覽至 Azure Cosmos DB 帳戶，然後按一下 [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="c593c-166">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="c593c-167">從入口網站複製 URI，並將它貼到 program.cs 檔案的 `<your endpoint URI>` 中。</span><span class="sxs-lookup"><span data-stu-id="c593c-167">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="c593c-168">然後從入口網站複製主要金鑰，並將它貼到 `<your key>`中。</span><span class="sxs-lookup"><span data-stu-id="c593c-168">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="c593c-169">如果您是使用 Azure Cosmos DB 模擬器，請將 `https://localhost:8081` 作為端點，並使用[如何使用 Azure Cosmos DB 模擬器開發](local-emulator.md)中的定義完善授權金鑰。</span><span class="sxs-lookup"><span data-stu-id="c593c-169">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="c593c-170">請務必移除 < 和 > 但保留端點和金鑰的雙引號。</span><span class="sxs-lookup"><span data-stu-id="c593c-170">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![NoSQL 教學課程用來建立 C# 主控台應用程式之 Azure 入口網站的螢幕擷取畫面。][keys]

<span data-ttu-id="c593c-173">讓我們建立 **DocumentClient**的新執行個體，啟動快速入門應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-173">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="c593c-174">在 **Main** 方法底下，加入 **GetStartedDemo** 這個新的非同步工作，以將新的 **DocumentClient** 具現化。</span><span class="sxs-lookup"><span data-stu-id="c593c-174">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="c593c-175">加入下列程式碼，以從 **Main** 方法執行非同步工作。</span><span class="sxs-lookup"><span data-stu-id="c593c-175">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="c593c-176">**Main** 方法會攔截例外狀況並將它們寫入主控台。</span><span class="sxs-lookup"><span data-stu-id="c593c-176">The **Main** method will catch exceptions and write them to the console.</span></span>

```csharp
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
```

<span data-ttu-id="c593c-177">按下 [DocumentDBGettingStarted] 按鈕以建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-177">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="c593c-178">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-178">Congratulations!</span></span> <span data-ttu-id="c593c-179">您已成功連接至 Azure Cosmos DB 帳戶，現在讓我們看看如何使用 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="c593c-179">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="c593c-180">步驟 4：建立資料庫</span><span class="sxs-lookup"><span data-stu-id="c593c-180">Step 4: Create a database</span></span>
<span data-ttu-id="c593c-181">在您新增用於建立資料庫的程式碼之前，請新增用於寫入主控台的協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="c593c-181">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="c593c-182">複製 **WriteToConsoleAndPromptToContinue** 方法並貼到 **GetStartedDemo** 方法之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-182">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="c593c-183">您可以使用 **DocumentClient** 類別的 [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) 方法來建立 Azure Cosmos DB [資料庫](documentdb-resources.md#databases)。</span><span class="sxs-lookup"><span data-stu-id="c593c-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="c593c-184">資料庫是分割給多個集合之 JSON 文件儲存體的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="c593c-184">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="c593c-185">複製下列程式碼並貼到 **GetStartedDemo** 方法的用戶端建立之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-185">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="c593c-186">這會建立名為 FamilyDB 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c593c-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="c593c-187">按下 [DocumentDBGettingStarted] 按鈕以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-187">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="c593c-188">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-188">Congratulations!</span></span> <span data-ttu-id="c593c-189">您已成功建立 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c593c-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="c593c-190"><a id="CreateColl"></a>步驟 5：建立集合</span><span class="sxs-lookup"><span data-stu-id="c593c-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="c593c-191">**CreateDocumentCollectionAsync** 會建立含有保留輸送量且具有價格含意的新集合。</span><span class="sxs-lookup"><span data-stu-id="c593c-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="c593c-192">如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="c593c-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="c593c-193">您可以使用 **DocumentClient** 類別的 [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) 方法建立[集合](documentdb-resources.md#collections)。</span><span class="sxs-lookup"><span data-stu-id="c593c-193">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="c593c-194">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="c593c-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="c593c-195">複製下列程式碼並貼到 **GetStartedDemo** 方法的資料庫建立之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-195">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="c593c-196">這會建立名為 FamilyCollection_oa 的文件集合。</span><span class="sxs-lookup"><span data-stu-id="c593c-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="c593c-197">按下 [DocumentDBGettingStarted] 按鈕以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-197">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="c593c-198">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-198">Congratulations!</span></span> <span data-ttu-id="c593c-199">您已成功建立 Azure Cosmos DB 文件集合。</span><span class="sxs-lookup"><span data-stu-id="c593c-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="c593c-200"><a id="CreateDoc"></a>步驟 6：建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="c593c-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="c593c-201">您可以使用 **DocumentClient** 類別的 [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) 方法來建立[文件](documentdb-resources.md#documents)。</span><span class="sxs-lookup"><span data-stu-id="c593c-201">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="c593c-202">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="c593c-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="c593c-203">現在可插入一或多份文件。</span><span class="sxs-lookup"><span data-stu-id="c593c-203">We can now insert one or more documents.</span></span> <span data-ttu-id="c593c-204">如果您已經有想要儲存於資料庫中的資料，就可以使用 Azure Cosmos DB 的 [資料移轉工具](import-data.md)。</span><span class="sxs-lookup"><span data-stu-id="c593c-204">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="c593c-205">首先，我們需要建立 **Family** 類別，以代表此範例中儲存在 Azure Cosmos DB 內的物件。</span><span class="sxs-lookup"><span data-stu-id="c593c-205">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="c593c-206">我們也會建立 **Family** 內使用的 **Parent**、**Child**、**Pet**、**Address** 子類別。</span><span class="sxs-lookup"><span data-stu-id="c593c-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="c593c-207">請注意，文件必須將 **Id** 屬性序列化為 JSON 中的**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="c593c-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="c593c-208">藉由在 **GetStartedDemo** 方法之後加入下列內部子類別來建立這些類別。</span><span class="sxs-lookup"><span data-stu-id="c593c-208">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="c593c-209">複製 **Family**、**Parent**、**Child**、**Pet** 和 **Address** 類別並貼到 **WriteToConsoleAndPromptToContinue** 方法之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-209">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="c593c-210">複製 **CreateFamilyDocumentIfNotExists** 方法並貼到 **CreateDocumentCollectionIfNotExists** 方法之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-210">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="c593c-211">插入兩個文件，一個給 Andersen 家族，另一個給 Wakefield 家族。</span><span class="sxs-lookup"><span data-stu-id="c593c-211">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="c593c-212">複製 `// ADD THIS PART TO YOUR CODE` 後面的程式碼並貼到 **GetStartedDemo** 方法的文件集合建立之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-212">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

<span data-ttu-id="c593c-213">按下 [DocumentDBGettingStarted] 按鈕以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-213">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="c593c-214">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-214">Congratulations!</span></span> <span data-ttu-id="c593c-215">您已成功建立兩個 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="c593c-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![說明 NoSQL 教學課程用來建立 C# 主控台應用程式之帳戶、線上資料庫、集合和文件之間階層式關聯性的圖表](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="c593c-217"><a id="Query"></a>步驟 7︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="c593c-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="c593c-218">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行豐富[查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="c593c-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="c593c-219">下列範例程式碼示範各種查詢，同時使用可在我們於前一個步驟中所插入文件上執行的 Azure Cosmos DB SQL 語法和 LINQ。</span><span class="sxs-lookup"><span data-stu-id="c593c-219">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="c593c-220">複製 **ExecuteSimpleQuery** 方法並貼到 **CreateFamilyDocumentIfNotExists** 方法之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-220">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="c593c-221">複製下列程式碼並貼到 **GetStartedDemo** 方法的次要文件建立之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-221">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="c593c-222">按下 [DocumentDBGettingStarted] 按鈕以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-222">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="c593c-223">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-223">Congratulations!</span></span> <span data-ttu-id="c593c-224">您已成功查詢 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="c593c-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="c593c-225">下圖說明如何針對您所建立的集合呼叫 Azure Cosmos DB SQL 查詢語法，相同邏輯也可以套用至 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="c593c-225">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![說明 NoSQL 教學課程用來建立 C# 主控台應用程式之查詢的範圍和意義的圖表](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="c593c-227">因為 Azure Cosmos DB 查詢已侷限於單一集合，所以查詢中的 [FROM](documentdb-sql-query.md#FromClause) 關鍵字是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="c593c-227">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="c593c-228">因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。</span><span class="sxs-lookup"><span data-stu-id="c593c-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="c593c-229">依預設，DocumentDB 會推斷該系列、根或您選擇的變數名稱來參考目前的集合。</span><span class="sxs-lookup"><span data-stu-id="c593c-229">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="c593c-230"><a id="ReplaceDocument"></a>步驟 8︰取代 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="c593c-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="c593c-231">Azure Cosmos DB 支援取代 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="c593c-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="c593c-232">複製 **ReplaceFamilyDocument** 方法並貼到 **ExecuteSimpleQuery** 方法之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-232">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="c593c-233">複製下列程式碼並貼到 **GetStartedDemo** 方法的查詢執行之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-233">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="c593c-234">取代文件後，此程式碼會再次執行相同的查詢以檢視變更後的文件。</span><span class="sxs-lookup"><span data-stu-id="c593c-234">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="c593c-235">按下 [DocumentDBGettingStarted] 按鈕以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-235">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="c593c-236">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-236">Congratulations!</span></span> <span data-ttu-id="c593c-237">您已成功取代 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="c593c-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="c593c-238"><a id="DeleteDocument"></a>步驟 9︰刪除 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="c593c-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="c593c-239">Azure Cosmos DB 支援刪除 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="c593c-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="c593c-240">複製 **DeleteFamilyDocument** 方法並貼到 **ReplaceFamilyDocument** 方法之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-240">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="c593c-241">複製下列程式碼並貼到 **GetStartedDemo** 方法的次要查詢執行之下。</span><span class="sxs-lookup"><span data-stu-id="c593c-241">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="c593c-242">按下 [DocumentDBGettingStarted] 按鈕以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-242">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="c593c-243">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-243">Congratulations!</span></span> <span data-ttu-id="c593c-244">您已成功刪除 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="c593c-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="c593c-245"><a id="DeleteDatabase"></a>步驟 10：刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="c593c-245"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="c593c-246">刪除已建立的資料庫將會移除資料庫和所有子系資源 (集合、文件等)。</span><span class="sxs-lookup"><span data-stu-id="c593c-246">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="c593c-247">複製下列程式碼並貼到 **GetStartedDemo** 方法的文件刪除之下，以刪除整個資料庫和所有子系資源。</span><span class="sxs-lookup"><span data-stu-id="c593c-247">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="c593c-248">按下 [DocumentDBGettingStarted] 按鈕以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-248">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="c593c-249">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-249">Congratulations!</span></span> <span data-ttu-id="c593c-250">您已成功刪除 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c593c-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="c593c-251"><a id="Run"></a>步驟 11：一起執行您的 C# 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="c593c-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="c593c-252">在 Visual Studio 中按下 [DocumentDBGettingStarted] 按鈕以在偵錯模式中建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="c593c-252">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="c593c-253">您應該可以看到在主控台視窗中開始使用應用程式的輸出。</span><span class="sxs-lookup"><span data-stu-id="c593c-253">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="c593c-254">輸出將會顯示新增的查詢結果，而且應該符合以下的範例文字。</span><span class="sxs-lookup"><span data-stu-id="c593c-254">The output will show the results of the queries we added and should match the example text below.</span></span>

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="c593c-255">恭喜！</span><span class="sxs-lookup"><span data-stu-id="c593c-255">Congratulations!</span></span> <span data-ttu-id="c593c-256">您已經完成本教學課程，並擁有運作中的 C# 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="c593c-256">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="c593c-257"><a id="GetSolution"></a>取得完整的教學課程解決方案</span><span class="sxs-lookup"><span data-stu-id="c593c-257"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="c593c-258">若要建置包含本文中所有範例的 GetStarted 方案，您將需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="c593c-258">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="c593c-259">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c593c-259">An active Azure account.</span></span> <span data-ttu-id="c593c-260">如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="c593c-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="c593c-261">[Azure Cosmos DB 帳戶][create-documentdb-dotnet.md#create-account]。</span><span class="sxs-lookup"><span data-stu-id="c593c-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="c593c-262">您可以在 GitHub 上找到 [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) 方案。</span><span class="sxs-lookup"><span data-stu-id="c593c-262">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="c593c-263">若要在 Visual Studio 中還原適用於 Azure Cosmos DB .NET Core SDK 之 DocumentDB API 的參考，請在 [方案總管] 的 **GetStarted** 方案上按一下滑鼠右鍵，然後按一下 [啟用 NuGet 套件還原]。</span><span class="sxs-lookup"><span data-stu-id="c593c-263">To restore the references to the DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="c593c-264">接下來，在 Program.cs 檔案中更新 EndpointUrl 和 AuthorizationKey 值，如[連線至 Azure Cosmos DB 帳戶](#Connect)中所述。</span><span class="sxs-lookup"><span data-stu-id="c593c-264">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c593c-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c593c-265">Next steps</span></span>
* <span data-ttu-id="c593c-266">需要更複雜的 ASP.NET MVC 教學課程嗎？</span><span class="sxs-lookup"><span data-stu-id="c593c-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="c593c-267">請參閱 [ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發](documentdb-dotnet-application.md)。</span><span class="sxs-lookup"><span data-stu-id="c593c-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="c593c-268">想要使用適用於 Azure Cosmos DB .NET Core SDK 的 DocumentDB API 開發 Xamarin iOS、Android 或 Forms 應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="c593c-268">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="c593c-269">請參閱[使用 Xamarin 和 Azure Cosmos DB 建置行動應用程式](mobile-apps-with-xamarin.md)。</span><span class="sxs-lookup"><span data-stu-id="c593c-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="c593c-270">需要使用 Azure Cosmos DB 來執行規模和效能測試嗎？</span><span class="sxs-lookup"><span data-stu-id="c593c-270">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="c593c-271">請參閱 [Azure Cosmos DB 的效能和級別測試](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="c593c-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="c593c-272">了解如何[監視 Azure Cosmos DB 要求、使用量及儲存體](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="c593c-272">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="c593c-273">在 [Query Playground](https://www.documentdb.com/sql/demo)中，針對範例資料集執行查詢。</span><span class="sxs-lookup"><span data-stu-id="c593c-273">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="c593c-274">若要深入了解有關程式設計模型的詳細資訊，請參閱 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="c593c-274">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
