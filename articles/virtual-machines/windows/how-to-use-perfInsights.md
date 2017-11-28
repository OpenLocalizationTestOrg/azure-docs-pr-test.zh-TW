---
title: "aaaHow toouse Microsoft Azure 中的 PerfInsights |Microsoft 文件"
description: "學習如何 toouse PerfInsights tootroubleshoot Windows VM 效能問題。"
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a><span data-ttu-id="b7ba6-103">如何 toouse PerfInsights</span><span class="sxs-lookup"><span data-stu-id="b7ba6-103">How toouse PerfInsights</span></span> 

<span data-ttu-id="b7ba6-104">[PerfInsights](http://aka.ms/perfinsightsdownload)是自動化的指令碼收集診斷資訊、 執行 I/O 壓力負載，並提供分析報表 toohelp Microsoft Azure 中的 Windows VM 效能問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-104">[PerfInsights](http://aka.ms/perfinsightsdownload) is an automated script that collects useful diagnostic information, runs I/O stress loads, and provides an analysis report toohelp troubleshoot Windows VM performance problems in Microsoft Azure.</span></span> 

<span data-ttu-id="b7ba6-105">我們建議您先執行此指令碼， 再開啟 Microsoft 支援票證處理 VM 效能問題。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-105">We recommend that you run this script before you open a Support ticket with Microsoft for VM performance issues.</span></span>

## <a name="supported-troubleshooting-scenarios"></a><span data-ttu-id="b7ba6-106">支援的疑難排解案例</span><span class="sxs-lookup"><span data-stu-id="b7ba6-106">Supported troubleshooting scenarios</span></span>

<span data-ttu-id="b7ba6-107">PerfInsights 可以收集並分析合併到唯一案例的多種資訊。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-107">PerfInsights can collect and analyze several kinds of information that are grouped into unique scenarios.</span></span>

### <a name="collect-disk-configuration"></a><span data-ttu-id="b7ba6-108">收集磁碟設定</span><span class="sxs-lookup"><span data-stu-id="b7ba6-108">Collect disk configuration</span></span> 

<span data-ttu-id="b7ba6-109">此案例，收集 hello 磁碟設定和其他重要的資訊，包括下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b7ba6-109">This scenario collects hello disk configuration and other important information, including hello following items:</span></span>

-   <span data-ttu-id="b7ba6-110">事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="b7ba6-110">Event logs</span></span>

-   <span data-ttu-id="b7ba6-111">所有傳入和傳出連線的網路狀態</span><span class="sxs-lookup"><span data-stu-id="b7ba6-111">Network status for all incoming and outgoing connections</span></span>

-   <span data-ttu-id="b7ba6-112">網路和防火牆組態設定</span><span class="sxs-lookup"><span data-stu-id="b7ba6-112">Network and firewall configuration settings</span></span>

-   <span data-ttu-id="b7ba6-113">工作清單中的 hello 系統目前正在執行的所有應用程式</span><span class="sxs-lookup"><span data-stu-id="b7ba6-113">Task list for all applications that are currently running on hello system</span></span>

-   <span data-ttu-id="b7ba6-114">Msinfo32 hello 虛擬機器 (VM) 所建立的資訊檔案</span><span class="sxs-lookup"><span data-stu-id="b7ba6-114">Information file created by msinfo32 for hello virtual machine (VM)</span></span>

-   <span data-ttu-id="b7ba6-115">Microsoft SQL Server 資料庫組態設定 （如果 hello VM 識別為執行 SQL Server 的伺服器）</span><span class="sxs-lookup"><span data-stu-id="b7ba6-115">Microsoft SQL Server database configuration settings (if hello VM is identified as a server that is running SQL Server)</span></span>

-   <span data-ttu-id="b7ba6-116">儲存體可靠性計數器</span><span class="sxs-lookup"><span data-stu-id="b7ba6-116">Storage reliability counters</span></span>

-   <span data-ttu-id="b7ba6-117">重要的 Windows Hotfix</span><span class="sxs-lookup"><span data-stu-id="b7ba6-117">Important Windows hotfixes</span></span>

-   <span data-ttu-id="b7ba6-118">已安裝的篩選器驅動程式</span><span class="sxs-lookup"><span data-stu-id="b7ba6-118">Installed filter drivers</span></span>

<span data-ttu-id="b7ba6-119">這是被動的集合，不應該影響 hello 系統的資訊。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-119">This is a passive collection of information that shouldn't affect hello system.</span></span> 

>[!Note]
><span data-ttu-id="b7ba6-120">這種情況下都會自動包含在每個 hello 下列案例中。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-120">This scenario is automatically included in each of hello following scenarios.</span></span>

### <a name="benchmarkstorage-performance-test"></a><span data-ttu-id="b7ba6-121">基準測試/儲存體效能測試</span><span class="sxs-lookup"><span data-stu-id="b7ba6-121">Benchmark/Storage Performance Test</span></span>

<span data-ttu-id="b7ba6-122">這種情況下執行 hello [diskspd](https://github.com/Microsoft/diskspd)針對所有的磁碟機附加 toohello VM 建立基準測試 （IOPS 和 MBPS）。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-122">This scenario runs hello [diskspd](https://github.com/Microsoft/diskspd) benchmark test (IOPS and MBPS) for all drives that are attached toohello VM.</span></span> 

> [!Note]
> <span data-ttu-id="b7ba6-123">此案例可能會影響 hello 系統，而且不應該在實際生產系統上執行。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-123">This scenario can affect hello system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="b7ba6-124">必要時，此案例中執行專用的維護視窗 tooavoid 任何問題。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-124">If necessary, run this scenario in a dedicated maintenance window tooavoid any problems.</span></span> <span data-ttu-id="b7ba6-125">增加的工作負載所造成的追蹤或基準測試的測試可能會影響您的 VM 的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-125">An increased workload that is caused by a trace or benchmark test could adversely affect hello performance of your VM.</span></span>
>

### <a name="general-vm-slow-analysis"></a><span data-ttu-id="b7ba6-126">一般 VM Slow 分析</span><span class="sxs-lookup"><span data-stu-id="b7ba6-126">General VM Slow analysis</span></span> 

<span data-ttu-id="b7ba6-127">這種情況下執行[效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx)使用 hello 計數器 hello Generalcounters.txt 檔案中指定的追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-127">This scenario runs a [performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) trace by using hello counters that are specified in hello Generalcounters.txt file.</span></span> <span data-ttu-id="b7ba6-128">如果 hello VM 識別為執行 SQL Server 的伺服器，它會執行使用 hello Sqlcounters.txt 檔中找到的 hello 計數器的效能計數器追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-128">If hello VM is identified as a server that is running SQL Server, it runs a performance counter trace by using hello counters that are found in hello Sqlcounters.txt file.</span></span> <span data-ttu-id="b7ba6-129">它也包含效能診斷資料。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-129">It also includes Performance Diagnostics data.</span></span>

### <a name="vm-slow-analysis-and-benchmark"></a><span data-ttu-id="b7ba6-130">VM Slow 分析和基準測試</span><span class="sxs-lookup"><span data-stu-id="b7ba6-130">VM Slow analysis and benchmark</span></span>

<span data-ttu-id="b7ba6-131">此案例會執行[效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx)追蹤，後面接著 [diskspd](https://github.com/Microsoft/diskspd) 基準測試。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-131">This scenario runs a [performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) trace that is followed by a [diskspd](https://github.com/Microsoft/diskspd) benchmark test.</span></span> 

> [!Note]
> <span data-ttu-id="b7ba6-132">此案例可能會影響 hello 系統，而且不應該在實際生產系統上執行。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-132">This scenario can affect hello system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="b7ba6-133">必要時，此案例中執行專用的維護視窗 tooavoid 任何問題。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-133">If necessary, run this scenario in a dedicated maintenance window tooavoid any problems.</span></span> <span data-ttu-id="b7ba6-134">增加的工作負載所造成的追蹤或基準測試的測試可能會影響您的 VM 的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-134">An increased workload that is caused by a trace or benchmark test could adversely affect hello performance of your VM.</span></span>
>

### <a name="azure-files-analysis"></a><span data-ttu-id="b7ba6-135">Azure 檔案分析</span><span class="sxs-lookup"><span data-stu-id="b7ba6-135">Azure Files analysis</span></span> 

<span data-ttu-id="b7ba6-136">此案例會同時執行特殊的效能計數器擷取與網路追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-136">This scenario runs a special performance counter capture together with a network trace.</span></span> <span data-ttu-id="b7ba6-137">擷取包含所有的 hello [SMB 用戶端共用] 計數器。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-137">The capture includes all hello "SMB Client Shares" counters.</span></span> <span data-ttu-id="b7ba6-138">hello 下面是一些索引鍵的 SMB 用戶端共用效能計數器屬於 hello 擷取：</span><span class="sxs-lookup"><span data-stu-id="b7ba6-138">hello following are some key SMB client share performance counters that are part of hello capture:</span></span>

| <span data-ttu-id="b7ba6-139">**類型**</span><span class="sxs-lookup"><span data-stu-id="b7ba6-139">**Type**</span></span>     | <span data-ttu-id="b7ba6-140">**SMB 用戶端共用計數器**</span><span class="sxs-lookup"><span data-stu-id="b7ba6-140">**SMB client shares counter**</span></span> |
|--------------|-------------------------------|
| <span data-ttu-id="b7ba6-141">IOPS</span><span class="sxs-lookup"><span data-stu-id="b7ba6-141">IOPS</span></span>         | <span data-ttu-id="b7ba6-142">資料要求/秒</span><span class="sxs-lookup"><span data-stu-id="b7ba6-142">Data Requests/sec</span></span>             |
|              | <span data-ttu-id="b7ba6-143">讀取要求/秒</span><span class="sxs-lookup"><span data-stu-id="b7ba6-143">Read Requests/sec</span></span>             |
|              | <span data-ttu-id="b7ba6-144">寫入要求/秒</span><span class="sxs-lookup"><span data-stu-id="b7ba6-144">Write Requests/sec</span></span>            |
| <span data-ttu-id="b7ba6-145">Latency</span><span class="sxs-lookup"><span data-stu-id="b7ba6-145">Latency</span></span>      | <span data-ttu-id="b7ba6-146">平均秒/資料要求</span><span class="sxs-lookup"><span data-stu-id="b7ba6-146">Avg. sec/Data Request</span></span>         |
|              | <span data-ttu-id="b7ba6-147">平均秒/讀取</span><span class="sxs-lookup"><span data-stu-id="b7ba6-147">Avg. sec/Read</span></span>                 |
|              | <span data-ttu-id="b7ba6-148">平均秒/寫入</span><span class="sxs-lookup"><span data-stu-id="b7ba6-148">Avg. sec/Write</span></span>                |
| <span data-ttu-id="b7ba6-149">IO 大小</span><span class="sxs-lookup"><span data-stu-id="b7ba6-149">IO Size</span></span>      | <span data-ttu-id="b7ba6-150">Avg.位元組/資料要求</span><span class="sxs-lookup"><span data-stu-id="b7ba6-150">Avg. Bytes/Data Request</span></span>       |
|              | <span data-ttu-id="b7ba6-151">Avg.位元組/讀取</span><span class="sxs-lookup"><span data-stu-id="b7ba6-151">Avg. Bytes/Read</span></span>               |
|              | <span data-ttu-id="b7ba6-152">Avg.位元組/寫入</span><span class="sxs-lookup"><span data-stu-id="b7ba6-152">Avg. Bytes/Write</span></span>              |
| <span data-ttu-id="b7ba6-153">輸送量</span><span class="sxs-lookup"><span data-stu-id="b7ba6-153">Throughput</span></span>   | <span data-ttu-id="b7ba6-154">資料位元組/秒</span><span class="sxs-lookup"><span data-stu-id="b7ba6-154">Data Bytes/sec</span></span>                |
|              | <span data-ttu-id="b7ba6-155">讀取位元組/秒</span><span class="sxs-lookup"><span data-stu-id="b7ba6-155">Read Bytes/sec</span></span>                |
|              | <span data-ttu-id="b7ba6-156">寫入位元組/秒</span><span class="sxs-lookup"><span data-stu-id="b7ba6-156">Write Bytes/sec</span></span>               |
| <span data-ttu-id="b7ba6-157">佇列長度</span><span class="sxs-lookup"><span data-stu-id="b7ba6-157">Queue Length</span></span> | <span data-ttu-id="b7ba6-158">Avg.讀取佇列長度</span><span class="sxs-lookup"><span data-stu-id="b7ba6-158">Avg. Read Queue Length</span></span>        |
|              | <span data-ttu-id="b7ba6-159">Avg.寫入佇列長度</span><span class="sxs-lookup"><span data-stu-id="b7ba6-159">Avg. Write Queue Length</span></span>       |
|              | <span data-ttu-id="b7ba6-160">Avg.資料佇列長度</span><span class="sxs-lookup"><span data-stu-id="b7ba6-160">Avg. Data Queue Length</span></span>        |

### <a name="custom-configuration"></a><span data-ttu-id="b7ba6-161">自訂組態</span><span class="sxs-lookup"><span data-stu-id="b7ba6-161">Custom configuration</span></span> 

<span data-ttu-id="b7ba6-162">當您執行自訂設定時，您是以平行方式執行所有的追蹤 (效能診斷、效能計數器、xperf、網路、storport)，視您選取多少不同的追蹤而定。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-162">When you run a custom configuration, you are running all traces (performance diagnostics, performance counter, xperf, network, storport) in parallel, depending how many different traces are selected.</span></span> <span data-ttu-id="b7ba6-163">完成追蹤之後，hello 工具會執行 hello diskspd benchmark 中，如果已選取。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-163">After tracing is completed, hello tool runs hello diskspd benchmark, if it is selected.</span></span> 

> [!Note]
> <span data-ttu-id="b7ba6-164">此案例可能會影響 hello 系統，而且不應該在實際生產系統上執行。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-164">This scenario can affect hello system and shouldn’t be run on a live production system.</span></span> <span data-ttu-id="b7ba6-165">必要時，此案例中執行專用的維護視窗 tooavoid 任何問題。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-165">If necessary, run this scenario in a dedicated maintenance window tooavoid any problems.</span></span> <span data-ttu-id="b7ba6-166">增加的工作負載所造成的追蹤或基準測試的測試可能會影響您的 VM 的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-166">An increased workload that is caused by a trace or benchmark test could adversely affect hello performance of your VM.</span></span>
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a><span data-ttu-id="b7ba6-167">Hello 指令碼所收集的資訊類型為何？</span><span class="sxs-lookup"><span data-stu-id="b7ba6-167">What kind of information is collected by hello script?</span></span>

<span data-ttu-id="b7ba6-168">資訊的 Windows VM、 磁碟或儲存集區組態、 收集效能計數器、 記錄檔和各種追蹤視使用的 hello 效能案例而定：</span><span class="sxs-lookup"><span data-stu-id="b7ba6-168">Information about Windows VM, disks or storage pools configuration, performance counters, logs and various traces are collected depending on hello performance scenario used:</span></span>

|<span data-ttu-id="b7ba6-169">收集的資料</span><span class="sxs-lookup"><span data-stu-id="b7ba6-169">Data collected</span></span>                              |  |  | <span data-ttu-id="b7ba6-170">效能測試案例</span><span class="sxs-lookup"><span data-stu-id="b7ba6-170">Performance Scenarios</span></span> |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | <span data-ttu-id="b7ba6-171">收集磁碟設定</span><span class="sxs-lookup"><span data-stu-id="b7ba6-171">Collect disk Configuration</span></span> | <span data-ttu-id="b7ba6-172">基準測試/儲存體效能測試</span><span class="sxs-lookup"><span data-stu-id="b7ba6-172">Benchmark/Storage Performance test</span></span> | <span data-ttu-id="b7ba6-173">一般 VM Slow 分析</span><span class="sxs-lookup"><span data-stu-id="b7ba6-173">General VM Slow analysis</span></span> | <span data-ttu-id="b7ba6-174">VM Slow 分析和基準測試</span><span class="sxs-lookup"><span data-stu-id="b7ba6-174">VM Slow analysis and benchmark</span></span> | <span data-ttu-id="b7ba6-175">Azure 檔案分析</span><span class="sxs-lookup"><span data-stu-id="b7ba6-175">Azure Files analysis</span></span> | <span data-ttu-id="b7ba6-176">自訂組態</span><span class="sxs-lookup"><span data-stu-id="b7ba6-176">Custom configuration</span></span> |
| <span data-ttu-id="b7ba6-177">來自事件記錄檔的資訊</span><span class="sxs-lookup"><span data-stu-id="b7ba6-177">Information from Event logs</span></span>      | <span data-ttu-id="b7ba6-178">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-178">Yes</span></span>                        | <span data-ttu-id="b7ba6-179">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-179">Yes</span></span>                                | <span data-ttu-id="b7ba6-180">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-180">Yes</span></span>                      | <span data-ttu-id="b7ba6-181">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-181">Yes</span></span>                            | <span data-ttu-id="b7ba6-182">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-182">Yes</span></span>                  | <span data-ttu-id="b7ba6-183">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-183">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-184">系統資訊</span><span class="sxs-lookup"><span data-stu-id="b7ba6-184">System information</span></span>               | <span data-ttu-id="b7ba6-185">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-185">Yes</span></span>                        | <span data-ttu-id="b7ba6-186">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-186">Yes</span></span>                                | <span data-ttu-id="b7ba6-187">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-187">Yes</span></span>                      | <span data-ttu-id="b7ba6-188">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-188">Yes</span></span>                            | <span data-ttu-id="b7ba6-189">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-189">Yes</span></span>                  | <span data-ttu-id="b7ba6-190">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-190">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-191">磁碟區對應</span><span class="sxs-lookup"><span data-stu-id="b7ba6-191">Volume Map</span></span>                       | <span data-ttu-id="b7ba6-192">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-192">Yes</span></span>                        | <span data-ttu-id="b7ba6-193">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-193">Yes</span></span>                                | <span data-ttu-id="b7ba6-194">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-194">Yes</span></span>                      | <span data-ttu-id="b7ba6-195">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-195">Yes</span></span>                            | <span data-ttu-id="b7ba6-196">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-196">Yes</span></span>                  | <span data-ttu-id="b7ba6-197">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-197">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-198">磁碟對應</span><span class="sxs-lookup"><span data-stu-id="b7ba6-198">Disk Map</span></span>                         | <span data-ttu-id="b7ba6-199">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-199">Yes</span></span>                        | <span data-ttu-id="b7ba6-200">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-200">Yes</span></span>                                | <span data-ttu-id="b7ba6-201">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-201">Yes</span></span>                      | <span data-ttu-id="b7ba6-202">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-202">Yes</span></span>                            | <span data-ttu-id="b7ba6-203">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-203">Yes</span></span>                  | <span data-ttu-id="b7ba6-204">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-204">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-205">正在執行的工作</span><span class="sxs-lookup"><span data-stu-id="b7ba6-205">Running Tasks</span></span>                    | <span data-ttu-id="b7ba6-206">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-206">Yes</span></span>                        | <span data-ttu-id="b7ba6-207">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-207">Yes</span></span>                                | <span data-ttu-id="b7ba6-208">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-208">Yes</span></span>                      | <span data-ttu-id="b7ba6-209">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-209">Yes</span></span>                            | <span data-ttu-id="b7ba6-210">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-210">Yes</span></span>                  | <span data-ttu-id="b7ba6-211">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-211">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-212">儲存體可靠性計數器</span><span class="sxs-lookup"><span data-stu-id="b7ba6-212">Storage Reliability Counters</span></span>     | <span data-ttu-id="b7ba6-213">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-213">Yes</span></span>                        | <span data-ttu-id="b7ba6-214">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-214">Yes</span></span>                                | <span data-ttu-id="b7ba6-215">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-215">Yes</span></span>                      | <span data-ttu-id="b7ba6-216">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-216">Yes</span></span>                            | <span data-ttu-id="b7ba6-217">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-217">Yes</span></span>                  | <span data-ttu-id="b7ba6-218">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-218">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-219">儲存體資訊</span><span class="sxs-lookup"><span data-stu-id="b7ba6-219">Storage information</span></span>              | <span data-ttu-id="b7ba6-220">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-220">Yes</span></span>                        | <span data-ttu-id="b7ba6-221">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-221">Yes</span></span>                                | <span data-ttu-id="b7ba6-222">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-222">Yes</span></span>                      | <span data-ttu-id="b7ba6-223">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-223">Yes</span></span>                            | <span data-ttu-id="b7ba6-224">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-224">Yes</span></span>                  | <span data-ttu-id="b7ba6-225">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-225">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-226">Fsutil 輸出</span><span class="sxs-lookup"><span data-stu-id="b7ba6-226">Fsutil output</span></span>                    | <span data-ttu-id="b7ba6-227">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-227">Yes</span></span>                        | <span data-ttu-id="b7ba6-228">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-228">Yes</span></span>                                | <span data-ttu-id="b7ba6-229">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-229">Yes</span></span>                      | <span data-ttu-id="b7ba6-230">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-230">Yes</span></span>                            | <span data-ttu-id="b7ba6-231">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-231">Yes</span></span>                  | <span data-ttu-id="b7ba6-232">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-232">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-233">篩選器驅動程式資訊</span><span class="sxs-lookup"><span data-stu-id="b7ba6-233">Filter Driver info</span></span>               | <span data-ttu-id="b7ba6-234">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-234">Yes</span></span>                        | <span data-ttu-id="b7ba6-235">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-235">Yes</span></span>                                | <span data-ttu-id="b7ba6-236">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-236">Yes</span></span>                      | <span data-ttu-id="b7ba6-237">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-237">Yes</span></span>                            | <span data-ttu-id="b7ba6-238">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-238">Yes</span></span>                  | <span data-ttu-id="b7ba6-239">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-239">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-240">Netstat 輸出</span><span class="sxs-lookup"><span data-stu-id="b7ba6-240">Netstat output</span></span>                   | <span data-ttu-id="b7ba6-241">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-241">Yes</span></span>                        | <span data-ttu-id="b7ba6-242">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-242">Yes</span></span>                                | <span data-ttu-id="b7ba6-243">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-243">Yes</span></span>                      | <span data-ttu-id="b7ba6-244">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-244">Yes</span></span>                            | <span data-ttu-id="b7ba6-245">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-245">Yes</span></span>                  | <span data-ttu-id="b7ba6-246">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-246">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-247">網路組態</span><span class="sxs-lookup"><span data-stu-id="b7ba6-247">Network configuration</span></span>            | <span data-ttu-id="b7ba6-248">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-248">Yes</span></span>                        | <span data-ttu-id="b7ba6-249">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-249">Yes</span></span>                                | <span data-ttu-id="b7ba6-250">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-250">Yes</span></span>                      | <span data-ttu-id="b7ba6-251">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-251">Yes</span></span>                            | <span data-ttu-id="b7ba6-252">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-252">Yes</span></span>                  | <span data-ttu-id="b7ba6-253">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-253">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-254">防火牆設定</span><span class="sxs-lookup"><span data-stu-id="b7ba6-254">Firewall configuration</span></span>           | <span data-ttu-id="b7ba6-255">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-255">Yes</span></span>                        | <span data-ttu-id="b7ba6-256">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-256">Yes</span></span>                                | <span data-ttu-id="b7ba6-257">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-257">Yes</span></span>                      | <span data-ttu-id="b7ba6-258">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-258">Yes</span></span>                            | <span data-ttu-id="b7ba6-259">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-259">Yes</span></span>                  | <span data-ttu-id="b7ba6-260">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-260">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-261">SQL Server 設定</span><span class="sxs-lookup"><span data-stu-id="b7ba6-261">SQL Server configuration</span></span>         | <span data-ttu-id="b7ba6-262">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-262">Yes</span></span>                        | <span data-ttu-id="b7ba6-263">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-263">Yes</span></span>                                | <span data-ttu-id="b7ba6-264">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-264">Yes</span></span>                      | <span data-ttu-id="b7ba6-265">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-265">Yes</span></span>                            | <span data-ttu-id="b7ba6-266">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-266">Yes</span></span>                  | <span data-ttu-id="b7ba6-267">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-267">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-268">效能診斷追蹤 *</span><span class="sxs-lookup"><span data-stu-id="b7ba6-268">Performance Diagnostics Traces *</span></span> |                            |                                    | <span data-ttu-id="b7ba6-269">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-269">Yes</span></span>                      |                                |                      | <span data-ttu-id="b7ba6-270">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-270">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-271">效能計數器追蹤 **</span><span class="sxs-lookup"><span data-stu-id="b7ba6-271">Performance counter Trace **</span></span>     |                            |                                    |                          |                                |                      | <span data-ttu-id="b7ba6-272">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-272">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-273">SMB 計數器追蹤 **</span><span class="sxs-lookup"><span data-stu-id="b7ba6-273">SMB counter Trace **</span></span>             |                            |                                    |                          |                                | <span data-ttu-id="b7ba6-274">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-274">Yes</span></span>                  |                      |
| <span data-ttu-id="b7ba6-275">SQL Server 計數器追蹤 **</span><span class="sxs-lookup"><span data-stu-id="b7ba6-275">SQL Server counter Trace **</span></span>      |                            |                                    |                          |                                |                      | <span data-ttu-id="b7ba6-276">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-276">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-277">XPerf 追蹤</span><span class="sxs-lookup"><span data-stu-id="b7ba6-277">XPerf Trace</span></span>                      |                            |                                    |                          |                                |                      | <span data-ttu-id="b7ba6-278">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-278">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-279">StorPort 追蹤</span><span class="sxs-lookup"><span data-stu-id="b7ba6-279">StorPort Trace</span></span>                   |                            |                                    |                          |                                |                      | <span data-ttu-id="b7ba6-280">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-280">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-281">網路追蹤</span><span class="sxs-lookup"><span data-stu-id="b7ba6-281">Network Trace</span></span>                    |                            |                                    |                          |                                | <span data-ttu-id="b7ba6-282">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-282">Yes</span></span>                  | <span data-ttu-id="b7ba6-283">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-283">Yes</span></span>                  |
| <span data-ttu-id="b7ba6-284">Diskspd 基準追蹤 ***</span><span class="sxs-lookup"><span data-stu-id="b7ba6-284">Diskspd Benchmark trace ***</span></span>      |                            | <span data-ttu-id="b7ba6-285">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-285">Yes</span></span>                                |                          | <span data-ttu-id="b7ba6-286">是</span><span class="sxs-lookup"><span data-stu-id="b7ba6-286">Yes</span></span>                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a><span data-ttu-id="b7ba6-287">效能診斷追蹤 (*)</span><span class="sxs-lookup"><span data-stu-id="b7ba6-287">Performance Diagnostics trace (*)</span></span>

<span data-ttu-id="b7ba6-288">執行規則引擎在 hello 背景 toocollect 資料和診斷進行中的效能問題。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-288">Runs a rule-based engine in hello background toocollect data and diagnose ongoing performance issues.</span></span> <span data-ttu-id="b7ba6-289">目前支援下列規則的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7ba6-289">hello following rules are currently supported:</span></span>

- <span data-ttu-id="b7ba6-290">HighCpuUsage 規則： 偵測到高 CPU 使用量的期間，並在這些時間週期期間顯示 hello 頂端 CPU 使用量取用者。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-290">HighCpuUsage rule: Detects high CPU usage periods and shows hello top CPU usage consumers during those periods.</span></span>
- <span data-ttu-id="b7ba6-291">HighDiskUsage 規則： 偵測到的實體磁碟上的高磁碟使用量期間，並在這些時間週期期間顯示 hello 最大的磁碟使用量取用者。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-291">HighDiskUsage rule: Detects high disk usage periods on physical disks and shows hello top disk usage consumers during those periods.</span></span>
- <span data-ttu-id="b7ba6-292">HighResolutionDiskMetric 規則： 顯示每部實體磁碟每 50 毫秒的 IOPS、輸送量和 IO 延遲計量。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-292">HighResolutionDiskMetric rule: Shows IOPS, throughput and IO latency metrics per 50 milliseconds for each physical disk.</span></span> <span data-ttu-id="b7ba6-293">它會協助 tooquickly 識別節流週期的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-293">It helps tooquickly identify disk throttling periods.</span></span>
- <span data-ttu-id="b7ba6-294">HighMemoryUsage 規則： 偵測到高記憶體使用量的期間，並在這些時間週期期間顯示 hello 最多記憶體的使用方式取用者。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-294">HighMemoryUsage rule: Detects high memory usage periods, and shows hello top memory usage consumers during those periods.</span></span>

> [!NOTE] 
> <span data-ttu-id="b7ba6-295">目前支援 Windows 版本，包括 hello.NET Framework 3.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-295">Currently, Windows versions that include hello .NET Framework 3.5 or later versions are supported.</span></span>

### <a name="performance-counter-trace-"></a><span data-ttu-id="b7ba6-296">效能計數器追蹤 (**)</span><span class="sxs-lookup"><span data-stu-id="b7ba6-296">Performance Counter trace (**)</span></span>

<span data-ttu-id="b7ba6-297">會收集下列效能計數器的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7ba6-297">Collects hello following Performance Counters:</span></span>

- <span data-ttu-id="b7ba6-298">\Process、\Processor、\Memory、\Thread、\PhysicalDisk、\LogicalDisk</span><span class="sxs-lookup"><span data-stu-id="b7ba6-298">\Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk</span></span>
- <span data-ttu-id="b7ba6-299">\Cache\Dirty Pages、\Cache\Lazy Write Flushes/sec、\Server\Pool Nonpaged、Failures、\Server\Pool Paged Failures</span><span class="sxs-lookup"><span data-stu-id="b7ba6-299">\Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures</span></span>
- <span data-ttu-id="b7ba6-300">\Network Interface、\IPv4\Datagrams、\IPv6\Datagrams、\TCPv4\Segments、\TCPv6\Segments、\Network Adapter、\WFPv4\Packets、\WFPv6\Packets、\UDPv4\Datagrams、\UDPv6\Datagrams、\TCPv4\Connection、\TCPv6\Connection、\Network QoS Policy\Packets、\Per Processor Network Interface Card Activity、\Microsoft Winsock BSP 下的已選取計數器</span><span class="sxs-lookup"><span data-stu-id="b7ba6-300">Selected counters under \Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments,  \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP</span></span>

#### <a name="for-sql-server-instances"></a><span data-ttu-id="b7ba6-301">SQL Server 執行個體</span><span class="sxs-lookup"><span data-stu-id="b7ba6-301">For SQL Server instances</span></span>
- <span data-ttu-id="b7ba6-302">\SQL Server:Buffer Manager、\SQLServer:Resource Pool Stats、\SQLServer:SQL Statistics\\</span><span class="sxs-lookup"><span data-stu-id="b7ba6-302">\SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\\</span></span>
- <span data-ttu-id="b7ba6-303">\SQLServer:Locks、\SQLServer:General、Statistics</span><span class="sxs-lookup"><span data-stu-id="b7ba6-303">\SQLServer:Locks, \SQLServer:General, Statistics</span></span>
- <span data-ttu-id="b7ba6-304">\SQLServer:Access 方法</span><span class="sxs-lookup"><span data-stu-id="b7ba6-304">\SQLServer:Access Methods</span></span>

#### <a name="for-azure-files"></a><span data-ttu-id="b7ba6-305">Azure 檔案</span><span class="sxs-lookup"><span data-stu-id="b7ba6-305">For Azure Files</span></span>
<span data-ttu-id="b7ba6-306">\SMB 用戶端共用</span><span class="sxs-lookup"><span data-stu-id="b7ba6-306">\SMB Client Shares</span></span>

### <a name="diskspd-benchmark-trace-"></a><span data-ttu-id="b7ba6-307">Diskspd 基準追蹤 (***)</span><span class="sxs-lookup"><span data-stu-id="b7ba6-307">Diskspd Benchmark trace (***)</span></span>
<span data-ttu-id="b7ba6-308">Diskspd IO 工作負載測試 [OS 磁碟 (寫入) 和集區磁碟 (讀取/寫入)]</span><span class="sxs-lookup"><span data-stu-id="b7ba6-308">Diskspd IO workload tests [OS Disk (write) and pool drives (read/write)]</span></span>

## <a name="run-hello-perfinsights-on-your-vm"></a><span data-ttu-id="b7ba6-309">在您的 VM 上執行 hello PerfInsights</span><span class="sxs-lookup"><span data-stu-id="b7ba6-309">Run hello PerfInsights on your VM</span></span>

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a><span data-ttu-id="b7ba6-310">為什麼應該 tooknow 之前我要執行 hello 指令碼？</span><span class="sxs-lookup"><span data-stu-id="b7ba6-310">What do I have tooknow before I run hello script?</span></span> 

<span data-ttu-id="b7ba6-311">**指令碼需求**</span><span class="sxs-lookup"><span data-stu-id="b7ba6-311">**Script requirements**</span></span>

1.  <span data-ttu-id="b7ba6-312">此指令碼必須 hello 發生 hello 效能問題的 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-312">This script must be run on hello VM that has hello performance issue.</span></span> 

2.  <span data-ttu-id="b7ba6-313">hello 支援下列作業系統： Windows Server 2008 R2、 2012、 2012 R2、 2016。Windows 8.1 和 Windows 10。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-313">hello following OSes are supported: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 and Windows 10.</span></span>

<span data-ttu-id="b7ba6-314">**當您在實際執行的 Vm 上執行 hello 指令碼的可能問題：**</span><span class="sxs-lookup"><span data-stu-id="b7ba6-314">**Possible issues when you run hello script on production VMs:**</span></span>

1.  <span data-ttu-id="b7ba6-315">hello 指令碼與已使用 XPerf 或 DiskSpd hello 「 基準 」 或 「 自訂 」 案例一起使用時，可能產生不良影響 hello 的 hello VM 的效能。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-315">hello script might adversely affect hello performance of hello VM when it is used together with hello "Benchmark" or "Custom" scenario that is configured by using XPerf or DiskSpd.</span></span> <span data-ttu-id="b7ba6-316">當您在生產環境中執行 hello 指令碼，請格外小心。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-316">Be careful when you run hello script in a production environment.</span></span>

2.  <span data-ttu-id="b7ba6-317">當您使用 hello 指令碼，以及已使用 DiskSpd 的 hello 「 基準 」 或 「 自訂 」 案例時，請確定沒有其他背景活動干擾 hello hello 測試磁碟上的 I/O 工作負載。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-317">When you use hello script together with hello "Benchmark" or "Custom" scenario that is configured by using DiskSpd, make sure that no other background activity interferes with hello I/O workload on hello tested disks.</span></span>

3.  <span data-ttu-id="b7ba6-318">根據預設，hello 指令碼會使用 hello 暫存磁碟機 toocollect 資料。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-318">By default, hello script uses hello temporary storage drive toocollect data.</span></span> <span data-ttu-id="b7ba6-319">如果追蹤會保持啟用更長的時間，可能是相關 hello 收集的資料數量。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-319">If tracing stays enabled for a longer time, hello amount of data that is collected might be relevant.</span></span> <span data-ttu-id="b7ba6-320">這可以降低 hello 可用性 hello 暫存磁碟，因此會影響依賴此磁碟機的任何應用程式上的空間。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-320">This can reduce hello availability of space on hello temporary disk, therefore affecting any application that relies on this drive.</span></span>

### <a name="how-do-i-run-perfinsights"></a><span data-ttu-id="b7ba6-321">如何執行 PerfInsights？</span><span class="sxs-lookup"><span data-stu-id="b7ba6-321">How do I run PerfInsights?</span></span> 

<span data-ttu-id="b7ba6-322">toorun hello 指令碼，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b7ba6-322">toorun hello script, follow these steps:</span></span>

1. <span data-ttu-id="b7ba6-323">下載 [PerfInsights.zip](http://aka.ms/perfinsightsdownload)。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-323">Download [PerfInsights.zip](http://aka.ms/perfinsightsdownload).</span></span>

2. <span data-ttu-id="b7ba6-324">解除封鎖 hello PerfInsights.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-324">Unblock hello PerfInsights.zip file.</span></span> <span data-ttu-id="b7ba6-325">這樣，以滑鼠右鍵按一下 hello PerfInsights.zip 檔案中，選取 toodo**屬性**。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-325">toodo this, right-click hello PerfInsights.zip file, select **Properties**.</span></span> <span data-ttu-id="b7ba6-326">在 hello**一般**索引標籤上，選取**解除封鎖**，然後選取 **確定**。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-326">In hello **General** tab, select **Unblock** and then select **OK**.</span></span> <span data-ttu-id="b7ba6-327">如此可確保 hello 指令碼會在沒有任何額外的安全性會提示執行。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-327">This will make sure that hello script runs without any additional security prompts.</span></span>  

    ![解除鎖定 hello zip 檔案](media/how-to-use-perfInsights/unlock-file.png)

3.  <span data-ttu-id="b7ba6-329">展開壓縮的 hello PerfInsights.zip 檔案至暫存磁碟機 （依預設，通常是 hello D 磁碟機）。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-329">Expand hello compressed PerfInsights.zip file into your temporary drive (by default, usually hello D drive).</span></span> <span data-ttu-id="b7ba6-330">hello 壓縮的檔案應包含 hello 下列檔案和資料夾：</span><span class="sxs-lookup"><span data-stu-id="b7ba6-330">hello compressed file should contain hello following files and folders:</span></span>

    ![hello zip 資料夾中的檔案](media/how-to-use-perfInsights/file-folder.png)

4.  <span data-ttu-id="b7ba6-332">系統管理員身分開啟 Windows PowerShell，然後執行 hello PerfInsights.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-332">Open Windows PowerShell as an administrator, and then run hello PerfInsights.ps1 script.</span></span>

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    <span data-ttu-id="b7ba6-333">您可能必須 tooenter"y"tooif 您詢問 tooconfirm 想 toochange hello 執行原則。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-333">You might have tooenter "y" tooif you are asked tooconfirm that you want toochange hello execution policy.</span></span>

    <span data-ttu-id="b7ba6-334">在 hello 免責聲明對話方塊方塊中，您可以向 Microsoft 支援的 hello 選項 tooshare 診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-334">In hello Disclaimer dialog box, you are given hello option tooshare diagnostic information with Microsoft Support.</span></span> <span data-ttu-id="b7ba6-335">您也必須同意 toohello 授權合約 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-335">You must also consent toohello license agreement toocontinue.</span></span> <span data-ttu-id="b7ba6-336">確認選項後按一下 [執行指令碼]。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-336">Make your selections, and then click **Run Script**.</span></span>

    ![[免責聲明] 方塊](media/how-to-use-perfInsights/disclaimer.png)

5.  <span data-ttu-id="b7ba6-338">如果可用的話，當您執行 hello 指令碼 （這是我們的統計資料） 時，請送出 hello 案例數目。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-338">Submit hello case number, if it is available, when you run hello script (This is for our statistics).</span></span> <span data-ttu-id="b7ba6-339">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-339">Then, click **OK**.</span></span>
    
    ![輸入支援識別碼](media/how-to-use-perfInsights/enter-support-number.png)

6.  <span data-ttu-id="b7ba6-341">選取暫存磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-341">Select your temporary storage drive.</span></span> <span data-ttu-id="b7ba6-342">hello 指令碼可以自動偵測 hello hello 磁碟機的磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-342">hello Script can auto-detect hello drive letter of hello drive.</span></span> <span data-ttu-id="b7ba6-343">如果在這個階段中發生任何問題，您可能會提示您 tooselect hello 磁碟機 （hello 預設磁碟機是 D）。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-343">If any problems occur in this stage, you might be prompted tooselect hello drive (hello default drive is D).</span></span> <span data-ttu-id="b7ba6-344">產生的記錄檔會儲存在這裡 hello 記錄檔中\_集合資料夾。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-344">Generated logs are stored here in hello log\_collection folder.</span></span> <span data-ttu-id="b7ba6-345">您輸入或接受 hello 磁碟機代號後，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-345">After you enter or accept hello drive letter, click **OK**.</span></span>

    ![輸入磁碟機](media/how-to-use-perfInsights/enter-drive.png)

7.  <span data-ttu-id="b7ba6-347">從 hello 提供清單中，選取疑難排解的情況。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-347">Select a troubleshooting scenario from hello provided list.</span></span>

       ![選取支援案例](media/how-to-use-perfInsights/select-scenarios.png)

8.  <span data-ttu-id="b7ba6-349">您也可以執行 PerfInsights 不顯示 UI。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-349">You can also run PerfInsights without UI.</span></span>

    <span data-ttu-id="b7ba6-350">hello 下列命令執行 hello 「 一般 VM 慢分析 」 疑難排解案例，而無 UI 提示，或為 30 秒內擷取資料。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-350">hello following command runs hello "General VM Slow analysis" troubleshooting scenario without a UI prompt or capture data for 30 seconds.</span></span> <span data-ttu-id="b7ba6-351">它會提示您 tooconsent toohello 相同免責聲明和步驟 4 中所述的使用者授權合約。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-351">It prompts you tooconsent toohello same disclaimer and EULA that  are mentioned in step 4.</span></span>

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    <span data-ttu-id="b7ba6-352">如果您想 PerfInsights toorun 以無訊息模式時，使用**-AcceptDisclaimerAndShareDiagnostics**參數。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-352">If you want PerfInsights toorun in silent mode, use the **-AcceptDisclaimerAndShareDiagnostics** parameter.</span></span> <span data-ttu-id="b7ba6-353">例如，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b7ba6-353">For example, use hello following command:</span></span>

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a><span data-ttu-id="b7ba6-354">如何疑難排解執行 hello 指令碼時的問題？</span><span class="sxs-lookup"><span data-stu-id="b7ba6-354">How do I troubleshoot issues while running hello script?</span></span>

<span data-ttu-id="b7ba6-355">如果不正常終止 hello 指令碼，您可以清除不一致的狀態執行 hello 指令碼，並搭配 hello-清除參數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b7ba6-355">If hello script terminates abnormally, you can clean up an inconsistent state by running hello script together with hello -Cleanup switch, as follows:</span></span>

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

<span data-ttu-id="b7ba6-356">如果 hello 自動偵測 hello 暫存磁碟機的期間發生任何問題，您可能會提示您 tooselect hello 磁碟機 （hello 預設磁碟機是 D）。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-356">If any problems occur during hello automatic detection of hello temporary drive, you might be prompted tooselect hello drive (hello default drive is D).</span></span>

![enter-drive](media/how-to-use-perfInsights/enter-drive.png)

<span data-ttu-id="b7ba6-358">hello 指令碼解除安裝 hello 公用程式工具，並會移除暫存資料夾。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-358">hello script uninstalls hello utility tools and removes temporary folders.</span></span>

### <a name="troubleshooting-other-script-issues"></a><span data-ttu-id="b7ba6-359">對其他指令碼問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b7ba6-359">Troubleshooting other script issues</span></span> 

<span data-ttu-id="b7ba6-360">如果您執行 hello 指令碼時，就會發生任何問題，請按 Ctrl + C toointerrupt hello 指令碼執行。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-360">If any problems occur when you run hello script, press Ctrl+C toointerrupt hello script execution.</span></span> <span data-ttu-id="b7ba6-361">tooremove 暫存物件，請參閱 hello 「 清除異常終止之後 」 一節。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-361">tooremove temporary objects, see hello "Clean up after abnormal termination" section.</span></span>

<span data-ttu-id="b7ba6-362">如果您嘗試幾次之後，即使持續 tooexperience 指令碼失敗，我們建議您以 「 偵錯模式 」 執行 hello 指令碼使用 hello"為偵錯 」 參數選項，在啟動時。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-362">If you continue tooexperience script failure even after several attempts, we recommend that you run hello script in "debug mode" by using hello "-Debug" parameter option on startup.</span></span>

<span data-ttu-id="b7ba6-363">Hello 失敗發生時，複製 hello 完整輸出的 hello PowerShell 主控台中，並將它傳送 toohello Microsoft 支援服務代理程式的使用者您的協助之後 toohelp 會對 hello 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-363">After hello failure occurs, copy hello full output of hello PowerShell console, and send it toohello Microsoft Support agent who is assisting you toohelp troubleshoot hello problem.</span></span>

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a><span data-ttu-id="b7ba6-364">如何在自訂組態模式下執行 hello 指令碼？</span><span class="sxs-lookup"><span data-stu-id="b7ba6-364">How do I run hello script in custom configuration mode?</span></span>

<span data-ttu-id="b7ba6-365">藉由選取 hello**自訂**組態中，您可以啟用數個追蹤，以平行方式 （使用 shift 鍵 toomulti 選取）：</span><span class="sxs-lookup"><span data-stu-id="b7ba6-365">By selecting hello **Custom** configuration, you can enable several traces in parallel (use Shift toomulti-select):</span></span>

![選取案例](media/how-to-use-perfInsights/select-scenario.png)

<span data-ttu-id="b7ba6-367">當您選取 hello 效能診斷時，效能計數器追蹤、 XPerf 追蹤、 網路追蹤或 Storport 追蹤案例中，遵循 hello hello 對話方塊中，再次嘗試 tooreproduce hello 效能緩慢的問題之後啟動 hello 追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-367">When you select hello Performance Diagnostics, Performance Counter Trace, XPerf Trace, Network Trace, or Storport Trace scenarios, follow hello instructions in hello dialog boxes, and try tooreproduce hello slow performance issue after you start hello traces.</span></span>

<span data-ttu-id="b7ba6-368">下列對話方塊中的 hello 可讓您啟動追蹤：</span><span class="sxs-lookup"><span data-stu-id="b7ba6-368">hello following dialog box lets you start a trace:</span></span>

![start-trace](media/how-to-use-perfInsights/start-trace-message.png)

<span data-ttu-id="b7ba6-370">toostop hello 追蹤，tooconfirm hello 命令中有第二個對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-370">toostop hello traces, you have tooconfirm hello command in a second dialog box.</span></span>

<span data-ttu-id="b7ba6-371">![stop-trace](media/how-to-use-perfInsights/stop-trace-message.png)
![stop-trace](media/how-to-use-perfInsights/ok-trace-message.png)</span><span class="sxs-lookup"><span data-stu-id="b7ba6-371">![stop-trace](media/how-to-use-perfInsights/stop-trace-message.png)
![stop-trace](media/how-to-use-perfInsights/ok-trace-message.png)</span></span>

<span data-ttu-id="b7ba6-372">當 hello 追蹤或作業都完成後，新的檔案會產生在 d:\\記錄\_集合 （或 hello 暫存磁碟機），名稱為**CollectedData\_yyyy MM dd\_hh\_公釐\_ss.zip。**</span><span class="sxs-lookup"><span data-stu-id="b7ba6-372">When hello traces or operations are completed, a new file is generated in D:\\log\_collection (or hello temporary drive) that is named **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip.**</span></span> <span data-ttu-id="b7ba6-373">您可以傳送分析此檔案 toohello 支援代理程式。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-373">You can send this file toohello Support agent for analysis.</span></span>

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a><span data-ttu-id="b7ba6-374">檢閱 hello PerfInsights 所建立的診斷報告</span><span class="sxs-lookup"><span data-stu-id="b7ba6-374">Review hello diagnostics report created by PerfInsights</span></span>

<span data-ttu-id="b7ba6-375">Hello 內**CollectedData\_yyyy MM dd\_hh\_公釐\_ss.zip 檔案**PerfInsights 產生，則可以找到詳細資料的 hello 發現 HTML 報表PerfInsights。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-375">Within hello **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip file,** that is generated by PerfInsights, you can find an HTML report that details hello findings of PerfInsights.</span></span> <span data-ttu-id="b7ba6-376">tooreview hello 報表中，展開 hello **CollectedData\_yyyy MM dd\_hh\_公釐\_ss.zip**檔案，然後再開啟 hello **PerfInsights Report.html**檔案。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-376">tooreview hello report, expand hello **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip** file, and then open hello **PerfInsights Report.html** file.</span></span>

<span data-ttu-id="b7ba6-377">選取 hello**發現** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-377">Select hello **Findings** tab.</span></span>

![[尋找] 索引標籤](media/how-to-use-perfInsights/findingtab.png)

<span data-ttu-id="b7ba6-379">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="b7ba6-379">**Notes**</span></span>

-   <span data-ttu-id="b7ba6-380">紅色訊息是已知的設定問題，可能會導致效能問題。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-380">Messages in red are known configuration issues that may cause performance issues.</span></span>

-   <span data-ttu-id="b7ba6-381">黃色訊息是警告，表示不一定會造成效能問題的非最佳化設定。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-381">Messages in yellow are warnings that represent non-optimal configurations that do not necessarily cause performance issues.</span></span>

-   <span data-ttu-id="b7ba6-382">藍色訊息僅為資訊聲明。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-382">Messages in blue are informative statements only.</span></span>

<span data-ttu-id="b7ba6-383">檢閱 hello 紅色 tooget 中的所有錯誤訊息的 HTTP 連結更詳細的 hello 發現與它們可能會如何影響 hello 效能最佳化組態的最佳作法的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-383">Review hello HTTP links for all error messages in red tooget more detailed information about hello findings and how they can affect hello performance or best practices for performance-optimized configurations.</span></span>

### <a name="disk-configuration-tab"></a><span data-ttu-id="b7ba6-384">[磁碟設定] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="b7ba6-384">Disk Configuration Tab</span></span>

<span data-ttu-id="b7ba6-385">hello**概觀**區段會顯示 hello 存放裝置設定，包括從 Diskpart 與儲存空間資訊的不同檢視</span><span class="sxs-lookup"><span data-stu-id="b7ba6-385">hello **Overview** section displays different views of hello storage configuration, including information from Diskpart and Storage Spaces</span></span>

<span data-ttu-id="b7ba6-386">hello **DiskMap**和**VolumeMap**各節說明如何邏輯雙重檢視方塊上的磁碟區和實體磁碟都是相關的 tooeach 其他。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-386">hello **DiskMap** and **VolumeMap** sections describe on a dual perspective how logical volumes and physical disks are related tooeach other.</span></span>

<span data-ttu-id="b7ba6-387">Hello PhysicalDisk 檢視方塊 (DiskMap)，在 hello 資料表會顯示 hello 磁碟上執行的所有邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-387">In hello PhysicalDisk perspective (DiskMap), hello table shows all logical volumes that are running on hello disk.</span></span> <span data-ttu-id="b7ba6-388">在下列範例的 hello，PhysicalDrive2 執行 2 邏輯磁碟區建立多個資料分割 （J 和 H）：</span><span class="sxs-lookup"><span data-stu-id="b7ba6-388">In hello following example, PhysicalDrive2 runs 2 Logical Volumes created on multiple partitions (J and H):</span></span>

![[資料] 索引標籤](media/how-to-use-perfInsights/disktab.png)

<span data-ttu-id="b7ba6-390">在 hello 磁碟區的檢視方塊中 (*VolumeMap*)，hello 表格顯示在每個邏輯磁碟區下的 hello 實體磁碟。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-390">In hello Volume perspective (*VolumeMap*), hello tables show all hello physical disks under each logical volume.</span></span> <span data-ttu-id="b7ba6-391">請注意，對於 RAID/動態磁碟，您可能會在多個實體磁碟上執行邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-391">Notice that for RAID/Dynamic disks, you might run a logical volume upon multiple physical disks.</span></span> <span data-ttu-id="b7ba6-392">在下列範例中的 hello *c:\\掛接*是設定為掛接點*SpannedDisk*上 PhysicalDisks \#2 和\#3:</span><span class="sxs-lookup"><span data-stu-id="b7ba6-392">In hello following sample *C:\\mount* is a mountpoint configured as *SpannedDisk* on PhysicalDisks \#2 and \#3:</span></span>

![[磁碟區] 索引標籤](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a><span data-ttu-id="b7ba6-394">[SQL Server] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="b7ba6-394">SQL Server tab</span></span>

<span data-ttu-id="b7ba6-395">如果 hello 目標 VM 裝載任何 SQL Server 執行個體，您會看到 [其他] 索引標籤中名為 hello 報表**SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="b7ba6-395">If hello target VM hosts any SQL Server instances, you will see an additional tab in hello report that is named **SQL Server**:</span></span>

![[SQL] 索引標籤](media/how-to-use-perfInsights/sqltab.png)

<span data-ttu-id="b7ba6-397">本節包含 「 概觀 」 和其他的子索引標籤，每個 hello hello VM 上裝載的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-397">This section contains an "Overview" and additional sub tabs for each of hello SQL Server instances hosted on hello VM.</span></span>

<span data-ttu-id="b7ba6-398">hello < 概觀 > 一節包含很有幫助的資料表，可總結所有 hello 實體磁碟 （系統和資料磁碟） 正在執行，且包含混合資料檔和交易記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-398">hello "Overview" section contains a helpful table that summarizes all hello physical disks (system and data disks) that are running and that contain a mixture of data files and transaction log files.</span></span>

<span data-ttu-id="b7ba6-399">在下列範例，hello *PhysicalDrive0* （執行 hello C 磁碟機） 會顯示，因為兩者 hello *modeldev*和*modellog*檔案位於 hello C 磁碟機，並他們屬於不同類型 (例如資料檔案和交易記錄檔，分別):</span><span class="sxs-lookup"><span data-stu-id="b7ba6-399">In hello following example, *PhysicalDrive0* (running hello C drive) is displayed because both hello *modeldev* and *modellog* files are located on hello C drive, and they are of different types (such as Data File and Transaction Log, respectively):</span></span>

![loginfo](media/how-to-use-perfInsights/loginfo.png)

<span data-ttu-id="b7ba6-401">hello SQL Server 執行個體特有的索引標籤包含一般的區段會顯示 hello 選執行個體的基本資訊以及進階的資訊，包括設定、 組態和使用者選項的其他章節。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-401">hello SQL Server instance-specific tabs contain a general section that displays basic information about hello selected instance and additional sections for advanced information, including Settings, Configurations, and User Options.</span></span>

## <a name="references-toohello-external-tools-used"></a><span data-ttu-id="b7ba6-402">參考用 toohello 外部工具</span><span class="sxs-lookup"><span data-stu-id="b7ba6-402">References toohello external tools used</span></span>

### <a name="diskspd"></a><span data-ttu-id="b7ba6-403">Diskspd</span><span class="sxs-lookup"><span data-stu-id="b7ba6-403">Diskspd</span></span>

<span data-ttu-id="b7ba6-404">DISKSPD 是儲存體負載產生器和效能測試工具從 hello Windows 和 Windows Server 和雲端伺服器基礎結構工程團隊。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-404">DISKSPD is a storage load generator and performance test tool from hello Windows and Windows Server and Cloud Server Infrastructure engineering teams.</span></span> <span data-ttu-id="b7ba6-405">如需詳細資訊，請參閱 [Diskspd](https://github.com/Microsoft/diskspd)。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-405">For more information, see [Diskspd](https://github.com/Microsoft/diskspd).</span></span>

### <a name="xperf"></a><span data-ttu-id="b7ba6-406">XPerf</span><span class="sxs-lookup"><span data-stu-id="b7ba6-406">XPerf</span></span>

<span data-ttu-id="b7ba6-407">Xperf 是從 Windows 效能工具套件 hello 命令列工具 toocapture 追蹤。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-407">Xperf is a command-line tool toocapture traces from hello Windows Performance Tools Kit.</span></span>

<span data-ttu-id="b7ba6-408">如需詳細資訊，請參閱 [Windows 效能工具組 – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/)。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-408">For more information, see [Windows Performance Toolkit – Xperf](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7ba6-409">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7ba6-409">Next Steps</span></span>

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a><span data-ttu-id="b7ba6-410">上傳診斷記錄和報告 tooMicrosoft 支援供進一步檢閱</span><span class="sxs-lookup"><span data-stu-id="b7ba6-410">Upload diagnostics logs and reports tooMicrosoft Support for further review</span></span>

<span data-ttu-id="b7ba6-411">當您使用 hello Microsoft 支援人員時，您可能要求的 tootransmit hello 輸出 PerfInsights tooassist hello 疑難排解程序所產生。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-411">When you work with hello Microsoft Support staff, you may be requested tootransmit hello output that is generated by PerfInsights tooassist hello troubleshooting process.</span></span>

<span data-ttu-id="b7ba6-412">hello 支援代理程式會建立 DTM 工作區，而且您會收到電子郵件訊息，其中包含連結 toohello [DTM 入口網站 (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) 以及唯一的使用者識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-412">hello Support agent will create a DTM workspace for you, and you will receive an email message that includes a link toohello [DTM portal (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) and a unique user ID and password.</span></span>

<span data-ttu-id="b7ba6-413">此訊息會從 **CTS 自動化診斷服務** (ctsadiag@microsoft.com) 傳送。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-413">This message will be sent from **CTS Automated Diagnostics Services** (ctsadiag@microsoft.com).</span></span>

![Hello 訊息的範例](media/how-to-use-perfInsights/supportemail.png)

<span data-ttu-id="b7ba6-415">為了增加安全性，您將會需要的 toochange 您密碼上的第一次使用。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-415">For additional security, you will be required toochange your password on first use.</span></span>

<span data-ttu-id="b7ba6-416">在您登入 tooDTM 之後，您會發現對話方塊方塊 tooupload hello **CollectedData\_yyyy MM dd\_hh\_公釐\_ss.zip** PerfInsights 收集的檔案。</span><span class="sxs-lookup"><span data-stu-id="b7ba6-416">After you log in tooDTM, you will find a dialog box tooupload hello **CollectedData\_yyyy-MM-dd\_hh\_mm\_ss.zip** file that was collected by PerfInsights.</span></span>
