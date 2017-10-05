---
title: "監視 Web 應用程式 | Microsoft Docs"
description: "了解如何在 Web 應用程式上設定監視"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="fcfd7-103">監視 App Service</span><span class="sxs-lookup"><span data-stu-id="fcfd7-103">Monitor App Service</span></span>
<span data-ttu-id="fcfd7-104">本教學課程將逐步引導您監視您的應用程式，並使用內建的平台工具來解決所發生的問題。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="fcfd7-105">這份文件的每個章節都會復習特定的功能。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="fcfd7-106">將功能一起使用可讓您︰</span><span class="sxs-lookup"><span data-stu-id="fcfd7-106">Using the features together let you:</span></span>
- <span data-ttu-id="fcfd7-107">識別應用程式中的問題。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="fcfd7-108">當您的程式碼或平台引起問題時進行判斷。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="fcfd7-109">縮小程式碼中的問題來源。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="fcfd7-110">偵錯和修正問題。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fcfd7-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="fcfd7-111">Before you begin</span></span>
- <span data-ttu-id="fcfd7-112">您必須有要監視的 Web 應用程式，並遵循概略的步驟。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="fcfd7-113">您可以遵循[在 Azure 中搭配 SQL Database 建立 ASP.NET 應用程式](app-service-web-tutorial-dotnet-sqldatabase.md)教學課程中所述的步驟來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="fcfd7-114">如果您想要試著進行應用程式的**遠端偵錯**，則您需要 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="fcfd7-115">如果尚未安裝 Visual Studio 2017，您可以下載並使用免費的 [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="fcfd7-116">務必在 Visual Studio 設定期間啟用 **Azure 開發**。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="fcfd7-117"><a name="metrics"></a> 步驟 1 - 檢視計量</span><span class="sxs-lookup"><span data-stu-id="fcfd7-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="fcfd7-118">**計量**有助於您了解︰</span><span class="sxs-lookup"><span data-stu-id="fcfd7-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="fcfd7-119">應用程式健全狀況</span><span class="sxs-lookup"><span data-stu-id="fcfd7-119">Application health</span></span>
- <span data-ttu-id="fcfd7-120">應用程式效能</span><span class="sxs-lookup"><span data-stu-id="fcfd7-120">App performance</span></span>
- <span data-ttu-id="fcfd7-121">資源耗用量</span><span class="sxs-lookup"><span data-stu-id="fcfd7-121">Resource consumption</span></span>

<span data-ttu-id="fcfd7-122">調查應用程式問題時，檢閱計量是不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="fcfd7-123">Azure 入口網站有一種快速方式，可使用 **Azure 監視器**，以視覺化方式檢查應用程式的計量。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="fcfd7-124">計量會提供應用程式之數個金鑰彙總的歷程記錄檢視。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="fcfd7-125">您應該針對 App Service 中裝載的任何應用程式，監視 Web 應用程式和 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="fcfd7-126">App Service 方案代表用來裝載應用程式的實體資源集合。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="fcfd7-127">所有指派給 App Service 方案的所有應用程式都會共用它所定義的資源，而讓您節省裝載多個應用程式時的成本。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="fcfd7-128">App Service 方案可定義：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-128">App Service plans define:</span></span>
> * <span data-ttu-id="fcfd7-129">區域：北歐、美國東部、東南亞等。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="fcfd7-130">執行個體大小：小型、中型、大型等。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="fcfd7-131">級別計數：一、二或三個執行個體等。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="fcfd7-132">SKU：免費、共用、基本、標準、進階等。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="fcfd7-133">若要檢視 Web 應用程式的計量，請移至您想要監視之應用程式的 [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="fcfd7-134">從這裡開始，您能以**監視圖格**的形式檢視應用程式計量的圖表。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="fcfd7-135">按一下圖格，以編輯和設定要檢視的計量和要顯示的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="fcfd7-136">根據預設，資源刀鋒視窗提供了應用程式要求的檢視和最後一個小時的錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="fcfd7-137">![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="fcfd7-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="fcfd7-138">如您在範例中所見，我們有一個應用程式產生了許多 **HTTP 伺服器錯誤**。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="fcfd7-139">大量的錯誤是我們要調查此應用程式的第一個徵兆。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="fcfd7-140">透過下列連結深入了解 Azure 監視器：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="fcfd7-141">開始使用 Azure 監視器</span><span class="sxs-lookup"><span data-stu-id="fcfd7-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="fcfd7-142">Azure 計量</span><span class="sxs-lookup"><span data-stu-id="fcfd7-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="fcfd7-143">支援 Azure 監視器的計量</span><span class="sxs-lookup"><span data-stu-id="fcfd7-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="fcfd7-144">Azure 儀表板</span><span class="sxs-lookup"><span data-stu-id="fcfd7-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="fcfd7-145"><a name="alerts"></a> 步驟 2 - 設定警示</span><span class="sxs-lookup"><span data-stu-id="fcfd7-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="fcfd7-146">**警示**可以設定成在您的應用程式發生特定條件時進行觸發。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="fcfd7-147">在[步驟 1 - 檢視計量](#metrics)中，我們看到應用程式有大量的錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="fcfd7-148">讓我們將警示設定為發生錯誤時會自動取得通知。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="fcfd7-149">在此情況下，我們希望每次 HTTP 50 X 錯誤數目超過某個臨界值時，警示會傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="fcfd7-150">若要建立警示，請瀏覽至 [監視] > [警示]，然後按一下 [+ 新增警示]。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Alerts](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="fcfd7-152">提供警示設定的值︰</span><span class="sxs-lookup"><span data-stu-id="fcfd7-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="fcfd7-153">**資源︰**使用警示來監視的網站。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="fcfd7-154">**名稱︰**您警示的名稱，在此案例中為︰高 HTTP 50X。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="fcfd7-155">**描述︰**這項警示所查看的純文字說明。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="fcfd7-156">**警示項目︰**警示可以查看計量或事件，此範例中，我們要查看計量。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="fcfd7-157">**計量︰**要監視的計量，在此情況下︰HTTP 伺服器錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="fcfd7-158">**條件︰**發出警示的時機，在此情況下，選取大於選項。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="fcfd7-159">**臨界值︰**所要尋找的值，在此情況下︰400。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="fcfd7-160">**期間︰**警示在計量的平均值期間運作。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="fcfd7-161">較短的時間會造成警示較敏感。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="fcfd7-162">在此情況下，我們看看 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="fcfd7-163">**電子郵件擁有者和參與者︰**在此情況下︰已啟用。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="fcfd7-164">現在已建立警示，每次應用程式超過設定的閾值時，就會傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="fcfd7-165">也可以在 Azure 入口網站中檢閱作用中警示。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![觸發的警示](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="fcfd7-167">透過下列連結深入了解 Azure 警示：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="fcfd7-168">Microsoft Azure 中的警示是什麼</span><span class="sxs-lookup"><span data-stu-id="fcfd7-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="fcfd7-169">對計量採取動作</span><span class="sxs-lookup"><span data-stu-id="fcfd7-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="fcfd7-170">建立計量警示</span><span class="sxs-lookup"><span data-stu-id="fcfd7-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="fcfd7-171"><a name="companion"></a> 步驟 3 - App Service Companion</span><span class="sxs-lookup"><span data-stu-id="fcfd7-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="fcfd7-172">**App Service Companion** 提供一種便利的方式，利用行動裝置 (iOS 或 Android) 中的原生體驗來監視您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="fcfd7-173">使用 Azure App Service Companion 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="fcfd7-174">檢閱應用程式計量</span><span class="sxs-lookup"><span data-stu-id="fcfd7-174">Review application metrics</span></span>
- <span data-ttu-id="fcfd7-175">檢閱應用程式警示和建議並採取動作</span><span class="sxs-lookup"><span data-stu-id="fcfd7-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="fcfd7-176">執行基本疑難排解 (瀏覽、啟動、停止、重新啟動應用程式)</span><span class="sxs-lookup"><span data-stu-id="fcfd7-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="fcfd7-177">取得重大事件的推播通知。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-177">Get push notifications for critical events.</span></span>

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="fcfd7-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="fcfd7-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="fcfd7-180">您可以從 [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) 或 [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps) 安裝 App Service Companion</span><span class="sxs-lookup"><span data-stu-id="fcfd7-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="fcfd7-181"><a name="diagnose"></a> 步驟 4 - 診斷並解決問題</span><span class="sxs-lookup"><span data-stu-id="fcfd7-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="fcfd7-182">**診斷並解決問題**可協助您區隔出應用程式問題與平台問題。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="fcfd7-183">它也可以建議可能的補救措施，讓您的 Web 應用程式回到良好的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![診斷並解決問題](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="fcfd7-185">繼續上一個步驟的範例，我們可以看到應用程式不斷發生可用性問題。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="fcfd7-186">相反地，平台可用性並未低於 100%。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="fcfd7-187">當應用程式發生問題而平台持續運作時，我們很清楚知道，需要處理的是應用程式問題。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="fcfd7-188"><a name="logging"></a> 步驟 5 - 記錄</span><span class="sxs-lookup"><span data-stu-id="fcfd7-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="fcfd7-189">現在我們已將失敗範圍縮小到應用程式問題，我們可以查看應用程式和伺服器記錄來取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="fcfd7-190">記錄功能可讓您同時收集 Web 應用程式的**應用程式診斷**和 **Web 伺服器診斷**記錄。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="fcfd7-191">應用程式診斷</span><span class="sxs-lookup"><span data-stu-id="fcfd7-191">Application Diagnostics</span></span>
<span data-ttu-id="fcfd7-192">應用程式診斷功能可讓您擷取應用程式在執行階段所產生的追蹤。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="fcfd7-193">將追蹤新增至您的應用程式，可大幅提升您的偵錯和固定點問題能力。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="fcfd7-194">在 ASP.NET 中，您可以使用 [System.Diagnostics.Trace 類別](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx)來記錄應用程式追蹤，以產生由記錄基礎結構所擷取的事件。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="fcfd7-195">您也可以指定追蹤的嚴重性，讓篩選變得更簡單。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-195">You can also specify the severity of the trace for easier filtering.</span></span>

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
<span data-ttu-id="fcfd7-196">若要啟用應用程式記錄功能，請移至 [監視] > [診斷記錄]，並使用切換來啟用應用程式記錄。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="fcfd7-198">應用程式記錄可以儲存至 Web 應用程式的檔案系統或推送至 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="fcfd7-199">如果是生產案例，建議使用 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcfd7-200">啟用記錄會影響您的應用程式效能與資源使用率。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="fcfd7-201">如果是生產案例，建議使用錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="fcfd7-202">只有在調查問題時，才能啟用更詳細資料記錄。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="fcfd7-203">Web 伺服器診斷</span><span class="sxs-lookup"><span data-stu-id="fcfd7-203">Web Server Diagnostics</span></span>
<span data-ttu-id="fcfd7-204">即使未檢測您的應用程式，仍會產生 Web 伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="fcfd7-205">App Service 可以收集三種不同類型的伺服器記錄：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="fcfd7-206">**Web 伺服器記錄**</span><span class="sxs-lookup"><span data-stu-id="fcfd7-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="fcfd7-207">使用 [W3C 擴充記錄檔格式 (英文)](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx) 的 HTTP 交易相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="fcfd7-208">當您需要判斷整體網站計量 (例如，處理的要求數量，或者有多少要求來自特定的 IP 位址) 時，非常實用。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="fcfd7-209">**詳細錯誤記錄**</span><span class="sxs-lookup"><span data-stu-id="fcfd7-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="fcfd7-210">對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="fcfd7-211">深入了解詳細的錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="fcfd7-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="fcfd7-212">**失敗要求的追蹤**</span><span class="sxs-lookup"><span data-stu-id="fcfd7-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="fcfd7-213">關於失敗要求的詳細資訊，包括用於處理要求的 IIS 元件追蹤，以及每個元件所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="fcfd7-214">在嘗試隔離導致特定 HTTP 錯誤的項目時，失敗的要求記錄就非常實用。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="fcfd7-215">深入了解失敗的要求追蹤</span><span class="sxs-lookup"><span data-stu-id="fcfd7-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="fcfd7-216">啟用伺服器記錄：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-216">To enable Server logging:</span></span>
- <span data-ttu-id="fcfd7-217">移至 [監視] > [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="fcfd7-218">使用切換來啟用不同類型的 Web 伺服器診斷。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![監視應用程式](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="fcfd7-220">啟用記錄會影響您的應用程式效能與資源使用率。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="fcfd7-221">如果是生產案例，建議使用錯誤記錄檔，只有在調查問題時，才能啟用更詳細資訊記錄。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="fcfd7-222">存取記錄</span><span class="sxs-lookup"><span data-stu-id="fcfd7-222">Accessing Logs</span></span>
<span data-ttu-id="fcfd7-223">使用 Azure 儲存體總管來存取 Blob 儲存體中所儲存的記錄。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="fcfd7-224">在下列路徑中，透過 FTP 存取儲存於 Web 應用程式檔案系統中的記錄：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="fcfd7-225">**應用程式記錄** - `%HOME%/LogFiles/Application/`。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="fcfd7-226">此資料夾內含有一或多個文字檔案，這些檔案涵蓋應用程式記錄所產生的資訊。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="fcfd7-227">**失敗的要求追蹤** - `%HOME%/LogFiles/W3SVC#########/`。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="fcfd7-228">此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="fcfd7-229">**詳細的錯誤記錄** - `%HOME%/LogFiles/DetailedErrors/`。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="fcfd7-230">此資料夾包含一或多個 .htm 檔案，以及關於您應用程式所產生之 HTTP 錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="fcfd7-231">**Web 伺服器記錄** - `%HOME%/LogFiles/http/RawLogs`。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="fcfd7-232">此資料夾包含一或多個運用 W3C 擴充記錄檔格式來格式化的文字檔。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="fcfd7-233"><a name="streaming"></a> 步驟 6 - 記錄資料流</span><span class="sxs-lookup"><span data-stu-id="fcfd7-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="fcfd7-234">資料流記錄在偵錯應用程式時非常便利，因為相較於透過 FTP 來[存取記錄](#Accessing-Logs)，這種方法比較節省時間。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="fcfd7-235">App Service 可以在產生**應用程式記錄**和 **Web 伺服器記錄**時對它們進行資料流處理。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="fcfd7-236">在嘗試資料流處理記錄時，請確定您已啟用收集記錄，如[記錄](#logging)一節中所述。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="fcfd7-237">若要串流記錄，移至 [監視]> [記錄資料流]。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="fcfd7-238">根據您要尋找的是何種資訊來選取 [應用程式記錄] 或 [Web 伺服器記錄]。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="fcfd7-239">從這裡開始，您也可以暫停、重新啟動，然後清除緩衝區。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![串流記錄](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="fcfd7-241">只有應用程式上有流量時，才會產生記錄，您也可以增加記錄的詳細資訊，以取得更多的事件或資訊。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="fcfd7-242"><a name="remote"></a> 步驟 7 - 遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="fcfd7-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="fcfd7-243">一旦您確定應用程式問題的來源後，請使用**遠端偵錯**來逐步執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="fcfd7-244">遠端偵錯可讓您將偵錯工具附加至在雲端中執行的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="fcfd7-245">您可以設定中斷點、直接操作記憶體、逐步執行程式碼，甚至變更程式碼路徑，就像您針對在本機執行的應用程式所做的。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="fcfd7-246">將偵錯工具附加至您在雲端中執行的應用程式：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="fcfd7-247">使用 Visual Studio 2017，開啟您要偵錯之應用程式的方案</span><span class="sxs-lookup"><span data-stu-id="fcfd7-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="fcfd7-248">設定一些中斷點，就像您針對本機開發所做的。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="fcfd7-249">開啟 [Cloud Explorer] \(ctr + /，ctrl + x)。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="fcfd7-250">視需要利用您的 Azure 認證登入。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="fcfd7-251">尋找您要偵錯的應用程式</span><span class="sxs-lookup"><span data-stu-id="fcfd7-251">Find the app you want to debug</span></span>
- <span data-ttu-id="fcfd7-252">從 [動作] 窗格選取 [附加偵錯工具]。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![遠端偵錯](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="fcfd7-254">Visual Studio 會設定您的應用程式以進行遠端偵錯，並啟動瀏覽器視窗，瀏覽至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="fcfd7-255">完整瀏覽您的應用程式，以觸發中斷點並逐步執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="fcfd7-256">不建議在生產環境中執行偵錯模式。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="fcfd7-257">如果您的生產應用程式並未調升規模到多個伺服器執行個體，偵錯就會防止 Web 伺服器回應其他要求。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="fcfd7-258">如需進行生產環境問題的疑難排解，您的最佳資源是[設定記錄](#logging)和 [Application Insights](#insights)。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="fcfd7-259"><a name="explorer"></a> 步驟 8 - 處理序總管</span><span class="sxs-lookup"><span data-stu-id="fcfd7-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="fcfd7-260">當您的應用程式相應放大至多個執行個體時，**處理序總管**可協助您識別執行個體特定的問題。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="fcfd7-261">使用**處理序總管**來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="fcfd7-262">列舉 App Service 方案的不同執行個體上的所有處理序。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="fcfd7-263">向下切入並檢視與每個處理序相關聯的控制代碼和模組。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="fcfd7-264">檢視處理序層級上的 CPU、工作集和執行緒計數，以協助您識別失控的處理序</span><span class="sxs-lookup"><span data-stu-id="fcfd7-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="fcfd7-265">尋找開啟檔案控制代碼，甚至終止特定的處理序執行個體。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="fcfd7-266">可在 [監視] > [處理序總管] 下方找到處理序總管。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![處理序總管](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="fcfd7-268"><a name="insights"></a> 步驟 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="fcfd7-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="fcfd7-269">**Application Insights** 可為您的應用程式提供應用程式分析和進階監視功能。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="fcfd7-270">請使用 Application Insights 來偵測並診斷例外狀況，以及 Web 應用程式中的效能問題。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="fcfd7-271">您可以在 [監視] > [Application Insights] 下方，針對 Web 應用程式啟用 Application Insights</span><span class="sxs-lookup"><span data-stu-id="fcfd7-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="fcfd7-272">Application Insights 可能會提示您安裝 Application Insights 網站延伸模組，以開始收集資料。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="fcfd7-273">安裝網站延伸模組會導致應用程式重新啟動。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="fcfd7-275">Application Insights 具有豐富的功能集，若要深入了解，請遵循[後續步驟](#next)一節中所含的連結。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="fcfd7-276"><a name="next"></a> 後續步驟</span><span class="sxs-lookup"><span data-stu-id="fcfd7-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="fcfd7-277">什麼是 Application Insights</span><span class="sxs-lookup"><span data-stu-id="fcfd7-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="fcfd7-278">使用 Application Insights 監視 Azure Web 應用程式效能</span><span class="sxs-lookup"><span data-stu-id="fcfd7-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="fcfd7-279">使用 Application Insights 監視任何網站的可用性和回應性</span><span class="sxs-lookup"><span data-stu-id="fcfd7-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
