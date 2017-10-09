---
title: "適用於 Windows Vm 在 Azure 中的 aaaStorage 解決方案 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作部署的指導方針 Azure 基礎結構服務中的儲存解決方案。"
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
ms.openlocfilehash: 57c27a7305964a56e6b2d1e73dee8e7da19fa8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a><span data-ttu-id="45ee5-103">適用於 Windows VM 的 Azure 儲存體基礎結構指導方針</span><span class="sxs-lookup"><span data-stu-id="45ee5-103">Azure storage infrastructure guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="45ee5-104">本文著重於了解達成最佳虛擬機器 (VM) 效能的儲存體需求及設計考量。</span><span class="sxs-lookup"><span data-stu-id="45ee5-104">This article focuses on understanding storage needs and design considerations for achieving optimum virtual machine (VM) performance.</span></span>

## <a name="implementation-guidelines-for-storage"></a><span data-ttu-id="45ee5-105">儲存體的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="45ee5-105">Implementation guidelines for storage</span></span>
<span data-ttu-id="45ee5-106">决策：</span><span class="sxs-lookup"><span data-stu-id="45ee5-106">Decisions:</span></span>

* <span data-ttu-id="45ee5-107">您將要 toouse Azure 受管理的磁碟或未受管理的磁碟嗎？</span><span class="sxs-lookup"><span data-stu-id="45ee5-107">Are you going toouse Azure Managed Disks or unmanaged disks?</span></span>
* <span data-ttu-id="45ee5-108">您是否有您的工作負載需要 toouse Standard 或 Premium 儲存體？</span><span class="sxs-lookup"><span data-stu-id="45ee5-108">Do you need toouse Standard or Premium storage for your workload?</span></span>
* <span data-ttu-id="45ee5-109">您是否需要磁碟條狀配置 toocreate 磁碟超過 4 TB？</span><span class="sxs-lookup"><span data-stu-id="45ee5-109">Do you need disk striping toocreate disks larger than 4TB?</span></span>
* <span data-ttu-id="45ee5-110">您是否有您的工作負載需要磁碟條狀配置 tooachieve 最佳 I/O 效能？</span><span class="sxs-lookup"><span data-stu-id="45ee5-110">Do you need disk striping tooachieve optimal I/O performance for your workload?</span></span>
* <span data-ttu-id="45ee5-111">哪些設定的儲存體帳戶是否需要 toohost 您的 IT 工作負載或基礎結構？</span><span class="sxs-lookup"><span data-stu-id="45ee5-111">What set of storage accounts do you need toohost your IT workload or infrastructure?</span></span>

<span data-ttu-id="45ee5-112">工作：</span><span class="sxs-lookup"><span data-stu-id="45ee5-112">Tasks:</span></span>

* <span data-ttu-id="45ee5-113">檢查 I/O 要求的 hello 應用程式部署，並規劃 hello 適當數目和類型的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ee5-113">Review I/O demands of hello applications you are deploying and plan hello appropriate number and type of storage accounts.</span></span>
* <span data-ttu-id="45ee5-114">建立儲存體帳戶使用您的命名慣例 hello 組。</span><span class="sxs-lookup"><span data-stu-id="45ee5-114">Create hello set of storage accounts using your naming convention.</span></span> <span data-ttu-id="45ee5-115">您可以使用 Azure PowerShell 或 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="45ee5-115">You can use Azure PowerShell or hello portal.</span></span>

## <a name="storage"></a><span data-ttu-id="45ee5-116">儲存體</span><span class="sxs-lookup"><span data-stu-id="45ee5-116">Storage</span></span>
<span data-ttu-id="45ee5-117">Azure 儲存體是部署和管理虛擬機器 (VM) 和應用程式的重要部分。</span><span class="sxs-lookup"><span data-stu-id="45ee5-117">Azure Storage is a key part of deploying and managing virtual machines (VMs) and applications.</span></span> <span data-ttu-id="45ee5-118">Azure 儲存體提供服務，用於儲存檔案資料、 非結構化的資料，以及訊息，而且它也支援 Vm 的 hello 基礎結構的一部分。</span><span class="sxs-lookup"><span data-stu-id="45ee5-118">Azure Storage provides services for storing file data, unstructured data, and messages, and it is also part of hello infrastructure supporting VMs.</span></span>

<span data-ttu-id="45ee5-119">[受管理的 azure 磁碟](../../storage/storage-managed-disks-overview.md)hello 幕後為您處理儲存體。</span><span class="sxs-lookup"><span data-stu-id="45ee5-119">[Azure Managed Disks](../../storage/storage-managed-disks-overview.md) handles storage for you behind hello scenes.</span></span> <span data-ttu-id="45ee5-120">使用 unmanaged 磁碟時，您建立儲存體帳戶 toohold hello 磁碟 （VHD 檔案） 為您的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="45ee5-120">With unmanaged disks, you create storage accounts toohold hello disks (VHD files) for your Azure VMs.</span></span> <span data-ttu-id="45ee5-121">當向上擴充，您必須確定您沒有任何磁碟超過儲存體的 hello IOPS 限制，因此，建立額外的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ee5-121">When scaling up, you must make sure you created additional storage accounts so you don’t exceed hello IOPS limit for storage with any of your disks.</span></span> <span data-ttu-id="45ee5-122">使用受管理磁碟時處理儲存體，您都不會再受到 hello 儲存體帳戶限制 (例如 20000 IOPS / 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="45ee5-122">With Managed Disks handling storage, you are no longer limited by hello storage account limits (such as 20,000 IOPS / account).</span></span> <span data-ttu-id="45ee5-123">您也不再有 toocopy 您自訂映像 （VHD 檔案） toomultiple 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ee5-123">You also no longer have toocopy your custom images (VHD files) toomultiple storage accounts.</span></span> <span data-ttu-id="45ee5-124">您可以在中央位置 – 一個儲存體帳戶每個 Azure 區域 – 中管理它們，並用 toocreate 數百個 Vm 的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="45ee5-124">You can manage them in a central location – one storage account per Azure region – and use them toocreate hundreds of VMs in a subscription.</span></span> <span data-ttu-id="45ee5-125">我們建議您針對新的部署使用受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="45ee5-125">We recommend you use Managed Disks for new deployments.</span></span>

<span data-ttu-id="45ee5-126">有兩種可供支援 VM 使用的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="45ee5-126">There are two types of storage accounts available for supporting VMs:</span></span>

* <span data-ttu-id="45ee5-127">標準儲存體帳戶提供您存取 tooblob （用來儲存 Azure VM 磁碟） 的儲存體，資料表儲存體，佇列儲存體和檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="45ee5-127">Standard storage accounts give you access tooblob storage (used for storing Azure VM disks), table storage, queue storage, and file storage.</span></span>
* <span data-ttu-id="45ee5-128">[進階儲存體](../../storage/storage-premium-storage.md) 帳戶可針對 I/O 密集的工作負載提供高效能且低延遲的磁碟支援 (例如 AlwaysOn 叢集中的 SQL Server)。</span><span class="sxs-lookup"><span data-stu-id="45ee5-128">[Premium storage](../../storage/storage-premium-storage.md) accounts deliver high-performance, low-latency disk support for I/O intensive workloads, such as SQL Servers in an AlwaysOn cluster.</span></span> <span data-ttu-id="45ee5-129">進階儲存體目前僅支援 Azure VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="45ee5-129">Premium storage currently supports Azure VM disks only.</span></span>

<span data-ttu-id="45ee5-130">Azure 會建立含有一個作業系統磁碟、一個暫存磁碟，以及零或多個選用資料磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="45ee5-130">Azure creates VMs with an operating system disk, a temporary disk, and zero or more optional data disks.</span></span> <span data-ttu-id="45ee5-131">hello 作業系統磁碟和資料磁碟會 Azure 分頁 blob，而 hello 暫存磁碟儲存在本機上 hello hello 機器所在的節點中。</span><span class="sxs-lookup"><span data-stu-id="45ee5-131">hello operating system disk and data disks are Azure page blobs, whereas hello temporary disk is stored locally on hello node where hello machine lives.</span></span> <span data-ttu-id="45ee5-132">請小心設計 tooonly 作為此暫存磁碟的非永續性資料 hello VM 可能會維護事件期間的主機之間移轉應用程式時。</span><span class="sxs-lookup"><span data-stu-id="45ee5-132">Take care when designing applications tooonly use this temporary disk for non-persistent data as hello VM may be migrated between hosts during a maintenance event.</span></span> <span data-ttu-id="45ee5-133">Hello 暫存磁碟上儲存的任何資料將會遺失。</span><span class="sxs-lookup"><span data-stu-id="45ee5-133">Any data stored on hello temporary disk would be lost.</span></span>

<span data-ttu-id="45ee5-134">持續性和高可用性是由提供 hello 基礎的 Azure 儲存體環境 tooensure 您資料會保持保護以防止未規劃的維護或硬體失敗。</span><span class="sxs-lookup"><span data-stu-id="45ee5-134">Durability and high availability is provided by hello underlying Azure Storage environment tooensure that your data remains protected against unplanned maintenance or hardware failures.</span></span> <span data-ttu-id="45ee5-135">當您設計您的 Azure 儲存體環境，您可以選擇 tooreplicate VM 儲存體：</span><span class="sxs-lookup"><span data-stu-id="45ee5-135">As you design your Azure Storage environment, you can choose tooreplicate VM storage:</span></span>

* <span data-ttu-id="45ee5-136">在指定 Azure 資料中心的本機上</span><span class="sxs-lookup"><span data-stu-id="45ee5-136">locally within a given Azure datacenter</span></span>
* <span data-ttu-id="45ee5-137">在指定區域內跨 Azure 資料中心</span><span class="sxs-lookup"><span data-stu-id="45ee5-137">across Azure datacenters within a given region</span></span>
* <span data-ttu-id="45ee5-138">跨不同區域內且跨 Azure 資料中心</span><span class="sxs-lookup"><span data-stu-id="45ee5-138">across Azure datacenters across different regions</span></span>

<span data-ttu-id="45ee5-139">您可以閱讀[更多關於高可用性的 hello 複寫選項](../../storage/storage-introduction.md#replication-for-durability-and-high-availability)。</span><span class="sxs-lookup"><span data-stu-id="45ee5-139">You can read [more about hello replication options for high availability](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).</span></span>

<span data-ttu-id="45ee5-140">作業系統磁碟和資料磁碟具有 4TB 的大小上限。</span><span class="sxs-lookup"><span data-stu-id="45ee5-140">Operating system disks and data disks have a maximum size of 4TB.</span></span> <span data-ttu-id="45ee5-141">您可以一起共用的資料磁碟 toopresent 邏輯磁碟區大於 4 TB tooyour VM 所使用儲存空間的 Windows Server 2012 或更新版本的 toosurpass 這項限制。</span><span class="sxs-lookup"><span data-stu-id="45ee5-141">You can use Storage Spaces in Windows Server 2012 or later toosurpass this limit by pooling together data disks toopresent logical volumes larger than 4TB tooyour VM.</span></span>

<span data-ttu-id="45ee5-142">設計 Azure 儲存體部署時有幾個延展性的限制 - 如需詳細資訊，請參閱 [Microsoft Azure 訂用帳戶和服務限制、配額與限制](../../azure-subscription-service-limits.md#storage-limits)。</span><span class="sxs-lookup"><span data-stu-id="45ee5-142">There are some scalability limits when designing your Azure Storage deployments - for more information, see [Microsoft Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="45ee5-143">另請參閱〈 [Azure 儲存體的延展性與效能目標](../../storage/storage-scalability-targets.md)〉。</span><span class="sxs-lookup"><span data-stu-id="45ee5-143">Also see [Azure storage scalability and performance targets](../../storage/storage-scalability-targets.md).</span></span>

<span data-ttu-id="45ee5-144">針對應用程式儲存體，您可以儲存非結構化的物件資料，例如文件、影像、備份、設定資料、記錄檔等等。</span><span class="sxs-lookup"><span data-stu-id="45ee5-144">For application storage, you can store unstructured object data such as documents, images, backups, configuration data, logs, etc.</span></span> <span data-ttu-id="45ee5-145">使用 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="45ee5-145">using blob storage.</span></span> <span data-ttu-id="45ee5-146">而不是您的應用程式撰寫 tooa 連接的虛擬磁碟 toohello VM hello 應用程式可以直接寫入 tooAzure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="45ee5-146">Rather than your application writing tooa virtual disk attached toohello VM, hello application can write directly tooAzure blob storage.</span></span> <span data-ttu-id="45ee5-147">Blob 儲存體也會提供 hello 選項[熱和冷卻儲存層](../../storage/storage-blob-storage-tiers.md)視您的可用性需求和成本條件約束。</span><span class="sxs-lookup"><span data-stu-id="45ee5-147">Blob storage also provides hello option of [hot and cool storage tiers](../../storage/storage-blob-storage-tiers.md) depending on your availability needs and cost constraints.</span></span>

## <a name="striped-disks"></a><span data-ttu-id="45ee5-148">等量磁碟</span><span class="sxs-lookup"><span data-stu-id="45ee5-148">Striped disks</span></span>
<span data-ttu-id="45ee5-149">除了可讓您 toocreate 磁碟超過 4 TB，在許多情況下，使用針對資料磁碟條狀配置可提高效能，藉由允許多個 blob tooback hello 儲存體的單一磁碟區。</span><span class="sxs-lookup"><span data-stu-id="45ee5-149">Besides allowing you toocreate disks larger than 4TB, in many instances, using striping for data disks enhances performance by allowing multiple blobs tooback hello storage for a single volume.</span></span> <span data-ttu-id="45ee5-150">使用等量，hello I/O 需要 toowrite，然後從單一的邏輯磁碟讀取的資料進行以平行方式。</span><span class="sxs-lookup"><span data-stu-id="45ee5-150">With striping, hello I/O required toowrite and read data from a single logical disk proceeds in parallel.</span></span>

<span data-ttu-id="45ee5-151">Azure 會加諸限制 hello 資料磁碟數目和 hello VM 大小而定，可用的頻寬量。</span><span class="sxs-lookup"><span data-stu-id="45ee5-151">Azure imposes limits on hello number of data disks and amount of bandwidth available, depending on hello VM size.</span></span> <span data-ttu-id="45ee5-152">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="45ee5-152">For details, see [Sizes for virtual machines](sizes.md).</span></span>

<span data-ttu-id="45ee5-153">如果您使用 Azure 資料磁碟的磁碟條狀配置，請考慮下列指導方針的 hello:</span><span class="sxs-lookup"><span data-stu-id="45ee5-153">If you are using disk striping for Azure data disks, consider hello following guidelines:</span></span>

* <span data-ttu-id="45ee5-154">附加 hello hello VM 大小所允許的最大的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="45ee5-154">Attach hello maximum data disks allowed for hello VM size.</span></span>
* <span data-ttu-id="45ee5-155">使用儲存空間。</span><span class="sxs-lookup"><span data-stu-id="45ee5-155">Use Storage Spaces.</span></span>
* <span data-ttu-id="45ee5-156">避免使用 Azure 資料磁碟快取選項 (快取原則 = 無)。</span><span class="sxs-lookup"><span data-stu-id="45ee5-156">Avoid using Azure data disk caching options (caching policy = None).</span></span>

<span data-ttu-id="45ee5-157">如需詳細資訊，請參閱〈 [儲存體空間 - 適用於效能的設計](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx)〉。</span><span class="sxs-lookup"><span data-stu-id="45ee5-157">For more information, see [Storage spaces - designing for performance](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).</span></span>

## <a name="multiple-storage-accounts"></a><span data-ttu-id="45ee5-158">多個儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="45ee5-158">Multiple storage accounts</span></span>
<span data-ttu-id="45ee5-159">本節不適太[Azure 受管理磁碟](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，因為您不會建立個別的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ee5-159">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create separate storage accounts.</span></span> 

<span data-ttu-id="45ee5-160">在設計您的 Azure 儲存體環境未受管理的磁碟時，您可以使用多個儲存體帳戶做為 Vm 的 hello 數部署會增加。</span><span class="sxs-lookup"><span data-stu-id="45ee5-160">When designing your Azure Storage environment for unmanaged disks, you can use multiple storage accounts as hello number of VMs you deploy increases.</span></span> <span data-ttu-id="45ee5-161">這種方式有助於分散出 hello I/O 跨 hello 基礎 Azure 儲存體基礎結構 toomaintain 最佳效能的 Vm 和應用程式。</span><span class="sxs-lookup"><span data-stu-id="45ee5-161">This approach helps distribute out hello I/O across hello underlying Azure Storage infrastructure toomaintain optimum performance for your VMs and applications.</span></span> <span data-ttu-id="45ee5-162">當您設計要部署的 hello 應用程式，請考慮 hello I/O 的需求，每個 VM 並平衡這些 Vm 出跨 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="45ee5-162">As you design hello applications that you are deploying, consider hello I/O requirements each VM has and balance out those VMs across Azure Storage accounts.</span></span> <span data-ttu-id="45ee5-163">分組所有 Vm 要求 (demand) toojust 一或兩個儲存體帳戶中的 hello 高 I/O tooavoid 再試一次。</span><span class="sxs-lookup"><span data-stu-id="45ee5-163">Try tooavoid grouping all hello high I/O demanding VMs in toojust one or two storage accounts.</span></span>

<span data-ttu-id="45ee5-164">如需 hello I/O 功能 hello 不同的 Azure 儲存體選項的詳細資訊，以及一些建議的最大值，請參閱 < [Azure 儲存體延展性和效能目標](../../storage/storage-scalability-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="45ee5-164">For more information about hello I/O capabilities of hello different Azure Storage options and some recommend maximums, see [Azure storage scalability and performance targets](../../storage/storage-scalability-targets.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45ee5-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45ee5-165">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

