---
title: "Azure web 應用程式的 aaaApplication 效能常見問題集 |Microsoft 文件"
description: "取得可用性、 效能及 hello Azure App Service Web 應用程式功能的應用程式問題的相關常見問題的解答 toofrequently。"
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a><span data-ttu-id="400c9-103">Azure Web 應用程式的應用程式效能常見問題集</span><span class="sxs-lookup"><span data-stu-id="400c9-103">Application performance FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="400c9-104">這篇文章有集 (Faq) 解答 toofrequently hello 的應用程式效能問題的相關[Azure App Service Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="400c9-104">This article has answers toofrequently asked questions (FAQs) about application performance issues for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a><span data-ttu-id="400c9-105">為何我的應用程式變慢？</span><span class="sxs-lookup"><span data-stu-id="400c9-105">Why is my app slow?</span></span>

<span data-ttu-id="400c9-106">多個因素可能會構成 tooslow 應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="400c9-106">Multiple factors might contribute tooslow app performance.</span></span> <span data-ttu-id="400c9-107">如需詳細的疑難排解步驟，請參閱[針對緩慢的 Web 應用程式效能進行疑難排解](app-service-web-troubleshoot-performance-degradation.md)。</span><span class="sxs-lookup"><span data-stu-id="400c9-107">For detailed troubleshooting steps, see [Troubleshoot slow web app performance](app-service-web-troubleshoot-performance-degradation.md).</span></span>

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a><span data-ttu-id="400c9-108">如何針對高 CPU 耗用量案例進行疑難排解？</span><span class="sxs-lookup"><span data-stu-id="400c9-108">How do I troubleshoot a high CPU-consumption scenario?</span></span>

<span data-ttu-id="400c9-109">在某些高 CPU 耗用量案例中，您的應用程式可能真正需要更多運算資源。</span><span class="sxs-lookup"><span data-stu-id="400c9-109">In some high CPU-consumption scenarios, your app might truly require more computing resources.</span></span> <span data-ttu-id="400c9-110">在此情況下，請考慮調整 tooa 高服務層，因此 hello 應用程式會取得所有所需的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="400c9-110">In that case, consider scaling tooa higher service tier so hello application gets all hello resources it needs.</span></span> <span data-ttu-id="400c9-111">若是其他情況，不正確的迴圈或程式碼撰寫慣例可能會造成高 CPU 耗用量。</span><span class="sxs-lookup"><span data-stu-id="400c9-111">Other times, high CPU consumption might be caused by a bad loop or by a coding practice.</span></span> <span data-ttu-id="400c9-112">深入了解什麼觸發增加的 CPU 耗用量是兩部分的處理序。</span><span class="sxs-lookup"><span data-stu-id="400c9-112">Getting insight into what's triggering increased CPU consumption is a two-part process.</span></span> <span data-ttu-id="400c9-113">首先，建立處理序傾印，並接著分析 hello 處理序傾印。</span><span class="sxs-lookup"><span data-stu-id="400c9-113">First, create a process dump, and then analyze hello process dump.</span></span> <span data-ttu-id="400c9-114">如需詳細資訊，請參閱[擷取及分析 Web 應用程式高 CPU 耗用量的傾印檔案](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/)。</span><span class="sxs-lookup"><span data-stu-id="400c9-114">For more information, see [Capture and analyze a dump file for high CPU consumption for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/).</span></span>

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a><span data-ttu-id="400c9-115">如何針對高記憶體耗用量案例進行疑難排解？</span><span class="sxs-lookup"><span data-stu-id="400c9-115">How do I troubleshoot a high memory-consumption scenario?</span></span>

<span data-ttu-id="400c9-116">在某些高記憶體耗用量案例中，您的應用程式可能真正需要更多運算資源。</span><span class="sxs-lookup"><span data-stu-id="400c9-116">In some high memory-consumption scenarios, your app might truly require more computing resources.</span></span> <span data-ttu-id="400c9-117">在此情況下，請考慮調整 tooa 高服務層，因此 hello 應用程式會取得所有所需的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="400c9-117">In that case, consider scaling tooa higher service tier so hello application gets all hello resources it needs.</span></span> <span data-ttu-id="400c9-118">其他時候，hello 程式碼中的錯誤可能會導致記憶體流失。</span><span class="sxs-lookup"><span data-stu-id="400c9-118">Other times, a bug in hello code might cause a memory leak.</span></span> <span data-ttu-id="400c9-119">程式碼撰寫慣例也可能會增加記憶體耗用量。</span><span class="sxs-lookup"><span data-stu-id="400c9-119">A coding practice also might increase memory consumption.</span></span> <span data-ttu-id="400c9-120">深入了解什麼觸發高記憶體耗用量是兩部分的處理序。</span><span class="sxs-lookup"><span data-stu-id="400c9-120">Getting insight into what's triggering high memory consumption is a two-part process.</span></span> <span data-ttu-id="400c9-121">首先，建立處理序傾印，並接著分析 hello 處理序傾印。</span><span class="sxs-lookup"><span data-stu-id="400c9-121">First, create a process dump, and then analyze hello process dump.</span></span> <span data-ttu-id="400c9-122">從 hello Azure 站台擴充程式庫損毀診斷程式可以有效率地執行這兩個步驟執行。</span><span class="sxs-lookup"><span data-stu-id="400c9-122">Crash Diagnoser from hello Azure Site Extension Gallery can efficiently perform both these steps.</span></span> <span data-ttu-id="400c9-123">如需詳細資訊，請參閱[擷取及分析 Web 應用程式間歇高記憶體的傾印檔案](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/)。</span><span class="sxs-lookup"><span data-stu-id="400c9-123">For more information, see [Capture and analyze a dump file for intermittent high memory for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/).</span></span>

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a><span data-ttu-id="400c9-124">如何使用 PowerShell 自動化 App Service Web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="400c9-124">How do I automate App Service web apps by using PowerShell?</span></span>

<span data-ttu-id="400c9-125">您可以使用 PowerShell cmdlet toomanage 及維護 App Service web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="400c9-125">You can use PowerShell cmdlets toomanage and maintain App Service web apps.</span></span> <span data-ttu-id="400c9-126">我們的部落格文章中[自動化使用 PowerShell 在 Azure App Service 中裝載的 web 應用程式](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/)，我們將描述如何 toouse Azure 資源管理員為基礎的 PowerShell cmdlet tooautomate 一般工作。</span><span class="sxs-lookup"><span data-stu-id="400c9-126">In our blog post [Automate web apps hosted in Azure App Service by using PowerShell](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), we describe how toouse Azure Resource Manager-based PowerShell cmdlets tooautomate common tasks.</span></span> <span data-ttu-id="400c9-127">hello 部落格文章也會有各種 web 應用程式管理工作的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="400c9-127">hello blog post also has sample code for various web apps management tasks.</span></span> <span data-ttu-id="400c9-128">如需所有 App Service Web 應用程式 Cmdlet 的說明和語法，請參閱 [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0)。</span><span class="sxs-lookup"><span data-stu-id="400c9-128">For descriptions and syntax for all App Service web apps cmdlets, see [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).</span></span>

## <a name="how-do-i-view-my-web-apps-event-logs"></a><span data-ttu-id="400c9-129">如何檢視我的 Web 應用程式事件記錄？</span><span class="sxs-lookup"><span data-stu-id="400c9-129">How do I view my web app's event logs?</span></span>

<span data-ttu-id="400c9-130">tooview 您 web 應用程式事件記錄檔：</span><span class="sxs-lookup"><span data-stu-id="400c9-130">tooview your web app's event logs:</span></span>

1. <span data-ttu-id="400c9-131">登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="400c9-131">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="400c9-132">在 hello 功能表中，選取 **偵錯主控台** > **CMD**。</span><span class="sxs-lookup"><span data-stu-id="400c9-132">In hello menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="400c9-133">選取 hello **LogFiles**資料夾。</span><span class="sxs-lookup"><span data-stu-id="400c9-133">Select hello **LogFiles** folder.</span></span>
4. <span data-ttu-id="400c9-134">tooview 事件記錄檔中，選取 hello 鉛筆圖示旁太**eventlog.xml**。</span><span class="sxs-lookup"><span data-stu-id="400c9-134">tooview event logs, select hello pencil icon next too**eventlog.xml**.</span></span>
5. <span data-ttu-id="400c9-135">toodownload hello 記錄檔，執行 hello PowerShell cmdlet `Save-AzureWebSiteLog -Name webappname`。</span><span class="sxs-lookup"><span data-stu-id="400c9-135">toodownload hello logs, run hello PowerShell cmdlet `Save-AzureWebSiteLog -Name webappname`.</span></span>

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a><span data-ttu-id="400c9-136">如何擷取 Web 應用程式的使用者模式記憶體傾印？</span><span class="sxs-lookup"><span data-stu-id="400c9-136">How do I capture a user-mode memory dump of my web app?</span></span>

<span data-ttu-id="400c9-137">toocapture 您 web 應用程式的使用者模式下記憶體傾印：</span><span class="sxs-lookup"><span data-stu-id="400c9-137">toocapture a user-mode memory dump of your web app:</span></span>

1. <span data-ttu-id="400c9-138">登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="400c9-138">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="400c9-139">選取 hello**處理序總管**功能表。</span><span class="sxs-lookup"><span data-stu-id="400c9-139">Select hello **Process Explorer** menu.</span></span>
3. <span data-ttu-id="400c9-140">以滑鼠右鍵按一下 hello **w3wp.exe**程序或您的 web 工作處理序。</span><span class="sxs-lookup"><span data-stu-id="400c9-140">Right-click hello **w3wp.exe** process or your WebJob process.</span></span>
4. <span data-ttu-id="400c9-141">選取 [下載記憶體傾印] >  [完整傾印]。</span><span class="sxs-lookup"><span data-stu-id="400c9-141">Select **Download Memory Dump** > **Full Dump**.</span></span>

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a><span data-ttu-id="400c9-142">如何檢視 Web 應用程式的處理序層級資訊？</span><span class="sxs-lookup"><span data-stu-id="400c9-142">How do I view process-level info for my web app?</span></span>

<span data-ttu-id="400c9-143">您有兩個選項可以用來檢視 Web 應用程式的處理序層級資訊：</span><span class="sxs-lookup"><span data-stu-id="400c9-143">You have two options for viewing process-level information for your web app:</span></span>

*   <span data-ttu-id="400c9-144">在 hello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="400c9-144">In hello Azure portal:</span></span>
    1. <span data-ttu-id="400c9-145">開啟 hello**處理序總管**hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="400c9-145">Open hello **Process Explorer** for hello web app.</span></span>
    2. <span data-ttu-id="400c9-146">toosee hello 詳細資料，選取 hello **w3wp.exe**程序。</span><span class="sxs-lookup"><span data-stu-id="400c9-146">toosee hello details, select hello **w3wp.exe** process.</span></span>
*   <span data-ttu-id="400c9-147">在 hello Kudu 主控台：</span><span class="sxs-lookup"><span data-stu-id="400c9-147">In hello Kudu console:</span></span>
    1. <span data-ttu-id="400c9-148">登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="400c9-148">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    2. <span data-ttu-id="400c9-149">選取 hello**處理序總管**功能表。</span><span class="sxs-lookup"><span data-stu-id="400c9-149">Select hello **Process Explorer** menu.</span></span>
    3. <span data-ttu-id="400c9-150">Hello **w3wp.exe**程序中，選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="400c9-150">For hello **w3wp.exe** process, select **Properties**.</span></span>

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a><span data-ttu-id="400c9-151">當我瀏覽 toomy 應用程式時，我看到 「 錯誤 403-此 web 應用程式已停止 」。</span><span class="sxs-lookup"><span data-stu-id="400c9-151">When I browse toomy app, I see "Error 403 - This web app is stopped."</span></span> <span data-ttu-id="400c9-152">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="400c9-152">How do I resolve this?</span></span>

<span data-ttu-id="400c9-153">有三個條件會造成這個錯誤：</span><span class="sxs-lookup"><span data-stu-id="400c9-153">Three conditions can cause this error:</span></span>

* <span data-ttu-id="400c9-154">hello web 應用程式已達到帳單的限制，並且已停用您的網站。</span><span class="sxs-lookup"><span data-stu-id="400c9-154">hello web app has reached a billing limit and your site has been disabled.</span></span>
* <span data-ttu-id="400c9-155">hello web 應用程式已停止在 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="400c9-155">hello web app has been stopped in hello portal.</span></span>
* <span data-ttu-id="400c9-156">hello web 應用程式已達到資源配額限制，可能會套用 tooa 免費或共用標尺服務計劃。</span><span class="sxs-lookup"><span data-stu-id="400c9-156">hello web app has reached a resource quota limit that might apply tooa Free or Shared scale service plan.</span></span>

<span data-ttu-id="400c9-157">toosee 中造成錯誤 hello 和 tooresolve hello 問題、 後續 hello 步驟[Web 應用程式: 「 錯誤 403 – 此 web 應用程式已停止 」](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/)。</span><span class="sxs-lookup"><span data-stu-id="400c9-157">toosee what is causing hello error and tooresolve hello issue, follow hello steps in [Web Apps: "Error 403 – This web app is stopped"](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).</span></span>

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a><span data-ttu-id="400c9-158">哪裡可以深入了解各種 App Service 方案的配額和限制？</span><span class="sxs-lookup"><span data-stu-id="400c9-158">Where can I learn more about quotas and limits for various App Service plans?</span></span>

<span data-ttu-id="400c9-159">如需配額和限制的詳細資訊，請參閱 [App Service 限制](../azure-subscription-service-limits.md#app-service-limits)。</span><span class="sxs-lookup"><span data-stu-id="400c9-159">For information about quotas and limits, see [App Service limits](../azure-subscription-service-limits.md#app-service-limits).</span></span> 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a><span data-ttu-id="400c9-160">我要如何減少 hello 回應 hello 第一個要求時間之後閒置時間？</span><span class="sxs-lookup"><span data-stu-id="400c9-160">How do I decrease hello response time for hello first request after idle time?</span></span>

<span data-ttu-id="400c9-161">根據預設，Web 應用程式如果閒置一段時間，就會卸載。</span><span class="sxs-lookup"><span data-stu-id="400c9-161">By default, web apps are unloaded if they are idle for a set period of time.</span></span> <span data-ttu-id="400c9-162">如此一來，hello 系統可以節省資源。</span><span class="sxs-lookup"><span data-stu-id="400c9-162">This way, hello system can conserve resources.</span></span> <span data-ttu-id="400c9-163">hello 選項的缺點是，hello 回應 toohello 第一個要求之後卸載 hello web 應用程式是較長，tooallow hello web 應用程式 tooload 並開始處理回應。</span><span class="sxs-lookup"><span data-stu-id="400c9-163">hello downside is that hello response toohello first request after hello web app is unloaded is longer, tooallow hello web app tooload and start serving responses.</span></span> <span data-ttu-id="400c9-164">在基本和標準服務計畫中，您可以開啟 hello **Always On**設定 tookeep hello 應用程式一律載入。</span><span class="sxs-lookup"><span data-stu-id="400c9-164">In Basic and Standard service plans, you can turn on hello **Always On** setting tookeep hello app always loaded.</span></span> <span data-ttu-id="400c9-165">這排除了更長的載入時間之後 hello 應用程式處於閒置狀態。</span><span class="sxs-lookup"><span data-stu-id="400c9-165">This eliminates longer load times after hello app is idle.</span></span> <span data-ttu-id="400c9-166">toochange hello **Always On**設定：</span><span class="sxs-lookup"><span data-stu-id="400c9-166">toochange hello **Always On** setting:</span></span>

1. <span data-ttu-id="400c9-167">在 hello Azure 入口網站，移 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="400c9-167">In hello Azure portal, go tooyour web app.</span></span>
2. <span data-ttu-id="400c9-168">選取 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="400c9-168">Select **Application settings**.</span></span>
3. <span data-ttu-id="400c9-169">針對 [永遠開啟]，選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="400c9-169">For **Always On**, select **On**.</span></span>

## <a name="how-do-i-turned-on-failed-request-tracing"></a><span data-ttu-id="400c9-170">如何開啟失敗的要求追蹤？</span><span class="sxs-lookup"><span data-stu-id="400c9-170">How do I turned on failed request tracing?</span></span>

<span data-ttu-id="400c9-171">tooturn 上失敗的要求追蹤：</span><span class="sxs-lookup"><span data-stu-id="400c9-171">tooturn on failed request tracing:</span></span>

1. <span data-ttu-id="400c9-172">在 hello Azure 入口網站，移 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="400c9-172">In hello Azure portal, go tooyour web app.</span></span>
3. <span data-ttu-id="400c9-173">選取 [所有設定] >  [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="400c9-173">Select **All Settings** > **Diagnostics Logs**.</span></span>
4. <span data-ttu-id="400c9-174">針對 [失敗的要求追蹤]，選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="400c9-174">For **Failed Request Tracing**, select **On**.</span></span>
5. <span data-ttu-id="400c9-175">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="400c9-175">Select **Save**.</span></span>
6. <span data-ttu-id="400c9-176">在 hello web 應用程式刀鋒視窗中，選取 **工具**。</span><span class="sxs-lookup"><span data-stu-id="400c9-176">On hello web app blade, select **Tools**.</span></span>
7. <span data-ttu-id="400c9-177">選取 [Visual Studio Online]。</span><span class="sxs-lookup"><span data-stu-id="400c9-177">Select **Visual Studio Online**.</span></span>
8. <span data-ttu-id="400c9-178">如果未設定 hello**上**，選取**上**。</span><span class="sxs-lookup"><span data-stu-id="400c9-178">If hello setting is not **On**, select **On**.</span></span>
9. <span data-ttu-id="400c9-179">選取 [執行]。</span><span class="sxs-lookup"><span data-stu-id="400c9-179">Select **Go**.</span></span>
10. <span data-ttu-id="400c9-180">選取 **Web.config**。</span><span class="sxs-lookup"><span data-stu-id="400c9-180">Select **Web.config**.</span></span>
11. <span data-ttu-id="400c9-181">在 system.webServer，加入這項設定 (toocapture 特定 URL):</span><span class="sxs-lookup"><span data-stu-id="400c9-181">In system.webServer, add this configuration (toocapture a specific URL):</span></span>

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. <span data-ttu-id="400c9-182">tootroubleshoot 緩慢效能問題，加入這項設定 （如果 hello 擷取要求花費超過 30 秒）：</span><span class="sxs-lookup"><span data-stu-id="400c9-182">tootroubleshoot slow-performance issues, add this configuration (if hello capturing request is taking more than 30 seconds):</span></span>
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. <span data-ttu-id="400c9-183">toodownload hello 失敗要求的追蹤，在 hello[入口網站](https://portal.azure.com)，移至 tooyour 網站。</span><span class="sxs-lookup"><span data-stu-id="400c9-183">toodownload hello failed request traces, in hello [portal](https://portal.azure.com), go tooyour website.</span></span>
15. <span data-ttu-id="400c9-184">選取 [工具] >  [Kudu] >  [執行]。</span><span class="sxs-lookup"><span data-stu-id="400c9-184">Select **Tools** > **Kudu** > **Go**.</span></span>
18. <span data-ttu-id="400c9-185">在 hello 功能表中，選取 **偵錯主控台** > **CMD**。</span><span class="sxs-lookup"><span data-stu-id="400c9-185">In hello menu, select **Debug Console** > **CMD**.</span></span>
19. <span data-ttu-id="400c9-186">選取 hello **LogFiles**資料夾，然後再選取 hello 開頭的名稱的資料夾**W3SVC**。</span><span class="sxs-lookup"><span data-stu-id="400c9-186">Select hello **LogFiles** folder, and then select hello folder with a name that starts with **W3SVC**.</span></span>
20. <span data-ttu-id="400c9-187">toosee hello XML 檔案，選取 hello 鉛筆圖示。</span><span class="sxs-lookup"><span data-stu-id="400c9-187">toosee hello XML file, select hello pencil icon.</span></span>

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a><span data-ttu-id="400c9-188">我看到 hello 訊息 「 背景工作處理序要求回收到期 too'Percent 記憶體 ' 限制。 」</span><span class="sxs-lookup"><span data-stu-id="400c9-188">I see hello message "Worker Process requested recycle due too'Percent Memory' limit."</span></span> <span data-ttu-id="400c9-189">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="400c9-189">How do I address this issue?</span></span>

<span data-ttu-id="400c9-190">hello 最大可用記憶體數量 32 位元處理序 （即使在 64 位元作業系統） 上的是 2 GB。</span><span class="sxs-lookup"><span data-stu-id="400c9-190">hello maximum available amount of memory for a 32-bit process (even on a 64-bit operating system) is 2 GB.</span></span> <span data-ttu-id="400c9-191">根據預設，hello 背景工作處理序設定 too32 位元應用程式服務中 （適用於與傳統 web 應用程式的相容性）。</span><span class="sxs-lookup"><span data-stu-id="400c9-191">By default, hello worker process is set too32-bit in App Service (for compatibility with legacy web applications).</span></span>

<span data-ttu-id="400c9-192">請考慮切換 too64 位元處理序，因此您可以利用 hello 額外的記憶體可用，您的 Web 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="400c9-192">Consider switching too64-bit processes so you can take advantage of hello additional memory available in your Web Worker role.</span></span> <span data-ttu-id="400c9-193">這會觸發 Web 應用程式重新啟動，請據以排程。</span><span class="sxs-lookup"><span data-stu-id="400c9-193">This triggers a web app restart, so schedule accordingly.</span></span>

<span data-ttu-id="400c9-194">另請注意，64 位元環境需要基本或標準服務方案。</span><span class="sxs-lookup"><span data-stu-id="400c9-194">Also note that a 64-bit environment requires a Basic or Standard service plan.</span></span> <span data-ttu-id="400c9-195">[免費] 與 [共用] 方案一律於 32 位元環境中執行。</span><span class="sxs-lookup"><span data-stu-id="400c9-195">Free and Shared plans always run in a 32-bit environment.</span></span>

<span data-ttu-id="400c9-196">如需詳細資訊，請參閱 [在 App Service 中設定 Web 應用程式](https://docs.microsoft.com/azure/app-service-web/web-sites-configure)。</span><span class="sxs-lookup"><span data-stu-id="400c9-196">For more information, see [Configure web apps in App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).</span></span>

## <a name="why-does-my-request-time-out-after-240-seconds"></a><span data-ttu-id="400c9-197">為何我的要求在 240 秒後逾時？</span><span class="sxs-lookup"><span data-stu-id="400c9-197">Why does my request time out after 240 seconds?</span></span>

<span data-ttu-id="400c9-198">Azure Load Balancer 有預設四分鐘的閒置逾時設定。</span><span class="sxs-lookup"><span data-stu-id="400c9-198">Azure Load Balancer has a default idle timeout setting of four minutes.</span></span> <span data-ttu-id="400c9-199">這通常對於 Web 要求是合理的回應時間限制。</span><span class="sxs-lookup"><span data-stu-id="400c9-199">This is generally a reasonable response time limit for a web request.</span></span> <span data-ttu-id="400c9-200">如果您的 Web 應用程式需要幕後處理，我們建議您使用 Azure WebJobs。</span><span class="sxs-lookup"><span data-stu-id="400c9-200">If your web app requires background processing, we recommend using Azure WebJobs.</span></span> <span data-ttu-id="400c9-201">hello Azure web 應用程式可以呼叫 web 工作，並在背景處理完成時收到通知。</span><span class="sxs-lookup"><span data-stu-id="400c9-201">hello Azure web app can call WebJobs and be notified when background processing is finished.</span></span> <span data-ttu-id="400c9-202">您可以從使用 WebJobs 的多個方法中選擇，包括佇列和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="400c9-202">You can choose from multiple methods for using WebJobs, including queues and triggers.</span></span>

<span data-ttu-id="400c9-203">WebJobs 是設計用來進行幕後處理。</span><span class="sxs-lookup"><span data-stu-id="400c9-203">WebJobs is designed for background processing.</span></span> <span data-ttu-id="400c9-204">您可以在 WebJob 中進行您想要的任意數量幕後處理。</span><span class="sxs-lookup"><span data-stu-id="400c9-204">You can do as much background processing as you want in a WebJob.</span></span> <span data-ttu-id="400c9-205">如需 WebJobs 的詳細資訊，請參閱[使用 WebJobs 執行背景工作](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs)。</span><span class="sxs-lookup"><span data-stu-id="400c9-205">For more information about WebJobs, see [Run background tasks with WebJobs](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).</span></span>

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a><span data-ttu-id="400c9-206">裝載於 App Service 中的 ASP.NET Core 應用程式有時候會停止回應。</span><span class="sxs-lookup"><span data-stu-id="400c9-206">ASP.NET Core applications that are hosted in App Service sometimes stop responding.</span></span> <span data-ttu-id="400c9-207">如何修正此問題？</span><span class="sxs-lookup"><span data-stu-id="400c9-207">How do I fix this issue?</span></span>

<span data-ttu-id="400c9-208">先前的已知的問題[Kestrel 版本](https://github.com/aspnet/KestrelHttpServer/issues/1182)裝載的 ASP.NET Core 1.0 應用程式可能會導致應用程式服務 toointermittently 停止回應。</span><span class="sxs-lookup"><span data-stu-id="400c9-208">A known issue with an earlier [Kestrel version](https://github.com/aspnet/KestrelHttpServer/issues/1182) might cause an ASP.NET Core 1.0 app that's hosted in App Service toointermittently stop responding.</span></span> <span data-ttu-id="400c9-209">您也可能會看到此訊息: 「 hello 指定 CGI 應用程式發生錯誤和 hello 終止伺服器 hello 程序 」。</span><span class="sxs-lookup"><span data-stu-id="400c9-209">You also might see this message: "hello specified CGI Application encountered an error and hello server terminated hello process."</span></span>

<span data-ttu-id="400c9-210">Kestrel 1.0.2 版已經修正這個問題。</span><span class="sxs-lookup"><span data-stu-id="400c9-210">This issue is fixed in Kestrel version 1.0.2.</span></span> <span data-ttu-id="400c9-211">此版本隨附於 hello ASP.NET Core 1.0.3 更新。</span><span class="sxs-lookup"><span data-stu-id="400c9-211">This version is included in hello ASP.NET Core 1.0.3 update.</span></span> <span data-ttu-id="400c9-212">tooresolve 這個問題，請確定您更新您的應用程式相依性 toouse Kestrel 1.0.2。</span><span class="sxs-lookup"><span data-stu-id="400c9-212">tooresolve this issue, make sure you update your app dependencies toouse Kestrel 1.0.2.</span></span> <span data-ttu-id="400c9-213">或者，您可以使用兩種因應措施 hello 部落格文章所述的其中一個[App Service web 應用程式中的 ASP.NET Core 1.0 變慢的效能問題](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites)。</span><span class="sxs-lookup"><span data-stu-id="400c9-213">Alternatively, you can use one of two workarounds that are described in hello blog post [ASP.NET Core 1.0 slow perf issues in App Service web apps](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).</span></span>


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a><span data-ttu-id="400c9-214">我在我的 web 應用程式的 hello 檔案結構中找不到我的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="400c9-214">I can't find my log files in hello file structure of my web app.</span></span> <span data-ttu-id="400c9-215">如何找到它們？</span><span class="sxs-lookup"><span data-stu-id="400c9-215">How can I find them?</span></span>

<span data-ttu-id="400c9-216">如果您使用應用程式服務的 hello 本機快取功能，會影響 hello hello LogFiles 資料夾結構和您的應用程式服務執行個體資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="400c9-216">If you use hello Local Cache feature of App Service, hello folder structure of hello LogFiles and Data folders for your App Service instance are affected.</span></span> <span data-ttu-id="400c9-217">使用本機快取時，hello 儲存記錄檔和資料的資料夾中建立子資料夾。</span><span class="sxs-lookup"><span data-stu-id="400c9-217">When Local Cache is used, subfolders are created in hello storage LogFiles and Data folders.</span></span> <span data-ttu-id="400c9-218">hello 子資料夾使用 hello 命名模式 「 唯一識別項 」 + 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="400c9-218">hello subfolders use hello naming pattern "unique identifier" + time stamp.</span></span> <span data-ttu-id="400c9-219">每個子資料夾對應 tooa VM 執行個體中的 hello web 應用程式正在執行或已執行。</span><span class="sxs-lookup"><span data-stu-id="400c9-219">Each subfolder corresponds tooa VM instance in which hello web app is running or has run.</span></span>

<span data-ttu-id="400c9-220">toodetermine 不論您使用本機快取，請檢查您的應用程式服務**應用程式設定** 索引標籤。如果正在使用本機快取，hello 應用程式設定`WEBSITE_LOCAL_CACHE_OPTION`設定得`Always`。</span><span class="sxs-lookup"><span data-stu-id="400c9-220">toodetermine whether you are using Local Cache, check your App Service **Application settings** tab. If Local Cache is being used, hello app setting `WEBSITE_LOCAL_CACHE_OPTION` is set too`Always`.</span></span> <span data-ttu-id="400c9-221">如需有關本機快取的詳細資訊，請參閱 hello[應用程式服務的本機快取概觀](https://docs.microsoft.com/azure/app-service/app-service-local-cache)。</span><span class="sxs-lookup"><span data-stu-id="400c9-221">For more information about Local Cache, see hello [App Service Local Cache overview](https://docs.microsoft.com/azure/app-service/app-service-local-cache).</span></span>

<span data-ttu-id="400c9-222">如果您不是使用本機快取，但是也遇到此問題，請提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="400c9-222">If you are not using Local Cache and are experiencing this issue, submit a support request.</span></span>

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a><span data-ttu-id="400c9-223">我看到 hello 訊息 」 嘗試已拒絕其存取權限的方式進行 tooaccess 通訊端。 」</span><span class="sxs-lookup"><span data-stu-id="400c9-223">I see hello message "An attempt was made tooaccess a socket in a way forbidden by its access permissions."</span></span> <span data-ttu-id="400c9-224">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="400c9-224">How do I resolve this?</span></span>

<span data-ttu-id="400c9-225">如果 hello 對外 TCP 連線 hello VM 執行個體上的用完，通常就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="400c9-225">This error typically occurs if hello outbound TCP connections on hello VM instance are exhausted.</span></span> <span data-ttu-id="400c9-226">App Service 中 hello 可以對每個 VM 執行個體的傳出連線數目上限會強制執行限制。</span><span class="sxs-lookup"><span data-stu-id="400c9-226">In App Service, limits are enforced for hello maximum number of outbound connections that can be made for each VM instance.</span></span> <span data-ttu-id="400c9-227">如需詳細資訊，請參閱[跨 VM 的數值限制](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits)。</span><span class="sxs-lookup"><span data-stu-id="400c9-227">For more information, see [Cross-VM numerical limits](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits).</span></span>

<span data-ttu-id="400c9-228">如果您嘗試從您的應用程式的本機位址 tooaccess 這項錯誤也可能會發生。</span><span class="sxs-lookup"><span data-stu-id="400c9-228">This error also might occur if you try tooaccess a local address from your application.</span></span> <span data-ttu-id="400c9-229">如需詳細資訊，請參閱[本機位址要求](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests)。</span><span class="sxs-lookup"><span data-stu-id="400c9-229">For more information, see [Local address requests](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests).</span></span>

<span data-ttu-id="400c9-230">如需 web 應用程式中的輸出連線的詳細資訊，請參閱 hello 部落格文章有關[傳出連線 tooAzure 網站](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="400c9-230">For more information about outbound connections in your web app, see hello blog post about [outgoing connections tooAzure websites](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).</span></span>

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a><span data-ttu-id="400c9-231">如何使用 Visual Studio tooremote 偵錯我的 App Service web 應用程式？</span><span class="sxs-lookup"><span data-stu-id="400c9-231">How do I use Visual Studio tooremote debug my App Service web app?</span></span>

<span data-ttu-id="400c9-232">如需詳細的逐步解說，為您示範如何 toodebug web 應用程式使用 Visual Studio，請參閱[遠端偵錯您的 App Service web 應用程式](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/)。</span><span class="sxs-lookup"><span data-stu-id="400c9-232">For a detailed walkthrough that shows you how toodebug your web app by using Visual Studio, see [Remote debug your App Service web app](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).</span></span>
