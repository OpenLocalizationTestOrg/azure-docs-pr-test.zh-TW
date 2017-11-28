---
title: "aaaManage Azure 磁碟以 hello Azure CLI |Microsoft 文件"
description: "教學課程-管理 Azure 磁碟以 hello Azure CLI"
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
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="a5285-103">管理 Azure 磁碟以 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a5285-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="a5285-104">Azure 虛擬機器使用的磁碟 toostore hello Vm 作業系統、 應用程式和資料。</span><span class="sxs-lookup"><span data-stu-id="a5285-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="a5285-105">建立 VM 時，重要 toochoose 磁碟大小和設定適當的 toohello 預期工作負載。</span><span class="sxs-lookup"><span data-stu-id="a5285-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="a5285-106">本教學課程涵蓋部署和管理 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="a5285-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="a5285-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5285-108">OS 磁碟和暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="a5285-109">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-109">Data disks</span></span>
> * <span data-ttu-id="a5285-110">標準和進階磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="a5285-111">磁碟效能</span><span class="sxs-lookup"><span data-stu-id="a5285-111">Disk performance</span></span>
> * <span data-ttu-id="a5285-112">連結及準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="a5285-113">調整磁碟的大小</span><span class="sxs-lookup"><span data-stu-id="a5285-113">Resizing disks</span></span>
> * <span data-ttu-id="a5285-114">磁碟快照集</span><span class="sxs-lookup"><span data-stu-id="a5285-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a5285-115">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a5285-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a5285-116">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="a5285-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a5285-117">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a5285-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="a5285-118">預設 Azure 磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-118">Default Azure disks</span></span>

<span data-ttu-id="a5285-119">建立 Azure 虛擬機器時，兩個磁碟會自動附加的 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a5285-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="a5285-120">**作業系統磁碟**-作業系統磁碟可以 too1 tb 向上調整大小和主機 hello Vm 的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a5285-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="a5285-121">hello OS 磁碟標示*/開發/sda*預設。</span><span class="sxs-lookup"><span data-stu-id="a5285-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="a5285-122">hello 磁碟快取的 hello 作業系統磁碟組態已針對 OS 效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="a5285-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="a5285-123">此設定，因為 hello OS 磁碟**不應該**裝載應用程式或資料。</span><span class="sxs-lookup"><span data-stu-id="a5285-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="a5285-124">請對應用程式和資料使用資料磁碟，本文稍後會詳細說明。</span><span class="sxs-lookup"><span data-stu-id="a5285-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="a5285-125">**暫存磁碟**-暫存磁碟使用固態磁碟機上 hello hello VM 為相同的 Azure 主機。</span><span class="sxs-lookup"><span data-stu-id="a5285-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="a5285-126">暫存磁碟的效能非常好，可用於暫存資料處理等作業。</span><span class="sxs-lookup"><span data-stu-id="a5285-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="a5285-127">不過，如果 hello VM 移動的 tooa 新主機，就會移除儲存在暫存磁碟上的任何資料。</span><span class="sxs-lookup"><span data-stu-id="a5285-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="a5285-128">hello hello 暫存磁碟的大小取決於 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="a5285-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="a5285-129">暫存磁碟會標示為 /dev/sdb，其掛接點為 /mnt。</span><span class="sxs-lookup"><span data-stu-id="a5285-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="a5285-130">暫存磁碟大小</span><span class="sxs-lookup"><span data-stu-id="a5285-130">Temporary disk sizes</span></span>

| <span data-ttu-id="a5285-131">類型</span><span class="sxs-lookup"><span data-stu-id="a5285-131">Type</span></span> | <span data-ttu-id="a5285-132">VM 大小</span><span class="sxs-lookup"><span data-stu-id="a5285-132">VM Size</span></span> | <span data-ttu-id="a5285-133">暫存磁碟大小上限 (GB)</span><span class="sxs-lookup"><span data-stu-id="a5285-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="a5285-134">一般用途</span><span class="sxs-lookup"><span data-stu-id="a5285-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="a5285-135">A 和 D 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-135">A and D series</span></span> | <span data-ttu-id="a5285-136">800</span><span class="sxs-lookup"><span data-stu-id="a5285-136">800</span></span> |
| [<span data-ttu-id="a5285-137">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="a5285-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="a5285-138">F 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-138">F series</span></span> | <span data-ttu-id="a5285-139">800</span><span class="sxs-lookup"><span data-stu-id="a5285-139">800</span></span> |
| [<span data-ttu-id="a5285-140">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="a5285-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="a5285-141">D 和 G 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-141">D and G series</span></span> | <span data-ttu-id="a5285-142">6144</span><span class="sxs-lookup"><span data-stu-id="a5285-142">6144</span></span> |
| [<span data-ttu-id="a5285-143">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="a5285-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="a5285-144">L 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-144">L series</span></span> | <span data-ttu-id="a5285-145">5630</span><span class="sxs-lookup"><span data-stu-id="a5285-145">5630</span></span> |
| [<span data-ttu-id="a5285-146">GPU</span><span class="sxs-lookup"><span data-stu-id="a5285-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="a5285-147">N 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-147">N series</span></span> | <span data-ttu-id="a5285-148">1440</span><span class="sxs-lookup"><span data-stu-id="a5285-148">1440</span></span> |
| [<span data-ttu-id="a5285-149">高效能</span><span class="sxs-lookup"><span data-stu-id="a5285-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="a5285-150">A 和 H 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-150">A and H series</span></span> | <span data-ttu-id="a5285-151">2000</span><span class="sxs-lookup"><span data-stu-id="a5285-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="a5285-152">Azure 資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-152">Azure data disks</span></span>

<span data-ttu-id="a5285-153">您可以新增額外資料磁碟，以便安裝應用程式和儲存資料。</span><span class="sxs-lookup"><span data-stu-id="a5285-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="a5285-154">資料磁碟應使用於任何需要持久且有回應之資料儲存體的情況。</span><span class="sxs-lookup"><span data-stu-id="a5285-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="a5285-155">每個資料磁碟的最大容量為 1 TB。</span><span class="sxs-lookup"><span data-stu-id="a5285-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="a5285-156">hello hello 虛擬機器大小會決定資料磁碟數目可為附加的 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="a5285-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="a5285-157">每個 VM 核心可以連結兩個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="a5285-158">每部 VM 的資料磁碟上限</span><span class="sxs-lookup"><span data-stu-id="a5285-158">Max data disks per VM</span></span>

| <span data-ttu-id="a5285-159">類型</span><span class="sxs-lookup"><span data-stu-id="a5285-159">Type</span></span> | <span data-ttu-id="a5285-160">VM 大小</span><span class="sxs-lookup"><span data-stu-id="a5285-160">VM Size</span></span> | <span data-ttu-id="a5285-161">每部 VM 的資料磁碟上限</span><span class="sxs-lookup"><span data-stu-id="a5285-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="a5285-162">一般用途</span><span class="sxs-lookup"><span data-stu-id="a5285-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="a5285-163">A 和 D 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-163">A and D series</span></span> | <span data-ttu-id="a5285-164">32</span><span class="sxs-lookup"><span data-stu-id="a5285-164">32</span></span> |
| [<span data-ttu-id="a5285-165">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="a5285-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="a5285-166">F 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-166">F series</span></span> | <span data-ttu-id="a5285-167">32</span><span class="sxs-lookup"><span data-stu-id="a5285-167">32</span></span> |
| [<span data-ttu-id="a5285-168">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="a5285-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="a5285-169">D 和 G 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-169">D and G series</span></span> | <span data-ttu-id="a5285-170">64</span><span class="sxs-lookup"><span data-stu-id="a5285-170">64</span></span> |
| [<span data-ttu-id="a5285-171">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="a5285-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="a5285-172">L 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-172">L series</span></span> | <span data-ttu-id="a5285-173">64</span><span class="sxs-lookup"><span data-stu-id="a5285-173">64</span></span> |
| [<span data-ttu-id="a5285-174">GPU</span><span class="sxs-lookup"><span data-stu-id="a5285-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="a5285-175">N 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-175">N series</span></span> | <span data-ttu-id="a5285-176">48</span><span class="sxs-lookup"><span data-stu-id="a5285-176">48</span></span> |
| [<span data-ttu-id="a5285-177">高效能</span><span class="sxs-lookup"><span data-stu-id="a5285-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="a5285-178">A 和 H 系列</span><span class="sxs-lookup"><span data-stu-id="a5285-178">A and H series</span></span> | <span data-ttu-id="a5285-179">32</span><span class="sxs-lookup"><span data-stu-id="a5285-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="a5285-180">VM 磁碟類型</span><span class="sxs-lookup"><span data-stu-id="a5285-180">VM disk types</span></span>

<span data-ttu-id="a5285-181">Azure 提供兩種類型的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="a5285-182">標準磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-182">Standard disk</span></span>

<span data-ttu-id="a5285-183">標準儲存體是以 HDD 為後盾，既可提供符合成本效益的儲存體，又可保有效能。</span><span class="sxs-lookup"><span data-stu-id="a5285-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="a5285-184">標準磁碟適合用於具成本效益的開發和測試工作負載。</span><span class="sxs-lookup"><span data-stu-id="a5285-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="a5285-185">進階磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-185">Premium disk</span></span>

<span data-ttu-id="a5285-186">進階磁碟是以 SSD 為基礎的高效能、低延遲磁碟為後盾。</span><span class="sxs-lookup"><span data-stu-id="a5285-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="a5285-187">最適合用於執行生產工作負載的 VM。</span><span class="sxs-lookup"><span data-stu-id="a5285-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="a5285-188">進階儲存體支援 DS 系列、DSv2 系列、GS 系列和 FS 系列 VM。</span><span class="sxs-lookup"><span data-stu-id="a5285-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="a5285-189">高階磁碟都是以三種類型 (P10，P20，P30)，hello hello 磁碟大小會決定 hello 磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="a5285-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="a5285-190">選取時，磁碟大小 hello 值會無條件進位 toohello 下一個類型。</span><span class="sxs-lookup"><span data-stu-id="a5285-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="a5285-191">例如，如果 hello 磁碟大小小於 128 GB，hello 磁碟類型為 P10。</span><span class="sxs-lookup"><span data-stu-id="a5285-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="a5285-192">如果 hello 磁碟大小為 512 GB 129 GB 之間，hello 大小是 P20。</span><span class="sxs-lookup"><span data-stu-id="a5285-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="a5285-193">任何超過 512 GB hello 大小是 P30。</span><span class="sxs-lookup"><span data-stu-id="a5285-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="a5285-194">進階磁碟效能</span><span class="sxs-lookup"><span data-stu-id="a5285-194">Premium disk performance</span></span>

|<span data-ttu-id="a5285-195">進階儲存體磁碟類型</span><span class="sxs-lookup"><span data-stu-id="a5285-195">Premium storage disk type</span></span> | <span data-ttu-id="a5285-196">P10</span><span class="sxs-lookup"><span data-stu-id="a5285-196">P10</span></span> | <span data-ttu-id="a5285-197">P20</span><span class="sxs-lookup"><span data-stu-id="a5285-197">P20</span></span> | <span data-ttu-id="a5285-198">P30</span><span class="sxs-lookup"><span data-stu-id="a5285-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a5285-199">磁碟大小 (上調)</span><span class="sxs-lookup"><span data-stu-id="a5285-199">Disk size (round up)</span></span> | <span data-ttu-id="a5285-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="a5285-200">128 GB</span></span> | <span data-ttu-id="a5285-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="a5285-201">512 GB</span></span> | <span data-ttu-id="a5285-202">1,024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="a5285-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="a5285-203">每一磁碟的 IOPS 上限</span><span class="sxs-lookup"><span data-stu-id="a5285-203">Max IOPS per disk</span></span> | <span data-ttu-id="a5285-204">500</span><span class="sxs-lookup"><span data-stu-id="a5285-204">500</span></span> | <span data-ttu-id="a5285-205">2,300</span><span class="sxs-lookup"><span data-stu-id="a5285-205">2,300</span></span> | <span data-ttu-id="a5285-206">5,000</span><span class="sxs-lookup"><span data-stu-id="a5285-206">5,000</span></span> |
<span data-ttu-id="a5285-207">每一磁碟的輸送量</span><span class="sxs-lookup"><span data-stu-id="a5285-207">Throughput per disk</span></span> | <span data-ttu-id="a5285-208">100 MB/秒</span><span class="sxs-lookup"><span data-stu-id="a5285-208">100 MB/s</span></span> | <span data-ttu-id="a5285-209">150 MB/秒</span><span class="sxs-lookup"><span data-stu-id="a5285-209">150 MB/s</span></span> | <span data-ttu-id="a5285-210">200 MB/秒</span><span class="sxs-lookup"><span data-stu-id="a5285-210">200 MB/s</span></span> |

<span data-ttu-id="a5285-211">雖然資料表上方的 hello 會識別每個磁碟的最大 IOPS 較高的效能等級可藉由多個資料磁碟條狀配置。</span><span class="sxs-lookup"><span data-stu-id="a5285-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="a5285-212">例如，Standard_GS5 VM 最高可達到 80,000 IOPS。</span><span class="sxs-lookup"><span data-stu-id="a5285-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="a5285-213">如需每部 VM 的最大 IOPS 詳細資訊，請參閱 [Linux VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="a5285-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="a5285-214">建立和連結磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-214">Create and attach disks</span></span>

<span data-ttu-id="a5285-215">可以建立資料磁碟，並將其附加到 VM 建立時或 tooan 現有 VM。</span><span class="sxs-lookup"><span data-stu-id="a5285-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="a5285-216">在建立 VM 時連結磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-216">Attach disk at VM creation</span></span>

<span data-ttu-id="a5285-217">建立資源群組以 hello [az 群組建立](https://docs.microsoft.com/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="a5285-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="a5285-218">建立 VM 使用 hello [az vm 建立]( /cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="a5285-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="a5285-219">hello`--datadisk-sizes-gb`引數是使用的 toospecify 應該建立額外的磁碟，並附加 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a5285-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="a5285-220">toocreate 和連接一個以上的磁碟，請使用空格分隔的磁碟大小值清單。</span><span class="sxs-lookup"><span data-stu-id="a5285-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="a5285-221">在下列範例的 hello，VM 會建立使用兩個資料磁碟時，這兩個 128 GB。</span><span class="sxs-lookup"><span data-stu-id="a5285-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="a5285-222">Hello 磁碟大小為 128 GB，因為這些磁碟都設定為 P10s，提供每個磁碟的最大 500 IOPS。</span><span class="sxs-lookup"><span data-stu-id="a5285-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="a5285-223">附加磁碟 tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="a5285-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="a5285-224">toocreate 並附加新磁碟 tooan 現有的虛擬機器，請使用 hello [az vm 磁碟附加](/cli/azure/vm/disk#attach)命令。</span><span class="sxs-lookup"><span data-stu-id="a5285-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="a5285-225">hello 下列範例會建立 premium 磁碟，128 gb 的大小，並將其附加的 toohello hello 最後一個步驟中建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="a5285-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="a5285-226">準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-226">Prepare data disks</span></span>

<span data-ttu-id="a5285-227">一旦磁碟已附加的 toohello 虛擬機器，必須設定 toobe toouse hello 磁碟 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="a5285-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="a5285-228">hello 下列範例顯示如何 toomanually 設定的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="a5285-229">使用 cloud-init (涵蓋於[稍後的教學課程](./tutorial-automate-vm-deployment.md)中) 也可以將此程序自動化。</span><span class="sxs-lookup"><span data-stu-id="a5285-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="a5285-230">手動設定</span><span class="sxs-lookup"><span data-stu-id="a5285-230">Manual configuration</span></span>

<span data-ttu-id="a5285-231">建立 SSH 連線與 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a5285-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="a5285-232">Hello hello 虛擬機器的公用 IP 取代 hello 範例 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a5285-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="a5285-233">分割磁碟 hello `fdisk`。</span><span class="sxs-lookup"><span data-stu-id="a5285-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="a5285-234">寫入檔案系統 toohello 磁碟分割使用 hello`mkfs`命令。</span><span class="sxs-lookup"><span data-stu-id="a5285-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="a5285-235">掛接 hello 新磁碟，使其在 hello 作業系統中存取。</span><span class="sxs-lookup"><span data-stu-id="a5285-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="a5285-236">hello 磁碟現在可以存取透過 hello *datadrive*掛接點，您可以藉由執行 hello 驗證`df -h`命令。</span><span class="sxs-lookup"><span data-stu-id="a5285-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="a5285-237">hello 輸出會顯示 hello 新磁碟機上有掛載*/datadrive*。</span><span class="sxs-lookup"><span data-stu-id="a5285-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="a5285-238">hello 磁碟機的 tooensure 會重新掛上重新開機後，必須將它加入 toohello */etc/hosts fstab*檔案。</span><span class="sxs-lookup"><span data-stu-id="a5285-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="a5285-239">開始以 hello hello 的 hello 磁碟 UUID 吧，toodo`blkid`公用程式。</span><span class="sxs-lookup"><span data-stu-id="a5285-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="a5285-240">hello 輸出會顯示 hello 的 hello 磁碟 UUID`/dev/sdc1`在此情況下。</span><span class="sxs-lookup"><span data-stu-id="a5285-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="a5285-241">新增下列 toohello 列類似 toohello */etc/hosts fstab*檔案。</span><span class="sxs-lookup"><span data-stu-id="a5285-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="a5285-242">也請注意，使用 barrier=0 可以停用寫入屏障，此組態可以改善磁碟效能。</span><span class="sxs-lookup"><span data-stu-id="a5285-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="a5285-243">既然 hello 磁碟已設定，關閉 hello SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="a5285-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="a5285-244">調整 VM 磁碟的大小</span><span class="sxs-lookup"><span data-stu-id="a5285-244">Resize VM disk</span></span>

<span data-ttu-id="a5285-245">一旦部署 VM 的大小可以增加 hello 作業系統磁碟或任何附加的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="a5285-246">當需要更多儲存空間或更高 （P10、 P20、 P30） 時，增加 hello 大小是磁碟的效能的有益的。</span><span class="sxs-lookup"><span data-stu-id="a5285-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="a5285-247">請注意，磁碟的大小不能減少。</span><span class="sxs-lookup"><span data-stu-id="a5285-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="a5285-248">增加磁碟大小，hello 識別碼前後需要 hello 磁碟的名稱。</span><span class="sxs-lookup"><span data-stu-id="a5285-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="a5285-249">使用 hello [az 磁碟清單](/cli/azure/vm/disk#list)命令 tooreturn 所有磁碟區在資源群組。</span><span class="sxs-lookup"><span data-stu-id="a5285-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="a5285-250">請注意 hello 磁碟名稱希望 tooresize。</span><span class="sxs-lookup"><span data-stu-id="a5285-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="a5285-251">hello VM 也必須已解除配置。</span><span class="sxs-lookup"><span data-stu-id="a5285-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="a5285-252">使用 hello [az vm 解除配置]( /cli/azure/vm#deallocate)命令 toostop 及取消配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a5285-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="a5285-253">使用 hello [az 磁碟更新](/cli/azure/vm/disk#update)命令 tooresize hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="a5285-254">此範例會調整大小的磁碟，名為*myDataDisk* too1 tb。</span><span class="sxs-lookup"><span data-stu-id="a5285-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="a5285-255">Hello 的調整大小作業完成後，請啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a5285-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="a5285-256">如果作業系統磁碟的 hello 調整大小時會自動展開 hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="a5285-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="a5285-257">如果您已調整大小的資料磁碟，任何目前的資料分割需要 toobe hello Vm 作業系統中，展開節點。</span><span class="sxs-lookup"><span data-stu-id="a5285-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="a5285-258">建立 Azure 磁碟快照集</span><span class="sxs-lookup"><span data-stu-id="a5285-258">Snapshot Azure disks</span></span>

<span data-ttu-id="a5285-259">取得磁碟的快照集建立 hello 磁碟的讀取，時間點複本。</span><span class="sxs-lookup"><span data-stu-id="a5285-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="a5285-260">Azure VM 的快照集可用於快速進行組態變更之前儲存 hello VM 的狀態。</span><span class="sxs-lookup"><span data-stu-id="a5285-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="a5285-261">在 hello 事件 hello 組態變更證明 toobe 討厭，可以使用 hello 快照還原 VM 狀態。</span><span class="sxs-lookup"><span data-stu-id="a5285-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="a5285-262">當 VM 有多個磁碟時，快照時每個磁碟與 hello 無關的其他人。</span><span class="sxs-lookup"><span data-stu-id="a5285-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="a5285-263">進行應用程式一致備份，請考慮在執行磁碟快照集之前停止 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a5285-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="a5285-264">或者，使用 hello [Azure 備份服務](/azure/backup/)，這可讓您 tooperform 自動化的 hello VM 正在執行時進行備份。</span><span class="sxs-lookup"><span data-stu-id="a5285-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="a5285-265">建立快照集</span><span class="sxs-lookup"><span data-stu-id="a5285-265">Create snapshot</span></span>

<span data-ttu-id="a5285-266">之前建立的虛擬機器磁碟的快照，hello 識別碼或名稱 hello 磁碟的需要。</span><span class="sxs-lookup"><span data-stu-id="a5285-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="a5285-267">使用 hello [az vm 顯示](https://docs.microsoft.com/en-us/cli/azure/vm#show)命令 tooreturn hello 磁碟識別碼。在此範例中，hello 磁碟識別碼儲存在變數，使其可以用於在稍後的步驟。</span><span class="sxs-lookup"><span data-stu-id="a5285-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="a5285-268">您已經有 hello 識別碼 hello 虛擬機器磁碟，hello 下列命令會建立 hello 磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="a5285-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="a5285-269">從快照集建立磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-269">Create disk from snapshot</span></span>

<span data-ttu-id="a5285-270">這個快照可轉換成使用的 toorecreate hello 虛擬機器磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="a5285-271">從快照集還原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a5285-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="a5285-272">刪除 hello 現有虛擬機器 toodemonstrate 虛擬機器復原。</span><span class="sxs-lookup"><span data-stu-id="a5285-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="a5285-273">建立新的虛擬機器從 hello 快照集磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="a5285-274">重新連結資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-274">Reattach data disk</span></span>

<span data-ttu-id="a5285-275">所有的資料磁碟都必須重新附加 toobe toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a5285-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="a5285-276">首先尋找 hello 資料磁碟名稱使用 hello [az 磁碟清單](https://docs.microsoft.com/cli/azure/disk#list)命令。</span><span class="sxs-lookup"><span data-stu-id="a5285-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="a5285-277">此範例中的位置 hello hello 磁碟中名為的變數名稱*datadisk*，hello 下一個步驟中所用。</span><span class="sxs-lookup"><span data-stu-id="a5285-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="a5285-278">使用 hello [az vm 磁碟附加](https://docs.microsoft.com/cli/azure/vm/disk#attach)命令 tooattach hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="a5285-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="a5285-279">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5285-279">Next steps</span></span>

<span data-ttu-id="a5285-280">在本教學課程中，您已了解 VM 磁碟的相關主題，像是：</span><span class="sxs-lookup"><span data-stu-id="a5285-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5285-281">OS 磁碟和暫存磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="a5285-282">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-282">Data disks</span></span>
> * <span data-ttu-id="a5285-283">標準和進階磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="a5285-284">磁碟效能</span><span class="sxs-lookup"><span data-stu-id="a5285-284">Disk performance</span></span>
> * <span data-ttu-id="a5285-285">連結及準備資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a5285-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="a5285-286">調整磁碟的大小</span><span class="sxs-lookup"><span data-stu-id="a5285-286">Resizing disks</span></span>
> * <span data-ttu-id="a5285-287">磁碟快照集</span><span class="sxs-lookup"><span data-stu-id="a5285-287">Disk snapshots</span></span>

<span data-ttu-id="a5285-288">前進 toohello 下一個教學課程的 toolearn 自動化 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="a5285-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a5285-289">自動設定 VM</span><span class="sxs-lookup"><span data-stu-id="a5285-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
