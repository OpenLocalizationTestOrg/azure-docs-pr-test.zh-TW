---
title: "aaaMonitor 可用性和回應的任何網站 |Microsoft 文件"
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
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a><span data-ttu-id="6727e-104">監視任何網站的可用性和回應性</span><span class="sxs-lookup"><span data-stu-id="6727e-104">Monitor availability and responsiveness of any web site</span></span>
<span data-ttu-id="6727e-105">您已部署您的 web 應用程式或網站 tooany 伺服器之後，您可以設定測試 toomonitor 其可用性和回應性。</span><span class="sxs-lookup"><span data-stu-id="6727e-105">After you've deployed your web app or web site tooany server, you can set up tests toomonitor its availability and responsiveness.</span></span> <span data-ttu-id="6727e-106">[Azure 的 Application Insights](app-insights-overview.md)傳送 web 要求 tooyour 應用程式上定期從 hello 世界各地的點。</span><span class="sxs-lookup"><span data-stu-id="6727e-106">[Azure Application Insights](app-insights-overview.md) sends web requests tooyour application at regular intervals from points around hello world.</span></span> <span data-ttu-id="6727e-107">如果應用程式沒有回應或回應太慢，則會警告您。</span><span class="sxs-lookup"><span data-stu-id="6727e-107">It alerts you if your application doesn't respond, or responds slowly.</span></span>

<span data-ttu-id="6727e-108">您可以設定可用性測試的任何 HTTP 或 HTTPS 端點可從存取 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="6727e-108">You can set up availability tests for any HTTP or HTTPS endpoint that is accessible from hello public internet.</span></span> <span data-ttu-id="6727e-109">您不需要 tooadd 任何您要測試的 toohello 網站。</span><span class="sxs-lookup"><span data-stu-id="6727e-109">You don't have tooadd anything toohello web site you're testing.</span></span> <span data-ttu-id="6727e-110">即使沒有 toobe 網站： 您可以測試您所仰賴的 REST API 服務。</span><span class="sxs-lookup"><span data-stu-id="6727e-110">It doesn't even have toobe your site: you could test a REST API service on which you depend.</span></span>

<span data-ttu-id="6727e-111">可用性測試有兩種：</span><span class="sxs-lookup"><span data-stu-id="6727e-111">There are two types of availability tests:</span></span>

* <span data-ttu-id="6727e-112">[URL ping 測試](#create)： 您可以在 hello Azure 入口網站中建立簡單的測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-112">[URL ping test](#create): a simple test that you can create in hello Azure portal.</span></span>
* <span data-ttu-id="6727e-113">[多重步驟 web 測試](#multi-step-web-tests)： 您在 Visual Studio Enterprise 和上傳 toohello 入口網站中建立的。</span><span class="sxs-lookup"><span data-stu-id="6727e-113">[Multi-step web test](#multi-step-web-tests): which you create in Visual Studio Enterprise and upload toohello portal.</span></span>

<span data-ttu-id="6727e-114">您可以建立註冊 too25 可用性測試每個應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="6727e-114">You can create up too25 availability tests per application resource.</span></span>

## <span data-ttu-id="6727e-115"><a name="create"></a>1.開啟可用性測試報告的資源</span><span class="sxs-lookup"><span data-stu-id="6727e-115"><a name="create"></a>1. Open a resource for your availability test reports</span></span>

<span data-ttu-id="6727e-116">**如果您已經設定 Application Insights**您 web 應用程式中，開啟其 Application Insights 資源在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6727e-116">**If you have already configured Application Insights** for your web app, open its Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="6727e-117">**或如果您想在新的資源中，報表 toosee**太註冊[Microsoft Azure](http://azure.com)，go toohello [Azure 入口網站](https://portal.azure.com)，並建立 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="6727e-117">**Or, if you want toosee your reports in a new resource,** sign up too[Microsoft Azure](http://azure.com), go toohello [Azure portal](https://portal.azure.com), and create an Application Insights resource.</span></span>

![New > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

<span data-ttu-id="6727e-119">按一下**所有資源**hello 新資源的 tooopen hello 概觀刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6727e-119">Click **All resources** tooopen hello Overview blade for hello new resource.</span></span>

## <span data-ttu-id="6727e-120"><a name="setup"></a>2.建立 URL Ping 測試</span><span class="sxs-lookup"><span data-stu-id="6727e-120"><a name="setup"></a>2. Create a URL ping test</span></span>
<span data-ttu-id="6727e-121">開啟 hello 可用性刀鋒視窗，並加入測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-121">Open hello Availability blade and add a test.</span></span>

![填滿至少 hello 您網站的 URL](./media/app-insights-monitor-web-app-availability/13-availability.png)

* <span data-ttu-id="6727e-123">**hello URL**可以是任何網頁想 tootest，但是它必須從可見 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="6727e-123">**hello URL** can be any web page you want tootest, but it must be visible from hello public internet.</span></span> <span data-ttu-id="6727e-124">hello URL 可以包含查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6727e-124">hello URL can include a query string.</span></span> <span data-ttu-id="6727e-125">例如，您可以訓練一下您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6727e-125">So, for example, you can exercise your database a little.</span></span> <span data-ttu-id="6727e-126">如果 hello URL 解析 tooa 重新導向，我們追蹤它 too10 重新導向。</span><span class="sxs-lookup"><span data-stu-id="6727e-126">If hello URL resolves tooa redirect, we follow it up too10 redirects.</span></span>
* <span data-ttu-id="6727e-127">**剖析相依要求**: hello 測試如果勾選此選項，要求映像、 指令碼、 樣式檔案及其他檔案 hello 受測的 web 網頁的一部分。</span><span class="sxs-lookup"><span data-stu-id="6727e-127">**Parse dependent requests**: If this option is checked, hello test requests images, scripts, style files, and other files that are part of hello web page under test.</span></span> <span data-ttu-id="6727e-128">hello 記錄的回應時間包括 hello 所花費時間 tooget 這些檔案。</span><span class="sxs-lookup"><span data-stu-id="6727e-128">hello recorded response time includes hello time taken tooget these files.</span></span> <span data-ttu-id="6727e-129">如果所有這些資源無法 hello hello 整個測試的逾時內已成功下載，hello 測試將會失敗。</span><span class="sxs-lookup"><span data-stu-id="6727e-129">hello test fails if all these resources cannot be successfully downloaded within hello timeout for hello whole test.</span></span> 

    <span data-ttu-id="6727e-130">如果未核取 hello 選項，hello 測試只會要求在您指定的 hello URL hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="6727e-130">If hello option is not checked, hello test only requests hello file at hello URL you specified.</span></span>
* <span data-ttu-id="6727e-131">**啟用重試**： 若勾選此選項，hello 測試失敗時，它會重試較短的間隔之後。</span><span class="sxs-lookup"><span data-stu-id="6727e-131">**Enable retries**:  If this option is checked, when hello test fails, it is retried after a short interval.</span></span> <span data-ttu-id="6727e-132">只有在連續三次重試失敗後，才會回報失敗。</span><span class="sxs-lookup"><span data-stu-id="6727e-132">A failure is reported only if three successive attempts fail.</span></span> <span data-ttu-id="6727e-133">接著會將後續的測試執行 hello 一般測試的頻率。</span><span class="sxs-lookup"><span data-stu-id="6727e-133">Subsequent tests are then performed at hello usual test frequency.</span></span> <span data-ttu-id="6727e-134">重試已暫時暫止，直到 hello 下一個成功為止。</span><span class="sxs-lookup"><span data-stu-id="6727e-134">Retry is temporarily suspended until hello next success.</span></span> <span data-ttu-id="6727e-135">此規則可個別套用在每個測試位置。</span><span class="sxs-lookup"><span data-stu-id="6727e-135">This rule is applied independently at each test location.</span></span> <span data-ttu-id="6727e-136">我們建議使用這個選項。</span><span class="sxs-lookup"><span data-stu-id="6727e-136">We recommend this option.</span></span> <span data-ttu-id="6727e-137">平均來說，大約 80% 失敗會在重試後消失。</span><span class="sxs-lookup"><span data-stu-id="6727e-137">On average, about 80% of failures disappear on retry.</span></span>
* <span data-ttu-id="6727e-138">**測試頻率**： 設定頻率 hello 測試從每個測試位置執行。</span><span class="sxs-lookup"><span data-stu-id="6727e-138">**Test frequency**: Sets how often hello test is run from each test location.</span></span> <span data-ttu-id="6727e-139">頻率為 5 分鐘且有五個測試位置，則您的網站平均每一分鐘會執行測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-139">With a frequency of five minutes and five test locations, your site is tested on average every minute.</span></span>
* <span data-ttu-id="6727e-140">**測試位置**是 hello 會將我們的伺服器傳送 web 要求 tooyour URL 的位置。</span><span class="sxs-lookup"><span data-stu-id="6727e-140">**Test locations** are hello places from where our servers send web requests tooyour URL.</span></span> <span data-ttu-id="6727e-141">請選擇多個位置，以便區分網站問題與網路問題。</span><span class="sxs-lookup"><span data-stu-id="6727e-141">Choose more than one so that you can distinguish problems in your website from network issues.</span></span> <span data-ttu-id="6727e-142">您可以選取 too16 位置。</span><span class="sxs-lookup"><span data-stu-id="6727e-142">You can select up too16 locations.</span></span>
* <span data-ttu-id="6727e-143">**成功準則**：</span><span class="sxs-lookup"><span data-stu-id="6727e-143">**Success criteria**:</span></span>

    <span data-ttu-id="6727e-144">**測試逾時**： 減少此值 toobe，提醒回應變慢。</span><span class="sxs-lookup"><span data-stu-id="6727e-144">**Test timeout**: Decrease this value toobe alerted about slow responses.</span></span> <span data-ttu-id="6727e-145">如果未在此期間內收到來自您的站台的 hello 回應 hello 測試被視為失敗。</span><span class="sxs-lookup"><span data-stu-id="6727e-145">hello test is counted as a failure if hello responses from your site have not been received within this period.</span></span> <span data-ttu-id="6727e-146">如果您選取**剖析相依要求**、 然後所有 hello 影像、 樣式檔案、 指令碼和其他相依的資源必須已在此期間內收到。</span><span class="sxs-lookup"><span data-stu-id="6727e-146">If you selected **Parse dependent requests**, then all hello images, style files, scripts, and other dependent resources must have been received within this period.</span></span>

    <span data-ttu-id="6727e-147">**HTTP 回應**: hello 傳回視為成功的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="6727e-147">**HTTP response**: hello returned status code that is counted as a success.</span></span> <span data-ttu-id="6727e-148">200 是表示已傳回標準的 web 網頁的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6727e-148">200 is hello code that indicates that a normal web page has been returned.</span></span>

    <span data-ttu-id="6727e-149">**內容比對**：字串，例如「歡迎！</span><span class="sxs-lookup"><span data-stu-id="6727e-149">**Content match**: a string, like "Welcome!"</span></span> <span data-ttu-id="6727e-150">我們會測試每個回應中的區分大小寫完全相符。</span><span class="sxs-lookup"><span data-stu-id="6727e-150">We test that an exact case-sensitive match occurs in every response.</span></span> <span data-ttu-id="6727e-151">必須是單純字串，不含萬用字元。</span><span class="sxs-lookup"><span data-stu-id="6727e-151">It must be a plain string, without wildcards.</span></span> <span data-ttu-id="6727e-152">別忘了，如果您可能必須 tooupdate 頁面內容變更它。</span><span class="sxs-lookup"><span data-stu-id="6727e-152">Don't forget that if your page content changes you might have tooupdate it.</span></span>
* <span data-ttu-id="6727e-153">**警示**，根據預設，如果會傳送 tooyou 失敗會在三個位置超過五分鐘。</span><span class="sxs-lookup"><span data-stu-id="6727e-153">**Alerts** are, by default, sent tooyou if there are failures in three locations over five minutes.</span></span> <span data-ttu-id="6727e-154">可能 toobe 網路問題，而不是問題與您的網站在同一個位置失敗。</span><span class="sxs-lookup"><span data-stu-id="6727e-154">A failure in one location is likely toobe a network problem, and not a problem with your site.</span></span> <span data-ttu-id="6727e-155">但您可以變更 hello 閾值 toobe 更多或較不區分大小寫，而且您也可以變更 hello 電子郵件應該傳送至。</span><span class="sxs-lookup"><span data-stu-id="6727e-155">But you can change hello threshold toobe more or less sensitive, and you can also change who hello emails should be sent to.</span></span>

    <span data-ttu-id="6727e-156">您可以設定會在產生警示時呼叫的 [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="6727e-156">You can set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span> <span data-ttu-id="6727e-157">(不過請注意，查詢參數目前不會當作屬性傳遞)。</span><span class="sxs-lookup"><span data-stu-id="6727e-157">(But note that, at present, query parameters are not passed through as Properties.)</span></span>

### <a name="test-more-urls"></a><span data-ttu-id="6727e-158">測試更多 URL</span><span class="sxs-lookup"><span data-stu-id="6727e-158">Test more URLs</span></span>
<span data-ttu-id="6727e-159">加入更多測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-159">Add more tests.</span></span> <span data-ttu-id="6727e-160">比方說，在加法 tootesting 首頁中，您可以確定您的資料庫藉由測試搜尋 hello URL 執行。</span><span class="sxs-lookup"><span data-stu-id="6727e-160">For example, In addition tootesting your home page, you can make sure your database is running by testing hello URL for a search.</span></span>


## <span data-ttu-id="6727e-161"><a name="monitor"></a>3.查看可用性測試結果</span><span class="sxs-lookup"><span data-stu-id="6727e-161"><a name="monitor"></a>3. See your availability test results</span></span>

<span data-ttu-id="6727e-162">在幾分鐘之後, 按**重新整理**toosee 測試結果。</span><span class="sxs-lookup"><span data-stu-id="6727e-162">After a few minutes, click **Refresh** toosee test results.</span></span> 

![Hello 家用刀鋒視窗上的摘要結果](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

<span data-ttu-id="6727e-164">hello scatterplot 顯示 hello 的範例中有診斷測試步驟的詳細資料的測試結果。</span><span class="sxs-lookup"><span data-stu-id="6727e-164">hello scatterplot shows samples of hello test results that have diagnostic test-step detail in them.</span></span> <span data-ttu-id="6727e-165">hello 測試引擎會儲存發生失敗的測試中的診斷詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6727e-165">hello test engine stores diagnostic detail for tests that have failures.</span></span> <span data-ttu-id="6727e-166">成功的測試，診斷詳細資料會儲存 hello 執行的子集。</span><span class="sxs-lookup"><span data-stu-id="6727e-166">For successful tests, diagnostic details are stored for a subset of hello executions.</span></span> <span data-ttu-id="6727e-167">將滑鼠停留在任何 hello 綠色/紅點 toosee hello 測試時間戳記、 測試持續期間、 位置和測試名稱。</span><span class="sxs-lookup"><span data-stu-id="6727e-167">Hover over any of hello green/red dots toosee hello test timestamp, test duration, location, and test name.</span></span> <span data-ttu-id="6727e-168">按一下瀏覽 hello 散佈圖 toosee hello 詳細資料中的 hello 測試結果的任何點。</span><span class="sxs-lookup"><span data-stu-id="6727e-168">Click through any dot in hello scatter plot toosee hello details of hello test result.</span></span>  

<span data-ttu-id="6727e-169">選取特定測試的位置，或減少 hello 時間週期 toosee 取得更多結果周圍 hello 感興趣的時段。</span><span class="sxs-lookup"><span data-stu-id="6727e-169">Select a particular test, location, or reduce hello time period toosee more results around hello time period of interest.</span></span> <span data-ttu-id="6727e-170">搜尋總管 toosee 產生的所有執行中，或使用此資料的分析查詢 toorun 自訂報表。</span><span class="sxs-lookup"><span data-stu-id="6727e-170">Use Search Explorer toosee results from all executions, or use Analytics queries toorun custom reports on this data.</span></span>

<span data-ttu-id="6727e-171">在加法 toohello 未經處理的結果，有兩個可用性度量計量瀏覽器中：</span><span class="sxs-lookup"><span data-stu-id="6727e-171">In addition toohello raw results, there are two Availability metrics in Metrics Explorer:</span></span> 

1. <span data-ttu-id="6727e-172">已成功，跨所有測試執行的 hello 測試的可用性： 百分比。</span><span class="sxs-lookup"><span data-stu-id="6727e-172">Availability: Percentage of hello tests that were successful, across all test executions.</span></span> 
2. <span data-ttu-id="6727e-173">測試持續期間︰所有測試執行中的平均測試持續期間。</span><span class="sxs-lookup"><span data-stu-id="6727e-173">Test Duration: Average test duration across all test executions.</span></span>

<span data-ttu-id="6727e-174">您可以在 hello 測試名稱、 位置 tooanalyze 趨勢的特定測試和 （或） 位置套用篩選。</span><span class="sxs-lookup"><span data-stu-id="6727e-174">You can apply filters on hello test name, location tooanalyze trends of a particular test and/or location.</span></span>

## <span data-ttu-id="6727e-175"><a name="edit"></a> 檢查和編輯測試</span><span class="sxs-lookup"><span data-stu-id="6727e-175"><a name="edit"></a> Inspect and edit tests</span></span>

<span data-ttu-id="6727e-176">從 hello 摘要 頁面上，選取特定測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-176">From hello summary page, select a specific test.</span></span> <span data-ttu-id="6727e-177">您可以在該頁面中看見其特定結果，並加以編輯或暫時將它停用。</span><span class="sxs-lookup"><span data-stu-id="6727e-177">There, you can see its specific results, and edit or temporarily disable it.</span></span>

![Edit or disable a web test](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

<span data-ttu-id="6727e-179">您可能想 toodisable 可用性測試或與它們相關聯規則，而您會在服務上執行維護的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="6727e-179">You might want toodisable availability tests or hello alert rules associated with them while you are performing maintenance on your service.</span></span> 

## <span data-ttu-id="6727e-180"><a name="failures"></a>如果您看到失敗</span><span class="sxs-lookup"><span data-stu-id="6727e-180"><a name="failures"></a>If you see failures</span></span>
<span data-ttu-id="6727e-181">按一下一個紅點。</span><span class="sxs-lookup"><span data-stu-id="6727e-181">Click a red dot.</span></span>

![按一下一個紅點](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


<span data-ttu-id="6727e-183">從可用性測試結果，您可以：</span><span class="sxs-lookup"><span data-stu-id="6727e-183">From an availability test result, you can:</span></span>

* <span data-ttu-id="6727e-184">檢查從伺服器收到 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="6727e-184">Inspect hello response received from your server.</span></span>
* <span data-ttu-id="6727e-185">開啟應用程式伺服器處理 hello 失敗的要求執行個體時傳送嗨遙測。</span><span class="sxs-lookup"><span data-stu-id="6727e-185">Open hello telemetry sent by your server app while processing hello failed request instance.</span></span>
* <span data-ttu-id="6727e-186">記錄問題或 Git 或 VSTS tootrack hello 問題中工作項目。</span><span class="sxs-lookup"><span data-stu-id="6727e-186">Log an issue or work item in Git or VSTS tootrack hello problem.</span></span> <span data-ttu-id="6727e-187">hello bug 會包含連結 toothis 事件。</span><span class="sxs-lookup"><span data-stu-id="6727e-187">hello bug will contain a link toothis event.</span></span>
* <span data-ttu-id="6727e-188">開啟 Visual Studio 中的 hello web 測試結果。</span><span class="sxs-lookup"><span data-stu-id="6727e-188">Open hello web test result in Visual Studio.</span></span>


<span data-ttu-id="6727e-189">*看起來正常，但回報為失敗？*</span><span class="sxs-lookup"><span data-stu-id="6727e-189">*Looks OK but reported as a failure?*</span></span> <span data-ttu-id="6727e-190">請檢查所有 hello 映像、 指令碼、 樣式表和 hello 頁面所載入的任何其他檔案。</span><span class="sxs-lookup"><span data-stu-id="6727e-190">Check all hello images, scripts, style sheets, and any other files loaded by hello page.</span></span> <span data-ttu-id="6727e-191">如果其中任何失敗，hello 測試報告為失敗，即使 hello 主要 html 網頁載入 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6727e-191">If any of them fails, hello test is reported as failed, even if hello main html page loads OK.</span></span>

<span data-ttu-id="6727e-192">沒有相關項目？</span><span class="sxs-lookup"><span data-stu-id="6727e-192">*No related items?*</span></span> <span data-ttu-id="6727e-193">如果您已針對伺服器端應用程式設定 Application Insights，這可能是因為正在進行[取樣](app-insights-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="6727e-193">If you have Application Insights set up for your server-side application, that may be because [sampling](app-insights-sampling.md) is in operation.</span></span> 

## <a name="multi-step-web-tests"></a><span data-ttu-id="6727e-194">多重步驟 Web 測試</span><span class="sxs-lookup"><span data-stu-id="6727e-194">Multi-step web tests</span></span>
<span data-ttu-id="6727e-195">您可以監視涉及一連串 URL 的案例。</span><span class="sxs-lookup"><span data-stu-id="6727e-195">You can monitor a scenario that involves a sequence of URLs.</span></span> <span data-ttu-id="6727e-196">例如，如果您要監視的銷售的網站，您可以測試，加入項目 toohello 購物車正常運作。</span><span class="sxs-lookup"><span data-stu-id="6727e-196">For example, if you are monitoring a sales website, you can test that adding items toohello shopping cart works correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="6727e-197">進行多步驟 Web 測試此會收取費用。</span><span class="sxs-lookup"><span data-stu-id="6727e-197">There is a charge for multi-step web tests.</span></span> <span data-ttu-id="6727e-198">[價格方案](http://azure.microsoft.com/pricing/details/application-insights/)。</span><span class="sxs-lookup"><span data-stu-id="6727e-198">[Pricing scheme](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>
> 

<span data-ttu-id="6727e-199">toocreate multi-step 測試，您使用 Visual Studio Enterprise 中，記錄 hello 案例並再上傳記錄 tooApplication Insights hello。</span><span class="sxs-lookup"><span data-stu-id="6727e-199">toocreate a multi-step test, you record hello scenario by using Visual Studio Enterprise, and then upload hello recording tooApplication Insights.</span></span> <span data-ttu-id="6727e-200">Application Insights 重新 hello 案例中執行的間隔，並確認 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="6727e-200">Application Insights replays hello scenario at intervals and verifies hello responses.</span></span>

> [!NOTE]
> <span data-ttu-id="6727e-201">您無法在測試中使用已編碼的函式或迴圈。</span><span class="sxs-lookup"><span data-stu-id="6727e-201">You can't use coded functions or loops in your tests.</span></span> <span data-ttu-id="6727e-202">hello 測試必須完全包含在 hello.webtest 指令碼。</span><span class="sxs-lookup"><span data-stu-id="6727e-202">hello test must be contained completely in hello .webtest script.</span></span> <span data-ttu-id="6727e-203">不過，您可以使用標準外掛程式。</span><span class="sxs-lookup"><span data-stu-id="6727e-203">However, you can use standard plugins.</span></span>
>

#### <a name="1-record-a-scenario"></a><span data-ttu-id="6727e-204">1.記錄案例</span><span class="sxs-lookup"><span data-stu-id="6727e-204">1. Record a scenario</span></span>
<span data-ttu-id="6727e-205">使用 Visual Studio Enterprise toorecord web 工作階段。</span><span class="sxs-lookup"><span data-stu-id="6727e-205">Use Visual Studio Enterprise toorecord a web session.</span></span>

1. <span data-ttu-id="6727e-206">建立 Web 效能測試專案。</span><span class="sxs-lookup"><span data-stu-id="6727e-206">Create a Web performance test project.</span></span>

    ![在 Visual Studio Enterprise 版本中，請從 hello Web 效能和負載測試範本建立專案。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * <span data-ttu-id="6727e-208">*沒看見 hello Web 效能和負載測試範本嗎？*</span><span class="sxs-lookup"><span data-stu-id="6727e-208">*Don't see hello Web Performance and Load Test template?*</span></span> <span data-ttu-id="6727e-209">- 關閉 Visual Studio Enterprise。</span><span class="sxs-lookup"><span data-stu-id="6727e-209">- Close Visual Studio Enterprise.</span></span> <span data-ttu-id="6727e-210">開啟**Visual Studio 安裝程式**toomodify Visual Studio 企業版安裝。</span><span class="sxs-lookup"><span data-stu-id="6727e-210">Open **Visual Studio Installer** toomodify your Visual Studio Enterprise installation.</span></span> <span data-ttu-id="6727e-211">在 [個別元件] 之下，選取 [Web 效能和負載測試工具]。</span><span class="sxs-lookup"><span data-stu-id="6727e-211">Under **Individual Components**, select **Web Performance and load testing tools**.</span></span>

2. <span data-ttu-id="6727e-212">開啟 hello.webtest 檔案，並開始錄製。</span><span class="sxs-lookup"><span data-stu-id="6727e-212">Open hello .webtest file and start recording.</span></span>

    ![開啟 hello.webtest 檔案，然後按一下 [記錄]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. <span data-ttu-id="6727e-214">請勿 hello 想 toosimulate 測試中的使用者動作： 開啟您的網站，加入產品 toohello 車等等。</span><span class="sxs-lookup"><span data-stu-id="6727e-214">Do hello user actions you want toosimulate in your test: open your website, add a product toohello cart, and so on.</span></span> <span data-ttu-id="6727e-215">然後停止測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-215">Then stop your test.</span></span>

    ![hello web 測試錄製器執行 Internet Explorer 中。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    <span data-ttu-id="6727e-217">不要讓案例太長。</span><span class="sxs-lookup"><span data-stu-id="6727e-217">Don't make a long scenario.</span></span> <span data-ttu-id="6727e-218">以 100 個步驟和 2 分鐘為限。</span><span class="sxs-lookup"><span data-stu-id="6727e-218">There's a limit of 100 steps and 2 minutes.</span></span>
4. <span data-ttu-id="6727e-219">編輯 hello 測試：</span><span class="sxs-lookup"><span data-stu-id="6727e-219">Edit hello test to:</span></span>

   * <span data-ttu-id="6727e-220">新增驗證 toocheck 收到 hello 文字和回應碼。</span><span class="sxs-lookup"><span data-stu-id="6727e-220">Add validations toocheck hello received text and response codes.</span></span>
   * <span data-ttu-id="6727e-221">移除任何多餘的互動。</span><span class="sxs-lookup"><span data-stu-id="6727e-221">Remove any superfluous interactions.</span></span> <span data-ttu-id="6727e-222">您也可以移除相依要求的圖片或 tooad 或追蹤的網站。</span><span class="sxs-lookup"><span data-stu-id="6727e-222">You could also remove dependent requests for pictures or tooad or tracking sites.</span></span>

     <span data-ttu-id="6727e-223">請記住您只能編輯 hello 測試指令碼-您無法加入自訂程式碼，或呼叫其他 web 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-223">Remember that you can only edit hello test script - you can't add custom code or call other web tests.</span></span> <span data-ttu-id="6727e-224">不在 hello 測試中插入迴圈。</span><span class="sxs-lookup"><span data-stu-id="6727e-224">Don't insert loops in hello test.</span></span> <span data-ttu-id="6727e-225">您可以使用標準 Web 測試的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="6727e-225">You can use standard web test plug-ins.</span></span>
5. <span data-ttu-id="6727e-226">Hello 測試在中執行 Visual Studio toomake 能運作。</span><span class="sxs-lookup"><span data-stu-id="6727e-226">Run hello test in Visual Studio toomake sure it works.</span></span>

    <span data-ttu-id="6727e-227">hello web 測試執行器會開啟網頁瀏覽器，並重複 hello 您所錄製的動作。</span><span class="sxs-lookup"><span data-stu-id="6727e-227">hello web test runner opens a web browser and repeats hello actions you recorded.</span></span> <span data-ttu-id="6727e-228">請確定運作如您所預期。</span><span class="sxs-lookup"><span data-stu-id="6727e-228">Make sure it works as you expect.</span></span>

    ![在 Visual Studio 中，開啟 hello.webtest 檔案並按一下 [執行]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a><span data-ttu-id="6727e-230">2.上傳 hello web 測試 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="6727e-230">2. Upload hello web test tooApplication Insights</span></span>
1. <span data-ttu-id="6727e-231">在 hello Application Insights 入口網站建立 web 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-231">In hello Application Insights portal, create a web test.</span></span>

    ![在 hello web 測試刀鋒視窗中，選擇 [新增]。](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. <span data-ttu-id="6727e-233">選取多重步驟的測試，並上傳 hello.webtest 檔案。</span><span class="sxs-lookup"><span data-stu-id="6727e-233">Select multi-step test, and upload hello .webtest file.</span></span>

    ![選取 [多步驟 Web 測試]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    <span data-ttu-id="6727e-235">Hello 測試集的位置、 頻率及警示參數在 hello 相同方式如 ping 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-235">Set hello test locations, frequency, and alert parameters in hello same way as for ping tests.</span></span>

#### <a name="3-see-hello-results"></a><span data-ttu-id="6727e-236">3.請參閱 hello 結果</span><span class="sxs-lookup"><span data-stu-id="6727e-236">3. See hello results</span></span>

<span data-ttu-id="6727e-237">檢視您的測試結果和任何失敗 hello 相同的方式為單一 url 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-237">View your test results and any failures in hello same way as single-url tests.</span></span>

<span data-ttu-id="6727e-238">此外，您可以下載 hello 測試結果 tooview Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="6727e-238">In addition, you can download hello test results tooview them in Visual Studio.</span></span>

#### <a name="too-many-failures"></a><span data-ttu-id="6727e-239">太多失敗項目？</span><span class="sxs-lookup"><span data-stu-id="6727e-239">Too many failures?</span></span>

* <span data-ttu-id="6727e-240">失敗的常見原因是該 hello 測試執行時間太長。</span><span class="sxs-lookup"><span data-stu-id="6727e-240">A common reason for failure is that hello test runs too long.</span></span> <span data-ttu-id="6727e-241">不可執行超過兩分鐘。</span><span class="sxs-lookup"><span data-stu-id="6727e-241">It mustn't run longer than two minutes.</span></span>

* <span data-ttu-id="6727e-242">別忘了必須載入正確的頁面上的所有 hello 資源 hello 測試 toosucceed，包括指令碼、 樣式表、 影像和其他等等。</span><span class="sxs-lookup"><span data-stu-id="6727e-242">Don't forget that all hello resources of a page must load correctly for hello test toosucceed, including scripts, style sheets, images, and so forth.</span></span>

* <span data-ttu-id="6727e-243">hello web 測試必須完全包含在 hello.webtest 指令碼： 您無法在 hello 測試中使用自動程式化的函式。</span><span class="sxs-lookup"><span data-stu-id="6727e-243">hello web test must be entirely contained in hello .webtest script: you can't use coded functions in hello test.</span></span>

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a><span data-ttu-id="6727e-244">將時間和隨機數字插入多重步驟測試中</span><span class="sxs-lookup"><span data-stu-id="6727e-244">Plugging time and random numbers into your multi-step test</span></span>
<span data-ttu-id="6727e-245">假設您要測試的工具會從外部來源取得與時間相關的資料 (例如股票)。</span><span class="sxs-lookup"><span data-stu-id="6727e-245">Suppose you're testing a tool that gets time-dependent data such as stocks from an external feed.</span></span> <span data-ttu-id="6727e-246">在錄製您的 web 測試時，有 toouse 特定時間，但您設定測試的 hello 參數，StartTime 和 EndTime。</span><span class="sxs-lookup"><span data-stu-id="6727e-246">When you record your web test, you have toouse specific times, but you set them as parameters of hello test, StartTime and EndTime.</span></span>

![具有參數的 Web 測試。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

<span data-ttu-id="6727e-248">當執行 hello 測試時，您想要的 EndTime toobe hello 永遠存在時間，而 StartTime 應該是 15 分鐘前。</span><span class="sxs-lookup"><span data-stu-id="6727e-248">When you run hello test, you'd like EndTime always toobe hello present time, and StartTime should be 15 minutes ago.</span></span>

<span data-ttu-id="6727e-249">Web 測試外掛程式提供 hello 方式 toodo 參數化次數。</span><span class="sxs-lookup"><span data-stu-id="6727e-249">Web Test Plug-ins provide hello way toodo parameterize times.</span></span>

1. <span data-ttu-id="6727e-250">針對您想要的每個變數參數值，各加入一個 Web 測試外掛程式。</span><span class="sxs-lookup"><span data-stu-id="6727e-250">Add a web test plug-in for each variable parameter value you want.</span></span> <span data-ttu-id="6727e-251">在 hello web 測試 工具列，選擇 **加入 Web 測試外掛程式**。</span><span class="sxs-lookup"><span data-stu-id="6727e-251">In hello web test toolbar, choose **Add Web Test Plugin**.</span></span>

    ![選擇 [加入 Web 測試外掛程式]，然後選取類型。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    <span data-ttu-id="6727e-253">在此範例中，我們會使用兩個執行個體的日期時間外掛程式 hello。</span><span class="sxs-lookup"><span data-stu-id="6727e-253">In this example, we use two instances of hello Date Time Plug-in.</span></span> <span data-ttu-id="6727e-254">一個執行個體設定為 "15 minutes ago"，另一個則設定為 "now"。</span><span class="sxs-lookup"><span data-stu-id="6727e-254">One instance is for "15 minutes ago" and another for "now."</span></span>
2. <span data-ttu-id="6727e-255">開啟每個外掛程式的 hello 的屬性。</span><span class="sxs-lookup"><span data-stu-id="6727e-255">Open hello properties of each plug-in.</span></span> <span data-ttu-id="6727e-256">加以命名，並將它設定 toouse hello 目前的時間。</span><span class="sxs-lookup"><span data-stu-id="6727e-256">Give it a name and set it toouse hello current time.</span></span> <span data-ttu-id="6727e-257">對其中一個，設定 [加入分鐘] = -15。</span><span class="sxs-lookup"><span data-stu-id="6727e-257">For one of them, set Add Minutes = -15.</span></span>

    ![設定 [名稱]、[使用目前時間] 和 [加入分鐘]。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. <span data-ttu-id="6727e-259">在 hello web 測試參數，使用 {{外掛程式 name}} tooreference 外掛程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="6727e-259">In hello web test parameters, use {{plug-in name}} tooreference a plug-in name.</span></span>

    ![Hello 測試參數中使用 {{外掛程式 name}}。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

<span data-ttu-id="6727e-261">現在，您可以上傳您的測試 toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6727e-261">Now, upload your test toohello portal.</span></span> <span data-ttu-id="6727e-262">在每個執行 hello 測試使用 hello 動態的值。</span><span class="sxs-lookup"><span data-stu-id="6727e-262">It uses hello dynamic values on every run of hello test.</span></span>

## <a name="dealing-with-sign-in"></a><span data-ttu-id="6727e-263">處理登入</span><span class="sxs-lookup"><span data-stu-id="6727e-263">Dealing with sign-in</span></span>
<span data-ttu-id="6727e-264">如果您的使用者登入 tooyour 應用程式，您會有不同的選項，來模擬登入，以便您可以測試背後 hello 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="6727e-264">If your users sign in tooyour app, you have various options for simulating sign-in so that you can test pages behind hello sign-in.</span></span> <span data-ttu-id="6727e-265">您使用的 hello 方法，取決於 hello hello 應用程式所提供的安全性類型。</span><span class="sxs-lookup"><span data-stu-id="6727e-265">hello approach you use depends on hello type of security provided by hello app.</span></span>

<span data-ttu-id="6727e-266">在所有情況下，您應該只針對測試的 hello 目的應用程式中建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="6727e-266">In all cases, you should create an account in your application just for hello purpose of testing.</span></span> <span data-ttu-id="6727e-267">可能的話，請限制 hello 這個測試帳戶的權限，讓不可能發生的 hello web 測試會影響到實際的使用者。</span><span class="sxs-lookup"><span data-stu-id="6727e-267">If possible, restrict hello permissions of this test account so that there's no possibility of hello web tests affecting real users.</span></span>

### <a name="simple-username-and-password"></a><span data-ttu-id="6727e-268">簡單的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="6727e-268">Simple username and password</span></span>
<span data-ttu-id="6727e-269">錄製 web 中的 hello 一般方式。</span><span class="sxs-lookup"><span data-stu-id="6727e-269">Record a web test in hello usual way.</span></span> <span data-ttu-id="6727e-270">先刪除 Cookie。</span><span class="sxs-lookup"><span data-stu-id="6727e-270">Delete cookies first.</span></span>

### <a name="saml-authentication"></a><span data-ttu-id="6727e-271">SAML 驗證</span><span class="sxs-lookup"><span data-stu-id="6727e-271">SAML authentication</span></span>
<span data-ttu-id="6727e-272">使用適用於 web 測試的 hello SAML 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="6727e-272">Use hello SAML plugin that is available for web tests.</span></span>

### <a name="client-secret"></a><span data-ttu-id="6727e-273">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="6727e-273">Client secret</span></span>
<span data-ttu-id="6727e-274">如果應用程式的登入路由牽涉到用戶端密碼，請使用此路由。</span><span class="sxs-lookup"><span data-stu-id="6727e-274">If your app has a sign-in route that involves a client secret, use that route.</span></span> <span data-ttu-id="6727e-275">Azure Active Directory (AAD) 是可提供用戶端密碼登入的服務範例。</span><span class="sxs-lookup"><span data-stu-id="6727e-275">Azure Active Directory (AAD) is an example of a service that provides a client secret sign-in.</span></span> <span data-ttu-id="6727e-276">AAD 時，在 hello 用戶端密碼為 hello 應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="6727e-276">In AAD, hello client secret is hello App Key.</span></span>

<span data-ttu-id="6727e-277">以下是使用應用程式金鑰之 Azure Web 應用程式的 Web 測試範例︰</span><span class="sxs-lookup"><span data-stu-id="6727e-277">Here's a sample web test of an Azure web app using an app key:</span></span>

![用戶端密碼範例](./media/app-insights-monitor-web-app-availability/110.png)

1. <span data-ttu-id="6727e-279">從使用用戶端密鑰 (AppKey) 的 AAD 取得權杖。</span><span class="sxs-lookup"><span data-stu-id="6727e-279">Get token from AAD using client secret (AppKey).</span></span>
2. <span data-ttu-id="6727e-280">從回應中擷取持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="6727e-280">Extract bearer token from response.</span></span>
3. <span data-ttu-id="6727e-281">呼叫 hello 授權標頭中使用持有人權杖的 API。</span><span class="sxs-lookup"><span data-stu-id="6727e-281">Call API using bearer token in hello authorization header.</span></span>

<span data-ttu-id="6727e-282">請確定 hello web 測試，實際的用戶端-也就是說，在 AAD-有它自己的應用程式，並使用其 clientId + appkey。</span><span class="sxs-lookup"><span data-stu-id="6727e-282">Make sure that hello web test is an actual client - that is, it has its own app in AAD - and use its clientId + appkey.</span></span> <span data-ttu-id="6727e-283">測試您的服務也有自己的應用程式在 AAD 中： hello appID 此應用程式的 URI 會反映在 hello 「 資源 」 欄位中的 hello web 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-283">Your service under test also has its own app in AAD: hello appID URI of this app is reflected in hello web test in hello “resource” field.</span></span>

### <a name="open-authentication"></a><span data-ttu-id="6727e-284">開放驗證</span><span class="sxs-lookup"><span data-stu-id="6727e-284">Open Authentication</span></span>
<span data-ttu-id="6727e-285">使用您的 Microsoft 或 Google 帳戶登入即是開放驗證的範例。</span><span class="sxs-lookup"><span data-stu-id="6727e-285">An example of open authentication is signing in with your Microsoft or Google account.</span></span> <span data-ttu-id="6727e-286">許多應用程式，使用 OAuth 提供 hello 用戶端密碼的替代方式，因此您第一種做法應該是 tooinvestigate 以排除這個可能性。</span><span class="sxs-lookup"><span data-stu-id="6727e-286">Many apps that use OAuth provide hello client secret alternative, so your first tactic should be tooinvestigate that possibility.</span></span>

<span data-ttu-id="6727e-287">如果您的測試必須在使用 OAuth 登入，hello 一般方法是：</span><span class="sxs-lookup"><span data-stu-id="6727e-287">If your test must sign in using OAuth, hello general approach is:</span></span>

* <span data-ttu-id="6727e-288">使用網頁瀏覽器、 hello 驗證網站和您的應用程式之間的 Fiddler tooexamine hello 流量之類的工具。</span><span class="sxs-lookup"><span data-stu-id="6727e-288">Use a tool such as Fiddler tooexamine hello traffic between your web browser, hello authentication site, and your app.</span></span>
* <span data-ttu-id="6727e-289">執行兩個或多個登入使用不同的電腦或瀏覽器，或在長時間間隔 (tooallow 語彙基元 tooexpire)。</span><span class="sxs-lookup"><span data-stu-id="6727e-289">Perform two or more sign-ins using different machines or browsers, or at long intervals (tooallow tokens tooexpire).</span></span>
* <span data-ttu-id="6727e-290">藉由比較不同的工作階段，找出從 hello 驗證網站時，會傳遞 tooyour 應用程式伺服器在登入之後所傳遞的 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="6727e-290">By comparing different sessions, identify hello token passed back from hello authenticating site, that is then passed tooyour app server after sign-in.</span></span>
* <span data-ttu-id="6727e-291">使用 Visual Studio 記錄 Web 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-291">Record a web test using Visual Studio.</span></span>
* <span data-ttu-id="6727e-292">參數化 hello 語彙基元，hello 驗證器，從傳回 hello 語彙基元時，設定 hello 參數，並使用 hello 查詢 toohello 站台中。</span><span class="sxs-lookup"><span data-stu-id="6727e-292">Parameterize hello tokens, setting hello parameter when hello token is returned from hello authenticator, and using it in hello query toohello site.</span></span>
  <span data-ttu-id="6727e-293">（visual Studio 嘗試 tooparameterize hello 測試，但不會正確地參數化 hello 語彙基元）。</span><span class="sxs-lookup"><span data-stu-id="6727e-293">(Visual Studio attempts tooparameterize hello test, but does not correctly parameterize hello tokens.)</span></span>


## <a name="performance-tests"></a><span data-ttu-id="6727e-294">效能測試</span><span class="sxs-lookup"><span data-stu-id="6727e-294">Performance tests</span></span>
<span data-ttu-id="6727e-295">您可以在網站上執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-295">You can run a load test on your website.</span></span> <span data-ttu-id="6727e-296">像 hello 可用性測試，您可以從我們 hello 世界各地點傳送的簡單要求或多個步驟要求。</span><span class="sxs-lookup"><span data-stu-id="6727e-296">Like hello availability test, you can send either simple requests or multi-step requests from our points around hello world.</span></span> <span data-ttu-id="6727e-297">不同於可用性測試，許多要求傳送時會同時模擬多位使用者。</span><span class="sxs-lookup"><span data-stu-id="6727e-297">Unlike an availability test, many requests are sent, simulating multiple simultaneous users.</span></span>

<span data-ttu-id="6727e-298">從 hello 概觀刀鋒視窗中，開啟**設定**，**效能測試**。</span><span class="sxs-lookup"><span data-stu-id="6727e-298">From hello Overview blade, open **Settings**, **Performance Tests**.</span></span> <span data-ttu-id="6727e-299">當您建立測試時，您獲邀參與 tooconnect tooor 建立 Visual Studio Team Services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6727e-299">When you create a test, you are invited tooconnect tooor create a Visual Studio Team Services account.</span></span>

<span data-ttu-id="6727e-300">Hello 測試完成時，便會顯示回應時間與成功率。</span><span class="sxs-lookup"><span data-stu-id="6727e-300">When hello test is complete, you are shown response times and success rates.</span></span>


![效能測試](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> <span data-ttu-id="6727e-302">tooobserve hello 效果的效能測試中，使用[即時資料流](app-insights-live-stream.md)和[Profiler](app-insights-profiler.md)。</span><span class="sxs-lookup"><span data-stu-id="6727e-302">tooobserve hello effects of a performance test, use [Live Stream](app-insights-live-stream.md) and [Profiler](app-insights-profiler.md).</span></span>
>

## <a name="automation"></a><span data-ttu-id="6727e-303">自動化</span><span class="sxs-lookup"><span data-stu-id="6727e-303">Automation</span></span>
* <span data-ttu-id="6727e-304">[使用 PowerShell 指令碼 tooset 可用性測試](app-insights-powershell.md#add-an-availability-test)自動。</span><span class="sxs-lookup"><span data-stu-id="6727e-304">[Use PowerShell scripts tooset up an availability test](app-insights-powershell.md#add-an-availability-test) automatically.</span></span>
* <span data-ttu-id="6727e-305">設定會在產生警示時呼叫的 [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="6727e-305">Set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span>

## <span data-ttu-id="6727e-306"><a name="qna"></a>有疑問嗎？</span><span class="sxs-lookup"><span data-stu-id="6727e-306"><a name="qna"></a>Questions?</span></span> <span data-ttu-id="6727e-307">有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="6727e-307">Problems?</span></span>
* <span data-ttu-id="6727e-308">*可以從我的 Web 測試呼叫程式碼嗎？*</span><span class="sxs-lookup"><span data-stu-id="6727e-308">*Can I call code from my web test?*</span></span>

    <span data-ttu-id="6727e-309">否。</span><span class="sxs-lookup"><span data-stu-id="6727e-309">No.</span></span> <span data-ttu-id="6727e-310">hello hello 測試步驟必須在 hello.webtest 檔案。</span><span class="sxs-lookup"><span data-stu-id="6727e-310">hello steps of hello test must be in hello .webtest file.</span></span> <span data-ttu-id="6727e-311">而且您不能呼叫其他 Web 測試或使用迴圈。</span><span class="sxs-lookup"><span data-stu-id="6727e-311">And you can't call other web tests or use loops.</span></span> <span data-ttu-id="6727e-312">但是這裡有一些您會覺得有用的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="6727e-312">But there are several plug-ins that you might find helpful.</span></span>
* <span data-ttu-id="6727e-313">*是否支援 HTTPS？*</span><span class="sxs-lookup"><span data-stu-id="6727e-313">*Is HTTPS supported?*</span></span>

    <span data-ttu-id="6727e-314">我們支援 TLS 1.1 和 TLS 1.2。</span><span class="sxs-lookup"><span data-stu-id="6727e-314">We support TLS 1.1 and TLS 1.2.</span></span>
* <span data-ttu-id="6727e-315">*「Web 測試」和「可用性測試」之間有任何差異嗎？*</span><span class="sxs-lookup"><span data-stu-id="6727e-315">*Is there a difference between "web tests" and "availability tests"?*</span></span>

    <span data-ttu-id="6727e-316">hello 兩個詞彙都可以參考交換使用。</span><span class="sxs-lookup"><span data-stu-id="6727e-316">hello two terms may be referenced interchangeably.</span></span> <span data-ttu-id="6727e-317">可用性測試更泛型的詞彙，其中包含單一 URL ping hello 除了測試 toohello multi-step web 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-317">Availability tests is a more generic term that includes hello single URL ping tests in addition toohello multi-step web tests.</span></span>
* <span data-ttu-id="6727e-318">*我希望 toouse 可用性測試我們內部執行伺服器上的防火牆後面。*</span><span class="sxs-lookup"><span data-stu-id="6727e-318">*I'd like toouse availability tests on our internal server that runs behind a firewall.*</span></span>

    <span data-ttu-id="6727e-319">有兩個可能的解決方案：</span><span class="sxs-lookup"><span data-stu-id="6727e-319">There are two possible solutions:</span></span>
    
    * <span data-ttu-id="6727e-320">設定您防火牆 toopermit 來自內送要求 hello [IP 位址的我們的測試代理程式](app-insights-ip-addresses.md)。</span><span class="sxs-lookup"><span data-stu-id="6727e-320">Configure your firewall toopermit incoming requests from hello [IP addresses of our web test agents](app-insights-ip-addresses.md).</span></span>
    * <span data-ttu-id="6727e-321">撰寫您自己的程式碼 tooperiodically 測試您的內部伺服器。</span><span class="sxs-lookup"><span data-stu-id="6727e-321">Write your own code tooperiodically test your internal server.</span></span> <span data-ttu-id="6727e-322">Hello 程式碼做為背景處理序在伺服器上執行測試您的防火牆後面。</span><span class="sxs-lookup"><span data-stu-id="6727e-322">Run hello code as a background process on a test server behind your firewall.</span></span> <span data-ttu-id="6727e-323">您的測試程序可以傳送其結果 tooApplication Insights 使用[TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) hello core SDK 封裝中的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6727e-323">Your test process can send its results tooApplication Insights by using [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in hello core SDK package.</span></span> <span data-ttu-id="6727e-324">這需要您測試伺服器 toohave 傳出存取 toohello Application Insights 擷取的端點，但這是多較小的安全性風險比 hello 另一種可允許傳入要求。</span><span class="sxs-lookup"><span data-stu-id="6727e-324">This requires your test server toohave outgoing access toohello Application Insights ingestion endpoint, but that is a much smaller security risk than hello alternative of permitting incoming requests.</span></span> <span data-ttu-id="6727e-325">hello 結果不會出現在 hello 可用性 web 測試的刀鋒視窗，但會顯示為可用性結果中分析、 搜尋和度量的總管。</span><span class="sxs-lookup"><span data-stu-id="6727e-325">hello results will not appear in hello availability web tests blades, but appears as availability results in Analytics, Search, and Metric Explorer.</span></span>
* <span data-ttu-id="6727e-326">*上傳多步驟 Web 測試失敗*</span><span class="sxs-lookup"><span data-stu-id="6727e-326">*Uploading a multi-step web test fails*</span></span>

    <span data-ttu-id="6727e-327">有 300 K 的大小限制。</span><span class="sxs-lookup"><span data-stu-id="6727e-327">There's a size limit of 300 K.</span></span>

    <span data-ttu-id="6727e-328">不支援迴圈。</span><span class="sxs-lookup"><span data-stu-id="6727e-328">Loops aren't supported.</span></span>

    <span data-ttu-id="6727e-329">不支援參考 tooother web 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-329">References tooother web tests aren't supported.</span></span>

    <span data-ttu-id="6727e-330">不支援資料來源。</span><span class="sxs-lookup"><span data-stu-id="6727e-330">Data sources aren't supported.</span></span>
* <span data-ttu-id="6727e-331">*多步驟測試未完成*</span><span class="sxs-lookup"><span data-stu-id="6727e-331">*My multi-step test doesn't complete*</span></span>

    <span data-ttu-id="6727e-332">每個測試有 100 個要求的限制。</span><span class="sxs-lookup"><span data-stu-id="6727e-332">There's a limit of 100 requests per test.</span></span>

    <span data-ttu-id="6727e-333">如果它執行時間長於兩分鐘的時間，停止 hello 測試。</span><span class="sxs-lookup"><span data-stu-id="6727e-333">hello test is stopped if it runs longer than two minutes.</span></span>
* <span data-ttu-id="6727e-334">*如何使用用戶端憑證執行測試？*</span><span class="sxs-lookup"><span data-stu-id="6727e-334">*How can I run a test with client certificates?*</span></span>

    <span data-ttu-id="6727e-335">很抱歉，我們不支援此功能。</span><span class="sxs-lookup"><span data-stu-id="6727e-335">We don't support that, sorry.</span></span>


## <span data-ttu-id="6727e-336"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="6727e-336"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="6727e-337">[搜尋診斷記錄][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="6727e-337">[Search diagnostic logs][diagnostic]</span></span>

<span data-ttu-id="6727e-338">[疑難排解][qna]</span><span class="sxs-lookup"><span data-stu-id="6727e-338">[Troubleshooting][qna]</span></span>

[<span data-ttu-id="6727e-339">Web 測試代理程式的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="6727e-339">IP addresses of web test agents</span></span>](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
