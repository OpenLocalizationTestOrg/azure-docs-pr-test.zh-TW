---
title: "從行動服務升級為 Azure App Service"
description: "了解如何輕鬆地將您的行動服務應用程式升級為 App Service 行動 App"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 81173b34d0d3b07c5c49d867b1dc5060c7311f12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-to-app-service"></a><span data-ttu-id="bf023-103">將您現有的 .NET Azure 行動服務升級為 App Service</span><span class="sxs-lookup"><span data-stu-id="bf023-103">Upgrade your existing .NET Azure Mobile Service to App Service</span></span>
<span data-ttu-id="bf023-104">App Service Mobile 是一種使用 Microsoft Azure 建置行動應用程式的新方式。</span><span class="sxs-lookup"><span data-stu-id="bf023-104">App Service Mobile is a new way to build mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="bf023-105">若要深入了解，請參閱 [何謂 Mobile Apps？]</span><span class="sxs-lookup"><span data-stu-id="bf023-105">To learn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="bf023-106">本主題說明如何將現有的 .NET 後端應用程式從 Azure 行動服務升級為新的 App Service Mobile Apps。</span><span class="sxs-lookup"><span data-stu-id="bf023-106">This topic describes how to upgrade an existing .NET backend application from Azure Mobile Services to a new App Service Mobile Apps.</span></span> <span data-ttu-id="bf023-107">執行此升級時，您現有的行動服務應用程式可以繼續運作。</span><span class="sxs-lookup"><span data-stu-id="bf023-107">While you perform this upgrade, your existing Mobile Services application can continue to operate.</span></span>   <span data-ttu-id="bf023-108">如果您需要升級 Node.js 後端應用程式，請參閱[升級 Node.js 行動服務](app-service-mobile-node-backend-upgrading-from-mobile-services.md)。</span><span class="sxs-lookup"><span data-stu-id="bf023-108">If you need to upgrade a Node.js backend application, refer to [Upgrading your Node.js Mobile Services](app-service-mobile-node-backend-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="bf023-109">當行動後端升級為 Azure App Service 時，就會具備所有 App Service 功能的存取權，而且會根據 [App Service 定價]而不是行動服務定價進行計費。</span><span class="sxs-lookup"><span data-stu-id="bf023-109">When a mobile backend is upgraded to Azure App Service, it has access to all App Service features and are billed according to [App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="bf023-110">移轉與升級</span><span class="sxs-lookup"><span data-stu-id="bf023-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="bf023-111">建議您在升級之前，先 [執行移轉](app-service-mobile-migrating-from-mobile-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="bf023-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="bf023-112">如此一來，您就能夠在同一個 App Service 方案中放置兩個版本的應用程式，而不需支付額外成本。</span><span class="sxs-lookup"><span data-stu-id="bf023-112">This way, you can put both versions of your application on the same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a><span data-ttu-id="bf023-113">Mobile Apps .NET 伺服器 SDK 中的增強功能</span><span class="sxs-lookup"><span data-stu-id="bf023-113">Improvements in Mobile Apps .NET server SDK</span></span>
<span data-ttu-id="bf023-114">升級為新的 [Mobile Apps SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) 提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="bf023-114">Upgrading to the new [Mobile Apps SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) provides the following benefits:</span></span>

* <span data-ttu-id="bf023-115">NuGet 相依性有更多彈性。</span><span class="sxs-lookup"><span data-stu-id="bf023-115">More flexibility on NuGet dependencies.</span></span> <span data-ttu-id="bf023-116">裝載環境不再提供它自己的 NuGet 封裝版本，因此您可以使用替代的相容版本。</span><span class="sxs-lookup"><span data-stu-id="bf023-116">The hosting environment no longer provides its own versions of NuGet packages, so you can use alternative compatible versions.</span></span> <span data-ttu-id="bf023-117">不過，如果行動伺服器 SDK 或相依性有新的重要 Bug 修正或安全性更新，您必須手動更新您的服務。</span><span class="sxs-lookup"><span data-stu-id="bf023-117">However, if there are new critical bugfixes or security updates to the Mobile Server SDK or dependencies, you must update your service manually.</span></span>
* <span data-ttu-id="bf023-118">Mobile SDK 有更多彈性。</span><span class="sxs-lookup"><span data-stu-id="bf023-118">More flexibility in the mobile SDK.</span></span> <span data-ttu-id="bf023-119">您可以明確地控制設定哪些功能和路由，例如驗證、資料表 API，以及推播註冊端點。</span><span class="sxs-lookup"><span data-stu-id="bf023-119">You can explicitly control which features and routes are set up, such as authentication, table APIs, and the push registration endpoint.</span></span> <span data-ttu-id="bf023-120">若要深入了解，請參閱[如何使用適用於 Azure Mobile Apps 的 .NET 伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="bf023-120">To learn more, see [How to use the .NET server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>
* <span data-ttu-id="bf023-121">支援其他 ASP.NET 專案類型和路由。</span><span class="sxs-lookup"><span data-stu-id="bf023-121">Support for other ASP.NET project types and routes.</span></span> <span data-ttu-id="bf023-122">您現在可以在與行動後端專案相同的專案中裝載 MVC 和 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="bf023-122">You can now host MVC and Web API controllers in the same project as your mobile backend project.</span></span>
* <span data-ttu-id="bf023-123">支援新的 App Service 驗證功能，可讓您跨 Web 和行動應用程式使用常見的驗證設定。</span><span class="sxs-lookup"><span data-stu-id="bf023-123">Support for new App Service authentication features, which allow you to use a common authentication configuration across your web and mobile apps.</span></span>

## <span data-ttu-id="bf023-124"><a name="overview"></a>基本升級概觀</span><span class="sxs-lookup"><span data-stu-id="bf023-124"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="bf023-125">在許多情況下，只需切換到新的 Mobile Apps 伺服器 SDK 並將程式碼重新發佈至新的行動 App 執行個體，即可完成升級。</span><span class="sxs-lookup"><span data-stu-id="bf023-125">In many cases, upgrading will be as simple as switching to the new Mobile Apps server SDK and republishing your code onto a new Mobile App instance.</span></span> <span data-ttu-id="bf023-126">但在某些情況下則需要一些額外的設定，例如進階驗證案例和使用排程工作。</span><span class="sxs-lookup"><span data-stu-id="bf023-126">There are, however some scenarios which will require some additional configuration, such as advanced authentication scenarios and working with scheduled jobs.</span></span> <span data-ttu-id="bf023-127">後續各節將逐一加以討論。</span><span class="sxs-lookup"><span data-stu-id="bf023-127">Each of these is covered in the later sections.</span></span>

> [!TIP]
> <span data-ttu-id="bf023-128">建議您先閱讀並徹底了解本主題的其餘部分，再開始升級。</span><span class="sxs-lookup"><span data-stu-id="bf023-128">It is advised that you read and understand the rest of this topic completely before starting an upgrade.</span></span> <span data-ttu-id="bf023-129">請記下您使用的下列任何功能。</span><span class="sxs-lookup"><span data-stu-id="bf023-129">Make note of any features you use which are called out below.</span></span>
>
>

<span data-ttu-id="bf023-130">行動服務用戶端 SDK 與新的 Mobile Apps 伺服器 SDK「不」  相容。</span><span class="sxs-lookup"><span data-stu-id="bf023-130">The Mobile Services client SDKs are **not** compatible with the new Mobile Apps server SDK.</span></span> <span data-ttu-id="bf023-131">為了提供您應用程式的服務持續性，您不應該將變更發佈至目前正在服務已發佈之用戶端的網站。</span><span class="sxs-lookup"><span data-stu-id="bf023-131">In order to provide continuity of service for your app, you should not publish changes to a site currently serving published clients.</span></span> <span data-ttu-id="bf023-132">而是應該建立新的行動應用程式做為重複項目。</span><span class="sxs-lookup"><span data-stu-id="bf023-132">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="bf023-133">您可以在同一個 App Service 方案中放置此應用程式，以避免產生額外的財務成本。</span><span class="sxs-lookup"><span data-stu-id="bf023-133">You can put this application on the same App Service plan to avoid incurring additional financial cost.</span></span>

<span data-ttu-id="bf023-134">您之後會有兩個版本的應用程式：一個維持不變並為已發佈的現有應用程式提供服務，另一個則可升級且目標為新的用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="bf023-134">You will then have two versions of the application: one which stays the same and serves published apps in the wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="bf023-135">您可依自己的步調移動並測試程式碼，但應該確定您所進行的任何錯誤修正都會套用到這兩個版本。</span><span class="sxs-lookup"><span data-stu-id="bf023-135">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied to both.</span></span> <span data-ttu-id="bf023-136">當您覺得已將現有用戶端應用程式的所需數量升級到最新版本，就可以視需要刪除原本移轉的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf023-136">Once you feel that a desired number of client apps in the wild have updated to the latest version, you can delete the original migrated app if you desire.</span></span>

<span data-ttu-id="bf023-137">完整的升級程序大致如下：</span><span class="sxs-lookup"><span data-stu-id="bf023-137">The full outline for the upgrade process is as follows:</span></span>

1. <span data-ttu-id="bf023-138">建立新的行動 App</span><span class="sxs-lookup"><span data-stu-id="bf023-138">Create a new Mobile App</span></span>
2. <span data-ttu-id="bf023-139">更新專案以使用新的伺服器 SDK</span><span class="sxs-lookup"><span data-stu-id="bf023-139">Update the project to use the new Server SDKs</span></span>
3. <span data-ttu-id="bf023-140">發行新版的用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="bf023-140">Release a new version of your client application</span></span>
4. <span data-ttu-id="bf023-141">(選擇性) 刪除原始已移轉的執行個體</span><span class="sxs-lookup"><span data-stu-id="bf023-141">(Optional) Delete your original migrated instance</span></span>

## <span data-ttu-id="bf023-142"><a name="mobile-app-version"></a>建立第二個應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="bf023-142"><a name="mobile-app-version"></a>Creating a second application instance</span></span>
<span data-ttu-id="bf023-143">升級的第一個步驟是建立將主控新版應用程式的行動 App 資源。</span><span class="sxs-lookup"><span data-stu-id="bf023-143">The first step in upgrading is to create the Mobile App resource which will host the new version of your application.</span></span> <span data-ttu-id="bf023-144">如果您已經移轉現有的行動服務，則您會想要在同一個主控方案中建立這個版本。</span><span class="sxs-lookup"><span data-stu-id="bf023-144">If you have already migrated an existing mobile service, you will want to create this version on the same hosting plan.</span></span> <span data-ttu-id="bf023-145">請開啟 [Azure 入口網站] ，並瀏覽到您已移轉的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf023-145">Open the [Azure portal] and navigate to your migrated application.</span></span> <span data-ttu-id="bf023-146">請記下其正在其上執行的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="bf023-146">Make note of the App Service Plan it is running on.</span></span>

<span data-ttu-id="bf023-147">接下來，依照 [.NET 後端建立指示](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app)建立第二個應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="bf023-147">Next, create the second application instance by following the [.NET backend creation instructions](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app).</span></span> <span data-ttu-id="bf023-148">當系統提示選取您的 App Service 方案或「主控方案」時，請選擇已移轉之應用程式的方案。</span><span class="sxs-lookup"><span data-stu-id="bf023-148">When prompted to select you App Service Plan or "hosting plan" choose the plan of your migrated application.</span></span>

<span data-ttu-id="bf023-149">您可能會想要使用與行動服務中相同的資料庫和通知中心。</span><span class="sxs-lookup"><span data-stu-id="bf023-149">You will likely want to use the same database and Notification Hub as you did in Mobile Services.</span></span> <span data-ttu-id="bf023-150">您可以複製這些值，方法是開啟 [Azure 入口網站]、瀏覽至原始的應用程式，然後依序按一下 [設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="bf023-150">You can copy these values by opening [Azure portal] and navigating to the original application, then click **Settings** > **Application settings**.</span></span> <span data-ttu-id="bf023-151">在 [連接字串] 下，複製 `MS_NotificationHubConnectionString` 和 `MS_TableConnectionString`。</span><span class="sxs-lookup"><span data-stu-id="bf023-151">Under **Connection Strings**, copy `MS_NotificationHubConnectionString` and `MS_TableConnectionString`.</span></span> <span data-ttu-id="bf023-152">瀏覽至新的升級網站並將它們貼上，覆寫任何現有的值。</span><span class="sxs-lookup"><span data-stu-id="bf023-152">Navigate to your new upgrade site and paste them in, overwriting any existing values.</span></span> <span data-ttu-id="bf023-153">針對您的應用程式需要的任何其他應用程式設定重複執行此程序。</span><span class="sxs-lookup"><span data-stu-id="bf023-153">Repeat this process for any other application settings your app needs.</span></span> <span data-ttu-id="bf023-154">如果不使用移轉的服務，您可以從 [Azure 傳統入口網站]上 [行動服務] 區段的 [設定] 索引標籤，讀取連接字串和 app 設定。</span><span class="sxs-lookup"><span data-stu-id="bf023-154">If not using a migrated service, you can read connection strings and app settings from the **Configure** tab of the Mobile Services section of the [Azure classic portal].</span></span>

<span data-ttu-id="bf023-155">針對您的應用程式製作 ASP.NET 專案的複本，然後將它發佈到新的網站。</span><span class="sxs-lookup"><span data-stu-id="bf023-155">Make a copy of the ASP.NET project for your application and publish it to your new site.</span></span> <span data-ttu-id="bf023-156">透過利用新 URL 更新的用戶端應用程式複本，驗證一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="bf023-156">Using a copy of your client application updated with the new URL, validate that everything works as expected.</span></span>

## <a name="updating-the-server-project"></a><span data-ttu-id="bf023-157">更新伺服器專案</span><span class="sxs-lookup"><span data-stu-id="bf023-157">Updating the server project</span></span>
<span data-ttu-id="bf023-158">行動應用程式有新的 [行動應用程式伺服器 SDK] ，提供許多與行動服務執行階段相同的功能。</span><span class="sxs-lookup"><span data-stu-id="bf023-158">Mobile Apps provides a new [Mobile App Server SDK] which provides much of the same functionality as the Mobile Services runtime.</span></span> <span data-ttu-id="bf023-159">首先，您應該移除對行動服務封裝的所有參考。</span><span class="sxs-lookup"><span data-stu-id="bf023-159">First, you should remove all references to the Mobile Services packages.</span></span> <span data-ttu-id="bf023-160">在 NuGet 封裝管理員中，搜尋 `WindowsAzure.MobileServices.Backend`。</span><span class="sxs-lookup"><span data-stu-id="bf023-160">In the NuGet package manager, search for `WindowsAzure.MobileServices.Backend`.</span></span> <span data-ttu-id="bf023-161">大部分的 app 將會在此處看見數個封裝，包括 `WindowsAzure.MobileServices.Backend.Tables` 和 `WindowsAzure.MobileServices.Backend.Entity`。</span><span class="sxs-lookup"><span data-stu-id="bf023-161">Most apps will see several packages here, including `WindowsAzure.MobileServices.Backend.Tables` and `WindowsAzure.MobileServices.Backend.Entity`.</span></span> <span data-ttu-id="bf023-162">在這種情況下，請從相依性樹狀目錄中的最低封裝 (例如 `Entity`) 開始，然後將它移除。</span><span class="sxs-lookup"><span data-stu-id="bf023-162">In such a case, start with the lowest package in the dependency tree, such as `Entity`, and remove it.</span></span> <span data-ttu-id="bf023-163">出現提示時，請勿移除所有相依的封裝。</span><span class="sxs-lookup"><span data-stu-id="bf023-163">When prompted, do not remove all dependant packages.</span></span> <span data-ttu-id="bf023-164">重複執行此程序，直到您移除了 `WindowsAzure.MobileServices.Backend` 本身為止。</span><span class="sxs-lookup"><span data-stu-id="bf023-164">Repeat this process until you have removed `WindowsAzure.MobileServices.Backend` itself.</span></span>

<span data-ttu-id="bf023-165">此時，您的專案將不再參考行動服務 SDK。</span><span class="sxs-lookup"><span data-stu-id="bf023-165">At this point you will have a project that no longer references Mobile Services SDKs.</span></span>

<span data-ttu-id="bf023-166">接下來，將新增 Mobile Apps SDK 的參考。</span><span class="sxs-lookup"><span data-stu-id="bf023-166">Next you will add references the Mobile Apps SDK.</span></span> <span data-ttu-id="bf023-167">在此升級中，大部分的開發人員都想要下載並安裝 `Microsoft.Azure.Mobile.Server.Quickstart` 封裝，因為這將會在整個必要集中提取。</span><span class="sxs-lookup"><span data-stu-id="bf023-167">For this upgrade, most developers will want to download and install the `Microsoft.Azure.Mobile.Server.Quickstart` package, as this will pull in the entire required set.</span></span>

<span data-ttu-id="bf023-168">屆時將會有不少因 SDK 之間的差異而產生的編譯器錯誤，但這些錯誤都很容易處理且將於本節的其餘部分加以說明。</span><span class="sxs-lookup"><span data-stu-id="bf023-168">There will be quite a few compiler errors resulting from differences between the SDKs, but these are easy to address and are covered in the rest of this section.</span></span>

### <a name="base-configuration"></a><span data-ttu-id="bf023-169">基本組態</span><span class="sxs-lookup"><span data-stu-id="bf023-169">Base configuration</span></span>
<span data-ttu-id="bf023-170">然後，在 WebApiConfig.cs 中，您可以取代：</span><span class="sxs-lookup"><span data-stu-id="bf023-170">Then, in WebApiConfig.cs, you can replace:</span></span>

        // Use this class to set configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class to set WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

<span data-ttu-id="bf023-171">取代為</span><span class="sxs-lookup"><span data-stu-id="bf023-171">with</span></span>

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> <span data-ttu-id="bf023-172">如果您想要深入了解新的 .NET 伺服器 SDK 以及如何從您的 app 新增/移除功能，請參閱 [如何使用 .NET 伺服器 SDK] 主題。</span><span class="sxs-lookup"><span data-stu-id="bf023-172">If you wish to learn more about the new .NET server SDK and how to add/remove features from your app, please see the [How to use the .NET server SDK] topic.</span></span>
>
>

<span data-ttu-id="bf023-173">如果您的應用程式會使用驗證功能，您也必須註冊 OWIN 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="bf023-173">If your app makes use of the authentication features, you will also need to register an OWIN middleware.</span></span> <span data-ttu-id="bf023-174">在此情況下，您應該將上述組態程式碼移入新的 OWIN 啟動類別。</span><span class="sxs-lookup"><span data-stu-id="bf023-174">In this case, you should move the above configuration code into a new OWIN Startup class.</span></span>

1. <span data-ttu-id="bf023-175">如果 NuGet 封裝 `Microsoft.Owin.Host.SystemWeb` 尚未包含於專案中，請新增它。</span><span class="sxs-lookup"><span data-stu-id="bf023-175">Add the NuGet package `Microsoft.Owin.Host.SystemWeb` if it is not already included in your project.</span></span>
2. <span data-ttu-id="bf023-176">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選取 [新增] -> [新項目]。</span><span class="sxs-lookup"><span data-stu-id="bf023-176">In Visual Studio, right click on your project and select **Add** -> **New Item**.</span></span> <span data-ttu-id="bf023-177">依序選取 [Web] -> [一般] -> [OWIN 啟動類別]。</span><span class="sxs-lookup"><span data-stu-id="bf023-177">Select **Web** -> **General** -> **OWIN Startup class**.</span></span>
3. <span data-ttu-id="bf023-178">將 MobileAppConfiguration 的上述程式碼從 `WebApiConfig.Register()` 移至您新啟動類別的 `Configuration()` 方法。</span><span class="sxs-lookup"><span data-stu-id="bf023-178">Move the above code for MobileAppConfiguration from `WebApiConfig.Register()` to the `Configuration()` method of your new startup class.</span></span>

<span data-ttu-id="bf023-179">確定 `Configuration()` 方法的結尾：</span><span class="sxs-lookup"><span data-stu-id="bf023-179">Make sure the `Configuration()` method ends with:</span></span>

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

<span data-ttu-id="bf023-180">有一些其他與驗證相關的變更，這些內容涵蓋於下列的完整驗證章節中。</span><span class="sxs-lookup"><span data-stu-id="bf023-180">There are additional changes related to authentication which are covered in the full authentication section below.</span></span>

### <a name="working-with-data"></a><span data-ttu-id="bf023-181">使用資料</span><span class="sxs-lookup"><span data-stu-id="bf023-181">Working with Data</span></span>
<span data-ttu-id="bf023-182">在行動服務中，會提供行動 app 名稱做為 Entity Framework 安裝程式中的預設結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="bf023-182">In Mobile Services, the mobile app name served as the default schema name in the Entity Framework setup.</span></span>

<span data-ttu-id="bf023-183">若要確定您的結構描述與之前參考的一樣，請使用下列內容來設定 DbContext 中適用於您應用程式的結構描述：</span><span class="sxs-lookup"><span data-stu-id="bf023-183">To ensure that you have the same schema being referenced as before, use the following to set the schema in the DbContext for your application:</span></span>

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

<span data-ttu-id="bf023-184">如果您執行了上述設定，請確定您具有 MS_MobileServiceName。</span><span class="sxs-lookup"><span data-stu-id="bf023-184">Please make sure you have MS_MobileServiceName set if you do the above.</span></span> <span data-ttu-id="bf023-185">如果您的應用程式先前已自訂這個結構描述，您也可以提供另一個結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="bf023-185">You can also provide another schema name if your application customized this previously.</span></span>

### <a name="system-properties"></a><span data-ttu-id="bf023-186">系統屬性</span><span class="sxs-lookup"><span data-stu-id="bf023-186">System Properties</span></span>
#### <a name="naming"></a><span data-ttu-id="bf023-187">命名</span><span class="sxs-lookup"><span data-stu-id="bf023-187">Naming</span></span>
<span data-ttu-id="bf023-188">在 Azure 行動服務伺服器 SDK 中，系統屬性一律會包含適用於屬性的雙底線 (`__`) 前置詞：</span><span class="sxs-lookup"><span data-stu-id="bf023-188">In the Azure Mobile Services server SDK, system properties always contain a double underscore (`__`) prefix for the properties:</span></span>

* <span data-ttu-id="bf023-189">__createdAt</span><span class="sxs-lookup"><span data-stu-id="bf023-189">__createdAt</span></span>
* <span data-ttu-id="bf023-190">__updatedAt</span><span class="sxs-lookup"><span data-stu-id="bf023-190">__updatedAt</span></span>
* <span data-ttu-id="bf023-191">__deleted</span><span class="sxs-lookup"><span data-stu-id="bf023-191">__deleted</span></span>
* <span data-ttu-id="bf023-192">__version</span><span class="sxs-lookup"><span data-stu-id="bf023-192">__version</span></span>

<span data-ttu-id="bf023-193">行動服務用戶端 SDK 具有特殊的邏輯，可用來剖析這種格式的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="bf023-193">The Mobile Services client SDKs have special logic for parsing system properties in this format.</span></span>

<span data-ttu-id="bf023-194">在 Azure Mobile Apps 中，系統屬性不再具有特殊格式並具有下列名稱：</span><span class="sxs-lookup"><span data-stu-id="bf023-194">In Azure Mobile Apps, system properties no longer have a special format and have the following names:</span></span>

* <span data-ttu-id="bf023-195">建立時間</span><span class="sxs-lookup"><span data-stu-id="bf023-195">createdAt</span></span>
* <span data-ttu-id="bf023-196">更新時間</span><span class="sxs-lookup"><span data-stu-id="bf023-196">updatedAt</span></span>
* <span data-ttu-id="bf023-197">已刪除</span><span class="sxs-lookup"><span data-stu-id="bf023-197">deleted</span></span>
* <span data-ttu-id="bf023-198">版本</span><span class="sxs-lookup"><span data-stu-id="bf023-198">version</span></span>

<span data-ttu-id="bf023-199">Mobile Apps 用戶端 SDK 會使用新的系統屬性名稱，因此不需要對用戶端程式碼進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="bf023-199">The Mobile Apps client SDKs use the new system properties names, so no changes are required to client code.</span></span> <span data-ttu-id="bf023-200">不過，如果您要直接對服務進行 REST 呼叫，則您應該據以變更您的查詢。</span><span class="sxs-lookup"><span data-stu-id="bf023-200">However, if you are directly making REST calls to your service then you should change your queries accordingly.</span></span>

#### <a name="local-store"></a><span data-ttu-id="bf023-201">本機存放區</span><span class="sxs-lookup"><span data-stu-id="bf023-201">Local store</span></span>
<span data-ttu-id="bf023-202">變更系統屬性的名稱，表示適用於行動服務的離線同步處理本機資料庫與 Mobile Apps 不相容。</span><span class="sxs-lookup"><span data-stu-id="bf023-202">The changes to the names of system properties mean that an offline sync local database for Mobile Services is not compatible with Mobile Apps.</span></span> <span data-ttu-id="bf023-203">如果可能，在將暫止的變更傳送到伺服器之前，您應該避免將用戶端應用程式從行動服務升級為 Mobile Apps。</span><span class="sxs-lookup"><span data-stu-id="bf023-203">If possible, you should avoid upgrading client apps from Mobile Services to Mobile Apps until after pending changes have been sent to the server.</span></span> <span data-ttu-id="bf023-204">接著，升級的應用程式應該使用新的資料庫檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="bf023-204">Then, the upgraded app should use a new database filename.</span></span>

<span data-ttu-id="bf023-205">如果用戶端應用程式是從行動服務升級為 Mobile Apps，但同時在操作佇列中有暫止的離線變更，則系統資料庫必須更新，才能使用新的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="bf023-205">If a client app is upgraded from Mobile Services to Mobile Apps while there are pending offline changes in the operation queue, then the system database must be updated to use the new column names.</span></span> <span data-ttu-id="bf023-206">在 iOS 上，可以使用輕量型移轉來變更資料行名稱，以達成這一點。</span><span class="sxs-lookup"><span data-stu-id="bf023-206">On iOS, this can be achieved using lightweight migrations to change the column names.</span></span> <span data-ttu-id="bf023-207">在 Android 和 .NET Managed 用戶端上，您應該撰寫自訂的 SQL，為資料物件資料表的資料行重新命名。</span><span class="sxs-lookup"><span data-stu-id="bf023-207">On Android and the .NET managed client, you should write custom SQL to rename the columns for your data object tables.</span></span>

<span data-ttu-id="bf023-208">在 iOS 上，您應該變更資料實體的核心資料結構描述，來符合下列內容。</span><span class="sxs-lookup"><span data-stu-id="bf023-208">On iOS, you should change your Core Data schema for your data entities to match the following.</span></span> <span data-ttu-id="bf023-209">請注意，屬性 `createdAt`、`updatedAt` 和 `version` 不再需要 `ms_` 前置詞：</span><span class="sxs-lookup"><span data-stu-id="bf023-209">Note that the properties `createdAt`, `updatedAt` and `version` no longer have an `ms_` prefix:</span></span>

| <span data-ttu-id="bf023-210">屬性</span><span class="sxs-lookup"><span data-stu-id="bf023-210">Attribute</span></span> | <span data-ttu-id="bf023-211">類型</span><span class="sxs-lookup"><span data-stu-id="bf023-211">Type</span></span> | <span data-ttu-id="bf023-212">注意</span><span class="sxs-lookup"><span data-stu-id="bf023-212">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bf023-213">id</span><span class="sxs-lookup"><span data-stu-id="bf023-213">id</span></span> |<span data-ttu-id="bf023-214">字串 (標示為必要)</span><span class="sxs-lookup"><span data-stu-id="bf023-214">String, marked required</span></span> |<span data-ttu-id="bf023-215">遠端存放區中的主索引鍵</span><span class="sxs-lookup"><span data-stu-id="bf023-215">primary key in remote store</span></span> |
| <span data-ttu-id="bf023-216">建立時間</span><span class="sxs-lookup"><span data-stu-id="bf023-216">createdAt</span></span> |<span data-ttu-id="bf023-217">日期</span><span class="sxs-lookup"><span data-stu-id="bf023-217">Date</span></span> |<span data-ttu-id="bf023-218">(選擇性) 對應至 createdAt 系統屬性</span><span class="sxs-lookup"><span data-stu-id="bf023-218">(optional) maps to createdAt system property</span></span> |
| <span data-ttu-id="bf023-219">更新時間</span><span class="sxs-lookup"><span data-stu-id="bf023-219">updatedAt</span></span> |<span data-ttu-id="bf023-220">日期</span><span class="sxs-lookup"><span data-stu-id="bf023-220">Date</span></span> |<span data-ttu-id="bf023-221">(選擇性) 對應至 updatedAt 系統屬性</span><span class="sxs-lookup"><span data-stu-id="bf023-221">(optional) maps to updatedAt system property</span></span> |
| <span data-ttu-id="bf023-222">版本</span><span class="sxs-lookup"><span data-stu-id="bf023-222">version</span></span> |<span data-ttu-id="bf023-223">String</span><span class="sxs-lookup"><span data-stu-id="bf023-223">String</span></span> |<span data-ttu-id="bf023-224">(選擇性) 用來偵測衝突，對應至版本</span><span class="sxs-lookup"><span data-stu-id="bf023-224">(optional) used to detect conflicts, maps to version</span></span> |

#### <a name="querying-system-properties"></a><span data-ttu-id="bf023-225">查詢系統屬性</span><span class="sxs-lookup"><span data-stu-id="bf023-225">Querying system properties</span></span>
<span data-ttu-id="bf023-226">在 Azure 行動服務中，預設不會傳送系統屬性，只有在使用查詢字串 `__systemProperties`要求它們時才會傳送。</span><span class="sxs-lookup"><span data-stu-id="bf023-226">In Azure Mobile Services, system properties are not sent by default, but only when they are requested using the query string `__systemProperties`.</span></span> <span data-ttu-id="bf023-227">相反地，在 Azure Mobile Apps 中，會 **一律選取** 系統屬性，因為它們是伺服器 SDK 物件模型的一部分。</span><span class="sxs-lookup"><span data-stu-id="bf023-227">In contrast, in Azure Mobile Apps system properties are **always selected** since they are part of the server SDK object model.</span></span>

<span data-ttu-id="bf023-228">這項變更主要會影響網域管理員的自訂實作，例如 `MappedEntityDomainManager`的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="bf023-228">This change mainly impacts custom implementations of domain managers, such as extensions of `MappedEntityDomainManager`.</span></span> <span data-ttu-id="bf023-229">在行動服務中，如果用戶端永遠不會要求任何系統屬性，就可以使用 `MappedEntityDomainManager` ，這實際上不會對應所有屬性。</span><span class="sxs-lookup"><span data-stu-id="bf023-229">In Mobile Services, if a client never requests any system properties, it is possible to use a `MappedEntityDomainManager` that does not actually map all properties.</span></span> <span data-ttu-id="bf023-230">不過，在 Azure Mobile Apps 中，這些未對應的屬性將導致 GET 查詢發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="bf023-230">However, in Azure Mobile Apps, these unmapped properties will cause an error in GET queries.</span></span>

<span data-ttu-id="bf023-231">解決此問題的最簡單方式是修改您的 DTO，讓它們繼承自 `ITableData` 而非 `EntityData`。</span><span class="sxs-lookup"><span data-stu-id="bf023-231">The easiest way to resolve the issue is to modify your DTOs so that they inherit from `ITableData` instead of `EntityData`.</span></span> <span data-ttu-id="bf023-232">接著，將 `[NotMapped]` 屬性新增到應省略的欄位。</span><span class="sxs-lookup"><span data-stu-id="bf023-232">Then, add the `[NotMapped]` attribute to the fields that should be omitted.</span></span>

<span data-ttu-id="bf023-233">例如，下列範例會定義 `TodoItem` 且不使用任何系統屬性：</span><span class="sxs-lookup"><span data-stu-id="bf023-233">For example, the following defines `TodoItem` with no system properties:</span></span>

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

<span data-ttu-id="bf023-234">附註：如果您收到有關 `NotMapped` 的錯誤，請將參考新增至組件 `System.ComponentModel.DataAnnotations`。</span><span class="sxs-lookup"><span data-stu-id="bf023-234">Note: if you get errors on `NotMapped`, add a reference to the assembly `System.ComponentModel.DataAnnotations`.</span></span>

### <a name="cors"></a><span data-ttu-id="bf023-235">CORS</span><span class="sxs-lookup"><span data-stu-id="bf023-235">CORS</span></span>
<span data-ttu-id="bf023-236">行動服務藉由包裝 ASP.NET CORS 解決方案，來包含一些適用於 CORS 的支援。</span><span class="sxs-lookup"><span data-stu-id="bf023-236">Mobile Services included some support for CORS by wrapping the ASP.NET CORS solution.</span></span> <span data-ttu-id="bf023-237">這個包裝層級已移除，以便讓開發人員擁有更多控制權，因此，您可以直接運用 [ASP.NET CORS 支援](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)。</span><span class="sxs-lookup"><span data-stu-id="bf023-237">This wrapping layer has been removed to give the developer more control, so you can directly leverage [ASP.NET CORS support](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

<span data-ttu-id="bf023-238">而使用 CORS 的主要考量，在於您必須允許使用 `eTag` 和 `Location` 標頭，用戶端 SDK 才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="bf023-238">The main areas of concern if using CORS are that the `eTag` and `Location` headers must be allowed in order for the client SDKs to work properly.</span></span>

### <a name="push-notifications"></a><span data-ttu-id="bf023-239">推播通知</span><span class="sxs-lookup"><span data-stu-id="bf023-239">Push Notifications</span></span>
<span data-ttu-id="bf023-240">對於推播，您可能會發現伺服器 SDK 中遺漏的主要項目是 PushRegistrationHandler 類別。</span><span class="sxs-lookup"><span data-stu-id="bf023-240">For push, the main item that you may find missing from the Server SDK is the PushRegistrationHandler class.</span></span> <span data-ttu-id="bf023-241">註冊在行動應用程式中處理方式稍有不同，依預設會啟用不具標籤的註冊。</span><span class="sxs-lookup"><span data-stu-id="bf023-241">Registrations are handled slightly differently in Mobile Apps, and tagless registrations are enabled by default.</span></span> <span data-ttu-id="bf023-242">管理標籤可使用自訂 API 來完成。</span><span class="sxs-lookup"><span data-stu-id="bf023-242">Managing tags may be accomplished by using custom APIs.</span></span> <span data-ttu-id="bf023-243">如需詳細資訊，請參閱 [註冊標籤](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) 的指示。</span><span class="sxs-lookup"><span data-stu-id="bf023-243">Please see the [registering for tags](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instructions for more information.</span></span>

### <a name="scheduled-jobs"></a><span data-ttu-id="bf023-244">排程的工作</span><span class="sxs-lookup"><span data-stu-id="bf023-244">Scheduled Jobs</span></span>
<span data-ttu-id="bf023-245">Mobile Apps 中並未內建排程的工作，因此您在 .NET 後端中的任何現有工作都必須個別升級。</span><span class="sxs-lookup"><span data-stu-id="bf023-245">Scheduled jobs are not built into Mobile Apps, so any existing jobs that you have in your .NET backend will need to be upgraded individually.</span></span> <span data-ttu-id="bf023-246">其中一個選項是在行動應用程式程式碼網站上建立排程 [Web 工作] 。</span><span class="sxs-lookup"><span data-stu-id="bf023-246">One option is to create a scheduled [Web Job] on the Mobile App code site.</span></span> <span data-ttu-id="bf023-247">您也可以設定用來保存工作程式碼的控制器，並設定依預期的排程在端點上執行的 [Azure 排程器] 。</span><span class="sxs-lookup"><span data-stu-id="bf023-247">You could also set up a controller that holds your job code and configure the [Azure Scheduler] to hit that endpoint on the expected schedule.</span></span>

### <a name="miscellaneous-changes"></a><span data-ttu-id="bf023-248">其他變更</span><span class="sxs-lookup"><span data-stu-id="bf023-248">Miscellaneous changes</span></span>
<span data-ttu-id="bf023-249">行動用戶端將取用的所有 ApiControllers 現在必須具備 `[MobileAppController]` 屬性。</span><span class="sxs-lookup"><span data-stu-id="bf023-249">All ApiControllers which will be consumed by a mobile client must now have the `[MobileAppController]` attribute.</span></span> <span data-ttu-id="bf023-250">預設不再包含此屬性，因此，其他 ApiControllers 不會受到行動格式器所影響。</span><span class="sxs-lookup"><span data-stu-id="bf023-250">This is no longer included by default so that other ApiControllers to go unaffected by the mobile formatters.</span></span>

<span data-ttu-id="bf023-251">`ApiServices` 物件不再是 SDK 的一部分。</span><span class="sxs-lookup"><span data-stu-id="bf023-251">The `ApiServices` object is no longer part of the SDK.</span></span> <span data-ttu-id="bf023-252">若要存取行動應用程式設定，您可以使用下列：</span><span class="sxs-lookup"><span data-stu-id="bf023-252">To access Mobile App settings, you can use the following:</span></span>

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

<span data-ttu-id="bf023-253">同樣地，現在已使用標準 ASP.NET 追蹤寫入完成記錄︰</span><span class="sxs-lookup"><span data-stu-id="bf023-253">Similarly, logging is now accomplished using the standard ASP.NET trace writing:</span></span>

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <span data-ttu-id="bf023-254"><a name="authentication"></a>驗證考量</span><span class="sxs-lookup"><span data-stu-id="bf023-254"><a name="authentication"></a>Authentication considerations</span></span>
<span data-ttu-id="bf023-255">行動服務的驗證元件現在已移到 App Service 驗證/授權功能中。</span><span class="sxs-lookup"><span data-stu-id="bf023-255">The authentication components of Mobile Services have now been moved into the App Service Authentication/Authorization feature.</span></span> <span data-ttu-id="bf023-256">您可以閱讀 [將驗證新增至您行動應用程式](app-service-mobile-ios-get-started-users.md) 一文，以了解如何為網站啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="bf023-256">You can learn about enabling this for your site by reading the [Add authentication to your mobile app](app-service-mobile-ios-get-started-users.md) topic.</span></span>

<span data-ttu-id="bf023-257">對於某些提供者 (例如 AAD、Facebook 及 Google)，您應該能夠運用來自您複製應用程式的現有註冊。</span><span class="sxs-lookup"><span data-stu-id="bf023-257">For some providers, such as AAD, Facebook, and Google, you should be able to leverage the existing registration from your copy application.</span></span> <span data-ttu-id="bf023-258">您只需瀏覽至身分識別提供者的入口網站，並將新的重新導向 URL 新增至註冊即可。</span><span class="sxs-lookup"><span data-stu-id="bf023-258">You simply need to navigate to the identity provider's portal and add a new redirect URL to the registration.</span></span> <span data-ttu-id="bf023-259">接著，利用用戶端識別碼和密碼來設定 App Service 驗證/授權。</span><span class="sxs-lookup"><span data-stu-id="bf023-259">Then configure App Service Authentication/Authorization with the client ID and secret.</span></span>

### <a name="controller-action-authorization"></a><span data-ttu-id="bf023-260">控制器動作授權</span><span class="sxs-lookup"><span data-stu-id="bf023-260">Controller action authorization</span></span>
<span data-ttu-id="bf023-261">`[AuthorizeLevel(AuthorizationLevel.User)]` 屬性的所有執行個體現在都必須變更，以使用標準的 ASP.NET `[Authorize]` 屬性。</span><span class="sxs-lookup"><span data-stu-id="bf023-261">Any instances of the `[AuthorizeLevel(AuthorizationLevel.User)]` attribute must now be changed to use the standard ASP.NET `[Authorize]` attribute.</span></span> <span data-ttu-id="bf023-262">此外，根據預設，控制器現在是匿名的，就如同在其他 ASP.NET 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="bf023-262">Additionally, controllers are now Anonymous by default, as in other ASP.NET applications.</span></span>
<span data-ttu-id="bf023-263">如果您使用其中一個其他 AuthorizeLevel 選項 (例如系統管理員或應用程式)，請注意，這些項目都不見了。</span><span class="sxs-lookup"><span data-stu-id="bf023-263">If you were using one of the other AuthorizeLevel options, such as Admin or Application, please note that these are gone.</span></span> <span data-ttu-id="bf023-264">您可以改為設定共用密碼的 AuthorizationFilters，或者設定 AAD 服務主體，安全地啟用服務對服務的呼叫。</span><span class="sxs-lookup"><span data-stu-id="bf023-264">You can instead set up AuthorizationFilters for shared secrets or configure an AAD Service Principal to enable service-to-service calls securely.</span></span>

### <a name="getting-additional-user-information"></a><span data-ttu-id="bf023-265">取得其他使用者資訊</span><span class="sxs-lookup"><span data-stu-id="bf023-265">Getting additional user information</span></span>
<span data-ttu-id="bf023-266">您可以取得其他使用者資訊，包括透過 `GetAppServiceIdentityAsync()` 方法存取權杖：</span><span class="sxs-lookup"><span data-stu-id="bf023-266">You can get additional user information, including access tokens through the `GetAppServiceIdentityAsync()` method:</span></span>

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

<span data-ttu-id="bf023-267">此外，如果您的應用程式依存於使用者識別碼 (例如，將它們儲存於資料庫中)，請務必注意，行動服務和 App Service Mobile Apps 之間的使用者識別碼是不同的。</span><span class="sxs-lookup"><span data-stu-id="bf023-267">Additionally, if your application takes dependencies on user IDs, such as storing them in a database, it is important to note that the user IDs between Mobile Services and App Service Mobile Apps are different.</span></span> <span data-ttu-id="bf023-268">不過，您仍然可以取得行動服務使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="bf023-268">You can still get the Mobile Services User ID, though.</span></span> <span data-ttu-id="bf023-269">所有的 ProviderCredentials 子類別都具有 UserId 屬性。</span><span class="sxs-lookup"><span data-stu-id="bf023-269">All of the ProviderCredentials subclasses have a UserId property.</span></span> <span data-ttu-id="bf023-270">因此，繼續之前的範例：</span><span class="sxs-lookup"><span data-stu-id="bf023-270">So continuing from the example before:</span></span>

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

<span data-ttu-id="bf023-271">如果您的應用程式依存於使用者識別碼，請務必盡可能使用相同的身分識別提供者註冊。</span><span class="sxs-lookup"><span data-stu-id="bf023-271">If your app does take any dependencies on user IDs, it is important that you leverage the same registration with an identity provider if possible.</span></span> <span data-ttu-id="bf023-272">使用者識別碼的範圍通常限定在已使用的應用程式註冊，因此引入新的註冊，可能會讓使用者在比對其資料時發生問題。</span><span class="sxs-lookup"><span data-stu-id="bf023-272">User IDs are typically scoped to the application registration that was used, so introducing a new registration could create problems with matching users to their data.</span></span>

### <a name="custom-authentication"></a><span data-ttu-id="bf023-273">自訂驗證</span><span class="sxs-lookup"><span data-stu-id="bf023-273">Custom authentication</span></span>
<span data-ttu-id="bf023-274">如果您的應用程式使用自訂的驗證解決方案，您會想要確定已升級的網站具備系統的存取權。</span><span class="sxs-lookup"><span data-stu-id="bf023-274">If your app is using a custom authentication solution, you will want to make sure that the upgraded site has access to the system.</span></span> <span data-ttu-id="bf023-275">請依照 [.NET 伺服器 SDK 概觀] 中適用於自訂驗證的新指示來整合您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="bf023-275">Follow the new instructions for custom authentication in the [.NET server SDK overview] to integrate your solution.</span></span> <span data-ttu-id="bf023-276">請注意，自訂驗證元件仍處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="bf023-276">Please note that the custom authentication components are still in preview.</span></span>

## <span data-ttu-id="bf023-277"><a name="updating-clients"></a>更新用戶端</span><span class="sxs-lookup"><span data-stu-id="bf023-277"><a name="updating-clients"></a>Updating clients</span></span>
<span data-ttu-id="bf023-278">在您擁有可運作的行動 App 後端之後，就能在取用它的新版用戶端應用程式上運作。</span><span class="sxs-lookup"><span data-stu-id="bf023-278">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="bf023-279">Mobile Apps 也會包含新版的用戶端 SDK，而且與上述的伺服器升級類似，您必須先移除所有對行動服務 SDK 的參考，然後安裝 Mobile Apps 版本。</span><span class="sxs-lookup"><span data-stu-id="bf023-279">Mobile Apps also includes a new version of the client SDKs, and similar to the server upgrade above, you will need to remove all references to the Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="bf023-280">版本間的其中一個主要變更是建構函式不再需要應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf023-280">One of the main changes between the versions is that the constructors no longer require an application key.</span></span> <span data-ttu-id="bf023-281">您現在只需傳入行動 App 的 URL。</span><span class="sxs-lookup"><span data-stu-id="bf023-281">You now simply pass in the URL of your Mobile App.</span></span> <span data-ttu-id="bf023-282">例如，在 .NET 用戶端上， `MobileServiceClient` 建構函式現在是：</span><span class="sxs-lookup"><span data-stu-id="bf023-282">For example, on the .NET clients, the `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of the Mobile App
        );

<span data-ttu-id="bf023-283">您可以透過下列連結，閱讀有關安裝新的 SDK 以及使用新結構的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="bf023-283">You can read about installing the new SDKs and using the new structure via the links below:</span></span>

* [<span data-ttu-id="bf023-284">iOS 3.0.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="bf023-284">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="bf023-285">.NET (Windows/Xamarin) 2.0.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="bf023-285">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<span data-ttu-id="bf023-286">如果您的應用程式會使用推播通知，請記下每個平台特定的註冊指示，因為也已有一些變更。</span><span class="sxs-lookup"><span data-stu-id="bf023-286">If your application makes use of push notifications, make note of the specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="bf023-287">當您準備好新的用戶端版本時，請嘗試對已升級的伺服器專案執行該版本。</span><span class="sxs-lookup"><span data-stu-id="bf023-287">When you have the new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="bf023-288">驗證它的運作方式之後，您就能將新版的應用程式發行給客戶。</span><span class="sxs-lookup"><span data-stu-id="bf023-288">After validating that it works, you can release a new version of your application to customers.</span></span> <span data-ttu-id="bf023-289">最後，在您的客戶有機會接收這些更新後，您就能刪除應用程式的行動服務版本。</span><span class="sxs-lookup"><span data-stu-id="bf023-289">Eventually, once your customers have had a chance to receive these updates, you can delete the Mobile Services version of your app.</span></span> <span data-ttu-id="bf023-290">現在，您已使用最新的 Mobile Apps 伺服器 SDK 完全升級為 App Service 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf023-290">At this point, you have completely upgraded to an App Service Mobile App using the latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

<span data-ttu-id="bf023-291">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="bf023-291">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="bf023-292">[Azure 傳統入口網站]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="bf023-292">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="bf023-293">[何謂 Mobile Apps？]: app-service-mobile-value-prop.md</span><span class="sxs-lookup"><span data-stu-id="bf023-293">[What are Mobile Apps?]: app-service-mobile-value-prop.md</span></span>
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
<span data-ttu-id="bf023-294">[行動應用程式伺服器 SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server</span><span class="sxs-lookup"><span data-stu-id="bf023-294">[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server</span></span>
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications to your mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication to your mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
<span data-ttu-id="bf023-295">[Azure 排程器]: /en-us/documentation/services/scheduler/</span><span class="sxs-lookup"><span data-stu-id="bf023-295">[Azure Scheduler]: /en-us/documentation/services/scheduler/</span></span>
<span data-ttu-id="bf023-296">[Web 工作]: ../app-service-web/websites-webjobs-resources.md</span><span class="sxs-lookup"><span data-stu-id="bf023-296">[Web Job]: ../app-service-web/websites-webjobs-resources.md</span></span>
<span data-ttu-id="bf023-297">[如何使用 .NET 伺服器 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="bf023-297">[How to use the .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
[Migrate from Mobile Services to an App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service to App Service]: app-service-mobile-migrating-from-mobile-services.md
<span data-ttu-id="bf023-298">[App Service 定價]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span><span class="sxs-lookup"><span data-stu-id="bf023-298">[App Service pricing]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span></span>
<span data-ttu-id="bf023-299">[.NET 伺服器 SDK 概觀]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="bf023-299">[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
