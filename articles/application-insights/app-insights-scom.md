---
title: "使用 Application Insights aaaSCOM 整合 |Microsoft 文件"
description: "如果您是 SCOM 使用者，請使用 Application Insights 來監視效能和診斷問題。 完整的儀表板、智慧警示、功能強大的診斷工具和分析查詢。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="c73f5-104">使用 Application Insights 的 SCOM 應用程式效能監視</span><span class="sxs-lookup"><span data-stu-id="c73f5-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="c73f5-105">如果您使用 System Center Operations Manager (SCOM) toomanage 您的伺服器，您可以監視效能和診斷效能問題的 hello 說明[Azure Application Insights](app-insights-asp-net.md)。</span><span class="sxs-lookup"><span data-stu-id="c73f5-105">If you use System Center Operations Manager (SCOM) toomanage your servers, you can monitor performance and diagnose performance issues with hello help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="c73f5-106">Application Insights 會監視 Web 應用程式的連入要求、REST 和 SQL 傳出呼叫、例外狀況，以及記錄追蹤。</span><span class="sxs-lookup"><span data-stu-id="c73f5-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="c73f5-107">它提供的儀表板具有度量圖表和智慧警示，以及透過此遙測來實現的強大診斷搜尋和分析查詢功能。</span><span class="sxs-lookup"><span data-stu-id="c73f5-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="c73f5-108">您可以使用 SCOM 管理組件來開啟 Application Insights 監視。</span><span class="sxs-lookup"><span data-stu-id="c73f5-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c73f5-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="c73f5-109">Before you start</span></span>
<span data-ttu-id="c73f5-110">我們假設︰</span><span class="sxs-lookup"><span data-stu-id="c73f5-110">We assume:</span></span>

* <span data-ttu-id="c73f5-111">您已熟悉 SCOM 中，並使用 SCOM 2012 R2 或 2016 toomanage IIS web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c73f5-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 toomanage your IIS web servers.</span></span>
* <span data-ttu-id="c73f5-112">您已安裝在伺服器上您想要使用 Application Insights toomonitor web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c73f5-112">You have already installed on your servers a web application that you want toomonitor with Application Insights.</span></span>
* <span data-ttu-id="c73f5-113">應用程式架構版本是 .NET 4.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c73f5-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="c73f5-114">您有存取 tooa 訂用帳戶[Microsoft Azure](https://azure.com)可以登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c73f5-114">You have access tooa subscription in [Microsoft Azure](https://azure.com) and can sign in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c73f5-115">您的組織可能有訂用帳戶，並可以加入您的 Microsoft 帳戶 tooit。</span><span class="sxs-lookup"><span data-stu-id="c73f5-115">Your organization may have a subscription, and can add your Microsoft account tooit.</span></span>

<span data-ttu-id="c73f5-116">(hello 開發小組可以建置 hello [Application Insights SDK](app-insights-asp-net.md)到 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c73f5-116">(hello development team might build hello [Application Insights SDK](app-insights-asp-net.md) into hello web app.</span></span> <span data-ttu-id="c73f5-117">此建置階段檢測可讓他們獲得更大的彈性來撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="c73f5-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="c73f5-118">不過，它並不重要： 您可以依照 hello 不論 SDK 內建的 hello 此處所述的步驟。)</span><span class="sxs-lookup"><span data-stu-id="c73f5-118">However, it doesn't matter: you can follow hello steps described here either with or without hello SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="c73f5-119">(一次) 安裝 Application Insights 管理組件</span><span class="sxs-lookup"><span data-stu-id="c73f5-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="c73f5-120">在執行 Operations Manager 的 hello 機器：</span><span class="sxs-lookup"><span data-stu-id="c73f5-120">On hello machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="c73f5-121">解除安裝任何舊版的 hello 管理組件：</span><span class="sxs-lookup"><span data-stu-id="c73f5-121">Uninstall any old version of hello management pack:</span></span>
   1. <span data-ttu-id="c73f5-122">在 Operations Manager 中，開啟 [系統管理] > [管理組件]。</span><span class="sxs-lookup"><span data-stu-id="c73f5-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="c73f5-123">刪除 hello 舊版本。</span><span class="sxs-lookup"><span data-stu-id="c73f5-123">Delete hello old version.</span></span>
2. <span data-ttu-id="c73f5-124">下載並安裝 hello 管理組件從 hello 類別目錄。</span><span class="sxs-lookup"><span data-stu-id="c73f5-124">Download and install hello management pack from hello catalog.</span></span>
3. <span data-ttu-id="c73f5-125">重新啟動 Operations Manager。</span><span class="sxs-lookup"><span data-stu-id="c73f5-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="c73f5-126">建立管理組件</span><span class="sxs-lookup"><span data-stu-id="c73f5-126">Create a management pack</span></span>
1. <span data-ttu-id="c73f5-127">在 Operations Manager 中，開啟 [撰寫中] > [.NET...(使用 Application Insights)] > [加入監視精靈]，然後再次選擇 [.NET...(使用 Application Insights)]。</span><span class="sxs-lookup"><span data-stu-id="c73f5-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="c73f5-128">Hello 組態之後您的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="c73f5-128">Name hello configuration after your app.</span></span> <span data-ttu-id="c73f5-129">（您需要 tooinstrument 一個應用程式一次）。</span><span class="sxs-lookup"><span data-stu-id="c73f5-129">(You have tooinstrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="c73f5-130">在 hello 相同精靈頁面上，請建立新的管理組件，或選取您稍早建立的 Application Insights 的組件。</span><span class="sxs-lookup"><span data-stu-id="c73f5-130">On hello same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="c73f5-131">(hello Application Insights[管理組件](https://technet.microsoft.com/library/cc974491.aspx)是的範本，您可以從中建立執行個體。</span><span class="sxs-lookup"><span data-stu-id="c73f5-131">(hello Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="c73f5-132">您可以重複使用相同的更新版本執行個體的 hello。）</span><span class="sxs-lookup"><span data-stu-id="c73f5-132">You can reuse hello same instance later.)</span></span>

    ![在 hello [一般] 索引標籤中，輸入 hello hello 應用程式名稱。](./media/app-insights-scom/040.png)

1. <span data-ttu-id="c73f5-136">選擇一個應用程式，您想 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="c73f5-136">Choose one app that you want toomonitor.</span></span> <span data-ttu-id="c73f5-137">在您的伺服器上安裝應用程式之間的 hello 搜尋功能搜尋。</span><span class="sxs-lookup"><span data-stu-id="c73f5-137">hello search feature searches among apps installed on your servers.</span></span>
   
    ![哪些 tooMonitor 索引標籤上，按一下 [新增]，輸入 hello 應用程式名稱的部分，按一下 [搜尋]，選擇 hello 應用程式，然後按一下 [新增]，[確定]。](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="c73f5-139">如果您不想 toomonitor hello 應用程式中的所有伺服器，hello 選擇性的監視範圍欄位可以是使用的 toospecify 您伺服器的子集。</span><span class="sxs-lookup"><span data-stu-id="c73f5-139">hello optional Monitoring scope field can be used toospecify a subset of your servers, if you don't want toomonitor hello app in all servers.</span></span>
2. <span data-ttu-id="c73f5-140">在 hello 下一步 精靈頁面上，您必須先提供您的認證 toosign tooMicrosoft Azure 中。</span><span class="sxs-lookup"><span data-stu-id="c73f5-140">On hello next wizard page, you must first provide your credentials toosign in tooMicrosoft Azure.</span></span>
   
    <span data-ttu-id="c73f5-141">這個頁面上，您可以選擇您想要分析並顯示 hello 遙測資料 toobe hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="c73f5-141">On this page, you choose hello Application Insights resource where you want hello telemetry data toobe analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="c73f5-142">如果 hello 應用程式已在開發期間設定為 Application Insights，請選取現有的資源。</span><span class="sxs-lookup"><span data-stu-id="c73f5-142">If hello application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="c73f5-143">否則，建立名為 hello 應用程式的新資源。</span><span class="sxs-lookup"><span data-stu-id="c73f5-143">Otherwise, create a new resource named for hello app.</span></span> <span data-ttu-id="c73f5-144">如果沒有其他應用程式之元件的 hello 相同的系統，將它們放在 hello 相同的資源群組、 toomake 存取 toohello 遙測更容易 toomanage。</span><span class="sxs-lookup"><span data-stu-id="c73f5-144">If there are other apps that are components of hello same system, put them in hello same resource group, toomake access toohello telemetry easier toomanage.</span></span>
     
     <span data-ttu-id="c73f5-145">您稍後可以變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="c73f5-145">You can change these settings later.</span></span>
     
     ![在 [Application Insights 設定] 索引標籤上按一下 [登入]，並提供適用於 Azure 的 Microsoft 帳戶認證。](./media/app-insights-scom/060.png)
3. <span data-ttu-id="c73f5-148">Hello 完成精靈。</span><span class="sxs-lookup"><span data-stu-id="c73f5-148">Complete hello wizard.</span></span>
   
    ![Click Create](./media/app-insights-scom/070.png)

<span data-ttu-id="c73f5-150">您想 toomonitor 每個應用程式重複此程序。</span><span class="sxs-lookup"><span data-stu-id="c73f5-150">Repeat this procedure for each app that you want toomonitor.</span></span>

<span data-ttu-id="c73f5-151">如果您稍後需要 toochange 設定，重新開啟 hello 屬性 hello 監視從 hello 撰寫視窗。</span><span class="sxs-lookup"><span data-stu-id="c73f5-151">If you need toochange settings later, re-open hello properties of hello monitor from hello Authoring window.</span></span>

![在 [撰寫] 中，選取 [使用 Application Insights 的 .NET 應用程式監視效能]、選取監視器，然後按一下 [屬性]。](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="c73f5-153">驗證監視</span><span class="sxs-lookup"><span data-stu-id="c73f5-153">Verify monitoring</span></span>
<span data-ttu-id="c73f5-154">hello 監視您已經安裝在每一部伺服器上搜尋您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c73f5-154">hello monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="c73f5-155">它會尋找 hello 應用程式，它會設定 Application Insights 狀態監視器 toomonitor hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c73f5-155">Where it finds hello app, it configures Application Insights Status Monitor toomonitor hello app.</span></span> <span data-ttu-id="c73f5-156">如有必要，先安裝狀態監視器 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="c73f5-156">If necessary, it first installs Status Monitor on hello server.</span></span>

<span data-ttu-id="c73f5-157">您可以確認它已找到的 hello 應用程式的執行個體：</span><span class="sxs-lookup"><span data-stu-id="c73f5-157">You can verify which instances of hello app it has found:</span></span>

![在 [監視] 中開啟 Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="c73f5-159">在 Application Insights 中檢視遙測</span><span class="sxs-lookup"><span data-stu-id="c73f5-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="c73f5-160">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽您的應用程式的 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="c73f5-160">In hello [Azure portal](https://portal.azure.com), browse toohello resource for your app.</span></span> <span data-ttu-id="c73f5-161">您會[看到顯示應用程式之遙測的圖表](app-insights-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="c73f5-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="c73f5-162">(如果它尚未顯示 hello 主頁面上尚未，按一下 即時度量資料流)。</span><span class="sxs-lookup"><span data-stu-id="c73f5-162">(If it hasn't shown up on hello main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c73f5-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c73f5-163">Next steps</span></span>
* <span data-ttu-id="c73f5-164">[設定儀表板](app-insights-dashboards.md)toobring 一起 hello 最重要圖表監視這與其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="c73f5-164">[Set up a dashboard](app-insights-dashboards.md) toobring together hello most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="c73f5-165">深入了解度量</span><span class="sxs-lookup"><span data-stu-id="c73f5-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="c73f5-166">設定警示</span><span class="sxs-lookup"><span data-stu-id="c73f5-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="c73f5-167">診斷效能問題</span><span class="sxs-lookup"><span data-stu-id="c73f5-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="c73f5-168">功能強大的分析查詢</span><span class="sxs-lookup"><span data-stu-id="c73f5-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="c73f5-169">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="c73f5-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

