---
title: "aaaAzure Insights 的應用程式的 Windows server 和背景工作角色 |Microsoft 文件"
description: "手動新增 hello Application Insights SDK tooyour ASP.NET 應用程式 tooanalyze 使用狀況、 可用性和效能。"
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
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="084e7-103">為 .NET 應用程式手動設定 Application Insights</span><span class="sxs-lookup"><span data-stu-id="084e7-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="084e7-104">您可以設定[Application Insights](app-insights-overview.md) toomonitor 各種不同的應用程式或應用程式角色、 元件或 microservices。</span><span class="sxs-lookup"><span data-stu-id="084e7-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="084e7-105">對於 Web 應用程式和服務，Visual Studio 會提供[單步驟設定](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="084e7-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="084e7-106">對於其他類型的 .NET 應用程式 (例如後端伺服器角色或桌面應用程式)，您可以手動設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="084e7-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![範例效能監視圖表](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="084e7-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="084e7-108">Before you start</span></span>

<span data-ttu-id="084e7-109">您需要：</span><span class="sxs-lookup"><span data-stu-id="084e7-109">You need:</span></span>

* <span data-ttu-id="084e7-110">訂用帳戶太[Microsoft Azure](http://azure.com)。</span><span class="sxs-lookup"><span data-stu-id="084e7-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="084e7-111">如果您的小組或組織有 Azure 訂用帳戶，hello 擁有者可以將您加入 tooit，使用您[Microsoft 帳戶](http://live.com)。</span><span class="sxs-lookup"><span data-stu-id="084e7-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="084e7-112">Visual Studio 2013 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="084e7-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="084e7-113"><a name="add"></a>1.選擇 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="084e7-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="084e7-114">hello 'resource' 是收集及顯示 hello Azure 入口網站中資料的位置。</span><span class="sxs-lookup"><span data-stu-id="084e7-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="084e7-115">您是否需要 toodecide toocreate 一個新或現有的共用。</span><span class="sxs-lookup"><span data-stu-id="084e7-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="084e7-116">屬於大型應用程式︰使用現有資源</span><span class="sxs-lookup"><span data-stu-id="084e7-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="084e7-117">如果您的 web 應用程式具有數個元件-例如前端的 web 應用程式和一個或多個後端服務層，則您應該從所有 hello 元件 toohello 傳送遙測相同的資源。</span><span class="sxs-lookup"><span data-stu-id="084e7-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="084e7-118">這會讓它們顯示在單一的應用程式對應，toobe，並將其可能 tootrace 來自一個元件 tooanother 的要求。</span><span class="sxs-lookup"><span data-stu-id="084e7-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="084e7-119">因此，如果您已經監視此應用程式的其他元件，然後只使用 hello 相同資源。</span><span class="sxs-lookup"><span data-stu-id="084e7-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="084e7-120">在 hello 開啟 hello 資源[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="084e7-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="084e7-121">獨立應用程式：建立新的資源</span><span class="sxs-lookup"><span data-stu-id="084e7-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="084e7-122">如果 hello 新應用程式是不相關的 tooother 應用程式，它應該有它自己的資源。</span><span class="sxs-lookup"><span data-stu-id="084e7-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="084e7-123">登入 toohello [Azure 入口網站](https://portal.azure.com/)，並建立新的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="084e7-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="084e7-124">選擇 ASP.NET 做為 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="084e7-124">Choose ASP.NET as hello application type.</span></span>

![按一下 新增，然後按一下Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="084e7-126">應用程式類型的 hello 選擇設定 hello 的 hello 資源刀鋒視窗的預設內容。</span><span class="sxs-lookup"><span data-stu-id="084e7-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="084e7-127">2.複製檢測機碼 hello</span><span class="sxs-lookup"><span data-stu-id="084e7-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="084e7-128">hello 索引鍵識別 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="084e7-128">hello key identifies hello resource.</span></span> <span data-ttu-id="084e7-129">您會將它安裝很快就在 hello SDK，順序 toodirect 資料 toohello 資源中。</span><span class="sxs-lookup"><span data-stu-id="084e7-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![按一下 內容選取 hello 金鑰，請按 ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="084e7-131"><a name="sdk"></a>3.安裝應用程式中的 hello Application Insights 套件</span><span class="sxs-lookup"><span data-stu-id="084e7-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="084e7-132">安裝和設定 hello Application Insights 封裝會根據您正在使用的 hello 平台而有所不同。</span><span class="sxs-lookup"><span data-stu-id="084e7-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="084e7-133">在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選擇 [管理 Nuget 套件]。</span><span class="sxs-lookup"><span data-stu-id="084e7-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Hello 專案上按一下滑鼠右鍵，然後選取 管理 Nuget 封裝](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="084e7-135">安裝 Windows server 應用程式，「 Microsoft.ApplicationInsights.WindowsServer。"hello Application Insights 套件</span><span class="sxs-lookup"><span data-stu-id="084e7-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![搜尋「Application Insights」](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="084e7-137">*哪個版本？*</span><span class="sxs-lookup"><span data-stu-id="084e7-137">*Which version?*</span></span>

    <span data-ttu-id="084e7-138">請檢查**包含發行前版本**如果您想 tootry 我們最新的功能。</span><span class="sxs-lookup"><span data-stu-id="084e7-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="084e7-139">hello 相關文件或部落格，請注意是否需要發行前版本。</span><span class="sxs-lookup"><span data-stu-id="084e7-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="084e7-140">*可以使用其他封裝嗎？*</span><span class="sxs-lookup"><span data-stu-id="084e7-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="084e7-141">是。</span><span class="sxs-lookup"><span data-stu-id="084e7-141">Yes.</span></span> <span data-ttu-id="084e7-142">如果您只想 toouse hello API toosend 您自己的遙測，請選擇 「 Microsoft.ApplicationInsights"。</span><span class="sxs-lookup"><span data-stu-id="084e7-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="084e7-143">hello Windows 伺服器套件包含 hello API 以及許多其他封裝，例如效能計數器集合與相依性監視。</span><span class="sxs-lookup"><span data-stu-id="084e7-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="084e7-144">tooupgrade toofuture 封裝版本</span><span class="sxs-lookup"><span data-stu-id="084e7-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="084e7-145">我們發行從時間 tootime hello SDK 的新版本。</span><span class="sxs-lookup"><span data-stu-id="084e7-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="084e7-146">tooupgrade tooa[新版 hello 封裝](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/)，再次開啟 NuGet 封裝管理員，然後篩選已安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="084e7-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="084e7-147">選取 **Microsoft.ApplicationInsights.WindowsServer**，然後選擇 [升級]。</span><span class="sxs-lookup"><span data-stu-id="084e7-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="084e7-148">如果您進行任何自訂 tooApplicationInsights.config，儲存一份之前升級，之後您的變更合併至 hello 新版本。</span><span class="sxs-lookup"><span data-stu-id="084e7-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="084e7-149">4.傳送遙測</span><span class="sxs-lookup"><span data-stu-id="084e7-149">4. Send telemetry</span></span>
<span data-ttu-id="084e7-150">**如果您已安裝只 hello API 套件：**</span><span class="sxs-lookup"><span data-stu-id="084e7-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="084e7-151">在中，例如設定在程式碼中的 hello 檢測金鑰`main()`:</span><span class="sxs-lookup"><span data-stu-id="084e7-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="084e7-152">`TelemetryConfiguration.Active.InstrumentationKey = "`您的金鑰 `";`</span><span class="sxs-lookup"><span data-stu-id="084e7-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="084e7-153">[撰寫您自己使用 hello API 的遙測](app-insights-api-custom-events-metrics.md#ikey)。</span><span class="sxs-lookup"><span data-stu-id="084e7-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="084e7-154">**如果您已安裝其他的 Application Insights 套件，**您可以如果您想要的話，使用 hello.config 檔案 tooset hello 檢測金鑰：</span><span class="sxs-lookup"><span data-stu-id="084e7-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="084e7-155">編輯 ApplicationInsights.config （這由 hello NuGet 安裝所加入）。</span><span class="sxs-lookup"><span data-stu-id="084e7-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="084e7-156">這只前面插入結尾標記的 hello:</span><span class="sxs-lookup"><span data-stu-id="084e7-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="084e7-157">`<InstrumentationKey>`*hello 檢測金鑰複製*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="084e7-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="084e7-158">請確定在 方案總管 ApplicationInsights.config hello 屬性會設太**建置動作 = 複製 tooOutput 目錄的內容 = 複製**。</span><span class="sxs-lookup"><span data-stu-id="084e7-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="084e7-159">如果您想太是程式碼中的有用 tooset hello 檢測金鑰[不同組建組態的交換器 hello 金鑰](app-insights-separate-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="084e7-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="084e7-160">如果您在程式碼中設定 hello 機碼，您不需要 tooset 在 hello`.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="084e7-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="084e7-161"><a name="run"></a> 執行專案</span><span class="sxs-lookup"><span data-stu-id="084e7-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="084e7-162">使用 hello **F5** toorun 您的應用程式，現在就試試看： 開啟不同的網頁 toogenerate 某些遙測。</span><span class="sxs-lookup"><span data-stu-id="084e7-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="084e7-163">在 Visual Studio 中，您會看到已傳送的 hello 事件計數。</span><span class="sxs-lookup"><span data-stu-id="084e7-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Visual Studio 中的事件計數](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="084e7-165"><a name="monitor"></a> 檢視遙測</span><span class="sxs-lookup"><span data-stu-id="084e7-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="084e7-166">傳回 toohello [Azure 入口網站](https://portal.azure.com/)並瀏覽 tooyour Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="084e7-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="084e7-167">尋找在 hello 概觀圖表中的資料。</span><span class="sxs-lookup"><span data-stu-id="084e7-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="084e7-168">剛開始的時候，您只會看見一或兩個資料點。</span><span class="sxs-lookup"><span data-stu-id="084e7-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="084e7-169">例如：</span><span class="sxs-lookup"><span data-stu-id="084e7-169">For example:</span></span>

![瀏覽 toomore 資料](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="084e7-171">按一下 透過任何圖表 toosee 度量詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="084e7-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="084e7-172">深入了解度量。</span><span class="sxs-lookup"><span data-stu-id="084e7-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="084e7-173">沒有資料？</span><span class="sxs-lookup"><span data-stu-id="084e7-173">No data?</span></span>
* <span data-ttu-id="084e7-174">使用 hello 應用程式，使其產生某些遙測開啟不同的頁面。</span><span class="sxs-lookup"><span data-stu-id="084e7-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="084e7-175">開啟 hello[搜尋](app-insights-diagnostic-search.md)磚，toosee 個別事件。</span><span class="sxs-lookup"><span data-stu-id="084e7-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="084e7-176">有時會事件稍長時 tooget hello 度量管線。</span><span class="sxs-lookup"><span data-stu-id="084e7-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="084e7-177">請稍等片刻，然後按一下 [重新整理 ]。</span><span class="sxs-lookup"><span data-stu-id="084e7-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="084e7-178">圖表定期重新整理本身，但您可以手動重新整理如果正在等待某些資料 tooshow。</span><span class="sxs-lookup"><span data-stu-id="084e7-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="084e7-179">請參閱 [疑難排解](app-insights-troubleshoot-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="084e7-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="084e7-180">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="084e7-180">Publish your app</span></span>
<span data-ttu-id="084e7-181">現在，將您的應用程式 tooyour 伺服器部署或 tooAzure 和監看式 hello 資料會累積。</span><span class="sxs-lookup"><span data-stu-id="084e7-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![使用 Visual Studio toopublish 您的應用程式](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="084e7-183">當您在偵錯模式執行時，以便您應該會看到資料出現在數秒內加速遙測 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="084e7-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="084e7-184">以發行組態部署應用程式時，資料累積會較為緩慢。</span><span class="sxs-lookup"><span data-stu-id="084e7-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="084e7-185">之後您發佈 tooyour 伺服器的任何資料嗎？</span><span class="sxs-lookup"><span data-stu-id="084e7-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="084e7-186">請在您的伺服器防火牆中，開啟連出流量的連接埠。</span><span class="sxs-lookup"><span data-stu-id="084e7-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="084e7-187">請參閱[本頁](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses)hello 清單的所需的位址</span><span class="sxs-lookup"><span data-stu-id="084e7-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="084e7-188">組建伺服器發生問題？</span><span class="sxs-lookup"><span data-stu-id="084e7-188">Trouble on your build server?</span></span>
<span data-ttu-id="084e7-189">請參閱 [此疑難排解項目](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild)。</span><span class="sxs-lookup"><span data-stu-id="084e7-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="084e7-190">如果您的應用程式會產生大量的遙測，hello 調整取樣模組將會自動減少 hello 磁碟區所傳送的 toohello 入口網站傳送代表性數部分的事件。</span><span class="sxs-lookup"><span data-stu-id="084e7-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="084e7-191">不過，事件是相關的 toohello 相同的要求會被選取或取消選取此選項為群組，如此您可以瀏覽相關的事件之間。</span><span class="sxs-lookup"><span data-stu-id="084e7-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="084e7-192">[了解取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="084e7-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="084e7-193">影片</span><span class="sxs-lookup"><span data-stu-id="084e7-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="084e7-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="084e7-194">Next steps</span></span>
* <span data-ttu-id="084e7-195">[新增更多的遙測](app-insights-asp-net-more.md)tooget hello 完整 360 度檢視您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="084e7-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

