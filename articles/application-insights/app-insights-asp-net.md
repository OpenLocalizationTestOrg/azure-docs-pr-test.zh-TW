---
title: "設定適用於使用 Azure Application Insights 的 ASP.NET web 應用程式分析 aaaSet |Microsoft 文件"
description: "針對裝載在內部部署環境或 Azure 的 ASP.NET 網站設定效能、可用性及使用情況分析。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="49bfa-103">設定 ASP.NET 網站的 Application Insights</span><span class="sxs-lookup"><span data-stu-id="49bfa-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="49bfa-104">此程序會設定您 ASP.NET web 應用程式 toosend 遙測 toohello [Azure Application Insights](app-insights-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="49bfa-104">This procedure configures your ASP.NET web app toosend telemetry toohello [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="49bfa-105">這也適用於裝載在 IIS 伺服器或 hello 雲端中的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="49bfa-105">It works for ASP.NET apps that are hosted either in your own IIS server or in hello Cloud.</span></span> <span data-ttu-id="49bfa-106">取得圖表並功能強大的查詢語言來協助您了解 hello 應用程式效能和人員使用的方式，再加上自動警示失敗或效能問題。</span><span class="sxs-lookup"><span data-stu-id="49bfa-106">You get charts and a powerful query language that help you understand hello performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="49bfa-107">許多開發人員會覺得這些功能很好，但您也可以擴充和自訂 hello 遙測，如果您需要。</span><span class="sxs-lookup"><span data-stu-id="49bfa-107">Many developers find these features great as they are, but you can also extend and customize hello telemetry if you need to.</span></span>

<span data-ttu-id="49bfa-108">在 Visual Studio 中只需按幾下滑鼠即可進行安裝。</span><span class="sxs-lookup"><span data-stu-id="49bfa-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="49bfa-109">您擁有 hello 選項 tooavoid 費用限制 hello 的遙測資料的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="49bfa-109">You have hello option tooavoid charges by limiting hello volume of telemetry.</span></span> <span data-ttu-id="49bfa-110">這可讓您 tooexperiment 和偵錯或 toomonitor 不許多使用者的站台。</span><span class="sxs-lookup"><span data-stu-id="49bfa-110">This allows you tooexperiment and debug, or toomonitor a site with not many users.</span></span> <span data-ttu-id="49bfa-111">當您決定您想繼續 toogo 和監視您的生產網站時，限制它是簡單 tooraise hello 更新版本。</span><span class="sxs-lookup"><span data-stu-id="49bfa-111">When you decide you want toogo ahead and monitor your production site, it's easy tooraise hello limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="49bfa-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="49bfa-112">Before you start</span></span>
<span data-ttu-id="49bfa-113">您需要：</span><span class="sxs-lookup"><span data-stu-id="49bfa-113">You need:</span></span>

* <span data-ttu-id="49bfa-114">Visual Studio 2013 Update 3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="49bfa-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="49bfa-115">越新版越好。</span><span class="sxs-lookup"><span data-stu-id="49bfa-115">Later is better.</span></span>
* <span data-ttu-id="49bfa-116">訂用帳戶太[Microsoft Azure](http://azure.com)。</span><span class="sxs-lookup"><span data-stu-id="49bfa-116">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="49bfa-117">如果您的小組或組織有 Azure 訂用帳戶，hello 擁有者可以將您加入 tooit，使用您[Microsoft 帳戶](http://live.com)。</span><span class="sxs-lookup"><span data-stu-id="49bfa-117">If your team or organization has an Azure subscription, hello owner can add you tooit, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="49bfa-118">如果您想要，有替代主題 toolook 在：</span><span class="sxs-lookup"><span data-stu-id="49bfa-118">There are alternative topics toolook at if you are interested in:</span></span>

* [<span data-ttu-id="49bfa-119">在執行階段檢測 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="49bfa-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="49bfa-120">Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="49bfa-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="49bfa-121"><a name="ide"></a>步驟 1： 加入 hello Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="49bfa-121"><a name="ide"></a> Step 1: Add hello Application Insights SDK</span></span>

<span data-ttu-id="49bfa-122">在 [方案總管] 中以滑鼠右鍵按一下 Web 應用程式，然後選擇 [新增] > [Application Insights 遙測] 或 [設定 Application Insights]。</span><span class="sxs-lookup"><span data-stu-id="49bfa-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![[方案總管] 的螢幕擷取畫面，其中已醒目提示 [新增 Application Insights 遙測]](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="49bfa-124">（在 Visual Studio 2015，另外還有 hello 新增專案 對話方塊中的選項 tooadd Application Insights。）</span><span class="sxs-lookup"><span data-stu-id="49bfa-124">(In Visual Studio 2015, there's also an option tooadd Application Insights in hello New Project dialog.)</span></span>

<span data-ttu-id="49bfa-125">繼續 toohello Application Insights 組態 頁面上：</span><span class="sxs-lookup"><span data-stu-id="49bfa-125">Continue toohello Application Insights configuration page:</span></span>

![[向 Application Insights 註冊您的應用程式] 頁面的螢幕擷取畫面](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="49bfa-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="49bfa-127">**a.**</span></span> <span data-ttu-id="49bfa-128">選取 hello 帳戶和您使用 tooaccess Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="49bfa-128">Select hello account and subscription that you use tooaccess Azure.</span></span>

<span data-ttu-id="49bfa-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="49bfa-129">**b.**</span></span> <span data-ttu-id="49bfa-130">選取您要 toosee hello 資料從您的應用程式的 Azure 中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="49bfa-130">Select hello resource in Azure where you want toosee hello data from your app.</span></span> <span data-ttu-id="49bfa-131">通常︰</span><span class="sxs-lookup"><span data-stu-id="49bfa-131">Usually:</span></span>

* <span data-ttu-id="49bfa-132">[將單一資源使用於單一應用程式的不同元件](app-insights-monitor-multi-role-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="49bfa-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="49bfa-133">為不相關的應用程式建立個別的資源。</span><span class="sxs-lookup"><span data-stu-id="49bfa-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="49bfa-134">如果您想 tooset hello 資源群組或 hello 位置儲存您的資料，請按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="49bfa-134">If you want tooset hello resource group or hello location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="49bfa-135">資源群組是使用的 toocontrol 存取 toodata。</span><span class="sxs-lookup"><span data-stu-id="49bfa-135">Resource groups are used toocontrol access toodata.</span></span> <span data-ttu-id="49bfa-136">相同，例如 hello 如果您有數個應用程式部分系統，您可能會其 Application Insights 資料放入 hello 相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="49bfa-136">For example, if you have several apps that form part of hello same system, you might put their Application Insights data in hello same resource group.</span></span>

<span data-ttu-id="49bfa-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="49bfa-137">**c.**</span></span> <span data-ttu-id="49bfa-138">在 hello 可用的資料磁碟區的限制，tooavoid 費用設定的端點。</span><span class="sxs-lookup"><span data-stu-id="49bfa-138">Set a cap at hello free data volume limit, tooavoid charges.</span></span> <span data-ttu-id="49bfa-139">Application Insights 是釋放 tooa 特定大量的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="49bfa-139">Application Insights is free up tooa certain volume of telemetry.</span></span> <span data-ttu-id="49bfa-140">建立 hello 資源之後，您可以變更您選取 hello 入口網站中的開啟**功能 + 定價** > **資料磁碟區管理** > **每日磁碟區的 cap**。</span><span class="sxs-lookup"><span data-stu-id="49bfa-140">After hello resource is created, you can change your selection in hello portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="49bfa-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="49bfa-141">**d.**</span></span> <span data-ttu-id="49bfa-142">按一下**註冊**toogo 繼續並設定 Application Insights web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="49bfa-142">Click **Register** toogo ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="49bfa-143">遙測傳送 toohello [Azure 入口網站](https://portal.azure.com)，偵錯期間和之後您已經發行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="49bfa-143">Telemetry will be sent toohello [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="49bfa-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="49bfa-144">**e.**</span></span> <span data-ttu-id="49bfa-145">如果偵錯時，您不想 toosend 遙測 toohello 入口網站，只新增 hello Application Insights SDK tooyour 應用程式，但不在 hello 入口網站中設定資源。</span><span class="sxs-lookup"><span data-stu-id="49bfa-145">If you don't want toosend telemetry toohello portal while you're debugging, just add hello Application Insights SDK tooyour app but don't configure a resource in hello portal.</span></span> <span data-ttu-id="49bfa-146">在偵錯時，您就可以在 Visual Studio 中的能夠 toosee 遙測。</span><span class="sxs-lookup"><span data-stu-id="49bfa-146">You will be able toosee telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="49bfa-147">更新版本中，您可以傳回 toothis 組態 頁面上，或您無法等到部署您的應用程式之後和[在執行階段遙測切換](app-insights-monitor-performance-live-website-now.md)。</span><span class="sxs-lookup"><span data-stu-id="49bfa-147">Later, you can return toothis configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="49bfa-148"><a name="run"></a> 步驟 2︰執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="49bfa-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="49bfa-149">按 F5 執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="49bfa-149">Run your app with F5.</span></span> <span data-ttu-id="49bfa-150">開啟不同頁面 toogenerate 某些遙測。</span><span class="sxs-lookup"><span data-stu-id="49bfa-150">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="49bfa-151">在 Visual Studio 中，您會看到 hello 事件已記錄的計數。</span><span class="sxs-lookup"><span data-stu-id="49bfa-151">In Visual Studio, you see a count of hello events that have been logged.</span></span>

![Visual Studio 的螢幕擷取畫面。](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="49bfa-154">步驟 3：查看遙測</span><span class="sxs-lookup"><span data-stu-id="49bfa-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="49bfa-155">您可以看到您在 Visual Studio 或 hello Application Insights 入口網站中的遙測。</span><span class="sxs-lookup"><span data-stu-id="49bfa-155">You can see your telemetry either in Visual Studio or in hello Application Insights web portal.</span></span> <span data-ttu-id="49bfa-156">搜尋遙測 toohelp Visual Studio 中偵錯應用程式。</span><span class="sxs-lookup"><span data-stu-id="49bfa-156">Search telemetry in Visual Studio toohelp you debug your app.</span></span> <span data-ttu-id="49bfa-157">監視效能和 hello web 入口網站時您的系統是即時的使用量。</span><span class="sxs-lookup"><span data-stu-id="49bfa-157">Monitor performance and usage in hello web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="49bfa-158">在 Visual Studio 中查看遙測</span><span class="sxs-lookup"><span data-stu-id="49bfa-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="49bfa-159">在 Visual Studio 中，開啟 hello Application Insights 視窗。</span><span class="sxs-lookup"><span data-stu-id="49bfa-159">In Visual Studio, open hello Application Insights window.</span></span> <span data-ttu-id="49bfa-160">按一下 hello **Application Insights**按鈕，或以滑鼠右鍵按一下您的專案，在 方案總管 中，選取**Application Insights**，然後按一下**搜尋即時遙測**.</span><span class="sxs-lookup"><span data-stu-id="49bfa-160">Either click hello **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="49bfa-161">在 hello Visual Studio Application Insights 搜尋視窗中，請參閱 hello**偵錯工作階段從資料**遙測 hello 伺服器端應用程式中產生的檢視。</span><span class="sxs-lookup"><span data-stu-id="49bfa-161">In hello Visual Studio Application Insights Search window, see hello **Data from Debug session** view for telemetry generated in hello server side of your app.</span></span> <span data-ttu-id="49bfa-162">試驗一下 hello 篩選，按一下任何事件 toosee 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="49bfa-162">Experiment with hello filters, and click any event toosee more detail.</span></span>

![螢幕擷取畫面的 hello hello Application Insights 視窗中檢視偵錯工作階段的資料。](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="49bfa-164">如果您沒有看到任何資料，請確定 hello 的時間範圍內正確，然後按一下 hello 搜尋圖示。</span><span class="sxs-lookup"><span data-stu-id="49bfa-164">If you don't see any data, make sure hello time range is correct, and click hello Search icon.</span></span>

<span data-ttu-id="49bfa-165">[深入了解 Visual Studio 中的 Application Insights 工具](app-insights-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="49bfa-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="49bfa-166">請參閱 web 入口網站中的遙測</span><span class="sxs-lookup"><span data-stu-id="49bfa-166">See telemetry in web portal</span></span>

<span data-ttu-id="49bfa-167">（除非您選擇 tooinstall 只有 hello SDK），您也可以查看 hello Application Insights 入口網站中的遙測。</span><span class="sxs-lookup"><span data-stu-id="49bfa-167">You can also see telemetry in hello Application Insights web portal (unless you chose tooinstall only hello SDK).</span></span> <span data-ttu-id="49bfa-168">hello 入口網站有多個圖表、 分析工具和跨元件檢視比 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="49bfa-168">hello portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="49bfa-169">hello 入口網站也提供警示。</span><span class="sxs-lookup"><span data-stu-id="49bfa-169">hello portal also provides alerts.</span></span>

<span data-ttu-id="49bfa-170">開啟 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="49bfa-170">Open your Application Insights resource.</span></span> <span data-ttu-id="49bfa-171">請登入 toohello [Azure 入口網站](https://portal.azure.com/)和尋找它，或以滑鼠右鍵按一下 hello 專案在 Visual Studio 中，並讓它帶您前往該處。</span><span class="sxs-lookup"><span data-stu-id="49bfa-171">Either sign in toohello [Azure portal](https://portal.azure.com/) and find it there, or right-click hello project in Visual Studio, and let it take you there.</span></span>

![螢幕擷取畫面的 Visual Studio 中，顯示如何 tooopen hello Application Insights 入口網站](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="49bfa-173">如果您收到存取錯誤： 有多個 Microsoft 認證集，而且您登入一組錯誤 hello？</span><span class="sxs-lookup"><span data-stu-id="49bfa-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with hello wrong set?</span></span> <span data-ttu-id="49bfa-174">在 hello 入口網站登出並再次登入。</span><span class="sxs-lookup"><span data-stu-id="49bfa-174">In hello portal, sign out and sign in again.</span></span>

<span data-ttu-id="49bfa-175">hello 入口網站開啟檢視的 hello 遙測資料從您的應用程式上。</span><span class="sxs-lookup"><span data-stu-id="49bfa-175">hello portal opens on a view of hello telemetry from your app.</span></span>

![Application Insights 概觀頁面的螢幕擷取畫面](./media/app-insights-asp-net/66.png)

<span data-ttu-id="49bfa-177">在 hello 入口網站中，按一下任何磚或圖表 toosee 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="49bfa-177">In hello portal, click any tile or chart toosee more detail.</span></span>

<span data-ttu-id="49bfa-178">[深入了解在 hello Azure 入口網站中使用 Application Insights](app-insights-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="49bfa-178">[Learn more about using Application Insights in hello Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="49bfa-179">步驟 4：發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="49bfa-179">Step 4: Publish your app</span></span>
<span data-ttu-id="49bfa-180">發行您的應用程式 tooyour IIS 伺服器或 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="49bfa-180">Publish your app tooyour IIS server or tooAzure.</span></span> <span data-ttu-id="49bfa-181">監看式[即時度量資料流](app-insights-metrics-explorer.md#live-metrics-stream)toomake 確定可以順利執行。</span><span class="sxs-lookup"><span data-stu-id="49bfa-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) toomake sure everything is running smoothly.</span></span>

<span data-ttu-id="49bfa-182">您遙測中的積存累積 hello Application Insights 入口網站，您可以用它來監視度量，搜尋您遙測，並設定[儀表板](app-insights-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="49bfa-182">Your telemetry builds up in hello Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="49bfa-183">您也可以使用 hello 強大[記錄分析查詢語言](https://docs.loganalytics.io/)tooanalyze 使用量和效能或 toofind 特定事件。</span><span class="sxs-lookup"><span data-stu-id="49bfa-183">You can also use hello powerful [Log Analytics query language](https://docs.loganalytics.io/) tooanalyze usage and performance, or toofind specific events.</span></span>

<span data-ttu-id="49bfa-184">您也可以繼續 tooanalyze 您遙測中的[Visual Studio](app-insights-visual-studio.md)，例如診斷搜尋的工具和[趨勢](app-insights-visual-studio-trends.md)。</span><span class="sxs-lookup"><span data-stu-id="49bfa-184">You can also continue tooanalyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="49bfa-185">如果您的應用程式傳送足夠的遙測 tooapproach hello[節流限制](app-insights-pricing.md#limits-summary)自動[取樣](app-insights-sampling.md)上切換。</span><span class="sxs-lookup"><span data-stu-id="49bfa-185">If your app sends enough telemetry tooapproach hello [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="49bfa-186">取樣可減少您應用程式傳送的同時保留供診斷之用的資料產生相互關聯的遙測 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="49bfa-186">Sampling reduces hello quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="49bfa-187"><a name="land"></a> 您全都準備好了</span><span class="sxs-lookup"><span data-stu-id="49bfa-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="49bfa-188">恭喜！</span><span class="sxs-lookup"><span data-stu-id="49bfa-188">Congratulations!</span></span> <span data-ttu-id="49bfa-189">您已安裝應用程式中的 hello Application Insights 套件，並在 Azure 上設定 toosend 遙測 toohello Application Insights 服務。</span><span class="sxs-lookup"><span data-stu-id="49bfa-189">You installed hello Application Insights package in your app, and configured it toosend telemetry toohello Application Insights service on Azure.</span></span>

![遙測移動的圖表](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="49bfa-191">hello 收到您的應用程式遙測的 Azure 資源由*檢測金鑰*。</span><span class="sxs-lookup"><span data-stu-id="49bfa-191">hello Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="49bfa-192">您可以在 hello ApplicationInsights.config 檔案中找到此機碼。</span><span class="sxs-lookup"><span data-stu-id="49bfa-192">You'll find this key in hello ApplicationInsights.config file.</span></span>


## <a name="upgrade-toofuture-sdk-versions"></a><span data-ttu-id="49bfa-193">升級 toofuture SDK 版本</span><span class="sxs-lookup"><span data-stu-id="49bfa-193">Upgrade toofuture SDK versions</span></span>
<span data-ttu-id="49bfa-194">tooupgrade tooa[新版 hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)，開啟 hello **NuGet 套件管理員**同樣地，和已安裝的封裝上的篩選。</span><span class="sxs-lookup"><span data-stu-id="49bfa-194">tooupgrade tooa [new release of hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open hello **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="49bfa-195">選取 **Microsoft.ApplicationInsights.Web**，然後選擇 [升級]。</span><span class="sxs-lookup"><span data-stu-id="49bfa-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="49bfa-196">如果您進行任何自訂 tooApplicationInsights.config，儲存的副本，然後再升級。</span><span class="sxs-lookup"><span data-stu-id="49bfa-196">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="49bfa-197">然後，您的變更合併 hello 新版本。</span><span class="sxs-lookup"><span data-stu-id="49bfa-197">Then, merge your changes into hello new version.</span></span>

## <a name="video"></a><span data-ttu-id="49bfa-198">影片</span><span class="sxs-lookup"><span data-stu-id="49bfa-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="49bfa-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49bfa-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="49bfa-200">更多遙測</span><span class="sxs-lookup"><span data-stu-id="49bfa-200">More telemetry</span></span>

* <span data-ttu-id="49bfa-201">**[瀏覽器和頁面載入資料](app-insights-javascript.md)** - 在您的網頁中插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="49bfa-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="49bfa-202">**[取得更詳細的相依性和例外狀況監視](app-insights-monitor-performance-live-website-now.md)** - 在您的伺服器上安裝狀態監視器。</span><span class="sxs-lookup"><span data-stu-id="49bfa-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="49bfa-203">**[程式碼的自訂事件](app-insights-api-custom-events-metrics.md)** toocount、 時間、 或量值使用者動作。</span><span class="sxs-lookup"><span data-stu-id="49bfa-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** toocount, time, or measure user actions.</span></span>
* <span data-ttu-id="49bfa-204">**[取得記錄資料](app-insights-asp-net-trace-logs.md)** - 將記錄資料與您的遙測相互關聯。</span><span class="sxs-lookup"><span data-stu-id="49bfa-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="49bfa-205">分析</span><span class="sxs-lookup"><span data-stu-id="49bfa-205">Analysis</span></span>

* <span data-ttu-id="49bfa-206">**[在 Visual Studio 中使用 Application Insights](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="49bfa-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="49bfa-207">包含有關使用遙測，偵錯資訊診斷搜尋] 和 [toocode 鑽研。</span><span class="sxs-lookup"><span data-stu-id="49bfa-207">Includes information about debugging with telemetry, diagnostic search, and drill through toocode.</span></span>
* <span data-ttu-id="49bfa-208">**[使用 hello Application Insights 入口網站](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="49bfa-208">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="49bfa-209">包括儀表板、功能強大的診斷和分析工具、警示、即時的應用程式相依性對應，以及遙測匯出的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="49bfa-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="49bfa-210">**[分析](app-insights-analytics-tour.md)** -hello 功能強大的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="49bfa-210">**[Analytics](app-insights-analytics-tour.md)** - hello powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="49bfa-211">Alerts</span><span class="sxs-lookup"><span data-stu-id="49bfa-211">Alerts</span></span>

* <span data-ttu-id="49bfa-212">[可用性測試](app-insights-monitor-web-app-availability.md)： 建立測試 toomake 確定您的網站會顯示 hello 網站上。</span><span class="sxs-lookup"><span data-stu-id="49bfa-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests toomake sure your site is visible on hello web.</span></span>
* <span data-ttu-id="49bfa-213">[智慧型診斷](app-insights-proactive-diagnostics.md)： 這些測試自動執行，因此您不需要 toodo 任何項目 tooset 註冊它們。</span><span class="sxs-lookup"><span data-stu-id="49bfa-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have toodo anything tooset them up.</span></span> <span data-ttu-id="49bfa-214">它們會讓您知道應用程式是否有不尋常的失敗要求率。</span><span class="sxs-lookup"><span data-stu-id="49bfa-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="49bfa-215">[度量的警示](app-insights-alerts.md)： 設定這些 toowarn 您如果度量超出閾值。</span><span class="sxs-lookup"><span data-stu-id="49bfa-215">[Metric alerts](app-insights-alerts.md): Set these toowarn you if a metric crosses a threshold.</span></span> <span data-ttu-id="49bfa-216">您可以在撰寫於程式碼中的自訂度量上設定它們。</span><span class="sxs-lookup"><span data-stu-id="49bfa-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="49bfa-217">自動化</span><span class="sxs-lookup"><span data-stu-id="49bfa-217">Automation</span></span>

* [<span data-ttu-id="49bfa-218">自動建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="49bfa-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
