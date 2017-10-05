---
title: "使用 Application Insights 來分析 Azure 上的即時 Web 應用程式 | Microsoft Docs"
description: "使用低資源使用量的分析工具來找出 Web 伺服器程式碼中的最忙碌路徑。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: ff39f9a84b86c14859aaee50ee368643fb2848ea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a><span data-ttu-id="cbf9d-103">使用 Application Insights 來分析即時 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="cbf9d-103">Profiling live Azure web apps with Application Insights</span></span>

<span data-ttu-id="cbf9d-104">Application Insights 的這項功能在應用程式服務為 GA，在 Compute 為預覽中。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-104">*This feature of Application Insights is GA for App Services and in preview for Compute.*</span></span>

<span data-ttu-id="cbf9d-105">使用 [Azure Application Insights](app-insights-overview.md) 的分析工具來了解即時 Web 應用程式中的每個方法各使用了多少時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-105">Find out how much time is spent in each method in your live web application by using the profiling tool of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="cbf9d-106">此工具會顯示應用程式所提供之即時要求的詳細設定檔，並醒目提示使用最多時間的「最忙碌路徑」。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-106">It shows you detailed profiles of live requests that were served by your app, and highlights the 'hot path' that is using the most time.</span></span> <span data-ttu-id="cbf9d-107">它會自動選取具有不同回應時間的範例。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-107">It automatically selects examples that have different response times.</span></span> <span data-ttu-id="cbf9d-108">分析工具會使用各種技術來盡量減少系統負荷。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-108">The profiler uses various techniques to minimize overhead.</span></span>

<span data-ttu-id="cbf9d-109">分析工具目前適用於在 Azure App Services (至少必須是基本定價層) 上執行的 ASP.NET Web 應用程式 </span><span class="sxs-lookup"><span data-stu-id="cbf9d-109">The profiler currently works for ASP.NET web apps running on Azure App Services, in at least the Basic pricing tier.</span></span> 

<a id="installation"></a>
## <a name="enable-the-profiler"></a><span data-ttu-id="cbf9d-110">啟用分析工具</span><span class="sxs-lookup"><span data-stu-id="cbf9d-110">Enable the profiler</span></span>

<span data-ttu-id="cbf9d-111">在程式碼中[安裝 Application Insights](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-111">[Install Application Insights](app-insights-asp-net.md) in your code.</span></span> <span data-ttu-id="cbf9d-112">如果已安裝，請確定您擁有的是最新版本 </span><span class="sxs-lookup"><span data-stu-id="cbf9d-112">If it's already installed, make sure you have the latest version.</span></span> <span data-ttu-id="cbf9d-113">(若要進行安裝，請在 [方案總管] 中以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-113">(To do this, right-click your project in Solution Explorer, and choose Manage NuGet packages.</span></span> <span data-ttu-id="cbf9d-114">選取 [更新] 並更新所有套件)。重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-114">Select Updates and update all packages.) Re-deploy your app.</span></span>

<span data-ttu-id="cbf9d-115">您使用的是 ASP.NET Core 嗎？[請查看這裡](#aspnetcore)。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-115">*Using ASP.NET Core? [Check here](#aspnetcore).*</span></span>

<span data-ttu-id="cbf9d-116">在 [https://portal.azure.com](https://portal.azure.com) 中，為您的 Web 應用程式開啟 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-116">In [https://portal.azure.com](https://portal.azure.com), open the Application Insights resource for your web app.</span></span> <span data-ttu-id="cbf9d-117">開啟 [效能] 然後按一下 [啟用 Application Insights 分析工具...]。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-117">Open **Performance** and click **Enable Application Insights Profiler...**.</span></span>

![按一下 [啟用程式碼分析工具] 橫幅][enable-profiler-banner]

<span data-ttu-id="cbf9d-119">或者，您隨時可以按一下 [設定] 來檢視狀態、啟用或停用分析工具。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-119">Alternatively, you can always click **Configure** to view status, enable, or disable the Profiler.</span></span>

![在 [效能] 刀鋒視窗中，按一下 [設定]][performance-blade]

<span data-ttu-id="cbf9d-121">使用 Application Insights 設定的 Web Apps 會列在 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-121">Web apps that are configured with Application Insights are listed on Configure blade.</span></span> <span data-ttu-id="cbf9d-122">請視需要依照指示來安裝分析工具代理程式。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-122">Follow instructions to install the Profiler agent if needed.</span></span> <span data-ttu-id="cbf9d-123">如果尚未使用 Application Insights 設定任何 Web 應用程式，請按一下 [新增連結的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-123">If no web app is configured with Application Insights yet, click *Add Linked Apps*.</span></span>

<span data-ttu-id="cbf9d-124">使用 [設定] 刀鋒視窗中的 [啟用分析工具] 或 [停用分析工具] 按鈕來控制所有連結的 Web Apps 之分析工具。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-124">Use the *Enable Profiler* or *Disable Profiler* buttons in the Configure blade to control the Profiler on all your linked web apps.</span></span>



![設定刀鋒視窗][linked app services]

<span data-ttu-id="cbf9d-126">若要停止或重新啟動個別 App Service 執行個體的分析工具，您可以在 [App Service 資源] 的 [Web 作業] 中找到它。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-126">To stop or restart the profiler for an individual App Service instance, you'll find it **in the App Service resource**, in **Web Jobs**.</span></span> <span data-ttu-id="cbf9d-127">若要刪除它，請在 [擴充功能] 底下查看。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-127">To delete it, look under **Extensions**.</span></span>

![停用 web 作業的分析工具][disable-profiler-webjob]

<span data-ttu-id="cbf9d-129">我們建議您將 Web Apps 上的分析工具啟用，儘速找出任何的效能問題。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-129">We recommend that you have the Profiler enabled on all your web apps to discover any performance issues as soon as possible.</span></span>

<span data-ttu-id="cbf9d-130">如果您使用 WebDeploy 來部署 Web 應用程式的變更，請確定您已排除 **App_Data** 資料夾，以免系統在部署期間刪除它。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-130">If you use WebDeploy to deploy changes to your web application, ensure that you exclude the **App_Data** folder from being deleted during deployment.</span></span> <span data-ttu-id="cbf9d-131">否則，當您下次將 Web 應用程式部署至 Azure 時，系統就會刪除分析工具擴充功能的檔案。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-131">Otherwise, the profiler extension's files will be deleted when you next deploy the web application to Azure.</span></span>

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a><span data-ttu-id="cbf9d-132">使用分析工具搭配 Azure VM 和 Compute 資源 (預覽)</span><span class="sxs-lookup"><span data-stu-id="cbf9d-132">Using profiler with Azure VMs and Compute resources (preview)</span></span>

<span data-ttu-id="cbf9d-133">當您[在執行階段啟用 Azure App Service 的 Application Insights](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights) 時，分析工具會自動提供使用。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-133">When you [enable Application Insights for Azure app services at run time](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), Profiler is automatically available.</span></span> <span data-ttu-id="cbf9d-134">(如果已啟用資源的 Application Insights，您可能需要透過 [設定] 精靈更新為最新版本。)</span><span class="sxs-lookup"><span data-stu-id="cbf9d-134">(If you already enabled Application Insights for the resource, you might need to update to the lates version through the **Configure** wizard.)</span></span>

<span data-ttu-id="cbf9d-135">現提供 [Azure Compute 資源的分析工具預覽版本](https://go.microsoft.com/fwlink/?linkid=848155)。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-135">There is a [preview version of the Profiler for Azure Compute resources](https://go.microsoft.com/fwlink/?linkid=848155).</span></span>


## <a name="limits"></a><span data-ttu-id="cbf9d-136">限制</span><span class="sxs-lookup"><span data-stu-id="cbf9d-136">Limits</span></span>

<span data-ttu-id="cbf9d-137">預設資料保留期為 5 天。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-137">The default data retention is 5 days.</span></span> <span data-ttu-id="cbf9d-138">每日擷取最多 10 GB。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-138">Maximum 10 GB ingested per day.</span></span>

<span data-ttu-id="cbf9d-139">分析工具服務不會收取費用。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-139">There is no charge for the profiler service.</span></span> <span data-ttu-id="cbf9d-140">Web 應用程式必須至少在應用程式服務的基本層中託管。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-140">Your web app must be hosted in at least the Basic tier of App Services.</span></span>

## <a name="viewing-profiler-data"></a><span data-ttu-id="cbf9d-141">檢視分析工具的資料</span><span class="sxs-lookup"><span data-stu-id="cbf9d-141">Viewing profiler data</span></span>

<span data-ttu-id="cbf9d-142">開啟 [效能] 刀鋒視窗，並向下捲動至作業清單。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-142">Open the Performance blade and scroll down to the operation list.</span></span>




![Application Insights 的 [效能] 刀鋒視窗 [範例] 資料行][performance-blade-examples]

<span data-ttu-id="cbf9d-144">資料表中有下列資料行：</span><span class="sxs-lookup"><span data-stu-id="cbf9d-144">The columns in the table are:</span></span>

* <span data-ttu-id="cbf9d-145">**計數** - 這些要求在刀鋒視窗之時間範圍內的數目。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-145">**Count** - The number of these requests in the time range of the blade.</span></span>
* <span data-ttu-id="cbf9d-146">**中位數** - 應用程式回應要求時一般會使用的時間長度。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-146">**Median** - The typical time your app takes to respond to a request.</span></span> <span data-ttu-id="cbf9d-147">在所有的回應中，有一半會快過此時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-147">Half of all responses were faster than this.</span></span>
* <span data-ttu-id="cbf9d-148">**第 95 個百分位數** - 95% 的回應會快過此時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-148">**95th percentile** 95% of responses were faster than this.</span></span> <span data-ttu-id="cbf9d-149">如果此數字和中位數差異極大，則表示應用程式可能有間歇性問題 </span><span class="sxs-lookup"><span data-stu-id="cbf9d-149">If this figure is very different from the median, there might be an intermittent problem with your app.</span></span> <span data-ttu-id="cbf9d-150">(或者，可能的解釋為有某者設計功能導致此結果，例如快取)。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-150">(Or it might be explained by a design feature such as caching.)</span></span>
* <span data-ttu-id="cbf9d-151">**範例** - 一個圖示，用來指出分析工具已擷取這項作業的堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-151">**Examples** - an icon indicates that the profiler has captured stack traces for this operation.</span></span>

<span data-ttu-id="cbf9d-152">按一下 [範例] 圖示就能開啟追蹤總管。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-152">Click the Examples icon to open the trace explorer.</span></span> <span data-ttu-id="cbf9d-153">此總管會顯示分析工具已擷取的數個範例，並依回應時間來分類。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-153">The explorer shows several samples that the profiler has captured, classified by response time.</span></span>

<span data-ttu-id="cbf9d-154">選取某個範例就會顯示要求在執行時所用時間的程式碼層級細目。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-154">Select a sample to show a code-level breakdown of time spent executing the request.</span></span>

![Application Insights 追蹤總管][trace-explorer]

<span data-ttu-id="cbf9d-156">[顯示最忙碌路徑] 會開啟最大的分葉節點，或者，至少也會是接近最大的節點。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-156">**Show hot path** opens the biggest leaf node, or at least something close.</span></span> <span data-ttu-id="cbf9d-157">在大部分情況下，這個節點會很接近效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-157">In most cases this node will be adjacent to a performance bottleneck.</span></span>



* <span data-ttu-id="cbf9d-158">**標籤**︰函式或事件的名稱。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-158">**Label**: The name of the function or event.</span></span> <span data-ttu-id="cbf9d-159">樹狀結構會混合顯示程式碼和發生的事件 (例如 SQL 和 http 事件)。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-159">The tree shows a mix of code and events that occurred (such as SQL and http events).</span></span> <span data-ttu-id="cbf9d-160">最上層事件代表要求整體的持續時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-160">The top event represents the overall request duration.</span></span>
* <span data-ttu-id="cbf9d-161">**經過**︰作業開始和結束之間的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-161">**Elapsed**: The time interval between the start of the operation and the end.</span></span>
* <span data-ttu-id="cbf9d-162">**何時**︰顯示函式/事件相對於其他函式的執行時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-162">**When**: Shows when the function/event was running in relation to other functions.</span></span>

## <a name="how-to-read-performance-data"></a><span data-ttu-id="cbf9d-163">如何讀取效能資料</span><span class="sxs-lookup"><span data-stu-id="cbf9d-163">How to read performance data</span></span>

<span data-ttu-id="cbf9d-164">Microsoft 服務分析工具會合併使用取樣方法和檢測功能來分析應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-164">Microsoft service profiler uses a combination of sampling method and instrumentation to analyze the performance of your application.</span></span>
<span data-ttu-id="cbf9d-165">當系統正在進行詳細的收集作業時，服務分析工具會對每個機器之 CPU 的指令指標進行取樣，頻率為每毫秒一次。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-165">When detailed collection is in progress, service profiler samples the instruction pointer of each of the machine's CPU in every millisecond.</span></span>
<span data-ttu-id="cbf9d-166">每此取樣都會擷取目前執行之執行緒的完整呼叫堆疊，以便獲得詳細而實用的資訊，來了解該執行緒在高低兩個抽象層執行了哪些作業。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-166">Each sample captures the complete call stack of the thread currently executing, giving detailed and useful information about what that thread was doing at both high and low levels of abstraction.</span></span> <span data-ttu-id="cbf9d-167">服務分析工具也會收集其他事件 (例如內容切換的事件，TPL 事件，以及執行緒集區事件) 來追蹤活動的關聯性和原因。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-167">Service profiler also collects other events such as context switching events, TPL events, and thread-pool events to track activity correlation and causality.</span></span>

<span data-ttu-id="cbf9d-168">時間表檢視中所顯示的呼叫堆疊是上述取樣和檢測的結果。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-168">The call stack shown in the timeline view is the result of the above sampling and instrumentation.</span></span> <span data-ttu-id="cbf9d-169">每個範例都會擷取執行緒的完整呼叫堆疊，因此範例中會包含 .NET Framework 的程式碼，以及您參考的其他架構。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-169">Because each sample captures the complete call stack of the thread, it includes code from the .NET framework, as well as other frameworks you reference.</span></span>

### <span data-ttu-id="cbf9d-170"><a id="jitnewobj"></a>物件配置 (`clr!JIT\_New or clr!JIT\_Newarr1`)</span><span class="sxs-lookup"><span data-stu-id="cbf9d-170"><a id="jitnewobj"></a>Object Allocation (`clr!JIT\_New or clr!JIT\_Newarr1`)</span></span>
<span data-ttu-id="cbf9d-171">`clr!JIT\_New and clr!JIT\_Newarr1` 是 .NET Framework 內的 Helper 函式，可從 Managed 堆積來配置記憶體。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-171">`clr!JIT\_New and clr!JIT\_Newarr1` are helper functions inside .NET framework that allocates memory from managed heap.</span></span> <span data-ttu-id="cbf9d-172">系統在配置物件時會叫用 `clr!JIT\_New`。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-172">`clr!JIT\_New` is invoked when an object is allocated.</span></span> <span data-ttu-id="cbf9d-173">系統在配置物件陣列時則會叫用 `clr!JIT\_Newarr1`。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-173">`clr!JIT\_Newarr1` is invoked when an object array is allocated.</span></span> <span data-ttu-id="cbf9d-174">這兩個函式的速度通常很快，應該不會花上多少時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-174">These two functions are typically very fast and should take relatively small amount of time.</span></span> <span data-ttu-id="cbf9d-175">如果您在時間表中看到 `clr!JIT\_New` 或 `clr!JIT\_Newarr1` 花了很久的時間，就表示程式碼可能配置了許多物件，並耗用了大量記憶體。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-175">If you see `clr!JIT\_New` or `clr!JIT\_Newarr1` take a substantial amount of time in your timeline, it's an indication that the code may be allocating many objects and consuming significant amount of memory.</span></span>

### <span data-ttu-id="cbf9d-176"><a id="theprestub"></a>載入程式碼 (`clr!ThePreStub`)</span><span class="sxs-lookup"><span data-stu-id="cbf9d-176"><a id="theprestub"></a>Loading Code (`clr!ThePreStub`)</span></span>
<span data-ttu-id="cbf9d-177">`clr!ThePreStub` 是 .NET Framework 內的 Helper 函式，可讓程式碼準備好進行第一次的執行。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-177">`clr!ThePreStub` is a helper function inside .NET framework that prepares the code to execute for the first time.</span></span> <span data-ttu-id="cbf9d-178">這通常包括但不限於 JIT (Just In Time) 編譯。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-178">This typically includes, but not limited to, JIT (Just In Time) compilation.</span></span> <span data-ttu-id="cbf9d-179">在程序的存留期內，每個 C# 方法最多只應該會叫用 `clr!ThePreStub` 一次。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-179">For each C# method, `clr!ThePreStub` should be invoked at most once during the lifetime of a process.</span></span>

<span data-ttu-id="cbf9d-180">如果您看到 `clr!ThePreStub` 花了很久的時間來處理要求，則表示該要求是第一個執行該方法的要求，因此 .NET Framework 執行階段要花很多時間來載入該方法。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-180">If you see `clr!ThePreStub` takes significant amount of time for a request, it indicates that request is the first one that executes that method, and the time for .NET framework runtime to load that method is significant.</span></span> <span data-ttu-id="cbf9d-181">您可以考慮使用準備程序來執行程式碼的這個部分，再讓使用者存取該程式碼，或考慮在您的組件上執行 NGen。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-181">You can consider a warm-up process that executes that portion of the code before your users access it, or consider running NGen on your assemblies.</span></span>

### <span data-ttu-id="cbf9d-182"><a id="lockcontention"></a>鎖定爭用 (`clr!JITutil\_MonContention` 或 `clr!JITutil\_MonEnterWorker`)</span><span class="sxs-lookup"><span data-stu-id="cbf9d-182"><a id="lockcontention"></a>Lock Contention (`clr!JITutil\_MonContention` or `clr!JITutil\_MonEnterWorker`)</span></span>
<span data-ttu-id="cbf9d-183">`clr!JITutil\_MonContention` 或 `clr!JITutil\_MonEnterWorker` 表示目前的執行緒正在等待系統釋放鎖定。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-183">`clr!JITutil\_MonContention` or `clr!JITutil\_MonEnterWorker` indicate the current thread is waiting for a lock to be released.</span></span> <span data-ttu-id="cbf9d-184">系統在執行 C# 鎖定陳述式、叫用 Monitor.Enter 方法或以 MethodImplOptions.Synchronized 屬性叫用方法時，常會出現此情形。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-184">This typically shows up when executing a C# lock statement, invoking Monitor.Enter method, or invoking a method with MethodImplOptions.Synchronized attribute.</span></span> <span data-ttu-id="cbf9d-185">當執行緒 A 取得鎖定但還未將其釋放之前，執行緒 B 就嘗試取得相同鎖定，系統一般就會發生鎖定爭用現象。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-185">Lock contention typically happens when thread A acquires a lock, and thread B tries to acquire the same lock before thread A releases it.</span></span>

### <span data-ttu-id="cbf9d-186"><a id="ngencold"></a>載入程式碼 (`[COLD]`)</span><span class="sxs-lookup"><span data-stu-id="cbf9d-186"><a id="ngencold"></a>Loading code (`[COLD]`)</span></span>
<span data-ttu-id="cbf9d-187">如果方法名稱包含 `[COLD]` (例如 `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`)，這表示 .NET Framework 執行階段所執行的程式碼尚未由<a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">特性指引最佳化</a>進行首次最佳化。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-187">If the method name contains `[COLD]`, such as `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, it means that the .NET framework runtime is executing code that is not optimized by <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">profile-guided optimization</a> for the first time.</span></span> <span data-ttu-id="cbf9d-188">每個方法最多只應該會在程序的存留期內顯示一次這個名稱。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-188">For each method, it should show up at most once during the lifetime of the process.</span></span>

<span data-ttu-id="cbf9d-189">如果某個要求在載入程式碼時花了很久的時間，就表示該要求是第一個在方法中執行這未最佳化部分的要求。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-189">If loading code takes significant amount of time for a request, it indicates that request is the first one to execute the unoptimized portion of the method.</span></span> <span data-ttu-id="cbf9d-190">您可以考慮使用準備程序來執行程式碼的這個部分，再讓使用者存取該程式碼。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-190">You can consider a warm up process that executes that portion of the code before your users access it.</span></span>

### <span data-ttu-id="cbf9d-191"><a id="httpclientsend"></a>傳送 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="cbf9d-191"><a id="httpclientsend"></a>Send HTTP Request</span></span>
<span data-ttu-id="cbf9d-192">`HttpClient.Send` 之類的方法表示程式碼正在等候 HTTP 要求完成。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-192">Methods such as `HttpClient.Send` indicate the code is waiting for a HTTP request to complete.</span></span>

### <span data-ttu-id="cbf9d-193"><a id="sqlcommand"></a>資料庫作業</span><span class="sxs-lookup"><span data-stu-id="cbf9d-193"><a id="sqlcommand"></a>Database Operation</span></span>
<span data-ttu-id="cbf9d-194">SqlCommand.Execute 之類的方法表示程式碼正在等候系統資料庫作業完成。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-194">Method such as SqlCommand.Execute indicates the code is waiting for a database operation to complete.</span></span>

### <span data-ttu-id="cbf9d-195"><a id="await"></a>等候 (`AWAIT\_TIME`)</span><span class="sxs-lookup"><span data-stu-id="cbf9d-195"><a id="await"></a>Waiting (`AWAIT\_TIME`)</span></span>
<span data-ttu-id="cbf9d-196">`AWAIT\_TIME` 表示程式碼正在等候另一個工作完成。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-196">`AWAIT\_TIME` indicates the code is waiting for another task to complete.</span></span> <span data-ttu-id="cbf9d-197">這通常會發生在 C# 'await' 陳述式。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-197">This typically happens with C# 'await' statement.</span></span> <span data-ttu-id="cbf9d-198">當程式碼執行 C# 'await' 時，執行緒會回溯控制權並將控制權交還給執行緒集區，而且系統不會將任何執行緒封鎖起來以等候 'await' 完成。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-198">When the code does a C# 'await', the thread unwinds and returns control to the thread-pool, and there is no thread that is blocked waiting for the 'await' to finish.</span></span> <span data-ttu-id="cbf9d-199">不過，就邏輯上來說，系統其實會將執行 await 的執行緒「封鎖」以等候作業完成。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-199">However, logically the thread that did the await is 'blocked' waiting for the operation to complete.</span></span> <span data-ttu-id="cbf9d-200">`AWAIT\_TIME` 表示為了等候工作完成而封鎖的時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-200">The `AWAIT\_TIME` indicates the blocked time waiting for the task to complete.</span></span>

### <span data-ttu-id="cbf9d-201"><a id="block"></a> 封鎖的時間</span><span class="sxs-lookup"><span data-stu-id="cbf9d-201"><a id="block"></a>Blocked Time</span></span>
<span data-ttu-id="cbf9d-202">`BLOCKED_TIME` 表示程式碼在等候另一項資源變成可用狀態，例如，等候同步處理物件、等候執行緒變成可用狀態，或等候要求完成。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-202">`BLOCKED_TIME` indicates the code is waiting for another resource to be available, such as waiting for a synchronization object, waiting for a thread to be available, or waiting for a request to finish.</span></span>

### <span data-ttu-id="cbf9d-203"><a id="cpu"></a>CPU 時間</span><span class="sxs-lookup"><span data-stu-id="cbf9d-203"><a id="cpu"></a>CPU Time</span></span>
<span data-ttu-id="cbf9d-204">CPU 正忙於執行指令。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-204">The CPU is busy executing the instructions.</span></span>

### <span data-ttu-id="cbf9d-205"><a id="disk"></a>磁碟時間</span><span class="sxs-lookup"><span data-stu-id="cbf9d-205"><a id="disk"></a>Disk Time</span></span>
<span data-ttu-id="cbf9d-206">應用程式正在執行磁碟作業。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-206">The application is performing disk operations.</span></span>

### <span data-ttu-id="cbf9d-207"><a id="network"></a>網路時間</span><span class="sxs-lookup"><span data-stu-id="cbf9d-207"><a id="network"></a>Network Time</span></span>
<span data-ttu-id="cbf9d-208">應用程式正在執行網路作業。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-208">The application is performing network operations.</span></span>

### <span data-ttu-id="cbf9d-209"><a id="when"></a>何時資料行</span><span class="sxs-lookup"><span data-stu-id="cbf9d-209"><a id="when"></a>When column</span></span>
<span data-ttu-id="cbf9d-210">這個視覺化資料行會顯示針對節點所收集的 INCLUSIVE 樣本如何隨著時間變化。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-210">This is a visualization of how the INCLUSIVE samples collected for a node vary over time.</span></span> <span data-ttu-id="cbf9d-211">要求的整個範圍會分成 32 個時間值區，而該節點的 INCLUSIVE 樣本則會累積到這 32 個值區。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-211">The total range of the request is divided into 32 time buckets and the inclusive samples for that node are accumulated into those 32 buckets.</span></span> <span data-ttu-id="cbf9d-212">接著，每個值區會以長條來表示，而長條的高度則代表換算後的值。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-212">Each bucket is then represented as a bar whose height represents a scaled value.</span></span> <span data-ttu-id="cbf9d-213">若節點標記為 `CPU_TIME` 或 `BLOCKED_TIME`，或是明顯與耗用資源 (CPU、磁碟、執行緒) 有關，長條就表示節點在該值區的一段時間內耗用了其中一項資源。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-213">For nodes marked `CPU_TIME` or `BLOCKED_TIME`, or where there is an obvious relationship of consuming a resource (cpu, disk, thread), the bar represents consuming one of those resources for the period of time of that bucket.</span></span> <span data-ttu-id="cbf9d-214">若您耗用多項資源，這些計量會大於 100%。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-214">For these metrics you can get greater than 100% by consuming multiple resources.</span></span> <span data-ttu-id="cbf9d-215">例如，通常來說，如果您在某個期間內使用兩個 CPU，計量會是 200%。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-215">For example, if on average you use two CPUs over an interval then you get 200%.</span></span>


## <span data-ttu-id="cbf9d-216"><a id="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="cbf9d-216"><a id="troubleshooting"></a>Troubleshooting</span></span>

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a><span data-ttu-id="cbf9d-217">如何知道 Application Insights 分析工具是否有執行？</span><span class="sxs-lookup"><span data-stu-id="cbf9d-217">How can I know whether Application Insights profiler is running?</span></span>

<span data-ttu-id="cbf9d-218">在 Web 應用程式中，分析工具會以連續性 Web 作業的形式來執行。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-218">The profiler runs as a continuous web job in Web App.</span></span> <span data-ttu-id="cbf9d-219">您可以在 https://portal.azure.com 中開啟 Web 應用程式資源，然後檢查 [Webjob] 刀鋒視窗中的「ApplicationInsightsProfiler」狀態。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-219">You can open the Web App resource in https://portal.azure.com and check "ApplicationInsightsProfiler" status in the WebJobs blade.</span></span> <span data-ttu-id="cbf9d-220">如果它沒有執行，請開啟 [記錄] 以進一步了解。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-220">If it isn't running, open **Logs** to find out more.</span></span>

### <a name="why-cant-i-find-any-stack-examples-even-though-the-profiler-is-running"></a><span data-ttu-id="cbf9d-221">為什麼分析工具明明已在執行，我卻找不到任何堆疊範例呢？</span><span class="sxs-lookup"><span data-stu-id="cbf9d-221">Why can't I find any stack examples even though the profiler is running?</span></span>

<span data-ttu-id="cbf9d-222">您可以檢查以下幾點。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-222">Here are a few things you can check.</span></span>

1. <span data-ttu-id="cbf9d-223">確定 Web App Service 方案服務方案至少是基本層。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-223">Make sure your Web App Service Plan is Basic tier and above.</span></span>
2. <span data-ttu-id="cbf9d-224">確定 Web 應用程式至少已啟用 Application Insights SDK 2.2 Beta 版。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-224">Make sure your Web App has Application Insights SDK 2.2 Beta and above enabled.</span></span>
3. <span data-ttu-id="cbf9d-225">確定 Web 應用程式的 APPINSIGHTS_INSTRUMENTATIONKEY 設定所擁有的檢測金鑰和 Application Insights SDK 所使用的金鑰相同。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-225">Make sure your Web App has the APPINSIGHTS_INSTRUMENTATIONKEY setting with the same instrumentation key used by Application Insights SDK.</span></span>
4. <span data-ttu-id="cbf9d-226">確定 Web 應用程式是在 .Net Framework 4.6 上執行。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-226">Make sure your Web App is running on .Net Framework 4.6.</span></span>
5. <span data-ttu-id="cbf9d-227">如果 Web 應用程式是 ASP.NET Core 應用程式，也請檢查[所需的相依性](#aspnetcore)。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-227">If it's an ASP.NET Core application, please also check [the required dependencies](#aspnetcore).</span></span>

<span data-ttu-id="cbf9d-228">在分析工具啟動之後，系統會有一段準備時間，分析工具會利用這段不長的時間積極收集幾項效能追蹤資料。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-228">After the profiler is started, there is a short warm-up period when the profiler actively collects several performance traces.</span></span> <span data-ttu-id="cbf9d-229">之後每隔一小時，分析工具會再花兩分鐘的時間收集效能追蹤資料。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-229">After that, the profiler collects performance traces for two minutes in every hour.</span></span>  

### <a name="i-was-using-azure-service-profiler-what-happened-to-it"></a><span data-ttu-id="cbf9d-230">我之前使用的是 Azure Service Profiler。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-230">I was using Azure Service Profiler.</span></span> <span data-ttu-id="cbf9d-231">它有什麼改變？</span><span class="sxs-lookup"><span data-stu-id="cbf9d-231">What happened to it?</span></span>  

<span data-ttu-id="cbf9d-232">當您啟用 Application Insights Profiler 時，Azure Service Profiler 代理程式就會停用。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-232">When you enable Application Insights Profiler, Azure Service Profiler agent is disabled.</span></span>

### <span data-ttu-id="cbf9d-233"><a id="double-counting"></a>平行執行緒重複計算</span><span class="sxs-lookup"><span data-stu-id="cbf9d-233"><a id="double-counting"></a>Double counting in parallel threads</span></span>

<span data-ttu-id="cbf9d-234">在某些情況下，堆疊檢視器的總時間計量會比要求實際的持續時間還多。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-234">In some cases the total time metric in the stack viewer is more than the actual duration of the request.</span></span>

<span data-ttu-id="cbf9d-235">當某個要求有兩個以上的關聯執行緒以平行方式運作時，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-235">This can happen when there are two or more threads associated with a request, operating in parallel.</span></span> <span data-ttu-id="cbf9d-236">於是，執行緒的總時間就會超過實際經過的時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-236">The total thread time is then more than the elapsed time.</span></span> <span data-ttu-id="cbf9d-237">執行緒經常要等候另一個執行緒完成。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-237">In many cases one thread may be waiting on the other to complete.</span></span> <span data-ttu-id="cbf9d-238">檢視器會嘗試偵測這個狀況，並省略不重要的等候，但在過程中，它會寧可顯示過多資訊，以免省略了可能重要的資訊。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-238">The viewer tries to detect this and omit the uninteresting wait, but errs on the side of showing too much rather than omitting what may be critical information.</span></span>  

<span data-ttu-id="cbf9d-239">當您在追蹤資料內看到平行執行緒，您必須判斷哪些執行緒正在等候，以便判斷出要求的關鍵路徑。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-239">When you see parallel threads in your traces, you need to determine which threads are waiting so you can determine the critical path for the request.</span></span> <span data-ttu-id="cbf9d-240">在大部分情況下，快速進入等候狀態的執行緒就只是在等候其他執行緒。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-240">In most cases, the thread that quickly goes into a wait state is simply waiting on the other threads.</span></span> <span data-ttu-id="cbf9d-241">請專注在其他執行緒上，並略過等候中執行緒的時間。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-241">Concentrate on the others and ignore the time in the waiting threads.</span></span>

### <span data-ttu-id="cbf9d-242"><a id="issue-loading-trace-in-viewer"></a>沒有分析資料</span><span class="sxs-lookup"><span data-stu-id="cbf9d-242"><a id="issue-loading-trace-in-viewer"></a>No profiling data</span></span>

1. <span data-ttu-id="cbf9d-243">如果您嘗試檢視的資料已存在好幾週，請試著限縮時間篩選器，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-243">If the data you are trying to view is older than a couple of weeks, try limiting your time filter and try again.</span></span>

2. <span data-ttu-id="cbf9d-244">確認系統未阻止 Proxy 或防火牆存取 https://gateway.azureserviceprofiler.net。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-244">Check that proxies or a firewall have not blocked access to https://gateway.azureserviceprofiler.net.</span></span>

3. <span data-ttu-id="cbf9d-245">檢查您在應用程式中使用的 Application Insights 檢測金鑰和您已啟用分析功能的 Application Insights 資源相同。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-245">Check that the Application Insights instrumentation key you are using in your app is the same as the Application Insights resource you've enabled profiling with.</span></span> <span data-ttu-id="cbf9d-246">金鑰通常位於 ApplicationInsights.config 中，但您也可以在 web.config 或 app.config 中找到。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-246">The key is usually in ApplicationInsights.config but can also be found in web.config or app.config.</span></span>

### <a name="error-report-in-the-profiling-viewer"></a><span data-ttu-id="cbf9d-247">分析檢視器的錯誤報表</span><span class="sxs-lookup"><span data-stu-id="cbf9d-247">Error report in the profiling viewer</span></span>

<span data-ttu-id="cbf9d-248">您可以從入口網站提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-248">File a support ticket from the portal.</span></span> <span data-ttu-id="cbf9d-249">請納入錯誤訊息內的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-249">Please include the correlation ID from the error message.</span></span>

## <a name="manual-installation"></a><span data-ttu-id="cbf9d-250">手動安裝</span><span class="sxs-lookup"><span data-stu-id="cbf9d-250">Manual installation</span></span>

<span data-ttu-id="cbf9d-251">當您設定分析工具時，系統會對 Web 應用程式的設定進行下列更新。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-251">When you configure the profiler, the following updates are made to the Web App's settings.</span></span> <span data-ttu-id="cbf9d-252">如果您的環境需要，您能以手動方式自行執行它們，例如，如果應用程式在 Azure App Service Environment (ASE) 中執行︰</span><span class="sxs-lookup"><span data-stu-id="cbf9d-252">You can do them yourself manually if your environment requires, for example, if your application runs in Azure App Service Environment (ASE):</span></span>

1. <span data-ttu-id="cbf9d-253">在 Web 應用程式控制刀鋒視窗中，開啟 [設定]。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-253">In the web app control blade, open Settings.</span></span>
2. <span data-ttu-id="cbf9d-254">將 [.Net Framework 版本] 設定為 [v4.6]。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-254">Set ".Net Framework version" to v4.6.</span></span>
3. <span data-ttu-id="cbf9d-255">將 [一律開啟] 設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-255">Set "Always On" to On.</span></span>
4. <span data-ttu-id="cbf9d-256">新增應用程式設定 "__APPINSIGHTS_INSTRUMENTATIONKEY__"，並將其值設定為 SDK 所使用的同一個檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-256">Add app setting "__APPINSIGHTS_INSTRUMENTATIONKEY__" and set the value to the same instrumentation key used by the SDK.</span></span>
5. <span data-ttu-id="cbf9d-257">開啟 [進階工具]。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-257">Open Advanced Tools.</span></span>
6. <span data-ttu-id="cbf9d-258">按一下 [執行] 以開啟 Kudu 網站。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-258">Click "Go" to open the Kudu website.</span></span>
7. <span data-ttu-id="cbf9d-259">在 Kudu 網站中，選取 [網站擴充功能]。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-259">In the Kudu website, select "Site extensions".</span></span>
8. <span data-ttu-id="cbf9d-260">從資源庫安裝 "__Application Insights__"。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-260">Install "__Application Insights__" from Gallery.</span></span>
9. <span data-ttu-id="cbf9d-261">重新啟動 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-261">Restart the web app.</span></span>

## <span data-ttu-id="cbf9d-262"><a id="aspnetcore"></a>ASP.NET Core 支援</span><span class="sxs-lookup"><span data-stu-id="cbf9d-262"><a id="aspnetcore"></a>ASP.NET Core Support</span></span>

<span data-ttu-id="cbf9d-263">ASP.NET Core 應用程式需要安裝 Microsoft.ApplicationInsights.AspNetCore Nuget 套件 2.1.0-beta6 或更新版本才能搭配分析工具使用。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-263">ASP.NET Core application needs to install Microsoft.ApplicationInsights.AspNetCore Nuget package 2.1.0-beta6 or higher to work with the Profiler.</span></span> <span data-ttu-id="cbf9d-264">在 2017/6/27 之後，我們將不再支援較低版本。</span><span class="sxs-lookup"><span data-stu-id="cbf9d-264">We no longer support the lower versions after 6/27/2017.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbf9d-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbf9d-265">Next steps</span></span>

* [<span data-ttu-id="cbf9d-266">在 Visual Studio 中使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="cbf9d-266">Working with Application Insights in Visual Studio</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
