---
title: "aaaGet 入門 API 應用程式和應用程式服務中的 ASP.NET |Microsoft 文件"
description: "了解如何 toocreate，部署和使用 Visual Studio 2015 使用 Azure 應用程式服務，ASP.NET 應用程式開發介面應用程式。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="a3436-103">在 Azure App Service 中開始使用 API Apps、ASP.NET 和 Swagger</span><span class="sxs-lookup"><span data-stu-id="a3436-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="a3436-104">這是 hello 第一次在一系列的說明如何 toouse 功能的 Azure 應用程式服務的教學課程，是為了開發和裝載 RESTful Api。</span><span class="sxs-lookup"><span data-stu-id="a3436-104">This is hello first in a series of tutorials that show how toouse features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="a3436-105">本教學課程涵蓋 Swagger 格式 API 中繼資料的支援。</span><span class="sxs-lookup"><span data-stu-id="a3436-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="a3436-106">您將了解：</span><span class="sxs-lookup"><span data-stu-id="a3436-106">You'll learn:</span></span>

* <span data-ttu-id="a3436-107">如何 toocreate 和部署[API apps](app-service-api-apps-why-best-platform.md)使用內建於 Visual Studio 2015 工具的 Azure App Service 中。</span><span class="sxs-lookup"><span data-stu-id="a3436-107">How toocreate and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="a3436-108">如何使用 hello tooautomate API 探索 Swashbuckle NuGet 封裝 toodynamically 產生 Swagger API 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a3436-108">How tooautomate API discovery by using hello Swashbuckle NuGet package toodynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="a3436-109">Toouse Swagger API 中繼資料 tooautomatically 產生 API 應用程式的用戶端程式碼的方式。</span><span class="sxs-lookup"><span data-stu-id="a3436-109">How toouse Swagger API metadata tooautomatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="a3436-110">範例應用程式概觀</span><span class="sxs-lookup"><span data-stu-id="a3436-110">Sample application overview</span></span>
<span data-ttu-id="a3436-111">在本教學課程中，您會使用簡單的待辦事項清單範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="a3436-112">hello 應用程式必須在單一頁面應用程式 (SPA) 的前端、 ASP.NET Web API 的中介層和 ASP.NET Web API 的資料層。</span><span class="sxs-lookup"><span data-stu-id="a3436-112">hello application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![API Apps 範例應用程式圖表](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="a3436-114">以下是 hello 的螢幕擷取畫面[AngularJS](https://angularjs.org/)前端。</span><span class="sxs-lookup"><span data-stu-id="a3436-114">Here's a screen shot of hello [AngularJS](https://angularjs.org/) front end.</span></span>

![API 的應用程式範例應用程式 toodo 清單](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="a3436-116">hello Visual Studio 方案包含三個專案：</span><span class="sxs-lookup"><span data-stu-id="a3436-116">hello Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="a3436-117">**ToDoListAngular** -hello 前端： 呼叫 hello 中介層 AngularJS SPA。</span><span class="sxs-lookup"><span data-stu-id="a3436-117">**ToDoListAngular** - hello front end: an AngularJS SPA that calls hello middle tier.</span></span>
* <span data-ttu-id="a3436-118">**ToDoListAPI** -hello 中介層： 呼叫 hello 資料層 tooperform 待辦項目上的 CRUD 作業的 ASP.NET Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="a3436-118">**ToDoListAPI** - hello middle tier: an ASP.NET Web API project that calls hello data tier tooperform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="a3436-119">**ToDoListDataAPI** -hello 資料層： 執行待辦項目上的 CRUD 作業的 ASP.NET Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="a3436-119">**ToDoListDataAPI** - hello data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="a3436-120">hello 三層式架構是許多架構，您可以使用 API Apps 實作用於此處僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="a3436-120">hello three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="a3436-121">每個階層中的 hello 程式碼很簡單，可能 toodemonstrate API 應用程式功能;例如，hello 資料層會使用伺服器記憶體，而非資料庫做為其持續性機制。</span><span class="sxs-lookup"><span data-stu-id="a3436-121">hello code in each tier is as simple as possible toodemonstrate API Apps features; for example, hello data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="a3436-122">完成本教學課程，您必須設定 hello 兩個 Web API 專案和應用程式服務 API 應用程式中的 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="a3436-122">On completing this tutorial, you'll have hello two Web API projects up and running in hello cloud in App Service API apps.</span></span>

<span data-ttu-id="a3436-123">hello hello 數列中的下一個教學課程部署 hello SPA 前端 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="a3436-123">hello next tutorial in hello series deploys hello SPA front end toohello cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3436-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="a3436-124">Prerequisites</span></span>
* <span data-ttu-id="a3436-125">ASP.NET Web API-hello 教學課程的指示假設您已經有基本知識的方式使用 ASP.NET toowork [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="a3436-125">ASP.NET Web API - hello tutorial instructions assume you have a basic knowledge of how toowork with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="a3436-126">Azure 帳戶 - 您可以[申請免費 Azure 帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)或[啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="a3436-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="a3436-127">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務已啟動，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="a3436-127">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="a3436-128">如此，您可以在 App Service 中立即建立短期的入門應用程式 — **不需信用卡**，不需任何承諾。</span><span class="sxs-lookup"><span data-stu-id="a3436-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="a3436-129">Visual Studio 2015 hello [Azure SDK for.NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK 會安裝 Visual Studio 2015 的自動如果還沒有。</span><span class="sxs-lookup"><span data-stu-id="a3436-129">Visual Studio 2015 with hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - hello SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="a3436-130">在 Visual Studio 中，按一下 [說明] -> [關於 Microsoft Visual Studio]，並確定您已安裝 "Azure App Service Tools v2.9.1" 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a3436-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Azure App Tools 版本](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="a3436-132">根據多少 hello SDK 相依性的您已經在電腦上，安裝 hello SDK 可能需要很長的時間，從 tooa 半小時或更多幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="a3436-132">Depending on how many of hello SDK dependencies you already have on your machine, installing hello SDK could take a long time, from several minutes tooa half hour or more.</span></span>
    > 
    > 

## <a name="download-hello-sample-application"></a><span data-ttu-id="a3436-133">下載 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="a3436-133">Download hello sample application</span></span>
1. <span data-ttu-id="a3436-134">下載 hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list)儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a3436-134">Download hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="a3436-135">您可以按一下 hello **Download ZIP**在本機電腦上的按鈕或再製 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a3436-135">You can click hello **Download ZIP** button or clone hello repository on your local machine.</span></span>
2. <span data-ttu-id="a3436-136">開啟 Visual Studio 2015 或 2013 hello ToDoList 方案。</span><span class="sxs-lookup"><span data-stu-id="a3436-136">Open hello ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="a3436-137">您將需要 tootrust 每個解決方案。</span><span class="sxs-lookup"><span data-stu-id="a3436-137">You will need tootrust each solution.</span></span>
         <span data-ttu-id="a3436-138">![安全性警告](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="a3436-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="a3436-139">建立 hello 解決方案 （CTRL + SHIFT + B） toorestore hello NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="a3436-139">Build hello solution (CTRL + SHIFT + B)  toorestore hello NuGet packages.</span></span>
   
    <span data-ttu-id="a3436-140">如果您在部署之前，您會想 toosee hello 應用程式在作業中的，您可以在本機執行。</span><span class="sxs-lookup"><span data-stu-id="a3436-140">If you want toosee hello application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="a3436-141">請確定 ToDoListDataAPI 您的啟始專案和方案執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="a3436-141">Make sure that ToDoListDataAPI is your startup project and run hello solution.</span></span> <span data-ttu-id="a3436-142">在您的瀏覽器中，您應該預期 toosee HTTP 403 錯誤。</span><span class="sxs-lookup"><span data-stu-id="a3436-142">You should expect toosee a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="a3436-143">使用 Swagger API 中繼資料和 UI</span><span class="sxs-lookup"><span data-stu-id="a3436-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="a3436-144">Azure App Service 內建支援 [Swagger 2.0](http://swagger.io/) API 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a3436-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="a3436-145">每個應用程式開發介面應用程式可以指定之 URL 端點的 Swagger JSON 格式傳回 hello API 的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a3436-145">Each API app can specify a URL endpoint that returns metadata for hello API in Swagger JSON format.</span></span> <span data-ttu-id="a3436-146">hello 傳回來自該端點的中繼資料可以是使用 toogenerate 用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="a3436-146">hello metadata returned from that endpoint can be used toogenerate client code.</span></span>

<span data-ttu-id="a3436-147">ASP.NET Web API 專案可以動態地產生 Swagger 中繼資料使用 hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="a3436-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="a3436-148">hello Swashbuckle NuGet 封裝已安裝在您下載的 hello ToDoListDataAPI 和 ToDoListAPI 專案中。</span><span class="sxs-lookup"><span data-stu-id="a3436-148">hello Swashbuckle NuGet package is already installed in hello ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="a3436-149">在本節中的 hello 教學課程，您查看產生的 hello Swagger 2.0 中繼資料，，然後再次嘗試測試 hello Swagger 中繼資料為基礎的 UI。</span><span class="sxs-lookup"><span data-stu-id="a3436-149">In this section of hello tutorial, you look at hello generated Swagger 2.0 metadata, and then you try out a test UI that is based on hello Swagger metadata.</span></span>

1. <span data-ttu-id="a3436-150">設定 hello ToDoListDataAPI 專案 (**不**hello ToDoListAPI 專案) 為 hello 啟始專案。</span><span class="sxs-lookup"><span data-stu-id="a3436-150">Set hello ToDoListDataAPI project (**not** hello ToDoListAPI project) as hello startup project.</span></span>
   
    ![將 ToDoDataAPI 設定為啟始專案](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="a3436-152">按 F5 或按一下**偵錯 > 開始偵錯**toorun hello 專案在偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="a3436-152">Press F5 or click **Debug > Start Debugging** toorun hello project in debug mode.</span></span>
   
    <span data-ttu-id="a3436-153">hello 瀏覽器會開啟並顯示 hello HTTP 403 錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="a3436-153">hello browser opens and shows hello HTTP 403 error page.</span></span>
3. <span data-ttu-id="a3436-154">在您的瀏覽器網址列中加入`swagger/docs/v1`toohello hello 列，然後按下 Return 結束。</span><span class="sxs-lookup"><span data-stu-id="a3436-154">In your browser address bar, add `swagger/docs/v1` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="a3436-155">(URL 是的 hello `http://localhost:45914/swagger/docs/v1`。)</span><span class="sxs-lookup"><span data-stu-id="a3436-155">(hello URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="a3436-156">這是 hello Swashbuckle tooreturn Swagger 2.0 JSON 中繼資料用於 hello 應用程式開發介面的預設 URL。</span><span class="sxs-lookup"><span data-stu-id="a3436-156">This is hello default URL used by Swashbuckle tooreturn Swagger 2.0 JSON metadata for hello API.</span></span>
   
    <span data-ttu-id="a3436-157">如果您使用 Internet Explorer，hello 瀏覽器會提示您 toodownload *v1.json*檔案。</span><span class="sxs-lookup"><span data-stu-id="a3436-157">If you're using Internet Explorer, hello browser prompts you toodownload a *v1.json* file.</span></span>
   
    ![在 IE 中下載 JSON 中繼資料](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="a3436-159">如果您使用 Chrome、 Firefox 或邊緣 hello 瀏覽器會顯示 hello JSON hello 瀏覽器視窗中。</span><span class="sxs-lookup"><span data-stu-id="a3436-159">If you're using Chrome, Firefox, or Edge, hello browser displays hello JSON in hello browser window.</span></span> <span data-ttu-id="a3436-160">處理 JSON 的方式，不同的瀏覽器和瀏覽器視窗可能看起來不完全與 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="a3436-160">Different browsers handle JSON differently, and your browser window may not look exactly like hello example.</span></span>
   
    ![Chrome 中的 JSON 中繼資料](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="a3436-162">hello 下列範例顯示 hello hello API，hello Swagger 中繼資料的第一個區段與 hello 的 hello 定義 Get 方法。</span><span class="sxs-lookup"><span data-stu-id="a3436-162">hello following sample shows hello first section of hello Swagger metadata for hello API, with hello definition for hello Get method.</span></span> <span data-ttu-id="a3436-163">此中繼資料是哪些磁碟機 hello Swagger UI 和使用它在稍後的章節的 hello 教學課程 tooautomatically 中 hello 下列步驟，使用產生的用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="a3436-163">This metadata is what drives hello Swagger UI that you use in hello following steps, and you use it in a later section of hello tutorial tooautomatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="a3436-164">關閉 hello 瀏覽器，並停止 Visual Studio 偵錯。</span><span class="sxs-lookup"><span data-stu-id="a3436-164">Close hello browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="a3436-165">在專案中 hello ToDoListDataAPI**方案總管 中**，開啟 hello *App_Start\SwaggerConfig.cs*檔案，然後向下 tooline 174 並取消註解下列程式碼的 hello 捲軸。</span><span class="sxs-lookup"><span data-stu-id="a3436-165">In hello ToDoListDataAPI project in **Solution Explorer**, open hello *App_Start\SwaggerConfig.cs* file, then scroll down tooline 174 and uncomment hello following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="a3436-166">hello *SwaggerConfig.cs*當您安裝在專案中的 hello Swashbuckle 封裝，建立檔案。</span><span class="sxs-lookup"><span data-stu-id="a3436-166">hello *SwaggerConfig.cs* file is created when you install hello Swashbuckle package in a project.</span></span> <span data-ttu-id="a3436-167">hello 檔案提供數種方式 tooconfigure Swashbuckle。</span><span class="sxs-lookup"><span data-stu-id="a3436-167">hello file provides a number of ways tooconfigure Swashbuckle.</span></span>
   
    <span data-ttu-id="a3436-168">已取消註解 Swagger UI 中用於 hello 遵循的步驟啟用 hello hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="a3436-168">hello code you've uncommented enables hello Swagger UI that you use in hello following steps.</span></span> <span data-ttu-id="a3436-169">當您使用 hello API 應用程式專案範本建立 Web API 專案時，這段程式碼會標記為註解預設基於安全性考量。</span><span class="sxs-lookup"><span data-stu-id="a3436-169">When you create a Web API project by using hello API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="a3436-170">再次執行 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a3436-170">Run hello project again.</span></span>
7. <span data-ttu-id="a3436-171">在您的瀏覽器網址列中加入`swagger`toohello hello 列，然後按下 Return 結束。</span><span class="sxs-lookup"><span data-stu-id="a3436-171">In your browser address bar, add `swagger` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="a3436-172">(URL 是的 hello `http://localhost:45914/swagger`。)</span><span class="sxs-lookup"><span data-stu-id="a3436-172">(hello URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="a3436-173">Hello Swagger UI 頁面出現時，按一下**ToDoList** toosee hello 可供使用的方法。</span><span class="sxs-lookup"><span data-stu-id="a3436-173">When hello Swagger UI page appears, click **ToDoList** toosee hello methods available.</span></span>
   
    ![Swagger UI 可用的方法](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="a3436-175">請先按一下 hello**取得**hello 清單中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a3436-175">Click hello first **Get** button in hello list.</span></span>
10. <span data-ttu-id="a3436-176">在 hello**參數**區段中，輸入星號做為 hello hello 值`owner`參數，然後再按一下**現在就試試看**。</span><span class="sxs-lookup"><span data-stu-id="a3436-176">In hello **Parameters** section, enter an asterisk as hello value of hello `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="a3436-177">當您在之後的教學課程中加入驗證時，hello 中介層將提供 hello 實際的使用者識別碼 toohello 資料層。</span><span class="sxs-lookup"><span data-stu-id="a3436-177">When you add authentication in later tutorials, hello middle tier will provide hello actual user ID toohello data tier.</span></span> <span data-ttu-id="a3436-178">現在，所有工作將會都有星號做為其擁有者識別碼而 hello 應用程式執行時不會啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="a3436-178">For now, all tasks will have asterisk as their owner ID while hello application runs without authentication enabled.</span></span>
    
    ![Swagger UI 試用](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="a3436-180">hello Swagger UI 呼叫 hello ToDoList Get 方法，並顯示 hello 回應程式碼和 JSON 結果。</span><span class="sxs-lookup"><span data-stu-id="a3436-180">hello Swagger UI calls hello ToDoList Get method and displays hello response code and JSON results.</span></span>
    
    ![Swagger UI 試用結果](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="a3436-182">按一下**Post**，然後按一下hello 下的**模型結構描述**。</span><span class="sxs-lookup"><span data-stu-id="a3436-182">Click **Post**, and then click hello box under **Model Schema**.</span></span>
    
    <span data-ttu-id="a3436-183">按一下 hello 模型結構描述 prefills hello 輸入的方塊，您可以指定 hello hello Post 方法的參數值。</span><span class="sxs-lookup"><span data-stu-id="a3436-183">Clicking hello model schema prefills hello input box where you can specify hello parameter value for hello Post method.</span></span> <span data-ttu-id="a3436-184">（如果這無法在 Internet Explorer 中運作，使用不同的瀏覽器或 hello 下一個步驟中手動輸入 hello 參數值）。</span><span class="sxs-lookup"><span data-stu-id="a3436-184">(If this doesn't work in Internet Explorer, use a different browser or enter hello parameter value manually in hello next step.)</span></span>  
    
    ![Swagger UI 試用文章](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="a3436-186">在 hello 變更 hello JSON`todo`參數輸入方塊，讓它看起來像下列範例，hello 或取代您自己的描述文字：</span><span class="sxs-lookup"><span data-stu-id="a3436-186">Change hello JSON in hello `todo` parameter input box so that it looks like hello following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="a3436-187">按一下 [立即試用] 。</span><span class="sxs-lookup"><span data-stu-id="a3436-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="a3436-188">hello ToDoList 應用程式開發介面會傳回 HTTP 204 回應碼之表示成功。</span><span class="sxs-lookup"><span data-stu-id="a3436-188">hello ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="a3436-189">請先按一下 hello**取得**按鈕，然後在該區段中的 hello 頁面 hello**現在就試試看** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a3436-189">Click hello first **Get** button, and then in that section of hello page click hello **Try it out** button.</span></span>
    
    <span data-ttu-id="a3436-190">Get 方法回應 hello 現在包含 hello 新 toodo 項目。</span><span class="sxs-lookup"><span data-stu-id="a3436-190">hello Get method response now includes hello new toodo item.</span></span>
15. <span data-ttu-id="a3436-191">選擇性： 也 hello Put、 Delete，再取得識別碼的方法。</span><span class="sxs-lookup"><span data-stu-id="a3436-191">Optional: Try also hello Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="a3436-192">關閉 hello 瀏覽器，並停止 Visual Studio 偵錯。</span><span class="sxs-lookup"><span data-stu-id="a3436-192">Close hello browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="a3436-193">Swashbuckle 可搭配任何 ASP.NET Web API 專案使用。</span><span class="sxs-lookup"><span data-stu-id="a3436-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="a3436-194">如果您想 tooadd Swagger 中繼資料產生 tooan 現有專案時，只安裝 hello Swashbuckle 封裝。</span><span class="sxs-lookup"><span data-stu-id="a3436-194">If you want tooadd Swagger metadata generation tooan existing project, just install hello Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="a3436-195">Swagger 中繼資料包含每個 API 作業的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="a3436-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="a3436-196">根據預設，Swashbuckle 可能會為 Web API 控制器方法產生重複的 Swagger 作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="a3436-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="a3436-197">如果控制器有多載的 HTTP 方法，例如 `Get()` 和 `Get(id)`，就會發生此情況。</span><span class="sxs-lookup"><span data-stu-id="a3436-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="a3436-198">如需 toohandle 的多載，請參閱[自訂 Swashbuckle 產生應用程式開發介面定義](app-service-api-dotnet-swashbuckle-customize.md)。</span><span class="sxs-lookup"><span data-stu-id="a3436-198">For information about how toohandle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="a3436-199">如果您在 Visual Studio 中建立 Web API 專案使用 hello Azure API 應用程式範本時，會產生的唯一作業識別碼的程式碼會自動加入 toohello *SwaggerConfig.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="a3436-199">If you create a Web API project in Visual Studio by using hello Azure API App template, code that generates unique operation IDs is automatically added toohello *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="a3436-200"><a id="createapiapp"></a>在 Azure 中建立 API 應用程式和部署程式碼 tooit</span><span class="sxs-lookup"><span data-stu-id="a3436-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code tooit</span></span>
<span data-ttu-id="a3436-201">在本節中，您可以使用 Azure 工具已整合至 Visual Studio hello**發行 Web**精靈 toocreate 新 API 的應用程式在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="a3436-201">In this section, you use Azure tools that are integrated into hello Visual Studio **Publish Web** wizard toocreate a new API app in Azure.</span></span> <span data-ttu-id="a3436-202">然後您部署 hello ToDoListDataAPI 專案 toohello 新 API 的應用程式，然後執行 hello Swagger UI 來呼叫 hello API。</span><span class="sxs-lookup"><span data-stu-id="a3436-202">Then you deploy hello ToDoListDataAPI project toohello new API app and call hello API by running hello Swagger UI.</span></span>

1. <span data-ttu-id="a3436-203">在**方案總管 中**hello ToDoListDataAPI 專案中，以滑鼠右鍵按一下，然後按**發行**。</span><span class="sxs-lookup"><span data-stu-id="a3436-203">In **Solution Explorer**, right-click hello ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![在 Visual Studio 中按一下 [發佈]](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="a3436-205">在 [hello**設定檔**hello 的步驟**發行 Web**精靈] 中，按一下**Microsoft Azure App Service**。</span><span class="sxs-lookup"><span data-stu-id="a3436-205">In hello **Profile** step of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![在 [發佈 Web] 中按一下 [Azure App Service]](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="a3436-207">登入 tooyour Azure 帳戶，如果您有不這樣做，或重新整理您的認證，如果過期。</span><span class="sxs-lookup"><span data-stu-id="a3436-207">Sign in tooyour Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="a3436-208">在 [hello 應用程式服務] 對話方塊中選擇 hello Azure**訂用帳戶**toouse，然後再按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a3436-208">In hello App Service dialog box, choose hello Azure **Subscription** you want toouse, and then click **New**.</span></span>
   
    ![在 [App Service] 對話方塊中按一下 [新增]](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="a3436-210">hello**主控** 索引標籤的 hello**建立 App Service**  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="a3436-210">hello **Hosting** tab of hello **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="a3436-211">因為您要部署已安裝的 Swashbuckle Web API 專案，Visual Studio 會假設您想 toocreate API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want toocreate an API App.</span></span> <span data-ttu-id="a3436-212">這會由 hello **API 應用程式名稱**標題，並由 hello 事實該 hello**變更類型**下拉式清單設定得**API 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a3436-212">This is indicated by hello **API App Name** title and by hello fact that hello **Change Type** drop-down list is set too**API App**.</span></span>
   
    ![[App Service] 對話方塊中的應用程式類型](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="a3436-214">輸入**API 應用程式名稱**，都是唯一的 hello *.azurewebsites.net*網域。</span><span class="sxs-lookup"><span data-stu-id="a3436-214">Enter an **API App Name** that is unique in hello *azurewebsites.net* domain.</span></span> <span data-ttu-id="a3436-215">您可以接受 hello Visual Studio 所建議的預設名稱。</span><span class="sxs-lookup"><span data-stu-id="a3436-215">You can accept hello default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="a3436-216">如果您輸入其他人已使用的名稱，您會看到紅色驚嘆號 toohello 權限。</span><span class="sxs-lookup"><span data-stu-id="a3436-216">If you enter a name that someone else has already used, you see a red exclamation mark toohello right.</span></span>
   
    <span data-ttu-id="a3436-217">hello hello API 應用程式的 URL 會`{API app name}.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="a3436-217">hello URL of hello API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="a3436-218">在 hello**資源群組**下拉式清單中，按一下**新增**，如果您想要的話，然後輸入"ToDoListGroup 」 或另一個名稱。</span><span class="sxs-lookup"><span data-stu-id="a3436-218">In hello **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="a3436-219">資源群組是 Azure 資源的集合，例如 API 應用程式、資料庫、VM 等等。</span><span class="sxs-lookup"><span data-stu-id="a3436-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="a3436-220">此教學課程中，它會是最佳 toocreate 新的資源群組，因為，能讓您輕鬆 toodelete 所有 hello hello 教學課程中建立的 Azure 資源的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a3436-220">For this tutorial, it's best toocreate a new resource group because that makes it easy toodelete in one step all hello Azure resources that you create for hello tutorial.</span></span>
   
    <span data-ttu-id="a3436-221">此方塊可讓您選取現有的[資源群組](../azure-resource-manager/resource-group-overview.md)，或藉由輸入與您的訂用帳戶中任何現有的資源群組不同的名稱，以建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a3436-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="a3436-222">按一下 hello**新增**按鈕的下一個 toohello **App Service 方案**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="a3436-222">Click hello **New** button next toohello **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="a3436-223">hello 螢幕擷取畫面顯示範例值**API 應用程式名稱**，**訂用帳戶**，和**資源群組**-您的值將會不同。</span><span class="sxs-lookup"><span data-stu-id="a3436-223">hello screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![建立 App Service 對話方塊](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="a3436-225">Hello 步驟中，您會建立 App Service 方案 hello 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="a3436-225">In hello following steps you create an App Service plan for hello new resource group.</span></span> <span data-ttu-id="a3436-226">App Service 方案指定 hello 您 API 應用程式執行的計算資源。</span><span class="sxs-lookup"><span data-stu-id="a3436-226">An App Service plan specifies hello compute resources that your API app runs on.</span></span> <span data-ttu-id="a3436-227">比方說，如果您選擇 hello 免費層，您 API 應用程式會執行共用的 Vm 上的部分付費層次中執行專用的 Vm 上時。</span><span class="sxs-lookup"><span data-stu-id="a3436-227">For example, if you choose hello free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="a3436-228">如需 App Service 方案的詳細資訊，請參閱 [App Service 方案概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a3436-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="a3436-229">在 [hello**設定 App Service 方案**] 對話方塊中，輸入"ToDoListPlan 」 或另一個名稱，如果您偏好。</span><span class="sxs-lookup"><span data-stu-id="a3436-229">In hello **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="a3436-230">在 hello**位置**下拉式清單中，選擇最接近 tooyou hello 位置。</span><span class="sxs-lookup"><span data-stu-id="a3436-230">In hello **Location** drop-down list, choose hello location that is closest tooyou.</span></span>
   
    <span data-ttu-id="a3436-231">這個設定會指定應用程式將執行所在的 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="a3436-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="a3436-232">選擇位置關閉 tooyou toominimize[延遲](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090)。</span><span class="sxs-lookup"><span data-stu-id="a3436-232">Choose a location close tooyou toominimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="a3436-233">在 hello**大小**下拉式清單中，按一下**免費**。</span><span class="sxs-lookup"><span data-stu-id="a3436-233">In hello **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="a3436-234">本教學課程，hello 免費定價層會提供足夠的效能。</span><span class="sxs-lookup"><span data-stu-id="a3436-234">For this tutorial, hello free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="a3436-235">在 [hello**設定 App Service 方案**] 對話方塊中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a3436-235">In hello **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![在 [設定 App Service 方案] 中按一下 [確定]](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="a3436-237">在 hello**建立 App Service**對話方塊中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="a3436-237">In hello **Create App Service** dialog box, click **Create**.</span></span>
    
    ![在 [建立 App Service] 對話方塊中按一下 [建立]](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="a3436-239">Visual Studio 建立 hello API 應用程式和發行設定檔，其中包含所有所需的 hello hello API 應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="a3436-239">Visual Studio creates hello API app and a publish profile that has all of hello required settings for hello API app.</span></span> <span data-ttu-id="a3436-240">然後它會開啟 hello**發行 Web**精靈中，您將使用此 toodeploy hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a3436-240">Then it opens hello **Publish Web** wizard, which you'll use toodeploy hello project.</span></span>
    
    <span data-ttu-id="a3436-241">hello**發行 Web**精靈 隨即開啟上 hello**連接** 索引標籤 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="a3436-241">hello **Publish Web** wizard opens on hello **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="a3436-242">在 hello**連接**索引標籤上，hello**伺服器**和**站台名稱**設定點 tooyour API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-242">On hello **Connection** tab, hello **Server** and **Site name** settings point tooyour API app.</span></span> <span data-ttu-id="a3436-243">hello**使用者名**和**密碼**會為您建立 Azure 的部署認證。</span><span class="sxs-lookup"><span data-stu-id="a3436-243">hello **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="a3436-244">部署之後，Visual Studio 會開啟瀏覽器 toohello**目的地 URL** (也就是說 hello 唯一目的**目的地 URL**)。</span><span class="sxs-lookup"><span data-stu-id="a3436-244">After deployment, Visual Studio opens a browser toohello **Destination URL** (that's hello only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="a3436-245">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a3436-245">Click **Next**.</span></span>
    
    ![在 [發佈 Web] 的 [連線] 索引標籤中按 [下一步]](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="a3436-247">hello 下一個索引標籤為 hello**設定** 索引標籤 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="a3436-247">hello next tab is hello **Settings** tab (shown below).</span></span> <span data-ttu-id="a3436-248">這裡您可以變更 hello 組建組態 索引標籤 toodeploy 的偵錯組建[遠端偵錯](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)。</span><span class="sxs-lookup"><span data-stu-id="a3436-248">Here you can change hello build configuration tab toodeploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="a3436-249">hello 索引標籤也提供數個**檔案發行選項**:</span><span class="sxs-lookup"><span data-stu-id="a3436-249">hello tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="a3436-250">在目的地移除多餘的檔案</span><span class="sxs-lookup"><span data-stu-id="a3436-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="a3436-251">在發行期間預先編譯</span><span class="sxs-lookup"><span data-stu-id="a3436-251">Precompile during publishing</span></span>
    * <span data-ttu-id="a3436-252">排除 hello App_Data 資料夾中的檔案</span><span class="sxs-lookup"><span data-stu-id="a3436-252">Exclude files from hello App_Data folder</span></span>
    
    <span data-ttu-id="a3436-253">在本教學課程中，您不需要這些。</span><span class="sxs-lookup"><span data-stu-id="a3436-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="a3436-254">如需它們執行了哪些作業的說明，請參閱 [操作說明：在 Visual Studio 中使用單鍵發佈來部署 Web 專案](https://msdn.microsoft.com/library/dd465337.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a3436-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="a3436-255">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a3436-255">Click **Next**.</span></span>
    
    ![在 [發佈 Web] 的 [設定] 索引標籤中按 [下一步]](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="a3436-257">接下來是 hello**預覽** 索引標籤 （如下所示），它將提供您哪些檔案即將從您的專案 toohello API 應用程式複製 toobe 機會 toosee。</span><span class="sxs-lookup"><span data-stu-id="a3436-257">Next is hello **Preview** tab (shown below), which gives you an opportunity toosee what files are going toobe copied from your project toohello API app.</span></span> <span data-ttu-id="a3436-258">當您要部署專案 tooan API 的應用程式，您已部署 tooearlier 時，只變更的檔案都會複製。</span><span class="sxs-lookup"><span data-stu-id="a3436-258">When you're deploying a project tooan API app that you already deployed tooearlier, only changed files are copied.</span></span> <span data-ttu-id="a3436-259">如果您想 toosee 複製內容的清單，您可以按一下 hello**啟動預覽** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a3436-259">If you want toosee a list of what will be copied, you can click hello **Start Preview** button.</span></span>
15. <span data-ttu-id="a3436-260">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="a3436-260">Click **Publish**.</span></span>
    
    ![在 [發佈 Web] 的 [預覽] 索引標籤中按一下 [發佈]](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="a3436-262">Visual Studio 部署 hello ToDoListDataAPI 專案 toohello 新 API 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-262">Visual Studio deploys hello ToDoListDataAPI project toohello new API app.</span></span> <span data-ttu-id="a3436-263">hello**輸出**視窗會記錄成功的部署，而且 」 已成功建立"頁面會出現在瀏覽器視窗開啟 toohello hello API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="a3436-263">hello **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened toohello URL of hello API app.</span></span>
    
    ![成功部署的輸出視窗](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![新的 API 應用程式已成功建立頁面](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="a3436-266">在 hello 瀏覽器的網址列中加入"swagger"toohello URL，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="a3436-266">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="a3436-267">(URL 是的 hello `http://{apiappname}.azurewebsites.net/swagger`。)</span><span class="sxs-lookup"><span data-stu-id="a3436-267">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="a3436-268">hello 瀏覽器會顯示的 hello hello 雲端中執行您稍早所見相同 Swagger 的 UI，但現在它。</span><span class="sxs-lookup"><span data-stu-id="a3436-268">hello browser displays hello same Swagger UI that you saw earlier, but now it's running in hello cloud.</span></span> <span data-ttu-id="a3436-269">試用 hello Get 方法，而且您會看到您正在回復 toohello 預設 2 待辦項目。</span><span class="sxs-lookup"><span data-stu-id="a3436-269">Try out hello Get method, and you see that you're back toohello default 2 to-do items.</span></span> <span data-ttu-id="a3436-270">hello 您稍早所做的變更已儲存在記憶體中 hello 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="a3436-270">hello changes you made earlier were saved in memory in hello local machine.</span></span>
17. <span data-ttu-id="a3436-271">開啟 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="a3436-271">Open hello [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="a3436-272">hello Azure 入口網站是管理 Azure 資源，例如應用程式開發介面應用程式的網頁介面。</span><span class="sxs-lookup"><span data-stu-id="a3436-272">hello Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="a3436-273">按一下 [其他服務] > [應用程式服務]。</span><span class="sxs-lookup"><span data-stu-id="a3436-273">Click **More Services > App Services**.</span></span>
    
    ![瀏覽應用程式服務](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="a3436-275">在 hello**應用程式服務**刀鋒視窗中，尋找並按一下新的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-275">In hello **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="a3436-276">(在 hello Azure 入口網站，稱為開啟 toohello 權限的 windows*刀鋒*。)</span><span class="sxs-lookup"><span data-stu-id="a3436-276">(In hello Azure portal, windows that open toohello right are called *blades*.)</span></span>
    
    ![[應用程式服務] 刀鋒視窗](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="a3436-278">有兩個刀鋒視窗會開啟。</span><span class="sxs-lookup"><span data-stu-id="a3436-278">Two blades open.</span></span> <span data-ttu-id="a3436-279">一個分頁有概觀 hello API 應用程式，並有一長串，您可以檢視和變更的設定。</span><span class="sxs-lookup"><span data-stu-id="a3436-279">One blade has an overview of hello API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="a3436-280">在 hello**設定**刀鋒視窗中，尋找 hello **API**區段，然後按一下**API 定義**。</span><span class="sxs-lookup"><span data-stu-id="a3436-280">In hello **Settings** blade, find hello **API** section and click **API Definition**.</span></span>
    
    ![[設定] 刀鋒視窗中的 API 定義](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="a3436-282">hello **API 定義**刀鋒視窗可讓您指定 hello URL 以 JSON 格式傳回 Swagger 2.0 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a3436-282">hello **API Definition** blade lets you specify hello URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="a3436-283">當 Visual Studio 建立 hello API 應用程式時，它會將 hello API 定義 URL toohello 預設值用於 Swashbuckle 產生的中繼資料更早版本，您所看到的 hello API 應用程式的基底 URL 加上`/swagger/docs/v1`。</span><span class="sxs-lookup"><span data-stu-id="a3436-283">When Visual Studio creates hello API app, it sets hello API definition URL toohello default value for Swashbuckle-generated metadata that you saw earlier, which is hello API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![API 定義 URL](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="a3436-285">當您所選取的應用程式開發介面應用程式 toogenerate 用戶端程式碼時，則 Visual Studio 會擷取 hello 中繼資料從這個 URL。</span><span class="sxs-lookup"><span data-stu-id="a3436-285">When you select an API app toogenerate client code for it, Visual Studio retrieves hello metadata from this URL.</span></span>

## <span data-ttu-id="a3436-286"><a id="codegen"></a>產生 hello 資料層的用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="a3436-286"><a id="codegen"></a> Generate client code for hello data tier</span></span>
<span data-ttu-id="a3436-287">將 Swagger 整合到 Azure API 應用程式的 hello 優點之一是自動產生程式碼。</span><span class="sxs-lookup"><span data-stu-id="a3436-287">One of hello advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="a3436-288">產生的用戶端類別會讓它更容易 toowrite 程式碼呼叫 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-288">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="a3436-289">hello ToDoListAPI 專案已經有 hello 產生用戶端程式碼，但 hello 步驟中，則會將其刪除並重新產生的 toosee toodo hello 程式碼的產生方式。</span><span class="sxs-lookup"><span data-stu-id="a3436-289">hello ToDoListAPI project already has hello generated client code, but in hello following steps you'll delete it and regenerate it toosee how toodo hello code generation.</span></span>

1. <span data-ttu-id="a3436-290">在 Visual Studio**方案總管 中**、 hello ToDoListAPI 在專案中，刪除 hello *ToDoListDataAPI*資料夾。</span><span class="sxs-lookup"><span data-stu-id="a3436-290">In Visual Studio **Solution Explorer**, in hello ToDoListAPI project, delete hello *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="a3436-291">**注意： 只有 hello 資料夾刪除，hello ToDoListDataAPI 專案。**</span><span class="sxs-lookup"><span data-stu-id="a3436-291">**Caution: Delete only hello folder, not hello ToDoListDataAPI project.**</span></span>
   
    ![刪除產生的用戶端程式碼](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="a3436-293">使用 hello 程式碼產生程序，您需透過 toogo 建立這個資料夾。</span><span class="sxs-lookup"><span data-stu-id="a3436-293">This folder was created by using hello code generation process that you're about toogo through.</span></span>
2. <span data-ttu-id="a3436-294">Hello ToDoListAPI 專案中，以滑鼠右鍵按一下，然後按一下**新增 > REST API 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="a3436-294">Right-click hello ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![在 Visual Studio 中新增 REST API 用戶端](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="a3436-296">在 hello**新增 REST API 用戶端**對話方塊中，按一下**Swagger URL**，然後按一下**選取 Azure 資產**。</span><span class="sxs-lookup"><span data-stu-id="a3436-296">In hello **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![選取 Azure 資產](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="a3436-298">在 hello **App Service**對話方塊中，展開您使用此教學課程中的 hello 資源群組並選取您的應用程式開發介面應用程式，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a3436-298">In hello **App Service** dialog box, expand hello resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![選取用於產生程式碼的 API 應用程式](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="a3436-300">請注意，當您傳回 toohello**新增 REST API 用戶端**對話方塊中，hello 文字方塊中已填入入 hello API 定義 URL 您稍早在 hello 入口網站中看到的值。</span><span class="sxs-lookup"><span data-stu-id="a3436-300">Notice that when you return toohello **Add REST API Client** dialog, hello text box has been filled in with hello API definition URL value that you saw earlier in hello portal.</span></span>
   
    ![API 定義 URL](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="a3436-302">用於產生程式碼的替代方式 tooget 中繼資料是 tooenter hello URL 直接而不是經過 hello 瀏覽對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a3436-302">An alternative way tooget metadata for code generation is tooenter hello URL directly instead of going through hello browse dialog.</span></span> <span data-ttu-id="a3436-303">如果您想 toogenerate 用戶端程式碼部署 tooAzure 之前，您無法在本機執行 hello Web API 專案提供 hello Swagger JSON 檔案，儲存 hello 檔案 toohello URL，請使用 hello 或**選取現有 Swagger 中繼資料檔案**選項。</span><span class="sxs-lookup"><span data-stu-id="a3436-303">Or if you want toogenerate client code before deploying tooAzure, you could run hello Web API project locally, go toohello URL that provides hello Swagger JSON file, save hello file, and use hello **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="a3436-304">在 hello**新增 REST API 用戶端**對話方塊中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a3436-304">In hello **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="a3436-305">Visual Studio 會建立名為 hello API 應用程式之後的資料夾，並產生用戶端類別。</span><span class="sxs-lookup"><span data-stu-id="a3436-305">Visual Studio creates a folder named after hello API app and generates client classes.</span></span>
   
    ![所產生用戶端的程式碼檔案](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="a3436-307">在 hello ToDoListAPI 專案中，開啟*Controllers\ToDoListController.cs* toosee hello 的程式碼行 40，呼叫 hello API 使用 hello 產生用戶端。</span><span class="sxs-lookup"><span data-stu-id="a3436-307">In hello ToDoListAPI project, open *Controllers\ToDoListController.cs* toosee hello code at line 40  that calls hello API by using hello generated client.</span></span>
   
    <span data-ttu-id="a3436-308">下列程式碼片段的 hello 顯示 hello 程式碼如何具現化 hello 用戶端物件並呼叫 hello Get 方法。</span><span class="sxs-lookup"><span data-stu-id="a3436-308">hello following snippet shows how hello code instantiates hello client object and calls hello Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="a3436-309">hello 建構函式參數取得 hello 端點 URL 從 hello`toDoListDataAPIURL`應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="a3436-309">hello constructor parameter gets hello endpoint URL from  hello `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="a3436-310">在 hello Web.config 檔案中，該值會是組 toohello 本機 IIS Express 的 URL hello API 專案，您可以在本機執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-310">In hello Web.config file, that value is set toohello local IIS Express URL of hello API project so that you can run hello application locally.</span></span> <span data-ttu-id="a3436-311">如果您省略 hello 建構函式參數，hello 預設端點。 產生 hello 的程式碼的 hello URL</span><span class="sxs-lookup"><span data-stu-id="a3436-311">If you omit hello constructor parameter, hello default endpoint is hello URL that you generated hello code from.</span></span>
7. <span data-ttu-id="a3436-312">用戶端類別將會產生具有不同的名稱，根據您應用程式開發介面的應用程式名稱;變更中的程式碼 hello *Controllers\ToDoListController.cs*使 hello 類型名稱符合您的專案中產生功能。</span><span class="sxs-lookup"><span data-stu-id="a3436-312">Your client class will be generated with a different name based on your API app name; change hello code in *Controllers\ToDoListController.cs* so that hello type name matches what was generated in your project.</span></span> <span data-ttu-id="a3436-313">例如，如果您將 API 應用程式命名為 ToDoListDataAPI071316，則會將此程式碼︰</span><span class="sxs-lookup"><span data-stu-id="a3436-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="a3436-314">toothis:</span><span class="sxs-lookup"><span data-stu-id="a3436-314">toothis:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a><span data-ttu-id="a3436-315">建立 API 應用程式 toohost hello 中介層</span><span class="sxs-lookup"><span data-stu-id="a3436-315">Create an API app toohost hello middle tier</span></span>
<span data-ttu-id="a3436-316">先前您[建立 hello 資料層應用程式開發介面應用程式和部署程式碼 tooit](#createapiapp)。</span><span class="sxs-lookup"><span data-stu-id="a3436-316">Earlier you [created hello data tier API app and deployed code tooit](#createapiapp).</span></span>  <span data-ttu-id="a3436-317">現在您遵循 hello hello 中介層應用程式開發介面應用程式相同的程序。</span><span class="sxs-lookup"><span data-stu-id="a3436-317">Now you follow hello same procedure for hello middle tier API app.</span></span>

1. <span data-ttu-id="a3436-318">在**方案總管 中**，以滑鼠右鍵按一下 hello 中介層 ToDoListAPI 專案 （不 hello 資料層 ToDoListDataAPI），然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="a3436-318">In **Solution Explorer**, right-click hello middle tier ToDoListAPI  project (not hello data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![在 Visual Studio 中按一下 [發佈]](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="a3436-320">在 hello**設定檔**hello 索引標籤**發行 Web**精靈 中，按一下**Microsoft Azure App Service**。</span><span class="sxs-lookup"><span data-stu-id="a3436-320">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="a3436-321">在 hello **App Service**對話方塊中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="a3436-321">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="a3436-322">在 hello**主控**hello 索引標籤**建立 App Service**對話方塊方塊中，接受預設 hello **API 應用程式名稱**輸入 hello 中是唯一的名稱或*名稱是.azurewebsites.net*網域。</span><span class="sxs-lookup"><span data-stu-id="a3436-322">In hello **Hosting** tab of hello **Create App Service** dialog box, accept hello default **API App Name** or enter a name that is unique in hello *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="a3436-323">選擇 hello Azure**訂用帳戶**已經使用。</span><span class="sxs-lookup"><span data-stu-id="a3436-323">Choose hello Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="a3436-324">在 hello**資源群組**下拉式清單中，選擇 hello 您稍早建立的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="a3436-324">In hello **Resource Group** drop-down, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="a3436-325">在 hello**應用程式服務方案**下拉式清單中，選擇 hello 相同您稍早建立的計畫。</span><span class="sxs-lookup"><span data-stu-id="a3436-325">In hello **App Service Plan** drop-down, choose hello same plan you created earlier.</span></span> <span data-ttu-id="a3436-326">它將預設 toothat 值。</span><span class="sxs-lookup"><span data-stu-id="a3436-326">It will default toothat value.</span></span>
8. <span data-ttu-id="a3436-327">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a3436-327">Click **Create**.</span></span>
   
    <span data-ttu-id="a3436-328">Visual Studio 建立 hello API 應用程式，建立的發行設定檔，並顯示 hello**連接**步驟 hello**發行 Web**精靈。</span><span class="sxs-lookup"><span data-stu-id="a3436-328">Visual Studio creates hello API app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
9. <span data-ttu-id="a3436-329">在 hello**連接**步驟 hello**發行 Web**精靈 中，按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="a3436-329">In hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="a3436-330">Visual Studio 部署 hello ToDoListAPI 專案 toohello 新 API 的應用程式，並開啟瀏覽器 toohello hello API 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="a3436-330">Visual Studio deploys hello ToDoListAPI project toohello new API app and opens a browser toohello URL of hello API app.</span></span> <span data-ttu-id="a3436-331">「 成功建立"hello 頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="a3436-331">hello "successfully created" page appears.</span></span>

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a><span data-ttu-id="a3436-332">設定 hello 中介層 toocall hello 資料層</span><span class="sxs-lookup"><span data-stu-id="a3436-332">Configure hello middle tier toocall hello data tier</span></span>
<span data-ttu-id="a3436-333">如果您現在稱為 hello 中介層應用程式開發介面應用程式，它就會嘗試使用仍在 hello Web.config 檔案中的 hello localhost URL toocall hello 資料層。</span><span class="sxs-lookup"><span data-stu-id="a3436-333">If you called hello middle tier API app now, it would try toocall hello data tier using hello localhost URL that is still in hello Web.config file.</span></span> <span data-ttu-id="a3436-334">這一節中，您可以輸入 hello 資料層應用程式開發介面應用程式 URL 到 hello 中介層應用程式開發介面應用程式中的環境設定。</span><span class="sxs-lookup"><span data-stu-id="a3436-334">In this section you enter hello data tier API app URL into an environment setting in hello middle tier API app.</span></span> <span data-ttu-id="a3436-335">當 hello hello 中介層應用程式開發介面應用程式中的程式碼擷取 hello 資料層 URL 設定時，hello 環境設定，將會覆寫何謂 hello Web.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="a3436-335">When hello code in hello middle tier API app retrieves hello data tier URL setting, hello environment setting will override what's in hello Web.config file.</span></span>

1. <span data-ttu-id="a3436-336">移 toohello [Azure 入口網站](https://portal.azure.com/)，然後瀏覽 toohello **API 應用程式**刀鋒視窗，您建立 toohost hello TodoListAPI （中介層） 專案的 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-336">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that you created toohost hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="a3436-337">在 hello API 應用程式**設定**刀鋒視窗中，按一下 **應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="a3436-337">In hello API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="a3436-338">在 hello API 應用程式**應用程式設定**刀鋒視窗中，捲動 toohello**應用程式設定**區段，加入 hello 下列索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="a3436-338">In hello API App's **Application Settings** blade, scroll down toohello **App settings** section and add hello following key and value.</span></span> <span data-ttu-id="a3436-339">hello 值將是 hello 的 hello 第一個 API 在這個教學課程中您發行應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="a3436-339">hello value will be hello URL of hello first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="a3436-340">**金鑰**</span><span class="sxs-lookup"><span data-stu-id="a3436-340">**Key**</span></span> | <span data-ttu-id="a3436-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="a3436-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="a3436-342">**值**</span><span class="sxs-lookup"><span data-stu-id="a3436-342">**Value**</span></span> |<span data-ttu-id="a3436-343">https://{您的資料層 API 應用程式名稱}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="a3436-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="a3436-344">**範例**</span><span class="sxs-lookup"><span data-stu-id="a3436-344">**Example**</span></span> |<span data-ttu-id="a3436-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="a3436-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="a3436-346">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a3436-346">Click **Save**.</span></span>
   
    ![按一下 [應用程式設定] 的 [儲存]](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="a3436-348">當 hello 程式碼在 Azure 中執行時，此值現在會覆寫 hello Web.config 檔案中的 hello localhost URL。</span><span class="sxs-lookup"><span data-stu-id="a3436-348">When hello code runs in Azure, this value will now override hello localhost URL that is in hello Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="a3436-349">測試</span><span class="sxs-lookup"><span data-stu-id="a3436-349">Test</span></span>
1. <span data-ttu-id="a3436-350">在瀏覽器視窗中，瀏覽 hello 新中介層應用程式開發介面應用程式，您剛才建立的 ToDoListAPI toohello URL。</span><span class="sxs-lookup"><span data-stu-id="a3436-350">In a browser window, browse toohello URL of hello new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="a3436-351">您可以按一下 hello 入口網站中的 hello API 應用程式的主要刀鋒視窗中的 hello URL 那里取得。</span><span class="sxs-lookup"><span data-stu-id="a3436-351">You can get there by clicking hello URL in hello API app's main blade in hello portal.</span></span>
2. <span data-ttu-id="a3436-352">在 hello 瀏覽器的網址列中加入"swagger"toohello URL，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="a3436-352">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="a3436-353">(URL 是的 hello `http://{apiappname}.azurewebsites.net/swagger`。)</span><span class="sxs-lookup"><span data-stu-id="a3436-353">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="a3436-354">hello 瀏覽器顯示 hello 相同 Swagger UI 之前看到的 ToDoListDataAPI，但現在`owner`是不必要的欄位 hello Get 作業，因為 hello 中介層應用程式開發介面應用程式正在為您傳送該值 toohello 資料層應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-354">hello browser displays hello same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for hello Get operation, because hello middle tier API app is sending that value toohello data tier API app for you.</span></span> <span data-ttu-id="a3436-355">(當您執行 hello 驗證教學課程時，hello 中介層會將傳送 hello 的實際使用者識別碼`owner`參數; 若為現在它硬式編碼星號。)</span><span class="sxs-lookup"><span data-stu-id="a3436-355">(When you do hello authentication tutorials, hello middle tier will send actual user IDs for hello `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="a3436-356">Hello Get 方法與 hello hello 中介層應用程式開發介面應用程式其他方法 toovalidate 成功呼叫 hello 資料層應用程式開發介面應用程式，請試試看。</span><span class="sxs-lookup"><span data-stu-id="a3436-356">Try out hello Get method and hello other methods toovalidate that hello middle tier API app is successfully calling hello data tier API app.</span></span>
   
    ![Swagger UI Get 方法](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="a3436-358">疑難排解</span><span class="sxs-lookup"><span data-stu-id="a3436-358">Troubleshooting</span></span>
<span data-ttu-id="a3436-359">如果您在瀏覽本教學課程時遇到問題，以下是一些疑難排解的相關說明︰</span><span class="sxs-lookup"><span data-stu-id="a3436-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="a3436-360">請確定您使用 hello 最新版 hello [Azure SDK for.NET](http://go.microsoft.com/fwlink/?linkid=518003)。</span><span class="sxs-lookup"><span data-stu-id="a3436-360">Make sure that you're using hello latest version of hello [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="a3436-361">Hello 專案名稱是類似 (ToDoListAPI，ToDoListDataAPI)。</span><span class="sxs-lookup"><span data-stu-id="a3436-361">Two of hello project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="a3436-362">如果項目看起來如下 hello 指示中所述，當您使用的專案，，請確定您已開啟 hello 正確的專案。</span><span class="sxs-lookup"><span data-stu-id="a3436-362">If things don't look as described in hello instructions when you are working with a project, make sure you have opened hello correct project.</span></span>
* <span data-ttu-id="a3436-363">如果您的公司網路，並嘗試透過防火牆 toodeploy tooAzure 應用程式服務，請確定連接埠 443 和 8172 已開啟的 Web Deploy。</span><span class="sxs-lookup"><span data-stu-id="a3436-363">If you're on a corporate network and are trying toodeploy tooAzure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="a3436-364">如果您無法開啟這些連接埠，則可以使用其他部署方法。</span><span class="sxs-lookup"><span data-stu-id="a3436-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="a3436-365">請參閱[部署您的應用程式服務的應用程式 tooAzure](../app-service-web/web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="a3436-365">See [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="a3436-366">「 路由名稱必須唯一 」 的錯誤-您可以取得這些如果您不小心將 hello 錯誤的專案 tooan API 應用程式部署，然後稍後部署 hello 正確一個 tooit。</span><span class="sxs-lookup"><span data-stu-id="a3436-366">"Route names must be unique" errors -- you could get these if you accidentally deploy hello wrong project tooan API app and then later deploy hello correct one tooit.</span></span> <span data-ttu-id="a3436-367">toocorrect 如此，重新部署 hello 正確的專案 toohello API 應用程式，在 hello**設定**hello 索引標籤**發行 Web**精靈選取**移除其他檔案，在目的地**.</span><span class="sxs-lookup"><span data-stu-id="a3436-367">toocorrect this, redeploy hello correct project toohello API app, and on hello **Settings** tab of hello **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="a3436-368">Azure App Service 中執行的 ASP.NET 應用程式開發介面應用程式之後，您可能想 toolearn 深入了解 Visual Studio 功能，可簡化疑難排解。</span><span class="sxs-lookup"><span data-stu-id="a3436-368">After you have your ASP.NET API app running in Azure App Service, you may want toolearn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="a3436-369">如需記錄和遠端偵錯等功能的相關資訊，請參閱[在 Visual Studio 中針對 Azure App Service 應用程式進行疑難排解](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="a3436-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3436-370">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3436-370">Next steps</span></span>
<span data-ttu-id="a3436-371">您已經看到如何 toodeploy 現有 Web API 專案 tooAPI 應用程式產生針對應用程式開發介面應用程式，用戶端程式碼和使用來自.NET 用戶端應用程式開發介面應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3436-371">You've seen how toodeploy existing Web API projects tooAPI apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="a3436-372">hello 這系列中的下一個教學課程會示範如何太[使用 CORS 從 JavaScript 用戶端的 tooconsume API 應用程式](app-service-api-cors-consume-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="a3436-372">hello next tutorial in this series shows how too[use CORS tooconsume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="a3436-373">如需有關用戶端產生程式碼的詳細資訊，請參閱 hello [Azure/AutoRest](https://github.com/azure/autorest) GitHub.com 上的儲存機制。有關使用 hello 產生用戶端的問題，請開啟[hello AutoRest 儲存機制中的問題](https://github.com/azure/autorest/issues)。</span><span class="sxs-lookup"><span data-stu-id="a3436-373">For more information about client code generation, see hello [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com. For help with problems using hello generated client, open an [issue in hello AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="a3436-374">如果您想 toocreate 新 API 的應用程式專案從頭，使用 hello **Azure API 應用程式**範本。</span><span class="sxs-lookup"><span data-stu-id="a3436-374">If you want toocreate new API app projects from scratch, use hello **Azure API App** template.</span></span>

![Visual Studio 中的 API 應用程式範本](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="a3436-376">hello **Azure API 應用程式**專案範本為對等 toochoosing hello**空**ASP.NET 4.5.2 範本中，按一下 [hello] 核取方塊 tooadd Web API 支援，並安裝 hello Swashbuckle NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="a3436-376">hello **Azure API App** project template is equivalent toochoosing hello **Empty** ASP.NET 4.5.2 template, clicking hello check box tooadd Web API support, and installing hello Swashbuckle NuGet package.</span></span> <span data-ttu-id="a3436-377">此外，hello 範本加入某些 Swashbuckle 組態程式碼設計 tooprevent hello 建立重複的 Swagger 作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="a3436-377">In addition, hello template adds some Swashbuckle configuration code designed tooprevent hello creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="a3436-378">一旦您已建立 API 應用程式專案，您可以將它部署 tooan API 應用程式 hello 您在本教學課程中看到的一樣。</span><span class="sxs-lookup"><span data-stu-id="a3436-378">Once you've created an API App project, you can deploy it tooan API app hello same way you saw in this tutorial.</span></span>

