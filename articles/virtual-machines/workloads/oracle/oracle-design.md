---
title: "在 Azure 上設計和實作 Oracle 資料庫 | Microsoft Docs"
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
ms.openlocfilehash: 1af7e1d40a0eb129875dd6a30ac899f2025bee13
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="90035-103">在 Azure 中設計和實作 Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="90035-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="90035-104">假設</span><span class="sxs-lookup"><span data-stu-id="90035-104">Assumptions</span></span>

- <span data-ttu-id="90035-105">您打算將 Oracle 資料庫從內部部署環境移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="90035-105">You're planning to migrate an Oracle database from on-premises to Azure.</span></span>
- <span data-ttu-id="90035-106">您已了解 Oracle AWR 報表中的各種計量。</span><span class="sxs-lookup"><span data-stu-id="90035-106">You have an understanding of the various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="90035-107">您已基本了解應用程式效能和平台使用量。</span><span class="sxs-lookup"><span data-stu-id="90035-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="90035-108">目標</span><span class="sxs-lookup"><span data-stu-id="90035-108">Goals</span></span>

- <span data-ttu-id="90035-109">了解如何將 Azure 中的 Oracle 部署最佳化。</span><span class="sxs-lookup"><span data-stu-id="90035-109">Understand how to optimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="90035-110">探索 Azure 環境中 Oracle 資料庫的效能調整選項。</span><span class="sxs-lookup"><span data-stu-id="90035-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="the-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="90035-111">內部部署和 Azure 實作之間的差異</span><span class="sxs-lookup"><span data-stu-id="90035-111">The differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="90035-112">以下是一些您在將內部部署應用程式移轉至 Azure 時應該謹記的重要事項。</span><span class="sxs-lookup"><span data-stu-id="90035-112">Following are some important things to keep in mind when you're migrating on-premises applications to Azure.</span></span> 

<span data-ttu-id="90035-113">其中的一項重要差異是，Azure 實作中的資源 (例如 VM、磁碟和虛擬網路) 會與其他用戶端共用。</span><span class="sxs-lookup"><span data-stu-id="90035-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="90035-114">此外，您可以根據需求來節流資源。</span><span class="sxs-lookup"><span data-stu-id="90035-114">In addition, resources can be throttled based on the requirements.</span></span> <span data-ttu-id="90035-115">Azure 更聚焦在讓失敗存活 (MTTR)，而不是聚焦於避免失敗 (MTBF)。</span><span class="sxs-lookup"><span data-stu-id="90035-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving the failure (MTTR).</span></span>

<span data-ttu-id="90035-116">下表列出 Oracle 資料庫在內部部署實作和 Azure 實作之間的一些差異。</span><span class="sxs-lookup"><span data-stu-id="90035-116">The following table lists some of the differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="90035-117">**內部部署實作**</span><span class="sxs-lookup"><span data-stu-id="90035-117">**On-premises implementation**</span></span> | <span data-ttu-id="90035-118">**Azure 實作**</span><span class="sxs-lookup"><span data-stu-id="90035-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="90035-119">**網路功能**</span><span class="sxs-lookup"><span data-stu-id="90035-119">**Networking**</span></span> |<span data-ttu-id="90035-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="90035-120">LAN/WAN</span></span>  |<span data-ttu-id="90035-121">SDN (軟體定義網路)</span><span class="sxs-lookup"><span data-stu-id="90035-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="90035-122">**安全性群組**</span><span class="sxs-lookup"><span data-stu-id="90035-122">**Security group**</span></span> |<span data-ttu-id="90035-123">IP/連接埠限制工具</span><span class="sxs-lookup"><span data-stu-id="90035-123">IP/port restriction tools</span></span> |[<span data-ttu-id="90035-124">網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="90035-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="90035-125">**恢復功能**</span><span class="sxs-lookup"><span data-stu-id="90035-125">**Resilience**</span></span> |<span data-ttu-id="90035-126">MTBF (平均失敗時間)</span><span class="sxs-lookup"><span data-stu-id="90035-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="90035-127">MTTR (平均復原時間)</span><span class="sxs-lookup"><span data-stu-id="90035-127">MTTR (mean time to recovery)</span></span>|
> | <span data-ttu-id="90035-128">**預定的維修**</span><span class="sxs-lookup"><span data-stu-id="90035-128">**Planned maintenance**</span></span> |<span data-ttu-id="90035-129">修補/升級</span><span class="sxs-lookup"><span data-stu-id="90035-129">Patching/upgrades</span></span>|<span data-ttu-id="90035-130">[可用性設定組](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (Azure 所管理的修補/升級)</span><span class="sxs-lookup"><span data-stu-id="90035-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="90035-131">**Resource**</span><span class="sxs-lookup"><span data-stu-id="90035-131">**Resource**</span></span> |<span data-ttu-id="90035-132">專用</span><span class="sxs-lookup"><span data-stu-id="90035-132">Dedicated</span></span>  |<span data-ttu-id="90035-133">與其他用戶端共用</span><span class="sxs-lookup"><span data-stu-id="90035-133">Shared with other clients</span></span>|
> | <span data-ttu-id="90035-134">**區域**</span><span class="sxs-lookup"><span data-stu-id="90035-134">**Regions**</span></span> |<span data-ttu-id="90035-135">資料中心</span><span class="sxs-lookup"><span data-stu-id="90035-135">Datacenters</span></span> |[<span data-ttu-id="90035-136">區域配對</span><span class="sxs-lookup"><span data-stu-id="90035-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="90035-137">**儲存體**</span><span class="sxs-lookup"><span data-stu-id="90035-137">**Storage**</span></span> |<span data-ttu-id="90035-138">SAN/實體磁碟</span><span class="sxs-lookup"><span data-stu-id="90035-138">SAN/physical disks</span></span> |[<span data-ttu-id="90035-139">Azure 受管理儲存體</span><span class="sxs-lookup"><span data-stu-id="90035-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="90035-140">**調整**</span><span class="sxs-lookup"><span data-stu-id="90035-140">**Scale**</span></span> |<span data-ttu-id="90035-141">垂直調整</span><span class="sxs-lookup"><span data-stu-id="90035-141">Vertical scale</span></span> |<span data-ttu-id="90035-142">水平調整</span><span class="sxs-lookup"><span data-stu-id="90035-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="90035-143">需求</span><span class="sxs-lookup"><span data-stu-id="90035-143">Requirements</span></span>

- <span data-ttu-id="90035-144">決定資料庫大小和成長率。</span><span class="sxs-lookup"><span data-stu-id="90035-144">Determine the database size and growth rate.</span></span>
- <span data-ttu-id="90035-145">決定 IOPS 需求，您可以根據 Oracle AWR 報表或其他網路監視工具進行評估。</span><span class="sxs-lookup"><span data-stu-id="90035-145">Determine the IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="90035-146">組態選項</span><span class="sxs-lookup"><span data-stu-id="90035-146">Configuration options</span></span>

<span data-ttu-id="90035-147">有四個可能的區域可供您進行調整，以改善 Azure 環境中的效能：</span><span class="sxs-lookup"><span data-stu-id="90035-147">There are four potential areas that you can tune to improve performance in an Azure environment:</span></span>

- <span data-ttu-id="90035-148">虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="90035-148">Virtual machine size</span></span>
- <span data-ttu-id="90035-149">網路輸送量</span><span class="sxs-lookup"><span data-stu-id="90035-149">Network throughput</span></span>
- <span data-ttu-id="90035-150">磁碟類型和設定</span><span class="sxs-lookup"><span data-stu-id="90035-150">Disk types and configurations</span></span>
- <span data-ttu-id="90035-151">磁碟快取設定</span><span class="sxs-lookup"><span data-stu-id="90035-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="90035-152">產生 AWR 報表</span><span class="sxs-lookup"><span data-stu-id="90035-152">Generate an AWR report</span></span>

<span data-ttu-id="90035-153">如果您目前已有 Oracle 資料庫，且打算移轉至 Azure，您會有數個選項。</span><span class="sxs-lookup"><span data-stu-id="90035-153">If you have an existing an Oracle database and are planning to migrate to Azure, you have several options.</span></span> <span data-ttu-id="90035-154">您可以執行 Oracle AWR 報表來取得計量 (IOPS、Mbps、GiB 等)。</span><span class="sxs-lookup"><span data-stu-id="90035-154">You can run the Oracle AWR report to get the metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="90035-155">然後根據收集到的計量選擇 VM。</span><span class="sxs-lookup"><span data-stu-id="90035-155">Then choose the VM based on the metrics that you collected.</span></span> <span data-ttu-id="90035-156">或者，連絡基礎結構小組，取得類似的資訊。</span><span class="sxs-lookup"><span data-stu-id="90035-156">Or you can contact your infrastructure team to get similar information.</span></span>

<span data-ttu-id="90035-157">您可以考慮在一般和尖峰工作負載期間執行 AWR 報表，以進行比較。</span><span class="sxs-lookup"><span data-stu-id="90035-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="90035-158">根據這些報表，您可以根據平均工作負載或最大工作負載來調整 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="90035-158">Based on these reports, you can size the VMs based on either the average workload or the maximum workload.</span></span>

<span data-ttu-id="90035-159">以下是如何產生 AWR 報表的範例：</span><span class="sxs-lookup"><span data-stu-id="90035-159">Following is an example of how to generate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="90035-160">重要計量</span><span class="sxs-lookup"><span data-stu-id="90035-160">Key metrics</span></span>

<span data-ttu-id="90035-161">以下是您可以從 AWR 報表取得的計量：</span><span class="sxs-lookup"><span data-stu-id="90035-161">Following are the metrics that you can obtain from the AWR report:</span></span>

- <span data-ttu-id="90035-162">核心總數</span><span class="sxs-lookup"><span data-stu-id="90035-162">Total number of cores</span></span>
- <span data-ttu-id="90035-163">CPU 時脈速度</span><span class="sxs-lookup"><span data-stu-id="90035-163">CPU clock speed</span></span>
- <span data-ttu-id="90035-164">記憶體總計 (GB)</span><span class="sxs-lookup"><span data-stu-id="90035-164">Total memory in GB</span></span>
- <span data-ttu-id="90035-165">CPU 使用率</span><span class="sxs-lookup"><span data-stu-id="90035-165">CPU utilization</span></span>
- <span data-ttu-id="90035-166">尖峰資料傳送速率</span><span class="sxs-lookup"><span data-stu-id="90035-166">Peak data transfer rate</span></span>
- <span data-ttu-id="90035-167">I/O 變更率 (讀/寫)</span><span class="sxs-lookup"><span data-stu-id="90035-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="90035-168">重做記錄速率 (MBPs)</span><span class="sxs-lookup"><span data-stu-id="90035-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="90035-169">網路輸送量</span><span class="sxs-lookup"><span data-stu-id="90035-169">Network throughput</span></span>
- <span data-ttu-id="90035-170">網路延遲速率 (低/高)</span><span class="sxs-lookup"><span data-stu-id="90035-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="90035-171">資料庫大小 (GB)</span><span class="sxs-lookup"><span data-stu-id="90035-171">Database size in GB</span></span>
- <span data-ttu-id="90035-172">透過 SQL*Net 從/至用戶端收到的位元組</span><span class="sxs-lookup"><span data-stu-id="90035-172">Bytes received via SQL*Net from/to client</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="90035-173">虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="90035-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-the-awr-report"></a><span data-ttu-id="90035-174">1.根據 AWR 報表中的 CPU、記憶體和 I/O 使用量來預估 VM 大小</span><span class="sxs-lookup"><span data-stu-id="90035-174">1. Estimate VM size based on CPU, memory, and I/O usage from the AWR report</span></span>

<span data-ttu-id="90035-175">您可以查看的一個事項是前五個定時前景事件，其指出系統瓶頸位置。</span><span class="sxs-lookup"><span data-stu-id="90035-175">One thing you might look at is the top five timed foreground events that indicate where the system bottlenecks are.</span></span>

<span data-ttu-id="90035-176">例如在下圖中，記錄檔案同步在頂端。</span><span class="sxs-lookup"><span data-stu-id="90035-176">For example, in the following diagram, the log file sync is at the top.</span></span> <span data-ttu-id="90035-177">這代表等候 LGWR 將記錄緩衝區寫入重做記錄檔的次數。</span><span class="sxs-lookup"><span data-stu-id="90035-177">It indicates the number of waits that are required before the LGWR writes the log buffer to the redo log file.</span></span> <span data-ttu-id="90035-178">這些結果代表您需要效能更好的儲存體或磁碟。</span><span class="sxs-lookup"><span data-stu-id="90035-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="90035-179">此外，此圖也會顯示 CPU (核心) 數目和記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="90035-179">In addition, the diagram also shows the number of CPU (cores) and the amount of memory.</span></span>

![AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="90035-181">下圖顯示讀取和寫入的 I/O 總計。</span><span class="sxs-lookup"><span data-stu-id="90035-181">The following diagram shows the total I/O of read and write.</span></span> <span data-ttu-id="90035-182">報表統計期間共有 59 GB 的讀取和 247.3 GB 的寫入。</span><span class="sxs-lookup"><span data-stu-id="90035-182">There were 59 GB read and 247.3 GB written during the time of the report.</span></span>

![AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="90035-184">2.選擇 VM</span><span class="sxs-lookup"><span data-stu-id="90035-184">2. Choose a VM</span></span>

<span data-ttu-id="90035-185">根據您從 AWR 報表收集到的資訊，下一個步驟是選擇符合您需求且大小類似的 VM。</span><span class="sxs-lookup"><span data-stu-id="90035-185">Based on the information that you collected from the AWR report, the next step is to choose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="90035-186">您可以在[記憶體最佳化](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory)一文中找到可用 VM 的清單。</span><span class="sxs-lookup"><span data-stu-id="90035-186">You can find a list of available VMs in the article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-the-vm-sizing-with-a-similar-vm-series-based-on-the-acu"></a><span data-ttu-id="90035-187">3.根據 ACU 微調類似 VM 系列的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="90035-187">3. Fine-tune the VM sizing with a similar VM series based on the ACU</span></span>

<span data-ttu-id="90035-188">在您選擇 VM 之後，請注意 VM 的 ACU。</span><span class="sxs-lookup"><span data-stu-id="90035-188">After you've chosen the VM, pay attention to the ACU for the VM.</span></span> <span data-ttu-id="90035-189">您可以根據較適合您需求的 ACU 值，選擇不同的 VM。</span><span class="sxs-lookup"><span data-stu-id="90035-189">You might choose a different VM based on the ACU value that better suits your requirements.</span></span> <span data-ttu-id="90035-190">如需詳細資訊，請參閱 [Azure 計算單位](https://docs.microsoft.com/azure/virtual-machines/windows/acu)。</span><span class="sxs-lookup"><span data-stu-id="90035-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![ACU 單位頁面的螢幕擷取畫面](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="90035-192">網路輸送量</span><span class="sxs-lookup"><span data-stu-id="90035-192">Network throughput</span></span>

<span data-ttu-id="90035-193">下圖顯示輸送量與 IOPS 之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="90035-193">The following diagram shows the relation between throughput and IOPS:</span></span>

![輸送量的螢幕擷取畫面](./media/oracle-design/throughput.png)

<span data-ttu-id="90035-195">總網路輸送量是根據下列資訊進行預估：</span><span class="sxs-lookup"><span data-stu-id="90035-195">The total network throughput is estimated based on the following information:</span></span>
- <span data-ttu-id="90035-196">SQL*Net 流量</span><span class="sxs-lookup"><span data-stu-id="90035-196">SQL*Net traffic</span></span>
- <span data-ttu-id="90035-197">MBps x 伺服器數目 (輸出串流，例如 Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="90035-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="90035-198">其他因素，例如應用程式複寫</span><span class="sxs-lookup"><span data-stu-id="90035-198">Other factors, such as application replication</span></span>

![SQL*Net 輸送量的螢幕擷取畫面](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="90035-200">根據您的網路頻寬需求，有各種閘道類型可供您選擇。</span><span class="sxs-lookup"><span data-stu-id="90035-200">Based on your network bandwidth requirements, there are various gateway types for you to choose from.</span></span> <span data-ttu-id="90035-201">這些類型包括基本、VpnGw 和 Azure ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="90035-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="90035-202">如需詳細資訊，請參閱 [VPN 閘道定價頁面](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h)。</span><span class="sxs-lookup"><span data-stu-id="90035-202">For more information, see the [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="90035-203">**建議**</span><span class="sxs-lookup"><span data-stu-id="90035-203">**Recommendations**</span></span>

- <span data-ttu-id="90035-204">與內部部署相較之下，網路延遲較高。</span><span class="sxs-lookup"><span data-stu-id="90035-204">Network latency is higher compared to an on-premises deployment.</span></span> <span data-ttu-id="90035-205">減少網路來回行程可以大幅改善效能。</span><span class="sxs-lookup"><span data-stu-id="90035-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="90035-206">若要減少來回行程，請合併相同虛擬機器上具有高交易或 “Chatty” 應用程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="90035-206">To reduce round-trips, consolidate applications that have high transactions or “chatty” apps on the same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="90035-207">磁碟類型和設定</span><span class="sxs-lookup"><span data-stu-id="90035-207">Disk types and configurations</span></span>

- <span data-ttu-id="90035-208">預設的 OS 磁碟：這些磁碟類型可提供持續性資料和快取。</span><span class="sxs-lookup"><span data-stu-id="90035-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="90035-209">它們最適合用在啟動時的 OS 存取，但其設計目的並非用於交易式或資料倉儲 (分析) 工作負載。</span><span class="sxs-lookup"><span data-stu-id="90035-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="90035-210">非受控磁碟：您可以使用這些磁碟類型來管理用來儲存虛擬硬碟 (VHD) 檔案 (對應至您的 VM 磁碟) 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="90035-210">*Unmanaged disks*: With these disk types, you manage the storage accounts that store the virtual hard disk (VHD) files that correspond to your VM disks.</span></span> <span data-ttu-id="90035-211">VHD 檔案會以分頁 Blob 的形式儲存在 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="90035-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="90035-212">受控磁碟：Azure 會管理您用於 VM 磁碟的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="90035-212">*Managed disks*: Azure manages the storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="90035-213">您可以指定需要的磁碟類型 (進階或標準) 和磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="90035-213">You specify the disk type (premium or standard) and the size of the disk that you need.</span></span> <span data-ttu-id="90035-214">Azure 會為您建立並管理該磁碟。</span><span class="sxs-lookup"><span data-stu-id="90035-214">Azure creates and manages the disk for you.</span></span>

- <span data-ttu-id="90035-215">進階儲存體磁碟：這些磁碟類型最適合生產工作負載使用。</span><span class="sxs-lookup"><span data-stu-id="90035-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="90035-216">進階儲存體支援可連結至特定大小系列 VM (例如 DS、DSv2、GS 和 F 系列 VM) 的 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="90035-216">Premium storage supports VM disks that can be attached to specific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="90035-217">進階磁碟會隨附不同的大小，而且您可以選擇範圍從 32 GB 到 4096 GB 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="90035-217">The premium disk comes with different sizes, and you can choose between disks ranging from 32 GB to 4,096 GB.</span></span> <span data-ttu-id="90035-218">每個磁碟大小都有自己的效能規格。</span><span class="sxs-lookup"><span data-stu-id="90035-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="90035-219">端視您的應用程式需求而定，您可以將一或多個磁碟連結至您的 VM。</span><span class="sxs-lookup"><span data-stu-id="90035-219">Depending on your application requirements, you can attach one or more disks to your VM.</span></span>

<span data-ttu-id="90035-220">當您從入口網站建立新的受控磁碟時，可以選擇您想要使用之磁碟類型的 [帳戶類型]。</span><span class="sxs-lookup"><span data-stu-id="90035-220">When you create a new managed disk from the portal, you can choose the **Account type** for the type of disk you want to use.</span></span> <span data-ttu-id="90035-221">請記住，並非所有可用的磁碟都會顯示在下拉式功能表中。</span><span class="sxs-lookup"><span data-stu-id="90035-221">Keep in mind that not all available disks are shown in the drop-down menu.</span></span> <span data-ttu-id="90035-222">在選擇特定的 VM 大小之後，功能表只會根據該 VM 大小顯示可用的進階儲存體 SKU。</span><span class="sxs-lookup"><span data-stu-id="90035-222">After you choose a particular VM size, the menu shows only the available premium storage SKUs that are based on that VM size.</span></span>

![受管理磁碟頁面的螢幕擷取畫面](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="90035-224">如需詳細資訊，請參閱 [VM 高效能進階儲存體與受控磁碟](https://docs.microsoft.com/azure/storage/storage-premium-storage)。</span><span class="sxs-lookup"><span data-stu-id="90035-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="90035-225">在 VM 上設定儲存體之後，您可能會想要在建立資料庫之前對磁碟進行負載測試。</span><span class="sxs-lookup"><span data-stu-id="90035-225">After you configure your storage on a VM, you might want to load test the disks before creating a database.</span></span> <span data-ttu-id="90035-226">知道延遲和輸送量方面的 I/O 速率可以協助您判斷 VM 是否支援具有延遲目標的預期輸送量。</span><span class="sxs-lookup"><span data-stu-id="90035-226">Knowing the I/O rate in terms of both latency and throughput can help you determine if the VMs support the expected throughput with latency targets.</span></span>

<span data-ttu-id="90035-227">有數種工具可以進行應用程式負載測試，例如 Oracle Orion、Sysbench 和 Fio。</span><span class="sxs-lookup"><span data-stu-id="90035-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="90035-228">在部署好 Oracle 資料庫之後，請再次執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="90035-228">Run the load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="90035-229">啟動您的一般和尖峰工作負載，其結果會顯示您環境的基準數據。</span><span class="sxs-lookup"><span data-stu-id="90035-229">Start your regular and peak workloads, and the results show you the baseline of your environment.</span></span>

<span data-ttu-id="90035-230">根據 IOPS 速率而非儲存體大小來調整儲存體大小可能更為重要。</span><span class="sxs-lookup"><span data-stu-id="90035-230">It might be more important to size the storage based on the IOPS rate rather than the storage size.</span></span> <span data-ttu-id="90035-231">例如，如果所需的 IOPS 是 5000，但您只需要 200 GB，則您可能仍會得到 P30 等級的進階磁碟，即使它隨附 200 GB 以上的儲存體。</span><span class="sxs-lookup"><span data-stu-id="90035-231">For example, if the required IOPS is 5,000, but you only need 200 GB, you might still get the P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="90035-232">IOPS 速率可以從 AWR 報表取得。</span><span class="sxs-lookup"><span data-stu-id="90035-232">The IOPS rate can be obtained from the AWR report.</span></span> <span data-ttu-id="90035-233">此速率是由重做記錄、實體讀取和寫入速率所決定。</span><span class="sxs-lookup"><span data-stu-id="90035-233">It's determined by the redo log, physical reads, and writes rate.</span></span>

![AWR 報表頁面的螢幕擷取畫面](./media/oracle-design/awr_report.png)

<span data-ttu-id="90035-235">例如：重做大小是每秒 12,200,000 個位元組，相當於 11.63 MBPs。</span><span class="sxs-lookup"><span data-stu-id="90035-235">For example, the redo size is 12,200,000 bytes per second, which is equal to 11.63 MBPs.</span></span>
<span data-ttu-id="90035-236">IOPS 是 12,200,000 / 2,358 = 5,174。</span><span class="sxs-lookup"><span data-stu-id="90035-236">The IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="90035-237">在清楚了解 I/O 需求之後，即可選擇最符合這些需求的磁碟機組合。</span><span class="sxs-lookup"><span data-stu-id="90035-237">After you have a clear picture of the I/O requirements, you can choose a combination of drives that are best suited to meet those requirements.</span></span>

<span data-ttu-id="90035-238">**建議**</span><span class="sxs-lookup"><span data-stu-id="90035-238">**Recommendations**</span></span>

- <span data-ttu-id="90035-239">針對資料的資料表空間，使用受管理儲存體或 Oracle ASM，將 I/O 工作負載分散到一些磁碟。</span><span class="sxs-lookup"><span data-stu-id="90035-239">For data tablespace, spread the I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="90035-240">隨著 I/O 區塊大小的增加，針對讀取密集和寫入密集作業，新增更多資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="90035-240">As the I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="90035-241">增加大型循序處理序的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="90035-241">Increase the block size for large sequential processes.</span></span>
- <span data-ttu-id="90035-242">使用資料壓縮來減少 I/O (適用於資料和索引)。</span><span class="sxs-lookup"><span data-stu-id="90035-242">Use data compression to reduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="90035-243">區隔不同資料磁碟上的重做記錄、系統、暫時和重做 TS。</span><span class="sxs-lookup"><span data-stu-id="90035-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="90035-244">不要將任何應用程式檔案放在預設 OS 磁碟 (/dev/sda)。</span><span class="sxs-lookup"><span data-stu-id="90035-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="90035-245">這些磁碟不適合用於快速 VM 啟動階段，因此可能不會為您的應用程式提供良好的效能。</span><span class="sxs-lookup"><span data-stu-id="90035-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="90035-246">磁碟快取設定</span><span class="sxs-lookup"><span data-stu-id="90035-246">Disk cache settings</span></span>

<span data-ttu-id="90035-247">有三個主機快取選項：</span><span class="sxs-lookup"><span data-stu-id="90035-247">There are three options for host caching:</span></span>

- <span data-ttu-id="90035-248">唯讀：快取所有要求，以供未來讀取。</span><span class="sxs-lookup"><span data-stu-id="90035-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="90035-249">所有寫入會直接保存到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="90035-249">All writes are persisted directly to Azure Blob storage.</span></span>

- <span data-ttu-id="90035-250">讀寫：這是「預先讀取」演算法。</span><span class="sxs-lookup"><span data-stu-id="90035-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="90035-251">快取讀取和寫入，以供未來讀取。</span><span class="sxs-lookup"><span data-stu-id="90035-251">The reads and writes are cached for future reads.</span></span> <span data-ttu-id="90035-252">非直接寫入式寫入會先保存到本機快取。</span><span class="sxs-lookup"><span data-stu-id="90035-252">Non-write-through writes are persisted to the local cache first.</span></span> <span data-ttu-id="90035-253">針對 SQL Server，因為它使用直接寫入式，所以寫入會保存到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="90035-253">For SQL Server, writes are persisted to Azure Storage because it uses write-through.</span></span> <span data-ttu-id="90035-254">它也會為輕量工作負載提供最低的磁碟延遲。</span><span class="sxs-lookup"><span data-stu-id="90035-254">It also provides the lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="90035-255">無 (停用)：使用此選項即可略過快取。</span><span class="sxs-lookup"><span data-stu-id="90035-255">*None* (disabled): By using this option, you can bypass the cache.</span></span> <span data-ttu-id="90035-256">所有資料都會傳輸至磁碟，並保存到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="90035-256">All the data is transferred to disk and persisted to Azure Storage.</span></span> <span data-ttu-id="90035-257">這種方法可提供您最高 I/O 速率來進行 I/O 密集式工作負載。</span><span class="sxs-lookup"><span data-stu-id="90035-257">This method gives you the highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="90035-258">您也需要考量「交易成本」。</span><span class="sxs-lookup"><span data-stu-id="90035-258">You also need to take “transaction cost” into consideration.</span></span>

<span data-ttu-id="90035-259">**建議**</span><span class="sxs-lookup"><span data-stu-id="90035-259">**Recommendations**</span></span>

<span data-ttu-id="90035-260">若要將輸送量最大化，建議您一開始先對主機快取使用 [無]。</span><span class="sxs-lookup"><span data-stu-id="90035-260">To maximize the throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="90035-261">針對進階儲存體，請記住您必須在使用 [唯讀] 或 [無] 選項掛接檔案系統時停用「屏障」。</span><span class="sxs-lookup"><span data-stu-id="90035-261">For Premium Storage, keep in mind that you must disable the "barriers" when you mount the file system with the **ReadOnly** or **None** options.</span></span> <span data-ttu-id="90035-262">將具有 UUID 的 /etc/fstab 檔案更新到磁碟。</span><span class="sxs-lookup"><span data-stu-id="90035-262">Update the /etc/fstab file with the UUID to the disks.</span></span>

<span data-ttu-id="90035-263">如需詳細資訊，請參閱[適用於 Linux VM 的進階儲存體](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms)。</span><span class="sxs-lookup"><span data-stu-id="90035-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![受管理磁碟頁面的螢幕擷取畫面](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="90035-265">針對 OS 磁碟，使用預設的 [讀取/寫入] 快取。</span><span class="sxs-lookup"><span data-stu-id="90035-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="90035-266">針對 SYSTEM、TEMP 和 UNDO，對快取功能使用 [無]。</span><span class="sxs-lookup"><span data-stu-id="90035-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="90035-267">針對 DATA，對快取功能使用 [無]。</span><span class="sxs-lookup"><span data-stu-id="90035-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="90035-268">但是，如果您的資料庫是唯讀或讀取密集，請使用 [唯讀] 快取。</span><span class="sxs-lookup"><span data-stu-id="90035-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="90035-269">除非您卸載 OS 層級的磁碟機，然後在進行變更後重新予以掛接，否則在儲存資料磁碟設定之後，就無法變更主機快取設定。</span><span class="sxs-lookup"><span data-stu-id="90035-269">After your data disk setting is saved, you can't change the host cache setting unless you unmount the drive at the OS level and then remount it after you've made the change.</span></span>


## <a name="security"></a><span data-ttu-id="90035-270">安全性</span><span class="sxs-lookup"><span data-stu-id="90035-270">Security</span></span>

<span data-ttu-id="90035-271">在安裝並設定 Azure 環境之後，下一個步驟是保護您的網路。</span><span class="sxs-lookup"><span data-stu-id="90035-271">After you have set up and configured your Azure environment, the next step is to secure your network.</span></span> <span data-ttu-id="90035-272">以下是一些建議：</span><span class="sxs-lookup"><span data-stu-id="90035-272">Here are some recommendations:</span></span>

- <span data-ttu-id="90035-273">NSG 原則：可以透過子網路或 NIC 來定義 NSG。</span><span class="sxs-lookup"><span data-stu-id="90035-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="90035-274">它更容易控制應用程式防火牆這類事項之安全性和強制路由的子網路層級存取。</span><span class="sxs-lookup"><span data-stu-id="90035-274">It's simpler to control access at the subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="90035-275">Jumpbox：基於更安全的存取，系統管理員不應該直接連線至應用程式服務或資料庫。</span><span class="sxs-lookup"><span data-stu-id="90035-275">*Jumpbox*: For more secure access, administrators should not directly connect to the application service or database.</span></span> <span data-ttu-id="90035-276">Jumpbox 作為系統管理員機器與 Azure 資源之間的媒體。</span><span class="sxs-lookup"><span data-stu-id="90035-276">A jumpbox is used as a media between the administrator machine and Azure resources.</span></span>
<span data-ttu-id="90035-277">![Jumpbox 拓撲頁面的螢幕擷取畫面](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="90035-277">![Screenshot of the Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="90035-278">系統管理員機器只應該對 Jumpbox 提供 IP 受限的存取權。</span><span class="sxs-lookup"><span data-stu-id="90035-278">The administrator machine should offer IP-restricted access to the jumpbox only.</span></span> <span data-ttu-id="90035-279">Jumpbox 應該要能夠存取應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="90035-279">The jumpbox should have access to the application and database.</span></span>

- <span data-ttu-id="90035-280">私人網路 (子網路)：我們建議您將應用程式服務和資料庫放在不同的子網路上，讓 NSG 原則可以設定更好的控制。</span><span class="sxs-lookup"><span data-stu-id="90035-280">*Private network* (subnets): We recommend that you have the application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="90035-281">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="90035-281">Additional reading</span></span>

- [<span data-ttu-id="90035-282">設定 Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="90035-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="90035-283">設定 Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="90035-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="90035-284">設定 Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="90035-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="90035-285">Oracle 備份和復原</span><span class="sxs-lookup"><span data-stu-id="90035-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="90035-286">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90035-286">Next steps</span></span>

- [<span data-ttu-id="90035-287">教學課程︰建立高可用性 VM</span><span class="sxs-lookup"><span data-stu-id="90035-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="90035-288">瀏覽 VM 部署 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="90035-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
