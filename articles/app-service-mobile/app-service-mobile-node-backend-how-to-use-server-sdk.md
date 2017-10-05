---
title: "如何使用適用於 Mobile Apps 的 Node.js 後端伺服器 SDK | Microsoft Docs"
description: "了解如何使用適用於 Azure App Service Mobile Apps 的 Node.js 後端伺服器 SDK。"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 1d3aa7a0089279a8eafeb0ded951a5238e189eaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="f6a66-103">如何使用 Azure Mobile Apps Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="f6a66-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="f6a66-104">本文提供詳細的資訊及範例，說明如何在 Azure App Service Mobile Apps 中使用 Node.js 後端。</span><span class="sxs-lookup"><span data-stu-id="f6a66-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="f6a66-105"><a name="Introduction"></a>簡介</span><span class="sxs-lookup"><span data-stu-id="f6a66-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="f6a66-106">Azure App Service Mobile Apps 可讓您將行動最佳化資料存取 Web API 新增至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6a66-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="f6a66-107">提供的 Azure App Service Mobile Apps SDK 適用於 ASP.NET 和 Node.js Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6a66-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="f6a66-108">此 SDK 提供下列作業：</span><span class="sxs-lookup"><span data-stu-id="f6a66-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="f6a66-109">資料存取的資料表作業 (讀取、插入、更新、刪除)</span><span class="sxs-lookup"><span data-stu-id="f6a66-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="f6a66-110">自訂 API 作業</span><span class="sxs-lookup"><span data-stu-id="f6a66-110">Custom API operations</span></span>

<span data-ttu-id="f6a66-111">這兩種作業都可用於 Azure App Service 所允許的所有識別提供者 (包括 Facebook、Twitter、Google 和 Microsoft 等社交識別提供者，以及用於企業身分識別的 Azure Active Directory) 之間的驗證。</span><span class="sxs-lookup"><span data-stu-id="f6a66-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="f6a66-112">您可以在 [GitHub 上的範例目錄]中找到每個使用案例的範例。</span><span class="sxs-lookup"><span data-stu-id="f6a66-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="f6a66-113">支援的平台</span><span class="sxs-lookup"><span data-stu-id="f6a66-113">Supported Platforms</span></span>
<span data-ttu-id="f6a66-114">Azure Mobile Apps Node SDK 支援 Node 目前的 LTS 版及更新版本。</span><span class="sxs-lookup"><span data-stu-id="f6a66-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="f6a66-115">在撰寫本文時，最新的 LTS 版本是 Node v4.5.0。</span><span class="sxs-lookup"><span data-stu-id="f6a66-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="f6a66-116">其他版本的 Node 可能可以運作，但不受支援。</span><span class="sxs-lookup"><span data-stu-id="f6a66-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="f6a66-117">Azure Mobile Apps Node SDK 支援兩種資料庫驅動程式：node-mssql 驅動程式支援 SQL Azure 和本機 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f6a66-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="f6a66-118">Sqlite3 驅動程式僅支援單一執行個體上的 SQLite 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6a66-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="f6a66-119"><a name="howto-cmdline-basicapp"></a>作法：使用命令列建立基本 Node.js 後端</span><span class="sxs-lookup"><span data-stu-id="f6a66-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="f6a66-120">每個 Azure App Service Mobile App Node.js 後端都會以 ExpressJS 應用程式的形式啟動。</span><span class="sxs-lookup"><span data-stu-id="f6a66-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="f6a66-121">在適用於 Node.js 的 Web 服務架構中，ExpressJS 最廣為使用。</span><span class="sxs-lookup"><span data-stu-id="f6a66-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="f6a66-122">您可以依照下列方式建立基本的 [Express] 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f6a66-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="f6a66-123">在命令或 PowerShell 視窗中，為您的專案建立目錄。</span><span class="sxs-lookup"><span data-stu-id="f6a66-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="f6a66-124">執行 npm init 以初始化封裝結構。</span><span class="sxs-lookup"><span data-stu-id="f6a66-124">Run npm init to initialize the package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="f6a66-125">Npm init 命令會詢問一組問題以初始化專案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="f6a66-126">請參閱範例輸出：</span><span class="sxs-lookup"><span data-stu-id="f6a66-126">See the example output:</span></span>

    ![npm init 輸出][0]
3. <span data-ttu-id="f6a66-128">從 npm 儲存機制安裝 express 和 azure-mobile-apps 資源庫。</span><span class="sxs-lookup"><span data-stu-id="f6a66-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="f6a66-129">建立 app.js 檔案以實作基本行動伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6a66-129">Create an app.js file to implement the basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="f6a66-130">此應用程式會建立具有單一端點 (`/tables/TodoItem`) 的行動最佳化 WebAPI，讓使用者可使用動態結構描述存取基礎 SQL 資料存放區，不需經過驗證。</span><span class="sxs-lookup"><span data-stu-id="f6a66-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="f6a66-131">它適用於下列用戶端程式庫快速入門：</span><span class="sxs-lookup"><span data-stu-id="f6a66-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="f6a66-132">[Android 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="f6a66-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="f6a66-133">[Apache Cordova 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="f6a66-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="f6a66-134">[iOS 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="f6a66-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="f6a66-135">[Windows 市集用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="f6a66-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="f6a66-136">[Xamarin.iOS 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="f6a66-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="f6a66-137">[Xamarin.Android 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="f6a66-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="f6a66-138">[Xamarin.Forms 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="f6a66-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="f6a66-139">您可以在 [GitHub 上的 basicapp 範例]中找到此基本應用程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="f6a66-140"><a name="howto-vs2015-basicapp"></a>作法：使用 Visual Studio 2015 建立 Node 後端</span><span class="sxs-lookup"><span data-stu-id="f6a66-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="f6a66-141">Visual Studio 2015 需要延伸模組才能在整合式開發環境 (IDE) 內開發 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6a66-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="f6a66-142">首先，請安裝 [Node.js Tools 1.1 for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="f6a66-143">安裝 Node.js Tools for Visual Studio 後，請建立 Express 4.x 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f6a66-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="f6a66-144">開啟 [新增專案] 對話方塊 (從 [檔案]  >  [新增]  >  [專案...])。</span><span class="sxs-lookup"><span data-stu-id="f6a66-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="f6a66-145">展開**範本** > **JavaScript** > **Node.js**。</span><span class="sxs-lookup"><span data-stu-id="f6a66-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="f6a66-146">選取 [基本 Azure Node.js Express 4 應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="f6a66-147">填入專案名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a66-147">Fill in the project name.</span></span>  <span data-ttu-id="f6a66-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-148">Click *OK*.</span></span>

    ![Visual Studio 2015 新專案][1]
5. <span data-ttu-id="f6a66-150">以滑鼠右鍵按一下 **npm** 節點，然後選取 [安裝新的 npm 套件...]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="f6a66-151">建立第一個 Node.js 應用程式時，您可能必須重新整理 npm 目錄。</span><span class="sxs-lookup"><span data-stu-id="f6a66-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="f6a66-152">如有必要，請按一下 [重新整理]  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="f6a66-153">在搜尋方塊中輸入 *azure-mobile-apps* 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="f6a66-154">按一下 [azure-mobile-apps 2.0.0] 套件，然後按一下 [安裝套件]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![安裝新的 npm 封裝][2]
8. <span data-ttu-id="f6a66-156">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-156">Click **Close**.</span></span>
9. <span data-ttu-id="f6a66-157">開啟 *app.js* 檔案，以新增 Azure Mobile Apps SDK 的支援。</span><span class="sxs-lookup"><span data-stu-id="f6a66-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="f6a66-158">在程式庫 require 陳述式底部的第 6 行，加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f6a66-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="f6a66-159">在其他 app.use 陳述式之後大約第 27 行，加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f6a66-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="f6a66-160">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-160">Save the file.</span></span>
10. <span data-ttu-id="f6a66-161">在本機執行應用程式 (已在 http://localhost:3000 上提供 API)，或發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f6a66-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <span data-ttu-id="f6a66-162"><a name="create-node-backend-portal"></a>作法：使用 Azure 入口網站建立 Node.js 後端</span><span class="sxs-lookup"><span data-stu-id="f6a66-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="f6a66-163">您可以在 [Azure 入口網站]中直接建立行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="f6a66-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="f6a66-164">您可以遵循下列步驟，或者依照 [建立行動應用程式](app-service-mobile-ios-get-started.md) 教學課程，一起建立用戶端和伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6a66-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="f6a66-165">本教學課程包含下列指示的簡化版本，最適合用於概念驗證專案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="f6a66-166">回到 [開始] 刀鋒視窗，在 [建立資料表 API] 底下，選擇 [Node.js] 作為您的 [後端語言]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="f6a66-167">核取 [我了解此將覆寫所有網站內容] 方塊，然後按一下 [建立 TodoItem 資料表]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="f6a66-168"><a name="download-quickstart"></a>作法：使用 Git 下載 Node.js 後端快速入門程式碼專案</span><span class="sxs-lookup"><span data-stu-id="f6a66-168"><a name="download-quickstart"></a>How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="f6a66-169">當您使用入口網站的 [快速入門]  刀鋒視窗建立 Node.js 行動應用程式後端時，系統會為您建立 Node.js 專案並將其部署至您的網站。</span><span class="sxs-lookup"><span data-stu-id="f6a66-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="f6a66-170">您可以在入口網站中新增資料表和 API，並編輯 Node.js 後端的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="f6a66-171">您也可以使用各種部署工具來下載後端專案，以便新增或修改資料表和 API，然後重新發佈專案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="f6a66-172">如需詳細資訊，請參閱 [Azure App Service 部署指南]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="f6a66-173">下列程序使用 Git 儲存機制來下載快速入門專案程式碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="f6a66-174">如果尚未安裝 Git，請先安裝。</span><span class="sxs-lookup"><span data-stu-id="f6a66-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="f6a66-175">安裝 Git 所需的步驟會因作業系統而有所不同。</span><span class="sxs-lookup"><span data-stu-id="f6a66-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="f6a66-176">如需作業系統特定的發佈和安裝指引，請參閱 [安裝 Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="f6a66-177">請依照[啟用 App Service 應用程式存放庫](../app-service-web/app-service-deploy-local-git.md#Step3)中的步驟，為您的後端網站啟用 Git 存放庫，並記下部署使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="f6a66-178">在您的行動應用程式後端的刀鋒視窗中，記下 [Git 複製 URL]  設定。</span><span class="sxs-lookup"><span data-stu-id="f6a66-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="f6a66-179">使用 Git 複製 URL 執行 `git clone` 命令，並在需要時輸入您的密碼，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f6a66-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="f6a66-180">瀏覽至本機目錄 (在上述範例中為 /todolist)，並注意專案檔案已下載。</span><span class="sxs-lookup"><span data-stu-id="f6a66-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="f6a66-181">在 `/tables` 目錄中找出 `todoitem.json` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="f6a66-182">該檔案定義了資料表上的權限。</span><span class="sxs-lookup"><span data-stu-id="f6a66-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="f6a66-183">另請在相同的目錄中找出 `todoitem.js` 檔案，該檔案定義了資料表的 CRUD 作業指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="f6a66-184">在您變更專案檔案之後，請執行下列命令來新增、認可變更，然後將變更上傳至網站：</span><span class="sxs-lookup"><span data-stu-id="f6a66-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>

        $ git commit -m "updated the table script"
        $ git push origin master

    <span data-ttu-id="f6a66-185">當您將新檔案加入至專案時，您必須先執行 `git add .` 命令。</span><span class="sxs-lookup"><span data-stu-id="f6a66-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="f6a66-186">每次有一組新的認可推送至網站時，就會重新發佈網站。</span><span class="sxs-lookup"><span data-stu-id="f6a66-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <span data-ttu-id="f6a66-187"><a name="howto-publish-to-azure"></a>作法：將您的 Node.js 後端發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="f6a66-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="f6a66-188">Microsoft Azure 提供許多將 Azure App Service Mobile Apps Node.js 後端發佈至 Azure 服務的機制。</span><span class="sxs-lookup"><span data-stu-id="f6a66-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="f6a66-189">其中包括使用整合至 Visual Studio 中的部署工具、命令列工具，和以原始檔控制為基礎的連續部署選項。</span><span class="sxs-lookup"><span data-stu-id="f6a66-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="f6a66-190">如需有關本主題的詳細資訊，請參閱 [Azure App Service 部署指南]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="f6a66-191">Azure App Service 提供 Node.js 應用程式方面的具體建議，您應該在部署之前先檢閱：</span><span class="sxs-lookup"><span data-stu-id="f6a66-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="f6a66-192">如何 [指定 Node 版本]</span><span class="sxs-lookup"><span data-stu-id="f6a66-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="f6a66-193">如何 [使用 Node 模組]</span><span class="sxs-lookup"><span data-stu-id="f6a66-193">How to [use Node modules]</span></span>

### <span data-ttu-id="f6a66-194"><a name="howto-enable-homepage"></a>作法：啟用應用程式的首頁</span><span class="sxs-lookup"><span data-stu-id="f6a66-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="f6a66-195">許多應用程式是 Web 和行動應用程式的組合，ExpressJS 架構可讓您結合兩方面。</span><span class="sxs-lookup"><span data-stu-id="f6a66-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="f6a66-196">但是有時候，您可能只想要實作行動介面。</span><span class="sxs-lookup"><span data-stu-id="f6a66-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="f6a66-197">它對於提供登陸頁面以確保 App Service 已啟動並執行很有用。</span><span class="sxs-lookup"><span data-stu-id="f6a66-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="f6a66-198">您可以提供您自己的首頁，或啟用暫時的首頁。</span><span class="sxs-lookup"><span data-stu-id="f6a66-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="f6a66-199">若要啟用暫時的首頁，請使用以下內容將 Azure Mobile Apps 具現化︰</span><span class="sxs-lookup"><span data-stu-id="f6a66-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="f6a66-200">如果您想要讓此選項僅在本機開發時可供使用，可以將此設定新增至 `azureMobile.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <span data-ttu-id="f6a66-201"><a name="TableOperations"></a>資料表作業</span><span class="sxs-lookup"><span data-stu-id="f6a66-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="f6a66-202">azure-mobile-apps Node.js Server SDK 提供將儲存在 Azure SQL Database 中的資料表公開為 WebAPI 的機制。</span><span class="sxs-lookup"><span data-stu-id="f6a66-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="f6a66-203">提供的作業有五種。</span><span class="sxs-lookup"><span data-stu-id="f6a66-203">Five operations are provided.</span></span>

| <span data-ttu-id="f6a66-204">作業</span><span class="sxs-lookup"><span data-stu-id="f6a66-204">Operation</span></span> | <span data-ttu-id="f6a66-205">說明</span><span class="sxs-lookup"><span data-stu-id="f6a66-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6a66-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="f6a66-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="f6a66-207">取得資料表中的所有記錄</span><span class="sxs-lookup"><span data-stu-id="f6a66-207">Get all records in the table</span></span> |
| <span data-ttu-id="f6a66-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="f6a66-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="f6a66-209">取得資料表中的特定記錄</span><span class="sxs-lookup"><span data-stu-id="f6a66-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="f6a66-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="f6a66-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="f6a66-211">在資料表中建立記錄</span><span class="sxs-lookup"><span data-stu-id="f6a66-211">Create a record in the table</span></span> |
| <span data-ttu-id="f6a66-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="f6a66-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="f6a66-213">更新資料表中的記錄</span><span class="sxs-lookup"><span data-stu-id="f6a66-213">Update a record in the table</span></span> |
| <span data-ttu-id="f6a66-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="f6a66-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="f6a66-215">刪除資料表中的記錄</span><span class="sxs-lookup"><span data-stu-id="f6a66-215">Delete a record in the table</span></span> |

<span data-ttu-id="f6a66-216">此 WebAPI 支援 [OData]，而且擴充資料表結構描述以支援[離線資料同步]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <span data-ttu-id="f6a66-217"><a name="howto-dynamicschema"></a>作法：使用動態結構描述定義資料表</span><span class="sxs-lookup"><span data-stu-id="f6a66-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="f6a66-218">資料表必須先經過定義才能使用。</span><span class="sxs-lookup"><span data-stu-id="f6a66-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="f6a66-219">資料表可用靜態結構描述來定義 (開發人員在結構描述中定義資料行)，或以動態方式定義 (SDK 會根據傳入的要求控制結構描述)。</span><span class="sxs-lookup"><span data-stu-id="f6a66-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="f6a66-220">此外，開發人員可將 Javascript 程式碼新增至定義，以控制 WebAPI 的特定層面。</span><span class="sxs-lookup"><span data-stu-id="f6a66-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="f6a66-221">根據最佳作法，您應在資料表目錄中的 Javascript 檔案內定義每個資料表，然後使用 tables.import() 方法匯入資料表。</span><span class="sxs-lookup"><span data-stu-id="f6a66-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="f6a66-222">擴充基本應用程式後，會調整 app.js 檔案：</span><span class="sxs-lookup"><span data-stu-id="f6a66-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="f6a66-223">在 ./tables/TodoItem.js 中定義資料表：</span><span class="sxs-lookup"><span data-stu-id="f6a66-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="f6a66-224">資料表依預設會使用動態結構描述。</span><span class="sxs-lookup"><span data-stu-id="f6a66-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="f6a66-225">若要全域關閉動態結構描述，請在 Azure 入口網站中將應用程式設定 **MS_DynamicSchema** 設為 false。</span><span class="sxs-lookup"><span data-stu-id="f6a66-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="f6a66-226">您可以在 [GitHub 上的待辦事項範例]中找到完整範例。</span><span class="sxs-lookup"><span data-stu-id="f6a66-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <span data-ttu-id="f6a66-227"><a name="howto-staticschema"></a>作法：使用靜態結構描述定義資料表</span><span class="sxs-lookup"><span data-stu-id="f6a66-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="f6a66-228">您可以將資料行明確定義為要透過 WebAPI 公開。</span><span class="sxs-lookup"><span data-stu-id="f6a66-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="f6a66-229">azure-mobile-apps Node.js SDK 會自動將離線資料同步所需的任何其他資料行新增至您所提供的清單。</span><span class="sxs-lookup"><span data-stu-id="f6a66-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="f6a66-230">例如，快速入門用戶端應用程式需要具有兩個資料行的資料表：文字 (字串) 和完整 (布林值)。</span><span class="sxs-lookup"><span data-stu-id="f6a66-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="f6a66-231">這可以定義在資料表定義 JavaScript 檔案中 (位於資料表目錄中)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f6a66-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="f6a66-232">如果您以靜態方式定義資料表，則您還必須呼叫 tables.initialize() 方法，以在啟動時建立資料庫結構描述。</span><span class="sxs-lookup"><span data-stu-id="f6a66-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="f6a66-233">tables.initialize() 方法會傳回 [Promise] ，避免 Web 服務在資料庫初始化之前處理要求。</span><span class="sxs-lookup"><span data-stu-id="f6a66-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <span data-ttu-id="f6a66-234"><a name="howto-sqlexpress-setup"></a>作法：以 SQL Express 作為本機電腦上的開發資料存放區</span><span class="sxs-lookup"><span data-stu-id="f6a66-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="f6a66-235">Azure Mobile Apps AzureMobile Apps Node SDK 提供三種現成可用的資料提供選項：SDK 提供三種現成可用的資料提供選項：</span><span class="sxs-lookup"><span data-stu-id="f6a66-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="f6a66-236">使用 **記憶體** 驅動程式，可提供非持續性的範例存放區</span><span class="sxs-lookup"><span data-stu-id="f6a66-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="f6a66-237">使用 **mssql** 驅動程式，可提供可供開發使用的 SQL Express 資料存放區</span><span class="sxs-lookup"><span data-stu-id="f6a66-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="f6a66-238">使用 **mssql** 驅動程式，可提供可供生產使用的 Azure SQL Database 資料存放區</span><span class="sxs-lookup"><span data-stu-id="f6a66-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="f6a66-239">Azure Mobile Apps Node.js SDK 會使用 [mssql Node.js 封裝] 來建立及使用 SQL Express 和 SQL Database 的連線。</span><span class="sxs-lookup"><span data-stu-id="f6a66-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="f6a66-240">要使用此封裝，您必須在 SQL Express 執行個體上啟用 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="f6a66-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="f6a66-241">記憶體驅動程式未提供完整的測試工具集。</span><span class="sxs-lookup"><span data-stu-id="f6a66-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="f6a66-242">如果您想要在本機上測試後端，建議您使用 SQL Express 資料存放區和 mssql 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="f6a66-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
>
>

1. <span data-ttu-id="f6a66-243">下載並安裝 [Microsoft SQL Server 2014 Express]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="f6a66-244">請確實安裝 SQL Server 2014 Express with Tools 版。</span><span class="sxs-lookup"><span data-stu-id="f6a66-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="f6a66-245">除非您明確需要 64 位元支援，32 位元版本在執行時會耗用較少的記憶體。</span><span class="sxs-lookup"><span data-stu-id="f6a66-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="f6a66-246">執行 SQL Server 2014 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="f6a66-246">Run the SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="f6a66-247">在左側的樹狀結構功能表中，展開 [SQL Server 網路組態]  節點。</span><span class="sxs-lookup"><span data-stu-id="f6a66-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="f6a66-248">按一下 [SQLEXPRESS 的通訊協定] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="f6a66-249">以滑鼠右鍵按一下 [TCP/IP]，然後選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="f6a66-250">在快顯對話方塊中按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="f6a66-251">以滑鼠右鍵按一下 [TCP/IP]，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="f6a66-252">按一下 [IP 位址]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f6a66-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="f6a66-253">尋找 **IPAll** 節點。</span><span class="sxs-lookup"><span data-stu-id="f6a66-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="f6a66-254">在 [TCP 連接埠] 欄位中，輸入 **1433**。</span><span class="sxs-lookup"><span data-stu-id="f6a66-254">In the **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="f6a66-255">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-255">Click **OK**.</span></span>  <span data-ttu-id="f6a66-256">在快顯對話方塊中按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="f6a66-257">在左側的樹狀結構功能表中，按一下 [SQL Server 服務]  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="f6a66-258">以滑鼠右鍵按一下 [SQL Server (SQLEXPRESS)]，然後選取 [重新啟動]</span><span class="sxs-lookup"><span data-stu-id="f6a66-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="f6a66-259">關閉 SQL Server 2014 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="f6a66-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="f6a66-260">執行 SQL Server 2014 Management Studio 並連接到您的本機 SQL Express 執行個體</span><span class="sxs-lookup"><span data-stu-id="f6a66-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>

   1. <span data-ttu-id="f6a66-261">以滑鼠右鍵按一下您在 [物件總管] 中的執行個體，然後選取 [屬性] </span><span class="sxs-lookup"><span data-stu-id="f6a66-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="f6a66-262">選取 [安全性] 頁面  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="f6a66-263">確定已選取 [SQL Server 及 Windows 驗證模式]  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="f6a66-264">按一下 [確定] </span><span class="sxs-lookup"><span data-stu-id="f6a66-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="f6a66-265">展開 [範本]  >  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="f6a66-266">以滑鼠右鍵按一下 [登入]，然後選取 [新增登入...]</span><span class="sxs-lookup"><span data-stu-id="f6a66-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="f6a66-267">輸入登入名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a66-267">Enter a Login name.</span></span>  <span data-ttu-id="f6a66-268">選取 [SQL Server 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="f6a66-269">輸入密碼，然後在 [確認密碼] 中輸入相同的密碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="f6a66-270">密碼必須符合 Windows 複雜性需求。</span><span class="sxs-lookup"><span data-stu-id="f6a66-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="f6a66-271">按一下 [確定] </span><span class="sxs-lookup"><span data-stu-id="f6a66-271">Click **OK**</span></span>

          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="f6a66-272">以滑鼠右鍵按一下新的登入，然後選取 [屬性] </span><span class="sxs-lookup"><span data-stu-id="f6a66-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="f6a66-273">選取 [伺服器角色]  頁面。</span><span class="sxs-lookup"><span data-stu-id="f6a66-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="f6a66-274">核取 **dbcreator** 伺服器角色旁的方塊。</span><span class="sxs-lookup"><span data-stu-id="f6a66-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="f6a66-275">按一下 [確定] </span><span class="sxs-lookup"><span data-stu-id="f6a66-275">Click **OK**</span></span>
   13. <span data-ttu-id="f6a66-276">關閉 SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="f6a66-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="f6a66-277">請確實記下您選取的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="f6a66-278">您可能需要根據您特定的資料庫需求指派其他伺服器角色或權限。</span><span class="sxs-lookup"><span data-stu-id="f6a66-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="f6a66-279">Node.js 應用程式會讀取 **SQLCONNSTR_MS_TableConnectionString** 環境變數，以取得此資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="f6a66-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="f6a66-280">您可以將該變數設定在環境中。</span><span class="sxs-lookup"><span data-stu-id="f6a66-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="f6a66-281">例如，您可以使用 PowerShell 來設定此環境變數：</span><span class="sxs-lookup"><span data-stu-id="f6a66-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="f6a66-282">透過 TCP/IP 連線存取資料庫，並提供連線的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <span data-ttu-id="f6a66-283"><a name="howto-config-localdev"></a>作法：設定專案以在本機上進行開發</span><span class="sxs-lookup"><span data-stu-id="f6a66-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="f6a66-284">Azure Mobile Apps 會從本機檔案系統讀取名為 *azureMobile.js* 的 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="f6a66-285">請勿使用此檔案在生產環境中設定 Azure Mobile Apps SDK，請改用 [Azure 入口網站] 中的 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="f6a66-286">*azureMobile.js* 檔案應會匯出組態物件。</span><span class="sxs-lookup"><span data-stu-id="f6a66-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="f6a66-287">最常見的設定如下：</span><span class="sxs-lookup"><span data-stu-id="f6a66-287">The most common settings are:</span></span>

* <span data-ttu-id="f6a66-288">資料庫設定</span><span class="sxs-lookup"><span data-stu-id="f6a66-288">Database Settings</span></span>
* <span data-ttu-id="f6a66-289">診斷記錄設定</span><span class="sxs-lookup"><span data-stu-id="f6a66-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="f6a66-290">替代 CORS 設定</span><span class="sxs-lookup"><span data-stu-id="f6a66-290">Alternate CORS Settings</span></span>

<span data-ttu-id="f6a66-291">以下是實作上述資料庫設定的 *azureMobile.js* 檔案範例：</span><span class="sxs-lookup"><span data-stu-id="f6a66-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="f6a66-292">建議您將 *azureMobile.js* 新增至您的 *.gitignore* 檔案 (或其他原始程式碼控制忽略檔案)，以防止密碼儲存在雲端中。</span><span class="sxs-lookup"><span data-stu-id="f6a66-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="f6a66-293">請一律在 [Azure 入口網站]內的 [應用程式設定] 中設定生產設定。</span><span class="sxs-lookup"><span data-stu-id="f6a66-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <span data-ttu-id="f6a66-294"><a name="howto-appsettings"></a>作法：設定行動應用程式的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="f6a66-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="f6a66-295">*azureMobile.js* 檔案中的大部分設定在 [Azure 入口網站]中都有對等的 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="f6a66-296">請使用下列清單在 [應用程式設定] 中設定您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="f6a66-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="f6a66-297">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="f6a66-297">App Setting</span></span> | <span data-ttu-id="f6a66-298">*azureMobile.js* 設定</span><span class="sxs-lookup"><span data-stu-id="f6a66-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="f6a66-299">說明</span><span class="sxs-lookup"><span data-stu-id="f6a66-299">Description</span></span> | <span data-ttu-id="f6a66-300">有效值</span><span class="sxs-lookup"><span data-stu-id="f6a66-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="f6a66-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="f6a66-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="f6a66-302">名稱</span><span class="sxs-lookup"><span data-stu-id="f6a66-302">name</span></span> |<span data-ttu-id="f6a66-303">應用程式的名稱</span><span class="sxs-lookup"><span data-stu-id="f6a66-303">The name of the app</span></span> |<span data-ttu-id="f6a66-304">字串</span><span class="sxs-lookup"><span data-stu-id="f6a66-304">string</span></span> |
| <span data-ttu-id="f6a66-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="f6a66-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="f6a66-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="f6a66-306">logging.level</span></span> |<span data-ttu-id="f6a66-307">要記錄的訊息的最小記錄層級</span><span class="sxs-lookup"><span data-stu-id="f6a66-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="f6a66-308">error、warning、info、verbose、debug、silly</span><span class="sxs-lookup"><span data-stu-id="f6a66-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="f6a66-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="f6a66-309">**MS_DebugMode**</span></span> |<span data-ttu-id="f6a66-310">debug</span><span class="sxs-lookup"><span data-stu-id="f6a66-310">debug</span></span> |<span data-ttu-id="f6a66-311">啟用或停用偵錯模式</span><span class="sxs-lookup"><span data-stu-id="f6a66-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="f6a66-312">true、false</span><span class="sxs-lookup"><span data-stu-id="f6a66-312">true, false</span></span> |
| <span data-ttu-id="f6a66-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="f6a66-313">**MS_TableSchema**</span></span> |<span data-ttu-id="f6a66-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="f6a66-314">data.schema</span></span> |<span data-ttu-id="f6a66-315">SQL 資料表的預設結構描述名稱</span><span class="sxs-lookup"><span data-stu-id="f6a66-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="f6a66-316">字串 (預設值：dbo)</span><span class="sxs-lookup"><span data-stu-id="f6a66-316">string (default: dbo)</span></span> |
| <span data-ttu-id="f6a66-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="f6a66-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="f6a66-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="f6a66-318">data.dynamicSchema</span></span> |<span data-ttu-id="f6a66-319">啟用或停用偵錯模式</span><span class="sxs-lookup"><span data-stu-id="f6a66-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="f6a66-320">true、false</span><span class="sxs-lookup"><span data-stu-id="f6a66-320">true, false</span></span> |
| <span data-ttu-id="f6a66-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="f6a66-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="f6a66-322">version (設定為未定義)</span><span class="sxs-lookup"><span data-stu-id="f6a66-322">version (set to undefined)</span></span> |<span data-ttu-id="f6a66-323">停用 X-ZUMO-Server-Version 標頭</span><span class="sxs-lookup"><span data-stu-id="f6a66-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="f6a66-324">true、false</span><span class="sxs-lookup"><span data-stu-id="f6a66-324">true, false</span></span> |
| <span data-ttu-id="f6a66-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="f6a66-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="f6a66-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="f6a66-326">skipversioncheck</span></span> |<span data-ttu-id="f6a66-327">停用用戶端 API 版本檢查</span><span class="sxs-lookup"><span data-stu-id="f6a66-327">Disables the client API version check</span></span> |<span data-ttu-id="f6a66-328">true、false</span><span class="sxs-lookup"><span data-stu-id="f6a66-328">true, false</span></span> |

<span data-ttu-id="f6a66-329">設定「應用程式設定」：</span><span class="sxs-lookup"><span data-stu-id="f6a66-329">To set an App Setting:</span></span>

1. <span data-ttu-id="f6a66-330">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="f6a66-331">選取 [所有資源] 或 [應用程式服務]，然後按一下行動應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a66-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="f6a66-332">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="f6a66-332">The Settings blade opens by default.</span></span> <span data-ttu-id="f6a66-333">如果沒有，請按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="f6a66-334">按一下 [一般] 功能表中的 [應用程式設定]  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="f6a66-335">捲動至 [應用程式設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="f6a66-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="f6a66-336">如果您的應用程式設定已經存在，請按一下應用程式設定的值來編輯該值。</span><span class="sxs-lookup"><span data-stu-id="f6a66-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="f6a66-337">如果您的應用程式設定不存在，請在 [機碼] 方塊中輸入「應用程式設定」及在 [值] 方塊中輸入值。</span><span class="sxs-lookup"><span data-stu-id="f6a66-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="f6a66-338">完成後，按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="f6a66-339">變更大部分的應用程式設定都需要重新啟動服務。</span><span class="sxs-lookup"><span data-stu-id="f6a66-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="f6a66-340"><a name="howto-use-sqlazure"></a>做法：使用 SQL Database 做為您的實際執行資料存放區</span><span class="sxs-lookup"><span data-stu-id="f6a66-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="f6a66-341">無論是何種 Azure App Service 應用程式類型，以 SQL Database 作為資料存放區的程序都是相同的。</span><span class="sxs-lookup"><span data-stu-id="f6a66-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="f6a66-342">如果您尚未執行，請依照下列步驟建立行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="f6a66-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="f6a66-343">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="f6a66-344">在頂端按一下滑鼠左鍵的視窗， **+ 新增**按鈕 > **Web + 行動** > **行動裝置應用程式**，然後提供您的行動裝置應用程式後端的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a66-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="f6a66-345">在 [資源群組]  方塊中，輸入與您應用程式相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a66-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="f6a66-346">系統將會選取預設 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="f6a66-347">如果您想要變更 App Service 方案，請按一下 [App Service 方案] > [+ 建立新方案]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="f6a66-348">為新的應用程式服務方案命名，並選取適當位置。</span><span class="sxs-lookup"><span data-stu-id="f6a66-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="f6a66-349">按一下 [定價層]，並選取適當的服務定價層。</span><span class="sxs-lookup"><span data-stu-id="f6a66-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="f6a66-350">選取 [檢視全部] 以檢視其他價格選項，例如 [免費] 和 [共用]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="f6a66-351">選取定價層後，請按一下 [選取]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6a66-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="f6a66-352">回到 [App Service 方案] 刀鋒視窗，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="f6a66-353">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-353">Click **Create**.</span></span> <span data-ttu-id="f6a66-354">佈建行動應用程式後端可能需要幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="f6a66-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="f6a66-355">行動應用程式後端佈建完畢後，入口網站會開啟行動應用程式後端的 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f6a66-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="f6a66-356">行動應用程式後端建立後，您可以選擇將現有的 SQL Database 連接到您的行動應用程式後端，或建立新的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f6a66-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="f6a66-357">在這一節中，您將建立 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f6a66-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="f6a66-358">如果在與行動應用程式後端相同的位置中已經有資料庫，您可以改為選取 [使用現有的資料庫]，然後選取該資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6a66-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="f6a66-359">我們不建議您使用位在不同位置的資料庫，因為這會產生更高的延遲。</span><span class="sxs-lookup"><span data-stu-id="f6a66-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="f6a66-360">在新「行動應用程式」後端中，依序按一下 [設定]  >  [行動應用程式]  >  [資料]  >  [+新增]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="f6a66-361">在 [新增資料連接] 刀鋒視窗中，依序按一下 [SQL Database - 設定必要設定]  >  [建立新的資料庫]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="f6a66-362">在 [名稱]  欄位中輸入新資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="f6a66-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="f6a66-363">按一下 [伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-363">Click **Server**.</span></span>  <span data-ttu-id="f6a66-364">在 [新增伺服器] 刀鋒視窗中，於 [伺服器名稱] 欄位中輸入唯一的伺服器名稱，然後提供合適的 [伺服器管理登入] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="f6a66-365">確定已勾選 [允許 Azure 服務存取伺服器]  。</span><span class="sxs-lookup"><span data-stu-id="f6a66-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="f6a66-366">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-366">Click **OK**.</span></span>

    ![建立 Azure SQL Database][6]
4. <span data-ttu-id="f6a66-368">在 [新增資料庫] 刀鋒視窗中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="f6a66-369">返回 [新增資料連接] 刀鋒視窗，選取 [連接字串]，輸入您建立資料庫時提供的登入與密碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="f6a66-370">如果您使用現有的資料庫，請提供該資料庫的登入認證。</span><span class="sxs-lookup"><span data-stu-id="f6a66-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="f6a66-371">輸入完成後，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f6a66-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="f6a66-372">再次返回 [新增資料連接] 刀鋒視窗，按一下 [確定] 以建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6a66-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="f6a66-373">建立資料庫可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="f6a66-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="f6a66-374">使用 [通知]  區域來監視部署的進度。</span><span class="sxs-lookup"><span data-stu-id="f6a66-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="f6a66-375">在資料庫成功部署之前，請勿繼續進行。</span><span class="sxs-lookup"><span data-stu-id="f6a66-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="f6a66-376">成功部署後，將會在您行動後端的 [應用程式設定] 中建立 SQL 資料庫執行個體的連接字串。</span><span class="sxs-lookup"><span data-stu-id="f6a66-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="f6a66-377">您可以在 [設定]  >  > 中找到每個使用案例的範例。</span><span class="sxs-lookup"><span data-stu-id="f6a66-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="f6a66-378"><a name="howto-tables-auth"></a>作法：需經過驗證才能存取資料表</span><span class="sxs-lookup"><span data-stu-id="f6a66-378"><a name="howto-tables-auth"></a>How to: Require authentication for access to tables</span></span>
<span data-ttu-id="f6a66-379">如果您想要在資料表端點使用「App Service 驗證」，就必須先在 [Azure 入口網站] 中設定「App Service 驗證」。</span><span class="sxs-lookup"><span data-stu-id="f6a66-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="f6a66-380">如需關於在 Azure App Service 中設定驗證的詳細資訊，請參閱您要使用的識別提供者所提供的組態指南：</span><span class="sxs-lookup"><span data-stu-id="f6a66-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="f6a66-381">[如何設定 Azure Active Directory 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="f6a66-382">[如何設定 Facebook 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="f6a66-383">[如何設定 Google 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="f6a66-384">[如何設定 Microsoft 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="f6a66-385">[如何設定 Twitter 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="f6a66-386">每個資料表都有一個存取屬性可用來控制對資料表的存取。</span><span class="sxs-lookup"><span data-stu-id="f6a66-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="f6a66-387">下列範例說明以靜態方式定義且需要驗證的資料表。</span><span class="sxs-lookup"><span data-stu-id="f6a66-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="f6a66-388">存取屬性接受三種值</span><span class="sxs-lookup"><span data-stu-id="f6a66-388">The access property can take one of three values</span></span>

* <span data-ttu-id="f6a66-389">*anonymous* 表示允許用戶端應用程式未經驗證就可讀取資料</span><span class="sxs-lookup"><span data-stu-id="f6a66-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="f6a66-390">*authenticated* 表示用戶端應用程式必須隨要求傳送有效的驗證權杖</span><span class="sxs-lookup"><span data-stu-id="f6a66-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="f6a66-391">*disabled* 表示此資料表目前已停用</span><span class="sxs-lookup"><span data-stu-id="f6a66-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="f6a66-392">如果未定義存取屬性，則會允許未經驗證的存取。</span><span class="sxs-lookup"><span data-stu-id="f6a66-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="f6a66-393"><a name="howto-tables-getidentity"></a>作法：透過資料表使用驗證宣告</span><span class="sxs-lookup"><span data-stu-id="f6a66-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="f6a66-394">您可以設定驗證設定時所要求的各種宣告。</span><span class="sxs-lookup"><span data-stu-id="f6a66-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="f6a66-395">這些宣告通常無法透過 `context.user` 物件取得。</span><span class="sxs-lookup"><span data-stu-id="f6a66-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="f6a66-396">但可使用 `context.user.getIdentity()` 方法取出。</span><span class="sxs-lookup"><span data-stu-id="f6a66-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="f6a66-397">`getIdentity()` 方法會傳回可解析成一項物件的 Promise。</span><span class="sxs-lookup"><span data-stu-id="f6a66-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="f6a66-398">物件會以驗證方法 (facebook、google、twitter、microsoftaccount 或 aad) 建立索引。</span><span class="sxs-lookup"><span data-stu-id="f6a66-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="f6a66-399">例如，如果您設定 Microsoft 帳戶驗證並要求電子郵件地址宣告時，可以利用下列資料表控制器將電子郵件地址加入記錄：</span><span class="sxs-lookup"><span data-stu-id="f6a66-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="f6a66-400">若要查看哪些宣告可用，請使用網頁瀏覽器來檢視網站的 `/.auth/me` 端點。</span><span class="sxs-lookup"><span data-stu-id="f6a66-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="f6a66-401"><a name="howto-tables-disabled"></a>做法：停用對特定資料表作業的存取權</span><span class="sxs-lookup"><span data-stu-id="f6a66-401"><a name="howto-tables-disabled"></a>How to: Disable access to specific table operations</span></span>
<span data-ttu-id="f6a66-402">除了會出現在資料表上以外，存取屬性也可用來控制個別作業。</span><span class="sxs-lookup"><span data-stu-id="f6a66-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="f6a66-403">共有四種作業：</span><span class="sxs-lookup"><span data-stu-id="f6a66-403">There are four operations:</span></span>

* <span data-ttu-id="f6a66-404">*read* 是在資料表上執行的 RESTful GET 作業</span><span class="sxs-lookup"><span data-stu-id="f6a66-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="f6a66-405">*insert* 是在資料表上執行的 RESTful POST 作業</span><span class="sxs-lookup"><span data-stu-id="f6a66-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="f6a66-406">*update* 是在資料表上執行的 RESTful PATCH 作業</span><span class="sxs-lookup"><span data-stu-id="f6a66-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="f6a66-407">*delete* 是在資料表上執行的 RESTful DELETE 作業</span><span class="sxs-lookup"><span data-stu-id="f6a66-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="f6a66-408">比方說，您可能會想要提供未經驗證的唯讀資料表：</span><span class="sxs-lookup"><span data-stu-id="f6a66-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="f6a66-409"><a name="howto-tables-query"></a>做法：調整與資料表作業搭配使用的查詢</span><span class="sxs-lookup"><span data-stu-id="f6a66-409"><a name="howto-tables-query"></a>How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="f6a66-410">資料表作業的常見需求是提供受限制的資料檢視。</span><span class="sxs-lookup"><span data-stu-id="f6a66-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="f6a66-411">例如，您可能會提供標有已驗證之使用者 ID 的資料表，因此您只能讀取或更新自己的記錄。</span><span class="sxs-lookup"><span data-stu-id="f6a66-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="f6a66-412">下列資料表定義提供這項功能：</span><span class="sxs-lookup"><span data-stu-id="f6a66-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="f6a66-413">正常執行的查詢作業，擁有供您使用 Where 子句來調整的查詢屬性。</span><span class="sxs-lookup"><span data-stu-id="f6a66-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="f6a66-414">查詢屬性是一種 [QueryJS] 物件，可用來將 OData 查詢轉換成資料後端可以處理的項目。</span><span class="sxs-lookup"><span data-stu-id="f6a66-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="f6a66-415">在簡單的等號比較案例中 (如同上例)，可以使用對應。</span><span class="sxs-lookup"><span data-stu-id="f6a66-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="f6a66-416">您也可以新增特定的 SQL 子句︰</span><span class="sxs-lookup"><span data-stu-id="f6a66-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="f6a66-417"><a name="howto-tables-softdelete"></a>作法：設定資料表上的虛刪除</span><span class="sxs-lookup"><span data-stu-id="f6a66-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="f6a66-418">虛刪除並不會實際刪除記錄。</span><span class="sxs-lookup"><span data-stu-id="f6a66-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="f6a66-419">它會將已刪除的資料行設定為 true，而將記錄標示為已在資料庫中刪除。</span><span class="sxs-lookup"><span data-stu-id="f6a66-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="f6a66-420">Azure Mobile Apps SDK 會自動從結果中移除已虛刪除的記錄，除非 Mobile Client SDK 使用 IncludeDeleted()。</span><span class="sxs-lookup"><span data-stu-id="f6a66-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="f6a66-421">若要為資料表設定虛刪除，請在資料表定義檔中設定 `softDelete` 屬性：</span><span class="sxs-lookup"><span data-stu-id="f6a66-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="f6a66-422">您應建立清除記錄的機制：從用戶端應用程式、透過 WebJob、Azure Function 或透過自訂 API。</span><span class="sxs-lookup"><span data-stu-id="f6a66-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="f6a66-423"><a name="howto-tables-seeding"></a>做法：在您的資料庫中植入資料</span><span class="sxs-lookup"><span data-stu-id="f6a66-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="f6a66-424">在建立新的應用程式時，您可能會想要在資料表中植入資料。</span><span class="sxs-lookup"><span data-stu-id="f6a66-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="f6a66-425">這可以在資料表定義 JavaScript 檔案中完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f6a66-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="f6a66-426">只有在 Azure Mobile Apps SDK 所建立的資料表中，才可執行資料植入。</span><span class="sxs-lookup"><span data-stu-id="f6a66-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="f6a66-427">如果資料表已存在於資料庫中，則不會在資料表中插入任何資料。</span><span class="sxs-lookup"><span data-stu-id="f6a66-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="f6a66-428">如果開啟動態結構描述，則會從植入的資料推斷結構描述。</span><span class="sxs-lookup"><span data-stu-id="f6a66-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="f6a66-429">建議您明確呼叫 `tables.initialize()` 方法，以在服務開始執行時建立資料表。</span><span class="sxs-lookup"><span data-stu-id="f6a66-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <span data-ttu-id="f6a66-430"><a name="Swagger"></a>作法：啟用 Swagger 支援</span><span class="sxs-lookup"><span data-stu-id="f6a66-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="f6a66-431">Azure App Service Mobile Apps 隨附內建 [Swagger] 支援。</span><span class="sxs-lookup"><span data-stu-id="f6a66-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="f6a66-432">若要啟用 Swagger 支援，請先安裝 swagger-ui 做為相依性：</span><span class="sxs-lookup"><span data-stu-id="f6a66-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="f6a66-433">安裝之後，您可以在 Azure Mobile Apps 建構函式中啟用 Swagger 支援：</span><span class="sxs-lookup"><span data-stu-id="f6a66-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="f6a66-434">您可能只想要在開發版本中啟用 Swagger 支援。</span><span class="sxs-lookup"><span data-stu-id="f6a66-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="f6a66-435">您可以使用 `NODE_ENV` 應用程式設定來執行這項工作：</span><span class="sxs-lookup"><span data-stu-id="f6a66-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="f6a66-436">swagger 端點位於 http://*yoursite*.azurewebsites.net/swagger。</span><span class="sxs-lookup"><span data-stu-id="f6a66-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="f6a66-437">您可以透過 `/swagger/ui` 端點存取 Swagger UI。</span><span class="sxs-lookup"><span data-stu-id="f6a66-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="f6a66-438">如果您選擇需要跨整個應用程式驗證，Swagger 會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f6a66-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="f6a66-439">為了獲得最佳結果，請在「Azure App Service 驗證/授權」設定中選擇允許未經驗證的要求通過，然後使用 `table.access` 屬性來控制驗證。</span><span class="sxs-lookup"><span data-stu-id="f6a66-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="f6a66-440">如果您想要只在本機進行開發時才使用 Swagger 支援，您也可以將 Swagger 選項新增到您的 `azureMobile.js` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="f6a66-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="f6a66-441"><a name="push">推播通知</span><span class="sxs-lookup"><span data-stu-id="f6a66-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="f6a66-442">Mobile Apps 會與 Azure 通知中樞整合，讓您能跨越所有主要平台，將目標推播通知傳送給數百萬部裝著。</span><span class="sxs-lookup"><span data-stu-id="f6a66-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="f6a66-443">藉由使用通知中樞，您可以傳送推播通知至 iOS、Android 和 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="f6a66-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="f6a66-444">若要深入了解您可以使用通知中樞執行的所有功能，請參閱 [通知中樞概觀](../notification-hubs/notification-hubs-push-notification-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f6a66-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="f6a66-445"></a><a name="send-push"></a>作法：傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="f6a66-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="f6a66-446">下列程式碼示範如何使用推播物件來傳送廣播推播通知給已註冊的 iOS 裝置︰</span><span class="sxs-lookup"><span data-stu-id="f6a66-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="f6a66-447">藉由從用戶端建立範本的推播註冊，您可以改為傳送範本推播訊息至所有支援平台上的裝置。</span><span class="sxs-lookup"><span data-stu-id="f6a66-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="f6a66-448">下列程式碼示範如何傳送範本通知︰</span><span class="sxs-lookup"><span data-stu-id="f6a66-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <span data-ttu-id="f6a66-449"><a name="push-user"></a>作法：使用標記將推播通知傳送給已驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="f6a66-449"><a name="push-user"></a>How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="f6a66-450">當驗證的使用者註冊推播通知之後，使用者識別碼便會自動加入到註冊中。</span><span class="sxs-lookup"><span data-stu-id="f6a66-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="f6a66-451">藉由使用這個標記，您可以傳送推播通知給特定使用者已註冊的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="f6a66-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="f6a66-452">下列程式碼會取得提出要求之使用者的 SID，並將範本推播通知傳送至該使用者的每個裝置註冊︰</span><span class="sxs-lookup"><span data-stu-id="f6a66-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="f6a66-453">在註冊來自已驗證用戶端的推播通知時，請確定驗證已完成，然後再嘗試註冊。</span><span class="sxs-lookup"><span data-stu-id="f6a66-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="f6a66-454"><a name="CustomAPI"></a> 自訂 API</span><span class="sxs-lookup"><span data-stu-id="f6a66-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="f6a66-455"><a name="howto-customapi-basic"></a>作法：定義自訂 API</span><span class="sxs-lookup"><span data-stu-id="f6a66-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="f6a66-456">除了透過 /tables 端點的資料存取 API 以外，Azure Mobile Apps 也可提供自訂 API 涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="f6a66-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="f6a66-457">自訂 API 會以類似於資料表定義的方法定義，並且可存取所有相同功能，包括驗證。</span><span class="sxs-lookup"><span data-stu-id="f6a66-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="f6a66-458">如果您想要在自訂 API 使用 App Service 驗證，就必須先在 [Azure 入口網站] 中設定 App Service 驗證。</span><span class="sxs-lookup"><span data-stu-id="f6a66-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="f6a66-459">如需關於在 Azure App Service 中設定驗證的詳細資訊，請參閱您要使用的識別提供者所提供的組態指南：</span><span class="sxs-lookup"><span data-stu-id="f6a66-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="f6a66-460">[如何設定 Azure Active Directory 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="f6a66-461">[如何設定 Facebook 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="f6a66-462">[如何設定 Google 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="f6a66-463">[如何設定 Microsoft 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="f6a66-464">[如何設定 Twitter 驗證]</span><span class="sxs-lookup"><span data-stu-id="f6a66-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="f6a66-465">定義自訂 API 的方法與資料表 API 很類似。</span><span class="sxs-lookup"><span data-stu-id="f6a66-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="f6a66-466">建立 [api]  目錄。</span><span class="sxs-lookup"><span data-stu-id="f6a66-466">Create an **api** directory</span></span>
2. <span data-ttu-id="f6a66-467">在 [api]  目錄中建立 API 定義 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="f6a66-468">使用匯入方法將 **api** 目錄匯入。</span><span class="sxs-lookup"><span data-stu-id="f6a66-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="f6a66-469">以下是根據我們先前使用的基本應用程式範例所做的原型 API 定義。</span><span class="sxs-lookup"><span data-stu-id="f6a66-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="f6a66-470">讓我們使用一個會透過 *Date.now()* 方法傳回伺服器日期的範例 API。</span><span class="sxs-lookup"><span data-stu-id="f6a66-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="f6a66-471">以下是 api/date.js 檔案：</span><span class="sxs-lookup"><span data-stu-id="f6a66-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="f6a66-472">每個參數都是標準 RESTful 動詞之一 - GET、POST、PATCH 或 DELETE。</span><span class="sxs-lookup"><span data-stu-id="f6a66-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="f6a66-473">此方法是會傳送必要輸出的標準 [ExpressJS 中介軟體] 函式。</span><span class="sxs-lookup"><span data-stu-id="f6a66-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <span data-ttu-id="f6a66-474"><a name="howto-customapi-auth"></a>做法：需經過驗證才能存取自訂 API</span><span class="sxs-lookup"><span data-stu-id="f6a66-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="f6a66-475">Azure Mobile Apps SDK 對於資料表端點和自訂 API 會使用相同的方式實作驗證。</span><span class="sxs-lookup"><span data-stu-id="f6a66-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="f6a66-476">若要在前一節開發的 API 中新增驗證，請新增 **access** 屬性：</span><span class="sxs-lookup"><span data-stu-id="f6a66-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="f6a66-477">您也可以指定特定作業的驗證：</span><span class="sxs-lookup"><span data-stu-id="f6a66-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="f6a66-478">對於需要驗證的自訂 API，必須使用資料表端點所使用的相同權杖。</span><span class="sxs-lookup"><span data-stu-id="f6a66-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="f6a66-479"><a name="howto-customapi-auth"></a>作法：處理大型檔案上傳</span><span class="sxs-lookup"><span data-stu-id="f6a66-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="f6a66-480">Azure Mobile Apps SDK 使用 [本文剖析器中介軟體](https://github.com/expressjs/body-parser) 來接受您提交的本文內容並加以解碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="f6a66-481">您可以預先設定讓本文剖析器接受較大的檔案上傳：</span><span class="sxs-lookup"><span data-stu-id="f6a66-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="f6a66-482">檔案會在傳輸之前經過 base-64 編碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="f6a66-483">這會增加實際上傳內容的大小 (也是您必須負擔的大小)。</span><span class="sxs-lookup"><span data-stu-id="f6a66-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <span data-ttu-id="f6a66-484"><a name="howto-customapi-sql"></a>作法：執行自訂 SQL 陳述式</span><span class="sxs-lookup"><span data-stu-id="f6a66-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="f6a66-485">Azure Mobile Apps SDK 允許透過要求物件存取整個「內容」，讓您能輕鬆地針對定義的資料提供者執行參數化的 SQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="f6a66-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="f6a66-486"><a name="Debugging"></a>偵錯、簡單資料表及簡單的 API</span><span class="sxs-lookup"><span data-stu-id="f6a66-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="f6a66-487"><a name="howto-diagnostic-logs"></a>作法：為 Azure Mobile Apps 偵錯、診斷和進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f6a66-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="f6a66-488">Azure App Service 提供數個適用於 Node.js 應用程式的偵錯和疑難排解技術。</span><span class="sxs-lookup"><span data-stu-id="f6a66-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="f6a66-489">若要開始針對您的 Node.js 行動後端進行疑難排解，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="f6a66-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="f6a66-490">[監視 Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="f6a66-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="f6a66-491">[在 Azure App Service 中啟用診斷記錄]</span><span class="sxs-lookup"><span data-stu-id="f6a66-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="f6a66-492">[在 Visual Studio 中疑難排解 Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="f6a66-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="f6a66-493">Node.js 應用程式可存取多種不同的診斷記錄工具。</span><span class="sxs-lookup"><span data-stu-id="f6a66-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="f6a66-494">在內部，Azure Mobile Apps Node.js SDK 會使用 [Winston] 進行診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="f6a66-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="f6a66-495">啟用偵錯模式，或是在 [Azure 入口網站]中將 **MS_DebugMode** 應用程式設定設為 true，即會自動啟用記錄功能。</span><span class="sxs-lookup"><span data-stu-id="f6a66-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="f6a66-496">產生的記錄檔會顯示在 [Azure 入口網站]上的診斷記錄中。</span><span class="sxs-lookup"><span data-stu-id="f6a66-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <span data-ttu-id="f6a66-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>作法：在 Azure 入口網站中使用簡單資料表</span><span class="sxs-lookup"><span data-stu-id="f6a66-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="f6a66-498">入口網站中的簡單資料表，可讓您直接在入口網站中建立及使用資料表。</span><span class="sxs-lookup"><span data-stu-id="f6a66-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="f6a66-499">您甚至可以使用 App Service 編輯器編輯資料表作業。</span><span class="sxs-lookup"><span data-stu-id="f6a66-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="f6a66-500">當您按一下後端網站設定中的 [簡單資料表]  時，可以新增、修改或刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="f6a66-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="f6a66-501">您也可以查看資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="f6a66-501">You can also see data in the table.</span></span>

![使用簡單資料表](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="f6a66-503">下列命令可用於資料表的命令列：</span><span class="sxs-lookup"><span data-stu-id="f6a66-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="f6a66-504">**變更權限** - 修改在資料表上讀取、插入、更新和刪除作業的權限。</span><span class="sxs-lookup"><span data-stu-id="f6a66-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span>
  <span data-ttu-id="f6a66-505">選項包括允許匿名存取、要求驗證，或停用作業的所有存取。</span><span class="sxs-lookup"><span data-stu-id="f6a66-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span>
* <span data-ttu-id="f6a66-506">**編輯指令碼** - 資料表的指令碼檔案會在 App Service 編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="f6a66-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="f6a66-507">**管理結構描述** - 新增或刪除資料行，或變更資料表索引。</span><span class="sxs-lookup"><span data-stu-id="f6a66-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="f6a66-508">**清除資料表** - 截斷現有的資料表可能會刪除所有資料列，但結構描述會維持不變。</span><span class="sxs-lookup"><span data-stu-id="f6a66-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="f6a66-509">**刪除資料列** - 刪除個別的資料列。</span><span class="sxs-lookup"><span data-stu-id="f6a66-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="f6a66-510">**檢視資料流記錄** - 將您連線到您網站的資料流記錄服務。</span><span class="sxs-lookup"><span data-stu-id="f6a66-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <span data-ttu-id="f6a66-511"><a name="work-easy-apis"></a>做法：在 Azure 入口網站中使用簡單 API</span><span class="sxs-lookup"><span data-stu-id="f6a66-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="f6a66-512">入口網站中的簡單 API，可讓您直接在入口網站中建立及使用自訂 API。</span><span class="sxs-lookup"><span data-stu-id="f6a66-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="f6a66-513">您可以使用 App Service 編輯器編輯 API 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f6a66-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="f6a66-514">當您按一下後端網站設定中的 [簡單資料表]  時，可以新增、修改或刪除自訂 API 端點。</span><span class="sxs-lookup"><span data-stu-id="f6a66-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![使用簡單 API](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="f6a66-516">在入口網站中，您可以變更指定 HTTP 動作的存取權限、在 App Service 編輯器中編輯 API 指令碼檔案，或檢視串流記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f6a66-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <span data-ttu-id="f6a66-517"><a name="online-editor"></a>作法：在 App Service 編輯器中編輯程式碼</span><span class="sxs-lookup"><span data-stu-id="f6a66-517"><a name="online-editor"></a>How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="f6a66-518">Azure 入口網站可讓您在 App Service 編輯器中編輯 Node.js 後端指令碼檔案，而不需將專案下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="f6a66-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="f6a66-519">若要在線上編輯器中編輯指令碼檔案：</span><span class="sxs-lookup"><span data-stu-id="f6a66-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="f6a66-520">在您的「行動應用程式」後端刀鋒視窗中，按一下 [所有設定] > [簡單資料表] 或 [簡單 API]，按一下資料表或 API，然後按一下 [編輯指令碼]。</span><span class="sxs-lookup"><span data-stu-id="f6a66-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="f6a66-521">指令碼檔案會在 App Service 編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="f6a66-521">The script file is opened in the App Service Editor.</span></span>

    ![App Service 編輯器](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="f6a66-523">在線上編輯器中變更程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="f6a66-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="f6a66-524">當您輸入資料時，會自動儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f6a66-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
<span data-ttu-id="f6a66-525">[Android 用戶端快速入門]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span></span>
<span data-ttu-id="f6a66-526">[Apache Cordova 用戶端快速入門]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="f6a66-527">[iOS 用戶端快速入門]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="f6a66-528">[Xamarin.iOS 用戶端快速入門]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="f6a66-529">[Xamarin.Android 用戶端快速入門]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="f6a66-530">[Xamarin.Forms 用戶端快速入門]: app-service-mobile-xamarin-forms-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span></span>
<span data-ttu-id="f6a66-531">[Windows 市集用戶端快速入門]: app-service-mobile-windows-store-dotnet-get-started.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span></span>
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
<span data-ttu-id="f6a66-532">[離線資料同步]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-532">[offline data sync]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="f6a66-533">[如何設定 Azure Active Directory 驗證]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-533">[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="f6a66-534">[如何設定 Facebook 驗證]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-534">[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="f6a66-535">[如何設定 Google 驗證]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-535">[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="f6a66-536">[如何設定 Microsoft 驗證]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-536">[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="f6a66-537">[如何設定 Twitter 驗證]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-537">[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
<span data-ttu-id="f6a66-538">[Azure App Service 部署指南]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="f6a66-539">[監視 Azure App Service]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-539">[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md</span></span>
<span data-ttu-id="f6a66-540">[在 Azure App Service 中啟用診斷記錄]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-540">[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="f6a66-541">[在 Visual Studio 中疑難排解 Azure App Service]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-541">[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span></span>
<span data-ttu-id="f6a66-542">[指定 Node 版本]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-542">[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md</span></span>
<span data-ttu-id="f6a66-543">[使用 Node 模組]: ../nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="f6a66-543">[use Node modules]: ../nodejs-use-node-modules-azure-apps.md</span></span>
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
<span data-ttu-id="f6a66-544">[Express]: http://expressjs.com/</span><span class="sxs-lookup"><span data-stu-id="f6a66-544">[Express]: http://expressjs.com/</span></span>
<span data-ttu-id="f6a66-545">[Swagger]: http://swagger.io/</span><span class="sxs-lookup"><span data-stu-id="f6a66-545">[Swagger]: http://swagger.io/</span></span>

<span data-ttu-id="f6a66-546">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="f6a66-546">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="f6a66-547">[OData]: http://www.odata.org</span><span class="sxs-lookup"><span data-stu-id="f6a66-547">[OData]: http://www.odata.org</span></span>
<span data-ttu-id="f6a66-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span><span class="sxs-lookup"><span data-stu-id="f6a66-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span></span>
<span data-ttu-id="f6a66-549">[GitHub 上的 basicapp 範例]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span><span class="sxs-lookup"><span data-stu-id="f6a66-549">[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span></span>
<span data-ttu-id="f6a66-550">[GitHub 上的待辦事項範例]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span><span class="sxs-lookup"><span data-stu-id="f6a66-550">[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span></span>
<span data-ttu-id="f6a66-551">[GitHub 上的範例目錄]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="f6a66-551">[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span></span>
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
<span data-ttu-id="f6a66-552">[QueryJS]: https://github.com/Azure/queryjs</span><span class="sxs-lookup"><span data-stu-id="f6a66-552">[QueryJS]: https://github.com/Azure/queryjs</span></span>
<span data-ttu-id="f6a66-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span><span class="sxs-lookup"><span data-stu-id="f6a66-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span></span>
<span data-ttu-id="f6a66-554">[mssql Node.js 封裝]: https://www.npmjs.com/package/mssql</span><span class="sxs-lookup"><span data-stu-id="f6a66-554">[mssql Node.js package]: https://www.npmjs.com/package/mssql</span></span>
<span data-ttu-id="f6a66-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span><span class="sxs-lookup"><span data-stu-id="f6a66-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span></span>
<span data-ttu-id="f6a66-556">[ExpressJS 中介軟體]: http://expressjs.com/guide/using-middleware.html</span><span class="sxs-lookup"><span data-stu-id="f6a66-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span></span>
<span data-ttu-id="f6a66-557">[Winston]: https://github.com/winstonjs/winston</span><span class="sxs-lookup"><span data-stu-id="f6a66-557">[Winston]: https://github.com/winstonjs/winston</span></span>
