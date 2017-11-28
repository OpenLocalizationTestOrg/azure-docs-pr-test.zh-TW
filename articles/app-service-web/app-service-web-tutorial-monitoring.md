---
title: "aaaMonitor Web 應用程式 |Microsoft 文件"
description: "深入了解如何註冊 Web 應用程式上的監視 tooset"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="9ad8e-103">監視 App Service</span><span class="sxs-lookup"><span data-stu-id="9ad8e-103">Monitor App Service</span></span>
<span data-ttu-id="9ad8e-104">本教學課程會逐步引導您透過監視您的應用程式和使用 hello 內建的平台工具 toosolve 問題發生時。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="9ad8e-105">這份文件的每個章節都會復習特定的功能。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="9ad8e-106">同時使用 hello 功能可讓您：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-106">Using hello features together let you:</span></span>
- <span data-ttu-id="9ad8e-107">識別應用程式中的問題。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="9ad8e-108">判斷當 hello 問題的起因是您的程式碼或 hello 平台。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="9ad8e-109">請縮小您的程式碼中的 hello 問題 hello 來源。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="9ad8e-110">偵錯和修正 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9ad8e-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="9ad8e-111">Before you begin</span></span>
- <span data-ttu-id="9ad8e-112">您需要 Web 應用程式 toomonitor 並遵循 hello 所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="9ad8e-113">您可以建立應用程式遵循 hello 中所述的 hello 步驟[建立 ASP.NET 應用程式在 Azure SQL Database 中](app-service-web-tutorial-dotnet-sqldatabase.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="9ad8e-114">如果您想 tootry**遠端偵錯**應用程式中，您需要 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="9ad8e-115">如果您還沒有安裝 Visual Studio 2017，您可以下載並使用可用的 hello [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="9ad8e-116">請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="9ad8e-117"><a name="metrics"></a> 步驟 1 - 檢視計量</span><span class="sxs-lookup"><span data-stu-id="9ad8e-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="9ad8e-118">**度量**會很有用的 toounderstand:</span><span class="sxs-lookup"><span data-stu-id="9ad8e-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="9ad8e-119">應用程式健全狀況</span><span class="sxs-lookup"><span data-stu-id="9ad8e-119">Application health</span></span>
- <span data-ttu-id="9ad8e-120">應用程式效能</span><span class="sxs-lookup"><span data-stu-id="9ad8e-120">App performance</span></span>
- <span data-ttu-id="9ad8e-121">資源耗用量</span><span class="sxs-lookup"><span data-stu-id="9ad8e-121">Resource consumption</span></span>

<span data-ttu-id="9ad8e-122">當調查應用程式問題，檢閱度量是很好的起點 toostart。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="9ad8e-123">Azure 入口網站已檢查您的應用程式使用的 hello 度量快速 toovisually **Azure 監視器**。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="9ad8e-124">計量會提供應用程式之數個金鑰彙總的歷程記錄檢視。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="9ad8e-125">App service 中裝載任何應用程式，您應監視 hello Web 應用程式和 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="9ad8e-126">App Service 方案代表 hello 集合使用的實體資源 toohost 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="9ad8e-127">所有應用程式指派 tooan 它允許您 toosave 成本裝載多個應用程式時所定義的應用程式服務計劃共用 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="9ad8e-128">App Service 方案可定義：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-128">App Service plans define:</span></span>
> * <span data-ttu-id="9ad8e-129">區域：北歐、美國東部、東南亞等。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="9ad8e-130">執行個體大小：小型、中型、大型等。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="9ad8e-131">級別計數：一、二或三個執行個體等。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="9ad8e-132">SKU：免費、共用、基本、標準、進階等。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="9ad8e-133">Web 應用程式，請移 toohello tooreview 度量**概觀**刀鋒視窗中的 hello 應用程式中，您想 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="9ad8e-134">從這裡開始，您能以**監視圖格**的形式檢視應用程式計量的圖表。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="9ad8e-135">按一下 hello 磚 tooedit 並設定哪些度量 tooview，hello 時間範圍 toodisplay。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="9ad8e-136">根據預設 hello 資源刀鋒視窗會提供 hello 應用程式要求的檢視和 hello 過去一小時內的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="9ad8e-137">![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="9ad8e-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="9ad8e-138">您可以看到在 hello 範例中，我們會有應用程式會將產生許多**HTTP 伺服器錯誤**。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="9ad8e-139">hello 大量的錯誤是 hello tooinvestigate 我們需要此應用程式的第一個指示。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="9ad8e-140">深入了解 Azure 監視器以 hello 下列連結：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="9ad8e-141">開始使用 Azure 監視器</span><span class="sxs-lookup"><span data-stu-id="9ad8e-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="9ad8e-142">Azure 計量</span><span class="sxs-lookup"><span data-stu-id="9ad8e-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="9ad8e-143">支援 Azure 監視器的計量</span><span class="sxs-lookup"><span data-stu-id="9ad8e-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="9ad8e-144">Azure 儀表板</span><span class="sxs-lookup"><span data-stu-id="9ad8e-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="9ad8e-145"><a name="alerts"></a> 步驟 2 - 設定警示</span><span class="sxs-lookup"><span data-stu-id="9ad8e-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="9ad8e-146">**警示**可以設定的 tootrigger 應用程式的特定條件。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="9ad8e-147">在[步驟 1-檢視度量](#metrics)，我們可了解 hello 應用程式有大量的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="9ad8e-148">可讓您設定警示 tooautomatically 在錯誤發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="9ad8e-149">在此情況下，我們想 hello 警示 toosend 電子郵件與每次 hello HTTP 50 X 錯誤的數目超過某個臨界值。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="9ad8e-150">toocreate 的警示，瀏覽過**監視** > **警示**按一下**[+] 新增警示**。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alerts](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="9ad8e-152">提供 hello 警示設定中的值：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="9ad8e-153">**資源：** hello 網站 toomonitor hello 警示。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="9ad8e-154">**名稱︰**您警示的名稱，在此案例中為︰高 HTTP 50X。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="9ad8e-155">**描述︰**這項警示所查看的純文字說明。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="9ad8e-156">**警示項目︰**警示可以查看計量或事件，此範例中，我們要查看計量。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="9ad8e-157">**計量：**哪些度量 toomonitor，在此情況下： *HTTP 伺服器錯誤*。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="9ad8e-158">**條件：**當 tooalert，在此情況下選取 hello*大於*選項。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="9ad8e-159">**臨界值：**什麼是在此情況下，值 toolook: *400*。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="9ad8e-160">**週期：**在 hello 平均標準值上操作的警示。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="9ad8e-161">較短的時間會造成警示較敏感。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="9ad8e-162">在此情況下，我們看看 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="9ad8e-163">**電子郵件擁有者和參與者︰**在此情況下︰已啟用。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="9ad8e-164">既然 hello 警示建立電子郵件會傳送每次 hello 應用程式超過設定的 hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="9ad8e-165">作用中警示也應審核 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![觸發的警示](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="9ad8e-167">深入了解 Azure 警示以 hello 下列連結：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="9ad8e-168">Microsoft Azure 中的警示是什麼</span><span class="sxs-lookup"><span data-stu-id="9ad8e-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="9ad8e-169">對計量採取動作</span><span class="sxs-lookup"><span data-stu-id="9ad8e-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="9ad8e-170">建立計量警示</span><span class="sxs-lookup"><span data-stu-id="9ad8e-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="9ad8e-171"><a name="companion"></a> 步驟 3 - App Service Companion</span><span class="sxs-lookup"><span data-stu-id="9ad8e-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="9ad8e-172">**應用程式服務隨附**提供便利的方式 toomonitor 應用程式與行動裝置 （iOS 或 Android） 的原生體驗。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="9ad8e-173">使用 Azure App Service Companion 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="9ad8e-174">檢閱應用程式計量</span><span class="sxs-lookup"><span data-stu-id="9ad8e-174">Review application metrics</span></span>
- <span data-ttu-id="9ad8e-175">檢閱應用程式警示和建議並採取動作</span><span class="sxs-lookup"><span data-stu-id="9ad8e-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="9ad8e-176">執行基本的疑難排解 （瀏覽、 啟動、 停止或重新啟動 hello 應用程式）</span><span class="sxs-lookup"><span data-stu-id="9ad8e-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="9ad8e-177">取得重大事件的推播通知。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-177">Get push notifications for critical events.</span></span>

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="9ad8e-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="9ad8e-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="9ad8e-180">您可以從 hello 安裝應用程式服務隨附[App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)或[Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="9ad8e-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="9ad8e-181"><a name="diagnose"></a> 步驟 4 - 診斷並解決問題</span><span class="sxs-lookup"><span data-stu-id="9ad8e-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="9ad8e-182">**診斷並解決問題**可協助您區隔出應用程式問題與平台問題。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="9ad8e-183">它也可以建議可能的補救措施 tooget 您 Web 應用程式後 toohealthy。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![診斷並解決問題](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="9ad8e-185">繼續 hello 範例表單上一個步驟，我們可以看到，hello 應用程式具有已有可用性問題。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="9ad8e-186">相反地，從 100%並未移動 hello 平台可用性。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="9ad8e-187">當 hello 應用程式發生問題而且 hello 組成的平台會保持，很清楚，我們在處理應用程式問題的指示。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="9ad8e-188"><a name="logging"></a> 步驟 5 - 記錄</span><span class="sxs-lookup"><span data-stu-id="9ad8e-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="9ad8e-189">既然我們已經縮小 hello 失敗 tooan 應用程式問題，我們來看看 hello 應用程式和伺服器記錄檔 tooget 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="9ad8e-190">記錄可讓您同時 toocollect **Application Diagnostics**和**Web Server 診斷**Web 應用程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="9ad8e-191">應用程式診斷</span><span class="sxs-lookup"><span data-stu-id="9ad8e-191">Application Diagnostics</span></span>
<span data-ttu-id="9ad8e-192">應用程式診斷可讓您 toocapture 所產生的追蹤 hello 應用程式在執行階段。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="9ad8e-193">加入追蹤 tooyour 應用程式可大幅提升您的能力 toodebug 和 pin 點的問題。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="9ad8e-194">在 ASP.NET 中，您可以記錄使用的應用程式追蹤[System.Diagnostics.Trace 類別](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)toogenerate hello 記錄基礎結構所擷取的事件。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="9ad8e-195">您也可以指定 hello 追蹤進行更容易篩選 hello 嚴重性。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="9ad8e-196">tooenable 應用程式記錄移過**監視** > **診斷記錄檔**和啟用的應用程式記錄使用 hello 切換。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="9ad8e-198">應用程式記錄檔可以是預存的 tooyour Web 應用程式的檔案系統或推入 tooblob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="9ad8e-199">生產案例中，對於建議的 toouse blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ad8e-200">啟用記錄會影響您的應用程式效能與資源使用率。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="9ad8e-201">如果是生產案例，建議使用錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="9ad8e-202">只有在調查問題時，才能啟用更詳細資料記錄。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="9ad8e-203">Web 伺服器診斷</span><span class="sxs-lookup"><span data-stu-id="9ad8e-203">Web Server Diagnostics</span></span>
<span data-ttu-id="9ad8e-204">即使未檢測您的應用程式，仍會產生 Web 伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="9ad8e-205">App Service 可以收集三種不同類型的伺服器記錄：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="9ad8e-206">**Web 伺服器記錄**</span><span class="sxs-lookup"><span data-stu-id="9ad8e-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="9ad8e-207">使用 hello HTTP 交易資訊[W3C 擴充的記錄檔格式](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="9ad8e-208">判斷整體站台的度量資訊，例如 hello 處理要求的數目或多少要求來自特定 IP 位址時很有用。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="9ad8e-209">**詳細錯誤記錄**</span><span class="sxs-lookup"><span data-stu-id="9ad8e-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="9ad8e-210">對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="9ad8e-211">深入了解詳細的錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="9ad8e-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="9ad8e-212">**失敗要求的追蹤**</span><span class="sxs-lookup"><span data-stu-id="9ad8e-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="9ad8e-213">失敗的要求，包括 hello IIS 元件的追蹤的詳細的資訊使用 tooprocess hello 要求和 hello 花費時間的每個元件。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="9ad8e-214">當嘗試 tooisolate 造成特定的 HTTP 錯誤的原因，則失敗的要求記錄檔會很有用。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="9ad8e-215">深入了解失敗的要求追蹤</span><span class="sxs-lookup"><span data-stu-id="9ad8e-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="9ad8e-216">tooenable 伺服器記錄：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-216">tooenable Server logging:</span></span>
- <span data-ttu-id="9ad8e-217">跳過**監視** > **診斷記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="9ad8e-218">啟用 hello 不同類型的 Web 伺服器診斷使用 hello 切換。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="9ad8e-220">啟用記錄會影響您的應用程式效能與資源使用率。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="9ad8e-221">如果是生產案例，建議使用錯誤記錄檔，只有在調查問題時，才能啟用更詳細資訊記錄。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="9ad8e-222">存取記錄</span><span class="sxs-lookup"><span data-stu-id="9ad8e-222">Accessing Logs</span></span>
<span data-ttu-id="9ad8e-223">使用 Azure 儲存體總管來存取 Blob 儲存體中所儲存的記錄。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="9ad8e-224">透過 FTP 存取儲存在 hello Web 應用程式的檔案系統中的記錄檔 hello 下列路徑底下：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="9ad8e-225">**應用程式記錄** - `%HOME%/LogFiles/Application/`。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="9ad8e-226">此資料夾內含有一或多個文字檔案，這些檔案涵蓋應用程式記錄所產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="9ad8e-227">**失敗的要求追蹤** - `%HOME%/LogFiles/W3SVC#########/`。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="9ad8e-228">此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="9ad8e-229">**詳細的錯誤記錄** - `%HOME%/LogFiles/DetailedErrors/`。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="9ad8e-230">此資料夾包含一或多個 .htm 檔案，以及關於您應用程式所產生之 HTTP 錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="9ad8e-231">**Web 伺服器記錄** - `%HOME%/LogFiles/http/RawLogs`。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="9ad8e-232">此資料夾包含一個或多個使用 hello W3C 擴充的記錄檔格式來格式化的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="9ad8e-233"><a name="streaming"></a> 步驟 6 - 記錄資料流</span><span class="sxs-lookup"><span data-stu-id="9ad8e-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="9ad8e-234">偵錯應用程式，因為它會將儲存時間太相比時，資料流記錄會很方便[存取 hello 記錄](#Accessing-Logs)透過 FTP。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="9ad8e-235">App Service 可以在產生**應用程式記錄**和 **Web 伺服器記錄**時對它們進行資料流處理。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="9ad8e-236">然後再嘗試 toostream 記錄檔，請確定您已啟用收集記錄檔，hello 中所述[記錄](#logging)> 一節。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="9ad8e-237">toostream 記錄移過**監視**> **記錄檔資料流**。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="9ad8e-238">根據您要尋找的是何種資訊來選取 [應用程式記錄] 或 [Web 伺服器記錄]。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="9ad8e-239">從這裡，您也可以暫停、 重新啟動，並清除 hello 緩衝區。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![串流記錄](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="9ad8e-241">Hello 應用程式上沒有流量時，才會產生記錄檔，您也可以增加記錄檔 tooget hello 詳細資訊，多個事件或資訊。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="9ad8e-242"><a name="remote"></a> 步驟 7 - 遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="9ad8e-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="9ad8e-243">Pin 碼指向 hello hello 應用程式的問題來源之後，使用**遠端偵錯**toowalk 透過 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="9ad8e-244">遠端偵錯可讓您將連接 Web 應用程式的偵錯工具 tooyour hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="9ad8e-245">您可以設定中斷點、 直接管理記憶體、 逐步執行程式碼，和甚至變更 hello 就像在本機執行的應用程式的程式碼路徑。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="9ad8e-246">tooattach hello 偵錯工具 tooyour 應用程式 hello 雲端中執行：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="9ad8e-247">使用 Visual Studio 2017，hello 應用程式的開啟 hello 方案想 toodebug</span><span class="sxs-lookup"><span data-stu-id="9ad8e-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="9ad8e-248">設定一些中斷點，就像您針對本機開發所做的。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="9ad8e-249">開啟 [Cloud Explorer] \(ctr + /，ctrl + x)。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="9ad8e-250">視需要利用您的 Azure 認證登入。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="9ad8e-251">尋找您想要 toodebug 的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="9ad8e-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="9ad8e-252">選取**附加偵錯工具**表單 hello**動作**窗格。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![遠端偵錯](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="9ad8e-254">Visual Studio 設定遠端偵錯您應用程式，並啟動瀏覽器視窗瀏覽 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="9ad8e-255">瀏覽您的應用程式 tootrigger 中斷點和逐步執行 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="9ad8e-256">不建議在生產環境中執行偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="9ad8e-257">如果您的生產環境應用程式未向外延展 toomultiple 伺服器執行個體中，偵錯防止 hello 回應 tooother 要求 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="9ad8e-258">如需疑難排解生產環境的問題，您的最佳資源太[設定記錄](#logging)和[Application Insights](#insights)。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="9ad8e-259"><a name="explorer"></a> 步驟 8 - 處理序總管</span><span class="sxs-lookup"><span data-stu-id="9ad8e-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="9ad8e-260">當您的應用程式會向外延展比一個執行個體，toomore**處理序總管**可協助您識別執行個體的特定問題。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="9ad8e-261">使用**處理序總管**來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9ad8e-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="9ad8e-262">列舉所有 hello 處理程序跨應用程式服務方案的不同執行個體。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="9ad8e-263">向下鑽研，並檢視 hello 控點，每個處理序相關聯的模組。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="9ad8e-264">檢視 CPU、 工作集和執行緒計數在 hello 處理層級 toohelp 識別失控處理程序</span><span class="sxs-lookup"><span data-stu-id="9ad8e-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="9ad8e-265">尋找開啟檔案控制代碼，甚至終止特定的處理序執行個體。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="9ad8e-266">可在 [監視] > [處理序總管] 下方找到處理序總管。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![處理序總管](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="9ad8e-268"><a name="insights"></a> 步驟 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="9ad8e-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="9ad8e-269">**Application Insights** 可為您的應用程式提供應用程式分析和進階監視功能。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="9ad8e-270">使用 Application Insights toodetect 和診斷例外狀況和 Web 應用程式中的效能問題。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="9ad8e-271">您可以在 [監視] > [Application Insights] 下方，針對 Web 應用程式啟用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="9ad8e-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="9ad8e-272">Application Insights 可能會提示您 tooinstall hello Application Insights 站台擴充 toostart 收集資料。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="9ad8e-273">安裝 hello 的網站擴充功能會導致應用程式重新啟動。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="9ad8e-275">Application Insights 有豐富的功能設定，toolearn 詳細資訊，請依照下列包含在 hello hello 連結[接下來的步驟](#next)> 一節。</span><span class="sxs-lookup"><span data-stu-id="9ad8e-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="9ad8e-276"><a name="next"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ad8e-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="9ad8e-277">什麼是 Application Insights</span><span class="sxs-lookup"><span data-stu-id="9ad8e-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="9ad8e-278">使用 Application Insights 監視 Azure Web 應用程式效能</span><span class="sxs-lookup"><span data-stu-id="9ad8e-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="9ad8e-279">使用 Application Insights 監視任何網站的可用性和回應性</span><span class="sxs-lookup"><span data-stu-id="9ad8e-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
