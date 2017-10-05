---
title: "如何使用適用於 Mobile Apps 的 .NET 後端伺服器 SDK | Microsoft Docs"
description: "了解如何使用適用於 Azure App Service Mobile Apps 的 .NET 後端伺服器 SDK。"
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
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="8df95-104">使用適用於 Azure Mobile Apps 的 .NET 後端伺服器 SDK</span><span class="sxs-lookup"><span data-stu-id="8df95-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="8df95-105">本主題說明如何在主要的 Azure App Service Mobile Apps 案例中使用 .NET 後端伺服器 SDK</span><span class="sxs-lookup"><span data-stu-id="8df95-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="8df95-106">Azure Mobile Apps SDK 可協助您從 ASP.NET 應用程式使用行動用戶端。</span><span class="sxs-lookup"><span data-stu-id="8df95-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="8df95-107">[適用於 Azure Mobile Apps 的 .NET 伺服器 SDK][2]是 GitHub 上的開放原始碼。</span><span class="sxs-lookup"><span data-stu-id="8df95-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="8df95-108">儲存機制包含所有原始程式碼，其中包括整個伺服器 SDK 單元測試組件和一些範例專案。</span><span class="sxs-lookup"><span data-stu-id="8df95-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="8df95-109">參考文件</span><span class="sxs-lookup"><span data-stu-id="8df95-109">Reference documentation</span></span>
<span data-ttu-id="8df95-110">伺服器 SDK 的參考文件位於此處：[Azure Mobile Apps .NET 參考資料][1]。</span><span class="sxs-lookup"><span data-stu-id="8df95-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="8df95-111"><a name="create-app"></a>作法：建立 .NET 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="8df95-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="8df95-112">如果您開始新的專案，您可以使用 [Azure 入口網站] 或 Visual Studio，建立 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df95-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="8df95-113">您可以在本機執行 App Service 應用程式，或將專案發佈至雲端架構 App Service 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df95-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="8df95-114">如果您將行動功能新增至現有的專案，請參閱 [下載並初始化 SDK](#install-sdk) 一節。</span><span class="sxs-lookup"><span data-stu-id="8df95-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="8df95-115">使用 Azure 入口網站建立 .NET 後端</span><span class="sxs-lookup"><span data-stu-id="8df95-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="8df95-116">若要建立 App Service 行動後端，請遵循[快速入門教學課程][3]或遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="8df95-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="8df95-117">回到 [開始使用] 刀鋒視窗，在 [建立資料表 API] 底下，選擇 [C#] 作為您的 [後端語言]。</span><span class="sxs-lookup"><span data-stu-id="8df95-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="8df95-118">按一下 [下載] ，將壓縮的專案檔案解壓縮至您的本機電腦，並在 Visual Studio 中開啟方案。</span><span class="sxs-lookup"><span data-stu-id="8df95-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="8df95-119">使用 Visual Studio 2013 和 Visual Studio 2015 建立 .NET 後端</span><span class="sxs-lookup"><span data-stu-id="8df95-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="8df95-120">安裝 [Azure SDK for .NET][4] (2.9.0 版或更新版本)，以在 Visual Studio 中建立 Azure Mobile Apps 專案。</span><span class="sxs-lookup"><span data-stu-id="8df95-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="8df95-121">當您安裝 SDK 之後，使用下列步驟建立 ASP.NET 應用程式：</span><span class="sxs-lookup"><span data-stu-id="8df95-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="8df95-122">開啟 [新增專案] 對話方塊 (從 [檔案]  >  [新增]  >  [專案...])。</span><span class="sxs-lookup"><span data-stu-id="8df95-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="8df95-123">展開 [範本] > [Visual C#]，然後選取 [Web]。</span><span class="sxs-lookup"><span data-stu-id="8df95-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="8df95-124">選取 [ASP.NET Web 應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="8df95-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="8df95-125">填入專案名稱。</span><span class="sxs-lookup"><span data-stu-id="8df95-125">Fill in the project name.</span></span> <span data-ttu-id="8df95-126">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8df95-126">Then click **OK**.</span></span>
5. <span data-ttu-id="8df95-127">在 [ASP.NET 4.5.2 範本] 底下，選取 [Azure 行動應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8df95-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="8df95-128">核取 [雲端中的主機]  以在雲端 (您可以在其中發佈這個專案) 建立行動後端。</span><span class="sxs-lookup"><span data-stu-id="8df95-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="8df95-129">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8df95-129">Click **OK**.</span></span>

## <span data-ttu-id="8df95-130"><a name="install-sdk"></a>如何：下載並初始化 SDK</span><span class="sxs-lookup"><span data-stu-id="8df95-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="8df95-131">SDK 可於 [NuGet.org]取得。</span><span class="sxs-lookup"><span data-stu-id="8df95-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="8df95-132">此封裝包含開始使用 SDK 所需的基本功能。</span><span class="sxs-lookup"><span data-stu-id="8df95-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="8df95-133">若要初始化 SDK，您需要在 **HttpConfiguration** 物件上執行動作。</span><span class="sxs-lookup"><span data-stu-id="8df95-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="8df95-134">安裝 SDK</span><span class="sxs-lookup"><span data-stu-id="8df95-134">Install the SDK</span></span>
<span data-ttu-id="8df95-135">若要安裝 SDK，請以滑鼠右鍵按一下 Visual Studio 中的伺服器專案，選取 [管理 NuGet 套件]，搜尋 [Microsoft.Azure.Mobile.Server] 套件，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="8df95-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="8df95-136"><a name="server-project-setup"></a> 初始化伺服器專案</span><span class="sxs-lookup"><span data-stu-id="8df95-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="8df95-137">初始化 .NET 後端伺服器專案的方式類似其他 ASP.NET 專案，可藉由包含 OWIN 啟動類別來完成。</span><span class="sxs-lookup"><span data-stu-id="8df95-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="8df95-138">請確定您已參考 NuGet 封裝 `Microsoft.Owin.Host.SystemWeb`。</span><span class="sxs-lookup"><span data-stu-id="8df95-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="8df95-139">若要在 Visual Studio 中新增這個類別，請在伺服器專案上按一下滑鼠右鍵，選取 **[新增]** >
**[新項目]**，然後依序選取 **[Web]** > **[一般]** > **[OWIN 啟動類別]**。</span><span class="sxs-lookup"><span data-stu-id="8df95-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="8df95-140">隨即產生具有下列屬性的類別：</span><span class="sxs-lookup"><span data-stu-id="8df95-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="8df95-141">在 OWIN 啟動類別的 `Configuration()` 方法中，使用 **HttpConfiguration** 物件來設定 Azure Mobile Apps 環境。</span><span class="sxs-lookup"><span data-stu-id="8df95-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="8df95-142">下列範例會初始化伺服器專案，不新增任何功能：</span><span class="sxs-lookup"><span data-stu-id="8df95-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="8df95-143">若要啟用個別功能，您必須在呼叫 **ApplyTo** 之前，於 **MobileAppConfiguration** 物件上呼叫擴充方法。</span><span class="sxs-lookup"><span data-stu-id="8df95-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="8df95-144">例如，下列程式碼會在初始化期間，將預設路由加入具有屬性 `[MobileAppController]` 的所有 API 控制器中：</span><span class="sxs-lookup"><span data-stu-id="8df95-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="8df95-145">Azure 入口網站的伺服器快速入門會呼叫 **UseDefaultConfiguration()**。</span><span class="sxs-lookup"><span data-stu-id="8df95-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="8df95-146">此命令相當於下列設定：</span><span class="sxs-lookup"><span data-stu-id="8df95-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="8df95-147">使用的擴充方法如下︰</span><span class="sxs-lookup"><span data-stu-id="8df95-147">The extension methods used are:</span></span>

* <span data-ttu-id="8df95-148">`AddMobileAppHomeController()` 提供預設 Azure Mobile Apps 首頁。</span><span class="sxs-lookup"><span data-stu-id="8df95-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="8df95-149">`MapApiControllers()` 會為以 `[MobileAppController]` 屬性裝飾的 WebAPI 控制器提供自訂 API 功能。</span><span class="sxs-lookup"><span data-stu-id="8df95-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="8df95-150">`AddTables()` 提供 `/tables` 端點與資料表控制器的對應。</span><span class="sxs-lookup"><span data-stu-id="8df95-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="8df95-151">`AddTablesWithEntityFramework()` 是使用以 Entity Framework 為基礎的控制器對應 `/tables` 端點的速記法。</span><span class="sxs-lookup"><span data-stu-id="8df95-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="8df95-152">`AddPushNotifications()` 提供向通知中樞註冊裝置的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="8df95-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="8df95-153">`MapLegacyCrossDomainController()` 提供用於本機開發的標準 CORS 標頭。</span><span class="sxs-lookup"><span data-stu-id="8df95-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="8df95-154">SDK 延伸模組</span><span class="sxs-lookup"><span data-stu-id="8df95-154">SDK extensions</span></span>
<span data-ttu-id="8df95-155">下列 NuGet 型擴充套件提供了許多您應用程式可以使用的行動功能。</span><span class="sxs-lookup"><span data-stu-id="8df95-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="8df95-156">您可以使用 **MobileAppConfiguration** 物件，在初始化期間啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="8df95-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="8df95-157">[Microsoft.Azure.Mobile.Server.Quickstart] 支援基本的 Mobile Apps 設定。</span><span class="sxs-lookup"><span data-stu-id="8df95-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="8df95-158">在初始化期間，透過呼叫 **UseDefaultConfiguration** 擴充方法來新增到組態。</span><span class="sxs-lookup"><span data-stu-id="8df95-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="8df95-159">此擴充包含下列擴充功能：通知、驗證、實體、資料表、跨網域和首頁封裝。</span><span class="sxs-lookup"><span data-stu-id="8df95-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="8df95-160">此封裝由 Azure 入口網站上可取得的 Mobile Apps 快速入門使用。</span><span class="sxs-lookup"><span data-stu-id="8df95-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="8df95-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) 實作網站根目錄的預設 [此行動應用程式已啟動並執行中] 頁面。</span><span class="sxs-lookup"><span data-stu-id="8df95-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="8df95-162">透過呼叫 **AddMobileAppHomeController** 擴充方法來新增到組態。</span><span class="sxs-lookup"><span data-stu-id="8df95-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="8df95-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) 包含適用於處理資料與設定資料管線的類別。</span><span class="sxs-lookup"><span data-stu-id="8df95-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="8df95-164">透過呼叫 **AddTables** 擴充方法來加入設定中。</span><span class="sxs-lookup"><span data-stu-id="8df95-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="8df95-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) 讓 Entity Framework 能存取 SQL Database 中的資料。</span><span class="sxs-lookup"><span data-stu-id="8df95-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="8df95-166">透過呼叫 **AddTablesWithEntityFramework** 擴充方法來加入設定中。</span><span class="sxs-lookup"><span data-stu-id="8df95-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="8df95-167">[Microsoft.Azure.Mobile.Server.Authentication] 啟用驗證，並設定用來驗證權杖的 OWIN 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="8df95-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="8df95-168">透過呼叫 **AddAppServiceAuthentication** 與 **IAppBuilder**.**UseAppServiceAuthentication** 擴充方法來新增到組態。</span><span class="sxs-lookup"><span data-stu-id="8df95-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="8df95-169">[Microsoft.Azure.Mobile.Server.Notifications] 啟用推播通知，並定義推播註冊端點。</span><span class="sxs-lookup"><span data-stu-id="8df95-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="8df95-170">透過呼叫 **AddPushNotifications** 擴充方法來加入設定中。</span><span class="sxs-lookup"><span data-stu-id="8df95-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="8df95-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) 建立從行動應用程式提供資料給舊版網頁瀏覽器的控制器。</span><span class="sxs-lookup"><span data-stu-id="8df95-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="8df95-172">透過呼叫 **MapLegacyCrossDomainController** 擴充方法來加入設定中。</span><span class="sxs-lookup"><span data-stu-id="8df95-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="8df95-173">[Microsoft.Azure.Mobile.Server.Login] 會提供 AppServiceLoginHandler.CreateToken() 方法，這是在自訂驗證案例期間使用的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="8df95-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="8df95-174"><a name="publish-server-project"></a>做法：發佈伺服器專案</span><span class="sxs-lookup"><span data-stu-id="8df95-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="8df95-175">本節說明如何從 Visual Studio 發佈 .NET 後端專案。</span><span class="sxs-lookup"><span data-stu-id="8df95-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="8df95-176">您也可以使用 Git 或 [Azure App Service 部署文件](../app-service-web/web-sites-deploy.md)中涵蓋的任何其他方法，來部署您的後端專案。</span><span class="sxs-lookup"><span data-stu-id="8df95-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="8df95-177">在 Visual Studio 中，重新建置專案以還原 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="8df95-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="8df95-178">在 [方案總管] 中，於專案上按一下滑鼠右鍵，然後按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="8df95-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="8df95-179">第一次發佈時，您必須定義發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="8df95-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="8df95-180">在定義設定檔後，您可以選取該設定檔，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="8df95-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="8df95-181">如果系統要求您選取發佈目標，請按一下 [Microsoft Azure App Service] > [下一步]，然後視需要使用您的 Azure 認證來登入。</span><span class="sxs-lookup"><span data-stu-id="8df95-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="8df95-182">Visual Studio 會直接從 Azure 下載並安全地儲存您的發佈設定。</span><span class="sxs-lookup"><span data-stu-id="8df95-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="8df95-183">選擇您的 [訂用帳戶]，從 [檢視] 中選取 [資源類型]，展開 [行動應用程式]，按一下您的行動應用程式後端，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8df95-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="8df95-184">驗證發佈設定檔資訊，然後按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="8df95-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="8df95-185">當您的行動應用程式後端已成功發佈後，您會看到表示成功的登陸頁面。</span><span class="sxs-lookup"><span data-stu-id="8df95-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="8df95-186"><a name="define-table-controller"></a> 做法：定義資料表控制器</span><span class="sxs-lookup"><span data-stu-id="8df95-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="8df95-187">定義資料表控制器，以對行動用戶端公開 SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="8df95-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="8df95-188">設定資料表控制器需要三個步驟︰</span><span class="sxs-lookup"><span data-stu-id="8df95-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="8df95-189">建立資料傳輸物件 (DTO) 類別。</span><span class="sxs-lookup"><span data-stu-id="8df95-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="8df95-190">在行動 DbContext 類別中設定資料表參考。</span><span class="sxs-lookup"><span data-stu-id="8df95-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="8df95-191">建立資料表控制器。</span><span class="sxs-lookup"><span data-stu-id="8df95-191">Create a table controller.</span></span>

<span data-ttu-id="8df95-192">資料傳輸物件 (DTO) 是繼承自 `EntityData`純 C# 物件。</span><span class="sxs-lookup"><span data-stu-id="8df95-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="8df95-193">例如：</span><span class="sxs-lookup"><span data-stu-id="8df95-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="8df95-194">DTO 用來定義 SQL Database 內的資料表。</span><span class="sxs-lookup"><span data-stu-id="8df95-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="8df95-195">若要建立資料庫項目，將 `DbSet<>` 屬性新增至您正在使用的 DbContext。</span><span class="sxs-lookup"><span data-stu-id="8df95-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="8df95-196">在 Azure Mobile Apps 的預設專案範本中，DbContext 稱為 `Models\MobileServiceContext.cs`：</span><span class="sxs-lookup"><span data-stu-id="8df95-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="8df95-197">如果已安裝 Azure SDK，您現在可以建立範本資料表控制器，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="8df95-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="8df95-198">以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [新增]  > 。</span><span class="sxs-lookup"><span data-stu-id="8df95-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="8df95-199">選取 [Azure Mobile Apps 資料表控制器] 選項，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8df95-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="8df95-200">在 [新增控制器]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="8df95-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="8df95-201">在 [模型類別]  下拉式清單中，選取您新的 DTO。</span><span class="sxs-lookup"><span data-stu-id="8df95-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="8df95-202">在 [DbContext]  下拉式清單中，選取 [行動服務 DbContext] 類別。</span><span class="sxs-lookup"><span data-stu-id="8df95-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="8df95-203">為您建立控制器名稱。</span><span class="sxs-lookup"><span data-stu-id="8df95-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="8df95-204">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="8df95-204">Click **Add**.</span></span>

<span data-ttu-id="8df95-205">快速入門伺服器專案包含簡單的 **TodoItemController**範例。</span><span class="sxs-lookup"><span data-stu-id="8df95-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="8df95-206"><a name="adjust-pagesize"></a>作法：調整資料表分頁大小</span><span class="sxs-lookup"><span data-stu-id="8df95-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="8df95-207">根據預設，Azure Mobile Apps 針對每個要求會傳回 50 個記錄。</span><span class="sxs-lookup"><span data-stu-id="8df95-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="8df95-208">分頁可確保用戶端不會佔用其 UI 執行緒或伺服器太久，以確保有良好的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="8df95-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="8df95-209">若要變更資料表分頁大小，請增加伺服器端「允許的查詢大小」和用戶端頁面大小。使用 `EnableQuery` 屬性可調整伺服器端「允許的查詢大小」︰</span><span class="sxs-lookup"><span data-stu-id="8df95-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="8df95-210">確定 PageSize 等於或大於用戶端所要求的大小。</span><span class="sxs-lookup"><span data-stu-id="8df95-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="8df95-211">如需變更用戶端頁面大小的詳細資料，請參閱特定用戶端的做法文件。</span><span class="sxs-lookup"><span data-stu-id="8df95-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="8df95-212">做法：定義自訂 API 控制器</span><span class="sxs-lookup"><span data-stu-id="8df95-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="8df95-213">自訂 API 控制器透過公開端點，提供最基本的功能給您的行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="8df95-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="8df95-214">您可以使用屬性 [MobileAppController] 來註冊行動裝置特定 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="8df95-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="8df95-215">`MobileAppController` 屬性會註冊路由、設定 Mobile Apps JSON 序列化程式，以及開啟 [用戶端版本檢查](app-service-mobile-client-and-server-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="8df95-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="8df95-216">在 Visual Studio 中，以滑鼠右鍵按一下 [控制器] 資料夾，然後按一下 [新增] > [控制器]，選取 [Web API 2 控制器&mdash;空白]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8df95-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="8df95-217">提供 [控制器名稱] \(例如 `CustomController`)，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8df95-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="8df95-218">在新的控制器類別檔案中，新增下列 Using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="8df95-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="8df95-219">將 **[MobileAppController]** 屬性套用到 API 控制器類別定義，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8df95-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="8df95-220">在 App_Start/Startup.MobileApp.cs 檔案中，新增對 **MapApiControllers** 擴充方法的呼叫，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8df95-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="8df95-221">您也可以使用 `UseDefaultConfiguration()` 擴充方法，而不是 `MapApiControllers()`。</span><span class="sxs-lookup"><span data-stu-id="8df95-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="8df95-222">用戶端仍然可以存取任何沒有套用 **MobileAppControllerAttribute** 的控制器，但是使用任何行動應用程式用戶端 SDK 的用戶端可能會無法正確取用。</span><span class="sxs-lookup"><span data-stu-id="8df95-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="8df95-223">做法：使用驗證</span><span class="sxs-lookup"><span data-stu-id="8df95-223">How to: Work with authentication</span></span>
<span data-ttu-id="8df95-224">Azure Mobile Apps 會使用 App Service 驗證 / 授權來保護您的行動後端。</span><span class="sxs-lookup"><span data-stu-id="8df95-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="8df95-225">本節說明如何在 .NET 後端伺服器專案中執行下列驗證相關工作：</span><span class="sxs-lookup"><span data-stu-id="8df95-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="8df95-226">做法：將驗證新增至伺服器專案</span><span class="sxs-lookup"><span data-stu-id="8df95-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="8df95-227">做法：針對應用程式使用自訂驗證</span><span class="sxs-lookup"><span data-stu-id="8df95-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="8df95-228">做法：取出已驗證的使用者資訊</span><span class="sxs-lookup"><span data-stu-id="8df95-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="8df95-229">做法︰限制授權使用者的資料存取</span><span class="sxs-lookup"><span data-stu-id="8df95-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="8df95-230"><a name="add-auth"></a>做法：將驗證新增至伺服器專案</span><span class="sxs-lookup"><span data-stu-id="8df95-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="8df95-231">您可以透過擴充 **MobileAppConfiguration** 物件並設定 OWIN 中介軟體，將驗證加入您的伺服器專案中。</span><span class="sxs-lookup"><span data-stu-id="8df95-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="8df95-232">安裝 [Microsoft.Azure.Mobile.Server.Quickstart] 封裝並呼叫 **UseDefaultConfiguration** 擴充方法時，您可以跳到步驟 3。</span><span class="sxs-lookup"><span data-stu-id="8df95-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="8df95-233">在 Visual Studio 中，安裝 [Microsoft.Azure.Mobile.Server.Authentication] 封裝。</span><span class="sxs-lookup"><span data-stu-id="8df95-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="8df95-234">在 Startup.cs 專案檔案中，在 **Configuration** 方法的開頭加入下列程式碼行：</span><span class="sxs-lookup"><span data-stu-id="8df95-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="8df95-235">此 OWIN 中介軟體元件會驗證相關聯 App Service 閘道所發出的權杖。</span><span class="sxs-lookup"><span data-stu-id="8df95-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="8df95-236">將 `[Authorize]` 屬性加入任何需要驗證的控制器或方法中。</span><span class="sxs-lookup"><span data-stu-id="8df95-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="8df95-237">若要了解如何在您的 Mobile Apps 後端驗證用戶端，請參閱 [將驗證新增至您的應用程式](app-service-mobile-ios-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="8df95-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="8df95-238"><a name="custom-auth"></a>做法：針對應用程式使用自訂驗證</span><span class="sxs-lookup"><span data-stu-id="8df95-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="8df95-239">如果您不想要使用其中一個 App Service 驗證/授權提供者，您可以實作自己的登入系統。</span><span class="sxs-lookup"><span data-stu-id="8df95-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="8df95-240">安裝 [Microsoft.Azure.Mobile.Server.Login] 封裝，協助產生驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="8df95-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="8df95-241">提供您自己的程式碼來驗證使用者認證。</span><span class="sxs-lookup"><span data-stu-id="8df95-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="8df95-242">例如，您可以針對資料庫中的 salted 和雜湊密碼進行檢查。</span><span class="sxs-lookup"><span data-stu-id="8df95-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="8df95-243">在下列範例中， `isValidAssertion()` 方法 (定義於其他地方) 會負責這些檢查。</span><span class="sxs-lookup"><span data-stu-id="8df95-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="8df95-244">自訂驗證的公開方式為建立 ApiController 及公開 `register` 和 `login` 動作。</span><span class="sxs-lookup"><span data-stu-id="8df95-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="8df95-245">用戶端應該使用的自訂 UI，向使用者收集資訊。</span><span class="sxs-lookup"><span data-stu-id="8df95-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="8df95-246">此資訊會接著透過標準 HTTP POST 呼叫提交至 API。</span><span class="sxs-lookup"><span data-stu-id="8df95-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="8df95-247">伺服器驗證這項判斷提示之後，便使用 `AppServiceLoginHandler.CreateToken()` 方法來發行權杖。</span><span class="sxs-lookup"><span data-stu-id="8df95-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="8df95-248">ApiController **不得**使用 `[MobileAppController]`屬性。</span><span class="sxs-lookup"><span data-stu-id="8df95-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="8df95-249">範例 `login` 動作︰</span><span class="sxs-lookup"><span data-stu-id="8df95-249">An example `login` action:</span></span>

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

<span data-ttu-id="8df95-250">在上述範例中，LoginResult 和 LoginResultUser 是公開必要屬性的可序列化物件。</span><span class="sxs-lookup"><span data-stu-id="8df95-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="8df95-251">用戶端預期有以下格式的 JSON 物件傳回登入回應：</span><span class="sxs-lookup"><span data-stu-id="8df95-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="8df95-252">`AppServiceLoginHandler.CreateToken()` 方法包含 audience 和 issuer 參數。</span><span class="sxs-lookup"><span data-stu-id="8df95-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="8df95-253">這兩個參數會使用 HTTPS 配置設定為應用程式根目錄的 URL。</span><span class="sxs-lookup"><span data-stu-id="8df95-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="8df95-254">同樣地，您應該將 secretKey 設定為您應用程式的簽署金鑰值。</span><span class="sxs-lookup"><span data-stu-id="8df95-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="8df95-255">請勿散發用戶端中的簽署金鑰，因為它可用來仿造金鑰和模擬使用者。</span><span class="sxs-lookup"><span data-stu-id="8df95-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="8df95-256">您可以藉由參考 WEBSITE\_AUTH\_SIGNING\_KEY 環境變數，在裝載於 App Service 時取得此簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="8df95-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="8df95-257">如果在本機偵錯內容中有需要，請依照 [使用驗證進行本機偵錯](#local-debug) 一節中的指示以取出金鑰，並將它儲存為應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="8df95-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="8df95-258">發行的權杖可能也包含其他宣告和到期日。</span><span class="sxs-lookup"><span data-stu-id="8df95-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="8df95-259">發行的權杖至少必須包含一個主體 (**sub**) 宣告。</span><span class="sxs-lookup"><span data-stu-id="8df95-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="8df95-260">您可以藉由多載驗證路由來支援標準用戶端 `loginAsync()` 方法。</span><span class="sxs-lookup"><span data-stu-id="8df95-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="8df95-261">如果用戶端呼叫 `client.loginAsync('custom');` 進行登入，您的路由必須是 `/.auth/login/custom`。</span><span class="sxs-lookup"><span data-stu-id="8df95-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="8df95-262">您可以使用 `MapHttpRoute()`設定自訂驗證控制器的路由：</span><span class="sxs-lookup"><span data-stu-id="8df95-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="8df95-263">使用 `loginAsync()` 方法以確保驗證權杖會附加至後續對服務的呼叫。</span><span class="sxs-lookup"><span data-stu-id="8df95-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="8df95-264"><a name="user-info"></a>做法：取出已驗證的使用者資訊</span><span class="sxs-lookup"><span data-stu-id="8df95-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="8df95-265">當 App Service 驗證使用者時，您可以存取指派的使用者識別碼及其他 .NET 後端程式碼中的資訊。</span><span class="sxs-lookup"><span data-stu-id="8df95-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="8df95-266">此使用者資訊可用於在後端進行授權決策。</span><span class="sxs-lookup"><span data-stu-id="8df95-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="8df95-267">下列程式碼會取得與要求相關聯的使用者識別碼︰</span><span class="sxs-lookup"><span data-stu-id="8df95-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="8df95-268">SID 衍生自提供者特定的使用者識別碼，且對指定的使用者和登入提供者而言都是靜態的。</span><span class="sxs-lookup"><span data-stu-id="8df95-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="8df95-269">SID 對無效的驗證權杖無效。</span><span class="sxs-lookup"><span data-stu-id="8df95-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="8df95-270">App Service 也可讓您向登入提供者要求特定宣告。</span><span class="sxs-lookup"><span data-stu-id="8df95-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="8df95-271">每個識別提供者均可使用識別提供者 SDK 來提供更多資訊。</span><span class="sxs-lookup"><span data-stu-id="8df95-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="8df95-272">例如，您可以將 Facebook 圖形 API 用於朋友的資訊。</span><span class="sxs-lookup"><span data-stu-id="8df95-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="8df95-273">您可以指定在 Azure 入口網站的提供者刀鋒視窗中要求的宣告。</span><span class="sxs-lookup"><span data-stu-id="8df95-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="8df95-274">某些宣告需要搭配識別提供者的額外設定。</span><span class="sxs-lookup"><span data-stu-id="8df95-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="8df95-275">下列程式碼會呼叫 **GetAppServiceIdentityAsync** 擴充方法以取得登入認證，其中包含對 Facebook 圖形 API 提出要求所需的存取權杖：</span><span class="sxs-lookup"><span data-stu-id="8df95-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="8df95-276">新增 `System.Security.Principal` 的 using 陳述式，以提供 **GetAppServiceIdentityAsync** 擴充方法。</span><span class="sxs-lookup"><span data-stu-id="8df95-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="8df95-277"><a name="authorize"></a>做法︰限制授權使用者的資料存取</span><span class="sxs-lookup"><span data-stu-id="8df95-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="8df95-278">在上一節中，我們已說明如何取出已驗證使用者的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="8df95-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="8df95-279">您可以根據此值限制存取資料和其他資源。</span><span class="sxs-lookup"><span data-stu-id="8df95-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="8df95-280">例如，將 userId 資料行新增到資料表，以及依使用者識別碼篩選查詢結果，是一種將傳回的資料限制為只有授權使用者的簡單方式。</span><span class="sxs-lookup"><span data-stu-id="8df95-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="8df95-281">下列程式碼只有在 SID 符合 TodoItem 資料表上 UserId 資料行中的值時才會傳回資料：</span><span class="sxs-lookup"><span data-stu-id="8df95-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="8df95-282">`Query()` 方法會傳回可由 LINQ 操作的 `IQueryable`來處理篩選。</span><span class="sxs-lookup"><span data-stu-id="8df95-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="8df95-283">做法：將推播通知新增至伺服器專案</span><span class="sxs-lookup"><span data-stu-id="8df95-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="8df95-284">透過擴充 **MobileAppConfiguration** 物件並建立通知中樞用戶端，將推播通知加入您的伺服器專案中。</span><span class="sxs-lookup"><span data-stu-id="8df95-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="8df95-285">在 Visual Studio 中，以滑鼠右鍵按一下伺服器專案並按一下 [管理 NuGet 封裝]，搜尋 `Microsoft.Azure.Mobile.Server.Notifications`，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="8df95-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="8df95-286">重複這個步驟以安裝 `Microsoft.Azure.NotificationHubs` 封裝，其中包含通知中樞用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="8df95-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="8df95-287">在 App_Start/Startup.MobileApp.cs 中，於初始化期間新增對 **AddPushNotifications** 擴充方法的呼叫：</span><span class="sxs-lookup"><span data-stu-id="8df95-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="8df95-288">新增下列建立通知中樞用戶端的程式碼：</span><span class="sxs-lookup"><span data-stu-id="8df95-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="8df95-289">您現在可以使用通知中樞用戶端，將推播通知傳送到已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="8df95-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="8df95-290">如需詳細資訊，請參閱 [將推播通知新增至您的應用程式](app-service-mobile-ios-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="8df95-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="8df95-291">若要進一步了解通知中樞，請參閱 [通知中樞概觀](../notification-hubs/notification-hubs-push-notification-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8df95-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="8df95-292"><a name="tags"></a>作法：使用標籤啟用有目標的推播</span><span class="sxs-lookup"><span data-stu-id="8df95-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="8df95-293">通知中樞可讓您使用標記將目標通知傳送至特定註冊。</span><span class="sxs-lookup"><span data-stu-id="8df95-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="8df95-294">自動建立數個標籤︰</span><span class="sxs-lookup"><span data-stu-id="8df95-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="8df95-295">安裝識別碼會識別特定裝置。</span><span class="sxs-lookup"><span data-stu-id="8df95-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="8df95-296">以驗證的 SID 為基礎的使用者識別碼會識別特定使用者。</span><span class="sxs-lookup"><span data-stu-id="8df95-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="8df95-297">您可以從 **MobileServiceClient** 上的 **installationId** 屬性存取安裝識別碼。</span><span class="sxs-lookup"><span data-stu-id="8df95-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="8df95-298">以下範例示範如何在通知中樞內使用安裝識別碼將標記加入特定安裝︰</span><span class="sxs-lookup"><span data-stu-id="8df95-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="8df95-299">建立安裝時，後端會忽略用戶端在推播通知註冊期間提供的任何標籤。</span><span class="sxs-lookup"><span data-stu-id="8df95-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="8df95-300">若要讓用戶端將標籤加入安裝，您必須建立自訂 API，以便加入使用上述模式的標籤。</span><span class="sxs-lookup"><span data-stu-id="8df95-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="8df95-301">如需相關範例，請參閱 App Service Mobile Apps 完整快速入門範例中的[用戶端新增的推播通知標籤][5]。</span><span class="sxs-lookup"><span data-stu-id="8df95-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="8df95-302"><a name="push-user"></a>做法：將推播通知傳送給已驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="8df95-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="8df95-303">當驗證的使用者註冊推播通知之後，使用者識別碼便會自動加入到註冊中。</span><span class="sxs-lookup"><span data-stu-id="8df95-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="8df95-304">藉由使用這個標籤，您可以傳送推播通知給該人員已註冊的所有裝置。</span><span class="sxs-lookup"><span data-stu-id="8df95-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="8df95-305">下列程式碼會取得提出要求之使用者的 SID，並將範本推播通知傳送至該人員的每個裝置註冊︰</span><span class="sxs-lookup"><span data-stu-id="8df95-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="8df95-306">在註冊來自已驗證用戶端的推播通知時，請確定驗證已完成，然後再嘗試註冊。</span><span class="sxs-lookup"><span data-stu-id="8df95-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="8df95-307">如需詳細資訊，請參閱適用於 .NET 後端之 App Service Mobile Apps 完整快速入門範例中的[推播給使用者][6]。</span><span class="sxs-lookup"><span data-stu-id="8df95-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="8df95-308">做法：針對 .NET 伺服器 SDK 進行偵錯和疑難排解</span><span class="sxs-lookup"><span data-stu-id="8df95-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="8df95-309">Azure App Service 提供了數個適用於 ASP.NET 應用程式的偵錯和疑難排解技術：</span><span class="sxs-lookup"><span data-stu-id="8df95-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="8df95-310">監視 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8df95-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="8df95-311">在 Azure App Service 中啟用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="8df95-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="8df95-312">在 Visual Studio 中疑難排解 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8df95-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="8df95-313">記錄</span><span class="sxs-lookup"><span data-stu-id="8df95-313">Logging</span></span>
<span data-ttu-id="8df95-314">您可以使用標準的 ASP.NET 追蹤寫入來寫入 App Service 診斷記錄：</span><span class="sxs-lookup"><span data-stu-id="8df95-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="8df95-315">您必須在行動應用程式後端中啟用診斷，才能寫入至記錄檔。</span><span class="sxs-lookup"><span data-stu-id="8df95-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="8df95-316">若要啟用診斷並寫入至記錄檔：</span><span class="sxs-lookup"><span data-stu-id="8df95-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="8df95-317">依照 [如何啟用診斷](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag)中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="8df95-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="8df95-318">在您的程式碼檔案中新增下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="8df95-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="8df95-319">建立從 .NET 後端寫入至診斷記錄的追蹤寫入器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8df95-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="8df95-320">重新發佈您的伺服器專案，並存取行動應用程式後端，以執行記錄的程式碼路徑。</span><span class="sxs-lookup"><span data-stu-id="8df95-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="8df95-321">下載記錄並進行評估，如 [作法：下載記錄](../app-service-web/web-sites-enable-diagnostic-log.md#download)中所述。</span><span class="sxs-lookup"><span data-stu-id="8df95-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="8df95-322"><a name="local-debug"></a>使用驗證進行本機偵錯</span><span class="sxs-lookup"><span data-stu-id="8df95-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="8df95-323">您可以在將變更發佈至雲端之前，在本機執行您的應用程式以測試變更。</span><span class="sxs-lookup"><span data-stu-id="8df95-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="8df95-324">對於大部分的 Azure Mobile Apps 後端，請在Visual Studio 中時按 F5  。</span><span class="sxs-lookup"><span data-stu-id="8df95-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="8df95-325">不過，使用驗證時有一些其他考量。</span><span class="sxs-lookup"><span data-stu-id="8df95-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="8df95-326">您必須擁有雲端式行動應用程式並且已設定 App Service 驗證/授權，而且您的用戶端必須有指定的雲端端點做為替代登入主機。</span><span class="sxs-lookup"><span data-stu-id="8df95-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="8df95-327">請參閱您用戶端平台的文件，以取得所需的特定步驟。</span><span class="sxs-lookup"><span data-stu-id="8df95-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="8df95-328">確定您的行動後端已安裝 [Microsoft.Azure.Mobile.Server.Authentication] 。</span><span class="sxs-lookup"><span data-stu-id="8df95-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="8df95-329">然後，在 `MobileAppConfiguration` 已套用至您的 `HttpConfiguration` 之後，在您的應用程式的 OWIN 啟動類別中加入下列項目：</span><span class="sxs-lookup"><span data-stu-id="8df95-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="8df95-330">在上述範例中，您應該使用 HTTPS 配置，將 Web.config 檔案中的 authAudience 和 authIssuer 應用程式設定，都設定為您應用程式根目錄的 URL。</span><span class="sxs-lookup"><span data-stu-id="8df95-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="8df95-331">同樣地，您應該將 authSigningKey 設定為您應用程式的簽署金鑰值。</span><span class="sxs-lookup"><span data-stu-id="8df95-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="8df95-332">若要取得簽署金鑰：</span><span class="sxs-lookup"><span data-stu-id="8df95-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="8df95-333">在 [Azure 入口網站]</span><span class="sxs-lookup"><span data-stu-id="8df95-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="8df95-334">按一下 [工具]、[Kudu]、[執行]。</span><span class="sxs-lookup"><span data-stu-id="8df95-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="8df95-335">在 Kudu 管理網站中，按一下 [環境] 。</span><span class="sxs-lookup"><span data-stu-id="8df95-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="8df95-336">尋找 *WEBSITE\_AUTH\_SIGNING\_KEY* 的值。</span><span class="sxs-lookup"><span data-stu-id="8df95-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="8df95-337">在本機應用程式組態中使用 authSigningKey  參數的簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="8df95-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="8df95-338">您的行動後端現已裝備，可在本機執行時驗證用戶端從雲端式端點取得的權杖。</span><span class="sxs-lookup"><span data-stu-id="8df95-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="8df95-339">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="8df95-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="8df95-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="8df95-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="8df95-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="8df95-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="8df95-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="8df95-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="8df95-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="8df95-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="8df95-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="8df95-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="8df95-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="8df95-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
