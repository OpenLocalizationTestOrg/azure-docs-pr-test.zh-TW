---
title: "App Service 中的 aaaSlow web 應用程式效能 |Microsoft 文件"
description: "本文可協助您針對 Azure App Service 中 Web 應用程式效能變慢的問題進行疑難排解。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "Web 應用程式效能、變慢的應用程式、應用程式變慢"
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a><span data-ttu-id="678c8-104">針對 Azure App Service 中 Web 應用程式效能變慢的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="678c8-104">Troubleshoot slow web app performance issues in Azure App Service</span></span>
<span data-ttu-id="678c8-105">本文可協助您針對 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)中 Web 應用程式效能變慢的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="678c8-105">This article helps you troubleshoot slow web app performance issues in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="678c8-106">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="678c8-106">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="678c8-107">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="678c8-107">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="678c8-108">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)，然後按一下 **取得支援**。</span><span class="sxs-lookup"><span data-stu-id="678c8-108">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="678c8-109">徵狀</span><span class="sxs-lookup"><span data-stu-id="678c8-109">Symptom</span></span>
<span data-ttu-id="678c8-110">當您瀏覽 hello web 應用程式時，hello 頁面載入緩慢和有時逾時。</span><span class="sxs-lookup"><span data-stu-id="678c8-110">When you browse hello web app, hello pages load slowly and sometimes timeout.</span></span>

## <a name="cause"></a><span data-ttu-id="678c8-111">原因</span><span class="sxs-lookup"><span data-stu-id="678c8-111">Cause</span></span>
<span data-ttu-id="678c8-112">此問題通常是因為應用程式層級問題所造成，例如：</span><span class="sxs-lookup"><span data-stu-id="678c8-112">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="678c8-113">網路要求耗費過長的時間</span><span class="sxs-lookup"><span data-stu-id="678c8-113">network requests taking a long time</span></span>
* <span data-ttu-id="678c8-114">應用程式程式碼或資料庫查詢的效率不佳</span><span class="sxs-lookup"><span data-stu-id="678c8-114">application code or database queries being inefficient</span></span>
* <span data-ttu-id="678c8-115">應用程式的記憶體/CPU 使用率過高</span><span class="sxs-lookup"><span data-stu-id="678c8-115">application using high memory/CPU</span></span>
* <span data-ttu-id="678c8-116">應用程式當機，因為 tooan 例外狀況</span><span class="sxs-lookup"><span data-stu-id="678c8-116">application crashing due tooan exception</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="678c8-117">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="678c8-117">Troubleshooting steps</span></span>
<span data-ttu-id="678c8-118">疑難排解可以分成三種不同的工作，依序為：</span><span class="sxs-lookup"><span data-stu-id="678c8-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="678c8-119">觀察和監視應用程式行為</span><span class="sxs-lookup"><span data-stu-id="678c8-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="678c8-120">收集資料</span><span class="sxs-lookup"><span data-stu-id="678c8-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="678c8-121">減少 hello 問題</span><span class="sxs-lookup"><span data-stu-id="678c8-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="678c8-122">[App Service Web Apps](/services/app-service/web/) 在每個步驟均提供您各種選項。</span><span class="sxs-lookup"><span data-stu-id="678c8-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="678c8-123">1.觀察和監視應用程式行為</span><span class="sxs-lookup"><span data-stu-id="678c8-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="678c8-124">追蹤服務健全狀況</span><span class="sxs-lookup"><span data-stu-id="678c8-124">Track Service health</span></span>
<span data-ttu-id="678c8-125">每次發生服務中斷或效能降低時，Microsoft Azure 就會發出公告。</span><span class="sxs-lookup"><span data-stu-id="678c8-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="678c8-126">您可以在 hello 追蹤 hello hello 服務健全狀況[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="678c8-126">You can track hello health of hello service on hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="678c8-127">如需詳細資訊，請參閱[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。</span><span class="sxs-lookup"><span data-stu-id="678c8-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="678c8-128">監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="678c8-128">Monitor your web app</span></span>
<span data-ttu-id="678c8-129">如果您的應用程式有任何問題，此選項可讓您 toofind 出。</span><span class="sxs-lookup"><span data-stu-id="678c8-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="678c8-130">在您的 web 應用程式] 刀鋒視窗中，按一下 [hello**要求與錯誤**磚。</span><span class="sxs-lookup"><span data-stu-id="678c8-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="678c8-131">hello**度量**刀鋒視窗會顯示您可以加入所有 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="678c8-131">hello **Metric** blade shows you all hello metrics you can add.</span></span>

<span data-ttu-id="678c8-132">某些您可能希望您的 web 應用程式 toomonitor hello 度量</span><span class="sxs-lookup"><span data-stu-id="678c8-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="678c8-133">平均記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="678c8-133">Average memory working set</span></span>
* <span data-ttu-id="678c8-134">平均回應時間</span><span class="sxs-lookup"><span data-stu-id="678c8-134">Average response time</span></span>
* <span data-ttu-id="678c8-135">CPU 時間</span><span class="sxs-lookup"><span data-stu-id="678c8-135">CPU time</span></span>
* <span data-ttu-id="678c8-136">記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="678c8-136">Memory working set</span></span>
* <span data-ttu-id="678c8-137">要求</span><span class="sxs-lookup"><span data-stu-id="678c8-137">Requests</span></span>

![監視 Web 應用程式效能](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

<span data-ttu-id="678c8-139">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="678c8-139">For more information, see:</span></span>

* [<span data-ttu-id="678c8-140">監視 Azure App Service 中的 Web Apps</span><span class="sxs-lookup"><span data-stu-id="678c8-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="678c8-141">接收警示通知</span><span class="sxs-lookup"><span data-stu-id="678c8-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a><span data-ttu-id="678c8-142">監視 Web 端點狀態</span><span class="sxs-lookup"><span data-stu-id="678c8-142">Monitor web endpoint status</span></span>
<span data-ttu-id="678c8-143">如果您執行您 web 應用程式在 hello**標準**定價層，Web 應用程式可讓您監視兩個端點從三個地理位置。</span><span class="sxs-lookup"><span data-stu-id="678c8-143">If you are running your web app in hello **Standard** pricing tier, Web Apps lets you monitor two endpoints from three geographic locations.</span></span>

<span data-ttu-id="678c8-144">端點監視能讓您設定從不同地理位置執行，且用來測試 Web URL 之回應時間和運作時間的 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="678c8-144">Endpoint monitoring configures web tests from geo-distributed locations that test response time and uptime of web URLs.</span></span> <span data-ttu-id="678c8-145">hello 測試會從每個位置中執行 HTTP GET 作業上 hello web URL toodetermine hello 回應時間和執行時間。</span><span class="sxs-lookup"><span data-stu-id="678c8-145">hello test performs an HTTP GET operation on hello web URL toodetermine hello response time and uptime from each location.</span></span> <span data-ttu-id="678c8-146">各個已設定的位置會每隔五分鐘執行一次測試。</span><span class="sxs-lookup"><span data-stu-id="678c8-146">Each configured location runs a test every five minutes.</span></span>

<span data-ttu-id="678c8-147">運作時間是透過 HTTP 回應碼來加以監視，而回應時間的測量單位是毫秒。</span><span class="sxs-lookup"><span data-stu-id="678c8-147">Uptime is monitored using HTTP response codes, and response time is measured in milliseconds.</span></span> <span data-ttu-id="678c8-148">如果 hello HTTP 回應碼大於或等於 too400 或如果 hello 回應時間超過 30 秒，則監視測試會失敗。</span><span class="sxs-lookup"><span data-stu-id="678c8-148">A monitoring test fails if hello HTTP response code is greater than or equal too400 or if hello response takes more than 30 seconds.</span></span> <span data-ttu-id="678c8-149">端點視為可用監視測試皆成功從所有 hello 指定位置。</span><span class="sxs-lookup"><span data-stu-id="678c8-149">An endpoint is considered available if its monitoring tests succeed from all hello specified locations.</span></span>

<span data-ttu-id="678c8-150">它，請參閱 tooset[監視 Azure App Service 中的應用程式](web-sites-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="678c8-150">tooset it up, see [Monitor apps in Azure App Service](web-sites-monitor.md).</span></span>

<span data-ttu-id="678c8-151">同時，亦請參閱 [讓 Azure 網站保持運作以及端點監視 - 對談來賓 Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) 的端點監視影片。</span><span class="sxs-lookup"><span data-stu-id="678c8-151">Also, see [Keeping Azure Web Sites up plus Endpoint Monitoring - with Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) for a video on endpoint monitoring.</span></span>

#### <a name="application-performance-monitoring-using-extensions"></a><span data-ttu-id="678c8-152">使用擴充功能的應用程式效能監視</span><span class="sxs-lookup"><span data-stu-id="678c8-152">Application performance monitoring using Extensions</span></span>
<span data-ttu-id="678c8-153">您也可以利用*網站擴充功能*監視應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="678c8-153">You can also monitor your application performance by using *site extensions*.</span></span>

<span data-ttu-id="678c8-154">每個 App Service web 應用程式提供可延伸管理結束點，可讓您 toouse 一組強大的工具部署為網站擴充功能。</span><span class="sxs-lookup"><span data-stu-id="678c8-154">Each App Service web app provides an extensible management end point that allows you toouse a powerful set of tools deployed as site extensions.</span></span> <span data-ttu-id="678c8-155">擴充功能包括：</span><span class="sxs-lookup"><span data-stu-id="678c8-155">Extensions include:</span></span> 

- <span data-ttu-id="678c8-156">原始程式碼編輯器，例如 [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="678c8-156">Source code editors like [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx).</span></span> 
- <span data-ttu-id="678c8-157">適用於已連線的資源，例如 MySQL 資料庫管理工具連線 tooa web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-157">Management tools for connected resources such as a MySQL database connected tooa web app.</span></span>

<span data-ttu-id="678c8-158">[Azure 的 Application Insights](/services/application-insights/)和[New Relic](/marketplace/partners/newrelic/newrelic/) hello 效能監視站台所提供的擴充功能的兩個。</span><span class="sxs-lookup"><span data-stu-id="678c8-158">[Azure Application Insights](/services/application-insights/) and [New Relic](/marketplace/partners/newrelic/newrelic/) are two of hello performance monitoring site extensions that are available.</span></span> <span data-ttu-id="678c8-159">toouse New Relic，您可以安裝在執行階段代理程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-159">toouse New Relic, you install an agent at runtime.</span></span> <span data-ttu-id="678c8-160">toouse Azure Application Insights，重建的 sdk，您的程式碼，您也可以安裝可提供存取 tooadditional 資料延伸模組。</span><span class="sxs-lookup"><span data-stu-id="678c8-160">toouse Azure Application Insights, you rebuild your code with an SDK, and you can also install an extension that provides access tooadditional data.</span></span> <span data-ttu-id="678c8-161">hello SDK 可讓您更詳細地撰寫的程式碼 toomonitor hello 和您的應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="678c8-161">hello SDK lets you write code toomonitor hello usage and performance of your app in more detail.</span></span>

<span data-ttu-id="678c8-162">toouse Application Insights，請參閱[監視 web 應用程式中的效能](../application-insights/app-insights-web-monitor-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="678c8-162">toouse Application Insights, see [Monitor performance in web applications](../application-insights/app-insights-web-monitor-performance.md).</span></span>

<span data-ttu-id="678c8-163">toouse New Relic，請參閱[新 Relic 應用程式效能在 Azure 上管理](../store-new-relic-cloud-services-dotnet-application-performance-management.md)。</span><span class="sxs-lookup"><span data-stu-id="678c8-163">toouse New Relic, see [New Relic Application Performance Management on Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).</span></span>

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="678c8-164">2.收集資料</span><span class="sxs-lookup"><span data-stu-id="678c8-164">2. Collect data</span></span>
<span data-ttu-id="678c8-165">hello Web 應用程式環境提供記錄資訊從 hello web 伺服器和 hello web 應用程式的診斷功能。</span><span class="sxs-lookup"><span data-stu-id="678c8-165">hello Web Apps environment provides diagnostic functionality for logging information from both hello web server and hello web application.</span></span> <span data-ttu-id="678c8-166">hello 資訊分成 web 伺服器的診斷和 application diagnostics。</span><span class="sxs-lookup"><span data-stu-id="678c8-166">hello information is separated into web server diagnostics and application diagnostics.</span></span>

#### <a name="enable-web-server-diagnostics"></a><span data-ttu-id="678c8-167">啟用網頁伺服器診斷</span><span class="sxs-lookup"><span data-stu-id="678c8-167">Enable web server diagnostics</span></span>
<span data-ttu-id="678c8-168">您可以啟用或停用下列種類的記錄檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="678c8-168">You can enable or disable hello following kinds of logs:</span></span>

* <span data-ttu-id="678c8-169">**詳細的錯誤記錄** - 對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="678c8-169">**Detailed Error Logging** - Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span> <span data-ttu-id="678c8-170">這可能包含可協助您判斷為什麼 hello 伺服器傳回 hello 錯誤碼的資訊。</span><span class="sxs-lookup"><span data-stu-id="678c8-170">This may contain information that can help determine why hello server returned hello error code.</span></span>
* <span data-ttu-id="678c8-171">**失敗要求追蹤**-詳細的失敗的要求，包括 hello IIS 使用的元件 tooprocess hello 要求和取得每個元件中的 hello 時間的追蹤資訊。</span><span class="sxs-lookup"><span data-stu-id="678c8-171">**Failed Request Tracing** - Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span> <span data-ttu-id="678c8-172">如果您正嘗試 tooimprove web 應用程式效能或隔離造成特定的 HTTP 錯誤，這可能會很有用。</span><span class="sxs-lookup"><span data-stu-id="678c8-172">This can be useful if you are attempting tooimprove web app performance or isolate what is causing a specific HTTP error.</span></span>
* <span data-ttu-id="678c8-173">**Web 伺服器記錄**-HTTP 交易使用 hello W3C 擴充的記錄檔格式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="678c8-173">**Web Server Logging** - Information about HTTP transactions using hello W3C extended log file format.</span></span> <span data-ttu-id="678c8-174">決定整體的 web 應用程式度量，例如 hello 處理要求的數目或多少要求來自特定 IP 位址時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="678c8-174">This is useful when determining overall web app metrics, such as hello number of requests handled or how many requests are from a specific IP address.</span></span>

#### <a name="enable-application-diagnostics"></a><span data-ttu-id="678c8-175">啟用應用程式診斷</span><span class="sxs-lookup"><span data-stu-id="678c8-175">Enable application diagnostics</span></span>
<span data-ttu-id="678c8-176">有數個選項 toocollect 應用程式的效能資料，Web 應用程式、 設定檔的即時應用程式從 Visual Studio 中，或修改您的應用程式程式碼 toolog 的詳細資訊和追蹤。</span><span class="sxs-lookup"><span data-stu-id="678c8-176">There are several options toocollect application performance data from Web Apps, profile your application live from Visual Studio, or modify your application code toolog more information and traces.</span></span> <span data-ttu-id="678c8-177">您可以選擇根據 hello 選項上多少的存取權，您有 toohello 應用程式，而且您從 監視工具的 hello 觀察到。</span><span class="sxs-lookup"><span data-stu-id="678c8-177">You can choose hello options based on how much access you have toohello application and what you observed from hello monitoring tools.</span></span>

##### <a name="use-application-insights-profiler"></a><span data-ttu-id="678c8-178">使用 Application Insights Profiler</span><span class="sxs-lookup"><span data-stu-id="678c8-178">Use Application Insights Profiler</span></span>
<span data-ttu-id="678c8-179">您可以啟用 hello 應用程式 Insights Profiler toostart 擷取詳細的效能追蹤。</span><span class="sxs-lookup"><span data-stu-id="678c8-179">You can enable hello Application Insights Profiler toostart capturing detailed performance traces.</span></span> <span data-ttu-id="678c8-180">您可以存取的 toofive 天前何時該添 tooinvestigate 問題是發生在過去的 hello 上擷取的追蹤。</span><span class="sxs-lookup"><span data-stu-id="678c8-180">You can access traces captured up toofive days ago when you need tooinvestigate problems happened in hello past.</span></span> <span data-ttu-id="678c8-181">您可以選擇此選項，只要您有 Azure 入口網站上的存取 toohello web 應用程式的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="678c8-181">You can choose this option as long as you have access toohello web app's Application Insights resource on Azure portal.</span></span>

<span data-ttu-id="678c8-182">應用程式 Insights 分析工具提供的統計資料指出哪一行程式碼使 hello 回應變慢的回應時間的每個 web 呼叫和追蹤。</span><span class="sxs-lookup"><span data-stu-id="678c8-182">Application Insights Profiler provides statistics on response time for each web call and traces that indicates which line of code caused hello slow responses.</span></span> <span data-ttu-id="678c8-183">有時 hello App Service 應用程式緩慢，是因為某些程式碼不會寫入在高效能的方式。</span><span class="sxs-lookup"><span data-stu-id="678c8-183">Sometimes hello App Service app is slow because certain code is not written in a performant way.</span></span> <span data-ttu-id="678c8-184">範例包括可以平行執行以及在不想要的資料庫鎖定爭用中執行的循序程式碼。</span><span class="sxs-lookup"><span data-stu-id="678c8-184">Examples include sequential code that can be run in parallel and undesired database lock contentions.</span></span> <span data-ttu-id="678c8-185">Hello 程式碼中移除這些瓶頸增加 hello 應用程式效能，但它們是永久 toodetect 而不需設定詳細追蹤和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="678c8-185">Removing these bottlenecks in hello code increases hello app's performance, but they are hard toodetect without setting up elaborate traces and logs.</span></span> <span data-ttu-id="678c8-186">應用程式 Insights 分析工具所收集的 hello 追蹤可協助識別 hello hello 應用程式變慢的程式碼行，並克服這項挑戰，App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-186">hello traces collected by Application Insights Profiler helps identifying hello lines of code that slows down hello application and overcome this challenge for App Service apps.</span></span>

 <span data-ttu-id="678c8-187">如需詳細資訊，請參閱[使用 Application Insights 來分析即時 Azure Web 應用程式](../application-insights/app-insights-profiler.md)。</span><span class="sxs-lookup"><span data-stu-id="678c8-187">For more information, see [Profiling live Azure web apps with Application Insights](../application-insights/app-insights-profiler.md).</span></span>

##### <a name="use-remote-profiling"></a><span data-ttu-id="678c8-188">使用遠端分析</span><span class="sxs-lookup"><span data-stu-id="678c8-188">Use Remote Profiling</span></span>
<span data-ttu-id="678c8-189">您可在 Azure App Service、Web Apps、API Apps 和 WebJobs 進行遠端分析。</span><span class="sxs-lookup"><span data-stu-id="678c8-189">In Azure App Service, Web Apps, API Apps, and WebJobs can be remotely profiled.</span></span> <span data-ttu-id="678c8-190">如果您擁有存取 toohello web 應用程式資源和您知道如何 tooreproduce hello 問題，或如果您知道 hello 完全發生的時間間隔 hello 效能問題，請選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="678c8-190">Choose this option if you have access toohello web app resource and you know how tooreproduce hello issue, or if you know hello exact time interval hello performance issue happens.</span></span>

<span data-ttu-id="678c8-191">遠端分析很有用，如果 hello hello 程序的 CPU 使用量過高和您的處理序執行速度比預期慢或 hello 的 HTTP 要求的延遲會超過正常情況，則您可以從遠端設定檔，您的程序並取得 hello CPU 取樣的呼叫堆疊 tooanalyzehello 程序活動和程式碼最忙碌路徑。</span><span class="sxs-lookup"><span data-stu-id="678c8-191">Remote Profiling is useful if hello CPU usage of hello process is high and your process is running slower than expected, or hello latency of HTTP requests are higher than normal, you can remotely profile your process and get hello CPU sampling call stacks tooanalyze hello process activity and code hot paths.</span></span>

<span data-ttu-id="678c8-192">如需詳細資訊，請參閱 [Azure App Service 中的遠端分析支援](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service)。</span><span class="sxs-lookup"><span data-stu-id="678c8-192">For more information, see [Remote Profiling support in Azure App Service](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).</span></span>

##### <a name="set-up-diagnostic-traces-manually"></a><span data-ttu-id="678c8-193">手動設定診斷追蹤</span><span class="sxs-lookup"><span data-stu-id="678c8-193">Set up diagnostic traces manually</span></span>
<span data-ttu-id="678c8-194">如果您有存取 toohello web 應用程式的原始程式碼，Application diagnostics 可讓您的 web 應用程式所產生的 toocapture 資訊。</span><span class="sxs-lookup"><span data-stu-id="678c8-194">If you have access toohello web application source code, Application diagnostics enables you toocapture information produced by a web application.</span></span> <span data-ttu-id="678c8-195">ASP.NET 應用程式可以使用 hello`System.Diagnostics.Trace`類別 toolog 資訊 toohello 應用程式診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="678c8-195">ASP.NET applications can use hello `System.Diagnostics.Trace` class toolog information toohello application diagnostics log.</span></span> <span data-ttu-id="678c8-196">不過，您需要 toochange hello 程式碼並重新部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-196">However, you need toochange hello code and redeploy your application.</span></span> <span data-ttu-id="678c8-197">如果您的應用程式是在測試環境上執行，建議使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="678c8-197">This method is recommended if your app is running on a testing environment.</span></span>

<span data-ttu-id="678c8-198">如需有關的詳細指示 tooconfigure 應用程式的記錄，請參閱[啟用 Azure App Service 中的 web 應用程式的診斷記錄](web-sites-enable-diagnostic-log.md)。</span><span class="sxs-lookup"><span data-stu-id="678c8-198">For detailed instructions on how tooconfigure your application for logging, see [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>

#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="678c8-199">使用 hello Azure App Service 支援入口網站</span><span class="sxs-lookup"><span data-stu-id="678c8-199">Use hello Azure App Service support portal</span></span>
<span data-ttu-id="678c8-200">Web 應用程式為您提供 hello 能力 tootroubleshoot 問題相關的 tooyour web 應用程式藉由查看 HTTP 記錄檔、 事件記錄檔、 處理序傾印，等等。</span><span class="sxs-lookup"><span data-stu-id="678c8-200">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="678c8-201">您可以利用我們位於 **http://&lt;your app name>.scm.azurewebsites.net/Support** 的支援入口網站，存取所有這方面的資訊。</span><span class="sxs-lookup"><span data-stu-id="678c8-201">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="678c8-202">hello Azure App Service 支援入口網站為您提供三個個別索引標籤的常見的疑難排解情況 toosupport hello 三個步驟：</span><span class="sxs-lookup"><span data-stu-id="678c8-202">hello Azure App Service support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="678c8-203">觀察目前的行為</span><span class="sxs-lookup"><span data-stu-id="678c8-203">Observe current behavior</span></span>
2. <span data-ttu-id="678c8-204">收集診斷資訊及執行 hello 內建的分析器來分析</span><span class="sxs-lookup"><span data-stu-id="678c8-204">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="678c8-205">減輕問題</span><span class="sxs-lookup"><span data-stu-id="678c8-205">Mitigate</span></span>

<span data-ttu-id="678c8-206">如果立即發生 hello 問題，請按一下**分析** > **診斷** > **現在診斷**toocreate 為您的診斷工作階段以收集 HTTP 記錄檔、 事件檢視器記錄檔、 記憶體傾印、 PHP 錯誤記錄檔和 PHP 處理序報表。</span><span class="sxs-lookup"><span data-stu-id="678c8-206">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which collects HTTP logs, event viewer logs, memory dumps, PHP error logs, and PHP process report.</span></span>

<span data-ttu-id="678c8-207">一旦 hello 資料收集，hello 支援入口網站上 hello 資料執行分析，並提供您的 HTML 報表。</span><span class="sxs-lookup"><span data-stu-id="678c8-207">Once hello data is collected, hello support portal runs an analysis on hello data and provides you with an HTML report.</span></span>

<span data-ttu-id="678c8-208">如果您想 toodownload hello 資料，根據預設，它就會儲存在 hello D:\home\data\DaaS 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="678c8-208">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="678c8-209">如需有關 hello Azure App Service 支援入口網站的詳細資訊，請參閱[Azure 網站的網站擴充功能的新更新 tooSupport](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)。</span><span class="sxs-lookup"><span data-stu-id="678c8-209">For more information on hello Azure App Service support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="678c8-210">使用 hello Kudu 偵錯主控台</span><span class="sxs-lookup"><span data-stu-id="678c8-210">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="678c8-211">Web Apps 隨附可用於偵錯、探索、上傳檔案的偵錯主控台，以及可以取得您環境相關資訊的 JSON 端點。</span><span class="sxs-lookup"><span data-stu-id="678c8-211">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="678c8-212">此主控台稱為 hello *Kudu 主控台*或 hello *SCM 儀表板*web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-212">This console is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="678c8-213">您可以將 toohello 連結存取這個儀表板**https://&lt;應用程式名稱 >.scm.azurewebsites.net/**。</span><span class="sxs-lookup"><span data-stu-id="678c8-213">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="678c8-214">Kudu 提供的 hello 事項包括：</span><span class="sxs-lookup"><span data-stu-id="678c8-214">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="678c8-215">您的應用程式的環境設定</span><span class="sxs-lookup"><span data-stu-id="678c8-215">environment settings for your application</span></span>
* <span data-ttu-id="678c8-216">記錄檔串流</span><span class="sxs-lookup"><span data-stu-id="678c8-216">log stream</span></span>
* <span data-ttu-id="678c8-217">診斷傾印</span><span class="sxs-lookup"><span data-stu-id="678c8-217">diagnostic dump</span></span>
* <span data-ttu-id="678c8-218">您可以執行 Powershell Cmdlet 和基本 DOS 命令的偵錯主控台。</span><span class="sxs-lookup"><span data-stu-id="678c8-218">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="678c8-219">Kudu 另一個有用功能是，如果您的應用程式會擲回第一個出現的例外狀況，您可以使用 Kudu 與 hello SysInternals 工具 Procdump toocreate 記憶體傾印。</span><span class="sxs-lookup"><span data-stu-id="678c8-219">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="678c8-220">這些記憶體傾印是 hello 程序的快照集，並經常可協助您疑難排解您 web 應用程式更複雜的問題。</span><span class="sxs-lookup"><span data-stu-id="678c8-220">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="678c8-221">如需 Kudu 可用功能的詳細資訊，請參閱 [您應該知道的 Azure 網站 Team Services 工具](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)。</span><span class="sxs-lookup"><span data-stu-id="678c8-221">For more information on features available in Kudu, see [Azure Websites Team Services tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="678c8-222">3.減少 hello 問題</span><span class="sxs-lookup"><span data-stu-id="678c8-222">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="678c8-223">標尺 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="678c8-223">Scale hello web app</span></span>
<span data-ttu-id="678c8-224">在 Azure 應用程式服務，以增加的效能和輸送量，您可以調整 hello 小數位數，執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-224">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="678c8-225">向上擴充 web 應用程式牽涉到兩個相關的動作： 變更您應用程式服務計劃 tooa 較高的定價層，以及設定某些設定之後您切換 toohello 更高的定價層。</span><span class="sxs-lookup"><span data-stu-id="678c8-225">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="678c8-226">如需有關調整的詳細資訊，請參閱 [在 Azure App Service 中調整 Web 應用程式規模](web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="678c8-226">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="678c8-227">此外，您可以選擇 toorun 多個執行個體上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-227">Additionally, you can choose toorun your application on more than one instance.</span></span> <span data-ttu-id="678c8-228">相應放大不僅提供您更強大的處理能力，同時也提供您一定程度的容錯量。</span><span class="sxs-lookup"><span data-stu-id="678c8-228">Scaling out not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="678c8-229">如果上一個執行個體關閉 hello 程序，hello 其他執行個體會繼續 tooserve 要求。</span><span class="sxs-lookup"><span data-stu-id="678c8-229">If hello process goes down on one instance, hello other instances continue tooserve requests.</span></span>

<span data-ttu-id="678c8-230">您可以設定 hello toobe 手動或自動縮放比例。</span><span class="sxs-lookup"><span data-stu-id="678c8-230">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="678c8-231">使用 AutoHeal</span><span class="sxs-lookup"><span data-stu-id="678c8-231">Use AutoHeal</span></span>
<span data-ttu-id="678c8-232">AutoHeal 回收 hello 取決於您選擇 （例如組態變更、 要求、 記憶體為基礎的限制或 hello 時間需要 tooexecute 要求） 設定您的應用程式的背景工作處理序。</span><span class="sxs-lookup"><span data-stu-id="678c8-232">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="678c8-233">大部分的 hello 時間回收 hello 程序是 hello 最快方式 toorecover 問題。</span><span class="sxs-lookup"><span data-stu-id="678c8-233">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="678c8-234">您永遠可以重新啟動 hello web 應用程式從直接在 hello Azure 入口網站中的，雖然 AutoHeal 會自動為您。</span><span class="sxs-lookup"><span data-stu-id="678c8-234">Though you can always restart hello web app from directly within hello Azure portal, AutoHeal does it automatically for you.</span></span> <span data-ttu-id="678c8-235">您只需要 toodo 是 hello web 應用程式的根 web.config 中新增一些觸發程序。</span><span class="sxs-lookup"><span data-stu-id="678c8-235">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="678c8-236">這些設定會在 hello 相同方式即使您的應用程式並不是.Net 應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-236">These settings would work in hello same way even if your application is not a .Net app.</span></span>

<span data-ttu-id="678c8-237">如需詳細資訊，請參閱 [自動修復 Azure 網站](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="678c8-237">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="678c8-238">重新啟動 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="678c8-238">Restart hello web app</span></span>
<span data-ttu-id="678c8-239">重新啟動，通常是 hello 最簡單方式 toorecover 從單次發生問題。</span><span class="sxs-lookup"><span data-stu-id="678c8-239">Restarting is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="678c8-240">在 [hello [Azure 入口網站](https://portal.azure.com/)，在您的 web 應用程式] 刀鋒視窗中，您擁有 hello 選項 toostop 或重新啟動您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-240">On hello [Azure portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![重新啟動 web 應用程式 toosolve 效能問題](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

<span data-ttu-id="678c8-242">您也可以使用 Azure Powershell 管理 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="678c8-242">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="678c8-243">如需詳細資訊，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="678c8-243">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
