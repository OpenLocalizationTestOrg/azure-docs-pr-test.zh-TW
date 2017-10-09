---
title: "aaaPlan 容量與縮放比例的 VMware 複寫 tooAzure 與 Azure Site Recovery |Microsoft 文件"
description: "當複寫與 Azure Site Recovery 的 VMware Vm tooAzure 時使用此發行項 tooplan 容量和小數位數"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 551533ab7090d85c216be242ea92781deb8287ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-vmware-tooazure-replication"></a><span data-ttu-id="14703-103">步驟 3： 規劃容量和 VMware tooAzure 複寫調整</span><span class="sxs-lookup"><span data-stu-id="14703-103">Step 3: Plan capacity and scaling for VMware tooAzure replication</span></span>

<span data-ttu-id="14703-104">使用容量規劃和調整，當複寫在內部部署 VMware Vm 和實體伺服器 tooAzure 與此發行項 toofigure [Azure Site Recovery](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="14703-104">Use this article toofigure out planning for capacity and scaling, when replicating on-premises VMware VMs and physical servers tooAzure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="14703-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="14703-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="14703-106">如何開始容量規劃？</span><span class="sxs-lookup"><span data-stu-id="14703-106">How do I start capacity planning?</span></span>

<span data-ttu-id="14703-107">您收集資訊的複寫環境，並規劃容量使用這項資訊，以及在本文中反白顯示 hello 考量。</span><span class="sxs-lookup"><span data-stu-id="14703-107">You gather information about your replication environment, and then plan capacity using this information, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="14703-108">收集資訊</span><span class="sxs-lookup"><span data-stu-id="14703-108">Gather information</span></span>

1. <span data-ttu-id="14703-109">下載 hello[部署規劃工具](https://aka.ms/asr-deployment-planner)VMware 複寫。</span><span class="sxs-lookup"><span data-stu-id="14703-109">Download hello [Deployment Planner tool](https://aka.ms/asr-deployment-planner) for VMware replication.</span></span>
2. <span data-ttu-id="14703-110">[閱讀此文章](site-recovery-deployment-planner.md)toounderstand toorun hello 工具的方式。</span><span class="sxs-lookup"><span data-stu-id="14703-110">[Read this article](site-recovery-deployment-planner.md) toounderstand how toorun hello tool.</span></span>
3. <span data-ttu-id="14703-111">使用 hello 工具收集相容和不相容的 Vm，每個 VM，磁碟的相關資訊和資料變換每個磁碟的。</span><span class="sxs-lookup"><span data-stu-id="14703-111">Using hello tool you gather information about compatible and incompatible VMs, disks per VM, and data churn per disk.</span></span> <span data-ttu-id="14703-112">網路頻寬需求和 hello 順利進行複寫和測試容錯移轉所需的 Azure 基礎結構，同時也包含 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="14703-112">hello tool also covers network bandwidth requirements, and hello Azure infrastructure needed for successful replication and test failover.</span></span>

## <a name="replication-considerations"></a><span data-ttu-id="14703-113">複寫考量</span><span class="sxs-lookup"><span data-stu-id="14703-113">Replication considerations</span></span>

<span data-ttu-id="14703-114">開始部署之前，請注意下列考量：</span><span class="sxs-lookup"><span data-stu-id="14703-114">Note these considerations before you start deployment:</span></span>

<span data-ttu-id="14703-115">**元件**</span><span class="sxs-lookup"><span data-stu-id="14703-115">**Component**</span></span> | <span data-ttu-id="14703-116">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="14703-116">**Details**</span></span> |
--- | --- | ---
<span data-ttu-id="14703-117">**複寫**</span><span class="sxs-lookup"><span data-stu-id="14703-117">**Replication**</span></span> | <span data-ttu-id="14703-118">**每日最大的變更率：**受保護的電腦只能使用一個處理序伺服器，而且單一處理序伺服器可以處理每日的變更率向上 too2 TB。</span><span class="sxs-lookup"><span data-stu-id="14703-118">**Maximum daily change rate:** A protected machine can only use one process server, and a single process server can handle a daily change rate up too2 TB.</span></span> <span data-ttu-id="14703-119">因此 2 TB 為 hello 最大的每日資料變更率支援的受保護的機器。</span><span class="sxs-lookup"><span data-stu-id="14703-119">Thus 2 TB is hello maximum daily data change rate that’s supported for a protected machine.</span></span><br/><br/> <span data-ttu-id="14703-120">**最大輸送量：**複寫的機器可以隸屬 tooone 在 Azure 中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="14703-120">**Maximum throughput:** A replicated machine can belong tooone storage account in Azure.</span></span> <span data-ttu-id="14703-121">標準儲存體帳戶可以處理最多 20,000 每秒的要求，並建議來源機器 too20 000 維持 hello 輸入/輸出作業每秒 (IOPS) 數目。</span><span class="sxs-lookup"><span data-stu-id="14703-121">A standard storage account can handle a maximum of 20,000 requests per second, and we recommend that you keep hello number of input/output operations per second (IOPS) across a source machine too20,000.</span></span> <span data-ttu-id="14703-122">例如，如果您有使用 5 磁碟時，來源電腦，而且每個磁碟會產生 hello 來源電腦上的 120 IOPS （8 千個大小），表示它會在每個磁碟的 IOPS 限制為 500 hello Azure 內。</span><span class="sxs-lookup"><span data-stu-id="14703-122">For example, if you have a source machine with 5 disks, and each disk generates 120 IOPS (8K size) on hello source machine, then it will be within hello Azure per disk IOPS limit of 500.</span></span> <span data-ttu-id="14703-123">（儲存體帳戶所需的 hello 數目是等於 toohello 總來源機器 IOPS，除以 20000）。</span><span class="sxs-lookup"><span data-stu-id="14703-123">(hello number of storage accounts required is equal toohello total source machine IOPS, divided by 20,000.)</span></span>

## <a name="configuration-server-capacity"></a><span data-ttu-id="14703-124">組態伺服器容量</span><span class="sxs-lookup"><span data-stu-id="14703-124">Configuration server capacity</span></span>

<span data-ttu-id="14703-125">hello 組態伺服器應該可以 toohandle hello 每日變更速率容量跨所有受保護的機器上執行的工作負載而且需要足夠的頻寬 toocontinuously 複寫資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="14703-125">hello configuration server should be able toohandle hello daily change rate capacity across all workloads running on protected machines, and needs sufficient bandwidth toocontinuously replicate data tooAzure Storage.</span></span>

<span data-ttu-id="14703-126">最佳做法，找出 hello 組態伺服器 hello 上相同的網路和區域網路區段，做為 hello 想 tooprotect 機器。</span><span class="sxs-lookup"><span data-stu-id="14703-126">As a best practice, locate hello configuration server on hello same network and LAN segment as hello machines you want tooprotect.</span></span> <span data-ttu-id="14703-127">它可以位於不同的網路，但您想 tooprotect 應該有層級 3 網路可見性 tooit 機器上。</span><span class="sxs-lookup"><span data-stu-id="14703-127">It can be located on a different network, but machines you want tooprotect should have layer 3 network visibility tooit.</span></span>

## <a name="sizing-recommendations"></a><span data-ttu-id="14703-128">大小調整建議</span><span class="sxs-lookup"><span data-stu-id="14703-128">Sizing recommendations</span></span>

<span data-ttu-id="14703-129">hello 表格摘要說明根據 CPU 調整建議。</span><span class="sxs-lookup"><span data-stu-id="14703-129">hello table summarizes sizing recommendations based on CPU.</span></span>

<span data-ttu-id="14703-130">**CPU**</span><span class="sxs-lookup"><span data-stu-id="14703-130">**CPU**</span></span> | <span data-ttu-id="14703-131">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="14703-131">**Memory**</span></span> | <span data-ttu-id="14703-132">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="14703-132">**Cache disk size**</span></span> | <span data-ttu-id="14703-133">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="14703-133">**Data change rate**</span></span> | <span data-ttu-id="14703-134">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="14703-134">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="14703-135">8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="14703-135">8 vCPUs (2 sockets * 4 cores @ 2.5 gigahertz [GHz])</span></span> | <span data-ttu-id="14703-136">16 GB</span><span class="sxs-lookup"><span data-stu-id="14703-136">16 GB</span></span> | <span data-ttu-id="14703-137">300 GB</span><span class="sxs-lookup"><span data-stu-id="14703-137">300 GB</span></span> | <span data-ttu-id="14703-138">500 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="14703-138">500 GB or less</span></span> | <span data-ttu-id="14703-139">複寫少於 100 部機器。</span><span class="sxs-lookup"><span data-stu-id="14703-139">Replicate less than 100 machines.</span></span>
<span data-ttu-id="14703-140">12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="14703-140">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="14703-141">18 GB</span><span class="sxs-lookup"><span data-stu-id="14703-141">18 GB</span></span> | <span data-ttu-id="14703-142">600 GB</span><span class="sxs-lookup"><span data-stu-id="14703-142">600 GB</span></span> | <span data-ttu-id="14703-143">500 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="14703-143">500 GB too1 TB</span></span> | <span data-ttu-id="14703-144">複寫 100-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="14703-144">Replicate between 100-150 machines.</span></span>
<span data-ttu-id="14703-145">16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="14703-145">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="14703-146">32 GB</span><span class="sxs-lookup"><span data-stu-id="14703-146">32 GB</span></span> | <span data-ttu-id="14703-147">1 TB</span><span class="sxs-lookup"><span data-stu-id="14703-147">1 TB</span></span> | <span data-ttu-id="14703-148">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="14703-148">1 TB too2 TB</span></span> | <span data-ttu-id="14703-149">複寫 150-200 部機器。</span><span class="sxs-lookup"><span data-stu-id="14703-149">Replicate between 150-200 machines.</span></span>
<span data-ttu-id="14703-150">部署另一個處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="14703-150">Deploy another process server</span></span> | | | <span data-ttu-id="14703-151">> 2 TB</span><span class="sxs-lookup"><span data-stu-id="14703-151">> 2 TB</span></span> | <span data-ttu-id="14703-152">如果您要複寫 200 個以上的機器，或如果 hello 每日資料變更速率超過 2TB，請部署額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-152">Deploy additional process servers if you're replicating more than 200 machines, or if hello daily data change rate exceeds 2 TB.</span></span>

<span data-ttu-id="14703-153">其中：</span><span class="sxs-lookup"><span data-stu-id="14703-153">Where:</span></span>

* <span data-ttu-id="14703-154">每個來源機器已設定各 100 GB 的 3 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="14703-154">Each source machine is configured with 3 disks of 100 GB each.</span></span>
* <span data-ttu-id="14703-155">我們使用具有 RAID 10 的 8 個 10 K RPM 的 SAS 磁碟機的效能評定儲存體以進行快取磁碟度量。</span><span class="sxs-lookup"><span data-stu-id="14703-155">We used benchmarking storage of 8 SAS drives of 10 K RPM, with RAID 10, for cache disk measurements.</span></span>

## <a name="process-server-capacity"></a><span data-ttu-id="14703-156">處理伺服器容量</span><span class="sxs-lookup"><span data-stu-id="14703-156">Process server capacity</span></span>


<span data-ttu-id="14703-157">hello 處理序伺服器接收複寫資料從受保護的機器，並最佳化與快取、 壓縮和加密。</span><span class="sxs-lookup"><span data-stu-id="14703-157">hello process server receives replication data from protected machines, and optimizes it with caching, compression, and encryption.</span></span> <span data-ttu-id="14703-158">然後它會傳送 hello 資料 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="14703-158">Then it sends hello data tooAzure.</span></span>

- <span data-ttu-id="14703-159">hello 處理序伺服器的電腦應該有足夠的資源 tooperform 這些工作。</span><span class="sxs-lookup"><span data-stu-id="14703-159">hello process server machine should have sufficient resources tooperform these tasks.</span></span>
- <span data-ttu-id="14703-160">hello 組態伺服器上預設會安裝第一個處理序伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="14703-160">hello first process server is installed by default on hello configuration server.</span></span> <span data-ttu-id="14703-161">您可以部署額外的處理序伺服器 tooscale 您的環境。</span><span class="sxs-lookup"><span data-stu-id="14703-161">You can deploy additional process servers tooscale your environment.</span></span>
- <span data-ttu-id="14703-162">hello 處理序伺服器會使用以磁碟為基礎的快取。</span><span class="sxs-lookup"><span data-stu-id="14703-162">hello process server uses a disk-based cache.</span></span> <span data-ttu-id="14703-163">使用不同的快取磁碟 600 GB 或更多的 toohandle 資料變更，儲存在網路瓶頸後或中斷 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="14703-163">Use a separate cache disk of 600 GB or more toohandle data changes stored in hello event of a network bottleneck or outage.</span></span>
- <span data-ttu-id="14703-164">如果您需要 tooprotect 200 個以上的機器，或每日變更率 hello 大於 2 TB，您可以加入處理序伺服器 toohandle hello 複寫載入。</span><span class="sxs-lookup"><span data-stu-id="14703-164">If you need tooprotect more than 200 machines, or hello daily change rate is greater than 2 TB, you can add process servers toohandle hello replication load.</span></span> <span data-ttu-id="14703-165">tooscale 外的，您可以：</span><span class="sxs-lookup"><span data-stu-id="14703-165">tooscale out, you can:</span></span>
    - <span data-ttu-id="14703-166">增加 hello 組態伺服器的數目。</span><span class="sxs-lookup"><span data-stu-id="14703-166">Increase hello number of configuration servers.</span></span> <span data-ttu-id="14703-167">例如，您可以保護 too400 機器組態，兩台伺服器上。</span><span class="sxs-lookup"><span data-stu-id="14703-167">For example, you can protect up too400 machines with two configuration servers.</span></span>
    - <span data-ttu-id="14703-168">新增更多的處理序伺服器，並使用這些 toohandle 流量，而不是 （或其他） hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-168">Add more process servers, and use these toohandle traffic instead of (or in addition to) hello configuration server.</span></span>


### <a name="example-process-server-scaling"></a><span data-ttu-id="14703-169">範例處理伺服器調整</span><span class="sxs-lookup"><span data-stu-id="14703-169">Example process server scaling</span></span>

<span data-ttu-id="14703-170">hello 下表描述的案例：</span><span class="sxs-lookup"><span data-stu-id="14703-170">hello following table describes a scenario in which:</span></span>

* <span data-ttu-id="14703-171">您不打算 toouse hello 組態伺服器的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-171">You're not planning toouse hello configuration server as a process server.</span></span>
* <span data-ttu-id="14703-172">您已設定額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-172">You've set up an additional process server.</span></span>
* <span data-ttu-id="14703-173">您已設定受保護的虛擬機器 toouse hello 額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-173">You've configured protected virtual machines toouse hello additional process server.</span></span>
* <span data-ttu-id="14703-174">每個受保護的來源機器已設定各 100 GB 的 3 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="14703-174">Each protected source machine is configured with three disks of 100 GB each.</span></span>

<span data-ttu-id="14703-175">**組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="14703-175">**Configuration server**</span></span> | <span data-ttu-id="14703-176">**額外處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="14703-176">**Additional process server**</span></span> | <span data-ttu-id="14703-177">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="14703-177">**Cache disk size**</span></span> | <span data-ttu-id="14703-178">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="14703-178">**Data change rate**</span></span> | <span data-ttu-id="14703-179">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="14703-179">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="14703-180">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="14703-180">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="14703-181">4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5 GHz)，8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="14703-181">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8 GB memory</span></span> | <span data-ttu-id="14703-182">300 GB</span><span class="sxs-lookup"><span data-stu-id="14703-182">300 GB</span></span> | <span data-ttu-id="14703-183">250 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="14703-183">250 GB or less</span></span> | <span data-ttu-id="14703-184">複寫 85 部或更少的機器。</span><span class="sxs-lookup"><span data-stu-id="14703-184">Replicate 85 or fewer machines.</span></span>
<span data-ttu-id="14703-185">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="14703-185">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="14703-186">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，12 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="14703-186">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12 GB memory</span></span> | <span data-ttu-id="14703-187">600 GB</span><span class="sxs-lookup"><span data-stu-id="14703-187">600 GB</span></span> | <span data-ttu-id="14703-188">250 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="14703-188">250 GB too1 TB</span></span> | <span data-ttu-id="14703-189">複寫 85-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="14703-189">Replicate between 85-150 machines.</span></span>
<span data-ttu-id="14703-190">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，18 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="14703-190">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz), 18 GB memory</span></span> | <span data-ttu-id="14703-191">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，24 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="14703-191">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24 GB memory</span></span> | <span data-ttu-id="14703-192">1 TB</span><span class="sxs-lookup"><span data-stu-id="14703-192">1 TB</span></span> | <span data-ttu-id="14703-193">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="14703-193">1 TB too2 TB</span></span> | <span data-ttu-id="14703-194">複寫 150-225 部機器。</span><span class="sxs-lookup"><span data-stu-id="14703-194">Replicate between 150-225 machines.</span></span>

<span data-ttu-id="14703-195">您可以在其中調整您的伺服器 hello 方式取決於您的喜好設定的向上延展或向外延展模型。</span><span class="sxs-lookup"><span data-stu-id="14703-195">hello way in which you scale your servers depends on your preference for a scale-up or scale-out model.</span></span>  <span data-ttu-id="14703-196">您部署幾個高階組態和處理序伺服器以相應增加，或使用較少的資源部署更多伺服器以相應放大。</span><span class="sxs-lookup"><span data-stu-id="14703-196">You scale up by deploying a few high-end configuration and process servers, or scale out by deploying more servers with fewer resources.</span></span> <span data-ttu-id="14703-197">比方說，如果您需要 tooprotect 220 機器，您可以執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="14703-197">For example, if you need tooprotect 220 machines, you could do either of hello following:</span></span>

* <span data-ttu-id="14703-198">設定 hello 12 vCPU、 18 GB 的記憶體，與 12 vCPU、 24 GB 的記憶體的額外的處理序伺服器的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-198">Set up hello configuration server with 12 vCPU, 18 GB of memory, and an additional process server with 12 vCPU, 24 GB of memory.</span></span> <span data-ttu-id="14703-199">設定受保護的機器 toouse hello 只用於其他處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-199">Configure protected machines toouse hello additional process server only.</span></span>
* <span data-ttu-id="14703-200">設定兩個組態伺服器 （2 x 8 vCPU、 16 GB 的 RAM） 和兩個額外的處理序伺服器 （1 x 8 vCPU 和 4 vCPU x 1 toohandle 135 + 85 [220] 機器）。</span><span class="sxs-lookup"><span data-stu-id="14703-200">Set up two configuration servers (2 x 8 vCPU, 16 GB RAM) and two additional process servers (1 x 8 vCPU and 4 vCPU x 1 toohandle 135 + 85 [220] machines).</span></span> <span data-ttu-id="14703-201">設定受保護的機器 toouse hello 只用於其他處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-201">Configure protected machines toouse hello additional process servers only.</span></span>

## <a name="deploy-additional-process-servers"></a><span data-ttu-id="14703-202">部署額外處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="14703-202">Deploy additional process servers</span></span>

<span data-ttu-id="14703-203">請遵循這些指示 tooset，額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-203">Follow these instructions tooset up an additional process server.</span></span> <span data-ttu-id="14703-204">設定好 hello 伺服器之後，您將移轉來源機器 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="14703-204">After setting up hello server, you migrate source machines toouse it.</span></span>

1. <span data-ttu-id="14703-205">在**站台復原伺服器**，按一下 hello 組態伺服器 > **+ 處理序伺服器**。</span><span class="sxs-lookup"><span data-stu-id="14703-205">In **Site Recovery servers**, click hello configuration server > **+Process Server**.</span></span>
2. <span data-ttu-id="14703-206">在 [伺服器類型] 中，按一下 [處理伺服器 (內部部署)]。</span><span class="sxs-lookup"><span data-stu-id="14703-206">In **Server type**, click **Process server (on-premises)**.</span></span>

    ![處理序伺服器](./media/vmware-walkthrough-capacity/migrate-ps2.png)
3. <span data-ttu-id="14703-208">下載 hello Site Recovery 整合安裝程式檔案。</span><span class="sxs-lookup"><span data-stu-id="14703-208">Download hello Site Recovery Unified Setup file.</span></span>
4. <span data-ttu-id="14703-209">執行安裝程式 tooinstall hello 處理序伺服器和 hello 保存庫中註冊它。</span><span class="sxs-lookup"><span data-stu-id="14703-209">Run setup tooinstall hello process server, and register it in hello vault.</span></span>
5. <span data-ttu-id="14703-210">在**開始之前**，選取**新增額外的處理序伺服器 tooscale 出部署**。</span><span class="sxs-lookup"><span data-stu-id="14703-210">In **Before you begin**, select **Add additional process servers tooscale out deployment**.</span></span>
6. <span data-ttu-id="14703-211">在**組態伺服器詳細資料**、 指定 hello 的 hello 組態伺服器上的 IP 位址和 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="14703-211">In **Configuration Server Details**, specify hello IP address of hello configuration server, and hello passphrase.</span></span> <span data-ttu-id="14703-212">如果您沒有 hello 複雜密碼，取得執行**[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** hello 組態伺服器上。</span><span class="sxs-lookup"><span data-stu-id="14703-212">If you don't have hello passphrase, get it by running **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n** on hello configuration server.</span></span>

    ![組態伺服器](./media/vmware-walkthrough-capacity/add-ps2.png)
7. <span data-ttu-id="14703-214">完成安裝程式在 hello hello 其餘部分相同的方式就像當您設定 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-214">Complete hello rest of setup in hello same way you did when you set up hello configuration server.</span></span>

### <a name="migrate-machines-toouse-hello-process-server"></a><span data-ttu-id="14703-215">移轉機器 toouse hello 處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="14703-215">Migrate machines toouse hello process server</span></span>

1. <span data-ttu-id="14703-216">在**設定** > **站台復原伺服器**，按一下 hello 組態伺服器 >**處理伺服器**。</span><span class="sxs-lookup"><span data-stu-id="14703-216">In **Settings** > **Site Recovery servers**, click hello configuration server > **Process servers**.</span></span>
2. <span data-ttu-id="14703-217">目前使用中的，以滑鼠右鍵按一下 hello 處理序伺服器 >**交換器**。</span><span class="sxs-lookup"><span data-stu-id="14703-217">Right-click hello process server currently in use > **Switch**.</span></span>

    ![切換處理伺服器](./media/vmware-walkthrough-capacity/migrate-ps3.png)
3. <span data-ttu-id="14703-219">在**選取目標處理序伺服器**，請選取該 hello 伺服器將處理 toouse，再選取 hello Vm hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-219">In **Select target process server**, select hello process server you want toouse, and select hello VMs that hello server will handle.</span></span>
4. <span data-ttu-id="14703-220">按一下 hello 資訊圖示。</span><span class="sxs-lookup"><span data-stu-id="14703-220">Click hello information icon.</span></span> <span data-ttu-id="14703-221">toohelp 您進行載入決策，hello 平均 tooreplicate 會顯示每個選取的 VM toohello 新處理序伺服器所需的空間。</span><span class="sxs-lookup"><span data-stu-id="14703-221">toohelp you make load decisions, hello average space that's needed tooreplicate each selected VM toohello new process server is displayed.</span></span>
5. <span data-ttu-id="14703-222">按一下 hello 核取記號 toostart 複寫 toohello 新處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-222">Click hello check mark toostart replication toohello new process server.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="14703-223">控制網路頻寬</span><span class="sxs-lookup"><span data-stu-id="14703-223">Control network bandwidth</span></span>

<span data-ttu-id="14703-224">當您執行[hello 部署規劃工具](site-recovery-deployment-planner.md)，您必須複寫 （hello 初始複寫，然後差異） toocalculate hello 頻寬，您可以控制 hello 數量所使用頻寬的複寫使用幾個選項：</span><span class="sxs-lookup"><span data-stu-id="14703-224">After you run [hello Deployment Planner tool](site-recovery-deployment-planner.md) toocalculate hello bandwidth you need for replication (hello initial replication and then delta), you can control hello amount of bandwidth used for replication using a couple of options:</span></span>

* <span data-ttu-id="14703-225">**節流的頻寬**： 複寫 tooAzure VMware 流量通過特定處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-225">**Throttle bandwidth**: VMware traffic that replicates tooAzure goes through a specific process server.</span></span> <span data-ttu-id="14703-226">您可以將做為處理序伺服器 hello 機器上的頻寬節流處理。</span><span class="sxs-lookup"><span data-stu-id="14703-226">You can throttle bandwidth on hello machines running as process servers.</span></span>
* <span data-ttu-id="14703-227">**影響頻寬**： 您可能會影響用來複寫使用數個登錄機碼的 hello 頻寬：</span><span class="sxs-lookup"><span data-stu-id="14703-227">**Influence bandwidth**: You can influence hello bandwidth used for replication by using a couple of registry keys:</span></span>
  * <span data-ttu-id="14703-228">hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM**登錄值會指定 hello 磁碟的資料傳輸 （初始或差異複寫） 所使用的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="14703-228">hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** registry value specifies hello number of threads that are used for data transfer (initial or delta replication) of a disk.</span></span> <span data-ttu-id="14703-229">較高的值會增加 hello 網路頻寬用於複寫。</span><span class="sxs-lookup"><span data-stu-id="14703-229">A higher value increases hello network bandwidth used for replication.</span></span>
  * <span data-ttu-id="14703-230">hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM**指定 hello 容錯回復期間用來傳送資料的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="14703-230">hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** specifies hello number of threads used for data transfer during failback.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="14703-231">節流頻寬</span><span class="sxs-lookup"><span data-stu-id="14703-231">Throttle bandwidth</span></span>

1. <span data-ttu-id="14703-232">開啟 Azure 備份 MMC 嵌入式管理單元在 hello 機器採取行動的 hello hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="14703-232">Open hello Azure Backup MMC snap-in on hello machine acting as hello process server.</span></span> <span data-ttu-id="14703-233">根據預設，備份的捷徑可在 hello 桌面上或 hello 下列資料夾中： C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin。</span><span class="sxs-lookup"><span data-stu-id="14703-233">By default, a shortcut for Backup is available on hello desktop, or in hello following folder: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="14703-234">在 hello 嵌入式管理單元，按一下 **變更屬性**。</span><span class="sxs-lookup"><span data-stu-id="14703-234">In hello snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="14703-235">在 hello**節流**索引標籤上，選取**啟用網際網路頻寬使用節流設定的備份操作**。</span><span class="sxs-lookup"><span data-stu-id="14703-235">On hello **Throttling** tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>
4. <span data-ttu-id="14703-236">設定工作的 hello 限制和非工作小時。</span><span class="sxs-lookup"><span data-stu-id="14703-236">Set hello limits for work and non-work hours.</span></span> <span data-ttu-id="14703-237">有效範圍是從每秒 512 Kbps too102 Mbps。</span><span class="sxs-lookup"><span data-stu-id="14703-237">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![節流](./media/vmware-walkthrough-capacity/throttle2.png)

<span data-ttu-id="14703-239">您也可以使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 節流。</span><span class="sxs-lookup"><span data-stu-id="14703-239">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="14703-240">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="14703-240">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="14703-241">**Set-OBMachineSetting -NoThrottle** 表示不需要節流。</span><span class="sxs-lookup"><span data-stu-id="14703-241">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth-for-a-vm"></a><span data-ttu-id="14703-242">影響 VM 的網路頻寬</span><span class="sxs-lookup"><span data-stu-id="14703-242">Influence network bandwidth for a VM</span></span>

1. <span data-ttu-id="14703-243">在登錄中的 hello VM，請移過**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。</span><span class="sxs-lookup"><span data-stu-id="14703-243">In registry of hello VM, go too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="14703-244">tooinfluence hello 頻寬流量複寫在磁碟上，修改 hello 值**UploadThreadsPerVM**，或建立 hello 索引鍵，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="14703-244">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value of **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="14703-245">從 Azure 容錯回復流量 tooinfluence hello 頻寬修改 hello 值**DownloadThreadsPerVM**。</span><span class="sxs-lookup"><span data-stu-id="14703-245">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value of **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="14703-246">hello 預設值為 4。</span><span class="sxs-lookup"><span data-stu-id="14703-246">hello default value is 4.</span></span> <span data-ttu-id="14703-247">在過度佈建的網路中，應該修改這些登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="14703-247">In an overprovisioned network, these registry keys should be modified.</span></span> <span data-ttu-id="14703-248">hello 上限為 32。</span><span class="sxs-lookup"><span data-stu-id="14703-248">hello maximum is 32.</span></span> <span data-ttu-id="14703-249">監視流量 toooptimize hello 值。</span><span class="sxs-lookup"><span data-stu-id="14703-249">Monitor traffic toooptimize hello value.</span></span>




## <a name="next-steps"></a><span data-ttu-id="14703-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14703-250">Next steps</span></span>

<span data-ttu-id="14703-251">跳過[步驟 4： 規劃網路](vmware-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="14703-251">Go too[Step 4: Plan networking](vmware-walkthrough-network.md).</span></span>
