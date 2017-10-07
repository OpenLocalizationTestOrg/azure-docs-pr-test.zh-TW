---
title: "在 Azure 診斷的效能計數器 aaaUse |Microsoft 文件"
description: "使用在 Azure 雲端服務或虛擬機器 toofind 瓶頸的效能計數器和調整效能。"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="be797-103">在 Azure 應用程式中建立及使用效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="be797-104">本文說明 hello 好處，以及如何 tooput 效能計數器到 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be797-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="be797-105">您可以使用它們 toocollect 資料、 找出瓶頸，並微調系統和應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="be797-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="be797-106">適用於 Windows Server、 IIS 和 ASP.NET 的效能計數器也會收集與使用 Azure web 角色、 背景工作角色和虛擬機器 toodetermine hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="be797-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="be797-107">您也可以建立和使用自訂效能計數器。</span><span class="sxs-lookup"><span data-stu-id="be797-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="be797-108">您可以採取下列方法來檢查效能計數器資料：</span><span class="sxs-lookup"><span data-stu-id="be797-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="be797-109">直接在 hello 與 hello 效能監視器 工具存取的應用程式主機上使用遠端桌面</span><span class="sxs-lookup"><span data-stu-id="be797-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="be797-110">使用 System Center Operations Manager hello Azure 管理組件</span><span class="sxs-lookup"><span data-stu-id="be797-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="be797-111">在含有其他監視工具存取 hello tooAzure 儲存體傳輸診斷資料。</span><span class="sxs-lookup"><span data-stu-id="be797-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="be797-112">如需詳細資訊，請參閱 [在 Azure 儲存體中儲存和檢視診斷資料](https://msdn.microsoft.com/library/azure/hh411534.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="be797-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="be797-113">如需有關監視的應用程式中 hello hello 效能[Azure 入口網站](http://portal.azure.com/)，請參閱[tooMonitor 雲端服務如何](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/)。</span><span class="sxs-lookup"><span data-stu-id="be797-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="be797-114">如上建立記錄和追蹤策略，以及使用診斷和其他技術 tootroubleshoot 問題的其他詳細指引和最佳化 Azure 應用程式，請參閱[開發 azure 的疑難排解最佳作法應用程式](https://msdn.microsoft.com/library/azure/hh771389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be797-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="be797-115">啟用效能計數器監視</span><span class="sxs-lookup"><span data-stu-id="be797-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="be797-116">預設不會啟用效能計數器。</span><span class="sxs-lookup"><span data-stu-id="be797-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="be797-117">您的應用程式或啟動工作必須修改 hello 預設診斷代理程式設定 tooinclude hello 特定效能計數器，您希望 toomonitor 每個角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="be797-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="be797-118">Microsoft Azure 可用的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="be797-119">Azure 提供 Windows Server、 IIS 和 ASP.NET 堆疊 hello hello 可用的效能計數器的子集。</span><span class="sxs-lookup"><span data-stu-id="be797-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="be797-120">hello 下表列出一些 Azure 應用程式特別感興趣的 hello 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="be797-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="be797-121">計數器類別：物件 (執行個體)</span><span class="sxs-lookup"><span data-stu-id="be797-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="be797-122">計數器名稱</span><span class="sxs-lookup"><span data-stu-id="be797-122">Counter Name</span></span> | <span data-ttu-id="be797-123">參考</span><span class="sxs-lookup"><span data-stu-id="be797-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be797-124">.NET CLR 例外狀況 (全域)</span><span class="sxs-lookup"><span data-stu-id="be797-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="be797-125"># Exceps Thrown / sec</span><span class="sxs-lookup"><span data-stu-id="be797-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="be797-126">例外狀況效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="be797-127">.NET CLR 記憶體 (全域)</span><span class="sxs-lookup"><span data-stu-id="be797-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="be797-128">記憶體回收中的時間 %</span><span class="sxs-lookup"><span data-stu-id="be797-128">% Time in GC</span></span> |<span data-ttu-id="be797-129">記憶體效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="be797-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="be797-130">ASP.NET</span></span> |<span data-ttu-id="be797-131">應用程式重新啟動</span><span class="sxs-lookup"><span data-stu-id="be797-131">Application Restarts</span></span> |<span data-ttu-id="be797-132">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="be797-133">ASP.NET</span></span> |<span data-ttu-id="be797-134">要求執行時間</span><span class="sxs-lookup"><span data-stu-id="be797-134">Request Execution Time</span></span> |<span data-ttu-id="be797-135">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="be797-136">ASP.NET</span></span> |<span data-ttu-id="be797-137">中斷連接的要求</span><span class="sxs-lookup"><span data-stu-id="be797-137">Requests Disconnected</span></span> |<span data-ttu-id="be797-138">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="be797-139">ASP.NET</span></span> |<span data-ttu-id="be797-140">背景工作角色處理序重新啟動</span><span class="sxs-lookup"><span data-stu-id="be797-140">Worker Process Restarts</span></span> |<span data-ttu-id="be797-141">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-142">ASP.NET 應用程式 (**總計**)</span><span class="sxs-lookup"><span data-stu-id="be797-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="be797-143">要求總數</span><span class="sxs-lookup"><span data-stu-id="be797-143">Requests Total</span></span> |<span data-ttu-id="be797-144">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-145">ASP.NET 應用程式 (**總計**)</span><span class="sxs-lookup"><span data-stu-id="be797-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="be797-146">要求/秒</span><span class="sxs-lookup"><span data-stu-id="be797-146">Requests/Sec</span></span> |<span data-ttu-id="be797-147">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="be797-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="be797-149">要求執行時間</span><span class="sxs-lookup"><span data-stu-id="be797-149">Request Execution Time</span></span> |<span data-ttu-id="be797-150">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="be797-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="be797-152">要求等候時間</span><span class="sxs-lookup"><span data-stu-id="be797-152">Request Wait Time</span></span> |<span data-ttu-id="be797-153">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="be797-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="be797-155">目前的要求</span><span class="sxs-lookup"><span data-stu-id="be797-155">Requests Current</span></span> |<span data-ttu-id="be797-156">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="be797-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="be797-158">已排入佇列的要求</span><span class="sxs-lookup"><span data-stu-id="be797-158">Requests Queued</span></span> |<span data-ttu-id="be797-159">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="be797-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="be797-161">遭拒絕的要求</span><span class="sxs-lookup"><span data-stu-id="be797-161">Requests Rejected</span></span> |<span data-ttu-id="be797-162">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-163">記憶體</span><span class="sxs-lookup"><span data-stu-id="be797-163">Memory</span></span> |<span data-ttu-id="be797-164">可用的 MB</span><span class="sxs-lookup"><span data-stu-id="be797-164">Available MBytes</span></span> |<span data-ttu-id="be797-165">記憶體效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="be797-166">記憶體</span><span class="sxs-lookup"><span data-stu-id="be797-166">Memory</span></span> |<span data-ttu-id="be797-167">認可的位元組</span><span class="sxs-lookup"><span data-stu-id="be797-167">Committed Bytes</span></span> |<span data-ttu-id="be797-168">記憶體效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="be797-169">處理器(總計)</span><span class="sxs-lookup"><span data-stu-id="be797-169">Processor(_Total)</span></span> |<span data-ttu-id="be797-170">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="be797-170">% Processor Time</span></span> |<span data-ttu-id="be797-171">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="be797-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="be797-172">TCPv4</span></span> |<span data-ttu-id="be797-173">連接失敗</span><span class="sxs-lookup"><span data-stu-id="be797-173">Connection Failures</span></span> |<span data-ttu-id="be797-174">TCP 物件</span><span class="sxs-lookup"><span data-stu-id="be797-174">TCP Object</span></span> |
| <span data-ttu-id="be797-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="be797-175">TCPv4</span></span> |<span data-ttu-id="be797-176">Connections Established</span><span class="sxs-lookup"><span data-stu-id="be797-176">Connections Established</span></span> |<span data-ttu-id="be797-177">TCP 物件</span><span class="sxs-lookup"><span data-stu-id="be797-177">TCP Object</span></span> |
| <span data-ttu-id="be797-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="be797-178">TCPv4</span></span> |<span data-ttu-id="be797-179">Connections Reset</span><span class="sxs-lookup"><span data-stu-id="be797-179">Connections Reset</span></span> |<span data-ttu-id="be797-180">TCP 物件</span><span class="sxs-lookup"><span data-stu-id="be797-180">TCP Object</span></span> |
| <span data-ttu-id="be797-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="be797-181">TCPv4</span></span> |<span data-ttu-id="be797-182">Segments Sent/sec</span><span class="sxs-lookup"><span data-stu-id="be797-182">Segments Sent/sec</span></span> |<span data-ttu-id="be797-183">TCP 物件</span><span class="sxs-lookup"><span data-stu-id="be797-183">TCP Object</span></span> |
| <span data-ttu-id="be797-184">網路介面(*)</span><span class="sxs-lookup"><span data-stu-id="be797-184">Network Interface(*)</span></span> |<span data-ttu-id="be797-185">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="be797-185">Bytes Received/sec</span></span> |<span data-ttu-id="be797-186">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="be797-186">Network Interface Object</span></span> |
| <span data-ttu-id="be797-187">網路介面(*)</span><span class="sxs-lookup"><span data-stu-id="be797-187">Network Interface(*)</span></span> |<span data-ttu-id="be797-188">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="be797-188">Bytes Sent/sec</span></span> |<span data-ttu-id="be797-189">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="be797-189">Network Interface Object</span></span> |
| <span data-ttu-id="be797-190">網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2)</span><span class="sxs-lookup"><span data-stu-id="be797-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="be797-191">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="be797-191">Bytes Received/sec</span></span> |<span data-ttu-id="be797-192">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="be797-192">Network Interface Object</span></span> |
| <span data-ttu-id="be797-193">網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2)</span><span class="sxs-lookup"><span data-stu-id="be797-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="be797-194">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="be797-194">Bytes Sent/sec</span></span> |<span data-ttu-id="be797-195">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="be797-195">Network Interface Object</span></span> |
| <span data-ttu-id="be797-196">網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2)</span><span class="sxs-lookup"><span data-stu-id="be797-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="be797-197">Bytes Total/sec</span><span class="sxs-lookup"><span data-stu-id="be797-197">Bytes Total/sec</span></span> |<span data-ttu-id="be797-198">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="be797-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="be797-199">建立並新增自訂效能計數器 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="be797-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="be797-200">Azure 有支援 toocreate 和修改自訂效能計數器針對 web 角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="be797-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="be797-201">hello 計數器可能會使用的 tootrack 並監視特定應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="be797-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="be797-202">您可以用更高權限，建立和刪除啟動工作、Web 角色或背景工作角色的自訂效能計數器類別和規範。</span><span class="sxs-lookup"><span data-stu-id="be797-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="be797-203">變更 toocustom 效能計數器的程式碼必須有更高的權限 toorun。</span><span class="sxs-lookup"><span data-stu-id="be797-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="be797-204">如果 hello 程式碼中的 web 角色或背景工作角色，hello 角色必須包含 hello 標記<Runtime executionContext="elevated" />hello ServiceDefinition.csdef 檔案中的 hello 角色 tooinitialize 正確。</span><span class="sxs-lookup"><span data-stu-id="be797-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="be797-205">您可以傳送自訂效能計數器資料 tooAzure 儲存體使用 hello 診斷代理程式。</span><span class="sxs-lookup"><span data-stu-id="be797-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="be797-206">hello Azure 程序會產生 hello 標準效能計數器資料。</span><span class="sxs-lookup"><span data-stu-id="be797-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="be797-207">自訂效能計數器資料必須由 Web 角色或背景工作角色應用程式建立。</span><span class="sxs-lookup"><span data-stu-id="be797-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="be797-208">請參閱[效能計數器型別](https://msdn.microsoft.com/library/z573042h.aspx)hello 資料類型的自訂效能計數器中可儲存的資訊。</span><span class="sxs-lookup"><span data-stu-id="be797-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="be797-209">如需在 Web 角色中建立及設定自訂效能計數器資料的範例，請參閱 [PerformanceCounters 範例](http://code.msdn.microsoft.com/azure/) 。</span><span class="sxs-lookup"><span data-stu-id="be797-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="be797-210">儲存和檢視效能計數器資料</span><span class="sxs-lookup"><span data-stu-id="be797-210">Store and view performance counter data</span></span>
<span data-ttu-id="be797-211">Azure 會快取效能計數器資料與其他診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="be797-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="be797-212">此資料是用於遠端監視執行 hello 角色執行個體時使用遠端桌面存取 tooview 工具，例如效能監視器。</span><span class="sxs-lookup"><span data-stu-id="be797-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="be797-213">toopersist hello hello 角色執行個體外部的資料，hello 診斷代理程式必須傳送 hello tooAzure 儲存資料。</span><span class="sxs-lookup"><span data-stu-id="be797-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="be797-214">hello hello 快取效能計數器資料的大小上限可以設定在 hello 診斷代理程式，或者可能是針對所有 hello 診斷資料，設定 toobe 共用限制的一部分。</span><span class="sxs-lookup"><span data-stu-id="be797-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="be797-215">如需設定 hello 緩衝區大小的詳細資訊，請參閱[OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx)和[DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be797-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="be797-216">請參閱[Azure 儲存體中檢視診斷資料及進行](https://msdn.microsoft.com/library/azure/hh411534.aspx)hello 診斷代理程式 tootransfer 資料 tooa 儲存體帳戶所設定的概觀。</span><span class="sxs-lookup"><span data-stu-id="be797-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="be797-217">記錄每個設定的效能計數器執行個體的指定的取樣率，並傳送 hello 取樣資料依排程的傳輸要求或隨選傳輸要求 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="be797-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="be797-218">可將自動傳輸的頻率排程為每分鐘一次。</span><span class="sxs-lookup"><span data-stu-id="be797-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="be797-219">傳送 hello 診斷代理程式的效能計數器資料會儲存在資料表中，WADPerformanceCountersTable，hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="be797-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="be797-220">使用標準 Azure 儲存體 API 方法即可存取和查詢此資料表。</span><span class="sxs-lookup"><span data-stu-id="be797-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="be797-221">請參閱[Microsoft Azure PerformanceCounters 範例](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9)查詢及顯示 hello WADPerformanceCountersTable 資料表中的效能計數器資料的範例。</span><span class="sxs-lookup"><span data-stu-id="be797-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="be797-222">依據 hello 診斷代理程式的傳輸頻率和佇列延遲，hello hello 儲存體帳戶中的最新效能計數器資料可能過期幾分鐘時間。</span><span class="sxs-lookup"><span data-stu-id="be797-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="be797-223">使用診斷組態檔來啟用效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="be797-224">使用下列程序 tooenable 效能計數器，Azure 應用程式中的 hello。</span><span class="sxs-lookup"><span data-stu-id="be797-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be797-225">必要條件</span><span class="sxs-lookup"><span data-stu-id="be797-225">Prerequisites</span></span>
<span data-ttu-id="be797-226">本節假設您擁有 hello 診斷監視器匯入您的應用程式，並加入 hello 診斷組態檔案 tooyour Visual Studio 方案 （在 SDK 2.4 和以下的 diagnostics.wadcfg 或 diagnostics.wadcfgx SDK 2.5 和更新版本）。</span><span class="sxs-lookup"><span data-stu-id="be797-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="be797-227">如需詳細資訊，請參閱[在 Azure 雲端服務和虛擬機器中啟用診斷](cloud-services-dotnet-diagnostics.md)中的步驟 1 和 2。</span><span class="sxs-lookup"><span data-stu-id="be797-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="be797-228">步驟 1：收集和儲存來自效能計數器的資料</span><span class="sxs-lookup"><span data-stu-id="be797-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="be797-229">加入 hello 診斷檔案 tooyour Visual Studio 方案之後，您可以設定 Azure 應用程式中的 hello 收集和儲存效能計數器資料。</span><span class="sxs-lookup"><span data-stu-id="be797-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="be797-230">這是藉由新增效能計數器 toohello 診斷檔案。</span><span class="sxs-lookup"><span data-stu-id="be797-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="be797-231">Hello 執行個體上，會先收集診斷資料，包括效能計數器。</span><span class="sxs-lookup"><span data-stu-id="be797-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="be797-232">hello 資料則保存的 toohello WADPerformanceCountersTable 資料表 hello Azure 資料表服務中，讓您將也需要 toospecify hello 應用程式中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="be797-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="be797-233">如果您要在 hello 計算模擬器在本機測試您的應用程式，您也可以儲存診斷資料在本機中 hello 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="be797-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="be797-234">儲存診斷資料之前，您必須先前往 toohello [Azure 入口網站](http://portal.azure.com/)並建立傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="be797-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="be797-235">最佳作法是 toolocate 儲存體帳戶中的 hello Azure 應用程式的相同地理位置。</span><span class="sxs-lookup"><span data-stu-id="be797-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="be797-236">所保留的 hello Azure 應用程式和儲存體帳戶會在 hello 相同的地理位置，您避免支付外部頻寬費用並降低延遲。</span><span class="sxs-lookup"><span data-stu-id="be797-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="be797-237">新增效能計數器 toohello 診斷檔案</span><span class="sxs-lookup"><span data-stu-id="be797-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="be797-238">有許多計數器可供您使用。</span><span class="sxs-lookup"><span data-stu-id="be797-238">There are many counters you can use.</span></span> <span data-ttu-id="be797-239">hello 下列範例示範為 web 和背景工作角色監視建議的數個效能計數器。</span><span class="sxs-lookup"><span data-stu-id="be797-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="be797-240">開啟 hello 診斷檔案 （在 SDK 2.4 和以下版本的 diagnostics.wadcfg 或 diagnostics.wadcfgx SDK 2.5 和更新版本），並新增下列 toohello DiagnosticMonitorConfiguration 元素 hello:</span><span class="sxs-lookup"><span data-stu-id="be797-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="be797-241">hello bufferQuotaInMB 屬性，指定 hello 供 hello 資料集合類型 （Azure 記錄檔、 IIS 記錄檔等） 的檔案系統儲存體數量上限。</span><span class="sxs-lookup"><span data-stu-id="be797-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="be797-242">hello 預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="be797-242">hello default is 0.</span></span> <span data-ttu-id="be797-243">當達到 hello 配額時，加入新的資料時，會刪除 hello 最舊的資料。</span><span class="sxs-lookup"><span data-stu-id="be797-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="be797-244">所有的 hello bufferQuotaInMB 屬性 hello 總和必須大於 hello hello OverallQuotaInMB 屬性值。</span><span class="sxs-lookup"><span data-stu-id="be797-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="be797-245">決定多少儲存空間必須為 hello 收集診斷資料的更詳細討論，請參閱 < 設定 WAD 」 一節的 hello[開發 Azure 應用程式的疑難排解最佳作法](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be797-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="be797-246">hello scheduledTransferPeriod 屬性，會指定 hello 資料傳輸的排程間隔，無條件進位 toohello 最接近的分鐘。</span><span class="sxs-lookup"><span data-stu-id="be797-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="be797-247">在 hello 遵循範例，它會設定 tooPT30M （30 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="be797-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="be797-248">設定 hello 傳輸週期 tooa 小的值，例如 1 分鐘，將會對在生產環境中的應用程式的效能造成負面影響，但可以是適合用來查看快速使用，當您正在測試的診斷。</span><span class="sxs-lookup"><span data-stu-id="be797-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="be797-249">hello 排程的傳輸期間應該夠小，tooensure 診斷資料不是覆寫在 hello 的執行個體，但夠大，它不會影響應用程式的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="be797-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="be797-250">hello counterSpecifier 屬性會指定 hello 效能計數器 toocollect。</span><span class="sxs-lookup"><span data-stu-id="be797-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="be797-251">hello sampleRate 屬性會指定 hello 的 hello 效能計數器應該取樣，在此情況下 30 秒的速率。</span><span class="sxs-lookup"><span data-stu-id="be797-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="be797-252">一旦您已經新增 hello 效能計數器的 toocollect，儲存變更 toohello 診斷檔案。</span><span class="sxs-lookup"><span data-stu-id="be797-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="be797-253">接下來，您需要 hello 診斷資料會保存到 toospecify hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="be797-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="be797-254">指定 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="be797-254">Specify hello storage account</span></span>
<span data-ttu-id="be797-255">您的診斷資訊 tooyour Azure 儲存體帳戶，您必須指定的 toopersist 您服務組態檔 (ServiceConfiguration.cscfg) 中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="be797-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="be797-256">Azure SDK 2.5，則可以指定 hello diagnostics.wadcfgx 檔案中的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="be797-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="be797-257">這些說明僅適用於 tooAzure SDK 2.4 和以下。</span><span class="sxs-lookup"><span data-stu-id="be797-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="be797-258">Azure SDK 2.5，則可以指定 hello diagnostics.wadcfgx 檔案中的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="be797-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="be797-259">tooset hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="be797-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="be797-260">開啟您的儲存體使用您慣用的文字編輯器和設定 hello 連接字串 hello ServiceConfiguration.Cloud.cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="be797-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="be797-261">hello *AccountName*和*AccountKey*值中找到 hello hello 儲存體帳戶儀表板中，在存取金鑰 底下的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="be797-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="be797-262">儲存 hello ServiceConfiguration.Cloud.cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="be797-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="be797-263">開啟 hello ServiceConfiguration.Local.cscfg 檔案，並確認 UseDevelopmentStorage 設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="be797-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="be797-264">既然 hello 連接字串已設定，您的應用程式將會在您的應用程式部署時保存診斷資料 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="be797-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="be797-265">儲存並建置您的專案，然後部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="be797-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="be797-266">步驟 2：(選擇性) 建立自訂效能計數器</span><span class="sxs-lookup"><span data-stu-id="be797-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="be797-267">此外 toohello 預先定義的效能計數器，您可以加入您自己的自訂效能計數器 toomonitor web 或背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="be797-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="be797-268">自訂效能計數器可能會使用的 tootrack 並監視特定應用程式的行為，可建立或刪除中啟動工作、 web 角色或背景工作角色，以更高權限。</span><span class="sxs-lookup"><span data-stu-id="be797-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="be797-269">hello Azure 診斷代理程式重新整理 hello 效能計數器組態 hello.wadcfg 檔案從一分鐘之後啟動。</span><span class="sxs-lookup"><span data-stu-id="be797-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="be797-270">如果您建立自訂效能計數器 hello OnStart 方法中，啟動工作花費超過一分鐘 tooexecute 自訂效能計數器將尚未建立時 hello Azure 診斷代理程式會嘗試 tooload 它們。</span><span class="sxs-lookup"><span data-stu-id="be797-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="be797-271">在此情況下，您會看到 Azure 診斷正確地擷取自訂效能計數器以外的所有診斷資料。</span><span class="sxs-lookup"><span data-stu-id="be797-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="be797-272">tooresolve 這個問題，請在啟動工作中建立 hello 效能計數器，或移動啟動工作的某些工作 toohello OnStart 方法之後建立 hello 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="be797-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="be797-273">執行下列步驟 toocreate 簡單自訂效能計數器名為"\MyCustomCounterCategory\MyButton1Counter"hello:</span><span class="sxs-lookup"><span data-stu-id="be797-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="be797-274">開啟 hello 服務定義檔 (CSDEF) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be797-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="be797-275">加入 hello Runtime 項目 toohello WebRole 或 WorkerRole 元素 tooallow 執行具有提高權限：</span><span class="sxs-lookup"><span data-stu-id="be797-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="be797-276">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="be797-276">Save hello file.</span></span>
4. <span data-ttu-id="be797-277">開啟 hello 診斷檔案 （在 SDK 2.4 和以下版本的 diagnostics.wadcfg 或 diagnostics.wadcfgx SDK 2.5 和更新版本），並新增下列 toohello DiagnosticMonitorConfiguration hello</span><span class="sxs-lookup"><span data-stu-id="be797-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="be797-278">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="be797-278">Save hello file.</span></span>
6. <span data-ttu-id="be797-279">建立您的角色中的 hello OnStart 方法中的 hello 自訂效能計數器分類之前叫用基底。OnStart。</span><span class="sxs-lookup"><span data-stu-id="be797-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="be797-280">hello 下列 C# 範例會建立自訂的類別目錄中，如果不存在：</span><span class="sxs-lookup"><span data-stu-id="be797-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="be797-281">更新您的應用程式中的 hello 計數器。</span><span class="sxs-lookup"><span data-stu-id="be797-281">Update hello counters within your application.</span></span> <span data-ttu-id="be797-282">下列範例中的 hello 更新 Button1_Click 事件中的自訂效能計數器：</span><span class="sxs-lookup"><span data-stu-id="be797-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="be797-283">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="be797-283">Save hello file.</span></span>  

<span data-ttu-id="be797-284">現在將由 hello Azure 診斷監視器收集自訂效能計數器資料。</span><span class="sxs-lookup"><span data-stu-id="be797-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="be797-285">步驟 3：查詢效能計數器資料</span><span class="sxs-lookup"><span data-stu-id="be797-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="be797-286">一旦應用程式部署和執行，hello 診斷監視器會開始收集效能計數器和保存該資料 tooAzure 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="be797-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="be797-287">您在 Visual Studio 中，使用伺服器總管之類的工具[Azure 儲存體總管](http://azurestorageexplorer.codeplex.com/)，或[Azure 診斷管理員](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx)cerebrata tooview hello 效能計數器 hello 中的資料WADPerformanceCountersTable 資料表。</span><span class="sxs-lookup"><span data-stu-id="be797-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="be797-288">您可以也以程式設計方式查詢 hello 資料表服務使用[C#](../cosmos-db/table-storage-how-to-use-dotnet.md)， [Java](../cosmos-db/table-storage-how-to-use-java.md)， [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md)， [Python](../cosmos-db/table-storage-how-to-use-python.md)， [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md)，或[PHP](../cosmos-db/table-storage-how-to-use-php.md)。</span><span class="sxs-lookup"><span data-stu-id="be797-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="be797-289">hello 下列 C# 範例會顯示針對 hello WADPerformanceCountersTable 資料表的基本查詢並儲存 hello 診斷資料 tooa CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="be797-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="be797-290">一旦 hello 效能計數器儲存 tooa CSV 檔案，您可以使用 hello 繪圖 Microsoft Excel 或某些其他工具 toovisualize hello 資料中的功能。</span><span class="sxs-lookup"><span data-stu-id="be797-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="be797-291">為確定 tooadd 參考 tooMicrosoft.WindowsAzure.Storage.dll，隨附於 hello Azure SDK for.NET 年 10 月 2012年及更新版本。</span><span class="sxs-lookup"><span data-stu-id="be797-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="be797-292">hello 組件是已安裝的 toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET sdk\version-num\ref\ 目錄。</span><span class="sxs-lookup"><span data-stu-id="be797-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="be797-293">實體對應 tooC # 物件使用自訂的類別衍生自**TableEntity**。</span><span class="sxs-lookup"><span data-stu-id="be797-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="be797-294">hello 下列程式碼會定義實體類別，代表效能計數器中 hello **WADPerformanceCountersTable**資料表。</span><span class="sxs-lookup"><span data-stu-id="be797-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="be797-295">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be797-295">Next Steps</span></span>
[<span data-ttu-id="be797-296">檢視有關 Azure 診斷的其他文章</span><span class="sxs-lookup"><span data-stu-id="be797-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
