---
title: "aaaAzure 偵錯工具 Insights 快照集應用程式的.NET 應用程式 |Microsoft 文件"
description: "在生產環境 .NET 應用程式中擲回例外狀況時，會自動收集偵錯快照集"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="b29b3-103">.NET 應用程式中的例外狀況偵錯快照集</span><span class="sxs-lookup"><span data-stu-id="b29b3-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="b29b3-104">發生例外狀況時，您可以自動從即時 Web 應用程式收集偵錯快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="b29b3-105">hello 快照顯示 hello 狀態的原始程式碼和變數在 hello 時刻 hello 例外狀況已擲回。</span><span class="sxs-lookup"><span data-stu-id="b29b3-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="b29b3-106">hello 快照偵錯工具 （預覽） 中[Azure Application Insights](app-insights-overview.md)監視 web 應用程式的例外狀況遙測。</span><span class="sxs-lookup"><span data-stu-id="b29b3-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="b29b3-107">在頂端擲回的例外狀況中，以便您擁有 hello 您需要在生產環境中的 toodiagnose 問題的資訊，它會收集快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="b29b3-108">包含 hello[快照集收集器 NuGet 套件](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)應用程式中，並選擇性地設定集合中的參數[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)。快照會顯示在[例外狀況](app-insights-asp-net-exceptions.md)hello Application Insights 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b29b3-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="b29b3-109">您可以檢視 hello 入口 toosee hello 呼叫堆疊中的偵錯快照集，然後檢查每個呼叫堆疊框架的變數。</span><span class="sxs-lookup"><span data-stu-id="b29b3-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="b29b3-110">tooget 功能更強大的偵錯體驗，與程式碼中，開啟快照集，與 Visual Studio 2017 企業[hello 快照偵錯工具擴充功能下載適用於 Visual Studio](https://aka.ms/snapshotdebugger)。</span><span class="sxs-lookup"><span data-stu-id="b29b3-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="b29b3-111">快照集集合適用於：</span><span class="sxs-lookup"><span data-stu-id="b29b3-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="b29b3-112">執行 .NET Framework 4.5 或更新版本的 .NET Framework 和 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b29b3-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="b29b3-113">在 Windows 上執行的 .NET Core 2.0 和 ASP.NET Core 2.0 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b29b3-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="b29b3-114">設定 ASP.NET 應用程式的快照集集合</span><span class="sxs-lookup"><span data-stu-id="b29b3-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="b29b3-115">如果您尚未這麼做，請[在 Web 應用程式中啟用 Application Insights](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="b29b3-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="b29b3-116">包含 hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)應用程式中的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="b29b3-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="b29b3-117">檢閱 hello hello 太加入封裝的預設選項[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="b29b3-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="b29b3-118">只有在例外狀況會報告的 tooApplication Insights 收集快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="b29b3-119">在某些情況下 （例如，hello.NET 平台的較舊版本），您可能需要過[設定例外狀況收集](app-insights-asp-net-exceptions.md#exceptions)toosee 例外狀況，其 hello 入口網站中的快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="b29b3-120">設定 ASP.NET Core 2.0 應用程式的快照集集合</span><span class="sxs-lookup"><span data-stu-id="b29b3-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="b29b3-121">如果您尚未這麼做，請[在 ASP.NET Core Web 應用程式中啟用 Application Insights](app-insights-asp-net-core.md)。</span><span class="sxs-lookup"><span data-stu-id="b29b3-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="b29b3-122">包含 hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)應用程式中的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="b29b3-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="b29b3-123">修改 hello`ConfigureServices`應用程式中的方法`Startup`類別 tooadd hello 快照集收集器的遙測處理器。</span><span class="sxs-lookup"><span data-stu-id="b29b3-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="b29b3-124">應加入的 hello 程式碼取決於 hello 參考 hello Microsoft.ApplicationInsights.ASPNETCore NuGet 封裝版本。</span><span class="sxs-lookup"><span data-stu-id="b29b3-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="b29b3-125">對於 Microsoft.ApplicationInsights.AspNetCore 2.1.0，新增：</span><span class="sxs-lookup"><span data-stu-id="b29b3-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="b29b3-126">對於 Microsoft.ApplicationInsights.AspNetCore 2.1.1，新增：</span><span class="sxs-lookup"><span data-stu-id="b29b3-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="b29b3-127">設定其他 .NET 應用程式的快照集集合</span><span class="sxs-lookup"><span data-stu-id="b29b3-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="b29b3-128">如果您的應用程式已不使用 Application Insights 檢測，以開始使用[啟用 Application Insights 和設定 hello 檢測金鑰](app-insights-windows-desktop.md)。</span><span class="sxs-lookup"><span data-stu-id="b29b3-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="b29b3-129">新增 hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)應用程式中的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="b29b3-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="b29b3-130">只有在例外狀況會報告的 tooApplication Insights 收集快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="b29b3-131">您可能需要 toomodify 程式碼 tooreport 它們。</span><span class="sxs-lookup"><span data-stu-id="b29b3-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="b29b3-132">hello 例外狀況處理程式碼主要取決於應用程式的 hello 結構，但是範例如下：</span><span class="sxs-lookup"><span data-stu-id="b29b3-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="b29b3-133">授與權限</span><span class="sxs-lookup"><span data-stu-id="b29b3-133">Grant permissions</span></span>

<span data-ttu-id="b29b3-134">Hello Azure 訂用帳戶的擁有者可以檢查快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="b29b3-135">其他使用者必須由擁有者授與權限。</span><span class="sxs-lookup"><span data-stu-id="b29b3-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="b29b3-136">toogrant 權限，指派 hello`Application Insights Snapshot Debugger`角色 toousers 人員將會檢查快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="b29b3-137">Tooindividual 使用者或群組由 hello 目標 Application Insights 資源的訂用帳戶擁有者或其資源群組或訂用帳戶，可以指派這個角色。</span><span class="sxs-lookup"><span data-stu-id="b29b3-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="b29b3-138">開啟 hello 存取控制 (IAM) 分頁。</span><span class="sxs-lookup"><span data-stu-id="b29b3-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="b29b3-139">按一下 hello + 新增 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b29b3-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="b29b3-140">從 hello 角色下拉式清單中選取應用程式 Insights 快照偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="b29b3-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="b29b3-141">搜尋並輸入 hello 使用者 tooadd 的名稱。</span><span class="sxs-lookup"><span data-stu-id="b29b3-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="b29b3-142">按一下 hello 儲存按鈕 tooadd hello 使用者 toohello 角色。</span><span class="sxs-lookup"><span data-stu-id="b29b3-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="b29b3-143">快照集可能會在變數和參數值中包含個人和其他機密資訊。</span><span class="sxs-lookup"><span data-stu-id="b29b3-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="b29b3-144">偵錯 hello Application Insights 入口網站中的快照集</span><span class="sxs-lookup"><span data-stu-id="b29b3-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="b29b3-145">如果快照集是用於指定的例外狀況或問題識別碼、**開啟偵錯快照集**按鈕是否出現在 hello[例外狀況](app-insights-asp-net-exceptions.md)hello Application Insights 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b29b3-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![例外狀況的 [開啟偵錯快照集] 按鈕](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="b29b3-147">在 [hello 偵錯快照檢視中，您會看到呼叫堆疊] 和 [變數] 窗格。</span><span class="sxs-lookup"><span data-stu-id="b29b3-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="b29b3-148">當您選取在 hello 呼叫堆疊 窗格中堆疊框架的 hello 呼叫、 您可以檢視本機變數和參數，該函式呼叫 hello 變數 窗格中。</span><span class="sxs-lookup"><span data-stu-id="b29b3-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Hello 入口網站中的檢視進行偵錯快照集](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="b29b3-150">快照集可能包含機密資訊，依預設為不可檢視。</span><span class="sxs-lookup"><span data-stu-id="b29b3-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="b29b3-151">tooview 快照集，您必須擁有 hello `Application Insights Snapshot Debugger` tooyou 指派角色。</span><span class="sxs-lookup"><span data-stu-id="b29b3-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="b29b3-152">Visual Studio 2017 Enterprise 的偵錯快照集</span><span class="sxs-lookup"><span data-stu-id="b29b3-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="b29b3-153">按一下 hello**下載快照集**按鈕 toodownload`.diagsession`檔案，可以開啟 Visual Studio 2017 Enterprise。</span><span class="sxs-lookup"><span data-stu-id="b29b3-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="b29b3-154">tooopen hello`.diagsession`檔案中，您必須先[下載並安裝 Visual Studio hello 快照 Debugger extension](https://aka.ms/snapshotdebugger)。</span><span class="sxs-lookup"><span data-stu-id="b29b3-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="b29b3-155">開啟 hello 快照集檔案之後，Visual Studio 中的 hello 小型傾印偵錯頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="b29b3-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="b29b3-156">按一下**偵錯 Managed 程式碼**toostart 偵錯 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="b29b3-157">hello 快照開啟 toohello 其中 hello 擲回例外狀況，讓您可以偵錯 hello hello 程序目前狀態的程式碼行。</span><span class="sxs-lookup"><span data-stu-id="b29b3-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![檢視 Visual Studio 中的偵錯快照集](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="b29b3-159">hello 下載快照集包含您的 web 應用程式伺服器找不到任何符號檔。</span><span class="sxs-lookup"><span data-stu-id="b29b3-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="b29b3-160">這些符號檔案是含有原始程式碼的必要的 tooassociate 快照集資料。</span><span class="sxs-lookup"><span data-stu-id="b29b3-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="b29b3-161">當您發行 web 應用程式時，App Service 應用程式，請確定 tooenable 符號部署。</span><span class="sxs-lookup"><span data-stu-id="b29b3-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="b29b3-162">快照集運作方式</span><span class="sxs-lookup"><span data-stu-id="b29b3-162">How snapshots work</span></span>

<span data-ttu-id="b29b3-163">當您的應用程式啟動時，會建立個別的快照集上傳者程序，可針對快照集要求監視應用程式。</span><span class="sxs-lookup"><span data-stu-id="b29b3-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="b29b3-164">要求快照集時，執行程序的 hello 的陰影複製會以大約 10 個 too20 分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="b29b3-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="b29b3-165">然後分析 hello 陰影程序，並建立同時 hello 主要處理序會繼續 toorun，及做流量 toousers 快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="b29b3-166">hello 快照集則以及任何相關符號 (.pdb) 檔上傳的 tooApplication Insights 需要 tooview hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="b29b3-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="b29b3-167">目前的限制</span><span class="sxs-lookup"><span data-stu-id="b29b3-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="b29b3-168">發佈符號</span><span class="sxs-lookup"><span data-stu-id="b29b3-168">Publish symbols</span></span>
<span data-ttu-id="b29b3-169">hello 快照偵錯工具需要符號檔 hello 實際執行伺服器 toodecode 變數和 tooprovide Visual Studio 中的偵錯經驗。</span><span class="sxs-lookup"><span data-stu-id="b29b3-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="b29b3-170">hello 15.2 版本的 Visual Studio 2017 發佈符號發行組建的預設發佈之後 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="b29b3-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="b29b3-171">在舊版中，您需要 tooadd hello 下列行 tooyour 發行設定檔`.pubxml`檔案，所以會發行在發行模式中的符號：</span><span class="sxs-lookup"><span data-stu-id="b29b3-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="b29b3-172">針對 Azure 計算和其他類型，請確定 hello 符號檔位於 hello hello 主應用程式.dll 的相同的資料夾 (通常`wwwroot/bin`) 或可用 hello 目前路徑上。</span><span class="sxs-lookup"><span data-stu-id="b29b3-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="b29b3-173">最佳化的組建</span><span class="sxs-lookup"><span data-stu-id="b29b3-173">Optimized builds</span></span>
<span data-ttu-id="b29b3-174">在某些情況下，本機變數無法檢視版本 」 組建中因為 hello 建置程序期間套用的最佳化。</span><span class="sxs-lookup"><span data-stu-id="b29b3-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b29b3-175">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b29b3-175">Troubleshooting</span></span>

<span data-ttu-id="b29b3-176">這些提示可協助您疑難排解問題 hello 快照偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="b29b3-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="b29b3-177">確認 hello 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="b29b3-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="b29b3-178">請確定您在已發行應用程式中使用 hello 正確的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="b29b3-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="b29b3-179">通常，Application Insights 會從 hello ApplicationInsights.config 檔案讀取 hello 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="b29b3-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="b29b3-180">請確認 hello 值為 hello 相同為 hello Application Insights 資源，請參閱 hello 入口網站中的 hello 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="b29b3-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="b29b3-181">請檢查 hello 上載程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="b29b3-181">Check hello uploader logs</span></span>

<span data-ttu-id="b29b3-182">建立快照集之後，磁碟上會建立小型傾印檔案 (.dmp)。</span><span class="sxs-lookup"><span data-stu-id="b29b3-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="b29b3-183">個別上載程序會採用該小型傾印檔案，並將它，以及任何相關聯的 Pdb tooApplication Insights 快照偵錯工具的儲存體上傳。</span><span class="sxs-lookup"><span data-stu-id="b29b3-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="b29b3-184">Hello 小型傾印已上傳成功之後，它會從磁碟中刪除。</span><span class="sxs-lookup"><span data-stu-id="b29b3-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="b29b3-185">hello hello 小型傾印上載程式記錄檔會保留在磁碟上。</span><span class="sxs-lookup"><span data-stu-id="b29b3-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="b29b3-186">在 App Service 環境中，您可以在 `D:\Home\LogFiles\Uploader_*.log` 中找到這些記錄。</span><span class="sxs-lookup"><span data-stu-id="b29b3-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="b29b3-187">使用 hello Kudu 管理網站的應用程式服務 toofind 這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b29b3-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="b29b3-188">Hello Azure 入口網站中開啟您的 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b29b3-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="b29b3-189">選取 hello**進階工具**刀鋒視窗中或搜尋**Kudu**。</span><span class="sxs-lookup"><span data-stu-id="b29b3-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="b29b3-190">按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="b29b3-190">Click **Go**.</span></span>
4. <span data-ttu-id="b29b3-191">在 hello**偵錯主控台**下拉式清單方塊中，選取**CMD**。</span><span class="sxs-lookup"><span data-stu-id="b29b3-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="b29b3-192">按一下 [LogFiles]。</span><span class="sxs-lookup"><span data-stu-id="b29b3-192">Click **LogFiles**.</span></span>

<span data-ttu-id="b29b3-193">您應會看到至少有一個檔案的名稱開頭為 `Uploader_` 且副檔名為 `.log`。</span><span class="sxs-lookup"><span data-stu-id="b29b3-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="b29b3-194">按一下 hello 合適的圖示 toodownload 任何記錄檔，或在瀏覽器中開啟它們。</span><span class="sxs-lookup"><span data-stu-id="b29b3-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="b29b3-195">hello 檔案名稱包含 hello 機器名稱。</span><span class="sxs-lookup"><span data-stu-id="b29b3-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="b29b3-196">如果 App Service 執行個體裝載於一部以上的電腦，每部電腦會有個別的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b29b3-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="b29b3-197">當 hello 上載程式偵測到新的小型傾印檔案時，它會記錄在 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b29b3-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="b29b3-198">以下是成功上傳的範例︰</span><span class="sxs-lookup"><span data-stu-id="b29b3-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="b29b3-199">Hello 前一個範例中的 hello 檢測金鑰是`c12a605e73c44346a984e00000000000`。</span><span class="sxs-lookup"><span data-stu-id="b29b3-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="b29b3-200">這個值應該符合您的應用程式的 hello 檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="b29b3-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="b29b3-201">hello 小型傾印是相關聯的快照集識別碼 hello `139e411a23934dc0b9ea08a626db16c5`。</span><span class="sxs-lookup"><span data-stu-id="b29b3-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="b29b3-202">您可以使用此識別碼更新 toolocate hello 相關聯的應用程式 Insights 分析中的例外狀況遙測。</span><span class="sxs-lookup"><span data-stu-id="b29b3-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="b29b3-203">hello 上載程式會掃描一次每隔 15 分鐘有關新的 Pdb。</span><span class="sxs-lookup"><span data-stu-id="b29b3-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="b29b3-204">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="b29b3-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="b29b3-205">應用程式_不_裝載在 App Service 中，hello 上載程式記錄檔位於 hello hello 小型傾印與相同的資料夾： `%TEMP%\Dumps\<ikey>` (其中`<ikey>`是您的檢測金鑰)。</span><span class="sxs-lookup"><span data-stu-id="b29b3-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="b29b3-206">使用 Application Insights 搜尋 toofind 例外狀況，其快照集</span><span class="sxs-lookup"><span data-stu-id="b29b3-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="b29b3-207">建立快照集時，擲回例外狀況的 hello 會標記為快照集識別碼。</span><span class="sxs-lookup"><span data-stu-id="b29b3-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="b29b3-208">報告的 tooApplication Insights hello 例外狀況遙測時，該快照集識別碼會當做自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="b29b3-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="b29b3-209">使用 Application Insights 中的 hello 搜尋刀鋒視窗，您可以找到以 hello 的所有遙測`ai.snapshot.id`自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="b29b3-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="b29b3-210">瀏覽 tooyour hello Azure 入口網站中的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="b29b3-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="b29b3-211">按一下 [搜尋] 。</span><span class="sxs-lookup"><span data-stu-id="b29b3-211">Click **Search**.</span></span>
3. <span data-ttu-id="b29b3-212">型別`ai.snapshot.id`在 hello 搜尋 文字方塊中，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="b29b3-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![搜尋具有快照集識別碼 hello 入口網站中的遙測](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="b29b3-214">此搜尋會不傳回任何結果，如果沒有快照集已回報的 tooApplication Insights hello 選取時間範圍內的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b29b3-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="b29b3-215">toosearch hello 上載程式記錄檔，從特定的快照集識別碼 hello 搜尋方塊中輸入該識別碼。</span><span class="sxs-lookup"><span data-stu-id="b29b3-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="b29b3-216">如果您找不到已上傳快照集的遙測，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b29b3-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="b29b3-217">請仔細檢查您所看到的 hello 右 Application Insights 資源 hello 檢測金鑰進行驗證。</span><span class="sxs-lookup"><span data-stu-id="b29b3-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="b29b3-218">使用 hello 上載程式記錄檔中的 hello 時間戳記，調整的 hello 搜尋 toocover hello 時間範圍篩選該時間範圍。</span><span class="sxs-lookup"><span data-stu-id="b29b3-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="b29b3-219">如果仍然沒有看到該快照集識別碼例外狀況，hello 例外狀況遙測未回報的 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="b29b3-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="b29b3-220">如果您的應用程式當機之後花費 hello 快照集，但 hello 例外狀況遙測報告它之前，可能會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="b29b3-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="b29b3-221">在此情況下，請檢查應用程式服務會記錄下的 hello `Diagnose and solve problems` toosee 如果發生非預期重新啟動或未處理例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b29b3-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b29b3-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b29b3-222">Next steps</span></span>

* <span data-ttu-id="b29b3-223">[在您的程式碼中設定 snappoints](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget 快照集，而不需等待例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b29b3-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="b29b3-224">[診斷 web 應用程式中的例外狀況](app-insights-asp-net-exceptions.md)說明如何 toomake 詳細例外狀況顯示 tooApplication 深入資訊。</span><span class="sxs-lookup"><span data-stu-id="b29b3-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="b29b3-225">[智慧型偵測](app-insights-proactive-diagnostics.md)會自動探索效能異常。</span><span class="sxs-lookup"><span data-stu-id="b29b3-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
