---
title: "aaaMigrate 傳統 VM tooan ARM 管理磁碟 VM |Microsoft 文件"
description: "移轉單一 Azure VM 從 hello 傳統部署模型 tooManaged hello Resource Manager 部署模型中的磁碟。"
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
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="24582-103">手動將移轉傳統 VM tooa 中的新 ARM 管理磁碟 VM hello VHD</span><span class="sxs-lookup"><span data-stu-id="24582-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="24582-104">本節可協助您 toomigrate 現有的 Azure Vm 從 hello 傳統部署模型太[管理磁碟](managed-disks-overview.md)hello Resource Manager 部署模型中。</span><span class="sxs-lookup"><span data-stu-id="24582-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="24582-105">規劃移轉 hello tooManaged 磁碟</span><span class="sxs-lookup"><span data-stu-id="24582-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="24582-106">本節可協助您 toomake hello 最佳決定 VM 和磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="24582-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="24582-107">位置</span><span class="sxs-lookup"><span data-stu-id="24582-107">Location</span></span>

<span data-ttu-id="24582-108">挑選 Azure 受控磁碟可用的位置。</span><span class="sxs-lookup"><span data-stu-id="24582-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="24582-109">如果您正在移轉 tooPremium 管理磁碟，也請確定高階儲存體可用規劃至 toomigrate hello 區域中。</span><span class="sxs-lookup"><span data-stu-id="24582-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="24582-110">如需可用位置的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。</span><span class="sxs-lookup"><span data-stu-id="24582-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="24582-111">VM 大小</span><span class="sxs-lookup"><span data-stu-id="24582-111">VM sizes</span></span>

<span data-ttu-id="24582-112">如果您要移轉 tooPremium 管理磁碟，您會有 hello VM 所在的區域中的 hello VM tooPremium 可用儲存體能夠大小 tooupdate hello 大小。</span><span class="sxs-lookup"><span data-stu-id="24582-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="24582-113">檢閱可支援進階儲存體 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="24582-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="24582-114">hello Azure VM 大小規格中所列[虛擬機器的大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="24582-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="24582-115">檢閱 hello 使用進階儲存體和選擇 hello 最適當的 VM 大小最適合您的工作負載的虛擬機器的效能特性。</span><span class="sxs-lookup"><span data-stu-id="24582-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="24582-116">請確定有足夠的頻寬可用的 VM toodrive hello 磁碟流量。</span><span class="sxs-lookup"><span data-stu-id="24582-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="24582-117">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="24582-117">Disk sizes</span></span>

<span data-ttu-id="24582-118">**進階受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="24582-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="24582-119">有七種型別的進階受控磁碟可以搭配 VM 使用，而且每種都有特定的 IOP 和輸送量限制。</span><span class="sxs-lookup"><span data-stu-id="24582-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="24582-120">當您選擇 hello VM 的高階磁碟類型根據 hello 產能、 效能、 延展性方面的應用程式需求和尖峰負載時，請考慮這些限制。</span><span class="sxs-lookup"><span data-stu-id="24582-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="24582-121">進階磁碟類型</span><span class="sxs-lookup"><span data-stu-id="24582-121">Premium Disks Type</span></span>  | <span data-ttu-id="24582-122">P4</span><span class="sxs-lookup"><span data-stu-id="24582-122">P4</span></span>    | <span data-ttu-id="24582-123">P6</span><span class="sxs-lookup"><span data-stu-id="24582-123">P6</span></span>    | <span data-ttu-id="24582-124">P10</span><span class="sxs-lookup"><span data-stu-id="24582-124">P10</span></span>   | <span data-ttu-id="24582-125">P20</span><span class="sxs-lookup"><span data-stu-id="24582-125">P20</span></span>   | <span data-ttu-id="24582-126">P30</span><span class="sxs-lookup"><span data-stu-id="24582-126">P30</span></span>   | <span data-ttu-id="24582-127">P40</span><span class="sxs-lookup"><span data-stu-id="24582-127">P40</span></span>   | <span data-ttu-id="24582-128">P50</span><span class="sxs-lookup"><span data-stu-id="24582-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="24582-129">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="24582-129">Disk size</span></span>           | <span data-ttu-id="24582-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="24582-130">128 GB</span></span>| <span data-ttu-id="24582-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="24582-131">512 GB</span></span>| <span data-ttu-id="24582-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="24582-132">128 GB</span></span>| <span data-ttu-id="24582-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="24582-133">512 GB</span></span>            | <span data-ttu-id="24582-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="24582-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="24582-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="24582-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="24582-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="24582-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="24582-137">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="24582-137">IOPS per disk</span></span>       | <span data-ttu-id="24582-138">120</span><span class="sxs-lookup"><span data-stu-id="24582-138">120</span></span>   | <span data-ttu-id="24582-139">240</span><span class="sxs-lookup"><span data-stu-id="24582-139">240</span></span>   | <span data-ttu-id="24582-140">500</span><span class="sxs-lookup"><span data-stu-id="24582-140">500</span></span>   | <span data-ttu-id="24582-141">2300</span><span class="sxs-lookup"><span data-stu-id="24582-141">2300</span></span>              | <span data-ttu-id="24582-142">5000</span><span class="sxs-lookup"><span data-stu-id="24582-142">5000</span></span>              | <span data-ttu-id="24582-143">7500</span><span class="sxs-lookup"><span data-stu-id="24582-143">7500</span></span>              | <span data-ttu-id="24582-144">7500</span><span class="sxs-lookup"><span data-stu-id="24582-144">7500</span></span>              | 
| <span data-ttu-id="24582-145">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="24582-145">Throughput per disk</span></span> | <span data-ttu-id="24582-146">每秒 25 MB</span><span class="sxs-lookup"><span data-stu-id="24582-146">25 MB per second</span></span>  | <span data-ttu-id="24582-147">每秒 50 MB</span><span class="sxs-lookup"><span data-stu-id="24582-147">50 MB per second</span></span>  | <span data-ttu-id="24582-148">每秒 100 MB</span><span class="sxs-lookup"><span data-stu-id="24582-148">100 MB per second</span></span> | <span data-ttu-id="24582-149">每秒 150 MB</span><span class="sxs-lookup"><span data-stu-id="24582-149">150 MB per second</span></span> | <span data-ttu-id="24582-150">每秒 200 MB</span><span class="sxs-lookup"><span data-stu-id="24582-150">200 MB per second</span></span> | <span data-ttu-id="24582-151">每秒 250 MB</span><span class="sxs-lookup"><span data-stu-id="24582-151">250 MB per second</span></span> | <span data-ttu-id="24582-152">每秒 250 MB</span><span class="sxs-lookup"><span data-stu-id="24582-152">250 MB per second</span></span> | 

<span data-ttu-id="24582-153">**標準受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="24582-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="24582-154">有七種型別的標準受控磁碟可搭配 VM 使用。</span><span class="sxs-lookup"><span data-stu-id="24582-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="24582-155">每種類型的容量各不相同，但其 IOPS 和輸送量限制相同。</span><span class="sxs-lookup"><span data-stu-id="24582-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="24582-156">選擇 hello 根據 hello 容量需求的應用程式的標準管理磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="24582-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="24582-157">標準磁碟類型</span><span class="sxs-lookup"><span data-stu-id="24582-157">Standard Disk Type</span></span>  | <span data-ttu-id="24582-158">S4</span><span class="sxs-lookup"><span data-stu-id="24582-158">S4</span></span>               | <span data-ttu-id="24582-159">S6</span><span class="sxs-lookup"><span data-stu-id="24582-159">S6</span></span>               | <span data-ttu-id="24582-160">S10</span><span class="sxs-lookup"><span data-stu-id="24582-160">S10</span></span>              | <span data-ttu-id="24582-161">S20</span><span class="sxs-lookup"><span data-stu-id="24582-161">S20</span></span>              | <span data-ttu-id="24582-162">S30</span><span class="sxs-lookup"><span data-stu-id="24582-162">S30</span></span>              | <span data-ttu-id="24582-163">S40</span><span class="sxs-lookup"><span data-stu-id="24582-163">S40</span></span>              | <span data-ttu-id="24582-164">S50</span><span class="sxs-lookup"><span data-stu-id="24582-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="24582-165">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="24582-165">Disk size</span></span>           | <span data-ttu-id="24582-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="24582-166">30 GB</span></span>            | <span data-ttu-id="24582-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="24582-167">64 GB</span></span>            | <span data-ttu-id="24582-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="24582-168">128 GB</span></span>           | <span data-ttu-id="24582-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="24582-169">512 GB</span></span>           | <span data-ttu-id="24582-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="24582-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="24582-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="24582-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="24582-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="24582-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="24582-173">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="24582-173">IOPS per disk</span></span>       | <span data-ttu-id="24582-174">500</span><span class="sxs-lookup"><span data-stu-id="24582-174">500</span></span>              | <span data-ttu-id="24582-175">500</span><span class="sxs-lookup"><span data-stu-id="24582-175">500</span></span>              | <span data-ttu-id="24582-176">500</span><span class="sxs-lookup"><span data-stu-id="24582-176">500</span></span>              | <span data-ttu-id="24582-177">500</span><span class="sxs-lookup"><span data-stu-id="24582-177">500</span></span>              | <span data-ttu-id="24582-178">500</span><span class="sxs-lookup"><span data-stu-id="24582-178">500</span></span>              | <span data-ttu-id="24582-179">500</span><span class="sxs-lookup"><span data-stu-id="24582-179">500</span></span>             | <span data-ttu-id="24582-180">500</span><span class="sxs-lookup"><span data-stu-id="24582-180">500</span></span>              | 
| <span data-ttu-id="24582-181">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="24582-181">Throughput per disk</span></span> | <span data-ttu-id="24582-182">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="24582-182">60 MB per second</span></span> | <span data-ttu-id="24582-183">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="24582-183">60 MB per second</span></span> | <span data-ttu-id="24582-184">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="24582-184">60 MB per second</span></span> | <span data-ttu-id="24582-185">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="24582-185">60 MB per second</span></span> | <span data-ttu-id="24582-186">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="24582-186">60 MB per second</span></span> | <span data-ttu-id="24582-187">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="24582-187">60 MB per second</span></span> | <span data-ttu-id="24582-188">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="24582-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="24582-189">磁碟快取原則</span><span class="sxs-lookup"><span data-stu-id="24582-189">Disk caching policy</span></span> 

<span data-ttu-id="24582-190">**進階受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="24582-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="24582-191">根據預設，快取原則的磁碟是*唯讀*針對所有 hello 高階資料磁碟，和*讀寫*hello Premium 作業系統磁碟附加 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="24582-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="24582-192">此組態設定，建議您使用 IOs 應用程式的 tooachieve hello 達到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="24582-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="24582-193">對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="24582-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="24582-194">價格</span><span class="sxs-lookup"><span data-stu-id="24582-194">Pricing</span></span>

<span data-ttu-id="24582-195">檢閱 hello[定價管理磁碟](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)。</span><span class="sxs-lookup"><span data-stu-id="24582-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="24582-196">定價的高階管理磁碟是與 hello 高階 Unmanaged 磁碟相同。</span><span class="sxs-lookup"><span data-stu-id="24582-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="24582-197">但標準受控磁碟與標準非受控磁碟的價格不同。</span><span class="sxs-lookup"><span data-stu-id="24582-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="24582-198">檢查清單</span><span class="sxs-lookup"><span data-stu-id="24582-198">Checklist</span></span>

1.  <span data-ttu-id="24582-199">如果您要移轉 tooPremium 管理磁碟，請確定它可以使用您要移轉至 hello 區域中。</span><span class="sxs-lookup"><span data-stu-id="24582-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="24582-200">決定 hello 您要將新 VM 系列。</span><span class="sxs-lookup"><span data-stu-id="24582-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="24582-201">如果您要移轉 tooPremium 管理磁碟，它應該是支援高階儲存體。</span><span class="sxs-lookup"><span data-stu-id="24582-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="24582-202">決定 hello 確切 VM 大小將會使用您要移轉至 hello 區域中可用的。</span><span class="sxs-lookup"><span data-stu-id="24582-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="24582-203">VM 大小需要 toobe 夠大 toosupport hello 您擁有的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="24582-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="24582-204">例如，如果您有四個資料磁碟，hello VM 必須有兩個或多個核心。</span><span class="sxs-lookup"><span data-stu-id="24582-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="24582-205">也請考慮處理能力、記憶體和網路頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="24582-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="24582-206">有 hello 目前 VM 詳細資料很方便，包括 hello 磁碟清單及其對應的 VHD blob。</span><span class="sxs-lookup"><span data-stu-id="24582-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="24582-207">為您的應用程式做好停機準備。</span><span class="sxs-lookup"><span data-stu-id="24582-207">Prepare your application for downtime.</span></span> <span data-ttu-id="24582-208">toodo 全新的移轉，您必須 toostop 所有 hello 處理 hello 目前系統中。</span><span class="sxs-lookup"><span data-stu-id="24582-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="24582-209">唯有如此，您可以取得它 tooconsistent 狀態，您可以移轉 toohello 新的平台。</span><span class="sxs-lookup"><span data-stu-id="24582-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="24582-210">停機持續時間取決於 hello hello 磁碟 toomigrate 中的資料數量。</span><span class="sxs-lookup"><span data-stu-id="24582-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="24582-211">移轉 hello VM</span><span class="sxs-lookup"><span data-stu-id="24582-211">Migrate hello VM</span></span>

<span data-ttu-id="24582-212">為您的應用程式做好停機準備。</span><span class="sxs-lookup"><span data-stu-id="24582-212">Prepare your application for downtime.</span></span> <span data-ttu-id="24582-213">toodo 全新的移轉，您必須 toostop 所有 hello 處理 hello 目前系統中。</span><span class="sxs-lookup"><span data-stu-id="24582-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="24582-214">唯有如此，您可以取得它 tooconsistent 狀態，您可以移轉 toohello 新的平台。</span><span class="sxs-lookup"><span data-stu-id="24582-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="24582-215">停機持續時間取決於 hello hello 磁碟 toomigrate 中的資料數量。</span><span class="sxs-lookup"><span data-stu-id="24582-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="24582-216">首先，設定 hello 一般參數：</span><span class="sxs-lookup"><span data-stu-id="24582-216">First, set hello common parameters:</span></span>

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

2.  <span data-ttu-id="24582-217">建立受管理的作業系統磁碟使用 hello VHD 從 hello 傳統 VM。</span><span class="sxs-lookup"><span data-stu-id="24582-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="24582-218">請確定您已提供 hello 完成 hello OS VHD toohello $osVhdUri 參數的 URI。</span><span class="sxs-lookup"><span data-stu-id="24582-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="24582-219">此外，根據您要移轉至的磁碟類型 (進階或標準)，將 **-AccountType** 輸入為 **PremiumLRS** 或 **StandardLRS**。</span><span class="sxs-lookup"><span data-stu-id="24582-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="24582-220">附加 hello OS 磁碟 toohello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="24582-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="24582-221">從 hello 資料 VHD 檔案建立受管理的資料磁碟，並將它新增 toohello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="24582-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="24582-222">建立新的 VM hello 藉由設定公用 IP、 虛擬網路和 NIC</span><span class="sxs-lookup"><span data-stu-id="24582-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

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
><span data-ttu-id="24582-223">可能有額外的步驟需要 toosupport 的應用程式不會涵蓋本指南。</span><span class="sxs-lookup"><span data-stu-id="24582-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="24582-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="24582-224">Next steps</span></span>

- <span data-ttu-id="24582-225">Toohello 虛擬機器連線。</span><span class="sxs-lookup"><span data-stu-id="24582-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="24582-226">如需指示，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="24582-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

