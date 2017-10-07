---
title: "Azure Cosmos DB 的 ASP.NET MVC 教學課程：Web 應用程式開發 | Microsoft Docs"
description: "ASP.NET MVC 教學課程 toocreate MVC web 應用程式使用 Azure Cosmos DB。 您將在託管於 Azure 網站的待辦事項應用程式儲存 JSON 和存取資料 - ASP NET MVC 教學課程逐步解說。"
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
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="37bf1-105"><a name="_Toc395809351"></a>ASP.NET MVC 教學課程：使用 Azure Cosmos DB 進行 Web 應用程式開發</span><span class="sxs-lookup"><span data-stu-id="37bf1-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37bf1-106">.NET</span><span class="sxs-lookup"><span data-stu-id="37bf1-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="37bf1-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="37bf1-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="37bf1-108">Java</span><span class="sxs-lookup"><span data-stu-id="37bf1-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="37bf1-109">Python</span><span class="sxs-lookup"><span data-stu-id="37bf1-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="37bf1-110">toohighlight 如何有效率地，您可以利用 Azure Cosmos DB toostore，與查詢 JSON 文件，這篇文章提供端對端逐步解說顯示如何 toobuild 使用 Azure Cosmos DB 待辦事項應用程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="37bf1-111">hello 工作將會儲存為 Azure Cosmos DB 中的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="37bf1-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Hello todo 清單本教學課程-ASP NET MVC 教學課程逐步解說所建立的 MVC web 應用程式的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="37bf1-113">本逐步解說會示範如何 toouse hello Azure Cosmos DB 服務 toostore 及存取資料從 Azure 上裝載的 ASP.NET MVC web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="37bf1-114">如果您想要尋求著重在 Azure Cosmos DB 的教學課程，而且不 hello ASP.NET MVC 元件，請參閱[建置 Azure Cosmos DB C# 主控台應用程式](documentdb-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="37bf1-115">本教學課程假設您先前有過使用 ASP.NET MVC 和 Azure 網站的經驗。</span><span class="sxs-lookup"><span data-stu-id="37bf1-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="37bf1-116">如果您是新 tooASP.NET 或 hello[必要條件工具](#_Toc395637760)，我們建議您下載 hello 完整的範例專案，從[GitHub] [ GitHub]和中的 hello 指示此範例中。</span><span class="sxs-lookup"><span data-stu-id="37bf1-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="37bf1-117">一旦建立它，您可以檢閱此文件 toogain 的深入了解 hello hello hello 專案內容中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="37bf1-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="37bf1-118"><a name="_Toc395637760"></a>此資料庫教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="37bf1-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="37bf1-119">這篇文章中的 hello 指示之前，您應該確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="37bf1-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="37bf1-120">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="37bf1-120">An active Azure account.</span></span> <span data-ttu-id="37bf1-121">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="37bf1-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="37bf1-122">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="37bf1-123">或</span><span class="sxs-lookup"><span data-stu-id="37bf1-123">OR</span></span>

    <span data-ttu-id="37bf1-124">Hello 的本機安裝[Azure Cosmos DB 模擬器](local-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="37bf1-125">[Visual Studio 2017](http://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="37bf1-126">Microsoft Azure SDK for.NET 的 Visual Studio 2017，可透過 hello Visual Studio 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="37bf1-127">已使用 Microsoft Visual Studio 社群 2017年採取這篇文章中的所有 hello 螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="37bf1-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="37bf1-128">如果您的系統設定的不同版本很可能您的螢幕和選項都不會完全，符合，但如果符合上述必要條件 hello 應該使用此解決方案。</span><span class="sxs-lookup"><span data-stu-id="37bf1-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="37bf1-129"><a name="_Toc395637761"></a>步驟 1：建立 Azure Cosmos DB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="37bf1-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="37bf1-130">我們將從建立 Azure Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="37bf1-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="37bf1-131">如果您已有 Azure Cosmos DB SQL (DocumentDB) 帳戶，或如果您使用 hello Azure Cosmos DB 模擬器本教學課程中，您可以跳過[建立新的 ASP.NET MVC 應用程式](#_Toc395637762)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="37bf1-132">我們現在會逐步解說如何 toocreate 新的 ASP.NET MVC 應用程式從 hello 從頭。</span><span class="sxs-lookup"><span data-stu-id="37bf1-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="37bf1-133"><a name="_Toc395637762"></a>步驟 2：建立新的 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="37bf1-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="37bf1-134">在 Visual Studio 中的 hello**檔案**功能表上，點太**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="37bf1-135">hello**新專案** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="37bf1-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="37bf1-136">在 [hello**專案類型**] 窗格中，展開**範本**， **Visual C#**， **Web**，然後選取**ASP.NET Web 應用程式**.</span><span class="sxs-lookup"><span data-stu-id="37bf1-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![螢幕擷取畫面 hello 新增專案 對話方塊與 hello 反白顯示的 ASP.NET Web 應用程式專案類型](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="37bf1-138">在 [hello**名稱**] 方塊中，輸入 hello 名稱的 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="37bf1-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="37bf1-139">本教學課程使用 hello 名稱"todo"。</span><span class="sxs-lookup"><span data-stu-id="37bf1-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="37bf1-140">如果您選擇 toouse 這以外的項目，然後每當本教學課程參 hello todo 命名空間，您需要 tooadjust hello 提供程式碼範例 toouse 任何您已命名為您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="37bf1-141">按一下**瀏覽**toonavigate toohello 資料夾位置，toocreate hello 專案，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="37bf1-142">hello**新的 ASP.NET Web 應用程式** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="37bf1-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Hello 反白顯示 hello MVC 應用程式範本 [新的 ASP.NET Web 應用程式] 對話方塊的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="37bf1-144">在 hello 範本 窗格中，選取  **MVC**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="37bf1-145">按一下**確定**，讓 Visual Studio 執行其動作周圍 scaffolding hello 空白 ASP.NET MVC 範本。</span><span class="sxs-lookup"><span data-stu-id="37bf1-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="37bf1-146">一旦完成 Visual Studio 建立 hello 未定案 MVC 應用程式會有空白的 ASP.NET 應用程式，您可以在本機執行。</span><span class="sxs-lookup"><span data-stu-id="37bf1-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="37bf1-147">我們會略過執行 hello 專案在本機相信我們所有看到的 hello ASP.NET"Hello World"應用程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="37bf1-148">讓我們前往直線 tooadding Azure Cosmos DB toothis 專案並建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="37bf1-149"><a name="_Toc395637767"></a>步驟 3： 加入 Azure Cosmos DB tooyour MVC web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="37bf1-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="37bf1-150">既然我們已經有大部分的 hello ASP.NET MVC 配管，我們需要針對此解決方案，讓我們協助 toohello 真正的目的，本教學課程，加入 Azure Cosmos DB tooour MVC web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="37bf1-151">hello Azure Cosmos DB.NET SDK 會封裝，並以 NuGet 封裝進行散發。</span><span class="sxs-lookup"><span data-stu-id="37bf1-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="37bf1-152">tooget hello Visual Studio 中的 NuGet 封裝，使用 Visual Studio 中的 hello NuGet 套件管理員中的 hello 專案上按一下滑鼠右鍵**方案總管 中**，然後按一下**管理 NuGet 封裝**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Hello 的螢幕擷取畫面以滑鼠右鍵按一下方案總管中，使用 管理 NuGet 封裝的反白顯示 hello web 應用程式專案的選項。](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="37bf1-154">hello**管理 NuGet 封裝** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="37bf1-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="37bf1-155">在 hello NuGet**瀏覽**方塊中，輸入***Azure DocumentDB***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="37bf1-156">（hello 封裝名稱尚未更新的 tooAzure Cosmos DB。）</span><span class="sxs-lookup"><span data-stu-id="37bf1-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="37bf1-157">從 hello 結果中，安裝 hello **microsoft Microsoft.Azure.DocumentDB**封裝。</span><span class="sxs-lookup"><span data-stu-id="37bf1-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="37bf1-158">這會下載並安裝 hello Azure Cosmos DB 封裝，以及所有相依性，例如 Newtonsoft.Json。</span><span class="sxs-lookup"><span data-stu-id="37bf1-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="37bf1-159">按一下**確定**hello 中**預覽**視窗中，和**我接受**hello 中**授權接受**視窗 toocomplete hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="37bf1-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Hello 管理 NuGet 封裝 視窗，以 hello Microsoft Azure DocumentDB 用戶端程式庫反白顯示的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="37bf1-161">或者，您可以使用 Package Manager Console tooinstall hello 套件 hello。</span><span class="sxs-lookup"><span data-stu-id="37bf1-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="37bf1-162">toodo，請在 hello**工具**功能表上，按一下  **NuGet 套件管理員**，然後按一下 **Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="37bf1-163">在 hello 提示字元中輸入下列 hello。</span><span class="sxs-lookup"><span data-stu-id="37bf1-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="37bf1-164">Hello 封裝安裝之後，您的 Visual Studio 方案應該類似下列兩個新的參考加入，Microsoft.Azure.Documents.Client 和 Newtonsoft.Json hello。</span><span class="sxs-lookup"><span data-stu-id="37bf1-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Hello 兩個參考的螢幕擷取畫面加入 toohello JSON 資料專案在 方案總管](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="37bf1-166"><a name="_Toc395637763"></a>步驟 4： 設定 hello ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="37bf1-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="37bf1-167">現在讓我們加入 hello 模型、 檢視和控制器 toothis MVC 應用程式：</span><span class="sxs-lookup"><span data-stu-id="37bf1-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="37bf1-168">[新增模型](#_Toc395637764)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="37bf1-169">[新增控制器](#_Toc395637765)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="37bf1-170">[新增檢視](#_Toc395637766)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="37bf1-171"><a name="_Toc395637764"></a>新增 JSON 資料模型</span><span class="sxs-lookup"><span data-stu-id="37bf1-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="37bf1-172">讓我們先建立 hello **M**在 MVC 中，hello 模型。</span><span class="sxs-lookup"><span data-stu-id="37bf1-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="37bf1-173">在**方案總管] 中**，以滑鼠右鍵按一下 hello**模型**資料夾中，按一下 [**新增**，然後按一下**類別**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="37bf1-174">hello**加入新項目** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="37bf1-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="37bf1-175">將您的新類別命名為 **Item.cs**，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="37bf1-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="37bf1-176">在這個新**Item.cs**檔案中，最後將之後 hello hello 面一行加入*使用陳述式*。</span><span class="sxs-lookup"><span data-stu-id="37bf1-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="37bf1-177">現在，將此程式碼取代</span><span class="sxs-lookup"><span data-stu-id="37bf1-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="37bf1-178">以下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="37bf1-178">with hello following code.</span></span>
   
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
   
    <span data-ttu-id="37bf1-179">Azure Cosmos DB 中的所有資料都傳送 hello 線上，而且儲存成 JSON。</span><span class="sxs-lookup"><span data-stu-id="37bf1-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="37bf1-180">toocontrol hello 方式將物件序列化/還原序列化，您可以使用的 JSON.NET 的 hello **JsonProperty**屬性示 hello**項目**剛才所建立的類別。</span><span class="sxs-lookup"><span data-stu-id="37bf1-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="37bf1-181">您沒有**有**toodo 這但我想 tooensure 我屬性都會遵循 hello JSON camelCase 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="37bf1-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="37bf1-182">不只可以您控制 hello 屬性名稱的 hello 格式時進入 JSON，但您可以完全重新命名.NET 屬性我如同以 hello**描述**屬性。</span><span class="sxs-lookup"><span data-stu-id="37bf1-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="37bf1-183"><a name="_Toc395637765"></a>新增控制器</span><span class="sxs-lookup"><span data-stu-id="37bf1-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="37bf1-184">會負責 hello **M**，現在讓我們來建立 hello **C**在 MVC 中，控制器類別。</span><span class="sxs-lookup"><span data-stu-id="37bf1-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="37bf1-185">在**方案總管 中**，以滑鼠右鍵按一下 hello**控制站**資料夾中，按一下**新增**，然後按一下**控制器**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="37bf1-186">hello**新增 Scaffold**  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="37bf1-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="37bf1-187">選取 Web API 5 控制器 - 空，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="37bf1-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Hello 以 hello MVC 5 控制器空反白顯示的選項加入 Scaffold 對話方塊的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="37bf1-189">將新的控制器命名為 **ItemController**</span><span class="sxs-lookup"><span data-stu-id="37bf1-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Hello [加入控制器] 對話方塊的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="37bf1-191">一旦建立 hello 檔案時，Visual Studio 方案看起來應該像 hello 下列 hello 新 ItemController.cs 檔案中與**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="37bf1-192">也會顯示 hello 稍早建立新 Item.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="37bf1-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Hello Visual Studio 方案-與 hello 新 ItemController.cs 檔案，並反白顯示 Item.cs 檔案的 [方案總管] 的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="37bf1-194">您可以關閉 ItemController.cs，再回來 tooit 更新版本。</span><span class="sxs-lookup"><span data-stu-id="37bf1-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="37bf1-195"><a name="_Toc395637766"></a>新增檢視</span><span class="sxs-lookup"><span data-stu-id="37bf1-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="37bf1-196">現在，讓我們來建立 hello **V**在 MVC 中，hello 檢視：</span><span class="sxs-lookup"><span data-stu-id="37bf1-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="37bf1-197">[新增項目索引檢視](#AddItemIndexView)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="37bf1-198">[新增項目檢視](#AddNewIndexView)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="37bf1-199">[新增編輯項目檢視](#_Toc395888515)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="37bf1-200"><a name="AddItemIndexView"></a>新增項目索引檢視</span><span class="sxs-lookup"><span data-stu-id="37bf1-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="37bf1-201">在**方案總管] 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下空白的 hello**項目**加入 hello 時為您建立 Visual Studio 的資料夾**ItemController**舊版中，按一下 [**新增**，然後按一下**檢視**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![顯示 hello 項目資料夾以反白顯示 hello 加入檢視命令，建立 Visual Studio 方案總管的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="37bf1-203">在 hello**加入檢視**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="37bf1-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="37bf1-204">在 hello**檢視名稱**方塊中，輸入***索引***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="37bf1-205">在 hello**範本**方塊中，選取***清單***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="37bf1-206">在 hello**模型類別**方塊中，選取***項目 (todo。模型）***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="37bf1-207">在 hello 版面配置頁面中，輸入***~/Views/Shared/_Layout.cshtml***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![螢幕擷取畫面顯示 hello 新增檢視對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="37bf1-209">設定所有這些值之後，按一下 [新增]  ，並讓 Visual Studio 建立新的範本檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="37bf1-210">一旦完成後，就會開啟 hello cshtml 檔案所建立。</span><span class="sxs-lookup"><span data-stu-id="37bf1-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="37bf1-211">因為我們將 tooit 稍後再回來，我們可以關閉 Visual Studio 中的該檔案。</span><span class="sxs-lookup"><span data-stu-id="37bf1-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="37bf1-212"><a name="AddNewIndexView"></a>新增項目檢視</span><span class="sxs-lookup"><span data-stu-id="37bf1-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="37bf1-213">我們建立類似 toohow**項目索引** 檢視中，現在我們將建立新的檢視，來建立新**項目**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="37bf1-214">在**方案總管 中**，以滑鼠右鍵按一下 hello**項目**資料夾再按一下**新增**，然後按一下**檢視**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="37bf1-215">在 hello**加入檢視**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="37bf1-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="37bf1-216">在 hello**檢視名稱**方塊中，輸入***建立***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="37bf1-217">在 hello**範本**方塊中，選取***建立***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="37bf1-218">在 hello**模型類別**方塊中，選取***項目 (todo。模型）***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="37bf1-219">在 hello 版面配置頁面中，輸入***~/Views/Shared/_Layout.cshtml***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="37bf1-220">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="37bf1-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="37bf1-221"><a name="_Toc395888515"></a>新增編輯項目檢視</span><span class="sxs-lookup"><span data-stu-id="37bf1-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="37bf1-222">最後，會加入一個編輯的最後一個檢視和**項目**在 hello 與之前相同的方式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="37bf1-223">在**方案總管 中**，以滑鼠右鍵按一下 hello**項目**資料夾再按一下**新增**，然後按一下**檢視**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="37bf1-224">在 hello**加入檢視**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="37bf1-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="37bf1-225">在 hello**檢視名稱**方塊中，輸入***編輯***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="37bf1-226">在 hello**範本**方塊中，選取***編輯***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="37bf1-227">在 hello**模型類別**方塊中，選取***項目 (todo。模型）***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="37bf1-228">在 hello 版面配置頁面中，輸入***~/Views/Shared/_Layout.cshtml***。</span><span class="sxs-lookup"><span data-stu-id="37bf1-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="37bf1-229">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="37bf1-229">Click **Add**.</span></span>

<span data-ttu-id="37bf1-230">完成之後，關閉所有 Visual Studio 中的 hello cshtml 文件，因為我們將稍後再回來 toothese 檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="37bf1-231"><a name="_Toc395637769"></a>步驟 5︰裝設 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="37bf1-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="37bf1-232">既然已處理 hello 標準的 MVC 動作完成，讓我們來開啟 tooadding hello 程式碼的 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="37bf1-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="37bf1-233">在本節中，我們會將 toohandle hello 後面的程式碼：</span><span class="sxs-lookup"><span data-stu-id="37bf1-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="37bf1-234">[列出未完成項目](#_Toc395637770)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="37bf1-235">[新增項目](#_Toc395637771)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="37bf1-236">[編輯項目](#_Toc395637772)。</span><span class="sxs-lookup"><span data-stu-id="37bf1-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="37bf1-237"><a name="_Toc395637770"></a>列出 MVC Web 應用程式中的未完成項目</span><span class="sxs-lookup"><span data-stu-id="37bf1-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="37bf1-238">hello 第一件事 toodo 這裡會加入包含所有 hello 邏輯 tooconnect tooand 使用 Azure Cosmos DB 的類別。</span><span class="sxs-lookup"><span data-stu-id="37bf1-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="37bf1-239">此教學課程中我們將會封裝此呼叫 DocumentDBRepository tooa 儲存機制類別中的所有邏輯。</span><span class="sxs-lookup"><span data-stu-id="37bf1-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="37bf1-240">在**方案總管 中**hello 專案上按一下滑鼠右鍵、 按一下**新增**，然後按一下**類別**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="37bf1-241">Hello 新類別命名**DocumentDBRepository**按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="37bf1-242">在新建立的 hello **DocumentDBRepository**類別，然後將 hello 下列*using 陳述式*上方 hello*命名空間*宣告</span><span class="sxs-lookup"><span data-stu-id="37bf1-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="37bf1-243">現在，將此程式碼取代</span><span class="sxs-lookup"><span data-stu-id="37bf1-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="37bf1-244">以下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="37bf1-244">with hello following code.</span></span>
   
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
   
    
3. <span data-ttu-id="37bf1-245">我們正在讀取組態中的某些值，因此開啟 hello **Web.config**應用程式的檔案並加入下列行下 hello hello `<AppSettings>` > 一節。</span><span class="sxs-lookup"><span data-stu-id="37bf1-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="37bf1-246">現在，更新 hello 值*端點*和*authKey*使用 hello 金鑰刀鋒視窗中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="37bf1-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="37bf1-247">使用 hello **URI** hello 做為 hello 端點設定，並使用 hello hello 值的索引鍵 刀鋒視窗從**主索引鍵**，或**次要金鑰**從 hello 做為 hello hello 值的索引鍵 刀鋒視窗authKey 設定。</span><span class="sxs-lookup"><span data-stu-id="37bf1-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="37bf1-248">會負責裝設 hello Azure Cosmos DB 儲存機制，現在讓我們來新增應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="37bf1-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="37bf1-249">hello 首先我們要 toobe 無法 toodo 待辦事項清單應用程式與為 toodisplay hello 不完整的項目。</span><span class="sxs-lookup"><span data-stu-id="37bf1-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="37bf1-250">複製並貼上下列程式碼片段中任何位置的 hello hello **DocumentDBRepository**類別。</span><span class="sxs-lookup"><span data-stu-id="37bf1-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="37bf1-251">開啟 hello **ItemController**我們稍早加入並新增下列 hello *using 陳述式*hello 命名空間宣告上方。</span><span class="sxs-lookup"><span data-stu-id="37bf1-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="37bf1-252">如果您專案不是"todo"，則您需要使用"todo tooupdate。模型 >。tooreflect hello 專案名稱。</span><span class="sxs-lookup"><span data-stu-id="37bf1-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="37bf1-253">現在，將此程式碼取代</span><span class="sxs-lookup"><span data-stu-id="37bf1-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="37bf1-254">以下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="37bf1-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="37bf1-255">開啟**Global.asax.cs**並加入下列行 toohello hello **Application_Start**方法</span><span class="sxs-lookup"><span data-stu-id="37bf1-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="37bf1-256">此時您的解決方案應該能夠 toobuild 沒有發生任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="37bf1-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="37bf1-257">如果您已執行 hello 應用程式現在，您將會進入 toohello **HomeController**和 hello**索引**該控制器的檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="37bf1-258">這是我們選擇在 hello 開頭 hello MVC 範本專案的 hello 預設行為，但我們不想要 ！</span><span class="sxs-lookup"><span data-stu-id="37bf1-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="37bf1-259">我們來變更 hello 路由這個 MVC 應用程式 tooalter 這種行為。</span><span class="sxs-lookup"><span data-stu-id="37bf1-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="37bf1-260">開啟***應用程式\_Start\RouteConfig.cs***並找出 hello 行開頭為 「 預設值:"並將它變更為下列 tooresemble hello。</span><span class="sxs-lookup"><span data-stu-id="37bf1-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="37bf1-261">這會告訴您擁有 hello URL toocontrol 中未指定值，如果 hello，而是路由行為的 ASP.NET MVC**首頁**，使用**項目**為 hello 控制站及使用者**索引**為 hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="37bf1-262">現在，如果您要執行 hello 應用程式，它會呼叫您**ItemController**這將會呼叫 toohello 儲存機制類別中，並使用 hello GetItems 方法 tooreturn 所有 hello 不完整的項目 toohello**檢視**\\**項目**\\**索引**檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="37bf1-263">如果建置並立即執行此專案，您現在應該會看到如下的內容。</span><span class="sxs-lookup"><span data-stu-id="37bf1-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Hello todo 清單 web 應用程式建立此資料庫的教學課程的螢幕擷取畫面](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="37bf1-265"><a name="_Toc395637771"></a>新增項目</span><span class="sxs-lookup"><span data-stu-id="37bf1-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="37bf1-266">讓我們將某些項目放入資料庫，讓我們有更多超過在空的方格窗格 toolook。</span><span class="sxs-lookup"><span data-stu-id="37bf1-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="37bf1-267">讓我們加入一些程式碼太 Azure Cosmos DB 中的 Azure Cosmos DBRepository 且 ItemController toopersist hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="37bf1-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="37bf1-268">新增下列方法 tooyour hello **DocumentDBRepository**類別。</span><span class="sxs-lookup"><span data-stu-id="37bf1-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="37bf1-269">這個方法只會採用傳遞 tooit 的物件，並將它保存在 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="37bf1-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="37bf1-270">開啟 hello ItemController.cs 檔案並加入下列程式碼片段 hello 類別內的 hello。</span><span class="sxs-lookup"><span data-stu-id="37bf1-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="37bf1-271">這是 ASP.NET MVC 如何知道哪些 toodo hello**建立**動作。</span><span class="sxs-lookup"><span data-stu-id="37bf1-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="37bf1-272">在此情況下只呈現 hello 相關 Create.cshtml 稍早建立的檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="37bf1-273">我們現在需要某些更多的程式碼，將會接受從 hello hello 提交此控制器中**建立**檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="37bf1-274">新增 hello 的程式碼 toohello ItemController.cs 類別，此控制站的表單 POST 哪些 toodo 告知 ASP.NET MVC 的下一個區塊。</span><span class="sxs-lookup"><span data-stu-id="37bf1-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="37bf1-275">此程式碼會呼叫 toohello DocumentDBRepository 中，並使用 hello CreateItemAsync 方法 toopersist hello 新 todo 項目 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="37bf1-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="37bf1-276">**安全性注意事項**: hello **ValidateAntiForgeryToken**屬性使用這裡 toohelp 保護此應用程式針對跨站台要求偽造攻擊。</span><span class="sxs-lookup"><span data-stu-id="37bf1-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="37bf1-277">多個 tooit 比只將這個屬性，檢視需要 toowork 與這個防偽語彙基元。</span><span class="sxs-lookup"><span data-stu-id="37bf1-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="37bf1-278">如需有關 hello 主旨，以及如何 tooimplement 這是否正確，請參閱範例[防止跨站台要求偽造][Preventing Cross-Site Request Forgery]。</span><span class="sxs-lookup"><span data-stu-id="37bf1-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="37bf1-279">hello 上所提供的原始程式碼[GitHub] [ GitHub]有 hello 完整實作的。</span><span class="sxs-lookup"><span data-stu-id="37bf1-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="37bf1-280">**安全性注意事項**： 我們也會使用 hello**繫結**hello 方法參數 toohelp 屬性防止過度張貼攻擊。</span><span class="sxs-lookup"><span data-stu-id="37bf1-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="37bf1-281">如需詳細資訊，請參閱 [ASP.NET MVC 中的基本 CRUD 作業][Basic CRUD Operations in ASP.NET MVC]。</span><span class="sxs-lookup"><span data-stu-id="37bf1-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="37bf1-282">這總結 hello 所需的程式碼 tooadd 新項目 tooour 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="37bf1-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="37bf1-283"><a name="_Toc395637772"></a>編輯項目</span><span class="sxs-lookup"><span data-stu-id="37bf1-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="37bf1-284">沒有為我們的最後一件事 toodo，並且可 tooadd hello 能力 tooedit**項目**hello 資料庫和 toomark 來完成。</span><span class="sxs-lookup"><span data-stu-id="37bf1-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="37bf1-285">hello 編輯檢視已加入 toohello 專案，因此我們只需要 tooadd 部分的程式碼 tooour 控制器和 toohello **DocumentDBRepository**類別一次。</span><span class="sxs-lookup"><span data-stu-id="37bf1-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="37bf1-286">新增下列 toohello hello **DocumentDBRepository**類別。</span><span class="sxs-lookup"><span data-stu-id="37bf1-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="37bf1-287">hello 的這些方法的第一個**GetItem**擷取項目從 Azure Cosmos DB 傳遞後 toohello **ItemController**然後在 toohello**編輯**檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="37bf1-288">hello hello 方法的第二個我們剛才加入取代 hello**文件**在 hello 版的 hello 與 Azure Cosmos DB**文件**hello 從傳入**ItemController**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="37bf1-289">新增下列 toohello hello **ItemController**類別。</span><span class="sxs-lookup"><span data-stu-id="37bf1-289">Add hello following toohello **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="37bf1-290">hello 第一個方法會處理 hello Http GET，hello 使用者按一下時 hello**編輯**連結從 hello**索引**檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="37bf1-291">此方法會提取[**文件**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx)從 Azure Cosmos 資料庫並將其傳遞 toohello**編輯**檢視。</span><span class="sxs-lookup"><span data-stu-id="37bf1-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="37bf1-292">hello**編輯**檢視然後將執行 Http POST toohello **IndexController**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="37bf1-293">我們加入了控制代碼傳遞更新的 hello 物件 tooAzure Cosmos DB toobe hello 第二個方法會保存在 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="37bf1-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="37bf1-294">這就是它，是我們需要 toorun 我們的應用程式的所有項目，清單不完整**項目**，加入新**項目**，並編輯**項目**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="37bf1-295"><a name="_Toc395637773"></a>步驟 6： 在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="37bf1-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="37bf1-296">tootest hello 應用程式在本機電腦，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="37bf1-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="37bf1-297">在 Visual Studio 中偵錯模式 toobuild hello 應用程式中按 F5。</span><span class="sxs-lookup"><span data-stu-id="37bf1-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="37bf1-298">它應該建置 hello 應用程式，並啟動我們先前看過的 hello 空白格線頁的瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="37bf1-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Hello todo 清單 web 應用程式建立此資料庫的教學課程的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="37bf1-300">按一下 hello**新建**連結並新增值 toohello**名稱**和**描述**欄位。</span><span class="sxs-lookup"><span data-stu-id="37bf1-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="37bf1-301">保留 hello**已完成**核取方塊取消選取 新否則 hello**項目**將加入已完成狀態中，而且不會出現在 hello 初始清單上。</span><span class="sxs-lookup"><span data-stu-id="37bf1-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Hello 建立檢視的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="37bf1-303">按一下**建立**而重新導向後 toohello**索引**檢視和您**項目**hello 清單中會出現。</span><span class="sxs-lookup"><span data-stu-id="37bf1-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Hello 索引檢視的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="37bf1-305">一些其他覺得可用 tooadd**項目**tooyour todo 清單。</span><span class="sxs-lookup"><span data-stu-id="37bf1-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="37bf1-306">按一下**編輯**下一步 tooan**項目**hello 清單也會採取 toohello**編輯**檢視您可以在其中更新任何屬性的物件，包括 hello **完成**旗標。</span><span class="sxs-lookup"><span data-stu-id="37bf1-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="37bf1-307">如果您將標示 hello**完成**旗標，然後按一下**儲存**，hello**項目**hello 未完成的工作清單中已經移除了。</span><span class="sxs-lookup"><span data-stu-id="37bf1-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Hello 勾選 hello 已完成方塊索引檢視的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="37bf1-309">一旦測試過 hello 應用程式，請按 Ctrl + F5 toostop 偵錯 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="37bf1-310">您已準備好 toodeploy ！</span><span class="sxs-lookup"><span data-stu-id="37bf1-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="37bf1-311"><a name="_Toc395637774"></a>步驟 7： 部署的 hello 應用程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="37bf1-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="37bf1-312">既然您已擁有 hello 完整的應用程式可以使用 Azure Cosmos DB 正常運作我們 toodeploy 此 web 應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="37bf1-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="37bf1-313">中的 hello 專案上按一下滑鼠右鍵 toopublish 所有您需要 toodo 這個應用程式是**方案總管 中**按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Hello 方案總管 中的 發佈 選項的螢幕擷取畫面](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="37bf1-315">在 hello**發行**對話方塊中，按一下  **Microsoft Azure App Service**，然後選取**建立新**toocreate 應用程式服務的設定檔，或是按一下**選取現有**toouse 現有的設定檔。</span><span class="sxs-lookup"><span data-stu-id="37bf1-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Visual Studio 中的 [發佈] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="37bf1-317">如果您有現有的 Azure App Service 設定檔，請輸入您的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="37bf1-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="37bf1-318">使用 hello**檢視**篩選 toosort 由資源群組或資源類型，然後選取您的 Azure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="37bf1-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Visual Studio 中的 [App Service] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="37bf1-320">toocreate 新的 Azure 應用程式服務設定檔中，按一下**新建**在 hello**發行** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="37bf1-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="37bf1-321">在 hello**建立 App Service**  對話方塊中，輸入您的 Web 應用程式名稱和適當的訂用帳戶、 資源群組和應用程式服務方案，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="37bf1-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Visual Studio 中的 [建立 App Service] 對話方塊](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="37bf1-323">幾秒後，Visual Studio 便會發佈 Web 應用程式並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！</span><span class="sxs-lookup"><span data-stu-id="37bf1-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="37bf1-324"><a name="_Toc395637775"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="37bf1-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="37bf1-325">恭喜！</span><span class="sxs-lookup"><span data-stu-id="37bf1-325">Congratulations!</span></span> <span data-ttu-id="37bf1-326">您只要建置您的第一個 ASP.NET MVC web 應用程式使用 Azure Cosmos DB 並發佈它 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="37bf1-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="37bf1-327">hello hello 完成應用程式，包括 hello 詳細資料的原始碼和刪除功能未包含在此教學課程可以下載或複製從[GitHub][GitHub]。</span><span class="sxs-lookup"><span data-stu-id="37bf1-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="37bf1-328">因此如果您想要加入該 tooyour 應用程式中，抓取 hello 程式碼，並將它加入 toothis 應用程式。</span><span class="sxs-lookup"><span data-stu-id="37bf1-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="37bf1-329">tooadd 額外的功能 tooyour 應用程式中，檢閱 hello Api 可在 hello [Azure Cosmos DB.NET 程式庫](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)感覺可用 toocontribute toohello Azure Cosmos DB.NET 程式庫上[GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="37bf1-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
