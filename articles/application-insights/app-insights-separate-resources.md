---
title: "在 Azure Application Insights 中區分開發、測試及發行的遙測 | Microsoft Docs"
description: "將遙測導向開發、測試和生產戳記的不同資源。"
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
ms.openlocfilehash: f51fa4639aaa60686cc349683713c6e5f9732bb9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="3a488-103">區分開發、測試及生產環境的遙測</span><span class="sxs-lookup"><span data-stu-id="3a488-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="3a488-104">當您在開發下一版 Web 應用程式時，您不會想看到新版與已發行版本的 [Application Insights](app-insights-overview.md) 遙測混合在一起。</span><span class="sxs-lookup"><span data-stu-id="3a488-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span></span> <span data-ttu-id="3a488-105">為了避免混淆，請將不同開發階段的遙測，以不同的檢測金鑰 (ikey) 傳送到不同的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="3a488-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="3a488-106">為了能夠在版本移到另一個階段時更輕鬆地變更檢測金鑰，您可以將 ikey 設定在程式碼中 (而不是設定在組態檔中)。</span><span class="sxs-lookup"><span data-stu-id="3a488-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span></span> 

<span data-ttu-id="3a488-107">(如果您的系統是「Azure 雲端服務」，有[另一個設定個別 ikey 的方法](app-insights-cloudservices.md))。</span><span class="sxs-lookup"><span data-stu-id="3a488-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="3a488-108">關於資源和檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="3a488-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="3a488-109">在為 Web 應用程式設定 Application Insights 監視時，您會在 Microsoft Azure 中建立 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="3a488-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="3a488-110">您可以在 Azure 入口網站開啟此資源，以便查看並分析從應用程式中收集到的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="3a488-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span></span> <span data-ttu-id="3a488-111">透過「檢測金鑰」(iKey) 即可識別資源。</span><span class="sxs-lookup"><span data-stu-id="3a488-111">The resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="3a488-112">當您安裝 Application Insights 套件來監視應用程式時，您必須為它設定檢測金鑰，以便讓它知道要將遙測資料傳送到哪裡。</span><span class="sxs-lookup"><span data-stu-id="3a488-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span></span>

<span data-ttu-id="3a488-113">在不同情況下，您一般可以選擇使用不同資源或單一的共用資源︰</span><span class="sxs-lookup"><span data-stu-id="3a488-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="3a488-114">獨立的不同應用程式 - 為每個應用程式使用不同的資源和 ikey。</span><span class="sxs-lookup"><span data-stu-id="3a488-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="3a488-115">單一商務應用程式的多個元件或角色 - 為所有元件應用程式使用[單一的共用資源](app-insights-monitor-multi-role-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="3a488-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span></span> <span data-ttu-id="3a488-116">透過 cloud_RoleName 屬性即可篩選或區隔遙測。</span><span class="sxs-lookup"><span data-stu-id="3a488-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span></span>
* <span data-ttu-id="3a488-117">開發、測試和發行 - 在生產「戳記」或階段，為各個系統版本使用不同的資源和 ikey。</span><span class="sxs-lookup"><span data-stu-id="3a488-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="3a488-118">A | B 測試 - 使用單一資源。</span><span class="sxs-lookup"><span data-stu-id="3a488-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="3a488-119">建立 TelemetryInitializer 即可在遙測中新增屬性來識別變體。</span><span class="sxs-lookup"><span data-stu-id="3a488-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span></span>


## <span data-ttu-id="3a488-120"><a name="dynamic-ikey"></a> 動態檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="3a488-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="3a488-121">若要能夠在程式碼歷經不同生產階段時更輕鬆地變更 ikey，請將 ikey 設定在程式碼中 (而不是設定在組態檔中)。</span><span class="sxs-lookup"><span data-stu-id="3a488-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span></span>

<span data-ttu-id="3a488-122">在初始化方法中設定金鑰，例如 ASP.NET 服務中的 global.aspx.cs：</span><span class="sxs-lookup"><span data-stu-id="3a488-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="3a488-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="3a488-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="3a488-124">在此範例中，不同資源的 ikeys 會放置在不同版本的 Web 組態檔中。</span><span class="sxs-lookup"><span data-stu-id="3a488-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="3a488-125">交換 Web 組態檔 (您可以在發行指令碼中進行) 將會交換目標資源。</span><span class="sxs-lookup"><span data-stu-id="3a488-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="3a488-126">網頁</span><span class="sxs-lookup"><span data-stu-id="3a488-126">Web pages</span></span>
<span data-ttu-id="3a488-127">iKey 也會用在您的應用程式網頁中，在 [您從快速啟動刀鋒視窗取得的指令碼](app-insights-javascript.md)中。</span><span class="sxs-lookup"><span data-stu-id="3a488-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="3a488-128">不要按其原義編寫至指令碼，請從伺服器狀態產生。</span><span class="sxs-lookup"><span data-stu-id="3a488-128">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="3a488-129">例如，在 ASP.NET 應用程式中：</span><span class="sxs-lookup"><span data-stu-id="3a488-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="3a488-130">*Razor 中的 JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3a488-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="3a488-131">建立其他 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="3a488-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="3a488-132">若要區分不同應用程式元件的遙測，或區分相同元件的不同戳記 (開發/測試/生產) 的遙測，則必須建立新的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="3a488-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="3a488-133">在 [portal.azure.com](https://portal.azure.com)中新增 Application Insights 資源：</span><span class="sxs-lookup"><span data-stu-id="3a488-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![按一下 [新增]，然後按一下 [Application Insights]](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="3a488-135">**應用程式類型** 會影響您在 [概觀] 刀鋒視窗中看到的內容，以及 [計量瀏覽器](app-insights-metrics-explorer.md)中提供的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a488-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="3a488-136">如果沒有看到您的應用程式類型，請針對網頁選擇其中一個 Web 類型。</span><span class="sxs-lookup"><span data-stu-id="3a488-136">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="3a488-137">**資源群組** 可讓您輕鬆管理屬性，例如 [存取控制](app-insights-resources-roles-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="3a488-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="3a488-138">您可以對開發、測試和生產環境使用不同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3a488-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="3a488-139">**訂用帳戶** 是您在 Azure 中的付款帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a488-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="3a488-140">**位置** 是我們保留您資料的地方。</span><span class="sxs-lookup"><span data-stu-id="3a488-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="3a488-141">目前無法變更位置。</span><span class="sxs-lookup"><span data-stu-id="3a488-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="3a488-142">**新增至儀表板** 可在 Azure 首頁上放置資源的快速存取圖格。</span><span class="sxs-lookup"><span data-stu-id="3a488-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="3a488-143">建立資源需要幾秒鐘。</span><span class="sxs-lookup"><span data-stu-id="3a488-143">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="3a488-144">完成時，您會看到警示。</span><span class="sxs-lookup"><span data-stu-id="3a488-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="3a488-145">(您可以撰寫 [PowerShell 指令碼](app-insights-powershell-script-create-resource.md)來自動建立資源)。</span><span class="sxs-lookup"><span data-stu-id="3a488-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

### <a name="getting-the-instrumentation-key"></a><span data-ttu-id="3a488-146">取得檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="3a488-146">Getting the instrumentation key</span></span>
<span data-ttu-id="3a488-147">檢測金鑰會識別您所建立的資源。</span><span class="sxs-lookup"><span data-stu-id="3a488-147">The instrumentation key identifies the resource that you created.</span></span> 

![按一下 [基本功能]，按一下 [檢測金鑰]，CTRL+C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="3a488-149">您將需要您的應用程式會將資料傳送至其中的所有資源的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="3a488-149">You need the instrumentation keys of all the resources to which your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="3a488-150">篩選組建編號</span><span class="sxs-lookup"><span data-stu-id="3a488-150">Filter on build number</span></span>
<span data-ttu-id="3a488-151">當您發佈新的 App 版本時，希望能夠將不同組建的遙測分開。</span><span class="sxs-lookup"><span data-stu-id="3a488-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="3a488-152">您可以設定 [應用程式版本] 屬性，如此便能篩選[搜尋](app-insights-diagnostic-search.md)和[計量總管](app-insights-metrics-explorer.md)的結果。</span><span class="sxs-lookup"><span data-stu-id="3a488-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![針對屬性進行篩選](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="3a488-154">設定 [應用程式版本] 屬性有幾種不同的方法。</span><span class="sxs-lookup"><span data-stu-id="3a488-154">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="3a488-155">直接設定：</span><span class="sxs-lookup"><span data-stu-id="3a488-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="3a488-156">在 [遙測初始設定式](app-insights-api-custom-events-metrics.md#defaults) 中將該行換行，以確保會以一致性方式設定所有 TelemetryClient 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3a488-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="3a488-157">[ASP.NET] 在 `BuildInfo.config`中設定版本。</span><span class="sxs-lookup"><span data-stu-id="3a488-157">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="3a488-158">Web 模組將會從 BuildLabel 節點取得版本。</span><span class="sxs-lookup"><span data-stu-id="3a488-158">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="3a488-159">在您的專案中包含此檔案， 而且記得要在 [方案總管] 中設定 [永遠複製] 屬性。</span><span class="sxs-lookup"><span data-stu-id="3a488-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

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
* <span data-ttu-id="3a488-160">[ASP.NET] 在 MSBuild 中自動產生 BuildInfo.config。</span><span class="sxs-lookup"><span data-stu-id="3a488-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="3a488-161">若要這樣做，請先在 `.csproj` 檔案中加入幾行：</span><span class="sxs-lookup"><span data-stu-id="3a488-161">To do this, add a few lines to your `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="3a488-162">這會產生一個稱為 *yourProjectName*.BuildInfo.config 的檔案。發佈程序會將這個檔案重新命名為 BuildInfo.config。</span><span class="sxs-lookup"><span data-stu-id="3a488-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="3a488-163">當您使用 Visual Studio 建置時，組建標籤會包含預留位置 (AutoGen_...)。</span><span class="sxs-lookup"><span data-stu-id="3a488-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="3a488-164">但是當使用 MSBuild 建立時，則會填入正確的版本號碼。</span><span class="sxs-lookup"><span data-stu-id="3a488-164">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="3a488-165">若要允許 MSBuild 產生版本號碼，請在 AssemblyReference.cs 中設定類似 `1.0.*` 的版本</span><span class="sxs-lookup"><span data-stu-id="3a488-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="3a488-166">版本和版次追蹤</span><span class="sxs-lookup"><span data-stu-id="3a488-166">Version and release tracking</span></span>
<span data-ttu-id="3a488-167">若要追蹤應用程式版本，請確定您的 Microsoft Build Engine 程序已產生 `buildinfo.config`。</span><span class="sxs-lookup"><span data-stu-id="3a488-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="3a488-168">在您的 .csproj 檔案中加入：</span><span class="sxs-lookup"><span data-stu-id="3a488-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="3a488-169">當它有組建資訊時，Application Insights Web 模組會自動新增 **應用程式版本** ，做為每個遙測項目的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a488-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="3a488-170">如此可讓您在執行[診斷搜尋](app-insights-diagnostic-search.md)或在[探索計量](app-insights-metrics-explorer.md)時，依據版本來篩選。</span><span class="sxs-lookup"><span data-stu-id="3a488-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="3a488-171">但請注意，組建版本號碼只由 Microsoft Build Engine 產生，而不是由 Visual Studio 中的開發人員組建產生。</span><span class="sxs-lookup"><span data-stu-id="3a488-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="3a488-172">版本註解</span><span class="sxs-lookup"><span data-stu-id="3a488-172">Release annotations</span></span>
<span data-ttu-id="3a488-173">如果您使用 Visual Studio Team Services，您可以[取得註解標記](app-insights-annotations.md) (每當發行新版本時，這會新增至您的圖表)。</span><span class="sxs-lookup"><span data-stu-id="3a488-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="3a488-174">下圖顯示此標記的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="3a488-174">The following image shows how this marker appears.</span></span>

![圖表上版本註解範例的螢幕擷取畫面](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="3a488-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a488-176">Next steps</span></span>

* [<span data-ttu-id="3a488-177">多個角色的共用資源</span><span class="sxs-lookup"><span data-stu-id="3a488-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="3a488-178">建立遙測初始設定式來區分 A |B 變體</span><span class="sxs-lookup"><span data-stu-id="3a488-178">Create a Telemetry Initializer to distinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
