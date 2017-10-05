---
title: ".NET 應用程式的 Azure Application Insights 快照集偵錯工具 | Microsoft Docs"
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
ms.openlocfilehash: 56eba2ff7af228b3c44354ad43b384288b4e1972
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="61538-103">.NET 應用程式中的例外狀況偵錯快照集</span><span class="sxs-lookup"><span data-stu-id="61538-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="61538-104">發生例外狀況時，您可以自動從即時 Web 應用程式收集偵錯快照集。</span><span class="sxs-lookup"><span data-stu-id="61538-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="61538-105">快照集會顯示擲回例外狀況時原始程式碼和變數的狀態。</span><span class="sxs-lookup"><span data-stu-id="61538-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="61538-106">[Application Insights](app-insights-overview.md) 中的快照集偵錯工具 (預覽) 會監視 web 應用程式的例外狀況遙測。</span><span class="sxs-lookup"><span data-stu-id="61538-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="61538-107">它會收集前幾個擲回例外狀況的快照集，讓您取得診斷生產環境中問題所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="61538-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="61538-108">將[快照集收集器 NuGet 套件](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector)納入您的應用程式，並選擇性地設定 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 中的集合參數。快照集會顯示在 Application Insights 入口網站中的[例外狀況](app-insights-asp-net-exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="61538-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="61538-109">您可以檢視入口網站中的偵錯快照集，以查看呼叫堆疊並檢查每個呼叫堆疊框架的變數。</span><span class="sxs-lookup"><span data-stu-id="61538-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="61538-110">若要使用原始程式碼取得更強大的偵錯體驗，可[下載 Visual Studio 的快照集偵錯工具擴充功能](https://aka.ms/snapshotdebugger)，以 Visual Studio 2017 Enterprise 開啟快照集。</span><span class="sxs-lookup"><span data-stu-id="61538-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="61538-111">快照集集合適用於：</span><span class="sxs-lookup"><span data-stu-id="61538-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="61538-112">執行 .NET Framework 4.5 或更新版本的 .NET Framework 和 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="61538-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="61538-113">在 Windows 上執行的 .NET Core 2.0 和 ASP.NET Core 2.0 應用程式。</span><span class="sxs-lookup"><span data-stu-id="61538-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="61538-114">設定 ASP.NET 應用程式的快照集集合</span><span class="sxs-lookup"><span data-stu-id="61538-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="61538-115">如果您尚未這麼做，請[在 Web 應用程式中啟用 Application Insights](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="61538-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="61538-116">將 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet 套件納入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="61538-116">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="61538-117">檢閱套件已新增至 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) 的預設選項：</span><span class="sxs-lookup"><span data-stu-id="61538-117">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="61538-118">快照集只會收集向 Application Insights 回報的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="61538-118">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="61538-119">在某些情況下 (例如，舊版的 .NET 平台)，您可能需要[設定例外狀況集合](app-insights-asp-net-exceptions.md#exceptions)，才能在入口網站中查看快照集的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="61538-119">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="61538-120">設定 ASP.NET Core 2.0 應用程式的快照集集合</span><span class="sxs-lookup"><span data-stu-id="61538-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="61538-121">如果您尚未這麼做，請[在 ASP.NET Core Web 應用程式中啟用 Application Insights](app-insights-asp-net-core.md)。</span><span class="sxs-lookup"><span data-stu-id="61538-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="61538-122">將 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet 套件納入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="61538-122">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="61538-123">修改您應用程式的 `Startup` 類別中的`ConfigureServices` 方法，以新增快照集收集器的遙測處理器。</span><span class="sxs-lookup"><span data-stu-id="61538-123">Modify the `ConfigureServices` method in your application's `Startup` class to add the Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="61538-124">您應新增的程式碼取決於參考的 Microsoft.ApplicationInsights.ASPNETCore NuGet 套件版本。</span><span class="sxs-lookup"><span data-stu-id="61538-124">The code you should add depends on the referenced version of the Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="61538-125">對於 Microsoft.ApplicationInsights.AspNetCore 2.1.0，新增：</span><span class="sxs-lookup"><span data-stu-id="61538-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="61538-126">對於 Microsoft.ApplicationInsights.AspNetCore 2.1.1，新增：</span><span class="sxs-lookup"><span data-stu-id="61538-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
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

       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="61538-127">設定其他 .NET 應用程式的快照集集合</span><span class="sxs-lookup"><span data-stu-id="61538-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="61538-128">如果您的應用程式尚未使用 Application Insights 檢測，請從[啟用 Application Insights 及設定檢測金鑰](app-insights-windows-desktop.md)著手。</span><span class="sxs-lookup"><span data-stu-id="61538-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="61538-129">在您的應用程式中新增 [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="61538-129">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="61538-130">快照集只會收集向 Application Insights 回報的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="61538-130">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="61538-131">您可能需要修改程式碼才能回報例外狀況。</span><span class="sxs-lookup"><span data-stu-id="61538-131">You may need to modify your code to report them.</span></span> <span data-ttu-id="61538-132">例外狀況處理程式碼取決於應用程式的結構，但有一個範例如下：</span><span class="sxs-lookup"><span data-stu-id="61538-132">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="61538-133">授與權限</span><span class="sxs-lookup"><span data-stu-id="61538-133">Grant permissions</span></span>

<span data-ttu-id="61538-134">Azure 訂用帳戶的擁有者可以檢查快照集。</span><span class="sxs-lookup"><span data-stu-id="61538-134">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="61538-135">其他使用者必須由擁有者授與權限。</span><span class="sxs-lookup"><span data-stu-id="61538-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="61538-136">若要授與權限，請指派 `Application Insights Snapshot Debugger` 角色給要檢查快照集的使用者。</span><span class="sxs-lookup"><span data-stu-id="61538-136">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="61538-137">這個角色可以由目標 Application Insights 資源或其資源群組或訂用帳戶的訂用帳戶擁有者，指派給個別使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="61538-137">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="61538-138">開啟 [存取控制] \(IAM) 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61538-138">Open the Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="61538-139">按一下 [+新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="61538-139">Click the +Add button.</span></span>
1. <span data-ttu-id="61538-140">從 [角色] 下拉式清單中選取 Application Insights 快照集偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="61538-140">Select Application Insights Snapshot Debugger from the Roles drop-down list.</span></span>
1. <span data-ttu-id="61538-141">搜尋並輸入要新增的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="61538-141">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="61538-142">按一下 [儲存] 按鈕，將使用者新增至角色。</span><span class="sxs-lookup"><span data-stu-id="61538-142">Click the Save button to add the user to the role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="61538-143">快照集可能會在變數和參數值中包含個人和其他機密資訊。</span><span class="sxs-lookup"><span data-stu-id="61538-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="61538-144">Application Insights 入口網站中的偵錯快照集</span><span class="sxs-lookup"><span data-stu-id="61538-144">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="61538-145">如果快照集可用於指定的例外狀況或問題識別碼，則 Application Insights 入口網站中的[例外狀況](app-insights-asp-net-exceptions.md)會出現 [開啟偵錯快照集] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="61538-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![例外狀況的 [開啟偵錯快照集] 按鈕](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="61538-147">在 [偵錯快照集] 檢視中，您會看到呼叫堆疊和變數窗格。</span><span class="sxs-lookup"><span data-stu-id="61538-147">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="61538-148">當您在 [呼叫堆疊] 窗格中選取呼叫堆疊的框架時，您可以檢視 [變數] 窗格中的本機變數和該函式呼叫的參數。</span><span class="sxs-lookup"><span data-stu-id="61538-148">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![檢視入口網站中的偵錯快照集](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="61538-150">快照集可能包含機密資訊，依預設為不可檢視。</span><span class="sxs-lookup"><span data-stu-id="61538-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="61538-151">若要檢視快照集，您必須有指派給您的 `Application Insights Snapshot Debugger` 角色。</span><span class="sxs-lookup"><span data-stu-id="61538-151">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="61538-152">Visual Studio 2017 Enterprise 的偵錯快照集</span><span class="sxs-lookup"><span data-stu-id="61538-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="61538-153">按一下 [下載快照集] 按鈕，下載可利用 Visual Studio 2017 Enterprise 開啟的 `.diagsession` 檔案。</span><span class="sxs-lookup"><span data-stu-id="61538-153">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="61538-154">若要開啟 `.diagsession` 檔案，您必須先[下載並安裝 Visual Studio 的快照集偵錯工具擴充功能](https://aka.ms/snapshotdebugger)。</span><span class="sxs-lookup"><span data-stu-id="61538-154">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="61538-155">開啟快照集檔案之後，Visual Studio 中的 [小型傾印偵錯] 分頁隨即出現。</span><span class="sxs-lookup"><span data-stu-id="61538-155">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="61538-156">按一下 [偵錯 Managed 程式碼] 以開始偵錯快照集。</span><span class="sxs-lookup"><span data-stu-id="61538-156">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="61538-157">快照集會開啟至擲回例外狀況的程式碼行，您可將程序的目前狀態進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="61538-157">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![檢視 Visual Studio 中的偵錯快照集](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="61538-159">下載的快照集會包含您 Web 應用程式伺服器上找到的任何符號檔。</span><span class="sxs-lookup"><span data-stu-id="61538-159">The downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="61538-160">若要建立快照集資料與原始程式碼的關聯，就需要這些符號檔。</span><span class="sxs-lookup"><span data-stu-id="61538-160">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="61538-161">對於 App Service 應用程式，當您發佈 Web 應用程式時請務必啟用符號部署。</span><span class="sxs-lookup"><span data-stu-id="61538-161">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="61538-162">快照集運作方式</span><span class="sxs-lookup"><span data-stu-id="61538-162">How snapshots work</span></span>

<span data-ttu-id="61538-163">當您的應用程式啟動時，會建立個別的快照集上傳者程序，可針對快照集要求監視應用程式。</span><span class="sxs-lookup"><span data-stu-id="61538-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="61538-164">要求快照集時，會在大約 10 到 20 毫秒內製作執行程序的陰影副本。</span><span class="sxs-lookup"><span data-stu-id="61538-164">When a snapshot is requested, a shadow copy of the running process is made in about 10 to 20 minutes.</span></span> <span data-ttu-id="61538-165">接著會將陰影程序進行分析，且在主要程序繼續執行並將流量提供給使用者時，會建立快照集。</span><span class="sxs-lookup"><span data-stu-id="61538-165">The shadow process is then analyzed, and a snapshot is created while the main process continues to run and serve traffic to users.</span></span> <span data-ttu-id="61538-166">接著，會將快照集與檢視快照集所需的任何相關符號 (.pdb) 檔案一起上傳至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="61538-166">The snapshot is then uploaded to Application Insights along with any relevant symbol (.pdb) files that are needed to view the snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="61538-167">目前的限制</span><span class="sxs-lookup"><span data-stu-id="61538-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="61538-168">發佈符號</span><span class="sxs-lookup"><span data-stu-id="61538-168">Publish symbols</span></span>
<span data-ttu-id="61538-169">快照集偵錯工具需要符號檔出現在生產環境伺服器上，才可將變數解碼並提供 Visual Studio 中的偵錯體驗。</span><span class="sxs-lookup"><span data-stu-id="61538-169">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="61538-170">15.2 版 Visual Studio 2017 發佈至 App Service 時，預設會發佈版本組建的符號。</span><span class="sxs-lookup"><span data-stu-id="61538-170">The 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="61538-171">在舊版中，您必須將下列這一行新增至發佈設定檔 `.pubxml` 檔案，才會在發行模式中將符號發佈：</span><span class="sxs-lookup"><span data-stu-id="61538-171">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="61538-172">針對 Azure Compute 和其他類型，請確定符號檔案與主要應用程式 .dll 位於相同資料夾 (通常為 `wwwroot/bin`)，或可在目前的路徑使用。</span><span class="sxs-lookup"><span data-stu-id="61538-172">For Azure Compute and other types, ensure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="61538-173">最佳化的組建</span><span class="sxs-lookup"><span data-stu-id="61538-173">Optimized builds</span></span>
<span data-ttu-id="61538-174">在某些情況下，由於建置程序期間所套用的最佳化，使版本組建無法檢視本機變數。</span><span class="sxs-lookup"><span data-stu-id="61538-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during the build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="61538-175">疑難排解</span><span class="sxs-lookup"><span data-stu-id="61538-175">Troubleshooting</span></span>

<span data-ttu-id="61538-176">這些提示可協助您針對快照集偵錯工具的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="61538-176">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="61538-177">驗證檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="61538-177">Verify the instrumentation key</span></span>

<span data-ttu-id="61538-178">確定您在已發佈的應用程式中使用正確的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="61538-178">Make sure that you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="61538-179">通常，Application Insights 會從 ApplicationInsights.config 檔案讀取檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="61538-179">Usually, Application Insights reads the instrumentation key from the ApplicationInsights.config file.</span></span> <span data-ttu-id="61538-180">確認此值與您在入口網站中看到之 Application Insights 資源的檢測金鑰相同。</span><span class="sxs-lookup"><span data-stu-id="61538-180">Verify that the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="61538-181">請檢查上傳程式記錄檔</span><span class="sxs-lookup"><span data-stu-id="61538-181">Check the uploader logs</span></span>

<span data-ttu-id="61538-182">建立快照集之後，磁碟上會建立小型傾印檔案 (.dmp)。</span><span class="sxs-lookup"><span data-stu-id="61538-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="61538-183">個別的上載程序會採用該小型傾印檔案，並將它 (以及任何相關聯的 PDB) 上傳至 Application Insights 快照集偵錯工具儲存體。</span><span class="sxs-lookup"><span data-stu-id="61538-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="61538-184">成功上傳小型傾印之後，它就會從磁碟中刪除。</span><span class="sxs-lookup"><span data-stu-id="61538-184">After the minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="61538-185">小型傾印上傳程式的記錄檔會保留在磁碟上。</span><span class="sxs-lookup"><span data-stu-id="61538-185">The log files for the minidump uploader are retained on disk.</span></span> <span data-ttu-id="61538-186">在 App Service 環境中，您可以在 `D:\Home\LogFiles\Uploader_*.log` 中找到這些記錄。</span><span class="sxs-lookup"><span data-stu-id="61538-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="61538-187">使用 App Service 的 Kudu 管理網站來尋找這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="61538-187">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="61538-188">在 Azure 入口網站中開啟您的 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="61538-188">Open your App Service application in the Azure portal.</span></span>

2. <span data-ttu-id="61538-189">選取 [進階工具] 刀鋒視窗，或搜尋 [Kudu]。</span><span class="sxs-lookup"><span data-stu-id="61538-189">Select the **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="61538-190">按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="61538-190">Click **Go**.</span></span>
4. <span data-ttu-id="61538-191">在 [偵錯主控台] 下拉式清單方塊中，選取 [CMD]。</span><span class="sxs-lookup"><span data-stu-id="61538-191">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="61538-192">按一下 [LogFiles]。</span><span class="sxs-lookup"><span data-stu-id="61538-192">Click **LogFiles**.</span></span>

<span data-ttu-id="61538-193">您應會看到至少有一個檔案的名稱開頭為 `Uploader_` 且副檔名為 `.log`。</span><span class="sxs-lookup"><span data-stu-id="61538-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="61538-194">按一下適當的圖示，以下載任何記錄檔，或在瀏覽器中開啟它們。</span><span class="sxs-lookup"><span data-stu-id="61538-194">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="61538-195">檔案名稱包含電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="61538-195">The file name includes the machine name.</span></span> <span data-ttu-id="61538-196">如果 App Service 執行個體裝載於一部以上的電腦，每部電腦會有個別的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="61538-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="61538-197">當上傳程式偵測到新的小型傾印檔案時，該檔案會記錄在記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="61538-197">When the uploader detects a new minidump file, it is recorded in the log file.</span></span> <span data-ttu-id="61538-198">以下是成功上傳的範例︰</span><span class="sxs-lookup"><span data-stu-id="61538-198">Here's an example of a successful upload:</span></span>

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

<span data-ttu-id="61538-199">在上述範例中，檢測金鑰為 `c12a605e73c44346a984e00000000000`。</span><span class="sxs-lookup"><span data-stu-id="61538-199">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="61538-200">這個值應該符合您應用程式的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="61538-200">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="61538-201">小型傾印會與識別碼為 `139e411a23934dc0b9ea08a626db16c5` 的快照集相關聯。</span><span class="sxs-lookup"><span data-stu-id="61538-201">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="61538-202">您稍後可以使用這個識別碼，在 Application Insights Analytics 中找出相關聯的例外狀況遙測。</span><span class="sxs-lookup"><span data-stu-id="61538-202">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="61538-203">上載程式約每隔 15 分鐘掃描一次新的 PDB。</span><span class="sxs-lookup"><span data-stu-id="61538-203">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="61538-204">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="61538-204">Here's an example:</span></span>

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

<span data-ttu-id="61538-205">若為「未」裝載於 App Service 中的應用程式，上傳程式記錄位於與小型傾印相同的資料夾中：`%TEMP%\Dumps\<ikey>` (其中 `<ikey>` 是您的檢測金鑰)。</span><span class="sxs-lookup"><span data-stu-id="61538-205">For applications that are _not_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="61538-206">使用 Application Insights 搜尋來尋找快照集例外狀況的</span><span class="sxs-lookup"><span data-stu-id="61538-206">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="61538-207">建立快照集後，擲回中的例外狀況會以快照集識別碼標記。</span><span class="sxs-lookup"><span data-stu-id="61538-207">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="61538-208">向 Application Insights 回報例外狀況遙測後，快照集識別碼會納入為自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="61538-208">When the exception telemetry is reported to Application Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="61538-209">使用 Application Insights 中的 [搜尋] 刀鋒視窗，您可以找到具有 `ai.snapshot.id` 自訂屬性的所有遙測。</span><span class="sxs-lookup"><span data-stu-id="61538-209">Using the Search blade in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="61538-210">在 Azure 入口網站中瀏覽至您的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="61538-210">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="61538-211">按一下 [搜尋] 。</span><span class="sxs-lookup"><span data-stu-id="61538-211">Click **Search**.</span></span>
3. <span data-ttu-id="61538-212">在 [搜尋] 文字方塊中輸入 `ai.snapshot.id`，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="61538-212">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![在入口網站中使用快照集識別碼搜尋遙測](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="61538-214">如果此搜尋未傳回任何結果，則不會針對所選時間範圍中您的應用程式向 Application Insights 回報任何快照集。</span><span class="sxs-lookup"><span data-stu-id="61538-214">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="61538-215">若要搜尋從上傳程式記錄檔中的特定快照集識別碼，請在 [搜尋] 方塊中輸入該識別碼。</span><span class="sxs-lookup"><span data-stu-id="61538-215">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="61538-216">如果您找不到已上傳快照集的遙測，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="61538-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="61538-217">請驗證檢測金鑰，仔細檢查您查看的是正確的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="61538-217">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="61538-218">使用上傳程式記錄中的時間戳記，調整搜尋的時間範圍篩選條件以涵蓋該時間範圍。</span><span class="sxs-lookup"><span data-stu-id="61538-218">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="61538-219">如果仍未看到具有該快照集識別碼的例外狀況，則未向 Application Insights 回報此例外狀況遙測。</span><span class="sxs-lookup"><span data-stu-id="61538-219">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="61538-220">如果您的應用程式在採用快照集之後，但回報例外狀況遙測之前損毀，可能會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="61538-220">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="61538-221">在此情況下，檢查 `Diagnose and solve problems` 之下的 App Service 記錄，查看是否發生非預期的重新啟動或未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="61538-221">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61538-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61538-222">Next steps</span></span>

* <span data-ttu-id="61538-223">[在您的程式碼中設定 Snappoint](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) 以取得快照集，而不需等待例外狀況。</span><span class="sxs-lookup"><span data-stu-id="61538-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="61538-224">[診斷 Web Apps 中的例外狀況](app-insights-asp-net-exceptions.md)說明如何讓 Application Insights 看見更多的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="61538-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span> 
* <span data-ttu-id="61538-225">[智慧型偵測](app-insights-proactive-diagnostics.md)會自動探索效能異常。</span><span class="sxs-lookup"><span data-stu-id="61538-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
