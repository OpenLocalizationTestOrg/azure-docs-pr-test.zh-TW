---
title: "服務網狀架構的效能監視的 aaaAzure |Microsoft 文件"
description: "了解用於監視及診斷 Azure Service Fabric 叢集的效能計數器。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="6bab5-103">效能度量</span><span class="sxs-lookup"><span data-stu-id="6bab5-103">Performance metrics</span></span>

<span data-ttu-id="6bab5-104">度量應該是您的叢集收集的 toounderstand hello 效能，以及它所執行的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bab5-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="6bab5-105">Service Fabric 叢集，我們建議收集下列效能計數器的 hello。</span><span class="sxs-lookup"><span data-stu-id="6bab5-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="6bab5-106">節點</span><span class="sxs-lookup"><span data-stu-id="6bab5-106">Nodes</span></span>

<span data-ttu-id="6bab5-107">針對叢集中的 hello 機器，請考慮收集下列效能計數器 hello 每部機器上的負載，並進行適當調整決策的叢集，了解 toobetter hello。</span><span class="sxs-lookup"><span data-stu-id="6bab5-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="6bab5-108">計數器類別</span><span class="sxs-lookup"><span data-stu-id="6bab5-108">Counter Category</span></span> | <span data-ttu-id="6bab5-109">計數器名稱</span><span class="sxs-lookup"><span data-stu-id="6bab5-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="6bab5-110">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6bab5-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6bab5-111">Avg.磁碟讀取佇列長度</span><span class="sxs-lookup"><span data-stu-id="6bab5-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="6bab5-112">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6bab5-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6bab5-113">Avg.磁碟寫入佇列長度</span><span class="sxs-lookup"><span data-stu-id="6bab5-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="6bab5-114">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6bab5-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6bab5-115">Avg.Disk sec/Read</span><span class="sxs-lookup"><span data-stu-id="6bab5-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="6bab5-116">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6bab5-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6bab5-117">Avg.Disk sec/Write</span><span class="sxs-lookup"><span data-stu-id="6bab5-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="6bab5-118">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6bab5-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6bab5-119">Disk Reads/sec </span><span class="sxs-lookup"><span data-stu-id="6bab5-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="6bab5-120">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6bab5-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6bab5-121">Disk Read Bytes/sec </span><span class="sxs-lookup"><span data-stu-id="6bab5-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="6bab5-122">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6bab5-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6bab5-123">Disk Writes/sec</span><span class="sxs-lookup"><span data-stu-id="6bab5-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="6bab5-124">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6bab5-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6bab5-125">Disk Write Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="6bab5-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="6bab5-126">記憶體</span><span class="sxs-lookup"><span data-stu-id="6bab5-126">Memory</span></span> | <span data-ttu-id="6bab5-127">可用的 MB</span><span class="sxs-lookup"><span data-stu-id="6bab5-127">Available MBytes</span></span> |
| <span data-ttu-id="6bab5-128">PagingFile</span><span class="sxs-lookup"><span data-stu-id="6bab5-128">PagingFile</span></span> | <span data-ttu-id="6bab5-129">% 使用量</span><span class="sxs-lookup"><span data-stu-id="6bab5-129">% Usage</span></span> |
| <span data-ttu-id="6bab5-130">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="6bab5-130">Process(Total)</span></span> | <span data-ttu-id="6bab5-131">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="6bab5-131">% Processor Time</span></span> |
| <span data-ttu-id="6bab5-132">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="6bab5-132">Process (per service)</span></span> | <span data-ttu-id="6bab5-133">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="6bab5-133">% Processor Time</span></span> |
| <span data-ttu-id="6bab5-134">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="6bab5-134">Process (per service)</span></span> | <span data-ttu-id="6bab5-135">識別碼處理序</span><span class="sxs-lookup"><span data-stu-id="6bab5-135">ID Process</span></span> |
| <span data-ttu-id="6bab5-136">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="6bab5-136">Process (per service)</span></span> | <span data-ttu-id="6bab5-137">私用位元組</span><span class="sxs-lookup"><span data-stu-id="6bab5-137">Private Bytes</span></span> |
| <span data-ttu-id="6bab5-138">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="6bab5-138">Process (per service)</span></span> | <span data-ttu-id="6bab5-139">執行緒計數</span><span class="sxs-lookup"><span data-stu-id="6bab5-139">Thread Count</span></span> |
| <span data-ttu-id="6bab5-140">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="6bab5-140">Process (per service)</span></span> | <span data-ttu-id="6bab5-141">虛擬位元組</span><span class="sxs-lookup"><span data-stu-id="6bab5-141">Virtual Bytes</span></span> |
| <span data-ttu-id="6bab5-142">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="6bab5-142">Process (per service)</span></span> | <span data-ttu-id="6bab5-143">工作集</span><span class="sxs-lookup"><span data-stu-id="6bab5-143">Working Set</span></span> |
| <span data-ttu-id="6bab5-144">Process (per service)</span><span class="sxs-lookup"><span data-stu-id="6bab5-144">Process (per service)</span></span> | <span data-ttu-id="6bab5-145">工作集 - 私用</span><span class="sxs-lookup"><span data-stu-id="6bab5-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="6bab5-146">.NET 應用程式與服務</span><span class="sxs-lookup"><span data-stu-id="6bab5-146">.NET applications and services</span></span>

<span data-ttu-id="6bab5-147">收集下列計數器，如果您要部署.NET services tooyour 叢集 hello。</span><span class="sxs-lookup"><span data-stu-id="6bab5-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="6bab5-148">計數器類別</span><span class="sxs-lookup"><span data-stu-id="6bab5-148">Counter Category</span></span> | <span data-ttu-id="6bab5-149">計數器名稱</span><span class="sxs-lookup"><span data-stu-id="6bab5-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="6bab5-150">.NET CLR 記憶體 (每一服務)</span><span class="sxs-lookup"><span data-stu-id="6bab5-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6bab5-151">處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="6bab5-151">Process ID</span></span> |
| <span data-ttu-id="6bab5-152">.NET CLR 記憶體 (每一服務)</span><span class="sxs-lookup"><span data-stu-id="6bab5-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6bab5-153">認可的位元組總數</span><span class="sxs-lookup"><span data-stu-id="6bab5-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="6bab5-154">.NET CLR 記憶體 (每一服務)</span><span class="sxs-lookup"><span data-stu-id="6bab5-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6bab5-155">保留的位元組總數</span><span class="sxs-lookup"><span data-stu-id="6bab5-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="6bab5-156">.NET CLR 記憶體 (每一服務)</span><span class="sxs-lookup"><span data-stu-id="6bab5-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6bab5-157">所有堆積中的位元組數</span><span class="sxs-lookup"><span data-stu-id="6bab5-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="6bab5-158">.NET CLR 記憶體 (每一服務)</span><span class="sxs-lookup"><span data-stu-id="6bab5-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6bab5-159">層代 0 集合數</span><span class="sxs-lookup"><span data-stu-id="6bab5-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="6bab5-160">.NET CLR 記憶體 (每一服務)</span><span class="sxs-lookup"><span data-stu-id="6bab5-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6bab5-161">層代 1 集合數</span><span class="sxs-lookup"><span data-stu-id="6bab5-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="6bab5-162">.NET CLR 記憶體 (每一服務)</span><span class="sxs-lookup"><span data-stu-id="6bab5-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6bab5-163">層代 2 集合數</span><span class="sxs-lookup"><span data-stu-id="6bab5-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="6bab5-164">.NET CLR 記憶體 (每一服務)</span><span class="sxs-lookup"><span data-stu-id="6bab5-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6bab5-165">記憶體回收中的時間 %</span><span class="sxs-lookup"><span data-stu-id="6bab5-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="6bab5-166">Service Fabric 的自訂效能計數器</span><span class="sxs-lookup"><span data-stu-id="6bab5-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="6bab5-167">Service Fabric 可產生大量的自訂效能計數器。</span><span class="sxs-lookup"><span data-stu-id="6bab5-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="6bab5-168">如果您擁有 hello 安裝 SDK 時，您可以應用程式效能監視中 Windows 電腦上看到 hello 完整清單 (開始 > 效能監視器)。</span><span class="sxs-lookup"><span data-stu-id="6bab5-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="6bab5-169">Hello 應用程式中，您要部署 tooyour 叢集，如果您使用 Reliable Actors，加入從 countes`Service Fabric Actor`和`Service Fabric Actor Method`類別 (請參閱[服務網狀架構可靠執行者診斷](service-fabric-reliable-actors-diagnostics.md))。</span><span class="sxs-lookup"><span data-stu-id="6bab5-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="6bab5-170">如果您使用 Reliable Services，我們同樣提供 `Service Fabric Service` 和 `Service Fabric Service Method` 計數器類別，您應該從這些類別收集計數器。</span><span class="sxs-lookup"><span data-stu-id="6bab5-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="6bab5-171">如果您使用可靠的集合，我們建議將加入 hello`Avg. Transaction ms/Commit`從 hello `Service Fabric Transactional Replicator` toocollect hello 平均認可延遲，每個交易標準。</span><span class="sxs-lookup"><span data-stu-id="6bab5-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6bab5-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bab5-172">Next steps</span></span>

* <span data-ttu-id="6bab5-173">深入了解[hello 平台層級的事件產生](service-fabric-diagnostics-event-generation-infra.md)Service Fabric 中</span><span class="sxs-lookup"><span data-stu-id="6bab5-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="6bab5-174">透過 [Azure 診斷](service-fabric-diagnostics-event-aggregation-wad.md)收集效能計量</span><span class="sxs-lookup"><span data-stu-id="6bab5-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
