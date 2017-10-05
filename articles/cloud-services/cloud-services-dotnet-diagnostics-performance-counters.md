---
title: "在 Azure 診斷中使用效能計數器 | Microsoft Docs"
description: "在 Azure 雲端服務或虛擬機器中使用效能計數器來找出瓶頸和調整效能。"
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
ms.openlocfilehash: 2cf765cb034725199127c547a9b8b997a4a6089c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="4fe12-103">在 Azure 應用程式中建立及使用效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="4fe12-104">本文說明效能計數器的優點，以及如何將效能計數器放入 Azure 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="4fe12-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="4fe12-105">您可以使用它們來收集資料、找出瓶頸，以及調整系統和應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="4fe12-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="4fe12-106">適用於 Windows Server、IIS 和 ASP.NET 的效能計數器也可用來收集資料，以判斷 Azure Web 角色、背景工作角色和虛擬機器的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="4fe12-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="4fe12-107">您也可以建立和使用自訂效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="4fe12-108">您可以採取下列方法來檢查效能計數器資料：</span><span class="sxs-lookup"><span data-stu-id="4fe12-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="4fe12-109">直接在應用程式主機上，使用透過遠端桌面存取的效能監視器工具</span><span class="sxs-lookup"><span data-stu-id="4fe12-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="4fe12-110">透過使用 Azure Management Pack 的 System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="4fe12-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="4fe12-111">透過其他監視工具，存取已傳輸至 Azure 儲存體的診斷資料。</span><span class="sxs-lookup"><span data-stu-id="4fe12-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="4fe12-112">如需詳細資訊，請參閱 [在 Azure 儲存體中儲存和檢視診斷資料](https://msdn.microsoft.com/library/azure/hh411534.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="4fe12-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="4fe12-113">如需在 [Azure 入口網站](http://portal.azure.com/)中監視應用程式效能的詳細資訊，請參閱[如何監視雲端服務](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/)。</span><span class="sxs-lookup"><span data-stu-id="4fe12-113">For more information on monitoring the performance of your application in the [Azure portal](http://portal.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="4fe12-114">如需建立記錄及追蹤策略、使用診斷和其他技術進行疑難排解，以及將 Azure 應用程式最佳化的其他深入指引，請參閱 [開發 Azure 應用程式的疑難排解最佳作法](https://msdn.microsoft.com/library/azure/hh771389.aspx)(英文)。</span><span class="sxs-lookup"><span data-stu-id="4fe12-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="4fe12-115">啟用效能計數器監視</span><span class="sxs-lookup"><span data-stu-id="4fe12-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="4fe12-116">預設不會啟用效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="4fe12-117">您的應用程式或啟動工作必須修改預設診斷代理程式組態，以納入您想要針對每個角色執行個體監視的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="4fe12-118">Microsoft Azure 可用的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="4fe12-119">Azure 為 Windows Server、IIS 和 ASP.NET 堆疊提供了一小組可用的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="4fe12-120">下表列出一些對 Azure 應用程式特別實用的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="4fe12-121">計數器類別：物件 (執行個體)</span><span class="sxs-lookup"><span data-stu-id="4fe12-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="4fe12-122">計數器名稱</span><span class="sxs-lookup"><span data-stu-id="4fe12-122">Counter Name</span></span> | <span data-ttu-id="4fe12-123">參考</span><span class="sxs-lookup"><span data-stu-id="4fe12-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4fe12-124">.NET CLR 例外狀況 (全域)</span><span class="sxs-lookup"><span data-stu-id="4fe12-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="4fe12-125"># Exceps Thrown / sec</span><span class="sxs-lookup"><span data-stu-id="4fe12-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="4fe12-126">例外狀況效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="4fe12-127">.NET CLR 記憶體 (全域)</span><span class="sxs-lookup"><span data-stu-id="4fe12-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="4fe12-128">記憶體回收中的時間 %</span><span class="sxs-lookup"><span data-stu-id="4fe12-128">% Time in GC</span></span> |<span data-ttu-id="4fe12-129">記憶體效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="4fe12-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4fe12-130">ASP.NET</span></span> |<span data-ttu-id="4fe12-131">應用程式重新啟動</span><span class="sxs-lookup"><span data-stu-id="4fe12-131">Application Restarts</span></span> |<span data-ttu-id="4fe12-132">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4fe12-133">ASP.NET</span></span> |<span data-ttu-id="4fe12-134">要求執行時間</span><span class="sxs-lookup"><span data-stu-id="4fe12-134">Request Execution Time</span></span> |<span data-ttu-id="4fe12-135">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4fe12-136">ASP.NET</span></span> |<span data-ttu-id="4fe12-137">中斷連接的要求</span><span class="sxs-lookup"><span data-stu-id="4fe12-137">Requests Disconnected</span></span> |<span data-ttu-id="4fe12-138">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4fe12-139">ASP.NET</span></span> |<span data-ttu-id="4fe12-140">背景工作角色處理序重新啟動</span><span class="sxs-lookup"><span data-stu-id="4fe12-140">Worker Process Restarts</span></span> |<span data-ttu-id="4fe12-141">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-142">ASP.NET 應用程式 (**總計**)</span><span class="sxs-lookup"><span data-stu-id="4fe12-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="4fe12-143">要求總數</span><span class="sxs-lookup"><span data-stu-id="4fe12-143">Requests Total</span></span> |<span data-ttu-id="4fe12-144">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-145">ASP.NET 應用程式 (**總計**)</span><span class="sxs-lookup"><span data-stu-id="4fe12-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="4fe12-146">要求/秒</span><span class="sxs-lookup"><span data-stu-id="4fe12-146">Requests/Sec</span></span> |<span data-ttu-id="4fe12-147">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="4fe12-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="4fe12-149">要求執行時間</span><span class="sxs-lookup"><span data-stu-id="4fe12-149">Request Execution Time</span></span> |<span data-ttu-id="4fe12-150">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="4fe12-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="4fe12-152">要求等候時間</span><span class="sxs-lookup"><span data-stu-id="4fe12-152">Request Wait Time</span></span> |<span data-ttu-id="4fe12-153">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="4fe12-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="4fe12-155">目前的要求</span><span class="sxs-lookup"><span data-stu-id="4fe12-155">Requests Current</span></span> |<span data-ttu-id="4fe12-156">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="4fe12-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="4fe12-158">已排入佇列的要求</span><span class="sxs-lookup"><span data-stu-id="4fe12-158">Requests Queued</span></span> |<span data-ttu-id="4fe12-159">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="4fe12-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="4fe12-161">遭拒絕的要求</span><span class="sxs-lookup"><span data-stu-id="4fe12-161">Requests Rejected</span></span> |<span data-ttu-id="4fe12-162">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-163">記憶體</span><span class="sxs-lookup"><span data-stu-id="4fe12-163">Memory</span></span> |<span data-ttu-id="4fe12-164">可用的 MB</span><span class="sxs-lookup"><span data-stu-id="4fe12-164">Available MBytes</span></span> |<span data-ttu-id="4fe12-165">記憶體效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="4fe12-166">記憶體</span><span class="sxs-lookup"><span data-stu-id="4fe12-166">Memory</span></span> |<span data-ttu-id="4fe12-167">認可的位元組</span><span class="sxs-lookup"><span data-stu-id="4fe12-167">Committed Bytes</span></span> |<span data-ttu-id="4fe12-168">記憶體效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="4fe12-169">處理器(總計)</span><span class="sxs-lookup"><span data-stu-id="4fe12-169">Processor(_Total)</span></span> |<span data-ttu-id="4fe12-170">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="4fe12-170">% Processor Time</span></span> |<span data-ttu-id="4fe12-171">ASP.NET 的效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="4fe12-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="4fe12-172">TCPv4</span></span> |<span data-ttu-id="4fe12-173">連接失敗</span><span class="sxs-lookup"><span data-stu-id="4fe12-173">Connection Failures</span></span> |<span data-ttu-id="4fe12-174">TCP 物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-174">TCP Object</span></span> |
| <span data-ttu-id="4fe12-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="4fe12-175">TCPv4</span></span> |<span data-ttu-id="4fe12-176">Connections Established</span><span class="sxs-lookup"><span data-stu-id="4fe12-176">Connections Established</span></span> |<span data-ttu-id="4fe12-177">TCP 物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-177">TCP Object</span></span> |
| <span data-ttu-id="4fe12-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="4fe12-178">TCPv4</span></span> |<span data-ttu-id="4fe12-179">Connections Reset</span><span class="sxs-lookup"><span data-stu-id="4fe12-179">Connections Reset</span></span> |<span data-ttu-id="4fe12-180">TCP 物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-180">TCP Object</span></span> |
| <span data-ttu-id="4fe12-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="4fe12-181">TCPv4</span></span> |<span data-ttu-id="4fe12-182">Segments Sent/sec</span><span class="sxs-lookup"><span data-stu-id="4fe12-182">Segments Sent/sec</span></span> |<span data-ttu-id="4fe12-183">TCP 物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-183">TCP Object</span></span> |
| <span data-ttu-id="4fe12-184">網路介面(*)</span><span class="sxs-lookup"><span data-stu-id="4fe12-184">Network Interface(*)</span></span> |<span data-ttu-id="4fe12-185">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="4fe12-185">Bytes Received/sec</span></span> |<span data-ttu-id="4fe12-186">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-186">Network Interface Object</span></span> |
| <span data-ttu-id="4fe12-187">網路介面(*)</span><span class="sxs-lookup"><span data-stu-id="4fe12-187">Network Interface(*)</span></span> |<span data-ttu-id="4fe12-188">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="4fe12-188">Bytes Sent/sec</span></span> |<span data-ttu-id="4fe12-189">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-189">Network Interface Object</span></span> |
| <span data-ttu-id="4fe12-190">網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2)</span><span class="sxs-lookup"><span data-stu-id="4fe12-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="4fe12-191">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="4fe12-191">Bytes Received/sec</span></span> |<span data-ttu-id="4fe12-192">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-192">Network Interface Object</span></span> |
| <span data-ttu-id="4fe12-193">網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2)</span><span class="sxs-lookup"><span data-stu-id="4fe12-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="4fe12-194">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="4fe12-194">Bytes Sent/sec</span></span> |<span data-ttu-id="4fe12-195">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-195">Network Interface Object</span></span> |
| <span data-ttu-id="4fe12-196">網路介面 (Microsoft 虛擬機器匯流排網路介面卡 _2)</span><span class="sxs-lookup"><span data-stu-id="4fe12-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="4fe12-197">Bytes Total/sec</span><span class="sxs-lookup"><span data-stu-id="4fe12-197">Bytes Total/sec</span></span> |<span data-ttu-id="4fe12-198">網路介面物件</span><span class="sxs-lookup"><span data-stu-id="4fe12-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="4fe12-199">建立自訂效能計數器並加入您的應用程式中</span><span class="sxs-lookup"><span data-stu-id="4fe12-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="4fe12-200">Azure 支援建立和修改 Web 角色和背景工作角色的自訂效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="4fe12-201">計數器可用來追蹤和監視應用程式特有的行為。</span><span class="sxs-lookup"><span data-stu-id="4fe12-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="4fe12-202">您可以用更高權限，建立和刪除啟動工作、Web 角色或背景工作角色的自訂效能計數器類別和規範。</span><span class="sxs-lookup"><span data-stu-id="4fe12-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="4fe12-203">必須擁有更高權限，才能執行對自訂效能計數器進行變更的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4fe12-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="4fe12-204">如果程式碼屬於 Web 角色或背景工作角色，角色必須在 ServiceDefinition.csdef 檔案中包含標記 <Runtime executionContext="elevated" /> ，才能正確地初始化角色。</span><span class="sxs-lookup"><span data-stu-id="4fe12-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
>
>

<span data-ttu-id="4fe12-205">您可以使用診斷代理程式，將自訂效能計數器資料傳送到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4fe12-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="4fe12-206">標準效能計數器資料是由 Azure 處理序產生。</span><span class="sxs-lookup"><span data-stu-id="4fe12-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="4fe12-207">自訂效能計數器資料必須由 Web 角色或背景工作角色應用程式建立。</span><span class="sxs-lookup"><span data-stu-id="4fe12-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="4fe12-208">如需自訂效能計數器可儲存的資料類型的相關資訊，請參閱 [效能計數器類型](https://msdn.microsoft.com/library/z573042h.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="4fe12-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="4fe12-209">如需在 Web 角色中建立及設定自訂效能計數器資料的範例，請參閱 [PerformanceCounters 範例](http://code.msdn.microsoft.com/azure/) 。</span><span class="sxs-lookup"><span data-stu-id="4fe12-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="4fe12-210">儲存和檢視效能計數器資料</span><span class="sxs-lookup"><span data-stu-id="4fe12-210">Store and view performance counter data</span></span>
<span data-ttu-id="4fe12-211">Azure 會快取效能計數器資料與其他診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="4fe12-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="4fe12-212">當角色執行個體正在執行時，使用遠端桌面存取來檢視效能監視器等工具，此資料即可供遠端監視。</span><span class="sxs-lookup"><span data-stu-id="4fe12-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="4fe12-213">若要在角色執行個體外部保存資料，則診斷代理程式必須將資料傳輸到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4fe12-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="4fe12-214">在診斷代理程式中可以設定快取的效能計數器資料的大小限制，或也可以將它設定為所有診斷資料之共用限制的一部分。</span><span class="sxs-lookup"><span data-stu-id="4fe12-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="4fe12-215">如需有關設定緩衝區大小的詳細資訊，請參閱 [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) 和 [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4fe12-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="4fe12-216">如需設定診斷代理程式以將資料傳輸到儲存體帳戶的概觀，請參閱 [在 Azure 儲存體中儲存和檢視診斷資料](https://msdn.microsoft.com/library/azure/hh411534.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="4fe12-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="4fe12-217">每個設定的效能計數器執行個體都會以指定的取樣速率進行記錄，而取樣的資料會經由排程的傳輸要求或隨選傳輸要求傳輸到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4fe12-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="4fe12-218">可將自動傳輸的頻率排程為每分鐘一次。</span><span class="sxs-lookup"><span data-stu-id="4fe12-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="4fe12-219">診斷代理程式所傳輸的效能計數器資料會儲存在儲存體帳戶的 WADPerformanceCountersTable 資料表中。</span><span class="sxs-lookup"><span data-stu-id="4fe12-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="4fe12-220">使用標準 Azure 儲存體 API 方法即可存取和查詢此資料表。</span><span class="sxs-lookup"><span data-stu-id="4fe12-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="4fe12-221">如需查詢及顯示 WADPerformanceCountersTable 資料表中效能計數器資料的範例，請參閱 [Microsoft Azure PerformanceCounters 範例](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) 。</span><span class="sxs-lookup"><span data-stu-id="4fe12-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="4fe12-222">視診斷代理程式的傳輸頻率和佇列延遲研定，儲存體帳戶中的最新效能計數器資料可能會過期幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="4fe12-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="4fe12-223">使用診斷組態檔來啟用效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="4fe12-224">使用下列程序在 Azure 應用程式中啟用效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fe12-225">必要條件</span><span class="sxs-lookup"><span data-stu-id="4fe12-225">Prerequisites</span></span>
<span data-ttu-id="4fe12-226">本節假設您已將診斷監視器匯入應用程式中，並已將診斷組態檔加入 Visual Studio 方案中 (SDK 2.4 和以下版本為 diagnostics.wadcfg，而 SDK 2.5 和以上版本為 diagnostics.wadcfgx)。</span><span class="sxs-lookup"><span data-stu-id="4fe12-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="4fe12-227">如需詳細資訊，請參閱[在 Azure 雲端服務和虛擬機器中啟用診斷](cloud-services-dotnet-diagnostics.md)中的步驟 1 和 2。</span><span class="sxs-lookup"><span data-stu-id="4fe12-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="4fe12-228">步驟 1：收集和儲存來自效能計數器的資料</span><span class="sxs-lookup"><span data-stu-id="4fe12-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="4fe12-229">將診斷檔案加入 Visual Studio 方案中後，您即可在 Azure 應用程式中進行效能計數器資料的收集和儲存設定。</span><span class="sxs-lookup"><span data-stu-id="4fe12-229">After you have added the diagnostics file to your Visual Studio solution, you can configure the collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="4fe12-230">將效能計數器加入診斷檔案中，即可完成此動作。</span><span class="sxs-lookup"><span data-stu-id="4fe12-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="4fe12-231">首先會在執行個體上收集診斷資料，包括效能計數器在內。</span><span class="sxs-lookup"><span data-stu-id="4fe12-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="4fe12-232">這項資料後續會持續存留在 Azure 資料表服務的 WADPerformanceCountersTable 資料表中，因此您也須在應用程式中指定儲存帳號。</span><span class="sxs-lookup"><span data-stu-id="4fe12-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="4fe12-233">如果您要使用計算模擬器在本機中測試應用程式，您也可以在儲存模擬器中本機儲存診斷資料。</span><span class="sxs-lookup"><span data-stu-id="4fe12-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="4fe12-234">在儲存診斷資料之前，您必須先移至 [Azure 入口網站](http://portal.azure.com/)，並建立傳統儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4fe12-234">Before you store diagnostics data, you must first go to the [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="4fe12-235">最佳做法是找出與您的 Azure 應用程式位在相同地理位置的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4fe12-235">A best practice is to locate your storage account in the same geo-location as your Azure application.</span></span> <span data-ttu-id="4fe12-236">將 Azure 應用程式和儲存體帳戶保存在相同的地理位置，可以避免支付外部頻寬成本並減少延遲。</span><span class="sxs-lookup"><span data-stu-id="4fe12-236">By keeping the Azure application and storage account are in the same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="4fe12-237">將效能計數器加入診斷檔案中</span><span class="sxs-lookup"><span data-stu-id="4fe12-237">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="4fe12-238">有許多計數器可供您使用。</span><span class="sxs-lookup"><span data-stu-id="4fe12-238">There are many counters you can use.</span></span> <span data-ttu-id="4fe12-239">下列範例說明幾個建議用於 Web 和背景工作角色監視的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-239">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="4fe12-240">開啟診斷檔案 (SDK 2.4 和以下版本為 diagnostics.wadcfg，而 SDK 2.5 和以上版本為 diagnostics.wadcfgx)，並將下列內容加入 DiagnosticMonitorConfiguration 元素中：</span><span class="sxs-lookup"><span data-stu-id="4fe12-240">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
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

<span data-ttu-id="4fe12-241">bufferQuotaInMB 屬性會指定可用於資料收集類型 (Azure 記錄、IIS 記錄等) 的檔案系統儲存體數量上限。</span><span class="sxs-lookup"><span data-stu-id="4fe12-241">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="4fe12-242">預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="4fe12-242">The default is 0.</span></span> <span data-ttu-id="4fe12-243">到達此配額時，即會在新增新資料時刪除最舊的資料。</span><span class="sxs-lookup"><span data-stu-id="4fe12-243">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="4fe12-244">所有 bufferQuotaInMB 屬性 (property) 的總和必須大於 OverallQuotaInMB 屬性 (attribute) 的值。</span><span class="sxs-lookup"><span data-stu-id="4fe12-244">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="4fe12-245">如需判斷收集診斷資料將需要多少儲存體的詳細討論，請參閱 [開發 Azure 應用程式的疑難排解最佳作法](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx)(英文) 中的「設定 WAD」一節。</span><span class="sxs-lookup"><span data-stu-id="4fe12-245">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="4fe12-246">scheduledTransferPeriod 屬性會指定排程的資料傳輸所採用的間隔 (四捨五入至最接近的分鐘)。</span><span class="sxs-lookup"><span data-stu-id="4fe12-246">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="4fe12-247">下列範例將此值設為 PT30M (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="4fe12-247">In the following examples, it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="4fe12-248">將傳輸期間設為較小的值 (例如 1 分鐘)，將對生產環境中的應用程式效能造成不良影響，但在執行測試時可能有助於診斷的快速運作。</span><span class="sxs-lookup"><span data-stu-id="4fe12-248">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="4fe12-249">排程的傳輸期間應大小適中，以確保執行個體上的診斷資料不會被覆寫，同時不會對應用程式的效能造成影響。</span><span class="sxs-lookup"><span data-stu-id="4fe12-249">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="4fe12-250">counterSpecifier 屬性會指定要收集的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-250">The counterSpecifier attribute specifies the performance counter to collect.</span></span> <span data-ttu-id="4fe12-251">sampleRate 屬性會指定對效能計數器取樣的頻率，在本例中為 30 秒。</span><span class="sxs-lookup"><span data-stu-id="4fe12-251">The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="4fe12-252">加入您要收集的效能計數器後，請將變更儲存至診斷檔案。</span><span class="sxs-lookup"><span data-stu-id="4fe12-252">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="4fe12-253">接著，您必須指定將持續保存診斷資料的儲存帳號。</span><span class="sxs-lookup"><span data-stu-id="4fe12-253">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="4fe12-254">指定儲存帳號</span><span class="sxs-lookup"><span data-stu-id="4fe12-254">Specify the storage account</span></span>
<span data-ttu-id="4fe12-255">若要讓您的診斷資訊持續存留於 Azure 儲存帳號中，您必須在服務組態檔 (ServiceConfiguration.cscfg) 中指定連接字串。</span><span class="sxs-lookup"><span data-stu-id="4fe12-255">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="4fe12-256">在 Azure SDK 2.5 中，儲存體帳戶可在 diagnostics.wadcfgx 檔案中指定。</span><span class="sxs-lookup"><span data-stu-id="4fe12-256">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="4fe12-257">這些指示只會套用至 Azure SDK 2.4 和以下版本。</span><span class="sxs-lookup"><span data-stu-id="4fe12-257">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="4fe12-258">在 Azure SDK 2.5 中，儲存體帳戶可在 diagnostics.wadcfgx 檔案中指定。</span><span class="sxs-lookup"><span data-stu-id="4fe12-258">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="4fe12-259">若要設定連接字串：</span><span class="sxs-lookup"><span data-stu-id="4fe12-259">To set the connection strings:</span></span>

1. <span data-ttu-id="4fe12-260">使用您慣用的文字編輯器開啟 ServiceConfiguration.Cloud.cscfg 檔案，然後設定儲存體的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4fe12-260">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="4fe12-261">*AccountName* 和 *AccountKey* 值可在 Azure 入口網站中儲存體帳戶儀表板的 [存取金鑰] 底下找到。</span><span class="sxs-lookup"><span data-stu-id="4fe12-261">The *AccountName* and *AccountKey* values are found in the Azure portal in the storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="4fe12-262">儲存 ServiceConfiguration.Cloud.cscfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="4fe12-262">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="4fe12-263">開啟 ServiceConfiguration.Local.cscfg 檔案，驗證 UseDevelopmentStorage 是否設為 true。</span><span class="sxs-lookup"><span data-stu-id="4fe12-263">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="4fe12-264">現在，連接字串已設定，您的應用程式將可在部署時，將診斷資料持續存留至您的儲存帳號中。</span><span class="sxs-lookup"><span data-stu-id="4fe12-264">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="4fe12-265">儲存並建置您的專案，然後部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="4fe12-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="4fe12-266">步驟 2：(選擇性) 建立自訂效能計數器</span><span class="sxs-lookup"><span data-stu-id="4fe12-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="4fe12-267">除了預先定義的效能計數器以外，您也可以新增自訂效能計數器，以監視 Web 或背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="4fe12-267">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="4fe12-268">自訂效能計數器可用來追蹤及監視應用程式特定行為，並可藉由提高的權限在啟動工作、Web 角色或背景工作角色中建立或刪除。</span><span class="sxs-lookup"><span data-stu-id="4fe12-268">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="4fe12-269">Azure 診斷代理程式會在啟動一分鐘後從 .wadcfg 檔案重新整理效能計數器組態。</span><span class="sxs-lookup"><span data-stu-id="4fe12-269">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="4fe12-270">如果您在 OnStart 方法中建立自訂效能計數器，而且您的啟動工作在一分鐘以後執行，則您的自訂效能計數器在 Azure 診斷代理程式嘗試載入時尚未建立。</span><span class="sxs-lookup"><span data-stu-id="4fe12-270">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="4fe12-271">在此情況下，您會看到 Azure 診斷正確地擷取自訂效能計數器以外的所有診斷資料。</span><span class="sxs-lookup"><span data-stu-id="4fe12-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="4fe12-272">若要解決此問題，請在啟動工作中建立效能計數器，或在建立效能計數器之後，將部分啟動工作移到 OnStart 方法。</span><span class="sxs-lookup"><span data-stu-id="4fe12-272">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="4fe12-273">執行下列步驟，可建立名為 "\MyCustomCounterCategory\MyButton1Counter" 的簡易自訂效能計數器：</span><span class="sxs-lookup"><span data-stu-id="4fe12-273">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="4fe12-274">開啟應用程式的服務定義檔 (CSDEF)。</span><span class="sxs-lookup"><span data-stu-id="4fe12-274">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="4fe12-275">將 Runtime 元素新增至 WebRole 或 WorkerRole 元素，使其可在提升的權限下執行：</span><span class="sxs-lookup"><span data-stu-id="4fe12-275">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="4fe12-276">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="4fe12-276">Save the file.</span></span>
4. <span data-ttu-id="4fe12-277">開啟診斷檔案 (SDK 2.4 和以下版本為 diagnostics.wadcfg，而 SDK 2.5 和以上版本為 diagnostics.wadcfgx)，並將下列內容加入 DiagnosticMonitorConfiguration 中</span><span class="sxs-lookup"><span data-stu-id="4fe12-277">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="4fe12-278">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="4fe12-278">Save the file.</span></span>
6. <span data-ttu-id="4fe12-279">在您角色的 OnStart 方法中建立自訂效能計數器類別，然後叫用 base.OnStart。</span><span class="sxs-lookup"><span data-stu-id="4fe12-279">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="4fe12-280">下列 C# 範例會建立自訂類別 (如果尚不存在)：</span><span class="sxs-lookup"><span data-stu-id="4fe12-280">The following C# example creates a custom category, if it does not already exist:</span></span>

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
7. <span data-ttu-id="4fe12-281">更新應用程式內的計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-281">Update the counters within your application.</span></span> <span data-ttu-id="4fe12-282">下列範例會更新 Button1_Click 事件的自訂效能計數器：</span><span class="sxs-lookup"><span data-stu-id="4fe12-282">The following example updates a custom performance counter on Button1_Click events:</span></span>

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
8. <span data-ttu-id="4fe12-283">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="4fe12-283">Save the file.</span></span>  

<span data-ttu-id="4fe12-284">Azure 診斷監視器現在即會收集自訂效能計數器資料。</span><span class="sxs-lookup"><span data-stu-id="4fe12-284">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="4fe12-285">步驟 3：查詢效能計數器資料</span><span class="sxs-lookup"><span data-stu-id="4fe12-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="4fe12-286">當應用程式完成部署並開始執行後，診斷監視器即會開始收集效能計數器，並將資料存留至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4fe12-286">Once your application is deployed and running, the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="4fe12-287">您可以使用 Visual Studio 中的伺服器總管、[Azure 儲存體總管](http://azurestorageexplorer.codeplex.com/)或 Cerebrata 提供的 [Azure 診斷管理員](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx)等工具，檢視 WADPerformanceCountersTable 資料表中的效能計數器資料。</span><span class="sxs-lookup"><span data-stu-id="4fe12-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="4fe12-288">您也可以透過程式設計，使用 [C#](../cosmos-db/table-storage-how-to-use-dotnet.md)、[Java](../cosmos-db/table-storage-how-to-use-java.md)、[Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md)、[Python](../cosmos-db/table-storage-how-to-use-python.md)、[Ruby](../cosmos-db/table-storage-how-to-use-ruby.md) 或 [PHP](../cosmos-db/table-storage-how-to-use-php.md) 來查詢表格服務。</span><span class="sxs-lookup"><span data-stu-id="4fe12-288">You can also programmatically query the Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="4fe12-289">下列 C# 範例將說明對 WADPerformanceCountersTable 資料表的基本查詢，並將診斷資料儲存至 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="4fe12-289">The following C# example shows a basic query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="4fe12-290">效能計數器儲存至 CSV 檔案後，您可以使用 Microsoft Excel 或其他工具的圖表功能，將資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="4fe12-290">Once the performance counters are saved to a CSV file, you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="4fe12-291">請務必為 Azure SDK for .NET (2012 年 10 月或更新版本) 隨附的 Microsoft.WindowsAzure.Storage.dll 新增參考。</span><span class="sxs-lookup"><span data-stu-id="4fe12-291">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="4fe12-292">此組件會安裝在 %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ 目錄中。</span><span class="sxs-lookup"><span data-stu-id="4fe12-292">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
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

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
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

<span data-ttu-id="4fe12-293">實體會使用衍生自 **TableEntity**的自訂類別來對應至 C# 物件。</span><span class="sxs-lookup"><span data-stu-id="4fe12-293">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="4fe12-294">下列程式碼會定義一個實體類別，用以代表 **WADPerformanceCountersTable** 資料表中的效能計數器。</span><span class="sxs-lookup"><span data-stu-id="4fe12-294">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4fe12-295">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4fe12-295">Next Steps</span></span>
[<span data-ttu-id="4fe12-296">檢視有關 Azure 診斷的其他文章</span><span class="sxs-lookup"><span data-stu-id="4fe12-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
