---
title: "Azure Cosmos DB 的 ASP.NET MVC 教學課程：Web 應用程式開發 | Microsoft Docs"
description: "使用 Azure Cosmos DB 建立 MVC Web 應用程式的 ASP.NET MVC 教學課程。 您將在託管於 Azure 網站的待辦事項應用程式儲存 JSON 和存取資料 - ASP NET MVC 教學課程逐步解說。"
keywords: "asp.net mvc 教學課程, web 應用程式開發, mvc web 應用程式, asp net mvc 教學課程逐步解說"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="14cc6-105"><a name="_Toc395809351"></a>ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發</span><span class="sxs-lookup"><span data-stu-id="14cc6-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14cc6-106">.NET</span><span class="sxs-lookup"><span data-stu-id="14cc6-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="14cc6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="14cc6-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="14cc6-108">Java</span><span class="sxs-lookup"><span data-stu-id="14cc6-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="14cc6-109">Python</span><span class="sxs-lookup"><span data-stu-id="14cc6-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="14cc6-110">為了特別說明您可以如何有效率地利用 Azure Cosmos DB 來儲存和查詢 JSON 文件，本文提供如何使用 Azure Cosmos DB 建置待辦事項應用程式的完整逐步解說。</span><span class="sxs-lookup"><span data-stu-id="14cc6-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="14cc6-111">在 Azure Cosmos DB 中，這些工作將會儲存為 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="14cc6-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![本教學課程所建立的待辦事項清單 Web 應用程式的螢幕擷取畫面 - ASP NET MVC 教學課程逐步解說](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="14cc6-113">本逐步解說會說明如何使用 Azure Cosmos DB 服務，來儲存和存取 Azure 上所託管的 ASP.NET MVC Web 應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="14cc6-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="14cc6-114">如果您要尋找僅著重於 Azure Cosmos DB (而不是 ASP.NET MVC 元件) 的教學課程，請參閱 [建置 Azure Cosmos DB C# 主控台應用程式](documentdb-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="14cc6-115">本教學課程假設您先前有過使用 ASP.NET MVC 和 Azure 網站的經驗。</span><span class="sxs-lookup"><span data-stu-id="14cc6-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="14cc6-116">如果您不熟悉 ASP.NET 或[必備工具](#_Toc395637760)，我們建議您從 [GitHub][GitHub] 下載完整的範例專案，並依照此範例的指示進行。</span><span class="sxs-lookup"><span data-stu-id="14cc6-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="14cc6-117">建置完成後，您可以檢閱此文章，以加深對專案內容中程式碼的了解。</span><span class="sxs-lookup"><span data-stu-id="14cc6-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="14cc6-118"><a name="_Toc395637760"></a>此資料庫教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="14cc6-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="14cc6-119">在依照本文中的指示進行之前，您應先確定備妥下列項目：</span><span class="sxs-lookup"><span data-stu-id="14cc6-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="14cc6-120">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="14cc6-120">An active Azure account.</span></span> <span data-ttu-id="14cc6-121">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="14cc6-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="14cc6-122">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="14cc6-123">或</span><span class="sxs-lookup"><span data-stu-id="14cc6-123">OR</span></span>

    <span data-ttu-id="14cc6-124">本機安裝的 [Azure Cosmos DB 模擬器](local-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="14cc6-125">[Visual Studio 2017](http://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="14cc6-126">Microsoft Azure SDK for .NET for Visual Studio 2017 (可透過 Visual Studio 安裝程式來取得)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="14cc6-127">本文中的所有螢幕擷取畫面都是使用 Microsoft Visual Studio Community 2017 所擷取的。</span><span class="sxs-lookup"><span data-stu-id="14cc6-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="14cc6-128">如果您的系統是設定使用不同的版本，則您的畫面和選項可能不會完全相符，但只要您符合上述必要條件，本方案應該還是有效。</span><span class="sxs-lookup"><span data-stu-id="14cc6-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="14cc6-129"><a name="_Toc395637761"></a>步驟 1：建立 Azure Cosmos DB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="14cc6-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="14cc6-130">我們將從建立 Azure Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="14cc6-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="14cc6-131">如果您已經擁有 Azure Cosmos DB 的 SQL (DocumentDB) 帳戶，或如果您正在使用 Azure Cosmos DB 模擬器來進行本教學課程，可以跳到[建立新的 ASP.NET MVC 應用程式](#_Toc395637762)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="14cc6-132">我們現在將從頭開始逐步解說如何建立新的 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14cc6-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="14cc6-133"><a name="_Toc395637762"></a>步驟 2：建立新的 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="14cc6-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="14cc6-134">在 Visual Studio 的 [檔案] 功能表中，指向 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="14cc6-135">[新增專案]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="14cc6-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="14cc6-136">在 [專案類型] 窗格中，依序展開 [範本]、[Visual C#]、[Web]，然後選取 [ASP.NET Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![[新增專案] 對話方塊的螢幕擷取畫面，內含反白顯示的 ASP.NET Web 應用程式專案類型](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="14cc6-138">在 [名稱]  方塊中，輸入專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="14cc6-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="14cc6-139">本教學課程使用 "todo" 名稱。</span><span class="sxs-lookup"><span data-stu-id="14cc6-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="14cc6-140">如果您選擇使用其他名稱，則每當本教學課程提及 todo 命名空間時，您必須調整提供的程式碼範例，以便使用您為應用程式所命名的名稱。</span><span class="sxs-lookup"><span data-stu-id="14cc6-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="14cc6-141">按一下 [瀏覽] 以巡覽至您想要建立專案的資料夾，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="14cc6-142">[新增 ASP.NET Web 應用程式] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="14cc6-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![[新增 ASP.NET Web 應用程式] 對話方塊的螢幕擷取畫面，內含反白顯示的 MVC 應用程式範本](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="14cc6-144">在 [範本] 窗格中，選取 [MVC] 。</span><span class="sxs-lookup"><span data-stu-id="14cc6-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="14cc6-145">按一下 [確定]  ，並讓 Visual Studio 執行有關 Scaffolding 空的 ASP.NET MVC 範本的作業。</span><span class="sxs-lookup"><span data-stu-id="14cc6-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="14cc6-146">Visual Studio 建立好未定案 MVC 應用程式之後，您便擁有可以在本機執行的空白 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14cc6-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="14cc6-147">我們會跳過在本機執行專案，因為我確定我們都已看過 ASP.NET "Hello World" 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14cc6-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="14cc6-148">讓我們直接跳到將 Azure Cosmos DB 新增至此專案，並建置應用程式的步驟。</span><span class="sxs-lookup"><span data-stu-id="14cc6-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="14cc6-149"><a name="_Toc395637767"></a>步驟 3：將 Azure Cosmos DB 新增至 MVC Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="14cc6-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="14cc6-150">既然我們已經完成了此解決方案的大部分 ASP.NET MVC 瑣事，現在可以開始本教學課程的真正目的，也就是將 Azure Cosmos DB 新增至 MVC Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14cc6-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="14cc6-151">Azure Cosmos DB .NET SDK 會進行封裝，並以 NuGet 封裝形式加以散發。</span><span class="sxs-lookup"><span data-stu-id="14cc6-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="14cc6-152">若要在 Visual Studio 中取得 NuGet 封裝，請使用 Visual Studio 中的 NuGet 封裝管理員，方法是以滑鼠右鍵按一下 [方案總管] 中的專案，然後按一下 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![[方案總管] 中 Web 應用程式專案的滑鼠右鍵選項螢幕擷取畫面，內含反白顯示的 [管理 NuGet 套件]。](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="14cc6-154">[ **管理 NuGet 封裝** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="14cc6-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="14cc6-155">在 NuGet [瀏覽] 方塊中，輸入 ***Azure DocumentDB***。</span><span class="sxs-lookup"><span data-stu-id="14cc6-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="14cc6-156">(套件名稱尚未更新為 Azure Cosmos DB)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="14cc6-157">從結果中，安裝 [Microsoft.Azure.DocumentDB by Microsoft] 套件。</span><span class="sxs-lookup"><span data-stu-id="14cc6-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="14cc6-158">這會下載和安裝 Azure Cosmos DB 套件，以及所有依存項目 (例如 Newtonsoft.Json)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="14cc6-159">按一下 [預覽] 視窗中的 [確定]，以及 [接受授權] 視窗中的 [我接受] 來完成安裝。</span><span class="sxs-lookup"><span data-stu-id="14cc6-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![[管理 NuGet 封裝] 視窗的螢幕擷取畫面，內含反白顯示的 Microsoft Azure DocumentDB 用戶端程式庫](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="14cc6-161">或者，您也可以使用 Package Manager Console 來安裝封裝。</span><span class="sxs-lookup"><span data-stu-id="14cc6-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="14cc6-162">若要這樣做，請在 [工具] 功能表上按一下 [NuGet 封裝管理員]，然後按一下 [Package Manager Console]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="14cc6-163">在出現提示時輸入下列內容：</span><span class="sxs-lookup"><span data-stu-id="14cc6-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="14cc6-164">安裝封裝之後，您的 Visual Studio 方案應該類似下列已新增兩個新參考 (Microsoft.Azure.Documents.Client 和 Newtonsoft.Json) 的方案。</span><span class="sxs-lookup"><span data-stu-id="14cc6-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![[方案總管] 中 JSON 資料專案新增兩個參考的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="14cc6-166"><a name="_Toc395637763"></a>步驟 4：設定 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="14cc6-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="14cc6-167">現在我們可以開始將模型、檢視和控制站新增至此 MVC 應用程式：</span><span class="sxs-lookup"><span data-stu-id="14cc6-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="14cc6-168">[新增模型](#_Toc395637764)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="14cc6-169">[新增控制器](#_Toc395637765)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="14cc6-170">[新增檢視](#_Toc395637766)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="14cc6-171"><a name="_Toc395637764"></a>新增 JSON 資料模型</span><span class="sxs-lookup"><span data-stu-id="14cc6-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="14cc6-172">首先，讓我們在 MVC 中建立 **M** (模型)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="14cc6-173">在 [方案總管] 中，以滑鼠右鍵按一下 **Models** 資料夾，再按一下 [新增]，然後按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="14cc6-174">[加入新項目]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="14cc6-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="14cc6-175">將您的新類別命名為 **Item.cs**，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="14cc6-176">在這個新的 **Item.cs** 檔案中，將下列程式碼加到最後一個 *using 陳述式*後面。</span><span class="sxs-lookup"><span data-stu-id="14cc6-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="14cc6-177">現在，將此程式碼取代</span><span class="sxs-lookup"><span data-stu-id="14cc6-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="14cc6-178">為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="14cc6-178">with the following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="14cc6-179">Azure Cosmos DB 中的所有資料都會透過線路傳遞，並儲存為 JSON。</span><span class="sxs-lookup"><span data-stu-id="14cc6-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="14cc6-180">如需透過 JSON.NET 控管物件序列化/取消序列化，您可以使用在剛才建立的 [項目] 類別中所示範 **JsonProperty** 屬性。</span><span class="sxs-lookup"><span data-stu-id="14cc6-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="14cc6-181">您 **無需** 這樣做，但我想確定所有屬性都會依照 JSON camelCase 的命名慣例命名。</span><span class="sxs-lookup"><span data-stu-id="14cc6-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="14cc6-182">使用 JSON 時，您不但可以控管屬性名稱格式，也可以跟我命名 **Description** 屬性一樣重新命名您的 .NET 屬性。</span><span class="sxs-lookup"><span data-stu-id="14cc6-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="14cc6-183"><a name="_Toc395637765"></a>新增控制器</span><span class="sxs-lookup"><span data-stu-id="14cc6-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="14cc6-184">我們已經建立了 **M**，現在讓我們建立 MVC 中的 **C** (控制器類別)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="14cc6-185">在 [方案總管] 中，以滑鼠右鍵按一下 **Controllers** 資料夾，按一下 [新增]，然後按一下 [控制器]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="14cc6-186">[ **新增 Scaffold** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="14cc6-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="14cc6-187">選取 [Web API 5 控制器 - 空]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![[新增 Scaffold] 對話方塊的螢幕擷取畫面，內含反白顯示的 [MVC 5 控制器 - 空的] 選項](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="14cc6-189">將新的控制器命名為 **ItemController**</span><span class="sxs-lookup"><span data-stu-id="14cc6-189">Name your new Controller, **ItemController.**</span></span>
   
    ![[新增控制器] 對話方塊的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="14cc6-191">檔案建立之後，您的 Visual Studio 方案應該類似包含下面 [方案總管] 中新 ItemController.cs 檔案的方案。</span><span class="sxs-lookup"><span data-stu-id="14cc6-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="14cc6-192">稍早建立的新 Item.cs 檔案也會顯示出來。</span><span class="sxs-lookup"><span data-stu-id="14cc6-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Visual Studio 的螢幕擷取畫面，[方案總管] 內含反白顯示的新 ItemController.cs 檔案和 Item.cs 檔案](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="14cc6-194">您可以先將 ItemController.cs 關閉，我們稍後會回頭使用此檔案。</span><span class="sxs-lookup"><span data-stu-id="14cc6-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="14cc6-195"><a name="_Toc395637766"></a>新增檢視</span><span class="sxs-lookup"><span data-stu-id="14cc6-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="14cc6-196">現在，我們可以開始建立 MVC 中的 **V** (檢視)：</span><span class="sxs-lookup"><span data-stu-id="14cc6-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="14cc6-197">[新增項目索引檢視](#AddItemIndexView)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="14cc6-198">[新增項目檢視](#AddNewIndexView)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="14cc6-199">[新增編輯項目檢視](#_Toc395888515)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="14cc6-200"><a name="AddItemIndexView"></a>新增項目索引檢視</span><span class="sxs-lookup"><span data-stu-id="14cc6-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="14cc6-201">在 [方案總管] 中，展開 **Views** 資料夾，以滑鼠右鍵按一下稍早您在建立 **ItemController** 時，Visual Studio 為您建立的空白 **Item** 資料夾，按一下 [新增]，然後按一下 [檢視]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![顯示 Visual Studio 方案建立之 Item 資料夾的 [方案總管] 螢幕擷取畫面，內含反白顯示的 [新增檢視] 命令](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="14cc6-203">在 [新增檢視]  對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="14cc6-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="14cc6-204">在 [檢視名稱] 方塊中，輸入***索引***。</span><span class="sxs-lookup"><span data-stu-id="14cc6-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="14cc6-205">在 [範本] 方塊中，選取 [清單]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="14cc6-206">在 [模型類別] 方塊中，選取 [項目 (todo.Models)]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="14cc6-207">在 [版面配置頁面] 方塊中，輸入 ***~/Views/Shared/_Layout.cshtml***。</span><span class="sxs-lookup"><span data-stu-id="14cc6-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![顯示 [新增檢視] 對話方塊的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="14cc6-209">設定所有這些值之後，按一下 [新增]  ，並讓 Visual Studio 建立新的範本檢視。</span><span class="sxs-lookup"><span data-stu-id="14cc6-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="14cc6-210">完成之後，系統便會開啟剛建立的 cshtml 檔案。</span><span class="sxs-lookup"><span data-stu-id="14cc6-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="14cc6-211">我們稍後會回頭使用此檔案，您可以先在 Visual Studio 中將該檔案關閉。</span><span class="sxs-lookup"><span data-stu-id="14cc6-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="14cc6-212"><a name="AddNewIndexView"></a>新增項目檢視</span><span class="sxs-lookup"><span data-stu-id="14cc6-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="14cc6-213">與建立 [項目索引] 檢視的方式類似，現在我們現在可以開始建立新的檢視，以供建立新的**項目**使用。</span><span class="sxs-lookup"><span data-stu-id="14cc6-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="14cc6-214">在 [方案總管] 中，再次以滑鼠右鍵按一下 **Item** 資料夾，按一下 [新增]，然後按一下 [檢視]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="14cc6-215">在 [新增檢視]  對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="14cc6-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="14cc6-216">在 [檢視名稱] 方塊中，輸入***建立***。</span><span class="sxs-lookup"><span data-stu-id="14cc6-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="14cc6-217">在 [範本] 方塊中，選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="14cc6-218">在 [模型類別] 方塊中，選取 [項目 (todo.Models)]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="14cc6-219">在 [版面配置頁面] 方塊中，輸入 ***~/Views/Shared/_Layout.cshtml***。</span><span class="sxs-lookup"><span data-stu-id="14cc6-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="14cc6-220">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="14cc6-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="14cc6-221"><a name="_Toc395888515"></a>新增編輯項目檢視</span><span class="sxs-lookup"><span data-stu-id="14cc6-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="14cc6-222">最後，使用與之前相同的方式新增最後一個檢視，以供編輯 **項目** 使用；</span><span class="sxs-lookup"><span data-stu-id="14cc6-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="14cc6-223">在 [方案總管] 中，再次以滑鼠右鍵按一下 **Item** 資料夾，按一下 [新增]，然後按一下 [檢視]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="14cc6-224">在 [新增檢視]  對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="14cc6-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="14cc6-225">在 [檢視名稱] 方塊中，輸入***編輯***。</span><span class="sxs-lookup"><span data-stu-id="14cc6-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="14cc6-226">在 [範本] 方塊中，選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="14cc6-227">在 [模型類別] 方塊中，選取 [項目 (todo.Models)]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="14cc6-228">在 [版面配置頁面] 方塊中，輸入 ***~/Views/Shared/_Layout.cshtml***。</span><span class="sxs-lookup"><span data-stu-id="14cc6-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="14cc6-229">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="14cc6-229">Click **Add**.</span></span>

<span data-ttu-id="14cc6-230">完成這項作業之後，請將 Visual Studio 中的所有 cshtml 文件關閉，我們稍後會回頭使用這些檢視。</span><span class="sxs-lookup"><span data-stu-id="14cc6-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="14cc6-231"><a name="_Toc395637769"></a>步驟 5︰裝設 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="14cc6-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="14cc6-232">我們已經建立了標準的 MVC 項目，現在可以開始新增 Azure Cosmos DB 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="14cc6-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="14cc6-233">在本節中，我們將新增程式碼來處理下列作業：</span><span class="sxs-lookup"><span data-stu-id="14cc6-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="14cc6-234">[列出未完成項目](#_Toc395637770)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="14cc6-235">[新增項目](#_Toc395637771)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="14cc6-236">[編輯項目](#_Toc395637772)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="14cc6-237"><a name="_Toc395637770"></a>列出 MVC Web 應用程式中的未完成項目</span><span class="sxs-lookup"><span data-stu-id="14cc6-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="14cc6-238">首先要執行的作業是新增類別，其中包含連線至及使用 Azure Cosmos DB 的所有邏輯。</span><span class="sxs-lookup"><span data-stu-id="14cc6-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="14cc6-239">在本教學課程中，我們會將所有邏輯封裝到名為 DocumentDBRepository 的儲存機制類別中。</span><span class="sxs-lookup"><span data-stu-id="14cc6-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="14cc6-240">在 [方案總管] 中，以滑鼠右鍵按一下專案，按一下 [新增]，然後按一下 [類別]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="14cc6-241">將新類別命名為 **DocumentDBRepository**，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="14cc6-242">在剛剛建立的 **DocumentDBRepository** 類別中，在「命名空間」宣告上方新增下列「using 陳述式」</span><span class="sxs-lookup"><span data-stu-id="14cc6-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="14cc6-243">現在，將此程式碼取代</span><span class="sxs-lookup"><span data-stu-id="14cc6-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="14cc6-244">為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="14cc6-244">with the following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. <span data-ttu-id="14cc6-245">我們打算從組態中讀取部分值，因此請開啟應用程式的 **Web.config** 檔案，並在 `<AppSettings>` 區段下新增下列幾行。</span><span class="sxs-lookup"><span data-stu-id="14cc6-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="14cc6-246">現在，使用 Azure 入口網站的 [金鑰] 刀鋒視窗來更新 [端點] 和 [authKey] 的值。</span><span class="sxs-lookup"><span data-stu-id="14cc6-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="14cc6-247">使用 [金鑰] 刀鋒視窗的 [URI] 做為端點設定的值，並使用 [金鑰] 刀鋒視窗的 [主索引鍵] 或 [次要金鑰] 做為 authKey 設定的值。</span><span class="sxs-lookup"><span data-stu-id="14cc6-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="14cc6-248">其會負責裝設 Azure Cosmos DB 存放庫，現在讓我們加入我們的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="14cc6-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="14cc6-249">我們想要對 todo 清單應用程式進行的第一件事就是顯示未完成的項目。</span><span class="sxs-lookup"><span data-stu-id="14cc6-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="14cc6-250">在 **DocumentDBRepository** 類別內的任意位置複製並貼上下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="14cc6-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="14cc6-251">開啟我們剛剛新增的 **ItemController** ，並在命名空間宣告上方新增下列 *using 陳述式*</span><span class="sxs-lookup"><span data-stu-id="14cc6-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="14cc6-252">如果您的專案名稱不是 "todo"，則您必須使用 "todo.Models" 進行更新，才能反映您的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="14cc6-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="14cc6-253">現在，將此程式碼取代</span><span class="sxs-lookup"><span data-stu-id="14cc6-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="14cc6-254">為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="14cc6-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="14cc6-255">開啟 **Global.asax.cs** 並將下列一行新增至 **Application_Start** 方法</span><span class="sxs-lookup"><span data-stu-id="14cc6-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="14cc6-256">此時，應該已經可以建置方案，而不會發生任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="14cc6-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="14cc6-257">如果您現在執行應用程式，您可以前往 **HomeController** 及該控制器的 [索引] 檢視。</span><span class="sxs-lookup"><span data-stu-id="14cc6-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="14cc6-258">這是我們在一開始時所選擇的 MVC 範本專案預設行為，但是我們不想要這樣的行為！</span><span class="sxs-lookup"><span data-stu-id="14cc6-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="14cc6-259">讓我們變更此 MVC 應用程式上的路由以改變此行為。</span><span class="sxs-lookup"><span data-stu-id="14cc6-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="14cc6-260">開啟 ***App\_Start\RouteConfig.cs***，並尋找以 "defaults:" 開頭的程式碼行，然後將它變更為如下所示。</span><span class="sxs-lookup"><span data-stu-id="14cc6-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="14cc6-261">如果您未在 URL 中指定控制路由行為的值，這會讓 ASP.NET MVC 知道改用 **Item** (**Home**) 作為控制器，並使用使用者**索引**作為檢視。</span><span class="sxs-lookup"><span data-stu-id="14cc6-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="14cc6-262">如果您執行應用程式，它現在會呼叫至您的 **ItemController**，進而呼叫至儲存機制類別，並使用 GetItems 方法將所有未完成的項目傳回 **Views**\\**Item**\\**Index** 檢視。</span><span class="sxs-lookup"><span data-stu-id="14cc6-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="14cc6-263">如果建置並立即執行此專案，您現在應該會看到如下的內容。</span><span class="sxs-lookup"><span data-stu-id="14cc6-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![本資料庫教學課程所建立的待辦事項清單 Web 應用程式的螢幕擷取畫面](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="14cc6-265"><a name="_Toc395637771"></a>新增項目</span><span class="sxs-lookup"><span data-stu-id="14cc6-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="14cc6-266">我們可以開始將一些項目放入資料庫中，所以除了空白方格以外，我們還可以看到其他項目。</span><span class="sxs-lookup"><span data-stu-id="14cc6-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="14cc6-267">讓我們將一些程式碼新增至 Azure Cosmos DBRepository 和 ItemController，以在 Azure Cosmos DB 中保留記錄。</span><span class="sxs-lookup"><span data-stu-id="14cc6-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="14cc6-268">將下列方法新增至 **DocumentDBRepository** 類別。</span><span class="sxs-lookup"><span data-stu-id="14cc6-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="14cc6-269">此方法只接受傳遞給它的物件，並將它保留在 Azure Cosmos DB 中。</span><span class="sxs-lookup"><span data-stu-id="14cc6-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="14cc6-270">開啟 ItemController.cs 檔案，並在類別中加入下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="14cc6-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="14cc6-271">這是 ASP.NET MVC 得知如何執行 **建立** 動作的方式。</span><span class="sxs-lookup"><span data-stu-id="14cc6-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="14cc6-272">在此情況下，只需轉譯先前建立的關聯 Create.cshtml 檢視。</span><span class="sxs-lookup"><span data-stu-id="14cc6-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="14cc6-273">現在此控制器需要更多程式碼，以接受 [建立]  檢視所提交的資料。</span><span class="sxs-lookup"><span data-stu-id="14cc6-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="14cc6-274">將下一個程式碼區塊新增至 ItemController.cs 類別，以告訴 ASP.NET MVC 如何使用表單 POST 來執行此控制器的作業。</span><span class="sxs-lookup"><span data-stu-id="14cc6-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="14cc6-275">這段程式碼會呼叫 DocumentDBRepository，並且使用 CreateItemAsync 方法將新的待辦事項項目保存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="14cc6-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="14cc6-276">**安全性注意事項**：此處所使用的 **ValidateAntiForgeryToken** 屬性可協助應用程式防止跨網站偽造要求攻擊。</span><span class="sxs-lookup"><span data-stu-id="14cc6-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="14cc6-277">這不光只是新增此屬性，您的檢視也必須使用這個防偽權杖。</span><span class="sxs-lookup"><span data-stu-id="14cc6-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="14cc6-278">如需此主題的詳細資訊以及如何正確實作此作業的範例，請參閱[防止跨網站偽造要求][Preventing Cross-Site Request Forgery]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="14cc6-279">[GitHub][GitHub] 上提供的原始程式碼已有完整實作。</span><span class="sxs-lookup"><span data-stu-id="14cc6-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="14cc6-280">**安全性注意事項**：我們也會在方法參數上使用 **Bind** 屬性，以協助防範 over-posting 攻擊。</span><span class="sxs-lookup"><span data-stu-id="14cc6-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="14cc6-281">如需詳細資訊，請參閱 [ASP.NET MVC 中的基本 CRUD 作業][Basic CRUD Operations in ASP.NET MVC]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="14cc6-282">這包括將新項目新增至資料庫所需的程式碼。</span><span class="sxs-lookup"><span data-stu-id="14cc6-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="14cc6-283"><a name="_Toc395637772"></a>編輯項目</span><span class="sxs-lookup"><span data-stu-id="14cc6-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="14cc6-284">我們最後還要做一件事，那就是新增在資料庫中編輯 **項目** ，以及將它們標示為已完成的功能。</span><span class="sxs-lookup"><span data-stu-id="14cc6-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="14cc6-285">編輯的檢視已經新增至專案，因此，我們只需重新將某些程式碼新增至控制器及 **DocumentDBRepository** 類別即可。</span><span class="sxs-lookup"><span data-stu-id="14cc6-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="14cc6-286">將下列程式碼新增至 **DocumentDBRepository** 類別。</span><span class="sxs-lookup"><span data-stu-id="14cc6-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="14cc6-287">這兩個方法中的第一個方法 (GetItem) 會從 Azure Cosmos DB 提取項目，此項目會被傳回 **ItemController**，接著傳至 [編輯] 檢視。</span><span class="sxs-lookup"><span data-stu-id="14cc6-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="14cc6-288">第二個剛剛新增的方法是使用從 **ItemController** 傳入的**文件**版本，來取代 Azure Cosmos DB 中的**文件**。</span><span class="sxs-lookup"><span data-stu-id="14cc6-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="14cc6-289">將下列程式碼新增至 **ItemController** 類別。</span><span class="sxs-lookup"><span data-stu-id="14cc6-289">Add the following to the **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="14cc6-290">第一個方法會處理當使用者按一下 [索引] 檢視中的 [編輯] 連結時所發生的 Http GET。</span><span class="sxs-lookup"><span data-stu-id="14cc6-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="14cc6-291">此方法會從 Azure Cosmos DB 中提取[**文件**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx)，並將它傳遞給 [編輯] 檢視。</span><span class="sxs-lookup"><span data-stu-id="14cc6-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="14cc6-292">[編輯] 檢視會接著對 **IndexController** 執行 Http POST。</span><span class="sxs-lookup"><span data-stu-id="14cc6-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="14cc6-293">所新增的第二個方法會處理此作業，將更新的物件傳遞至 Azure Cosmos DB，並保留在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="14cc6-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="14cc6-294">這樣便大功告成了，這些就是我們必須執行應用程式的所有作業：列出未完成**項目**、新增**項目**，最後是編輯**項目**。</span><span class="sxs-lookup"><span data-stu-id="14cc6-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="14cc6-295"><a name="_Toc395637773"></a>步驟 6：在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="14cc6-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="14cc6-296">若要在本機電腦測試應用程式，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="14cc6-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="14cc6-297">在 Visual Studio 中按 F5，即可在偵錯模式下建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="14cc6-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="14cc6-298">這樣應該可以建置應用程式，並啟動含有先前所看過之空白方格頁面的瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="14cc6-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![本資料庫教學課程所建立的待辦事項清單 Web 應用程式的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="14cc6-300">按一下 [新建] 連結，並在 [名稱] 和 [描述] 欄位中新增值。</span><span class="sxs-lookup"><span data-stu-id="14cc6-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="14cc6-301">將 [已完成] 核取方塊保持為未選取狀態，否則，**新項目**會以已完成的狀態新增，且不會出現在初始清單中。</span><span class="sxs-lookup"><span data-stu-id="14cc6-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![[建立] 檢視的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="14cc6-303">按一下 [建立]，您便會被重新導向回到 [索引] 檢視，且您的**項目**便會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="14cc6-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![[索引] 檢視的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="14cc6-305">依需要新增一些 **項目** 至 [待辦事項] 清單。</span><span class="sxs-lookup"><span data-stu-id="14cc6-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="14cc6-306">按一下清單上 [項目] 旁邊的 [編輯]，您便會被帶到 [編輯] 檢視，您可以在此更新物件的任何屬性 (包括 [已完成] 旗標)。</span><span class="sxs-lookup"><span data-stu-id="14cc6-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="14cc6-307">如果您標示 [完成] 旗標，然後按一下 [儲存]，則**項目**會從未完成的工作清單中移除。</span><span class="sxs-lookup"><span data-stu-id="14cc6-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![[索引] 檢視的螢幕擷取畫面，內含勾選的 [已完成] 方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="14cc6-309">完成測試應用程式後，按 Ctrl + F5 停止偵錯應用程式。</span><span class="sxs-lookup"><span data-stu-id="14cc6-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="14cc6-310">您現在可以開始進行部署。</span><span class="sxs-lookup"><span data-stu-id="14cc6-310">You're ready to deploy!</span></span>

## <span data-ttu-id="14cc6-311"><a name="_Toc395637774"></a>步驟 7：將應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="14cc6-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="14cc6-312">您已經擁有可在 Azure Cosmos DB 正常運作的完整應用程式，我們現在要將此 Web 應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="14cc6-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="14cc6-313">若要發佈此應用程式，您只需要以滑鼠右鍵按一下 [方案總管] 上的專案，然後按一下 [發佈] 即可。</span><span class="sxs-lookup"><span data-stu-id="14cc6-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![[方案總管] 中 [發佈] 選項的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="14cc6-315">在 [發佈] 對話方塊中，按一下 [Microsoft Azure App Service]，然後選取 [建立新的] 來建立 App Service 設定檔，或按一下 [選取現有的] 來使用現有設定檔。</span><span class="sxs-lookup"><span data-stu-id="14cc6-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Visual Studio 中的 [發佈] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="14cc6-317">如果您有現有的 Azure App Service 設定檔，請輸入您的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="14cc6-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="14cc6-318">使用 [檢視] 篩選器來依資源群組或資源類型排序，然後選取您的 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="14cc6-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Visual Studio 中的 [App Service] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="14cc6-320">若要建立新的 Azure App Service 設定檔，請按一下 [發佈] 對話方塊中的 [建立新的]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="14cc6-321">在 [建立 App Service] 對話方塊中，輸入您的 Web 應用程式名稱和適當的訂用帳戶、資源群組和 App Service 方案，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="14cc6-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Visual Studio 中的 [建立 App Service] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="14cc6-323">幾秒後，Visual Studio 便會發佈 Web 應用程式並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！</span><span class="sxs-lookup"><span data-stu-id="14cc6-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="14cc6-324"><a name="_Toc395637775"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="14cc6-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="14cc6-325">恭喜！</span><span class="sxs-lookup"><span data-stu-id="14cc6-325">Congratulations!</span></span> <span data-ttu-id="14cc6-326">您剛剛使用 Azure Cosmos DB 建置您的第一個 ASP.NET MVC Web 應用程式，並將它發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="14cc6-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="14cc6-327">您可以從 [GitHub][GitHub]下載或複製完整應用程式 (包括不包含在本教學課程中的詳細資料和刪除功能) 的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="14cc6-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="14cc6-328">所以如果您想要將程式碼加入您的應用程式，請抓取程式碼，並將它加入這個應用程式。</span><span class="sxs-lookup"><span data-stu-id="14cc6-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="14cc6-329">若要將其他功能新增至您的應用程式，請檢閱 [Azure Cosmos DB .NET 程式庫](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)中提供的 API，並歡迎您貢獻到 [GitHub][GitHub] 上的 Azure Cosmos DB .NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="14cc6-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
