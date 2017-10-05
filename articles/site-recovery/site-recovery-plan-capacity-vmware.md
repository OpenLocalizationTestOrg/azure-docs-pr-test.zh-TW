---
title: "使用 Azure Site Recovery 針對 VMware 到 Azure 的複寫進行容量和規模調整規劃 | Microsoft Docs"
description: "使用 Azure Site Recovery 將 VMware VM 複寫至 Azure 時，可使用本文來進行容量規劃和調整。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: rayne
ms.openlocfilehash: 8b580ac239bfb6d7b633fb03d4cfb91b168b0610
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="plan-capacity-and-scaling-for-vmware-replication-with-azure-site-recovery"></a><span data-ttu-id="22f68-103">使用 Azure Site Recovery 規劃容量並調整 Azure 中的 VMware 複寫</span><span class="sxs-lookup"><span data-stu-id="22f68-103">Plan capacity and scaling for VMware replication with Azure Site Recovery</span></span>

<span data-ttu-id="22f68-104">您可透過這篇文章，了解在使用 [Azure Site Recovery](site-recovery-overview.md) 將內部部署 VMware VM 和實體伺服器複寫至 Azure 時，如何進行容量規劃和調整。</span><span class="sxs-lookup"><span data-stu-id="22f68-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises VMware VMs and physical servers to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="22f68-105">如何開始容量規劃？</span><span class="sxs-lookup"><span data-stu-id="22f68-105">How do I start capacity planning?</span></span>

<span data-ttu-id="22f68-106">針對 VM 複寫，執行 [Azure Site Recovery Deployment Planner](https://aka.ms/asr-deployment-planner-doc) 以收集複寫環境的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="22f68-106">Gather information about your replication environment by running the [Azure Site Recovery Deployment Planner](https://aka.ms/asr-deployment-planner-doc) for VMware replication.</span></span> <span data-ttu-id="22f68-107">[深入了解](site-recovery-deployment-planner.md) 此工具。</span><span class="sxs-lookup"><span data-stu-id="22f68-107">[Learn more](site-recovery-deployment-planner.md) about this tool.</span></span> <span data-ttu-id="22f68-108">您可收集相容與不相容 VM、每個 VM 的磁碟，以及每個磁碟的資料變換等相關資訊。</span><span class="sxs-lookup"><span data-stu-id="22f68-108">You'll gather information about compatible and incompatible VMs, disks per VM, and data churn per disk.</span></span> <span data-ttu-id="22f68-109">此工具也涵蓋網路頻寬需求，以及要成功複寫和測試容錯移轉所需的 Azure 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="22f68-109">The tool also covers network bandwidth requirements, and the Azure infrastructure needed for successful replication and test failover.</span></span>

## <a name="capacity-considerations"></a><span data-ttu-id="22f68-110">容量考量</span><span class="sxs-lookup"><span data-stu-id="22f68-110">Capacity considerations</span></span>

<span data-ttu-id="22f68-111">**元件**</span><span class="sxs-lookup"><span data-stu-id="22f68-111">**Component**</span></span> | <span data-ttu-id="22f68-112">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="22f68-112">**Details**</span></span> |
--- | --- | ---
<span data-ttu-id="22f68-113">**複寫**</span><span class="sxs-lookup"><span data-stu-id="22f68-113">**Replication**</span></span> | <span data-ttu-id="22f68-114">**每日變更率上限：**受保護的機器只能使用一部處理序伺服器，而且單一處理序伺服器可處理的每日變更率最多為 2 TB。</span><span class="sxs-lookup"><span data-stu-id="22f68-114">**Maximum daily change rate:** A protected machine can only use one process server, and a single process server can handle a daily change rate up to 2 TB.</span></span> <span data-ttu-id="22f68-115">因此 2 TB 是針對受保護機器支援的每日資料變更率上限。</span><span class="sxs-lookup"><span data-stu-id="22f68-115">Thus 2 TB is the maximum daily data change rate that’s supported for a protected machine.</span></span><br/><br/> <span data-ttu-id="22f68-116">**最大輸送量：**複寫的機器可以屬於 Azure 中的一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="22f68-116">**Maximum throughput:** A replicated machine can belong to one storage account in Azure.</span></span> <span data-ttu-id="22f68-117">標準儲存體帳戶每秒可處理最多 20000 個要求，建議您將來源機器的每秒輸入/輸出作業 (IOPS) 數保持為 20000。</span><span class="sxs-lookup"><span data-stu-id="22f68-117">A standard storage account can handle a maximum of 20,000 requests per second, and we recommend that you keep the number of input/output operations per second (IOPS) across a source machine to 20,000.</span></span> <span data-ttu-id="22f68-118">例如，如果您有一部具備 5 個磁碟的來源機器，並且在來源機器上的每個磁碟會產生 120 個 IOP (8K 大小)，則它會在 Azure 每個磁碟 IOPS 限制 500 之內 </span><span class="sxs-lookup"><span data-stu-id="22f68-118">For example, if you have a source machine with 5 disks, and each disk generates 120 IOPS (8K size) on the source machine, then it will be within the Azure per disk IOPS limit of 500.</span></span> <span data-ttu-id="22f68-119">(所需的儲存體帳戶數目等於來源機器 IOPS 總數除以 20000)。</span><span class="sxs-lookup"><span data-stu-id="22f68-119">(The number of storage accounts required is equal to the total source machine IOPS, divided by 20,000.)</span></span>
<span data-ttu-id="22f68-120">**組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="22f68-120">**Configuration server**</span></span> | <span data-ttu-id="22f68-121">組態伺服器應該要能夠處理在受保護機器上執行之所有工作負載的每日變更率容量，因此需要足夠頻寬以持續地將資料複寫到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="22f68-121">The configuration server should be able to handle the daily change rate capacity across all workloads running on protected machines, and needs sufficient bandwidth to continuously replicate data to Azure Storage.</span></span><br/><br/> <span data-ttu-id="22f68-122">最佳做法是將組態伺服器放在與您想要保護的機器相同的網路與 LAN 區段上。</span><span class="sxs-lookup"><span data-stu-id="22f68-122">As a best practice, locate the configuration server on the same network and LAN segment as the machines you want to protect.</span></span> <span data-ttu-id="22f68-123">它可以位於不同的網路，但是您想要保護的機器應該具有第 3 層網路可見性。</span><span class="sxs-lookup"><span data-stu-id="22f68-123">It can be located on a different network, but machines you want to protect should have layer 3 network visibility to it.</span></span><br/><br/> <span data-ttu-id="22f68-124">下一節的資料表會摘要說明組態伺服器的大小建議。</span><span class="sxs-lookup"><span data-stu-id="22f68-124">Size recommendations for the configuration server are summarized in the table in the following section.</span></span>
<span data-ttu-id="22f68-125">**處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="22f68-125">**Process server**</span></span> | <span data-ttu-id="22f68-126">組態伺服器上會安裝第一部處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-126">The first process server is installed by default on the configuration server.</span></span> <span data-ttu-id="22f68-127">您可以部署額外的處理序伺服器來調整您的環境。</span><span class="sxs-lookup"><span data-stu-id="22f68-127">You can deploy additional process servers to scale your environment.</span></span> <br/><br/> <span data-ttu-id="22f68-128">處理序伺服器會從受保護的機器接收複寫資料，並透過快取、壓縮和加密予以最佳化。</span><span class="sxs-lookup"><span data-stu-id="22f68-128">The process server receives replication data from protected machines, and optimizes it with caching, compression, and encryption.</span></span> <span data-ttu-id="22f68-129">然後，它會將資料傳送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="22f68-129">Then it sends the data to Azure.</span></span> <span data-ttu-id="22f68-130">處理序伺服器機器應該要有足夠的資源來執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="22f68-130">The process server machine should have sufficient resources to perform these tasks.</span></span><br/><br/> <span data-ttu-id="22f68-131">處理序伺服器使用磁碟快取。</span><span class="sxs-lookup"><span data-stu-id="22f68-131">The process server uses a disk-based cache.</span></span> <span data-ttu-id="22f68-132">請另外使用一個 600 GB 以上的快取磁碟，來處理發生網路瓶頸或中斷時儲存的資料變更。</span><span class="sxs-lookup"><span data-stu-id="22f68-132">Use a separate cache disk of 600 GB or more to handle data changes stored in the event of a network bottleneck or outage.</span></span>

## <a name="size-recommendations-for-the-configuration-server"></a><span data-ttu-id="22f68-133">組態伺服器的大小建議</span><span class="sxs-lookup"><span data-stu-id="22f68-133">Size recommendations for the configuration server</span></span>

<span data-ttu-id="22f68-134">**CPU**</span><span class="sxs-lookup"><span data-stu-id="22f68-134">**CPU**</span></span> | <span data-ttu-id="22f68-135">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="22f68-135">**Memory**</span></span> | <span data-ttu-id="22f68-136">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="22f68-136">**Cache disk size**</span></span> | <span data-ttu-id="22f68-137">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="22f68-137">**Data change rate**</span></span> | <span data-ttu-id="22f68-138">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="22f68-138">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="22f68-139">8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="22f68-139">8 vCPUs (2 sockets * 4 cores @ 2.5 gigahertz [GHz])</span></span> | <span data-ttu-id="22f68-140">16 GB</span><span class="sxs-lookup"><span data-stu-id="22f68-140">16 GB</span></span> | <span data-ttu-id="22f68-141">300 GB</span><span class="sxs-lookup"><span data-stu-id="22f68-141">300 GB</span></span> | <span data-ttu-id="22f68-142">500 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="22f68-142">500 GB or less</span></span> | <span data-ttu-id="22f68-143">複寫少於 100 部機器。</span><span class="sxs-lookup"><span data-stu-id="22f68-143">Replicate less than 100 machines.</span></span>
<span data-ttu-id="22f68-144">12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="22f68-144">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="22f68-145">18 GB</span><span class="sxs-lookup"><span data-stu-id="22f68-145">18 GB</span></span> | <span data-ttu-id="22f68-146">600 GB</span><span class="sxs-lookup"><span data-stu-id="22f68-146">600 GB</span></span> | <span data-ttu-id="22f68-147">500 GB 至 1 TB</span><span class="sxs-lookup"><span data-stu-id="22f68-147">500 GB to 1 TB</span></span> | <span data-ttu-id="22f68-148">複寫 100-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="22f68-148">Replicate between 100-150 machines.</span></span>
<span data-ttu-id="22f68-149">16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="22f68-149">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="22f68-150">32 GB</span><span class="sxs-lookup"><span data-stu-id="22f68-150">32 GB</span></span> | <span data-ttu-id="22f68-151">1 TB</span><span class="sxs-lookup"><span data-stu-id="22f68-151">1 TB</span></span> | <span data-ttu-id="22f68-152">1 TB 至 2 TB</span><span class="sxs-lookup"><span data-stu-id="22f68-152">1 TB to 2 TB</span></span> | <span data-ttu-id="22f68-153">複寫 150-200 部機器。</span><span class="sxs-lookup"><span data-stu-id="22f68-153">Replicate between 150-200 machines.</span></span>
<span data-ttu-id="22f68-154">部署另一個處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="22f68-154">Deploy another process server</span></span> | | | <span data-ttu-id="22f68-155">> 2 TB</span><span class="sxs-lookup"><span data-stu-id="22f68-155">> 2 TB</span></span> | <span data-ttu-id="22f68-156">如果您要複寫 200 部以上的機器，或如果每日資料變更率超過 2 TB，部署額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-156">Deploy additional process servers if you're replicating more than 200 machines, or if the daily data change rate exceeds 2 TB.</span></span>

<span data-ttu-id="22f68-157">其中：</span><span class="sxs-lookup"><span data-stu-id="22f68-157">Where:</span></span>

* <span data-ttu-id="22f68-158">每個來源機器已設定各 100 GB 的 3 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="22f68-158">Each source machine is configured with 3 disks of 100 GB each.</span></span>
* <span data-ttu-id="22f68-159">我們使用具有 RAID 10 的 8 個 10 K RPM 的 SAS 磁碟機的效能評定儲存體以進行快取磁碟度量。</span><span class="sxs-lookup"><span data-stu-id="22f68-159">We used benchmarking storage of 8 SAS drives of 10 K RPM, with RAID 10, for cache disk measurements.</span></span>

## <a name="size-recommendations-for-the-process-server"></a><span data-ttu-id="22f68-160">處理序伺服器的大小建議</span><span class="sxs-lookup"><span data-stu-id="22f68-160">Size recommendations for the process server</span></span>

<span data-ttu-id="22f68-161">如果您要保護超過 200 部機器，或每日變更率大於 2 TB，您可以新增處理序伺服器來處理複寫負載。</span><span class="sxs-lookup"><span data-stu-id="22f68-161">If you need to protect more than 200 machines, or the daily change rate is greater than 2 TB, you can add process servers to handle the replication load.</span></span> <span data-ttu-id="22f68-162">若要擴充，您可以：</span><span class="sxs-lookup"><span data-stu-id="22f68-162">To scale out, you can:</span></span>

* <span data-ttu-id="22f68-163">增加組態伺服器的數目。</span><span class="sxs-lookup"><span data-stu-id="22f68-163">Increase the number of configuration servers.</span></span> <span data-ttu-id="22f68-164">例如，您可以使用兩部組態伺服器保護最多 400 部機器。</span><span class="sxs-lookup"><span data-stu-id="22f68-164">For example, you can protect up to 400 machines with two configuration servers.</span></span>
* <span data-ttu-id="22f68-165">新增更多的處理序伺服器並使用它們來處理流量，以取代 (或搭配) 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-165">Add more process servers, and use these to handle traffic instead of (or in addition to) the configuration server.</span></span>

<span data-ttu-id="22f68-166">下表描述情況如下的案例：</span><span class="sxs-lookup"><span data-stu-id="22f68-166">The following table describes a scenario in which:</span></span>

* <span data-ttu-id="22f68-167">您不打算使用組態伺服器作為處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-167">You're not planning to use the configuration server as a process server.</span></span>
* <span data-ttu-id="22f68-168">您已設定額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-168">You've set up an additional process server.</span></span>
* <span data-ttu-id="22f68-169">您已設定受保護的虛擬機器，以使用額外的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-169">You've configured protected virtual machines to use the additional process server.</span></span>
* <span data-ttu-id="22f68-170">每個受保護的來源機器已設定各 100 GB 的 3 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="22f68-170">Each protected source machine is configured with three disks of 100 GB each.</span></span>

<span data-ttu-id="22f68-171">**組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="22f68-171">**Configuration server**</span></span> | <span data-ttu-id="22f68-172">**額外處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="22f68-172">**Additional process server**</span></span> | <span data-ttu-id="22f68-173">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="22f68-173">**Cache disk size**</span></span> | <span data-ttu-id="22f68-174">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="22f68-174">**Data change rate**</span></span> | <span data-ttu-id="22f68-175">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="22f68-175">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="22f68-176">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="22f68-176">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="22f68-177">4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5 GHz)，8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="22f68-177">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8 GB memory</span></span> | <span data-ttu-id="22f68-178">300 GB</span><span class="sxs-lookup"><span data-stu-id="22f68-178">300 GB</span></span> | <span data-ttu-id="22f68-179">250 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="22f68-179">250 GB or less</span></span> | <span data-ttu-id="22f68-180">複寫 85 部或更少的機器。</span><span class="sxs-lookup"><span data-stu-id="22f68-180">Replicate 85 or fewer machines.</span></span>
<span data-ttu-id="22f68-181">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="22f68-181">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="22f68-182">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，12 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="22f68-182">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12 GB memory</span></span> | <span data-ttu-id="22f68-183">600 GB</span><span class="sxs-lookup"><span data-stu-id="22f68-183">600 GB</span></span> | <span data-ttu-id="22f68-184">250 GB 至 1 TB</span><span class="sxs-lookup"><span data-stu-id="22f68-184">250 GB to 1 TB</span></span> | <span data-ttu-id="22f68-185">複寫 85-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="22f68-185">Replicate between 85-150 machines.</span></span>
<span data-ttu-id="22f68-186">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，18 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="22f68-186">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz), 18 GB memory</span></span> | <span data-ttu-id="22f68-187">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，24 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="22f68-187">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24 GB memory</span></span> | <span data-ttu-id="22f68-188">1 TB</span><span class="sxs-lookup"><span data-stu-id="22f68-188">1 TB</span></span> | <span data-ttu-id="22f68-189">1 TB 至 2 TB</span><span class="sxs-lookup"><span data-stu-id="22f68-189">1 TB to 2 TB</span></span> | <span data-ttu-id="22f68-190">複寫 150-225 部機器。</span><span class="sxs-lookup"><span data-stu-id="22f68-190">Replicate between 150-225 machines.</span></span>

<span data-ttu-id="22f68-191">您調整伺服器的方式取決於相應增加或相應放大模型的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="22f68-191">The way in which you scale your servers depends on your preference for a scale-up or scale-out model.</span></span>  <span data-ttu-id="22f68-192">您部署幾個高階組態和處理序伺服器以相應增加，或使用較少的資源部署更多伺服器以相應放大。</span><span class="sxs-lookup"><span data-stu-id="22f68-192">You scale up by deploying a few high-end configuration and process servers, or scale out by deploying more servers with fewer resources.</span></span> <span data-ttu-id="22f68-193">例如，如果您需要保護 220 部機器，您可以執行下列任一項：</span><span class="sxs-lookup"><span data-stu-id="22f68-193">For example, if you need to protect 220 machines, you could do either of the following:</span></span>

* <span data-ttu-id="22f68-194">設定有 12 個 vCPU、18 GB 記憶體的組態伺服器，並另外設定一部有 12 個 vCPU、24 GB 記憶體的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-194">Set up the configuration server with 12 vCPU, 18 GB of memory, and an additional process server with 12 vCPU, 24 GB of memory.</span></span> <span data-ttu-id="22f68-195">將受保護機器設定為只使用額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-195">Configure protected machines to use the additional process server only.</span></span>
* <span data-ttu-id="22f68-196">設定兩部組態伺服器 (2 x 8 個 vCPU、16 GB RAM)，並另外設定兩部處理序伺服器 (1 x 8 個 vCPU 和 1 x 4 個 vCPU，以處理 135 + 85 [220] 部機器)。</span><span class="sxs-lookup"><span data-stu-id="22f68-196">Set up two configuration servers (2 x 8 vCPU, 16 GB RAM) and two additional process servers (1 x 8 vCPU and 4 vCPU x 1 to handle 135 + 85 [220] machines).</span></span> <span data-ttu-id="22f68-197">將受保護機器設定為只使用額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-197">Configure protected machines to use the additional process servers only.</span></span>


## <a name="control-network-bandwidth"></a><span data-ttu-id="22f68-198">控制網路頻寬</span><span class="sxs-lookup"><span data-stu-id="22f68-198">Control network bandwidth</span></span>

<span data-ttu-id="22f68-199">在使用 [Deployment Planner 工具](site-recovery-deployment-planner.md)來計算複寫 (初始複寫，然後是差異複寫) 所需的頻寬之後，您可以使用幾個選項來控制用於複寫的頻寬大小：</span><span class="sxs-lookup"><span data-stu-id="22f68-199">After you've used the [the Deployment Planner tool](site-recovery-deployment-planner.md) to calculate the bandwidth you need for replication (the initial replication and then delta), you can control the amount of bandwidth used for replication using a couple of options:</span></span>

* <span data-ttu-id="22f68-200">**節流頻寬**︰複寫至 Azure 的 VMware 流量會經過特定的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-200">**Throttle bandwidth**: VMware traffic that replicates to Azure goes through a specific process server.</span></span> <span data-ttu-id="22f68-201">您可在執行作為處理序伺服器的機器上進行頻寬節流。</span><span class="sxs-lookup"><span data-stu-id="22f68-201">You can throttle bandwidth on the machines running as process servers.</span></span>
* <span data-ttu-id="22f68-202">**影響頻寬**︰您可以使用幾個登錄機碼來影響用於複寫的頻寬：</span><span class="sxs-lookup"><span data-stu-id="22f68-202">**Influence bandwidth**: You can influence the bandwidth used for replication by using a couple of registry keys:</span></span>
  * <span data-ttu-id="22f68-203">**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** 登錄值可指定用於磁碟資料傳輸 (初始或差異複寫) 的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="22f68-203">The **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** registry value specifies the number of threads that are used for data transfer (initial or delta replication) of a disk.</span></span> <span data-ttu-id="22f68-204">較高的值可增加複寫所用的網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="22f68-204">A higher value increases the network bandwidth used for replication.</span></span>
  * <span data-ttu-id="22f68-205">**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** 可指定在容錯回復期間用於資料傳輸的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="22f68-205">The **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** specifies the number of threads used for data transfer during failback.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="22f68-206">節流頻寬</span><span class="sxs-lookup"><span data-stu-id="22f68-206">Throttle bandwidth</span></span>

1. <span data-ttu-id="22f68-207">在作為處理序伺服器的機器上開啟 Azure 備份 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="22f68-207">Open the Azure Backup MMC snap-in on the machine acting as the process server.</span></span> <span data-ttu-id="22f68-208">根據預設，備份的捷徑位於桌面上或在下列資料夾中：C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin。</span><span class="sxs-lookup"><span data-stu-id="22f68-208">By default, a shortcut for Backup is available on the desktop, or in the following folder: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="22f68-209">在嵌入式管理單元中，按一下 [變更屬性]。</span><span class="sxs-lookup"><span data-stu-id="22f68-209">In the snap-in, click **Change Properties**.</span></span>

    ![用以變更屬性之 Azure 備份 MMC 嵌入式管理單元選項的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/throttle1.png)
3. <span data-ttu-id="22f68-211">在 [節流] 索引標籤上，選取 [啟用備份作業的網際網路頻寬使用節流功能]。</span><span class="sxs-lookup"><span data-stu-id="22f68-211">On the **Throttling** tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span> <span data-ttu-id="22f68-212">設定工作和非工作時數的限制。</span><span class="sxs-lookup"><span data-stu-id="22f68-212">Set the limits for work and non-work hours.</span></span> <span data-ttu-id="22f68-213">有效範圍是每秒 512 Kbps 到 102 Mbps。</span><span class="sxs-lookup"><span data-stu-id="22f68-213">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![[Azure 備份屬性] 對話方塊的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/throttle2.png)

<span data-ttu-id="22f68-215">您也可以使用 [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) Cmdlet 來設定節流。</span><span class="sxs-lookup"><span data-stu-id="22f68-215">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="22f68-216">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="22f68-216">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="22f68-217">**Set-OBMachineSetting -NoThrottle** 表示不需要節流。</span><span class="sxs-lookup"><span data-stu-id="22f68-217">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth-for-a-vm"></a><span data-ttu-id="22f68-218">影響 VM 的網路頻寬</span><span class="sxs-lookup"><span data-stu-id="22f68-218">Influence network bandwidth for a VM</span></span>

1. <span data-ttu-id="22f68-219">在 VM 的登錄中，瀏覽至 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。</span><span class="sxs-lookup"><span data-stu-id="22f68-219">In the VM's registry, navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="22f68-220">若要影響複製磁碟上的頻寬流量，請修改 **UploadThreadsPerVM** 的值，如果不存在則請建立機碼。</span><span class="sxs-lookup"><span data-stu-id="22f68-220">To influence the bandwidth traffic on a replicating disk, modify the value of **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="22f68-221">若要影響從 Azure 容錯回復流量的頻寬，請修改 **DownloadThreadsPerVM** 的值。</span><span class="sxs-lookup"><span data-stu-id="22f68-221">To influence the bandwidth for failback traffic from Azure, modify the value of **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="22f68-222">預設值為 4。</span><span class="sxs-lookup"><span data-stu-id="22f68-222">The default value is 4.</span></span> <span data-ttu-id="22f68-223">在 “overprovisioned” 網路中，這些登錄機碼必須變更自其預設值。</span><span class="sxs-lookup"><span data-stu-id="22f68-223">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="22f68-224">最大值為 32。</span><span class="sxs-lookup"><span data-stu-id="22f68-224">The maximum is 32.</span></span> <span data-ttu-id="22f68-225">監視流量，將此值最佳化。</span><span class="sxs-lookup"><span data-stu-id="22f68-225">Monitor traffic to optimize the value.</span></span>


## <a name="deploy-additional-process-servers"></a><span data-ttu-id="22f68-226">部署額外處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="22f68-226">Deploy additional process servers</span></span>

<span data-ttu-id="22f68-227">如果您必須將您的部署相應放大至超過 200 部來源機器，或是擁有總計超過 2 TB 的每日變換率，您便需要額外的處理序伺服器來處理流量。</span><span class="sxs-lookup"><span data-stu-id="22f68-227">If you have to scale out your deployment beyond 200 source machines, or you have a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span> <span data-ttu-id="22f68-228">遵循這些指示以設定處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-228">Follow these instructions to set up the process server.</span></span> <span data-ttu-id="22f68-229">設定伺服器之後，請移轉來源機器以便使用它。</span><span class="sxs-lookup"><span data-stu-id="22f68-229">After setting up the server, you migrate source machines to use it.</span></span>

1. <span data-ttu-id="22f68-230">在 [Site Recovery 伺服器] 中，依序按一下 [組態伺服器] 和 [處理序伺服器]。</span><span class="sxs-lookup"><span data-stu-id="22f68-230">In **Site Recovery servers**, click the configuration server, and then click **Process Server**.</span></span>

    ![要新增處理序伺服器之 Site Recovery 伺服器選項的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/migrate-ps1.png)
2. <span data-ttu-id="22f68-232">在 [伺服器類型] 中，按一下 [處理伺服器 (內部部署)]。</span><span class="sxs-lookup"><span data-stu-id="22f68-232">In **Server type**, click **Process server (on-premises)**.</span></span>

    ![[處理序伺服器] 對話方塊的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
3. <span data-ttu-id="22f68-234">下載 Site Recovery 統一安裝檔案，然後執行它以安裝處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-234">Download the Site Recovery Unified Setup file, and run it to install the process server.</span></span> <span data-ttu-id="22f68-235">這也會在保存庫中註冊處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-235">This also registers it in the vault.</span></span>
4. <span data-ttu-id="22f68-236">在 [開始之前] 中，選取 [新增額外處理序伺服器以相應放大部署]。</span><span class="sxs-lookup"><span data-stu-id="22f68-236">In **Before you begin**, select **Add additional process servers to scale out deployment**.</span></span>
5. <span data-ttu-id="22f68-237">以您 [設定](#step-2-set-up-the-source-environment) 組態伺服器時的相同方式完成精靈。</span><span class="sxs-lookup"><span data-stu-id="22f68-237">Complete the wizard in the same way you did when you [set up](#step-2-set-up-the-source-environment) the configuration server.</span></span>

    ![Azure Site Recovery 統一安裝精靈的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/add-ps1.png)
6. <span data-ttu-id="22f68-239">在 [組態伺服器詳細資料] 中，指定組態伺服器的 IP 位址，以及複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="22f68-239">In **Configuration Server Details**, specify the IP address of the configuration server, and the passphrase.</span></span> <span data-ttu-id="22f68-240">若要取得複雜密碼，請在組態伺服器上執行 **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n**。</span><span class="sxs-lookup"><span data-stu-id="22f68-240">To obtain the passphrase, run **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n** on the configuration server.</span></span>

    ![[組態伺服器詳細資料] 頁面的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/add-ps2.png)

### <a name="migrate-machines-to-use-the-new-process-server"></a><span data-ttu-id="22f68-242">移轉機器以使用新的處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="22f68-242">Migrate machines to use the new process server</span></span>
1. <span data-ttu-id="22f68-243">在 [設定] > [Site Recovery 伺服器] 中，按一下組態伺服器，然後展開 [處理伺服器]。</span><span class="sxs-lookup"><span data-stu-id="22f68-243">In **Settings** > **Site Recovery servers**, click the configuration server, and then expand **Process servers**.</span></span>

    ![[處理序伺服器] 對話方塊的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
2. <span data-ttu-id="22f68-245">以滑鼠右鍵按一下目前使用中的處理序伺服器，然後按一下 [切換]。</span><span class="sxs-lookup"><span data-stu-id="22f68-245">Right-click the process server currently in use, and click **Switch**.</span></span>

    ![[組態伺服器] 對話方塊的螢幕擷取畫面](./media/site-recovery-vmware-to-azure/migrate-ps3.png)
3. <span data-ttu-id="22f68-247">在 [選取目標處理序伺服器] 中，選取您要使用的新處理序伺服器，然後選取該伺服器將處理的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="22f68-247">In **Select target process server**, select the new process server you want to use, and then select the virtual machines that the server will handle.</span></span> <span data-ttu-id="22f68-248">按一下資訊圖示以取得伺服器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="22f68-248">Click the information icon to get information about the server.</span></span> <span data-ttu-id="22f68-249">為了協助您進行負載的判斷，會顯示將每個選取的虛擬機器複寫到新的處理序伺服器所需的平均空間。</span><span class="sxs-lookup"><span data-stu-id="22f68-249">To help you make load decisions, the average space that's needed to replicate each selected virtual machine to the new process server is displayed.</span></span> <span data-ttu-id="22f68-250">按一下核取記號以開始複寫到新處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="22f68-250">Click the check mark to start replicating to the new process server.</span></span>


## <a name="next-steps"></a><span data-ttu-id="22f68-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22f68-251">Next steps</span></span>

<span data-ttu-id="22f68-252">下載並執行 [Azure Site Recovery Deployment Planner](https://aka.ms/asr-deployment-planner)。</span><span class="sxs-lookup"><span data-stu-id="22f68-252">Download and run the [Azure Site Recovery Deployment Planner](https://aka.ms/asr-deployment-planner)</span></span>