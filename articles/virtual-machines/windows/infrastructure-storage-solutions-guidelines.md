---
title: "Azure 中 Windows VM 的儲存體解決方案 | Microsoft Docs"
description: "了解適合用來在 Azure 基礎結構服務中部署儲存體解決方案的關鍵設計和實作指導方針。"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ba0d66c5af771ebcb3ca8e6742e15a5506d8fd61
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a><span data-ttu-id="9c93c-103">適用於 Windows VM 的 Azure 儲存體基礎結構指導方針</span><span class="sxs-lookup"><span data-stu-id="9c93c-103">Azure storage infrastructure guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="9c93c-104">本文著重於了解達成最佳虛擬機器 (VM) 效能的儲存體需求及設計考量。</span><span class="sxs-lookup"><span data-stu-id="9c93c-104">This article focuses on understanding storage needs and design considerations for achieving optimum virtual machine (VM) performance.</span></span>

## <a name="implementation-guidelines-for-storage"></a><span data-ttu-id="9c93c-105">儲存體的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="9c93c-105">Implementation guidelines for storage</span></span>
<span data-ttu-id="9c93c-106">决策：</span><span class="sxs-lookup"><span data-stu-id="9c93c-106">Decisions:</span></span>

* <span data-ttu-id="9c93c-107">您計劃使用 Azure 受控磁碟或非受控磁碟？</span><span class="sxs-lookup"><span data-stu-id="9c93c-107">Are you going to use Azure Managed Disks or unmanaged disks?</span></span>
* <span data-ttu-id="9c93c-108">您是否需要針對工作負載使用標準或進階儲存體？</span><span class="sxs-lookup"><span data-stu-id="9c93c-108">Do you need to use Standard or Premium storage for your workload?</span></span>
* <span data-ttu-id="9c93c-109">您是否需要進行磁碟等量以建立大於 4TB 的磁碟？</span><span class="sxs-lookup"><span data-stu-id="9c93c-109">Do you need disk striping to create disks larger than 4TB?</span></span>
* <span data-ttu-id="9c93c-110">您是否需要進行磁碟等量以獲得工作負載的最佳 I/O 效能？</span><span class="sxs-lookup"><span data-stu-id="9c93c-110">Do you need disk striping to achieve optimal I/O performance for your workload?</span></span>
* <span data-ttu-id="9c93c-111">您需要用來裝載 IT 工作負載或基礎結構的是哪種儲存體帳戶組合？</span><span class="sxs-lookup"><span data-stu-id="9c93c-111">What set of storage accounts do you need to host your IT workload or infrastructure?</span></span>

<span data-ttu-id="9c93c-112">工作：</span><span class="sxs-lookup"><span data-stu-id="9c93c-112">Tasks:</span></span>

* <span data-ttu-id="9c93c-113">檢閱您正在部署的應用程式 I/O 需求，並規劃適當的儲存體帳戶數目和類型。</span><span class="sxs-lookup"><span data-stu-id="9c93c-113">Review I/O demands of the applications you are deploying and plan the appropriate number and type of storage accounts.</span></span>
* <span data-ttu-id="9c93c-114">使用您的命名慣例來建立儲存體帳戶組合。</span><span class="sxs-lookup"><span data-stu-id="9c93c-114">Create the set of storage accounts using your naming convention.</span></span> <span data-ttu-id="9c93c-115">您可以使用 Azure PowerShell 或入口網站。</span><span class="sxs-lookup"><span data-stu-id="9c93c-115">You can use Azure PowerShell or the portal.</span></span>

## <a name="storage"></a><span data-ttu-id="9c93c-116">儲存體</span><span class="sxs-lookup"><span data-stu-id="9c93c-116">Storage</span></span>
<span data-ttu-id="9c93c-117">Azure 儲存體是部署和管理虛擬機器 (VM) 和應用程式的重要部分。</span><span class="sxs-lookup"><span data-stu-id="9c93c-117">Azure Storage is a key part of deploying and managing virtual machines (VMs) and applications.</span></span> <span data-ttu-id="9c93c-118">Azure 儲存體提供服務來儲存檔案資料、非結構化資料和訊息，同時也是支援 VM 的基礎結構的一部分。</span><span class="sxs-lookup"><span data-stu-id="9c93c-118">Azure Storage provides services for storing file data, unstructured data, and messages, and it is also part of the infrastructure supporting VMs.</span></span>

<span data-ttu-id="9c93c-119">[Azure 受控磁碟](../../storage/storage-managed-disks-overview.md)會在幕後為您管理儲存體。</span><span class="sxs-lookup"><span data-stu-id="9c93c-119">[Azure Managed Disks](../../storage/storage-managed-disks-overview.md) handles storage for you behind the scenes.</span></span> <span data-ttu-id="9c93c-120">利用非受控磁碟，您可以建立儲存體帳戶來保存 Azure VM 的磁碟 (VHD 檔案)。</span><span class="sxs-lookup"><span data-stu-id="9c93c-120">With unmanaged disks, you create storage accounts to hold the disks (VHD files) for your Azure VMs.</span></span> <span data-ttu-id="9c93c-121">相應增加時，您必須確定已建立其他儲存體帳戶，讓您不會超過任何磁碟的儲存體 IOPS 限制。</span><span class="sxs-lookup"><span data-stu-id="9c93c-121">When scaling up, you must make sure you created additional storage accounts so you don’t exceed the IOPS limit for storage with any of your disks.</span></span> <span data-ttu-id="9c93c-122">由於受控磁碟會處理儲存體，您不再受限於儲存體帳戶限制 (例如 20,000 IOPS / 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="9c93c-122">With Managed Disks handling storage, you are no longer limited by the storage account limits (such as 20,000 IOPS / account).</span></span> <span data-ttu-id="9c93c-123">您也不再需要將自訂映像 (VHD 檔案) 複製到多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c93c-123">You also no longer have to copy your custom images (VHD files) to multiple storage accounts.</span></span> <span data-ttu-id="9c93c-124">您可以集中管理它們 (每個 Azure 區域一個儲存體帳戶)，並利用它們在一個訂用帳戶中建立數百個 VM。</span><span class="sxs-lookup"><span data-stu-id="9c93c-124">You can manage them in a central location – one storage account per Azure region – and use them to create hundreds of VMs in a subscription.</span></span> <span data-ttu-id="9c93c-125">我們建議您針對新的部署使用受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="9c93c-125">We recommend you use Managed Disks for new deployments.</span></span>

<span data-ttu-id="9c93c-126">有兩種可供支援 VM 使用的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="9c93c-126">There are two types of storage accounts available for supporting VMs:</span></span>

* <span data-ttu-id="9c93c-127">標準儲存體帳戶讓您能夠存取 blob 儲存體 (用於存放 Azure VM 磁碟)、表格儲存體、佇列儲存體和檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="9c93c-127">Standard storage accounts give you access to blob storage (used for storing Azure VM disks), table storage, queue storage, and file storage.</span></span>
* <span data-ttu-id="9c93c-128">[進階儲存體](../../storage/storage-premium-storage.md) 帳戶可針對 I/O 密集的工作負載提供高效能且低延遲的磁碟支援 (例如 AlwaysOn 叢集中的 SQL Server)。</span><span class="sxs-lookup"><span data-stu-id="9c93c-128">[Premium storage](../../storage/storage-premium-storage.md) accounts deliver high-performance, low-latency disk support for I/O intensive workloads, such as SQL Servers in an AlwaysOn cluster.</span></span> <span data-ttu-id="9c93c-129">進階儲存體目前僅支援 Azure VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="9c93c-129">Premium storage currently supports Azure VM disks only.</span></span>

<span data-ttu-id="9c93c-130">Azure 會建立含有一個作業系統磁碟、一個暫存磁碟，以及零或多個選用資料磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="9c93c-130">Azure creates VMs with an operating system disk, a temporary disk, and zero or more optional data disks.</span></span> <span data-ttu-id="9c93c-131">作業系統磁碟和資料磁碟都是 Azure 頁面 Blob，而暫存磁碟會儲存在本機機器所在的節點上。</span><span class="sxs-lookup"><span data-stu-id="9c93c-131">The operating system disk and data disks are Azure page blobs, whereas the temporary disk is stored locally on the node where the machine lives.</span></span> <span data-ttu-id="9c93c-132">請注意，在設計應用程式時，請務必僅將此暫存磁碟用於非持續性資料上，因為 VM 可能會在維護事件期間於主機之間移轉。</span><span class="sxs-lookup"><span data-stu-id="9c93c-132">Take care when designing applications to only use this temporary disk for non-persistent data as the VM may be migrated between hosts during a maintenance event.</span></span> <span data-ttu-id="9c93c-133">任何儲存在暫存磁碟上的資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="9c93c-133">Any data stored on the temporary disk would be lost.</span></span>

<span data-ttu-id="9c93c-134">持久性和高可用性是由基礎 Azure 儲存體環境所提供，以確保您的資料能在發生非計畫性維護或硬體失敗時受到保護。</span><span class="sxs-lookup"><span data-stu-id="9c93c-134">Durability and high availability is provided by the underlying Azure Storage environment to ensure that your data remains protected against unplanned maintenance or hardware failures.</span></span> <span data-ttu-id="9c93c-135">設計您的 Azure 儲存體環境時，您可以選擇複寫 VM 儲存體：</span><span class="sxs-lookup"><span data-stu-id="9c93c-135">As you design your Azure Storage environment, you can choose to replicate VM storage:</span></span>

* <span data-ttu-id="9c93c-136">在指定 Azure 資料中心的本機上</span><span class="sxs-lookup"><span data-stu-id="9c93c-136">locally within a given Azure datacenter</span></span>
* <span data-ttu-id="9c93c-137">在指定區域內跨 Azure 資料中心</span><span class="sxs-lookup"><span data-stu-id="9c93c-137">across Azure datacenters within a given region</span></span>
* <span data-ttu-id="9c93c-138">跨不同區域內且跨 Azure 資料中心</span><span class="sxs-lookup"><span data-stu-id="9c93c-138">across Azure datacenters across different regions</span></span>

<span data-ttu-id="9c93c-139">您可以 [深入了解高可用性的複寫選項](../../storage/storage-introduction.md#replication-for-durability-and-high-availability)。</span><span class="sxs-lookup"><span data-stu-id="9c93c-139">You can read [more about the replication options for high availability](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).</span></span>

<span data-ttu-id="9c93c-140">作業系統磁碟和資料磁碟具有 4TB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="9c93c-140">Operating system disks and data disks have a maximum size of 4TB.</span></span> <span data-ttu-id="9c93c-141">您可以使用 Windows Server 2012 或更新版本中的「儲存空間」，匯集資料磁碟來提供大於 4TB 的邏輯磁碟區給 VM，以超越此限制。</span><span class="sxs-lookup"><span data-stu-id="9c93c-141">You can use Storage Spaces in Windows Server 2012 or later to surpass this limit by pooling together data disks to present logical volumes larger than 4TB to your VM.</span></span>

<span data-ttu-id="9c93c-142">設計 Azure 儲存體部署時有幾個延展性的限制 - 如需詳細資訊，請參閱 [Microsoft Azure 訂用帳戶和服務限制、配額與限制](../../azure-subscription-service-limits.md#storage-limits)。</span><span class="sxs-lookup"><span data-stu-id="9c93c-142">There are some scalability limits when designing your Azure Storage deployments - for more information, see [Microsoft Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="9c93c-143">另請參閱〈 [Azure 儲存體的延展性與效能目標](../../storage/storage-scalability-targets.md)〉。</span><span class="sxs-lookup"><span data-stu-id="9c93c-143">Also see [Azure storage scalability and performance targets](../../storage/storage-scalability-targets.md).</span></span>

<span data-ttu-id="9c93c-144">針對應用程式儲存體，您可以儲存非結構化的物件資料，例如文件、影像、備份、設定資料、記錄檔等等。</span><span class="sxs-lookup"><span data-stu-id="9c93c-144">For application storage, you can store unstructured object data such as documents, images, backups, configuration data, logs, etc.</span></span> <span data-ttu-id="9c93c-145">使用 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9c93c-145">using blob storage.</span></span> <span data-ttu-id="9c93c-146">與其讓您的應用程式寫入附加至 VM 的虛擬磁碟，該應用程式可以直接寫入 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9c93c-146">Rather than your application writing to a virtual disk attached to the VM, the application can write directly to Azure blob storage.</span></span> <span data-ttu-id="9c93c-147">根據您的可用性需求和成本限制，blob 儲存體也提供[經常性存取與非經常性存取儲存層](../../storage/storage-blob-storage-tiers.md)的選項。</span><span class="sxs-lookup"><span data-stu-id="9c93c-147">Blob storage also provides the option of [hot and cool storage tiers](../../storage/storage-blob-storage-tiers.md) depending on your availability needs and cost constraints.</span></span>

## <a name="striped-disks"></a><span data-ttu-id="9c93c-148">等量磁碟</span><span class="sxs-lookup"><span data-stu-id="9c93c-148">Striped disks</span></span>
<span data-ttu-id="9c93c-149">除了讓您能夠建立大於 4TB 的磁碟，在許多情況下，針對資料磁碟使用等量，可透過允許多個 Blob 備份單一磁碟區的儲存體來增強效能。</span><span class="sxs-lookup"><span data-stu-id="9c93c-149">Besides allowing you to create disks larger than 4TB, in many instances, using striping for data disks enhances performance by allowing multiple blobs to back the storage for a single volume.</span></span> <span data-ttu-id="9c93c-150">從單一邏輯磁碟寫入和讀取資料所需的 I/O 會透過等量速度以平行方式繼續進行。</span><span class="sxs-lookup"><span data-stu-id="9c93c-150">With striping, the I/O required to write and read data from a single logical disk proceeds in parallel.</span></span>

<span data-ttu-id="9c93c-151">根據 VM 的大小而定，Azure 會強制限制資料磁碟數量和可用的頻寬量。</span><span class="sxs-lookup"><span data-stu-id="9c93c-151">Azure imposes limits on the number of data disks and amount of bandwidth available, depending on the VM size.</span></span> <span data-ttu-id="9c93c-152">如需詳細資訊，請參閱[虛擬機器的大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="9c93c-152">For details, see [Sizes for virtual machines](sizes.md).</span></span>

<span data-ttu-id="9c93c-153">如果您針對 Azure 資料磁碟使用磁碟等量，請考量下列指導方針：</span><span class="sxs-lookup"><span data-stu-id="9c93c-153">If you are using disk striping for Azure data disks, consider the following guidelines:</span></span>

* <span data-ttu-id="9c93c-154">連接 VM 大小所允許的資料磁碟數目上限。</span><span class="sxs-lookup"><span data-stu-id="9c93c-154">Attach the maximum data disks allowed for the VM size.</span></span>
* <span data-ttu-id="9c93c-155">使用儲存空間。</span><span class="sxs-lookup"><span data-stu-id="9c93c-155">Use Storage Spaces.</span></span>
* <span data-ttu-id="9c93c-156">避免使用 Azure 資料磁碟快取選項 (快取原則 = 無)。</span><span class="sxs-lookup"><span data-stu-id="9c93c-156">Avoid using Azure data disk caching options (caching policy = None).</span></span>

<span data-ttu-id="9c93c-157">如需詳細資訊，請參閱〈 [儲存體空間 - 適用於效能的設計](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx)〉。</span><span class="sxs-lookup"><span data-stu-id="9c93c-157">For more information, see [Storage spaces - designing for performance](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).</span></span>

## <a name="multiple-storage-accounts"></a><span data-ttu-id="9c93c-158">多個儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="9c93c-158">Multiple storage accounts</span></span>
<span data-ttu-id="9c93c-159">本節不適用 [Azure 受控磁碟](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，因為您不會建立個別的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c93c-159">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create separate storage accounts.</span></span> 

<span data-ttu-id="9c93c-160">針對非受控磁碟設計您的 Azure 儲存體環境時，隨著您部署的 VM 數目增加，您可以善用多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c93c-160">When designing your Azure Storage environment for unmanaged disks, you can use multiple storage accounts as the number of VMs you deploy increases.</span></span> <span data-ttu-id="9c93c-161">這個方式可協助將 I/O 分散到基礎 Azure 儲存體基礎結構上，以維持 VM 和應用程式的最佳效能。</span><span class="sxs-lookup"><span data-stu-id="9c93c-161">This approach helps distribute out the I/O across the underlying Azure Storage infrastructure to maintain optimum performance for your VMs and applications.</span></span> <span data-ttu-id="9c93c-162">當您設計要部署的應用程式時，請考慮每個 VM 的 I/O 需求，並使那些 VM 在 Azure 儲存體帳戶之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="9c93c-162">As you design the applications that you are deploying, consider the I/O requirements each VM has and balance out those VMs across Azure Storage accounts.</span></span> <span data-ttu-id="9c93c-163">請盡量避免只將所有高 I/O 需求的 VM 分配到一個或兩個儲存體帳戶上。</span><span class="sxs-lookup"><span data-stu-id="9c93c-163">Try to avoid grouping all the high I/O demanding VMs in to just one or two storage accounts.</span></span>

<span data-ttu-id="9c93c-164">如需不同 Azure 儲存體選項的 I/O 功能以及一些建議最大值的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](../../storage/storage-scalability-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="9c93c-164">For more information about the I/O capabilities of the different Azure Storage options and some recommend maximums, see [Azure storage scalability and performance targets](../../storage/storage-scalability-targets.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c93c-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c93c-165">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

