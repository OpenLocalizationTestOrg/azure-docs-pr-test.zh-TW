---
title: "將 VM 移轉至 Azure 進階儲存體 | Microsoft Docs"
description: "將您現有的 VM 移轉至 Azure 進階儲存體。 「進階儲存體」可針對在「Azure 虛擬機器」上執行且需要大量 I/O 的工作負載，提供高效能、低延遲的磁碟支援。"
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 645b37fff2dd6a12114719bac66a937cf8e8ffaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="5f955-104">移轉至 Azure 進階儲存體 (非受控磁碟)</span><span class="sxs-lookup"><span data-stu-id="5f955-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="5f955-105">本文討論如何將使用非受控標準磁碟的 VM，移轉至使用非受控進階磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="5f955-106">建議您對新 VM 使用 Azure 受控磁碟，並將先前的非受控磁碟轉換成受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f955-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="5f955-107">受控磁碟會處理基礎儲存體帳戶，您不需要再處理。</span><span class="sxs-lookup"><span data-stu-id="5f955-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="5f955-108">如需詳細資訊，請參閱[受控磁碟概觀](storage-managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5f955-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="5f955-109">針對執行時需要大量 I/O 之工作負載的虛擬機器，「Azure 進階儲存體」可提供高效能、低延遲的磁碟支援。</span><span class="sxs-lookup"><span data-stu-id="5f955-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="5f955-110">您可以將應用程式的 VM 磁碟移轉到「Azure 進階儲存體」，以利用這些磁碟的速度和效能。</span><span class="sxs-lookup"><span data-stu-id="5f955-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="5f955-111">本指南的目的，在於協助「Azure 進階儲存體」的新使用者做好準備，以便從他們目前的系統順利轉換到「進階儲存體」。</span><span class="sxs-lookup"><span data-stu-id="5f955-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="5f955-112">本指南說明此程序中的三個重要元件︰</span><span class="sxs-lookup"><span data-stu-id="5f955-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="5f955-113">規劃移轉至進階儲存體</span><span class="sxs-lookup"><span data-stu-id="5f955-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="5f955-114">準備並將虛擬硬碟 (VHD) 複製到進階儲存體</span><span class="sxs-lookup"><span data-stu-id="5f955-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="5f955-115">使用進階儲存體來建立 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5f955-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="5f955-116">您可以將 VM 從其他平台移轉到 Azure 進階儲存體，或將現有的 Azure VM 從標準儲存體移轉到進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f955-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="5f955-117">本指南涵蓋這兩種案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f955-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="5f955-118">請根據您的案例，依照相關小節中所指定的步驟操作。</span><span class="sxs-lookup"><span data-stu-id="5f955-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="5f955-119">如需進階儲存體的功能概觀和價格，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="5f955-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="5f955-120">建議您將任何需要高 IOPS 的虛擬機器磁碟移轉到「Azure 進階儲存體」，以發揮應用程式最佳效能。</span><span class="sxs-lookup"><span data-stu-id="5f955-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="5f955-121">如果您的磁碟不需要高 IOPS，您可以在「標準儲存體」中維護它來限制成本，這會將虛擬機器磁碟資料儲存在「硬碟機 (HDD)」上而非 SSD 上。</span><span class="sxs-lookup"><span data-stu-id="5f955-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="5f955-122">要完整地完成移轉程序，可能需要在本指南中提供的步驟之前和之後執行其他動作。</span><span class="sxs-lookup"><span data-stu-id="5f955-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="5f955-123">例如，設定虛擬網路或端點，或是在應用程式本身中進行程式碼變更，應用程式可能都需要一些停機時間。</span><span class="sxs-lookup"><span data-stu-id="5f955-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="5f955-124">這些動作會隨著每個應用程式而不同，您應完成這些動作以及本指南中所提供的步驟，才能盡可能順暢地完整轉換至進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f955-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="5f955-125"><a name="plan-the-migration-to-premium-storage"></a>規劃移轉至進階儲存體</span><span class="sxs-lookup"><span data-stu-id="5f955-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="5f955-126">這一節確保您準備好遵循本文中的移轉步驟，並協助您對於 VM 和磁碟類型做出最佳的決策。</span><span class="sxs-lookup"><span data-stu-id="5f955-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5f955-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f955-127">Prerequisites</span></span>
* <span data-ttu-id="5f955-128">您將需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-128">You will need an Azure subscription.</span></span> <span data-ttu-id="5f955-129">如果您沒有訂用帳戶，可以建立一個月的[免費試用](https://azure.microsoft.com/pricing/free-trial/)訂用帳戶，或造訪 [Azure 價格](https://azure.microsoft.com/pricing/)以了解其他選項。</span><span class="sxs-lookup"><span data-stu-id="5f955-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="5f955-130">若要執行 PowerShell Cmdlet，您將需要 Microsoft Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="5f955-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="5f955-131">如需安裝點和安裝指示的詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="5f955-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="5f955-132">當您計劃使用在進階儲存體上執行的 Azure VM 時，您需要使用可支援進階儲存體的 VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="5f955-133">您可以將「標準」和「進階」儲存體磁碟與支援「進階儲存體」的 VM 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5f955-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="5f955-134">未來進階儲存體磁碟將可搭配更多 VM 類型使用。</span><span class="sxs-lookup"><span data-stu-id="5f955-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="5f955-135">如需所有可用 Azure VM 磁碟類型和大小的詳細資訊，請參閱[虛擬機器的大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="5f955-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="5f955-136">考量</span><span class="sxs-lookup"><span data-stu-id="5f955-136">Considerations</span></span>
<span data-ttu-id="5f955-137">Azure VM 支援連接數個「進階儲存體」磁碟，讓您應用程式的每一 VM 最多可擁有 256 TB 的儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f955-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="5f955-138">使用「進階儲存體」時，您應用程式的每一 VM 可達到 80,000 IOPS (每秒輸入/輸出作業)，而每一 VM 的每秒磁碟輸送量為 2000 MB，且讀取作業的延遲極低。</span><span class="sxs-lookup"><span data-stu-id="5f955-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="5f955-139">您有各種 VM 和磁碟的選項。</span><span class="sxs-lookup"><span data-stu-id="5f955-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="5f955-140">這一節協助您尋找最適合您工作負載的選項。</span><span class="sxs-lookup"><span data-stu-id="5f955-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="5f955-141">VM 大小</span><span class="sxs-lookup"><span data-stu-id="5f955-141">VM sizes</span></span>
<span data-ttu-id="5f955-142">Azure VM 大小的規格已列在 [虛擬機器的大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)一文中。</span><span class="sxs-lookup"><span data-stu-id="5f955-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5f955-143">請檢閱使用於進階儲存體的虛擬機器效能特性，然後選擇最適合您的工作負載的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="5f955-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="5f955-144">確定 VM 上有足夠的磁碟流量頻寬。</span><span class="sxs-lookup"><span data-stu-id="5f955-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="5f955-145">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="5f955-145">Disk sizes</span></span>
<span data-ttu-id="5f955-146">有五種類型的磁碟可以搭配您的 VM 使用，而且每種都有特定的 IOP 和輸送量限制。</span><span class="sxs-lookup"><span data-stu-id="5f955-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="5f955-147">為您的 VM 選擇磁碟類型時，請根據應用程式在容量、效能、延展性以及尖峰負載方面的需求，將這些限制考量進去。</span><span class="sxs-lookup"><span data-stu-id="5f955-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="5f955-148">進階磁碟類型</span><span class="sxs-lookup"><span data-stu-id="5f955-148">Premium Disks Type</span></span>  | <span data-ttu-id="5f955-149">P10</span><span class="sxs-lookup"><span data-stu-id="5f955-149">P10</span></span>   | <span data-ttu-id="5f955-150">P20</span><span class="sxs-lookup"><span data-stu-id="5f955-150">P20</span></span>   | <span data-ttu-id="5f955-151">P30</span><span class="sxs-lookup"><span data-stu-id="5f955-151">P30</span></span>            | <span data-ttu-id="5f955-152">P40</span><span class="sxs-lookup"><span data-stu-id="5f955-152">P40</span></span>            | <span data-ttu-id="5f955-153">P50</span><span class="sxs-lookup"><span data-stu-id="5f955-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="5f955-154">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="5f955-154">Disk size</span></span>           | <span data-ttu-id="5f955-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="5f955-155">128 GB</span></span>| <span data-ttu-id="5f955-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="5f955-156">512 GB</span></span>| <span data-ttu-id="5f955-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="5f955-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="5f955-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="5f955-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="5f955-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="5f955-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="5f955-160">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="5f955-160">IOPS per disk</span></span>       | <span data-ttu-id="5f955-161">500</span><span class="sxs-lookup"><span data-stu-id="5f955-161">500</span></span>   | <span data-ttu-id="5f955-162">2300</span><span class="sxs-lookup"><span data-stu-id="5f955-162">2300</span></span>  | <span data-ttu-id="5f955-163">5000</span><span class="sxs-lookup"><span data-stu-id="5f955-163">5000</span></span>           | <span data-ttu-id="5f955-164">7500</span><span class="sxs-lookup"><span data-stu-id="5f955-164">7500</span></span>           | <span data-ttu-id="5f955-165">7500</span><span class="sxs-lookup"><span data-stu-id="5f955-165">7500</span></span>           | 
| <span data-ttu-id="5f955-166">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="5f955-166">Throughput per disk</span></span> | <span data-ttu-id="5f955-167">每秒 100 MB</span><span class="sxs-lookup"><span data-stu-id="5f955-167">100 MB per second</span></span> | <span data-ttu-id="5f955-168">每秒 150 MB</span><span class="sxs-lookup"><span data-stu-id="5f955-168">150 MB per second</span></span> | <span data-ttu-id="5f955-169">每秒 200 MB</span><span class="sxs-lookup"><span data-stu-id="5f955-169">200 MB per second</span></span> | <span data-ttu-id="5f955-170">每秒 250 MB</span><span class="sxs-lookup"><span data-stu-id="5f955-170">250 MB per second</span></span> | <span data-ttu-id="5f955-171">每秒 250 MB</span><span class="sxs-lookup"><span data-stu-id="5f955-171">250 MB per second</span></span> |

<span data-ttu-id="5f955-172">根據您的工作負載，決定您的 VM 是否需要額外的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f955-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="5f955-173">您可以將數個持續性資料磁碟連接至您的 VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="5f955-174">如有需要，您可以跨磁碟等量磁碟區以增加磁碟區的容量和效能。</span><span class="sxs-lookup"><span data-stu-id="5f955-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="5f955-175">(請參閱[這裡](storage-premium-storage-performance.md#disk-striping)的磁碟等量化說明。)如果您使用[儲存空間][4]等量進階儲存體資料磁碟，應該對所使用的每個磁碟中的每個資料行進行設定。</span><span class="sxs-lookup"><span data-stu-id="5f955-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="5f955-176">否則，等量磁碟區的整體效能可能會因為磁碟之間的流量分配不平均而低於預期。</span><span class="sxs-lookup"><span data-stu-id="5f955-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="5f955-177">而對於 Linux VM，您可以使用 *mdadm* 公用程式來達到相同的效果。</span><span class="sxs-lookup"><span data-stu-id="5f955-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="5f955-178">如需詳細資訊，請參閱文章 [在 Linux 上設定軟體 RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 。</span><span class="sxs-lookup"><span data-stu-id="5f955-178">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="5f955-179">儲存體帳戶延展性目標</span><span class="sxs-lookup"><span data-stu-id="5f955-179">Storage account scalability targets</span></span>
<span data-ttu-id="5f955-180">進階儲存體帳戶除了 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)之外，還有以下延展性目標。</span><span class="sxs-lookup"><span data-stu-id="5f955-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="5f955-181">如果您的應用程式需求超出單一儲存體帳戶的延展性目標，請建置使用多個儲存體帳戶的應用程式，並將資料分散到那些儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5f955-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="5f955-182">總帳戶容量</span><span class="sxs-lookup"><span data-stu-id="5f955-182">Total Account Capacity</span></span> | <span data-ttu-id="5f955-183">本地備援儲存體帳戶總頻寬</span><span class="sxs-lookup"><span data-stu-id="5f955-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="5f955-184">磁碟容量：35 TB</span><span class="sxs-lookup"><span data-stu-id="5f955-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="5f955-185">快照容量：10 TB</span><span class="sxs-lookup"><span data-stu-id="5f955-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="5f955-186">每秒最多 50 Gbps (輸入 + 輸出)</span><span class="sxs-lookup"><span data-stu-id="5f955-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="5f955-187">如需有關「進階儲存體」規格的詳細資訊，請查看[使用進階儲存體時的延展性和效能目標](storage-premium-storage.md#scalability-and-performance-targets)。</span><span class="sxs-lookup"><span data-stu-id="5f955-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="5f955-188">磁碟快取原則</span><span class="sxs-lookup"><span data-stu-id="5f955-188">Disk caching policy</span></span>
<span data-ttu-id="5f955-189">根據預設，所有 Premium 資料磁碟的磁碟快取原則都是*唯讀*，而連接至 VM 的 Premium 作業系統磁碟的磁碟快取原則則是*讀寫*。</span><span class="sxs-lookup"><span data-stu-id="5f955-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="5f955-190">為使應用程式的 IO 達到最佳效能，建議使用此組態設定。</span><span class="sxs-lookup"><span data-stu-id="5f955-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="5f955-191">對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="5f955-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="5f955-192">而您可以使用 [Azure 入口網站](https://portal.azure.com)或 *Set-AzureDataDisk* Cmdlet 的 *-HostCaching* 參數來更新現有資料磁碟的快取設定。</span><span class="sxs-lookup"><span data-stu-id="5f955-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="5f955-193">位置</span><span class="sxs-lookup"><span data-stu-id="5f955-193">Location</span></span>
<span data-ttu-id="5f955-194">挑選 Azure 進階儲存體可用的位置。</span><span class="sxs-lookup"><span data-stu-id="5f955-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="5f955-195">如需可使用 Azure 服務之地點的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。</span><span class="sxs-lookup"><span data-stu-id="5f955-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="5f955-196">相較於與儲存 VM 磁碟的儲存體帳戶位於不同區域的 VM，位於相同區域將提供更優越的效能。</span><span class="sxs-lookup"><span data-stu-id="5f955-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="5f955-197">其他 Azure VM 組態設定</span><span class="sxs-lookup"><span data-stu-id="5f955-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="5f955-198">建立 Azure VM 時，系統會要求您設定某些 VM 設定。</span><span class="sxs-lookup"><span data-stu-id="5f955-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="5f955-199">請記住，有一些對於 VM 存留期的設定是固定的，但是您稍後可以修改或新增其他設定。</span><span class="sxs-lookup"><span data-stu-id="5f955-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="5f955-200">檢閱這些 Azure VM 組態設定，並確定會適當地設定這些設定以符合您的工作負載需求。</span><span class="sxs-lookup"><span data-stu-id="5f955-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="5f955-201">最佳化</span><span class="sxs-lookup"><span data-stu-id="5f955-201">Optimization</span></span>
<span data-ttu-id="5f955-202">[Azure 進階儲存體︰針對高效能進行設計](storage-premium-storage-performance.md)提供使用 Azure 進階儲存體來建置高效能應用程式的指導方針。</span><span class="sxs-lookup"><span data-stu-id="5f955-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="5f955-203">您可以遵循指定方針，並根據您的應用程式所採用的技術，結合適合的效能最佳作法。</span><span class="sxs-lookup"><span data-stu-id="5f955-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="5f955-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>準備並將虛擬硬碟 (VHD) 複製到進階儲存體</span><span class="sxs-lookup"><span data-stu-id="5f955-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="5f955-205">下一節提供從您的 VM 準備 VHD 以及將 VHD 複製到 Azure 儲存體的指導方針。</span><span class="sxs-lookup"><span data-stu-id="5f955-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="5f955-206">案例 1：「將現有的 Azure VM 移轉到 Azure 進階儲存體。」</span><span class="sxs-lookup"><span data-stu-id="5f955-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="5f955-207">案例 2：「我要將其他平台上的 VM 移轉到 Azure 進階儲存體。」</span><span class="sxs-lookup"><span data-stu-id="5f955-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="5f955-208">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f955-208">Prerequisites</span></span>
<span data-ttu-id="5f955-209">若要準備移轉 VHD，您需要︰</span><span class="sxs-lookup"><span data-stu-id="5f955-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="5f955-210">Azure 訂用帳戶、儲存體帳戶，以及該儲存體帳戶中存放所複製 VHD 的容器。</span><span class="sxs-lookup"><span data-stu-id="5f955-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="5f955-211">請注意，目的地儲存體帳戶可以是標準或進階儲存體帳戶，端視您的需求而定。</span><span class="sxs-lookup"><span data-stu-id="5f955-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="5f955-212">將 VHD 一般化的工具 (如果您打算透過 VHD 建立多個 VM 執行個體)。</span><span class="sxs-lookup"><span data-stu-id="5f955-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="5f955-213">例如，適用於 Windows 的 sysprep 或適用於 Ubuntu 的 virt-sysprep。</span><span class="sxs-lookup"><span data-stu-id="5f955-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="5f955-214">將 VHD 檔案上傳至儲存體帳戶的工具。</span><span class="sxs-lookup"><span data-stu-id="5f955-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="5f955-215">請參閱[使用 AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md)或使用 [Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5f955-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="5f955-216">本指南說明使用 AzCopy 工具複製 VHD 的方法。</span><span class="sxs-lookup"><span data-stu-id="5f955-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="5f955-217">如果您選擇 AzCopy 的同步複製選項，為了達到最佳效能，請使用 Azure VM 中的上述其中一項工具複製 VHD，此 Azure VM 必須和目的地儲存體帳戶位於同一區域。</span><span class="sxs-lookup"><span data-stu-id="5f955-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="5f955-218">如果從不同區域的 Azure VM 複製 VHD，您的效能可能會變慢。</span><span class="sxs-lookup"><span data-stu-id="5f955-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="5f955-219">若要在頻寬有限的情況下複製大量資料，請考慮使用 [Azure 匯入/匯出服務來將資料傳送至 Blob 儲存體](storage-import-export-service.md)，透過將硬碟運送到 Azure 資料中心的方式來傳輸資料。</span><span class="sxs-lookup"><span data-stu-id="5f955-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="5f955-220">使用 Azure 匯入/匯出服務時，您僅能將資料複製到標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="5f955-221">當資料在您的標準儲存體帳戶中之後，您就可以使用 [複製 Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) 或 AzCopy，將資料移轉到您的進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="5f955-222">請注意，Microsoft Azure 僅支援固定大小的 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f955-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="5f955-223">不支援 VHDX 檔案或動態 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="5f955-224">如果您有動態 VHD，可以使用 [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) Cmdlet，將其轉換成固定的大小。</span><span class="sxs-lookup"><span data-stu-id="5f955-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="5f955-225"><a name="scenario1"></a>案例 1：「將現有的 Azure VM 移轉到 Azure 進階儲存體。」</span><span class="sxs-lookup"><span data-stu-id="5f955-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="5f955-226">如果您要移轉現有的 Azure VM，請停止 VM，依據您想要的 VHD 類型準備 VHD，然後使用 AzCopy 或 PowerShell 複製 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="5f955-227">VM 必須完全關閉，才能以全新狀態移轉。</span><span class="sxs-lookup"><span data-stu-id="5f955-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="5f955-228">在移轉完成之前會有停機時間。</span><span class="sxs-lookup"><span data-stu-id="5f955-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="5f955-229">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="5f955-229">Step 1.</span></span> <span data-ttu-id="5f955-230">準備 VHD 進行移轉</span><span class="sxs-lookup"><span data-stu-id="5f955-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="5f955-231">如果是將現有的 Azure VM 移轉到進階儲存體，您的 VHD 可能是：</span><span class="sxs-lookup"><span data-stu-id="5f955-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="5f955-232">一般化作業系統映像</span><span class="sxs-lookup"><span data-stu-id="5f955-232">A generalized operating system image</span></span>
* <span data-ttu-id="5f955-233">唯一的作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="5f955-233">A unique operating system disk</span></span>
* <span data-ttu-id="5f955-234">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="5f955-234">A data disk</span></span>

<span data-ttu-id="5f955-235">下面將逐步解說準備 VHD 的 3 個案例。</span><span class="sxs-lookup"><span data-stu-id="5f955-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="5f955-236">使用一般化作業系統 VHD 建立多個 VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="5f955-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="5f955-237">如果您要上傳將用於建立多個一般 Azure VM 執行個體的 VHD，您必須先使用 sysprep 公用程式將 VHD 一般化。</span><span class="sxs-lookup"><span data-stu-id="5f955-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="5f955-238">這適用於內部部署或雲端的 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="5f955-239">Sysprep 會移除 VHD 中所有電腦特定的資訊。</span><span class="sxs-lookup"><span data-stu-id="5f955-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f955-240">將 VM 一般化之前，請先擷取快照或備份。</span><span class="sxs-lookup"><span data-stu-id="5f955-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="5f955-241">執行 sysprep 會停止並解除配置 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="5f955-242">按照下方的步驟操作，以在 Windows OS VHD 中執行 sysprep。</span><span class="sxs-lookup"><span data-stu-id="5f955-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="5f955-243">請注意，執行 Sysprep 命令會要求您關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5f955-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="5f955-244">如需 Sysprep 的詳細資訊，請參閱 [Sysprep 概觀](http://technet.microsoft.com/library/hh825209.aspx)或 [Sysprep 技術參考](http://technet.microsoft.com/library/cc766049.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5f955-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="5f955-245">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5f955-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="5f955-246">輸入下列命令以開啟 Sysprep：</span><span class="sxs-lookup"><span data-stu-id="5f955-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="5f955-247">在 [系統準備工具] 中依序選取 [進入系統全新體驗 (OOBE)]、[一般化] 核取方塊、[關機]，然後按一下 [確定] \(如下方圖片所示)。</span><span class="sxs-lookup"><span data-stu-id="5f955-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="5f955-248">Sysprep 會將作業系統一般化並關閉系統。</span><span class="sxs-lookup"><span data-stu-id="5f955-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="5f955-249">若是 Ubuntu VM，使用 virt-sysprep 可達到相同效果。</span><span class="sxs-lookup"><span data-stu-id="5f955-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="5f955-250">如需詳細資訊，請參閱 [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) 。</span><span class="sxs-lookup"><span data-stu-id="5f955-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="5f955-251">至於其他 Linux 作業系統，請參閱 [Linux 伺服器佈建軟體](http://www.cyberciti.biz/tips/server-provisioning-software.html) 的一些開放原始碼。</span><span class="sxs-lookup"><span data-stu-id="5f955-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="5f955-252">使用唯一作業系統 VHD 建立單一 VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="5f955-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="5f955-253">如果您有應用程式在需要機器專屬資料的 VM 上執行，請勿將 VHD 一般化。</span><span class="sxs-lookup"><span data-stu-id="5f955-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="5f955-254">非一般化的 VHD 可用來建立唯一的 Azure VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="5f955-255">例如，如果您的 VHD 上有網域控制站，執行 sysprep 將會使它與網域控制站一樣沒有效率。</span><span class="sxs-lookup"><span data-stu-id="5f955-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="5f955-256">檢閱在您的 VM 上執行的應用程式，以及對這些應用程式執行 sysprep 的影響，然後再將 VHD 一般化。</span><span class="sxs-lookup"><span data-stu-id="5f955-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="5f955-257">註冊資料磁碟 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-257">Register data disk VHD</span></span>
<span data-ttu-id="5f955-258">如果您在 Azure 中有要移轉的資料磁碟，必須確定使用這些資料磁碟的 VM 已關閉。</span><span class="sxs-lookup"><span data-stu-id="5f955-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="5f955-259">遵循以下所述的步驟，將 VHD 複製到 Azure 進階儲存體並註冊為佈建的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f955-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="5f955-260">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="5f955-260">Step 2.</span></span> <span data-ttu-id="5f955-261">為您的 VHD 建立目的地</span><span class="sxs-lookup"><span data-stu-id="5f955-261">Create the destination for your VHD</span></span>
<span data-ttu-id="5f955-262">建立儲存體帳戶來維護您的 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="5f955-263">規劃儲存 VHD 的位置時，請考量下列幾點：</span><span class="sxs-lookup"><span data-stu-id="5f955-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="5f955-264">目標進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-264">The target Premium storage account.</span></span>
* <span data-ttu-id="5f955-265">儲存體帳戶位置必須與您將在最終階段建立之可支援進階儲存體的 Azure VM 相同。</span><span class="sxs-lookup"><span data-stu-id="5f955-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="5f955-266">您可以複製到新的儲存體帳戶，或打算根據您的需求，使用相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="5f955-267">為下一個階段複製並儲存目的地儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f955-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="5f955-268">若是資料磁碟，您可以選擇將一些資料磁碟保留在標準儲存體帳戶中 (例如，具有散熱器儲存體的磁碟)，但我們強烈建議您移動生產工作負載的所有資料以使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f955-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="5f955-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>步驟 3.</span><span class="sxs-lookup"><span data-stu-id="5f955-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="5f955-270">使用 AzCopy 或 PowerShell 複製 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="5f955-271">您必須尋找您的容器路徑和儲存體帳戶金鑰，才能處理這兩個選項之一。</span><span class="sxs-lookup"><span data-stu-id="5f955-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="5f955-272">容器路徑和儲存體帳戶金鑰位於 **Azure 入口網站** > **儲存體**。</span><span class="sxs-lookup"><span data-stu-id="5f955-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="5f955-273">容器 URL 類似 "https://myaccount.blob.core.windows.net/mycontainer/"。</span><span class="sxs-lookup"><span data-stu-id="5f955-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="5f955-274">選項 1︰使用 AzCopy 複製 VHD (非同步複製)</span><span class="sxs-lookup"><span data-stu-id="5f955-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="5f955-275">您可以使用 AzCopy，透過網際網路輕鬆上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="5f955-276">根據 VHD 的大小，這可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="5f955-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="5f955-277">使用這個選項時，請記得檢查儲存體帳戶輸入/輸出限制。</span><span class="sxs-lookup"><span data-stu-id="5f955-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="5f955-278">如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) 。</span><span class="sxs-lookup"><span data-stu-id="5f955-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="5f955-279">從這裡下載並安裝 AzCopy： [AzCopy 的最新版本](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="5f955-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="5f955-280">開啟 Azure PowerShell，並移至安裝 AzCopy 所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5f955-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="5f955-281">使用下列命令，將 VHD 檔案從「來源」複製到「目的地」。</span><span class="sxs-lookup"><span data-stu-id="5f955-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="5f955-282">範例：</span><span class="sxs-lookup"><span data-stu-id="5f955-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="5f955-283">以下是有關用於 AzCopy 命令中之參數的描述：</span><span class="sxs-lookup"><span data-stu-id="5f955-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="5f955-284">**/Source: *&lt;source&gt;：***包含 VHD 的資料夾或儲存體容器 URL 的位置。</span><span class="sxs-lookup"><span data-stu-id="5f955-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="5f955-285">**/SourceKey: *&lt;source-account-key&gt;：***來源儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f955-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="5f955-286">**/Dest: *&lt;destination&gt;：***要複製 VHD 的目的地儲存體容器 URL。</span><span class="sxs-lookup"><span data-stu-id="5f955-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="5f955-287">**/DestKey: *&lt;dest-account-key&gt;：***目的地儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f955-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="5f955-288">**/Pattern: *&lt;file-name&gt;：***指定要複製 VHD 的目標檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="5f955-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="5f955-289">如需使用 AzCopy 工具的詳細資訊，請參閱 [使用 AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md)》\。</span><span class="sxs-lookup"><span data-stu-id="5f955-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="5f955-290">選項 2：使用 PowerShell 複製 VHD (同步處理的複製)</span><span class="sxs-lookup"><span data-stu-id="5f955-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="5f955-291">您也可以使用 PowerShell Cmdlet Start-AzureStorageBlobCopy 來複製 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f955-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="5f955-292">在 Azure PowerShell 上使用下列命令來複製 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="5f955-293">將 <> 中的值取代為您的來源和目的地儲存體帳戶中的對應值。</span><span class="sxs-lookup"><span data-stu-id="5f955-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="5f955-294">若要使用此命令，您的目的地儲存體帳戶中必須具有名為 vhds 的容器。</span><span class="sxs-lookup"><span data-stu-id="5f955-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="5f955-295">如果此容器不存在，請先加以建立，再執行命令。</span><span class="sxs-lookup"><span data-stu-id="5f955-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="5f955-296">範例：</span><span class="sxs-lookup"><span data-stu-id="5f955-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="5f955-297"><a name="scenario2"></a>案例 2：「我要將其他平台上的 VM 移轉到 Azure 進階儲存體。」</span><span class="sxs-lookup"><span data-stu-id="5f955-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="5f955-298">如果您將 VHD 從非 Azure 雲端儲存體移轉至 Azure，您必須先將 VHD 匯出至本機目錄。</span><span class="sxs-lookup"><span data-stu-id="5f955-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="5f955-299">讓儲存 VHD 所在本機目錄的完整來源路徑位於方便取得的位置，然後使用 AzCopy 將它上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f955-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="5f955-300">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="5f955-300">Step 1.</span></span> <span data-ttu-id="5f955-301">將 VHD 匯出至本機目錄</span><span class="sxs-lookup"><span data-stu-id="5f955-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="5f955-302">從 AWS 複製 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="5f955-303">如果您使用的是 AWS，請將 EC2 執行個體匯出至 Amazon S3 貯體中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="5f955-304">請依照 Amazon 文件中所述的「匯出 Amazon EC2 執行個體」步驟，安裝 Amazon EC2 命令列介面 (CLI) 工具並執行 create-instance-export-task 命令，將 EC2 執行個體匯出到 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f955-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="5f955-305">執行 **create-instance-export-task** 命令時，請務必讓 DISK&#95;IMAGE&#95;FORMAT 變數使用 **VHD**。</span><span class="sxs-lookup"><span data-stu-id="5f955-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="5f955-306">已匯出的 VHD 檔案會儲存在您在該程序期間所指定的 Amazon S3 貯體中。</span><span class="sxs-lookup"><span data-stu-id="5f955-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="5f955-307">從 S3 貯體下載 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f955-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="5f955-308">然後選取 VHD 檔案，再依序按一下 [動作] > [下載]。</span><span class="sxs-lookup"><span data-stu-id="5f955-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="5f955-309">從其他非 Azure 雲端複製 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="5f955-310">如果您將 VHD 從非 Azure 雲端儲存體移轉至 Azure，您必須先將 VHD 匯出至本機目錄。</span><span class="sxs-lookup"><span data-stu-id="5f955-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="5f955-311">複製儲存 VHD 所在本機目錄的完整來源路徑。</span><span class="sxs-lookup"><span data-stu-id="5f955-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="5f955-312">從內部部署複製 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="5f955-313">如果您要從內部部署環境移轉 VHD，將需要儲存 VHD 的完整來源路徑。</span><span class="sxs-lookup"><span data-stu-id="5f955-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="5f955-314">來源路徑可能是伺服器位置或檔案共用。</span><span class="sxs-lookup"><span data-stu-id="5f955-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="5f955-315">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="5f955-315">Step 2.</span></span> <span data-ttu-id="5f955-316">為您的 VHD 建立目的地</span><span class="sxs-lookup"><span data-stu-id="5f955-316">Create the destination for your VHD</span></span>
<span data-ttu-id="5f955-317">建立儲存體帳戶來維護您的 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="5f955-318">規劃儲存 VHD 的位置時，請考量下列幾點：</span><span class="sxs-lookup"><span data-stu-id="5f955-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="5f955-319">目標儲存體帳戶可能是 Standard 或進階儲存體，端視您的應用程式需求而定。</span><span class="sxs-lookup"><span data-stu-id="5f955-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="5f955-320">儲存體帳戶區域必須與您將在最終階段建立之可支援進階儲存體的 Azure VM 相同。</span><span class="sxs-lookup"><span data-stu-id="5f955-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="5f955-321">您可以複製到新的儲存體帳戶，或打算根據您的需求，使用相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="5f955-322">為下一個階段複製並儲存目的地儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f955-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="5f955-323">強烈建議您移動生產工作負載的所有資料以使用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f955-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="5f955-324">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="5f955-324">Step 3.</span></span> <span data-ttu-id="5f955-325">將 VHD 上傳至 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="5f955-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="5f955-326">現在，您的 VHD 位於本機目錄中，您可以使用 AzCopy 或 AzurePowerShell 將 .vhd 檔案上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f955-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="5f955-327">下面提供兩個選項︰</span><span class="sxs-lookup"><span data-stu-id="5f955-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="5f955-328">選項 1︰使用 Azure PowerShell Add-AzureVhd 上傳 .vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="5f955-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="5f955-329">範例 <Uri> 可能是 ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***。</span><span class="sxs-lookup"><span data-stu-id="5f955-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="5f955-330">範例 <FileInfo> 可能是 ***"C:\path\to\upload.vhd"***。</span><span class="sxs-lookup"><span data-stu-id="5f955-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="5f955-331">選項 2︰使用 AzCopy 上傳 .vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="5f955-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="5f955-332">您可以使用 AzCopy，透過網際網路輕鬆上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="5f955-333">根據 VHD 的大小，這可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="5f955-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="5f955-334">使用這個選項時，請記得檢查儲存體帳戶輸入/輸出限制。</span><span class="sxs-lookup"><span data-stu-id="5f955-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="5f955-335">如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) 。</span><span class="sxs-lookup"><span data-stu-id="5f955-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="5f955-336">從這裡下載並安裝 AzCopy： [AzCopy 的最新版本](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="5f955-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="5f955-337">開啟 Azure PowerShell，並移至安裝 AzCopy 所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5f955-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="5f955-338">使用下列命令，將 VHD 檔案從「來源」複製到「目的地」。</span><span class="sxs-lookup"><span data-stu-id="5f955-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="5f955-339">範例：</span><span class="sxs-lookup"><span data-stu-id="5f955-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="5f955-340">以下是有關用於 AzCopy 命令中之參數的描述：</span><span class="sxs-lookup"><span data-stu-id="5f955-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="5f955-341">**/Source: *&lt;source&gt;：***包含 VHD 的資料夾或儲存體容器 URL 的位置。</span><span class="sxs-lookup"><span data-stu-id="5f955-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="5f955-342">**/SourceKey: *&lt;source-account-key&gt;：***來源儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f955-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="5f955-343">**/Dest: *&lt;destination&gt;：***要複製 VHD 的目的地儲存體容器 URL。</span><span class="sxs-lookup"><span data-stu-id="5f955-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="5f955-344">**/DestKey: *&lt;dest-account-key&gt;：***目的地儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="5f955-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="5f955-345">**/BlobType: page:** 將目的地指定為分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="5f955-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="5f955-346">**/Pattern: *&lt;file-name&gt;：***指定要複製 VHD 的目標檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="5f955-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="5f955-347">如需使用 AzCopy 工具的詳細資訊，請參閱 [使用 AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md)》\。</span><span class="sxs-lookup"><span data-stu-id="5f955-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="5f955-348">上傳 VHD 的其他選項</span><span class="sxs-lookup"><span data-stu-id="5f955-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="5f955-349">您也可以使用下方其中一種方法將 VHD 上傳至您的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="5f955-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="5f955-350">Azure 儲存體複製 Blob API</span><span class="sxs-lookup"><span data-stu-id="5f955-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="5f955-351">Azure 儲存體總管上傳 Blob</span><span class="sxs-lookup"><span data-stu-id="5f955-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="5f955-352">儲存體匯入/匯出服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="5f955-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="5f955-353">如果預估的上傳時間長度超過 7 天，我們建議使用匯入/匯出服務。</span><span class="sxs-lookup"><span data-stu-id="5f955-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="5f955-354">您可以使用 [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) 從資料大小和傳輸單位來評估時間。</span><span class="sxs-lookup"><span data-stu-id="5f955-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="5f955-355">匯入/匯出可用來複製到標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="5f955-356">您必須使用 AzCopy 之類的工具，從 Standard 儲存體帳戶複製到進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="5f955-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>使用進階儲存體建立 Azure VM</span><span class="sxs-lookup"><span data-stu-id="5f955-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="5f955-358">將 VHD 上傳或複製到所需的儲存體帳戶之後，請遵循本節中的指示，根據您的情況，將 VHD 註冊為作業系統映像或作業系統磁碟，然後從該映像或磁碟建立 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="5f955-359">一旦建立之後，資料磁碟 VHD 就可以連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="5f955-360">本節的結尾會提供範例移轉指令碼。</span><span class="sxs-lookup"><span data-stu-id="5f955-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="5f955-361">這個簡單的指令碼不符合所有案例。</span><span class="sxs-lookup"><span data-stu-id="5f955-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="5f955-362">您可能需要更新指令碼以符合您的特定案例。</span><span class="sxs-lookup"><span data-stu-id="5f955-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="5f955-363">若要查看此指令碼是否適用於您的案例，請參閱下面的[範例移轉指令碼](#a-sample-migration-script)。</span><span class="sxs-lookup"><span data-stu-id="5f955-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="5f955-364">檢查清單</span><span class="sxs-lookup"><span data-stu-id="5f955-364">Checklist</span></span>
1. <span data-ttu-id="5f955-365">等到所有的 VHD 磁碟複製完成。</span><span class="sxs-lookup"><span data-stu-id="5f955-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="5f955-366">請確定進階儲存體可在您要移轉到的區域中使用。</span><span class="sxs-lookup"><span data-stu-id="5f955-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="5f955-367">決定您將要使用的新 VM 系列。</span><span class="sxs-lookup"><span data-stu-id="5f955-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="5f955-368">這應可支援進階儲存體，而且大小取決於區域中的可用性和您的需求。</span><span class="sxs-lookup"><span data-stu-id="5f955-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="5f955-369">決定您將要使用的確切 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="5f955-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="5f955-370">VM 大小必須足以支援您所擁有的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="5f955-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="5f955-371">例如</span><span class="sxs-lookup"><span data-stu-id="5f955-371">E.g.</span></span> <span data-ttu-id="5f955-372">如果您有 4 個資料磁碟，VM 必須有 2 個或多個核心。</span><span class="sxs-lookup"><span data-stu-id="5f955-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="5f955-373">也請考慮處理能力、記憶體和網路頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="5f955-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="5f955-374">在目標區域中建立進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="5f955-375">這是您將用於新 VM 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f955-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="5f955-376">請備妥目前 VM 的詳細資料，包括磁碟和對應 VHD Blob 的清單。</span><span class="sxs-lookup"><span data-stu-id="5f955-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="5f955-377">為您的應用程式做好停機準備。</span><span class="sxs-lookup"><span data-stu-id="5f955-377">Prepare your application for downtime.</span></span> <span data-ttu-id="5f955-378">若要進行全新移轉，您必須停止目前系統中的所有處理。</span><span class="sxs-lookup"><span data-stu-id="5f955-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="5f955-379">只有這樣，您才可以使其維持在可移轉至新平台的一致狀態。</span><span class="sxs-lookup"><span data-stu-id="5f955-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="5f955-380">停機持續時間將取決於磁碟中要移轉的資料量。</span><span class="sxs-lookup"><span data-stu-id="5f955-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="5f955-381">如果您要從指定的 VHD 磁碟建立 Azure Resource Manager VM，請參閱[此範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)以便使用現有的磁碟部署 Azure Resource Manager VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="5f955-382">註冊 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-382">Register your VHD</span></span>
<span data-ttu-id="5f955-383">若要透過 OS VHD 建立 VM，或將資料磁碟連接到新的 VM，您必須先註冊 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="5f955-384">根據您的 VHD 案例，遵循以下步驟。</span><span class="sxs-lookup"><span data-stu-id="5f955-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="5f955-385">建立多個 Azure VM 執行個體的一般化的作業系統 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="5f955-386">將一般化的作業系統映像 VHD 上傳至儲存體帳戶之後，將其註冊為 **Azure VM 映像**，以便您從該映像建立一個或多個 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="5f955-387">使用下列 PowerShell Cmdlet 將您的 VHD 註冊為 Azure VM 作業系統映像。</span><span class="sxs-lookup"><span data-stu-id="5f955-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="5f955-388">提供存放複製的 VHD 的完整容器 URL。</span><span class="sxs-lookup"><span data-stu-id="5f955-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="5f955-389">複製並儲存這個新 Azure VM 映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="5f955-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="5f955-390">在上述範例中，該名稱是 *OSImageName*。</span><span class="sxs-lookup"><span data-stu-id="5f955-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="5f955-391">建立單一 Azure VM 執行個體的唯一作業系統 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="5f955-392">將唯一的作業系統 VHD 上傳至儲存體帳戶之後，將其註冊為 **Azure 作業系統磁碟**，以便您從該磁碟建立 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="5f955-393">使用下列 PowerShell Cmdlet 將您的 VHD 註冊為 Azure 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f955-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="5f955-394">提供存放複製的 VHD 的完整容器 URL。</span><span class="sxs-lookup"><span data-stu-id="5f955-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="5f955-395">複製並儲存這個新 Azure 作業系統磁碟的名稱。</span><span class="sxs-lookup"><span data-stu-id="5f955-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="5f955-396">在上述範例中，該名稱是「OSDisk」 。</span><span class="sxs-lookup"><span data-stu-id="5f955-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="5f955-397">連接至新 Azure VM 執行個體的資料磁碟 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="5f955-398">將資料磁碟 VHD 上傳至儲存體帳戶之後，將其註冊為 Azure 資料磁碟，便可以連接到新的 DS 系列、DSv2 系列或 GS 系列 Azure VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="5f955-399">使用下列 PowerShell Cmdlet 將您的 VHD 註冊為 Azure 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f955-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="5f955-400">提供存放複製的 VHD 的完整容器 URL。</span><span class="sxs-lookup"><span data-stu-id="5f955-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="5f955-401">複製並儲存這個新 Azure 資料磁碟的名稱。</span><span class="sxs-lookup"><span data-stu-id="5f955-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="5f955-402">在上述範例中，該名稱是「DataDisk」 。</span><span class="sxs-lookup"><span data-stu-id="5f955-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="5f955-403">建立可支援進階儲存體的 VM</span><span class="sxs-lookup"><span data-stu-id="5f955-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="5f955-404">註冊 OS 映像或 OS 磁碟之後，請建立新的 DS 系列、DSv2 系列或 GS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="5f955-405">您將使用您註冊的作業系統映像或作業系統磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="5f955-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="5f955-406">從進階儲存體層選取 VM 類型。</span><span class="sxs-lookup"><span data-stu-id="5f955-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="5f955-407">在下列範例中，我們使用的 VM 大小為「Standard_DS2」。</span><span class="sxs-lookup"><span data-stu-id="5f955-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="5f955-408">更新磁碟大小以確定它符合您的容量、效能需求，和可用的 Azure 磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="5f955-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="5f955-409">依照下方的 PowerShell Cmdlet 逐步建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="5f955-410">首先，設定一般參數：</span><span class="sxs-lookup"><span data-stu-id="5f955-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="5f955-411">首先，建立您將在當中裝載新 VM 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5f955-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="5f955-412">接下來，根據您的情況，透過您註冊的 OS 映像或 OS 磁碟，建立 Azure VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="5f955-413">建立多個 Azure VM 執行個體的一般化的作業系統 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="5f955-414">使用您註冊的 **Azure 作業系統映像** ，建立一個或多個新的 DS 系列 Azure VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="5f955-415">如下方所示，在建立新的 VM 時，於 VM 組態中指定此 OS 映像名稱。</span><span class="sxs-lookup"><span data-stu-id="5f955-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="5f955-416">建立單一 Azure VM 執行個體的唯一作業系統 VHD</span><span class="sxs-lookup"><span data-stu-id="5f955-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="5f955-417">使用您註冊的 **Azure 作業系統磁碟** ，建立新的 DS 系列 Azure VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="5f955-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="5f955-418">如下方所示，在建立新的 VM 時，於 VM 組態中指定此 OS 的磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="5f955-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="5f955-419">指定其他 Azure VM 資訊，例如雲端服務、區域、儲存體帳戶、可用性設定組以及快取原則。</span><span class="sxs-lookup"><span data-stu-id="5f955-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="5f955-420">請注意，VM 執行個體必須與相關的作業系統或資料磁碟共置，因此選取的雲端服務、區域和儲存體帳戶全都必須與這些磁碟的基礎 VHD 位於相同的位置。</span><span class="sxs-lookup"><span data-stu-id="5f955-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="5f955-421">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="5f955-421">Attach data disk</span></span>
<span data-ttu-id="5f955-422">最後，如果您已經註冊資料磁碟 VHD，請將它們連接至可支援進階儲存體的新 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="5f955-423">使用下列 PowerShell Cmdlet，將資料磁碟連接至新的 VM，並指定快取原則。</span><span class="sxs-lookup"><span data-stu-id="5f955-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="5f955-424">在下列範例中，快取原則設定為「ReadOnly」 。</span><span class="sxs-lookup"><span data-stu-id="5f955-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="5f955-425">可能有一些支援應用程式所需的其他步驟不包含在本指南中。</span><span class="sxs-lookup"><span data-stu-id="5f955-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="5f955-426">檢查和規劃備份</span><span class="sxs-lookup"><span data-stu-id="5f955-426">Checking and plan backup</span></span>
<span data-ttu-id="5f955-427">在新的 VM 啟動並執行後，請使用與原始 VM 相同的登入識別碼和密碼加以存取，並確認一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="5f955-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="5f955-428">所有設定 (包括等量磁碟區) 都會出現在新的 VM 中。</span><span class="sxs-lookup"><span data-stu-id="5f955-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="5f955-429">最後一個步驟是依據應用程式的需求為新的 VM 規劃備份和維護排程。</span><span class="sxs-lookup"><span data-stu-id="5f955-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="5f955-430"><a name="a-sample-migration-script"></a>範例移轉指令碼</span><span class="sxs-lookup"><span data-stu-id="5f955-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="5f955-431">如果您有多個要移轉的 VM，透過 PowerShell 指令碼將其自動化會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="5f955-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="5f955-432">以下是將 VM 的移轉自動化的範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="5f955-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="5f955-433">請注意，以下指令碼只是範例，且對於目前的 VM 磁碟做了幾個相關假設。</span><span class="sxs-lookup"><span data-stu-id="5f955-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="5f955-434">您可能需要更新指令碼以符合您的特定案例。</span><span class="sxs-lookup"><span data-stu-id="5f955-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="5f955-435">假設如下：</span><span class="sxs-lookup"><span data-stu-id="5f955-435">The assumptions are:</span></span>

* <span data-ttu-id="5f955-436">您正在建立傳統 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="5f955-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="5f955-437">您的來源作業系統磁碟和來源資料磁碟位於相同儲存體帳戶和相同容器中。</span><span class="sxs-lookup"><span data-stu-id="5f955-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="5f955-438">如果您的作業系統磁碟和資料磁碟不在相同的地方，您可以使用 AzCopy 或 Azure PowerShell 來複製不同儲存體帳戶和容器之間的 VHD。</span><span class="sxs-lookup"><span data-stu-id="5f955-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="5f955-439">請參閱上一個步驟︰[使用 AzCopy 或 PowerShell 複製 VHD](#copy-vhd-with-azcopy-or-powershell)。</span><span class="sxs-lookup"><span data-stu-id="5f955-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="5f955-440">編輯此指令碼以符合您的案例是另一個選擇，但我們建議使用 AzCopy 或 PowerShell，因為比較容易且快速。</span><span class="sxs-lookup"><span data-stu-id="5f955-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="5f955-441">以下提供自動化指令碼。</span><span class="sxs-lookup"><span data-stu-id="5f955-441">The automation script is provided below.</span></span> <span data-ttu-id="5f955-442">以您的資訊取代文字，並更新指令碼以符合您的特定案例。</span><span class="sxs-lookup"><span data-stu-id="5f955-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="5f955-443">使用現有的指令碼不會保留來源 VM 的網路組態。</span><span class="sxs-lookup"><span data-stu-id="5f955-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="5f955-444">您必須在移轉後的 VM 上重新設定網路設定。</span><span class="sxs-lookup"><span data-stu-id="5f955-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check the Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="5f955-445"><a name="optimization"></a>最佳化</span><span class="sxs-lookup"><span data-stu-id="5f955-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="5f955-446">您目前的 VM 組態可以自訂，以適用於標準磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f955-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="5f955-447">例如，在等量磁碟區中使用多個磁碟，以提高效能。</span><span class="sxs-lookup"><span data-stu-id="5f955-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="5f955-448">例如，您無須在進階儲存體上個別使用 4 個磁碟，而可以藉由單一磁碟發揮成本效益。</span><span class="sxs-lookup"><span data-stu-id="5f955-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="5f955-449">這樣最佳化必須就個別案例來處理，且在移轉之後需執行自訂步驟。</span><span class="sxs-lookup"><span data-stu-id="5f955-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="5f955-450">另請注意，此程序可能不適用於依賴設定中所定義之磁碟配置的資料庫和應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f955-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="5f955-451">準備工作</span><span class="sxs-lookup"><span data-stu-id="5f955-451">Preparation</span></span>
1. <span data-ttu-id="5f955-452">依照前一節中的說明完成簡單移轉。</span><span class="sxs-lookup"><span data-stu-id="5f955-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="5f955-453">在移轉之後，將會在新 VM 上執行最佳化。</span><span class="sxs-lookup"><span data-stu-id="5f955-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="5f955-454">定義最佳化組態所需的新磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="5f955-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="5f955-455">判斷目前磁碟/磁碟區與新磁碟規格之間的對應。</span><span class="sxs-lookup"><span data-stu-id="5f955-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="5f955-456">執行步驟</span><span class="sxs-lookup"><span data-stu-id="5f955-456">Execution steps</span></span>
1. <span data-ttu-id="5f955-457">在進階儲存體 VM 上以正確的大小建立新的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f955-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="5f955-458">登入 VM，並將資料從目前的磁碟區複製到對應至該磁碟區的新磁碟。</span><span class="sxs-lookup"><span data-stu-id="5f955-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="5f955-459">請為所有需要對應至新磁碟的目前磁碟區執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="5f955-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="5f955-460">接下來，請變更應用程式設定以切換至新的磁碟，並卸離舊磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5f955-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="5f955-461">如需調整應用程式以獲得更好的磁碟效能，請參閱[最佳化應用程式效能](storage-premium-storage-performance.md#optimizing-application-performance)。</span><span class="sxs-lookup"><span data-stu-id="5f955-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="5f955-462">應用程式移轉</span><span class="sxs-lookup"><span data-stu-id="5f955-462">Application migrations</span></span>
<span data-ttu-id="5f955-463">資料庫和其他複雜的應用程式在移轉時，可能需要應用程式提供者所定義的特殊步驟。</span><span class="sxs-lookup"><span data-stu-id="5f955-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="5f955-464">請參閱個別的應用程式文件。</span><span class="sxs-lookup"><span data-stu-id="5f955-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="5f955-465">例如</span><span class="sxs-lookup"><span data-stu-id="5f955-465">E.g.</span></span> <span data-ttu-id="5f955-466">資料庫通常可透過備份和還原來移轉。</span><span class="sxs-lookup"><span data-stu-id="5f955-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f955-467">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f955-467">Next steps</span></span>
<span data-ttu-id="5f955-468">如需移轉虛擬機器的特定案例，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="5f955-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="5f955-469">在儲存體帳戶之間移轉 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5f955-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="5f955-470">建立並上傳 Windows Server VHD 到 Azure。</span><span class="sxs-lookup"><span data-stu-id="5f955-470">Create and upload a Windows Server VHD to Azure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="5f955-471">建立及上傳包含 Linux 作業系統的虛擬硬碟</span><span class="sxs-lookup"><span data-stu-id="5f955-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="5f955-472">將虛擬機器從 Amazon AWS 移轉至 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5f955-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="5f955-473">若要深入了解 Azure 儲存體和 Azure 虛擬機器，也請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="5f955-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="5f955-474">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="5f955-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="5f955-475">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5f955-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="5f955-476">進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體</span><span class="sxs-lookup"><span data-stu-id="5f955-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
