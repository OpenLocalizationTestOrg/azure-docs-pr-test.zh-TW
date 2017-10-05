---
title: "使用 Azure Application Insights 監視即時 ASP.NET Web 應用程式 | Microsoft Docs"
description: "監視網站的效能而不重新部署網站。 使用裝載於內部部署、VM 中或 Azure 上的 ASP.NET Web 應用程式。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d07a0c81f89100c378456bbea8dca1c009cc8d77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="55b9a-104">在執行階段使用 Application Insights 檢測 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="55b9a-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="55b9a-105">您可以使用 Azure Application Insights 檢測即時 Web 應用程式，而不需修改或重新部署您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="55b9a-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span></span> <span data-ttu-id="55b9a-106">如果您的應用程式是由內部部署 IIS 伺服器裝載，請安裝狀態監視器。</span><span class="sxs-lookup"><span data-stu-id="55b9a-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="55b9a-107">如果這些是 Azure Web 應用程式或在 Azure VM 中執行，您可以從 Azure 控制台切換為 Application Insights 監視。</span><span class="sxs-lookup"><span data-stu-id="55b9a-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span></span> <span data-ttu-id="55b9a-108">(我們還提供有關檢測[即時 J2EE Web 應用程式](app-insights-java-live.md)和 [Azure 雲端服務](app-insights-cloudservices.md)的個別文章)。您需要 [Microsoft Azure](http://azure.com) 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="55b9a-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![範例圖表](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="55b9a-110">下列三種途徑均可讓您將 Application Insights 套用至 .NET Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="55b9a-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span></span>

* <span data-ttu-id="55b9a-111">**建置階段：**[新增 Application Insights SDK][greenbrown] 至您的 Web 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="55b9a-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span></span>
* <span data-ttu-id="55b9a-112">**執行階段︰** 如下所述，檢測伺服器上的 Web 應用程式，而不需重建並重新部署程式碼。</span><span class="sxs-lookup"><span data-stu-id="55b9a-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span></span>
* <span data-ttu-id="55b9a-113">**兩者︰** 將 SDK 建置到您的 Web 應用程式程式碼中，同時套用執行階段延伸模組。</span><span class="sxs-lookup"><span data-stu-id="55b9a-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span></span> <span data-ttu-id="55b9a-114">集合兩者之優點。</span><span class="sxs-lookup"><span data-stu-id="55b9a-114">Get the best of both options.</span></span>

<span data-ttu-id="55b9a-115">以下是您可在每種途徑中取得的優勢摘要︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="55b9a-116">建置階段</span><span class="sxs-lookup"><span data-stu-id="55b9a-116">Build time</span></span> | <span data-ttu-id="55b9a-117">執行階段</span><span class="sxs-lookup"><span data-stu-id="55b9a-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="55b9a-118">要求和例外狀況</span><span class="sxs-lookup"><span data-stu-id="55b9a-118">Requests & exceptions</span></span> |<span data-ttu-id="55b9a-119">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-119">Yes</span></span> |<span data-ttu-id="55b9a-120">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-120">Yes</span></span> |
| [<span data-ttu-id="55b9a-121">更詳細的例外狀況</span><span class="sxs-lookup"><span data-stu-id="55b9a-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="55b9a-122">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-122">Yes</span></span> |
| [<span data-ttu-id="55b9a-123">相依性診斷</span><span class="sxs-lookup"><span data-stu-id="55b9a-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="55b9a-124">在 .Net 4.6 + 上，但較少細節</span><span class="sxs-lookup"><span data-stu-id="55b9a-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="55b9a-125">是，完整詳細資料︰結果碼、SQL 命令文字、HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="55b9a-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="55b9a-126">系統效能計數器</span><span class="sxs-lookup"><span data-stu-id="55b9a-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="55b9a-127">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-127">Yes</span></span> |<span data-ttu-id="55b9a-128">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-128">Yes</span></span> |
| <span data-ttu-id="55b9a-129">[自訂遙測的 API][api]</span><span class="sxs-lookup"><span data-stu-id="55b9a-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="55b9a-130">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-130">Yes</span></span> |<span data-ttu-id="55b9a-131">否</span><span class="sxs-lookup"><span data-stu-id="55b9a-131">No</span></span> |
| [<span data-ttu-id="55b9a-132">追蹤記錄檔整合</span><span class="sxs-lookup"><span data-stu-id="55b9a-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="55b9a-133">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-133">Yes</span></span> |<span data-ttu-id="55b9a-134">否</span><span class="sxs-lookup"><span data-stu-id="55b9a-134">No</span></span> |
| [<span data-ttu-id="55b9a-135">頁面檢視和使用者資料</span><span class="sxs-lookup"><span data-stu-id="55b9a-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="55b9a-136">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-136">Yes</span></span> |<span data-ttu-id="55b9a-137">否</span><span class="sxs-lookup"><span data-stu-id="55b9a-137">No</span></span> |
| <span data-ttu-id="55b9a-138">需要重新建置程式碼</span><span class="sxs-lookup"><span data-stu-id="55b9a-138">Need to rebuild code</span></span> |<span data-ttu-id="55b9a-139">是</span><span class="sxs-lookup"><span data-stu-id="55b9a-139">Yes</span></span> | <span data-ttu-id="55b9a-140">否</span><span class="sxs-lookup"><span data-stu-id="55b9a-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="55b9a-141">監視即時 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="55b9a-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="55b9a-142">如果您的應用程式是以 Azure Web 服務的形式執行，以下是如何開始監視的方法︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-142">If your application is running as an Azure web service, here's how to switch on monitoring:</span></span>

* <span data-ttu-id="55b9a-143">在 Azure 中於應用程式控制台選取 [Application Insights]。</span><span class="sxs-lookup"><span data-stu-id="55b9a-143">Select Application Insights on the app's control panel in Azure.</span></span>

    ![針對 Azure Web 應用程式設定 Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="55b9a-145">當 [Application Insights 摘要] 頁面開啟時，按一下頁面底部的連結以開啟完整的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="55b9a-145">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span></span>

    ![點選 Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="55b9a-147">[監視雲端和 VM 應用程式](app-insights-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="55b9a-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="55b9a-148">在 Azure 中啟用用戶端監視</span><span class="sxs-lookup"><span data-stu-id="55b9a-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="55b9a-149">如果您已在 Azure 中啟用 Application Insights，即可新增頁面檢視和使用者遙測。</span><span class="sxs-lookup"><span data-stu-id="55b9a-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="55b9a-150">選取 [設定] > [應用程式設定]</span><span class="sxs-lookup"><span data-stu-id="55b9a-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="55b9a-151">在 [應用程式設定] 之下，新增索引鍵值組︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="55b9a-152">索引鍵︰`APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="55b9a-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="55b9a-153">值: `true`</span><span class="sxs-lookup"><span data-stu-id="55b9a-153">Value: `true`</span></span>
3. <span data-ttu-id="55b9a-154">**儲存**設定並**重新啟動**您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-154">**Save** the settings and **Restart** your app.</span></span>

<span data-ttu-id="55b9a-155">Application Insights JavaScript SDK 現在已插入每個網頁中。</span><span class="sxs-lookup"><span data-stu-id="55b9a-155">The Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="55b9a-156">監視即時 IIS Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="55b9a-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="55b9a-157">如果您的應用程式裝載於 IIS 伺服器上，請使用狀態監視器來啟用 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="55b9a-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="55b9a-158">在 IIS Web 伺服器上，以系統管理員認證登入。</span><span class="sxs-lookup"><span data-stu-id="55b9a-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="55b9a-159">如果尚未安裝 Application Insights 狀態監視器，請下載並執行[狀態監視器安裝程式](http://go.microsoft.com/fwlink/?LinkId=506648) (或執行 [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) 並在其中搜尋 Application Insights 狀態監視器)。</span><span class="sxs-lookup"><span data-stu-id="55b9a-159">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="55b9a-160">在狀態監視器中，選取您想要監視的已安裝 Web 應用程式或網站。</span><span class="sxs-lookup"><span data-stu-id="55b9a-160">In Status Monitor, select the installed web application or website that you want to monitor.</span></span> <span data-ttu-id="55b9a-161">利用您的 Azure 認證登入。</span><span class="sxs-lookup"><span data-stu-id="55b9a-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="55b9a-162">在 Application Insights 入口網站中設定您要在其中檢視結果的資源。</span><span class="sxs-lookup"><span data-stu-id="55b9a-162">Configure the resource where you want to see the results in the Application Insights portal.</span></span> <span data-ttu-id="55b9a-163">(通常最好建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="55b9a-163">(Normally, it's best to create a new resource.</span></span> <span data-ttu-id="55b9a-164">如果您已經為此應用程式設定 [Web 測試][availability]或[用戶端監視][client]，請選取現有的資源。)</span><span class="sxs-lookup"><span data-stu-id="55b9a-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![選擇應用程式和資源。](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="55b9a-166">重新啟動 IIS。</span><span class="sxs-lookup"><span data-stu-id="55b9a-166">Restart IIS.</span></span>

    ![選擇對話方塊頂端的 [重新啟動]。](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="55b9a-168">您的 Web 服務會中斷一小段時間。</span><span class="sxs-lookup"><span data-stu-id="55b9a-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="55b9a-169">自訂監視選項</span><span class="sxs-lookup"><span data-stu-id="55b9a-169">Customize monitoring options</span></span>

<span data-ttu-id="55b9a-170">啟用 Application Insights 可將 DLL 和 ApplicationInsights.config 新增至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-170">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span></span> <span data-ttu-id="55b9a-171">您可以[編輯 .config 檔案](app-insights-configuration-with-applicationinsights-config.md)﹐以變更某些選項。</span><span class="sxs-lookup"><span data-stu-id="55b9a-171">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="55b9a-172">當您重新發佈您的應用程式時，請重新啟用 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="55b9a-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="55b9a-173">重新發佈您的應用程式之前，請考慮[將 Application Insights 新增至 Visual Studio 中的程式碼][greenbrown]。</span><span class="sxs-lookup"><span data-stu-id="55b9a-173">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="55b9a-174">您將取得更詳細的遙測，並且能夠撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="55b9a-174">You'll get more detailed telemetry and the ability to write custom telemetry.</span></span>

<span data-ttu-id="55b9a-175">如果您想要重新發行，但不將 Application Insights 新增至程式碼，請留意部署程序可能會從已發佈的網站中刪除 DLL 和 ApplicationInsights.config。</span><span class="sxs-lookup"><span data-stu-id="55b9a-175">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span></span> <span data-ttu-id="55b9a-176">因此：</span><span class="sxs-lookup"><span data-stu-id="55b9a-176">Therefore:</span></span>

1. <span data-ttu-id="55b9a-177">如果您已編輯 ApplicationInsights.config，請在重新發佈應用程式前複製一份。</span><span class="sxs-lookup"><span data-stu-id="55b9a-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="55b9a-178">重新發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-178">Republish your app.</span></span>
3. <span data-ttu-id="55b9a-179">重新啟用 Application Insights 監視功能。</span><span class="sxs-lookup"><span data-stu-id="55b9a-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="55b9a-180">(使用適當的方法︰Azure Web 應用程式控制台或 IIS 主機上的狀態監視器。)</span><span class="sxs-lookup"><span data-stu-id="55b9a-180">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="55b9a-181">恢復您在 .config 檔案上執行的所有編輯。</span><span class="sxs-lookup"><span data-stu-id="55b9a-181">Reinstate any edits you performed on the .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="55b9a-182">針對 Application Insights 的執行階段組態進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="55b9a-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="55b9a-183">無法連接？</span><span class="sxs-lookup"><span data-stu-id="55b9a-183">Can't connect?</span></span> <span data-ttu-id="55b9a-184">沒有遙測資料？</span><span class="sxs-lookup"><span data-stu-id="55b9a-184">No telemetry?</span></span>

* <span data-ttu-id="55b9a-185">在伺服器的防火牆中開啟[必要的傳出連接埠](app-insights-ip-addresses.md#outgoing-ports)，以允許狀態監視器運作。</span><span class="sxs-lookup"><span data-stu-id="55b9a-185">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span></span>

* <span data-ttu-id="55b9a-186">開啟狀態監視器，然後選取左窗格中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="55b9a-187">檢查 [設定通知] 區段中是否有任何關於此應用程式的診斷訊息：</span><span class="sxs-lookup"><span data-stu-id="55b9a-187">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span></span>

  ![開啟 [效能] 刀鋒視窗，即可查看要求、回應時間、相依性和其他資料](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="55b9a-189">如果您在伺服器上看到有關「權限不足」的訊息，請嘗試下列操作：</span><span class="sxs-lookup"><span data-stu-id="55b9a-189">On the server, if you see a message about "insufficient permissions", try the following:</span></span>
  * <span data-ttu-id="55b9a-190">在 IIS 管理員中，選取應用程式集區，開啟 [進階設定]，並記下 [處理序模型] 下的身分識別。</span><span class="sxs-lookup"><span data-stu-id="55b9a-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span></span>
  * <span data-ttu-id="55b9a-191">在電腦的管理控制台中，將此身分識別加入至效能監試器使用者群組。</span><span class="sxs-lookup"><span data-stu-id="55b9a-191">In Computer management control panel, add this identity to the Performance Monitor Users group.</span></span>
* <span data-ttu-id="55b9a-192">如果您的伺服器上已安裝 MMA/SCOM (Microsoft Operations Management Suite)，某些版本可能會發生衝突。</span><span class="sxs-lookup"><span data-stu-id="55b9a-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="55b9a-193">解除安裝 SCOM 和狀態監視器，重新安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="55b9a-193">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span></span>
* <span data-ttu-id="55b9a-194">請參閱[疑難排解][qna]。</span><span class="sxs-lookup"><span data-stu-id="55b9a-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="55b9a-195">系統需求</span><span class="sxs-lookup"><span data-stu-id="55b9a-195">System Requirements</span></span>
<span data-ttu-id="55b9a-196">支援伺服器上 Application Insights 狀態監視器的作業系統：</span><span class="sxs-lookup"><span data-stu-id="55b9a-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="55b9a-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="55b9a-197">Windows Server 2008</span></span>
* <span data-ttu-id="55b9a-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="55b9a-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="55b9a-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="55b9a-199">Windows Server 2012</span></span>
* <span data-ttu-id="55b9a-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="55b9a-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="55b9a-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="55b9a-201">Windows Server 2016</span></span>

<span data-ttu-id="55b9a-202">(含最新版 SP 和 .NET Framework 4.5)</span><span class="sxs-lookup"><span data-stu-id="55b9a-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="55b9a-203">在用戶端 Windows 7、8、8.1 和 10 上，一樣需含有 .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="55b9a-203">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="55b9a-204">IIS 支援：IIS 7、7.5、8、8.5 (需要有 IIS)</span><span class="sxs-lookup"><span data-stu-id="55b9a-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="55b9a-205">使用 PowerShell 進行自動化</span><span class="sxs-lookup"><span data-stu-id="55b9a-205">Automation with PowerShell</span></span>
<span data-ttu-id="55b9a-206">您可以在 IIS 伺服器上使用 PowerShell 啟動和停止監視。</span><span class="sxs-lookup"><span data-stu-id="55b9a-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="55b9a-207">先匯入 Application Insights 模組︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-207">First import the Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="55b9a-208">找出受監視的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="55b9a-209">`-Name` (選擇性) Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="55b9a-209">`-Name` (Optional) The name of a web app.</span></span>
* <span data-ttu-id="55b9a-210">顯示此 IIS 伺服器中每個 Web 應用程式 (或具名應用程式) 的 Application Insights 監視狀態。</span><span class="sxs-lookup"><span data-stu-id="55b9a-210">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span></span>
* <span data-ttu-id="55b9a-211">傳回每個應用程式的 `ApplicationInsightsApplication`︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="55b9a-212">`SdkState==EnabledAfterDeployment`︰應用程式正受到監視，並已在執行階段透過「狀態監視器」工具或 `Start-ApplicationInsightsMonitoring` 進行檢測。</span><span class="sxs-lookup"><span data-stu-id="55b9a-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="55b9a-213">`SdkState==Disabled`︰不會針對 Application insights 檢測應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-213">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span></span> <span data-ttu-id="55b9a-214">應用程式從未接受檢測，或「狀態監視器」工具或 `Stop-ApplicationInsightsMonitoring`已停用執行階段監視。</span><span class="sxs-lookup"><span data-stu-id="55b9a-214">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="55b9a-215">`SdkState==EnabledByCodeInstrumentation`︰已透過將 SDK 加入至原始程式碼來檢測應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-215">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span></span> <span data-ttu-id="55b9a-216">其 SDK 無法更新或停止。</span><span class="sxs-lookup"><span data-stu-id="55b9a-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="55b9a-217">`SdkVersion` 會顯示正用來監視此應用程式的版本。</span><span class="sxs-lookup"><span data-stu-id="55b9a-217">`SdkVersion` shows the version in use for monitoring this app.</span></span>
  * <span data-ttu-id="55b9a-218">`LatestAvailableSdkVersion`會顯示 NuGet 資源庫上目前可用的版本。</span><span class="sxs-lookup"><span data-stu-id="55b9a-218">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span></span> <span data-ttu-id="55b9a-219">若要將應用程式升級至此版本，請使用 `Update-ApplicationInsightsMonitoring`。</span><span class="sxs-lookup"><span data-stu-id="55b9a-219">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="55b9a-220">`-Name` 應用程式在 IIS 中的名稱</span><span class="sxs-lookup"><span data-stu-id="55b9a-220">`-Name` The name of the app in IIS</span></span>
* <span data-ttu-id="55b9a-221">`-InstrumentationKey` 您想要在其中顯示結果之 Application Insights 資源的 ikey。</span><span class="sxs-lookup"><span data-stu-id="55b9a-221">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span></span>
* <span data-ttu-id="55b9a-222">這個 Cmdlet 只會影響尚未檢測的應用程式，也就是 SdkState==NotInstrumented。</span><span class="sxs-lookup"><span data-stu-id="55b9a-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="55b9a-223">這個 Cmdlet 不會影響已經過檢測的應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-223">The cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="55b9a-224">不論是在建置階段透過將 SDK 新增至程式碼，還是在執行階段透過先前使用的這個 Cmdlet，都沒有影響。</span><span class="sxs-lookup"><span data-stu-id="55b9a-224">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="55b9a-225">用來檢測應用程式的 SDK 版本是最常下載到此伺服器的版本。</span><span class="sxs-lookup"><span data-stu-id="55b9a-225">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span></span>

    <span data-ttu-id="55b9a-226">若要下載最新版本，請使用 Update-ApplicationInsightsVersion。</span><span class="sxs-lookup"><span data-stu-id="55b9a-226">To download the latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="55b9a-227">成功時會傳回 `ApplicationInsightsApplication` 。</span><span class="sxs-lookup"><span data-stu-id="55b9a-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="55b9a-228">如果失敗，則會在 stderr 記錄追蹤。</span><span class="sxs-lookup"><span data-stu-id="55b9a-228">If it fails, it logs a trace to stderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="55b9a-229">`-Name` 應用程式在 IIS 中的名稱</span><span class="sxs-lookup"><span data-stu-id="55b9a-229">`-Name` The name of an app in IIS</span></span>
* <span data-ttu-id="55b9a-230">`-All` 停止監視此 IIS 伺服器中所有 `SdkState==EnabledAfterDeployment` 的應用程式</span><span class="sxs-lookup"><span data-stu-id="55b9a-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="55b9a-231">停止監視指定應用程式並移除檢測。</span><span class="sxs-lookup"><span data-stu-id="55b9a-231">Stops monitoring the specified apps and removes instrumentation.</span></span> <span data-ttu-id="55b9a-232">它僅適用於已在執行階段使用「狀態監視器」工具或 Start-ApplicationInsightsApplication 進行檢測的應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-232">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="55b9a-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="55b9a-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="55b9a-234">傳回 ApplicationInsightsApplication。</span><span class="sxs-lookup"><span data-stu-id="55b9a-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="55b9a-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="55b9a-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="55b9a-236">`-Name`：Web 應用程式在 IIS 中的名稱。</span><span class="sxs-lookup"><span data-stu-id="55b9a-236">`-Name`: The name of a web app in IIS.</span></span>
* <span data-ttu-id="55b9a-237">`-InstrumentationKey` (選擇性)。使用此參數可變更應用程式的遙測所要傳送至的資源。</span><span class="sxs-lookup"><span data-stu-id="55b9a-237">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span></span>
* <span data-ttu-id="55b9a-238">此 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="55b9a-238">This cmdlet:</span></span>
  * <span data-ttu-id="55b9a-239">將具名應用程式升級至最近下載到這台電腦之 SDK 的版本。</span><span class="sxs-lookup"><span data-stu-id="55b9a-239">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span></span> <span data-ttu-id="55b9a-240">(僅適用於 `SdkState==EnabledAfterDeployment`時)</span><span class="sxs-lookup"><span data-stu-id="55b9a-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="55b9a-241">如果您提供檢測金鑰，具名應用程式會重新設定為將遙測傳送至具有該索引鍵的資源。</span><span class="sxs-lookup"><span data-stu-id="55b9a-241">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span></span> <span data-ttu-id="55b9a-242">(適用於 `SdkState != Disabled`時)</span><span class="sxs-lookup"><span data-stu-id="55b9a-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="55b9a-243">將最新的 Application Insights SDK 下載至伺服器。</span><span class="sxs-lookup"><span data-stu-id="55b9a-243">Downloads the latest Application Insights SDK to the server.</span></span>

## <span data-ttu-id="55b9a-244"><a name="questions"></a>狀態監視器的相關問題</span><span class="sxs-lookup"><span data-stu-id="55b9a-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="55b9a-245">什麼是狀態監視器？</span><span class="sxs-lookup"><span data-stu-id="55b9a-245">What is Status Monitor?</span></span>

<span data-ttu-id="55b9a-246">您在 IIS Web 伺服器中安裝的桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="55b9a-247">它可協助您檢測和設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55b9a-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="55b9a-248">如何使用狀態監視器？</span><span class="sxs-lookup"><span data-stu-id="55b9a-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="55b9a-249">檢測在 IIS 伺服器上執行的任何 Web 應用程式 - 即使它已在執行中。</span><span class="sxs-lookup"><span data-stu-id="55b9a-249">To instrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="55b9a-250">針對已在編譯階段[使用 Application Insights SDK 建置](app-insights-asp-net.md)的 Web 應用程式，啟用其他遙測。</span><span class="sxs-lookup"><span data-stu-id="55b9a-250">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="55b9a-251">是否可以在執行之後將它關閉？</span><span class="sxs-lookup"><span data-stu-id="55b9a-251">Can I close it after it runs?</span></span>

<span data-ttu-id="55b9a-252">是。</span><span class="sxs-lookup"><span data-stu-id="55b9a-252">Yes.</span></span> <span data-ttu-id="55b9a-253">檢測您選取的網站之後，您可以將它關閉。</span><span class="sxs-lookup"><span data-stu-id="55b9a-253">After it has instrumented the websites you select, you can close it.</span></span>

<span data-ttu-id="55b9a-254">它本身不會收集遙測資料。</span><span class="sxs-lookup"><span data-stu-id="55b9a-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="55b9a-255">它只會設定 Web 應用程式和設定一些權限。</span><span class="sxs-lookup"><span data-stu-id="55b9a-255">It just configures the web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="55b9a-256">狀態監視器有何作用？</span><span class="sxs-lookup"><span data-stu-id="55b9a-256">What does Status Monitor do?</span></span>

<span data-ttu-id="55b9a-257">當您選取 Web 應用程式以供狀態監視器檢測時︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-257">When you select a web app for Status Monitor to instrument:</span></span>

* <span data-ttu-id="55b9a-258">下載 Application Insights 組件和 .config 檔案並且放置於 Web 應用程式的 binaries 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="55b9a-258">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span></span>
* <span data-ttu-id="55b9a-259">修改 `web.config` 以新增 Application Insights HTTP 追蹤模組。</span><span class="sxs-lookup"><span data-stu-id="55b9a-259">Modifies `web.config` to add the Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="55b9a-260">啟用 CLR 剖析以收集相依性呼叫。</span><span class="sxs-lookup"><span data-stu-id="55b9a-260">Enables CLR profiling to collect dependency calls.</span></span>

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a><span data-ttu-id="55b9a-261">每次更新應用程式時，是否需要執行狀態監視器？</span><span class="sxs-lookup"><span data-stu-id="55b9a-261">Do I need to run Status Monitor whenever I update the app?</span></span>

<span data-ttu-id="55b9a-262">如果您是以累加方式重新部署，則不需要。</span><span class="sxs-lookup"><span data-stu-id="55b9a-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="55b9a-263">如果您在發佈程序中選取 [刪除現有的檔案] 選項，則必須重新執行狀態監視器才能設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="55b9a-263">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="55b9a-264">會收集哪些遙測資料？</span><span class="sxs-lookup"><span data-stu-id="55b9a-264">What telemetry is collected?</span></span>

<span data-ttu-id="55b9a-265">對於只會在執行階段使用狀態監視器檢測的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="55b9a-266">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="55b9a-266">HTTP requests</span></span>
* <span data-ttu-id="55b9a-267">相依性呼叫</span><span class="sxs-lookup"><span data-stu-id="55b9a-267">Calls to dependencies</span></span>
* <span data-ttu-id="55b9a-268">例外狀況</span><span class="sxs-lookup"><span data-stu-id="55b9a-268">Exceptions</span></span>
* <span data-ttu-id="55b9a-269">效能計數器</span><span class="sxs-lookup"><span data-stu-id="55b9a-269">Performance counters</span></span>

<span data-ttu-id="55b9a-270">對於在編譯階段已經過檢測的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="55b9a-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="55b9a-271">處理程序計數器。</span><span class="sxs-lookup"><span data-stu-id="55b9a-271">Process counters.</span></span>
 * <span data-ttu-id="55b9a-272">相依性呼叫 (.NET 4.5)；在相依性呼叫中傳回值 (.NET 4.6)。</span><span class="sxs-lookup"><span data-stu-id="55b9a-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="55b9a-273">例外狀況堆疊追蹤值。</span><span class="sxs-lookup"><span data-stu-id="55b9a-273">Exception stack trace values.</span></span>

[<span data-ttu-id="55b9a-274">深入了解</span><span class="sxs-lookup"><span data-stu-id="55b9a-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="55b9a-275">影片</span><span class="sxs-lookup"><span data-stu-id="55b9a-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="55b9a-276"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="55b9a-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="55b9a-277">檢視遙測：</span><span class="sxs-lookup"><span data-stu-id="55b9a-277">View your telemetry:</span></span>

* <span data-ttu-id="55b9a-278">[探索計量](app-insights-metrics-explorer.md)以監視效能和使用量</span><span class="sxs-lookup"><span data-stu-id="55b9a-278">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span></span>
* <span data-ttu-id="55b9a-279">[搜尋事件和記錄][diagnostic]以診斷問題</span><span class="sxs-lookup"><span data-stu-id="55b9a-279">[Search events and logs][diagnostic] to diagnose problems</span></span>
* <span data-ttu-id="55b9a-280">更多進階查詢的[分析](app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="55b9a-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="55b9a-281">建立儀表板</span><span class="sxs-lookup"><span data-stu-id="55b9a-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="55b9a-282">新增更多遙測：</span><span class="sxs-lookup"><span data-stu-id="55b9a-282">Add more telemetry:</span></span>

* <span data-ttu-id="55b9a-283">[建立 Web 測試][availability]，確定您的網站保持即時狀態。</span><span class="sxs-lookup"><span data-stu-id="55b9a-283">[Create web tests][availability] to make sure your site stays live.</span></span>
* <span data-ttu-id="55b9a-284">[新增 Web 用戶端遙測][usage]，以查看網頁程式碼中的例外狀況，並讓您插入追蹤呼叫。</span><span class="sxs-lookup"><span data-stu-id="55b9a-284">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span></span>
* <span data-ttu-id="55b9a-285">[將 Application Insights SDK 新增至您的程式碼][greenbrown]，以便插入追蹤和記錄呼叫</span><span class="sxs-lookup"><span data-stu-id="55b9a-285">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
