---
title: "在 Azure 上資料庫 aaaDesign 和實作 Oracle |Microsoft 文件"
description: "在 Azure 環境中設計和實作 Oracle 資料庫。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="447bc-103">在 Azure 中設計和實作 Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="447bc-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="447bc-104">假設</span><span class="sxs-lookup"><span data-stu-id="447bc-104">Assumptions</span></span>

- <span data-ttu-id="447bc-105">您計劃 toomigrate 內部 tooAzure 從 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="447bc-105">You're planning toomigrate an Oracle database from on-premises tooAzure.</span></span>
- <span data-ttu-id="447bc-106">您了解的 hello 各種標準 Oracle AWR 報表中。</span><span class="sxs-lookup"><span data-stu-id="447bc-106">You have an understanding of hello various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="447bc-107">您已基本了解應用程式效能和平台使用量。</span><span class="sxs-lookup"><span data-stu-id="447bc-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="447bc-108">目標</span><span class="sxs-lookup"><span data-stu-id="447bc-108">Goals</span></span>

- <span data-ttu-id="447bc-109">了解如何 toooptimize Oracle 部署在 Azure 中的。</span><span class="sxs-lookup"><span data-stu-id="447bc-109">Understand how toooptimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="447bc-110">探索 Azure 環境中 Oracle 資料庫的效能調整選項。</span><span class="sxs-lookup"><span data-stu-id="447bc-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="447bc-111">hello 內部之間的差異和 Azure 的實作</span><span class="sxs-lookup"><span data-stu-id="447bc-111">hello differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="447bc-112">以下是一些重要事情 tookeep 記住，當您移轉內部部署應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="447bc-112">Following are some important things tookeep in mind when you're migrating on-premises applications tooAzure.</span></span> 

<span data-ttu-id="447bc-113">其中的一項重要差異是，Azure 實作中的資源 (例如 VM、磁碟和虛擬網路) 會與其他用戶端共用。</span><span class="sxs-lookup"><span data-stu-id="447bc-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="447bc-114">此外，資源可以進行節流處理 hello 需求為基礎。</span><span class="sxs-lookup"><span data-stu-id="447bc-114">In addition, resources can be throttled based on hello requirements.</span></span> <span data-ttu-id="447bc-115">而不是將焦點放在避免發生失敗 (MTBF)，Azure 更專注於存活 hello 失敗 (MTTR)。</span><span class="sxs-lookup"><span data-stu-id="447bc-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving hello failure (MTTR).</span></span>

<span data-ttu-id="447bc-116">hello 下表列出一些在內部部署實作和 Azure 的 Oracle 資料庫實作的 hello 差異。</span><span class="sxs-lookup"><span data-stu-id="447bc-116">hello following table lists some of hello differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="447bc-117">**內部部署實作**</span><span class="sxs-lookup"><span data-stu-id="447bc-117">**On-premises implementation**</span></span> | <span data-ttu-id="447bc-118">**Azure 實作**</span><span class="sxs-lookup"><span data-stu-id="447bc-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="447bc-119">**網路功能**</span><span class="sxs-lookup"><span data-stu-id="447bc-119">**Networking**</span></span> |<span data-ttu-id="447bc-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="447bc-120">LAN/WAN</span></span>  |<span data-ttu-id="447bc-121">SDN (軟體定義網路)</span><span class="sxs-lookup"><span data-stu-id="447bc-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="447bc-122">**安全性群組**</span><span class="sxs-lookup"><span data-stu-id="447bc-122">**Security group**</span></span> |<span data-ttu-id="447bc-123">IP/連接埠限制工具</span><span class="sxs-lookup"><span data-stu-id="447bc-123">IP/port restriction tools</span></span> |[<span data-ttu-id="447bc-124">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="447bc-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="447bc-125">**恢復功能**</span><span class="sxs-lookup"><span data-stu-id="447bc-125">**Resilience**</span></span> |<span data-ttu-id="447bc-126">MTBF (平均失敗時間)</span><span class="sxs-lookup"><span data-stu-id="447bc-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="447bc-127">MTTR (時間 toorecovery)</span><span class="sxs-lookup"><span data-stu-id="447bc-127">MTTR (mean time toorecovery)</span></span>|
> | <span data-ttu-id="447bc-128">**預定的維修**</span><span class="sxs-lookup"><span data-stu-id="447bc-128">**Planned maintenance**</span></span> |<span data-ttu-id="447bc-129">修補/升級</span><span class="sxs-lookup"><span data-stu-id="447bc-129">Patching/upgrades</span></span>|<span data-ttu-id="447bc-130">[可用性設定組](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (Azure 所管理的修補/升級)</span><span class="sxs-lookup"><span data-stu-id="447bc-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="447bc-131">**Resource**</span><span class="sxs-lookup"><span data-stu-id="447bc-131">**Resource**</span></span> |<span data-ttu-id="447bc-132">專用</span><span class="sxs-lookup"><span data-stu-id="447bc-132">Dedicated</span></span>  |<span data-ttu-id="447bc-133">與其他用戶端共用</span><span class="sxs-lookup"><span data-stu-id="447bc-133">Shared with other clients</span></span>|
> | <span data-ttu-id="447bc-134">**區域**</span><span class="sxs-lookup"><span data-stu-id="447bc-134">**Regions**</span></span> |<span data-ttu-id="447bc-135">資料中心</span><span class="sxs-lookup"><span data-stu-id="447bc-135">Datacenters</span></span> |[<span data-ttu-id="447bc-136">區域配對</span><span class="sxs-lookup"><span data-stu-id="447bc-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="447bc-137">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="447bc-137">**Storage**</span></span> |<span data-ttu-id="447bc-138">SAN/實體磁碟</span><span class="sxs-lookup"><span data-stu-id="447bc-138">SAN/physical disks</span></span> |[<span data-ttu-id="447bc-139">Azure 受管理儲存體</span><span class="sxs-lookup"><span data-stu-id="447bc-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="447bc-140">**調整**</span><span class="sxs-lookup"><span data-stu-id="447bc-140">**Scale**</span></span> |<span data-ttu-id="447bc-141">垂直調整</span><span class="sxs-lookup"><span data-stu-id="447bc-141">Vertical scale</span></span> |<span data-ttu-id="447bc-142">水平調整</span><span class="sxs-lookup"><span data-stu-id="447bc-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="447bc-143">需求</span><span class="sxs-lookup"><span data-stu-id="447bc-143">Requirements</span></span>

- <span data-ttu-id="447bc-144">決定 hello 資料庫大小和成長率。</span><span class="sxs-lookup"><span data-stu-id="447bc-144">Determine hello database size and growth rate.</span></span>
- <span data-ttu-id="447bc-145">判斷 hello IOPS 需求，您可以根據 Oracle AWR 報表或其他網路監視工具來估計。</span><span class="sxs-lookup"><span data-stu-id="447bc-145">Determine hello IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="447bc-146">組態選項</span><span class="sxs-lookup"><span data-stu-id="447bc-146">Configuration options</span></span>

<span data-ttu-id="447bc-147">有四個可能的區域，您可以微調 tooimprove Azure 環境中的效能：</span><span class="sxs-lookup"><span data-stu-id="447bc-147">There are four potential areas that you can tune tooimprove performance in an Azure environment:</span></span>

- <span data-ttu-id="447bc-148">虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="447bc-148">Virtual machine size</span></span>
- <span data-ttu-id="447bc-149">網路輸送量</span><span class="sxs-lookup"><span data-stu-id="447bc-149">Network throughput</span></span>
- <span data-ttu-id="447bc-150">磁碟類型和設定</span><span class="sxs-lookup"><span data-stu-id="447bc-150">Disk types and configurations</span></span>
- <span data-ttu-id="447bc-151">磁碟快取設定</span><span class="sxs-lookup"><span data-stu-id="447bc-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="447bc-152">產生 AWR 報表</span><span class="sxs-lookup"><span data-stu-id="447bc-152">Generate an AWR report</span></span>

<span data-ttu-id="447bc-153">如果您有現有的 Oracle 資料庫，並計劃 toomigrate tooAzure，您會有數個選項。</span><span class="sxs-lookup"><span data-stu-id="447bc-153">If you have an existing an Oracle database and are planning toomigrate tooAzure, you have several options.</span></span> <span data-ttu-id="447bc-154">您可以執行 hello Oracle AWR 報表 tooget hello 度量 （IOPS、 Mbps、 GiBs，等等）。</span><span class="sxs-lookup"><span data-stu-id="447bc-154">You can run hello Oracle AWR report tooget hello metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="447bc-155">然後選擇 的 hello VM 會根據您所收集的 hello 度量。</span><span class="sxs-lookup"><span data-stu-id="447bc-155">Then choose hello VM based on hello metrics that you collected.</span></span> <span data-ttu-id="447bc-156">或連絡您基礎結構小組 tooget 類似的資訊。</span><span class="sxs-lookup"><span data-stu-id="447bc-156">Or you can contact your infrastructure team tooget similar information.</span></span>

<span data-ttu-id="447bc-157">您可以考慮在一般和尖峰工作負載期間執行 AWR 報表，以進行比較。</span><span class="sxs-lookup"><span data-stu-id="447bc-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="447bc-158">根據這些報表，您可以調整大小的 Vm 依據 hello 平均工作負載或 hello 最大工作負載的 hello。</span><span class="sxs-lookup"><span data-stu-id="447bc-158">Based on these reports, you can size hello VMs based on either hello average workload or hello maximum workload.</span></span>

<span data-ttu-id="447bc-159">以下是如何的範例 toogenerate AWR 報表：</span><span class="sxs-lookup"><span data-stu-id="447bc-159">Following is an example of how toogenerate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="447bc-160">重要計量</span><span class="sxs-lookup"><span data-stu-id="447bc-160">Key metrics</span></span>

<span data-ttu-id="447bc-161">以下是您可以從 hello AWR 報表取得的 hello 度量：</span><span class="sxs-lookup"><span data-stu-id="447bc-161">Following are hello metrics that you can obtain from hello AWR report:</span></span>

- <span data-ttu-id="447bc-162">核心總數</span><span class="sxs-lookup"><span data-stu-id="447bc-162">Total number of cores</span></span>
- <span data-ttu-id="447bc-163">CPU 時脈速度</span><span class="sxs-lookup"><span data-stu-id="447bc-163">CPU clock speed</span></span>
- <span data-ttu-id="447bc-164">記憶體總計 (GB)</span><span class="sxs-lookup"><span data-stu-id="447bc-164">Total memory in GB</span></span>
- <span data-ttu-id="447bc-165">CPU 使用率</span><span class="sxs-lookup"><span data-stu-id="447bc-165">CPU utilization</span></span>
- <span data-ttu-id="447bc-166">尖峰資料傳送速率</span><span class="sxs-lookup"><span data-stu-id="447bc-166">Peak data transfer rate</span></span>
- <span data-ttu-id="447bc-167">I/O 變更率 (讀/寫)</span><span class="sxs-lookup"><span data-stu-id="447bc-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="447bc-168">重做記錄速率 (MBPs)</span><span class="sxs-lookup"><span data-stu-id="447bc-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="447bc-169">網路輸送量</span><span class="sxs-lookup"><span data-stu-id="447bc-169">Network throughput</span></span>
- <span data-ttu-id="447bc-170">網路延遲速率 (低/高)</span><span class="sxs-lookup"><span data-stu-id="447bc-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="447bc-171">資料庫大小 (GB)</span><span class="sxs-lookup"><span data-stu-id="447bc-171">Database size in GB</span></span>
- <span data-ttu-id="447bc-172">位元組收到透過 SQL * Net 從 / tooclient</span><span class="sxs-lookup"><span data-stu-id="447bc-172">Bytes received via SQL*Net from/tooclient</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="447bc-173">虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="447bc-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a><span data-ttu-id="447bc-174">1.估計的 VM 大小根據 CPU、 記憶體和 I/O 使用方式，從 hello AWR 報表</span><span class="sxs-lookup"><span data-stu-id="447bc-174">1. Estimate VM size based on CPU, memory, and I/O usage from hello AWR report</span></span>

<span data-ttu-id="447bc-175">您可能會看到一件事是 hello 前五個定時的前景事件，以指出 hello 系統瓶頸的所在。</span><span class="sxs-lookup"><span data-stu-id="447bc-175">One thing you might look at is hello top five timed foreground events that indicate where hello system bottlenecks are.</span></span>

<span data-ttu-id="447bc-176">比方說，在下列圖表 hello，hello 記錄檔案同步處理是在 hello 最上方。</span><span class="sxs-lookup"><span data-stu-id="447bc-176">For example, in hello following diagram, hello log file sync is at hello top.</span></span> <span data-ttu-id="447bc-177">它會指出等候之前 hello LGWR 寫入 hello 記錄緩衝區 toohello 重做記錄檔所需的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="447bc-177">It indicates hello number of waits that are required before hello LGWR writes hello log buffer toohello redo log file.</span></span> <span data-ttu-id="447bc-178">這些結果代表您需要效能更好的儲存體或磁碟。</span><span class="sxs-lookup"><span data-stu-id="447bc-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="447bc-179">此外，hello 圖表也會顯示 hello CPU （核心） 的數目和記憶體的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="447bc-179">In addition, hello diagram also shows hello number of CPU (cores) and hello amount of memory.</span></span>

![Hello AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="447bc-181">hello 下列圖表顯示 hello 總 I/O 的讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="447bc-181">hello following diagram shows hello total I/O of read and write.</span></span> <span data-ttu-id="447bc-182">沒有 59 GB，讀取和寫入 hello hello 報表階段期間的 247.3 GB。</span><span class="sxs-lookup"><span data-stu-id="447bc-182">There were 59 GB read and 247.3 GB written during hello time of hello report.</span></span>

![Hello AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="447bc-184">2.選擇 VM</span><span class="sxs-lookup"><span data-stu-id="447bc-184">2. Choose a VM</span></span>

<span data-ttu-id="447bc-185">根據您從 hello AWR 報表收集到的 hello 資訊，hello 下一個步驟是大小的 toochoose 類似符合您需求的 VM。</span><span class="sxs-lookup"><span data-stu-id="447bc-185">Based on hello information that you collected from hello AWR report, hello next step is toochoose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="447bc-186">您可以在 hello 文件中找到可用 Vm 的清單[記憶體最佳化](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory)。</span><span class="sxs-lookup"><span data-stu-id="447bc-186">You can find a list of available VMs in hello article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a><span data-ttu-id="447bc-187">3.使用類似的 VM 系列，根據 hello ACU 微調 hello VM 大小</span><span class="sxs-lookup"><span data-stu-id="447bc-187">3. Fine-tune hello VM sizing with a similar VM series based on hello ACU</span></span>

<span data-ttu-id="447bc-188">您選擇 hello VM 之後，請特別注意 toohello ACU hello VM。</span><span class="sxs-lookup"><span data-stu-id="447bc-188">After you've chosen hello VM, pay attention toohello ACU for hello VM.</span></span> <span data-ttu-id="447bc-189">您可以選擇不同的 VM 依據 hello ACU 值更符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="447bc-189">You might choose a different VM based on hello ACU value that better suits your requirements.</span></span> <span data-ttu-id="447bc-190">如需詳細資訊，請參閱 [Azure 計算單位](https://docs.microsoft.com/azure/virtual-machines/windows/acu)。</span><span class="sxs-lookup"><span data-stu-id="447bc-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Hello ACU 單位頁面的螢幕擷取畫面](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="447bc-192">網路輸送量</span><span class="sxs-lookup"><span data-stu-id="447bc-192">Network throughput</span></span>

<span data-ttu-id="447bc-193">下列圖表顯示 hello 關聯性之間的輸送量和 IOPS 的 hello:</span><span class="sxs-lookup"><span data-stu-id="447bc-193">hello following diagram shows hello relation between throughput and IOPS:</span></span>

![輸送量的螢幕擷取畫面](./media/oracle-design/throughput.png)

<span data-ttu-id="447bc-195">hello 整體網路輸送量估計根據 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="447bc-195">hello total network throughput is estimated based on hello following information:</span></span>
- <span data-ttu-id="447bc-196">SQL*Net 流量</span><span class="sxs-lookup"><span data-stu-id="447bc-196">SQL*Net traffic</span></span>
- <span data-ttu-id="447bc-197">MBps x 伺服器數目 (輸出串流，例如 Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="447bc-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="447bc-198">其他因素，例如應用程式複寫</span><span class="sxs-lookup"><span data-stu-id="447bc-198">Other factors, such as application replication</span></span>

![螢幕擷取畫面的 hello SQL * Net 輸送量](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="447bc-200">根據您的網路頻寬需求，有各種 toochoose 從閘道類型。</span><span class="sxs-lookup"><span data-stu-id="447bc-200">Based on your network bandwidth requirements, there are various gateway types for you toochoose from.</span></span> <span data-ttu-id="447bc-201">這些類型包括基本、VpnGw 和 Azure ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="447bc-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="447bc-202">如需詳細資訊，請參閱 hello [VPN 閘道定價頁面](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h)。</span><span class="sxs-lookup"><span data-stu-id="447bc-202">For more information, see hello [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="447bc-203">**建議**</span><span class="sxs-lookup"><span data-stu-id="447bc-203">**Recommendations**</span></span>

- <span data-ttu-id="447bc-204">網路延遲為更高版本的比較的 tooan 內部部署。</span><span class="sxs-lookup"><span data-stu-id="447bc-204">Network latency is higher compared tooan on-premises deployment.</span></span> <span data-ttu-id="447bc-205">減少網路來回行程可以大幅改善效能。</span><span class="sxs-lookup"><span data-stu-id="447bc-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="447bc-206">tooreduce 往返，彙總 hello 有高交易或 「 多對話 」 應用程式的應用程式相同的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="447bc-206">tooreduce round-trips, consolidate applications that have high transactions or “chatty” apps on hello same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="447bc-207">磁碟類型和設定</span><span class="sxs-lookup"><span data-stu-id="447bc-207">Disk types and configurations</span></span>

- <span data-ttu-id="447bc-208">預設的 OS 磁碟：這些磁碟類型可提供持續性資料和快取。</span><span class="sxs-lookup"><span data-stu-id="447bc-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="447bc-209">它們最適合用在啟動時的 OS 存取，但其設計目的並非用於交易式或資料倉儲 (分析) 工作負載。</span><span class="sxs-lookup"><span data-stu-id="447bc-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="447bc-210">*Unmanaged 磁碟*： 您可以使用 [磁碟] 類型，這些管理 hello 儲存 hello 對應 tooyour VM 磁碟的虛擬硬碟 (VHD) 檔案的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="447bc-210">*Unmanaged disks*: With these disk types, you manage hello storage accounts that store hello virtual hard disk (VHD) files that correspond tooyour VM disks.</span></span> <span data-ttu-id="447bc-211">VHD 檔案會以分頁 Blob 的形式儲存在 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="447bc-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="447bc-212">*管理磁碟*: Azure 管理您使用的 VM 磁碟的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="447bc-212">*Managed disks*: Azure manages hello storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="447bc-213">指定 hello 磁碟類型 （高階或標準） 以及您需要的 hello 磁碟 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="447bc-213">You specify hello disk type (premium or standard) and hello size of hello disk that you need.</span></span> <span data-ttu-id="447bc-214">Azure 會建立，並會為您管理 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="447bc-214">Azure creates and manages hello disk for you.</span></span>

- <span data-ttu-id="447bc-215">進階儲存體磁碟：這些磁碟類型最適合生產工作負載使用。</span><span class="sxs-lookup"><span data-stu-id="447bc-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="447bc-216">Premium 儲存體支援的 VM 磁碟可以是附加 toospecific 大小系列 Vm，例如 DS、 DSv2、 GS 和 F 系列 Vm。</span><span class="sxs-lookup"><span data-stu-id="447bc-216">Premium storage supports VM disks that can be attached toospecific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="447bc-217">hello premium 磁碟隨附不同的大小，而且您可以選擇介於 32 GB too4，096 GB 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="447bc-217">hello premium disk comes with different sizes, and you can choose between disks ranging from 32 GB too4,096 GB.</span></span> <span data-ttu-id="447bc-218">每個磁碟大小都有自己的效能規格。</span><span class="sxs-lookup"><span data-stu-id="447bc-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="447bc-219">根據您的應用程式需求，您可以附加一或多個磁碟 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="447bc-219">Depending on your application requirements, you can attach one or more disks tooyour VM.</span></span>

<span data-ttu-id="447bc-220">當您從 hello 入口網站建立新的受管理的磁碟時，您可以選擇 hello**帳戶類型**想 toouse hello 類型的磁碟。</span><span class="sxs-lookup"><span data-stu-id="447bc-220">When you create a new managed disk from hello portal, you can choose hello **Account type** for hello type of disk you want toouse.</span></span> <span data-ttu-id="447bc-221">請記住，並非所有可用的磁碟所示 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="447bc-221">Keep in mind that not all available disks are shown in hello drop-down menu.</span></span> <span data-ttu-id="447bc-222">您選擇特定的 VM 大小之後，hello 功能表會顯示 hello 可用的 premium 儲存體為基礎的 VM 大小的 Sku。</span><span class="sxs-lookup"><span data-stu-id="447bc-222">After you choose a particular VM size, hello menu shows only hello available premium storage SKUs that are based on that VM size.</span></span>

![Hello 受管理的磁碟 頁面的螢幕擷取畫面](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="447bc-224">如需詳細資訊，請參閱 [VM 高效能進階儲存體與受控磁碟](https://docs.microsoft.com/azure/storage/storage-premium-storage)。</span><span class="sxs-lookup"><span data-stu-id="447bc-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="447bc-225">在 VM 上設定您的儲存體之後，您可能想 tooload 測試 hello 磁碟之前建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="447bc-225">After you configure your storage on a VM, you might want tooload test hello disks before creating a database.</span></span> <span data-ttu-id="447bc-226">了解 hello 延遲和輸送量方面的 I/O 速率可協助您判斷如果 hello Vm 支援 hello 預期輸送量，而延遲的目標。</span><span class="sxs-lookup"><span data-stu-id="447bc-226">Knowing hello I/O rate in terms of both latency and throughput can help you determine if hello VMs support hello expected throughput with latency targets.</span></span>

<span data-ttu-id="447bc-227">有數種工具可以進行應用程式負載測試，例如 Oracle Orion、Sysbench 和 Fio。</span><span class="sxs-lookup"><span data-stu-id="447bc-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="447bc-228">在部署 Oracle 資料庫之後，再次執行 hello 負載測試。</span><span class="sxs-lookup"><span data-stu-id="447bc-228">Run hello load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="447bc-229">啟動您的規則和尖峰工作負載，而且 hello 結果顯示 hello 環境的基準。</span><span class="sxs-lookup"><span data-stu-id="447bc-229">Start your regular and peak workloads, and hello results show you hello baseline of your environment.</span></span>

<span data-ttu-id="447bc-230">它可能會更重要的 hello IOPS 速率，而不是 hello 儲存體大小為基礎的 toosize hello 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="447bc-230">It might be more important toosize hello storage based on hello IOPS rate rather than hello storage size.</span></span> <span data-ttu-id="447bc-231">例如，如果 hello 需要 IOPS 為 5000，但是您只需要 200 GB，可能仍可使用 hello P30 類別高階磁碟即使這樣有 200 GB 以上的儲存體。</span><span class="sxs-lookup"><span data-stu-id="447bc-231">For example, if hello required IOPS is 5,000, but you only need 200 GB, you might still get hello P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="447bc-232">hello IOPS 速率可以取自 hello AWR 報表。</span><span class="sxs-lookup"><span data-stu-id="447bc-232">hello IOPS rate can be obtained from hello AWR report.</span></span> <span data-ttu-id="447bc-233">而是由決定 hello 重做記錄檔、 實體的讀取和寫入的速率。</span><span class="sxs-lookup"><span data-stu-id="447bc-233">It's determined by hello redo log, physical reads, and writes rate.</span></span>

![Hello AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/awr_report.png)

<span data-ttu-id="447bc-235">例如，hello 重做大小為 12,200,000 位元組 / 秒，也就是等於 too11.63 MBPs。</span><span class="sxs-lookup"><span data-stu-id="447bc-235">For example, hello redo size is 12,200,000 bytes per second, which is equal too11.63 MBPs.</span></span>
<span data-ttu-id="447bc-236">hello IOPS 是 12200000 / 2,358 = 5,174。</span><span class="sxs-lookup"><span data-stu-id="447bc-236">hello IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="447bc-237">清楚地了解的 hello I/O 需求之後，您可以選擇最適合的 toomeet 的磁碟機的組合這些需求。</span><span class="sxs-lookup"><span data-stu-id="447bc-237">After you have a clear picture of hello I/O requirements, you can choose a combination of drives that are best suited toomeet those requirements.</span></span>

<span data-ttu-id="447bc-238">**建議**</span><span class="sxs-lookup"><span data-stu-id="447bc-238">**Recommendations**</span></span>

- <span data-ttu-id="447bc-239">針對資料的資料表空間分散 hello I/O 工作負載的磁碟數目使用受管理存放裝置或 Oracle ASM。</span><span class="sxs-lookup"><span data-stu-id="447bc-239">For data tablespace, spread hello I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="447bc-240">隨著 hello I/O 區塊大小增加為大量讀取和寫入密集作業，加入更多的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="447bc-240">As hello I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="447bc-241">提高大型循序處理程序的 hello 區塊大小。</span><span class="sxs-lookup"><span data-stu-id="447bc-241">Increase hello block size for large sequential processes.</span></span>
- <span data-ttu-id="447bc-242">使用資料壓縮 tooreduce I/O （針對資料和索引）。</span><span class="sxs-lookup"><span data-stu-id="447bc-242">Use data compression tooreduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="447bc-243">區隔不同資料磁碟上的重做記錄、系統、暫時和重做 TS。</span><span class="sxs-lookup"><span data-stu-id="447bc-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="447bc-244">不要將任何應用程式檔案放在預設 OS 磁碟 (/dev/sda)。</span><span class="sxs-lookup"><span data-stu-id="447bc-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="447bc-245">這些磁碟不適合用於快速 VM 啟動階段，因此可能不會為您的應用程式提供良好的效能。</span><span class="sxs-lookup"><span data-stu-id="447bc-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="447bc-246">磁碟快取設定</span><span class="sxs-lookup"><span data-stu-id="447bc-246">Disk cache settings</span></span>

<span data-ttu-id="447bc-247">有三個主機快取選項：</span><span class="sxs-lookup"><span data-stu-id="447bc-247">There are three options for host caching:</span></span>

- <span data-ttu-id="447bc-248">唯讀：快取所有要求，以供未來讀取。</span><span class="sxs-lookup"><span data-stu-id="447bc-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="447bc-249">會保存所有寫入直接 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="447bc-249">All writes are persisted directly tooAzure Blob storage.</span></span>

- <span data-ttu-id="447bc-250">讀寫：這是「預先讀取」演算法。</span><span class="sxs-lookup"><span data-stu-id="447bc-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="447bc-251">hello 讀取和寫入快取供後續的讀取。</span><span class="sxs-lookup"><span data-stu-id="447bc-251">hello reads and writes are cached for future reads.</span></span> <span data-ttu-id="447bc-252">非直接寫入式寫入為先保存 toohello 本機快取。</span><span class="sxs-lookup"><span data-stu-id="447bc-252">Non-write-through writes are persisted toohello local cache first.</span></span> <span data-ttu-id="447bc-253">For SQL Server 寫入為保存的 tooAzure 儲存體，因為它會貫穿式寫入使用。</span><span class="sxs-lookup"><span data-stu-id="447bc-253">For SQL Server, writes are persisted tooAzure Storage because it uses write-through.</span></span> <span data-ttu-id="447bc-254">它也會提供輕的工作負載的最低磁碟延遲 hello。</span><span class="sxs-lookup"><span data-stu-id="447bc-254">It also provides hello lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="447bc-255">*無*（停用）： 使用此選項，您可以略過 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="447bc-255">*None* (disabled): By using this option, you can bypass hello cache.</span></span> <span data-ttu-id="447bc-256">所有 hello 傳送的 toodisk 及資料保存 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="447bc-256">All hello data is transferred toodisk and persisted tooAzure Storage.</span></span> <span data-ttu-id="447bc-257">這個方法提供下列 hello I/O 密集型工作負載的最高的 I/O 速率。</span><span class="sxs-lookup"><span data-stu-id="447bc-257">This method gives you hello highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="447bc-258">您也需要 tootake 」 交易成本 」 納入考量。</span><span class="sxs-lookup"><span data-stu-id="447bc-258">You also need tootake “transaction cost” into consideration.</span></span>

<span data-ttu-id="447bc-259">**建議**</span><span class="sxs-lookup"><span data-stu-id="447bc-259">**Recommendations**</span></span>

<span data-ttu-id="447bc-260">toomaximize hello 輸送量，建議您開始使用**無**主機快取。</span><span class="sxs-lookup"><span data-stu-id="447bc-260">toomaximize hello throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="447bc-261">Premium 儲存體，請記住，您必須停用 hello 「 屏障 」 時掛接 hello 檔案系統與 hello **ReadOnly**或**無**選項。</span><span class="sxs-lookup"><span data-stu-id="447bc-261">For Premium Storage, keep in mind that you must disable hello "barriers" when you mount hello file system with hello **ReadOnly** or **None** options.</span></span> <span data-ttu-id="447bc-262">更新 hello /etc/fstab hello UUID toohello 磁碟檔案。</span><span class="sxs-lookup"><span data-stu-id="447bc-262">Update hello /etc/fstab file with hello UUID toohello disks.</span></span>

<span data-ttu-id="447bc-263">如需詳細資訊，請參閱[適用於 Linux VM 的進階儲存體](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms)。</span><span class="sxs-lookup"><span data-stu-id="447bc-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Hello 受管理的磁碟 頁面的螢幕擷取畫面](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="447bc-265">針對 OS 磁碟，使用預設的 [讀取/寫入] 快取。</span><span class="sxs-lookup"><span data-stu-id="447bc-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="447bc-266">針對 SYSTEM、TEMP 和 UNDO，對快取功能使用 [無]。</span><span class="sxs-lookup"><span data-stu-id="447bc-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="447bc-267">針對 DATA，對快取功能使用 [無]。</span><span class="sxs-lookup"><span data-stu-id="447bc-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="447bc-268">但是，如果您的資料庫是唯讀或讀取密集，請使用 [唯讀] 快取。</span><span class="sxs-lookup"><span data-stu-id="447bc-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="447bc-269">儲存您的資料磁碟的設定之後，您就無法變更 hello 主機快取設定，除非您卸載在 hello 作業系統層級的 hello 磁碟機，並再重新掛接它之後所做變更的 hello。</span><span class="sxs-lookup"><span data-stu-id="447bc-269">After your data disk setting is saved, you can't change hello host cache setting unless you unmount hello drive at hello OS level and then remount it after you've made hello change.</span></span>


## <a name="security"></a><span data-ttu-id="447bc-270">安全性</span><span class="sxs-lookup"><span data-stu-id="447bc-270">Security</span></span>

<span data-ttu-id="447bc-271">您已安裝並設定 Azure 環境後，hello 下一個步驟是 toosecure 您的網路。</span><span class="sxs-lookup"><span data-stu-id="447bc-271">After you have set up and configured your Azure environment, hello next step is toosecure your network.</span></span> <span data-ttu-id="447bc-272">以下是一些建議：</span><span class="sxs-lookup"><span data-stu-id="447bc-272">Here are some recommendations:</span></span>

- <span data-ttu-id="447bc-273">NSG 原則：可以透過子網路或 NIC 來定義 NSG。</span><span class="sxs-lookup"><span data-stu-id="447bc-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="447bc-274">在 hello 子網路層級安全性和強制的路由項目 （例如防火牆） 應用程式的較簡單 toocontrol 存取它。</span><span class="sxs-lookup"><span data-stu-id="447bc-274">It's simpler toocontrol access at hello subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="447bc-275">*Jumpbox*： 更安全的存取，系統管理員不應直接連接 toohello 應用程式服務或資料庫。</span><span class="sxs-lookup"><span data-stu-id="447bc-275">*Jumpbox*: For more secure access, administrators should not directly connect toohello application service or database.</span></span> <span data-ttu-id="447bc-276">Jumpbox 做為 hello 管理員機器之間的 Azure 資源的媒體。</span><span class="sxs-lookup"><span data-stu-id="447bc-276">A jumpbox is used as a media between hello administrator machine and Azure resources.</span></span>
<span data-ttu-id="447bc-277">![Hello Jumpbox 拓樸 頁面的螢幕擷取畫面](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="447bc-277">![Screenshot of hello Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="447bc-278">hello 管理員電腦應該提供 IP 限制存取 toohello jumpbox 只。</span><span class="sxs-lookup"><span data-stu-id="447bc-278">hello administrator machine should offer IP-restricted access toohello jumpbox only.</span></span> <span data-ttu-id="447bc-279">hello jumpbox 應有存取 toohello 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="447bc-279">hello jumpbox should have access toohello application and database.</span></span>

- <span data-ttu-id="447bc-280">*私人網路*（子網路）： 我們建議，您擁有 hello 應用程式服務和資料庫上不同的子網路，因此 NSG 原則可以設定更好的控制。</span><span class="sxs-lookup"><span data-stu-id="447bc-280">*Private network* (subnets): We recommend that you have hello application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="447bc-281">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="447bc-281">Additional reading</span></span>

- [<span data-ttu-id="447bc-282">設定 Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="447bc-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="447bc-283">設定 Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="447bc-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="447bc-284">設定 Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="447bc-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="447bc-285">Oracle 備份和復原</span><span class="sxs-lookup"><span data-stu-id="447bc-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="447bc-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="447bc-286">Next steps</span></span>

- [<span data-ttu-id="447bc-287">教學課程︰建立高可用性 VM</span><span class="sxs-lookup"><span data-stu-id="447bc-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="447bc-288">瀏覽 VM 部署 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="447bc-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
