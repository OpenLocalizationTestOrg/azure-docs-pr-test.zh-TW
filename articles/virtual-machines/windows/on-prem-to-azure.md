---
title: "從 AWS 和其他平台移轉至 Azure 中的受控磁碟 | Microsoft Docs"
description: "在 Azure 中使用從其他雲端 (如 AWS) 或其他虛擬化平台上傳的 VHD 建立 VM，並充分利用 Azure 受控磁碟。"
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
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 685c35dbd4265ca6852de6db2e5a30fc2a611d7c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-to-managed-disks-in-azure"></a><span data-ttu-id="68444-103">從 Amazon Web Services (AWS) 和其他平台移轉至 Azure 中的受控磁碟</span><span class="sxs-lookup"><span data-stu-id="68444-103">Migrate from Amazon Web Services (AWS) and other platforms to Managed Disks in Azure</span></span>

<span data-ttu-id="68444-104">您可以將 VHD 檔案從 AWS 或內部部署虛擬化解決方案上傳至 Azure，以建立利用受控磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="68444-104">You can upload VHD files from AWS or on-premises virtualization solutions to Azure to create VMs that take advantage of Managed Disks.</span></span> <span data-ttu-id="68444-105">使用 Azure 受控磁碟就不需要為 Azure IaaS VM 管理儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="68444-105">Azure Managed Disks removes the need of to managing storage accounts for Azure IaaS VMs.</span></span> <span data-ttu-id="68444-106">您只需要指定類型 (進階或標準)，還有您需要的磁碟大小，Azure 就會替您建立及管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="68444-106">You have to only specify the type (Premium or Standard) and size of disk you need, and Azure will create and manage the disk for you.</span></span> 

<span data-ttu-id="68444-107">您可以上傳一般化和特製化 VHD。</span><span class="sxs-lookup"><span data-stu-id="68444-107">You can upload either generalized and specialized VHDs.</span></span> 
- <span data-ttu-id="68444-108">**一般化 VHD** - 已使用 Sysprep 將您所有的個人帳戶資訊移除。</span><span class="sxs-lookup"><span data-stu-id="68444-108">**Generalized VHD** - has had all of your personal account information removed using Sysprep.</span></span> 
- <span data-ttu-id="68444-109">**特製化 VHD** - 會從原始的 VM 維護使用者帳戶、應用程式和其他狀態資料。</span><span class="sxs-lookup"><span data-stu-id="68444-109">**Specialized VHD** - maintains the user accounts, applications and other state data from your original VM.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="68444-110">將任何 VHD 上傳至 Azure 之前，您應該遵循[準備 Windows VHD 或 VHDX 以上傳至 Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="68444-110">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
>
>


| <span data-ttu-id="68444-111">案例</span><span class="sxs-lookup"><span data-stu-id="68444-111">Scenario</span></span>                                                                                                                         | <span data-ttu-id="68444-112">文件</span><span class="sxs-lookup"><span data-stu-id="68444-112">Documentation</span></span>                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="68444-113">您可能想要將現有的 AWS EC2 執行個體移轉至 Azure 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="68444-113">You have an existing AWS EC2 instances that you could like to migrate to Azure Managed Disks</span></span>                                     | [<span data-ttu-id="68444-114">從 Amazon Web Services (AWS) 將 VM 移至 Azure</span><span class="sxs-lookup"><span data-stu-id="68444-114">Move a VM from Amazon Web Services (AWS) to Azure</span></span>](aws-to-azure.md)                           |
| <span data-ttu-id="68444-115">您想要將來自 AWS 和其他虛擬化平台的 VM 做為映像來建立多個 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="68444-115">You have a VM from and other virtualization platform that you would like to use to use as an image to create multiple Azure VMs.</span></span> | [<span data-ttu-id="68444-116">將一般化 VHD 上傳，並使用它在 Azure 中建立新的 VM</span><span class="sxs-lookup"><span data-stu-id="68444-116">Upload a generalized VHD and use it to create a new VMs in Azure</span></span>](upload-generalized-managed.md) |
| <span data-ttu-id="68444-117">您想要在 Azure 中重新建立唯一自訂的 VM。</span><span class="sxs-lookup"><span data-stu-id="68444-117">You have a uniquely customized VM that you would like to recreate in Azure.</span></span>                                                      | [<span data-ttu-id="68444-118">將特製化 VHD 上傳至 Azure，並建立新的 VM</span><span class="sxs-lookup"><span data-stu-id="68444-118">Upload a specialized VHD to Azure and create a new VM</span></span>](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a><span data-ttu-id="68444-119">受控磁碟概觀</span><span class="sxs-lookup"><span data-stu-id="68444-119">Overview of Managed Disks</span></span>

<span data-ttu-id="68444-120">Azure 受控磁碟可免除管理儲存體帳戶的需求，進而簡化 VM 管理。</span><span class="sxs-lookup"><span data-stu-id="68444-120">Azure Managed Disks simplifies VM management by removing the need to manage storage accounts.</span></span> <span data-ttu-id="68444-121">受控磁碟也受惠於可用性設定組中更佳的 VM 可靠性。</span><span class="sxs-lookup"><span data-stu-id="68444-121">Managed Disks also benefit from better reliability of VMs in an Availability Set.</span></span> <span data-ttu-id="68444-122">它可確保可用性設定組中不同 VM 的磁碟完全彼此隔離，以避免單一失敗點。</span><span class="sxs-lookup"><span data-stu-id="68444-122">It ensures that the disks of different VMs in an Availability Set will be sufficiently isolated from each other to avoid single point of failures.</span></span> <span data-ttu-id="68444-123">它會自動以不同的儲存體縮放單位 (戳記) 將不同 VM 的磁碟放在一個可用性設定組中，以限制硬體和軟體失敗所引起之單一儲存體縮放單位失敗的影響。</span><span class="sxs-lookup"><span data-stu-id="68444-123">It automatically places disks of different VMs in an Availability Set in different Storage scale units (stamps) which limits the impact of single Storage scale unit failures caused due to hardware and software failures.</span></span> <span data-ttu-id="68444-124">根據您的需求，您可選擇兩種類型的儲存體選項︰</span><span class="sxs-lookup"><span data-stu-id="68444-124">Based on your needs, you can choose from two types of storage options:</span></span> 
 
- <span data-ttu-id="68444-125">[進階受控磁碟](../../storage/common/storage-premium-storage.md)是固態硬碟 (SSD) 式儲存媒體，可針對執行大量 I/O 工作負載的虛擬機器，提供高效能、低延遲的磁碟支援。</span><span class="sxs-lookup"><span data-stu-id="68444-125">[Premium Managed Disks](../../storage/common/storage-premium-storage.md) are Solid State Drive (SSD) based storage storage media which delivers highperformance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="68444-126">您可以將這類磁碟移轉至進階受控磁碟，以利用這類磁碟的速度和效能。</span><span class="sxs-lookup"><span data-stu-id="68444-126">You can take advantage of the speed and performance of these disks by migrating to Premium Managed Disks.</span></span>  

- <span data-ttu-id="68444-127">[標準受控磁碟](../../storage/common/storage-standard-storage.md)使用固態硬碟 (SSD) 式儲存媒體，最適合用於開發/測試及其他較不容易受效能變異影響的不常用工作負載。</span><span class="sxs-lookup"><span data-stu-id="68444-127">[Standard Managed Disks](../../storage/common/storage-standard-storage.md) use Hard Disk Drive (HDD) based storage media and are best suited for Dev/Test and other infrequent access workloads that are less sensitive to performance variability.</span></span>  

## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="68444-128">規劃移轉至受控磁碟</span><span class="sxs-lookup"><span data-stu-id="68444-128">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="68444-129">本節可協助您做出最佳的 VM 和磁碟類型決策。</span><span class="sxs-lookup"><span data-stu-id="68444-129">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="68444-130">位置</span><span class="sxs-lookup"><span data-stu-id="68444-130">Location</span></span>

<span data-ttu-id="68444-131">挑選 Azure 受控磁碟可用的位置。</span><span class="sxs-lookup"><span data-stu-id="68444-131">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="68444-132">如果您要移轉至進階受控磁碟，也請確保進階儲存體可用於您打算移轉至的區域。</span><span class="sxs-lookup"><span data-stu-id="68444-132">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="68444-133">如需可使用 Azure 服務之地點的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。</span><span class="sxs-lookup"><span data-stu-id="68444-133">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="68444-134">VM 大小</span><span class="sxs-lookup"><span data-stu-id="68444-134">VM sizes</span></span>

<span data-ttu-id="68444-135">如果您要移轉至進階受控磁碟，您必須將 VM 大小更新為 VM 所在區域中進階儲存體可支援的大小。</span><span class="sxs-lookup"><span data-stu-id="68444-135">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="68444-136">檢閱進階儲存體可支援的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="68444-136">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="68444-137">Azure VM 大小的規格已列在 [虛擬機器的大小](sizes.md)一文中。</span><span class="sxs-lookup"><span data-stu-id="68444-137">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="68444-138">請檢閱使用於進階儲存體的虛擬機器效能特性，然後選擇最適合您的工作負載的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="68444-138">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="68444-139">確定 VM 上有足夠的磁碟流量頻寬。</span><span class="sxs-lookup"><span data-stu-id="68444-139">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="68444-140">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="68444-140">Disk sizes</span></span>

<span data-ttu-id="68444-141">**進階受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="68444-141">**Premium Managed Disks**</span></span>

<span data-ttu-id="68444-142">有三種類型的進階受控磁碟可以搭配您的 VM 使用，而且每種都有特定的 IOP 和輸送量限制。</span><span class="sxs-lookup"><span data-stu-id="68444-142">There are three types of Premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="68444-143">為您的 VM 選擇進階磁碟類型時，請根據應用程式在容量、效能、延展性以及尖峰負載方面的需求，將這些限制納入考量。</span><span class="sxs-lookup"><span data-stu-id="68444-143">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="68444-144">進階磁碟類型</span><span class="sxs-lookup"><span data-stu-id="68444-144">Premium Disks Type</span></span>  | <span data-ttu-id="68444-145">P10</span><span class="sxs-lookup"><span data-stu-id="68444-145">P10</span></span>               | <span data-ttu-id="68444-146">P20</span><span class="sxs-lookup"><span data-stu-id="68444-146">P20</span></span>               | <span data-ttu-id="68444-147">P30</span><span class="sxs-lookup"><span data-stu-id="68444-147">P30</span></span>               |
|---------------------|-------------------|-------------------|-------------------|
| <span data-ttu-id="68444-148">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="68444-148">Disk size</span></span>           | <span data-ttu-id="68444-149">128 GB</span><span class="sxs-lookup"><span data-stu-id="68444-149">128 GB</span></span>            | <span data-ttu-id="68444-150">512 GB</span><span class="sxs-lookup"><span data-stu-id="68444-150">512 GB</span></span>            | <span data-ttu-id="68444-151">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="68444-151">1024 GB (1 TB)</span></span>    |
| <span data-ttu-id="68444-152">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="68444-152">IOPS per disk</span></span>       | <span data-ttu-id="68444-153">500</span><span class="sxs-lookup"><span data-stu-id="68444-153">500</span></span>               | <span data-ttu-id="68444-154">2300</span><span class="sxs-lookup"><span data-stu-id="68444-154">2300</span></span>              | <span data-ttu-id="68444-155">5000</span><span class="sxs-lookup"><span data-stu-id="68444-155">5000</span></span>              |
| <span data-ttu-id="68444-156">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="68444-156">Throughput per disk</span></span> | <span data-ttu-id="68444-157">每秒 100 MB</span><span class="sxs-lookup"><span data-stu-id="68444-157">100 MB per second</span></span> | <span data-ttu-id="68444-158">每秒 150 MB</span><span class="sxs-lookup"><span data-stu-id="68444-158">150 MB per second</span></span> | <span data-ttu-id="68444-159">每秒 200 MB</span><span class="sxs-lookup"><span data-stu-id="68444-159">200 MB per second</span></span> |

<span data-ttu-id="68444-160">**標準受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="68444-160">**Standard Managed Disks**</span></span>

<span data-ttu-id="68444-161">有五種類型的標準受控磁碟可搭配您的 VM 使用。</span><span class="sxs-lookup"><span data-stu-id="68444-161">There are five types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="68444-162">每種類型的容量各不相同，但其 IOPS 和輸送量限制相同。</span><span class="sxs-lookup"><span data-stu-id="68444-162">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="68444-163">根據您應用程式的容量需求，選擇標準受控磁碟的類型。</span><span class="sxs-lookup"><span data-stu-id="68444-163">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="68444-164">標準磁碟類型</span><span class="sxs-lookup"><span data-stu-id="68444-164">Standard Disk Type</span></span>  | <span data-ttu-id="68444-165">S4</span><span class="sxs-lookup"><span data-stu-id="68444-165">S4</span></span>               | <span data-ttu-id="68444-166">S6</span><span class="sxs-lookup"><span data-stu-id="68444-166">S6</span></span>               | <span data-ttu-id="68444-167">S10</span><span class="sxs-lookup"><span data-stu-id="68444-167">S10</span></span>              | <span data-ttu-id="68444-168">S20</span><span class="sxs-lookup"><span data-stu-id="68444-168">S20</span></span>              | <span data-ttu-id="68444-169">S30</span><span class="sxs-lookup"><span data-stu-id="68444-169">S30</span></span>              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| <span data-ttu-id="68444-170">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="68444-170">Disk size</span></span>           | <span data-ttu-id="68444-171">30 GB</span><span class="sxs-lookup"><span data-stu-id="68444-171">30 GB</span></span>            | <span data-ttu-id="68444-172">64 GB</span><span class="sxs-lookup"><span data-stu-id="68444-172">64 GB</span></span>            | <span data-ttu-id="68444-173">128 GB</span><span class="sxs-lookup"><span data-stu-id="68444-173">128 GB</span></span>           | <span data-ttu-id="68444-174">512 GB</span><span class="sxs-lookup"><span data-stu-id="68444-174">512 GB</span></span>           | <span data-ttu-id="68444-175">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="68444-175">1024 GB (1 TB)</span></span>   |
| <span data-ttu-id="68444-176">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="68444-176">IOPS per disk</span></span>       | <span data-ttu-id="68444-177">500</span><span class="sxs-lookup"><span data-stu-id="68444-177">500</span></span>              | <span data-ttu-id="68444-178">500</span><span class="sxs-lookup"><span data-stu-id="68444-178">500</span></span>              | <span data-ttu-id="68444-179">500</span><span class="sxs-lookup"><span data-stu-id="68444-179">500</span></span>              | <span data-ttu-id="68444-180">500</span><span class="sxs-lookup"><span data-stu-id="68444-180">500</span></span>              | <span data-ttu-id="68444-181">500</span><span class="sxs-lookup"><span data-stu-id="68444-181">500</span></span>              |
| <span data-ttu-id="68444-182">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="68444-182">Throughput per disk</span></span> | <span data-ttu-id="68444-183">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="68444-183">60 MB per second</span></span> | <span data-ttu-id="68444-184">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="68444-184">60 MB per second</span></span> | <span data-ttu-id="68444-185">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="68444-185">60 MB per second</span></span> | <span data-ttu-id="68444-186">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="68444-186">60 MB per second</span></span> | <span data-ttu-id="68444-187">每秒 60 MB</span><span class="sxs-lookup"><span data-stu-id="68444-187">60 MB per second</span></span> |

### <a name="disk-caching-policy"></a><span data-ttu-id="68444-188">磁碟快取原則</span><span class="sxs-lookup"><span data-stu-id="68444-188">Disk caching policy</span></span> 

<span data-ttu-id="68444-189">**進階受控磁碟**</span><span class="sxs-lookup"><span data-stu-id="68444-189">**Premium Managed Disks**</span></span>

<span data-ttu-id="68444-190">根據預設，所有 Premium 資料磁碟的磁碟快取原則都是*唯讀*，而連接至 VM 的 Premium 作業系統磁碟的磁碟快取原則則是*讀寫*。</span><span class="sxs-lookup"><span data-stu-id="68444-190">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="68444-191">為使應用程式的 IO 達到最佳效能，建議使用此組態設定。</span><span class="sxs-lookup"><span data-stu-id="68444-191">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="68444-192">對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="68444-192">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="68444-193">價格</span><span class="sxs-lookup"><span data-stu-id="68444-193">Pricing</span></span>

<span data-ttu-id="68444-194">請檢閱[受控磁碟的價格](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)。</span><span class="sxs-lookup"><span data-stu-id="68444-194">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="68444-195">進階受控磁碟與進階非受控磁碟的價格相同。</span><span class="sxs-lookup"><span data-stu-id="68444-195">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="68444-196">但標準受控磁碟與標準非受控磁碟的價格不同。</span><span class="sxs-lookup"><span data-stu-id="68444-196">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="next-steps"></a><span data-ttu-id="68444-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68444-197">Next Steps</span></span>

- <span data-ttu-id="68444-198">將任何 VHD 上傳至 Azure 之前，您應該遵循[準備 Windows VHD 或 VHDX 以上傳至 Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="68444-198">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
