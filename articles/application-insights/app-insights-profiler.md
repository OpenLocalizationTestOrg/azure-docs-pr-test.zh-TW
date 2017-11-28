---
title: "使用 Application Insights 在 Azure 上的 aaaProfiling 即時 web 應用程式 |Microsoft 文件"
description: "低耗用量分析工具找出您的 web 伺服器程式碼中的 hello 最忙碌路徑。"
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
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a><span data-ttu-id="1d672-103">使用 Application Insights 來分析即時 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="1d672-103">Profiling live Azure web apps with Application Insights</span></span>

<span data-ttu-id="1d672-104">Application Insights 的這項功能在應用程式服務為 GA，在 Compute 為預覽中。</span><span class="sxs-lookup"><span data-stu-id="1d672-104">*This feature of Application Insights is GA for App Services and in preview for Compute.*</span></span>

<span data-ttu-id="1d672-105">找出多少時間的即時 web 應用程式中的每個方法中使用程式碼剖析工具的 hello [Azure Application Insights](app-insights-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1d672-105">Find out how much time is spent in each method in your live web application by using hello profiling tool of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1d672-106">它會顯示詳細的設定檔的即時應用程式所服務的要求，並反白顯示 hello ' 最忙碌路徑' 使用 hello 最多時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-106">It shows you detailed profiles of live requests that were served by your app, and highlights hello 'hot path' that is using hello most time.</span></span> <span data-ttu-id="1d672-107">它會自動選取具有不同回應時間的範例。</span><span class="sxs-lookup"><span data-stu-id="1d672-107">It automatically selects examples that have different response times.</span></span> <span data-ttu-id="1d672-108">hello 分析工具會使用各種技術 toominimize 額外負荷。</span><span class="sxs-lookup"><span data-stu-id="1d672-108">hello profiler uses various techniques toominimize overhead.</span></span>

<span data-ttu-id="1d672-109">hello 分析工具目前適用於 ASP.NET web 應用程式執行於 Azure 應用程式服務，在至少 hello 基本定價層。</span><span class="sxs-lookup"><span data-stu-id="1d672-109">hello profiler currently works for ASP.NET web apps running on Azure App Services, in at least hello Basic pricing tier.</span></span> 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a><span data-ttu-id="1d672-110">啟用 hello 程式碼剖析工具</span><span class="sxs-lookup"><span data-stu-id="1d672-110">Enable hello profiler</span></span>

<span data-ttu-id="1d672-111">在程式碼中[安裝 Application Insights](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="1d672-111">[Install Application Insights](app-insights-asp-net.md) in your code.</span></span> <span data-ttu-id="1d672-112">如果已安裝，請確定您擁有 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="1d672-112">If it's already installed, make sure you have hello latest version.</span></span> <span data-ttu-id="1d672-113">(toodo，以滑鼠右鍵按一下方案總管] 中的專案，然後選擇 [管理 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="1d672-113">(toodo this, right-click your project in Solution Explorer, and choose Manage NuGet packages.</span></span> <span data-ttu-id="1d672-114">選取 [更新] 並更新所有套件)。重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d672-114">Select Updates and update all packages.) Re-deploy your app.</span></span>

<span data-ttu-id="1d672-115">您使用的是 ASP.NET Core 嗎？[請查看這裡](#aspnetcore)。</span><span class="sxs-lookup"><span data-stu-id="1d672-115">*Using ASP.NET Core? [Check here](#aspnetcore).*</span></span>

<span data-ttu-id="1d672-116">在[https://portal.azure.com](https://portal.azure.com)，開啟您的 web 應用程式的 hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="1d672-116">In [https://portal.azure.com](https://portal.azure.com), open hello Application Insights resource for your web app.</span></span> <span data-ttu-id="1d672-117">開啟 [效能] 然後按一下 [啟用 Application Insights 分析工具...]。</span><span class="sxs-lookup"><span data-stu-id="1d672-117">Open **Performance** and click **Enable Application Insights Profiler...**.</span></span>

![按一下 在橫幅中 hello 啟用程式碼剖析工具][enable-profiler-banner]

<span data-ttu-id="1d672-119">或者，您隨時可以按一下**設定**tooview 狀態、 啟用或停用 hello 程式碼剖析工具。</span><span class="sxs-lookup"><span data-stu-id="1d672-119">Alternatively, you can always click **Configure** tooview status, enable, or disable hello Profiler.</span></span>

![在 hello 效能刀鋒視窗中，按一下 設定][performance-blade]

<span data-ttu-id="1d672-121">使用 Application Insights 設定的 Web Apps 會列在 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1d672-121">Web apps that are configured with Application Insights are listed on Configure blade.</span></span> <span data-ttu-id="1d672-122">請依照下列指示 tooinstall hello 程式碼剖析工具代理程式有需要。</span><span class="sxs-lookup"><span data-stu-id="1d672-122">Follow instructions tooinstall hello Profiler agent if needed.</span></span> <span data-ttu-id="1d672-123">如果尚未使用 Application Insights 設定任何 Web 應用程式，請按一下 [新增連結的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1d672-123">If no web app is configured with Application Insights yet, click *Add Linked Apps*.</span></span>

<span data-ttu-id="1d672-124">使用 hello*啟用程式碼剖析工具*或*停用分析工具*hello 設定刀鋒視窗 toocontrol 按鈕 hello 所有連結的 web 應用程式的程式碼剖析工具。</span><span class="sxs-lookup"><span data-stu-id="1d672-124">Use hello *Enable Profiler* or *Disable Profiler* buttons in hello Configure blade toocontrol hello Profiler on all your linked web apps.</span></span>



![設定刀鋒視窗][linked app services]

<span data-ttu-id="1d672-126">toostop 或重新啟動 hello profiler 個別的應用程式服務執行個體，您會發現它**hello App Service 資源中**，請在**Web 工作**。</span><span class="sxs-lookup"><span data-stu-id="1d672-126">toostop or restart hello profiler for an individual App Service instance, you'll find it **in hello App Service resource**, in **Web Jobs**.</span></span> <span data-ttu-id="1d672-127">toodelete 它查看**延伸**。</span><span class="sxs-lookup"><span data-stu-id="1d672-127">toodelete it, look under **Extensions**.</span></span>

![停用 web 作業的分析工具][disable-profiler-webjob]

<span data-ttu-id="1d672-129">我們建議您擁有 hello 分析工具在所有您 web 應用程式 toodiscover 任何效能問題儘速上啟用。</span><span class="sxs-lookup"><span data-stu-id="1d672-129">We recommend that you have hello Profiler enabled on all your web apps toodiscover any performance issues as soon as possible.</span></span>

<span data-ttu-id="1d672-130">如果您使用 WebDeploy toodeploy 變更 tooyour web 應用程式，請確定您排除 hello **App_Data**在部署期間刪除的資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d672-130">If you use WebDeploy toodeploy changes tooyour web application, ensure that you exclude hello **App_Data** folder from being deleted during deployment.</span></span> <span data-ttu-id="1d672-131">否則 hello 延伸模組程式碼剖析工具檔案將會刪除當您下次部署 hello web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="1d672-131">Otherwise, hello profiler extension's files will be deleted when you next deploy hello web application tooAzure.</span></span>

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a><span data-ttu-id="1d672-132">使用分析工具搭配 Azure VM 和 Compute 資源 (預覽)</span><span class="sxs-lookup"><span data-stu-id="1d672-132">Using profiler with Azure VMs and Compute resources (preview)</span></span>

<span data-ttu-id="1d672-133">當您[在執行階段啟用 Azure App Service 的 Application Insights](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights) 時，分析工具會自動提供使用。</span><span class="sxs-lookup"><span data-stu-id="1d672-133">When you [enable Application Insights for Azure app services at run time](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), Profiler is automatically available.</span></span> <span data-ttu-id="1d672-134">(如果您已啟用 Application Insights hello 資源，您可能需要透過 hello tooupdate toohello lates 版本**設定**精靈。)</span><span class="sxs-lookup"><span data-stu-id="1d672-134">(If you already enabled Application Insights for hello resource, you might need tooupdate toohello lates version through hello **Configure** wizard.)</span></span>

<span data-ttu-id="1d672-135">沒有[預覽版的 Azure 計算資源的程式碼剖析工具 hello](https://go.microsoft.com/fwlink/?linkid=848155)。</span><span class="sxs-lookup"><span data-stu-id="1d672-135">There is a [preview version of hello Profiler for Azure Compute resources](https://go.microsoft.com/fwlink/?linkid=848155).</span></span>


## <a name="limits"></a><span data-ttu-id="1d672-136">限制</span><span class="sxs-lookup"><span data-stu-id="1d672-136">Limits</span></span>

<span data-ttu-id="1d672-137">hello 預設資料保留為 5 天。</span><span class="sxs-lookup"><span data-stu-id="1d672-137">hello default data retention is 5 days.</span></span> <span data-ttu-id="1d672-138">每日擷取最多 10 GB。</span><span class="sxs-lookup"><span data-stu-id="1d672-138">Maximum 10 GB ingested per day.</span></span>

<span data-ttu-id="1d672-139">沒有 hello 分析工具服務需付費。</span><span class="sxs-lookup"><span data-stu-id="1d672-139">There is no charge for hello profiler service.</span></span> <span data-ttu-id="1d672-140">您的 web 應用程式必須裝載在至少 hello 基本層的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="1d672-140">Your web app must be hosted in at least hello Basic tier of App Services.</span></span>

## <a name="viewing-profiler-data"></a><span data-ttu-id="1d672-141">檢視分析工具的資料</span><span class="sxs-lookup"><span data-stu-id="1d672-141">Viewing profiler data</span></span>

<span data-ttu-id="1d672-142">開啟 hello 效能刀鋒視窗，然後向下的捲動 toohello 作業清單。</span><span class="sxs-lookup"><span data-stu-id="1d672-142">Open hello Performance blade and scroll down toohello operation list.</span></span>




![Application Insights 的 [效能] 刀鋒視窗 [範例] 資料行][performance-blade-examples]

<span data-ttu-id="1d672-144">hello hello 資料表中的資料行如下：</span><span class="sxs-lookup"><span data-stu-id="1d672-144">hello columns in hello table are:</span></span>

* <span data-ttu-id="1d672-145">**計數**-hello hello 的 hello 刀鋒視窗的時間範圍中這些要求的數目。</span><span class="sxs-lookup"><span data-stu-id="1d672-145">**Count** - hello number of these requests in hello time range of hello blade.</span></span>
* <span data-ttu-id="1d672-146">**中位數**-hello 一般應用程式會採用 toorespond tooa 要求的時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-146">**Median** - hello typical time your app takes toorespond tooa request.</span></span> <span data-ttu-id="1d672-147">在所有的回應中，有一半會快過此時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-147">Half of all responses were faster than this.</span></span>
* <span data-ttu-id="1d672-148">**第 95 個百分位數** - 95% 的回應會快過此時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-148">**95th percentile** 95% of responses were faster than this.</span></span> <span data-ttu-id="1d672-149">如果此圖中的 hello 中間值大不相同，可能是您的應用程式發生間歇性問題。</span><span class="sxs-lookup"><span data-stu-id="1d672-149">If this figure is very different from hello median, there might be an intermittent problem with your app.</span></span> <span data-ttu-id="1d672-150">(或者，可能的解釋為有某者設計功能導致此結果，例如快取)。</span><span class="sxs-lookup"><span data-stu-id="1d672-150">(Or it might be explained by a design feature such as caching.)</span></span>
* <span data-ttu-id="1d672-151">**範例**-圖示表示該 hello profiler 擷取這項作業的堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="1d672-151">**Examples** - an icon indicates that hello profiler has captured stack traces for this operation.</span></span>

<span data-ttu-id="1d672-152">按一下 [hello 範例圖示 tooopen hello 追蹤總管]。</span><span class="sxs-lookup"><span data-stu-id="1d672-152">Click hello Examples icon tooopen hello trace explorer.</span></span> <span data-ttu-id="1d672-153">hello 總管 中顯示已捕捉 hello 程式碼剖析工具的數個範例，分類依回應時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-153">hello explorer shows several samples that hello profiler has captured, classified by response time.</span></span>

<span data-ttu-id="1d672-154">選取範例 tooshow 時間花費在執行 hello 的要求的程式碼層級細分。</span><span class="sxs-lookup"><span data-stu-id="1d672-154">Select a sample tooshow a code-level breakdown of time spent executing hello request.</span></span>

![Application Insights 追蹤總管][trace-explorer]

<span data-ttu-id="1d672-156">**顯示 最忙碌路徑**開啟 hello 最大的分葉節點，或至少是關閉。</span><span class="sxs-lookup"><span data-stu-id="1d672-156">**Show hot path** opens hello biggest leaf node, or at least something close.</span></span> <span data-ttu-id="1d672-157">在大部分情況下此節點會相鄰 tooa 效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="1d672-157">In most cases this node will be adjacent tooa performance bottleneck.</span></span>



* <span data-ttu-id="1d672-158">**標籤**: hello 的 hello 函式或事件的名稱。</span><span class="sxs-lookup"><span data-stu-id="1d672-158">**Label**: hello name of hello function or event.</span></span> <span data-ttu-id="1d672-159">hello 樹狀會顯示混合的程式碼和 （如 SQL 和 http 的事件） 發生的事件。</span><span class="sxs-lookup"><span data-stu-id="1d672-159">hello tree shows a mix of code and events that occurred (such as SQL and http events).</span></span> <span data-ttu-id="1d672-160">hello 最上層事件代表 hello 整體要求持續時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-160">hello top event represents hello overall request duration.</span></span>
* <span data-ttu-id="1d672-161">**經過**: hello hello hello 作業開始 hello 結束之間的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="1d672-161">**Elapsed**: hello time interval between hello start of hello operation and hello end.</span></span>
* <span data-ttu-id="1d672-162">**當**： 顯示 hello 函式/事件執行關聯 tooother 函式中時。</span><span class="sxs-lookup"><span data-stu-id="1d672-162">**When**: Shows when hello function/event was running in relation tooother functions.</span></span>

## <a name="how-tooread-performance-data"></a><span data-ttu-id="1d672-163">如何 tooread 效能資料</span><span class="sxs-lookup"><span data-stu-id="1d672-163">How tooread performance data</span></span>

<span data-ttu-id="1d672-164">Microsoft 服務程式碼剖析工具會使用取樣方法和檢測 tooanalyze hello 應用程式效能的組合。</span><span class="sxs-lookup"><span data-stu-id="1d672-164">Microsoft service profiler uses a combination of sampling method and instrumentation tooanalyze hello performance of your application.</span></span>
<span data-ttu-id="1d672-165">正在進行詳細的集合時，服務程式碼剖析工具範例 hello 指令指標的每個每毫秒中的 hello 機器的 CPU。</span><span class="sxs-lookup"><span data-stu-id="1d672-165">When detailed collection is in progress, service profiler samples hello instruction pointer of each of hello machine's CPU in every millisecond.</span></span>
<span data-ttu-id="1d672-166">每個範例會擷取目前執行中，提供詳細的有用的資訊，該怎麼辦，執行緒做了這兩種最高和最低層級的抽象概念的 hello 執行緒 hello 完整呼叫堆疊。</span><span class="sxs-lookup"><span data-stu-id="1d672-166">Each sample captures hello complete call stack of hello thread currently executing, giving detailed and useful information about what that thread was doing at both high and low levels of abstraction.</span></span> <span data-ttu-id="1d672-167">服務程式碼剖析工具也會收集其他事件，例如內容切換的事件，TPL 事件和執行緒集區事件 tootrack 活動相互關聯及因果。</span><span class="sxs-lookup"><span data-stu-id="1d672-167">Service profiler also collects other events such as context switching events, TPL events, and thread-pool events tootrack activity correlation and causality.</span></span>

<span data-ttu-id="1d672-168">hello hello 時間表檢視中顯示的呼叫堆疊是 hello 的上述取樣和檢測 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="1d672-168">hello call stack shown in hello timeline view is hello result of hello above sampling and instrumentation.</span></span> <span data-ttu-id="1d672-169">因為每個範例會擷取 hello 執行緒 hello 完整呼叫堆疊，它會包含從 hello.NET framework 中，當您參考其他架構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d672-169">Because each sample captures hello complete call stack of hello thread, it includes code from hello .NET framework, as well as other frameworks you reference.</span></span>

### <span data-ttu-id="1d672-170"><a id="jitnewobj"></a>物件配置 (`clr!JIT\_New or clr!JIT\_Newarr1`)</span><span class="sxs-lookup"><span data-stu-id="1d672-170"><a id="jitnewobj"></a>Object Allocation (`clr!JIT\_New or clr!JIT\_Newarr1`)</span></span>
<span data-ttu-id="1d672-171">`clr!JIT\_New and clr!JIT\_Newarr1` 是 .NET Framework 內的 Helper 函式，可從 Managed 堆積來配置記憶體。</span><span class="sxs-lookup"><span data-stu-id="1d672-171">`clr!JIT\_New and clr!JIT\_Newarr1` are helper functions inside .NET framework that allocates memory from managed heap.</span></span> <span data-ttu-id="1d672-172">系統在配置物件時會叫用 `clr!JIT\_New`。</span><span class="sxs-lookup"><span data-stu-id="1d672-172">`clr!JIT\_New` is invoked when an object is allocated.</span></span> <span data-ttu-id="1d672-173">系統在配置物件陣列時則會叫用 `clr!JIT\_Newarr1`。</span><span class="sxs-lookup"><span data-stu-id="1d672-173">`clr!JIT\_Newarr1` is invoked when an object array is allocated.</span></span> <span data-ttu-id="1d672-174">這兩個函式的速度通常很快，應該不會花上多少時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-174">These two functions are typically very fast and should take relatively small amount of time.</span></span> <span data-ttu-id="1d672-175">如果您看到`clr!JIT\_New`或`clr!JIT\_Newarr1`製作時間表大量時間，就表示 hello 程式碼可能是配置許多物件和耗用大量的記憶體。</span><span class="sxs-lookup"><span data-stu-id="1d672-175">If you see `clr!JIT\_New` or `clr!JIT\_Newarr1` take a substantial amount of time in your timeline, it's an indication that hello code may be allocating many objects and consuming significant amount of memory.</span></span>

### <span data-ttu-id="1d672-176"><a id="theprestub"></a>載入程式碼 (`clr!ThePreStub`)</span><span class="sxs-lookup"><span data-stu-id="1d672-176"><a id="theprestub"></a>Loading Code (`clr!ThePreStub`)</span></span>
<span data-ttu-id="1d672-177">`clr!ThePreStub`是 helper 函式會準備 hello 程式碼 tooexecute hello 第一次的.NET framework 內。</span><span class="sxs-lookup"><span data-stu-id="1d672-177">`clr!ThePreStub` is a helper function inside .NET framework that prepares hello code tooexecute for hello first time.</span></span> <span data-ttu-id="1d672-178">這通常包括但不限於 JIT (Just In Time) 編譯。</span><span class="sxs-lookup"><span data-stu-id="1d672-178">This typically includes, but not limited to, JIT (Just In Time) compilation.</span></span> <span data-ttu-id="1d672-179">每個 C# 方法`clr!ThePreStub`應叫用的處理序 hello 存留期間最多一次。</span><span class="sxs-lookup"><span data-stu-id="1d672-179">For each C# method, `clr!ThePreStub` should be invoked at most once during hello lifetime of a process.</span></span>

<span data-ttu-id="1d672-180">如果您看到`clr!ThePreStub`會花費相當大量的要求的時間，它會指出該要求是 hello 執行該方法和.NET framework 執行階段 tooload，方法是重要的 hello 時間的第一個。</span><span class="sxs-lookup"><span data-stu-id="1d672-180">If you see `clr!ThePreStub` takes significant amount of time for a request, it indicates that request is hello first one that executes that method, and hello time for .NET framework runtime tooload that method is significant.</span></span> <span data-ttu-id="1d672-181">您可以考慮執行 hello 程式碼的該部分的使用者存取權，或考慮您的組件上執行 NGen 之前準備程序。</span><span class="sxs-lookup"><span data-stu-id="1d672-181">You can consider a warm-up process that executes that portion of hello code before your users access it, or consider running NGen on your assemblies.</span></span>

### <span data-ttu-id="1d672-182"><a id="lockcontention"></a>鎖定爭用 (`clr!JITutil\_MonContention` 或 `clr!JITutil\_MonEnterWorker`)</span><span class="sxs-lookup"><span data-stu-id="1d672-182"><a id="lockcontention"></a>Lock Contention (`clr!JITutil\_MonContention` or `clr!JITutil\_MonEnterWorker`)</span></span>
<span data-ttu-id="1d672-183">`clr!JITutil\_MonContention`或`clr!JITutil\_MonEnterWorker`表示 hello 目前執行緒正在等候釋放鎖定 toobe。</span><span class="sxs-lookup"><span data-stu-id="1d672-183">`clr!JITutil\_MonContention` or `clr!JITutil\_MonEnterWorker` indicate hello current thread is waiting for a lock toobe released.</span></span> <span data-ttu-id="1d672-184">系統在執行 C# 鎖定陳述式、叫用 Monitor.Enter 方法或以 MethodImplOptions.Synchronized 屬性叫用方法時，常會出現此情形。</span><span class="sxs-lookup"><span data-stu-id="1d672-184">This typically shows up when executing a C# lock statement, invoking Monitor.Enter method, or invoking a method with MethodImplOptions.Synchronized attribute.</span></span> <span data-ttu-id="1d672-185">當執行緒 A 會在取得鎖定，和執行緒 B 會嘗試 tooacquire hello 相同鎖定的執行緒釋放它之前，通常是鎖定爭用。</span><span class="sxs-lookup"><span data-stu-id="1d672-185">Lock contention typically happens when thread A acquires a lock, and thread B tries tooacquire hello same lock before thread A releases it.</span></span>

### <span data-ttu-id="1d672-186"><a id="ngencold"></a>載入程式碼 (`[COLD]`)</span><span class="sxs-lookup"><span data-stu-id="1d672-186"><a id="ngencold"></a>Loading code (`[COLD]`)</span></span>
<span data-ttu-id="1d672-187">如果 hello 方法名稱包含`[COLD]`，例如`mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`，則表示該 hello.NET framework 執行階段執行所未最佳化的程式碼<a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">特性指引最佳化</a>hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="1d672-187">If hello method name contains `[COLD]`, such as `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, it means that hello .NET framework runtime is executing code that is not optimized by <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">profile-guided optimization</a> for hello first time.</span></span> <span data-ttu-id="1d672-188">每個方法，它應該顯示 hello 處理序 hello 存留期間最多一次。</span><span class="sxs-lookup"><span data-stu-id="1d672-188">For each method, it should show up at most once during hello lifetime of hello process.</span></span>

<span data-ttu-id="1d672-189">如果載入程式碼會花很長的時間的要求，就表示該要求 hello 第一個 tooexecute hello 最佳化的一部分 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="1d672-189">If loading code takes significant amount of time for a request, it indicates that request is hello first one tooexecute hello unoptimized portion of hello method.</span></span> <span data-ttu-id="1d672-190">您可以考慮您的使用者存取權限才能執行 hello 程式碼的該部分的程序暖機。</span><span class="sxs-lookup"><span data-stu-id="1d672-190">You can consider a warm up process that executes that portion of hello code before your users access it.</span></span>

### <span data-ttu-id="1d672-191"><a id="httpclientsend"></a>傳送 HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="1d672-191"><a id="httpclientsend"></a>Send HTTP Request</span></span>
<span data-ttu-id="1d672-192">這類方法`HttpClient.Send`表示 hello 程式碼正在等候 HTTP 要求 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1d672-192">Methods such as `HttpClient.Send` indicate hello code is waiting for a HTTP request toocomplete.</span></span>

### <span data-ttu-id="1d672-193"><a id="sqlcommand"></a>資料庫作業</span><span class="sxs-lookup"><span data-stu-id="1d672-193"><a id="sqlcommand"></a>Database Operation</span></span>
<span data-ttu-id="1d672-194">例如 SqlCommand.Execute 方法表示資料庫作業 toocomplete 正在等待 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d672-194">Method such as SqlCommand.Execute indicates hello code is waiting for a database operation toocomplete.</span></span>

### <span data-ttu-id="1d672-195"><a id="await"></a>等候 (`AWAIT\_TIME`)</span><span class="sxs-lookup"><span data-stu-id="1d672-195"><a id="await"></a>Waiting (`AWAIT\_TIME`)</span></span>
<span data-ttu-id="1d672-196">`AWAIT\_TIME`指出 hello 程式碼等候另一個工作 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1d672-196">`AWAIT\_TIME` indicates hello code is waiting for another task toocomplete.</span></span> <span data-ttu-id="1d672-197">這通常會發生在 C# 'await' 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1d672-197">This typically happens with C# 'await' statement.</span></span> <span data-ttu-id="1d672-198">Hello 程式碼執行時以 C# 'await'、 hello 執行緒會回溯控制 toohello 執行緒集區，並傳回沒有遭到封鎖而等待 hello 'await' toofinish 沒有執行緒。</span><span class="sxs-lookup"><span data-stu-id="1d672-198">When hello code does a C# 'await', hello thread unwinds and returns control toohello thread-pool, and there is no thread that is blocked waiting for hello 'await' toofinish.</span></span> <span data-ttu-id="1d672-199">不過，以邏輯方式 hello，未 hello await '封鎖' hello 作業 toocomplete 正在等候的執行緒。</span><span class="sxs-lookup"><span data-stu-id="1d672-199">However, logically hello thread that did hello await is 'blocked' waiting for hello operation toocomplete.</span></span> <span data-ttu-id="1d672-200">`AWAIT\_TIME`表示等候 hello 工作 toocomplete hello 封鎖時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-200">The `AWAIT\_TIME` indicates hello blocked time waiting for hello task toocomplete.</span></span>

### <span data-ttu-id="1d672-201"><a id="block"></a> 封鎖的時間</span><span class="sxs-lookup"><span data-stu-id="1d672-201"><a id="block"></a>Blocked Time</span></span>
<span data-ttu-id="1d672-202">`BLOCKED_TIME`表示可以使用，例如等待同步處理物件、 使用，或等候要求 toofinish 執行緒 toobe 正在等候另一個資源 toobe 正在等待 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="1d672-202">`BLOCKED_TIME` indicates hello code is waiting for another resource toobe available, such as waiting for a synchronization object, waiting for a thread toobe available, or waiting for a request toofinish.</span></span>

### <span data-ttu-id="1d672-203"><a id="cpu"></a>CPU 時間</span><span class="sxs-lookup"><span data-stu-id="1d672-203"><a id="cpu"></a>CPU Time</span></span>
<span data-ttu-id="1d672-204">hello CPU 忙於執行 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="1d672-204">hello CPU is busy executing hello instructions.</span></span>

### <span data-ttu-id="1d672-205"><a id="disk"></a>磁碟時間</span><span class="sxs-lookup"><span data-stu-id="1d672-205"><a id="disk"></a>Disk Time</span></span>
<span data-ttu-id="1d672-206">hello 應用程式正在執行磁碟作業。</span><span class="sxs-lookup"><span data-stu-id="1d672-206">hello application is performing disk operations.</span></span>

### <span data-ttu-id="1d672-207"><a id="network"></a>網路時間</span><span class="sxs-lookup"><span data-stu-id="1d672-207"><a id="network"></a>Network Time</span></span>
<span data-ttu-id="1d672-208">hello 應用程式正在執行網路作業。</span><span class="sxs-lookup"><span data-stu-id="1d672-208">hello application is performing network operations.</span></span>

### <span data-ttu-id="1d672-209"><a id="when"></a>何時資料行</span><span class="sxs-lookup"><span data-stu-id="1d672-209"><a id="when"></a>When column</span></span>
<span data-ttu-id="1d672-210">這是收集節點 hello 內含樣本的會隨著時間的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="1d672-210">This is a visualization of how hello INCLUSIVE samples collected for a node vary over time.</span></span> <span data-ttu-id="1d672-211">hello 總 hello 要求的範圍分為 32 時間貯體，而該節點的 hello 內含樣本會累積到這些 32 個值區。</span><span class="sxs-lookup"><span data-stu-id="1d672-211">hello total range of hello request is divided into 32 time buckets and hello inclusive samples for that node are accumulated into those 32 buckets.</span></span> <span data-ttu-id="1d672-212">接著，每個值區會以長條來表示，而長條的高度則代表換算後的值。</span><span class="sxs-lookup"><span data-stu-id="1d672-212">Each bucket is then represented as a bar whose height represents a scaled value.</span></span> <span data-ttu-id="1d672-213">節點標示`CPU_TIME`或`BLOCKED_TIME`，或當耗用的資源 (cpu、 磁碟、 執行緒) 的明顯關聯性時，hello 列代表 hello 段時間的貯體中使用這些資源的其中一個。</span><span class="sxs-lookup"><span data-stu-id="1d672-213">For nodes marked `CPU_TIME` or `BLOCKED_TIME`, or where there is an obvious relationship of consuming a resource (cpu, disk, thread), hello bar represents consuming one of those resources for hello period of time of that bucket.</span></span> <span data-ttu-id="1d672-214">若您耗用多項資源，這些計量會大於 100%。</span><span class="sxs-lookup"><span data-stu-id="1d672-214">For these metrics you can get greater than 100% by consuming multiple resources.</span></span> <span data-ttu-id="1d672-215">例如，通常來說，如果您在某個期間內使用兩個 CPU，計量會是 200%。</span><span class="sxs-lookup"><span data-stu-id="1d672-215">For example, if on average you use two CPUs over an interval then you get 200%.</span></span>


## <span data-ttu-id="1d672-216"><a id="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="1d672-216"><a id="troubleshooting"></a>Troubleshooting</span></span>

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a><span data-ttu-id="1d672-217">如何知道 Application Insights 分析工具是否有執行？</span><span class="sxs-lookup"><span data-stu-id="1d672-217">How can I know whether Application Insights profiler is running?</span></span>

<span data-ttu-id="1d672-218">hello 分析工具會執行以 Web 應用程式中的連續 web 工作。</span><span class="sxs-lookup"><span data-stu-id="1d672-218">hello profiler runs as a continuous web job in Web App.</span></span> <span data-ttu-id="1d672-219">您可以在 https://portal.azure.com 開啟 hello Web 應用程式資源，並檢查 hello WebJobs 刀鋒視窗中的"ApplicationInsightsProfiler 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="1d672-219">You can open hello Web App resource in https://portal.azure.com and check "ApplicationInsightsProfiler" status in hello WebJobs blade.</span></span> <span data-ttu-id="1d672-220">如果它不執行中，開啟**記錄**toofind 深入了解。</span><span class="sxs-lookup"><span data-stu-id="1d672-220">If it isn't running, open **Logs** toofind out more.</span></span>

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a><span data-ttu-id="1d672-221">為什麼找不到任何堆疊範例即使 hello 分析工具執行？</span><span class="sxs-lookup"><span data-stu-id="1d672-221">Why can't I find any stack examples even though hello profiler is running?</span></span>

<span data-ttu-id="1d672-222">您可以檢查以下幾點。</span><span class="sxs-lookup"><span data-stu-id="1d672-222">Here are a few things you can check.</span></span>

1. <span data-ttu-id="1d672-223">確定 Web App Service 方案服務方案至少是基本層。</span><span class="sxs-lookup"><span data-stu-id="1d672-223">Make sure your Web App Service Plan is Basic tier and above.</span></span>
2. <span data-ttu-id="1d672-224">確定 Web 應用程式至少已啟用 Application Insights SDK 2.2 Beta 版。</span><span class="sxs-lookup"><span data-stu-id="1d672-224">Make sure your Web App has Application Insights SDK 2.2 Beta and above enabled.</span></span>
3. <span data-ttu-id="1d672-225">請確定您的 Web 應用程式具有 hello APPINSIGHTS_INSTRUMENTATIONKEY 設定以 hello 使用相同的檢測金鑰的 Application Insights SDK。</span><span class="sxs-lookup"><span data-stu-id="1d672-225">Make sure your Web App has hello APPINSIGHTS_INSTRUMENTATIONKEY setting with hello same instrumentation key used by Application Insights SDK.</span></span>
4. <span data-ttu-id="1d672-226">確定 Web 應用程式是在 .Net Framework 4.6 上執行。</span><span class="sxs-lookup"><span data-stu-id="1d672-226">Make sure your Web App is running on .Net Framework 4.6.</span></span>
5. <span data-ttu-id="1d672-227">如果是 ASP.NET Core 應用程式，也請[hello 所需的相依性](#aspnetcore)。</span><span class="sxs-lookup"><span data-stu-id="1d672-227">If it's an ASP.NET Core application, please also check [hello required dependencies](#aspnetcore).</span></span>

<span data-ttu-id="1d672-228">Hello 程式碼剖析工具啟動之後，沒有 hello 分析工具目前正在收集數個效能追蹤簡短熱身期間。</span><span class="sxs-lookup"><span data-stu-id="1d672-228">After hello profiler is started, there is a short warm-up period when hello profiler actively collects several performance traces.</span></span> <span data-ttu-id="1d672-229">之後，hello 分析工具會收集每個小時內的兩分鐘的效能追蹤。</span><span class="sxs-lookup"><span data-stu-id="1d672-229">After that, hello profiler collects performance traces for two minutes in every hour.</span></span>  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a><span data-ttu-id="1d672-230">我之前使用的是 Azure Service Profiler。</span><span class="sxs-lookup"><span data-stu-id="1d672-230">I was using Azure Service Profiler.</span></span> <span data-ttu-id="1d672-231">哪些情形的 tooit？</span><span class="sxs-lookup"><span data-stu-id="1d672-231">What happened tooit?</span></span>  

<span data-ttu-id="1d672-232">當您啟用 Application Insights Profiler 時，Azure Service Profiler 代理程式就會停用。</span><span class="sxs-lookup"><span data-stu-id="1d672-232">When you enable Application Insights Profiler, Azure Service Profiler agent is disabled.</span></span>

### <span data-ttu-id="1d672-233"><a id="double-counting"></a>平行執行緒重複計算</span><span class="sxs-lookup"><span data-stu-id="1d672-233"><a id="double-counting"></a>Double counting in parallel threads</span></span>

<span data-ttu-id="1d672-234">在某些情況下 hello hello 堆疊檢視器中的總時間度量大於 hello hello 要求的實際持續時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-234">In some cases hello total time metric in hello stack viewer is more than hello actual duration of hello request.</span></span>

<span data-ttu-id="1d672-235">當某個要求有兩個以上的關聯執行緒以平行方式運作時，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="1d672-235">This can happen when there are two or more threads associated with a request, operating in parallel.</span></span> <span data-ttu-id="1d672-236">hello 執行緒總時間大於然後 hello 經過的時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-236">hello total thread time is then more than hello elapsed time.</span></span> <span data-ttu-id="1d672-237">在許多情況下一個執行緒可能會等候 hello 其他 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1d672-237">In many cases one thread may be waiting on hello other toocomplete.</span></span> <span data-ttu-id="1d672-238">這個 hello 檢視器會嘗試 toodetect 和省略 hello 認為不重要的等候，但顯示太多而不是省略可能重要資訊的 hello 一邊方面會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1d672-238">hello viewer tries toodetect this and omit hello uninteresting wait, but errs on hello side of showing too much rather than omitting what may be critical information.</span></span>  

<span data-ttu-id="1d672-239">在您的追蹤中看到的平行執行緒，您會需要 toodetermine 的執行緒正在等候，因此您可以判斷 hello hello 要求的關鍵路徑。</span><span class="sxs-lookup"><span data-stu-id="1d672-239">When you see parallel threads in your traces, you need toodetermine which threads are waiting so you can determine hello critical path for hello request.</span></span> <span data-ttu-id="1d672-240">在大部分情況下，快速地進入等候狀態是只等待 hello 執行緒 hello 其他執行緒。</span><span class="sxs-lookup"><span data-stu-id="1d672-240">In most cases, hello thread that quickly goes into a wait state is simply waiting on hello other threads.</span></span> <span data-ttu-id="1d672-241">一開始可集中在 hello 其他項目，並忽略 hello hello 的等候中執行緒的時間。</span><span class="sxs-lookup"><span data-stu-id="1d672-241">Concentrate on hello others and ignore hello time in hello waiting threads.</span></span>

### <span data-ttu-id="1d672-242"><a id="issue-loading-trace-in-viewer"></a>沒有分析資料</span><span class="sxs-lookup"><span data-stu-id="1d672-242"><a id="issue-loading-trace-in-viewer"></a>No profiling data</span></span>

1. <span data-ttu-id="1d672-243">如果您嘗試 hello 資料 tooview 會超過幾週，請嘗試限制時間篩選，再試一次。</span><span class="sxs-lookup"><span data-stu-id="1d672-243">If hello data you are trying tooview is older than a couple of weeks, try limiting your time filter and try again.</span></span>

2. <span data-ttu-id="1d672-244">核取，proxy 或防火牆沒有封鎖存取 toohttps://gateway.azureserviceprofiler.net。</span><span class="sxs-lookup"><span data-stu-id="1d672-244">Check that proxies or a firewall have not blocked access toohttps://gateway.azureserviceprofiler.net.</span></span>

3. <span data-ttu-id="1d672-245">請檢查您應用程式中使用的檢測金鑰為 Application Insights hello 相同 hello Application Insights 資源，您已啟用透過程式碼剖析為該 hello。</span><span class="sxs-lookup"><span data-stu-id="1d672-245">Check that hello Application Insights instrumentation key you are using in your app is hello same as hello Application Insights resource you've enabled profiling with.</span></span> <span data-ttu-id="1d672-246">hello 索引鍵通常是 ApplicationInsights.config，但也可以在 web.config 或 app.config 中找到。</span><span class="sxs-lookup"><span data-stu-id="1d672-246">hello key is usually in ApplicationInsights.config but can also be found in web.config or app.config.</span></span>

### <a name="error-report-in-hello-profiling-viewer"></a><span data-ttu-id="1d672-247">Hello 設定檔檢視器中的錯誤報表</span><span class="sxs-lookup"><span data-stu-id="1d672-247">Error report in hello profiling viewer</span></span>

<span data-ttu-id="1d672-248">提出支援票證從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1d672-248">File a support ticket from hello portal.</span></span> <span data-ttu-id="1d672-249">請附上 hello 從 hello 錯誤訊息的相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d672-249">Please include hello correlation ID from hello error message.</span></span>

## <a name="manual-installation"></a><span data-ttu-id="1d672-250">手動安裝</span><span class="sxs-lookup"><span data-stu-id="1d672-250">Manual installation</span></span>

<span data-ttu-id="1d672-251">當您設定 hello 程式碼剖析工具時，hello 下列更新是作 toohello Web 應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="1d672-251">When you configure hello profiler, hello following updates are made toohello Web App's settings.</span></span> <span data-ttu-id="1d672-252">如果您的環境需要，您能以手動方式自行執行它們，例如，如果應用程式在 Azure App Service Environment (ASE) 中執行︰</span><span class="sxs-lookup"><span data-stu-id="1d672-252">You can do them yourself manually if your environment requires, for example, if your application runs in Azure App Service Environment (ASE):</span></span>

1. <span data-ttu-id="1d672-253">在 hello web 應用程式控制項刀鋒視窗中，開啟 設定。</span><span class="sxs-lookup"><span data-stu-id="1d672-253">In hello web app control blade, open Settings.</span></span>
2. <span data-ttu-id="1d672-254">設定 「.Net Framework 版本"toov4.6。</span><span class="sxs-lookup"><span data-stu-id="1d672-254">Set ".Net Framework version" toov4.6.</span></span>
3. <span data-ttu-id="1d672-255">設定 「 永遠開啟 」 tooOn。</span><span class="sxs-lookup"><span data-stu-id="1d672-255">Set "Always On" tooOn.</span></span>
4. <span data-ttu-id="1d672-256">新增應用程式設定"__APPINSIGHTS_INSTRUMENTATIONKEY__"和集 hello 值 toohello hello SDK 使用相同的檢測金鑰。</span><span class="sxs-lookup"><span data-stu-id="1d672-256">Add app setting "__APPINSIGHTS_INSTRUMENTATIONKEY__" and set hello value toohello same instrumentation key used by hello SDK.</span></span>
5. <span data-ttu-id="1d672-257">開啟 [進階工具]。</span><span class="sxs-lookup"><span data-stu-id="1d672-257">Open Advanced Tools.</span></span>
6. <span data-ttu-id="1d672-258">按一下"Go"tooopen hello Kudu 網站。</span><span class="sxs-lookup"><span data-stu-id="1d672-258">Click "Go" tooopen hello Kudu website.</span></span>
7. <span data-ttu-id="1d672-259">在 hello Kudu 網站，選取 「 網站擴充功能 」。</span><span class="sxs-lookup"><span data-stu-id="1d672-259">In hello Kudu website, select "Site extensions".</span></span>
8. <span data-ttu-id="1d672-260">從資源庫安裝 "__Application Insights__"。</span><span class="sxs-lookup"><span data-stu-id="1d672-260">Install "__Application Insights__" from Gallery.</span></span>
9. <span data-ttu-id="1d672-261">重新啟動 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d672-261">Restart hello web app.</span></span>

## <span data-ttu-id="1d672-262"><a id="aspnetcore"></a>ASP.NET Core 支援</span><span class="sxs-lookup"><span data-stu-id="1d672-262"><a id="aspnetcore"></a>ASP.NET Core Support</span></span>

<span data-ttu-id="1d672-263">ASP.NET Core 應用程式需要 tooinstall Microsoft.ApplicationInsights.AspNetCore Nuget 封裝 2.1.0-beta6 或更高版本 toowork 以 hello 程式碼剖析工具。</span><span class="sxs-lookup"><span data-stu-id="1d672-263">ASP.NET Core application needs tooinstall Microsoft.ApplicationInsights.AspNetCore Nuget package 2.1.0-beta6 or higher toowork with hello Profiler.</span></span> <span data-ttu-id="1d672-264">我們在 6/27/2017年之後不再支援 hello 較低版本。</span><span class="sxs-lookup"><span data-stu-id="1d672-264">We no longer support hello lower versions after 6/27/2017.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d672-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d672-265">Next steps</span></span>

* [<span data-ttu-id="1d672-266">在 Visual Studio 中使用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="1d672-266">Working with Application Insights in Visual Studio</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
