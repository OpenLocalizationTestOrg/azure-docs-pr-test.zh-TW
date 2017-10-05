---
title: "將傳統 VM 移轉到 ARM 受管理的磁碟 VM | Microsoft Docs"
description: "將單一 Azure VM 從傳統部署模型移轉至 Resource Manager 部署模型中的受管理的磁碟。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 82389834d85981c0ed71bdcc891fbfdbe1377654
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manually-migrate-a-classic-vm-to-a-new-arm-managed-disk-vm-from-the-vhd"></a><span data-ttu-id="af16d-103">手動從 VHD 將傳統 VM 移轉到新的 ARM 受管理的磁碟 VM</span><span class="sxs-lookup"><span data-stu-id="af16d-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span></span> 


<span data-ttu-id="af16d-104">本節協助您將現有 Azure VM 從傳統部署模型移轉至 Resource Manager 部署模型中的[受控磁碟](managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="af16d-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](managed-disks-overview.md) in the Resource Manager deployment model.</span></span>


## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="af16d-105">規劃移轉至受控磁碟</span><span class="sxs-lookup"><span data-stu-id="af16d-105">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="af16d-106">本節可協助您做出最佳的 VM 和磁碟類型決策。</span><span class="sxs-lookup"><span data-stu-id="af16d-106">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="af16d-107">位置</span><span class="sxs-lookup"><span data-stu-id="af16d-107">Location</span></span>

<span data-ttu-id="af16d-108">挑選 Azure 受控磁碟可用的位置。</span><span class="sxs-lookup"><span data-stu-id="af16d-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="af16d-109">如果您要移轉至進階受控磁碟，也請確保進階儲存體可用於您打算移轉至的區域。</span><span class="sxs-lookup"><span data-stu-id="af16d-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="af16d-110">如需可用位置的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。</span><span class="sxs-lookup"><span data-stu-id="af16d-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="af16d-111">VM 大小</span><span class="sxs-lookup"><span data-stu-id="af16d-111">VM sizes</span></span>

<span data-ttu-id="af16d-112">如果您要移轉至進階受控磁碟，您必須將 VM 大小更新為 VM 所在區域中進階儲存體可支援的大小。</span><span class="sxs-lookup"><span data-stu-id="af16d-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="af16d-113">檢閱進階儲存體可支援的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="af16d-113">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="af16d-114">Azure VM 大小的規格已列在 [虛擬機器的大小](sizes.md)一文中。</span><span class="sxs-lookup"><span data-stu-id="af16d-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="af16d-115">請檢閱使用於進階儲存體的虛擬機器效能特性，然後選擇最適合您的工作負載的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="af16d-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="af16d-116">確定 VM 上有足夠的磁碟流量頻寬。</span><span class="sxs-lookup"><span data-stu-id="af16d-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="af16d-117">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="af16d-117">Disk sizes</span></span>

<span data-ttu-id="af16d-118">**進階受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="af16d-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="af16d-119">有七種型別的進階受控磁碟可以搭配 VM 使用，而且每種都有特定的 IOP 和輸送量限制。</span><span class="sxs-lookup"><span data-stu-id="af16d-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="af16d-120">為您的 VM 選擇進階磁碟類型時，請根據應用程式在容量、效能、延展性以及尖峰負載方面的需求，將這些限制納入考量。</span><span class="sxs-lookup"><span data-stu-id="af16d-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="af16d-121">進階磁碟類型</span><span class="sxs-lookup"><span data-stu-id="af16d-121">Premium Disks Type</span></span>  | <span data-ttu-id="af16d-122">P4</span><span class="sxs-lookup"><span data-stu-id="af16d-122">P4</span></span>    | <span data-ttu-id="af16d-123">P6</span><span class="sxs-lookup"><span data-stu-id="af16d-123">P6</span></span>    | <span data-ttu-id="af16d-124">P10</span><span class="sxs-lookup"><span data-stu-id="af16d-124">P10</span></span>   | <span data-ttu-id="af16d-125">P20</span><span class="sxs-lookup"><span data-stu-id="af16d-125">P20</span></span>   | <span data-ttu-id="af16d-126">P30</span><span class="sxs-lookup"><span data-stu-id="af16d-126">P30</span></span>   | <span data-ttu-id="af16d-127">P40</span><span class="sxs-lookup"><span data-stu-id="af16d-127">P40</span></span>   | <span data-ttu-id="af16d-128">P50</span><span class="sxs-lookup"><span data-stu-id="af16d-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="af16d-129">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="af16d-129">Disk size</span></span>           | <span data-ttu-id="af16d-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="af16d-130">128 GB</span></span>| <span data-ttu-id="af16d-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="af16d-131">512 GB</span></span>| <span data-ttu-id="af16d-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="af16d-132">128 GB</span></span>| <span data-ttu-id="af16d-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="af16d-133">512 GB</span></span>            | <span data-ttu-id="af16d-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="af16d-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="af16d-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="af16d-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="af16d-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="af16d-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="af16d-137">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="af16d-137">IOPS per disk</span></span>       | <span data-ttu-id="af16d-138">120</span><span class="sxs-lookup"><span data-stu-id="af16d-138">120</span></span>   | <span data-ttu-id="af16d-139">240</span><span class="sxs-lookup"><span data-stu-id="af16d-139">240</span></span>   | <span data-ttu-id="af16d-140">500</span><span class="sxs-lookup"><span data-stu-id="af16d-140">500</span></span>   | <span data-ttu-id="af16d-141">2300</span><span class="sxs-lookup"><span data-stu-id="af16d-141">2300</span></span>              | <span data-ttu-id="af16d-142">5000</span><span class="sxs-lookup"><span data-stu-id="af16d-142">5000</span></span>              | <span data-ttu-id="af16d-143">7500</span><span class="sxs-lookup"><span data-stu-id="af16d-143">7500</span></span>              | <span data-ttu-id="af16d-144">7500</span><span class="sxs-lookup"><span data-stu-id="af16d-144">7500</span></span>              | 
| <span data-ttu-id="af16d-145">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="af16d-145">Throughput per disk</span></span> | <span data-ttu-id="af16d-146">每秒 25 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-146">25 MB per second</span></span>  | <span data-ttu-id="af16d-147">每秒 50 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-147">50 MB per second</span></span>  | <span data-ttu-id="af16d-148">每秒 100 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-148">100 MB per second</span></span> | <span data-ttu-id="af16d-149">每秒 150 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-149">150 MB per second</span></span> | <span data-ttu-id="af16d-150">每秒 200 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-150">200 MB per second</span></span> | <span data-ttu-id="af16d-151">每秒 250 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-151">250 MB per second</span></span> | <span data-ttu-id="af16d-152">每秒 250 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-152">250 MB per second</span></span> | 

<span data-ttu-id="af16d-153">**標準受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="af16d-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="af16d-154">有七種型別的標準受控磁碟可搭配 VM 使用。</span><span class="sxs-lookup"><span data-stu-id="af16d-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="af16d-155">每種類型的容量各不相同，但其 IOPS 和輸送量限制相同。</span><span class="sxs-lookup"><span data-stu-id="af16d-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="af16d-156">根據您應用程式的容量需求，選擇標準受控磁碟的類型。</span><span class="sxs-lookup"><span data-stu-id="af16d-156">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="af16d-157">標準磁碟類型</span><span class="sxs-lookup"><span data-stu-id="af16d-157">Standard Disk Type</span></span>  | <span data-ttu-id="af16d-158">S4</span><span class="sxs-lookup"><span data-stu-id="af16d-158">S4</span></span>               | <span data-ttu-id="af16d-159">S6</span><span class="sxs-lookup"><span data-stu-id="af16d-159">S6</span></span>               | <span data-ttu-id="af16d-160">S10</span><span class="sxs-lookup"><span data-stu-id="af16d-160">S10</span></span>              | <span data-ttu-id="af16d-161">S20</span><span class="sxs-lookup"><span data-stu-id="af16d-161">S20</span></span>              | <span data-ttu-id="af16d-162">S30</span><span class="sxs-lookup"><span data-stu-id="af16d-162">S30</span></span>              | <span data-ttu-id="af16d-163">S40</span><span class="sxs-lookup"><span data-stu-id="af16d-163">S40</span></span>              | <span data-ttu-id="af16d-164">S50</span><span class="sxs-lookup"><span data-stu-id="af16d-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="af16d-165">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="af16d-165">Disk size</span></span>           | <span data-ttu-id="af16d-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="af16d-166">30 GB</span></span>            | <span data-ttu-id="af16d-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="af16d-167">64 GB</span></span>            | <span data-ttu-id="af16d-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="af16d-168">128 GB</span></span>           | <span data-ttu-id="af16d-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="af16d-169">512 GB</span></span>           | <span data-ttu-id="af16d-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="af16d-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="af16d-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="af16d-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="af16d-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="af16d-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="af16d-173">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="af16d-173">IOPS per disk</span></span>       | <span data-ttu-id="af16d-174">500</span><span class="sxs-lookup"><span data-stu-id="af16d-174">500</span></span>              | <span data-ttu-id="af16d-175">500</span><span class="sxs-lookup"><span data-stu-id="af16d-175">500</span></span>              | <span data-ttu-id="af16d-176">500</span><span class="sxs-lookup"><span data-stu-id="af16d-176">500</span></span>              | <span data-ttu-id="af16d-177">500</span><span class="sxs-lookup"><span data-stu-id="af16d-177">500</span></span>              | <span data-ttu-id="af16d-178">500</span><span class="sxs-lookup"><span data-stu-id="af16d-178">500</span></span>              | <span data-ttu-id="af16d-179">500</span><span class="sxs-lookup"><span data-stu-id="af16d-179">500</span></span>             | <span data-ttu-id="af16d-180">500</span><span class="sxs-lookup"><span data-stu-id="af16d-180">500</span></span>              | 
| <span data-ttu-id="af16d-181">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="af16d-181">Throughput per disk</span></span> | <span data-ttu-id="af16d-182">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-182">60 MB per second</span></span> | <span data-ttu-id="af16d-183">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-183">60 MB per second</span></span> | <span data-ttu-id="af16d-184">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-184">60 MB per second</span></span> | <span data-ttu-id="af16d-185">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-185">60 MB per second</span></span> | <span data-ttu-id="af16d-186">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-186">60 MB per second</span></span> | <span data-ttu-id="af16d-187">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-187">60 MB per second</span></span> | <span data-ttu-id="af16d-188">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="af16d-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="af16d-189">磁碟快取原則</span><span class="sxs-lookup"><span data-stu-id="af16d-189">Disk caching policy</span></span> 

<span data-ttu-id="af16d-190">**進階受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="af16d-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="af16d-191">根據預設，所有 Premium 資料磁碟的磁碟快取原則都是*唯讀*，而連接至 VM 的 Premium 作業系統磁碟的磁碟快取原則則是*讀寫*。</span><span class="sxs-lookup"><span data-stu-id="af16d-191">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="af16d-192">為使應用程式的 IO 達到最佳效能，建議使用此組態設定。</span><span class="sxs-lookup"><span data-stu-id="af16d-192">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="af16d-193">對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="af16d-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="af16d-194">價格</span><span class="sxs-lookup"><span data-stu-id="af16d-194">Pricing</span></span>

<span data-ttu-id="af16d-195">請檢閱[受控磁碟的價格](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)。</span><span class="sxs-lookup"><span data-stu-id="af16d-195">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="af16d-196">進階受控磁碟與進階非受控磁碟的價格相同。</span><span class="sxs-lookup"><span data-stu-id="af16d-196">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="af16d-197">但標準受控磁碟與標準非受控磁碟的價格不同。</span><span class="sxs-lookup"><span data-stu-id="af16d-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="af16d-198">檢查清單</span><span class="sxs-lookup"><span data-stu-id="af16d-198">Checklist</span></span>

1.  <span data-ttu-id="af16d-199">如果您要移轉至進階受控磁碟，請確定它可在您要移轉到的區域中使用。</span><span class="sxs-lookup"><span data-stu-id="af16d-199">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span></span>

2.  <span data-ttu-id="af16d-200">決定您將要使用的新 VM 系列。</span><span class="sxs-lookup"><span data-stu-id="af16d-200">Decide the new VM series you will be using.</span></span> <span data-ttu-id="af16d-201">如果您要移轉至進階受控磁碟，它應可支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="af16d-201">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span></span>

3.  <span data-ttu-id="af16d-202">決定在您要移轉至的區域中可用的確切 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="af16d-202">Decide the exact VM size you will use which are available in the region you are migrating to.</span></span> <span data-ttu-id="af16d-203">VM 大小必須足以支援您所擁有的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="af16d-203">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="af16d-204">例如，如果您有 4 個資料磁碟，VM 必須有 2 個或更多核心。</span><span class="sxs-lookup"><span data-stu-id="af16d-204">For example, if you have four data disks, the VM must have two or more cores.</span></span> <span data-ttu-id="af16d-205">也請考慮處理能力、記憶體和網路頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="af16d-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="af16d-206">請備妥目前 VM 的詳細資料，包括磁碟和對應 VHD Blob 的清單。</span><span class="sxs-lookup"><span data-stu-id="af16d-206">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="af16d-207">為您的應用程式做好停機準備。</span><span class="sxs-lookup"><span data-stu-id="af16d-207">Prepare your application for downtime.</span></span> <span data-ttu-id="af16d-208">若要進行全新移轉，您必須停止目前系統中的所有處理。</span><span class="sxs-lookup"><span data-stu-id="af16d-208">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="af16d-209">只有這樣，您才可以使其維持在可移轉至新平台的一致狀態。</span><span class="sxs-lookup"><span data-stu-id="af16d-209">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="af16d-210">停機持續時間取決於磁碟中要移轉的資料量。</span><span class="sxs-lookup"><span data-stu-id="af16d-210">Downtime duration depends on the amount of data in the disks to migrate.</span></span>


## <a name="migrate-the-vm"></a><span data-ttu-id="af16d-211">移轉 VM</span><span class="sxs-lookup"><span data-stu-id="af16d-211">Migrate the VM</span></span>

<span data-ttu-id="af16d-212">為您的應用程式做好停機準備。</span><span class="sxs-lookup"><span data-stu-id="af16d-212">Prepare your application for downtime.</span></span> <span data-ttu-id="af16d-213">若要進行全新移轉，您必須停止目前系統中的所有處理。</span><span class="sxs-lookup"><span data-stu-id="af16d-213">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="af16d-214">只有這樣，您才可以使其維持在可移轉至新平台的一致狀態。</span><span class="sxs-lookup"><span data-stu-id="af16d-214">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="af16d-215">停機持續時間取決於磁碟中要移轉的資料量。</span><span class="sxs-lookup"><span data-stu-id="af16d-215">Downtime duration depends the amount of data in the disks to migrate.</span></span>


1.  <span data-ttu-id="af16d-216">首先，設定一般參數：</span><span class="sxs-lookup"><span data-stu-id="af16d-216">First, set the common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="af16d-217">使用傳統 VM 中的 VHD 建立受控 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="af16d-217">Create a managed OS disk using the VHD from the classic VM.</span></span>

    <span data-ttu-id="af16d-218">請確定您已將 OS VHD 的完整 URI 提供給 $osVhdUri 參數。</span><span class="sxs-lookup"><span data-stu-id="af16d-218">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span></span> <span data-ttu-id="af16d-219">此外，根據您要移轉至的磁碟類型 (進階或標準)，將 **-AccountType** 輸入為 **PremiumLRS** 或 **StandardLRS**。</span><span class="sxs-lookup"><span data-stu-id="af16d-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="af16d-220">將 OS 磁碟附加至新的 VM。</span><span class="sxs-lookup"><span data-stu-id="af16d-220">Attach the OS disk to the new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="af16d-221">從資料 VHD 檔案建立受控資料磁碟，並將它新增到新的 VM。</span><span class="sxs-lookup"><span data-stu-id="af16d-221">Create a managed data disk from the data VHD file and add it to the new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="af16d-222">藉由設定公用 IP、虛擬網路和 NIC，建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="af16d-222">Create the new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="af16d-223">可能有一些支援應用程式所需的其他步驟不包含在本指南中。</span><span class="sxs-lookup"><span data-stu-id="af16d-223">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="af16d-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af16d-224">Next steps</span></span>

- <span data-ttu-id="af16d-225">連接至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="af16d-225">Connect to the virtual machine.</span></span> <span data-ttu-id="af16d-226">如需指示，請參閱 [如何連接和登入執行 Windows 的 Azure 虛擬機器](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="af16d-226">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

