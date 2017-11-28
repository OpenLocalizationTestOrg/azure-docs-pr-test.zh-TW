---
title: "與 hello Node.js 後端伺服器的行動應用程式 SDK 的 aaaHow toowork |Microsoft 文件"
description: "了解如何與 toowork hello Node.js 後端伺服器 SDK Azure App Service 行動應用程式。"
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
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="a5e79-103">如何 toouse hello Azure 行動應用程式 Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="a5e79-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="a5e79-104">本文章提供詳細的資訊和範例顯示如何 toowork Node.js 後端 Azure App Service 行動應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="a5e79-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="a5e79-105"><a name="Introduction"></a>簡介</span><span class="sxs-lookup"><span data-stu-id="a5e79-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="a5e79-106">Azure App Service 行動應用程式提供 hello 功能 tooadd 行動最佳化資料存取 Web API tooa web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5e79-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="a5e79-107">ASP.NET 和 Node.js web 應用程式提供 hello Azure App Service 行動應用程式 SDK。</span><span class="sxs-lookup"><span data-stu-id="a5e79-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="a5e79-108">hello SDK 提供 hello 下列作業：</span><span class="sxs-lookup"><span data-stu-id="a5e79-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="a5e79-109">資料存取的資料表作業 (讀取、插入、更新、刪除)</span><span class="sxs-lookup"><span data-stu-id="a5e79-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="a5e79-110">自訂 API 作業</span><span class="sxs-lookup"><span data-stu-id="a5e79-110">Custom API operations</span></span>

<span data-ttu-id="a5e79-111">這兩種作業都可用於 Azure App Service 所允許的所有識別提供者 (包括 Facebook、Twitter、Google 和 Microsoft 等社交識別提供者，以及用於企業身分識別的 Azure Active Directory) 之間的驗證。</span><span class="sxs-lookup"><span data-stu-id="a5e79-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="a5e79-112">您可以找到每個範例使用案例中 hello [GitHub 上的範例目錄]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="a5e79-113">支援的平台</span><span class="sxs-lookup"><span data-stu-id="a5e79-113">Supported Platforms</span></span>
<span data-ttu-id="a5e79-114">hello Azure 行動應用程式節點 SDK 支援的 hello LTS 目前版本的節點及更新版本。</span><span class="sxs-lookup"><span data-stu-id="a5e79-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="a5e79-115">撰寫、 hello 新版 LTS 為節點 v4.5.0。</span><span class="sxs-lookup"><span data-stu-id="a5e79-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="a5e79-116">其他版本的 Node 可能可以運作，但不受支援。</span><span class="sxs-lookup"><span data-stu-id="a5e79-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="a5e79-117">hello Azure 行動應用程式節點 SDK 支援兩個資料庫驅動程式-hello 節點 mssql 驅動程式支援 SQL Azure 和本機 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a5e79-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="a5e79-118">hello sqlite3 驅動程式的單一執行個體只支援 SQLite 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a5e79-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="a5e79-119"><a name="howto-cmdline-basicapp"></a>如何： 建立基本的 Node.js 後端使用 hello 命令列</span><span class="sxs-lookup"><span data-stu-id="a5e79-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="a5e79-120">每個 Azure App Service Mobile App Node.js 後端都會以 ExpressJS 應用程式的形式啟動。</span><span class="sxs-lookup"><span data-stu-id="a5e79-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="a5e79-121">ExpressJS 是 hello 熱門 web 服務架構，適用於 Node.js。</span><span class="sxs-lookup"><span data-stu-id="a5e79-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="a5e79-122">您可以依照下列方式建立基本的 [Express] 應用程式：</span><span class="sxs-lookup"><span data-stu-id="a5e79-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="a5e79-123">在命令或 PowerShell 視窗中，為您的專案建立目錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="a5e79-124">請執行 npm init tooinitialize hello 封裝結構。</span><span class="sxs-lookup"><span data-stu-id="a5e79-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="a5e79-125">hello npm init 命令會要求一組問題 tooinitialize hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="a5e79-126">請參閱 hello 範例輸出：</span><span class="sxs-lookup"><span data-stu-id="a5e79-126">See hello example output:</span></span>

    ![hello npm init 輸出][0]
3. <span data-ttu-id="a5e79-128">Hello npm 儲存機制安裝 hello 快速和 azure 行動應用程式程式庫。</span><span class="sxs-lookup"><span data-stu-id="a5e79-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="a5e79-129">建立 app.js 檔案 tooimplement hello 基本行動伺服器。</span><span class="sxs-lookup"><span data-stu-id="a5e79-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="a5e79-130">此應用程式建立行動裝置最佳化的 WebAPI 與單一端點 (`/tables/TodoItem`) 提供未驗證的存取 tooan 基礎 SQL 資料存放區中使用動態結構描述。</span><span class="sxs-lookup"><span data-stu-id="a5e79-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="a5e79-131">它適用於下列用戶端程式庫快速入門：</span><span class="sxs-lookup"><span data-stu-id="a5e79-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="a5e79-132">[Android 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="a5e79-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="a5e79-133">[Apache Cordova 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="a5e79-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="a5e79-134">[iOS 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="a5e79-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="a5e79-135">[Windows 市集用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="a5e79-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="a5e79-136">[Xamarin.iOS 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="a5e79-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="a5e79-137">[Xamarin.Android 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="a5e79-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="a5e79-138">[Xamarin.Forms 用戶端快速入門]</span><span class="sxs-lookup"><span data-stu-id="a5e79-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="a5e79-139">您可以在 hello 這個基本應用程式找到 hello 程式碼[GitHub 上的 basicapp 範例]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="a5e79-140"><a name="howto-vs2015-basicapp"></a>作法：使用 Visual Studio 2015 建立 Node 後端</span><span class="sxs-lookup"><span data-stu-id="a5e79-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="a5e79-141">Visual Studio 2015 需要 hello IDE 內延伸 toodevelop Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5e79-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="a5e79-142">toostart，安裝 hello [Node.js Tools 1.1 for Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="a5e79-143">一旦安裝 hello Node.js Tools for Visual Studio，建立 Express 4.x 應用程式：</span><span class="sxs-lookup"><span data-stu-id="a5e79-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="a5e79-144">開啟 hello**新專案**對話方塊 (從**檔案** > **新增** > **專案...**).</span><span class="sxs-lookup"><span data-stu-id="a5e79-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="a5e79-145">展開**範本** > **JavaScript** > **Node.js**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="a5e79-146">選取 hello**基本 Azure Node.js Express 4 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="a5e79-147">填寫 hello 專案名稱。</span><span class="sxs-lookup"><span data-stu-id="a5e79-147">Fill in hello project name.</span></span>  <span data-ttu-id="a5e79-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-148">Click *OK*.</span></span>

    ![Visual Studio 2015 新專案][1]
5. <span data-ttu-id="a5e79-150">以滑鼠右鍵按一下 hello **npm**節點，然後選取**安裝新的 npm 封裝...**.</span><span class="sxs-lookup"><span data-stu-id="a5e79-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="a5e79-151">您可能需要 toorefresh hello npm 目錄上建立第一個 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a5e79-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="a5e79-152">如有必要，請按一下 [重新整理]  。</span><span class="sxs-lookup"><span data-stu-id="a5e79-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="a5e79-153">輸入*azure 行動應用程式*hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="a5e79-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="a5e79-154">按一下 hello **azure 行動-應用程式 2.0.0**封裝，然後按一下 **安裝套件**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![安裝新的 npm 封裝][2]
8. <span data-ttu-id="a5e79-156">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-156">Click **Close**.</span></span>
9. <span data-ttu-id="a5e79-157">開啟 hello *app.js*檔案 hello Azure 行動應用程式 SDK 的 tooadd 支援。</span><span class="sxs-lookup"><span data-stu-id="a5e79-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="a5e79-158">底端列 6 at hello hello 程式庫需要陳述式，加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a5e79-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="a5e79-159">在大約列 27 之後 hello 其他 app.use 陳述式中，加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a5e79-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="a5e79-160">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-160">Save hello file.</span></span>
10. <span data-ttu-id="a5e79-161">請執行 hello 應用程式在本機 (hello http://localhost:3000 提供應用程式開發介面)，或發行 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a5e79-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="a5e79-162"><a name="create-node-backend-portal"></a>如何： 建立 Node.js 後端使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a5e79-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="a5e79-163">您可以建立行動裝置應用程式後端從右 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="a5e79-164">您可以依照下列步驟，或建立下列 hello 一起用戶端和伺服器 hello[建立行動應用程式](app-service-mobile-ios-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="a5e79-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="a5e79-165">hello 教學課程包含這些指示的簡化的版本，而且是最適合的專案概念證明。</span><span class="sxs-lookup"><span data-stu-id="a5e79-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="a5e79-166">在 hello*開始*刀鋒視窗底下**建立資料表 API**，選擇**Node.js**做為您**後端語言**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="a5e79-167">核取方塊 hello"**我了解此將覆寫所有網站內容。**"，然後按一下 **建立 TodoItem 資料表**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="a5e79-168"><a name="download-quickstart"></a>如何： 下載 hello Node.js 後端快速入門的程式碼專案使用 Git</span><span class="sxs-lookup"><span data-stu-id="a5e79-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="a5e79-169">當您建立 Node.js 行動裝置應用程式後端使用 hello 網站**快速入門**刀鋒視窗中，您與已部署的 tooyour 網站建立 Node.js 專案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="a5e79-170">您可以加入資料表和應用程式開發介面，並編輯 hello 入口網站中的 hello Node.js 後端的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="a5e79-171">您也可以使用各種部署工具 toodownload hello 後端專案，讓您可以新增或修改的資料表和應用程式開發介面，然後重新發行 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="a5e79-172">如需詳細資訊，請參閱 [Azure App Service 部署指南]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="a5e79-173">hello 下列程序使用 Git 儲存機制 toodownload hello 快速入門專案代碼。</span><span class="sxs-lookup"><span data-stu-id="a5e79-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="a5e79-174">如果尚未安裝 Git，請先安裝。</span><span class="sxs-lookup"><span data-stu-id="a5e79-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="a5e79-175">hello 步驟需要的 tooinstall Git 因作業系統不同。</span><span class="sxs-lookup"><span data-stu-id="a5e79-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="a5e79-176">如需作業系統特定的發佈和安裝指引，請參閱 [安裝 Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="a5e79-177">中的 hello 步驟[啟用 hello App Service 應用程式儲存機制](../app-service-web/app-service-deploy-local-git.md#Step3)tooenable hello Git 儲存機制，為您記下 hello 部署使用者名稱和密碼的後端網站。</span><span class="sxs-lookup"><span data-stu-id="a5e79-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="a5e79-178">在您的行動裝置應用程式後端 hello 刀鋒視窗，記下的 hello **Git 複製 URL**設定。</span><span class="sxs-lookup"><span data-stu-id="a5e79-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="a5e79-179">執行 hello`git clone`命令使用 hello Git 複製 URL，輸入您的密碼時所需，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="a5e79-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="a5e79-180">瀏覽 toolocal 目錄，即在上述範例中的 hello /todolist，並請注意，專案檔已下載。</span><span class="sxs-lookup"><span data-stu-id="a5e79-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="a5e79-181">找出 hello`todoitem.json`檔案在 hello`/tables`目錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="a5e79-182">該檔案定義了資料表上的權限。</span><span class="sxs-lookup"><span data-stu-id="a5e79-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="a5e79-183">也可以找到 hello`todoitem.js`相同檔案中 hello 定義 CRUD 作業 hello 資料表編寫指令碼的目錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="a5e79-184">您所做的變更 tooproject 檔案之後，執行下列命令 tooadd，認可，則上傳變更 toohello 站台的 hello:</span><span class="sxs-lookup"><span data-stu-id="a5e79-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="a5e79-185">當您新增新檔案 toohello 專案時，您必須先 tooexecute hello`git add .`命令。</span><span class="sxs-lookup"><span data-stu-id="a5e79-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="a5e79-186">每次一組新的認可已推送 toohello 站台重新發行 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="a5e79-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="a5e79-187"><a name="howto-publish-to-azure"></a>如何： 發行您的 Node.js 後端 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a5e79-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="a5e79-188">Microsoft Azure 提供許多發行您的 Azure App Service 行動應用程式 Node.js 後端，hello Azure 服務的機制。</span><span class="sxs-lookup"><span data-stu-id="a5e79-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="a5e79-189">其中包括使用整合至 Visual Studio 中的部署工具、命令列工具，和以原始檔控制為基礎的連續部署選項。</span><span class="sxs-lookup"><span data-stu-id="a5e79-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="a5e79-190">如需有關本主題的詳細資訊，請參閱 [Azure App Service 部署指南]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="a5e79-191">Azure App Service 提供 Node.js 應用程式方面的具體建議，您應該在部署之前先檢閱：</span><span class="sxs-lookup"><span data-stu-id="a5e79-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="a5e79-192">如何太[指定 hello 節點版本]</span><span class="sxs-lookup"><span data-stu-id="a5e79-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="a5e79-193">如何太[使用節點模組]</span><span class="sxs-lookup"><span data-stu-id="a5e79-193">How too[use Node modules]</span></span>

### <span data-ttu-id="a5e79-194"><a name="howto-enable-homepage"></a>作法：啟用應用程式的首頁</span><span class="sxs-lookup"><span data-stu-id="a5e79-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="a5e79-195">許多應用程式是 web 和行動裝置應用程式的組合，hello ExpressJS 架構可讓您 toocombine 兩個 facet。</span><span class="sxs-lookup"><span data-stu-id="a5e79-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="a5e79-196">有時候，不過，您可能希望 tooonly 實作行動裝置的介面。</span><span class="sxs-lookup"><span data-stu-id="a5e79-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="a5e79-197">有用的 tooprovide 登陸頁面 tooensure hello 應用程式服務已啟動並執行它。</span><span class="sxs-lookup"><span data-stu-id="a5e79-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="a5e79-198">您可以提供您自己的首頁，或啟用暫時的首頁。</span><span class="sxs-lookup"><span data-stu-id="a5e79-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="a5e79-199">tooenable 暫存的首頁上，使用下列 tooinstantiate Azure 行動應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="a5e79-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="a5e79-200">如果您只想使用此選項，在本機開發時，您可以加入此設定 tooyour`azureMobile.js`檔案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="a5e79-201"><a name="TableOperations"></a>資料表作業</span><span class="sxs-lookup"><span data-stu-id="a5e79-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="a5e79-202">hello azure 行動應用程式 Node.js 伺服器 SDK 提供機制 tooexpose 資料儲存為 WebAPI Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="a5e79-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="a5e79-203">提供的作業有五種。</span><span class="sxs-lookup"><span data-stu-id="a5e79-203">Five operations are provided.</span></span>

| <span data-ttu-id="a5e79-204">作業</span><span class="sxs-lookup"><span data-stu-id="a5e79-204">Operation</span></span> | <span data-ttu-id="a5e79-205">說明</span><span class="sxs-lookup"><span data-stu-id="a5e79-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5e79-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="a5e79-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="a5e79-207">取得 hello 資料表中的所有記錄</span><span class="sxs-lookup"><span data-stu-id="a5e79-207">Get all records in hello table</span></span> |
| <span data-ttu-id="a5e79-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="a5e79-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="a5e79-209">取得 hello 資料表中的特定記錄</span><span class="sxs-lookup"><span data-stu-id="a5e79-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="a5e79-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="a5e79-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="a5e79-211">建立 hello 資料表中的記錄</span><span class="sxs-lookup"><span data-stu-id="a5e79-211">Create a record in hello table</span></span> |
| <span data-ttu-id="a5e79-212">PATCH /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="a5e79-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="a5e79-213">更新 hello 資料表中的記錄</span><span class="sxs-lookup"><span data-stu-id="a5e79-213">Update a record in hello table</span></span> |
| <span data-ttu-id="a5e79-214">DELETE /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="a5e79-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="a5e79-215">刪除 hello 資料表中的記錄</span><span class="sxs-lookup"><span data-stu-id="a5e79-215">Delete a record in hello table</span></span> |

<span data-ttu-id="a5e79-216">支援這個 WebAPI [OData]並擴充 hello 資料表結構描述 toosupport[離線的資料同步]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="a5e79-217"><a name="howto-dynamicschema"></a>作法：使用動態結構描述定義資料表</span><span class="sxs-lookup"><span data-stu-id="a5e79-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="a5e79-218">資料表必須先經過定義才能使用。</span><span class="sxs-lookup"><span data-stu-id="a5e79-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="a5e79-219">資料表可以定義，使用靜態結構描述 （hello 開發人員定義 hello hello 結構描述內的資料行） 或動態 （hello SDK 控制項 hello 根據連入要求的結構描述）。</span><span class="sxs-lookup"><span data-stu-id="a5e79-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="a5e79-220">此外，hello 開發人員可以藉由新增 Javascript 程式碼 toohello 定義控制 hello WebAPI 的特定層面。</span><span class="sxs-lookup"><span data-stu-id="a5e79-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="a5e79-221">最佳做法，您應該在 hello 資料表目錄中，Javascript 檔案中定義的每個資料表，然後使用 tables.import() 方法 tooimport hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="a5e79-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="a5e79-222">擴充 hello basic 應用程式，會調整 hello app.js 檔案：</span><span class="sxs-lookup"><span data-stu-id="a5e79-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="a5e79-223">中的 hello 資料表定義。 / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="a5e79-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="a5e79-224">資料表依預設會使用動態結構描述。</span><span class="sxs-lookup"><span data-stu-id="a5e79-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="a5e79-225">關閉動態結構描述的 tooturn 全域設定 hello 應用程式設定**MS_DynamicSchema** toofalse hello Azure 入口網站中的。</span><span class="sxs-lookup"><span data-stu-id="a5e79-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="a5e79-226">您可以在 hello 找到完整的範例[GitHub 上的 todo 範例]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="a5e79-227"><a name="howto-staticschema"></a>作法：使用靜態結構描述定義資料表</span><span class="sxs-lookup"><span data-stu-id="a5e79-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="a5e79-228">您可以明確定義透過 hello WebAPI hello 資料行 tooexpose。</span><span class="sxs-lookup"><span data-stu-id="a5e79-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="a5e79-229">hello azure 行動應用程式 Node.js SDK 會自動將您提供的離線資料同步處理 toohello 清單所需的任何其他資料行。</span><span class="sxs-lookup"><span data-stu-id="a5e79-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="a5e79-230">例如，快速入門用戶端應用程式需要具有兩個資料行的資料表：文字 (字串) 和完整 (布林值)。</span><span class="sxs-lookup"><span data-stu-id="a5e79-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="a5e79-231">hello 資料表可以定義 hello 資料表定義 JavaScript 檔案中 （位於 hello 資料表目錄），如下所示：</span><span class="sxs-lookup"><span data-stu-id="a5e79-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="a5e79-232">如果您以靜態方式定義的資料表，然後您必須也 hello tables.initialize() 方法 toocreate hello 資料庫結構描述上呼叫啟動。</span><span class="sxs-lookup"><span data-stu-id="a5e79-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="a5e79-233">hello tables.initialize() 方法會傳回[承諾]以便 hello web 服務不會服務正在初始化 hello 資料庫之前，要求。</span><span class="sxs-lookup"><span data-stu-id="a5e79-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="a5e79-234"><a name="howto-sqlexpress-setup"></a>作法：以 SQL Express 作為本機電腦上的開發資料存放區</span><span class="sxs-lookup"><span data-stu-id="a5e79-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="a5e79-235">hello Azure 行動應用程式 hello AzureMobile 應用程式節點 SDK 提供三個選項來服務資料 hello 現成： SDK 提供 hello 現成提供資料的三個選項：</span><span class="sxs-lookup"><span data-stu-id="a5e79-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="a5e79-236">使用 hello**記憶體**驅動程式 tooprovide 非持續性範例存放區</span><span class="sxs-lookup"><span data-stu-id="a5e79-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="a5e79-237">使用 hello **mssql**驅動程式 tooprovide 開發 SQL Express 資料存放區</span><span class="sxs-lookup"><span data-stu-id="a5e79-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="a5e79-238">使用 hello **mssql**驅動程式 tooprovide 生產環境的 Azure SQL Database 資料存放區</span><span class="sxs-lookup"><span data-stu-id="a5e79-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="a5e79-239">hello Azure 行動應用程式 Node.js SDK 會使用 hello [mssql Node.js 封裝]tooestablish 及使用連線 tooboth SQL Express 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="a5e79-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="a5e79-240">要使用此封裝，您必須在 SQL Express 執行個體上啟用 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="a5e79-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="a5e79-241">hello 記憶體驅動程式不提供一組完整的測試。</span><span class="sxs-lookup"><span data-stu-id="a5e79-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="a5e79-242">如果您想 tootest 後端在本機，我們會建議 hello 使用 SQL Express 的資料存放區，且 hello mssql 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="a5e79-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="a5e79-243">下載並安裝 [Microsoft SQL Server 2014 Express]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="a5e79-244">請確定您安裝 hello SQL Server 2014 Express with Tools 版本。</span><span class="sxs-lookup"><span data-stu-id="a5e79-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="a5e79-245">除非您明確需要 64 位元支援，hello 32 位元版本執行時，就會耗用較少的記憶體。</span><span class="sxs-lookup"><span data-stu-id="a5e79-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="a5e79-246">執行 SQL Server 2014 組態管理員 hello。</span><span class="sxs-lookup"><span data-stu-id="a5e79-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="a5e79-247">展開 hello **SQL Server 網路組態**hello 左側的樹狀結構功能表中的節點。</span><span class="sxs-lookup"><span data-stu-id="a5e79-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="a5e79-248">按一下 [SQLEXPRESS 的通訊協定] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="a5e79-249">以滑鼠右鍵按一下 [TCP/IP]，然後選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="a5e79-250">按一下**確定**hello 快顯對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="a5e79-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="a5e79-251">以滑鼠右鍵按一下 [TCP/IP]，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="a5e79-252">按一下 hello **IP 位址** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a5e79-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="a5e79-253">尋找 hello **IPAll**節點。</span><span class="sxs-lookup"><span data-stu-id="a5e79-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="a5e79-254">在 hello **TCP 連接埠**欄位中，輸入**1433年**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="a5e79-255">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-255">Click **OK**.</span></span>  <span data-ttu-id="a5e79-256">按一下**確定**hello 快顯對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="a5e79-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="a5e79-257">按一下**SQL Server 服務**hello 左側的樹狀結構功能表中。</span><span class="sxs-lookup"><span data-stu-id="a5e79-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="a5e79-258">以滑鼠右鍵按一下 [SQL Server (SQLEXPRESS)]，然後選取 [重新啟動]</span><span class="sxs-lookup"><span data-stu-id="a5e79-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="a5e79-259">關閉 hello SQL Server 2014 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="a5e79-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="a5e79-260">執行 hello SQL Server 2014 Management Studio 並連接 tooyour 本機 SQL Express 執行個體</span><span class="sxs-lookup"><span data-stu-id="a5e79-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="a5e79-261">以滑鼠右鍵按一下您在 hello 物件總管 中的執行個體，然後選取**屬性**</span><span class="sxs-lookup"><span data-stu-id="a5e79-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="a5e79-262">選取 hello**安全性**頁面。</span><span class="sxs-lookup"><span data-stu-id="a5e79-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="a5e79-263">請確定 hello **SQL Server 及 Windows 驗證模式**選取</span><span class="sxs-lookup"><span data-stu-id="a5e79-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="a5e79-264">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="a5e79-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="a5e79-265">展開**安全性** > **登入**hello 物件總管 中</span><span class="sxs-lookup"><span data-stu-id="a5e79-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="a5e79-266">以滑鼠右鍵按一下 [登入]，然後選取 [新增登入...]</span><span class="sxs-lookup"><span data-stu-id="a5e79-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="a5e79-267">輸入登入名稱。</span><span class="sxs-lookup"><span data-stu-id="a5e79-267">Enter a Login name.</span></span>  <span data-ttu-id="a5e79-268">選取 [SQL Server 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="a5e79-269">輸入密碼，然後輸入 hello 相同密碼**確認密碼**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="a5e79-270">hello 密碼必須符合 Windows 複雜性需求。</span><span class="sxs-lookup"><span data-stu-id="a5e79-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="a5e79-271">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="a5e79-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="a5e79-272">以滑鼠右鍵按一下新的登入，然後選取 [屬性] </span><span class="sxs-lookup"><span data-stu-id="a5e79-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="a5e79-273">選取 hello**伺服器角色**頁面</span><span class="sxs-lookup"><span data-stu-id="a5e79-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="a5e79-274">檢查 hello 方塊的下一個 toohello **dbcreator**伺服器角色</span><span class="sxs-lookup"><span data-stu-id="a5e79-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="a5e79-275">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="a5e79-275">Click **OK**</span></span>
   13. <span data-ttu-id="a5e79-276">關閉 hello SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="a5e79-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="a5e79-277">請確定您記錄 hello 使用者名稱和您選取的密碼。</span><span class="sxs-lookup"><span data-stu-id="a5e79-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="a5e79-278">根據您特定資料庫的需求，您可能需要 tooassign 其他伺服器角色或權限。</span><span class="sxs-lookup"><span data-stu-id="a5e79-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="a5e79-279">hello Node.js 應用程式讀取 hello **SQLCONNSTR_MS_TableConnectionString** hello 這個資料庫的連接字串的環境變數。</span><span class="sxs-lookup"><span data-stu-id="a5e79-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="a5e79-280">您可以將該變數設定在環境中。</span><span class="sxs-lookup"><span data-stu-id="a5e79-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="a5e79-281">例如，您可以使用 PowerShell tooset 這個環境變數：</span><span class="sxs-lookup"><span data-stu-id="a5e79-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="a5e79-282">透過 TCP/IP 連接來存取 hello 資料庫和 hello 連線提供使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="a5e79-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="a5e79-283"><a name="howto-config-localdev"></a>作法：設定專案以在本機上進行開發</span><span class="sxs-lookup"><span data-stu-id="a5e79-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="a5e79-284">Azure 行動應用程式會讀取名為的 JavaScript 檔案*azureMobile.js*從 hello 本機檔案系統。</span><span class="sxs-lookup"><span data-stu-id="a5e79-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="a5e79-285">不使用在生產環境中的此檔案 tooconfigure hello Azure 行動應用程式 SDK-hello 內使用應用程式設定[Azure 入口網站]改為。</span><span class="sxs-lookup"><span data-stu-id="a5e79-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="a5e79-286">hello *azureMobile.js*檔案應該匯出的組態物件。</span><span class="sxs-lookup"><span data-stu-id="a5e79-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="a5e79-287">hello 最常見的設定如下：</span><span class="sxs-lookup"><span data-stu-id="a5e79-287">hello most common settings are:</span></span>

* <span data-ttu-id="a5e79-288">資料庫設定</span><span class="sxs-lookup"><span data-stu-id="a5e79-288">Database Settings</span></span>
* <span data-ttu-id="a5e79-289">診斷記錄設定</span><span class="sxs-lookup"><span data-stu-id="a5e79-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="a5e79-290">替代 CORS 設定</span><span class="sxs-lookup"><span data-stu-id="a5e79-290">Alternate CORS Settings</span></span>

<span data-ttu-id="a5e79-291">範例*azureMobile.js*檔案實作 hello 前面資料庫設定如下所示：</span><span class="sxs-lookup"><span data-stu-id="a5e79-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

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

<span data-ttu-id="a5e79-292">我們建議您新增*azureMobile.js* tooyour *.gitignore*檔案 （或其他忽略檔案原始程式碼控制） tooprevent hello 雲端中儲存的密碼。</span><span class="sxs-lookup"><span data-stu-id="a5e79-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="a5e79-293">永遠設定實際執行應用程式設定內 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="a5e79-294"><a name="howto-appsettings"></a>作法：設定行動應用程式的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="a5e79-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="a5e79-295">大部分的設定，在 hello *azureMobile.js*檔案具有對等的應用程式設定在 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="a5e79-296">在應用程式設定中使用下列清單 tooconfigure hello 您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="a5e79-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="a5e79-297">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="a5e79-297">App Setting</span></span> | <span data-ttu-id="a5e79-298">*azureMobile.js* 設定</span><span class="sxs-lookup"><span data-stu-id="a5e79-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="a5e79-299">說明</span><span class="sxs-lookup"><span data-stu-id="a5e79-299">Description</span></span> | <span data-ttu-id="a5e79-300">有效值</span><span class="sxs-lookup"><span data-stu-id="a5e79-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a5e79-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="a5e79-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="a5e79-302">名稱</span><span class="sxs-lookup"><span data-stu-id="a5e79-302">name</span></span> |<span data-ttu-id="a5e79-303">hello hello 應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="a5e79-303">hello name of hello app</span></span> |<span data-ttu-id="a5e79-304">字串</span><span class="sxs-lookup"><span data-stu-id="a5e79-304">string</span></span> |
| <span data-ttu-id="a5e79-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="a5e79-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="a5e79-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="a5e79-306">logging.level</span></span> |<span data-ttu-id="a5e79-307">最小的記錄層級的訊息 toolog</span><span class="sxs-lookup"><span data-stu-id="a5e79-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="a5e79-308">error、warning、info、verbose、debug、silly</span><span class="sxs-lookup"><span data-stu-id="a5e79-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="a5e79-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="a5e79-309">**MS_DebugMode**</span></span> |<span data-ttu-id="a5e79-310">debug</span><span class="sxs-lookup"><span data-stu-id="a5e79-310">debug</span></span> |<span data-ttu-id="a5e79-311">啟用或停用偵錯模式</span><span class="sxs-lookup"><span data-stu-id="a5e79-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="a5e79-312">true、false</span><span class="sxs-lookup"><span data-stu-id="a5e79-312">true, false</span></span> |
| <span data-ttu-id="a5e79-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="a5e79-313">**MS_TableSchema**</span></span> |<span data-ttu-id="a5e79-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="a5e79-314">data.schema</span></span> |<span data-ttu-id="a5e79-315">SQL 資料表的預設結構描述名稱</span><span class="sxs-lookup"><span data-stu-id="a5e79-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="a5e79-316">字串 (預設值：dbo)</span><span class="sxs-lookup"><span data-stu-id="a5e79-316">string (default: dbo)</span></span> |
| <span data-ttu-id="a5e79-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="a5e79-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="a5e79-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="a5e79-318">data.dynamicSchema</span></span> |<span data-ttu-id="a5e79-319">啟用或停用偵錯模式</span><span class="sxs-lookup"><span data-stu-id="a5e79-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="a5e79-320">true、false</span><span class="sxs-lookup"><span data-stu-id="a5e79-320">true, false</span></span> |
| <span data-ttu-id="a5e79-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="a5e79-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="a5e79-322">版本 (組 tooundefined)</span><span class="sxs-lookup"><span data-stu-id="a5e79-322">version (set tooundefined)</span></span> |<span data-ttu-id="a5e79-323">停用 hello X ZUMO-伺服器版本標頭</span><span class="sxs-lookup"><span data-stu-id="a5e79-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="a5e79-324">true、false</span><span class="sxs-lookup"><span data-stu-id="a5e79-324">true, false</span></span> |
| <span data-ttu-id="a5e79-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="a5e79-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="a5e79-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="a5e79-326">skipversioncheck</span></span> |<span data-ttu-id="a5e79-327">停用 hello 用戶端應用程式開發介面版本檢查</span><span class="sxs-lookup"><span data-stu-id="a5e79-327">Disables hello client API version check</span></span> |<span data-ttu-id="a5e79-328">true、false</span><span class="sxs-lookup"><span data-stu-id="a5e79-328">true, false</span></span> |

<span data-ttu-id="a5e79-329">tooset 應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="a5e79-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="a5e79-330">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="a5e79-331">選取**所有資源**或**應用程式服務**然後按一下 hello 行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="a5e79-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="a5e79-332">預設會開啟 hello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5e79-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="a5e79-333">如果沒有，請按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="a5e79-334">按一下**應用程式設定**hello 一般功能表中。</span><span class="sxs-lookup"><span data-stu-id="a5e79-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="a5e79-335">捲動 toohello 應用程式設定 區段。</span><span class="sxs-lookup"><span data-stu-id="a5e79-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="a5e79-336">如果您的應用程式設定已存在，請按一下 hello 應用程式設定 tooedit hello 值 hello 值。</span><span class="sxs-lookup"><span data-stu-id="a5e79-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="a5e79-337">如果您的應用程式設定不存在，請 hello 金鑰 方塊和 hello 值方塊中的 hello 值中輸入 hello 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="a5e79-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="a5e79-338">完成後，按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="a5e79-339">變更大部分的應用程式設定都需要重新啟動服務。</span><span class="sxs-lookup"><span data-stu-id="a5e79-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="a5e79-340"><a name="howto-use-sqlazure"></a>做法：使用 SQL Database 做為您的實際執行資料存放區</span><span class="sxs-lookup"><span data-stu-id="a5e79-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="a5e79-341">無論是何種 Azure App Service 應用程式類型，以 SQL Database 作為資料存放區的程序都是相同的。</span><span class="sxs-lookup"><span data-stu-id="a5e79-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="a5e79-342">如果您尚未執行此動作，請遵循這些步驟 toocreate 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="a5e79-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="a5e79-343">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="a5e79-344">在 [hello 左上方的 hello] 視窗中按一下 hello **+ 新增**按鈕 > **Web + 行動** > **行動裝置應用程式**，然後提供您的行動裝置應用程式後端的名稱。</span><span class="sxs-lookup"><span data-stu-id="a5e79-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="a5e79-345">在 hello**資源群組**方塊中，輸入您的應用程式的名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="a5e79-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="a5e79-346">選取 hello 預設應用程式服務計劃。</span><span class="sxs-lookup"><span data-stu-id="a5e79-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="a5e79-347">如果您想 toochange 您 App Service 方案，您可以按一下應用程式服務方案 hello > **+ 建立新**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="a5e79-348">提供 hello 新的 App Service 方案的名稱，然後選取適當的位置。</span><span class="sxs-lookup"><span data-stu-id="a5e79-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="a5e79-349">按一下 hello 定價層，然後選取適當的定價層 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="a5e79-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="a5e79-350">選取**檢視所有**tooview 多定價選項，例如**免費**和**共用**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="a5e79-351">一旦您選取的定價層，按一下 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a5e79-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="a5e79-352">在 hello **App Service 方案**刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="a5e79-353">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-353">Click **Create**.</span></span> <span data-ttu-id="a5e79-354">佈建行動應用程式後端可能需要幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="a5e79-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="a5e79-355">Hello 入口網站 hello 行動裝置應用程式後端會佈建之後，開啟 hello**設定**hello 行動裝置應用程式後端的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a5e79-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="a5e79-356">一旦建立 hello 行動裝置應用程式後端時，您可以選擇 tooeither 連接現有 SQL 資料庫 tooyour 行動裝置應用程式後端，或建立新的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a5e79-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="a5e79-357">在這一節中，您將建立 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="a5e79-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="a5e79-358">如果您已經有資料庫在 hello 與 hello 行動裝置應用程式後端相同的位置，您可以改為選擇**使用現有的資料庫**，然後選取該資料庫。</span><span class="sxs-lookup"><span data-stu-id="a5e79-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="a5e79-359">hello 使用不同的位置中的資料庫不會建議因為更高的延遲。</span><span class="sxs-lookup"><span data-stu-id="a5e79-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="a5e79-360">在 hello 新行動裝置應用程式後端中，按一下 **設定** > **行動裝置應用程式** > **資料** > **+ 加**.</span><span class="sxs-lookup"><span data-stu-id="a5e79-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="a5e79-361">在 hello**加入資料連接**刀鋒視窗中，按一下**SQL Database-必要的設定** > **建立新的資料庫**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="a5e79-362">輸入 hello hello 新資料庫名稱在 hello**名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="a5e79-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="a5e79-363">按一下 [伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-363">Click **Server**.</span></span>  <span data-ttu-id="a5e79-364">在 hello**新的伺服器**刀鋒視窗中，在 hello 中輸入唯一的伺服器名稱**伺服器名稱**欄位，並提供適合**Server 系統管理員登入**和**密碼**.</span><span class="sxs-lookup"><span data-stu-id="a5e79-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="a5e79-365">請確定**允許 azure 服務 tooaccess 伺服器**已核取。</span><span class="sxs-lookup"><span data-stu-id="a5e79-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="a5e79-366">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-366">Click **OK**.</span></span>

    ![建立 Azure SQL Database][6]
4. <span data-ttu-id="a5e79-368">在 hello**新資料庫**刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="a5e79-369">在 hello**加入資料連接**刀鋒視窗中，選取**連接字串**，輸入 hello 登入和建立 hello 資料庫時，您所提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="a5e79-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="a5e79-370">如果您使用現有的資料庫時，提供該資料庫 hello 登入認證。</span><span class="sxs-lookup"><span data-stu-id="a5e79-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="a5e79-371">輸入完成後，按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a5e79-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="a5e79-372">在 hello**加入資料連接**刀鋒視窗中，按一下**確定**toocreate hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a5e79-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="a5e79-373">建立 hello 資料庫可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="a5e79-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="a5e79-374">使用 hello**通知**hello 部署的區域 toomonitor hello 進度。</span><span class="sxs-lookup"><span data-stu-id="a5e79-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="a5e79-375">不進行直到 hello 資料庫已成功部署。</span><span class="sxs-lookup"><span data-stu-id="a5e79-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="a5e79-376">已成功部署之後，為行動後端應用程式設定中的 hello SQL Database 執行個體建立連接字串。</span><span class="sxs-lookup"><span data-stu-id="a5e79-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="a5e79-377">您可以看到這個應用程式中的設定 hello**設定** > **應用程式設定** > **連接字串**。</span><span class="sxs-lookup"><span data-stu-id="a5e79-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="a5e79-378"><a name="howto-tables-auth"></a>如何： 存取 tootables 要求進行驗證</span><span class="sxs-lookup"><span data-stu-id="a5e79-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="a5e79-379">如果您想與 hello 資料表端點 toouse 應用程式服務驗證，您必須設定應用程式服務驗證中 hello [Azure 入口網站]第一次。</span><span class="sxs-lookup"><span data-stu-id="a5e79-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="a5e79-380">在 Azure 應用程式服務中設定驗證的詳細檢閱 hello 身分識別提供者的設定指南 hello 想 toouse:</span><span class="sxs-lookup"><span data-stu-id="a5e79-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="a5e79-381">[如何 tooconfigure Azure Active Directory 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="a5e79-382">[如何 tooconfigure Facebook 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="a5e79-383">[如何 tooconfigure Google 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="a5e79-384">[如何 tooconfigure Microsoft 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="a5e79-385">[如何 tooconfigure Twitter 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="a5e79-386">每個資料表都可以使用的 toocontrol 存取 toohello 資料表存取屬性。</span><span class="sxs-lookup"><span data-stu-id="a5e79-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="a5e79-387">hello 下列範例會顯示為需要驗證的靜態定義的資料表。</span><span class="sxs-lookup"><span data-stu-id="a5e79-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="a5e79-388">hello 存取屬性可以接受三個值的其中一個</span><span class="sxs-lookup"><span data-stu-id="a5e79-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="a5e79-389">*匿名*表示 hello 用戶端應用程式允許未經驗證的 tooread 資料</span><span class="sxs-lookup"><span data-stu-id="a5e79-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="a5e79-390">*驗證*指示 hello 用戶端應用程式必須傳送有效的驗證 token 與 hello 要求</span><span class="sxs-lookup"><span data-stu-id="a5e79-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="a5e79-391">*disabled* 表示此資料表目前已停用</span><span class="sxs-lookup"><span data-stu-id="a5e79-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="a5e79-392">如果未定義 hello 存取屬性，則允許未驗證的存取。</span><span class="sxs-lookup"><span data-stu-id="a5e79-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="a5e79-393"><a name="howto-tables-getidentity"></a>作法：透過資料表使用驗證宣告</span><span class="sxs-lookup"><span data-stu-id="a5e79-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="a5e79-394">您可以設定驗證設定時所要求的各種宣告。</span><span class="sxs-lookup"><span data-stu-id="a5e79-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="a5e79-395">這些宣告不是通常可透過 hello`context.user`物件。</span><span class="sxs-lookup"><span data-stu-id="a5e79-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="a5e79-396">不過，他們可以使用擷取 hello`context.user.getIdentity()`方法。</span><span class="sxs-lookup"><span data-stu-id="a5e79-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="a5e79-397">hello`getIdentity()`方法傳回的承諾，解析 tooan 物件。</span><span class="sxs-lookup"><span data-stu-id="a5e79-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="a5e79-398">hello 物件，做為驗證方法 （facebook、 google、 twitter、 microsoftaccount 或 aad） 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a5e79-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="a5e79-399">例如，如果您設定 Microsoft 帳戶驗證與要求 hello 電子郵件地址宣告時，您可以加入 hello 電子郵件地址 toohello 記錄以下列資料表控制器的 hello:</span><span class="sxs-lookup"><span data-stu-id="a5e79-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

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
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="a5e79-400">toosee 哪些宣告可供使用，使用 web 瀏覽器 tooview hello`/.auth/me`網站的端點。</span><span class="sxs-lookup"><span data-stu-id="a5e79-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="a5e79-401"><a name="howto-tables-disabled"></a>如何： 停用存取 toospecific 資料表作業</span><span class="sxs-lookup"><span data-stu-id="a5e79-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="a5e79-402">加法 tooappearing hello 資料表上，在 hello 存取屬性可以使用的 toocontrol 個別作業。</span><span class="sxs-lookup"><span data-stu-id="a5e79-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="a5e79-403">共有四種作業：</span><span class="sxs-lookup"><span data-stu-id="a5e79-403">There are four operations:</span></span>

* <span data-ttu-id="a5e79-404">*讀取*hello RESTful 取得作業 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="a5e79-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="a5e79-405">*插入*hello 資料表 hello RESTful POST 作業</span><span class="sxs-lookup"><span data-stu-id="a5e79-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="a5e79-406">*更新*hello RESTful 修補作業 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="a5e79-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="a5e79-407">*刪除*hello 資料表上的 hello RESTful 刪除作業</span><span class="sxs-lookup"><span data-stu-id="a5e79-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="a5e79-408">例如，您可能希望 tooprovide 唯讀未經驗證的資料表：</span><span class="sxs-lookup"><span data-stu-id="a5e79-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="a5e79-409"><a name="howto-tables-query"></a>如何： 調整資料表作業所使用的 hello 查詢</span><span class="sxs-lookup"><span data-stu-id="a5e79-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="a5e79-410">資料表作業的共通需求是 tooprovide hello 資料的限制檢視。</span><span class="sxs-lookup"><span data-stu-id="a5e79-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="a5e79-411">例如，您可能會提供的資料表，則會標記為 hello 驗證使用者識別碼，使您可以只讀取或更新自己的記錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="a5e79-412">下列資料表定義的 hello 提供下列功能：</span><span class="sxs-lookup"><span data-stu-id="a5e79-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="a5e79-413">正常執行的查詢作業，擁有供您使用 Where 子句來調整的查詢屬性。</span><span class="sxs-lookup"><span data-stu-id="a5e79-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="a5e79-414">hello 查詢屬性是[QueryJS]物件，這個物件可以處理使用的 tooconvert hello 資料後端 OData 查詢 toosomething。</span><span class="sxs-lookup"><span data-stu-id="a5e79-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="a5e79-415">針對簡單的等號比較 （例如 hello 之前) 的情況下，可以使用對應。</span><span class="sxs-lookup"><span data-stu-id="a5e79-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="a5e79-416">您也可以新增特定的 SQL 子句︰</span><span class="sxs-lookup"><span data-stu-id="a5e79-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="a5e79-417"><a name="howto-tables-softdelete"></a>作法：設定資料表上的虛刪除</span><span class="sxs-lookup"><span data-stu-id="a5e79-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="a5e79-418">虛刪除並不會實際刪除記錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="a5e79-419">而是它將其標記為藉由設定 hello 刪除資料行 tootrue hello 資料庫中刪除。</span><span class="sxs-lookup"><span data-stu-id="a5e79-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="a5e79-420">除非 hello 行動用戶端 SDK 使用 IncludeDeleted() hello Azure 行動應用程式 SDK 會自動從結果移除虛刪除的記錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="a5e79-421">tooconfigure 軟體的資料表刪除，請設定 hello `softDelete` hello 資料表定義檔中的屬性：</span><span class="sxs-lookup"><span data-stu-id="a5e79-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="a5e79-422">您應建立清除記錄的機制：從用戶端應用程式、透過 WebJob、Azure Function 或透過自訂 API。</span><span class="sxs-lookup"><span data-stu-id="a5e79-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="a5e79-423"><a name="howto-tables-seeding"></a>做法：在您的資料庫中植入資料</span><span class="sxs-lookup"><span data-stu-id="a5e79-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="a5e79-424">當建立新的應用程式，您可能會想 tooseed 具有資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="a5e79-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="a5e79-425">作法是在 hello 資料表定義 JavaScript 檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a5e79-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
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

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="a5e79-426">只有執行植入的資料，當 hello 資料表由 hello Azure 行動應用程式 SDK。</span><span class="sxs-lookup"><span data-stu-id="a5e79-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="a5e79-427">Hello 資料表已經存在 hello 資料庫內，如果沒有資料會插入 hello 資料表中。</span><span class="sxs-lookup"><span data-stu-id="a5e79-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="a5e79-428">如果已開啟動態結構描述，結構描述會推斷 hello 植入資料。</span><span class="sxs-lookup"><span data-stu-id="a5e79-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="a5e79-429">我們建議您明確地呼叫 hello`tables.initialize()`方法 toocreate hello 資料表 hello 服務開始執行時。</span><span class="sxs-lookup"><span data-stu-id="a5e79-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="a5e79-430"><a name="Swagger"></a>作法：啟用 Swagger 支援</span><span class="sxs-lookup"><span data-stu-id="a5e79-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="a5e79-431">Azure App Service Mobile Apps 隨附內建 [Swagger] 支援。</span><span class="sxs-lookup"><span data-stu-id="a5e79-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="a5e79-432">tooenable Swagger 支援，請先安裝 hello swagger ui 做為相依性：</span><span class="sxs-lookup"><span data-stu-id="a5e79-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="a5e79-433">安裝之後，您可以啟用 Swagger hello Azure 行動應用程式建構函式中的支援：</span><span class="sxs-lookup"><span data-stu-id="a5e79-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="a5e79-434">您可能只想 tooenable Swagger 版本所支援之開發。</span><span class="sxs-lookup"><span data-stu-id="a5e79-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="a5e79-435">您可以使用 `NODE_ENV` 應用程式設定來執行這項工作：</span><span class="sxs-lookup"><span data-stu-id="a5e79-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="a5e79-436">hello swagger 端點位於 http://*您的站台*.azurewebsites.net/swagger。</span><span class="sxs-lookup"><span data-stu-id="a5e79-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="a5e79-437">您可以存取透過 hello hello Swagger UI`/swagger/ui`端點。</span><span class="sxs-lookup"><span data-stu-id="a5e79-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="a5e79-438">如果您選擇 toorequire 驗證整個應用程式之間，Swagger 會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a5e79-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="a5e79-439">為獲得最佳結果，選擇透過 tooallow 未經驗證的要求在 hello Azure 應用程式服務驗證 / 授權設定，然後控制驗證使用 hello`table.access`屬性。</span><span class="sxs-lookup"><span data-stu-id="a5e79-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="a5e79-440">您也可以加入 hello Swagger 選項 tooyour`azureMobile.js`檔案，如果您只想 Swagger 支援在本機開發時。</span><span class="sxs-lookup"><span data-stu-id="a5e79-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="a5e79-441"><a name="push">推播通知</span><span class="sxs-lookup"><span data-stu-id="a5e79-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="a5e79-442">行動應用程式整合了 Azure 通知中樞 tooenable 您的裝置為目標的 toosend 推播通知 toomillions 跨所有主要平台。</span><span class="sxs-lookup"><span data-stu-id="a5e79-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="a5e79-443">藉由使用通知中樞，您可以傳送推播通知 tooiOS、 Android 和 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="a5e79-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="a5e79-444">詳細資訊，您可以使用執行的 toolearn 通知中心，請參閱[通知中心概觀](../notification-hubs/notification-hubs-push-notification-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a5e79-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="a5e79-445"></a><a name="send-push"></a>作法：傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="a5e79-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="a5e79-446">hello，下列程式碼顯示如何 toouse hello 推播物件 toosend 廣播推播通知 tooregistered iOS 裝置：</span><span class="sxs-lookup"><span data-stu-id="a5e79-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="a5e79-447">藉由建立範本的推播登錄從 hello 用戶端，您可以改為傳送所有支援的平台上的範本推播訊息 toodevices。</span><span class="sxs-lookup"><span data-stu-id="a5e79-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="a5e79-448">hello 下列程式碼會示範如何 toosend 範本通知：</span><span class="sxs-lookup"><span data-stu-id="a5e79-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="a5e79-449"><a name="push-user"></a>如何： 傳送推播通知 tooan 驗證使用標記的使用者</span><span class="sxs-lookup"><span data-stu-id="a5e79-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="a5e79-450">當已驗證的使用者註冊推播通知時，使用者識別碼標籤會自動加入 toohello 註冊。</span><span class="sxs-lookup"><span data-stu-id="a5e79-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="a5e79-451">藉由使用此標記，您可以傳送推播通知 tooall 裝置已註冊的特定使用者。</span><span class="sxs-lookup"><span data-stu-id="a5e79-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="a5e79-452">hello 下列程式碼取得 hello 發出 hello 要求使用者的 SID，並將傳送範本推播通知 tooevery 裝置登錄該使用者：</span><span class="sxs-lookup"><span data-stu-id="a5e79-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="a5e79-453">在註冊來自已驗證用戶端的推播通知時，請確定驗證已完成，然後再嘗試註冊。</span><span class="sxs-lookup"><span data-stu-id="a5e79-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="a5e79-454"><a name="CustomAPI"></a> 自訂 API</span><span class="sxs-lookup"><span data-stu-id="a5e79-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="a5e79-455"><a name="howto-customapi-basic"></a>作法：定義自訂 API</span><span class="sxs-lookup"><span data-stu-id="a5e79-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="a5e79-456">此外 toohello 資料存取應用程式開發介面透過 hello /tables 端點，Azure 行動應用程式可以提供自訂應用程式開發介面的涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="a5e79-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="a5e79-457">自訂 Api 類似的方式 toohello 資料表定義中所定義，而且可以存取所有 hello 相同的功能，包括驗證。</span><span class="sxs-lookup"><span data-stu-id="a5e79-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="a5e79-458">如果您想 toouse 具有自訂 API 的應用程式服務驗證，您必須設定應用程式服務驗證中 hello [Azure 入口網站]第一次。</span><span class="sxs-lookup"><span data-stu-id="a5e79-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="a5e79-459">在 Azure 應用程式服務中設定驗證的詳細檢閱 hello 身分識別提供者的設定指南 hello 想 toouse:</span><span class="sxs-lookup"><span data-stu-id="a5e79-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="a5e79-460">[如何 tooconfigure Azure Active Directory 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="a5e79-461">[如何 tooconfigure Facebook 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="a5e79-462">[如何 tooconfigure Google 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="a5e79-463">[如何 tooconfigure Microsoft 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="a5e79-464">[如何 tooconfigure Twitter 驗證]</span><span class="sxs-lookup"><span data-stu-id="a5e79-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="a5e79-465">自訂 Api 會定義大致相同方式與 hello 資料表 API hello。</span><span class="sxs-lookup"><span data-stu-id="a5e79-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="a5e79-466">建立 [api]  目錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-466">Create an **api** directory</span></span>
2. <span data-ttu-id="a5e79-467">建立應用程式開發介面定義 JavaScript 檔案在 hello **api**目錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="a5e79-468">使用 hello 匯入方法 tooimport hello **api**目錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="a5e79-469">以下是我們先前使用的 hello basic 應用程式範例為基礎的 hello 原型 api 定義。</span><span class="sxs-lookup"><span data-stu-id="a5e79-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="a5e79-470">我們以範例應用程式開發介面中傳回 hello 伺服器的日期使用 hello *Date.now()*方法。</span><span class="sxs-lookup"><span data-stu-id="a5e79-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="a5e79-471">以下是 hello api/date.js 檔案：</span><span class="sxs-lookup"><span data-stu-id="a5e79-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="a5e79-472">每一個參數的其中一個 hello 標準 RESTful 指令動詞為 GET、 POST、 PATCH 或 DELETE。</span><span class="sxs-lookup"><span data-stu-id="a5e79-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="a5e79-473">hello 方法是一種標準[ExpressJS 中介軟體]傳送 hello 所需的輸出函式。</span><span class="sxs-lookup"><span data-stu-id="a5e79-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="a5e79-474"><a name="howto-customapi-auth"></a>如何： 存取 tooa 自訂 API 要求進行驗證</span><span class="sxs-lookup"><span data-stu-id="a5e79-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="a5e79-475">Azure 行動應用程式 SDK 實作驗證中 hello hello 表格端點和自訂應用程式開發介面的方式相同。</span><span class="sxs-lookup"><span data-stu-id="a5e79-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="a5e79-476">若要加入驗證 toohello API 開發 hello 前一節中，加入**存取**屬性：</span><span class="sxs-lookup"><span data-stu-id="a5e79-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="a5e79-477">您也可以指定特定作業的驗證：</span><span class="sxs-lookup"><span data-stu-id="a5e79-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="a5e79-478">hello 用於 hello 資料表端點的相同語彙基元必須用於需要驗證的自訂 Api。</span><span class="sxs-lookup"><span data-stu-id="a5e79-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="a5e79-479"><a name="howto-customapi-auth"></a>作法：處理大型檔案上傳</span><span class="sxs-lookup"><span data-stu-id="a5e79-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="a5e79-480">Azure 行動應用程式 SDK 會使用 hello[主體剖析器中介軟體](https://github.com/expressjs/body-parser)tooaccept 及解碼您上傳的本文內容。</span><span class="sxs-lookup"><span data-stu-id="a5e79-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="a5e79-481">您可以預先設定的內文剖析器 tooaccept 較大的檔案上傳：</span><span class="sxs-lookup"><span data-stu-id="a5e79-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="a5e79-482">base 64 編碼傳輸之前 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="a5e79-483">這會增加 hello hello 實際的上傳大小 （並因此 hello 必須負責的大小）。</span><span class="sxs-lookup"><span data-stu-id="a5e79-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="a5e79-484"><a name="howto-customapi-sql"></a>作法：執行自訂 SQL 陳述式</span><span class="sxs-lookup"><span data-stu-id="a5e79-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="a5e79-485">hello Azure 行動應用程式 SDK 可讓存取 toohello hello 要求物件，透過整個內容 tooexecute 可讓您輕鬆地參數化 SQL 陳述式 toohello 定義的資料提供者：</span><span class="sxs-lookup"><span data-stu-id="a5e79-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="a5e79-486"><a name="Debugging"></a>偵錯、簡單資料表及簡單的 API</span><span class="sxs-lookup"><span data-stu-id="a5e79-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="a5e79-487"><a name="howto-diagnostic-logs"></a>作法：為 Azure Mobile Apps 偵錯、診斷和進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="a5e79-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="a5e79-488">hello Azure 應用程式服務提供數個偵錯和疑難排解 Node.js 應用程式的技術。</span><span class="sxs-lookup"><span data-stu-id="a5e79-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="a5e79-489">請參閱下列文章 tooget 疑難排解 Node.js 行動後端啟動 toohello:</span><span class="sxs-lookup"><span data-stu-id="a5e79-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="a5e79-490">[監視 Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="a5e79-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="a5e79-491">[在 Azure App Service 中啟用診斷記錄]</span><span class="sxs-lookup"><span data-stu-id="a5e79-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="a5e79-492">[在 Visual Studio 中疑難排解 Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="a5e79-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="a5e79-493">Node.js 應用程式可存取 tooa 各種不同的診斷記錄檔工具。</span><span class="sxs-lookup"><span data-stu-id="a5e79-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="a5e79-494">就內部而言，使用 Azure 行動應用程式 Node.js SDK 的 hello[邱吉爾]的診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="a5e79-495">記錄會自動啟用啟用偵錯模式，或設定 hello **MS_DebugMode** hello 中的應用程式設定 tootrue [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="a5e79-496">產生的記錄檔會出現在 hello 診斷記錄檔上 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="a5e79-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>如何： 在 hello Azure 入口網站中使用簡單的資料表</span><span class="sxs-lookup"><span data-stu-id="a5e79-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="a5e79-498">Hello 入口網站中的簡單資料表可讓您建立和使用 hello 入口網站中的資料表權限。</span><span class="sxs-lookup"><span data-stu-id="a5e79-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="a5e79-499">您甚至可以編輯資料表作業使用 hello 應用程式服務的編輯器。</span><span class="sxs-lookup"><span data-stu-id="a5e79-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="a5e79-500">當您按一下後端網站設定中的 [簡單資料表]  時，可以新增、修改或刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="a5e79-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="a5e79-501">您也可以查看 hello 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="a5e79-501">You can also see data in hello table.</span></span>

![使用簡單資料表](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="a5e79-503">hello 下列命令可在資料表的 hello 命令列上：</span><span class="sxs-lookup"><span data-stu-id="a5e79-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="a5e79-504">**變更權限**-修改 hello 權限讀取、 插入、 更新及刪除 hello 資料表上的作業。</span><span class="sxs-lookup"><span data-stu-id="a5e79-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="a5e79-505">選項為 tooallow 匿名存取、 toorequire 驗證或 toodisable 所有存取 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="a5e79-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="a5e79-506">**編輯指令碼**-hello hello 資料表的指令碼檔案會在 hello 應用程式服務編輯器中開啟。</span><span class="sxs-lookup"><span data-stu-id="a5e79-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="a5e79-507">**管理結構描述**-新增或刪除資料行或變更 hello 資料表索引。</span><span class="sxs-lookup"><span data-stu-id="a5e79-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="a5e79-508">**清除資料表**-截斷現有的資料表不會刪除所有資料列，但又 hello 結構描述變更。</span><span class="sxs-lookup"><span data-stu-id="a5e79-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="a5e79-509">**刪除資料列** - 刪除個別的資料列。</span><span class="sxs-lookup"><span data-stu-id="a5e79-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="a5e79-510">**檢視資料流記錄**-將您連線 toohello 串流您的站台的記錄檔服務。</span><span class="sxs-lookup"><span data-stu-id="a5e79-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="a5e79-511"><a name="work-easy-apis"></a>如何： 在 hello Azure 入口網站中使用簡單的應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="a5e79-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="a5e79-512">Hello 入口網站中的簡單 Api 可讓您建立和使用 hello 入口網站中的自訂 Api 權限。</span><span class="sxs-lookup"><span data-stu-id="a5e79-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="a5e79-513">您可以編輯應用程式開發介面使用 hello 應用程式服務編輯器的指令碼。</span><span class="sxs-lookup"><span data-stu-id="a5e79-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="a5e79-514">當您按一下後端網站設定中的 [簡單資料表]  時，可以新增、修改或刪除自訂 API 端點。</span><span class="sxs-lookup"><span data-stu-id="a5e79-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![使用簡單 API](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="a5e79-516">在 hello 入口網站，您可以變更 hello 給定 HTTP 動作的存取權限、 編輯 hello API 指令碼檔案中的應用程式服務編輯器中，或是檢視 hello 串流記錄。</span><span class="sxs-lookup"><span data-stu-id="a5e79-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="a5e79-517"><a name="online-editor"></a>如何： hello 應用程式服務編輯器中編輯程式碼</span><span class="sxs-lookup"><span data-stu-id="a5e79-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="a5e79-518">hello Azure 入口網站可讓您編輯 hello 應用程式服務編輯器中的 Node.js 後端指令碼檔案，而不必下載 hello 專案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="a5e79-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="a5e79-519">tooedit hello 線上編輯器中的指令碼檔案：</span><span class="sxs-lookup"><span data-stu-id="a5e79-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="a5e79-520">在您的「行動應用程式」後端刀鋒視窗中，按一下 [所有設定] > [簡單資料表] 或 [簡單 API]，按一下資料表或 API，然後按一下 [編輯指令碼]。</span><span class="sxs-lookup"><span data-stu-id="a5e79-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="a5e79-521">hello 應用程式服務編輯器中開啟 hello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-521">hello script file is opened in hello App Service Editor.</span></span>

    ![App Service 編輯器](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="a5e79-523">Hello 線上編輯器中，讓您變更 toohello 的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="a5e79-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="a5e79-524">當您輸入資料時，會自動儲存變更。</span><span class="sxs-lookup"><span data-stu-id="a5e79-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android 用戶端快速入門]: app-service-mobile-android-get-started.md
[Apache Cordova 用戶端快速入門]: app-service-mobile-cordova-get-started.md
[iOS 用戶端快速入門]: app-service-mobile-ios-get-started.md
[Xamarin.iOS 用戶端快速入門]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android 用戶端快速入門]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms 用戶端快速入門]: app-service-mobile-xamarin-forms-get-started.md
[Windows 市集用戶端快速入門]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[離線的資料同步]: app-service-mobile-offline-data-sync.md
[如何 tooconfigure Azure Active Directory 驗證]: app-service-mobile-how-to-configure-active-directory-authentication.md
[如何 tooconfigure Facebook 驗證]: app-service-mobile-how-to-configure-facebook-authentication.md
[如何 tooconfigure Google 驗證]: app-service-mobile-how-to-configure-google-authentication.md
[如何 tooconfigure Microsoft 驗證]: app-service-mobile-how-to-configure-microsoft-authentication.md
[如何 tooconfigure Twitter 驗證]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service 部署指南]: ../app-service-web/web-sites-deploy.md
[監視 Azure App Service]: ../app-service-web/web-sites-monitor.md
[在 Azure App Service 中啟用診斷記錄]: ../app-service-web/web-sites-enable-diagnostic-log.md
[在 Visual Studio 中疑難排解 Azure App Service]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[指定 hello 節點版本]: ../nodejs-specify-node-version-azure-apps.md
[使用節點模組]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure 入口網站]: https://portal.azure.com/
[OData]: http://www.odata.org
[承諾]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[GitHub 上的 basicapp 範例]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[GitHub 上的 todo 範例]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[GitHub 上的範例目錄]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js 封裝]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS 中介軟體]: http://expressjs.com/guide/using-middleware.html
[邱吉爾]: https://github.com/winstonjs/winston
