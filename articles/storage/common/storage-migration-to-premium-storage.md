---
title: "aaaMigrating Vm tooAzure 高階儲存體 |Microsoft 文件"
description: "移轉您現有的 Vm tooAzure 高階儲存體。 「進階儲存體」可針對在「Azure 虛擬機器」上執行且需要大量 I/O 的工作負載，提供高效能、低延遲的磁碟支援。"
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
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="c3136-104">移轉 tooAzure 高階儲存體 （Unmanaged 磁碟）</span><span class="sxs-lookup"><span data-stu-id="c3136-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="c3136-105">本文將討論如何使用未受管理的標準磁碟 tooa VM 來使用的 VM，toomigrate unmanaged 高階磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="c3136-106">我們建議您對於新的 Vm，使用 Azure 受管理的磁碟，並將轉換上一個 unmanaged 的磁碟 toomanaged 磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="c3136-107">管理磁碟控制代碼 hello 基礎儲存體帳戶，因此您不需要。</span><span class="sxs-lookup"><span data-stu-id="c3136-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="c3136-108">如需詳細資訊，請參閱[受控磁碟概觀](../../virtual-machines/windows/managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c3136-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="c3136-109">針對執行時需要大量 I/O 之工作負載的虛擬機器，「Azure 進階儲存體」可提供高效能、低延遲的磁碟支援。</span><span class="sxs-lookup"><span data-stu-id="c3136-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="c3136-110">移轉您的應用程式的 VM 磁碟 tooAzure 高階儲存體，您可以利用 hello 速度的與這些磁碟的效能。</span><span class="sxs-lookup"><span data-stu-id="c3136-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="c3136-111">本指南用途 hello 是 toohelp 更好的 Azure 高階儲存體的新使用者準備 toomake 平順地轉換從其目前的系統 tooPremium 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c3136-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="c3136-112">hello 指南來解決此程序中的 hello 主要元件中的三種：</span><span class="sxs-lookup"><span data-stu-id="c3136-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="c3136-113">規劃 hello 移轉 tooPremium 儲存體</span><span class="sxs-lookup"><span data-stu-id="c3136-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="c3136-114">準備和複製虛擬硬碟 (Vhd) tooPremium 儲存體</span><span class="sxs-lookup"><span data-stu-id="c3136-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="c3136-115">使用進階儲存體來建立 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c3136-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="c3136-116">您可以從其他平台 tooAzure 高階儲存體移轉 Vm，或從標準儲存體 tooPremium 存放裝置移轉現有的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="c3136-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="c3136-117">本指南涵蓋這兩種案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="c3136-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="c3136-118">請遵循 hello hello 相關區段，根據您的案例中指定的步驟。</span><span class="sxs-lookup"><span data-stu-id="c3136-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="c3136-119">如需進階儲存體的功能概觀和價格，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="c3136-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="c3136-120">我們建議您移轉任何 hello 最佳效能，您的應用程式需要高 IOPS tooAzure 高階儲存體的虛擬機器磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="c3136-121">如果您的磁碟不需要高 IOPS，您可以在「標準儲存體」中維護它來限制成本，這會將虛擬機器磁碟資料儲存在「硬碟機 (HDD)」上而非 SSD 上。</span><span class="sxs-lookup"><span data-stu-id="c3136-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="c3136-122">完成完整的 hello 移轉程序可能需要執行其他動作之前和之後提供本指南中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="c3136-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="c3136-123">範例包括設定虛擬網路或端點或 hello 應用程式本身可能需要在您的應用程式停機一段時間內的程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="c3136-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="c3136-124">這些動作唯一 tooeach 應用程式，而且您應該提供此指南 toomake hello 完整的轉換 tooPremium 盡可能的緊密性儲存體中的 hello 步驟以及完成。</span><span class="sxs-lookup"><span data-stu-id="c3136-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="c3136-125"><a name="plan-the-migration-to-premium-storage"></a>規劃 hello 移轉 tooPremium 儲存體</span><span class="sxs-lookup"><span data-stu-id="c3136-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="c3136-126">本節可確保您已準備好 toofollow hello 移轉步驟，在本文中，並協助您 toomake hello 最佳決定 VM 和磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="c3136-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c3136-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="c3136-127">Prerequisites</span></span>
* <span data-ttu-id="c3136-128">您將需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3136-128">You will need an Azure subscription.</span></span> <span data-ttu-id="c3136-129">如果您沒有訂用帳戶，可以建立一個月的[免費試用](https://azure.microsoft.com/pricing/free-trial/)訂用帳戶，或造訪 [Azure 價格](https://azure.microsoft.com/pricing/)以了解其他選項。</span><span class="sxs-lookup"><span data-stu-id="c3136-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="c3136-130">tooexecute PowerShell cmdlet，您將需要 hello Microsoft Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="c3136-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="c3136-131">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) hello 安裝點和安裝指示。</span><span class="sxs-lookup"><span data-stu-id="c3136-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="c3136-132">當您計劃 toouse 高階儲存體上執行的 Azure Vm 時，您會需要 toouse hello 高階儲存體功能的 Vm。</span><span class="sxs-lookup"><span data-stu-id="c3136-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="c3136-133">您可以將「標準」和「進階」儲存體磁碟與支援「進階儲存體」的 VM 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c3136-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="c3136-134">高階儲存體磁碟將會提供更多的 VM 類型，在未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="c3136-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="c3136-135">如需所有可用 Azure VM 磁碟類型和大小的詳細資訊，請參閱[虛擬機器的大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[雲端服務的大小](../../cloud-services/cloud-services-sizes-specs.md)。</span><span class="sxs-lookup"><span data-stu-id="c3136-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="c3136-136">考量</span><span class="sxs-lookup"><span data-stu-id="c3136-136">Considerations</span></span>
<span data-ttu-id="c3136-137">Azure VM 支援附加數個進階儲存體磁碟，以便您的應用程式可以有向上 too256 TB 的每個 VM 的存放空間。</span><span class="sxs-lookup"><span data-stu-id="c3136-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="c3136-138">使用「進階儲存體」時，您應用程式的每一 VM 可達到 80,000 IOPS (每秒輸入/輸出作業)，而每一 VM 的每秒磁碟輸送量為 2000 MB，且讀取作業的延遲極低。</span><span class="sxs-lookup"><span data-stu-id="c3136-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="c3136-139">您有各種 VM 和磁碟的選項。</span><span class="sxs-lookup"><span data-stu-id="c3136-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="c3136-140">這個區段是 toohelp toofind 最適合您的工作負載選項。</span><span class="sxs-lookup"><span data-stu-id="c3136-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="c3136-141">VM 大小</span><span class="sxs-lookup"><span data-stu-id="c3136-141">VM sizes</span></span>
<span data-ttu-id="c3136-142">hello Azure VM 大小規格中所列[虛擬機器的大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c3136-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="c3136-143">檢閱 hello 使用進階儲存體和選擇 hello 最適當的 VM 大小最適合您的工作負載的虛擬機器的效能特性。</span><span class="sxs-lookup"><span data-stu-id="c3136-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="c3136-144">請確定有足夠的頻寬可用的 VM toodrive hello 磁碟流量。</span><span class="sxs-lookup"><span data-stu-id="c3136-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="c3136-145">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="c3136-145">Disk sizes</span></span>
<span data-ttu-id="c3136-146">有五種類型的磁碟可以搭配您的 VM 使用，而且每種都有特定的 IOP 和輸送量限制。</span><span class="sxs-lookup"><span data-stu-id="c3136-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="c3136-147">請考量這些限制時選擇您的 VM hello 磁碟類型根據 hello 產能、 效能、 延展性方面的應用程式需求和尖峰負載。</span><span class="sxs-lookup"><span data-stu-id="c3136-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="c3136-148">進階磁碟類型</span><span class="sxs-lookup"><span data-stu-id="c3136-148">Premium Disks Type</span></span>  | <span data-ttu-id="c3136-149">P10</span><span class="sxs-lookup"><span data-stu-id="c3136-149">P10</span></span>   | <span data-ttu-id="c3136-150">P20</span><span class="sxs-lookup"><span data-stu-id="c3136-150">P20</span></span>   | <span data-ttu-id="c3136-151">P30</span><span class="sxs-lookup"><span data-stu-id="c3136-151">P30</span></span>            | <span data-ttu-id="c3136-152">P40</span><span class="sxs-lookup"><span data-stu-id="c3136-152">P40</span></span>            | <span data-ttu-id="c3136-153">P50</span><span class="sxs-lookup"><span data-stu-id="c3136-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="c3136-154">磁碟大小</span><span class="sxs-lookup"><span data-stu-id="c3136-154">Disk size</span></span>           | <span data-ttu-id="c3136-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="c3136-155">128 GB</span></span>| <span data-ttu-id="c3136-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="c3136-156">512 GB</span></span>| <span data-ttu-id="c3136-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="c3136-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="c3136-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="c3136-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="c3136-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="c3136-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="c3136-160">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="c3136-160">IOPS per disk</span></span>       | <span data-ttu-id="c3136-161">500</span><span class="sxs-lookup"><span data-stu-id="c3136-161">500</span></span>   | <span data-ttu-id="c3136-162">2300</span><span class="sxs-lookup"><span data-stu-id="c3136-162">2300</span></span>  | <span data-ttu-id="c3136-163">5000</span><span class="sxs-lookup"><span data-stu-id="c3136-163">5000</span></span>           | <span data-ttu-id="c3136-164">7500</span><span class="sxs-lookup"><span data-stu-id="c3136-164">7500</span></span>           | <span data-ttu-id="c3136-165">7500</span><span class="sxs-lookup"><span data-stu-id="c3136-165">7500</span></span>           | 
| <span data-ttu-id="c3136-166">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="c3136-166">Throughput per disk</span></span> | <span data-ttu-id="c3136-167">每秒 100 MB</span><span class="sxs-lookup"><span data-stu-id="c3136-167">100 MB per second</span></span> | <span data-ttu-id="c3136-168">每秒 150 MB</span><span class="sxs-lookup"><span data-stu-id="c3136-168">150 MB per second</span></span> | <span data-ttu-id="c3136-169">每秒 200 MB</span><span class="sxs-lookup"><span data-stu-id="c3136-169">200 MB per second</span></span> | <span data-ttu-id="c3136-170">每秒 250 MB</span><span class="sxs-lookup"><span data-stu-id="c3136-170">250 MB per second</span></span> | <span data-ttu-id="c3136-171">每秒 250 MB</span><span class="sxs-lookup"><span data-stu-id="c3136-171">250 MB per second</span></span> |

<span data-ttu-id="c3136-172">根據您的工作負載，決定您的 VM 是否需要額外的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="c3136-173">您可以附加數個永續性資料磁碟 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="c3136-174">如有需要您可以等量分割跨 hello 磁碟 tooincrease hello 容量和效能的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c3136-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="c3136-175">(請參閱[這裡](storage-premium-storage-performance.md#disk-striping)的磁碟等量化說明。)如果您使用[儲存空間][4]等量進階儲存體資料磁碟，應該對所使用的每個磁碟中的每個資料行進行設定。</span><span class="sxs-lookup"><span data-stu-id="c3136-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="c3136-176">否則，hello 整體 hello 等量磁碟區的效能可能會低於預期到期 toouneven 流量分散在 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="c3136-177">適用於 Linux Vm，您可以使用 hello *mdadm*公用程式 tooachieve hello 相同。</span><span class="sxs-lookup"><span data-stu-id="c3136-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="c3136-178">如需詳細資訊，請參閱文章 [在 Linux 上設定軟體 RAID](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 。</span><span class="sxs-lookup"><span data-stu-id="c3136-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="c3136-179">儲存體帳戶延展性目標</span><span class="sxs-lookup"><span data-stu-id="c3136-179">Storage account scalability targets</span></span>
<span data-ttu-id="c3136-180">進階儲存體帳戶有下列加法 toohello 中的延展性目標的 hello [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="c3136-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="c3136-181">如果應用程式的需求超過單一儲存體帳戶的 hello 延展性目標時，建置您的應用程式 toouse 多個儲存體帳戶，並分割這些儲存體帳戶間的資料。</span><span class="sxs-lookup"><span data-stu-id="c3136-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="c3136-182">總帳戶容量</span><span class="sxs-lookup"><span data-stu-id="c3136-182">Total Account Capacity</span></span> | <span data-ttu-id="c3136-183">本地備援儲存體帳戶總頻寬</span><span class="sxs-lookup"><span data-stu-id="c3136-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="c3136-184">磁碟容量：35 TB</span><span class="sxs-lookup"><span data-stu-id="c3136-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="c3136-185">快照容量：10 TB</span><span class="sxs-lookup"><span data-stu-id="c3136-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="c3136-186">設定輸入 + 輸出每秒的 too50 gb</span><span class="sxs-lookup"><span data-stu-id="c3136-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="c3136-187">如 hello 高階儲存體規格的詳細資訊，請簽出[延展性和效能目標時使用進階儲存體](storage-premium-storage.md#scalability-and-performance-targets)。</span><span class="sxs-lookup"><span data-stu-id="c3136-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="c3136-188">磁碟快取原則</span><span class="sxs-lookup"><span data-stu-id="c3136-188">Disk caching policy</span></span>
<span data-ttu-id="c3136-189">根據預設，快取原則的磁碟是*唯讀*針對所有 hello 高階資料磁碟，和*讀寫*hello Premium 作業系統磁碟附加 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="c3136-190">此組態設定，建議您使用 IOs 應用程式的 tooachieve hello 達到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="c3136-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="c3136-191">對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="c3136-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="c3136-192">可以使用更新現有的資料磁碟的 hello 快取設定[Azure 入口網站](https://portal.azure.com)或 hello *-HostCaching* hello 參數*Set-azuredatadisk* cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c3136-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="c3136-193">位置</span><span class="sxs-lookup"><span data-stu-id="c3136-193">Location</span></span>
<span data-ttu-id="c3136-194">挑選 Azure 進階儲存體可用的位置。</span><span class="sxs-lookup"><span data-stu-id="c3136-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="c3136-195">如需可使用 Azure 服務之地點的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。</span><span class="sxs-lookup"><span data-stu-id="c3136-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="c3136-196">Vm 位於 hello 相同為 hello 的 hello VM 會提供較佳的效能比如果它們位於不同的區域儲存區，hello 磁碟的儲存體帳戶地區。</span><span class="sxs-lookup"><span data-stu-id="c3136-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="c3136-197">其他 Azure VM 組態設定</span><span class="sxs-lookup"><span data-stu-id="c3136-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="c3136-198">建立 Azure VM 時，您將會詢問 tooconfigure 特定 VM 設定。</span><span class="sxs-lookup"><span data-stu-id="c3136-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="c3136-199">請記住，一些設定固定 hello 存留期的 hello VM，而您可以修改，或稍後新增其他項目。</span><span class="sxs-lookup"><span data-stu-id="c3136-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="c3136-200">檢閱這些 Azure VM 組態設定，並確定這些是適當設定 toomatch 工作負載需求。</span><span class="sxs-lookup"><span data-stu-id="c3136-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="c3136-201">最佳化</span><span class="sxs-lookup"><span data-stu-id="c3136-201">Optimization</span></span>
<span data-ttu-id="c3136-202">[Azure 進階儲存體︰針對高效能進行設計](storage-premium-storage-performance.md)提供使用 Azure 進階儲存體來建置高效能應用程式的指導方針。</span><span class="sxs-lookup"><span data-stu-id="c3136-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="c3136-203">您可以遵循 hello 結合效能最佳作法適用於 tootechnologies 應用程式所使用的指導方針。</span><span class="sxs-lookup"><span data-stu-id="c3136-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="c3136-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>準備和複製虛擬硬碟 (Vhd) tooPremium 儲存體</span><span class="sxs-lookup"><span data-stu-id="c3136-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="c3136-205">hello 之後 > 一節提供準備從您的 VM 的 Vhd 和複製 Vhd tooAzure 儲存體的指導方針。</span><span class="sxs-lookup"><span data-stu-id="c3136-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="c3136-206">案例 1: 「 我正在移轉現有的 Azure Vm tooAzure 高階儲存體。 」</span><span class="sxs-lookup"><span data-stu-id="c3136-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="c3136-207">案例 2: 「 我正在移轉 Vm 從其他平台 tooAzure 高階儲存體。 」</span><span class="sxs-lookup"><span data-stu-id="c3136-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="c3136-208">必要條件</span><span class="sxs-lookup"><span data-stu-id="c3136-208">Prerequisites</span></span>
<span data-ttu-id="c3136-209">tooprepare hello Vhd 進行移轉，您將需要：</span><span class="sxs-lookup"><span data-stu-id="c3136-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="c3136-210">Azure 訂用帳戶、 儲存體帳戶和該儲存體容器中的帳戶 toowhich 您可以複製您的 VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="c3136-211">請注意 hello 目的地儲存體帳戶可以依照個人需求的 Standard 或 Premium 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3136-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="c3136-212">工具 toogeneralize hello VHD，如果您計劃 toocreate 從它的多個 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3136-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="c3136-213">例如，適用於 Windows 的 sysprep 或適用於 Ubuntu 的 virt-sysprep。</span><span class="sxs-lookup"><span data-stu-id="c3136-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="c3136-214">工具 tooupload hello VHD 檔案 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3136-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="c3136-215">請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)或使用[Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c3136-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="c3136-216">本指南說明複製 VHD 使用 hello AzCopy 工具。</span><span class="sxs-lookup"><span data-stu-id="c3136-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="c3136-217">如果您選擇使用 AzCopy，以獲得最佳效能的同步複本選項複製 VHD 從 Azure VM 中 hello 執行這些工具的其中一個 hello 目的地儲存體帳戶與相同的區域。</span><span class="sxs-lookup"><span data-stu-id="c3136-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="c3136-218">如果從不同區域的 Azure VM 複製 VHD，您的效能可能會變慢。</span><span class="sxs-lookup"><span data-stu-id="c3136-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="c3136-219">透過有限頻寬中複製大量資料，請考慮[使用 hello Azure 匯入/匯出服務 tootransfer 資料 tooBlob 儲存體](../storage-import-export-service.md); 這可讓您 tootransfer 傳送硬碟資料磁碟機 tooan Azure資料中心。</span><span class="sxs-lookup"><span data-stu-id="c3136-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](../storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="c3136-220">您可以使用 Azure 匯入/匯出服務 toocopy 資料 tooa 標準儲存體帳戶只 hello。</span><span class="sxs-lookup"><span data-stu-id="c3136-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="c3136-221">一旦 hello 資料是在標準儲存體帳戶，您可以使用任一 hello[複製 Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx)或 AzCopy tootransfer hello 資料 tooyour 進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3136-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="c3136-222">請注意，Microsoft Azure 僅支援固定大小的 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="c3136-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="c3136-223">不支援 VHDX 檔案或動態 VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="c3136-224">如果您有動態 VHD，您可以將它轉換使用 hello toofixed 大小[CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c3136-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="c3136-225"><a name="scenario1"></a>案例 1: 「 我正在移轉現有的 Azure Vm tooAzure 高階儲存體。 」</span><span class="sxs-lookup"><span data-stu-id="c3136-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="c3136-226">如果您要移轉現有的 Azure Vm，停止 hello VM，準備 Vhd，每個您想，VHD 的 hello 類型，然後複製 hello VHD 利用 AzCopy 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c3136-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="c3136-227">hello VM 需要 toobe 完全關閉 toomigrate 乾淨的狀態。</span><span class="sxs-lookup"><span data-stu-id="c3136-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="c3136-228">Hello 移轉作業完成之前，將會中斷。</span><span class="sxs-lookup"><span data-stu-id="c3136-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="c3136-229">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="c3136-229">Step 1.</span></span> <span data-ttu-id="c3136-230">準備 VHD 進行移轉</span><span class="sxs-lookup"><span data-stu-id="c3136-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="c3136-231">如果您要移轉現有的 Azure Vm tooPremium 存放裝置，可能是您的 VHD:</span><span class="sxs-lookup"><span data-stu-id="c3136-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="c3136-232">一般化作業系統映像</span><span class="sxs-lookup"><span data-stu-id="c3136-232">A generalized operating system image</span></span>
* <span data-ttu-id="c3136-233">唯一的作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="c3136-233">A unique operating system disk</span></span>
* <span data-ttu-id="c3136-234">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="c3136-234">A data disk</span></span>

<span data-ttu-id="c3136-235">下面將逐步解說準備 VHD 的 3 個案例。</span><span class="sxs-lookup"><span data-stu-id="c3136-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="c3136-236">使用一般化的作業系統 VHD toocreate 多個 VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="c3136-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="c3136-237">如果您要上傳的 VHD，將會使用的 toocreate 多個一般的 Azure VM 執行個體，您必須先一般化 VHD 使用 sysprep 公用程式。</span><span class="sxs-lookup"><span data-stu-id="c3136-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="c3136-238">這適用於 tooa 是在內部部署的 VHD 或 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="c3136-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="c3136-239">Sysprep 會移除 hello VHD 中的任何電腦特定的資訊。</span><span class="sxs-lookup"><span data-stu-id="c3136-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3136-240">將 VM 一般化之前，請先擷取快照或備份。</span><span class="sxs-lookup"><span data-stu-id="c3136-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="c3136-241">執行 sysprep 將會停止並取消配置 hello VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3136-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="c3136-242">請遵循以下 toosysprep Windows OS VHD 的步驟。</span><span class="sxs-lookup"><span data-stu-id="c3136-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="c3136-243">請注意，執行 hello Sysprep 命令將會要求您 tooshut 關閉 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c3136-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="c3136-244">如需 Sysprep 的詳細資訊，請參閱 [Sysprep 概觀](http://technet.microsoft.com/library/hh825209.aspx)或 [Sysprep 技術參考](http://technet.microsoft.com/library/cc766049.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c3136-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="c3136-245">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="c3136-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="c3136-246">輸入下列命令 tooopen Sysprep hello:</span><span class="sxs-lookup"><span data-stu-id="c3136-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="c3136-247">Hello 系統準備工具，在選取進入系統的全新體驗 (OOBE)，選取 hello 一般化核取方塊，選取**關機**，然後按一下**確定**hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="c3136-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="c3136-248">Sysprep 會一般化 hello 作業系統，並關閉 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="c3136-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="c3136-249">Ubuntu vm，使用 virt sysprep tooachieve hello 相同。</span><span class="sxs-lookup"><span data-stu-id="c3136-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="c3136-250">如需詳細資訊，請參閱 [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) 。</span><span class="sxs-lookup"><span data-stu-id="c3136-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="c3136-251">另請參閱 hello 開放原始碼的某些[佈建的 Linux 伺服器軟體](http://www.cyberciti.biz/tips/server-provisioning-software.html)針對其他 Linux 作業系統。</span><span class="sxs-lookup"><span data-stu-id="c3136-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="c3136-252">使用唯一的作業系統 VHD toocreate 單一 VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="c3136-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="c3136-253">如果您有 hello 的 vm 需要 hello 機器特定資料上執行的應用程式時，請勿一般化 hello VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="c3136-254">非一般化的 VHD 可以是使用的 toocreate 唯一的 Azure VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3136-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="c3136-255">例如，如果您的 VHD 上有網域控制站，執行 sysprep 將會使它與網域控制站一樣沒有效率。</span><span class="sxs-lookup"><span data-stu-id="c3136-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="c3136-256">檢閱 hello 上 VM 與 hello 影響您在其上執行 sysprep 一般化 hello VHD 之前執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3136-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="c3136-257">註冊資料磁碟 VHD</span><span class="sxs-lookup"><span data-stu-id="c3136-257">Register data disk VHD</span></span>
<span data-ttu-id="c3136-258">如果您有 Azure toobe 中的資料磁碟移轉，您必須先確定 hello Vm 使用這些磁碟都已關閉的資料。</span><span class="sxs-lookup"><span data-stu-id="c3136-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="c3136-259">請依照下述 toocopy VHD tooAzure 高階儲存體的 hello 步驟並註冊為佈建的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="c3136-260">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="c3136-260">Step 2.</span></span> <span data-ttu-id="c3136-261">建立 VHD 的 hello 目的地</span><span class="sxs-lookup"><span data-stu-id="c3136-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="c3136-262">建立儲存體帳戶來維護您的 VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="c3136-263">請考慮下列點的規劃位置時的 hello toostore 您的 Vhd:</span><span class="sxs-lookup"><span data-stu-id="c3136-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="c3136-264">hello 目標進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3136-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="c3136-265">hello 儲存體帳戶位置必須是相同高階儲存體在 hello 最後階段中，您將建立能夠 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="c3136-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="c3136-266">您無法複製 tooa 新的儲存體帳戶或計劃 toouse hello 相同儲存體帳戶會根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="c3136-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="c3136-267">複製並儲存 hello 儲存體帳戶金鑰的 hello 目的地儲存體帳戶的 hello 下一個階段。</span><span class="sxs-lookup"><span data-stu-id="c3136-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="c3136-268">針對資料磁碟，您可以選擇 tookeep 某些資料磁碟標準儲存體帳戶 （例如，磁碟有溫度更低的儲存體），但我們強烈建議您移動生產工作負載 toouse premium 儲存體的所有資料。</span><span class="sxs-lookup"><span data-stu-id="c3136-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="c3136-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>步驟 3.</span><span class="sxs-lookup"><span data-stu-id="c3136-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="c3136-270">使用 AzCopy 或 PowerShell 複製 VHD</span><span class="sxs-lookup"><span data-stu-id="c3136-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="c3136-271">您將需要 toofind 容器路徑及儲存體帳戶金鑰 tooprocess 這兩個選項之一。</span><span class="sxs-lookup"><span data-stu-id="c3136-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="c3136-272">容器路徑和儲存體帳戶金鑰位於 **Azure 入口網站** > **儲存體**。</span><span class="sxs-lookup"><span data-stu-id="c3136-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="c3136-273">hello 容器 URL 會類似"https://myaccount.blob.core.windows.net/mycontainer/"。</span><span class="sxs-lookup"><span data-stu-id="c3136-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="c3136-274">選項 1︰使用 AzCopy 複製 VHD (非同步複製)</span><span class="sxs-lookup"><span data-stu-id="c3136-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="c3136-275">使用 AzCopy，您可以輕鬆地上載透過 hello 網際網路 hello VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="c3136-276">Hello hello Vhd 大小而定，這可能需要時間。</span><span class="sxs-lookup"><span data-stu-id="c3136-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="c3136-277">使用此選項時，請記住 toocheck hello 儲存體帳戶入口/出口限制。</span><span class="sxs-lookup"><span data-stu-id="c3136-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="c3136-278">如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) 。</span><span class="sxs-lookup"><span data-stu-id="c3136-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="c3136-279">從這裡下載並安裝 AzCopy： [AzCopy 的最新版本](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="c3136-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="c3136-280">開啟 Azure PowerShell，並移 toohello AzCopy 安裝所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c3136-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="c3136-281">使用 hello 下列命令 toocopy hello VHD 檔案從 「 來源 」 太 「 目的地 」。</span><span class="sxs-lookup"><span data-stu-id="c3136-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="c3136-282">範例：</span><span class="sxs-lookup"><span data-stu-id="c3136-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="c3136-283">以下是 hello AzCopy 命令中使用的 hello 參數的描述：</span><span class="sxs-lookup"><span data-stu-id="c3136-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="c3136-284">**/ 來源： *&lt;來源&gt;:***  hello 資料夾或包含 hello VHD 的儲存體容器 URL 的位置。</span><span class="sxs-lookup"><span data-stu-id="c3136-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="c3136-285">**/ SourceKey: *&lt;來源帳戶金鑰&gt;:***  hello 來源儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c3136-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="c3136-286">**/ 目的地： *&lt;目的地&gt;:*** 儲存體容器 URL toocopy hello VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="c3136-287">**/ DestKey: *&lt;目的地帳戶金鑰&gt;:***  hello 目的地儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c3136-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="c3136-288">**/ 模式： *&lt;檔案名稱&gt;:***  hello VHD toocopy 指定 hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="c3136-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="c3136-289">如需詳細資訊，使用 AzCopy 工具，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="c3136-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="c3136-290">選項 2：使用 PowerShell 複製 VHD (同步處理的複製)</span><span class="sxs-lookup"><span data-stu-id="c3136-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="c3136-291">您也可以複製使用 hello PowerShell cmdlet 開始 AzureStorageBlobCopy hello VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="c3136-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="c3136-292">使用下列命令，在 Azure PowerShell toocopy VHD 上的 hello。</span><span class="sxs-lookup"><span data-stu-id="c3136-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="c3136-293">取代 hello <> 的來源和目的地儲存體帳戶中的對應值。</span><span class="sxs-lookup"><span data-stu-id="c3136-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="c3136-294">此命令時，您必須在目的地儲存體帳戶中稱為 vhd 容器 toouse。</span><span class="sxs-lookup"><span data-stu-id="c3136-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="c3136-295">如果 hello 容器不存在，建立一個執行 hello 命令之前。</span><span class="sxs-lookup"><span data-stu-id="c3136-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="c3136-296">範例：</span><span class="sxs-lookup"><span data-stu-id="c3136-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="c3136-297"><a name="scenario2"></a>案例 2: 「 我正在移轉 Vm 從其他平台 tooAzure 高階儲存體。 」</span><span class="sxs-lookup"><span data-stu-id="c3136-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="c3136-298">如果您從非 Azure 雲端儲存體 tooAzure 移轉 VHD，您必須先匯出 hello VHD tooa 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="c3136-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="c3136-299">Hello 完整的來源路徑的 VHD 儲存位置很方便，hello 本機目錄，然後再使用 AzCopy tooupload 它 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c3136-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="c3136-300">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="c3136-300">Step 1.</span></span> <span data-ttu-id="c3136-301">匯出 VHD tooa 本機目錄</span><span class="sxs-lookup"><span data-stu-id="c3136-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="c3136-302">從 AWS 複製 VHD</span><span class="sxs-lookup"><span data-stu-id="c3136-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="c3136-303">如果您使用 AWS，匯出 hello EC2 執行個體 tooa Amazon S3 貯體中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="c3136-304">請遵循 hello hello Amazon 匯出 Amazon EC2 執行個體 tooinstall hello Amazon EC2 命令列介面 (CLI) 工具的文件中所述的步驟，並執行 hello 建立執行個體-匯出的工作命令 tooexport hello EC2 執行個體 tooa VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="c3136-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="c3136-305">要確定 toouse **VHD** hello 磁碟 #95; 映像 &#95;格式的變數時執行 hello**建立執行個體-匯出的工作**命令。</span><span class="sxs-lookup"><span data-stu-id="c3136-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="c3136-306">hello 匯出的 VHD 檔案會儲存在您指定在此過程中的 hello Amazon S3 貯體。</span><span class="sxs-lookup"><span data-stu-id="c3136-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="c3136-307">Hello VHD 檔案下載從 hello S3 貯體。</span><span class="sxs-lookup"><span data-stu-id="c3136-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="c3136-308">選取 hello VHD 檔案，然後**動作** > **下載**。</span><span class="sxs-lookup"><span data-stu-id="c3136-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="c3136-309">從其他非 Azure 雲端複製 VHD</span><span class="sxs-lookup"><span data-stu-id="c3136-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="c3136-310">如果您從非 Azure 雲端儲存體 tooAzure 移轉 VHD，您必須先匯出 hello VHD tooa 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="c3136-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="c3136-311">複製 hello 本機目錄儲存 VHD 的 hello 完整的來源的路徑。</span><span class="sxs-lookup"><span data-stu-id="c3136-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="c3136-312">從內部部署複製 VHD</span><span class="sxs-lookup"><span data-stu-id="c3136-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="c3136-313">如果您要移轉 VHD 從內部部署環境，您必須儲存 VHD 的 hello 完整的來源路徑。</span><span class="sxs-lookup"><span data-stu-id="c3136-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="c3136-314">hello 來源路徑可能是伺服器位置或檔案共用。</span><span class="sxs-lookup"><span data-stu-id="c3136-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="c3136-315">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="c3136-315">Step 2.</span></span> <span data-ttu-id="c3136-316">建立 VHD 的 hello 目的地</span><span class="sxs-lookup"><span data-stu-id="c3136-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="c3136-317">建立儲存體帳戶來維護您的 VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="c3136-318">請考慮下列點的規劃位置時的 hello toostore 您的 Vhd:</span><span class="sxs-lookup"><span data-stu-id="c3136-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="c3136-319">hello 目標儲存體帳戶可能是根據您的應用程式需求的標準或進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="c3136-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="c3136-320">hello 儲存體帳戶區域必須是相同高階儲存體在 hello 最後階段中，您將建立能夠 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="c3136-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="c3136-321">您無法複製 tooa 新的儲存體帳戶或計劃 toouse hello 相同儲存體帳戶會根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="c3136-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="c3136-322">複製並儲存 hello 儲存體帳戶金鑰的 hello 目的地儲存體帳戶的 hello 下一個階段。</span><span class="sxs-lookup"><span data-stu-id="c3136-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="c3136-323">我們強烈建議您移動生產工作負載 toouse premium 儲存體的所有資料。</span><span class="sxs-lookup"><span data-stu-id="c3136-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="c3136-324">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="c3136-324">Step 3.</span></span> <span data-ttu-id="c3136-325">上傳 hello VHD tooAzure 儲存體</span><span class="sxs-lookup"><span data-stu-id="c3136-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="c3136-326">現在，您會將您的 VHD 在 hello 本機目錄，您可以使用 AzCopy 或 AzurePowerShell tooupload hello.vhd 檔案 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c3136-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="c3136-327">下面提供兩個選項︰</span><span class="sxs-lookup"><span data-stu-id="c3136-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="c3136-328">選項 1： 使用 Azure PowerShell Add-azurevhd tooupload hello.vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="c3136-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="c3136-329">範例 <Uri> 可能是 ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***。</span><span class="sxs-lookup"><span data-stu-id="c3136-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="c3136-330">範例 <FileInfo> 可能是 ***"C:\path\to\upload.vhd"***。</span><span class="sxs-lookup"><span data-stu-id="c3136-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="c3136-331">選項 2： 使用 AzCopy tooupload hello.vhd 檔案</span><span class="sxs-lookup"><span data-stu-id="c3136-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="c3136-332">使用 AzCopy，您可以輕鬆地上載透過 hello 網際網路 hello VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="c3136-333">Hello hello Vhd 大小而定，這可能需要時間。</span><span class="sxs-lookup"><span data-stu-id="c3136-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="c3136-334">使用此選項時，請記住 toocheck hello 儲存體帳戶入口/出口限制。</span><span class="sxs-lookup"><span data-stu-id="c3136-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="c3136-335">如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) 。</span><span class="sxs-lookup"><span data-stu-id="c3136-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="c3136-336">從這裡下載並安裝 AzCopy： [AzCopy 的最新版本](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="c3136-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="c3136-337">開啟 Azure PowerShell，並移 toohello AzCopy 安裝所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c3136-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="c3136-338">使用 hello 下列命令 toocopy hello VHD 檔案從 「 來源 」 太 「 目的地 」。</span><span class="sxs-lookup"><span data-stu-id="c3136-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="c3136-339">範例：</span><span class="sxs-lookup"><span data-stu-id="c3136-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="c3136-340">以下是 hello AzCopy 命令中使用的 hello 參數的描述：</span><span class="sxs-lookup"><span data-stu-id="c3136-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="c3136-341">**/ 來源： *&lt;來源&gt;:***  hello 資料夾或包含 hello VHD 的儲存體容器 URL 的位置。</span><span class="sxs-lookup"><span data-stu-id="c3136-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="c3136-342">**/ SourceKey: *&lt;來源帳戶金鑰&gt;:***  hello 來源儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c3136-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="c3136-343">**/ 目的地： *&lt;目的地&gt;:*** 儲存體容器 URL toocopy hello VHD。</span><span class="sxs-lookup"><span data-stu-id="c3136-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="c3136-344">**/ DestKey: *&lt;目的地帳戶金鑰&gt;:***  hello 目的地儲存體帳戶的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="c3136-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="c3136-345">**/ BlobType： 頁面：**指定該 hello 目的地是分頁 blob。</span><span class="sxs-lookup"><span data-stu-id="c3136-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="c3136-346">**/ 模式： *&lt;檔案名稱&gt;:***  hello VHD toocopy 指定 hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="c3136-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="c3136-347">如需詳細資訊，使用 AzCopy 工具，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="c3136-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="c3136-348">上傳 VHD 的其他選項</span><span class="sxs-lookup"><span data-stu-id="c3136-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="c3136-349">您也可以上傳 VHD tooyour 儲存體帳戶使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="c3136-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="c3136-350">Azure 儲存體複製 Blob API</span><span class="sxs-lookup"><span data-stu-id="c3136-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="c3136-351">Azure 儲存體總管上傳 Blob</span><span class="sxs-lookup"><span data-stu-id="c3136-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="c3136-352">儲存體匯入/匯出服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="c3136-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="c3136-353">如果預估的上傳時間長度超過 7 天，我們建議使用匯入/匯出服務。</span><span class="sxs-lookup"><span data-stu-id="c3136-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="c3136-354">您可以使用[DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello 時間資料的大小和傳輸的單位。</span><span class="sxs-lookup"><span data-stu-id="c3136-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="c3136-355">可以匯入/匯出用 toocopy tooa 標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3136-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="c3136-356">您必須從標準儲存體 toopremium 儲存體帳戶，使用 AzCopy 這類工具 toocopy。</span><span class="sxs-lookup"><span data-stu-id="c3136-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="c3136-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>使用進階儲存體建立 Azure VM</span><span class="sxs-lookup"><span data-stu-id="c3136-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="c3136-358">Hello VHD 上傳或複製 toohello 需要儲存體帳戶之後，請遵循此節 tooregister hello VHD 中的 hello 指示做為作業系統映像或根據您的案例的作業系統磁碟，然後從它建立的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3136-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="c3136-359">hello 資料磁碟 VHD 可以附加的 toohello VM 建立之後。</span><span class="sxs-lookup"><span data-stu-id="c3136-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="c3136-360">本節的 hello 結尾會提供範例移轉指令碼。</span><span class="sxs-lookup"><span data-stu-id="c3136-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="c3136-361">這個簡單的指令碼不符合所有案例。</span><span class="sxs-lookup"><span data-stu-id="c3136-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="c3136-362">您可能需要 tooupdate hello 指令碼 toomatch 與您特定案例。</span><span class="sxs-lookup"><span data-stu-id="c3136-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="c3136-363">toosee 如果此指令碼適用於 tooyour 案例中，請參閱下面的[範例移轉指令碼](#a-sample-migration-script)。</span><span class="sxs-lookup"><span data-stu-id="c3136-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="c3136-364">檢查清單</span><span class="sxs-lookup"><span data-stu-id="c3136-364">Checklist</span></span>
1. <span data-ttu-id="c3136-365">等候所有 hello VHD 磁碟複製已完成。</span><span class="sxs-lookup"><span data-stu-id="c3136-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="c3136-366">請確認您要移轉至 hello 區域中，進階儲存體可供使用。</span><span class="sxs-lookup"><span data-stu-id="c3136-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="c3136-367">決定 hello 您要將新 VM 系列。</span><span class="sxs-lookup"><span data-stu-id="c3136-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="c3136-368">它應該是支援、 高階儲存體，而 hello 大小應該根據 hello 區域中的 hello 可用性並根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="c3136-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="c3136-369">決定 hello 您將使用完全 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="c3136-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="c3136-370">VM 大小需要 toobe 夠大 toosupport hello 您擁有的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="c3136-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="c3136-371">例如</span><span class="sxs-lookup"><span data-stu-id="c3136-371">E.g.</span></span> <span data-ttu-id="c3136-372">如果您有 4 個資料磁碟，hello VM 必須有 2 個以上的核心。</span><span class="sxs-lookup"><span data-stu-id="c3136-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="c3136-373">也請考慮處理能力、記憶體和網路頻寬需求。</span><span class="sxs-lookup"><span data-stu-id="c3136-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="c3136-374">Hello 目標區域中建立進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3136-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="c3136-375">這是您將用於 hello hello 帳戶新的 VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="c3136-376">有 hello 目前 VM 詳細資料很方便，包括 hello 磁碟清單及其對應的 VHD blob。</span><span class="sxs-lookup"><span data-stu-id="c3136-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="c3136-377">為您的應用程式做好停機準備。</span><span class="sxs-lookup"><span data-stu-id="c3136-377">Prepare your application for downtime.</span></span> <span data-ttu-id="c3136-378">toodo 全新的移轉，您必須 toostop 所有 hello 處理 hello 目前系統中。</span><span class="sxs-lookup"><span data-stu-id="c3136-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="c3136-379">唯有如此，您可以取得它 tooconsistent 狀態，您可以移轉 toohello 新的平台。</span><span class="sxs-lookup"><span data-stu-id="c3136-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="c3136-380">停機持續時間將取決於 hello hello 磁碟 toomigrate 中的資料數量。</span><span class="sxs-lookup"><span data-stu-id="c3136-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="c3136-381">如果您要從特定的 VHD 磁碟建立 Azure 資源管理員 VM，請參閱太[此範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)部署使用現有的磁碟資源管理員 VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="c3136-382">註冊 VHD</span><span class="sxs-lookup"><span data-stu-id="c3136-382">Register your VHD</span></span>
<span data-ttu-id="c3136-383">將 VM 從 OS VHD 或 tooattach 資料磁碟 tooa toocreate 新的 VM，您必須先註冊它們。</span><span class="sxs-lookup"><span data-stu-id="c3136-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="c3136-384">根據您的 VHD 案例，遵循以下步驟。</span><span class="sxs-lookup"><span data-stu-id="c3136-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="c3136-385">一般化作業系統 VHD toocreate 多個 Azure VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="c3136-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="c3136-386">一般化的作業系統映像的 VHD 是上傳 toohello 儲存體帳戶之後，註冊為**Azure VM 映像**，讓您可以從它建立一個或多個 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3136-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="c3136-387">使用下列 PowerShell cmdlet tooregister hello VHD 做為 Azure VM 的 OS 映像。</span><span class="sxs-lookup"><span data-stu-id="c3136-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="c3136-388">提供 VHD 複製到其中的 hello 完整容器 URL。</span><span class="sxs-lookup"><span data-stu-id="c3136-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="c3136-389">複製並儲存 hello 這個新的 Azure VM 映像名稱。</span><span class="sxs-lookup"><span data-stu-id="c3136-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="c3136-390">在 hello 上述範例中，它是*OSImageName*。</span><span class="sxs-lookup"><span data-stu-id="c3136-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="c3136-391">唯一的作業系統 VHD toocreate 單一 Azure VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="c3136-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="c3136-392">Hello 唯一 OS VHD 後上傳的 toohello 儲存體帳戶，做為其註冊**Azure 作業系統磁碟**，讓您可以從它建立的 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3136-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="c3136-393">使用這些 PowerShell cmdlet tooregister VHD 當做 Azure 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="c3136-394">提供 VHD 複製到其中的 hello 完整容器 URL。</span><span class="sxs-lookup"><span data-stu-id="c3136-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="c3136-395">複製並儲存 hello 這個新的 Azure 作業系統磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="c3136-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="c3136-396">在 hello 上述範例中，它是*OSDisk*。</span><span class="sxs-lookup"><span data-stu-id="c3136-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="c3136-397">資料磁碟 VHD toobe 附加 toonew Azure VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="c3136-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="c3136-398">Hello 資料磁碟，vhd 上傳 toostorage 帳戶之後，其註冊為 Azure 資料磁碟，讓它可以是附加的 tooyour 新 DS 系列、 DSv2 系列或 GS 系列 Azure VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3136-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="c3136-399">使用這些 PowerShell cmdlet tooregister VHD 當做 Azure 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="c3136-400">提供 VHD 複製到其中的 hello 完整容器 URL。</span><span class="sxs-lookup"><span data-stu-id="c3136-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="c3136-401">複製並儲存 hello 這個新的 Azure 資料磁碟的名稱。</span><span class="sxs-lookup"><span data-stu-id="c3136-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="c3136-402">在 hello 上述範例中，它是*DataDisk*。</span><span class="sxs-lookup"><span data-stu-id="c3136-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="c3136-403">建立可支援進階儲存體的 VM</span><span class="sxs-lookup"><span data-stu-id="c3136-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="c3136-404">一次 hello OS 映像或作業系統磁碟會註冊，建立新的 DS 系列、 DSv2 系列或 GS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="c3136-405">您將使用 hello 作業系統映像或作業系統磁碟名稱註冊。</span><span class="sxs-lookup"><span data-stu-id="c3136-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="c3136-406">從 hello 高階儲存體層選取 hello VM 類型。</span><span class="sxs-lookup"><span data-stu-id="c3136-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="c3136-407">在下列範例中，我們會使用 hello *Standard_DS2* VM 大小。</span><span class="sxs-lookup"><span data-stu-id="c3136-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="c3136-408">更新 hello 磁碟大小 toomake 確定它符合您的容量和效能需求和 hello 可用的 Azure 磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="c3136-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="c3136-409">遵循以下 toocreate hello 逐步解說 PowerShell cmdlet hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="c3136-410">首先，設定 hello 一般參數：</span><span class="sxs-lookup"><span data-stu-id="c3136-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="c3136-411">首先，建立您將在當中裝載新 VM 的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c3136-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="c3136-412">接下來，根據您的案例，請從任一 hello 作業系統映像或作業系統磁碟的註冊，讓您建立 hello Azure VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3136-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="c3136-413">一般化作業系統 VHD toocreate 多個 Azure VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="c3136-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="c3136-414">建立一或多個新 DS 系列 Azure VM 執行個體使用 hello hello **Azure OS 映像**您註冊。</span><span class="sxs-lookup"><span data-stu-id="c3136-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="c3136-415">如下所示，建立新的 VM 時，請在 hello VM 組態中指定此作業系統映像名稱。</span><span class="sxs-lookup"><span data-stu-id="c3136-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="c3136-416">唯一的作業系統 VHD toocreate 單一 Azure VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="c3136-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="c3136-417">建立新 DS 系列 Azure VM 執行個體使用 hello **Azure 作業系統磁碟**您註冊。</span><span class="sxs-lookup"><span data-stu-id="c3136-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="c3136-418">當建立 hello 新的 VM，如下所示，請在 hello VM 組態中指定此作業系統磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="c3136-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="c3136-419">指定其他 Azure VM 資訊，例如雲端服務、區域、儲存體帳戶、可用性設定組以及快取原則。</span><span class="sxs-lookup"><span data-stu-id="c3136-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="c3136-420">請注意，hello VM 執行個體必須位於相同位置與相關聯的作業系統或資料磁碟，因此 hello 選取雲端服務、 區域和儲存體帳戶必須是在 hello 與 hello 基礎這些磁碟的 Vhd 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="c3136-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="c3136-421">連結資料磁碟</span><span class="sxs-lookup"><span data-stu-id="c3136-421">Attach data disk</span></span>
<span data-ttu-id="c3136-422">最後，如果您已註冊資料磁碟 Vhd，將它們附加 toohello 新 Premium 儲存體支援 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="c3136-423">使用下列 PowerShell 指令程式 tooattach 資料磁碟 toohello 新的 VM，並指定 hello 快取原則。</span><span class="sxs-lookup"><span data-stu-id="c3136-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="c3136-424">在下例 hello 快取原則設定太*ReadOnly*。</span><span class="sxs-lookup"><span data-stu-id="c3136-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="c3136-425">可能有額外的步驟需要 toosupport 的應用程式不會涵蓋本指南。</span><span class="sxs-lookup"><span data-stu-id="c3136-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="c3136-426">檢查和規劃備份</span><span class="sxs-lookup"><span data-stu-id="c3136-426">Checking and plan backup</span></span>
<span data-ttu-id="c3136-427">一次 hello 新的 VM 已啟動且正在執行，它使用 hello 相同的登入識別碼和密碼的存取為 hello 原始 VM，並確認一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="c3136-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="c3136-428">所有的 hello 設定，包括 hello 等量磁碟區，就會出現在 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="c3136-429">hello 最後一個步驟是 tooplan hello 應用程式的需求為基礎的新 VM 的備份和維護排程。</span><span class="sxs-lookup"><span data-stu-id="c3136-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="c3136-430"><a name="a-sample-migration-script"></a>範例移轉指令碼</span><span class="sxs-lookup"><span data-stu-id="c3136-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="c3136-431">如果您有多個 Vm toomigrate，透過 PowerShell 指令碼自動化會很有用。</span><span class="sxs-lookup"><span data-stu-id="c3136-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="c3136-432">以下是範例指令碼自動化 hello 移轉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c3136-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="c3136-433">請注意，以下的指令碼是只是範例，而且有幾個有關 hello 目前 VM 磁碟所做的假設。</span><span class="sxs-lookup"><span data-stu-id="c3136-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="c3136-434">您可能需要 tooupdate hello 指令碼 toomatch 與您特定案例。</span><span class="sxs-lookup"><span data-stu-id="c3136-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="c3136-435">hello 假設如下：</span><span class="sxs-lookup"><span data-stu-id="c3136-435">hello assumptions are:</span></span>

* <span data-ttu-id="c3136-436">您正在建立傳統 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="c3136-437">您的來源作業系統磁碟和來源資料磁碟位於相同儲存體帳戶和相同容器中。</span><span class="sxs-lookup"><span data-stu-id="c3136-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="c3136-438">如果您的 OS 磁碟和資料磁碟不在 hello 相同放置，您可以使用 AzCopy 或 Azure PowerShell toocopy Vhd 透過儲存體帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="c3136-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="c3136-439">Toohello 上一個步驟，請參閱：[利用 AzCopy 或 PowerShell 的複製 VHD](#copy-vhd-with-azcopy-or-powershell)。</span><span class="sxs-lookup"><span data-stu-id="c3136-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="c3136-440">編輯這個指令碼 toomeet 您的案例是另一個選擇，但建議使用 AzCopy 或 PowerShell，因為它是更方便且快速。</span><span class="sxs-lookup"><span data-stu-id="c3136-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="c3136-441">hello 自動化指令碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="c3136-441">hello automation script is provided below.</span></span> <span data-ttu-id="c3136-442">文字取代成您的資訊並 hello 指令碼 toomatch 以更新您的特定案例。</span><span class="sxs-lookup"><span data-stu-id="c3136-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="c3136-443">使用 hello 現有指令碼不會保存 hello 您來源 VM 網路設定。</span><span class="sxs-lookup"><span data-stu-id="c3136-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="c3136-444">您必須在您移轉的 Vm 上 toore-config hello 網路設定。</span><span class="sxs-lookup"><span data-stu-id="c3136-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
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


    #Check hello Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
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
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="c3136-445"><a name="optimization"></a>最佳化</span><span class="sxs-lookup"><span data-stu-id="c3136-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="c3136-446">目前的 VM 組態可自訂特別 toowork 與標準磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="c3136-447">比方說，tooincrease hello 效能等量磁碟區中使用多個磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="c3136-448">例如，而不是在進階儲存體分別使用 4 個磁碟，您可能會無法 toooptimize hello 成本具有單一磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3136-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="c3136-449">最佳化處理以案例為基礎的這個需求 toobe 等 hello 移轉之後需要自訂的步驟。</span><span class="sxs-lookup"><span data-stu-id="c3136-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="c3136-450">此外，請注意，此程序也不適用於資料庫和應用程式相依於定義 hello 安裝程式中的 hello 磁碟配置。</span><span class="sxs-lookup"><span data-stu-id="c3136-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="c3136-451">準備工作</span><span class="sxs-lookup"><span data-stu-id="c3136-451">Preparation</span></span>
1. <span data-ttu-id="c3136-452">完成 hello hello 中所述的簡單移轉前一節。</span><span class="sxs-lookup"><span data-stu-id="c3136-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="c3136-453">最佳化會對 hello hello 移轉之後的新 VM。</span><span class="sxs-lookup"><span data-stu-id="c3136-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="c3136-454">定義 hello hello 最佳化設定所需新磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="c3136-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="c3136-455">判斷對應的 hello 目前磁碟/磁碟區 toohello 新磁碟的規格。</span><span class="sxs-lookup"><span data-stu-id="c3136-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="c3136-456">執行步驟</span><span class="sxs-lookup"><span data-stu-id="c3136-456">Execution steps</span></span>
1. <span data-ttu-id="c3136-457">建立新的磁碟 hello 與 hello hello Premium 儲存體 VM 上的正確大小。</span><span class="sxs-lookup"><span data-stu-id="c3136-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="c3136-458">登入 toohello VM 與複製 hello 資料從 hello 目前磁碟區 toohello 新磁碟對應 toothat 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c3136-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="c3136-459">所有 hello 目前磁碟區的 toomap tooa 新磁碟才能執行這項都操作。</span><span class="sxs-lookup"><span data-stu-id="c3136-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="c3136-460">接著，變更 hello 應用程式設定 tooswitch toohello 新磁碟，並卸離 hello 舊的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c3136-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="c3136-461">微調 hello 以提升磁碟效能的應用程式，請參閱太[最佳化應用程式效能](storage-premium-storage-performance.md#optimizing-application-performance)。</span><span class="sxs-lookup"><span data-stu-id="c3136-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="c3136-462">應用程式移轉</span><span class="sxs-lookup"><span data-stu-id="c3136-462">Application migrations</span></span>
<span data-ttu-id="c3136-463">資料庫與其他複雜的應用程式可能需要特殊步驟，hello hello 移轉的應用程式提供者所定義。</span><span class="sxs-lookup"><span data-stu-id="c3136-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="c3136-464">請參閱 toorespective 應用程式文件。</span><span class="sxs-lookup"><span data-stu-id="c3136-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="c3136-465">例如</span><span class="sxs-lookup"><span data-stu-id="c3136-465">E.g.</span></span> <span data-ttu-id="c3136-466">資料庫通常可透過備份和還原來移轉。</span><span class="sxs-lookup"><span data-stu-id="c3136-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3136-467">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3136-467">Next steps</span></span>
<span data-ttu-id="c3136-468">請參閱下列資源來移轉虛擬機器的特定案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3136-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="c3136-469">在儲存體帳戶之間移轉 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c3136-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="c3136-470">建立並上傳 Windows Server VHD tooAzure。</span><span class="sxs-lookup"><span data-stu-id="c3136-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="c3136-471">建立和上傳的虛擬硬碟包含 hello Linux 作業系統</span><span class="sxs-lookup"><span data-stu-id="c3136-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="c3136-472">從 Amazon AWS tooMicrosoft Azure 移轉的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c3136-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="c3136-473">另請參閱下列資源 toolearn 深入了解 Azure 儲存體和 Azure 虛擬機器的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3136-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="c3136-474">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="c3136-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="c3136-475">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c3136-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="c3136-476">進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體</span><span class="sxs-lookup"><span data-stu-id="c3136-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
