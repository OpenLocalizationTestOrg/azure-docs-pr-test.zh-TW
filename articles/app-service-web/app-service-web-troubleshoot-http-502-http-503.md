---
title: "503 服務無法使用 」 錯誤 aaaFix 502 不正確的閘道，|Microsoft 文件"
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
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="5e1d9-104">對您的 Azure Web 應用程式中「502 不正確的閘道」和「503 服務無法使用」的 HTTP 錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="5e1d9-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="5e1d9-105">在裝載於 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)的 Web 應用程式中「502 不正確的閘道」和「503 服務無法使用」是常見的錯誤。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="5e1d9-106">本文可協助您對這些錯誤進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="5e1d9-107">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5e1d9-108">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="5e1d9-109">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)，然後按一下 **取得支援**。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="5e1d9-110">徵狀</span><span class="sxs-lookup"><span data-stu-id="5e1d9-110">Symptom</span></span>
<span data-ttu-id="5e1d9-111">當您瀏覽 toohello web 應用程式時，它會傳回 HTTP 錯誤"502 不正確的閘道 」 或 HTTP"503 服務無法使用 」 錯誤。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="5e1d9-112">原因</span><span class="sxs-lookup"><span data-stu-id="5e1d9-112">Cause</span></span>
<span data-ttu-id="5e1d9-113">此問題通常是因為應用程式層級問題所造成，例如：</span><span class="sxs-lookup"><span data-stu-id="5e1d9-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="5e1d9-114">要求耗費過長的時間</span><span class="sxs-lookup"><span data-stu-id="5e1d9-114">requests taking a long time</span></span>
* <span data-ttu-id="5e1d9-115">應用程式的記憶體/CPU 使用率過高</span><span class="sxs-lookup"><span data-stu-id="5e1d9-115">application using high memory/CPU</span></span>
* <span data-ttu-id="5e1d9-116">應用程式當機到期 tooan 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="5e1d9-117">疑難排解步驟 toosolve"502 不正確的閘道 」 和 「 503 服務無法使用 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="5e1d9-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="5e1d9-118">疑難排解可以分成三種不同的工作，依序為：</span><span class="sxs-lookup"><span data-stu-id="5e1d9-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="5e1d9-119">觀察和監視應用程式行為</span><span class="sxs-lookup"><span data-stu-id="5e1d9-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="5e1d9-120">收集資料</span><span class="sxs-lookup"><span data-stu-id="5e1d9-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="5e1d9-121">減少 hello 問題</span><span class="sxs-lookup"><span data-stu-id="5e1d9-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="5e1d9-122">[App Service Web Apps](/services/app-service/web/) 在每個步驟均提供您各種選項。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="5e1d9-123">1.觀察和監視應用程式行為</span><span class="sxs-lookup"><span data-stu-id="5e1d9-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="5e1d9-124">追蹤服務健全狀況</span><span class="sxs-lookup"><span data-stu-id="5e1d9-124">Track Service health</span></span>
<span data-ttu-id="5e1d9-125">每次發生服務中斷或效能降低時，Microsoft Azure 就會發出公告。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="5e1d9-126">您可以在 hello 追蹤 hello hello 服務健全狀況[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="5e1d9-127">如需詳細資訊，請參閱[追蹤服務健全狀況](../monitoring-and-diagnostics/insights-service-health.md)。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="5e1d9-128">監視 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e1d9-128">Monitor your web app</span></span>
<span data-ttu-id="5e1d9-129">如果您的應用程式有任何問題，此選項可讓您 toofind 出。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="5e1d9-130">在您的 web 應用程式] 刀鋒視窗中，按一下 [hello**要求與錯誤**磚。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="5e1d9-131">hello**度量**刀鋒視窗會顯示您可以加入所有 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="5e1d9-132">某些您可能希望您的 web 應用程式 toomonitor hello 度量</span><span class="sxs-lookup"><span data-stu-id="5e1d9-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="5e1d9-133">平均記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="5e1d9-133">Average memory working set</span></span>
* <span data-ttu-id="5e1d9-134">平均回應時間</span><span class="sxs-lookup"><span data-stu-id="5e1d9-134">Average response time</span></span>
* <span data-ttu-id="5e1d9-135">CPU 時間</span><span class="sxs-lookup"><span data-stu-id="5e1d9-135">CPU time</span></span>
* <span data-ttu-id="5e1d9-136">記憶體工作集</span><span class="sxs-lookup"><span data-stu-id="5e1d9-136">Memory working set</span></span>
* <span data-ttu-id="5e1d9-137">要求</span><span class="sxs-lookup"><span data-stu-id="5e1d9-137">Requests</span></span>

![監視 Web 應用程式，以解決 502 不正確的閘道和 503 服務無法使用的 HTTP 錯誤](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="5e1d9-139">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5e1d9-139">For more information, see:</span></span>

* [<span data-ttu-id="5e1d9-140">監視 Azure App Service 中的 Web Apps</span><span class="sxs-lookup"><span data-stu-id="5e1d9-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="5e1d9-141">接收警示通知</span><span class="sxs-lookup"><span data-stu-id="5e1d9-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="5e1d9-142">2.收集資料</span><span class="sxs-lookup"><span data-stu-id="5e1d9-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="5e1d9-143">使用 hello Azure 應用程式服務支援入口網站</span><span class="sxs-lookup"><span data-stu-id="5e1d9-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="5e1d9-144">Web 應用程式為您提供 hello 能力 tootroubleshoot 問題相關的 tooyour web 應用程式藉由查看 HTTP 記錄檔、 事件記錄檔、 處理序傾印，等等。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="5e1d9-145">您可以利用我們位於 **http://&lt;your app name>.scm.azurewebsites.net/Support** 的支援入口網站，存取所有這方面的資訊。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="5e1d9-146">hello Azure 應用程式服務支援入口網站為您提供三個個別的索引標籤 toosupport hello 三個步驟的一般疑難排解的情況下：</span><span class="sxs-lookup"><span data-stu-id="5e1d9-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="5e1d9-147">觀察目前的行為</span><span class="sxs-lookup"><span data-stu-id="5e1d9-147">Observe current behavior</span></span>
2. <span data-ttu-id="5e1d9-148">收集診斷資訊及執行 hello 內建的分析器來分析</span><span class="sxs-lookup"><span data-stu-id="5e1d9-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="5e1d9-149">減輕問題</span><span class="sxs-lookup"><span data-stu-id="5e1d9-149">Mitigate</span></span>

<span data-ttu-id="5e1d9-150">如果立即發生 hello 問題，請按一下**分析** > **診斷** > **現在診斷**toocreate 為您的診斷工作階段這將會收集 HTTP 記錄，事件檢視器記錄檔，記憶體傾印、 PHP 錯誤記錄檔和 PHP 處理報表。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="5e1d9-151">一旦 hello 資料收集時，它也會在 hello 資料執行分析，並提供 HTML 報表。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="5e1d9-152">如果您想 toodownload hello 資料，根據預設，它就會儲存在 hello D:\home\data\DaaS 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="5e1d9-153">如需有關 hello Azure 應用程式服務支援入口網站的詳細資訊，請參閱[Azure 網站的網站擴充功能的新更新 tooSupport](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="5e1d9-154">使用 hello Kudu 偵錯主控台</span><span class="sxs-lookup"><span data-stu-id="5e1d9-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="5e1d9-155">Web Apps 隨附可用於偵錯、探索、上傳檔案的偵錯主控台，以及可以取得您環境相關資訊的 JSON 端點。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="5e1d9-156">這稱為 hello *Kudu 主控台*或 hello *SCM 儀表板*web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="5e1d9-157">您可以將 toohello 連結存取這個儀表板**https://&lt;應用程式名稱 >.scm.azurewebsites.net/**。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="5e1d9-158">Kudu 提供的 hello 事項包括：</span><span class="sxs-lookup"><span data-stu-id="5e1d9-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="5e1d9-159">您的應用程式的環境設定</span><span class="sxs-lookup"><span data-stu-id="5e1d9-159">environment settings for your application</span></span>
* <span data-ttu-id="5e1d9-160">記錄檔串流</span><span class="sxs-lookup"><span data-stu-id="5e1d9-160">log stream</span></span>
* <span data-ttu-id="5e1d9-161">診斷傾印</span><span class="sxs-lookup"><span data-stu-id="5e1d9-161">diagnostic dump</span></span>
* <span data-ttu-id="5e1d9-162">您可以執行 Powershell Cmdlet 和基本 DOS 命令的偵錯主控台。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="5e1d9-163">Kudu 另一個有用功能是，如果您的應用程式會擲回第一個出現的例外狀況，您可以使用 Kudu 與 hello SysInternals 工具 Procdump toocreate 記憶體傾印。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="5e1d9-164">這些記憶體傾印是 hello 程序的快照集，並經常可協助您疑難排解您 web 應用程式更複雜的問題。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="5e1d9-165">如需有關 Kudu 可用功能的詳細資訊，請參閱 [您應該知道的 Azure 網站線上工具](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="5e1d9-166">3.減少 hello 問題</span><span class="sxs-lookup"><span data-stu-id="5e1d9-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="5e1d9-167">標尺 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e1d9-167">Scale hello web app</span></span>
<span data-ttu-id="5e1d9-168">在 Azure 應用程式服務，以增加的效能和輸送量，您可以調整 hello 小數位數，執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="5e1d9-169">向上擴充 web 應用程式牽涉到兩個相關的動作： 變更您應用程式服務計劃 tooa 較高的定價層，以及設定某些設定之後您切換 toohello 更高的定價層。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="5e1d9-170">如需有關調整的詳細資訊，請參閱 [在 Azure App Service 中調整 Web 應用程式規模](web-sites-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="5e1d9-171">此外，您可以選擇 toorun 多個執行個體上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="5e1d9-172">這不僅提供您更強大的處理能力，同時也提供您一定程度的容錯量。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="5e1d9-173">如果 hello 程序關閉上一個執行個體，hello 其他執行個體將仍然繼續服務的要求。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="5e1d9-174">您可以設定 hello toobe 手動或自動縮放比例。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="5e1d9-175">使用 AutoHeal</span><span class="sxs-lookup"><span data-stu-id="5e1d9-175">Use AutoHeal</span></span>
<span data-ttu-id="5e1d9-176">AutoHeal 回收 hello 取決於您選擇 （例如組態變更、 要求、 記憶體為基礎的限制或 hello 時間需要 tooexecute 要求） 設定您的應用程式的背景工作處理序。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="5e1d9-177">大部分的 hello 時間回收 hello 程序是 hello 最快方式 toorecover 問題。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="5e1d9-178">您永遠可以重新啟動 hello web 應用程式從直接在 hello Azure 入口網站中的，雖然 AutoHeal 會自動替您完成。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="5e1d9-179">您只需要 toodo 是 hello web 應用程式的根 web.config 中新增一些觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="5e1d9-180">請注意，這些設定會在 hello 相同方式即使您的應用程式並不是其中一個.Net。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="5e1d9-181">如需詳細資訊，請參閱 [自動修復 Azure 網站](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="5e1d9-182">重新啟動 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e1d9-182">Restart hello web app</span></span>
<span data-ttu-id="5e1d9-183">這通常是 hello 最簡單方式 toorecover 從單次發生問題。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="5e1d9-184">在 [hello [Azure 入口網站](https://portal.azure.com/)，在您的 web 應用程式] 刀鋒視窗中，您擁有 hello 選項 toostop 或重新啟動您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![重新啟動應用程式 toosolve HTTP 錯誤 502 不正確的閘道和 503 服務無法使用](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="5e1d9-186">您也可以使用 Azure Powershell 管理 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="5e1d9-187">如需詳細資訊，請參閱 [將 Azure PowerShell 與 Azure 資源管理員搭配使用](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="5e1d9-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

