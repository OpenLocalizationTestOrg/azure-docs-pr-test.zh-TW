---
title: "使用 Azure CLI 管理 Azure 磁碟 | Microsoft Docs"
description: "教學課程 - 使用 Azure CLI 管理 Azure 磁碟"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d77dd2b44dca8cee6fa2e93e79cda76c80ccfe1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-the-azure-cli"></a><span data-ttu-id="b8274-103">使用 Azure CLI 管理 Azure 磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-103">Manage Azure disks with the Azure CLI</span></span>

<span data-ttu-id="b8274-104">Azure 虛擬機器使用硬碟來儲存 VM 作業系統、應用程式和資料。</span><span class="sxs-lookup"><span data-stu-id="b8274-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="b8274-105">建立 VM 時，請務必選擇適合所預期工作負載的磁碟大小和組態。</span><span class="sxs-lookup"><span data-stu-id="b8274-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="b8274-106">本教學課程涵蓋部署和管理 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8274-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="b8274-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="b8274-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8274-108">OS 磁碟和暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="b8274-109">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-109">Data disks</span></span>
> * <span data-ttu-id="b8274-110">標準和進階磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="b8274-111">磁碟效能</span><span class="sxs-lookup"><span data-stu-id="b8274-111">Disk performance</span></span>
> * <span data-ttu-id="b8274-112">連結及準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="b8274-113">調整磁碟的大小</span><span class="sxs-lookup"><span data-stu-id="b8274-113">Resizing disks</span></span>
> * <span data-ttu-id="b8274-114">磁碟快照集</span><span class="sxs-lookup"><span data-stu-id="b8274-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b8274-115">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b8274-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b8274-116">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="b8274-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="b8274-117">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="b8274-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="b8274-118">預設 Azure 磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-118">Default Azure disks</span></span>

<span data-ttu-id="b8274-119">建立 Azure 虛擬機器後，有兩個磁碟會自動連結到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8274-119">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="b8274-120">**作業系統磁碟** - 作業系統磁碟可裝載 VM 作業系統，其大小可以高達 1 TB。</span><span class="sxs-lookup"><span data-stu-id="b8274-120">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span> <span data-ttu-id="b8274-121">OS 磁碟預設會標示為 /dev/sda。</span><span class="sxs-lookup"><span data-stu-id="b8274-121">The OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="b8274-122">OS 磁碟的磁碟快取組態已針對 OS 效能進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="b8274-122">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="b8274-123">因為此組態，OS 磁碟**不得**裝載應用程式或資料。</span><span class="sxs-lookup"><span data-stu-id="b8274-123">Because of this configuration, the OS disk **should not** host applications or data.</span></span> <span data-ttu-id="b8274-124">請對應用程式和資料使用資料磁碟，本文稍後會詳細說明。</span><span class="sxs-lookup"><span data-stu-id="b8274-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="b8274-125">**暫存磁碟** - 暫存磁碟會使用與 VM 位於相同 Azure 主機的固態磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b8274-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="b8274-126">暫存磁碟的效能非常好，可用於暫存資料處理等作業。</span><span class="sxs-lookup"><span data-stu-id="b8274-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="b8274-127">不過，如果 VM 移至新的主機，則會移除儲存在暫存磁碟上的任何資料。</span><span class="sxs-lookup"><span data-stu-id="b8274-127">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="b8274-128">暫存磁碟的大小取決於 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="b8274-128">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="b8274-129">暫存磁碟會標示為 /dev/sdb，其掛接點為 /mnt。</span><span class="sxs-lookup"><span data-stu-id="b8274-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="b8274-130">暫存磁碟大小</span><span class="sxs-lookup"><span data-stu-id="b8274-130">Temporary disk sizes</span></span>

| <span data-ttu-id="b8274-131">類型</span><span class="sxs-lookup"><span data-stu-id="b8274-131">Type</span></span> | <span data-ttu-id="b8274-132">VM 大小</span><span class="sxs-lookup"><span data-stu-id="b8274-132">VM Size</span></span> | <span data-ttu-id="b8274-133">暫存磁碟大小上限 (GB)</span><span class="sxs-lookup"><span data-stu-id="b8274-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="b8274-134">一般用途</span><span class="sxs-lookup"><span data-stu-id="b8274-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="b8274-135">A 和 D 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-135">A and D series</span></span> | <span data-ttu-id="b8274-136">800</span><span class="sxs-lookup"><span data-stu-id="b8274-136">800</span></span> |
| [<span data-ttu-id="b8274-137">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="b8274-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="b8274-138">F 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-138">F series</span></span> | <span data-ttu-id="b8274-139">800</span><span class="sxs-lookup"><span data-stu-id="b8274-139">800</span></span> |
| [<span data-ttu-id="b8274-140">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="b8274-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="b8274-141">D 和 G 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-141">D and G series</span></span> | <span data-ttu-id="b8274-142">6144</span><span class="sxs-lookup"><span data-stu-id="b8274-142">6144</span></span> |
| [<span data-ttu-id="b8274-143">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="b8274-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="b8274-144">L 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-144">L series</span></span> | <span data-ttu-id="b8274-145">5630</span><span class="sxs-lookup"><span data-stu-id="b8274-145">5630</span></span> |
| [<span data-ttu-id="b8274-146">GPU</span><span class="sxs-lookup"><span data-stu-id="b8274-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="b8274-147">N 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-147">N series</span></span> | <span data-ttu-id="b8274-148">1440</span><span class="sxs-lookup"><span data-stu-id="b8274-148">1440</span></span> |
| [<span data-ttu-id="b8274-149">高效能</span><span class="sxs-lookup"><span data-stu-id="b8274-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="b8274-150">A 和 H 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-150">A and H series</span></span> | <span data-ttu-id="b8274-151">2000</span><span class="sxs-lookup"><span data-stu-id="b8274-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="b8274-152">Azure 資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-152">Azure data disks</span></span>

<span data-ttu-id="b8274-153">您可以新增額外資料磁碟，以便安裝應用程式和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="b8274-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="b8274-154">資料磁碟應使用於任何需要持久且有回應之資料儲存體的情況。</span><span class="sxs-lookup"><span data-stu-id="b8274-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="b8274-155">每個資料磁碟的最大容量為 1 TB。</span><span class="sxs-lookup"><span data-stu-id="b8274-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="b8274-156">虛擬機器的大小會決定可連結到 VM 的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="b8274-156">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="b8274-157">每個 VM 核心可以連結兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8274-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="b8274-158">每部 VM 的資料磁碟上限</span><span class="sxs-lookup"><span data-stu-id="b8274-158">Max data disks per VM</span></span>

| <span data-ttu-id="b8274-159">類型</span><span class="sxs-lookup"><span data-stu-id="b8274-159">Type</span></span> | <span data-ttu-id="b8274-160">VM 大小</span><span class="sxs-lookup"><span data-stu-id="b8274-160">VM Size</span></span> | <span data-ttu-id="b8274-161">每部 VM 的資料磁碟上限</span><span class="sxs-lookup"><span data-stu-id="b8274-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="b8274-162">一般用途</span><span class="sxs-lookup"><span data-stu-id="b8274-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="b8274-163">A 和 D 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-163">A and D series</span></span> | <span data-ttu-id="b8274-164">32</span><span class="sxs-lookup"><span data-stu-id="b8274-164">32</span></span> |
| [<span data-ttu-id="b8274-165">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="b8274-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="b8274-166">F 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-166">F series</span></span> | <span data-ttu-id="b8274-167">32</span><span class="sxs-lookup"><span data-stu-id="b8274-167">32</span></span> |
| [<span data-ttu-id="b8274-168">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="b8274-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="b8274-169">D 和 G 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-169">D and G series</span></span> | <span data-ttu-id="b8274-170">64</span><span class="sxs-lookup"><span data-stu-id="b8274-170">64</span></span> |
| [<span data-ttu-id="b8274-171">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="b8274-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="b8274-172">L 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-172">L series</span></span> | <span data-ttu-id="b8274-173">64</span><span class="sxs-lookup"><span data-stu-id="b8274-173">64</span></span> |
| [<span data-ttu-id="b8274-174">GPU</span><span class="sxs-lookup"><span data-stu-id="b8274-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="b8274-175">N 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-175">N series</span></span> | <span data-ttu-id="b8274-176">48</span><span class="sxs-lookup"><span data-stu-id="b8274-176">48</span></span> |
| [<span data-ttu-id="b8274-177">高效能</span><span class="sxs-lookup"><span data-stu-id="b8274-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="b8274-178">A 和 H 系列</span><span class="sxs-lookup"><span data-stu-id="b8274-178">A and H series</span></span> | <span data-ttu-id="b8274-179">32</span><span class="sxs-lookup"><span data-stu-id="b8274-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="b8274-180">VM 磁碟類型</span><span class="sxs-lookup"><span data-stu-id="b8274-180">VM disk types</span></span>

<span data-ttu-id="b8274-181">Azure 提供兩種類型的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8274-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="b8274-182">標準磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-182">Standard disk</span></span>

<span data-ttu-id="b8274-183">標準儲存體是以 HDD 為後盾，既可提供符合成本效益的儲存體，又可保有效能。</span><span class="sxs-lookup"><span data-stu-id="b8274-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="b8274-184">標準磁碟適合用於具成本效益的開發和測試工作負載。</span><span class="sxs-lookup"><span data-stu-id="b8274-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="b8274-185">進階磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-185">Premium disk</span></span>

<span data-ttu-id="b8274-186">進階磁碟是以 SSD 為基礎的高效能、低延遲磁碟為後盾。</span><span class="sxs-lookup"><span data-stu-id="b8274-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="b8274-187">最適合用於執行生產工作負載的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="b8274-188">進階儲存體支援 DS 系列、DSv2 系列、GS 系列和 FS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="b8274-189">進階磁碟有三種類型 (P10、P20、P30)，磁碟的大小可決定磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="b8274-189">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="b8274-190">進行選取時，磁碟大小值會上調為下一個類型。</span><span class="sxs-lookup"><span data-stu-id="b8274-190">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="b8274-191">例如，如果磁碟大小少於 128 GB，則磁碟類型為 P10。</span><span class="sxs-lookup"><span data-stu-id="b8274-191">For example, if the disk size is less than 128 GB, the disk type is P10.</span></span> <span data-ttu-id="b8274-192">如果磁碟大小介於 129 GB 與 512 GB 之間，則大小為 P20。</span><span class="sxs-lookup"><span data-stu-id="b8274-192">If the disk size is between 129 GB and 512 GB, the size is a P20.</span></span> <span data-ttu-id="b8274-193">任何超過 512 GB 的磁碟，其大小是 P30。</span><span class="sxs-lookup"><span data-stu-id="b8274-193">Anything over 512 GB, the size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="b8274-194">進階磁碟效能</span><span class="sxs-lookup"><span data-stu-id="b8274-194">Premium disk performance</span></span>

|<span data-ttu-id="b8274-195">進階儲存體磁碟類型</span><span class="sxs-lookup"><span data-stu-id="b8274-195">Premium storage disk type</span></span> | <span data-ttu-id="b8274-196">P10</span><span class="sxs-lookup"><span data-stu-id="b8274-196">P10</span></span> | <span data-ttu-id="b8274-197">P20</span><span class="sxs-lookup"><span data-stu-id="b8274-197">P20</span></span> | <span data-ttu-id="b8274-198">P30</span><span class="sxs-lookup"><span data-stu-id="b8274-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b8274-199">磁碟大小 (上調)</span><span class="sxs-lookup"><span data-stu-id="b8274-199">Disk size (round up)</span></span> | <span data-ttu-id="b8274-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="b8274-200">128 GB</span></span> | <span data-ttu-id="b8274-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="b8274-201">512 GB</span></span> | <span data-ttu-id="b8274-202">1,024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="b8274-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="b8274-203">每一磁碟的 IOPS 上限</span><span class="sxs-lookup"><span data-stu-id="b8274-203">Max IOPS per disk</span></span> | <span data-ttu-id="b8274-204">500</span><span class="sxs-lookup"><span data-stu-id="b8274-204">500</span></span> | <span data-ttu-id="b8274-205">2,300</span><span class="sxs-lookup"><span data-stu-id="b8274-205">2,300</span></span> | <span data-ttu-id="b8274-206">5,000</span><span class="sxs-lookup"><span data-stu-id="b8274-206">5,000</span></span> |
<span data-ttu-id="b8274-207">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="b8274-207">Throughput per disk</span></span> | <span data-ttu-id="b8274-208">100 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8274-208">100 MB/s</span></span> | <span data-ttu-id="b8274-209">150 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8274-209">150 MB/s</span></span> | <span data-ttu-id="b8274-210">200 MB/秒</span><span class="sxs-lookup"><span data-stu-id="b8274-210">200 MB/s</span></span> |

<span data-ttu-id="b8274-211">雖然上表指出每個磁碟的最大 IOPS，但可藉由分割多個資料磁碟來達到較高等級的效能。</span><span class="sxs-lookup"><span data-stu-id="b8274-211">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="b8274-212">例如，Standard_GS5 VM 最高可達到 80,000 IOPS。</span><span class="sxs-lookup"><span data-stu-id="b8274-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="b8274-213">如需每部 VM 的最大 IOPS 詳細資訊，請參閱 [Linux VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="b8274-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="b8274-214">建立和連結磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-214">Create and attach disks</span></span>

<span data-ttu-id="b8274-215">您可以建立資料磁碟並在建立 VM 時連結，或連結至現有的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-215">Data disks can be created and attached at VM creation time or to an existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="b8274-216">在建立 VM 時連結磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-216">Attach disk at VM creation</span></span>

<span data-ttu-id="b8274-217">使用 [az group create](https://docs.microsoft.com/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="b8274-217">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="b8274-218">使用 [az vm create]( /cli/azure/vm#create) 命令來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-218">Create a VM using the [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="b8274-219">`--datadisk-sizes-gb` 引數用來指定應該建立一個額外的磁碟並連結至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8274-219">The `--datadisk-sizes-gb` argument is used to specify that an additional disk should be created and attached to the virtual machine.</span></span> <span data-ttu-id="b8274-220">若要建立並連結多個磁碟，請使用以空格分隔的磁碟大小值清單。</span><span class="sxs-lookup"><span data-stu-id="b8274-220">To create and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="b8274-221">在下列範例中，會建立具有兩個資料磁碟 (均為 128 GB) 的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-221">In the following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="b8274-222">因為磁碟大小是 128 GB，所以這些磁碟都會設為 P10，其可提供每個磁碟最高 500 IOPS。</span><span class="sxs-lookup"><span data-stu-id="b8274-222">Because the disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-to-existing-vm"></a><span data-ttu-id="b8274-223">將磁碟連結至現有的 VM</span><span class="sxs-lookup"><span data-stu-id="b8274-223">Attach disk to existing VM</span></span>

<span data-ttu-id="b8274-224">若要建立新的磁碟並將它連結至現有的虛擬機器，請使用 [az vm disk attach](/cli/azure/vm/disk#attach) 命令。</span><span class="sxs-lookup"><span data-stu-id="b8274-224">To create and attach a new disk to an existing virtual machine, use the [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="b8274-225">下列範例會建立進階磁碟 (大小為 128 GB)，並將它連結至最後一個步驟中建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-225">The following example creates a premium disk, 128 gigabytes in size, and attaches it to the VM created in the last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="b8274-226">準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-226">Prepare data disks</span></span>

<span data-ttu-id="b8274-227">將磁碟連結到虛擬機器後，必須將作業系統設定為使用該磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8274-227">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="b8274-228">下列範例示範如何手動設定磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8274-228">The following example shows how to manually configure a disk.</span></span> <span data-ttu-id="b8274-229">使用 cloud-init (涵蓋於[稍後的教學課程](./tutorial-automate-vm-deployment.md)中) 也可以將此程序自動化。</span><span class="sxs-lookup"><span data-stu-id="b8274-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="b8274-230">手動設定</span><span class="sxs-lookup"><span data-stu-id="b8274-230">Manual configuration</span></span>

<span data-ttu-id="b8274-231">建立虛擬機器的 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="b8274-231">Create an SSH connection with the virtual machine.</span></span> <span data-ttu-id="b8274-232">以虛擬機器的公用 IP 位址取代範例 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8274-232">Replace the example IP address with the public IP of the virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="b8274-233">使用 `fdisk` 分割磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8274-233">Partition the disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="b8274-234">使用 `mkfs` 命令將檔案系統寫入至磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="b8274-234">Write a file system to the partition by using the `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="b8274-235">掛接新磁碟，使其可在作業系統中存取。</span><span class="sxs-lookup"><span data-stu-id="b8274-235">Mount the new disk so that it is accessible in the operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="b8274-236">現在可以透過 datadrive 掛接點存取磁碟，而執行 `df -h` 命令可驗證此掛接點。</span><span class="sxs-lookup"><span data-stu-id="b8274-236">The disk can now be accessed through the *datadrive* mountpoint, which can be verified by running the `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="b8274-237">輸出會顯示掛接在 /datadrive 上的新磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b8274-237">The output shows the new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="b8274-238">為了確保磁碟機會在重新開機之後重新掛接，必須將磁碟機新增至 /etc/fstab 檔案。</span><span class="sxs-lookup"><span data-stu-id="b8274-238">To ensure that the drive is remounted after a reboot, it must be added to the */etc/fstab* file.</span></span> <span data-ttu-id="b8274-239">若要這麼做，請使用 `blkid` 公用程式取得磁碟的 UUID。</span><span class="sxs-lookup"><span data-stu-id="b8274-239">To do so, get the UUID of the disk with the `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="b8274-240">輸出會顯示磁碟機的 UUID，在此情況下為 `/dev/sdc1`。</span><span class="sxs-lookup"><span data-stu-id="b8274-240">The output displays the UUID of the drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="b8274-241">將類似以下的一行新增至 /etc/fstab 檔案。</span><span class="sxs-lookup"><span data-stu-id="b8274-241">Add a line similar to the following to the */etc/fstab* file.</span></span> <span data-ttu-id="b8274-242">也請注意，使用 barrier=0 可以停用寫入屏障，此組態可以改善磁碟效能。</span><span class="sxs-lookup"><span data-stu-id="b8274-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="b8274-243">現在已設定磁碟，請關閉 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b8274-243">Now that the disk has been configured, close the SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="b8274-244">調整 VM 磁碟的大小</span><span class="sxs-lookup"><span data-stu-id="b8274-244">Resize VM disk</span></span>

<span data-ttu-id="b8274-245">部署 VM 後，作業系統磁碟或任何連結的資料磁碟可以增加大小。</span><span class="sxs-lookup"><span data-stu-id="b8274-245">Once a VM has been deployed, the operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="b8274-246">需要更多儲存空間或更高層級的效能 (P10、P20、P30) 時，增加磁碟的大小很有幫助。</span><span class="sxs-lookup"><span data-stu-id="b8274-246">Increasing the size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="b8274-247">請注意，磁碟的大小不能減少。</span><span class="sxs-lookup"><span data-stu-id="b8274-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="b8274-248">增加磁碟大小之前，需要有磁碟的識別碼或名稱。</span><span class="sxs-lookup"><span data-stu-id="b8274-248">Before increasing disk size, the Id or name of the disk is needed.</span></span> <span data-ttu-id="b8274-249">使用 [az disk list](/cli/azure/vm/disk#list) 命令來傳回資源群組中的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8274-249">Use the [az disk list](/cli/azure/vm/disk#list) command to return all disks in a resource group.</span></span> <span data-ttu-id="b8274-250">記下您想要調整大小的磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="b8274-250">Take note of the disk name that you would like to resize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="b8274-251">此外，也必須將 VM 解除配置。</span><span class="sxs-lookup"><span data-stu-id="b8274-251">The VM must also be deallocated.</span></span> <span data-ttu-id="b8274-252">使用 [az vm deallocate]( /cli/azure/vm#deallocate) 命令來停止並解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-252">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="b8274-253">使用 [az disk update](/cli/azure/vm/disk#update) 命令來調整磁碟的大小。</span><span class="sxs-lookup"><span data-stu-id="b8274-253">Use the [az disk update](/cli/azure/vm/disk#update) command to resize the disk.</span></span> <span data-ttu-id="b8274-254">這個範例會將名為 myDataDisk 的磁碟大小調整為 1 TB。</span><span class="sxs-lookup"><span data-stu-id="b8274-254">This example resizes a disk named *myDataDisk* to 1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="b8274-255">調整大小作業完成後，請啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-255">Once the resize operation has completed, start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="b8274-256">如果您已調整作業系統磁碟的大小，則會自動擴充資料分割。</span><span class="sxs-lookup"><span data-stu-id="b8274-256">If you’ve resized the operating system disk, the partition is automatically be expanded.</span></span> <span data-ttu-id="b8274-257">如果您已調整資料磁碟的大小，則必須在 VM 作業系統中擴充所有目前的資料分割。</span><span class="sxs-lookup"><span data-stu-id="b8274-257">If you have resized a data disk, any current partitions need to be expanded in the VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="b8274-258">建立 Azure 磁碟快照集</span><span class="sxs-lookup"><span data-stu-id="b8274-258">Snapshot Azure disks</span></span>

<span data-ttu-id="b8274-259">建立磁碟快照集，以建立磁碟的讀取、時間點複本。</span><span class="sxs-lookup"><span data-stu-id="b8274-259">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span></span> <span data-ttu-id="b8274-260">進行組態變更之前，Azure VM 快照集可用於快速儲存 VM 的狀態。</span><span class="sxs-lookup"><span data-stu-id="b8274-260">Azure VM snapshots are useful for quickly saving the state of a VM before making configuration changes.</span></span> <span data-ttu-id="b8274-261">在證實不需要組態變更的事件中，可使用快照集還原 VM 狀態。</span><span class="sxs-lookup"><span data-stu-id="b8274-261">In the event the configuration changes prove to be undesired, VM state can be restored using the snapshot.</span></span> <span data-ttu-id="b8274-262">當 VM 有多個磁碟時，每個磁碟會各自產生快照集。</span><span class="sxs-lookup"><span data-stu-id="b8274-262">When a VM has more than one disk, a snapshot is taken of each disk independently of the others.</span></span> <span data-ttu-id="b8274-263">進行應用程式一致備份時，請考慮在建立磁碟快照集之前停止 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-263">For taking application consistent backups, consider stopping the VM before taking disk snapshots.</span></span> <span data-ttu-id="b8274-264">或者，使用 [Azure 備份服務](/azure/backup/)，其可讓您在 VM 執行時執行自動化備份。</span><span class="sxs-lookup"><span data-stu-id="b8274-264">Alternatively, use the [Azure Backup service](/azure/backup/), which enables you to perform automated backups while the VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="b8274-265">建立快照集</span><span class="sxs-lookup"><span data-stu-id="b8274-265">Create snapshot</span></span>

<span data-ttu-id="b8274-266">建立虛擬機器磁碟快照集之前，需要磁碟的識別碼或名稱。</span><span class="sxs-lookup"><span data-stu-id="b8274-266">Before creating a virtual machine disk snapshot, the Id or name of the disk is needed.</span></span> <span data-ttu-id="b8274-267">使用 [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) 命令傳回磁碟識別碼。</span><span class="sxs-lookup"><span data-stu-id="b8274-267">Use the [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command to return the disk id.</span></span> <span data-ttu-id="b8274-268">在此範例中，磁碟會儲存在變數中，以便使用於稍後的步驟。</span><span class="sxs-lookup"><span data-stu-id="b8274-268">In this example, the disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="b8274-269">您現在有虛擬機器磁碟的識別碼，下列命令會建立磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="b8274-269">Now that you have the id of the virtual machine disk, the following command creates a snapshot of the disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="b8274-270">從快照集建立磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-270">Create disk from snapshot</span></span>

<span data-ttu-id="b8274-271">此快照集可以接著轉換成磁碟，進而用於重新建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8274-271">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="b8274-272">從快照集還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b8274-272">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="b8274-273">若要示範虛擬機器復原，請刪除現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8274-273">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="b8274-274">從快照磁碟建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8274-274">Create a new virtual machine from the snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="b8274-275">重新連結資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-275">Reattach data disk</span></span>

<span data-ttu-id="b8274-276">所有資料磁碟都必須重新連結至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8274-276">All data disks need to be reattached to the virtual machine.</span></span>

<span data-ttu-id="b8274-277">首先使用 [az disk list](https://docs.microsoft.com/cli/azure/disk#list) 命令尋找資料磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="b8274-277">First find the data disk name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="b8274-278">此範例會將磁碟名稱放入名為 datadisk 的變數，該變數使用於下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="b8274-278">This example places the name of the disk in a variable named *datadisk*, which is used in the next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="b8274-279">使用 [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) 命令來連結磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8274-279">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="b8274-280">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8274-280">Next steps</span></span>

<span data-ttu-id="b8274-281">在本教學課程中，您已了解 VM 磁碟的相關主題，像是：</span><span class="sxs-lookup"><span data-stu-id="b8274-281">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8274-282">OS 磁碟和暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-282">OS disks and temporary disks</span></span>
> * <span data-ttu-id="b8274-283">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-283">Data disks</span></span>
> * <span data-ttu-id="b8274-284">標準和進階磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-284">Standard and Premium disks</span></span>
> * <span data-ttu-id="b8274-285">磁碟效能</span><span class="sxs-lookup"><span data-stu-id="b8274-285">Disk performance</span></span>
> * <span data-ttu-id="b8274-286">連結及準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b8274-286">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="b8274-287">調整磁碟的大小</span><span class="sxs-lookup"><span data-stu-id="b8274-287">Resizing disks</span></span>
> * <span data-ttu-id="b8274-288">磁碟快照集</span><span class="sxs-lookup"><span data-stu-id="b8274-288">Disk snapshots</span></span>

<span data-ttu-id="b8274-289">請前進到下一個教學課程，以了解如何自動設定 VM。</span><span class="sxs-lookup"><span data-stu-id="b8274-289">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b8274-290">自動設定 VM</span><span class="sxs-lookup"><span data-stu-id="b8274-290">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
