---
title: "App Service 中的 Web 應用程式效能變慢 | Microsoft Docs"
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
ms.openlocfilehash: 1cfe7ec37ad8b24a8bd9ab2bf67e95675a57b675
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a><span data-ttu-id="72c3f-104">針對 Azure App Service 中 Web 應用程式效能變慢的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="72c3f-104">Troubleshoot slow web app performance issues in Azure App Service</span></span>
<span data-ttu-id="72c3f-105">本文可協助您針對 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)中 Web 應用程式效能變慢的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="72c3f-105">This article helps you troubleshoot slow web app performance issues in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="72c3f-106">如果在本文章中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="72c3f-106">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="72c3f-107">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="72c3f-107">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="72c3f-108">請移至 [Azure 支援網站](https://azure.microsoft.com/support/options/) ，然後按一下 **取得支援**。</span><span class="sxs-lookup"><span data-stu-id="72c3f-108">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="72c3f-109">徵狀</span><span class="sxs-lookup"><span data-stu-id="72c3f-109">Symptom</span></span>
<span data-ttu-id="72c3f-110">當您瀏覽 Web 應用程式時，頁面載入緩慢且有時候會逾時。</span><span class="sxs-lookup"><span data-stu-id="72c3f-110">When you browse the web app, the pages load slowly and sometimes timeout.</span></span>

## <a name="cause"></a><span data-ttu-id="72c3f-111">原因</span><span class="sxs-lookup"><span data-stu-id="72c3f-111">Cause</span></span>
<span data-ttu-id="72c3f-112">此問題通常是因為應用程式層級問題所造成，例如：</span><span class="sxs-lookup"><span data-stu-id="72c3f-112">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="72c3f-113">網路要求耗費過長的時間</span><span class="sxs-lookup"><span data-stu-id="72c3f-113">network requests taking a long time</span></span>
* <span data-ttu-id="72c3f-114">應用程式程式碼或資料庫查詢的效率不佳</span><span class="sxs-lookup"><span data-stu-id="72c3f-114">application code or database queries being inefficient</span></span>
* <span data-ttu-id="72c3f-115">應用程式的記憶體/CPU 使用率過高</span><span class="sxs-lookup"><span data-stu-id="72c3f-115">application using high memory/CPU</span></span>
* <span data-ttu-id="72c3f-116">應用程式因例外狀況導致損毀</span><span class="sxs-lookup"><span data-stu-id="72c3f-116">application crashing due to an exception</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="72c3f-117">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="72c3f-117">Troubleshooting steps</span></span>
<span data-ttu-id="72c3f-118">疑難排解可以分成三種不同的工作，依序為：</span><span class="sxs-lookup"><span data-stu-id="72c3f-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="72c3f-119">觀察和監視應用程式行為</span><span class="sxs-lookup"><span data-stu-id="72c3f-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="72c3f-120">收集資料</span><span class="sxs-lookup"><span data-stu-id="72c3f-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="72c3f-121">減輕問題</span><span class="sxs-lookup"><span data-stu-id="72c3f-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="72c3f-122">[App Service Web Apps](/services/app-service/web/) 在每個步驟均提供您各種選項。</span><span class="sxs-lookup"><span data-stu-id="72c3f-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="72c3f-123">1.觀察和監視應用程式行為</span><span class="sxs-lookup"><span data-stu-id="72c3f-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="72c3f-124">追蹤服務健全狀況</span><span class="sxs-lookup"><span data-stu-id="72c3f-124">Track Service health</span></span>
<span data-ttu-id="72c3f-125">每次發生服務中斷或效能降低時，Microsoft Azure 就會發出公告。</span><span class="sxs-lookup"><span data-stu-id="72c3f-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="72c3f-126">您可以在 [Azure 入口網站](https://portal.azure.com/)上追蹤服務的健康情況。</span><span class="sxs-lookup"><span data-stu-id="72c3f-126">You can track the health of the service on the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="72c3f-127">如需詳細資訊，請參閱[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="72c3f-128">監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="72c3f-128">Monitor your web app</span></span>
<span data-ttu-id="72c3f-129">此選項可讓您了解應用程式是否有任何問題。</span><span class="sxs-lookup"><span data-stu-id="72c3f-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="72c3f-130">在 Web 應用程式刀鋒視窗中，按一下 [ **要求和錯誤** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="72c3f-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="72c3f-131">[計量] 刀鋒視窗會顯示所有可以加入的計量。</span><span class="sxs-lookup"><span data-stu-id="72c3f-131">The **Metric** blade shows you all the metrics you can add.</span></span>

<span data-ttu-id="72c3f-132">某些您可能想用以監視 Web 應用程式的計量為</span><span class="sxs-lookup"><span data-stu-id="72c3f-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="72c3f-133">平均記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="72c3f-133">Average memory working set</span></span>
* <span data-ttu-id="72c3f-134">平均回應時間</span><span class="sxs-lookup"><span data-stu-id="72c3f-134">Average response time</span></span>
* <span data-ttu-id="72c3f-135">CPU 時間</span><span class="sxs-lookup"><span data-stu-id="72c3f-135">CPU time</span></span>
* <span data-ttu-id="72c3f-136">記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="72c3f-136">Memory working set</span></span>
* <span data-ttu-id="72c3f-137">要求</span><span class="sxs-lookup"><span data-stu-id="72c3f-137">Requests</span></span>

![監視 Web 應用程式效能](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

<span data-ttu-id="72c3f-139">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="72c3f-139">For more information, see:</span></span>

* [<span data-ttu-id="72c3f-140">監視 Azure App Service 中的 Web Apps</span><span class="sxs-lookup"><span data-stu-id="72c3f-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="72c3f-141">接收警示通知</span><span class="sxs-lookup"><span data-stu-id="72c3f-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a><span data-ttu-id="72c3f-142">監視 Web 端點狀態</span><span class="sxs-lookup"><span data-stu-id="72c3f-142">Monitor web endpoint status</span></span>
<span data-ttu-id="72c3f-143">若您在**標準**定價層中執行 Web 應用程式，Web Apps 可讓您從三個地理位置監視兩個端點。</span><span class="sxs-lookup"><span data-stu-id="72c3f-143">If you are running your web app in the **Standard** pricing tier, Web Apps lets you monitor two endpoints from three geographic locations.</span></span>

<span data-ttu-id="72c3f-144">端點監視能讓您設定從不同地理位置執行，且用來測試 Web URL 之回應時間和運作時間的 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="72c3f-144">Endpoint monitoring configures web tests from geo-distributed locations that test response time and uptime of web URLs.</span></span> <span data-ttu-id="72c3f-145">這項測試會針對 Web URL 執行 HTTP GET 作業，以從每個位置判斷回應時間和執行時間。</span><span class="sxs-lookup"><span data-stu-id="72c3f-145">The test performs an HTTP GET operation on the web URL to determine the response time and uptime from each location.</span></span> <span data-ttu-id="72c3f-146">各個已設定的位置會每隔五分鐘執行一次測試。</span><span class="sxs-lookup"><span data-stu-id="72c3f-146">Each configured location runs a test every five minutes.</span></span>

<span data-ttu-id="72c3f-147">運作時間是透過 HTTP 回應碼來加以監視，而回應時間的測量單位是毫秒。</span><span class="sxs-lookup"><span data-stu-id="72c3f-147">Uptime is monitored using HTTP response codes, and response time is measured in milliseconds.</span></span> <span data-ttu-id="72c3f-148">如果 HTTP 回應碼大於或等於 400，或是當回應時間超過 30 秒時，監視測試即告失敗。</span><span class="sxs-lookup"><span data-stu-id="72c3f-148">A monitoring test fails if the HTTP response code is greater than or equal to 400 or if the response takes more than 30 seconds.</span></span> <span data-ttu-id="72c3f-149">如果所有指定位置上的端點監視測試全都成功，表示該端點可用。</span><span class="sxs-lookup"><span data-stu-id="72c3f-149">An endpoint is considered available if its monitoring tests succeed from all the specified locations.</span></span>

<span data-ttu-id="72c3f-150">若要設定，請參閱[監視 Azure App Service 中的應用程式](web-sites-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-150">To set it up, see [Monitor apps in Azure App Service](web-sites-monitor.md).</span></span>

<span data-ttu-id="72c3f-151">同時，亦請參閱 [讓 Azure 網站保持運作以及端點監視 - 對談來賓 Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) 的端點監視影片。</span><span class="sxs-lookup"><span data-stu-id="72c3f-151">Also, see [Keeping Azure Web Sites up plus Endpoint Monitoring - with Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) for a video on endpoint monitoring.</span></span>

#### <a name="application-performance-monitoring-using-extensions"></a><span data-ttu-id="72c3f-152">使用擴充功能的應用程式效能監視</span><span class="sxs-lookup"><span data-stu-id="72c3f-152">Application performance monitoring using Extensions</span></span>
<span data-ttu-id="72c3f-153">您也可以利用*網站擴充功能*監視應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="72c3f-153">You can also monitor your application performance by using *site extensions*.</span></span>

<span data-ttu-id="72c3f-154">每個 App Service Web 應用程式都提供可擴充的管理端點，讓您得以運用一套以網站擴充功能形式部署的強大工具。</span><span class="sxs-lookup"><span data-stu-id="72c3f-154">Each App Service web app provides an extensible management end point that allows you to use a powerful set of tools deployed as site extensions.</span></span> <span data-ttu-id="72c3f-155">擴充功能包括：</span><span class="sxs-lookup"><span data-stu-id="72c3f-155">Extensions include:</span></span> 

- <span data-ttu-id="72c3f-156">原始程式碼編輯器，例如 [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-156">Source code editors like [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx).</span></span> 
- <span data-ttu-id="72c3f-157">適用於已連線的資源的管理工具，例如連線到 Web 應用程式的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="72c3f-157">Management tools for connected resources such as a MySQL database connected to a web app.</span></span>

<span data-ttu-id="72c3f-158">[Azure Application Insights](/services/application-insights/) 和 [New Relic](/marketplace/partners/newrelic/newrelic/) 是兩個可用的效能監視網站擴充功能。</span><span class="sxs-lookup"><span data-stu-id="72c3f-158">[Azure Application Insights](/services/application-insights/) and [New Relic](/marketplace/partners/newrelic/newrelic/) are two of the performance monitoring site extensions that are available.</span></span> <span data-ttu-id="72c3f-159">若要使用 New Relic，您需要在執行階段安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="72c3f-159">To use New Relic, you install an agent at runtime.</span></span> <span data-ttu-id="72c3f-160">若要使用 Azure Application Insights，請透過 SDK 重建程式碼，您也可以安裝可存取其他資料的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="72c3f-160">To use Azure Application Insights, you rebuild your code with an SDK, and you can also install an extension that provides access to additional data.</span></span> <span data-ttu-id="72c3f-161">SDK 可讓您撰寫程式碼來監視應用程式的詳細使用狀況和效能。</span><span class="sxs-lookup"><span data-stu-id="72c3f-161">The SDK lets you write code to monitor the usage and performance of your app in more detail.</span></span>

<span data-ttu-id="72c3f-162">若要使用 Application Insights，請參閱 [監視 Web 應用程式的效能](../application-insights/app-insights-web-monitor-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-162">To use Application Insights, see [Monitor performance in web applications](../application-insights/app-insights-web-monitor-performance.md).</span></span>

<span data-ttu-id="72c3f-163">若要使用 New Relic，請參閱 [Azure 上的 New Relic 應用程式效能管理](../store-new-relic-cloud-services-dotnet-application-performance-management.md)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-163">To use New Relic, see [New Relic Application Performance Management on Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).</span></span>

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="72c3f-164">2.收集資料</span><span class="sxs-lookup"><span data-stu-id="72c3f-164">2. Collect data</span></span>
<span data-ttu-id="72c3f-165">Web Apps 環境會針對來自 Web 伺服器和 Web 應用程式的記錄資訊提供診斷功能。</span><span class="sxs-lookup"><span data-stu-id="72c3f-165">The Web Apps environment provides diagnostic functionality for logging information from both the web server and the web application.</span></span> <span data-ttu-id="72c3f-166">此資訊可區分為網頁伺服器診斷與應用程式診斷。</span><span class="sxs-lookup"><span data-stu-id="72c3f-166">The information is separated into web server diagnostics and application diagnostics.</span></span>

#### <a name="enable-web-server-diagnostics"></a><span data-ttu-id="72c3f-167">啟用網頁伺服器診斷</span><span class="sxs-lookup"><span data-stu-id="72c3f-167">Enable web server diagnostics</span></span>
<span data-ttu-id="72c3f-168">您可以啟用或停用下列各種記錄：</span><span class="sxs-lookup"><span data-stu-id="72c3f-168">You can enable or disable the following kinds of logs:</span></span>

* <span data-ttu-id="72c3f-169">**詳細的錯誤記錄** - 對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="72c3f-169">**Detailed Error Logging** - Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span> <span data-ttu-id="72c3f-170">這當中包含的資訊可協助您判斷為何伺服器傳回錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="72c3f-170">This may contain information that can help determine why the server returned the error code.</span></span>
* <span data-ttu-id="72c3f-171">**失敗的要求追蹤** - 關於失敗要求的詳細資訊，包括用於處理要求的 IIS 元件追蹤，以及每個元件所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="72c3f-171">**Failed Request Tracing** - Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span> <span data-ttu-id="72c3f-172">若您嘗試提升 Web 應用程式的效能，或是想要隔離造成特定 HTTP 錯誤的原因，這個方法將有所助益。</span><span class="sxs-lookup"><span data-stu-id="72c3f-172">This can be useful if you are attempting to improve web app performance or isolate what is causing a specific HTTP error.</span></span>
* <span data-ttu-id="72c3f-173">**Web 伺服器記錄** - 使用 W3C 擴充記錄檔格式的 HTTP 交易相關資訊。</span><span class="sxs-lookup"><span data-stu-id="72c3f-173">**Web Server Logging** - Information about HTTP transactions using the W3C extended log file format.</span></span> <span data-ttu-id="72c3f-174">當您需要判斷整體 Web 應用程式計量 (例如，所處理的要求數量，或來自特定 IP 位址要求的數量) 時，這個方法將有所助益。</span><span class="sxs-lookup"><span data-stu-id="72c3f-174">This is useful when determining overall web app metrics, such as the number of requests handled or how many requests are from a specific IP address.</span></span>

#### <a name="enable-application-diagnostics"></a><span data-ttu-id="72c3f-175">啟用應用程式診斷</span><span class="sxs-lookup"><span data-stu-id="72c3f-175">Enable application diagnostics</span></span>
<span data-ttu-id="72c3f-176">有幾個選項可收集來自 Web Apps 的效能資料、透過 Visual Studio 即時分析您的應用程式，或修改您的應用程式程式碼，以記錄詳細資訊和追蹤。</span><span class="sxs-lookup"><span data-stu-id="72c3f-176">There are several options to collect application performance data from Web Apps, profile your application live from Visual Studio, or modify your application code to log more information and traces.</span></span> <span data-ttu-id="72c3f-177">您可以根據您對應用程式擁有多少存取權，以及您從監視工具觀察到的內容來選擇選項。</span><span class="sxs-lookup"><span data-stu-id="72c3f-177">You can choose the options based on how much access you have to the application and what you observed from the monitoring tools.</span></span>

##### <a name="use-application-insights-profiler"></a><span data-ttu-id="72c3f-178">使用 Application Insights Profiler</span><span class="sxs-lookup"><span data-stu-id="72c3f-178">Use Application Insights Profiler</span></span>
<span data-ttu-id="72c3f-179">您可以啟用 Application Insights Profiler 以開始擷取詳細的效能追蹤。</span><span class="sxs-lookup"><span data-stu-id="72c3f-179">You can enable the Application Insights Profiler to start capturing detailed performance traces.</span></span> <span data-ttu-id="72c3f-180">當您要調查過去發生的問題時，可存取最多五天前擷取的追蹤。</span><span class="sxs-lookup"><span data-stu-id="72c3f-180">You can access traces captured up to five days ago when you need to investigate problems happened in the past.</span></span> <span data-ttu-id="72c3f-181">只要您有 Azure 入口網站上的 Web 應用程式之 Application Insights 資源的存取權，即可選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="72c3f-181">You can choose this option as long as you have access to the web app's Application Insights resource on Azure portal.</span></span>

<span data-ttu-id="72c3f-182">Application Insights Profiler 提供每個 Web 呼叫和追蹤之回應時間的統計資料，指出哪一行程式碼造成回應變慢。</span><span class="sxs-lookup"><span data-stu-id="72c3f-182">Application Insights Profiler provides statistics on response time for each web call and traces that indicates which line of code caused the slow responses.</span></span> <span data-ttu-id="72c3f-183">App Service 應用程式有時候會因為特定程式碼未以有效率的方式撰寫而變慢。</span><span class="sxs-lookup"><span data-stu-id="72c3f-183">Sometimes the App Service app is slow because certain code is not written in a performant way.</span></span> <span data-ttu-id="72c3f-184">範例包括可以平行執行以及在不想要的資料庫鎖定爭用中執行的循序程式碼。</span><span class="sxs-lookup"><span data-stu-id="72c3f-184">Examples include sequential code that can be run in parallel and undesired database lock contentions.</span></span> <span data-ttu-id="72c3f-185">在程式碼中移除這些瓶頸會增加應用程式的效能，但是如果沒有設定精細的追蹤和記錄，則難以偵測。</span><span class="sxs-lookup"><span data-stu-id="72c3f-185">Removing these bottlenecks in the code increases the app's performance, but they are hard to detect without setting up elaborate traces and logs.</span></span> <span data-ttu-id="72c3f-186">Application Insights Profiler 收集的追蹤有助於識別造成應用程式速度變慢的程式碼，並針對 App Service 應用程式克服這項挑戰。</span><span class="sxs-lookup"><span data-stu-id="72c3f-186">The traces collected by Application Insights Profiler helps identifying the lines of code that slows down the application and overcome this challenge for App Service apps.</span></span>

 <span data-ttu-id="72c3f-187">如需詳細資訊，請參閱[使用 Application Insights 來分析即時 Azure Web 應用程式](../application-insights/app-insights-profiler.md)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-187">For more information, see [Profiling live Azure web apps with Application Insights](../application-insights/app-insights-profiler.md).</span></span>

##### <a name="use-remote-profiling"></a><span data-ttu-id="72c3f-188">使用遠端分析</span><span class="sxs-lookup"><span data-stu-id="72c3f-188">Use Remote Profiling</span></span>
<span data-ttu-id="72c3f-189">您可在 Azure App Service、Web Apps、API Apps 和 WebJobs 進行遠端分析。</span><span class="sxs-lookup"><span data-stu-id="72c3f-189">In Azure App Service, Web Apps, API Apps, and WebJobs can be remotely profiled.</span></span> <span data-ttu-id="72c3f-190">如果您具備 Web 應用程式資源的存取權，而且知道如何重現問題，或如果您知道發生效能問題的精確時間間隔，請選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="72c3f-190">Choose this option if you have access to the web app resource and you know how to reproduce the issue, or if you know the exact time interval the performance issue happens.</span></span>

<span data-ttu-id="72c3f-191">如果 CPU 使用量偏高而且您的處理序執行速度比預期緩慢，此時遠端分析相當有用，或 HTTP 要求的延遲情形高於一般，您可以從遠端分析處理序，取得 CPU 取樣呼叫堆疊，來分析處理序活動和程式碼忙碌路徑。</span><span class="sxs-lookup"><span data-stu-id="72c3f-191">Remote Profiling is useful if the CPU usage of the process is high and your process is running slower than expected, or the latency of HTTP requests are higher than normal, you can remotely profile your process and get the CPU sampling call stacks to analyze the process activity and code hot paths.</span></span>

<span data-ttu-id="72c3f-192">如需詳細資訊，請參閱 [Azure App Service 中的遠端分析支援](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-192">For more information, see [Remote Profiling support in Azure App Service](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).</span></span>

##### <a name="set-up-diagnostic-traces-manually"></a><span data-ttu-id="72c3f-193">手動設定診斷追蹤</span><span class="sxs-lookup"><span data-stu-id="72c3f-193">Set up diagnostic traces manually</span></span>
<span data-ttu-id="72c3f-194">如果您具有 Web 應用程式原始程式碼的存取權，應用程式診斷功能可讓您擷取 Web 應用程式所產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="72c3f-194">If you have access to the web application source code, Application diagnostics enables you to capture information produced by a web application.</span></span> <span data-ttu-id="72c3f-195">ASP.NET 應用程式會使用 `System.Diagnostics.Trace` 類別將資訊記錄到應用程式診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="72c3f-195">ASP.NET applications can use the `System.Diagnostics.Trace` class to log information to the application diagnostics log.</span></span> <span data-ttu-id="72c3f-196">不過，您需要變更程式碼並重新部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="72c3f-196">However, you need to change the code and redeploy your application.</span></span> <span data-ttu-id="72c3f-197">如果您的應用程式是在測試環境上執行，建議使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="72c3f-197">This method is recommended if your app is running on a testing environment.</span></span>

<span data-ttu-id="72c3f-198">如需如何設定應用程式記錄功能的詳細指示，請參閱 [在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能](web-sites-enable-diagnostic-log.md)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-198">For detailed instructions on how to configure your application for logging, see [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>

#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="72c3f-199">使用 Azure App Service 支援入口網站</span><span class="sxs-lookup"><span data-stu-id="72c3f-199">Use the Azure App Service support portal</span></span>
<span data-ttu-id="72c3f-200">Web Apps 透過查看 HTTP 記錄檔、事件記錄檔、處理序傾印等，提供您疑難排解 Web 應用程式相關問題的能力。</span><span class="sxs-lookup"><span data-stu-id="72c3f-200">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="72c3f-201">您可以利用我們位於 **http://&lt;your app name>.scm.azurewebsites.net/Support** 的支援入口網站，存取所有這方面的資訊。</span><span class="sxs-lookup"><span data-stu-id="72c3f-201">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="72c3f-202">Azure App Service 支援入口網站提供三個不同的索引標籤，支援常見疑難排解案例的三個步驟：</span><span class="sxs-lookup"><span data-stu-id="72c3f-202">The Azure App Service support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="72c3f-203">觀察目前的行為</span><span class="sxs-lookup"><span data-stu-id="72c3f-203">Observe current behavior</span></span>
2. <span data-ttu-id="72c3f-204">藉由收集診斷資訊與執行內建分析器進行分析</span><span class="sxs-lookup"><span data-stu-id="72c3f-204">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="72c3f-205">減輕問題</span><span class="sxs-lookup"><span data-stu-id="72c3f-205">Mitigate</span></span>

<span data-ttu-id="72c3f-206">若問題現在正好發生，請按一下 [分析] > [診斷] > [立即診斷]，將為您建立診斷工作階段，該工作階段會收集 HTTP 記錄檔、事件檢視器記錄檔、記憶體傾印、PHP 錯誤記錄檔和 PHP 流程報表。</span><span class="sxs-lookup"><span data-stu-id="72c3f-206">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which collects HTTP logs, event viewer logs, memory dumps, PHP error logs, and PHP process report.</span></span>

<span data-ttu-id="72c3f-207">完成資料收集後，支援入口網站將對資料執行分析，並提供您一份 HTML 報表。</span><span class="sxs-lookup"><span data-stu-id="72c3f-207">Once the data is collected, the support portal runs an analysis on the data and provides you with an HTML report.</span></span>

<span data-ttu-id="72c3f-208">若您想下載資料，根據預設，資料會儲存在 D:\home\data\DaaS 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="72c3f-208">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="72c3f-209">如需有關 Azure App Service 支援入口網站的詳細資訊，請參閱[支援 Azure 網站的網站擴充功能最新更新](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-209">For more information on the Azure App Service support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="72c3f-210">使用 Kudu 偵錯主控台</span><span class="sxs-lookup"><span data-stu-id="72c3f-210">Use the Kudu Debug Console</span></span>
<span data-ttu-id="72c3f-211">Web Apps 隨附可用於偵錯、探索、上傳檔案的偵錯主控台，以及可以取得您環境相關資訊的 JSON 端點。</span><span class="sxs-lookup"><span data-stu-id="72c3f-211">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="72c3f-212">此主控台稱為 Web 應用程式的 *Kudu 主控台*或 *SCM 儀表板*。</span><span class="sxs-lookup"><span data-stu-id="72c3f-212">This console is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="72c3f-213">您可以前往連結 **https://&lt;Your app name>.scm.azurewebsites.net/** 存取此儀表板。</span><span class="sxs-lookup"><span data-stu-id="72c3f-213">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="72c3f-214">Kudu 提供的部分項目為：</span><span class="sxs-lookup"><span data-stu-id="72c3f-214">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="72c3f-215">您的應用程式的環境設定</span><span class="sxs-lookup"><span data-stu-id="72c3f-215">environment settings for your application</span></span>
* <span data-ttu-id="72c3f-216">記錄檔串流</span><span class="sxs-lookup"><span data-stu-id="72c3f-216">log stream</span></span>
* <span data-ttu-id="72c3f-217">診斷傾印</span><span class="sxs-lookup"><span data-stu-id="72c3f-217">diagnostic dump</span></span>
* <span data-ttu-id="72c3f-218">您可以執行 Powershell Cmdlet 和基本 DOS 命令的偵錯主控台。</span><span class="sxs-lookup"><span data-stu-id="72c3f-218">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="72c3f-219">Kudu 的另一項實用功能是，如果應用程式擲回第一次例外狀況，您可以使用 Kudu 和 SysInternals 工具 Procdump 建立記憶體傾印。</span><span class="sxs-lookup"><span data-stu-id="72c3f-219">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="72c3f-220">這些記憶體傾印是處理序的快照集，通常可以協助您疑難排解 Web 應用程式較複雜的問題。</span><span class="sxs-lookup"><span data-stu-id="72c3f-220">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="72c3f-221">如需 Kudu 可用功能的詳細資訊，請參閱 [您應該知道的 Azure 網站 Team Services 工具](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-221">For more information on features available in Kudu, see [Azure Websites Team Services tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="72c3f-222">3.減輕問題</span><span class="sxs-lookup"><span data-stu-id="72c3f-222">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="72c3f-223">調整 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="72c3f-223">Scale the web app</span></span>
<span data-ttu-id="72c3f-224">在 Azure App Service 中，為提高效能和輸送量，您可以調整所執行之應用程式的大小。</span><span class="sxs-lookup"><span data-stu-id="72c3f-224">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="72c3f-225">相應增加 Web 應用程式規模牽涉到兩個相關動作：將 App Service 方案變更為較高的定價層，以及在改為較高的定價層後進行某些設定。</span><span class="sxs-lookup"><span data-stu-id="72c3f-225">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="72c3f-226">如需有關調整的詳細資訊，請參閱 [在 Azure App Service 中調整 Web 應用程式規模](web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-226">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="72c3f-227">此外，您可以選擇在多個執行個體上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="72c3f-227">Additionally, you can choose to run your application on more than one instance.</span></span> <span data-ttu-id="72c3f-228">相應放大不僅提供您更強大的處理能力，同時也提供您一定程度的容錯量。</span><span class="sxs-lookup"><span data-stu-id="72c3f-228">Scaling out not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="72c3f-229">若流程在某個執行個體上中斷，其他執行個體會繼續處理要求。</span><span class="sxs-lookup"><span data-stu-id="72c3f-229">If the process goes down on one instance, the other instances continue to serve requests.</span></span>

<span data-ttu-id="72c3f-230">您可以將調整設定為手動或自動。</span><span class="sxs-lookup"><span data-stu-id="72c3f-230">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="72c3f-231">使用 AutoHeal</span><span class="sxs-lookup"><span data-stu-id="72c3f-231">Use AutoHeal</span></span>
<span data-ttu-id="72c3f-232">AutoHeal 會根據您選擇的設定 (例如組態變更、要求、以記憶體為基礎的限制或執行要求所需的時間)，回收應用程式的背景工作角色處理序。</span><span class="sxs-lookup"><span data-stu-id="72c3f-232">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="72c3f-233">在大部分情況下，回收處理序是從問題中復原的最快方式。</span><span class="sxs-lookup"><span data-stu-id="72c3f-233">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="72c3f-234">雖然您永遠可以從 Azure 入口網站中直接重新啟動 Web 應用程式，AutoHeal 會自動為您完成。</span><span class="sxs-lookup"><span data-stu-id="72c3f-234">Though you can always restart the web app from directly within the Azure portal, AutoHeal does it automatically for you.</span></span> <span data-ttu-id="72c3f-235">您只需要在 Web 應用程式的根目錄 web.config 中加入某些觸發程序。</span><span class="sxs-lookup"><span data-stu-id="72c3f-235">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="72c3f-236">即使您的應用程式並非 .Net 應用程式，這些設定的運作方式仍相同。</span><span class="sxs-lookup"><span data-stu-id="72c3f-236">These settings would work in the same way even if your application is not a .Net app.</span></span>

<span data-ttu-id="72c3f-237">如需詳細資訊，請參閱 [自動修復 Azure 網站](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-237">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="72c3f-238">重新啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="72c3f-238">Restart the web app</span></span>
<span data-ttu-id="72c3f-239">若要從一次性問題中復原，重新啟動通常是最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="72c3f-239">Restarting is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="72c3f-240">在 [Azure 入口網站](https://portal.azure.com/)上的 Web 應用程式刀鋒視窗中，有提供停止或重新啟動應用程式的選項。</span><span class="sxs-lookup"><span data-stu-id="72c3f-240">On the [Azure portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![重新啟動 Web 應用程式以解決效能問題](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

<span data-ttu-id="72c3f-242">您也可以使用 Azure Powershell 管理 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72c3f-242">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="72c3f-243">如需詳細資訊，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="72c3f-243">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
