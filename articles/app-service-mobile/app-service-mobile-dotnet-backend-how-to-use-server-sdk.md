---
title: "與 hello.NET 後端伺服器的行動應用程式 SDK 的 aaaHow toowork |Microsoft 文件"
description: "了解如何與 toowork hello Azure App Service 行動應用程式的.NET 後端伺服器 SDK。"
keywords: "App Service, Azure App Service, 行動應用程式, 行動服務, 調整, 可調整, 應用程式部署, Azure 應用程式部署"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="84b45-104">可搭配 hello.NET 後端伺服器 SDK 用於 Azure 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="84b45-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="84b45-105">本主題說明如何 toouse hello Azure App Service 行動應用程式的重要案例中的.NET 後端伺服器 SDK。</span><span class="sxs-lookup"><span data-stu-id="84b45-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="84b45-106">hello Azure 行動應用程式 SDK，可協助您使用從您的 ASP.NET 應用程式的行動用戶端。</span><span class="sxs-lookup"><span data-stu-id="84b45-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="84b45-107">hello [.NET server 的 Azure 行動應用程式 SDK] [ 2]是開放原始碼 GitHub 上的。</span><span class="sxs-lookup"><span data-stu-id="84b45-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="84b45-108">hello 儲存機制] 含有包括 hello 整部伺服器 SDK 的單元測試套件和某些範例專案的所有原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="84b45-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="84b45-109">參考文件</span><span class="sxs-lookup"><span data-stu-id="84b45-109">Reference documentation</span></span>
<span data-ttu-id="84b45-110">hello hello server SDK 的參考文件集位於此處： [Azure 行動應用程式的.NET 參考][1]。</span><span class="sxs-lookup"><span data-stu-id="84b45-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="84b45-111"><a name="create-app"></a>作法：建立 .NET 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="84b45-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="84b45-112">如果您要啟動新的專案，您可以建立 App Service 應用程式使用任一 hello [Azure 入口網站]或 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="84b45-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="84b45-113">您可以在本機執行 hello App Service 應用程式，或發行 hello 專案 tooyour 雲端 App Service 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="84b45-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="84b45-114">如果您要加入行動功能 tooan 現有專案，請參閱 hello[下載，並初始化 hello SDK](#install-sdk) > 一節。</span><span class="sxs-lookup"><span data-stu-id="84b45-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="84b45-115">建立.NET 後端使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="84b45-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="84b45-116">toocreate App Service 行動後端，請遵循 hello[快速入門教學課程][ 3]或遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84b45-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="84b45-117">在 [hello*開始*刀鋒視窗底下**建立資料表 API**，選擇**C#**做為您**後端語言**。</span><span class="sxs-lookup"><span data-stu-id="84b45-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="84b45-118">按一下**下載**、 擷取壓縮的專案檔案 tooyour 本機電腦，並在 Visual Studio 中開啟 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="84b45-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="84b45-119">使用 Visual Studio 2013 和 Visual Studio 2015 建立 .NET 後端</span><span class="sxs-lookup"><span data-stu-id="84b45-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="84b45-120">安裝 hello [Azure SDK for.NET] [ 4] (2.9.0 版本或更新版本) toocreate Visual Studio 中的 Azure 行動應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="84b45-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="84b45-121">一旦您已安裝 hello SDK，建立 ASP.NET 應用程式使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84b45-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="84b45-122">開啟 hello**新專案**對話方塊 (從*檔案* > **新增** > **專案...**).</span><span class="sxs-lookup"><span data-stu-id="84b45-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="84b45-123">展開 [範本] > [Visual C#]，然後選取 [Web]。</span><span class="sxs-lookup"><span data-stu-id="84b45-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="84b45-124">選取 [ASP.NET Web 應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="84b45-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="84b45-125">填寫 hello 專案名稱。</span><span class="sxs-lookup"><span data-stu-id="84b45-125">Fill in hello project name.</span></span> <span data-ttu-id="84b45-126">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="84b45-126">Then click **OK**.</span></span>
5. <span data-ttu-id="84b45-127">在 [ASP.NET 4.5.2 範本] 底下，選取 [Azure 行動應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84b45-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="84b45-128">請檢查**hello 雲端中的主機**toocreate 行動後端中 hello 雲端 toowhich 可以發行這個專案。</span><span class="sxs-lookup"><span data-stu-id="84b45-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="84b45-129">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="84b45-129">Click **OK**.</span></span>

## <span data-ttu-id="84b45-130"><a name="install-sdk"></a>如何： 下載並初始化 hello SDK</span><span class="sxs-lookup"><span data-stu-id="84b45-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="84b45-131">hello 是否可以使用 SDK [NuGet.org]。此套件包含 hello 所需的基底功能 tooget 開始使用 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="84b45-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="84b45-132">tooinitialize hello SDK，您需要在 hello tooperform 動作**HttpConfiguration**物件。</span><span class="sxs-lookup"><span data-stu-id="84b45-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="84b45-133">安裝 SDK hello</span><span class="sxs-lookup"><span data-stu-id="84b45-133">Install hello SDK</span></span>
<span data-ttu-id="84b45-134">tooinstall hello SDK，以滑鼠右鍵按一下 hello 伺服器專案，在 Visual Studio 中，選取**管理 NuGet 封裝**，搜尋 hello [Microsoft.Azure.Mobile.Server]封裝，然後按一下 [ **安裝**。</span><span class="sxs-lookup"><span data-stu-id="84b45-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="84b45-135"><a name="server-project-setup"></a>初始化 hello 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="84b45-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="84b45-136">.NET 後端伺服器專案是初始化類似 tooother ASP.NET 專案，包括 OWIN 啟動類別。</span><span class="sxs-lookup"><span data-stu-id="84b45-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="84b45-137">請確認您擁有參考 hello NuGet 封裝`Microsoft.Owin.Host.SystemWeb`。</span><span class="sxs-lookup"><span data-stu-id="84b45-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="84b45-138">tooadd 這個類別，在 Visual Studio 中，以滑鼠右鍵按一下您的伺服器專案並選取**新增** >
**新項目**，然後**Web**  >  **一般** > **OWIN 啟動 「 類別**。</span><span class="sxs-lookup"><span data-stu-id="84b45-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="84b45-139">類別會產生以 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="84b45-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="84b45-140">在 [hello`Configuration()`您 OWIN 啟動類別方法，使用**HttpConfiguration**物件 tooconfigure hello Azure 行動應用程式環境。</span><span class="sxs-lookup"><span data-stu-id="84b45-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="84b45-141">下列範例中的 hello 初始化 hello 伺服器專案，沒有新增的功能：</span><span class="sxs-lookup"><span data-stu-id="84b45-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="84b45-142">tooenable 個別功能，您必須呼叫擴充方法 hello **MobileAppConfiguration**物件之前先呼叫**ApplyTo**。</span><span class="sxs-lookup"><span data-stu-id="84b45-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="84b45-143">例如，下列程式碼的 hello 加入 hello 預設路由傳送的 hello 屬性 tooall API 控制器`[MobileAppController]`初始化期間：</span><span class="sxs-lookup"><span data-stu-id="84b45-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="84b45-144">從 hello 伺服器快速入門 hello Azure 入口網站呼叫**UseDefaultConfiguration()**。</span><span class="sxs-lookup"><span data-stu-id="84b45-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="84b45-145">安裝此對等 toohello:</span><span class="sxs-lookup"><span data-stu-id="84b45-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="84b45-146">使用的 hello 擴充方法是：</span><span class="sxs-lookup"><span data-stu-id="84b45-146">hello extension methods used are:</span></span>

* <span data-ttu-id="84b45-147">`AddMobileAppHomeController()`提供 hello 預設 Azure 行動應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="84b45-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="84b45-148">`MapApiControllers()`提供自訂 API 功能以 hello 裝飾 WebAPI 控制器`[MobileAppController]`屬性。</span><span class="sxs-lookup"><span data-stu-id="84b45-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="84b45-149">`AddTables()`提供的 hello 對應`/tables`端點 tootable 控制站。</span><span class="sxs-lookup"><span data-stu-id="84b45-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="84b45-150">`AddTablesWithEntityFramework()`是對應 hello 速記`/tables`使用 Entity Framework 的端點基礎控制站。</span><span class="sxs-lookup"><span data-stu-id="84b45-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="84b45-151">`AddPushNotifications()` 提供向通知中樞註冊裝置的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="84b45-152">`MapLegacyCrossDomainController()` 提供用於本機開發的標準 CORS 標頭。</span><span class="sxs-lookup"><span data-stu-id="84b45-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="84b45-153">SDK 延伸模組</span><span class="sxs-lookup"><span data-stu-id="84b45-153">SDK extensions</span></span>
<span data-ttu-id="84b45-154">下列 NuGet 基礎的擴充功能封裝 hello 提供各種可供您的應用程式的行動裝置功能。</span><span class="sxs-lookup"><span data-stu-id="84b45-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="84b45-155">在初始化期間啟用擴充功能使用 hello **MobileAppConfiguration**物件。</span><span class="sxs-lookup"><span data-stu-id="84b45-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="84b45-156">[Microsoft.Azure.Mobile.Server.Quickstart]支援 hello 基本的行動應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="84b45-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="84b45-157">組態設定加入的 toohello 呼叫 hello **UseDefaultConfiguration**初始化期間的擴充方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="84b45-158">此擴充包含下列擴充功能：通知、驗證、實體、資料表、跨網域和首頁封裝。</span><span class="sxs-lookup"><span data-stu-id="84b45-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="84b45-159">此套件會使用 hello hello Azure 入口網站上的行動應用程式快速入門。</span><span class="sxs-lookup"><span data-stu-id="84b45-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="84b45-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/)實作 hello 預設*此行動裝置應用程式已啟動並執行頁面*hello 網站根目錄。</span><span class="sxs-lookup"><span data-stu-id="84b45-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="84b45-161">藉由呼叫加入 toohello 組態**AddMobileAppHomeController**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="84b45-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/)包括資料和設定總 hello 資料管線中的類別。</span><span class="sxs-lookup"><span data-stu-id="84b45-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="84b45-163">加入呼叫 hello toohello 組態**AddTables**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="84b45-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/)啟用 hello SQL Database 中的 hello Entity Framework tooaccess 資料。</span><span class="sxs-lookup"><span data-stu-id="84b45-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="84b45-165">加入呼叫 hello toohello 組態**AddTablesWithEntityFramework**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="84b45-166">[Microsoft.Azure.Mobile.Server.Authentication]啟用驗證並設定總 hello OWIN 中介軟體使用 toovalidate 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="84b45-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="84b45-167">加入呼叫 hello toohello 組態**AddAppServiceAuthentication**和**IAppBuilder**。**UseAppServiceAuthentication**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="84b45-168">[Microsoft.Azure.Mobile.Server.Notifications] 啟用推播通知，並定義推播註冊端點。</span><span class="sxs-lookup"><span data-stu-id="84b45-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="84b45-169">加入呼叫 hello toohello 組態**AddPushNotifications**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="84b45-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/)會建立可從您的行動裝置應用程式的網頁瀏覽器做資料 toolegacy 控制站。</span><span class="sxs-lookup"><span data-stu-id="84b45-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="84b45-171">藉由呼叫加入 toohello 組態**MapLegacyCrossDomainController**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="84b45-172">[Microsoft.Azure.Mobile.Server.Login]提供 hello AppServiceLoginHandler.CreateToken() 方法，這是自訂的驗證案例期間使用的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="84b45-173"><a name="publish-server-project"></a>如何： 將 hello 伺服器專案發行</span><span class="sxs-lookup"><span data-stu-id="84b45-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="84b45-174">本節說明如何 toopublish.NET 後端專案從 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="84b45-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="84b45-175">您也可以部署您的後端專案使用 Git 或任一 hello hello 中涵蓋的其他方法[Azure App Service 部署文件](../app-service-web/web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="84b45-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="84b45-176">在 Visual Studio 中，重建 hello 專案 toorestore NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="84b45-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="84b45-177">在 [方案總管] 中，以滑鼠右鍵按一下 hello 專案中，按一下 [**發行**。</span><span class="sxs-lookup"><span data-stu-id="84b45-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="84b45-178">hello 第一次發行時，您需要 toodefine 發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="84b45-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="84b45-179">在定義設定檔後，您可以選取該設定檔，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="84b45-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="84b45-180">如果系統詢問 tooselect 發行目標，請按一下**Microsoft Azure App Service** > **下一步**，（如果需要），然後使用您的 Azure 認證登入。</span><span class="sxs-lookup"><span data-stu-id="84b45-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="84b45-181">Visual Studio 會直接從 Azure 下載並安全地儲存您的發佈設定。</span><span class="sxs-lookup"><span data-stu-id="84b45-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="84b45-182">選擇您的 [訂用帳戶]，從 [檢視] 中選取 [資源類型]，展開 [行動應用程式]，按一下您的行動應用程式後端，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="84b45-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="84b45-183">確認 hello 發行設定檔資訊，然後按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="84b45-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="84b45-184">當您的行動應用程式後端已成功發佈後，您會看到表示成功的登陸頁面。</span><span class="sxs-lookup"><span data-stu-id="84b45-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="84b45-185"><a name="define-table-controller"></a> 做法：定義資料表控制器</span><span class="sxs-lookup"><span data-stu-id="84b45-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="84b45-186">定義資料表控制器 tooexpose SQL 資料表 toomobile 用戶端。</span><span class="sxs-lookup"><span data-stu-id="84b45-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="84b45-187">設定資料表控制器需要三個步驟︰</span><span class="sxs-lookup"><span data-stu-id="84b45-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="84b45-188">建立資料傳輸物件 (DTO) 類別。</span><span class="sxs-lookup"><span data-stu-id="84b45-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="84b45-189">Hello 行動 DbContext 類別中設定的資料表參考。</span><span class="sxs-lookup"><span data-stu-id="84b45-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="84b45-190">建立資料表控制器。</span><span class="sxs-lookup"><span data-stu-id="84b45-190">Create a table controller.</span></span>

<span data-ttu-id="84b45-191">資料傳輸物件 (DTO) 是繼承自 `EntityData`純 C# 物件。</span><span class="sxs-lookup"><span data-stu-id="84b45-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="84b45-192">例如：</span><span class="sxs-lookup"><span data-stu-id="84b45-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="84b45-193">hello DTO 是使用的 toodefine hello SQL database 中的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="84b45-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="84b45-194">toocreate hello 資料庫項目，加入`DbSet<>`hello DbContext 您使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="84b45-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="84b45-195">在 [hello 預設 Azure 行動應用程式的專案範本，hello DbContext 稱為`Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="84b45-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="84b45-196">如果您擁有的 hello 安裝 Azure SDK，您現在可以建立範本資料表控制器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="84b45-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="84b45-197">Hello 控制器] 資料夾上按一下滑鼠右鍵，然後選取**新增** > **控制器...**.</span><span class="sxs-lookup"><span data-stu-id="84b45-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="84b45-198">選取 hello **Azure 行動應用程式資料表控制器**選項，然後按一下 [**新增**。</span><span class="sxs-lookup"><span data-stu-id="84b45-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="84b45-199">在 [hello**加入控制器**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="84b45-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="84b45-200">在 [hello**模型類別**下拉式清單中，選取您新 DTO。</span><span class="sxs-lookup"><span data-stu-id="84b45-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="84b45-201">在 [hello **DbContext**下拉式清單中，選取 hello 行動服務 DbContext 類別。</span><span class="sxs-lookup"><span data-stu-id="84b45-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="84b45-202">為您建立 hello 控制器名稱。</span><span class="sxs-lookup"><span data-stu-id="84b45-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="84b45-203">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="84b45-203">Click **Add**.</span></span>

<span data-ttu-id="84b45-204">hello 快速入門伺服器專案包含簡單的範例**TodoItemController**。</span><span class="sxs-lookup"><span data-stu-id="84b45-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="84b45-205"><a name="adjust-pagesize"></a>如何： 調整 hello 表格分頁大小</span><span class="sxs-lookup"><span data-stu-id="84b45-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="84b45-206">根據預設，Azure Mobile Apps 針對每個要求會傳回 50 個記錄。</span><span class="sxs-lookup"><span data-stu-id="84b45-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="84b45-207">分頁可確保該 hello 用戶端不會不佔用太久，其 UI 執行緒，也不 hello 伺服器確保良好的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="84b45-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="84b45-208">toochange hello 資料表分頁大小增加 hello 伺服器端 「 允許查詢大小 」 和 hello 「 允許查詢大小 」 的用戶端頁面大小 hello 伺服器端會調整使用 hello`EnableQuery`屬性：</span><span class="sxs-lookup"><span data-stu-id="84b45-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="84b45-209">確定 hello PageSize hello 相同或大於 hello hello 用戶端要求的大小。</span><span class="sxs-lookup"><span data-stu-id="84b45-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="84b45-210">如需變更 hello 用戶端頁面大小的詳細資訊，請參閱 toohello 特定用戶端如何文件。</span><span class="sxs-lookup"><span data-stu-id="84b45-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="84b45-211">做法：定義自訂 API 控制器</span><span class="sxs-lookup"><span data-stu-id="84b45-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="84b45-212">自訂 API 控制器 hello 提供 hello 最基本功能 tooyour 行動裝置應用程式後端所公開的端點。</span><span class="sxs-lookup"><span data-stu-id="84b45-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="84b45-213">您可以註冊行動裝置特定 API 控制器會使用 hello [MobileAppController] 屬性。</span><span class="sxs-lookup"><span data-stu-id="84b45-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="84b45-214">hello`MobileAppController`屬性註冊 hello 路由、 設定 hello 行動應用程式的 JSON 序列化程式，並開啟[用戶端版本檢查](app-service-mobile-client-and-server-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="84b45-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="84b45-215">在 Visual Studio 中，以滑鼠右鍵按一下 hello Controllers 資料夾，然後按一下 [**新增** > **控制器**，選取**Web API 2 控制器&mdash;空**和按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="84b45-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="84b45-216">提供 [控制器名稱] \(例如 `CustomController`)，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="84b45-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="84b45-217">在 [hello 新控制器的類別檔案，加入 [hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="84b45-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="84b45-218">套用 hello **[MobileAppController]**屬性 toohello API 控制器類別定義，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="84b45-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="84b45-219">App_Start/Startup.MobileApp.cs 檔案中加入呼叫 toohello **MapApiControllers**擴充方法，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="84b45-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="84b45-220">您也可以使用 hello`UseDefaultConfiguration()`擴充方法，而不是`MapApiControllers()`。</span><span class="sxs-lookup"><span data-stu-id="84b45-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="84b45-221">用戶端仍然可以存取任何沒有套用 **MobileAppControllerAttribute** 的控制器，但是使用任何行動應用程式用戶端 SDK 的用戶端可能會無法正確取用。</span><span class="sxs-lookup"><span data-stu-id="84b45-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="84b45-222">做法：使用驗證</span><span class="sxs-lookup"><span data-stu-id="84b45-222">How to: Work with authentication</span></span>
<span data-ttu-id="84b45-223">Azure 行動應用程式會使用應用程式服務驗證 / 授權 toosecure 行動後端。</span><span class="sxs-lookup"><span data-stu-id="84b45-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="84b45-224">這個區段會顯示如何 tooperform hello 下列驗證相關的工作，在.NET 後端伺服器專案中：</span><span class="sxs-lookup"><span data-stu-id="84b45-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="84b45-225">如何： 加入驗證 tooa 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="84b45-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="84b45-226">做法：針對應用程式使用自訂驗證</span><span class="sxs-lookup"><span data-stu-id="84b45-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="84b45-227">做法：取出已驗證的使用者資訊</span><span class="sxs-lookup"><span data-stu-id="84b45-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="84b45-228">做法︰限制授權使用者的資料存取</span><span class="sxs-lookup"><span data-stu-id="84b45-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="84b45-229"><a name="add-auth"></a>如何： 加入驗證 tooa 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="84b45-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="84b45-230">您可以新增驗證 tooyour 伺服器專案延伸 hello **MobileAppConfiguration**物件和設定 OWIN 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="84b45-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="84b45-231">當您安裝 hello [Microsoft.Azure.Mobile.Server.Quickstart]封裝並呼叫 hello **UseDefaultConfiguration**擴充方法，您可以略過 toostep 3。</span><span class="sxs-lookup"><span data-stu-id="84b45-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="84b45-232">在 Visual Studio 安裝 hello [Microsoft.Azure.Mobile.Server.Authentication]封裝。</span><span class="sxs-lookup"><span data-stu-id="84b45-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="84b45-233">在 hello Startup.cs 專案檔案中，加入下列一行程式碼在 hello hello 開頭的 hello**組態**方法：</span><span class="sxs-lookup"><span data-stu-id="84b45-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="84b45-234">此 OWIN 中介軟體元件驗證相關聯的 hello App Service 閘道所發行的權杖。</span><span class="sxs-lookup"><span data-stu-id="84b45-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="84b45-235">新增 hello`[Authorize]`屬性 tooany 控制器或需要驗證的方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="84b45-236">有關如何 toolearn tooauthenticate 用戶端 tooyour 行動應用程式後端，請參閱[新增 authentication tooyour 應用程式](app-service-mobile-ios-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="84b45-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="84b45-237"><a name="custom-auth"></a>做法：針對應用程式使用自訂驗證</span><span class="sxs-lookup"><span data-stu-id="84b45-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="84b45-238">如果您不想 toouse 其中一個 hello 應用程式服務驗證/授權提供者，您可以實作自己的登入系統。</span><span class="sxs-lookup"><span data-stu-id="84b45-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="84b45-239">安裝 hello [Microsoft.Azure.Mobile.Server.Login]封裝 tooassist 與驗證權杖產生。</span><span class="sxs-lookup"><span data-stu-id="84b45-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="84b45-240">提供您自己的程式碼來驗證使用者認證。</span><span class="sxs-lookup"><span data-stu-id="84b45-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="84b45-241">例如，您可以針對資料庫中的 salted 和雜湊密碼進行檢查。</span><span class="sxs-lookup"><span data-stu-id="84b45-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="84b45-242">Hello 下列範例中，在 hello `isValidAssertion()` （其他地方定義） 的方法會負責這些檢查。</span><span class="sxs-lookup"><span data-stu-id="84b45-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="84b45-243">hello 自訂驗證由建立 ApiController，而且已公開`register`和`login`動作。</span><span class="sxs-lookup"><span data-stu-id="84b45-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="84b45-244">hello 用戶端應該使用 hello 使用者自訂 UI toocollect hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="84b45-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="84b45-245">hello 資訊是透過標準的 HTTP POST 送出的 toohello API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="84b45-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="84b45-246">一旦 hello 伺服器驗證 hello 判斷提示，在核發權杖使用 hello`AppServiceLoginHandler.CreateToken()`方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="84b45-247">hello ApiController**不應該**使用 hello`[MobileAppController]`屬性。</span><span class="sxs-lookup"><span data-stu-id="84b45-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="84b45-248">範例 `login` 動作︰</span><span class="sxs-lookup"><span data-stu-id="84b45-248">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="84b45-249">在上述範例中的 hello，LoginResult 和 LoginResultUser 是可序列化的物件公開的必要的屬性。</span><span class="sxs-lookup"><span data-stu-id="84b45-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="84b45-250">hello 用戶端必須要有登入回應 toobe 傳回為 hello 表單的 JSON 物件：</span><span class="sxs-lookup"><span data-stu-id="84b45-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="84b45-251">hello`AppServiceLoginHandler.CreateToken()`方法包含*觀眾*和*簽發者*參數。</span><span class="sxs-lookup"><span data-stu-id="84b45-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="84b45-252">這兩個參數會設定 toohello 使用 hello HTTPS 配置的應用程式根目錄 URL。</span><span class="sxs-lookup"><span data-stu-id="84b45-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="84b45-253">同樣地，您應該設定*secretKey* toobe hello 值，您的應用程式的簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="84b45-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="84b45-254">不要散發 hello 簽署金鑰，用戶端中的，它可以是使用的 toomint 索引鍵，並模擬使用者。</span><span class="sxs-lookup"><span data-stu-id="84b45-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="84b45-255">您可以取得簽署金鑰時所參考 hello 裝載的應用程式服務的 hello*網站\_AUTH\_簽署\_金鑰*環境變數。</span><span class="sxs-lookup"><span data-stu-id="84b45-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="84b45-256">如果需要在本機偵錯內容中，請遵循 hello 中的 hello 指示[本機偵錯工具驗證](#local-debug)區段 tooretrieve hello 金鑰並將它儲存為應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="84b45-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="84b45-257">其他宣告和到期日，也可能包括 hello 發出權杖。</span><span class="sxs-lookup"><span data-stu-id="84b45-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="84b45-258">Hello 發行權杖必須至少包含主旨 (**sub**) 宣告。</span><span class="sxs-lookup"><span data-stu-id="84b45-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="84b45-259">您可以支援標準用戶端 hello`loginAsync()`透過 hello 驗證路由的多載的方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="84b45-260">如果 hello 用戶端呼叫`client.loginAsync('custom');`toolog 中的，您的路由必須`/.auth/login/custom`。</span><span class="sxs-lookup"><span data-stu-id="84b45-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="84b45-261">您可以設定 hello 路由 hello 自訂驗證控制器使用`MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="84b45-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="84b45-262">使用 hello`loginAsync()`方法可確保該 hello 驗證語彙基元會附加 tooevery 後續呼叫 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="84b45-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="84b45-263"><a name="user-info"></a>做法：取出已驗證的使用者資訊</span><span class="sxs-lookup"><span data-stu-id="84b45-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="84b45-264">當使用者驗證應用程式服務時，您可以存取 hello 分派使用者識別碼和在.NET 後端程式碼中的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="84b45-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="84b45-265">hello 使用者資訊可以用於在 hello 後端進行授權決策。</span><span class="sxs-lookup"><span data-stu-id="84b45-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="84b45-266">hello 下列程式碼會取得 hello 與要求相關聯的使用者識別碼：</span><span class="sxs-lookup"><span data-stu-id="84b45-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="84b45-267">hello SID 衍生自 hello 特定提供者使用者識別碼，而且是靜態的給定的使用者和登入提供者。</span><span class="sxs-lookup"><span data-stu-id="84b45-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="84b45-268">hello SID 是無效的驗證權杖則為 null。</span><span class="sxs-lookup"><span data-stu-id="84b45-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="84b45-269">App Service 也可讓您向登入提供者要求特定宣告。</span><span class="sxs-lookup"><span data-stu-id="84b45-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="84b45-270">每個識別提供者均可使用識別提供者 SDK 來提供更多資訊。</span><span class="sxs-lookup"><span data-stu-id="84b45-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="84b45-271">例如，您可以使用 hello Facebook 圖形 API 的朋友的資訊。</span><span class="sxs-lookup"><span data-stu-id="84b45-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="84b45-272">您可以指定要求的宣告在 hello hello Azure 入口網站中的提供者] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="84b45-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="84b45-273">某些宣告需要 hello 身分識別提供者的其他設定。</span><span class="sxs-lookup"><span data-stu-id="84b45-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="84b45-274">hello 下列程式碼呼叫 hello **GetAppServiceIdentityAsync**延伸方法 tooget hello 登入認證，包括對 hello Facebook 圖形 API 的 hello 存取權杖需要的 toomake 要求：</span><span class="sxs-lookup"><span data-stu-id="84b45-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="84b45-275">加入 using 陳述式`System.Security.Principal`tooprovide hello **GetAppServiceIdentityAsync**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="84b45-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="84b45-276"><a name="authorize"></a>做法︰限制授權使用者的資料存取</span><span class="sxs-lookup"><span data-stu-id="84b45-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="84b45-277">Hello 前一節，我們也示範了如何 tooretrieve hello 已驗證使用者的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="84b45-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="84b45-278">您可以限制存取 toodata 及其他資源，根據此值。</span><span class="sxs-lookup"><span data-stu-id="84b45-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="84b45-279">例如，新增使用者識別碼資料行 tootables 和篩選 hello 使用者識別碼 hello 查詢結果是傳回的資料只有 tooauthorized 使用者簡單的方式 toolimit。</span><span class="sxs-lookup"><span data-stu-id="84b45-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="84b45-280">hello 下列程式碼時，傳回資料列只 hello SID 符合 hello hello TodoItem 資料表上的使用者識別碼資料行中的值：</span><span class="sxs-lookup"><span data-stu-id="84b45-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="84b45-281">hello`Query()`方法會傳回`IQueryable`，可由 LINQ toohandle 篩選操作。</span><span class="sxs-lookup"><span data-stu-id="84b45-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="84b45-282">如何： 加入推播通知 tooa 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="84b45-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="84b45-283">新增推播通知 tooyour 伺服器專案延伸 hello **MobileAppConfiguration**物件及建立通知中樞的用戶端。</span><span class="sxs-lookup"><span data-stu-id="84b45-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="84b45-284">在 Visual Studio 中，以滑鼠右鍵按一下 hello 伺服器專案，然後按一下**管理 NuGet 封裝**，搜尋`Microsoft.Azure.Mobile.Server.Notifications`，然後按一下 [**安裝**。</span><span class="sxs-lookup"><span data-stu-id="84b45-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="84b45-285">重複此步驟 tooinstall hello`Microsoft.Azure.NotificationHubs`封裝，其中包含 hello 通知中樞的用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="84b45-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="84b45-286">在 App_Start/Startup.MobileApp.cs，並加入呼叫 toohello **AddPushNotifications()**初始化期間的擴充方法：</span><span class="sxs-lookup"><span data-stu-id="84b45-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="84b45-287">加入下列程式碼會建立通知中樞的用戶端 hello:</span><span class="sxs-lookup"><span data-stu-id="84b45-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="84b45-288">您現在可以使用 hello 通知中樞的用戶端 toosend 推播通知 tooregistered 裝置。</span><span class="sxs-lookup"><span data-stu-id="84b45-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="84b45-289">如需詳細資訊，請參閱[新增推播通知 tooyour 應用程式](app-service-mobile-ios-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="84b45-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="84b45-290">toolearn 深入了解通知中心，請參閱[通知中心概觀](../notification-hubs/notification-hubs-push-notification-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="84b45-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="84b45-291"><a name="tags"></a>作法：使用標籤啟用有目標的推播</span><span class="sxs-lookup"><span data-stu-id="84b45-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="84b45-292">通知中樞可讓您透過使用標記 toospecific 註冊傳送目標的通知。</span><span class="sxs-lookup"><span data-stu-id="84b45-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="84b45-293">自動建立數個標籤︰</span><span class="sxs-lookup"><span data-stu-id="84b45-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="84b45-294">hello 安裝識別碼會識別特定的裝置。</span><span class="sxs-lookup"><span data-stu-id="84b45-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="84b45-295">hello 使用者 Id 根據已驗證的 hello SID 來識別特定的使用者。</span><span class="sxs-lookup"><span data-stu-id="84b45-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="84b45-296">hello 的安裝識別碼可從 hello **installationId**屬性 hello **MobileServiceClient**。</span><span class="sxs-lookup"><span data-stu-id="84b45-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="84b45-297">hello 下列範例示範如何使用安裝識別碼 tooadd 標記 tooa 特定安裝在通知中樞：</span><span class="sxs-lookup"><span data-stu-id="84b45-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="84b45-298">Hello 後端建立 hello 安裝時，會忽略任何推播通知登錄期間 hello 用戶端所提供的標記。</span><span class="sxs-lookup"><span data-stu-id="84b45-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="84b45-299">用戶端 tooadd tooenable 標記 toohello 安裝，您必須建立自訂 API 中，加入標記使用 hello 前面模式。</span><span class="sxs-lookup"><span data-stu-id="84b45-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="84b45-300">請參閱[用戶端新增推播通知標記][ 5]在 hello App Service 行動應用程式已完成的快速入門範例中的範例。</span><span class="sxs-lookup"><span data-stu-id="84b45-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="84b45-301"><a name="push-user"></a>如何： 傳送推播通知 tooan 驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="84b45-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="84b45-302">當已驗證的使用者註冊推播通知時，使用者識別碼標籤會自動加入 toohello 註冊。</span><span class="sxs-lookup"><span data-stu-id="84b45-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="84b45-303">藉由使用此標記，您可以傳送推播通知 tooall 裝置已註冊該人員。</span><span class="sxs-lookup"><span data-stu-id="84b45-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="84b45-304">hello 下列程式碼取得 hello 提出要求的使用者的 SID，並將傳送範本推播通知 tooevery 裝置登錄該人員：</span><span class="sxs-lookup"><span data-stu-id="84b45-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="84b45-305">在註冊來自已驗證用戶端的推播通知時，請確定驗證已完成，然後再嘗試註冊。</span><span class="sxs-lookup"><span data-stu-id="84b45-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="84b45-306">如需詳細資訊，請參閱[推送 toousers] [ 6] hello App Service 行動應用程式已完成的快速入門範例.NET 後端中。</span><span class="sxs-lookup"><span data-stu-id="84b45-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="84b45-307">如何： 偵錯和疑難排解 hello.NET 伺服器 SDK</span><span class="sxs-lookup"><span data-stu-id="84b45-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="84b45-308">Azure App Service 提供了數個適用於 ASP.NET 應用程式的偵錯和疑難排解技術：</span><span class="sxs-lookup"><span data-stu-id="84b45-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="84b45-309">監視 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="84b45-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="84b45-310">在 Azure App Service 中啟用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="84b45-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="84b45-311">在 Visual Studio 中疑難排解 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="84b45-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="84b45-312">記錄</span><span class="sxs-lookup"><span data-stu-id="84b45-312">Logging</span></span>
<span data-ttu-id="84b45-313">您可以使用標準 ASP.NET 追蹤寫入 hello 撰寫 tooApp 服務診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="84b45-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="84b45-314">您可以撰寫 toohello 記錄檔之前，您必須在您的行動裝置應用程式後端啟用診斷。</span><span class="sxs-lookup"><span data-stu-id="84b45-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="84b45-315">tooenable 診斷和寫入 toohello 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="84b45-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="84b45-316">中的 hello 步驟[如何 tooenable 診斷](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag)。</span><span class="sxs-lookup"><span data-stu-id="84b45-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="84b45-317">將 hello 面一行加入程式碼檔中使用陳述式：</span><span class="sxs-lookup"><span data-stu-id="84b45-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="84b45-318">建立追蹤寫入器 toowrite hello.NET 後端 toohello 診斷記錄檔，如下所示：</span><span class="sxs-lookup"><span data-stu-id="84b45-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="84b45-319">重新發佈您的伺服器專案，而且存取 hello 行動裝置應用程式後端 tooexecute hello 程式碼路徑與 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="84b45-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="84b45-320">下載並評估 hello 記錄中所述[How to： 下載記錄檔](../app-service-web/web-sites-enable-diagnostic-log.md#download)。</span><span class="sxs-lookup"><span data-stu-id="84b45-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="84b45-321"><a name="local-debug"></a>使用驗證進行本機偵錯</span><span class="sxs-lookup"><span data-stu-id="84b45-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="84b45-322">您可以執行您的應用程式本機 tootest 變更之前發佈 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="84b45-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="84b45-323">對於大部分的 Azure Mobile Apps 後端，請在Visual Studio 中時按 F5  。</span><span class="sxs-lookup"><span data-stu-id="84b45-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="84b45-324">不過，使用驗證時有一些其他考量。</span><span class="sxs-lookup"><span data-stu-id="84b45-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="84b45-325">您必須擁有雲端式行動裝置應用程式與應用程式服務驗證/授權設定，而且您的用戶端必須指定 hello 替代登入主控件以 hello 雲端端點。</span><span class="sxs-lookup"><span data-stu-id="84b45-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="84b45-326">請參閱 hello 文件以 hello 所需的特定步驟為您用戶端平台。</span><span class="sxs-lookup"><span data-stu-id="84b45-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="84b45-327">確定您的行動後端已安裝 [Microsoft.Azure.Mobile.Server.Authentication] 。</span><span class="sxs-lookup"><span data-stu-id="84b45-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="84b45-328">然後，在您的應用程式 OWIN 啟動類別中，加入 hello 下列程式碼之後,`MobileAppConfiguration`已套用的 tooyour `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="84b45-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="84b45-329">在上述範例中的 hello，您應該設定 hello *authAudience*和*authIssuer* Web.config 中的應用程式設定檔 tooeach 是應用程式根目錄的 URL 使用 hello HTTPS配置。</span><span class="sxs-lookup"><span data-stu-id="84b45-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="84b45-330">同樣地，您應該設定*authSigningKey* toobe hello 值，您的應用程式的簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="84b45-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="84b45-331">tooobtain hello 簽署金鑰：</span><span class="sxs-lookup"><span data-stu-id="84b45-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="84b45-332">瀏覽 tooyour 應用程式內 hello [Azure 入口網站]</span><span class="sxs-lookup"><span data-stu-id="84b45-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="84b45-333">按一下 [工具]、[Kudu]、[執行]。</span><span class="sxs-lookup"><span data-stu-id="84b45-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="84b45-334">在 hello Kudu 管理入口網站中，按一下 [**環境**。</span><span class="sxs-lookup"><span data-stu-id="84b45-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="84b45-335">尋找 hello 值*網站\_AUTH\_簽署\_金鑰*。</span><span class="sxs-lookup"><span data-stu-id="84b45-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="84b45-336">使用簽署金鑰 hello 的 hello *authSigningKey*本機應用程式組態中的參數。您的行動裝置後端現在已備妥的 toovalidate 語彙基元時，在本機執行 hello 的用戶端會從 hello 以雲端為基礎的端點來取得 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="84b45-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[Azure 入口網站]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
