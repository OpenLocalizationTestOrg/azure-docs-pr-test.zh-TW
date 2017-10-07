---
title: "aaaManage Azure 磁碟以 hello Azure PowerShell |Microsoft 文件"
description: "教學課程-管理以 hello Azure PowerShell 的 Azure 磁碟"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="7ca5e-103">使用 PowerShell 管理 Azure 磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="7ca5e-104">Azure 虛擬機器使用的磁碟 toostore hello Vm 作業系統、 應用程式和資料。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="7ca5e-105">建立 VM 時，重要 toochoose 磁碟大小和設定適當的 toohello 預期工作負載。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="7ca5e-106">本教學課程涵蓋部署和管理 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="7ca5e-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="7ca5e-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ca5e-108">OS 磁碟和暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="7ca5e-109">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-109">Data disks</span></span>
> * <span data-ttu-id="7ca5e-110">標準和進階磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="7ca5e-111">磁碟效能</span><span class="sxs-lookup"><span data-stu-id="7ca5e-111">Disk performance</span></span>
> * <span data-ttu-id="7ca5e-112">連結及準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="7ca5e-113">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="7ca5e-114">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="7ca5e-115">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="7ca5e-116">預設 Azure 磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-116">Default Azure disks</span></span>

<span data-ttu-id="7ca5e-117">建立 Azure 虛擬機器時，兩個磁碟會自動附加的 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="7ca5e-118">**作業系統磁碟**-作業系統磁碟可以 too1 tb 向上調整大小和主機 hello Vm 的作業系統。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="7ca5e-119">hello OS 磁碟被指派的磁碟機代號*c:*預設。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="7ca5e-120">hello 磁碟快取的 hello 作業系統磁碟組態已針對 OS 效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="7ca5e-121">hello OS 磁碟**不應該**裝載應用程式或資料。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="7ca5e-122">請對應用程式和資料使用資料磁碟，本文稍後會詳細說明。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="7ca5e-123">**暫存磁碟**-暫存磁碟使用固態磁碟機上 hello hello VM 為相同的 Azure 主機。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="7ca5e-124">暫存磁碟的效能非常好，可用於暫存資料處理等作業。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="7ca5e-125">不過，如果 hello VM 移動的 tooa 新主機，就會移除儲存在暫存磁碟上的任何資料。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="7ca5e-126">hello hello 暫存磁碟的大小取決於 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="7ca5e-127">預設會將磁碟機代號 d: 指派給暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="7ca5e-128">暫存磁碟大小</span><span class="sxs-lookup"><span data-stu-id="7ca5e-128">Temporary disk sizes</span></span>

| <span data-ttu-id="7ca5e-129">類型</span><span class="sxs-lookup"><span data-stu-id="7ca5e-129">Type</span></span> | <span data-ttu-id="7ca5e-130">VM 大小</span><span class="sxs-lookup"><span data-stu-id="7ca5e-130">VM Size</span></span> | <span data-ttu-id="7ca5e-131">暫存磁碟大小上限 (GB)</span><span class="sxs-lookup"><span data-stu-id="7ca5e-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="7ca5e-132">一般用途</span><span class="sxs-lookup"><span data-stu-id="7ca5e-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="7ca5e-133">A 和 D 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-133">A and D series</span></span> | <span data-ttu-id="7ca5e-134">800</span><span class="sxs-lookup"><span data-stu-id="7ca5e-134">800</span></span> |
| [<span data-ttu-id="7ca5e-135">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="7ca5e-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="7ca5e-136">F 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-136">F series</span></span> | <span data-ttu-id="7ca5e-137">800</span><span class="sxs-lookup"><span data-stu-id="7ca5e-137">800</span></span> |
| [<span data-ttu-id="7ca5e-138">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="7ca5e-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="7ca5e-139">D 和 G 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-139">D and G series</span></span> | <span data-ttu-id="7ca5e-140">6144</span><span class="sxs-lookup"><span data-stu-id="7ca5e-140">6144</span></span> |
| [<span data-ttu-id="7ca5e-141">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="7ca5e-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="7ca5e-142">L 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-142">L series</span></span> | <span data-ttu-id="7ca5e-143">5630</span><span class="sxs-lookup"><span data-stu-id="7ca5e-143">5630</span></span> |
| [<span data-ttu-id="7ca5e-144">GPU</span><span class="sxs-lookup"><span data-stu-id="7ca5e-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="7ca5e-145">N 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-145">N series</span></span> | <span data-ttu-id="7ca5e-146">1440</span><span class="sxs-lookup"><span data-stu-id="7ca5e-146">1440</span></span> |
| [<span data-ttu-id="7ca5e-147">高效能</span><span class="sxs-lookup"><span data-stu-id="7ca5e-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="7ca5e-148">A 和 H 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-148">A and H series</span></span> | <span data-ttu-id="7ca5e-149">2000</span><span class="sxs-lookup"><span data-stu-id="7ca5e-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="7ca5e-150">Azure 資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-150">Azure data disks</span></span>

<span data-ttu-id="7ca5e-151">您可以新增額外資料磁碟，以便安裝應用程式和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="7ca5e-152">資料磁碟應使用於任何需要持久且有回應之資料儲存體的情況。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="7ca5e-153">每個資料磁碟的最大容量為 1 TB。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="7ca5e-154">hello hello 虛擬機器大小會決定資料磁碟數目可為附加的 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="7ca5e-155">每個 VM 核心可以連結兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="7ca5e-156">每部 VM 的資料磁碟上限</span><span class="sxs-lookup"><span data-stu-id="7ca5e-156">Max data disks per VM</span></span>

| <span data-ttu-id="7ca5e-157">類型</span><span class="sxs-lookup"><span data-stu-id="7ca5e-157">Type</span></span> | <span data-ttu-id="7ca5e-158">VM 大小</span><span class="sxs-lookup"><span data-stu-id="7ca5e-158">VM Size</span></span> | <span data-ttu-id="7ca5e-159">每部 VM 的資料磁碟上限</span><span class="sxs-lookup"><span data-stu-id="7ca5e-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="7ca5e-160">一般用途</span><span class="sxs-lookup"><span data-stu-id="7ca5e-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="7ca5e-161">A 和 D 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-161">A and D series</span></span> | <span data-ttu-id="7ca5e-162">32</span><span class="sxs-lookup"><span data-stu-id="7ca5e-162">32</span></span> |
| [<span data-ttu-id="7ca5e-163">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="7ca5e-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="7ca5e-164">F 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-164">F series</span></span> | <span data-ttu-id="7ca5e-165">32</span><span class="sxs-lookup"><span data-stu-id="7ca5e-165">32</span></span> |
| [<span data-ttu-id="7ca5e-166">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="7ca5e-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="7ca5e-167">D 和 G 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-167">D and G series</span></span> | <span data-ttu-id="7ca5e-168">64</span><span class="sxs-lookup"><span data-stu-id="7ca5e-168">64</span></span> |
| [<span data-ttu-id="7ca5e-169">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="7ca5e-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="7ca5e-170">L 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-170">L series</span></span> | <span data-ttu-id="7ca5e-171">64</span><span class="sxs-lookup"><span data-stu-id="7ca5e-171">64</span></span> |
| [<span data-ttu-id="7ca5e-172">GPU</span><span class="sxs-lookup"><span data-stu-id="7ca5e-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="7ca5e-173">N 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-173">N series</span></span> | <span data-ttu-id="7ca5e-174">48</span><span class="sxs-lookup"><span data-stu-id="7ca5e-174">48</span></span> |
| [<span data-ttu-id="7ca5e-175">高效能</span><span class="sxs-lookup"><span data-stu-id="7ca5e-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="7ca5e-176">A 和 H 系列</span><span class="sxs-lookup"><span data-stu-id="7ca5e-176">A and H series</span></span> | <span data-ttu-id="7ca5e-177">32</span><span class="sxs-lookup"><span data-stu-id="7ca5e-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="7ca5e-178">VM 磁碟類型</span><span class="sxs-lookup"><span data-stu-id="7ca5e-178">VM disk types</span></span>

<span data-ttu-id="7ca5e-179">Azure 提供兩種類型的磁碟。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="7ca5e-180">標準磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-180">Standard disk</span></span>

<span data-ttu-id="7ca5e-181">標準儲存體是以 HDD 為後盾，既可提供符合成本效益的儲存體，又可保有效能。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="7ca5e-182">標準磁碟適合用於具成本效益的開發和測試工作負載。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="7ca5e-183">進階磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-183">Premium disk</span></span>

<span data-ttu-id="7ca5e-184">進階磁碟是以 SSD 為基礎的高效能、低延遲磁碟為後盾。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="7ca5e-185">最適合用於執行生產工作負載的 VM。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="7ca5e-186">進階儲存體支援 DS 系列、DSv2 系列、GS 系列和 FS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="7ca5e-187">高階磁碟都是以三種類型 (P10，P20，P30)，hello hello 磁碟大小會決定 hello 磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="7ca5e-188">選取時，磁碟大小 hello 值會無條件進位 toohello 下一個類型。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="7ca5e-189">比方說，如果 hello 大小低於 128 GB hello 磁碟類型就是 P10，129 和 512 P20，與超過 512 P30 之間。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="7ca5e-190">進階磁碟效能</span><span class="sxs-lookup"><span data-stu-id="7ca5e-190">Premium disk performance</span></span>

|<span data-ttu-id="7ca5e-191">進階儲存體磁碟類型</span><span class="sxs-lookup"><span data-stu-id="7ca5e-191">Premium storage disk type</span></span> | <span data-ttu-id="7ca5e-192">P10</span><span class="sxs-lookup"><span data-stu-id="7ca5e-192">P10</span></span> | <span data-ttu-id="7ca5e-193">P20</span><span class="sxs-lookup"><span data-stu-id="7ca5e-193">P20</span></span> | <span data-ttu-id="7ca5e-194">P30</span><span class="sxs-lookup"><span data-stu-id="7ca5e-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7ca5e-195">磁碟大小 (上調)</span><span class="sxs-lookup"><span data-stu-id="7ca5e-195">Disk size (round up)</span></span> | <span data-ttu-id="7ca5e-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="7ca5e-196">128 GB</span></span> | <span data-ttu-id="7ca5e-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="7ca5e-197">512 GB</span></span> | <span data-ttu-id="7ca5e-198">1,024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="7ca5e-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="7ca5e-199">每一磁碟的 IOPS</span><span class="sxs-lookup"><span data-stu-id="7ca5e-199">IOPS per disk</span></span> | <span data-ttu-id="7ca5e-200">500</span><span class="sxs-lookup"><span data-stu-id="7ca5e-200">500</span></span> | <span data-ttu-id="7ca5e-201">2,300</span><span class="sxs-lookup"><span data-stu-id="7ca5e-201">2,300</span></span> | <span data-ttu-id="7ca5e-202">5,000</span><span class="sxs-lookup"><span data-stu-id="7ca5e-202">5,000</span></span> |
<span data-ttu-id="7ca5e-203">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="7ca5e-203">Throughput per disk</span></span> | <span data-ttu-id="7ca5e-204">100 MB/秒</span><span class="sxs-lookup"><span data-stu-id="7ca5e-204">100 MB/s</span></span> | <span data-ttu-id="7ca5e-205">150 MB/秒</span><span class="sxs-lookup"><span data-stu-id="7ca5e-205">150 MB/s</span></span> | <span data-ttu-id="7ca5e-206">200 MB/秒</span><span class="sxs-lookup"><span data-stu-id="7ca5e-206">200 MB/s</span></span> |

<span data-ttu-id="7ca5e-207">雖然資料表上方的 hello 會識別每個磁碟的最大 IOPS 較高的效能等級可藉由多個資料磁碟條狀配置。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="7ca5e-208">比方說，磁碟可以是 64 的資料會附加 tooStandard_GS5 VM。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="7ca5e-209">如果上述每個磁碟的大小調整為 P30，就可以達到 80,000 IOPS 的最大值。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="7ca5e-210">如需每部 VM 的最大 IOPS 詳細資訊，請參閱 [Linux VM 大小](./sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="7ca5e-211">建立和連結磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-211">Create and attach disks</span></span>

<span data-ttu-id="7ca5e-212">在本教學課程 toocomplete hello 範例中的，您必須擁有現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="7ca5e-213">如有需要，這個[指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)可以為您建立一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="7ca5e-214">當工作透過 hello 教學課程中，取代 hello 資源群組和 VM 名稱在需要時。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="7ca5e-215">建立 hello 初始組態[新增 AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig)。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="7ca5e-216">hello 下列範例會設定為 128 gb 大小的磁碟。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="7ca5e-217">建立 hello 資料磁碟以 hello[新增 AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk)命令。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="7ca5e-218">Get hello 虛擬機器，而您想 tooadd hello 資料磁碟 toowith hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm)命令。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="7ca5e-219">新增 hello 資料磁碟 toohello 虛擬機器組態 hello[新增 AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk)命令。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="7ca5e-220">更新 hello 的虛擬機器以 hello[更新 AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk)命令。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="7ca5e-221">準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-221">Prepare data disks</span></span>

<span data-ttu-id="7ca5e-222">一旦磁碟已附加的 toohello 虛擬機器，必須設定 toobe toouse hello 磁碟 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="7ca5e-223">hello 下列範例示範如何 toomanually 設定 hello 新增的第一個磁碟 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="7ca5e-224">此程序也可以自動化使用 hello[自訂指令碼延伸](./tutorial-automate-vm-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="7ca5e-225">手動設定</span><span class="sxs-lookup"><span data-stu-id="7ca5e-225">Manual configuration</span></span>

<span data-ttu-id="7ca5e-226">建立 hello 虛擬機器的 RDP 連接。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="7ca5e-227">開啟 PowerShell 並執行這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="7ca5e-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-228">Next steps</span></span>

<span data-ttu-id="7ca5e-229">在本教學課程中，您已了解 VM 磁碟的相關主題，像是：</span><span class="sxs-lookup"><span data-stu-id="7ca5e-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ca5e-230">OS 磁碟和暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="7ca5e-231">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-231">Data disks</span></span>
> * <span data-ttu-id="7ca5e-232">標準和進階磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="7ca5e-233">磁碟效能</span><span class="sxs-lookup"><span data-stu-id="7ca5e-233">Disk performance</span></span>
> * <span data-ttu-id="7ca5e-234">連結及準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7ca5e-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="7ca5e-235">前進 toohello 下一個教學課程的 toolearn 自動化 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="7ca5e-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ca5e-236">自動設定 VM</span><span class="sxs-lookup"><span data-stu-id="7ca5e-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
