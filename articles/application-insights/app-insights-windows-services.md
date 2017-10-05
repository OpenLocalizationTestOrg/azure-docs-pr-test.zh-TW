---
title: "適用於 Windows 伺服器和背景工作角色的 Azure Application Insights | Microsoft Docs"
description: "將 Application Insights SDK 手動新增至您的 ASP.NET 應用程式，以分析使用情況、可用性和效能。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 4b9f8c618a69c4c157dafeb7f726aae24efad428
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="fc3d9-103">為 .NET 應用程式手動設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="fc3d9-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="fc3d9-104">您可以設定 [Application Insights](app-insights-overview.md) 以監視各種不同的應用程式或應用程式角色、元件或微服務。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-104">You can configure [Application Insights](app-insights-overview.md) to monitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="fc3d9-105">對於 Web 應用程式和服務，Visual Studio 會提供[單步驟設定](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="fc3d9-106">對於其他類型的 .NET 應用程式 (例如後端伺服器角色或桌面應用程式)，您可以手動設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![範例效能監視圖表](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="fc3d9-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="fc3d9-108">Before you start</span></span>

<span data-ttu-id="fc3d9-109">您需要：</span><span class="sxs-lookup"><span data-stu-id="fc3d9-109">You need:</span></span>

* <span data-ttu-id="fc3d9-110">[Microsoft Azure](http://azure.com)訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-110">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="fc3d9-111">如果您的小組或組織擁有 Azure 訂用帳戶，擁有者就可以使用您的 [Microsoft 帳戶](http://live.com)將您加入。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="fc3d9-112">Visual Studio 2013 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="fc3d9-113"><a name="add"></a>1.選擇 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="fc3d9-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="fc3d9-114">「資源」是在 Azure 入口網站中收集和顯示您資料的位置。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-114">The 'resource' is where your data is collected and displayed in the Azure portal.</span></span> <span data-ttu-id="fc3d9-115">您需要決定是否要建立新的資源，或共用現有資源。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-115">You need to decide whether to create a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="fc3d9-116">屬於大型應用程式︰使用現有資源</span><span class="sxs-lookup"><span data-stu-id="fc3d9-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="fc3d9-117">如果您的 Web 應用程式有多個元件 (例如，前端 Web 應用程式和一或多個後端服務)，您應該將來自所有元件的遙測傳送至相同的資源。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all the components to the same resource.</span></span> <span data-ttu-id="fc3d9-118">這會讓它們顯示在單一應用程式對應上，並可追蹤元件之間的要求。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-118">This will enable them to be displayed on a single Application Map, and make it possible to trace a request from one component to another.</span></span>

<span data-ttu-id="fc3d9-119">因此，如果您已監視此應用程式的其他元件，只要使用相同的資源即可。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-119">So, if you're already monitoring other components of this app, then just use the same resource.</span></span>

<span data-ttu-id="fc3d9-120">在 [Azure 入口網站](https://portal.azure.com/)中開啟資源。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-120">Open the resource in the [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="fc3d9-121">獨立應用程式：建立新的資源</span><span class="sxs-lookup"><span data-stu-id="fc3d9-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="fc3d9-122">如果新的應用程式與其他應用程式無關，則應該有自己的資源。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-122">If the new app is unrelated to other applications, then it should have its own resource.</span></span>

<span data-ttu-id="fc3d9-123">登入 [Azure 入口網站](https://portal.azure.com/)，並建立新的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-123">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="fc3d9-124">選擇 ASP.NET 做為應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-124">Choose ASP.NET as the application type.</span></span>

![按一下 [新增]，然後按一下 [Application Insights]](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="fc3d9-126">所選的應用程式類型會設定資源刀鋒視窗的預設內容。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-126">The choice of application type sets the default content of the resource blades.</span></span>

## <a name="2-copy-the-instrumentation-key"></a><span data-ttu-id="fc3d9-127">2.複製檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="fc3d9-127">2. Copy the Instrumentation Key</span></span>
<span data-ttu-id="fc3d9-128">可識別資源的金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-128">The key identifies the resource.</span></span> <span data-ttu-id="fc3d9-129">您很快就會將它安裝在 SDK 中，以便將資料導向資源。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-129">You'll install it soon in the SDK, in order to direct data to the resource.</span></span>

![按一下 [屬性]，選取金鑰，然後按下 CTRL+C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="fc3d9-131"><a name="sdk"></a>3.在您的應用程式中安裝 Application Insights 套件</span><span class="sxs-lookup"><span data-stu-id="fc3d9-131"><a name="sdk"></a>3. Install the Application Insights package in your application</span></span>
<span data-ttu-id="fc3d9-132">安裝和設定 Application Insights 套件會因您所正在使用的平台而有所不同。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-132">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span></span> 

1. <span data-ttu-id="fc3d9-133">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選擇 [管理 Nuget 套件]。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![以滑鼠右鍵按一下專案，然後選取 [管理 NuGet 套件]](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="fc3d9-135">針對 Windows Server 應用程式安裝 Application Insights 套件 "Microsoft.ApplicationInsights.WindowsServer"。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-135">Install the Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![搜尋「Application Insights」](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="fc3d9-137">*哪個版本？*</span><span class="sxs-lookup"><span data-stu-id="fc3d9-137">*Which version?*</span></span>

    <span data-ttu-id="fc3d9-138">如果您想要嘗試最新的功能，請勾選 [包括搶鮮版]。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-138">Check **Include prerelease** if you want to try our latest features.</span></span> <span data-ttu-id="fc3d9-139">相關的文件或部落格會指明您是否需要搶鮮版。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-139">The relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="fc3d9-140">*可以使用其他封裝嗎？*</span><span class="sxs-lookup"><span data-stu-id="fc3d9-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="fc3d9-141">是。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-141">Yes.</span></span> <span data-ttu-id="fc3d9-142">如果您只想要使用 API 來傳送自己的遙測，請選擇 "Microsoft.ApplicationInsights"。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-142">Choose "Microsoft.ApplicationInsights" if you only want to use the API to send your own telemetry.</span></span> <span data-ttu-id="fc3d9-143">Windows Server 套件會包含 API 及其他套件，例如效能計數器收集和相依性監視。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-143">The Windows Server package includes the API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="to-upgrade-to-future-package-versions"></a><span data-ttu-id="fc3d9-144">升級至未來的套件版本</span><span class="sxs-lookup"><span data-stu-id="fc3d9-144">To upgrade to future package versions</span></span>
<span data-ttu-id="fc3d9-145">我們隨時會發行新版的 SDK。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-145">We release a new version of the SDK from time to time.</span></span>

<span data-ttu-id="fc3d9-146">若要升級至[新版的套件](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/)，請再次開啟 NuGet 套件管理員，並篩選出已安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-146">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="fc3d9-147">選取 **Microsoft.ApplicationInsights.WindowsServer**，然後選擇 [升級]。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="fc3d9-148">如果您已對 ApplicationInsights.config 進行任何的自訂，請在升級前儲存複本，並在升級後合併您的變更到新版本中。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-148">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="fc3d9-149">4.傳送遙測</span><span class="sxs-lookup"><span data-stu-id="fc3d9-149">4. Send telemetry</span></span>
<span data-ttu-id="fc3d9-150">**如果您只安裝 API 套件︰**</span><span class="sxs-lookup"><span data-stu-id="fc3d9-150">**If you installed only the API package:**</span></span>

* <span data-ttu-id="fc3d9-151">在程式碼中設定檢測金鑰，例如在 `main()`中：</span><span class="sxs-lookup"><span data-stu-id="fc3d9-151">Set the instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="fc3d9-152">`TelemetryConfiguration.Active.InstrumentationKey = "`您的金鑰 `";`</span><span class="sxs-lookup"><span data-stu-id="fc3d9-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="fc3d9-153">[使用 API 撰寫自己的遙測](app-insights-api-custom-events-metrics.md#ikey)。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-153">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="fc3d9-154">**如果您安裝了其他 Application Insights 封裝** ，您可以視需要使用 .config 檔案來設定檢測金鑰︰</span><span class="sxs-lookup"><span data-stu-id="fc3d9-154">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span></span>

* <span data-ttu-id="fc3d9-155">編輯 ApplicationInsights.config (已由 NuGet 安裝加入)。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-155">Edit ApplicationInsights.config (which was added by the NuGet install).</span></span> <span data-ttu-id="fc3d9-156">在結尾標記前面插入此內容：</span><span class="sxs-lookup"><span data-stu-id="fc3d9-156">Insert this just before the closing tag:</span></span>
  
    <span data-ttu-id="fc3d9-157">`<InstrumentationKey>`您複製的檢測金鑰 `</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="fc3d9-157">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="fc3d9-158">確定 [方案總管] 中 ApplicationInsights.config 的屬性已設定為 [建置動作] = [內容]、[複製到輸出目錄] = [複製] 。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-158">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>

<span data-ttu-id="fc3d9-159">如果您想要[針對不同建置組態切換金鑰](app-insights-separate-resources.md)，在程式碼中設定檢測金鑰便很實用。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-159">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="fc3d9-160">如果您在程式碼中設定金鑰，您不必在 `.config` 檔案中設定它。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-160">If you set the key in code, you don't have to set it in the `.config` file.</span></span>

## <span data-ttu-id="fc3d9-161"><a name="run"></a> 執行專案</span><span class="sxs-lookup"><span data-stu-id="fc3d9-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="fc3d9-162">使用 **F5** 執行應用程式並立即試用：開啟不同的頁面來產生一些遙測。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-162">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span></span>

<span data-ttu-id="fc3d9-163">在 Visual Studio 中，您可以看見已傳送到的事件計數。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-163">In Visual Studio, you'll see a count of the events that have been sent.</span></span>

![Visual Studio 中的事件計數](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="fc3d9-165"><a name="monitor"></a> 檢視遙測</span><span class="sxs-lookup"><span data-stu-id="fc3d9-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="fc3d9-166">返回 [Azure 入口網站](https://portal.azure.com/) ，並且瀏覽至您的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-166">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="fc3d9-167">在 [概觀] 圖表中尋找資料。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-167">Look for data in the Overview charts.</span></span> <span data-ttu-id="fc3d9-168">剛開始的時候，您只會看見一或兩個資料點。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="fc3d9-169">例如：</span><span class="sxs-lookup"><span data-stu-id="fc3d9-169">For example:</span></span>

![Click through to more data](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="fc3d9-171">按一下任何圖表以查看詳細度量。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-171">Click through any chart to see more detailed metrics.</span></span> [<span data-ttu-id="fc3d9-172">深入了解度量。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="fc3d9-173">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="fc3d9-173">No data?</span></span>
* <span data-ttu-id="fc3d9-174">使用應用程式、開啟不同頁面，以產生一些遙測。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-174">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="fc3d9-175">開啟 [ [搜尋](app-insights-diagnostic-search.md) ] 磚來查看個別事件。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-175">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="fc3d9-176">有時候，事件通過計量管線所需的時間較長。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-176">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="fc3d9-177">請稍等片刻，然後按一下 [重新整理 ]。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="fc3d9-178">圖表會定期自行重新整理，但是如果您在等待一些要顯示的資料，您可以手動重新整理。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="fc3d9-179">請參閱 [疑難排解](app-insights-troubleshoot-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="fc3d9-180">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="fc3d9-180">Publish your app</span></span>
<span data-ttu-id="fc3d9-181">現在將應用程式部署至您的伺服器或 Azure，並觀看資料累積情形。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-181">Now deploy your application to your server or to Azure and watch the data accumulate.</span></span>

![使用 Visual Studio 來發佈您的應用程式](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="fc3d9-183">以偵錯模式執行時，系統會透過管線迅速傳送遙測資料，因此您應該可以在幾秒內看見資料。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-183">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="fc3d9-184">以發行組態部署應用程式時，資料累積會較為緩慢。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="fc3d9-185">發佈資料到伺服器之後，卻沒有資料？</span><span class="sxs-lookup"><span data-stu-id="fc3d9-185">No data after you publish to your server?</span></span>
<span data-ttu-id="fc3d9-186">請在您的伺服器防火牆中，開啟連出流量的連接埠。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="fc3d9-187">請參閱[本頁](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses)以取得必要位址清單</span><span class="sxs-lookup"><span data-stu-id="fc3d9-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="fc3d9-188">組建伺服器發生問題？</span><span class="sxs-lookup"><span data-stu-id="fc3d9-188">Trouble on your build server?</span></span>
<span data-ttu-id="fc3d9-189">請參閱 [此疑難排解項目](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild)。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="fc3d9-190">如果您的應用程式會產生大量遙測，調適性取樣模型會自動藉由僅傳送事件代表性片段，減少傳送到入口網站的量。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-190">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="fc3d9-191">不過，與同一個要求相關的事件會選取或取消選取為群組，讓您可以在相關事件之間瀏覽。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-191">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="fc3d9-192">[了解取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="fc3d9-193">影片</span><span class="sxs-lookup"><span data-stu-id="fc3d9-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="fc3d9-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc3d9-194">Next steps</span></span>
* <span data-ttu-id="fc3d9-195">[新增更多遙測](app-insights-asp-net-more.md) 可取得應用程式的完整 360 度檢視。</span><span class="sxs-lookup"><span data-stu-id="fc3d9-195">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span></span>

