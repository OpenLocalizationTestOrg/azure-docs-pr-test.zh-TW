---
title: "使用 Azure Site Recovery 針對 VMware 到 Azure 的複寫進行容量和規模調整規劃 | Microsoft Docs"
description: "使用 Azure Site Recovery 將 VMware VM 複寫至 Azure 時，可參考本文來進行容量和規模調整規劃"
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
ms.openlocfilehash: f5b334e594e3d002e1862b25c4faba7163efa7d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-vmware-to-azure-replication"></a><span data-ttu-id="e9bfd-103">步驟 3：針對 VMware 到 Azure 的複寫進行容量和規模調整規劃</span><span class="sxs-lookup"><span data-stu-id="e9bfd-103">Step 3: Plan capacity and scaling for VMware to Azure replication</span></span>

<span data-ttu-id="e9bfd-104">使用這篇文章來了解使用 [Azure Site Recovery](site-recovery-overview.md) 將內部部署 VMware VM 和實體伺服器複寫至 Azure 時，如何進行容量和規模調整規劃。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises VMware VMs and physical servers to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="e9bfd-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="e9bfd-106">如何開始容量規劃？</span><span class="sxs-lookup"><span data-stu-id="e9bfd-106">How do I start capacity planning?</span></span>

<span data-ttu-id="e9bfd-107">您需收集複寫環境的相關資訊，然後使用此資訊搭配本文中強調的考量事項來規劃容量。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-107">You gather information about your replication environment, and then plan capacity using this information, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="e9bfd-108">收集資訊</span><span class="sxs-lookup"><span data-stu-id="e9bfd-108">Gather information</span></span>

1. <span data-ttu-id="e9bfd-109">下載用於 VMware 複寫的[部署規劃工具](https://aka.ms/asr-deployment-planner)。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-109">Download the [Deployment Planner tool](https://aka.ms/asr-deployment-planner) for VMware replication.</span></span>
2. <span data-ttu-id="e9bfd-110">[閱讀這篇文章](site-recovery-deployment-planner.md)以了解如何執行此工具。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-110">[Read this article](site-recovery-deployment-planner.md) to understand how to run the tool.</span></span>
3. <span data-ttu-id="e9bfd-111">使用此工具，您將可收集相容和不相容 VM、每個 VM 的磁碟，以及每個磁碟的資料變換等相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-111">Using the tool you gather information about compatible and incompatible VMs, disks per VM, and data churn per disk.</span></span> <span data-ttu-id="e9bfd-112">此工具也涵蓋網路頻寬需求，以及要成功複寫和測試容錯移轉所需的 Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-112">The tool also covers network bandwidth requirements, and the Azure infrastructure needed for successful replication and test failover.</span></span>

## <a name="replication-considerations"></a><span data-ttu-id="e9bfd-113">複寫考量</span><span class="sxs-lookup"><span data-stu-id="e9bfd-113">Replication considerations</span></span>

<span data-ttu-id="e9bfd-114">開始部署之前，請注意下列考量：</span><span class="sxs-lookup"><span data-stu-id="e9bfd-114">Note these considerations before you start deployment:</span></span>

<span data-ttu-id="e9bfd-115">**元件**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-115">**Component**</span></span> | <span data-ttu-id="e9bfd-116">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-116">**Details**</span></span> |
--- | --- | ---
<span data-ttu-id="e9bfd-117">**複寫**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-117">**Replication**</span></span> | <span data-ttu-id="e9bfd-118">**每日變更率上限：**受保護的機器只能使用一部處理序伺服器，而且單一處理序伺服器可處理的每日變更率最多為 2 TB。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-118">**Maximum daily change rate:** A protected machine can only use one process server, and a single process server can handle a daily change rate up to 2 TB.</span></span> <span data-ttu-id="e9bfd-119">因此 2 TB 是針對受保護機器支援的每日資料變更率上限。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-119">Thus 2 TB is the maximum daily data change rate that’s supported for a protected machine.</span></span><br/><br/> <span data-ttu-id="e9bfd-120">**最大輸送量：**複寫的機器可以屬於 Azure 中的一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-120">**Maximum throughput:** A replicated machine can belong to one storage account in Azure.</span></span> <span data-ttu-id="e9bfd-121">標準儲存體帳戶每秒可處理最多 20000 個要求，建議您將來源機器的每秒輸入/輸出作業 (IOPS) 數保持為 20000。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-121">A standard storage account can handle a maximum of 20,000 requests per second, and we recommend that you keep the number of input/output operations per second (IOPS) across a source machine to 20,000.</span></span> <span data-ttu-id="e9bfd-122">例如，如果您有一部具備 5 個磁碟的來源機器，並且在來源機器上的每個磁碟會產生 120 個 IOP (8K 大小)，則它會在 Azure 每個磁碟 IOPS 限制 500 之內 </span><span class="sxs-lookup"><span data-stu-id="e9bfd-122">For example, if you have a source machine with 5 disks, and each disk generates 120 IOPS (8K size) on the source machine, then it will be within the Azure per disk IOPS limit of 500.</span></span> <span data-ttu-id="e9bfd-123">(所需的儲存體帳戶數目等於來源機器 IOPS 總數除以 20000)。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-123">(The number of storage accounts required is equal to the total source machine IOPS, divided by 20,000.)</span></span>

## <a name="configuration-server-capacity"></a><span data-ttu-id="e9bfd-124">組態伺服器容量</span><span class="sxs-lookup"><span data-stu-id="e9bfd-124">Configuration server capacity</span></span>

<span data-ttu-id="e9bfd-125">組態伺服器應該要能夠處理在受保護機器上執行之所有工作負載的每日變更率容量，因此需要足夠頻寬以持續地將資料複寫到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-125">The configuration server should be able to handle the daily change rate capacity across all workloads running on protected machines, and needs sufficient bandwidth to continuously replicate data to Azure Storage.</span></span>

<span data-ttu-id="e9bfd-126">最佳做法是將組態伺服器放在與您想要保護的機器相同的網路與 LAN 區段上。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-126">As a best practice, locate the configuration server on the same network and LAN segment as the machines you want to protect.</span></span> <span data-ttu-id="e9bfd-127">它可以位於不同的網路，但是您想要保護的機器應該具有第 3 層網路可見性。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-127">It can be located on a different network, but machines you want to protect should have layer 3 network visibility to it.</span></span>

## <a name="sizing-recommendations"></a><span data-ttu-id="e9bfd-128">大小調整建議</span><span class="sxs-lookup"><span data-stu-id="e9bfd-128">Sizing recommendations</span></span>

<span data-ttu-id="e9bfd-129">下表根據 CPU 來摘要說明大小調整建議。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-129">The table summarizes sizing recommendations based on CPU.</span></span>

<span data-ttu-id="e9bfd-130">**CPU**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-130">**CPU**</span></span> | <span data-ttu-id="e9bfd-131">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-131">**Memory**</span></span> | <span data-ttu-id="e9bfd-132">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-132">**Cache disk size**</span></span> | <span data-ttu-id="e9bfd-133">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-133">**Data change rate**</span></span> | <span data-ttu-id="e9bfd-134">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-134">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="e9bfd-135">8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e9bfd-135">8 vCPUs (2 sockets * 4 cores @ 2.5 gigahertz [GHz])</span></span> | <span data-ttu-id="e9bfd-136">16 GB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-136">16 GB</span></span> | <span data-ttu-id="e9bfd-137">300 GB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-137">300 GB</span></span> | <span data-ttu-id="e9bfd-138">500 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="e9bfd-138">500 GB or less</span></span> | <span data-ttu-id="e9bfd-139">複寫少於 100 部機器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-139">Replicate less than 100 machines.</span></span>
<span data-ttu-id="e9bfd-140">12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e9bfd-140">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="e9bfd-141">18 GB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-141">18 GB</span></span> | <span data-ttu-id="e9bfd-142">600 GB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-142">600 GB</span></span> | <span data-ttu-id="e9bfd-143">500 GB 至 1 TB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-143">500 GB to 1 TB</span></span> | <span data-ttu-id="e9bfd-144">複寫 100-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-144">Replicate between 100-150 machines.</span></span>
<span data-ttu-id="e9bfd-145">16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="e9bfd-145">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="e9bfd-146">32 GB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-146">32 GB</span></span> | <span data-ttu-id="e9bfd-147">1 TB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-147">1 TB</span></span> | <span data-ttu-id="e9bfd-148">1 TB 至 2 TB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-148">1 TB to 2 TB</span></span> | <span data-ttu-id="e9bfd-149">複寫 150-200 部機器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-149">Replicate between 150-200 machines.</span></span>
<span data-ttu-id="e9bfd-150">部署另一個處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="e9bfd-150">Deploy another process server</span></span> | | | <span data-ttu-id="e9bfd-151">> 2 TB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-151">> 2 TB</span></span> | <span data-ttu-id="e9bfd-152">如果您要複寫 200 部以上的機器，或如果每日資料變更率超過 2 TB，部署額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-152">Deploy additional process servers if you're replicating more than 200 machines, or if the daily data change rate exceeds 2 TB.</span></span>

<span data-ttu-id="e9bfd-153">其中：</span><span class="sxs-lookup"><span data-stu-id="e9bfd-153">Where:</span></span>

* <span data-ttu-id="e9bfd-154">每個來源機器已設定各 100 GB 的 3 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-154">Each source machine is configured with 3 disks of 100 GB each.</span></span>
* <span data-ttu-id="e9bfd-155">我們使用具有 RAID 10 的 8 個 10 K RPM 的 SAS 磁碟機的效能評定儲存體以進行快取磁碟度量。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-155">We used benchmarking storage of 8 SAS drives of 10 K RPM, with RAID 10, for cache disk measurements.</span></span>

## <a name="process-server-capacity"></a><span data-ttu-id="e9bfd-156">處理伺服器容量</span><span class="sxs-lookup"><span data-stu-id="e9bfd-156">Process server capacity</span></span>


<span data-ttu-id="e9bfd-157">處理序伺服器會從受保護的機器接收複寫資料，並透過快取、壓縮和加密予以最佳化。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-157">The process server receives replication data from protected machines, and optimizes it with caching, compression, and encryption.</span></span> <span data-ttu-id="e9bfd-158">然後，它會將資料傳送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-158">Then it sends the data to Azure.</span></span>

- <span data-ttu-id="e9bfd-159">處理序伺服器機器應該要有足夠的資源來執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-159">The process server machine should have sufficient resources to perform these tasks.</span></span>
- <span data-ttu-id="e9bfd-160">組態伺服器上會安裝第一部處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-160">The first process server is installed by default on the configuration server.</span></span> <span data-ttu-id="e9bfd-161">您可以部署額外的處理序伺服器來調整您的環境。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-161">You can deploy additional process servers to scale your environment.</span></span>
- <span data-ttu-id="e9bfd-162">處理序伺服器使用磁碟快取。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-162">The process server uses a disk-based cache.</span></span> <span data-ttu-id="e9bfd-163">請另外使用一個 600 GB 以上的快取磁碟，來處理發生網路瓶頸或中斷時儲存的資料變更。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-163">Use a separate cache disk of 600 GB or more to handle data changes stored in the event of a network bottleneck or outage.</span></span>
- <span data-ttu-id="e9bfd-164">如果您要保護超過 200 部機器，或每日變更率大於 2 TB，您可以新增處理序伺服器來處理複寫負載。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-164">If you need to protect more than 200 machines, or the daily change rate is greater than 2 TB, you can add process servers to handle the replication load.</span></span> <span data-ttu-id="e9bfd-165">若要擴充，您可以：</span><span class="sxs-lookup"><span data-stu-id="e9bfd-165">To scale out, you can:</span></span>
    - <span data-ttu-id="e9bfd-166">增加組態伺服器的數目。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-166">Increase the number of configuration servers.</span></span> <span data-ttu-id="e9bfd-167">例如，您可以使用兩部組態伺服器保護最多 400 部機器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-167">For example, you can protect up to 400 machines with two configuration servers.</span></span>
    - <span data-ttu-id="e9bfd-168">新增更多的處理序伺服器並使用它們來處理流量，以取代 (或搭配) 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-168">Add more process servers, and use these to handle traffic instead of (or in addition to) the configuration server.</span></span>


### <a name="example-process-server-scaling"></a><span data-ttu-id="e9bfd-169">範例處理伺服器調整</span><span class="sxs-lookup"><span data-stu-id="e9bfd-169">Example process server scaling</span></span>

<span data-ttu-id="e9bfd-170">下表描述情況如下的案例：</span><span class="sxs-lookup"><span data-stu-id="e9bfd-170">The following table describes a scenario in which:</span></span>

* <span data-ttu-id="e9bfd-171">您不打算使用組態伺服器作為處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-171">You're not planning to use the configuration server as a process server.</span></span>
* <span data-ttu-id="e9bfd-172">您已設定額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-172">You've set up an additional process server.</span></span>
* <span data-ttu-id="e9bfd-173">您已設定受保護的虛擬機器，以使用額外的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-173">You've configured protected virtual machines to use the additional process server.</span></span>
* <span data-ttu-id="e9bfd-174">每個受保護的來源機器已設定各 100 GB 的 3 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-174">Each protected source machine is configured with three disks of 100 GB each.</span></span>

<span data-ttu-id="e9bfd-175">**組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-175">**Configuration server**</span></span> | <span data-ttu-id="e9bfd-176">**額外處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-176">**Additional process server**</span></span> | <span data-ttu-id="e9bfd-177">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-177">**Cache disk size**</span></span> | <span data-ttu-id="e9bfd-178">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-178">**Data change rate**</span></span> | <span data-ttu-id="e9bfd-179">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="e9bfd-179">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="e9bfd-180">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="e9bfd-180">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="e9bfd-181">4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5 GHz)，8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="e9bfd-181">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8 GB memory</span></span> | <span data-ttu-id="e9bfd-182">300 GB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-182">300 GB</span></span> | <span data-ttu-id="e9bfd-183">250 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="e9bfd-183">250 GB or less</span></span> | <span data-ttu-id="e9bfd-184">複寫 85 部或更少的機器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-184">Replicate 85 or fewer machines.</span></span>
<span data-ttu-id="e9bfd-185">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="e9bfd-185">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="e9bfd-186">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，12 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="e9bfd-186">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12 GB memory</span></span> | <span data-ttu-id="e9bfd-187">600 GB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-187">600 GB</span></span> | <span data-ttu-id="e9bfd-188">250 GB 至 1 TB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-188">250 GB to 1 TB</span></span> | <span data-ttu-id="e9bfd-189">複寫 85-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-189">Replicate between 85-150 machines.</span></span>
<span data-ttu-id="e9bfd-190">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，18 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="e9bfd-190">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz), 18 GB memory</span></span> | <span data-ttu-id="e9bfd-191">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，24 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="e9bfd-191">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24 GB memory</span></span> | <span data-ttu-id="e9bfd-192">1 TB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-192">1 TB</span></span> | <span data-ttu-id="e9bfd-193">1 TB 至 2 TB</span><span class="sxs-lookup"><span data-stu-id="e9bfd-193">1 TB to 2 TB</span></span> | <span data-ttu-id="e9bfd-194">複寫 150-225 部機器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-194">Replicate between 150-225 machines.</span></span>

<span data-ttu-id="e9bfd-195">您調整伺服器的方式取決於相應增加或相應放大模型的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-195">The way in which you scale your servers depends on your preference for a scale-up or scale-out model.</span></span>  <span data-ttu-id="e9bfd-196">您部署幾個高階組態和處理序伺服器以相應增加，或使用較少的資源部署更多伺服器以相應放大。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-196">You scale up by deploying a few high-end configuration and process servers, or scale out by deploying more servers with fewer resources.</span></span> <span data-ttu-id="e9bfd-197">例如，如果您需要保護 220 部機器，您可以執行下列任一項：</span><span class="sxs-lookup"><span data-stu-id="e9bfd-197">For example, if you need to protect 220 machines, you could do either of the following:</span></span>

* <span data-ttu-id="e9bfd-198">設定有 12 個 vCPU、18 GB 記憶體的組態伺服器，並另外設定一部有 12 個 vCPU、24 GB 記憶體的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-198">Set up the configuration server with 12 vCPU, 18 GB of memory, and an additional process server with 12 vCPU, 24 GB of memory.</span></span> <span data-ttu-id="e9bfd-199">將受保護機器設定為只使用額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-199">Configure protected machines to use the additional process server only.</span></span>
* <span data-ttu-id="e9bfd-200">設定兩部組態伺服器 (2 x 8 個 vCPU、16 GB RAM)，並另外設定兩部處理序伺服器 (1 x 8 個 vCPU 和 1 x 4 個 vCPU，以處理 135 + 85 [220] 部機器)。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-200">Set up two configuration servers (2 x 8 vCPU, 16 GB RAM) and two additional process servers (1 x 8 vCPU and 4 vCPU x 1 to handle 135 + 85 [220] machines).</span></span> <span data-ttu-id="e9bfd-201">將受保護機器設定為只使用額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-201">Configure protected machines to use the additional process servers only.</span></span>

## <a name="deploy-additional-process-servers"></a><span data-ttu-id="e9bfd-202">部署額外處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="e9bfd-202">Deploy additional process servers</span></span>

<span data-ttu-id="e9bfd-203">請依照下列指示來設定額外的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-203">Follow these instructions to set up an additional process server.</span></span> <span data-ttu-id="e9bfd-204">設定伺服器之後，請移轉來源機器以便使用它。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-204">After setting up the server, you migrate source machines to use it.</span></span>

1. <span data-ttu-id="e9bfd-205">在 [Site Recovery 伺服器] 中，按一下組態伺服器 > [+處理伺服器]。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-205">In **Site Recovery servers**, click the configuration server > **+Process Server**.</span></span>
2. <span data-ttu-id="e9bfd-206">在 [伺服器類型] 中，按一下 [處理伺服器 (內部部署)]。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-206">In **Server type**, click **Process server (on-premises)**.</span></span>

    ![處理序伺服器](./media/vmware-walkthrough-capacity/migrate-ps2.png)
3. <span data-ttu-id="e9bfd-208">下載 Site Recovery「整合安裝」檔案。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-208">Download the Site Recovery Unified Setup file.</span></span>
4. <span data-ttu-id="e9bfd-209">執行安裝程式來安裝處理伺服器，然後在保存庫中註冊它。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-209">Run setup to install the process server, and register it in the vault.</span></span>
5. <span data-ttu-id="e9bfd-210">在 [開始之前] 中，選取 [新增額外處理序伺服器以相應放大部署]。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-210">In **Before you begin**, select **Add additional process servers to scale out deployment**.</span></span>
6. <span data-ttu-id="e9bfd-211">在 [組態伺服器詳細資料] 中，指定組態伺服器的 IP 位址，以及複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-211">In **Configuration Server Details**, specify the IP address of the configuration server, and the passphrase.</span></span> <span data-ttu-id="e9bfd-212">如果您沒有複雜密碼，請在組態伺服器上執行 **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n** 來取得它。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-212">If you don't have the passphrase, get it by running **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n** on the configuration server.</span></span>

    ![組態伺服器](./media/vmware-walkthrough-capacity/add-ps2.png)
7. <span data-ttu-id="e9bfd-214">執行安裝程式的剩餘步驟，就像您安裝組態伺服器時一樣。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-214">Complete the rest of setup in the same way you did when you set up the configuration server.</span></span>

### <a name="migrate-machines-to-use-the-process-server"></a><span data-ttu-id="e9bfd-215">移轉機器以使用處理伺服器</span><span class="sxs-lookup"><span data-stu-id="e9bfd-215">Migrate machines to use the process server</span></span>

1. <span data-ttu-id="e9bfd-216">在 [設定] > [Site Recovery 伺服器] 中，按一下組態伺服器 > [處理序伺服器]。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-216">In **Settings** > **Site Recovery servers**, click the configuration server > **Process servers**.</span></span>
2. <span data-ttu-id="e9bfd-217">在目前使用中的處理伺服器上按一下滑鼠右鍵 > [切換]。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-217">Right-click the process server currently in use > **Switch**.</span></span>

    ![切換處理伺服器](./media/vmware-walkthrough-capacity/migrate-ps3.png)
3. <span data-ttu-id="e9bfd-219">在 [選取目標處理伺服器] 中，選取您想要使用的處理伺服器，然後選取該伺服器將處理的 VM。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-219">In **Select target process server**, select the process server you want to use, and select the VMs that the server will handle.</span></span>
4. <span data-ttu-id="e9bfd-220">按一下資訊圖示。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-220">Click the information icon.</span></span> <span data-ttu-id="e9bfd-221">為了協助您進行負載決策，會顯示將每個選取的 VM 複寫到新處理伺服器所需的平均空間。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-221">To help you make load decisions, the average space that's needed to replicate each selected VM to the new process server is displayed.</span></span>
5. <span data-ttu-id="e9bfd-222">按一下核取記號以開始複寫到新的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-222">Click the check mark to start replication to the new process server.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="e9bfd-223">控制網路頻寬</span><span class="sxs-lookup"><span data-stu-id="e9bfd-223">Control network bandwidth</span></span>

<span data-ttu-id="e9bfd-224">在執行[部署規劃工具](site-recovery-deployment-planner.md)來計算複寫 (初始複寫，然後是差異複寫) 所需的頻寬之後，您可以使用幾個選項來控制用於複寫的頻寬大小：</span><span class="sxs-lookup"><span data-stu-id="e9bfd-224">After you run [the Deployment Planner tool](site-recovery-deployment-planner.md) to calculate the bandwidth you need for replication (the initial replication and then delta), you can control the amount of bandwidth used for replication using a couple of options:</span></span>

* <span data-ttu-id="e9bfd-225">**節流頻寬**︰複寫至 Azure 的 VMware 流量會經過特定的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-225">**Throttle bandwidth**: VMware traffic that replicates to Azure goes through a specific process server.</span></span> <span data-ttu-id="e9bfd-226">您可在執行作為處理序伺服器的機器上進行頻寬節流。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-226">You can throttle bandwidth on the machines running as process servers.</span></span>
* <span data-ttu-id="e9bfd-227">**影響頻寬**︰您可以使用幾個登錄機碼來影響用於複寫的頻寬：</span><span class="sxs-lookup"><span data-stu-id="e9bfd-227">**Influence bandwidth**: You can influence the bandwidth used for replication by using a couple of registry keys:</span></span>
  * <span data-ttu-id="e9bfd-228">**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** 登錄值可指定用於磁碟資料傳輸 (初始或差異複寫) 的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-228">The **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** registry value specifies the number of threads that are used for data transfer (initial or delta replication) of a disk.</span></span> <span data-ttu-id="e9bfd-229">較高的值可增加複寫所用的網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-229">A higher value increases the network bandwidth used for replication.</span></span>
  * <span data-ttu-id="e9bfd-230">**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** 可指定在容錯回復期間用於資料傳輸的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-230">The **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** specifies the number of threads used for data transfer during failback.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="e9bfd-231">節流頻寬</span><span class="sxs-lookup"><span data-stu-id="e9bfd-231">Throttle bandwidth</span></span>

1. <span data-ttu-id="e9bfd-232">在作為處理序伺服器的機器上開啟 Azure 備份 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-232">Open the Azure Backup MMC snap-in on the machine acting as the process server.</span></span> <span data-ttu-id="e9bfd-233">根據預設，備份的捷徑位於桌面上或在下列資料夾中：C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-233">By default, a shortcut for Backup is available on the desktop, or in the following folder: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="e9bfd-234">在嵌入式管理單元中，按一下 [變更屬性]。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-234">In the snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="e9bfd-235">在 [節流] 索引標籤上，選取 [啟用備份作業的網際網路頻寬使用節流功能]。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-235">On the **Throttling** tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>
4. <span data-ttu-id="e9bfd-236">設定工作和非工作時數的限制。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-236">Set the limits for work and non-work hours.</span></span> <span data-ttu-id="e9bfd-237">有效範圍是每秒 512 Kbps 到 102 Mbps。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-237">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![節流](./media/vmware-walkthrough-capacity/throttle2.png)

<span data-ttu-id="e9bfd-239">您也可以使用 [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) Cmdlet 來設定節流。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-239">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="e9bfd-240">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="e9bfd-240">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="e9bfd-241">**Set-OBMachineSetting -NoThrottle** 表示不需要節流。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-241">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth-for-a-vm"></a><span data-ttu-id="e9bfd-242">影響 VM 的網路頻寬</span><span class="sxs-lookup"><span data-stu-id="e9bfd-242">Influence network bandwidth for a VM</span></span>

1. <span data-ttu-id="e9bfd-243">在 VM 的登錄中，移至 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-243">In registry of the VM, go to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="e9bfd-244">若要影響複製磁碟上的頻寬流量，請修改 **UploadThreadsPerVM** 的值，如果不存在則請建立機碼。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-244">To influence the bandwidth traffic on a replicating disk, modify the value of **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="e9bfd-245">若要影響從 Azure 容錯回復流量的頻寬，請修改 **DownloadThreadsPerVM** 的值。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-245">To influence the bandwidth for failback traffic from Azure, modify the value of **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="e9bfd-246">預設值為 4。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-246">The default value is 4.</span></span> <span data-ttu-id="e9bfd-247">在過度佈建的網路中，應該修改這些登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-247">In an overprovisioned network, these registry keys should be modified.</span></span> <span data-ttu-id="e9bfd-248">最大值為 32。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-248">The maximum is 32.</span></span> <span data-ttu-id="e9bfd-249">監視流量，將此值最佳化。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-249">Monitor traffic to optimize the value.</span></span>




## <a name="next-steps"></a><span data-ttu-id="e9bfd-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9bfd-250">Next steps</span></span>

<span data-ttu-id="e9bfd-251">移至[步驟 4：規劃網路](vmware-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="e9bfd-251">Go to [Step 4: Plan networking](vmware-walkthrough-network.md).</span></span>
