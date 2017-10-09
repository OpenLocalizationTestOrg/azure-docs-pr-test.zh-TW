---
title: "aaaAzure 儲存體延展性和效能目標 |Microsoft 文件"
description: "Azure 儲存體，包括容量、 要求率，以及傳入和傳出的頻寬，這兩個標準和進階儲存體帳戶，以了解 hello 延展性和效能目標。 了解內的每個 hello Azure 儲存體服務的資料分割的效能目標。"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 98de116a01b64f3418808a5f626b6c70d8d432e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a><span data-ttu-id="78096-104">Azure 儲存體延展性和效能目標</span><span class="sxs-lookup"><span data-stu-id="78096-104">Azure Storage Scalability and Performance Targets</span></span>
## <a name="overview"></a><span data-ttu-id="78096-105">概觀</span><span class="sxs-lookup"><span data-stu-id="78096-105">Overview</span></span>
<span data-ttu-id="78096-106">本主題描述 Microsoft Azure 儲存體 hello 延展性和效能主題。</span><span class="sxs-lookup"><span data-stu-id="78096-106">This topic describes hello scalability and performance topics for Microsoft Azure Storage.</span></span> <span data-ttu-id="78096-107">如需其他 Azure 限制的摘要，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="78096-107">For a summary of other Azure limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

> [!NOTE]
> <span data-ttu-id="78096-108">所有儲存體帳戶 hello 新的平面網路拓撲上執行，而且支援下面所述，不論它們在何時建立 hello 延展性和效能目標。</span><span class="sxs-lookup"><span data-stu-id="78096-108">All storage accounts run on hello new flat network topology and support hello scalability and performance targets outlined below, regardless of when they were created.</span></span> <span data-ttu-id="78096-109">如需 hello Azure 儲存體平面網路架構及延展性的詳細資訊，請參閱[Microsoft Azure 儲存體： 高可用雲端儲存體服務具有強式一致性](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)。</span><span class="sxs-lookup"><span data-stu-id="78096-109">For more information on hello Azure Storage flat network architecture and on scalability, see [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>
> 
> [!IMPORTANT]
> <span data-ttu-id="78096-110">此處所列的 hello 延展性和效能目標是高階的目標，但是可達成。</span><span class="sxs-lookup"><span data-stu-id="78096-110">hello scalability and performance targets listed here are high-end targets, but are achievable.</span></span> <span data-ttu-id="78096-111">在所有情況下，hello 要求率和頻寬，方法是儲存體帳戶取決於儲存時，物件 hello 大小 hello 存取模式的使用率，並 hello 應用程式執行的工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="78096-111">In all cases, hello request rate and bandwidth achieved by your storage account depends upon hello size of objects stored, hello access patterns utilized, and hello type of workload your application performs.</span></span> <span data-ttu-id="78096-112">會確定 tootest 服務 toodetermine 無論其效能是某符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="78096-112">Be sure tootest your service toodetermine whether its performance meets your requirements.</span></span> <span data-ttu-id="78096-113">可能的話，請避免 hello 流量速率中的突然出現尖峰，並確保流量平均分散到資料分割。</span><span class="sxs-lookup"><span data-stu-id="78096-113">If possible, avoid sudden spikes in hello rate of traffic and ensure that traffic is well-distributed across partitions.</span></span>
> 
> <span data-ttu-id="78096-114">當您的應用程式達到 hello 限制的資料分割可以處理您的工作負載時，Azure 儲存體將會開始 tooreturn 錯誤碼 503 （伺服器忙碌） 或錯誤碼 500 （作業逾時） 回應。</span><span class="sxs-lookup"><span data-stu-id="78096-114">When your application reaches hello limit of what a partition can handle for your workload, Azure Storage will begin tooreturn error code 503 (Server Busy) or error code 500 (Operation Timeout) responses.</span></span> <span data-ttu-id="78096-115">當發生這種情況時，hello 應用程式應該使用指數輪詢原則的重試。</span><span class="sxs-lookup"><span data-stu-id="78096-115">When this occurs, hello application should use an exponential backoff policy for retries.</span></span> <span data-ttu-id="78096-116">hello 指數型輪詢允許流量 toothat 資料分割中的 hello hello 分割 toodecrease 及 tooease 出尖峰負載。</span><span class="sxs-lookup"><span data-stu-id="78096-116">hello exponential backoff allows hello load on hello partition toodecrease, and tooease out spikes in traffic toothat partition.</span></span>
> 
> 

<span data-ttu-id="78096-117">如果 hello 應用程式需要超過 hello 延展性目標的單一儲存體帳戶，您可以建置應用程式 toouse 多個儲存體帳戶，並這些儲存體帳戶間分割您的資料物件。</span><span class="sxs-lookup"><span data-stu-id="78096-117">If hello needs of your application exceed hello scalability targets of a single storage account, you can build your application toouse multiple storage accounts, and partition your data objects across those storage accounts.</span></span> <span data-ttu-id="78096-118">如需批量價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/) 。</span><span class="sxs-lookup"><span data-stu-id="78096-118">See [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/) for information on volume pricing.</span></span>

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a><span data-ttu-id="78096-119">Blob、佇列、資料表和檔案的延展性目標</span><span class="sxs-lookup"><span data-stu-id="78096-119">Scalability targets for blobs, queues, tables, and files</span></span>
[!INCLUDE [azure-storage-limits](../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a><span data-ttu-id="78096-120">虛擬機器磁碟的延展性目標</span><span class="sxs-lookup"><span data-stu-id="78096-120">Scalability targets for virtual machine disks</span></span>
[!INCLUDE [azure-storage-limits-vm-disks](../../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="78096-121">如需詳細資訊，請參閱 [Windows VM 大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或 [Linux VM 大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="78096-121">See [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

## <a name="managed-virtual-machine-disks"></a><span data-ttu-id="78096-122">受管理的虛擬機器磁碟</span><span class="sxs-lookup"><span data-stu-id="78096-122">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="78096-123">未受管理的虛擬機器磁碟</span><span class="sxs-lookup"><span data-stu-id="78096-123">Unmanaged virtual machine disks</span></span>
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a><span data-ttu-id="78096-124">Azure Resource Manager 的延展性目標</span><span class="sxs-lookup"><span data-stu-id="78096-124">Scalability targets for Azure resource manager</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a><span data-ttu-id="78096-125">Azure 儲存體中的分割</span><span class="sxs-lookup"><span data-stu-id="78096-125">Partitions in Azure Storage</span></span>
<span data-ttu-id="78096-126">保存資料儲存在 Azure 儲存體 （blob、 訊息、 實體和檔案） 中的每個物件所屬 tooa 分割，並由資料分割索引鍵識別。</span><span class="sxs-lookup"><span data-stu-id="78096-126">Every object that holds data that is stored in Azure Storage (blobs, messages, entities, and files) belongs tooa partition, and is identified by a partition key.</span></span> <span data-ttu-id="78096-127">hello 資料分割可決定如何 Azure 儲存體進行負載平衡的 blob、 訊息、 實體和檔案跨伺服器 toomeet hello 傳輸需要這些物件。</span><span class="sxs-lookup"><span data-stu-id="78096-127">hello partition determines how Azure Storage load balances blobs, messages, entities, and files across servers toomeet hello traffic needs of those objects.</span></span> <span data-ttu-id="78096-128">hello 資料分割索引鍵是唯一的且使用的 toolocate blob、 訊息或實體。</span><span class="sxs-lookup"><span data-stu-id="78096-128">hello partition key is unique and is used toolocate a blob, message, or entity.</span></span>

<span data-ttu-id="78096-129">在上面顯示的 hello 資料表[標準儲存體帳戶的延展性目標](#standard-storage-accounts)清單 hello 每個服務的單一資料分割的效能目標。</span><span class="sxs-lookup"><span data-stu-id="78096-129">hello table shown above in [Scalability Targets for Standard Storage Accounts](#standard-storage-accounts) lists hello performance targets for a single partition for each service.</span></span>

<span data-ttu-id="78096-130">資料分割會影響 hello hello 下列方式中的儲存體服務的每個負載平衡和延展性：</span><span class="sxs-lookup"><span data-stu-id="78096-130">Partitions affect load balancing and scalability for each of hello storage services in hello following ways:</span></span>

* <span data-ttu-id="78096-131">**Blob**: hello blob 的資料分割索引鍵是帳戶名稱 + 容器名稱 + blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="78096-131">**Blobs**: hello partition key for a blob is account name + container name + blob name.</span></span> <span data-ttu-id="78096-132">這表示如果 hello blob 上的負載需要它的每個 blob 可以有自己的資料分割。</span><span class="sxs-lookup"><span data-stu-id="78096-132">This means that each blob can have its own partition if load on hello blob demands it.</span></span> <span data-ttu-id="78096-133">Blob 可以分散安裝在存取 toothem 出順序 tooscale 中許多伺服器，但只可由單一伺服器提供單一 blob。</span><span class="sxs-lookup"><span data-stu-id="78096-133">Blobs can be distributed across many servers in order tooscale out access toothem, but a single blob can only be served by a single server.</span></span> <span data-ttu-id="78096-134">雖然 Blog 可以在 Blog 容器中邏輯分組，但這種分組方式的意涵卻非分割。</span><span class="sxs-lookup"><span data-stu-id="78096-134">While blobs can be logically grouped in blob containers, there are no partitioning implications from this grouping.</span></span>
* <span data-ttu-id="78096-135">**檔案**: hello 檔案的資料分割索引鍵是帳戶名稱 + 檔案共用名稱。</span><span class="sxs-lookup"><span data-stu-id="78096-135">**Files**: hello partition key for a file is account name + file share name.</span></span> <span data-ttu-id="78096-136">這表示檔案共用中的所有檔案也都位於單一分割區中。</span><span class="sxs-lookup"><span data-stu-id="78096-136">This means all files in a file share are also in a single partition.</span></span>
* <span data-ttu-id="78096-137">**訊息**: hello 訊息的資料分割索引鍵並 hello 帳戶名稱 + 佇列名稱，因此佇列中的所有訊息會分組成單一資料分割，會由單一伺服器。</span><span class="sxs-lookup"><span data-stu-id="78096-137">**Messages**: hello partition key for a message is hello account name + queue name, so all messages in a queue are grouped into a single partition and are served by a single server.</span></span> <span data-ttu-id="78096-138">可能由不同的伺服器，但是儲存體帳戶可能有許多佇列 toobalance hello 載入處理不同的佇列。</span><span class="sxs-lookup"><span data-stu-id="78096-138">Different queues may be processed by different servers toobalance hello load for however many queues a storage account may have.</span></span>
* <span data-ttu-id="78096-139">**實體**: hello 實體的資料分割索引鍵是帳戶名稱 + 資料表名稱 + 資料分割索引鍵，其中 hello 資料分割索引鍵是所需的 hello hello 值使用者定義**PartitionKey** hello 實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="78096-139">**Entities**: hello partition key for an entity is account name + table name + partition key, where hello partition key is hello value of hello required user-defined **PartitionKey** property for hello entity.</span></span> <span data-ttu-id="78096-140">以相同的資料分割索引鍵的值分組到相同資料分割，且會由 hello 相同的 hello hello 的所有實體都分割伺服器。</span><span class="sxs-lookup"><span data-stu-id="78096-140">All entities with hello same partition key value are grouped into hello same partition and are served by hello same partition server.</span></span> <span data-ttu-id="78096-141">這是重要的點 toounderstand 設計您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="78096-141">This is an important point toounderstand in designing your application.</span></span> <span data-ttu-id="78096-142">您的應用程式應該 hello 延展性的優勢散佈跨多個資料分割的實體群組於單一資料分割的 hello 資料存取優點與實體之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="78096-142">Your application should balance hello scalability benefits of spreading entities across multiple partitions with hello data access advantages of grouping entities in a single partition.</span></span>  

<span data-ttu-id="78096-143">主要優點 toogrouping 至單一資料分割的資料表中的實體集是的 hello 相同資料分割，因為在單一伺服器上存在的資料分割中的實體為可能 tooperform 不可部分完成的批次作業。</span><span class="sxs-lookup"><span data-stu-id="78096-143">A key advantage toogrouping a set of entities in a table into a single partition is that it's possible tooperform atomic batch operations across entities in hello same partition, since a partition exists on a single server.</span></span> <span data-ttu-id="78096-144">因此，如果您想 tooperform 批次作業上的實體群組，請考慮群組它們文件以 hello 相同的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="78096-144">Therefore, if you wish tooperform batch operations on a group of entities, consider grouping them with hello same partition key.</span></span> 

<span data-ttu-id="78096-145">在 hello 另一方面，hello 相同資料表，但有不同的資料分割索引鍵中的實體可以進行負載平衡到不同的伺服器，因此可能 toohave 較大的延展性。</span><span class="sxs-lookup"><span data-stu-id="78096-145">On hello other hand, entities that are in hello same table but have different partition keys can be load balanced across different servers, making it possible toohave greater scalability.</span></span>

<span data-ttu-id="78096-146">[這裡](https://msdn.microsoft.com/library/azure/hh508997.aspx)可以找到設計資料表分割策略的詳細建議。</span><span class="sxs-lookup"><span data-stu-id="78096-146">Detailed recommendations for designing partitioning strategy for tables can be found [here](https://msdn.microsoft.com/library/azure/hh508997.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="78096-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="78096-147">See Also</span></span>
* [<span data-ttu-id="78096-148">儲存體定價詳細資料</span><span class="sxs-lookup"><span data-stu-id="78096-148">Storage Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/storage/)
* [<span data-ttu-id="78096-149">Azure 訂用帳戶和服務限制、配額與限制</span><span class="sxs-lookup"><span data-stu-id="78096-149">Azure Subscription and Service Limits, Quotas, and Constraints</span></span>](../azure-subscription-service-limits.md)
* [<span data-ttu-id="78096-150">Premium 儲存體：Azure 虛擬機器工作負載適用的高效能儲存體</span><span class="sxs-lookup"><span data-stu-id="78096-150">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)
* [<span data-ttu-id="78096-151">Azure 儲存體複寫</span><span class="sxs-lookup"><span data-stu-id="78096-151">Azure Storage Replication</span></span>](storage-redundancy.md)
* [<span data-ttu-id="78096-152">Microsoft Azure 儲存體效能與延展性檢查清單</span><span class="sxs-lookup"><span data-stu-id="78096-152">Microsoft Azure Storage Performance and Scalability Checklist</span></span>](storage-performance-checklist.md)
* [<span data-ttu-id="78096-153">Microsoft Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="78096-153">Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

