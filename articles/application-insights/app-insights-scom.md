---
title: "SCOM 與 Application Insights 的整合 | Microsoft Docs"
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
ms.openlocfilehash: 9c205465981fabdbb696cdc44f765532bbb992b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a><span data-ttu-id="d09c3-104">使用 Application Insights 的 SCOM 應用程式效能監視</span><span class="sxs-lookup"><span data-stu-id="d09c3-104">Application Performance Monitoring using Application Insights for SCOM</span></span>
<span data-ttu-id="d09c3-105">如果您使用 System Center Operations Manager (SCOM) 來管理您的伺服器，您便可以透過 [Azure Application Insights](app-insights-asp-net.md) 的協助來監視效能及診斷效能問題。</span><span class="sxs-lookup"><span data-stu-id="d09c3-105">If you use System Center Operations Manager (SCOM) to manage your servers, you can monitor performance and diagnose performance issues with the help of [Azure Application Insights](app-insights-asp-net.md).</span></span> <span data-ttu-id="d09c3-106">Application Insights 會監視 Web 應用程式的連入要求、REST 和 SQL 傳出呼叫、例外狀況，以及記錄追蹤。</span><span class="sxs-lookup"><span data-stu-id="d09c3-106">Application Insights monitors your web application's incoming requests, outgoing REST and SQL calls, exceptions, and log traces.</span></span> <span data-ttu-id="d09c3-107">它提供的儀表板具有度量圖表和智慧警示，以及透過此遙測來實現的強大診斷搜尋和分析查詢功能。</span><span class="sxs-lookup"><span data-stu-id="d09c3-107">It provides dashboards with metric charts and smart alerts, as well as powerful diagnostic search and analytical queries over this telemetry.</span></span> 

<span data-ttu-id="d09c3-108">您可以使用 SCOM 管理組件來開啟 Application Insights 監視。</span><span class="sxs-lookup"><span data-stu-id="d09c3-108">You can switch on Application Insights monitoring by using an SCOM management pack.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d09c3-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="d09c3-109">Before you start</span></span>
<span data-ttu-id="d09c3-110">我們假設︰</span><span class="sxs-lookup"><span data-stu-id="d09c3-110">We assume:</span></span>

* <span data-ttu-id="d09c3-111">您熟悉 SCOM，而且您使用 SCOM 2012 R2 或 2016 來管理您的 IIS Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d09c3-111">You're familiar with SCOM, and that you use SCOM 2012 R2 or 2016 to manage your IIS web servers.</span></span>
* <span data-ttu-id="d09c3-112">您已在伺服器上安裝想要使用 Application Insights 監視的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09c3-112">You have already installed on your servers a web application that you want to monitor with Application Insights.</span></span>
* <span data-ttu-id="d09c3-113">應用程式架構版本是 .NET 4.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d09c3-113">App framework version is .NET 4.5 or later.</span></span>
* <span data-ttu-id="d09c3-114">您可以存取 [Microsoft Azure](https://azure.com) 中的訂用帳戶，而且可以登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d09c3-114">You have access to a subscription in [Microsoft Azure](https://azure.com) and can sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d09c3-115">您的組織可能擁有訂用帳戶，並且可以在其中新增您的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d09c3-115">Your organization may have a subscription, and can add your Microsoft account to it.</span></span>

<span data-ttu-id="d09c3-116">(開發小組可以將 [Application Insights SDK](app-insights-asp-net.md) 建置到 Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d09c3-116">(The development team might build the [Application Insights SDK](app-insights-asp-net.md) into the web app.</span></span> <span data-ttu-id="d09c3-117">此建置階段檢測可讓他們獲得更大的彈性來撰寫自訂遙測。</span><span class="sxs-lookup"><span data-stu-id="d09c3-117">This build-time instrumentation gives them greater flexibility in writing custom telemetry.</span></span> <span data-ttu-id="d09c3-118">不過，這並不重要︰您可以依照此處所述的步驟來進行，不論有沒有內建 SDK 都可以。)</span><span class="sxs-lookup"><span data-stu-id="d09c3-118">However, it doesn't matter: you can follow the steps described here either with or without the SDK built in.)</span></span>

## <a name="one-time-install-application-insights-management-pack"></a><span data-ttu-id="d09c3-119">(一次) 安裝 Application Insights 管理組件</span><span class="sxs-lookup"><span data-stu-id="d09c3-119">(One time) Install Application Insights management pack</span></span>
<span data-ttu-id="d09c3-120">在執行 Operations Manager 的電腦上：</span><span class="sxs-lookup"><span data-stu-id="d09c3-120">On the machine where you run Operations Manager:</span></span>

1. <span data-ttu-id="d09c3-121">解除安裝任何舊版管理組件︰</span><span class="sxs-lookup"><span data-stu-id="d09c3-121">Uninstall any old version of the management pack:</span></span>
   1. <span data-ttu-id="d09c3-122">在 Operations Manager 中，開啟 [系統管理] > [管理組件]。</span><span class="sxs-lookup"><span data-stu-id="d09c3-122">In Operations Manager, open Administration, Management Packs.</span></span> 
   2. <span data-ttu-id="d09c3-123">刪除舊版本。</span><span class="sxs-lookup"><span data-stu-id="d09c3-123">Delete the old version.</span></span>
2. <span data-ttu-id="d09c3-124">從目錄下載並安裝管理組件。</span><span class="sxs-lookup"><span data-stu-id="d09c3-124">Download and install the management pack from the catalog.</span></span>
3. <span data-ttu-id="d09c3-125">重新啟動 Operations Manager。</span><span class="sxs-lookup"><span data-stu-id="d09c3-125">Restart Operations Manager.</span></span>

## <a name="create-a-management-pack"></a><span data-ttu-id="d09c3-126">建立管理組件</span><span class="sxs-lookup"><span data-stu-id="d09c3-126">Create a management pack</span></span>
1. <span data-ttu-id="d09c3-127">在 Operations Manager 中，開啟 [撰寫中] > [.NET...(使用 Application Insights)] > [加入監視精靈]，然後再次選擇 [.NET...(使用 Application Insights)]。</span><span class="sxs-lookup"><span data-stu-id="d09c3-127">In Operations Manager, open **Authoring**, **.NET...with Application Insights**, **Add Monitoring Wizard**, and again choose **.NET...with Application Insights**.</span></span>
   
    ![](./media/app-insights-scom/020.png)
2. <span data-ttu-id="d09c3-128">以您的應用程式命名組態 </span><span class="sxs-lookup"><span data-stu-id="d09c3-128">Name the configuration after your app.</span></span> <span data-ttu-id="d09c3-129">(您必須一次檢測一個應用程式)。</span><span class="sxs-lookup"><span data-stu-id="d09c3-129">(You have to instrument one app at a time.)</span></span>
   
    ![](./media/app-insights-scom/030.png)
3. <span data-ttu-id="d09c3-130">在相同的精靈頁面上，建立新的管理組件或選取您稍早為 Application Insights 建立的組件。</span><span class="sxs-lookup"><span data-stu-id="d09c3-130">On the same wizard page, either create a new management pack, or select a pack that you created for Application Insights earlier.</span></span>
   
     <span data-ttu-id="d09c3-131">(Application Insights [管理組件](https://technet.microsoft.com/library/cc974491.aspx)是可供您用來建立執行個體的範本。</span><span class="sxs-lookup"><span data-stu-id="d09c3-131">(The Application Insights [management pack](https://technet.microsoft.com/library/cc974491.aspx) is a template, from which you create an instance.</span></span> <span data-ttu-id="d09c3-132">稍後您可以重複使用相同的執行個體。)</span><span class="sxs-lookup"><span data-stu-id="d09c3-132">You can reuse the same instance later.)</span></span>

    ![在 [一般屬性] 索引標籤中，輸入應用程式的名稱。](./media/app-insights-scom/040.png)

1. <span data-ttu-id="d09c3-136">選擇一個您想要監視的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09c3-136">Choose one app that you want to monitor.</span></span> <span data-ttu-id="d09c3-137">搜尋功能會搜尋伺服器上所安裝的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09c3-137">The search feature searches among apps installed on your servers.</span></span>
   
    ![在 [要監視的項目] 索引標籤上按一下 [新增]、輸入部分應用程式名稱、按一下 [搜尋]、選擇應用程式，然後按一下 [新增] 和 [確定]。](./media/app-insights-scom/050.png)
   
    <span data-ttu-id="d09c3-139">如果您不想要在所有伺服器監視應用程式，選用的 [監視範圍] 欄位可用來指定伺服器的子集。</span><span class="sxs-lookup"><span data-stu-id="d09c3-139">The optional Monitoring scope field can be used to specify a subset of your servers, if you don't want to monitor the app in all servers.</span></span>
2. <span data-ttu-id="d09c3-140">在下一個精靈頁面上，您必須先提供用來登入 Microsoft Azure 的認證。</span><span class="sxs-lookup"><span data-stu-id="d09c3-140">On the next wizard page, you must first provide your credentials to sign in to Microsoft Azure.</span></span>
   
    <span data-ttu-id="d09c3-141">在這個頁面上，您可以選擇想要在其中分析和顯示遙測資料的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="d09c3-141">On this page, you choose the Application Insights resource where you want the telemetry data to be analyzed and displayed.</span></span> 
   
   * <span data-ttu-id="d09c3-142">如果在開發期間已針對 Application Insights 設定了應用程式，請選取其現有資源。</span><span class="sxs-lookup"><span data-stu-id="d09c3-142">If the application was configured for Application Insights during development, select its existing resource.</span></span>
   * <span data-ttu-id="d09c3-143">否則，請建立以應用程式命名的新資源。</span><span class="sxs-lookup"><span data-stu-id="d09c3-143">Otherwise, create a new resource named for the app.</span></span> <span data-ttu-id="d09c3-144">如果有其他應用程式是同一個系統的元件，請將它們放在相同的資源群組，以便能更輕鬆地管理遙測的存取權。</span><span class="sxs-lookup"><span data-stu-id="d09c3-144">If there are other apps that are components of the same system, put them in the same resource group, to make access to the telemetry easier to manage.</span></span>
     
     <span data-ttu-id="d09c3-145">您稍後可以變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="d09c3-145">You can change these settings later.</span></span>
     
     ![在 [Application Insights 設定] 索引標籤上按一下 [登入]，並提供適用於 Azure 的 Microsoft 帳戶認證。](./media/app-insights-scom/060.png)
3. <span data-ttu-id="d09c3-148">完成精靈。</span><span class="sxs-lookup"><span data-stu-id="d09c3-148">Complete the wizard.</span></span>
   
    ![Click Create](./media/app-insights-scom/070.png)

<span data-ttu-id="d09c3-150">針對您想要監視的每個應用程式重複此程序。</span><span class="sxs-lookup"><span data-stu-id="d09c3-150">Repeat this procedure for each app that you want to monitor.</span></span>

<span data-ttu-id="d09c3-151">如果您稍後需要變更設定，請從 [撰寫] 視窗重新開啟監視屬性。</span><span class="sxs-lookup"><span data-stu-id="d09c3-151">If you need to change settings later, re-open the properties of the monitor from the Authoring window.</span></span>

![在 [撰寫] 中，選取 [使用 Application Insights 的 .NET 應用程式監視效能]、選取監視器，然後按一下 [屬性]。](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a><span data-ttu-id="d09c3-153">驗證監視</span><span class="sxs-lookup"><span data-stu-id="d09c3-153">Verify monitoring</span></span>
<span data-ttu-id="d09c3-154">您已安裝的監視器會在每一部伺服器上搜尋您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09c3-154">The monitor that you have installed searches for your app on every server.</span></span> <span data-ttu-id="d09c3-155">它會在找到應用程式的地方設定 Application Insights 狀態監視器來監視應用程式。</span><span class="sxs-lookup"><span data-stu-id="d09c3-155">Where it finds the app, it configures Application Insights Status Monitor to monitor the app.</span></span> <span data-ttu-id="d09c3-156">如有必要，它會先在伺服器上安裝狀態監視器。</span><span class="sxs-lookup"><span data-stu-id="d09c3-156">If necessary, it first installs Status Monitor on the server.</span></span>

<span data-ttu-id="d09c3-157">您可以驗證它已找到之應用程式的執行個體︰</span><span class="sxs-lookup"><span data-stu-id="d09c3-157">You can verify which instances of the app it has found:</span></span>

![在 [監視] 中開啟 Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a><span data-ttu-id="d09c3-159">在 Application Insights 中檢視遙測</span><span class="sxs-lookup"><span data-stu-id="d09c3-159">View telemetry in Application Insights</span></span>
<span data-ttu-id="d09c3-160">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽至應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="d09c3-160">In the [Azure portal](https://portal.azure.com), browse to the resource for your app.</span></span> <span data-ttu-id="d09c3-161">您會[看到顯示應用程式之遙測的圖表](app-insights-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="d09c3-161">You [see charts showing telemetry](app-insights-dashboards.md) from your app.</span></span> <span data-ttu-id="d09c3-162">(如果它尚未顯示在主頁面上，請按一下 [即時度量串流])。</span><span class="sxs-lookup"><span data-stu-id="d09c3-162">(If it hasn't shown up on the main page yet, click Live Metrics Stream.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d09c3-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d09c3-163">Next steps</span></span>
* <span data-ttu-id="d09c3-164">[設定儀表板](app-insights-dashboards.md) 以將監視此應用程式和其他應用程式的最重要圖表結合在一起。</span><span class="sxs-lookup"><span data-stu-id="d09c3-164">[Set up a dashboard](app-insights-dashboards.md) to bring together the most important charts monitoring this and other apps.</span></span>
* [<span data-ttu-id="d09c3-165">深入了解度量</span><span class="sxs-lookup"><span data-stu-id="d09c3-165">Learn about metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="d09c3-166">設定警示</span><span class="sxs-lookup"><span data-stu-id="d09c3-166">Set up alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="d09c3-167">診斷效能問題</span><span class="sxs-lookup"><span data-stu-id="d09c3-167">Diagnosing performance issues</span></span>](app-insights-detect-triage-diagnose.md)
* [<span data-ttu-id="d09c3-168">功能強大的分析查詢</span><span class="sxs-lookup"><span data-stu-id="d09c3-168">Powerful Analytics queries</span></span>](app-insights-analytics.md)
* [<span data-ttu-id="d09c3-169">可用性 Web 測試</span><span class="sxs-lookup"><span data-stu-id="d09c3-169">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md)

