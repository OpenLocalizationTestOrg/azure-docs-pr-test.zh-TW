---
title: "使用 Azure Site Recovery 針對實體伺服器到 Azure 的複寫進行容量和規模調整規劃 | Microsoft Docs"
description: "使用 Azure Site Recovery 將 Windows/Linux 實體伺服器複寫至 Azure 時，可參考本文來進行容量和規模調整規劃"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 554f59ee-0b49-4779-9737-90cb601ef6fe
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 971ad6dd39f94aa7944f6ed3b31bc3acc605d9a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-physical-server-to-azure-replication"></a><span data-ttu-id="bf011-103">步驟 3：針對實體伺服器到 Azure 的複寫進行容量和規模調整規劃</span><span class="sxs-lookup"><span data-stu-id="bf011-103">Step 3: Plan capacity and scaling for physical server to Azure replication</span></span>

<span data-ttu-id="bf011-104">使用 [Azure Site Recovery](site-recovery-overview.md) 將內部部署 Windows/Linux 實體伺服器複寫至 Azure 時，可參考本文來了解容量和規模調整。</span><span class="sxs-lookup"><span data-stu-id="bf011-104">Use this article to figure out capacity and scaling, when you're replicating on-premises Windows/Linux physical servers to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="bf011-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="bf011-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="plan-deployment-capacity"></a><span data-ttu-id="bf011-106">規劃部署容量</span><span class="sxs-lookup"><span data-stu-id="bf011-106">Plan deployment capacity</span></span>

1. <span data-ttu-id="bf011-107">若要了解如何預估複寫需求，以及如何調整 Site Recovery 元件大小，請參閱這篇[文章](site-recovery-plan-capacity-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="bf011-107">Read this [article](site-recovery-plan-capacity-vmware.md) to learn about estimating replication requirements, and guidance for sizing Site Recovery components.</span></span>
2. <span data-ttu-id="bf011-108">若要了解如何調整元件伺服器規模，以及如何控制複寫之機器的頻寬，請參閱下面的考量。</span><span class="sxs-lookup"><span data-stu-id="bf011-108">Read the considerations below to learn about scaling component servers, and controlling replicated machine bandwidth.</span></span>

## <a name="replication-considerations"></a><span data-ttu-id="bf011-109">複寫考量</span><span class="sxs-lookup"><span data-stu-id="bf011-109">Replication considerations</span></span>

<span data-ttu-id="bf011-110">請使用下列考量來了解複寫之伺服器的需求。</span><span class="sxs-lookup"><span data-stu-id="bf011-110">Use these considerations to figure out replicated server requirements.</span></span>

<span data-ttu-id="bf011-111">**元件**</span><span class="sxs-lookup"><span data-stu-id="bf011-111">**Component**</span></span> | <span data-ttu-id="bf011-112">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="bf011-112">**Details**</span></span> 
--- | --- 
<span data-ttu-id="bf011-113">**複寫**</span><span class="sxs-lookup"><span data-stu-id="bf011-113">**Replication**</span></span> | <span data-ttu-id="bf011-114">**每日變更率上限：**受保護的機器只能使用一部處理序伺服器，而且單一處理序伺服器可處理的每日變更率最多為 2 TB。</span><span class="sxs-lookup"><span data-stu-id="bf011-114">**Maximum daily change rate:** A protected machine can only use one process server, and a single process server can handle a daily change rate up to 2 TB.</span></span> <span data-ttu-id="bf011-115">因此 2 TB 是針對受保護機器支援的每日資料變更率上限。</span><span class="sxs-lookup"><span data-stu-id="bf011-115">Thus 2 TB is the maximum daily data change rate that’s supported for a protected machine.</span></span><br/><br/> <span data-ttu-id="bf011-116">**最大輸送量：**複寫的機器可以屬於 Azure 中的一個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bf011-116">**Maximum throughput:** A replicated machine can belong to one storage account in Azure.</span></span> <span data-ttu-id="bf011-117">標準儲存體帳戶每秒可處理最多 20000 個要求，建議您將來源機器的每秒輸入/輸出作業 (IOPS) 數保持為 20000。</span><span class="sxs-lookup"><span data-stu-id="bf011-117">A standard storage account can handle a maximum of 20,000 requests per second, and we recommend that you keep the number of input/output operations per second (IOPS) across a source machine to 20,000.</span></span> <span data-ttu-id="bf011-118">例如，如果您有一部具備 5 個磁碟的來源機器，並且在來源機器上的每個磁碟會產生 120 個 IOP (8K 大小)，則它會在 Azure 每個磁碟 IOPS 限制 500 之內 </span><span class="sxs-lookup"><span data-stu-id="bf011-118">For example, if you have a source machine with 5 disks, and each disk generates 120 IOPS (8K size) on the source machine, then it will be within the Azure per disk IOPS limit of 500.</span></span> <span data-ttu-id="bf011-119">(所需的儲存體帳戶數目等於來源機器 IOPS 總數除以 20000)。</span><span class="sxs-lookup"><span data-stu-id="bf011-119">(The number of storage accounts required is equal to the total source machine IOPS, divided by 20,000.)</span></span>

## <a name="configuration-server-capacity"></a><span data-ttu-id="bf011-120">組態伺服器容量</span><span class="sxs-lookup"><span data-stu-id="bf011-120">Configuration server capacity</span></span>

<span data-ttu-id="bf011-121">組態伺服器應該要能夠處理在受保護機器上執行之所有工作負載的每日變更率容量，因此需要足夠頻寬以持續地將資料複寫到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="bf011-121">The configuration server should be able to handle the daily change rate capacity across all workloads running on protected machines, and needs sufficient bandwidth to continuously replicate data to Azure Storage.</span></span>

<span data-ttu-id="bf011-122">最佳做法是將組態伺服器放在與您想要保護的機器相同的網路與 LAN 區段上。</span><span class="sxs-lookup"><span data-stu-id="bf011-122">As a best practice, locate the configuration server on the same network and LAN segment as the machines you want to protect.</span></span> <span data-ttu-id="bf011-123">它可以位於不同的網路，但是您想要保護的機器應該具有第 3 層網路可見性。</span><span class="sxs-lookup"><span data-stu-id="bf011-123">It can be located on a different network, but machines you want to protect should have layer 3 network visibility to it.</span></span>

## <a name="sizing-recommendations"></a><span data-ttu-id="bf011-124">大小調整建議</span><span class="sxs-lookup"><span data-stu-id="bf011-124">Sizing recommendations</span></span>

<span data-ttu-id="bf011-125">下表根據 CPU 來摘要說明大小調整建議。</span><span class="sxs-lookup"><span data-stu-id="bf011-125">The table summarizes sizing recommendations based on CPU.</span></span>

<span data-ttu-id="bf011-126">**CPU**</span><span class="sxs-lookup"><span data-stu-id="bf011-126">**CPU**</span></span> | <span data-ttu-id="bf011-127">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="bf011-127">**Memory**</span></span> | <span data-ttu-id="bf011-128">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="bf011-128">**Cache disk size**</span></span> | <span data-ttu-id="bf011-129">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="bf011-129">**Data change rate**</span></span> | <span data-ttu-id="bf011-130">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="bf011-130">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="bf011-131">8 個 vCPU (2 個插槽 * 4 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="bf011-131">8 vCPUs (2 sockets * 4 cores @ 2.5 gigahertz [GHz])</span></span> | <span data-ttu-id="bf011-132">16 GB</span><span class="sxs-lookup"><span data-stu-id="bf011-132">16 GB</span></span> | <span data-ttu-id="bf011-133">300 GB</span><span class="sxs-lookup"><span data-stu-id="bf011-133">300 GB</span></span> | <span data-ttu-id="bf011-134">500 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="bf011-134">500 GB or less</span></span> | <span data-ttu-id="bf011-135">複寫少於 100 部機器。</span><span class="sxs-lookup"><span data-stu-id="bf011-135">Replicate less than 100 machines.</span></span>
<span data-ttu-id="bf011-136">12 個 vCPU (2 個插槽 * 6 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="bf011-136">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="bf011-137">18 GB</span><span class="sxs-lookup"><span data-stu-id="bf011-137">18 GB</span></span> | <span data-ttu-id="bf011-138">600 GB</span><span class="sxs-lookup"><span data-stu-id="bf011-138">600 GB</span></span> | <span data-ttu-id="bf011-139">500 GB 至 1 TB</span><span class="sxs-lookup"><span data-stu-id="bf011-139">500 GB to 1 TB</span></span> | <span data-ttu-id="bf011-140">複寫 100-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="bf011-140">Replicate between 100-150 machines.</span></span>
<span data-ttu-id="bf011-141">16 個 vCPU (2 個插槽 * 8 核心 @ 2.5GHz)</span><span class="sxs-lookup"><span data-stu-id="bf011-141">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> | <span data-ttu-id="bf011-142">32 GB</span><span class="sxs-lookup"><span data-stu-id="bf011-142">32 GB</span></span> | <span data-ttu-id="bf011-143">1 TB</span><span class="sxs-lookup"><span data-stu-id="bf011-143">1 TB</span></span> | <span data-ttu-id="bf011-144">1 TB 至 2 TB</span><span class="sxs-lookup"><span data-stu-id="bf011-144">1 TB to 2 TB</span></span> | <span data-ttu-id="bf011-145">複寫 150-200 部機器。</span><span class="sxs-lookup"><span data-stu-id="bf011-145">Replicate between 150-200 machines.</span></span>
<span data-ttu-id="bf011-146">部署另一個處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="bf011-146">Deploy another process server</span></span> | | | <span data-ttu-id="bf011-147">> 2 TB</span><span class="sxs-lookup"><span data-stu-id="bf011-147">> 2 TB</span></span> | <span data-ttu-id="bf011-148">如果您要複寫 200 部以上的機器，或如果每日資料變更率超過 2 TB，部署額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-148">Deploy additional process servers if you're replicating more than 200 machines, or if the daily data change rate exceeds 2 TB.</span></span>

<span data-ttu-id="bf011-149">其中：</span><span class="sxs-lookup"><span data-stu-id="bf011-149">Where:</span></span>

* <span data-ttu-id="bf011-150">每個來源機器已設定各 100 GB 的 3 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="bf011-150">Each source machine is configured with 3 disks of 100 GB each.</span></span>
* <span data-ttu-id="bf011-151">我們使用具有 RAID 10 的 8 個 10 K RPM 的 SAS 磁碟機的效能評定儲存體以進行快取磁碟度量。</span><span class="sxs-lookup"><span data-stu-id="bf011-151">We used benchmarking storage of 8 SAS drives of 10 K RPM, with RAID 10, for cache disk measurements.</span></span>

## <a name="process-server-capacity"></a><span data-ttu-id="bf011-152">處理伺服器容量</span><span class="sxs-lookup"><span data-stu-id="bf011-152">Process server capacity</span></span>


<span data-ttu-id="bf011-153">處理序伺服器會從受保護的機器接收複寫資料，並透過快取、壓縮和加密予以最佳化。</span><span class="sxs-lookup"><span data-stu-id="bf011-153">The process server receives replication data from protected machines, and optimizes it with caching, compression, and encryption.</span></span> <span data-ttu-id="bf011-154">然後，它會將資料傳送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="bf011-154">Then it sends the data to Azure.</span></span>

- <span data-ttu-id="bf011-155">處理序伺服器機器應該要有足夠的資源來執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="bf011-155">The process server machine should have sufficient resources to perform these tasks.</span></span>
- <span data-ttu-id="bf011-156">組態伺服器上會安裝第一部處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-156">The first process server is installed by default on the configuration server.</span></span> <span data-ttu-id="bf011-157">您可以部署額外的處理序伺服器來調整您的環境。</span><span class="sxs-lookup"><span data-stu-id="bf011-157">You can deploy additional process servers to scale your environment.</span></span>
- <span data-ttu-id="bf011-158">處理序伺服器使用磁碟快取。</span><span class="sxs-lookup"><span data-stu-id="bf011-158">The process server uses a disk-based cache.</span></span> <span data-ttu-id="bf011-159">請另外使用一個 600 GB 以上的快取磁碟，來處理發生網路瓶頸或中斷時儲存的資料變更。</span><span class="sxs-lookup"><span data-stu-id="bf011-159">Use a separate cache disk of 600 GB or more to handle data changes stored in the event of a network bottleneck or outage.</span></span>
- <span data-ttu-id="bf011-160">如果您要保護超過 200 部機器，或每日變更率大於 2 TB，您可以新增處理序伺服器來處理複寫負載。</span><span class="sxs-lookup"><span data-stu-id="bf011-160">If you need to protect more than 200 machines, or the daily change rate is greater than 2 TB, you can add process servers to handle the replication load.</span></span> <span data-ttu-id="bf011-161">若要擴充，您可以：</span><span class="sxs-lookup"><span data-stu-id="bf011-161">To scale out, you can:</span></span>
    - <span data-ttu-id="bf011-162">增加組態伺服器的數目。</span><span class="sxs-lookup"><span data-stu-id="bf011-162">Increase the number of configuration servers.</span></span> <span data-ttu-id="bf011-163">例如，您可以使用兩部組態伺服器保護最多 400 部機器。</span><span class="sxs-lookup"><span data-stu-id="bf011-163">For example, you can protect up to 400 machines with two configuration servers.</span></span>
    - <span data-ttu-id="bf011-164">新增更多的處理序伺服器並使用它們來處理流量，以取代 (或搭配) 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-164">Add more process servers, and use these to handle traffic instead of (or in addition to) the configuration server.</span></span>


### <a name="example-process-server-scaling"></a><span data-ttu-id="bf011-165">範例處理伺服器調整</span><span class="sxs-lookup"><span data-stu-id="bf011-165">Example process server scaling</span></span>

<span data-ttu-id="bf011-166">下表描述情況如下的案例：</span><span class="sxs-lookup"><span data-stu-id="bf011-166">The following table describes a scenario in which:</span></span>

* <span data-ttu-id="bf011-167">您不打算使用組態伺服器作為處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-167">You're not planning to use the configuration server as a process server.</span></span>
* <span data-ttu-id="bf011-168">您已設定額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-168">You've set up an additional process server.</span></span>
* <span data-ttu-id="bf011-169">您已設定受保護的虛擬機器，以使用額外的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-169">You've configured protected virtual machines to use the additional process server.</span></span>
* <span data-ttu-id="bf011-170">每個受保護的來源機器已設定各 100 GB 的 3 個磁碟。</span><span class="sxs-lookup"><span data-stu-id="bf011-170">Each protected source machine is configured with three disks of 100 GB each.</span></span>

<span data-ttu-id="bf011-171">**組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="bf011-171">**Configuration server**</span></span> | <span data-ttu-id="bf011-172">**額外處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="bf011-172">**Additional process server**</span></span> | <span data-ttu-id="bf011-173">**快取磁碟大小**</span><span class="sxs-lookup"><span data-stu-id="bf011-173">**Cache disk size**</span></span> | <span data-ttu-id="bf011-174">**資料變更率**</span><span class="sxs-lookup"><span data-stu-id="bf011-174">**Data change rate**</span></span> | <span data-ttu-id="bf011-175">**受保護的機器**</span><span class="sxs-lookup"><span data-stu-id="bf011-175">**Protected machines**</span></span>
--- | --- | --- | --- | ---
<span data-ttu-id="bf011-176">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="bf011-176">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="bf011-177">4 個 vCPU (2 個通訊端 * 雙核心 @ 2.5 GHz)，8 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="bf011-177">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8 GB memory</span></span> | <span data-ttu-id="bf011-178">300 GB</span><span class="sxs-lookup"><span data-stu-id="bf011-178">300 GB</span></span> | <span data-ttu-id="bf011-179">250 GB 或更少</span><span class="sxs-lookup"><span data-stu-id="bf011-179">250 GB or less</span></span> | <span data-ttu-id="bf011-180">複寫 85 部或更少的機器。</span><span class="sxs-lookup"><span data-stu-id="bf011-180">Replicate 85 or fewer machines.</span></span>
<span data-ttu-id="bf011-181">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，16 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="bf011-181">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 16 GB memory</span></span> | <span data-ttu-id="bf011-182">8 個 vCPU (2 個通訊端 * 四核心 @ 2.5 GHz)，12 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="bf011-182">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12 GB memory</span></span> | <span data-ttu-id="bf011-183">600 GB</span><span class="sxs-lookup"><span data-stu-id="bf011-183">600 GB</span></span> | <span data-ttu-id="bf011-184">250 GB 至 1 TB</span><span class="sxs-lookup"><span data-stu-id="bf011-184">250 GB to 1 TB</span></span> | <span data-ttu-id="bf011-185">複寫 85-150 部機器。</span><span class="sxs-lookup"><span data-stu-id="bf011-185">Replicate between 85-150 machines.</span></span>
<span data-ttu-id="bf011-186">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，18 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="bf011-186">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz), 18 GB memory</span></span> | <span data-ttu-id="bf011-187">12 個 vCPU (2 個通訊端 * 六核心 @ 2.5 GHz)，24 GB 記憶體</span><span class="sxs-lookup"><span data-stu-id="bf011-187">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24 GB memory</span></span> | <span data-ttu-id="bf011-188">1 TB</span><span class="sxs-lookup"><span data-stu-id="bf011-188">1 TB</span></span> | <span data-ttu-id="bf011-189">1 TB 至 2 TB</span><span class="sxs-lookup"><span data-stu-id="bf011-189">1 TB to 2 TB</span></span> | <span data-ttu-id="bf011-190">複寫 150-225 部機器。</span><span class="sxs-lookup"><span data-stu-id="bf011-190">Replicate between 150-225 machines.</span></span>

<span data-ttu-id="bf011-191">您調整伺服器的方式取決於相應增加或相應放大模型的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="bf011-191">The way in which you scale your servers depends on your preference for a scale-up or scale-out model.</span></span>  <span data-ttu-id="bf011-192">您部署幾個高階組態和處理序伺服器以相應增加，或使用較少的資源部署更多伺服器以相應放大。</span><span class="sxs-lookup"><span data-stu-id="bf011-192">You scale up by deploying a few high-end configuration and process servers, or scale out by deploying more servers with fewer resources.</span></span> <span data-ttu-id="bf011-193">例如，如果您需要保護 220 部機器，您可以執行下列任一項：</span><span class="sxs-lookup"><span data-stu-id="bf011-193">For example, if you need to protect 220 machines, you could do either of the following:</span></span>

* <span data-ttu-id="bf011-194">設定有 12 個 vCPU、18 GB 記憶體的組態伺服器，並另外設定一部有 12 個 vCPU、24 GB 記憶體的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-194">Set up the configuration server with 12 vCPU, 18 GB of memory, and an additional process server with 12 vCPU, 24 GB of memory.</span></span> <span data-ttu-id="bf011-195">將受保護機器設定為只使用額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-195">Configure protected machines to use the additional process server only.</span></span>
* <span data-ttu-id="bf011-196">設定兩部組態伺服器 (2 x 8 個 vCPU、16 GB RAM)，並另外設定兩部處理序伺服器 (1 x 8 個 vCPU 和 1 x 4 個 vCPU，以處理 135 + 85 [220] 部機器)。</span><span class="sxs-lookup"><span data-stu-id="bf011-196">Set up two configuration servers (2 x 8 vCPU, 16 GB RAM) and two additional process servers (1 x 8 vCPU and 4 vCPU x 1 to handle 135 + 85 [220] machines).</span></span> <span data-ttu-id="bf011-197">將受保護機器設定為只使用額外的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-197">Configure protected machines to use the additional process servers only.</span></span>

## <a name="deploy-additional-process-servers"></a><span data-ttu-id="bf011-198">部署額外處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="bf011-198">Deploy additional process servers</span></span>

1. <span data-ttu-id="bf011-199">依照[這些指示](site-recovery-vmware-setup-azure-ps-resource-manager.md)來設定額外的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-199">Follow [these instructions](site-recovery-vmware-setup-azure-ps-resource-manager.md) to set up an additional process server.</span></span>
2. <span data-ttu-id="bf011-200">如果您沒有複雜密碼，請在組態伺服器上執行 **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n** 來取得它。</span><span class="sxs-lookup"><span data-stu-id="bf011-200">If you don't have the passphrase, run **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n** on the configuration server to get it.</span></span>
3. <span data-ttu-id="bf011-201">設定處理伺服器之後，您需移轉來源機器以使用它。</span><span class="sxs-lookup"><span data-stu-id="bf011-201">After setting up the process server, you migrate source machines to use it.</span></span>

    1. <span data-ttu-id="bf011-202">在 [設定] > [Site Recovery 伺服器] 中，按一下組態伺服器 > [處理序伺服器]。</span><span class="sxs-lookup"><span data-stu-id="bf011-202">In **Settings** > **Site Recovery servers**, click the configuration server > **Process servers**.</span></span>
    2. <span data-ttu-id="bf011-203">在目前使用中的處理伺服器上按一下滑鼠右鍵 > [切換]。</span><span class="sxs-lookup"><span data-stu-id="bf011-203">Right-click the process server currently in use > **Switch**.</span></span>
    3. <span data-ttu-id="bf011-204">在 [選取目標處理伺服器] 中，選取您想要使用的處理伺服器，然後選取該伺服器將處理的 VM。</span><span class="sxs-lookup"><span data-stu-id="bf011-204">In **Select target process server**, select the process server you want to use, and select the VMs that the server will handle.</span></span>
    4. <span data-ttu-id="bf011-205">按一下資訊圖示。</span><span class="sxs-lookup"><span data-stu-id="bf011-205">Click the information icon.</span></span> <span data-ttu-id="bf011-206">為了協助您進行負載決策，會顯示將每個選取的 VM 複寫到新處理伺服器所需的平均空間。</span><span class="sxs-lookup"><span data-stu-id="bf011-206">To help you make load decisions, the average space that's needed to replicate each selected VM to the new process server is displayed.</span></span>
    5. <span data-ttu-id="bf011-207">按一下核取記號以開始複寫到新的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-207">Click the check mark to start replication to the new process server.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="bf011-208">控制網路頻寬</span><span class="sxs-lookup"><span data-stu-id="bf011-208">Control network bandwidth</span></span>

<span data-ttu-id="bf011-209">在執行[部署規劃工具](site-recovery-deployment-planner.md)來計算複寫 (初始複寫，然後是差異複寫) 所需的頻寬之後，您可以使用幾個選項來控制用於複寫的頻寬大小：</span><span class="sxs-lookup"><span data-stu-id="bf011-209">After you run [the Deployment Planner tool](site-recovery-deployment-planner.md) to calculate the bandwidth you need for replication (the initial replication and then delta), you can control the amount of bandwidth used for replication using a couple of options:</span></span>

* <span data-ttu-id="bf011-210">**節流頻寬**︰複寫至 Azure 的 VMware 流量會經過特定的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="bf011-210">**Throttle bandwidth**: VMware traffic that replicates to Azure goes through a specific process server.</span></span> <span data-ttu-id="bf011-211">您可在執行作為處理序伺服器的機器上進行頻寬節流。</span><span class="sxs-lookup"><span data-stu-id="bf011-211">You can throttle bandwidth on the machines running as process servers.</span></span>
* <span data-ttu-id="bf011-212">**影響頻寬**︰您可以使用幾個登錄機碼來影響用於複寫的頻寬：</span><span class="sxs-lookup"><span data-stu-id="bf011-212">**Influence bandwidth**: You can influence the bandwidth used for replication by using a couple of registry keys:</span></span>
  * <span data-ttu-id="bf011-213">**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** 登錄值可指定用於磁碟資料傳輸 (初始或差異複寫) 的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="bf011-213">The **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** registry value specifies the number of threads that are used for data transfer (initial or delta replication) of a disk.</span></span> <span data-ttu-id="bf011-214">較高的值可增加複寫所用的網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="bf011-214">A higher value increases the network bandwidth used for replication.</span></span>
  * <span data-ttu-id="bf011-215">**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** 可指定在容錯回復期間用於資料傳輸的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="bf011-215">The **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** specifies the number of threads used for data transfer during failback.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="bf011-216">節流頻寬</span><span class="sxs-lookup"><span data-stu-id="bf011-216">Throttle bandwidth</span></span>

1. <span data-ttu-id="bf011-217">在作為處理序伺服器的機器上開啟 Azure 備份 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="bf011-217">Open the Azure Backup MMC snap-in on the machine acting as the process server.</span></span> <span data-ttu-id="bf011-218">根據預設，備份的捷徑位於桌面上或在下列資料夾中：C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin。</span><span class="sxs-lookup"><span data-stu-id="bf011-218">By default, a shortcut for Backup is available on the desktop, or in the following folder: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="bf011-219">在嵌入式管理單元中，按一下 [變更屬性]。</span><span class="sxs-lookup"><span data-stu-id="bf011-219">In the snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="bf011-220">在 [節流] 索引標籤上，選取 [啟用備份作業的網際網路頻寬使用節流功能]。</span><span class="sxs-lookup"><span data-stu-id="bf011-220">On the **Throttling** tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>
4. <span data-ttu-id="bf011-221">設定工作和非工作時數的限制。</span><span class="sxs-lookup"><span data-stu-id="bf011-221">Set the limits for work and non-work hours.</span></span> <span data-ttu-id="bf011-222">有效範圍是每秒 512 Kbps 到 102 Mbps。</span><span class="sxs-lookup"><span data-stu-id="bf011-222">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![節流](./media/physical-walkthrough-capacity/throttle2.png)

<span data-ttu-id="bf011-224">您也可以使用 [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) Cmdlet 來設定節流。</span><span class="sxs-lookup"><span data-stu-id="bf011-224">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="bf011-225">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="bf011-225">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="bf011-226">**Set-OBMachineSetting -NoThrottle** 表示不需要節流。</span><span class="sxs-lookup"><span data-stu-id="bf011-226">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth-for-a-vm"></a><span data-ttu-id="bf011-227">影響 VM 的網路頻寬</span><span class="sxs-lookup"><span data-stu-id="bf011-227">Influence network bandwidth for a VM</span></span>

1. <span data-ttu-id="bf011-228">在 VM 的登錄中，移至 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。</span><span class="sxs-lookup"><span data-stu-id="bf011-228">In registry of the VM, go to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="bf011-229">若要影響複製磁碟上的頻寬流量，請修改 **UploadThreadsPerVM** 的值，如果不存在則請建立機碼。</span><span class="sxs-lookup"><span data-stu-id="bf011-229">To influence the bandwidth traffic on a replicating disk, modify the value of **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="bf011-230">若要影響從 Azure 容錯回復流量的頻寬，請修改 **DownloadThreadsPerVM** 的值。</span><span class="sxs-lookup"><span data-stu-id="bf011-230">To influence the bandwidth for failback traffic from Azure, modify the value of **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="bf011-231">預設值為 4。</span><span class="sxs-lookup"><span data-stu-id="bf011-231">The default value is 4.</span></span> <span data-ttu-id="bf011-232">在過度佈建的網路中，應該修改這些登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="bf011-232">In an overprovisioned network, these registry keys should be modified.</span></span> <span data-ttu-id="bf011-233">最大值為 32。</span><span class="sxs-lookup"><span data-stu-id="bf011-233">The maximum is 32.</span></span> <span data-ttu-id="bf011-234">監視流量，將此值最佳化。</span><span class="sxs-lookup"><span data-stu-id="bf011-234">Monitor traffic to optimize the value.</span></span>




## <a name="next-steps"></a><span data-ttu-id="bf011-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf011-235">Next steps</span></span>

<span data-ttu-id="bf011-236">移至[步驟 4：規劃網路](physical-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="bf011-236">Go to [Step 4: Plan networking](physical-walkthrough-network.md).</span></span>
