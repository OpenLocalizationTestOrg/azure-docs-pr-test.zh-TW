---
title: "aaaSeparating 遙測從開發、 測試和發行 Azure Application Insights |Microsoft 文件"
description: "開發、 測試和生產戳記直接遙測 toodifferent 資源。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="540e2-103">區分開發、測試及生產環境的遙測</span><span class="sxs-lookup"><span data-stu-id="540e2-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="540e2-104">當您開發 hello 下一版的 web 應用程式時，您不想註冊 hello toomix [Application Insights](app-insights-overview.md) hello 新的版本與 hello 已發行版本的遙測。</span><span class="sxs-lookup"><span data-stu-id="540e2-104">When you are developing hello next version of a web application, you don't want toomix up hello [Application Insights](app-insights-overview.md) telemetry from hello new version and hello already released version.</span></span> <span data-ttu-id="540e2-105">tooavoid 混淆的可能性，傳送嗨遙測，從不同的開發階段 tooseparate Application Insights 資源，使用個別的檢測金鑰 (ikeys)。</span><span class="sxs-lookup"><span data-stu-id="540e2-105">tooavoid confusion, send hello telemetry from different development stages tooseparate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="540e2-106">toomake 它更容易 toochange hello 檢測金鑰為版本從移動一個階段 tooanother 可能很有用的 tooset hello ikey hello 組態檔案中的程式碼而不是。</span><span class="sxs-lookup"><span data-stu-id="540e2-106">toomake it easier toochange hello instrumentation key as a version moves from one stage tooanother, it can be useful tooset hello ikey in code instead of in hello configuration file.</span></span> 

<span data-ttu-id="540e2-107">(如果您的系統是「Azure 雲端服務」，有[另一個設定個別 ikey 的方法](app-insights-cloudservices.md))。</span><span class="sxs-lookup"><span data-stu-id="540e2-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="540e2-108">關於資源和檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="540e2-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="540e2-109">在為 Web 應用程式設定 Application Insights 監視時，您會在 Microsoft Azure 中建立 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="540e2-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="540e2-110">您在 hello 順序 toosee 在 Azure 入口網站中開啟此資源，並分析 hello 遙測收集從您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="540e2-110">You open this resource in hello Azure portal in order toosee and analyze hello telemetry collected from your app.</span></span> <span data-ttu-id="540e2-111">hello 資源由*檢測金鑰*(ikey)。</span><span class="sxs-lookup"><span data-stu-id="540e2-111">hello resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="540e2-112">當您安裝 hello Application Insights 封裝 toomonitor 應用程式，您將它設定為與 hello 檢測金鑰，讓它知道 toosend hello 遙測的其中。</span><span class="sxs-lookup"><span data-stu-id="540e2-112">When you install hello Application Insights package toomonitor your app, you configure it with hello instrumentation key, so that it knows where toosend hello telemetry.</span></span>

<span data-ttu-id="540e2-113">您通常會選擇 toouse 不同資源或單一的共用的資源在不同案例中：</span><span class="sxs-lookup"><span data-stu-id="540e2-113">You typically choose toouse separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="540e2-114">獨立的不同應用程式 - 為每個應用程式使用不同的資源和 ikey。</span><span class="sxs-lookup"><span data-stu-id="540e2-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="540e2-115">使用多個元件或角色的一個商務應用程式-[單一共用的資源](app-insights-monitor-multi-role-apps.md)針對所有 hello 元件應用程式。</span><span class="sxs-lookup"><span data-stu-id="540e2-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all hello component apps.</span></span> <span data-ttu-id="540e2-116">遙測可以篩選或依 hello cloud_RoleName 屬性。</span><span class="sxs-lookup"><span data-stu-id="540e2-116">Telemetry can be filtered or segmented by hello cloud_RoleName property.</span></span>
* <span data-ttu-id="540e2-117">開發、 測試和發行集使用個別的資源和 ikey '的戳記' hello 系統的版本或實際執行階段。</span><span class="sxs-lookup"><span data-stu-id="540e2-117">Development, Test, and Release - Use a separate resource and ikey for versions of hello system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="540e2-118">A | B 測試 - 使用單一資源。</span><span class="sxs-lookup"><span data-stu-id="540e2-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="540e2-119">建立 TelemetryInitializer tooadd 識別 hello 變化屬性 toohello 遙測。</span><span class="sxs-lookup"><span data-stu-id="540e2-119">Create a TelemetryInitializer tooadd a property toohello telemetry that identifies hello variants.</span></span>


## <span data-ttu-id="540e2-120"><a name="dynamic-ikey"></a> 動態檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="540e2-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="540e2-121">toomake 方便您的生產環境中，階段之間移動的 toochange hello ikey hello 的程式碼在設定程式碼，而不是 hello 組態檔中。</span><span class="sxs-lookup"><span data-stu-id="540e2-121">toomake it easier toochange hello ikey as hello code moves between stages of production, set it in code instead of in hello configuration file.</span></span>

<span data-ttu-id="540e2-122">在初始設定方法，例如 global.aspx.cs ASP.NET 服務中設定 hello 機碼：</span><span class="sxs-lookup"><span data-stu-id="540e2-122">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="540e2-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="540e2-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="540e2-124">在此範例中，hello 不同資源的 hello ikeys 會放置在不同版本的 hello web 組態檔。</span><span class="sxs-lookup"><span data-stu-id="540e2-124">In this example, hello ikeys for hello different resources are placed in different versions of hello web configuration file.</span></span> <span data-ttu-id="540e2-125">正在交換 hello web 的組態檔的可執行的 hello 發行指令碼一部分-將會交換 hello 目標資源。</span><span class="sxs-lookup"><span data-stu-id="540e2-125">Swapping hello web configuration file - which you can do as part of hello release script - will swap hello target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="540e2-126">網頁</span><span class="sxs-lookup"><span data-stu-id="540e2-126">Web pages</span></span>
<span data-ttu-id="540e2-127">hello iKey 也會在您的應用程式中的網頁，hello [hello 快速入門刀鋒視窗中取得的指令碼](app-insights-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="540e2-127">hello iKey is also used in your app's web pages, in hello [script that you got from hello quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="540e2-128">常值到 hello 指令碼中編碼，並不會從 hello 伺服器狀態產生它。</span><span class="sxs-lookup"><span data-stu-id="540e2-128">Instead of coding it literally into hello script, generate it from hello server state.</span></span> <span data-ttu-id="540e2-129">例如，在 ASP.NET 應用程式中：</span><span class="sxs-lookup"><span data-stu-id="540e2-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="540e2-130">*Razor 中的 JavaScript*</span><span class="sxs-lookup"><span data-stu-id="540e2-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="540e2-131">建立其他 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="540e2-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="540e2-132">tooseparate 遙測不同的應用程式元件，或針對不同的戳記 （開發/測試/生產環境） 的 hello 相同元件，則您將必須 toocreate 新的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="540e2-132">tooseparate telemetry for different application components, or for different stamps (dev/test/production) of hello same component, then you'll have toocreate a new Application Insights resource.</span></span>

<span data-ttu-id="540e2-133">在 hello [portal.azure.com](https://portal.azure.com)，加入 Application Insights 資源：</span><span class="sxs-lookup"><span data-stu-id="540e2-133">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![按一下 新增，然後按一下Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="540e2-135">**應用程式類型**會影響您在 hello 概觀刀鋒視窗，然後 hello 中可用的屬性上看到[度量總管](app-insights-metrics-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="540e2-135">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="540e2-136">如果您沒有看到您的應用程式的類型，請選擇其中一種 web 網頁的 hello web 類型。</span><span class="sxs-lookup"><span data-stu-id="540e2-136">If you don't see your type of app, choose one of hello web types for web pages.</span></span>
* <span data-ttu-id="540e2-137">**資源群組** 可讓您輕鬆管理屬性，例如 [存取控制](app-insights-resources-roles-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="540e2-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="540e2-138">您可以對開發、測試和生產環境使用不同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="540e2-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="540e2-139">**訂用帳戶** 是您在 Azure 中的付款帳戶。</span><span class="sxs-lookup"><span data-stu-id="540e2-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="540e2-140">**位置** 是我們保留您資料的地方。</span><span class="sxs-lookup"><span data-stu-id="540e2-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="540e2-141">目前無法變更位置。</span><span class="sxs-lookup"><span data-stu-id="540e2-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="540e2-142">**新增 toodashboard**可以在 Azure 首頁上放置快速存取磚以取得您的資源。</span><span class="sxs-lookup"><span data-stu-id="540e2-142">**Add toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="540e2-143">建立 hello 資源需要花幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="540e2-143">Creating hello resource takes a few seconds.</span></span> <span data-ttu-id="540e2-144">完成時，您會看到警示。</span><span class="sxs-lookup"><span data-stu-id="540e2-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="540e2-145">(您可以撰寫[PowerShell 指令碼](app-insights-powershell-script-create-resource.md)toocreate 資源自動。)</span><span class="sxs-lookup"><span data-stu-id="540e2-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) toocreate a resource automatically.)</span></span>

### <a name="getting-hello-instrumentation-key"></a><span data-ttu-id="540e2-146">取得 hello 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="540e2-146">Getting hello instrumentation key</span></span>
<span data-ttu-id="540e2-147">hello 檢測金鑰會識別您所建立的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="540e2-147">hello instrumentation key identifies hello resource that you created.</span></span> 

![按一下 Essentials，請按一下 hello 檢測金鑰 CTRL + C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="540e2-149">您需要 hello 檢測金鑰的所有 hello 資源 toowhich 您的應用程式會傳送資料。</span><span class="sxs-lookup"><span data-stu-id="540e2-149">You need hello instrumentation keys of all hello resources toowhich your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="540e2-150">篩選組建編號</span><span class="sxs-lookup"><span data-stu-id="540e2-150">Filter on build number</span></span>
<span data-ttu-id="540e2-151">當您發行應用程式的新版本時，您會想從不同的組建 toobe 無法 tooseparate hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="540e2-151">When you publish a new version of your app, you'll want toobe able tooseparate hello telemetry from different builds.</span></span>

<span data-ttu-id="540e2-152">您可以設定 hello 應用程式版本屬性，以便您可以篩選[搜尋](app-insights-diagnostic-search.md)和[度量總管](app-insights-metrics-explorer.md)結果。</span><span class="sxs-lookup"><span data-stu-id="540e2-152">You can set hello Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![針對屬性進行篩選](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="540e2-154">有數種不同的方法設定的 hello 應用程式版本屬性。</span><span class="sxs-lookup"><span data-stu-id="540e2-154">There are several different methods of setting hello Application Version property.</span></span>

* <span data-ttu-id="540e2-155">直接設定：</span><span class="sxs-lookup"><span data-stu-id="540e2-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="540e2-156">包裝在該行[遙測初始設定式](app-insights-api-custom-events-metrics.md#defaults)tooensure 一致地設定所有 TelemetryClient 執行個體。</span><span class="sxs-lookup"><span data-stu-id="540e2-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) tooensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="540e2-157">[ASP.NET]集合中的 hello 版本`BuildInfo.config`。</span><span class="sxs-lookup"><span data-stu-id="540e2-157">[ASP.NET] Set hello version in `BuildInfo.config`.</span></span> <span data-ttu-id="540e2-158">hello web 模組將挑選 hello hello BuildLabel 節點版本。</span><span class="sxs-lookup"><span data-stu-id="540e2-158">hello web module will pick up hello version from hello BuildLabel node.</span></span> <span data-ttu-id="540e2-159">在您的專案中包含這個檔案，並記住 tooset hello 永遠複製屬性在 [方案總管]。</span><span class="sxs-lookup"><span data-stu-id="540e2-159">Include this file in your project and remember tooset hello Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="540e2-160">[ASP.NET] 在 MSBuild 中自動產生 BuildInfo.config。</span><span class="sxs-lookup"><span data-stu-id="540e2-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="540e2-161">toodo，加入幾行 tooyour`.csproj`檔案：</span><span class="sxs-lookup"><span data-stu-id="540e2-161">toodo this, add a few lines tooyour `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="540e2-162">這會產生檔案，稱為*yourProjectName*。BuildInfo.config。 hello 發行程序重新命名它 tooBuildInfo.config。</span><span class="sxs-lookup"><span data-stu-id="540e2-162">This generates a file called *yourProjectName*.BuildInfo.config. hello Publish process renames it tooBuildInfo.config.</span></span>

    <span data-ttu-id="540e2-163">當您使用 Visual Studio 建置 hello 組建標籤會包含預留位置 (AutoGen_...)。</span><span class="sxs-lookup"><span data-stu-id="540e2-163">hello build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="540e2-164">但是，MSBuild 以建立時，其中已填入 hello 正確的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="540e2-164">But when built with MSBuild, it is populated with hello correct version number.</span></span>

    <span data-ttu-id="540e2-165">tooallow MSBuild toogenerate 版本號碼，將版本設定 hello 喜歡`1.0.*`AssemblyReference.cs 中</span><span class="sxs-lookup"><span data-stu-id="540e2-165">tooallow MSBuild toogenerate version numbers, set hello version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="540e2-166">版本和版次追蹤</span><span class="sxs-lookup"><span data-stu-id="540e2-166">Version and release tracking</span></span>
<span data-ttu-id="540e2-167">tootrack hello 應用程式版本，請確定`buildinfo.config`由您的 Microsoft Build Engine 程序所產生。</span><span class="sxs-lookup"><span data-stu-id="540e2-167">tootrack hello application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="540e2-168">在您的 .csproj 檔案中加入：</span><span class="sxs-lookup"><span data-stu-id="540e2-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="540e2-169">當有 hello 組建資訊時，hello Application Insights web 模組自動加入**應用程式版本**做為屬性 tooevery 項目的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="540e2-169">When it has hello build info, hello Application Insights web module automatically adds **Application version** as a property tooevery item of telemetry.</span></span> <span data-ttu-id="540e2-170">可讓您 toofilter 版本執行時[診斷搜尋](app-insights-diagnostic-search.md)，或當您[瀏覽度量](app-insights-metrics-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="540e2-170">That allows you toofilter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="540e2-171">不過，請注意，hello 組建版本號碼會產生僅供 Microsoft Build Engine，不是由 hello 開發人員建置 Visual Studio 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="540e2-171">However, notice that hello build version number is generated only by hello Microsoft Build Engine, not by hello developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="540e2-172">版本註解</span><span class="sxs-lookup"><span data-stu-id="540e2-172">Release annotations</span></span>
<span data-ttu-id="540e2-173">如果您使用 Visual Studio Team Services 時，您可以[取得註解標記](app-insights-annotations.md)加入 tooyour 圖表，每當您發行新版本。</span><span class="sxs-lookup"><span data-stu-id="540e2-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added tooyour charts whenever you release a new version.</span></span> <span data-ttu-id="540e2-174">hello 下列影像顯示此標記的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="540e2-174">hello following image shows how this marker appears.</span></span>

![圖表上版本註解範例的螢幕擷取畫面](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="540e2-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="540e2-176">Next steps</span></span>

* [<span data-ttu-id="540e2-177">多個角色的共用資源</span><span class="sxs-lookup"><span data-stu-id="540e2-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="540e2-178">建立遙測初始設定式 toodistinguish A |B 變異</span><span class="sxs-lookup"><span data-stu-id="540e2-178">Create a Telemetry Initializer toodistinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
