---
title: "aaaMonitor 即時的 ASP.NET web 應用程式與 Azure Application Insights |Microsoft 文件"
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
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="45924-104">在執行階段使用 Application Insights 檢測 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="45924-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="45924-105">您可以檢測即時 web 應用程式使用 Azure Application Insights，而不需要 toomodify 或重新部署您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="45924-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="45924-106">如果您的應用程式是由內部部署 IIS 伺服器裝載，請安裝狀態監視器。</span><span class="sxs-lookup"><span data-stu-id="45924-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="45924-107">如果它們是 Azure web 應用程式，或在 Azure VM 中執行，您可以切換 hello Azure 控制台中的 Application Insights 監視。</span><span class="sxs-lookup"><span data-stu-id="45924-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="45924-108">(我們還提供有關檢測[即時 J2EE Web 應用程式](app-insights-java-live.md)和 [Azure 雲端服務](app-insights-cloudservices.md)的個別文章)。您需要 [Microsoft Azure](http://azure.com) 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45924-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![範例圖表](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="45924-110">您可以選擇三個路由 tooapply Application Insights tooyour.NET web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="45924-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="45924-111">**建置時間：** [新增 hello Application Insights SDK] [ greenbrown] tooyour web 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="45924-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="45924-112">**執行階段：**檢測 hello 伺服器上的 web 應用程式，如下所述，而不需要重建並重新部署 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="45924-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="45924-113">**兩者：** hello SDK 建置成 web 應用程式程式碼，以及也適用於 hello 執行階段擴充。</span><span class="sxs-lookup"><span data-stu-id="45924-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="45924-114">取得兩個選項的最佳 hello。</span><span class="sxs-lookup"><span data-stu-id="45924-114">Get hello best of both options.</span></span>

<span data-ttu-id="45924-115">以下是您可在每種途徑中取得的優勢摘要︰</span><span class="sxs-lookup"><span data-stu-id="45924-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="45924-116">建置階段</span><span class="sxs-lookup"><span data-stu-id="45924-116">Build time</span></span> | <span data-ttu-id="45924-117">執行階段</span><span class="sxs-lookup"><span data-stu-id="45924-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="45924-118">要求和例外狀況</span><span class="sxs-lookup"><span data-stu-id="45924-118">Requests & exceptions</span></span> |<span data-ttu-id="45924-119">是</span><span class="sxs-lookup"><span data-stu-id="45924-119">Yes</span></span> |<span data-ttu-id="45924-120">是</span><span class="sxs-lookup"><span data-stu-id="45924-120">Yes</span></span> |
| [<span data-ttu-id="45924-121">更詳細的例外狀況</span><span class="sxs-lookup"><span data-stu-id="45924-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="45924-122">是</span><span class="sxs-lookup"><span data-stu-id="45924-122">Yes</span></span> |
| [<span data-ttu-id="45924-123">相依性診斷</span><span class="sxs-lookup"><span data-stu-id="45924-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="45924-124">在 .Net 4.6 + 上，但較少細節</span><span class="sxs-lookup"><span data-stu-id="45924-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="45924-125">是，完整詳細資料︰結果碼、SQL 命令文字、HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="45924-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="45924-126">系統效能計數器</span><span class="sxs-lookup"><span data-stu-id="45924-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="45924-127">是</span><span class="sxs-lookup"><span data-stu-id="45924-127">Yes</span></span> |<span data-ttu-id="45924-128">是</span><span class="sxs-lookup"><span data-stu-id="45924-128">Yes</span></span> |
| <span data-ttu-id="45924-129">[自訂遙測的 API][api]</span><span class="sxs-lookup"><span data-stu-id="45924-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="45924-130">是</span><span class="sxs-lookup"><span data-stu-id="45924-130">Yes</span></span> |<span data-ttu-id="45924-131">否</span><span class="sxs-lookup"><span data-stu-id="45924-131">No</span></span> |
| [<span data-ttu-id="45924-132">追蹤記錄檔整合</span><span class="sxs-lookup"><span data-stu-id="45924-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="45924-133">是</span><span class="sxs-lookup"><span data-stu-id="45924-133">Yes</span></span> |<span data-ttu-id="45924-134">否</span><span class="sxs-lookup"><span data-stu-id="45924-134">No</span></span> |
| [<span data-ttu-id="45924-135">頁面檢視和使用者資料</span><span class="sxs-lookup"><span data-stu-id="45924-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="45924-136">是</span><span class="sxs-lookup"><span data-stu-id="45924-136">Yes</span></span> |<span data-ttu-id="45924-137">否</span><span class="sxs-lookup"><span data-stu-id="45924-137">No</span></span> |
| <span data-ttu-id="45924-138">需要 toorebuild 程式碼</span><span class="sxs-lookup"><span data-stu-id="45924-138">Need toorebuild code</span></span> |<span data-ttu-id="45924-139">是</span><span class="sxs-lookup"><span data-stu-id="45924-139">Yes</span></span> | <span data-ttu-id="45924-140">否</span><span class="sxs-lookup"><span data-stu-id="45924-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="45924-141">監視即時 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="45924-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="45924-142">如果您的應用程式正在執行做為 Azure web 服務，這裡的方式，來監視 tooswitch:</span><span class="sxs-lookup"><span data-stu-id="45924-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="45924-143">在 Azure 中的 hello 應用程式的控制面板上選取 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="45924-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![針對 Azure Web 應用程式設定 Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="45924-145">Hello Application Insights 摘要 頁面開啟時，按一下 hello hello 底部 tooopen hello 完整的 Application Insights 資源連結。</span><span class="sxs-lookup"><span data-stu-id="45924-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![按一下 透過 tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="45924-147">[監視雲端和 VM 應用程式](app-insights-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="45924-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="45924-148">在 Azure 中啟用用戶端監視</span><span class="sxs-lookup"><span data-stu-id="45924-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="45924-149">如果您已在 Azure 中啟用 Application Insights，即可新增頁面檢視和使用者遙測。</span><span class="sxs-lookup"><span data-stu-id="45924-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="45924-150">選取 [設定] > [應用程式設定]</span><span class="sxs-lookup"><span data-stu-id="45924-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="45924-151">在 [應用程式設定] 之下，新增索引鍵值組︰</span><span class="sxs-lookup"><span data-stu-id="45924-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="45924-152">索引鍵︰`APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="45924-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="45924-153">值: `true`</span><span class="sxs-lookup"><span data-stu-id="45924-153">Value: `true`</span></span>
3. <span data-ttu-id="45924-154">**儲存**hello 設定和**重新啟動**您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45924-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="45924-155">hello Application Insights JavaScript SDK 現在插入每個網頁。</span><span class="sxs-lookup"><span data-stu-id="45924-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="45924-156">監視即時 IIS Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="45924-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="45924-157">如果您的應用程式裝載於 IIS 伺服器上，請使用狀態監視器來啟用 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="45924-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="45924-158">在 IIS Web 伺服器上，以系統管理員認證登入。</span><span class="sxs-lookup"><span data-stu-id="45924-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="45924-159">如果尚未安裝 Application Insights 狀態監視器，下載並執行 hello[狀態監視安裝程式](http://go.microsoft.com/fwlink/?LinkId=506648)(或執行[Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) ，並在其中搜尋應用程式 Insights 狀態監視）。</span><span class="sxs-lookup"><span data-stu-id="45924-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="45924-160">在狀態監視器中，選取 hello 安裝 web 應用程式或您想 toomonitor 的網站。</span><span class="sxs-lookup"><span data-stu-id="45924-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="45924-161">利用您的 Azure 認證登入。</span><span class="sxs-lookup"><span data-stu-id="45924-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="45924-162">設定您想要 toosee hello 結果 hello Application Insights 入口網站中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="45924-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="45924-163">（通常是最佳 toocreate 新的資源。</span><span class="sxs-lookup"><span data-stu-id="45924-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="45924-164">如果您已經為此應用程式設定 [Web 測試][availability]或[用戶端監視][client]，請選取現有的資源。)</span><span class="sxs-lookup"><span data-stu-id="45924-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![選擇應用程式和資源。](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="45924-166">重新啟動 IIS。</span><span class="sxs-lookup"><span data-stu-id="45924-166">Restart IIS.</span></span>

    ![選擇在 hello hello 對話方塊頂端的重新啟動。](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="45924-168">您的 Web 服務會中斷一小段時間。</span><span class="sxs-lookup"><span data-stu-id="45924-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="45924-169">自訂監視選項</span><span class="sxs-lookup"><span data-stu-id="45924-169">Customize monitoring options</span></span>

<span data-ttu-id="45924-170">啟用 Application Insights 加入 Dll 和 ApplicationInsights.config tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45924-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="45924-171">您可以[編輯 hello.config 檔案](app-insights-configuration-with-applicationinsights-config.md)toochange 部份 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="45924-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="45924-172">當您重新發佈您的應用程式時，請重新啟用 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="45924-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="45924-173">在重新發行應用程式之前，請考慮[Visual Studio 中加入 Application Insights toohello 程式碼][greenbrown]。</span><span class="sxs-lookup"><span data-stu-id="45924-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="45924-174">您會取得更詳細的遙測和 hello 能力 toowrite 自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="45924-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="45924-175">如果您想 toore-發行，而不加入 Application Insights toohello 程式碼，請注意，hello 部署程序可能會刪除 hello Dll 並從 hello ApplicationInsights.config 發行網站。</span><span class="sxs-lookup"><span data-stu-id="45924-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="45924-176">因此：</span><span class="sxs-lookup"><span data-stu-id="45924-176">Therefore:</span></span>

1. <span data-ttu-id="45924-177">如果您已編輯 ApplicationInsights.config，請在重新發佈應用程式前複製一份。</span><span class="sxs-lookup"><span data-stu-id="45924-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="45924-178">重新發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45924-178">Republish your app.</span></span>
3. <span data-ttu-id="45924-179">重新啟用 Application Insights 監視功能。</span><span class="sxs-lookup"><span data-stu-id="45924-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="45924-180">(使用 hello 適當的方法： hello Azure web 應用程式控制項面板或 IIS 主機上的 hello 狀態監視器。)</span><span class="sxs-lookup"><span data-stu-id="45924-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="45924-181">恢復所有您在 hello.config 檔案執行的編輯。</span><span class="sxs-lookup"><span data-stu-id="45924-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="45924-182">針對 Application Insights 的執行階段組態進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="45924-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="45924-183">無法連接？</span><span class="sxs-lookup"><span data-stu-id="45924-183">Can't connect?</span></span> <span data-ttu-id="45924-184">沒有遙測資料？</span><span class="sxs-lookup"><span data-stu-id="45924-184">No telemetry?</span></span>

* <span data-ttu-id="45924-185">開啟[hello 必要的外寄連接埠](app-insights-ip-addresses.md#outgoing-ports)中伺服器的防火牆 tooallow 狀態監視器 toowork。</span><span class="sxs-lookup"><span data-stu-id="45924-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="45924-186">開啟狀態監視器，然後選取左窗格中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45924-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="45924-187">檢查是否有此應用程式在 hello [設定通知] 區段中的任何診斷訊息：</span><span class="sxs-lookup"><span data-stu-id="45924-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![開啟 hello 效能刀鋒視窗 toosee 要求、 回應時間、 相依性和其他資料](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="45924-189">Hello 在伺服器上，如果您看到有關 「 權限不足 」 的訊息，請嘗試 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="45924-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="45924-190">在 [IIS 管理員] 中，選取您應用程式集區中，開啟**進階設定**，然後在**處理序模型**請注意 hello 身分識別。</span><span class="sxs-lookup"><span data-stu-id="45924-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="45924-191">在電腦管理控制台中，新增此身分識別 toohello Performance Monitor Users 群組。</span><span class="sxs-lookup"><span data-stu-id="45924-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="45924-192">如果您的伺服器上已安裝 MMA/SCOM (Microsoft Operations Management Suite)，某些版本可能會發生衝突。</span><span class="sxs-lookup"><span data-stu-id="45924-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="45924-193">解除安裝 SCOM 和狀態監視，並重新安裝 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="45924-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="45924-194">請參閱[疑難排解][qna]。</span><span class="sxs-lookup"><span data-stu-id="45924-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="45924-195">系統需求</span><span class="sxs-lookup"><span data-stu-id="45924-195">System Requirements</span></span>
<span data-ttu-id="45924-196">支援伺服器上 Application Insights 狀態監視器的作業系統：</span><span class="sxs-lookup"><span data-stu-id="45924-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="45924-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="45924-197">Windows Server 2008</span></span>
* <span data-ttu-id="45924-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="45924-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="45924-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="45924-199">Windows Server 2012</span></span>
* <span data-ttu-id="45924-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="45924-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="45924-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="45924-201">Windows Server 2016</span></span>

<span data-ttu-id="45924-202">(含最新版 SP 和 .NET Framework 4.5)</span><span class="sxs-lookup"><span data-stu-id="45924-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="45924-203">Hello 用戶端上： Windows 7、 8、 8.1 和 10，一次使用.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="45924-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="45924-204">IIS 支援：IIS 7、7.5、8、8.5 (需要有 IIS)</span><span class="sxs-lookup"><span data-stu-id="45924-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="45924-205">使用 PowerShell 進行自動化</span><span class="sxs-lookup"><span data-stu-id="45924-205">Automation with PowerShell</span></span>
<span data-ttu-id="45924-206">您可以在 IIS 伺服器上使用 PowerShell 啟動和停止監視。</span><span class="sxs-lookup"><span data-stu-id="45924-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="45924-207">第一次匯入 hello Application Insights 模組：</span><span class="sxs-lookup"><span data-stu-id="45924-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="45924-208">找出受監視的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="45924-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="45924-209">`-Name`（選擇性） hello 的 web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="45924-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="45924-210">顯示 hello 這個 IIS 伺服器中的 Application Insights 監視狀態，每個 web 應用程式 （或 hello 名為應用程式）。</span><span class="sxs-lookup"><span data-stu-id="45924-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="45924-211">傳回每個應用程式的 `ApplicationInsightsApplication`︰</span><span class="sxs-lookup"><span data-stu-id="45924-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="45924-212">`SdkState==EnabledAfterDeployment`： 應用程式正受到監視，與 hello 狀態監視工具，或藉由已檢測執行階段`Start-ApplicationInsightsMonitoring`。</span><span class="sxs-lookup"><span data-stu-id="45924-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="45924-213">`SdkState==Disabled`: hello 應用程式則不會檢測 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="45924-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="45924-214">它永遠不會檢測，或是使用 hello 狀態監視工具，或使用執行階段監視已停用`Stop-ApplicationInsightsMonitoring`。</span><span class="sxs-lookup"><span data-stu-id="45924-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="45924-215">`SdkState==EnabledByCodeInstrumentation`: hello 應用程式已檢測加入 hello SDK toohello 來源的程式碼。</span><span class="sxs-lookup"><span data-stu-id="45924-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="45924-216">其 SDK 無法更新或停止。</span><span class="sxs-lookup"><span data-stu-id="45924-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="45924-217">`SdkVersion`顯示 hello 版本中用來監視此應用程式。</span><span class="sxs-lookup"><span data-stu-id="45924-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="45924-218">`LatestAvailableSdkVersion`顯示目前可用的 hello 版本 hello NuGet gallery 上。</span><span class="sxs-lookup"><span data-stu-id="45924-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="45924-219">tooupgrade hello 應用程式 toothis 版本，使用`Update-ApplicationInsightsMonitoring`。</span><span class="sxs-lookup"><span data-stu-id="45924-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="45924-220">`-Name`hello 在 IIS 中的 hello 應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="45924-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="45924-221">`-InstrumentationKey`hello ikey 的 hello 您想要顯示 hello 結果 toobe Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="45924-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="45924-222">這個 Cmdlet 只會影響尚未檢測的應用程式，也就是 SdkState==NotInstrumented。</span><span class="sxs-lookup"><span data-stu-id="45924-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="45924-223">hello cmdlet 不會影響已檢測的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45924-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="45924-224">它不不管 hello 應用程式已在建置階段檢測將 hello SDK toohello 程式碼，或在執行階段的先前使用這個 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="45924-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="45924-225">hello SDK 版本使用 tooinstrument hello 應用程式是最近的 hello 版本 toothis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="45924-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="45924-226">toodownload hello 最新版本，使用 Update ApplicationInsightsVersion。</span><span class="sxs-lookup"><span data-stu-id="45924-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="45924-227">成功時會傳回 `ApplicationInsightsApplication` 。</span><span class="sxs-lookup"><span data-stu-id="45924-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="45924-228">如果失敗，就會記錄追蹤 toostderr。</span><span class="sxs-lookup"><span data-stu-id="45924-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="45924-229">`-Name`hello 在 IIS 中的應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="45924-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="45924-230">`-All` 停止監視此 IIS 伺服器中所有 `SdkState==EnabledAfterDeployment` 的應用程式</span><span class="sxs-lookup"><span data-stu-id="45924-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="45924-231">停止監視 hello 指定應用程式，並移除檢測。</span><span class="sxs-lookup"><span data-stu-id="45924-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="45924-232">僅適用於在執行階段使用已檢測的應用程式 hello 狀態監視工具或開始 ApplicationInsightsApplication 的。</span><span class="sxs-lookup"><span data-stu-id="45924-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="45924-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="45924-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="45924-234">傳回 ApplicationInsightsApplication。</span><span class="sxs-lookup"><span data-stu-id="45924-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="45924-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="45924-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="45924-236">`-Name`: hello 的 web 應用程式在 IIS 中的名稱。</span><span class="sxs-lookup"><span data-stu-id="45924-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="45924-237">`-InstrumentationKey` (選擇性)。使用此 toochange hello 資源 toowhich hello 應用程式的遙測傳送。</span><span class="sxs-lookup"><span data-stu-id="45924-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="45924-238">此 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="45924-238">This cmdlet:</span></span>
  * <span data-ttu-id="45924-239">名為應用程式 toohello 版的 hello SDK 升級 hello 最近下載 toothis 機器。</span><span class="sxs-lookup"><span data-stu-id="45924-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="45924-240">(僅適用於 `SdkState==EnabledAfterDeployment`時)</span><span class="sxs-lookup"><span data-stu-id="45924-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="45924-241">如果您提供的檢測金鑰時，名為應用程式的 hello 是重新設定的 toosend 遙測 toohello 資源與該索引鍵。</span><span class="sxs-lookup"><span data-stu-id="45924-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="45924-242">(適用於 `SdkState != Disabled`時)</span><span class="sxs-lookup"><span data-stu-id="45924-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="45924-243">下載最新版 Application Insights SDK toohello 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="45924-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="45924-244"><a name="questions"></a>狀態監視器的相關問題</span><span class="sxs-lookup"><span data-stu-id="45924-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="45924-245">什麼是狀態監視器？</span><span class="sxs-lookup"><span data-stu-id="45924-245">What is Status Monitor?</span></span>

<span data-ttu-id="45924-246">您在 IIS Web 伺服器中安裝的桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="45924-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="45924-247">它可協助您檢測和設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45924-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="45924-248">如何使用狀態監視器？</span><span class="sxs-lookup"><span data-stu-id="45924-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="45924-249">tooinstrument 任何 web 應用程式執行您的 IIS 伺服器-即使已在執行。</span><span class="sxs-lookup"><span data-stu-id="45924-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="45924-250">web 應用程式已 tooenable 其他遙測[hello Application Insights SDK 以建置](app-insights-asp-net.md)在編譯時間。</span><span class="sxs-lookup"><span data-stu-id="45924-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="45924-251">是否可以在執行之後將它關閉？</span><span class="sxs-lookup"><span data-stu-id="45924-251">Can I close it after it runs?</span></span>

<span data-ttu-id="45924-252">是。</span><span class="sxs-lookup"><span data-stu-id="45924-252">Yes.</span></span> <span data-ttu-id="45924-253">它也已檢測您選取的 hello 網站之後，您可以將它關閉。</span><span class="sxs-lookup"><span data-stu-id="45924-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="45924-254">它本身不會收集遙測資料。</span><span class="sxs-lookup"><span data-stu-id="45924-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="45924-255">它只會設定 hello web 應用程式，並設定某些權限。</span><span class="sxs-lookup"><span data-stu-id="45924-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="45924-256">狀態監視器有何作用？</span><span class="sxs-lookup"><span data-stu-id="45924-256">What does Status Monitor do?</span></span>

<span data-ttu-id="45924-257">當您選取狀態監視 tooinstrument web 應用的程式：</span><span class="sxs-lookup"><span data-stu-id="45924-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="45924-258">下載並置於 hello web 應用程式的二進位檔案的資料夾中的 hello Application Insights 組件和.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="45924-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="45924-259">修改`web.config`tooadd hello 應用程式 Insights HTTP 追蹤模組。</span><span class="sxs-lookup"><span data-stu-id="45924-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="45924-260">啟用 CLR 程式碼分析 toocollect 相依性呼叫。</span><span class="sxs-lookup"><span data-stu-id="45924-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="45924-261">每當更新 hello 應用程式是否需要 toorun 狀態監視器？</span><span class="sxs-lookup"><span data-stu-id="45924-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="45924-262">如果您是以累加方式重新部署，則不需要。</span><span class="sxs-lookup"><span data-stu-id="45924-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="45924-263">如果您選取 hello '刪除現有檔案' 選項在 hello 發佈程序，您需要 toore 執行狀態監視器 tooconfigure Application Insights。</span><span class="sxs-lookup"><span data-stu-id="45924-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="45924-264">會收集哪些遙測資料？</span><span class="sxs-lookup"><span data-stu-id="45924-264">What telemetry is collected?</span></span>

<span data-ttu-id="45924-265">對於只會在執行階段使用狀態監視器檢測的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="45924-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="45924-266">HTTP 要求</span><span class="sxs-lookup"><span data-stu-id="45924-266">HTTP requests</span></span>
* <span data-ttu-id="45924-267">呼叫 toodependencies</span><span class="sxs-lookup"><span data-stu-id="45924-267">Calls toodependencies</span></span>
* <span data-ttu-id="45924-268">例外狀況</span><span class="sxs-lookup"><span data-stu-id="45924-268">Exceptions</span></span>
* <span data-ttu-id="45924-269">效能計數器</span><span class="sxs-lookup"><span data-stu-id="45924-269">Performance counters</span></span>

<span data-ttu-id="45924-270">對於在編譯階段已經過檢測的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="45924-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="45924-271">處理程序計數器。</span><span class="sxs-lookup"><span data-stu-id="45924-271">Process counters.</span></span>
 * <span data-ttu-id="45924-272">相依性呼叫 (.NET 4.5)；在相依性呼叫中傳回值 (.NET 4.6)。</span><span class="sxs-lookup"><span data-stu-id="45924-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="45924-273">例外狀況堆疊追蹤值。</span><span class="sxs-lookup"><span data-stu-id="45924-273">Exception stack trace values.</span></span>

[<span data-ttu-id="45924-274">深入了解</span><span class="sxs-lookup"><span data-stu-id="45924-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="45924-275">影片</span><span class="sxs-lookup"><span data-stu-id="45924-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="45924-276"><a name="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="45924-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="45924-277">檢視遙測：</span><span class="sxs-lookup"><span data-stu-id="45924-277">View your telemetry:</span></span>

* <span data-ttu-id="45924-278">[瀏覽度量](app-insights-metrics-explorer.md)toomonitor 效能和使用方式</span><span class="sxs-lookup"><span data-stu-id="45924-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="45924-279">[搜尋事件和記錄檔][ diagnostic] toodiagnose 問題</span><span class="sxs-lookup"><span data-stu-id="45924-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="45924-280">更多進階查詢的[分析](app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="45924-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="45924-281">建立儀表板</span><span class="sxs-lookup"><span data-stu-id="45924-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="45924-282">新增更多遙測：</span><span class="sxs-lookup"><span data-stu-id="45924-282">Add more telemetry:</span></span>

* <span data-ttu-id="45924-283">[建立 web 測試][ availability] toomake 網站保持即時。</span><span class="sxs-lookup"><span data-stu-id="45924-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="45924-284">[新增 web 用戶端遙測][ usage]從網頁程式碼和您插入的 toolet toosee 例外狀況追蹤呼叫。</span><span class="sxs-lookup"><span data-stu-id="45924-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="45924-285">[將 Application Insights SDK tooyour 程式碼加入][ greenbrown] ，讓您可以插入追蹤和記錄的呼叫</span><span class="sxs-lookup"><span data-stu-id="45924-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
