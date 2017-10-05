---
title: "修正 502 不正確的閘道、503 服務無法使用錯誤 |Microsoft Docs"
description: "針對 Azure App Service 所裝載之 Web 應用程式的「502 不正確的閘道」和「503 服務無法使用」錯誤進行疑難排解。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 不正確的閘道、503 服務無法使用、錯誤 503、錯誤 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="664fe-104">對您的 Azure Web 應用程式中「502 不正確的閘道」和「503 服務無法使用」的 HTTP 錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="664fe-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="664fe-105">在裝載於 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)的 Web 應用程式中「502 不正確的閘道」和「503 服務無法使用」是常見的錯誤。</span><span class="sxs-lookup"><span data-stu-id="664fe-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="664fe-106">本文可協助您對這些錯誤進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="664fe-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="664fe-107">如果在本文章中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="664fe-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="664fe-108">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="664fe-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="664fe-109">請移至 [Azure 支援網站](https://azure.microsoft.com/support/options/) ，然後按一下 **取得支援**。</span><span class="sxs-lookup"><span data-stu-id="664fe-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="664fe-110">徵狀</span><span class="sxs-lookup"><span data-stu-id="664fe-110">Symptom</span></span>
<span data-ttu-id="664fe-111">當您瀏覽至 Web 應用程式時，它傳回 HTTP「502 不正確的閘道」錯誤或 HTTP「503 服務無法使用」錯誤。</span><span class="sxs-lookup"><span data-stu-id="664fe-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="664fe-112">原因</span><span class="sxs-lookup"><span data-stu-id="664fe-112">Cause</span></span>
<span data-ttu-id="664fe-113">此問題通常是因為應用程式層級問題所造成，例如：</span><span class="sxs-lookup"><span data-stu-id="664fe-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="664fe-114">要求耗費過長的時間</span><span class="sxs-lookup"><span data-stu-id="664fe-114">requests taking a long time</span></span>
* <span data-ttu-id="664fe-115">應用程式的記憶體/CPU 使用率過高</span><span class="sxs-lookup"><span data-stu-id="664fe-115">application using high memory/CPU</span></span>
* <span data-ttu-id="664fe-116">應用程式因例外狀況導致損毀</span><span class="sxs-lookup"><span data-stu-id="664fe-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="664fe-117">解決「502 錯誤閘道」和「503 服務無法使用」錯誤的疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="664fe-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="664fe-118">疑難排解可以分成三種不同的工作，依序為：</span><span class="sxs-lookup"><span data-stu-id="664fe-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="664fe-119">觀察和監視應用程式行為</span><span class="sxs-lookup"><span data-stu-id="664fe-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="664fe-120">收集資料</span><span class="sxs-lookup"><span data-stu-id="664fe-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="664fe-121">減輕問題</span><span class="sxs-lookup"><span data-stu-id="664fe-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="664fe-122">[App Service Web Apps](/services/app-service/web/) 在每個步驟均提供您各種選項。</span><span class="sxs-lookup"><span data-stu-id="664fe-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="664fe-123">1.觀察和監視應用程式行為</span><span class="sxs-lookup"><span data-stu-id="664fe-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="664fe-124">追蹤服務健全狀況</span><span class="sxs-lookup"><span data-stu-id="664fe-124">Track Service health</span></span>
<span data-ttu-id="664fe-125">每次發生服務中斷或效能降低時，Microsoft Azure 就會發出公告。</span><span class="sxs-lookup"><span data-stu-id="664fe-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="664fe-126">您可以在 [Azure 入口網站](https://portal.azure.com/)上追蹤服務健全狀況。</span><span class="sxs-lookup"><span data-stu-id="664fe-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="664fe-127">如需詳細資訊，請參閱[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。</span><span class="sxs-lookup"><span data-stu-id="664fe-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="664fe-128">監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="664fe-128">Monitor your web app</span></span>
<span data-ttu-id="664fe-129">此選項可讓您了解應用程式是否有任何問題。</span><span class="sxs-lookup"><span data-stu-id="664fe-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="664fe-130">在 Web 應用程式刀鋒視窗中，按一下 [ **要求和錯誤** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="664fe-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="664fe-131">[ **度量** ] 刀鋒視窗將顯示所有可以加入的計量。</span><span class="sxs-lookup"><span data-stu-id="664fe-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="664fe-132">某些您可能想用以監視 Web 應用程式的計量為</span><span class="sxs-lookup"><span data-stu-id="664fe-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="664fe-133">平均記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="664fe-133">Average memory working set</span></span>
* <span data-ttu-id="664fe-134">平均回應時間</span><span class="sxs-lookup"><span data-stu-id="664fe-134">Average response time</span></span>
* <span data-ttu-id="664fe-135">CPU 時間</span><span class="sxs-lookup"><span data-stu-id="664fe-135">CPU time</span></span>
* <span data-ttu-id="664fe-136">記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="664fe-136">Memory working set</span></span>
* <span data-ttu-id="664fe-137">要求</span><span class="sxs-lookup"><span data-stu-id="664fe-137">Requests</span></span>

![監視 Web 應用程式，以解決 502 不正確的閘道和 503 服務無法使用的 HTTP 錯誤](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="664fe-139">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="664fe-139">For more information, see:</span></span>

* [<span data-ttu-id="664fe-140">監視 Azure App Service 中的 Web Apps</span><span class="sxs-lookup"><span data-stu-id="664fe-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="664fe-141">接收警示通知</span><span class="sxs-lookup"><span data-stu-id="664fe-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="664fe-142">2.收集資料</span><span class="sxs-lookup"><span data-stu-id="664fe-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="664fe-143">使用 Azure App Service 支援入口網站</span><span class="sxs-lookup"><span data-stu-id="664fe-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="664fe-144">Web Apps 透過查看 HTTP 記錄檔、事件記錄檔、處理序傾印等，提供您疑難排解 Web 應用程式相關問題的能力。</span><span class="sxs-lookup"><span data-stu-id="664fe-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="664fe-145">您可以利用我們位於 **http://&lt;your app name>.scm.azurewebsites.net/Support** 的支援入口網站，存取所有這方面的資訊。</span><span class="sxs-lookup"><span data-stu-id="664fe-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="664fe-146">Azure App Service 支援入口網站提供三個不同的索引標籤，支援常見疑難排解案例的三個步驟：</span><span class="sxs-lookup"><span data-stu-id="664fe-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="664fe-147">觀察目前的行為</span><span class="sxs-lookup"><span data-stu-id="664fe-147">Observe current behavior</span></span>
2. <span data-ttu-id="664fe-148">藉由收集診斷資訊與執行內建分析器進行分析</span><span class="sxs-lookup"><span data-stu-id="664fe-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="664fe-149">減輕問題</span><span class="sxs-lookup"><span data-stu-id="664fe-149">Mitigate</span></span>

<span data-ttu-id="664fe-150">若問題現在正好發生，請按一下 [分析][診斷] >  > [立即診斷]，將為您建立診斷工作階段，該工作階段會收集 HTTP 記錄檔、事件檢視器記錄檔、記憶體傾印、PHP 錯誤記錄檔和 PHP 處理序報告。</span><span class="sxs-lookup"><span data-stu-id="664fe-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="664fe-151">完成資料收集後，將對資料執行分析並提供您一份 HTML 報告。</span><span class="sxs-lookup"><span data-stu-id="664fe-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="664fe-152">若您想下載資料，根據預設，資料會儲存在 D:\home\data\DaaS 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="664fe-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="664fe-153">如需有關 Azure App Service 支援入口網站的詳細資訊，請參閱 [支援 Azure 網站的網站擴充功能最新更新](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)。</span><span class="sxs-lookup"><span data-stu-id="664fe-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="664fe-154">使用 Kudu 偵錯主控台</span><span class="sxs-lookup"><span data-stu-id="664fe-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="664fe-155">Web Apps 隨附可用於偵錯、探索、上傳檔案的偵錯主控台，以及可以取得您環境相關資訊的 JSON 端點。</span><span class="sxs-lookup"><span data-stu-id="664fe-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="664fe-156">這稱為 Web 應用程式的 *Kudu 主控台*或 *SCM 儀表板*。</span><span class="sxs-lookup"><span data-stu-id="664fe-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="664fe-157">您可以前往連結 **https://&lt;Your app name>.scm.azurewebsites.net/** 存取此儀表板。</span><span class="sxs-lookup"><span data-stu-id="664fe-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="664fe-158">Kudu 提供的部分項目為：</span><span class="sxs-lookup"><span data-stu-id="664fe-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="664fe-159">您的應用程式的環境設定</span><span class="sxs-lookup"><span data-stu-id="664fe-159">environment settings for your application</span></span>
* <span data-ttu-id="664fe-160">記錄檔串流</span><span class="sxs-lookup"><span data-stu-id="664fe-160">log stream</span></span>
* <span data-ttu-id="664fe-161">診斷傾印</span><span class="sxs-lookup"><span data-stu-id="664fe-161">diagnostic dump</span></span>
* <span data-ttu-id="664fe-162">您可以執行 Powershell Cmdlet 和基本 DOS 命令的偵錯主控台。</span><span class="sxs-lookup"><span data-stu-id="664fe-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="664fe-163">Kudu 的另一項實用功能是，如果應用程式擲回第一次例外狀況，您可以使用 Kudu 和 SysInternals 工具 Procdump 建立記憶體傾印。</span><span class="sxs-lookup"><span data-stu-id="664fe-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="664fe-164">這些記憶體傾印是處理序的快照集，通常可以協助您疑難排解 Web 應用程式較複雜的問題。</span><span class="sxs-lookup"><span data-stu-id="664fe-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="664fe-165">如需有關 Kudu 可用功能的詳細資訊，請參閱 [您應該知道的 Azure 網站線上工具](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)。</span><span class="sxs-lookup"><span data-stu-id="664fe-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="664fe-166">3.減輕問題</span><span class="sxs-lookup"><span data-stu-id="664fe-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="664fe-167">調整 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="664fe-167">Scale the web app</span></span>
<span data-ttu-id="664fe-168">在 Azure App Service 中，為提高效能和輸送量，您可以調整所執行之應用程式的大小。</span><span class="sxs-lookup"><span data-stu-id="664fe-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="664fe-169">相應增加 Web 應用程式規模牽涉到兩個相關動作：將 App Service 方案變更為較高的定價層，以及在改為較高的定價層後進行某些設定。</span><span class="sxs-lookup"><span data-stu-id="664fe-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="664fe-170">如需有關調整的詳細資訊，請參閱 [在 Azure App Service 中調整 Web 應用程式規模](web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="664fe-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="664fe-171">此外，您可以選擇在多個執行個體上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="664fe-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="664fe-172">這不僅提供您更強大的處理能力，同時也提供您一定程度的容錯量。</span><span class="sxs-lookup"><span data-stu-id="664fe-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="664fe-173">若處理序在某個執行個體上中斷，其他執行個體仍將繼續處理要求。</span><span class="sxs-lookup"><span data-stu-id="664fe-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="664fe-174">您可以將調整設定為手動或自動。</span><span class="sxs-lookup"><span data-stu-id="664fe-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="664fe-175">使用 AutoHeal</span><span class="sxs-lookup"><span data-stu-id="664fe-175">Use AutoHeal</span></span>
<span data-ttu-id="664fe-176">AutoHeal 會根據您選擇的設定 (例如組態變更、要求、以記憶體為基礎的限制或執行要求所需的時間)，回收應用程式的背景工作角色處理序。</span><span class="sxs-lookup"><span data-stu-id="664fe-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="664fe-177">在大部分情況下，回收處理序是從問題中復原的最快方式。</span><span class="sxs-lookup"><span data-stu-id="664fe-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="664fe-178">雖然您永遠可以從 Azure 入口網站中直接重新啟動 Web 應用程式，AutoHeal 會自動為您完成。</span><span class="sxs-lookup"><span data-stu-id="664fe-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="664fe-179">您只需要在 Web 應用程式的根目錄 web.config 中加入某些觸發程序。</span><span class="sxs-lookup"><span data-stu-id="664fe-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="664fe-180">請注意，即使您的應用程式並非 .Net，這些設定的運作方式仍相同。</span><span class="sxs-lookup"><span data-stu-id="664fe-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="664fe-181">如需詳細資訊，請參閱 [自動修復 Azure 網站](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="664fe-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="664fe-182">重新啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="664fe-182">Restart the web app</span></span>
<span data-ttu-id="664fe-183">若要從一次性問題中復原，這通常是最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="664fe-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="664fe-184">在 [Azure 入口網站](https://portal.azure.com/)上的 Web 應用程式刀鋒視窗中有提供停止或重新啟動應用程式的選項。</span><span class="sxs-lookup"><span data-stu-id="664fe-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![重新啟動應用程式，以解決 502 不正確的閘道和 503 服務無法使用的 HTTP 錯誤](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="664fe-186">您也可以使用 Azure Powershell 管理 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="664fe-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="664fe-187">如需詳細資訊，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="664fe-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

