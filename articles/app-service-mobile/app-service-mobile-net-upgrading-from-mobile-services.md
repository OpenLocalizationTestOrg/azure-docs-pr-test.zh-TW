---
title: "aaaUpgrade 從行動服務 tooAzure 應用程式服務"
description: "了解如何 tooeasily 升級您的行動服務應用程式 tooan App Service 行動應用程式"
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
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a><span data-ttu-id="240fd-103">升級您現有的.NET 的 Azure 行動服務 tooApp 服務</span><span class="sxs-lookup"><span data-stu-id="240fd-103">Upgrade your existing .NET Azure Mobile Service tooApp Service</span></span>
<span data-ttu-id="240fd-104">App Service Mobile 是新的方式 toobuild 行動應用程式使用 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="240fd-104">App Service Mobile is a new way toobuild mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="240fd-105">詳細資訊，請參閱 toolearn[行動應用程式是什麼？]。</span><span class="sxs-lookup"><span data-stu-id="240fd-105">toolearn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="240fd-106">本主題描述如何 tooupgrade 現有的.NET 後端應用程式從 Azure Mobile Services tooa 新應用程式服務的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="240fd-106">This topic describes how tooupgrade an existing .NET backend application from Azure Mobile Services tooa new App Service Mobile Apps.</span></span> <span data-ttu-id="240fd-107">當您執行此升級時，現有的行動服務應用程式可以繼續 toooperate。</span><span class="sxs-lookup"><span data-stu-id="240fd-107">While you perform this upgrade, your existing Mobile Services application can continue toooperate.</span></span>   <span data-ttu-id="240fd-108">如果您需要 tooupgrade Node.js 後端應用程式，請參閱太[升級您的 Node.js 行動服務](app-service-mobile-node-backend-upgrading-from-mobile-services.md)。</span><span class="sxs-lookup"><span data-stu-id="240fd-108">If you need tooupgrade a Node.js backend application, refer too[Upgrading your Node.js Mobile Services](app-service-mobile-node-backend-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="240fd-109">升級的 tooAzure App Service 行動後端時，它有 App Service 功能且計費太根據存取 tooall[應用程式服務定價]、 定價不行動服務。</span><span class="sxs-lookup"><span data-stu-id="240fd-109">When a mobile backend is upgraded tooAzure App Service, it has access tooall App Service features and are billed according too[App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="240fd-110">移轉與升級</span><span class="sxs-lookup"><span data-stu-id="240fd-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="240fd-111">建議您在升級之前，先 [執行移轉](app-service-mobile-migrating-from-mobile-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="240fd-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="240fd-112">如此一來，您可以將您的應用程式的兩個版本上 hello 相同 App Service 方案，並會產生任何額外的成本。</span><span class="sxs-lookup"><span data-stu-id="240fd-112">This way, you can put both versions of your application on hello same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a><span data-ttu-id="240fd-113">Mobile Apps .NET 伺服器 SDK 中的增強功能</span><span class="sxs-lookup"><span data-stu-id="240fd-113">Improvements in Mobile Apps .NET server SDK</span></span>
<span data-ttu-id="240fd-114">升級新 toohello[行動應用程式 SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/)提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="240fd-114">Upgrading toohello new [Mobile Apps SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) provides hello following benefits:</span></span>

* <span data-ttu-id="240fd-115">NuGet 相依性有更多彈性。</span><span class="sxs-lookup"><span data-stu-id="240fd-115">More flexibility on NuGet dependencies.</span></span> <span data-ttu-id="240fd-116">不再裝載環境的 hello 提供它自己版本的 NuGet 封裝，因此您可以使用替代的相容版本。</span><span class="sxs-lookup"><span data-stu-id="240fd-116">hello hosting environment no longer provides its own versions of NuGet packages, so you can use alternative compatible versions.</span></span> <span data-ttu-id="240fd-117">不過，如果有新的重大 bugfixes 或安全性更新 toohello Mobile 伺服器 SDK 的相依性，您必須手動更新您的服務。</span><span class="sxs-lookup"><span data-stu-id="240fd-117">However, if there are new critical bugfixes or security updates toohello Mobile Server SDK or dependencies, you must update your service manually.</span></span>
* <span data-ttu-id="240fd-118">更具彈性的 hello 行動 SDK。</span><span class="sxs-lookup"><span data-stu-id="240fd-118">More flexibility in hello mobile SDK.</span></span> <span data-ttu-id="240fd-119">您可以明確地控制哪些功能，和路由設定，例如驗證時，資料表的 Api，且會 hello 推播註冊端點。</span><span class="sxs-lookup"><span data-stu-id="240fd-119">You can explicitly control which features and routes are set up, such as authentication, table APIs, and hello push registration endpoint.</span></span> <span data-ttu-id="240fd-120">詳細資訊，請參閱 toolearn[如何 toouse hello Azure 行動應用程式的.NET 伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="240fd-120">toolearn more, see [How toouse hello .NET server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>
* <span data-ttu-id="240fd-121">支援其他 ASP.NET 專案類型和路由。</span><span class="sxs-lookup"><span data-stu-id="240fd-121">Support for other ASP.NET project types and routes.</span></span> <span data-ttu-id="240fd-122">您現在可以為您的行動裝置的後端專案裝載 MVC 和 Web API 控制器 hello 相同專案中。</span><span class="sxs-lookup"><span data-stu-id="240fd-122">You can now host MVC and Web API controllers in hello same project as your mobile backend project.</span></span>
* <span data-ttu-id="240fd-123">支援新的應用程式服務驗證功能，可讓您的 web 和行動裝置應用程式之間的 toouse 常見的驗證設定。</span><span class="sxs-lookup"><span data-stu-id="240fd-123">Support for new App Service authentication features, which allow you toouse a common authentication configuration across your web and mobile apps.</span></span>

## <span data-ttu-id="240fd-124"><a name="overview"></a>基本升級概觀</span><span class="sxs-lookup"><span data-stu-id="240fd-124"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="240fd-125">在許多情況下，升級將會做為切換 toohello 新行動裝置應用程式伺服器 SDK，並重新發行到新的行動裝置應用程式執行個體上的程式碼一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="240fd-125">In many cases, upgrading will be as simple as switching toohello new Mobile Apps server SDK and republishing your code onto a new Mobile App instance.</span></span> <span data-ttu-id="240fd-126">但在某些情況下則需要一些額外的設定，例如進階驗證案例和使用排程工作。</span><span class="sxs-lookup"><span data-stu-id="240fd-126">There are, however some scenarios which will require some additional configuration, such as advanced authentication scenarios and working with scheduled jobs.</span></span> <span data-ttu-id="240fd-127">每一種涵蓋 hello 中稍後的章節。</span><span class="sxs-lookup"><span data-stu-id="240fd-127">Each of these is covered in hello later sections.</span></span>

> [!TIP]
> <span data-ttu-id="240fd-128">建議您閱讀，並在開始升級之前完全了解本主題的 hello rest。</span><span class="sxs-lookup"><span data-stu-id="240fd-128">It is advised that you read and understand hello rest of this topic completely before starting an upgrade.</span></span> <span data-ttu-id="240fd-129">請記下您使用的下列任何功能。</span><span class="sxs-lookup"><span data-stu-id="240fd-129">Make note of any features you use which are called out below.</span></span>
>
>

<span data-ttu-id="240fd-130">hello 行動服務用戶端 Sdk 是**不**與新行動裝置應用程式伺服器 hello SDK 相容。</span><span class="sxs-lookup"><span data-stu-id="240fd-130">hello Mobile Services client SDKs are **not** compatible with hello new Mobile Apps server SDK.</span></span> <span data-ttu-id="240fd-131">在順序 tooprovide 服務連續性的應用程式，您不應該發行變更 tooa 站台目前正在服務已發佈的用戶端。</span><span class="sxs-lookup"><span data-stu-id="240fd-131">In order tooprovide continuity of service for your app, you should not publish changes tooa site currently serving published clients.</span></span> <span data-ttu-id="240fd-132">而是應該建立新的行動應用程式做為重複項目。</span><span class="sxs-lookup"><span data-stu-id="240fd-132">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="240fd-133">您可以將此應用程式相同的應用程式服務計劃在 hello tooavoid 產生額外的財務成本。</span><span class="sxs-lookup"><span data-stu-id="240fd-133">You can put this application on hello same App Service plan tooavoid incurring additional financial cost.</span></span>

<span data-ttu-id="240fd-134">您將會讓 hello 應用程式的兩個版本： 一哪些保持 hello 相同，並提供 wild，hello 和 hello 中已發行的應用程式另一個您可以接著升級和目標服務以新的用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="240fd-134">You will then have two versions of hello application: one which stays hello same and serves published apps in hello wild, and hello other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="240fd-135">您可以移動，或您的程式碼測試您的速度，但您應該確定您所做的任何 bug 修正取得套用的 tooboth。</span><span class="sxs-lookup"><span data-stu-id="240fd-135">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied tooboth.</span></span> <span data-ttu-id="240fd-136">在您覺得 hello wild 中的用戶端應用程式所需的數目有更新 toohello 最新版本，如果您想要您可以刪除 hello 原始移轉應用程式。</span><span class="sxs-lookup"><span data-stu-id="240fd-136">Once you feel that a desired number of client apps in hello wild have updated toohello latest version, you can delete hello original migrated app if you desire.</span></span>

<span data-ttu-id="240fd-137">hello 完整大綱 hello 升級程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="240fd-137">hello full outline for hello upgrade process is as follows:</span></span>

1. <span data-ttu-id="240fd-138">建立新的行動 App</span><span class="sxs-lookup"><span data-stu-id="240fd-138">Create a new Mobile App</span></span>
2. <span data-ttu-id="240fd-139">更新 hello 專案 toouse hello 新伺服器 Sdk</span><span class="sxs-lookup"><span data-stu-id="240fd-139">Update hello project toouse hello new Server SDKs</span></span>
3. <span data-ttu-id="240fd-140">發行新版的用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="240fd-140">Release a new version of your client application</span></span>
4. <span data-ttu-id="240fd-141">(選擇性) 刪除原始已移轉的執行個體</span><span class="sxs-lookup"><span data-stu-id="240fd-141">(Optional) Delete your original migrated instance</span></span>

## <span data-ttu-id="240fd-142"><a name="mobile-app-version"></a>建立第二個應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="240fd-142"><a name="mobile-app-version"></a>Creating a second application instance</span></span>
<span data-ttu-id="240fd-143">hello 升級的第一個步驟是應用的將主控新版本程式中的 hello toocreate hello 行動裝置應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="240fd-143">hello first step in upgrading is toocreate hello Mobile App resource which will host hello new version of your application.</span></span> <span data-ttu-id="240fd-144">如果您已移轉現有的行動服務，您會想 toocreate hello 上的這個版本相同的主控方案。</span><span class="sxs-lookup"><span data-stu-id="240fd-144">If you have already migrated an existing mobile service, you will want toocreate this version on hello same hosting plan.</span></span> <span data-ttu-id="240fd-145">開啟 hello [Azure 入口網站]並瀏覽 tooyour 移轉應用程式。</span><span class="sxs-lookup"><span data-stu-id="240fd-145">Open hello [Azure portal] and navigate tooyour migrated application.</span></span> <span data-ttu-id="240fd-146">記下 hello App Service 方案上執行。</span><span class="sxs-lookup"><span data-stu-id="240fd-146">Make note of hello App Service Plan it is running on.</span></span>

<span data-ttu-id="240fd-147">接下來，建立下列 hello hello 第二個應用程式執行個體[.NET 後端建立指示](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app)。</span><span class="sxs-lookup"><span data-stu-id="240fd-147">Next, create hello second application instance by following hello [.NET backend creation instructions](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app).</span></span> <span data-ttu-id="240fd-148">當您的應用程式服務方案或 「 主機計劃 」 選擇提示的 tooselect hello 計劃已移轉的應用程式。</span><span class="sxs-lookup"><span data-stu-id="240fd-148">When prompted tooselect you App Service Plan or "hosting plan" choose hello plan of your migrated application.</span></span>

<span data-ttu-id="240fd-149">您可能會想 toouse hello 相同的資料庫與通知中樞為您未在行動服務中。</span><span class="sxs-lookup"><span data-stu-id="240fd-149">You will likely want toouse hello same database and Notification Hub as you did in Mobile Services.</span></span> <span data-ttu-id="240fd-150">您可以複製這些值開啟[Azure 入口網站]巡覽 toohello 原始應用程式，然後按一下**設定** > **應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="240fd-150">You can copy these values by opening [Azure portal] and navigating toohello original application, then click **Settings** > **Application settings**.</span></span> <span data-ttu-id="240fd-151">在 [連接字串] 下，複製 `MS_NotificationHubConnectionString` 和 `MS_TableConnectionString`。</span><span class="sxs-lookup"><span data-stu-id="240fd-151">Under **Connection Strings**, copy `MS_NotificationHubConnectionString` and `MS_TableConnectionString`.</span></span> <span data-ttu-id="240fd-152">瀏覽 tooyour 新升級的站台，然後將它們貼在中，覆寫任何現有的值。</span><span class="sxs-lookup"><span data-stu-id="240fd-152">Navigate tooyour new upgrade site and paste them in, overwriting any existing values.</span></span> <span data-ttu-id="240fd-153">針對您的應用程式需要的任何其他應用程式設定重複執行此程序。</span><span class="sxs-lookup"><span data-stu-id="240fd-153">Repeat this process for any other application settings your app needs.</span></span> <span data-ttu-id="240fd-154">如果未使用移轉的服務，您可以將連接字串和應用程式設定讀取 hello**設定**] 索引標籤的 hello 行動服務 > 一節的 hello [Azure 傳統入口網站]。</span><span class="sxs-lookup"><span data-stu-id="240fd-154">If not using a migrated service, you can read connection strings and app settings from hello **Configure** tab of hello Mobile Services section of hello [Azure classic portal].</span></span>

<span data-ttu-id="240fd-155">製作的應用程式的 hello ASP.NET 專案，並將它發行 tooyour 新站台。</span><span class="sxs-lookup"><span data-stu-id="240fd-155">Make a copy of hello ASP.NET project for your application and publish it tooyour new site.</span></span> <span data-ttu-id="240fd-156">使用一份 hello 新的 URL 以更新的用戶端應用程式，驗證確認一切如預期運作。</span><span class="sxs-lookup"><span data-stu-id="240fd-156">Using a copy of your client application updated with hello new URL, validate that everything works as expected.</span></span>

## <a name="updating-hello-server-project"></a><span data-ttu-id="240fd-157">更新 hello 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="240fd-157">Updating hello server project</span></span>
<span data-ttu-id="240fd-158">行動應用程式提供了新[行動應用程式伺服器 SDK]其中提供許多的 hello 與 hello 行動服務執行階段相同的功能。</span><span class="sxs-lookup"><span data-stu-id="240fd-158">Mobile Apps provides a new [Mobile App Server SDK] which provides much of hello same functionality as hello Mobile Services runtime.</span></span> <span data-ttu-id="240fd-159">首先，您應該移除所有參考 toohello 行動服務封裝。</span><span class="sxs-lookup"><span data-stu-id="240fd-159">First, you should remove all references toohello Mobile Services packages.</span></span> <span data-ttu-id="240fd-160">在 [hello NuGet 封裝管理員] 中，搜尋`WindowsAzure.MobileServices.Backend`。</span><span class="sxs-lookup"><span data-stu-id="240fd-160">In hello NuGet package manager, search for `WindowsAzure.MobileServices.Backend`.</span></span> <span data-ttu-id="240fd-161">大部分的 app 將會在此處看見數個封裝，包括 `WindowsAzure.MobileServices.Backend.Tables` 和 `WindowsAzure.MobileServices.Backend.Entity`。</span><span class="sxs-lookup"><span data-stu-id="240fd-161">Most apps will see several packages here, including `WindowsAzure.MobileServices.Backend.Tables` and `WindowsAzure.MobileServices.Backend.Entity`.</span></span> <span data-ttu-id="240fd-162">在這種情況下，啟動與 hello 最低套件 hello 相依性樹狀目錄中，例如`Entity`，並將它移除。</span><span class="sxs-lookup"><span data-stu-id="240fd-162">In such a case, start with hello lowest package in hello dependency tree, such as `Entity`, and remove it.</span></span> <span data-ttu-id="240fd-163">出現提示時，請勿移除所有相依的封裝。</span><span class="sxs-lookup"><span data-stu-id="240fd-163">When prompted, do not remove all dependant packages.</span></span> <span data-ttu-id="240fd-164">重複執行此程序，直到您移除了 `WindowsAzure.MobileServices.Backend` 本身為止。</span><span class="sxs-lookup"><span data-stu-id="240fd-164">Repeat this process until you have removed `WindowsAzure.MobileServices.Backend` itself.</span></span>

<span data-ttu-id="240fd-165">此時，您的專案將不再參考行動服務 SDK。</span><span class="sxs-lookup"><span data-stu-id="240fd-165">At this point you will have a project that no longer references Mobile Services SDKs.</span></span>

<span data-ttu-id="240fd-166">接下來您將會新增參考 hello 行動應用程式 SDK。</span><span class="sxs-lookup"><span data-stu-id="240fd-166">Next you will add references hello Mobile Apps SDK.</span></span> <span data-ttu-id="240fd-167">針對這個升級中，大部分的開發人員會想 toodownload 並安裝 hello`Microsoft.Azure.Mobile.Server.Quickstart`封裝，因為這會在 hello 必要整組中提取。</span><span class="sxs-lookup"><span data-stu-id="240fd-167">For this upgrade, most developers will want toodownload and install hello `Microsoft.Azure.Mobile.Server.Quickstart` package, as this will pull in hello entire required set.</span></span>

<span data-ttu-id="240fd-168">會有極多的編譯器錯誤造成 hello Sdk 之間的差異，但這些是簡單 tooaddress，涵蓋在 hello 本節其餘部分。</span><span class="sxs-lookup"><span data-stu-id="240fd-168">There will be quite a few compiler errors resulting from differences between hello SDKs, but these are easy tooaddress and are covered in hello rest of this section.</span></span>

### <a name="base-configuration"></a><span data-ttu-id="240fd-169">基本組態</span><span class="sxs-lookup"><span data-stu-id="240fd-169">Base configuration</span></span>
<span data-ttu-id="240fd-170">然後，在 WebApiConfig.cs 中，您可以取代：</span><span class="sxs-lookup"><span data-stu-id="240fd-170">Then, in WebApiConfig.cs, you can replace:</span></span>

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

<span data-ttu-id="240fd-171">取代為</span><span class="sxs-lookup"><span data-stu-id="240fd-171">with</span></span>

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> <span data-ttu-id="240fd-172">如果您想要 toolearn 新.NET 伺服器 hello SDK 與 tooadd/移除功能從您的應用程式的方式的詳細資訊，請參閱 hello [toouse 如何 hello.NET 伺服器 SDK]主題。</span><span class="sxs-lookup"><span data-stu-id="240fd-172">If you wish toolearn more about hello new .NET server SDK and how tooadd/remove features from your app, please see hello [How toouse hello .NET server SDK] topic.</span></span>
>
>

<span data-ttu-id="240fd-173">如果您的應用程式會使用 hello 驗證功能，您也需要 tooregister OWIN 中介軟體。</span><span class="sxs-lookup"><span data-stu-id="240fd-173">If your app makes use of hello authentication features, you will also need tooregister an OWIN middleware.</span></span> <span data-ttu-id="240fd-174">在此情況下，您應該將 hello 上述組態程式碼移到新的 OWIN 啟動 「 類別。</span><span class="sxs-lookup"><span data-stu-id="240fd-174">In this case, you should move hello above configuration code into a new OWIN Startup class.</span></span>

1. <span data-ttu-id="240fd-175">將 hello NuGet 套件加入`Microsoft.Owin.Host.SystemWeb`如果它已不包含在專案中。</span><span class="sxs-lookup"><span data-stu-id="240fd-175">Add hello NuGet package `Microsoft.Owin.Host.SystemWeb` if it is not already included in your project.</span></span>
2. <span data-ttu-id="240fd-176">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選取 [新增] -> [新項目]。</span><span class="sxs-lookup"><span data-stu-id="240fd-176">In Visual Studio, right click on your project and select **Add** -> **New Item**.</span></span> <span data-ttu-id="240fd-177">依序選取 [Web] -> [一般] -> [OWIN 啟動類別]。</span><span class="sxs-lookup"><span data-stu-id="240fd-177">Select **Web** -> **General** -> **OWIN Startup class**.</span></span>
3. <span data-ttu-id="240fd-178">移動程式碼上方 hello MobileAppConfiguration 從`WebApiConfig.Register()`toohello`Configuration()`新啟動類別的方法。</span><span class="sxs-lookup"><span data-stu-id="240fd-178">Move hello above code for MobileAppConfiguration from `WebApiConfig.Register()` toohello `Configuration()` method of your new startup class.</span></span>

<span data-ttu-id="240fd-179">請確定 hello`Configuration()`方法的結尾：</span><span class="sxs-lookup"><span data-stu-id="240fd-179">Make sure hello `Configuration()` method ends with:</span></span>

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

<span data-ttu-id="240fd-180">有其他變更的相關的 tooauthentication 涵蓋的 hello 完整驗證一節。</span><span class="sxs-lookup"><span data-stu-id="240fd-180">There are additional changes related tooauthentication which are covered in hello full authentication section below.</span></span>

### <a name="working-with-data"></a><span data-ttu-id="240fd-181">使用資料</span><span class="sxs-lookup"><span data-stu-id="240fd-181">Working with Data</span></span>
<span data-ttu-id="240fd-182">行動服務中 hello 行動裝置應用程式名稱會當作 hello Entity Framework 安裝程式中的 hello 預設結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="240fd-182">In Mobile Services, hello mobile app name served as hello default schema name in hello Entity Framework setup.</span></span>

<span data-ttu-id="240fd-183">您擁有的 tooensure hello 相同結構描述所參考的如往常一般，之後在您的應用程式的 hello DbContext tooset hello 結構描述使用 hello:</span><span class="sxs-lookup"><span data-stu-id="240fd-183">tooensure that you have hello same schema being referenced as before, use hello following tooset hello schema in hello DbContext for your application:</span></span>

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

<span data-ttu-id="240fd-184">請確定您有 MS_MobileServiceName 如果您不要 hello 上述設定。</span><span class="sxs-lookup"><span data-stu-id="240fd-184">Please make sure you have MS_MobileServiceName set if you do hello above.</span></span> <span data-ttu-id="240fd-185">如果您的應用程式先前已自訂這個結構描述，您也可以提供另一個結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="240fd-185">You can also provide another schema name if your application customized this previously.</span></span>

### <a name="system-properties"></a><span data-ttu-id="240fd-186">系統屬性</span><span class="sxs-lookup"><span data-stu-id="240fd-186">System Properties</span></span>
#### <a name="naming"></a><span data-ttu-id="240fd-187">命名</span><span class="sxs-lookup"><span data-stu-id="240fd-187">Naming</span></span>
<span data-ttu-id="240fd-188">在 [hello Azure Mobile Services 伺服器 SDK 系統屬性永遠包含雙底線 (`__`) hello 屬性的前置詞：</span><span class="sxs-lookup"><span data-stu-id="240fd-188">In hello Azure Mobile Services server SDK, system properties always contain a double underscore (`__`) prefix for hello properties:</span></span>

* <span data-ttu-id="240fd-189">__createdAt</span><span class="sxs-lookup"><span data-stu-id="240fd-189">__createdAt</span></span>
* <span data-ttu-id="240fd-190">__updatedAt</span><span class="sxs-lookup"><span data-stu-id="240fd-190">__updatedAt</span></span>
* <span data-ttu-id="240fd-191">__deleted</span><span class="sxs-lookup"><span data-stu-id="240fd-191">__deleted</span></span>
* <span data-ttu-id="240fd-192">__version</span><span class="sxs-lookup"><span data-stu-id="240fd-192">__version</span></span>

<span data-ttu-id="240fd-193">hello 行動服務用戶端 Sdk 有特殊邏輯，來剖析下列格式的系統屬性。</span><span class="sxs-lookup"><span data-stu-id="240fd-193">hello Mobile Services client SDKs have special logic for parsing system properties in this format.</span></span>

<span data-ttu-id="240fd-194">Azure 行動應用程式，在系統內容不會再有特殊格式，並具有下列名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="240fd-194">In Azure Mobile Apps, system properties no longer have a special format and have hello following names:</span></span>

* <span data-ttu-id="240fd-195">建立時間</span><span class="sxs-lookup"><span data-stu-id="240fd-195">createdAt</span></span>
* <span data-ttu-id="240fd-196">更新時間</span><span class="sxs-lookup"><span data-stu-id="240fd-196">updatedAt</span></span>
* <span data-ttu-id="240fd-197">已刪除</span><span class="sxs-lookup"><span data-stu-id="240fd-197">deleted</span></span>
* <span data-ttu-id="240fd-198">版本</span><span class="sxs-lookup"><span data-stu-id="240fd-198">version</span></span>

<span data-ttu-id="240fd-199">hello 行動應用程式用戶端 Sdk 使用 hello 新系統屬性的名稱，因此不必變更需要 tooclient 程式碼。</span><span class="sxs-lookup"><span data-stu-id="240fd-199">hello Mobile Apps client SDKs use hello new system properties names, so no changes are required tooclient code.</span></span> <span data-ttu-id="240fd-200">不過，如果您直接進行 REST 呼叫 tooyour 服務，則您應該據以變更您的查詢。</span><span class="sxs-lookup"><span data-stu-id="240fd-200">However, if you are directly making REST calls tooyour service then you should change your queries accordingly.</span></span>

#### <a name="local-store"></a><span data-ttu-id="240fd-201">本機存放區</span><span class="sxs-lookup"><span data-stu-id="240fd-201">Local store</span></span>
<span data-ttu-id="240fd-202">系統屬性 hello 變更 toohello 名稱表示行動服務的離線同步處理本機資料庫不是與行動應用程式相容。</span><span class="sxs-lookup"><span data-stu-id="240fd-202">hello changes toohello names of system properties mean that an offline sync local database for Mobile Services is not compatible with Mobile Apps.</span></span> <span data-ttu-id="240fd-203">可能的話，您應該避免從應用程式直到之後暫止的變更尚未傳送 toohello server 的行動服務 tooMobile 升級用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="240fd-203">If possible, you should avoid upgrading client apps from Mobile Services tooMobile Apps until after pending changes have been sent toohello server.</span></span> <span data-ttu-id="240fd-204">然後，hello 升級應用程式應該使用新的資料庫檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="240fd-204">Then, hello upgraded app should use a new database filename.</span></span>

<span data-ttu-id="240fd-205">如果有暫止的離線變更 hello 作業佇列中時，用戶端應用程式已升級從行動服務 tooMobile 應用程式，則 hello 系統資料庫必須是更新的 toouse hello 新資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="240fd-205">If a client app is upgraded from Mobile Services tooMobile Apps while there are pending offline changes in hello operation queue, then hello system database must be updated toouse hello new column names.</span></span> <span data-ttu-id="240fd-206">在 iOS 上，這可以使用輕量型移轉 toochange hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="240fd-206">On iOS, this can be achieved using lightweight migrations toochange hello column names.</span></span> <span data-ttu-id="240fd-207">Android 和 hello.NET 受管理用戶端上，您應該撰寫自訂的 SQL toorename hello 資料行的資料物件資料表。</span><span class="sxs-lookup"><span data-stu-id="240fd-207">On Android and hello .NET managed client, you should write custom SQL toorename hello columns for your data object tables.</span></span>

<span data-ttu-id="240fd-208">在 iOS 上，您可以變更您的核心資料結構描述資料實體 toomatch hello 下列。</span><span class="sxs-lookup"><span data-stu-id="240fd-208">On iOS, you should change your Core Data schema for your data entities toomatch hello following.</span></span> <span data-ttu-id="240fd-209">請注意，hello 屬性`createdAt`，`updatedAt`和`version`不再有`ms_`前置詞：</span><span class="sxs-lookup"><span data-stu-id="240fd-209">Note that hello properties `createdAt`, `updatedAt` and `version` no longer have an `ms_` prefix:</span></span>

| <span data-ttu-id="240fd-210">屬性</span><span class="sxs-lookup"><span data-stu-id="240fd-210">Attribute</span></span> | <span data-ttu-id="240fd-211">類型</span><span class="sxs-lookup"><span data-stu-id="240fd-211">Type</span></span> | <span data-ttu-id="240fd-212">注意</span><span class="sxs-lookup"><span data-stu-id="240fd-212">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="240fd-213">id</span><span class="sxs-lookup"><span data-stu-id="240fd-213">id</span></span> |<span data-ttu-id="240fd-214">字串 (標示為必要)</span><span class="sxs-lookup"><span data-stu-id="240fd-214">String, marked required</span></span> |<span data-ttu-id="240fd-215">遠端存放區中的主索引鍵</span><span class="sxs-lookup"><span data-stu-id="240fd-215">primary key in remote store</span></span> |
| <span data-ttu-id="240fd-216">建立時間</span><span class="sxs-lookup"><span data-stu-id="240fd-216">createdAt</span></span> |<span data-ttu-id="240fd-217">Date</span><span class="sxs-lookup"><span data-stu-id="240fd-217">Date</span></span> |<span data-ttu-id="240fd-218">（選擇性） 對應 toocreatedAt 系統屬性</span><span class="sxs-lookup"><span data-stu-id="240fd-218">(optional) maps toocreatedAt system property</span></span> |
| <span data-ttu-id="240fd-219">更新時間</span><span class="sxs-lookup"><span data-stu-id="240fd-219">updatedAt</span></span> |<span data-ttu-id="240fd-220">Date</span><span class="sxs-lookup"><span data-stu-id="240fd-220">Date</span></span> |<span data-ttu-id="240fd-221">（選擇性） 對應 tooupdatedAt 系統屬性</span><span class="sxs-lookup"><span data-stu-id="240fd-221">(optional) maps tooupdatedAt system property</span></span> |
| <span data-ttu-id="240fd-222">版本</span><span class="sxs-lookup"><span data-stu-id="240fd-222">version</span></span> |<span data-ttu-id="240fd-223">String</span><span class="sxs-lookup"><span data-stu-id="240fd-223">String</span></span> |<span data-ttu-id="240fd-224">（選擇性） 使用的 toodetect 衝突，對應 tooversion</span><span class="sxs-lookup"><span data-stu-id="240fd-224">(optional) used toodetect conflicts, maps tooversion</span></span> |

#### <a name="querying-system-properties"></a><span data-ttu-id="240fd-225">查詢系統屬性</span><span class="sxs-lookup"><span data-stu-id="240fd-225">Querying system properties</span></span>
<span data-ttu-id="240fd-226">在 Azure Mobile Services 中，系統屬性不會傳送預設情況下，但要求使用 hello 查詢字串時，只`__systemProperties`。</span><span class="sxs-lookup"><span data-stu-id="240fd-226">In Azure Mobile Services, system properties are not sent by default, but only when they are requested using hello query string `__systemProperties`.</span></span> <span data-ttu-id="240fd-227">相反地，在 Azure 行動應用程式系統屬性是**一律選取**因為它們是 hello 伺服器 SDK 物件模型的一部分。</span><span class="sxs-lookup"><span data-stu-id="240fd-227">In contrast, in Azure Mobile Apps system properties are **always selected** since they are part of hello server SDK object model.</span></span>

<span data-ttu-id="240fd-228">這項變更主要會影響網域管理員的自訂實作，例如 `MappedEntityDomainManager`的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="240fd-228">This change mainly impacts custom implementations of domain managers, such as extensions of `MappedEntityDomainManager`.</span></span> <span data-ttu-id="240fd-229">在行動服務，如果用戶端永遠不會要求任何系統屬性，就可能 toouse`MappedEntityDomainManager`實際上未對應的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="240fd-229">In Mobile Services, if a client never requests any system properties, it is possible toouse a `MappedEntityDomainManager` that does not actually map all properties.</span></span> <span data-ttu-id="240fd-230">不過，在 Azure Mobile Apps 中，這些未對應的屬性將導致 GET 查詢發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="240fd-230">However, in Azure Mobile Apps, these unmapped properties will cause an error in GET queries.</span></span>

<span data-ttu-id="240fd-231">hello 最簡單的方式 tooresolve hello 問題，使其繼承從是 toomodify 您 DTOs`ITableData`而不是`EntityData`。</span><span class="sxs-lookup"><span data-stu-id="240fd-231">hello easiest way tooresolve hello issue is toomodify your DTOs so that they inherit from `ITableData` instead of `EntityData`.</span></span> <span data-ttu-id="240fd-232">接著，新增 hello`[NotMapped]`屬性應省略 toohello 欄位。</span><span class="sxs-lookup"><span data-stu-id="240fd-232">Then, add hello `[NotMapped]` attribute toohello fields that should be omitted.</span></span>

<span data-ttu-id="240fd-233">例如，下列 hello 定義`TodoItem`與任何系統屬性：</span><span class="sxs-lookup"><span data-stu-id="240fd-233">For example, hello following defines `TodoItem` with no system properties:</span></span>

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

<span data-ttu-id="240fd-234">注意： 如果您收到錯誤訊息`NotMapped`，加入組件參考 toohello `System.ComponentModel.DataAnnotations`。</span><span class="sxs-lookup"><span data-stu-id="240fd-234">Note: if you get errors on `NotMapped`, add a reference toohello assembly `System.ComponentModel.DataAnnotations`.</span></span>

### <a name="cors"></a><span data-ttu-id="240fd-235">CORS</span><span class="sxs-lookup"><span data-stu-id="240fd-235">CORS</span></span>
<span data-ttu-id="240fd-236">行動服務藉由包裝 hello ASP.NET CORS 方案包含一些適用於 CORS 支援。</span><span class="sxs-lookup"><span data-stu-id="240fd-236">Mobile Services included some support for CORS by wrapping hello ASP.NET CORS solution.</span></span> <span data-ttu-id="240fd-237">此文繞圖圖層移除的 toogive hello 開發人員已更大的控制權，因此您可以直接利用[ASP.NET CORS 支援](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)。</span><span class="sxs-lookup"><span data-stu-id="240fd-237">This wrapping layer has been removed toogive hello developer more control, so you can directly leverage [ASP.NET CORS support](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

<span data-ttu-id="240fd-238">hello 的問題，如果使用 CORS 的主要區域是該 hello`eTag`和`Location`標頭必須允許 hello 用戶端 Sdk toowork 順序正確。</span><span class="sxs-lookup"><span data-stu-id="240fd-238">hello main areas of concern if using CORS are that hello `eTag` and `Location` headers must be allowed in order for hello client SDKs toowork properly.</span></span>

### <a name="push-notifications"></a><span data-ttu-id="240fd-239">推播通知</span><span class="sxs-lookup"><span data-stu-id="240fd-239">Push Notifications</span></span>
<span data-ttu-id="240fd-240">推入，您可能會發現遺漏 hello Server SDK hello 主要項目是 hello PushRegistrationHandler 類別。</span><span class="sxs-lookup"><span data-stu-id="240fd-240">For push, hello main item that you may find missing from hello Server SDK is hello PushRegistrationHandler class.</span></span> <span data-ttu-id="240fd-241">註冊在行動應用程式中處理方式稍有不同，依預設會啟用不具標籤的註冊。</span><span class="sxs-lookup"><span data-stu-id="240fd-241">Registrations are handled slightly differently in Mobile Apps, and tagless registrations are enabled by default.</span></span> <span data-ttu-id="240fd-242">管理標籤可使用自訂 API 來完成。</span><span class="sxs-lookup"><span data-stu-id="240fd-242">Managing tags may be accomplished by using custom APIs.</span></span> <span data-ttu-id="240fd-243">請參閱 hello[標記註冊](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags)如需詳細資訊的指示。</span><span class="sxs-lookup"><span data-stu-id="240fd-243">Please see hello [registering for tags](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instructions for more information.</span></span>

### <a name="scheduled-jobs"></a><span data-ttu-id="240fd-244">排程的工作</span><span class="sxs-lookup"><span data-stu-id="240fd-244">Scheduled Jobs</span></span>
<span data-ttu-id="240fd-245">排程的工作不建行動裝置應用程式，因此您在.NET 後端中有任何現有的作業將需要 toobe 個別升級。</span><span class="sxs-lookup"><span data-stu-id="240fd-245">Scheduled jobs are not built into Mobile Apps, so any existing jobs that you have in your .NET backend will need toobe upgraded individually.</span></span> <span data-ttu-id="240fd-246">其中一個選項是排程的 toocreate [Web 工作]hello 行動裝置應用程式程式碼的站台上。</span><span class="sxs-lookup"><span data-stu-id="240fd-246">One option is toocreate a scheduled [Web Job] on hello Mobile App code site.</span></span> <span data-ttu-id="240fd-247">您無法同時設定了控制器保存您的作業程式碼，並設定 hello [Azure 排程器]toohit hello 預期排程該端點。</span><span class="sxs-lookup"><span data-stu-id="240fd-247">You could also set up a controller that holds your job code and configure hello [Azure Scheduler] toohit that endpoint on hello expected schedule.</span></span>

### <a name="miscellaneous-changes"></a><span data-ttu-id="240fd-248">其他變更</span><span class="sxs-lookup"><span data-stu-id="240fd-248">Miscellaneous changes</span></span>
<span data-ttu-id="240fd-249">這會由行動用戶端的所有 ApiControllers 現在必須都具有 hello`[MobileAppController]`屬性。</span><span class="sxs-lookup"><span data-stu-id="240fd-249">All ApiControllers which will be consumed by a mobile client must now have hello `[MobileAppController]` attribute.</span></span> <span data-ttu-id="240fd-250">這已不再包含根據預設，讓其他不受影響的 ApiControllers toogo hello 行動格式器。</span><span class="sxs-lookup"><span data-stu-id="240fd-250">This is no longer included by default so that other ApiControllers toogo unaffected by hello mobile formatters.</span></span>

<span data-ttu-id="240fd-251">hello`ApiServices`物件不再是 hello SDK 的一部分。</span><span class="sxs-lookup"><span data-stu-id="240fd-251">hello `ApiServices` object is no longer part of hello SDK.</span></span> <span data-ttu-id="240fd-252">tooaccess 行動裝置應用程式設定，您可以使用下列 hello:</span><span class="sxs-lookup"><span data-stu-id="240fd-252">tooaccess Mobile App settings, you can use hello following:</span></span>

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

<span data-ttu-id="240fd-253">同樣地，記錄現在即可完成使用標準 ASP.NET 追蹤寫入 hello:</span><span class="sxs-lookup"><span data-stu-id="240fd-253">Similarly, logging is now accomplished using hello standard ASP.NET trace writing:</span></span>

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <span data-ttu-id="240fd-254"><a name="authentication"></a>驗證考量</span><span class="sxs-lookup"><span data-stu-id="240fd-254"><a name="authentication"></a>Authentication considerations</span></span>
<span data-ttu-id="240fd-255">行動服務的 hello 驗證元件現在已移到 hello 應用程式服務驗證和授權功能。</span><span class="sxs-lookup"><span data-stu-id="240fd-255">hello authentication components of Mobile Services have now been moved into hello App Service Authentication/Authorization feature.</span></span> <span data-ttu-id="240fd-256">您可以了解啟用此站台所讀取的 hello[新增驗證 tooyour 行動裝置應用程式](app-service-mobile-ios-get-started-users.md)主題。</span><span class="sxs-lookup"><span data-stu-id="240fd-256">You can learn about enabling this for your site by reading hello [Add authentication tooyour mobile app](app-service-mobile-ios-get-started-users.md) topic.</span></span>

<span data-ttu-id="240fd-257">對於某些提供者，例如 AAD、 Facebook 和 Google，您應該能夠 tooleverage hello 現有註冊從您複製的應用程式。</span><span class="sxs-lookup"><span data-stu-id="240fd-257">For some providers, such as AAD, Facebook, and Google, you should be able tooleverage hello existing registration from your copy application.</span></span> <span data-ttu-id="240fd-258">您只需要 toonavigate toohello 身分識別提供者的入口網站，並加入新的重新導向 URL toohello 註冊。</span><span class="sxs-lookup"><span data-stu-id="240fd-258">You simply need toonavigate toohello identity provider's portal and add a new redirect URL toohello registration.</span></span> <span data-ttu-id="240fd-259">接著設定應用程式服務驗證/授權與 hello 用戶端識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="240fd-259">Then configure App Service Authentication/Authorization with hello client ID and secret.</span></span>

### <a name="controller-action-authorization"></a><span data-ttu-id="240fd-260">控制器動作授權</span><span class="sxs-lookup"><span data-stu-id="240fd-260">Controller action authorization</span></span>
<span data-ttu-id="240fd-261">任何執行個體的 hello`[AuthorizeLevel(AuthorizationLevel.User)]`屬性現在必須變更的 toouse hello 標準 ASP.NET`[Authorize]`屬性。</span><span class="sxs-lookup"><span data-stu-id="240fd-261">Any instances of hello `[AuthorizeLevel(AuthorizationLevel.User)]` attribute must now be changed toouse hello standard ASP.NET `[Authorize]` attribute.</span></span> <span data-ttu-id="240fd-262">此外，根據預設，控制器現在是匿名的，就如同在其他 ASP.NET 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="240fd-262">Additionally, controllers are now Anonymous by default, as in other ASP.NET applications.</span></span>
<span data-ttu-id="240fd-263">如果您使用其中一個 hello 其他 AuthorizeLevel 選項，例如系統管理員或應用程式，請注意，這些是消失。</span><span class="sxs-lookup"><span data-stu-id="240fd-263">If you were using one of hello other AuthorizeLevel options, such as Admin or Application, please note that these are gone.</span></span> <span data-ttu-id="240fd-264">相反地，您可以為共用密碼設定 AuthorizationFilters 或安全地設定 AAD 服務主體 tooenable 服務對服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="240fd-264">You can instead set up AuthorizationFilters for shared secrets or configure an AAD Service Principal tooenable service-to-service calls securely.</span></span>

### <a name="getting-additional-user-information"></a><span data-ttu-id="240fd-265">取得其他使用者資訊</span><span class="sxs-lookup"><span data-stu-id="240fd-265">Getting additional user information</span></span>
<span data-ttu-id="240fd-266">您可以取得額外的使用者資訊，包括存取權杖透過 hello`GetAppServiceIdentityAsync()`方法：</span><span class="sxs-lookup"><span data-stu-id="240fd-266">You can get additional user information, including access tokens through hello `GetAppServiceIdentityAsync()` method:</span></span>

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

<span data-ttu-id="240fd-267">此外，如果您的應用程式使用者識別碼上, 使用相依性，例如將它們儲存在資料庫中，務必 hello 行動服務與應用程式服務的行動應用程式之間的使用者識別碼的 toonote 會不同。</span><span class="sxs-lookup"><span data-stu-id="240fd-267">Additionally, if your application takes dependencies on user IDs, such as storing them in a database, it is important toonote that hello user IDs between Mobile Services and App Service Mobile Apps are different.</span></span> <span data-ttu-id="240fd-268">您還可以透過取得 hello 行動服務使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="240fd-268">You can still get hello Mobile Services User ID, though.</span></span> <span data-ttu-id="240fd-269">Hello ProviderCredentials 子類別的所有有使用者識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="240fd-269">All of hello ProviderCredentials subclasses have a UserId property.</span></span> <span data-ttu-id="240fd-270">因此從 hello 範例，然後再繼續：</span><span class="sxs-lookup"><span data-stu-id="240fd-270">So continuing from hello example before:</span></span>

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

<span data-ttu-id="240fd-271">如果您的應用程式採用任何相依項目上的使用者 Id，很重要，運用盡可能 hello 與身分識別提供者相同的登錄。</span><span class="sxs-lookup"><span data-stu-id="240fd-271">If your app does take any dependencies on user IDs, it is important that you leverage hello same registration with an identity provider if possible.</span></span> <span data-ttu-id="240fd-272">使用者識別碼會是通常已設定領域的 toohello 應用程式登錄，因此導入新的註冊，則可以建立比對使用者 tootheir 資料的問題。</span><span class="sxs-lookup"><span data-stu-id="240fd-272">User IDs are typically scoped toohello application registration that was used, so introducing a new registration could create problems with matching users tootheir data.</span></span>

### <a name="custom-authentication"></a><span data-ttu-id="240fd-273">自訂驗證</span><span class="sxs-lookup"><span data-stu-id="240fd-273">Custom authentication</span></span>
<span data-ttu-id="240fd-274">如果您的應用程式使用的自訂驗證解決方案，您會想 toomake 確定該 hello 升級站台具有存取 toohello 系統。</span><span class="sxs-lookup"><span data-stu-id="240fd-274">If your app is using a custom authentication solution, you will want toomake sure that hello upgraded site has access toohello system.</span></span> <span data-ttu-id="240fd-275">遵循 hello 新的自訂驗證 hello [.NET 伺服器 SDK 概觀]toointegrate 您的方案。</span><span class="sxs-lookup"><span data-stu-id="240fd-275">Follow hello new instructions for custom authentication in hello [.NET server SDK overview] toointegrate your solution.</span></span> <span data-ttu-id="240fd-276">請注意，hello 自訂驗證元件仍在預覽中。</span><span class="sxs-lookup"><span data-stu-id="240fd-276">Please note that hello custom authentication components are still in preview.</span></span>

## <span data-ttu-id="240fd-277"><a name="updating-clients"></a>更新用戶端</span><span class="sxs-lookup"><span data-stu-id="240fd-277"><a name="updating-clients"></a>Updating clients</span></span>
<span data-ttu-id="240fd-278">在您擁有可運作的行動 App 後端之後，就能在取用它的新版用戶端應用程式上運作。</span><span class="sxs-lookup"><span data-stu-id="240fd-278">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="240fd-279">行動應用程式也包含新版 hello client Sdk，以及類似的 toohello server 升級上方，您將需要的 tooremove toohello 行動服務 Sdk 之前的所有參照安裝 hello 行動應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="240fd-279">Mobile Apps also includes a new version of hello client SDKs, and similar toohello server upgrade above, you will need tooremove all references toohello Mobile Services SDKs before installing hello Mobile Apps versions.</span></span>

<span data-ttu-id="240fd-280">其中一個 hello hello 版本之間的主要變更是 hello 建構函式不再需要應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="240fd-280">One of hello main changes between hello versions is that hello constructors no longer require an application key.</span></span> <span data-ttu-id="240fd-281">您現在只需傳入 hello 行動應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="240fd-281">You now simply pass in hello URL of your Mobile App.</span></span> <span data-ttu-id="240fd-282">例如，在 hello.NET 用戶端，hello`MobileServiceClient`建構函式現在是：</span><span class="sxs-lookup"><span data-stu-id="240fd-282">For example, on hello .NET clients, hello `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

<span data-ttu-id="240fd-283">您可以閱讀安裝 hello 新 Sdk，並使用 hello 透過以下的 hello 連結新的結構：</span><span class="sxs-lookup"><span data-stu-id="240fd-283">You can read about installing hello new SDKs and using hello new structure via hello links below:</span></span>

* [<span data-ttu-id="240fd-284">iOS 3.0.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="240fd-284">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="240fd-285">.NET (Windows/Xamarin) 2.0.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="240fd-285">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<span data-ttu-id="240fd-286">如果您的應用程式更能使用推播通知，請記下 hello 特定註冊指示每個平台，已有一些變更有以及。</span><span class="sxs-lookup"><span data-stu-id="240fd-286">If your application makes use of push notifications, make note of hello specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="240fd-287">當您擁有 hello 新用戶端版本準備好時，現在就試試看對您已升級的伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="240fd-287">When you have hello new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="240fd-288">驗證它運作之後，您可以釋放您的應用程式 toocustomers 的新版本。</span><span class="sxs-lookup"><span data-stu-id="240fd-288">After validating that it works, you can release a new version of your application toocustomers.</span></span> <span data-ttu-id="240fd-289">最後，一旦您的客戶有機會 tooreceive 這些更新，您可以刪除 hello 行動服務應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="240fd-289">Eventually, once your customers have had a chance tooreceive these updates, you can delete hello Mobile Services version of your app.</span></span> <span data-ttu-id="240fd-290">此時，您完全升級 tooan App Service 行動應用程式使用最新版行動應用程式伺服器 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="240fd-290">At this point, you have completely upgraded tooan App Service Mobile App using hello latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

[Azure 入口網站]: https://portal.azure.com/
[Azure 傳統入口網站]: https://manage.windowsazure.com/
[什麼是 Mobile Apps？]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[行動應用程式伺服器 SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure 排程器]: /en-us/documentation/services/scheduler/
[Web 工作]: ../app-service-web/websites-webjobs-resources.md
[如何 toouse hello.NET 伺服器 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[App Service 價格]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET 伺服器 SDK 概觀]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
