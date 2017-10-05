---
title: "監視任何網站的可用性和回應性 | Microsoft Docs"
description: "在 Application Insights 中設定 Web 測試。 如果網站無法使用或回應緩慢，將收到警示。"
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 6c7f52fc3998b0b29301206ffbc6a5a0c4134f6a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a><span data-ttu-id="4d55d-104">監視任何網站的可用性和回應性</span><span class="sxs-lookup"><span data-stu-id="4d55d-104">Monitor availability and responsiveness of any web site</span></span>
<span data-ttu-id="4d55d-105">將 Web 應用程式或網站部署至任何伺服器之後，您可以設定測試來監視其可用性和回應性。</span><span class="sxs-lookup"><span data-stu-id="4d55d-105">After you've deployed your web app or web site to any server, you can set up tests to monitor its availability and responsiveness.</span></span> <span data-ttu-id="4d55d-106">[Azure Application Insights](app-insights-overview.md) 會將來自全球各地的 Web 要求定期傳送給您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d55d-106">[Azure Application Insights](app-insights-overview.md) sends web requests to your application at regular intervals from points around the world.</span></span> <span data-ttu-id="4d55d-107">如果應用程式沒有回應或回應太慢，則會警告您。</span><span class="sxs-lookup"><span data-stu-id="4d55d-107">It alerts you if your application doesn't respond, or responds slowly.</span></span>

<span data-ttu-id="4d55d-108">您可以為公用網際網路可存取的任何 HTTP 或 HTTPS 端點設定可用性測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-108">You can set up availability tests for any HTTP or HTTPS endpoint that is accessible from the public internet.</span></span> <span data-ttu-id="4d55d-109">您不需要在您測試的網站上加入任何東西。</span><span class="sxs-lookup"><span data-stu-id="4d55d-109">You don't have to add anything to the web site you're testing.</span></span> <span data-ttu-id="4d55d-110">甚至不必是您的網站︰您可以測試您依賴的 REST API 服務。</span><span class="sxs-lookup"><span data-stu-id="4d55d-110">It doesn't even have to be your site: you could test a REST API service on which you depend.</span></span>

<span data-ttu-id="4d55d-111">可用性測試有兩種：</span><span class="sxs-lookup"><span data-stu-id="4d55d-111">There are two types of availability tests:</span></span>

* <span data-ttu-id="4d55d-112">[URL Ping 測試](#create)：您可以在 Azure 入口網站中建立的簡單測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-112">[URL ping test](#create): a simple test that you can create in the Azure portal.</span></span>
* <span data-ttu-id="4d55d-113">[多步驟 Web 測試](#multi-step-web-tests)：您可以在 Visual Studio Enterprise 中建立並上傳至入口網站的測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-113">[Multi-step web test](#multi-step-web-tests): which you create in Visual Studio Enterprise and upload to the portal.</span></span>

<span data-ttu-id="4d55d-114">每個應用程式資源最多可以建立 25 項可用性測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-114">You can create up to 25 availability tests per application resource.</span></span>

## <span data-ttu-id="4d55d-115"><a name="create"></a>1.開啟可用性測試報告的資源</span><span class="sxs-lookup"><span data-stu-id="4d55d-115"><a name="create"></a>1. Open a resource for your availability test reports</span></span>

<span data-ttu-id="4d55d-116">**如果您已針對應用程式設定 Application Insights**，請在 [Azure 入口網站](https://portal.azure.com)中開啟其 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="4d55d-116">**If you have already configured Application Insights** for your web app, open its Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="4d55d-117">**或者，如果您想要在新的資源中查看報告，**請註冊 [Microsoft Azure](http://azure.com)，並移至 [Azure 入口網站](https://portal.azure.com)，然後建立 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="4d55d-117">**Or, if you want to see your reports in a new resource,** sign up to [Microsoft Azure](http://azure.com), go to the [Azure portal](https://portal.azure.com), and create an Application Insights resource.</span></span>

![New > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

<span data-ttu-id="4d55d-119">按一下 [所有資源]  ，以開啟新資源的 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4d55d-119">Click **All resources** to open the Overview blade for the new resource.</span></span>

## <span data-ttu-id="4d55d-120"><a name="setup"></a>2.建立 URL Ping 測試</span><span class="sxs-lookup"><span data-stu-id="4d55d-120"><a name="setup"></a>2. Create a URL ping test</span></span>
<span data-ttu-id="4d55d-121">開啟 [可用性] 刀鋒視窗並新增一項測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-121">Open the Availability blade and add a test.</span></span>

![Fill at least the URL of your website](./media/app-insights-monitor-web-app-availability/13-availability.png)

* <span data-ttu-id="4d55d-123">**URL** 可以是您想要測試的任何網頁，但必須可從公用網際網路看見它。</span><span class="sxs-lookup"><span data-stu-id="4d55d-123">**The URL** can be any web page you want to test, but it must be visible from the public internet.</span></span> <span data-ttu-id="4d55d-124">URL 可以包含查詢字串。</span><span class="sxs-lookup"><span data-stu-id="4d55d-124">The URL can include a query string.</span></span> <span data-ttu-id="4d55d-125">例如，您可以訓練一下您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d55d-125">So, for example, you can exercise your database a little.</span></span> <span data-ttu-id="4d55d-126">如果 URL 解析為重新導向，我們會跟隨它，最多 10 個重新導向。</span><span class="sxs-lookup"><span data-stu-id="4d55d-126">If the URL resolves to a redirect, we follow it up to 10 redirects.</span></span>
* <span data-ttu-id="4d55d-127">**剖析相依要求**︰若已核取這個選項，測試會要求影像、指令碼、樣式檔案以及其他屬於受測試網頁的檔案。</span><span class="sxs-lookup"><span data-stu-id="4d55d-127">**Parse dependent requests**: If this option is checked, the test requests images, scripts, style files, and other files that are part of the web page under test.</span></span> <span data-ttu-id="4d55d-128">記錄的回應時間包含取得這些檔案所需的時間。</span><span class="sxs-lookup"><span data-stu-id="4d55d-128">The recorded response time includes the time taken to get these files.</span></span> <span data-ttu-id="4d55d-129">如果無法在逾時內為整個測試成功下載所有這些資源，則測試將會失敗。</span><span class="sxs-lookup"><span data-stu-id="4d55d-129">The test fails if all these resources cannot be successfully downloaded within the timeout for the whole test.</span></span> 

    <span data-ttu-id="4d55d-130">如果未核取這個選項，測試只會要求您指定之 URL 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="4d55d-130">If the option is not checked, the test only requests the file at the URL you specified.</span></span>
* <span data-ttu-id="4d55d-131">**啟用重試**：若已核取這個選項，就會在短時間內進行重試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-131">**Enable retries**:  If this option is checked, when the test fails, it is retried after a short interval.</span></span> <span data-ttu-id="4d55d-132">只有在連續三次重試失敗後，才會回報失敗。</span><span class="sxs-lookup"><span data-stu-id="4d55d-132">A failure is reported only if three successive attempts fail.</span></span> <span data-ttu-id="4d55d-133">後續測試則會以一般測試頻率執行。</span><span class="sxs-lookup"><span data-stu-id="4d55d-133">Subsequent tests are then performed at the usual test frequency.</span></span> <span data-ttu-id="4d55d-134">重試會暫時停止，直到下次成功為止。</span><span class="sxs-lookup"><span data-stu-id="4d55d-134">Retry is temporarily suspended until the next success.</span></span> <span data-ttu-id="4d55d-135">此規則可個別套用在每個測試位置。</span><span class="sxs-lookup"><span data-stu-id="4d55d-135">This rule is applied independently at each test location.</span></span> <span data-ttu-id="4d55d-136">我們建議使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="4d55d-136">We recommend this option.</span></span> <span data-ttu-id="4d55d-137">平均來說，大約 80% 失敗會在重試後消失。</span><span class="sxs-lookup"><span data-stu-id="4d55d-137">On average, about 80% of failures disappear on retry.</span></span>
* <span data-ttu-id="4d55d-138">**測試頻率**：設定從每個測試位置執行測試的頻率。</span><span class="sxs-lookup"><span data-stu-id="4d55d-138">**Test frequency**: Sets how often the test is run from each test location.</span></span> <span data-ttu-id="4d55d-139">頻率為 5 分鐘且有五個測試位置，則您的網站平均每一分鐘會執行測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-139">With a frequency of five minutes and five test locations, your site is tested on average every minute.</span></span>
* <span data-ttu-id="4d55d-140">**測試位置** 是我們的伺服器將 Web 要求傳送至您的 URL 的位置。</span><span class="sxs-lookup"><span data-stu-id="4d55d-140">**Test locations** are the places from where our servers send web requests to your URL.</span></span> <span data-ttu-id="4d55d-141">請選擇多個位置，以便區分網站問題與網路問題。</span><span class="sxs-lookup"><span data-stu-id="4d55d-141">Choose more than one so that you can distinguish problems in your website from network issues.</span></span> <span data-ttu-id="4d55d-142">您最多可以選取 16 個位置。</span><span class="sxs-lookup"><span data-stu-id="4d55d-142">You can select up to 16 locations.</span></span>
* <span data-ttu-id="4d55d-143">**成功準則**：</span><span class="sxs-lookup"><span data-stu-id="4d55d-143">**Success criteria**:</span></span>

    <span data-ttu-id="4d55d-144">**測試逾時**：減少此值以警示回應變慢。</span><span class="sxs-lookup"><span data-stu-id="4d55d-144">**Test timeout**: Decrease this value to be alerted about slow responses.</span></span> <span data-ttu-id="4d55d-145">如果未在這段時間內收到您網站的回應，則測試會視為失敗。</span><span class="sxs-lookup"><span data-stu-id="4d55d-145">The test is counted as a failure if the responses from your site have not been received within this period.</span></span> <span data-ttu-id="4d55d-146">如果已選取 [剖析相依要求] ，則必須在這段時間內收到所有映像、樣式檔、指令碼和其他相依資源。</span><span class="sxs-lookup"><span data-stu-id="4d55d-146">If you selected **Parse dependent requests**, then all the images, style files, scripts, and other dependent resources must have been received within this period.</span></span>

    <span data-ttu-id="4d55d-147">**HTTP 回應**：視為成功的回覆狀態碼。</span><span class="sxs-lookup"><span data-stu-id="4d55d-147">**HTTP response**: The returned status code that is counted as a success.</span></span> <span data-ttu-id="4d55d-148">200 是表示已傳回標準 Web 網頁的代碼。</span><span class="sxs-lookup"><span data-stu-id="4d55d-148">200 is the code that indicates that a normal web page has been returned.</span></span>

    <span data-ttu-id="4d55d-149">**內容比對**：字串，例如「歡迎！</span><span class="sxs-lookup"><span data-stu-id="4d55d-149">**Content match**: a string, like "Welcome!"</span></span> <span data-ttu-id="4d55d-150">我們會測試每個回應中的區分大小寫完全相符。</span><span class="sxs-lookup"><span data-stu-id="4d55d-150">We test that an exact case-sensitive match occurs in every response.</span></span> <span data-ttu-id="4d55d-151">必須是單純字串，不含萬用字元。</span><span class="sxs-lookup"><span data-stu-id="4d55d-151">It must be a plain string, without wildcards.</span></span> <span data-ttu-id="4d55d-152">別忘了，如果頁面內容變更，則可能需要更新。</span><span class="sxs-lookup"><span data-stu-id="4d55d-152">Don't forget that if your page content changes you might have to update it.</span></span>
* <span data-ttu-id="4d55d-153"> 傳送給您。</span><span class="sxs-lookup"><span data-stu-id="4d55d-153">**Alerts** are, by default, sent to you if there are failures in three locations over five minutes.</span></span> <span data-ttu-id="4d55d-154">某個位置的失敗很可能是網路問題，而不是您的網站發生問題。</span><span class="sxs-lookup"><span data-stu-id="4d55d-154">A failure in one location is likely to be a network problem, and not a problem with your site.</span></span> <span data-ttu-id="4d55d-155">但您可以將臨界值變更為更敏感或更不敏感，也可以變更應該將電子郵件傳送給哪一個人。</span><span class="sxs-lookup"><span data-stu-id="4d55d-155">But you can change the threshold to be more or less sensitive, and you can also change who the emails should be sent to.</span></span>

    <span data-ttu-id="4d55d-156">您可以設定會在產生警示時呼叫的 [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-156">You can set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span> <span data-ttu-id="4d55d-157">(不過請注意，查詢參數目前不會當作屬性傳遞)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-157">(But note that, at present, query parameters are not passed through as Properties.)</span></span>

### <a name="test-more-urls"></a><span data-ttu-id="4d55d-158">測試更多 URL</span><span class="sxs-lookup"><span data-stu-id="4d55d-158">Test more URLs</span></span>
<span data-ttu-id="4d55d-159">加入更多測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-159">Add more tests.</span></span> <span data-ttu-id="4d55d-160">例如，除了測試首頁以外，您也可以測試搜尋的 URL 來確定資料庫在執行中。</span><span class="sxs-lookup"><span data-stu-id="4d55d-160">For example, In addition to testing your home page, you can make sure your database is running by testing the URL for a search.</span></span>


## <span data-ttu-id="4d55d-161"><a name="monitor"></a>3.查看可用性測試結果</span><span class="sxs-lookup"><span data-stu-id="4d55d-161"><a name="monitor"></a>3. See your availability test results</span></span>

<span data-ttu-id="4d55d-162">數分鐘之後，按一下 [重新整理] 來查看測試結果。</span><span class="sxs-lookup"><span data-stu-id="4d55d-162">After a few minutes, click **Refresh** to see test results.</span></span> 

![首頁刀鋒視窗上的摘要結果](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

<span data-ttu-id="4d55d-164">散佈圖會顯示測試結果的範例，其中包含診斷測試步驟詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4d55d-164">The scatterplot shows samples of the test results that have diagnostic test-step detail in them.</span></span> <span data-ttu-id="4d55d-165">測試引擎會儲存失敗測試的診斷詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4d55d-165">The test engine stores diagnostic detail for tests that have failures.</span></span> <span data-ttu-id="4d55d-166">對於成功的測試，系統會儲存執行子集的診斷詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4d55d-166">For successful tests, diagnostic details are stored for a subset of the executions.</span></span> <span data-ttu-id="4d55d-167">將滑鼠停留在任何綠點/紅點上，以查看測試時間戳記、測試持續期間、位置和測試名稱。</span><span class="sxs-lookup"><span data-stu-id="4d55d-167">Hover over any of the green/red dots to see the test timestamp, test duration, location, and test name.</span></span> <span data-ttu-id="4d55d-168">點選散佈圖中的任何點以查看測試結果的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4d55d-168">Click through any dot in the scatter plot to see the details of the test result.</span></span>  

<span data-ttu-id="4d55d-169">選取特定測試、位置，或縮短時間週期，以查看更多有關感興趣時間週期的結果。</span><span class="sxs-lookup"><span data-stu-id="4d55d-169">Select a particular test, location, or reduce the time period to see more results around the time period of interest.</span></span> <span data-ttu-id="4d55d-170">使用 [搜尋總管] 以查看所有執行的結果，或使用分析查詢對此資料執行自訂報告。</span><span class="sxs-lookup"><span data-stu-id="4d55d-170">Use Search Explorer to see results from all executions, or use Analytics queries to run custom reports on this data.</span></span>

<span data-ttu-id="4d55d-171">除了未經處理的結果，[計量瀏覽器] 中有兩個可用性計量︰</span><span class="sxs-lookup"><span data-stu-id="4d55d-171">In addition to the raw results, there are two Availability metrics in Metrics Explorer:</span></span> 

1. <span data-ttu-id="4d55d-172">可用性︰所有測試執行中測試成功的百分比。</span><span class="sxs-lookup"><span data-stu-id="4d55d-172">Availability: Percentage of the tests that were successful, across all test executions.</span></span> 
2. <span data-ttu-id="4d55d-173">測試持續期間︰所有測試執行中的平均測試持續期間。</span><span class="sxs-lookup"><span data-stu-id="4d55d-173">Test Duration: Average test duration across all test executions.</span></span>

<span data-ttu-id="4d55d-174">您可以對測試名稱、位置套用篩選條件，以分析特定測試及/或位置的趨勢。</span><span class="sxs-lookup"><span data-stu-id="4d55d-174">You can apply filters on the test name, location to analyze trends of a particular test and/or location.</span></span>

## <span data-ttu-id="4d55d-175"><a name="edit"></a> 檢查和編輯測試</span><span class="sxs-lookup"><span data-stu-id="4d55d-175"><a name="edit"></a> Inspect and edit tests</span></span>

<span data-ttu-id="4d55d-176">從摘要頁面中，選取特定測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-176">From the summary page, select a specific test.</span></span> <span data-ttu-id="4d55d-177">您可以在該頁面中看見其特定結果，並加以編輯或暫時將它停用。</span><span class="sxs-lookup"><span data-stu-id="4d55d-177">There, you can see its specific results, and edit or temporarily disable it.</span></span>

![Edit or disable a web test](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

<span data-ttu-id="4d55d-179">當您對服務執行維護時，您可能會想要停用可用性測試或與其相關聯的警示規則。</span><span class="sxs-lookup"><span data-stu-id="4d55d-179">You might want to disable availability tests or the alert rules associated with them while you are performing maintenance on your service.</span></span> 

## <span data-ttu-id="4d55d-180"><a name="failures"></a>如果您看到失敗</span><span class="sxs-lookup"><span data-stu-id="4d55d-180"><a name="failures"></a>If you see failures</span></span>
<span data-ttu-id="4d55d-181">按一下一個紅點。</span><span class="sxs-lookup"><span data-stu-id="4d55d-181">Click a red dot.</span></span>

![按一下一個紅點](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


<span data-ttu-id="4d55d-183">從可用性測試結果，您可以：</span><span class="sxs-lookup"><span data-stu-id="4d55d-183">From an availability test result, you can:</span></span>

* <span data-ttu-id="4d55d-184">檢查從伺服器收到的回應。</span><span class="sxs-lookup"><span data-stu-id="4d55d-184">Inspect the response received from your server.</span></span>
* <span data-ttu-id="4d55d-185">在處理失敗的要求執行個體時，開啟應用程式伺服器所傳送的遙測。</span><span class="sxs-lookup"><span data-stu-id="4d55d-185">Open the telemetry sent by your server app while processing the failed request instance.</span></span>
* <span data-ttu-id="4d55d-186">在 Git 或 VSTS 中記錄問題或工作項目來追蹤問題。</span><span class="sxs-lookup"><span data-stu-id="4d55d-186">Log an issue or work item in Git or VSTS to track the problem.</span></span> <span data-ttu-id="4d55d-187">Bug 將包含此事件的連結。</span><span class="sxs-lookup"><span data-stu-id="4d55d-187">The bug will contain a link to this event.</span></span>
* <span data-ttu-id="4d55d-188">在 Visual Studio 中開啟 Web 測試結果。</span><span class="sxs-lookup"><span data-stu-id="4d55d-188">Open the web test result in Visual Studio.</span></span>


<span data-ttu-id="4d55d-189">*看起來正常，但回報為失敗？*</span><span class="sxs-lookup"><span data-stu-id="4d55d-189">*Looks OK but reported as a failure?*</span></span> <span data-ttu-id="4d55d-190">請檢查所有映像、指令碼、樣式表和頁面載入的任何其他檔案。</span><span class="sxs-lookup"><span data-stu-id="4d55d-190">Check all the images, scripts, style sheets, and any other files loaded by the page.</span></span> <span data-ttu-id="4d55d-191">如果其中有任何一個失敗，即使主要的 html 頁面載入正常，測試皆會回報為失敗。</span><span class="sxs-lookup"><span data-stu-id="4d55d-191">If any of them fails, the test is reported as failed, even if the main html page loads OK.</span></span>

<span data-ttu-id="4d55d-192">沒有相關項目？</span><span class="sxs-lookup"><span data-stu-id="4d55d-192">*No related items?*</span></span> <span data-ttu-id="4d55d-193">如果您已針對伺服器端應用程式設定 Application Insights，這可能是因為正在進行[取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-193">If you have Application Insights set up for your server-side application, that may be because [sampling](app-insights-sampling.md) is in operation.</span></span> 

## <a name="multi-step-web-tests"></a><span data-ttu-id="4d55d-194">多重步驟 Web 測試</span><span class="sxs-lookup"><span data-stu-id="4d55d-194">Multi-step web tests</span></span>
<span data-ttu-id="4d55d-195">您可以監視涉及一連串 URL 的案例。</span><span class="sxs-lookup"><span data-stu-id="4d55d-195">You can monitor a scenario that involves a sequence of URLs.</span></span> <span data-ttu-id="4d55d-196">例如，如果您正在監視銷售網站，您可以測試將項目加入購物車正確運作。</span><span class="sxs-lookup"><span data-stu-id="4d55d-196">For example, if you are monitoring a sales website, you can test that adding items to the shopping cart works correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="4d55d-197">進行多步驟 Web 測試此會收取費用。</span><span class="sxs-lookup"><span data-stu-id="4d55d-197">There is a charge for multi-step web tests.</span></span> <span data-ttu-id="4d55d-198">[價格方案](http://azure.microsoft.com/pricing/details/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-198">[Pricing scheme](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>
> 

<span data-ttu-id="4d55d-199">若要建立多重步驟測試，您可以使用 Visual Studio Enterprise 來記錄案例，然後將記錄結果上傳至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="4d55d-199">To create a multi-step test, you record the scenario by using Visual Studio Enterprise, and then upload the recording to Application Insights.</span></span> <span data-ttu-id="4d55d-200">Application Insights 會不時地重新執行案例，並確認回應。</span><span class="sxs-lookup"><span data-stu-id="4d55d-200">Application Insights replays the scenario at intervals and verifies the responses.</span></span>

> [!NOTE]
> <span data-ttu-id="4d55d-201">您無法在測試中使用已編碼的函式或迴圈。</span><span class="sxs-lookup"><span data-stu-id="4d55d-201">You can't use coded functions or loops in your tests.</span></span> <span data-ttu-id="4d55d-202">測試必須完全包含於 .webtest 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="4d55d-202">The test must be contained completely in the .webtest script.</span></span> <span data-ttu-id="4d55d-203">不過，您可以使用標準外掛程式。</span><span class="sxs-lookup"><span data-stu-id="4d55d-203">However, you can use standard plugins.</span></span>
>

#### <a name="1-record-a-scenario"></a><span data-ttu-id="4d55d-204">1.記錄案例</span><span class="sxs-lookup"><span data-stu-id="4d55d-204">1. Record a scenario</span></span>
<span data-ttu-id="4d55d-205">使用 Visual Studio Enterprise 來記錄 Web 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4d55d-205">Use Visual Studio Enterprise to record a web session.</span></span>

1. <span data-ttu-id="4d55d-206">建立 Web 效能測試專案。</span><span class="sxs-lookup"><span data-stu-id="4d55d-206">Create a Web performance test project.</span></span>

    ![在 Visual Studio Enterprise 版本中，從「Web 效能」和「負載測試」範本建立專案。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * <span data-ttu-id="4d55d-208">*沒看見 Web 效能和負載測試範本嗎？*</span><span class="sxs-lookup"><span data-stu-id="4d55d-208">*Don't see the Web Performance and Load Test template?*</span></span> <span data-ttu-id="4d55d-209">- 關閉 Visual Studio Enterprise。</span><span class="sxs-lookup"><span data-stu-id="4d55d-209">- Close Visual Studio Enterprise.</span></span> <span data-ttu-id="4d55d-210">開啟 [Visual Studio 安裝程式] 以修改 Visual Studio Enterprise 安裝。</span><span class="sxs-lookup"><span data-stu-id="4d55d-210">Open **Visual Studio Installer** to modify your Visual Studio Enterprise installation.</span></span> <span data-ttu-id="4d55d-211">在 [個別元件] 之下，選取 [Web 效能和負載測試工具]。</span><span class="sxs-lookup"><span data-stu-id="4d55d-211">Under **Individual Components**, select **Web Performance and load testing tools**.</span></span>

2. <span data-ttu-id="4d55d-212">開啟 .webtest 檔案，並開始記錄。</span><span class="sxs-lookup"><span data-stu-id="4d55d-212">Open the .webtest file and start recording.</span></span>

    ![開啟 .webtest 檔案，然後按一下 [記錄]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. <span data-ttu-id="4d55d-214">執行您想要在測試中模擬的使用者動作：開啟網站、將產品加入購物車等等。</span><span class="sxs-lookup"><span data-stu-id="4d55d-214">Do the user actions you want to simulate in your test: open your website, add a product to the cart, and so on.</span></span> <span data-ttu-id="4d55d-215">然後停止測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-215">Then stop your test.</span></span>

    ![在 Internet Explorer 中執行 Web 測試錄製器。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    <span data-ttu-id="4d55d-217">不要讓案例太長。</span><span class="sxs-lookup"><span data-stu-id="4d55d-217">Don't make a long scenario.</span></span> <span data-ttu-id="4d55d-218">以 100 個步驟和 2 分鐘為限。</span><span class="sxs-lookup"><span data-stu-id="4d55d-218">There's a limit of 100 steps and 2 minutes.</span></span>
4. <span data-ttu-id="4d55d-219">編輯本測試以進行下列事項：</span><span class="sxs-lookup"><span data-stu-id="4d55d-219">Edit the test to:</span></span>

   * <span data-ttu-id="4d55d-220">加入驗證以檢查收到的文字和回應碼。</span><span class="sxs-lookup"><span data-stu-id="4d55d-220">Add validations to check the received text and response codes.</span></span>
   * <span data-ttu-id="4d55d-221">移除任何多餘的互動。</span><span class="sxs-lookup"><span data-stu-id="4d55d-221">Remove any superfluous interactions.</span></span> <span data-ttu-id="4d55d-222">您也可以移除圖片或廣告或追蹤網站的相依要求。</span><span class="sxs-lookup"><span data-stu-id="4d55d-222">You could also remove dependent requests for pictures or to ad or tracking sites.</span></span>

     <span data-ttu-id="4d55d-223">請記住您只能編輯此測試指令碼 - 您無法加入自訂程式碼或呼叫其他 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-223">Remember that you can only edit the test script - you can't add custom code or call other web tests.</span></span> <span data-ttu-id="4d55d-224">請勿在此測試中插入迴圈。</span><span class="sxs-lookup"><span data-stu-id="4d55d-224">Don't insert loops in the test.</span></span> <span data-ttu-id="4d55d-225">您可以使用標準 Web 測試的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="4d55d-225">You can use standard web test plug-ins.</span></span>
5. <span data-ttu-id="4d55d-226">在 Visual Studio 中執行測試，以確定可以運作。</span><span class="sxs-lookup"><span data-stu-id="4d55d-226">Run the test in Visual Studio to make sure it works.</span></span>

    <span data-ttu-id="4d55d-227">Web 測試執行器會開啟網頁瀏覽器，並重複您已記錄的動作。</span><span class="sxs-lookup"><span data-stu-id="4d55d-227">The web test runner opens a web browser and repeats the actions you recorded.</span></span> <span data-ttu-id="4d55d-228">請確定運作如您所預期。</span><span class="sxs-lookup"><span data-stu-id="4d55d-228">Make sure it works as you expect.</span></span>

    ![在 Visual Studio 中，開啟 .webtest 檔案，並按一下 [執行]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-the-web-test-to-application-insights"></a><span data-ttu-id="4d55d-230">2.將 Web 測試上傳至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="4d55d-230">2. Upload the web test to Application Insights</span></span>
1. <span data-ttu-id="4d55d-231">在 Application Insights 入口網站中，建立 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-231">In the Application Insights portal, create a web test.</span></span>

    ![在 [Web 測試] 刀鋒視窗中，選擇 [加入]。](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. <span data-ttu-id="4d55d-233">選取多重步驟測試，並上傳 .webtest 檔案。</span><span class="sxs-lookup"><span data-stu-id="4d55d-233">Select multi-step test, and upload the .webtest file.</span></span>

    ![選取 [多步驟 Web 測試]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    <span data-ttu-id="4d55d-235">以進行 ping 測試的相同方式設定測試位置、頻率及警示參數。</span><span class="sxs-lookup"><span data-stu-id="4d55d-235">Set the test locations, frequency, and alert parameters in the same way as for ping tests.</span></span>

#### <a name="3-see-the-results"></a><span data-ttu-id="4d55d-236">3.查看結果</span><span class="sxs-lookup"><span data-stu-id="4d55d-236">3. See the results</span></span>

<span data-ttu-id="4d55d-237">就像在單一 URL 測試中一樣，以相同的方式檢視您的測試結果和任何失敗項目。</span><span class="sxs-lookup"><span data-stu-id="4d55d-237">View your test results and any failures in the same way as single-url tests.</span></span>

<span data-ttu-id="4d55d-238">此外，您可以下載測試結果，以在 Visual Studio 中檢視。</span><span class="sxs-lookup"><span data-stu-id="4d55d-238">In addition, you can download the test results to view them in Visual Studio.</span></span>

#### <a name="too-many-failures"></a><span data-ttu-id="4d55d-239">太多失敗項目？</span><span class="sxs-lookup"><span data-stu-id="4d55d-239">Too many failures?</span></span>

* <span data-ttu-id="4d55d-240">失敗的常見原因是在測試執行太長。</span><span class="sxs-lookup"><span data-stu-id="4d55d-240">A common reason for failure is that the test runs too long.</span></span> <span data-ttu-id="4d55d-241">不可執行超過兩分鐘。</span><span class="sxs-lookup"><span data-stu-id="4d55d-241">It mustn't run longer than two minutes.</span></span>

* <span data-ttu-id="4d55d-242">別忘了，必須正確載入頁面的所有資源，測試才能成功 (包括指令碼、樣式表、映像等等)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-242">Don't forget that all the resources of a page must load correctly for the test to succeed, including scripts, style sheets, images, and so forth.</span></span>

* <span data-ttu-id="4d55d-243">Web 測試必須完全包含在 .webtest 指令碼中：您無法在測試中使用編碼的函式。</span><span class="sxs-lookup"><span data-stu-id="4d55d-243">The web test must be entirely contained in the .webtest script: you can't use coded functions in the test.</span></span>

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a><span data-ttu-id="4d55d-244">將時間和隨機數字插入多重步驟測試中</span><span class="sxs-lookup"><span data-stu-id="4d55d-244">Plugging time and random numbers into your multi-step test</span></span>
<span data-ttu-id="4d55d-245">假設您要測試的工具會從外部來源取得與時間相關的資料 (例如股票)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-245">Suppose you're testing a tool that gets time-dependent data such as stocks from an external feed.</span></span> <span data-ttu-id="4d55d-246">當您記錄 Web 測試時，您必須使用特定的時間，但您將它們設為測試的參數：StartTime 和 EndTime。</span><span class="sxs-lookup"><span data-stu-id="4d55d-246">When you record your web test, you have to use specific times, but you set them as parameters of the test, StartTime and EndTime.</span></span>

![具有參數的 Web 測試。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

<span data-ttu-id="4d55d-248">當您執行測試時，希望 EndTime 永遠為目前時間，而 StartTime 為 15 分鐘前。</span><span class="sxs-lookup"><span data-stu-id="4d55d-248">When you run the test, you'd like EndTime always to be the present time, and StartTime should be 15 minutes ago.</span></span>

<span data-ttu-id="4d55d-249">Web 測試外掛程式提供將時間參數化的方法。</span><span class="sxs-lookup"><span data-stu-id="4d55d-249">Web Test Plug-ins provide the way to do parameterize times.</span></span>

1. <span data-ttu-id="4d55d-250">針對您想要的每個變數參數值，各加入一個 Web 測試外掛程式。</span><span class="sxs-lookup"><span data-stu-id="4d55d-250">Add a web test plug-in for each variable parameter value you want.</span></span> <span data-ttu-id="4d55d-251">在 Web 測試工具列中，選擇 [加入 Web 測試外掛程式] 。</span><span class="sxs-lookup"><span data-stu-id="4d55d-251">In the web test toolbar, choose **Add Web Test Plugin**.</span></span>

    ![選擇 [加入 Web 測試外掛程式]，然後選取類型。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    <span data-ttu-id="4d55d-253">在此範例中，我們會使用兩個日期時間外掛程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="4d55d-253">In this example, we use two instances of the Date Time Plug-in.</span></span> <span data-ttu-id="4d55d-254">一個執行個體設定為 "15 minutes ago"，另一個則設定為 "now"。</span><span class="sxs-lookup"><span data-stu-id="4d55d-254">One instance is for "15 minutes ago" and another for "now."</span></span>
2. <span data-ttu-id="4d55d-255">開啟每個外掛程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="4d55d-255">Open the properties of each plug-in.</span></span> <span data-ttu-id="4d55d-256">為屬性命名，然後將它設為使用目前時間。</span><span class="sxs-lookup"><span data-stu-id="4d55d-256">Give it a name and set it to use the current time.</span></span> <span data-ttu-id="4d55d-257">對其中一個，設定 [加入分鐘] = -15。</span><span class="sxs-lookup"><span data-stu-id="4d55d-257">For one of them, set Add Minutes = -15.</span></span>

    ![設定 [名稱]、[使用目前時間] 和 [加入分鐘]。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. <span data-ttu-id="4d55d-259">在 Web 測試參數中，使用 {{plug-in name}} 來參考外掛程式名稱。</span><span class="sxs-lookup"><span data-stu-id="4d55d-259">In the web test parameters, use {{plug-in name}} to reference a plug-in name.</span></span>

    ![在測試參數中，使用 {{plug-in name}}。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

<span data-ttu-id="4d55d-261">現在將您的測試上傳至入口網站。</span><span class="sxs-lookup"><span data-stu-id="4d55d-261">Now, upload your test to the portal.</span></span> <span data-ttu-id="4d55d-262">在每次執行測試時，它會使用動態值。</span><span class="sxs-lookup"><span data-stu-id="4d55d-262">It uses the dynamic values on every run of the test.</span></span>

## <a name="dealing-with-sign-in"></a><span data-ttu-id="4d55d-263">處理登入</span><span class="sxs-lookup"><span data-stu-id="4d55d-263">Dealing with sign-in</span></span>
<span data-ttu-id="4d55d-264">如果使用者登入您的應用程式，您有許多模擬登入的選項，以便在登入後方測試頁面。</span><span class="sxs-lookup"><span data-stu-id="4d55d-264">If your users sign in to your app, you have various options for simulating sign-in so that you can test pages behind the sign-in.</span></span> <span data-ttu-id="4d55d-265">您使用的方法取決於應用程式所提供的安全性類型。</span><span class="sxs-lookup"><span data-stu-id="4d55d-265">The approach you use depends on the type of security provided by the app.</span></span>

<span data-ttu-id="4d55d-266">在所有情況下，您應該只為了測試用途在您的應用程式中建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d55d-266">In all cases, you should create an account in your application just for the purpose of testing.</span></span> <span data-ttu-id="4d55d-267">可能的話，限制此測試帳戶的權限，讓 Web 測試不可能影響實際使用者。</span><span class="sxs-lookup"><span data-stu-id="4d55d-267">If possible, restrict the permissions of this test account so that there's no possibility of the web tests affecting real users.</span></span>

### <a name="simple-username-and-password"></a><span data-ttu-id="4d55d-268">簡單的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="4d55d-268">Simple username and password</span></span>
<span data-ttu-id="4d55d-269">以一般方式記錄 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-269">Record a web test in the usual way.</span></span> <span data-ttu-id="4d55d-270">先刪除 Cookie。</span><span class="sxs-lookup"><span data-stu-id="4d55d-270">Delete cookies first.</span></span>

### <a name="saml-authentication"></a><span data-ttu-id="4d55d-271">SAML 驗證</span><span class="sxs-lookup"><span data-stu-id="4d55d-271">SAML authentication</span></span>
<span data-ttu-id="4d55d-272">使用適用於 Web 測試的 SAML 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="4d55d-272">Use the SAML plugin that is available for web tests.</span></span>

### <a name="client-secret"></a><span data-ttu-id="4d55d-273">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="4d55d-273">Client secret</span></span>
<span data-ttu-id="4d55d-274">如果應用程式的登入路由牽涉到用戶端密碼，請使用此路由。</span><span class="sxs-lookup"><span data-stu-id="4d55d-274">If your app has a sign-in route that involves a client secret, use that route.</span></span> <span data-ttu-id="4d55d-275">Azure Active Directory (AAD) 是可提供用戶端密碼登入的服務範例。</span><span class="sxs-lookup"><span data-stu-id="4d55d-275">Azure Active Directory (AAD) is an example of a service that provides a client secret sign-in.</span></span> <span data-ttu-id="4d55d-276">在 AAD 中，用戶端密碼是應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="4d55d-276">In AAD, the client secret is the App Key.</span></span>

<span data-ttu-id="4d55d-277">以下是使用應用程式金鑰之 Azure Web 應用程式的 Web 測試範例︰</span><span class="sxs-lookup"><span data-stu-id="4d55d-277">Here's a sample web test of an Azure web app using an app key:</span></span>

![用戶端密碼範例](./media/app-insights-monitor-web-app-availability/110.png)

1. <span data-ttu-id="4d55d-279">從使用用戶端密鑰 (AppKey) 的 AAD 取得權杖。</span><span class="sxs-lookup"><span data-stu-id="4d55d-279">Get token from AAD using client secret (AppKey).</span></span>
2. <span data-ttu-id="4d55d-280">從回應中擷取持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="4d55d-280">Extract bearer token from response.</span></span>
3. <span data-ttu-id="4d55d-281">使用授權標頭中的持有人權杖呼叫 API。</span><span class="sxs-lookup"><span data-stu-id="4d55d-281">Call API using bearer token in the authorization header.</span></span>

<span data-ttu-id="4d55d-282">請確定 Web 測試是實際的用戶端 (也就是，在 AAD 中具有自己的應用程式) 並使用其 clientId + appkey。</span><span class="sxs-lookup"><span data-stu-id="4d55d-282">Make sure that the web test is an actual client - that is, it has its own app in AAD - and use its clientId + appkey.</span></span> <span data-ttu-id="4d55d-283">您測試中的服務在 AAD 中也有自己的應用程式︰此應用程式的 appID URI 會反映於 [資源] 欄位中的 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-283">Your service under test also has its own app in AAD: the appID URI of this app is reflected in the web test in the “resource” field.</span></span>

### <a name="open-authentication"></a><span data-ttu-id="4d55d-284">開放驗證</span><span class="sxs-lookup"><span data-stu-id="4d55d-284">Open Authentication</span></span>
<span data-ttu-id="4d55d-285">使用您的 Microsoft 或 Google 帳戶登入即是開放驗證的範例。</span><span class="sxs-lookup"><span data-stu-id="4d55d-285">An example of open authentication is signing in with your Microsoft or Google account.</span></span> <span data-ttu-id="4d55d-286">許多使用 OAuth 的應用程式都提供替代用戶端密碼，第一個技巧就是調查該可能性。</span><span class="sxs-lookup"><span data-stu-id="4d55d-286">Many apps that use OAuth provide the client secret alternative, so your first tactic should be to investigate that possibility.</span></span>

<span data-ttu-id="4d55d-287">如果您的測試必須使用 OAuth 登入，則常用的方式是：</span><span class="sxs-lookup"><span data-stu-id="4d55d-287">If your test must sign in using OAuth, the general approach is:</span></span>

* <span data-ttu-id="4d55d-288">使用 Fiddler 等工具來檢查網頁瀏覽器、驗證網站及您的應用程式之間的流量。</span><span class="sxs-lookup"><span data-stu-id="4d55d-288">Use a tool such as Fiddler to examine the traffic between your web browser, the authentication site, and your app.</span></span>
* <span data-ttu-id="4d55d-289">使用不同的電腦或瀏覽器，或以較長時間間隔 (讓權杖過期) 執行兩次以上的登入。</span><span class="sxs-lookup"><span data-stu-id="4d55d-289">Perform two or more sign-ins using different machines or browsers, or at long intervals (to allow tokens to expire).</span></span>
* <span data-ttu-id="4d55d-290">藉由比較不同的工作階段，識別從驗證網站傳回的權杖，登入之後此權杖會傳遞至您的應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d55d-290">By comparing different sessions, identify the token passed back from the authenticating site, that is then passed to your app server after sign-in.</span></span>
* <span data-ttu-id="4d55d-291">使用 Visual Studio 記錄 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-291">Record a web test using Visual Studio.</span></span>
* <span data-ttu-id="4d55d-292">將權杖參數化，當驗證器傳回權杖時設定參數，然後在查詢網站時使用參數。</span><span class="sxs-lookup"><span data-stu-id="4d55d-292">Parameterize the tokens, setting the parameter when the token is returned from the authenticator, and using it in the query to the site.</span></span>
  <span data-ttu-id="4d55d-293">(Visual Studio 會嘗試將測試參數化，但不會正確地將權杖參數化。)</span><span class="sxs-lookup"><span data-stu-id="4d55d-293">(Visual Studio attempts to parameterize the test, but does not correctly parameterize the tokens.)</span></span>


## <a name="performance-tests"></a><span data-ttu-id="4d55d-294">效能測試</span><span class="sxs-lookup"><span data-stu-id="4d55d-294">Performance tests</span></span>
<span data-ttu-id="4d55d-295">您可以在網站上執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-295">You can run a load test on your website.</span></span> <span data-ttu-id="4d55d-296">例如可用性測試，您可以從我們在全球各地的點傳送簡單要求或多個步驟的要求。</span><span class="sxs-lookup"><span data-stu-id="4d55d-296">Like the availability test, you can send either simple requests or multi-step requests from our points around the world.</span></span> <span data-ttu-id="4d55d-297">不同於可用性測試，許多要求傳送時會同時模擬多位使用者。</span><span class="sxs-lookup"><span data-stu-id="4d55d-297">Unlike an availability test, many requests are sent, simulating multiple simultaneous users.</span></span>

<span data-ttu-id="4d55d-298">從 [概觀] 刀鋒視窗，開啟 [設定]、[效能測試]。</span><span class="sxs-lookup"><span data-stu-id="4d55d-298">From the Overview blade, open **Settings**, **Performance Tests**.</span></span> <span data-ttu-id="4d55d-299">當建立測試時，您會受邀連接或建立 Visual Studio Team 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d55d-299">When you create a test, you are invited to connect to or create a Visual Studio Team Services account.</span></span>

<span data-ttu-id="4d55d-300">測試完成時，會為您顯示回應時間和成功率。</span><span class="sxs-lookup"><span data-stu-id="4d55d-300">When the test is complete, you are shown response times and success rates.</span></span>


![效能測試](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> <span data-ttu-id="4d55d-302">若要觀察效能測試的影響，請使用[即時串流](app-insights-live-stream.md)和[分析工具](app-insights-profiler.md)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-302">To observe the effects of a performance test, use [Live Stream](app-insights-live-stream.md) and [Profiler](app-insights-profiler.md).</span></span>
>

## <a name="automation"></a><span data-ttu-id="4d55d-303">自動化</span><span class="sxs-lookup"><span data-stu-id="4d55d-303">Automation</span></span>
* <span data-ttu-id="4d55d-304">[使用 PowerShell 指令碼自動設定可用性測試](app-insights-powershell.md#add-an-availability-test)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-304">[Use PowerShell scripts to set up an availability test](app-insights-powershell.md#add-an-availability-test) automatically.</span></span>
* <span data-ttu-id="4d55d-305">設定會在產生警示時呼叫的 [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="4d55d-305">Set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span>

## <span data-ttu-id="4d55d-306"><a name="qna"></a>有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="4d55d-306"><a name="qna"></a>Questions?</span></span> <span data-ttu-id="4d55d-307">有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="4d55d-307">Problems?</span></span>
* <span data-ttu-id="4d55d-308">*可以從我的 Web 測試呼叫程式碼嗎？*</span><span class="sxs-lookup"><span data-stu-id="4d55d-308">*Can I call code from my web test?*</span></span>

    <span data-ttu-id="4d55d-309">否。</span><span class="sxs-lookup"><span data-stu-id="4d55d-309">No.</span></span> <span data-ttu-id="4d55d-310">測試步驟必須在 .webtest 檔案中。</span><span class="sxs-lookup"><span data-stu-id="4d55d-310">The steps of the test must be in the .webtest file.</span></span> <span data-ttu-id="4d55d-311">而且您不能呼叫其他 Web 測試或使用迴圈。</span><span class="sxs-lookup"><span data-stu-id="4d55d-311">And you can't call other web tests or use loops.</span></span> <span data-ttu-id="4d55d-312">但是這裡有一些您會覺得有用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="4d55d-312">But there are several plug-ins that you might find helpful.</span></span>
* <span data-ttu-id="4d55d-313">*是否支援 HTTPS？*</span><span class="sxs-lookup"><span data-stu-id="4d55d-313">*Is HTTPS supported?*</span></span>

    <span data-ttu-id="4d55d-314">我們支援 TLS 1.1 和 TLS 1.2。</span><span class="sxs-lookup"><span data-stu-id="4d55d-314">We support TLS 1.1 and TLS 1.2.</span></span>
* <span data-ttu-id="4d55d-315">*「Web 測試」和「可用性測試」之間有任何差異嗎？*</span><span class="sxs-lookup"><span data-stu-id="4d55d-315">*Is there a difference between "web tests" and "availability tests"?*</span></span>

    <span data-ttu-id="4d55d-316">這兩個詞彙可能會交替參考。</span><span class="sxs-lookup"><span data-stu-id="4d55d-316">The two terms may be referenced interchangeably.</span></span> <span data-ttu-id="4d55d-317">可用性測試是更廣泛的詞彙，除了多重步驟 Web 測試以外，還包含單一 URL ping 測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-317">Availability tests is a more generic term that includes the single URL ping tests in addition to the multi-step web tests.</span></span>
* <span data-ttu-id="4d55d-318">*我想要在位於防火牆後面執行的內部伺服器上使用可用性測試。*</span><span class="sxs-lookup"><span data-stu-id="4d55d-318">*I'd like to use availability tests on our internal server that runs behind a firewall.*</span></span>

    <span data-ttu-id="4d55d-319">有兩個可能的解決方案：</span><span class="sxs-lookup"><span data-stu-id="4d55d-319">There are two possible solutions:</span></span>
    
    * <span data-ttu-id="4d55d-320">設定防火牆以允許來自[我們 Web 測試代理程式的 IP 位址](app-insights-ip-addresses.md)所發出的內送要求。</span><span class="sxs-lookup"><span data-stu-id="4d55d-320">Configure your firewall to permit incoming requests from the [IP addresses of our web test agents](app-insights-ip-addresses.md).</span></span>
    * <span data-ttu-id="4d55d-321">撰寫您自己的程式碼以定期測試您的內部伺服器。</span><span class="sxs-lookup"><span data-stu-id="4d55d-321">Write your own code to periodically test your internal server.</span></span> <span data-ttu-id="4d55d-322">執行程式碼作為您防火牆後方測試伺服器上的背景處理序。</span><span class="sxs-lookup"><span data-stu-id="4d55d-322">Run the code as a background process on a test server behind your firewall.</span></span> <span data-ttu-id="4d55d-323">您的測試處理序可以使用核心 SDK 套件中的 [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API，將其結果傳送至 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="4d55d-323">Your test process can send its results to Application Insights by using [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in the core SDK package.</span></span> <span data-ttu-id="4d55d-324">這需要測試伺服器具有 Application Insights 內嵌端點的連出存取，但這比起替代的允許連入要求是較小的安全性風險。</span><span class="sxs-lookup"><span data-stu-id="4d55d-324">This requires your test server to have outgoing access to the Application Insights ingestion endpoint, but that is a much smaller security risk than the alternative of permitting incoming requests.</span></span> <span data-ttu-id="4d55d-325">結果不會出現在 [可用性 web 測試] 刀鋒視窗中，但會在分析、搜尋和計量瀏覽器中出現作為可用性結果。</span><span class="sxs-lookup"><span data-stu-id="4d55d-325">The results will not appear in the availability web tests blades, but appears as availability results in Analytics, Search, and Metric Explorer.</span></span>
* <span data-ttu-id="4d55d-326">*上傳多步驟 Web 測試失敗*</span><span class="sxs-lookup"><span data-stu-id="4d55d-326">*Uploading a multi-step web test fails*</span></span>

    <span data-ttu-id="4d55d-327">有 300 K 的大小限制。</span><span class="sxs-lookup"><span data-stu-id="4d55d-327">There's a size limit of 300 K.</span></span>

    <span data-ttu-id="4d55d-328">不支援迴圈。</span><span class="sxs-lookup"><span data-stu-id="4d55d-328">Loops aren't supported.</span></span>

    <span data-ttu-id="4d55d-329">不支援其他 Web 測試的參考。</span><span class="sxs-lookup"><span data-stu-id="4d55d-329">References to other web tests aren't supported.</span></span>

    <span data-ttu-id="4d55d-330">不支援資料來源。</span><span class="sxs-lookup"><span data-stu-id="4d55d-330">Data sources aren't supported.</span></span>
* <span data-ttu-id="4d55d-331">*多步驟測試未完成*</span><span class="sxs-lookup"><span data-stu-id="4d55d-331">*My multi-step test doesn't complete*</span></span>

    <span data-ttu-id="4d55d-332">每個測試有 100 個要求的限制。</span><span class="sxs-lookup"><span data-stu-id="4d55d-332">There's a limit of 100 requests per test.</span></span>

    <span data-ttu-id="4d55d-333">如果執行時間超過兩分鐘，就會停止測試。</span><span class="sxs-lookup"><span data-stu-id="4d55d-333">The test is stopped if it runs longer than two minutes.</span></span>
* <span data-ttu-id="4d55d-334">*如何使用用戶端憑證執行測試？*</span><span class="sxs-lookup"><span data-stu-id="4d55d-334">*How can I run a test with client certificates?*</span></span>

    <span data-ttu-id="4d55d-335">很抱歉，我們不支援此功能。</span><span class="sxs-lookup"><span data-stu-id="4d55d-335">We don't support that, sorry.</span></span>


## <span data-ttu-id="4d55d-336"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="4d55d-336"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="4d55d-337">[搜尋診斷記錄][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="4d55d-337">[Search diagnostic logs][diagnostic]</span></span>

<span data-ttu-id="4d55d-338">[疑難排解][qna]</span><span class="sxs-lookup"><span data-stu-id="4d55d-338">[Troubleshooting][qna]</span></span>

[<span data-ttu-id="4d55d-339">Web 測試代理程式的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4d55d-339">IP addresses of web test agents</span></span>](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
